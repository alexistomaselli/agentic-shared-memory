---
name: asm-bootstrap
description: Skill de onboarding para sembrar la estructura de conocimiento ASM (knowledge/) de un cliente dentro de su repositorio <empresa>-soe.
license: MIT
metadata:
  author: alexistomaselli
  version: "2.1.0"
---

# ASM Bootstrap Skill (Onboarding de conocimiento)

Esta skill transforma a un agente de IA (Antigravity, Claude Code, Codex) en un
inicializador de la **memoria organizacional (ASM)** de una empresa.

> **Alcance (importante):** ASM se ocupa **solo de la carpeta `knowledge/`**. El
> repositorio del cliente es `<empresa>-soe` y su scaffold completo
> (`model/`, `systems/`, `automations/`, `governance/`) es responsabilidad de la
> Metodología SOE, no de esta skill. Esta skill no crea esas carpetas.

Cuando el usuario (asesor/ingeniero) invoque esta skill, **seguí estrictamente
estos pasos en orden, sin saltar ninguno.**

## Fase 1: La entrevista (interacción con el humano)

Actuá como analista de negocios y hacé las siguientes preguntas, **UNA POR UNA**
(no todas de golpe). Esperá la respuesta antes de avanzar.

1. **"¿Cuál es el nombre de la empresa o cliente?"**
2. **"¿A qué industria pertenece y cuál es su modelo de negocio principal?"**
3. **"¿Cuáles son los principales puntos de dolor o problemas operativos que motivan esta asesoría?"**
4. **"¿Quiénes son los *stakeholders* o responsables clave con los que interactuaremos?"**

## Fase 2: Ejecución automática (generación de la memoria)

Una vez respondidas las 4 preguntas, generá la estructura `knowledge/` y los
archivos semilla. Ejecutá estos pasos de inmediato sin pedir permiso.

> **Contexto:** estos pasos asumen que trabajás dentro del repositorio
> `<empresa>-soe`. Si todavía no existe, indicá al usuario que lo cree primero
> (ver paso 4) y luego sembrá `knowledge/` dentro de él.

1. Creá las siguientes carpetas (todas bajo `knowledge/`):
   - `knowledge/`
   - `knowledge/fuentes/` (material crudo: reuniones, documentos, capturas)
   - `knowledge/live/daily/`
   - `knowledge/live/inbox/`
   - `knowledge/live/sessions/`
   - `knowledge/decisions/`
   - `knowledge/processes/`
   - `knowledge/foundations/`

2. Creá **`knowledge/current_state.md`** con un resumen ejecutivo de la entrevista
   (nombre, modelo de negocio, puntos de dolor, stakeholders). Es la foto inicial.

3. Creá el primer ADR en **`knowledge/decisions/ADR-001_adopcion-asm.md`**:
   - Frontmatter:
     ```yaml
     ---
     author_role: advisor
     status: approved
     date: <fecha-actual>
     ---
     ```
   - Contenido: por qué la empresa adopta ASM como su modelo de gestión del
     conocimiento dentro de su SOE.

4. **Repositorio:** el repositorio del cliente debe llamarse `<empresa>-soe`
   (ej. `acme-soe`), siguiendo la convención de la Metodología SOE. ASM vive
   dentro, como `knowledge/`. (El scaffold completo del `<empresa>-soe` lo arma la
   metodología SOE; esta skill solo siembra `knowledge/`.)

5. **Cierre:** imprimí un mensaje de éxito e indicá al usuario que inicialice su
   índice semántico local apuntando a la carpeta de conocimiento:
   `qmd --index <empresa>-soe collection add docs ./knowledge/`

> **Material de relevamiento:** el material crudo de reuniones (ej. export de
> Fathom), documentos y capturas va en `knowledge/fuentes/` (subcarpetas
> `reuniones/`, `documentos/`, `capturas/`), con nombre `<AAAA-MM-DD>-<slug>`. Es
> permanente y trazable; de ahí se destilan requerimientos.

> **Regla de oro:** incluí los frontmatters (YAML) en todos los archivos Markdown
> de negocio que crees, identificando `author_role: advisor`.
