# MedPredict — Disease Risk Prediction System

MedPredict estimates clinical risk for **heart disease**, **hypertension**, **stroke**, and **diabetes** using trained machine-learning models. Patients can run predictions and review history; providers can look up a patient and support clinical workflows; admins manage users and system overview.

## Stack

| Layer | Tech |
|-------|------|
| Frontend | React 18, Vite, Tailwind CSS, Axios |
| Backend | Django 5, Django REST Framework, PostgreSQL |
| ML | scikit-learn / joblib pipelines (`.pkl` under `backend/ml_models/`) |

## Project layout

```
├── frontend/              # React SPA (Vite, port 3000)
├── backend/               # Django API (port 8000)
│   ├── apps/              # accounts, patients, predictions, …
│   └── ml_models/         # Training scripts + model artifacts
├── medical-ml-system/     # Notebooks and ML experiments
├── docs/                  # Additional documentation
└── HOW_TO_RUN.md          # Detailed local setup guide
```

## Quick start

Full instructions are in **[HOW_TO_RUN.md](./HOW_TO_RUN.md)**. Summary:

```bash
# Backend
cd backend
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env               # configure secret key and database
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver

# Frontend (separate terminal)
cd frontend
cp .env.example .env               # VITE_API_BASE_URL=http://localhost:8000
npm install
npm run dev
```

| Service | URL |
|---------|-----|
| App | http://localhost:3000 |
| API | http://127.0.0.1:8000 |
| Django admin | http://127.0.0.1:8000/admin/ |

To use the in-app Admin Dashboard (`/admin-dashboard`), assign the `admin` role to a user in Django admin.

## Roles

| Role | Capabilities |
|------|----------------|
| Patient | Run predictions and view personal history |
| Provider | Look up a patient by ID; run and review predictions |
| Admin | User and system overview via `/admin-dashboard` |

## Documentation

- [HOW_TO_RUN.md](./HOW_TO_RUN.md) — setup, run, Docker, troubleshooting  
- [backend/README.md](./backend/README.md) — API overview and environment variables  
- [frontend/README.md](./frontend/README.md) — frontend setup  
