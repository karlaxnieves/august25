---
title: Resume an Inquiry
excerpt: >-
  Creates a session token that is returned as `meta.session-token`. If the
  inquiry's status is `expired`, changes the status to `pending`. The
  `session-token` must be included when loading the inquiry flow if the
  inquiry's status is `pending`.

  This endpoint will error if the inquiry is redacted.

  This endpoint first tries to reuse any existing valid unused
  [sessions](https://docs.withpersona.com/docs/inquiry-sessions). If none exist,
  a new session is created.

  For more information, see [Resuming
  Inquiries](https://docs.withpersona.com/docs/inquiries-resuming-inquiries).
api:
  file: persona-webhooks.json
  operationId: resume-an-inquiry
hidden: false
---