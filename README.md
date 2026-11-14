# TagBack + PingME

Private QR lost-and-found (TagBack) with a community layer (places, rides, communities).
Single Express server (`server.js`) serving a single-page frontend (`public/index.html`).

## Run locally
    npm install
    npm start          # http://localhost:3000

## Environment variables
| Name | Required | Purpose |
|---|---|---|
| `PLACE_KEY` | yes (production) | Password for the responder/community inbox. Without it a random key is printed in the logs. |
| `ANTHROPIC_API_KEY` | no | AI category suggestions. Without it the built-in rules are used. |
| `RESEND_API_KEY` | no | Email alerts to owners. |
| `DATA_FILE` | no | Where data is stored (default `./data.json`). Point at a persistent disk in production. |
| `PORT` | set by Render | |

## Deploy on Render
1. Push this folder to GitHub (`git add . && git commit -m "deploy ready" && git push`).
2. Render dashboard > your service > Environment: add `PLACE_KEY` (any strong password).
3. Settings > Health Check Path: `/healthz`. Render redeploys automatically on every push.

## Free-plan caveats
- Data lives in `data.json` on an ephemeral disk: it resets on every redeploy/restart. Fine for demos.
- The service sleeps after ~15 min idle; the first request then takes ~30-60s. Open the site once before a demo.
- To keep data, upgrade the plan and attach a disk (see the commented block in `render.yaml`).
