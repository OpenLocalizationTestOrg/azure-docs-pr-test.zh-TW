---
title: "例外狀況處理與錯誤記錄案例 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 044de27c75da93c95609110d2b73336c42f746fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="8d4cf-103">案例︰適用於邏輯應用程式的例外狀況處理與記錄錯誤</span><span class="sxs-lookup"><span data-stu-id="8d4cf-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="8d4cf-104">本案例說明如何擴充邏輯應用程式，以提升對於例外狀況處理的支援。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-104">This scenario describes how you can extend a logic app to better support exception handling.</span></span> <span data-ttu-id="8d4cf-105">我們使用了現實生活的使用案例來回答下列案例：「Azure Logic Apps 是否支援例外狀況與錯誤處理？」</span><span class="sxs-lookup"><span data-stu-id="8d4cf-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="8d4cf-106">目前的 Azure Logic Apps 結構描述會提供標準的動作回應範本。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-106">The current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="8d4cf-107">這個範本包括內部驗證和 API 應用程式所傳回的錯誤回應。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="8d4cf-108">案例和使用案例概觀</span><span class="sxs-lookup"><span data-stu-id="8d4cf-108">Scenario and use case overview</span></span>

<span data-ttu-id="8d4cf-109">以下為適用於此案例的使用案例：</span><span class="sxs-lookup"><span data-stu-id="8d4cf-109">Here's the story as the use case for this scenario:</span></span> 

<span data-ttu-id="8d4cf-110">知名的醫療保健組織找到了我們，他們想要開發 Azure 解決方案，以使用 Microsoft Dynamics CRM Online 建立病患入口網站。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="8d4cf-111">他們需要在 Dynamics CRM Online 病患入口網站和 Salesforce 之間傳送預約記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="8d4cf-112">因此要求我們對所有病患記錄使用 [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) 標準。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="8d4cf-113">此專案有兩大需求︰</span><span class="sxs-lookup"><span data-stu-id="8d4cf-113">The project had two major requirements:</span></span>  

* <span data-ttu-id="8d4cf-114">用來記錄從 Dynamics CRM Online 入口網站傳送過來之記錄的方法</span><span class="sxs-lookup"><span data-stu-id="8d4cf-114">A method to log records sent from the Dynamics CRM Online portal</span></span>
* <span data-ttu-id="8d4cf-115">用來檢視工作流程中所發生之任何錯誤的方法</span><span class="sxs-lookup"><span data-stu-id="8d4cf-115">A way to view any errors that occurred within the workflow</span></span>

> [!TIP]
> <span data-ttu-id="8d4cf-116">如需關於此專案的高階影片，請參閱[整合使用者群組 (英文)](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group")。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-the-problem"></a><span data-ttu-id="8d4cf-117">問題解決方式</span><span class="sxs-lookup"><span data-stu-id="8d4cf-117">How we solved the problem</span></span>

<span data-ttu-id="8d4cf-118">我們選擇以 [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") 做為記錄檔和錯誤記錄的存放庫 (Cosmos DB 會將記錄當做文件)。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for the log and error records (Cosmos DB refers to records as documents).</span></span> <span data-ttu-id="8d4cf-119">由於 Azure Logic Apps 具有適用於所有回應的標準範本，因此我們不需要建立自訂結構描述。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span></span> <span data-ttu-id="8d4cf-120">我們可以建立 API 應用程式來**插入**及**查詢**錯誤和記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-120">We could create an API app to **Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="8d4cf-121">我們也可以為 API 應用程式中的每個項目定義結構描述。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-121">We could also define a schema for each within the API app.</span></span>  

<span data-ttu-id="8d4cf-122">另一個需求是要在特定日期之後清除記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-122">Another requirement was to purge records after a certain date.</span></span> <span data-ttu-id="8d4cf-123">Cosmos DB 具有稱為[存留時間 (英文)](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "存留時間") (TTL) 的屬性，這可讓我們設定每一筆記錄或每一個集合的「存留時間」值。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-123">Cosmos DB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span></span> <span data-ttu-id="8d4cf-124">此功能讓我們不需手動在 Cosmos DB 中刪除記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-124">This capability eliminated the need to manually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d4cf-125">為了完成本教學課程，您必須建立一個 Cosmos DB 資料庫和兩個集合 (記錄和錯誤)。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-125">To complete this tutorial, you need to create a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-the-logic-app"></a><span data-ttu-id="8d4cf-126">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="8d4cf-126">Create the logic app</span></span>

<span data-ttu-id="8d4cf-127">第一個步驟是建立邏輯應用程式，並在邏輯應用程式設計工具中開啟該應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-127">The first step is to create the logic app and open the app in Logic App Designer.</span></span> <span data-ttu-id="8d4cf-128">在此範例中，我們會使用父子邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="8d4cf-129">假設我們已建立父項，而且將要建立一個子邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-129">Let's assume that we have already created the parent and are going to create one child logic app.</span></span>

<span data-ttu-id="8d4cf-130">由於我們將記錄來自 Dynamics CRM Online 的記錄，因此讓我們從最上層開始。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span></span> <span data-ttu-id="8d4cf-131">我們必須使用**要求**觸發程序，因為父邏輯應用程式會觸發這個子項。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-131">We must use a **Request** trigger because the parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="8d4cf-132">邏輯應用程式觸發程序</span><span class="sxs-lookup"><span data-stu-id="8d4cf-132">Logic app trigger</span></span>

<span data-ttu-id="8d4cf-133">我們使用**要求**觸發程序，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8d4cf-133">We are using a **Request** trigger as shown in the following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="8d4cf-134">步驟</span><span class="sxs-lookup"><span data-stu-id="8d4cf-134">Steps</span></span>

<span data-ttu-id="8d4cf-135">我們必須記錄來自 Dynamics CRM Online 入口網站的病患記錄來源 (要求)。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="8d4cf-136">我們必須從 Dynamics CRM Online 取得新的預約記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="8d4cf-137">來自 CRM 的觸發程序會提供我們 **CRM PatentId**、**記錄類型**、**新的或更新的記錄** (新增或更新布林值) 和 **SalesforceId**。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="8d4cf-138">**SalesforceId** 可以是 null，因為它只會用於更新。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-138">The **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="8d4cf-139">我們使用 CRM **PatientID** 和 [記錄類型] 來取得 CRM 記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span></span>

2. <span data-ttu-id="8d4cf-140">接下來，必須新增 DocumentDB API 應用程式 **InsertLogEntry** 作業，如在這裡的邏輯應用程式設計工具所示。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="8d4cf-141">**插入記錄檔項目**</span><span class="sxs-lookup"><span data-stu-id="8d4cf-141">**Insert log entry**</span></span>

   ![插入記錄檔項目](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="8d4cf-143">**插入錯誤項目**</span><span class="sxs-lookup"><span data-stu-id="8d4cf-143">**Insert error entry**</span></span>

   ![插入記錄檔項目](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="8d4cf-145">**檢查建立記錄失敗**</span><span class="sxs-lookup"><span data-stu-id="8d4cf-145">**Check for create record failure**</span></span>

   ![條件](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="8d4cf-147">邏輯應用程式原始程式碼</span><span class="sxs-lookup"><span data-stu-id="8d4cf-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="8d4cf-148">以下僅是範例。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-148">The following examples are samples only.</span></span> <span data-ttu-id="8d4cf-149">由於此教學課程是以目前在生產環境中的實作為基礎，因此，**來源節點**的值可能不會顯示與安排預約相關的屬性。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="8d4cf-150">記錄</span><span class="sxs-lookup"><span data-stu-id="8d4cf-150">Logging</span></span>

<span data-ttu-id="8d4cf-151">下列邏輯應用程式的程式碼範例示範如何處理記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-151">The following logic app code sample shows how to handle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="8d4cf-152">記錄檔項目</span><span class="sxs-lookup"><span data-stu-id="8d4cf-152">Log entry</span></span>

<span data-ttu-id="8d4cf-153">以下是用來插入記錄項目的邏輯應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-153">Here is the logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="8d4cf-154">記錄檔要求</span><span class="sxs-lookup"><span data-stu-id="8d4cf-154">Log request</span></span>

<span data-ttu-id="8d4cf-155">以下是張貼至 API 應用程式的記錄要求訊息。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-155">Here is the log request message posted to the API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="8d4cf-156">記錄檔回應</span><span class="sxs-lookup"><span data-stu-id="8d4cf-156">Log response</span></span>

<span data-ttu-id="8d4cf-157">以下是來自 API 應用程式的記錄回應訊息。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-157">Here is the log response message from the API app.</span></span>

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

<span data-ttu-id="8d4cf-158">現在讓我們看看錯誤處理步驟。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-158">Now let's look at the error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="8d4cf-159">錯誤處理</span><span class="sxs-lookup"><span data-stu-id="8d4cf-159">Error handling</span></span>

<span data-ttu-id="8d4cf-160">下列邏輯應用程式程式碼範例示範如何實作錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-160">The following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="8d4cf-161">建立錯誤記錄</span><span class="sxs-lookup"><span data-stu-id="8d4cf-161">Create error record</span></span>

<span data-ttu-id="8d4cf-162">以下是用來建立錯誤記錄的邏輯應用程式原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-162">Here is the logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="8d4cf-163">將錯誤插入至 Cosmos DB--要求</span><span class="sxs-lookup"><span data-stu-id="8d4cf-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="8d4cf-164">將錯誤插入至 Cosmos DB--回應</span><span class="sxs-lookup"><span data-stu-id="8d4cf-164">Insert error into Cosmos DB--response</span></span>

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
        "body": "CRM failed to complete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
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

#### <a name="salesforce-error-response"></a><span data-ttu-id="8d4cf-165">Salesforce 錯誤回應</span><span class="sxs-lookup"><span data-stu-id="8d4cf-165">Salesforce error response</span></span>

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
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-the-response-back-to-parent-logic-app"></a><span data-ttu-id="8d4cf-166">將回應傳回父邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="8d4cf-166">Return the response back to parent logic app</span></span>

<span data-ttu-id="8d4cf-167">取得回應之後，您可以將回應傳回父邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-167">After you get the response, you can pass the response back to the parent logic app.</span></span>

#### <a name="return-success-response-to-parent-logic-app"></a><span data-ttu-id="8d4cf-168">將成功回應傳回給父邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="8d4cf-168">Return success response to parent logic app</span></span>

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

#### <a name="return-error-response-to-parent-logic-app"></a><span data-ttu-id="8d4cf-169">將錯誤回應傳回給父邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="8d4cf-169">Return error response to parent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="8d4cf-170">Cosmos DB 存放庫和入口網站</span><span class="sxs-lookup"><span data-stu-id="8d4cf-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="8d4cf-171">我們的解決方案新增了含有 [Cosmos DB](https://azure.microsoft.com/services/documentdb) 的功能。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="8d4cf-172">錯誤管理入口網站</span><span class="sxs-lookup"><span data-stu-id="8d4cf-172">Error management portal</span></span>

<span data-ttu-id="8d4cf-173">若要檢視錯誤，您可以建立 MVC Web 應用程式，以顯示來自 Cosmos DB 的錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-173">To view the errors, you can create an MVC web app to display the error records from Cosmos DB.</span></span> <span data-ttu-id="8d4cf-174">目前的版本中包含**清單**、**詳細資料**、**編輯**和**刪除**作業。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span></span>

> [!NOTE]
> <span data-ttu-id="8d4cf-175">編輯作業︰Cosmos DB 會取代整份文件。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-175">Edit operation: Cosmos DB replaces the entire document.</span></span> <span data-ttu-id="8d4cf-176">**清單**和**詳細資料**檢視中所顯示的記錄只是範例。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-176">The records shown in the **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="8d4cf-177">而非實際的病患預約記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="8d4cf-178">以下是使用先前所述方法建立之 MVC 應用程式詳細資料的範例。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-178">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="8d4cf-179">錯誤管理清單</span><span class="sxs-lookup"><span data-stu-id="8d4cf-179">Error management list</span></span>
![錯誤清單](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="8d4cf-181">錯誤管理詳細資料檢視</span><span class="sxs-lookup"><span data-stu-id="8d4cf-181">Error management detail view</span></span>
![錯誤詳細資料](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="8d4cf-183">記錄檔管理入口網站</span><span class="sxs-lookup"><span data-stu-id="8d4cf-183">Log management portal</span></span>

<span data-ttu-id="8d4cf-184">為了檢視記錄檔，我們還建立了 MVC Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-184">To view the logs, we also created an MVC web app.</span></span> <span data-ttu-id="8d4cf-185">以下是使用先前所述方法建立之 MVC 應用程式詳細資料的範例。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-185">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="8d4cf-186">範例記錄檔詳細資料檢視</span><span class="sxs-lookup"><span data-stu-id="8d4cf-186">Sample log detail view</span></span>
![記錄檔詳細資料檢視](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="8d4cf-188">API 應用程式詳細資料</span><span class="sxs-lookup"><span data-stu-id="8d4cf-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="8d4cf-189">Logic Apps 例外狀況管理 API</span><span class="sxs-lookup"><span data-stu-id="8d4cf-189">Logic Apps exception management API</span></span>

<span data-ttu-id="8d4cf-190">我們的開放原始碼 Azure Logic Apps 例外狀況管理 API 應用程式提供了這裡所說的功能，其中有兩個控制器：</span><span class="sxs-lookup"><span data-stu-id="8d4cf-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="8d4cf-191">**ErrorController** 會在 DocumentDB 集合中插入錯誤記錄 (文件)。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="8d4cf-192">**LogController** 會在 DocumentDB 集合中插入記錄檔記錄 (文件)。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="8d4cf-193">這兩個控制器使用 `async Task<dynamic>` 作業，允許作業在執行階段解析，讓我們可以在作業的主體中建立 DocumentDB 結構描述。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span></span> 
> 

<span data-ttu-id="8d4cf-194">DocumentDB 中的每個文件都必須具有唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="8d4cf-195">我們將會使用 `PatientId` ，並加入轉換為 Unix 時間戳記值 (雙精確度) 的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span></span> <span data-ttu-id="8d4cf-196">我們會將值截斷以移除小數值。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-196">We truncate the value to remove the fractional value.</span></span>

<span data-ttu-id="8d4cf-197">您可以[從 GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs)檢視我們的錯誤控制器 API 的原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="8d4cf-198">我們使用下列語法，從邏輯應用程式呼叫 API：</span><span class="sxs-lookup"><span data-stu-id="8d4cf-198">We call the API from a logic app by using the following syntax:</span></span>

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

<span data-ttu-id="8d4cf-199">上述程式碼範例的運算式會檢查 Create_NewPatientRecord 狀態是否為 **Failed**。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="8d4cf-200">摘要</span><span class="sxs-lookup"><span data-stu-id="8d4cf-200">Summary</span></span>

* <span data-ttu-id="8d4cf-201">您可以在邏輯應用程式中輕鬆地實作記錄和錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="8d4cf-202">您可以使用 DocumentDB 做為記錄檔和錯誤記錄 (文件) 的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-202">You can use DocumentDB as the repository for log and error records (documents).</span></span>
* <span data-ttu-id="8d4cf-203">您可以使用 MVC 建立入口網站，以顯示記錄檔和錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-203">You can use MVC to create a portal to display log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="8d4cf-204">原始程式碼</span><span class="sxs-lookup"><span data-stu-id="8d4cf-204">Source code</span></span>

<span data-ttu-id="8d4cf-205">Logic Apps 例外狀況管理 API 應用程式的原始程式碼可在此 [GitHub 儲存機制](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "邏輯應用程式例外狀況管理 API")觀賞此專案的高階影片。</span><span class="sxs-lookup"><span data-stu-id="8d4cf-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d4cf-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8d4cf-206">Next steps</span></span>

* [<span data-ttu-id="8d4cf-207">檢視更多邏輯應用程式的範例和案例</span><span class="sxs-lookup"><span data-stu-id="8d4cf-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="8d4cf-208">了解如何監視邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="8d4cf-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="8d4cf-209">建立邏輯應用程式的自動化部署範本</span><span class="sxs-lookup"><span data-stu-id="8d4cf-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
