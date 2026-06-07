# Zengo Countdown Timer Pattern

## The core problem: email clients don't run JavaScript

JavaScript-based countdowns work in browsers but **never in email clients** (Gmail, Outlook, Apple Mail, etc.). To show a live countdown in email, you need a server-rendered image that re-renders the current countdown every time the email is opened.

---

## How it works in production

```
Email open → email client loads <img src="https://countdown-service/timer.gif?to=2026-07-14">
           → server calculates current time delta
           → server returns a GIF with the live countdown
           → recipient sees the current count, not the sent-time count
```

Every open shows a fresh countdown. Cached by most clients for ~60s, which is accurate enough.

---

## Option 1 — Sendtric (Free, Recommended for getting started)

**Setup (one-time):**
1. Go to [sendtric.com](https://www.sendtric.com/)
2. Create a timer: set end date = July 14, 2026 18:00 UTC
3. Choose colors: Background `#ebe8e5`, text `#101010`
4. Copy the embed URL: `https://free.sendtric.com/embed/{YOUR_TIMER_ID}`

**Email HTML:**
```html
<!-- Countdown Section — white bg -->
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0" style="background:#ffffff;">
  <tr>
    <td align="center" style="padding:40px 32px 32px;">
      <p style="margin:0 0 6px;font-family:Verdana,sans-serif;font-size:11px;font-weight:700;
                letter-spacing:2px;text-transform:uppercase;color:#707482;">SEMI-FINALS COUNTDOWN</p>
      <h3 style="margin:0 0 20px;font-family:Verdana,sans-serif;font-size:20px;
                  font-weight:700;color:#101010;">The Last Four takes shape in...</h3>
      <!-- LIVE COUNTDOWN IMAGE — re-renders on every open -->
      <img src="https://free.sendtric.com/embed/{YOUR_TIMER_ID}"
           alt="Countdown to semi-final"
           width="320"
           style="display:block;margin:0 auto;border:0;">
      <p style="margin:16px 0 0;font-family:Verdana,sans-serif;font-size:12px;color:#707482;">
        First semi-final: July 14, 2026 &middot; MetLife Stadium, New Jersey
      </p>
    </td>
  </tr>
</table>
```

---

## Option 2 — Countdownmail.com (No setup, URL-parameterized)

No account needed — pass all config via URL parameters:

```
https://countdownmail.com/api/create?skin=6&from=2026-07-14+18:00:00&color=101010&src=zengo.com
```

Parameters:
| Param | Value | Notes |
|---|---|---|
| `skin` | `6` | Minimal style — closest to Zengo design |
| `from` | `2026-07-14+18:00:00` | Target date (URL-encoded space = +) |
| `color` | `101010` | Text color hex (no #) |
| `src` | `zengo.com` | Your domain (for their tracking) |

**Email HTML:**
```html
<img src="https://countdownmail.com/api/create?skin=6&from=2026-07-14+18:00:00&color=101010&src=zengo.com"
     alt="37 days remaining"
     width="300"
     style="display:block;margin:0 auto;border:0;">
```

> ⚠️ Skin colors may not match Zengo's cream boxes exactly. Test before sending.

---

## Option 3 — Custom Branded Endpoint (Production / Best Quality)

For exact Zengo styling (`#ebe8e5` cream boxes, Verdana, Zengo token sizes), build a serverless function:

**Endpoint spec:**
```
GET https://countdown.zengo.com/timer.png?to=2026-07-14T18:00:00Z

Response: image/png (regenerated on each request)
```

**Stack:** Vercel Edge Function or AWS Lambda + `canvas` or `sharp` npm package

**Implementation (Node.js / Vercel):**
```javascript
// /api/timer.js
import { createCanvas } from 'canvas';

export default function handler(req, res) {
  const target = new Date(req.query.to || '2026-07-14T18:00:00Z');
  const now    = new Date();
  const diff   = target - now;

  const days  = Math.max(0, Math.floor(diff / 86400000));
  const hours = Math.max(0, Math.floor((diff % 86400000) / 3600000));
  const mins  = Math.max(0, Math.floor((diff % 3600000) / 60000));
  const secs  = Math.max(0, Math.floor((diff % 60000) / 1000));

  // Render: 4 cream cells + separators
  const canvas = createCanvas(340, 100);
  const ctx    = canvas.getContext('2d');

  // Background transparent
  ctx.clearRect(0, 0, 340, 100);

  const cells = [
    { val: String(days).padStart(2,'0'),  label: 'DAYS' },
    { val: String(hours).padStart(2,'0'), label: 'HRS'  },
    { val: String(mins).padStart(2,'0'),  label: 'MINS' },
    { val: String(secs).padStart(2,'0'),  label: 'SECS' },
  ];

  let x = 0;
  cells.forEach((c, i) => {
    // Cream box
    ctx.fillStyle = '#ebe8e5';
    ctx.beginPath();
    ctx.roundRect(x, 0, 70, 80, 8);
    ctx.fill();

    // Number
    ctx.fillStyle = '#101010';
    ctx.font = 'bold 32px Verdana';
    ctx.textAlign = 'center';
    ctx.fillText(c.val, x + 35, 48);

    // Label
    ctx.fillStyle = '#707482';
    ctx.font = '10px Verdana';
    ctx.fillText(c.label, x + 35, 68);

    x += 70;

    // Separator
    if (i < 3) {
      ctx.fillStyle = '#101010';
      ctx.font = 'bold 28px Verdana';
      ctx.fillText(':', x + 8, 44);
      x += 20;
    }
  });

  const buf = canvas.toBuffer('image/png');
  res.setHeader('Content-Type', 'image/png');
  res.setHeader('Cache-Control', 'no-cache, max-age=60');
  res.send(buf);
}
```

**Braze email HTML:**
```html
<img src="https://countdown.zengo.com/timer.png?to=2026-07-14T18:00:00Z"
     alt="Countdown to World Cup Semi-Final"
     width="340"
     style="display:block;margin:0 auto;border:0;">
```

---

## Option 4 — Braze Connected Content wrapper (for dynamic dates)

When the target date is campaign-specific (varies per send), use Connected Content so the URL is built via Liquid:

```liquid
{% assign semi_date = "2026-07-14T18%3A00%3A00Z" %}

<img src="https://countdown.zengo.com/timer.png?to={{semi_date}}"
     alt="Countdown timer"
     width="340"
     style="display:block;margin:0 auto;border:0;">
```

Or with a Sendtric embed that has a static ID (timer ID created at campaign setup):
```liquid
<img src="https://free.sendtric.com/embed/{{campaign.${timer_id} | default: 'FALLBACK_ID'}}"
     alt="Days until semi-final"
     width="320"
     style="display:block;margin:0 auto;">
```

---

## For Mockups / Browser Previews Only (not for email)

In browser preview HTML files (`.html` files opened locally), use JavaScript:

```html
<div id="countdown" style="display:inline-flex;gap:0;align-items:center;"></div>

<script>
var target = new Date('2026-07-14T18:00:00Z').getTime();
function pad(n) { return n < 10 ? '0' + n : n; }
function render(diff) {
  var parts = [
    { v: Math.floor(diff/86400000),           l: 'DAYS' },
    { v: Math.floor(diff%86400000/3600000),   l: 'HRS'  },
    { v: Math.floor(diff%3600000/60000),      l: 'MINS' },
    { v: Math.floor(diff%60000/1000),         l: 'SECS' },
  ];
  var html = '';
  parts.forEach(function(p, i) {
    html += '<div style="background:#ebe8e5;border-radius:10px;padding:14px 18px;text-align:center;min-width:64px;">'
          + '<span style="font-family:Verdana;font-size:32px;font-weight:700;color:#101010;display:block;line-height:1;">' + pad(p.v) + '</span>'
          + '<span style="font-family:Verdana;font-size:10px;color:#707482;text-transform:uppercase;letter-spacing:1px;display:block;margin-top:6px;">' + p.l + '</span>'
          + '</div>';
    if (i < 3) html += '<span style="font-size:28px;font-weight:700;color:#101010;padding:0 8px;padding-bottom:20px;">:</span>';
  });
  document.getElementById('countdown').innerHTML = html;
}
function tick() {
  var diff = Math.max(0, target - Date.now());
  render(diff);
}
tick();
setInterval(tick, 1000);
</script>
```

> **⚠️ Never use this in the actual email code.** JavaScript is stripped by all email clients. For email, use Option 1, 2, or 3 above.

---

## Countdown Design Spec (Zengo brand)

| Element | Value |
|---|---|
| Box background | `#ebe8e5` (cream) |
| Box border-radius | `10px` |
| Box padding | `14px 18px` |
| Number font | Verdana, bold, 32px |
| Number color | `#101010` |
| Label font | Verdana, 10px |
| Label color | `#707482` |
| Label style | uppercase, letter-spacing 1px |
| Separator | `:` in `#101010`, bold 28px |
| Section background | `#ffffff` (white) |
| Container border | `1px solid #ebebeb`, `border-radius:20px` |

---

## Campaign checklist

- [ ] Timer end date/time confirmed (in UTC)
- [ ] Timer ID created in Sendtric (or custom endpoint deployed)
- [ ] Image URL tested in browser — renders correct countdown
- [ ] Fallback `alt` text set (e.g. "37 days remaining" at send time)
- [ ] Tested in Gmail + Outlook + Apple Mail (confirm image loads, not blocked)
- [ ] Cache-Control header set to `max-age=60` on custom endpoint
