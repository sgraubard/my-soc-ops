# Bingo Mixer — Agent Instructions

Social bingo game for in-person mixers. [Workshop guide](workshop/GUIDE.md). Stack: React 19 + TypeScript + Vite 8, Tailwind CSS v4 ([config](.github/instructions/tailwind-4.instructions.md)), Vitest + Testing Library.

## ✅ Before Finishing Any Task

- [ ] `npm run lint` — no errors
- [ ] `npm run build` — no type errors
- [ ] `npm run test` — all tests pass

## Commands

| Command         | Purpose                      |
| --------------- | ---------------------------- |
| `npm run dev`   | Dev server at localhost:5173 |
| `npm run build` | `tsc -b && vite build`       |
| `npm run test`  | Vitest (non-watch)           |
| `npm run lint`  | ESLint                       |

## Architecture

```
src/
  types/index.ts       # BingoSquareData, BingoLine, GameState
  data/questions.ts    # Question bank + FREE_SPACE constant
  utils/bingoLogic.ts  # Pure functions: generateBoard, toggleSquare, checkBingo, getWinningSquareIds
  hooks/useBingoGame.ts  # Single source of truth; localStorage persistence
  components/          # StartScreen, GameScreen, BingoBoard, BingoSquare, BingoModal
  App.tsx              # Renders StartScreen or GameScreen based on gameState
```

## Key Conventions

- **State machine**: `'start' → 'playing' → 'bingo'`; board is 5×5, `CENTER_INDEX = 12` = free space (pre-marked)
- **Logic is pure**: all game logic in `bingoLogic.ts`; components receive props only from `useBingoGame`
- **LocalStorage**: key `'bingo-game-state'`, `STORAGE_VERSION = 1` — always validate before loading
- **Tailwind tokens** (in `src/index.css` `@theme`): `accent`, `accent-light`, `marked`, `marked-border`, `bingo`
- **Tests**: `*.test.ts` next to source; only pure functions tested; use `vi.mock` for randomness in `generateBoard`
- **GitHub Pages**: `VITE_REPO_NAME` env var sets Vite `base` path

## Custom Agents & Prompts

| File                                                             | Purpose                                   |
| ---------------------------------------------------------------- | ----------------------------------------- |
| [quiz-master.agent.md](.github/agents/quiz-master.agent.md)      | Generate themed bingo questions           |
| [pixel-jam.agent.md](.github/agents/pixel-jam.agent.md)          | Design UI iteratively                     |
| [tdd.agent.md](.github/agents/tdd.agent.md)                      | TDD orchestrator (red → green → refactor) |
| [ui-review.agent.md](.github/agents/ui-review.agent.md)          | UI code review                            |
| [setup.prompt.md](.github/prompts/setup.prompt.md)               | Project onboarding prompt                 |
| [frontend-design SKILL](.github/skills/frontend-design/SKILL.md) | Frontend design workflow                  |
