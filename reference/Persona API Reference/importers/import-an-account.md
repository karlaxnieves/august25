---
title: Import Accounts
excerpt: |-
  Bulk import accounts by uploading a CSV file.

  Each row should be the details for a new account. The columns we allow are:
    - reference_id
    - name_first
    - name_middle
    - name_last
    - birthdate
    - social_security_number
    - tags
api:
  file: persona-webhooks.json
  operationId: import-an-account
hidden: false
---