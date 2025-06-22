---
title: new page
excerpt: jm
deprecated: false
hidden: false
metadata:
  title: test
  description: testing
  image: https://files.readme.io/25ff87b-IMG_5887.jpeg
  robots: noindex
next:
  description: ''
---
If you are interested in building a highly custom enrollment funnel instead of using the [Enrollment Widget](doc:credit-as-a-service-signup-widget), we've got you covered!  Our Signup API (SAPI) allows you to build and control the flow of input fields.

> 🚧 
> 
> By using the SAPI, you will need to keep up to date with any improvements to the API and adjust accordingly on your end.  ConsumerDirect® will always give ample notice of upcoming changes.

> ❗️ Proxy Enrollments
> 
> To prevent fraud and protect the data of your customers, the system may block traffic identified to the same device or IP address. If you plan on doing proxy enrollments for your customers on the same device, please reach out to your Partner Support representative.

## Step-By-Step Guide

This tutorial walks you through the process of using the ConsumerDirect® Signup API (SAPI) to enroll a customer into the platform. Listed below is a step-by-step guide to get you production ready.

### 1. Request Access

In order to use the SAPI you will need an API client key for our stage environment to begin testing. If you don’t already have a client key, you can request one by emailing [partnerintegration@consumerdirect.com](mailto:partnerintegration@consumerdirect.com).

> 🚧 Client Key and Environment
> 
> Client keys are issued per environment.  Please make sure you are testing against the correct environment for the client key issued. 
> 
> Stage:         <https://stage-api.consumerdirect.io>  
> Production:    <https://api.consumerdirect.io>
> 
> White label partners, please reach out to your partner support representative to get the proper URLs for your environment.

### 2. Build The Funnel

Initially all development will be against our stage environment, please point your API calls to:  
<https://stage-api.consumerdirect.io>

Here are some examples of the typical flow of API calls for the SAPI depending on which type of subscription you're trying to support.

[block:parameters]
{
  "data": {
    "h-0": "Typical Flow For Paid Subscription",
    "h-1": "Typical Flow For Sponsored Subscription",
    "0-0": "1. [GET /start](ref:getstart-4)  \n2. [GET /campaign](ref:getcampaign-4)  \n3. [POST /validate/email](ref:postvalidateemail)  \n4. [POST /customer/create](ref:postcustomercreate-4)  \n5. [POST /customer/update/identity](ref:postcustomerupdateidentity-4)  \n6. [GET /id-verification](ref:getidverification-4)  \n7. [POST /id-verification](ref:postidverification-4)  \n8. [POST /validate/credit-card](ref:postvalidatecreditcardnumber)  \n9. [POST /customer/update/credit-card](ref:postcustomerupdatecreditcard-4)  \n10. [POST /complete](ref:postcomplete-4)",
    "0-1": "1. [GET /start](ref:getstart-4)  \n2. [GET /campaign](ref:getcampaign-4)  \n3. [POST /validate/email](ref:postvalidateemail)  \n4. [POST /validate/sponsor-code](ref:postvalidatesponsorcode)  \n5. [POST /customer/create](ref:postcustomercreate-4)  \n6. [POST /customer/update/identity](ref:postcustomerupdateidentity-4)  \n7. [GET /id-verification](ref:getidverification-4)  \n8. [POST /id-verification](ref:postidverification-4)  \n9. [POST /complete](ref:postcomplete-4)"
  },
  "cols": 2,
  "rows": 1,
  "align": [
    "left",
    "left"
  ]
}
[/block]

### 3. Test Your Funnel

You'll want to complete a customer enrollment to ensure ensure all your API calls are working properly and to verify the customers are being enrolled with the correct subscription information and PID tracking.

To confirm you have built everything correctly please ensure you are receiving a 200 HTTP responses for all completed endpoint calls.

Testing can be performed using one of the [Sandbox Testing Identities](doc:sandbox-testing).  

### 4. Compliance Review

Once you've tested your entire enrollment funnel, you will need to submit a video of the enrollment process from beginning to end for a compliance review.

For a list of requirements please go to [Compliance Review](doc:support-compliance-review) 

Please submit this video to [partnerintegration@consumerdirect.com](mailto:partnerintegration@consumerdirect.com).

If approved, you should receive your production client key within 24-48 hours.

### 5. Move to Production

There are 2 steps to move from the stage environment to production:

1. Change the stage environment URL to <https://api.consumerdirect.io>
2. Replace the stage client key with the production client key issued by ConsumerDirect® for all API calls

Once completed you can start sending real enrollments!

> ❗️ Production Testing
> 
> Testing with real customer information on production is not recommended as they will be treated as real enrollment which you and/or the customer will be charged for.  This can also cause unwanted data corruption.    
> 
> However, during your initial launch of your enrollment funnel using SAPI, we do recommend you test with the [Sandbox Testing Identities](doc:sandbox-testing) to ensure a successful cutover to production.
> 
> For additional support please reach out to your Partner Support Specialist.

## Enrollment API Flow

This section will walk you step-by-step through the entire enrollment process for both Paid and Sponsored subscriptions.

### 1. Initialize Enrollment

The first call you'll make is to our [Start Enrollment](ref:getstart-4) API endpoint.  You'll pass your `clientKey` and optional tracking parameters associated with the enrollment.  To support the dynamic display of offer details associated with the enrollment, you can optionally call the [Campaign Details](ref:getcampaign-4) endpoint.

> ❗️ PID Importance
> 
> The most important tracking parameter is PID which controls subscription options and pricing, if not passed the PID will be set to your default PID associated with your client key.

The Start Enrollment API call returns the `trackingToken` that is used in subsequent SAPI calls and an additional anonymous id for the user since they're not yet a customer on the platform.  Below is a sample response from the Start Enrollment API call.

```json Sample Start Enrollment Response
{
  "trackingToken": "53679db0-093e-11e5-b939-0800200c9a66",
  "anonymousId": "52c9756a-6e64-474c-8562-247dc515a643"
}
```

> ❗️ One Tracking Token Per Enrollment
> 
> The trackingToken will be used throughout the current enrollment **ONLY**.  It's important to understand that tracking tokens cannot be reused for future enrollments.  For each unique enrollment please call Start Enrollment again to be issued a new trackingToken.

### 2. Create Customer

Once you have a `trackingToken`, you can now call the [Create Customer](ref:postcustomercreate-4) API endpoint.  This endpoint requires a unique email address and password for the customer.  This will double as their login credentials on our platform (unless the customer changes it post enrollment).

Since the email address has to be unique, we advise calling the [Validate Email Address](ref:postvalidateemail) API endpoint to ensure the email address is valid and not tied to an existing account before proceeding.  For additional account security we offer email validation via a one time code emailed to the customer.  To use this feature please reference the [Send Email Verification Code](ref:getaccountverificationsend) and [Verify Account with Email Code](ref:postaccountverification) API endpoints.

```json Sample Create Customer Response
{
  "customerToken": "b3e9f907-8cc8-4e3a-849b-b16c6eb23682",
  "isFinancialObligationMet": false,
  "planType": "BASIC",
  "PID": "12345"
}
```

> 👍 Customer Token Created
> 
> Congratulations, you have now created the customer on the ConsumerDirect® platform, but they do not yet have an active subscription.  This means we will not bill for these customers.  You'll want to store the customerToken GUID for subsequent calls as this is their unique identifier in our system.  If you have your own identity store you'll want to connect our customerToken with your own customer ID.

> 📘 Sponsor Code Verification (optional feature)
> 
> If your enrollment funnel requires a customer to enter in your sponsor code, use the [Validate Sponsor Code](ref:getvalidatesponsorcode-4) API endpoint to confirm if the sponsored code provided valid before calling the create customer endpoint.

### 3. Set Identity

Every customer created in the platform must verify their identity in order to view their credit data. This requires submitting certain PII information with our [Set Identity (WITH SSN)](ref:postcustomerupdateidentity-4) API endpoint.   

SSN will be one of those mandatory data point which has a similar unique restriction as the email address.  To validate that the SSN does not already exist in our system for another account, we advise calling [Validate SSN](ref:postvalidatessn) prior to calling the [Set Identity (WITH SSN)](ref:postcustomerupdateidentity-4) API endpoint.  

If you find the SSN already exists, the enrollment cannot move forward and you should notify the customer that their SSN has already been registered with the platform.  

> 📘 identity.ssnPartial Behavior
> 
> When using our SSNs from our Sandbox Test Identities during the Validate SSN call, identity.ssnPartial will always fail and will require another call to check the full identity.ssn to succeed.

### 4. Verify Identity

Now that we have the customer's PII, we can begin the process of verifying their identity.  The entire process starts with a risk assessment of their digital transaction (Digital Verification).  Then it would proceed to the actual verification step which can be accomplished through Knowledge Based Answers (KBA) or One-Time Passcode (OTP).  Below are the details of each step.

#### Digital Verification (DV)

This is risk assessment service of a digital transaction providing device information used by consumers to access client’s web-site or portal. You will need to generate and pass along a digital Blackbox retrieved using the following TU javascript files.

1. include config.js and loader_only.js onto your signup page
   1. ```Text loader_only.js
      /*
       Copyright(c) 2018, iovation, inc. All rights reserved.
      */
      (function B(){function v(e,a){var b={},c;for(c=e.length-1;-1<c;c--)0<c?b[c]=function(){var d=c;return function(){return w(e[d],b[d+1],a)}}():w(e[c],b[c+1],a)}function w(e,n,k){var c=document.createElement("script"),f,g,l;l=A(a[k]&&a[k].staticVer&&a[k].staticVer+"/"||e[1]);e[0]=e[0].replace("##version##",l);f=e[0].split("?")[0].split("/");g=f[f.length-1].split(".")[0];u.test(e[1])&&l!==e[1]&&d("loader: Overriding configured version with staticVer.");c.setAttribute("src",e[0]);c&&c.addEventListener?
      c.addEventListener("error",function(){b[k+"_"+g+"_load_failure"]="true"}):c.attachEvent&&c.attachEvent("onerror",function(){b[k+"_"+g+"_load_failure"]="true"});n&&(c.onload=n);document.getElementsByTagName("head")[0].appendChild(c)}function d(e){if("function"===typeof a.trace_handler)try{a.trace_handler(e)}catch(b){}}function f(b,a){var d=null!==b&&void 0!==b;return!d||"1"!==b.toString()&&"true"!==b.toString().toLowerCase()?!d||"0"!==b.toString()&&"false"!==b.toString().toLowerCase()?"boolean"===
      typeof a?a:!1:!1:!0}function A(a){d("********** version before replace: "+a+" **********");d('localNamespace[ "url_dots_to_dashes" ]: '+b.url_dots_to_dashes);d("numericVersionPattern.test( output ): "+u.test(a));b.url_dots_to_dashes&&u.test(a)&&(a=a.replace(/\./g,"-"));d("version after replace: "+a);return a}var g=window,x=g.io_global_object_name||"IGLOO",a=g[x]=g[x]||{},b=a.loader=a.loader||{},y=[],z=[],u=/^[0-9]{1,3}(\.[0-9]{1,3}){2}\/$/;if(b.loaderMain)return d("loader: Loader script has already run, try reducing the number of places it's being included."),
      !1;b.loaderMain=B;b.loaderVer="5.2.2";(function(){var e=f(b.tp,!0),n=f(b.fp_static,!0),k=f(b.fp_dyn,!0),c=f(b.enable_legacy_compatibility),u=f(b.tp_split),v=b.tp_host&&b.tp_host.replace(/\/+$/,"")||"https://mpsnare.iesnare.com",l=b.fp_static_override_uri,m=void 0!==b.uri_hook?b.uri_hook+"/":"/iojs/",p=(b.version||"versionOrAliasIsRequired")+"/",w=b.subkey?g.encodeURIComponent(b.subkey)+"/":"",x=b.tp_resource||"wdp.js",q=b.tp_host?"&tp_host="+g.encodeURIComponent(b.tp_host):"",C=l?"&fp_static_uri="+
      g.encodeURIComponent(l):"",r,t,h;b.tp_host=v;r=f(a.enable_flash,!0);t=a.io&&a.io.enable_flash;h=a.fp&&a.fp.enable_flash;t=void 0!==t&&null!==t?f(t,!0):r;void 0!==h&&null!==h?h=f(h,!0):t=r;r=t?"&flash=true":"&flash=false";h=h?"&flash=true":"&flash=false";q="?loaderVer="+b.loaderVer+"&compat="+c+"&tp="+e+"&tp_split="+u+q+"&fp_static="+n+"&fp_dyn="+k+C;e||n||d("loader: Not currently configured to load fp_static or tp script(s).");a.fp&&a.fp.staticVer&&a.fp.staticVer+"/"!==p&&(p=A(a.fp.staticVer+"/"),
      d("loader: Configured version replaced with that from pre-loaded static script."));n||a.fp&&a.fp.staticMain?(m=(m+"##version##"+w).replace(/\/\//g,"/"),n&&(a.fp&&a.fp.staticMain?c&&!a.fp.preCompatMain&&d("loader: enable_legacy_compatibility on, but included static does not have the compat wrapper."):l?y.push([l,""]):y.push([m+"static_wdp.js"+q+h,p])),!k||a.fp&&a.fp.dynMain?a.fp&&a.fp.dynMain&&d("loader: First party dynamic script has already been loaded, disable fp_dyn or make sure you're not manually including the dynamic file separately."):
      y.push([m+"dyn_wdp.js"+q+h,p])):f(b.fp_dyn)&&d("loader: Invalid Config, first party dynamic script set to load without static.");e&&(a.io&&a.io.staticMain?d("loader: Third party script has already been loaded."):(m=v+"/##version##"+w,u?(z.push([m+"static_wdp.js"+q+r,p]),z.push([m+"dyn_wdp.js"+q+r,p]),b.tp_resource&&d("loader: Invalid Config: both tp_resource and tp_split set. Ignoring tp_resource.")):z.push([m+x+q+r,p])))})();v(y,"fp");v(z,"io")})();
      ```
   2. ```Text config.js
      /* Copyright(c) 2018, iovation, inc. All rights reserved. */
      window.io_global_object_name = "IGLOO"
      window.IGLOO = window.IGLOO || {
        "enable_flash" : false,
        "bbout_element_id" : "ioBlackBox",  // this can be changed to store in a different hidden field (or removed to use a different collection method)
        "loader" : {
          "subkey"  : "i07bAlexpwOuUoOhI2Z81QL0xKnFrxmVSbWC7Ar-XH4",
          "version" : "general5"
        }
      };
      ```
2. With both scripts loaded on the page, you can use the following method to get the blackbox data `window.IGLOO.getBlackbox()`
   1. example: `var blackbox_info = window.IGLOO.getBlackbox();`
   2. the returned blackbox data will look like the following: `{ blackbox: 'blackbox_value', finished: true }`
      1. **blackbox**: the updated value of the blackbox 
      2. **finished**: a Boolean indicating whether all the collection methods have completed.
3. There are two ways to pass the newly fetched Blackbox on to the [Get Questions](ref:getidverification-4) endpoint:
   1. Include an input in your form with the following property `id="ioBlackBox"` and `name="transunionDigitalVerificationBlackBox"` and the getBlackbox() method will automatically fill that input with the retrieved blackbox property
   2. You may choose a different input ID, that the getBlackbox() method automatically fills, by editing the config.js file, line 5:`"bbout_element_id" : "ioBlackBox",`
4. Save the response from the `window.IGLOO.getBlackbox()` method:
   1. `var blackbox_info = window.IGLOO.getBlackbox();`
   2. include the blackbox data with your call to [Get Questions](ref:getidverification-4) `blackbox_info.blackbox` in a field named `transunionDigitalVerificationBlackBox`

After you have retrieved and saved the blackbox data from DV, you'll want to [Get Questions](ref:getidverification-4) for the customer.  Based on the bureau's matching logic against their data sources, the customer may be eligible for OTP.  Please review the response from the [Get Questions](ref:getidverification-4) call to discern what to display next.

#### Verification Method: KBA

This process involves the customer answering a set of multiple choice questions based on their credit information.

```json Sample Get Questions Response
{
  "idVerificationCriteria": {
    "referenceNumber": 7271524018421871000,
    "question1": {
      "name": "AUTO_LOAN",
      "displayName": "When did you open your most recent auto loan?",
      "type": "MC",
      "choiceList": {
        "choice": [
          {
            "key": "1980",
            "display": "1980"
          },
          {
            "key": "1969",
            "display": "1969"
          },
          {
            "key": "2012",
            "display": "2012"
          },
          {
            "key": "2003",
            "display": "2003"
          },
          {
            "key": "!(1980^1969^2012^2003)",
            "display": "None of the above"
          }
        ]
      }
    }
  }
}
```

Based on your customer's selected answer to each question, you would then post the [Answer Questions](ref:postidverification-4).  To submit your customer's answers to the questions, we create an answers object that contains a key: numeric value property for each of the entries in the questions array. The key is the id of the question; the value is the id of the answer that we've selected. 

Due to the risk level of some customer's PII, they may be required to answer a second set of questions.  Please make sure your build anticipates for this scenario.

#### Verification Method: OTP

If the customer is eligible for OTP, the [Get Questions](ref:getidverification-4) call will return `idVerificationCriteria.question1.name == 'IDM_Choice` 

The formatting of the question/answer response for this step is unchanged from KBA, but you may want to change the text on the page to more accurately reflect the question.  Also, the POST object from this step is identical to the original Q&A flow from KBA.  

Although the customer is eligible for OTP, KBA can still be an option. Here are the 3 options in a OTP process:

1. Voice call to get PIN
2. Text message to get PIN
3. KBA 

The response from the POST will include `idVerificationCriteria.question1.name === 'IDM_PINVERIFY'` if either a voice call or text verification is submitted.

- This step requires an open text input for the user to input their pin, this value should be submitted in the POST data to /id-verification as `'idVerificationCriteria.userInput'`
- This text input has the following validation rules: Only numbers, minimum length of 4, maximum length of 8
- Each PIN can be tried only 3 times before it is considered a failed verification attempt
- Each PIN is only valid for 15 minutes before it is considered a failed verification attempt

In situations where the user does not receive a PIN or cannot retrieve a PIN, you may POST a value of `'RESET'` to the `'idVerificationCriteria.userInput'` field.  This request returns a ID verification failed error and clears the current verification attempt.  Once this is done, we highly recommend that you allow the user to confirm and resubmit their info to the [Set Identity (WITH SSN)](ref:postcustomerupdateidentity-4) API endpoint, or you can simply request a new verification session with the [Get Questions](ref:getidverification-4) API endpoint.  

> 📘 Sandbox Questions and Answers
> 
> Certain sandbox test identities will produce canned questions which means any answer will trigger a pass.  To properly test a failure scenario, make sure you are using test identities that provide unique questions and answers for passing.

> ❗️ Production Max Attempt
> 
> In production, the [Get Questions](ref:getidverification-4) call, regardless of OTP or KBA, is only allowed up to 3 times per SSN in a rolling 30 days.  Since this can be due to bad data provided by the customer during the Set Identity call, we recommend that the UI allows a customer to review their PII again before attempting to get a new set of questions.  Any changes to the PII would require another Set Identity call before moving onto the Verify Identity call.

### 5. Set Payment Method

For customers enrolling into a paid subscription, we currently support paying by credit card and accept Visa, Mastercard, Discover Card and American Express.  Accepting the credit card information is a two-step process: first will need to call the [Validate Credit Card](ref:postvalidatecreditcardnumber) API endpoint to ensure this is a valid card.  

```json Sample Validate Credit Card Response
{
  "creditCardToken": "5288fa42-3984-473a-826f-dab110acc6ea"
}
```

If successful you'll be returned a `creditCardToken` representing the customers stored credit card number on our platform.  You'll then call the [Set Credit Card](ref:postcustomerupdatecreditcard-4) API endpoint providing the returned `creditCardToken` as well as the rest of the customers billing information.

```json Sample Set Credit Card Response
{
  "planType": "PREMIUM",
  "isFinancialObligationMet": false
}
```

> 📘 Sponsored Codes
> 
> For sponsored subscriptions where you have collected a Sponsored Code during the [Customer Create](ref:postcustomercreate-4) call, you can bypass this step.  
> 
> However, we do recommend to still expose an ability to collect the sponsored code on the credit card page in case your customer missed entering it in on the first step of enrollment.  To do this, use the [Customer Update Sponsor Code](ref:postcustomerupdatesponsorcode-4) API endpoint to pass that information now.

> 🚧 Set Member Plan (optional)
> 
> If you are offering multiple plan options and you would like to give customers an option to change the plan they originally elected during the create identity call, you can [Set Member Plan](ref:postcustomerupdatememberplan-4) to present the options.

### 6. Complete Enrollment

Last but not least, let's [Complete](ref:postcomplete-4) this enrollment.  A successful response will return the membership plan type that the customer is now subscribed to as well as temporary password to allow the customer to log into their account from your confirmation page.  

This is a secure way way to get customers to login without you having to store their password for security purposes.  This temporary password is only valid for 15 minutes.  Please reference the login code to allow the customer to login. 

> 📘 Confirmation Page
> 
> When hosting the enrollment funnel on your website, be sure to include a confirmation page recapping the offer details of the member plan they just enrolled into.  To enhance engagement and lower the risk of refunds and chargebacks, allowing them to log in and use their membership immediately is advised.

> 🚧 Set Security Questions (optional feature)
> 
> After a customer has successfully completes their signup and logs into SmartCredit® they will be prompted to set up a security question.  If you would like to include the security question within your enrollment funnel you can do so with the [Security Question](ref:getsecurityquestions-1) call to get a list of valid security questions.

## Troubleshooting

Please see [Troubleshooting (SAPI)](doc:troubleshooting-sapi) for any issues.