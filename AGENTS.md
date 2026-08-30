# Guidelines

- For new DOM/browser API usage, use `app.ownerDocument` and `app.ownerWindow` instead of globals; without `app`, derive them from the mounted node's `ownerDocument` and its `defaultView`.

## Running in Base44 (dev)

- This is the Excalidraw monorepo. The runnable app is `excalidraw-app`, a Vite + React dev server. Packages (`packages/*`) are consumed from source via Vite aliases in `excalidraw-app/vite.config.mts`, so no pre-build of packages is needed.
- Dev compose: `docker compose -f docker-compose.base44.yml up -d`. It runs `yarn install --frozen-lockfile` then `vite --host 0.0.0.0 --port 3000` from `excalidraw-app`. Preview port 3000.
- `excalidraw-app/vite.config.mts` has `server.open: true`, which crashes headless containers (`spawn xdg-open ENOENT`). The compose installs a no-op `/usr/local/bin/xdg-open` to neutralize it — do not remove that step.
- Vite loads env from `envDir: "../"` (repo root `.env.development`). `VITE_APP_PORT` is pinned to 3000 via compose env. The core whiteboard renders with no backend; collaboration (WS :3002), AI (:3016), and Firebase are optional and unreachable locally, which is expected.
- No external secrets are required to boot.
