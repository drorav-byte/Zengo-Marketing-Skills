---
name: zengo-campaign
description: Production-ready Zengo prediction markets email system for SFMC. Covers design tokens, section layout, component library, SFMC setup, and naming rules. Always combine with zengo-launch-kit for campaign copy and etoro-email-builder for SFMC delivery rules.
---

# Zengo Campaign Skill

This skill enables production-ready Zengo marketing campaign emails using correct SFMC architecture and Zengo's landing page design language. It applies to acquisition, onboarding, event, and reactivation Zengo campaign emails.

## Design System Source
All design tokens derive from the Zengo landing page (v4 and above), **not** eToro's DarkBlueGreen theme.

---

## Core Color Palette

| Token | Hex | Usage |
|---|---|---|
| Ink | `#101010` | Dark section backgrounds, text on light |
| Card dark | `#202020` | Cards on dark backgrounds |
| Card border | `#2f3436` | Subtle borders on dark cards |
| White | `#ffffff` | Light section backgrounds |
| Orange | `#fe990c` | Primary CTA, eyebrow dots, active accents |
| Teal | `#00cecb` | Yes badge text, live eyebrow dot |
| Red | `#ff5e5b` | No badge text |
| Cream | `#ebe8e5` | Cream feature card background, footer bg |
| Blue | `#7bb5f5` | Blue feature card background (approx — use landing page source) |
| Navy | `#1a2332` | Dark navy feature card background (approx — use landing page source) |
| Body text (dark bg) | `#a7aab3` | Body/lede on dark backgrounds |
| Muted text (dark bg) | `#707482` | Captions, labels, metadata on dark |

### Yes / No Badge Colors (market cards)
| Badge | Background | Text |
|---|---|---|
| Yes | `#002929` | `#00cecb` |
| No | `#331312` | `#ff5e5b` |

### MiniCard component (used in modals and in-app)
- Background: `#1b1c1d`; border: `rgba(255,255,255,.06)`; border-radius: 12px
- Yes bar bg: `#004f4d`; text: `#00CECB`
- No bar bg: `#4a1614`; text: `#FF5E5B`

---

## Typography

Primary font: **Satoshi** (landing page, web). Email-safe fallback: `Verdana, sans-serif`.

| Element | Size | Weight | Letter-spacing |
|---|---|---|---|
| H1 hero | 32px | 900 | -0.03em |
| H2 section | 28px | 900 | -0.03em |
| H3 card | 20px | 700 | -0.02em |
| Body / lede | 15px | 500 | 0 |
| Eyebrow | 11px | 700 | 0.10–0.12em |
| CTA | 16px | 700 | -0.01em |
| Caption / meta | 11px | 500–600 | 0.06em |
| Market % | 22–26px | 900 | -0.03em |

---

## Section Background Alternation — CRITICAL

The Zengo site and emails use **alternating light/dark sections**, not an all-dark layout. Follow this sequence:

| Section | Background |
|---|---|
| Logo header | Dark (`#101010`) |
| Hero (photo or color) | Dark (`#101010`) or full-bleed photo |
| Stats bar | **Dark** (`#101010`) — white numbers on dark |
| Markets / Live section | **White** (`#ffffff`) — dark cards on white bg |
| "Your Edge" / Feature cards | **Dark** (`#101010`) |
| FIFA / Event countdown | **White** (`#ffffff`) — cream countdown on white |
| Final CTA section | Orange (`#fe990c`) |
| Disclaimer | Dark (`#1a1a1a`) |
| Footer | Dark (`#101010`) |

---

## Section Components

### Hero
- Full-bleed image or dark `#101010` card with rounded corners (16–20px radius)
- Eyebrow: orange dot + uppercase label, 11px, letter-spacing 0.12em
- Headline: 32px, weight 900, white, -0.03em
- Subheadline/lede: 15px, weight 500, `#a7aab3`
- CTA: orange pill, `#fe990c` bg, `#101010` text, border-radius 90px, 15px padding vertical

### Stats Bar — DARK background
- Background: `#101010` (NOT white)
- 3 columns, white metric numbers (26px, weight 900), gray labels (`#707482`, uppercase)
- Border between columns: subtle dark divider or spacing only
- Stats: **8M+ Predictors · $4.2B+ Volume · 24K+ Active markets**

### Live Markets Section — WHITE background
- Page/section background: `#ffffff`
- Eyebrow: `● Live from Polymarket` — teal dot, `#707482` text
- Section headline: large, bold, `#101010`, e.g. "See what the world thinks will happen next"
- Filter chips (optional in email): All · FIFA · Sports · Crypto · Politics · Tech & AI · Culture
- Market cards (see Market Card component below) sit on white bg

### Market Card
Dark card (`#202020` or `#1b1c1d`) on white section background. Structure:
```
[Icon] Market Title
──────────────────────────────
Outcome A     XX%   [Yes] [No]
Outcome B     XX%   [Yes] [No]
Outcome C     XX%   [Yes] [No]
+N outcomes
──────────────────────────────
Ends [date]          $XXXm Vol.
```
- Pricing format where shown: **"Yes 31¢ · No 69¢"** (cent format, not just %)
- Yes/No buttons: pill shape, teal bg for Yes, red bg for No
- Volume and end date in small muted text

### "Your Edge" / Feature Cards — DARK background
Section background: `#101010`.
Headline: "Your predictions. Your wallet. Your control." (white, 900 weight)
Subtext + orange accent line: "Same security, more opportunity."

**4 feature card colorways (left to right):**

| # | Background | Approx Hex | Headline | Body |
|---|---|---|---|---|
| 1 | Blue | `#7bb5f5` | "Real markets, real prices." | "Deep prediction-market liquidity... not a house edge." CTA: "Try now →" |
| 2 | Dark navy | `#1a2332` | "Trusted by Millions" | "2M+ people already trust Zengo wallet." |
| 3 | Orange | `#fe990c` | "Zero-hack infrastructure." | "MPC splits your key — no seed phrase." CTA: "How MPC works →" |
| 4 | Cream | `#ebe8e5` | "Secure recovery." | "Zengo's 3-Factor recovery system." CTA: "See an example →" |

Each card: border-radius 20px, icon at top, headline 18–20px weight 700, body 13px, CTA text link with arrow.
Text color on blue/cream cards: `#101010`. Text color on navy/orange cards: `#101010` or `#ffffff` depending on contrast.

### FIFA / Event Section — WHITE background
- Section background: **white** (`#ffffff`)
- FIFA World Cup trophy logo/crest at top center
- Headline (two lines):
  - Line 1: "Back your team." — black (`#101010`), 900 weight
  - Line 2: "Make your call." — orange (`#fe990c`), 900 weight
- Countdown timer: **cream/light boxes** (`#ebe8e5` or similar), dark text, format: `DD : HH : MM : SS` with "Days · Hours · Minutes · Seconds" labels
- Team cards: dark bg (`#101010` or `#1b1c1d`), 3-column grid
- Tagline: "48 nations. 104 matches. One winning bracket." — black bold
- CTA: orange pill "Trade now"

### FIFA Team Card
Each team card shows a **specific market** (not always "Win tournament"):
```
[Flag image]  Team Name
              Market description (e.g. "Win the 2026 FIFA World Cup")
──────────────────────────────
[Teal bar]────────────[Red bar]
Yes XX¢ ←                → No XX¢
              XX%
```
- Pricing: cent format e.g. "Yes 31¢" / "No 69¢"
- Progress bar: split teal (Yes side) and red (No side) proportional to probability
- Percentage large centered below bar (22–26px, white, 900 weight)

**Current World Cup 2026 market odds (from Polymarket, as at launch):**
| Team | Market | Yes% | Yes¢ | No¢ |
|---|---|---|---|---|
| Argentina | Win the 2026 FIFA World Cup | 31% | 31¢ | 69¢ |
| Brazil | Reach the top 4 | 58% | 58¢ | 42¢ |
| England | Reach the final | 42% | 42¢ | 58¢ |
| France | Win the 2026 FIFA World Cup | 25% | 25¢ | 75¢ |
| Spain | Win the 2026 FIFA World Cup | 22% | 22¢ | 78¢ |

*Update odds from Polymarket before sending. These are illustrative defaults.*

### How It Works (4 steps)
- Dark background (`#202020` card or `#101010` section)
- 4 numbered orange circles (36px diameter, `#fe990c` bg, `#101010` text)
- Steps: (1) Download Zengo · (2) Add USDC · (3) Back your position · (4) Settle fast

### CTA Section (closing)
- Background: orange (`#fe990c`)
- Headline: white or `#101010` depending on contrast (test — `#101010` on orange is correct per brand)
- CTA button: dark pill (`#101010` bg, white text), border-radius 90px

### Disclaimer Block
- Background: `#1a1a1a` or dark card, border-radius 12px
- Text color: `rgba(255,255,255,0.35)` — semi-transparent white
- Font size: 10px, line-height 1.6

---

## Naming Conventions

**NEVER** use "prediction market/markets" in email copy or subject lines. Instead use:
- "Zengo markets"
- "trade on outcomes"
- "make your call"
- "back your view"
- "markets"

*Note: The Zengo website does use "prediction markets" in its own hero headline — this rule applies to email copy only.*

---

## SFMC Setup

```
%%[
  SET @HideHeader = "true"
  SET @campaignGroup = "eToroZengo"
  SET @campaignSubGroup = "[SubGroup]"   /* e.g. FIFA_WorldCup2026_Winner */
  SET @emailName = "Zengo_[CampaignName]_[Language]"
]%%
```

- Inject Zengo logo as first content block (150px width, white on dark)
- Logo S3 path: `https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/zengo-logo-white.png`
- CTA tracking: wrap URLs in `%%=RedirectTo(CloudPagesURL(N))=%%`

---

## Required Disclaimers (all 3, every email)

1. Cryptoassets are highly volatile. Your capital is at risk. The value of your position may go down as well as up and you may receive back less than you invest. Past performance is not a reliable indicator of future results.
2. Zengo is a non-custodial wallet. You are solely responsible for safeguarding access to your assets. Zengo Ltd does not hold, custody, or control your funds.
3. Regulated services provided by eToro (Europe) Ltd (CySEC), eToro (UK) Ltd (FCA), and eToro AUS Capital Limited (ASIC). Zengo markets may not be available in all regions. Subject to local regulation.

---

## Reference Materials

- `references/zengo-email-patterns.md` — SFMC HTML component library
- `references/zengo-copy-bank.md` — Approved copy templates and messaging framework
- `zengo-launch-kit/SKILL.md` — Campaign copy, social, in-app, FIFA angles
- `zengo-image-background/SKILL.md` — Photo/app-screenshot hero variant
