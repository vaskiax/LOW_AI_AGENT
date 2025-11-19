# Vector Database Retriever: Memoria de Largo Plazo (RAG)

**Archivo:** `vector database retriever final.json`

## Descripción
Es el sistema de **RAG (Retrieval-Augmented Generation)**. Permite a LOW responder preguntas basándose en una base de conocimiento privada (documentos previamente guardados y vectorizados en Supabase), en lugar de usar solo su conocimiento general.

![Imagen del flujo de vector_database_retriever.json aquí](assets/rag.png)

## Flujo de Trabajo

1.  **Input:** Recibe una pregunta específica del usuario.
2.  **Embedding:** Convierte la pregunta en un vector numérico usando el modelo `text-embedding-ada-002` de OpenAI.
3.  **Búsqueda Vectorial (Supabase):** Compara el vector de la pregunta con los vectores de los documentos almacenados para encontrar los fragmentos de texto más relevantes (similitud semántica).
4.  **Síntesis (Agente RAG):**
    *   Recibe los fragmentos de texto recuperados.
    *   Utiliza GPT-4.1-mini para construir una respuesta que conteste la pregunta del usuario *exclusivamente* usando esa información recuperada.
5.  **Salida:** Devuelve la respuesta en texto plano.