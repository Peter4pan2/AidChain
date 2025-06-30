# AidChain - Blockchain  Governance Fund Contract

A Clarity smart contract for securely managing donations and withdrawals in a decentralized disaster-relief funding system. This governance contract ensures responsible fund distribution, with admin control, donor protection, and multi-signer transaction execution.

---

## 📑 Table of Contents

* [Overview](#overview)
* [Features](#features)
* [Contract Components](#contract-components)

  * [Data Variables](#data-variables)
  * [Core Functions](#core-functions)
  * [Validation Rules](#validation-rules)
  * [Multisig Governance](#multisig-governance)
* [Error Codes](#error-codes)
* [Security Considerations](#security-considerations)
* [License](#license)

---

## 📘 Overview

This smart contract is intended to support **decentralized governance** of a disaster-relief fund. It offers:

* Admin-only configurable rules
* Donation and withdrawal validation logic
* Signer-based approval of sensitive transactions
* Immutable, blockchain-based audit trail

---

## ✅ Features

* 🔐 **Admin privileges** for updating rules and permissions
* 💸 **Minimum donation enforcement**
* 💳 **Withdrawal limits per recipient**
* 👥 **Multisig transaction proposals and approvals**
* 🔍 Transparent access to pending and approved actions

---

## 🔧 Contract Components

### 🗂️ Data Variables

| Variable              | Type        | Description                                   |
| --------------------- | ----------- | --------------------------------------------- |
| `admin`               | `principal` | Address with special permissions              |
| `min-donation`        | `uint`      | Minimum donation threshold                    |
| `withdrawal-limit`    | `uint`      | Max allowed withdrawal per recipient          |
| `required-signatures` | `uint`      | Signatures needed to execute critical actions |
| `tx-nonce`            | `uint`      | Incremental ID generator for transactions     |

---

### ⚙️ Core Functions

#### 🔧 Admin Functions

* `set-admin(new-admin)` – Change contract administrator
* `set-min-donation(amount)` – Set minimum donation amount
* `set-withdrawal-limit(amount)` – Set withdrawal limit
* `set-required-signatures(amount)` – Adjust number of required multisig approvals

#### 📖 Read-only Accessors

* `get-admin()` – Returns current admin address
* `get-min-donation()` – Returns current minimum donation requirement
* `get-withdrawal-limit()` – Returns current withdrawal limit
* `get-required-signatures()` – Returns number of required signer approvals

---

### 🔍 Validation Rules

* `validate-donation(amount)` – Ensures donations meet minimum requirement
* `validate-withdrawal(amount)` – Ensures withdrawals are within allowed limits

---

### 🔐 Multisig Governance

| Function                              | Description                                    |
| ------------------------------------- | ---------------------------------------------- |
| `add-signer(new-signer)`              | Add a new signer (admin-only)                  |
| `remove-signer(signer)`               | Remove an existing signer (admin-only)         |
| `propose-transaction(action, params)` | Submit a new multisig transaction for approval |
| `get-pending-transaction(tx-id)`      | View transaction details                       |
| `get-tx-nonce()`                      | View the latest transaction nonce              |
| `is-signer(address)`                  | Check if an address is a recognized signer     |

> `execute-transaction(tx-id)` is a private function that would be invoked internally once sufficient approvals are collected.

---

## ⚠️ Error Codes

| Code   | Meaning                                    |
| ------ | ------------------------------------------ |
| `u401` | Unauthorized access                        |
| `u402` | Invalid donation or transaction parameters |
| `u403` | Invalid configuration or signer state      |
| `u404` | Not found / invalid address                |
| `u405` | Withdrawal amount exceeds allowed limit    |

---

## 🔐 Security Considerations

* Prevents admin assignment to zero address (`SP000000000000000000002Q6VF78`)
* Limits transaction parameter sizes and count
* Uses nonce to avoid ID collisions in pending transactions
* Allows only valid signers to propose/approve multisig actions

---

## 🪪 License

This smart contract is open-source under the [MIT License](https://opensource.org/licenses/MIT). You may use, modify, and distribute it as per the terms of the license.

---
