# Fuentes

Material crudo de relevamiento: la materia prima de la que se destilan
requerimientos, procesos, reglas y decisiones. Se preserva para **trazabilidad**
("¿de dónde salió este requerimiento?").

> **Fuente (cruda) ≠ conocimiento procesado.** Lo procesado vive en `processes/`,
> `foundations/` y `decisions/`. Las fuentes son **permanentes** (no se borran ni
> se migran como `live/`).

## Subcarpetas (crear según necesidad)

- `reuniones/` — resúmenes/minutas de reuniones (ej. export de Fathom) + transcript.
- `documentos/` — documentos que comparte el cliente (Word, PDF, Excel/planillas).
- `capturas/` — screenshots de sistemas actuales.

## Convención de nombres

`<AAAA-MM-DD>-<slug>.<ext>` — la fecha es **cuándo se obtuvo** la fuente. La carpeta
ya indica el tipo; el nombre no lo repite. No se usan carpetas diarias (las fuentes
se organizan por tipo, no por día).

Ejemplos:
- `reuniones/2026-07-03-primer-contacto.md`
- `documentos/2026-07-05-plan-de-cuentas.xlsx`
- `capturas/2026-07-05-pantalla-sistema-contable.png`

## Encabezado de cada archivo `.md`

```yaml
---
tipo: reunion | documento | captura
fecha: <AAAA-MM-DD>
fuente: <Fathom | cliente | ...>
participantes: [ ... ]
---
```
