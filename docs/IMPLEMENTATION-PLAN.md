# KRA eTIMS OSCU Connector — Implementation Plan

## Status and source-of-truth rule

This is a certification-oriented engineering scaffold, not a claim of KRA certification or production approval. Implementations MUST be checked against the current KRA-issued OSCU integration specification, interface control document, onboarding pack, and test scenarios supplied to the integrator. Do not infer endpoint paths, field names, enum values, cryptographic rules, or response codes from unofficial examples.

**Blocking input:** add the current official KRA OSCU API documentation and any KRA-issued certification test pack to `docs/kra-source/`. Record document title, version, issue date, source/contact, and SHA-256. Until then, protocol-specific adapters remain deliberately unimplemented.

## Intended architecture

- **Transport adapter:** HTTPS client using the exact base URLs, paths, headers, TLS/mTLS, timeouts, and retry rules prescribed by KRA.
- **Authentication provider:** isolates token/key/certificate acquisition and renewal; secrets only from environment/secret manager.
- **Protocol DTOs:** versioned request/response schemas copied from the official specification and validated at runtime.
- **Invoice domain:** typed invoice, seller/buyer, line, tax, payment, totals, and references; decimal arithmetic only.
- **Submission orchestrator:** validates, serializes, submits, records correlation identifiers, and handles documented status transitions.
- **Persistence/audit:** append-only submission attempts and response evidence; idempotency keys; no silent mutation of submitted invoices.
- **Diagnostics:** structured redacted logs, health checks, metrics, and correlation IDs.
- **Certification harness:** deterministic fixtures, mock KRA server, contract tests, negative tests, and evidence export.

## Safety and compliance invariants

1. No production submission without explicit environment selection and valid credentials.
2. Never log passwords, tokens, private keys, certificate contents, or full sensitive taxpayer payloads.
3. Do not retry non-idempotent operations unless KRA documents safe retry semantics or the request can be reconciled first.
4. Persist request fingerprint, attempt timestamp, transport outcome, sanitized response, and KRA reference where permitted.
5. Preserve original invoice data and every submission attempt for audit; corrections follow KRA-prescribed credit/debit note or cancellation workflow.
6. Use decimal-safe monetary arithmetic and validate line, tax-category, and invoice totals before submission.
7. Treat KRA responses as authoritative; do not fabricate control codes, receipt numbers, QR payloads, or fiscalization outcomes.
8. Keep sandbox/test and production configuration strictly separated.

## Delivery phases

### Phase 0 — Specification capture
- Add official KRA documents and version register.
- Extract exact endpoint catalogue, auth flow, schemas, enumerations, limits, error codes, signing/encryption requirements, and timeout/retry rules.
- Resolve ambiguities with KRA before coding protocol details.

### Phase 1 — Domain and contract model
- Implement invoice domain types and decimal calculations.
- Generate or hand-author DTOs from the official schema.
- Add schema validation and golden request/response fixtures.

### Phase 2 — Transport and security
- Implement auth and TLS exactly as specified.
- Add certificate/key loading, rotation, redaction, timeout, and safe retry policy.
- Add test/sandbox configuration and production guardrails.

### Phase 3 — Workflows
- Implement registration/device initialization only if included in the supplied OSCU specification.
- Implement invoice submission, status/reconciliation, receipt/QR handling, and correction workflows only as documented.
- Implement duplicate detection and idempotent reconciliation.

### Phase 4 — Certification readiness
- Map every KRA test case to automated tests and evidence.
- Run positive, negative, boundary, concurrency, recovery, and security tests.
- Produce versioned evidence bundle and unresolved-issues register.
- Submit through KRA's designated certification process; certification can only be granted by KRA.

## Required acceptance gates

- 100% of documented mandatory KRA scenarios pass in the designated test environment.
- Contract tests use the exact current KRA schema/version.
- No secrets or prohibited taxpayer data in logs.
- Duplicate/retry/recovery tests prove no duplicate fiscalization.
- All totals reconcile exactly under the documented rounding rules.
- Production mode is disabled until credentials, endpoint, and approval are configured.
