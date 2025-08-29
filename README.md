CrowdStacks – Decentralized Crowdfunding on Stacks

A milestone-based crowdfunding platform built on the Stacks blockchain. Campaign funds are escrowed in smart contracts and released only when goals are met, ensuring accountability for backers and creators.

Quick Start
Prerequisites

Node.js 18+

Docker Desktop

Clarinet CLI (npm install -g @hirosystems/clarinet)

Installation
# Install dependencies
npm install

# Start local Clarinet devnet
cd contracts && clarinet integrate

# Launch frontend (in a new terminal)
npm run dev


Visit http://localhost:3000
 to access the DApp.

Testing
npm test

# or directly in Clarinet console
cd contracts && clarinet console
(contract-call? .crowdfunding contribute u5000000)

Project Structure

/contracts/ – Clarity smart contracts and tests

/app/ – Next.js frontend application

/components/ – Reusable UI components

/lib/ – Blockchain helpers and config

/public/ – Static assets

Demo Workflow

Start local blockchain with Clarinet

Launch frontend (npm run dev)

Create a campaign

Contribute STX to campaign

Confetti triggers when goal is reached

Withdraw funds (if successful) or request refund

Documentation

See ABOUT.md for technical architecture and implementation details.
