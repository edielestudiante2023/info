# Cycloid Talent SAS — Sitio Web Informativo

Sitio web corporativo de **Cycloid Talent SAS**, empresa colombiana especializada en consultoria de Seguridad y Salud en el Trabajo (SG-SST). Presenta los servicios de la empresa, paginas informativas regulatorias, codigos QR para capacitaciones y una agenda de consultores integrada con Google Sheets.

## Stack tecnologico

| Componente | Tecnologia |
|------------|------------|
| Frontend | HTML5, CSS3 (SCSS), JavaScript |
| Template | HTML5 UP Editorial (CCA 3.0) |
| Librerias JS | jQuery 3.7.0, DataTables 1.13.6 |
| Iconos | FontAwesome 5+ |
| Datos externos | Google Sheets (CSV publico) |
| Servidor | Nginx (Ubuntu 24.04) en produccion |

## Paginas del sitio

| Pagina | Descripcion |
|--------|-------------|
| `index.html` | Landing principal — servicios, soluciones, contacto |
| `cocolab2025.html` | Guia sobre Resolucion 3461/2025 (COCOLAB) |
| `agenda.html` | Agenda de consultores — lectura en tiempo real de Google Sheets |
| `qrbrigadista.html` | QR para inscripcion a capacitacion de brigada de emergencia |
| `qrInduccionSST.html` | QR para induccion SST en propiedad horizontal |
| `qrEvSimulacro.html` | QR para evaluacion de simulacro |
| `visita1.html` | QR para registro de visitas |

## Estructura del proyecto

```
info/
├── assets/
│   ├── css/              # Estilos compilados (main.css, fontawesome)
│   ├── js/               # jQuery, DataTables, scripts del template
│   ├── sass/             # Fuentes SCSS del template Editorial
│   └── webfonts/         # FontAwesome (eot, svg, ttf, woff, woff2)
├── images/               # Logos, QR codes, favicon
├── docs/                 # Documentacion tecnica
├── index.html            # Landing principal
├── cocolab2025.html      # Pagina COCOLAB 2025
├── agenda.html           # Agenda con Google Sheets
├── qrbrigadista.html     # QR Brigadista
├── qrInduccionSST.html   # QR Induccion SST
├── qrEvSimulacro.html    # QR Evaluacion Simulacro
├── visita1.html          # QR Visita
├── LICENSE.txt           # Licencia CCA 3.0 (HTML5 UP)
├── CONTRIBUTING.md       # Guia de contribucion
└── .gitignore            # Exclusiones de git
```

## Servicios externos

| Servicio | Uso | Metodo |
|----------|-----|--------|
| Google Sheets | Agenda de consultores (CSV publico) | Fetch desde JS en `agenda.html` |

No se requieren API keys ni variables de entorno. El sitio es 100% estatico.

## Requisitos previos

- Servidor web (Apache, Nginx, o cualquier servidor de archivos estaticos)
- No requiere PHP, Node.js ni base de datos

## Instalacion local

```bash
# Clonar el repositorio
git clone https://github.com/edielestudiante2023/info.git
cd info

# Opcion 1: Abrir directamente en el navegador
# Abrir index.html en cualquier navegador

# Opcion 2: Usar un servidor local
# Con Python:
python -m http.server 8080

# Con VS Code:
# Instalar extension Live Server y hacer clic en "Go Live"
```

## Deploy a produccion

El sitio se despliega en el servidor de produccion via SSH. El pipeline CI/CD automatiza este proceso (ver `.gitea/workflows/`).

Para deploy manual, consultar la documentacion interna del equipo.

## Documentacion adicional

- [CONTRIBUTING.md](CONTRIBUTING.md) — Guia de contribucion y flujo de ramas
- [docs/HARDENING-info.md](docs/HARDENING-info.md) — Documento de hardening del repositorio
