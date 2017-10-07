---
title: "aaaImplement 災害復原使用備份與還原在 Azure API 管理 |Microsoft 文件"
description: "深入了解如何 toouse 備份和還原 tooperform 嚴重損壞修復，在 Azure API 管理。"
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
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>如何 tooimplement 災害復原使用服務備份和還原在 Azure API 管理
藉由選擇 toopublish 和管理您的應用程式開發介面透過 Azure API 管理，您就可以運用許多錯誤容錯和基礎結構功能，您原本必須另外 toodesign 實作和管理。 hello Azure 平台可降低在 hello 成本可能發生失敗的較大的分數。

從可用性問題在影響其中是您的 API 管理服務的 hello 區域 toorecover 裝載您應該準備好 tooreconstitute 隨時都是您在不同的區域中的服務。 視您的可用性目標和復原時間目標，您可能會想 tooreserve 中一或多個區域的備份服務並再試一次 toomaintain 其設定及內容與 hello active service 不同步。 hello 服務備份和還原功能提供 hello 所需的建置組塊，實作嚴重損壞修復策略。

本指南也說明如何 tooauthenticate Azure 資源管理員要求，以及如何 toobackup 和還原您的 API 管理服務執行個體。

> [!NOTE]
> 備份與還原 API 管理服務執行個體的災害復原的 hello 程序也可用來複寫案例，例如臨時的 API 管理服務執行個體。
>
> 請注意，每個備份在 30 天後到期。 如果您嘗試 toorestore 備份 hello 30 天的逾期期限過期之後，hello 還原會失敗並`Cannot restore: backup expired`訊息。
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>驗證 Azure 資源管理員要求
> [!IMPORTANT]
> hello 備份和還原的 REST API 使用 Azure 資源管理員並具有不同的驗證機制比 hello REST Api 來管理您 API 管理的實體。 本節中的 hello 步驟說明如何 tooauthenticate Azure 資源管理員的要求。 如需詳細資訊，請參閱 [驗證 Azure Resource Manager 要求](http://msdn.microsoft.com/library/azure/dn790557.aspx)。
>
>

所有 hello 工作使用 hello Azure 資源管理員的資源上執行之必須使用 Azure Active Directory 使用下列步驟的 hello 進行驗證。

* 新增應用程式 toohello Azure Active Directory 租用戶。
* 設定您加入的 hello 應用程式的權限。
* 取得 hello 權杖來驗證要求 tooAzure 資源管理員。

hello 第一個步驟是 toocreate Azure Active Directory 應用程式。 登入 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)使用 hello 訂用帳戶包含您的 API 管理服務執行個體，並瀏覽 toohello**應用程式**預設 Azure Active Directory 索引標籤。

> [!NOTE]
> 如果 hello Azure Active Directory 預設目錄是不可見的 tooyour 帳戶，hello Azure 訂用帳戶 toogrant hello hello 連絡系統管理員所需的權限 tooyour 帳戶。

![建立 Azure Active Directory 應用程式][api-management-add-aad-application]

按一下 [新增]，[新增我的組織正在開發的應用程式]，然後選擇 [原生用戶端應用程式]。 輸入描述性名稱，然後按一下 hello 下一步箭頭。 輸入預留位置 URL，例如`http://resources`hello**重新導向 URI**，就如同它是必要的欄位，但不是會更新版本使用 hello 值。 按一下 [hello] 核取方塊 toosave hello 應用程式。

Hello 應用程式儲存之後，按一下**設定**，捲動 toohello**權限 tooother 應用程式**區段，然後按一下 **新增應用程式**。

![新增權限][api-management-aad-permissions-add]

選取**Windows** **Azure 服務管理 API**按一下 hello 核取方塊 tooadd hello 應用程式。

![新增權限][api-management-aad-permissions]

按一下**委派的權限**旁邊新加入的 hello **Windows** **Azure 服務管理 API**應用程式中，核取方塊 hello**存取 Azure服務管理 （預覽）**，然後按一下**儲存**。

![新增權限][api-management-aad-delegated-permissions]

先前 tooinvoking hello 產生的 Api hello 備份和還原它，就需要 tooget 語彙基元。 hello 下列範例會使用 hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget 封裝 tooretrieve hello 語彙基元。

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
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

取代`{tentand id}`， `{application id}`，和`{redirect uri}`使用下列指示的 hello。

取代`{tenant id}`hello 的 hello 您剛才建立的 Azure Active Directory 應用程式的租用戶識別碼。 您可以按一下來存取 hello 識別碼**檢視端點**。

![端點][api-management-aad-default-directory]

![端點][api-management-endpoint]

取代`{application id}`和`{redirect uri}`使用 hello**用戶端識別碼**hello URL 從 hello 和**重新導向 Uri**來自 Azure Active Directory 應用程式的區段**設定**  索引標籤。

![資源][api-management-aad-resources]

一旦指定 hello 值，hello 程式碼範例將返回語彙基元的類似 toohello，下列範例。

![權杖][api-management-arm-token]

呼叫 hello 備份和還原 hello 下列各節中所述的作業之前，設定 REST 呼叫的 hello 授權要求標頭。

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"> </a>備份 API 管理服務
下列 HTTP 要求的 API 管理服務問題 hello 向上 tooback:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

其中：

* `subscriptionId`-hello 訂用帳戶包含您正嘗試 toobackup hello API 管理服務識別碼
* `resourceGroupName`-hello 'Api 表單的預設值-{服務區域}' 中的字串其中`service-region`識別 hello hello 想 toobackup API 管理服務的裝載位置的 Azure 區域，例如：`North-Central-US`
* `serviceName`-hello hello 您要進行的備份在其建立 hello 時指定的 API 管理服務名稱
* `api-version` - 取代為 `2014-02-14`

Hello hello 要求主體中指定 hello 目標 Azure 儲存體帳戶名稱、 存取金鑰、 blob 容器名稱，以及備份名稱：

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

設定 hello hello 值`Content-Type`要求標頭太`application/json`。

備份是一項長時間執行的作業，可能需要多個分鐘 toocomplete。  如果 hello 要求成功，並已起始 hello 備份程序將會收到`202 Accepted`回應狀態碼和`Location`標頭。  請 'GET' 要求在 hello toohello URL`Location`標頭 toofind 出 hello hello 作業狀態。 Hello 備份正在進行時，您將繼續 tooreceive '202 已接受' 的狀態碼。 回應碼`200 OK`會指出 hello 備份作業成功完成。

請注意下列條件約束進行的備份要求時的 hello。

* **容器**hello 要求主體中指定**必須存在於**。
* 備份進行時，請「避免嘗試任何服務管理作業」  ，如提升或降低 SKU、變更網域名稱等。
* 還原**備份只會保證 30 天**自其建立 hello 快照。
* **使用量資料**用來建立分析報表**就不會包含**hello 備份中。 使用[Azure API 管理 REST API] [ Azure API Management REST API] tooperiodically 擷取分析報表，以妥善保存。
* hello 與您執行服務備份的頻率會影響您的復原點目標。 toominimize 它建議實作定期備份，以及執行指定備份後進行重要變更 tooyour API 管理服務。
* **變更**提出的 toohello 服務組態 （例如應用程式開發介面、 原則、 開發人員入口網站的外觀），備份作業正在進行**可能不會包含在 hello 備份，因此將會遺失**。

## <a name="step2"> </a>還原 API 管理服務
toorestore API 管理服務從先前建立的備份進行下列 HTTP 要求的 hello:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

其中：

* `subscriptionId`-hello 訂用帳戶包含您要還原備份時的 hello API 管理服務識別碼
* `resourceGroupName`-hello 'Api 表單的預設值-{服務區域}' 中的字串其中`service-region`識別 hello Azure 區域裝載 hello API 管理服務，您要還原至備份的位置，例如：`North-Central-US`
* `serviceName`-hello hello API 管理 hello 其建立時指定還原到的服務名稱
* `api-version` - 取代為 `2014-02-14`

Hello hello 要求主體中指定 hello 備份檔案位置，也就是 Azure 儲存體帳戶名稱、 存取金鑰、 blob 容器名稱，以及備份名稱：

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

設定 hello hello 值`Content-Type`要求標頭太`application/json`。

還原是長時間執行的作業，可能會佔用 too30 或多個分鐘 toocomplete。  如果 hello 要求成功，已起始 hello 還原程序，您會收到`202 Accepted`回應狀態碼和`Location`標頭。  請 'GET' 要求在 hello toohello URL`Location`標頭 toofind 出 hello hello 作業狀態。 Hello 還原正在進行時，您將繼續 tooreceive '202 已接受' 狀態碼。 回應碼`200 OK`會指出 hello 還原作業成功完成。

> [!IMPORTANT]
> **hello SKU**的 hello 服務還原到**必須符合**hello hello 的 SKU 備份正在還原服務。
>
> **變更**提出的 toohello 服務組態 （例如應用程式開發介面、 原則、 開發人員入口網站的外觀），還原作業正在進行中**可能會覆寫**。
>
>

## <a name="next-steps"></a>後續步驟
簽出 hello 遵循 hello 備份/還原程序的兩個不同的逐步解說的 Microsoft 部落格。

* [複寫 Azure API 管理帳戶 (英文)](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * 感謝您 tooGisela 她比重 toothis 發行項。
* [Azure API 管理：備份和還原組態 (英文)](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * 藉由 Stuart 詳細 hello 方法不符合 hello 正式的指導，但它是非常有趣。

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
