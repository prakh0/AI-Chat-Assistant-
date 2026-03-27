# AI Communication Assistant (WhatsApp + Gmail)

An end-to-end AI automation system that **reads, understands, and replies** to messages from:

-  WhatsApp (via webhook API)  
-  Gmail (via Gmail API)  

Powered by a locally running **Qwen LLM**, this system generates intelligent, human-like replies without relying on external paid APIs.

---

#  Demo

##  WhatsApp Interaction

**User:** Hi  
**Bot:** Hey! How can I help you today?

**User:** Can you help me with my order?  
**Bot:** Sure! Could you share your order details?

---

## 📧 Gmail Auto-Reply
*Email:*
**Subject:** Meeting tomorrow

Hi, are we still on for tomorrow?

**AI Reply:**
Hi! Yes, we’re on. What time works best for you?

---

# Features

- Real-time WhatsApp auto-replies  
- Automated Gmail responses  
- Multi-user session memory  
- Local LLM inference (Qwen 0.5B)  
- Email cleaning & truncation  
- Secure environment variable handling  

---

# Architecture

## WhatsApp Flow (Webhook-based)

    ┌──────────────┐
    │ WhatsApp API │
    └──────┬───────┘
           │  (Webhook via ngrok)
           ▼
    ┌──────────────┐
    │  FastAPI App │   ← main.py
    └──────┬───────┘
           ▼
    ┌──────────────┐
    │  LLM Model   │   ← model.py
    └──────────────┘

---

## Gmail Flow (Independent Script)

    ┌──────────────┐
    │  Gmail API   │
    └──────┬───────┘
           ▼
    ┌──────────────┐
    │ Gmail Script │   ← gmail.py
    └──────┬───────┘
           ▼
    ┌──────────────┐
    │  LLM Model   │   ← model.py
    └──────────────┘

---

# Prerequisites

- Python 3.10+  
- Gmail API credentials (OAuth)  
- WhatsApp API (Meta Cloud API / Twilio)  
- ngrok (for local tunneling)  

---

# Installation

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

---

# Environment Setup

- Create a .env file:
  ```
  EMAIL=your_email@gmail.com
  OAUTH_CREDENTIALS_FILE=Oauth_cred_chatbot_gmail.json
  VERIFY_TOKEN=your_verify_token
  ACCESS_TOKEN=your_whatsapp_access_token
  PHONE_NUMBER_ID=your_phone_number_id
  ```

  ---
  
# Running the Application

1. Start FastAPI Server (WhatsApp)
2. Expose with ngrok
3. Configure Webhook
**Set webhook URL:**
```
https://your-ngrok-url/webhook
```
# For Email Assistant
Run Gmail Auto-Reply
```python gmail.py```

---

# Core Components

## `main.py`

- FastAPI webhook server  
- Handles WhatsApp events  
- Routes messages to LLM  

## `gmail.py`

- Fetches unread emails  
- Cleans + truncates content  
- Sends AI-generated replies  

## `model.py`

- Loads Qwen LLM  
- Maintains session memory  
- Generates responses using chat templates  

---

# Performance Notes

- First run loads model into memory (~5–10 sec)  
- CPU inference: ~2–4 sec per response  
- Input size significantly affects latency  

---

# Tech Stack

- FastAPI
- Hugging Face Transformers
- PyTorch
- Gmail API
- WhatsApp API
- ngrok

---
