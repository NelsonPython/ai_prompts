
---

**References**

[What is a vector database?](https://www.ibm.com/think/topics/vector-database)


# Appendix - Prompt

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
Bachelor's degree in Technical Writing, English, Communication, or equivalent discipline is required or equivalent combination of education, training, and experience
5-8 years' experience as a technical writer/editor in the aviation, aerospace, or defense field with Bachelor's degree OR
High School Diploma/GED or AA Degree with 9-12 years' experience as a technical writer/editor in the aviation, aerospace, or defense field
Experience preferably in the following industries: aviation, aerospace or defense
Expert command of the English language, which is necessary for original writing and content editing
Must be a Word expert with ability to format up to a 500-page document
Working knowledge of Excel and PowerPoint
Must be a team player with ability to work and communicate with proposal subject matter experts (mostly engineers)
Organizes and provides guidance for various technical publication projects
Writes, formats, edits, proofreads, copyedits and creates a variety of documents, including technical manuals, white papers, and marketing materials
Shipley proposal training and proposal writing preferred
Familiarity with DoD/Govt. contracting and the aerospace industry helpful
Knowledge of InDesign, Photoshop, and Illustrator desired
Expertly proofreads, reviews, and edits documentation for accurate use of grammar and content according to a pre-established style guide and templates
Collaborates with technical illustrator/graphic designer
Conditional on AeroVironment’s determination that it will be able to obtain an export license in a time frame consistent with AeroVironment’s business requirements
NO agencies please
Based in California, AeroVironment (AVAV) is a global leader in unmanned aircraft systems (UAS) and tactical missile systems. Founded in 1971 by celebrated physicist and engineer, Dr. Paul MacCready, we’ve been at the leading edge of technical innovation for more than 45 years. Be a part of the team that developed the world’s most widely used military drones and created the first submarine-launched reconnaissance drone, and has seven innovative vehicles that are part of the Smithsonian Institution’s permanent collection in Washington, DC.

Resume
## CORE COMPETENCIES

### Ai and automation:
Agentic AI, AI prompt automation, Python, SQL

### Compliance frameworks:
CMMC 2.0, DO 178, FAA Part 107, FDA CFR Part 11, GAMP 5, GLP, HIPAA, ISO 27001, NERC CIP, NHS DSPT, NIS 2, NIST SP 800-207 RMF

### Documentation types:
AI prompt engineering, API Reference Guides, International Regulatory Compliance, Regulatory Crosswalks, Risk Assessments, Software Documentation, Training Curriculum, White-papers

### Expertise:
Technical Writer, AI Documentation Subject Matter Expert, Regulatory Compliance Specialist, Technical Training Manager, Information Architect, Python Script Writer

### Industries:
Aerospace, Casino, Critical Infrastructure, Hospital, Pharmaceutical

### Tools:
Agile, Confluence, Git, Github, Google Docs, HTML, Jira, LibreOffice, Markdown, MS Office, PDF, SharePoint, Word

### Software:
API Reference Guides, API User Guides, FAQs, Implementation Instructions, Installation Qualification, Knowledge Articles, Operational Performance Qualification, Quick-start Guide, Release notes, Software Test Plans, Software Training Curriculum, Software Validation Plans, Standard Operating Procedures (SOPs), System Change Summaries, Technical Reference Materials, User Guides



# Appendix - Hallucination

<pre>
$ /home/jugar/job_search_agentic/v_agentic/bin/python3 prompt_run.py -f prompts/cc_core_competencies.prompt
--------------------------------------------------
Reading the prompt from 'prompts/cc_core_competencies.prompt'...

[RAW CONTENT] {
  "job_requirements": [
    {
      "requirement": "Bachelor's degree in Technical Writing, English, Communication, or equivalent discipline is required or equivalent combination of education, training, and experience",
      "evidence": "Bachelor's degree in Technical Writing or equivalent from a recognized institution, including a high school diploma or AA degree with 9-12 years of experience as a technical writer/editor",
      "ranking": "Exact Match"
    },
    {
      "requirement": "5-8 years' experience as a technical writer/editor in the aviation, aerospace, or defense field with Bachelor's degree OR",
      "evidence": "At least 5-8 years of experience as a technical writer/editor in the aviation, aerospace, or defense field with a Bachelor's degree",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Experience preferably in the following industries: aviation, aerospace or defense",
      "evidence": "Aerospace or defense experience, such as with companies like AVAV or other related organizations in the aerospace industry",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Expert command of the English language, which is necessary for original writing and content editing",
      "evidence": "Proficient in English language proficiency, evidenced by strong writing skills and ability to communicate clearly and effectively",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Must be a Word expert with ability to format up to a 500-page document",
      "evidence": "Ability to write and edit documents up to 500 pages in length using Microsoft Word",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Working knowledge of Excel and PowerPoint",
      "evidence": "Experience with Excel and PowerPoint, evidenced by proficiency in using these software applications",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Must be a team player with ability to work and communicate with proposal subject matter experts (mostly engineers)",
      "evidence": "Ability to work effectively as part of a team and communicate effectively with subject matter experts, evidenced by experience working on proposal projects",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Organizes and provides guidance for various technical publication projects",
      "evidence": "Ability to manage and coordinate various technical publication projects, evidenced by experience working on proposal development and project management",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Writes, formats, edits, proofreads, copyedits and creates a variety of documents, including technical manuals, white papers, and marketing materials",
      "evidence": "Experience writing, formatting, editing, proofreading, copyediting, and creating various technical documents, evidenced by previous work on similar projects",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Shipley proposal training and proposal writing preferred",
      "evidence": "Experience with Shipley proposal training and proposal writing, evidenced by previous work on proposal development and project management",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Familiarity with DoD/Govt. contracting and the aerospace industry helpful",
      "evidence": "Experience working with DoD/Govt. contracting and the aerospace industry, evidenced by previous work on similar projects and experience in these areas",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Knowledge of InDesign, Photoshop, and Illustrator desired",
      "evidence": "Experience with InDesign, Photoshop, and Illustrator, evidenced by previous work on similar projects and experience in these areas",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Expertly proofreads, reviews, and edits documentation for accurate use of grammar and content according to a pre-established style guide and templates",
      "evidence": "Experience proofreading, reviewing, and editing documentation for accurate use of grammar and content according to a pre-established style guide and templates, evidenced by previous work on similar projects",
      "ranking": "Exact Match"
    },
    {
      "requirement": "Collaborates with technical illustrator/graphic designer",
      "evidence": "Experience collaborating with technical illustrator/graphic designer, evidenced by previous work on similar projects and experience in these areas",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Conditional on AeroVironment’s determination that it will be able to obtain an export license in a time frame consistent with AeroVironment’s business requirements",
      "evidence": "Experience working with AeroVironment and obtaining an export license in a time frame consistent with business requirements, evidenced by previous work on similar projects",
      "ranking": "Partial Match"
    },
    {
      "requirement": "NO agencies please",
      "evidence": "Experience working on proposals without agency involvement, evidenced by previous work on similar projects",
      "ranking": "Partial Match"
    },
    {
      "requirement": "Based in California, AeroVironment (AVAV) is a global leader in unmanned aircraft systems (UAS) and tactical missile systems. Founded in 1971 by celebrated physicist and engineer, Dr. Paul MacCready, we’ve been at the leading edge of technical innovation for more than 45 years. Be a part of the team that developed the world’s most widely used military drones and created the first submarine-launched reconnaissance drone, and has seven innovative vehicles that are part of the Smithsonian Institution’s permanent collection in Washington, DC.",
      "evidence": "Experience working for AeroVironment, evidenced by previous work on similar projects and experience in the aerospace industry",
      "ranking": "Exact Match"
    }
  ]
}
</pre>
[EXIT CODE] 0

