# ADR-0003 — Shared backend for Android and Web

- **Date:** 2026-11-07
- **Status:** Proposed — NOT adopted yet
- **Decision type:** Platform architecture

## Context

The product requires Android and browser interfaces while preserving consistent AI policy, rate limits, source verification, and secret management.

## Options to evaluate

1. Flutter for Android and Web + one FastAPI backend.
2. Flutter for Android + conventional web frontend + one FastAPI backend.
3. Other cross-platform frontend, with a single backend.

## Proposed design

One server-side API mediates ingestion, retrieval, LLM calls, authentication if needed, abuse controls, logging, and citations. No privileged LLM credentials live in browser or Android clients.

## Evidence required before acceptance

Test developer productivity, desktop accessibility/usability, web performance, deployment friction, maintainability, and solo-developer cost. Compare against one realistic frontend alternative.

## Revisit trigger

Inadequate browser experience, accessibility, performance, or frontend release complexity.
