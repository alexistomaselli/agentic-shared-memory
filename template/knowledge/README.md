# Knowledge Base Template

Esta carpeta actúa como memoria centralizada para todos los agentes de IA que trabajan en este proyecto.

## Estructura
- `current_state.md`: Estado actual del proyecto.
- `foundations/`: Reglas de negocio y modelo core.
- `decisions/`: ADRs y decisiones clave.
- `live/`: Buffer operativo (memoria viva diaria).

**Importante:** Asegúrate de inicializar un índice local de QMD para esta carpeta usando:
`qmd --index <nombre-proyecto> collection add docs ./knowledge/`
