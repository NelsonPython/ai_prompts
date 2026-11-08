<img src="images/reg_ai.jpg" width=1000 height=250>

# How can I find AI regulations?

*[Connect your AI assistant to AI regulation data](https://regulations.ai/mcp)* and use the MCP server that gives live access to AI laws around the world.

## search

Search everything — laws, definitions, enforcement, research, news. Returns ids, titles and links.

## fetch

Retrieve one record by id: the key facts, a summary, and the page it came from.

## search_regulations

Filter AI laws by jurisdiction, status or instrument type.

## get_regulation

One instrument: jurisdiction, status, dates, official source.

## recent_changes

What has moved recently. A general model cannot answer this — the corpus is rescanned weekly.

Example 1: "What are the recent changes AI regulations?"

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


## get_glossary_term

A term of art, with how many separate laws define it and how they differ.

## list_jurisdictions

Every jurisdiction covered, with counts.

## compare_regulations

Two to five instruments side by side.

