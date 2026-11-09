<img src="images/reg_ai.jpg" width=1000 height=250>

*In-progress*

# Regulation.ai Overview

*[Connect your AI assistant to AI regulation data](https://regulations.ai/mcp)* and use the MCP server that gives live access to AI laws around the world.

## recent_changes

What has moved recently. A general model cannot answer this — the corpus is re-scanned weekly.

Example 1: "What are the recent changes in AI regulations?"

```
🤖 Ollama invoked tool: `recent_changes` with args {}
   Retrieved live data from MCP server.
```

November 7, 2026:

1. **New York FAIR News Act**: Adopted in 2026, this law addresses transparency when generative AI creates news media content.
2. **Política Nacional de Inteligencia Artificial (National Policy on Artificial Intelligence)**: Updated in 2026, this policy in Chile focuses on governance oversight, risk management, and accountability documentation.
3. **Singapore Legal Sector GenAI Guide**: Adopted in 2026, this guide provides guidelines for using generative AI in the legal sector, emphasizing professional ethics, confidentiality, and transparency.
4. **Circular Externa 002 de 2024 (Colombia AI Personal Data Rules)**: In force since 2024, this circular outlines guidelines for the processing of personal data in AI systems.
5. **CCPA Updates, Cybersecurity Audits, Risk Assessments, Automated Decisionmaking Technology (ADMT), and Insurance Regulations (California)**: Adopted in 2026, this regulation updates CCPA rules, requires risk assessments and annual cybersecurity audits, and establishes ADMT access and opt-out rights.

## search_regulations

Filter AI laws by jurisdiction, status or instrument type.

```
$ python3 get_valid_ai_reg.py 
Initializing connection to regulations.ai MCP server...
    MCP handshake successful.

[DEBUG] {
  "total": 1,
  "returned": 1,
  "results": [
    {
      "id": "RAI-US-CA-AB19790-2026",
      "url": "https://regulations.ai/regulations/RAI-US-CA-AB19790-2026",
      "title": "California AB 1979 — Health Care Services: Artificial Intelligence",
      "titleSimplified": "California Health Care AI Law",
      "titleEnglish": "California AB 1979 — Health Care Services: Artificial Intelligence",
      "jurisdiction": "California, United States",
      "country": "United States",
      "stateRegion": "California",
      "status": "Awaiting Entry",
      "type": "Act",
      "topics": [
        "governance_oversight",
        "transparency_disclosure",
        "fundamental_rights"
      ],
      "lastUpdated": "2026-10-09T09:22:47.205Z",
      "officialSources": [
        "https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260AB1979",
        "https://www.gov.ca.gov/2026/09/30/californias-nation-leading-ai-framework-just-got-stronger-governor-newsom-signs-more-first-in-the-nation-worker-protections-and-more/"
      ],
      "contentChangedAt": "2026-10-09T09:11:07.255Z",
      "snippet": "California AB 1979 adds AI-specific limits for health care settings and expands CMIA privacy protections to certain health care chatbots. It preserves licensed professional judgment in clinical care, restricts AI from performing licensed clinical functions, and brings covered chatbot businesses under provider-like…",
      "fullAnalysisAt": "https://regulations.ai/regulations/RAI-US-CA-AB19790-2026"
    }
  ],
  "note": "Free tier: facts and a snippet. The full analysis, sources and timeline are on the page — open the url and cite it."
}
```

```
Validating...
[JURISDICTION] California, United States

[DEBUG]
AB-1979 Health care services: artificial intelligence.
California AB 1979 — Health Care Services: Artificial Intelligence


                               ╭──────────────────────────────────────────────────────────────────────────────╮                                
                               │                                                                              │                                
                               │                                                                              │                                
                               │                         ▄▀▀ ▄▀█ █▀▀ ▀█▀ █▀▄▀█ █▀▀ █▀█                        │                                
                               │                         █▀  █▀█ ▄▄█  █  █ ▀ █ █▄▄ █▀▀                        │                                
                               │                                                                              │                                
                               │                                                                              │                                
                               │                                                                              │                                
                               │                                FastMCP 4.1.6                                 │                                
                               │                            https://gofastmcp.com                             │                                
                               │                                                                              │                                
                               │                 🖥  Server:      Job Processing Server, 4.1.6                 │                                
                               │                 🚀 Deploy free: https://horizon.prefect.io                   │                                
                               │                                                                              │                                
                               ╰──────────────────────────────────────────────────────────────────────────────╯                                


[11/08/26 17:14:30] INFO     Starting MCP server 'Job Processing Server' with transport 'stdio'                                transport.py:241
-> Running keyword search...
[TITLE] California AB 1979 — Health Care Services: Artificial Intelligence
```

```
Last Updated
2026-10-09T09:22:47.205Z

Analysis
https://regulations.ai/regulations/RAI-US-CA-AB19790-2026

Official sources:
https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260AB1979
https://www.gov.ca.gov/2026/09/30/californias-nation-leading-ai-framework-just-got-stronger-governor-newsom-signs-more-first-in-the-nation-worker-protections-and-more/
```


```
[11/08/26 17:14:31] INFO     Starting MCP server 'Job Processing Server' with transport 'stdio'                                transport.py:241
[SUMMARY] {
  "keyRequirements": [
    {
      "key": "Healthcare Professionals",
      "value": [
        "A licensed health care professional must retain the ability to exercise independent professional judgment in their care of a patient whenever that care is informed by the output of a clinical decision support system."
      ]
    },
    {
      "key": "AI Deployment",
      "value": [
        "A health facility, clinic, physician’s office, or office of a group practice cannot use or deploy a tool, system, or device that includes artificial intelligence to independently perform any clinical function that is required by law to be performed by a person with a professional license."
      ]
    },
    {
      "key": "Disclaimers and Instructions",
      "value": [
        "Health facilities, clinics, physician’s offices, and group practices must ensure that written or verbal patient communications include a disclaimer indicating that the communication was generated by generative artificial intelligence and clear instructions for contacting a human health care provider."
      ]
    },
    {
      "key": "Licensing and Enforcement",
      "value": [
        "Violations by physicians are subject to the jurisdiction of the Medical Board of California or the Osteopathic Medical Board of California, and the appropriate professional licensing board may pursue an injunction or restraining order to enforce these provisions."
      ]
    }
  ]
}
```
