# LOW: (Orchestrator)

**Archivo:** `LOW.json`

## Descripción
Este es el **Agente Principal** y punto de entrada del sistema. Actúa como un enrutador inteligente que recibe mensajes de WhatsApp, mantiene el contexto de la conversación (memoria) y decide qué herramienta subalterna ejecutar para satisfacer la solicitud del usuario.

![Imagen del flujo de LOW.json aquí](../assets/low.png)

## Flujo de Trabajo

1.  **Trigger (WhatsApp):** Se activa al recibir un mensaje.
2.  **Filtro de Seguridad:** Verifica que el `wa_id` (número de teléfono) corresponda al administrador autorizado.
3.  **Gestión de Memoria:** Utiliza un nodo `Memory Buffer Window` vinculado al ID del usuario para recordar los últimos 10 turnos de conversación.
4.  **Cerebro Central (AI Agent):**
    *   Utiliza el modelo **GPT-4o-mini**.
    *   Tiene instrucciones de sistema (System Prompt) para actuar como un orquestador.
    *   Evalúa la intención del usuario y enruta la solicitud a una de las siguientes herramientas disponibles:
        *   `ResumeTailor`: Para hojas de vida.
        *   `DuelistCardCrafter`: Para cartas creativas.
        *   `google_drive_manager`: Para archivos.
        *   `researcher`: Para búsquedas web/académicas.
        *   `prompter`: Para generar estructuras de IA.
        *   `vector database retriever final`: Para consultas de conocimiento interno.
5.  **Respuesta:** Envía el resultado final (texto o medios) de vuelta al usuario por WhatsApp.