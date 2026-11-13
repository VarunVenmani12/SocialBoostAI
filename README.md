# SocialBoost AI

SocialBoost AI is a modular monolith project. This repository currently contains the Phase 1 Sprint 1 backend and web frontend foundation.

## Local development with Docker Compose

1. Copy `.env.example` to `.env` and change the local development values if needed.
2. Start the services with `docker compose up --build`.
3. Open the frontend at <http://localhost:5173> and the backend health check at <http://localhost:8000/health/>.

The Compose configuration starts PostgreSQL, Django, and the Vite development server. It does not run migrations.

## Run services without Docker

Backend (from the repository root):

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r backend/requirements/base.txt
python backend/manage.py runserver
```

Frontend:

```powershell
cd frontend
npm install
npm run dev
```

The Django development server requires PostgreSQL settings from the environment. Set the variables listed in `.env.example` and use a locally reachable PostgreSQL instance.
