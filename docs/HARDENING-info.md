# HARDENING DE REPOSITORIO — info

**Fecha:** 2026-04-05
**Aplicativo:** info — Sitio web corporativo Cycloid Talent SAS
**Empresa:** Cycloid Talent SAS
**Preparado para:** Edwin Lopez (consultor de infraestructura)

---

## TABLA DE CONTENIDO

1. Descripcion del aplicativo
2. Inventario de servicios externos
3. Documentacion del proyecto (README, CONTRIBUTING, .gitignore)
4. Ramas de trabajo
5. Pipelines CI/CD (Gitea)
6. Organizacion del repositorio
7. Hallazgos y acciones pendientes

> **Nota:** Este aplicativo no tiene base de datos. Se omite la fase de mapa de BD.

---

## 1. DESCRIPCION DEL APLICATIVO

### Stack tecnologico

| Componente | Tecnologia |
|------------|------------|
| Frontend | HTML5, CSS3 (SCSS), JavaScript |
| Template | HTML5 UP Editorial (CCA 3.0) |
| Librerias JS | jQuery 3.7.0, DataTables 1.13.6 |
| Iconos | FontAwesome 5+ (webfonts) |
| Datos externos | Google Sheets (CSV publico) |
| Servidor web | Nginx (Ubuntu 24.04) |
| Hosting | Hetzner |

### Paginas del sitio (7)

| Pagina | Descripcion |
|--------|-------------|
| `index.html` | Landing principal — servicios SST, soluciones, contacto |
| `cocolab2025.html` | Guia sobre Resolucion 3461/2025 (Comites de Convivencia Laboral) |
| `agenda.html` | Agenda de consultores — lectura en tiempo real de Google Sheets via CSV |
| `qrbrigadista.html` | QR para inscripcion a capacitacion de brigada de emergencia |
| `qrInduccionSST.html` | QR para induccion SST en propiedad horizontal |
| `qrEvSimulacro.html` | QR para evaluacion de simulacro de evacuacion |
| `visita1.html` | QR para registro de primera visita |

### Estructura del proyecto

```
info/
├── assets/
│   ├── css/              # main.css, fontawesome-all.min.css
│   ├── js/               # jQuery 3.7.0, DataTables, scripts del template
│   ├── sass/             # Fuentes SCSS del template Editorial
│   └── webfonts/         # FontAwesome (eot, svg, ttf, woff, woff2)
├── images/               # Logos, QR codes, favicon
├── docs/                 # Documentacion tecnica
├── .gitea/workflows/     # Pipelines CI/CD
├── index.html            # Landing principal
├── cocolab2025.html      # Pagina COCOLAB 2025
├── agenda.html           # Agenda con Google Sheets
├── qrbrigadista.html     # QR Brigadista
├── qrInduccionSST.html   # QR Induccion SST
├── qrEvSimulacro.html    # QR Evaluacion Simulacro
├── visita1.html          # QR Visita
├── LICENSE.txt           # Licencia CCA 3.0 (HTML5 UP)
├── README.md             # Documentacion principal
├── CONTRIBUTING.md       # Guia de contribucion
└── .gitignore            # Exclusiones de git
```

### Caracteristicas tecnicas

- **Sitio 100% estatico** — No requiere PHP, Node.js ni base de datos
- **Sin autenticacion** — Todas las paginas son publicas
- **Sin cron jobs** — No hay tareas programadas
- **Sin variables de entorno** — No se necesita `.env`
- **Unica integracion externa:** Google Sheets CSV (publico, sin API key)

### Servidor de produccion

| Dato | Valor |
|------|-------|
| OS | Ubuntu 24.04.3 LTS |
| Web server | Nginx |
| Acceso SSH | Llave ed25519 (ver documentacion interna) |

> IP, hostname y rutas se documentan internamente, no en repositorio publico.

---

## 2. INVENTARIO DE SERVICIOS EXTERNOS

### Servicios identificados

| Servicio | Uso | Archivo | Metodo | Requiere API Key |
|----------|-----|---------|--------|------------------|
| Google Sheets | Agenda de consultores | `agenda.html` | Fetch CSV publico via JS | No |

### URL de Google Sheets

```
https://docs.google.com/spreadsheets/d/e/2PACX-1vQ8L2llrzRuxxJKtdQV1y7gJiTRL0KO7_jA4nX-KaqA65J4aFE_sceAkBkQUQDK53TxrrmmBGO_6vpF/pub?gid=0&single=true&output=csv
```

Esta es una URL de publicacion publica de Google Sheets. No contiene credenciales y no requiere autenticacion.

### Evaluacion de seguridad

- **No hay API keys** en el codigo
- **No hay credenciales hardcodeadas**
- **No hay variables de entorno** referenciadas
- **No hay servicios de pago** integrados
- **Riesgo: BAJO** — El unico servicio externo es una hoja de calculo publica

### Contacto (hardcodeado en HTML, es intencional)

- Email: `cycloidtalent.sas@gmail.com` (enlace mailto en index.html)
- Telefono: `322 907 4371` (enlace tel en index.html)

---

## 3. DOCUMENTACION DEL PROYECTO

### Archivos creados en el repositorio

| Archivo | Descripcion |
|---------|-------------|
| `README.md` | Documentacion principal: stack, paginas, estructura, instalacion, deploy |
| `CONTRIBUTING.md` | Guia de contribucion: flujo de ramas, convencion de commits, reglas |
| `.gitignore` | Exclusiones: OS, IDEs, temporales, .claude/, .env |

### README.md incluye

- Stack tecnologico completo
- 7 paginas con descripcion
- Estructura de carpetas
- Servicios externos documentados
- Requisitos previos e instrucciones de instalacion local
- Instrucciones de deploy a produccion
- Links a documentacion adicional

### CONTRIBUTING.md incluye

- Flujo de ramas (main → develop → feature/ → hotfix/)
- Convencion de commits (feat:, fix:, docs:, style:, refactor:, chore:)
- Convencion de nombres de ramas
- 5 reglas (no push directo, no credenciales, no temporales, no destructivos)
- Proceso de revision con pipeline CI/CD

### .gitignore incluye

- Archivos de SO (.DS_Store, Thumbs.db, *.stackdump)
- Editores e IDEs (.vscode/, .idea/)
- Claude Code (.claude/)
- Archivos temporales (tmp_*, *.log, nohup.out)
- Archivos de notas (z_*, y_*, Z_*, ZZ_*)
- Dependencias futuras (node_modules/, vendor/)
- Variables de entorno (.env, .env.local, .env.production)

---

## 4. RAMAS DE TRABAJO

### Estructura creada

```
main          <- Produccion. Solo codigo validado y estable.
develop       <- Integracion. Aqui se unen los cambios antes de ir a main.
feature/xxx   <- Nuevas funcionalidades. Se crean desde develop.
hotfix/xxx    <- Correcciones urgentes. Se crean desde main.
```

### Estado actual

| Rama | Estado | Commit actual |
|------|--------|---------------|
| main | Existente, en remoto (origin/main) | 26a25fe (imagene qr simulacro) |
| develop | Creada localmente, pendiente push | Mismo commit que main |
| cycloid | Legacy — sera reemplazada por develop | Mismo commit que main |

### Proteccion de ramas (pendiente en Gitea)

- **main:** protegida, requiere PR, no push directo
- **develop:** protegida, requiere PR desde feature/

### Flujo de trabajo

- Nueva funcionalidad: `develop` → `feature/nombre` → PR a `develop` → PR a `main`
- Hotfix urgente: `main` → `hotfix/nombre` → PR a `main` + PR a `develop`

---

## 5. PIPELINES CI/CD

### Plataforma: Gitea con Gitea Runner (act_runner)

### Pipeline 1: Validar y Deploy a Dev/QA

**Archivo:** `.gitea/workflows/validate-and-deploy-qa.yml`
**Trigger:** Push/PR a develop o feature/*

```
git push → Gitea → Runner → Validate HTML + Secrets Scan → Deploy SSH → QA
```

| Job | Que hace | Bloquea si falla |
|-----|----------|------------------|
| validate | Verifica que todos los HTML existan y no esten vacios + assets criticos | Si |
| secrets-scan | Busca credenciales hardcodeadas (API keys, passwords, tokens) | Si |
| deploy-qa | SSH al servidor QA y ejecuta git pull | Solo en push a develop |

### Pipeline 2: Cutover a Produccion

**Archivo:** `.gitea/workflows/cutover-production.yml`
**Trigger:** Push a main (despues de merge de PR desde develop)

```
PR develop → main → Validate → Secrets Scan → Deploy SSH → Produccion (Hetzner)
                                                          → Verificacion HTTP post-deploy
```

| Job | Que hace |
|-----|----------|
| validate | Verifica HTML y assets criticos |
| secrets-scan | Busca credenciales hardcodeadas |
| deploy-production | SSH al Hetzner + git reset --hard origin/main + verificacion HTTP |

**Todo por pipeline, nada manual.**

### Secrets necesarios en Gitea

**Para Dev/QA:** QA_HOST, QA_USER, QA_SSH_KEY, QA_PATH
**Para Produccion:** PROD_HOST, PROD_USER, PROD_SSH_KEY, PROD_PATH, PROD_URL

### Flujo completo

```
feature/xxx → push → Validacion → PR a develop → Validacion → merge
                                                                 ↓
                                          Deploy automatico a QA
                                                                 ↓
                                              Pruebas en QA
                                                                 ↓
                                          PR develop → main → Validacion → merge
                                                                             ↓
                                                     Cutover automatico a Hetzner
                                                                             ↓
                                                          Verificacion post-deploy
                                                                             ↓
                                                              EN PRODUCCION
```

---

## 6. ORGANIZACION DEL REPOSITORIO

### Estado del repositorio

| Aspecto | Estado actual | Accion |
|---------|---------------|--------|
| Visibilidad | PUBLICO en GitHub | Migrar a Gitea privado |
| .gitignore | Creado (excluye tmp, basura, .claude, IDEs) | OK |
| Credenciales en codigo | Ninguna encontrada | OK |
| Credenciales en historial git | Ninguna encontrada | OK |

### Archivos basura trackeados en git (pendiente limpieza)

| Archivo | Tipo | Accion recomendada |
|---------|------|-------------------|
| `text.txt` | Notas de setup de Google Sheets | Eliminar (informacion ya en docs/) |
| `README.txt` | Creditos del template HTML5 UP | Eliminar (creditos ya en LICENSE.txt) |
| `.vscode/settings.json` | Config local del editor | Eliminar del tracking (ya en .gitignore) |

### Archivos que SI deben quedarse

- Todos los `.html` — paginas funcionales del sitio
- `assets/` completo — CSS, JS, SCSS, webfonts
- `images/` completo — logos y QR codes
- `LICENSE.txt` — licencia del template
- `README.md` — documentacion principal
- `CONTRIBUTING.md` — guia de contribucion
- `.gitignore` — exclusiones

---

## 7. HALLAZGOS Y ACCIONES PENDIENTES

### Prioridad ALTA

| # | Accion | Responsable |
|---|--------|-------------|
| 1 | Hacer repo privado en GitHub o migrar a Gitea privado | Consultor/Cliente |
| 2 | Push de rama `develop` al remoto | Cliente |
| 3 | Configurar proteccion de ramas en Gitea | Consultor |
| 4 | Configurar secrets en Gitea para pipelines CI/CD | Consultor |

### Prioridad MEDIA

| # | Accion | Responsable |
|---|--------|-------------|
| 5 | Eliminar `text.txt` del repo (commit de limpieza) | Cliente |
| 6 | Eliminar `README.txt` del repo (creditos ya en LICENSE.txt) | Cliente |
| 7 | Eliminar `.vscode/settings.json` del tracking | Cliente |
| 8 | Eliminar rama `cycloid` (reemplazada por `develop`) | Cliente |

### Prioridad BAJA

| # | Accion | Responsable |
|---|--------|-------------|
| 9 | Agregar HTTPS/SSL al dominio si no esta configurado | Consultor |
| 10 | Considerar minificacion de CSS/JS para produccion | Cliente |
| 11 | Agregar meta tags Open Graph para redes sociales | Cliente |

### Observaciones generales

- **Seguridad:** El repositorio no contiene credenciales ni datos sensibles. El riesgo principal es que sea publico en GitHub sin necesidad.
- **Complejidad:** Baja. Es un sitio estatico con 7 paginas HTML, sin backend ni base de datos.
- **Estado:** Funcional. Todas las paginas estan completas y el sitio esta desplegado en produccion.
- **Mantenimiento:** Minimo. Solo se actualiza cuando se agregan nuevas paginas o QR codes.

---

## CHECKLIST DE ENTREGABLES

### Archivos funcionales en el repositorio (obligatorios)

- [x] `README.md` — Documentacion principal profesional
- [x] `CONTRIBUTING.md` — Guia de contribucion con flujo de ramas
- [ ] `.env.example` — No aplica (sitio estatico sin variables de entorno)
- [x] `.gitea/workflows/validate-and-deploy-qa.yml` — Pipeline Dev/QA
- [x] `.gitea/workflows/cutover-production.yml` — Pipeline produccion
- [x] `.gitignore` — Creado y actualizado
- [x] Rama `develop` creada

### Documento para el consultor (obligatorio)

- [x] `docs/HARDENING-info.md` — Este documento

---

*Documento generado el 2026-04-05. Preparado como entregable del proceso de hardening del repositorio info.*
