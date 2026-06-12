# Agent Documentation - Star Dance Academy

This file details the workspace configuration, design decisions, and architectural guidelines established for the modern, high-converting landing page of **Star Dance Academy** in Raipur, Chhattisgarh. It acts as a hand-off log for subsequent AI agents or human developers working on this codebase.

## 1. Project Context
- **Client**: Star Dance Academy (Raipur's premier dance academy).
- **Location Context**: Localized for Samta Colony, Raipur, seeking organic ranking in Raipur search results.
- **Vibe & Style**: High-contrast, energetic, and highly professional. Inspired by the bold typography and structured visual layouts of **Broadway Dance Center (BDC)** and the sleek, immersive dark-themed media elements of **CLI Studios**.
- **Social Proof**: 4.9/5 stars on Google (182 verified reviews).
- **Session Timestamp**: June 12, 2026.
- **Created By**: Antigravity (Advanced Agentic Coding assistant from Google DeepMind).
- **GitHub Repository**: [shriyanshthakur/star-dance-academy](https://github.com/shriyanshthakur/star-dance-academy)

---

## 2. Tech Stack & Integration

### Core Stack
- **Framework**: [Astro v6](https://astro.build) (Static site output model).
- **Styling**: Tailwind CSS v4 integrated natively via Vite (`@tailwindcss/vite`).

### Custom Theme & Typography
- **Google Fonts Integration**:
  - Headings: `Syne` (Bold, wide, high-contrast personality).
  - Accents/UI: `Outfit` (Modern, geometric geometric-sans).
  - Body Copy: `Plus Jakarta Sans` (Clean, highly readable humanist-sans).
- **Design Tokens**: Managed in the CSS theme layer in [global.css](file:///d:/projects/star-dance-academy/src/styles/global.css).
  - Brand Palette: Energetic Reds (`#FF1A40`), Warm Golds/Yellows (`#FFC72C`), Stark Blacks/Whites (`#080808` / `#FAFAFA`).
  - Custom UI elements: `.glass-card`, `.glass-card-hover`, and thick BDC frames (`.bdc-frame`).

---

## 3. Directory Structure & Files

Key files created/modified during the session:
```text
d:/projects/star-dance-academy/
├── package.json                 # Configured Astro + Tailwind CSS v4 dependencies
├── astro.config.mjs             # Integrated @tailwindcss/vite Vite plugin
├── agent.md                     # This agent developer document
├── public/
│   └── favicon.svg              # Brand star-type favicon
└── src/
    ├── styles/
    │   └── global.css           # Google Fonts imports, Tailwind @theme mappings, custom scrollbars
    ├── layouts/
    │   └── Layout.astro         # LocalBusiness Schema JSON-LD, SEO tags, responsive mobile drawer
    ├── components/
    │   ├── Hero.astro           # Dynamic background, bold tagline, CTA targets
    │   ├── About.astro          # Mission copy, stats counters, BDC framed grid images
    │   ├── ClassStyles.astro    # Curriculum masonry grid, customized styles array & hover zooms
    │   ├── Testimonials.astro   # Google Rating summary, student reviews container
    │   └── Footer.astro         # Contact hours, WhatsApp redirection form (inputs optional)
    └── pages/
        └── index.astro          # Orchestrates all landing page segments
```

---

## 4. Architectural & Styling Details

### A. Responsive Mobile Navigation Drawer
- Built a mobile navigation toggle button inside the header next to the CTA.
- Created a slide-out navigation overlay (`#mobile-menu`) with backdrop blur (`backdrop-blur-xl`) that slides out from the right (`translate-x-full`).
- Tied it to an inline, lightweight client-side script that toggles classes and manages `document.body.style.overflow` to prevent scrolling when open.

### B. Grid Column Balance & Typography Scaling
- **About Section Grid**:
  - Set the left column span to `lg:col-span-7` (58% width) and the right column to `lg:col-span-5` (42% width).
  - Scaled the heading size to `text-3xl sm:text-4xl lg:text-4xl xl:text-5xl 2xl:text-6xl`. This ensures long Syne words (like "PROFESSIONAL") fit perfectly without running under the images on smaller laptop viewports.
- **Class Styles Header**:
  - Swapped the `md:flex-row` side-by-side layout with `lg:flex-row` to keep the elements stacked on tablets and only go horizontal on desktops.
  - Reduced the heading size to `text-3xl sm:text-4xl lg:text-4xl xl:text-5xl`.
- **Testimonials Columns**:
  - Balanced the columns to `lg:col-span-5` (left) and `lg:col-span-7` (right) with the same heading sizes.

### C. Prevention of iOS Form Focus Auto-Zoom
- Set input text size to `text-base` (16px) on form input fields (`Your Name`, `WhatsApp Number`) and select dropdowns in the footer batch inquiry card.
- This prevents mobile Safari and Chrome on iOS devices from zooming in automatically on focus, keeping the user viewport locked.

### D. WhatsApp Redirection & Fallback Messaging
- Created a form in the footer with optional fields (Name, Preferred Style) that redirects to the academy's phone number (`+91 93295 59903`) on WhatsApp.
- **With Inputs**: Sends a compiled booking request detailing user name and style choice.
- **Without Inputs**: Submitting empty/blank fields triggers a fallback automated message:
  `Hi Star Dance Academy! I absolutely love your academy and would like to inquire about batch schedules, fee structure, and trial classes. Let's chat!`

### E. WebAssembly Out of Memory (OOM) Compiler Fix
- **Issue**: Excessively long Unsplash URLs with nested query tags (`ixlib`, `ixid`, `%3D%3D` encoded tokens) pasted during image edits caused the Astro WASM compiler to panic and trigger an Out of Memory crash.
- **Solution**: Shortened Unsplash image URLs in `About.astro` (Frame 2) and `ClassStyles.astro` (Styles Array) to a standardized parameters layout (`?auto=format&fit=crop&w=600&q=80`). This resolved the memory leaks during AST transformations and restored build stability.

---

## 5. Development & Operations Guide

### Dev Server
To start the local developer server:
```powershell
npm run dev
```

### Static Production Build
To build the optimized static project:
```powershell
npm run build
```
This builds static HTML and client assets inside the `/dist` directory. The production build now compiles stably and is completely warning-free (1.40s execution time).
