# 🪂 Gasless Merkle Airdrop (EIP-712 + Foundry)

This repository contains a **production-style implementation of a gasless token airdrop system** using:

- Merkle Trees (for scalable distribution)
- ECDSA Signatures (for user authorization)
- EIP-712 (for secure structured signing)

Built using Foundry as part of an advanced smart contract + security learning journey.

---

## 🚀 Problem

Airdropping tokens to thousands of users is expensive and inefficient:

### ❌ Naive Approach
- Store all addresses on-chain
- Loop through them
- O(N) gas cost → not scalable

---

## ✅ Solution

### Merkle Airdrop + Signature-Based Claims

- Store only a **Merkle Root on-chain**
- Users prove eligibility using **Merkle Proofs**
- Users authorize claims via **EIP-712 signatures**
- A **relayer executes the transaction and pays gas**

👉 Result:
- O(log N) verification  
- Gasless UX for users  
- Secure + scalable distribution  

---

## 🏗️ Architecture Overview

### 🔹 1. Off-chain (Data Layer)
- Generate whitelist (address + amount)
- Build Merkle Tree using `murky`
- Export:
  - Merkle Root
  - Merkle Proofs

---

### 🔹 2. On-chain (Verification Layer)

#### `MerkleAirdrop.sol`

- Verifies:
  - Merkle Proof (eligibility)
  - EIP-712 Signature (authorization)

- Prevents:
  - Double claims
  - Signature replay / malleability issues

- Follows:
  - CEI Pattern
  - SafeERC20 usage

---

### 🔹 3. Authorization Layer (Signatures)

- User signs structured data: AirdropClaim(address account, uint256 amount)
- Uses: EIP-712 (domain separation + UX)
- OpenZeppelin ECDSA (safe recovery)

---

### 🔹 4. Execution Layer (Relayer)

- Relayer submits transaction:
- Pays gas
- Passes signature + proof

- Contract verifies everything → transfers tokens

---

## 🔁 End-to-End Flow

1. User signs claim message (off-chain)
2. Relayer submits transaction
3. Contract verifies:
 - Signature (ECDSA)
 - Merkle Proof
4. Tokens are transferred to user

---

## ⚙️ Project Structure

### 📦 Contracts

- `BagelToken.sol` → ERC20 token
- `MerkleAirdrop.sol` → Airdrop logic

---

### 🧪 Testing

- Foundry-based unit tests
- Uses real Merkle proofs
- Simulates users via `vm.prank()`

---

### ⚙️ Scripts

- `GenerateInput.s.sol` → whitelist generation  
- `MakeMerkle.s.sol` → Merkle tree + proofs  
- `DeployMerkleAirdrop.s.sol` → deployment + funding  
- `Interact.s.sol` → relayer execution  

---

### 🔧 CLI Workflow

- `cast call` → generate EIP-712 digest  
- `cast wallet sign --no-hash` → sign message  
- `forge script` → execute relayer transaction  

---

## 🔐 Signature Handling

- Raw signature = 65 bytes  
- `r` → first 32 bytes  
- `s` → next 32 bytes  
- `v` → final byte  

- Extracted using **Yul assembly** (`mload`)

---

## 🌍 Advanced Topics Covered

- Merkle Trees & Proofs  
- Gas optimization (O(N) → O(log N))  
- ECDSA (v, r, s)  
- EIP-712 structured signing  
- Signature malleability  
- Safe signature recovery (no raw `ecrecover`)  
- Meta-transactions (gasless UX)  
- Foundry scripting & automation  
- Ethereum vs zkSync execution differences  
- Transaction types (EIP-1559, blobs, AA)  

---

## ⚠️ Key Learnings

- Smart contracts don’t trust `msg.sender`  
→ they trust cryptographic proofs  

- Signing ≠ sending transactions  

- Off-chain computation + on-chain verification  
→ core Web3 design pattern  

---

## 📌 Status

✅ Module Complete  
🧠 Built as a learning + system design project  

---

## 📈 Learning in Public

This project was built while documenting progress daily on X (Twitter).

---

## 🤝 Connect & Collaborate

I'm actively seeking opportunities to contribute to Web3 projects and collaborate with other developers. Whether you're:
- 👨‍💼 A company looking for smart contract developers
- 🎓 A learner wanting to discuss these concepts
- 🛠️ A developer interested in collaboration
- 🔍 A recruiter evaluating technical skills

**Let's connect!**

- 💼 **LinkedIn:** [Siddharth Choudhary](https://www.linkedin.com/in/siddharth-choudhary-797391215/)
- 🐦 **X/Twitter:** [Sid_Hary_](https://x.com/Sid_Hary_)
- 📧 **Email:** sidforwork46@gmail.com


## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

## 🤝 Acknowledgements

* **Cyfrin Updraft** for the foundational knowledge.
---

**Made with ❤️ using Foundry**
