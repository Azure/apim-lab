---
title: Verification
parent: Azure Apim Creation
has_children: false
nav_order: 2
---

## Verifying the API Management instance

Once the APIM instance has been created, please verify that it functions correctly by following these steps:

1) Navigate to the newly-created APIM instance in the Azure Portal.  
2) Select the **APIs** blade, then select the *Echo API*.   
3) Press the **Test** tab, then select the **GET Retrieve resource** operation.  
4) Press **Send** to issue a simple request.  

  ![APIM Echo API Test Send](../../assets/images/apim-echo-api-test-1.png)

5) Observe the `200` Success response.  

  ![APIM Echo API Test Success](../../assets/images/apim-echo-api-test-2.png)

At this time you have successfully verified that APIM is set up!

### Verification Failure (and Path to Success)

You may have noticed the *Request URL* and may be tempted to put it in your browser, issue a CURL statement, etc. If you do, you may see a `401` error and wonder what's happening.

![APIM Echo API Test 401](../../assets/images/apim-echo-api-test-3.png)

The reason for this the unauthorized access status code is that the *Echo API* requires a subscription key to be set. Whereas tests originating in APIM account for this automatically, external callers cannot (and, naturally, should not).

Back in APIM, switch to the **Settings** tab and uncheck **Subscription required** and press **Save** at the bottom of the page.

> Subscriptions are important and useful, but in this case, we just want to quickly verify the APIM instance is working as intended.

![APIM Echo API Disable Required Subscription](../../assets/images/apim-echo-api-test-4.png)

Accessing the link in your browser should now show you no error message. In fact, in order to verify the 200, it's easiest to open your Developer Tools (F12), navigate to the **Network** tab, and look at **All** requests to see the 200.

![APIM Echo API Browser Success](../../assets/images/apim-echo-api-test-5.png)

Alternatively, you can issue a verbose (`-v`) CURL command against the **Echo API** and observe the `200` Success:
`curl -v https://<your apim instance>.azure-api.net/echo/resource?param1=sample`

![APIM Echo API Curl Success](../../assets/images/apim-echo-api-test-6.png)