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

**Out of scope (v1):** milestone gating, AI budget scoring, sectorized buckets, fiat on-ramps.

---

## Why this exists (short narrative)

Indie crowdfunding often fails on accountability. High-profile projects (LA Game Space, Yogventures!, The Stomping Land) burned trust. CrowdStacks doesn’t try to judge games or micromanage delivery in v1. It adds a minimal guardrail:

- Backers see transparent on-chain progress.
- Funds don’t move until the **single** target is reached.
- If the project misses, backers can self-serve refunds.

This avoids heavy “milestone lock” friction that many indie devs resist and keeps the MVP shippable.

---

## Trade-offs / Risks

- No milestone gates → some backers will want finer control.
- If creators need upfront cash, this model can be too strict.
- Competes with Kickstarter/Indiegogo/Patreon attention.
- Budget “judgment” and AI estimation are deferred to a later version.

---

## Install & Run

**Prereqs**
- Node.js 18+
- Docker Desktop
- Clarinet
  ```bash
  npm install -g @hirosystems/clarinet
Setup

bash
Copy code
# deps
npm install

# start local Stacks devnet
cd contracts
clarinet integrate
Frontend

bash
Copy code
# new terminal (project root)
npm run dev
# open http://localhost:3000
Testing
bash
Copy code
npm test
Clarinet console:

bash
Copy code
cd contracts
clarinet console
Example call:

clarity
Copy code
(contract-call? .crowdfunding contribute u1000000)
Project Structure
/contracts — Clarity contract + tests

/app — Next.js app router pages

/page.tsx (Home)

/create/page.tsx (Create)

/admin/page.tsx (Admin)

/lib/stacks.ts — network + contract helpers

/public — static assets

Contract Notes (v4)
campaigns map holds: owner, title, description, goal (µSTX), total, deadline, active, deleted, contributor-count.

contributions map: {campaign-id, contributor} -> amount.

Withdraw path: owner only, campaign active, total >= goal.

Refund path: deadline > 0, past deadline, total < goal.

Finalize failure: closes an expired, failed campaign.

Wallet / Postconditions
Leather shows “no transfers” unless you allow spend:

Use Deny mode with a standard STX postcondition:

makeStandardSTXPostCondition(sender, LessEqual, amountµ)

If you omit it (or set Deny with empty list), contribution will abort by postcondition.

Failure Modes to Watch
Wrong contract address/name in pages → all reads/writes hit the wrong deployment.

Passing only amount to contribute (missing campaign-id) → signature mismatch.

Deny mode without postconditions → abort_by_post_condition.

Title/description length > limits or non-ASCII → Clarity rejects.

Next Steps (after MVP)
Optional milestone unlocks (opt-in), not hard locks.

Optional AI budget sanity checks (advisory only).

Off-chain media proofing + on-chain references.
