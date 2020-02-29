*web3.eth.Contract* essentially creates an abstraction of a smart contract in jS
that we can use to call the functions of the Smart Contract. If we want to actually
interact with the Smart Contract on the EVM, we must understand the interface of the
contract and *web3.eth.Contract* helps us in that.

The web3.eth.Contract object makes it easy to interact with smart contracts on the
ethereum blockchain. When you create a new contract object you give it the json
interface of the respective smart contract and web3 will auto convert all calls into
low level ABI calls over RPC for you.

This allows you to interact with smart contracts as if they were JavaScript objects.

The method to create a new contract is:

new web3.eth.Contract(jsonInterface[, address][, options])

Here, *jsonInterface* is the interface for the contract to instantiate. ABI is
essentially a JSON file that shows what a Smart contract can do. We also need
the location of the smart contract, it's address. Everything in Ethereum has an
address, including users and contracts.
