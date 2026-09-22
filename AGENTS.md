# Base44 notes

- The app users see is the Fastify server (`server.js`) serving the static site in `public/` on port 2345 (mapped to host 3000). No build step is needed for it.
- The root `index.html` + Vite config reference a `src/` React entry that does not exist in this repo; `npm run dev`/`npm run build` are vestigial. Edit files under `public/` for UI changes.
- Dev stack: `docker compose -f docker-compose.base44.yml up -d` (node:22 image, repo bind-mounted, nodemon restarts on `server.js`/`masqr.js`/`config.js`). Static file edits in `public/` are live immediately (hard refresh browser).
- Verify: `curl -s -o /dev/null -w '%{http_code}' localhost:3000/` → 200.
- Optional password gate lives in `config.js` (`challenge: true`); Masqr licensing middleware in `masqr.js` needs env vars and is off by default.
