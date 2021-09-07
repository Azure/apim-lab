---
title: CORS policy
parent: Policy Expressions
has_children: false
nav_order: 1
---


### Cross-origin resource sharing (CORS)

The cors policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.

<https://docs.microsoft.com/en-us/azure/api-management/api-management-cross-domain-policies#CORS>

If you go to the global scope located in ´All APIs´you should find something like this:

- On the left Menu, click on `APIs`
- Then select the `All APIs` option
- Then go to the `Inbound Processing` area
- Click on the `cors` policy

![](../../assets/images/apim-policy-cors-all-apis.png)  

```xml
<!-- Inbound -->
    <cors allow-credentials="true">
            <allowed-origins>
                <origin>https://famc-apim.developer.azure-api.net</origin>
                <origin>https://markcolorweb.azurewebsites.net</origin>
            </allowed-origins>
            <allowed-methods preflight-result-max-age="300">
                <method>*</method>
            </allowed-methods>
            <allowed-headers>
                <header>*</header>
            </allowed-headers>
            <expose-headers>
                <header>*</header>
            </expose-headers>
        </cors>
```

