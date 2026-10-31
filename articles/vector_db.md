# Experiment - Comparing


---

**References**

[What is a vector database?](https://www.ibm.com/think/topics/vector-database)


# Appendix - Prompt
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

### Ai and automation:
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

# Appendix - Ollama Response

### Timeout
Prompt with keywords consistently produces `Timeout`.

### Hallucinations
Removing keywords from the Prompt allows the prompt to run results in hallucinations: 

<pre>
$ python3 prompt_run.py -f prompts/cc_core_competencies.prompt
--------------------------------------------------

  Reading the prompt from 'prompts/cc_core_competencies.prompt'...
[RAW CONTENT] {
  "job_requirements": [
    {
      "requirement": "3+ years of experience in technical writing, instructional design, developer education, technical curriculum development, or a related field",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"    <- Hallucination
    },
    {
      "requirement": "Demonstrated experience creating hands-on technical workshops, developer training materials, and comprehensive technical documentation",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Strong understanding of LLMs, generative AI, prompting, APIs, and vector database systems",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Experience developing technical content for software engineers, application developers, platform engineers, or similarly technical audiences",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Exceptional technical writing and editing skills, with the ability to communicate complex concepts clearly without sacrificing technical accuracy",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Ability to read, understand, and explain code examples in Python or similar programming languages",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Familiarity with software development workflows",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Experience collaborating with engineers to validate technical documentation, troubleshoot exercises, and improve developer learning experiences",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Strong organizational skills and the ability to independently manage multiple content deliverables in a fast-moving environment",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Experience developing educational content or documentation for AI/ML platforms, developer tools, or emerging AI technologies",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Familiarity with AI safety, model evaluations, LLM testing, or responsible AI development",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Experience with vector databases, retrieval-Augmented Generation (RAG), embeddings, or agentic AI workflows",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Experience with documentation platforms, static site generators, or documentation-as-Code workflows",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    },
    {
      "requirement": "Previous experience working with AI research teams, developer platforms, or early-stage technology companies",
      "evidence": "Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "Exact Match"   <- Hallucination
    }
  ]
}
</pre>

# Appendix - Gemini Response 

<pre>
{
  "job_requirements": [
    {
      "requirement": "Technical Writing",
      "evidence": "Regulatory compliance documentation, Software documentation (API Reference Guides, API User Guides, Quick-start Guides, User Guides, etc.)",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Instructional Design",
      "evidence": "Software Training Curriculum",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Developer Education",
      "evidence": "Software Training Curriculum, API Reference Guides, API User Guides, Quick-start Guides",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Technical Curriculum Development",
      "evidence": "Software Training Curriculum",
      "ranking": "Exact Match"
    },
    {
      "requirement": "LLMs",
      "evidence": "AI prompt automation, AI Prompt Engineering",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Generative AI",
      "evidence": "Agentic AI, AI prompt automation, AI Prompt Engineering",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Prompting",
      "evidence": "AI prompt automation, AI Prompt Engineering",
      "ranking": "Exact Match"
    },
    {
      "requirement": "APIs",
      "evidence": "API Reference Guides, API User Guides",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Vector Database Systems",
      "evidence": "None",
      "ranking": "No Match"
    },
    {
      "requirement": "Hands-on Technical Workshops",
      "evidence": "None",
      "ranking": "No Match"    <- Partial Hallucination
    },
    {
      "requirement": "Developer Training Materials",
      "evidence": "Software Training Curriculum, API Reference Guides, Quick-start Guides",
      "ranking": "Exact Match" 
    },
    {
      "requirement": "Technical Documentation",
      "evidence": "Software documentation, Regulatory compliance documentation",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Interactive Exercises",
      "evidence": "None",
      "ranking": "No Match"    <- Hallucination
    },
    {
      "requirement": "Code Walkthroughs",
      "evidence": "None",
      "ranking": "No Match"   <- Hallucination
    },
    {
      "requirement": "Lab Guides",
      "evidence": "None",
      "ranking": "No Match"   <- Hallucination
    },
    {
      "requirement": "Instructor Resources",
      "evidence": "None",
      "ranking": "No Match"   <- Hallucination
    },
    {
      "requirement": "API and SDK Documentation",
      "evidence": "API Reference Guides, API User Guides",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Technical Accuracy",
      "evidence": "Regulatory compliance documentation (Software Installation/Operational/Performance Qualification, Validation Plans, SOPs)",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Accessibility",
      "evidence": "None",
      "ranking": "No Match"   <- Hallucination
    },
    {
      "requirement": "Real-World Developer Workflows",
      "evidence": "Git, Github, Markdown, HTML, Agile",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Python",
      "evidence": "Python listed under Ai and automation",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Git/GitHub",
      "evidence": "Git, Github listed under Tools",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Markdown",
      "evidence": "Markdown listed under Tools",
      "ranking": "Partial Match"   <- Hallucination
    },
    {
      "requirement": "Version Control",
      "evidence": "Git, Github listed under Tools",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Testing",
      "evidence": "Software Installation Qualification, Software Operational Qualification, Software Performance Qualification, Software Validation Plans",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Engineering Partners",
      "evidence": "Agile",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Technical Validation",
      "evidence": "Software Validation Plans, Software Installation Qualification, Software Operational Qualification, Software Performance Qualification",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Troubleshooting",
      "evidence": "Cybersecurity Guidance, Quick-start Guides, FAQs, Tuning Guides",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Developer Learning Experience",
      "evidence": "Software Training Curriculum, Quick-start Guides, API Reference Guides",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Agentic AI",
      "evidence": "Agentic AI listed under Ai and automation",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Model Evaluations",
      "evidence": "None",
      "ranking": "No Match"   <- Hallucination
    },
    {
      "requirement": "LLM Testing",
      "evidence": "None",
      "ranking": "No Match"
    },
    {
      "requirement": "Responsible AI Development",
      "evidence": "None",
      "ranking": "No Match"   <- Hallucination
    },
    {
      "requirement": "Vector Databases",
      "evidence": "None",
      "ranking": "No Match"
    },
    {
      "requirement": "Retrieval-Augmented Generation (RAG)",
      "evidence": "None",
      "ranking": "No Match"
    },
    {
      "requirement": "Embeddings",
      "evidence": "None",
      "ranking": "No Match"
    },
    {
      "requirement": "Agenic AI Workflows",
      "evidence": "Agentic AI, AI prompt automation",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Documentation Platforms",
      "evidence": "Confluence, SharePoint listed under Tools",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Static Site Generators",
      "evidence": "None",
      "ranking": "No Match"
    },
    {
      "requirement": "Documentation-as-Code Workflows",
      "evidence": "Git, Github, Markdown, HTML listed under Tools",
      "ranking": "Partial Match"
    },
    {
      "requirement": "3+ years of experience in technical writing, instructional design, developer education, technical curriculum development, or a related field",
      "evidence": "Lists competencies in Regulatory compliance documentation, Software documentation, Software Training Curriculum",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Demonstrated experience creating hands-on technical workshops, developer training materials, and comprehensive technical documentation",
      "evidence": "Software Training Curriculum, Software documentation (API Reference Guides, API User Guides, Quick-start Guides, User Guides)",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Strong understanding of LLMs, generative AI, prompting, APIs, and vector database systems",
      "evidence": "Agentic AI, AI prompt automation, AI Prompt Engineering, API Reference Guides, API User Guides (No vector database systems mentioned)",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Experience developing technical content for software engineers, application developers, platform engineers, or similarly technical audiences",
      "evidence": "API Reference Guides, API User Guides, Software Training Curriculum, Tuning Guides",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Exceptional technical writing and editing skills, with the ability to communicate complex concepts clearly without sacrificing technical accuracy",
      "evidence": "International Regulatory Compliance Guides, Journal Articles, Regulatory Crosswalks, Software Validation Plans, White-papers",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Ability to read, understand, and explain code examples in Python, TypeScript, or similar programming languages",
      "evidence": "Python, SQL, HTML listed in core competencies and tools",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Familiarity with software development workflows, including Git/GitHub, Markdown/MDX, version control, and testing",
      "evidence": "Git, Github, Markdown, Software Validation Plans",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Experience collaborating with engineers to validate technical documentation, troubleshoot exercises, and improve developer learning experiences",
      "evidence": "Software Validation Plans, Agile, Software Training Curriculum",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Strong organizational skills and the ability to independently manage multiple content deliverables in a fast-moving environment",
      "evidence": "Agile, Jira, Confluence listed under Tools",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Experience developing educational content or documentation for AI/ML platforms, developer tools, or emerging AI technologies",
      "evidence": "Agentic AI, AI prompt automation, AI Prompt Engineering, Software Training Curriculum, API Reference Guides",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Familiarity with AI safety, model evaluations, LLM testing, or responsible AI development",
      "evidence": "Cybersecurity Guidance, ISO 27001, NIST SP 800-207 RMF (No explicit AI safety, model evaluation, or LLM testing mentioned)",
      "ranking": "No Match"
    },
    {
      "requirement": "Experience with vector databases, retrieval-Augmented Generation (RAG), embeddings, or agentic AI workflows",
      "evidence": "Agentic AI, AI prompt automation",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Experience with documentation platforms, static site generators, or documentation-as-Code workflows",
      "evidence": "Confluence, SharePoint, Git, Github, Markdown, HTML",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Previous experience working with AI research teams, developer platforms, or early-stage technology companies",
      "evidence": "Industries: Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical",
      "ranking": "No Match"   <- Partial Hallucination
    }
  ]
}
</pre>

