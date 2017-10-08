---
title: "aaaMove 資料從 Azure 資料表的 / |Microsoft 文件"
description: "深入了解如何從 Azure 資料表儲存體，使用 Azure Data Factory 的/toomove 資料。"
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
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="97660-103">移動資料 tooand 使用 Azure Data Factory 的 Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="97660-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="97660-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從 Azure 資料表儲存體中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="97660-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="97660-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="97660-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="97660-106">您可以從任何支援的來源資料儲存 tooAzure 資料表儲存體，或從 Azure 資料表儲存體支援 tooany 接收資料存放區來複製資料。</span><span class="sxs-lookup"><span data-stu-id="97660-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="97660-107">如需支援做為來源或接收器 hello 複製活動的資料存放區的清單，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="97660-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="97660-108">開始使用</span><span class="sxs-lookup"><span data-stu-id="97660-108">Getting started</span></span>
<span data-ttu-id="97660-109">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出「Azure 資料表儲存體」。</span><span class="sxs-lookup"><span data-stu-id="97660-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="97660-110">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="97660-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="97660-111">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="97660-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="97660-112">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="97660-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="97660-113">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="97660-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="97660-114">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="97660-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="97660-115">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="97660-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="97660-116">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="97660-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="97660-117">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="97660-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="97660-118">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="97660-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="97660-119">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="97660-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="97660-120">如需使用的 toocopy 資料至 azure 或從 Azure 資料表儲存體的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples)本文一節。</span><span class="sxs-lookup"><span data-stu-id="97660-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="97660-121">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure 資料表儲存體的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="97660-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="97660-122">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="97660-122">Linked service properties</span></span>
<span data-ttu-id="97660-123">有兩種類型的連結服務中，您可以使用 toolink Azure blob 儲存體 tooan Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="97660-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="97660-124">它們是：**AzureStorage** 連結服務和 **AzureStorageSas** 連結服務。</span><span class="sxs-lookup"><span data-stu-id="97660-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="97660-125">hello Azure 儲存體連結服務提供 hello 與全域存取 toohello Azure 儲存體的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="97660-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="97660-126">而 hello Azure 儲存體 SAS （共用存取簽章） 連結的限制/時間繫結存取 toohello Azure 儲存體的 hello data factory 提供服務。</span><span class="sxs-lookup"><span data-stu-id="97660-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="97660-127">這兩個連結服務之間沒有其他差異。</span><span class="sxs-lookup"><span data-stu-id="97660-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="97660-128">選擇符合您需求的 hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="97660-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="97660-129">hello 下列各節提供更多詳細資料這兩個連結的服務。</span><span class="sxs-lookup"><span data-stu-id="97660-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="97660-130">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="97660-130">Dataset properties</span></span>
<span data-ttu-id="97660-131">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="97660-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="97660-132">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="97660-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="97660-133">hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="97660-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="97660-134">hello **typeProperties** hello 資料集的類型 > 一節**AzureTable**具有下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="97660-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="97660-135">屬性</span><span class="sxs-lookup"><span data-stu-id="97660-135">Property</span></span> | <span data-ttu-id="97660-136">說明</span><span class="sxs-lookup"><span data-stu-id="97660-136">Description</span></span> | <span data-ttu-id="97660-137">必要</span><span class="sxs-lookup"><span data-stu-id="97660-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97660-138">tableName</span><span class="sxs-lookup"><span data-stu-id="97660-138">tableName</span></span> |<span data-ttu-id="97660-139">參照的連結服務的 hello Azure 資料表的資料庫執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="97660-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="97660-140">是。</span><span class="sxs-lookup"><span data-stu-id="97660-140">Yes.</span></span> <span data-ttu-id="97660-141">當 tableName azureTableSourceQuery 沒有指定時，hello 資料表內的所有記錄都會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="97660-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="97660-142">如果同時指定 azureTableSourceQuery，滿足 hello 查詢的 hello 資料表內的記錄將會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="97660-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="97660-143">Data factory 的結構描述</span><span class="sxs-lookup"><span data-stu-id="97660-143">Schema by Data Factory</span></span>
<span data-ttu-id="97660-144">若是無結構描述的資料存放區，例如 Azure 資料表，hello Data Factory 服務會推斷 hello 結構描述，其中一種 hello 下列方式：</span><span class="sxs-lookup"><span data-stu-id="97660-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="97660-145">如果您指定資料的 hello 結構使用 hello**結構**hello 資料集定義，hello Data Factory 服務中的屬性會接受此結構做為 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="97660-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="97660-146">在此情況下，如果資料列的資料行沒有值，系統就會為它提供 null 值。</span><span class="sxs-lookup"><span data-stu-id="97660-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="97660-147">如果您未指定資料的 hello 結構使用 hello**結構**hello 資料集定義，Data Factory 中的屬性會推斷 hello 結構描述使用 hello 資料中的 hello 第一個資料列。</span><span class="sxs-lookup"><span data-stu-id="97660-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="97660-148">在此情況下，如果 hello 第一個資料列不包含 hello 完整結構描述，某些資料行缺少 hello 的複製作業的結果中。</span><span class="sxs-lookup"><span data-stu-id="97660-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="97660-149">因此，對於無結構描述的資料來源，hello 最佳作法是使用 hello 資料 toospecify hello 結構**結構**屬性。</span><span class="sxs-lookup"><span data-stu-id="97660-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="97660-150">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="97660-150">Copy activity properties</span></span>
<span data-ttu-id="97660-151">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="97660-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="97660-152">屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="97660-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="97660-153">屬性中的 hello hello 活動 hello typeProperties 區段可用另一方面會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="97660-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="97660-154">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="97660-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="97660-155">**AzureTableSource**支援下列屬性 typeProperties > 一節中的 hello:</span><span class="sxs-lookup"><span data-stu-id="97660-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="97660-156">屬性</span><span class="sxs-lookup"><span data-stu-id="97660-156">Property</span></span> | <span data-ttu-id="97660-157">說明</span><span class="sxs-lookup"><span data-stu-id="97660-157">Description</span></span> | <span data-ttu-id="97660-158">允許的值</span><span class="sxs-lookup"><span data-stu-id="97660-158">Allowed values</span></span> | <span data-ttu-id="97660-159">必要</span><span class="sxs-lookup"><span data-stu-id="97660-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="97660-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="97660-160">azureTableSourceQuery</span></span> |<span data-ttu-id="97660-161">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="97660-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="97660-162">Azure 資料表查詢字串。</span><span class="sxs-lookup"><span data-stu-id="97660-162">Azure table query string.</span></span> <span data-ttu-id="97660-163">請參閱 hello 下一節中的範例。</span><span class="sxs-lookup"><span data-stu-id="97660-163">See examples in hello next section.</span></span> |<span data-ttu-id="97660-164">否。</span><span class="sxs-lookup"><span data-stu-id="97660-164">No.</span></span> <span data-ttu-id="97660-165">當 tableName azureTableSourceQuery 沒有指定時，hello 資料表內的所有記錄都會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="97660-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="97660-166">如果同時指定 azureTableSourceQuery，滿足 hello 查詢的 hello 資料表內的記錄將會複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="97660-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="97660-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="97660-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="97660-168">指出是否壓抑 hello 的資料表不存在例外狀況。</span><span class="sxs-lookup"><span data-stu-id="97660-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="97660-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="97660-169">TRUE</span></span><br/><span data-ttu-id="97660-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="97660-170">FALSE</span></span> |<span data-ttu-id="97660-171">否</span><span class="sxs-lookup"><span data-stu-id="97660-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="97660-172">azureTableSourceQuery 範例</span><span class="sxs-lookup"><span data-stu-id="97660-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="97660-173">如果 Azure 資料表資料行是字串類型：</span><span class="sxs-lookup"><span data-stu-id="97660-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="97660-174">如果 Azure 資料表資料行是日期時間類型：</span><span class="sxs-lookup"><span data-stu-id="97660-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="97660-175">**AzureTableSink**支援下列屬性 typeProperties > 一節中的 hello:</span><span class="sxs-lookup"><span data-stu-id="97660-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="97660-176">屬性</span><span class="sxs-lookup"><span data-stu-id="97660-176">Property</span></span> | <span data-ttu-id="97660-177">說明</span><span class="sxs-lookup"><span data-stu-id="97660-177">Description</span></span> | <span data-ttu-id="97660-178">允許的值</span><span class="sxs-lookup"><span data-stu-id="97660-178">Allowed values</span></span> | <span data-ttu-id="97660-179">必要</span><span class="sxs-lookup"><span data-stu-id="97660-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="97660-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="97660-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="97660-181">預設資料分割索引鍵值，可供 hello 接收。</span><span class="sxs-lookup"><span data-stu-id="97660-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="97660-182">字串值。</span><span class="sxs-lookup"><span data-stu-id="97660-182">A string value.</span></span> |<span data-ttu-id="97660-183">否</span><span class="sxs-lookup"><span data-stu-id="97660-183">No</span></span> |
| <span data-ttu-id="97660-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="97660-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="97660-185">指定的值用做為資料分割索引鍵的 hello 資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="97660-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="97660-186">如果未指定，azuretabledefaultpartitionkeyvalue 會做為 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="97660-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="97660-187">資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="97660-187">A column name.</span></span> |<span data-ttu-id="97660-188">否</span><span class="sxs-lookup"><span data-stu-id="97660-188">No</span></span> |
| <span data-ttu-id="97660-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="97660-189">azureTableRowKeyName</span></span> |<span data-ttu-id="97660-190">指定的資料行值用做為資料列索引鍵的 hello 資料行的名稱。</span><span class="sxs-lookup"><span data-stu-id="97660-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="97660-191">如果未指定，則會針對每個資料列使用 GUID。</span><span class="sxs-lookup"><span data-stu-id="97660-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="97660-192">資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="97660-192">A column name.</span></span> |<span data-ttu-id="97660-193">否</span><span class="sxs-lookup"><span data-stu-id="97660-193">No</span></span> |
| <span data-ttu-id="97660-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="97660-194">azureTableInsertType</span></span> |<span data-ttu-id="97660-195">hello 模式 tooinsert 資料插入 Azure 資料表。</span><span class="sxs-lookup"><span data-stu-id="97660-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="97660-196">這個屬性控制與相符的資料分割和資料列的索引鍵的 hello 輸出資料表中的現有資料列是否具有取代或合併其值。</span><span class="sxs-lookup"><span data-stu-id="97660-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="97660-197">toolearn 有關這些設定 （「 合併 」 和 「 取代 」） 的運作方式，請參閱[插入或合併實體](https://msdn.microsoft.com/library/azure/hh452241.aspx)和[插入或取代實體](https://msdn.microsoft.com/library/azure/hh452242.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="97660-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="97660-198">此設定適用於在 hello 資料列層級，不 hello 資料表層級，和這兩個選項會刪除 hello 輸出資料表不存在於 hello 輸入的資料列。</span><span class="sxs-lookup"><span data-stu-id="97660-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="97660-199">合併 (預設值)</span><span class="sxs-lookup"><span data-stu-id="97660-199">merge (default)</span></span><br/><span data-ttu-id="97660-200">取代</span><span class="sxs-lookup"><span data-stu-id="97660-200">replace</span></span> |<span data-ttu-id="97660-201">否</span><span class="sxs-lookup"><span data-stu-id="97660-201">No</span></span> |
| <span data-ttu-id="97660-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="97660-202">writeBatchSize</span></span> |<span data-ttu-id="97660-203">Hello 叫用 writeBatchSize 或 writeBatchTimeout 時，請將資料插入至 hello Azure 資料表中。</span><span class="sxs-lookup"><span data-stu-id="97660-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="97660-204">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="97660-204">Integer (number of rows)</span></span> |<span data-ttu-id="97660-205">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="97660-205">No (default: 10000)</span></span> |
| <span data-ttu-id="97660-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="97660-206">writeBatchTimeout</span></span> |<span data-ttu-id="97660-207">用戶端 hello 叫用 writeBatchSize 或 writeBatchTimeout 時，將資料插入 hello Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="97660-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="97660-208">時間範圍</span><span class="sxs-lookup"><span data-stu-id="97660-208">timespan</span></span><br/><br/><span data-ttu-id="97660-209">範例：“00:20:00” (20 分鐘)</span><span class="sxs-lookup"><span data-stu-id="97660-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="97660-210">否 （預設 toostorage 用戶端預設逾時值 90 秒）</span><span class="sxs-lookup"><span data-stu-id="97660-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="97660-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="97660-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="97660-212">對應的來源資料行 tooa 目的地資料行之前您可以使用 hello 目的地資料行，如 hello azureTablePartitionKeyName 使用 hello 轉譯程式的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="97660-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="97660-213">下列範例的 hello，來源資料行 DivisionID 就是對應的 toohello 目的地資料行： DivisionID。</span><span class="sxs-lookup"><span data-stu-id="97660-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="97660-214">hello DivisionID 已指定為 hello 資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="97660-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="97660-215">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="97660-215">JSON examples</span></span>
<span data-ttu-id="97660-216">hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="97660-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="97660-217">它們會顯示如何從 Azure 資料表儲存體和 Azure Blob Database toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="97660-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="97660-218">不過，資料可以複製**直接**從任何支援的 hello 接收的 hello 來源 tooany。</span><span class="sxs-lookup"><span data-stu-id="97660-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="97660-219">如需詳細資訊，請參閱"支援資料存放區和格式 」 「 hello 」 一節中[使用複製活動移動資料](data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="97660-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="97660-220">範例： 將資料從 Azure 資料表 tooAzure Blob 複製</span><span class="sxs-lookup"><span data-stu-id="97660-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="97660-221">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="97660-221">hello following sample shows:</span></span>

1. <span data-ttu-id="97660-222">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務 (同時用於資料表和 Blob)。</span><span class="sxs-lookup"><span data-stu-id="97660-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="97660-223">[AzureTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="97660-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="97660-224">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="97660-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="97660-225">hello[管線](data-factory-create-pipelines.md)與使用複製活動[AzureTableSource](#activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="97660-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="97660-226">hello 範例會將屬於 toohello Azure 資料表 tooa blob 中的預設資料分割的每個小時的資料。</span><span class="sxs-lookup"><span data-stu-id="97660-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="97660-227">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="97660-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="97660-228">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="97660-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="97660-229">Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="97660-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="97660-230">如 hello 第一個、 指定 hello 連接字串，包含 hello 帳戶金鑰和 hello 更新版本，您可以指定 hello 共用存取簽章 (SAS) Uri。</span><span class="sxs-lookup"><span data-stu-id="97660-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="97660-231">請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="97660-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="97660-232">**Azure 資料表輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="97660-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="97660-233">hello 範例假設您有 Azure 資料表中建立資料表"MyTable"。</span><span class="sxs-lookup"><span data-stu-id="97660-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="97660-234">設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="97660-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="97660-235">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="97660-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="97660-236">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="97660-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="97660-237">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="97660-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="97660-238">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="97660-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="97660-239">**具有 AzureTableSource 和 BlobSink 的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="97660-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="97660-240">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="97660-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="97660-241">在 hello 管線 JSON 定義中，hello**來源**類型設定得**AzureTableSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="97660-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="97660-242">使用指定的 hello SQL 查詢**AzureTableSourceQuery**屬性選取 hello 資料 hello 預設分割區從每個小時 toocopy。</span><span class="sxs-lookup"><span data-stu-id="97660-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="97660-243">範例： 從 Azure Blob tooAzure 資料表複製資料</span><span class="sxs-lookup"><span data-stu-id="97660-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="97660-244">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="97660-244">hello following sample shows:</span></span>

1. <span data-ttu-id="97660-245">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務 (同時用於資料表和 Blob)</span><span class="sxs-lookup"><span data-stu-id="97660-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="97660-246">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="97660-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="97660-247">[AzureTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="97660-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="97660-248">hello[管線](data-factory-create-pipelines.md)與使用複製活動[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)和[AzureTableSink](#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="97660-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="97660-249">hello 範例從 Azure blob tooan Azure 資料表複製時間序列資料的每小時。</span><span class="sxs-lookup"><span data-stu-id="97660-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="97660-250">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="97660-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="97660-251">**Azure 儲存體 (同時適用於 Azure 資料表和 Blob) 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="97660-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="97660-252">Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="97660-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="97660-253">如 hello 第一個、 指定 hello 連接字串，包含 hello 帳戶金鑰和 hello 更新版本，您可以指定 hello 共用存取簽章 (SAS) Uri。</span><span class="sxs-lookup"><span data-stu-id="97660-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="97660-254">請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="97660-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="97660-255">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="97660-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="97660-256">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="97660-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="97660-257">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="97660-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="97660-258">年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="97660-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="97660-259">"external":"true"的設定會在該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="97660-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="97660-260">**Azure 資料表輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="97660-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="97660-261">hello 範例會將名為"MyTable"Azure 資料表中的資料 tooa 資料表複製。</span><span class="sxs-lookup"><span data-stu-id="97660-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="97660-262">建立 Azure 資料表具有如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="97660-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="97660-263">新的資料列會加入 toohello 資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="97660-263">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="97660-264">**具有 BlobSource 和 AzureTableSink 的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="97660-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="97660-265">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="97660-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="97660-266">在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**AzureTableSink**。</span><span class="sxs-lookup"><span data-stu-id="97660-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="97660-267">Azure 資料表的類型對應</span><span class="sxs-lookup"><span data-stu-id="97660-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="97660-268">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello。</span><span class="sxs-lookup"><span data-stu-id="97660-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="97660-269">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="97660-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="97660-270">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="97660-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="97660-271">移動資料時太 & 從 Azure 資料表，hello 遵循[Azure 表格服務所定義的對應](https://msdn.microsoft.com/library/azure/dd179338.aspx)可用從 Azure 資料表 OData 類型 too.NET 型別，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="97660-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="97660-272">OData 資料類型</span><span class="sxs-lookup"><span data-stu-id="97660-272">OData Data Type</span></span> | <span data-ttu-id="97660-273">.NET 類型</span><span class="sxs-lookup"><span data-stu-id="97660-273">.NET Type</span></span> | <span data-ttu-id="97660-274">詳細資料</span><span class="sxs-lookup"><span data-stu-id="97660-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97660-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="97660-275">Edm.Binary</span></span> |<span data-ttu-id="97660-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="97660-276">byte[]</span></span> |<span data-ttu-id="97660-277">向上 too64 KB 的位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="97660-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="97660-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="97660-278">Edm.Boolean</span></span> |<span data-ttu-id="97660-279">布林</span><span class="sxs-lookup"><span data-stu-id="97660-279">bool</span></span> |<span data-ttu-id="97660-280">布林值。</span><span class="sxs-lookup"><span data-stu-id="97660-280">A Boolean value.</span></span> |
| <span data-ttu-id="97660-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="97660-281">Edm.DateTime</span></span> |<span data-ttu-id="97660-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="97660-282">DateTime</span></span> |<span data-ttu-id="97660-283">以國際標準時間 (UTC) 表示的 64 位元值。</span><span class="sxs-lookup"><span data-stu-id="97660-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="97660-284">hello 支援日期時間範圍是從午夜 12:00，1601年西元 1</span><span class="sxs-lookup"><span data-stu-id="97660-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="97660-285">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="97660-285">(C.E.), UTC.</span></span> <span data-ttu-id="97660-286">hello 範圍會在年 12 月 31 日結束 9999。</span><span class="sxs-lookup"><span data-stu-id="97660-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="97660-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="97660-287">Edm.Double</span></span> |<span data-ttu-id="97660-288">double</span><span class="sxs-lookup"><span data-stu-id="97660-288">double</span></span> |<span data-ttu-id="97660-289">64 位元的浮點值。</span><span class="sxs-lookup"><span data-stu-id="97660-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="97660-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="97660-290">Edm.Guid</span></span> |<span data-ttu-id="97660-291">Guid</span><span class="sxs-lookup"><span data-stu-id="97660-291">Guid</span></span> |<span data-ttu-id="97660-292">128 位元的全域唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="97660-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="97660-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="97660-293">Edm.Int32</span></span> |<span data-ttu-id="97660-294">Int32</span><span class="sxs-lookup"><span data-stu-id="97660-294">Int32</span></span> |<span data-ttu-id="97660-295">32 位元的整數。</span><span class="sxs-lookup"><span data-stu-id="97660-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="97660-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="97660-296">Edm.Int64</span></span> |<span data-ttu-id="97660-297">Int64</span><span class="sxs-lookup"><span data-stu-id="97660-297">Int64</span></span> |<span data-ttu-id="97660-298">64 位元的整數。</span><span class="sxs-lookup"><span data-stu-id="97660-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="97660-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="97660-299">Edm.String</span></span> |<span data-ttu-id="97660-300">String</span><span class="sxs-lookup"><span data-stu-id="97660-300">String</span></span> |<span data-ttu-id="97660-301">UTF 16 編碼值。</span><span class="sxs-lookup"><span data-stu-id="97660-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="97660-302">字串值可能是 up too64 KB。</span><span class="sxs-lookup"><span data-stu-id="97660-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="97660-303">類型轉換範例</span><span class="sxs-lookup"><span data-stu-id="97660-303">Type Conversion Sample</span></span>
<span data-ttu-id="97660-304">下列範例中的 hello 適用於資料複製到 Azure Blob tooAzure 資料表使用類型轉換。</span><span class="sxs-lookup"><span data-stu-id="97660-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="97660-305">假設 hello Blob 資料集的 CSV 格式，而且包含三個資料行。</span><span class="sxs-lookup"><span data-stu-id="97660-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="97660-306">其中一個方法是使用 hello 星期幾的縮寫法文名稱的自訂日期時間格式的 datetime 資料行。</span><span class="sxs-lookup"><span data-stu-id="97660-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="97660-307">定義 hello Blob 來源的資料集以及 hello 資料行的類型定義，如下所示。</span><span class="sxs-lookup"><span data-stu-id="97660-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

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
<span data-ttu-id="97660-308">從 Azure 資料表 OData 類型 too.NET 類型指定 hello 類型對應，您會定義 hello 資料表 Azure 資料表中以 hello 遵循結構描述。</span><span class="sxs-lookup"><span data-stu-id="97660-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="97660-309">**Azure 資料表結構描述：**</span><span class="sxs-lookup"><span data-stu-id="97660-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="97660-310">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="97660-310">Column name</span></span> | <span data-ttu-id="97660-311">類型</span><span class="sxs-lookup"><span data-stu-id="97660-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="97660-312">userid</span><span class="sxs-lookup"><span data-stu-id="97660-312">userid</span></span> |<span data-ttu-id="97660-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="97660-313">Edm.Int64</span></span> |
| <span data-ttu-id="97660-314">名稱</span><span class="sxs-lookup"><span data-stu-id="97660-314">name</span></span> |<span data-ttu-id="97660-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="97660-315">Edm.String</span></span> |
| <span data-ttu-id="97660-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="97660-316">lastlogindate</span></span> |<span data-ttu-id="97660-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="97660-317">Edm.DateTime</span></span> |

<span data-ttu-id="97660-318">接下來，定義 hello Azure 資料表的資料集，如下所示。</span><span class="sxs-lookup"><span data-stu-id="97660-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="97660-319">由於 hello 基礎資料存放區中已經指定 hello 型別資訊，因此不需要 toospecify hello 類型資訊的 「 結構 」 一節。</span><span class="sxs-lookup"><span data-stu-id="97660-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

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

<span data-ttu-id="97660-320">在此情況下，Data Factory 自動類型轉換包括 hello Datetime 欄位與 hello 自訂 datetime 格式移動資料，從 Blob tooAzure 資料表時，使用 hello 「 fr-fr 」 文化特性。</span><span class="sxs-lookup"><span data-stu-id="97660-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="97660-321">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="97660-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="97660-322">效能和微調</span><span class="sxs-lookup"><span data-stu-id="97660-322">Performance and Tuning</span></span>
<span data-ttu-id="97660-323">關於金鑰 toolearn 因素影響效能的 Azure Data Factory 和各種方式 toooptimize 中的資料移動 （複製活動），請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="97660-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
