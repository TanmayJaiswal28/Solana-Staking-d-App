# Solana Staking Dapp  

**A starter template for building a Solana staking decentralized application** – combines a React + Next.js frontend with wallet connectivity and the Anchor‑generated IDL for a Solana staking program.

## Overview  

This repository provides the front‑end scaffold for a Solana staking DApp. It includes:

- A Next.js (v13) application written in React 18.  
- Wallet integration via `@solana/wallet-adapter` (Phantom, Solflare, etc.).  
- UI components for staking, unstaking, claiming rewards and basic admin actions.  
- The Anchor IDL (`lib/idl.json`) that describes the on‑chain staking program (instructions such as `initialize`, `stake`, `unstake`, `claimRewards`, `addRewards`, …).

The template is intended as a **starting point**; you must compile and deploy the Rust Anchor program separately and configure the front‑end to point at the deployed program’s address.

## Features  

| Feature | Description |
|---------|-------------|
| **Wallet connection** | `components/WalletConnect.js` lets users connect a Solana wallet. |
| **Stake / Unstake** | `components/StakeForm.js` and `components/UnstakeForm.js` call the `stake` and `unstake` instructions from the IDL. |
| **Claim rewards** | `components/ClaimRewards.js` invokes the `claimRewards` instruction. |
| **Admin panel** | `components/AdminPanel.js` (available under `/admin`) provides UI for adding rewards, withdrawing tokens and updating the reward rate. |
| **Staking statistics** | `components/StakingStats.js` displays pool‑level data (total staked, reward rate, etc.). |
| **Responsive styling** | Tailwind CSS with a custom primary/secondary palette. |
| **Static export support** | `next.config.js` sets `output: "export"` so the app can be built as a static site. |

## Tech Stack  

- **Framework**: Next.js 13 (React 18)  
- **Styling**: Tailwind CSS 3  
- **Solana SDK**: `@solana/web3.js`, `@solana/spl-token`  
- **Wallet adapters**: `@solana/wallet-adapter-base`, `@solana/wallet-adapter-react`, `@solana/wallet-adapter-react-ui`, `@solana/wallet-adapter-wallets`  
- **Anchor integration**: `@project-serum/anchor` (loads the IDL)  
- **Utilities**: `react-hot-toast` for notifications, `bs58` for base58 encoding  

## Getting Started  

### Prerequisites  

- Node ≥ 18  
- npm (scripts use npm)  
- A deployed Solana staking program compiled with Anchor (the IDL in `lib/idl.json` must match the on‑chain program).  

### Installation  

```bash
# Clone the repository
git clone https://github.com/TanmayJaiswal28/Solana-Staking-d-App.git
cd Solana-Staking-d-App/Solana-Staking-Dapp

# Install dependencies
npm install
```

### Configuration  

Create a `.env.local` file (you can start from the existing template) and set at least:

```env
NEXT_PUBLIC_SOLANA_RPC=https://api.devnet.solana.com
NEXT_PUBLIC_STAKING_PROGRAM_ID=YourProgramPublicKey
```

These variables are read by the front‑end to connect to the Solana RPC endpoint and to locate the deployed staking program.

### Development  

```bash
npm run dev
```

The app will be available at `http://localhost:3000`.

### Build / Static Export  

```bash
npm run build   # builds and exports to the `out` directory
npm run start   # serves the exported site (requires a static server)
```

To clean the workspace:

```bash
npm run clear
```

## Project Structure (high‑level)  

```
app/
│   layout.js          – global layout (includes DashboardLayout)
│   page.js            – placeholder landing page
│   admin/page.js      – admin UI
│   stake/page.js      – staking UI
│   rewards/page.js    – rewards UI
components/
│   WalletConnect.js
│   StakeForm.js
│   UnstakeForm.js
│   ClaimRewards.js
│   AdminPanel.js
│   StakingStats.js
│   DashboardLayout.js
│   WithdrawTokens.js
contexts/
│   WalletContext.js   – React context for wallet state
hooks/
│   useStakingContract.js – wrapper around Anchor program calls
lib/
│   idl.json            – Anchor IDL for the staking program
utils/
│   constants.js
│   helpers.js
public/
│   images/…            – logo and background assets
styles/
│   globals.css
tailwind.config.js
postcss.config.js
next.config.js
package.json
```

## Current Status & Limitations  

- **Front‑end only** – the repository does **not** include the compiled Solana program; you must build and deploy the Rust Anchor contract (`Solana-Staking-Dapp/Contract/SolanaICO.rs`) separately.  
- The default `app/page.js` renders a simple placeholder (`<div>page</div>`); replace it with your own landing/dashboard as needed.  
- No environment‑variable validation is built in; missing RPC or program ID will cause runtime errors.  
- No automated tests, CI pipelines, or licensing information are provided.  
- The UI is functional but minimal; further styling and UX improvements are expected.  

## Contributing  

Contributions are welcome. To contribute:

1. Fork the repository.  
2. Create a feature branch (`git checkout -b feature/your-feature`).  
3. Make your changes and ensure the app builds (`npm run dev`).  
4. Open a Pull Request describing the change and any required manual testing steps.  

---

Happy staking!
