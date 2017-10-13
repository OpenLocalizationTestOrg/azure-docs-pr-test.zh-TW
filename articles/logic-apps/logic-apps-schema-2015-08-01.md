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
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Azure Logic Apps 的結構描述更新 - 2015 年 8 月 1 日預覽

這個新的結構描述和 Azure Logic Apps 的 API 版本包含重要的改良功能，讓邏輯應用程式更可靠且更輕鬆地使用︰

*   **APIApp** 動作類型更新為新的 [**APIConnection**](#api-connections) 動作類型。
*   **Repeat** 重新命名為 [**Foreach**](#foreach) 。
*   不再需要 [**HTTP 接聽程式** API 應用程式](#http-listener)。
*   呼叫子工作流程時使用[新的結構描述](#child-workflows)。

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a>移至 API 連線

最大的改變是您不再需要將 API Apps 部署至您的 Azure 訂用帳戶，因此您可以使用 API。 以下是您可以使用 API 的方法︰

* Managed API
* 您自訂的 Web API

每一種方式都因為其管理和裝載模型不同，而有稍微不同的處理方式。 此模型的優點之一是您不再受限於只能存取部署在 Azure 資源群組中的資源。 

### <a name="managed-apis"></a>Managed API

Microsoft 會代表您管理某些 API，例如 Office 365、Salesforce、Twitter 和 FTP。 您可以直接使用部分 Managed API (例如 Bing 翻譯)，有些則需要設定。 此組態稱為「連接」 。

例如，當您使用 Office 365 時，您必須建立包含 Office 365 登入權杖的連線。 系統會安全地儲存並重新整理此權杖，讓您的邏輯應用程式隨時都可呼叫 Office 365 API。 或者，如果您想要連線到 SQL 或 FTP 伺服器，您必須建立具有連接字串的連線。 

這些動作在此定義內稱為 `APIConnection`。 以下是一個呼叫 Office 365 來傳送電子郵件的連接範例：

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

`host` 物件是輸入的一部分且對 API 連線是唯一的，並包含兩個部分：`api` 和 `connection`。

`api` 有用來裝載該 Managed API 的執行階段 URL。 您可以呼叫 `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`，來查看所有可供使用的 Managed API。

當您使用 API 時，該 API 或許定義了任何*連接參數*。 如果 API 並未定義，則不需任何*連接* 。 如果 API 定義了參數，您就必須建立連線。 建立的連線有您所選擇的名稱。 您接著會在 `host` 物件內的 `connection` 物件中參考該名稱。 若要在資源群組中建立連接，請呼叫：

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

使用下列主體：

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

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>在 Azure Resource Manager 範本中部署 Managed API

您可以在 Azure Resource Manager 範本中建立完整的應用程式，但前提是不需進行互動式登入。
如果需要登入，您可以使用 Azure Resource Manager 範本來設定所有項目，但仍然必須造訪入口網站來授權連接。 

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

在此範例中，您可以看到連接只是存在於資源群組中的資源。 它們會參考您訂用帳戶中可供使用的 Managed API。

### <a name="your-custom-web-apis"></a>您自訂的 Web API

如果您使用自己的 API，不是 Microsoft 管理的 API，則應使用內建 **HTTP** 動作來呼叫它們。 為了獲得理想的體驗，您應該公開您 API 的 Swagger 端點。 這個端點可讓邏輯應用程式設計工具呈現您 API 的輸入和輸出。 如果沒有 Swagger，設計工具就只能將輸入和輸出顯示為不透明的 JSON 物件。

下列範例顯示新的 `metadata.apiDefinitionUrl` 屬性：

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

如果您將 Web API 裝載於 Azure App Service 上，您的 Web API 就會自動顯示於設計工具的可用動作清單中。 如果不是，則您必須直接貼在 URL 中。 Swagger 端點必須未經驗證，才能在邏輯應用程式設計工具內使用，雖然您可以使用 Swagger 中支援的任何方法來保護 API 本身。

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>搭配 2015-08-01-preview 呼叫已部署的 API 應用程式

如果您先前已部署 API 應用程式，您可以使用 **HTTP** 動作呼叫應用程式。

例如，如果您使用 Dropbox 列出檔案，您的 **2014-12-01-preview** 結構描述版本定義可能會有如下的內容：

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

您可以如此範例建構同等的 HTTP 動作，邏輯應用程式定義的 parameters 區段保持不變：

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

逐一解說這些屬性：

| 動作屬性 | 說明 |
| --- | --- |
| `type` |`Http` 而不是 `APIapp` |
| `metadata.apiDefinitionUrl` |若要在邏輯應用程式設計工具中使用此動作，請包含中繼資料端點，它的建構來源是：`{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |建構來源：`{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |一律為 `POST` |
| `inputs.body` |與 API 應用程式參數相同 |
| `inputs.authentication` |與 API 應用程式驗證相同 |

此方法應可適用於 API 應用程式的所有動作。 不過，請記住這些先前的 API 應用程式已不再受到支援。 因此，您應該移至兩個其他先前選項其中之一，受管理的 API 或裝載自訂的 Web API。

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a>將 'repeat' 重新命名為 'foreach'

針對先前的結構描述版本，我們接到許多的客戶意見，他們覺得 **Repeat** 造成混淆，並沒有正確表達 **Repeat** 真的是 for-each 迴圈。 因此，我們已將 `repeat` 重新命名為 `foreach`。 例如，您先前可以撰寫：

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

您現在可以撰寫：

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

`@repeatItem()` 函式先前是用來參考目前反覆處理的項目。 此函式現已簡化為 `@item()`。 

### <a name="reference-outputs-from-foreach"></a>參考來自 'foreach' 的輸出

為簡化方式，從 `foreach` 的動作輸出不會包含在一個稱為 `repeatItems` 的物件。 雖然從先前 `repeat` 範例的輸出是︰

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

現在，這些輸出為：

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

在以前，參考這些輸出時，若要取得動作的主體：

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

現在，您可以改為執行：

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

經過這些變更，已移除函式 `@repeatItem()`、`@repeatBody()` 和 `@repeatOutputs()`。

<a name="http-listener"></a>
## <a name="native-http-listener"></a>原生 HTTP 接聽程式

HTTP 接聽程式功能現在是內建的。 因此您不再需要部署 HTTP 接聽程式 API 應用程式。 請參閱 [這裡有關如何讓您的邏輯應用程式端點可供呼叫的完整詳細資料](../logic-apps/logic-apps-http-endpoint.md)。 

經過這些變更，我們已移除 `@accessKeys()` 函式，改為以 `@listCallbackURL()` 函式來取得端點 (如果需要)。 此外，您現在必須在邏輯應用程式中至少定義一個觸發程序。 如果您想要 `/run` 工作流程，您必須具備下列其中一個觸發程序：`manual`、`apiConnectionWebhook` 或 `httpWebhook`。

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>呼叫子工作流程

在以前，呼叫子工作流程時必須移至該工作流程、取得存取權杖，然後將權杖貼到要呼叫該子工作流程的邏輯應用程式定義中。 在新的結構描述中，Logic Apps 引擎會在執行階段自動為子工作流程產生 SAS，因此您不需要將任何機密資料貼到定義中。 下列是一個範例：

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

第二個改進是我們允許子工作流程完整存取內送要求。 這表示您可以將參數傳入 queries 區段和 headers 物件中，而且您可以完整定義整個主體。

最後是必須對子工作流程進行的變更。 儘管您以前可能會直接呼叫子工作流程，但現在，您必須在工作流程中定義觸發程序端點，以供父工作流程呼叫。 一般而言，您需要新增具有 `manual` 類型的觸發程序，然後在父定義中使用該觸發程序。 請注意，`host` 屬性明確地具有 `triggerName`，因為您一律需指定要叫用的觸發程序。

## <a name="other-changes"></a>其他變更

### <a name="new-queries-property"></a>新的 'queries' 屬性

所有動作類型現在支援一個稱為 `queries`的新輸入。 這個輸出可以是結構化物件，而您不必手動組合該字串。

### <a name="renamed-parse-function-to-json"></a>將 'parse()' 函式重新命名為 'json()'

我們很快地將加入更多內容類型，因此已將 `parse()` 函式重新命名為 `json()`。

## <a name="coming-soon-enterprise-integration-apis"></a>敬請期待：企業整合 API

我們還沒有企業整合 API 的受管理版本，像是 AS2。 同時，您可以透過 HTTP 動作使用現有的已部署 BizTalk API。 如需詳細資訊，請參閱[整合藍圖](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/)中的「使用已部署的 API 應用程式」。 
