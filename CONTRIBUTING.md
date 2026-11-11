# Contributing to AutoGrowth Pro

Thanks for your interest! Every contribution helps: bug reports, documentation, translations and code.

## How to contribute

1. **Open an issue** first for bugs or feature ideas, so we can discuss them.
2. **Fork** the repository and create a branch: `git checkout -b feature/my-change`.
3. Run the project locally (see the README) and check that:
   - the backend starts and `GET /health` returns `{"status": "ok"}`
   - `cd frontend && npm run build` succeeds
4. **Open a pull request** with a clear description of what changed and why.

## Guidelines

- Keep pull requests small and focused.
- Never commit secrets (`.env`, API keys). Use `.env.example` for new variables.
- Translations live in `frontend/locales/` and `backend/app/i18n/`. Corrections and new languages are welcome.
- Be respectful and constructive in every discussion.

## License

By contributing, you agree that your contributions are licensed under the [MIT License](LICENSE).
