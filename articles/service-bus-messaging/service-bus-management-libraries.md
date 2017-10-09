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
# <a name="service-bus-management-libraries"></a>服務匯流排管理程式庫

服務匯流排命名空間和實體時，動態地佈建 hello Azure 服務匯流排管理程式庫。 這可讓複雜的部署和傳訊的案例，並可讓您 tooprogrammatically 決定哪些實體 tooprovision。 這些程式庫目前適用於 .NET。

## <a name="supported-functionality"></a>支援的功能

* 建立、更新、刪除命名空間
* 建立、更新、刪除佇列
* 建立、更新、刪除主題
* 建立、更新、刪除訂用帳戶

## <a name="prerequisites"></a>必要條件

tooget 開始使用 hello 服務匯流排管理程式庫，您必須向 hello Azure Active Directory (AAD) 服務。 AAD 會要求您驗證做為服務主體時，可提供存取 tooyour Azure 資源。 如需建立服務主體的詳細資訊，請參閱以下其中一篇文章：  

* [使用 hello Azure 入口網站 toocreate Active Directory 應用程式和服務主體可存取資源](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [使用 Azure CLI toocreate 服務主體 tooaccess 資源](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

這些教學課程提供您與`AppId`（用戶端識別碼）、 `TenantId`，和`ClientSecret`（驗證金鑰），全部都是用於驗證由 hello 管理程式庫。 您必須擁有**擁有者**想 toorun hello 資源群組的權限。

## <a name="programming-pattern"></a>程式設計模式

hello 模式 toomanipulate 任何服務匯流排資源會遵循一般的通訊協定：

1. 取得語彙基元，從 Azure Active Directory 使用 hello **Microsoft.IdentityModel.Clients.ActiveDirectory**程式庫。
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. 建立 hello`ServiceBusManagementClient`物件。

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. 設定 hello `CreateOrUpdate` tooyour 參數指定值。

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Execute 呼叫 hello。

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>後續步驟
* [.NET 管理範例](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Microsoft.Azure.Management.ServiceBus API 參考](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
