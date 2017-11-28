---
title: "August-1-2015 預覽結構描述更新 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="a661d-103">Azure Logic Apps 的結構描述更新 - 2015 年 8 月 1 日預覽</span><span class="sxs-lookup"><span data-stu-id="a661d-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="a661d-104">這個新的結構描述和 Azure Logic Apps 的 API 版本包含重要的改良功能，讓邏輯應用程式更可靠且更輕鬆地使用︰</span><span class="sxs-lookup"><span data-stu-id="a661d-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="a661d-105">**APIApp** 動作類型更新為新的 [**APIConnection**](#api-connections) 動作類型。</span><span class="sxs-lookup"><span data-stu-id="a661d-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="a661d-106">**Repeat** 重新命名為 [**Foreach**](#foreach) 。</span><span class="sxs-lookup"><span data-stu-id="a661d-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="a661d-107">不再需要 [**HTTP 接聽程式** API 應用程式](#http-listener)。</span><span class="sxs-lookup"><span data-stu-id="a661d-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="a661d-108">呼叫子工作流程時使用[新的結構描述](#child-workflows)。</span><span class="sxs-lookup"><span data-stu-id="a661d-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="a661d-109">移至 API 連線</span><span class="sxs-lookup"><span data-stu-id="a661d-109">Move to API connections</span></span>

<span data-ttu-id="a661d-110">最大的改變是您不再需要將 API Apps 部署至您的 Azure 訂用帳戶，因此您可以使用 API。</span><span class="sxs-lookup"><span data-stu-id="a661d-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="a661d-111">以下是您可以使用 API 的方法︰</span><span class="sxs-lookup"><span data-stu-id="a661d-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="a661d-112">Managed API</span><span class="sxs-lookup"><span data-stu-id="a661d-112">Managed APIs</span></span>
* <span data-ttu-id="a661d-113">您自訂的 Web API</span><span class="sxs-lookup"><span data-stu-id="a661d-113">Your custom Web APIs</span></span>

<span data-ttu-id="a661d-114">每一種方式都因為其管理和裝載模型不同，而有稍微不同的處理方式。</span><span class="sxs-lookup"><span data-stu-id="a661d-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="a661d-115">此模型的優點之一是您不再受限於只能存取部署在 Azure 資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="a661d-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="a661d-116">Managed API</span><span class="sxs-lookup"><span data-stu-id="a661d-116">Managed APIs</span></span>

<span data-ttu-id="a661d-117">Microsoft 會代表您管理某些 API，例如 Office 365、Salesforce、Twitter 和 FTP。</span><span class="sxs-lookup"><span data-stu-id="a661d-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="a661d-118">您可以直接使用部分 Managed API (例如 Bing 翻譯)，有些則需要設定。</span><span class="sxs-lookup"><span data-stu-id="a661d-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="a661d-119">此組態稱為「連接」 。</span><span class="sxs-lookup"><span data-stu-id="a661d-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="a661d-120">例如，當您使用 Office 365 時，您必須建立包含 Office 365 登入權杖的連線。</span><span class="sxs-lookup"><span data-stu-id="a661d-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="a661d-121">系統會安全地儲存並重新整理此權杖，讓您的邏輯應用程式隨時都可呼叫 Office 365 API。</span><span class="sxs-lookup"><span data-stu-id="a661d-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="a661d-122">或者，如果您想要連線到 SQL 或 FTP 伺服器，您必須建立具有連接字串的連線。</span><span class="sxs-lookup"><span data-stu-id="a661d-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="a661d-123">這些動作在此定義內稱為 `APIConnection`。</span><span class="sxs-lookup"><span data-stu-id="a661d-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="a661d-124">以下是一個呼叫 Office 365 來傳送電子郵件的連接範例：</span><span class="sxs-lookup"><span data-stu-id="a661d-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

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

<span data-ttu-id="a661d-125">`host` 物件是輸入的一部分且對 API 連線是唯一的，並包含兩個部分：`api` 和 `connection`。</span><span class="sxs-lookup"><span data-stu-id="a661d-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="a661d-126">`api` 有用來裝載該 Managed API 的執行階段 URL。</span><span class="sxs-lookup"><span data-stu-id="a661d-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="a661d-127">您可以呼叫 `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`，來查看所有可供使用的 Managed API。</span><span class="sxs-lookup"><span data-stu-id="a661d-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="a661d-128">當您使用 API 時，該 API 或許定義了任何*連接參數*。</span><span class="sxs-lookup"><span data-stu-id="a661d-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="a661d-129">如果 API 並未定義，則不需任何*連接* 。</span><span class="sxs-lookup"><span data-stu-id="a661d-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="a661d-130">如果 API 定義了參數，您就必須建立連線。</span><span class="sxs-lookup"><span data-stu-id="a661d-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="a661d-131">建立的連線有您所選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="a661d-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="a661d-132">您接著會在 `host` 物件內的 `connection` 物件中參考該名稱。</span><span class="sxs-lookup"><span data-stu-id="a661d-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="a661d-133">若要在資源群組中建立連接，請呼叫：</span><span class="sxs-lookup"><span data-stu-id="a661d-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="a661d-134">使用下列主體：</span><span class="sxs-lookup"><span data-stu-id="a661d-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="a661d-135">在 Azure Resource Manager 範本中部署 Managed API</span><span class="sxs-lookup"><span data-stu-id="a661d-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="a661d-136">您可以在 Azure Resource Manager 範本中建立完整的應用程式，但前提是不需進行互動式登入。</span><span class="sxs-lookup"><span data-stu-id="a661d-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="a661d-137">如果需要登入，您可以使用 Azure Resource Manager 範本來設定所有項目，但仍然必須造訪入口網站來授權連接。</span><span class="sxs-lookup"><span data-stu-id="a661d-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

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

<span data-ttu-id="a661d-138">在此範例中，您可以看到連接只是存在於資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="a661d-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="a661d-139">它們會參考您訂用帳戶中可供使用的 Managed API。</span><span class="sxs-lookup"><span data-stu-id="a661d-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="a661d-140">您自訂的 Web API</span><span class="sxs-lookup"><span data-stu-id="a661d-140">Your custom Web APIs</span></span>

<span data-ttu-id="a661d-141">如果您使用自己的 API，不是 Microsoft 管理的 API，則應使用內建 **HTTP** 動作來呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="a661d-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="a661d-142">為了獲得理想的體驗，您應該公開您 API 的 Swagger 端點。</span><span class="sxs-lookup"><span data-stu-id="a661d-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="a661d-143">這個端點可讓邏輯應用程式設計工具呈現您 API 的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="a661d-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="a661d-144">如果沒有 Swagger，設計工具就只能將輸入和輸出顯示為不透明的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="a661d-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="a661d-145">下列範例顯示新的 `metadata.apiDefinitionUrl` 屬性：</span><span class="sxs-lookup"><span data-stu-id="a661d-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="a661d-146">如果您將 Web API 裝載於 Azure App Service 上，您的 Web API 就會自動顯示於設計工具的可用動作清單中。</span><span class="sxs-lookup"><span data-stu-id="a661d-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="a661d-147">如果不是，則您必須直接貼在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="a661d-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="a661d-148">Swagger 端點必須未經驗證，才能在邏輯應用程式設計工具內使用，雖然您可以使用 Swagger 中支援的任何方法來保護 API 本身。</span><span class="sxs-lookup"><span data-stu-id="a661d-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="a661d-149">搭配 2015-08-01-preview 呼叫已部署的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="a661d-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="a661d-150">如果您先前已部署 API 應用程式，您可以使用 **HTTP** 動作呼叫應用程式。</span><span class="sxs-lookup"><span data-stu-id="a661d-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="a661d-151">例如，如果您使用 Dropbox 列出檔案，您的 **2014-12-01-preview** 結構描述版本定義可能會有如下的內容：</span><span class="sxs-lookup"><span data-stu-id="a661d-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="a661d-152">您可以如此範例建構同等的 HTTP 動作，邏輯應用程式定義的 parameters 區段保持不變：</span><span class="sxs-lookup"><span data-stu-id="a661d-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="a661d-153">逐一解說這些屬性：</span><span class="sxs-lookup"><span data-stu-id="a661d-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="a661d-154">動作屬性</span><span class="sxs-lookup"><span data-stu-id="a661d-154">Action property</span></span> | <span data-ttu-id="a661d-155">說明</span><span class="sxs-lookup"><span data-stu-id="a661d-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="a661d-156">`Http` 而不是 `APIapp`</span><span class="sxs-lookup"><span data-stu-id="a661d-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="a661d-157">若要在邏輯應用程式設計工具中使用此動作，請包含中繼資料端點，它的建構來源是：`{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="a661d-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="a661d-158">建構來源：`{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="a661d-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="a661d-159">一律為 `POST`</span><span class="sxs-lookup"><span data-stu-id="a661d-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="a661d-160">與 API 應用程式參數相同</span><span class="sxs-lookup"><span data-stu-id="a661d-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="a661d-161">與 API 應用程式驗證相同</span><span class="sxs-lookup"><span data-stu-id="a661d-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="a661d-162">此方法應可適用於 API 應用程式的所有動作。</span><span class="sxs-lookup"><span data-stu-id="a661d-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="a661d-163">不過，請記住這些先前的 API 應用程式已不再受到支援。</span><span class="sxs-lookup"><span data-stu-id="a661d-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="a661d-164">因此，您應該移至兩個其他先前選項其中之一，受管理的 API 或裝載自訂的 Web API。</span><span class="sxs-lookup"><span data-stu-id="a661d-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="a661d-165">將 'repeat' 重新命名為 'foreach'</span><span class="sxs-lookup"><span data-stu-id="a661d-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="a661d-166">針對先前的結構描述版本，我們接到許多的客戶意見，他們覺得 **Repeat** 造成混淆，並沒有正確表達 **Repeat** 真的是 for-each 迴圈。</span><span class="sxs-lookup"><span data-stu-id="a661d-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="a661d-167">因此，我們已將 `repeat` 重新命名為 `foreach`。</span><span class="sxs-lookup"><span data-stu-id="a661d-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="a661d-168">例如，您先前可以撰寫：</span><span class="sxs-lookup"><span data-stu-id="a661d-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="a661d-169">您現在可以撰寫：</span><span class="sxs-lookup"><span data-stu-id="a661d-169">Now you would write:</span></span>

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

<span data-ttu-id="a661d-170">`@repeatItem()` 函式先前是用來參考目前反覆處理的項目。</span><span class="sxs-lookup"><span data-stu-id="a661d-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="a661d-171">此函式現已簡化為 `@item()`。</span><span class="sxs-lookup"><span data-stu-id="a661d-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="a661d-172">參考來自 'foreach' 的輸出</span><span class="sxs-lookup"><span data-stu-id="a661d-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="a661d-173">為簡化方式，從 `foreach` 的動作輸出不會包含在一個稱為 `repeatItems` 的物件。</span><span class="sxs-lookup"><span data-stu-id="a661d-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="a661d-174">雖然從先前 `repeat` 範例的輸出是︰</span><span class="sxs-lookup"><span data-stu-id="a661d-174">While the outputs from the previous `repeat` example were:</span></span>

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

<span data-ttu-id="a661d-175">現在，這些輸出為：</span><span class="sxs-lookup"><span data-stu-id="a661d-175">Now these outputs are:</span></span>

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

<span data-ttu-id="a661d-176">在以前，參考這些輸出時，若要取得動作的主體：</span><span class="sxs-lookup"><span data-stu-id="a661d-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

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

<span data-ttu-id="a661d-177">現在，您可以改為執行：</span><span class="sxs-lookup"><span data-stu-id="a661d-177">Now you can do instead:</span></span>

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

<span data-ttu-id="a661d-178">經過這些變更，已移除函式 `@repeatItem()`、`@repeatBody()` 和 `@repeatOutputs()`。</span><span class="sxs-lookup"><span data-stu-id="a661d-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="a661d-179">原生 HTTP 接聽程式</span><span class="sxs-lookup"><span data-stu-id="a661d-179">Native HTTP listener</span></span>

<span data-ttu-id="a661d-180">HTTP 接聽程式功能現在是內建的。</span><span class="sxs-lookup"><span data-stu-id="a661d-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="a661d-181">因此您不再需要部署 HTTP 接聽程式 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a661d-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="a661d-182">請參閱 [這裡有關如何讓您的邏輯應用程式端點可供呼叫的完整詳細資料](../logic-apps/logic-apps-http-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="a661d-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="a661d-183">經過這些變更，我們已移除 `@accessKeys()` 函式，改為以 `@listCallbackURL()` 函式來取得端點 (如果需要)。</span><span class="sxs-lookup"><span data-stu-id="a661d-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="a661d-184">此外，您現在必須在邏輯應用程式中至少定義一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="a661d-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="a661d-185">如果您想要 `/run` 工作流程，您必須具備下列其中一個觸發程序：`manual`、`apiConnectionWebhook` 或 `httpWebhook`。</span><span class="sxs-lookup"><span data-stu-id="a661d-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="a661d-186">呼叫子工作流程</span><span class="sxs-lookup"><span data-stu-id="a661d-186">Call child workflows</span></span>

<span data-ttu-id="a661d-187">在以前，呼叫子工作流程時必須移至該工作流程、取得存取權杖，然後將權杖貼到要呼叫該子工作流程的邏輯應用程式定義中。</span><span class="sxs-lookup"><span data-stu-id="a661d-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="a661d-188">在新的結構描述中，Logic Apps 引擎會在執行階段自動為子工作流程產生 SAS，因此您不需要將任何機密資料貼到定義中。</span><span class="sxs-lookup"><span data-stu-id="a661d-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="a661d-189">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="a661d-189">Here is an example:</span></span>

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

<span data-ttu-id="a661d-190">第二個改進是我們允許子工作流程完整存取內送要求。</span><span class="sxs-lookup"><span data-stu-id="a661d-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="a661d-191">這表示您可以將參數傳入 queries 區段和 headers 物件中，而且您可以完整定義整個主體。</span><span class="sxs-lookup"><span data-stu-id="a661d-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="a661d-192">最後是必須對子工作流程進行的變更。</span><span class="sxs-lookup"><span data-stu-id="a661d-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="a661d-193">儘管您以前可能會直接呼叫子工作流程，但現在，您必須在工作流程中定義觸發程序端點，以供父工作流程呼叫。</span><span class="sxs-lookup"><span data-stu-id="a661d-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="a661d-194">一般而言，您需要新增具有 `manual` 類型的觸發程序，然後在父定義中使用該觸發程序。</span><span class="sxs-lookup"><span data-stu-id="a661d-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="a661d-195">請注意，`host` 屬性明確地具有 `triggerName`，因為您一律需指定要叫用的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="a661d-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="a661d-196">其他變更</span><span class="sxs-lookup"><span data-stu-id="a661d-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="a661d-197">新的 'queries' 屬性</span><span class="sxs-lookup"><span data-stu-id="a661d-197">New 'queries' property</span></span>

<span data-ttu-id="a661d-198">所有動作類型現在支援一個稱為 `queries`的新輸入。</span><span class="sxs-lookup"><span data-stu-id="a661d-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="a661d-199">這個輸出可以是結構化物件，而您不必手動組合該字串。</span><span class="sxs-lookup"><span data-stu-id="a661d-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="a661d-200">將 'parse()' 函式重新命名為 'json()'</span><span class="sxs-lookup"><span data-stu-id="a661d-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="a661d-201">我們很快地將加入更多內容類型，因此已將 `parse()` 函式重新命名為 `json()`。</span><span class="sxs-lookup"><span data-stu-id="a661d-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="a661d-202">敬請期待：企業整合 API</span><span class="sxs-lookup"><span data-stu-id="a661d-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="a661d-203">我們還沒有企業整合 API 的受管理版本，像是 AS2。</span><span class="sxs-lookup"><span data-stu-id="a661d-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="a661d-204">同時，您可以透過 HTTP 動作使用現有的已部署 BizTalk API。</span><span class="sxs-lookup"><span data-stu-id="a661d-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="a661d-205">如需詳細資訊，請參閱[整合藍圖](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/)中的「使用已部署的 API 應用程式」。</span><span class="sxs-lookup"><span data-stu-id="a661d-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
