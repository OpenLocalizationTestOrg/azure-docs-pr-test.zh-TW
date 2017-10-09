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
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Azure Logic Apps 的結構描述更新 - 2015 年 8 月 1 日預覽

這個新的結構描述和 API 版本 Azure 邏輯應用程式包含多個製作邏輯應用程式的重要改良 toouse 可靠且更容易：

*   hello **APIApp**動作類型是新的更新的 tooa [ **APIConnection** ](#api-connections)動作類型。
*   **重複**重新命名過[**Foreach**](#foreach)。
*   hello [ **HTTP 接聽程式**API 應用程式](#http-listener)已不再需要。
*   呼叫子工作流程時使用[新的結構描述](#child-workflows)。

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>移動 tooAPI 連線

hello 最大變更是，您不再需要 toodeploy API 應用程式到您的 Azure 訂閱，您可以使用 Api。 以下是您可以使用 Api 的 hello 方法：

* Managed API
* 您自訂的 Web API

每一種方式都因為其管理和裝載模型不同，而有稍微不同的處理方式。 此模型中的其中一個優點是您不再限制 tooresources 部署在 Azure 資源群組中。 

### <a name="managed-apis"></a>Managed API

Microsoft 會代表您管理某些 API，例如 Office 365、Salesforce、Twitter 和 FTP。 您可以直接使用部分 Managed API (例如 Bing 翻譯)，有些則需要設定。 此組態稱為「連接」 。

例如，當您使用 Office 365 時，您必須建立包含 Office 365 登入權杖的連線。 這個語彙基元會安全地儲存，並重新整理可讓您的邏輯應用程式一律呼叫 hello Office 365 API。 或者，如果您希望 tooconnect tooyour SQL 或 FTP 伺服器時，您必須建立具有 hello 連接字串的連接。 

這些動作在此定義內稱為 `APIConnection`。 呼叫 Office 365 toosend 電子郵件連線的範例如下：

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

hello`host`物件是輸入部分的唯一 tooAPI 連線，且包含具有組件：`api`和`connection`。

hello`api`具有 hello 執行階段裝載的受管理應用程式開發介面的 URL。 您可以查看所有可用的 hello 藉由呼叫 managed Api `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`。

當您使用應用程式開發介面時，hello API 可能會或可能不含任何*連接參數*定義。 Hello 應用程式開發介面不是，如果沒有*連接*需要。 如果 hello API，您必須建立連接。 建立 hello 連接都有您所選擇的 hello 名稱。 您再參考 hello 中的 hello 名稱`connection`物件內 hello`host`物件。 toocreate 在資源群組中，呼叫的連接：

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

以 hello 下列主體：

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

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>在 Azure Resource Manager 範本中部署 Managed API

您可以在 Azure Resource Manager 範本中建立完整的應用程式，但前提是不需進行互動式登入。
如果登入需要，您可以設定 hello Azure Resource Manager 範本時，所有項目，不過您仍然需要 toovisit hello 入口 tooauthorize hello 連線。 

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

您可以看到在這個範例 hello 連線是只存在於資源群組的資源。 事件所參考 hello 受管理應用程式開發介面使用 tooyou 您訂用帳戶中。

### <a name="your-custom-web-apis"></a>您自訂的 Web API

如果您使用您自己的 Api，不受 Microsoft 管理的項目，使用內建的 hello **HTTP**動作 toocall 它們。 為了獲得理想的體驗，您應該公開您 API 的 Swagger 端點。 此端點可讓 hello 邏輯應用程式的設計工具 toorender hello 輸入，而且您 API 的輸出。 沒有 Swagger，hello 設計工具可以只顯示 hello 輸入及輸出為不透明的 JSON 物件。

以下是範例顯示 hello 新`metadata.apiDefinitionUrl`屬性：

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

如果您裝載您的 Web API，Azure App Service 上，您的 Web API 就會自動出現在 hello hello 設計工具中可用動作清單中。 如果沒有，您在 toopaste hello URL 直接。 hello Swagger 端點必須是可 hello 邏輯應用程式的設計工具，用於未經驗證的 toobe，雖然您可以保護任何 Swagger 所支援的方法與 hello API 本身。

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>搭配 2015-08-01-preview 呼叫已部署的 API 應用程式

如果您先前部署 API 應用程式，您可以呼叫 hello 應用程式以 hello **HTTP**動作。

例如，如果您使用 Dropbox toolist 檔案，您**2014年-12-01-預覽**結構描述版本定義可能像這樣：

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

Hello 的 hello 邏輯應用程式定義的參數區段保持不變時，您可以建構等此範例中，hello 相等 HTTP 動作：

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
| `metadata.apiDefinitionUrl` |toouse hello 邏輯應用程式的設計工具，這個動作包括 hello 中繼資料端點，建構自：`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |建構來源：`{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |一律為 `POST` |
| `inputs.body` |相同 toohello API 應用程式參數 |
| `inputs.authentication` |相同 toohello API 應用程式驗證 |

此方法應可適用於 API 應用程式的所有動作。 不過，請記住這些先前的 API 應用程式已不再受到支援。 因此您應該一併移動的 hello tooone 上述兩個其他選項，受管理的應用程式開發介面或裝載您自訂的 Web API。

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>重新命名 'repeat' too'foreach'

Hello 先前的結構描述版本，我們收到太多客戶的意見反應，**重複**會造成混淆並沒有正確擷取的**重複**真的 for each 迴圈。 如此一來，我們已重新命名`repeat`太`foreach`。 例如，您先前可以撰寫：

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

hello 函式`@repeatItem()`先前使用的 tooreference hello 目前項目要反覆查看。 此函式現在已簡化太`@item()`。 

### <a name="reference-outputs-from-foreach"></a>參考來自 'foreach' 的輸出

為簡化，hello 輸出從`foreach`動作不會包含在一個稱為物件`repeatItems`。 雖然 hello 輸出從先前的 hello`repeat`範例是：

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

先前，tooget toohello 本文的 hello 參照這些輸出的動作：

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

這些變更，hello 函式`@repeatItem()`， `@repeatBody()`，和`@repeatOutputs()`會移除。

<a name="http-listener"></a>
## <a name="native-http-listener"></a>原生 HTTP 接聽程式

hello 功能現在內建的 HTTP 接聽程式。 因此您不再需要 toodeploy HTTP 接聽程式的 API 應用程式。 請參閱[hello 完整詳細資料的方式 toomake 您邏輯應用程式端點可呼叫這裡](../logic-apps/logic-apps-http-endpoint.md)。 

這些變更，我們移除了 hello`@accessKeys()`函式，我們取代 hello`@listCallbackURL()`取得 hello 端點時所需的函式。 此外，您現在必須在邏輯應用程式中至少定義一個觸發程序。 如果您想太`/run`hello 工作流程，您必須擁有這些觸發程序的其中一個： `manual`， `apiConnectionWebhook`，或`httpWebhook`。

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>呼叫子工作流程

之前，呼叫子工作流程，您必須將 toohello 工作流程中，取得 hello 存取權杖，並貼上 hello 語彙基元中您想要 toocall hello 邏輯應用程式定義的子工作流程。 與 hello 新結構描述，引擎會自動產生 SAS，以在執行階段針對 hello Logic Apps 讓您不要有太貼上任何機密 hello 定義 hello 子工作流程。 下列是一個範例：

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

第二個改進是我們會賦予 hello 子工作流程的完整存取 toohello 連入要求。 這表示您可以在 hello 傳遞參數*查詢*區段在 hello*標頭*物件，而且您可以完全定義 hello 整個本文。

最後，有必要的變更 toohello 子工作流程。 雖然您無法直接先前呼叫的子工作流程，您現在必須定義觸發程序端點 hello 父 toocall 的 hello 工作流程中。 一般而言，您可以在其中加入觸發程序具有`manual`類型，而然後 hello 父定義中使用該觸發程序。 請注意 hello`host`屬性特別的是包含`triggerName`您一定要指定觸發程序，因為您叫用。

## <a name="other-changes"></a>其他變更

### <a name="new-queries-property"></a>新的 'queries' 屬性

所有動作類型現在支援一個稱為 `queries`的新輸入。 此輸入可以是結構化的物件，而不是您以手動方式具有 tooassemble hello 字串。

### <a name="renamed-parse-function-toojson"></a>重新命名 'parse()' 函式 too'json()'

我們要加入更多的內容類型過期，因此我們在重新命名 hello`parse()`函式太`json()`。

## <a name="coming-soon-enterprise-integration-apis"></a>敬請期待：企業整合 API

我們沒有 hello 企業整合應用程式開發介面，例如 AS2 的受管理的版本。 同時，您可以使用您現有部署的 BizTalk 應用程式開發介面透過 hello HTTP 動作。 如需詳細資訊，請參閱 「 使用您已部署的應用程式開發介面應用程式 」 在 hello[整合藍圖](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/)。 
