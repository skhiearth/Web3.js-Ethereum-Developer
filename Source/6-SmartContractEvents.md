## Prerequisites:
```
npm install web3
npm install ethereumjs-tx
```


Smart Contracts on the Ethereum blockchain can emit events. What this means essentially
is that they can emit a signal that says something happened inside the contract, and
can broadcast that event to the entire network, and a consumer can subscribe to that event
to find out something happened inside the network.

An event `transfer` is part of the ERC20 standard.

The Solidity source code for the event's interface looks like this:
```
event Transfer(address indexed _from, address indexed _to, uint256 _value)
```
