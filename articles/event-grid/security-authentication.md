---
title: "aaaAzure 事件方格安全性和驗證"
description: "說明 Azure Event Grid 與其概念。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a>Event Grid 安全性與驗證 

Azure Event Grid 有三種驗證方法：

* 事件訂閱
* 事件發佈
* WebHook 事件傳遞

## <a name="webhook-event-delivery"></a>WebHook 事件傳遞

Webhook 為其中一個即時 Azure 事件方格中的許多方式 tooreceive 事件。

每當有未傳遞新事件準備 toobe，事件方格會傳送 HTTP 要求與 hello 事件 tooyour WebHook 與 hello 主體中。

當您註冊您自己的 WebHook 端點事件方格時，它傳送給您以簡單的驗證程式碼的 POST 要求中順序 tooprove 端點擁有權。 您的應用程式需要 toorespond 回應後 hello 驗證程式碼。 事件方格將不會傳送事件 tooWebHook 皆未通過 hello 驗證的端點。
 
### <a name="validation-details"></a>驗證詳細資料：

* 在 hello 訂用帳戶建立/更新事件時，事件方格會公佈"SubscriptionValidationEvent 」 事件 toohello 目標端點。
* hello 事件中包含的標頭值 「 事件類型:: 驗證 」。
* hello 事件主體具有 hello 和其他事件方格事件相同的結構描述。
* hello 事件資料包含以隨機產生的字串"ValidationCode"屬性例如“ValidationCode: acb13…”。

順序 tooprove 端點擁有權，以回應後 hello 驗證程式碼如"ValidationResponse: acb13...」。

最後，它是重要 toonote Azure 事件方格僅支援 HTTPS webhook 端點。
## <a name="event-subscription"></a>事件訂閱

toosubscribe tooan 事件，您必須擁有 hello **Microsoft.EventGrid/EventSubscriptions/Write** hello 權限所需的資源。 您需要此權限，因為您要撰寫的新訂用帳戶在 hello 範圍 hello 資源。 hello 必要資源與根據您要訂閱 tooa 系統主題或自訂的主題。 本節會說明這兩種類型。

### <a name="system-topics-azure-service-publishers"></a>系統主題 (Azure 服務發行者)

對於系統的主題，您需要權限 toowrite 新事件訂閱 hello 範圍的 hello 資源發佈 hello 事件。 hello hello 之資源的格式如下：`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`

例如，toosubscribe tooan 事件上名為的儲存體帳戶**myacct**，您在需要 hello Microsoft.EventGrid/EventSubscriptions/Write 權限：`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`

### <a name="custom-topics"></a>自訂主題

如需自訂主題，您需要權限 toowrite 新事件訂閱 hello 範圍的 hello 事件方格主題。 hello hello 之資源的格式如下：`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`

例如，toosubscribe tooa 自訂主題名為**mytopic**，您在需要 hello Microsoft.EventGrid/EventSubscriptions/Write 權限：`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`

## <a name="topic-publishing"></a>主題發佈

主題使用共用存取簽章 (SAS) 或金鑰驗證。 我們建議使用 SAS，但金鑰驗證提供簡單的程式編寫，並且與許多現有的 Webhook 發佈者相容。 

Hello HTTP 標頭中包含 hello 驗證值。 使用 SAS， **aeg sas 權杖**hello 標頭值。 針對驗證、 使用**aeg sas 金鑰**hello 標頭值。

### <a name="key-authentication"></a>金鑰驗證

Hello 最簡單形式的驗證金鑰驗證。 使用 hello 格式：`aeg-sas-key: <your key>`

舉例來說，您將金鑰與此一起傳遞： 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a>SAS 權杖

事件方格的 SAS 權杖包含 hello 資源、 到期時間和簽章。 hello hello SAS 權杖的格式為： `r={resource}&e={expiration}&s={signature}`。

hello 資源是 hello 路徑的 hello 主題 toowhich 傳送事件。 以下為一個有效資源路徑的例子：`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`

您可以產生 hello 簽章從機碼。

以下為一個有效 **aeg-sas-token** 值的例子：

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

hello 下列範例會建立 SAS 權杖使用事件方格：

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a>Management Access Control

Azure 事件方格可讓您 toocontrol hello 的層級指定的存取 toodifferent 使用者 toodo 各種管理操作，例如清單事件訂閱、 建立新的並產生索引鍵。 Event Grid 為此使用 Azure 的 Role Based Access Check (RBAC)。

### <a name="operation-types"></a>作業類型

Azure 事件方格支援 hello 下列動作：

* Microsoft.EventGrid/*/read 
* Microsoft.EventGrid/*/write 
* Microsoft.EventGrid/*/delete 
* Microsoft.EventGrid/eventSubscriptions/getFullUrl/action 
* Microsoft.EventGrid/topics/listKeys/action 
* Microsoft.EventGrid/topics/regenerateKey/action

hello 最後三個作業傳回潛在機密資訊的取得從標準的讀取作業中篩選掉。 為您 toorestrict 存取 toothese 作業的最佳作法是。 您可以使用建立自訂角色[Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)， [Azure 命令列介面 (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)，和 hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md)。

### <a name="enforcing-role-based-access-check-rbac"></a>強制執行 Role Based Access Check (RBAC)

使用下列步驟 tooenforce RBAC 針對不同使用者的 hello:

#### <a name="create-a-custom-role-definition-file-json"></a>建立自訂的角色定義檔案 (.json)

hello 下面是範例事件方格角色定義可讓使用者 tooperform 組不同的動作。

**EventGridReadOnlyRole.json**：只允許唯讀作業。
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

**EventGridNoDeleteListKeysRole.json**：允許限制的張貼動作，但不允許刪除。
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
**EventGridContributorRole.json**：允許所有 Grid 動作。  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a>安裝與登入 tooAzure CLI

* Azure CLI 0.8.8 版或更新版本。 tooinstall hello 最新版本並關聯它與您 Azure 訂用帳戶，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。
* Azure CLI 中的 Azure Resource Manager。 跳過[hello 資源管理員的使用 hello Azure CLI](../xplat-cli-azure-resource-manager.md)如需詳細資訊。

#### <a name="create-a-custom-role"></a>建立自訂角色

toocreate 自訂安全性角色，使用：

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a>Hello 角色 tooa 使用者指派


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a>後續步驟

* 如簡介 tooEvent 格線，請參閱[有關事件方格](overview.md)
