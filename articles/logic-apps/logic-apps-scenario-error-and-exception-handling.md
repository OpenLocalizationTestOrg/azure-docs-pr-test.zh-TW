---
title: "aaaException 處理與錯誤記錄的案例-Azure 邏輯應用程式 |Microsoft 文件"
description: "說明有關適用於 Azure Logic Apps 的進階例外狀況處理與錯誤記錄的實際使用案例"
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>案例︰適用於邏輯應用程式的例外狀況處理與記錄錯誤

這個案例說明如何擴充邏輯應用程式 toobetter 支援例外狀況處理。 我們使用實際的使用案例 tooanswer hello 問題: 「 Azure 邏輯應用程式支援例外狀況和錯誤處理？ 」

> [!NOTE]
> hello 目前 Azure 邏輯應用程式的結構描述會提供標準範本動作回應。 這個範本包括內部驗證和 API 應用程式所傳回的錯誤回應。

## <a name="scenario-and-use-case-overview"></a>案例和使用案例概觀

以下是 hello 劇本做為此案例中的 hello 使用案例： 

已知的醫療保健組織從事我們 toodevelop Azure 解決方案中會建立使用 Microsoft Dynamics CRM Online 的病患的入口網站。 但這需要 hello Dynamics CRM Online 病患入口網站與 Salesforce toosend 約會記錄。 我們要求 toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/)標準所有病患的記錄。

hello 專案有兩個主要需求：  

* 方法 toolog 記錄傳送 hello 從 Dynamics CRM Online 入口網站
* 方式 tooview hello 工作流程內所發生的任何錯誤

> [!TIP]
> 如需這個專案的高層級影片，請參閱[整合使用者群組](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "整合使用者群組")。

## <a name="how-we-solved-hello-problem"></a>我們如何解決 hello 問題

我們之所以選擇[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB")為 hello 記錄和錯誤記錄 （Cosmos DB 參照為文件 toorecords） 儲存機制。 因為 Azure 邏輯應用程式的標準範本的所有回應，我們沒有 toocreate 自訂結構描述。 我們無法建立 API 應用程式太**插入**和**查詢**錯誤和記錄檔記錄。 我們也可以 hello API 應用程式中每個定義結構描述。  

另一個需求是 toopurge 記錄在特定日期之後。 Cosmos DB 具有名[時間 tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "時間 tooLive") (TTL)，這允許我們 tooset**時間 tooLive**每個記錄或集合的值。 這項功能也會刪除 hello 需要 toomanually Cosmos DB 中的刪除記錄。

> [!IMPORTANT]
> toocomplete 本教學課程中，您需要 toocreate Cosmos DB 資料庫和兩個集合 （記錄和錯誤）。

## <a name="create-hello-logic-app"></a>建立 hello 邏輯應用程式

hello 第一個步驟是 toocreate hello 邏輯應用程式並在邏輯應用程式的設計工具中開啟的 hello 應用程式。 在此範例中，我們會使用父子邏輯應用程式。 假設我們已經建立 hello 父代，而且即將 toocreate 一個子邏輯應用程式。

因為我們 toolog hello 記錄傳出 Dynamics CRM Online，讓我們開始在 hello 最上方。 我們必須使用**要求**觸發，因為 hello 父邏輯應用程式會觸發此子系。

### <a name="logic-app-trigger"></a>邏輯應用程式觸發程序

我們使用**要求**觸發 hello 下列範例所示：

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a>步驟

我們必須從 hello Dynamics CRM Online 入口網站會記錄 hello 病患記錄 hello 的來源 （要求）。

1. 我們必須從 Dynamics CRM Online 取得新的預約記錄。

   來自 CRM hello 觸發程序會將我們提供 hello **CRM PatentId**，**記錄類型**，**新增或更新記錄**(新增或更新的布林值)，和**SalesforceId**。 hello **SalesforceId**可以是 null，因為它只會用更新。
   我們使用 hello CRM 取得 hello CRM 記錄**PatientID**和 hello**記錄類型**。

2. 接下來，我們需要 tooadd 我們 DocumentDB API 的應用程式**InsertLogEntry**如下所示，在邏輯應用程式的設計工具中的作業。

   **插入記錄檔項目**

   ![插入記錄檔項目](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **插入錯誤項目**

   ![插入記錄檔項目](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **檢查建立記錄失敗**

   ![條件](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>邏輯應用程式原始程式碼

> [!NOTE]
> hello 遵循範例是僅範例。 本教學課程根據現在在生產環境中實作，因為 hello 值**來源節點**可能不會顯示屬性的相關的 tooscheduling 約會。 > 

### <a name="logging"></a>記錄

hello 下列邏輯應用程式程式碼範例將示範如何 toohandle 記錄。

#### <a name="log-entry"></a>記錄檔項目

以下是 hello 邏輯應用程式原始碼來插入記錄項目。

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a>記錄檔要求

以下是 hello 記錄的要求訊息公佈 toohello API 應用程式。

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a>記錄檔回應

以下是從 hello API 應用程式的 hello 記錄回應訊息。

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

現在讓我們看看 hello 錯誤處理步驟。

### <a name="error-handling"></a>錯誤處理

hello 下列邏輯應用程式程式碼範例示範如何實作錯誤處理。

#### <a name="create-error-record"></a>建立錯誤記錄

以下是 hello 邏輯應用程式原始程式碼建立錯誤記錄。

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a>將錯誤插入至 Cosmos DB--要求

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a>將錯誤插入至 Cosmos DB--回應

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a>Salesforce 錯誤回應

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a>傳回 hello 回應後 tooparent 邏輯應用程式

您收到 hello 回應之後，您可以傳遞 hello 回應後 toohello 父邏輯應用程式。

#### <a name="return-success-response-tooparent-logic-app"></a>傳回成功回應 tooparent 邏輯應用程式

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a>傳回的錯誤回應 tooparent 邏輯應用程式

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a>Cosmos DB 存放庫和入口網站

我們的解決方案新增了含有 [Cosmos DB](https://azure.microsoft.com/services/documentdb) 的功能。

### <a name="error-management-portal"></a>錯誤管理入口網站

tooview hello 錯誤，您可以從 Cosmos DB 建立 MVC web 應用程式 toodisplay hello 錯誤記錄。 hello**清單**，**詳細資料**，**編輯**，和**刪除**hello 目前版本中包含的作業。

> [!NOTE]
> 編輯作業： Cosmos DB 取代 hello 整份文件。 hello 記錄顯示 hello**清單**和**詳細**檢視是僅範例。 而非實際的病患預約記錄。

以下是範例我們的 MVC 應用程式的詳細資料之前建立 hello 所述的方法。

#### <a name="error-management-list"></a>錯誤管理清單
![錯誤清單](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>錯誤管理詳細資料檢視
![錯誤詳細資料](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>記錄檔管理入口網站

tooview hello 記錄檔，我們也建立 MVC web 應用程式。 以下是範例我們的 MVC 應用程式的詳細資料之前建立 hello 所述的方法。

#### <a name="sample-log-detail-view"></a>範例記錄檔詳細資料檢視
![記錄檔詳細資料檢視](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>API 應用程式詳細資料

#### <a name="logic-apps-exception-management-api"></a>Logic Apps 例外狀況管理 API

我們的開放原始碼 Azure Logic Apps 例外狀況管理 API 應用程式提供了這裡所說的功能，其中有兩個控制器：

* **ErrorController** 會在 DocumentDB 集合中插入錯誤記錄 (文件)。
* **LogController** 會在 DocumentDB 集合中插入記錄檔記錄 (文件)。

> [!TIP]
> 兩個控制器使用`async Task<dynamic>`作業，因此我們可以建立，在執行階段，讓作業 tooresolve hello DocumentDB hello hello 作業主體中的結構描述。 
> 

DocumentDB 中的每個文件都必須具有唯一識別碼。 我們使用`PatientId`和加入的時間戳記轉換 tooa Unix 時間戳記值 (double)。 我們會截斷 hello 值 tooremove hello 小數的值。

您可以檢視錯誤 controller API hello 原始程式碼[從 GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs)。

我們使用 hello，請使用下列語法來呼叫 hello API 從邏輯應用程式：

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

hello 運算式在上述程式碼範例會檢查 hello *Create_NewPatientRecord*狀態**失敗**。

## <a name="summary"></a>摘要

* 您可以在邏輯應用程式中輕鬆地實作記錄和錯誤處理。
* 記錄和錯誤記錄 （文件），您可以為 hello 儲存機制使用 DocumentDB。
* 您可以使用 MVC toocreate 入口 toodisplay 記錄和錯誤記錄。

### <a name="source-code"></a>原始程式碼

hello hello Logic Apps 例外狀況管理 API 的應用程式的原始碼位於這[GitHub 儲存機制](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "邏輯應用程式例外狀況管理 API")。

## <a name="next-steps"></a>後續步驟

* [檢視更多邏輯應用程式的範例和案例](../logic-apps/logic-apps-examples-and-scenarios.md)
* [了解如何監視邏輯應用程式](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [建立邏輯應用程式的自動化部署範本](../logic-apps/logic-apps-create-deploy-template.md)
