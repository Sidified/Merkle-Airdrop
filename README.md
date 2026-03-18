# 🪂 Merkle Airdrop & Signatures (WIP)

This repository contains my implementation of a **gas-efficient and secure token airdrop system** using **Merkle Trees and (upcoming) ECDSA signatures**.

The goal of this project is to understand and build the same architecture used by real-world protocols (like Uniswap, Arbitrum) to distribute tokens at scale.

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

### 🥯 BagelToken.sol
- Minimal ERC20 token using OpenZeppelin
- Owner-controlled minting

### 🌳 MerkleAirdrop.sol
- Merkle Proof verification using OpenZeppelin
- Double-claim protection using mapping
- Follows **CEI (Checks-Effects-Interactions)** pattern
- Uses **SafeERC20** for secure transfers
- Gas-optimized with `immutable` variables

---

## 🔐 Key Concepts Covered

- Merkle Trees & Proofs
- Gas optimization (O(N) → O(log N))
- Double hashing for security
- CEI pattern (reentrancy prevention)
- Safe ERC20 interactions

---

## ⚠️ Work In Progress

This project is actively being built as part of my **Advanced Foundry / Smart Contract Security journey**.

### 🔜 Upcoming Features:
- ECDSA Signature verification
- Gasless claims via relayers
- Foundry scripts for:
  - Merkle tree generation
  - Deployment
  - Interaction
- Extensive testing

---

## 📈 Learning in Public

I’m documenting this journey daily on X (Twitter), sharing:
- What I learn
- What I build
- Key insights

This repo will evolve alongside those posts.

---

## 🛠️ Tech Stack

- Solidity
- Foundry
- OpenZeppelin

---

## 📌 Status

🟡 In Progress — actively building and improving

---

## 🤝 Feedback

If you have suggestions or spot improvements, feel free to open an issue or reach out!