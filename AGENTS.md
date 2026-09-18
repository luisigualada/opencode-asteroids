# Asteroids agent notes

## Run and verify

- This is a dependency-free static site: open `index.html` directly, or run `npx serve .` and use `http://localhost:3000`.
- There is no tracked build, lint, formatter, or test command. For JavaScript changes, run `node --check game.js` and manually exercise the game in a browser.
- Manual checks should cover arrow-key movement, Space firing and restart, collisions, and level progression; handled game keys must not scroll the page.

## Implementation constraints

- `index.html` is the browser entrypoint and loads the single global `game.js` script after an 800×600 canvas. Keep its `W`/`H` constants aligned with the canvas dimensions.
- The request-animation-frame loop supplies seconds-based `dt` and caps it at 0.05. Keep motion and timers `dt`-based; wrapping uses `wrap()`.
- Entity removal is deferred: mark an entity with `dead`, then filter it after update/collision processing. Preserve that lifecycle when adding entities or collisions.
- `justPressed` is consumed by `pressed()` for one-shot inputs (Space); continuous controls use `keys`.
