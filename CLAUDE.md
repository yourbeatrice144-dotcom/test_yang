# Todo

브라우저에서만 동작하는 클라이언트 전용 to-do 웹앱.

## 스택

- **Next.js (App Router)** — 페이지/레이아웃은 `src/app` 아래에 둔다.
- **TypeScript** — 모든 소스는 `.ts` / `.tsx`.
- **Tailwind CSS** — 스타일은 유틸리티 클래스로 작성한다. 별도 CSS 파일을 늘리지 않는다.
- **클라이언트 전용** — 서버, DB, API 라우트 없음. 데이터는 브라우저 `localStorage`에만 저장한다.

## 폴더 구조

```
src/
  app/
    layout.tsx      루트 레이아웃, metadata
    page.tsx        메인 화면
    globals.css     Tailwind 지시문만
  components/       재사용 UI 컴포넌트
  lib/
    todo-store.ts   todo 데이터 접근 계층 (localStorage 읽기/쓰기)
public/             정적 파일
```

경로 별칭은 `@/*` → `src/*` (예: `import { getTodos } from "@/lib/todo-store"`).

## 규칙

1. **데이터 접근은 반드시 `src/lib/todo-store.ts`를 통해서만 한다.**
   컴포넌트에서 `localStorage`를 직접 호출하지 않는다. 저장 키, 직렬화,
   기본값 처리는 전부 store 안에 둔다.
2. **상태관리 라이브러리를 추가하지 않는다.** Redux, Zustand, Jotai 등 금지.
   `useState`, `useEffect`, `useReducer`, `useContext` 같은 React 내장 훅만 사용한다.
3. **커밋 전에 `npm run build`가 통과하는지 확인한다.** 빌드가 깨진 상태로 커밋/푸시하지 않는다.

## 배포

깃허브에 push하면 버셀(Vercel)이 자동으로 빌드·배포한다.
따라서 `main`에 올라가는 커밋은 항상 빌드가 통과해야 한다.

@AGENTS.md
