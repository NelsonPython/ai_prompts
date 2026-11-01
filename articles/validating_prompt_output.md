<img src="images/valid_prompt.jpg" width=1000 height=250>

# Part 1:  Validating Prompt Output

Validating AI prompt results includes assessing whether the inferences made are clear and consistent.  In this example, a job description was downloaded using the freehire.me API.  The original content was summarized by AI, then for this example, a human anonymized it by removing references to the hiring company.  Rather than tackle the entire resume, this prompt aims to match job requirements with one section, a complete list of core competencies.  Because the resume contains over 15 years of experience in different roles, all core competencies may not be applicable.  AI is tasked with reading the job description, evaluating the resume, and ranking matches as exact, partial, or no match. 

### AI Prompt

<pre>
You are an algorithm that matches Job Requirements and Resume.
1. Do not fabricate data.
2. Evaluate and rank evidence from the Resume and only record the actual requirement, the evidence, and your ranking.  Strictly put your output in this json schema:
{
  "job_requirements": [
    {
      "requirement": "String",
      "evidence": "String", 
      "ranking": "Exact Match | Partial Match | No Match",
    }
  ]
}

Requirements

Technical Writing
Instructional Design
Developer Education
Technical Curriculum Development
LLMs
Generative AI
Prompting
APIs
Vector Database Systems
Hands-on Technical Workshops
Developer Training Materials
Technical Documentation
Interactive Exercises
Code Walkthroughs
Lab Guides
Instructor Resources
API and SDK Documentation
Technical Accuracy
Accessibility
Real-World Developer Workflows
Python
Git/GitHub
Markdown
Version Control
Testing
Engineering Partners
Technical Validation
Troubleshooting
Developer Learning Experience
Agentic AI
Model Evaluations
LLM Testing
Responsible AI Development
Vector Databases
Retrieval-Augmented Generation (RAG)
Embeddings
Agenic AI Workflows
Documentation Platforms
Static Site Generators
Documentation-as-Code Workflows
3+ years of experience in technical writing, instructional design, developer education, technical curriculum development, or a related field
Demonstrated experience creating hands-on technical workshops, developer training materials, and comprehensive technical documentation
Strong understanding of LLMs, generative AI, prompting, APIs, and vector database systems
Experience developing technical content for software engineers, application developers, platform engineers, or similarly technical audiences
Exceptional technical writing and editing skills, with the ability to communicate complex concepts clearly without sacrificing technical accuracy
Ability to read, understand, and explain code examples in Python or similar programming languages
Familiarity with software development workflows, including Git/GitHub, Markdown, version control, and testing
Experience collaborating with engineers to validate technical documentation, troubleshoot exercises, and improve developer learning experiences
Strong organizational skills and the ability to independently manage multiple content deliverables in a fast-moving environment
Experience developing educational content or documentation for AI/ML platforms, developer tools, or emerging AI technologies
Familiarity with AI safety, model evaluations, LLM testing, or responsible AI development
Experience with vector databases, retrieval-Augmented Generation (RAG), embeddings, or agentic AI workflows
Experience with documentation platforms, static site generators, or documentation-as-Code workflows
Previous experience working with AI research teams, developer platforms, or early-stage technology companies

Resume
## CORE COMPETENCIES

### AI and Automation:
Agentic AI, AI prompt automation, Python, SQL

### Compliance frameworks:
CMMC 2.0, DO 178, FAA Part 107, FDA CFR Part 11, GAMP 5, GLP, HIPAA, ISO 27001, NERC CIP, NHS DSPT, NIS 2, NIST SP 800-207 RMF

### Industries:
Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical

### Regulatory compliance documentation:
International Regulatory Compliance Guides, Journal Articles, Regulatory Crosswalks, Risk Assessments, Software Installation Qualification, Software Operational Qualification, Software Performance Qualification, Software Validation Plans, Standard Operating Procedures (SOPs), White-papers

### Software documentation:
AI Prompt Engineering, API Reference Guides, API User Guides, Cybersecurity Guidance, FAQs, Knowledge Articles, Quick-start Guides, Release notes, Software Training Curriculum, Tuning Guides, User Guides

### Tools:
Agile, Confluence, Git, Github, Google Docs, HTML, Jira, LibreOffice, Markdown, MS Office, PDF, SharePoint, Word
</pre>

# Ollama Responses

The script was run three times.  First, the keywords were included.  Second, a model optimized for coding was used.  Third, a model optimized for chatting was used.

### 1. Timeout
The prompt with keywords consistently timed out.

### 2.  Hallucinations from qwen2.5-coder:1.5b
Removing keywords from the Prompt allows the prompt to run, but the `qwen2.5-coder:1.5b` model hallucinated as shown in the annotated sample output below.

<pre>
  [RAW CONTENT] {
  "job_requirements": [
    {
      "requirement": "3+ years of experience in technical writing, instructional design, developer education, technical curriculum development, or a related field",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"    <- Hallucination.  Evidence says nothing about 3+ years of experience...
    },
    {
      "requirement": "Demonstrated experience creating hands-on technical workshops, developer training materials, and comprehensive technical documentation",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination.  Evidence says nothing about demonstrated experience...
    },
    {
      "requirement": "Strong understanding of LLMs, generative AI, prompting, APIs, and vector database systems",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination.  Evidence says nothing about strong understanding of LLMs...
    }...
</pre>

### 3. Hallucinations from llama3.2:latest

This model performed better but sometimes it compared requirements to other requirements.

<pre>
[RAW CONTENT] {
  "job_requirements": [
    {
      "requirement": "Technical Writing Experience",
      "evidence": "Experience creating hands-on technical workshops, developer training materials, and comprehensive technical documentation",
      "ranking": "Exact Match" <- While this is an exact match, both the requirement and evidence are part of the Requirements.  A valid section of the resume was not cited.
    },
    {
      "requirement": "Strong Understanding of AI/ML",
      "evidence": "Agentic AI, AI prompt automation, Python, SQL",
      "ranking": "Exact Match" <- Partial Match because there is no evidence of "strong understanding"
    },
    {
      "requirement": "Technical Editing Skills",
      "evidence": "Agentic AI, AI prompt automation, Python, SQL, Exceptional technical writing and editing skills",
      "ranking": "Partial Match" <- This is a good assessment because a requirement is matched to a section of the resume.
    }...
</pre>

# Gemini Response 

Gemini often correctly infers that a requirement is met by a section of the resume.

<pre>
{
  "job_requirements": [
    {
      "requirement": "Technical Writing",
      "evidence": "Regulatory compliance documentation, Software documentation (API Reference Guides, API User Guides, Quick-start Guides, User Guides, etc.)",
      "ranking": "Exact Match" <- Gemini correctly infers that Technical writing includes documentation listed in evidence.
    },
    {
      "requirement": "Instructional Design",
      "evidence": "Software Training Curriculum",
      "ranking": "Partial Match" <- Gemini correctly infers that Software Training Curriculum includes Instructional Design
    },
    {
      "requirement": "Developer Education",
      "evidence": "Software Training Curriculum, API Reference Guides, API User Guides, Quick-start Guides",
      "ranking": "Partial Match" <- Gemini correctly infers that the evidence is part of developer education
    }...
</pre>
                                   
# Comparing Results

In this experiment, Gemini is being used to test whether the AI Prompt can work.  Gemini generally makes correct inferences.  

Running experiments on small Ollama models provides an opportunity to learn.  These models frequently hallucinated.  They found the instructions ambiguous.  The AI prompt attempted to associate Job Requirements with Requirements and Resume with Resume through capitalization and consistent terms.  It did not include examples of expected output.  The models only had one chance to complete the task with no loop providing clarification of ambiguities.  Runtime settings were not optimized and the Ollama chat API endpoint was used without streaming.  *To be continued...*

---

**References:**

[Ollama API Documentation - Endpoints](https://ollama.readthedocs.io/en/api/)

