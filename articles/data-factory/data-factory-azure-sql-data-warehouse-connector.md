---
title: "從 Azure SQL 資料倉儲來回複製資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Azure SQL 資料倉儲來回複製資料"
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
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="b16b6-103">使用 Azure Data Factory 從 Azure SQL 資料倉儲來回複製資料</span><span class="sxs-lookup"><span data-stu-id="b16b6-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="b16b6-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，將資料移進/移出「Azure SQL 資料倉儲」。</span><span class="sxs-lookup"><span data-stu-id="b16b6-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b16b6-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="b16b6-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="b16b6-106">若要達到最佳效能，請使用 PolyBase 將資料載入 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b16b6-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b16b6-107">如需詳細資訊，請參閱 [使用 PolyBase 將資料載入 Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) 。</span><span class="sxs-lookup"><span data-stu-id="b16b6-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="b16b6-108">如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="b16b6-109">支援的案例</span><span class="sxs-lookup"><span data-stu-id="b16b6-109">Supported scenarios</span></span>
<span data-ttu-id="b16b6-110">您可以**從 Azure SQL 資料倉儲**將資料複製到下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="b16b6-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="b16b6-111">您可以從下列資料存放區將資料複製**到 Azure SQL 資料倉儲**：</span><span class="sxs-lookup"><span data-stu-id="b16b6-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="b16b6-112">從 SQL Server 或 Azure SQL Database 中將資料複製到 Azure SQL 資料倉儲時，如果目的地存放區中沒有資料表，Data Factory 可以使用來源資料存放區中的資料表結構描述，在 SQL 資料倉儲中自動建立資料表。</span><span class="sxs-lookup"><span data-stu-id="b16b6-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="b16b6-113">請參閱[自動建立資料表](#auto-table-creation)以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="b16b6-114">支援的驗證類型</span><span class="sxs-lookup"><span data-stu-id="b16b6-114">Supported authentication type</span></span>
<span data-ttu-id="b16b6-115">Azure SQL 資料倉儲連接器支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="b16b6-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b16b6-116">開始使用</span><span class="sxs-lookup"><span data-stu-id="b16b6-116">Getting started</span></span>
<span data-ttu-id="b16b6-117">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出「Azure SQL 資料倉儲」。</span><span class="sxs-lookup"><span data-stu-id="b16b6-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="b16b6-118">要建立將資料複製到 Azure SQL 資料倉儲，或複製 Azure SQL 資料倉儲資料的管線，最簡單的方法是使用複製資料精靈。</span><span class="sxs-lookup"><span data-stu-id="b16b6-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="b16b6-119">請參閱[教學課程︰使用 Data Factory 將資料載入 SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md)以取得使用複製資料精靈建立管線的快速逐步解說。</span><span class="sxs-lookup"><span data-stu-id="b16b6-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="b16b6-120">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b16b6-121">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="b16b6-122">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="b16b6-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="b16b6-123">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-123">Create a **data factory**.</span></span> <span data-ttu-id="b16b6-124">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="b16b6-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="b16b6-125">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="b16b6-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="b16b6-126">例如，如果您將資料從 Azure blob 儲存體複製到 Azure SQL 資料倉儲，您會建立兩個連結服務，將 Azure 儲存體帳戶和 Azure SQL 資料倉儲連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="b16b6-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="b16b6-127">有關 Azure SQL 資料倉儲專屬的連結服務屬性，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="b16b6-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="b16b6-128">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="b16b6-129">在上一個步驟所述的範例中，您會建立資料集來指定 blob 容器和包含輸入資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="b16b6-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="b16b6-130">您還會建立另一個資料集來指定 Azure SQL 資料倉儲中的資料表，以保存從 Blob 儲存體複製的資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="b16b6-131">有關 Azure SQL 資料倉儲專屬的資料集屬性，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="b16b6-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="b16b6-132">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="b16b6-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="b16b6-133">在稍早所述的範例中，您會使用 BlobSource 作為來源，以及使用 SqlDWSink 作為複製活動的接收器。</span><span class="sxs-lookup"><span data-stu-id="b16b6-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="b16b6-134">同樣地，如果您是從 Azure SQL 資料倉儲複製到 Azure Blob 儲存體，則需要在複製活動中使用 SqlDWSource 和 BlobSink。</span><span class="sxs-lookup"><span data-stu-id="b16b6-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="b16b6-135">有關 Azure SQL 資料倉儲專屬的複製活動屬性，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="b16b6-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="b16b6-136">如需有關如何使用資料存放區作為來源或接收器的詳細資訊，請在上一節按一下適用於您的資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="b16b6-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="b16b6-137">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="b16b6-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="b16b6-138">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="b16b6-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="b16b6-139">如需相關範例，其中含有用來將資料複製到「Azure SQL 資料倉儲」(或從「Azure SQL 資料倉儲」複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples-for-copying-data-to-and-from-sql-data-warehouse)一節。</span><span class="sxs-lookup"><span data-stu-id="b16b6-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="b16b6-140">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義「Azure SQL 資料倉儲」特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="b16b6-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b16b6-141">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="b16b6-141">Linked service properties</span></span>
<span data-ttu-id="b16b6-142">下表提供 Azure SQL 資料倉儲連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="b16b6-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="b16b6-143">屬性</span><span class="sxs-lookup"><span data-stu-id="b16b6-143">Property</span></span> | <span data-ttu-id="b16b6-144">說明</span><span class="sxs-lookup"><span data-stu-id="b16b6-144">Description</span></span> | <span data-ttu-id="b16b6-145">必要</span><span class="sxs-lookup"><span data-stu-id="b16b6-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b16b6-146">類型</span><span class="sxs-lookup"><span data-stu-id="b16b6-146">type</span></span> |<span data-ttu-id="b16b6-147">類型屬性必須設為： **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="b16b6-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="b16b6-148">是</span><span class="sxs-lookup"><span data-stu-id="b16b6-148">Yes</span></span> |
| <span data-ttu-id="b16b6-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="b16b6-149">connectionString</span></span> |<span data-ttu-id="b16b6-150">針對 connectionString 屬性指定連線到 Azure SQL 資料倉儲執行個體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="b16b6-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="b16b6-151">僅支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="b16b6-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="b16b6-152">是</span><span class="sxs-lookup"><span data-stu-id="b16b6-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="b16b6-153">設定 [Azure SQL Database 防火牆](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)和資料庫伺服器，以[允許 Azure 服務存取伺服器](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="b16b6-154">此外，如果您要從 Azure 外部 (包括從具有 Data Factory 閘道器的內部部署資料來源) 將資料複製到 Azure SQL 資料倉儲，則必須為傳送資料到 Azure SQL 資料倉儲的機器設定適當的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="b16b6-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="b16b6-155">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="b16b6-155">Dataset properties</span></span>
<span data-ttu-id="b16b6-156">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="b16b6-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b16b6-157">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b16b6-158">每個資料集類型的 typeProperties 區段都不同，可提供資料存放區中資料的位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b16b6-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="b16b6-159">**AzureSqlDWTable** 類型資料集的 **typeProperties** 區段具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b16b6-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="b16b6-160">屬性</span><span class="sxs-lookup"><span data-stu-id="b16b6-160">Property</span></span> | <span data-ttu-id="b16b6-161">說明</span><span class="sxs-lookup"><span data-stu-id="b16b6-161">Description</span></span> | <span data-ttu-id="b16b6-162">必要</span><span class="sxs-lookup"><span data-stu-id="b16b6-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b16b6-163">tableName</span><span class="sxs-lookup"><span data-stu-id="b16b6-163">tableName</span></span> |<span data-ttu-id="b16b6-164">Azure SQL 資料倉儲資料庫中連結服務所參照的資料表名稱或檢視名稱。</span><span class="sxs-lookup"><span data-stu-id="b16b6-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="b16b6-165">是</span><span class="sxs-lookup"><span data-stu-id="b16b6-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="b16b6-166">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="b16b6-166">Copy activity properties</span></span>
<span data-ttu-id="b16b6-167">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="b16b6-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b16b6-168">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="b16b6-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="b16b6-169">複製活動只會採用一個輸入，而且只產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="b16b6-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="b16b6-170">而活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="b16b6-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="b16b6-171">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="b16b6-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="b16b6-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="b16b6-172">SqlDWSource</span></span>
<span data-ttu-id="b16b6-173">如果來源類型為 **SqlDWSource**，則 **typeProperties** 區段可使用下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b16b6-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="b16b6-174">屬性</span><span class="sxs-lookup"><span data-stu-id="b16b6-174">Property</span></span> | <span data-ttu-id="b16b6-175">說明</span><span class="sxs-lookup"><span data-stu-id="b16b6-175">Description</span></span> | <span data-ttu-id="b16b6-176">允許的值</span><span class="sxs-lookup"><span data-stu-id="b16b6-176">Allowed values</span></span> | <span data-ttu-id="b16b6-177">必要</span><span class="sxs-lookup"><span data-stu-id="b16b6-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b16b6-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="b16b6-178">sqlReaderQuery</span></span> |<span data-ttu-id="b16b6-179">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-179">Use the custom query to read data.</span></span> |<span data-ttu-id="b16b6-180">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="b16b6-180">SQL query string.</span></span> <span data-ttu-id="b16b6-181">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="b16b6-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="b16b6-182">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-182">No</span></span> |
| <span data-ttu-id="b16b6-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="b16b6-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="b16b6-184">從來源資料表讀取資料的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="b16b6-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="b16b6-185">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="b16b6-185">Name of the stored procedure.</span></span> <span data-ttu-id="b16b6-186">最後一個 SQL 陳述式必須是預存程序中的 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b16b6-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="b16b6-187">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-187">No</span></span> |
| <span data-ttu-id="b16b6-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="b16b6-188">storedProcedureParameters</span></span> |<span data-ttu-id="b16b6-189">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="b16b6-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="b16b6-190">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="b16b6-190">Name/value pairs.</span></span> <span data-ttu-id="b16b6-191">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="b16b6-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="b16b6-192">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-192">No</span></span> |

<span data-ttu-id="b16b6-193">如果已為 SqlDWSource 指定 **sqlReaderQuery** ，複製活動會針對 Azure SQL 資料倉儲來源執行這項查詢以取得資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="b16b6-194">或者，您可以藉由指定 **sqlReaderStoredProcedureName** 和 **storedProcedureParameters** (如果預存程序接受參數) 來指定預存程序。</span><span class="sxs-lookup"><span data-stu-id="b16b6-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="b16b6-195">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，就會使用資料集 JSON 的結構區段中定義的資料行來建立一個查詢，以對 Azure SQL 資料倉儲執行。</span><span class="sxs-lookup"><span data-stu-id="b16b6-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b16b6-196">範例：`select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="b16b6-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="b16b6-197">如果資料集定義沒有結構，則會從資料表中選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="b16b6-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="b16b6-198">SqlDWSource 範例</span><span class="sxs-lookup"><span data-stu-id="b16b6-198">SqlDWSource example</span></span>

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
<span data-ttu-id="b16b6-199">**預存程序定義：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-199">**The stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="b16b6-200">管線</span><span class="sxs-lookup"><span data-stu-id="b16b6-200">SqlDWSink</span></span>
<span data-ttu-id="b16b6-201">**SqlDWSink** 支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b16b6-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="b16b6-202">屬性</span><span class="sxs-lookup"><span data-stu-id="b16b6-202">Property</span></span> | <span data-ttu-id="b16b6-203">說明</span><span class="sxs-lookup"><span data-stu-id="b16b6-203">Description</span></span> | <span data-ttu-id="b16b6-204">允許的值</span><span class="sxs-lookup"><span data-stu-id="b16b6-204">Allowed values</span></span> | <span data-ttu-id="b16b6-205">必要</span><span class="sxs-lookup"><span data-stu-id="b16b6-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b16b6-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="b16b6-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="b16b6-207">指定要讓「複製活動」執行的查詢，以便清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="b16b6-208">如需詳細資訊，請參閱 [可重複性](#repeatability-during-copy)一節。</span><span class="sxs-lookup"><span data-stu-id="b16b6-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="b16b6-209">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="b16b6-209">A query statement.</span></span> |<span data-ttu-id="b16b6-210">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-210">No</span></span> |
| <span data-ttu-id="b16b6-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="b16b6-211">allowPolyBase</span></span> |<span data-ttu-id="b16b6-212">指出是否使用 PolyBase (適用的話) 而不是使用 BULKINSERT 機制。</span><span class="sxs-lookup"><span data-stu-id="b16b6-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="b16b6-213">建議使用 PolyBase 將資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b16b6-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="b16b6-214">請參閱 [使用 PolyBase 將資料載入 Azure SQL 資料倉儲](#use-polybase-to-load-data-into-azure-sql-data-warehouse) 一節中的條件約束和詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="b16b6-215">True</span><span class="sxs-lookup"><span data-stu-id="b16b6-215">True</span></span> <br/><span data-ttu-id="b16b6-216">FALSE (預設值)</span><span class="sxs-lookup"><span data-stu-id="b16b6-216">False (default)</span></span> |<span data-ttu-id="b16b6-217">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-217">No</span></span> |
| <span data-ttu-id="b16b6-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="b16b6-218">polyBaseSettings</span></span> |<span data-ttu-id="b16b6-219">可以在 **allowPolybase** 屬性設定為 **true** 時指定的一組屬性。</span><span class="sxs-lookup"><span data-stu-id="b16b6-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="b16b6-220">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-220">No</span></span> |
| <span data-ttu-id="b16b6-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="b16b6-221">rejectValue</span></span> |<span data-ttu-id="b16b6-222">指定在查詢失敗前可以拒絕的資料列數目或百分比。</span><span class="sxs-lookup"><span data-stu-id="b16b6-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="b16b6-223">在 **CREATE EXTERNAL TABLE (Transact-SQL)** 主題的 [引數](https://msdn.microsoft.com/library/dn935021.aspx) 一節中，深入了解 PolyBase 的拒絕選項。</span><span class="sxs-lookup"><span data-stu-id="b16b6-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="b16b6-224">0 (預設值)、1、2、…</span><span class="sxs-lookup"><span data-stu-id="b16b6-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="b16b6-225">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-225">No</span></span> |
| <span data-ttu-id="b16b6-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="b16b6-226">rejectType</span></span> |<span data-ttu-id="b16b6-227">指定要將 rejectValue 選項指定為常值或百分比。</span><span class="sxs-lookup"><span data-stu-id="b16b6-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="b16b6-228">值 (預設值)、百分比</span><span class="sxs-lookup"><span data-stu-id="b16b6-228">Value (default), Percentage</span></span> |<span data-ttu-id="b16b6-229">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-229">No</span></span> |
| <span data-ttu-id="b16b6-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="b16b6-230">rejectSampleValue</span></span> |<span data-ttu-id="b16b6-231">決定在 PolyBase 重新計算已拒絕的資料列百分比之前，所要擷取的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="b16b6-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="b16b6-232">1、2、…</span><span class="sxs-lookup"><span data-stu-id="b16b6-232">1, 2, …</span></span> |<span data-ttu-id="b16b6-233">是，如果 **rejectType** 是 **percentage**</span><span class="sxs-lookup"><span data-stu-id="b16b6-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="b16b6-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="b16b6-234">useTypeDefault</span></span> |<span data-ttu-id="b16b6-235">指定當 PolyBase 從文字檔擷取資料時，如何處理分隔符號文字檔中的遺漏值。</span><span class="sxs-lookup"><span data-stu-id="b16b6-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="b16b6-236">從 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx) 的＜引數＞一節深入了解這個屬性。</span><span class="sxs-lookup"><span data-stu-id="b16b6-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="b16b6-237">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="b16b6-237">True, False (default)</span></span> |<span data-ttu-id="b16b6-238">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-238">No</span></span> |
| <span data-ttu-id="b16b6-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="b16b6-239">writeBatchSize</span></span> |<span data-ttu-id="b16b6-240">當緩衝區大小達到 writeBatchSize 時，將資料插入 SQL 資料表中</span><span class="sxs-lookup"><span data-stu-id="b16b6-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="b16b6-241">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="b16b6-241">Integer (number of rows)</span></span> |<span data-ttu-id="b16b6-242">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="b16b6-242">No (default: 10000)</span></span> |
| <span data-ttu-id="b16b6-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="b16b6-243">writeBatchTimeout</span></span> |<span data-ttu-id="b16b6-244">在逾時前等待批次插入作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="b16b6-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="b16b6-245">時間範圍</span><span class="sxs-lookup"><span data-stu-id="b16b6-245">timespan</span></span><br/><br/> <span data-ttu-id="b16b6-246">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="b16b6-247">否</span><span class="sxs-lookup"><span data-stu-id="b16b6-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="b16b6-248">SqlDWSink 範例</span><span class="sxs-lookup"><span data-stu-id="b16b6-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="b16b6-249">使用 PolyBase 將資料載入 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="b16b6-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="b16b6-250">使用 [PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) 是以高輸送量將大量資料載入 Azure SQL 資料倉儲的有效方法。</span><span class="sxs-lookup"><span data-stu-id="b16b6-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="b16b6-251">使用 PolyBase 而不是預設的 BULKINSERT 機制，即可看到輸送量大幅提升。</span><span class="sxs-lookup"><span data-stu-id="b16b6-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="b16b6-252">請參閱[複製效能參考編號](data-factory-copy-activity-performance.md#performance-reference)了解詳細的比較。</span><span class="sxs-lookup"><span data-stu-id="b16b6-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="b16b6-253">如需使用案例的逐步解說，請參閱[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="b16b6-254">如果您的來源資料位在 Azure Blob 或 Azure Data Lake Store，且其格式與 PolyBase 相容，您就可以使用 PolyBase 直接複製到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b16b6-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="b16b6-255">請參閱**[使用 PolyBase 直接複製](#direct-copy-using-polybase)**了解詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="b16b6-256">如果您的來源資料存放區與格式不受 PolyBase 支援，您可以改為使用[使用 PolyBase 分段複製](#staged-copy-using-polybase)功能。</span><span class="sxs-lookup"><span data-stu-id="b16b6-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="b16b6-257">它也能透過將資料自動轉換為 PolyBase 相容的格式，並將資料儲存在 Azure Blob 儲存體中，來提供更佳的輸送量。</span><span class="sxs-lookup"><span data-stu-id="b16b6-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="b16b6-258">然後，它會將資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b16b6-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="b16b6-259">將 `allowPolyBase` 屬性設定為 **true** (如下列範例所示)，以便 Azure Data Factory 使用 PolyBase，將資料複製到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b16b6-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b16b6-260">當您將 allowPolyBase 設定為 true 時，您可以使用 `polyBaseSettings` 屬性群組來指定 PolyBase 特定屬性。</span><span class="sxs-lookup"><span data-stu-id="b16b6-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="b16b6-261">如需您可搭配 polyBaseSettings 使用之屬性的詳細資訊，請參閱 [SqlDWSink](#SqlDWSink) 一節。</span><span class="sxs-lookup"><span data-stu-id="b16b6-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="b16b6-262">使用 PolyBase 直接複製</span><span class="sxs-lookup"><span data-stu-id="b16b6-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="b16b6-263">SQL 資料倉儲 PolyBase 直接支援 Azure Blob 和 Azure Data Lake Store (使用服務主體) 做為來源與特定檔案格式需求。</span><span class="sxs-lookup"><span data-stu-id="b16b6-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="b16b6-264">如果您的來源資料符合本節所述準則，您就可以使用 PolyBase，從來源資料存放區直接複製到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b16b6-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="b16b6-265">否則，您可以使用 [使用 PolyBase 分段複製](#staged-copy-using-polybase)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="b16b6-266">若要有效率地將資料從 Data Lake Store 複製到 SQL 資料倉儲，深入了解 [使用 Data Lake Store 與 SQL 資料倉儲時，Azure Data Factory 能讓您更輕鬆容易發現資料中的重要資訊](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="b16b6-267">如果不符合需求，Azure Data Factory 會檢查設定，並自動切換回適用於資料移動的 BULKINSERT 機制。</span><span class="sxs-lookup"><span data-stu-id="b16b6-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="b16b6-268">「來源已連結服務」的類型為：AzureStorage 或具備服務主題驗證的 AzureDataLakeStore。</span><span class="sxs-lookup"><span data-stu-id="b16b6-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="b16b6-269">「輸入資料集」**的類型為**：**AzureBlob** 或 **AzureDataLakeStore**，而 `type` 屬性底下的格式類型為 **OrcFormat** 或 **TextFormat** 並具備下列組態：</span><span class="sxs-lookup"><span data-stu-id="b16b6-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="b16b6-270">`rowDelimiter` 必須是 **\n**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="b16b6-271">`nullValue` 設定為「空字串」 ("") 或將 `treatEmptyAsNull` 設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="b16b6-272">`encodingName` 設定為 **utf-8**，也就是「預設」值。</span><span class="sxs-lookup"><span data-stu-id="b16b6-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="b16b6-273">未指定 `escapeChar`、`quoteChar`、`firstRowAsHeader` 和 `skipLineCount`。</span><span class="sxs-lookup"><span data-stu-id="b16b6-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="b16b6-274">`compression` 可以是「無壓縮」、**GZip** 或 **Deflate**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="b16b6-275">管線中複製活動的 **BlobSource** 或 **AzureDataLakeStore** 之下沒有 `skipHeaderLineCount` 設定。</span><span class="sxs-lookup"><span data-stu-id="b16b6-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="b16b6-276">管線中複製活動的 **SqlDWSink** 之下沒有 `sliceIdentifierColumnName` 設定。</span><span class="sxs-lookup"><span data-stu-id="b16b6-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="b16b6-277">(PolyBase 保證所有資料都已更新，或在單一執行未更新任何項目。</span><span class="sxs-lookup"><span data-stu-id="b16b6-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="b16b6-278">若要達到「重複性」，您可以使用 `sqlWriterCleanupScript`)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="b16b6-279">目前沒有任何 `columnMapping` 使用於相關聯的複製活動。</span><span class="sxs-lookup"><span data-stu-id="b16b6-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="b16b6-280">使用 PolyBase 分段複製</span><span class="sxs-lookup"><span data-stu-id="b16b6-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="b16b6-281">當來源資料不符合上一節介紹的準則時，您可以啟用透過過渡暫存 Azure Blob 儲存體 (不能是進階儲存體) 複製資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="b16b6-282">在此情況下，Azure Data Factory 會自動執行資料轉換，以符合 PolyBase 的資料格式需求，然後使用 PolyBase 將資料載入到 SQL 資料倉儲，最後從 Blob 儲存體清空您的暫存資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="b16b6-283">如需透過暫存 Azure Blob 複製資料通常如何運作的詳細資訊，請參閱 [分段複製](data-factory-copy-activity-performance.md#staged-copy) 。</span><span class="sxs-lookup"><span data-stu-id="b16b6-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="b16b6-284">當您使用 PolyBase 和分段，將資料從內部部署資料存放區複製到 Azure SQL 資料倉儲時，如果您的「資料管理閘道」版本低於 2.4，就必須在閘道電腦上安裝 JRE (Java Runtime Environment)，以便用來將來源資料轉換為適當格式。</span><span class="sxs-lookup"><span data-stu-id="b16b6-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="b16b6-285">建議您將閘道升級為最新的版本，以避免這類相依性。</span><span class="sxs-lookup"><span data-stu-id="b16b6-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="b16b6-286">若要使用此功能，請建立 [Azure 儲存體連結服務](data-factory-azure-blob-connector.md#azure-storage-linked-service)，這是指具有過渡 Blob 儲存體的 Azure 儲存體帳戶，然後針對複製活動指定 `enableStaging` 和 `stagingSettings` 屬性，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="b16b6-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="b16b6-287">使用 PolyBase 時的最佳作法</span><span class="sxs-lookup"><span data-stu-id="b16b6-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="b16b6-288">除了 [Azure SQL 資料倉儲的最佳做法](../sql-data-warehouse/sql-data-warehouse-best-practices.md)之外，下列章節還提供其他最佳做法。</span><span class="sxs-lookup"><span data-stu-id="b16b6-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="b16b6-289">必要的資料庫權限</span><span class="sxs-lookup"><span data-stu-id="b16b6-289">Required database permission</span></span>
<span data-ttu-id="b16b6-290">若要使用 PolyBase，要用來將資料載入 SQL 資料倉儲的使用者必須具備目標資料庫的 ["CONTROL" 權限](https://msdn.microsoft.com/library/ms191291.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="b16b6-291">達到此目標的其中一個方法是將該使用者新增為 "db_owner" 角色的成員。</span><span class="sxs-lookup"><span data-stu-id="b16b6-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="b16b6-292">依照[本節](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization)了解如何進行這項動作。</span><span class="sxs-lookup"><span data-stu-id="b16b6-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="b16b6-293">資料列大小和資料類型限制</span><span class="sxs-lookup"><span data-stu-id="b16b6-293">Row size and data type limitation</span></span>
<span data-ttu-id="b16b6-294">PolyBase 載入被限制為只能載入小於 **1 MB**，且不能載入至 VARCHR(MAX)、NVARCHAR(MAX) 或 VARBINARY(MAX) 的資料列。</span><span class="sxs-lookup"><span data-stu-id="b16b6-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="b16b6-295">請參閱[這裡](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="b16b6-296">如果您的來源資料包含大於 1 MB 的資料列，建議您將來源資料表垂直分割成數個小型資料表，而每個資料表的最大資料列大小均不超過限制。</span><span class="sxs-lookup"><span data-stu-id="b16b6-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="b16b6-297">然後可以使用 PolyBase 載入較小的資料表而在 Azure SQL 資料倉儲中合併在一起。</span><span class="sxs-lookup"><span data-stu-id="b16b6-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="b16b6-298">SQL 資料倉儲資源類別</span><span class="sxs-lookup"><span data-stu-id="b16b6-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="b16b6-299">若要達到最佳的可能輸送量，請考慮透過 PolyBase 將更大的資源類別指派給要用來將資料載入 SQL 資料倉儲的使用者。</span><span class="sxs-lookup"><span data-stu-id="b16b6-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="b16b6-300">遵循[變更使用者資源類別範例](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)，了解如何執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="b16b6-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="b16b6-301">Azure SQL 資料倉儲中的 tableName</span><span class="sxs-lookup"><span data-stu-id="b16b6-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="b16b6-302">下表提供的範例是關於如何針對各種結構描述和資料表名稱組合，在資料集 JSON 中指定 **tableName** 屬性。</span><span class="sxs-lookup"><span data-stu-id="b16b6-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="b16b6-303">DB 結構描述</span><span class="sxs-lookup"><span data-stu-id="b16b6-303">DB Schema</span></span> | <span data-ttu-id="b16b6-304">資料表名稱</span><span class="sxs-lookup"><span data-stu-id="b16b6-304">Table name</span></span> | <span data-ttu-id="b16b6-305">tableName JSON 屬性</span><span class="sxs-lookup"><span data-stu-id="b16b6-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b16b6-306">dbo</span><span class="sxs-lookup"><span data-stu-id="b16b6-306">dbo</span></span> |<span data-ttu-id="b16b6-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="b16b6-307">MyTable</span></span> |<span data-ttu-id="b16b6-308">MyTable 或 dbo.MyTable 或 [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="b16b6-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="b16b6-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="b16b6-309">dbo1</span></span> |<span data-ttu-id="b16b6-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="b16b6-310">MyTable</span></span> |<span data-ttu-id="b16b6-311">dbo1.MyTable 或 [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="b16b6-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="b16b6-312">dbo</span><span class="sxs-lookup"><span data-stu-id="b16b6-312">dbo</span></span> |<span data-ttu-id="b16b6-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="b16b6-313">My.Table</span></span> |<span data-ttu-id="b16b6-314">[My.Table] 或 [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="b16b6-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="b16b6-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="b16b6-315">dbo1</span></span> |<span data-ttu-id="b16b6-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="b16b6-316">My.Table</span></span> |<span data-ttu-id="b16b6-317">[dbo1].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="b16b6-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="b16b6-318">如果您看到下列錯誤，可能是您為 tableName 屬性指定的值有問題。</span><span class="sxs-lookup"><span data-stu-id="b16b6-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="b16b6-319">請參閱資料表，以正確的方式指定 tableName JSON 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="b16b6-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="b16b6-320">包含預設值的資料行</span><span class="sxs-lookup"><span data-stu-id="b16b6-320">Columns with default values</span></span>
<span data-ttu-id="b16b6-321">Data Factory 中的 PolyBase 功能目前只接受與目標資料表中相同的資料行數目。</span><span class="sxs-lookup"><span data-stu-id="b16b6-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="b16b6-322">假設您有內含四個資料行的資料表，且其中一個資料行已使用預設值進行定義。</span><span class="sxs-lookup"><span data-stu-id="b16b6-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="b16b6-323">輸入資料應該仍會包含四個資料行。</span><span class="sxs-lookup"><span data-stu-id="b16b6-323">The input data should still contain four columns.</span></span> <span data-ttu-id="b16b6-324">提供 3 個資料行的輸入資料集會產生類似下列訊息的錯誤︰</span><span class="sxs-lookup"><span data-stu-id="b16b6-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="b16b6-325">NULL 值是一種特殊形式的預設值。</span><span class="sxs-lookup"><span data-stu-id="b16b6-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="b16b6-326">如果資料行可為 null，該資料行的輸入資料 (在 Blob 中) 可以是空的 (不能在輸入資料集中遺漏)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="b16b6-327">PolyBase 會在 Azure SQL 資料倉儲中為其插入 NULL。</span><span class="sxs-lookup"><span data-stu-id="b16b6-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="b16b6-328">自動建立資料表</span><span class="sxs-lookup"><span data-stu-id="b16b6-328">Auto table creation</span></span>
<span data-ttu-id="b16b6-329">如果您使用複製精靈從 SQL Server 或 Azure SQL Database 中將資料複製到 Azure SQL 資料倉儲，且目的地存放區中沒有對應來源資料表的資料表，Data Factory 可以使用來源資料表結構描述，在資料倉儲中自動建立資料表。</span><span class="sxs-lookup"><span data-stu-id="b16b6-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="b16b6-330">Data Factory 會以和來源資料存放區中的資料表相同的名稱，在目的地存放區中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="b16b6-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="b16b6-331">資料行的資料類型會根據下列類型對應來選擇。</span><span class="sxs-lookup"><span data-stu-id="b16b6-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="b16b6-332">它會視需要執行類型轉換，以修正來源和目的地存放區之間所有不相容的情況。</span><span class="sxs-lookup"><span data-stu-id="b16b6-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="b16b6-333">它也會使用循環配置資源資料表散發。</span><span class="sxs-lookup"><span data-stu-id="b16b6-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="b16b6-334">來源 SQL Database 資料行類型</span><span class="sxs-lookup"><span data-stu-id="b16b6-334">Source SQL Database column type</span></span> | <span data-ttu-id="b16b6-335">目的地 SQL DW 資料行類型 (大小限制)</span><span class="sxs-lookup"><span data-stu-id="b16b6-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="b16b6-336">int</span><span class="sxs-lookup"><span data-stu-id="b16b6-336">Int</span></span> | <span data-ttu-id="b16b6-337">int</span><span class="sxs-lookup"><span data-stu-id="b16b6-337">Int</span></span> |
| <span data-ttu-id="b16b6-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="b16b6-338">BigInt</span></span> | <span data-ttu-id="b16b6-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="b16b6-339">BigInt</span></span> |
| <span data-ttu-id="b16b6-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b16b6-340">SmallInt</span></span> | <span data-ttu-id="b16b6-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b16b6-341">SmallInt</span></span> |
| <span data-ttu-id="b16b6-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="b16b6-342">TinyInt</span></span> | <span data-ttu-id="b16b6-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="b16b6-343">TinyInt</span></span> |
| <span data-ttu-id="b16b6-344">Bit</span><span class="sxs-lookup"><span data-stu-id="b16b6-344">Bit</span></span> | <span data-ttu-id="b16b6-345">Bit</span><span class="sxs-lookup"><span data-stu-id="b16b6-345">Bit</span></span> |
| <span data-ttu-id="b16b6-346">十進位</span><span class="sxs-lookup"><span data-stu-id="b16b6-346">Decimal</span></span> | <span data-ttu-id="b16b6-347">十進位</span><span class="sxs-lookup"><span data-stu-id="b16b6-347">Decimal</span></span> |
| <span data-ttu-id="b16b6-348">數值</span><span class="sxs-lookup"><span data-stu-id="b16b6-348">Numeric</span></span> | <span data-ttu-id="b16b6-349">十進位</span><span class="sxs-lookup"><span data-stu-id="b16b6-349">Decimal</span></span> |
| <span data-ttu-id="b16b6-350">Float</span><span class="sxs-lookup"><span data-stu-id="b16b6-350">Float</span></span> | <span data-ttu-id="b16b6-351">Float</span><span class="sxs-lookup"><span data-stu-id="b16b6-351">Float</span></span> |
| <span data-ttu-id="b16b6-352">Money</span><span class="sxs-lookup"><span data-stu-id="b16b6-352">Money</span></span> | <span data-ttu-id="b16b6-353">Money</span><span class="sxs-lookup"><span data-stu-id="b16b6-353">Money</span></span> |
| <span data-ttu-id="b16b6-354">Real</span><span class="sxs-lookup"><span data-stu-id="b16b6-354">Real</span></span> | <span data-ttu-id="b16b6-355">Real</span><span class="sxs-lookup"><span data-stu-id="b16b6-355">Real</span></span> |
| <span data-ttu-id="b16b6-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="b16b6-356">SmallMoney</span></span> | <span data-ttu-id="b16b6-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="b16b6-357">SmallMoney</span></span> |
| <span data-ttu-id="b16b6-358">Binary</span><span class="sxs-lookup"><span data-stu-id="b16b6-358">Binary</span></span> | <span data-ttu-id="b16b6-359">Binary</span><span class="sxs-lookup"><span data-stu-id="b16b6-359">Binary</span></span> |
| <span data-ttu-id="b16b6-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="b16b6-360">Varbinary</span></span> | <span data-ttu-id="b16b6-361">Varbinary (最多 8000)</span><span class="sxs-lookup"><span data-stu-id="b16b6-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="b16b6-362">日期</span><span class="sxs-lookup"><span data-stu-id="b16b6-362">Date</span></span> | <span data-ttu-id="b16b6-363">日期</span><span class="sxs-lookup"><span data-stu-id="b16b6-363">Date</span></span> |
| <span data-ttu-id="b16b6-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-364">DateTime</span></span> | <span data-ttu-id="b16b6-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-365">DateTime</span></span> |
| <span data-ttu-id="b16b6-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="b16b6-366">DateTime2</span></span> | <span data-ttu-id="b16b6-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="b16b6-367">DateTime2</span></span> |
| <span data-ttu-id="b16b6-368">時間</span><span class="sxs-lookup"><span data-stu-id="b16b6-368">Time</span></span> | <span data-ttu-id="b16b6-369">時間</span><span class="sxs-lookup"><span data-stu-id="b16b6-369">Time</span></span> |
| <span data-ttu-id="b16b6-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b16b6-370">DateTimeOffset</span></span> | <span data-ttu-id="b16b6-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b16b6-371">DateTimeOffset</span></span> |
| <span data-ttu-id="b16b6-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-372">SmallDateTime</span></span> | <span data-ttu-id="b16b6-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-373">SmallDateTime</span></span> |
| <span data-ttu-id="b16b6-374">文字</span><span class="sxs-lookup"><span data-stu-id="b16b6-374">Text</span></span> | <span data-ttu-id="b16b6-375">Varchar (最多 8000)</span><span class="sxs-lookup"><span data-stu-id="b16b6-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="b16b6-376">NText</span><span class="sxs-lookup"><span data-stu-id="b16b6-376">NText</span></span> | <span data-ttu-id="b16b6-377">NVarChar (最多 4000)</span><span class="sxs-lookup"><span data-stu-id="b16b6-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="b16b6-378">映像</span><span class="sxs-lookup"><span data-stu-id="b16b6-378">Image</span></span> | <span data-ttu-id="b16b6-379">VarBinary (最多 8000)</span><span class="sxs-lookup"><span data-stu-id="b16b6-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="b16b6-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="b16b6-380">UniqueIdentifier</span></span> | <span data-ttu-id="b16b6-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="b16b6-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="b16b6-382">Char</span><span class="sxs-lookup"><span data-stu-id="b16b6-382">Char</span></span> | <span data-ttu-id="b16b6-383">Char</span><span class="sxs-lookup"><span data-stu-id="b16b6-383">Char</span></span> |
| <span data-ttu-id="b16b6-384">NChar</span><span class="sxs-lookup"><span data-stu-id="b16b6-384">NChar</span></span> | <span data-ttu-id="b16b6-385">NChar</span><span class="sxs-lookup"><span data-stu-id="b16b6-385">NChar</span></span> |
| <span data-ttu-id="b16b6-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="b16b6-386">VarChar</span></span> | <span data-ttu-id="b16b6-387">VarChar (最多 8000)</span><span class="sxs-lookup"><span data-stu-id="b16b6-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="b16b6-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="b16b6-388">NVarChar</span></span> | <span data-ttu-id="b16b6-389">NVarChar (最多 4000)</span><span class="sxs-lookup"><span data-stu-id="b16b6-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="b16b6-390">xml</span><span class="sxs-lookup"><span data-stu-id="b16b6-390">Xml</span></span> | <span data-ttu-id="b16b6-391">Varchar (最多 8000)</span><span class="sxs-lookup"><span data-stu-id="b16b6-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="b16b6-392">Azure SQL 資料倉儲的類型對應</span><span class="sxs-lookup"><span data-stu-id="b16b6-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="b16b6-393">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會使用下列 2 個步驟的方法，執行自動類型轉換，將來源類型轉換成接收類型：</span><span class="sxs-lookup"><span data-stu-id="b16b6-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="b16b6-394">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="b16b6-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="b16b6-395">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="b16b6-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="b16b6-396">將資料移進和移出 Azure SQL 資料倉儲時，會使用下列從 SQL 類型到 .NET 類型的對應，以及反向的對應。</span><span class="sxs-lookup"><span data-stu-id="b16b6-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="b16b6-397">此對應與 [ADO.NET 的 SQL Server 資料類型對應相同](https://msdn.microsoft.com/library/cc716729.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="b16b6-398">SQL Server Database Engine 類型</span><span class="sxs-lookup"><span data-stu-id="b16b6-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="b16b6-399">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="b16b6-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b16b6-400">bigint</span><span class="sxs-lookup"><span data-stu-id="b16b6-400">bigint</span></span> |<span data-ttu-id="b16b6-401">Int64</span><span class="sxs-lookup"><span data-stu-id="b16b6-401">Int64</span></span> |
| <span data-ttu-id="b16b6-402">binary</span><span class="sxs-lookup"><span data-stu-id="b16b6-402">binary</span></span> |<span data-ttu-id="b16b6-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-403">Byte[]</span></span> |
| <span data-ttu-id="b16b6-404">bit</span><span class="sxs-lookup"><span data-stu-id="b16b6-404">bit</span></span> |<span data-ttu-id="b16b6-405">Boolean</span><span class="sxs-lookup"><span data-stu-id="b16b6-405">Boolean</span></span> |
| <span data-ttu-id="b16b6-406">char</span><span class="sxs-lookup"><span data-stu-id="b16b6-406">char</span></span> |<span data-ttu-id="b16b6-407">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-407">String, Char[]</span></span> |
| <span data-ttu-id="b16b6-408">日期</span><span class="sxs-lookup"><span data-stu-id="b16b6-408">date</span></span> |<span data-ttu-id="b16b6-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-409">DateTime</span></span> |
| <span data-ttu-id="b16b6-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-410">Datetime</span></span> |<span data-ttu-id="b16b6-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-411">DateTime</span></span> |
| <span data-ttu-id="b16b6-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="b16b6-412">datetime2</span></span> |<span data-ttu-id="b16b6-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-413">DateTime</span></span> |
| <span data-ttu-id="b16b6-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b16b6-414">Datetimeoffset</span></span> |<span data-ttu-id="b16b6-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b16b6-415">DateTimeOffset</span></span> |
| <span data-ttu-id="b16b6-416">十進位</span><span class="sxs-lookup"><span data-stu-id="b16b6-416">Decimal</span></span> |<span data-ttu-id="b16b6-417">十進位</span><span class="sxs-lookup"><span data-stu-id="b16b6-417">Decimal</span></span> |
| <span data-ttu-id="b16b6-418">FILESTREAM 屬性 (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="b16b6-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="b16b6-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-419">Byte[]</span></span> |
| <span data-ttu-id="b16b6-420">Float</span><span class="sxs-lookup"><span data-stu-id="b16b6-420">Float</span></span> |<span data-ttu-id="b16b6-421">兩倍</span><span class="sxs-lookup"><span data-stu-id="b16b6-421">Double</span></span> |
| <span data-ttu-id="b16b6-422">image</span><span class="sxs-lookup"><span data-stu-id="b16b6-422">image</span></span> |<span data-ttu-id="b16b6-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-423">Byte[]</span></span> |
| <span data-ttu-id="b16b6-424">int</span><span class="sxs-lookup"><span data-stu-id="b16b6-424">int</span></span> |<span data-ttu-id="b16b6-425">Int32</span><span class="sxs-lookup"><span data-stu-id="b16b6-425">Int32</span></span> |
| <span data-ttu-id="b16b6-426">money</span><span class="sxs-lookup"><span data-stu-id="b16b6-426">money</span></span> |<span data-ttu-id="b16b6-427">十進位</span><span class="sxs-lookup"><span data-stu-id="b16b6-427">Decimal</span></span> |
| <span data-ttu-id="b16b6-428">nchar</span><span class="sxs-lookup"><span data-stu-id="b16b6-428">nchar</span></span> |<span data-ttu-id="b16b6-429">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-429">String, Char[]</span></span> |
| <span data-ttu-id="b16b6-430">ntext</span><span class="sxs-lookup"><span data-stu-id="b16b6-430">ntext</span></span> |<span data-ttu-id="b16b6-431">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-431">String, Char[]</span></span> |
| <span data-ttu-id="b16b6-432">numeric</span><span class="sxs-lookup"><span data-stu-id="b16b6-432">numeric</span></span> |<span data-ttu-id="b16b6-433">十進位</span><span class="sxs-lookup"><span data-stu-id="b16b6-433">Decimal</span></span> |
| <span data-ttu-id="b16b6-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="b16b6-434">nvarchar</span></span> |<span data-ttu-id="b16b6-435">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-435">String, Char[]</span></span> |
| <span data-ttu-id="b16b6-436">real</span><span class="sxs-lookup"><span data-stu-id="b16b6-436">real</span></span> |<span data-ttu-id="b16b6-437">單一</span><span class="sxs-lookup"><span data-stu-id="b16b6-437">Single</span></span> |
| <span data-ttu-id="b16b6-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="b16b6-438">rowversion</span></span> |<span data-ttu-id="b16b6-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-439">Byte[]</span></span> |
| <span data-ttu-id="b16b6-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="b16b6-440">smalldatetime</span></span> |<span data-ttu-id="b16b6-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="b16b6-441">DateTime</span></span> |
| <span data-ttu-id="b16b6-442">smallint</span><span class="sxs-lookup"><span data-stu-id="b16b6-442">smallint</span></span> |<span data-ttu-id="b16b6-443">Int16</span><span class="sxs-lookup"><span data-stu-id="b16b6-443">Int16</span></span> |
| <span data-ttu-id="b16b6-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="b16b6-444">smallmoney</span></span> |<span data-ttu-id="b16b6-445">十進位</span><span class="sxs-lookup"><span data-stu-id="b16b6-445">Decimal</span></span> |
| <span data-ttu-id="b16b6-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="b16b6-446">sql_variant</span></span> |<span data-ttu-id="b16b6-447">物件 *</span><span class="sxs-lookup"><span data-stu-id="b16b6-447">Object *</span></span> |
| <span data-ttu-id="b16b6-448">文字</span><span class="sxs-lookup"><span data-stu-id="b16b6-448">text</span></span> |<span data-ttu-id="b16b6-449">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-449">String, Char[]</span></span> |
| <span data-ttu-id="b16b6-450">分析</span><span class="sxs-lookup"><span data-stu-id="b16b6-450">time</span></span> |<span data-ttu-id="b16b6-451">時間範圍</span><span class="sxs-lookup"><span data-stu-id="b16b6-451">TimeSpan</span></span> |
| <span data-ttu-id="b16b6-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="b16b6-452">timestamp</span></span> |<span data-ttu-id="b16b6-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-453">Byte[]</span></span> |
| <span data-ttu-id="b16b6-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="b16b6-454">tinyint</span></span> |<span data-ttu-id="b16b6-455">位元組</span><span class="sxs-lookup"><span data-stu-id="b16b6-455">Byte</span></span> |
| <span data-ttu-id="b16b6-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="b16b6-456">uniqueidentifier</span></span> |<span data-ttu-id="b16b6-457">Guid</span><span class="sxs-lookup"><span data-stu-id="b16b6-457">Guid</span></span> |
| <span data-ttu-id="b16b6-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="b16b6-458">varbinary</span></span> |<span data-ttu-id="b16b6-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-459">Byte[]</span></span> |
| <span data-ttu-id="b16b6-460">varchar</span><span class="sxs-lookup"><span data-stu-id="b16b6-460">varchar</span></span> |<span data-ttu-id="b16b6-461">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="b16b6-461">String, Char[]</span></span> |
| <span data-ttu-id="b16b6-462">xml</span><span class="sxs-lookup"><span data-stu-id="b16b6-462">xml</span></span> |<span data-ttu-id="b16b6-463">xml</span><span class="sxs-lookup"><span data-stu-id="b16b6-463">Xml</span></span> |

<span data-ttu-id="b16b6-464">您也可以在複製活動定義中，將來自來源資料集的資料行與來自接收資料集的資料行對應。</span><span class="sxs-lookup"><span data-stu-id="b16b6-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="b16b6-465">如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="b16b6-466">往返 SQL 資料倉儲複製資料的 JSON 範例</span><span class="sxs-lookup"><span data-stu-id="b16b6-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="b16b6-467">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="b16b6-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b16b6-468">它們會示範如何將資料複製到 Azure SQL 資料倉儲和 Azure Blob 儲存體，以及複製其中的資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="b16b6-469">不過，您可以在 Azure Data Factory 中使用複製活動，從任何來源 **直接** 將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="b16b6-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="b16b6-470">範例：將資料從 Azure SQL 資料倉儲複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="b16b6-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="b16b6-471">此範例會定義下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="b16b6-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="b16b6-472">[AzureSqlDW](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="b16b6-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="b16b6-473">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="b16b6-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b16b6-474">[AzureSqlDWTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b16b6-475">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b16b6-476">具有使用 [SqlDWSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b16b6-477">此範例會每小時將時間序列 (每小時、每日等等) 資料從 Azure SQL 資料倉儲資料庫中的資料表複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="b16b6-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="b16b6-478">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="b16b6-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b16b6-479">**Azure SQL 資料倉儲連結服務：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="b16b6-480">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="b16b6-481">**Azure SQL 資料倉儲輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="b16b6-482">此範例假設您已在 SQL Azure 資料倉儲中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="b16b6-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="b16b6-483">設定 “external”: ”true” 會通知 Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="b16b6-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="b16b6-484">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="b16b6-485">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b16b6-486">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="b16b6-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b16b6-487">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="b16b6-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="b16b6-488">**管線中使用 SqlDWSource 和 BlobSink 的複製活動：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="b16b6-489">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="b16b6-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b16b6-490">在管線 JSON 定義中，**source** 類型設為 **SqlDWSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="b16b6-491">針對 **SqlReaderQuery** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="b16b6-492">在此範例中，已為 SqlDWSource 指定 **sqlReaderQuery** 。</span><span class="sxs-lookup"><span data-stu-id="b16b6-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="b16b6-493">複製活動會針對 Azure SQL 資料倉儲來源執行這項查詢以取得資料。</span><span class="sxs-lookup"><span data-stu-id="b16b6-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="b16b6-494">或者，您可以藉由指定 **sqlReaderStoredProcedureName** 和 **storedProcedureParameters** (如果預存程序接受參數) 來指定預存程序。</span><span class="sxs-lookup"><span data-stu-id="b16b6-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="b16b6-495">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，就會使用資料集 JSON 的結構區段中定義的資料行來建立一個查詢，以對 Azure SQL 資料倉儲執行 (從 mytable 選取 column1、column2)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b16b6-496">如果資料集定義沒有結構，則會從資料表中選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="b16b6-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="b16b6-497">範例：將資料從 Azure Blob 複製到 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="b16b6-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="b16b6-498">此範例會定義下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="b16b6-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="b16b6-499">[AzureSqlDW](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="b16b6-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="b16b6-500">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="b16b6-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b16b6-501">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="b16b6-502">[AzureSqlDWTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="b16b6-503">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [SqlDWSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="b16b6-504">此範例會每小時將時間序列資料 (每小時、每日等等) 從 Azure Blob 複製到 Azure SQL 資料倉儲資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="b16b6-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="b16b6-505">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="b16b6-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="b16b6-506">**Azure SQL 資料倉儲連結服務：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="b16b6-507">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="b16b6-508">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="b16b6-509">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="b16b6-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b16b6-510">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="b16b6-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="b16b6-511">資料夾路徑使用開始時間的年、月、日部分，而檔案名稱使用開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="b16b6-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="b16b6-512">“external”: “true” 設定會通知 Data Factory 服務：這是 Data Factory 外部的資料表而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="b16b6-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="b16b6-513">**Azure SQL 資料倉儲輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="b16b6-514">此範例會將資料複製到 Azure SQL 資料倉儲中名為 "MyTable" 的資料表。</span><span class="sxs-lookup"><span data-stu-id="b16b6-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b16b6-515">請在Azure SQL 資料倉儲中建立此資料表，其資料行的數目如您預期 Blob CSV 檔案要包含的數目。</span><span class="sxs-lookup"><span data-stu-id="b16b6-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="b16b6-516">此資料表會每小時加入新的資料列。</span><span class="sxs-lookup"><span data-stu-id="b16b6-516">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="b16b6-517">**具有 BlobSource 和 SqlDWSink 的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="b16b6-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="b16b6-518">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="b16b6-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="b16b6-519">在管線 JSON 定義中，**source** 類型設為 **BlobSource**，而 **sink** 類型設為 **SqlDWSink**。</span><span class="sxs-lookup"><span data-stu-id="b16b6-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

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
<span data-ttu-id="b16b6-520">如需逐步解說，請參閱 Azure SQL 資料倉儲文件中的[使用 Azure Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲](data-factory-load-sql-data-warehouse.md)和[使用 Azure Data Factory 載入資料](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md)文章。</span><span class="sxs-lookup"><span data-stu-id="b16b6-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b16b6-521">效能和微調</span><span class="sxs-lookup"><span data-stu-id="b16b6-521">Performance and Tuning</span></span>
<span data-ttu-id="b16b6-522">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="b16b6-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
