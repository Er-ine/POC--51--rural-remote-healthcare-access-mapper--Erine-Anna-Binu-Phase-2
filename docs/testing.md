# Testing and Local Verification

## Frontend

Run from `frontend/` after installing dependencies with `npm ci`:

```sh
npm run lint
npm run build
```

There is no frontend test-runner script or checked-in frontend test suite in the
current repository.

## Backend

The backend has no checked-in automated test suite. Install its dependencies
from `backend/requirements.txt`, then run the API locally from `backend/`:

```sh
python -m uvicorn app.main:app --host 127.0.0.1 --port 8000
```

Check `GET http://127.0.0.1:8000/health` and
`GET http://127.0.0.1:8000/api/analysis/underserved-areas`.

## Docker Compose

Validate and start the containerized application from the repository root:

```sh
docker compose config -q
docker compose up --build
```

With the services running, check the same backend endpoints and load
`http://localhost:3000` in a browser. The frontend's browser request uses
`NEXT_PUBLIC_API_URL`; because it is a public Next.js variable, it is set at
image build time.