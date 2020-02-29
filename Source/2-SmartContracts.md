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
```
new web3.eth.Contract(jsonInterface[, address][, options])
```
Here, *jsonInterface* is the interface for the contract to instantiate. ABI is
essentially a JSON file that shows what a Smart contract can do. We also need
the location of the smart contract, it's address. Everything in Ethereum has an
address, including users and contracts.

# Talk to a `Token` contract on the main Ethereum Blockchain
Ethereum has a way to define tokens called ERC20Tokens.

Fire up the node console started by running `node` in the terminal.
```
var Web3 = require('web3')
var web3 = new Web3('https://mainnet.infura.io/v3/74e7531425ca4e4bb400cb891852d190')
```

Create an instance of the Smart Contract in web3. We find a token using Etherscan.
```
var abi = [{"constant":true,"inputs":[],"name":"name","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_amount","type":"uint256"}],"name":"approve","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_newOwner","type":"address"}],"name":"setOwner","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"totalSupply","outputs":[{"name":"supply","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_from","type":"address"},{"name":"_to","type":"address"},{"name":"_amount","type":"uint256"}],"name":"transferFrom","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"decimals","outputs":[{"name":"","type":"uint8"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"seal","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_bonus","type":"uint256"}],"name":"offerBonus","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"isSealed","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"lastMintedTimestamp","outputs":[{"name":"","type":"uint32"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"symbol","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_amount","type":"uint256"}],"name":"transfer","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_owner","type":"address"},{"name":"_amount","type":"uint256"},{"name":"_isRaw","type":"bool"},{"name":"timestamp","type":"uint32"}],"name":"mint","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_value","type":"uint256"},{"name":"_extraData","type":"bytes"}],"name":"approveAndCall","outputs":[{"name":"success","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"},{"name":"_spender","type":"address"}],"name":"allowance","outputs":[{"name":"remaining","type":"uint256"}],"payable":false,"type":"function"},{"inputs":[],"payable":false,"type":"constructor"},{"payable":false,"type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_from","type":"address"},{"indexed":true,"name":"_to","type":"address"},{"indexed":false,"name":"_value","type":"uint256"}],"name":"Transfer","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_owner","type":"address"},{"indexed":true,"name":"_spender","type":"address"},{"indexed":false,"name":"_value","type":"uint256"}],"name":"Approval","type":"event"}]
```

We pass the address of the token, also found using Etherscan.
```
var contractAddress = '0xD850942eF8811f2A866692A623011bDE52a462C1'
var contract = new web3.eth.Contract(abi, contractAddress) // Creating a new contract as a JavaScript object
```

To get list of all methods;
```
contract.methods
```

We can now use the methods in the Smart Contract. For e.g., to get the name of the token;
```
contract.methods.name().call((err, result) => {
  console.log(result)
})
```

For e.g., to get the symbol;
```
contract.methods.symbol().call((err, result) => {
  console.log(result)
})
```

For e.g., to look at the total supply;
```
contract.methods.totalSupply().call((err, result) => {
  console.log(result)
})
```

Next, to get specific details from the tokens. For e.g, to get the balance of the token owned by a user
```
var accountAddress = '0x000000000000000000007cd4706885c41853ec7b' // Address of someone who holds these tokens, found using Etherscan
contract.methods.balanceOf(accountAddress).call((err, result) => {
  console.log(result)
})
```
