---
title: "aaaSchema 更新年 8 月 1 2015 preview-Azure 邏輯應用程式 |Microsoft 文件"
description: "使用結構描述 2015-08-01-preview 版本建立 Azure Logic Apps 的 JSON 定義"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="c214a-103">Azure Logic Apps 的結構描述更新 - 2015 年 8 月 1 日預覽</span><span class="sxs-lookup"><span data-stu-id="c214a-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="c214a-104">這個新的結構描述和 API 版本 Azure 邏輯應用程式包含多個製作邏輯應用程式的重要改良 toouse 可靠且更容易：</span><span class="sxs-lookup"><span data-stu-id="c214a-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="c214a-105">hello **APIApp**動作類型是新的更新的 tooa [ **APIConnection** ](#api-connections)動作類型。</span><span class="sxs-lookup"><span data-stu-id="c214a-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="c214a-106">**重複**重新命名過[**Foreach**](#foreach)。</span><span class="sxs-lookup"><span data-stu-id="c214a-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="c214a-107">hello [ **HTTP 接聽程式**API 應用程式](#http-listener)已不再需要。</span><span class="sxs-lookup"><span data-stu-id="c214a-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="c214a-108">呼叫子工作流程時使用[新的結構描述](#child-workflows)。</span><span class="sxs-lookup"><span data-stu-id="c214a-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="c214a-109">移動 tooAPI 連線</span><span class="sxs-lookup"><span data-stu-id="c214a-109">Move tooAPI connections</span></span>

<span data-ttu-id="c214a-110">hello 最大變更是，您不再需要 toodeploy API 應用程式到您的 Azure 訂閱，您可以使用 Api。</span><span class="sxs-lookup"><span data-stu-id="c214a-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="c214a-111">以下是您可以使用 Api 的 hello 方法：</span><span class="sxs-lookup"><span data-stu-id="c214a-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="c214a-112">Managed API</span><span class="sxs-lookup"><span data-stu-id="c214a-112">Managed APIs</span></span>
* <span data-ttu-id="c214a-113">您自訂的 Web API</span><span class="sxs-lookup"><span data-stu-id="c214a-113">Your custom Web APIs</span></span>

<span data-ttu-id="c214a-114">每一種方式都因為其管理和裝載模型不同，而有稍微不同的處理方式。</span><span class="sxs-lookup"><span data-stu-id="c214a-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="c214a-115">此模型中的其中一個優點是您不再限制 tooresources 部署在 Azure 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="c214a-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="c214a-116">Managed API</span><span class="sxs-lookup"><span data-stu-id="c214a-116">Managed APIs</span></span>

<span data-ttu-id="c214a-117">Microsoft 會代表您管理某些 API，例如 Office 365、Salesforce、Twitter 和 FTP。</span><span class="sxs-lookup"><span data-stu-id="c214a-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="c214a-118">您可以直接使用部分 Managed API (例如 Bing 翻譯)，有些則需要設定。</span><span class="sxs-lookup"><span data-stu-id="c214a-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="c214a-119">此組態稱為「連接」 。</span><span class="sxs-lookup"><span data-stu-id="c214a-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="c214a-120">例如，當您使用 Office 365 時，您必須建立包含 Office 365 登入權杖的連線。</span><span class="sxs-lookup"><span data-stu-id="c214a-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="c214a-121">這個語彙基元會安全地儲存，並重新整理可讓您的邏輯應用程式一律呼叫 hello Office 365 API。</span><span class="sxs-lookup"><span data-stu-id="c214a-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="c214a-122">或者，如果您希望 tooconnect tooyour SQL 或 FTP 伺服器時，您必須建立具有 hello 連接字串的連接。</span><span class="sxs-lookup"><span data-stu-id="c214a-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="c214a-123">這些動作在此定義內稱為 `APIConnection`。</span><span class="sxs-lookup"><span data-stu-id="c214a-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="c214a-124">呼叫 Office 365 toosend 電子郵件連線的範例如下：</span><span class="sxs-lookup"><span data-stu-id="c214a-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

<span data-ttu-id="c214a-125">hello`host`物件是輸入部分的唯一 tooAPI 連線，且包含具有組件：`api`和`connection`。</span><span class="sxs-lookup"><span data-stu-id="c214a-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="c214a-126">hello`api`具有 hello 執行階段裝載的受管理應用程式開發介面的 URL。</span><span class="sxs-lookup"><span data-stu-id="c214a-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="c214a-127">您可以查看所有可用的 hello 藉由呼叫 managed Api `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`。</span><span class="sxs-lookup"><span data-stu-id="c214a-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="c214a-128">當您使用應用程式開發介面時，hello API 可能會或可能不含任何*連接參數*定義。</span><span class="sxs-lookup"><span data-stu-id="c214a-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="c214a-129">Hello 應用程式開發介面不是，如果沒有*連接*需要。</span><span class="sxs-lookup"><span data-stu-id="c214a-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="c214a-130">如果 hello API，您必須建立連接。</span><span class="sxs-lookup"><span data-stu-id="c214a-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="c214a-131">建立 hello 連接都有您所選擇的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="c214a-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="c214a-132">您再參考 hello 中的 hello 名稱`connection`物件內 hello`host`物件。</span><span class="sxs-lookup"><span data-stu-id="c214a-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="c214a-133">toocreate 在資源群組中，呼叫的連接：</span><span class="sxs-lookup"><span data-stu-id="c214a-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="c214a-134">以 hello 下列主體：</span><span class="sxs-lookup"><span data-stu-id="c214a-134">With hello following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="c214a-135">在 Azure Resource Manager 範本中部署 Managed API</span><span class="sxs-lookup"><span data-stu-id="c214a-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="c214a-136">您可以在 Azure Resource Manager 範本中建立完整的應用程式，但前提是不需進行互動式登入。</span><span class="sxs-lookup"><span data-stu-id="c214a-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="c214a-137">如果登入需要，您可以設定 hello Azure Resource Manager 範本時，所有項目，不過您仍然需要 toovisit hello 入口 tooauthorize hello 連線。</span><span class="sxs-lookup"><span data-stu-id="c214a-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

<span data-ttu-id="c214a-138">您可以看到在這個範例 hello 連線是只存在於資源群組的資源。</span><span class="sxs-lookup"><span data-stu-id="c214a-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="c214a-139">事件所參考 hello 受管理應用程式開發介面使用 tooyou 您訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="c214a-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="c214a-140">您自訂的 Web API</span><span class="sxs-lookup"><span data-stu-id="c214a-140">Your custom Web APIs</span></span>

<span data-ttu-id="c214a-141">如果您使用您自己的 Api，不受 Microsoft 管理的項目，使用內建的 hello **HTTP**動作 toocall 它們。</span><span class="sxs-lookup"><span data-stu-id="c214a-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="c214a-142">為了獲得理想的體驗，您應該公開您 API 的 Swagger 端點。</span><span class="sxs-lookup"><span data-stu-id="c214a-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="c214a-143">此端點可讓 hello 邏輯應用程式的設計工具 toorender hello 輸入，而且您 API 的輸出。</span><span class="sxs-lookup"><span data-stu-id="c214a-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="c214a-144">沒有 Swagger，hello 設計工具可以只顯示 hello 輸入及輸出為不透明的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="c214a-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="c214a-145">以下是範例顯示 hello 新`metadata.apiDefinitionUrl`屬性：</span><span class="sxs-lookup"><span data-stu-id="c214a-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

<span data-ttu-id="c214a-146">如果您裝載您的 Web API，Azure App Service 上，您的 Web API 就會自動出現在 hello hello 設計工具中可用動作清單中。</span><span class="sxs-lookup"><span data-stu-id="c214a-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="c214a-147">如果沒有，您在 toopaste hello URL 直接。</span><span class="sxs-lookup"><span data-stu-id="c214a-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="c214a-148">hello Swagger 端點必須是可 hello 邏輯應用程式的設計工具，用於未經驗證的 toobe，雖然您可以保護任何 Swagger 所支援的方法與 hello API 本身。</span><span class="sxs-lookup"><span data-stu-id="c214a-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="c214a-149">搭配 2015-08-01-preview 呼叫已部署的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="c214a-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="c214a-150">如果您先前部署 API 應用程式，您可以呼叫 hello 應用程式以 hello **HTTP**動作。</span><span class="sxs-lookup"><span data-stu-id="c214a-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="c214a-151">例如，如果您使用 Dropbox toolist 檔案，您**2014年-12-01-預覽**結構描述版本定義可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="c214a-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="c214a-152">Hello 的 hello 邏輯應用程式定義的參數區段保持不變時，您可以建構等此範例中，hello 相等 HTTP 動作：</span><span class="sxs-lookup"><span data-stu-id="c214a-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="c214a-153">逐一解說這些屬性：</span><span class="sxs-lookup"><span data-stu-id="c214a-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="c214a-154">動作屬性</span><span class="sxs-lookup"><span data-stu-id="c214a-154">Action property</span></span> | <span data-ttu-id="c214a-155">說明</span><span class="sxs-lookup"><span data-stu-id="c214a-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="c214a-156">`Http` 而不是 `APIapp`</span><span class="sxs-lookup"><span data-stu-id="c214a-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="c214a-157">toouse hello 邏輯應用程式的設計工具，這個動作包括 hello 中繼資料端點，建構自：`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="c214a-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="c214a-158">建構來源：`{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="c214a-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="c214a-159">一律為 `POST`</span><span class="sxs-lookup"><span data-stu-id="c214a-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="c214a-160">相同 toohello API 應用程式參數</span><span class="sxs-lookup"><span data-stu-id="c214a-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="c214a-161">相同 toohello API 應用程式驗證</span><span class="sxs-lookup"><span data-stu-id="c214a-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="c214a-162">此方法應可適用於 API 應用程式的所有動作。</span><span class="sxs-lookup"><span data-stu-id="c214a-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="c214a-163">不過，請記住這些先前的 API 應用程式已不再受到支援。</span><span class="sxs-lookup"><span data-stu-id="c214a-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="c214a-164">因此您應該一併移動的 hello tooone 上述兩個其他選項，受管理的應用程式開發介面或裝載您自訂的 Web API。</span><span class="sxs-lookup"><span data-stu-id="c214a-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="c214a-165">重新命名 'repeat' too'foreach'</span><span class="sxs-lookup"><span data-stu-id="c214a-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="c214a-166">Hello 先前的結構描述版本，我們收到太多客戶的意見反應，**重複**會造成混淆並沒有正確擷取的**重複**真的 for each 迴圈。</span><span class="sxs-lookup"><span data-stu-id="c214a-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="c214a-167">如此一來，我們已重新命名`repeat`太`foreach`。</span><span class="sxs-lookup"><span data-stu-id="c214a-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="c214a-168">例如，您先前可以撰寫：</span><span class="sxs-lookup"><span data-stu-id="c214a-168">For example, previously you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

<span data-ttu-id="c214a-169">您現在可以撰寫：</span><span class="sxs-lookup"><span data-stu-id="c214a-169">Now you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

<span data-ttu-id="c214a-170">hello 函式`@repeatItem()`先前使用的 tooreference hello 目前項目要反覆查看。</span><span class="sxs-lookup"><span data-stu-id="c214a-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="c214a-171">此函式現在已簡化太`@item()`。</span><span class="sxs-lookup"><span data-stu-id="c214a-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="c214a-172">參考來自 'foreach' 的輸出</span><span class="sxs-lookup"><span data-stu-id="c214a-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="c214a-173">為簡化，hello 輸出從`foreach`動作不會包含在一個稱為物件`repeatItems`。</span><span class="sxs-lookup"><span data-stu-id="c214a-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="c214a-174">雖然 hello 輸出從先前的 hello`repeat`範例是：</span><span class="sxs-lookup"><span data-stu-id="c214a-174">While hello outputs from hello previous `repeat` example were:</span></span>

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

<span data-ttu-id="c214a-175">現在，這些輸出為：</span><span class="sxs-lookup"><span data-stu-id="c214a-175">Now these outputs are:</span></span>

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

<span data-ttu-id="c214a-176">先前，tooget toohello 本文的 hello 參照這些輸出的動作：</span><span class="sxs-lookup"><span data-stu-id="c214a-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="c214a-177">現在，您可以改為執行：</span><span class="sxs-lookup"><span data-stu-id="c214a-177">Now you can do instead:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="c214a-178">這些變更，hello 函式`@repeatItem()`， `@repeatBody()`，和`@repeatOutputs()`會移除。</span><span class="sxs-lookup"><span data-stu-id="c214a-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="c214a-179">原生 HTTP 接聽程式</span><span class="sxs-lookup"><span data-stu-id="c214a-179">Native HTTP listener</span></span>

<span data-ttu-id="c214a-180">hello 功能現在內建的 HTTP 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="c214a-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="c214a-181">因此您不再需要 toodeploy HTTP 接聽程式的 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c214a-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="c214a-182">請參閱[hello 完整詳細資料的方式 toomake 您邏輯應用程式端點可呼叫這裡](../logic-apps/logic-apps-http-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="c214a-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="c214a-183">這些變更，我們移除了 hello`@accessKeys()`函式，我們取代 hello`@listCallbackURL()`取得 hello 端點時所需的函式。</span><span class="sxs-lookup"><span data-stu-id="c214a-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="c214a-184">此外，您現在必須在邏輯應用程式中至少定義一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c214a-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="c214a-185">如果您想太`/run`hello 工作流程，您必須擁有這些觸發程序的其中一個： `manual`， `apiConnectionWebhook`，或`httpWebhook`。</span><span class="sxs-lookup"><span data-stu-id="c214a-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="c214a-186">呼叫子工作流程</span><span class="sxs-lookup"><span data-stu-id="c214a-186">Call child workflows</span></span>

<span data-ttu-id="c214a-187">之前，呼叫子工作流程，您必須將 toohello 工作流程中，取得 hello 存取權杖，並貼上 hello 語彙基元中您想要 toocall hello 邏輯應用程式定義的子工作流程。</span><span class="sxs-lookup"><span data-stu-id="c214a-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="c214a-188">與 hello 新結構描述，引擎會自動產生 SAS，以在執行階段針對 hello Logic Apps 讓您不要有太貼上任何機密 hello 定義 hello 子工作流程。</span><span class="sxs-lookup"><span data-stu-id="c214a-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="c214a-189">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="c214a-189">Here is an example:</span></span>

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

<span data-ttu-id="c214a-190">第二個改進是我們會賦予 hello 子工作流程的完整存取 toohello 連入要求。</span><span class="sxs-lookup"><span data-stu-id="c214a-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="c214a-191">這表示您可以在 hello 傳遞參數*查詢*區段在 hello*標頭*物件，而且您可以完全定義 hello 整個本文。</span><span class="sxs-lookup"><span data-stu-id="c214a-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="c214a-192">最後，有必要的變更 toohello 子工作流程。</span><span class="sxs-lookup"><span data-stu-id="c214a-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="c214a-193">雖然您無法直接先前呼叫的子工作流程，您現在必須定義觸發程序端點 hello 父 toocall 的 hello 工作流程中。</span><span class="sxs-lookup"><span data-stu-id="c214a-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="c214a-194">一般而言，您可以在其中加入觸發程序具有`manual`類型，而然後 hello 父定義中使用該觸發程序。</span><span class="sxs-lookup"><span data-stu-id="c214a-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="c214a-195">請注意 hello`host`屬性特別的是包含`triggerName`您一定要指定觸發程序，因為您叫用。</span><span class="sxs-lookup"><span data-stu-id="c214a-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="c214a-196">其他變更</span><span class="sxs-lookup"><span data-stu-id="c214a-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="c214a-197">新的 'queries' 屬性</span><span class="sxs-lookup"><span data-stu-id="c214a-197">New 'queries' property</span></span>

<span data-ttu-id="c214a-198">所有動作類型現在支援一個稱為 `queries`的新輸入。</span><span class="sxs-lookup"><span data-stu-id="c214a-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="c214a-199">此輸入可以是結構化的物件，而不是您以手動方式具有 tooassemble hello 字串。</span><span class="sxs-lookup"><span data-stu-id="c214a-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="c214a-200">重新命名 'parse()' 函式 too'json()'</span><span class="sxs-lookup"><span data-stu-id="c214a-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="c214a-201">我們要加入更多的內容類型過期，因此我們在重新命名 hello`parse()`函式太`json()`。</span><span class="sxs-lookup"><span data-stu-id="c214a-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="c214a-202">敬請期待：企業整合 API</span><span class="sxs-lookup"><span data-stu-id="c214a-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="c214a-203">我們沒有 hello 企業整合應用程式開發介面，例如 AS2 的受管理的版本。</span><span class="sxs-lookup"><span data-stu-id="c214a-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="c214a-204">同時，您可以使用您現有部署的 BizTalk 應用程式開發介面透過 hello HTTP 動作。</span><span class="sxs-lookup"><span data-stu-id="c214a-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="c214a-205">如需詳細資訊，請參閱 「 使用您已部署的應用程式開發介面應用程式 」 在 hello[整合藍圖](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/)。</span><span class="sxs-lookup"><span data-stu-id="c214a-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
