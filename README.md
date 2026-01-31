# SwiftRide-Ledger
Ledger-first transaction system for WhatsApp-based mobility payments.
# SwiftRide Ledger

SwiftRide Ledger is the transaction backbone for the SwiftRide mobility system.
It records, tracks, and governs all ride-related and payment-related activities
using a transparent, auditable ledger-first approach.

The ledger is designed to operate with:
- WhatsApp as the user interface
- Google Sheets as the initial ledger store
- CodeBank governance rules for compliance and expansion

This repository defines the **rules**, not just the data.

---

## Core Principles

- Every action is a transaction
- Every transaction has a unique ID
- Every transaction has a status
- No transaction is invisible
- No balance is implied — only recorded

---

## Supported Transaction Types

- TOP_UP
- DEBIT
- RIDE_PAYMENT
- DRIVER_PAYOUT
- REVERSAL
- ADJUSTMENT

---

## Transaction Lifecycle

PENDING → VERIFIED → APPROVED → COMPLETED  
FAILED / REVERSED (terminal states)

---

## Initial Deployment

Phase 1 uses:
- Google Forms for input
- Google Sheets as the ledger
- Apps Script for automation
- WhatsApp Business for user interaction

Later phases migrate to APIs and databases without changing ledger rules.

---

## Relationship to CodeBank

# SwiftRide Ledger Schema

Each row in the ledger represents ONE transaction.

## Required Fields

| Field Name | Description |
|----------|-------------|
| Transaction_ID | Unique system-generated ID |
| Timestamp | Time transaction entered system |
| User_WhatsApp | WhatsApp number initiating transaction |
| Transaction_Type | TOP_UP, DEBIT, RIDE_PAYMENT |
| Amount_ZAR | Monetary value |
| Reference | External or internal reference |
| Channel | WhatsApp |
| Status | PENDING, APPROVED, COMPLETED, FAILED |
| Source | Google Form / WhatsApp |
| Notes | Optional system or operator notes |

No calculated balances are stored.
Balances are derived from transaction history.


SwiftRide Ledger is a vertical implementation of CodeBank Core Ledger Logic.
All rules defined here must remain compatible with CodeBank governance standards.
