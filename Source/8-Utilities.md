## Prerequisites:
```
npm install web3
```

The following are some extra utilities available in the **web3.js** library;


```
const Web3 = require('web3')
const web3 = new Web3('https://mainnet.infura.io/hqRzEqFKv6IsjRxfVUWH')

// Get average gas price in wei from last few blocks median gas price
web3.eth.getGasPrice().then((result) => {
  console.log(web3.utils.fromWei(result, 'ether')
})

// Use sha256 Hashing function
console.log(web3.utils.sha3('Dapp University'))

// Use keccak256 Hashing function (alias)
console.log(web3.utils.keccak256('Dapp University'))

// Get a Random Hex
console.log(web3.utils.randomHex(32)) // Here 32 is the length of the required hex

// Get access to the underscore JS library - a collection of useful functions
const _ = web3.utils._

_.each({ key1: 'value1', key2: 'value2' }, (value, key) => {
  console.log(key)
})
```
