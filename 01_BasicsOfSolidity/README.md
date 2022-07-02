# Introduction
This code is based on the course [Solidity, Blockchain, and Smart Contract Course](https://github.com/smartcontractkit/full-blockchain-solidity-course-py).
In this README you can find some notes/comments about basics of Solidity. There won't be everything, for the complete lesson plese have a look to the course of Patrick Collins (Patrick Alpha), above.

Latest Solidity version at the time of this doc: 0.8.15

# Scopes in Solidity
* `public`: function `f()` can be called from everywhere (within a contract, in his derivated and outside)
* `external`: it's recommanded if we expect to call function `f()` externally (actually, this is a bit inaccurate: more discussion below).
* `internal`: function `f()` can only be called in this contract and in his derivated. (default)
* `private`: function `f()` can be called in this contract only, not in derivated ones (only `this->f()` is allowed).

For variables, the concept is similar. Scope determines their visibility.

## Focus: `public` or `external`?
We've already said that `external` keyword is recommanded for functions that are called externally to a contract. Actually, there is a workaround that permits `external` functions to be called outside the contract. Being part of the contract interface, they are instances of the contract: they can be accessed through `this->f()` inside the contract (but not simply through `f()` as `internal` and `private` functions.

So, `public` and `external` functions _seems_ to have the same scope, and this is in part to. In past versions of Solidity there was a reason according to which using `external` functions required less gas than `public` functions for large amount of data. Now this is not valid anymore and the rationale has been moved to the keywords `memory` vs `calldata` (we discuss about them in the next two paragraphs of this README). [This post](https://ethereum.stackexchange.com/questions/19380/external-vs-public-best-practices) on Ethereum StackExchange is particularly interesting in this respect, but only to understand the evolution of Solidity. At the current state, that post is outdated.

To conclude, I feel to say that `external` is a subset of `public`, without any comment on their convenience from gas point of view.

# `view` functions vs `pure` functions
Normally, functions which are not `internal` or `private` consumes GAS to be invoked. This doesn't happen when `public` or `external` functions are labeled with `view` or `pure` keyword.

`view` is used to look at the Blockchain status. Reading the blockchain without modifying it has no costs in Ethereum. Naturally, inside a `view` function we can't modify blockchains' objects. For instance, the following snippet of code will return an *error*:

```
uint256 private blockchainIntVariable = 66;

function lookIntVariable() public view returns(uint256) {
    blockchainIntVariable = 67; // Not allowed! We need to pay to perform this operation --> no in a `view` function
    return blockchainIntVariable; // Allowed.
}
```

`pure` functions don't modify as well the blockchain status. Actually, they don't look at all at blockchain status. They are functions that return the same output upon the same input. Obviously, even though they do not concern the blockchain, they are part of the smart contract. Example:
```
function offset() public pure returns(uint256) {
    return 4;
}
```
Passing a state variable (like `blockchainIntVariable`) as a parameter of a `pure` function is not possible: it will lead to a Solidity error.

# `memory` vs `storage` vs `calldata` keywords
These three keywords defines *where* a variable is stored (note: they also concern functions' parameters). [This article](https://medium.com/coinmonks/solidity-storage-vs-memory-vs-calldata-8c7e8c38bce) explains the concept with useful examples. Let's do a resume of this source (and others) here:

`storage` is where state variables (i.e., variables who are part of a smart contract) are stored. Functions except `pure` and `view` can modify state variables, so variables labeled as `storage` can be modified as well. This location is *persistent* along with the smart contract. In other words, storage variables are stored in the blockchain. The data location - the storage - is composed of 32-bytes slots. Multiple variables can share the same slot, and a variable can also occupies more than one slot. Slots are contiguous to keep the memory location as most compacted as possible. An exception is reprensented by dynamic data structures (e.g., non-static arrays, lists, etc.) whose dimension is unknown a priori. They are stored in a separated storage, and the starting address is computed through a `keccak-256` hash, the same as [Merkle Trees](https://github.com/TheBulgarianUmbrella/BinaryMerkleTree). `const` variables are not saved in the storage but embedded in the smart contract executable. With respect to `memory` and `calldata` variables, since they are stored in the blockchain, they consume much more gas.

Example in the source code: function XXX consumed YYY gas.
```
ToDo
```

`memory`


`calldata`

# Basic types in Solidity
ToDo
