# Changelog / Testing Report

## Fixed
- `src/components/ErrorBoundary.tsx`: never showed its fallback (missing `getDerivedStateFromError`); typed props/state (removed `any`).
- `src/main.tsx`: ErrorBoundary was never mounted; now wraps `<App />`.
- `src/components/chat/ChatWithIan.tsx`: removed a dev-only effect that made an extra `GET /api/chat` just to `console.log("API Key loaded")`.
- `package.json`: removed the placeholder `test` script that always failed.

## Removed files
None (nothing was safe to delete without a build to verify).

## Tests
- PASSED (static): all relative and `@/` imports resolve; all `/images`, `/fonts`, `/assets` references exist in `public/`.
- NOT PERFORMED: `npm install`, `npm run typecheck`, `npm run build`, running the site, chat, login/admin inbox, Supabase CRUD, responsive checks. The sandbox has no network (npm registry unreachable) and there are no Supabase/Gemini credentials. Run `npm install && npm run typecheck && npm run build` locally to verify.

## Remaining observations (not changed)
- `index.html` loads Tailwind via the Play CDN (`cdn.tailwindcss.com`) with an inline config, while `tailwindcss` and `@tailwindcss/vite` are installed but `theme.css` does not import Tailwind. Switching to the build-time plugin is recommended for production but needs a build to verify, so I left it.
- `api/chat.ts` duplicates profile facts from `src/content/profile.ts` (intentional, documented in README).

## Setup
See README.md: Node 20.19+/22.12+, `npm install`, `cp .env.example .env.local`, `npm run dev`. Database: run `supabase/schema.sql` on a fresh Supabase project.
