
<img src="images/valid_prompt.jpg" width=1000 height=250>

# Part 2:  Validating AI Prompt Responses

In Part 1, the small Ollama models struggled with ambiguity, hallucinations, and failure to complete tasks before timing out.  While humans can easily read and compare text, AI is better at math.  By converting text into lists of numbers called "embeddings", AI can perform more computations with fewer timeouts and compute more accurate inferences.  

### What are Vector Embeddings?

**Embeddings** are lists of floating-point numbers that represent unstructured data like text, images, audio, video, or code.  Models translate this unstructured data into this mathematical format so that items with similar meanings are placed close to each other.  For example, the embedding for the word *"kitten"* will be mathematically closer to *"puppy"* than to *"skyscraper."*  This allows computers to better understand the context of the data so it can calculate the semantic similarity of two words, for example, *kitten* and *puppy* both commonly refer to *pets* while *skyscraper* is a building.  

Vector embeddings can be stored in a vector database.  [LanceDB](https://www.lancedb.com/) is an open-source vector database designed for lightening fast similarity searches.  LanceDB stores embeddings in folders on the filesystem.  This makes it possible to use LanceDB for small projects, as well as scaling up to billions of vector embeddings on low-cost object storage like Amazon S3.

## Example:  Matching Skills to Job Requirements

Gemini wrote the following script to load the LanceDB database.  First, it ingests resume data into a LanceDB database.  Then, it opens the full resume and reads the Professional Experience section.  Next, it computes embeddings and stores them in a LanceDB database.  Run this script once to store embeddings for future queries. 

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

In order to match skills in the embedded resume, the job requirements must also be embedded.  Import essential libraries and modules for building an AI-powered data processing and retrieval pipeline, commonly referred to as [RAG (Retrieval-Augmented Generation)](https://www.ibm.com/think/topics/retrieval-augmented-generation).  According to IBM, the most common approach to RAG is to create dense vector representations of a knowledge base, in this case the full resume.  Then, query the database calculating the semantic similarity of each job requirement.  


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

Initialize the core components needed for the pipeline.  The `run_pipeline` function expects four parameters:
- `raw_jd_text`: The raw text of the job description.
- `distance`: A distance threshold value used to filter out irrelevant search results.  When using `cosine`, the distance of the most accurate responses is generally between 0.35 an 0.45.  When using `L2`, it ranges from 0.8 to 1.1.
- `limit`: The maximum number of search results to fetch.
- `distance_calc`: The metric used for distance calculation.  The default is `cosine`, but `L2` can also be chosen.

Double check run parameters by printing a status message displaying the chosen limit, distance calculation method, and threshold.  Connect to the instance of **Ollama** running locally.  Use the `llama3.2` model with a `temperature=0.0`.  This temperature setting tells the model to report deterministic and factual results. Setup Ollama's `nomic-embed-text` model to convert job description text into numerical vectors for comparison with resume embeddings already stored in the database in a folder named `./lancedb_data`.  Open the table called `resume_chunks`.  This table is located inside the database and contains the pre-chunked and vectorized data from the resume.

```
def run_pipeline(raw_jd_text: str, distance: float, limit: int, distance_calc: str):
    print(f"\nInitializing Ollama models and LanceDB limited to {limit} search results using {distance_calc} distance threshold of {distance}.")
    llm = ChatOllama(model="llama3.2", temperature=0.0)
    embeddings = OllamaEmbeddings(model="nomic-embed-text")
    db = lancedb.connect("./lancedb_data")
    table = db.open_table("resume_chunks")
```

## Executing the LLM-powered Prompt Chain

Set up and execute an LLM-powered prompt chain to ingest job description text and convert it to JSON format.  `ChatPromptTemplate.from_messages` creates a prompt template with `System Message` and `Human Message`.  The `System Message` named "system" gives the LLM a persona of "technical requirement parser".  It provides strict instructions on what to extract from the text and dictates the specific JSON schema for output:
* `raw_phrase`: Original text from the job description.
* `canonical_skill`: A standardized version of a technical skill.
* `execution_tier`: Categorized domains, *Software Validation*, *Training*, *Technical Writing*, or *Regulatory Compliance*.
* `search_queries`: 2–3 semantic phrases designed for vector database searches.

The `Human Message` named "human" passes `{raw_jd}` into the prompt with the actual raw text of the job description.  This separation of duties and structured format helps AI avoid getting confused and hallucinating a match from two similar requirements rather than querying skills in the resume. 

`normalizer_chain = normalizer_prompt | llm | JsonOutputParser()` uses LangChain's pipe operator (`|`) to link three components together into a single workflow:
1. **`normalizer_prompt`**: Merges input variables into the prompt, for example replacing {raw_jd} with job description text.
2. **`llm`**: Sends the formatted prompt to the local language model `llama3.2`.
3. **`JsonOutputParser()`**: Forces the LLM's text output into a valid JSON object.

`normalized_data = normalizer_chain.invoke(...)` runs the pipeline and stores the result in `normalized_data`.

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

Loop through the requirements stored in normalized_data.  For each requirement, extract the skill name and execution tier.

```
    print("Querying LanceDB using normalized search queries with distance filtering...")
    DISTANCE_THRESHOLD = distance
    retrieved_results = []
    for req in normalized_data.get("requirements", []):
        skill_name = req["canonical_skill"]
        execution_tier = req["execution_tier"]
```
For every search query associated with a requirement, convert the text string to a `query_vector`.  Use the distance calculation and distance threshold to find the closest matching vectors in the LanceDB.  Limit the number of responses to the input limit.

```
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
```
Multiple queries may return overlapping text chunks.  Use set() to remove duplicates.  Append a structured dictionary containing the skill name, execution tier, and the formatted context string to the `retrieved_results` list.
```
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
Setup argparse to gather the input parameters including the file path of the job description, the distance threshold, limit for the number of responses, and the distance calculation.

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

```
Read the job description and run the pipeline.

```
    with open(args["job_path"], "r") as f:
        job_text = f.read()
    
    results = run_pipeline(job_text, args["distance"], args["limit"], args["distance_calc"])
```

Print results in a format that is easy for humans to read.

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

Part 1 identified two problems, timeouts and hallucinations.  In Part 1, the script ran quickly and did not time out.  It also more accurately matched experience to job requirements.

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
