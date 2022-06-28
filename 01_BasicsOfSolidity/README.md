# Disclaimer
This code is based on the course [Solidity, Blockchain, and Smart Contract Course](https://github.com/smartcontractkit/full-blockchain-solidity-course-py).
In this README you can find some notes/comments about basics of Solidity. There won't be everything, for the complete lesson plese have a look to the course of Patrick Collins (Alpha), above.

# Scopes in Solidity
* `public`: function `f()` can be called from everywhere (within a contract, in his derivated and outside)
* `external`: as above it's recommanded to use this scope if we expect to call function `f()` externally (actually, this is a bit inaccurate: more discussion below).
* `internal`: function `f()` can only be called in this contract and in his derivated. (default)
* `private`: function `f()` can be called in this contract only, not in derivated ones (only `this->f()` is allowed).

For variables, the concept is similar. Scope determines their visibility.

## Focus: `public` vs `external`
[This post](https://ethereum.stackexchange.com/questions/19380/external-vs-public-best-practices) on ethereum stackexchange is particularly interesting in this respect.
Here a resume from this discussion. Firstly, let's give a better definition for `external` keyword.

# `pure` functions vs `view` functions
ToDo

# `memory` keyword vs `storage` keyword
ToDo

# Basics data structures in Solidity
ToDo
