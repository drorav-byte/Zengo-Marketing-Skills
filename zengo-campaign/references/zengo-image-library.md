# Zengo Image & Asset Library

All production assets for Zengo email campaigns. Upload files to S3 before use.

**S3 base path:**
`https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/`

---

## Logo & Brand Assets

### zengo-wordmark.svg
- **Type:** SVG vector
- **Description:** Zengo wordmark (Z icon + "zengo" text). Uses `fill="currentColor"` — color is inherited from CSS `color` property.
- **Dimensions:** viewBox `0 0 210 51` — render at 150px wide in email
- **Usage:**
  - On dark backgrounds: set `color:#ffffff` (white)
  - On light backgrounds: set `color:#101010` (black)
  - Use as the email header logo block on `#101010` background
- **Email HTML:**
  ```html
  <img src="{S3_BASE}/zengo-wordmark-white.png" alt="Zengo" width="150" height="37" style="display:block;">
  ```
  *(Export SVG to PNG at 2× for email; provide white and black variants)*

### zengo-wordmark-orange.svg
- **Type:** SVG vector
- **Description:** Zengo wordmark hardcoded to orange `#FE990C`. Same geometry as above.
- **Usage:** Promotional headers, social assets, or any dark surface where the orange variant is needed. **Not for standard email headers** (use white wordmark there).

### zengo-lockup-orange.svg
- **Type:** SVG vector
- **Description:** Full brand lockup combining:
  - Zengo wordmark in orange `#FE990C` (Zengo Z icon + "zengo" text)
  - "an eToro company" sub-label in `#101010`, font Inter, weight 400
  - eToro logo mark in green `#6DFF8A`
- **Usage:** Footer of emails or any placement requiring the eToro parent-company attribution. Placed on white or light backgrounds so the orange and green are visible.
- **Do NOT use** as the primary email header — use `zengo-wordmark.svg` (white) there instead.

---

## Hero / Lifestyle Photography

All lifestyle photography follows the same visual style:
- **Aesthetic:** Warm golden hour light (late afternoon/sunset)
- **Settings:** Urban — city streets, waterfronts, rooftops, modern buildings
- **Subjects:** Young, aspirational adults (25–35) using smartphones
- **Mood:** Confident, focused, mobile-first — not posed or stock-photo style
- **Tone:** Premium but accessible. Not finance-corporate.

### hero.png ← PRIMARY EMAIL HEADER
- **Description:** Young male model, curly hair, sunglasses, looking at phone. Close-up urban portrait. Warm golden light, brick/glass building in background.
- **Usage:** **Primary email hero image / header photo.** Use as the full-width photo hero in the `zengo-image-background` pattern. This is the designated main header theme.
- **Email placement:** Full-width hero block, 640px wide, min 480px tall, `border-radius:16px`
- **S3 path:** `{S3_BASE}/hero.png`
- **Copy overlay suggestion:** Dark overlay + headline on top left; CTA button bottom left

### img-88e6.png ← ALTERNATIVE HERO (Female)
- **Description:** Young woman in smart-casual outfit (black jacket, wide-leg trousers) walking down steps of a modern glass building, holding coffee, checking phone. Warm golden hour.
- **Usage:** Alternative hero for audience segments where a female subject is preferred. Same layout rules as `hero.png`.
- **S3 path:** `{S3_BASE}/img-88e6.png`

### img-b8fb.png ← LIFESTYLE GRID / SECONDARY HERO
- **Description:** 4-panel grid featuring the same male model as `hero.png` in four NYC settings:
  1. Top-left: walking down a brownstone street
  2. Top-right: sitting at a waterfront (Hudson River / harbour)
  3. Bottom-left: on a park bench with city skyline behind
  4. Bottom-right: rooftop terrace with Empire State Building
- **Usage:** Social media creative, landing page lifestyle sections, or multi-panel email sections. Also suitable as a secondary email hero if a more editorial feel is needed.
- **S3 path:** `{S3_BASE}/img-b8fb.png`

---

## App Screenshot Photography

Real-device photography showing the Zengo app UI. Use to illustrate the "Find a market" / "How it works" steps.

### card-find.jpg ← "FIND A MARKET" STEP IMAGE
- **Description:** Hand holding iPhone on a marble countertop / table. Phone screen clearly shows the Zengo Predictions app:
  - Prediction Balance: **$920.10**
  - "Add Funds" (orange button) / "Withdraw" button
  - Market tabs: Trending · FIFA · Politics · Sports · Crypto
  - **2026 FIFA World Cup Winner** card: France 18%, Spain 17%
  - **BTC > $150k by Dec 31** card: 62% Yes
  - "Zengo Wallet Balance $1,000.00"
- **Setting:** Marble surface, warm ambient light, teal glass of water in background
- **Usage:** Step 1 ("Find a market") image card in How It Works sections. Also used in product feature sections showing the real app UI.
- **S3 path:** `{S3_BASE}/card-find.jpg`

### card-trade.png ← "TRADE" STEP IMAGE
- **Description:** Two hands holding an iPhone showing the **2026 FIFA World Cup Winner** trading chart view. A Spain flag team card is visible at the bottom of the screen.
- **Usage:** Step 3 ("Trade or hold") image card. Also suitable for chart/trading feature sections.
- **S3 path:** `{S3_BASE}/card-trade.png`

### card-buy.png ← "BUY" STEP IMAGE
- **Description:** 4 friends (mixed group, diverse) dining together at a modern restaurant. Warm, social, lifestyle-forward. Not phone-centric — evokes the idea of real-world knowledge / social signals.
- **Usage:** Step 2 ("Buy Yes or No") image card. Conveys the idea of "put your social knowledge to work."
- **S3 path:** `{S3_BASE}/card-buy.png`

---

## Illustrations & 3D Assets

### coin.png ← ZENGO COIN (Single)
- **Description:** Single 3D rendered Zengo coin. Gold/bronze metallic finish. Zengo Z logo embossed on face. Transparent background.
- **Usage:**
  - Inline with body copy as a brand accent
  - Alongside stats (e.g. "$4.2B+ volume")
  - Small decorative element in feature cards
- **Dimensions:** Square, ~400×400px source. Render at 40–80px in email.
- **S3 path:** `{S3_BASE}/coin.png`

### cta-coins.png ← ZENGO COINS (Scattered / CTA)
- **Description:** Multiple Zengo coins in various angles/orientations, scattered across a white background. 3D rendered, same gold/bronze finish. Transparent/white background.
- **Usage:** CTA section decoration. Place behind or beside the main CTA headline for energy and visual interest. Works best on orange (`#FE990C`) or white backgrounds.
- **Dimensions:** ~600×600px source. Use at full width of CTA section or as a right-aligned decorative element.
- **S3 path:** `{S3_BASE}/cta-coins.png`

### wallet.png ← SELF-CUSTODY WALLET VISUAL
- **Description:** 3D rendered black leather wallet (open, bi-fold style) with Zengo coins going into it. Evokes self-custody and ownership.
- **Usage:** "Your wallet. Your control." feature sections. Self-custody messaging. MPC / security feature cards.
- **S3 path:** `{S3_BASE}/wallet.png`

---

## FIFA / Sports Assets

### fifa-crest.png (also: img-1c51.png — identical duplicate)
- **Description:** Official **FIFA World Cup 2026** crest. Large bold "26" in black with the gold World Cup trophy integrated into the design. "FIFA" wordmark below in black. Black on transparent/white background.
- **Usage:** FIFA email section header. Place centered at top of the FIFA/event section on white background, ~80–100px tall.
- **Note:** This is the official FIFA licensed mark. Use only in FIFA World Cup campaign contexts.
- **S3 path:** `{S3_BASE}/fifa-crest.png`

### argentina.png ← TEAM FLAG
- **Description:** Argentina national flag. Light blue and white horizontal stripes with gold Sun of May emblem in center.
- **Usage:** Team card illustration for Argentina markets. Use as flag image within FIFA team cards (40×28px or similar).
- **S3 path:** `{S3_BASE}/argentina.png`
- **Note:** Other team flags should follow the same naming convention: `{country-name}.png`

---

## Utility Assets

### qr.png ← DOWNLOAD QR CODE
- **Description:** Standard black and white QR code. Links to the Zengo app download URL (`go.zengo.com/AJDQ/n5fzujtk`).
- **Usage:** Bottom of emails (especially acquisition/onboarding emails). Include alongside "Download Zengo" CTA for desktop readers who want to scan to download on mobile. Render at 100–120px.
- **S3 path:** `{S3_BASE}/qr.png`
- **Placement:** Typically bottom-right of a final CTA section, paired with "Scan to download" caption.

### iso-badge.png
- **Description:** ISO/security certification badge. White asset — requires dark background to be visible.
- **Usage:** Footer trust signals. Place on dark `#101010` or `#202020` background alongside disclaimer text.
- **S3 path:** `{S3_BASE}/iso-badge.png`

---

## Photography Style Guide (for new asset requests)

When briefing new photography or selecting stock for Zengo emails:

| Attribute | Spec |
|---|---|
| **Lighting** | Warm golden hour (not studio flash, not overcast) |
| **Settings** | Urban — city streets, rooftops, waterfronts, modern buildings |
| **Subjects** | 25–35, aspirational, diverse. Always using a smartphone |
| **Composition** | Candid or semi-candid. Not posed direct-to-camera |
| **Color grade** | Warm amber/gold tones. High contrast. Slight filmic quality |
| **Brand feel** | Premium but human. Urban confidence. Not finance-corporate |
| **Avoid** | Studio white backgrounds, stock-photo smiles, crypto clichés (charts/candles/rockets) |

---

## Asset Checklist for New Email Builds

| Asset needed | File to use |
|---|---|
| Email header (standard) | `hero.png` or `img-88e6.png` |
| Email header (alternative) | `img-b8fb.png` |
| Zengo logo on dark bg | `zengo-wordmark.svg` (white export) |
| Zengo logo on light bg | `zengo-wordmark.svg` (black export) |
| eToro attribution lockup | `zengo-lockup-orange.svg` |
| FIFA section header | `fifa-crest.png` |
| Step 1 — Find a market | `card-find.jpg` |
| Step 2 — Buy Yes/No | `card-buy.png` |
| Step 3 — Trade/hold | `card-trade.png` |
| CTA decoration | `cta-coins.png` |
| Self-custody feature | `wallet.png` |
| Coin accent | `coin.png` |
| Download QR | `qr.png` |
| Argentina team card | `argentina.png` |
