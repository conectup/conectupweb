# ConectUp — Web

Sitio estático de ConectUp: soluciones tecnológicas a medida.

## Stack

HTML + CSS + JS vanilla. Un único `index.html` autocontenido (estilos y tweaks inline, sin build). Fuentes cargadas desde Google Fonts.

## Desarrollo local

Requiere Node.js (para `npx`). No hay dependencias que instalar.

```bash
npm run dev
```

Levanta un servidor en [http://localhost:3000](http://localhost:3000) y abre el navegador.

Alternativa sin Node:

```bash
python -m http.server 3000
```

## Estructura

```
.
├── index.html        # Sitio completo (HTML + CSS + JS inline)
├── package.json      # Scripts de dev server
├── .gitignore
└── README.md
```

## Flujo de ramas

| Rama             | Propósito                                       |
| ---------------- | ----------------------------------------------- |
| `main`           | Producción. Sólo merges desde `pre`.            |
| `pre`            | Preproducción / staging. Integra develop-\*.    |
| `develop-nero`   | Rama de trabajo de Nero.                        |
| `develop-miwel`  | Rama de trabajo de Miwel.                       |

Flujo: `develop-<dev>` → PR a `pre` → validación → PR a `main`.

Cada developer trabaja libremente en su rama `develop-*`. Para promover a preproducción se abre PR hacia `pre`. Sólo tras validar en `pre` se mergea a `main` (producción).

## Deploy

**Producción**: [conectupweb.pages.dev](https://conectupweb.pages.dev) (Cloudflare Pages)

### Auto-deploy

Cada push a `main` dispara el workflow `.github/workflows/deploy.yml` que
sube la raíz del repo a Cloudflare Pages via Wrangler.

Secrets requeridos en el repo (ya configurados):
- `CLOUDFLARE_API_TOKEN` — token con permiso "Cloudflare Pages · Edit"
- `CLOUDFLARE_ACCOUNT_ID` — ID de la cuenta destino

### Deploy manual

```bash
CLOUDFLARE_API_TOKEN=xxx npx wrangler pages deploy . --project-name=conectupweb --branch=main
```
