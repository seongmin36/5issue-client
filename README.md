# 5issue-client

**신선식품 커머스 모바일 웹 — Next.js 16 App Router 프론트엔드**

## 소개

사용자의 장보기 흐름을 홈에서 결제·주문 조회까지 한 앱 안에서 끝내는 모바일 우선 PWA입니다.

- **카카오·네이버 소셜 로그인**으로 시작
- **홈**(히어로 배너·추천 구좌) **· 검색 · 상품 · 장바구니 · 주문서 · 마이페이지**로 쇼핑 흐름을 구성
- **주문, 배송지, 취소·반품·교환, My냉장고·레시피**(AI 추천)를 마이페이지에서 이어서 관리
- **토스페이먼츠**로 결제수단 선택부터 승인까지 연결
- **PWA**로 앱에 가까운 실행과 기본 오프라인 셸을 제공

> 프론트엔드 2인(+백엔드·AI·디자인 파트) 팀 프로젝트입니다. 서비스 자체는 운영 비용 문제로 중단했고, **[컴포넌트 카탈로그(Chromatic)](https://develop--6a978509faf77cfdcaeb125d.chromatic.com/)** 는 지금도 열람할 수 있습니다.

## 기여 범위 — [seongmin36](https://github.com/seongmin36)

경쟁사 기준선 측정부터 병목 분석, 개선, 측정 방법론 검증까지 **성능 과제 전반을 주도**했습니다. 아래 표가 직접 코드를 작업한 항목입니다.

| README 섹션 | 작업                                                           | PR                             |
| ----------- | -------------------------------------------------------------- | ------------------------------ |
| 3-1         | 인증 401 재시도 루프 차단 — in-flight 프로미스로 동시 재발급 합치기 | [#123](https://github.com/5issue/total-client/pull/123)                 |
| 3-2         | Pretendard 자체 호스팅 → TTF에서 WOFF2로 전환 (6.7MB → 2.06MB)  | [#122](https://github.com/5issue/total-client/pull/122), [#168](https://github.com/5issue/total-client/pull/168) |
| 3-3         | Critical CSS 인라인 — 렌더링 차단 450ms → 0ms                   | [#168](https://github.com/5issue/total-client/pull/168)                 |
| 3-4         | 외부 SDK 라우트 분리·지연 로드, 시트 지연 마운트               | [#123](https://github.com/5issue/total-client/pull/123), [#73](https://github.com/5issue/total-client/pull/73), [#194](https://github.com/5issue/total-client/pull/194) |
| 3-5         | 히어로 배너 LCP `fetchPriority` 명시 + `preload` 복귀           | [#165](https://github.com/5issue/total-client/pull/165), [#188](https://github.com/5issue/total-client/pull/188) |
| 3-7         | 이미지 포맷 협상(AVIF·WebP) + CDN 도메인 화이트리스트 등록      | [#157](https://github.com/5issue/total-client/pull/157)                 |
| 3-8         | Lighthouse 측정 방법론 검증 — Lantern 시뮬레이션 아티팩트 규명  | 측정·분석                      |

표에 없는 **3-6**(종횡비 토큰)과 3-4의 서버 컴포넌트 구조는 팀원 [dew2314](https://github.com/dew2314) 작업입니다 — 측정 결과에 영향을 주는 부분이라 본문에는 남기되, 해당 섹션에 작업자를 표시해 뒀습니다.

## 기술 스택

| **분류**      | **기술**                                                                                                                                                                                                                                                                                                                           | **선정 이유**                                                                 |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| Framework     | <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=next.js&logoColor=white">                                                                                                                                                                                                                           | App Router에서 화면, RSC, Route Handler(BFF)를 한 프레임워크로 관리           |
| Library       | <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=React&logoColor=white">                                                                                                                                                                                                                               | 컴포넌트 단위로 홈·상품·장바구니·결제 UI를 조합                               |
| Language      | <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white">                                                                                                                                                                                                                     | API 응답·폼·상태를 컴파일 타임에 고정                                         |
| Styling       | <img src="https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white">                                                                                                                                                                                                                  | Tailwind v4 CSS-first. 디자인 토큰은 `src/styles/tokens`가 소스               |
| State         | <img src="https://img.shields.io/badge/TanStack_Query-FF4154?style=for-the-badge&logo=reactquery&logoColor=white"> <img src="https://img.shields.io/badge/Zustand-433E38?style=for-the-badge">                                                                                                                                     | 서버 상태는 Query, 화면 UI 상태만 Zustand. 서버 응답을 스토어에 복사하지 않음 |
| Validation    | <img src="https://img.shields.io/badge/Zod-3E67B1?style=for-the-badge&logo=zod&logoColor=white">                                                                                                                                                                                                                                   | 외부 응답과 폼을 같은 스키마로 검증                                           |
| Form          | <img src="https://img.shields.io/badge/React_Hook_Form-EC5990?style=for-the-badge&logo=reacthookform&logoColor=white">                                                                                                                                                                                                             | 회원가입·배송지·주문서 입력                                                   |
| Auth          | <img src="https://img.shields.io/badge/Kakao-FFCD00?style=for-the-badge&logo=kakaotalk&logoColor=000000"> <img src="https://img.shields.io/badge/Naver-03C75A?style=for-the-badge&logo=naver&logoColor=white">                                                                                                                     | OAuth는 BFF가 처리. Access Token은 메모리, Refresh Token은 HttpOnly 쿠키      |
| Payment       | <img src="https://img.shields.io/badge/Toss_Payments-0064FF?style=for-the-badge">                                                                                                                                                                                                                                                  | API 개별 연동 키로 자체 결제수단 UI 유지                                      |
| PWA           | <img src="https://img.shields.io/badge/Serwist-5A0FC8?style=for-the-badge">                                                                                                                                                                                                                                                        | 서비스 워커·웹 앱 매니페스트                                                  |
| Test          | <img src="https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge&logo=playwright&logoColor=white"> <img src="https://img.shields.io/badge/Vitest-6E9F18?style=for-the-badge&logo=vitest&logoColor=white"> <img src="https://img.shields.io/badge/Storybook-FF4785?style=for-the-badge&logo=storybook&logoColor=white"> | E2E, 유닛, 컴포넌트 카탈로그(Chromatic)                                       |
| Quality       | <img src="https://img.shields.io/badge/ESLint-4B32C3?style=for-the-badge&logo=eslint&logoColor=white"> <img src="https://img.shields.io/badge/Prettier-F7B93E?style=for-the-badge&logo=prettier&logoColor=black">                                                                                                                  | 커밋 전 스타일·린트 통일                                                      |
| Delivery      | <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white"> <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white">                                                                                                              | `output: "standalone"` 이미지와 k8s 매니페스트 예시                           |
| Collaboration | <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white"> <img src="https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white">                                                                                                                        | 브랜치 `develop`, Conventional Commits, Figma 토큰은 CSS에 수동 반영          |

## 핵심 설계

### 1. BFF

브라우저는 Spring·AI를 직접 호출하지 않습니다. `publicFetch` / `privateFetch`가 `/api/**`만 치고, Route Handler가 `API_INTERNAL_URL`·`AI_SERVICE_INTERNAL_URL`로 프록시합니다. 응답은 Zod로 검증한 뒤 `{ statusCode, message, data }` 봉투로 내려줍니다.

### 2. 인증

로그인 URL과 `redirectUri`는 서버가 계산합니다. Refresh Token은 HttpOnly 쿠키, Access Token은 메모리입니다. 앱 부팅 시 `/api/auth/refresh`로 access를 채우고, 이후 401이면 같은 경로로 한 번만 재발급합니다. 동시 호출은 in-flight Promise로 합칩니다.

### 3. 성능

마켓컬리 실측(메인 PNG 2.4MB, LCP 21.6초, TBT 650ms)을 기준으로 잡았습니다. `<img>` 대신 `next/image`(AVIF·WebP), 종횡비 선고정, LCP 후보만 `preload` + `fetchPriority="high"`, CSS 인라인, Pretendard WOFF2 자체 호스팅을 씁니다. 목표는 홈·상품 상세 LCP 2.5초 미만, CLS 0.1 미만, 접근성 95점 이상입니다. 측정값과 개선 내역은 [성능·접근성 최적화](#성능접근성-최적화)에 정리했습니다.

### 4. 디자인 토큰

Figma 변수를 Style Dictionary로 빌드하지 않습니다. `src/styles/tokens/color.css`·`typography.css`가 소스이고, 변경 시 MCP로 변수를 다시 읽어 CSS에 1:1로 반영합니다.

## 성능·접근성 최적화

마켓컬리를 벤치마킹하면서, **기존 마켓컬리가 구조적으로 손대지 못한 지점을 우리 코드에서는 어디까지 잡을 수 있는지**를 과제로 잡았습니다. 측정은 전부 모바일 기준 Lighthouse이고, 아래 수치는 저장된 리포트 JSON에서 직접 확인한 값만 적었습니다.

<!-- 요약을 이미지로 바꾸려면 아래 표를 지우고 이 자리에 넣으세요.
     다만 README 최상단 요약은 텍스트를 권장합니다 — 모바일에서 축소돼도 숫자가 읽히고,
     복사·검색·스크린리더가 되며, 깃허브 다크모드에서 흰 배경 이미지가 튀지 않습니다. -->

| 지표        | 마켓컬리 | 개선 후 (시뮬레이션) | 개선 후 (실측) |
| ----------- | -------- | -------------------- | -------------- |
| Performance | 40점     | 78점                 | **98점**       |
| LCP         | 21.6초   | 4.2초                | **1.55초**     |
| TBT         | 650ms    | 60ms                 | 155ms          |
| 접근성      | 76점     | 96점                 | **96점**       |

두 가지를 특히 신경 썼습니다.

- **측정 도구 자체를 의심했습니다.** 개선 후에도 LCP가 14~30초로 요동쳐, Lighthouse 기본 모드(Lantern 시뮬레이션)가 만들어낸 수치 아티팩트임을 `2,057,688B ÷ 184.3KB/s ≈ 10.9초` 산술로 증명하고 측정 방식을 바꿨습니다 → **3-8**
- **성과로 세지 않은 항목을 남겼습니다.** Before/After JSON 대조에서 변화가 확인되지 않은 2건은 개선 목록에서 제외했습니다 → **끝내지 못한 것**

### 최적화 4단계 흐름

<img width="902" height="238" alt="스크린샷 2026-10-08 오전 3 55 18" src="https://github.com/user-attachments/assets/7c8b6c6c-4f54-4f17-9edc-64a07e41d5e0" />

---

### 1단계. 기준선 — 마켓컬리 Lighthouse 측정

벤치마킹 대상의 현재 상태를 먼저 측정해, "우리가 실제로 개선 가능한 항목"과 "비즈니스 제약상 어쩔 수 없는 항목"을 분리했습니다.

<img width="1346" height="725" alt="스크린샷 2026-10-08 오전 4 28 23" src="https://github.com/user-attachments/assets/8ce0cbbf-812c-485d-9bfb-17dfeb29a19b" />

| 항목               | 마켓컬리 메인 측정값 |
| ------------------ | -------------------- |
| Performance        | **40점**             |
| 접근성             | 76점                 |
| 권장사항           | 77점                 |
| SEO                | 85점                 |
| FCP                | 5.1초                |
| LCP                | **21.6초**           |
| TBT                | **650ms**            |
| CLS                | 0.004                |
| Speed Index        | 13.6초               |
| 메인 히어로 이미지 | PNG 2.4MB            |

이미지·레이아웃 안정성·접근성 세 가지 모두 **레거시 코드베이스에서는 비용이 크지만 신규 프로젝트에서는 처음부터 강제할 수 있는** 항목이라고 판단했습니다 — 원본 PNG는 포맷 협상·리사이즈로, 레이아웃 흔들림은 종횡비 토큰으로, 접근성은 기능 변경 없이 토큰과 속성만으로 잡을 수 있습니다.

이 분석이 그대로 기술 스택 선택 근거가 됐습니다 — `next/image`의 포맷 변환·리사이즈와 화면별 렌더링 전략(SSG/ISR)을 쓰려고 Next.js를 선택했습니다.

---

### 2단계. 1차 측정 — 우리 프로젝트 (2026-09-30)

구현이 올라온 뒤 같은 조건으로 우리 서비스를 측정했습니다. 카테고리 점수는 기준선을 앞섰지만(66점 vs 40점), **LCP 41.7초는 기준선 21.6초보다 두 배 가까이 나빴습니다.**

<img width="1519" height="730" alt="스크린샷 2026-10-10 오전 4 41 07" src="https://github.com/user-attachments/assets/fb3b7774-f9d7-4c33-bca4-b2656d6a2b5e" />

| 항목             | 1차 측정값                        | 판정                     |
| ---------------- | --------------------------------- | ------------------------ |
| Performance      | 66점                              | 기준선 40점 대비 +26     |
| LCP              | 41.7초 (41,673ms) + 타임아웃 경고 | 사실상 측정 불가         |
| 폰트 전송량      | 6.7MB (6,747,322B, TTF)           | 전체 전송량의 79%        |
| 렌더링 차단 CSS  | 450ms (66KB 청크, score 0)        | 첫 렌더가 CSS를 기다림   |
| 총 전송량        | 8.70MB / 93건                     | 2차에서 29% 감축         |
| 접근성           | 96점 (color-contrast 실패 요소 37개) | 점수는 양호, 실패는 잔존 |
| 레거시 JS 폴리필 | 43,785B                           | 미해결                   |

---

### 3단계. 코드 개선 — 2차 측정 (2026-10-01 ~ 10-02)

#### 3-1. 인증 재시도 루프 차단 → `src/lib/apiClient.ts`

가장 큰 수치 개선이지만 성능 코드를 고친 게 아닙니다. 401 처리 흐름 자체가 잘못돼 있었습니다.

`privateFetch`를 **401 → 재발급 1회 → 원 요청 1회 재시도**로 고정하고, 재발급이 실패하면 즉시 세션을 정리하고 종료합니다. 재시도가 다시 401을 받아도 루프로 돌아가지 않습니다.

```ts
// src/lib/apiClient.ts
try {
  return parseOrThrow(schema, unwrap(await doFetch()));
} catch (e) {
  if (!(e instanceof ApiError) || e.statusCode !== 401) throw e;

  const refreshed = await tryRefresh();
  if (!refreshed) {
    clearAccessToken();
    throw new ApiError(401, '로그인이 만료되었습니다. 다시 로그인해주세요.');
  }
  return parseOrThrow(schema, unwrap(await doFetch())); // 재시도는 1회뿐
}
```

여기에 **동시 재발급 합치기**가 함께 필요했습니다. `refresh_token`은 서버에서 1회용으로 회전되는데, 페이지 진입 직후 `SessionBootstrap`의 무음 재발급과 `privateFetch`의 401 인터셉터가 같은 틱에 몰립니다(`/cart`에서 실제 재현). 중복 호출하면 먼저 도착한 쪽은 성공하고 뒤따라온 쪽이 "이미 쓴 토큰"으로 거부당하면서, **방금 심어진 새 쿠키를 지워버립니다.** in-flight 프로미스를 공유해 동시 호출을 네트워크 요청 1건으로 합쳤습니다.

```ts
let refreshPromise: Promise<boolean> | null = null;

function tryRefresh(): Promise<boolean> {
  if (refreshPromise) return refreshPromise; // 진행 중이면 그 프로미스를 그대로 돌려줌
  refreshPromise = (async () => {
    /* ... */
  })().finally(() => (refreshPromise = null));
  return refreshPromise;
}
```

> **LCP 41.7초 → 4.2초.** 단, 이 수치는 "41.7초짜리 타임아웃이 사라지고 정상 범위로 돌아왔다"는 방향성으로 읽는 것이 정확합니다 — 두 값 모두 시뮬레이션 모드 측정치이고, 그 신뢰도는 3-8에서 따로 검증했습니다.

#### 3-2. 폰트 TTF → WOFF2 → `src/lib/fonts.ts`

Pretendard는 Google Fonts에 없어 `next/font/google`을 쓸 수 없습니다. `pretendard` npm 패키지의 정적 파일을 `next/font/local`로 직접 로드하는데, 이때 **어느 경로의 파일을 집는지가 전송량을 3배 이상 갈라놓습니다.**

```ts
// src/lib/fonts.ts
export const pretendard = localFont({
  // dist/public/variable/ 의 TTF(6.4MB)가 아니라, 같은 내용을 WOFF2로 압축한 파일(2.0MB)
  src: '../../node_modules/pretendard/dist/web/variable/woff2/PretendardVariable.woff2',
  variable: '--font-pretendard',
  display: 'swap', // 폰트 대기 중 텍스트를 숨기지 않음
  weight: '45 930', // TTF fvar 테이블 실측 범위 — 가변축 하나로 전 굵기 커버
});
```

가변축과 글리프는 동일하고 포맷만 다릅니다. 굵기별 파일을 따로 받지 않고 가변 폰트 하나로 끝내기 때문에 추가 요청도 없습니다.

> **폰트 전송량 6.7MB → 2.06MB (69% 감소).**
>
> 과거에 한 번 되돌린 이력이 있습니다 — 당시 설치된 패키지 버전에 `dist/web/variable/woff2/` 경로가 비어 있어 TTF로 롤백했습니다. 패키지를 올릴 때 이 경로의 파일 존재를 다시 확인해야 합니다(주석으로 남겨둠).

#### 3-3. Critical CSS 인라인 → `next.config.ts`

Next는 기본적으로 CSS를 `<link>`로 내보내고, 브라우저는 그 응답을 받기 전까지 첫 렌더를 하지 못합니다. 1차 측정에서 66KB 청크가 약 450ms를 잡아먹었습니다.

```ts
experimental: {
  inlineCss: true,
}
```

Tailwind 같은 atomic CSS는 페이지가 커져도 **실제로 쓰는 클래스만큼만** CSS가 늘어나기 때문에, 인라인해도 HTML이 과도하게 커지지 않습니다. 프로덕션 빌드에서만 `<style>`로 인라인해 첫 렌더가 CSS 요청을 기다리지 않게 했습니다. 트레이드오프는 명시적으로 선택했습니다 — **신규 방문자의 LCP를 위해 재방문자의 CSS 캐싱 이득을 포기**합니다.

> **렌더링 차단 450ms → 0ms (차단 리소스 0개, score 0 → 1).** Before/After가 가장 깔끔하게 떨어지는 항목입니다.

#### 3-4. 첫 화면에 실리는 JavaScript 제한

마켓컬리의 TBT 650ms는 1단계 리포트에 "초기 번들·서드파티 스크립트가 메인 스레드를 장시간 점유"로 기록돼 있습니다. 같은 항목에서 **60ms**가 나온 건 번들을 튜닝해서가 아니라, **애초에 메인 스레드를 점유할 코드를 첫 화면에 올리지 않았기** 때문입니다. 네 가지가 그 결과를 만듭니다.

- **페이지 셸이 서버 컴포넌트로 남습니다.** 상태가 필요한 구획만 클라이언트 경계로 분리하는 구조로, 홈 화면 API 연동에서 잡혔습니다 — [dew2314](https://github.com/dew2314) 작업([#137](https://github.com/5issue/total-client/pull/137)).
- **서드파티 추적 스크립트가 없습니다.** 애널리틱스·광고 태그·채팅 위젯을 하나도 붙이지 않았고, 런타임 의존성도 11개입니다. 시연 스코프 프로젝트라 가능했던 조건이기도 합니다.
- **외부 스크립트 2개는 쓰는 라우트에서만 로드합니다.** 토스 SDK는 `requestTossPayment.ts` → `CheckoutView` 한 경로뿐이라 홈 번들에 들어가지 않고 결제 시점에 `loadTossPayments()`로 받아옵니다([#123](https://github.com/5issue/total-client/pull/123)). 카카오 우편번호 SDK는 `strategy="afterInteractive"`로 첫 페인트 이후에 붙습니다([#73](https://github.com/5issue/total-client/pull/73)).
- **바텀시트는 데이터가 오기 전까지 마운트하지 않습니다.** `useProductDetail(activeProductId ?? '', activeProductId !== null)`로 쿼리를 `enabled` 게이팅하고 시트도 조건부 렌더라, 첫 렌더에는 시트 트리가 존재하지 않아 하이드레이션 대상에서도 빠집니다([#194](https://github.com/5issue/total-client/pull/194)).

> **TBT 650ms → 60ms.** 마켓컬리 기준선 대비이고, 우리 1차 TBT는 이미 173ms였습니다. 없던 병목을 없앤 게 아니라 **만들지 않은 쪽**에 가깝습니다 — 어느 항목도 TBT를 겨냥해 따로 작업한 게 아니라, 기능 구현 과정에서 내린 선택이 그대로 측정값으로 나타난 경우입니다.

#### 3-5. LCP 이미지 우선순위 → `src/components/organisms/home/HeroBanner/HeroBanner.tsx`

홈의 LCP 후보 1순위는 히어로 배너 이미지입니다. 여기서 두 가지를 바로잡았습니다.

```tsx
<Image
  src={slide.imageSrc}
  alt={slide.imageAlt}
  fill
  preload // Next 16 App Router 의 정식 prop (priority 는 레거시 Pages Router)
  fetchPriority="high" // preload/priority 어느 쪽을 써도 자동으로 붙지 않는 별도 prop
  quality={90}
  sizes="(max-width: 480px) 100vw, 402px"
  className="object-cover"
/>
```

- **`preload` vs `priority`** — 현재 App Router 공식 문서는 LCP 이미지에 `preload`를 쓰라고 안내합니다. `priority`는 레거시 Pages Router 문서에만 남아 있습니다. 이전 PR에서 "`preload`는 존재하지 않는 prop"이라는 전제로 `priority`로 되돌린 적이 있었는데, 조사 결과 그 전제가 틀렸습니다.
- **`fetchPriority`는 별도로 붙여야 합니다.** `next/image` 소스(`get-img-props.ts`)를 확인했더니 `fetchPriority`는 `rest`로 그대로 통과만 되고 lazy 해제 로직과는 무관합니다. 즉 `preload`나 `priority`를 줘도 `fetchpriority` 속성은 자동으로 생기지 않습니다. 배포 사이트의 실제 SSR HTML을 떠서 속성이 없는 것을 확인한 뒤 명시적으로 추가했습니다.

`sizes`로 뷰포트별 필요 폭을 알려주어 과대 이미지 다운로드를 막고, `quality={90}`은 기본 75에서 올린 값입니다("이미지가 뿌옇다"는 리뷰 대응 — 다만 근본 원인은 소스 자산 900×672가 3배율 기기의 이상적 해상도 1,206px에 못 미쳐 업스케일이 불가능한 쪽이라, 자산 교체는 디자인팀 요청으로 남겨뒀습니다).

> **`fetchpriority=high` 적용, `priorityHinted: false` 해소.** 공식 문서와 `next/image` 소스를 직접 확인해 이전 PR의 잘못된 전제를 되돌린 건이기도 합니다.

#### 3-6. CLS 0 — 종횡비 토큰 선고정 → `src/styles/globals.css`

> 이 항목은 [dew2314](https://github.com/dew2314) 작업입니다([#85](https://github.com/5issue/total-client/pull/85)). 측정 결과에 영향을 줘서 함께 적어둡니다.

Figma 실측 종횡비를 토큰으로 선언해, 이미지가 들어가는 자리를 로드 전에 확보합니다.

```css
--aspect-hero-banner: 402 / 298; /* 히어로 배너 (node 577:20652) */
--aspect-product-card: 150 / 240;
```

리스트 썸네일도 같은 규칙이라(`h-21` + `aspect-3/4`) 이미지 도착 전후로 행 높이가 변하지 않고, 측정에서 **CLS 0**으로 나타났습니다.

#### 3-7. 이미지 포맷 협상 → `next.config.ts`

기준선에서 가장 먼저 눈에 띈 항목이 "메인 히어로 이미지 PNG 2.4MB"였습니다. `next/image`에 포맷 협상을 켜두면 브라우저가 지원하는 최신 포맷으로 내려가고, 디바이스 폭에 맞춰 리사이즈됩니다.

```ts
images: {
  formats: ['image/avif', 'image/webp'], // 원본 PNG 대신 포맷 협상
  remotePatterns: [...REMOTE_IMAGE_PATTERNS],
  qualities: [75, 90], // Next 16 은 화이트리스트에 없는 quality 를 빌드에서 차단
}
```

다만 이 설정은 `next/image`를 통과한 이미지에만 걸립니다. 상품 이미지 CDN 두 도메인이 `remotePatterns`에 없어 렌더링 자체가 막혀 있었고(리사이즈 경로가 `/hdims/`·`/shop/`·`/product/`로 제각각), 이를 등록하면서 상품 이미지도 포맷 협상 대상에 들어왔습니다. 목록은 이후 별도 모듈(`src/lib/imageHosts.ts`)로 분리돼 런타임 URL 검증과 공유됩니다 — [dew2314](https://github.com/dew2314) 작업([#173](https://github.com/5issue/total-client/pull/173)).

> **원본 PNG → AVIF·WebP.** 기준선의 2.4MB PNG에 직접 대응하는 항목입니다.

#### 3-8. 측정 방식 자체의 검증 — "LCP 14초"의 정체

개선 후에도 LCP가 로컬 14.3초, 배포 17.6초로 나와 원인을 추적했는데, **코드 문제가 아니라 Lighthouse 기본 모드(Lantern 시뮬레이션)의 산출물**이었습니다. 같은 리포트 안에서 숫자가 두 갈래로 갈립니다.

| 종류                                | LCP 값       | 의미                             |
| ----------------------------------- | ------------ | -------------------------------- |
| `observedLargestContentfulPaint`    | **238ms**    | 트레이스에서 실측된 값           |
| `largestContentfulPaint` (채점용)   | **14,258ms** | Lantern이 느린 4G로 재시뮬레이션 |
| └ `lcpLoadDuration`                 | 11,121ms     | 시뮬레이션상 이미지 다운로드     |

`network-requests` 원본을 보면 원인이 드러납니다.

```
PretendardVariable.woff2    2,057,688 B   priority: High   isLinkPreload: true   시작 32ms
today-deal.webp (LCP 이미지)   20,069 B   priority: High   isLinkPreload: true   시작 32ms
```

폰트와 LCP 이미지가 **정확히 같은 시점에, 똑같이 High 우선순위 preload로** 요청됩니다. throttle 설정이 1,474.56Kbps(≈184.3KB/s)이므로 `2,057,688 B ÷ 184.3KB/s ≈ 10.9초`, `lcpLoadDuration` 11.1초와 거의 일치합니다. 20KB 이미지인데도 2MB 폰트가 같은 파이프를 거의 다 점유한다고 모델링된 결과입니다.

실제 쓰로틀링(`--throttling-method=devtools`)으로 3회 재측정하자 결과가 안정됐습니다.

| 모드                      | 1회          | 2회          | 3회          |
| ------------------------- | ------------ | ------------ | ------------ |
| 기본(Lantern 시뮬레이션)  | 0.72 / 29.9s | 0.72 / 30.1s | 0.67 / 17.6s |
| devtools(실제 쓰로틀링)   | 1.00 / 1.54s | 1.00 / 1.51s | 0.99 / 1.57s |

같은 페이지가 시뮬레이션에서는 17.6~30초로 요동치고, 실제 쓰로틀링에서는 세 번 다 1.5초대로 수렴합니다.

> **측정 방식을 바꿨습니다.** 코드가 아니라 도구가 만든 숫자였고, 이후 성능 판단은 devtools 모드를 기준으로 하되 시뮬레이션 수치는 경쟁사와 같은 조건의 비교용으로만 병기합니다. 리포트 숫자를 그대로 믿었다면 없는 병목을 쫓았을 구간입니다.

#### 2차 측정 결과 정리

3-1 ~ 3-7의 개선을 모두 반영한 뒤 다시 측정한 결과입니다.

<img width="1518" height="717" alt="스크린샷 2026-10-10 오전 4 19 33" src="https://github.com/user-attachments/assets/d454b821-bfcd-4061-90cf-1b4cac7fefb5" />

---

### 4단계. 마켓컬리 대비 최종 결과

<img width="1290" height="677" alt="스크린샷 2026-10-08 오전 4 37 29" src="https://github.com/user-attachments/assets/5fd1d6ae-1cda-48c1-82a8-eda3b7c6666b" />

시뮬레이션 축은 **경쟁사와 동일한 조건에서의 비교**(Mobile · Slow 4G · 4x CPU throttling), 실측 축은 **실제 모바일 쓰로틀링에서의 성능**입니다. 두 축을 분리해 병기합니다.

| 지표        | 마켓컬리 | 우리 (시뮬레이션) | 우리 (실측, 6회) |
| ----------- | -------- | ----------------- | ---------------- |
| Performance | 40점     | 78점              | **98점**         |
| FCP         | 5.1초    | 2.1초             | 1.15초           |
| LCP         | 21.6초   | 4.2초             | **1.55초**       |
| TBT         | 650ms    | 60ms              | 155ms \*         |
| CLS         | 0.004    | 0                 | **0**            |
| Speed Index | 13.6초   | 6.1초             | 1.20초           |
| 접근성      | 76점     | 96점              | **96점**         |
| 권장사항    | 77점     | 96점              | —                |
| SEO         | 85점     | 100점             | —                |

\* TBT 155ms는 6회 평균입니다. 서버 지연 670ms가 겹친 1회성 outlier를 제외하면 **91ms**(나머지 5회는 79~116ms)입니다. 평균과 제외값을 둘 다 적는 쪽을 택했습니다 — 유리한 숫자만 고르지 않고, 왜 두 값이 다른지 설명할 수 있게 하기 위해서입니다.

실측 Performance는 최고점 100점이 아니라 **6회 평균 98점**을 대표값으로 씁니다. LCP 분해도 평균 기준으로 합이 맞습니다 — TTFB 59.9ms + 리소스 로드 지연 570.0ms + 이미지 다운로드 893.7ms + 렌더 지연 26.1ms = 1,549.7ms.

#### 접근성

접근성 96점은 점수 자체보다 **코드에 들어간 규칙**으로 설명하는 편이 정확합니다.

- **터치 타깃 44px** — 시각 크기는 Figma 실측값을 유지하고, `::before` 확장 영역으로 히트 영역만 44×44px로 넓히는 패턴을 공통으로 씁니다(`QuantityStepper`, `ProductCard`, `ProductMiniCard`, `Calendar`, `ThemeToggle`). 디자인을 바꾸지 않고 접근성 기준을 맞추는 방식입니다.
- **확대 제한 없음** — `viewport`에서 `user-scalable=no`·`maximum-scale`을 쓰지 않습니다.
- **아이콘만으로 상태를 알리지 않음** — 디자인 시스템에 Play 아이콘이 없어 배너 재생/일시정지는 글리프가 고정인데, `aria-pressed`·`aria-label`로 상태를 전달합니다.
- **axe 자동 검증** — Storybook `@storybook/addon-a11y`로 컴포넌트 단위 접근성 검사를 CI에서 함께 돌립니다.

#### 끝내지 못한 것

발표 시 방어 가능하도록, **리포트에서 변화가 확인되지 않은 항목은 성과로 세지 않았습니다.** 1차 이후 개선 목록에 올렸다가 Before/After JSON 대조에서 수치 변화가 없어 제외한 항목이 둘, 구조로 남아 있는 문제가 하나입니다.

| 항목                        | 상태                                                                                                                      |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| 브라우저 타깃 조정·폴리필 제거 | 레거시 JS 43,785B(`Array.prototype.at`/`flat`)가 1차·2차 동일. `browserslist` 미설정 — 실제로 적용되지 않았습니다.          |
| 색상 대비 교체              | `color-contrast` 실패 요소 37개가 선택자까지 동일. 시맨틱 상태색 4색이 흰 배경 대비 2.06 / 1.67 / 1.28 / 1.10:1로 4.5:1에 미달합니다(`tokens/color.css`에 기록). 텍스트용 강조색은 디자인 확인 대기입니다. |
| 폰트 preload 경쟁           | `fonts.ts`에 `preload` 옵션을 명시하지 않아 Next 기본값(`true`)이 적용됩니다 — 2.0MB 폰트가 LCP 이미지와 같은 High 우선순위로 경쟁하는 구조가 남아 있습니다. 실측 성능에는 영향이 없었지만 시뮬레이션 수치를 끌어내리는 원인입니다. |

대신 실제로 차이가 확인된 **총 전송량(8.70MB/93건 → 6.20MB/62건, 29% 감소)**을 성과 항목으로 넣었습니다.

#### 측정 재현

홈은 로그인 가드가 걸려 있어 그냥 돌리면 `/login`이 측정됩니다. 미들웨어가 `refresh_token` 쿠키의 유효성이 아니라 **존재 여부만** 확인하므로, 더미 쿠키로 통과시킨 뒤 측정합니다.

```bash
# form-factor·화면 에뮬레이션은 모바일이 CLI 기본값 (Mobile · Slow 4G · 4x CPU throttling)
lighthouse https://<host>/ \
  --throttling-method=devtools \
  --extra-headers='{"Cookie":"refresh_token=dummy"}' \
  --output=json --output-path=./lighthouse.json
```

`finalDisplayedUrl`이 `/login`이 아닌지, `extraHeaders`에 쿠키가 실제로 들어갔는지, FCP와 LCP가 서로 다른 값인지(같으면 히어로 배너가 없는 화면을 측정한 것) 세 가지를 리포트에서 확인합니다.

---

## 문서

진입점은 [`CLAUDE.md`](./CLAUDE.md)이고, 상세 규칙은 [`.agents/`](./.agents)입니다.

- [API](./.agents/api-convention/SKILLS.md) — BFF, `publicFetch`/`privateFetch`, Zod, 쿼리 키
- [구조](./.agents/structure-convention/SKILLS.md) — 라우트, Atomic Design, 화면별 렌더링
- [코드 스타일](./.agents/code-style-convention/SKILLS.md) — 상태, 폼, 토큰, 이미지, 접근성
- [Git](./.agents/git-convention/SKILLS.md) — 브랜치, Conventional Commits, PR
- [보안](./.agents/security-convention/SKILLS.md) — FE-01~FE-16

컴포넌트 카탈로그는 [Chromatic develop](https://develop--6a978509faf77cfdcaeb125d.chromatic.com/)에 올라갑니다(상단 링크와 동일).
