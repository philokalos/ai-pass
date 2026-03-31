# AI Pass

AI 구독 디지털 기프트카드 — 프리미엄 선물 경험을 위한 인터랙티브 웹앱

**Live**: https://philokalos.github.io/ai-pass/

## 주요 기능

- **Security Seal 애니메이션**: 다크 오버레이에서 "Break Seal & Enter" 잠금 해제 효과
- **3D 플립 카드**: 터치/클릭/스와이프로 앞뒷면 전환 (`transform-style: preserve-3d`)
- **Snow Particle 애니메이션**: Canvas 기반 눈 파티클 효과
- **사운드 이펙트**: Web Audio API (iOS 지원을 위한 lazy AudioContext 초기화)
- **QR 코드 페이지**: 모바일에서 바로 스캔 가능한 기프트카드 전달
- **모바일 최적화**: Mobile-first 반응형 디자인

## 기프트카드 정보

- **금액**: ₩60,000
- **유효기간**: 180일
- **지원 서비스**: Midjourney, Suno, ChatGPT Plus, Claude Pro 등

## 기술 스택

| 항목 | 내용 |
|------|------|
| Frontend | Vanilla HTML5 / CSS3 / JavaScript (ES6+) |
| 빌드 | 없음 (No build step) |
| 배포 | GitHub Pages |
| 테스트 | Playwright E2E |

## 사용법

1. QR 코드를 모바일로 스캔
2. 언박싱 애니메이션 감상
3. 카드 앞면에서 기프트 상세 확인
4. 카드를 뒤집어 사용 안내 확인

## 시작하기

```bash
# 로컬 서버 실행
python3 -m http.server 8000

# 또는 npm 사용
npm run serve   # :3000

# E2E 테스트
npm run test:e2e
```

브라우저에서 `http://localhost:8000` 접속

## 프로젝트 구조

```
ai-pass/
  index.html        # 메인 기프트카드 페이지 (CSS/JS 포함)
  qr-generator.html # QR 코드 생성 페이지
  e2e/              # Playwright E2E 테스트
```

## 참고사항

- 상태는 세션 전용 (새로고침 시 초기화 — 선물 경험을 위한 의도적 설계)
- 사운드가 재생되지 않으면 사용자 제스처 후 재시도 (iOS 브라우저 정책)

## License

MIT
