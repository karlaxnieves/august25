---
title: Update an Inquiry
excerpt: >-
  Updates an existing Inquiry.


  Note that if you use webhooks, updates to inquiries that are not in progress
  can result in data getting out of sync. For example, updating a completed
  Inquiry will not cause your Inquiry completed webhook to retrigger.


  Inquiries represent a snapshot of data collected from an individual, so we
  generally do not recommend updating an Inquiry's data after the Inquiry has
  been finalized.
api:
  file: persona-webhooks.json
  operationId: update-an-inquiry
hidden: false
---