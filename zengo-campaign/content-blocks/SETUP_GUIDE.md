# Zengo Braze Email Setup Guide
## Start-from-zero email infrastructure — do these steps in order

---

## STEP 1 — Create 5 Content Blocks in Braze

Go to: **Content → Templates → Content Block → Create Content Block**

For each block:
- Type: **HTML**
- Paste the code from the matching file below

| Block Name (exact) | File to paste |
|---|---|
| `zengo_logo_header` | `CB_zengo_logo_header.html` |
| `zengo_stats_bar` | `CB_zengo_stats_bar.html` |
| `zengo_how_it_works` | `CB_zengo_how_it_works.html` |
| `zengo_orange_cta` | `CB_zengo_orange_cta.html` |
| `zengo_dark_footer` | `CB_zengo_dark_footer.html` |

**The name MUST be exact** — it's what Liquid uses to reference:
```liquid
{{content_blocks.${zengo_logo_header}}}
```

After creating each block, **click Save** (no need to publish — Content Blocks publish automatically when referenced).

---

## STEP 2 — Create the Welcome Email Campaign

Go to: **Campaigns → Create Campaign → Email**

### Campaign settings:
- **Name:** `Zengo_Onboarding_Welcome_EN_v1`
- **From name:** `Zengo`
- **From email:** use the Zengo verified sender address (check Settings → Email Preferences)
- **Subject line:** `Welcome to Zengo — your edge starts here`
- **Preview text:** `Predict. Win. Repeat. Here's how to make your first call.`

### Email body:
1. In the email editor, select **HTML editor** (not drag-and-drop)
2. Paste the full contents of: `zengo-welcome-braze-v1.html`
3. The file is at: `C:\Users\drorav\OneDrive - globaltrad\Documents\Work\zengo-welcome-braze-v1.html`

### Before sending — verify these Liquid tags render correctly:
- `{{${first_name} | default: 'there'}}` → shows user's first name
- `{{${language}}}` → used for multi-language headline switching
- `{{${set_user_to_unsubscribed_url}}}` → unsubscribe link
- `{{${email_footer}}}` → Braze compliance footer (must be present)

---

## STEP 3 — Set Up the Welcome Canvas (Email Flow)

Go to: **Canvas → Create Canvas**

### Canvas: Zengo Onboarding v1

**Entry:** 
- Trigger: Custom event `zengo_account_verified` (or segment: Zengo Verified = true AND Email Subscribed = true AND Received Welcome Email = false)
- Entry window: All time
- Re-eligibility: OFF (welcome = once only)

**Canvas Steps:**

```
[Entry: zengo_account_verified]
          ↓
[Wait: 30 min]
          ↓
[Message: Welcome Email]
  Channel: Email
  Campaign: Zengo_Onboarding_Welcome_EN_v1
          ↓
[Wait: 2 days]
          ↓
[Filter: Did NOT open welcome email?]
     Yes ↓           No ↓
[D2 Nudge Email]   [EXIT — engaged]
  "Your call is waiting"
          ↓
[Wait: 5 days]
          ↓
[Filter: Still no first trade?]
     Yes ↓
[D7 Re-engage Email]
  "Still thinking? Here's an easy first call."
          ↓
[EXIT]
```

---

## STEP 4 — Assets to Upload to S3 (if not already there)

Check S3 bucket: `etoro-production/e-marketing/MarketingAutomation/Zengo/`

Required for welcome email:
- `hero.png` — full-bleed hero background image
- `zengo-wordmark-white.png` — Zengo white logo
- `card-find.jpg` — How It Works step 1 card
- `card-buy.png` — How It Works step 2 card
- `card-trade.png` — How It Works step 3 card
- `appstore-badge.png` — App Store download badge
- `playstore-badge.png` — Google Play badge

If any are missing: ask design to upload, or use these temp URLs (flagcdn flags are already CDN-hosted and need no upload).

---

## STEP 5 — Sender Domain Verification

Before any email sends:
1. Go to **Settings → Email Settings**
2. Confirm `zengo.com` is a verified sending domain
3. If not: add DNS records provided by Braze (DKIM + SPF)
4. Test with **Send Test** to your own address first

---

## What the Content Blocks look like:

| Block | What it renders |
|---|---|
| `zengo_logo_header` | Dark header bar with Zengo white wordmark, centered |
| `zengo_stats_bar` | Dark row: 8M+ Predictors · $4.2B+ Volume · 24K+ Active Markets |
| `zengo_how_it_works` | 3-column dark section: Find → Back → Settle with card images |
| `zengo_orange_cta` | Orange section with customizable headline + dark pill button + app store badges |
| `zengo_dark_footer` | 3 regulatory disclaimers + unsubscribe link + `{{${email_footer}}}` |

---

## Notes for future emails

Once Content Blocks are created, every new email starts with:
```html
{{content_blocks.${zengo_logo_header}}}
```
...and ends with:
```html
{{content_blocks.${zengo_dark_footer}}}
```

The `zengo_dark_footer` block already includes `{{${email_footer}}}` — **do not add it again** in the main template.

For market data: uncomment the `{% connected_content %}` block in the welcome email template once you have the Zengo API endpoint available.
