# 🌉 Cross-Chain Credit Delegation + Under-Collateralized Lending Protocol

This protocol enables **under-collateralized lending across chains** by allowing users to **delegate their creditworthiness** from one chain (e.g., Sepolia) to another (e.g., Fuji). It leverages Chainlink’s **CCIP**, **Functions**, **Data Feeds**, and **Automation** to orchestrate secure, automated, and interoperable credit-based lending in a multi-chain world.

---

## ✨ Features

- ✅ Cross-chain credit delegation (lender on Sepolia, borrower on Fuji)
- ✅ Chainlink Functions for real-time credit score calculation
- ✅ Chainlink CCIP for secure cross-chain communication
- ✅ Chainlink Automation for lifecycle enforcement
- ✅ Chainlink Data Feeds for dynamic collateral evaluation

---

## 📁 Project Structure

├── contracts/
│ ├── LendingManager.sol
│ ├── BorrowingManager.sol
│ ├── CreditScoreOracle.sol
│ ├── AutomationRegistry.sol
│ ├── interfaces/
│ │ ├── ICCIPReceiver.sol
│ │ ├── IChainlinkFunctions.sol
│ │ ├── IChainlinkDataFeeds.sol
│ ├── libraries/
│ │ └── MessageUtils.sol
│
├── script/
│ ├── DeploySepolia.s.sol
│ ├── DeployFuji.s.sol
│ ├── DeployAll.s.sol
│ ├── ConfigureCCIP.s.sol
│
├── test/
│ ├── LendingManager.t.sol
│ ├── BorrowingManager.t.sol
│ ├── CreditScoreOracle.t.sol
│ ├── CrossChainFlow.t.sol
│ └── mocks/
│ ├── MockCCIPRouter.sol
│ ├── MockFunctionsOracle.sol
│ └── MockDataFeed.sol
│
├── frontend/
│ ├── pages/
│ │ ├── index.tsx
│ │ ├── lender.tsx
│ │ └── borrower.tsx
│ ├── components/
│ │ ├── CreditForm.tsx
│ │ └── LoanStatusCard.tsx
│ └── utils/
│ └── useContract.ts
│
├── foundry.toml
├── .env
└── README.md


---

## 🔍 Key File Descriptions

### 🔐 Smart Contracts (Solidity)

| File | Description |
|------|-------------|
| **LendingManager.sol** | Deployed on Sepolia. Allows lenders to delegate credit and initiate CCIP messages to Fuji. |
| **BorrowingManager.sol** | Deployed on Fuji. Allows borrowers to request loans and process CCIP delegation data. |
| **CreditScoreOracle.sol** | Uses Chainlink Functions to calculate borrower credit score from off-chain/on-chain data. |
| **AutomationRegistry.sol** | Triggers repayment deadlines and loan status updates using Chainlink Automation. |
| **interfaces/** | Contains interfaces for CCIP, Chainlink Functions, and Data Feeds. |
| **libraries/MessageUtils.sol** | Encodes/decodes cross-chain messages for standardized CCIP payloads. |

---

### 📜 Scripts

| Script | Description |
|--------|-------------|
| **DeploySepolia.s.sol** | Deploys LendingManager contract to Sepolia. |
| **DeployFuji.s.sol** | Deploys BorrowingManager contract to Fuji. |
| **DeployAll.s.sol** | Deploys both contracts for local/integration testing. |
| **ConfigureCCIP.s.sol** | Sets trusted senders and CCIP router configuration between chains. |

---

### 🧪 Tests (Foundry)

| File | Description |
|------|-------------|
| **LendingManager.t.sol** | Unit test for credit delegation logic. |
| **BorrowingManager.t.sol** | Unit test for loan request and score validation. |
| **CreditScoreOracle.t.sol** | Tests Chainlink Functions integration and credit score output. |
| **CrossChainFlow.t.sol** | Full E2E cross-chain simulation using mocks. |
| **mocks/** | Simulated CCIP router, data feed, and functions oracle for testing. |

---

### 🌐 Frontend (Next.js + Ethers/ViEM)

| File | Description |
|------|-------------|
| **index.tsx** | Welcome page + role selection (Lender / Borrower). |
| **lender.tsx** | UI for lenders to delegate credit. |
| **borrower.tsx** | UI for borrowers to request and view loan status. |
| **CreditForm.tsx** | Reusable form for user interactions. |
| **LoanStatusCard.tsx** | Displays loan and credit data dynamically. |
| **useContract.ts** | Hook for smart contract interactions via Ethers.js or Viem. |

---

## 🔧 Setup Instructions

### 1. Install Dependencies

```bash
forge install
npm install # (for frontend)


.env Example

SEPOLIA_RPC_URL=https://sepolia.infura.io/v3/YOUR_KEY
FUJI_RPC_URL=https://api.avax-test.network/ext/bc/C/rpc
PRIVATE_KEY=your_private_key
LENDING_MANAGER_ADDRESS=...
BORROWING_MANAGER_ADDRESS=...
CHAINLINK_FUNCTIONS_ORACLE=...
CHAINLINK_CROSS_CHAIN_ROUTER=...


**Deploy Contracts**
forge script script/DeploySepolia.s.sol --rpc-url $SEPOLIA_RPC_URL --broadcast
forge script script/DeployFuji.s.sol --rpc-url $FUJI_RPC_URL --broadcast

Configure CCIP Routing

forge script script/ConfigureCCIP.s.sol --broadcast


Credit Score Calculation Logic

Category	                   Weight	              Description
1. On-Chain Activity        	30%	           Wallet age, number of transactions, gas spent
2. DeFi Lending History   	  25%	           Aave, Compound, etc. borrowing/repayment track record
3. Credit Delegation History	10%	           Previously delegated credit & repayment status
4. Reputation Signals	        15%            GitHub activity, ENS name, Proof of Humanity
5. Social Score (Optional)   	10%	           GitHub, Twitter, Lens, Farcaster (Sybil-resistance)
6. Collateral/Asset Holdings	10%	           Assets held in wallets as soft fallback
