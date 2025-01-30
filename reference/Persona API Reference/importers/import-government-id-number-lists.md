---
title: Import Government ID Number Lists
excerpt: >-
  Bulk import government ID number List Items by uploading a CSV file.


  Each row should be the details for a new List Item. The columns we allow are:
    - id_number
    - id_class

  Common values for id_class include `pp` for passport and `dl` for driver
  license. Please contact us or reach out to
  [support@withpersona.com](mailto:support@withpersona.com) if you need help
  getting id_class values.
api:
  file: persona-webhooks.json
  operationId: import-government-id-number-lists
hidden: false
---