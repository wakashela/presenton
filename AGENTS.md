# Repository Guidelines

## Project Structure & Module Organization

`electron/` contains the desktop application and its runtime integration. `servers/fastapi/` holds the Python API and its `tests/`; `servers/nextjs/` contains the frontend and its tests. Repository tooling and Node tests live in `scripts/`, presentation templates in `templates/`, documentation in `docs/`, and README images in `readme_assets/`. Check `CONTRIBUTING.md`: contributions outside `electron/` may not currently be accepted.

## Build, Test, and Development Commands

- `cd electron && npm run setup:env` installs desktop, frontend, and backend dependencies; `npm run dev` starts the desktop development app.
- `cd electron && npm run build:all` builds the desktop components; `npm run dist` packages the application.
- `npm ci && npm test` at the repository root runs the Node tooling tests.
- `./test-local.sh` runs the local CI test groups. See `.github/workflows/README.md` for prerequisites and individual commands.
- In `servers/nextjs/`, run `npm test`, `npm run lint`, and `npm run build` for frontend checks.

## Coding Style & Naming Conventions

Follow the surrounding code and preserve existing indentation and naming. Use Python's four-space indentation and descriptive `snake_case` names; follow the existing TypeScript and React conventions for frontend and Electron code. Run the Next.js ESLint check before submitting frontend changes. Avoid unrelated formatting changes.

## Testing Guidelines

Add focused regression tests for behavior changes. Python tests use pytest and follow `test_*.py` in `servers/fastapi/tests/`; run them from `servers/fastapi/` with `uv run --locked python -m pytest`. Root tooling uses Node's test runner and `*.test.mjs` files. Frontend CI also runs Node and Cypress component tests. Configure the test environment as described in `.github/workflows/README.md`. No repository-wide coverage threshold is documented.

## Commit & Pull Request Guidelines

Recent commits use concise, scoped messages such as `fix(chat): prevent editor context overflow`; follow that pattern where practical. Use descriptive branches such as `fix/export-pptx-error`. Open an issue or discussion for feature proposals, and describe the problem, solution, and validation in the pull request. Link relevant issues and include screenshots for visible changes. For bugs, provide reproduction steps, expected and actual behavior, and relevant logs.

## Security & Configuration

Keep API keys and local `.env` values out of commits. Consult the README for supported environment variables and Docker configuration.
