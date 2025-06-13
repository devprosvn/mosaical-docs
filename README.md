
# Mosaical MVP - Decentralized NFT Fractionalization Platform

Mosaical là một nền tảng phi tập trung cho phép phân mảnh (fractionalize) NFT và tạo ra các token DPO (Diversified Portfolio Option) để giao dịch và đầu tư vào danh mục NFT đa dạng.

## 📋 Todo List

### ✅ Completed
- [x] Smart contract development (8 contracts)
- [x] Contract compilation system
- [x] Deployment scripts for Saga chainlet
- [x] Contract flattening for verification
- [x] Basic testing framework
- [x] Environment configuration
- [x] Contract verification on Saga Explorer

### 🔧 In Progress
- [ ] Frontend development
- [ ] API integration
- [ ] Advanced testing scenarios

### 📅 Planned
- [ ] Oracle price feed integration
- [ ] Cross-chain bridge functionality
- [ ] Governance voting mechanism
- [ ] Staking rewards system
- [ ] Mobile application
- [ ] Audit and security review

## 🏗️ System Architecture

```mermaid
graph TB
    User[👤 User] --> Frontend[🖥️ Frontend DApp]
    Frontend --> Web3[🔗 Web3 Provider]
    Web3 --> Saga[🌐 Saga Chainlet]
    
    subgraph "Smart Contracts"
        MockNFT[🎮 MockGameNFT]
        Vault[🏦 NFTVaultV3]
        DPO[💰 DPOTokenV3]
        Loan[📋 LoanManagerV3]
        Oracle[📊 GameFiOracleV3]
        Gov[🗳️ MosaicalGovernance]
        GovToken[🎫 GovernanceToken]
        Bridge[🌉 MosaicalSagaBridge]
    end
    
    Saga --> MockNFT
    Saga --> Vault
    Saga --> DPO
    Saga --> Loan
    Saga --> Oracle
    Saga --> Gov
    Saga --> GovToken
    Saga --> Bridge
    
    Oracle --> ExternalAPI[📡 External Price APIs]
    Bridge --> OtherChains[⛓️ Other Blockchains]
```

## 🎯 Core Features

### 1. NFT Fractionalization
- Deposit NFTs vào vault để nhận DPO tokens
- Phân mảnh ownership của high-value NFTs
- Liquidity mining và yield farming

### 2. Decentralized Finance (DeFi)
- Lending/borrowing với NFT collateral
- Interest distribution system
- Order book trading cho DPO tokens

### 3. Governance System
- Community voting trên protocol changes
- Proposal creation và execution
- Token-based voting power

### 4. Cross-chain Bridge
- Transfer assets giữa các chains
- Multi-chain NFT support
- Unified liquidity pools

## 📊 Functional Diagram

```mermaid
flowchart TD
    Start([🚀 User Start]) --> Choice{Select Action}
    
    Choice -->|Deposit NFT| DepositFlow[📥 Deposit NFT]
    Choice -->|Trade DPO| TradeFlow[💱 Trade DPO Tokens]
    Choice -->|Borrow| BorrowFlow[💰 Borrow Against NFT]
    Choice -->|Governance| GovFlow[🗳️ Governance Actions]
    
    DepositFlow --> CheckNFT{Valid NFT?}
    CheckNFT -->|Yes| MintDPO[🪙 Mint DPO Tokens]
    CheckNFT -->|No| Error1[❌ Error: Invalid NFT]
    MintDPO --> Success1[✅ Success: DPO Received]
    
    TradeFlow --> CheckBalance{Sufficient Balance?}
    CheckBalance -->|Yes| ExecuteTrade[⚡ Execute Trade]
    CheckBalance -->|No| Error2[❌ Error: Insufficient Funds]
    ExecuteTrade --> Success2[✅ Success: Trade Complete]
    
    BorrowFlow --> CheckCollateral{Valid Collateral?}
    CheckCollateral -->|Yes| CreateLoan[📋 Create Loan]
    CheckCollateral -->|No| Error3[❌ Error: Invalid Collateral]
    CreateLoan --> Success3[✅ Success: Loan Created]
    
    GovFlow --> CheckVotingPower{Has Voting Power?}
    CheckVotingPower -->|Yes| Vote[🗳️ Cast Vote]
    CheckVotingPower -->|No| Error4[❌ Error: No Voting Power]
    Vote --> Success4[✅ Success: Vote Recorded]
    
    Success1 --> End([🏁 End])
    Success2 --> End
    Success3 --> End
    Success4 --> End
    Error1 --> End
    Error2 --> End
    Error3 --> End
    Error4 --> End
```

## 🎭 Use Case Diagram

### System Level Use Cases

```mermaid
graph LR
    User[👤 User]
    Investor[👨‍💼 Investor]
    Admin[👑 Admin]
    Oracle[🤖 Oracle]
    
    subgraph "Mosaical System"
        UC1[Deposit NFT]
        UC2[Withdraw NFT]
        UC3[Trade DPO Tokens]
        UC4[Create Loan]
        UC5[Repay Loan]
        UC6[Vote on Proposals]
        UC7[Create Proposals]
        UC8[Update Prices]
        UC9[Manage System]
        UC10[Bridge Assets]
    end
    
    User --> UC1
    User --> UC2
    User --> UC3
    User --> UC4
    User --> UC5
    User --> UC6
    
    Investor --> UC3
    Investor --> UC6
    Investor --> UC7
    
    Admin --> UC9
    Admin --> UC7
    
    Oracle --> UC8
    
    User --> UC10
```

### NFT Vault Module Use Cases

```mermaid
graph LR
    NFTOwner[🎨 NFT Owner]
    DPOHolder[💰 DPO Holder]
    
    subgraph "NFT Vault Module"
        UC1[Deposit NFT]
        UC2[Withdraw NFT]
        UC3[Check Vault Status]
        UC4[Calculate DPO Value]
        UC5[Emergency Withdraw]
    end
    
    NFTOwner --> UC1
    NFTOwner --> UC2
    NFTOwner --> UC3
    NFTOwner --> UC5
    
    DPOHolder --> UC2
    DPOHolder --> UC3
    DPOHolder --> UC4
```

### Loan Manager Module Use Cases

```mermaid
graph LR
    Borrower[💳 Borrower]
    Lender[🏦 Lender]
    
    subgraph "Loan Manager Module"
        UC1[Create Loan Request]
        UC2[Approve Loan]
        UC3[Repay Loan]
        UC4[Liquidate Collateral]
        UC5[Check Loan Status]
        UC6[Calculate Interest]
    end
    
    Borrower --> UC1
    Borrower --> UC3
    Borrower --> UC5
    
    Lender --> UC2
    Lender --> UC4
    Lender --> UC5
    Lender --> UC6
```

### Governance Module Use Cases

```mermaid
graph LR
    TokenHolder[🎫 Token Holder]
    Proposer[📝 Proposer]
    
    subgraph "Governance Module"
        UC1[Create Proposal]
        UC2[Vote on Proposal]
        UC3[Execute Proposal]
        UC4[Delegate Voting Power]
        UC5[Check Voting History]
    end
    
    TokenHolder --> UC2
    TokenHolder --> UC4
    TokenHolder --> UC5
    
    Proposer --> UC1
    Proposer --> UC3
```

## 🏛️ Class Diagram

```mermaid
classDiagram
    class MockGameNFT {
        +string name
        +string symbol
        +constructor(name, symbol)
        +mint(to, tokenId)
        +exists(tokenId) bool
        +tokenURI(tokenId) string
    }
    
    class NFTVaultV3 {
        +mapping vaultedNFTs
        +mapping dpoBalances
        +address oracle
        +constructor(oracle)
        +depositNFT(collection, tokenId)
        +withdrawNFT(collection, tokenId)
        +calculateDPOValue(collection, tokenId) uint256
        +emergencyWithdraw(collection, tokenId)
    }
    
    class DPOTokenV3 {
        +mapping authorizedMinters
        +mapping tokenHoldings
        +mapping claimableInterest
        +constructor()
        +mint(to, amount)
        +mintOnLoan(collection, tokenId, borrower, amount)
        +distributeInterest(collection, tokenId, holder, amount)
        +claimInterest(collection, tokenId)
        +placeBuyOrder(collection, tokenId, amount, price)
        +placeSellOrder(collection, tokenId, amount, price)
    }
    
    class LoanManagerV3 {
        +address nftVault
        +address dpoToken
        +mapping loans
        +constructor(vault, dpoToken)
        +createLoan(collection, tokenId, amount, duration)
        +repayLoan(loanId)
        +liquidateLoan(loanId)
        +calculateInterest(loanId) uint256
    }
    
    class GameFiOracleV3 {
        +mapping priceFeeds
        +mapping authorizedUpdaters
        +constructor()
        +updatePrice(collection, tokenId, price)
        +getPrice(collection, tokenId) uint256
        +addPriceFeed(collection, feedAddress)
    }
    
    class MosaicalGovernance {
        +address governanceToken
        +mapping proposals
        +constructor(govToken)
        +createProposal(description, targets, values, calldatas)
        +vote(proposalId, support)
        +executeProposal(proposalId)
        +getVotingPower(account) uint256
    }
    
    class GovernanceToken {
        +constructor(name, symbol)
        +mint(to, amount)
        +delegate(delegatee)
        +getVotes(account) uint256
    }
    
    class MosaicalSagaBridge {
        +address trustedRemote
        +mapping bridgedAssets
        +constructor(trustedRemote)
        +bridgeToRemote(tokenId, amount, recipient)
        +receiveFromRemote(tokenId, amount, recipient)
        +updateTrustedRemote(newRemote)
    }
    
    NFTVaultV3 --> GameFiOracleV3 : uses
    NFTVaultV3 --> DPOTokenV3 : mints
    LoanManagerV3 --> NFTVaultV3 : manages
    LoanManagerV3 --> DPOTokenV3 : mints
    MosaicalGovernance --> GovernanceToken : uses
    MockGameNFT --> NFTVaultV3 : deposited to
```

## 📊 Entity Relationship Diagram

```mermaid
erDiagram
    USER {
        address wallet_address PK
        uint256 dpo_balance
        uint256 governance_tokens
        uint256 voting_power
        bool is_authorized_minter
    }
    
    NFT {
        address collection_address PK
        uint256 token_id PK
        address owner
        bool is_vaulted
        uint256 estimated_value
        string metadata_uri
    }
    
    VAULT {
        address vault_address PK
        uint256 total_dpo_minted
        uint256 total_nfts_deposited
        address oracle_address
        bool emergency_paused
    }
    
    DPO_TOKEN {
        address token_address PK
        uint256 total_supply
        uint256 decimals
        string name
        string symbol
    }
    
    LOAN {
        uint256 loan_id PK
        address borrower
        address collection_address
        uint256 token_id
        uint256 principal_amount
        uint256 interest_rate
        uint256 duration
        uint256 start_timestamp
        bool is_repaid
        bool is_liquidated
    }
    
    PROPOSAL {
        uint256 proposal_id PK
        address proposer
        string description
        uint256 vote_start
        uint256 vote_end
        uint256 votes_for
        uint256 votes_against
        bool executed
        bool cancelled
    }
    
    VOTE {
        uint256 vote_id PK
        uint256 proposal_id FK
        address voter
        bool support
        uint256 voting_power
        uint256 timestamp
    }
    
    PRICE_FEED {
        address collection_address PK
        uint256 token_id PK
        uint256 current_price
        uint256 last_updated
        address feed_source
        bool is_active
    }
    
    BRIDGE_TRANSACTION {
        uint256 tx_id PK
        address from_chain
        address to_chain
        address sender
        address recipient
        uint256 amount
        uint256 timestamp
        bool completed
    }
    
    USER ||--o{ NFT : owns
    USER ||--o{ LOAN : borrows
    USER ||--o{ VOTE : casts
    USER ||--o{ PROPOSAL : creates
    
    NFT ||--o| VAULT : deposited_in
    NFT ||--o| LOAN : collateral_for
    NFT ||--o| PRICE_FEED : has_price
    
    VAULT ||--|| DPO_TOKEN : mints
    VAULT ||--o{ LOAN : manages
    
    PROPOSAL ||--o{ VOTE : receives
    
    LOAN }|--|| NFT : secured_by
    LOAN }|--|| USER : borrowed_by
    
    PRICE_FEED }|--|| NFT : prices
```

## 🚀 Quick Start

### 1. Environment Setup
```bash
# Copy environment template
cp .env.example .env

# Edit .env with your private key and network settings
```

### 2. Compile Contracts
```bash
# Using workflow button or command
npm run compile
# or
node scripts/compile.js
```

### 3. Deploy Contracts
```bash
# Deploy to Saga chainlet
npx hardhat run scripts/deploy.js --network devpros

# Deploy with JSON output
npx hardhat run scripts/deploy-with-json.js --network devpros
```

### 4. Verify Contracts
```bash
# Flatten contracts first
node scripts/flatten.js

# Manual verification on Saga Explorer
# Use flattened files in /flattened directory
```

### 5. Run Tests
```bash
npx hardhat test
```

## 📁 Project Structure

```
├── contracts/              # Smart contracts
│   ├── MockGameNFT.sol     # Example NFT contract
│   ├── NFTVaultV3.sol      # NFT vault for deposits
│   ├── DPOTokenV3.sol      # Fractionalized tokens
│   ├── LoanManagerV3.sol   # Lending protocol
│   ├── GameFiOracleV3.sol  # Price oracle
│   ├── MosaicalGovernance.sol # DAO governance
│   ├── GovernanceToken.sol # Voting tokens
│   └── MosaicalSagaBridge.sol # Cross-chain bridge
├── scripts/                # Deployment & utility scripts
├── test/                   # Test files
├── deployments/            # Deployment records
├── flattened/              # Flattened contracts for verification
└── .env.example           # Environment template
```

## 🌐 Network Configuration

### Saga Chainlet (devpros)
- **RPC URL**: `https://devpros-2749656616387000-1.jsonrpc.sagarpc.io`
- **Chain ID**: `2749656616387000`
- **Explorer**: `https://devpros-2749656616387000-1.sagaexplorer.io`
- **WebSocket**: `https://devpros-2749656616387000-1.ws.sagarpc.io`

### Contract Addresses (Latest Deployment)
```json
{
  "MockGameNFT": "0x165ABbf7859997e9Ebed825df101E313Db642dda",
  "GovernanceToken": "0x54bef235A25daC5B4386A05e25D37688C5379936",
  "GameFiOracleV3": "0x980F5eA0dc03175056BC041f4708C82B74d6E322",
  "NFTVaultV3": "0x869d9bF00823018f74854033040943A1ff5EFf60",
  "MosaicalGovernance": "0xd31E3D5e43E9945B4AF2aDD7f5a54C00E76b0991",
  "DPOTokenV3": "0x6d66483DC259783f4E4aDe90b1fAB01F8A876D2e",
  "LoanManagerV3": "0xC9D80AF77a91d7FB7A73189D1D97ABc29399460c",
  "MosaicalSagaBridge": "0x2FbA9CcF4930FB188a4A5A7a7bFC6aDBda0eb439"
}
```

## 🔧 Available Scripts

| Command | Description |
|---------|-------------|
| `npm run compile` | Compile smart contracts |
| `npm run deploy` | Deploy contracts to network |
| `npm run test` | Run test suite |
| `npm run flatten` | Generate flattened contracts |
| `npm run verify` | Verify contracts on explorer |

## 🛡️ Security Considerations

- All contracts use OpenZeppelin secure implementations
- Multi-signature requirements for critical operations
- Emergency pause mechanisms
- Oracle price manipulation protection
- Reentrancy guards on financial functions

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📞 Support

For support and questions:
- Create an issue in the repository
- Join our Discord community
- Follow our documentation

---

*Built with ❤️ on Saga Chainlet*


# 🎨 Mosaical - NFT Lending Platform

## 📋 Overview

Mosaical is a decentralized NFT lending platform that allows users to use their NFTs as collateral to borrow DPSV tokens. The platform integrates AI-powered price prediction, real-time analytics, and DPO (Decentralized Public Offering) features.

## ✨ Features

- **NFT Vault Management**: Deposit and manage NFT collections as collateral
- **Lending & Borrowing**: Borrow DPSV tokens against NFT collateral
- **AI Price Prediction**: Machine learning models for NFT price forecasting
- **Real-time Analytics**: Market data visualization and portfolio tracking
- **DPO Panel**: Decentralized public offering management
- **Multi-language Support**: English and Vietnamese language support
- **Web3 Integration**: MetaMask and wallet connectivity

## 🏗️ System Architecture

```mermaid
graph TB
    subgraph "Frontend Layer"
        A[React + TypeScript App]
        B[Web3 Context]
        C[Language Context]
        D[UI Components]
    end
    
    subgraph "Backend Layer"
        E[Node.js Express Server]
        F[Socket.io WebSocket]
        G[Web3 Service]
        H[Indexer Service]
    end
    
    subgraph "AI Layer"
        I[Python AI API]
        J[NFT Price Predictor]
        K[Data Scraper]
        L[ML Models]
    end
    
    subgraph "Data Layer"
        M[PostgreSQL Database]
        N[JSON Prediction Files]
        O[CSV Datasets]
    end
    
    subgraph "External APIs"
        P[CoinGecko API]
        Q[Blockchain RPC]
        R[NFT Marketplaces]
    end
    
    A --> E
    A --> B
    B --> G
    E --> F
    E --> H
    E --> M
    I --> J
    I --> K
    J --> L
    J --> N
    K --> O
    K --> P
    G --> Q
    H --> R
    
    style A fill:#4f46e5
    style E fill:#059669
    style I fill:#dc2626
    style M fill:#7c3aed
```

## 🎯 Use Case Diagram - Overall System

```mermaid
graph TD
    subgraph "Actors"
        U1[NFT Owner]
        U2[Borrower]
        U3[Lender]
        U4[DPO Investor]
        U5[Admin]
    end
    
    subgraph "Core Use Cases"
        UC1[Connect Wallet]
        UC2[Deposit NFT]
        UC3[Withdraw NFT]
        UC4[Borrow DPSV]
        UC5[Repay Loan]
        UC6[View Analytics]
        UC7[Predict Prices]
        UC8[Participate in DPO]
        UC9[Manage Portfolio]
        UC10[Monitor Health Factor]
    end
    
    U1 --> UC1
    U1 --> UC2
    U1 --> UC3
    U2 --> UC4
    U2 --> UC5
    U2 --> UC10
    U3 --> UC6
    U3 --> UC7
    U4 --> UC8
    U5 --> UC9
    
    UC2 --> UC4
    UC4 --> UC5
    UC6 --> UC7
    
    style U1 fill:#3b82f6
    style U2 fill:#10b981
    style U3 fill:#f59e0b
    style U4 fill:#ef4444
    style U5 fill:#8b5cf6
```

## 🏛️ Module Use Case Diagrams

### NFT Vault Module

```mermaid
graph TD
    subgraph "NFT Vault Actors"
        A1[NFT Owner]
        A2[Smart Contract]
    end
    
    subgraph "NFT Vault Use Cases"
        V1[View NFT Collection]
        V2[Deposit NFT to Vault]
        V3[Withdraw NFT from Vault]
        V4[Check NFT Valuation]
        V5[Approve NFT Transfer]
        V6[Update NFT Metadata]
    end
    
    A1 --> V1
    A1 --> V2
    A1 --> V3
    A1 --> V4
    A2 --> V5
    A2 --> V6
    
    V2 --> V5
    V4 --> V2
```

### Lending Module

```mermaid
graph TD
    subgraph "Lending Actors"
        L1[Borrower]
        L2[Loan Contract]
        L3[Oracle Service]
    end
    
    subgraph "Lending Use Cases"
        LC1[Calculate Loan Amount]
        LC2[Create Loan Request]
        LC3[Approve Loan]
        LC4[Disburse Funds]
        LC5[Monitor Health Factor]
        LC6[Liquidate Position]
        LC7[Repay Loan]
        LC8[Calculate Interest]
    end
    
    L1 --> LC1
    L1 --> LC2
    L1 --> LC7
    L2 --> LC3
    L2 --> LC4
    L2 --> LC6
    L3 --> LC5
    L3 --> LC8
    
    LC1 --> LC2
    LC2 --> LC3
    LC3 --> LC4
    LC5 --> LC6
```

### AI Prediction Module

```mermaid
graph TD
    subgraph "AI Actors"
        AI1[Data Scientist]
        AI2[ML Models]
        AI3[External APIs]
    end
    
    subgraph "AI Use Cases"
        AI4[Scrape NFT Data]
        AI5[Process Market Data]
        AI6[Train ML Models]
        AI7[Generate Predictions]
        AI8[Validate Model Performance]
        AI9[Update Price Forecasts]
        AI10[Serve Prediction API]
    end
    
    AI1 --> AI4
    AI1 --> AI6
    AI1 --> AI8
    AI2 --> AI7
    AI2 --> AI9
    AI3 --> AI5
    AI3 --> AI10
    
    AI4 --> AI5
    AI5 --> AI6
    AI6 --> AI7
    AI7 --> AI9
```

## 🎨 Class Diagram

```mermaid
classDiagram
    class User {
        +String address
        +String nonce
        +Date createdAt
        +Date updatedAt
        +connectWallet()
        +signMessage()
        +authenticate()
    }

    class NFT {
        +String tokenId
        +String contractAddress
        +String ownerAddress
        +String collectionName
        +String tokenName
        +String tokenUri
        +Object metadata
        +Boolean deposited
        +Number valueEth
        +deposit()
        +withdraw()
        +updateValue()
    }

    class Loan {
        +String loanId
        +String userAddress
        +Number nftId
        +Number borrowedAmount
        +Number collateralValue
        +Number interestRate
        +Number healthFactor
        +Number ltv
        +Date createdAt
        +createLoan()
        +repayLoan()
        +liquidate()
        +calculateHealthFactor()
    }

    class Prediction {
        +String collectionId
        +Array futurePredictions
        +Object modelPerformance
        +Date timestamp
        +generatePrediction()
        +updateModel()
        +validateAccuracy()
    }

    class Transaction {
        +String txHash
        +String userAddress
        +String type
        +Number amount
        +String status
        +Date timestamp
        +processTransaction()
        +validateTransaction()
        +updateStatus()
    }

    class DPOProject {
        +String projectId
        +String name
        +String description
        +Number targetAmount
        +Number raisedAmount
        +Date startDate
        +Date endDate
        +String status
        +createProject()
        +invest()
        +closeProject()
    }

    %% relationships using UML multiplicities    
    User "1" --> "0..*" NFT : owns
    User "1" --> "0..*" Loan : borrows
    User "1" --> "0..*" Transaction : makes
    User "1" --> "0..*" DPOProject : invests
    NFT "1" --> "0..1" Loan : collateralizes
    Loan "1" --> "0..*" Transaction : generates
    Prediction "1" --> "0..*" NFT : predicts
```

## 🗃️ Entity Relationship Diagram

```mermaid
erDiagram
    USERS {
        varchar address PK
        varchar nonce
        timestamp created_at
        timestamp updated_at
    }
    
    NFTS {
        serial id PK
        varchar token_id
        varchar contract_address
        varchar owner_address FK
        varchar collection_name
        varchar token_name
        text token_uri
        jsonb metadata
        boolean deposited
        timestamp deposited_at
        decimal value_eth
        timestamp created_at
        timestamp updated_at
    }
    
    LOANS {
        serial id PK
        varchar loan_id UK
        varchar user_address FK
        integer nft_id FK
        decimal borrowed_amount
        decimal collateral_value
        decimal interest_rate
        decimal health_factor
        decimal ltv
        varchar status
        timestamp due_date
        timestamp created_at
        timestamp updated_at
    }
    
    TRANSACTIONS {
        serial id PK
        varchar tx_hash UK
        varchar user_address FK
        varchar type
        decimal amount
        varchar currency
        varchar status
        timestamp timestamp
        jsonb metadata
    }
    
    PREDICTIONS {
        serial id PK
        varchar collection_id
        jsonb future_predictions
        jsonb model_performance
        timestamp timestamp
        timestamp created_at
    }
    
    DPO_PROJECTS {
        serial id PK
        varchar project_id UK
        varchar name
        text description
        decimal target_amount
        decimal raised_amount
        timestamp start_date
        timestamp end_date
        varchar status
        timestamp created_at
    }
    
    DPO_INVESTMENTS {
        serial id PK
        varchar project_id FK
        varchar investor_address FK
        decimal amount
        timestamp invested_at
    }
    
    USERS ||--o{ NFTS : owns
    USERS ||--o{ LOANS : borrows
    USERS ||--o{ TRANSACTIONS : makes
    USERS ||--o{ DPO_INVESTMENTS : invests
    NFTS ||--|| LOANS : secures
    LOANS ||--o{ TRANSACTIONS : generates
    DPO_PROJECTS ||--o{ DPO_INVESTMENTS : receives
```

## 🔄 Functional Flow Diagram

```mermaid
flowchart TD
    A[User Connects Wallet] --> B{Wallet Connected?}
    B -->|No| A
    B -->|Yes| C[Browse NFT Collections]
    
    C --> D[Select NFT to Deposit]
    D --> E[Approve NFT Transfer]
    E --> F[Deposit NFT to Vault]
    F --> G[NFT Valuation via AI]
    
    G --> H[Calculate Max Loan Amount]
    H --> I[User Requests Loan]
    I --> J{Health Factor > 1.2?}
    
    J -->|No| K[Reject Loan Request]
    J -->|Yes| L[Create Loan Contract]
    L --> M[Disburse DPSV Tokens]
    
    M --> N[Monitor Loan Health]
    N --> O{Health Factor < 1.1?}
    O -->|Yes| P[Liquidation Warning]
    O -->|No| Q[Continue Monitoring]
    
    P --> R{User Repays?}
    R -->|Yes| S[Update Health Factor]
    R -->|No| T[Liquidate NFT]
    
    S --> Q
    T --> U[Auction NFT]
    U --> V[Settle Debt]
    
    Q --> W[User Repays Loan]
    W --> X[Return NFT to User]
    
    style A fill:#4f46e5
    style G fill:#dc2626
    style M fill:#059669
    style T fill:#ef4444
```

## 📊 Data Flow Diagram

```mermaid
flowchart LR
    subgraph "External Data Sources"
        A[CoinGecko API]
        B[Blockchain Networks]
        C[NFT Marketplaces]
    end
    
    subgraph "Data Collection Layer"
        D[Data Scraper]
        E[Blockchain Indexer]
        F[Price Aggregator]
    end
    
    subgraph "Processing Layer"
        G[Data Preprocessor]
        H[Feature Engineer]
        I[ML Pipeline]
    end
    
    subgraph "Storage Layer"
        J[Raw Data Storage]
        K[Processed Data]
        L[Model Storage]
        M[Prediction Cache]
    end
    
    subgraph "API Layer"
        N[REST API]
        O[WebSocket API]
        P[AI Prediction API]
    end
    
    subgraph "Frontend"
        Q[React Dashboard]
        R[Real-time Charts]
        S[User Interface]
    end
    
    A --> D
    B --> E
    C --> F
    
    D --> G
    E --> G
    F --> G
    
    G --> H
    H --> I
    
    G --> J
    H --> K
    I --> L
    I --> M
    
    J --> N
    K --> N
    L --> P
    M --> P
    
    N --> O
    P --> O
    
    O --> Q
    Q --> R
    Q --> S
```

## 🏃‍♂️ Getting Started

### Prerequisites

- Node.js 18+
- Python 3.11+
- PostgreSQL 16+
- Git

### Installation

1. **Clone the repository:**
```bash
git clone <repository-url>
cd mosaical-nft-lending
```

2. **Install frontend dependencies:**
```bash
npm install
```

3. **Install backend dependencies:**
```bash
cd backend
npm install
cd ..
```

4. **Install AI dependencies:**
```bash
cd ai
pip install -r requirements.txt
cd ..
```

5. **Setup environment variables:**
```bash
cp backend/.env.example backend/.env
# Edit backend/.env with your configuration
```

6. **Setup database:**
```bash
cd backend
npm run migrate
cd ..
```

### Running the Application

**Development Mode (Full Stack + AI):**
```bash
npm run dev
```

This will start:
- Frontend on port 3001
- Backend API on port 3001
- AI API on port 5000

## 🚀 Deployment

The application is configured for Replit deployment:

1. **Build the application:**
```bash
npm run build
```

2. **Deploy via Replit:**
- Click the "Deploy" button in Replit
- Configure environment variables
- Deploy to autoscale

## 📁 Project Structure

```
mosaical-nft-lending/
├── src/                    # Frontend React application
│   ├── components/         # Reusable UI components
│   ├── contexts/          # React contexts (Web3, Language)
│   ├── pages/             # Main application pages
│   └── lib/               # Utility functions
├── backend/               # Node.js backend API
│   ├── routes/            # API route handlers
│   ├── services/          # Business logic services
│   ├── config/            # Configuration files
│   └── utils/             # Backend utilities
├── ai/                    # Python AI/ML services
│   ├── datasets/          # Training data
│   ├── models/            # Trained ML models
│   └── predictions/       # Generated predictions
└── docs/                  # Documentation
```

## 🔧 API Endpoints

### Authentication
- `POST /api/auth/login` - Web3 authentication
- `POST /api/auth/nonce` - Get nonce for signing

### User Management
- `GET /api/user/profile` - Get user profile
- `PUT /api/user/profile` - Update user profile
- `GET /api/user/balance` - Get DPSV balance

### NFT Operations
- `GET /api/nfts` - List user NFTs
- `POST /api/nfts/deposit` - Deposit NFT
- `POST /api/nfts/withdraw` - Withdraw NFT
- `GET /api/nfts/valuation/:id` - Get NFT valuation

### Lending
- `POST /api/loans/create` - Create new loan
- `GET /api/loans` - List user loans
- `POST /api/loans/repay` - Repay loan
- `GET /api/loans/health/:id` - Check health factor

### Analytics
- `GET /api/analytics/dashboard` - Dashboard metrics
- `GET /api/analytics/portfolio` - Portfolio analytics
- `GET /api/analytics/market` - Market data

### AI Predictions
- `GET /api/predictions/:collection` - Get price predictions
- `GET /api/predictions/all` - Get all predictions
- `POST /api/predictions/refresh` - Refresh predictions

## 🧪 Testing

```bash
# Run frontend tests
npm test

# Run backend tests
cd backend
npm test

# Run AI model tests
cd ai
python -m pytest tests/
```

## 📋 TODO List

### ✅ Completed Features
- [x] Basic React frontend with TypeScript
- [x] Web3 wallet integration (MetaMask)
- [x] Multi-language support (EN/VI)
- [x] NFT vault interface
- [x] Loan management interface
- [x] AI price prediction integration
- [x] Real-time analytics dashboard
- [x] DPO panel interface
- [x] Backend API with Express.js
- [x] PostgreSQL database integration
- [x] AI/ML price prediction models
- [x] CoinGecko API integration
- [x] Socket.io for real-time updates
- [x] DPSV token conversion

### 🚧 In Progress
- [ ] Smart contract integration
- [ ] Blockchain transaction processing
- [ ] Advanced ML model optimization
- [ ] Mobile responsive design improvements

### 📅 Planned Features

#### Phase 1: Core Infrastructure
- [ ] Smart contract deployment on Saga
- [ ] Automated liquidation system
- [ ] Advanced portfolio analytics
- [ ] Mobile app development

#### Phase 2: Advanced Features
- [ ] Cross-chain NFT support
- [ ] Yield farming integration
- [ ] DAO governance implementation
- [ ] Advanced trading features

#### Phase 3: Enterprise Features
- [ ] Institutional lending
- [ ] Insurance protocol integration
- [ ] Advanced risk management
- [ ] Regulatory compliance tools

#### Phase 4: Ecosystem Expansion
- [ ] NFT marketplace integration
- [ ] DeFi protocol partnerships
- [ ] Layer 2 scaling solutions
- [ ] Cross-platform compatibility

### 🐛 Known Issues
- [ ] Price prediction accuracy needs improvement
- [ ] UI responsiveness on mobile devices
- [ ] Socket.io connection stability
- [ ] Database query optimization needed

### 🔧 Technical Improvements
- [ ] Add comprehensive error handling
- [ ] Implement rate limiting
- [ ] Add API documentation with Swagger
- [ ] Improve test coverage (target: 80%+)
- [ ] Add performance monitoring
- [ ] Implement caching strategy
- [ ] Add CI/CD pipeline
- [ ] Security audit and penetration testing

### 🎨 UI/UX Improvements
- [ ] Dark/light theme toggle
- [ ] Improved loading states
- [ ] Better error messages
- [ ] Accessibility improvements
- [ ] Animation and micro-interactions
- [ ] Mobile-first responsive design

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support and questions:
- Create an issue on GitHub
- Join our Discord community
- Email: support@mosaical.io

## 🙏 Acknowledgments

- CoinGecko for NFT market data
- Saga blockchain for infrastructure
- OpenZeppelin for smart contract standards
- React and TypeScript communities

---

Built with ❤️ by the Mosaical Team
