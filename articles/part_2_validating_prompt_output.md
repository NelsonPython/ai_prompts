
<img src="images/valid_prompt.jpg" width=1000 height=250>

# Part 2:  Validating AI Prompt Responses

Running an AI Prompt seems easy for a human, just type instructions and wait for a response, then chat until you get an answer that you can fact check.  Programming an AI agent to perform a task autonomously, requires AI to work hard behind the scenes trying to understand instructions and validate responses.  Vector embeddings can help AI speed up performance and improve accuracy.  

## What are Vector Embeddings?

**Embeddings** are lists of floating-point numbers that represent unstructured data like text, images, audio, video, or code.  Models translate the unstructured data into this mathematical format so that items with similar meanings (features) are placed close to each other.  For example, the embedding for the word *"kitten"* will be mathematically closer to *"puppy"* than to *"skyscraper."*  This allows computers to better understand the context of data so it can respond more accurately.  

Vector embeddings can be stored in a vector database.  [LanceDB](https://www.lancedb.com/) is an open-source vector database designed for AI applications.  Embeddings are stored in folders so running a server is not necessary.  While LanceDB can scale to handle billions of vector embeddings on low-cost object storage like Amazon S3, it can also be used for small projects.

## Why Use the LanceDB Vector Database?

- Lightening fast similarity searches
- Low cost storage
- Hybrid searches and filtering

## Example - Matching Skills to Job Requirements

First, the full resume was ingested into a LanceDB database.  Then, the prompt was revised to use embeddings.

### Ingesting Data

Gemini wrote this Python script to read the Professional Experience section of the `full_resume.json`, then compute and save embeddings in a LanceDB database.

```
import json
import lancedb
from langchain_ollama import OllamaEmbeddings

def ingest_resume_to_lancedb(json_path: str):
    print("Initializing Ollama embeddings and LanceDB...")
    embeddings = OllamaEmbeddings(model="nomic-embed-text")
    db = lancedb.connect("./lancedb_data")

    # Load resume JSON
    with open(json_path, "r", encoding="utf-8") as f:
        resume = json.load(f)

    chunk_records = []
    idx = 0

    # Chunk Professional Experience (Title, Company, and Bullets)
    for exp in resume.get("professional_experience", []):
        title = exp.get("title", "Role")
        company = exp.get("company", "Company")
        dates = exp.get("dates", "")
        tags = ", ".join(exp.get("domain_tags", []))
        bullets = " ".join(exp.get("bullets", []))
        
        text = f"Role: {title} at {company} ({dates}). Domains: {tags}. Experience: {bullets}"
        
        chunk_records.append({
            "id": idx,
            "vector": embeddings.embed_query(text),
            "text": text,
            "source": "professional_experience"
        })
        idx += 1

    # Create or overwrite LanceDB table
    table = db.create_table("resume_chunks", data=chunk_records, mode="overwrite")
    print(f"Ingested {len(chunk_records)} structured resume chunks into LanceDB")

if __name__ == "__main__":
    ingest_resume_to_lancedb("full_resume.json")
```


### Searching


```
{
    "professional_experience": [
        {
            "title": "Technical Writer",
            "company": "Crane Aerospace",
            "dates": "Feb 2022 \u2013 Jun 2022",
            "domain_tags": [
                "Aerospace, CMMC 2.0, Regulatory Compliance, Python Automation. "
            ],
            "bullets": [
                "Partnered with IT management to formulate exhaustive corporate compliance documentation for cybersecurity readiness. Engineered custom Python scripts to automate compliance documentation templates directly from government guidelines. Improved accuracy, completeness, and on-time documentation delivery."
            ]
        },
        {
            "title": "Technical Writer",
            "company": "TXOne Networks",
            "dates": "Jan 2022 \u2013 Nov 2022",
            "domain_tags": [
                "OT/ICS, Cyber Threat Intelligence, Zero Trust, Sales Support. "
            ],
            "bullets": [
                "Published authoritative hardening recommendations for portable security devices and industrial firewalls. Authored blog posts and white papers published on TXOne Networks website. Developed compliance crosswalks for NERC CIP, NIST, NIS 2, and NHS DSPT."
            ]
        },
        {
            "title": "Technical Writer",
            "company": "IOTA",
            "dates": "Feb 2018 \u2013 Apr 2020",
            "domain_tags": [
                "API Documentation, Blockchain, IoT, Developer Education. "
            ],
            "bullets": [
                "Developed comprehensive REST API user guides. Wrote training guides explaining cross-brand IoT device communication via blockchain. Developed trade show demos Wrote curriculum and taught training seminars"
            ]
        }
    ]
}
```
