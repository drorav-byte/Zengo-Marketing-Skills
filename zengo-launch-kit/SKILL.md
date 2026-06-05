---
name: zengo-launch-kit
description: >
  Campaign copy, creative specs, and channel briefs for the Zengo Predictions launch. Sourced from Launch_Kit_V6. Contains ready-to-use social copy (X/Twitter, Facebook, Instagram, LinkedIn), in-app messaging specs (Braze modal, popup, push, content card), and email campaign brief. Activate when building or briefing any Zengo launch campaign asset across any channel. Always combine with zengo-campaign skill for design tokens and SFMC email patterns.
---

# Zengo Launch Kit V6

Source: `Launch_Kit_V6__offline_.html` — Zengo Predictions launch campaign.

---

## Campaign Narrative

Three creative angles. Pick one or A/B test:

| Creative | Angle | Key line |
|----------|-------|----------|
| **A — General Launch** | Self-custody + markets together | "Predict the world. Now on Zengo." / "Trade the world. With Confidence." |
| **B — FIFA World Cup** | Sports event momentum | "Back your team. Make your call." |
| **C — Knowledge** | Empowerment / conviction | "Put your knowledge to work." |

---

## Design Tokens (shared across all channels)

From Launch Kit source code:
```
INK    = #101010
ORANGE = #FE990C   ← primary accent (confirmed across landing page + launch kit)
TEAL   = #00CECB   ← Yes badges
RED    = #FF5E5B   ← No badges
BLUE   = #4B8EF5   ← secondary/info
GREEN  = #5FC52E   ← success
```

---

## 01 · X / Twitter — 3 Posts

### Post A — General Launch
```
🔮 Predict the world. Now on Zengo.

⚽ Sports, 💼 politics, 📈 crypto, 📰 news — real-world outcomes you can trade with real conviction. Live prices, settled in USDC, secured by the only crypto wallet never to be hacked.

Predict the world.
→ go.zengo.com/AJDQ/n5fzujtk
```
*Stats reference: 212 replies · 684 reposts · 4.1K likes · 128K views*

### Post B — FIFA World Cup
```
⚽ 48 nations. 104 matches. One winner.

🏆 FIFA World Cup 2026 markets are live in Zengo.
Back your team with conviction — not guesswork. Kicks off June 11.

Back your team. Make your call.
→ go.zengo.com/AJDQ/n5fzujtk
```
*Stats reference: 147 replies · 903 reposts · 5.6K likes · 203K views*

### Post C — Knowledge
```
🧠 Put your knowledge to work.

⚽ Sports. 📈 Crypto. 💼 Politics — real-world outcomes you can predict with conviction.

🔍 Find a market → 💡 Buy Yes or No → 📈 Trade or hold → 🏆 Claim your wins.

→ go.zengo.com/AJDQ/n5fzujtk
```
*Stats reference: 96 replies · 418 reposts · 2.9K likes · 74K views*

---

## 02 · Facebook — 2 Posts (Company Page)

### Post A — General Launch
```
🔮 Prediction markets are now live in Zengo — sports, politics, crypto and culture.

🌍 Real crowd-driven prices, not house odds. Secured by your self-custodial wallet.

🏆 Find a market → take a position → claim your wins.

Download Zengo: go.zengo.com/AJDQ/n5fzujtk

Subject to local regulation.
```
*Stats reference: 2.4K likes · 186 comments · 341 shares*

### Post B — FIFA World Cup
```
⚽ FIFA World Cup 2026 markets are live. 🏆

🌍 48 nations. 104 matches. Back your team with conviction — real prices set by the crowd, not a bookmaker. All inside your Zengo wallet.

Opens June 11. Subject to local regulation.
→ go.zengo.com/AJDQ/n5fzujtk
```
*Stats reference: 3.1K likes · 247 comments · 512 shares*

---

## 03 · Instagram — 3 Posts (Feed)

### Post A — General Launch
```
🔮 Predict the world. Now on Zengo.

⚽ Sports. 📈 Crypto. 💼 Politics. 📰 News.

Real prices. Real outcomes. Settled in USDC. Link in bio.
```
*Stats reference: 18.4K likes*

### Post B — FIFA World Cup
```
⚽ FIFA World Cup 2026 is here. 🏆

🥇 48 nations. 104 matches. One winner.

Back your team - make your call. Link in bio.
```
*Stats reference: 24.7K likes*

### Post C — Knowledge
```
🧠 Put your knowledge to work. Now on Zengo.

🔍 Find a market.
💡 Buy Yes or No.
📈 Trade or hold.
🏆 Claim your wins.

Real prices. Real outcomes. Settled in USDC. Link in bio.
```
*Stats reference: 16.2K likes*

---

## 04 · LinkedIn — 3 Posts (Company Page)

### Post A — Trade the World
```
🌍 Trade the world — with confidence.

The self-custodial wallet trusted by 2M+ people now brings you the world's deepest prediction markets.

⚽ Sports. 💼 Politics. 📈 Crypto — real crowd-driven prices, settled in USDC.

No seed phrase. No giving up your funds. Backed by a seven-year record of zero hacks.

Same security, more opportunity. Now live.
#PredictionMarkets #SelfCustody #Crypto #Fintech
```
*Stats reference: 2,184 reactions · 147 comments · 396 reposts*

### Post B — FIFA World Cup
```
⚽ The FIFA World Cup 2026 is coming - and so are the markets. 🏆

Starting June 11, Zengo users can back their team with conviction across 48 nations and 104 matches.

Live prediction markets, real crowd-driven prices, settled in USDC - all inside a wallet you fully control.

Back your team. Make your call.
#WorldCup2026 #PredictionMarkets #Zengo
```
*Stats reference: 1,562 reactions · 94 comments · 241 reposts*

### Post C — Knowledge
```
🧠 Put your knowledge to work.

Most people consume the news. Zengo users predict it.

🔍 Find a market · 💡 Buy Yes or No · 📈 Trade or hold · 🏆 Claim your wins.

Real crowd-driven prices — not house odds. Settled in USDC, inside the wallet you fully own.

Same security. More opportunity. Now live.
#PredictionMarkets #Zengo #Crypto
```
*Stats reference: 1,841 reactions · 122 comments · 307 reposts*

---

## 05 · In-App (Braze) — 4 Surfaces

### 1 · Modal (⭐ Recommended)
**Trigger:** Next app open after launch. Suppress once dismissed or CTA tapped.

**Header (dark bg `#101010`):**
- Zengo wordmark (white)
- Mini market card (MiniCard component)

**Body (white bg):**
- Label: "Now live" — orange, 12px, letter-spacing 0.02em
- Headline: "Predict the world." — `#101010`, 24px, 900 weight
- Body: "⚽ Sports. 📈 Crypto. 💼 Politics - real-world outcomes, real prices, settled in USDC."
- CTA (orange pill): "Place your first prediction"
- Secondary: "Maybe later"

### 1b · Modal V2 — Journey Version (Alt)
**A/B test against standard modal.**

**Header:** "Put your knowledge **to work.**" (orange accent)

**4-Step List:**
- 🔍 Find a market · ⚽ Sports · 📈 Crypto · 💼 Politics
- 💡 Buy Yes or No · Real crowd-driven prices
- 📈 Trade or hold · Exit anytime or hold to settlement
- 🏆 Claim your wins · Settled in USDC

**CTA (orange pill):** "Predict now" / Secondary: "Maybe later"

### 2 · Popup (Bottom Sheet)
**Trigger:** First open of the Predictions tab. Ideal for FIFA campaign.

- FIFA crest image + "FIFA WORLD CUP 2026" label (orange, uppercase)
- Headline: "Markets are live." — `#101010`, 20px, 900
- Body: "48 nations. 104 matches. Back your team with conviction — prices are set by the crowd, not the house."
- CTA (dark pill `#101010`): "Back your team. Make your call."
- Secondary: "Dismiss"

### 3 · Push Notification
**Trigger:** Fire to lapsed users on launch day to drive re-opens.

- App: ZENGO
- Title: "🔮 Predict the world."
- Body: "⚽ Sports. 📈 Crypto. 💼 Politics. Real prices, secured by your wallet."

### 4 · Content Card (Persistent Feed)
**Duration:** Show to all users for 7 days post-launch. Persists until dismissed.

- Card header (dark bg): "New" badge (orange) · Zengo wordmark · mini market card
- Headline: "Predict the world."
- Body: "Real markets, real prices - inside your self-custodial Zengo wallet."
- CTA link: "Place your first prediction →" (orange text)
- Second card (dimmed): "FIFA World Cup 2026 markets · 48 nations. 104 matches. Back your team."

---

## 06 · Email (Braze Canvas)

**Trigger:** Canvas step after wallet activation
**Platform:** Braze (welcome email, not SFMC)
**Note:** For SFMC email builds → use zengo-campaign skill + zengo-email-patterns.md

---

## App UI Data (from AppBackground component)

**Prediction Balance display:** `$920.10`

**Live market rows shown in app:**
| Market | % | Yes | No |
|--------|---|-----|----|
| 2026 FIFA World Cup Winner | 25% | 25¢ | 75¢ |
| NBA Championship 2026 | 34% | 34¢ | 66¢ |
| BTC > $150k by Dec 31 | 62% | 62¢ | 38¢ |

**App home tabs:** Trending · FIFA · Sports · Crypto

**App button colors:**
- Add Funds: bg `#FE990C`, text `#101010`
- Withdraw: bg `#26211a`, text `#d8b274`

**MiniCard component (used in modals):**
- bg: `#1b1c1d`, border-radius 12, border `rgba(255,255,255,.06)`
- Yes bar: bg `#004f4d`, text `#00CECB`
- No bar: bg `#4a1614`, text `#FF5E5B`

---

## Creative Component Names (for design team reference)

| Creative | Component name |
|----------|---------------|
| X · General Launch | `CreativeLaunchV4` |
| X · World Cup | `CreativeWorldCupV4` |
| X · Knowledge | `CreativeKnowledgeV6` |
| FB · General Launch | `CreativeFBLaunchV4` |
| FB · World Cup | `CreativeFBWorldCupV4` |
| IG · General Launch | `CreativeIGLaunchV4` |
| IG · World Cup | `CreativeIGWorldCupV4` |
| IG · Knowledge | `CreativeIGKnowledgeV6` |
| LI · Trade | `CreativeLITradeV6` |
| LI · World Cup | `CreativeWCLinkedInV4` |
| LI · Knowledge | `CreativeLIKnowledgeV6` |
| Security | `CreativeSecurityV4` |

---

## Key URLs

- Download / CTA: `https://go.zengo.com/AJDQ/n5fzujtk`
- MPC explainer: `https://zengo.com/mpc-wallet/`
- 3FA recovery: `https://help.zengo.com/en/articles/2603673-what-is-zengo-s-recovery-kit`

---

## Regulatory Note (always include on social)

"Subject to local regulation." on Facebook posts.
Availability note: "Availability is subject to local regulation; restricted regions stay hidden in-app until rules change."
