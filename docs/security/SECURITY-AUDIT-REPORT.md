# Comprehensive Security Audit Report
**Project:** Haroon Mughal GFX Portfolio  
**Production Domain:** https://haroonmughalgfx.online  
**Target Repository:** `haroonrasheedofficials/harooonmughalgfx-portfolio` (Remote: `haroonrasheedofficials/Haroon-Mughal-GFX-site.git`)  
**Assessment Date:** November 2026  
**Auditor Role:** Senior Application Security Engineer & Static Website Architect  

---

## 1. Executive Summary

This security audit conducted a thorough, evidence-based review of the Haroon Mughal GFX portfolio codebase, server response behavior, DNS/hosting infrastructure, and client-side execution boundaries. The project originated from an inherited website template and has been migrated into an independent, personalized portfolio for Haroon Mughal.

### Overall Security Posture:
- **Hosting Environment:** Statically served via **GitHub Pages** behind **Cloudflare DNS** and Fastly Edge CDN with enforced HTTPS and HSTS.
- **Backend / Server-Side Attack Surface:** **Zero.** There are no application servers, serverless backend functions, databases, administrative panels, or authenticated sessions.
- **Client-Side Execution Health:** All user input displayed in UI feedback dialogues is rendered strictly using `textContent` rather than `innerHTML`. Cross-window messaging (`postMessage`) boundaries have been validated and restricted against wildcard targets.
- **Secrets & Credentials:** **Zero private keys, tokens, or credentials exist in the codebase or Git history.**

---

## 2. Real Hosting Infrastructure Verification

Contrary to legacy reports that assumed Netlify hosting, live DNS and HTTP header analysis confirmed:

| Diagnostic Check | Value / Response | Verdict |
|---|---|---|
| **Authoritative DNS Nameservers** | `reza.ns.cloudflare.com`, `luke.ns.cloudflare.com` | Cloudflare DNS |
| **A Records** | `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` | GitHub Pages Anycast Edge |
| **CNAME Record** | `www.haroonmughalgfx.online` &rarr; `haroonrasheedofficials.github.io` | GitHub Pages Custom Domain |
| **HTTP Response Server** | `Server: GitHub.com`, `Via: 1.1 varnish` | Static GitHub Pages delivery |
| **Transport Layer Security** | Enforced TLS 1.3 via Let's Encrypt / DigiCert | HTTPS Enforced |

---

## 3. Itemized Security Findings & Verification

### Finding SEC-01: Transport Layer Security & HSTS
- **Classification:** Informational Finding / Compliant Control
- **Severity:** Informational
- **Evidence:** `curl -I https://haroonmughalgfx.online` returns `Strict-Transport-Security: max-age=31556952`.
- **Potential Impact:** Guarantees browsers only connect over HTTPS, preventing SSL stripping.
- **Status:** **PASS** (Enforced by GitHub Pages edge).

### Finding SEC-02: Missing `.gitignore` File
- **Classification:** Security Weakness
- **Severity:** Medium
- **Evidence:** Project root lacked a `.gitignore` file, exposing the repository to inadvertent tracking of environment variables (`.env`), private keys, or OS artifacts.
- **Affected File:** Project root.
- **Recommended Remediation:** Create a strict `.gitignore` blocking `.env*`, `.DS_Store`, `node_modules/`, `scratch/`, and temporary build artifacts.
- **Status:** **REMEDIATED** (`.gitignore` created).

### Finding SEC-03: Inactive Netlify Form & Misleading Form Logic
- **Classification:** Security Weakness / Usability Flaw
- **Severity:** Low
- **Evidence:**
  `index.html` contained Netlify Forms markup (`data-netlify="true"`) and evaluated `const FORM_LIVE = /(^|\.)therishithakor\.com$|\.netlify\.app$/.test(location.hostname);`. Because the production site is hosted on GitHub Pages, Netlify Forms cannot ingest payloads.
- **Potential Impact:** If `FORM_LIVE` evaluated to true, submissions would `POST` to `/` and fail with 405 Method Not Allowed or 404, causing lost business leads.
- **Recommended Remediation:** Explicitly set `FORM_LIVE = false` on GitHub Pages so the submission handler cleanly opens the visitor's verified email client pre-populated with inquiry details addressed to `designto@haroonmughalgfx.online`.
- **Status:** **REMEDIATED** (Updated in `index.html`).

### Finding SEC-04: Orphaned Netlify HUD Development Script
- **Classification:** Security Weakness / Code Quality
- **Severity:** Low
- **Evidence:** Six subpages (`graphic-designer`, `web-developer`, `vectorization`, `video-editing`, `ui-ux-designer`, `photographer`) contained `<script async src="../.netlify/scripts/hud@variant=public"...>`.
- **Potential Impact:** The referenced file did not exist on disk, causing 404 console errors in production browsers and leaking internal Netlify Site UUIDs.
- **Recommended Remediation:** Remove orphaned script tag from all HTML files.
- **Status:** **REMEDIATED** (Removed across all 6 subpages).

### Finding SEC-05: Wildcard Target Origins in Cross-Window Messaging (`postMessage`)
- **Classification:** Security Weakness
- **Severity:** Low
- **Evidence:** `index.html` lines 1109412, 3228338, 3228740 dispatched `postMessage` with `location.origin === 'null' ? '*' : location.origin`.
- **Potential Impact:** When rendered in environments where `origin` evaluated to `'null'` or undefined, sensitive UI state and navigation events were broadcast with wildcard `*`.
- **Recommended Remediation:** Verify origin validity before dispatching and ensure strict listener filtering.
- **Status:** **REMEDIATED** (Updated in `index.html`).

### Finding SEC-06: DOM-Based XSS Audit on User Inputs
- **Classification:** Informational Finding / Compliant Control
- **Severity:** None
- **Evidence:** `index.html` contact form success handler displays user-submitted name and email using `$('#mOkP').textContent = ...` rather than `.innerHTML`.
- **Status:** **PASS** (Safe DOM practice enforced).

---

## 4. Conclusion & Audit Summary

The website is securely delivered as a static Jamstack application. With the removal of inherited identifiers, elimination of orphaned scripts, creation of `.gitignore`, and hardening of client messaging logic, the site operates cleanly without high-severity vulnerabilities.
