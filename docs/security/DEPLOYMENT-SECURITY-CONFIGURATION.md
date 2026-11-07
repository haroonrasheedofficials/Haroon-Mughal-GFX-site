# Deployment & Infrastructure Security Configuration
**Project:** Haroon Mughal GFX Portfolio  
**Target Domain:** https://haroonmughalgfx.online  
**Hosting Provider:** GitHub Pages (Custom Domain)  
**DNS & Edge Proxy:** Cloudflare DNS  
**Date:** November 2026  

---

## 1. Hosting Architecture Overview

The portfolio is deployed directly from the `master` branch of the GitHub repository `haroonrasheedofficials/Haroon-Mughal-GFX-site` using GitHub Pages.

```
[ User Browser ]
       |
       v  (HTTPS / TLS 1.3)
[ Cloudflare Anycast DNS (reza.ns.cloudflare.com / luke.ns.cloudflare.com) ]
       |
       v  (A Records: 185.199.108.153 - 185.199.111.153)
[ GitHub Pages Edge CDN / Fastly Reverse Proxy ]
       |
       v  (Static File Ingestion)
[ GitHub Repository master branch (CNAME: haroonmughalgfx.online) ]
```

---

## 2. Infrastructure Configuration Assessment

### A. Custom Domain & CNAME Verification
- **Repository Root CNAME:** `CNAME` file in repository root contains:
  ```
  haroonmughalgfx.online
  ```
- **DNS Records:**
  - Apex Domain (`haroonmughalgfx.online`): Resolves to the four GitHub Pages Anycast IP addresses (`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`).
  - Subdomain (`www.haroonmughalgfx.online`): CNAME points to `haroonrasheedofficials.github.io`.

### B. Supported vs. Unsupported Controls on GitHub Pages

| Security Control | GitHub Pages Native Support | Recommended Implementation Strategy |
|---|---|---|
| **HTTPS Enforcement** | Native / Supported | Enabled in GitHub repository Settings &rarr; Pages &rarr; Enforce HTTPS. |
| **Strict-Transport-Security (HSTS)** | Native / Supported | Enabled by default (`Strict-Transport-Security: max-age=31556952`). |
| **Server-Side Custom HTTP Headers (e.g. `_headers`, `netlify.toml`)** | **Not Supported** | Custom edge headers cannot be injected via static repo files on GitHub Pages. |
| **Edge Security Headers via Cloudflare** | Supported (via Cloudflare Dashboard) | Cloudflare Transform Rules or Cloudflare Workers can inject `Content-Security-Policy` and `X-Frame-Options` at the edge. |
| **HTML `<meta http-equiv>` Security Directives** | Supported (Client-side) | Added directly in HTML documents where supported by browsers. |

---

## 3. Recommended Edge Configuration via Cloudflare

Because the domain's authoritative nameservers reside on Cloudflare, edge security headers can be enforced by adding a **Response Header Modification Rule** in the Cloudflare dashboard:

```http
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

### Content Security Policy (CSP) Policy Draft:
```http
Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline' https://www.googletagmanager.com; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self' data:; connect-src 'self' https://www.google-analytics.com https://*.google-analytics.com; frame-src 'self'; object-src 'none';
```
*(Note: Because the homepage dynamically generates three.js textures, loads data URIs, and executes inline animation loops, `'unsafe-inline'` and `data:` are required).*
