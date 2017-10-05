---
title: "Azure 服務匯流排管理程式庫| Microsoft Docs"
description: "從 .NET 管理服務匯流排命名空間和傳訊實體。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 1db00dc1f91e8976b622030450445babbe547ad8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="62500-103">服務匯流排管理程式庫</span><span class="sxs-lookup"><span data-stu-id="62500-103">Service Bus management libraries</span></span>

<span data-ttu-id="62500-104">Azure 服務匯流排管理程式庫可以動態佈建服務匯流排命名空間和實體。</span><span class="sxs-lookup"><span data-stu-id="62500-104">The Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="62500-105">這適合複雜的部署和傳訊案例，且可讓您以程式設計方式決定要佈建的實體。</span><span class="sxs-lookup"><span data-stu-id="62500-105">This enables complex deployments and messaging scenarios, and makes it possible to programmatically determine what entities to provision.</span></span> <span data-ttu-id="62500-106">這些程式庫目前適用於 .NET。</span><span class="sxs-lookup"><span data-stu-id="62500-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="62500-107">支援的功能</span><span class="sxs-lookup"><span data-stu-id="62500-107">Supported functionality</span></span>

* <span data-ttu-id="62500-108">建立、更新、刪除命名空間</span><span class="sxs-lookup"><span data-stu-id="62500-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="62500-109">建立、更新、刪除佇列</span><span class="sxs-lookup"><span data-stu-id="62500-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="62500-110">建立、更新、刪除主題</span><span class="sxs-lookup"><span data-stu-id="62500-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="62500-111">建立、更新、刪除訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="62500-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62500-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="62500-112">Prerequisites</span></span>

<span data-ttu-id="62500-113">若要開始使用服務匯流排管理程式庫，您必須使用 Azure Active Directory (AAD) 服務來驗證。</span><span class="sxs-lookup"><span data-stu-id="62500-113">To get started using the Service Bus management libraries, you must authenticate with the Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="62500-114">AAD 會要求您以提供 Azure 資源存取權的服務主體來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="62500-114">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="62500-115">如需建立服務主體的詳細資訊，請參閱以下其中一篇文章：</span><span class="sxs-lookup"><span data-stu-id="62500-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="62500-116">使用 Azure 入口網站來建立可存取資源的 Active Directory 應用程式和服務主體</span><span class="sxs-lookup"><span data-stu-id="62500-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="62500-117">使用 Azure PowerShell 建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="62500-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="62500-118">使用 Azure CLI 建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="62500-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="62500-119">這些教學課程會提供您 `AppId` (用戶端識別碼)、`TenantId` 和 `ClientSecret` (驗證金鑰)，全部由管理程式庫用於驗證。</span><span class="sxs-lookup"><span data-stu-id="62500-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="62500-120">針對您想要執行的資源群組，您必須具備「擁有者」權限。</span><span class="sxs-lookup"><span data-stu-id="62500-120">You must have **Owner** permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="62500-121">程式設計模式</span><span class="sxs-lookup"><span data-stu-id="62500-121">Programming pattern</span></span>

<span data-ttu-id="62500-122">操控任何服務匯流排資源的模式，都會遵循共通的協定：</span><span class="sxs-lookup"><span data-stu-id="62500-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="62500-123">使用 **Microsoft.IdentityModel.Clients.ActiveDirectory** 程式庫從 Azure Active Directory 取得權杖。</span><span class="sxs-lookup"><span data-stu-id="62500-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="62500-124">建立 `ServiceBusManagementClient` 物件。</span><span class="sxs-lookup"><span data-stu-id="62500-124">Create the `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="62500-125">將 `CreateOrUpdate` 參數設定為您指定的值。</span><span class="sxs-lookup"><span data-stu-id="62500-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="62500-126">執行呼叫。</span><span class="sxs-lookup"><span data-stu-id="62500-126">Execute the call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="62500-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62500-127">Next steps</span></span>
* [<span data-ttu-id="62500-128">.NET 管理範例</span><span class="sxs-lookup"><span data-stu-id="62500-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="62500-129">Microsoft.Azure.Management.ServiceBus API 參考</span><span class="sxs-lookup"><span data-stu-id="62500-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
