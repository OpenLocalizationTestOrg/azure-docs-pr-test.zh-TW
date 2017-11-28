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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="b68bb-103">案例︰適用於邏輯應用程式的例外狀況處理與記錄錯誤</span><span class="sxs-lookup"><span data-stu-id="b68bb-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="b68bb-104">這個案例說明如何擴充邏輯應用程式 toobetter 支援例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="b68bb-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="b68bb-105">我們使用實際的使用案例 tooanswer hello 問題: 「 Azure 邏輯應用程式支援例外狀況和錯誤處理？ 」</span><span class="sxs-lookup"><span data-stu-id="b68bb-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="b68bb-106">hello 目前 Azure 邏輯應用程式的結構描述會提供標準範本動作回應。</span><span class="sxs-lookup"><span data-stu-id="b68bb-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="b68bb-107">這個範本包括內部驗證和 API 應用程式所傳回的錯誤回應。</span><span class="sxs-lookup"><span data-stu-id="b68bb-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="b68bb-108">案例和使用案例概觀</span><span class="sxs-lookup"><span data-stu-id="b68bb-108">Scenario and use case overview</span></span>

<span data-ttu-id="b68bb-109">以下是 hello 劇本做為此案例中的 hello 使用案例：</span><span class="sxs-lookup"><span data-stu-id="b68bb-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="b68bb-110">已知的醫療保健組織從事我們 toodevelop Azure 解決方案中會建立使用 Microsoft Dynamics CRM Online 的病患的入口網站。</span><span class="sxs-lookup"><span data-stu-id="b68bb-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="b68bb-111">但這需要 hello Dynamics CRM Online 病患入口網站與 Salesforce toosend 約會記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="b68bb-112">我們要求 toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/)標準所有病患的記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="b68bb-113">hello 專案有兩個主要需求：</span><span class="sxs-lookup"><span data-stu-id="b68bb-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="b68bb-114">方法 toolog 記錄傳送 hello 從 Dynamics CRM Online 入口網站</span><span class="sxs-lookup"><span data-stu-id="b68bb-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="b68bb-115">方式 tooview hello 工作流程內所發生的任何錯誤</span><span class="sxs-lookup"><span data-stu-id="b68bb-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="b68bb-116">如需這個專案的高層級影片，請參閱[整合使用者群組](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "整合使用者群組")。</span><span class="sxs-lookup"><span data-stu-id="b68bb-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="b68bb-117">我們如何解決 hello 問題</span><span class="sxs-lookup"><span data-stu-id="b68bb-117">How we solved hello problem</span></span>

<span data-ttu-id="b68bb-118">我們之所以選擇[Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB")為 hello 記錄和錯誤記錄 （Cosmos DB 參照為文件 toorecords） 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b68bb-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="b68bb-119">因為 Azure 邏輯應用程式的標準範本的所有回應，我們沒有 toocreate 自訂結構描述。</span><span class="sxs-lookup"><span data-stu-id="b68bb-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="b68bb-120">我們無法建立 API 應用程式太**插入**和**查詢**錯誤和記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="b68bb-121">我們也可以 hello API 應用程式中每個定義結構描述。</span><span class="sxs-lookup"><span data-stu-id="b68bb-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="b68bb-122">另一個需求是 toopurge 記錄在特定日期之後。</span><span class="sxs-lookup"><span data-stu-id="b68bb-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="b68bb-123">Cosmos DB 具有名[時間 tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "時間 tooLive") (TTL)，這允許我們 tooset**時間 tooLive**每個記錄或集合的值。</span><span class="sxs-lookup"><span data-stu-id="b68bb-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="b68bb-124">這項功能也會刪除 hello 需要 toomanually Cosmos DB 中的刪除記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b68bb-125">toocomplete 本教學課程中，您需要 toocreate Cosmos DB 資料庫和兩個集合 （記錄和錯誤）。</span><span class="sxs-lookup"><span data-stu-id="b68bb-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="b68bb-126">建立 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b68bb-126">Create hello logic app</span></span>

<span data-ttu-id="b68bb-127">hello 第一個步驟是 toocreate hello 邏輯應用程式並在邏輯應用程式的設計工具中開啟的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68bb-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="b68bb-128">在此範例中，我們會使用父子邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68bb-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="b68bb-129">假設我們已經建立 hello 父代，而且即將 toocreate 一個子邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68bb-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="b68bb-130">因為我們 toolog hello 記錄傳出 Dynamics CRM Online，讓我們開始在 hello 最上方。</span><span class="sxs-lookup"><span data-stu-id="b68bb-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="b68bb-131">我們必須使用**要求**觸發，因為 hello 父邏輯應用程式會觸發此子系。</span><span class="sxs-lookup"><span data-stu-id="b68bb-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="b68bb-132">邏輯應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="b68bb-132">Logic app trigger</span></span>

<span data-ttu-id="b68bb-133">我們使用**要求**觸發 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="b68bb-133">We are using a **Request** trigger as shown in hello following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="b68bb-134">步驟</span><span class="sxs-lookup"><span data-stu-id="b68bb-134">Steps</span></span>

<span data-ttu-id="b68bb-135">我們必須從 hello Dynamics CRM Online 入口網站會記錄 hello 病患記錄 hello 的來源 （要求）。</span><span class="sxs-lookup"><span data-stu-id="b68bb-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="b68bb-136">我們必須從 Dynamics CRM Online 取得新的預約記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="b68bb-137">來自 CRM hello 觸發程序會將我們提供 hello **CRM PatentId**，**記錄類型**，**新增或更新記錄**(新增或更新的布林值)，和**SalesforceId**。</span><span class="sxs-lookup"><span data-stu-id="b68bb-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="b68bb-138">hello **SalesforceId**可以是 null，因為它只會用更新。</span><span class="sxs-lookup"><span data-stu-id="b68bb-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="b68bb-139">我們使用 hello CRM 取得 hello CRM 記錄**PatientID**和 hello**記錄類型**。</span><span class="sxs-lookup"><span data-stu-id="b68bb-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="b68bb-140">接下來，我們需要 tooadd 我們 DocumentDB API 的應用程式**InsertLogEntry**如下所示，在邏輯應用程式的設計工具中的作業。</span><span class="sxs-lookup"><span data-stu-id="b68bb-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="b68bb-141">**插入記錄檔項目**</span><span class="sxs-lookup"><span data-stu-id="b68bb-141">**Insert log entry**</span></span>

   ![插入記錄檔項目](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="b68bb-143">**插入錯誤項目**</span><span class="sxs-lookup"><span data-stu-id="b68bb-143">**Insert error entry**</span></span>

   ![插入記錄檔項目](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="b68bb-145">**檢查建立記錄失敗**</span><span class="sxs-lookup"><span data-stu-id="b68bb-145">**Check for create record failure**</span></span>

   ![條件](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="b68bb-147">邏輯應用程式原始程式碼</span><span class="sxs-lookup"><span data-stu-id="b68bb-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="b68bb-148">hello 遵循範例是僅範例。</span><span class="sxs-lookup"><span data-stu-id="b68bb-148">hello following examples are samples only.</span></span> <span data-ttu-id="b68bb-149">本教學課程根據現在在生產環境中實作，因為 hello 值**來源節點**可能不會顯示屬性的相關的 tooscheduling 約會。 ></span><span class="sxs-lookup"><span data-stu-id="b68bb-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="b68bb-150">記錄</span><span class="sxs-lookup"><span data-stu-id="b68bb-150">Logging</span></span>

<span data-ttu-id="b68bb-151">hello 下列邏輯應用程式程式碼範例將示範如何 toohandle 記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="b68bb-152">記錄檔項目</span><span class="sxs-lookup"><span data-stu-id="b68bb-152">Log entry</span></span>

<span data-ttu-id="b68bb-153">以下是 hello 邏輯應用程式原始碼來插入記錄項目。</span><span class="sxs-lookup"><span data-stu-id="b68bb-153">Here is hello logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="b68bb-154">記錄檔要求</span><span class="sxs-lookup"><span data-stu-id="b68bb-154">Log request</span></span>

<span data-ttu-id="b68bb-155">以下是 hello 記錄的要求訊息公佈 toohello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68bb-155">Here is hello log request message posted toohello API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="b68bb-156">記錄檔回應</span><span class="sxs-lookup"><span data-stu-id="b68bb-156">Log response</span></span>

<span data-ttu-id="b68bb-157">以下是從 hello API 應用程式的 hello 記錄回應訊息。</span><span class="sxs-lookup"><span data-stu-id="b68bb-157">Here is hello log response message from hello API app.</span></span>

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

<span data-ttu-id="b68bb-158">現在讓我們看看 hello 錯誤處理步驟。</span><span class="sxs-lookup"><span data-stu-id="b68bb-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="b68bb-159">錯誤處理</span><span class="sxs-lookup"><span data-stu-id="b68bb-159">Error handling</span></span>

<span data-ttu-id="b68bb-160">hello 下列邏輯應用程式程式碼範例示範如何實作錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="b68bb-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="b68bb-161">建立錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="b68bb-161">Create error record</span></span>

<span data-ttu-id="b68bb-162">以下是 hello 邏輯應用程式原始程式碼建立錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-162">Here is hello logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="b68bb-163">將錯誤插入至 Cosmos DB--要求</span><span class="sxs-lookup"><span data-stu-id="b68bb-163">Insert error into Cosmos DB--request</span></span>

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

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="b68bb-164">將錯誤插入至 Cosmos DB--回應</span><span class="sxs-lookup"><span data-stu-id="b68bb-164">Insert error into Cosmos DB--response</span></span>

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

#### <a name="salesforce-error-response"></a><span data-ttu-id="b68bb-165">Salesforce 錯誤回應</span><span class="sxs-lookup"><span data-stu-id="b68bb-165">Salesforce error response</span></span>

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

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="b68bb-166">傳回 hello 回應後 tooparent 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b68bb-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="b68bb-167">您收到 hello 回應之後，您可以傳遞 hello 回應後 toohello 父邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68bb-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="b68bb-168">傳回成功回應 tooparent 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b68bb-168">Return success response tooparent logic app</span></span>

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

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="b68bb-169">傳回的錯誤回應 tooparent 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b68bb-169">Return error response tooparent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="b68bb-170">Cosmos DB 存放庫和入口網站</span><span class="sxs-lookup"><span data-stu-id="b68bb-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="b68bb-171">我們的解決方案新增了含有 [Cosmos DB](https://azure.microsoft.com/services/documentdb) 的功能。</span><span class="sxs-lookup"><span data-stu-id="b68bb-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="b68bb-172">錯誤管理入口網站</span><span class="sxs-lookup"><span data-stu-id="b68bb-172">Error management portal</span></span>

<span data-ttu-id="b68bb-173">tooview hello 錯誤，您可以從 Cosmos DB 建立 MVC web 應用程式 toodisplay hello 錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="b68bb-174">hello**清單**，**詳細資料**，**編輯**，和**刪除**hello 目前版本中包含的作業。</span><span class="sxs-lookup"><span data-stu-id="b68bb-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="b68bb-175">編輯作業： Cosmos DB 取代 hello 整份文件。</span><span class="sxs-lookup"><span data-stu-id="b68bb-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="b68bb-176">hello 記錄顯示 hello**清單**和**詳細**檢視是僅範例。</span><span class="sxs-lookup"><span data-stu-id="b68bb-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="b68bb-177">而非實際的病患預約記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="b68bb-178">以下是範例我們的 MVC 應用程式的詳細資料之前建立 hello 所述的方法。</span><span class="sxs-lookup"><span data-stu-id="b68bb-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="b68bb-179">錯誤管理清單</span><span class="sxs-lookup"><span data-stu-id="b68bb-179">Error management list</span></span>
![錯誤清單](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="b68bb-181">錯誤管理詳細資料檢視</span><span class="sxs-lookup"><span data-stu-id="b68bb-181">Error management detail view</span></span>
![錯誤詳細資料](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="b68bb-183">記錄檔管理入口網站</span><span class="sxs-lookup"><span data-stu-id="b68bb-183">Log management portal</span></span>

<span data-ttu-id="b68bb-184">tooview hello 記錄檔，我們也建立 MVC web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b68bb-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="b68bb-185">以下是範例我們的 MVC 應用程式的詳細資料之前建立 hello 所述的方法。</span><span class="sxs-lookup"><span data-stu-id="b68bb-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="b68bb-186">範例記錄檔詳細資料檢視</span><span class="sxs-lookup"><span data-stu-id="b68bb-186">Sample log detail view</span></span>
![記錄檔詳細資料檢視](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="b68bb-188">API 應用程式詳細資料</span><span class="sxs-lookup"><span data-stu-id="b68bb-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="b68bb-189">Logic Apps 例外狀況管理 API</span><span class="sxs-lookup"><span data-stu-id="b68bb-189">Logic Apps exception management API</span></span>

<span data-ttu-id="b68bb-190">我們的開放原始碼 Azure Logic Apps 例外狀況管理 API 應用程式提供了這裡所說的功能，其中有兩個控制器：</span><span class="sxs-lookup"><span data-stu-id="b68bb-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="b68bb-191">**ErrorController** 會在 DocumentDB 集合中插入錯誤記錄 (文件)。</span><span class="sxs-lookup"><span data-stu-id="b68bb-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="b68bb-192">**LogController** 會在 DocumentDB 集合中插入記錄檔記錄 (文件)。</span><span class="sxs-lookup"><span data-stu-id="b68bb-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="b68bb-193">兩個控制器使用`async Task<dynamic>`作業，因此我們可以建立，在執行階段，讓作業 tooresolve hello DocumentDB hello hello 作業主體中的結構描述。</span><span class="sxs-lookup"><span data-stu-id="b68bb-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="b68bb-194">DocumentDB 中的每個文件都必須具有唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="b68bb-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="b68bb-195">我們使用`PatientId`和加入的時間戳記轉換 tooa Unix 時間戳記值 (double)。</span><span class="sxs-lookup"><span data-stu-id="b68bb-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="b68bb-196">我們會截斷 hello 值 tooremove hello 小數的值。</span><span class="sxs-lookup"><span data-stu-id="b68bb-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="b68bb-197">您可以檢視錯誤 controller API hello 原始程式碼[從 GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs)。</span><span class="sxs-lookup"><span data-stu-id="b68bb-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="b68bb-198">我們使用 hello，請使用下列語法來呼叫 hello API 從邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="b68bb-198">We call hello API from a logic app by using hello following syntax:</span></span>

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

<span data-ttu-id="b68bb-199">hello 運算式在上述程式碼範例會檢查 hello *Create_NewPatientRecord*狀態**失敗**。</span><span class="sxs-lookup"><span data-stu-id="b68bb-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="b68bb-200">摘要</span><span class="sxs-lookup"><span data-stu-id="b68bb-200">Summary</span></span>

* <span data-ttu-id="b68bb-201">您可以在邏輯應用程式中輕鬆地實作記錄和錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="b68bb-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="b68bb-202">記錄和錯誤記錄 （文件），您可以為 hello 儲存機制使用 DocumentDB。</span><span class="sxs-lookup"><span data-stu-id="b68bb-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="b68bb-203">您可以使用 MVC toocreate 入口 toodisplay 記錄和錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="b68bb-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="b68bb-204">原始程式碼</span><span class="sxs-lookup"><span data-stu-id="b68bb-204">Source code</span></span>

<span data-ttu-id="b68bb-205">hello hello Logic Apps 例外狀況管理 API 的應用程式的原始碼位於這[GitHub 儲存機制](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "邏輯應用程式例外狀況管理 API")。</span><span class="sxs-lookup"><span data-stu-id="b68bb-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="b68bb-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b68bb-206">Next steps</span></span>

* [<span data-ttu-id="b68bb-207">檢視更多邏輯應用程式的範例和案例</span><span class="sxs-lookup"><span data-stu-id="b68bb-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="b68bb-208">了解如何監視邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="b68bb-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="b68bb-209">建立邏輯應用程式的自動化部署範本</span><span class="sxs-lookup"><span data-stu-id="b68bb-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
