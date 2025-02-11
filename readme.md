# 📌 Chatbot con Base de Datos e Integraciones

Este proyecto describe un flujo de trabajo que integra múltiples sistemas para mejorar la interacción con bases de datos y fuentes de información externas. Se basa en la recuperación de información desde almacenes vectoriales utilizando **Pinecone**, el procesamiento con **OpenAI**, y la automatización con **n8n**. Además, **Evolution API está configurado con RabbitMQ** para facilitar su escalamiento.

---

## 🔹 Flujo General

### 1️⃣ **Recepción de Mensajes**
- Se activa un `Webhook Trigger` que recibe un mensaje entrante.
- Se evalúa si el mensaje contiene un documento o texto común.

### 2️⃣ **Procesamiento de Mensajes**
- Se realiza un `Switch` para diferenciar entre texto normal o documentos.
- Se envía un menú dependiendo de la clasificación del mensaje.

### 3️⃣ **Chat con Base de Datos**
- Se ejecuta el `Select Prompt` para determinar la pregunta.
- Se realiza la consulta con `Question and Answer Chain`.
- Se buscan respuestas en el **almacén vectorial Pinecone**.
- Se utiliza **OpenAI** para mejorar la respuesta generada.
- Se envía la respuesta final al usuario.

---

## 🔹 Integraciones Externas

### 🔎 **Búsqueda en Evolution API**
- Se ejecuta un `Schedule Trigger` para buscar información histórica.
- Se convierte la data en **JSON**.
- Se almacena en **Pinecone Vector Store**.
- Se procesan los datos con embeddings de **OpenAI**.
- Se utiliza `Recursive Character Text Splitter` para mejorar el almacenamiento.
- Se envía la información procesada a la API.
- **Evolution API está configurado con RabbitMQ** para escalabilidad y procesamiento distribuido.

### 📒 **Búsqueda en Notion**
- Se ejecuta un `Schedule Trigger` para extraer información.
- Se realiza una petición HTTP a **Notion**.
- Se limpia la información extraída.
- Se convierte la data en **JSON**.
- Se almacena en **Pinecone Vector Store**.
- Se procesan los datos con embeddings de **OpenAI**.
- Se utiliza `Recursive Character Text Splitter`.
- Se envía la información procesada a la API para su uso.

---

## 🔹 Escalabilidad con RabbitMQ

Para manejar grandes volúmenes de datos y consultas concurrentes, **Evolution API está configurado con RabbitMQ**. Esto permite:
- **Balanceo de carga automático** en la ejecución de consultas.
- **Procesamiento distribuido** para evitar cuellos de botella.
- **Eficiencia en la recuperación de datos** desde Pinecone y OpenAI.

---

## 🚀 Tecnologías Utilizadas
- **n8n** → Automatización del flujo.
- **OpenAI** → Embeddings y procesamiento de lenguaje natural.
- **Pinecone** → Almacén de datos vectoriales.
- **Notion API** → Recuperación de información documental.
- **Evolution API con RabbitMQ** → Procesamiento distribuido y escalable.

---

## 📌 Contribuciones
Si deseas mejorar este flujo, puedes contribuir mediante **pull requests** o reportar problemas en la sección de issues.

---

## 🛠️ Futuras Mejoras
- Implementación de análisis semántico avanzado.
- Integración con más bases de datos.
- Mejora en la eficiencia de almacenamiento de vectores.

