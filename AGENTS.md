# AGENTS.md  
## Purpose  
This document defines **rules, expectations, and operating boundaries** for **AI agents and human contributors** working on this repository. The goal is **consistency, safety, and maintainability**.  
---  
## 🤖 Agent Role  
Agents operating on this repository act as:  
> **Backend Infrastructure Assistants**  
They may:  
- Add new REST endpoints  
- Extend gRPC service mappings  
- Improve caching or performance  
- Refactor code for clarity  
- Add documentation and comments  
They must **not**:  
- Change ChirpStack business logic  
- Store secrets or tokens in code  
- Modify production credentials  
- Introduce breaking API changes without approval  
---  
## 💐 Coding Standards  
- **ES Modules only** (`import`, no `require`)  
- Node.js ≥ 18  
- Prefer async / await  
- Keep routes thin, logic reusable  
- No inline secrets  
- Explicit error handling for all gRPC calls  
---  
## 🔁 API Design Rules  
- REST routes must remain **UI-friendly**  
- Pagination pattern must be consistent:  
  - `limit`  
  - `offset`  
  - `totalCount`  
- Responses should not leak raw gRPC internals  
- Field naming follows **camelCase**  
---  
## 🔎 Caching Rules  
- Lists → short TTL  
- Details → medium TTL  
- Mutations must invalidate:  
  - Object cache  
  - Parent list cache  
- No cache persistence without approval  
---  
## 🔒 Security Rules  
- gRPC authentication must always use metadata:  
  ```  
  authorization: Bearer <token>  
  ```  
- Never log tokens  
- No hardcoded credentials  
- Assume this service runs behind a secure gateway  
---  
## 🤕 Testing Expectations  
Agents may add:  
- Smoke tests  
- Contract tests  
- Mocked gRPC tests  
But should **not** introduce heavy test frameworks unless requested.  
---  
## 💐 Change Discipline  
When making changes:  
1. Prefer backward compatibility  
2. Update README if behavior changes  
3. Keep commits small and reversible  
4. Comment complex logic  
---  
## 💀 Philosophy  
This backend exists to:  
- Make ChirpStack easier to integrate  
- Reduce frontend complexity  
- Enforce clean boundaries  
- Scale safely with growing IoT deployments  
Keep it **boring, predictable, and reliable**. 
