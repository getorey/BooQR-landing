# Landing — BooQR 영업·BMT 페이지

본 디렉터리는 [getorey/BooQR-landing](https://github.com/getorey/BooQR-landing) 저장소로 자동 배포된다.

## 구조

```
landing/
├── index.html        — 단일 페이지 (Tailwind CDN, 빌드 단계 0)
└── README.md         — 본 파일 (배포 시 함께 푸시)
```

## 자동 배포 플로우

```
[로컬에서 landing/ 수정]
        ↓
PR을 main으로 → 머지
        ↓
[수동] git checkout deploy/landing && git merge main && git push
        ↓
.github/workflows/deploy-landing.yml 트리거
        ↓
landing/ 만 추출 → getorey/BooQR-landing 으로 force push
        ↓
GitHub Pages 자동 빌드·배포 (BooQR-landing 저장소 측)
```

`deploy/landing` 브랜치를 운영 게이트로 사용 — main에 들어간 즉시 배포되지 않고
영업 일정에 맞춰 fast-forward 머지하면 배포됨.

## 사전 셋업 (한 번만)

### 1. BooQR-landing 저장소 준비
- repo: https://github.com/getorey/BooQR-landing (이미 존재)
- Settings → Pages → Source: `Deploy from a branch` → `main` / `/ (root)`

### 2. 배포 토큰 (Personal Access Token)
- GitHub 우측 상단 프로필 → Settings → Developer settings → Personal access tokens → Tokens (classic)
- "Generate new token" → 권한 `repo`만 → 만료 1년
- 이 token을 BooQR repo에 secret으로 등록:
  - Settings → Secrets and variables → Actions
  - `LANDING_DEPLOY_TOKEN` = (위 PAT)

### 3. deploy/landing 브랜치 생성 (한 번만)
```bash
git checkout -b deploy/landing
git push origin deploy/landing
```

## 운영 시 배포 절차

```bash
# 1. landing/ 수정 후 PR로 main에 머지

# 2. 배포 시점에:
git checkout deploy/landing
git pull
git merge --ff-only origin/main
git push origin deploy/landing

# 3. Actions 탭에서 "Deploy Landing" 워크플로 진행 상황 확인
```

## 로컬 미리보기

빌드 단계 없음. 그냥 브라우저로 열기:

```bash
open landing/index.html

# 또는 간단 HTTP 서버
python3 -m http.server 8080 --directory landing
# → http://localhost:8080
```

## 데모 URL 변경 시

`index.html`에서 `demo-booqr.koavio.com`을 검색해 새 도메인으로 일괄 교체.
나중에 별도 데모 환경(예: `demo.booqr.kr`)이 생기면 이 부분만 수정 + 머지·배포.

## 디자인 변경

Tailwind CDN을 쓰고 있어 빌드 없음. 클래스 직접 수정 → 저장 → 새로고침.
v2 작업 시 별도 PR로 진행 권장.
