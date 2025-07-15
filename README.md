# WackyFlip‑Currency

**Coins • Gems • Tickets • Purchases**
Backend microservice and client SDK for Wacky Flip’s virtual economy: balances, transactions, shops, and item unlocks.

---

## 🎯 Overview

`WackyFlip‑Currency` manages every credit earned, gem bought, ticket spent, and cosmetic unlocked across [Wacky Flip](https://wackyflip.com) games. It provides secure APIs for **wallets, purchases, rewards, promo codes,** and **server‑side validation** so that flips stay fair and fraud‑free.

---

## ✨ Core Features

| Module                    | Highlights                                                                                  |
| ------------------------- | ------------------------------------------------------------------------------------------- |
| 💰 **Wallets**            | Per‑user balances for coins, gems, event tickets, & premium tokens                          |
| 🏪 **Storefront**         | SKU/price catalog, regional pricing, discounts, & flash sales                               |
| 🎁 **Rewards Engine**     | Daily log‑ins, mission payouts, tournament prizes, promo codes                              |
| 🔐 **Transaction Ledger** | Atomic debit/credit ops with rollback & audit trail                                         |
| 📦 **Inventory Service**  | Own / equip / consume virtual items (ties to `WackyFlip‑Avatars`, `UIKit` themes, boosters) |
| 🧮 **Exchange Rates**     | Server‑driven coin↔gem conversions & real‑money purchase hooks                              |
| 🛡️ **Anti‑Fraud**        | JWT auth, server reconciliation, rate limits, signature checks                              |

---

## 🛠 Tech Stack

| Layer    | Tech                                           |
| -------- | ---------------------------------------------- |
| API      | Node.js + Fastify (TypeScript)                 |
| DB       | PostgreSQL (ledger) + Redis (hot balances)     |
| Auth     | JWT (via `WackyFlip‑Auth`)                     |
| Payments | Stripe & Google/Apple in‑app purchase webhooks |
| Queue    | BullMQ (transaction mailers, reward grants)    |

---

## 📂 Repository Structure

```
WackyFlip-Currency/
├─ src/
│  ├─ controllers/     # REST/GraphQL endpoints
│  ├─ models/          # TypeORM entities (UserBalance, LedgerEntry, Item)
│  ├─ services/        # Business logic (shop, rewards, iap validate)
│  ├─ queues/          # Job processors (grantRewards, promoBatch)
│  └─ utils/           # Helpers (signatures, price calc)
├─ prisma/             # DB schema & migrations
├─ sdk/                # Lightweight client SDK (JS/RN/Unity)
├─ scripts/            # CLI tools (bulk grant, promo import)
├─ docs/
│  ├─ api.md
│  └─ iap-flows.md
└─ README.md
```

---

## 🚀 Quick Start (Dev)

```bash
git clone https://github.com/wackyflipgame/WackyFlip-Currency.git
cd WackyFlip-Currency
pnpm install
cp .env.example .env            # fill PG/Redis/Stripe keys
pnpm prisma migrate dev
pnpm dev
```

Local API: **`http://localhost:4010`**
GraphQL Playground: **`/graphql`**

---

## 🔌 Example Usage (Web Client)

```ts
import { CurrencyClient } from '@wackyflip/currency-sdk';

const currency = new CurrencyClient({
  token: userJWT,
  endpoint: 'https://api.wackyflip.com/currency'
});

const wallet = await currency.wallet.get();
console.log(wallet.coins, wallet.gems);

// Buy a Rainbow Skin for 500 coins
await currency.shop.purchase('skin_rainbow_noob');

// Redeem promo code
await currency.rewards.redeemCode('FLIP2025');
```

---

## 🧩 Integrations

* **`WackyFlip‑Avatars`** – Unlock skins and accessories
* **`WackyFlip‑Stats`** – Reward coins for achievements
* **`WackyFlip‑Tournaments`** – Prize payouts & entry tickets
* **`WackyFlip‑Social`** – Gift coins or items to friends

---

## 📈 Roadmap

* [ ] Dynamic pricing by region & currency
* [ ] Blockchain/NFT optional layer (research)
* [ ] Marketplace for player‑to‑player trades
* [ ] Server‑driven bundles & limited‑time loot crates

---

## 🤝 Contributing

1. Fork & branch (`feat/voucher-system`)
2. Follow ESLint + Prettier (`pnpm lint:fix`)
3. Add tests (`pnpm test`)
4. Open PR with clear description

See [`docs/contributing.md`](docs/) for detailed guidelines.

---

## 🧾 License

MIT © 2025 Wacky Flip Studios
