# 🧠 Marketing Campaign Assistant (Google ADK)

This project is a **multi-agent marketing campaign assistant** built using the **Google ADK (Agent Development Kit)**.  
It automates the creation of a complete marketing campaign brief—from market research to ad copy and visual suggestions—powered by **Gemini models**.

---

## 🚀 Features

- **Sequential multi-agent pipeline** using `SequentialAgent`
- Automated **market research**, **messaging strategy**, **ad copywriting**, and **visual concept generation**
- Uses **Google Search** via ADK tools for real-world research
- Outputs a final **Markdown-formatted campaign brief**
- Easy configuration with `.env` file for environment variables

---

## 🧩 Project Structure

```
marketing_campaign_agent/
│
├── __init__.py               # Initializes the agent module
├── agent.py                  # Defines the agent orchestration and all sub-agents
├── instructions.py           # Holds prompt instructions for each agent role
└── .env                      # Contains environment variables for API configuration
```

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/marketing-campaign-agent.git
cd marketing-campaign-agent
```

### 2. Create and Activate a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
```

### 3. Install Dependencies

You need to have the **Google ADK SDK** and **dotenv** installed.

```bash
pip install google-adk python-dotenv
```

*(If Google ADK is not on PyPI yet, install it from its GitHub or internal source as per your environment.)*

---

## 🔑 Environment Variables

Your `.env` file should look like this:

```bash
GOOGLE_API_KEY=your-google-api-key
GOOGLE_GENAI_MODEL=gemini-2.0-flash
GOOGLE_GENAI_USE_VERTEXAI=FALSE
```

These variables are automatically loaded via `dotenv` in `agent.py`.

---

## 🧠 Agent Overview

The project defines a **SequentialAgent pipeline** consisting of specialized sub-agents:

| Agent Name | Role | Input | Output Key |
|-------------|------|--------|-------------|
| `MarketResearcher` | Conducts market research using Google Search | Product idea | `market_research_summary` |
| `MessagingStrategist` | Crafts core messages & value propositions | Market research summary | `key_messaging` |
| `AdCopyWriter` | Creates ad copy variations | Key messaging | `ad_copy_variations` |
| `VisualSuggester` | Suggests visual ideas | Ad copy | `visual_concepts` |
| `CampaignBriefFormatter` | Combines all outputs into a final Markdown brief | All previous outputs | `final_campaign_brief` |

The orchestrator agent (`MarketingCampaignAssistant`) coordinates all these steps automatically.

---

## 🧰 How It Works

1. The **user** provides a new product idea (e.g., “AI-powered fitness app”).
2. The **root agent** (`campaign_orchestrator`) triggers a chain of agents.
3. Each agent performs its task and stores its result in the shared `state`.
4. The **final output** is a complete marketing campaign brief in Markdown format.

Example flow:

```
Product Idea ➜ Market Research ➜ Messaging Strategy ➜ Ad Copy ➜ Visual Concepts ➜ Final Campaign Brief
```

---

## ▶️ Running the Agent

You can initialize and run the campaign orchestrator in Python:

```python
from marketing_campaign_agent.agent import root_agent

# Provide a product idea
result = root_agent.run("A smart water bottle that tracks hydration and sends reminders")

print(result["final_campaign_brief"])
```

This will print out a structured **marketing campaign brief** in Markdown.

---

## 🧪 Example Output

```markdown
# Marketing Campaign Brief

## Market Insights
- The smart hydration market is growing rapidly...
- Key competitors include...

## Key Messaging
- “Stay hydrated, stay smart.”
- “Your bottle knows you better.”

## Ad Copy
**Tweet:** "Never forget to drink water again 💧 SmartBottle keeps your hydration on track!"
**Headline:** "Smart Hydration for a Smarter You"

## Visual Concepts
- Minimalist product photos with blue and white tones
- Lifestyle shots of athletes using the bottle
```

---

## 🧱 Built With

- [Google ADK (Agent Development Kit)](https://github.com/google/adk)
- [Gemini 2.0 Flash Model](https://cloud.google.com/vertex-ai/generative-ai/docs/models)
- [Python Dotenv](https://pypi.org/project/python-dotenv/)

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
