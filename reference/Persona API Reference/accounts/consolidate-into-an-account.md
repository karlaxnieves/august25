---
title: Consolidate Accounts
excerpt: >-
  Consolidates several source Accounts' information into one target Account. Any
  Persona resource associated with the source Account will be transferred over
  to the destination Account. However, the Account's attributes will **not** be
  transferred. After consolidation, you can update the destination Account's
  attributes using the [Account update
  endpoint](https://docs.withpersona.com/reference/update-an-account).


  This endpoint can be used to clean up duplicate Accounts.


  Note: A source account can only be consolidated once. Afterwards, the source
  account will be archived.
api:
  file: persona-webhooks.json
  operationId: consolidate-into-an-account
hidden: false
---