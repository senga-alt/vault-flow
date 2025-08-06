# VaultFlow Pro 🚀

[![Clarity](https://img.shields.io/badge/Clarity-3.0-blue.svg)](https://docs.stacks.co/clarity)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-Vitest-yellow.svg)](tests/)

> **Advanced Bitcoin Yield Aggregation Protocol on Stacks**

VaultFlow Pro is a sophisticated DeFi protocol that enables Bitcoin holders to earn optimized yields through intelligent staking mechanisms while maintaining full custody and liquidity through tokenized representations.

## 🌟 Overview

VaultFlow Pro revolutionizes Bitcoin yield generation by creating a decentralized infrastructure where users can stake their Bitcoin and receive vfBTC tokens representing their position. The protocol employs advanced yield optimization algorithms, risk assessment scoring, and optional insurance coverage to maximize returns while minimizing exposure.

### Key Features

- **🔄 Dynamic Yield Distribution** - Compound interest calculations with optimized APY
- **📊 Risk Assessment System** - Integrated scoring for portfolio optimization
- **🛡️ Insurance Module** - Optional coverage for additional security layers
- **📈 Real-time Analytics** - Comprehensive yield tracking and performance metrics
- **🪙 SIP-010 Compliance** - Standard-compliant tokenized staking positions
- **⚡ Instant Liquidity** - Flexible staking/unstaking with immediate access

## 🏗️ Architecture

The protocol consists of several core components:

### Smart Contract Structure

```
VaultFlow Pro Contract
├── Protocol Management
│   ├── Initialization
│   ├── Owner Controls
│   └── Emergency Functions
├── Staking Engine
│   ├── Deposit & Stake
│   ├── Withdraw & Unstake
│   └── Position Management
├── Yield Distribution
│   ├── Automated Distribution
│   ├── Harvest Rewards
│   └── Compound Interest
├── Token System (SIP-010)
│   ├── Transfer Functions
│   ├── Balance Queries
│   └── Metadata Management
├── Risk Assessment
│   ├── Profile Scoring
│   ├── Position Analysis
│   └── Risk Mitigation
└── Insurance Module
    ├── Coverage Management
    ├── Reserve Pool
    └── Claims Processing
```

### Core Constants

| Constant | Value | Description |
|----------|-------|-------------|
| `MINIMUM_STAKE_AMOUNT` | 1,000,000 μBTC | 0.01 BTC minimum entry |
| `BASE_YIELD_RATE` | 750 basis points | 7.5% optimized APY |
| `YIELD_DISTRIBUTION_BLOCKS` | 144 blocks | ~24 hours cycle |

## 🚀 Getting Started

### Prerequisites

- [Clarinet CLI](https://github.com/hirosystems/clarinet) - Stacks development environment
- [Node.js](https://nodejs.org/) (v18+) - For testing framework
- [Git](https://git-scm.com/) - Version control

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/senga-alt/vault-flow.git
   cd vault-flow
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Verify installation**

   ```bash
   clarinet check
   ```

### Quick Start

1. **Initialize the protocol**

   ```clarity
   (contract-call? .vault-flow initialize-vaultflow-protocol u750)
   ```

2. **Stake Bitcoin**

   ```clarity
   (contract-call? .vault-flow deposit-and-stake u10000000) ;; 0.1 BTC
   ```

3. **Check your position**

   ```clarity
   (contract-call? .vault-flow get-participant-stake-info tx-sender)
   ```

## 🧪 Testing

The project includes comprehensive test coverage using Vitest and Clarinet SDK.

### Run Tests

```bash
# Run all tests
npm test

# Run tests with coverage report
npm run test:report

# Watch mode for development
npm run test:watch
```

### Test Structure

```
tests/
└── vault-flow.test.ts      # Main contract test suite
    ├── Protocol Initialization
    ├── Staking Operations
    ├── Yield Distribution
    ├── Token Transfers
    ├── Risk Assessment
    └── Insurance Module
```

## 📋 API Reference

### Public Functions

#### Protocol Management

##### `initialize-vaultflow-protocol`

```clarity
(define-public (initialize-vaultflow-protocol (initial-yield-rate uint))
```

**Purpose**: Initialize the protocol with base yield rate  
**Access**: Owner only  
**Parameters**: `initial-yield-rate` - APY in basis points (750 = 7.5%)

#### Core Staking

##### `deposit-and-stake`

```clarity
(define-public (deposit-and-stake (deposit-amount uint))
```

**Purpose**: Stake Bitcoin and receive vfBTC tokens  
**Access**: Public  
**Parameters**: `deposit-amount` - Amount in μBTC (min: 1,000,000)

##### `withdraw-and-unstake`

```clarity
(define-public (withdraw-and-unstake (withdrawal-amount uint))
```

**Purpose**: Unstake position and harvest pending rewards  
**Access**: Public  
**Parameters**: `withdrawal-amount` - Amount in μBTC

#### Yield Management

##### `execute-protocol-yield-distribution`

```clarity
(define-public (execute-protocol-yield-distribution)
```

**Purpose**: Distribute protocol-wide yield rewards  
**Access**: Owner only  
**Frequency**: Every 144 blocks (~24 hours)

##### `harvest-accumulated-yield`

```clarity
(define-public (harvest-accumulated-yield)
```

**Purpose**: Claim individual yield rewards  
**Access**: Public  
**Effect**: Compounds rewards into staking position

### Read-Only Functions

#### Analytics & Queries

##### `get-comprehensive-protocol-metrics`

```clarity
(define-read-only (get-comprehensive-protocol-metrics))
```

**Returns**: Protocol TVL, yield distributed, APY, status

##### `get-participant-stake-info`

```clarity
(define-read-only (get-participant-stake-info (participant principal)))
```

**Returns**: Individual staking balance

##### `get-participant-risk-assessment`

```clarity
(define-read-only (get-participant-risk-assessment (participant principal)))
```

**Returns**: Risk score for participant

### SIP-010 Token Functions

The contract implements full SIP-010 compliance:

- `get-name` - Returns "VaultFlow Staked BTC"
- `get-symbol` - Returns "vfBTC"
- `get-decimals` - Returns 8
- `get-balance` - Account balance lookup
- `get-total-supply` - Total protocol TVL
- `transfer` - Token transfer with memo support

## 🛡️ Security Features

### Access Controls

- **Owner-only functions** for critical operations
- **Participant validation** for all user interactions
- **Amount validation** with minimum thresholds

### Economic Security

- **Risk assessment scoring** based on position size
- **Insurance module** for additional protection
- **Yield distribution limits** to prevent manipulation

### Operational Security

- **Time-locked distributions** prevent gaming
- **Balance validation** on all transfers
- **State consistency** checks throughout

## 🎯 Use Cases

### For Individual Investors

- **Passive Income**: Earn steady yield on Bitcoin holdings
- **Liquidity**: Maintain access to funds through vfBTC tokens
- **Security**: Benefit from protocol insurance and risk management

### For Institutional Players

- **Portfolio Optimization**: Diversify Bitcoin holdings with yield
- **Risk Management**: Leverage integrated risk assessment tools
- **Compliance**: SIP-010 standard ensures regulatory compatibility

### For DeFi Integration

- **Composability**: vfBTC tokens work with other DeFi protocols
- **Liquidity Provision**: Use staked positions as collateral
- **Yield Farming**: Compound returns across multiple protocols

## 🔧 Configuration

### Network Settings

The protocol supports deployment across Stacks networks:

- **Devnet** - Local development (`settings/Devnet.toml`)
- **Testnet** - Public testing (`settings/Testnet.toml`)
- **Mainnet** - Production (`settings/Mainnet.toml`)

### Protocol Parameters

Key parameters can be adjusted by the contract owner:

| Parameter | Default | Description |
|-----------|---------|-------------|
| Base Yield Rate | 7.5% | Annual percentage yield |
| Distribution Frequency | 144 blocks | Yield distribution cycle |
| Minimum Stake | 0.01 BTC | Entry threshold |
| Insurance Coverage | Optional | Risk protection toggle |

## 📊 Performance Metrics

### Gas Optimization

- **Efficient calculations** minimize transaction costs
- **Batch operations** reduce multiple call overhead
- **Storage optimization** keeps state lean

### Yield Performance

- **Compound interest** maximizes returns
- **Dynamic rates** adapt to market conditions
- **Risk-adjusted pricing** optimizes yield/risk ratio

## 🤝 Contributing

We welcome contributions from the community! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create a feature branch
3. Write tests for new functionality
4. Ensure all tests pass
5. Submit a pull request

### Code Standards

- Follow Clarity best practices
- Maintain comprehensive test coverage
- Document all public functions
- Use meaningful variable names

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
