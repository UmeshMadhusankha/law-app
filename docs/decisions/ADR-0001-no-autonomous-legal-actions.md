# ADR-0001 — Exclude autonomous legal actions

- **Date:** 2026-11-07
- **Status:** Accepted (from the user-defined product constraint)
- **Decision type:** Product and system boundary
- **Source:** Initial project proposal, §§3 and 11

## Context

A legal awareness assistant can help citizens understand options without acting as their legal representative. Delegated legal actions create disproportionate error, authorization, and liability risks.

## Decision

The app will not autonomously submit complaints, contact authorities, file legal documents, send legal notices, or otherwise act legally on behalf of a user. It will remain an informational tool; appropriate legal referrals may be presented.

## Alternatives considered

- Informational system only — selected, narrow and easier to verify.
- Agentic legal workflows — excluded as a permanent product constraint.

## Consequences

- No external action tools with legal effect in the AI pipeline.
- Any user-facing legal resource link must be presented as a user-directed option, not an action the agent takes.
- Security and acceptance tests should verify the assistant cannot trigger autonomous legal actions.

## Revisit trigger

None within this product's stated scope. A materially different product would require a separate decision process.
