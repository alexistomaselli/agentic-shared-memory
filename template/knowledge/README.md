# Knowledge Base Template

Esta carpeta actúa como memoria centralizada para todos los agentes de IA que trabajan en este proyecto.

## Estructura
- `current_state.md`: Estado actual del proyecto.
- `fuentes/`: Material **crudo** de relevamiento (reuniones, documentos, capturas). Permanente; de acá se destilan requerimientos. No se migra como `live/`.
- `foundations/`: Reglas de negocio y modelo core.
- `decisions/`: ADRs (decisiones en general, naming, arquitecturas).
- `processes/`: Definiciones de la empresa y módulos de negocio inamovibles (SOPs).
- `live/`: Buffer operativo (memoria viva diaria).

**Importante:** Asegúrate de inicializar un índice local de QMD para esta carpeta usando:
`qmd --index <nombre-proyecto> collection add docs ./knowledge/`
