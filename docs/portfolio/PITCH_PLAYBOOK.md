# Presentation and Personal Pitch Playbook

**Initialized:** 2026-11-07  
**Status:** draft language for a project in **planning/design**, not a shipped app. Customize personal details to what the owner can substantiate. Do not imply the project has already been deployed or legally validated.

## 1. Interview self-introduction — ~25 seconds

"I'm an aspiring AI engineer with experience from machine-learning projects, including Sinhala-focused model evaluation. I'm now developing my skills in production AI engineering through a Sri Lankan legal-awareness project. My focus is not simply generating answers: it's designing verifiable legal-source retrieval, clear uncertainty handling, security boundaries and repeatable evaluation. The project is currently in requirements and architecture planning, and I'm documenting trade-offs and evidence as I build."

## 2. Project elevator pitch — ~35 seconds

"People often find legal explanations online without knowing which law supports them or whether the source is still current. I'm designing an AI-powered legal-awareness assistant for Sri Lanka, initially covering selected questions about fundamental rights, police interactions and complaint institutions. It will provide a plain-language summary, official source references, an explicit evidence status and a longer explanation. A major design decision is to verify not just that a document is official but also its version and legal effective date. The MVP will use one backend for Android and Web, with publication gated by legal review and safety testing."

## 3. Technical deep-dive — ~90 seconds

"I propose a modular monolith: Flutter Web and Android clients call a Python/FastAPI backend. The backend retrieves only approved, versioned legal passages from a PostgreSQL source registry. I'll compare lexical retrieval with vector/hybrid search on a reviewed benchmark rather than assuming embeddings help. A hosted LLM will draft a structured explanation from the retrieved passages, but deterministic validators will check allowed versions, exact citation pointers and output shape. If evidence is missing or a check fails, the system abstains or qualifies the answer. An important limitation is that those checks cannot prove semantic legal correctness; human-reviewed legal scenarios remain essential. We also plan to avoid default chat-history storage and keep secrets entirely on the backend. The system is still in design, so I won't claim benchmark scores or deployment results yet."

## 4. Group presentation outline — 5 minutes

1. **Problem (45s):** An official PDF can still be outdated, and a convincing chatbot can be wrong.
2. **User and scope (45s):** Ordinary citizens seeking *general* legal awareness; narrowly defined first pilot.
3. **Core solution (60s):** Summary → legal citations → evidence status → explanation; show a conceptual UI, not a fake working app.
4. **Architecture (75s):** Shared clients/API, source registry, retrieval, LLM draft, version/citation gates, safe abstention.
5. **Validation and ethics (45s):** Human-reviewed benchmark, no autonomous actions, data minimization, correction process.
6. **Status and next step (30s):** Phase 0 documents drafted; source and reviewer validation still pending.

## 5. Honest demo narration — current state

"This is a design walkthrough, not a live legal advice service. We have a proposed answer format and a documented source-approval workflow. Next we will build a small, reviewed corpus and evaluate retrieval and citation checks before generating user-facing answers."

**When a working demo later exists:** show one success and one deliberate abstention; cite actual document/version IDs and benchmark run. Never describe unreviewed synthetic answers as verified law.

## 6. Difficult interview questions

**Q: How do you prevent hallucinations?**  
A: "I can't guarantee zero hallucinations. I'm designing approved-source retrieval, source/version checks, structured outputs, citation validation, abstention and human-reviewed evaluation. I will report residual error rates when measured."

**Q: Isn't RAG just searching PDFs?**  
A: "For legal information, document authority and effective dates matter. The product needs provision-level status, traceable citations, human review and evaluation; indexing documents alone is insufficient."

**Q: Why not fine-tune an open-source legal model?**  
A: "Fine-tuning does not ensure knowledge of current amendments. An approved corpus and retriever provide better auditability initially; we'll test the simpler baseline before adding more model complexity."

**Q: How do you secure prompt injection?**  
A: "A prompt is not a security boundary. The LLM has no action tools; only approved sources enter retrieval, API keys remain server-side, and outputs are checked by backend policy and tests."

**Q: What about Sinhala/Tamil?**  
A: "They're essential long-term, but legal translation is high risk. We'll validate each language against human-reviewed legal scenarios instead of relying on general multilingual ability."

**Q: Is it compliant with Sri Lanka's data protection law?**  
A: "Compliance hasn't yet been established. We've found staged commencement orders and plan to minimize data, review provider processing and engage appropriate legal advice before any public release."

**Q: What have you personally accomplished?**  
A: "At this stage I have established the project specification and am reviewing the requirements and design proposals. Implementation, tests and measured outcomes are not yet complete. I'll connect future claims to actual code and evaluation artifacts."

## 7. Evidence and delivery practice

For every public talk or interview, update the stage of the project, confirm the demo truly works, cite GitHub commits and evaluation reports, remove unearned claims, and rehearse explaining one design trade-off without buzzwords.

## Story update — 2026-11-08: Why not ingest everything and answer everything?

**30-second explanation (at design stage):**

"I've separated **document discovery** from **validated answer coverage**. Sri Lanka publishes important legal materials across Parliament, official gazettes and court sources, but collecting PDFs alone won't show which provisions were active on a particular date or prove an AI explanation correct. My design preserves past and future laws with explicit status labels, while current legal explanations must cite applicable provisions. I plan to grow the coverage only as legal reviews and benchmark results support it. The system is still in Phase 0; I haven't implemented or measured those controls yet."

**Revenue/ethics question:** "A lawyer directory may be useful later, but paid referrals and commission arrangements raise professional-conduct and privacy issues, so we are not letting potential payments influence legal answers or assuming the business model is permissible."

**Budget question:** "I budgeted the first sprint for manual source cataloguing and evaluation design, rather than paying for an unverified chatbot or broad web crawler."


## Pitch update — 2026-11-08: data-driven MVP selection

**Current truthful 20-second explanation:**

"For our Sri Lankan legal-awareness platform, we are organizing official materials into 20 candidate legal areas and comparing source provenance, amendment history, extractability and review feasibility before choosing the first AI-answer topics. The manifest is a research starting point, not a complete or approved legal database. We'll validate selected topics and show both current and historical or upcoming legal changes with clear status labels."

**Interview follow-up:** Why not scrape everything first? "A bulk download is not the same as a reliable corpus. We need provenance, version links and provision-level legal force; I prefer controlled discovery, then quality evaluation, and only then approval for answers."

## Pitch update — Batch 001 real ingestion evidence, 2026-11-08

**25-second engineering explanation:** "We collected ten official-source legal PDFs totaling 538 pages and recorded cryptographic hashes and exact PDF-page provenance. The first extraction showed why legal RAG needs quality gates: one entire Act was image-only, and another had OCR-corrupted text. We are tracking amendments and scheduled commencement separately rather than treating the latest downloaded PDF as complete law. The material is still under review; no AI legal answers have been approved."

**Question: Why not launch now?** "Text extraction is not verification. A legal answer requires the right effective provision, a reliable citation and a reviewed explanation; we haven't measured those capabilities yet."

**Claim discipline:** Do not say 'we indexed 538 pages for reliable legal question answering'. Say 'we enumerated and drafted page-level text for 538 source pages; extraction and legal status still need review'.

## Presentation story — 2026-11-08: Why not simply extract text from every PDF?

**~40-second technical pitch (demonstrated prototype, not deployed service):**

"Our first ingestion batch revealed two different failures. One official Act was image-only, so normal PDF extraction returned nothing. Another had a text layer, but some words were visibly corrupted. This led me to adopt an adaptive ingestion architecture: preserve the original source, detect extraction quality, route scans to OCR, and validate the results before legal text can enter the approved RAG corpus. We tested OCR locally on both examples and recovered searchable text from all 20 pages of the scanned Act. But searchable text is not the same as legally accurate text—manual proofing and measured accuracy are still required."

**Audience takeaway:** Good AI architecture does not mean more folders or tools. It means responding to real failure modes with a reusable, testable safety boundary.

**Whiteboard sketch:** `Original PDF + hash → text inspection → direct extraction OR OCR → page-aligned verification → human/source approval → approved search corpus`.

**Hard questions:**

- **Why not OCR every page?** More compute and possible damage to good digital text; use an adaptive fallback.
- **Is the problem solved?** Two OCR output PDFs are searchable and visually sampled, but transcription correctness and backend automation are not measured or complete.
- **What would you measure?** Gold text word error rate, section-number accuracy, page-text presence, review queue size, and ingestion runtime per page.
- **Who did the work?** The owner explicitly chose the pattern and asked to retain it as an ADR. The initial local OCR conversion was run with assistant help.

## Demo and presentation update — OCR source-quality incident (2026-11-08)

**Short story:** “Our first batch exposed a hidden failure mode in legal AI: even if an OCR PDF is searchable, its text can turn a paragraph (b) reference into paragraph (6). I verified selected examples in the original page image rather than trusting the extracted text. We record those failures before indexing, and do not treat unreviewed material as approved law.”

**Evidence:** Three short-span OCR issues owner-confirmed in the Child Protection Authority Act; other three worksheet items unreviewed. No overall OCR accuracy figure is available. The sample was selected to expose failures, not estimate population-wide error rates.

**Trade-off:** With roughly ten hours/week, prioritize targeted quality gates for candidate answer provisions and automated checks over manually certifying every page now. **Limitation:** A future human/legal review process is still necessary for answer release.
