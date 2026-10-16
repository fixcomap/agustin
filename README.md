# fixcomap/agustin

Portfolio de Agustín Prieto en [agustin.fixcomap.com](https://agustin.fixcomap.com). HTML/CSS estático,
sin framework ni build; misma paleta que [fixcomap.com](https://fixcomap.com).

## Cómo se despliega

Este repo no tiene pipeline propio. `.github/workflows/ci.yml` es el mismo en todos los repos de
fixcomap y llama al pipeline estándar de [`fixcomap/platform`](https://github.com/fixcomap/platform),
que lee [`catalog/agustin.yaml`](https://github.com/fixcomap/platform/blob/main/catalog/agustin.yaml)
para saber qué es este repo (`type: static`) y cómo publicarlo. El proyecto de Cloudflare Pages
(`fixcomap-agustin`), los dominios y el DNS también salen de ese fichero.

| Evento | Qué pasa |
|---|---|
| PR a `develop` o `main` | gitflow, gitleaks + trivy, HTML (W3C Nu), CSP en `_headers`, preview en `<rama>.fixcomap-agustin.pages.dev` |
| Merge a `develop` | lo anterior + preview en `develop.fixcomap-agustin.pages.dev` |
| Merge a `main` | producción tras aprobar el environment `production`, con smoke test de https://agustin.fixcomap.com |

El único check obligatorio es `cicd / ok`. Si un deploy falla, Pages sigue sirviendo la versión
anterior.

Flujo de ramas (GitFlow):

```sh
git switch develop && git pull && git switch -c feature/<cambio>
# ... cambios, commits "<tipo>(<ámbito>): <descripción>" ...
gh pr create --base develop --fill          # checks en verde, sin aprobación; mirar la preview
# para publicar:
git switch develop && git pull && git switch -c release/AAAA-MM-DD
gh pr create --base main --fill             # 1 aprobación (o bypass de admin)
# tras el merge: PR de main a develop (back-merge)
```

## Desarrollo local

Sin build: `public/` se publica tal cual. Para verlo, cualquier servidor estático:

```sh
python3 -m http.server -d public 8000      # http://localhost:8000
```

| Fichero | Qué es |
|---|---|
| `public/index.html`, `public/style.css` | la página |
| `public/_headers` | cabeceras de Pages: CSP estricta (sin JS), HSTS, nosniff |
| `public/assets/` | foto y CV; se suben a mano con los nombres de `public/assets/README.md` |
