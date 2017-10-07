---
title: "aaaAzure 事件中心管理程式庫 |Microsoft 文件"
description: "從 .NET 管理事件中樞命名空間和實體"
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="5e19f-103">事件中樞管理程式庫</span><span class="sxs-lookup"><span data-stu-id="5e19f-103">Event Hubs management libraries</span></span>

<span data-ttu-id="5e19f-104">事件中樞命名空間和實體時，動態地佈建 hello 事件中心管理程式庫。</span><span class="sxs-lookup"><span data-stu-id="5e19f-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="5e19f-105">這可讓複雜的部署和傳訊的案例，好讓您以程式設計的方式可以判斷哪些實體 tooprovision。</span><span class="sxs-lookup"><span data-stu-id="5e19f-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="5e19f-106">這些程式庫目前適用於 .NET。</span><span class="sxs-lookup"><span data-stu-id="5e19f-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="5e19f-107">支援的功能</span><span class="sxs-lookup"><span data-stu-id="5e19f-107">Supported functionality</span></span>

* <span data-ttu-id="5e19f-108">建立、更新、刪除命名空間</span><span class="sxs-lookup"><span data-stu-id="5e19f-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="5e19f-109">建立、更新、刪除事件中樞</span><span class="sxs-lookup"><span data-stu-id="5e19f-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="5e19f-110">建立、更新、刪除取用者群組</span><span class="sxs-lookup"><span data-stu-id="5e19f-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e19f-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="5e19f-111">Prerequisites</span></span>

<span data-ttu-id="5e19f-112">tooget 開始使用 hello 事件中心管理程式庫，您必須驗證與 Azure Active Directory (AAD)。</span><span class="sxs-lookup"><span data-stu-id="5e19f-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="5e19f-113">AAD 會要求您驗證做為服務主體時，可提供存取 tooyour Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="5e19f-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="5e19f-114">如需建立服務主體的詳細資訊，請參閱以下其中一篇文章：</span><span class="sxs-lookup"><span data-stu-id="5e19f-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="5e19f-115">使用 hello Azure 入口網站 toocreate Active Directory 應用程式和服務主體可存取資源</span><span class="sxs-lookup"><span data-stu-id="5e19f-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="5e19f-116">使用 Azure PowerShell toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="5e19f-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="5e19f-117">使用 Azure CLI toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="5e19f-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="5e19f-118">這些教學課程提供您與`AppId`（用戶端識別碼）、 `TenantId`，和`ClientSecret`（驗證金鑰），全部都是用於驗證由 hello 管理程式庫。</span><span class="sxs-lookup"><span data-stu-id="5e19f-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="5e19f-119">您必須擁有**擁有者**想 toorun hello 資源群組的權限。</span><span class="sxs-lookup"><span data-stu-id="5e19f-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="5e19f-120">程式設計模式</span><span class="sxs-lookup"><span data-stu-id="5e19f-120">Programming pattern</span></span>

<span data-ttu-id="5e19f-121">hello 模式 toomanipulate 任何事件中樞資源會遵循一般的通訊協定：</span><span class="sxs-lookup"><span data-stu-id="5e19f-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="5e19f-122">取得權杖從 AAD 使用 hello`Microsoft.IdentityModel.Clients.ActiveDirectory`程式庫。</span><span class="sxs-lookup"><span data-stu-id="5e19f-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="5e19f-123">建立 hello`EventHubManagementClient`物件。</span><span class="sxs-lookup"><span data-stu-id="5e19f-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="5e19f-124">設定 hello `CreateOrUpdate` tooyour 參數指定值。</span><span class="sxs-lookup"><span data-stu-id="5e19f-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="5e19f-125">Execute 呼叫 hello。</span><span class="sxs-lookup"><span data-stu-id="5e19f-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="5e19f-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e19f-126">Next steps</span></span>
* [<span data-ttu-id="5e19f-127">.NET 管理範例</span><span class="sxs-lookup"><span data-stu-id="5e19f-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="5e19f-128">Microsoft.Azure.Management.EventHub 參考</span><span class="sxs-lookup"><span data-stu-id="5e19f-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
