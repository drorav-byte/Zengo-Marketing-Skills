---
name: zengo-campaign
description: >
  Build production-ready Zengo marketing campaign emails using the correct SFMC content-block architecture and Zengo's landing page design language. Activate for ANY Zengo campaign email, onboarding, acquisition, or event email. Always use alongside etoro-email-builder for SFMC architecture rules. CRITICAL: Design tokens are sourced from the Zengo Predictions landing page HTML — not from eToro's DarkBlueGreen theme. Never write "prediction market/markets" — use "Zengo markets" or "trade on outcomes". Read references/zengo-email-patterns.md for all HTML components.
---

# Zengo Campaign Skill

## Source of Truth

Design system extracted directly from `Zengo___Prediction_Markets.html` (Landing Page v4).

---

## CSS Design Tokens (from `:root`)

```css
--white:     #ffffff
--cream:     #ebe8e5
--ink:       #101010   /* primary dark bg, main text */
--card:      #202020   /* card backgrounds */
--ink2:      #18191a   /* country pill bg, deep dark */
--gray:      #707482   /* eyebrow text, muted labels */
--gray-light:#a7aab3   /* body text on dark sections */
--gray-300:  #bdbcc3   /* stat percentages */
--gray-400:  #adb3b7   /* team card sub text */
--orange:    #fe990c   /* PRIMARY ACCENT — CTAs, highlights, eyebrow dots */
--teal:      #00cecb   /* Yes button text */
--teal-bg:   #002929   /* Yes button background */
--red:       #ff5e5b   /* No button text */
--red-bg:    #331312   /* No button background */
--blue:      #6cb1ff   /* edge card variant */
--border:    #c8c9cd   /* FAQ toggle */
--stroke:    #2f3436   /* card hover border, icon bg */
```

**Key colour decisions:**
- Page background on dark sections: `--ink` = `#101010`
- Page background on light sections: `--white` = `#ffffff`
- Primary accent: `--orange` = `#fe990c` (NOT `#F5A200` — that was a prior wrong assumption)
- CTA button text on orange: `--ink` = `#101010`
- Yes badge: bg `#002929`, text `#00cecb`
- No badge: bg `#331312`, text `#ff5e5b`
- Section divider between light/dark: just switching background — no horizontal rule

---

## Typography (from CSS)

**Font:** `Satoshi` (web font) → email fallback: `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`
> For SFMC email: use `Verdana, sans-serif` (email-safe). All size/weight values below come directly from the landing page.

| Element | Size | Weight | Letter-spacing | Color |
|---------|------|--------|---------------|-------|
| Hero h1 | 88px (→ email: 32px) | 900 | -0.03em | `#ffffff` |
| Section h2 | 83px (→ email: 28px) | 900 | -0.03em | context |
| FIFA/countdown h2 | 83px (→ email: 28px) | 900 | -0.03em | `#101010` |
| Edge card h3 | 34px (→ email: 22px) | 700 | -0.03em | context |
| How-it-works h3 | — | 700 | — | `#ffffff` |
| Eyebrow | 18px (→ email: 11px) | 500 | -0.03em | `#707482` |
| Lede/body large | 24px (→ email: 16px) | 500 | -0.03em | `#707482` |
| Body text (dark bg) | 18px (→ email: 14px) | 500 | -0.03em | `#a7aab3` |
| Stat number | 64px (→ email: 32px) | 900 | -0.03em | `#101010` |
| Stat label | 20px (→ email: 13px) | 500 | -0.03em | `#707482` |
| CTA button | 18px (→ email: 16px) | 700 | -0.03em | `#101010` |
| Team card % | 57px (→ email: 36px) | 900 | — | `#bdbcc3` |
| FAQ question | 20px (→ email: 16px) | 700 | -0.03em | `#ffffff` |
| FAQ answer | 18px (→ email: 14px) | 500 | -0.03em | `#a7aab3` |
| Footer col header | 15.6px | 700 | -0.01em | `#fe990c` |
| Disclaimer/legal | 14px | 400 | — | `#ffffff` |

---

## Section Inventory (in page order)

1. **Hero** — full-bleed video/image, rounded card (`border-radius:24px`), dark gradient overlay, text bottom-left, orange CTA, Trustpilot stars
2. **Stats** — white bg, 3 stats: `$4.2B+` / `24K+` / `8M+`, large black numbers, gray labels
3. **Momentum / Live Markets** — white bg, eyebrow "Live from Polymarket" (teal dot), filterable market cards grid, orange CTA
4. **Your Edge** — dark bg (`--ink`), 4 feature cards in 2×2 grid: blue / dark-navy / orange / cream variants
5. **FIFA World Cup Campaign** — white bg, orange eyebrow dot, FIFA crest image, large h2 with orange accent, countdown (cream cells), team cards (dark bg), orange CTA
6. **How It Works** — dark bg, 2-col layout: left = headline + body, right = 4 numbered steps
7. **Available Globally** — orange bg (`--orange`), marquee of country pills (dark `--ink2` bg, `--stroke` border)
8. **FAQ** — dark bg, accordion list, dark card items
9. **Final CTA** — orange bg, QR code + download button, large headline
10. **Footer** — dark bg, brand column + 5 link columns, social icons, legal

---

## Component Patterns

### Eyebrow
- Dot + label. Two variants:
  - **Teal dot:** `--teal` (`#00cecb`) + `--gray` text → "Live from Polymarket"
  - **Orange dot:** `--orange` (`#fe990c`) + `--gray` text → "World Cup 2026 · Featured campaign"

### CTA Buttons
- **Primary (orange pill):** bg `#fe990c`, color `#101010`, font-weight 700, border-radius 90px, padding 16px 28px, font-size 18px
- **Outline (light):** border 1px solid `#ffffff`, color `#ffffff`, hover fills white with dark text
- **Dark pill:** bg `#101010`, color `#ebe8e5`, border-radius 10px

### Market Card (`.market-card`)
- bg: `#101010` (--ink)
- border-radius: 16px
- padding: 24px 12px
- border: 1px solid transparent → hover: `#2f3436`
- Icon: 46×46px, border-radius 6px, bg `#2f3436`
- Title: 17px, 700 weight, `#ffffff`
- Outcome row: name (13px, 500, white) + pct (16px, 700, `#bdbcc3`) + Yes/No badges
- Yes badge: bg `#002929`, color `#00cecb`, border-radius 4px, padding 3px 12px
- No badge: bg `#331312`, color `#ff5e5b`, border-radius 4px, padding 3px 12px
- Footer: 12px, `#707482`, icon + "Ends [date]" + "$[N]M Vol."

### Team Card (`.team-card`) — FIFA section
- bg: `#101010`, border-radius 16px, padding 24px 12px
- Flag: 62×62px, border-radius 6px
- Team name: 29px, 700, `#ffffff`
- Sub text: 16px, 500, `#adb3b7`
- Progress bar: 5px, teal fill (Yes %) + red fill (No %)
- Prices: teal for Yes, red for No
- Large % number: 57px, 900, `#bdbcc3`

### Countdown (`.cd-cell`) — FIFA section
- bg: `#ebe8e5` (cream)
- border-radius: 16px
- Number: 111px, 900, `#101010`
- Label: 24px, 500, `#707482`
- Separator `:` — same size, `#101010`

### Edge/Feature Card (`.edge-card`)
- border-radius: 20px, padding: 30px, min-height: 327px
- Variants: `.orange` (bg `#fe990c`), `.blue` (bg `#6cb1ff`), `.cream` (bg `#ebe8e5`), `.darkc` (bg `#202020` or custom dark)
- Icon: 52×52px SVG
- H3: 34px, 700, -0.03em
- P: 16px, 500, 1.5 line-height

### How It Works Steps
- Step number: standalone `--ink` colored circle or just text in dark bg
- H3: bold, white
- P: 18px, 500, `#a7aab3`
- Steps are 1–4: Find a market / Take a position / Trade or hold / Claim your wins

### Country Pill (`.country-pill`) — Globally section
- bg: `#18191a` (--ink2)
- border: 1.5px solid `#2f3436` (--stroke)
- border-radius: 143px, padding: 13px 22px, height: 55px
- Flag: 30×22px, border-radius 3px
- Country name: 18px, 500, `#ffffff`

### Stats (`.stat`)
- Number: 64px, 900, `#101010`
- Label: 20px, 500, `#707482`
- Landing page stats: `$4.2B+` Predicted volume / `24K+` Active markets / `8M+` Predictors

---

## SFMC Color Overrides for Email (translating landing page → email)

The landing page is light (`--white`) background in most sections, dark (`--ink`) in others. For email, we default to **dark sections** (`--ink` = `#101010`) throughout (matching the Figma dark theme).

| Landing page token | Email value | Notes |
|---|---|---|
| Section bg (dark) | `#101010` | Replaces all `bgcolor` |
| Section bg (light) | `#ffffff` | Stats bar, light sections |
| Orange accent | `#fe990c` | CTAs, eyebrow dot, step circles |
| CTA text | `#101010` | Black on orange |
| Card bg | `#202020` | Market card, feature card |
| Card border hover | `#2f3436` | Subtle border |
| Body text (dark bg) | `#a7aab3` | |
| Muted/label text | `#707482` | |
| White headings | `#ffffff` | |
| Yes badge bg | `#002929` | |
| Yes badge text | `#00cecb` | |
| No badge bg | `#331312` | |
| No badge text | `#ff5e5b` | |
| Cream (countdown bg) | `#ebe8e5` | |
| Orange section bg | `#fe990c` | Final CTA, globally section |

---

## SFMC Variable Block — Zengo

```
%%[ set @fallback = "en-gb"
    set @CampaignGroup = "eToroZengo"
    set @CampaignSubGroup = "Marketing"
    set @HideHeader = "true"
    set @subject = "{subject line}"
    set @preheader = "{preheader text}"
    set @TrackingLink = "?utm_medium=email&utm_source=%%jobid%%&utm_campaign=eToroZengo_Marketing_%%jobid%%_{CampaignName}"
]%%
<!--theme: %%[ set @theme = "DarkBlueGreen" ]%% -->
<!--newSTR-->
```

- `@HideHeader = "true"` — suppress eToro logo; inject Zengo logo header as first content block
- `@CampaignSubGroup = "Operational"` for transactional/onboarding

---

## Campaign Types

| Type | Audience | Angle | CTA |
|------|----------|-------|-----|
| Acquisition | eToro crypto users | "Trade on outcomes, with confidence." | Get Zengo |
| Onboarding | New Zengo users | 4-step orientation | Open Zengo |
| Event/market | Active Zengo users | "Back your team. Make your call." | Trade now |
| Pro Upsell | Essentials users | Bitcoin Vaults + discounted fees | Upgrade to Pro |
| Reactivation | Inactive 30/60/90d | "The market won't wait." | Return to Zengo |

---

## Naming Rules

**NEVER write:** "prediction market" / "prediction markets"  
**Use instead:** "Zengo markets" / "trade on outcomes" / "make your call" / "back your view"

---

## Disclaimers (always include)

1. *Cryptoasset investing is highly volatile and unregulated in some jurisdictions. No consumer protection. Tax on profits may apply.*
2. *Zengo is a non-custodial wallet. Assets held in Zengo are not covered by eToro's regulatory protections. You are responsible for securing access to your wallet.*
3. *eToro (UK) Ltd. is authorised and regulated by the Financial Conduct Authority (FCA). eToro (Europe) Ltd. is authorised and regulated by the Cyprus Securities Exchange Commission (CySEC). eToro AUS Capital Limited is regulated by the Australian Securities and Investments Commission (ASIC).*

---

## Reference Files

| File | Purpose |
|------|---------|
| `references/zengo-email-patterns.md` | All SFMC HTML component patterns with correct colors |
| `references/zengo-copy-bank.md` | Subject lines, headlines, CTAs, body copy |
