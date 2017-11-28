---
title: "aaaMove 資料從 Azure Cosmos DB / |Microsoft 文件"
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
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="3bc2f-103">從使用 Azure Data Factory 的 Azure Cosmos DB 移動資料 tooand</span><span class="sxs-lookup"><span data-stu-id="3bc2f-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="3bc2f-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從 Azure Cosmos DB (DocumentDB API) 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="3bc2f-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="3bc2f-106">您可以從任何支援的來源資料儲存 tooAzure Cosmos DB，或從 Azure Cosmos DB tooany 支援接收資料存放區來複製資料。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="3bc2f-107">如需支援做為來源或接收器 hello 複製活動的資料存放區的清單，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3bc2f-108">Azure Cosmos DB 連接器只支援 DocumentDB API。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="3bc2f-109">toocopy 資料當做-是要從/JSON 檔案或另一個 Cosmos DB 集合，請參閱[匯入/匯出 JSON 文件](#importexport-json-documents)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="3bc2f-110">開始使用</span><span class="sxs-lookup"><span data-stu-id="3bc2f-110">Getting started</span></span>
<span data-ttu-id="3bc2f-111">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="3bc2f-112">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="3bc2f-113">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="3bc2f-114">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3bc2f-115">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3bc2f-116">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="3bc2f-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="3bc2f-117">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="3bc2f-118">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="3bc2f-119">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3bc2f-120">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="3bc2f-121">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="3bc2f-122">如需使用的 toocopy 資料，從 Cosmos DB 的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples)本文一節。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="3bc2f-123">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooCosmos DB 的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="3bc2f-124">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="3bc2f-124">Linked service properties</span></span>
<span data-ttu-id="3bc2f-125">下表中的 hello 提供 JSON 項目特定 tooAzure Cosmos 資料庫連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="3bc2f-126">**屬性**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-126">**Property**</span></span> | <span data-ttu-id="3bc2f-127">**說明**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-127">**Description**</span></span> | <span data-ttu-id="3bc2f-128">**必要**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3bc2f-129">類型</span><span class="sxs-lookup"><span data-stu-id="3bc2f-129">type</span></span> |<span data-ttu-id="3bc2f-130">hello 類型屬性必須設定為： **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="3bc2f-131">是</span><span class="sxs-lookup"><span data-stu-id="3bc2f-131">Yes</span></span> |
| <span data-ttu-id="3bc2f-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="3bc2f-132">connectionString</span></span> |<span data-ttu-id="3bc2f-133">指定所需 tooconnect tooAzure Cosmos DB 資料庫的資訊。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="3bc2f-134">是</span><span class="sxs-lookup"><span data-stu-id="3bc2f-134">Yes</span></span> |

<span data-ttu-id="3bc2f-135">範例：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-135">Example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="3bc2f-136">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="3bc2f-136">Dataset properties</span></span>
<span data-ttu-id="3bc2f-137">如需區段和屬性可用來定義資料集的完整清單，請參閱 toohello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3bc2f-138">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3bc2f-139">hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="3bc2f-140">hello typeProperties 區段 hello 資料集型別的**DocumentDbCollection**具有下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="3bc2f-141">**屬性**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-141">**Property**</span></span> | <span data-ttu-id="3bc2f-142">**說明**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-142">**Description**</span></span> | <span data-ttu-id="3bc2f-143">**必要**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3bc2f-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="3bc2f-144">collectionName</span></span> |<span data-ttu-id="3bc2f-145">Hello Cosmos DB 文件集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="3bc2f-146">是</span><span class="sxs-lookup"><span data-stu-id="3bc2f-146">Yes</span></span> |

<span data-ttu-id="3bc2f-147">範例：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-147">Example:</span></span>

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
### <a name="schema-by-data-factory"></a><span data-ttu-id="3bc2f-148">Data factory 的結構描述</span><span class="sxs-lookup"><span data-stu-id="3bc2f-148">Schema by Data Factory</span></span>
<span data-ttu-id="3bc2f-149">針對無結構描述的資料存放區，例如 Azure Cosmos DB，hello Data Factory 服務會推斷 hello 結構描述 hello 下列方式之一：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="3bc2f-150">如果您指定資料的 hello 結構使用 hello**結構**hello 資料集定義，hello Data Factory 服務中的屬性會接受此結構做為 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="3bc2f-151">在此情況下，如果資料列不包含資料行的值，則會使用 null 值。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="3bc2f-152">如果您未指定資料 hello 結構使用 hello**結構**hello 資料集定義，hello Data Factory 服務中的屬性會推斷 hello 結構描述使用 hello 資料中的 hello 第一個資料列。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="3bc2f-153">在此情況下，如果 hello 第一個資料列不包含 hello 完整結構描述，某些資料行將會遺失在 hello 的複製作業的結果。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="3bc2f-154">因此，對於無結構描述的資料來源，hello 最佳作法是使用 hello 資料 toospecify hello 結構**結構**屬性。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="3bc2f-155">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="3bc2f-155">Copy activity properties</span></span>
<span data-ttu-id="3bc2f-156">如需區段和屬性可用來定義活動的完整清單，請參閱 toohello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3bc2f-157">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="3bc2f-158">hello 複製活動會採用只有 1 個輸入，並產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="3bc2f-159">屬性中的 hello hello 活動 hello typeProperties 區段可用另一方面改變與每個活動類型與它們的來源與接收的 hello 類型而異的複製活動發生。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="3bc2f-160">當來源的類型時，複製活動發生**DocumentDbCollectionSource** hello 下列屬性可用於**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="3bc2f-161">**屬性**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-161">**Property**</span></span> | <span data-ttu-id="3bc2f-162">**說明**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-162">**Description**</span></span> | <span data-ttu-id="3bc2f-163">**允許的值**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-163">**Allowed values**</span></span> | <span data-ttu-id="3bc2f-164">**必要**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3bc2f-165">query</span><span class="sxs-lookup"><span data-stu-id="3bc2f-165">query</span></span> |<span data-ttu-id="3bc2f-166">指定 hello 查詢 tooread 資料。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="3bc2f-167">Azure Cosmos DB 所支援的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="3bc2f-168">範例： `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="3bc2f-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="3bc2f-169">否</span><span class="sxs-lookup"><span data-stu-id="3bc2f-169">No</span></span> <br/><br/><span data-ttu-id="3bc2f-170">如果未指定，hello 執行的 SQL 陳述式：`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="3bc2f-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="3bc2f-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="3bc2f-171">nestingSeparator</span></span> |<span data-ttu-id="3bc2f-172">巢狀 hello 文件的特殊字元 tooindicate</span><span class="sxs-lookup"><span data-stu-id="3bc2f-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="3bc2f-173">任何字元。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-173">Any character.</span></span> <br/><br/><span data-ttu-id="3bc2f-174">Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="3bc2f-175">Azure Data Factory 可讓使用者 toodenote 階層 nestingSeparator，也就是透過 「。 」</span><span class="sxs-lookup"><span data-stu-id="3bc2f-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="3bc2f-176">在上述範例 hello。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-176">in hello above examples.</span></span> <span data-ttu-id="3bc2f-177">Hello 分隔符號 hello 複製活動會產生三個子系的元素與 hello"Name"物件第一個中間和最後一個、 相應 too"Name.First"，"Name.Middle"和"Name.Last"hello 在資料表定義。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="3bc2f-178">否</span><span class="sxs-lookup"><span data-stu-id="3bc2f-178">No</span></span> |

<span data-ttu-id="3bc2f-179">**DocumentDbCollectionSink**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="3bc2f-180">**屬性**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-180">**Property**</span></span> | <span data-ttu-id="3bc2f-181">**說明**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-181">**Description**</span></span> | <span data-ttu-id="3bc2f-182">**允許的值**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-182">**Allowed values**</span></span> | <span data-ttu-id="3bc2f-183">**必要**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3bc2f-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="3bc2f-184">nestingSeparator</span></span> |<span data-ttu-id="3bc2f-185">需要 hello 來源資料行名稱 tooindicate 巢狀文件中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="3bc2f-186">例如上述： `Name.First` hello 輸出資料表會產生下列 JSON 結構 hello Cosmos DB 文件中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3bc2f-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="3bc2f-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="3bc2f-187">"Name": {</span></span><br/>    <span data-ttu-id="3bc2f-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="3bc2f-188">"First": "John"</span></span><br/><span data-ttu-id="3bc2f-189">},</span><span class="sxs-lookup"><span data-stu-id="3bc2f-189">},</span></span> |<span data-ttu-id="3bc2f-190">為使用的 tooseparate 巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="3bc2f-191">預設值為 `.` (點)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="3bc2f-192">為使用的 tooseparate 巢狀層級的字元。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="3bc2f-193">預設值為 `.` (點)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="3bc2f-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3bc2f-194">writeBatchSize</span></span> |<span data-ttu-id="3bc2f-195">並行要求數目 tooAzure Cosmos DB 服務 toocreate 文件。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="3bc2f-196">使用這個屬性來複製從 Cosmos DB 的資料時，您可以微調 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="3bc2f-197">當您增加叫用 writeBatchSize，因為會傳送多個平行要求 tooCosmos DB 時，您可以預期更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="3bc2f-198">不過，您必須先 tooavoid 節流，可擲回 hello 錯誤訊息: 「 要求率非常大 」。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="3bc2f-199">節流是由許多因素所決定，包括文件大小、文件中的詞彙數目、目標集合的檢索原則等。複製作業，您可以使用較佳的集合 (例如 S3) toohave hello 大部分可用的輸送量 （2500 的要求單位/秒）。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="3bc2f-200">Integer</span><span class="sxs-lookup"><span data-stu-id="3bc2f-200">Integer</span></span> |<span data-ttu-id="3bc2f-201">否 (預設值：5)</span><span class="sxs-lookup"><span data-stu-id="3bc2f-201">No (default: 5)</span></span> |
| <span data-ttu-id="3bc2f-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3bc2f-202">writeBatchTimeout</span></span> |<span data-ttu-id="3bc2f-203">在逾時之前，請等待 hello 作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="3bc2f-204">時間範圍</span><span class="sxs-lookup"><span data-stu-id="3bc2f-204">timespan</span></span><br/><br/> <span data-ttu-id="3bc2f-205">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="3bc2f-206">否</span><span class="sxs-lookup"><span data-stu-id="3bc2f-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="3bc2f-207">匯入/匯出 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="3bc2f-207">Import/Export JSON documents</span></span>
<span data-ttu-id="3bc2f-208">使用此 Cosmos DB 連接器，您可以輕鬆地</span><span class="sxs-lookup"><span data-stu-id="3bc2f-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="3bc2f-209">將 JSON 文件從各種來源匯入到 Cosmos DB，包括 Azure Blob、Azure Data Lake、內部部署的檔案系統，或 Azure Data Factory 所支援的其他檔案型存放區。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="3bc2f-210">將 JSON 文件從 Cosmos DB 集合匯出至各種檔案型存放區。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="3bc2f-211">在兩個 Cosmos DB 集合之間依原樣移轉資料。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="3bc2f-212">tooachieve 複製這類結構描述無關，</span><span class="sxs-lookup"><span data-stu-id="3bc2f-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="3bc2f-213">複製精靈時，請檢查 hello **」 匯出為-tooJSON 檔案或 Cosmos DB 集合"**選項。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="3bc2f-214">當使用 JSON 編輯，請不要指定 hello 「 結構 」 一節中的 Cosmos DB 的資料集，也不 Cosmos DB 上的 「 nestingSeparator"屬性來源/接收器複製活動中。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="3bc2f-215">從 tooimport / 匯出 tooJSON 檔案，資料集中 hello 檔案存放區格式類型指定為"JsonFormat，「 組態 」 filePattern 」 並略過 hello rest 格式設定，請參閱[JSON 格式](data-factory-supported-file-and-compression-formats.md#json-format)詳細資料 區段。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="3bc2f-216">JSON 範例</span><span class="sxs-lookup"><span data-stu-id="3bc2f-216">JSON examples</span></span>
<span data-ttu-id="3bc2f-217">hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3bc2f-218">它們會顯示如何從 Azure Cosmos DB 和 Azure Blob 儲存體 toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="3bc2f-219">不過，資料可以複製**直接**從任何 hello 接收所述的 hello 來源 tooany[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="3bc2f-220">範例： 將資料從 Azure Cosmos DB tooAzure Blob 複製</span><span class="sxs-lookup"><span data-stu-id="3bc2f-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="3bc2f-221">顯示 hello 以下的範例：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-221">hello sample below shows:</span></span>

1. <span data-ttu-id="3bc2f-222">[DocumentDb](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="3bc2f-223">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3bc2f-224">[DocumentDbCollection](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="3bc2f-225">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3bc2f-226">具有使用 [DocumentDbCollectionSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3bc2f-227">hello 範例會在 Azure Cosmos DB tooAzure Blob 複製資料。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="3bc2f-228">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="3bc2f-229">**Azure Cosmos DB 連結服務︰**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-229">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="3bc2f-230">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="3bc2f-231">**Azure DocumentDB 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="3bc2f-232">hello 範例假設您擁有名為的集合**人員**Azure Cosmos DB 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="3bc2f-233">設定"external":"true"，並指定 externalData hello Azure Data Factory 服務該 hello 資料表的原則資訊是外部 toohello 資料處理站，而不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="3bc2f-234">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="3bc2f-235">資料會複製的 tooa 新 blob hello 路徑 hello blob 反映 hello 特定的日期時間的小時資料粒度的每個小時。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

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
<span data-ttu-id="3bc2f-236">範例 hello Cosmos DB 資料庫中的人員集合中的 JSON 文件：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

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
<span data-ttu-id="3bc2f-237">Cosmos DB 支援在階層式 JSON 文件上使用類似 SQL 的語法來查詢文件。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="3bc2f-238">範例：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="3bc2f-239">hello 下列管線將資料從 hello hello Azure Cosmos DB 資料庫 tooan Azure blob 中的使用者集合。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="3bc2f-240">Hello 複製活動 hello 一部分已指定輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

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
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="3bc2f-241">範例： 將資料從 Azure Blob tooAzure Cosmos DB 複製</span><span class="sxs-lookup"><span data-stu-id="3bc2f-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="3bc2f-242">顯示 hello 以下的範例：</span><span class="sxs-lookup"><span data-stu-id="3bc2f-242">hello sample below shows:</span></span>

1. <span data-ttu-id="3bc2f-243">[DocumentDb](#azure-documentdb-linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="3bc2f-244">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3bc2f-245">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="3bc2f-246">[DocumentDbCollection](#azure-documentdb-dataset-type-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="3bc2f-247">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="3bc2f-248">hello 範例會將資料從 Azure blob tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="3bc2f-249">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="3bc2f-250">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="3bc2f-251">**Azure Cosmos DB 連結服務︰**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-251">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="3bc2f-252">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-252">**Azure Blob input dataset:**</span></span>

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
<span data-ttu-id="3bc2f-253">**Azure Cosmos DB 輸出資料集︰**</span><span class="sxs-lookup"><span data-stu-id="3bc2f-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="3bc2f-254">hello 範例會從名為"Person"的資料 tooa 集合複製。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-254">hello sample copies data tooa collection named “Person”.</span></span>

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
<span data-ttu-id="3bc2f-255">hello 下列管線將資料從 Azure Blob toohello hello Cosmos DB 中的使用者集合。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="3bc2f-256">Hello 複製活動 hello 一部分已指定輸入和輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
<span data-ttu-id="3bc2f-257">如果輸入 hello 範例 blob 做</span><span class="sxs-lookup"><span data-stu-id="3bc2f-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="3bc2f-258">然後 hello 的輸出就會在 Cosmos DB 中的 JSON:</span><span class="sxs-lookup"><span data-stu-id="3bc2f-258">Then hello output JSON in Cosmos DB will be as:</span></span>

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
<span data-ttu-id="3bc2f-259">Azure Cosmos DB 是 JSON 文件的 NoSQL 存放區 (允許巢狀結構)。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="3bc2f-260">Azure Data Factory 可讓使用者透過的 toodenote 階層**nestingSeparator**，也就是"。"</span><span class="sxs-lookup"><span data-stu-id="3bc2f-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="3bc2f-261">。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-261">in this example.</span></span> <span data-ttu-id="3bc2f-262">Hello 分隔符號 hello 複製活動會產生三個子系的元素與 hello"Name"物件第一個中間和最後一個、 相應 too"Name.First"，"Name.Middle"和"Name.Last"hello 在資料表定義。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="3bc2f-263">附錄</span><span class="sxs-lookup"><span data-stu-id="3bc2f-263">Appendix</span></span>
1. <span data-ttu-id="3bc2f-264">**問題：**沒有 hello 複製活動支援更新現有的記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="3bc2f-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="3bc2f-265">**答：** 否。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-265">**Answer:** No.</span></span>
2. <span data-ttu-id="3bc2f-266">**問題：**的運作方式的複製 tooAzure Cosmos DB 處理重試已複製的記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="3bc2f-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="3bc2f-267">**回答：**如果記錄具有 「 識別碼 」 欄位，而且 hello 複製作業會嘗試 tooinsert hello 的記錄相同識別碼 hello 複製作業會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="3bc2f-268">**問：**Data Factory 支援[範圍或雜湊式資料分割](../documentdb/documentdb-partition-data.md)嗎？</span><span class="sxs-lookup"><span data-stu-id="3bc2f-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="3bc2f-269">**答：** 否。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-269">**Answer:** No.</span></span>
4. <span data-ttu-id="3bc2f-270">**問：**我可以為資料表指定多個 Azure Cosmos DB 集合嗎？</span><span class="sxs-lookup"><span data-stu-id="3bc2f-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="3bc2f-271">**答：** 否。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-271">**Answer:** No.</span></span> <span data-ttu-id="3bc2f-272">目前只能指定一個集合。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3bc2f-273">效能和微調</span><span class="sxs-lookup"><span data-stu-id="3bc2f-273">Performance and Tuning</span></span>
<span data-ttu-id="3bc2f-274">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="3bc2f-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
