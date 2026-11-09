ResumeRooms 🟦

Walk your resume through the hiring process. ResumeRooms is a browser-based, 3D-styled career tool: upload a resume, get an ATS-style score from four different "reviewers", fix what's wrong, study what's missing, and rehearse in a mock-interview room themed like the company you're targeting.

Single static file. No backend, no build step, no sign-up. Your resume text never leaves your browser.

<!-- Add a screenshot or GIF here: docs/demo.gif -->
Why this exists

Most free ATS checkers stop at a number. Candidates then have to guess what to fix, what to learn, and how to practise. ResumeRooms turns that into a guided path through four rooms:

Room	What happens
01 · ATS Lab	Pick a target role, optionally paste a job description, upload a resume (PDF, DOCX, TXT) or paste text. Get a scorecard.
02 · Suggestion Room	Prioritised fixes: contact details, missing keywords, section order, weak phrases, repeated words, typos, STAR-method gaps.
03 · Study Room	Topic cards built from your missing keywords, each with an official-docs link and YouTube search links.
04 · Mock Test Room	Choose a company office (Nvidia, Google, Amazon, Microsoft, TCS/Infosys, Other). Timed questions: resume deep-dives, technical, behavioural, company-style.

A small candidate avatar walks between rooms as you scroll.

Features
Four-reviewer scoring: ATS parser, technical recruiter, hiring manager and HR each score separately, then combine into one total.
Role or JD matching: six built-in role keyword banks, or paste a job description and its top terms become the keyword list.
Actionable fixes with severity (high / medium / low) instead of just a number.
Resume deep-dive questions generated from skills actually found in your resume.
3D feel without a 3D engine: CSS perspective floors, mouse-tilt scenes, scroll parallax, scroll-reveal and a scroll-driven avatar.
Light and dark mode via prefers-color-scheme; respects prefers-reduced-motion.
Private by design: all parsing and scoring run client-side.
How it works
flowchart LR
  A[Upload PDF / DOCX / TXT<br/>or paste text] --> B[Text extraction<br/>pdf.js · mammoth.js]
  B --> C[analyze()]
  J[Role keyword bank<br/>or pasted JD] --> C
  C --> D[Four reviewer scores]
  C --> E[Fix list]
  C --> F[Missing keywords]
  D --> G[ATS Lab scorecard]
  E --> H[Suggestion Room]
  F --> I[Study Room topics]
  F --> K[Mock Test questions]
Scoring model

analyze() runs these checks on the extracted text:

Keywords: hits and misses against the role bank (or JD terms)
Contact: email, phone, LinkedIn, GitHub/portfolio (required for technical roles)
Structure: Summary, Skills, Experience, Projects, Education headings and their order
Impact: share of bullet-like lines with numbers; strong action verbs; weak phrases ("responsible for", "worked on")
Language: doubled words, lowercase "i", common typos, odd spacing, repeated words and repeated bullet openers
Length: word count against a typical fresher range
Reviewer	Weight in total	Looks mostly at
ATS parser	35%	Keyword coverage, standard sections, parsable contact info
Technical recruiter	20%	Contact completeness, summary, quantified impact, length
Hiring manager	25%	Keyword depth, projects/GitHub, metrics, skills section
HR	20%	Structure, grammar and consistency, professionalism
Tech stack
HTML, CSS, vanilla JavaScript (single file)
pdf.js for PDF text extraction
mammoth.js for DOCX text extraction
Libraries loaded from cdnjs; no npm install required
Getting started
bash
git clone https://github.com/<your-username>/resume-rooms.git
cd resume-rooms

# Option 1: just open it
open index.html            # macOS  (Windows: start index.html, Linux: xdg-open index.html)

# Option 2: serve locally
python -m http.server 8000 # then visit http://localhost:8000
Deploy for free
GitHub Pages: Settings → Pages → deploy from main branch, root folder.
Netlify / Vercel / Cloudflare Pages: drag and drop the folder.
Project structure
resume-rooms/
├── index.html   # entire app: markup, styles, scripts
└── README.md

Key places to edit inside index.html:

Name	Purpose
ROLES	Keyword bank per role. Add a role and it appears in the dropdown.
analyze()	Scoring and fix-generation logic.
D	Topic → official docs URL + short study note.
Q, BH, CQ	Role, behavioural and company-style question banks.
CO	Company names and accent colours for the mock room.
Known limitations (read this before trusting a score)

The score is a heuristic, not a real ATS. Workday, Greenhouse, Taleo and others parse differently and publish no scoring formula. Treat the number as a checklist, not a verdict.
Keyword matching is literal. "ML" will not match "machine learning" yet.
Grammar checks are rule-based and catch only simple issues.
Mock questions are original, written around commonly discussed interview themes. They are not scraped from Glassdoor or Reddit; the page links to search results for real candidate reports.
YouTube links are search results, not hand-picked videos. Sort by recent uploads and view count.
PDF extraction can scramble multi-column layouts, and scanned/image-only PDFs have no text. Paste text instead. Legacy .doc is not supported.

Roadmap
 Synonym- and embedding-aware keyword matching
 LLM-powered STAR rewrites through a small backend (FastAPI/Flask)
 Server-side parsing (pdfplumber, python-docx) for more reliable extraction
 True 3D rooms with Three.js
 Licensed or user-submitted interview question database
 Save progress and score history
 Voice-based mock interviews with feedback
Privacy

Resume text is processed entirely in your browser. There is no server, no analytics and no storage in this version. If you add an LLM backend later, tell users clearly what is sent where.

Contributing

Issues and pull requests are welcome. Good first contributions: new role keyword banks, more company question sets, better typo and grammar rules, accessibility improvements.

Fork the repo and create a branch: git checkout -b feature/your-change
Make your change and test it in a browser with a few sample resumes
Open a pull request describing what changed and why
Acknowledgements

Visual direction (dark navy, glowing blue square, terrain, scroll storytelling) was inspired by the public look of bluesqx.com. No code, images or branding were copied.

License

MIT. Add a LICENSE file to the repo.

Author

Built by Vishal Kashyap · LinkedIn