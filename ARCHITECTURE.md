# Architecture — Rural & Remote Healthcare Access Mapper

## Overview

The project consists of a Next.js web frontend and a FastAPI backend. The frontend
renders the interactive healthcare-access map and visualizations; the backend
calculates each settlement's distance to the nearest healthcare facility in the
same country and classifies access.

## Components

| Component | Technology | Responsibility |
| --- | --- | --- |
| Frontend | Next.js 16 App Router, React 19, TypeScript | User interface, browser-side API request, map and analytics |
| Map and visualizations | Leaflet, React-Leaflet, Turf.js, D3.js | Basemap, spatial overlays, charts and interactive map |
| Backend | FastAPI, Uvicorn, Pydantic | Health check, API routing, response schemas and accessibility analysis |
| Data | Python in-memory records | 30 settlement and 30 healthcare facility records; no database |

## Data Flow

1. The browser loads the Next.js application.
2. The frontend requests `GET /api/analysis/underserved-areas` from the FastAPI
   service using `NEXT_PUBLIC_API_URL` as its base URL.
3. The backend analyzes the in-memory settlement and facility records with the
   Haversine distance calculation and returns the nearest-facility results.
4. The frontend filters and presents the response in the map, rankings, panels,
   and analytics.

The backend also exposes `GET /health` for service health checks.

## Local and Container Setup

For local development, run the backend on port 8000 and the frontend on port
3000. Docker Compose runs those same two services, publishing configurable host
ports and passing the browser API URL at frontend build time. The backend's
`CORS_ORIGINS` setting controls which frontend origins may call the API.

## Data Limitations

The application uses illustrative sample records held in memory. Facility
names/coordinates are described in the project documentation as real-based,
while demographic and operational figures are synthetic. The application is a
demonstration and does not provide verified clinical or public-health guidance.
