# Beanchain Frontend

Vite + React 19 starter for the Beanchain web app. It uses TanStack Router for routing, TanStack Query for data fetching/caching, Tailwind CSS v4 for styling, and Biome for linting/formatting.

## Quick Start

- Prerequisites: `Node >= 18`, `pnpm` installed.
- Copy environment file: `cp .env.example .env`.
- Set `VITE_APP_URL` to your backend base URL and `VITE_APP_NAME` as desired.
- Install dependencies: `pnpm install`.
- Start dev server: `pnpm dev` and open `http://localhost:3333`.

## Environment Variables

- `VITE_APP_URL`: Base URL of the backend API (e.g., `http://localhost:8080`).
- `VITE_APP_NAME`: App display name (used in UI/metadata).

## Scripts

- `pnpm dev`: Run the Vite dev server on port `3333`.
- `pnpm start`: Alias of `dev`.
- `pnpm build`: Build production assets (`dist/`) and run TypeScript type-check.
- `pnpm serve`: Preview the production build locally.
- `pnpm test`: Run unit and component tests with Vitest.
- `pnpm lint`: Lint the project with Biome.
- `pnpm format`: Format files with Biome.
- `pnpm check`: Combined lint + format checks.

## Tech Stack

- React 19, Vite 6
- TanStack Router (code-splitting enabled)
- TanStack Query (+ Devtools)
- Tailwind CSS v4
- React Hook Form + Zod
- Zustand (state management)
- Testing Library + Vitest

## Project Structure

```
beanchain-frontend/
├─ src/
│  ├─ components/        # Reusable UI and providers (e.g., AuthProvider)
│  ├─ dto/               # Data transfer objects / types
│  ├─ hooks/             # Custom React hooks
│  ├─ lib/               # Utilities/libraries
│  ├─ pages/             # Page-level components (optional)
│  ├─ routes/            # TanStack Router route files
│  ├─ services/          # API clients (Axios) and service logic
│  ├─ utils/             # General utilities
│  ├─ main.tsx           # App entry, providers, router setup
│  ├─ routeTree.gen.ts   # Generated route tree (do not edit)
│  └─ styles.css         # Global styles
└─ vite.config.ts        # Vite + Tailwind + Router plugin config
```

### Routing

- The router is configured in `src/main.tsx` using a generated `routeTree.gen.ts`.
- Routes live under `src/routes/`. Adding or editing files here updates the route tree.
- The plugin is enabled in `vite.config.ts` with `autoCodeSplitting: true`.
- Do not manually edit `routeTree.gen.ts`; restart the dev server if it falls out of sync.

### Data & State

- TanStack Query is initialized in `main.tsx` via `QueryClientProvider`.
- Global client state can use `zustand` when needed.
- Forms should use `react-hook-form` with `zod` for schema validation.

### Styling

- Tailwind CSS v4 is wired via `@tailwindcss/vite` plugin in `vite.config.ts`.
- Use utility classes in components and add any global CSS in `src/styles.css`.
- The alias `@` maps to `src/` for cleaner imports.

## Build & Deploy

- Production build: `pnpm build` outputs to `dist/`.
- Preview locally: `pnpm serve` then open the printed URL.
- Deploy `dist/` to your static hosting (Netlify, Vercel, Nginx, etc.).
- Ensure `VITE_APP_URL` is set appropriately for the target environment.

## Testing & Quality

- Run tests: `pnpm test` (uses Vitest + Testing Library).
- Lint: `pnpm lint`.
- Format: `pnpm format`.
- Pre-commit suggestion: run `pnpm check` to lint and format together.

## Troubleshooting

- Route tree issues: delete `routeTree.gen.ts` and restart `pnpm dev` to regenerate.
- Port conflicts: change the dev port in `package.json` (`vite --port 3333`).
- Node version errors: upgrade to a supported Node LTS (`>= 18`).
- API 404/CORS: verify `VITE_APP_URL` matches your backend and supports CORS.

## Monorepo Notes

This frontend lives alongside `beanchain-backend/`. For local development, run the backend and point `VITE_APP_URL` to it. Refer to the backend README for setup.