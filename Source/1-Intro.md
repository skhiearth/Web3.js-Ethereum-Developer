**Web3.js** is the main JavaScript library for interacting with the Ethereum
Blockchain and developing DApps. The Smart contract development deals with
writing code that is actually deployed on the Ethereum Blockchain. On the other hand,
a client or a website talks to the blockchain and that is where the web3.js
library comes into play. It gives us a way to build a client that can talk to the
Ethereum blockchain. A website talks to a blockchain using a JSON-RPC. It is a method
that allows us to talk to the blockchain. Ethereum is a P2P network of nodes that all
talk to one another. We use the JSON-RPC protocol to make requests to a particular node
on the network and that's going to kind of act like an API. Essentially, a call to a
smart contract is a JSON-RPC request to a node in the blockchain network.

# Setting up
In the terminal, type `node`, and then in the node terminal do the following:
var Web3 = require('web3')
var url = 'https://mainnet.infura.io/v3/74e7531425ca4e4bb400cb891852d190' // Get URL from Infura
var web3 = new Web3(url)

# Interacting with accounts using Web3
var address = '0x53d284357ec70cE289D6D64134DfAc8E511c8a3D' // Find an account using Etherscan
web3.eth.getBalance(address, (err, bal) => {
  balance = bal
})
balance // Prints out the value of Wei owned by the account
web3.utils.fromWei(balance, 'ether') // Run this to get the Ether balance

# Creating an account using Web3
web3.eth.accounts.create()

# We can also connect to a local private Ethereum network for development purposes.
var url = 'HTTP://127.0.0.1:7545' // Get URL from Ganache
var web3 = new Web3(url)

var address = '0x3f53c658065C5918fA2edBe39F22806D30b2c57a' // Use any address on Ganache
web3.eth.getBalance(address, (err, wei) => {
  balance = web3.utils.fromWei(wei, 'ether')
})
balance
