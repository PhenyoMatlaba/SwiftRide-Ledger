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

# Transaction Flow

1. User submits request via WhatsApp
2. Data is captured via Google Form
3. Entry is written to Ledger Sheet
4. System assigns Transaction_ID
5. Status is set to PENDING
6. Operator or automation verifies
7. Status updated accordingly
8. User is notified via WhatsApp

At no point is money assumed.
Only confirmed transactions change status.

# Transaction Status Rules

## PENDING
- Default state on creation
- No financial effect

## VERIFIED
- Data checked
- Awaiting approval

## APPROVED
- Accepted by system/operator
- Ready for settlement

## COMPLETED
- Financial action confirmed
- Final state

## FAILED
- Invalid or rejected
- No retry without new transaction

## REVERSED
- Used only if COMPLETED was incorrect
- Requires audit entry
# Audit Log Rules

Every status change creates an audit entry.

Audit entries must include:
- Audit_ID
- Timestamp
- Transaction_ID
- Old_Status
- New_Status
- Actor (System / Operator)
- Reason

Audit logs are immutable.

# WhatsApp Flow Mapping

WhatsApp is the front-end, not the ledger.

User actions:
- Send message
- Click quick reply
- Submit form link

System actions:
- Read ledger
- Update status
- Respond with confirmation

WhatsApp never stores balances.
It only reflects ledger truth.
# Google Sheets Mapping

Ledger Sheet = Source of truth

Rules:
- No manual edits to Status column
- Transaction_ID auto-generated only
- Append-only (no deletions)

Apps Script enforces these rules.
# Changelog

## v1.0.0
- Initial ledger schema
- Google Sheets deployment
- WhatsApp-first flow

