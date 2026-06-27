# resumes-ai-rag

Minimal scaffold for RAG-based Resume Search API (Node.js + Express + TypeScript).

Quick start

1. Install dependencies

```bash
npm install
```

2. Copy `.env.example` to `.env` and set `MONGODB_URI` and keys.

3. Run in development

```bash
npm run dev
```

4. Build and run

```bash
npm run build
npm start
```

Health endpoints

- `GET /v1/health` — returns `{ name, version, uptime }`
- `GET /v1/health/db` — pings MongoDB and returns `{ ok, latencyMs }`
