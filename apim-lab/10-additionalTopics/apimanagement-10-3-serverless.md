---
title: API Proxy to Serverless
parent: Additional Topics
has_children: false
nav_order: 3
---

## Additional Topics - API Proxy to Serverless

Azure Serverless (Functions and Logic Apps) can be configured to benefit from the advantages of API Management.

### Azure Functions

- Create a simple function that is Triggered by an HTTP Request

Example:

![](../../assets/images/APIMFunctionExample.png)

```c#
    //string[] strColors = { "blue", "lightblue", "darkblue" };
    string[] strColors = { "green", "lightgreen", "darkgreen" };

    Random r = new Random();
    int rInt = r.Next(strColors.Length);

    return  (ActionResult)new OkObjectResult(strColors[rInt]);
```

Lets add the function to API Management.   In the API blade select [+Add API] and the [Function App] tile

![](../../assets/images/APIMFunctionAddAPI.png)

- Select the [Browse] button to get a list of Functions in the subscription

![](../../assets/images/APIMFunctionAddBrowse.png)

- Select the Function App and then the Function

![](../../assets/images/APIMFunctionSelect.png)

![](../../assets/images/APIMFunctionSelect2.png)

- Amend the Names / Descriptions, URL suffix and select the Products

![](../../assets/images/APIMFunctionCreate.png)

- As previously add CORS policy

- Validate the function works - either from the Azure management portal or the developer portal

![](../../assets/images/APIMFunctionTest1.png)

![](../../assets/images/APIMFunctionTest2.png)

### Azure Logic Apps

- Create a simple logic app that is Triggered by an HTTP Request

Example:

![](../../assets/images/APIMLogicAppExample1.png)

![](../../assets/images/APIMLogicAppExample2.png)

Use the following sample message to generate the schema of the Request body payload.  By specifying the schema, the individual fields (in this case `msg`) can be extracted and referred to in the subsequent logic

```json
{
  "msg": "text"
}
```

Lets add the function to API Managament. In the API blade select [+Add API] and the [Logic App] tile

![](../../assets/images/APIMLogicAppAddAPI.png)

- Select the [Browse] button to get a list of Logic Apps in the subscription

![](../../assets/images/APIMLogicAppAddBrowse.png)

- Select the Logic App

![](../../assets/images/APILogicAppSelect%20.png)

- Amend the Names / Descriptions, URL suffix  and select the Products

![](../../assets/images/APIMLogicAppCreate.png)

 As previously add CORS policy

- Validate the Logic App works - either from the Azure management portal or the developer poral

![](../../assets/images/APIMLogicAppTest1.png)

![](../../assets/images/APIMLogicAppTest2.png)

- Check the Logic App audit

![](../../assets/images/APIMLogicAppTest3.png)

- Check the email was sent

![](../../assets/images/APIMLogicAppTest4.png)


