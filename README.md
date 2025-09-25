
#  Skill-MintX - Talent Marketplace Smart Contract

A decentralized talent marketplace that enables verified talent to offer services via time-bound auctions. Clients can bid for these services, and talent can complete the auction and earn STX, while the platform collects a small fee.

---

## 📜 Table of Contents

* [Overview](#overview)
* [Features](#features)
* [Contract Details](#contract-details)
* [Constants](#constants)
* [Error Codes](#error-codes)
* [Data Structures](#data-structures)
* [Functions](#functions)

  * [Public Functions](#public-functions)
  * [Read-only Functions](#read-only-functions)
* [Usage Flow](#usage-flow)
* [Security & Validations](#security--validations)
* [Stats & Metrics](#stats--metrics)
* [Future Improvements](#future-improvements)

---

## 📖 Overview

This smart contract enables a **Talent Auction System** on the Stacks blockchain. Verified users (talents) can create auctions offering their services, and other users (clients) can bid on these auctions using STX tokens.

Auctions are competitive and time-bound. Once ended, the highest bidder wins, and the talent receives the payment (minus a platform fee).

---

## 🚀 Features

* Talent registration with verification
* Auction creation with price, category, and time-bound duration
* Secure bidding with bid increments and balance checks
* Automatic fund transfers to winning talents
* Fee collection mechanism for platform sustainability
* Error handling for robust user experience
* Transparent read-only views for audits and front-end display

---

## 🔍 Contract Details

| Parameter        | Value                          |
| ---------------- | ------------------------------ |
| Language         | Clarity                        |
| Platform         | Stacks Blockchain              |
| Contract Purpose | Talent Auction Marketplace     |
| Fee Rate         | 5% (configurable via constant) |
| Min/Max Auction  | 1 day to 30 days               |
| Price Bounds     | 1 STX to 1,000,000 STX         |

---

## 📌 Constants

| Constant Name          | Value            | Description                       |
| ---------------------- | ---------------- | --------------------------------- |
| `FEE-RATE`             | `u50`            | Platform fee (5%) in basis points |
| `MIN-AUCTION-DURATION` | `u144`           | 1 day (blocks)                    |
| `MAX-AUCTION-DURATION` | `u4320`          | 30 days (blocks)                  |
| `MIN-PRICE`            | `u1000000`       | Minimum auction price (1 STX)     |
| `MAX-PRICE`            | `u1000000000000` | Maximum price (1,000,000 STX)     |

---

## ❗ Error Codes

| Error Code                        | Meaning                        |
| --------------------------------- | ------------------------------ |
| `u1`   - `ERR-NOT-AUTHORIZED`     | Unauthorized access            |
| `u2`   - `ERR-INVALID-STATE`      | Invalid state for action       |
| `u3`   - `ERR-NOT-FOUND`          | Item not found                 |
| `u4`   - `ERR-INVALID-DURATION`   | Auction duration invalid       |
| `u5`   - `ERR-INSUFFICIENT-FUNDS` | STX balance insufficient       |
| `u6`   - `ERR-ALREADY-REGISTERED` | Talent already registered      |
| `u7`   - `ERR-INVALID-PRICE`      | Price not within valid range   |
| `u8`   - `ERR-AUCTION-EXPIRED`    | Auction has ended              |
| `u9`   - `ERR-AUCTION-NOT-ENDED`  | Auction still ongoing          |
| `u10`  - `ERR-SELF-BIDDING`       | Cannot bid on your own auction |
| `u11`  - `ERR-INVALID-BID`        | Bid too low or invalid         |
| `u12`  - `ERR-EMPTY-TITLE`        | Auction title is required      |
| `u13`  - `ERR-EMPTY-DESCRIPTION`  | Description is required        |
| `u14`  - `ERR-EMPTY-CATEGORY`     | Category is required           |
| `u15`  - `ERR-AUCTION-NOT-ACTIVE` | Auction is not in active state |

---

## 🗂️ Data Structures

### 🔹 Talents (Map)

```clojure
(define-map talents principal { verified, rating, total-earnings, auctions-completed, registration-height })
```

### 🔹 Auctions (Map)

```clojure
(define-map auctions uint {
    talent, title, description, price,
    end-height, highest-bid, highest-bidder,
    status, category, creation-height
})
```

### 🔹 Global Data Vars

```clojure
next-auction-id            ;; Unique auction ID tracker
total-auctions-completed   ;; Stats counter
total-fees-collected       ;; Total fees for contract owner
```

---

## 📥 Public Functions

### ✅ `register-talent`

Registers the sender as a verified talent.

* Fails if already registered.

---

### ✅ `create-auction (title, description, category, price, blocks)`

Creates a new auction.

* Duration must be within min/max range.
* Price must be valid.
* Fields must not be empty.

Returns: `auction-id`

---

### ✅ `place-bid (auction-id, amount)`

Places a bid on an auction.

* Must be higher than current bid + 5%.
* Refunds previous bidder.
* Transfers fee to platform.

---

### ✅ `complete-auction (auction-id)`

Completes the auction by the talent once the deadline is over.

* Transfers funds to the talent.
* Updates talent statistics and auction status.

---

## 🔍 Read-only Functions

| Function                            | Description                                              |
| ----------------------------------- | -------------------------------------------------------- |
| `get-auction (auction-id)`          | Returns auction details                                  |
| `get-talent-info (address)`         | Returns talent profile                                   |
| `get-contract-stats`                | Returns global stats like total auctions, fees collected |
| `is-registered (address)`           | Checks if address is registered                          |
| `can-complete-auction (auction-id)` | Checks if auction is ready to be completed               |

---

## 🔄 Usage Flow

1. **Talent Registration**

   * Call `register-talent`.

2. **Auction Creation**

   * Call `create-auction` with details.

3. **Bidding**

   * Clients call `place-bid` with STX.

4. **Auction Completion**

   * After deadline, talent calls `complete-auction`.

5. **Fee Collection**

   * Contract owner receives 5% of each winning bid.

---

## 🔒 Security & Validations

* **No self-bidding** allowed.
* **Bid increment enforcement** (5% minimum).
* **Balance checks** before transfer.
* **State validation** before any update.
* **Auction expiry** strictly enforced.

---

## 📈 Stats & Metrics

* `total-auctions-completed`: For tracking platform usage.
* `total-fees-collected`: Contract owner revenue.
* `talent` profile includes:

  * `total-earnings`
  * `auctions-completed`
  * `rating` (reserved for future)
  * `verified` status

---

## 🛠️ Future Improvements

* Reputation/rating system for talents
* Filtering auctions by category
* On-chain feedback/review mechanism
* NFT proof of service completion
* Decentralized dispute resolution

---
