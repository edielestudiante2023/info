# Guia de Contribucion — info (Cycloid Talent SAS)

## Flujo de ramas

```
main          <- Produccion. Solo codigo validado y estable.
develop       <- Integracion. Cambios se unen aqui antes de ir a main.
feature/xxx   <- Nuevas funcionalidades. Se crean desde develop.
hotfix/xxx    <- Correcciones urgentes. Se crean desde main.
```

### Flujo de trabajo

- **Nueva funcionalidad:** `develop` → `feature/nombre` → PR a `develop` → PR a `main`
- **Hotfix urgente:** `main` → `hotfix/nombre` → PR a `main` + PR a `develop`

## Convencion de commits

Usar prefijos para identificar el tipo de cambio:

| Prefijo | Uso |
|---------|-----|
| `feat:` | Nueva funcionalidad o pagina |
| `fix:` | Correccion de errores |
| `docs:` | Cambios en documentacion |
| `style:` | Cambios de estilos CSS/SCSS |
| `refactor:` | Reestructuracion sin cambio funcional |
| `chore:` | Mantenimiento, configuracion, limpieza |

Ejemplos:
```
feat: agregar pagina de simulacro de evacuacion
fix: corregir tabla responsiva en agenda.html
docs: actualizar README con instrucciones de deploy
style: ajustar colores del sidebar en mobile
chore: actualizar .gitignore
```

## Convencion de nombres de ramas

| Tipo | Formato | Ejemplo |
|------|---------|---------|
| Feature | `feature/modulo-descripcion` | `feature/agenda-filtro-fecha` |
| Hotfix | `hotfix/bug-descripcion` | `hotfix/qr-imagen-rota` |

## Reglas

1. **No push directo a `main`** — Siempre via PR revisado
2. **No push directo a `develop`** — Siempre via PR desde feature/
3. **No credenciales en el codigo** — Ninguna API key, password o token
4. **No archivos temporales** — No subir archivos de prueba, bocetos o logs
5. **No operaciones destructivas en produccion** — No borrar ni sobreescribir sin revision

## Proceso de revision

1. Crear rama `feature/` o `hotfix/` desde la rama correspondiente
2. Hacer los cambios y commits siguiendo la convencion
3. Push de la rama al remoto
4. Crear PR en Gitea/GitHub
5. El pipeline CI/CD valida automaticamente (sintaxis, seguridad)
6. Revision por otro miembro del equipo
7. Merge a `develop` (o `main` en hotfix)
