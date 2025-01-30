---
title: Retrieve an Inquiry
excerpt: >-
  Retrieves the details of an existing Inquiry.


  In the [Embedded Flow](https://docs.withpersona.com/docs/embedded-flow), the
  `inquiry-id` is the first parameter of the onStart callback. In the [Hosted
  Flow](https://docs.withpersona.com/docs/hosted-flow), the `inquiry-id` is a
  query parameter in the onComplete callback.


  Template information will be found in `data.relationships.inquiry-template` if
  the inquiry is a Dynamic Flow inquiry, and in `data.relationships.template` if
  the inquiry is a Legacy 2.0 inquiry. For more information, see [Dynamic Flow
  vs. Legacy
  Templates](https://docs.withpersona.com/docs/inquiry-templates#dynamic-flow-vs-legacy-templates).
api:
  file: persona-webhooks.json
  operationId: retrieve-an-inquiry
hidden: false
---