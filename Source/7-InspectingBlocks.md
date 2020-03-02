## Prerequisites:
```
npm install web3
```


Inspecting blocks on the blockchain using the following web3.js methods;
`getBlockNumber` - returns the actual latest block,
`getBlock` - we can pass block hash or block number to get information.


```
const Web3 = require('web3')
const web3 = new Web3('https://mainnet.infura.io/v3/74e7531425ca4e4bb400cb891852d190')

// Latest block number
web3.eth.getBlockNumber().then(console.log)

// Latest block details
web3.eth.getBlock('latest').then(console.log) // All details of the block

web3.eth.getBlock('latest').then((block) => {
  console.log(block.hash) // Return the hash of the latest block
})

// Details of a particular block (using number of hash)
web3.eth.getBlock('9592249').then((block) => {
  console.log({
    blockHash: block.hash,
    blockNumber: block.number
  }) // Return the hash and number of the block
})

// Get 10 latest blocks
web3.eth.getBlockNumber().then((latest) => {
  for(let i = 0; i < 10; i++){
    web3.eth.getBlock(latest - 1).then((block) => {
      console.log({
        blockHash: block.hash,
        blockNumber: block.number
      })
    })
  }
})

// Get number of transactions in latest block
web3.eth.getBlockTransactionCount('latest').then(console.log)
```
