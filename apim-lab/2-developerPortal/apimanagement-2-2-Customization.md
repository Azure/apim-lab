---
title: Customizing Developer Portal
parent: Developer Portal
has_children: false
nav_order: 2
---

 
## Customizing the Developer Portal

### Site Configuration

The Developer Portal is based on a fork of the [Paperbits Web framework](https://paperbits.io/) and is enriched with API Management-specific features. The fork resides at <https://github.com/Azure/api-management-developer-portal>.

It is possible to self-host and manage your own Developer Portal outside of an API Management instance. This is an advanced option, which allows you to edit the portal's codebase and extend the provided core functionality. This is documented at <https://github.com/Azure/api-management-developer-portal/wiki> and <https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-developer-portal>.

Before you make your portal available to visitors, you should personalize the automatically-generated content. Recommended changes include the layouts, styles, and the content of the home page. This is documented at <https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-developer-portal-customize>.

A video on customization is available at <https://www.youtube.com/watch?v=5mMtUSmfUlw>.

![](../../assets/images/APIMDevConfig.png)

![](../../assets/images/APIDevConfig2.png)

![](../../assets/images/APIMDevStyles.png)

### Email Configuration

The templates for the email notifications are managed from the Azure Management Portal, directly on the blade's resource menu.

Look at the available notifications and notifications templates which are customizable.

![](../../assets/images/APIMNotifications.png)

![](../../assets/images/APIMNotificationTemplates.png)

![](../../assets/images/APIMNotificationEdit.png)