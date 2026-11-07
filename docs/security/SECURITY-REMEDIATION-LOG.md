# Security Remediation Log
**Project:** Haroon Mughal GFX Portfolio  
**Domain:** https://haroonmughalgfx.online  
**Date:** November 2026  

This log provides an auditable record of all security and code hardening fixes implemented during the migration.

---

## Remediation Entries

### Fix REM-01: Implementation of Comprehensive `.gitignore`
- **Related Finding:** SEC-02
- **Action Taken:** Created `.gitignore` in repository root.
- **Rules Added:**
  - Operating system metadata (`.DS_Store`, `Thumbs.db`, `desktop.ini`)
  - Environment variables and secrets (`.env*`, `*.key`, `*.pem`, `*.cert`)
  - Node modules and temporary scratch folders (`node_modules/`, `scratch/`, `*.log`, `.netlify/`)
- **Verification:** `git status` confirms untracked scratch scripts and local artifacts are no longer staged.

---

### Fix REM-02: Normalization of Storage Keys & Removal of Inherited Identifiers
- **Related Finding:** Identity Sanitization
- **Files Modified:**
  - `index.html`
  - `graphic-designer/index.html`
  - `web-developer/index.html`
  - `vectorization/index.html`
  - `video-editing/index.html`
  - `app-developer/index.html`
  - `ui-ux-designer/index.html`
  - `photographer/index.html`
  - `legal/index.html`
- **Action Taken:**
  - Updated theme storage key from `rishi-mode` to `haroon-mode`, while preserving fallback read `(localStorage.getItem('haroon-mode') || localStorage.getItem('rishi-mode'))` so existing visitors maintain their preferred theme.
  - Updated analytics consent key to `haroon-analytics`.

---

### Fix REM-03: Form Handling Alignment for GitHub Pages Hosting
- **Related Finding:** SEC-03
- **File Modified:** `index.html`
- **Action Taken:**
  - Removed outdated domain check: `const FORM_LIVE = /(^|\.)therishithakor\.com$|\.netlify\.app$/.test(location.hostname);`
  - Set `FORM_LIVE = false;` to seamlessly route contact submissions to the pre-formatted `mailto:designto@haroonmughalgfx.online` client flow.
- **Verification:** Form modal cleanly opens user's email client with recipient `designto@haroonmughalgfx.online` and populated inquiry body.

---

### Fix REM-04: Removal of Orphaned Netlify HUD Development Script
- **Related Finding:** SEC-04
- **Files Modified:**
  - `graphic-designer/index.html`
  - `web-developer/index.html`
  - `vectorization/index.html`
  - `video-editing/index.html`
  - `ui-ux-designer/index.html`
  - `photographer/index.html`
- **Action Taken:** Deleted `<script async src="../.netlify/scripts/hud@variant=public"...></script>` tags across all subpages.
- **Verification:** Elimination of 404 network request errors in browser developer tools.

---

### Fix REM-05: Hardening of `postMessage` Target Origins
- **Related Finding:** SEC-05
- **File Modified:** `index.html`
- **Action Taken:** Replaced open wildcard dispatch with conditional origin validation:
  `((location.origin && location.origin !== 'null') ? location.origin : '*')`.
- **Verification:** Internal iframe communication (door views, ability card modal) continues functioning flawlessly without console warnings.

---

### Fix REM-06: Legal & Privacy Documentation Rewrite
- **Related Finding:** Privacy Compliance / Identity
- **Files Modified:**
  - `legal/index.html`
  - `legal/licenses.txt`
- **Action Taken:**
  - Rewrote `legal/index.html` to reflect Haroon Mughal GFX ownership, the `https://haroonmughalgfx.online` production domain, GitHub Pages hosting context, and official contact `designto@haroonmughalgfx.online`.
  - Replaced inherited font references with active font system (Galano Grotesque + Svara).
  - Clarified portfolio ownership in `legal/licenses.txt` while strictly retaining all open-source author license texts.
