# AGENTS.md!!!!

Juego tipo PacMan en JS/HTML/CSS vanilla, sin build ni dependencias. El proyecto existe para aprender **Spec Driven Development**; toda comunicación, comentarios y specs van en español.

## Ejecución

- No hay `package.json`, npm, lint, tests ni CI. No intentar ejecutar esos comandos.
- Para probar: abrir `src/index.html` directo en el navegador (funciona por `file://`; no se necesita servidor).

## Arquitectura

- **Sin módulos ES.** Los scripts se cargan como `<script>` en orden en `src/index.html`: `maze.js` → `game.js` → `render.js` → `main.js`, y se comunican por globals en `window` (p. ej. `window.MAZE`, `window.createGame`). El orden de carga importa: un archivo JS nuevo necesita su etiqueta `<script>` en la posición correcta de ese orden.
- `maze.js`: define `MAZE` (laberinto 28x31, fila de túnel 14 con wrap horizontal). Es la matriz **prístina: nunca se muta**; `createGame()` la copia a `game.grid`.
- Valores de celda: `0` vacío, `1` pared, `2` dot, `3` puerta de la caseta (bloquea a Pacman pero no a los fantasmas).
- `game.js` = estado y reglas; `render.js` = dibujo (usa `game.grid`, no `MAZE`, para reflejar los dots comidos); `main.js` = bucle, teclado y overlay.

## Flujo spec-driven (obligatorio para features nuevas)

- Skills instaladas: `/spec` y `/spec-impl` (definidas en `.agents/skills/`, lock en `skills-lock.json`).
- Las specs viven en `specs/NN-slug.md` (numeradas con dos dígitos). Si la carpeta no existe, el flujo la crea.
- `/spec` diseña la spec con preguntas y la guarda en estado **Borrador**. El humano la revisa y cambia el estado a **Aprobado** (el agente nunca lo hace solo).
- `/spec-impl` solo implementa specs con estado que signifique "Aprobado"; crea la rama `spec-NN-slug` e implementa paso a paso con pausas para revisar diffs.
- **Nunca hacer commit automáticamente**; solo a petición explícita del usuario.

## Estilo de código

- Comentarios en español, comillas simples, punto y coma.
- Convención inusual del repo: espacios dentro de los paréntesis, p. ej. `funcion( arg )` y `grid[ y ][ x ]`. Mantenerla al editar archivos existentes.
