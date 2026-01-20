---
title: API Proxy to Serverless
parent: Additional Topics
has_children: false
nav_order: 3
---

## API Proxy to Serverless

Azure Serverless (Functions and Logic Apps) can be configured to benefit from the advantages of Azure API Management.

### Azure Functions

In this section, we will create a simple HTTP Triggered Azure Function which runs on the [Flex Consumption](https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-plan) plan. Flex Consumption is a Linux-based Azure Functions hosting plan that uses a serverless billing model and provides private networking, flexible memory size allocation and fast scale-out capabilities.

- Create a simple function that is Triggered by an HTTP Request. Navigate to the **Azure Functions** portal and click **Create**.

![](../../assets/images/azf-create.png)

- In the **Create Azure Function** screen, select **Flex Consumption**.

![](../../assets/images/azf-flex-consumption.png)

- On the **Basics** properties screen, fill in the details as follows:

- **Resource Group (create new)**: `af-dev-we-apimazf-[your-initials]-01`
- **Function App Name**: `APIMAZF`
- **Region**: `West Europe`
- **Runtime stack**: `3.12`
- **Instance size**: `512MB`

![](../../assets/images/azf-flex-basics.png)

- On the **Authentication** section, select **Managed Identities** for all of the options as shown below.

![](../../assets/images/azf-flex-auth.png)

- Wait for the Azure Function to be created and deployed and then go to resource. You should see your new Azure Function App. It's empty at the moment, we'll need to add a function handler.

![](../../assets/images/azf-created-props.png)

- You can add a function handler to your Azure Function in a variety of ways, through the command line, VS Code and so on. We'll keep it simple and use the CLI. Open a **Cloud Shell** (not Powershell) on this page. Run the following commands in this cloudshell. These commands will populate the directory with a simple Python function handler that is triggered by HTTP:
  - `func init --worker-runtime python`
  - `func new --name HttpExample --template "HTTP trigger" --authlevel "function"`

- Finally, run the following command to publish your local function to your Azure Function App:

  - `func azure functionapp publish APIMAZF`

![](../../assets/images/azf-cloudshell-created.png)

- The function will take a while to deploy to your function app but once complete, you should see a green success message in the cloud shell terminal and a new **HTTPExample** function listed in the **Functions** section of the **Overview** blade.

![](../../assets/images/azf-published.png)

- If you click on the **HTTPExample** Function, this will take you to the **Code + Test** console where you can inspect the **function_app.py** Python Code. As you can see below, the template HTTP Trigger code is very simple. It defines a single route which prints a successful message and a personalised message if a **name** is passed as query parameter. Let's test that next with an API.

![](../../assets/images/azf-python-code.png)

- Let's now create an API based on this Azure Function App and HTTPTrigger. Add the function to Azure API Management. In the API blade select [+Add API] and the [Function App] tile

![](../../assets/images/apim-azure-function-add-api.png)

- Select the **Browse** button.

![](../../assets/images/apim-azure-function-add-browse.png)

- Select the Function App we created earlier and then **Select**.

![](../../assets/images/apim-azure-function-select-1.png)

- Select the HTTPExample Function Handler from the app and then **Select**.

![](../../assets/images/apim-azure-function-select-2.png)

- Accept the defaults and click **Create**


- Validate the function works in the APIM portal. Select the **APIMAZF** API, select **Test**, then select the **HTTExample** post route. Add a **Query Parameter** called **Name** with the value of your choice. Click **Send** to see the response. You can optionally test again but this time remove the **name** query parameter to see a different response.

![](../../assets/images/apim-azure-function-test-1.png)

![](../../assets/images/apim-azure-function-test-2.png)

Congratulations, you have successfully created an API from an Azure Function!

### Azure Logic Apps

- Create a simple logic app that is Triggered by an HTTP Request

Example:

![](../../assets/images/apim-logic-app-example-1.png)

![](../../assets/images/apim-logic-app-example-2.png)

Use the following sample message to generate the schema of the Request body payload.  By specifying the schema, the individual fields (in this case `msg`) can be extracted and referred to in the subsequent logic

```json
{
  "msg": "text"
}
```

Lets add the function to API Managament. In the API blade select [+Add API] and the [Logic App] tile

![](../../assets/images/apim-logic-app-add-api.png)

- Select the [Browse] button to get a list of Logic Apps in the subscription

![](../../assets/images/apim-logic-app-add-browse.png)

- Select the Logic App

![](../../assets/images/apim-logic-app-select.png)

- Amend the Names / Descriptions, URL suffix  and select the Products

![](../../assets/images/apim-logic-app-create.png)

 As previously add CORS policy

- Validate the Logic App works - either from the Azure management portal or the developer poral

![](../../assets/images/apim-logic-app-test-1.png)

![](../../assets/images/apim-logic-app-test-2.png)

- Check the Logic App audit

![](../../assets/images/apim-logic-app-test-3.png)

- Check the email was sent

![](../../assets/images/apim-logic-app-test-4.png)


