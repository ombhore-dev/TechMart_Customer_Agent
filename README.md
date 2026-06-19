# TechMart AI Customer Support Agent 🛒🤖

> A production-style AI agent that automates e-commerce refund decisions using **GPT-4o, LangGraph, FastAPI & SQLite** — with full reasoning transparency.

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![OpenAI](https://img.shields.io/badge/GPT--4o-412991?style=for-the-badge&logo=openai&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

---

## 🎥 Demo

👉 [Watch Loom Walkthrough](https://www.loom.com/share/c9cd5abdb4f141fda46024aec820383a)

---

## 🔍 What It Does

TechMart simulates a real-world AI customer support workflow. A customer sends a refund request in natural language — the agent:

1. **Looks up** the customer profile + order history from a SQLite CRM
2. **Evaluates** refund eligibility using a deterministic policy engine (not the LLM)
3. **Responds** via GPT-4o with a warm, policy-grounded customer message
4. **Logs** every tool call, LLM invocation, and policy check for full auditability

> 💡 The LLM **never decides** refund outcomes — all approval/denial logic lives in the policy engine, making decisions auditable and consistent.

---

## ✨ Features

- 🤖 **LangGraph Agent** — `call_model → run_tools` loop with conditional edges
- 🔧 **GPT-4o Function Calling** — `lookup_customer` and `evaluate_refund` tools
- 📋 **Deterministic Policy Engine** — tier-based return windows (Standard 30d / Premium 45d / VIP 60d), open-box rules, high-value order conditions
- 🗄️ **SQLite CRM** — 15 pre-seeded customer profiles with order history
- 💬 **Chat Interface** — Clean HTML/CSS/JS frontend
- 🔍 **Reasoning Dashboard** — Real-time tool execution trace & policy check logs
- 🧪 **Automated Test Suite** — Pytest-based refund policy unit tests
- 🐳 **Docker Ready** — Containerized for easy deployment

---

## 🏗️ Architecture

```
User Message
      │
      ▼
FastAPI API Layer
      │
      ▼
LangGraph Agent (StateGraph)
      │
      ├── lookup_customer() ──► SQLite CRM
      │
      └── evaluate_refund() ──► Refund Policy Engine
                                        │
                                        ▼
                               APPROVED / DENIED /
                          APPROVED_WITH_CONDITIONS / NEEDS_INFO
                                        │
                                        ▼
                           GPT-4o formats final response
                                        │
                                        ▼
                        Frontend Chat + Reasoning Dashboard
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| LLM | OpenAI GPT-4o |
| Agent Framework | LangGraph |
| Backend API | FastAPI + Uvicorn |
| Database | SQLite |
| Frontend | HTML + CSS + JavaScript |
| Testing | Pytest |
| Config | python-dotenv |

---

## 🚀 Quick Start

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/TechMart_Customer_Agent.git
cd TechMart_Customer_Agent
```

### 2. Set up environment
```bash
cp .env.example .env
# Add your OpenAI API key to .env
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the app
```bash
python main.py
```

### 5. Open in browser
```
http://localhost:8000
```

---

## 🧪 Run Tests

```bash
pytest tests/
```

Tests cover the core refund policy engine — return window validation, open-box rules, VIP goodwill policy, and high-value order conditions.

---

## 📁 Project Structure

```
TechMart_Customer_Agent/
├── main.py                     # FastAPI entry point
├── requirements.txt
├── .env.example                # API key template
├── frontend/
│   └── index.html              # Chat UI + Reasoning Dashboard
├── backend/
│   ├── agents/
│   │   └── support_agent.py    # LangGraph agent + GPT-4o integration
│   ├── tools/
│   │   └── refund_tools.py     # Tool schemas + dispatch logic
│   ├── policies/
│   │   └── refund_policy.py    # Pure-function policy engine
│   ├── database/
│   │   └── crm.py              # SQLite CRM layer + seed data
│   └── api/
│       └── routes.py           # FastAPI router
└── tests/
    └── test_refund_engine.py   # Policy unit tests
```

---

## 🧾 Sample Test Customers

| Email | Tier | Scenario |
|---|---|---|
| priya.sharma@gmail.com | Premium | Standard refund request |
| sneha.iyer@gmail.com | VIP | High-value order (₹79,900) |
| vikram.singh@gmail.com | Standard | Previous denied refund on account |
| aditya.verma@gmail.com | VIP | Open-box laptop |

---

## 📌 Key Design Decisions

- **Policy-first architecture** — business rules are hardcoded Python, not prompt-engineered. This prevents the LLM from hallucinating refund approvals.
- **LangGraph for agent control flow** — explicit state machine makes the agent's reasoning easy to trace and debug.
- **Reasoning logs** — every LLM call, tool invocation, and policy check is timestamped and surfaced in the UI.

---

## 📄 License

MIT License — see [LICENSE](LICENSE)
