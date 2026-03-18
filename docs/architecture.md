# Architecture — ai-pass

## 개요

단일 HTML 파일 아키텍처. 빌드 스텝 없음.

## 파일 구조

```
ai-pass/
  index.html        # 메인 페이지 (CSS + JS 인라인 포함)
  qr-generator.html # QR 코드 생성 유틸리티
  e2e/              # Playwright E2E 테스트
```

## 핵심 컴포넌트

| 컴포넌트 | 설명 |
|----------|------|
| Security Seal | 다크 오버레이 → 잠금 해제 애니메이션 |
| Flip Card | CSS 3D transform (preserve-3d) |
| Snow Particles | requestAnimationFrame Canvas 루프 |
| Audio Engine | Web Audio API (lazy init) |

## 상태 관리

세션 전용 JavaScript 변수 (`isFlipped`, `isAnimating`, `hasLiked`, `snowParticles[]`)
localStorage 없음 — 새로고침 시 초기화가 의도된 동작.

## 배포

GitHub Pages 직접 서빙 (빌드 불필요).
