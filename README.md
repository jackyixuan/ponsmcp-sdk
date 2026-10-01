# @ponsmcp/sdk

> TypeScript SDK for integrating PonsMCP autonomous payments into AI agents and applications, settled on Robinhood Chain.

[![npm version](https://img.shields.io/npm/v/@ponsmcp/sdk)](https://www.npmjs.com/package/@ponsmcp/sdk)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Robinhood Chain](https://img.shields.io/badge/chain-Robinhood_Chain_4663-6c47ff)](https://robinhoodchain.blockscout.com)

---

## Installation

```bash
npm install @ponsmcp/sdk
# or
yarn add @ponsmcp/sdk
```

---

## Quick Start

```ts
import { PonsMCPClient } from '@ponsmcp/sdk'

const client = new PonsMCPClient({
  rpcUrl: 'https://rpc.mainnet.chain.robinhood.com',
  wallet: await loadAgentWallet(),
  policies: {
    maxPerTransaction: 100_000_000, // 100 USDG (6 decimals, micro-units)
    dailyLimit: 1_000_000_000       // 1000 USDG
  }
})

// Agent encounters HTTP 402 — pay automatically
const result = await client.payForResource({
  url: 'https://api.weather.com/premium/forecast',
  parameters: { location: 'SF', days: 7 }
})

console.log(`Payment finalized: ${result.hash}`)
```

---

## Features

- **Intent-based payment API** — describe what you need, SDK handles the rest
- **Automatic MPP negotiation** — parses HTTP 402 responses and negotiates payment terms
- **Robinhood Chain wallet integration** — native support for EVM wallets (chainId 4663)
- **USDG settlement** — Global Dollar (6 decimals) as the default settlement currency
- **Configurable spending policies** — per-transaction caps, daily limits, merchant allowlists

---

## Network

| Setting | Value |
|---------|-------|
| Chain | Robinhood Chain (Arbitrum Orbit L2) |
| Chain ID | `4663` |
| RPC | `https://rpc.mainnet.chain.robinhood.com` |
| Explorer | `https://robinhoodchain.blockscout.com` |
| Gas token | ETH |
| Settlement token | USDG (`0x5fc5360D0400a0Fd4f2af552ADD042D716F1d168`, 6 decimals) |

---

## License

MIT — see [LICENSE](LICENSE).
