# The Power of Preprocessing

Data engineering is the invisible architecture that transforms raw, chaotic data into clean, accessible fuel for AI.  Preprocessing is the unglamorous analysis of input data so that code can comprehend it.  

In theory, a job description and a resume should include a standard set of keywords that identify the skills needed for a particular job.  In practice, job descriptions vary from formal, official verbiage to rock star slang.  

When I first tried using AI to distill my sprawling work history into a sharp, tailored resume, I took the brute-force approach. I dumped my entire career history and a target job description straight into Gemini and told it to work its magic.  Instead of a resume, it wrote science fiction.

I revised the prompt - same result.  I asked Gemini to revise the prompt - same result.  I asked other AI to revise the prompt - same result.  I stopped revising the prompt and started preprocessing the data.

## Preprocessing Data

<img src="images/json.jpeg" width=1000 height=250>

## JSON

In 2001, JSON (JavaScript Object Notation) was introduced as a human and machine readable format.  It became the universal standard for sending data over the internet.  Today, AI can use JSON to organize its unpredictable responses. 

I encoded my entire resume into JSON format with separate sections for Core Competencies, Professional Experience, Education, Invited Speaker, Honors and Awards, Publications, and Avocation.  Here's a portion of my Professional Experience.

```
 {
 "professional_experience": [
    {
      "job_no": 17,
      "title": "Technical Editor – AI Prompts",
      "company": "PromptMelodic",
      "dates": "Jan 2026 – Nov 2026",
      "skills": [
        "ai",
        "ai prompt",
        "agentic",
        "code",
        "docs",
        "embeddings",
        "rag",
        "vector",
        "vector database",
        "mcp"
        ],
      "bullets": [
        "Evaluate Agentic AI documentation pipelines to ensure accuracy and completeness.",
        "Edit complex technical content produced by generative AI."
      ]
    },
    {
      "job_no": 16,
      "title": "AI Subject Matter Expert",
      "company": "FBI InfraGard",
      "dates": "Oct 2024 – Dec 2025",
      "skills": [
        "ai",
        "critical infrastructure",
        "cyber",
        "cybersecurity",
        "intelligence",
        "public safety",
        "threat"
      ],
      "bullets": [
        "Appointed leader: Artificial Intelligence Cross Sector Council (AI-CSC) Research Initiative.",
        "Compiled a master repository of AI vulnerabilities impacting critical infrastructure and public safety."
      ]
    }
}

```
<img src="images/count_vectorizer.jpeg" width=1000 height=250>

## [CountVectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html)

Job descriptions are keyword-heavy documents listing skills, tools, and methodologies.  This function extracts words along with counts.  If you change `ngram_range=(1,2)` it will extract short phrases such as "machine learning".  ENGLISH_STOP_WORDS contains grammar words such as "the or a".  I added a custom list of terms, `custom_stopwords`, including "collaborate, desired, experience..."  I also overrode the `top_n=20` limit and chose the top 150 words.

```
from sklearn.feature_extraction.text import CountVectorizer, ENGLISH_STOP_WORDS

def extract_job_desc_keywords(text, custom_stopwords=None, top_n=20):
    stop_words = set(ENGLISH_STOP_WORDS)
    if custom_stopwords:
        stop_words.update(custom_stopwords)
    vectorizer = CountVectorizer(stop_words=list(stop_words), ngram_range=(1, 1), max_features=top_n)

    X = vectorizer.fit_transform([text])
    
    # Extract words/phrases along with counts
    word_counts = zip(vectorizer.get_feature_names_out(), X.toarray()[0])
    job_keyword_counts = sorted(word_counts, key=lambda x: x[1], reverse=True)
    job_keywords = [item[0] for item in job_keyword_counts]
    return job_keyword_counts, job_keywords
```
<img src="images/fuzzy_search.jpeg" width=1000 height=250>

## Fuzzy Search

Fuzzy searching looks for near matches and returns a percentage.  I used [RapidFuzz](https://pypi.org/project/RapidFuzz/) and selected a match criteria or score of 70%.

```
def fuzzy_search_rapidfuzz(target_phrase: str, text_lines: list[str], score_cutoff: int = 70):
    """
    Uses RapidFuzz token_set_ratio which handles typos, word order changes, 
    and matching short phrases within long lines.
    """
    # process.extract returns tuples of (matched_string, score, index)
    results = process.extract(
        target_phrase, 
        text_lines, 
        scorer=fuzz.token_set_ratio, 
        score_cutoff=score_cutoff
    )

    matches = []
    for line, score, idx in results:
        matches.append({
            "line_number": idx + 1,
            "score": round(score, 2),
            "line": line
        })
    
    return matches
```
<img src="images/semantic_search.jpeg" width=1000 height=250>


## Semantic Search

Having found 
