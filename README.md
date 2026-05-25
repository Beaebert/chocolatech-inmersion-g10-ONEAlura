# 🍫 ChocolaTech HR Agent — Workflow n8n + Telegram

> Proyecto de práctica desarrollado en el marco de la capacitación **Oracle Next Education (ONE) + Alura LATAM**, implementando un agente inteligente que responde consultas de empleados a través de Telegram.

---

## 📋 Descripción

Este repositorio contiene los recursos necesarios para construir un **workflow de automatización en n8n** que potencia a un agente conversacional en Telegram. El agente responde dudas de los empleados de **ChocolaTech** sobre políticas internas de Recursos Humanos, basándose en una base de conocimiento estructurada.

### 💬 ¿Cómo funciona?

Un empleado escribe en el chat de Telegram una consulta como:

- *"¿Cuántos días de licencia tengo por año?"*
- *"¿Cuál es la flexibilidad horaria semanal que puedo solicitar?"*
- *"¿Cuáles son los beneficios de viaje disponibles?"*

El agente procesa la pregunta, consulta la base de conocimiento y devuelve una respuesta clara y precisa, sin necesidad de contactar a RRHH directamente.

---

## 🗂️ Contenido del repositorio

| Archivo / Carpeta | Descripción |
|---|---|
| `knowledge-base/` | Documentos de normas y políticas internas de ChocolaTech |
| `workflow/` | Exportación del flujo n8n (`.json`) listo para importar |
| `prompts/` | Instrucciones del sistema utilizadas para el agente |
| `README.md` | Este archivo |

---

## 🧠 Base de conocimiento — Temas cubiertos

El agente puede responder consultas sobre las siguientes áreas de RRHH:

- 📅 **Licencias y ausencias** — días disponibles, procedimientos, tipos de licencia
- 🕐 **Horarios y flexibilidad** — horarios fijos, bancos de horas, trabajo remoto
- ✈️ **Beneficios de viaje** — viáticos, reembolsos, política de traslados
- 🤝 **Normas de conducta** — código de ética, convivencia y comportamiento
- 🎁 **Beneficios para empleados** — salud, capacitación, descuentos y más

---

## 🛠️ Tecnologías utilizadas

| Herramienta | Rol |
|---|---|
| **n8n** | Motor de automatización y orquestación del workflow |
| **Telegram Bot API** | Canal de comunicación con el empleado |
| **Cohere** | Embeddings para vectorizar la base de conocimiento + modelo de chat que genera las respuestas |
| **Railway** | Infraestructura en la nube donde corre la instancia de n8n |
| **Vector Store (RAG)** | Recuperación semántica de información desde los documentos de ChocolaTech |

---

## 🔍 ¿Qué es Cohere y para qué se usa aquí?

[Cohere](https://cohere.com/) es una plataforma de inteligencia artificial especializada en procesamiento de lenguaje natural (NLP). En este proyecto cumple **dos roles fundamentales**:

### 1. 📐 Embeddings — convertir texto en vectores

Los documentos de políticas de ChocolaTech (`.txt`) no pueden ser "buscados" semánticamente tal como están. Cohere los transforma en **vectores numéricos** (embeddings): representaciones matemáticas del significado de cada fragmento de texto.

```
"¿Cuántos días de licencia tengo?" 
        ↓ Cohere Embed
[0.021, -0.84, 0.33, 0.91, ...]  ← vector de alta dimensión
```

Esto permite que cuando un empleado hace una pregunta, el sistema encuentre los fragmentos más relevantes del reglamento **por similitud de significado**, no solo por palabras clave exactas.

### 2. 💬 Modelo de chat — generar la respuesta

Una vez recuperados los fragmentos relevantes, el **modelo de lenguaje de Cohere** (Command R o similar) recibe el contexto y la pregunta del empleado, y genera una respuesta natural, clara y basada exclusivamente en las políticas de ChocolaTech.

```
Contexto: [fragmentos del reglamento recuperados]
Pregunta: "¿Puedo pedir flexibilidad horaria?"
        ↓ Cohere Chat
Respuesta: "Sí, según el reglamento interno podés solicitar..."
```

---

## 🚂 ¿Qué es Railway y para qué se usa aquí?

[Railway](https://railway.app/) es una plataforma de infraestructura en la nube orientada a desarrolladores, pensada para desplegar aplicaciones y servicios de forma rápida y sin configuración compleja de servidores.

En este proyecto, Railway actúa como el **entorno donde vive y corre la instancia de n8n**:

- ☁️ **Hosting de n8n** — en lugar de ejecutar n8n localmente (solo en tu computadora), Railway lo mantiene corriendo en la nube de forma continua
- 🔄 **Disponibilidad 24/7** — el bot de Telegram puede recibir y responder mensajes en cualquier momento, sin necesidad de tener el equipo encendido
- 🔧 **Variables de entorno seguras** — las credenciales (tokens, API keys) se configuran de forma segura sin hardcodearlas en el código
- 📦 **Despliegue simple** — Railway levanta n8n desde una imagen de Docker con mínima configuración manual

---

## 🚀 Cómo usar este proyecto

### 1. Clonar el repositorio

```bash
git clone https://github.com/Beaebert/chocolatech-inmersion-g10-ONEAlura.git
```

### 2. Importar el workflow en n8n

1. Abrí tu instancia de **n8n**
2. Andá a **Workflows → Import from file**
3. Seleccioná el archivo `.json` de la carpeta `workflow/`

### 3. Configurar credenciales

- 🔑 **Telegram Bot Token** — Creá un bot con [@BotFather](https://t.me/BotFather) y copiá el token
- 🔑 **Cohere API Key** — para los nodos de embeddings y el modelo de chat ([obtené tu key acá](https://dashboard.cohere.com/api-keys))

### 4. Cargar la base de conocimiento

Subí los documentos de la carpeta `knowledge-base/` al Vector Store configurado en el workflow para que el agente tenga acceso a la información de ChocolaTech.

### 5. Activar el workflow

Activá el workflow en n8n y ¡listo! El bot de Telegram comenzará a responder consultas.

---

## 🎓 Contexto académico

Este proyecto fue desarrollado como práctica integradora de la **Inmersión en Automatización e IA** de:

- 🟠 **Oracle Next Education (ONE)**
- 🔵 **Alura LATAM**

El objetivo es aplicar conceptos de automatización, integración de APIs e inteligencia artificial generativa en un caso de uso empresarial real.

---

## 👩‍💻 Autora

**Beatriz Ebert** — Analista Funcional Técnica Jr. | Apasionada por el desarrollo .NET y la automatización con IA

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Beatriz%20Ebert-0077B5?style=flat&logo=linkedin)](https://www.linkedin.com/in/beatrizebert/)
[![GitHub](https://img.shields.io/badge/GitHub-Beaebert-181717?style=flat&logo=github)](https://github.com/Beaebert)

---

## 📄 Licencia

Este repositorio es de uso educativo. Los documentos de políticas de ChocolaTech son ficticios y fueron creados con fines de práctica.

## 📸 Demo

### Workflow en n8n
![Workflow n8n](./assets/workflow-n8n.png)

### Conversación en Telegram
![Demo Telegram](./assets/demo-telegram.png)
