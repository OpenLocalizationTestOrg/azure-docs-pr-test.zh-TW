---
title: "aaaResource 管理員 REST Api |Microsoft 文件"
description: "Hello 資源管理員 REST Api 驗證和使用方式範例的概觀"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>資源管理員 REST API
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [入口網站](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

每個已部署的範本，之後每個呼叫 tooAzure 資源管理員 中，後面背後的每個設定的儲存體帳戶有一或多個呼叫 toohello Azure 資源管理員的 RESTful API。 本主題是專供的 toothose Api 和如何呼叫它們而不使用任何 SDK。 如果您想要完整控制要求 tooAzure 或您慣用的語言 hello SDK 無法使用或不支援您所需要的 hello 操作，則這個方法會很有用。

這篇文章不會進出公開在 Azure 中，但而是使用某些作業做為範例的連接 toothem 的方式每一種 API。 了解 hello 基本概念之後，您可以閱讀 hello [Azure 資源管理員 REST API 參考](https://docs.microsoft.com/rest/api/resources/)toofind 的詳細資訊的 toouse hello rest hello 應用程式開發介面的方式。

## <a name="authentication"></a>驗證
Resource Manager 的驗證由 Azure Active Directory (AD) 處理。 tooconnect tooany API，您必須先 tooauthenticate 與 Azure AD tooreceive tooevery 要求，您可以傳遞之驗證語彙基元。 因為我們要描述的純虛擬的呼叫，直接 toohello REST Api，我們假設您不想 tooauthenticate 由提示輸入使用者名稱和密碼。 我們也假設您不使用雙重要素驗證機制。 因此，我們會建立稱為 Azure AD 應用程式和服務主體所使用的 toolog 中。 但是請記住，Azure AD 支援數項驗證程序和全部都可能是該驗證權杖，供後續的 API 要求所使用的 tooretrieve。
請依照[建立 Azure AD 應用程式和服務主體](resource-group-create-service-principal-portal.md)的逐步指示。

### <a name="generating-an-access-token"></a>產生存取權杖
Azure AD 的驗證方式是呼叫 tooAzure AD 中，位於 login.microsoftonline.com。tooauthenticate，您需要下列資訊 toohave hello:

* Azure AD 租用戶識別碼 （hello Azure AD 使用 toolog 中的名稱，通常 hello 與您的公司相同但並非必要）
* （已取得 hello Azure AD 應用程式建立步驟期間） 的應用程式識別碼
* 密碼 （您所選取建立 hello Azure AD 應用程式時）

在下列 HTTP 要求的 hello，請確定 tooreplace"Azure AD 租用戶識別碼"，"應用程式識別碼 」 和 「 密碼 」 及 hello 正確的值。

**一般 HTTP 要求︰**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

...（如果驗證成功） 將導致回應類似 toohello 下列回應：

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
（在前面回應 hello hello access_token 已縮短的 tooincrease 可讀性）

**使用 Bash 產生存取權杖：**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**使用 PowerShell 產生存取權杖：**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

hello 回應包含存取權杖、 資訊多久該語彙基元有效，以及相關資訊的資源，您可以使用該語彙基元。
您在上一個 HTTP 呼叫 hello 中收到 hello 存取權杖必須傳入的所有要求 toohello 資源管理員 API。 您可以將它當做 hello 值"Bearer YOUR_ACCESS_TOKEN"名為 「 授權 」 標頭值。 請注意"Bearer"和存取權杖的 hello 間距。

您可以看到從 hello HTTP 結果上方，hello 權杖的有效期為特定的一段時間期間，您應該快取並重複使用該相同的語彙基元。 即使是針對每個應用程式開發介面呼叫 Azure AD 可能 tooauthenticate，將高效率不佳。

## <a name="calling-resource-manager-rest-apis"></a>呼叫 Resource Manager REST API
本主題只會使用幾個應用程式開發介面 tooexplain hello 基本用法的 hello REST 作業。 如需所有 hello 作業的資訊，請參閱[Azure 資源管理員 REST Api](https://docs.microsoft.com/rest/api/resources/)。

### <a name="list-all-subscriptions"></a>列出所有訂用帳戶
其中一個 hello 最簡單的作業，您可以為 toolist hello 可用訂用帳戶可以存取。 在 hello 下列要求，您會看到如何 hello 存取權杖以傳遞做為標頭：

(以您實際的存取權杖取代 YOUR_ACCESS_TOKEN。)

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

...，如此一來，您以取得訂用帳戶的清單，允許此服務主體 tooaccess

(為了便於閱讀，已縮短訂用帳戶識別碼)

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>列出特定訂用帳戶中的所有資源群組
可用以 hello 資源管理員 Api 的所有資源都在資源群組巢都狀。 您可以使用下列 HTTP GET 要求的 hello 您訂用帳戶中現有的資源群組查詢資源管理員。 請注意如何 hello 訂用帳戶 ID 傳入 hello URL 的一部分此時間。

(以實際的存取權杖和訂用帳戶識別碼取代 YOUR_ACCESS_TOKEN 和 SUBSCRIPTION_ID)

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

hello 您收到的回應取決於您是否有定義任何資源群組，如果是這樣，多少。

(為了便於閱讀，已縮短訂用帳戶識別碼)

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>建立資源群組
目前為止，我們已只被查詢 hello 資源管理員 Api 的資訊。 它是我們建立某些資源，並讓我們開始 hello 它們全部，資源群組的最簡單的時間。 hello 下列 HTTP 要求建立資源群組中 地區/您所選擇的位置，並將標記 tooit。

（取代 YOUR_ACCESS_TOKEN、 SUBSCRIPTION_ID、 RESOURCE_GROUP_NAME 您實際存取權杖、 訂用帳戶 ID 和名稱的 hello 想 toocreate 的資源群組）

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

如果成功，會產生下列回應類似 toohello 的回應：

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

您已在 Azure 中成功建立資源群組。 恭喜！

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>部署資源 tooa 資源群組使用資源管理員範本
Resource Manager 可讓您使用範本來部署資源。 範本定義數個資源及其相依性。 本節中，我們假設您熟悉資源管理員範本和我們剛為您示範如何 toomake hello API 呼叫 toostart 部署。 如需有關建構範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。

部署範本不會與不同多 toohow 呼叫其他應用程式開發介面。 較特別的是部署範本可能需要很長的時間。 hello API 呼叫只會傳回，也可以 tooyou 為開發人員 tooquery 狀態為 hello 部署 toofind 出 hello 部署完成。 如需詳細資訊，請參閱[追蹤非同步 Azure 作業](resource-manager-async-operations.md)。

在此範例中，我們使用 [GitHub](https://github.com/Azure/azure-quickstart-templates) 上提供的公開範本。 我們使用 hello 範本部署 Linux VM toohello 美國西部地區。 即使這個範例會使用公用等 GitHub 儲存機制中可用的範本，您可以改為傳遞 hello 完整範本，為 hello 要求的一部分。 請注意，我們提供了 hello 內所使用的參數值在 hello 要求部署範本。

（取代 SUBSCRIPTION_ID、 RESOURCE_GROUP_NAME、 DEPLOYMENT_NAME、 YOUR_ACCESS_TOKEN、 GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME、 ADMIN_USER_NAME、 ADMIN_PASSWORD 和 DNS_NAME_FOR_PUBLIC_IP toovalues 適用於您的要求）

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

hello 長 JSON 回應此要求已省略的 tooimprove 可讀性，這份文件。 hello 回應會包含您所建立的 hello 樣板化部署的相關資訊。

## <a name="next-steps"></a>後續步驟

- toolearn 有關處理非同步 REST 作業，請參閱[追蹤非同步的 Azure 作業](resource-manager-async-operations.md)。
