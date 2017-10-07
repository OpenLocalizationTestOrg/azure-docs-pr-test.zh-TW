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
# <a name="event-hubs-management-libraries"></a>事件中樞管理程式庫

事件中樞命名空間和實體時，動態地佈建 hello 事件中心管理程式庫。 這可讓複雜的部署和傳訊的案例，好讓您以程式設計的方式可以判斷哪些實體 tooprovision。 這些程式庫目前適用於 .NET。

## <a name="supported-functionality"></a>支援的功能

* 建立、更新、刪除命名空間
* 建立、更新、刪除事件中樞
* 建立、更新、刪除取用者群組

## <a name="prerequisites"></a>必要條件

tooget 開始使用 hello 事件中心管理程式庫，您必須驗證與 Azure Active Directory (AAD)。 AAD 會要求您驗證做為服務主體時，可提供存取 tooyour Azure 資源。 如需建立服務主體的詳細資訊，請參閱以下其中一篇文章：  

* [使用 hello Azure 入口網站 toocreate Active Directory 應用程式和服務主體可存取資源](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [使用 Azure CLI toocreate 服務主體 tooaccess 資源](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

這些教學課程提供您與`AppId`（用戶端識別碼）、 `TenantId`，和`ClientSecret`（驗證金鑰），全部都是用於驗證由 hello 管理程式庫。 您必須擁有**擁有者**想 toorun hello 資源群組的權限。

## <a name="programming-pattern"></a>程式設計模式

hello 模式 toomanipulate 任何事件中樞資源會遵循一般的通訊協定：

1. 取得權杖從 AAD 使用 hello`Microsoft.IdentityModel.Clients.ActiveDirectory`程式庫。
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. 建立 hello`EventHubManagementClient`物件。
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. 設定 hello `CreateOrUpdate` tooyour 參數指定值。
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Execute 呼叫 hello。
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>後續步驟
* [.NET 管理範例](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Microsoft.Azure.Management.EventHub 參考](/dotnet/api/Microsoft.Azure.Management.EventHub) 
