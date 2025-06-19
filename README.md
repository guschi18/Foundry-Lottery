# 🎲 Foundry Lottery - Provably Random Smart Contract Raffle

A decentralized, transparent, and provably random lottery system built with Solidity and Foundry, leveraging Chainlink VRF (Verifiable Random Function) and Chainlink Automation for true randomness and automated execution.

## 🌟 Overview

This project implements a fully decentralized lottery/raffle smart contract that ensures fairness through cryptographic randomness and automated operations. Users can participate by purchasing tickets with ETH, and winners are selected automatically using Chainlink's verifiable random number generation.

## ✨ Key Features

### 🎯 Core Functionality
- **Decentralized Lottery System**: Users enter by paying an entrance fee in ETH
- **Provably Random Winner Selection**: Uses Chainlink VRF v2.5 for cryptographically secure randomness
- **Automated Operation**: Chainlink Automation triggers lottery draws at regular intervals
- **Transparent & Fair**: All operations are on-chain and verifiable

### 🔒 Security Features
- **CEI Pattern**: Follows Checks-Effects-Interactions pattern for security
- **State Management**: Proper state transitions prevent race conditions
- **Access Control**: Only automated systems can trigger winner selection
- **Comprehensive Error Handling**: Custom errors for better gas efficiency and debugging

### 🛠 Technical Implementation
- **Built with Foundry**: Modern Solidity development framework
- **Chainlink Integration**: VRF v2.5 for randomness, Automation for triggers
- **Multi-Network Support**: Configured for Sepolia testnet and local development
- **Comprehensive Testing**: Unit tests with 100% coverage

## 🏗 Architecture

```
Raffle Contract
├── Entry System: Users pay entrance fee to participate
├── State Management: OPEN/CALCULATING states prevent conflicts
├── Automation Integration: Chainlink Keepers check conditions
├── VRF Integration: Request and receive random numbers
└── Winner Selection: Automated payout to randomly selected winner
```

## 🎮 How It Works

1. **Entry Phase**: Users call `enterRaffle()` with the required entrance fee
2. **Automation Check**: Chainlink Automation monitors if conditions are met:
   - Time interval has passed
   - Raffle is in OPEN state
   - Contract has ETH balance
   - At least one player is registered
3. **Winner Selection**: When conditions are met, `performUpkeep()` is triggered:
   - State changes to CALCULATING
   - Requests random number from Chainlink VRF
4. **Payout**: VRF callback selects winner and transfers entire balance

## 🚀 Quick Start

### Prerequisites
- [Foundry](https://getfoundry.sh/)
- [Node.js](https://nodejs.org/)

### Installation
```bash
git clone https://github.com/[your-username]/foundry-lottery
cd foundry-lottery
make install
```

### Local Development
```bash
# Start local blockchain
make anvil

# Deploy to local network
forge script script/DeployRaffle.s.sol:DeployRaffle --rpc-url http://localhost:8545 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 --broadcast
```

### Testing
```bash
# Run all tests
make test

# Run tests with coverage
forge coverage
```

## 🌐 Deployment

### Sepolia Testnet
```bash
make deploy-sepolia
```

### Environment Variables
Create a `.env` file with:
```env
SEPOLIA_RPC_URL=your_sepolia_rpc_url
PRIVATE_KEY=your_private_key
ETHERSCAN_API_KEY=your_etherscan_api_key
```

## 📋 Smart Contract Details

### Main Contract: `Raffle.sol`
- **Entry Fee**: Configurable minimum payment to participate
- **Interval**: Time between lottery rounds (configurable)
- **VRF Integration**: Chainlink VRF v2.5 for random number generation
- **Automation**: Chainlink Automation for decentralized execution

### Configuration: `HelperConfig.s.sol`
- **Multi-Network Support**: Sepolia and local configurations
- **Mock Deployments**: Automated mock contracts for testing
- **Dynamic Configuration**: Chain-specific parameters

### Testing Suite: `RaffleTest.t.sol`
- **Comprehensive Coverage**: Tests all contract functionality
- **Edge Cases**: Validates error conditions and state transitions
- **Integration Tests**: Full workflow testing with mocks

## 🔧 Technical Specifications

- **Solidity Version**: ^0.8.18
- **Framework**: Foundry
- **Oracle**: Chainlink VRF v2.5
- **Automation**: Chainlink Automation
- **Networks**: Ethereum Sepolia, Local development
- **Gas Optimization**: Efficient state management and custom errors

## 📊 Contract Functions

### Public Functions
- `enterRaffle()`: Join the lottery by paying entrance fee
- `checkUpkeep()`: View function to check if upkeep is needed
- `performUpkeep()`: Trigger winner selection (called by Automation)

### View Functions
- `getRaffleState()`: Current state (OPEN/CALCULATING)
- `getRecentWinner()`: Address of last winner
- `getNumberOfPlayers()`: Current participant count
- `getEntranceFee()`: Required payment to enter

## 🛡 Security Considerations

- **Reentrancy Protection**: CEI pattern implementation
- **State Validation**: Proper state checks before state changes
- **Randomness**: Chainlink VRF ensures unpredictable outcomes
- **Access Control**: Restricted functions prevent manipulation
- **Error Handling**: Comprehensive custom errors for all failure modes

## 🎯 Future Enhancements

- [ ] Multiple lottery pools with different entry fees
- [ ] NFT rewards for participants
- [ ] Referral system
- [ ] Frontend interface
- [ ] Historical winner tracking
- [ ] Emergency pause functionality

## 🤝 Contributing

Contributions are welcome! Please read our contributing guidelines and submit pull requests for any improvements.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙋‍♂️ Support

If you have questions or need help, please open an issue or contact the development team.

## 🔗 Links

- [Chainlink VRF Documentation](https://docs.chain.link/vrf)
- [Chainlink Automation Documentation](https://docs.chain.link/automation)
- [Foundry Documentation](https://book.getfoundry.sh/)

---

⚠️ **Disclaimer**: This is a educational project. Please ensure you understand the risks before deploying to mainnet or using with real funds.