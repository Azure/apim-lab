---
title: Monitoring your API's
parent: Analytics and Monitoring
has_children: false
nav_order: 1
---

# Basic Monitoring with Azure Monitor

Analytics is available in the Azure management portal from the Analytics blade.

- Look at the dashboard and detailed :  Timeline , Geography , APIs , Operations , Products , Subscriptions , Users , Requests

![](../../assets/images/APIMAnalytics.png)

![](../../assets/images/APIMAnalytics2.png)


# How to integrate Azure API Management with Azure Application Insights

Azure API Management allows for easy integration with Azure Application Insights - an extensible service for web developers building and managing apps on multiple platforms. This guide walks through every step of such integration and describes strategies for reducing performance impact on your API Management service instance.

### Create an Azure Application Insights instance

Before you can use Azure Application Insights, you first need to create an instance of the service.

1. Open the **Azure portal** and navigate to **Application Insights**.  
    ![App Insights create](../../assets/images/apim-app-insights-instance-1.png)  
2. Click **+ Add**.  
    ![App Insights create](../../assets/images/apim-app-insights-instance-2.png)  
3. Fill the form. Select **General** as the **Application Type**.
4. Click **Create**.

### Create a connection between Azure Application Insights and Azure API Management service instance

1. Navigate to your **Azure API Management service instance** in the **Azure portal**.
2. Select **Application Insights** from the menu on the left.
3. Click **+ Add**.  
    ![App Insights logger](../../assets/images/apim-app-insights-logger-1.png)  
4. Select the previously created **Application Insights** instance and provide a short description.
5. Click **Create**.
6. You have just created an Azure Application Insights logger with an instrumentation key. It should now appear in the list.  
    ![App Insights logger](../../assets/images/apim-app-insights-logger-2.png)  

> Behind the scene, a [Logger](https://docs.microsoft.com/rest/api/apimanagement/2019-12-01/logger/createorupdate) entity is created in your API Management instance, containing the Instrumentation Key of the Application Insights instance.

### Enable Application Insights logging for your API

1. Navigate to your **Azure API Management service instance** in the **Azure portal**.
2. Select **APIs** from the menu on the left.
3. Click on your API, for example **Color API**.
4. Go to the **Settings** tab from the top bar.
5. Scroll down to the **Diagnostics Logs** section.  
    ![App Insights logger](../../assets/images/apim-app-insights-api-1.png)  
6. Check the **Enable** box.
7. Select your attached logger in the **Destination** dropdown.
8. Input **100** as **Sampling (%)** and tick the **Always log errors** checkbox.
9. Click **Save**.

> Overriding the default value **0** in the **First bytes of body** field may significantly decrease the performance of your APIs.

> Behind the scene, a [Diagnostic](https://docs.microsoft.com/rest/api/apimanagement/2019-12-01/diagnostic/createorupdate) entity named 'applicationinsights' is created at the API level.



### What data is added to Azure Application Insights

Azure Application Insights receives:

+ *Request* telemetry item, for every incoming request (*frontend request*, *frontend response*),
+ *Dependency* telemetry item, for every request forwarded to a backend service (*backend request*, *backend response*),
+ *Exception* telemetry item, for every failed request.

A failed request is a request, which:

+ failed because of a closed client connection, or
+ triggered an *on-error* section of the API policies, or
+ has a response HTTP status code matching 4xx or 5xx.

If you go into your Application Insights instance, after few seconds, you should be able to see logs and metrics

![App Insights logger](../../assets/images/apim-app-insights-api-2.png)  

### Performance implications and log sampling

> Logging all events may have serious performance implications, depending on incoming requests rate.

Based on internal load tests, enabling this feature caused a 40%-50% reduction in throughput when request rate exceeded 1,000 requests per second. Azure Application Insights is designed to use statistical analysis for assessing application performances. It is not intended to be an audit system and is not suited for logging each individual request for high-volume APIs.

You can manipulate the number of requests being logged by adjusting the **Sampling** setting (see the steps above). Value 100% means all requests are logged, while 0% reflects no logging at all. **Sampling** helps to reduce the volume of telemetry, effectively preventing from significant performance degradation, while still carrying the benefits of logging.

Skipping logging of headers and body of requests and responses will also have positive impact on alleviating performance issues.

