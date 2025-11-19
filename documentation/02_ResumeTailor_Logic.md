# ResumeTailor: Agente de RRHH Autónomo

**Archivo:** `ResumeTailor.json`

## Descripción
Una herramienta compleja diseñada para crear hojas de vida hiper-personalizadas. No se limita a escribir; investiga, redacta, se auto-evalúa y genera documentos finales en PDF.

![Imagen del flujo de ResumeTailor.json aquí](assets\cv.png)

## Flujo de Trabajo

1.  **Input:** Recibe una URL de una oferta de trabajo.
2.  **Recuperación de Información (Info Retriever):**
    *   Analiza un "Manifiesto" en Google Drive.
    *   Extrae datos personales (experiencia, educación, skills) desde archivos específicos (Google Docs y Sheets).
3.  **Generación de Borrador (Sketch Creator):** Redacta un primer borrador del CV en Markdown adaptado a la oferta usando GPT-4.
4.  **Ciclo de Evaluación y Mejora:**
    *   **Evaluator (GPT-4.1):** Actúa como un reclutador crítico. Asigna un puntaje (0-100) y genera recomendaciones.
    *   **Logic Gate:** Si el puntaje es < 85, pasa al editor.
    *   **Editor (GPT-4):** Reescribe el CV aplicando las recomendaciones del evaluador.
5.  **Renderizado:**
    *   Convierte el Markdown final a código **LaTeX** profesional.
    *   Convierte el código a un archivo binario (PDF).
6.  **Entrega:** Sube el archivo a Google Drive y lo envía por WhatsApp al usuario.