# Certification Readiness Checklist

Use this as an evidence tracker. Mark an item complete only when the corresponding evidence exists and is reviewed.

## KRA source documents
- [ ] Current official OSCU integration/API specification received.
- [ ] Version, issue date, and document provenance recorded.
- [ ] KRA onboarding and environment details received.
- [ ] Official certification test cases and expected results received.
- [ ] Any security, network, certificate, and data-retention requirements received.
- [ ] Specification gaps and written KRA clarifications recorded.

## Protocol conformance
- [ ] Base URLs and endpoint paths match the official version.
- [ ] HTTP methods, headers, content types, and character encoding match.
- [ ] Authentication, token lifecycle, certificates, and TLS match.
- [ ] Request/response schemas and required/conditional fields match.
- [ ] Enumerations, tax codes, units, currencies, and payment codes match.
- [ ] Date/time formats, timezone, precision, and rounding match.
- [ ] Error codes and validation messages handled as specified.
- [ ] Rate limits, payload limits, timeouts, and retry semantics match.

## Functional scenarios
- [ ] Seller/TIS setup and device initialization (if applicable).
- [ ] Valid invoice submission.
- [ ] All applicable tax categories and mixed-rate invoices.
- [ ] Exempt, zero-rated, and other special cases supported by the specification.
- [ ] Discounts, charges, rounding, and totals.
- [ ] Cash, card, bank, mobile money, and split payments where supported.
- [ ] Credit/debit note, cancellation, and correction flows where supported.
- [ ] Duplicate submission and idempotency/reconciliation.
- [ ] Offline/network interruption and recovery, if permitted.
- [ ] Receipt/control number/QR processing exactly as specified.

## Security and audit
- [ ] Secrets stored outside source control.
- [ ] TLS/certificate validation enabled.
- [ ] Logs redact credentials and sensitive payload fields.
- [ ] Role separation and least privilege reviewed.
- [ ] Audit trail is append-only and timestamped.
- [ ] Production environment protected by explicit approval/configuration.
- [ ] Dependency and vulnerability scans completed.

## Evidence pack
- [ ] Test environment and software build versions recorded.
- [ ] Automated test report exported.
- [ ] Request/response evidence sanitized and correlated.
- [ ] Negative and boundary test results included.
- [ ] Known limitations and deviations disclosed.
- [ ] KRA certification submission and outcome recorded.

**Important:** passing this internal checklist is not KRA certification. Only KRA can confirm acceptance/certification.
