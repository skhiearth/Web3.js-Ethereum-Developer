## Prerequisites:
```
npm install web3
npm install ethereumjs-tx
```


Anything that writes data to the Ethereum blockchain triggers a **transaction**,
which costs a gas, and it changes the state of the blockchain. e.g., sending ether,
calling a Smart Contract function, deploying a smart contract etc.

```
const Web3 = require('web3')
const web3 = new Web3('HTTP://127.0.0.1:7545')

const account1 = '0x3f53c658065C5918fA2edBe39F22806D30b2c57a'
const account2 = '0x996B74C311F2633aF4ACEeB0e8511C496C7441F8'

web3.eth.getBalance(account1, (err, result) => {
  console.log(result)
})

// Send ether from one account to another
web3.eth.sendTransaction({
  from: account1,
  to: account2,
  value: web3.utils.toWei('1', 'ether')
})

// Check new balance - decreased balance in account 1 and increased balance in account 2
web3.eth.getBalance(account1, (err, result) => {
  console.log(result)
})

web3.eth.getBalance(account2, (err, result) => {
  console.log(result)
})
```


This is a very simple example in a test environment with `Ganache` running where all
accounts are **unlocked**. Essentially what that means it that for in order for transactions to
be broadcasted on the network, they need to be signed with the account before sending them.
We can basically unlock accounts upon creation so that transactions are signed, that is what
happens with Ganache. In something like `geth`, we can unlock account
using `web3.eth.personal.unlockAccount`. In development, it is easy to unlock account without
having to sign every transaction.


In an Ethereum node, if we don't want to trust the node, keeping all the account
data local and sign the transaction using private key locally, we use **web3** for the signing;

```
// Creating a transaction, signing, broadcasting and sending it.
var Tx = require('ethereumjs-tx').Transaction
const Web3 = require('web3')
const web3 = new Web3('https://ropsten.infura.io/v3/74e7531425ca4e4bb400cb891852d190') // Address from Infura

const account1 = '0x2902EEa694aB8927641f989E8C7c8a4b2f3605FA'
const account2 = '0x74c21895ded89cF6232E69770075B2a0dA9963F7'
// Accounts created on Ropsten using Metamask and Ether added using Faucet

// We use ethereumjs-tx to sign the transactions we are broadcasting to the network. In order
// to do this, we convert this primary key to a string of binary data.

const privateKey1 = Buffer.from(process.env.PRIVATE_KEY_1, 'hex')
const privateKey2 = Buffer.from(process.env.PRIVATE_KEY_2, 'hex') // Private key stored as environment variables

// export PRIVATE_KEY_1 = 'your_key' // Creating an environment variable

web3.eth.getTransactionCount(account1, (err, txCount) => {
  // Building the transaction
  const txObject = {
    nonce: web3.utils.toHex(txCount), // Safeguard to prevent double spend problem
    to: account2,
    value: web3.utils.toHex(web3.utils.toWei('1', 'ether')),
    gasLimit: web3.utils.toHex(21000), // Safeguard
    gasPrice: web3.utils.toHex(web3.utils.toWei('10', 'gwei')) // Cost of each unit of gas
  }

  // Signing the transaction
  const tx = new Tx(txObject, {'chain':'ropsten'})
  tx.sign(privateKey1) // Private Key of Sender

  // Serialising transaction to hex string
  const serializedTransaction = tx.serialize()
  const raw = '0x' + serializedTransaction.toString('hex')

  // Broadcast the transaction
  web3.eth.sendSignedTransaction(raw, (err, txHash) => {
    console.log('txHash:', txHash)
  })
})
```
