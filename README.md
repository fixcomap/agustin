# fixcomap/agustin

Portfolio de Agustín Prieto en [agustin.fixcomap.com](https://agustin.fixcomap.com). HTML/CSS estático,
sin framework ni build; misma paleta que [fixcomap.com](https://fixcomap.com).

Sin pipeline propio: `ci.yml` llama a los reusable workflows de
[`fixcomap/platform`](https://github.com/fixcomap/platform) (`rw-static-checks`, `rw-pages-deploy`).
Cada PR publica una preview `<rama>.fixcomap-agustin.pages.dev`, `develop` la preview `develop.…` y
`main` producción (environment `production`). El proyecto de Pages, su dominio y el DNS viven en
`platform` (`infra/dns/pages.tf`).

| Fichero | Qué es |
|---|---|
| `public/index.html`, `public/style.css` | la página |
| `public/_headers` | CSP estricta (sin JS), HSTS, nosniff |
| `public/assets/` | foto y CV; se suben a mano (`public/assets/README.md`) |

Flujo: GitFlow como en `platform` y `web` (`feature/*` → `develop`; `release/AAAA-MM-DD` → `main`).
Runbook en el `CONTRIBUTING.md` de `platform`.
