# fixcomap/agustin

Portfolio de Agustín Prieto en [agustin.fixcomap.com](https://agustin.fixcomap.com). HTML/CSS estático,
sin framework ni build, con CSP estricta (sin JS).

## Desarrollo local

```sh
python3 -m http.server -d public 8000      # http://localhost:8000
```

| Fichero | Qué es |
|---|---|
| `public/index.html`, `public/style.css` | la página |
| `public/_headers` | cabeceras de seguridad |
| `public/assets/` | foto y CV (nombres en `public/assets/README.md`) |

## Despliegue

Pipeline estándar de [fixcomap/platform](https://github.com/fixcomap/platform): PR → checks;
`develop` → preview privada; `main` → producción con aprobación.
