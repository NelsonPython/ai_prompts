
<img src="images/valid_prompt.jpg" width=1000 height=250>

# Part 2:  Validating AI Prompt Responses

Running an AI Prompt seems easy for a human, just type instructions and wait for a response, then chat until you get an answer that you can fact check.  Programming an AI agent to perform a task autonomously, requires AI to work hard behind the scenes trying to understand instructions and validate responses.  Vector embeddings can help AI speed up performance and improve accuracy.  

### What are Vector Embeddings?

**Embeddings** are lists of floating-point numbers that represent unstructured data like text, images, audio, video, or code.  Models translate the unstructured data into this mathematical format so that items with similar meanings (features) are placed close to each other.  For example, the embedding for the word *"kitten"* will be mathematically closer to *"puppy"* than to *"skyscraper."*  This allows computers to better understand the context of data so it can respond more accurately.  

Vector embeddings can be stored in a vector database.  [LanceDB](https://www.lancedb.com/) is an open-source vector database designed for AI applications.  Embeddings are stored in folders so running a server is not necessary.  While LanceDB can scale to handle billions of vector embeddings on low-cost object storage like Amazon S3, it can also be used for small projects.

### Why Use the LanceDB Vector Database?

- Lightening fast similarity searches
- Low cost storage
- Hybrid searches and filtering

## Example:  Matching Skills to Job Requirements

First, ingest resume data into a LanceDB database by reading the Professional Experience section of the 'full_resume.json', then computing and storing embeddings in a LanceDB database.  Gemini wrote the following script.

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

### Using the Vector Database to Match Skills and Job Requirements

Import essential libraries and modules for building an AI-powered data processing and retrieval pipeline.

```
import argparse
import json
import lancedb
from langchain_ollama import ChatOllama, OllamaEmbeddings
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import JsonOutputParser
```

`argparse` - Python module for parsing command-line parameters that allows users to run the script with different parameters.

`json` - Python's built-in module for retrieving data formatted as JSON (JavaScript Object Notation), an industry standard for LLM responses.

`lancedb` - Python client library for **LanceDB**, an open-source vector database that allows the script to connect to a local or remote vector database, store, and efficiently query high-dimensional vector embeddings.

`ChatOllama` from `langchain_ollama`- LangChain's integration wrapper for chat models running locally via **Ollama** that enables the script to send structured prompts and receive responses from locally hosted Large Language Models, such as Llama 3.2.

`OllamaEmbeddings` from `langchain_ollama` - LangChain's wrapper for generating embeddings locally via **Ollama** that converts text in search queries or document chunks into numerical vector representations using models such as `nomic-embed-text`.

`ChatPromptTemplate` from `langchain_core.prompts` - A LangChain utility designed to format prompts for chat models by combining system messages, human messages, and placeholder variables.  Using this format makes it easier to dynamically build instructions for the LLM.

`JsonOutputParser` from `langchain_core.output_parsers` - LangChain parser that instructs the LLM to output valid JSON and parses that text response directly into a Python dictionary or list.  This ensures more reliable, structured data extraction from the LLM's text output so downstream code can safely process it.


### Initializing Core Components for RAG

Initialize the core components needed for this RAG (Retrieval-Augmented Generation) pipeline.  The `run_pipeline` function expects four parameters:
- `raw_jd_text`: The raw text of the job description.
- `distance`: The threshold value used to filter out irrelevant search results.
- `limit`: The maximum number of search results to fetch.
- `distance_calc`: The metric used for distance calculation, either `cosine` or `L2`.

Print a status message displaying the chosen limit, distance calculation method, and threshold.  Connect to an instance of **Ollama** running locally and using the `llama3.2` model with a `temperature=0.0`.  This temperature aims to report deterministic and factual results.  Setup Ollama's `nomic-embed-text` model to convert job description text into numerical vectors for comparison with resume embeddings stored in the resume database.  Connect to the resume database stored in a local folder named `./lancedb_data` and open a table called `"resume_chunks"`.  This table is located inside the database and contains the pre-chunked and vectorized data from the resume.

```
def run_pipeline(raw_jd_text: str, distance: float, limit: int, distance_calc: str):
    print(f"\nInitializing Ollama models and LanceDB limited to {limit} search results using {distance_calc} distance threshold of {distance}.")
    llm = ChatOllama(model="llama3.2", temperature=0.0)
    embeddings = OllamaEmbeddings(model="nomic-embed-text")
    db = lancedb.connect("./lancedb_data")
    table = db.open_table("resume_chunks")
```

## Executing the LLM-powered Prompt Chain

Set up and execute an LLM-powered prompt chain that takes an unstructured, messy job description and converts it into JSON format.  Create a prompt template, `ChatPromptTemplate.from_messages`).  The `System Message (`"system"`)` gives the LLM a persona of "technical requirement parser" as well as strict instructions on what to extract from the text. It dictates that the output must follow a specific JSON schema with four key fields:
* `raw_phrase`: The original text snippet from the job description.
* `canonical_skill`: A standardized version of the technical skill.
* `execution_tier`: The categorized domain of *Software Validation*, *Training*, *Technical Writing*, or *Regulatory Compliance*.
* `search_queries`: 2–3 semantic phrases designed for vector database searches.

The `Human Message (`"human"`)` passes the actual raw text of the job description `{raw_jd}` into the prompt.

`normalizer_chain = normalizer_prompt | llm | JsonOutputParser()` uses LangChain's pipe operator (`|`) to link three components together into a single workflow:
1. **`normalizer_prompt`**: Formats the input variables into the prompt.
2. **`llm`**: Sends the formatted prompt to the local language model `llama3.2`.
3. **`JsonOutputParser()`**: Forces the LLM's text output into a valid JSON object.

`normalized_data = normalizer_chain.invoke(...)` runs the pipeline by passing it the raw job description text and storing the result in a structured Python dictionary, `normalized_data`.

```
    print("Normalizing job description into structured criteria...")
    normalizer_prompt = ChatPromptTemplate.from_messages([
        ("system", 
         "You are a technical requirement parser. Take unstructured, noisy job descriptions and extract explicit technical requirements.\n\n"
         "For each requirement, output:\n"
         "1. 'raw_phrase': The exact or approximate text from the input.\n"
         "2. 'canonical_skill': Standardized technical term.\n"
         "3. 'execution_tier': Infer depth from context: 'Software Validation' | 'Training' | 'Technical Writing' | 'Regulatory Compliance'.\n"
         "4. 'search_queries': 2-3 specific semantic phrases to search in a vector database.\n\n"
         "Return ONLY a JSON object formatted as:\n"
         "{{\n"
         '  "requirements": [\n'
         "    {{\n"
         '      "raw_phrase": "String",\n'
         '      "canonical_skill": "String",\n'
         '      "execution_tier": "Software Validation" | "Training" | "Technical Writing" | "Regulatory Compliance",\n'
         '      "search_queries": ["String"]\n'
         "    }}\n"
         "  ],\n"
         '  "rationale": "String"\n'
         "}}"
        ),
        ("human", "Raw Job Description Text:\n{raw_jd}")
    ])

    normalizer_chain = normalizer_prompt | llm | JsonOutputParser()
    normalized_data = normalizer_chain.invoke({"raw_jd": raw_jd_text})
```

```
    print("Querying LanceDB using normalized search queries with distance filtering...")
    DISTANCE_THRESHOLD = distance
    retrieved_results = []
    for req in normalized_data.get("requirements", []):
        skill_name = req["canonical_skill"]
        execution_tier = req["execution_tier"]
        
        retrieved_chunks_for_skill = []
        
        for query_text in req["search_queries"]:
            query_vector = embeddings.embed_query(query_text)

            # Fetch top <limit> closest matching chunks from LanceDB
            if distance_calc =="L2":
                search_results = table.search(query_vector).limit(limit).to_list()
            elif distance_calc == "cosine":
                search_results = table.search(query_vector).metric("cosine").limit(limit).to_list()
            
            for result in search_results:
                distance = result.get("_distance", 0.0)
                if distance < DISTANCE_THRESHOLD:
                    retrieved_chunks_for_skill.append(result["text"])
                
        # Deduplicate and format unique chunks with ' | ' separator (or "None" if empty)
        unique_chunks = list(set(retrieved_chunks_for_skill))
        formatted_context = " | ".join(unique_chunks) if unique_chunks else "None"
        
        retrieved_results.append({
            "canonical_skill": skill_name,
            "target_execution_tier": execution_tier,
            "retrieved_resume_context": formatted_context
        })

    return retrieved_results
```

```
if __name__ == "__main__":
    ap = argparse.ArgumentParser(description="Get raw job descriptions from job_desc/filename.txt and output structured retrieval results")
    ap.add_argument(
        "-j", "--job_path",
        required=True,
        help="Select a job description, normally stored in job_desc/filename.txt"
    )
    ap.add_argument(
        "-d", "--distance",
        type=float,
        default=0.35,
        help="Recommended percent between 0.80 and 1.3 for L2 (Euclidean) absolute distance or 0.35 to 0.45 for cosine angle measurement."
    )
    ap.add_argument(
        "-c", "--distance_calc",
        type=str,
        default="cosine",
        help="Choose L2 (Euclidean) absolute distance or cosine angle measurement."
    )
    ap.add_argument(
        "-n", "--limit",
        type=int,
        default=2,
        help="Limit for selecting the top matches"
    )    
    args = vars(ap.parse_args())

    with open(args["job_path"], "r") as f:
        job_text = f.read()
    
    results = run_pipeline(job_text, args["distance"], args["limit"], args["distance_calc"])
```

Print results in a format easy for humans to read.

```
    print("\n--- Job Description Analysis ---")
    print(json.dumps(results, indent=2))

    unique_chunks = set()
    for item in results:
        ctx = item.get("retrieved_resume_context")
        if ctx and ctx != "None":
            for chunk in ctx.split(" | "):
                unique_chunks.add(chunk.strip())

    for index, chunk in enumerate(sorted(unique_chunks), 1):
        print(f"\n[{index}] {chunk}")
``` 

## Results

Part 1 identified two problems, timeouts and hallucinations.  This script ran quickly and did not time out.  It more accurately matched experience to job requirements.

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
