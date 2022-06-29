# Disclaimer
This code is based on the course [Solidity, Blockchain, and Smart Contract Course](https://github.com/smartcontractkit/full-blockchain-solidity-course-py).
In this README you can find some notes/comments about basics of Solidity. There won't be everything, for the complete lesson plese have a look to the course of Patrick Collins (Alpha), above.

# Scopes in Solidity
* `public`: function `f()` can be called from everywhere (within a contract, in his derivated and outside)
* `external`: it's recommanded to use this scope if we expect to call function `f()` externally (actually, this is a bit inaccurate: more discussion below).
* `internal`: function `f()` can only be called in this contract and in his derivated. (default)
* `private`: function `f()` can be called in this contract only, not in derivated ones (only `this->f()` is allowed).

For variables, the concept is similar. Scope determines their visibility.

## Focus: `public` or `external`?
We've already said that `external` keyword is recommanded for functions that are called externally to a contract. Actually, there is a workaround that permits `external` functions to be called outside the contract. Being part of the contract interface, they are instances of the contract: they can be accessed through `this->f()` inside the contract (but not simply through `f()` as `internal` and `private` functions.

So, `public` and `external` functions _seems_ to have the same scope, and this is in part to. In past versions of Solidity there was a reason according to which using `external` functions required less GAS than `public` functions for large amount of data. Now this is not valid anymore and the rationale has been moved to the keywords `memory` vs `calldata` (we discuss about them in the next two paragraphs of this README). [This post](https://ethereum.stackexchange.com/questions/19380/external-vs-public-best-practices) on Ethereum StackExchange is particularly interesting in this respect, but only to understand the evolution of Solidity. At the current state (Solidity 0.9), that post is outdated.

# `pure` functions vs `view` functions
ToDo

# `memory` keyword vs `storage` (vs `calldata`) keyword
ToDo

# Basics data structures in Solidity
ToDo
