# Personal & Project Pitch Playbook

Last updated: 2026-11-07. **Stage: concept and planning.** Scripts should be updated when there is a working prototype or real evaluation data.

## 30-second personal pitch — internship / networking

> I'm an aspiring AI engineer with experience in machine learning projects, including work connected to Sinhala language evaluation. I'm now planning an AI-powered legal awareness platform focused on Sri Lanka. Rather than making another general chatbot, I'm focusing on evidence-grounded retrieval, verifiable citations, privacy, and testing when the system should refuse to answer. I'm using the project to develop production AI engineering skills and to demonstrate the trade-offs behind the design.

## 45-second product pitch — general audience

> People often struggle to find clear, trustworthy explanations of their basic legal rights. I'm designing an Android and web-based legal awareness assistant initially focused on police interactions and fundamental rights in Sri Lanka. The goal is simple: give a plain-language summary, show the relevant official legal sources, explain the strength and limits of the evidence, and expand into detail when needed. It won't act as a lawyer or take legal action for anyone. The engineering challenge is ensuring the sources are valid, current, and accurately cited—especially when the system is uncertain.

## 90-second technical pitch — engineering audience

> This is an evidence-grounded legal information system, not an autonomous legal agent. I'm evaluating a shared API and structured, version-aware RAG pipeline for Android and Web. Legal documents would be ingested with provenance and effective-date metadata, retrieved using a tested combination of section-aware, keyword, and semantic search, and used to generate constrained answers. Backend checks would validate answer structure and source references; insufficient evidence would trigger a qualified response or abstention. I plan to evaluate retrieval recall, claim-level grounding, citation correctness, appropriate abstention, security tests, latency, and cost by language. Crucially, those are measured properties of the pipeline, not a made-up percentage that the legal answer is correct. I'm documenting choices in ADRs and will only claim outcomes after reproducible benchmarks and relevant legal-source review.

## 5-minute group presentation outline

1. **0:00–0:45 — Problem:** Why accessible legal information and source reliability matter. Avoid unsupported statistics.
2. **0:45–1:30 — Intended users and boundaries:** Citizens, police-related interactions, legal information rather than legal representation.
3. **1:30–2:30 — Product walkthrough:** Question → short answer → exact legal source → evidence status → detailed explanation. If no working app exists, label this as a proposed flow, not a live demo.
4. **2:30–3:40 — Engineering design:** Versioned corpus, RAG retrieval, deterministic validators, security, no autonomous action tools.
5. **3:40–4:30 — Evaluation evidence:** Show **only measured** citation, abstention, retrieval, latency and multilingual results; otherwise show the testing plan transparently.
6. **4:30–5:00 — Limitations, roadmap and ask:** Known legal/regulatory verification needs and next milestone.

## Demonstration script checklist

- [ ] State whether the demo is a mock-up, local prototype, beta, or deployed product.
- [ ] Use a known, reviewed example question; show source title, provision, and applicability/version.
- [ ] Show an unsupported or ambiguous question and the system's safe fallback.
- [ ] Explain that generated language can be wrong and how feedback/review works.
- [ ] Avoid entering private identifying details in a public demonstration.
- [ ] Do not imply attorney endorsement, government affiliation, or legal accuracy guarantees.

## Likely audience questions

**Why not just ask a general-purpose AI?** The product is being designed around specific verifiable sources, document versions, visible citations, and independent tests; these properties still need to be demonstrated in the prototype.

**How will you avoid hallucinations?** Not by prompting alone: retrieval, backend source checks, explicit evidence sufficiency and abstention, benchmark tests, and reviewer checks. Residual failures remain possible.

**How will you handle outdated laws?** Provenance, amendments, effective dates, source versioning, and a planned re-verification workflow; current legal status must be verified before launch.

**What if someone relies on a wrong answer?** Conservative scope, clear limits, safety-oriented product design, appropriate referral, reporting channels, and professional/legal review before release.

**What's your personal technical contribution?** Point to an implemented commit, an ADR, a benchmark and a lesson learned. While still planning, say which decisions and experiments you intend to own.

## After each milestone

Record one new before/after demo, one genuine technical lesson, one measurable result where available, one audience-appropriate pitch update, and one question you cannot yet answer.
