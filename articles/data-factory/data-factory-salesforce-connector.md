---
title: "使用 Data Factory 從 Salesforce 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Salesforce 移動資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="4682b-103">使用 Azure Data Factory 從 Salesforce 移動資料</span><span class="sxs-lookup"><span data-stu-id="4682b-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="4682b-104">本文概述如何在 Azure Data Factory 使用複製活動，將資料從 Salesforce 複製到 [支援的來源與接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 資料表的 [接收] 欄底下列出的任何資料存放區。</span><span class="sxs-lookup"><span data-stu-id="4682b-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4682b-105">本文是根據 [資料移動活動](data-factory-data-movement-activities.md) 一文，該文呈現使用複製活動移動資料的一般概觀以及支援的資料存放區組合。</span><span class="sxs-lookup"><span data-stu-id="4682b-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="4682b-106">Azure Data Factory 目前只支援將資料從 Salesforce 移動到 [支援的接收資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)，但不支援將資料從其他資料存放區移動到 Salesforce。</span><span class="sxs-lookup"><span data-stu-id="4682b-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="4682b-107">支援的版本</span><span class="sxs-lookup"><span data-stu-id="4682b-107">Supported versions</span></span>
<span data-ttu-id="4682b-108">此連接器使用下列其中一個 Salesforce 版本︰Developer Edition、Professional Edition、Enterprise Edition 或 Unlimited Edition。</span><span class="sxs-lookup"><span data-stu-id="4682b-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="4682b-109">並且支援從 Salesforce 生產、沙箱和自訂網域複製。</span><span class="sxs-lookup"><span data-stu-id="4682b-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4682b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4682b-110">Prerequisites</span></span>
* <span data-ttu-id="4682b-111">必須啟用 API 權限。</span><span class="sxs-lookup"><span data-stu-id="4682b-111">API permission must be enabled.</span></span> <span data-ttu-id="4682b-112">請參閱 [如何在 Salesforce 中透過權限集啟用 API 存取權？](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="4682b-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="4682b-113">若要將資料從 Salesforce 複製到內部部署資料存放區，您必須在內部部署環境中至少安裝資料管理閘道 2.0。</span><span class="sxs-lookup"><span data-stu-id="4682b-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="4682b-114">Salesforce 要求限制</span><span class="sxs-lookup"><span data-stu-id="4682b-114">Salesforce request limits</span></span>
<span data-ttu-id="4682b-115">Salesforce 對於 API 要求總數和並行 API 要求均有限制。</span><span class="sxs-lookup"><span data-stu-id="4682b-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="4682b-116">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="4682b-116">Note the following points:</span></span>

- <span data-ttu-id="4682b-117">如果並行要求數目超過限制，便會進行節流，而且您會看到隨機失敗。</span><span class="sxs-lookup"><span data-stu-id="4682b-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="4682b-118">如果要求總數超過限制，Salesforce 帳戶將會封鎖 24 小時。</span><span class="sxs-lookup"><span data-stu-id="4682b-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="4682b-119">在上述兩種情況中，您也可能會收到「REQUEST_LIMIT_EXCEEDED」錯誤。</span><span class="sxs-lookup"><span data-stu-id="4682b-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="4682b-120">如需詳細資訊，請參閱 [Salesforce 開發人員限制](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf)文章的＜API 要求限制＞一節。</span><span class="sxs-lookup"><span data-stu-id="4682b-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4682b-121">開始使用</span><span class="sxs-lookup"><span data-stu-id="4682b-121">Getting started</span></span>
<span data-ttu-id="4682b-122">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 Salesforce 移動資料。</span><span class="sxs-lookup"><span data-stu-id="4682b-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="4682b-123">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="4682b-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="4682b-124">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="4682b-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="4682b-125">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="4682b-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4682b-126">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="4682b-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4682b-127">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="4682b-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="4682b-128">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="4682b-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="4682b-129">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="4682b-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="4682b-130">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="4682b-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4682b-131">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="4682b-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="4682b-132">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="4682b-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="4682b-133">如需相關範例，其中含有用來從 Salesforce 複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 Salesforce 複製到 Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="4682b-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="4682b-134">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Salesforce 特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="4682b-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="4682b-135">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="4682b-135">Linked service properties</span></span>
<span data-ttu-id="4682b-136">下表提供 Salesforce 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="4682b-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="4682b-137">屬性</span><span class="sxs-lookup"><span data-stu-id="4682b-137">Property</span></span> | <span data-ttu-id="4682b-138">說明</span><span class="sxs-lookup"><span data-stu-id="4682b-138">Description</span></span> | <span data-ttu-id="4682b-139">必要</span><span class="sxs-lookup"><span data-stu-id="4682b-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4682b-140">類型</span><span class="sxs-lookup"><span data-stu-id="4682b-140">type</span></span> |<span data-ttu-id="4682b-141">類型屬性必須設為： **Salesforce**。</span><span class="sxs-lookup"><span data-stu-id="4682b-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="4682b-142">是</span><span class="sxs-lookup"><span data-stu-id="4682b-142">Yes</span></span> |
| <span data-ttu-id="4682b-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="4682b-143">environmentUrl</span></span> | <span data-ttu-id="4682b-144">指定 Salesforce 執行個體的 URL。</span><span class="sxs-lookup"><span data-stu-id="4682b-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="4682b-145">- 預設值為 "https://login.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="4682b-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="4682b-146">- 若要從沙箱複製資料，請指定 "https://test.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="4682b-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="4682b-147">- 若要從自訂網域複製資料，舉例來說，請指定 "https://[網域].my.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="4682b-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="4682b-148">否</span><span class="sxs-lookup"><span data-stu-id="4682b-148">No</span></span> |
| <span data-ttu-id="4682b-149">username</span><span class="sxs-lookup"><span data-stu-id="4682b-149">username</span></span> |<span data-ttu-id="4682b-150">指定使用者帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="4682b-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="4682b-151">是</span><span class="sxs-lookup"><span data-stu-id="4682b-151">Yes</span></span> |
| <span data-ttu-id="4682b-152">password</span><span class="sxs-lookup"><span data-stu-id="4682b-152">password</span></span> |<span data-ttu-id="4682b-153">指定使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="4682b-153">Specify a password for the user account.</span></span> |<span data-ttu-id="4682b-154">是</span><span class="sxs-lookup"><span data-stu-id="4682b-154">Yes</span></span> |
| <span data-ttu-id="4682b-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="4682b-155">securityToken</span></span> |<span data-ttu-id="4682b-156">指定使用者帳戶的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="4682b-156">Specify a security token for the user account.</span></span> <span data-ttu-id="4682b-157">如需如何重設/取得安全性權杖的指示，請參閱 [取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 。</span><span class="sxs-lookup"><span data-stu-id="4682b-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="4682b-158">若要整體了解安全性權杖，請參閱[安全性和 API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)。</span><span class="sxs-lookup"><span data-stu-id="4682b-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="4682b-159">是</span><span class="sxs-lookup"><span data-stu-id="4682b-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="4682b-160">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="4682b-160">Dataset properties</span></span>
<span data-ttu-id="4682b-161">如需定義資料集的區段和屬性完整清單，請參閱 [建立資料集](data-factory-create-datasets.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="4682b-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4682b-162">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="4682b-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="4682b-163">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="4682b-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="4682b-164">**RelationalTable** 類型資料集的 typeProperties 區段有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="4682b-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="4682b-165">屬性</span><span class="sxs-lookup"><span data-stu-id="4682b-165">Property</span></span> | <span data-ttu-id="4682b-166">說明</span><span class="sxs-lookup"><span data-stu-id="4682b-166">Description</span></span> | <span data-ttu-id="4682b-167">必要</span><span class="sxs-lookup"><span data-stu-id="4682b-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4682b-168">tableName</span><span class="sxs-lookup"><span data-stu-id="4682b-168">tableName</span></span> |<span data-ttu-id="4682b-169">Salesforce 中資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="4682b-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="4682b-170">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="4682b-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="4682b-171">任何自訂物件都需要 API 名稱的「__c」部分。</span><span class="sxs-lookup"><span data-stu-id="4682b-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="4682b-173">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="4682b-173">Copy activity properties</span></span>
<span data-ttu-id="4682b-174">如需定義活動的區段和屬性完整清單，請參閱 [建立管線](data-factory-create-pipelines.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="4682b-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4682b-175">名稱、描述、輸入和輸出資料表以及各種原則等屬性都適用於所有活動類型。</span><span class="sxs-lookup"><span data-stu-id="4682b-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="4682b-176">另一方面，活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4682b-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="4682b-177">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4682b-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="4682b-178">在複製活動中，如果來源類型為 **RelationalSource** (包含 Salesforce)，則 typeProperties 區段可使用下列屬性：</span><span class="sxs-lookup"><span data-stu-id="4682b-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="4682b-179">屬性</span><span class="sxs-lookup"><span data-stu-id="4682b-179">Property</span></span> | <span data-ttu-id="4682b-180">說明</span><span class="sxs-lookup"><span data-stu-id="4682b-180">Description</span></span> | <span data-ttu-id="4682b-181">允許的值</span><span class="sxs-lookup"><span data-stu-id="4682b-181">Allowed values</span></span> | <span data-ttu-id="4682b-182">必要</span><span class="sxs-lookup"><span data-stu-id="4682b-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4682b-183">query</span><span class="sxs-lookup"><span data-stu-id="4682b-183">query</span></span> |<span data-ttu-id="4682b-184">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="4682b-184">Use the custom query to read data.</span></span> |<span data-ttu-id="4682b-185">SQL-92 查詢或 [Salesforce 物件查詢語言 (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 查詢。</span><span class="sxs-lookup"><span data-stu-id="4682b-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="4682b-186">例如：`select * from MyTable__c`。</span><span class="sxs-lookup"><span data-stu-id="4682b-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="4682b-187">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="4682b-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="4682b-188">任何自訂物件都需要 API 名稱的「__c」部分。</span><span class="sxs-lookup"><span data-stu-id="4682b-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="4682b-190">查詢秘訣</span><span class="sxs-lookup"><span data-stu-id="4682b-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="4682b-191">在 DateTime 資料行上使用 Where 子句來擷取資料</span><span class="sxs-lookup"><span data-stu-id="4682b-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="4682b-192">指定 SOQL 或 SQL 查詢時，請注意 DateTime 格式差異。</span><span class="sxs-lookup"><span data-stu-id="4682b-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="4682b-193">例如：</span><span class="sxs-lookup"><span data-stu-id="4682b-193">For example:</span></span>

* <span data-ttu-id="4682b-194">**SOQL 範例**：`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="4682b-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="4682b-195">**SQL 範例**：</span><span class="sxs-lookup"><span data-stu-id="4682b-195">**SQL sample**:</span></span>
    * <span data-ttu-id="4682b-196">**使用複製精靈指定查詢︰**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="4682b-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="4682b-197">**使用 JSON 編輯指定查詢 (適當地逸出字元)︰**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="4682b-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="4682b-198">從 Salesforce 報表擷取資料</span><span class="sxs-lookup"><span data-stu-id="4682b-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="4682b-199">例如，您可以藉由以 `{call "<report name>"}` 方式指定查詢，從 Salesforce 報表擷取資料。</span><span class="sxs-lookup"><span data-stu-id="4682b-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="4682b-200">`"query": "{call \"TestReport\"}"`。</span><span class="sxs-lookup"><span data-stu-id="4682b-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="4682b-201">從 Salesforce 資源回收筒擷取已刪除的記錄</span><span class="sxs-lookup"><span data-stu-id="4682b-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="4682b-202">若要從「Salesforce 資源回收筒」查詢虛刪除記錄，您可以在查詢中指定 **"IsDeleted = 1"**。</span><span class="sxs-lookup"><span data-stu-id="4682b-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="4682b-203">例如，</span><span class="sxs-lookup"><span data-stu-id="4682b-203">For example,</span></span>

* <span data-ttu-id="4682b-204">若只要查詢已刪除的記錄，請指定 "select * from MyTable__c **where IsDeleted= 1**"</span><span class="sxs-lookup"><span data-stu-id="4682b-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="4682b-205">若要查詢所有記錄 (包括現有和已刪除的記錄)，請指定 "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="4682b-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="4682b-206">JSON 範例：將資料從 Salesforce 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="4682b-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="4682b-207">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="4682b-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4682b-208">這些範例示範如何將資料從 Salesforce 複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4682b-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="4682b-209">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="4682b-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="4682b-210">以下是為了實作案例所必須建立的 Data Factory 構件。</span><span class="sxs-lookup"><span data-stu-id="4682b-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="4682b-211">清單後面的各節會提供有關這些步驟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4682b-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="4682b-212">[Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="4682b-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="4682b-213">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="4682b-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="4682b-214">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="4682b-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="4682b-215">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="4682b-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="4682b-216">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="4682b-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="4682b-217">**Salesforce 連結服務**</span><span class="sxs-lookup"><span data-stu-id="4682b-217">**Salesforce linked service**</span></span>

<span data-ttu-id="4682b-218">此範例使用 **Salesforce** 連結服務。</span><span class="sxs-lookup"><span data-stu-id="4682b-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="4682b-219">如需此連結服務所支援的屬性，請參閱 [Salesforce 連結服務](#linked-service-properties) 一節。</span><span class="sxs-lookup"><span data-stu-id="4682b-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="4682b-220">如需如何重設/取得安全性權杖的指示，請參閱 [取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 。</span><span class="sxs-lookup"><span data-stu-id="4682b-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="4682b-221">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="4682b-221">**Azure Storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```
<span data-ttu-id="4682b-222">**Salesforce 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="4682b-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="4682b-223">將 **external** 設定為 **true** 會通知 Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="4682b-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4682b-224">任何自訂物件都需要 API 名稱的「__c」部分。</span><span class="sxs-lookup"><span data-stu-id="4682b-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="4682b-226">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="4682b-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="4682b-227">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="4682b-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="4682b-228">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="4682b-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="4682b-229">此管線包含「複製活動」，該活動已設定為使用輸入和輸出資料集，並且排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="4682b-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="4682b-230">在管線 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="4682b-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="4682b-231">如需 RelationalSource 支援的屬性清單，請參閱 [RelationalSource 類型屬性](#copy-activity-properties) 。</span><span class="sxs-lookup"><span data-stu-id="4682b-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]
    }
}
```
> [!IMPORTANT]
> <span data-ttu-id="4682b-232">任何自訂物件都需要 API 名稱的「__c」部分。</span><span class="sxs-lookup"><span data-stu-id="4682b-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="4682b-234">Salesforce 的類型對應</span><span class="sxs-lookup"><span data-stu-id="4682b-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="4682b-235">Salesforce 類型</span><span class="sxs-lookup"><span data-stu-id="4682b-235">Salesforce type</span></span> | <span data-ttu-id="4682b-236">以 .NET 為基礎的類型</span><span class="sxs-lookup"><span data-stu-id="4682b-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="4682b-237">自動編號</span><span class="sxs-lookup"><span data-stu-id="4682b-237">Auto Number</span></span> |<span data-ttu-id="4682b-238">String</span><span class="sxs-lookup"><span data-stu-id="4682b-238">String</span></span> |
| <span data-ttu-id="4682b-239">核取方塊</span><span class="sxs-lookup"><span data-stu-id="4682b-239">Checkbox</span></span> |<span data-ttu-id="4682b-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="4682b-240">Boolean</span></span> |
| <span data-ttu-id="4682b-241">貨幣</span><span class="sxs-lookup"><span data-stu-id="4682b-241">Currency</span></span> |<span data-ttu-id="4682b-242">兩倍</span><span class="sxs-lookup"><span data-stu-id="4682b-242">Double</span></span> |
| <span data-ttu-id="4682b-243">日期</span><span class="sxs-lookup"><span data-stu-id="4682b-243">Date</span></span> |<span data-ttu-id="4682b-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="4682b-244">DateTime</span></span> |
| <span data-ttu-id="4682b-245">日期/時間</span><span class="sxs-lookup"><span data-stu-id="4682b-245">Date/Time</span></span> |<span data-ttu-id="4682b-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="4682b-246">DateTime</span></span> |
| <span data-ttu-id="4682b-247">電子郵件</span><span class="sxs-lookup"><span data-stu-id="4682b-247">Email</span></span> |<span data-ttu-id="4682b-248">String</span><span class="sxs-lookup"><span data-stu-id="4682b-248">String</span></span> |
| <span data-ttu-id="4682b-249">識別碼</span><span class="sxs-lookup"><span data-stu-id="4682b-249">Id</span></span> |<span data-ttu-id="4682b-250">String</span><span class="sxs-lookup"><span data-stu-id="4682b-250">String</span></span> |
| <span data-ttu-id="4682b-251">查閱關聯性</span><span class="sxs-lookup"><span data-stu-id="4682b-251">Lookup Relationship</span></span> |<span data-ttu-id="4682b-252">String</span><span class="sxs-lookup"><span data-stu-id="4682b-252">String</span></span> |
| <span data-ttu-id="4682b-253">複選挑選清單</span><span class="sxs-lookup"><span data-stu-id="4682b-253">Multi-Select Picklist</span></span> |<span data-ttu-id="4682b-254">String</span><span class="sxs-lookup"><span data-stu-id="4682b-254">String</span></span> |
| <span data-ttu-id="4682b-255">Number</span><span class="sxs-lookup"><span data-stu-id="4682b-255">Number</span></span> |<span data-ttu-id="4682b-256">兩倍</span><span class="sxs-lookup"><span data-stu-id="4682b-256">Double</span></span> |
| <span data-ttu-id="4682b-257">百分比</span><span class="sxs-lookup"><span data-stu-id="4682b-257">Percent</span></span> |<span data-ttu-id="4682b-258">兩倍</span><span class="sxs-lookup"><span data-stu-id="4682b-258">Double</span></span> |
| <span data-ttu-id="4682b-259">電話</span><span class="sxs-lookup"><span data-stu-id="4682b-259">Phone</span></span> |<span data-ttu-id="4682b-260">String</span><span class="sxs-lookup"><span data-stu-id="4682b-260">String</span></span> |
| <span data-ttu-id="4682b-261">挑選清單</span><span class="sxs-lookup"><span data-stu-id="4682b-261">Picklist</span></span> |<span data-ttu-id="4682b-262">String</span><span class="sxs-lookup"><span data-stu-id="4682b-262">String</span></span> |
| <span data-ttu-id="4682b-263">文字</span><span class="sxs-lookup"><span data-stu-id="4682b-263">Text</span></span> |<span data-ttu-id="4682b-264">String</span><span class="sxs-lookup"><span data-stu-id="4682b-264">String</span></span> |
| <span data-ttu-id="4682b-265">文字區域</span><span class="sxs-lookup"><span data-stu-id="4682b-265">Text Area</span></span> |<span data-ttu-id="4682b-266">String</span><span class="sxs-lookup"><span data-stu-id="4682b-266">String</span></span> |
| <span data-ttu-id="4682b-267">文字區域 (完整)</span><span class="sxs-lookup"><span data-stu-id="4682b-267">Text Area (Long)</span></span> |<span data-ttu-id="4682b-268">String</span><span class="sxs-lookup"><span data-stu-id="4682b-268">String</span></span> |
| <span data-ttu-id="4682b-269">文字區域 (豐富)</span><span class="sxs-lookup"><span data-stu-id="4682b-269">Text Area (Rich)</span></span> |<span data-ttu-id="4682b-270">String</span><span class="sxs-lookup"><span data-stu-id="4682b-270">String</span></span> |
| <span data-ttu-id="4682b-271">文字 (加密)</span><span class="sxs-lookup"><span data-stu-id="4682b-271">Text (Encrypted)</span></span> |<span data-ttu-id="4682b-272">String</span><span class="sxs-lookup"><span data-stu-id="4682b-272">String</span></span> |
| <span data-ttu-id="4682b-273">URL</span><span class="sxs-lookup"><span data-stu-id="4682b-273">URL</span></span> |<span data-ttu-id="4682b-274">String</span><span class="sxs-lookup"><span data-stu-id="4682b-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="4682b-275">若要將來自來源資料集的資料行與來自接收資料集的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="4682b-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="4682b-276">效能和微調</span><span class="sxs-lookup"><span data-stu-id="4682b-276">Performance and tuning</span></span>
<span data-ttu-id="4682b-277">若要了解 Azure Data Factory 中影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法，請參閱 [複製活動的效能及微調指南](data-factory-copy-activity-performance.md) 。</span><span class="sxs-lookup"><span data-stu-id="4682b-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
