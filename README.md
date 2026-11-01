# 태오의 머지 에볼루션 (Taeo's Merge Evolution)

> ⚠️ **주의 (공개 저장소 연동 폴더)**
> 이 폴더(`taeo_game/`)는 상위 `to_ai` 비공개(Private) 저장소 푸시와 **별도로**, 외부 웹 실행 및 이미지 에셋 호스팅을 위해 **전용 공개(Public) GitHub 저장소(`https://github.com/hgkim-one/taeo-merge-assets`)에 업로드되는 폴더**입니다.
> 자세한 작업·보안·배포 규칙은 반드시 [`AGENTS.md`](./AGENTS.md)를 확인하세요.

## 실행 및 배포 경로

- **GitHub Pages (직접 실행)**: <https://hgkim-one.github.io/taeo-merge-assets/>
- **Google Sites**: <https://sites.google.com/view/taeo-merge-evolution>
- **전용 공개 저장소 (Public, Noindex 설정됨)**: <https://github.com/hgkim-one/taeo-merge-assets>

## 폴더 구성

- `game.html` / `index.html`: 7종 진화 테마(3,253개 아이템) 통합 단일 HTML 게임 파일 (Gzip 인라인 번들 + 반응형 모바일/태블릿/데스크탑 레이아웃 적용)
- `assets/`: 7종 테마 일러스트 에셋 (`items/`, `pokemon/`, `mecha/`, `scp/`, `trevor/`, `weapons/`)
- `robots.txt` / `.nojekyll`: 검색엔진 크롤링 차단(`Disallow: /`) 및 GitHub Pages 정적 서빙 설정
- `AGENTS.md`: `to_ai` 전체 푸시와 별도로 진행되는 `taeo-merge-assets` 공개 저장소 배포 및 보안 규칙
- `temp/`: 일회성 빌드·검수 보조 스크립트 보관 폴더 (**공개 저장소 업로드 제외 대상**)
