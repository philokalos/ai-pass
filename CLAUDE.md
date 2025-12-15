# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**AI Creative Pass** - A premium digital gift card experience for AI subscriptions (Manito gift).
Single-page web app optimized for QR code scanning on mobile devices.

## Live URLs

- **Gift Card**: https://philokalos.github.io/ai-pass/
- **QR Generator**: https://philokalos.github.io/ai-pass/qr-generator.html
- **Repository**: https://github.com/philokalos/ai-pass

## File Structure

```
ai-pass/
├── index.html        # Main gift card app (all CSS/JS embedded)
├── qr-generator.html # QR code generator for the gift card URL
├── CLAUDE.md         # This file
└── README.md         # Project documentation
```

## Architecture

- **Single HTML file**: All CSS and JavaScript embedded in `index.html`
- **No build system**: Vanilla HTML/CSS/JS, no frameworks or dependencies
- **Static hosting**: GitHub Pages deployment

## Key Features

- **Landing animation**: 3-second unboxing sequence on first visit
- **3D flip card**: Touch/click/swipe interaction for front/back viewing
- **Responsive design**: Mobile-first, supports tablet and desktop
- **Visit tracking**: localStorage for animation skip on return visits

## Development

### Local Testing

```bash
# Using Python (recommended)
python3 -m http.server 8000
# Open http://localhost:8000

# Using Node.js
npx serve .
# Open http://localhost:3000

# Or simply open index.html directly in browser
```

### Reset State

Clear localStorage to reset animation and flip tracking:
- Browser DevTools > Application > Local Storage > Clear
- Or press `Ctrl+R` while on the page

### Keyboard Shortcuts

- `Space`: Flip card
- `Ctrl+R`: Reset localStorage and reload

## Design Tokens

Key values in CSS variables (`:root`):
- Card dimensions: 340x480px (mobile), 420x592px (tablet+)
- Colors: Purple gradient background (`#667eea` to `#764ba2`)
- Fonts: Inter (display), JetBrains Mono (amounts/numbers)
- Animation easing: `cubic-bezier(0.4, 0.0, 0.2, 1)`

## Deployment

### GitHub Pages

1. Push to `main` branch
2. Settings > Pages > Source: Deploy from branch
3. Select `main` branch, `/ (root)` folder
4. Access at: `https://<username>.github.io/<repo-name>/`

### QR Code Generation

Generate QR pointing to deployed URL using any QR generator service.
