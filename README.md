# mpc-multisig
💝 This project received a $25,000 grant from the [DFINITY foundation](https://dfinity.org/grants).

A multi-signature smart account built on the Internet Computer Protocol. Uses multi-party computation (MPC) for Ethereum transaction signing. Expandable to Bitcoin and Solana.

## Why is this needed?

* There's currently no fully on-chain and self-custodial multisignature that supports all major blockchains.
* Every multisignature platform has its own protocol and UX, so there's no unified user experience for all networks.

Using threshold ECDSA, which ICP provides as a network primitive, creating a cross-chain Gnosis Safe equivalent is possible.

## How it works
A database stores identifiers for users and vaults, and is in charge of deploying new vault smart accounts. Each wallet runs as its own contract with an isolated private key, so when you create a wallet, a new contract is deployed specifically for that wallet. These contracts then connect to EVM-based networks through the IC's EVM RPC canister to broadcast transactions and query blockchain data.

When a team approves a transaction, the backend constructs the unsigned transaction, sends it to the smart account for signing, which then broadcasts the signed transaction through the selected network's RPC. All of this happens on-chain within ICP.

## Installation

```bash
# Install dependencies
dfx deps pull
dfx deps deploy evm_rpc
dfx deps deploy internet_identity

# Start local IC replica
dfx start --background

# Deploy the application
dfx deploy

# Generate frontend types
npm run generate
```

Your application will be available at `http://localhost:4943?canisterId={asset_canister_id}`.
