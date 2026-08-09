# 🌍 Stellar Carbon Registry

A decentralized carbon credit tokenization, trading, and retirement protocol built on the Stellar network using Soroban smart contracts.

## Overview

Stellar Carbon Registry enables projects (reforestation, renewable energy, direct air capture) to **issue** tokenized carbon credits on-chain. Buyers can **purchase** and **retire** credits transparently — every retirement is permanent, verifiable, and auditable.

## Why

Carbon markets suffer from double-counting, opaque registries, and slow settlement. By tokenizing credits on Stellar with Soroban, we get:
- **Transparent issuance** — every credit's origin is on-chain
- **Instant settlement** — no clearinghouse delays
- **Immutable retirement** — retired credits can never be re-traded
- **Low fees** — Stellar's sub-cent transactions make micro-credits viable

## Architecture

### Soroban Contract (`contracts/carbon-registry`)
| Function | Description |
|---|---|
| `initialize` | Set admin, verifier, USDC token |
| `issue_credits` | Verifier mints credits for a project with metadata (region, project_type, vintage) |
| `buy_credits` | Purchase credits at listed price (USDC) |
| `retire_credits` | Permanently retire credits (burn) — generates a retirement certificate |
| `list_credits` | List credits for sale at a price |
| `get_project` | View project metadata and credit balance |
| `get_retirement` | View retirement certificate details |

### Frontend (`frontend`)
React + Vite + Freighter wallet integration for browsing projects, buying credits, and viewing retirement certificates.

## Flows

1. **Verifier** calls `issue_credits(project_id, amount, metadata)` — credits minted to project account
2. **Project owner** calls `list_credits(project_id, price_per_credit, amount)` — credits listed for sale
3. **Buyer** calls `buy_credits(listing_id, amount)` — USDC transferred, credits moved to buyer
4. **Buyer** calls `retire_credits(amount, reason)` — credits burned, retirement certificate issued

## Build & Test

```bash
cd contracts/carbon-registry && cargo test
cd ../../frontend && npm install && npm run dev
```

## License

MIT
