# Security Design

- Keep credentials, tokens, client secrets, private keys, and certificates out of Git.
- Supply secrets through deployment secret management or protected environment variables.
- Never disable TLS certificate verification.
- Use separate credentials and configuration for test and production.
- Redact authorization headers, cookies, keys, taxpayer identifiers, and invoice details from logs unless KRA explicitly requires retained evidence in a protected store.
- Restrict evidence access and define retention according to KRA and applicable Kenyan legal requirements.
- Use append-only audit events for invoice creation, submission, response, retry, reconciliation, and correction.
- Apply least-privilege access to runtime identities and CI.
- Pin and scan dependencies; generate an SBOM for release candidates.
- Rotate credentials/certificates according to KRA policy and document emergency revocation.
- Do not expose debug endpoints or mock KRA services in production.
