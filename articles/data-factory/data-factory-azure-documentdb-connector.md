---
title: "從 Azure Cosmos DB 來回移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Azure Cosmos DB 集合來回移動資料"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 7a11c6ade0325b08ad520448bbf82d64a0a555f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="c0594-103">使用 Azure Data Factory 從 Azure Cosmos DB 來回移動資料</span><span class="sxs-lookup"><span data-stu-id="c0594-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="c0594-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，將資料移進/移出 Azure Cosmos DB (DocumentDB API)。</span><span class="sxs-lookup"><span data-stu-id="c0594-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="c0594-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="c0594-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="c0594-106">您可以將資料從任何支援的來源資料存放區複製到 Azure Cosmos DB，或從 Azure Cosmos DB 複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="c0594-106">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="c0594-107">如需複製活動所支援作為來源或接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="c0594-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c0594-108">Azure Cosmos DB 連接器只支援 DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="c0594-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="c0594-109">若要將資料依原樣複製到 JSON 檔案或另一個 Cosmos DB 集合，或從這些檔案或集合依原樣複製資料，請參閱[匯入/匯出 JSON 文件](#importexport-json-documents)。</span><span class="sxs-lookup"><span data-stu-id="c0594-109">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c0594-110">開始使用</span><span class="sxs-lookup"><span data-stu-id="c0594-110">Getting started</span></span>
<span data-ttu-id="c0594-111">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="c0594-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="c0594-112">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="c0594-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c0594-113">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="c0594-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="c0594-114">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="c0594-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c0594-115">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="c0594-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c0594-116">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="c0594-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="c0594-117">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="c0594-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c0594-118">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="c0594-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c0594-119">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="c0594-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c0594-120">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="c0594-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c0594-121">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="c0594-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c0594-122">如需相關範例，其中含有用來將資料複製到 Cosmos DB (或從 Cosmos DB 複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples)一節。</span><span class="sxs-lookup"><span data-stu-id="c0594-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="c0594-123">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Cosmos DB 特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="c0594-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="c0594-124">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="c0594-124">Linked service properties</span></span>
<span data-ttu-id="c0594-125">下表提供 Azure Cosmos DB 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="c0594-125">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="c0594-126">**屬性**</span><span class="sxs-lookup"><span data-stu-id="c0594-126">**Property**</span></span> | <span data-ttu-id="c0594-127">**說明**</span><span class="sxs-lookup"><span data-stu-id="c0594-127">**Description**</span></span> | <span data-ttu-id="c0594-128">**必要**</span><span class="sxs-lookup"><span data-stu-id="c0594-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0594-129">類型</span><span class="sxs-lookup"><span data-stu-id="c0594-129">type</span></span> |<span data-ttu-id="c0594-130">類型屬性必須設為： **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="c0594-130">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="c0594-131">是</span><span class="sxs-lookup"><span data-stu-id="c0594-131">Yes</span></span> |
| <span data-ttu-id="c0594-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="c0594-132">connectionString</span></span> |<span data-ttu-id="c0594-133">指定連接到 Azure Cosmos DB 資料庫所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="c0594-133">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="c0594-134">是</span><span class="sxs-lookup"><span data-stu-id="c0594-134">Yes</span></span> |

<span data-ttu-id="c0594-135">範例：</span><span class="sxs-lookup"><span data-stu-id="c0594-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c0594-136">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="c0594-136">Dataset properties</span></span>
<span data-ttu-id="c0594-137">如需可用來定義資料集的完整區段和屬性清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="c0594-137">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c0594-138">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="c0594-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c0594-139">每個資料集類型的 typeProperties 區段都不同，可提供資料存放區中資料的位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c0594-139">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c0594-140">**DocumentDbCollection** 類型資料集的 typeProperties 區段具有下列屬性。</span><span class="sxs-lookup"><span data-stu-id="c0594-140">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="c0594-141">**屬性**</span><span class="sxs-lookup"><span data-stu-id="c0594-141">**Property**</span></span> | <span data-ttu-id="c0594-142">**說明**</span><span class="sxs-lookup"><span data-stu-id="c0594-142">**Description**</span></span> | <span data-ttu-id="c0594-143">**必要**</span><span class="sxs-lookup"><span data-stu-id="c0594-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0594-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="c0594-144">collectionName</span></span> |<span data-ttu-id="c0594-145">Cosmos DB 文件集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="c0594-145">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="c0594-146">是</span><span class="sxs-lookup"><span data-stu-id="c0594-146">Yes</span></span> |

<span data-ttu-id="c0594-147">範例：</span><span class="sxs-lookup"><span data-stu-id="c0594-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="c0594-148">Data factory 的結構描述</span><span class="sxs-lookup"><span data-stu-id="c0594-148">Schema by Data Factory</span></span>
<span data-ttu-id="c0594-149">針對無結構描述的資料存放區 (如 Azure Cosmos DB)，Data Factory 服務會以下列一種方式推斷結構描述：</span><span class="sxs-lookup"><span data-stu-id="c0594-149">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="c0594-150">如果您是使用資料集定義中的 **structure** 屬性來定義結構，Data Factory 服務會將此結構接受為結構描述。</span><span class="sxs-lookup"><span data-stu-id="c0594-150">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="c0594-151">在此情況下，如果資料列不包含資料行的值，則會使用 null 值。</span><span class="sxs-lookup"><span data-stu-id="c0594-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="c0594-152">如果您不是使用資料集定義中的 **structure** 屬性來指定結構，Data Factory 服務會使用資料的第一列來推斷結構描述。</span><span class="sxs-lookup"><span data-stu-id="c0594-152">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="c0594-153">在此情況下，如果第一個資料列不包含完整的結構描述，某些資料行會因複製作業而遺失。</span><span class="sxs-lookup"><span data-stu-id="c0594-153">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="c0594-154">因此，對於無結構描述的資料來源來說，最佳作法是使用 **structure** 屬性來指定資料結構。</span><span class="sxs-lookup"><span data-stu-id="c0594-154">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c0594-155">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="c0594-155">Copy activity properties</span></span>
<span data-ttu-id="c0594-156">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="c0594-156">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c0594-157">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="c0594-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="c0594-158">複製活動只會採用一個輸入，而且只產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="c0594-158">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="c0594-159">另一方面，活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同，而在複製活動的案例中，可用的屬性會根據來源與接收的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="c0594-159">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c0594-160">在複製活動的案例中，如果來源類型為 **DocumentDbCollectionSource**，則 **typeProperties** 區段可使用下列屬性：</span><span class="sxs-lookup"><span data-stu-id="c0594-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="c0594-161">**屬性**</span><span class="sxs-lookup"><span data-stu-id="c0594-161">**Property**</span></span> | <span data-ttu-id="c0594-162">**說明**</span><span class="sxs-lookup"><span data-stu-id="c0594-162">**Description**</span></span> | <span data-ttu-id="c0594-163">**允許的值**</span><span class="sxs-lookup"><span data-stu-id="c0594-163">**Allowed values**</span></span> | <span data-ttu-id="c0594-164">**必要**</span><span class="sxs-lookup"><span data-stu-id="c0594-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c0594-165">query</span><span class="sxs-lookup"><span data-stu-id="c0594-165">query</span></span> |<span data-ttu-id="c0594-166">指定查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c0594-166">Specify the query to read data.</span></span> |<span data-ttu-id="c0594-167">Azure Cosmos DB 所支援的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="c0594-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="c0594-168">範例： `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="c0594-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="c0594-169">否</span><span class="sxs-lookup"><span data-stu-id="c0594-169">No</span></span> <br/><br/><span data-ttu-id="c0594-170">如果未指定，執行的 SQL 陳述式：`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="c0594-170">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="c0594-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="c0594-171">nestingSeparator</span></span> |<span data-ttu-id="c0594-172">用來表示文件為巢狀文件的特殊字元</span><span class="sxs-lookup"><span data-stu-id="c0594-172">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="c0594-173">任何字元。</span><span class="sxs-lookup"><span data-stu-id="c0594-173">Any character.</span></span> <br/><br/><span data-ttu-id="c0594-174">Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。</span><span class="sxs-lookup"><span data-stu-id="c0594-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="c0594-175">Azure Data Factory 可讓使用者透過 nestingSeparator (也就是上述範例中的 “.”) 表示階層</span><span class="sxs-lookup"><span data-stu-id="c0594-175">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="c0594-176">。</span><span class="sxs-lookup"><span data-stu-id="c0594-176">in the above examples.</span></span> <span data-ttu-id="c0594-177">使用分隔符號，複製活動將會根據資料表定義中的 “Name.First”、“Name.Middle” 和 “Name.Last”，產生含有三個子元素 (First、Middle 和 Last) 的 "Name" 物件。</span><span class="sxs-lookup"><span data-stu-id="c0594-177">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="c0594-178">否</span><span class="sxs-lookup"><span data-stu-id="c0594-178">No</span></span> |

<span data-ttu-id="c0594-179">**DocumentDbCollectionSink** 支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="c0594-179">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="c0594-180">**屬性**</span><span class="sxs-lookup"><span data-stu-id="c0594-180">**Property**</span></span> | <span data-ttu-id="c0594-181">**說明**</span><span class="sxs-lookup"><span data-stu-id="c0594-181">**Description**</span></span> | <span data-ttu-id="c0594-182">**允許的值**</span><span class="sxs-lookup"><span data-stu-id="c0594-182">**Allowed values**</span></span> | <span data-ttu-id="c0594-183">**必要**</span><span class="sxs-lookup"><span data-stu-id="c0594-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c0594-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="c0594-184">nestingSeparator</span></span> |<span data-ttu-id="c0594-185">來源資料行名稱中用來表示需要巢狀文件的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="c0594-185">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="c0594-186">就上述範例而言：輸出資料表中的 `Name.First` 會在 Cosmos DB 文件中產生下列 JSON 結構：</span><span class="sxs-lookup"><span data-stu-id="c0594-186">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="c0594-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="c0594-187">"Name": {</span></span><br/>    <span data-ttu-id="c0594-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="c0594-188">"First": "John"</span></span><br/><span data-ttu-id="c0594-189">},</span><span class="sxs-lookup"><span data-stu-id="c0594-189">},</span></span> |<span data-ttu-id="c0594-190">用來分隔巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="c0594-190">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="c0594-191">預設值為 `.` (點)。</span><span class="sxs-lookup"><span data-stu-id="c0594-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="c0594-192">用來分隔巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="c0594-192">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="c0594-193">預設值為 `.` (點)。</span><span class="sxs-lookup"><span data-stu-id="c0594-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="c0594-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="c0594-194">writeBatchSize</span></span> |<span data-ttu-id="c0594-195">為了建立文件而傳送到 Azure Cosmos DB 服務的平行要求數目。</span><span class="sxs-lookup"><span data-stu-id="c0594-195">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="c0594-196">使用這個屬性從 Cosmos DB 來回複製資料時，可以微調效能。</span><span class="sxs-lookup"><span data-stu-id="c0594-196">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="c0594-197">增加 writeBatchSize 時，您可預期有更好的效能，因為對 Cosmos DB 傳送了更多的平行要求。</span><span class="sxs-lookup"><span data-stu-id="c0594-197">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="c0594-198">不過，您必須避免可能擲回錯誤訊息的節流：「要求速率很高」。</span><span class="sxs-lookup"><span data-stu-id="c0594-198">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="c0594-199">節流是由許多因素所決定，包括文件大小、文件中的詞彙數目、目標集合的檢索原則等。對於複製作業，您可以使用更好的集合 (例如 S3) 以取得最多可用輸送量 (2,500 要求單位/秒)。</span><span class="sxs-lookup"><span data-stu-id="c0594-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="c0594-200">Integer</span><span class="sxs-lookup"><span data-stu-id="c0594-200">Integer</span></span> |<span data-ttu-id="c0594-201">否 (預設值：5)</span><span class="sxs-lookup"><span data-stu-id="c0594-201">No (default: 5)</span></span> |
| <span data-ttu-id="c0594-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="c0594-202">writeBatchTimeout</span></span> |<span data-ttu-id="c0594-203">在逾時前等待作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="c0594-203">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="c0594-204">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c0594-204">timespan</span></span><br/><br/> <span data-ttu-id="c0594-205">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="c0594-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="c0594-206">否</span><span class="sxs-lookup"><span data-stu-id="c0594-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="c0594-207">匯入/匯出 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="c0594-207">Import/Export JSON documents</span></span>
<span data-ttu-id="c0594-208">使用此 Cosmos DB 連接器，您可以輕鬆地</span><span class="sxs-lookup"><span data-stu-id="c0594-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="c0594-209">將 JSON 文件從各種來源匯入到 Cosmos DB，包括 Azure Blob、Azure Data Lake、內部部署的檔案系統，或 Azure Data Factory 所支援的其他檔案型存放區。</span><span class="sxs-lookup"><span data-stu-id="c0594-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="c0594-210">將 JSON 文件從 Cosmos DB 集合匯出至各種檔案型存放區。</span><span class="sxs-lookup"><span data-stu-id="c0594-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="c0594-211">在兩個 Cosmos DB 集合之間依原樣移轉資料。</span><span class="sxs-lookup"><span data-stu-id="c0594-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="c0594-212">達成這種無從驗證結構描述的複製</span><span class="sxs-lookup"><span data-stu-id="c0594-212">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="c0594-213">使用複製精靈時，核取 [依原樣匯出到 JSON 檔案或 Cosmos DB 集合] 選項。</span><span class="sxs-lookup"><span data-stu-id="c0594-213">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="c0594-214">使用 JSON 編輯時，請勿在 Cosmos DB 資料集中指定 "structure" 區段，也不要在複製活動的 Cosmos DB 來源/接收器上指定 "nestingSeparator" 屬性。</span><span class="sxs-lookup"><span data-stu-id="c0594-214">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="c0594-215">若要從 JSON 檔案匯入或匯出到這些檔案，請在檔案存放區資料集內，將格式類型指定為 "JsonFormat"、設定 "filePattern"，然後略過其餘格式設定，如需詳細資料，請參閱 [JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)一節。</span><span class="sxs-lookup"><span data-stu-id="c0594-215">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="c0594-216">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="c0594-216">JSON examples</span></span>
<span data-ttu-id="c0594-217">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="c0594-217">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c0594-218">它們示範如何將資料複製到 Azure Cosmos DB 和 Azure Blob 儲存體，以及從中複製資料。</span><span class="sxs-lookup"><span data-stu-id="c0594-218">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="c0594-219">不過，您可以使用 Azure Data Factory 中的「複製活動」，將資料從任何來源「直接」複製到[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)所述的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="c0594-219">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="c0594-220">範例：將資料從 Azure Cosmos DB 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="c0594-220">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="c0594-221">下列範例顯示：</span><span class="sxs-lookup"><span data-stu-id="c0594-221">The sample below shows:</span></span>

1. <span data-ttu-id="c0594-222">[DocumentDb](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="c0594-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="c0594-223">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="c0594-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c0594-224">[DocumentDbCollection](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="c0594-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="c0594-225">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="c0594-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c0594-226">具有使用 [DocumentDbCollectionSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="c0594-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c0594-227">此範例會將 Azure Cosmos DB 中的資料複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="c0594-227">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="c0594-228">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="c0594-228">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c0594-229">**Azure Cosmos DB 連結服務︰**</span><span class="sxs-lookup"><span data-stu-id="c0594-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="c0594-230">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="c0594-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="c0594-231">**Azure DocumentDB 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="c0594-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="c0594-232">此範例假設您在 Azure Cosmos DB 資料庫中擁有名為 Person 的集合。</span><span class="sxs-lookup"><span data-stu-id="c0594-232">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="c0594-233">設定 “external”: ”true” 和指定 externalData 原則即可通知 Data Factory 服務：這是 Azure Data Factory 外部的資料表而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="c0594-233">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="c0594-234">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="c0594-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c0594-235">資料會每小時利用可反映特定日期時間及小時資料粒度的 Blob 路徑，複製到新的 Blob。</span><span class="sxs-lookup"><span data-stu-id="c0594-235">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="c0594-236">Cosmos DB 資料庫中 Person 集合中的範例 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="c0594-236">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="c0594-237">Cosmos DB 支援在階層式 JSON 文件上使用類似 SQL 的語法來查詢文件。</span><span class="sxs-lookup"><span data-stu-id="c0594-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="c0594-238">範例：</span><span class="sxs-lookup"><span data-stu-id="c0594-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="c0594-239">下列管線會將資料從 Azure Cosmos DB 資料庫中的 Person 集合複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="c0594-239">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="c0594-240">複製活動中已指定為輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="c0594-240">As part of the copy activity the input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="c0594-241">範例：將資料從 Azure Blob 複製到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c0594-241">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="c0594-242">下列範例顯示：</span><span class="sxs-lookup"><span data-stu-id="c0594-242">The sample below shows:</span></span>

1. <span data-ttu-id="c0594-243">[DocumentDb](#azure-documentdb-linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="c0594-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="c0594-244">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="c0594-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c0594-245">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="c0594-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="c0594-246">[DocumentDbCollection](#azure-documentdb-dataset-type-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="c0594-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="c0594-247">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="c0594-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="c0594-248">此範例將資料從 Azure Blob 複製到 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="c0594-248">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="c0594-249">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="c0594-249">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c0594-250">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="c0594-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="c0594-251">**Azure Cosmos DB 連結服務︰**</span><span class="sxs-lookup"><span data-stu-id="c0594-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="c0594-252">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="c0594-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="c0594-253">**Azure Cosmos DB 輸出資料集︰**</span><span class="sxs-lookup"><span data-stu-id="c0594-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="c0594-254">此範例會將資料複製到名為 "Person" 的集合。</span><span class="sxs-lookup"><span data-stu-id="c0594-254">The sample copies data to a collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="c0594-255">下列管線會將資料從 Azure Blob 複製到 Cosmos DB 資料庫中的 Person 集合。</span><span class="sxs-lookup"><span data-stu-id="c0594-255">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="c0594-256">複製活動中已指定為輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="c0594-256">As part of the copy activity the input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="c0594-257">如果範例 Blob 輸入為</span><span class="sxs-lookup"><span data-stu-id="c0594-257">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="c0594-258">則 Cosmos DB 中的輸出 JSON 會是：</span><span class="sxs-lookup"><span data-stu-id="c0594-258">Then the output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="c0594-259">Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。</span><span class="sxs-lookup"><span data-stu-id="c0594-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="c0594-260">Azure Data Factory 可讓使用者透過 **nestingSeparator** (也就是此範例中的 “.”) 表示階層</span><span class="sxs-lookup"><span data-stu-id="c0594-260">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="c0594-261">。</span><span class="sxs-lookup"><span data-stu-id="c0594-261">in this example.</span></span> <span data-ttu-id="c0594-262">使用分隔符號，複製活動將會根據資料表定義中的 “Name.First”、“Name.Middle” 和 “Name.Last”，產生含有三個子元素 (First、Middle 和 Last) 的 "Name" 物件。</span><span class="sxs-lookup"><span data-stu-id="c0594-262">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="c0594-263">附錄</span><span class="sxs-lookup"><span data-stu-id="c0594-263">Appendix</span></span>
1. <span data-ttu-id="c0594-264">**問：** 複製活動支援現有記錄的更新嗎？</span><span class="sxs-lookup"><span data-stu-id="c0594-264">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="c0594-265">**答：** 否。</span><span class="sxs-lookup"><span data-stu-id="c0594-265">**Answer:** No.</span></span>
2. <span data-ttu-id="c0594-266">**問題：**的運作方式的複製到 Azure Cosmos DB 處理重試已複製的記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="c0594-266">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="c0594-267">**回：** 如果記錄有 [識別碼] 欄位，而複製作業嘗試插入具有相同識別碼的記錄，則複製作業會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="c0594-267">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="c0594-268">**問題：** Data Factory 支援[範圍或雜湊為基礎的資料分割](../documentdb/documentdb-partition-data.md)嗎？</span><span class="sxs-lookup"><span data-stu-id="c0594-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="c0594-269">**答：** 否。</span><span class="sxs-lookup"><span data-stu-id="c0594-269">**Answer:** No.</span></span>
4. <span data-ttu-id="c0594-270">**問題：**我可以指定資料表的多個 Azure Cosmos DB 集合嗎？</span><span class="sxs-lookup"><span data-stu-id="c0594-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="c0594-271">**答：** 否。</span><span class="sxs-lookup"><span data-stu-id="c0594-271">**Answer:** No.</span></span> <span data-ttu-id="c0594-272">目前只能指定一個集合。</span><span class="sxs-lookup"><span data-stu-id="c0594-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c0594-273">效能和微調</span><span class="sxs-lookup"><span data-stu-id="c0594-273">Performance and Tuning</span></span>
<span data-ttu-id="c0594-274">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="c0594-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
