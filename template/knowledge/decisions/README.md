# Decisions (ADRs)

Architecture Decision Records: el histórico inmutable del **por qué** de las
decisiones clave (naming, elección de herramientas, arquitectura, cambios de
proceso, etc.).

## Formato

Cada decisión es un archivo `ADR-NNN_titulo.md` con frontmatter:

```yaml
---
author_role: advisor
status: approved
date: <fecha>
---
```

## Regla

Los ADR no se editan retroactivamente. Si una decisión cambia, se agrega un nuevo
ADR que **supersede** al anterior, dejando trazable la evolución del criterio.
