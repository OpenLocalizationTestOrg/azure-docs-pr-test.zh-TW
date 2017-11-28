---
title: "將資料從 Salesforce aaaMove 使用 Data Factory |Microsoft 文件"
description: "深入了解如何將資料從 Salesforce toomove 使用 Azure Data Factory。"
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
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="82ec5-103">使用 Azure Data Factory 從 Salesforce 移動資料</span><span class="sxs-lookup"><span data-stu-id="82ec5-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="82ec5-104">本文概述如何使用複製活動，以及在 Azure data factory toocopy 資料從 Salesforce tooany 資料存放區中 hello hello 接收的資料行底下所列[支援來源與接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="82ec5-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="82ec5-105">這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)文件，複製活動與支援的資料存放區組合顯示的資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="82ec5-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="82ec5-106">Azure Data Factory 目前只支援將資料從 Salesforce 移過[支援接收資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)，但不支援從其他資料存放區 tooSalesforce 移動資料。</span><span class="sxs-lookup"><span data-stu-id="82ec5-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="82ec5-107">支援的版本</span><span class="sxs-lookup"><span data-stu-id="82ec5-107">Supported versions</span></span>
<span data-ttu-id="82ec5-108">此連接器支援下列 Salesforce 的版本中的 hello: Developer Edition、 專業版、 企業版或無限制的版本。</span><span class="sxs-lookup"><span data-stu-id="82ec5-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="82ec5-109">並且支援從 Salesforce 生產、沙箱和自訂網域複製。</span><span class="sxs-lookup"><span data-stu-id="82ec5-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82ec5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="82ec5-110">Prerequisites</span></span>
* <span data-ttu-id="82ec5-111">必須啟用 API 權限。</span><span class="sxs-lookup"><span data-stu-id="82ec5-111">API permission must be enabled.</span></span> <span data-ttu-id="82ec5-112">請參閱 [如何在 Salesforce 中透過權限集啟用 API 存取權？](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="82ec5-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="82ec5-113">從 Salesforce tooon 內部部署資料存放區 toocopy 資料，您必須至少在內部部署環境中安裝資料管理閘道器 2.0。</span><span class="sxs-lookup"><span data-stu-id="82ec5-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="82ec5-114">Salesforce 要求限制</span><span class="sxs-lookup"><span data-stu-id="82ec5-114">Salesforce request limits</span></span>
<span data-ttu-id="82ec5-115">Salesforce 對於 API 要求總數和並行 API 要求均有限制。</span><span class="sxs-lookup"><span data-stu-id="82ec5-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="82ec5-116">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="82ec5-116">Note hello following points:</span></span>

- <span data-ttu-id="82ec5-117">如果 hello 並行要求數目超過 hello 限制，就會發生節流，而且您會看到隨機失敗。</span><span class="sxs-lookup"><span data-stu-id="82ec5-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="82ec5-118">如果 hello 的總要求數超出 hello 限制，hello 的 Salesforce 帳戶會被封鎖 24 小時。</span><span class="sxs-lookup"><span data-stu-id="82ec5-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="82ec5-119">您也可能會收到 hello"REQUEST_LIMIT_EXCEEDED 」 錯誤，這兩種案例中。</span><span class="sxs-lookup"><span data-stu-id="82ec5-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="82ec5-120">請參閱 hello hello"應用程式開發介面要求的限制 」 一節[Salesforce 開發人員限制](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf)文件以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="82ec5-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="82ec5-121">開始使用</span><span class="sxs-lookup"><span data-stu-id="82ec5-121">Getting started</span></span>
<span data-ttu-id="82ec5-122">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 Salesforce 移動資料。</span><span class="sxs-lookup"><span data-stu-id="82ec5-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="82ec5-123">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="82ec5-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="82ec5-124">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="82ec5-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="82ec5-125">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="82ec5-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="82ec5-126">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="82ec5-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="82ec5-127">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="82ec5-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="82ec5-128">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="82ec5-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="82ec5-129">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="82ec5-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="82ec5-130">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="82ec5-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="82ec5-131">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="82ec5-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="82ec5-132">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="82ec5-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="82ec5-133">具有使用的 toocopy 資料來自 Salesforce 的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Salesforce tooAzure Blob 複製](#json-example-copy-data-from-salesforce-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="82ec5-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="82ec5-134">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooSalesforce 的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="82ec5-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="82ec5-135">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="82ec5-135">Linked service properties</span></span>
<span data-ttu-id="82ec5-136">hello 下表提供說明是特定 toohello Salesforce 連結服務的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="82ec5-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="82ec5-137">屬性</span><span class="sxs-lookup"><span data-stu-id="82ec5-137">Property</span></span> | <span data-ttu-id="82ec5-138">說明</span><span class="sxs-lookup"><span data-stu-id="82ec5-138">Description</span></span> | <span data-ttu-id="82ec5-139">必要</span><span class="sxs-lookup"><span data-stu-id="82ec5-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82ec5-140">類型</span><span class="sxs-lookup"><span data-stu-id="82ec5-140">type</span></span> |<span data-ttu-id="82ec5-141">hello 類型屬性必須設定為： **Salesforce**。</span><span class="sxs-lookup"><span data-stu-id="82ec5-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="82ec5-142">是</span><span class="sxs-lookup"><span data-stu-id="82ec5-142">Yes</span></span> |
| <span data-ttu-id="82ec5-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="82ec5-143">environmentUrl</span></span> | <span data-ttu-id="82ec5-144">指定 hello URL 的 Salesforce 執行個體。</span><span class="sxs-lookup"><span data-stu-id="82ec5-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="82ec5-145">- 預設值為 " https://login.salesforce.com "。</span><span class="sxs-lookup"><span data-stu-id="82ec5-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="82ec5-146">-從沙箱，toocopy 資料指定"https://test.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="82ec5-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="82ec5-147">-toocopy 資料從自訂網域，指定，例如，"https://[domain].my.salesforce.com"。</span><span class="sxs-lookup"><span data-stu-id="82ec5-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="82ec5-148">否</span><span class="sxs-lookup"><span data-stu-id="82ec5-148">No</span></span> |
| <span data-ttu-id="82ec5-149">username</span><span class="sxs-lookup"><span data-stu-id="82ec5-149">username</span></span> |<span data-ttu-id="82ec5-150">指定 hello 使用者帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="82ec5-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="82ec5-151">是</span><span class="sxs-lookup"><span data-stu-id="82ec5-151">Yes</span></span> |
| <span data-ttu-id="82ec5-152">password</span><span class="sxs-lookup"><span data-stu-id="82ec5-152">password</span></span> |<span data-ttu-id="82ec5-153">指定 hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="82ec5-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="82ec5-154">是</span><span class="sxs-lookup"><span data-stu-id="82ec5-154">Yes</span></span> |
| <span data-ttu-id="82ec5-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="82ec5-155">securityToken</span></span> |<span data-ttu-id="82ec5-156">指定 hello 使用者帳戶的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="82ec5-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="82ec5-157">請參閱[取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm)如需有關指示 tooreset 取得安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="82ec5-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="82ec5-158">一般情況下，請參閱關於安全性權杖的 toolearn[安全性和 hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)。</span><span class="sxs-lookup"><span data-stu-id="82ec5-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="82ec5-159">是</span><span class="sxs-lookup"><span data-stu-id="82ec5-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="82ec5-160">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="82ec5-160">Dataset properties</span></span>
<span data-ttu-id="82ec5-161">區段和屬性都可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="82ec5-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="82ec5-162">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="82ec5-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="82ec5-163">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="82ec5-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="82ec5-164">hello typeProperties 區段 hello 類型的資料集**RelationalTable**具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="82ec5-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="82ec5-165">屬性</span><span class="sxs-lookup"><span data-stu-id="82ec5-165">Property</span></span> | <span data-ttu-id="82ec5-166">說明</span><span class="sxs-lookup"><span data-stu-id="82ec5-166">Description</span></span> | <span data-ttu-id="82ec5-167">必要</span><span class="sxs-lookup"><span data-stu-id="82ec5-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82ec5-168">tableName</span><span class="sxs-lookup"><span data-stu-id="82ec5-168">tableName</span></span> |<span data-ttu-id="82ec5-169">在 Salesforce 中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="82ec5-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="82ec5-170">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="82ec5-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="82ec5-171">hello"__c"hello API 名稱部分所需的任何自訂的物件。</span><span class="sxs-lookup"><span data-stu-id="82ec5-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="82ec5-173">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="82ec5-173">Copy activity properties</span></span>
<span data-ttu-id="82ec5-174">區段和屬性都可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="82ec5-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="82ec5-175">名稱、描述、輸入和輸出資料表以及各種原則等屬性都適用於所有活動類型。</span><span class="sxs-lookup"><span data-stu-id="82ec5-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="82ec5-176">中可用的 hello 屬性 hello typeProperties > 一節的 hello 活動 hello 另一方面，每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="82ec5-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="82ec5-177">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="82ec5-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="82ec5-178">複製活動中，當 hello 來源 hello 型別的**RelationalSource** （包括 Salesforce），下列屬性的 hello 可用 typeProperties 區段中：</span><span class="sxs-lookup"><span data-stu-id="82ec5-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="82ec5-179">屬性</span><span class="sxs-lookup"><span data-stu-id="82ec5-179">Property</span></span> | <span data-ttu-id="82ec5-180">說明</span><span class="sxs-lookup"><span data-stu-id="82ec5-180">Description</span></span> | <span data-ttu-id="82ec5-181">允許的值</span><span class="sxs-lookup"><span data-stu-id="82ec5-181">Allowed values</span></span> | <span data-ttu-id="82ec5-182">必要</span><span class="sxs-lookup"><span data-stu-id="82ec5-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82ec5-183">query</span><span class="sxs-lookup"><span data-stu-id="82ec5-183">query</span></span> |<span data-ttu-id="82ec5-184">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="82ec5-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="82ec5-185">SQL-92 查詢或 [Salesforce 物件查詢語言 (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 查詢。</span><span class="sxs-lookup"><span data-stu-id="82ec5-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="82ec5-186">例如：`select * from MyTable__c`。</span><span class="sxs-lookup"><span data-stu-id="82ec5-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="82ec5-187">否 (如果 hello **tableName**的 hello**資料集**指定)</span><span class="sxs-lookup"><span data-stu-id="82ec5-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="82ec5-188">hello"__c"hello API 名稱部分所需的任何自訂的物件。</span><span class="sxs-lookup"><span data-stu-id="82ec5-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="82ec5-190">查詢秘訣</span><span class="sxs-lookup"><span data-stu-id="82ec5-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="82ec5-191">在 DateTime 資料行上使用 Where 子句來擷取資料</span><span class="sxs-lookup"><span data-stu-id="82ec5-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="82ec5-192">何時指定 hello SOQL 或 SQL 查詢，請注意 toohello 日期時間格式的差異。</span><span class="sxs-lookup"><span data-stu-id="82ec5-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="82ec5-193">例如：</span><span class="sxs-lookup"><span data-stu-id="82ec5-193">For example:</span></span>

* <span data-ttu-id="82ec5-194">**SOQL 範例**：`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="82ec5-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="82ec5-195">**SQL 範例**：</span><span class="sxs-lookup"><span data-stu-id="82ec5-195">**SQL sample**:</span></span>
    * <span data-ttu-id="82ec5-196">**使用複製精靈 toospecify hello 查詢：**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="82ec5-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="82ec5-197">**使用 JSON 編輯 toospecify hello 查詢 （逸出字元正確）：**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="82ec5-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="82ec5-198">從 Salesforce 報表擷取資料</span><span class="sxs-lookup"><span data-stu-id="82ec5-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="82ec5-199">例如，您可以藉由以 `{call "<report name>"}` 方式指定查詢，從 Salesforce 報表擷取資料。</span><span class="sxs-lookup"><span data-stu-id="82ec5-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="82ec5-200">`"query": "{call \"TestReport\"}"`。</span><span class="sxs-lookup"><span data-stu-id="82ec5-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="82ec5-201">從 Salesforce 資源回收筒擷取已刪除的記錄</span><span class="sxs-lookup"><span data-stu-id="82ec5-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="82ec5-202">來自 Salesforce 的 資源回收筒 tooquery hello 虛刪除記錄，您可以指定**"IsDeleted = 1"**在查詢中。</span><span class="sxs-lookup"><span data-stu-id="82ec5-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="82ec5-203">例如，</span><span class="sxs-lookup"><span data-stu-id="82ec5-203">For example,</span></span>

* <span data-ttu-id="82ec5-204">tooquery 只有 hello 刪除記錄，會指定 「 選取 * 從 MyTable__c**其中 IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="82ec5-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="82ec5-205">所有 hello 記錄包括現有的 hello 和刪除，hello tooquery 指定 「 選取 * 從 MyTable__c**其中 IsDeleted = 0 或 IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="82ec5-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="82ec5-206">JSON 範例： 從 Salesforce tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="82ec5-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="82ec5-207">hello 下列範例將提供範例 JSON 定義，您可以使用 toocreate 管線使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="82ec5-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="82ec5-208">它們會顯示如何從 Salesforce tooAzure Blob 儲存體 toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="82ec5-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="82ec5-209">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="82ec5-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="82ec5-210">以下是您將需要 toocreate tooimplement hello 案例 hello Data Factory 成品。</span><span class="sxs-lookup"><span data-stu-id="82ec5-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="82ec5-211">hello 以下各節 hello 清單提供關於這些步驟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="82ec5-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="82ec5-212">連結的類型之服務的 hello [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="82ec5-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="82ec5-213">連結的類型之服務的 hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="82ec5-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="82ec5-214">輸入[資料集](data-factory-create-datasets.md)hello 型別的[RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="82ec5-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="82ec5-215">輸出[資料集](data-factory-create-datasets.md)hello 型別的[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="82ec5-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="82ec5-216">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="82ec5-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="82ec5-217">**Salesforce 連結服務**</span><span class="sxs-lookup"><span data-stu-id="82ec5-217">**Salesforce linked service**</span></span>

<span data-ttu-id="82ec5-218">這個範例會使用 hello **Salesforce**連結服務。</span><span class="sxs-lookup"><span data-stu-id="82ec5-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="82ec5-219">請參閱 hello [Salesforce 連結服務](#linked-service-properties)hello 屬性這項連結服務所支援的區段。</span><span class="sxs-lookup"><span data-stu-id="82ec5-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="82ec5-220">請參閱[取得安全性權杖](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm)如需如何 tooreset/get hello 安全性權杖的指示。</span><span class="sxs-lookup"><span data-stu-id="82ec5-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

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
<span data-ttu-id="82ec5-221">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="82ec5-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="82ec5-222">**Salesforce 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="82ec5-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="82ec5-223">設定**外部**太**true**該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="82ec5-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82ec5-224">hello"__c"hello API 名稱部分所需的任何自訂的物件。</span><span class="sxs-lookup"><span data-stu-id="82ec5-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="82ec5-226">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="82ec5-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="82ec5-227">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="82ec5-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="82ec5-228">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="82ec5-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="82ec5-229">hello 管線包含設定的複製活動 toouse hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="82ec5-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="82ec5-230">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**，和 hello**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="82ec5-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="82ec5-231">請參閱[RelationalSource 類型屬性](#copy-activity-properties)的 hello hello RelationalSource 所支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="82ec5-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="82ec5-232">hello"__c"hello API 名稱部分所需的任何自訂的物件。</span><span class="sxs-lookup"><span data-stu-id="82ec5-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory - Salesforce 連線 - API 名稱](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="82ec5-234">Salesforce 的類型對應</span><span class="sxs-lookup"><span data-stu-id="82ec5-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="82ec5-235">Salesforce 類型</span><span class="sxs-lookup"><span data-stu-id="82ec5-235">Salesforce type</span></span> | <span data-ttu-id="82ec5-236">以 .NET 為基礎的類型</span><span class="sxs-lookup"><span data-stu-id="82ec5-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="82ec5-237">自動編號</span><span class="sxs-lookup"><span data-stu-id="82ec5-237">Auto Number</span></span> |<span data-ttu-id="82ec5-238">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-238">String</span></span> |
| <span data-ttu-id="82ec5-239">核取方塊</span><span class="sxs-lookup"><span data-stu-id="82ec5-239">Checkbox</span></span> |<span data-ttu-id="82ec5-240">Boolean</span><span class="sxs-lookup"><span data-stu-id="82ec5-240">Boolean</span></span> |
| <span data-ttu-id="82ec5-241">貨幣</span><span class="sxs-lookup"><span data-stu-id="82ec5-241">Currency</span></span> |<span data-ttu-id="82ec5-242">兩倍</span><span class="sxs-lookup"><span data-stu-id="82ec5-242">Double</span></span> |
| <span data-ttu-id="82ec5-243">日期</span><span class="sxs-lookup"><span data-stu-id="82ec5-243">Date</span></span> |<span data-ttu-id="82ec5-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="82ec5-244">DateTime</span></span> |
| <span data-ttu-id="82ec5-245">日期/時間</span><span class="sxs-lookup"><span data-stu-id="82ec5-245">Date/Time</span></span> |<span data-ttu-id="82ec5-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="82ec5-246">DateTime</span></span> |
| <span data-ttu-id="82ec5-247">電子郵件</span><span class="sxs-lookup"><span data-stu-id="82ec5-247">Email</span></span> |<span data-ttu-id="82ec5-248">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-248">String</span></span> |
| <span data-ttu-id="82ec5-249">識別碼</span><span class="sxs-lookup"><span data-stu-id="82ec5-249">Id</span></span> |<span data-ttu-id="82ec5-250">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-250">String</span></span> |
| <span data-ttu-id="82ec5-251">查閱關聯性</span><span class="sxs-lookup"><span data-stu-id="82ec5-251">Lookup Relationship</span></span> |<span data-ttu-id="82ec5-252">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-252">String</span></span> |
| <span data-ttu-id="82ec5-253">複選挑選清單</span><span class="sxs-lookup"><span data-stu-id="82ec5-253">Multi-Select Picklist</span></span> |<span data-ttu-id="82ec5-254">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-254">String</span></span> |
| <span data-ttu-id="82ec5-255">Number</span><span class="sxs-lookup"><span data-stu-id="82ec5-255">Number</span></span> |<span data-ttu-id="82ec5-256">兩倍</span><span class="sxs-lookup"><span data-stu-id="82ec5-256">Double</span></span> |
| <span data-ttu-id="82ec5-257">百分比</span><span class="sxs-lookup"><span data-stu-id="82ec5-257">Percent</span></span> |<span data-ttu-id="82ec5-258">兩倍</span><span class="sxs-lookup"><span data-stu-id="82ec5-258">Double</span></span> |
| <span data-ttu-id="82ec5-259">電話</span><span class="sxs-lookup"><span data-stu-id="82ec5-259">Phone</span></span> |<span data-ttu-id="82ec5-260">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-260">String</span></span> |
| <span data-ttu-id="82ec5-261">挑選清單</span><span class="sxs-lookup"><span data-stu-id="82ec5-261">Picklist</span></span> |<span data-ttu-id="82ec5-262">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-262">String</span></span> |
| <span data-ttu-id="82ec5-263">文字</span><span class="sxs-lookup"><span data-stu-id="82ec5-263">Text</span></span> |<span data-ttu-id="82ec5-264">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-264">String</span></span> |
| <span data-ttu-id="82ec5-265">文字區域</span><span class="sxs-lookup"><span data-stu-id="82ec5-265">Text Area</span></span> |<span data-ttu-id="82ec5-266">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-266">String</span></span> |
| <span data-ttu-id="82ec5-267">文字區域 (完整)</span><span class="sxs-lookup"><span data-stu-id="82ec5-267">Text Area (Long)</span></span> |<span data-ttu-id="82ec5-268">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-268">String</span></span> |
| <span data-ttu-id="82ec5-269">文字區域 (豐富)</span><span class="sxs-lookup"><span data-stu-id="82ec5-269">Text Area (Rich)</span></span> |<span data-ttu-id="82ec5-270">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-270">String</span></span> |
| <span data-ttu-id="82ec5-271">文字 (加密)</span><span class="sxs-lookup"><span data-stu-id="82ec5-271">Text (Encrypted)</span></span> |<span data-ttu-id="82ec5-272">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-272">String</span></span> |
| <span data-ttu-id="82ec5-273">URL</span><span class="sxs-lookup"><span data-stu-id="82ec5-273">URL</span></span> |<span data-ttu-id="82ec5-274">String</span><span class="sxs-lookup"><span data-stu-id="82ec5-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="82ec5-275">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="82ec5-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="82ec5-276">效能和微調</span><span class="sxs-lookup"><span data-stu-id="82ec5-276">Performance and tuning</span></span>
<span data-ttu-id="82ec5-277">請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="82ec5-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
