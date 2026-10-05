# Bitácora QA — git-manager @ localhost:34115

**Sesión:** 2026-10-05
**Repositorio de pruebas:** `/home/dev_root/Desktop/pro/pruebas-git`
**Aplicación:** git-manager (Wails + React, `wails dev` en :34115)

## Preparación del repo

- `git init` / rama `main`
- Commit `d03d211` — Initial commit (README.md)
- Rama `feature/login`
- Rama `develop`
- Commit `bede680` — Add app.js (en `develop`)
- Tag `v0.1.0`

## Resultados de pruebas (resumen)

| Flujo | Resultado |
|---|---|
| Añadir repo (Crear proyecto) | ✅ OK |
| FolderPicker Buscar proyecto | ⚠️ Abre y navega pero NO añade el repo (D1) |
| Detalle de repo (overview) | ✅ OK |
| Branches: filtros, búsqueda, paginación | ✅ OK |
| Crear rama "test-qa-branch" | ✅ OK (verificado en terminal) |
| Menú contextual de rama (more_vert) | ✅ OK |
| Eliminar rama con confirmación | ✅ OK |
| Commits: filtros rama/autor/tag/fecha | ✅ OK |
| Historial agrupado por día | ✅ OK |
| Stats | ⚠️ Datos simulados (D5) |
| Settings: guardar/restablecer | ✅ OK |
| Tema oscuro | ❌ No aplica (D2) |
| Calendario mensual | ❌ Meses desfasados + totales inconsistentes (D3) |
| Referencias `origin/main` | ❌ Upstream inexistente (D4) |
| Sidebar "Mi proyecto" | ❌ Nombre fijo (D6) |
| Consola | ❌ 404 favicon + error IPC (D7) |

## Defectos registrados

Ver `Task/2026-10-05/qa-defectos-2026-10-05.md` en el repo `git-manager`.

## Estado final del repo de pruebas

- Ramas: `main`, `develop`, `feature/login`
- Tags: `v0.1.0`
- `test-qa-branch` creada y eliminada durante la sesión
- Rama activa: `main`
