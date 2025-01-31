---
title: Technical requirements
parent: Prerequisites
has_children: false
nav_order: 1
---

## Technical requirements

- Azure requirements
  - Access to the [Azure Portal](https://www.portal.azure.com)
  - Access to an active [Azure subscription](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)
  - **Contributor** role in a resource group to be able to deploy an Azure API Management instance

- During this lab, we will add existing APIs to our Azure API Management instance. The following APIs/websites should be available:
  - [Colors API](https://colors-api.azurewebsites.net/swagger/v1/swagger.json), in case this website is down you can deploy your own API using the following [instructions](../10-additional-topics/additional-topics-10-2-container-instance.md)
  - [Colors website](https://colors-web.azurewebsites.net), in case this website is down you can deploy your own website using the following [instructions](../10-additional-topics/additional-topics-10-2-container-instance.md)
  - [Star Wars API](https://swapi.dev/)
  - [Calculator API](http://calcapi.cloudapp.net/calcapi.json)
- For the DevOps part, you need to have access to a valid [Azure DevOps](https://dev.azure.com) organization.

**VIDEO**: There is a video example that walks through getting started which includes technical requirements that you can find [HERE](https://youtu.be/ZyPIu8oeEYI?si=F-6RXHiG3J85E3cM)