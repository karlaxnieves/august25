---
title: Redact an Account
excerpt: >-
  Permanently deletes personally identifiable information (PII) for an Account
  and all associated Inquiries, Verifications and Reports. The response
  indicates a successful redaction of the Account. Redaction of the Account's
  associated child objects are done asynchronously and may take  some time
  before all associated child objects are fully redacted. **This action cannot
  be undone**.


  This endpoint can be used to comply with privacy regulations such as GDPR /
  CCPA or to enforce data privacy.


  Note: An account is still updatable after redaction. If you want to delete
  data continuously, please reach out to us to help you setup a retention
  policy.
api:
  file: persona-webhooks.json
  operationId: redact-an-account
hidden: false
---