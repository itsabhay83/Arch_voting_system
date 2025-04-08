
# 🗳️ BlockBallot: A Trustworthy Decentralized Voting System

BlockBallot is a secure, transparent, and verifiable decentralized voting platform built on the Solana blockchain. Designed to reinforce trust in digital interactions, it ensures one-vote-per-wallet integrity, real-time results, and automatic closure of polls — all optimized for minimal gas usage.

## User Interface



https://github.com/user-attachments/assets/7c82994c-7b16-43ea-9a18-1f754bcb536d

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


# 📘 BlockBallot Code Documentation
BlockBallot is a decentralized voting system built with Solana and Anchor. This documentation explains the smart contract structure, core modules, data types, and interaction flow.

# 📁 Project Structure

            
            BlockBallot/
            ├── programs/
            │   └── blockballot/
            │       ├── src/
            │       │   ├── lib.rs          # Main program entry point
            │       │   └── context.rs      # Poll and vote context handlers
            │       │   └── state.rs        # Data structures
            │       │   └── errors.rs       # Custom errors
            ├── app/                        # React frontend
            ├── tests/                      # Anchor test cases


# 🧠 Smart Contract Overview (lib.rs)
The smart contract includes logic for:

**Poll Creation**

**Voting**

**Result Tallying**

**Time-bound Expiry**

# 🏗️ Key Instructions
# 1. create_poll
``` bash
#[derive(Accounts)]

pub struct CreatePoll<'info> {
    #[account(init, payer = user, space = Poll::LEN)]
    pub poll: Account<'info, Poll>,
    #[account(mut)]
    pub user: Signer<'info>,
    pub system_program: Program<'info, System>,
}
```
Creates a new poll.

Inputs:

question: String

options: Vec<String>

duration: i64 (in seconds)

State:

Poll account stores all poll data.

# 2. cast_vote
``` bash
#[derive(Accounts)]
pub struct CastVote<'info> {
    #[account(mut, has_one = poll)]
    pub vote: Account<'info, Vote>,
    #[account(mut)]
    pub poll: Account<'info, Poll>,
    pub user: Signer<'info>,
}
```
Casts a vote for a given option in a poll.

Constraints:

Each wallet can only vote once.

Voting after expiry is rejected.

# 📦 Data Structures (state.rs)
# Poll
```bash
#[account]
pub struct Poll {
    pub creator: Pubkey,
    pub question: String,
    pub options: Vec<String>,
    pub votes: Vec<u32>,
    pub expiry_time: i64,
    pub voters: Vec<Pubkey>, // to prevent double-voting
}
```
votes: Parallel to options, count of votes per option.

expiry_time: Unix timestamp when poll ends.

# Vote
```bash
#[account]
pub struct Vote {
    pub poll: Pubkey,
    pub voter: Pubkey,
    pub choice: u8, // Index of chosen option
}
```
# ⚠️ Error Handling (errors.rs)
```bash
#[error_code]
pub enum BlockBallotError {
    #[msg("Voting period has expired.")]
    PollExpired,
    #[msg("You have already voted.")]
    DuplicateVote,
    #[msg("Invalid option index.")]
    InvalidOption,
}
```
🧪 Test Suite (tests/blockballot.ts)
Includes:

Poll creation tests

Valid and invalid voting

Time-bound enforcement

Duplicate wallet prevention

Run with:

```bash
anchor test
```
# 🔗 Frontend Interaction (Web3)
# Key Solana libraries used:
```bash
import { Connection, PublicKey, Transaction } from "@solana/web3.js";
import { Program, AnchorProvider } from "@project-serum/anchor";
Poll creation: program.rpc.createPoll(...)

Voting: program.rpc.castVote(...)

Fetch poll: program.account.poll.fetch(pollPubKey)
```

📌 Notes
Expiry time is validated on-chain for deterministic trust.

Voter list is stored in Poll account to check if wallet already voted.

All on-chain data is stored using Anchor serialization.

---


Made by Abhay

















