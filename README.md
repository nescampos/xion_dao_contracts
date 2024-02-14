# Xion DAO Contracts

This is a collection of smart contracts for building composable, modular, and upgradable DAOs for Xion Network.

## Overview

Every DAO is made up of three modules:

1. A voting power module, which manages the voting power of DAO members.
2. Any number of proposal modules, which manage proposals in the DAO.
3. A core module, which holds the DAO treasury.

![image](https://user-images.githubusercontent.com/30676292/220181882-737c4dd3-a85d-498c-a1f2-067b317418a9.png)

For example, voting power might be based on staked governance tokens, staked NFTs, or membership and proposal modules might implement yes/no, multiple-choice, or ranked-choice voting.

Each module type has a standard interface. As a result, any voting module can be used with any proposal module, and any proposal module with any voting module.

## DAO Contracts

- `xion-dao-core` - the core module for DAOs.
- `external` - contracts used by DAOs that are not part of a DAO module (from other repositories).
- `pre-propose` - pre-propose modules.
- `proposal` - proposal modules.
- `voting` - voting modules.
- `staking` - cw20 staking functionality and a staking rewards system. 

## Packages

This folder contains various libraries and external packages, adapted (preserving licenses and intellectual property) so that Xion Daos can operate correctly.
The owners of these codes include DAO DAO, Cosmos open source, among others.

## Developer

- [Nestor Campos](https://www.linkedin.com/in/nescampos/)