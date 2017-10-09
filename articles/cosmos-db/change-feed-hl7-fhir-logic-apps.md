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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="b986b-104">使用 Logic Apps 與 Azure Cosmos DB 對 HL7 FHIR 病患的醫療保健記錄變更發出通知</span><span class="sxs-lookup"><span data-stu-id="b986b-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="b986b-105">Azure MVP Howard Edidin 最近已由想 tooadd 新功能 tootheir 病患的入口網站的醫療保健組織聯繫。</span><span class="sxs-lookup"><span data-stu-id="b986b-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="b986b-106">已更新其健全狀況資料錄，以及它們需要病患 toobe 無法 toosubscribe toothese 更新時，它們就會需要 toosend 通知 toopatients。</span><span class="sxs-lookup"><span data-stu-id="b986b-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="b986b-107">本文逐步建立此醫療保健組織使用 Azure Cosmos DB、 Logic Apps 和 Service Bus hello 變更摘要的通知解決方案。</span><span class="sxs-lookup"><span data-stu-id="b986b-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="b986b-108">專案需求</span><span class="sxs-lookup"><span data-stu-id="b986b-108">Project requirements</span></span>
- <span data-ttu-id="b986b-109">提供者以 XML 格式傳送 HL7 綜合臨床文件架構 (Consolidated-Clinical Document Architecture, C-CDA) 文件。</span><span class="sxs-lookup"><span data-stu-id="b986b-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="b986b-110">C-CDA 文件幾乎包含所有類型的臨床文件，包括家族史和免疫記錄之類的臨床文件，以及系統管理、工作流程和財務方面的文件。</span><span class="sxs-lookup"><span data-stu-id="b986b-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="b986b-111">C CDA 文件轉換太[HL7 FHIR 資源](http://hl7.org/fhir/2017Jan/resourcelist.html)JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="b986b-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="b986b-112">修改過的 FHIR 資源文件會以 JSON 格式透過電子郵件傳送。</span><span class="sxs-lookup"><span data-stu-id="b986b-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="b986b-113">方案工作流程</span><span class="sxs-lookup"><span data-stu-id="b986b-113">Solution workflow</span></span> 

<span data-ttu-id="b986b-114">在高層級，hello 專案需要下列工作流程步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="b986b-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="b986b-115">將 C CDA 文件 tooFHIR 資源的轉換。</span><span class="sxs-lookup"><span data-stu-id="b986b-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="b986b-116">針對修改過的 FHIR 資源執行週期性觸發輪詢。</span><span class="sxs-lookup"><span data-stu-id="b986b-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="b986b-117">新增或修改過的文件，呼叫自訂應用程式、 FhirNotificationApi、 tooconnect tooAzure Cosmos DB 和查詢。</span><span class="sxs-lookup"><span data-stu-id="b986b-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="b986b-118">儲存 hello 回應 tootoohello 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="b986b-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="b986b-119">Hello 服務匯流排佇列中的新訊息輪詢。</span><span class="sxs-lookup"><span data-stu-id="b986b-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="b986b-120">傳送電子郵件通知 toopatients。</span><span class="sxs-lookup"><span data-stu-id="b986b-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="b986b-121">方案架構</span><span class="sxs-lookup"><span data-stu-id="b986b-121">Solution architecture</span></span>
<span data-ttu-id="b986b-122">此解決方案需要三個需求完成 hello 方案工作流程的上方的 Logic Apps toomeet hello。</span><span class="sxs-lookup"><span data-stu-id="b986b-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="b986b-123">hello 三個邏輯應用程式如下：</span><span class="sxs-lookup"><span data-stu-id="b986b-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="b986b-124">**HL7 FHIR 對應應用程式**： 收到 hello HL7 C CDA 文件，請將其轉換 toohello FHIR 資源，然後將它儲存 tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="b986b-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="b986b-125">**EHR 應用程式**： 查詢 hello Azure Cosmos DB FHIR 儲存機制，並將儲存 hello 回應 tooa 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="b986b-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="b986b-126">此邏輯應用程式會使用[API 應用程式](#api-app)tooretrieve 新增和變更文件。</span><span class="sxs-lookup"><span data-stu-id="b986b-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="b986b-127">**處理程序通知應用程式**: hello 主體中傳送嗨 FHIR 資源文件與電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="b986b-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![此 HL7 FHIR 保健解決方案中使用的 hello 三 Logic Apps](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="b986b-129">Hello 解決方案中使用的 azure 服務</span><span class="sxs-lookup"><span data-stu-id="b986b-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="b986b-130">Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="b986b-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="b986b-131">Azure Cosmos DB hello 遵循圖所示為 hello hello FHIR 資源的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b986b-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![使用此 HL7 FHIR 醫療保健教學課程中的 hello Azure Cosmos DB 帳戶](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="b986b-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b986b-133">Logic Apps</span></span>
<span data-ttu-id="b986b-134">邏輯應用程式處理 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="b986b-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="b986b-135">hello 下列螢幕擷取畫面顯示 hello 這個解決方案所建立的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="b986b-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="b986b-136">**HL7 FHIR 對應應用程式**： 收到 hello HL7 C CDA 文件，並將其轉換 tooan FHIR 資源使用 Logic apps hello 企業版整合套件。</span><span class="sxs-lookup"><span data-stu-id="b986b-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="b986b-137">hello 企業版整合套件會處理 hello 對應從 hello C CDA tooFHIR 資源。</span><span class="sxs-lookup"><span data-stu-id="b986b-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![hello 邏輯應用程式使用 tooreceive HL7 FHIR 醫療記錄](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="b986b-139">**EHR 應用程式**： 查詢 hello Azure Cosmos DB FHIR 儲存機制，並儲存 hello 回應 tooa 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="b986b-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="b986b-140">以下是 hello hello GetNewOrModifiedFHIRDocuments 應用程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="b986b-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![hello 邏輯應用程式使用 tooquery Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="b986b-142">**處理程序通知應用程式**: hello 主體中傳送嗨 FHIR 資源文件與電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="b986b-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![hello 會與 hello HL7 FHIR 資源病患的電子郵件傳送 hello 主體中的邏輯應用程式](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="b986b-144">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="b986b-144">Service Bus</span></span>
<span data-ttu-id="b986b-145">下列圖顯示 hello 病患佇列 hello。</span><span class="sxs-lookup"><span data-stu-id="b986b-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="b986b-146">hello Tag 屬性值會用於 hello 電子郵件主旨。</span><span class="sxs-lookup"><span data-stu-id="b986b-146">hello Tag property value is used for hello email subject.</span></span>

![hello 這個 HL7 FHIR 教學課程中使用的服務匯流排佇列](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="b986b-148">API 應用程式</span><span class="sxs-lookup"><span data-stu-id="b986b-148">API app</span></span>
<span data-ttu-id="b986b-149">API 應用程式連接 tooAzure Cosmos DB 與新的或修改 FHIR 文件的資源類型的查詢。</span><span class="sxs-lookup"><span data-stu-id="b986b-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="b986b-150">此應用程式有一個控制器 **FhirNotificationApi** 與一項作業 **GetNewOrModifiedFhirDocuments**，請參閱 [API 應用程式來源](#api-app-source)。</span><span class="sxs-lookup"><span data-stu-id="b986b-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="b986b-151">我們使用 hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx)從 hello Azure Cosmos DB DocumentDB.NET 應用程式開發介面的類別。</span><span class="sxs-lookup"><span data-stu-id="b986b-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="b986b-152">如需詳細資訊，請參閱 hello[變更摘要的本文](change-feed.md)。</span><span class="sxs-lookup"><span data-stu-id="b986b-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="b986b-153">GetNewOrModifiedFhirDocuments 作業</span><span class="sxs-lookup"><span data-stu-id="b986b-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="b986b-154">**輸入**</span><span class="sxs-lookup"><span data-stu-id="b986b-154">**Inputs**</span></span>
- <span data-ttu-id="b986b-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="b986b-155">DatabaseId</span></span>
- <span data-ttu-id="b986b-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="b986b-156">CollectionId</span></span>
- <span data-ttu-id="b986b-157">HL7 FHIR 資源類型名稱</span><span class="sxs-lookup"><span data-stu-id="b986b-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="b986b-158">布林值︰從頭開始</span><span class="sxs-lookup"><span data-stu-id="b986b-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="b986b-159">Int：傳回的文件數目</span><span class="sxs-lookup"><span data-stu-id="b986b-159">Int: Number of documents returned</span></span>

<span data-ttu-id="b986b-160">**輸出**</span><span class="sxs-lookup"><span data-stu-id="b986b-160">**Outputs**</span></span>
- <span data-ttu-id="b986b-161">成功︰狀態碼︰200，回應︰文件清單 (JSON 陣列)</span><span class="sxs-lookup"><span data-stu-id="b986b-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="b986b-162">失敗︰狀態碼︰404，回應：「找不到 'resource name' 資源類型的文件」</span><span class="sxs-lookup"><span data-stu-id="b986b-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="b986b-163">**Hello API 應用程式的來源**</span><span class="sxs-lookup"><span data-stu-id="b986b-163">**Source for hello API app**</span></span>

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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="b986b-164">測試 hello FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="b986b-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="b986b-165">hello 下列影像示範 swagger 的方式使用的 tootootest hello [FhirNotificationApi](#api-app-source)。</span><span class="sxs-lookup"><span data-stu-id="b986b-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![hello Swagger 檔案使用 tootest hello API 應用程式](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="b986b-167">Azure 入口網站儀表板</span><span class="sxs-lookup"><span data-stu-id="b986b-167">Azure portal dashboard</span></span>

<span data-ttu-id="b986b-168">hello 下列影像顯示所有 hello hello Azure 入口網站中執行此方案的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="b986b-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![hello 顯示此 HL7 FHIR 教學課程中使用的所有 hello 服務的 Azure 入口網站](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="b986b-170">摘要</span><span class="sxs-lookup"><span data-stu-id="b986b-170">Summary</span></span>

- <span data-ttu-id="b986b-171">您已經學會 Azure Cosmos DB 具有原生支援新的通知或修改文件和是多麼的輕鬆 toouse。</span><span class="sxs-lookup"><span data-stu-id="b986b-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="b986b-172">利用 Logic Apps，您可以建立工作流程，而不需要撰寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="b986b-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="b986b-173">使用 Azure Service Bus 佇列 toohandle hello 發佈 hello HL7 FHIR 文件。</span><span class="sxs-lookup"><span data-stu-id="b986b-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b986b-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b986b-174">Next steps</span></span>
<span data-ttu-id="b986b-175">如需有關 Azure Cosmos DB 的詳細資訊，請參閱 hello [Azure Cosmos DB 首頁](https://azure.microsoft.com/services/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="b986b-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="b986b-176">如需 Logic Apps 的詳細資訊，請參閱 [Logic Apps](https://azure.microsoft.com/services/logic-apps/)。</span><span class="sxs-lookup"><span data-stu-id="b986b-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


