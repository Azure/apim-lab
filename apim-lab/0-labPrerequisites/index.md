---
title: Prerequisites
has_children: false
nav_order: 1
---


## Check that you have everything ready to do the workshop

Please check that you have the following requirements to complete the hands-on lab:

- Azure requirements
  - Access to the [Azure Portal](https://www.portal.azure.com)
  - Access to an active [Azure subscription](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade)
  - Contributor role in a resource group to be able to deploy an API Management instance
- During part 3 of this lab, we will add existing APIs to our API Management instance. The following APIs/websites should be available:
  - [Colors API](https://colors-api.azurewebsites.net/swagger/v1/swagger.json), in case this website is down you can deploy your own API using the following [instructions](../10-additionalTopics/apimanagement-10-2-containerinstance.md)
  - [Colors website](https://colors-web.azurewebsites.net), in case this website is down you can deploy your own website using the following [instructions](../10-additionalTopics/apimanagement-10-2-containerinstance.md)
  - [Star Wars API](https://swapi.dev/)
  - [Calculator API](http://calcapi.cloudapp.net/calcapi.json)
- For part 8 you need to have access to a valid [Azure DevOps](https://dev.azure.com) organization.

**An API Management instance can take some time to provision.** Please follow the steps outlined in APIM Creation prior to the workshop.
