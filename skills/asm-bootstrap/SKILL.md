---
name: asm-bootstrap
description: Skill de automatización de Onboarding para inicializar la estructura Agentic Shared Memory (ASM) para un cliente o proyecto nuevo.
license: MIT
metadata:
  author: alexistomaselli
  version: "1.0.0"
---

# ASM Bootstrap Skill (Onboarding Automático)

Esta skill está diseñada para transformar a un Agente de IA (como Antigravity, Claude Code o Codex) en un Arquitecto Inicializador de proyectos ASM. 

Cuando el usuario (asesor/ingeniero) invoque esta skill, **debes seguir estrictamente estos pasos en orden, sin saltar ninguno.**

## Fase 1: La Entrevista (Interacción con el humano)
Actúa como un analista de negocios y hazle al humano las siguientes preguntas, **UNA POR UNA** (no hagas todas las preguntas de golpe). Espera su respuesta antes de avanzar a la siguiente.

1. **"¿Cuál es el nombre de la empresa o cliente para el que vamos a configurar ASM?"**
2. **"¿A qué industria pertenece y cuál es su modelo de negocio principal?"**
3. **"¿Cuáles son los principales puntos de dolor o problemas operativos que motivan esta asesoría?"**
4. **"¿Quiénes son los *Stakeholders* o responsables clave de la empresa con los que interactuaremos?"**

## Fase 2: Ejecución Automática (Generación del ADN)
Una vez que el humano haya respondido a las 4 preguntas, generarás automáticamente la estructura de directorios y los archivos semilla basándote en la información recolectada. Ejecuta estos pasos de inmediato sin pedir permiso:

1. Crea las siguientes carpetas en la raíz del proyecto local:
   - `knowledge/`
   - `knowledge/live/daily/`
   - `knowledge/live/inbox/`
   - `knowledge/live/sessions/`
   - `knowledge/decisions/`
   - `knowledge/processes/`
   - `knowledge/foundations/`

2. Crea el archivo principal **`knowledge/current_state.md`**. En él debes volcar un resumen ejecutivo con la información que obtuviste en la entrevista (Nombre de la Empresa, Modelo de Negocio, Puntos de Dolor, Stakeholders). Este documento será la foto inicial del sistema.

3. Crea el primer archivo de decisión en **`knowledge/decisions/ADR-001_adopcion-asm.md`**. 
   - Añade el Frontmatter:
     ```yaml
     ---
     author_role: advisor
     status: approved
     date: <fecha-actual>
     ---
     ```
   - En el contenido, redacta formalmente por qué la empresa ha decidido adoptar la arquitectura Agentic Shared Memory (ASM) como su modelo de Knowledge Management.

4. **Creación del Repositorio:** Informa al usuario que el repositorio a crear en GitHub deberá llamarse obligatoriamente `<nombre-empresa>-asm` (ej. `acme-asm`), para mantener la convención del estándar.

5. **Instrucciones Finales:** Imprime en consola un mensaje de éxito felicitando al usuario, e indícale que ejecute el siguiente comando para inicializar su índice semántico local respetando la nomenclatura:
   `qmd --index <nombre-empresa>-asm collection add docs ./knowledge/`

> **Regla de Oro:** Asegúrate de incluir los Frontmatters (YAML) en todos los archivos Markdown de negocio que crees, identificando que el `author_role` es `advisor`.