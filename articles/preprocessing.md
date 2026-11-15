# The Power of Preprocessing

Data engineering is the invisible architecture that transforms raw, chaotic data into clean, accessible fuel for AI.  Preprocessing is the unglamorous analysis of input data so that code can comprehend it.  

In theory, a job description and a resume should include a standard set of keywords that identify the skills needed for a particular job.  In practice, job descriptions vary from formal, official verbiage to rock star slang.  

When I first tried using AI to distill my sprawling work history into a sharp, tailored resume, I took the brute-force approach. I dumped my entire career history and a target job description straight into Gemini and told it to work its magic.  Instead of a resume, it wrote science fiction.

I revised the prompt - same result.  I asked Gemini to revise the prompt - same result.  I asked other AI to revise the prompt - same.  I stopped revising the prompt and started preprocessing the data.

## JSON

In 2001, JSON (JavaScript Object Notation) was introduced as a human and machine readable format.  It became the universal standard for sending data over the internet.  Today, AI can use JSON to organize its unpredictable responses. 

I encoded my entire resume into JSON format with separate sections for Core Competencies, Professional Experience, Education, Invited Speaker, Honors and Awards, Publications, and Avocation.  This articles focuses on Professional Experience.

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
    },
    {
      "job_no": 15,
      "title": "Technical Documentation Manager",
      "company": "Cyberlaw Project",
      "dates": "Jun 2023 – Sep 2024",
      "skills": [
        "ai",
        "compliance",
        "cyber",
        "cybersecurity",
        "legal",
        "regulations",
        "regulatory"
      ],
      "bullets": [
        "Managed a comprehensive documentation pipeline for tracking, analyzing, and reporting cybersecurity legislation."
      ]
    },
    {
      "job_no": 14,
      "title": "Technical Writer",
      "company": "Amazon Zoox RoboTaxi",
      "dates": "Jul 2022 – May 2023",
      "skills": [
        "agile",
        "autonomous",
        "cloud",
        "curriculum",
        "developer",
        "guides",
        "knowledge",
        "software",
        "training",
        "user"
      ],
      "bullets": [
        "Designed software developers training program and knowledge-base hosted in Confluence",
        "Collaborated with domain experts to build curriculum for software developers.",
        "Authored online courses including Managing Data Science Experiments for Autonomous Systems, GPGPU Programming, HPC Cluster Scheduling (AWS/On-Premises), Git/GitHub Best Practices, QA/Release Management, Code Style and Code Navigation.",
        "Authored video courses including Setting up a Development Environment with Virtual Machines, Train the Trainer – How to Develop Text and Video Training for Hybrid Workplaces.",
        "Taught on-boarding classes in-person and via Zoom."
      ]
    },
    {
      "job_no": 13,
      "title": "Technical Writer",
      "company": "Crane Aerospace",
      "dates": "Feb 2022 – Jun 2022",
      "skills": [
        "aerospace",
        "automation",
        "cmmc",
        "code",
        "docs",
        "compliance",
        "regulations",
        "regulatory"
      ],
      "bullets": [
        "Partnered with IT management to formulate corporate compliance documentation for cybersecurity readiness.",
        "Developed a documentation pipeline that generated compliance templates directly from government guidelines. Significantly improved accuracy."
      ]
    },
    {
      "job_no": 12,
      "title": "Technical Writer",
      "company": "TXOne Networks",
      "dates": "Jan 2022 – Nov 2022",
      "skills": [
        "compliance",
        "ics",
        "intelligence",
        "industrial control systems",
        "ot",
        "operational technology",
        "regulations",
        "regulatory",
        "sales",
        "threat",
        "zero trust"
      ],
      "bullets": [
        "Researched and wrote authoritative recommendations for OT Zero Trust network configurations to safeguard critical infrastructure.",
        "Authored blog posts and white papers published on TXOne Networks website.",
        "Developed compliance crosswalks for NERC CIP, NIST, NIS 2, and NHS DSPT."
      ]
    },
    {
      "job_no": 11,
      "title": "Certified Content Publisher",
      "company": "Intel",
      "dates": "Aug 2021 – Dec 2022",
      "skills": [
        "automation",
        "high-performance",
        "open source",
        "performance",
        "processors",
        "semiconductor",
        "web"
      ],
      "bullets": [
        "Authored tuning guides for open-source software optimization on 3rd Gen Intel® Xeon® Scalable Processors.",
        "Automated monitoring URL links in webpages, significantly improving uptime.",
        "Achieved the Intel Certified Content Publisher certification and managed publication to website."
      ]
    },
    {
      "job_no": 10,
      "title": "Student",
      "company": "Don Quijote Spanish Language School",
      "dates": "May 2020 – Jul 2021",
      "skills": [
        "spanish",
        "languages"
      ],
      "bullets": [
        "Attended Spanish and Mandarin language classes"
      ]
    },
    {
      "job_no": 9,
      "title": "Technical Writer",
      "company": "IOTA",
      "dates": "Feb 2018 – Apr 2020",
      "skills": [
        "api",
        "blockchain",
        "documentation",
        "developer",
        "iot",
        "reference",
        "software",
        "web"
      ],
      "bullets": [
        "Developed comprehensive REST API user guides.",
        "Wrote training guides explaining cross-brand IoT device communication.",
        "Developed trade show demos",
        "Wrote curriculum and taught training seminars"
      ]
    },
    {
      "job_no": 8,
      "title": "Sales Specialist",
      "company": "Georgio Armani Corporation",
      "dates": "Nov 2017 – Jan 2018",
      "skills": [
        "sales",
        "tourism"
      ],
      "bullets": [
        "Conducted research for marketing designer clothes to Chinese tourists."
      ]
    },
    {
      "job_no": 7,
      "title": "Student",
      "company": "Don Quijote Spanish Language School",
      "dates": "Aug 2016 – Oct 2017",
      "skills": [
        "spanish",
        "languages"
      ],
      "bullets": [
        "Attended Spanish and Mandarin language classes."
      ]
    },
    {
      "job_no": 6,
      "title": "English Teacher",
      "company": "Jiangsu University of Technology",
      "dates": "Dec 2015 – Jul 2016",
      "skills": [
        "curriculum",
        "english",
        "training",
        "teaching"
      ],
      "bullets": [
        "Developed curriculum and taught English Communications and Business English."
      ]
    },
    {
      "job_no": 5,
      "company": "Oxford Seminars",
      "title": "ESL English Teacher",
      "dates": "Mar 2015 – Nov 2015",
      "skills": [
        "curriculum",
        "english",
        "training",
        "teaching"
      ],
      "bullets": [
        "Achieved TESOL teaching certificate."
      ]
    },
    {
      "job_no": 4,
      "title": "Software Validation Regulatory Compliance Specialist",
      "company": "SCIEX",
      "dates": "Jul 2009 – Feb 2015",
      "skills": [
        "compliance",
        "lab",
        "pharmaceutical",
        "software",
        "regulations",
        "regulatory",
        "testing",
        "validation"
      ],
      "bullets": [
        "Headed the international compliance project to identify regulatory gaps for certification of GLP lab equipment.",
        "Harmonized SFDA (China) and US FDA compliance standards into a unified international validation protocol.",
        "Formulated cybersecurity procedures and ISMS templates after achieving GIAC® Certified ISO-27000 Specialist, CCNA, CEH, CHFI, and PMP certifications.",
        "Led the bioinformatics documentation project for quantitation tools used for bioanalysis, environmental testing, and pharmaceutical analysis.",
        "Published project management guidance for working in China.",
        "Published case studies for best practices in leading international teams."
      ]
    },
    {
      "job_no": 3,
      "title": "AI Subject Matter Expert (SME)",
      "company": "NASA",
      "dates": "Jan 2000 – Jun 2009",
      "skills": [
        "ai",
        "aerospace",
        "autonomous",
        "compliance",
        "regulations",
        "regulatory compliance"
      ],
      "bullets": [
        "Served as a subject matter expert for technical documentation of Advanced Diagnostic Systems.",
        "Authored an award-winning survey of automated vehicle health monitoring systems for the Space Shuttle.",
        "Formulated verification and validation recommendations and regulatory compliance documentation for neural adaptive flight controllers.",
        "Contributed recommendations for testing robotic control software onboard the Mars rover, Curiosity.",
        "Served on the NASA Software Engineering Technology Leadership Panel.",
        "Awarded $1M grant funding for contingency planning research to improve autonomous drone safety.",
        "Recommended the procedure for FAA FAR Part 107 drone pilot certification.",
        "Published technical reports and journal articles. See https://github.com/NelsonPython/publications"
      ]
    },
    {
      "job_no": 2,
      "title": "Data consultant",
      "company": "Hitachi – Rush St. Luke's Presbyterian Medical Center",
      "dates": "Jan 1996 — Dec 1999",
      "skills": [
        "database",
        "data warehouse",
        "datawarehouse",
        "healthcare",
        "informatics",
        "web"
      ],
      "bullets": [
        "Built a working prototype for a health informatics web portal."
      ]
    },
    {
      "job_no": 1,
      "title": "Webmaster",
      "company": "Mirage Resorts",
      "dates": "Jan 1994 — Dec 1995",
      "skills": [
        "casino",
        "database",
        "documentation",
        "dynamic",
        "knowledge",
        "HR",
        "human relations",
        "web"
      ],
      "bullets": [
        "Architected the initial public website and the first corporate intranet featuring HR policies and procedures and employee training courses.",
        "Developed an automated tracking system for OSHA training on the critical path for opening the Bellagio Casino Resort."
      ]
    }
  ]
}

```

