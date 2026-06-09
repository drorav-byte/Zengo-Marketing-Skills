# Zengo SFMC Email Patterns

All components sourced from `Zengo___Prediction_Markets.html` (Landing Page v4).
Design tokens from `:root` — do not substitute eToro values.

**Color quick-ref (from landing page `:root`):**
- Dark section bg: `#101010` (--ink)
- Light section bg: `#ffffff` (--white)
- Orange accent: `#fe990c` (--orange) ← CORRECT value from source
- Card bg: `#202020` (--card)
- Card border: `#2f3436` (--stroke)
- Body text dark bg: `#a7aab3` (--gray-light)
- Muted labels: `#707482` (--gray)
- Yes bg/text: `#002929` / `#00cecb`
- No bg/text: `#331312` / `#ff5e5b`
- Cream: `#ebe8e5`
- CTA text on orange: `#101010`
- SFMC font: `Verdana, sans-serif`

---

## AMPScript Block — Standard

```
%%[ set @fallback = "en-gb"
    set @CampaignGroup = "eToroZengo"
    set @CampaignSubGroup = "Marketing"
    set @HideHeader = "true"
    set @subject = "{subject}"
    set @preheader = "{preheader}"
    set @TrackingLink = "?utm_medium=email&utm_source=%%jobid%%&utm_campaign=eToroZengo_Marketing_%%jobid%%_{CampaignName}"
]%%
<!--theme: %%[ set @theme = "DarkBlueGreen" ]%% -->
<!--newSTR-->
```

---

## Preheader

```html
<!-- PREHEADER --><div style="display:none;font-size:1px;color:#101010;line-height:1px;max-height:0px;max-width:0px;opacity:0;overflow:hidden;">
 %%=v(@preheader)=%%</div>
```

---

## Zengo Logo Header (replaces eToro header)

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

## Section Wrapper — Dark (`#101010`)

Every dark section uses this outer shell. Replace `{PADDING_TOP}` / `{PADDING_BOTTOM}` and inner content.

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding-bottom:{PADDING_BOTTOM}px;padding-left:40px;padding-right:40px;padding-top:{PADDING_TOP}px;text-align:{left|center}">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%;text-align:{left|center}">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">

      {ROWS}

     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

## Section Wrapper — Light (`#ffffff`)

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#ffffff"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#ffffff;background-color:#ffffff;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ffffff;background-color:#ffffff;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding-bottom:{PADDING_BOTTOM}px;padding-left:40px;padding-right:40px;padding-top:{PADDING_TOP}px;text-align:{left|center}">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%;text-align:{left|center}">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">

      {ROWS}

     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

## Section Wrapper — Orange (`#fe990c`)

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#fe990c"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#fe990c;background-color:#fe990c;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#fe990c;background-color:#fe990c;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding-bottom:{PADDING_BOTTOM}px;padding-left:40px;padding-right:40px;padding-top:{PADDING_TOP}px;text-align:center">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%;text-align:center">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">

      {ROWS}

     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## Eyebrow (teal dot variant — "Live from" style)

```html
<tr>
 <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:10px;padding-left:0;word-break:break-word">
  <div style="font-family:Verdana,sans-serif;font-size:11px;font-weight:500;letter-spacing:-0.03em;line-height:16px;color:#707482;text-align:left">
   <span style="display:inline-block;width:8px;height:8px;border-radius:50%;background:#00cecb;vertical-align:middle;margin-right:8px"></span>{Eyebrow text}</div></td></tr>
```

## Eyebrow (orange dot variant — featured/campaign style)

```html
<tr>
 <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:10px;padding-left:0;word-break:break-word">
  <div style="font-family:Verdana,sans-serif;font-size:11px;font-weight:500;letter-spacing:-0.03em;line-height:16px;color:#707482;text-align:left">
   <span style="display:inline-block;width:8px;height:8px;border-radius:50%;background:#fe990c;vertical-align:middle;margin-right:8px"></span>{Eyebrow text}</div></td></tr>
```

---

## Hero Headline (dark bg)

```html
<tr>
 <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:16px;padding-left:0;word-break:break-word">
  <div style="font-family:Verdana,sans-serif;font-size:32px;font-weight:900;line-height:1.04;letter-spacing:-0.03em;color:#ffffff;text-align:left">
   {White headline}<br><span style="color:#fe990c">{Orange accent}</span></div></td></tr>
```

## Hero Headline (light bg / FIFA-style)

```html
<tr>
 <td align="center" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:16px;padding-left:0;word-break:break-word">
  <div style="font-family:Verdana,sans-serif;font-size:32px;font-weight:900;line-height:1.04;letter-spacing:-0.03em;color:#101010;text-align:center">
   {Dark headline}<br><span style="color:#fe990c">{Orange accent}</span></div></td></tr>
```

## Lede / Body (dark bg)

```html
<tr>
 <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:16px;padding-left:0;word-break:break-word">
  <div style="font-family:Verdana,sans-serif;font-size:15px;font-weight:500;line-height:1.45;letter-spacing:-0.03em;color:#a7aab3;text-align:left">
   {Body text}</div></td></tr>
```

## Lede / Body (light bg)

```html
<tr>
 <td align="left" style="font-size:0px;padding-top:0;padding-right:0;padding-bottom:16px;padding-left:0;word-break:break-word">
  <div style="font-family:Verdana,sans-serif;font-size:15px;font-weight:500;line-height:1.45;letter-spacing:-0.03em;color:#707482;text-align:left">
   {Body text}</div></td></tr>
```

---

## CTA Button — Orange Pill (primary)

From landing page: `btn-orange` = bg `#fe990c`, color `#101010`, border-radius 90px, padding 16px 28px, font-weight 700, font-size 18px.

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding-bottom:40px;padding-left:40px;padding-right:40px;padding-top:8px;text-align:{left|center}">
    <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="border-collapse:separate;line-height:100%">
     <tr>
      <td align="center" bgcolor="#fe990c" role="presentation" style="border:0;border-radius:90px;cursor:auto;mso-padding-alt:16px 28px;background:#fe990c" valign="middle">
       <a href="{URL}%%=v(@TrackingLink)=%%" style="display:inline-block;background:#fe990c;color:#101010;font-family:Verdana,sans-serif;font-size:16px;font-weight:700;line-height:22px;margin:0;text-decoration:none;text-transform:none;padding:16px 28px;mso-padding-alt:0;border-radius:90px;letter-spacing:-0.02em" target="_blank">{CTA Label}</a></td></tr></table></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

## CTA Button — Orange Pill on Light Background

Same as above but section bg `#ffffff`:

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#ffffff"><tr><td ...
```

---

## Stats Bar (light bg — from landing page stats section)

Three stats: `$4.2B+` / `24K+` / `8M+` on white bg, large black numbers.

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#ffffff"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#ffffff;background-color:#ffffff;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ffffff;background-color:#ffffff;width:100%">
  <tr>
   <td style="font-size:0px;padding:0;word-break:break-word">
    <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
     <tr>
      <td align="center" style="padding:32px 0;width:33.33%;border-right:1px solid #e8e8e8;vertical-align:top">
       <div style="font-family:Verdana,sans-serif;font-size:32px;font-weight:900;line-height:1.05;letter-spacing:-0.03em;color:#101010">$4.2B+</div>
       <div style="font-family:Verdana,sans-serif;font-size:13px;font-weight:500;letter-spacing:-0.03em;color:#707482;margin-top:6px">Predicted volume globally</div></td>
      <td align="center" style="padding:32px 0;width:33.33%;border-right:1px solid #e8e8e8;vertical-align:top">
       <div style="font-family:Verdana,sans-serif;font-size:32px;font-weight:900;line-height:1.05;letter-spacing:-0.03em;color:#101010">24K+</div>
       <div style="font-family:Verdana,sans-serif;font-size:13px;font-weight:500;letter-spacing:-0.03em;color:#707482;margin-top:6px">Active markets worldwide</div></td>
      <td align="center" style="padding:32px 0;width:33.33%;vertical-align:top">
       <div style="font-family:Verdana,sans-serif;font-size:32px;font-weight:900;line-height:1.05;letter-spacing:-0.03em;color:#101010">8M+</div>
       <div style="font-family:Verdana,sans-serif;font-size:13px;font-weight:500;letter-spacing:-0.03em;color:#707482;margin-top:6px">Predictors on the platform</div></td>
     </tr>
    </table></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## Market Card (dark bg — from `.market-card`)

bg `#202020`, border-radius 16px, icon 46×46px.

```html
<tr>
 <td style="padding-bottom:12px">
  <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#202020;border-radius:16px;border:1px solid transparent;width:100%">
   <tr>
    <td style="padding:20px 18px 16px 18px">
     <!-- Card header: icon + title -->
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
      <tr>
       <td style="width:46px;vertical-align:middle;padding-right:10px">
        <div style="width:46px;height:46px;border-radius:6px;background:#2f3436;font-size:22px;line-height:46px;text-align:center">{ICON_EMOJI}</div></td>
       <td style="vertical-align:middle">
        <div style="font-family:Verdana,sans-serif;font-size:15px;font-weight:700;line-height:1.2;color:#ffffff">{Market Title}</div></td></tr></table>
     <!-- Divider -->
     <div style="height:1px;background:#2f3436;margin:12px 0;font-size:0;line-height:0">&nbsp;</div>
     <!-- Outcome rows -->
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
      <!-- Outcome row template (repeat for each outcome) -->
      <tr>
       <td style="padding:5px 0;vertical-align:middle">
        <div style="font-family:Verdana,sans-serif;font-size:13px;font-weight:500;color:#ffffff">{Outcome name}</div></td>
       <td style="width:44px;text-align:right;padding-right:12px;vertical-align:middle">
        <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:700;color:#bdbcc3">{17%}</div></td>
       <td style="width:50px;text-align:center;padding-right:6px;vertical-align:middle">
        <div style="display:inline-block;background:#002929;border-radius:4px;padding:3px 10px;font-family:Verdana,sans-serif;font-size:12px;font-weight:500;color:#00cecb;line-height:18px">Yes</div></td>
       <td style="width:42px;text-align:center;vertical-align:middle">
        <div style="display:inline-block;background:#331312;border-radius:4px;padding:3px 10px;font-family:Verdana,sans-serif;font-size:12px;font-weight:500;color:#ff5e5b;line-height:18px">No</div></td></tr>
     </table>
     <!-- +N outcomes -->
     <div style="font-family:Verdana,sans-serif;font-size:12px;font-weight:500;color:#707482;margin-top:8px">+{N} outcomes</div>
     <!-- Card footer -->
     <div style="height:1px;background:#2f3436;margin:12px 0;font-size:0;line-height:0">&nbsp;</div>
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
      <tr>
       <td style="vertical-align:middle">
        <div style="font-family:Verdana,sans-serif;font-size:12px;font-weight:500;color:#707482">Ends {DATE}</div></td>
       <td style="text-align:right;vertical-align:middle">
        <div style="font-family:Verdana,sans-serif;font-size:12px;font-weight:500;color:#707482">${VOL} Vol.</div></td></tr></table>
    </td></tr></table></td></tr>
```

---

## Team Card (dark bg — from `.team-card`, FIFA section)

```html
<tr>
 <td style="padding-bottom:12px">
  <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;border-radius:16px;border:1px solid #2f3436;width:100%">
   <tr>
    <td style="padding:20px 18px">
     <!-- Flag + name -->
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%" style="margin-bottom:14px">
      <tr>
       <td style="width:56px;vertical-align:middle;padding-right:10px">
        <div style="width:52px;height:52px;border-radius:6px;background:#2f3436;overflow:hidden">
         <img src="{FLAG_URL}" width="52" height="52" alt="{Country} flag" style="display:block;width:52px;height:52px;object-fit:cover;border:0" /></div></td>
       <td style="vertical-align:middle">
        <div style="font-family:Verdana,sans-serif;font-size:22px;font-weight:700;line-height:1.1;letter-spacing:-0.03em;color:#ffffff">{Team Name}</div>
        <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;color:#adb3b7;margin-top:2px">{Market subtitle e.g. Win the 2026 FIFA World Cup}</div></td></tr></table>
     <!-- Progress bar -->
     <div style="height:5px;border-radius:3px;background:#331312;overflow:hidden;margin-bottom:6px">
      <div style="height:5px;background:#00cecb;width:{YES_PCT}%;border-radius:3px"></div></div>
     <!-- Yes/No prices -->
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%" style="margin-bottom:10px">
      <tr>
       <td><div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;color:#00cecb">Yes {YES_CENTS}¢</div></td>
       <td style="text-align:right"><div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;color:#ff5e5b">No · {NO_CENTS}¢</div></td></tr></table>
     <!-- Big % -->
     <div style="font-family:Verdana,sans-serif;font-size:36px;font-weight:900;color:#bdbcc3;text-align:center">{PCT}%</div>
    </td></tr></table></td></tr>
```

---

## How It Works — 4 Steps (dark bg)

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0px;padding-bottom:40px;padding-left:40px;padding-right:40px;padding-top:40px;text-align:left">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0;direction:ltr;display:inline-block;vertical-align:top;width:100%">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">
      <tr>
       <td style="padding-bottom:28px">
        <div style="font-family:Verdana,sans-serif;font-size:24px;font-weight:900;line-height:1.08;letter-spacing:-0.03em;color:#ffffff">How it works.</div></td></tr>
      <!-- Step 1 -->
      <tr>
       <td style="padding-bottom:24px">
        <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
         <tr>
          <td style="width:36px;vertical-align:top;padding-right:16px;padding-top:2px">
           <div style="width:32px;height:32px;border-radius:50%;background:#fe990c;font-family:Verdana,sans-serif;font-size:14px;font-weight:700;color:#101010;text-align:center;line-height:32px">1</div></td>
          <td style="vertical-align:top">
           <div style="font-family:Verdana,sans-serif;font-size:15px;font-weight:700;color:#ffffff;margin-bottom:5px">Find a market</div>
           <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;line-height:1.45;color:#a7aab3">Browse hundreds of live markets across sports, crypto, politics, tech and macro — the world's deepest market liquidity, straight inside your Zengo wallet.</div></td></tr></table></td></tr>
      <!-- Step 2 -->
      <tr>
       <td style="padding-bottom:24px">
        <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
         <tr>
          <td style="width:36px;vertical-align:top;padding-right:16px;padding-top:2px">
           <div style="width:32px;height:32px;border-radius:50%;background:#fe990c;font-family:Verdana,sans-serif;font-size:14px;font-weight:700;color:#101010;text-align:center;line-height:32px">2</div></td>
          <td style="vertical-align:top">
           <div style="font-family:Verdana,sans-serif;font-size:15px;font-weight:700;color:#ffffff;margin-bottom:5px">Take a position</div>
           <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;line-height:1.45;color:#a7aab3">Each contract trades between 0¢ and $1. Take Yes at 40¢ and collect $1 if the event happens — a 150% return. Take No if you think otherwise.</div></td></tr></table></td></tr>
      <!-- Step 3 -->
      <tr>
       <td style="padding-bottom:24px">
        <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
         <tr>
          <td style="width:36px;vertical-align:top;padding-right:16px;padding-top:2px">
           <div style="width:32px;height:32px;border-radius:50%;background:#fe990c;font-family:Verdana,sans-serif;font-size:14px;font-weight:700;color:#101010;text-align:center;line-height:32px">3</div></td>
          <td style="vertical-align:top">
           <div style="font-family:Verdana,sans-serif;font-size:15px;font-weight:700;color:#ffffff;margin-bottom:5px">Trade or hold</div>
           <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;line-height:1.45;color:#a7aab3">Markets are liquid. Exit at the live price any time, or hold to collect full resolution value. Your position is always on-chain — fully transparent.</div></td></tr></table></td></tr>
      <!-- Step 4 -->
      <tr>
       <td>
        <table border="0" cellpadding="0" cellspacing="0" role="presentation" width="100%">
         <tr>
          <td style="width:36px;vertical-align:top;padding-right:16px;padding-top:2px">
           <div style="width:32px;height:32px;border-radius:50%;background:#fe990c;font-family:Verdana,sans-serif;font-size:14px;font-weight:700;color:#101010;text-align:center;line-height:32px">4</div></td>
          <td style="vertical-align:top">
           <div style="font-family:Verdana,sans-serif;font-size:15px;font-weight:700;color:#ffffff;margin-bottom:5px">Claim your wins</div>
           <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;line-height:1.45;color:#a7aab3">When markets resolve, earnings settle automatically as USDC — straight into your balance. Withdraw to your Zengo wallet any time. No volatility. No bridges.</div></td></tr></table></td></tr>
     </table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## Feature/Edge Card Row — Orange Variant

Based on `.edge-card.orange` from landing page.

```html
<tr>
 <td style="padding-bottom:12px">
  <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#fe990c;border-radius:20px;width:100%">
   <tr>
    <td style="padding:28px 28px 24px">
     <div style="font-family:Verdana,sans-serif;font-size:20px;font-weight:700;line-height:1;letter-spacing:-0.03em;color:#101010;margin-bottom:10px">{Card Headline}</div>
     <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;line-height:1.5;letter-spacing:-0.03em;color:#101010">{Card body}</div>
    </td></tr></table></td></tr>
```

## Feature/Edge Card Row — Dark Variant

Based on `.edge-card.darkc`.

```html
<tr>
 <td style="padding-bottom:12px">
  <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#202020;border-radius:20px;width:100%">
   <tr>
    <td style="padding:28px 28px 24px">
     <div style="font-family:Verdana,sans-serif;font-size:20px;font-weight:700;line-height:1;letter-spacing:-0.03em;color:#ffffff;margin-bottom:10px">{Card Headline}</div>
     <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;line-height:1.5;letter-spacing:-0.03em;color:#a7aab3">{Card body}</div>
    </td></tr></table></td></tr>
```

## Feature/Edge Card Row — Cream Variant

Based on `.edge-card.cream`.

```html
<tr>
 <td style="padding-bottom:12px">
  <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#ebe8e5;border-radius:20px;width:100%">
   <tr>
    <td style="padding:28px 28px 24px">
     <div style="font-family:Verdana,sans-serif;font-size:20px;font-weight:700;line-height:1;letter-spacing:-0.03em;color:#101010;margin-bottom:10px">{Card Headline}</div>
     <div style="font-family:Verdana,sans-serif;font-size:14px;font-weight:500;line-height:1.5;letter-spacing:-0.03em;color:#707482">{Card body}</div>
    </td></tr></table></td></tr>
```

---

## Hero Image (full-width, no padding)

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td style="font-size:0px;padding:0;word-break:break-word">
    <img src="{S3_URL}" width="640" alt="{ALT}" style="display:block;width:100%;max-width:640px;height:auto;border:0;border-radius:16px" /></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## Disclaimer Block

```html
<!--[if mso | IE]><table align="center" border="0" cellpadding="0" cellspacing="0" class="disclaimer-wrapper-outlook" role="presentation" style="width:640px" width="640" bgcolor="#101010"><tr><td style="line-height:0px;font-size:0px;mso-line-height-rule:exactly"><![endif]--><div class="disclaimer-wrapper" style="background:#101010;background-color:#101010;margin:0 auto;max-width:640px">
 <table align="center" border="0" cellpadding="0" cellspacing="0" role="presentation" style="background:#101010;background-color:#101010;width:100%">
  <tr>
   <td class="column-wrapper" style="direction:ltr;font-size:0;padding:22px 40px;text-align:left">
    <!--[if mso | IE]><table role="presentation" border="0" cellpadding="0" cellspacing="0"><tr><td class="" style="vertical-align:top;width:560px"><![endif]--><div class="mj-column-per-100 mj-outlook-group-fix" style="font-size:0px;text-align:left;direction:ltr;display:inline-block;vertical-align:top;width:100%">
     <table border="0" cellpadding="0" cellspacing="0" role="presentation" style="vertical-align:top" width="100%">
      <tr>
       <td align="left" style="font-size:0;padding:6px 0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:12px;line-height:1.4;text-align:left;color:rgba(255,255,255,0.35)">
         <i>Cryptoasset investing is highly volatile and unregulated in some jurisdictions. No consumer protection. Tax on profits may apply.</i></div></td></tr>
      <tr>
       <td align="left" style="font-size:0;padding:4px 0;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:12px;line-height:1.4;text-align:left;color:rgba(255,255,255,0.35)">
         <i>Zengo is a non-custodial wallet. Assets held in Zengo are not covered by eToro's regulatory protections. You are responsible for securing access to your wallet.</i></div></td></tr>
      <tr>
       <td align="left" style="font-size:0;padding:4px 0 8px;word-break:break-word">
        <div style="font-family:Verdana,sans-serif;font-size:12px;line-height:1.4;text-align:left;color:rgba(255,255,255,0.35)">
         <i>eToro (UK) Ltd. is authorised and regulated by the Financial Conduct Authority (FCA). eToro (Europe) Ltd. is authorised and regulated by the Cyprus Securities Exchange Commission (CySEC). eToro AUS Capital Limited is regulated by the Australian Securities and Investments Commission (ASIC).</i></div></td></tr></table></div><!--[if mso | IE]></td></tr></table><![endif]--></td></tr></table></div>
<!--[if mso | IE]></td></tr></table><![endif]-->
```

---

## Email Section Order

```
AMPScript block
<!--theme: ...-->
<!--newSTR-->
PREHEADER
ZENGO LOGO HEADER         (dark bg #101010)
HERO IMAGE                (full-width, no padding, border-radius 16px)
HERO TEXT                 (dark bg, eyebrow + headline + body + CTA)
STATS BAR                 (light bg #ffffff — optional)
LIVE MARKET CARD(S)       (dark bg #101010 with #202020 cards)
HOW IT WORKS              (dark bg #101010, orange numbered circles)
FEATURE/EDGE CARDS        (dark bg #101010, orange/cream/dark card variants)
GLOBAL AVAILABILITY       (orange bg #fe990c — optional)
CLOSING CTA               (orange bg or dark bg, large headline)
DISCLAIMER                (dark bg #101010)
```
