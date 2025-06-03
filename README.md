# AVAX/BTC.b Liquidity Provider Agent

This repository contains a proof-of-concept liquidity provider agent for the
AVAX/BTC.b pool on Trader Joe V2.2. The script is intended to run locally using
Python and a Llama3 model. It demonstrates the basic structure required to
monitor the active liquidity bin and rebalance positions within the rewarded
range.

**Warning:** This code is a simplified example and does not implement the full
logic required for production use. It uses placeholder contract addresses and
assumes an existing local installation of a Llama3 model.

## Requirements

- Python 3.10+
- `web3` and `python-dotenv` packages
- Access to a local Llama3 model (see comments in the code)
- An Avalanche C‑Chain wallet with enough funds for gas

Install dependencies with:

```bash
pip install web3 python-dotenv transformers
```

## Usage

Create a `.env` file with the following variables:

```
RPC_URL=<Avalanche RPC URL>
WALLET_ADDRESS=<Your wallet address>
PRIVATE_KEY=<Private key for the wallet>
```

Then run the script:

```bash
python liquidity_provider.py
```

The agent will check the pool status every three minutes and attempt to keep
liquidity within the active bin plus the two adjacent bins while reserving
0.2 AVAX for gas fees.

## Algorithm Overview

1. Fetch the current active bin from the liquidity bin pair contract.
2. Determine whether the position is within the rewarded range (active bin ±2).
3. If outside the range, remove liquidity and swap tokens as needed.
4. Reprovide liquidity in the optimal bins.
5. Wait three minutes and repeat.

Gas usage is minimized by avoiding unnecessary rebalances and batching
transactions whenever possible.

## Disclaimer

This project is for educational purposes only. It does not include comprehensive
error handling, complete ABI definitions, or production‑ready management of
private keys. Use at your own risk.
