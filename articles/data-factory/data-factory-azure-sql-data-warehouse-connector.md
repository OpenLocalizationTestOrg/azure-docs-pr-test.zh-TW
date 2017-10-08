---
title: "aaaCopy 資料從 Azure SQL 資料倉儲的 / |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 Azure SQL 資料倉儲中的 toocopy 資料"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="2e1f6-103">從 Azure SQL 資料倉儲使用 Azure Data Factory 複製資料 tooand</span><span class="sxs-lookup"><span data-stu-id="2e1f6-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="2e1f6-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從 Azure SQL 資料倉儲中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2e1f6-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="2e1f6-106">tooachieve 最佳效能，使用 PolyBase tooload 資料到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2e1f6-107">hello[使用 PolyBase tooload 資料到 Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse)> 一節有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="2e1f6-108">如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="2e1f6-109">支援的案例</span><span class="sxs-lookup"><span data-stu-id="2e1f6-109">Supported scenarios</span></span>
<span data-ttu-id="2e1f6-110">您可以將資料複製**從 Azure SQL 資料倉儲**toohello 下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="2e1f6-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="2e1f6-111">您可以將資料複製下列資料存放區的 hello **tooAzure SQL 資料倉儲**:</span><span class="sxs-lookup"><span data-stu-id="2e1f6-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="2e1f6-112">從 SQL Server 或 Azure SQL Database tooAzure 複製資料時 SQL 資料倉儲，如果 hello 資料表不存在於 hello 目的地存放區，資料處理站可以自動建立 hello 資料表在 SQL 資料倉儲中使用 hello 來源中的 hello hello 資料表結構描述資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="2e1f6-113">請參閱[自動建立資料表](#auto-table-creation)以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="2e1f6-114">支援的驗證類型</span><span class="sxs-lookup"><span data-stu-id="2e1f6-114">Supported authentication type</span></span>
<span data-ttu-id="2e1f6-115">Azure SQL 資料倉儲連接器支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2e1f6-116">開始使用</span><span class="sxs-lookup"><span data-stu-id="2e1f6-116">Getting started</span></span>
<span data-ttu-id="2e1f6-117">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出「Azure SQL 資料倉儲」。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="2e1f6-118">最簡單方式 toocreate hello 管線可將資料從 Azure SQL 資料倉儲複製是 toouse hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="2e1f6-119">請參閱[教學課程： 將資料載入 SQL 資料倉儲與 Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="2e1f6-120">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2e1f6-121">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="2e1f6-122">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e1f6-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2e1f6-123">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-123">Create a **data factory**.</span></span> <span data-ttu-id="2e1f6-124">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="2e1f6-125">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="2e1f6-126">例如，如果您從 Azure blob 儲存體 tooan Azure SQL 資料倉儲中複製資料，您建立兩個連結的服務 toolink 您的 Azure 儲存體帳戶和 Azure SQL 資料倉儲 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="2e1f6-127">連結的服務是特定 tooAzure SQL 資料倉儲的內容，請參閱[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="2e1f6-128">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="2e1f6-129">在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="2e1f6-130">而且，您建立另一個資料集 toospecify hello 資料表保存 hello 資料複製 hello blob 儲存體中的 hello Azure SQL 資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="2e1f6-131">如為特定 tooAzure SQL 資料倉儲的資料集屬性，請參閱[資料集屬性](#dataset-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="2e1f6-132">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="2e1f6-133">在先前所述 hello 範例中，您使用 BlobSource 作為來源和 SqlDWSink 做為接收器 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="2e1f6-134">同樣地，如果您要複製 Azure SQL 資料倉儲 tooAzure Blob 儲存體，您使用 SqlDWSource 和 BlobSink hello 複製活動中。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="2e1f6-135">複製活動是特定 tooAzure SQL 資料倉儲的屬性，請參閱[複製活動屬性](#copy-activity-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="2e1f6-136">如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="2e1f6-137">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2e1f6-138">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2e1f6-139">如需使用的 toocopy 資料至 azure 或從 Azure SQL 資料倉儲的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-sql-data-warehouse)本文一節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="2e1f6-140">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure SQL 資料倉儲的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="2e1f6-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2e1f6-141">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="2e1f6-141">Linked service properties</span></span>
<span data-ttu-id="2e1f6-142">下表中的 hello 提供 JSON 項目特定 tooAzure SQL 資料倉儲連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="2e1f6-143">屬性</span><span class="sxs-lookup"><span data-stu-id="2e1f6-143">Property</span></span> | <span data-ttu-id="2e1f6-144">說明</span><span class="sxs-lookup"><span data-stu-id="2e1f6-144">Description</span></span> | <span data-ttu-id="2e1f6-145">必要</span><span class="sxs-lookup"><span data-stu-id="2e1f6-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e1f6-146">類型</span><span class="sxs-lookup"><span data-stu-id="2e1f6-146">type</span></span> |<span data-ttu-id="2e1f6-147">hello 類型屬性必須設定為： **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="2e1f6-148">是</span><span class="sxs-lookup"><span data-stu-id="2e1f6-148">Yes</span></span> |
| <span data-ttu-id="2e1f6-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="2e1f6-149">connectionString</span></span> |<span data-ttu-id="2e1f6-150">指定所需的資訊 tooconnect toohello Azure SQL 資料倉儲執行個體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="2e1f6-151">僅支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="2e1f6-152">是</span><span class="sxs-lookup"><span data-stu-id="2e1f6-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="2e1f6-153">設定[Azure SQL Database 防火牆](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)太 hello 資料庫伺服器和[允許 Azure 服務 tooaccess hello 伺服器](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="2e1f6-154">此外，如果您要從內部部署資料來源與資料處理站閘道外部 Azure 包括複製資料 tooAzure SQL 資料倉儲，設定正在傳送資料 tooAzure SQL 資料倉儲的 hello 機器的適當 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="2e1f6-155">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="2e1f6-155">Dataset properties</span></span>
<span data-ttu-id="2e1f6-156">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2e1f6-157">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2e1f6-158">hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2e1f6-159">hello **typeProperties** hello 資料集的類型 > 一節**AzureSqlDWTable**具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e1f6-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="2e1f6-160">屬性</span><span class="sxs-lookup"><span data-stu-id="2e1f6-160">Property</span></span> | <span data-ttu-id="2e1f6-161">說明</span><span class="sxs-lookup"><span data-stu-id="2e1f6-161">Description</span></span> | <span data-ttu-id="2e1f6-162">必要</span><span class="sxs-lookup"><span data-stu-id="2e1f6-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e1f6-163">tableName</span><span class="sxs-lookup"><span data-stu-id="2e1f6-163">tableName</span></span> |<span data-ttu-id="2e1f6-164">參照 hello 資料表或檢視 hello 連結的服務的 hello Azure SQL 資料倉儲資料庫中的名稱。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="2e1f6-165">是</span><span class="sxs-lookup"><span data-stu-id="2e1f6-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2e1f6-166">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="2e1f6-166">Copy activity properties</span></span>
<span data-ttu-id="2e1f6-167">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2e1f6-168">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="2e1f6-169">hello 複製活動會採用只有 1 個輸入，並產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="2e1f6-170">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2e1f6-171">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="2e1f6-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="2e1f6-172">SqlDWSource</span></span>
<span data-ttu-id="2e1f6-173">當來源屬於型別**SqlDWSource**中的下列屬性的 hello 可用**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="2e1f6-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="2e1f6-174">屬性</span><span class="sxs-lookup"><span data-stu-id="2e1f6-174">Property</span></span> | <span data-ttu-id="2e1f6-175">說明</span><span class="sxs-lookup"><span data-stu-id="2e1f6-175">Description</span></span> | <span data-ttu-id="2e1f6-176">允許的值</span><span class="sxs-lookup"><span data-stu-id="2e1f6-176">Allowed values</span></span> | <span data-ttu-id="2e1f6-177">必要</span><span class="sxs-lookup"><span data-stu-id="2e1f6-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2e1f6-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="2e1f6-178">sqlReaderQuery</span></span> |<span data-ttu-id="2e1f6-179">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="2e1f6-180">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-180">SQL query string.</span></span> <span data-ttu-id="2e1f6-181">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="2e1f6-182">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-182">No</span></span> |
| <span data-ttu-id="2e1f6-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="2e1f6-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="2e1f6-184">名稱的 hello 預存程序會從 hello 來源資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="2e1f6-185">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-185">Name of hello stored procedure.</span></span> <span data-ttu-id="2e1f6-186">hello 最後一個 SQL 陳述式必須在 hello 預存程序中的 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="2e1f6-187">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-187">No</span></span> |
| <span data-ttu-id="2e1f6-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="2e1f6-188">storedProcedureParameters</span></span> |<span data-ttu-id="2e1f6-189">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="2e1f6-190">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-190">Name/value pairs.</span></span> <span data-ttu-id="2e1f6-191">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="2e1f6-192">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-192">No</span></span> |

<span data-ttu-id="2e1f6-193">如果 hello **sqlReaderQuery**指定 hello SqlDWSource，hello 複製活動與 hello Azure SQL 資料倉儲來源 tooget hello 資料執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="2e1f6-194">或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="2e1f6-195">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 資料集 JSON hello 結構區段中定義的資料行是使用的 toobuild 針對 hello Azure SQL 資料倉儲查詢 toorun。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2e1f6-196">範例：`select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="2e1f6-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="2e1f6-197">如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="2e1f6-198">SqlDWSource 範例</span><span class="sxs-lookup"><span data-stu-id="2e1f6-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="2e1f6-199">**hello 預存程序定義：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-199">**hello stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a><span data-ttu-id="2e1f6-200">管線</span><span class="sxs-lookup"><span data-stu-id="2e1f6-200">SqlDWSink</span></span>
<span data-ttu-id="2e1f6-201">**SqlDWSink**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="2e1f6-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="2e1f6-202">屬性</span><span class="sxs-lookup"><span data-stu-id="2e1f6-202">Property</span></span> | <span data-ttu-id="2e1f6-203">說明</span><span class="sxs-lookup"><span data-stu-id="2e1f6-203">Description</span></span> | <span data-ttu-id="2e1f6-204">允許的值</span><span class="sxs-lookup"><span data-stu-id="2e1f6-204">Allowed values</span></span> | <span data-ttu-id="2e1f6-205">必要</span><span class="sxs-lookup"><span data-stu-id="2e1f6-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2e1f6-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="2e1f6-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="2e1f6-207">複製活動 tooexecute 查詢指定的特定配量的資料清除。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="2e1f6-208">如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy)一節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="2e1f6-209">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-209">A query statement.</span></span> |<span data-ttu-id="2e1f6-210">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-210">No</span></span> |
| <span data-ttu-id="2e1f6-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="2e1f6-211">allowPolyBase</span></span> |<span data-ttu-id="2e1f6-212">指出是否 toouse PolyBase （如果適用的話），而不是 BULKINSERT 機制。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="2e1f6-213">**使用 PolyBase 是建議的方式 tooload 資料到 SQL 資料倉儲的 hello。**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="2e1f6-214">請參閱[使用 PolyBase tooload 資料到 Azure SQL 資料倉儲](#use-polybase-to-load-data-into-azure-sql-data-warehouse)條件約束和詳細資料 > 一節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="2e1f6-215">True</span><span class="sxs-lookup"><span data-stu-id="2e1f6-215">True</span></span> <br/><span data-ttu-id="2e1f6-216">FALSE (預設值)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-216">False (default)</span></span> |<span data-ttu-id="2e1f6-217">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-217">No</span></span> |
| <span data-ttu-id="2e1f6-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="2e1f6-218">polyBaseSettings</span></span> |<span data-ttu-id="2e1f6-219">一組屬性，可指定當 hello **allowPolybase**屬性設定太**true**。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="2e1f6-220">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-220">No</span></span> |
| <span data-ttu-id="2e1f6-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="2e1f6-221">rejectValue</span></span> |<span data-ttu-id="2e1f6-222">指定 hello 數目或百分比的 hello 查詢失敗前，可能會拒絕的資料列。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="2e1f6-223">深入了解 hello PolyBase 拒絕之選項的 hello**引數**區段[CREATE EXTERNAL TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935021.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="2e1f6-224">0 (預設值)、1、2、…</span><span class="sxs-lookup"><span data-stu-id="2e1f6-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="2e1f6-225">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-225">No</span></span> |
| <span data-ttu-id="2e1f6-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="2e1f6-226">rejectType</span></span> |<span data-ttu-id="2e1f6-227">指定是否要將 hello rejectValue 選項指定為常值或百分比。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="2e1f6-228">值 (預設值)、百分比</span><span class="sxs-lookup"><span data-stu-id="2e1f6-228">Value (default), Percentage</span></span> |<span data-ttu-id="2e1f6-229">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-229">No</span></span> |
| <span data-ttu-id="2e1f6-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="2e1f6-230">rejectSampleValue</span></span> |<span data-ttu-id="2e1f6-231">決定 hello 數量的資料列 tooretrieve hello PolyBase 重新計算 hello 百分比的已拒絕的資料列之前。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="2e1f6-232">1、2、…</span><span class="sxs-lookup"><span data-stu-id="2e1f6-232">1, 2, …</span></span> |<span data-ttu-id="2e1f6-233">是，如果 **rejectType** 是 **percentage**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="2e1f6-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="2e1f6-234">useTypeDefault</span></span> |<span data-ttu-id="2e1f6-235">指定如何 toohandle 遺漏值中的分隔的文字檔案 PolyBase hello 文字檔案中擷取的資料時。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="2e1f6-236">深入了解來自 hello 引數 > 一節中的這個屬性[CREATE EXTERNAL FILE FORMAT (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935026.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="2e1f6-237">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-237">True, False (default)</span></span> |<span data-ttu-id="2e1f6-238">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-238">No</span></span> |
| <span data-ttu-id="2e1f6-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="2e1f6-239">writeBatchSize</span></span> |<span data-ttu-id="2e1f6-240">用戶端 hello 緩衝區的大小達到叫用 writeBatchSize 時，將資料插入 hello SQL 資料表</span><span class="sxs-lookup"><span data-stu-id="2e1f6-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="2e1f6-241">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-241">Integer (number of rows)</span></span> |<span data-ttu-id="2e1f6-242">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-242">No (default: 10000)</span></span> |
| <span data-ttu-id="2e1f6-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="2e1f6-243">writeBatchTimeout</span></span> |<span data-ttu-id="2e1f6-244">在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="2e1f6-245">時間範圍</span><span class="sxs-lookup"><span data-stu-id="2e1f6-245">timespan</span></span><br/><br/> <span data-ttu-id="2e1f6-246">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="2e1f6-247">否</span><span class="sxs-lookup"><span data-stu-id="2e1f6-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="2e1f6-248">SqlDWSink 範例</span><span class="sxs-lookup"><span data-stu-id="2e1f6-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="2e1f6-249">使用 PolyBase tooload 資料到 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="2e1f6-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="2e1f6-250">使用 [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) 是以高輸送量將大量資料載入 Azure SQL 資料倉儲的有效方法。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="2e1f6-251">您可以看到 hello 輸送量較大提高而不是 hello 預設 BULKINSERT 機制使用 PolyBase。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="2e1f6-252">請參閱[複製效能參考編號](data-factory-copy-activity-performance.md#performance-reference)了解詳細的比較。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="2e1f6-253">如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="2e1f6-254">如果您的來源資料位於**Azure Blob 或 Azure Data Lake Store**，和 hello 格式相容，使用 PolyBase，您可以直接複製的 tooAzure 使用 PolyBase 的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="2e1f6-255">請參閱**[使用 PolyBase 直接複製](#direct-copy-using-polybase)**了解詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="2e1f6-256">如果您的來源資料存放區和格式不原本支援 PolyBase，您可以使用 hello **[接移的複本，使用 PolyBase](#staged-copy-using-polybase)** 改用功能。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="2e1f6-257">它也提供更佳的輸送量會自動將 hello 資料轉換成 PolyBase 相容的格式，並將 hello 資料儲存在 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="2e1f6-258">然後，它會將資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="2e1f6-259">設定 hello`allowPolyBase`屬性太**true** hello 遵循範例中的 Azure Data Factory toouse PolyBase toocopy 資料到 Azure SQL 資料倉儲中所示。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2e1f6-260">當您設定 allowPolyBase tootrue 時，您可以指定 PolyBase 特定屬性使用 hello`polyBaseSettings`屬性群組。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="2e1f6-261">請參閱 hello [SqlDWSink](#SqlDWSink)如需詳細資訊，您可以使用 polyBaseSettings 屬性 > 一節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="2e1f6-262">使用 PolyBase 直接複製</span><span class="sxs-lookup"><span data-stu-id="2e1f6-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="2e1f6-263">SQL 資料倉儲 PolyBase 直接支援 Azure Blob 和 Azure Data Lake Store (使用服務主體) 做為來源與特定檔案格式需求。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="2e1f6-264">如果您的來源資料符合本節所述的 hello 準則，您可以直接從來源資料存放區 tooAzure 使用 PolyBase 的 SQL 資料倉儲中複製。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="2e1f6-265">否則，您可以使用 [使用 PolyBase 分段複製](#staged-copy-using-polybase)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="2e1f6-266">從資料倉儲的資料湖存放區 tooSQL toocopy 資料有效，進一步了解從[Azure Data Factory 可讓它使用 SQL 資料倉儲中的資料湖存放區時，即使資料更容易及方便 toouncover insights](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="2e1f6-267">如果不符合 hello 需求，Azure Data Factory 會檢查 hello 設定，並自動回復 toohello BULKINSERT hello 資料移動機制。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="2e1f6-268">「來源已連結服務」的類型為：AzureStorage 或具備服務主題驗證的 AzureDataLakeStore。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="2e1f6-269">hello**輸入資料集**的型別： **AzureBlob**或**AzureDataLakeStore**，和 hello 底下的格式類型`type`屬性是**OrcFormat**，或**TextFormat**以 hello 的設定：</span><span class="sxs-lookup"><span data-stu-id="2e1f6-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="2e1f6-270">`rowDelimiter` 必須是 **\n**。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="2e1f6-271">`nullValue`設定得**空字串**("")，或`treatEmptyAsNull`設定得**true**。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="2e1f6-272">`encodingName`設定得**utf-8**，也就是**預設**值。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="2e1f6-273">未指定 `escapeChar`、`quoteChar`、`firstRowAsHeader` 和 `skipLineCount`。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="2e1f6-274">`compression` 可以是「無壓縮」、**GZip** 或 **Deflate**。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="2e1f6-275">沒有任何`skipHeaderLineCount`底下**BlobSource**或**AzureDataLakeStore** hello 管線中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="2e1f6-276">沒有任何`sliceIdentifierColumnName`底下**SqlDWSink** hello 管線中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="2e1f6-277">(PolyBase 保證所有資料都已更新，或在單一執行未更新任何項目。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="2e1f6-278">tooachieve**重複性**，您可以使用`sqlWriterCleanupScript`)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="2e1f6-279">沒有任何`columnMapping`用於複製活動中相關聯的 hello。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="2e1f6-280">使用 PolyBase 分段複製</span><span class="sxs-lookup"><span data-stu-id="2e1f6-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="2e1f6-281">當您的來源資料不符合 hello 上一節中導入的 hello 準則時，您可以啟用透過暫時臨時 Azure Blob 儲存體 （不能是進階儲存體） 複製資料。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="2e1f6-282">在此情況下，Azure Data Factory 自動 hello 資料 toomeet 資料格式需求 PolyBase，然後再使用 PolyBase tooload 資料到 SQL 資料倉儲上執行轉換，並在上次清除暫存資料從 hello Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="2e1f6-283">如需透過暫存 Azure Blob 複製資料通常如何運作的詳細資訊，請參閱 [分段複製](data-factory-copy-activity-performance.md#staged-copy) 。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="2e1f6-284">當複製資料的內部資料儲存到 Azure SQL 資料倉儲使用 PolyBase，而且準備後，如果您的資料管理閘道器版本低於 2.4，JRE (Java Runtime Environment) 需要您的閘道機器的來源資料是使用的 tootransform成適當格式。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="2e1f6-285">建議您升級閘道 toohello 的最新 tooavoid 這類相依性。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="2e1f6-286">此功能 toouse，建立[Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)參考 toohello 具有 hello 過渡版的 blob 儲存體的 Azure 儲存體帳戶，然後指定 hello`enableStaging`和`stagingSettings`hello 複製活動的屬性hello，下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="2e1f6-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="2e1f6-287">使用 PolyBase 時的最佳作法</span><span class="sxs-lookup"><span data-stu-id="2e1f6-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="2e1f6-288">hello 下列各節提供額外的最佳作法 toohello 中提及的[Azure SQL 資料倉儲的最佳作法](../sql-data-warehouse/sql-data-warehouse-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="2e1f6-289">必要的資料庫權限</span><span class="sxs-lookup"><span data-stu-id="2e1f6-289">Required database permission</span></span>
<span data-ttu-id="2e1f6-290">它 toouse PolyBase，需要 hello 使用者正在使用的 tooload 資料到 SQL 資料倉儲具有 hello [「 控制 」 權限](https://msdn.microsoft.com/library/ms191291.aspx)hello 目標資料庫上。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="2e1f6-291">其中一種方式是 tooadd 的 tooachieve"db_owner 」 角色的成員身分的使用者。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="2e1f6-292">深入了解如何 toodo，依照[本節](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="2e1f6-293">資料列大小和資料類型限制</span><span class="sxs-lookup"><span data-stu-id="2e1f6-293">Row size and data type limitation</span></span>
<span data-ttu-id="2e1f6-294">Polybase 載入受到 tooloading 資料列都小於**1MB**而且無法載入 tooVARCHR(MAX)，nvarchar （max） 或 varbinary （max）。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="2e1f6-295">請參閱太[這裡](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="2e1f6-296">如果您有來源資料與資料列的大小大於 1 MB，您可能為每一個函數 hello 最大資料列大小未超過 hello 限制的數個小型的垂直想 toosplit hello 來源資料表。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="2e1f6-297">使用 PolyBase 和 Azure SQL 資料倉儲中合併在一起，可以接著載入 hello 較小的資料表。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="2e1f6-298">SQL 資料倉儲資源類別</span><span class="sxs-lookup"><span data-stu-id="2e1f6-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="2e1f6-299">tooachieve 最佳可能輸送量，請考慮 tooassign 較大資源類別 toohello 使用者正在使用 tooload 資料到透過 PolyBase 的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="2e1f6-300">深入了解如何 toodo，依照[變更使用者資源類別範例](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="2e1f6-301">Azure SQL 資料倉儲中的 tableName</span><span class="sxs-lookup"><span data-stu-id="2e1f6-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="2e1f6-302">hello 下表提供的範例如何 toospecify hello **tableName**中資料集的結構描述和資料表名稱的各種組合的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="2e1f6-303">DB 結構描述</span><span class="sxs-lookup"><span data-stu-id="2e1f6-303">DB Schema</span></span> | <span data-ttu-id="2e1f6-304">資料表名稱</span><span class="sxs-lookup"><span data-stu-id="2e1f6-304">Table name</span></span> | <span data-ttu-id="2e1f6-305">tableName JSON 屬性</span><span class="sxs-lookup"><span data-stu-id="2e1f6-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e1f6-306">dbo</span><span class="sxs-lookup"><span data-stu-id="2e1f6-306">dbo</span></span> |<span data-ttu-id="2e1f6-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="2e1f6-307">MyTable</span></span> |<span data-ttu-id="2e1f6-308">MyTable 或 dbo.MyTable 或 [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="2e1f6-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="2e1f6-309">dbo1</span></span> |<span data-ttu-id="2e1f6-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="2e1f6-310">MyTable</span></span> |<span data-ttu-id="2e1f6-311">dbo1.MyTable 或 [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="2e1f6-312">dbo</span><span class="sxs-lookup"><span data-stu-id="2e1f6-312">dbo</span></span> |<span data-ttu-id="2e1f6-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="2e1f6-313">My.Table</span></span> |<span data-ttu-id="2e1f6-314">[My.Table] 或 [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="2e1f6-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="2e1f6-315">dbo1</span></span> |<span data-ttu-id="2e1f6-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="2e1f6-316">My.Table</span></span> |<span data-ttu-id="2e1f6-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="2e1f6-318">如果您看到下列錯誤 hello，它可能與您指定 hello tableName 屬性 hello 值的問題。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="2e1f6-319">請參閱 hello 表 hello hello tableName JSON 屬性的正確方式 toospecify 值。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="2e1f6-320">包含預設值的資料行</span><span class="sxs-lookup"><span data-stu-id="2e1f6-320">Columns with default values</span></span>
<span data-ttu-id="2e1f6-321">PolyBase Data Factory 中的功能只接受目前 hello 與 hello 目標資料表的資料行數目相同。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="2e1f6-322">假設您有內含四個資料行的資料表，且其中一個資料行已使用預設值進行定義。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="2e1f6-323">hello 輸入的資料應仍包含四個資料行。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="2e1f6-324">提供 3 個資料行的輸入資料集，會產生錯誤類似 toohello 下列訊息：</span><span class="sxs-lookup"><span data-stu-id="2e1f6-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="2e1f6-325">NULL 值是一種特殊形式的預設值。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="2e1f6-326">如果 hello 資料行是可為 null，hello 輸入中的資料 （blob) 針對該資料行可能是空白 （無法遺漏 hello 輸入資料集）。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="2e1f6-327">PolyBase hello Azure SQL 資料倉儲中將它們都是 NULL。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="2e1f6-328">自動建立資料表</span><span class="sxs-lookup"><span data-stu-id="2e1f6-328">Auto table creation</span></span>
<span data-ttu-id="2e1f6-329">如果您使用複製精靈 toocopy 資料從 SQL Server 或 Azure SQL Database tooAzure SQL 資料倉儲與 hello 資料表對應 toohello 來源資料表不存在 hello 目的地存放區中，資料處理站可以在自動建立 hello 資料表 hello使用 hello 來源資料表的結構描述的資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="2e1f6-330">Data Factory 建立 hello 目的地存放區中的 hello 資料表相同的 hello 與資料表 hello 來源資料存放區中的名稱。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="2e1f6-331">hello 資料行的資料類型會選擇根據 hello 下列型別對應。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="2e1f6-332">如有需要它會執行類型轉換 toofix 來源和目的地存放區之間任何不相容。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="2e1f6-333">它也會使用循環配置資源資料表散發。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="2e1f6-334">來源 SQL Database 資料行類型</span><span class="sxs-lookup"><span data-stu-id="2e1f6-334">Source SQL Database column type</span></span> | <span data-ttu-id="2e1f6-335">目的地 SQL DW 資料行類型 (大小限制)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="2e1f6-336">int</span><span class="sxs-lookup"><span data-stu-id="2e1f6-336">Int</span></span> | <span data-ttu-id="2e1f6-337">int</span><span class="sxs-lookup"><span data-stu-id="2e1f6-337">Int</span></span> |
| <span data-ttu-id="2e1f6-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="2e1f6-338">BigInt</span></span> | <span data-ttu-id="2e1f6-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="2e1f6-339">BigInt</span></span> |
| <span data-ttu-id="2e1f6-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="2e1f6-340">SmallInt</span></span> | <span data-ttu-id="2e1f6-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="2e1f6-341">SmallInt</span></span> |
| <span data-ttu-id="2e1f6-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="2e1f6-342">TinyInt</span></span> | <span data-ttu-id="2e1f6-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="2e1f6-343">TinyInt</span></span> |
| <span data-ttu-id="2e1f6-344">Bit</span><span class="sxs-lookup"><span data-stu-id="2e1f6-344">Bit</span></span> | <span data-ttu-id="2e1f6-345">Bit</span><span class="sxs-lookup"><span data-stu-id="2e1f6-345">Bit</span></span> |
| <span data-ttu-id="2e1f6-346">十進位</span><span class="sxs-lookup"><span data-stu-id="2e1f6-346">Decimal</span></span> | <span data-ttu-id="2e1f6-347">十進位</span><span class="sxs-lookup"><span data-stu-id="2e1f6-347">Decimal</span></span> |
| <span data-ttu-id="2e1f6-348">數值</span><span class="sxs-lookup"><span data-stu-id="2e1f6-348">Numeric</span></span> | <span data-ttu-id="2e1f6-349">十進位</span><span class="sxs-lookup"><span data-stu-id="2e1f6-349">Decimal</span></span> |
| <span data-ttu-id="2e1f6-350">Float</span><span class="sxs-lookup"><span data-stu-id="2e1f6-350">Float</span></span> | <span data-ttu-id="2e1f6-351">Float</span><span class="sxs-lookup"><span data-stu-id="2e1f6-351">Float</span></span> |
| <span data-ttu-id="2e1f6-352">Money</span><span class="sxs-lookup"><span data-stu-id="2e1f6-352">Money</span></span> | <span data-ttu-id="2e1f6-353">Money</span><span class="sxs-lookup"><span data-stu-id="2e1f6-353">Money</span></span> |
| <span data-ttu-id="2e1f6-354">Real</span><span class="sxs-lookup"><span data-stu-id="2e1f6-354">Real</span></span> | <span data-ttu-id="2e1f6-355">Real</span><span class="sxs-lookup"><span data-stu-id="2e1f6-355">Real</span></span> |
| <span data-ttu-id="2e1f6-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="2e1f6-356">SmallMoney</span></span> | <span data-ttu-id="2e1f6-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="2e1f6-357">SmallMoney</span></span> |
| <span data-ttu-id="2e1f6-358">Binary</span><span class="sxs-lookup"><span data-stu-id="2e1f6-358">Binary</span></span> | <span data-ttu-id="2e1f6-359">Binary</span><span class="sxs-lookup"><span data-stu-id="2e1f6-359">Binary</span></span> |
| <span data-ttu-id="2e1f6-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="2e1f6-360">Varbinary</span></span> | <span data-ttu-id="2e1f6-361">Varbinary （向上 too8000)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="2e1f6-362">Date</span><span class="sxs-lookup"><span data-stu-id="2e1f6-362">Date</span></span> | <span data-ttu-id="2e1f6-363">日期</span><span class="sxs-lookup"><span data-stu-id="2e1f6-363">Date</span></span> |
| <span data-ttu-id="2e1f6-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-364">DateTime</span></span> | <span data-ttu-id="2e1f6-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-365">DateTime</span></span> |
| <span data-ttu-id="2e1f6-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="2e1f6-366">DateTime2</span></span> | <span data-ttu-id="2e1f6-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="2e1f6-367">DateTime2</span></span> |
| <span data-ttu-id="2e1f6-368">時間</span><span class="sxs-lookup"><span data-stu-id="2e1f6-368">Time</span></span> | <span data-ttu-id="2e1f6-369">時間</span><span class="sxs-lookup"><span data-stu-id="2e1f6-369">Time</span></span> |
| <span data-ttu-id="2e1f6-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="2e1f6-370">DateTimeOffset</span></span> | <span data-ttu-id="2e1f6-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="2e1f6-371">DateTimeOffset</span></span> |
| <span data-ttu-id="2e1f6-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-372">SmallDateTime</span></span> | <span data-ttu-id="2e1f6-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-373">SmallDateTime</span></span> |
| <span data-ttu-id="2e1f6-374">文字</span><span class="sxs-lookup"><span data-stu-id="2e1f6-374">Text</span></span> | <span data-ttu-id="2e1f6-375">Varchar （向上 too8000)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="2e1f6-376">NText</span><span class="sxs-lookup"><span data-stu-id="2e1f6-376">NText</span></span> | <span data-ttu-id="2e1f6-377">NVarChar （向上 too4000)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="2e1f6-378">映像</span><span class="sxs-lookup"><span data-stu-id="2e1f6-378">Image</span></span> | <span data-ttu-id="2e1f6-379">VarBinary （向上 too8000)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="2e1f6-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="2e1f6-380">UniqueIdentifier</span></span> | <span data-ttu-id="2e1f6-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="2e1f6-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="2e1f6-382">Char</span><span class="sxs-lookup"><span data-stu-id="2e1f6-382">Char</span></span> | <span data-ttu-id="2e1f6-383">Char</span><span class="sxs-lookup"><span data-stu-id="2e1f6-383">Char</span></span> |
| <span data-ttu-id="2e1f6-384">NChar</span><span class="sxs-lookup"><span data-stu-id="2e1f6-384">NChar</span></span> | <span data-ttu-id="2e1f6-385">NChar</span><span class="sxs-lookup"><span data-stu-id="2e1f6-385">NChar</span></span> |
| <span data-ttu-id="2e1f6-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="2e1f6-386">VarChar</span></span> | <span data-ttu-id="2e1f6-387">VarChar （向上 too8000)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="2e1f6-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="2e1f6-388">NVarChar</span></span> | <span data-ttu-id="2e1f6-389">NVarChar （向上 too4000)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="2e1f6-390">xml</span><span class="sxs-lookup"><span data-stu-id="2e1f6-390">Xml</span></span> | <span data-ttu-id="2e1f6-391">Varchar （向上 too8000)</span><span class="sxs-lookup"><span data-stu-id="2e1f6-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="2e1f6-392">Azure SQL 資料倉儲的類型對應</span><span class="sxs-lookup"><span data-stu-id="2e1f6-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="2e1f6-393">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：</span><span class="sxs-lookup"><span data-stu-id="2e1f6-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="2e1f6-394">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="2e1f6-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="2e1f6-395">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="2e1f6-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="2e1f6-396">當您從 Azure SQL 資料倉儲 & 太移動資料，hello 下列的對應會使用從 SQL 型別 too.NET 類型，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="2e1f6-397">hello 對應是相同 hello [ADO.NET 的 SQL Server 資料類型對應](https://msdn.microsoft.com/library/cc716729.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="2e1f6-398">SQL Server Database Engine 類型</span><span class="sxs-lookup"><span data-stu-id="2e1f6-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="2e1f6-399">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="2e1f6-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="2e1f6-400">bigint</span><span class="sxs-lookup"><span data-stu-id="2e1f6-400">bigint</span></span> |<span data-ttu-id="2e1f6-401">Int64</span><span class="sxs-lookup"><span data-stu-id="2e1f6-401">Int64</span></span> |
| <span data-ttu-id="2e1f6-402">binary</span><span class="sxs-lookup"><span data-stu-id="2e1f6-402">binary</span></span> |<span data-ttu-id="2e1f6-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-403">Byte[]</span></span> |
| <span data-ttu-id="2e1f6-404">bit</span><span class="sxs-lookup"><span data-stu-id="2e1f6-404">bit</span></span> |<span data-ttu-id="2e1f6-405">Boolean</span><span class="sxs-lookup"><span data-stu-id="2e1f6-405">Boolean</span></span> |
| <span data-ttu-id="2e1f6-406">char</span><span class="sxs-lookup"><span data-stu-id="2e1f6-406">char</span></span> |<span data-ttu-id="2e1f6-407">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-407">String, Char[]</span></span> |
| <span data-ttu-id="2e1f6-408">日期</span><span class="sxs-lookup"><span data-stu-id="2e1f6-408">date</span></span> |<span data-ttu-id="2e1f6-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-409">DateTime</span></span> |
| <span data-ttu-id="2e1f6-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-410">Datetime</span></span> |<span data-ttu-id="2e1f6-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-411">DateTime</span></span> |
| <span data-ttu-id="2e1f6-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="2e1f6-412">datetime2</span></span> |<span data-ttu-id="2e1f6-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-413">DateTime</span></span> |
| <span data-ttu-id="2e1f6-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="2e1f6-414">Datetimeoffset</span></span> |<span data-ttu-id="2e1f6-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="2e1f6-415">DateTimeOffset</span></span> |
| <span data-ttu-id="2e1f6-416">十進位</span><span class="sxs-lookup"><span data-stu-id="2e1f6-416">Decimal</span></span> |<span data-ttu-id="2e1f6-417">十進位</span><span class="sxs-lookup"><span data-stu-id="2e1f6-417">Decimal</span></span> |
| <span data-ttu-id="2e1f6-418">FILESTREAM 屬性 (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="2e1f6-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="2e1f6-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-419">Byte[]</span></span> |
| <span data-ttu-id="2e1f6-420">Float</span><span class="sxs-lookup"><span data-stu-id="2e1f6-420">Float</span></span> |<span data-ttu-id="2e1f6-421">兩倍</span><span class="sxs-lookup"><span data-stu-id="2e1f6-421">Double</span></span> |
| <span data-ttu-id="2e1f6-422">image</span><span class="sxs-lookup"><span data-stu-id="2e1f6-422">image</span></span> |<span data-ttu-id="2e1f6-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-423">Byte[]</span></span> |
| <span data-ttu-id="2e1f6-424">int</span><span class="sxs-lookup"><span data-stu-id="2e1f6-424">int</span></span> |<span data-ttu-id="2e1f6-425">Int32</span><span class="sxs-lookup"><span data-stu-id="2e1f6-425">Int32</span></span> |
| <span data-ttu-id="2e1f6-426">money</span><span class="sxs-lookup"><span data-stu-id="2e1f6-426">money</span></span> |<span data-ttu-id="2e1f6-427">十進位</span><span class="sxs-lookup"><span data-stu-id="2e1f6-427">Decimal</span></span> |
| <span data-ttu-id="2e1f6-428">nchar</span><span class="sxs-lookup"><span data-stu-id="2e1f6-428">nchar</span></span> |<span data-ttu-id="2e1f6-429">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-429">String, Char[]</span></span> |
| <span data-ttu-id="2e1f6-430">ntext</span><span class="sxs-lookup"><span data-stu-id="2e1f6-430">ntext</span></span> |<span data-ttu-id="2e1f6-431">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-431">String, Char[]</span></span> |
| <span data-ttu-id="2e1f6-432">numeric</span><span class="sxs-lookup"><span data-stu-id="2e1f6-432">numeric</span></span> |<span data-ttu-id="2e1f6-433">十進位</span><span class="sxs-lookup"><span data-stu-id="2e1f6-433">Decimal</span></span> |
| <span data-ttu-id="2e1f6-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="2e1f6-434">nvarchar</span></span> |<span data-ttu-id="2e1f6-435">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-435">String, Char[]</span></span> |
| <span data-ttu-id="2e1f6-436">real</span><span class="sxs-lookup"><span data-stu-id="2e1f6-436">real</span></span> |<span data-ttu-id="2e1f6-437">單一</span><span class="sxs-lookup"><span data-stu-id="2e1f6-437">Single</span></span> |
| <span data-ttu-id="2e1f6-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="2e1f6-438">rowversion</span></span> |<span data-ttu-id="2e1f6-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-439">Byte[]</span></span> |
| <span data-ttu-id="2e1f6-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-440">smalldatetime</span></span> |<span data-ttu-id="2e1f6-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="2e1f6-441">DateTime</span></span> |
| <span data-ttu-id="2e1f6-442">smallint</span><span class="sxs-lookup"><span data-stu-id="2e1f6-442">smallint</span></span> |<span data-ttu-id="2e1f6-443">Int16</span><span class="sxs-lookup"><span data-stu-id="2e1f6-443">Int16</span></span> |
| <span data-ttu-id="2e1f6-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="2e1f6-444">smallmoney</span></span> |<span data-ttu-id="2e1f6-445">十進位</span><span class="sxs-lookup"><span data-stu-id="2e1f6-445">Decimal</span></span> |
| <span data-ttu-id="2e1f6-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="2e1f6-446">sql_variant</span></span> |<span data-ttu-id="2e1f6-447">物件 *</span><span class="sxs-lookup"><span data-stu-id="2e1f6-447">Object *</span></span> |
| <span data-ttu-id="2e1f6-448">文字</span><span class="sxs-lookup"><span data-stu-id="2e1f6-448">text</span></span> |<span data-ttu-id="2e1f6-449">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-449">String, Char[]</span></span> |
| <span data-ttu-id="2e1f6-450">分析</span><span class="sxs-lookup"><span data-stu-id="2e1f6-450">time</span></span> |<span data-ttu-id="2e1f6-451">時間範圍</span><span class="sxs-lookup"><span data-stu-id="2e1f6-451">TimeSpan</span></span> |
| <span data-ttu-id="2e1f6-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="2e1f6-452">timestamp</span></span> |<span data-ttu-id="2e1f6-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-453">Byte[]</span></span> |
| <span data-ttu-id="2e1f6-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="2e1f6-454">tinyint</span></span> |<span data-ttu-id="2e1f6-455">位元組</span><span class="sxs-lookup"><span data-stu-id="2e1f6-455">Byte</span></span> |
| <span data-ttu-id="2e1f6-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="2e1f6-456">uniqueidentifier</span></span> |<span data-ttu-id="2e1f6-457">Guid</span><span class="sxs-lookup"><span data-stu-id="2e1f6-457">Guid</span></span> |
| <span data-ttu-id="2e1f6-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="2e1f6-458">varbinary</span></span> |<span data-ttu-id="2e1f6-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-459">Byte[]</span></span> |
| <span data-ttu-id="2e1f6-460">varchar</span><span class="sxs-lookup"><span data-stu-id="2e1f6-460">varchar</span></span> |<span data-ttu-id="2e1f6-461">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="2e1f6-461">String, Char[]</span></span> |
| <span data-ttu-id="2e1f6-462">xml</span><span class="sxs-lookup"><span data-stu-id="2e1f6-462">xml</span></span> |<span data-ttu-id="2e1f6-463">xml</span><span class="sxs-lookup"><span data-stu-id="2e1f6-463">Xml</span></span> |

<span data-ttu-id="2e1f6-464">您也可以將對應從來源資料集 toocolumns 接收 hello 複製活動定義中的資料集的資料行。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="2e1f6-465">如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="2e1f6-466">從 SQL 資料倉儲中複製資料 tooand JSON 範例</span><span class="sxs-lookup"><span data-stu-id="2e1f6-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="2e1f6-467">hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2e1f6-468">它們會顯示如何從 Azure SQL 資料倉儲和 Azure Blob 儲存體 toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="2e1f6-469">不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="2e1f6-470">範例： 將資料複製 Azure SQL 資料倉儲 tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="2e1f6-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="2e1f6-471">hello 範例會定義下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e1f6-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="2e1f6-472">[AzureSqlDW](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="2e1f6-473">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2e1f6-474">[AzureSqlDWTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="2e1f6-475">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2e1f6-476">具有使用 [SqlDWSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2e1f6-477">hello 範例將時間序列 （每小時、 每日等等） 資料從 Azure SQL 資料倉儲資料庫 tooa blob 中的資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="2e1f6-478">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="2e1f6-479">**Azure SQL 資料倉儲連結服務：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="2e1f6-480">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="2e1f6-481">**Azure SQL 資料倉儲輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="2e1f6-482">hello 範例假設您已建立資料表"MyTable"Azure SQL 資料倉儲中，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="2e1f6-483">設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="2e1f6-484">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2e1f6-485">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2e1f6-486">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2e1f6-487">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="2e1f6-488">**管線中使用 SqlDWSource 和 BlobSink 的複製活動：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="2e1f6-489">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2e1f6-490">在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlDWSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="2e1f6-491">指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> <span data-ttu-id="2e1f6-492">在 hello 範例**sqlReaderQuery** hello SqlDWSource 指定。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="2e1f6-493">hello 複製活動會針對 hello Azure SQL 資料倉儲來源 tooget hello 資料執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="2e1f6-494">或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="2e1f6-495">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 資料集 JSON hello 結構區段中定義的資料行是使用的 toobuild 查詢 (選取 column1、 column2 從 mytable) toorun 針對 hello Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2e1f6-496">如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="2e1f6-497">範例： 將資料從 Azure Blob tooAzure SQL 資料倉儲中複製</span><span class="sxs-lookup"><span data-stu-id="2e1f6-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="2e1f6-498">hello 範例會定義下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e1f6-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="2e1f6-499">[AzureSqlDW](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="2e1f6-500">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2e1f6-501">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="2e1f6-502">[AzureSqlDWTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="2e1f6-503">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [SqlDWSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="2e1f6-504">hello 範例時間序列資料 （每小時、 每天、 等等） 從 Azure blob tooa 資料表複製 Azure SQL 資料倉儲資料庫中的每個小時。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="2e1f6-505">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="2e1f6-506">**Azure SQL 資料倉儲連結服務：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="2e1f6-507">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="2e1f6-508">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="2e1f6-509">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2e1f6-510">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2e1f6-511">年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="2e1f6-512">"external":"true"的設定會在這個資料表是外部 toohello 資料處理站，而不產生 hello data factory 中的活動時通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="2e1f6-513">**Azure SQL 資料倉儲輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="2e1f6-514">hello 範例複製 Azure SQL 資料倉儲中名為"MyTable"的資料 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2e1f6-515">在具有 Azure SQL 資料倉儲中建立 hello 資料表如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="2e1f6-516">新的資料列會加入 toohello 資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-516">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="2e1f6-517">**具有 BlobSource 和 SqlDWSink 的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="2e1f6-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="2e1f6-518">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2e1f6-519">在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlDWSink**。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="2e1f6-520">如需逐步解說，請參閱 hello，請參閱[Azure SQL 資料倉儲將在 15 分鐘與 Azure Data Factory 載入 1TB](data-factory-load-sql-data-warehouse.md)和[載入資料有 Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) hello Azure SQL 資料倉儲中的發行項文件。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2e1f6-521">效能和微調</span><span class="sxs-lookup"><span data-stu-id="2e1f6-521">Performance and Tuning</span></span>
<span data-ttu-id="2e1f6-522">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="2e1f6-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
