# Researcher: Agente de Investigación Académica

**Archivo:** `researcher.json`

## Descripción
Este agente permite realizar investigaciones bibliográficas. Se conecta a APIs externas para buscar *papers* científicos y artículos, procesa la información y entrega un resumen estructurado.

![Imagen del flujo de researcher.json aquí](assets\research.png)

## Flujo de Trabajo

1.  **Pre-procesamiento (Code Node):** Limpia la consulta del usuario, valida la longitud y define parámetros de búsqueda (alcance, idioma, formato).
2.  **Búsqueda Paralela (APIs):**
    *   **Crossref API:** Busca metadatos de trabajos académicos.
    *   **Arxiv API:** Busca pre-prints científicos.
3.  **Agregación:** Fusiona los resultados de ambas fuentes.
4.  **Parsing y Formateo:** Convierte los datos JSON crudos (título, año, abstract) en un formato de texto legible.
5.  **Síntesis (LLM):** Un modelo GPT-4 toma la lista de artículos y genera un "Reporte Narrativo", resumiendo los hallazgos, destacando patrones y formateando la respuesta con emojis y estructura clara.