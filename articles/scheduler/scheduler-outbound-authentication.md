---
title: "aaaScheduler 輸出驗證"
description: "排程器輸出驗證"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a>排程器輸出驗證
排程器作業可能需要 toocall 出 tooservices 需要驗證。 如此一來，被呼叫的服務可以判斷是否 hello 排程器工作可以存取它的資源。 其中某些服務包括其他 Azure 服務、Salesforce.com、Facebook 和安全的自訂網站。

## <a name="adding-and-removing-authentication"></a>新增和移除驗證
加入驗證 tooa 排程器工作很簡單 – 將 JSON 子項目`authentication`toohello`request`時建立或更新工作項目。 密碼的 hello 一部分在 PUT、 PATCH 或 POST 要求 – 傳送 toohello 排程器服務`authentication`物件 – 永遠不會在回應中傳回。 在回應中，密碼資訊設定 toonull，或可能具有代表 hello 驗證實體的公開金鑰語彙基元。

tooremove 驗證、 PUT 或 PATCH hello 作業明確地設定 hello `authentication` toonull 的物件。 您將不會看到回應中傳回的任何驗證屬性。

目前，hello 僅支援驗證類型是 hello`ClientCertificate`模型 （適用於使用 hello SSL/TLS 用戶端憑證）、 hello`Basic`模型 （適用於基本驗證），然後 hello`ActiveDirectoryOAuth`模型 （適用於 Active Directory OAuth驗證）。

## <a name="request-body-for-clientcertificate-authentication"></a>ClientCertificate 驗證的要求本文
加入使用 hello 驗證時`ClientCertificate`模型中，指定下列額外的項目 hello 要求主體中的 hello。  

| 元素 | 說明 |
|:--- |:--- |
| *authentication (父元素)* |使用 SSL 用戶端憑證的驗證物件。 |
| *type* |必要。 驗證類型。SSL 用戶端憑證，hello 值必須是`ClientCertificate`。 |
| *pfx* |必要。 Hello PFX 檔案的 Base64 編碼內容。 |
| *password* |必要。 密碼 tooaccess hello PFX 檔案。 |

## <a name="response-body-for-clientcertificate-authentication"></a>ClientCertificate 驗證的回應本文
當使用驗證資訊會傳送要求時，hello 回應會包含 hello 遵循驗證相關的項目。

| 元素 | 說明 |
|:--- |:--- |
| *authentication (父元素)* |使用 SSL 用戶端憑證的驗證物件。 |
| *type* |驗證類型。 SSL 用戶端憑證，hello 值是`ClientCertificate`。 |
| *certificateThumbprint* |hello hello 憑證指紋。 |
| *certificateSubjectName* |hello 主體辨別的名稱 hello 憑證。 |
| *certificateExpiration* |hello hello 憑證的到期日。 |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>ClientCertificate 驗證的範例 REST 要求
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>ClientCertificate 驗證的範例 REST 回應
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a>基本驗證的要求本文
加入使用 hello 驗證時`Basic`模型中，指定下列額外的項目 hello 要求主體中的 hello。

| 元素 | 說明 |
|:--- |:--- |
| *authentication (父元素)* |使用基本驗證的驗證物件。 |
| *type* |必要。 驗證類型。 Hello 值必須是基本驗證， `Basic`。 |
| *username* |必要。 使用者名稱 tooauthenticate。 |
| *password* |必要。 密碼 tooauthenticate。 |

## <a name="response-body-for-basic-authentication"></a>基本驗證的回應本文
當使用驗證資訊會傳送要求時，hello 回應會包含 hello 遵循驗證相關的項目。

| 元素 | 說明 |
|:--- |:--- |
| *authentication (父元素)* |使用基本驗證的驗證物件。 |
| *type* |驗證類型。 基本驗證 hello 值是`Basic`。 |
| *username* |hello 驗證使用者名稱。 |

## <a name="sample-rest-request-for-basic-authentication"></a>基本驗證的範例 REST 要求
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a>基本驗證的範例 REST 回應
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth 驗證的要求本文
加入使用 hello 驗證時`ActiveDirectoryOAuth`模型中，指定下列額外的項目 hello 要求主體中的 hello。

| 元素 | 說明 |
|:--- |:--- |
| *authentication (父元素)* |使用 ActiveDirectoryOAuth 驗證的驗證物件。 |
| *type* |必要。 驗證類型。 ActiveDirectoryOAuth 驗證的 hello 值必須是`ActiveDirectoryOAuth`。 |
| *tenant* |必要。 hello hello Azure AD 租用戶的租用戶識別碼。 |
| *audience* |必要。 這會設定 toohttps://management.core.windows.net/。 |
| *clientId* |必要。 Hello Azure AD 應用程式提供 hello 用戶端識別碼。 |
| *secret* |必要。 正在要求 hello 語彙基元的 hello 用戶端的密碼。 |

### <a name="determining-your-tenant-identifier"></a>判斷您的租用戶識別碼
您可以執行，以尋找 hello hello Azure AD 租用戶的租用戶識別碼`Get-AzureAccount`Azure PowerShell 中。

## <a name="response-body-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth 驗證的回應本文
當使用驗證資訊會傳送要求時，hello 回應會包含 hello 遵循驗證相關的項目。

| 元素 | 說明 |
|:--- |:--- |
| *authentication (父元素)* |使用 ActiveDirectoryOAuth 驗證的驗證物件。 |
| *type* |驗證類型。 ActiveDirectoryOAuth 驗證的 hello 值是`ActiveDirectoryOAuth`。 |
| *tenant* |hello hello Azure AD 租用戶的租用戶識別碼。 |
| *audience* |這會設定 toohttps://management.core.windows.net/。 |
| *clientId* |hello hello Azure AD 應用程式的用戶端識別項。 |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth 驗證的範例 REST 要求
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>ActiveDirectoryOAuth 驗證的範例 REST 回應
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a>另請參閱
 [排程器是什麼？](scheduler-intro.md)

 [Azure 排程器概念、術語及實體階層](scheduler-concepts-terms.md)

 [開始在 hello Azure 入口網站中使用排程器](scheduler-get-started-portal.md)

 [Azure 排程器的計劃和計費](scheduler-plans-billing.md)

 [Azure 排程器 REST API 參考](https://msdn.microsoft.com/library/mt629143)

 [Azure 排程器 PowerShell Cmdlet 參考](scheduler-powershell-reference.md)

 [Azure 排程器高可用性和可靠性](scheduler-high-availability-reliability.md)

 [Azure 排程器限制、預設值和錯誤碼](scheduler-limits-defaults-errors.md)

