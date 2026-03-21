# 🪂 Merkle Airdrop & Signatures (WIP)

This repository contains my implementation of a **gas-efficient and secure token airdrop system** using **Merkle Trees and ECDSA signatures (gasless claims)**.

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
- Users authorize claims via **signatures (gasless UX)**

---

## 🏗️ Current Implementation

### 🥯 Smart Contracts

#### BagelToken.sol
- Minimal ERC20 token using OpenZeppelin
- Owner-controlled minting

#### MerkleAirdrop.sol
- Merkle Proof verification
- Double-claim protection
- CEI pattern (reentrancy-safe)
- SafeERC20 transfers
- Gas optimized with `immutable`

### 🔐 Signature-Based Claims (NEW)

- EIP-712 structured data signing
- ECDSA signature verification (OpenZeppelin)
- Prevents unauthorized claims
- Enables **gasless airdrop via relayers**

Flow:
1. User signs message off-chain  
2. Relayer submits transaction  
3. Contract verifies signature + Merkle proof  
4. Tokens are transferred  

---

### ⚙️ Off-chain Infrastructure (Foundry Scripts)

#### GenerateInput.s.sol
- Creates whitelist data (addresses + token amounts)

#### MakeMerkle.s.sol
- Generates Merkle Tree using `murky`
- Outputs root + proofs

#### DeployMerkleAirdrop.s.sol
- Deploys contracts
- Mints tokens
- Funds airdrop contract

#### Interact.s.sol (Relayer)
- Simulates relayer submitting claims
- Uses signature + proof

---

### 🧪 Testing

- Unit tests using Foundry
- Uses real Merkle proofs
- `vm.prank()` for simulating users
- Validates claim execution

---

## 🔐 Key Concepts Covered

- Merkle Trees & Proofs
- Gas optimization (O(N) → O(log N))
- Off-chain computation + on-chain verification
- ECDSA (v, r, s signatures)
- EIP-712 structured data signing
- Signature verification & replay protection
- CEI pattern
- Safe ERC20 interactions
- Deployment scripting
- Relayer-based execution

---

## ⚠️ Work In Progress

### 🔜 Upcoming:
- Signature splitting (v, r, s from raw signature)
- Full relayer automation
- Advanced testing for signatures
- Potential frontend / integration

---

## 📈 Learning in Public

I’m documenting this journey daily on X (Twitter), sharing:
- What I learn
- What I build
- Key insights

---

## 🛠️ Tech Stack

- Solidity
- Foundry
- OpenZeppelin
- Murky

---

## 📌 Status

🟡 In Progress — now implementing **gasless signature-based claims**

---

## 🤝 Feedback

Open to suggestions, improvements, and discussions!