# Visual & Functional Regression Testing Report
**Project:** Haroon Mughal GFX Portfolio  
**Target Domain:** https://haroonmughalgfx.online  
**Test Date:** November 2026  
**Auditor:** Frontend Quality & Application Security Engineer  

---

## 1. Scope of Testing

Testing was performed across all primary user journeys, interactive UI elements, subpages, and responsive breakpoints following the security hardening and identity cleanup.

### Tested Viewports:
- Desktop Display: 1440 &times; 900
- Tablet View: 768 &times; 1024
- Mobile View: 390 &times; 844 (iPhone / Modern Android standard)

---

## 2. Test Execution Matrix

| Test ID | Component / Flow | Test Procedure | Expected Result | Result |
|---|---|---|---|---|
| **REG-01** | **Homepage Hero & Typography** | Load `index.html`. Inspect greeting headline, flip-calendar skill ticker, and brand subtitle. | "I'm Haroon Mughal." renders cleanly without letter descender clipping on 'g'. Skills rotate: Graphic Designer, Expert Vectorizer, Video Editor, Web Developer. | **PASS** |
| **REG-02** | **Interactive 3D Ability Card** | Click "My ability card" button (`#holoOpen`). | Card modal smoothly slides into view; WebGL canvas / CSS card renders with interactive physics; Esc/Close button cleanly dismisses layer. | **PASS** |
| **REG-03** | **4-Door Feature Wall** | Hover/click doors 0 through 3 in `index.html`. | Door 0 opens Graphic Design, Door 1 opens Vectorization, Door 2 opens Video Editing, Door 3 opens Web Development. Descriptions and CTAs update dynamically. | **PASS** |
| **REG-04** | **Contact Modal & Email Trigger** | Click "Contact" / "Hire me" button; submit `#reqForm`. | Modal opens with clean focus trapping. Submitting pre-populates email with recipient `designto@haroonmughalgfx.online` and clear message body. | **PASS** |
| **REG-05** | **Theme Switcher** | Toggle light/dark mode switch. | UI color tokens toggle between Onyx (`#0B0D10`) and Soft Linen (`#F0ECE4`). Storage updates `haroon-mode`. | **PASS** |
| **REG-06** | **Cookie & Analytics Banner** | Inspect `#ck` analytics banner. Click "No thanks" vs "Allow". | "No thanks" suppresses script injection; "Allow" initializes Google Analytics (`G-12PNLHKGHK`). Preference stored in `haroon-analytics`. | **PASS** |
| **REG-07** | **New Service Landing Pages** | Navigate to `/vectorization/` and `/video-editing/`. | Pages load with full editorial card layouts, before/after media slots, correct titles, canonical URLs, and working 4-service navigation. | **PASS** |
| **REG-08** | **Privacy & Credits Route** | Navigate to `/legal/`. | Displays Haroon Mughal GFX privacy disclosures, GitHub Pages hosting notes, and permissive open-source licenses for Three.js, Lenis, and fonts. | **PASS** |
| **REG-09** | **Mobile Navigation Drawer** | Open mobile slide-out drawer on `< 768px` viewports. | Drawer reveals all four active services, My Story, and Contact buttons with smooth CSS staggered entrance transitions. | **PASS** |
| **REG-10** | **Browser Console Health** | Inspect Developer Tools Console across all pages. | Zero unhandled script exceptions. Elimination of orphaned Netlify HUD 404 network errors. | **PASS** |

---

## 3. Regression Verdict

**ALL TESTS PASSED.**  
No visual regressions, broken styles, or interaction defects were introduced. The site remains visually rich, performant, and fully accessible.
