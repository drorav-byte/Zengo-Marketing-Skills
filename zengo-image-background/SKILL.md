---
name: zengo-image-background
description: >
  Build Zengo SFMC emails that use a full-width lifestyle/app screenshot image as the hero. Use this skill when an uploaded image is intended as the main visual, or the brief calls for a photo-driven hero. Always use alongside etoro-email-builder and zengo-campaign skills. Design tokens come from zengo-campaign SKILL.md (landing page v4 source). Triggers: "use this image for the email", "image as background", "photo hero", "app screenshot hero", or when an image is uploaded as the email hero.
---

# Zengo Image-Background Hero Skill

Extension of `zengo-campaign` for emails where a photo or app screenshot is the primary visual.

---

## Design Source

All colors and typography from `zengo-campaign` SKILL.md (landing page v4):
- Dark bg: `#101010`
- Orange: `#fe990c`
- Body text: `#a7aab3`
- Card bg: `#202020`

---

## When to Use

- A real photo (lifestyle, people, sports) is provided as hero asset
- An app screenshot is provided (e.g. Predict.png — Zengo app showing market card)
- Any email where the image IS the primary visual

---

## S3 Convention

- Path: `https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/{ImageName}.jpg`
- Dimensions: 640×480px minimum, 640px width required
- Use `border-radius:16px` on hero image (matches landing page `.hero-card` border-radius: 24px → email: 16px)

---

## Zengo Logo Header Image (from Menu-Mobile-Copy-38.png)

From the logo asset: black background, `zengo` wordmark in white, `an eToro company` in green below.
- S3 path: `https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/zengo-etoro-logo.png`
- Display width: 150px
- Background: `#101010`

```html
<!-- ===== ZENGO LOGO HEADER ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td style="font-size:0px;padding:20px 40px;word-break:break-word;text-align:left">
    <img src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/zengo-etoro-logo.png" width="150" alt="Zengo — an eToro company" style="display:block;width:150px;height:auto;border:0" /></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## Hero Image (full-width, no padding, rounded)

```html
<!-- ===== HERO IMAGE ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td style="font-size:0px;padding:0 20px;word-break:break-word">
    <img src="{S3_IMAGE_URL}" width="600" alt="{ALT_TEXT}" style="display:block;width:100%;max-width:600px;height:auto;border:0;border-radius:16px" /></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## Eyebrow with Live Dot (from Predict.png / landing page style)

The Predict.png app screenshot uses "LIVE FROM POLYMARKET" in small caps with a red/orange dot. In email, use the orange dot + gray text eyebrow pattern (as defined in zengo-email-patterns.md).

```html
<tr>
 <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:8px;padding-left:0;word-break:break-word">
  <div style="font-family:Verdana,sans-serif;font-size:11px;font-weight:500;letter-spacing:0.08em;line-height:16px;color:#707482;text-align:left;text-transform:uppercase">
   <span style="display:inline-block;width:7px;height:7px;border-radius:50%;background:#fe990c;vertical-align:middle;margin-right:6px"></span>LIVE FROM ZENGO</div></td></tr>
```

---

## Live Market Card (from Predict.png)

The Predict.png shows the Zengo app market card UI. In email this is the Market Card pattern from `zengo-email-patterns.md`. Key values from the image:
- Card bg: `#202020`
- Yes badge: `#002929` / `#00cecb`
- No badge: `#331312` / `#ff5e5b`
- Footer: clock icon + "Ends [date]" · "$[N] Vol."

Use the Market Card pattern from `zengo-email-patterns.md`.

---

## Email Section Order (Image-Background Style)

```
AMPScript block (with @HideHeader = "true")
<!--theme: ...-->
<!--newSTR-->
PREHEADER
ZENGO LOGO HEADER       (dark #101010, 150px logo)
HERO IMAGE              (full-width, 20px side padding, border-radius 16px)
HERO TEXT               (dark #101010, orange-dot eyebrow, headline, body, CTA)
LIVE MARKET CARD(S)     (dark #101010, #202020 cards)
HOW IT WORKS            (dark #101010, orange circles) — optional
CLOSING CTA             (orange #fe990c or dark bg)
DISCLAIMER              (dark #101010)
```
