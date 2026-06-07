# Zengo Braze Patterns & Reference

Zengo uses **Braze** (not SFMC) as its marketing platform. This file is the Braze equivalent
of `zengo-sfmc-patterns.md` — it covers email code structure, Liquid templating, Connected
Content for live market data, Canvas architecture, and multi-language patterns.

---

## SFMC → Braze: Quick Translation

| SFMC concept | Braze equivalent |
|---|---|
| AMPScript `%%[ ]%%` | Liquid `{% %}` / `{{ }}` |
| `AttributeValue("FirstName")` | `{{${first_name}}}` |
| `%%subscription_center_url%%` | `${set_user_to_unsubscribed_url}` |
| `<!--newSTR-->` content block | Full `<html>` document (no wrapper needed) |
| `@HideHeader = "true"` | Not needed — Braze doesn't inject a header |
| `@campaignGroup` / `@campaignSubGroup` | Campaign name + Canvas name in dashboard |
| Journey Builder | Canvas |
| Triggered sends | Action-triggered Campaign or Canvas entry |
| Subscription Center | Braze Preference Center + Subscription Groups |
| Content Builder block | Content Block → `{{content_blocks.${name}}}` |
| `HTTPGet()` dynamic data | Connected Content `{% connected_content %}` |
| Publications / lists | Subscription Groups |

---

## 1. Email HTML Structure

Braze requires **complete HTML** in the HTML editor. You own the entire document.
Braze auto-injects: open-tracking pixel, click-tracking rewrites, list-unsubscribe header.

```html
<!DOCTYPE html>
<html lang="{{${language} | default: 'en'}}">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>Email title</title>
  <style>
    body { margin:0; padding:0; background:#101010; font-family:Verdana,Geneva,sans-serif; }
    table { border-collapse:collapse; }
    img { border:0; outline:none; text-decoration:none; display:block; }
  </style>
</head>
<body style="margin:0;padding:0;background:#101010;">

  <!-- EMAIL CONTENT HERE -->

  <!-- Required footer — define content in Braze dashboard → Email Preferences -->
  {{${email_footer}}}

</body>
</html>
```

**Critical rules:**
- `{{${email_footer}}}` is **mandatory** in every commercial email (CAN-SPAM/GDPR compliance)
- The footer must include unsubscribe URL + physical mailing address
- Define footer content once in Braze dashboard → Email Preferences (max 100 KB)
- Do NOT duplicate unsubscribe logic in the body if `{{${email_footer}}}` handles it

---

## 2. Liquid Personalization

Braze uses **Liquid 5** (Shopify's template language) with Braze extensions.

### Standard user attributes
```liquid
{{${first_name} | default: 'there'}}
{{${last_name}}}
{{${email_address}}}
{{${country}}}          {# ISO 3166-1 alpha-2, e.g. "GB", "DE", "FR" #}
{{${language}}}         {# ISO 639-1, e.g. "en", "fr", "de" #}
{{${user_id}}}          {# Braze internal ID #}
{{${external_id}}}      {# Your system's user ID (eToro/Zengo user ID) #}
{{${time_zone}}}        {# IANA format, e.g. "Europe/London" #}
```

### Zengo custom attributes (examples — confirm exact names in Braze dashboard)
```liquid
{{custom_attribute.${zengo_balance}}}
{{custom_attribute.${zengo_prediction_count}}}
{{custom_attribute.${zengo_verified}}}
{{custom_attribute.${zengo_tier}}}
{{custom_attribute.${last_prediction_date}}}
{{custom_attribute.${preferred_market_category}}}
```

### Personalized greeting (safe pattern with default)
```liquid
Hi {{${first_name} | default: 'there'}},
```

### Abort if critical data is missing
```liquid
{% if custom_attribute.${zengo_balance} == blank %}
  {% abort_message('No Zengo balance — skipping send') %}
{% endif %}
```

---

## 3. Multi-Language Pattern

Zengo operates in **13 languages** (IT, ES, DE, FR, AR top markets).
Use `{{${language}}}` for conditional content blocks.

```liquid
{% if ${language} == 'fr' %}
  <h1>Qui fera partie des quatre derniers ?</h1>
{% elsif ${language} == 'de' %}
  <h1>Wer macht das letzte Quartett?</h1>
{% elsif ${language} == 'es' %}
  <h1>¿Quién llega a las semifinales?</h1>
{% elsif ${language} == 'it' %}
  <h1>Chi arriverà alle semifinali?</h1>
{% elsif ${language} == 'ar' %}
  <h1 dir="rtl">من سيصل إلى الدور نصف النهائي؟</h1>
{% else %}
  <h1>Who Makes the Last Four?</h1>
{% endif %}
```

**Arabic RTL note:** Add `dir="rtl"` to the `<html>` tag or specific `<table>`/`<td>` elements when `{{${language}}} == 'ar'`.

```liquid
{% if ${language} == 'ar' %}
  <html lang="ar" dir="rtl">
{% else %}
  <html lang="{{${language} | default: 'en'}}">
{% endif %}
```

---

## 4. Connected Content — Live Market Odds

Connected Content pulls live data at send time. Use this to inject real Polymarket/Zengo
market odds into the email without hardcoding.

### Basic pattern
```liquid
{% connected_content https://api.zengo.com/markets/featured :save markets %}
{% if markets == nil %}
  {% abort_message('Market data unavailable') %}
{% endif %}
```

### Access response fields
```liquid
{{markets.items[0].market_name}}
{{markets.items[0].yes_price}}
{{markets.items[0].no_price}}
{{markets.items[0].probability}}
```

### Example: FIFA World Cup market
```liquid
{% connected_content https://api.zengo.com/markets/fifa-2026-winner :save wc :cache_max_age 300 %}

{% assign france_yes = wc.france.yes_price %}
{% assign france_no  = wc.france.no_price %}

<!-- France card -->
<td style="...">
  <p>France</p>
  <span style="color:#00cecb;">YES {{france_yes}}¢</span>
  <span style="color:#ff5e5b;">NO {{france_no}}¢</span>
</td>
```

### Polymarket fallback (if Zengo API not available)
```liquid
{% connected_content https://gamma-api.polymarket.com/markets?slug=2026-fifa-world-cup-winner :save pm :cache_max_age 300 %}
{% if pm == nil or pm.size == 0 %}
  {# Fall back to hardcoded odds from last known prices #}
  {% assign france_yes = 25 %}
  {% assign france_no  = 75 %}
{% else %}
  {% assign france_yes = pm[0].outcomePrices[0] | times: 100 | round %}
  {% assign france_no  = pm[0].outcomePrices[1] | times: 100 | round %}
{% endif %}
```

### Connected Content rules
- GET responses cached 5 min by default (add `:cache_max_age` for longer)
- POST not cached — add `:cache_max_age` explicitly
- Max response: 1 MB | Timeout: 2 seconds
- On 404: renders empty string (does NOT abort automatically — add abort logic manually)
- Store credentials (API keys, tokens) in Braze dashboard → Connected Content credentials

---

## 5. Content Blocks

Reusable components managed centrally. Use for headers, footers, disclaimer text, logo blocks.

```liquid
{{content_blocks.${zengo_logo_header}}}
{{content_blocks.${zengo_dark_footer}}}
{{content_blocks.${zengo_disclaimer_en}}}
{{content_blocks.${zengo_orange_cta_section}}}
```

**Rules:**
- Max 50 KB per block
- One level of nesting only (a content block cannot contain another content block)
- Name is fixed after saving — choose carefully
- Copy exact Liquid tag from the block's Detail page in Braze dashboard

**Recommended blocks to create for Zengo:**
| Block name | Content |
|---|---|
| `zengo_logo_header` | Dark bar with Zengo wordmark-white |
| `zengo_orange_cta` | Orange section with coins, QR, "Start Predicting →" |
| `zengo_dark_footer` | Disclaimer text + unsubscribe link + ISO badge |
| `zengo_stats_bar` | 48 Nations · $4.2B+ · 1¢ |
| `zengo_how_it_works` | 3-step cards (Find, Buy, Trade) |

---

## 6. Subscription / Unsubscribe

```liquid
{# In email body — inline unsubscribe link #}
<a href="{{${set_user_to_unsubscribed_url}}}" style="color:#fe990c;">Unsubscribe</a>

{# Link to Braze preference center (manages subscription groups) #}
<a href="{{${preference_center_url}}}" style="color:#fe990c;">Email Preferences</a>

{# Full auto-footer tag (required — renders your workspace footer template) #}
{{${email_footer}}}
```

**Do not use** SFMC-style `%%subscription_center_url%%` or `%%profile_center_url%%` — these are SFMC-only.

---

## 7. Campaign vs Canvas — When to Use

### Use a Campaign for:
- One-shot promotional emails (World Cup markets live, price alert, feature launch)
- Event-triggered single emails (user registered → send welcome)
- A/B test a single message (up to 8 variants)

### Use a Canvas for:
- Multi-step lifecycle journeys (onboarding drip, win-back sequence, LTV nurture)
- Delay → message → check action → branch logic
- Cross-channel sequences (email D1 → push D3 → in-app D7)

### Zengo lifecycle Canvas structure (example — Onboarding)
```
[Entry trigger: User registers on Zengo]
       ↓
[Message step: Welcome email — hero.png, "Predict. Win. Repeat."]
       ↓ (delay: 24 hours)
[Decision split: Has made first prediction?]
   YES ↓                          NO ↓
[Exit / move to LTV Canvas]    [Message step: "Your first market is waiting" nudge]
                                       ↓ (delay: 48 hours)
                               [Decision split: Still no prediction?]
                                   YES ↓              NO ↓
                               [Push + email]          [Exit]
```

---

## 8. Email Naming Convention (Zengo in Braze)

Since Braze manages naming in the dashboard (no AMPScript variables), use a consistent naming pattern:

```
[Platform]_[CampaignType]_[Topic]_[Language]_[Version]

Examples:
Zengo_Onboarding_Welcome_EN_v1
Zengo_FIFA_WorldCupWinner_EN_v1
Zengo_FIFA_SemiFinal_FR_v1
Zengo_Reactivation_60d_EN_v1
Zengo_Blast_NewMarkets_AR_v1
```

**Canvas naming:**
```
Zengo_Canvas_Onboarding_EN
Zengo_Canvas_Reactivation_60d
Zengo_Canvas_LTV_HighTier
```

---

## 9. Full Email Template — Zengo Braze Boilerplate

Paste this as the starting point for any new Zengo email in Braze's HTML editor.

```html
<!DOCTYPE html>
<html lang="{{${language} | default: 'en'}}">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>{{subject_line}}</title>
  <style>
    body  { margin:0; padding:0; background:#101010; font-family:Verdana,Geneva,sans-serif; }
    table { border-collapse:collapse; }
    img   { border:0; outline:none; text-decoration:none; display:block; }
    a     { color:#fe990c; text-decoration:none; }
    @media only screen and (max-width:600px) {
      .email-wrapper { width:100% !important; }
      .mobile-full   { width:100% !important; display:block !important; }
    }
  </style>
</head>
<body style="margin:0;padding:0;background:#101010;">

{# ─── ABORT CONDITIONS ──────────────────────────────────────────── #}
{% if custom_attribute.${zengo_verified} == false %}
  {% abort_message('User not Zengo verified') %}
{% endif %}

{# ─── CONNECTED CONTENT (if needed) ────────────────────────────── #}
{# {% connected_content https://api.zengo.com/markets/featured :save markets :cache_max_age 300 %} #}

{# ─── EMAIL WRAPPER ─────────────────────────────────────────────── #}
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0"
       style="background:#101010;">
  <tr>
    <td align="center">
      <table role="presentation" class="email-wrapper" width="640" cellpadding="0" cellspacing="0" border="0"
             style="max-width:640px;width:100%;">

        {# PREHEADER — update per campaign #}
        <tr>
          <td style="display:none;max-height:0;overflow:hidden;mso-hide:all;font-size:1px;line-height:1px;color:#101010;">
            {PREHEADER TEXT HERE}&nbsp;&#8203;&nbsp;&#8203;&nbsp;&#8203;&nbsp;&#8203;&nbsp;&#8203;&nbsp;&#8203;
          </td>
        </tr>

        {# LOGO HEADER #}
        {{content_blocks.${zengo_logo_header}}}

        {# ── HERO SECTION — dark ──────────────────────────────── #}
        <tr>
          <td style="background:#101010;padding:8px 32px 40px;">
            <p style="margin:0 0 12px;font-family:Verdana,Geneva,sans-serif;font-size:11px;font-weight:700;
                       letter-spacing:2px;text-transform:uppercase;color:#fe990c;">
              <span style="display:inline-block;width:6px;height:6px;background:#fe990c;border-radius:50%;
                           vertical-align:middle;margin-right:8px;"></span>
              {EYEBROW TEXT}
            </p>
            <h1 style="margin:0 0 16px;font-family:Verdana,Geneva,sans-serif;font-size:36px;font-weight:700;
                        line-height:1.1;color:#ffffff;">
              {HEADLINE}
            </h1>
            <p style="margin:0 0 28px;font-family:Verdana,Geneva,sans-serif;font-size:15px;line-height:1.65;color:#a7aab3;">
              {SUB-COPY}
            </p>
            <table role="presentation" cellpadding="0" cellspacing="0" border="0">
              <tr>
                <td style="background:#fe990c;border-radius:100px;padding:14px 32px;">
                  <a href="{CTA_URL}"
                     style="font-family:Verdana,Geneva,sans-serif;font-size:15px;font-weight:700;
                            color:#101010;text-decoration:none;display:block;white-space:nowrap;">
                    {CTA TEXT} &rarr;
                  </a>
                </td>
              </tr>
            </table>
          </td>
        </tr>

        {# ── CONTENT SECTIONS — add/remove as needed ─────────── #}

        {# ── ORANGE CTA SECTION ───────────────────────────────── #}
        {{content_blocks.${zengo_orange_cta}}}

        {# ── FOOTER / DISCLAIMER ──────────────────────────────── #}
        {{content_blocks.${zengo_dark_footer}}}

        {# Braze required footer — unsubscribe + address #}
        {{${email_footer}}}

      </table>
    </td>
  </tr>
</table>

</body>
</html>
```

---

## 10. Liquid Personalization Tokens — Zengo-Specific

| Use case | Liquid tag |
|---|---|
| First name greeting | `{{${first_name} \| default: 'there'}}` |
| Country-specific content | `{% if ${country} == 'GB' %}...{% endif %}` |
| Language-specific copy | `{% if ${language} == 'fr' %}...{% endif %}` |
| User's Zengo balance | `{{custom_attribute.${zengo_balance} \| default: '0'}}` |
| Prediction count | `{{custom_attribute.${zengo_prediction_count} \| default: '0'}}` |
| Yes/No pricing from API | `{{markets.featured.yes_price}}` (via Connected Content) |
| Unsubscribe link | `{{${set_user_to_unsubscribed_url}}}` |
| Preference center | `{{${preference_center_url}}}` |
| Canvas entry property | `{{canvas_entry_properties.${event_name}}}` |

---

## 11. Key Design Tokens (unchanged from Zengo design system)

| Token | Value | Usage |
|---|---|---|
| Ink | `#101010` | Dark section backgrounds |
| Card dark | `#202020` | Cards on dark sections |
| White | `#ffffff` | Light section backgrounds |
| Orange | `#fe990c` | CTA, eyebrow dots, accents |
| Teal | `#00cecb` | YES badge, live dot |
| Red | `#ff5e5b` | NO badge |
| Cream | `#ebe8e5` | Countdown cells, feature card bg |
| Body muted | `#a7aab3` | Body text on dark |
| Caption muted | `#707482` | Labels, captions on dark |
| Font | Verdana (email fallback for Satoshi) | All email text |
| S3 base | `https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/` | All image assets |
