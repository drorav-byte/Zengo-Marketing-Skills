# Zengo Marketing Skills

Claude Code skills for building Zengo campaign emails and multi-channel assets in SFMC and Braze.

---

## Skills

### [`zengo-campaign`](./zengo-campaign/SKILL.md)

Core skill for all Zengo SFMC email builds. Contains:
- Full design token set extracted from the Zengo Predictions landing page v4 (`#101010` ink, `#fe990c` orange, `#00cecb` teal, `#ff5e5b` red)
- Typography scale with email-safe fallbacks (`Verdana, sans-serif`)
- SFMC AMPScript variable block (`@HideHeader = "true"`, `@CampaignGroup = "eToroZengo"`)
- Section inventory, component patterns (market cards, team cards, CTAs, eyebrows, how-it-works steps)
- Campaign type matrix: Acquisition / Onboarding / Event / Pro Upsell / Reactivation
- Naming rules: never write "prediction market/markets" — use "Zengo markets" or "trade on outcomes"
- Required disclaimers

**Reference files:**
| File | Purpose |
|------|---------|
| [`references/zengo-email-patterns.md`](./zengo-campaign/references/zengo-email-patterns.md) | Production-ready SFMC HTML components with correct Zengo colors |
| [`references/zengo-copy-bank.md`](./zengo-campaign/references/zengo-copy-bank.md) | Subject lines, preheaders, headlines, CTAs, FAQ copy |

---

### [`zengo-launch-kit`](./zengo-launch-kit/SKILL.md)

Campaign copy and channel briefs for the Zengo Predictions launch (source: Launch Kit V6). Contains:
- Three creative angles: General Launch / FIFA World Cup / Knowledge
- Ready-to-use social copy for X/Twitter, Facebook, Instagram, LinkedIn (with engagement benchmarks)
- In-app (Braze) specs: modal, popup/bottom sheet, push notification, content card
- App UI data: live market rows, balance display, button colors, MiniCard component spec
- Creative component names for design team handoff

Use alongside `zengo-campaign` for any Zengo launch asset across any channel.

---

### [`zengo-image-background`](./zengo-image-background/SKILL.md)

Extension of `zengo-campaign` for emails where a photo or app screenshot is the primary hero visual. Contains:
- S3 path convention for hero images (`etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/`)
- Zengo logo header HTML (150px, dark `#101010` background)
- Full-width hero image block (640×480px min, `border-radius: 16px`)
- Orange-dot eyebrow pattern for image-driven layouts
- Live Market Card pattern adapted from the Predict.png app screenshot
- Email section order specific to image-background style

Triggers: uploaded image as hero, "photo hero", "app screenshot hero", "use this image for the email".

---

## Design Tokens (quick reference)

| Token | Value | Use |
|-------|-------|-----|
| Ink (dark bg) | `#101010` | Primary background, main text |
| Orange | `#fe990c` | CTAs, eyebrow dots, step circles, accent |
| Card bg | `#202020` | Market cards, feature cards |
| Body text (dark) | `#a7aab3` | Paragraph text on dark sections |
| Muted/label | `#707482` | Eyebrow text, stat labels |
| Teal | `#00cecb` | Yes badge text |
| Teal bg | `#002929` | Yes badge background |
| Red | `#ff5e5b` | No badge text |
| Red bg | `#331312` | No badge background |
| Cream | `#ebe8e5` | Countdown cells, cream card variant |
| CTA text | `#101010` | Black text on orange button |

---

## Usage

Always combine skills:
- **Any Zengo email** → `zengo-campaign` + `etoro-email-builder`
- **Photo/screenshot hero** → `zengo-image-background` + `zengo-campaign` + `etoro-email-builder`
- **Launch or multi-channel brief** → `zengo-launch-kit` + `zengo-campaign`
