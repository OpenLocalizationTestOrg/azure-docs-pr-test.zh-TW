---
title: "摘要 HL7 FHIR 資源-Azure Cosmos DB aaaChange |Microsoft 文件"
description: "了解如何註冊 tooset 變更 HL7 FHIR 病患醫療保健記錄使用 Azure 邏輯應用程式、 Azure Cosmos DB 和 Service Bus 的通知。"
keywords: hl7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>使用 Logic Apps 與 Azure Cosmos DB 對 HL7 FHIR 病患的醫療保健記錄變更發出通知

Azure MVP Howard Edidin 最近已由想 tooadd 新功能 tootheir 病患的入口網站的醫療保健組織聯繫。 已更新其健全狀況資料錄，以及它們需要病患 toobe 無法 toosubscribe toothese 更新時，它們就會需要 toosend 通知 toopatients。 

本文逐步建立此醫療保健組織使用 Azure Cosmos DB、 Logic Apps 和 Service Bus hello 變更摘要的通知解決方案。 

## <a name="project-requirements"></a>專案需求
- 提供者以 XML 格式傳送 HL7 綜合臨床文件架構 (Consolidated-Clinical Document Architecture, C-CDA) 文件。 C-CDA 文件幾乎包含所有類型的臨床文件，包括家族史和免疫記錄之類的臨床文件，以及系統管理、工作流程和財務方面的文件。 
- C CDA 文件轉換太[HL7 FHIR 資源](http://hl7.org/fhir/2017Jan/resourcelist.html)JSON 格式。
- 修改過的 FHIR 資源文件會以 JSON 格式透過電子郵件傳送。

## <a name="solution-workflow"></a>方案工作流程 

在高層級，hello 專案需要下列工作流程步驟 hello: 
1. 將 C CDA 文件 tooFHIR 資源的轉換。
2. 針對修改過的 FHIR 資源執行週期性觸發輪詢。 
2. 新增或修改過的文件，呼叫自訂應用程式、 FhirNotificationApi、 tooconnect tooAzure Cosmos DB 和查詢。
3. 儲存 hello 回應 tootoohello 服務匯流排佇列。
4. Hello 服務匯流排佇列中的新訊息輪詢。
5. 傳送電子郵件通知 toopatients。

## <a name="solution-architecture"></a>方案架構
此解決方案需要三個需求完成 hello 方案工作流程的上方的 Logic Apps toomeet hello。 hello 三個邏輯應用程式如下：
1. **HL7 FHIR 對應應用程式**： 收到 hello HL7 C CDA 文件，請將其轉換 toohello FHIR 資源，然後將它儲存 tooAzure Cosmos DB。
2. **EHR 應用程式**： 查詢 hello Azure Cosmos DB FHIR 儲存機制，並將儲存 hello 回應 tooa 服務匯流排佇列。 此邏輯應用程式會使用[API 應用程式](#api-app)tooretrieve 新增和變更文件。
3. **處理程序通知應用程式**: hello 主體中傳送嗨 FHIR 資源文件與電子郵件通知。

![此 HL7 FHIR 保健解決方案中使用的 hello 三 Logic Apps](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Hello 解決方案中使用的 azure 服務

#### <a name="azure-cosmos-db-documentdb-api"></a>Azure Cosmos DB DocumentDB API
Azure Cosmos DB hello 遵循圖所示為 hello hello FHIR 資源的儲存機制。

![使用此 HL7 FHIR 醫療保健教學課程中的 hello Azure Cosmos DB 帳戶](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Logic Apps
邏輯應用程式處理 hello 工作流程。 hello 下列螢幕擷取畫面顯示 hello 這個解決方案所建立的邏輯應用程式。 


1. **HL7 FHIR 對應應用程式**： 收到 hello HL7 C CDA 文件，並將其轉換 tooan FHIR 資源使用 Logic apps hello 企業版整合套件。 hello 企業版整合套件會處理 hello 對應從 hello C CDA tooFHIR 資源。

    ![hello 邏輯應用程式使用 tooreceive HL7 FHIR 醫療記錄](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **EHR 應用程式**： 查詢 hello Azure Cosmos DB FHIR 儲存機制，並儲存 hello 回應 tooa 服務匯流排佇列。 以下是 hello hello GetNewOrModifiedFHIRDocuments 應用程式的程式碼。

    ![hello 邏輯應用程式使用 tooquery Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **處理程序通知應用程式**: hello 主體中傳送嗨 FHIR 資源文件與電子郵件通知。

    ![hello 會與 hello HL7 FHIR 資源病患的電子郵件傳送 hello 主體中的邏輯應用程式](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>服務匯流排
下列圖顯示 hello 病患佇列 hello。 hello Tag 屬性值會用於 hello 電子郵件主旨。

![hello 這個 HL7 FHIR 教學課程中使用的服務匯流排佇列](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>API 應用程式
API 應用程式連接 tooAzure Cosmos DB 與新的或修改 FHIR 文件的資源類型的查詢。 此應用程式有一個控制器 **FhirNotificationApi** 與一項作業 **GetNewOrModifiedFhirDocuments**，請參閱 [API 應用程式來源](#api-app-source)。

我們使用 hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx)從 hello Azure Cosmos DB DocumentDB.NET 應用程式開發介面的類別。 如需詳細資訊，請參閱 hello[變更摘要的本文](change-feed.md)。 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>GetNewOrModifiedFhirDocuments 作業

**輸入**
- DatabaseId
- CollectionId
- HL7 FHIR 資源類型名稱
- 布林值︰從頭開始
- Int：傳回的文件數目

**輸出**
- 成功︰狀態碼︰200，回應︰文件清單 (JSON 陣列)
- 失敗︰狀態碼︰404，回應：「找不到 'resource name' 資源類型的文件」

<a id="api-app-source"></a>

**Hello API 應用程式的來源**

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-hello-fhirnotificationapi"></a>測試 hello FhirNotificationApi 

hello 下列影像示範 swagger 的方式使用的 tootootest hello [FhirNotificationApi](#api-app-source)。

![hello Swagger 檔案使用 tootest hello API 應用程式](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Azure 入口網站儀表板

hello 下列影像顯示所有 hello hello Azure 入口網站中執行此方案的 Azure 服務。

![hello 顯示此 HL7 FHIR 教學課程中使用的所有 hello 服務的 Azure 入口網站](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>摘要

- 您已經學會 Azure Cosmos DB 具有原生支援新的通知或修改文件和是多麼的輕鬆 toouse。 
- 利用 Logic Apps，您可以建立工作流程，而不需要撰寫任何程式碼。
- 使用 Azure Service Bus 佇列 toohandle hello 發佈 hello HL7 FHIR 文件。

## <a name="next-steps"></a>後續步驟
如需有關 Azure Cosmos DB 的詳細資訊，請參閱 hello [Azure Cosmos DB 首頁](https://azure.microsoft.com/services/cosmos-db/)。 如需 Logic Apps 的詳細資訊，請參閱 [Logic Apps](https://azure.microsoft.com/services/logic-apps/)。


