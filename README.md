# WhatsApp AI Business Automation

An AI-powered customer message processing backend built with **n8n, Groq, and PostgreSQL**.

The workflow is designed to receive WhatsApp-style incoming messages through a webhook, understand the customer's request using an AI agent, extract structured information, detect duplicate messages, store conversation data, and return a clean response.

> **Note:** This repository contains the automation backend. A live WhatsApp Business/API account and credentials are not included.

## 🚀 Workflow

```text
Incoming Message
       ↓
    Webhook
       ↓
   Edit Fields
       ↓
    AI Agent
       ↓
  Groq LLM
       ↓
 Parse AI Output
       ↓
 Check Duplicate
       ↓
      IF
     ↙  ↘
Duplicate  New Message
   ↓          ↓
Response   PostgreSQL
              ↓
           Response
```

## ✨ Features

* 📱 WhatsApp-ready webhook endpoint
* 🤖 AI-powered message understanding
* 🧠 Structured customer intent extraction
* 📍 Location extraction
* 🏷️ Category detection
* 💰 Budget extraction
* 📋 Requirements extraction
* 🌐 Language detection
* 📝 Automatic conversation summaries
* 🔁 Duplicate message detection
* 🗄️ PostgreSQL conversation storage
* ⚡ Automated JSON responses
* 🧩 Modular n8n architecture

## 🧠 AI Extraction

The AI agent converts an incoming message into structured data:

```json
{
  "intent": "property_search",
  "name": "",
  "location": "Kazanchis",
  "category": "apartment",
  "requirements": [
    "2 bedrooms"
  ],
  "budget": "",
  "language": "English",
  "summary": "Customer is looking for a 2-bedroom apartment in Kazanchis.",
  "needs_human": false
}
```

The system is instructed not to invent information that the customer did not provide.

## 🗄️ Database

Conversation data is stored in PostgreSQL.

### `conversations`

| Field          | Type      | Description                       |
| -------------- | --------- | --------------------------------- |
| `id`           | SERIAL    | Unique conversation record        |
| `phone`        | VARCHAR   | Customer phone number             |
| `message`      | TEXT      | Original message                  |
| `message_type` | VARCHAR   | Message type                      |
| `intent`       | VARCHAR   | Detected customer intent          |
| `name`         | VARCHAR   | Customer name                     |
| `location`     | VARCHAR   | Requested location                |
| `category`     | VARCHAR   | Requested category                |
| `requirements` | JSONB     | Customer requirements             |
| `budget`       | VARCHAR   | Customer budget                   |
| `language`     | VARCHAR   | Detected language                 |
| `summary`      | TEXT      | AI-generated summary              |
| `needs_human`  | BOOLEAN   | Whether human support is required |
| `created_at`   | TIMESTAMP | Record creation time              |

## 🔄 Duplicate Detection

Before storing a new conversation, the workflow checks PostgreSQL for an existing message from the same phone number.

This helps prevent duplicate processing when the same message is received more than once.

## 🔌 Technologies

* **n8n** — Workflow automation
* **Groq** — Large language model inference
* **PostgreSQL** — Conversation database
* **Webhook API** — Incoming message interface
* **JavaScript** — AI output parsing and data transformation

## 📁 Repository Structure

```text
whatsapp-ai-business-automation/
│
├── workflow/
│   └── whatsapp-ai-agent.json
│
├── docs/
│   └── architecture.md
│
├── README.md
└── .gitignore
```

## ⚙️ Setup

### 1. Install n8n

Run n8n locally or deploy it on a server.

### 2. Import the workflow

Import:

```text
workflow/whatsapp-ai-agent.json
```

into n8n.

### 3. Configure Groq

Add your own Groq API credentials to the AI model node.

### 4. Configure PostgreSQL

Create a PostgreSQL credential in n8n and connect it to the PostgreSQL nodes.

### 5. Configure your messaging provider

The webhook is designed to accept incoming WhatsApp-style requests.

A WhatsApp Business/API provider can be connected later.

Example incoming request:

```json
{
  "phone": "251911111111",
  "message": "I need a 2 bedroom apartment in Kazanchis",
  "message_type": "text"
}
```

### 6. Activate the workflow

Once the webhook, AI model, database, and messaging provider are configured, activate the workflow.

## 🔐 Security

Never commit API keys or passwords to GitHub.

Credentials should be configured inside n8n using its credential system or environment variables.

The example workflow intentionally does **not** contain real API keys, passwords, or database credentials.

## 🎯 Use Cases

This architecture can be adapted for:

* Real estate customer inquiries
* E-commerce customer support
* Lead qualification
* Appointment requests
* Service businesses
* Customer support automation
* Sales lead collection
* WhatsApp AI assistants

## 🔮 Future Improvements

* WhatsApp Business API integration
* Conversation history and long-term memory
* Human-agent handoff
* CRM integration
* Property/product database search
* Multilingual Ethiopian-language support
* Lead scoring
* Analytics dashboard
* Authentication and webhook verification
* Improved duplicate detection
* Production error handling and logging

## 👨‍💻 Project Purpose

This project demonstrates how **AI agents, workflow automation, APIs, and databases** can be combined to build an intelligent customer communication backend.

It is designed as a portfolio project showcasing practical automation engineering with n8n and AI.

---

**Built with n8n + Groq + PostgreSQL**
