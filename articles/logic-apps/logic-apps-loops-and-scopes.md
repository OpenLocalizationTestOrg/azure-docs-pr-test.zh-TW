---
title: "aaaCreate 迴圈和範圍，或 debatch 中工作流程-Azure 邏輯應用程式資料 |Microsoft 文件"
description: "建立動作群組成範圍的資料，透過迴圈 tooiterate 或 debatch 資料 toostart Azure 邏輯應用程式中的多個工作流程。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a>Logic Apps 迴圈、範圍和解除批次處理
  
邏輯應用程式提供方式 toowork 陣列、 集合、 批次，與工作流程內迴圈的數目。
  
## <a name="foreach-loop-and-arrays"></a>ForEach 迴圈和陣列
  
邏輯應用程式可讓您對資料集的 tooloop 和每個項目執行的動作。  這是可透過 hello`foreach`動作。  在 hello 設計工具中，您可以指定 tooadd for each 迴圈。  選取您想 tooiterate 透過 hello 陣列之後, 您就可以開始加入動作。  您目前是有限的 tooonly 一個動作，每個 「 foreach 迴圈 」，但 hello 即將週中，將會提高此限制。  一次 hello 迴圈中，您可以開始的 toospecify 應該會發生什麼在 hello 陣列的每個值。

如果使用程式碼檢視，您就可以指定 for each 迴圈，如下所示。  這是 for each 迴圈的範例，可針對每個包含「microsoft.com」的電子郵件地址傳送傳送電子郵件︰

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  A`foreach`動作可以逐一查看 too5，000 資料列組成的陣列。  預設會平行執行每個反覆運算。  

### <a name="sequential-foreach-loops"></a>循序 ForEach 迴圈

foreach 迴圈 tooexecute 循序 hello 的 tooenable`Sequential`應加入作業選項。

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Until 迴圈
  
  您可以執行某個動作或一系列動作，直到符合某個條件為止。  hello 最常見的案例呼叫端點直到取得所需的 hello 回應。  在 hello 設計工具中，您可以指定 tooadd until 迴圈。  在新增之後 hello 迴圈內的動作，您可以設定 hello 結束條件，以及 hello 迴圈限制。  迴圈循環之間有 1 分鐘的延遲。
  
  如果使用程式碼檢視，您可以指定 until 迴圈，如下所示。  這是呼叫的 HTTP 端點，直到 hello 值 'Completed' hello 回應主體的範例。  它將會在符合下列其中一種情況時完成 
  
  * HTTP 回應具有「已完成」的狀態
  * 已嘗試 1 小時的時間
  * 已執行過 100 次的迴圈
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a>SplitOn 和解除批次處理

有時觸發程序可能會收到項目，toodebatch 並啟動工作流程，每個項目的陣列。  這可以透過 hello 完成`spliton`命令。  根據預設，如果您的觸發程序 Swagger 指定的承載是一個陣列，即會新增 `spliton` ，並針對每個項目開始執行。  SplitOn 只能加入 tooa 觸發程序。  這可以在定義程式碼檢視中手動設定或覆寫。  目前 SplitOn 可以 debatch too5，000 項目組成的陣列。  您不能有`spliton`和也實作 hello 同步回應模式。  呼叫的任何工作流程具有`response`此外動作太`spliton`會以非同步方式執行，並傳送立即`202 Accepted`回應。  

SplitOn 可以指定程式碼檢視中，為下列範例中的 hello。  這會收到項目陣列，並在每一列上解除批次處理。

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a>範圍

很可能 toogroup 一系列動作一起使用的範圍。  這特別適合用來實作例外狀況處理。  Hello 設計工具中，您可以加入新的領域，並開始新增在其內部的任何動作。  您可以在 hello 如下的程式碼檢視中定義範圍：


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```