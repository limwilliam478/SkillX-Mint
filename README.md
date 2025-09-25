

# SkillX-Mint - Talent Marketplace & CosmoFund Smart Contract Suite

## Overview

This project is a comprehensive suite of Clarity smart contracts for the **Stacks blockchain**, combining two decentralized applications:

1. **Talent Marketplace** – A trust-based auction platform for verified talents to showcase their skills and sell services.
2. **CosmoFund** – A decentralized crowdfunding platform for funding space exploration or other high-impact projects.

Together, these contracts offer secure, permissionless, and transparent interactions using native STX tokens, empowering both individuals and communities.

---

## 📦 Modules

### 1. Talent Marketplace

A decentralized platform where verified individuals ("talents") can auction their services to the highest bidder, with built-in rating, earnings tracking, and error handling.

#### Key Features

* ✅ **Talent Registration** with verification and activity tracking.
* 📢 **Auction Creation** with strict validation (min/max duration, pricing).
* 💸 **Secure Bidding** with anti-self-bidding and automatic refunds for outbid participants.
* 🏁 **Auction Completion** with automatic earnings transfer and performance stats updates.
* 🔐 **Comprehensive Error Handling** and state validation.

#### Constants

* `FEE-RATE`: 5% platform fee.
* `MIN/MAX-AUCTION-DURATION`: 1 to 30 days.
* `MIN/MAX-PRICE`: 1 STX to 1,000,000 STX.

#### Error Codes

Handled via `err u1` to `err u15`, covering authorization, state, bidding logic, string validation, and auction status.

#### Public Functions

* `register-talent`
* `create-auction`
* `place-bid`
* `complete-auction`

#### Read-Only Utilities

* `get-auction`
* `get-talent-info`
* `get-contract-stats`
* `is-registered`
* `can-complete-auction`

---

### 2. CosmoFund (Decentralized Crowdfunding)

A decentralized fundraising contract where project creators raise funds with optional voting for fund release. It includes built-in voting, deadline extensions, and refund logic.

#### Key Features

* 🌌 **Project Submission** with name, funding goal, and deadline.
* 🙋 **Contributions** using STX.
* ✅ **On-chain Voting** for fund release decisions.
* 🔄 **Deadline Extensions** based on funding milestones.
* 🔒 **Withdrawals & Refunds** with threshold-based governance.

#### Constants

* `EXTENSION_THRESHOLD`: 75% raised before extension allowed.
* `VOTING_PERIOD_DAYS`: 7 days.
* `MIN_VOTE_THRESHOLD_PERCENT`: 60%.
* `MIN_VOTE_COUNT_THRESHOLD`: 10 votes.

#### Public Functions

* `submit-project`
* `contribute`
* `vote`
* `withdraw-funds`
* `refund`
* `cancel-project`
* `extend-deadline`

#### Read-Only Utilities

* `get-project`
* `get-contribution`
* `get-vote`
* `get-voting-status`

---
