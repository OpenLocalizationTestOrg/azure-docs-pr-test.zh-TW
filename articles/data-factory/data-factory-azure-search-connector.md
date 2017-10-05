---
title: "使用 Data Factory將資料推送到搜尋索引 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory，將資料推送到 Azure 搜尋服務索引。"
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
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="298d2-103">使用 Azure Data Factory 將資料推送到 Azure 搜尋服務索引</span><span class="sxs-lookup"><span data-stu-id="298d2-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="298d2-104">本文說明如何使用「複製活動」，將資料從支援的來源資料存放區推送到「Azure 搜尋」索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="298d2-105">支援的來源資料存放區會列於[支援的來源與接收器](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格的 [來源] 欄中。</span><span class="sxs-lookup"><span data-stu-id="298d2-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="298d2-106">本文是根據 [資料移動活動](data-factory-data-movement-activities.md) 一文，該文呈現使用複製活動移動資料的一般概觀以及支援的資料存放區組合。</span><span class="sxs-lookup"><span data-stu-id="298d2-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="298d2-107">啟用連線</span><span class="sxs-lookup"><span data-stu-id="298d2-107">Enabling connectivity</span></span>
<span data-ttu-id="298d2-108">若要讓 Data Factory 服務連接到內部部署資料存放區，您要在內部部署環境中安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="298d2-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="298d2-109">您可以在裝載來源資料存放區的同一部電腦上或個別電腦上安裝閘道，以避免與資料存放區競用資源。</span><span class="sxs-lookup"><span data-stu-id="298d2-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="298d2-110">資料管理閘道會透過安全且可管理的方式，將內部部署資料來源連接到雲端服務。</span><span class="sxs-lookup"><span data-stu-id="298d2-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="298d2-111">如需資料管理閘道的詳細資訊，請參閱 [在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="298d2-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="298d2-112">開始使用</span><span class="sxs-lookup"><span data-stu-id="298d2-112">Getting started</span></span>
<span data-ttu-id="298d2-113">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料從來源資料存放區推送到「Azure 搜尋」索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="298d2-114">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="298d2-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="298d2-115">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="298d2-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="298d2-116">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="298d2-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="298d2-117">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="298d2-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="298d2-118">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="298d2-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="298d2-119">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="298d2-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="298d2-120">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="298d2-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="298d2-121">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="298d2-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="298d2-122">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="298d2-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="298d2-123">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="298d2-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="298d2-124">如需相關範例，其中含有用來將資料複製到「Azure 搜尋」索引之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從內部部署 SQL Server 複製到 Azure 搜尋索引](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index)一節。</span><span class="sxs-lookup"><span data-stu-id="298d2-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="298d2-125">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義「Azure 搜尋索引」特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="298d2-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="298d2-126">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="298d2-126">Linked service properties</span></span>

<span data-ttu-id="298d2-127">下表提供 Azure 搜尋服務連結服務專屬之 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="298d2-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="298d2-128">屬性</span><span class="sxs-lookup"><span data-stu-id="298d2-128">Property</span></span> | <span data-ttu-id="298d2-129">說明</span><span class="sxs-lookup"><span data-stu-id="298d2-129">Description</span></span> | <span data-ttu-id="298d2-130">必要</span><span class="sxs-lookup"><span data-stu-id="298d2-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="298d2-131">類型</span><span class="sxs-lookup"><span data-stu-id="298d2-131">type</span></span> | <span data-ttu-id="298d2-132">type 屬性必須設為：**AzureSearch**。</span><span class="sxs-lookup"><span data-stu-id="298d2-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="298d2-133">yes</span><span class="sxs-lookup"><span data-stu-id="298d2-133">Yes</span></span> |
| <span data-ttu-id="298d2-134">URL</span><span class="sxs-lookup"><span data-stu-id="298d2-134">url</span></span> | <span data-ttu-id="298d2-135">Azure 搜尋服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="298d2-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="298d2-136">是</span><span class="sxs-lookup"><span data-stu-id="298d2-136">Yes</span></span> |
| <span data-ttu-id="298d2-137">key</span><span class="sxs-lookup"><span data-stu-id="298d2-137">key</span></span> | <span data-ttu-id="298d2-138">Azure 搜尋服務的系統管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="298d2-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="298d2-139">是</span><span class="sxs-lookup"><span data-stu-id="298d2-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="298d2-140">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="298d2-140">Dataset properties</span></span>

<span data-ttu-id="298d2-141">如需定義資料集的區段和屬性完整清單，請參閱 [建立資料集](data-factory-create-datasets.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="298d2-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="298d2-142">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="298d2-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="298d2-143">不同類型資料集的 **typeProperties** 區段不同。</span><span class="sxs-lookup"><span data-stu-id="298d2-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="298d2-144">**AzureSearchIndex** 類型資料集的 typeProperties 區段有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="298d2-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="298d2-145">屬性</span><span class="sxs-lookup"><span data-stu-id="298d2-145">Property</span></span> | <span data-ttu-id="298d2-146">說明</span><span class="sxs-lookup"><span data-stu-id="298d2-146">Description</span></span> | <span data-ttu-id="298d2-147">必要</span><span class="sxs-lookup"><span data-stu-id="298d2-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="298d2-148">類型</span><span class="sxs-lookup"><span data-stu-id="298d2-148">type</span></span> | <span data-ttu-id="298d2-149">type 屬性必須設為 **AzureSearchIndex**。</span><span class="sxs-lookup"><span data-stu-id="298d2-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="298d2-150">yes</span><span class="sxs-lookup"><span data-stu-id="298d2-150">Yes</span></span> |
| <span data-ttu-id="298d2-151">IndexName</span><span class="sxs-lookup"><span data-stu-id="298d2-151">indexName</span></span> | <span data-ttu-id="298d2-152">Azure 搜尋服務索引的名稱。</span><span class="sxs-lookup"><span data-stu-id="298d2-152">Name of the Azure Search index.</span></span> <span data-ttu-id="298d2-153">Data Factory 不會建立索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-153">Data Factory does not create the index.</span></span> <span data-ttu-id="298d2-154">索引必須存在於 Azure 搜尋服務中。</span><span class="sxs-lookup"><span data-stu-id="298d2-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="298d2-155">是</span><span class="sxs-lookup"><span data-stu-id="298d2-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="298d2-156">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="298d2-156">Copy activity properties</span></span>
<span data-ttu-id="298d2-157">如需定義活動的區段和屬性完整清單，請參閱 [建立管線](data-factory-create-pipelines.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="298d2-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="298d2-158">屬性 (例如名稱、描述、輸入和輸出資料表，以及各種原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="298d2-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="298d2-159">而 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="298d2-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="298d2-160">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="298d2-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="298d2-161">對於「複製活動」，當接收的類型為 **AzureSearchIndexSink** 時，typeProperties 區段中會有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="298d2-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="298d2-162">屬性</span><span class="sxs-lookup"><span data-stu-id="298d2-162">Property</span></span> | <span data-ttu-id="298d2-163">說明</span><span class="sxs-lookup"><span data-stu-id="298d2-163">Description</span></span> | <span data-ttu-id="298d2-164">允許的值</span><span class="sxs-lookup"><span data-stu-id="298d2-164">Allowed values</span></span> | <span data-ttu-id="298d2-165">必要</span><span class="sxs-lookup"><span data-stu-id="298d2-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="298d2-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="298d2-166">WriteBehavior</span></span> | <span data-ttu-id="298d2-167">指定若文件已經存在於索引中，是否要合併或取代。</span><span class="sxs-lookup"><span data-stu-id="298d2-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="298d2-168">請參閱 [WriteBehavior 屬性](#writebehavior-property)。</span><span class="sxs-lookup"><span data-stu-id="298d2-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="298d2-169">合併 (預設值)</span><span class="sxs-lookup"><span data-stu-id="298d2-169">Merge (default)</span></span><br/><span data-ttu-id="298d2-170">上傳</span><span class="sxs-lookup"><span data-stu-id="298d2-170">Upload</span></span>| <span data-ttu-id="298d2-171">否</span><span class="sxs-lookup"><span data-stu-id="298d2-171">No</span></span> |
| <span data-ttu-id="298d2-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="298d2-172">WriteBatchSize</span></span> | <span data-ttu-id="298d2-173">當緩衝區大小達到 writeBatchSize 時，將資料上傳至 Azure 搜尋服務中。</span><span class="sxs-lookup"><span data-stu-id="298d2-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="298d2-174">如需詳細資訊，請參閱 [WriteBatchSize 屬性](#writebatchsize-property)。</span><span class="sxs-lookup"><span data-stu-id="298d2-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="298d2-175">1 到 1000。</span><span class="sxs-lookup"><span data-stu-id="298d2-175">1 to 1,000.</span></span> <span data-ttu-id="298d2-176">預設值為 1000。</span><span class="sxs-lookup"><span data-stu-id="298d2-176">Default value is 1000.</span></span> | <span data-ttu-id="298d2-177">否</span><span class="sxs-lookup"><span data-stu-id="298d2-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="298d2-178">WriteBehavior 屬性</span><span class="sxs-lookup"><span data-stu-id="298d2-178">WriteBehavior property</span></span>
<span data-ttu-id="298d2-179">AzureSearchSink 會在寫入資料時更新插入。</span><span class="sxs-lookup"><span data-stu-id="298d2-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="298d2-180">換句話說，在撰寫文件時，如果文件索引鍵已經存在於 Azure 搜尋服務索引中，Azure 搜尋服務就會更新現有的文件，而不是擲回衝突例外狀況。</span><span class="sxs-lookup"><span data-stu-id="298d2-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="298d2-181">AzureSearchSink (藉由使用 AzureSearch SDK) 提供下列兩種更新插入行為：</span><span class="sxs-lookup"><span data-stu-id="298d2-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="298d2-182">**合併**︰將新文件中的所有資料行與現有的文件相結合。</span><span class="sxs-lookup"><span data-stu-id="298d2-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="298d2-183">對於新文件中含有 null 值的資料行，則會保留現有文件中的值。</span><span class="sxs-lookup"><span data-stu-id="298d2-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="298d2-184">**上傳**：新的文件會取代現有的文件。</span><span class="sxs-lookup"><span data-stu-id="298d2-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="298d2-185">針對新文件中未指定的資料行，不論現有的文件中是否具有非 null 的值，都會將值設為 null。</span><span class="sxs-lookup"><span data-stu-id="298d2-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="298d2-186">預設行為是**合併**。</span><span class="sxs-lookup"><span data-stu-id="298d2-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="298d2-187">WriteBatchSize 屬性</span><span class="sxs-lookup"><span data-stu-id="298d2-187">WriteBatchSize Property</span></span>
<span data-ttu-id="298d2-188">Azure 搜尋服務支援批次寫入文件。</span><span class="sxs-lookup"><span data-stu-id="298d2-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="298d2-189">一個批次可包含 1 到 1,000 個動作。</span><span class="sxs-lookup"><span data-stu-id="298d2-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="298d2-190">一個動作可指示一份文件來執行上傳/合併作業。</span><span class="sxs-lookup"><span data-stu-id="298d2-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="298d2-191">資料類型支援</span><span class="sxs-lookup"><span data-stu-id="298d2-191">Data type support</span></span>
<span data-ttu-id="298d2-192">下表指出是否支援 Azure 搜尋服務資料類型。</span><span class="sxs-lookup"><span data-stu-id="298d2-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="298d2-193">Azure 搜尋服務資料類型</span><span class="sxs-lookup"><span data-stu-id="298d2-193">Azure Search data type</span></span> | <span data-ttu-id="298d2-194">在 Azure 搜尋服務接收器中受到支援</span><span class="sxs-lookup"><span data-stu-id="298d2-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="298d2-195">String</span><span class="sxs-lookup"><span data-stu-id="298d2-195">String</span></span> | <span data-ttu-id="298d2-196">Y</span><span class="sxs-lookup"><span data-stu-id="298d2-196">Y</span></span> |
| <span data-ttu-id="298d2-197">Int32</span><span class="sxs-lookup"><span data-stu-id="298d2-197">Int32</span></span> | <span data-ttu-id="298d2-198">Y</span><span class="sxs-lookup"><span data-stu-id="298d2-198">Y</span></span> |
| <span data-ttu-id="298d2-199">Int64</span><span class="sxs-lookup"><span data-stu-id="298d2-199">Int64</span></span> | <span data-ttu-id="298d2-200">Y</span><span class="sxs-lookup"><span data-stu-id="298d2-200">Y</span></span> |
| <span data-ttu-id="298d2-201">兩倍</span><span class="sxs-lookup"><span data-stu-id="298d2-201">Double</span></span> | <span data-ttu-id="298d2-202">Y</span><span class="sxs-lookup"><span data-stu-id="298d2-202">Y</span></span> |
| <span data-ttu-id="298d2-203">Boolean</span><span class="sxs-lookup"><span data-stu-id="298d2-203">Boolean</span></span> | <span data-ttu-id="298d2-204">Y</span><span class="sxs-lookup"><span data-stu-id="298d2-204">Y</span></span> |
| <span data-ttu-id="298d2-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="298d2-205">DataTimeOffset</span></span> | <span data-ttu-id="298d2-206">Y</span><span class="sxs-lookup"><span data-stu-id="298d2-206">Y</span></span> |
| <span data-ttu-id="298d2-207">字串陣列</span><span class="sxs-lookup"><span data-stu-id="298d2-207">String Array</span></span> | <span data-ttu-id="298d2-208">N</span><span class="sxs-lookup"><span data-stu-id="298d2-208">N</span></span> |
| <span data-ttu-id="298d2-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="298d2-209">GeographyPoint</span></span> | <span data-ttu-id="298d2-210">N</span><span class="sxs-lookup"><span data-stu-id="298d2-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="298d2-211">JSON 範例：將資料從內部部署 SQL Server 複製到 Azure 搜尋索引</span><span class="sxs-lookup"><span data-stu-id="298d2-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="298d2-212">下列範例顯示︰</span><span class="sxs-lookup"><span data-stu-id="298d2-212">The following sample shows:</span></span>

1.  <span data-ttu-id="298d2-213">[AzureSearch](#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="298d2-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="298d2-214">[OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="298d2-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="298d2-215">[SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="298d2-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="298d2-216">[AzureSearchIndex](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="298d2-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="298d2-217">具有使用 [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) 和 [AzureSearchIndexSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="298d2-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="298d2-218">這個範例每小時都會將時間序列的資料從內部部署 SQL Server 資料庫複製到 Azure 搜尋服務索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="298d2-219">範例後面的各節將會說明此範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="298d2-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="298d2-220">第一步是在內部部署電腦上設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="298d2-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="298d2-221">如需相關指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="298d2-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="298d2-222">**Azure 搜尋服務連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="298d2-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="298d2-223">**SQL Server 連結服務**</span><span class="sxs-lookup"><span data-stu-id="298d2-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="298d2-224">**SQL Server 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="298d2-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="298d2-225">此範例假設您已在 SQL Server 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="298d2-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="298d2-226">您可以使用單一資料集來查詢相同資料庫內的多個資料表，但針對資料集的 tableName typeProperty 必須使用單一資料表。</span><span class="sxs-lookup"><span data-stu-id="298d2-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="298d2-227">設定 “external”: ”true” 可讓 Data Factory 服務知道資料集是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="298d2-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="298d2-228">**Azure 搜尋服務輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="298d2-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="298d2-229">此範例會將資料複製到名為 **products** 的 Azure 搜尋服務索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="298d2-230">Data Factory 不會建立索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-230">Data Factory does not create the index.</span></span> <span data-ttu-id="298d2-231">若要測試範例，請以此名稱建立索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="298d2-232">使用與輸入資料集相同的資料行數目建立 Azure 搜尋服務索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="298d2-233">每小時都會將新項目加入至 Azure 搜尋服務索引。</span><span class="sxs-lookup"><span data-stu-id="298d2-233">New entries are added to the Azure Search index every hour.</span></span>

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

<span data-ttu-id="298d2-234">**具有 SQL 來源和「Azure 搜尋索引」接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="298d2-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="298d2-235">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="298d2-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="298d2-236">在管線 JSON 定義中，將 **source** 類型設為 **SqlSource**，並且將 **sink** 類型設為 **AzureSearchIndexSink**。</span><span class="sxs-lookup"><span data-stu-id="298d2-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="298d2-237">針對 **SqlReaderQuery** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="298d2-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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

<span data-ttu-id="298d2-238">如果您從雲端資料存放區將資料複製到 Azure 搜尋服務，則 `executionLocation` 是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="298d2-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="298d2-239">下列 JSON 程式碼片段顯示必須在「複製活動」的 `typeProperties` 下進行的變更。</span><span class="sxs-lookup"><span data-stu-id="298d2-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="298d2-240">參閱[在雲端資料存放區之間複製資料](data-factory-data-movement-activities.md#global)一節以取得支援的值和更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="298d2-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="298d2-241">從雲端來源複製</span><span class="sxs-lookup"><span data-stu-id="298d2-241">Copy from a cloud source</span></span>
<span data-ttu-id="298d2-242">如果您從雲端資料存放區將資料複製到 Azure 搜尋服務，則 `executionLocation` 是必要屬性。</span><span class="sxs-lookup"><span data-stu-id="298d2-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="298d2-243">下列 JSON 程式碼片段顯示必須在「複製活動」的 `typeProperties` 下進行的變更。</span><span class="sxs-lookup"><span data-stu-id="298d2-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="298d2-244">參閱[在雲端資料存放區之間複製資料](data-factory-data-movement-activities.md#global)一節以取得支援的值和更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="298d2-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="298d2-245">您也可以在複製活動定義中，將來自來源資料集的資料行與來自接收資料集的資料行對應。</span><span class="sxs-lookup"><span data-stu-id="298d2-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="298d2-246">如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="298d2-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="298d2-247">效能和微調</span><span class="sxs-lookup"><span data-stu-id="298d2-247">Performance and tuning</span></span>  
<span data-ttu-id="298d2-248">若要了解影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="298d2-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="298d2-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="298d2-249">Next steps</span></span>
<span data-ttu-id="298d2-250">請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="298d2-250">See the following articles:</span></span>

* <span data-ttu-id="298d2-251">[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得使用「複製活動」來建立管線的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="298d2-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
