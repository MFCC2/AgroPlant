# AGTECH — Doctor Cultivos IA

## Structure

```
doctor-cultivos/          — Angular 22 standalone SPA (main project)
  src/main.ts             — Frontend entrypoint (bootstrapApplication)
  src/app/                — Components, services, routes
  backend/main.py         — FastAPI backend + MobileNetV3 TorchScript model
  backend/requirements.txt— Python deps
backend-plantas/          — Older Python backend copy (not the deployed one)
```

All frontend commands run from `doctor-cultivos/`.

## Commands

| Command | Action |
|---------|--------|
| `npm start` | Dev server on `http://localhost:4200` |
| `npm run build` | Production build |
| `npm test` | Run Vitest unit tests (via `@angular/build:unit-test`) |
| `npm run watch` | Dev build with `--watch` |
| `cd backend && python main.py` | Start FastAPI backend on `:8000` (reload enabled) |

## Conventions

- **No linter** — only Prettier for formatting: single quotes, 100 print width
- **TypeScript `strict: false`** — non-strict mode (no strict null checks, etc.)
- **Angular standalone components** only (no NgModules)
- **No proxy config** — backend URL is hardcoded in two places: `diagnostico.service.ts:10` and `diagnostico.component.ts:427` (points to `https://agetch.onrender.com/diagnosticar`)
- **Hardcoded Groq API key** in `environments/environment.ts` — do not commit changes to this file
- **EditorConfig**: indent 2 spaces, UTF-8
- **No CI/CD pipeline** configured

## Backend

- FastAPI app at `doctor-cultivos/backend/main.py`
- Endpoints: `POST /diagnosticar` (image file + lat/lon), `GET /` (health)
- Model downloaded at runtime from Google Drive (TorchScript MobileNetV3)
- 38 PlantVillage disease classes, Spanish treatment dictionary
- Open-Meteo weather + Nominatim geocoding integration
