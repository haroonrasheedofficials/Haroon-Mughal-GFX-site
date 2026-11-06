# Service Media Production & Asset Specification Checklist
**Brand:** Haroon Mughal GFX  
**Domain:** https://haroonmughalgfx.online  
**Date:** March 2025  

This document specifies the exact image, video, and vector media assets required to replace the placeholder/pending slots across the four active service pages of the Haroon Mughal GFX portfolio.

---

## 1. Vectorization Service Media (`vectorization/index.html`)

| Asset Identifier | Slot Description | Recommended Format | Dimensions / Aspect Ratio | Purpose & Content Guidance | Status |
|---|---|---|---|---|---|
| `vectorization-compare-1.webp` | Before & After Comparison (Card 1) | WebP / PNG | 1200 &times; 800 (3:2) | Side-by-side or split slider visual showing a blurry, pixelated low-res JPEG/PNG logo on the left vs a razor-sharp, mathematically pure vector wireframe/outline on the right. | **Pending Upload** |
| `vector-production-spec.webp` | Production Spec Sheet Mockup (Card 2) | WebP | 1200 &times; 800 (3:2) | Clean technical layout demonstrating cut paths, color separation layers, and Pantone/CMYK callouts ready for CNC, vinyl, embroidery, or screen printing. | **Pending Upload** |
| `vector-package-overview.webp` | Master Deliverable Package Preview (Card 3) | WebP | 1200 &times; 800 (3:2) | High-end editorial mockup showing organized client deliverables: `.AI`, `.EPS`, `.SVG`, `.PDF` folder structure with full-color, white knock-out, and solid black logo variations. | **Pending Upload** |

---

## 2. Video Editing Service Media (`video-editing/index.html`)

| Asset Identifier | Slot Description | Recommended Format | Dimensions / Aspect Ratio | Purpose & Content Guidance | Status |
|---|---|---|---|---|---|
| `reel-showcase-1.mp4` | Short-Form Vertical Reel | MP4 (H.264 / AAC) | 1080 &times; 1920 (9:16 vertical) | Fast-paced, high-retention short-form video edit (15–30 sec) with dynamic kinetic typography captions, zooms, sound effects, and sound design. Max file size: < 8MB. | **Pending Upload** |
| `reel-showcase-1.webp` | Video Poster for Card 1 | WebP | 1080 &times; 1920 (9:16 vertical) | Static poster fallback frame for `reel-showcase-1.mp4` when video is paused or loading. | **Pending Upload** |
| `youtube-edit-1.mp4` | Long-Form Narrative / YouTube Video | MP4 (H.264 / AAC) | 1920 &times; 1080 (16:9 widescreen) | Horizontal edit reel showcasing documentary/talking-head narrative pacing, chapter markers, motion lower thirds, and B-roll transitions. | **Pending Upload** |
| `youtube-edit-1.webp` | Video Poster for Card 2 | WebP | 1920 &times; 1080 (16:9 widescreen) | Crisp 16:9 thumbnail / poster frame for long-form video preview. | **Pending Upload** |
| `color-grade-compare.webp` | Color Grading Before/After (Card 3) | WebP | 1200 &times; 800 (3:2) | Split screen displaying flat, washed-out Log/RAW camera profile vs rich, balanced cinematic color grade with natural skin tones and deep contrast. | **Pending Upload** |

---

## 3. Graphic Design Service Media (`graphic-designer/index.html`)

| Asset Identifier | Slot Description | Recommended Format | Dimensions / Aspect Ratio | Purpose & Content Guidance | Status |
|---|---|---|---|---|---|
| `brand-identity-deck-1.webp` | Brand Identity Showcase | WebP | 1440 &times; 960 (3:2) | Comprehensive brand identity showcase: typography scales, color palettes, stationery mockups, and logo guidelines. | **Pending Direct Replacement** |
| `social-creative-suite.webp` | High-Impact Social Grid | WebP | 1200 &times; 1200 (1:1) | Multi-tile cohesive Instagram / LinkedIn carousel design demonstrating brand continuity across multiple feeds. | **Pending Direct Replacement** |
| `packaging-print-mockup.webp` | Packaging & Collateral | WebP | 1400 &times; 900 (~16:10) | Physical product packaging, merchandise, or print collateral with realistic shadows and textures. | **Pending Direct Replacement** |

*Note: Existing artwork hanging on lines inside `graphic-designer/index.html` has been supplemented with an editorial disclaimer indicating they serve as layout & stylistic samples. Official custom client decks will replace them as provided.*

---

## 4. Web Developer Service Media (`web-developer/index.html`)

| Asset Identifier | Slot Description | Recommended Format | Dimensions / Aspect Ratio | Purpose & Content Guidance | Status |
|---|---|---|---|---|---|
| `web-project-1.mp4` / `web-project-1.webp` | Production Website Recording 1 | MP4 / WebP | 1280 &times; 732 (~16:9) | Clean screen recording of responsive website interactions, navigation flow, and micro-interactions. | **Preserved / Pending Review** |
| `web-project-2.mp4` / `web-project-2.webp` | Production Website Recording 2 | MP4 / WebP | 1280 &times; 732 (~16:9) | Modern landing page showcasing dynamic transitions, typography balance, and conversion-focused CTAs. | **Preserved / Pending Review** |

---

## 5. Homepage & Open Graph Media (`index.html`)

| Asset Identifier | Slot Description | Recommended Format | Dimensions | Purpose & Content Guidance | Status |
|---|---|---|---|---|---|
| `og.jpg` / `og-cover.avif` | Global Social Share & Open Graph | JPEG / WebP / AVIF | 1200 &times; 630 (1.91:1) | Branded social banner featuring the "Haroon Mughal GFX" wordmark, the four services list, and Sunlit Clay accent on Onyx background. | **Active / Updated** |
| `icon-192.png` / `icon-512.png` | Web App Manifest Icons | PNG | 192 &times; 192 and 512 &times; 512 | Crisp transparent Haroon Mughal GFX monogram or brand icon. | **Ready for Review** |

---

### Instructions for Applying Media Files:
1. Place newly prepared files into their respective subdirectories (`vectorization/`, `video-editing/`, etc.).
2. In the target HTML file, replace the `<div class="stage">` placeholder block with `<img src="..." alt="..." loading="lazy">` or `<video controls muted playsinline poster="..." src="..."></video>`.
3. Validate that file sizes are optimized (< 250KB for images, < 10MB for video previews) to maintain sub-second page performance.
