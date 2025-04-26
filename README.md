# SUI CLI Commands Cheatsheet 📋

[![SUI](https://img.shields.io/badge/SUI-Blockchain-blue)](https://sui.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

> A comprehensive collection of SUI CLI commands for blockchain developers and enthusiasts.

## Table of Contents

- [Installation](#installation)
- [Client Configuration](#client-configuration)
- [Wallet Management](#wallet-management)
- [Object Operations](#object-operations)
- [Transaction Commands](#transaction-commands)
- [Package Management](#package-management)
- [Network Commands](#network-commands)
- [Keytool](#keytool)
- [Faucet](#faucet)
- [Advanced Commands](#advanced-commands)
- [Debugging](#debugging)
- [Common Use Cases](#common-use-cases)
- [Environment Variables](#environment-variables)
- [Best Practices](#best-practices)
- [Contributing](#contributing)
- [License](#license)

## Installation

```bash
# Install SUI CLI
cargo install --locked --git https://github.com/MystenLabs/sui.git --branch devnet sui

# Check version
sui --version
```

## Client Configuration

```bash
# Get current configuration
sui client envs

# Switch to specific network
sui client switch --env devnet  # devnet, testnet, mainnet

# Add new environment
sui client new-env --alias <name> --rpc <url>

# View active address
sui client active-address

# Switch active address
sui client switch --address <address>
```

## Wallet Management

```bash
# Create new address
sui client new-address ed25519  # Ed25519 key scheme (recommended)
sui client new-address secp256k1  # Secp256k1 key scheme

# List all addresses
sui client addresses

# Get the gas coins for active address
sui client gas

# Check balance
sui client balance

# Import key
sui keytool import <private-key> <key-scheme>

# Export key
sui keytool export <address>
```

## Object Operations

```bash
# Get object details
sui client object <object-id>

# List objects owned by address
sui client objects

# List objects with specific type
sui client objects --type <package-id>::<module>::<type>

# Merge coins
sui client merge-coin --primary-coin <coin-id> --coin-to-merge <coin-id>

# Split coins
sui client split-coin --coin-id <coin-id> --amounts <amount1> <amount2>
```

## Transaction Commands

```bash
# Transfer SUI
sui client transfer-sui --to <recipient-address> --sui-coin-object-id <coin-id> --amount <amount>

# Transfer object
sui client transfer --to <recipient-address> --object-id <object-id>

# Call Move function
sui client call --package <package-id> --module <module> --function <function> --args <args>

# Dry run a transaction
sui client call --package <package-id> --module <module> --function <function> --args <args> --dry-run

# Pay all gas with a specific coin
sui client pay-all-sui --input-coins <coin-id> --recipient <address>

# Pay specific amount
sui client pay-sui --input-coins <coin-id> --recipients <address> --amounts <amount>
```

## Package Management

```bash
# Build Move package
sui move build

# Test Move package
sui move test

# Publish Move package
sui client publish --gas-budget <budget>

# Upgrade package
sui client upgrade --upgrade-capability <cap-id>
```

## Network Commands

```bash
# Get network status
sui client env

# Show validators
sui client validators

# Display chain identifier
sui client chain-identifier

# View transaction
sui client tx <transaction-digest>

# View transaction effects
sui client transactions --tx-digest <digest>
```

## Keytool

```bash
# Generate new key
sui keytool generate ed25519

# Show current key
sui keytool show

# List all keys
sui keytool list

# Sign arbitrary data
sui keytool sign --address <address> --data <data>

# Multi-sig operations
sui keytool multi-sig-address --pks <pk1> <pk2> --weights <w1> <w2> --threshold <threshold>
```

## Faucet

**Note: Only available on testnet/devnet**

```bash
# Request tokens from faucet
sui client faucet

# Request tokens for specific address
sui client faucet --address <address>
```

## Advanced Commands

```bash
# Execute transaction block
sui client execute-signed-tx --tx-bytes <bytes> --signatures <signatures>

# Get transaction block in JSON format
sui client tx <digest> --json

# Batch transaction
sui client batch-transaction --single-transactions <tx1> <tx2>

# PTB (Programmable Transaction Block)
sui client ptb --split-coins @<coin> <amount> --transfer-objects [0] @<recipient>
```

## Debugging

```bash
# Verbose output
sui client call --package <pkg> --module <mod> --function <func> --verbose

# Get object version
sui client object <object-id> --version <version>

# Check gas estimation
sui client gas-estimate --package <pkg> --module <mod> --function <func>
```

## Common Use Cases

### Create NFT
```bash
sui client call --package <package> --module <module> --function mint_nft --args <name> <description> <url>
```

### Transfer Multiple Objects
```bash
sui client transfer --to <recipient> --object-id <id1>,<id2>,<id3>
```

### Batch Payments
```bash
sui client pay-sui --input-coins <coin1>,<coin2> --recipients <addr1>,<addr2> --amounts <amt1>,<amt2>
```

## Environment Variables

```bash
# Set default environment
export SUI_ENV=devnet

# Set custom RPC endpoint
export SUI_RPC_URL=https://fullnode.devnet.sui.io:443

# Set custom network
export SUI_NETWORK=testnet
```

## Best Practices

1. 🔍 Always check gas before major transactions
2. 🧪 Use `--dry-run` to test transactions before executing
3. 🔐 Keep private keys secure and never share
4. 💾 Regularly backup your keystore
5. ⛽ Use appropriate gas budgets to avoid failed transactions
6. 🔄 For complex operations, use PTBs (Programmable Transaction Blocks)
7. 📊 Monitor transaction status with `sui client tx <digest>`

## Contributing

Feel free to contribute to this cheatsheet by:
1. Forking the repository
2. Creating a feature branch (`git checkout -b feature/AmazingCommand`)
3. Committing your changes (`git commit -m 'Add some AmazingCommand'`)
4. Pushing to the branch (`git push origin feature/AmazingCommand`)
5. Opening a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### 🌟 Show your support

Give a ⭐️ if this project helped you!

### 📝 Notes

- Replace placeholders like `<address>`, `<object-id>`, etc., with actual values when using these commands
- Commands and features may change as SUI evolves. Check official documentation for the latest updates

### 🔗 Useful Links

- [SUI Documentation](https://docs.sui.io/)
- [SUI GitHub Repository](https://github.com/MystenLabs/sui)
- [SUI Discord Community](https://discord.gg/sui)
