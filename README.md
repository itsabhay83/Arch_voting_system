
# 🗳️ BlockBallot: A Trustworthy Decentralized Voting System

BlockBallot is a secure, transparent, and verifiable decentralized voting platform built on the Solana blockchain. Designed to reinforce trust in digital interactions, it ensures one-vote-per-wallet integrity, real-time results, and automatic closure of polls — all optimized for minimal gas usage.

## Features

- **Decentralized & Transparent**: Built on Solana to ensure votes are immutable, auditable, and secure.
- **Customizable Poll Creation**: Users can launch polls with configurable options, duration, and access control.
- **One-Vote-Per-Wallet Security**: On-chain enforcement of single vote per wallet prevents manipulation and fraud.
- **Real-Time Tallying**: See live voting results as votes are cast.
- **Time-Bound Polling**: Automatic poll closure based on duration set at creation.
- **Access Control**: Only authorized users can create and administer polls.
- **Optimized for Gas Efficiency**: Cost-effective transaction execution using Anchor and Solana.

## 🚀 Getting Started

### Prerequisites

- Node.js (v14 or later)
- Yarn package manager
- Solana CLI tools
- A Solana wallet (e.g., Phantom Wallet)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/sherwinvishesh/BlockBallot.git
cd BlockBallot
```
2. Install dependencies:
```bash
yarn install
```
3. Generate a New Wallet:
```bash
solana-keygen new -o id.json
```
4. Airdrop SOL into Wallet:
```bash
solana airdrop 4 <publicKey> --url devnet
```
5. Build the Anchor Project:
```bash
anchor build
```
6. Get Program ID:
```bash
solana address -k ./target/deploy/BlockBallot.json
```
7. Deploy the Anchor Program:
```bash
anchor deploy
```
8. Start the development server:
```bash
yarn dev
```

9. Open your browser and navigate to `http://localhost:3000` to view the application.

### Usage

1. Connect your Solana wallet to the application.
2. To create a poll, click on "Create Poll" and follow the prompts.
3. To vote in an existing poll, enter the poll code and select your choice.
4. View real-time results after voting.


## Technologies Used

- **Frontend**:
  - React.js
  - Tailwind CSS for styling
  - react-router-dom for routing

- **Blockchain**:
  - Solana blockchain
  - @solana/web3.js for Solana interactions
  - @project-serum/anchor for smart contract interactions

- **Wallet Integration**:
  - @solana/wallet-adapter for connecting to Solana wallets

- **Build Tools**:
  - Create React App
  - Webpack

- **Version Control**:
  - Git & GitHub


## Contributing

We welcome contributions from the community, especially those that enhance its blockchain capabilities. Feel free to fork the repository, make your improvements, and submit a pull request.

---


Made by Abhay








