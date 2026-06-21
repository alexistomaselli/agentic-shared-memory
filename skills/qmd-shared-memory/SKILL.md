---
name: qmd-shared-memory
description: Instruye al agente a estructurar y mantener la memoria viva y el conocimiento estable usando Markdown y QMD.
license: MIT
metadata:
  author: alexistomaselli
  version: "1.0.0"
---

# QMD Shared Memory Skill

Esta skill instruye al agente sobre cómo usar y organizar el directorio `knowledge/` de manera que todos los agentes del equipo (Codex, Antigravity, OpenClaw) puedan compartir el mismo contexto asíncrono sin depender de un servidor centralizado.

## Jerarquía de la Base de Conocimiento

El proyecto debe mantener la siguiente estructura local en la carpeta `knowledge/`:

- `live/daily/`: Buffer operativo. Aquí anotarás los sprints, los logs de sesiones y análisis temporales. Cada archivo debe tener prefijo de fecha (ej. `YYYY-MM-DD_feature-X.md`).
- `live/sessions/`: Resúmenes de conversaciones con los humanos.
- `decisions/`: ADRs (Architecture Decision Records). El por qué de las decisiones. Historial de herramientas elegidas, naming, arquitectura general, etc.
- `processes/`: Casos de uso de negocio inamovibles, definiciones de la empresa y flujos operativos (SOPs).
- `foundations/`: Reglas de negocio core, esquemas de datos y flujos funcionales (lo estable).
- `current_state.md`: Una fotografía actual del estado del sistema.

## Flujo de Trabajo (El "Memory Loop")

1. **Recuperación (Bootstrap):** Antes de iniciar una tarea compleja, debes consultar la memoria utilizando el índice local de `qmd`:
   ```bash
   qmd --index <project_name> query "contexto sobre funcionalidad X"
   ```
2. **Buffer de Trabajo:** Todo progreso diario lo vas anotando en un archivo en `live/daily/`.
3. **Consolidación:** Cuando una funcionalidad se estabiliza, la información relevante de `live/` se destila y se migra hacia `current_state.md`, `processes/` o `foundations/`.

> **El principio cardinal:** Si la información no está en los archivos Markdown (y por lo tanto no se sube a Git), no existe para el resto del ecosistema multi-agente.