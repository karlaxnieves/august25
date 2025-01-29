---
title: New Doc
excerpt: this is a test
deprecated: false
hidden: false
metadata:
  robots: index
---
Playing around with Mermaid diagrams :stuck_out_tongue:

This is a test string to be edited!

<HTMLBlock>{`
<html>
  <head>
    <style>
      html[data-theme="dark"] h1 {
        color: red !important;
      }
      
      [data-color--mode="dark"] .messageLine0 {
        color: red !important;
      }
    </style>
  </head>
  <body>
    <h1>This is a test heading</h1>
    <p>If dark mode is enabled, this heading should turn red.</p>
  </body>
</html>
`}</HTMLBlock>

<br />

# TEST

```mermaid
%%{
  init: {
    'theme': 'base',
    'themeVariables': {
      'background': '#FFFFFF' /* Default for light mode */
    }
  }
}%%

sequenceDiagram
    participant Alice
    participant Bob
    Alice->>Bob: Hello Bob, how are you?
    Bob-->>Alice: I'm good, thanks!
```

<br />

Another sentence appear!

```mermaid
sequenceDiagram
    participant EMP App
    participant EMP BE 
    participant Drive API
    participant Stripe

    note over EMP App:1. Retrieve publishable API key, unless it's cached
    EMP App->>EMP BE:GET - publishable API key
    activate EMP App
    activate EMP BE
    note over EMP BE:Retrieve publishable API key, unless it's cached
    EMP BE->>Drive API:GET - publishable API key
    activate Drive API
    Drive API-->>EMP BE:return
    deactivate Drive API
    EMP BE-->>EMP App:return
    deactivate EMP BE
    deactivate EMP App

    note over EMP App:2. Create SetupIntent to be used with Stripe client-side library

    EMP App->>EMP BE: GET - Create SetupIntent
    activate EMP App
    activate EMP BE
    EMP BE->>Drive API:GET - Create SetupIntent
    activate Drive API
    Drive API-->>EMP BE:return
    deactivate Drive API
    EMP BE-->>EMP App:return
    deactivate EMP BE
    deactivate EMP App

    note over EMP App:3.Use Stripe client-side library with the publishable API key

    activate EMP App
    EMP App->>EMP App: Collect PaymentMethod details
    EMP App->>Stripe: Confirm SetupIntent with client-secret
    activate Stripe
    Stripe-->>EMP App:return
    deactivate EMP App
    deactivate Stripe

    note over EMP App:4.Associate the newly created PaymentMethod.id to an user

    EMP App->>EMP BE: POST - Create credit-card on user with PaymentMethod id
    activate EMP App
    activate EMP BE
    EMP BE->>Drive API:GET - Create credit-card on user with PaymentMethod id
    activate Drive API
    Drive API-->>EMP BE:return
    deactivate Drive API
    EMP BE-->>EMP App:return
    deactivate EMP BE
    deactivate EMP App
```

<HTMLBlock>{`
<style>
@media (prefers-color-scheme: dark) {
 [data-color-mode="system"] .messageLine0 .mermaid {
   color: white; 
 }
}
  
[data-color-mode="dark"] .messageLine0 .mermaid {
  color: white; 
}
</style>
`}</HTMLBlock>