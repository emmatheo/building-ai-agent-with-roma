# building-ai-agen# 🚀 Build Your First AI Agent with ROMA  

This repository is a **beginner-friendly tutorial** on how to install, configure, and run your first AI agent using [ROMA](https://github.com/sentient-agi/ROMA), an open-source multi-agent framework by Sentient.  

With this guide, you’ll:  
✅ Install ROMA in your local environment  
✅ Create a custom **Crypto Research Agent**  
✅ Add a **CoinGecko price tool**  
✅ Run it in your browser  

---

## 🧠 What is ROMA?  
ROMA (**Reasoning-Oriented Multi-Agent**) is a framework for building and orchestrating AI agents.  

Key features:  
- Agents defined in simple **YAML configs**  
- Powered by **LLMs via OpenRouter**  
- Agents can use **custom tools** (Python functions, APIs, scripts)  
- Run and coordinate multiple agents at once  

Think of ROMA as an **operating system for AI agents**.  

---

## ⚙️ Setup & Installation  

### 1. Clone ROMA
```bash
git clone https://github.com/sentient-agi/ROMA.git
cd ROMA
t-with-roma
Beginner-friendly tutorial on building your first AI agent using ROMA
./setup.sh --docker
cd docker
docker compose up -d
Open in Browser

Go to:
👉 http://localhost:3000

You should now see the ROMA dashboard running locally.

.

🤖 Create Your First Agent

Open the file:

ROMA/agent_configs/agents.yaml


Add this block:
agents:

  - id: crypto_researcher
    name: Crypto Researcher
    description: "Finds and summarizes latest crypto insights."
    role: researcher
    goals:
      - Search for crypto news
      - Summarize into simple insights
      - Give token price updates
    model: openrouter/deepseek/deepseek-chat-v3.1:free
    tools:
      - get_price
Add a Custom Tool

Create a new file:
import requests

def get_price(coin: str, currency: str = "usd") -> str:
    """
    Fetch the current price of a coin from CoinGecko.
    Example: get_price("bitcoin", "usd")
    """
    url = f"https://api.coingecko.com/api/v3/simple/price?ids={coin}&vs_currencies={currency}"
    try:
        res = requests.get(url, timeout=10).json()
        if coin in res:
            return f"The current {coin} price is {res[coin][currency]} {currency.upper()}"
        return f"Could not find price for {coin}"
    except Exception as e:
        return f"Error fetching price: {str(e)}"
