---
title: Import Email Address Lists
excerpt: >-
  Bulk import email address List Items by uploading a CSV file.


  Each row should be the details for a new List Item. The columns we allow are:
    - value
    - match_type (either 'email_address' or 'domain')

  A match_type of 'email_address' will need to match the entire email address of
  an individual, while a match_type of 'domain' will match on the email address
  domain of an individual (i.e. all email addresses with domain 'gmail.com').
api:
  file: persona-webhooks.json
  operationId: import-email-address-lists
hidden: false
---