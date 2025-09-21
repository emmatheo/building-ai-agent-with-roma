<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Build Your First AI Agent with ROMA</title>
</head>
<body style="font-family: Arial, sans-serif; line-height: 1.6; max-width: 900px; margin: auto;">

  <h1>🚀 Build Your First AI Agent with ROMA</h1>

  <p>
    This repository is a <strong>beginner-friendly tutorial</strong> on how to install, configure, and run your first AI agent 
    using <a href="https://github.com/sentient-agi/ROMA" target="_blank">ROMA</a>, 
    an open-source multi-agent framework by Sentient.
  </p>

  <p>With this guide, you’ll:</p>
  <ul>
    <li>✅ Install ROMA in your local environment</li>
    <li>✅ Create a custom <strong>Crypto Research Agent</strong></li>
    <li>✅ Add a <strong>CoinGecko price tool</strong></li>
    <li>✅ Run it in your browser</li>
  </ul>

  <hr>

  <h2>🧠 What is ROMA?</h2>
  <p>
    ROMA (<strong>Reasoning-Oriented Multi-Agent</strong>) is a framework for building and orchestrating AI agents.
  </p>
  <p>Key features:</p>
  <ul>
    <li>Agents defined in simple <strong>YAML configs</strong></li>
    <li>Powered by <strong>LLMs via OpenRouter</strong></li>
    <li>Agents can use <strong>custom tools</strong> (Python functions, APIs, scripts)</li>
    <li>Run and coordinate multiple agents at once</li>
  </ul>

  <p><em>Think of ROMA as an operating system for AI agents.</em></p>

  <hr>

  <h2>⚙️ Setup & Installation</h2>

  <h3>1. Clone ROMA</h3>
  <pre><code>git clone https://github.com/sentient-agi/ROMA.git
cd ROMA
</code></pre>

  <h3>2. Setup with Docker</h3>
  <pre><code>./setup.sh --docker
cd docker
docker compose up -d
</code></pre>

  <h3>3. Open in Browser</h3>
  <p>Go to 👉 <a href="http://localhost:3000">http://localhost:3000</a></p>
  <p>You should now see the <strong>ROMA dashboard</strong> running locally.</p>

  <hr>

  <h2>🤖 Create Your First Agent</h2>
  <p>Open the file:</p>
  <pre><code>ROMA/agent_configs/agents.yaml</code></pre>

  <p>Add this block:</p>
  <pre><code>agents:

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
</code></pre>

  <hr>

  <h2>🛠️ Add a Custom Tool</h2>
  <p>Create a new file:</p>
  <pre><code>ROMA/tools/coingecko.py</code></pre>

  <pre><code>import requests

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
</code></pre>

  <p>Then edit:</p>
  <pre><code>ROMA/tools/__init__.py</code></pre>

  <p>Add this line at the bottom:</p>
  <pre><code>from .coingecko import get_price</code></pre>

  <hr>

  <h2>▶️ Run & Test</h2>
  <p>Restart ROMA:</p>
  <pre><code>cd docker
docker compose down
docker compose up -d
</code></pre>

  <p>Now go back to 👉 <a href="http://localhost:3000">http://localhost:3000</a></p>

  <p>Select <strong>Crypto Researcher</strong> agent and try:</p>
  <ul>
    <li>“What’s the price of bitcoin?”</li>
    <li>“What’s the price of ethereum?”</li>
    <li>“Summarize today’s Solana news.”</li>
  </ul>

  <hr>

  <h2>📊 Example Flow Diagram</h2>
  <p><img src="images/roma-flow.png" alt="ROMA Agent Flow"><br>
  <em>(Agent → Tool → Response)</em></p>

  <hr>

  <h2>🌟 What’s Next?</h2>
  <ul>
    <li>Add more tools (Twitter API, Telegram bot, news scraper)</li>
    <li>Create multi-agent pipelines (Researcher → Writer → Publisher)</li>
    <li>Deploy your agent online</li>
  </ul>

  <hr>

  <h2>📚 References</h2>
  <ul>
    <li><a href="https://github.com/sentient-agi/ROMA">ROMA GitHub</a></li>
    <li><a href="https://openrouter.ai/">OpenRouter</a> for free API models</li>
  </ul>

  <hr>

  <h3>✍️ Author</h3>
  <p>
    This tutorial was created to help beginners start building with ROMA.<br>
    Pull requests, feedback, and forks are welcome! 🚀
  </p>

</body>
</html>
