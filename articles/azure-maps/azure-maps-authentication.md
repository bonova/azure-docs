---
title: Authentication with Azure Maps | Microsoft Docs
description: Authentication for using Azure Maps services.
author: walsehgal
ms.author: v-musehg
ms.date: 10/24/2019
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: philmea
ms.custom: mvc
---

# Authentication with Azure Maps

Azure Maps supports two ways to authenticate requests: Shared Key and Azure Active Directory (Azure AD). This article explains these authentication methods to help guide your implementation.

## Shared Key authentication

Shared Key authentication  passes keys generated by an Azure Maps account with each request to Azure Maps.  Two keys are generated when your Azure Maps account is created. For each request to Azure Maps services, the subscription key needs to be added as a parameter to the URL.

> [!Tip]
> We recommend regenerating your keys regularly. You're provided with two keys so that you can maintain connections with one key while regenerating the other. When you regenerate your keys, you need to update any applications that access the account to use the new keys.

For information about viewing your keys, see [View authentication details](https://aka.ms/amauthdetails).

## Authentication with Azure Active Directory (Preview)

Azure Maps now offers [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis) integration for the authentication of requests for Azure Maps services. Azure AD provides identity-based authentication, including [role-based access control (RBAC)](https://docs.microsoft.com/azure/role-based-access-control/overview), to grant user-level, group-level and application-level access to Azure Maps resources. The sections that follow can help you understand the concepts and components of Azure Maps integration with Azure AD.

## Authentication with OAuth access tokens

Azure Maps accepts **OAuth 2.0** access tokens for Azure AD tenants associated with an Azure subscription that contains an Azure Maps account. Azure Maps accepts tokens for:

* Azure AD users. 
* Partner applications that use permissions delegated by users.
* Managed identities for Azure resources.

Azure Maps generates a *unique identifier (client ID)* for each Azure Maps account. When you combine this client ID with additional parameters, you can request tokens from Azure AD by specifying the values in the following table depending upon your Azure Environment.

| Azure Environment   | Azure AD token endpoint |
| --------------------|-------------------------|
| Azure Public        | https://login.microsoftonline.com |
| Azure Government    | https://login.microsoftonline.us |


For more information about how to configure Azure AD and request tokens for Azure Maps, see [Manage authentication in Azure Maps](https://docs.microsoft.com/azure/azure-maps/how-to-manage-authentication).

For general information about requesting tokens from Azure AD, see [What is authentication?](https://docs.microsoft.com/azure/active-directory/develop/authentication-scenarios).

## Request Azure Map resources with OAuth tokens

After a token is received from Azure AD, a request can be sent to Azure Maps with the following two required request headers set:

| Request header    |    Value    |
|:------------------|:------------|
| x-ms-client-id    | 30d7cc….9f55|
| Authorization     | Bearer eyJ0e….HNIVN |

> [!Note]
> `x-ms-client-id` is the Azure Maps account-based GUID that appears on the Azure Maps authentication page.

Here's an example of an Azure Maps route request that uses an OAuth token:

```
GET /route/directions/json?api-version=1.0&query=52.50931,13.42936:52.50274,13.43872 
Host: atlas.microsoft.com 
x-ms-client-id: 30d7cc….9f55 
Authorization: Bearer eyJ0e….HNIVN 
```

For information about viewing your client ID, see [View authentication details](https://aka.ms/amauthdetails).

## Control access with RBAC

Azure AD lets you control access to secured resources by using RBAC. After you create your Azure Maps account and register your Azure Maps Azure AD application within your Azure AD tenant, you can set up RBAC for a user, group, application, or Azure resource on the Azure Maps account portal page.

Azure Maps supports read access control for individual Azure AD users, groups, applications, and Azure services via managed identities for Azure resources.

![Azure Maps Data Reader (Preview)](./media/azure-maps-authentication/concept.png)

For information about viewing your RBAC settings, see [How to configure RBAC for Azure Maps](https://aka.ms/amrbac).

## Managed identities for Azure resources and Azure Maps

[Managed identities for Azure resources](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) provide Azure services (Azure App Service, Azure Functions, Azure Virtual Machines, and so on) with an automatically managed identity that can be authorized for access to Azure Maps services.  

## Next steps

* To learn more about authenticating an application with Azure AD and Azure Maps, see [Manage authentication in Azure Maps](https://docs.microsoft.com/azure/azure-maps/how-to-manage-authentication).

* To learn more about authenticating the Azure Maps Map Control and Azure AD, see [Use the Azure Maps Map Control](https://aka.ms/amaadmc).
