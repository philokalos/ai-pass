# CLAUDE.md - AI Pass

Digital gift card | Single HTML + Vanilla JS

**Live**: https://philokalos.github.io/ai-pass/

## Commands

```bash
python3 -m http.server 8000    # Local testing
# Clear localStorage to reset state (DevTools > Application)
```

## Architecture

- **Single HTML file**: All CSS/JS embedded in `index.html`
- **No build**: Vanilla HTML/CSS/JS, GitHub Pages deployment
- **State**: Session-only (intentional reset on reload for gift experience)

## Key Features

1. **Security Seal**: Dark overlay → "Break Seal & Enter" unlock animation
2. **3D Flip Card**: Touch/click/swipe with `transform-style: preserve-3d`
3. **Snow Particles**: Canvas animation with spawner interval
4. **Sound Effects**: Web Audio API with lazy AudioContext init

## State (Session Only)

```javascript
isFlipped          // Current flip state
hasFlippedThisSession  // Session flip tracking
isAnimating        // Animation lock
hasLiked           // Like button (persists in session)
snowParticles[]    // Active particles
```

## Anti-Patterns

| Wrong | Correct |
|-------|---------|
| Ignore `audioCtx.resume()` Promise | `return audioCtx.resume().catch(() => audioCtx)` |
| Multiple `triggerSnow()` calls | Call `stopSnow()` first to clear interval |
| Touch + click double fire | Check `sealTouchHandled` timing |
| Set `left/top` every frame | Use transform only (avoid layout recalc) |

## Design Tokens

```css
--card-bg: #FFFFFF
--card-border: #000000
--card-shadow: 10px 10px 0px 0px #000000
--info-bg: #FFE500
--font-display: 'Inter Tight'
--font-mono: 'JetBrains Mono'
```

Card: 380x640px (mobile), 480x760px (tablet+)

## Troubleshooting

| Issue | Solution |
|-------|----------|
| No sound | Check `audioCtx.state`, iOS needs user gesture |
| Card flips twice | Touch-to-click conversion timing |
| Snow animation slow | Particles accumulating, call `stopSnow()` |
| QR page blank | Check cdn.jsdelivr.net accessibility |
