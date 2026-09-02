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
| 개발자명 | `Nursing XR` — Play 콘솔의 개발자 이름과 **문자열이 일치**해야 합니다 |
| 개인정보 보호책임자 | `Jacob Kim` (제14조) |
| 문의 이메일 | `ped.simulation@gmail.com` (머리말·제9조·제14조·바닥글 4곳) |
| 공고일 / 시행일 | `2026년 9월 2일` — 실제 공개일과 다르면 `index.html` 안 4곳을 고치세요 |

### 백엔드와 대조가 필요한 값

방침에 적은 아래 두 가지는 `mt-app` 백엔드를 직접 확인하지 못하고 통상값으로 기재했습니다.
**방침 내용이 실제 동작과 다르면 그 자체가 위반**이므로 한 번 대조해 주세요.

- **보유 기간** (제5조) — 문의 내역 1년, 서버 접속 로그 3개월로 명시
- **비밀번호 일방향 암호화** (제12조) — bcrypt/argon2 등으로 해시 저장하는지

## 2. GitHub Pages 배포

### 최초 1회 — 사람이 눌러야 하는 스위치

**Settings → Pages → Build and deployment → Source 를 `GitHub Actions` 로 변경**

Pages 를 처음 켜는 것은 저장소 관리자 권한이 필요해서 워크플로의 `GITHUB_TOKEN` 으로는 못 합니다
(`Create Pages site failed. Error: Resource not accessible by integration`).
이 스위치만 한 번 바꾸면 그 뒤로는 손댈 일이 없습니다.

### 그 다음부터는 자동

`.github/workflows/deploy-pages.yml` 이 **기본 브랜치** 푸시마다 배포합니다.
게시되는 파일은 `index.html` 하나이고, README 와 `docs/` 는 저장소 문서라 사이트에 올라가지 않습니다.

```
https://nursingxr.github.io/med-vocab-policy/
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
- [ ] 제14조에 `Jacob Kim` / `ped.simulation@gmail.com` 이 보인다

## 3. Play 콘솔 등록 위치

| 콘솔 항목 | 값 |
|---|---|
| 앱 콘텐츠 → **개인정보처리방침** | `https://nursingxr.github.io/med-vocab-policy/` |
| 스토어 등재정보 → 개인정보처리방침 URL | 위와 동일 |
| 앱 콘텐츠 → **데이터 안전** | `docs/play-data-safety.md` 참고 |
| 앱 콘텐츠 → **계정 삭제 요청 URL** | 아래 4번 참고 |

---

## 4. 남은 과제 — 계정 삭제 경로 (Play 정책 필수)

Google Play는 **앱 안에서 계정을 만들 수 있는 앱**에 대해 두 가지를 모두 요구합니다.

1. **앱 내 계정 삭제 경로** — 현재 `med-vocab` 앱의 *설정* 화면에는 탈퇴 메뉴가 없습니다. (미구현)
2. **웹에서 접근 가능한 계정 삭제 요청 URL** — 로그인 없이 열리는 페이지여야 합니다.

이 방침의 **제9조**는 이메일 기반 삭제 요청 절차를 명시하고 있어 *방침 문서로서의* 요건은 충족하지만,
위 1·2번은 별도 작업입니다. 백엔드에 `DELETE /auth/me` 계열 엔드포인트를 추가하고
설정 화면에 "회원 탈퇴"를 붙이는 것이 정석이며, 그전까지는 최소한 2번(삭제 요청 전용 페이지)을
이 저장소에 추가해 콘솔에 등록해야 심사에서 지적받지 않습니다.
