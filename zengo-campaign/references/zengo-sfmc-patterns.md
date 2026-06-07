# Zengo SFMC Email Patterns

Zengo emails use the **same eToro SFMC base template + content injection architecture** as all eToro emails. Read `etoro-email-builder` skill first to understand the base system. This file documents Zengo-specific adaptations only.

## Critical differences vs eToro emails

| Item | eToro | Zengo |
|---|---|---|
| `@HideHeader` | omitted (shows eToro logo) | **`"true"`** — always suppress eToro logo |
| First content block | hero image or text | **Zengo wordmark block** (replaces header) |
| `@theme` | `"DarkBlueGreen"` | `"DarkBlueGreen"` (still required for base CSS) |
| `@CampaignGroup` | `"eToro{Product}"` | **`"eToroZengo"`** |
| Primary accent | `#13c636` green | **`#fe990c`** orange |
| Page background | `#000021` | **`#101010`** |
| Body text | `rgba(255,255,255,0.6)` | **`#a7aab3`** |
| Card border | `rgba(19,198,54,0.25)` | **`rgba(254,153,12,0.25)`** |
| CTA bg | `#13c636` | **`#fe990c`** |
| CTA text | `#000021` | **`#101010`** |
| Yes badge bg/text | n/a | `#002929` / `#00cecb` |
| No badge bg/text | n/a | `#331312` / `#ff5e5b` |

---

## 1. AMPscript Variable Block

```
%%[ set @fallback = "en-gb"
    set @HideHeader = "true"
    set @CampaignGroup = "eToroZengo"
    set @CampaignSubGroup = "FIFA_WorldCup2026_Winner"
    set @subject = "{Email subject line}"
    set @preheader = "{Preheader text shown in inbox preview.}"
    set @TrackingLink = "?utm_medium=email&utm_source={sourceID}&utm_campaign=eToroZengo_{CampaignSubGroup}_{jobID}_{CampaignName}"
]%%
<!--theme: %%[ set @theme = "DarkBlueGreen" ]%% -->
<!--newSTR-->
```

---

## 2. Preheader (identical to eToro pattern)

```html
<!-- PREHEADER --><div style="display:none;font-size:1px;color:#101010;line-height:1px;max-height:0px;max-width:0px;opacity:0;overflow:hidden;">
 %%=v(@preheader)=%%</div>
```

---

## 3. Zengo Design Tokens

| Token | Hex / Value | Usage |
|---|---|---|
| Page/section background | `#101010` | All section `bgcolor` and `background-color` |
| Orange accent | `#fe990c` | CTAs, eyebrows, active accents, step circles |
| Teal | `#00cecb` | Yes badge text, live market eyebrow dot |
| Red | `#ff5e5b` | No badge text |
| Dark card bg | `#202020` | Market/team cards on dark sections |
| MiniCard bg | `#1b1c1d` | Market cards on white sections |
| Card border | `rgba(254,153,12,0.25)` | Zengo card borders (orange tint) |
| MiniCard border | `rgba(255,255,255,0.06)` | Cards on white section bg |
| White section bg | `#ffffff` | Live markets + FIFA sections |
| Cream | `#ebe8e5` | Countdown cells, cream feature card |
| Heading text | `#ffffff` | All headings on dark bg |
| Heading text (light section) | `#101010` | Headings on white bg |
| Body text | `#a7aab3` | Paragraphs on dark bg |
| Body text (light section) | `#707482` | Captions/meta on white bg |
| Yes badge bg | `#002929` | Yes outcome badge background |
| Yes badge text | `#00cecb` | Yes outcome badge text |
| No badge bg | `#331312` | No outcome badge background |
| No badge text | `#ff5e5b` | No outcome badge text |
| Split bar Yes | `#004f4d` | Teal side of probability split bar |
| Split bar No | `#4a1614` | Red side of probability split bar |
| Disclaimer text | `rgba(255,255,255,0.35)` | Legal/regulatory text |
| Divider line | `rgba(255,255,255,0.1)` | Horizontal rules |
| Font stack | `Verdana,sans-serif` | All text |
| Email max-width | `640px` | All outer wrappers |
| Content inner width | `560px` | Inner td in Outlook conditionals |
| Side padding | `40px` | Left/right on `column-wrapper` tds |

---

## 4. Section Wrapper (Zengo dark — replaces `#000021` with `#101010`)

```html
<!-- ===== SECTION NAME ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding-bottom:{N}px;padding-left:40px;padding-right:40px;padding-top:{N}px;text-align:{left|center}">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%;text-align:{left|center}">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">

      {CONTENT ROWS}

     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

### Section Wrapper — White background (for live markets + FIFA sections)

Replace every `#101010` with `#ffffff`:

```html
<!--[if mso | IE]><table ... bgcolor="#ffffff"><![endif]--><div style="background:#ffffff;background-color:#ffffff;...">
 <table ... style="background:#ffffff;background-color:#ffffff;...">
```

---

## 5. Zengo Wordmark Header Block

**Always the first content block** (suppresses eToro logo via `@HideHeader = "true"`).

```html
<!-- ===== ZENGO LOGO HEADER ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td style="padding:20px 32px;font-size:0px">
    <img src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/zengo-wordmark-white.png"
         width="150" height="37" alt="Zengo"
         style="display:block;width:150px;height:auto;border:0" /></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 6. Hero Image Block (full-width)

```html
<!-- ===== HERO IMAGE ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td style="font-size:0px;padding:0 16px;word-break:break-word">
    <img src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/hero.png"
         width="608" alt="" style="display:block;width:100%;height:auto;border:0;border-radius:16px" /></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

- Side padding `0 16px` keeps 16px gap each side on 640px wrapper
- `border-radius:16px` on image (note: Outlook ignores this — acceptable)
- Default hero: `hero.png`. Alternate: `img-88e6.png` (female), `img-b8fb.png` (lifestyle grid)

---

## 7. Hero Text Section

```html
<!-- ===== HERO TEXT ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding-bottom:16px;padding-left:40px;padding-right:40px;padding-top:36px;text-align:left">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%;text-align:left">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">
      <!-- Eyebrow -->
      <tr>
       <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:12px;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:11px;font-weight:bold;letter-spacing:0.12em;line-height:16px;color:#fe990c;text-align:left;text-transform:uppercase">
         ● &nbsp;{EYEBROW LABEL}</div></td></tr>
      <!-- Headline -->
      <tr>
       <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:14px;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:28px;font-weight:bold;line-height:34px;letter-spacing:-0.03em;color:#ffffff;text-align:left">
         {Main headline}<br>
         <span style="color:#fe990c">{Orange accent line}</span></div></td></tr>
      <!-- Body -->
      <tr>
       <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:28px;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:14px;line-height:22px;color:#a7aab3;text-align:left">
         {Body copy}</div></td></tr>
     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 8. Primary CTA Button (orange pill)

```html
<!-- ===== CTA ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding-bottom:40px;padding-left:40px;padding-right:40px;padding-top:0;text-align:center">
    <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="border-collapse:separate;width:220px;line-height:100%;margin:0 auto">
     <tr>
      <td align="center" bgcolor="#fe990c" role="presentation" style="border:0;border-radius:77px;cursor:auto;mso-padding-alt:12px 28px;background:#fe990c" valign="middle">
       <a alias="cta-{slug}" href="{URL}%%=v(@TrackingLink)=%%" style="display:inline-block;width:164px;background:#fe990c;color:#101010;font-family:Verdana,sans-serif;font-size:15px;font-weight:bold;line-height:22px;margin:0;text-decoration:none;text-transform:none;padding:12px 28px;mso-padding-alt:0;border-radius:77px" target="_blank">{Button Label}</a></td></tr></table></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 9. Stats Bar (dark background)

```html
<!-- ===== STATS BAR ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td style="padding:0 16px 16px;font-size:0">
    <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%"
           style="background:#1a1a1a;border-radius:12px">
     <tr>
      <td width="33%" style="padding:20px 12px;text-align:center;border-right:1px solid #2a2a2a;word-break:break-word">
       <div style="font-family:Verdana,sans-serif;font-size:22px;font-weight:bold;line-height:1;letter-spacing:-0.03em;color:#ffffff;margin-bottom:4px">{STAT VALUE}</div>
       <div style="font-family:Verdana,sans-serif;font-size:10px;font-weight:bold;color:#707482;text-transform:uppercase;letter-spacing:0.06em">{STAT LABEL}</div></td>
      <td width="33%" style="padding:20px 12px;text-align:center;border-right:1px solid #2a2a2a;word-break:break-word">
       <div style="font-family:Verdana,sans-serif;font-size:22px;font-weight:bold;line-height:1;letter-spacing:-0.03em;color:#ffffff;margin-bottom:4px">{STAT VALUE}</div>
       <div style="font-family:Verdana,sans-serif;font-size:10px;font-weight:bold;color:#707482;text-transform:uppercase;letter-spacing:0.06em">{STAT LABEL}</div></td>
      <td width="33%" style="padding:20px 12px;text-align:center;word-break:break-word">
       <div style="font-family:Verdana,sans-serif;font-size:22px;font-weight:bold;line-height:1;letter-spacing:-0.03em;color:#ffffff;margin-bottom:4px">{STAT VALUE}</div>
       <div style="font-family:Verdana,sans-serif;font-size:10px;font-weight:bold;color:#707482;text-transform:uppercase;letter-spacing:0.06em">{STAT LABEL}</div></td>
     </tr>
    </table></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

**Default stats for Zengo:**
- `$170M+` · Market volume
- `32` · Team outcomes
- `Jul 19` · Market closes

---

## 10. Live Markets Section Header (white bg)

```html
<!-- ===== LIVE MARKETS HEADER ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#ffffff"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#ffffff;background-color:#ffffff;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ffffff;background-color:#ffffff;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding:28px 40px 8px;text-align:left">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%;text-align:left">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">
      <!-- Teal eyebrow -->
      <tr>
       <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:4px;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:11px;font-weight:bold;letter-spacing:0.10em;line-height:16px;color:#00cecb;text-align:left;text-transform:uppercase">
         ● &nbsp;Live from Polymarket</div></td></tr>
      <!-- Market name -->
      <tr>
       <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:4px;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:20px;font-weight:bold;line-height:26px;letter-spacing:-0.03em;color:#101010;text-align:left">
         {Market Title}</div></td></tr>
      <!-- Market meta -->
      <tr>
       <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:0;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:12px;line-height:18px;color:#707482;text-align:left">
         {$XXXm Vol} · Ends {date}</div></td></tr>
     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 11. Team/Market Card (2-column grid, white section)

Team cards sit inside a white section wrapper. Each row is a 2-column layout using side-by-side `<td>` elements.

```html
<!-- ===== TEAM CARDS ROW ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#ffffff"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#ffffff;background-color:#ffffff;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ffffff;background-color:#ffffff;width:100%">
  <tr>
   <td style="padding:0 28px 12px;font-size:0">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td style="vertical-align:top;width:272px"><![endif]--><div style="display:inline-block;vertical-align:top;width:49%;max-width:272px;padding-right:6px">

     <!-- LEFT CARD -->
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%"
            style="background:#1b1c1d;border-radius:14px;border:1px solid rgba(255,255,255,0.06)">
      <tr><td style="padding:16px 16px 14px">
       <!-- Flag + team name row -->
       <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%" style="margin-bottom:10px">
        <tr>
         <td style="vertical-align:middle">
          <table border="0" cellpadding="0" cellspacing="0" role="presentation">
           <tr>
            <td style="padding-right:8px;vertical-align:middle">
             <img src="https://flagcdn.com/w40/{cc}.png" width="26" height="17" alt="{Country}"
                  style="display:block;width:26px;height:auto;border-radius:2px;border:0" /></td>
            <td style="vertical-align:middle">
             <div style="font-family:Verdana,sans-serif;font-size:13px;font-weight:bold;color:#ffffff;margin-bottom:2px">{Country Name}</div>
             <div style="font-family:Verdana,sans-serif;font-size:10px;color:#707482">{Market label e.g. Win the 2026 World Cup}</div></td></tr></table></td>
         <td style="text-align:right;vertical-align:middle">
          <div style="font-family:Verdana,sans-serif;font-size:20px;font-weight:bold;letter-spacing:-0.03em;color:#ffffff">{XX}%</div></td></tr></table>
       <!-- Split probability bar -->
       <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%" style="margin-bottom:6px">
        <tr>
         <td width="{YES_PCT}%" height="5" style="background:#004f4d;border-radius:4px 0 0 4px;font-size:0;line-height:0">&nbsp;</td>
         <td width="{NO_PCT}%" height="5" style="background:#4a1614;border-radius:0 4px 4px 0;font-size:0;line-height:0">&nbsp;</td></tr></table>
       <!-- Cent pricing -->
       <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%" style="margin-bottom:12px">
        <tr>
         <td style="font-family:Verdana,sans-serif;font-size:10px;font-weight:bold;color:#00cecb">Yes {XX}¢</td>
         <td style="font-family:Verdana,sans-serif;font-size:10px;font-weight:bold;color:#ff5e5b;text-align:right">No {XX}¢</td></tr></table>
       <!-- YES / NO buttons -->
       <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
        <tr>
         <td width="48%">
          <a href="https://go.zengo.com/AJDQ/n5fzujtk%%=v(@TrackingLink)=%%" style="display:block;text-align:center;background:#002929;color:#00cecb;font-family:Verdana,sans-serif;font-size:11px;font-weight:bold;padding:8px 0;border-radius:8px;text-decoration:none" target="_blank">YES</a></td>
         <td width="4%"></td>
         <td width="48%">
          <a href="https://go.zengo.com/AJDQ/n5fzujtk%%=v(@TrackingLink)=%%" style="display:block;text-align:center;background:#331312;color:#ff5e5b;font-family:Verdana,sans-serif;font-size:11px;font-weight:bold;padding:8px 0;border-radius:8px;text-decoration:none" target="_blank">NO</a></td></tr></table>
      </td></tr></table>

    </div><!--[if mso | IE]></td><td style="vertical-align:top;width:272px"><![endif]--><div style="display:inline-block;vertical-align:top;width:49%;max-width:272px;padding-left:6px">

     <!-- RIGHT CARD — same structure, different team data -->

    </div><!--[if mso | IE]></td></tr></table><![endif]-->
   </td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

**Country code → flagcdn.com URL:**
- France → `fr`, Spain → `es`, England → `gb-eng`, Argentina → `ar`, Brazil → `br`, Germany → `de`, Portugal → `pt`, Netherlands → `nl`, Italy → `it`, USA → `us`, Morocco → `ma`, Japan → `jp`

---

## 12. FIFA Section — White bg + Cream Countdown

```html
<!-- ===== FIFA SECTION ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#ffffff"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#ffffff;background-color:#ffffff;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ffffff;background-color:#ffffff;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding:24px 40px 32px;text-align:center">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%;text-align:center">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">

      <!-- FIFA Crest -->
      <tr>
       <td align="center" style="font-size:0px;padding-bottom:20px;word-break:break-word">
        <img src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/fifa-crest.png"
             width="80" alt="FIFA World Cup 2026" style="display:inline-block;width:80px;height:auto;border:0" /></td></tr>

      <!-- Headline: two lines -->
      <tr>
       <td align="center" style="font-size:0px;padding-bottom:24px;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:26px;font-weight:bold;line-height:1.15;letter-spacing:-0.03em;color:#101010;text-align:center">
         Back your team.<br><span style="color:#fe990c">Make your call.</span></div></td></tr>

      <!-- Countdown — cream cells -->
      <tr>
       <td align="center" style="font-size:0px;padding-bottom:24px;word-break:break-word">
        <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="margin:0 auto">
         <tr>
          <td style="padding:0 4px">
           <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ebe8e5;border-radius:12px;width:64px">
            <tr><td style="padding:12px 6px;text-align:center">
             <div style="font-family:Verdana,sans-serif;font-size:28px;font-weight:bold;letter-spacing:-0.03em;color:#101010;line-height:1">04</div>
             <div style="font-family:Verdana,sans-serif;font-size:9px;font-weight:bold;color:#707482;text-transform:uppercase;letter-spacing:0.06em;margin-top:3px">Days</div>
            </td></tr></table></td>
          <td style="font-family:Verdana,sans-serif;font-size:22px;font-weight:bold;color:#101010;padding:0 2px 12px;vertical-align:middle">:</td>
          <td style="padding:0 4px">
           <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ebe8e5;border-radius:12px;width:64px">
            <tr><td style="padding:12px 6px;text-align:center">
             <div style="font-family:Verdana,sans-serif;font-size:28px;font-weight:bold;letter-spacing:-0.03em;color:#101010;line-height:1">12</div>
             <div style="font-family:Verdana,sans-serif;font-size:9px;font-weight:bold;color:#707482;text-transform:uppercase;letter-spacing:0.06em;margin-top:3px">Hours</div>
            </td></tr></table></td>
          <td style="font-family:Verdana,sans-serif;font-size:22px;font-weight:bold;color:#101010;padding:0 2px 12px;vertical-align:middle">:</td>
          <td style="padding:0 4px">
           <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ebe8e5;border-radius:12px;width:64px">
            <tr><td style="padding:12px 6px;text-align:center">
             <div style="font-family:Verdana,sans-serif;font-size:28px;font-weight:bold;letter-spacing:-0.03em;color:#101010;line-height:1">03</div>
             <div style="font-family:Verdana,sans-serif;font-size:9px;font-weight:bold;color:#707482;text-transform:uppercase;letter-spacing:0.06em;margin-top:3px">Mins</div>
            </td></tr></table></td>
          <td style="font-family:Verdana,sans-serif;font-size:22px;font-weight:bold;color:#101010;padding:0 2px 12px;vertical-align:middle">:</td>
          <td style="padding:0 4px">
           <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ebe8e5;border-radius:12px;width:64px">
            <tr><td style="padding:12px 6px;text-align:center">
             <div style="font-family:Verdana,sans-serif;font-size:28px;font-weight:bold;letter-spacing:-0.03em;color:#101010;line-height:1">07</div>
             <div style="font-family:Verdana,sans-serif;font-size:9px;font-weight:bold;color:#707482;text-transform:uppercase;letter-spacing:0.06em;margin-top:3px">Secs</div>
            </td></tr></table></td>
         </tr></table></td></tr>

      <!-- Tagline -->
      <tr>
       <td align="center" style="font-size:0px;padding-bottom:24px;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:bold;letter-spacing:-0.01em;color:#101010;text-align:center">
         48 nations. 104 matches. One winning bracket.</div></td></tr>

     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 13. Orange CTA Section (with Zengo coins)

```html
<!-- ===== ORANGE CTA SECTION ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#fe990c"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#fe990c;background-color:#fe990c;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#fe990c;background-color:#fe990c;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding:44px 40px;text-align:center">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%;text-align:center">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">
      <!-- Coins image -->
      <tr>
       <td align="center" style="font-size:0px;padding-bottom:16px;word-break:break-word">
        <img src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/cta-coins.png"
             width="120" alt="" style="display:inline-block;width:120px;height:auto;border:0" /></td></tr>
      <!-- Headline -->
      <tr>
       <td align="center" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:10px;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:22px;font-weight:bold;line-height:1.2;letter-spacing:-0.03em;color:#101010;text-align:center">
         {CTA headline}</div></td></tr>
      <!-- Subtext -->
      <tr>
       <td align="center" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:24px;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:13px;line-height:1.6;color:#101010;text-align:center;max-width:380px;margin:0 auto">
         {CTA subtext}</div></td></tr>
      <!-- Dark pill CTA -->
      <tr>
       <td align="center" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:20px;padding-left:0;word-break:break-word">
        <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="border-collapse:separate;width:200px;line-height:100%;margin:0 auto">
         <tr>
          <td align="center" bgcolor="#101010" role="presentation" style="border:0;border-radius:77px;cursor:auto;mso-padding-alt:12px 28px;background:#101010" valign="middle">
           <a alias="cta-{slug}" href="https://go.zengo.com/AJDQ/n5fzujtk%%=v(@TrackingLink)=%%" style="display:inline-block;width:144px;background:#101010;color:#ffffff;font-family:Verdana,sans-serif;font-size:15px;font-weight:bold;line-height:22px;margin:0;text-decoration:none;text-transform:none;padding:12px 28px;mso-padding-alt:0;border-radius:77px" target="_blank">Download Zengo</a></td></tr></table></td></tr>
      <!-- QR code -->
      <tr>
       <td align="center" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:0;padding-left:0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:11px;color:#101010;opacity:0.6;margin-bottom:8px">Or scan to download</div>
        <img src="https://etoro-production.s3.eu-west-1.amazonaws.com/e-marketing/MarketingAutomation/Zengo/qr.png"
             width="72" alt="Scan to download Zengo" style="display:inline-block;width:72px;height:auto;border-radius:6px;border:0" /></td></tr>
     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 14. Divider (identical to eToro pattern, bg changes to `#101010`)

```html
<!-- ===== DIVIDER ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td style="padding:0 40px;font-size:0;line-height:0">
    <div style="height:1px;background:rgba(255,255,255,0.1);font-size:0;line-height:0">&nbsp;</div></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 15. Disclaimer (Zengo 3-part regulatory text)

Uses `disclaimer-wrapper-outlook` / `disclaimer-wrapper` classes (same as eToro):

```html
<!-- ===== DISCLAIMER ===== -->
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="disclaimer-wrapper-outlook" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div class="disclaimer-wrapper" style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0;padding:22px 40px;text-align:left">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0px;text-align:left;direction:ltr;display:inline-block;vertical-align:top;width:100%">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">
      <tr>
       <td align="left" style="font-size:0;padding:8px 0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:13px;line-height:19px;text-align:left;color:rgba(255,255,255,0.35)">
         <i>Cryptoassets are highly volatile. Your capital is at risk. The value of your position may go down as well as up and you may receive back less than you invest. Past performance is not a reliable indicator of future results.</i></div></td></tr>
      <tr>
       <td align="left" style="font-size:0;padding:4px 0 8px;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:13px;line-height:19px;text-align:left;color:rgba(255,255,255,0.35)">
         <i>Zengo is a non-custodial wallet. You are solely responsible for safeguarding access to your assets. Zengo Ltd does not hold, custody, or control your funds.</i></div></td></tr>
      <tr>
       <td align="left" style="font-size:0;padding:4px 0 8px;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:13px;line-height:19px;text-align:left;color:rgba(255,255,255,0.35)">
         <i>eToro (UK) Ltd. is authorised and regulated by the Financial Conduct Authority (FCA). eToro (Europe) Ltd. is authorised and regulated by the Cyprus Securities Exchange Commission (CySEC). eToro AUS Capital Limited is regulated by the Australian Securities and Investments Commission (ASIC). Zengo markets may not be available in all regions. Subject to local regulation.</i></div></td></tr>
     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 16. Full Email Block Output Order

```
AMPscript block (with @HideHeader = "true")
<!--theme: DarkBlueGreen -->
<!--newSTR-->
<!-- PREHEADER -->
<!-- ===== ZENGO LOGO HEADER ===== -->
<!-- ===== HERO IMAGE ===== -->
<!-- ===== HERO TEXT ===== -->
<!-- ===== CTA ===== -->
<!-- ===== STATS BAR ===== -->
<!-- ===== LIVE MARKETS HEADER ===== -->
<!-- ===== TEAM CARDS ROW ===== -->  (repeat per row)
<!-- ===== FIFA SECTION ===== -->    (if FIFA campaign)
<!-- ===== DIVIDER ===== -->
<!-- ===== ORANGE CTA SECTION ===== -->
<!-- ===== DIVIDER ===== -->
<!-- ===== DISCLAIMER ===== -->
```

---

## 18. Side-by-Side (SBS) — 2-column layout

The SBS pattern splits a row into two equal columns using CSS classes defined in the base template. It supports a normal variant (image left) and a flipped variant (image right), achieved purely via CSS direction — no DOM change needed.

**CSS classes (base template defines these):**
- `sbs-wrapper` / `sbs-wrapper-v2` — outer container holding all SBS rows
- `sbs` — one row, columns in source order (`direction:ltr`)
- `sbs-flipped` — one row, columns reversed visually (`direction:rtl` on the wrapper `<td>`)
- `sbs-col-left` / `sbs-col-right` — the two 50% column divs
- `sbs-col-left-inner` / `sbs-col-right-inner` — inner `<td>` for each column's content
- `sbs-col-left-outlook` / `sbs-col-right-outlook` — Outlook conditional `<td>` widths
- `mj-column-per-50` — 50% column (280px on 640px email)
- `mj-full-width-mobile` — makes content full-width on mobile
- `mobile-fit` / `mobile-fit-outlook` — mobile responsive helpers

### SBS Wrapper

```html
<!-- ===== SBS SECTION ===== -->
<div class="sbs-wrapper sbs-wrapper-v2" style="{BG};margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="{BG};width:100%">
  <tr>
   <td style="direction:ltr;font-size:0;padding:0;text-align:center">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><![endif]-->

    {SBS ROWS}

    <!--[if mso | IE]></table><![endif]-->
   </td></tr></table></div>
```

### SBS Row — Normal (image left, text right)

```html
<!--[if mso | IE]><tr><td class="sbs-outlook mobile-fit-outlook" width="640px"><table align="center" border="0" cellpadding="0" cellspacing="0" class="sbs-outlook mobile-fit-outlook" role="presentation" style="width:640px" width="640"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div class="sbs mobile-fit" style="margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0;{PADDING};text-align:center">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="sbs-col-left-outlook" style="vertical-align:middle;width:280px"><![endif]-->
    <div class="mj-column-per-50 mj-outlook-group-fix sbs-col-left" style="font-size:0px;text-align:left;direction:ltr;display:inline-block;vertical-align:middle;width:100%">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%"><tr>
      <td class="sbs-col-left-inner" style="vertical-align:middle;{PADDING}" valign="middle">
       <!-- IMAGE CONTENT -->
       <table border="0" cellpadding="0" cellspacing="0" class="mj-full-width-mobile" role="presentation" style="border-collapse:collapse;border-spacing:0px"><tr>
        <td class="mj-full-width-mobile" style="width:280px">
         <img alt="{ALT}" height="auto" src="{S3_IMAGE_URL}" width="280"
              style="border:0;display:block;outline:none;text-decoration:none;height:auto;width:100%" />
        </td></tr></table>
      </td></tr></table>
    </div>
    <!--[if mso | IE]></td><td class="sbs-col-right-outlook" style="vertical-align:middle;width:280px"><![endif]-->
    <div class="mj-column-per-50 mj-outlook-group-fix sbs-col-right" style="font-size:0px;text-align:left;direction:ltr;display:inline-block;vertical-align:middle;width:100%">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%"><tr>
      <td class="sbs-col-right-inner" style="vertical-align:middle;{PADDING}" valign="middle">
       <!-- TEXT CONTENT -->
       <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
        <tr><td align="left" style="font-size:0;{PADDING};word-break:break-word">
         <div style="{HEADING STYLES}">{Title}</div></td></tr>
        <tr><td align="left" style="font-size:0;{PADDING};word-break:break-word">
         <div style="{BODY STYLES}">{Body text}</div></td></tr>
       </table>
      </td></tr></table>
    </div>
    <!--[if mso | IE]></td></tr></table><![endif]-->
   </td></tr></table></div>
<!--[if mso | IE]></td></tr></table></td></tr><![endif]-->
```

### SBS Row — Flipped (image right, text left)

Identical structure but:
1. Outer class is `sbs-flipped` / `sbs-flipped-outlook`
2. `column-wrapper` td uses `direction:rtl` — this reverses visual order without changing DOM
3. Both column divs still use `direction:ltr` internally

```html
<!--[if mso | IE]><tr><td class="sbs-flipped-outlook mobile-fit-outlook" width="640px"><table align="center" border="0" cellpadding="0" cellspacing="0" class="sbs-flipped-outlook mobile-fit-outlook" role="presentation" style="width:640px" width="640"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div class="sbs-flipped mobile-fit" style="margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="width:100%">
  <tr>
   <td class="column-wrapper" style="direction:rtl;font-size:0;{PADDING};text-align:center">
    <!-- same interior structure as SBS Normal — only direction:rtl changes -->
    {LEFT COL (image) + RIGHT COL (text) — same as normal}
   </td></tr></table></div>
<!--[if mso | IE]></td></tr></table></td></tr><![endif]-->
```

### SBS Key Rules

| Rule | Detail |
|---|---|
| Normal row | `direction:ltr` on `column-wrapper` → DOM order = visual order |
| Flipped row | `direction:rtl` on `column-wrapper` → DOM order reversed visually, no HTML change |
| Column width | `mj-column-per-50` → each column is 50% (280px on 640px email) |
| Outlook column width | `width:280px` in each Outlook `<td>` conditional |
| Mobile | `mj-full-width-mobile` on the image `<td>` → full width on small screens |
| Image table | Must use `border-collapse:collapse;border-spacing:0px` to prevent client gaps |
| Rows | Each SBS row is a separate `<div class="sbs …">` inside one shared `sbs-wrapper` |
| Alternating | Typical pattern: row 1 = `sbs`, row 2 = `sbs-flipped`, row 3 = `sbs`, … |

---

## 19. Full-width Image with Link

When an image needs to be entirely clickable. Key structural detail: the inner `<table>` must use `border-collapse:collapse;border-spacing:0px` and the `<td>` must carry an explicit `width:640px` — both prevent rendering gaps in email clients.

```html
<!--[if mso | IE]><table … style="width:640px" width="640" bgcolor="{BG}"><tr><td …><![endif]--><div style="{BG};margin:0 auto;max-width:640px">
 <table … style="{BG};width:100%"><tr>
  <td style="font-size:0px;padding:0;word-break:break-word">
   <table border="0" cellpadding="0" cellspacing="0" role="presentation"
          style="border-collapse:collapse;border-spacing:0px"><tr>
    <td style="width:640px">
     <a href="{URL}%%=v(@TrackingLink)=%%" target="_blank">
      <img height="auto" src="{S3_IMAGE_URL}" width="640"
           style="border:0;display:block;outline:none;text-decoration:none;height:auto;width:100%" />
     </a>
    </td></tr></table>
  </td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## 20. AMPscript Personalization Tokens

```
%%FIRSTNAME%%          — user's first name
%%USERNAME%%           — username fallback
%%=v(@preheader)=%%    — inject preheader variable
%%=v(@TrackingLink)=%% — append to every CTA href

Conditional pattern (name fallback):
%%[IF not empty([FIRSTNAME]) AND FIRSTNAME != "UNKNOWN" THEN]%%
 <strong>%%FIRSTNAME%%</strong>
%%[ELSE]%%
 <strong>%%USERNAME%%</strong>
%%[ENDIF]%%
```

---

## 17. Zengo-specific Mistakes to Avoid

| Wrong | Correct |
|---|---|
| Using `#000021` | Use `#101010` — Zengo page bg |
| Using `#13c636` green | Use `#fe990c` orange — Zengo accent |
| Showing eToro logo | `@HideHeader = "true"` + Zengo wordmark as first block |
| Emoji flags | `<img>` from `flagcdn.com/w40/{cc}.png` — consistent across clients |
| Yes/No as plain buttons only | Must include split bar + `Yes {XX}¢ / No {XX}¢` pricing above buttons |
| White section using `bgcolor="#101010"` | White sections use `bgcolor="#ffffff"` and all `#101010` → `#ffffff` |
| Hardcoding odds | Fetch from Polymarket before each send, update manually per campaign |
| Writing `"prediction market/markets"` in copy | Use "Zengo markets", "trade on outcomes", "make your call" |
| Missing `alias="cta-{slug}"` on CTA `<a>` | Required for SFMC click tracking |
| Missing `%%=v(@TrackingLink)=%%` on hrefs | Every CTA href needs it appended after the base URL |
