## 🔐 Credenciales Requeridas para n8n

Para que el agente **LOW** y sus herramientas funcionen correctamente, debes configurar las siguientes credenciales en tu instancia de n8n.

### 🧠 Inteligencia Artificial
*   **OpenAI API (`openAiApi`):**
    *   Necesaria para: GPT-4o, GPT-4o-mini, DALL-E 3 y Embeddings.
    *   Requisito: Una API Key activa con saldo en [platform.openai.com](https://platform.openai.com).
*   **Google Gemini / PaLM (`googlePalmApi`):**
    *   Necesaria para: El enrutador del gestor de archivos y el Prompter.
    *   Requisito: API Key de Google AI Studio.

### ☁️ Google Cloud Platform (OAuth2)
Para que LOW acceda a tu Drive, Docs y Sheets, necesitas un proyecto en Google Cloud Console con las siguientes APIs habilitadas y credenciales OAuth configuradas:

*   **Google Drive OAuth2 (`googleDriveOAuth2Api`):** Para guardar/descargar archivos y buscar el manifiesto.
*   **Google Docs OAuth2 (`googleDocsOAuth2Api`):** Para leer tus plantillas de CV y escribir el resultado.
*   **Google Sheets OAuth2 (`googleSheetsOAuth2Api`):** Para leer tus datos estructurados (experiencia, educación).

> 💡 **Nota:** Puedes usar el mismo *Client ID* y *Client Secret* para las tres credenciales en n8n, pero debes autenticar cada una por separado.

### 💬 Mensajería (WhatsApp)
*   **WhatsApp Cloud API (`whatsAppApi` y `whatsAppTriggerApi`):**
    *   Necesaria para: Recibir mensajes y enviar respuestas (Texto, PDFs, Imágenes).
    *   Requisito: Una cuenta en Meta for Developers con un número de teléfono de prueba o producción configurado. Necesitarás el `Access Token` y el `Phone Number ID`.

### 🗄️ Base de Datos Vectorial
*   **Supabase API (`supabaseApi`):**
    *   Necesaria para: El sistema RAG (VectorRetriever) y almacenar el conocimiento.
    *   Requisito: La `Project URL` y la `Service Role Key` (o Anon Key) de tu proyecto en Supabase.

### 🌐 Otros
*   **HTTP Bearer Auth:**
    *   Utilizada en algunos nodos para descargar archivos multimedia de WhatsApp de forma segura utilizando el Token de Meta.