# Google Drive Manager: Operador de Archivos

**Archivo:** `google_drive_manager.json`

## Descripción
Herramienta utilitaria que permite a LOW interactuar directamente con el almacenamiento en la nube. Maneja la lógica de guardar, buscar y descargar archivos, además de indexarlos para búsquedas semánticas.

![Imagen del flujo de google_drive_manager.json aquí](../assets/drive.png)

## Flujo de Trabajo

1.  **Interpretación de Operación:** Un modelo **Gemini** analiza la solicitud para determinar la acción: `save_file`, `search_file`, o `download_file`.
2.  **Ejecución (Switch):**
    *   **Guardar:** Sube el archivo a Drive. Adicionalmente, usa un **Vector Store (Supabase)** para vectorizar el contenido del documento y hacerlo "buscable" por su significado en el futuro.
    *   **Buscar:** Utiliza la herramienta nativa de Google Drive para listar archivos que coincidan con la query.
    *   **Descargar:** Obtiene el binario del archivo por ID y lo prepara para envío.
3.  **Notificación:** Confirma la acción o envía el archivo solicitado al usuario vía WhatsApp.