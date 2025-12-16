# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**AI Creative Pass** - A premium digital gift card experience for AI subscriptions (Manito gift).
Single-page web app optimized for QR code scanning on mobile devices.

## Live URLs

- **Gift Card**: https://philokalos.github.io/ai-pass/
- **QR Generator**: https://philokalos.github.io/ai-pass/qr-generator.html
- **Repository**: https://github.com/philokalos/ai-pass

## Architecture

- **Single HTML file**: All CSS and JavaScript embedded in `index.html`
- **No build system**: Vanilla HTML/CSS/JS, no frameworks
- **Static hosting**: GitHub Pages deployment
- **External dependency**: `qr-generator.html` uses qrcode.js from CDN

### CSS Structure (index.html)

Organized in numbered sections:
1. **CSS Variables & Design System** - Design tokens in `:root`
2. **Reset & Base Styles** - Normalize and body setup
3. **Security Seal Overlay** - Dark overlay with unlock button
4. **Main Container Styles** - Wrapper with blur/reveal animation
5. **3D Flip Card Styles** - `transform-style: preserve-3d` flip mechanics
6. **Card Front Styles** - Amount box, service list, brutalist borders
7. **Card Back Styles** - How-to-use steps, info boxes
8. **Flip Indicator Styles** - "Tap to flip" button
9. **Responsive Styles** - Breakpoints at 768px, 1024px, 360px, landscape

### JavaScript Structure (index.html)

1. **State Management** - `isFlipped`, `flipCount` (localStorage persistence)
2. **DOM Elements** - Cached references to key elements
3. **Interaction Logic** - Security seal unlock animation
4. **Card Flip Mechanics** - `flipCard()` with CSS class toggle
5. **Touch & Swipe Handlers** - Horizontal swipe detection (50px threshold)

## Key Features

- **Security seal**: Dark overlay with "Break Seal & Enter" button (first screen)
- **3D flip card**: Touch/click/swipe interaction for front/back viewing
- **Responsive design**: Mobile-first, supports tablet and desktop
- **Visit tracking**: localStorage for flip indicator visibility

## Development

### Local Testing

```bash
python3 -m http.server 8000
# Open http://localhost:8000
```

### Reset State

Clear localStorage to reset flip tracking:
- Browser DevTools > Application > Local Storage > Clear

## Design Tokens

Current brutalist design system (`:root` variables):

```css
/* Background */
--bg-color: #E0E0E0;
--grid-color: rgba(0, 0, 0, 0.15);  /* 32px grid pattern */

/* Card */
--card-bg: #FFFFFF;
--card-border: #000000;
--card-border-width: 3px;
--card-shadow: 10px 10px 0px 0px #000000;

/* Accent */
--info-bg: #FFE500;  /* Yellow info boxes */

/* Typography */
--font-display: 'Inter Tight';
--font-mono: 'JetBrains Mono';
```

Card dimensions: `380x640px` (mobile), `480x760px` (tablet+)

## Deployment

Push to `main` branch triggers GitHub Pages deployment.
Access at: `https://philokalos.github.io/ai-pass/`
