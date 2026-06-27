Purpose
- Provide Copilot side-chat a concise, authoritative project context, coding rules, constraints, and response format so generated edits are safe, minimal, and enterprise-grade.

Project context (concise)
- Project: Resume Search RAG service (Node.js + Express, TypeScript).
- Layout expectations: `src/app.ts`, `src/server.ts`, `src/routes/`, `src/services/`, `src/repositories/`, `src/config/`, `src/middleware/`, `src/types/`.
- Integrations: MongoDB (Atlas), Mistral embeddings/LLM (configurable via env), optional groq LLM.
- Performance target: low-moderate traffic, P95 3–5s acceptable; prioritize relevance over raw latency.
- Security: Do not hardcode or leak secrets. Read secrets from environment variables only.

Coding rules & conventions
- Language: TypeScript (ES2022/Node 18+). Prefer `async`/`await` and explicit typing.
- Keep changes minimal and isolated to requested files.
- Use descriptive names (no one-letter variable names).
- Avoid global side-effects; register new routes/services in `src/app.ts` or the DI entrypoint.
- Add or update unit tests for significant logic changes; prefer focused, deterministic tests.
- Error handling: return JSON `{ error: string, code?: string }` for 4xx/5xx responses.
- Logging: structured JSON logs including `requestId`, `endpoint`, `durationMs`, and `componentTimings`.

Environment variables (examples)
- `NODE_ENV`
- `PORT`
- `MONGODB_URI`
- `MISTRAL_API_KEY`
- `MISTRAL_EMBED_MODEL` (default: mistral-embed)
- `LLM_API_KEY` (if using groq or another LLM provider)

Response format for code tasks (required)
- For each proposed change return:
  - File path(s) and full file content (ready to paste).
  - One-line summary of the change.
  - Commands to validate locally (build/test/run).
- If a change requires secrets, infra access, or schema changes, list them explicitly.

When to ask clarifying questions
- If the task touches unspecified infra (e.g., Atlas vector index), request required connection strings or index JSON before code generation.
- If the task would change public APIs or versions, confirm schema/versioning expectations.

Reference
- Keep `Architecture.md` in the repo as the source of truth for search, embedding, re-ranking, and logging behavior.
