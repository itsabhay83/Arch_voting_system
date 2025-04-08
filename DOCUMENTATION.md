# 📘 BlockBallot Code Documentation
BlockBallot is a decentralized voting system built with Solana and Anchor. This documentation explains the smart contract structure, core modules, data types, and interaction flow.

# 📁 Project Structure
**plaintext**
            Copy
            Edit
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