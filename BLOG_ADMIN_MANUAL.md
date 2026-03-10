# GitHub Blog 관리자 실전 매뉴얼 (초보자용)

이 문서는 현재 저장소 구조를 기준으로 작성된 운영 매뉴얼입니다.

대상:
- 웹 개발 비전공자
- HTML/CSS/Jekyll/GitHub Pages 초보자
- GitHub 블로그를 처음 운영하는 사람

목적:
- 블로그를 혼자 유지보수할 수 있도록 만들기
- "무엇을 바꿀 때 어떤 파일을 수정하는지" 즉시 찾기
- 실수 없이 수정하고 복구하는 방법 익히기

---

## 1) 이 블로그의 기본 구조

현재 저장소 핵심 구조:

```text
github_blog
├ .github/workflows/jekyll-gh-pages.yml
├ _config.yml
├ _data/navigation.yml
├ _includes/head/custom.html
├ _pages/
│  ├ about.md
│  ├ categories.md
│  ├ portfolio.md
│  └ projects.md
├ _posts/
├ assets/css/main.scss
├ images/
├ projects/README.md
├ templates/post-template.md
├ index.md
└ README.md
```

파일/폴더 역할:

| 파일/폴더 | 역할 | 바꾸면 어디가 바뀌나 |
|---|---|---|
| `_config.yml` | 블로그 전체 설정(제목, 설명, URL, 테마, 작성자 등) | 사이트 전역(헤더, 메타 정보, 기본 레이아웃) |
| `_data/navigation.yml` | 상단 메뉴 항목 | 상단 네비게이션 메뉴 |
| `index.md` | 홈 화면 내용 | 메인(첫 화면) 본문 |
| `_pages/about.md` | 소개 페이지 | `/about/` 페이지 |
| `_pages/categories.md` | 카테고리 목록 페이지 | `/categories/` 페이지 |
| `_pages/projects.md` | 프로젝트 요약 페이지 | `/projects/` 페이지 |
| `_pages/portfolio.md` | 포트폴리오 로드맵 페이지 | `/portfolio/` 페이지 |
| `_posts/*.md` | 블로그 글 본문 | 각 포스트 페이지 + 홈 목록 |
| `templates/post-template.md` | 글 템플릿 | 새 글 작성 시 복붙용 기준 |
| `_includes/head/custom.html` | 공통 head 커스텀(MathJax 등) | 수식 렌더링/공통 스크립트 |
| `assets/css/main.scss` | 스타일(CSS) 커스텀 | 색상, 간격, 폰트 등 디자인 |
| `images/` | 포스트 이미지 저장 폴더 | 글 내부 이미지 표시 |
| `.github/workflows/jekyll-gh-pages.yml` | GitHub Pages 자동 배포 | push 후 빌드/배포 동작 |

---

## 2) "무엇을 바꿀 때 어디를 수정?" 빠른 표

아래 표는 실무에서 가장 많이 하는 변경 기준입니다.

| 변경하고 싶은 것 | 수정 파일 | 수정 위치 | 수정 예시 | 반영 결과 | 주의사항 |
|---|---|---|---|---|---|
| 블로그 제목 | `_config.yml` | `title:` | `title: "My Robot Blog"` | 브라우저 제목/사이트 전역 제목 | 큰따옴표 유지 권장 |
| 소개글(사이트 설명) | `_config.yml` | `description:` | `description: "ROS2 and robotics notes"` | SEO 설명/메타 정보 | 너무 길면 검색 결과에서 잘림 |
| 메뉴 바꾸기 | `_data/navigation.yml` | `main:` 아래 항목 | `- title: "About"` `url: /about/` | 상단 메뉴 즉시 변경 | `url` 끝 슬래시(`/`) 유지 |
| 프로필 정보 | `_config.yml` | `author:` 블록 | `name`, `bio`, `links` 수정 | 글 우측/프로필 영역 표시 | 들여쓰기(공백) 틀리면 빌드 실패 |
| 홈 화면 문구 | `index.md` | Front matter 아래 본문 | 홈 소개 문장 수정 | 메인 화면 텍스트 변경 | `---` 구분선 유지 |
| 새 글 작성 | `_posts/` | 새 파일 생성 | `2026-03-11-my-post.md` | 홈 목록+개별 글 생성 | 파일명 날짜 형식 필수 |
| 카테고리 추가 | 포스트 파일 | `categories: [...]` | `categories: [Robot Control]` | 카테고리 페이지에 분류 | 오타 나면 새 카테고리로 분리됨 |
| 태그 추가 | 포스트 파일 | `tags: [...]` | `tags: [ros2, qos]` | 태그 분류/검색 보조 | 태그 표기는 일관성 유지 |
| 이미지 삽입 | `images/` + 포스트 | 본문 markdown | `![설명](/github_blog/images/a.png)` | 글에 이미지 출력 | 경로에 `baseurl` 포함 |
| 코드 블록 | 포스트 | 본문 markdown | <code>```python ... ```</code> | 문법 하이라이트 | 백틱 3개 정확히 닫기 |
| 수식 넣기 | 포스트 | 본문 markdown | `$a+b$`, `$$...$$` | MathJax 렌더링 | `_includes/head/custom.html` 유지 필요 |
| 테마 색상 | `assets/css/main.scss` | CSS 규칙 추가 | `body { background:#0f1115; }` | 디자인/색감 변경 | 과도한 변경 전 백업 커밋 |
| favicon 바꾸기 | `images/` + `_config.yml` | 아이콘 파일/설정 | `_config.yml`에 `favicon: "/github_blog/images/favicon.ico"` | 브라우저 탭 아이콘 변경 | 파일 경로 정확히 |
| About 수정 | `_pages/about.md` | 본문 | 경력/학습 계획 수정 | 소개 페이지 변경 | 페이지 front matter 유지 |

---

## 3) 초보자 기준 작업 순서

### A. 글 작성 순서
1. `templates/post-template.md`를 복사
2. `_posts/`에 `YYYY-MM-DD-title.md` 이름으로 저장
3. 맨 위 `title/date/categories/tags` 수정
4. 본문 작성
5. 저장 후 커밋/푸시

### B. 이미지 넣는 순서
1. 이미지 파일을 `images/`에 저장
2. 포스트 본문에 markdown 삽입
3. 예시:

```md
![2-link simulation](/github_blog/images/2link-sim.png)
```

4. 커밋/푸시 후 페이지에서 깨짐 여부 확인

### C. 메뉴 수정 순서
1. `_data/navigation.yml` 열기
2. `main:` 아래 메뉴 항목 추가/수정/삭제
3. 저장 후 커밋/푸시
4. 상단 메뉴 링크 동작 확인

### D. 설정 파일 수정 순서
1. `_config.yml` 수정 전 백업 커밋
2. 한 번에 한 항목만 수정
3. 커밋 메시지 명확히 작성
4. 푸시 후 Actions 빌드 성공 여부 확인

### E. 수정 후 GitHub 반영 순서
1. 로컬 수정
2. `git add .`
3. `git commit -m "설명"`
4. `git push`
5. GitHub Actions 성공 확인
6. 사이트 새로고침(강력 새로고침 권장)

---

## 4) 실수 방지 가이드

함부로 수정 금지(주의):
- `.github/workflows/jekyll-gh-pages.yml`  
  배포 파이프라인이므로 의미를 모르면 수정 금지
- `_config.yml`의 들여쓰기 구조  
  YAML 문법 오류 시 빌드 실패
- `.git/` 폴더  
  절대 수동 수정 금지

수정 전 백업 방법:

```bash
git checkout -b backup/2026-03-11-before-config
```

또는 최소한 커밋:

```bash
git add .
git commit -m "backup: before editing config"
```

잘못 수정했을 때 복구:

파일 1개만 원복:

```bash
git restore _config.yml
```

최근 커밋만 되돌리기(기록 남김):

```bash
git revert HEAD
git push
```

좋은 커밋 메시지 예시:
- `post: add ros2 qos notes`
- `config: update blog title and description`
- `nav: add portfolio menu`
- `style: improve code block readability`

---

## 5) 자주 하는 작업 매뉴얼

### 5-1. 새 글 작성
1. `templates/post-template.md` 복사
2. `_posts/2026-03-11-ros2-qos.md` 생성
3. front matter 채우기
4. 본문 작성 후 push

### 5-2. 기존 글 수정
1. 해당 파일 열기 (`_posts/...`)
2. 본문/태그/카테고리 수정
3. commit/push

### 5-3. 이미지 추가
1. `images/`에 파일 업로드
2. 포스트 본문에 이미지 링크 삽입
3. push 후 이미지 출력 확인

### 5-4. 카테고리 정리
1. 관련 포스트의 `categories:` 값 통일
2. 대소문자/띄어쓰기 일관성 유지
3. `/categories/` 페이지 확인

### 5-5. 소개 페이지 수정
1. `_pages/about.md` 수정
2. 경력, 학습 로드맵, 연락처 갱신

### 5-6. 네비게이션 메뉴 수정
1. `_data/navigation.yml` 수정
2. 새 페이지가 있으면 메뉴에 추가

### 5-7. push 후 반영 확인
1. GitHub 저장소 > Actions
2. 최근 run 성공(초록 체크) 확인
3. `https://seokeon.github.io/github_blog/` 접속

---

## 6) Markdown 빠른 문법

제목:

```md
# 대제목
## 중제목
### 소제목
```

본문/강조:

```md
일반 문장
**굵게**
*기울임*
```

코드 블록:

```md
```python
print("hello")
```
```

이미지:

```md
![설명](/github_blog/images/sample.png)
```

링크:

```md
[내 깃허브](https://github.com/SeoKeon)
```

표:

```md
| 항목 | 값 |
|---|---|
| 언어 | Python |
```

체크리스트:

```md
- [x] ROS2 설치
- [ ] tf2 실습
```

인용문:

```md
> 핵심 개념 요약
```

수식:

```md
인라인: $a^2 + b^2 = c^2$

블록:
$$
T = A \cdot B
$$
```

---

## 7) GitHub 업로드 워크플로우 (로컬 -> 배포)

로컬에서 수정 후:

```bash
git add .
git commit -m "post: add 2-link IK notes"
git push
```

반영 확인:
1. GitHub `Actions` 탭
2. 워크플로우 성공 확인
3. 사이트 접속 후 변경점 확인

---

## 8) 로봇 엔지니어 포트폴리오 운영 추천 방식

카테고리 운영(추천):
- `Robot Math`: 수학 개념/증명/짧은 코드 검증
- `Robot Kinematics`: FK/IK, Jacobian, singularity
- `ROS2`: 노드, 토픽, QoS, tf2 실습
- `Robot Control`: PID, state-space, 필터, 안정화
- `Robot Projects`: 완성형 프로젝트 글
- `Study Log`: 주간 회고, 학습 계획/정리

공부 기록 vs 포트폴리오 글 구분:
- 공부 기록(`Study Log`): 짧고 자주, 시행착오 중심
- 포트폴리오(`Robot Projects`): 길고 구조화, 결과/수치/링크 중심

프로젝트 글 권장 템플릿:
1. Problem
2. System Architecture
3. Math/Control Background
4. Implementation
5. Result (이미지/그래프/영상)
6. GitHub Repo Link
7. Lessons Learned

---

## 처음 운영할 때 가장 자주 쓰는 수정 작업 TOP 10

1. 새 글 작성: `_posts/`
2. 글 카테고리/태그 수정: 포스트 front matter
3. 홈 소개 문구 변경: `index.md`
4. About 업데이트: `_pages/about.md`
5. 메뉴 항목 수정: `_data/navigation.yml`
6. 이미지 추가/교체: `images/`
7. 사이트 제목/설명 변경: `_config.yml`
8. 수식 표시 점검: `_includes/head/custom.html`
9. 스타일 미세 조정: `assets/css/main.scss`
10. 배포 상태 확인: `.github/workflows/jekyll-gh-pages.yml` + Actions 탭

---

필요하면 다음 단계로 `BLOG_ADMIN_MANUAL.md`를 더 쪼개서
- `01-basic.md`
- `02-daily-ops.md`
- `03-troubleshooting.md`
형태로 분리해 관리할 수 있습니다.
