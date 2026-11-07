# Personal Portfolio — Hugo Celadon

Hugo와 Celadon 테마를 활용하여 제작한 개인 포트폴리오 웹사이트입니다. 자기소개, 학력 및 활동 이력, 개발 프로젝트, 학습 기록을 소개합니다.

## 1. 프로젝트 정보

| 항목 | 내용 |
|---|---|
| 프로젝트명 | Personal Portfolio |
| 제작자 | 배성민 |
| 사용 테마 | Hugo Celadon |
| 정적 사이트 생성기 | Hugo Extended |
| 버전 관리 | Git / GitHub |
| 자동 배포 | GitHub Actions |
| 호스팅 | GitHub Pages |
| 배포 브랜치 | main |

- **웹사이트:** https://seongmin-vae.github.io/portfolio.assignment/
- **GitHub 저장소:** https://github.com/seongmin-vae/portfolio.assignment
- **GitHub Actions:** https://github.com/seongmin-vae/portfolio.assignment/actions

## 2. 개발 및 실행 환경 (P56)

### 사용 도구 및 버전

| 도구 | 버전 | 용도 |
|---|---|---|
| Hugo Extended | 0.167.0 | 정적 웹사이트 빌드 |
| Python | 3.9 이상 | 교수님 제공 준비 스크립트 실행 |
| Python (Actions) | 3.12 | 배포 자동화 스크립트 실행 |
| Node.js (Actions) | 24 | 배포 작업 환경 구성 |
| Go (Actions) | 1.27.1 | Hugo 관련 빌드 환경 |
| Dart Sass (Actions) | 1.105.0 | 스타일시트 빌드 지원 |
| Git | 설치된 로컬 버전 | 소스 코드 버전 관리 |

배포 준비에는 수업에서 제공된 `prepare_github_pages.py` 버전 3.1을 사용했습니다.

GitHub Actions에서는 워크플로에 지정된 도구를 자동으로 설치합니다. 로컬에서 사이트를 미리 확인하는 경우에는 Git과 Hugo Extended가 기본적으로 필요하며, 테마의 스타일 처리 환경에 따라 Dart Sass가 추가로 필요할 수 있습니다.

### 설치 방법

**1. Git 설치**

https://git-scm.com/downloads

설치 후 Git Bash에서 확인합니다.

```bash
git --version
```

**2. Hugo Extended 설치**

Hugo Extended 0.167.0 릴리스:

https://github.com/gohugoio/hugo/releases/tag/v0.167.0

운영체제에 맞는 Extended 버전을 다운로드하고 압축을 해제한 뒤, 실행 파일이 있는 경로를 PATH 환경 변수에 등록합니다.

설치 확인:

```bash
hugo version
```

출력에 `v0.167.0`과 `extended`가 표시되는지 확인합니다.

**3. Python 설치 (배포 준비 스크립트를 다시 실행하는 경우)**

https://www.python.org/downloads/

Python 3.9 이상이 필요하며, GitHub Actions에서는 Python 3.12를 사용합니다.

```bash
python --version
```

기존 저장소에는 배포 준비 결과가 이미 포함되어 있으므로, 사이트 콘텐츠를 수정할 때마다 준비 스크립트를 다시 실행할 필요는 없습니다.

## 3. 프로젝트 설치 및 로컬 실행 (P56)

### 3.1. 저장소 복제

Git Bash에서 다음 명령어를 실행합니다.

```bash
git clone https://github.com/seongmin-vae/portfolio.assignment.git
cd portfolio.assignment
```

### 3.2. Hugo 사이트 폴더로 이동

실제로 배포되는 Hugo 사이트는 저장소 최상위의 `site/` 폴더 안에 있습니다.

```bash
cd site
```

### 3.3. 로컬 개발 서버 실행

```bash
hugo server --config hugo.toml,pages.json --theme template --themesDir themes --baseURL http://localhost:1313/
```

실행에 성공하면 브라우저에서 다음 주소에 접속합니다.

http://localhost:1313/

개발 서버가 실행 중인 동안에는 Markdown 콘텐츠와 설정 파일을 수정하면서 결과를 확인할 수 있습니다.

서버를 종료하려면 터미널에서 `Ctrl + C`를 누릅니다.

### 3.4. 정적 사이트 빌드

`site/` 폴더에서 다음 명령어를 실행합니다.

```bash
hugo --gc --minify --config hugo.toml,pages.json --destination ../public --baseURL https://seongmin-vae.github.io/portfolio.assignment/ --theme template --themesDir themes --enableGitInfo=false
```

빌드 결과는 저장소 최상위의 `public/` 폴더에 생성됩니다.

실제 GitHub Pages 배포에서는 교수님이 제공하신 자동화 스크립트가 추가로 URL 경로를 보정합니다. 따라서 로컬 Hugo 빌드와 배포용 빌드에는 이 처리 과정의 차이가 있습니다.

## 4. 주요 파일 구조 및 수정 위치 (P57)

```text
portfolio.assignment/
├── .github/
│   ├── workflows/
│   │   └── hugo-pages.yml
│   └── pages_build.py
├── site/
│   ├── hugo.toml
│   ├── pages.json
│   ├── data/
│   │   ├── profile.yaml
│   │   ├── news.yaml
│   │   ├── research.yaml
│   │   └── writing.yaml
│   ├── content/
│   │   └── writing/
│   ├── static/
│   │   └── images/
│   └── themes/
│       └── template/
├── .github-pages.json
├── prepare_github_pages.py
└── README.md
```

### 주요 수정 파일

| 파일 경로 | 수정 내용 |
|---|---|
| `site/hugo.toml` | 사이트 제목, 메뉴, 섹션 구성, Hugo 설정 |
| `site/data/profile.yaml` | 자기소개, 프로필 사진, 외부 링크 |
| `site/data/news.yaml` | EXPERIENCE 섹션의 학력 및 활동 이력 |
| `site/data/research.yaml` | PROJECTS 섹션의 프로젝트 정보 |
| `site/data/writing.yaml` | WRITING 섹션의 카드 정보 |
| `site/content/writing/` | 개별 Markdown 게시글 및 학습 기록 |
| `site/static/images/` | 프로필, 프로젝트, 게시글 이미지 |
| `site/themes/template/assets/css/main.css` | 테마의 CSS 디자인 및 메뉴 스타일 |
| `site/pages.json` | GitHub Pages 배포 주소 등 운영 설정 |
| `.github/workflows/hugo-pages.yml` | GitHub Actions 자동 배포 설정 |

일반적인 콘텐츠 수정은 `site/data/`, `site/content/`, `site/static/images/`에서 수행합니다.

배포 주소나 빌드 설정을 변경하지 않는 한 `site/pages.json`, `.github-pages.json`, `.github/pages_build.py` 등을 수정할 필요는 없습니다.

## 5. GitHub Actions 자동 배포 방법 (P57)

이 프로젝트는 `main` 브랜치에 새로운 커밋이 push되면 GitHub Actions를 통해 자동으로 빌드 및 배포되도록 구성되어 있습니다.

### 5.1. 파일 수정

VS Code 등의 편집기를 사용하여 필요한 파일을 수정하고 저장합니다.

예를 들어 새로운 학습 기록을 작성하려면 `site/content/writing/` 폴더에 Markdown 파일을 추가합니다.

### 5.2. 변경 파일 확인

저장소 최상위 폴더에서 Git Bash를 실행하고 다음 명령어를 입력합니다.

```bash
git status
```

### 5.3. 변경 사항 커밋

```bash
git add -A
git commit -m "Update portfolio content"
```

실제 수정 내용에 따라 커밋 메시지를 구체적으로 작성합니다.

### 5.4. main 브랜치에 push

```bash
git push origin main
```

push가 완료되면 `.github/workflows/hugo-pages.yml`에 정의된 워크플로가 자동으로 실행됩니다.

### 5.5. GitHub Actions 확인

다음 페이지에 접속합니다.

https://github.com/seongmin-vae/portfolio.assignment/actions

`Deploy Hugo to GitHub Pages` 워크플로의 최신 실행을 선택한 뒤 다음 두 작업을 확인합니다.

- **build:** Hugo 정적 사이트 빌드 및 배포 파일 생성
- **deploy:** GitHub Pages에 생성 결과물 게시

두 작업이 모두 성공했는지 확인합니다.

오류가 발생하면 실패한 작업을 클릭하여 로그를 확인하고, 원인을 수정한 후 다시 commit 및 push합니다.

### 5.6. 공개 웹사이트에서 변경 사항 확인

배포가 성공하면 다음 주소에 접속합니다.

https://seongmin-vae.github.io/portfolio.assignment/

수정한 내용이 실제 공개 화면에 반영되었는지 확인합니다.

변경 사항이 보이지 않으면 브라우저에서 `Ctrl + Shift + R`을 눌러 강력 새로고침하거나 시크릿 창에서 확인합니다.

소개, 경력, 프로젝트, 게시글 등의 메뉴가 정상적으로 이동하는지도 확인합니다.

## 6. 최종 커밋 및 배포 버전 확인

현재 GitHub 원격 저장소의 `main` 브랜치 최신 커밋 SHA는 다음 명령어로 확인할 수 있습니다.

```bash
git ls-remote origin refs/heads/main
```

로컬 저장소에서 현재 체크아웃된 커밋은 다음과 같이 확인합니다.

```bash
git rev-parse HEAD
```

최종 제출 보고서에는 원격 `main`의 전체 SHA와 해당 커밋 URL, 대응되는 Actions 실행 URL 및 상태를 기록합니다.

## 7. 사용 테마 및 출처

- **테마:** [Hugo Celadon](https://themes.gohugo.io/themes/hugo-celadon/)
- **테마 원본:** https://github.com/Yajie-Xu/hugo-celadon
- **정적 사이트 생성기:** https://gohugo.io/
- **배포 플랫폼:** https://pages.github.com/
- **배포 준비:** 수업에서 제공한 `prepare_github_pages.py` v3.1
- **테마 라이선스:** MIT License

원본 테마의 라이선스와 저작자 고지를 유지합니다.

사이트 내 콘텐츠는 개인이 직접 작성하거나 수정한 내용이며, 외부 자료 및 AI 생성 자료를 사용한 경우 해당 자료의 출처와 사용 목적을 별도로 표시합니다.
