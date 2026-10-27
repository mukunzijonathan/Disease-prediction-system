# MedPredict — Disease Risk Prediction System

Full-stack app that estimates risk for **heart disease**, **hypertension**, **stroke**, and **diabetes** using trained scikit-learn models, with role-based access for patients, providers, and admins.

## Stack

| Layer | Tech |
|-------|------|
| Frontend | React 18, Vite, Tailwind CSS, Axios (session + CSRF) |
| Backend | Django 5, Django REST Framework, PostgreSQL (SQLite OK for local) |
| ML | scikit-learn / joblib pipelines (`.pkl` under `backend/ml_models/`) |

## Project layout

```
├── frontend/              # React SPA (Vite, port 3000)
├── backend/               # Django API (port 8000)
│   ├── apps/              # accounts, patients, predictions, …
│   └── ml_models/         # Training scripts + model artifacts
├── medical-ml-system/     # Notebooks / earlier ML experiments
├── docs/                  # Frontend planning notes
└── HOW_TO_RUN.md          # Detailed local setup
```

## Quick start

See **[HOW_TO_RUN.md](./HOW_TO_RUN.md)** for full steps. Summary:

```bash
# Backend
cd backend
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env               # set DJANGO_SECRET_KEY and DB values
python manage.py migrate
python manage.py createsuperuser   # interactive; do not commit credentials
python manage.py runserver

# Frontend (separate terminal)
cd frontend
cp .env.example .env               # VITE_API_BASE_URL=http://localhost:8000
npm install
npm run dev
```

- App: http://localhost:3000  
- API: http://127.0.0.1:8000  
- Django admin: http://127.0.0.1:8000/admin/

Assign the `admin` role in Django admin (or via the shell) if you need the in-app Admin Dashboard at `/admin-dashboard`.

## Roles

- **Patient** — run predictions, view personal history  
- **Provider** — look up a patient by ID and run / review predictions  
- **Admin** — user and system overview via `/admin-dashboard`

## Security notes

- Never commit `.env` files or real passwords. Use `.env.example` as a template only.
- Create accounts with `createsuperuser` / Register — do not hardcode credentials in docs or scripts.
- Demo seed data (`python ml_models/seed_demo_data.py`) reads passwords from environment variables; see that script’s header for required vars.
- Rotate any credentials that were previously committed in this repository.

## Docs

- [HOW_TO_RUN.md](./HOW_TO_RUN.md) — setup, run, Docker, troubleshooting  
- [backend/README.md](./backend/README.md) — API overview and env vars  
- [frontend/README.md](./frontend/README.md) — frontend setup  
