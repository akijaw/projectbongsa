# 멘토링 연구 프로젝트 — 옥쌤과 아이들

중학생 대상 바이브 코딩 입문 멘토링 자료 모음입니다. 아래 순서대로 진행하도록 설계되어 있어요.

## 파일 구성

| 파일 | 용도 | 형식 |
|---|---|---|
| `OT_바이브코딩.pptx` | 오프라인 오리엔테이션용 발표 슬라이드 (7장) | PowerPoint |
| `mentoring_site.html` | "규칙이 왜 중요한지" 개념을 체험하는 데모 사이트 (STEP1~3) | 순수 HTML/CSS/JS |
| `study_site_full_guide.html` | 이름·과목·사이트종류를 고르면 실제 제작 프롬프트를 안내하는 실습 가이드 (STEP1~6) | 순수 HTML/CSS/JS |

**둘 다 외부 라이브러리/빌드 과정이 필요 없습니다.** 파일을 더블클릭해서 브라우저로 열면 바로 실행되고, 코드를 수정한 뒤에도 저장하고 새로고침만 하면 바로 반영돼요.

## 진행 순서 (제안)

1. `OT_바이브코딩.pptx`로 오프닝
2. `mentoring_site.html`에서 개념 체험 (규칙 실험실 → 비교 체험 → 나만의 규칙)
3. `study_site_full_guide.html`에서 실제 제작 (이름/과목/종류 선택 → STEP1~5 프롬프트 실습 → STEP6 배포)

## `study_site_full_guide.html` 구조 (수정 이어받을 사람은 여기부터 읽으세요)

파일 안에 크게 두 화면이 있어요.

- `#selectScreen` — 이름 입력 + 과목(물리/화학/생명과학/지구과학/정보) + 사이트 종류(암기카드/문제풀이/오답노트/공부계획+타이머) 선택
- `#guideScreen` — 선택한 조합에 맞춰 STEP1~6이 채워지는 화면

콘텐츠는 JS의 두 데이터 객체가 전부 관리합니다. 코드 안에 상세 주석을 달아뒀어요.

```js
const SUBJECTS = { physics: {...}, chemistry: {...}, ... }  // 과목별 콘텐츠
const TYPES    = { flashcard: {...}, quiz: {...}, ... }     // 사이트 종류별 프롬프트
```

**새 과목을 추가하고 싶다면** → `SUBJECTS`에 항목 추가 + `<div class="subject-grid">`에 카드 하나 추가
**새 사이트 종류를 추가하고 싶다면** → `TYPES`에 항목 추가 + `startGuide()` 안의 분기(`if(pickedType === ...)`)에 미리보기 로직 추가 + `<div class="type-grid">`에 카드 하나 추가

디자인 토큰(색상 등)은 파일 상단 `:root` CSS 변수에 모여 있어요. 과목을 고르면 `--accent`/`--accent-light`가 JS로 바뀌면서 테마 색이 바뀌는 구조입니다.

## 배포 (STEP6에서 학생들에게 안내하는 방법)

완성한 HTML 파일을 [Netlify Drop](https://app.netlify.com/drop)에 드래그하면 회원가입 없이 즉시 실제 URL이 생성됩니다. 이 저장소의 파일을 실제로 배포하고 싶다면 팀 차원에서는 GitHub Pages를 쓰는 것도 방법이에요 (아래 참고).

## 함께 작업하기 (Git)

이 폴더는 git 저장소로 초기화되어 있어요. 팀원이 이어서 작업하려면:

1. 이 폴더 전체를 압축 파일로 받거나, GitHub 저장소로 올려서 공유
2. GitHub에 올리는 경우:
   ```bash
   git remote add origin <팀 저장소 주소>
   git push -u origin main
   ```
3. 이후로는 각자 수정하고 `git add . && git commit -m "설명" && git push`로 반영
4. 충돌 없이 함께 작업하려면 기능별로 브랜치를 나눠서 작업하는 걸 추천해요 (예: `feature/새과목-추가`)

## 오늘까지의 변경 이력

`git log`로 지금까지의 작업 단위를 확인할 수 있어요.
