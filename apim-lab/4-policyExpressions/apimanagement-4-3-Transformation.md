---
title: Transformation policies
parent: Policy Expressions
has_children: false
nav_order: 3
---


## Colors API 

### Transformation - replace string

The find-and-replace policy finds a request or response substring and replaces it with a different substring.

- Open the Colors API, then open the ApiRandomColor operation 'Code View'
- Add the outbound policy to change from "blue" to "yellow"
- Invoke the API using the Starter product key and examine the response
- Invoke the API using the Unlimited product key and examine the response


```xml
<find-and-replace from="blue" to="yellow" />

```

With Starter key and Unlimited key:

![](../../assets/images/replacepolicy.png)

## Star Wars API

### Transformation - conditional

Another C# example to manipulate the response body, depending on the product - with this expression a subscriber of the Starter product will only get back a subset of the information.  Other products will get the full information.

- Open the Star Wars API, then open the GetPeopleById operation 'Code View'
- Add the outbound policy to conditionally change the response body
- Invoke the API using the Starter product key and examine the response
- Invoke the API using the Unlimited product key and examine the response

Not the inbound header is set to ensure that the Response Body is not encoded as that causes the JSON parsing to fail.

```xml
<!-- Inbound -->
        <set-header name="Accept-Encoding" exists-action="override">
            <value>deflate</value>
        </set-header>
<!-- Outbound -->
<choose>
    <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">
        <set-body>@{
                var response = context.Response.Body.As<JObject>();
                foreach (var key in new [] {"hair_color", "skin_color", "eye_color", "gender"}) {
                    response.Property(key).Remove();
                }
                return response.ToString();
            }
        </set-body>
    </when>
</choose>

```

With Starter key:

![](../../assets/images/APIMResponseCondStarter.png)

With Unlimited key:

![](../../assets/images/APIMResponseCondUnlimited.png)

## Calculator API 

### Transformation - XML to JSON

A frequent requirement is to transform content, especially with legacy APIs

Remember the Calc API that returned XML
- Open the Calculator API 'Code View'
- Add the outbound policy to transform the response's body to JSON
- Invoke the API and examine the response - note that its now JSON

```xml
<!-- Outbound -->
<xml-to-json kind="direct" apply="always" consider-accept-header="false" />
```

![](../../assets/images/APIMResponseXMLtoJSON.png)


### Delete response headers

A frequent requirement is to remove headers - example those that might leak potential security information

- Open the Calculator API 'Code View'
- Add the outbound policy to delete the response headers
- Invoke the API and examine the response

```xml
<!-- Outbound -->
<set-header name="x-aspnet-version" exists-action="delete" />
<set-header name="x-powered-by" exists-action="delete" />
```

Before:
![](../../assets/images/APIMResponseDeleteHeaders.png)

After policy applied:
![](../../assets/images/APIMResponseDeleteHeaders2.png)

### Amend what's passed to the backend

Policy expressions can include C# code. Can access a number of .NET Framework types and their members .NET Framework type.  A variable named `context` is implicitly available and its members provide information pertinent to the API request.

More info <https://docs.microsoft.com/en-us/azure/api-management/api-management-policy-expressions>

- Open the Calculator API 'Code View'
- Add the inbound policy to amend the query string and header
- Invoke the API - use the Trace function to examine what was passed to the backend

```xml
<!-- Inbound -->
<set-query-parameter name="x-product-name" exists-action="override">
    <value>@(context.Product.Name)</value>
</set-query-parameter>
<set-header name="x-request-context-data" exists-action="override">
    <value>@(context.User.Id)</value>
    <value>@(context.Deployment.Region)</value>
</set-header>
```

Note - this trace below was from the Developer portal.  I got errors when testing from the Azure Management portal, as the [User Id] is unable to be evaluated.

![](../../assets/images/APIMTraceAmendBackend.png)