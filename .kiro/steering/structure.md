---
inclusion: always
---
# Where things go

- `src/book.ts`: the book, its works and handovers; pure functions, no screen.
- `src/ghost.ts`: the ghost rules; pure, tested by properties.
- `src/share.ts`: the artist's share and what is still owed; pure.
- `src/export.ts`: "Put these works on Galleris": the spreadsheet and photos.
- `src/store.ts`: Firestore reads and writes, nothing else.
- `src/ui/`: screens; they call the pure modules and show `src/words.ts`.
- `src/words.ts`: every word on screen.
- `tests/`: one test file per pure module.
