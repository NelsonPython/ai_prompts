<img src="images/reg_ai.jpg" width=1000 height=250>

# Regulations.ai

*[Connect your AI assistant to AI regulation data](https://regulations.ai/mcp)* explains how to use the Regulations.ai MCP server to gain live access to AI laws around the world.

## search_regulations

Use `search_regulations("AB 1979", "California")` to find information about California AB 1979 — Health Care Services: Artificial Intelligence.  The results are in JSON format.

```
{
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

Validate results by checking against other reputable sources.  The ground_truth comes from [Bill Text: CA AB1979 | 2025-2026 | Regular Session | Chaptered](https://legiscan.com/CA/text/AB1979/id/3461144)

```
    ground_truth = {
        "jurisdiction": "California",
        "titleEnglish": (
            "AB-1979 Health care services: artificial intelligence."
        ),
        "snippet": ("This bill would require a health facility, clinic, physician’s office, or office of a group practice
to take reasonable steps to ensure that a licensed health care professional, acting within their scope of practice,
retains the ability to exercise independent professional judgment in their care of a patient whenever that care is
informed by the output of a clinical decision support system, as defined. The bill would prohibit a health facility,
clinic, physician’s office, or office of a group practice from using or deploying a tool, system, or device that
includes artificial intelligence to independently perform any clinical function that is required by law to be performed
by a person with a professional license.")
    }
```
Validate results against the ground truth.

```
Validating jurisdiction with a keyword search:
[JURISDICTION] California, United States

Validating title with a keyword search followed with a semantic search if no keywords are found.

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

[11/08/26 17:14:30] INFO Starting MCP server 'Job Processing Server' with transport 'stdio' transport.py:241

-> Running keyword search...
[TITLE] California AB 1979 — Health Care Services: Artificial Intelligence

-> Running semantic search...
True
The input text 'AB-1979 Health care services: artificial intelligence' is essentially the same as the official name 'California AB 1979 — Health Care Services: Artificial Intelligence'. The only difference is the abbreviation 'AB' at the beginning, which is a common practice in legislation numbering systems. The rest of the text is identical, including the name of the legislation and the description of the subject matter. Therefore, these two texts refer to the same legislation.
[TITLE] California AB 1979 — Health Care Services: Artificial Intelligence
```

**Results for Human review**

Last Updated
2026-10-09T09:22:47.205Z

Analysis
https://regulations.ai/regulations/RAI-US-CA-AB19790-2026

Official sources:
https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=202520260AB1979

https://www.gov.ca.gov/2026/09/30/californias-nation-leading-ai-framework-just-got-stronger-governor-newsom-signs-more-first-in-the-nation-worker-protections-and-more/

**Summary in JSON format**

AI summarizes AB 1979 into JSON format for easy ingestion into downstream systems.  

```
[SUMMARY] {
  "keyRequirements": [
    {
      "key": "Healthcare Professionals",
      "value": [
        "A licensed health care professional must retain the ability to exercise independent professional judgment
 in their care of a patient whenever that care is informed by the output of a clinical decision support system."
      ]
    },
    {
      "key": "AI Deployment",
      "value": [
        "A health facility, clinic, physician’s office, or office of a group practice cannot use or deploy a tool,
system, or device that includes artificial intelligence to independently perform any clinical function that is
required by law to be performed by a person with a professional license."
      ]
    },
    {
      "key": "Disclaimers and Instructions",
      "value": [
        "Health facilities, clinics, physician’s offices, and group practices must ensure that written or
verbal patient communications include a disclaimer indicating that the communication was generated by
generative artificial intelligence and clear instructions for contacting a human health care provider."
      ]
    },
    {
      "key": "Licensing and Enforcement",
      "value": [
        "Violations by physicians are subject to the jurisdiction of the Medical Board of California or
the Osteopathic Medical Board of California, and the appropriate professional licensing board may pursue
an injunction or restraining order to enforce these provisions."
      ]
    }
  ]
}
```
