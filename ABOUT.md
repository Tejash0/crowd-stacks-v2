# CrowdStacks — About

CrowdStacks is a crowdfunding dApp for indie games on the Stacks blockchain. It focuses on basic accountability without changing how creators work: contributions are escrowed on-chain and **can only be withdrawn if the campaign meets its funding goal**. If a deadline is set and the goal isn’t met, contributors can **claim refunds**. No milestone locks in v1.

---

## Scope (MVP)

- **On-chain campaigns**
  - `create-campaign(title, description, goal, deadline|0)`
  - Soft delete/archive; title/description edits; goal/deadline updates (owner only)

- **Funding**
  - `contribute(campaign-id, amount)` (escrows STX in contract)
  - **Withdraw** only when `total >= goal` and campaign is active
  - **Refunds**: if `deadline > 0 && block-height > deadline && total < goal`

- **Read-onlys**
  - Totals, active counts, per-campaign status, user contribution

- **Frontend**
  - Home (list + contribute), Create (form), Admin (owner CRUD)
  - Leather wallet; explicit STX postconditions for contributions

> **Out of scope (v1):** milestone gating, AI budget scoring, sectorized buckets, fiat on-ramps.

---

## Why this exists (short narrative)

Indie crowdfunding often fails on accountability. High-profile projects (LA Game Space, Yogventures!, The Stomping Land) burned trust. CrowdStacks doesn’t try to judge games or micromanage delivery in v1. It adds a minimal guardrail:

- Backers see transparent on-chain progress.
- Funds don’t move until the **single** target is reached.
- If the project misses, backers can self-serve refunds.

This avoids heavy “milestone lock” friction that many indie devs resist and keeps the MVP shippable.

---

## Trade-offs / Risks

- **No milestone gates** — some backers will want finer control.
- If creators need **upfront cash**, this model can be too strict.
- **Competes** with Kickstarter/Indiegogo/Patreon attention.
- Budget “judgment” and AI estimation are **deferred** to a later version.

---

## Install & Run

### Prerequisites
- Node.js 18+
- Docker Desktop
- Clarinet
  ```bash
  npm install -g @hirosystems/clarinet
