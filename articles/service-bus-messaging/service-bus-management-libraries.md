---
title: "aaaAzure 服務匯流排管理程式庫 |Microsoft 文件"
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
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="d278a-103">服務匯流排管理程式庫</span><span class="sxs-lookup"><span data-stu-id="d278a-103">Service Bus management libraries</span></span>

<span data-ttu-id="d278a-104">服務匯流排命名空間和實體時，動態地佈建 hello Azure 服務匯流排管理程式庫。</span><span class="sxs-lookup"><span data-stu-id="d278a-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="d278a-105">這可讓複雜的部署和傳訊的案例，並可讓您 tooprogrammatically 決定哪些實體 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="d278a-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="d278a-106">這些程式庫目前適用於 .NET。</span><span class="sxs-lookup"><span data-stu-id="d278a-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="d278a-107">支援的功能</span><span class="sxs-lookup"><span data-stu-id="d278a-107">Supported functionality</span></span>

* <span data-ttu-id="d278a-108">建立、更新、刪除命名空間</span><span class="sxs-lookup"><span data-stu-id="d278a-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="d278a-109">建立、更新、刪除佇列</span><span class="sxs-lookup"><span data-stu-id="d278a-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="d278a-110">建立、更新、刪除主題</span><span class="sxs-lookup"><span data-stu-id="d278a-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="d278a-111">建立、更新、刪除訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d278a-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d278a-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="d278a-112">Prerequisites</span></span>

<span data-ttu-id="d278a-113">tooget 開始使用 hello 服務匯流排管理程式庫，您必須向 hello Azure Active Directory (AAD) 服務。</span><span class="sxs-lookup"><span data-stu-id="d278a-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="d278a-114">AAD 會要求您驗證做為服務主體時，可提供存取 tooyour Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d278a-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="d278a-115">如需建立服務主體的詳細資訊，請參閱以下其中一篇文章：</span><span class="sxs-lookup"><span data-stu-id="d278a-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="d278a-116">使用 hello Azure 入口網站 toocreate Active Directory 應用程式和服務主體可存取資源</span><span class="sxs-lookup"><span data-stu-id="d278a-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="d278a-117">使用 Azure PowerShell toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="d278a-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="d278a-118">使用 Azure CLI toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="d278a-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="d278a-119">這些教學課程提供您與`AppId`（用戶端識別碼）、 `TenantId`，和`ClientSecret`（驗證金鑰），全部都是用於驗證由 hello 管理程式庫。</span><span class="sxs-lookup"><span data-stu-id="d278a-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="d278a-120">您必須擁有**擁有者**想 toorun hello 資源群組的權限。</span><span class="sxs-lookup"><span data-stu-id="d278a-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="d278a-121">程式設計模式</span><span class="sxs-lookup"><span data-stu-id="d278a-121">Programming pattern</span></span>

<span data-ttu-id="d278a-122">hello 模式 toomanipulate 任何服務匯流排資源會遵循一般的通訊協定：</span><span class="sxs-lookup"><span data-stu-id="d278a-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="d278a-123">取得語彙基元，從 Azure Active Directory 使用 hello **Microsoft.IdentityModel.Clients.ActiveDirectory**程式庫。</span><span class="sxs-lookup"><span data-stu-id="d278a-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="d278a-124">建立 hello`ServiceBusManagementClient`物件。</span><span class="sxs-lookup"><span data-stu-id="d278a-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="d278a-125">設定 hello `CreateOrUpdate` tooyour 參數指定值。</span><span class="sxs-lookup"><span data-stu-id="d278a-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="d278a-126">Execute 呼叫 hello。</span><span class="sxs-lookup"><span data-stu-id="d278a-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="d278a-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d278a-127">Next steps</span></span>
* [<span data-ttu-id="d278a-128">.NET 管理範例</span><span class="sxs-lookup"><span data-stu-id="d278a-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="d278a-129">Microsoft.Azure.Management.ServiceBus API 參考</span><span class="sxs-lookup"><span data-stu-id="d278a-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
