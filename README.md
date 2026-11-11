# AutoGrowth Pro

**Open-source B2B growth automation for small businesses: lead discovery, email outreach and AI-assisted content in one self-hosted stack.**

AutoGrowth Pro helps solo entrepreneurs, small businesses and local agencies (restaurants, hotels, shops, service companies) run their own prospecting without expensive marketing tools. It is also designed as a **teaching resource** for vocational and business schools learning how a modern SaaS is built and run.

> Status: early stage (v0.x). Feedback, issues and contributions are welcome.

## Features

- **Lead generation**: finds businesses through the Google Places API and enriches contacts with Hunter.io
- **Email automation**: campaigns sent over SMTP, with open tracking, `List-Unsubscribe` headers and country-specific compliance footers
- **AI content**: email and marketing copy generated with the Claude API (Anthropic)
- **Billing**: Stripe subscriptions and webhooks (optional, for people who want to run it as a service)
- **Client dashboard and admin panel**: Next.js and Tailwind, available in 6 languages (EN, FR, DE, ES, IT, PT)
- **Scheduler**: background jobs for leads, emails, onboarding and billing (APScheduler)
- **Extras**: affiliate tracking, A/B tests, rate limiting

## Tech stack

| Layer | Tools |
|---|---|
| Backend | Python 3.12, FastAPI, SQLAlchemy, PostgreSQL, Redis, APScheduler |
| Frontend | Next.js 14, React 18, TypeScript, Tailwind CSS, Recharts |
| Infra | Docker Compose, Nginx |

```
backend/    FastAPI API: routers, services, models, automation pipelines
frontend/   Next.js app: landing page, client dashboard, admin
nginx/      Reverse proxy (HTTPS) for production
scripts/    Deployment and Stripe setup helpers
```

## Quick start (local)

Requirements: Docker and Docker Compose.

```bash
git clone https://github.com/Franck2505/autonomous-business-automation.git
cd autonomous-business-automation
cp .env.example .env          # then edit .env (see "Configuration")
docker compose up -d db redis backend frontend
```

- Frontend: http://localhost:3000
- API: http://localhost:8000 (interactive docs at http://localhost:8000/docs)
- Health check: http://localhost:8000/health

The `nginx` service is for production only: it needs TLS certificates in `nginx/certs/`.

### Without Docker

```bash
# Backend
cd backend
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
DATABASE_URL=sqlite:///./dev.db uvicorn app.main:app --reload

# Frontend (in another terminal)
cd frontend
npm install --legacy-peer-deps
npm run dev
```

## Configuration

Every setting lives in `.env` (see `.env.example`). The app starts with empty API keys; each integration only turns on once its key is set.

| Variable | Purpose |
|---|---|
| `SECRET_KEY` | JWT signing key. Generate one with `openssl rand -hex 32` |
| `ANTHROPIC_API_KEY` | AI content generation |
| `GOOGLE_PLACES_API_KEY`, `HUNTER_IO_API_KEY` | Lead discovery and enrichment |
| `SMTP_*`, `FROM_EMAIL` | Outgoing email |
| `STRIPE_*` | Subscriptions (optional). Use test keys (`sk_test_...`) for development |

## Responsible use

This tool contacts businesses by email. **You are responsible for complying with the law where you operate**, for example GDPR and ePrivacy in the EU or CAN-SPAM in the US. That means a legitimate interest or consent, a clear sender identity, an easy unsubscribe link, and respect for opt-outs. Do not use it to send spam.

## Roadmap

- [ ] Automated tests (pytest and Playwright) and CI
- [ ] Alembic database migrations
- [ ] GDPR consent and opt-out registry management
- [ ] "Education mode" with demo data, for classroom use
- [ ] Contributor documentation and architecture guide

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
