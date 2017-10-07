---
title: "aaaCopy 資料至 azure 或從 Azure Blob 儲存體 |Microsoft 文件"
description: "了解如何 toocopy blob 在 Azure Data Factory 中的資料。 使用我們的範例： 如何從 Azure Blob 儲存體和 Azure SQL Database toocopy 資料 tooand。"
keywords: "blob 資料, azure blob 複製"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="8417c-105">從 Azure Blob 儲存體，使用 Azure Data Factory 複製資料 tooor</span><span class="sxs-lookup"><span data-stu-id="8417c-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="8417c-106">本文說明如何 toouse hello Azure Data Factory toocopy 資料 tooand 從 Azure Blob 儲存體中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="8417c-107">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="8417c-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="8417c-108">概觀</span><span class="sxs-lookup"><span data-stu-id="8417c-108">Overview</span></span>
<span data-ttu-id="8417c-109">您可以從任何支援的來源資料儲存 tooAzure Blob 儲存體，或從 Azure Blob 儲存體支援 tooany 接收資料存放區來複製資料。</span><span class="sxs-lookup"><span data-stu-id="8417c-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="8417c-110">hello 下表提供一份資料存放區支援做為來源或接收 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="8417c-111">例如，您可以將資料**從** SQL Server 資料庫或 Azure SQL Database 移**到** Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8417c-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="8417c-112">而且，您可以將資料「從」 Azure Blob 儲存體複製「到」 Azure SQL 資料倉儲或 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="8417c-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="8417c-113">支援的案例</span><span class="sxs-lookup"><span data-stu-id="8417c-113">Supported scenarios</span></span>
<span data-ttu-id="8417c-114">您可以將資料複製**從 Azure Blob 儲存體**toohello 下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="8417c-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="8417c-115">您可以將資料複製下列資料存放區的 hello **tooAzure Blob 儲存體**:</span><span class="sxs-lookup"><span data-stu-id="8417c-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="8417c-116">複製活動支援複製資料的 / tooboth 一般用途的 Azure 儲存體帳戶和熱/冷卻 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8417c-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="8417c-117">hello 活動支援**讀取區塊、 附加、 或分頁 blob**，但支援**撰寫 tooonly 區塊 blob**。</span><span class="sxs-lookup"><span data-stu-id="8417c-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="8417c-118">不支援使用「Azure 進階儲存體」作為接收器，因為它是以分頁 Blob 為後盾。</span><span class="sxs-lookup"><span data-stu-id="8417c-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="8417c-119">複製活動不會刪除資料來源 hello hello 資料已順利複製 toohello 目的地之後。</span><span class="sxs-lookup"><span data-stu-id="8417c-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="8417c-120">如果您需要 toodelete 來源資料複製成功之後，建立[自訂活動](data-factory-use-custom-activities.md)toodelete hello 資料，並使用 hello 管線中的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="8417c-121">如需範例，請參閱 hello [GitHub 上的刪除 blob 或資料夾範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity)。</span><span class="sxs-lookup"><span data-stu-id="8417c-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="8417c-122">開始使用</span><span class="sxs-lookup"><span data-stu-id="8417c-122">Get started</span></span>
<span data-ttu-id="8417c-123">您可以建立內含複製活動的管線，使用不同的工具/API 將資料移進/移出 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8417c-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="8417c-124">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="8417c-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="8417c-125">此發行項[逐步解說](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage)建立管線 toocopy 資料從 Azure Blob 儲存體位置 tooanother Azure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="8417c-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="8417c-126">如需建立管線 toocopy 資料從 Azure Blob 儲存體 tooAzure SQL Database 的教學課程，請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="8417c-127">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="8417c-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8417c-128">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="8417c-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="8417c-129">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="8417c-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="8417c-130">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="8417c-130">Create a **data factory**.</span></span> <span data-ttu-id="8417c-131">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="8417c-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="8417c-132">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="8417c-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="8417c-133">例如，如果您從 Azure blob 儲存體 tooan Azure SQL database 中複製資料，您建立兩個連結的服務 toolink 您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="8417c-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="8417c-134">對於屬於特定 tooAzure Blob 儲存體連結的服務屬性，請參閱[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="8417c-135">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="8417c-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="8417c-136">在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8417c-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="8417c-137">而且，您保存 hello 資料複製 hello blob 儲存體中的 hello Azure SQL database 中建立另一個資料集 toospecify hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="8417c-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="8417c-138">如為特定 tooAzure Blob 儲存體的資料集屬性，請參閱[資料集屬性](#dataset-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="8417c-139">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="8417c-140">在先前所述 hello 範例中，您使用 BlobSource 作為來源與 SqlSink 做為接收器 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="8417c-141">同樣地，如果您要複製 Azure SQL Database tooAzure Blob 儲存體，您使用 SqlSource 和 BlobSink hello 複製活動中。</span><span class="sxs-lookup"><span data-stu-id="8417c-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="8417c-142">特定 tooAzure Blob 儲存體複製活動內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="8417c-143">如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。</span><span class="sxs-lookup"><span data-stu-id="8417c-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="8417c-144">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="8417c-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="8417c-145">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="8417c-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="8417c-146">如需使用的 toocopy 資料至 azure 或從 Azure Blob 儲存體的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-blob-storage  )本文一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="8417c-147">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAzure Blob 儲存體的 JSON 屬性的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8417c-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8417c-148">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-148">Linked service properties</span></span>
<span data-ttu-id="8417c-149">有兩種類型的連結服務中，您可以使用 toolink Azure 儲存體 tooan Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="8417c-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="8417c-150">它們是：**AzureStorage** 連結服務和 **AzureStorageSas** 連結服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="8417c-151">hello Azure 儲存體連結服務提供 hello 與全域存取 toohello Azure 儲存體的資料處理站。</span><span class="sxs-lookup"><span data-stu-id="8417c-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="8417c-152">而 hello Azure 儲存體 SAS （共用存取簽章） 連結的限制/時間繫結存取 toohello Azure 儲存體的 hello data factory 提供服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="8417c-153">這兩個連結服務之間沒有其他差異。</span><span class="sxs-lookup"><span data-stu-id="8417c-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="8417c-154">選擇符合您需求的 hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="8417c-155">hello 下列各節提供更多詳細資料這兩個連結的服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="8417c-156">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-156">Dataset properties</span></span>
<span data-ttu-id="8417c-157">資料集 toorepresent toospecify Azure Blob 儲存體中的輸入或輸出資料，設定 hello hello 資料集的類型屬性： **AzureBlob**。</span><span class="sxs-lookup"><span data-stu-id="8417c-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="8417c-158">設定 hello **linkedServiceName**連結服務的 hello Azure 儲存體或 Azure 儲存體 SAS hello 資料集 toohello 名稱的內容。</span><span class="sxs-lookup"><span data-stu-id="8417c-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="8417c-159">hello hello 資料集的類型屬性指定 hello **blob 容器**和 hello**資料夾**hello blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="8417c-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="8417c-160">如 JSON 區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="8417c-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8417c-161">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="8417c-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8417c-162">資料處理站都會支援下列基礎符合 CLS 標準的.NET 型別值提供 「 結構 」 的結構描述上讀取資料來源類似 Azure blob 中的類型資訊的 hello: Int16、 Int32、 Int64、 單一、 Double、 Decimal、 Byte []、 Bool、 字串、 Guid、 Datetime、Datetimeoffset、 Timespan。</span><span class="sxs-lookup"><span data-stu-id="8417c-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="8417c-163">Data Factory 會移動資料的來源資料的資料存放區 tooa 接收資料存放區時，會自動執行類型轉換。</span><span class="sxs-lookup"><span data-stu-id="8417c-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="8417c-164">hello **typeProperties**區段是不同的資料集的每個型別，並提供資訊 hello 位置相關格式等，hello hello 資料儲存區的資料。</span><span class="sxs-lookup"><span data-stu-id="8417c-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="8417c-165">hello typeProperties 區段類型的資料集**AzureBlob**資料集具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="8417c-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="8417c-166">屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-166">Property</span></span> | <span data-ttu-id="8417c-167">說明</span><span class="sxs-lookup"><span data-stu-id="8417c-167">Description</span></span> | <span data-ttu-id="8417c-168">必要</span><span class="sxs-lookup"><span data-stu-id="8417c-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8417c-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="8417c-169">folderPath</span></span> |<span data-ttu-id="8417c-170">路徑 toohello 容器，並且在 hello blob 儲存體中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8417c-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="8417c-171">範例：myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="8417c-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="8417c-172">是</span><span class="sxs-lookup"><span data-stu-id="8417c-172">Yes</span></span> |
| <span data-ttu-id="8417c-173">fileName</span><span class="sxs-lookup"><span data-stu-id="8417c-173">fileName</span></span> |<span data-ttu-id="8417c-174">Hello blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-174">Name of hello blob.</span></span> <span data-ttu-id="8417c-175">fileName 是選擇性的，而且區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="8417c-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="8417c-176">如果您在上指定的檔名、 hello 活動 （包括複製） 運作 hello 特定 Blob。</span><span class="sxs-lookup"><span data-stu-id="8417c-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="8417c-177">若未指定檔名，複本會輸入資料集的 hello folderPath 中包含所有 Blob。</span><span class="sxs-lookup"><span data-stu-id="8417c-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="8417c-178">當**fileName**未指定輸出資料集和**preserveHierarchy**中未指定活動接收 hello hello 產生檔案名稱會在 hello 遵循此格式： 資料。<Guid>。txt (例如:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="8417c-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="8417c-179">否</span><span class="sxs-lookup"><span data-stu-id="8417c-179">No</span></span> |
| <span data-ttu-id="8417c-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="8417c-180">partitionedBy</span></span> |<span data-ttu-id="8417c-181">partitionedBy 是選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="8417c-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="8417c-182">您可以使用它 toospecify 動態 folderPath 和 filename 時間序列資料的。</span><span class="sxs-lookup"><span data-stu-id="8417c-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="8417c-183">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="8417c-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="8417c-184">請參閱 hello[使用 partitionedBy 屬性區段](#using-partitionedBy-property)如需詳細資訊和範例。</span><span class="sxs-lookup"><span data-stu-id="8417c-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="8417c-185">否</span><span class="sxs-lookup"><span data-stu-id="8417c-185">No</span></span> |
| <span data-ttu-id="8417c-186">format</span><span class="sxs-lookup"><span data-stu-id="8417c-186">format</span></span> | <span data-ttu-id="8417c-187">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="8417c-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="8417c-188">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="8417c-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="8417c-189">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="8417c-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="8417c-190">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="8417c-191">否</span><span class="sxs-lookup"><span data-stu-id="8417c-191">No</span></span> |
| <span data-ttu-id="8417c-192">compression</span><span class="sxs-lookup"><span data-stu-id="8417c-192">compression</span></span> | <span data-ttu-id="8417c-193">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="8417c-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="8417c-194">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="8417c-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="8417c-195">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="8417c-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="8417c-196">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="8417c-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="8417c-197">否</span><span class="sxs-lookup"><span data-stu-id="8417c-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="8417c-198">使用 partitionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-198">Using partitionedBy property</span></span>
<span data-ttu-id="8417c-199">當 hello 上一節中所述，您可指定動態 folderPath 和 filename 時間序列資料的 hello **partitionedBy**屬性， [Data Factory 函數與 hello 系統變數](data-factory-functions-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="8417c-200">如需時間序列資料集、排程和配量的詳細資訊，請參閱[建立資料集](data-factory-create-datasets.md)和[排程和執行](data-factory-scheduling-and-execution.md)等文章。</span><span class="sxs-lookup"><span data-stu-id="8417c-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="8417c-201">範例 1</span><span class="sxs-lookup"><span data-stu-id="8417c-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="8417c-202">在此範例中，指定在 hello 格式 (YYYYMMDDHH) 的 Data Factory 系統變數 SliceStart hello 值取代 {Slice}。</span><span class="sxs-lookup"><span data-stu-id="8417c-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="8417c-203">hello SliceStart 是指 toostart hello 配量時間。</span><span class="sxs-lookup"><span data-stu-id="8417c-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="8417c-204">hello folderPath 是不同的每個配量。</span><span class="sxs-lookup"><span data-stu-id="8417c-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="8417c-205">例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="8417c-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="8417c-206">範例 2</span><span class="sxs-lookup"><span data-stu-id="8417c-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="8417c-207">在此範例中，SliceStart 的年、月、日和時間會擷取到 folderPath 和 fileName 屬性所使用的個別變數。</span><span class="sxs-lookup"><span data-stu-id="8417c-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="8417c-208">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-208">Copy activity properties</span></span>
<span data-ttu-id="8417c-209">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="8417c-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8417c-210">屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="8417c-211">而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="8417c-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="8417c-212">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="8417c-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="8417c-213">如果您要移動的資料從 Azure Blob 儲存體，您設定 hello 來源類型 hello 複製活動中太**BlobSource**。</span><span class="sxs-lookup"><span data-stu-id="8417c-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="8417c-214">同樣地，如果您要移動資料 tooan Azure Blob 儲存體，您設定 hello 接收器類型 hello 複製活動中太**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="8417c-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="8417c-215">本節提供 BlobSource 和 BlobSink 支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="8417c-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="8417c-216">**BlobSource**支援下列屬性在 hello hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="8417c-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="8417c-217">屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-217">Property</span></span> | <span data-ttu-id="8417c-218">說明</span><span class="sxs-lookup"><span data-stu-id="8417c-218">Description</span></span> | <span data-ttu-id="8417c-219">允許的值</span><span class="sxs-lookup"><span data-stu-id="8417c-219">Allowed values</span></span> | <span data-ttu-id="8417c-220">必要</span><span class="sxs-lookup"><span data-stu-id="8417c-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8417c-221">遞迴</span><span class="sxs-lookup"><span data-stu-id="8417c-221">recursive</span></span> |<span data-ttu-id="8417c-222">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8417c-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="8417c-223">True (預設值)、False</span><span class="sxs-lookup"><span data-stu-id="8417c-223">True (default value), False</span></span> |<span data-ttu-id="8417c-224">否</span><span class="sxs-lookup"><span data-stu-id="8417c-224">No</span></span> |

<span data-ttu-id="8417c-225">**BlobSink**支援下列屬性的 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="8417c-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="8417c-226">屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-226">Property</span></span> | <span data-ttu-id="8417c-227">說明</span><span class="sxs-lookup"><span data-stu-id="8417c-227">Description</span></span> | <span data-ttu-id="8417c-228">允許的值</span><span class="sxs-lookup"><span data-stu-id="8417c-228">Allowed values</span></span> | <span data-ttu-id="8417c-229">必要</span><span class="sxs-lookup"><span data-stu-id="8417c-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8417c-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="8417c-230">copyBehavior</span></span> |<span data-ttu-id="8417c-231">Hello 來源 BlobSource 或檔案系統時，請定義 hello 複製行為。</span><span class="sxs-lookup"><span data-stu-id="8417c-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="8417c-232"><b>PreserveHierarchy</b>： 保留 hello hello 目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="8417c-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="8417c-233">hello 的來源檔案 toosource 資料夾的相對路徑會是相同 toohello 的目標檔案 tootarget 資料夾的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="8417c-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="8417c-234"><b>FlattenHierarchy</b>: hello 來源資料夾中的所有檔案都位於 hello 第一次層級的目標資料夾。</span><span class="sxs-lookup"><span data-stu-id="8417c-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="8417c-235">hello 目標檔案已自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="8417c-236"><b>MergeFiles</b>： 合併 hello 來源資料夾 tooone 檔案中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="8417c-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="8417c-237">如果指定 hello/Blob 檔案的名稱，則 hello 合併的檔案名稱就是指定之名稱; hello否則，將會自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="8417c-238">否</span><span class="sxs-lookup"><span data-stu-id="8417c-238">No</span></span> |

<span data-ttu-id="8417c-239">**BlobSource** 也支援這兩個屬性以提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="8417c-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="8417c-240">**treatEmptyAsNull**： 指定是否 tootreat null 或空字串視為 null 值。</span><span class="sxs-lookup"><span data-stu-id="8417c-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="8417c-241">**skipHeaderLineCount** - 指定需略過多少行。</span><span class="sxs-lookup"><span data-stu-id="8417c-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="8417c-242">僅適用於輸入資料集使用 TextFormat 時。</span><span class="sxs-lookup"><span data-stu-id="8417c-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="8417c-243">同樣地， **BlobSink**支援 hello 遵循回溯相容性的屬性。</span><span class="sxs-lookup"><span data-stu-id="8417c-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="8417c-244">**blobWriterAddHeader**： 指定是否 tooadd 寫入 tooan 時的資料行定義的標頭輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="8417c-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="8417c-245">下列實作的屬性的資料集現在支援 hello hello 相同的功能： **treatEmptyAsNull**， **skipLineCount**， **firstRowAsHeader**。</span><span class="sxs-lookup"><span data-stu-id="8417c-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="8417c-246">hello 下表提供使用指引來取代這些 blob 來源/接收器屬性 hello 新資料集屬性。</span><span class="sxs-lookup"><span data-stu-id="8417c-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="8417c-247">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-247">Copy Activity property</span></span> | <span data-ttu-id="8417c-248">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="8417c-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="8417c-249">BlobSource 上的 skipHeaderLineCount</span><span class="sxs-lookup"><span data-stu-id="8417c-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="8417c-250">skipLineCount 和 firstRowAsHeader。</span><span class="sxs-lookup"><span data-stu-id="8417c-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="8417c-251">線條會略過第一次，然後做為標頭讀取 hello 第一個資料列。</span><span class="sxs-lookup"><span data-stu-id="8417c-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="8417c-252">BlobSource 上的 treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="8417c-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="8417c-253">輸入資料集上的 treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="8417c-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="8417c-254">BlobSink 上的 blobWriterAddHeader</span><span class="sxs-lookup"><span data-stu-id="8417c-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="8417c-255">輸出資料集上的 firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="8417c-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="8417c-256">如需這些屬性的詳細資訊，請參閱 [指定 TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) 一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="8417c-257">遞迴和 copyBehavior 範例</span><span class="sxs-lookup"><span data-stu-id="8417c-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="8417c-258">本章節描述 hello hello 複製作業，針對遞迴和 copyBehavior 值的不同組合產生的行為。</span><span class="sxs-lookup"><span data-stu-id="8417c-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="8417c-259">遞迴</span><span class="sxs-lookup"><span data-stu-id="8417c-259">recursive</span></span> | <span data-ttu-id="8417c-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="8417c-260">copyBehavior</span></span> | <span data-ttu-id="8417c-261">產生的行為</span><span class="sxs-lookup"><span data-stu-id="8417c-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8417c-262">true</span><span class="sxs-lookup"><span data-stu-id="8417c-262">true</span></span> |<span data-ttu-id="8417c-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="8417c-263">preserveHierarchy</span></span> |<span data-ttu-id="8417c-264">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="8417c-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="8417c-265">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-265">Folder1</span></span><br/><span data-ttu-id="8417c-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8417c-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8417c-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8417c-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8417c-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="8417c-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8417c-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8417c-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8417c-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8417c-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8417c-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8417c-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8417c-272">hello 目標資料夾 Folder1 建立以相同結構為 hello 來源 hello</span><span class="sxs-lookup"><span data-stu-id="8417c-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="8417c-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-273">Folder1</span></span><br/><span data-ttu-id="8417c-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8417c-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8417c-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8417c-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8417c-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="8417c-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8417c-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8417c-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8417c-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8417c-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8417c-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8417c-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="8417c-280">true</span><span class="sxs-lookup"><span data-stu-id="8417c-280">true</span></span> |<span data-ttu-id="8417c-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="8417c-281">flattenHierarchy</span></span> |<span data-ttu-id="8417c-282">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="8417c-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="8417c-283">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-283">Folder1</span></span><br/><span data-ttu-id="8417c-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8417c-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8417c-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8417c-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8417c-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="8417c-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8417c-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8417c-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8417c-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8417c-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8417c-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8417c-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8417c-290">使用下列結構的 hello 建立 hello 目標 Folder1:</span><span class="sxs-lookup"><span data-stu-id="8417c-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="8417c-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-291">Folder1</span></span><br/><span data-ttu-id="8417c-292">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="8417c-293">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="8417c-294">&nbsp;&nbsp;&nbsp;&nbsp;File3 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="8417c-295">&nbsp;&nbsp;&nbsp;&nbsp;File4 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="8417c-296">&nbsp;&nbsp;&nbsp;&nbsp;File5 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="8417c-297">true</span><span class="sxs-lookup"><span data-stu-id="8417c-297">true</span></span> |<span data-ttu-id="8417c-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="8417c-298">mergeFiles</span></span> |<span data-ttu-id="8417c-299">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="8417c-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="8417c-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-300">Folder1</span></span><br/><span data-ttu-id="8417c-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8417c-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8417c-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8417c-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8417c-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="8417c-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8417c-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8417c-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8417c-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8417c-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8417c-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8417c-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8417c-307">使用下列結構的 hello 建立 hello 目標 Folder1:</span><span class="sxs-lookup"><span data-stu-id="8417c-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="8417c-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-308">Folder1</span></span><br/><span data-ttu-id="8417c-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 的內容會合併成一個檔案，並有自動產生的檔案名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="8417c-310">false</span><span class="sxs-lookup"><span data-stu-id="8417c-310">false</span></span> |<span data-ttu-id="8417c-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="8417c-311">preserveHierarchy</span></span> |<span data-ttu-id="8417c-312">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="8417c-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="8417c-313">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-313">Folder1</span></span><br/><span data-ttu-id="8417c-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8417c-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8417c-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8417c-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8417c-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="8417c-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8417c-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8417c-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8417c-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8417c-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8417c-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8417c-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8417c-320">使用下列結構的 hello 建立 hello 目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="8417c-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-321">Folder1</span></span><br/><span data-ttu-id="8417c-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8417c-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8417c-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8417c-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="8417c-324">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="8417c-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="8417c-325">false</span><span class="sxs-lookup"><span data-stu-id="8417c-325">false</span></span> |<span data-ttu-id="8417c-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="8417c-326">flattenHierarchy</span></span> |<span data-ttu-id="8417c-327">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="8417c-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="8417c-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-328">Folder1</span></span><br/><span data-ttu-id="8417c-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8417c-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8417c-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8417c-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8417c-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="8417c-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8417c-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8417c-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8417c-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8417c-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8417c-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8417c-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8417c-335">使用下列結構的 hello 建立 hello 目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="8417c-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-336">Folder1</span></span><br/><span data-ttu-id="8417c-337">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="8417c-338">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="8417c-339">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="8417c-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="8417c-340">false</span><span class="sxs-lookup"><span data-stu-id="8417c-340">false</span></span> |<span data-ttu-id="8417c-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="8417c-341">mergeFiles</span></span> |<span data-ttu-id="8417c-342">來源資料夾 Folder1 以 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="8417c-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="8417c-343">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-343">Folder1</span></span><br/><span data-ttu-id="8417c-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="8417c-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="8417c-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="8417c-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="8417c-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="8417c-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="8417c-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="8417c-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="8417c-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="8417c-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="8417c-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="8417c-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="8417c-350">使用下列結構的 hello 建立 hello 目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="8417c-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="8417c-351">Folder1</span></span><br/><span data-ttu-id="8417c-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 的內容會合併成一個檔案，並有自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="8417c-353">File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="8417c-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="8417c-354">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="8417c-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="8417c-355">逐步解說： 使用複製精靈 toocopy 資料，從 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="8417c-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="8417c-356">讓我們看看如何 tooquickly 複製資料，從 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8417c-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="8417c-357">在這個逐步解說中，來源和目的地資料存放區的類型都是：Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8417c-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="8417c-358">hello 管線，在此逐步解說中的資料複製 tooanother 資料夾 hello 中相同的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="8417c-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="8417c-359">這個逐步解說是刻意簡單 tooshow 您的設定或使用 Blob 儲存體做為來源或接收器的屬性。</span><span class="sxs-lookup"><span data-stu-id="8417c-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="8417c-360">必要條件</span><span class="sxs-lookup"><span data-stu-id="8417c-360">Prerequisites</span></span>
1. <span data-ttu-id="8417c-361">建立一個一般用途的「Azure 儲存體帳戶」(如果您還沒有此帳戶)。</span><span class="sxs-lookup"><span data-stu-id="8417c-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="8417c-362">您同時使用 hello blob 儲存體**來源**和**目的地**資料儲存在這個逐步解說。</span><span class="sxs-lookup"><span data-stu-id="8417c-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="8417c-363">如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)步驟 toocreate 其中一個發行項。</span><span class="sxs-lookup"><span data-stu-id="8417c-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="8417c-364">建立名為的 blob 容器**adfblobconnector** hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="8417c-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="8417c-365">建立名為的資料夾**輸入**在 hello **adfblobconnector**容器。</span><span class="sxs-lookup"><span data-stu-id="8417c-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="8417c-366">建立名為**emp.txt**以 hello 下列內容，並將它上傳 toohello**輸入**資料夾使用工具，像是[Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="8417c-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="8417c-367">建立 hello 資料處理站</span><span class="sxs-lookup"><span data-stu-id="8417c-367">Create hello data factory</span></span>
1. <span data-ttu-id="8417c-368">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8417c-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8417c-369">按一下**+ 新增**從 hello 左上角，按一下 **智慧 + 分析**，然後按一下**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="8417c-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="8417c-370">在 hello**新的 data factory**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="8417c-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="8417c-371">輸入**ADFBlobConnectorDF** hello**名稱**。</span><span class="sxs-lookup"><span data-stu-id="8417c-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="8417c-372">hello hello Azure data factory 的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="8417c-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="8417c-373">如果您收到 hello 錯誤： `*Data factory name “ADFBlobConnectorDF” is not available`、 變更 hello hello data factory (例如，yournameADFBlobConnectorDF) 名稱，然後再次嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="8417c-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="8417c-374">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="8417c-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="8417c-375">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8417c-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="8417c-376">資源群組，請選取**使用現有**tooselect 現有資源群組 （或） 選取**建立新**tooenter 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="8417c-377">選取**位置**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="8417c-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="8417c-378">選取**Pin toodashboard**在 hello hello 刀鋒視窗底部的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="8417c-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="8417c-379">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8417c-379">Click **Create**.</span></span>
3. <span data-ttu-id="8417c-380">Hello 建立完成之後，您會看到 hello **Data Factory**刀鋒視窗中 hello 下列影像所示：![資料 factory 首頁](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="8417c-381">複製精靈</span><span class="sxs-lookup"><span data-stu-id="8417c-381">Copy Wizard</span></span>
1. <span data-ttu-id="8417c-382">在 hello Data Factory 首頁上，按一下 hello**複製資料 [預覽]**磚 toolaunch**複製資料精靈**個別索引標籤中。</span><span class="sxs-lookup"><span data-stu-id="8417c-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="8417c-383">如果您看到該 hello 網頁瀏覽器卡在 [授權]，停用/取消核取**封鎖第三方 cookie 和站台資料**設定 （或） 保留啟用它，並建立的例外狀況**login.microsoftonline.com**，然後再次嘗試重新啟動 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="8417c-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="8417c-384">在 hello**屬性**頁面：</span><span class="sxs-lookup"><span data-stu-id="8417c-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="8417c-385">針對 [工作名稱]，輸入 **CopyPipeline**。</span><span class="sxs-lookup"><span data-stu-id="8417c-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="8417c-386">hello 工作名稱是您的 data factory 中的 hello 管線 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="8417c-387">輸入**描述**hello 工作 （選擇性）。</span><span class="sxs-lookup"><span data-stu-id="8417c-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="8417c-388">如**工作韻律或工作排程**，保留 hello**排程定期執行**選項。</span><span class="sxs-lookup"><span data-stu-id="8417c-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="8417c-389">如果您想的 toorun 排程重複執行此工作一次，而不是，選取**執行一次，就**。</span><span class="sxs-lookup"><span data-stu-id="8417c-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="8417c-390">如果您選取 [立即執行一次] 選項，系統就會建立一個[單次管線](data-factory-create-pipelines.md#onetime-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="8417c-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="8417c-391">保留 hello 設定**週期性模式**。</span><span class="sxs-lookup"><span data-stu-id="8417c-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="8417c-392">這項工作執行每日之間 hello 的開始和結束時間您指定 hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="8417c-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="8417c-393">變更 hello**的開始日期時間**太**04/21/2017年**。</span><span class="sxs-lookup"><span data-stu-id="8417c-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="8417c-394">變更 hello**結束日期時間**太**04/25/2017年**。</span><span class="sxs-lookup"><span data-stu-id="8417c-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="8417c-395">您可能想 tootype hello 日期，而不是瀏覽 hello 行事曆。</span><span class="sxs-lookup"><span data-stu-id="8417c-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="8417c-396">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8417c-396">Click **Next**.</span></span>
      <span data-ttu-id="8417c-397">![複製工具 - 屬性頁面](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="8417c-398">在 hello**來源資料存放區**頁面上，按一下**Azure Blob 儲存體**磚。</span><span class="sxs-lookup"><span data-stu-id="8417c-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="8417c-399">您可以使用這個頁面 toospecify hello 來源資料存放區 hello 複製工作。</span><span class="sxs-lookup"><span data-stu-id="8417c-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="8417c-400">您可以使用現有的資料存放區連結服務或指定新的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="8417c-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="8417c-401">toouse 現有連結服務，您就必須選取**從現有連結的服務**和選取 hello 右邊的連結的服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="8417c-402">![複製工具 - 來源資料存放區頁面](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="8417c-403">在 hello**指定 hello Azure Blob 儲存體帳戶**頁面：</span><span class="sxs-lookup"><span data-stu-id="8417c-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="8417c-404">保留 hello 自動產生名稱為**連接名稱**。</span><span class="sxs-lookup"><span data-stu-id="8417c-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="8417c-405">hello 連接名稱是 hello hello 連結服務類型的名稱： Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8417c-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="8417c-406">確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。</span><span class="sxs-lookup"><span data-stu-id="8417c-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="8417c-407">針對 [Azure 訂用帳戶]，選取您的 Azure 訂用帳戶或保留 [全選]。</span><span class="sxs-lookup"><span data-stu-id="8417c-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="8417c-408">選取**Azure 儲存體帳戶**從 hello hello 選取訂用帳戶中可使用的清單中的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8417c-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="8417c-409">您也可以選擇 tooenter 儲存體帳戶設定手動選取**手動輸入**選項 hello**帳戶選取方法**。</span><span class="sxs-lookup"><span data-stu-id="8417c-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="8417c-410">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8417c-410">Click **Next**.</span></span> 
      <span data-ttu-id="8417c-411">![複製工具-指定 hello Azure Blob 儲存體帳戶](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="8417c-412">在**選擇 hello 輸入的檔案或資料夾**頁面：</span><span class="sxs-lookup"><span data-stu-id="8417c-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="8417c-413">按兩下 [adfblobcontainer]。</span><span class="sxs-lookup"><span data-stu-id="8417c-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="8417c-414">選取 [input]，然後按一下 [選擇]。</span><span class="sxs-lookup"><span data-stu-id="8417c-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="8417c-415">在本逐步解說，您可以選取 hello 輸入的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8417c-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="8417c-416">您也可以改為選取 hello 資料夾 hello emp.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="8417c-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="8417c-417">![複製工具-選擇 hello 輸入的檔案或資料夾](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="8417c-418">在 hello**選擇 hello 輸入的檔案或資料夾**頁面：</span><span class="sxs-lookup"><span data-stu-id="8417c-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="8417c-419">確認該 hello**檔案或資料夾**設定得**adfblobconnector/輸入**。</span><span class="sxs-lookup"><span data-stu-id="8417c-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="8417c-420">如果 hello 檔案子資料夾中，比方說，2017年/04/01、 2017年/04/02 等等，請輸入 adfblobconnector/輸入 / {year} / {month} / {day} 檔案或資料夾。</span><span class="sxs-lookup"><span data-stu-id="8417c-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="8417c-421">當您按下 TAB 鍵超出 hello 文字方塊中時，您會看到三個下拉式清單 tooselect 格式的年份 (yyyy)、 month (MM) 和一天 (dd)。</span><span class="sxs-lookup"><span data-stu-id="8417c-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="8417c-422">請勿設定 [以遞迴方式複製檔案]。</span><span class="sxs-lookup"><span data-stu-id="8417c-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="8417c-423">選取此選項 toorecursively 周遊，透過檔案 toobe 複製的 toohello 目的地的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8417c-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="8417c-424">不執行 hello**二進位複製**選項。</span><span class="sxs-lookup"><span data-stu-id="8417c-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="8417c-425">選取此選項 tooperform 二進位的來源檔案 toohello 目的複本。</span><span class="sxs-lookup"><span data-stu-id="8417c-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="8417c-426">未選取此逐步解說中，讓您可以查看更多的 hello 接下來的頁面選項。</span><span class="sxs-lookup"><span data-stu-id="8417c-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="8417c-427">確認該 hello**壓縮類型**設定得**無**。</span><span class="sxs-lookup"><span data-stu-id="8417c-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="8417c-428">如果您的來源檔案會壓縮其中一種支援的 hello 格式，請選取這個選項的值。</span><span class="sxs-lookup"><span data-stu-id="8417c-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="8417c-429">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8417c-429">Click **Next**.</span></span>
    <span data-ttu-id="8417c-430">![複製工具-選擇 hello 輸入的檔案或資料夾](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="8417c-431">在 hello**檔案格式設定** 頁面上，您會看到 hello 分隔符號和是藉由剖析 hello 檔案的 自動偵測到的 hello 精靈的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="8417c-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="8417c-432">確認 hello 下列選項：。</span><span class="sxs-lookup"><span data-stu-id="8417c-432">Confirm hello following options: a.</span></span> <span data-ttu-id="8417c-433">hello**檔案格式**設定得**文字格式**。</span><span class="sxs-lookup"><span data-stu-id="8417c-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="8417c-434">您可以查看所有支援的 hello 格式 hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="8417c-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="8417c-435">例如：JSON、Avro、ORC、Parquet。</span><span class="sxs-lookup"><span data-stu-id="8417c-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="8417c-436">b.</span><span class="sxs-lookup"><span data-stu-id="8417c-436">b.</span></span> <span data-ttu-id="8417c-437">hello**資料行分隔符號**設定得`Comma (,)`。</span><span class="sxs-lookup"><span data-stu-id="8417c-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="8417c-438">您可以看到 hello hello 下拉式清單中的 Data Factory 支援其他資料行分隔符號。</span><span class="sxs-lookup"><span data-stu-id="8417c-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="8417c-439">您也可以指定自訂的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="8417c-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="8417c-440">c.</span><span class="sxs-lookup"><span data-stu-id="8417c-440">c.</span></span> <span data-ttu-id="8417c-441">hello**資料列分隔符號**設定得`Carriage Return + Line feed (\r\n)`。</span><span class="sxs-lookup"><span data-stu-id="8417c-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="8417c-442">您可以看到 hello hello 下拉式清單中的 Data Factory 支援其他資料列分隔符號。</span><span class="sxs-lookup"><span data-stu-id="8417c-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="8417c-443">您也可以指定自訂的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="8417c-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="8417c-444">d.</span><span class="sxs-lookup"><span data-stu-id="8417c-444">d.</span></span> <span data-ttu-id="8417c-445">hello**略過行數**設定得**0**。</span><span class="sxs-lookup"><span data-stu-id="8417c-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="8417c-446">如果您想略過在 hello hello 檔案最上方的幾行 toobe，輸入 hello 數字。</span><span class="sxs-lookup"><span data-stu-id="8417c-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="8417c-447">e.</span><span class="sxs-lookup"><span data-stu-id="8417c-447">e.</span></span>  <span data-ttu-id="8417c-448">hello**第一個資料列包含資料行名稱**未設定。</span><span class="sxs-lookup"><span data-stu-id="8417c-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="8417c-449">如果 hello 原始程式檔包含 hello 第一個資料列中的資料行名稱，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="8417c-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="8417c-450">f.</span><span class="sxs-lookup"><span data-stu-id="8417c-450">f.</span></span> <span data-ttu-id="8417c-451">hello**空的資料行值視為 null**選項設定。</span><span class="sxs-lookup"><span data-stu-id="8417c-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="8417c-452">展開**進階設定**toosee 進階可用的選項。</span><span class="sxs-lookup"><span data-stu-id="8417c-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="8417c-453">在 hello hello 頁面底部，請參閱 hello**預覽**的 hello emp.txt 檔中的資料。</span><span class="sxs-lookup"><span data-stu-id="8417c-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="8417c-454">按一下**結構描述**hello 底部 toosee hello 結構描述推斷藉由在 hello 資料 hello 原始程式檔中查看該 hello 複製精靈 」 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8417c-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="8417c-455">按一下**下一步**在檢閱 hello 分隔符號和預覽資料。</span><span class="sxs-lookup"><span data-stu-id="8417c-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="8417c-456">![複製工具 - 檔案格式設定](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="8417c-457">在 hello**目的地資料存放區頁面**，選取**Azure Blob 儲存體**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8417c-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="8417c-458">您正在使用 hello Azure Blob 儲存體，以在此逐步解說中這兩個 hello 來源和目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="8417c-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="8417c-459">![複製精靈 - 選取目的地資料存放區](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="8417c-460">在**指定 hello Azure Blob 儲存體帳戶**頁面：</span><span class="sxs-lookup"><span data-stu-id="8417c-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="8417c-461">輸入**AzureStorageLinkedService** hello**連接名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="8417c-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="8417c-462">確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。</span><span class="sxs-lookup"><span data-stu-id="8417c-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="8417c-463">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8417c-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="8417c-464">選取您的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8417c-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="8417c-465">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8417c-465">Click **Next**.</span></span>     
10. <span data-ttu-id="8417c-466">在 hello**選擇 hello 輸出檔案或資料夾**頁面：</span><span class="sxs-lookup"><span data-stu-id="8417c-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="8417c-467">將 [資料夾路徑] 指定為 **adfblobconnector/output/{year}/{month}/{day}**。</span><span class="sxs-lookup"><span data-stu-id="8417c-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="8417c-468">輸入 **TAB**。</span><span class="sxs-lookup"><span data-stu-id="8417c-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="8417c-469">Hello**年**，選取**yyyy**。</span><span class="sxs-lookup"><span data-stu-id="8417c-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="8417c-470">Hello**月份**，確認已設定太**公釐**。</span><span class="sxs-lookup"><span data-stu-id="8417c-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="8417c-471">Hello**天**，確認已設定太**dd**。</span><span class="sxs-lookup"><span data-stu-id="8417c-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="8417c-472">確認該 hello**壓縮類型**設定得**無**。</span><span class="sxs-lookup"><span data-stu-id="8417c-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="8417c-473">確認該 hello**複製行為**設定得**合併檔案**。</span><span class="sxs-lookup"><span data-stu-id="8417c-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="8417c-474">如果 hello 輸出檔案具有相同的名稱已存在的 hello，hello 新內容也會加入的 toohello 相同檔案 hello 結尾。</span><span class="sxs-lookup"><span data-stu-id="8417c-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="8417c-475">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8417c-475">Click **Next**.</span></span>
    <span data-ttu-id="8417c-476">![複製工具 - 選擇輸出檔案或資料夾](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="8417c-477">在 hello**檔案格式設定**頁面上，檢閱 hello 設定，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8417c-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="8417c-478">這裡 hello 其他選項的其中一個是 tooadd 標頭 toohello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="8417c-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="8417c-479">如果您選取該選項時，標頭資料列會加入與 hello 資料行的名稱，從 hello hello 來源結構描述。</span><span class="sxs-lookup"><span data-stu-id="8417c-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="8417c-480">檢視 hello hello 來源結構描述時，您可以重新命名 hello 預設資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="8417c-481">例如，您可以變更第一個資料行 tooFirst hello 名稱和第二個資料行 tooLast 名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="8417c-482">然後，hello 產生輸出檔案具有標頭，與這些名稱當做資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="8417c-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="8417c-483">![複製工具 - 目的地的檔案格式設定](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="8417c-484">在 hello**效能設定**頁面上，確認**雲端單位**和**平行複製**設定得**自動**，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="8417c-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="8417c-485">如需有關這些設定的詳細資料，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md#parallel-copy)。</span><span class="sxs-lookup"><span data-stu-id="8417c-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="8417c-486">![複製工具 - 效能設定](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="8417c-487">在 hello**摘要**頁面上，檢閱所有設定 （工作內容、 設定來源和目的地，並複製設定值），然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8417c-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="8417c-488">![複製工具 - 摘要頁面](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="8417c-489">檢閱資訊在 hello**摘要**頁面，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="8417c-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="8417c-490">hello 精靈會建立兩個連結的服務、 兩個資料集 （輸入與輸出），以及一個管線 （從啟動 hello 複製精靈 」 的位置） 的 hello data factory 中。</span><span class="sxs-lookup"><span data-stu-id="8417c-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="8417c-491">![複製工具 - 部署頁面](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="8417c-492">監視 hello 管線 （複製工作）</span><span class="sxs-lookup"><span data-stu-id="8417c-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="8417c-493">按一下 hello 連結`Click here toomonitor copy pipeline`上 hello**部署**頁面。</span><span class="sxs-lookup"><span data-stu-id="8417c-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="8417c-494">您應該會看見 hello**監視和管理應用程式**個別索引標籤中。![監視及管理應用程式](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="8417c-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="8417c-495">變更 hello**啟動**太時間 hello 頂端`04/19/2017`和**結束**時間太`04/27/2017`，然後按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="8417c-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="8417c-496">您應該會看到五個活動 windows hello 中的**活動 WINDOWS**清單。</span><span class="sxs-lookup"><span data-stu-id="8417c-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="8417c-497">hello **WindowStart**時間應該涵蓋所有日從管線開始 toopipeline 結束時間。</span><span class="sxs-lookup"><span data-stu-id="8417c-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="8417c-498">按一下**重新整理**按鈕 hello**活動 WINDOWS** tooReady 設定幾次，直到您看到所有的 hello 活動 windows hello 狀態的清單。</span><span class="sxs-lookup"><span data-stu-id="8417c-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="8417c-499">現在，確認 hello 輸出檔會產生 adfblobconnector 容器 hello 輸出資料夾中。</span><span class="sxs-lookup"><span data-stu-id="8417c-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="8417c-500">您應該會看到下列資料夾結構 hello 輸出資料夾中的 hello:</span><span class="sxs-lookup"><span data-stu-id="8417c-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="8417c-501">如需有關監視及管理 Data Factory 的詳細資訊，請參閱[監視和管理 Data Factory 管線](data-factory-monitor-manage-app.md)一文。</span><span class="sxs-lookup"><span data-stu-id="8417c-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="8417c-502">Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="8417c-502">Data Factory entities</span></span>
<span data-ttu-id="8417c-503">現在，請切換後 toohello hello Data Factory 首頁索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8417c-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="8417c-504">請注意，您的 Data Factory 現在有兩個已連結的服務、兩個資料集，以及一條管線。</span><span class="sxs-lookup"><span data-stu-id="8417c-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![含有實體的 Data Factory 首頁](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="8417c-506">按一下**作者及部署**toolaunch Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="8417c-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Data Factory 編輯器](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="8417c-508">您應該會看到下列 data factory 中的 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="8417c-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="8417c-509">兩個已連結的服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-509">Two linked services.</span></span> <span data-ttu-id="8417c-510">其中一個 hello 來源和目的地 hello hello 另一個。</span><span class="sxs-lookup"><span data-stu-id="8417c-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="8417c-511">這兩個 hello 連結服務，請參閱 toohello 在本逐步解說的相同 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8417c-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="8417c-512">兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="8417c-512">Two datasets.</span></span> <span data-ttu-id="8417c-513">一個輸入資料集和一個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="8417c-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="8417c-514">在本逐步解說中，都使用 hello 相同 blob 容器，但是參考 toodifferent 資料夾 （輸入與輸出）。</span><span class="sxs-lookup"><span data-stu-id="8417c-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="8417c-515">一條管線。</span><span class="sxs-lookup"><span data-stu-id="8417c-515">A pipeline.</span></span> <span data-ttu-id="8417c-516">hello 管線包含複製活動會使用 blob 來源和 blob 接收 toocopy 資料從 Azure blob 位置 tooanother Azure blob 的位置。</span><span class="sxs-lookup"><span data-stu-id="8417c-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="8417c-517">hello 下列各節提供有關這些實體的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8417c-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="8417c-518">連結的服務</span><span class="sxs-lookup"><span data-stu-id="8417c-518">Linked services</span></span>
<span data-ttu-id="8417c-519">您應該會看到兩個已連結的服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-519">You should see two linked services.</span></span> <span data-ttu-id="8417c-520">其中一個 hello 來源和目的地 hello hello 另一個。</span><span class="sxs-lookup"><span data-stu-id="8417c-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="8417c-521">在本逐步解說中，這兩個定義外觀 hello 相同 hello 名稱除外。</span><span class="sxs-lookup"><span data-stu-id="8417c-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="8417c-522">hello**類型**hello 連結的服務已設定太**AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="8417c-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="8417c-523">Hello 連結服務定義的最重要的屬性為 hello **connectionString**，這由 Data Factory tooconnect tooyour 在執行階段的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8417c-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="8417c-524">忽略 hello 定義中的 hello hubName 屬性。</span><span class="sxs-lookup"><span data-stu-id="8417c-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="8417c-525">來源 Blob 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="8417c-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="8417c-526">目的地 Blob 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="8417c-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="8417c-527">如需有關「Azure 儲存體」連結服務的詳細資訊，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="8417c-528">資料集</span><span class="sxs-lookup"><span data-stu-id="8417c-528">Datasets</span></span>
<span data-ttu-id="8417c-529">有兩個資料集：一個輸入資料集和一個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="8417c-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="8417c-530">hello 資料集的 hello 類型設定得**AzureBlob**兩者。</span><span class="sxs-lookup"><span data-stu-id="8417c-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="8417c-531">輸入資料集 hello 點 toohello**輸入**資料夾 hello **adfblobconnector** blob 容器。</span><span class="sxs-lookup"><span data-stu-id="8417c-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="8417c-532">hello**外部**屬性設定太**true** hello 為此資料集的資料就不會產生 hello 管線與 hello 複製活動會做為輸入此資料集。</span><span class="sxs-lookup"><span data-stu-id="8417c-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="8417c-533">hello 輸出資料集點 toohello**輸出**hello 資料夾相同的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="8417c-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="8417c-534">hello 輸出資料集也會使用 hello 年、 月和日的 hello **SliceStart**系統變數 toodynamically 評估 hello hello 輸出檔的路徑。</span><span class="sxs-lookup"><span data-stu-id="8417c-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="8417c-535">如需 Data Factory 所支援的函式與系統變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="8417c-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="8417c-536">hello**外部**屬性設定太**false** （預設值） 因為此資料集由 hello 管線所產生。</span><span class="sxs-lookup"><span data-stu-id="8417c-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="8417c-537">如需有關 Azure Blob 資料集所支援屬性的詳細資訊，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="8417c-538">輸入資料集</span><span class="sxs-lookup"><span data-stu-id="8417c-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="8417c-539">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="8417c-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="8417c-540">管線</span><span class="sxs-lookup"><span data-stu-id="8417c-540">Pipeline</span></span>
<span data-ttu-id="8417c-541">hello 管線有一個活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="8417c-542">hello**類型**hello 活動已設定太**複製**。</span><span class="sxs-lookup"><span data-stu-id="8417c-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="8417c-543">在 hello hello 活動的類型屬性，有兩個區段，另一個用於來源和接收另一個 hello。</span><span class="sxs-lookup"><span data-stu-id="8417c-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="8417c-544">hello 來源類型會設定太**BlobSource**為 hello 活動正在將資料複製從 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8417c-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="8417c-545">hello 接收器類型會設定太**BlobSink**作為複製資料 tooa blob 儲存體的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="8417c-546">hello 複製活動採用 InputDataset z4y hello 和當做輸入 OutputDataset-z4y 做為 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="8417c-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="8417c-547">如需有關 BlobSource 和 BlobSink 所支援屬性的詳細資訊，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="8417c-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="8417c-548">從 Blob 儲存體複製資料 tooand JSON 範例</span><span class="sxs-lookup"><span data-stu-id="8417c-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="8417c-549">hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8417c-550">它們會顯示如何從 Azure Blob 儲存體和 Azure SQL Database toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="8417c-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="8417c-551">不過，資料可以複製**直接**從任何來源 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="8417c-552">JSON 範例： 從 Blob 儲存體 tooSQL 資料庫複製資料</span><span class="sxs-lookup"><span data-stu-id="8417c-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="8417c-553">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="8417c-553">hello following sample shows:</span></span>

1. <span data-ttu-id="8417c-554">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="8417c-555">[AzureStorage](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="8417c-556">[AzureBlob](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="8417c-557">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8417c-558">具有使用 [BlobSource](#copy-activity-properties) 和 [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8417c-559">hello 範例從 Azure blob tooan Azure SQL 資料表複製時間序列資料的每小時。</span><span class="sxs-lookup"><span data-stu-id="8417c-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="8417c-560">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="8417c-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="8417c-561">**Azure SQL 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="8417c-561">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="8417c-562">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="8417c-562">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="8417c-563">Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="8417c-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="8417c-564">如 hello 第一個、 指定 hello 連接字串，包含 hello 帳戶金鑰和 hello 更新版本，您可以指定 hello 共用存取簽章 (SAS) Uri。</span><span class="sxs-lookup"><span data-stu-id="8417c-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="8417c-565">請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8417c-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="8417c-566">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="8417c-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="8417c-567">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="8417c-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8417c-568">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="8417c-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8417c-569">年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="8417c-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="8417c-570">"external":"true"的設定會在該 hello 資料表是外部 toohello 資料處理站並不產生 hello data factory 中的活動時通知 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="8417c-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
<span data-ttu-id="8417c-571">**Azure SQL 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="8417c-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="8417c-572">hello 範例複製 Azure SQL database 中名為"MyTable"的資料 tooa 資料表。</span><span class="sxs-lookup"><span data-stu-id="8417c-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="8417c-573">在與您 Azure SQL database 中建立 hello 資料表如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="8417c-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="8417c-574">新的資料列會加入 toohello 資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="8417c-574">New rows are added toohello table every hour.</span></span>

```json
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
<span data-ttu-id="8417c-575">**具有 Blob 來源和 SQL 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="8417c-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="8417c-576">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="8417c-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="8417c-577">在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和**接收**類型設定得**SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="8417c-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
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
            "type": "BlobSource"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="8417c-578">JSON 範例： 將資料複製 Azure SQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="8417c-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="8417c-579">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="8417c-579">hello following sample shows:</span></span>

1. <span data-ttu-id="8417c-580">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="8417c-581">[AzureStorage](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="8417c-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="8417c-582">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8417c-583">[AzureBlob](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="8417c-584">具有使用 [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) 和 [BlobSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="8417c-585">hello 範例從 Azure SQL 資料表 tooan Azure blob 複製時間序列資料的每小時。</span><span class="sxs-lookup"><span data-stu-id="8417c-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="8417c-586">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="8417c-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="8417c-587">**Azure SQL 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="8417c-587">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="8417c-588">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="8417c-588">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="8417c-589">Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="8417c-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="8417c-590">如 hello 第一個、 指定 hello 連接字串，包含 hello 帳戶金鑰和 hello 更新版本，您可以指定 hello 共用存取簽章 (SAS) Uri。</span><span class="sxs-lookup"><span data-stu-id="8417c-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="8417c-591">請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8417c-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="8417c-592">**Azure SQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="8417c-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="8417c-593">hello 範例假設您已建立資料表"MyTable"Azure SQL 中，而且包含稱為 「 timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="8417c-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="8417c-594">設定"external":"true"會通知 Data Factory 服務的 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。</span><span class="sxs-lookup"><span data-stu-id="8417c-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
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

<span data-ttu-id="8417c-595">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="8417c-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8417c-596">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="8417c-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8417c-597">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="8417c-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8417c-598">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="8417c-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
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
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

<span data-ttu-id="8417c-599">**具有 SQL 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="8417c-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="8417c-600">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="8417c-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="8417c-601">在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="8417c-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="8417c-602">指定 hello SQL 查詢**SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="8417c-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
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

> [!NOTE]
> <span data-ttu-id="8417c-603">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="8417c-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8417c-604">效能和微調</span><span class="sxs-lookup"><span data-stu-id="8417c-604">Performance and Tuning</span></span>
<span data-ttu-id="8417c-605">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="8417c-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
