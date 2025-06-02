# Cross-Chain Credit Protocol

A decentralized credit protocol enabling cross-chain lending and borrowing using Chainlink CCIP and Functions.

## Project Structure

```
crosschain-credit/
│
├── contracts/               # Smart contracts
│   ├── LendingManager.sol     # On Sepolia: Handles delegation & CCIP messages to Fuji
│   ├── BorrowingManager.sol    # On Fuji: Handles loan requests, credit validation
│   ├── CreditScoreOracle.sol   # Uses Chainlink Functions to compute credit score
│   ├── CCIPReceiverBase.sol    # Abstract contract to handle CCIP messages
│   ├── AutomationRegistry.sol  # Optional: Automation contract to manage lifecycle
│   ├── interfaces/            # Contract interfaces
│   └── libraries/             # Utility libraries
│
├── script/                  # Deployment scripts
├── test/                     # Test files
├── frontend/                 # Next.js frontend (optional)
├── foundry.toml              # Foundry configuration
└── .env                      # Environment variables
```

## Setup

1. Install dependencies:
   ```bash
   forge install
   ```

2. Copy `.env.example` to `.env` and fill in your environment variables.

3. Compile contracts:
   ```bash
   forge build
   ```

## Testing

Run tests:
```bash
forge test
```

## Deployment

Deploy to Sepolia:
```bash
forge script script/DeploySepolia.s.sol --rpc-url $SEPOLIA_RPC_URL --broadcast -vvvv
```

Deploy to Fuji:
```bash
forge script script/DeployFuji.s.sol --rpc-url $FUJI_RPC_URL --broadcast -vvvv
```

## License

MIT
