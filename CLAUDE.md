# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**my-profile-site** is a personal portfolio website for 박창호 (a freelance developer). It's a static site built with vanilla HTML, CSS, and JavaScript—no build tools, no frameworks, just plain web technologies. The site showcases a professional profile with sections for About, Skills, Portfolio, and Contact.

## Architecture

The project follows a traditional static site structure:

- **index.html** — Single HTML file containing the full page markup. All sections (header, hero, about, skills, portfolio, contact, footer) are defined here with semantic HTML5 elements.
- **style.css** — Custom CSS file that supplements Tailwind CSS (loaded via CDN). Contains animations, responsive media queries, dark mode support, and custom styles for components like `.nav-link`, `.portfolio-card`, and gradient effects.
- **script.js** — Vanilla JavaScript for interactivity: smooth scrolling navigation, active nav link highlighting on scroll, header shadow on scroll, and portfolio card animations.

**No dependencies:** The project uses Tailwind CSS via CDN (https://cdn.tailwindcss.com) and has no npm packages, package.json, or build step.

## Key Files & Their Responsibilities

### index.html
- **Structure:** Defines all page sections (header/nav, hero, about, skills, portfolio, contact, footer).
- **Color scheme:** Red gradient theme (`bg-gradient-to-br from-red-800 via-red-700 to-red-900` for hero, red accents throughout). Tailwind and custom classes mixed.
- **Responsiveness:** Uses Tailwind's responsive prefixes (`md:`, `lg:`) for grid layouts and typography scaling.
- **Navigation:** Fixed header with smooth-scroll anchor links to `#about`, `#skills`, `#portfolio`, `#contact`.
- **Portfolio section:** Three placeholder cards (프로젝트 1–3) with emoji icons, descriptions, and GitHub/Live links (currently `#`).
- **Content:** All in Korean; tagline is "시작이절반이다에서 절반만 하는애" (starting is half done, and I only do half).

### style.css
- **Scroll behavior:** Smooth scrolling via `scroll-behavior: smooth` on `html`.
- **Navigation styling:** `.nav-link.active` class with blue color and bottom border (applied by JS on scroll).
- **Animations:**
  - `fadeIn` keyframe with staggered `animation-delay` per section (0s, 0.1s, 0.2s, etc.).
  - `gradientShift` for animated gradient text backgrounds.
  - `portfolio-card` hover effect: `translateY(-8px)`, shadow, and gradient overlay on background.
  - Nav link underline animation via `::after` pseudo-element on hover.
- **Responsive design:** Media query for max-width 768px adjusts nav gap, section padding, font sizes, and portfolio card margins.
- **Dark mode:** `@media (prefers-color-scheme: dark)` with slate/navy background colors and light text.

### script.js
- **Smooth scroll:** Intercepts clicks on anchor links (`a[href^="#"]`), prevents default, and scrolls to target smoothly.
- **Active nav link:** `updateActiveNavLink()` function checks scroll position and highlights the nav link for the current section. Runs on `scroll` and `load` events.
- **Header shadow:** Adds/removes `shadow-md` class on header when scroll > 100px.
- **Portfolio card click animation:** Resets CSS animation on click (minimal visual effect).
- **Page load log:** Console message "프로필 웹사이트 로드 완료!" on DOMContentLoaded.

## Development Workflow

Since there's no build step, development is immediate:

1. **Edit files locally** — Make changes to index.html, style.css, or script.js.
2. **Open in browser** — Open `index.html` directly in a web browser (file:// protocol works fine for static content).
3. **Refresh to see changes** — Browser cache may require Ctrl+F5 or hard refresh.

No linting, testing, or deployment pipeline is configured yet.

## Common Tasks

### Update portfolio projects
Edit the three `.portfolio-card` divs in `index.html` (around lines 90–140). Replace the placeholder title, description, emoji, and GitHub/Live links. Each card follows the same structure:
```html
<div class="portfolio-card bg-white rounded-lg shadow-md overflow-hidden hover:shadow-2xl transition">
    <div class="bg-gradient-to-br from-red-600 to-red-700 h-48 flex items-center justify-center">
        <span class="text-white text-6xl">EMOJI</span>
    </div>
    <div class="p-6">
        <h3 class="text-2xl font-bold text-gray-900 mb-2">PROJECT TITLE</h3>
        <p class="text-gray-700 mb-4">DESCRIPTION</p>
        <div class="flex gap-2">
            <a href="GITHUB_URL" class="inline-block text-red-600 hover:text-red-700 font-semibold">GitHub →</a>
            <a href="LIVE_URL" class="inline-block text-red-700 hover:text-red-800 font-semibold ml-4">Live →</a>
        </div>
    </div>
</div>
```

### Change colors
The site uses a red theme. To adjust:
- Red gradients in index.html: Update `from-red-800`, `via-red-700`, `to-red-900`, `from-red-600`, etc.
- Custom styles in style.css: Gradients like `linear-gradient(135deg, #7c3aed, #6d28d9)` (purple in hover effect) can be replaced.
- Tailwind uses standard color names; use Tailwind docs for exact hex values or use custom Tailwind config if more control is needed (would require CDN custom config or local build).

### Update About section text
Edit the paragraph text in the "About Me" section (index.html, around lines 45–54). Keep the HTML structure and Tailwind classes intact.

### Add animations or transitions
- New animations go in style.css as `@keyframes`.
- Apply them to elements using `animation: name duration timing delay` or Tailwind's `animate-` classes (if Tailwind supports them—custom ones must use CSS).
- Test in browser; be mindful of performance (GPU-accelerated properties like `transform` and `opacity` are faster).

### Add new sections
Follow the existing pattern:
1. Add a section element with an `id` for anchor links: `<section id="newsection">`.
2. Use the same structure: max-width container, padding, background color from the red palette or white.
3. Add a nav link in the header: `<li><a href="#newsection" class="nav-link">Label</a></li>`.
4. The JavaScript will auto-highlight the nav link on scroll without changes.

## Accessibility & Performance Notes

- **Tailwind via CDN:** Site is lightweight and loads fast, but Tailwind is unoptimized (full bundle). For production, consider Tailwind build/purging.
- **Color contrast:** Red theme has good contrast for accessibility in light mode; dark mode is implemented but may need refinement for WCAG AA compliance.
- **Smooth scroll:** Supported in all modern browsers; older browsers fall back to instant scroll.
- **Responsive:** Covers mobile (< 768px) and desktop. Test on various screen sizes when making layout changes.

## Future Enhancements (Not Yet Implemented)

- Form validation for contact section (currently non-functional; just displays a placeholder message).
- Dynamic portfolio projects (could pull from a JSON file or API with a small JS change, but not currently needed).
- Build pipeline with Tailwind JIT for smaller CSS bundle.
- Testing framework for JavaScript interactivity.
- SEO meta tags (basic ones are in index.html, but could be expanded).
