# booqr-landing

BooQR 제품 소개 정적 페이지 — `demo.booqr.kr`로 배포되는 마케팅 사이트.

## 호스팅

- GitHub Pages (이 저장소의 `main` 브랜치 자동 배포)
- 커스텀 도메인: `demo.booqr.kr`
- 자동 HTTPS (Let's Encrypt)

## 운영 앱과의 관계

이 저장소는 정적 안내 페이지만 포함합니다. 실제 BooQR SaaS 본체는 별도의 private 저장소(`getorey/BooQR`)에서 Railway에 배포됩니다.

| 자산 | 저장소 | 호스팅 | 도메인 |
|---|---|---|---|
| 운영 앱 | `getorey/BooQR` (private) | Railway | `booqr.kr` |
| 정적 안내 페이지 (이 저장소) | `getorey/booqr-landing` (public) | GitHub Pages | `demo.booqr.kr` |

## 디렉터리 구조

```
booqr-landing/
├── index.html        메인
├── features.html     기능
├── flow.html         입장 흐름
├── pricing.html      도입 비용
├── contact.html      문의
├── CNAME             demo.booqr.kr
├── .nojekyll         Jekyll 처리 끄기
├── assets/
│   ├── style.css
│   └── screenshots/  실 화면 캡처 (가짜 데이터 사용)
└── .github/workflows/deploy-pages.yml
```

## 콘텐츠 수정

마케팅 카피·연락처·이미지 등 일반적인 변경은 `main` 브랜치에 직접 푸시하면 자동 배포됩니다. 긴급한 오타 수정은 GitHub 웹 에디터에서도 가능합니다.

```bash
git checkout main
# 파일 수정
git commit -am "docs: 도입 문의 연락처 변경"
git push origin main
# → GitHub Actions가 demo.booqr.kr에 자동 배포
```

## 보안

이 저장소는 public입니다. 어떤 시크릿(API 키, DB 비밀번호, HMAC 시크릿)도 절대 커밋하지 마세요. 모든 fetch 호출은 키 없이 호출 가능한 공개 API만 사용합니다 (현재 mailto와 정적 콘텐츠만 사용).

## 스크린샷 정책

`assets/screenshots/`에 들어가는 화면 캡처는 반드시 **운영 환경의 시연용 가짜 tenant(`demo_internal`)**에서 생성한 것만 사용합니다. 실 기관·실 방문자 데이터가 노출되지 않도록 주의합니다.

## 라이선스

(추후 결정)
