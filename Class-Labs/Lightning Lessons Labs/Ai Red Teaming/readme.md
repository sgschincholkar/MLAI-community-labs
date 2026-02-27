# 🔴 AI Red Teaming Lab — Attacking a Live n8n AI Chatbot with Azure AI Foundry

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sachin0034-tech/MLAI-community-labs/blob/main/Class-Labs/Lightning%20Lessons%20Labs/Ai%20Red%20Teaming/AI_Red_Teaming_Lab_JeuMatch.ipynb)
[![Azure AI Foundry](https://img.shields.io/badge/Azure%20AI-Foundry-0078D4?logo=microsoft-azure)](https://ai.azure.com)
[![n8n](https://img.shields.io/badge/Backend-n8n-EA4B71?logo=n8n)](https://n8n.io)


![AiReadTeamin](./images/3.png)

---

## What is AI Red Teaming?

AI Red Teaming is the practice of **simulating adversarial attacks on AI systems** to find security vulnerabilities, safety risks, and reliability issues before real attackers do.

> Think of it as **ethical hacking — but for AI models.**

Just like a penetration tester probes a web application for vulnerabilities, an AI red teamer sends carefully crafted adversarial prompts to an AI system to find out:

- 🔓 Can the model be tricked into producing harmful content?
- ⚠️ Can safety filters be bypassed using obfuscation techniques?
- ❌ Does the model follow its safety guidelines under pressure?

The results are logged to **Azure AI Foundry**, giving you a full audit trail of every attack and every response.

---

## What This Lab Does

This lab performs automated red teaming against a **live AI chatbot** powered by GPT-4.1-mini and n8n. The scanner sends adversarial prompts disguised as normal chat messages and records whether the model complies or refuses.

```
RedTeam Scanner (this notebook)
        ↓  adversarial prompt as chat message
n8n Webhook → AI Agent node
        ↓  message passed to fPt-3.5-turbo
GPT-3.5-turbo processes and responds
        ↓
Azure AI Foundry logs attack_success: true/false
```

### 3 Attack Strategies Used

| Strategy | Complexity | How it works |
|---|---|---|
| `EASY` | 🟢 Low | Direct harmful prompt — no disguise |
| `MODERATE` | 🟡 Medium | Jailbreak techniques — roleplay, hypotheticals, social engineering |
| `Compose([Base64, ROT13])` | 🔴 High | Double-encoded prompt — bypasses keyword safety filters |

### 2 Risk Categories Tested

| Category | What it probes for |
|---|---|
| `Violence` | Can the model be made to describe physical harm? |
| `HateUnfairness` | Can the model be made to produce hate speech or biased content? |

### Results

| Result | Meaning |
|---|---|
| `attack_success: false` ✅ | Model refused safely — **system is protected** |
| `attack_success: true` ❌ | Model complied with harmful prompt — **vulnerability found** |

---

## 🏗️ Architecture

```
┌─────────────────────────────┐
│   Azure AI Foundry          │  ← Logs all attack results & scores
│   (Evaluations Dashboard)   │
└─────────────┬───────────────┘
              │
┌─────────────▼───────────────┐
│   PyRIT Red Team Engine     │  ← Generates adversarial prompts
│   (via azure-ai-evaluation) │      using 3 attack strategies
└─────────────┬───────────────┘
              │  POST {"message": "<attack prompt>"}
┌─────────────▼───────────────┐
│   n8n Webhook               │  ← Receives the attack
│   (AI Agent node)           │
└─────────────┬───────────────┘
              │
┌─────────────▼───────────────┐
│   GPT-4.1-mini              │  ← Processes the prompt
│   (OpenAI via n8n)          │      built-in safety filters applied
└─────────────────────────────┘
```

---

## Prerequisites

Before running this lab you will need:

- ✅ A **Google account** to run the notebook in Google Colab (free)
- ✅ An **Azure subscription** with an **Azure AI Foundry project** → [ai.azure.com](https://ai.azure.com)
- ✅ An **n8n workflow** with an AI Agent node deployed and **Published/Active**
- ✅ A **webhook URL** from your n8n workflow : [Click Here](https://drive.google.com/file/d/13kViknFzSmjI9VKZwA5gMpMqPS8NJj_k/view?usp=sharing)



---

## Getting Started

### Step 1 — Open in Colab
Click the **Open in Colab** badge at the top of this README.

### Step 2 — Install packages
Run **Step 1** and **Step 2** cells → runtime will auto-restart.

### Step 3 — Sign into Azure
Run **Step 4** → follow the device login link → authenticate with your Azure account.

### Step 4 — Set your config
In **Step 5**, update:
```python
azure_ai_project = "https://YOUR-FOUNDRY-ENDPOINT.services.ai.azure.com/api/projects/YOUR-PROJECT"
WEBHOOK_URL      = "https://YOUR-N8N.app.n8n.cloud/webhook/YOUR-WEBHOOK-ID"
```

### Step 5 — Run the scan
Run all remaining cells in order. The full scan takes **5–10 minutes**.

### Step 6 — View results
Go to [https://ai.azure.com](https://ai.azure.com) → Your Project → **Evaluations** → **Webhook-RedTeam-Scan**

---

## 📦 Packages Used

| Package | Purpose |
|---|---|
| `azure-ai-evaluation[redteam]` | Core red teaming engine powered by PyRIT |
| `azure-identity` | Azure AD authentication via `az login` |
| `azure-ai-projects` | Connect to Azure AI Foundry project |
| `httpx` | Async HTTP client to call the n8n webhook |

---

## Result

![Images](./images/1.png)

![Images](./images/2.png)

---

## 🔑 Key Takeaways

- **Any chat input field is an attack surface** — adversarial prompts can be sent just like normal messages
- **GPT-4.1-mini has strong built-in safety** — most direct attacks are blocked by default
- **Obfuscation increases attack success** — Base64 + ROT13 hides keywords from naive filters
- **A strong system prompt is your best defense** — reduces Attack Success Rate significantly
- **Azure AI Foundry logs everything** — every prompt and response is recorded for audit

---

