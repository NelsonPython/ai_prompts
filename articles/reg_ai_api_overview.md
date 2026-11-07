<img src="images/reg_ai.jpg" width=1000 height=250>

# How can I quickly find AI laws and regulations?

[Connect your AI assistant to AI regulation data](https://regulations.ai/mcp) and use the free MCP server that gives live access to AI laws around the world.  Here's the first example of output from the Python script `ai_regulations_chat.py` that invokes the Ollama model `llama3.2:latest` to answer a series of questions designed to test the key features of the API.  *Results currently under review*

**Run ai_regulations_chat.py**
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

The AI laws in California include:

1. Health care professions: deceptive terms or letters: artificial intelligence. (AB 489, enacted as Chapter 615 of the Statutes of 2025)
2. [California Executive Order N-9-26 — Independent Oversight of Frontier AI](https://www.gov.ca.gov/wp-content/uploads/2026/09/FINAL-N-9-26-AI-EO-9.18.26-SIGNED.pdf)
3. California SB 243 - Companion Chatbot Disclosure Requirements (enacted as Chapter 677 of the Statutes of 2025)

**Validation** AI responded with an Assembly Bill, a Senate Bill, and an executive order issued by the California governor.  Search [Legiscan](https://legiscan.com/gaits/search?sort=desc&order=Status&state=CA&keyword=artificial%20intelligence) for current legislation.


### TEST CASE 2: "What has moved recently in AI regulation according to recent changes?"

```
🤖 Ollama invoked tool: `recent_changes` with args {}
      Retrieved live data from MCP server.
```

The AI regulation tracker shows changes in AI regulations worldwide. The recent changes include:

1. Luxembourg AI Act Implementation Bill: This bill aims to implement the [EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng) in Luxembourg and includes provisions on governance oversight, market surveillance, and enforcement penalties.
2. Kazakhstan AI Administrative Penalties Law: This law introduces new fines and sanctions for AI-related offenses, including disclosure failures and harmful failures to manage high-risk systems.
3. Italy ChatGPT Privacy Safeguards Order: This regulation requires companies to implement ChatGPT privacy safeguards and provides a framework for data protection and transparency.
4. UK Workplace AI and Workers' Rights Bill: This bill aims to regulate AI technologies in the workplace and provide workers' rights, but its status is stalled.
5. Finland AI Supervision Act: This act supplements the EU AI Act by allocating supervision, designating a central contact point, and creating an administrative sanctions board.

These changes demonstrate the growing importance of AI regulation worldwide, with countries implementing their own laws and regulations to address the risks and benefits of AI technologies.

**Validaton:**  The term "recent" is vague.  

1.  As of November 7, 2026, there is no dedicated national legislative act governing AI in Luxembourg. However, Luxembourg is directly subject to the Regulation (EU) 2024/1689 – Artificial Intelligence Act (“EU AI Act”), which establishes harmonised rules for AI across all EU member states. The Act introduces a risk-based approach, banning certain harmful AI practices, and imposes strict obligations on high-risk and general-purpose AI systems.  Bill of law 8476 was submitted to the Parliament on 23 December 2024 and supplements the EU AI Act with the necessary national provisions for Luxembourg.  It is still under discussion.
2. Kazakhstan introduced [new fines and sanctions for AI-related offenses](https://en.orda.kz/kazakhstan-introduces-fines-for-misuse-of-artificial-intelligence-9324/) in November 2025.
3. [Artificial intelligence: stop to ChatGPT by the Italian SA Personal data is collected unlawfully, no age verification system is in place for children](https://www.garanteprivacy.it/web/guest/home/docweb/-/docweb-display/docweb/9870847#english) was enacted in March 2023.
4. [UK Workplace AI and Workers' Rights Bill](https://bills.parliament.uk/bills/3464#timeline) stalled in 2023.
5. [National supervision of EU Artificial Intelligence Act to begin – laws on powers of authorities to take effect at start of the year](https://valtioneuvosto.fi/en/-/1410877/national-supervision-of-eu-artificial-intelligence-act-to-begin-laws-on-powers-of-authorities-to-take-effect-at-start-of-the-year) entered into force in January 2026.

### TEST CASE 3: "Search for enforcement actions or litigation related to artificial intelligence."
```
   🤖 Ollama invoked tool: `search` with args {"query": "enforcement actions or litigation artificial intelligence"}
      Retrieved live data from MCP server.
```

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
