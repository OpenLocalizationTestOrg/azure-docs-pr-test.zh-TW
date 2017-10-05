---
title: "從 Azure SQL Database 來回複製資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Azure SQL 資料庫來回複製資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="fde07-103">使用 Azure Data Factory 從 Azure SQL Database 來回複製資料</span><span class="sxs-lookup"><span data-stu-id="fde07-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="fde07-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，將資料移進/移出 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="fde07-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="fde07-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="fde07-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="fde07-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="fde07-106">Supported scenarios</span></span>
<span data-ttu-id="fde07-107">您可以**從 Azure SQL Database**將資料複製到下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="fde07-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="fde07-108">您可以從下列資料存放區將資料複製**到 Azure SQL Database**：</span><span class="sxs-lookup"><span data-stu-id="fde07-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="fde07-109">支援的驗證類型</span><span class="sxs-lookup"><span data-stu-id="fde07-109">Supported authentication type</span></span>
<span data-ttu-id="fde07-110">Azure SQL Database 連接器支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="fde07-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fde07-111">開始使用</span><span class="sxs-lookup"><span data-stu-id="fde07-111">Getting started</span></span>
<span data-ttu-id="fde07-112">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="fde07-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="fde07-113">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="fde07-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="fde07-114">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="fde07-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="fde07-115">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="fde07-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fde07-116">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="fde07-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fde07-117">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="fde07-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="fde07-118">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="fde07-118">Create a **data factory**.</span></span> <span data-ttu-id="fde07-119">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="fde07-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="fde07-120">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="fde07-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="fde07-121">例如，如果您將資料從 Azure blob 儲存體複製到 Azure SQL 資料庫，您會建立兩個連結服務，將 Azure 儲存體帳戶和 Azure SQL 資料庫連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="fde07-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="fde07-122">有關 Azure SQL Database 專屬的連結服務屬性，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="fde07-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="fde07-123">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="fde07-124">在上一個步驟所述的範例中，您會建立資料集來指定 blob 容器和包含輸入資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fde07-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="fde07-125">您還會建立另一個資料集來指定 Azure SQL Database 中的 SQL 資料表，以保存從 Blob 儲存體複製的資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="fde07-126">有關 Azure Data Lake Store 專屬的資料集屬性，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="fde07-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="fde07-127">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="fde07-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="fde07-128">在稍早所述的範例中，您使用 BlobSource 作為來源，以及使用 SqlSink 作為複製活動的接收器。</span><span class="sxs-lookup"><span data-stu-id="fde07-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="fde07-129">同樣地，如果您是從 Azure SQL Database 複製到 Azure Blob 儲存體，則需要在複製活動中使用 SqlSource 和 BlobSink。</span><span class="sxs-lookup"><span data-stu-id="fde07-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="fde07-130">有關 Azure SQL Database 專屬的複製活動屬性，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="fde07-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="fde07-131">如需有關如何使用資料存放區作為來源或接收器的詳細資訊，請在上一節按一下適用於您的資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="fde07-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="fde07-132">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="fde07-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="fde07-133">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="fde07-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="fde07-134">如需相關範例，其中含有用來將資料複製到 Azure SQL Database (或從 Azure SQL Database 複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples-for-copying-data-to-and-from-sql-database)一節。</span><span class="sxs-lookup"><span data-stu-id="fde07-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="fde07-135">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Azure SQL Database 特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="fde07-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="fde07-136">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="fde07-136">Linked service properties</span></span>
<span data-ttu-id="fde07-137">Azure SQL 已連結服務可將 Azure SQL Database 連結到您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="fde07-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="fde07-138">下表提供 Azure SQL 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="fde07-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="fde07-139">屬性</span><span class="sxs-lookup"><span data-stu-id="fde07-139">Property</span></span> | <span data-ttu-id="fde07-140">說明</span><span class="sxs-lookup"><span data-stu-id="fde07-140">Description</span></span> | <span data-ttu-id="fde07-141">必要</span><span class="sxs-lookup"><span data-stu-id="fde07-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fde07-142">類型</span><span class="sxs-lookup"><span data-stu-id="fde07-142">type</span></span> |<span data-ttu-id="fde07-143">type 屬性必須設為： **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="fde07-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="fde07-144">是</span><span class="sxs-lookup"><span data-stu-id="fde07-144">Yes</span></span> |
| <span data-ttu-id="fde07-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="fde07-145">connectionString</span></span> |<span data-ttu-id="fde07-146">針對 connectionString 屬性指定連接到 Azure SQL Database 執行個體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="fde07-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="fde07-147">僅支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="fde07-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="fde07-148">是</span><span class="sxs-lookup"><span data-stu-id="fde07-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="fde07-149">設定 [Azure SQL Database 防火牆](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)和資料庫伺服器，以[允許 Azure 服務存取伺服器](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)。</span><span class="sxs-lookup"><span data-stu-id="fde07-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="fde07-150">此外，如果您要從 Azure 外部 (包括從具有 Fata Factory 閘道器的內部部署資料來源) 將資料複製到 Azure SQL Database，請為傳送資料到 Azure SQL Database 的機器設定適當的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="fde07-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="fde07-151">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="fde07-151">Dataset properties</span></span>
<span data-ttu-id="fde07-152">若要指定資料集以代表 Azure SQL Database 中的輸入或輸出資料，您需將資料集的類型屬性設定成：**AzureSqlTable**。</span><span class="sxs-lookup"><span data-stu-id="fde07-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="fde07-153">請將資料集的 **linkedServiceName** 屬性設定成 Azure SQL 已連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="fde07-154">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="fde07-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fde07-155">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="fde07-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fde07-156">每個資料集類型的 typeProperties 區段都不同，可提供資料存放區中資料的位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fde07-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="fde07-157">**AzureSqlTable** 類型資料集的 **typeProperties** 區段具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="fde07-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="fde07-158">屬性</span><span class="sxs-lookup"><span data-stu-id="fde07-158">Property</span></span> | <span data-ttu-id="fde07-159">說明</span><span class="sxs-lookup"><span data-stu-id="fde07-159">Description</span></span> | <span data-ttu-id="fde07-160">必要</span><span class="sxs-lookup"><span data-stu-id="fde07-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fde07-161">tableName</span><span class="sxs-lookup"><span data-stu-id="fde07-161">tableName</span></span> |<span data-ttu-id="fde07-162">Azure SQL Database 執行個體中連結服務所參考的資料表或檢視的名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="fde07-163">是</span><span class="sxs-lookup"><span data-stu-id="fde07-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fde07-164">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="fde07-164">Copy activity properties</span></span>
<span data-ttu-id="fde07-165">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="fde07-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fde07-166">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="fde07-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="fde07-167">複製活動只會採用一個輸入，而且只產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="fde07-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="fde07-168">而活動的 **typeProperties** 區段中，可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="fde07-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="fde07-169">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="fde07-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="fde07-170">如果您要將資料從 Azure SQL Database 移出，請將複製活動中的來源類型設定為 **SqlSource**。</span><span class="sxs-lookup"><span data-stu-id="fde07-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="fde07-171">同樣的，如果您要將資料移進 Azure SQL Database，請將複製活動中的接收器類型設定為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="fde07-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="fde07-172">本節提供 SqlSource 和 SqlSink 支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="fde07-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="fde07-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="fde07-173">SqlSource</span></span>
<span data-ttu-id="fde07-174">在複製活動中，如果來源的類型為 **SqlSource**，則 **typeProperties** 區段有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="fde07-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="fde07-175">屬性</span><span class="sxs-lookup"><span data-stu-id="fde07-175">Property</span></span> | <span data-ttu-id="fde07-176">說明</span><span class="sxs-lookup"><span data-stu-id="fde07-176">Description</span></span> | <span data-ttu-id="fde07-177">允許的值</span><span class="sxs-lookup"><span data-stu-id="fde07-177">Allowed values</span></span> | <span data-ttu-id="fde07-178">必要</span><span class="sxs-lookup"><span data-stu-id="fde07-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fde07-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="fde07-179">sqlReaderQuery</span></span> |<span data-ttu-id="fde07-180">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-180">Use the custom query to read data.</span></span> |<span data-ttu-id="fde07-181">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="fde07-181">SQL query string.</span></span> <span data-ttu-id="fde07-182">範例： `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="fde07-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="fde07-183">否</span><span class="sxs-lookup"><span data-stu-id="fde07-183">No</span></span> |
| <span data-ttu-id="fde07-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="fde07-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="fde07-185">從來源資料表讀取資料的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="fde07-186">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-186">Name of the stored procedure.</span></span> <span data-ttu-id="fde07-187">最後一個 SQL 陳述式必須是預存程序中的 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="fde07-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="fde07-188">否</span><span class="sxs-lookup"><span data-stu-id="fde07-188">No</span></span> |
| <span data-ttu-id="fde07-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fde07-189">storedProcedureParameters</span></span> |<span data-ttu-id="fde07-190">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="fde07-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="fde07-191">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="fde07-191">Name/value pairs.</span></span> <span data-ttu-id="fde07-192">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="fde07-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="fde07-193">否</span><span class="sxs-lookup"><span data-stu-id="fde07-193">No</span></span> |

<span data-ttu-id="fde07-194">如果已為 SqlSource 指定 **sqlReaderQuery** ，複製活動會針對 Azure SQL Database 來源執行這項查詢以取得資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="fde07-195">或者，您可以藉由指定 **sqlReaderStoredProcedureName** 和 **storedProcedureParameters** (如果預存程序接受參數) 來指定預存程序。</span><span class="sxs-lookup"><span data-stu-id="fde07-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="fde07-196">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，就會使用資料集 JSON 的結構區段中定義的資料行來建立一個查詢 (`select column1, column2 from mytable`)，以對 Azure SQL Database 執行。</span><span class="sxs-lookup"><span data-stu-id="fde07-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="fde07-197">如果資料集定義沒有結構，則會從資料表中選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="fde07-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="fde07-198">當您使用 **sqlReaderStoredProcedureName** 時，仍必須為資料集 JSON 中的 **tableName** 屬性指定值。</span><span class="sxs-lookup"><span data-stu-id="fde07-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="fde07-199">雖然目前尚未針對此資料表來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="fde07-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="fde07-200">SqlSource 範例</span><span class="sxs-lookup"><span data-stu-id="fde07-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="fde07-201">**預存程序定義：**</span><span class="sxs-lookup"><span data-stu-id="fde07-201">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="fde07-202">管線</span><span class="sxs-lookup"><span data-stu-id="fde07-202">SqlSink</span></span>
<span data-ttu-id="fde07-203">**SqlSink** 支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="fde07-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="fde07-204">屬性</span><span class="sxs-lookup"><span data-stu-id="fde07-204">Property</span></span> | <span data-ttu-id="fde07-205">說明</span><span class="sxs-lookup"><span data-stu-id="fde07-205">Description</span></span> | <span data-ttu-id="fde07-206">允許的值</span><span class="sxs-lookup"><span data-stu-id="fde07-206">Allowed values</span></span> | <span data-ttu-id="fde07-207">必要</span><span class="sxs-lookup"><span data-stu-id="fde07-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fde07-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="fde07-208">writeBatchTimeout</span></span> |<span data-ttu-id="fde07-209">在逾時前等待批次插入作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="fde07-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="fde07-210">時間範圍</span><span class="sxs-lookup"><span data-stu-id="fde07-210">timespan</span></span><br/><br/> <span data-ttu-id="fde07-211">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="fde07-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="fde07-212">否</span><span class="sxs-lookup"><span data-stu-id="fde07-212">No</span></span> |
| <span data-ttu-id="fde07-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="fde07-213">writeBatchSize</span></span> |<span data-ttu-id="fde07-214">當緩衝區大小達到 writeBatchSize 時，將資料插入 SQL 資料表中</span><span class="sxs-lookup"><span data-stu-id="fde07-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="fde07-215">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="fde07-215">Integer (number of rows)</span></span> |<span data-ttu-id="fde07-216">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="fde07-216">No (default: 10000)</span></span> |
| <span data-ttu-id="fde07-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="fde07-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="fde07-218">指定要讓「複製活動」執行的查詢，以便清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="fde07-219">如需詳細資訊，請參閱[可重複複製](#repeatable-copy)。</span><span class="sxs-lookup"><span data-stu-id="fde07-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="fde07-220">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="fde07-220">A query statement.</span></span> |<span data-ttu-id="fde07-221">否</span><span class="sxs-lookup"><span data-stu-id="fde07-221">No</span></span> |
| <span data-ttu-id="fde07-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="fde07-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="fde07-223">指定要讓「複製活動」以自動產生的分割識別碼填入的資料行名稱，這可在重新執行時用來清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="fde07-224">如需詳細資訊，請參閱[可重複複製](#repeatable-copy)。</span><span class="sxs-lookup"><span data-stu-id="fde07-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="fde07-225">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="fde07-226">否</span><span class="sxs-lookup"><span data-stu-id="fde07-226">No</span></span> |
| <span data-ttu-id="fde07-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="fde07-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="fde07-228">將資料更新插入 (更新/插入) 目標資料表中的預存程序名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="fde07-229">預存程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-229">Name of the stored procedure.</span></span> |<span data-ttu-id="fde07-230">否</span><span class="sxs-lookup"><span data-stu-id="fde07-230">No</span></span> |
| <span data-ttu-id="fde07-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fde07-231">storedProcedureParameters</span></span> |<span data-ttu-id="fde07-232">預存程序的參數。</span><span class="sxs-lookup"><span data-stu-id="fde07-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="fde07-233">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="fde07-233">Name/value pairs.</span></span> <span data-ttu-id="fde07-234">參數的名稱和大小寫必須符合預存程序參數的名稱和大小寫。</span><span class="sxs-lookup"><span data-stu-id="fde07-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="fde07-235">否</span><span class="sxs-lookup"><span data-stu-id="fde07-235">No</span></span> |
| <span data-ttu-id="fde07-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="fde07-236">sqlWriterTableType</span></span> |<span data-ttu-id="fde07-237">指定要在預存程序中使用的資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="fde07-238">複製活動可讓正在移動的資料可用於此資料表類型的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="fde07-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="fde07-239">然後，預存程序程式碼可以合併正在複製的資料與現有的資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="fde07-240">資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-240">A table type name.</span></span> |<span data-ttu-id="fde07-241">否</span><span class="sxs-lookup"><span data-stu-id="fde07-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="fde07-242">SqlSink 範例</span><span class="sxs-lookup"><span data-stu-id="fde07-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="fde07-243">往返 SQL Database 複製資料的 JSON 範例</span><span class="sxs-lookup"><span data-stu-id="fde07-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="fde07-244">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="fde07-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fde07-245">它們會示範如何將資料複製到 Azure SQL Database 和 Azure Blob 儲存體，以及複製其中的資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="fde07-246">不過，您可以在 Azure Data Factory 中使用複製活動，從任何來源 **直接** 將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="fde07-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="fde07-247">範例：將資料從 Azure SQL Database 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="fde07-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="fde07-248">相同內容會定義下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="fde07-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="fde07-249">[AzureSqlDatabase](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="fde07-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="fde07-250">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="fde07-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fde07-251">[AzureSqlTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="fde07-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="fde07-252">[Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="fde07-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fde07-253">具有使用 [SqlSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之「複製活動」的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="fde07-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fde07-254">此範例會每小時將時間序列資料 (每小時、每日等等) 從 Azure SQL Database 中的資料表複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="fde07-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="fde07-255">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="fde07-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="fde07-256">**Azure SQL Database 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="fde07-256">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="fde07-257">如需這個連結的服務所支援屬性的清單，請參閱 [Azure SQL 連結的服務](#linked-service) 一文。</span><span class="sxs-lookup"><span data-stu-id="fde07-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="fde07-258">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="fde07-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="fde07-259">如需這個連結的服務所支援屬性的清單，請參閱 [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) 一文。</span><span class="sxs-lookup"><span data-stu-id="fde07-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="fde07-260">**Azure SQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="fde07-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="fde07-261">此範例假設您已在 SQL Azure 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="fde07-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="fde07-262">設定 “external”: ”true” 會通知 Azure Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="fde07-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="fde07-263">如需這個資料集類型所支援屬性的清單，請參閱 [Azure SQL 資料集型別屬性](#dataset) 小節。</span><span class="sxs-lookup"><span data-stu-id="fde07-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="fde07-264">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="fde07-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fde07-265">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="fde07-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fde07-266">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="fde07-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="fde07-267">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="fde07-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
<span data-ttu-id="fde07-268">如需這個資料集類型所支援屬性的清單，請參閱 [Azure Blob 資料集型別屬性](data-factory-azure-blob-connector.md#dataset-properties) 小節。</span><span class="sxs-lookup"><span data-stu-id="fde07-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="fde07-269">**具有 SQL 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="fde07-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="fde07-270">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="fde07-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="fde07-271">在管線 JSON 定義中，**source** 類型設為 **SqlSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="fde07-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="fde07-272">針對 **SqlReaderQuery** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="fde07-273">在此範例中，已為 SqlSource 指定 **sqlReaderQuery** 。</span><span class="sxs-lookup"><span data-stu-id="fde07-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="fde07-274">複製活動會針對 Azure SQL Database 來源執行這項查詢以取得資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="fde07-275">或者，您可以藉由指定 **sqlReaderStoredProcedureName** 和 **storedProcedureParameters** (如果預存程序接受參數) 來指定預存程序。</span><span class="sxs-lookup"><span data-stu-id="fde07-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="fde07-276">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，就會使用資料集 JSON 的結構區段中定義的資料行來建立一個查詢，以對 Azure SQL Database 執行。</span><span class="sxs-lookup"><span data-stu-id="fde07-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="fde07-277">例如： `select column1, column2 from mytable`。</span><span class="sxs-lookup"><span data-stu-id="fde07-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="fde07-278">如果資料集定義沒有結構，則會從資料表中選取所有資料行。</span><span class="sxs-lookup"><span data-stu-id="fde07-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="fde07-279">如需 SqlSource 和 BlobSink 所支援屬性的清單，請參閱 [SQL 來源](#sqlsource)小節和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="fde07-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="fde07-280">範例：將資料從 Azure Blob 複製到 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="fde07-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="fde07-281">此範例會定義下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="fde07-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="fde07-282">[AzureSqlDatabase](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="fde07-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="fde07-283">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="fde07-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fde07-284">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="fde07-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="fde07-285">[AzureSqlTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="fde07-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="fde07-286">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [SqlSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="fde07-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="fde07-287">此範例會每小時將時間序列資料 (每小時、每日等等) 從 Azure Blob 複製到 Azure SQL Database 中的資料表。</span><span class="sxs-lookup"><span data-stu-id="fde07-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="fde07-288">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="fde07-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="fde07-289">**Azure SQL 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="fde07-289">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="fde07-290">如需這個連結的服務所支援屬性的清單，請參閱 [Azure SQL 連結的服務](#linked-service) 一文。</span><span class="sxs-lookup"><span data-stu-id="fde07-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="fde07-291">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="fde07-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="fde07-292">如需這個連結的服務所支援屬性的清單，請參閱 [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) 一文。</span><span class="sxs-lookup"><span data-stu-id="fde07-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="fde07-293">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="fde07-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="fde07-294">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="fde07-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fde07-295">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="fde07-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="fde07-296">資料夾路徑使用開始時間的年、月、日部分，而檔案名稱使用開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="fde07-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="fde07-297">“external”: “true” 設定會通知 Data Factory 服務：這是 Data Factory 外部的資料表而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="fde07-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="fde07-298">如需這個資料集類型所支援屬性的清單，請參閱 [Azure Blob 資料集型別屬性](data-factory-azure-blob-connector.md#dataset-properties) 小節。</span><span class="sxs-lookup"><span data-stu-id="fde07-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="fde07-299">**Azure SQL Database 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="fde07-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="fde07-300">此範例會將資料複製到 Azure SQL 中名為 "MyTable" 的資料表。</span><span class="sxs-lookup"><span data-stu-id="fde07-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="fde07-301">請在Azure SQL 中建立此資料表，其資料行的數目如您預期 Blob CSV 檔案要包含的數目。</span><span class="sxs-lookup"><span data-stu-id="fde07-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="fde07-302">此資料表會每小時加入新的資料列。</span><span class="sxs-lookup"><span data-stu-id="fde07-302">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
<span data-ttu-id="fde07-303">如需這個資料集類型所支援屬性的清單，請參閱 [Azure SQL 資料集型別屬性](#dataset) 小節。</span><span class="sxs-lookup"><span data-stu-id="fde07-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="fde07-304">**具有 Blob 來源和 SQL 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="fde07-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="fde07-305">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="fde07-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="fde07-306">在管線 JSON 定義中，**source** 類型設為 **BlobSource**，而 **sink** 類型設為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="fde07-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
<span data-ttu-id="fde07-307">如需 SqlSink 和 BlobSource 所支援屬性的清單，請參閱 [SQL 接收器](#sqlsink)小節和 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="fde07-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="fde07-308">目標資料庫中的身分識別資料行</span><span class="sxs-lookup"><span data-stu-id="fde07-308">Identity columns in the target database</span></span>
<span data-ttu-id="fde07-309">本節提供的範例將示範，如何把資料從沒有身分識別資料行的來源資料表，複製到具有身分識別資料行的目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="fde07-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="fde07-310">**來源資料表：**</span><span class="sxs-lookup"><span data-stu-id="fde07-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="fde07-311">**目的地資料表：**</span><span class="sxs-lookup"><span data-stu-id="fde07-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="fde07-312">請注意，目標資料表具有身分識別資料行。</span><span class="sxs-lookup"><span data-stu-id="fde07-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="fde07-313">**來源資料集 JSON 定義**</span><span class="sxs-lookup"><span data-stu-id="fde07-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="fde07-314">**目的地資料集 JSON 定義**</span><span class="sxs-lookup"><span data-stu-id="fde07-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="fde07-315">請注意，您的來源資料表與目標資料表的結構描述不同 (目標資料表有一個具有身分識別的額外資料行)。</span><span class="sxs-lookup"><span data-stu-id="fde07-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="fde07-316">在此案例中，您必須在目標資料集定義中指定 **structure** 屬性，這不包含身分識別資料行。</span><span class="sxs-lookup"><span data-stu-id="fde07-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="fde07-317">從 SQL 接收器叫用預存程序</span><span class="sxs-lookup"><span data-stu-id="fde07-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="fde07-318">如需在管線的複製活動中從 SQL 接收器叫用預存程序的範例，請參閱[在複製活動中叫用 SQL 接收器的預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)一文。</span><span class="sxs-lookup"><span data-stu-id="fde07-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="fde07-319">Azure SQL Database 的類型對應</span><span class="sxs-lookup"><span data-stu-id="fde07-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="fde07-320">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會使用下列 2 個步驟的方法，執行自動類型轉換，將來源類型轉換成接收類型：</span><span class="sxs-lookup"><span data-stu-id="fde07-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="fde07-321">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="fde07-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="fde07-322">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="fde07-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="fde07-323">將資料移進和移出 Azure SQL Database 時，會使用下列從 SQL 類型到 .NET 類型的對應，以及反向的對應。</span><span class="sxs-lookup"><span data-stu-id="fde07-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="fde07-324">此對應與 ADO.NET 的 SQL Server 資料類型對應相同。</span><span class="sxs-lookup"><span data-stu-id="fde07-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="fde07-325">SQL Server Database Engine 類型</span><span class="sxs-lookup"><span data-stu-id="fde07-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="fde07-326">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="fde07-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="fde07-327">bigint</span><span class="sxs-lookup"><span data-stu-id="fde07-327">bigint</span></span> |<span data-ttu-id="fde07-328">Int64</span><span class="sxs-lookup"><span data-stu-id="fde07-328">Int64</span></span> |
| <span data-ttu-id="fde07-329">binary</span><span class="sxs-lookup"><span data-stu-id="fde07-329">binary</span></span> |<span data-ttu-id="fde07-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fde07-330">Byte[]</span></span> |
| <span data-ttu-id="fde07-331">bit</span><span class="sxs-lookup"><span data-stu-id="fde07-331">bit</span></span> |<span data-ttu-id="fde07-332">Boolean</span><span class="sxs-lookup"><span data-stu-id="fde07-332">Boolean</span></span> |
| <span data-ttu-id="fde07-333">char</span><span class="sxs-lookup"><span data-stu-id="fde07-333">char</span></span> |<span data-ttu-id="fde07-334">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="fde07-334">String, Char[]</span></span> |
| <span data-ttu-id="fde07-335">日期</span><span class="sxs-lookup"><span data-stu-id="fde07-335">date</span></span> |<span data-ttu-id="fde07-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="fde07-336">DateTime</span></span> |
| <span data-ttu-id="fde07-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="fde07-337">Datetime</span></span> |<span data-ttu-id="fde07-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="fde07-338">DateTime</span></span> |
| <span data-ttu-id="fde07-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="fde07-339">datetime2</span></span> |<span data-ttu-id="fde07-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="fde07-340">DateTime</span></span> |
| <span data-ttu-id="fde07-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="fde07-341">Datetimeoffset</span></span> |<span data-ttu-id="fde07-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="fde07-342">DateTimeOffset</span></span> |
| <span data-ttu-id="fde07-343">十進位</span><span class="sxs-lookup"><span data-stu-id="fde07-343">Decimal</span></span> |<span data-ttu-id="fde07-344">十進位</span><span class="sxs-lookup"><span data-stu-id="fde07-344">Decimal</span></span> |
| <span data-ttu-id="fde07-345">FILESTREAM 屬性 (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="fde07-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="fde07-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fde07-346">Byte[]</span></span> |
| <span data-ttu-id="fde07-347">Float</span><span class="sxs-lookup"><span data-stu-id="fde07-347">Float</span></span> |<span data-ttu-id="fde07-348">兩倍</span><span class="sxs-lookup"><span data-stu-id="fde07-348">Double</span></span> |
| <span data-ttu-id="fde07-349">image</span><span class="sxs-lookup"><span data-stu-id="fde07-349">image</span></span> |<span data-ttu-id="fde07-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fde07-350">Byte[]</span></span> |
| <span data-ttu-id="fde07-351">int</span><span class="sxs-lookup"><span data-stu-id="fde07-351">int</span></span> |<span data-ttu-id="fde07-352">Int32</span><span class="sxs-lookup"><span data-stu-id="fde07-352">Int32</span></span> |
| <span data-ttu-id="fde07-353">money</span><span class="sxs-lookup"><span data-stu-id="fde07-353">money</span></span> |<span data-ttu-id="fde07-354">十進位</span><span class="sxs-lookup"><span data-stu-id="fde07-354">Decimal</span></span> |
| <span data-ttu-id="fde07-355">nchar</span><span class="sxs-lookup"><span data-stu-id="fde07-355">nchar</span></span> |<span data-ttu-id="fde07-356">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="fde07-356">String, Char[]</span></span> |
| <span data-ttu-id="fde07-357">ntext</span><span class="sxs-lookup"><span data-stu-id="fde07-357">ntext</span></span> |<span data-ttu-id="fde07-358">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="fde07-358">String, Char[]</span></span> |
| <span data-ttu-id="fde07-359">numeric</span><span class="sxs-lookup"><span data-stu-id="fde07-359">numeric</span></span> |<span data-ttu-id="fde07-360">十進位</span><span class="sxs-lookup"><span data-stu-id="fde07-360">Decimal</span></span> |
| <span data-ttu-id="fde07-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="fde07-361">nvarchar</span></span> |<span data-ttu-id="fde07-362">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="fde07-362">String, Char[]</span></span> |
| <span data-ttu-id="fde07-363">real</span><span class="sxs-lookup"><span data-stu-id="fde07-363">real</span></span> |<span data-ttu-id="fde07-364">單一</span><span class="sxs-lookup"><span data-stu-id="fde07-364">Single</span></span> |
| <span data-ttu-id="fde07-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="fde07-365">rowversion</span></span> |<span data-ttu-id="fde07-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fde07-366">Byte[]</span></span> |
| <span data-ttu-id="fde07-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="fde07-367">smalldatetime</span></span> |<span data-ttu-id="fde07-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="fde07-368">DateTime</span></span> |
| <span data-ttu-id="fde07-369">smallint</span><span class="sxs-lookup"><span data-stu-id="fde07-369">smallint</span></span> |<span data-ttu-id="fde07-370">Int16</span><span class="sxs-lookup"><span data-stu-id="fde07-370">Int16</span></span> |
| <span data-ttu-id="fde07-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="fde07-371">smallmoney</span></span> |<span data-ttu-id="fde07-372">十進位</span><span class="sxs-lookup"><span data-stu-id="fde07-372">Decimal</span></span> |
| <span data-ttu-id="fde07-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="fde07-373">sql_variant</span></span> |<span data-ttu-id="fde07-374">物件 *</span><span class="sxs-lookup"><span data-stu-id="fde07-374">Object *</span></span> |
| <span data-ttu-id="fde07-375">文字</span><span class="sxs-lookup"><span data-stu-id="fde07-375">text</span></span> |<span data-ttu-id="fde07-376">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="fde07-376">String, Char[]</span></span> |
| <span data-ttu-id="fde07-377">分析</span><span class="sxs-lookup"><span data-stu-id="fde07-377">time</span></span> |<span data-ttu-id="fde07-378">時間範圍</span><span class="sxs-lookup"><span data-stu-id="fde07-378">TimeSpan</span></span> |
| <span data-ttu-id="fde07-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="fde07-379">timestamp</span></span> |<span data-ttu-id="fde07-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fde07-380">Byte[]</span></span> |
| <span data-ttu-id="fde07-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="fde07-381">tinyint</span></span> |<span data-ttu-id="fde07-382">位元組</span><span class="sxs-lookup"><span data-stu-id="fde07-382">Byte</span></span> |
| <span data-ttu-id="fde07-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="fde07-383">uniqueidentifier</span></span> |<span data-ttu-id="fde07-384">Guid</span><span class="sxs-lookup"><span data-stu-id="fde07-384">Guid</span></span> |
| <span data-ttu-id="fde07-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="fde07-385">varbinary</span></span> |<span data-ttu-id="fde07-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="fde07-386">Byte[]</span></span> |
| <span data-ttu-id="fde07-387">varchar</span><span class="sxs-lookup"><span data-stu-id="fde07-387">varchar</span></span> |<span data-ttu-id="fde07-388">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="fde07-388">String, Char[]</span></span> |
| <span data-ttu-id="fde07-389">xml</span><span class="sxs-lookup"><span data-stu-id="fde07-389">xml</span></span> |<span data-ttu-id="fde07-390">xml</span><span class="sxs-lookup"><span data-stu-id="fde07-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="fde07-391">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="fde07-391">Map source to sink columns</span></span>
<span data-ttu-id="fde07-392">若要了解如何將來源資料集內的資料行對應至接收資料集內的資料行，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="fde07-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="fde07-393">可重複複製</span><span class="sxs-lookup"><span data-stu-id="fde07-393">Repeatable copy</span></span>
<span data-ttu-id="fde07-394">將資料複製到 SQL Server 資料庫時，複製活動預設會將資料附加至接收資料表。</span><span class="sxs-lookup"><span data-stu-id="fde07-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="fde07-395">若要改為執行 UPSERT，請參閱[對 SqlSink 進行可重複的寫入](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink)一文。</span><span class="sxs-lookup"><span data-stu-id="fde07-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="fde07-396">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="fde07-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="fde07-397">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="fde07-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fde07-398">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="fde07-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fde07-399">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="fde07-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fde07-400">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="fde07-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fde07-401">效能和微調</span><span class="sxs-lookup"><span data-stu-id="fde07-401">Performance and Tuning</span></span>
<span data-ttu-id="fde07-402">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="fde07-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
