# LOW: Life Organizer & Work-assistant 🤖

LOW es un **Agente de Inteligencia Artificial Orquestador** construido sobre **n8n**. Funciona como un asistente personal integral que opera a través de WhatsApp, capaz de gestionar tareas complejas mediante el uso de herramientas especializadas (Sub-agentes).

```mermaid
graph TD
    %% Estilos
    classDef whatsapp fill:#25D366,stroke:#fff,stroke-width:2px,color:white;
    classDef n8n fill:#EA4B71,stroke:#333,stroke-width:2px,color:white;
    classDef ai fill:#722F37,stroke:#fff,stroke-width:2px,color:white;
    classDef drive fill:#4285F4,stroke:#fff,stroke-width:2px,color:white;
    classDef subagent fill:#FF9900,stroke:#333,stroke-width:2px,color:black;

    %% Inicio
    User((Usuario)) -->|Mensaje / Archivo| WA[WhatsApp Webhook]
    class WA whatsapp

    subgraph "LOW Orchestrator (Cerebro Central)"
        WA --> Auth{Validar Teléfono?}
        Auth -- No --> Ignore[Ignorar]
        Auth -- Si --> Memory[(Buffer Memory)]
        Memory --> Router{{AI Agent Router<br>GPT-4o-mini}}
        class Auth,Memory,Router n8n
    end

    %% Enrutamiento
    Router -->|Intención: CV| ResumeTailor
    Router -->|Intención: Carta| Duelist
    Router -->|Intención: Archivos| DriveMgr
    Router -->|Intención: Investigar| Researcher
    Router -->|Intención: RAG| VectorDB
    Router -->|Intención: Prompting| Prompter

    %% Sub-Agente 1: ResumeTailor
    subgraph "1. ResumeTailor (RRHH)"
        ResumeTailor(ResumeTailor Start) --> GetInfo[Info Retriever<br>Drive Manifesto]
        GetInfo --> Draft[GPT-4o Draft]
        Draft --> Eval{Evaluator<br>GPT-4.1 Score > 85?}
        Eval -- No --> Editor[Editor GPT-4<br>Apply Fixes]
        Editor --> Eval
        Eval -- Si --> LaTeX[Render LaTeX]
        LaTeX --> PDF[Convert to PDF]
        class ResumeTailor,GetInfo,Draft,Eval,Editor,LaTeX,PDF subagent
    end

    %% Sub-Agente 2: Duelist
    subgraph "2. DuelistCardCrafter (Creativo)"
        Duelist(Duelist Start) --> Concept[LLM Concept]
        Concept --> Dalle[DALL-E 3 Gen]
        Dalle --> Comp[Image Composition<br>Template + Text]
        class Duelist,Concept,Dalle,Comp subagent
    end

    %% Sub-Agente 3: Drive Manager
    subgraph "3. GoogleDriveManager"
        DriveMgr(DriveMgr Start) --> Gem[Gemini Router]
        Gem -->|Save| SaveVec[Upload + Vectorize]
        Gem -->|Search| SearchDr[Drive Search Tool]
        Gem -->|Download| DownDr[Get Binary]
        class DriveMgr,Gem,SaveVec,SearchDr,DownDr subagent
    end

    %% Sub-Agente 4: Researcher
    subgraph "4. Researcher (Academic)"
        Researcher(Researcher Start) --> Pre[Query Clean]
        Pre --> APIs[Crossref + Arxiv APIs]
        APIs --> Agg[Aggregate & Parse]
        Agg --> Report[GPT-4 Narrative Report]
        class Researcher,Pre,APIs,Agg,Report subagent
    end

    %% Sub-Agente 5: Vector Retriever
    subgraph "5. VectorRetriever (RAG)"
        VectorDB(Vector Start) --> Emb[Embeddings<br>ada-002]
        Emb --> Supabase[(Supabase Vector Store)]
        Supabase --> Context[Get Context]
        Context --> RAGAnswer[GPT-4.1 Answer]
        class VectorDB,Emb,Supabase,Context,RAGAnswer subagent
    end

    %% Sub-Agente 6: Prompter
    subgraph "6. Prompter (Meta-Tool)"
        Prompter(Prompter Start) --> Analyze[Analizar Intención]
        Analyze --> Struct[Generar Estructura<br>Prompt o Tool Def]
        class Prompter,Analyze,Struct subagent
    end

    %% Salidas
    PDF --> OutputWA[Enviar a WhatsApp]
    Comp --> OutputWA
    SaveVec --> OutputWA
    SearchDr --> OutputWA
    DownDr --> OutputWA
    Report --> OutputWA
    RAGAnswer --> OutputWA
    Struct --> OutputWA
    
    OutputWA --> User
    class OutputWA whatsapp
```

## 🚀 Características Principales

LOW no es un simple chatbot; es un enrutador inteligente que decide qué herramienta usar según la intención del usuario:

## 📂 Flujos de Trabajo (Workflows)

El sistema se compone de 7 flujos interconectados en n8n:

1.  **LOW (Orchestrator):** El cerebro central que gestiona WhatsApp y enruta las peticiones.
2.  **ResumeTailor:** Agente especializado en crear y optimizar CVs con LaTeX.
3.  **DuelistCardCrafter:** Generador de arte y cartas coleccionables con IA.
4.  **Researcher:** Buscador de papers académicos en Arxiv y Crossref.
5.  **GoogleDriveManager:** Gestor de archivos (subida/bajada) con indexación vectorial.
6.  **VectorRetriever:** Sistema RAG para consultas sobre la base de conocimiento propia.
7.  **Prompter:** Asistente para crear prompts y definiciones de herramientas de IA.

## 🛠️ Stack Tecnológico

*   **Core:** n8n (Workflow Automation).
*   **Modelos:** GPT-4o, GPT-4o-mini, DALL-E 3, text-embedding-ada-002.
*   **Database:** Supabase (Vector Store).
*   **Interface:** WhatsApp Business API.
*   **Integraciones:** Google Drive, Google Docs/Sheets.

## 📂 Estructura del Proyecto

Este repositorio contiene los flujos JSON para importar en n8n. Revisa la carpeta `/documentation` para detalles profundos de cada agente.

---
