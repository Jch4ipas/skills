---
name: security
description: Security agent
license: MIT
compatibility: opencode
---

# Security

## Do:

- Apply least privilege to all agent tools and permissions.
- Validate and sanitize all external inputs (user messages, documents, API responses).
- Implement human-in-the-loop for high-risk actions.
- Isolate memory and context between users/sessions.
- Monitor agent behavior and set up anomaly detection.
- Use structured outputs with schema validation.
- Sign and verify inter-agent communications.
- Classify data and apply appropriate protections.

## Don't:

- Give agents unrestricted tool access or wildcard permissions.
- Trust content from external sources (websites, emails, documents).
- Allow agents to execute arbitrary code without sandboxing.
- Store sensitive data in agent memory without encryption/redaction.
- Let agents make high-impact decisions without human oversight.
- Ignore cost controls (unbounded loops can cause DoW).
- Pass unsanitized data between agents in multi-agent systems.
- Log sensitive data (PII, credentials) in plain text.
