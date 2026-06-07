---
name: zengo-launch-kit
description: Campaign copy, creative specs, and channel briefs for the Zengo Predictions launch. Sourced from Launch_Kit_V6. Contains ready-to-use social copy (X/Twitter, Facebook, Instagram, LinkedIn), in-app messaging specs (Braze modal, popup, push, content card), and email campaign brief. Activate when building or briefing any Zengo launch campaign asset across any channel. Always combine with zengo-campaign skill for design tokens and SFMC email patterns.
---

# Zengo Launch Kit V6

## Campaign Narrative

Three creative angles. Pick one or A/B test:

| Creative | Angle | Key line |
|----------|-------|----------|
| **A — General Launch** | Self-custody + markets together | "Predict the world. Now on Zengo." / "Trade the world. With Confidence." |
| **B — FIFA World Cup** | Sports event momentum | "Back your team. Make your call." |
| **C — Knowledge** | Empowerment / conviction | "Put your knowledge to work." |

---

## Design Tokens (shared across all channels)

```
INK    = #101010    ← primary dark background
ORANGE = #FE990C    ← primary accent (CTAs, eyebrows, active states)
TEAL   = #00CECB    ← Yes badges, live dot
RED    = #FF5E5B    ← No badges
BLUE   = #7BB5F5    ← feature card (approx — source from landing page)
NAVY   = #1A2332    ← feature card (approx — source from landing page)
CREAM  = #EBE8E5    ← feature card, countdown timer cells
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

## FIFA World Cup 2026 — Section Design Spec

### CRITICAL: FIFA section uses WHITE background
The FIFA campaign section on the landing page and in email uses **white/light background**, not dark.
Do not apply dark `#101010` to this section.

### Layout sequence (white bg):
1. FIFA World Cup 2026 trophy logo/crest — centered, ~80px
2. Two-line headline:
   - "Back your team." — `#101010`, weight 900, large
   - "Make your call." — `#fe990c`, weight 900, large
3. Countdown timer (see below)
4. Team cards — 3-column grid (dark cards on white bg)
5. Tagline: **"48 nations. 104 matches. One winning bracket."** — `#101010`, bold
6. CTA: orange pill "Trade now"

### Countdown Timer
- Cell background: **cream / light** (`#ebe8e5` or similar) — NOT dark
- Cell text (numbers): `#101010`, large, weight 900
- Cell label (Days/Hours/Minutes/Seconds): `#707482`, small, uppercase
- Separator: `:` in `#101010`
- Border-radius: 12–16px on each cell

### Team Cards — DARK on white section
Each team card shows a **specific, distinct market** per team (not all "Win tournament"):

| Team | Market shown | Yes% | Yes¢ | No¢ |
|---|---|---|---|---|
| Argentina | Win the 2026 FIFA World Cup | 31% | 31¢ | 69¢ |
| Brazil | Reach the top 4 | 58% | 58¢ | 42¢ |
| England | Reach the final | 42% | 42¢ | 58¢ |

*Odds sourced from Polymarket. Update before each send. Use these as illustrative defaults only.*

**Team card structure:**
```
[Flag image]  Team Name
              Market description
──────────────────────────────────
[Teal ←──────────────────── Red]  (proportional split bar)
Yes XX¢                    No XX¢
              XX%           (large, centered)
```

- Progress bar: split bar — teal side = Yes probability, red side = No probability
- Pricing: **cent format** ("Yes 31¢" / "No 69¢") shown at bar ends
- Percentage: 22–26px, white, weight 900, centered below bar
- Card bg: `#101010` or `#1b1c1d`; border-radius: 16px

---

## App UI Reference Data

**Prediction Balance display:** `$920.10`

**Live market rows shown in app (defaults):**
| Market | % | Yes | No |
|--------|---|-----|----|
| 2026 FIFA World Cup Winner | 25% | 25¢ | 75¢ |
| NBA Championship 2026 | 34% | 34¢ | 66¢ |
| BTC > $150k by Dec 31 | 62% | 62¢ | 38¢ |

**App home tabs:** Trending · FIFA · Sports · Crypto

**App button colors:**
- Add Funds: bg `#FE990C`, text `#101010`
- Withdraw: bg `#26211a`, text `#d8b274`

---

## World Cup Winner Market — Full Odds (from Polymarket)

Top teams at time of launch:

| Team | Win WC % | Yes¢ | No¢ |
|---|---|---|---|
| France | 25% | 25¢ | 75¢ |
| Spain | 22% | 22¢ | 78¢ |
| England | 19% | 19¢ | 81¢ |
| Argentina | 31% | 31¢ | 69¢ |
| Brazil | — (shown as Top 4) | — | — |

*Source: Zengo landing page → Live from Polymarket section. Always refresh before send.*

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
