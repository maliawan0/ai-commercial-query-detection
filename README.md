# AI Commercial Query Detection

Quantify and secure potential sponsorship revenue **before production begins**.

Upload a script, define a production budget, and the tool surfaces commercial integration opportunities — brand placements a scene could plausibly carry — along with the budget impact of each. Accepted suggestions are saved as a reusable analysis and can be exported as an evidence pack for a sponsor conversation.

## The workflow

1. **Input** — upload the script and enter budget parameters
2. **Review** — AI-generated integration suggestions, accepted or rejected one by one
3. **Dashboard** — budget impact of the accepted set, visualised
4. **Evidence pack** — an exportable summary to take to sponsors
5. **History** — every saved analysis kept per user

## Stack

| Layer | Technology |
|---|---|
| Backend | FastAPI, Pydantic, Motor/PyMongo, JWT auth |
| Frontend | React 18, TypeScript, Vite, Tailwind CSS, shadcn/ui |
| State/data | TanStack Query, React Router |
| Database | MongoDB |

## Layout

```
backend/
  app/
    routers/    # auth, analyses, users
    models/     # User, Analysis documents
    schemas/    # request/response contracts
    auth.py     # JWT issue + verify
    db.py       # Mongo client
    main.py     # app + CORS + route registration
frontend/
  src/
    pages/      # Home, InputForm, Review, Dashboard, EvidencePack, History, Settings, auth
    components/ # BudgetChart, SaveAnalysisButton, Header, PrivateRoute
    context/    # AuthContext
```

## Running it locally

**Backend**

```bash
cd backend
cp .env.example .env        # set MONGO_URI, JWT secret, CORS_ORIGINS
pip install -r requirements.txt
uvicorn app.main:app --reload
```

**Frontend**

```bash
cd frontend
npm install
npm run dev
```

The client expects the API at the origin listed in `CORS_ORIGINS` (defaults to `http://localhost:5173`).

## API surface

All routes are versioned under `/api/v1`.

| Method | Route | Purpose |
|---|---|---|
| `POST` | `/api/v1/auth/register` | Create an account |
| `POST` | `/api/v1/auth/login` | Exchange credentials for a JWT |
| `GET/POST` | `/api/v1/analyses` | List or save analyses |
| `GET` | `/api/v1/users/me` | Current user |
