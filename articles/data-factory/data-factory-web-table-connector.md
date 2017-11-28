---
title: "從 Web 表中使用 Azure Data Factory aaaMove 資料 |Microsoft 文件"
description: "深入了解如何使用 web 資料表的 toomove 資料頁面上使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="b4894-103">使用 Azure Data Factory 來移動 Web 資料表的資料</span><span class="sxs-lookup"><span data-stu-id="b4894-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="b4894-104">本文概述如何在 Azure Data Factory toomove 資料從資料表中的網頁 tooa toouse hello 複製活動支援接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b4894-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="b4894-105">這篇文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)呈現資料移動的一般概觀，以及複製活動與 hello 清單做為來源/接收器所支援的資料存放區的發行項。</span><span class="sxs-lookup"><span data-stu-id="b4894-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="b4894-106">目前資料處理站都會支援只從 Web 資料表 tooother 資料移動的資料存放區，但不是將資料從其他資料會儲存 tooa Web 資料表的目的地。</span><span class="sxs-lookup"><span data-stu-id="b4894-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4894-107">此 Web 連接器目前只支援從 HTML 網頁擷取資料表內容。</span><span class="sxs-lookup"><span data-stu-id="b4894-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="b4894-108">從 HTTP/s 的端點，tooretrieve 資料使用[HTTP 連接器](data-factory-http-connector.md)改為。</span><span class="sxs-lookup"><span data-stu-id="b4894-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b4894-109">開始使用</span><span class="sxs-lookup"><span data-stu-id="b4894-109">Getting started</span></span>
<span data-ttu-id="b4894-110">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="b4894-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="b4894-111">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="b4894-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="b4894-112">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="b4894-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="b4894-113">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="b4894-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b4894-114">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="b4894-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b4894-115">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="b4894-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="b4894-116">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="b4894-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="b4894-117">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="b4894-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="b4894-118">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="b4894-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b4894-119">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="b4894-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="b4894-120">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="b4894-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="b4894-121">具有使用的 toocopy 資料從 web 資料表的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Web 資料表 tooAzure Blob 複製](#json-example-copy-data-from-web-table-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="b4894-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="b4894-122">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa Web 資料表的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="b4894-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b4894-123">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="b4894-123">Linked service properties</span></span>
<span data-ttu-id="b4894-124">下表中的 hello 提供 JSON 項目特定 tooWeb 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="b4894-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="b4894-125">屬性</span><span class="sxs-lookup"><span data-stu-id="b4894-125">Property</span></span> | <span data-ttu-id="b4894-126">說明</span><span class="sxs-lookup"><span data-stu-id="b4894-126">Description</span></span> | <span data-ttu-id="b4894-127">必要</span><span class="sxs-lookup"><span data-stu-id="b4894-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4894-128">類型</span><span class="sxs-lookup"><span data-stu-id="b4894-128">type</span></span> |<span data-ttu-id="b4894-129">hello 類型屬性必須設定為： **Web**</span><span class="sxs-lookup"><span data-stu-id="b4894-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="b4894-130">是</span><span class="sxs-lookup"><span data-stu-id="b4894-130">Yes</span></span> |
| <span data-ttu-id="b4894-131">Url</span><span class="sxs-lookup"><span data-stu-id="b4894-131">Url</span></span> |<span data-ttu-id="b4894-132">URL toohello Web 來源</span><span class="sxs-lookup"><span data-stu-id="b4894-132">URL toohello Web source</span></span> |<span data-ttu-id="b4894-133">是</span><span class="sxs-lookup"><span data-stu-id="b4894-133">Yes</span></span> |
| <span data-ttu-id="b4894-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="b4894-134">authenticationType</span></span> |<span data-ttu-id="b4894-135">匿名。</span><span class="sxs-lookup"><span data-stu-id="b4894-135">Anonymous.</span></span> |<span data-ttu-id="b4894-136">是</span><span class="sxs-lookup"><span data-stu-id="b4894-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="b4894-137">使用匿名驗證</span><span class="sxs-lookup"><span data-stu-id="b4894-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="b4894-138">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="b4894-138">Dataset properties</span></span>
<span data-ttu-id="b4894-139">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="b4894-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b4894-140">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="b4894-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b4894-141">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b4894-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b4894-142">hello typeProperties 區段類型的資料集**WebTable**具有下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="b4894-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="b4894-143">屬性</span><span class="sxs-lookup"><span data-stu-id="b4894-143">Property</span></span> | <span data-ttu-id="b4894-144">說明</span><span class="sxs-lookup"><span data-stu-id="b4894-144">Description</span></span> | <span data-ttu-id="b4894-145">必要</span><span class="sxs-lookup"><span data-stu-id="b4894-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b4894-146">類型</span><span class="sxs-lookup"><span data-stu-id="b4894-146">type</span></span> |<span data-ttu-id="b4894-147">hello 資料集的類型。</span><span class="sxs-lookup"><span data-stu-id="b4894-147">type of hello dataset.</span></span> <span data-ttu-id="b4894-148">必須設定得**WebTable**</span><span class="sxs-lookup"><span data-stu-id="b4894-148">must be set too**WebTable**</span></span> |<span data-ttu-id="b4894-149">是</span><span class="sxs-lookup"><span data-stu-id="b4894-149">Yes</span></span> |
| <span data-ttu-id="b4894-150">路徑</span><span class="sxs-lookup"><span data-stu-id="b4894-150">path</span></span> |<span data-ttu-id="b4894-151">相對 URL toohello 資源包含 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="b4894-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="b4894-152">否。</span><span class="sxs-lookup"><span data-stu-id="b4894-152">No.</span></span> <span data-ttu-id="b4894-153">若未指定路徑，則會使用連結的 hello 服務定義中指定的唯一 hello URL。</span><span class="sxs-lookup"><span data-stu-id="b4894-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="b4894-154">index</span><span class="sxs-lookup"><span data-stu-id="b4894-154">index</span></span> |<span data-ttu-id="b4894-155">hello hello 資源中的 hello 資料表的索引。</span><span class="sxs-lookup"><span data-stu-id="b4894-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="b4894-156">請參閱[Get 索引的資料表中的 HTML 網頁的](#get-index-of-a-table-in-an-html-page)> 一節步驟 toogetting 索引的 HTML 網頁中的資料表。</span><span class="sxs-lookup"><span data-stu-id="b4894-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="b4894-157">是</span><span class="sxs-lookup"><span data-stu-id="b4894-157">Yes</span></span> |

<span data-ttu-id="b4894-158">**範例：**</span><span class="sxs-lookup"><span data-stu-id="b4894-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="b4894-159">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="b4894-159">Copy activity properties</span></span>
<span data-ttu-id="b4894-160">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="b4894-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b4894-161">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="b4894-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="b4894-162">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="b4894-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="b4894-163">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="b4894-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="b4894-164">目前，當複製活動中的 hello 來源屬於型別**WebSource**，支援任何其他屬性。</span><span class="sxs-lookup"><span data-stu-id="b4894-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="b4894-165">JSON 範例： 從 Web 資料表 tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="b4894-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="b4894-166">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="b4894-166">hello following sample shows:</span></span>

1. <span data-ttu-id="b4894-167">[Web](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="b4894-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="b4894-168">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="b4894-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b4894-169">[WebTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b4894-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b4894-170">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b4894-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b4894-171">具有使用 [WebSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="b4894-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b4894-172">hello 範例將資料從 Azure blob Web 資料表 tooan 每小時。</span><span class="sxs-lookup"><span data-stu-id="b4894-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="b4894-173">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="b4894-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="b4894-174">hello 下列範例顯示如何從 Web 資料表 tooan Azure toocopy 資料的 blob。</span><span class="sxs-lookup"><span data-stu-id="b4894-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="b4894-175">不過，資料可以複製直接的 hello tooany 接收器中所述的 hello[資料移動活動](data-factory-data-movement-activities.md)hello 複製活動使用 Azure Data Factory 中的發行項。</span><span class="sxs-lookup"><span data-stu-id="b4894-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="b4894-176">**Web 連結服務**本例使用 hello Web 連結服務與匿名驗證。</span><span class="sxs-lookup"><span data-stu-id="b4894-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="b4894-177">請參閱 [Web 連結服務](#linked-service-properties) 一節，來了解您可以使用的不同驗證類型。</span><span class="sxs-lookup"><span data-stu-id="b4894-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="b4894-178">**Azure 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="b4894-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="b4894-179">**WebTable 的輸入資料集**設定**外部**太**true**該 hello 集外部 toohello 資料處理站，且不產生 hello 中的活動時，會通知 hello Data Factory 服務資料處理站。</span><span class="sxs-lookup"><span data-stu-id="b4894-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="b4894-180">請參閱[Get 索引的資料表中的 HTML 網頁的](#get-index-of-a-table-in-an-html-page)> 一節步驟 toogetting 索引的 HTML 網頁中的資料表。</span><span class="sxs-lookup"><span data-stu-id="b4894-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="b4894-181">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="b4894-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="b4894-182">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="b4894-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="b4894-183">**具有複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="b4894-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="b4894-184">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="b4894-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="b4894-185">在 hello 管線 JSON 定義中，hello**來源**類型設定得**WebSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="b4894-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="b4894-186">請參閱[WebSource 類型屬性](#copy-activity-type-properties)hello hello WebSource 支援之屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="b4894-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="b4894-187">取得 HTML 網頁中資料表的索引</span><span class="sxs-lookup"><span data-stu-id="b4894-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="b4894-188">啟動**Excel 2016**切換 toohello**資料** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b4894-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="b4894-189">按一下**新查詢**hello 在工具列上，指向 太**從其他來源**按一下**從 Web**。</span><span class="sxs-lookup"><span data-stu-id="b4894-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Power Query 功能表](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="b4894-191">在 hello**從 Web**對話方塊方塊中，輸入**URL**您在將使用連結的服務 JSON (例如： https://en.wikipedia.org/wiki/) 以及您可以為 hello 資料集指定的路徑 (例如： AFI %27s_100_Years...100_Movies)，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="b4894-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![[從 Web] 對話方塊](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="b4894-193">此範例中使用的 URL：https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="b4894-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="b4894-194">如果您看到**存取 Web 內容**對話方塊中，選取 hello 右邊**URL**，**驗證**，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="b4894-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![[存取 Web 內容] 對話方塊](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="b4894-196">按一下**資料表**hello 樹狀結構檢視 toosee 內容從 hello 資料表中的項目，然後按一下**編輯**hello 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b4894-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![[導覽器] 對話方塊](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="b4894-198">在 hello**查詢編輯器**視窗中，按一下**進階編輯器**hello 工具列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b4894-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![[進階編輯器] 按鈕](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="b4894-200">在 hello [進階編輯器] 對話方塊中，hello 數目接下來太 「 來源 」 是 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="b4894-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![進階編輯器及索引](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="b4894-202">如果您使用 Excel 2013，使用[Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello 索引。</span><span class="sxs-lookup"><span data-stu-id="b4894-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="b4894-203">請參閱[連接 tooa 網頁](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8)文件以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b4894-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="b4894-204">hello 步驟很相似，但您使用[Microsoft Power BI desktop](https://powerbi.microsoft.com/desktop/)。</span><span class="sxs-lookup"><span data-stu-id="b4894-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="b4894-205">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="b4894-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b4894-206">效能和微調</span><span class="sxs-lookup"><span data-stu-id="b4894-206">Performance and Tuning</span></span>
<span data-ttu-id="b4894-207">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="b4894-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
