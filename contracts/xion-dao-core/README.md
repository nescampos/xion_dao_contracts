# xion-dao-core

This contract is the core module for all Xion DAOs. It handles
management of voting power and proposal modules, executes messages,
and holds the DAO's treasury.


## Developing
Core messages and interfaces are defined in the [dao-interfaces](../../packages/dao-interface) package. If you are building new modules or a contract that interacts with a DAO, use `dao-interface`.

## Treasury management

For management of non-native assets this contract maintains a list of
[cw20](https://github.com/CosmWasm/cw-plus/tree/1568d9f7796ef93747e5e5e45484447fddbea80b/packages/cw20)
and
[cw721](https://github.com/CosmWasm/cw-nfts/tree/c7be7aba9fb270abefee5a3696be62f2736592a0/packages/cw721)
tokens who's balances the DAO would like to track. This allows
frontends to list these tokens in the DAO's treasury. This tracking is
needed as, for non-native tokens, there is no on-chain data source for
all of the cw20 and cw721 tokens owned by a DAO. It may also help
reduce spam as random shitcoins sent to the DAO won't be displayed in
treasury listings, unless the DAO approves them.

### Managing the treasury

There are two ways that a non-native token may be added to the DAO
treasury.

If `automatically_add_[cw20s|cw721s]` is set to true in the DAO,
the DAO will add the token to the treasury upon receiving the token
via cw20's `Send` method and cw721's `SendNft` method.

```
pub enum ExecuteMsg {
    /// Executed when the contract receives a cw20 token. Depending on
    /// the contract's configuration the contract will automatically
    /// add the token to its treasury.
    #[cfg(feature = "cw20")]
    Receive(cw20::Cw20ReceiveMsg),
    /// Executed when the contract receives a cw721 token. Depending
    /// on the contract's configuration the contract will
    /// automatically add the token to its treasury.
    ReceiveNft(cw721::Cw721ReceiveMsg),
	// ...
}
```

The DAO may always add or remove non-native tokens via the
`UpdateCw20List` and `UpdateCw721List` methods:

```rust
pub enum ExecuteMsg {
    /// Updates the list of cw20 tokens this contract has registered.
    #[cfg(feature = "cw20")]
    UpdateCw20List {
        to_add: Vec<String>,
        to_remove: Vec<String>,
    },
    /// Updates the list of cw721 tokens this contract has registered.
    UpdateCw721List {
        to_add: Vec<String>,
        to_remove: Vec<String>,
    },
	// ...
}
```
