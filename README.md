# 🪂 Merkle Airdrop & Signatures (WIP)

This repository contains my implementation of a **gas-efficient and secure token airdrop system** using **Merkle Trees and (upcoming) ECDSA signatures**.

The goal is to understand and build the same architecture used by real-world protocols (like Uniswap, Arbitrum) to distribute tokens at scale.

---

## 🚀 What This Project Solves

Airdropping tokens to thousands of users is expensive and inefficient if done naively.

### ❌ Naive Approach:
- Store all addresses on-chain
- Loop through them
- Extremely high gas costs (O(N))

### ✅ This Approach:
- Store only a **Merkle Root on-chain**
- Users prove eligibility using **Merkle Proofs**
- Verification cost becomes **O(log N)**

---

## 🏗️ Current Implementation

### 🥯 Smart Contracts

#### BagelToken.sol
- Minimal ERC20 token using OpenZeppelin
- Owner-controlled minting

#### MerkleAirdrop.sol
- Merkle Proof verification using OpenZeppelin
- Double-claim protection
- Follows **CEI (Checks-Effects-Interactions)** pattern
- Uses **SafeERC20** for secure transfers
- Gas-optimized with `immutable` variables

---

### ⚙️ Off-chain Infrastructure (Foundry Scripts)

#### GenerateInput.s.sol
- Creates whitelist data (addresses + token amounts)
- Outputs structured JSON

#### MakeMerkle.s.sol
- Generates Merkle Tree using `murky`
- Outputs:
  - Merkle Root
  - Proofs for each user

#### DeployMerkleAirdrop.s.sol
- Deploys contracts
- Mints tokens
- Funds the airdrop contract

---

### 🧪 Testing

- Unit tests using Foundry
- Uses real Merkle proofs from generated JSON
- `vm.prank()` to simulate user interactions
- Validates successful token claims

---

## 🔐 Key Concepts Covered

- Merkle Trees & Proofs
- Gas optimization (O(N) → O(log N))
- Off-chain computation + on-chain verification
- Double hashing for security
- CEI pattern (reentrancy prevention)
- Safe ERC20 interactions
- Deployment scripting
- Testing with real cryptographic data

---

## ⚠️ Work In Progress

This project is actively being built as part of my **Advanced Foundry / Smart Contract Security journey**.

### 🔜 Upcoming Features:
- ECDSA Signature verification
- Gasless claims via relayers
- EIP-712 typed structured data
- Signature validation inside `claim()`

---

## 📈 Learning in Public

I’m documenting this journey daily on X (Twitter), sharing:
- What I learn
- What I build
- Key insights

This repo evolves alongside those posts.

---

## 🛠️ Tech Stack

- Solidity
- Foundry
- OpenZeppelin
- Murky (Merkle Tree generation)

---

## 📌 Status

🟡 In Progress — transitioning from Merkle proofs → signature-based claims

---

## 🤝 Feedback

If you have suggestions or spot improvements, feel free to open an issue or reach out!