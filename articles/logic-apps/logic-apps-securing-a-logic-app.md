---
title: "aaaSecure 存取 tooAzure Logic Apps |Microsoft 文件"
description: "新增安全性來保護存取 tootriggers、 輸入和輸出、 動作參數，以及與 Azure 邏輯應用程式中的工作流程搭配使用的服務。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a>安全存取 tooyour 邏輯應用程式

有許多工具可用 toohelp 安全應用程式邏輯。

* 保護存取 tootrigger 邏輯應用程式 （HTTP 要求觸發程序）
* 保護存取 toomanage 編輯或讀取邏輯應用程式
* 保護存取 toocontents 的測試回合的輸入和輸出
* 保護工作流程中動作內的參數或輸入
* 從工作流程中接收要求的安全存取 tooservices

## <a name="secure-access-tootrigger"></a>安全存取 tootrigger

當您使用邏輯應用程式引發 HTTP 要求 ([要求](../connectors/connectors-native-reqres.md)或[Webhook](../connectors/connectors-native-webhook.md))，您可以限制存取，讓只有獲得授權的用戶端可以引發 hello 邏輯應用程式。 所有傳入邏輯應用程式的要求都會透過 SSL 加密並保護。

### <a name="shared-access-signature"></a>共用存取簽章

邏輯應用程式的每個要求端點包含[共用存取簽章 (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello URL 的一部分。 每個 URL 都包含 `sp`、`sv` 和 `sig` 查詢參數。 所指定權限`sp`，而且對應 tooHTTP 方法允許，`sv`是 hello 使用版本 toogenerate，和`sig`是使用的 tooauthenticate 存取 tootrigger。 hello 簽章會產生與秘密金鑰的所有 hello URL 路徑和屬性上使用 hello SHA256 演算法。 hello 祕密金鑰永遠不會公開和發行，並會保留加密並儲存，一部分的 hello 邏輯應用程式。 邏輯應用程式只會授權包含有效的簽章與 hello 祕密金鑰建立的觸發程序。

#### <a name="regenerate-access-keys"></a>重新產生存取金鑰

您可以重新產生新的安全金鑰在任何時候透過 hello REST API 或 Azure 入口網站。 先前使用 hello 舊金鑰產生的所有目前 Url 會失效，無法再授權 toofire hello 邏輯應用程式。

1. 在 hello Azure 入口網站，開啟您想 tooregenerate 索引鍵的 hello 邏輯應用程式
1. 按一下 hello**便捷鍵**下的功能表項目**設定**
1. 選擇 hello 金鑰 tooregenerate 和完整 hello 程序

您重新產生之後擷取的 Url 會以 hello 新的存取金鑰簽署。

#### <a name="creating-callback-urls-with-an-expiration-date"></a>使用具有到期日期的回呼 URL

如果您與其他合作對象共用 hello URL，您可以在具有特定索引鍵和到期日，視需要產生 Url。 您可以順暢地向前復原索引鍵，或確定存取 toofire 應用程式是受限制的 tooa 特定 timespan。 您可以指定到期日 hello 透過 url [REST API 的 logic apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers):

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Hello 主體中包含 hello 屬性`NotAfter`為 JSON 的日期字串，它會傳回回呼 URL，才會有效直到 hello`NotAfter`日期和時間。

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a>建立具有主要或次要秘密金鑰的 URL

當您產生，或以要求為基礎的觸發程序的回呼 Url 的清單時，您也可以指定哪些金鑰 toouse toosign hello URL。  您可以產生 URL，由 hello 透過特定的金鑰簽署[REST API 的 logic apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers) ，如下所示：

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

Hello 主體中包含 hello 屬性`KeyType`為`Primary`或`Secondary`。  這會傳回所指定的 hello 安全金鑰簽章的 URL。

### <a name="restrict-incoming-ip-addresses"></a>限制傳入的 IP 位址

此外 toohello 共用存取簽章，您可能想要 toorestrict 只從特定的用戶端呼叫邏輯應用程式。  例如，如果您管理您的端點，透過 Azure API 管理，您可以限制 hello 邏輯應用程式 tooonly 接受 hello 要求，當 hello 要求來自 hello API 管理執行個體的 IP 位址。

可以在 hello 邏輯應用程式設定中設定此設定：

1. 在 hello Azure 入口網站，開啟您想 tooadd IP 位址限制的 hello 邏輯應用程式
1. 按一下 hello**存取控制設定**下的功能表項目**設定**
1. 指定 IP 位址範圍 toobe hello 觸發程序所接受的 hello 的清單

有效的 IP 範圍可接受 hello 格式`192.168.1.1/255`。 如果您想 hello 邏輯應用程式 tooonly 引發為巢狀的邏輯應用程式，請選取 hello**只有其他的 logic apps**選項。 此選項會將空的陣列 toohello 資源，這表示只有呼叫 hello 從服務本身 （父邏輯應用程式） 引發已成功。

> [!NOTE]
> 您仍然可以執行要求的觸發程序邏輯應用程式，透過 REST API hello / 管理`/triggers/{triggerName}/run`不論 IP。 此案例需要驗證的 hello Azure REST API，而且所有事件會都出現在 hello Azure 稽核記錄檔。 請適當地設定存取控制原則。

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>在 hello 資源定義上設定 IP 範圍

如果您使用[部署範本](logic-apps-create-deploy-template.md)tooautomate 可以 hello 資源範本設定您的部署 hello IP 範圍設定。  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a>新增 Azure Active Directory、OAuth 或其他安全性

更多授權通訊協定在邏輯應用程式頂端的 tooadd [Azure API 管理](https://azure.microsoft.com/services/api-management/)當做 API 邏輯應用程式提供豐富監視、 安全性、 原則和文件以 hello 功能 tooexpose 任何端點。 Azure API 管理可以公開 hello 邏輯應用程式，這可以使用 Azure Active Directory、 憑證、 OAuth、 或其他安全性標準的公用或私用端點。 收到要求時，Azure API 管理轉送 hello 要求 toohello 邏輯應用程式 （執行任何所需的轉換或進行中的限制）。 您可以使用 hello hello 邏輯應用程式 tooonly 上的設定允許 hello 邏輯應用程式 toobe 觸發從 API 管理連入 IP 範圍。

## <a name="secure-access-toomanage-or-edit-logic-apps"></a>安全存取 toomanage 或編輯邏輯應用程式

您可以限制存取 toomanagement 作業邏輯應用程式，以便只有特定使用者或群組能夠 tooperform hello 資源上的作業。 邏輯應用程式使用 hello Azure[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)功能，並且可以自訂以 hello 相同的工具。  有幾個內建的角色，您也可以將指派的訂用帳戶 tooas 成員：

* **邏輯應用程式參與者**-提供存取 tooview、 編輯和更新邏輯應用程式。  無法移除 hello 資源或執行管理作業。
* **邏輯應用程式運算子**-可以檢視 hello 邏輯應用程式和執行歷程記錄，並啟用/停用。  無法編輯或更新 hello 定義。

您也可以使用[Azure 資源鎖定](../azure-resource-manager/resource-group-lock-resources.md)tooprevent 變更或刪除邏輯應用程式。 此功能相當重要 tooprevent 實際執行資源變更或刪除。

## <a name="secure-access-toocontents-of-hello-run-history"></a>安全存取 toocontents 的 hello 執行歷程記錄

您可以從上一個回合 toospecific IP 位址範圍來限制存取 toocontents 的輸入或輸出。  

工作流程執行中的所有資料在傳輸及靜止時都會加密。 當呼叫 toorun 記錄時，hello 服務驗證 hello 要求，並提供連結 toohello 要求和回應輸入和輸出。 這個連結可以在受保護的只要求指定的 IP 位址範圍內的 tooview 內容傳回 hello 內容。 您可以使用此功能來進行其他存取控制。 您甚至可以指定如 `0.0.0.0` 的 IP 位址，這樣就沒有人可以存取輸入/輸出。 只有具備系統管理員權限的人可能會移除這項限制，提供 hello 可能性 '在 just-in-time' 存取 tooworkflow 內容。

中的 hello Azure 入口網站的 hello 資源設定，可以設定此設定：

1. 在 hello Azure 入口網站，開啟您想 tooadd IP 位址限制的 hello 邏輯應用程式
1. 按一下 hello**存取控制設定**下的功能表項目**設定**
1. 指定 IP 位址範圍存取 toocontent hello 的清單

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a>在 hello 資源定義上設定 IP 範圍

如果您使用[部署範本](logic-apps-create-deploy-template.md)tooautomate 可以 hello 資源範本設定您的部署 hello IP 範圍設定。  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a>保護工作流程中的參數和輸入

您可以 tooparameterize 部署的工作流程定義的某些層面的環境。 此外，某些參數可能是安全的參數，編輯工作流程，例如用戶端識別碼和用戶端密碼時，您不想 tooappear [Azure Active Directory 驗證](../connectors/connectors-native-http.md#authentication)的 HTTP 動作。

### <a name="using-parameters-and-secure-parameters"></a>使用參數和安全參數

tooaccess hello 資源在執行階段，參數值的 hello[工作流程定義語言](http://aka.ms/logicappsdocs)提供`@parameters()`作業。 此外，您也可以[hello 資源部署範本中指定參數](../azure-resource-manager/resource-group-authoring-templates.md#parameters)。 但是，如果您指定 hello 參數類型為`securestring`，hello 參數將不會傳回與 hello 其餘 hello 資源定義，而且不會藉由部署後檢視 hello 資源存取。

> [!NOTE]
> 如果您的參數使用 hello 標頭或要求主體中，hello 參數可能會看到存取 hello 執行歷程記錄和外送 HTTP 要求。 因此請確定 tooset 內容的存取原則。
> 授權標頭絕對不會透過輸入或輸出來顯示。 因此如果有使用 hello 密碼，hello 密碼不可以擷取。

#### <a name="resource-deployment-template-with-secrets"></a>含有密碼的資源部署範本

hello 下列範例將示範參考參數的安全部署`secret`在執行階段。 在不同的參數檔案中，您可以指定 hello 的 hello 環境值`secret`，或使用[Azure 資源管理員 KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve 機密資料，在部署階段。

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a>安全存取 tooservices 接收要求，從工作流程

有許多方式 toohelp 安全任何端點 hello 邏輯應用程式需要 tooaccess。

### <a name="using-authentication-on-outbound-requests"></a>在外送要求上使用驗證

當使用 HTTP、 HTTP + Swagger (開啟的 API) 或 Webhook 動作，您可以加入驗證 toohello 要求傳送。 您可以包括基本驗證、憑證驗證或 Azure Active Directory 驗證。 有關如何 tooconfigure 此驗證可找到[本文](../connectors/connectors-native-http.md#authentication)。

### <a name="restricting-access-toologic-app-ip-addresses"></a>限制存取 toologic 應用程式的 IP 位址

邏輯應用程式的所有呼叫都來自每個區域一組特定的 IP 位址。 您可以加入其他篩選 tooonly 接受來自指定 IP 位址的要求。 如需這些 IP 位址清單，請參閱[邏輯應用程式的限制和設定](logic-apps-limits-and-config.md#configuration)。

### <a name="on-premises-connectivity"></a>內部部署連線能力

邏輯應用程式提供數個服務 tooprovide 安全、 可靠與整合的內部通訊。

#### <a name="on-premises-data-gateway"></a>內部部署資料閘道

多 managed 的連接器邏輯應用程式提供安全的連線 tooon 內部部署系統，包括檔案系統、 SQL、 SharePoint、 DB2 和更多。 hello 閘道轉送上 hello Azure Service Bus 透過加密通道在內部部署來源的資料。 所有流量都來自為 hello 閘道代理程式的安全輸出流量。 深入了解[hello 資料閘道的運作方式](logic-apps-gateway-install.md#gateway-cloud-service)。

#### <a name="azure-api-management"></a>Azure API 管理

[Azure API 管理](https://azure.microsoft.com/services/api-management/)有內部部署連線選項，包括安全的 proxy 和通訊 tooon 內部部署系統的站對站 VPN 和 ExpressRoute 整合。 在 hello 邏輯應用程式的設計工具，您可以快速地選取 API 從 Azure API 管理公開工作流程中，提供快速存取 tooon 內部部署系統。

#### <a name="hybrid-connections-from-azure-app-service"></a>Azure App Service 的混合式連線

Azure API 和 Web 應用程式 toocommunicate 內部部署，您可以使用 hello 在內部部署混合式連接功能。  混合式連線及 tooconfigure 可以找到方式的詳細資訊[本文](../app-service-web/web-sites-hybrid-connection-get-started.md)。

## <a name="next-steps"></a>後續步驟
[建立部署範本](logic-apps-create-deploy-template.md)  
[例外狀況處理](logic-apps-exception-handling.md)  
[監視邏輯應用程式](logic-apps-monitor-your-logic-apps.md)  
[診斷邏輯應用程式失敗和問題](logic-apps-diagnosing-failures.md)  
