# Website Color System Migration Report — Brand Palette

**Project:** Rishi Thakor Portfolio & Subpages  
**Role:** Senior UI/UX Designer, Creative Director & Frontend Design Systems Engineer  
**Status:** Completed & Verified  

---

## 1. Executive Summary

A comprehensive theme migration was executed across the entire existing website to implement the official five-color brand palette. The architecture transitioned from fragmented, warm-grey legacy tokens (`#1A1818`, `#E8E4E0`, `#6B5C5C`, etc.) to a centralized, scalable CSS design token system rooted in the source-of-truth brand palette. 

No page layouts, responsive breakpoints, typography families, copywriting, images, videos, or animations were modified. The structural and interactive integrity of the site remains 100% intact while adopting a dark editorial identity with warm minimalistic accents.

---

## 2. Official Brand Palette & Token Mapping

| Brand Color Name | HEX Code | Design System Token | Primary Intended Role |
| :--- | :--- | :--- | :--- |
| **Sunlit Clay** | `#F8B55F` | `--color-brand-accent`<br>`--color-focus` | Primary brand accent, active state markers, CTA highlights, badges, focus rings, key headings |
| **Onyx** | `#0B0D10` | `--color-background-primary`<br>`--color-text-dark` | Main dark page background, high-contrast dark text on light surfaces |
| **Shadow Grey** | `#181C24` | `--color-background-secondary` | Secondary dark surfaces, cards, navigation surfaces, panels, containers |
| **Bright Snow** | `#FAF8F5` | `--color-surface-light`<br>`--color-text-primary` | Primary light text on dark backgrounds, clean light surfaces |
| **Soft Linen** | `#F0ECE4` | `--color-surface-warm`<br>`--color-text-secondary` | Warm secondary surfaces, subtle contrast, light page backgrounds |

### Centralized Token System

```css
:root {
  --color-brand-accent: #F8B55F;
  --color-background-primary: #0B0D10;
  --color-background-secondary: #181C24;
  --color-surface-light: #FAF8F5;
  --color-surface-warm: #F0ECE4;

  --color-text-primary: #FAF8F5;
  --color-text-secondary: #F0ECE4;
  --color-text-dark: #0B0D10;

  --color-border-dark: rgba(250, 248, 245, 0.12);
  --color-border-light: rgba(11, 13, 16, 0.12);

  --color-focus: #F8B55F;
}
```

---

## 3. Files Modified

| File Path | Description | Changes Applied |
| :--- | :--- | :--- |
| `index.html` | Primary portfolio homepage | Centralized `:root` & `[data-mode="dark"]` tokens, meta theme-color, loader pills & progress bar, hero gradients, modal request dialog, timeline indicator, door frame atmosphere, site footer, back-to-top button, cookie consent banner. |
| `app-developer/index.html` | iOS App Development showcase | Implemented brand token system, updated phone card frames, floating back navigation, footer, back-to-top button, skeleton loading shimmer, cookie consent banner. |
| `graphic-designer/index.html` | Graphic Design showcase | Implemented brand token system, updated world sections (static & dynamic WORLDS JS array), peg board, footer, back-to-top button, skeleton loader, cookie consent banner. |
| `ui-ux-designer/index.html` | UI/UX Design showcase | Implemented brand token system, monitor frames, floating back navigation, footer, back-to-top button, skeleton loading shimmer, cookie consent banner. |
| `web-developer/index.html` | Web Development showcase | Implemented brand token system, monitor frames, floating back navigation, footer, back-to-top button, skeleton loading shimmer, cookie consent banner. |
| `photographer/index.html` | Photography canvas & gallery | Implemented brand token system, canvas clear color (`#0B0D10`), floating chips, back-to-top button, skeleton loading shimmer, cookie consent banner. |
| `legal/index.html` | Privacy & credits page | Implemented brand token system, layout cards, table border hairlines, focus states, cookie consent banner. |

---

## 4. Previous Colors Replaced

| Legacy Color | Usage in Previous Theme | Replacement in New Design System |
| :--- | :--- | :--- |
| `#1A1818` | Main dark background & dark text | `--color-background-primary` (`#0B0D10`) / `--color-background-secondary` (`#181C24`) / `--color-text-dark` (`#0B0D10`) |
| `#E8E4E0` | Main light background & light text | `--color-surface-warm` (`#F0ECE4`) / `--color-text-primary` (`#FAF8F5`) |
| `#6B5C5C` / `#6B4F4F` | Old muddy purple/brown accent | `--color-brand-accent` (`#F8B55F`) |
| `#C4B0B0` / `#D9C6C6` | Old secondary accent & focus outlines | `--color-brand-accent` (`#F8B55F`) & `--color-focus` (`#F8B55F`) |
| `#221F1F` / `#232020` / `#252121` | Inconsistent dark surfaces | `--color-background-secondary` (`#181C24`) |
| `#0F0E0E` / `#050505` | Inconsistent dark mode backgrounds | `--color-background-primary` (`#0B0D10`) |
| `#F0ECE9` / `#F3F0EC` / `#DED8D4` | Inconsistent light panel surfaces | `--color-surface-light` (`#FAF8F5`) / `--color-surface-warm` (`#F0ECE4`) |
| `#A4552C` | Orange sub-navigation active color | `--color-brand-accent` (`#F8B55F`) |
| `rgba(232,228,224,...)` | Light mode text RGB triplet | `rgba(250,248,245,...)` (Derived from Bright Snow) |
| `rgba(26,24,24,...)` | Dark mode text RGB triplet | `rgba(11,13,16,...)` (Derived from Onyx) |

---

## 5. Components Updated

1. **Header & Navigation:**
   - Stuck header background and border hairlines mapped to tokens.
   - Time badge, clock separators, and chip buttons styled with Soft Linen, Shadow Grey, and Sunlit Clay hover states.
   - Fullscreen navigation menu overlay (`.navm`) adopting Onyx and Sunlit Clay interactive hovers.
   - Subpage floating back pills (`.backd`) adopting Shadow Grey with Bright Snow text and focus rings.

2. **Hero Section & Intros:**
   - Hero radial gradient smoothly fading between Bright Snow (`#FAF8F5`) and Soft Linen (`#F0ECE4`).
   - Dark mode hero background transitioning between Shadow Grey (`#181C24`) and Onyx (`#0B0D10`).
   - Ability card tag and holographic modal viewer (`.holo`, `.cl`) styled with Onyx, Shadow Grey, and Sunlit Clay progress indicator.

3. **Buttons & Interactive CTAs:**
   - Primary buttons (`.pill--dark`, `.sf__btn`, `.ck button[data-ck="yes"]`) powered by Sunlit Clay with high-contrast Onyx text.
   - Outline and ghost buttons using semi-transparent hairlines with subtle hover fills.
   - Back-to-top floating button (`.totop`) with circular SVG progress ring and Sunlit Clay focus indicator.

4. **Cards & Portfolios:**
   - App developer iPhone frames and monitor wrappers preserving authentic hardware colors while cards utilize Shadow Grey / Bright Snow surfaces.
   - Graphic design "world" editorial panels mapped to the new palette.
   - UI/UX and Web Developer stacked project cards utilizing Shadow Grey surfaces in dark mode and Bright Snow / Soft Linen in light mode.

5. **Timeline & Interactive Story:**
   - Active status indicators, timeline dots, and chapter labels updated to Sunlit Clay.
   - Ambient background lighting balanced with minimal opacity to prevent color clash.

6. **Doors Interactive Installation:**
   - Wall, baseboard, casing, and room variables harmonized with the new tokens.
   - Brass plate and turn handle textures preserved in their realistic material appearance while the lighting sill and spill glow adapt to Sunlit Clay warm radiance.

7. **Forms & Modals:**
   - Project inquiry modal (`.modal__panel`) utilizing Soft Linen in light mode and Shadow Grey in dark mode.
   - Form inputs with subtle border hairlines, focusing cleanly with Sunlit Clay rings.
   - Submission success badge highlighted in Sunlit Clay with Onyx iconography.

8. **Cookie Consent Banner (`.ck`):**
   - Harmonized identically across all 7 pages with Shadow Grey container, Bright Snow text, and Sunlit Clay "Allow" button.

---

## 6. Remaining Legacy Colors & Technical Justification

Zero instances of the old UI theme colors (`#1A1818`, `#E8E4E0`, `#6B5C5C`, `#6B4F4F`, `#C4B0B0`, `#D9C6C6`) remain in the codebase.

The only colors outside the exact 5 brand values that intentionally remain are:
- **Realistic Physical Materials (Skeuomorphic Elements):**
  - Brass doorplate & lever handle gradients (brass reflections: `#c9a866`, `#a98747`, `#efdfb2`, etc.).
  - Physics pull-cord canvas knot & wood tassel (wood gradient: `#5b4a2c`, `#7c4828`, `#24150c`, etc.).
  - Hardware device frames (Mac monitor aluminium and iPhone stainless steel bezel gradients).
- **Physical Flip Calendar Paper & Steel Ringlets:**
  - Real paper shadows and metallic spiral ringlets (`#a9a9a9`, `#ededed`, `#6f6f6f`).
- **Media Assets & Video Elements:**
  - Embedded client video poster backgrounds and project thumbnail media.
- **Pulse Availability Status:**
  - The live availability dot (`#8FBF7A`) in the footer indicating active freelance availability.

All these elements are contextual photographic/physical rendering details rather than site theme colors, preserving asset integrity per section 6 & 8 of the requirements.

---

## 7. Accessibility and Contrast Verification

Contrast calculations evaluated in accordance with WCAG 2.1 standards:

| Element Pair | Colors Evaluated | Contrast Ratio | WCAG AA Requirement | Result |
| :--- | :--- | :---: | :---: | :---: |
| Primary text on Dark Background | Bright Snow (`#FAF8F5`) on Onyx (`#0B0D10`) | **18.36:1** | ≥ 4.5:1 | **PASSED (AAA)** |
| Secondary text on Dark Background | Soft Linen (`#F0ECE4`) on Onyx (`#0B0D10`) | **16.51:1** | ≥ 4.5:1 | **PASSED (AAA)** |
| Primary text on Card Surfaces | Bright Snow (`#FAF8F5`) on Shadow Grey (`#181C24`) | **16.10:1** | ≥ 4.5:1 | **PASSED (AAA)** |
| Secondary text on Card Surfaces | Soft Linen (`#F0ECE4`) on Shadow Grey (`#181C24`) | **14.49:1** | ≥ 4.5:1 | **PASSED (AAA)** |
| Dark text on Warm Light Surface | Onyx (`#0B0D10`) on Soft Linen (`#F0ECE4`) | **16.51:1** | ≥ 4.5:1 | **PASSED (AAA)** |
| Dark text on Clean Light Surface | Onyx (`#0B0D10`) on Bright Snow (`#FAF8F5`) | **18.36:1** | ≥ 4.5:1 | **PASSED (AAA)** |
| **Primary CTA Button Text** | Onyx (`#0B0D10`) on Sunlit Clay (`#F8B55F`) | **10.90:1** | ≥ 4.5:1 | **PASSED (AAA)** |
| Accent Indicator on Dark Foundation | Sunlit Clay (`#F8B55F`) on Onyx (`#0B0D10`) | **10.90:1** | ≥ 3.0:1 | **PASSED (AAA)** |
| Accent Indicator on Card Surface | Sunlit Clay (`#F8B55F`) on Shadow Grey (`#181C24`) | **9.56:1** | ≥ 3.0:1 | **PASSED (AAA)** |

- **Keyboard Navigation & Focus:** Clear 2px outline using `--color-focus` (`#F8B55F`) with 2px–3px offset across all interactive links, buttons, and form inputs.
- **Touch & Mobile Targets:** Preserved 44px minimum touch targets across all mobile buttons, chips, and navigational triggers.

---

## 8. Verification & Validation Results

1. **Syntax & Parsing:** Verified through standard HTML parser across all 7 HTML documents; zero parse errors detected.
2. **Git Diff Audit:** All 7 modified files inspected; changes strictly isolated to color migration, CSS token propagation, and contrast refinement.
3. **Responsive Breakpoints:** No changes made to layout containers, flexbox/grid dimensions, font sizes, or viewport rules.
4. **Theme Toggling:** Light and dark transitions function seamlessly with View Transitions and preserve user preference in `localStorage`.

---
*Report generated for Website Color System Migration.*

