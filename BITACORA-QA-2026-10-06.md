# Bitácora QA — Comparación mocks (:5431) vs implementación (:34115)

**Sesión:** 2026-10-06
**Repositorio de pruebas:** `/home/dev_root/Desktop/pro/pruebas-git`
**Versiones:** mocks `http://localhost:5431` (Vite + VITE_USE_MOCKS=true) · implementación `http://localhost:34115` (`wails dev`)

## Método

Recorrido flujo por flujo en ambas versiones con Playwright; la implementación
debe replicar el comportamiento de la versión con mocks usando datos reales
del repo `pruebas-git`.

## Defectos encontrados y corregidos

1. **Modal Nuevo Commit: archivos con estado invertido/truncado** — `WorkingTreeFiles`
   usaba `Run()` que devuelve la salida con `TrimSpace`, corrompiendo el parseo de
   `git status --porcelain` (` M README.md` se leía como staged y con ruta `EADME.md`).
   ✅ Corregido: nuevo `GitExecutor.RunRaw` sin recorte; repositorio: `git_log.go`,
   `git_executor.go`, `git_stats.go`, `git_commit_detail.go` (explorador/líneas usan
   contenido crudo). Verificado: `staged:false`, `path:"README.md"`.

2. **Crear commit no aplicaba los archivos seleccionados en el modal** — el backend
   solo ejecutaba `git commit -m`; los archivos elegidos en el modal nunca se
   agregaban a staging y el commit fallaba ("nothing to commit").
   ✅ Corregido: `CreateCommitInput.files` + `git add -- <file>` por cada archivo
   seleccionado (backend `domain/commit.go`, `usecase/commit.go`,
   `repository/git_log.go`; frontend `commitService.ts`, `useCommitHistory.ts`,
   `NewCommitModal.tsx`, `CommitsView.tsx`, `HistoryView.tsx`).
   Verificado: commit `f213a75` creado con README.md y diálogo "Commit subido".

## Comparación de flujos (implementación vs mocks)

| Flujo | Resultado |
|---|---|
| Listado de repositorios | ✅ Paridad (datos reales vs mock) |
| Añadir repo (dropdown) | ✅ |
| FolderPicker "Buscar proyecto" | ✅ Añade el repo seleccionado (D1 corregido) |
| Detalle repo (overview, ecosistema, actividad) | ✅ Paridad |
| Branches: filtros, búsqueda, autor/estado, orden | ✅ Paridad |
| Crear rama "test-qa-branch" | ✅ Creada y eliminada (real) |
| Menú contextual de rama + eliminar con confirmación | ✅ |
| Commits: filtros rama/autor/tag, búsqueda | ✅ Paridad (1 commit en feature/login) |
| Historial agrupado por día | ✅ Paridad |
| Nuevo Commit: staged/unstaged reales | ✅ Corregido |
| Stats (Total Commits, contribuidores, rangos) | ✅ Datos reales + botón "Último año" |
| Calendario mensual | ✅ Paridad (navegación de mes decorativa en ambas) |
| Settings: tema oscuro, guardar, restablecer | ✅ Paridad (html class `dark`) |
| Ctrl+K buscador | ✅ |
| Sidebar con nombre real del repo | ✅ "pruebas-git" |
| Consola | ✅ Mismo `TypeError ... ipc.js` benigno que la versión mock (ruido de Wails) |

## Estado final

- Rama activa: `main`; commits: `f213a75` (creado en QA), `b58a3d9`, `d03d211`
- `test-qa-branch` creada y eliminada durante la sesión
- Sin defectos abiertos de paridad respecto a la versión con mocks
