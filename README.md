# House of Voi – Slot Machine  
Provably fair, on-chain slot machine for the Voi Network

## Overview

This repository contains the on-chain logic and supporting scripts for the **House of Voi Slot Machine**, a fully verifiable blockchain slot machine.

- 🧩 **Commit–reveal randomness** for verifiable fairness  
- 💰 **On-chain payouts** — instant, transparent, immutable  
- 🎰 **Upgradeable design** that extends to multi-reel machines and tournaments  
- ⚙️ **Built on the Voi Network**, compatible with Algorand’s AVM model  

> **Goal:** demonstrate how yield-bearing tokens and commit–reveal mechanics combine to create a transparent, fun, and fair gaming experience.

---

## How It Works

1. **Commit Phase** – The slot machine commits to a secret random seed hash.  
2. **Player Spin** – The player submits a spin transaction with their wager.  
3. **Reveal Phase** – The seed is revealed, validated against the commitment, and used to compute reel results.  
4. **Payout** – The contract settles the payout if the result is a win.  

All randomness and outcomes can be independently verified using on-chain data.

---

## Repository Structure

| Path | Description |
|------|--------------|
| `contract.py` | Core smart contract logic: spin resolution, payouts, and fairness proofs. |
| `artifacts/` | Compiled TEAL + ABI JSON files. |
| `src/` | TypeScript helpers and deployment scripts. |
| `src/scripts/clients/` | Generated TypeScript clients for each contract. |
| `generate_clients.sh` | Builds ABI clients for contracts and moves them into `src/scripts/clients/`. |
| `commands.sh` | Helper aliases for building, testing, and deploying. |
| `Dockerfile` | Containerized environment for consistent builds. |

---

## Prerequisites

- Node.js and npm  
- [AlgoKit CLI](https://github.com/algorandfoundation/algokit-cli)  
- Python + Pipenv (or standard `pip`)  
- Optional: Docker and VSCode  

---

## Setup

```bash
git clone https://github.com/House-of-Voi/slot-machine.git
cd slot-machine

# Python deps
pipenv install  # or pip install -r requirements.txt

# JS deps
cd src/scripts
npm install
cd ../..
```

---

## Development Flow

### 1. Edit the Contract
Modify `contract.py` for logic changes. This file defines game rules, spin resolution, and payouts.

### 2. Generate Clients and Build Artifacts
```bash
source commands.sh
build-all
```

This compiles contracts and regenerates typed clients under `src/scripts/clients/`.

### 3. Run Local Devnet (Optional)
```bash
algokit localnet start
```
Then open `https://lora.algokit.io/localnet` to verify your devnet status and faucet test funds.

### 4. Run Tests
```bash
mocha
```

---

## Deployment

1. Edit `src/scripts/command.ts`:  
   - Import your contract clients.  
   - Set `DeployType` with the contracts you want to deploy.  
   - Adjust RPC endpoints (`ALGO_SERVER`, `ALGO_INDEXER_SERVER`).  

2. Compile and deploy:
```bash
cd src/scripts
npx tsc
cd ../..
cli deploy -t SlotMachine -n SlotMachine
```

---

## Verifying Fairness

After each spin, the contract reveals the seed used to generate results. Anyone can:

1. Recompute the hash chain / commitment.  
2. Re-derive reel results deterministically.  
3. Confirm payout logic matches contract execution.

---

## Roadmap

- [ ] 5-Reel & Multi-Line Mode  
- [ ] Progressive Jackpots  
- [ ] Tournament & Leaderboard System  
- [ ] Animated Front-End Integration  
- [ ] On-Chain Fairness Verifier  

---

## Security

> **Warning:** This is experimental software.  
> Do not deploy with real value without code review and audit.  

Please report potential vulnerabilities or randomness exploits via GitHub Issues.

---

## License

MIT
