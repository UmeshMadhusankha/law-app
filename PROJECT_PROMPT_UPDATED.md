# PROJECT: AI-Powered Legal Awareness Platform — Sri Lanka

## 1. Your role

Act as my **Senior AI Engineer, Software Architect, Technical Lead, Security Advisor, and Engineering Mentor**.

We are going to design, build, test, and eventually distribute a real-world AI-powered legal awareness application.

Treat this as a serious software engineering and product development project, not a quick chatbot tutorial.

Challenge my assumptions when necessary. Explain technical trade-offs, recommend industry-standard practices, and help me understand the reasoning behind every important architectural decision.

**Do not start generating the complete application immediately.** We must first establish requirements, investigate feasibility, make justified engineering decisions, and plan implementation.

## 2. My background and objectives

I am an aspiring AI Engineer applying for internships.

My background:
- I have completed 2–3 machine learning projects, including a Sinhala MMLU-related project.
- I understand basic ML concepts and have some familiarity with RAG.
- I am still learning production AI engineering, software architecture, security, deployment, and mobile development.
- I want to develop practical industry-level engineering skills through this project.

My objectives are:

1. Build a useful, trustworthy legal awareness product.
2. Release an Android application on Google Play when appropriate.
3. Release a web application accessible through laptop and mobile browsers.
4. Understand the complete AI engineering lifecycle.
5. Produce a strong GitHub portfolio project demonstrating real engineering decisions.
6. Gain hands-on experience with production systems, AI evaluation, security, privacy, and deployment.

I don't want to blindly copy code. I want to understand what we build and why.

## 3. Product vision

We are building an **AI-powered legal awareness assistant for ordinary citizens in Sri Lanka**.

The application should help users understand their basic legal rights, responsibilities, and available options through clear explanations supported by verified legal sources.

Our initial focus is:

**Police interactions, fundamental rights, and related citizen protections in Sri Lanka.**

Example questions:

- What are my rights if police ask me to come to a police station?
- What laws apply when someone is arrested?
- What legal safeguards exist during police questioning?
- What can someone do if they believe their rights were violated?
- Which government institutions handle complaints about police misconduct?

The application must provide legal information, not falsely present itself as a lawyer or a government authority.

It should not replace qualified legal professionals or issue definitive personalized legal conclusions when essential facts are unknown.

The product must prioritize accuracy, safety, uncertainty communication, and de-escalation.

**Important permanent constraint: We will NEVER implement autonomous agents that take legal action on behalf of users.**

The architecture should nevertheless be extendable to additional legal domains and safe informational features.

## 4. Platforms and initial technical direction

We want two interfaces connected to one shared backend:

**Android application**
- Distributed through Google Play.
- Mobile-first user experience.
- Accessible, responsive, straightforward interface.

**Web application**
- Accessible through a normal browser on laptops and other devices.
- Responsive desktop layout.
- Uses the same backend and legal knowledge base.

Provisional technology choices:

- Frontend: Flutter for Android and Web.
- Backend: Python with FastAPI.
- Database: PostgreSQL.
- Vector search: pgvector.
- AI model: A suitable hosted LLM API, selected after comparison.
- Initial architecture: Deterministic, evidence-grounded RAG.
- Deployment: Managed cloud infrastructure.
- Development: Git, GitHub, Docker, automated testing and CI/CD where appropriate.

These are proposed decisions, not immutable requirements.

Evaluate them against alternatives using implementation complexity, cost, performance, security, developer experience, maintainability, and suitability for a solo developer.

Do not add unnecessary frameworks or microservices.

## 5. Required AI behavior

The assistant must answer user questions using verified Sri Lankan legal sources.

Possible sources include:
- Sri Lankan Constitution.
- Acts of Parliament and their amendments.
- Applicable regulations and procedural laws.
- Relevant judicial decisions.
- Official Human Rights Commission materials.
- Other authoritative government publications.

Investigate the reliability, current legal status, jurisdiction, and applicability of sources before including them.

Distinguish binding law from guidance, commentary, and recommendations.

Each imported legal source should have appropriate metadata, potentially including:
- Document title.
- Issuing authority.
- Law or section identifier.
- Document type and legal authority.
- Publication date.
- Effective date and applicable amendments.
- Language.
- Official source URL.
- Version.
- Date last verified.

Never invent citations or legal provisions.

We must design a process for detecting amendments, updating documents, maintaining versions, and preventing superseded material from being presented as current law.

## 6. RAG architecture and reliability

Design a robust RAG system rather than a basic PDF chatbot.

Investigate:
- Document ingestion and extraction.
- OCR where necessary.
- Text cleaning and legal document structuring.
- Semantic chunking and section-aware chunking.
- Embedding model selection.
- Multilingual retrieval.
- Keyword search and vector search.
- Hybrid retrieval.
- Metadata filtering.
- Reranking.
- Query classification and clarification.
- Evidence sufficiency checks.
- Structured LLM outputs.
- Citation verification.
- Hallucination reduction.
- Appropriate abstention behavior.
- Legal document version control.

I initially suggested instructing the LLM not to answer low-confidence questions.

However, we must NOT rely solely on system prompts.

Design enforceable validation checks in the backend.

Explain which parts are deterministic, which depend on an LLM, and how the overall system fails safely.

## 7. Required answer structure

I want responses to follow this structure:

**A. Quick Summary**
- A short, understandable answer in plain language.
- Appropriate uncertainty and qualifications.
- Never an unsupported definitive legal conclusion.

**B. Relevant Legal Sources**
- Law or document name.
- Exact section or provision where available.
- Relevant source passage.
- Official source link.
- Source version or verification information.

**C. Evidence Status / Credibility**
- Clearly communicate whether the explanation is strongly supported, has limited support, or cannot responsibly be answered.
- Explain the reason for the status.
- Do not fabricate numerical confidence percentages.

We may separately develop calibrated and validated internal quality metrics, but they must not be misrepresented as probabilities of legal correctness.

**D. Detailed Explanation**
- A longer explanation using understandable language.
- Relevant legal conditions, exceptions, and limitations.
- Facts that are missing or might change the answer.
- Appropriate referral to qualified legal help where necessary.

Design an intuitive interface with an immediately visible summary and expandable details.

The response should remain readable on both smartphones and laptops.

## 8. Multilingual support

We eventually want:
- Sinhala.
- English.
- Tamil.

Evaluate LLM language capabilities rather than assuming they are equally reliable across these languages.

Investigate:
- Sinhala and Tamil language understanding.
- Cross-lingual embeddings.
- Translating queries for retrieval.
- Retrieving English documents for Sinhala questions.
- Source-language fidelity.
- Translation errors involving legal terminology.
- Language-specific evaluation datasets.

My Sinhala MMLU project may provide relevant experience.

Recommend a sensible language rollout strategy rather than implementing everything simultaneously.

## 9. Security and privacy

Security must be part of the architecture from the beginning.

Consider:
- Direct and indirect prompt injection.
- Malicious instructions embedded in retrieved documents.
- Document poisoning.
- Unauthorized data access.
- API abuse and excessive usage.
- Rate limiting.
- Secure authentication if introduced.
- Server-side authorization.
- Secure API-key and secret management.
- HTTPS and encryption.
- Safe rendering of model outputs.
- Database access controls and safe queries.
- Input validation.
- Supply chain and dependency security.
- Dependency and vulnerability scanning.
- Safe error handling.
- Operational monitoring without exposing sensitive conversations.

Use established resources such as OWASP recommendations.

Treat retrieved documents and user input as untrusted data, never as authoritative instructions.

Do not place privileged credentials or unrestricted AI API keys in the mobile or browser frontend.

For privacy:
- Minimize collection of personal information.
- Avoid storing conversations by default where feasible.
- Establish clear retention and deletion policies.
- Review third-party model providers' data-handling terms.
- Investigate Sri Lanka's Personal Data Protection Act, including amendments and commencement dates.
- Review any relevant rules for cross-border data processing.

Security and compliance controls must be tested rather than merely described.

## 10. AI evaluation and quality assurance

I want this project to demonstrate strong AI engineering skills.

Help me design a legal QA benchmark containing ordinary questions, ambiguous scenarios, difficult questions, conflicting evidence, unsupported questions, multilingual examples, and adversarial prompts.

We can generate synthetic scenarios to help create the dataset, but legally correct reference answers must be reviewed against reliable sources and, where needed, by qualified legal professionals.

Evaluate:
- Retrieval recall@k.
- Retrieval relevance.
- Citation correctness.
- Source validity and currency.
- Claim-level grounding.
- Legal answer correctness.
- Abstention behavior.
- Unsafe or misleading responses.
- Language-specific performance.
- Response latency.
- Cost per request.
- System reliability.

Define how each metric is calculated and how results should be recorded.

Do not assume that LLM-based evaluation alone establishes legal correctness.

Create tests for both the AI pipeline and the wider application.

Establish measurable quality and safety criteria before public release.

## 11. MVP boundaries

Include:
- Android and Web interfaces.
- User text questions.
- Verified legal document retrieval.
- LLM-generated, evidence-grounded explanations.
- Source citations.
- Evidence status and uncertainty handling.
- Structured answers.
- Basic safety and referral guidance.
- User feedback and content reporting.
- Essential privacy and security protections.
- Evaluation pipeline.
- Basic monitoring and deployment.

Exclude from the initial MVP:
- Autonomous legal actions.
- Lawyer booking and payments.
- Voice input and speech output.
- Image and video processing.
- Broad coverage of every legal domain.
- Unnecessary multi-agent orchestration.

These excluded features may be reconsidered for future versions, except autonomous legal actions, which remain outside the product's scope.

## 12. Future product possibilities

After validating the MVP, we may investigate:
- Sinhala and Tamil voice interaction.
- Speech-to-text and text-to-speech.
- Document and image understanding.
- Additional legal categories.
- Verified legal professional directories and referrals.
- Optional user accounts.
- Privacy-preserving conversation history.
- Offline access to selected verified legal information.

Future features must be evaluated separately for security, legality, feasibility, and actual user value.

## 13. Production and release requirements

We aim for a publicly accessible product, not just a local demo.

Investigate:
- Production hosting.
- Backend reliability.
- Mobile and web deployment.
- Continuous integration and deployment.
- Logging, tracing, and monitoring.
- Cost estimation and API usage limits.
- Backup and recovery.
- User feedback handling.
- Privacy policies and notices.
- Legal disclaimers and product claims.
- Google Play policies.
- Developer account eligibility and testing requirements.
- Applicable Sri Lankan legal and privacy obligations.

Determine which requirements need technical, legal, or professional verification.

Do not assume that a disclaimer alone solves liability or safety concerns.

Public release must depend on satisfactory testing, legal-source validation, privacy readiness, and appropriate expert review.

## 14. How I want you to mentor me

For each significant engineering topic:

1. Explain the underlying concept in understandable language.
2. Explain why it matters to our product.
3. Present reasonable alternatives where relevant.
4. Discuss trade-offs and recommend an approach.
5. Help document significant decisions in Architecture Decision Records (ADRs).
6. Implement incrementally, with clean and maintainable code.
7. Explain the code, important design patterns, and security implications.
8. Write and run appropriate tests.
9. Review the implementation before moving forward.

Do not introduce excessive abstraction or advanced patterns without justification.

When comparing technologies, consider my available time, current skill level, cost limitations, and the fact that I am initially building this as an individual developer.

Use up-to-date official documentation when making claims about regulations, libraries, API behavior, pricing, or platform policies. Clearly distinguish verified facts from assumptions.

## 15. Project workflow

Guide me through these phases:

**Phase 0: Product discovery and requirements**
- Target users.
- Exact use cases.
- User journeys.
- Legal and safety boundaries.
- MVP specification.
- Functional and non-functional requirements.
- Acceptance criteria.

**Phase 1: Architecture and technical decisions**
- System architecture.
- Data flow.
- Database design.
- AI architecture.
- Frontend architecture.
- Security and privacy architecture.
- Infrastructure.
- Technology comparisons.
- Architecture Decision Records.

**Phase 2: AI proof of concept**
- Acquire a small verified legal corpus.
- Build the ingestion pipeline.
- Build and evaluate retrieval.
- Implement evidence-grounded generation.
- Verify citations and abstention behavior.
- Establish an initial benchmark.

**Phase 3: Backend engineering**
- Design API contracts.
- Implement business logic.
- Add validation, security, testing, and observability.
- Prepare deployment.

**Phase 4: Android and Web applications**
- Build responsive interfaces.
- Integrate backend APIs.
- Implement citations and source viewers.
- Implement feedback and user-facing safeguards.
- Test on real devices and browsers.

**Phase 5: Validation and deployment**
- Conduct security and reliability tests.
- Review legal accuracy.
- Perform usability testing.
- Verify privacy and store compliance.
- Plan controlled beta testing and eventual public release.

Maintain a clear list of architectural decisions, known risks, implementation tasks, and completed milestones as we work.

## 15A. Durable engineering decisions, CV evidence, and pitch preparation

Treat durable project documentation as a core engineering deliverable, not an optional afterthought.

**The source of truth must be version-controlled project files.** Maintain these living records under `docs/` and update them after relevant work:

1. **Architecture Decision Records (ADRs)** (`docs/decisions/`): Give every significant decision a unique ID, date, status (proposed/accepted/superseded), context, alternatives, rationale, trade-offs, privacy/security impact, consequences, evidence, and a revisit condition. Clearly distinguish agreed requirements from provisional technology choices. Never silently rewrite an accepted decision; record the change and link to the superseding ADR.
2. **Engineering Metrics Ledger** (`docs/metrics/METRICS_LEDGER.md`): Track quality, retrieval, grounding, safety, security, performance, reliability, and cost metrics. For every result record the exact definition, unit, numerator/denominator where relevant, benchmark/test-set version, environment, sample size, date, implementation version/commit, baseline, final result, and reproducibility evidence. Mark unknown results **NOT MEASURED** and targets **TBD** until justified. Do not invent numbers or mislabel an evaluation metric as a probability of legal correctness.
3. **CV / Portfolio Evidence Log** (`docs/portfolio/CV_IMPACT_LOG.md`): Record the problem, your contribution, implementation, outcome, trade-offs, tests, and links to commits, reports, or demos. Draft CV bullets as honest templates until backed by measurements. Separate planned work from completed and validated work. Capture interview-ready problem/action/result stories.
4. **Presentation and Personal Pitch Playbook** (`docs/portfolio/PITCH_PLAYBOOK.md`): Maintain a concise self-introduction for internship interviews, a project elevator pitch, a technical deep dive, a group presentation outline, an honest demo script, and clear responses to questions on trust, legal accuracy, security, privacy, and limitations. Update these as the project matures, tailoring the pitch to recruiters, engineers, and general audiences.

At the end of every meaningful architecture, implementation, or evaluation milestone, explicitly report: **Decision update; Metric/evidence update; CV/portfolio insight; Pitch/story update; Next verification step.** Record only facts supported by work actually completed. Never claim a file was saved or a result measured unless it was really saved or measured.

Use Git to preserve these records across sessions. If a new chat cannot access the repository or files, ask me to provide the latest records rather than assuming you remember them.

## 16. Your first response in this new chat

Do not jump straight into writing code.

Start by doing the following:

1. Review this entire proposal as a senior AI architect.
2. Identify its strongest aspects and biggest engineering risks.
3. Recommend the simplest feasible Android + Web architecture.
4. Evaluate the feasibility of obtaining and maintaining trustworthy Sri Lankan legal sources.
5. Present an initial MVP Product Requirements Document.
6. Propose a phased technical learning and development roadmap.
7. Identify the critical engineering decisions we must make before implementation.
8. Initialize the ADR index, metric ledger, portfolio evidence log, and pitch playbook without inventing achieved results.
9. Ask only the most important remaining questions, while suggesting sensible defaults.

Be analytical, constructive, practical, and willing to disagree with me when justified.

Our guiding principle is:

**Build a reliable, privacy-conscious and evidence-grounded legal awareness application while learning genuine production AI engineering practices.**