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

## State Management

### Session State (메모리만, localStorage 미사용)
```javascript
let isFlipped = false;           // 현재 뒤집힘 상태
let hasFlippedThisSession = false;  // 세션 중 뒤집힘 여부
let isAnimating = false;         // 애니메이션 잠금
let hasLiked = false;            // 좋아요 상태 (리셋 안됨)
```

### Audio Context
```javascript
let audioCtx = null;  // 공유 Web Audio API context
// getAudioContext()에서 lazy 초기화
```

### Snow Particles
```javascript
let snowParticles = [];      // 활성 파티클 배열
let snowAnimationId = null;  // requestAnimationFrame ID
let snowSpawnerId = null;    // setInterval ID
```

**의도적 설계**: 페이지 리로드 시 모든 상태 초기화 (일회용 선물 카드 경험)

## ⚠️ Anti-Patterns

### ❌ AudioContext resume() Promise 무시
```javascript
if (audioCtx.state === 'suspended') {
  audioCtx.resume();  // Promise 반환하지만 무시됨
}
```
- **위치**: `index.html:1100-1110`
- **해결**: `return audioCtx.resume().catch(() => audioCtx)`

### ❌ Snow 애니메이션 메모리 누수
```javascript
// triggerSnow() 여러 번 호출 시 interval 누적
snowSpawnerId = setInterval(...);  // 이전 interval 미정리
```
- **위치**: `index.html:1569-1572`
- **해결**: `triggerSnow()` 시작 시 `stopSnow()` 호출

### ❌ Touch/Click 이중 핸들러
```javascript
let sealTouchHandled = false;
// touchend → unlockContent() 후 click도 발생 가능
```
- **위치**: `index.html:1257-1277`
- 타이밍 window에서 이중 실행 가능

### ❌ CSS left/top 불필요한 재설정
```javascript
p.el.style.left = '0';  // transform으로 이미 처리됨
p.el.style.top = '0';
```
- **위치**: `index.html:1658-1661`
- 매 프레임 layout recalc 유발

## Troubleshooting

| 증상 | 원인 | 해결 |
|------|------|------|
| 소리 안남 | AudioContext suspended | DevTools > Console > `audioCtx.state` 확인 |
| 소리 안남 | iOS Safari user gesture 필요 | 첫 터치 이벤트에서 resume() 호출 |
| 카드 두 번 뒤집힘 | touch-to-click 변환 | `sealTouchHandled` 플래그 타이밍 확인 |
| 좋아요 버튼 리셋 안됨 | 의도된 동작 | `hasLiked`는 세션 중 영구 (설계 확인) |
| Snow 애니메이션 느림 | 파티클 누적 | `stopSnow()` 호출 누락 확인 |
| QR 페이지 빈 화면 | CDN 차단/다운 | `cdn.jsdelivr.net` 접근성 확인 |
