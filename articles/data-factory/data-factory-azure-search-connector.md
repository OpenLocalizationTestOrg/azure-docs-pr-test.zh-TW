---
title: "使用 Data Factory aaaPush 資料 tooSearch 索引 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 toopush 資料 tooAzure 搜尋索引。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="be583-103">藉由使用 Azure Data Factory 推播資料 tooan Azure 搜尋索引</span><span class="sxs-lookup"><span data-stu-id="be583-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="be583-104">本文說明如何 toouse hello 複製活動 toopush 資料從支援的來源資料存放區 tooAzure 搜尋索引。</span><span class="sxs-lookup"><span data-stu-id="be583-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="be583-105">支援的來源資料存放區會列在 hello 來源資料行的 hello[支援來源與接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="be583-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="be583-106">這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)文件，複製活動與支援的資料存放區組合顯示的資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="be583-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="be583-107">啟用連線</span><span class="sxs-lookup"><span data-stu-id="be583-107">Enabling connectivity</span></span>
<span data-ttu-id="be583-108">tooallow Data Factory 服務連接到 tooan 在內部部署資料存放區，您在內部部署環境中安裝資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="be583-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="be583-109">您可以在 hello 裝載 hello 來源資料的同一部電腦儲存，或在不同的機器 tooavoid 競用資源的 hello 資料存放區上安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="be583-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="be583-110">資料管理閘道器會在內部部署資料來源 toocloud 服務連接安全且受管理的方式。</span><span class="sxs-lookup"><span data-stu-id="be583-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="be583-111">如需資料管理閘道的詳細資訊，請參閱 [在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="be583-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="be583-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="be583-112">Getting started</span></span>
<span data-ttu-id="be583-113">您可以建立管線，與使用不同的工具 Api 會將資料從來源資料存放區 tooAzure 搜尋索引推送複製活動。</span><span class="sxs-lookup"><span data-stu-id="be583-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="be583-114">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="be583-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="be583-115">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="be583-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="be583-116">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="be583-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="be583-117">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="be583-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="be583-118">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="be583-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="be583-119">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="be583-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="be583-120">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="be583-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="be583-121">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="be583-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="be583-122">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="be583-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="be583-123">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="be583-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="be583-124">具有使用的 toocopy 資料 tooAzure 搜尋索引的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從內部部署 SQL Server tooAzure 搜尋索引複製](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index)本文一節。</span><span class="sxs-lookup"><span data-stu-id="be583-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="be583-125">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure 搜尋索引的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="be583-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="be583-126">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="be583-126">Linked service properties</span></span>

<span data-ttu-id="be583-127">hello 下表提供說明屬於特定 toohello 連結的 Azure 搜尋服務的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="be583-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="be583-128">屬性</span><span class="sxs-lookup"><span data-stu-id="be583-128">Property</span></span> | <span data-ttu-id="be583-129">說明</span><span class="sxs-lookup"><span data-stu-id="be583-129">Description</span></span> | <span data-ttu-id="be583-130">必要</span><span class="sxs-lookup"><span data-stu-id="be583-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="be583-131">類型</span><span class="sxs-lookup"><span data-stu-id="be583-131">type</span></span> | <span data-ttu-id="be583-132">hello 類型屬性必須設定為： **AzureSearch**。</span><span class="sxs-lookup"><span data-stu-id="be583-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="be583-133">是</span><span class="sxs-lookup"><span data-stu-id="be583-133">Yes</span></span> |
| <span data-ttu-id="be583-134">url</span><span class="sxs-lookup"><span data-stu-id="be583-134">url</span></span> | <span data-ttu-id="be583-135">Hello Azure 搜尋服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="be583-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="be583-136">是</span><span class="sxs-lookup"><span data-stu-id="be583-136">Yes</span></span> |
| <span data-ttu-id="be583-137">key</span><span class="sxs-lookup"><span data-stu-id="be583-137">key</span></span> | <span data-ttu-id="be583-138">Hello Azure 搜尋服務的管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="be583-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="be583-139">是</span><span class="sxs-lookup"><span data-stu-id="be583-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="be583-140">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="be583-140">Dataset properties</span></span>

<span data-ttu-id="be583-141">區段和屬性都可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="be583-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="be583-142">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="be583-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="be583-143">hello **typeProperties**區段是不同的資料集的每個型別。</span><span class="sxs-lookup"><span data-stu-id="be583-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="be583-144">hello typeProperties 區段 hello 類型的資料集**AzureSearchIndex**具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="be583-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="be583-145">屬性</span><span class="sxs-lookup"><span data-stu-id="be583-145">Property</span></span> | <span data-ttu-id="be583-146">說明</span><span class="sxs-lookup"><span data-stu-id="be583-146">Description</span></span> | <span data-ttu-id="be583-147">必要</span><span class="sxs-lookup"><span data-stu-id="be583-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="be583-148">類型</span><span class="sxs-lookup"><span data-stu-id="be583-148">type</span></span> | <span data-ttu-id="be583-149">hello type 屬性必須設定得**AzureSearchIndex**。</span><span class="sxs-lookup"><span data-stu-id="be583-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="be583-150">是</span><span class="sxs-lookup"><span data-stu-id="be583-150">Yes</span></span> |
| <span data-ttu-id="be583-151">IndexName</span><span class="sxs-lookup"><span data-stu-id="be583-151">indexName</span></span> | <span data-ttu-id="be583-152">Hello Azure 搜尋索引的名稱。</span><span class="sxs-lookup"><span data-stu-id="be583-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="be583-153">Data Factory 不會建立 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="be583-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="be583-154">hello 索引必須存在於 Azure 搜尋中。</span><span class="sxs-lookup"><span data-stu-id="be583-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="be583-155">是</span><span class="sxs-lookup"><span data-stu-id="be583-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="be583-156">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="be583-156">Copy activity properties</span></span>
<span data-ttu-id="be583-157">區段和屬性都可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="be583-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="be583-158">屬性 (例如名稱、描述、輸入和輸出資料表，以及各種原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="be583-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="be583-159">而 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="be583-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="be583-160">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="be583-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="be583-161">複製活動 hello 接收器是 hello 類型時的**AzureSearchIndexSink**，typeProperties 節中會使用下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="be583-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="be583-162">屬性</span><span class="sxs-lookup"><span data-stu-id="be583-162">Property</span></span> | <span data-ttu-id="be583-163">說明</span><span class="sxs-lookup"><span data-stu-id="be583-163">Description</span></span> | <span data-ttu-id="be583-164">允許的值</span><span class="sxs-lookup"><span data-stu-id="be583-164">Allowed values</span></span> | <span data-ttu-id="be583-165">必要</span><span class="sxs-lookup"><span data-stu-id="be583-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="be583-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="be583-166">WriteBehavior</span></span> | <span data-ttu-id="be583-167">指定是否 toomerge 或取代文件時已存在於 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="be583-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="be583-168">請參閱 hello [WriteBehavior 屬性](#writebehavior-property)。</span><span class="sxs-lookup"><span data-stu-id="be583-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="be583-169">合併 (預設值)</span><span class="sxs-lookup"><span data-stu-id="be583-169">Merge (default)</span></span><br/><span data-ttu-id="be583-170">上傳</span><span class="sxs-lookup"><span data-stu-id="be583-170">Upload</span></span>| <span data-ttu-id="be583-171">否</span><span class="sxs-lookup"><span data-stu-id="be583-171">No</span></span> |
| <span data-ttu-id="be583-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="be583-172">WriteBatchSize</span></span> | <span data-ttu-id="be583-173">將資料上傳至 hello Azure 搜尋索引，當 hello 緩衝區大小到達叫用 writeBatchSize 時。</span><span class="sxs-lookup"><span data-stu-id="be583-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="be583-174">請參閱 hello[叫用 WriteBatchSize 屬性](#writebatchsize-property)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="be583-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="be583-175">1 too1，000。</span><span class="sxs-lookup"><span data-stu-id="be583-175">1 too1,000.</span></span> <span data-ttu-id="be583-176">預設值為 1000。</span><span class="sxs-lookup"><span data-stu-id="be583-176">Default value is 1000.</span></span> | <span data-ttu-id="be583-177">否</span><span class="sxs-lookup"><span data-stu-id="be583-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="be583-178">WriteBehavior 屬性</span><span class="sxs-lookup"><span data-stu-id="be583-178">WriteBehavior property</span></span>
<span data-ttu-id="be583-179">AzureSearchSink 會在寫入資料時更新插入。</span><span class="sxs-lookup"><span data-stu-id="be583-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="be583-180">換句話說，在撰寫文件中，如果 hello 文件索引鍵已存在於 hello Azure 搜尋索引時，Azure 搜尋更新 hello 現有文件，而不是擲回衝突例外狀況。</span><span class="sxs-lookup"><span data-stu-id="be583-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="be583-181">hello AzureSearchSink 提供下列兩種 upsert 行為 （藉由使用 AzureSearch SDK） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="be583-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="be583-182">**合併**: hello 新文件中的所有 hello 資料行都結合現有的其中一個 hello。</span><span class="sxs-lookup"><span data-stu-id="be583-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="be583-183">若是 hello 新文件中的 null 值的資料行，則會保留 hello hello 現有的其中一個值。</span><span class="sxs-lookup"><span data-stu-id="be583-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="be583-184">**上傳**: hello 新文件取代 hello 現有的我的最愛。</span><span class="sxs-lookup"><span data-stu-id="be583-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="be583-185">Hello 新文件中未指定資料行，hello 值設定 toonull 是否有非 null 值 hello 現有文件中。</span><span class="sxs-lookup"><span data-stu-id="be583-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="be583-186">hello 預設行為是**合併**。</span><span class="sxs-lookup"><span data-stu-id="be583-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="be583-187">WriteBatchSize 屬性</span><span class="sxs-lookup"><span data-stu-id="be583-187">WriteBatchSize Property</span></span>
<span data-ttu-id="be583-188">Azure 搜尋服務支援批次寫入文件。</span><span class="sxs-lookup"><span data-stu-id="be583-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="be583-189">批次可包含 1 too1，000 動作。</span><span class="sxs-lookup"><span data-stu-id="be583-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="be583-190">動作會處理一個文件 tooperform hello 上傳/合併作業。</span><span class="sxs-lookup"><span data-stu-id="be583-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="be583-191">資料類型支援</span><span class="sxs-lookup"><span data-stu-id="be583-191">Data type support</span></span>
<span data-ttu-id="be583-192">hello 下表會指定是否支援的 Azure 搜尋資料類型。</span><span class="sxs-lookup"><span data-stu-id="be583-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="be583-193">Azure 搜尋服務資料類型</span><span class="sxs-lookup"><span data-stu-id="be583-193">Azure Search data type</span></span> | <span data-ttu-id="be583-194">在 Azure 搜尋服務接收器中受到支援</span><span class="sxs-lookup"><span data-stu-id="be583-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="be583-195">String</span><span class="sxs-lookup"><span data-stu-id="be583-195">String</span></span> | <span data-ttu-id="be583-196">Y</span><span class="sxs-lookup"><span data-stu-id="be583-196">Y</span></span> |
| <span data-ttu-id="be583-197">Int32</span><span class="sxs-lookup"><span data-stu-id="be583-197">Int32</span></span> | <span data-ttu-id="be583-198">Y</span><span class="sxs-lookup"><span data-stu-id="be583-198">Y</span></span> |
| <span data-ttu-id="be583-199">Int64</span><span class="sxs-lookup"><span data-stu-id="be583-199">Int64</span></span> | <span data-ttu-id="be583-200">Y</span><span class="sxs-lookup"><span data-stu-id="be583-200">Y</span></span> |
| <span data-ttu-id="be583-201">兩倍</span><span class="sxs-lookup"><span data-stu-id="be583-201">Double</span></span> | <span data-ttu-id="be583-202">Y</span><span class="sxs-lookup"><span data-stu-id="be583-202">Y</span></span> |
| <span data-ttu-id="be583-203">Boolean</span><span class="sxs-lookup"><span data-stu-id="be583-203">Boolean</span></span> | <span data-ttu-id="be583-204">Y</span><span class="sxs-lookup"><span data-stu-id="be583-204">Y</span></span> |
| <span data-ttu-id="be583-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="be583-205">DataTimeOffset</span></span> | <span data-ttu-id="be583-206">Y</span><span class="sxs-lookup"><span data-stu-id="be583-206">Y</span></span> |
| <span data-ttu-id="be583-207">字串陣列</span><span class="sxs-lookup"><span data-stu-id="be583-207">String Array</span></span> | <span data-ttu-id="be583-208">N</span><span class="sxs-lookup"><span data-stu-id="be583-208">N</span></span> |
| <span data-ttu-id="be583-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="be583-209">GeographyPoint</span></span> | <span data-ttu-id="be583-210">N</span><span class="sxs-lookup"><span data-stu-id="be583-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="be583-211">JSON 範例： 將資料從內部部署 SQL Server tooAzure 搜尋索引複製</span><span class="sxs-lookup"><span data-stu-id="be583-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="be583-212">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="be583-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="be583-213">[AzureSearch](#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="be583-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="be583-214">[OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="be583-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="be583-215">[SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="be583-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="be583-216">[AzureSearchIndex](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="be583-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="be583-217">具有使用 [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) 和 [AzureSearchIndexSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="be583-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="be583-218">hello 範例從內部部署 SQL Server 資料庫 tooan Azure 搜尋索引複製時間序列資料的每小時。</span><span class="sxs-lookup"><span data-stu-id="be583-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="be583-219">此範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="be583-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="be583-220">第一個步驟中，安裝程式在內部部署電腦上的 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="be583-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="be583-221">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="be583-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="be583-222">**Azure 搜尋服務連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="be583-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="be583-223">**SQL Server 連結服務**</span><span class="sxs-lookup"><span data-stu-id="be583-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="be583-224">**SQL Server 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="be583-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="be583-225">hello 範例假設您已建立資料表"MyTable"SQL Server 中，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="be583-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="be583-226">您可以透過 hello hello 資料集的 tableName typeProperty 必須使用相同的資料庫，使用單一資料集，但單一資料表內的多個資料表進行查詢。</span><span class="sxs-lookup"><span data-stu-id="be583-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="be583-227">設定"external":"true"會通知 Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="be583-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="be583-228">**Azure 搜尋服務輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="be583-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="be583-229">hello 範例複本資料 tooan Azure 搜尋索引名為**產品**。</span><span class="sxs-lookup"><span data-stu-id="be583-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="be583-230">Data Factory 不會建立 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="be583-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="be583-231">tootest hello 範例，請使用此名稱建立索引。</span><span class="sxs-lookup"><span data-stu-id="be583-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="be583-232">建立 hello Azure 搜尋索引以 hello 與 hello 輸入資料集的資料行數目相同。</span><span class="sxs-lookup"><span data-stu-id="be583-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="be583-233">新的項目會加入 toohello Azure 搜尋索引的每個小時。</span><span class="sxs-lookup"><span data-stu-id="be583-233">New entries are added toohello Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="be583-234">**具有 SQL 來源和「Azure 搜尋索引」接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="be583-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="be583-235">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="be583-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="be583-236">在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**和**接收**類型設定得**AzureSearchIndexSink**。</span><span class="sxs-lookup"><span data-stu-id="be583-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="be583-237">指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="be583-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="be583-238">如果您從雲端資料存放區將資料複製到 Azure 搜尋服務，則 `executionLocation` 是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="be583-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="be583-239">hello 下列 JSON 片段顯示需要在複製活動的 hello 變更`typeProperties`做為範例。</span><span class="sxs-lookup"><span data-stu-id="be583-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="be583-240">參閱[在雲端資料存放區之間複製資料](data-factory-data-movement-activities.md#global)一節以取得支援的值和更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="be583-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="be583-241">從雲端來源複製</span><span class="sxs-lookup"><span data-stu-id="be583-241">Copy from a cloud source</span></span>
<span data-ttu-id="be583-242">如果您從雲端資料存放區將資料複製到 Azure 搜尋服務，則 `executionLocation` 是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="be583-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="be583-243">hello 下列 JSON 片段顯示需要在複製活動的 hello 變更`typeProperties`做為範例。</span><span class="sxs-lookup"><span data-stu-id="be583-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="be583-244">參閱[在雲端資料存放區之間複製資料](data-factory-data-movement-activities.md#global)一節以取得支援的值和更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="be583-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="be583-245">您也可以將對應從來源資料集 toocolumns 接收 hello 複製活動定義中的資料集的資料行。</span><span class="sxs-lookup"><span data-stu-id="be583-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="be583-246">如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="be583-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="be583-247">效能和微調</span><span class="sxs-lookup"><span data-stu-id="be583-247">Performance and tuning</span></span>  
<span data-ttu-id="be583-248">請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="be583-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be583-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be583-249">Next steps</span></span>
<span data-ttu-id="be583-250">請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="be583-250">See hello following articles:</span></span>

* <span data-ttu-id="be583-251">[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得使用「複製活動」來建立管線的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="be583-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
