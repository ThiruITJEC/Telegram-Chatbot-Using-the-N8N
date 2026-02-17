# Telegram-Chatbot-Using-the-N8N
An automated Telegram chatbot workflow built using n8n and OpenAI GPT, designed to generate neutral, authoritative responses in a global news reporting style.
**🤖 Telegram AI News Chatbot – n8n Workflow**

This project is an automation workflow built using n8n that integrates Telegram with OpenAI to generate AI-powered responses in a professional global news anchor tone.

🛠 n8n Tools Used in This Workflow

This workflow uses the following n8n nodes:

**1️⃣ Telegram Trigger Node**

Node Type: n8n-nodes-base.telegramTrigger

**📌 Purpose**

Listens for incoming messages from Telegram users.

Acts as the entry point of the workflow.

**⚙️ Configuration**

Update Type: message

Requires Telegram Bot API credentials.

Uses webhook-based communication.

**🔄 Output**

**Captures:**

message.text

message.chat.id

User details

**2️⃣ AI Agent Node (LangChain Agent)**

**Node Type:** @n8n/n8n-nodes-langchain.agent

**📌 Purpose**

Processes incoming user messages.

Sends the message to the connected language model.

Applies a system prompt to control tone and style.

**🧠 System Prompt Used**

The agent is configured to respond as:

A global news anchor delivering professional, neutral, and authoritative responses.

**🔄 Input**

Receives {{$json.message.text}} from Telegram Trigger.

**🔄 Output**

Returns AI-generated structured response.

**3️⃣ OpenAI Chat Model Node**

Node Type: @n8n/n8n-nodes-langchain.lmChatOpenAi

**📌 Purpose**

Connects to OpenAI's language model.

Generates AI responses.

**⚙️ Configuration**

Model: gpt-5-mini (configurable)

Requires OpenAI API credentials.

Connected to AI Agent via ai_languageModel input.

**🔄 Function**

Acts as the LLM backend for the AI Agent.

**4️⃣ Telegram Send Message Node**

Node Type: n8n-nodes-base.telegram

**📌 Purpose**

Sends the AI-generated response back to the user.

**⚙️ Configuration**

Chat ID: {{$('Telegram Trigger').item.json.message.chat.id}}

Text: {{$json.output}}

**🔄 Function**

Completes the request-response cycle.

**🔄 Workflow Architecture**
**Telegram Trigger
        ↓
AI Agent (LangChain)
        ↓
OpenAI Chat Model
        ↓
Send Telegram Message**

**🧩 How the Tools Work Together
**
Telegram Trigger captures user input.

AI Agent applies the news-style system prompt.

OpenAI model generates the response.

Telegram node sends the formatted reply.

**🔐 Required Credentials in n8n**

You must configure:

✅ Telegram API Credentials (Bot Token)

✅ OpenAI API Key

🚀 Deployment Notes

Works in local n8n setup

Can be deployed using Docker

Requires public webhook URL for production (ngrok / VPS / Cloud)

**📌 Why n8n?**

Low-code automation

Easy API integrations

Credential management

Workflow-based architecture

Scalable & extensible
