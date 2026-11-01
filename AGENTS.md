# Base44 dev notes
- `docker-compose.base44.yml`: `webui` (Streamlit, host 3000, runOnSave + poll watcher) and `api` (FastAPI via `uvicorn app.asgi:app --reload`, host 8080, docs at /docs). Source is bind-mounted; Python deps are baked into the image — rebuild after changing requirements.txt.
- Build uses `DOCKER_BUILD_MIRROR=default` / `PIP_USE_OFFICIAL=1` (Chinese mirrors are slow from the sandbox).
- `config.toml` is auto-created from `config.example.toml` on first run (gitignored). LLM / Pexels / Pixabay API keys are entered in the WebUI Settings and stored there — no env secrets needed to boot.
- XSRF/CORS disabled for Streamlit only in the Base44 compose so the proxied preview websocket works.
- Health: `curl localhost:3000/_stcore/health` → `ok`.
