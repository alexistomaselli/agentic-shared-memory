# Agentic Shared Memory (ASM)

Patrón arquitectónico para la **Gestión del Conocimiento (Knowledge Management) y Memoria Descentralizada**, diseñado para digitalizar el "ADN corporativo" de una empresa y habilitar la colaboración sin fricciones entre humanos, consultores y ecosistemas multi-agente (Claude, Antigravity, OpenClaw, etc.) utilizando **Markdown**, **Git** y **QMD**.

## El Problema Moderno
Actualmente, las empresas sufren de fragmentación de contexto: el histórico de decisiones, las reglas de negocio y los manuales operativos (SOPs) mueren en PDFs olvidados, plataformas como Notion/Confluence, o peor aún, están dispersos en computadoras y "cabezas distintas". 
Esto genera una pérdida brutal de trazabilidad para la empresa y hace que cualquier integración de IA o consultoría requiera semanas de recolección de contexto manual.

## La Solución (ASM)
El patrón **Agentic Shared Memory** soluciona esto unificando la información de la empresa bajo un estándar auditable y directamente "consumible" por cualquier inteligencia artificial o humano.

1. **Markdown como Fuente de Verdad:** Todo el conocimiento de la empresa (procesos inamovibles, decisiones técnicas, bitácoras operativas) se guarda en archivos `.md` planos versionados en un repositorio Git. 
2. **Transferencia Tecnológica Inmediata:** Un LLM conectado a esta estructura no tiene que leer 40 páginas desordenadas; puede consultar exactamente el proceso o la decisión que necesita. Esto permite a dueños y consultores auditar y escalar la empresa de inmediato.
3. **QMD como Cerebro Local:** Cada máquina (sea la laptop de un consultor o un servidor autónomo) corre un índice `qmd` que vectoriza este repositorio en milisegundos, permitiendo a los agentes IA consultar el "cerebro corporativo" localmente.

---

## 🚀 La Capa de Interacción: ASM Client Dashboard

El repositorio Git sirve como "Backend" de la organización, pero las empresas y sus empleados no interactúan directamente con Git o archivos Markdown. Para ellos, el patrón ASM se integra con una **Capa de Presentación Web (El Client Dashboard)**.

El ecosistema ASM completo consiste en:
- **El Consultor/Ingeniero:** Accede al repositorio en crudo usando IDEs y consolas, trabajando directamente en Markdown.
- **La Organización (Cliente):** Accede a una Web App (Dashboard ASM) que lee y renderiza los archivos del repositorio en una interfaz intuitiva. El dashboard posee su propio agente de Inteligencia Artificial que se comunica con el usuario en lenguaje natural, y, por detrás, edita y hace *commits* en los archivos Markdown para mantener la estructura ASM sana sin que el humano deba aprender sintaxis técnica.

---

### Arquitectura Visual

```mermaid
flowchart TD
    %% Base de Conocimiento Centralizada
    subgraph Repo ["Repositorio del Proyecto / ADN Empresa (Git)"]
        direction TB
        F1["📄 current_state.md (Estado general de la organización)"]
        F2["📂 foundations/ (Reglas de negocio y modelo)"]
        F3["📂 decisions/ (Histórico del 'Por qué')"]
        F5["📂 processes/ (Manuales operativos inamovibles / SOPs)"]
        F4["📂 live/daily/ (Bitácora de avance diario y sprints)"]
    end

    %% Entorno Consultor / Local
    subgraph EntornoLocal ["Entorno Local (Humano / Consultor)"]
        direction TB
        QMD1[("Índice QMD Local")]
        AG1["🤖 Agente IDE Local / LLM"]
        
        QMD1 -- Lee e Indexa --> Repo
        AG1 -- Busca (qmd query) --> QMD1
    end

    %% Entorno Empresa
    subgraph EntornoEmpresa ["Entorno Empresa (Client Dashboard)"]
        direction TB
        WebApp["🖥️ Web App Dashboard"]
        AGE["🤖 Agente Web / MCP"]
        
        WebApp -- LLM -- AGE
        AGE -- Escribe en Git --> Repo
    end
```

## Estructura de la Memoria (Knowledge Loop)

Copia la carpeta `template/knowledge/` de este repositorio al directorio de tu empresa o proyecto para establecer el esqueleto de conocimiento:

- `live/daily/`: Buffer operativo. Aquí los humanos o agentes anotan el avance de cada sprint o sesión cronológicamente (ej. `YYYY-MM-DD_feature-X.md`).
- `decisions/`: ADRs (Architecture Decision Records). El histórico inmutable del *por qué* de decisiones clave (naming de la empresa, elección de herramientas, etc).
- `processes/`: Módulos de negocio inamovibles y flujos operativos (SOPs). **Aquí es donde vive cómo opera la empresa.**
- `foundations/`: Reglas de negocio core y procesos funcionales estables.
- `current_state.md`: Una fotografía consolidada del estado actual de la operación.

## Skills para Agentes IA

Si usas asistentes de IA, puedes instalarles las **Skills** proveídas en este repositorio (`skills/`). Al leerlas, el agente comprenderá instantáneamente cómo debe comportarse:

- `qmd-shared-memory/SKILL.md`: Para mantener la trazabilidad del trabajo diario.
- `asm-bootstrap/SKILL.md`: Para automatizar el "Onboarding" de una empresa (entrevista y generación automática de este repositorio).