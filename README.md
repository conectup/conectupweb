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

Al ser estático, cualquier hosting de archivos estáticos sirve (GitHub Pages, Netlify, Vercel, Cloudflare Pages, S3, etc.). El contenido a desplegar es la raíz del repo.
