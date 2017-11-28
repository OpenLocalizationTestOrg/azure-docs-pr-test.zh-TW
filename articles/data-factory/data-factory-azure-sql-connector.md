---
title: "aaaCopy 資料從 Azure SQL Database 的 / |Microsoft 文件"
description: "深入了解如何從 Azure SQL Database 使用 Azure Data Factory 的/toocopy 資料。"
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
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="00323-103">從 Azure SQL Database 使用 Azure Data Factory 複製資料 tooand</span><span class="sxs-lookup"><span data-stu-id="00323-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="00323-104">本文說明 toouse 中從 Azure SQL Database 的 Azure Data Factory toomove 資料 tooand hello 複製活動的方式。</span><span class="sxs-lookup"><span data-stu-id="00323-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="00323-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="00323-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="00323-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="00323-106">Supported scenarios</span></span>
<span data-ttu-id="00323-107">您可以將資料複製**從 Azure SQL Database** toohello 下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="00323-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="00323-108">您可以將資料複製下列資料存放區的 hello **tooAzure SQL Database**:</span><span class="sxs-lookup"><span data-stu-id="00323-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="00323-109">支援的驗證類型</span><span class="sxs-lookup"><span data-stu-id="00323-109">Supported authentication type</span></span>
<span data-ttu-id="00323-110">Azure SQL Database 連接器支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="00323-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="00323-111">開始使用</span><span class="sxs-lookup"><span data-stu-id="00323-111">Getting started</span></span>
<span data-ttu-id="00323-112">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="00323-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="00323-113">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="00323-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="00323-114">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="00323-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="00323-115">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="00323-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="00323-116">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="00323-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="00323-117">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="00323-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="00323-118">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="00323-118">Create a **data factory**.</span></span> <span data-ttu-id="00323-119">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="00323-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="00323-120">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="00323-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="00323-121">例如，如果您從 Azure blob 儲存體 tooan Azure SQL database 中複製資料，您建立兩個連結的服務 toolink 您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="00323-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="00323-122">連結的服務是特定 tooAzure SQL 資料庫的內容，請參閱[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="00323-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="00323-123">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="00323-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="00323-124">在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="00323-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="00323-125">而且，您保存 hello 資料複製 hello blob 儲存體中的 hello Azure SQL database 中建立另一個資料集 toospecify hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="00323-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="00323-126">資料集是特定 tooAzure 資料湖存放區的屬性，請參閱[資料集屬性](#dataset-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="00323-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="00323-127">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="00323-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="00323-128">在先前所述 hello 範例中，您使用 BlobSource 作為來源與 SqlSink 做為接收器 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="00323-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="00323-129">同樣地，如果您要複製 Azure SQL Database tooAzure Blob 儲存體，您使用 SqlSource 和 BlobSink hello 複製活動中。</span><span class="sxs-lookup"><span data-stu-id="00323-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="00323-130">特定 tooAzure SQL Database 複製活動內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="00323-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="00323-131">如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。</span><span class="sxs-lookup"><span data-stu-id="00323-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="00323-132">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="00323-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="00323-133">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="00323-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="00323-134">如需使用的 toocopy 資料至 azure 或從 Azure SQL Database 的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-sql-database)本文一節。</span><span class="sxs-lookup"><span data-stu-id="00323-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="00323-135">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure SQL Database 的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="00323-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="00323-136">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="00323-136">Linked service properties</span></span>
<span data-ttu-id="00323-137">Azure SQL 連結服務連結的 Azure SQL database tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="00323-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="00323-138">hello 下表提供的 JSON 元素特定 tooAzure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="00323-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="00323-139">屬性</span><span class="sxs-lookup"><span data-stu-id="00323-139">Property</span></span> | <span data-ttu-id="00323-140">說明</span><span class="sxs-lookup"><span data-stu-id="00323-140">Description</span></span> | <span data-ttu-id="00323-141">必要</span><span class="sxs-lookup"><span data-stu-id="00323-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00323-142">類型</span><span class="sxs-lookup"><span data-stu-id="00323-142">type</span></span> |<span data-ttu-id="00323-143">hello 類型屬性必須設定為： **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="00323-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="00323-144">是</span><span class="sxs-lookup"><span data-stu-id="00323-144">Yes</span></span> |
| <span data-ttu-id="00323-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="00323-145">connectionString</span></span> |<span data-ttu-id="00323-146">指定所需的資訊 tooconnect toohello Azure SQL Database 執行個體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="00323-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="00323-147">僅支援基本驗證。</span><span class="sxs-lookup"><span data-stu-id="00323-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="00323-148">是</span><span class="sxs-lookup"><span data-stu-id="00323-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="00323-149">設定[Azure SQL Database 防火牆](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)太 hello 資料庫伺服器[允許 Azure 服務 tooaccess hello 伺服器](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure)。</span><span class="sxs-lookup"><span data-stu-id="00323-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="00323-150">此外，如果您要從內部部署資料來源與資料處理站閘道外部 Azure 包括複製資料 tooAzure SQL 資料庫，設定正在傳送資料 tooAzure SQL Database 的 hello 機器的適當 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="00323-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="00323-151">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="00323-151">Dataset properties</span></span>
<span data-ttu-id="00323-152">資料集 toorepresent toospecify Azure SQL database 中的輸入或輸出資料，設定 hello hello 資料集的類型屬性： **AzureSqlTable**。</span><span class="sxs-lookup"><span data-stu-id="00323-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="00323-153">設定 hello **linkedServiceName**屬性 hello 資料集 toohello 名稱 hello Azure SQL 連結服務。</span><span class="sxs-lookup"><span data-stu-id="00323-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="00323-154">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="00323-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="00323-155">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="00323-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="00323-156">hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="00323-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="00323-157">hello **typeProperties** hello 資料集的類型 > 一節**AzureSqlTable**具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="00323-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="00323-158">屬性</span><span class="sxs-lookup"><span data-stu-id="00323-158">Property</span></span> | <span data-ttu-id="00323-159">說明</span><span class="sxs-lookup"><span data-stu-id="00323-159">Description</span></span> | <span data-ttu-id="00323-160">必要</span><span class="sxs-lookup"><span data-stu-id="00323-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00323-161">tableName</span><span class="sxs-lookup"><span data-stu-id="00323-161">tableName</span></span> |<span data-ttu-id="00323-162">參照 hello 資料表或檢視中的連結服務的 hello Azure SQL Database 執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="00323-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="00323-163">是</span><span class="sxs-lookup"><span data-stu-id="00323-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="00323-164">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="00323-164">Copy activity properties</span></span>
<span data-ttu-id="00323-165">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="00323-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="00323-166">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="00323-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="00323-167">hello 複製活動會採用只有 1 個輸入，並產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="00323-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="00323-168">而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="00323-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="00323-169">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="00323-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="00323-170">如果您要移動資料從 Azure SQL database，您設定 hello 來源類型 hello 複製活動中太**SqlSource**。</span><span class="sxs-lookup"><span data-stu-id="00323-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="00323-171">同樣地，如果您要移動資料 tooan Azure SQL database，您設定 hello 接收器類型 hello 複製活動中太**SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="00323-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="00323-172">本節提供 SqlSource 和 SqlSink 支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="00323-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="00323-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="00323-173">SqlSource</span></span>
<span data-ttu-id="00323-174">複製活動中，當 hello 來源的類型為**SqlSource**中的下列屬性的 hello 可用**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="00323-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="00323-175">屬性</span><span class="sxs-lookup"><span data-stu-id="00323-175">Property</span></span> | <span data-ttu-id="00323-176">說明</span><span class="sxs-lookup"><span data-stu-id="00323-176">Description</span></span> | <span data-ttu-id="00323-177">允許的值</span><span class="sxs-lookup"><span data-stu-id="00323-177">Allowed values</span></span> | <span data-ttu-id="00323-178">必要</span><span class="sxs-lookup"><span data-stu-id="00323-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00323-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="00323-179">sqlReaderQuery</span></span> |<span data-ttu-id="00323-180">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="00323-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="00323-181">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="00323-181">SQL query string.</span></span> <span data-ttu-id="00323-182">範例： `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="00323-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="00323-183">否</span><span class="sxs-lookup"><span data-stu-id="00323-183">No</span></span> |
| <span data-ttu-id="00323-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="00323-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="00323-185">名稱的 hello 預存程序會從 hello 來源資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="00323-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="00323-186">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="00323-186">Name of hello stored procedure.</span></span> <span data-ttu-id="00323-187">hello 最後一個 SQL 陳述式必須在 hello 預存程序中的 SELECT 陳述式。</span><span class="sxs-lookup"><span data-stu-id="00323-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="00323-188">否</span><span class="sxs-lookup"><span data-stu-id="00323-188">No</span></span> |
| <span data-ttu-id="00323-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="00323-189">storedProcedureParameters</span></span> |<span data-ttu-id="00323-190">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="00323-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="00323-191">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="00323-191">Name/value pairs.</span></span> <span data-ttu-id="00323-192">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="00323-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="00323-193">否</span><span class="sxs-lookup"><span data-stu-id="00323-193">No</span></span> |

<span data-ttu-id="00323-194">如果 hello **sqlReaderQuery**指定 hello SqlSource，hello 複製活動會針對 hello Azure SQL Database 來源 tooget hello 資料執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="00323-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="00323-195">或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。</span><span class="sxs-lookup"><span data-stu-id="00323-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="00323-196">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 資料集 JSON hello 結構區段中定義的資料行是使用的 toobuild 查詢 (`select column1, column2 from mytable`) toorun 針對 hello Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="00323-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="00323-197">如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="00323-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="00323-198">當您使用**sqlReaderStoredProcedureName**，您仍然需要 toospecify 值 hello **tableName** hello 資料集 JSON 中的屬性。</span><span class="sxs-lookup"><span data-stu-id="00323-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="00323-199">雖然目前尚未針對此資料表來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="00323-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="00323-200">SqlSource 範例</span><span class="sxs-lookup"><span data-stu-id="00323-200">SqlSource example</span></span>

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

<span data-ttu-id="00323-201">**hello 預存程序定義：**</span><span class="sxs-lookup"><span data-stu-id="00323-201">**hello stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="00323-202">管線</span><span class="sxs-lookup"><span data-stu-id="00323-202">SqlSink</span></span>
<span data-ttu-id="00323-203">**SqlSink**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="00323-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="00323-204">屬性</span><span class="sxs-lookup"><span data-stu-id="00323-204">Property</span></span> | <span data-ttu-id="00323-205">說明</span><span class="sxs-lookup"><span data-stu-id="00323-205">Description</span></span> | <span data-ttu-id="00323-206">允許的值</span><span class="sxs-lookup"><span data-stu-id="00323-206">Allowed values</span></span> | <span data-ttu-id="00323-207">必要</span><span class="sxs-lookup"><span data-stu-id="00323-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00323-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="00323-208">writeBatchTimeout</span></span> |<span data-ttu-id="00323-209">在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="00323-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="00323-210">時間範圍</span><span class="sxs-lookup"><span data-stu-id="00323-210">timespan</span></span><br/><br/> <span data-ttu-id="00323-211">範例：“00:30:00” (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="00323-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="00323-212">否</span><span class="sxs-lookup"><span data-stu-id="00323-212">No</span></span> |
| <span data-ttu-id="00323-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="00323-213">writeBatchSize</span></span> |<span data-ttu-id="00323-214">當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="00323-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="00323-215">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="00323-215">Integer (number of rows)</span></span> |<span data-ttu-id="00323-216">否 (預設值：10000)</span><span class="sxs-lookup"><span data-stu-id="00323-216">No (default: 10000)</span></span> |
| <span data-ttu-id="00323-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="00323-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="00323-218">複製活動 tooexecute 查詢指定的特定配量的資料清除。</span><span class="sxs-lookup"><span data-stu-id="00323-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="00323-219">如需詳細資訊，請參閱[可重複複製](#repeatable-copy)。</span><span class="sxs-lookup"><span data-stu-id="00323-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="00323-220">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="00323-220">A query statement.</span></span> |<span data-ttu-id="00323-221">否</span><span class="sxs-lookup"><span data-stu-id="00323-221">No</span></span> |
| <span data-ttu-id="00323-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="00323-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="00323-223">指定複製活動 toofill 的資料行名稱與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。</span><span class="sxs-lookup"><span data-stu-id="00323-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="00323-224">如需詳細資訊，請參閱[可重複複製](#repeatable-copy)。</span><span class="sxs-lookup"><span data-stu-id="00323-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="00323-225">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="00323-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="00323-226">否</span><span class="sxs-lookup"><span data-stu-id="00323-226">No</span></span> |
| <span data-ttu-id="00323-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="00323-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="00323-228">名稱的 hello 預存程序 upserts （更新/插入） 資料到 hello 目標資料表。</span><span class="sxs-lookup"><span data-stu-id="00323-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="00323-229">名稱的 hello 預存程序。</span><span class="sxs-lookup"><span data-stu-id="00323-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="00323-230">否</span><span class="sxs-lookup"><span data-stu-id="00323-230">No</span></span> |
| <span data-ttu-id="00323-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="00323-231">storedProcedureParameters</span></span> |<span data-ttu-id="00323-232">Hello 參數，預存程序。</span><span class="sxs-lookup"><span data-stu-id="00323-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="00323-233">名稱/值組。</span><span class="sxs-lookup"><span data-stu-id="00323-233">Name/value pairs.</span></span> <span data-ttu-id="00323-234">名稱和大小寫的參數必須符合 hello 名稱和大小寫的 hello 預存程序參數。</span><span class="sxs-lookup"><span data-stu-id="00323-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="00323-235">否</span><span class="sxs-lookup"><span data-stu-id="00323-235">No</span></span> |
| <span data-ttu-id="00323-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="00323-236">sqlWriterTableType</span></span> |<span data-ttu-id="00323-237">指定用於 hello 預存程序中的資料表類型名稱 toobe。</span><span class="sxs-lookup"><span data-stu-id="00323-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="00323-238">複製活動移動 hello 資料可讓在暫存資料表與此資料表類型。</span><span class="sxs-lookup"><span data-stu-id="00323-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="00323-239">預存程序程式碼可以再合併 hello 資料會被複製現有的資料。</span><span class="sxs-lookup"><span data-stu-id="00323-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="00323-240">資料表類型名稱。</span><span class="sxs-lookup"><span data-stu-id="00323-240">A table type name.</span></span> |<span data-ttu-id="00323-241">否</span><span class="sxs-lookup"><span data-stu-id="00323-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="00323-242">SqlSink 範例</span><span class="sxs-lookup"><span data-stu-id="00323-242">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="00323-243">從 SQL Database 中複製資料 tooand JSON 範例</span><span class="sxs-lookup"><span data-stu-id="00323-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="00323-244">hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="00323-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="00323-245">它們會顯示如何從 Azure SQL Database 和 Azure Blob 儲存體 toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="00323-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="00323-246">不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="00323-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="00323-247">範例： 將資料複製 Azure SQL Database tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="00323-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="00323-248">hello 相同定義下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="00323-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="00323-249">[AzureSqlDatabase](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="00323-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="00323-250">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="00323-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="00323-251">[AzureSqlTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="00323-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="00323-252">[Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="00323-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="00323-253">具有使用 [SqlSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之「複製活動」的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="00323-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="00323-254">hello 範例時間序列資料 （每小時、 每天、 等等） 資料表中的複製 Azure SQL database tooa blob 中的每個小時。</span><span class="sxs-lookup"><span data-stu-id="00323-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="00323-255">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="00323-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="00323-256">**Azure SQL Database 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="00323-256">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="00323-257">請參閱 hello [Azure SQL 連結服務](#linked-service)hello 清單支援這項連結服務屬性 > 一節。</span><span class="sxs-lookup"><span data-stu-id="00323-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="00323-258">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="00323-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="00323-259">請參閱 hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) hello 清單支援這項連結服務屬性的發行項。</span><span class="sxs-lookup"><span data-stu-id="00323-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="00323-260">**Azure SQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="00323-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="00323-261">hello 範例假設您已建立資料表"MyTable"Azure SQL 中，而且包含稱為 「 timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="00323-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="00323-262">設定"external":"true"會通知 hello Azure Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="00323-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="00323-263">請參閱 hello [Azure SQL 資料集型別屬性](#dataset)一節，以 hello 清單支援這個 dataset 類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="00323-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="00323-264">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="00323-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="00323-265">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="00323-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="00323-266">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="00323-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="00323-267">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="00323-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="00323-268">請參閱 hello [Azure Blob 資料集型別屬性](data-factory-azure-blob-connector.md#dataset-properties)一節，以 hello 清單支援這個 dataset 類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="00323-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="00323-269">**具有 SQL 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="00323-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="00323-270">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="00323-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="00323-271">在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="00323-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="00323-272">指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="00323-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
<span data-ttu-id="00323-273">在 hello 範例**sqlReaderQuery** hello SqlSource 指定。</span><span class="sxs-lookup"><span data-stu-id="00323-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="00323-274">hello 複製活動會針對 hello Azure SQL Database 來源 tooget hello 資料執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="00323-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="00323-275">或者，您可以指定預存程序，藉由指定 hello **sqlReaderStoredProcedureName**和**storedProcedureParameters** （如果 hello 預存程序會採用參數）。</span><span class="sxs-lookup"><span data-stu-id="00323-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="00323-276">如果您未指定 sqlReaderQuery 或 sqlReaderStoredProcedureName，hello hello 資料集 JSON hello 結構區段中定義的資料行是使用的 toobuild hello Azure SQL Database 針對查詢 toorun。</span><span class="sxs-lookup"><span data-stu-id="00323-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="00323-277">例如： `select column1, column2 from mytable`。</span><span class="sxs-lookup"><span data-stu-id="00323-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="00323-278">如果您不需要 hello 資料集定義 hello 結構，所有資料行選取的 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="00323-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="00323-279">請參閱 hello [Sql 來源](#sqlsource)區段和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello 支援 SqlSource 和 BlobSink 屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="00323-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="00323-280">範例： 將資料從 Azure Blob tooAzure SQL Database 中複製</span><span class="sxs-lookup"><span data-stu-id="00323-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="00323-281">hello 範例會定義下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="00323-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="00323-282">[AzureSqlDatabase](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="00323-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="00323-283">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="00323-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="00323-284">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="00323-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="00323-285">[AzureSqlTable](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="00323-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="00323-286">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 和 [SqlSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="00323-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="00323-287">hello 範例時間序列資料 （每小時、 每天、 等等） 從 Azure blob tooa 資料表複製 Azure SQL database 中的每個小時。</span><span class="sxs-lookup"><span data-stu-id="00323-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="00323-288">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="00323-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="00323-289">**Azure SQL 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="00323-289">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="00323-290">請參閱 hello [Azure SQL 連結服務](#linked-service)hello 清單支援這項連結服務屬性 > 一節。</span><span class="sxs-lookup"><span data-stu-id="00323-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="00323-291">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="00323-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="00323-292">請參閱 hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) hello 清單支援這項連結服務屬性的發行項。</span><span class="sxs-lookup"><span data-stu-id="00323-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="00323-293">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="00323-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="00323-294">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="00323-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="00323-295">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="00323-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="00323-296">年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="00323-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="00323-297">"external":"true"的設定會在這個資料表是外部 toohello 資料處理站，而不產生 hello data factory 中的活動時通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="00323-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="00323-298">請參閱 hello [Azure Blob 資料集型別屬性](data-factory-azure-blob-connector.md#dataset-properties)一節，以 hello 清單支援這個 dataset 類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="00323-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="00323-299">**Azure SQL Database 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="00323-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="00323-300">hello 範例會將名為"MyTable"中 Azure SQL 資料 tooa 資料表複製。</span><span class="sxs-lookup"><span data-stu-id="00323-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="00323-301">建立 hello 資料表與 Azure SQL 中如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="00323-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="00323-302">新的資料列會加入 toohello 資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="00323-302">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="00323-303">請參閱 hello [Azure SQL 資料集型別屬性](#dataset)一節，以 hello 清單支援這個 dataset 類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="00323-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="00323-304">**具有 Blob 來源和 SQL 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="00323-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="00323-305">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="00323-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="00323-306">在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="00323-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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
<span data-ttu-id="00323-307">請參閱 hello [Sql 接收](#sqlsink)區段和[BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) hello 支援 SqlSink 和 BlobSource 屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="00323-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="00323-308">Hello 目標資料庫中的識別資料行</span><span class="sxs-lookup"><span data-stu-id="00323-308">Identity columns in hello target database</span></span>
<span data-ttu-id="00323-309">本節提供的範例資料複製到來源資料表沒有識別資料行的 tooa 目的地資料表之 identity 資料行。</span><span class="sxs-lookup"><span data-stu-id="00323-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="00323-310">**來源資料表：**</span><span class="sxs-lookup"><span data-stu-id="00323-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="00323-311">**目的地資料表：**</span><span class="sxs-lookup"><span data-stu-id="00323-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="00323-312">請注意該 hello 目標資料表有識別資料行。</span><span class="sxs-lookup"><span data-stu-id="00323-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="00323-313">**來源資料集 JSON 定義**</span><span class="sxs-lookup"><span data-stu-id="00323-313">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="00323-314">**目的地資料集 JSON 定義**</span><span class="sxs-lookup"><span data-stu-id="00323-314">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="00323-315">請注意，您的來源資料表與目標資料表的結構描述不同 (目標資料表有一個具有身分識別的額外資料行)。</span><span class="sxs-lookup"><span data-stu-id="00323-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="00323-316">在此案例中，您需要 toospecify**結構**hello 目標資料集定義，其中不包括 hello 識別資料行中的屬性。</span><span class="sxs-lookup"><span data-stu-id="00323-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="00323-317">從 SQL 接收器叫用預存程序</span><span class="sxs-lookup"><span data-stu-id="00323-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="00323-318">如需在管線的複製活動中從 SQL 接收器叫用預存程序的範例，請參閱[在複製活動中叫用 SQL 接收器的預存程序](data-factory-invoke-stored-procedure-from-copy-activity.md)一文。</span><span class="sxs-lookup"><span data-stu-id="00323-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="00323-319">Azure SQL Database 的類型對應</span><span class="sxs-lookup"><span data-stu-id="00323-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="00323-320">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)複製活動的文件以 hello 遵循 2 步驟方法執行從來源類型 toosink 類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="00323-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="00323-321">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="00323-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="00323-322">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="00323-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="00323-323">當您從 Azure SQL Database 中移動資料 tooand，hello 下列的對應會使用從 SQL 型別 too.NET 類型，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="00323-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="00323-324">hello 對應是相同 hello ADO.NET 的 SQL Server 資料類型對應。</span><span class="sxs-lookup"><span data-stu-id="00323-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="00323-325">SQL Server Database Engine 類型</span><span class="sxs-lookup"><span data-stu-id="00323-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="00323-326">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="00323-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="00323-327">bigint</span><span class="sxs-lookup"><span data-stu-id="00323-327">bigint</span></span> |<span data-ttu-id="00323-328">Int64</span><span class="sxs-lookup"><span data-stu-id="00323-328">Int64</span></span> |
| <span data-ttu-id="00323-329">binary</span><span class="sxs-lookup"><span data-stu-id="00323-329">binary</span></span> |<span data-ttu-id="00323-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="00323-330">Byte[]</span></span> |
| <span data-ttu-id="00323-331">bit</span><span class="sxs-lookup"><span data-stu-id="00323-331">bit</span></span> |<span data-ttu-id="00323-332">Boolean</span><span class="sxs-lookup"><span data-stu-id="00323-332">Boolean</span></span> |
| <span data-ttu-id="00323-333">char</span><span class="sxs-lookup"><span data-stu-id="00323-333">char</span></span> |<span data-ttu-id="00323-334">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="00323-334">String, Char[]</span></span> |
| <span data-ttu-id="00323-335">日期</span><span class="sxs-lookup"><span data-stu-id="00323-335">date</span></span> |<span data-ttu-id="00323-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="00323-336">DateTime</span></span> |
| <span data-ttu-id="00323-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="00323-337">Datetime</span></span> |<span data-ttu-id="00323-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="00323-338">DateTime</span></span> |
| <span data-ttu-id="00323-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="00323-339">datetime2</span></span> |<span data-ttu-id="00323-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="00323-340">DateTime</span></span> |
| <span data-ttu-id="00323-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="00323-341">Datetimeoffset</span></span> |<span data-ttu-id="00323-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="00323-342">DateTimeOffset</span></span> |
| <span data-ttu-id="00323-343">十進位</span><span class="sxs-lookup"><span data-stu-id="00323-343">Decimal</span></span> |<span data-ttu-id="00323-344">十進位</span><span class="sxs-lookup"><span data-stu-id="00323-344">Decimal</span></span> |
| <span data-ttu-id="00323-345">FILESTREAM 屬性 (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="00323-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="00323-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="00323-346">Byte[]</span></span> |
| <span data-ttu-id="00323-347">Float</span><span class="sxs-lookup"><span data-stu-id="00323-347">Float</span></span> |<span data-ttu-id="00323-348">兩倍</span><span class="sxs-lookup"><span data-stu-id="00323-348">Double</span></span> |
| <span data-ttu-id="00323-349">image</span><span class="sxs-lookup"><span data-stu-id="00323-349">image</span></span> |<span data-ttu-id="00323-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="00323-350">Byte[]</span></span> |
| <span data-ttu-id="00323-351">int</span><span class="sxs-lookup"><span data-stu-id="00323-351">int</span></span> |<span data-ttu-id="00323-352">Int32</span><span class="sxs-lookup"><span data-stu-id="00323-352">Int32</span></span> |
| <span data-ttu-id="00323-353">money</span><span class="sxs-lookup"><span data-stu-id="00323-353">money</span></span> |<span data-ttu-id="00323-354">十進位</span><span class="sxs-lookup"><span data-stu-id="00323-354">Decimal</span></span> |
| <span data-ttu-id="00323-355">nchar</span><span class="sxs-lookup"><span data-stu-id="00323-355">nchar</span></span> |<span data-ttu-id="00323-356">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="00323-356">String, Char[]</span></span> |
| <span data-ttu-id="00323-357">ntext</span><span class="sxs-lookup"><span data-stu-id="00323-357">ntext</span></span> |<span data-ttu-id="00323-358">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="00323-358">String, Char[]</span></span> |
| <span data-ttu-id="00323-359">numeric</span><span class="sxs-lookup"><span data-stu-id="00323-359">numeric</span></span> |<span data-ttu-id="00323-360">十進位</span><span class="sxs-lookup"><span data-stu-id="00323-360">Decimal</span></span> |
| <span data-ttu-id="00323-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="00323-361">nvarchar</span></span> |<span data-ttu-id="00323-362">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="00323-362">String, Char[]</span></span> |
| <span data-ttu-id="00323-363">real</span><span class="sxs-lookup"><span data-stu-id="00323-363">real</span></span> |<span data-ttu-id="00323-364">單一</span><span class="sxs-lookup"><span data-stu-id="00323-364">Single</span></span> |
| <span data-ttu-id="00323-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="00323-365">rowversion</span></span> |<span data-ttu-id="00323-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="00323-366">Byte[]</span></span> |
| <span data-ttu-id="00323-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="00323-367">smalldatetime</span></span> |<span data-ttu-id="00323-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="00323-368">DateTime</span></span> |
| <span data-ttu-id="00323-369">smallint</span><span class="sxs-lookup"><span data-stu-id="00323-369">smallint</span></span> |<span data-ttu-id="00323-370">Int16</span><span class="sxs-lookup"><span data-stu-id="00323-370">Int16</span></span> |
| <span data-ttu-id="00323-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="00323-371">smallmoney</span></span> |<span data-ttu-id="00323-372">十進位</span><span class="sxs-lookup"><span data-stu-id="00323-372">Decimal</span></span> |
| <span data-ttu-id="00323-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="00323-373">sql_variant</span></span> |<span data-ttu-id="00323-374">物件 *</span><span class="sxs-lookup"><span data-stu-id="00323-374">Object *</span></span> |
| <span data-ttu-id="00323-375">文字</span><span class="sxs-lookup"><span data-stu-id="00323-375">text</span></span> |<span data-ttu-id="00323-376">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="00323-376">String, Char[]</span></span> |
| <span data-ttu-id="00323-377">分析</span><span class="sxs-lookup"><span data-stu-id="00323-377">time</span></span> |<span data-ttu-id="00323-378">時間範圍</span><span class="sxs-lookup"><span data-stu-id="00323-378">TimeSpan</span></span> |
| <span data-ttu-id="00323-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="00323-379">timestamp</span></span> |<span data-ttu-id="00323-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="00323-380">Byte[]</span></span> |
| <span data-ttu-id="00323-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="00323-381">tinyint</span></span> |<span data-ttu-id="00323-382">位元組</span><span class="sxs-lookup"><span data-stu-id="00323-382">Byte</span></span> |
| <span data-ttu-id="00323-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="00323-383">uniqueidentifier</span></span> |<span data-ttu-id="00323-384">Guid</span><span class="sxs-lookup"><span data-stu-id="00323-384">Guid</span></span> |
| <span data-ttu-id="00323-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="00323-385">varbinary</span></span> |<span data-ttu-id="00323-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="00323-386">Byte[]</span></span> |
| <span data-ttu-id="00323-387">varchar</span><span class="sxs-lookup"><span data-stu-id="00323-387">varchar</span></span> |<span data-ttu-id="00323-388">String、Char[]</span><span class="sxs-lookup"><span data-stu-id="00323-388">String, Char[]</span></span> |
| <span data-ttu-id="00323-389">xml</span><span class="sxs-lookup"><span data-stu-id="00323-389">xml</span></span> |<span data-ttu-id="00323-390">xml</span><span class="sxs-lookup"><span data-stu-id="00323-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="00323-391">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="00323-391">Map source toosink columns</span></span>
<span data-ttu-id="00323-392">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="00323-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="00323-393">可重複複製</span><span class="sxs-lookup"><span data-stu-id="00323-393">Repeatable copy</span></span>
<span data-ttu-id="00323-394">當複製資料 tooSQL 伺服器資料庫，hello 複製活動將預設附加 toohello 接收資料表。</span><span class="sxs-lookup"><span data-stu-id="00323-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="00323-395">相反地，請參閱 tooperform UPSERT[可重複寫入 tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink)發行項。</span><span class="sxs-lookup"><span data-stu-id="00323-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="00323-396">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="00323-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="00323-397">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="00323-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="00323-398">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="00323-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="00323-399">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="00323-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="00323-400">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="00323-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="00323-401">效能和微調</span><span class="sxs-lookup"><span data-stu-id="00323-401">Performance and Tuning</span></span>
<span data-ttu-id="00323-402">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="00323-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
