---
title: Redact an Inquiry
excerpt: >-
  Permanently deletes personally identifiable information (PII) for an Inquiry
  and all associated Verifications, Reports, or other Persona resources. The
  response indicates a successful redaction of the Inquiry. Redaction of the
  Inquiry's associated child objects are done asynchronously and may take some
  time before all associated child objects are fully redacted. **This action
  cannot be undone**.


  This endpoint can be used to comply with privacy regulations such as GDPR /
  CCPA or to enforce data privacy.
api:
  file: persona-webhooks.json
  operationId: redact-an-inquiry
hidden: false
---