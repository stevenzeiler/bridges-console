# AGENTS.md

## What this is

`bridges-console` is a small npm library (v1.0.0) that embeds an interactive Node REPL with classes loaded as globals. Dormant since 2014-12-11.

## Stack

- ES6 source in `src/`, compiled by `gulp` 3.8 and `gulp-6to5` 1.x into `build/` (committed). `package.json` `main` is `./build/index.js`.
- Runtime dependencies: `require-all-to-camel ^1.0.0`, `lodash ^2.4.1`, `bluebird ^2.3.11`.
- Gulp 3 does not run on Node 12 and later (known upstream), so rebuilding on a current Node is expected to fail. Not tried in this pass.

## Layout

- `src/console.js`, `src/index.js`: source. `build/`: compiled output that is actually loaded.
- `app/models/market.js`, `test/models/*.js`: sample classes for the demo.
- `test/basic.js`, `test/gatewayd.js`: demo scripts that open a REPL.
- `gulpfile.js`: the single `default` task that compiles `src/` to `build/`.

## Commands

- Install: `npm install` (old dev dependencies; may fail or warn on today's Node).
- Build: `npx gulp` (expected to fail on modern Node, see above). If you change `src/`, `build/` must be regenerated and committed together.
- Test: `npm test` opens an interactive prompt; it has no assertions.
- Run: `npm run console`.

## Rules

- Add or update tests with every change. If a change cannot be tested, say why in the pull request.
- Never commit secrets: keys, tokens, passwords, `.env` files. Use placeholders such as `sXXXXXXXX`.
- Use Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`).
- Keep `docs/STATUS.md` current when behaviour or tooling changes.

## What agents may and may not do

- May: fix bugs, improve docs, add tests, open pull requests against `master`.
- May not, without Steven: archive or delete the repo, publish to npm or any registry, rewrite git history, change the license, or merge their own pull requests.
