<img src="images/reg_ai.jpg" width=1000 height=250>

# How can I quickly find AI laws and regulations?

[Connect your AI assistant to AI regulation data](https://regulations.ai/mcp) and use the free MCP server that gives live access to AI laws world-wide.  Here's the first example of the key features along with validation of results.  *Results currently under review*

```
$ python3 ai_regulations_chat.py 
Initializing connection to regulations.ai MCP server...
MCP handshake successful.
```

### TEST CASE 1: "What are the AI laws in California?"

```
   🤖 Ollama invoked tool: `search_regulations` with args {"jurisdiction": "California", "query": "AI laws"}
      Retrieved live data from MCP server.
```

📝 **AI Analysis Response:**

The AI laws in California include:

1. Health care professions: deceptive terms or letters: artificial intelligence. (AB 489, enacted as Chapter 615 of the Statutes of 2025)
2. [California Executive Order N-9-26 — Independent Oversight of Frontier AI](https://www.gov.ca.gov/wp-content/uploads/2026/09/FINAL-N-9-26-AI-EO-9.18.26-SIGNED.pdf)
3. California SB 243 - Companion Chatbot Disclosure Requirements (enacted as Chapter 677 of the Statutes of 2025)

VALIDATION:  This information is true.  Search [Legiscan](https://legiscan.com/gaits/search?sort=desc&order=Status&state=CA&keyword=artificial%20intelligence) for current legislation.


### TEST CASE 2: "What has moved recently in AI regulation according to recent changes?"

```
🤖 Ollama invoked tool: `recent_changes` with args {}
      Retrieved live data from MCP server.
```

📝 **AI Analysis Response:**

The AI regulation tracker shows changes in AI regulations worldwide. The recent changes include:

1. Luxembourg AI Act Implementation Bill: This bill aims to implement the [EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng) in Luxembourg and includes provisions on governance oversight, market surveillance, and enforcement penalties.
2. Kazakhstan AI Administrative Penalties Law: This law introduces new fines and sanctions for AI-related offenses, including disclosure failures and harmful failures to manage high-risk systems.
3. Italy ChatGPT Privacy Safeguards Order: This regulation requires companies to implement ChatGPT privacy safeguards and provides a framework for data protection and transparency.
4. UK Workplace AI and Workers' Rights Bill: This bill aims to regulate AI technologies in the workplace and provide workers' rights, but its status is stalled.
5. Finland AI Supervision Act: This act supplements the EU AI Act by allocating supervision, designating a central contact point, and creating an administrative sanctions board.

These changes demonstrate the growing importance of AI regulation worldwide, with countries implementing their own laws and regulations to address the risks and benefits of AI technologies.

VALIDATION:  The term "recent" is vague.  

1.  As of November 7, 2026, there is no dedicated national legislative act governing AI in Luxembourg. However, Luxembourg is directly subject to the Regulation (EU) 2024/1689 – Artificial Intelligence Act (“EU AI Act”), which establishes harmonised rules for AI across all EU member states. The Act introduces a risk-based approach, banning certain harmful AI practices, and imposes strict obligations on high-risk and general-purpose AI systems.  Bill of law 8476 was submitted to the Parliament on 23 December 2024 and supplements the EU AI Act with the necessary national provisions for Luxembourg.  It is still under discussion.
2. Kazakhstan introduced [new fines and sanctions for AI-related offenses](https://en.orda.kz/kazakhstan-introduces-fines-for-misuse-of-artificial-intelligence-9324/) in November 2025.
3.  [Artificial intelligence: stop to ChatGPT by the Italian SA Personal data is collected unlawfully, no age verification system is in place for children](https://www.garanteprivacy.it/web/guest/home/docweb/-/docweb-display/docweb/9870847#english) was enacted in March 2023.
4.  



### TEST CASE 3: "Search for enforcement actions or litigation related to artificial intelligence."
```
   🤖 Ollama invoked tool: `search` with args {"query": "enforcement actions or litigation artificial intelligence"}
      Retrieved live data from MCP server.
```

📝 **AI Analysis Response:**

Here are some enforcement actions and litigation related to artificial intelligence:

1. Louisiana AI Medical Transcription Disclosure (Regulation ID: RAI-US-LA-HB47500-2026)
2. AI, Governance and Ethics: Global Perspectives. (Research Paper)
3. A robust governance for the AI act: AI office, AI Board, scientific panel, and national authorities (Research Paper)
4. Assessing European Union Member States' Implementation of the Artificial Intelligence Act (Research Paper)
5. Towards the effective extraterritorial enforcement of the AI Act (Research Paper)
6. Artificial intelligence in governance: recent trends, risks, challenges, innovative frameworks and future directions (Research Paper)
7. Artificial intelligence policy worldwide: a comparative analysis (Research Paper)
8. Agencia de Acceso a la Informacion Publica (AAIP) v Public and private entities using AI (Enforcement Action)
9. Berlin Commissioner for Data Protection (BlnBDI) v Hangzhou DeepSeek Artificial Intelligence Co., Ltd. (Enforcement Action)

These sources provide information on various aspects of artificial intelligence, including governance, ethics, implementation, and enforcement. They also highlight the importance of regulating AI to ensure its safe and responsible use.


### TEST CASE 4: "List the available tools and jurisdictions covered on regulations.ai."

```   🤖 Ollama invoked tool: `search` with args {"query": "available tools and jurisdictions covered"}
      Retrieved live data from MCP server.
```

📝 **AI Analysis Response:**
Based on the search results provided, the available tools covered on regulations.ai include:

1. Spanish Data Protection Agency (AEPD)
2. Autoridade Nacional de Proteção de Dados (ANPD) - Brazil
3. Bavarian State Office for Data Protection Supervision (BayLDA) - Germany
4. Garante per la protezione dei dati personali - Italy
5. High Court of Kenya (judicial review)
6. National Privacy Commission (NPC) - Philippines
7. Federal Trade Commission (FTC) - United States

As for the jurisdictions covered, the search results provide information on the following:

1. Spain
2. Brazil
3. Germany
4. Italy
5. Kenya
6. Philippines
7. United States

These jurisdictions have been involved in cases related to AI regulation, data protection,
and privacy, and the search results provide information on the enforcement actions taken by these authorities.

### Python script

```
import json
import urllib.request
import urllib.error
import sys

try:
    import ollama
except ImportError:
    print("Error: The 'ollama' package is required. Install it using: pip install ollama")
    sys.exit(1)

SERVER_URL = "https://regulations.ai/api/mcp/v1"
OLLAMA_MODEL = "llama3.2:latest"
API_KEY = None  # Optional: "using an API key raises the response limits

TEST_QUESTIONS = [
    "What are the AI laws in California?",
    "What has moved recently in AI regulation according to recent changes?",
    "Search for enforcement actions or litigation related to artificial intelligence.",
    "List the available tools and jurisdictions covered on regulations.ai."
]


def call_mcp_server(method: str, params: dict, request_id: int = 1) -> dict:
    """Sends JSON-RPC 2.0 requests to the regulations.ai MCP server using native urllib."""
    headers = {
        "Content-Type": "application/json",
        "Accept": "application/json, text/event-stream",
        "User-Agent": "Legal-Chat-Ollama-Client/1.0"
    }
    if API_KEY:
        headers["Authorization"] = f"Bearer {API_KEY}"

    payload = {
        "jsonrpc": "2.0",
        "method": method,
        "params": params,
        "id": request_id
    }

    req = urllib.request.Request(
        SERVER_URL,
        data=json.dumps(payload).encode("utf-8"),
        headers=headers,
        method="POST"
    )

    with urllib.request.urlopen(req, timeout=30) as resp:
        if resp.status == 200:
            return json.loads(resp.read().decode("utf-8"))
        raise Exception(f"MCP Server HTTP status code: {resp.status}")


# --- MCP Tool Definitions for Ollama ---

def search_regulations(query: str, jurisdiction: str = None) -> str:
    """
    Search AI regulations across jurisdictions by keyword, status, or jurisdiction.
    Args:
        query: Search term (e.g., 'artificial intelligence')
        jurisdiction: State or country filter (e.g., 'California')
    """
    args = {"query": query}
    if jurisdiction:
        args["jurisdiction"] = jurisdiction

    response = call_mcp_server("tools/call", {"name": "search_regulations", "arguments": args}, request_id=2)
    content_list = response.get("result", {}).get("content", [])
    if content_list and content_list[0].get("type") == "text":
        return content_list[0].get("text")
    return json.dumps(response)


def search(query: str) -> str:
    """
    Search everything on regulations.ai — laws, policies, enforcement actions, litigation, research, and news.
    Args:
        query: Search term
    """
    response = call_mcp_server("tools/call", {"name": "search", "arguments": {"query": query}}, request_id=3)
    content_list = response.get("result", {}).get("content", [])
    if content_list and content_list[0].get("type") == "text":
        return content_list[0].get("text")
    return json.dumps(response)


def recent_changes() -> str:
    """What has moved recently in AI regulation: newly added records, status changes, and milestones."""
    response = call_mcp_server("tools/call", {"name": "recent_changes", "arguments": {}}, request_id=4)
    content_list = response.get("result", {}).get("content", [])
    if content_list and content_list[0].get("type") == "text":
        return content_list[0].get("text")
    return json.dumps(response)


def list_jurisdictions() -> str:
    """List every jurisdiction covered, with how many regulations each has."""
    response = call_mcp_server("tools/call", {"name": "list_jurisdictions", "arguments": {}}, request_id=5)
    content_list = response.get("result", {}).get("content", [])
    if content_list and content_list[0].get("type") == "text":
        return content_list[0].get("text")
    return json.dumps(response)


def run_legal_chat_suite():
    # 1. Initialize MCP Session
    print("🔌 Initializing connection to regulations.ai MCP server...")
    try:
        call_mcp_server("initialize", {
            "protocolVersion": "2025-06-18",
            "capabilities": {},
            "clientInfo": {"name": "Legal-Chat-Agent", "version": "1.0.0"}
        }, request_id=1)
        print("   MCP handshake successful.\n")
    except Exception as e:
        print(f"   MCP Initialization failed: {e}")
        return

    available_tools = {
        "search_regulations": search_regulations,
        "search": search,
        "recent_changes": recent_changes,
        "list_jurisdictions": list_jurisdictions
    }

    # 2. Iterate through test questions
    for idx, prompt in enumerate(TEST_QUESTIONS, start=1):
        print("=" * 80)
        print(f" TEST CASE {idx}: \"{prompt}\"")
        print("=" * 80)

        messages = [{"role": "user", "content": prompt}]

        # Ask Ollama with tool bindings
        try:
            response = ollama.chat(
                model=OLLAMA_MODEL,
                messages=messages,
                tools=[search_regulations, search, recent_changes, list_jurisdictions]
            )
        except Exception as e:
            print(f"Ollama error: {e}")
            continue

        # Handle tool calls if requested by the model
        if response.message.tool_calls:
            messages.append(response.message)

            for tool_call in response.message.tool_calls:
                func_name = tool_call.function.name
                func_args = tool_call.function.arguments

                print(f"   🤖 Ollama invoked tool: `{func_name}` with args {json.dumps(func_args)}")

                if func_name in available_tools:
                    tool_output = available_tools[func_name](**func_args)
                    print(f"   Retrieved live data from MCP server.")

                    messages.append({
                        "role": "tool",
                        "tool_name": func_name,
                        "content": tool_output
                    })

            # Get final synthesized response from Ollama
            final_response = ollama.chat(
                model=OLLAMA_MODEL,
                messages=messages
            )
            print("\n📝 **AI Analysis Response:**")
            print(final_response.message.content)
        else:
            print("\n📝 **Direct AI Response (No tools used):**")
            print(response.message.content)
        
        print("\n")


if __name__ == "__main__":
    run_legal_chat_suite()
```
