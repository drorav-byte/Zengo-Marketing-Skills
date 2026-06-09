---
name: zengo-image-background
description: >
  Build Zengo emails where a full-bleed App Store / Play Store image IS the hero background.
  Braze emails use CSS background-image + VML Outlook fallback. SFMC emails use a <div> overlay.
  Activate when brief says "image as background", "hero image", "app store hero", or a Figma
  App Store screenshot is the primary visual. Platform split: Zengo = Braze ONLY. Never use
  SFMC for Zengo campaigns.
---

# Zengo Image-Background Hero Skill

Builds Zengo emails where a photo or App Store screenshot IS the full-bleed hero background.

> **Platform split: Zengo = Braze ONLY. Regular eToro = SFMC ONLY. Never mix.**

---

## Braze: Full-Bleed Background Image Pattern

Complete reference email: `zengo-campaign/emails/zengo-welcome-appstore-braze-v1.html`

### Layer 1 — CSS (Gmail, Apple Mail, iOS, Android)
```html
<div style="
  background-image:
    linear-gradient(to bottom, rgba(10,10,10,0.30) 0%, rgba(10,10,10,0.55) 50%, rgba(10,10,10,0.92) 100%),
    url('https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/YOUR-IMAGE.jpg');
  background-size: cover;
  background-position: center top;
  background-color: #101010;
  min-height: 580px;
">...</div>
```

### Layer 2 — VML (Outlook — required)
```html
<!--[if gte mso 9]>
<v:rect xmlns:v="urn:schemas-microsoft-com:vml" fill="true" stroke="false"
        style="width:600px;height:580px;display:block;">
  <v:fill type="frame"
          src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/YOUR-IMAGE.jpg"
          color="#101010"/>
  <v:textbox inset="0,0,0,0" style="mso-fit-shape-to-text:true;">
<![endif]-->
<!-- content visible in BOTH CSS and VML clients -->
<!--[if gte mso 9]></v:textbox></v:rect><![endif]-->
```

**Always stack gradient ON TOP of image** (gradient listed first in `background-image`).

### Gradient formula
| Image type | Gradient |
|---|---|
| Dark image, text at bottom | `rgba(10,10,10,0.30) → rgba(10,10,10,0.92)` |
| Light image | Add +0.15 to all opacity values |
| Text in center | Flat `rgba(10,10,10,0.55)` across all stops |

### Hero copy template
```
EYEBROW (orange #fe990c, 11px, caps, 0.14em spacing)  →  Welcome to Zengo
HEADLINE (white, 44px, 900 weight, line-break at 3-4 words)  →  Predict on what / you believe.
SUB-COPY (rgba(255,255,255,0.88), 17px)  →  {{first_name}}, the markets are waiting for you.
CTA (orange pill, border-radius:100px, padding:16px 44px)  →  Start Predicting
```

---

## App Store Images in Figma → Braze Email Hero

**Figma file:** `KiJ4p9z24Wu1enW0yUfQA9` · **Node:** `78:119239`

| Image | Theme | Email use |
|---|---|---|
| "One crypto wallet. Every market." | Hand + phone, dark | Product intro |
| **"Predict on what you believe."** | Dark moody portrait | **Welcome (zengo-welcome-appstore-braze-v1.html)** |
| "Buy and sell in seconds." | Outdoor + $$$ amounts | Activation |
| "Swap anything, instantly." | Dark outdoor | Feature email |
| "Never lose your crypto ever again." | Security theme | Trust/retention |
| "Real humans. Any hour." | Indoor portrait | Support email |

Export: Select frame → JPG 2× → upload to S3 at `etoro-production/e-marketing/MarketingAutomation/Zengo/`

---

## Image technical requirements

| Spec | Value |
|---|---|
| Format | JPG (photos) / PNG (UI/graphics) |
| Width | 1200px (renders 600px at 2× retina) |
| Height | 1160px+ (580px hero at 2×) |
| Subject safe zone | Center 60% of frame |
| Max file size | 200KB |

---

## When to activate
- Brief says "image as background", "hero background", "app store style"
- A Figma App Store / Play Store screenshot is the primary visual
- Campaign is photo-forward or editorial in feel

---

## Designated Hero Images

### Primary Header — `hero.png`
The **designated main email header/theme** for Zengo campaigns.

- **Visual:** Young male model, curly hair, sunglasses, looking at phone. Urban street scene. Warm golden hour light. Close-up portrait angle.
- **S3 path:** `https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/hero.png`
- **Dimensions:** Minimum 640×480px. Use full-width at 640px, `border-radius:16px`
- **Overlay:** Apply dark semi-transparent overlay (`rgba(16,16,16,0.45)`) to ensure text legibility

### Alternative Header — `img-88e6.png`
Use when female subject is preferred or for audience variation.
- **Visual:** Young woman in smart-casual outfit walking down steps of a modern glass building, holding coffee, checking phone. Warm golden hour.
- **S3 path:** `{S3_BASE}/img-88e6.png`

### Secondary / Editorial — `img-b8fb.png`
4-panel NYC lifestyle grid of the same male model. Use for multi-panel or editorial layouts.
- **S3 path:** `{S3_BASE}/img-b8fb.png`

→ See `references/zengo-image-library.md` for the full asset catalog with all paths and usage guidance.

---

## Photography Style

All Zengo lifestyle photography follows this consistent visual identity:

| Attribute | Spec |
|---|---|
| **Lighting** | Warm golden hour — amber/gold tones, high contrast |
| **Settings** | Urban: city streets, rooftops, waterfronts, modern buildings |
| **Subjects** | 25–35, aspirational, always using a smartphone |
| **Composition** | Candid/semi-candid. Never direct-to-camera posed |
| **Mood** | Confident, focused, premium but human |
| **Avoid** | Studio flash, stock-photo smiles, crypto clichés (candles, rockets) |

---

## Email Structure with Photo Hero

```
[AMPScript block]
[Preheader]
[Dark header: Zengo logo — 150px wide, white, on #101010 bg]
[Hero image — full width, 640px, border-radius:16px, 20px side padding]
[Hero text section — dark #101010 bg: eyebrow + headline + lede + CTA]
[Live market cards — WHITE bg]
[Optional: How It Works — dark card]
[CTA section — orange #FE990C bg + scattered coins]
[Disclaimer — dark card]
[Footer — dark]
```

---

## Hero Image Block — HTML Pattern

```html
<!-- Hero image -->
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0">
  <tr>
    <td style="padding:0 20px 20px;">
      <img src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/hero.png"
           alt=""
           width="600"
           style="display:block;width:100%;max-width:600px;height:auto;
                  border-radius:16px;object-fit:cover;">
    </td>
  </tr>
</table>
```

For hero image with text overlay (dark gradient):
```html
<!-- Hero with overlay — use VML background for Outlook -->
<!--[if mso]>
<v:rect xmlns:v="urn:schemas-microsoft-com:vml" fill="true" stroke="false"
        style="width:600px;height:480px;">
  <v:fill type="frame" src="{HERO_IMAGE_URL}" color="#101010"/>
  <v:textbox inset="40px,40px,40px,40px">
<![endif]-->
<div style="background-image:url('{HERO_IMAGE_URL}');background-size:cover;
            background-position:center;border-radius:16px;min-height:400px;
            padding:48px 40px;position:relative;">
  <div style="background:linear-gradient(to bottom,rgba(16,16,16,0.5),rgba(16,16,16,0.7));
              position:absolute;inset:0;border-radius:16px;"></div>
  <!-- Content on top -->
  <div style="position:relative;z-index:1;">
    <!-- eyebrow, headline, CTA here -->
  </div>
</div>
<!--[if mso]></v:textbox></v:rect><![endif]-->
```

---

## Zengo Logo Header

Always inject Zengo logo as the **first** content block. Never show eToro logo.

```html
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0"
       style="background-color:#101010;">
  <tr>
    <td style="padding:24px 32px 20px;">
      <img src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/zengo-wordmark-white.png"
           alt="Zengo"
           width="150"
           height="37"
           style="display:block;width:150px;height:auto;">
    </td>
  </tr>
</table>
```

**Logo variants available:**
| File | Color | Use on |
|---|---|---|
| `zengo-wordmark-white.png` | White | Dark backgrounds (`#101010`, `#202020`) |
| `zengo-wordmark-black.png` | Black | White/light backgrounds |
| `zengo-wordmark-orange.svg` / `.png` | Orange `#FE990C` | Promotional or lockup use |
| `zengo-lockup-orange.svg` | Orange + "an eToro company" | Footer attribution only |

*Export SVGs to PNG at 2× resolution (300×74px) for email client compatibility.*

---

## App Screenshot Hero

When the hero is a device mockup / app screenshot (e.g. `card-find.jpg`):

- Use `card-find.jpg` for "Find a market" step — shows real Predictions UI on marble surface
- Use `card-trade.png` for trading chart view — shows 2026 FIFA WC Winner chart
- Dimensions: full-width (640px), `border-radius:16px`
- No text overlay needed — these images are compositionally complete
- Pair with a text section **below** the image (not on top)

---

## SFMC Setup (same as zengo-campaign)

```
%%[
  SET @HideHeader = "true"
  SET @campaignGroup = "eToroZengo"
  SET @campaignSubGroup = "[SubGroup]"
  SET @emailName = "Zengo_[CampaignName]_[Language]"
]%%
```

---

## Asset Reference

All image assets and S3 paths → `references/zengo-image-library.md`
Design tokens, section components, naming rules → `zengo-campaign/SKILL.md`
