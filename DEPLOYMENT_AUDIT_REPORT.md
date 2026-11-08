# DEPLOYMENT AUDIT REPORT: HAROON MUGHAL GFX PORTFOLIO

**Date:** November 8, 2026  
**Investigator:** Antigravity Senior Frontend & DevOps Engineer  
**Status:** Audit Completed — Root Causes Identified & Fix Strategy Prepared  

---

## EXECUTIVE SUMMARY

Your portfolio website operates in **VS Code Live Server** using the local files in this workspace. However, the production website (`https://haroonmughalgfx.online/`) is experiencing severe errors:
1. `GET /vendor/lenis.min.mis 404`
2. `GET /undefined?embed 404`
3. `Uncaught TypeError: Cannot read properties of null (reading 'getBoundingClientRect')`
4. Console reports `window.SITE`, `gsap`, `ScrollTrigger`, and `Lenis` as undefined.

Our deep audit revealed **two primary root causes**:
1. **Hosting & Repository Misalignment:** The live production domain is **NOT** serving from Hostinger. DNS queries and HTTP response headers prove that `haroonmughalgfx.online` resolves to **GitHub Pages IP addresses** (`185.199.108.153` - `185.199.111.153`) serving your active local repository (`haroonrasheedofficials/Haroon-Mughal-GFX-site`) branch `master`. Meanwhile, you believed the site was deploying from Hostinger via `haroonrasheedofficials/harooonmughalgfx-portfolio` branch `main`.
2. **Local Code Bugs in the Master Codebase:** 
   - A stray typo in `index.html` line 2290: `setTimeout(() => { warm(4); ... }, 600)`. Because `ROUTES` has length 4 (indices 0 to 3), `ROUTES[4]` is `undefined`, generating `/undefined?embed 404`.
   - Missing Lenis fallback/bundle: `index.html` imports Lenis from `./vendor/lenis.min.mjs` which does not exist locally or in the repo.
   - Guard missing in `vectorization/index.html` and `video-editing/index.html`: `checkHidden()` queries `.mon__screen`, which does not exist on static custom preview cards, causing `null.getBoundingClientRect()`.
   - The template used in the other repository (`harooonmughalgfx-portfolio`) had a completely different structure using `content.js` and CDN GSAP/ScrollTrigger, explaining why error messages mentioning `window.SITE` were observed when looking at other branches/repos.

---

## 1. ARCHITECTURE & REPOSITORY INVENTORY

### A. Local Git Workspace
- **Branch:** `master`
- **Remote Origin:** `https://github.com/haroonrasheedofficials/Haroon-Mughal-GFX-site.git`
- **Head Commit:** `6875506 fix: integrate consent-based Google Analytics through GTM`
- **Architecture:** Self-contained rich interactive vanilla ES Module architecture (`index.html` ~3.27MB with embedded SVGs, base64 data, custom spring physics, door transitions, iframe room embeds).
- **Service Directories Present:**
  - `graphic-designer/`
  - `vectorization/`
  - `video-editing/`
  - `web-developer/`
  - `photographer/`
  - `app-developer/`
  - `ui-ux-designer/`
  - `legal/`

### B. Remote GitHub Repositories Compared

| Metric / Item | Active Local & Deployed Repo (`Haroon-Mughal-GFX-site`) | Target Repo Referenced in Prompt (`harooonmughalgfx-portfolio`) |
| :--- | :--- | :--- |
| **Default Branch** | `master` | `main` |
| **CNAME file** | Present (`haroonmughalgfx.online`) | **Deleted** on Nov 7, 2026 (`commit da8a9c8`) |
| **Architecture** | Single-bundle interactive portfolio with doors and iframes | Separate architecture reading `content.js`, using CDN GSAP + ScrollTrigger |
| **index.html size**| ~3,273,345 bytes (exact match with live site) | ~187,984 bytes |
| **Hosting Target** | Currently live on GitHub Pages under custom domain | None (CNAME deleted) |

---

## 2. PRODUCTION SOURCE COMPARISON & CONFIRMED DISCREPANCIES

When inspecting `curl.exe -I https://haroonmughalgfx.online/`:
```http
HTTP/1.1 200 OK
Server: GitHub.com
Content-Length: 3273345
Last-Modified: Sat, 07 Nov 2026 04:45:08 GMT
ETag: "6aeeacd4-31f281"
```
The live server response length is **3,273,345 bytes**, which matches `Haroon-Mughal-GFX-site/index.html` down to the exact byte!

### Root Cause Analysis of Specific Observed Errors:

1. **`GET /undefined?embed 404`**
   - **Root Cause:** In `index.html` line 2290:
     ```javascript
     const near = new IntersectionObserver(es => {
       if (es.some(e => e.isIntersecting)){
         near.disconnect();
         setTimeout(() => { warm(4); setTimeout(() => [0, 1, 2, 3].forEach(warm), 1500); }, 600);
       }
     });
     ```
     `ROUTES` is defined as `['graphic-designer/', 'vectorization/', 'video-editing/', 'web-developer/']`.
     Index `4` does not exist! When `warm(4)` calls `loadRoom(4)`, `ROUTES[4]` evaluates to `undefined`, requesting `f.src = undefined + '?embed'`.
   - **Fix:** Remove `warm(4)` and validate `if (!ROUTES[i]) return;` inside `loadRoom(i)`.

2. **`Cannot read properties of null (reading 'getBoundingClientRect')`**
   - **Root Cause:** In `vectorization/index.html` and `video-editing/index.html`:
     ```javascript
     const screens = cards.map(c => ({
       c,
       scr: c.querySelector('.mon__screen'),
       hidden: true,
       s: shots.find(x => x.c === c),
       v: c.querySelector('video')
     }));
     ...
     function checkHidden(){
       screens.forEach((o, i) => {
         const r = o.scr.getBoundingClientRect(); // CRASHES when o.scr is null!
     ```
     The cards in `vectorization` and `video-editing` were customized to have custom deliverables stages without `.mon__screen`. When `checkHidden()` executes on page load or scroll, `o.scr` is `null`.
   - **Fix:** Guard with `if (!o || !o.scr) return;`.

3. **`GET /vendor/lenis.min.mis 404` and Lenis undefined**
   - **Root Cause:** In `index.html`:
     ```html
     <script type="importmap">
     { "imports": { "lenis": "./vendor/lenis.min.mjs" } }
     </script>
     ```
     Neither `./vendor/lenis.min.mjs` nor `./vendor/` exists locally or in the repo. (A typo `.mis` also appeared in earlier tests).
   - **Fix:** Use official verified CDN in importmap or provide graceful fallback so native scrolling works seamlessly if Lenis fails to load.

4. **`window.SITE`, `gsap`, and `ScrollTrigger` undefined**
   - **Root Cause:** These are **not part of the `Haroon-Mughal-GFX-site` codebase**. They belonged to the alternate template in `harooonmughalgfx-portfolio`. If you attempted to load `content.js` on `Haroon-Mughal-GFX-site`, it returned 404 because `content.js` is not used by your current rich interactive website.

5. **`GET /favicon.ico 404` and `favicon.svg`**
   - **Root Cause:** Root has `Favicon.png` (capital F) and `apple-touch-icon.ico`. Root had no `favicon.ico` or `favicon.svg`. Standard browsers request `/favicon.ico` automatically by default when opening the site root.

---

## 3. HOSTINGER VS GITHUB PAGES DEPLOYMENT STATUS

### Where is the website currently hosted?
DNS lookup for `haroonmughalgfx.online`:
```
Addresses:  185.199.111.153
            185.199.108.153
            185.199.110.153
            185.199.109.153
```
These are the official Anycast IP addresses of **GitHub Pages**.
The domain `haroonmughalgfx.online` is pointing to GitHub Pages, configured via the `CNAME` file in `Haroon-Mughal-GFX-site` (`master` branch).

### What about Hostinger?
If you intended to host the site on **Hostinger Web Hosting**:
- Your domain's DNS `A` records are currently pointing to GitHub, **bypassing Hostinger completely**.
- To deploy to Hostinger, the files would need to be uploaded to Hostinger's `public_html` directory, and your domain DNS records would need to point to Hostinger's Server IP.
- Alternatively, if you prefer GitHub Pages (free, automated, SSL included), your current repository `Haroon-Mughal-GFX-site` is already linked, deployed, and live!

---

## 4. ACTIONABLE REPAIR PLAN

To make production match the flawless VS Code Live Server experience without breaking any visuals:

### Step 1: Fix Local Code Bugs
1. **Fix `warm(4)` bug in `index.html`**:
   - Guard `loadRoom(i)`: `if (!ROUTES[i]) return;`.
   - Remove erroneous `warm(4)` call.
2. **Fix `getBoundingClientRect` null checks**:
   - In `vectorization/index.html`, `video-editing/index.html`, `app-developer/index.html`, `ui-ux-designer/index.html`, `web-developer/index.html`:
   - In `checkHidden()`, add `if (!o || !o.scr) return;`.
   - Guard `span` and `next` card accesses: `if (next) ...`.
3. **Fix Lenis Import & Fallbacks**:
   - Update importmap to point to a reliable CDN:
     `{ "imports": { "lenis": "https://cdn.jsdelivr.net/npm/lenis@1.1.14/dist/lenis.min.mjs" } }`
   - Ensure the `try / catch` around dynamic import gracefully falls back to native scrolling without throwing unhandled exceptions.
4. **Fix Favicon**:
   - Ensure `<link rel="icon">` correctly points to the existing `Favicon.png` or provide a standard fallback.

### Step 2: Deployment Alignment
Decide your preferred hosting target:
- **Option A (GitHub Pages — Already Connected):** Commit the targeted code fixes to `master` and push to `origin` (`haroonrasheedofficials/Haroon-Mughal-GFX-site`). GitHub Pages will build and deploy in ~60 seconds.
- **Option B (Hostinger):** Export the local directory files and upload directly into Hostinger's `public_html` file manager or Git deployment, and point the domain's DNS `A` record to your Hostinger server IP.
