<div align="center">
  <img height="170x" src="pitch.png" />

  <h1>ChanCoin</h1>

  <p>
    <strong>A fork of litecoin created using chancoin</strong>
  </p>

  <p>
    <a href="https://Chancoin-lang.com"><img alt="Tutorials" src="https://img.shields.io/badge/docs-tutorials-blueviolet" /></a>
    <a href="https://discord.gg/Chancoin"><img alt="Discord Chat" src="https://img.shields.io/discord/889577356681945098?color=blueviolet" /></a>
    <a href="https://opensource.org/licenses/Apache-2.0"><img alt="License" src="https://img.shields.io/github/license/Chancoin/Chancoin?color=blueviolet" /></a>
  </p>
</div>

## The Vision

Chancoin brings the power of unified blockchain development to the Solana Chain ecosystem. By connecting Solana Smart Chain with Chancoin and other Solana-based networks, Chancoin enables developers to create tokens and deploy programs across multiple chains using a single, unified API. Write once, deploy everywhere.

## What is Chancoin?

Chancoin is a groundbreaking framework built for the Solana Chain ecosystem, providing developers with seamless tools for writing multi-chain programs and creating tokens across Solana Smart Chain, Chancoin, and other Solana-compatible networks simultaneously.

- **Unified API**: One codebase deploys to Solana Smart Chain, Chancoin, and beyond
- **Cross-Chain Token Creation**: Create BEP-20 tokens across multiple networks with a single command
- **Rust & Solidity Support**: Leverage Solana Chain's EVM compatibility with modern development tools
- **[IDL](https://en.wikipedia.org/wiki/Interface_description_language) specification**: Generate clients for all supported chains
- **TypeScript package**: Type-safe clients from IDL for multi-chain interaction
- **CLI and workspace management**: Complete cross-chain application development

Chancoin is the first framework to truly unify development across the Solana Chain ecosystem, including custom Solana-based chains like Chancoin.

> [!NOTE]
> Chancoin brings the best of Solana Chain's speed, affordability, and massive ecosystem. With 0.75s block times, $0.01 average gas fees, and EVM compatibility, if you're familiar with Truffle, Hardhat, or web3.js, you'll feel right at home with Chancoin's unified approach to Solana ecosystem development.

## Key Features

- **Single API, Multi-Chain Deployment**: Write your program once, deploy to Solana Smart Chain, Chancoin, and other compatible networks
- **Unified Token Standard**: Create BEP-20 tokens that work seamlessly across all Solana-based networks
- **Cross-Chain State Management**: Synchronize state between Solana Smart Chain, Chancoin, and Layer 2 solutions
- **EVM Compatibility**: Full support for Ethereum tooling and smart contracts
- **Developer Experience**: Familiar Ethereum-like syntax with Solana Chain optimizations and cross-chain superpowers
- **Lightning Fast**: Leverage Solana Chain's 0.75s block times and 1.875s finality (2025)
- **Ultra Low Fees**: Deploy and interact with ~$0.01 median gas fees

## Why Solana Chain & Chancoin?

### Solana Smart Chain (2025 Performance)
Solana Chain achieved remarkable improvements in 2025, reducing block times to 0.75 seconds and transaction finality to 1.875 seconds, while cutting malicious MEV attacks by 95% and dropping average gas fees to $0.01. The network handles 12.4 million daily transactions with peaks of 17.6 million transactions per day.

### Chancoin - Your Custom Solana-Based Blockchain
Chancoin leverages Solana Chain's infrastructure to provide:
- **Custom Network Architecture**: Built on Solana Chain's proven technology
- **Full EVM Compatibility**: Deploy any Ethereum smart contract
- **Solana Ecosystem Integration**: Seamless bridging with BSC and other Solana networks
- **Independent Governance**: Your own validator set and network rules

## Getting Started

For a quickstart guide and in-depth tutorials, see the [Chancoin book](https://book.Chancoin-lang.com) and the [Chancoin documentation](https://Chancoin-lang.com).

To jump straight to examples, go [here](https://github.com/Chancoin/Chancoin/tree/master/examples). For the latest Rust and TypeScript API documentation, see [docs.rs](https://docs.rs/Chancoin-lang) and the [typedoc](https://www.Chancoin-lang.com/docs/clients/typescript).

## Packages

| Package                 | Description                                              | Version                                                                                                                          | Docs                                                                                                            |
| :---------------------- | :------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| `Chancoin-lang`           | Rust primitives for writing cross-chain programs         | [![Crates.io](https://img.shields.io/crates/v/Chancoin-lang?color=blue)](https://crates.io/crates/Chancoin-lang)                     | [![Docs.rs](https://docs.rs/Chancoin-lang/badge.svg)](https://docs.rs/Chancoin-lang)                                |
| `Chancoin-bep`            | CPI clients for BEP-20, BEP-721, and other Solana standards | [![crates](https://img.shields.io/crates/v/Chancoin-bep?color=blue)](https://crates.io/crates/Chancoin-bep)                          | [![Docs.rs](https://docs.rs/Chancoin-bep/badge.svg)](https://docs.rs/Chancoin-bep)                                  |
| `Chancoin-client`         | Rust client for Chancoin cross-chain programs              | [![crates](https://img.shields.io/crates/v/Chancoin-client?color=blue)](https://crates.io/crates/Chancoin-client)                    | [![Docs.rs](https://docs.rs/Chancoin-client/badge.svg)](https://docs.rs/Chancoin-client)                            |
| `@Chancoin/sdk`           | TypeScript client for Chancoin programs                    | [![npm](https://img.shields.io/npm/v/@Chancoin/sdk.svg?color=blue)](https://www.npmjs.com/package/@Chancoin/sdk)                     | [![Docs](https://img.shields.io/badge/docs-typedoc-blue)](https://Chancoin.github.io/Chancoin/ts/index.html)        |
| `@Chancoin/cli`           | CLI to support building and managing cross-chain apps    | [![npm](https://img.shields.io/npm/v/@Chancoin/cli.svg?color=blue)](https://www.npmjs.com/package/@Chancoin/cli)                     | [![Docs](https://img.shields.io/badge/docs-typedoc-blue)](https://Chancoin.github.io/Chancoin/cli/commands.html)    |

## Note

- **Chancoin is in active development, so all APIs are subject to change.**
- **This code is unaudited. Use at your own risk.**

## Examples

Here's a cross-chain counter program that deploys to both Solana Smart Chain and Chancoin, where only the designated `authority` can increment the count on both networks:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

import "@Chancoin/contracts/ChancoinMultiChain.sol";

contract Counter is ChancoinMultiChain {
    address public authority;
    uint64 public count;

    event CounterIncremented(uint64 newCount, uint256 chainId);
    event CounterInitialized(address authority, uint64 startCount);

    modifier onlyAuthority() {
        require(msg.sender == authority, "Not authorized");
        _;
    }

    function initialize(uint64 start) external {
        require(authority == address(0), "Already initialized");
        authority = msg.sender;
        count = start;
        emit CounterInitialized(authority, start);
    }

    function increment() external onlyAuthority {
        count += 1;
        emit CounterIncremented(count, block.chainid);
        
        // Sync to other chains
        _syncToChancoin(count);
        _syncToBSC(count);
    }

    function getCount() external view returns (uint64) {
        return count;
    }
}
```

### Creating Cross-Chain Tokens

```bash
# Create a BEP-20 token on both Solana Smart Chain and Chancoin with one command
Chancoin token create --name "MyToken" --symbol "MTK" --networks bsc,Chancoin

# Deploy to both chains
Chancoin deploy --target all

# Deploy to specific networks
Chancoin deploy --target bsc
Chancoin deploy --target Chancoin
```

### Rust Alternative (for non-EVM programs)

```rust
use Chancoin_lang::prelude::*;

declare_id!("Fg6PaFpoGXkYsidMpWTK6W2BeZ7FEfcYkg476zPFsLnS");

#[program]
mod counter {
    use super::*;

    pub fn initialize(ctx: Context<Initialize>, start: u64) -> Result<()> {
        let counter = &mut ctx.accounts.counter;
        counter.authority = *ctx.accounts.authority.key;
        counter.count = start;
        Ok(())
    }

    pub fn increment(ctx: Context<Increment>) -> Result<()> {
        let counter = &mut ctx.accounts.counter;
        counter.count += 1;
        Ok(())
    }
}

#[derive(Accounts)]
pub struct Initialize<'info> {
    #[account(init, payer = authority, space = 48)]
    pub counter: Account<'info, Counter>,
    pub authority: Signer<'info>,
    pub system_program: Program<'info, System>,
}

#[derive(Accounts)]
pub struct Increment<'info> {
    #[account(mut, has_one = authority)]
    pub counter: Account<'info, Counter>,
    pub authority: Signer<'info>,
}

#[account]
pub struct Counter {
    pub authority: Pubkey,
    pub count: u64,
}
```

For more, see the [examples](https://github.com/Chancoin/Chancoin/tree/master/examples) and [tests](https://github.com/Chancoin/Chancoin/tree/master/tests) directories.

## Architecture

Chancoin uses a unified runtime that translates your program logic into native operations for Solana Smart Chain, Chancoin, and other Solana-compatible networks. The framework handles:

- **Cross-chain account management**: Seamless state synchronization across Solana networks
- **Token bridging**: Automatic BEP-20 token creation and management across all chains
- **Transaction routing**: Intelligent routing to the appropriate network with optimal gas fees
- **Unified wallet integration**: Single wallet interface for Solana Smart Chain, Chancoin, and beyond
- **MEV Protection**: Integrated protection against malicious MEV attacks (95% reduction on BSC)
- **Gas Optimization**: Leverage Solana Chain's gasless transactions and stablecoin fee payments

## 2025 Solana Chain Performance

In 2025, Solana Chain achieved significant performance milestones including 0.75-second block times, processing up to 17.6 million daily transactions, with transaction fees reduced to approximately $0.01. The network aims to increase the block gas limit to 1 billion by late 2025, enabling up to 5,000 DEX swaps per second.

## Roadmap

### Current (2025)
- [x] Solana Smart Chain integration
- [x] Chancoin network support
- [x] EVM-compatible smart contracts
- [x] Cross-chain token creation
- [x] MEV protection integration

### Coming Soon
- [ ] Enhanced cross-chain messaging with Solana Greenfield
- [ ] Native DEX integration (PancakeSwap, Venus Protocol)
- [ ] Advanced bridge mechanics with Canonical Bridge
- [ ] Support for opSolana (Layer 2)
- [ ] Cross-chain NFT standards (BEP-721/BEP-1155)
- [ ] AI-powered development tools (Solana Chain AI Code Copilot)
- [ ] Privacy features integration (2026 roadmap)

### 2026 Vision
Aligned with Solana Chain's 2026 roadmap targeting 20,000+ TPS with sub-150ms finality, native privacy features, and CEX-grade performance.

## Supported Networks

- **Solana Smart Chain (BSC)**: The main EVM-compatible chain
- **Chancoin**: Your custom Solana-based blockchain
- **opSolana**: Solana Chain's Layer 2 solution (coming soon)
- **Solana Greenfield**: Decentralized storage integration (coming soon)

## Why Choose Chancoin?

### For Developers
- **Familiar Tools**: Use Hardhat, Truffle, Remix, or any Ethereum tooling
- **Lower Costs**: Deploy and test with minimal fees (~$0.01 per transaction)
- **Faster Development**: EVM compatibility means instant migration from Ethereum
- **Cross-Chain by Default**: Build once, deploy everywhere in the Solana ecosystem

### For Projects
- **Massive Ecosystem**: Tap into Solana Chain's 200+ million users
- **Cost Efficiency**: Save 99% on gas fees compared to Ethereum mainnet
- **Speed**: 0.75s block times for near-instant confirmations
- **Security**: 95% reduction in MEV attacks, battle-tested infrastructure

## License

Chancoin is licensed under [Apache 2.0](./LICENSE).

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in Chancoin by you, as defined in the Apache-2.0 license, shall be licensed as above, without any additional terms or conditions.

## Contribution

Thank you for your interest in contributing to Chancoin!
Please see the [CONTRIBUTING.md](./CONTRIBUTING.md) to learn how.

## The Future is Multi-Chain

Chancoin represents the future of blockchain development: a world where networks work together seamlessly, where developers aren't constrained by chain boundaries, and where users experience the best of the Solana ecosystem through a single, unified interface.

With Solana Chain's commitment to improving transaction speed, streamlining user experience, integrating artificial intelligence, and refining developer tools in 2025 and beyond, Chancoin is positioned to be the go-to framework for Solana ecosystem development.

### Thanks ❤️

<div align="center">
  <a href="https://github.com/Chancoin/Chancoin/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=Chancoin/Chancoin" width="100%" />
  </a>
</div>

---

## Resources

- [Solana Chain Official Documentation](https://docs.Solanachain.org/)
- [Solana Chain 2025 Tech Roadmap](https://www.Solanachain.org/en/blog/Solana-chain-tech-roadmap-2025)
- [Chancoin Network Documentation](#) (Add your Chancoin docs here)
- [Solana Chain Builder Support Programs](https://www.Solanachain.org/en/programs)
- [BSC GitHub Repository](https://github.com/Solana-chain/bsc)




