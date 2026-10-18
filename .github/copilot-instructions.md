# Copilot instructions

Single-file space quiz: everything (HTML, CSS, JS) lives in `index.html`. No build, no dependencies, no tests, no linter. Not a git repo. Run it by opening the file directly (`file://`), no server needed.

## Architecture

- Questions are the `Q` array of `[question, [4 options], correctIndex]`. The "/ 10" in the Mission Control panel markup is hardcoded; update it if the question count changes.
- State is two globals, `i` (current question) and `s` (score). `render()` rebuilds the question view via `innerHTML` and re-wires handlers each time; `finish()` renders the results screen (emoji and message are chosen by score ratio); "Play again" resets `i`/`s` and calls `render()`.
- The progress bar (`#bar`) lives inside the `.mission` (Mission Control) score panel, alongside `#score`. `render()` and `finish()` both update `#bar` and `#score`, so keep those IDs.
- Background (stars, planets, rocket) is fixed-position decoration with `pointer-events:none`; `.hero` and `main` sit above it via `z-index`.

## Conventions

- The page is always dark-themed (space background); `main` overrides the colour variables locally. `:root` still defines `prefers-color-scheme` variables for the shared tokens (`--accent`, `--good`, `--bad`, etc.).
- Feedback uses CSS classes `.correct` (pulse animation) and `.wrong` (shake animation) on `.opt`; after an answer, all options are disabled and the correct one is always highlighted.
- Keyboard focus is managed explicitly: first option after each render, "Next" after answering, "Play again" on results. Preserve this when changing flow.
- Body text is 15px system sans-serif; the layout is a narrow centred column (`max-width:440px`).
- UI copy is in English.

## Testing

Manual only: open the page in the integrated browser and drive it with the `evaluate_javascript` action (click `.opt`, `.next`, `.again`; assert `#score`, `#bar` width, `.fb` text, `.big`/`.emoji` on results).
