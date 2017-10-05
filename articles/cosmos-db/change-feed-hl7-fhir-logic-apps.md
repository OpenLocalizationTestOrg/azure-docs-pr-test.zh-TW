---
title: "變更 HL7 FHIR 資源的摘要 - Azure Cosmos DB | Microsoft Docs"
description: "了解如何使用 Azure Logic Apps、Azure Cosmos DB 和服務匯流排，來設定 HL7 FHIR 病患之醫療保健記錄的變更通知。"
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
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="7dfc0-104">使用 Logic Apps 與 Azure Cosmos DB 對 HL7 FHIR 病患的醫療保健記錄變更發出通知</span><span class="sxs-lookup"><span data-stu-id="7dfc0-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="7dfc0-105">某家醫療保健組織最近與 Howard Edidin 這位 Azure MVP 連絡，因為他們想要在其病患入口網站中新增功能。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="7dfc0-106">他們需要在病患的健康記錄有所更新時對病患發出通知，並讓他們能夠訂閱這些更新。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="7dfc0-107">本文會逐步引導您了解使用 Azure Cosmos DB、Logic Apps 和服務匯流排，為此醫療保健組織所建立的變更摘要通知方案。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="7dfc0-108">專案需求</span><span class="sxs-lookup"><span data-stu-id="7dfc0-108">Project requirements</span></span>
- <span data-ttu-id="7dfc0-109">提供者以 XML 格式傳送 HL7 綜合臨床文件架構 (Consolidated-Clinical Document Architecture, C-CDA) 文件。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="7dfc0-110">C-CDA 文件幾乎包含所有類型的臨床文件，包括家族史和免疫記錄之類的臨床文件，以及系統管理、工作流程和財務方面的文件。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="7dfc0-111">C-CDA 文件會轉換成 JSON 格式的 [HL7 FHIR 資源](http://hl7.org/fhir/2017Jan/resourcelist.html)。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="7dfc0-112">修改過的 FHIR 資源文件會以 JSON 格式透過電子郵件傳送。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="7dfc0-113">方案工作流程</span><span class="sxs-lookup"><span data-stu-id="7dfc0-113">Solution workflow</span></span> 

<span data-ttu-id="7dfc0-114">概括而言，此專案需要下列工作流程步驟︰</span><span class="sxs-lookup"><span data-stu-id="7dfc0-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="7dfc0-115">將 C-CDA 文件轉換成 FHIR 資源。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="7dfc0-116">針對修改過的 FHIR 資源執行週期性觸發輪詢。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="7dfc0-117">呼叫自訂應用程式 FhirNotificationApi 來連線到 Azure Cosmos DB，並查詢是否有新的或修改過的文件。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="7dfc0-118">將回應儲存到服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="7dfc0-119">輪詢服務匯流排佇列中的新訊息。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="7dfc0-120">傳送電子郵件通知給病患。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="7dfc0-121">方案架構</span><span class="sxs-lookup"><span data-stu-id="7dfc0-121">Solution architecture</span></span>
<span data-ttu-id="7dfc0-122">此方案需要三個 Logic Apps 才能符合上述需求，並完成方案工作流程。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="7dfc0-123">這三個邏輯應用程式分別是︰</span><span class="sxs-lookup"><span data-stu-id="7dfc0-123">The three logic apps are:</span></span>
1. <span data-ttu-id="7dfc0-124">**HL7-FHIR-Mapping 應用程式**︰接收 HL7 C-CDA 文件、將其轉換為 FHIR 資源，然後儲存至 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="7dfc0-125">**EHR 應用程式**︰查詢 Azure Cosmos DB FHIR 存放庫，並將回應儲存到服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="7dfc0-126">此邏輯應用程式使用 [API 應用程式](#api-app)來擷取新的和變更的文件。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="7dfc0-127">**處理通知應用程式**︰傳送內文中有 FHIR 資源文件的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![此 HL7 FHIR 醫療保健方案所使用的三個 Logic Apps](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="7dfc0-129">此方案所使用的 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="7dfc0-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="7dfc0-130">Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="7dfc0-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="7dfc0-131">Azure Cosmos DB 是 FHIR 資源的存放庫，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![此 HL7 FHIR 醫療保健教學課程所使用的 Azure Cosmos DB 帳戶](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="7dfc0-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="7dfc0-133">Logic Apps</span></span>
<span data-ttu-id="7dfc0-134">Logic Apps 會處理工作流程程序。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="7dfc0-135">下列螢幕擷取畫面顯示為此方案所建立的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="7dfc0-136">**HL7-FHIR-Mapping 應用程式**︰接收 HL7 C-CDA 文件，然後使用適用於 Logic Apps 的企業整合套件將其轉換為 FHIR 資源。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="7dfc0-137">企業整合套件會處理 C-CDA 與 FHIR 資源的對應。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![用來接收 HL7 FHIR 醫療保健記錄的邏輯應用程式](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="7dfc0-139">**EHR 應用程式**︰查詢 Azure Cosmos DB FHIR 存放庫，並將回應儲存到服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="7dfc0-140">GetNewOrModifiedFHIRDocuments 應用程式的程式碼在下面。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![用來查詢 Azure Cosmos DB 的邏輯應用程式](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="7dfc0-142">**處理通知應用程式**︰傳送內文中有 FHIR 資源文件的電子郵件通知。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![會傳送內文中有 HL7 FHIR 資源之電子郵件給病患的邏輯應用程式](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="7dfc0-144">服務匯流排</span><span class="sxs-lookup"><span data-stu-id="7dfc0-144">Service Bus</span></span>
<span data-ttu-id="7dfc0-145">下圖顯示病患佇列。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="7dfc0-146">電子郵件主旨會使用 Tag 屬性值。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-146">The Tag property value is used for the email subject.</span></span>

![此 HL7 FHIR 教學課程所使用的服務匯流排佇列](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="7dfc0-148">API 應用程式</span><span class="sxs-lookup"><span data-stu-id="7dfc0-148">API app</span></span>
<span data-ttu-id="7dfc0-149">API 應用程式會連線到 Azure Cosmos DB，並依資源類型查詢新的或修改過的 FHIR 文件。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="7dfc0-150">此應用程式有一個控制器 **FhirNotificationApi** 與一項作業 **GetNewOrModifiedFhirDocuments**，請參閱 [API 應用程式來源](#api-app-source)。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="7dfc0-151">我們會使用來自 Azure Cosmos DB .NET API 的 [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) 類別。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="7dfc0-152">如需詳細資訊，請參閱[變更摘要文章](change-feed.md)。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="7dfc0-153">GetNewOrModifiedFhirDocuments 作業</span><span class="sxs-lookup"><span data-stu-id="7dfc0-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="7dfc0-154">**輸入**</span><span class="sxs-lookup"><span data-stu-id="7dfc0-154">**Inputs**</span></span>
- <span data-ttu-id="7dfc0-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="7dfc0-155">DatabaseId</span></span>
- <span data-ttu-id="7dfc0-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="7dfc0-156">CollectionId</span></span>
- <span data-ttu-id="7dfc0-157">HL7 FHIR 資源類型名稱</span><span class="sxs-lookup"><span data-stu-id="7dfc0-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="7dfc0-158">布林值︰從頭開始</span><span class="sxs-lookup"><span data-stu-id="7dfc0-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="7dfc0-159">Int：傳回的文件數目</span><span class="sxs-lookup"><span data-stu-id="7dfc0-159">Int: Number of documents returned</span></span>

<span data-ttu-id="7dfc0-160">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7dfc0-160">**Outputs**</span></span>
- <span data-ttu-id="7dfc0-161">成功︰狀態碼︰200，回應︰文件清單 (JSON 陣列)</span><span class="sxs-lookup"><span data-stu-id="7dfc0-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="7dfc0-162">失敗︰狀態碼︰404，回應：「找不到 'resource name' 資源類型的文件」</span><span class="sxs-lookup"><span data-stu-id="7dfc0-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="7dfc0-163">**API 應用程式的來源**</span><span class="sxs-lookup"><span data-stu-id="7dfc0-163">**Source for the API app**</span></span>

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
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
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

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="7dfc0-164">測試 FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="7dfc0-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="7dfc0-165">下圖示範如何使用 Swagger 來測試 [FhirNotificationApi](#api-app-source)。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![用來測試 API 應用程式的 Swagger 檔案](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="7dfc0-167">Azure 入口網站儀表板</span><span class="sxs-lookup"><span data-stu-id="7dfc0-167">Azure portal dashboard</span></span>

<span data-ttu-id="7dfc0-168">下圖顯示此方案在 Azure 入口網站中執行的所有 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![顯示此 HL7 FHIR 教學課程所使用之所有服務的 Azure 入口網站](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="7dfc0-170">摘要</span><span class="sxs-lookup"><span data-stu-id="7dfc0-170">Summary</span></span>

- <span data-ttu-id="7dfc0-171">您已了解 Azure Cosmos DB 原生支援對新的或修改過的文件發出通知，以及其使用方式有多麼簡單。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="7dfc0-172">利用 Logic Apps，您可以建立工作流程，而不需要撰寫任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="7dfc0-173">使用 Azure 服務匯流排佇列來處理 HL7 FHIR 文件的散發。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dfc0-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7dfc0-174">Next steps</span></span>
<span data-ttu-id="7dfc0-175">如需 Azure Cosmos DB 的詳細資訊，請參閱 [Azure Cosmos DB 首頁](https://azure.microsoft.com/services/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="7dfc0-176">如需 Logic Apps 的詳細資訊，請參閱 [Logic Apps](https://azure.microsoft.com/services/logic-apps/)。</span><span class="sxs-lookup"><span data-stu-id="7dfc0-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


