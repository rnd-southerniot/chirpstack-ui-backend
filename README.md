# ChirpStack UI Backend

An **Express.js backend service** that exposes clean REST APIs for managing **Tenants, Applications, Devices, and Gateways** in **ChirpStack**, powered by the **ChirpStack gRPC API**.

This project is designed to act as a **UI-friendly middleware** between modern web frontends and ChirpStack’s gRPC services.

---

## ✨ Key Features

- gRPC → REST translation layer for ChirpStack
- Supports:
  - Tenants
  - Applications
  - Devices
  - Gateways
- Pagination, search, filtering, and ordering
- Built-in **in-memory caching** (TTL-based)
- ESM-first (no `require`, fully modern Node.js)
- Clean, predictable API routes for frontend use
- Designed for extensibility (auth, RBAC, rate-limits)

---

## 🧱 Architecture Overview

```
Frontend (React / Next.js / UI)
        |
        v
Express REST API
        |
        v
ChirpStack gRPC API
```

This backend **does not replace ChirpStack** — it **simplifies integration** and improves developer productivity.

---

## 🚀 Tech Stack

- Node.js (ESM)
- Express.js
- ChirpStack gRPC SDK
- @grpc/grpc-js
- node-cache (TTL caching)
- dotenv

---

## 📚 Project Structure

```
src/
 ├─ index.js            # Server entry point
 ├─ grpc.js             # gRPC clients + auth metadata
 ├─ cache.js            # TTL cache utilities
 ├─ routes/
 │   ├─ tenants.js
 │   ├─ apps.js
 │   ├─ devices.js
 │   └─ gateways.js
 ├─ utils/
 │   ├─ params.js       # pagination, search, filters
 │   └─ errors.js       # gRPC → HTTP error mapping
```

---

## ⚙️ Environment Variables

Create a `.env` file:

```env
PORT=3001
CHIRPSTACK_GRPC_ADDR=10.10.8.50:8080
CHIRPSTACK_TOKEN=YOUR_API_TOKEN
CACHE_TTL_LIST=15
CACHE_TTL_DETAIL=60
```

⚠️ **Important:**  
Use the **gRPC port** (usually `8080`), not the REST API port (`8090`).

---

## ▶️ Running the Project

```bash
npm install
npm run dev
```

Health check:

```bash
curl http://localhost:3001/health
```

---

## 🔗 REST API Endpoints (Examples)

```
GET /api/tenants
GET /api/tenants/:tenantId
GET /api/tenants/:tenantId/apps
GET /api/apps/:appId/devices
GET /api/devices/:devEui
GET /api/tenants/:tenantId/gateways
```

All list endpoints support:
- `limit`
- `offset`
- `search`
- filters (where applicable)

---

## 🔐 Authentication & Security

- Uses **ChirpStack API Token** for gRPC authentication
- App-level auth (JWT, SSO, RBAC) is intentionally **left pluggable**
- Designed to sit behind:
  - NGINX
  - Cloudflare Zero Trust
  - Internal VPN

---

## 🗑️ Roadmap

- [ ] App-level authentication (JWT / SSO)
- [ ] RBAC enforcement
- [ ] Persistent cache (Redis)
- [ ] Rate limiting
- [ ] OpenAPI (Swagger) documentation
- [ ] Docker image

---

## 💜 License

Internal / Private use (update if public licensing is required).
