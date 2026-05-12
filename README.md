# AmbientBot — Cloudflare Pages

Frontend del AmbientBot desplegado en Cloudflare Pages.

## Arquitectura

```
Cloudflare Pages (frontend) → Cloudflare Tunnel (API proxy) → pc.valy:8766 (backend RAG)
```

- **Frontend:** Este repo — HTML/JS/CSS estático servido desde el edge de Cloudflare
- **Backend:** Python + ChromaDB corriendo en pc.valy (local)
- **Conexión:** Cloudflare tunnel redirige a pc.valy:8766

## Configuración

El archivo `config.js` contiene la URL base de la API:

```js
const API_BASE = 'https://tunnel-url.trycloudflare.com';
```

Este archivo se actualiza automáticamente cuando el tunnel URL cambia.

## Endpoints API

| Ruta | Método | Descripción |
|------|--------|-------------|
| `/api/ask` | POST | Consulta RAG (body: `{"question": "..."}`) |
| `/api/status` | GET | Estado del backend y cantidad de chunks |
| `/api/alertas` | GET | Alertas normativas recientes |

## Deploy

Conectado a GitHub → Cloudflare Pages con deploy automático en cada push a main.
