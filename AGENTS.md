# AGENTS.md — Vay Thế Chấp Sổ Đỏ Landing Page

## Project Overview
A single-page HTML landing site for a Vietnamese mortgage/loan brokerage service (`vay thế chấp sổ đỏ`). It collects leads via a form and drives phone/Zalo conversions. No build step — plain HTML/CSS/JS.

## Business Objective
Run Google Search/Display Ads for the domain **thechapsodo.online** to generate high-quality mortgage leads. The page must comply with Google Ads policies for financial services and be optimized for conversion rate (CRO) to maximize ad spend ROI.

## File Structure
```
/
├── index.html              # Main landing page (lead form, CTA buttons, modals)
├── privacy-policy.html     # Standalone privacy policy page
└── terms-of-service.html   # Standalone terms of service page
```

## Tech Stack
- Pure HTML5 + inline CSS + vanilla JavaScript
- No frameworks, no build tools
- Responsive design with CSS Grid/Flexbox
- Google Ads conversion tracking (`gtag.js`)
- Backend: Serverless function via DigitalOcean Functions (`API_BASE` in JS)

## Key Conventions
- All styles are inline or in a `<style>` block within `index.html` (no external CSS file)
- Conversion events are tracked via inline `onclick` handlers calling `gtag_report_conversion*` functions
- Form submits via `fetch()` POST to a DigitalOcean Functions endpoint
- Phone/Zalo number hardcoded: `0876.887.555`
- Zalo link: `https://zalo.me/0876887555`

## Deployment
- **Server**: `lev` (SSH as `thanh@lev`)
- **Web root**: `/etc/caddy/ads_thechap/`
- **Web server**: Caddy
- Deploy by SCP: `scp index.html thanh@lev:/etc/caddy/ads_thechap/index.html`

## Conversion Tracking IDs
| Action | Function | `send_to` |
|--------|----------|-----------|
| Phone call | `gtag_report_conversion()` | `AW-18113735600/4ShLCLn3y6EcELDXpr1D` |
| Form submit | `gtag_report_conversion_form()` | `AW-18113735600/ycz2CLWw9qEcELDXpr1D` |
| Zalo click | `gtag_report_conversion_zalo()` | `AW-18113735600/uakYCLD85KMcELDXpr1D` |

## Google Ads Policy Compliance (Financial Services)
To ensure the site runs smoothly on Google Ads without disapprovals or account suspension, the page **must** satisfy the following:

### 1. Transparency & Disclosure
- Clearly state that this is a **brokerage/tư vấn service**, not a bank. Do not imply direct lending.
- Display the business model prominently: *"Chúng tôi là đơn vị TƯ VẤN & KẾT NỐI khách hàng với ngân hàng đối tác."*
- Include a visible **Privacy Policy** and **Terms of Service** link in the footer.

### 2. No Misleading Claims
- Avoid absolute guarantees: "vay chắc chắn", "100% duyệt", "không cần hồ sơ".
- Use qualifying language: *"hỗ trợ nợ xấu"*, *"duyệt hồ sơ nhanh"*, *"lãi suất từ X%"*.
- Interest rates must reflect realistic market ranges. Do not advertise rates lower than what banks actually offer.

### 3. Prohibited Content
- No payday loan-style language (e.g., "vay nóng", "vay tiền nhanh trong ngày", "vay không cần thế chấp").
- No targeting of vulnerable groups with predatory language.
- No hidden fees or terms. Any potential fees must be disclosed.

### 4. Data Collection
- Form fields must be relevant and minimal (Name, Phone, Location, Loan amount, Debt status, Message).
- Must include a clear privacy/data usage notice near the form or in the footer.
- Do not request sensitive financial information (bank passwords, OTPs, ID card photos) on the landing page.

### 5. Landing Page Experience
- Page must load fast (under 3 seconds).
- Must be mobile-friendly and responsive.
- No intrusive interstitials or pop-ups that block the main content.
- Contact information must be accurate and match the business.

### 6. URL & Domain
- The advertised domain is **thechapsodo.online**. Ensure all links in ads point to this domain.
- No redirects to unrelated domains.

## Conversion Rate Optimization (CRO) Guidelines
To maximize lead generation and ad budget efficiency:

### 1. Above-the-Fold (Hero Section)
- **Headline**: Must immediately communicate value proposition (e.g., *"Vay Thế Chấp Sổ Đỏ — Lãi Suất Từ 0.8%/Tháng"*).
- **Primary CTA**: High-contrast button above the fold. "ĐĂNG KÝ VAY NGAY" or "GỌI NGAY".
- **Trust signals**: Hotline/Zalo number visible, trust badges if available.
- **Form placement**: Consider embedding a short form directly in the hero section for higher conversion.

### 2. Form Optimization
- **Reduce friction**: Keep form fields to the absolute minimum (Name, Phone, Loan amount are highest priority).
- **Progressive profiling**: Use follow-up calls to collect additional details.
- **Clear submit button**: Large, contrasting color, action-oriented text ("GỬI ĐĂNG KÝ — NHẬN TƯ VẤN NGAY").
- **Success state**: Show immediate confirmation message and prompt next action (call/Zalo).

### 3. Multiple Conversion Paths
- **Phone call**: Click-to-call button on mobile. Floating CTA for calls.
- **Zalo chat**: Floating Zalo button. Many Vietnamese users prefer Zalo over forms.
- **Form submit**: Primary lead capture method for tracking.
- All conversion actions must fire the correct `gtag_report_conversion*` event for accurate attribution.

### 4. Social Proof & Trust
- Add testimonials (text or video) if available.
- Show partner bank logos.
- Display stats: *"Đã hỗ trợ X khách hàng"*, *"Giải ngân X tỷ đồng"* (only if verifiable).
- Include media mentions or certifications if any.

### 5. Urgency & Scarcity (Use Ethically)
- Limited-time rate offers (e.g., *"Lãi suất ưu đãi đến hết tháng"*).
- Urgency should not be false or misleading.

### 6. Page Speed & UX
- Optimize images (compress, use WebP where possible).
- Minimize render-blocking resources.
- Ensure fast mobile experience — majority of traffic will be mobile.
- Test on actual devices, not just browser resize.

### 7. A/B Testing Priorities
- Headline variations (rate-focused vs. speed-focused vs. support-focused).
- CTA button text and color.
- Form placement (inline hero vs. dedicated section vs. sticky bar).
- Phone-first vs. Form-first vs. Zalo-first layout.

## Notes for Agents
- Keep the inline style structure; do not split into external CSS unless explicitly requested.
- When updating conversion tags, ensure all 3 functions remain distinct.
- The form uses client-side validation; backend validation is minimal.
- Do not commit or push to Git unless explicitly asked.
- Any changes to interest rates, terms, or claims must be checked against the Google Ads Policy Compliance section above.
- When modifying CTA buttons, ensure the `onclick` tracking events remain intact.
