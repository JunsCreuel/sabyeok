# 새벽의 댓글창 — 프로젝트 메모

## 반드시 지킬 구현 조건 (모든 단계 공통)

- **반응형 웹 필수**: 폰이든 태블릿이든 데스크톱이든 화면 크기에 관계없이 레이아웃이
  깨지지 않고 자연스럽게 반응해야 한다. 고정 픽셀 폭 대신 상대 단위(%, rem, flex,
  grid, clamp())와 미디어 쿼리를 사용한다. 새 화면/컴포넌트를 만들 때마다 좁은
  화면(모바일)과 넓은 화면(데스크톱) 모두에서 확인한다.

## 기술 스택

React 19 + Vite, react-router-dom 7(HashRouter), Context+useState 전역 상태
(`src/store/useApp.jsx`), 순수 CSS(`src/index.css` 토큰), oxlint. GitHub Pages
배포(`vite.config.js`의 `base: './'`, main 푸시 시 Actions 자동 배포).

## 백엔드: Firebase (Auth + Firestore)

- 호스팅은 계속 GitHub Pages. Firebase는 백엔드(로그인, 데이터 저장)로만 사용.
- 설정은 `src/firebase.js`. Firebase 웹 config 값은 비밀키가 아니라 공개
  클라이언트 식별자라 코드에 그대로 둔다(보안은 Firestore 규칙이 담당).
- 로그인: 닉네임+비밀번호 입력을 받아, 닉네임을 해시한 가짜 이메일로 Firebase
  Auth(Email/Password)에 가입·로그인한다. 실제 이메일 수집 없음, 비밀번호
  찾기도 없는 간이 계정.
- 닉네임 프로필은 Firestore `users/{uid}` 문서에 저장.
- Firestore 보안 규칙은 저장소의 `firestore.rules`에 참고용으로 보관 —
  자동 배포되지 않으므로 규칙을 바꿀 때마다 Firebase 콘솔 > Firestore Database
  > Rules 탭에 수동으로 붙여넣고 게시해야 한다.

## 디자인 시스템

`JunsCreuel/Poppin-Room`(같은 소유자의 이전 프로젝트) UI 구조를 참고: 굵은
검정 2px 테두리, 알약형(pill) 버튼/네비, 화이트 배경, 둥근 카드. 색상만 새벽
컨셉에 맞게 라벤더/민트/살구 파스텔로 재구성(`src/index.css`의 `--lavender`,
`--mint`, `--apricot` 등).

## 작업 방식

- main에 직접 커밋 금지. 기능 브랜치에서 화면 단위로 작업.
- 한 번에 다 만들지 않고 단계별로 진행, 매 단계 후 요약하고 다음 단계 진행 여부 확인.
- 커밋은 기능/파일 단위로 잘게 나누고 커밋 메시지로 변경 내용을 알 수 있게 작성.
- 새 라이브러리 추가는 꼭 필요할 때만, 추가 전 이유를 설명하고 확인받는다.
- 문구/색상/세부 UI 등 애매한 기획 판단은 임의로 정하지 않고 먼저 제안 후 확인받는다.
