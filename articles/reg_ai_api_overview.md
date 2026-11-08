<img src="images/reg_ai.jpg" width=1000 height=250>

# How can I quickly find AI regulations?

*[Connect your AI assistant to AI regulation data](https://regulations.ai/mcp)* and use the free MCP server that gives live access to AI laws around the world.  Here's an example of output from the Python script `ai_regulations_chat.py` that invokes the Ollama model `llama3.2:latest` to answer a series of questions designed to try out key features of the API.


## TEST CASE 1: "What are the AI laws in California?"

```API 
🤖 Ollama invoked tool: `search_regulations` with args {"jurisdiction": "California", "query": "AI laws"}
   Retrieved live data from MCP server.
```

The AI laws in California include:

1. Health care professions: deceptive terms or letters: artificial intelligence. (AB 489, enacted as Chapter 615 of the Statutes of 2025)
2. [California Executive Order N-9-26 — Independent Oversight of Frontier AI](https://www.gov.ca.gov/wp-content/uploads/2026/09/FINAL-N-9-26-AI-EO-9.18.26-SIGNED.pdf)
3. California SB 243 - Companion Chatbot Disclosure Requirements (enacted as Chapter 677 of the Statutes of 2025)

**Validation** AI responded with California Assembly Bill AB 489, California Senate Bill SB 243, and Executive Order N-9-26 issued by the California governor.  Search [Legiscan](https://legiscan.com/gaits/search?sort=desc&order=Status&state=CA&keyword=artificial%20intelligence) for current legislation.

## TEST CASE 2

Whether communicating with AI or a Human, you must ask clear, concise questions.  In the first run, the question was vague.

### Example 1:  "What has moved recently in AI regulation according to recent changes?"

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

**Validaton:**  "What has moved recently" is vague and the actions reported range from 2023 t0 2026.

1.  As of November 7, 2026, there is no dedicated [national legislative act governing AI in Luxembourg](https://cms.law/en/int/expert-guides/ai-regulation-scanner/luxembourg). However, Luxembourg is directly subject to the Regulation (EU) 2024/1689 – Artificial Intelligence Act (“EU AI Act”), which establishes harmonised rules for AI across all EU member states. The Act introduces a risk-based approach, banning certain harmful AI practices, and imposes strict obligations on high-risk and general-purpose AI systems.  Bill of law 8476 was submitted to the Parliament on 23 December 2024 and supplements the EU AI Act with the necessary national provisions for Luxembourg.  It is still under discussion.
2. Kazakhstan introduced [new fines and sanctions for AI-related offenses](https://en.orda.kz/kazakhstan-introduces-fines-for-misuse-of-artificial-intelligence-9324/) in November 2025.
3. [Artificial intelligence: stop to ChatGPT by the Italian SA Personal data is collected unlawfully, no age verification system is in place for children](https://www.garanteprivacy.it/web/guest/home/docweb/-/docweb-display/docweb/9870847#english) was enacted in March 2023.
4. [UK Workplace AI and Workers' Rights Bill](https://bills.parliament.uk/bills/3464#timeline) stalled in 2023.
5. [National supervision of EU Artificial Intelligence Act to begin – laws on powers of authorities to take effect at start of the year](https://valtioneuvosto.fi/en/-/1410877/national-supervision-of-eu-artificial-intelligence-act-to-begin-laws-on-powers-of-authorities-to-take-effect-at-start-of-the-year) entered into force in January 2026.


### Example 2:  "What are the recent changes in AI regulations?"

```
   🤖 Ollama invoked tool: `recent_changes` with args {}
    Retrieved live data from MCP server.
```

Based on the provided information, the recent changes in AI regulations can be summarized as follows:

1. **New York FAIR News Act**: Adopted in 2026, this law addresses transparency when generative AI creates news media content.
2. **Política Nacional de Inteligencia Artificial (National Policy on Artificial Intelligence)**: Updated in 2026, this policy in Chile focuses on governance oversight, risk management, and accountability documentation.
3. **Singapore Legal Sector GenAI Guide**: Adopted in 2026, this guide provides guidelines for using generative AI in the legal sector, emphasizing professional ethics, confidentiality, and transparency.
4. **Circular Externa 002 de 2024 (Colombia AI Personal Data Rules)**: In force since 2024, this circular outlines guidelines for the processing of personal data in AI systems.
5. **CCPA Updates, Cybersecurity Audits, Risk Assessments, Automated Decision-making Technology (ADMT), and Insurance Regulations (California)**: Adopted in 2026, this regulation updates CCPA rules, requires risk assessments and annual cybersecurity audits, and establishes ADMT access and opt-out rights.


## TEST CASE 3 

When using limited resources, keep the question simple.  In the first run, the question had two parts, search for enforcement actions and find litigation related to AI.

### Example 1: "Search for enforcement actions or litigation related to artificial intelligence."

```
🤖 Ollama invoked tool: `search` with args {"query": "enforcement actions or litigation artificial intelligence"}
   Retrieved live data from MCP server.
```      

Here are some enforcement actions and litigation related to artificial intelligence:

1. [Louisiana AI Medical Transcription Disclosure (Regulation ID: RAI-US-LA-HB47500-2026)](https://www.legis.la.gov/legis/ViewDocument.aspx?d=1445230).  A healthcare professional must obtain consent from a patient to use certain software.
2. AI, Governance and Ethics: Global Perspectives. (Research Paper)
3. A robust governance for the AI act: AI office, AI Board, scientific panel, and national authorities (Research Paper)
4. Assessing European Union Member States' Implementation of the Artificial Intelligence Act (Research Paper)
5. Towards the effective extraterritorial enforcement of the AI Act (Research Paper)
6. Artificial intelligence in governance: recent trends, risks, challenges, innovative frameworks and future directions (Research Paper)
7. Artificial intelligence policy worldwide: a comparative analysis (Research Paper)
8. Agencia de Acceso a la Informacion Publica (AAIP) v Public and private entities using AI (Enforcement Action).  Found the [Guia de la AAIP para user La Inteligencia artificial de mantra responsable](https://www.argentina.gob.ar/noticias/guia-de-la-aaip-para-usar-la-inteligencia-artificial-de-manera-responsable). 
9. [Berlin Commissioner for Data Protection (BlnBDI) v Hangzhou DeepSeek Artificial Intelligence Co., Ltd.](https://www.datenschutz-berlin.de/fileadmin/user_upload/pdf/pressemitteilungen/2025/20250627-BlnBDI-Press-Release_DeepSeek.pdf) (Enforcement Action)

These sources provide information on various aspects of artificial intelligence, including governance, ethics, implementation, and enforcement. They also highlight the importance of regulating AI to ensure its safe and responsible use.

**Validation:**  The response is very broad covering enforcement actions as well as research papers.

### Example 2: "What are the top enforcement actions related to artificial intelligence?"

```
   🤖 Ollama invoked tool: `search` with args {"query": "artificial intelligence enforcement actions"}
      Retrieved live data from MCP server.
```

The top enforcement actions related to artificial intelligence (AI) can be summarized as follows:

1. United States - Maine - AI Transparency Act (2025): This act aims to increase transparency and accountability in AI decision-making processes.
2. Virginia AI Chatbot Minor Protection Act (2026): This act aims to protect minors from harm caused by AI-powered chatbots.
3. Argentina - AI Innovation Committee (16/2024): This committee aims to promote the development and use of AI in Argentina.
4. Argentina - AI Transparency and Data Protection (161/2023): This law aims to ensure the transparency and protection of personal data in AI-powered systems.
5. Australia - Queensland - AI Governance Policy (2024): This policy aims to establish a framework for the governance of AI in Queensland, Australia.
6. Bulgaria - AI Coordinated Plan (2021): This plan aims to promote the development and use of AI in Bulgaria.
7. Brazil - National AI Strategy (Portaria MCTI No. 4.617): This strategy aims to promote the development and use of AI in Brazil.
8. Chile - Consumer Protection in AI (Resolución Exenta N°33/2022): This resolution aims to protect consumers from harm caused by AI-powered systems.
9. Colombia - National AI Policy (CONPES 4144): This policy aims to promote the development and use of AI in Colombia.
10. Germany AI Act Implementation Law: This law aims to implement the AI Act in Germany and ensure its effective enforcement.


## TEST CASE 4: 

The first request had two parts, list the available tools and list the jurisdictions covered in regulations.ai.

### "List the available tools and jurisdictions covered in regulations.ai."

```
🤖 Ollama invoked tool: `search` with args {"query": "available tools and jurisdictions covered"}
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

### "List the jurisdictions covered in regulations.ai"





