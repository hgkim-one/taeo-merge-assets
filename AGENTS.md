# `taeo_game` 프로젝트 작업 및 배포 규칙 (필독)

> ⚠️ **중요: 공개(Public) GitHub 저장소 별도 업로드 안내**
> 이 폴더(`~/to_ai/taeo_game/`)는 상위 `~/to_ai` 전체 비공개(Private) 저장소 푸시와 **별도로**, 웹 게임 실행 및 에셋 호스팅을 위해 **전용 공개(Public) GitHub 저장소(`https://github.com/hgkim-one/taeo-merge-assets.git`)에 업로드되는 공개 폴더**입니다.
> 추후 작업 시 착오나 비공개 자료 유출이 발생하지 않도록 아래 규칙을 반드시 준수합니다.

---

## 1. 저장소 분리 구조 및 역할

| 구분 | 대상 경로 | GitHub 저장소 | 공개 여부 | 용도 |
| :--- | :--- | :--- | :--- | :--- |
| **전체 워크스페이스** | `~/to_ai/` 전체 | `https://github.com/hgkim-one/to_ai.git` | 🔒 **Private (비공개)** | 전체 프로젝트 소스 및 히스토리 백업 |
| **게임 전용 배포본** | `~/to_ai/taeo_game/` (게임 본체 및 `assets/`) | `https://github.com/hgkim-one/taeo-merge-assets.git` | 🌐 **Public (공개)** | GitHub Pages 직접 실행 및 Google Sites 에셋(`raw.githubusercontent.com`) 연동 |

- **GitHub Pages 실행 URL**: `https://hgkim-one.github.io/taeo-merge-assets/`
- **Google Sites 연동 URL**: `https://sites.google.com/view/taeo-merge-evolution`

---

## 2. 보안 및 검색엔진 비공개(Noindex) 유지 규칙

1. **민감 정보 절대 포함 금지**:
   - `taeo_game/` 내부 파일은 공개 저장소(`hgkim-one/taeo-merge-assets`)에 그대로 업로드되므로, **개인정보, 계정 비밀번호, API Key/토큰, 내부 서버 주소, 타 하위 프로젝트(`kms_dev`, `kookmin` 등) 파일**을 절대 이 폴더에 넣지 않습니다.
2. **임시 파일(`temp/`) 공개 저장소 업로드 제외**:
   - 검수용 스크린샷, 일회성 빌드/패치 스크립트 등은 반드시 `taeo_game/temp/` 안에서만 작업하고 작업 완료 후 정리하며, **공개 저장소(`taeo-merge-assets`)에는 `temp/` 폴더를 업로드하지 않습니다.**
   - 공개 저장소 업로드 대상 파일: `game.html`, `index.html`, `robots.txt`, `.nojekyll`, `README.md`, `AGENTS.md`, `assets/**`
3. **검색엔진 크롤링 차단 설정 유지**:
   - 공개 저장소이더라도 검색엔진(Google, Bing 등)에 노출되지 않도록 아래 두 가지를 항상 유지해야 합니다.
     - `robots.txt`:
       ```text
       User-agent: *
       Disallow: /
       ```
     - `game.html` 및 `index.html` `<head>` 메타 태그:
       ```html
       <meta name="robots" content="noindex, nofollow, noarchive, nosnippet, noimageindex">
       <meta name="googlebot" content="noindex, nofollow, noarchive, nosnippet, noimageindex">
       ```

---

## 3. 코드/에셋 수정 시 표준 배포 절차 (이중 푸시 필수)

`taeo_game/game.html` 또는 `taeo_game/assets/`를 수정한 경우, 반드시 아래 순서로 **1) `to_ai` 비공개 저장소**와 **2) `taeo-merge-assets` 공개 저장소** 양쪽 모두에 반영합니다.

### Step 1. `index.html` 동기화
GitHub Pages 루트 접속(`https://hgkim-one.github.io/taeo-merge-assets/`) 시 최신 게임이 바로 실행되도록 `game.html`을 `index.html`로 복사합니다.
```powershell
Copy-Item C:\Users\honggu\to_ai\taeo_game\game.html C:\Users\honggu\to_ai\taeo_game\index.html -Force
```

### Step 2. `taeo-merge-assets` (게임 전용 공개 저장소) 동기화 및 푸시
`taeo_game/`의 배포 대상 파일만 전용 공개 저장소(`https://github.com/hgkim-one/taeo-merge-assets.git`)에 커밋 및 푸시합니다 (`temp/` 제외, `--force` 금지).

### Step 3. `to_ai` (전체 비공개 저장소) 커밋 및 푸시
```powershell
git -C C:\Users\honggu\to_ai add taeo_game/
git -C C:\Users\honggu\to_ai commit -m "Update taeo_game"
git -C C:\Users\honggu\to_ai push origin main
```

### Step 4. Google Sites 업데이트 및 시각 검증
- Google Sites(`https://sites.google.com/view/taeo-merge-evolution`)에 최신 `game.html` 소스 코드(235KB Gzip 번들) 또는 임베드 구성을 반영하고 **게시**합니다.
- 배포 후 **모바일(`320x568`, `375x667`, `390x844`), 태블릿(`768x1024`, `1024x768`), 데스크탑(`1366x768`, `1920x1080`)** 뷰포트에서 레이아웃 깨짐(런처 모달 1열 카드 그리드, `8x8` 타일 배지, 스크롤 여부)과 실제 게임 실행을 시각적으로 검증합니다.
