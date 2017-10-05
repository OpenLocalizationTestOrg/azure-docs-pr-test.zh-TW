---
title: "從 Azure 資料表來回移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Azure 表格儲存體來回移動資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="b3d4d-103">使用 Azure Data Factory 從 Azure 資料表來回移動資料</span><span class="sxs-lookup"><span data-stu-id="b3d4d-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="b3d4d-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，將資料移進/移出「Azure 資料表儲存體」。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="b3d4d-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="b3d4d-106">您可以將資料從任何支援的來源資料存放區複製到「Azure 資料表儲存體」，或從「Azure 資料表儲存體」複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="b3d4d-107">如需複製活動所支援作為來源或接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="b3d4d-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="b3d4d-108">Getting started</span></span>
<span data-ttu-id="b3d4d-109">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出「Azure 資料表儲存體」。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="b3d4d-110">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="b3d4d-111">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="b3d4d-112">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b3d4d-113">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b3d4d-114">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="b3d4d-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="b3d4d-115">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="b3d4d-116">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="b3d4d-117">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b3d4d-118">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b3d4d-119">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b3d4d-120">如需相關範例，其中含有用來將資料複製到「Azure 資料表儲存體」(或從「Azure 資料表儲存體」複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples)一節。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="b3d4d-121">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義「Azure 資料表儲存體」特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="b3d4d-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="b3d4d-122">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="b3d4d-122">Linked service properties</span></span>
<span data-ttu-id="b3d4d-123">您可以使用兩種類型的連結服務，將 Azure Blob 儲存體連結至 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="b3d4d-124">它們是：**AzureStorage** 連結服務和 **AzureStorageSas** 連結服務。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="b3d4d-125">Azure 儲存體連結服務可將 Azure 儲存體的全域存取權提供給 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="b3d4d-126">而 Azure 儲存體 SAS (共用存取簽章) 連結服務會將 Azure 儲存體的受限制/時間繫結存取權提供給 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="b3d4d-127">這兩個連結服務之間沒有其他差異。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="b3d4d-128">選擇符合您需求的連結服務。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="b3d4d-129">以下章節提供這兩個連結服務的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="b3d4d-130">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="b3d4d-130">Dataset properties</span></span>
<span data-ttu-id="b3d4d-131">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b3d4d-132">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b3d4d-133">每個資料集類型的 typeProperties 區段都不同，可提供資料存放區中資料的位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="b3d4d-134">**AzureTable** 類型資料集的 **typeProperties** 區段有下列屬性。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="b3d4d-135">屬性</span><span class="sxs-lookup"><span data-stu-id="b3d4d-135">Property</span></span> | <span data-ttu-id="b3d4d-136">說明</span><span class="sxs-lookup"><span data-stu-id="b3d4d-136">Description</span></span> | <span data-ttu-id="b3d4d-137">必要</span><span class="sxs-lookup"><span data-stu-id="b3d4d-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3d4d-138">tableName</span><span class="sxs-lookup"><span data-stu-id="b3d4d-138">tableName</span></span> |<span data-ttu-id="b3d4d-139">Azure 資料表資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="b3d4d-140">是。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-140">Yes.</span></span> <span data-ttu-id="b3d4d-141">指定 tableName 時若沒有指定 azureTableSourceQuery，資料表中的所有記錄都會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="b3d4d-142">如果同時指定了 azureTableSourceQuery，則資料表中符合查詢的記錄會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="b3d4d-143">Data factory 的結構描述</span><span class="sxs-lookup"><span data-stu-id="b3d4d-143">Schema by Data Factory</span></span>
<span data-ttu-id="b3d4d-144">針對無結構描述的資料存放區 (如 Azure 資料表)，Data Factory 服務會以下列一種方式推斷結構描述：</span><span class="sxs-lookup"><span data-stu-id="b3d4d-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="b3d4d-145">如果您是使用資料集定義中的 **structure** 屬性來定義結構，Data Factory 服務會將此結構接受為結構描述。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="b3d4d-146">在此情況下，如果資料列的資料行沒有值，系統就會為它提供 null 值。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="b3d4d-147">如果您沒有使用資料集定義中的 **structure** 屬性來指定結構，Data Factory 服務將會使用資料的第一列來推斷結構描述。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="b3d4d-148">在此情況下，如果第一個資料列未包含完整的結構描述，複製作業的結果中就會遺失一些資料行。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="b3d4d-149">因此，對於無結構描述的資料來源來說，最佳作法是使用 **structure** 屬性來指定資料結構。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="b3d4d-150">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="b3d4d-150">Copy activity properties</span></span>
<span data-ttu-id="b3d4d-151">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b3d4d-152">屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="b3d4d-153">另一方面，活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="b3d4d-154">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="b3d4d-155">**AzureTableSource** 在 typeProperties 區段中支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b3d4d-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="b3d4d-156">屬性</span><span class="sxs-lookup"><span data-stu-id="b3d4d-156">Property</span></span> | <span data-ttu-id="b3d4d-157">說明</span><span class="sxs-lookup"><span data-stu-id="b3d4d-157">Description</span></span> | <span data-ttu-id="b3d4d-158">允許的值</span><span class="sxs-lookup"><span data-stu-id="b3d4d-158">Allowed values</span></span> | <span data-ttu-id="b3d4d-159">必要</span><span class="sxs-lookup"><span data-stu-id="b3d4d-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b3d4d-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="b3d4d-160">azureTableSourceQuery</span></span> |<span data-ttu-id="b3d4d-161">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-161">Use the custom query to read data.</span></span> |<span data-ttu-id="b3d4d-162">Azure 資料表查詢字串。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-162">Azure table query string.</span></span> <span data-ttu-id="b3d4d-163">請參閱下一節中的範例。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-163">See examples in the next section.</span></span> |<span data-ttu-id="b3d4d-164">否。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-164">No.</span></span> <span data-ttu-id="b3d4d-165">指定 tableName 時若沒有指定 azureTableSourceQuery，資料表中的所有記錄都會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="b3d4d-166">如果同時指定了 azureTableSourceQuery，則資料表中符合查詢的記錄會複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="b3d4d-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="b3d4d-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="b3d4d-168">指出是否忍受資料表不存在的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="b3d4d-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="b3d4d-169">TRUE</span></span><br/><span data-ttu-id="b3d4d-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="b3d4d-170">FALSE</span></span> |<span data-ttu-id="b3d4d-171">否</span><span class="sxs-lookup"><span data-stu-id="b3d4d-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="b3d4d-172">azureTableSourceQuery 範例</span><span class="sxs-lookup"><span data-stu-id="b3d4d-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="b3d4d-173">如果 Azure 資料表資料行是字串類型：</span><span class="sxs-lookup"><span data-stu-id="b3d4d-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="b3d4d-174">如果 Azure 資料表資料行是日期時間類型：</span><span class="sxs-lookup"><span data-stu-id="b3d4d-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="b3d4d-175">**AzureTableSink** 在 typeProperties 區段中支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b3d4d-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="b3d4d-176">屬性</span><span class="sxs-lookup"><span data-stu-id="b3d4d-176">Property</span></span> | <span data-ttu-id="b3d4d-177">說明</span><span class="sxs-lookup"><span data-stu-id="b3d4d-177">Description</span></span> | <span data-ttu-id="b3d4d-178">允許的值</span><span class="sxs-lookup"><span data-stu-id="b3d4d-178">Allowed values</span></span> | <span data-ttu-id="b3d4d-179">必要</span><span class="sxs-lookup"><span data-stu-id="b3d4d-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b3d4d-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="b3d4d-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="b3d4d-181">可供接收器使用的預設資料分割索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="b3d4d-182">字串值。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-182">A string value.</span></span> |<span data-ttu-id="b3d4d-183">否</span><span class="sxs-lookup"><span data-stu-id="b3d4d-183">No</span></span> |
| <span data-ttu-id="b3d4d-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="b3d4d-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="b3d4d-185">指定其值用來作為分割區索引鍵的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="b3d4d-186">如果未指定，則會使用 AzureTableDefaultPartitionKeyValue 做為資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="b3d4d-187">資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-187">A column name.</span></span> |<span data-ttu-id="b3d4d-188">否</span><span class="sxs-lookup"><span data-stu-id="b3d4d-188">No</span></span> |
| <span data-ttu-id="b3d4d-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="b3d4d-189">azureTableRowKeyName</span></span> |<span data-ttu-id="b3d4d-190">指定其值用來作為資料列索引鍵的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="b3d4d-191">如果未指定，則會針對每個資料列使用 GUID。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="b3d4d-192">資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-192">A column name.</span></span> |<span data-ttu-id="b3d4d-193">否</span><span class="sxs-lookup"><span data-stu-id="b3d4d-193">No</span></span> |
| <span data-ttu-id="b3d4d-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="b3d4d-194">azureTableInsertType</span></span> |<span data-ttu-id="b3d4d-195">將資料插入 Azure 資料表的模式。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="b3d4d-196">此屬性可控制針對輸出資料表中具有相符分割區和資料列索引鍵的現有資料列，是要取代還是合併其值。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="b3d4d-197">若要了解這些設定 (合併和取代) 的運作方式，請參閱[插入或合併實體](https://msdn.microsoft.com/library/azure/hh452241.aspx)和[插入或取代實體](https://msdn.microsoft.com/library/azure/hh452242.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="b3d4d-198">此設定是在資料列層級套用，而不是在資料表層級套用，而且兩個選項都不會刪除存在於輸出資料表中但不存在於輸入中的資料列。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="b3d4d-199">合併 (預設值)</span><span class="sxs-lookup"><span data-stu-id="b3d4d-199">merge (default)</span></span><br/><span data-ttu-id="b3d4d-200">取代</span><span class="sxs-lookup"><span data-stu-id="b3d4d-200">replace</span></span> |<span data-ttu-id="b3d4d-201">否</span><span class="sxs-lookup"><span data-stu-id="b3d4d-201">No</span></span> |
| <span data-ttu-id="b3d4d-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="b3d4d-202">writeBatchSize</span></span> |<span data-ttu-id="b3d4d-203">在達到 WriteBatchSize 或 writeBatchTimeout 時將資料插入 Azure 資料表中。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="b3d4d-204">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="b3d4d-204">Integer (number of rows)</span></span> |<span data-ttu-id="b3d4d-205">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="b3d4d-205">No (default: 10000)</span></span> |
| <span data-ttu-id="b3d4d-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="b3d4d-206">writeBatchTimeout</span></span> |<span data-ttu-id="b3d4d-207">在達到 WriteBatchSize 或 writeBatchTimeout 時將資料插入 Azure 資料表中</span><span class="sxs-lookup"><span data-stu-id="b3d4d-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="b3d4d-208">時間範圍</span><span class="sxs-lookup"><span data-stu-id="b3d4d-208">timespan</span></span><br/><br/><span data-ttu-id="b3d4d-209">範例：“00:20:00” (20 分鐘)</span><span class="sxs-lookup"><span data-stu-id="b3d4d-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="b3d4d-210">否 (預設為儲存體用戶端預設逾時值 90 秒)</span><span class="sxs-lookup"><span data-stu-id="b3d4d-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="b3d4d-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="b3d4d-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="b3d4d-212">您必須先使用轉譯器 JSON 屬性將來源資料行對應至目的地資料行，才能使用目的地資料行作為 azureTablePartitionKeyName。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="b3d4d-213">在下列範例中，來源資料行 DivisionID 會對應至目的地資料行：DivisionID。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="b3d4d-214">DivisionID 被指定為分割區索引鍵。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="b3d4d-215">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="b3d4d-215">JSON examples</span></span>
<span data-ttu-id="b3d4d-216">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b3d4d-217">它們會示範如何將資料複製到 Azure 表格儲存體和 Azure Blob 儲存體，以及複製其中的資料。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="b3d4d-218">不過，您可以將資料從任何來源**直接**複製到任何支援的接收器。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="b3d4d-219">如需詳細資訊，請參閱[使用複製活動來移動資料](data-factory-data-movement-activities.md)中的＜支援的資料存放區和格式＞一節。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="b3d4d-220">範例：將資料從 Azure 資料表複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="b3d4d-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="b3d4d-221">下列範例顯示︰</span><span class="sxs-lookup"><span data-stu-id="b3d4d-221">The following sample shows:</span></span>

1. <span data-ttu-id="b3d4d-222">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務 (同時用於資料表和 Blob)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="b3d4d-223">[AzureTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="b3d4d-224">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="b3d4d-225">具有使用 [AzureTableSource](#activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b3d4d-226">此範例會每小時將 Azure 資料表中屬於預設資料分割的資料複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="b3d4d-227">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b3d4d-228">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-228">**Azure storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="b3d4d-229">Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="b3d4d-230">對於前者指定連接字串，包含帳戶金鑰，對於後者指定共用存取簽章 (SAS) Uri。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="b3d4d-231">請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="b3d4d-232">**Azure 資料表輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="b3d4d-233">此範例假設您已在 Azure 資料表中建立資料表 "MyTable"。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="b3d4d-234">設定 “external”: ”true” 會通知 Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="b3d4d-235">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="b3d4d-236">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b3d4d-237">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b3d4d-238">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="b3d4d-239">**具有 AzureTableSource 和 BlobSink 的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="b3d4d-240">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b3d4d-241">在管線 JSON 定義中，**source** 類型設定為 **AzureTableSource**，且 **sink** 類型設定為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b3d4d-242">使用 **AzureTableSourceQuery** 屬性指定的 SQL 查詢會每小時從預設分割中選取要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="b3d4d-243">範例：將資料從 Azure Blob 複製到 Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="b3d4d-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="b3d4d-244">下列範例顯示︰</span><span class="sxs-lookup"><span data-stu-id="b3d4d-244">The following sample shows:</span></span>

1. <span data-ttu-id="b3d4d-245">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務 (同時用於資料表和 Blob)</span><span class="sxs-lookup"><span data-stu-id="b3d4d-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="b3d4d-246">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="b3d4d-247">[AzureTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b3d4d-248">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [AzureTableSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="b3d4d-249">此範例會每小時將時間序列資料從 Azure Blob 複製到 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="b3d4d-250">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b3d4d-251">**Azure 儲存體 (同時適用於 Azure 資料表和 Blob) 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="b3d4d-252">Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="b3d4d-253">對於前者指定連接字串，包含帳戶金鑰，對於後者指定共用存取簽章 (SAS) Uri。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="b3d4d-254">請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="b3d4d-255">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="b3d4d-256">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b3d4d-257">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b3d4d-258">資料夾路徑會使用開始時間的年、月及日部分，而檔案名稱則使用開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="b3d4d-259">“external”: “true” 設定可讓 Data Factory 服務知道資料集是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
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

<span data-ttu-id="b3d4d-260">**Azure 資料表輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="b3d4d-261">此範例會將資料複製到 Azure 資料表中名為 "MyTable" 的資料表。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="b3d4d-262">請建立資料行數目與您預期 Blob CSV 檔案要包含的數目相同的 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="b3d4d-263">此資料表會每小時加入新的資料列。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-263">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="b3d4d-264">**具有 BlobSource 和 AzureTableSink 的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="b3d4d-265">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b3d4d-266">在管線 JSON 定義中，**source** 類型設定為 **BlobSource**，且 **sink** 類型設定為 **AzureTableSink**。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="b3d4d-267">Azure 資料表的類型對應</span><span class="sxs-lookup"><span data-stu-id="b3d4d-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="b3d4d-268">如 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會藉由下列含有兩個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="b3d4d-269">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="b3d4d-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="b3d4d-270">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="b3d4d-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="b3d4d-271">將資料移入及移出 Azure 資料表時，從 Azure 資料表 OData 類型到 .NET 類型的對應會使用下列 [Azure 資料表服務定義的對應](https://msdn.microsoft.com/library/azure/dd179338.aspx)，反向對應亦適用。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="b3d4d-272">OData 資料類型</span><span class="sxs-lookup"><span data-stu-id="b3d4d-272">OData Data Type</span></span> | <span data-ttu-id="b3d4d-273">.NET 類型</span><span class="sxs-lookup"><span data-stu-id="b3d4d-273">.NET Type</span></span> | <span data-ttu-id="b3d4d-274">詳細資料</span><span class="sxs-lookup"><span data-stu-id="b3d4d-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3d4d-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="b3d4d-275">Edm.Binary</span></span> |<span data-ttu-id="b3d4d-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="b3d4d-276">byte[]</span></span> |<span data-ttu-id="b3d4d-277">上限為 64 KB 的位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="b3d4d-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="b3d4d-278">Edm.Boolean</span></span> |<span data-ttu-id="b3d4d-279">布林</span><span class="sxs-lookup"><span data-stu-id="b3d4d-279">bool</span></span> |<span data-ttu-id="b3d4d-280">布林值。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-280">A Boolean value.</span></span> |
| <span data-ttu-id="b3d4d-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="b3d4d-281">Edm.DateTime</span></span> |<span data-ttu-id="b3d4d-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="b3d4d-282">DateTime</span></span> |<span data-ttu-id="b3d4d-283">以國際標準時間 (UTC) 表示的 64 位元值。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="b3d4d-284">支援的 DateTime 範圍從西元 1601 年 1 月 1 日午夜 12:00 開始</span><span class="sxs-lookup"><span data-stu-id="b3d4d-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="b3d4d-285">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="b3d4d-285">(C.E.), UTC.</span></span> <span data-ttu-id="b3d4d-286">此範圍結束於 9999 年 12 月 31 日。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="b3d4d-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="b3d4d-287">Edm.Double</span></span> |<span data-ttu-id="b3d4d-288">double</span><span class="sxs-lookup"><span data-stu-id="b3d4d-288">double</span></span> |<span data-ttu-id="b3d4d-289">64 位元的浮點值。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="b3d4d-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="b3d4d-290">Edm.Guid</span></span> |<span data-ttu-id="b3d4d-291">Guid</span><span class="sxs-lookup"><span data-stu-id="b3d4d-291">Guid</span></span> |<span data-ttu-id="b3d4d-292">128 位元的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="b3d4d-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="b3d4d-293">Edm.Int32</span></span> |<span data-ttu-id="b3d4d-294">Int32</span><span class="sxs-lookup"><span data-stu-id="b3d4d-294">Int32</span></span> |<span data-ttu-id="b3d4d-295">32 位元的整數。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="b3d4d-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="b3d4d-296">Edm.Int64</span></span> |<span data-ttu-id="b3d4d-297">Int64</span><span class="sxs-lookup"><span data-stu-id="b3d4d-297">Int64</span></span> |<span data-ttu-id="b3d4d-298">64 位元的整數。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="b3d4d-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="b3d4d-299">Edm.String</span></span> |<span data-ttu-id="b3d4d-300">String</span><span class="sxs-lookup"><span data-stu-id="b3d4d-300">String</span></span> |<span data-ttu-id="b3d4d-301">UTF 16 編碼值。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="b3d4d-302">字串值最大可達 64 KB。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="b3d4d-303">類型轉換範例</span><span class="sxs-lookup"><span data-stu-id="b3d4d-303">Type Conversion Sample</span></span>
<span data-ttu-id="b3d4d-304">下列範例適用於使用類型轉換從 Azure Blob 複製資料到 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="b3d4d-305">假設 Blob 資料集採用 CSV 格式而且包含三個資料行。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="b3d4d-306">其中一個是含有自訂日期時間格式 (使用法文縮寫星期幾名稱) 的日期時間資料行。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="b3d4d-307">請依下列方式，定義「Blob 來源」資料集及資料行的類型定義。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
<span data-ttu-id="b3d4d-308">如果使用從「Azure 資料表」OData 類型到 .NET 類型的類型對應，您就會在「Azure 資料表」中定義具有下列結構描述的資料表。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="b3d4d-309">**Azure 資料表結構描述：**</span><span class="sxs-lookup"><span data-stu-id="b3d4d-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="b3d4d-310">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="b3d4d-310">Column name</span></span> | <span data-ttu-id="b3d4d-311">類型</span><span class="sxs-lookup"><span data-stu-id="b3d4d-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="b3d4d-312">userid</span><span class="sxs-lookup"><span data-stu-id="b3d4d-312">userid</span></span> |<span data-ttu-id="b3d4d-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="b3d4d-313">Edm.Int64</span></span> |
| <span data-ttu-id="b3d4d-314">名稱</span><span class="sxs-lookup"><span data-stu-id="b3d4d-314">name</span></span> |<span data-ttu-id="b3d4d-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="b3d4d-315">Edm.String</span></span> |
| <span data-ttu-id="b3d4d-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="b3d4d-316">lastlogindate</span></span> |<span data-ttu-id="b3d4d-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="b3d4d-317">Edm.DateTime</span></span> |

<span data-ttu-id="b3d4d-318">接著，依下列方式定義「Azure 資料表」資料集。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="b3d4d-319">您不需要指定含有類型資訊的「結構」區段，因為類型資訊已在基礎資料存放區中指定。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="b3d4d-320">在此情況下，Data Factory 會自動進行類型轉換，包括將資料從 Blob 移到「Azure 資料表」時，含有自訂日期時間格式 (使用 "fr-fr" 文化特性) 的 Datetime 欄位。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="b3d4d-321">若要將來自來源資料集的資料行與來自接收資料集的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b3d4d-322">效能和微調</span><span class="sxs-lookup"><span data-stu-id="b3d4d-322">Performance and Tuning</span></span>
<span data-ttu-id="b3d4d-323">若要了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="b3d4d-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
