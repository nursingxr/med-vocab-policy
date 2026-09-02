# med-vocab-policy

Nursing XR(`com.nursingxr.med_vocab`) 앱의 **개인정보처리방침 공개용 저장소**입니다.
Google Play 콘솔에 등록할 공개 URL을 GitHub Pages로 호스팅합니다.

| 파일 | 내용 |
|---|---|
| `index.html` | 개인정보처리방침 본문 (한국어, 반응형, 다크 모드·인쇄 지원, 외부 의존성 없음) |
| `docs/play-data-safety.md` | Play 콘솔 **데이터 안전(Data safety)** 설문 작성용 답변 매핑 |

방침 내용은 `nursingxr/med-vocab` 저장소의 앱 코드(v1.2.12)를 실제로 읽고 작성했습니다.
근거가 된 지점은 `docs/play-data-safety.md`에 코드 위치와 함께 정리해 두었습니다.

---

## 1. 기재 정보

| 항목 | 값 |
|---|---|
| 개인정보처리자 | 주식회사 널싱엑스알 (사업자등록번호 `524-81-02626`) |
| 본사 | 충청남도 아산시 배방읍 희망로 46번길, 충남콘텐츠기업지원센터 403호 |
| 기업부설연구소 | 서울특별시 성동구 왕십리로 222, 한양대학교 융합교육관 901호 |
| 개인정보 보호책임자 | `Jacob Kim` (제14조) |
| 문의 이메일 | `young@nursing-xr.com` |
| 앱 개발자명 (Play 콘솔) | Play 콘솔의 개발자 이름과 **문자열이 일치**해야 합니다 |
| 공고일 / 시행일 | `2026년 9월 2일` — 실제 공개일과 다르면 `index.html` 안 4곳을 고치세요 |

### 아직 비어 있는 항목 — `class="todo"` 로 검색

| 위치 | 항목 |
|---|---|
| 제7조 위탁 표 | **AI 제공사 법인명** — 예: `OpenAI, L.L.C.` / `Anthropic PBC` / `Google LLC` |
| 제7조 위탁 표 | **제공사 API 데이터 보존 정책 URL** — 예: `https://openai.com/policies/…` |

`mt-app` 백엔드가 어느 제공사의 API를 호출하는지 확인해서 채우세요.
「개인정보 보호법」상 국외 이전은 **수탁자를 특정**해야 하므로 "생성형 AI 모델 제공사" 같은
포괄 표현으로는 부족합니다.

### 백엔드와 대조가 필요한 값

- **보유 기간** (제5조) — 문의 내역 1년, 서버 접속 로그 3개월로 명시
- **비밀번호 일방향 암호화** (제12조) — bcrypt/argon2 등으로 해시 저장하는지
- **계정 삭제 엔드포인트** — 제9조가 앱 내 삭제를 주 경로로 안내합니다.
  `DELETE /auth/me` 계열 엔드포인트가 백엔드에 있어야 문구가 사실이 됩니다.

## 2. GitHub Pages 배포

### 최초 1회 — 사람이 눌러야 하는 스위치

**Settings → Pages → Build and deployment → Source 를 `GitHub Actions` 로 변경**

Pages 를 처음 켜는 것은 저장소 관리자 권한이 필요해서 워크플로의 `GITHUB_TOKEN` 으로는 못 합니다
(`Create Pages site failed. Error: Resource not accessible by integration`).
이 스위치만 한 번 바꾸면 그 뒤로는 손댈 일이 없습니다.

### 그 다음부터는 자동

`.github/workflows/deploy-pages.yml` 이 **기본 브랜치** 푸시마다 배포합니다.
게시되는 파일은 아래 두 개이고, README 와 `docs/` 는 저장소 문서라 사이트에 올라가지 않습니다.

```
https://nursingxr.github.io/med-vocab-policy/                      (개인정보처리방침)
https://nursingxr.github.io/med-vocab-policy/delete-account.html   (계정 삭제 요청)
```

> **기본 브랜치를 `main` 으로 바꿔 두세요** (Settings → General → Default branch).
> Source 를 `GitHub Actions` 로 지정하면 GitHub 이 `github-pages` 환경을 만드는데,
> 이 환경은 **기본 브랜치에서 출발한 배포만 허용**합니다.
> 워크플로에 `if: github.ref_name == github.event.repository.default_branch` 를 걸어 두었으므로
> 기본 브랜치가 아닌 곳에서는 조용히 건너뛰고, 기본 브랜치를 바꿔도 워크플로는 손댈 필요가 없습니다.
> (이 가드가 없으면 스텝을 하나도 밟지 못한 채 실패합니다 — Actions 로그에 스텝이 안 찍히면 그 증상입니다.)

### 배포 후 자가 점검

- [ ] 시크릿 창(로그아웃 상태)에서 URL이 열린다 — Google 심사자는 비로그인 상태로 접근합니다
- [ ] 모바일 화면에서 가로 스크롤 없이 읽힌다
- [ ] 페이지 제목에 "개인정보처리방침"이 보인다
- [ ] 제14조에 `Jacob Kim` / `young@nursing-xr.com` / 사업자등록번호가 보인다
- [ ] `delete-account.html` 이 로그인 없이 열린다

## 3. Play 콘솔 등록 위치

| 콘솔 항목 | 값 |
|---|---|
| 앱 콘텐츠 → **개인정보처리방침** | `https://nursingxr.github.io/med-vocab-policy/` |
| 스토어 등재정보 → 개인정보처리방침 URL | 위와 동일 |
| 앱 콘텐츠 → **데이터 안전** | `docs/play-data-safety.md` 참고 |
| 앱 콘텐츠 → **앱 액세스** · 스토어 등재정보 문안 | `med-vocab` 저장소의 `docs/play-console-listing.md` |
| 앱 콘텐츠 → **계정 삭제 요청 URL** | `https://nursingxr.github.io/med-vocab-policy/delete-account.html` |

---

## 4. 남은 과제 — 앱 내 계정 삭제 기능

Google Play(데이터 안전 · 계정 삭제 요청 URL)와 App Store 심사 가이드라인 5.1.1(v)는
계정 생성이 가능한 앱에 **앱 내 삭제 기능**을 요구합니다.

- **웹 삭제 요청 URL** — `delete-account.html` 로 해결. 로그인 없이 열립니다. ✅
- **앱 내 삭제 UI** — `med-vocab` 저장소에 구현했습니다 (설정 > 계정 > 계정 삭제, 비밀번호 재확인).
- **백엔드 엔드포인트** — ⚠️ **아직 없습니다.** `mt-app` 에 `DELETE /auth/me` 계열이 들어가야
  앱 내 삭제가 실제로 동작하고, 제9조 문구가 사실이 됩니다.
  이 저장소의 방침을 **공개 배포하기 전에** 백엔드부터 확인하세요.
