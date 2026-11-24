---
inclusion: always
---
# How it is built

- **A small web app**: Vite, TypeScript, no framework heavier than it needs.
  Opens fast on a cheap Android phone on slow data: the first screen under
  150 KB of script.
- **Shared between two people**: Firebase Firestore on the free Spark plan.
  No card, no paid features. **If Firebase asks for a card, stop and tell
  the owner.** No Cloud Storage: photos are shrunk in the browser to about
  100 KB each and kept with their handover.
- **No account to start**: the artist creates a book and shares a link with
  the gallery; each side types their name once on that phone.
- **Keys**: the Firebase config lives in `src/firebase-config.ts`, which is
  ignored by git; `src/firebase-config.example.ts` shows its shape. Never
  commit a key.
- **Tests**: Vitest for unit tests and fast-check for property tests (the
  share sums, the ghost rules). `npm test` must pass before any commit.
- **Accessible**: every control reachable by keyboard, 44px tap targets,
  text contrast WCAG AA; `prefers-reduced-motion` stops every drift and fade
  (a ghost then shows as a dashed outline instead).
