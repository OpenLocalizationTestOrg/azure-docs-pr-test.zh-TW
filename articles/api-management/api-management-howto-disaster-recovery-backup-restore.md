---
title: "在 Azure API 管理中使用備份和還原實作災害復原 | Microsoft Docs"
description: "了解如何在 Azure API 管理中使用備份和還原來執行災難復原。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>如何在 Azure API 管理中使用服務備份和還原實作災害復原
選擇透過 Azure API 管理來發佈及管理 API，您將能夠利用許多非 Azure API 管理使用者須另行設計、實作及管理的容錯和基礎結構功能。 Azure 平台可緩和絕大部分可能的失敗後果，且成本低廉。

若要從影響範圍涵蓋 API 管理服務託管所在之區域的可用性問題復原，您應該要做好準備能隨時在其他區域重新建構服務。 由於可用性目標和復原時間目標不盡相同，您也許會想要在一或多個區域預留備份服務，並嘗試與作用中的服務維持組態和內容同步。 服務備份和還原功能可提供實作災害復原策略時所不可或缺的建置組塊。

本指南說明如何驗證 Azure Resource Manager 的要求，以及如何備份和還原您的 API 管理服務執行個體。

> [!NOTE]
> 備份與還原嚴重損壞修復的 API 管理服務執行個體的程序，也可用於預備等案例，以複寫 API 管理服務執行個體。
>
> 請注意，每個備份在 30 天後到期。 如果您在過了 30 天的到期時間後嘗試還原備份，還原會失敗並傳回 `Cannot restore: backup expired` 訊息。
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>驗證 Azure 資源管理員要求
> [!IMPORTANT]
> 備份和還原的 REST API 會使用 Azure 資源管理員，並有不同的驗證機制的 REST API 來管理您的 API 管理實體。 本節中的步驟描述如何驗證 Azure 資源管理員的要求。 如需詳細資訊，請參閱 [驗證 Azure Resource Manager 要求](http://msdn.microsoft.com/library/azure/dn790557.aspx)。
>
>

所有您使用 Azure 資源管理員對資源所做的工作，必須透過 Azure Active Directory 使用以下步驟驗證。

* 新增應用程式到 Azure Active Directory 租用戶。
* 設定您所新增之應用程式的權限。
* 取得向 Azure 資源管理員驗證要求的權杖。

第一個步驟是建立 Azure Active Directory 應用程式。 使用含 API 管理服務執行個體的訂用帳戶登入 [Azure 傳統入口網站](http://manage.windowsazure.com/)，並瀏覽至預設 Azure Active Directory 的 [應用程式] 索引標籤。

> [!NOTE]
> 如果您的帳戶看不到 Azure Active Directory 預設目錄，請連絡 Azure 訂用帳戶的系統管理員，以授與您的帳戶必要權限。

![建立 Azure Active Directory 應用程式][api-management-add-aad-application]

按一下 [新增]，[新增我的組織正在開發的應用程式]，然後選擇 [原生用戶端應用程式]。 輸入描述性名稱，然後按一下下一步箭頭。 輸入 [重新導向 URI] 的預留位置 URL，例如 `http://resources`，因為它是必要的欄位，但稍後不會使用這個值。 按一下核取方塊以儲存應用程式。

儲存應用程式之後，按一下 [組態]，向下捲動至 [其他應用程式的權限] 區段，然後按一下 [新增應用程式]。

![新增權限][api-management-aad-permissions-add]

選取 [Windows Azure 服務管理 API]，然後按一下核取方塊以新增應用程式。

![新增權限][api-management-aad-permissions]

按一下新增的 [Windows Azure 服務管理 API] 應用程式旁邊的 [委派權限]，核取 [存取 Azure 服務管理 (預覽)]，然後按一下 [儲存]。

![新增權限][api-management-aad-delegated-permissions]

在叫用產生備份並將其還原的 API 之前，必須先取得權杖。 以下範例會使用 [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) NuGet 封裝來擷取權杖。

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

使用下列指示取代 `{tentand id}`、`{application id}` 和 `{redirect uri}`。

使用剛才建立的 Azure Active Directory 應用程式的租用戶識別碼取代 `{tenant id}` 。 您可以按一下 [檢視端點] 來存取識別碼。

![端點][api-management-aad-default-directory]

![端點][api-management-endpoint]

使用 Azure Active Directory 應用程式的 [設定] 索引標籤中的 [用戶端識別碼] 和 [重新導向 URI] 區段中的 URL，取代 `{application id}` 和 `{redirect uri}`。

![資源][api-management-aad-resources]

一旦指定了值，程式碼範例將傳回類似以下範例的權杖。

![權杖][api-management-arm-token]

呼叫下節描述的備份和還原作業之前，請先設定您 REST 呼叫的授權要求標頭。

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"> </a>備份 API 管理服務
若要備份 API 管理服務，請發出以下 HTTP 要求：

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

其中：

* `subscriptionId` -  訂用帳戶的識別碼，此訂用帳戶含有您嘗試備份的 API 管理服務
* `resourceGroupName` - 'Api-Default-{service-region}' 形式的字串；其中，`service-region` 可識別在其中裝載您嘗試備份之 API 管理服務的 Azure 區域 (例如 `North-Central-US`)
* `serviceName` - 要備份之 API 管理服務的名稱，該名稱是在服務建立時所指定
* `api-version` - 取代為 `2014-02-14`

在要求的本文中指定目標 Azure 儲存體帳戶名稱、存取金鑰、Blob 容器名稱和備份名稱：

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

將 `Content-Type` 要求標頭的值設定為 `application/json`。

備份作業的執行時間較長，因此可能需要幾分鐘的時間才能完成。  如果要求成功並已起始備份程序，則會收到含有 `Location` 標頭的 `202 Accepted` 回應狀態碼。  請向 `Location` 標頭中的 URL 發出 'GET' 要求，以查明作業的狀態。 當備份進行時，您會持續收到「202 已接受」狀態碼。 回應碼 `200 OK` 代表備份作業已成功完成。

進行備份的要求時，請注意下列條件約束。

* 在要求本文中指定的**容器****必須存在**。
* 備份進行時，請「避免嘗試任何服務管理作業」  ，如提升或降低 SKU、變更網域名稱等。
* 備份還原的**保證僅限建立後的 30 天內**。
* 備份**不包含**用來建立分析報告的**使用量資料**。 請使用 [Azure API 管理 REST API][Azure API Management REST API] 來定期擷取分析報告，以利妥善保存。
* 執行服務備份的頻率會影響您的復原點目標。 為了盡可能縮小，建議您實施定期備份，以及在針對 API 管理服務做出重要變更後執行隨選備份。
* 在備份作業進行時針對服務組態 (如 API、原則、開發人員入口網站外觀) 所做的**變更****可能不會納入備份中，因此可能會遺失**。

## <a name="step2"> </a>還原 API 管理服務
若要從先前建立的備份還原 API 管理服務，請發出以下 HTTP 要求：

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

其中：

* `subscriptionId` - 訂用帳戶的識別碼，此訂用帳戶含有您要還原備份的目標 API 管理服務
* `resourceGroupName` - 'Api-Default-{service-region}' 形式的字串；其中，`service-region` 可識別在其中裝載您要還原備份之目標 API 管理服務的 Azure 區域 (例如 `North-Central-US`)
* `serviceName` - 要還原之目標 API 管理服務的名稱，該名稱是在服務建立時所指定
* `api-version` - 取代為 `2014-02-14`

在要求的本文中指定備份檔案位置，即 Azure 儲存體帳戶名稱、存取金鑰、Blob 容器名稱和備份名稱：

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

將 `Content-Type` 要求標頭的值設定為 `application/json`。

還原作業的執行時間較長，因此可能需要 30 分鐘以上的時間才能完成。  如果要求成功並已起始還原程序，則會收到含有 `Location` 標頭的 `202 Accepted` 回應狀態碼。  請向 `Location` 標頭中的 URL 發出 'GET' 要求，以查明作業的狀態。 當還原進行時，您會持續收到「202 已接受」狀態碼。 回應碼 `200 OK` 代表還原作業已成功完成。

> [!IMPORTANT]
> 用於還原之目標服務的 **SKU****必須符合**即將還原之已備份服務的 SKU。
>
> 在還原作業進行時針對服務組態 (如 API、原則、開發人員入口網站外觀) 所做的**變更****可能會遭到覆寫**。
>
>

## <a name="next-steps"></a>後續步驟
請參閱下列 Microsoft 部落格中，兩個不同的備份/還原程序逐步解說。

* [複寫 Azure API 管理帳戶 (英文)](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * 感謝 Gisela 提供此文章。
* [Azure API 管理：備份和還原組態 (英文)](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * Stuart 詳細說明的方法與正式指南不同，但非常有意思。

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
