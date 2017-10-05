---
title: "在 Azure Blob 儲存體來回複製資料 | Microsoft Docs"
description: "了解如何在 Azure Data Factory 複製 Blob 資料。 使用我們的範例：如何在 Azure Blob 儲存體和 Azure SQL Database 將資料複製進來和複製出去。"
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
ms.openlocfilehash: 2cf955b52010869a4e753c441e17bdd32fd2e63d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="5554d-105">使用 Azure Data Factory 在 Azure Blob 儲存體來回複製資料</span><span class="sxs-lookup"><span data-stu-id="5554d-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="5554d-106">本文說明如何使用 Azure Data Factory 中的「複製活動」，在 Azure Blob 儲存體來回複製資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="5554d-107">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="5554d-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="5554d-108">概觀</span><span class="sxs-lookup"><span data-stu-id="5554d-108">Overview</span></span>
<span data-ttu-id="5554d-109">您可以將資料從任何支援的來源資料存放區複製到「Azure Blob 儲存體」，或從「Azure Blob 儲存體」複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5554d-109">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="5554d-110">下表提供複製活動所支援作為來源或接收器的資料存放區清單。</span><span class="sxs-lookup"><span data-stu-id="5554d-110">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="5554d-111">例如，您可以將資料**從** SQL Server 資料庫或 Azure SQL Database 移**到** Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5554d-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="5554d-112">而且，您可以將資料「從」 Azure Blob 儲存體複製「到」 Azure SQL 資料倉儲或 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="5554d-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="5554d-113">支援的案例</span><span class="sxs-lookup"><span data-stu-id="5554d-113">Supported scenarios</span></span>
<span data-ttu-id="5554d-114">您可以將資料從 Azure Blob 儲存體儲存到下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="5554d-114">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="5554d-115">您可以從下列資料存放區將資料複製到 Azure Blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="5554d-115">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="5554d-116">複製活動支援在一般用途的 Azure 儲存體帳戶以及經常性存取/非經常性存取 Blob 儲存體來回複製資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-116">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="5554d-117">此活動支援從區塊、附加或分頁 Blob 讀取，但只支援寫入至區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="5554d-117">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="5554d-118">不支援使用「Azure 進階儲存體」作為接收器，因為它是以分頁 Blob 為後盾。</span><span class="sxs-lookup"><span data-stu-id="5554d-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="5554d-119">資料成功複製至目的地後，複製活動不會從來源刪除資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-119">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="5554d-120">如果您需要在成功複製後刪除來源資料，請建立[自訂活動](data-factory-use-custom-activities.md)來刪除資料，然後在管道中使用該活動。</span><span class="sxs-lookup"><span data-stu-id="5554d-120">If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline.</span></span> <span data-ttu-id="5554d-121">如需範例，請參閱 [刪除 GitHub 上的 Blob 或資料夾範例 (英文)](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity)。</span><span class="sxs-lookup"><span data-stu-id="5554d-121">For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="5554d-122">開始使用</span><span class="sxs-lookup"><span data-stu-id="5554d-122">Get started</span></span>
<span data-ttu-id="5554d-123">您可以建立內含複製活動的管線，使用不同的工具/API 將資料移進/移出 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5554d-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="5554d-124">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="5554d-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="5554d-125">這篇文章中有建立管線的[逐步解說](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage)，可將資料從 Azure Blob 儲存體位置複製到另一個 Azure Blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="5554d-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="5554d-126">如需建立管線以將資料從 Azure Blob 儲存體複製到 Azure SQL Database 的教學課程，請參閱[教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-126">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="5554d-127">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="5554d-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5554d-128">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="5554d-129">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="5554d-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="5554d-130">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="5554d-130">Create a **data factory**.</span></span> <span data-ttu-id="5554d-131">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="5554d-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="5554d-132">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="5554d-132">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="5554d-133">例如，如果您將資料從 Azure Blob 儲存體複製到 Azure SQL 資料庫，您會建立兩個連結服務，將 Azure 儲存體帳戶和 Azure SQL 資料庫連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="5554d-133">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="5554d-134">有關 Azure Blob 儲存體專屬的連結服務屬性，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-134">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="5554d-135">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-135">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="5554d-136">在上一個步驟所述的範例中，您可以建立資料集來指定包含輸入資料的 Blob 容器與資料夾。</span><span class="sxs-lookup"><span data-stu-id="5554d-136">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="5554d-137">同時建立另一個資料集來指定 Azure SQL 資料庫中的 SQL 資料表，以保存從 Blob 儲存體複製的資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-137">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="5554d-138">如需 Azure Blob 儲存體專屬的資料集屬性，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-138">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="5554d-139">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="5554d-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="5554d-140">在稍早所述的範例中，您使用 BlobSource 作為來源，以及使用 SqlSink 作為複製活動的接收器。</span><span class="sxs-lookup"><span data-stu-id="5554d-140">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="5554d-141">同樣地，如果您是從 Azure SQL Database 複製到 Azure Blob 儲存體，則在複製活動中使用 SqlSource 和 BlobSink。</span><span class="sxs-lookup"><span data-stu-id="5554d-141">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="5554d-142">針對 Azure Blob 儲存體專屬的複製活動屬性，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-142">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="5554d-143">如需有關如何使用資料存放區作為來源或接收器的詳細資訊，請按一下上一節中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="5554d-143">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="5554d-144">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="5554d-144">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="5554d-145">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="5554d-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="5554d-146">如需相關範例，其中含有用來將資料複製到「Azure Blob 儲存體」(或從「Azure Blob 儲存體」複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples-for-copying-data-to-and-from-blob-storage  )一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-146">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="5554d-147">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Azure Blob 儲存體專屬的 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="5554d-147">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5554d-148">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-148">Linked service properties</span></span>
<span data-ttu-id="5554d-149">您可以使用兩種類型的已連結服務，將「Azure 儲存體」連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="5554d-149">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="5554d-150">它們是：**AzureStorage** 連結服務和 **AzureStorageSas** 連結服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="5554d-151">Azure 儲存體連結服務可將 Azure 儲存體的全域存取權提供給 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="5554d-151">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="5554d-152">而 Azure 儲存體 SAS (共用存取簽章) 連結服務會將 Azure 儲存體的受限制/時間繫結存取權提供給 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="5554d-152">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="5554d-153">這兩個連結服務之間沒有其他差異。</span><span class="sxs-lookup"><span data-stu-id="5554d-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="5554d-154">選擇符合您需求的連結服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-154">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="5554d-155">以下章節提供這兩個連結服務的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-155">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="5554d-156">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-156">Dataset properties</span></span>
<span data-ttu-id="5554d-157">若要指定資料集以代表「Azure Blob 儲存體」中的輸入或輸出資料，您需將資料集的類型屬性設定成：**AzureBlob**。</span><span class="sxs-lookup"><span data-stu-id="5554d-157">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="5554d-158">請將資料集的 **linkedServiceName** 屬性設定成「Azure 儲存體」或「Azure 儲存體 SAS」已連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-158">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="5554d-159">資料集的類型屬性會指定 Blob 儲存體中的「Blob 容器」和「資料夾」。</span><span class="sxs-lookup"><span data-stu-id="5554d-159">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="5554d-160">如需定義資料集的 JSON 區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="5554d-160">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5554d-161">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="5554d-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5554d-162">Data Factory 支援使用下列符合 CLS 規範的 .NET 型類型值，在 “structure” 中針對在讀取時驗證結構描述 (schema-on-read) 的資料來源 (例如 Azure Blob) 提供類型資訊：Int16、Int32、Int64、Single、Double、Decimal、Byte[]、Bool、String、Guid、Datetime、Datetimeoffset、Timespan。</span><span class="sxs-lookup"><span data-stu-id="5554d-162">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="5554d-163">Data Factory 會在將資料從來源資料存放區移到接收資料存放區時，自動執行類型轉換。</span><span class="sxs-lookup"><span data-stu-id="5554d-163">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="5554d-164">每個資料集類型的 **TypeProperties** 區段都不同，可提供資料存放區中資料的位置、格式等相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5554d-164">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="5554d-165">**AzureBlob** 類型資料集的 typeProperties 區段具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="5554d-165">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="5554d-166">屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-166">Property</span></span> | <span data-ttu-id="5554d-167">說明</span><span class="sxs-lookup"><span data-stu-id="5554d-167">Description</span></span> | <span data-ttu-id="5554d-168">必要</span><span class="sxs-lookup"><span data-stu-id="5554d-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5554d-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="5554d-169">folderPath</span></span> |<span data-ttu-id="5554d-170">Blob 儲存體中容器和資料夾的路徑。</span><span class="sxs-lookup"><span data-stu-id="5554d-170">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="5554d-171">範例：myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="5554d-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="5554d-172">是</span><span class="sxs-lookup"><span data-stu-id="5554d-172">Yes</span></span> |
| <span data-ttu-id="5554d-173">fileName</span><span class="sxs-lookup"><span data-stu-id="5554d-173">fileName</span></span> |<span data-ttu-id="5554d-174">Blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-174">Name of the blob.</span></span> <span data-ttu-id="5554d-175">fileName 是選擇性的，而且區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5554d-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="5554d-176">如果您指定檔案名稱，活動 (包括複製) 適用於特定的 Blob。</span><span class="sxs-lookup"><span data-stu-id="5554d-176">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="5554d-177">如果您未指定 fileName，複製會包含 folderPath 中的所有 Blob 以做為輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="5554d-177">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="5554d-178">當沒有為輸出資料集指定 fileName，且沒有為活動接收器指定 preserveHierarchy 時，所產生檔案的名稱會採用此格式：Data.<Guid>.txt (例如 Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="5554d-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="5554d-179">否</span><span class="sxs-lookup"><span data-stu-id="5554d-179">No</span></span> |
| <span data-ttu-id="5554d-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="5554d-180">partitionedBy</span></span> |<span data-ttu-id="5554d-181">partitionedBy 是選擇性的屬性。</span><span class="sxs-lookup"><span data-stu-id="5554d-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="5554d-182">您可以用來指定時間序列資料的動態 folderPath 和 filename。</span><span class="sxs-lookup"><span data-stu-id="5554d-182">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="5554d-183">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="5554d-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="5554d-184">如需詳細資訊和範例，請參閱 [使用 partitionedBy 屬性](#using-partitionedBy-property) 一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-184">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="5554d-185">否</span><span class="sxs-lookup"><span data-stu-id="5554d-185">No</span></span> |
| <span data-ttu-id="5554d-186">format</span><span class="sxs-lookup"><span data-stu-id="5554d-186">format</span></span> | <span data-ttu-id="5554d-187">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="5554d-187">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="5554d-188">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="5554d-188">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="5554d-189">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="5554d-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="5554d-190">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="5554d-190">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="5554d-191">否</span><span class="sxs-lookup"><span data-stu-id="5554d-191">No</span></span> |
| <span data-ttu-id="5554d-192">compression</span><span class="sxs-lookup"><span data-stu-id="5554d-192">compression</span></span> | <span data-ttu-id="5554d-193">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="5554d-193">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="5554d-194">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="5554d-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="5554d-195">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="5554d-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="5554d-196">如需詳細資訊，請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="5554d-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="5554d-197">否</span><span class="sxs-lookup"><span data-stu-id="5554d-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="5554d-198">使用 partitionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-198">Using partitionedBy property</span></span>
<span data-ttu-id="5554d-199">如上一節所述，您可以使用 **partitionedBy** 屬性、[Data Factory 函式及系統變數](data-factory-functions-variables.md)，來指定時間序列資料的動態 folderPath 和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-199">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="5554d-200">如需時間序列資料集、排程和配量的詳細資訊，請參閱[建立資料集](data-factory-create-datasets.md)和[排程和執行](data-factory-scheduling-and-execution.md)等文章。</span><span class="sxs-lookup"><span data-stu-id="5554d-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="5554d-201">範例 1</span><span class="sxs-lookup"><span data-stu-id="5554d-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="5554d-202">在此範例中，{Slice} 會取代成 Data Factory 系統變數 SliceStart 的值 (使用指定的格式 (YYYYMMDDHH))。</span><span class="sxs-lookup"><span data-stu-id="5554d-202">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="5554d-203">SliceStart 是指配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="5554d-203">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="5554d-204">每個配量的 folderPath 都不同。</span><span class="sxs-lookup"><span data-stu-id="5554d-204">The folderPath is different for each slice.</span></span> <span data-ttu-id="5554d-205">例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="5554d-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="5554d-206">範例 2</span><span class="sxs-lookup"><span data-stu-id="5554d-206">Sample 2</span></span>

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

<span data-ttu-id="5554d-207">在此範例中，SliceStart 的年、月、日和時間會擷取到 folderPath 和 fileName 屬性所使用的個別變數。</span><span class="sxs-lookup"><span data-stu-id="5554d-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="5554d-208">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-208">Copy activity properties</span></span>
<span data-ttu-id="5554d-209">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="5554d-209">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5554d-210">屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="5554d-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="5554d-211">而活動的 **typeProperties** 區段中，可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5554d-211">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="5554d-212">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5554d-212">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="5554d-213">如果您要將資料從 Azure Blob 儲存體移出，請將複製活動中的來源類型設定為 **BlobSource**。</span><span class="sxs-lookup"><span data-stu-id="5554d-213">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="5554d-214">同樣地，如果您要將資料移入 Azure Blob 儲存體，請將複製活動中的接收類型設定為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="5554d-214">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="5554d-215">本節提供 BlobSource 和 BlobSink 支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="5554d-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="5554d-216">**BlobSource** 在 **typeProperties** 區段中支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="5554d-216">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="5554d-217">屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-217">Property</span></span> | <span data-ttu-id="5554d-218">說明</span><span class="sxs-lookup"><span data-stu-id="5554d-218">Description</span></span> | <span data-ttu-id="5554d-219">允許的值</span><span class="sxs-lookup"><span data-stu-id="5554d-219">Allowed values</span></span> | <span data-ttu-id="5554d-220">必要</span><span class="sxs-lookup"><span data-stu-id="5554d-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5554d-221">遞迴</span><span class="sxs-lookup"><span data-stu-id="5554d-221">recursive</span></span> |<span data-ttu-id="5554d-222">表示是否從子資料夾，或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-222">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="5554d-223">True (預設值)、False</span><span class="sxs-lookup"><span data-stu-id="5554d-223">True (default value), False</span></span> |<span data-ttu-id="5554d-224">否</span><span class="sxs-lookup"><span data-stu-id="5554d-224">No</span></span> |

<span data-ttu-id="5554d-225">**BlobSink** 在 **typeProperties** 區段中支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="5554d-225">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="5554d-226">屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-226">Property</span></span> | <span data-ttu-id="5554d-227">說明</span><span class="sxs-lookup"><span data-stu-id="5554d-227">Description</span></span> | <span data-ttu-id="5554d-228">允許的值</span><span class="sxs-lookup"><span data-stu-id="5554d-228">Allowed values</span></span> | <span data-ttu-id="5554d-229">必要</span><span class="sxs-lookup"><span data-stu-id="5554d-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5554d-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="5554d-230">copyBehavior</span></span> |<span data-ttu-id="5554d-231">當來源為 BlobSource 或 FileSystem 時，定義複製行為。</span><span class="sxs-lookup"><span data-stu-id="5554d-231">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="5554d-232"><b>PreserveHierarchy</b>：保留目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="5554d-232"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="5554d-233">來源檔案到來源資料夾的相對路徑，與目標檔案到目標資料夾的相對路徑相同。</span><span class="sxs-lookup"><span data-stu-id="5554d-233">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="5554d-234"><b>FlattenHierarchy</b>：來自來源資料夾的所有檔案都在目標資料夾的第一層中。</span><span class="sxs-lookup"><span data-stu-id="5554d-234"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="5554d-235">目標檔案會有自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-235">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="5554d-236"><b>MergeFiles</b>：將來源資料夾的所有檔案合併為一個檔案。</span><span class="sxs-lookup"><span data-stu-id="5554d-236"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="5554d-237">如果已指定檔案/Blob 名稱，合併檔案名稱會是指定的名稱；否則，就會是自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-237">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="5554d-238">否</span><span class="sxs-lookup"><span data-stu-id="5554d-238">No</span></span> |

<span data-ttu-id="5554d-239">**BlobSource** 也支援這兩個屬性以提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="5554d-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="5554d-240">**treatEmptyAsNull**：指定是否將 null 或空字串視為 null 值。</span><span class="sxs-lookup"><span data-stu-id="5554d-240">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="5554d-241">**skipHeaderLineCount** - 指定需略過多少行。</span><span class="sxs-lookup"><span data-stu-id="5554d-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="5554d-242">僅適用於輸入資料集使用 TextFormat 時。</span><span class="sxs-lookup"><span data-stu-id="5554d-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="5554d-243">同樣地， **BlobSink** 支援下列屬性以提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="5554d-243">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="5554d-244">**blobWriterAddHeader**︰指定是否要在寫入至輸出資料集時新增資料行定義的標頭。</span><span class="sxs-lookup"><span data-stu-id="5554d-244">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="5554d-245">資料集現在支援下列會實作相同功能的屬性︰**treatEmptyAsNull**、**skipLineCount**、**firstRowAsHeader**。</span><span class="sxs-lookup"><span data-stu-id="5554d-245">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="5554d-246">下表提供有關使用新的資料集屬性來取代這些 Blob 來源/接收屬性的指引。</span><span class="sxs-lookup"><span data-stu-id="5554d-246">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="5554d-247">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-247">Copy Activity property</span></span> | <span data-ttu-id="5554d-248">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="5554d-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="5554d-249">BlobSource 上的 skipHeaderLineCount</span><span class="sxs-lookup"><span data-stu-id="5554d-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="5554d-250">skipLineCount 和 firstRowAsHeader。</span><span class="sxs-lookup"><span data-stu-id="5554d-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="5554d-251">會先略過行，然後讀取第一個資料列做為標頭。</span><span class="sxs-lookup"><span data-stu-id="5554d-251">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="5554d-252">BlobSource 上的 treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="5554d-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="5554d-253">輸入資料集上的 treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="5554d-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="5554d-254">BlobSink 上的 blobWriterAddHeader</span><span class="sxs-lookup"><span data-stu-id="5554d-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="5554d-255">輸出資料集上的 firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="5554d-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="5554d-256">如需這些屬性的詳細資訊，請參閱 [指定 TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) 一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="5554d-257">遞迴和 copyBehavior 範例</span><span class="sxs-lookup"><span data-stu-id="5554d-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="5554d-258">本節說明遞迴和 copyBehavior 值在不同組合的情況下，複製作業所產生的行為。</span><span class="sxs-lookup"><span data-stu-id="5554d-258">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="5554d-259">遞迴</span><span class="sxs-lookup"><span data-stu-id="5554d-259">recursive</span></span> | <span data-ttu-id="5554d-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="5554d-260">copyBehavior</span></span> | <span data-ttu-id="5554d-261">產生的行為</span><span class="sxs-lookup"><span data-stu-id="5554d-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5554d-262">true</span><span class="sxs-lookup"><span data-stu-id="5554d-262">true</span></span> |<span data-ttu-id="5554d-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="5554d-263">preserveHierarchy</span></span> |<span data-ttu-id="5554d-264">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="5554d-264">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="5554d-265">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-265">Folder1</span></span><br/><span data-ttu-id="5554d-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5554d-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5554d-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5554d-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5554d-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5554d-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5554d-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5554d-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5554d-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5554d-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5554d-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5554d-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5554d-272">會以與來源相同的結構，建立目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-272">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="5554d-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-273">Folder1</span></span><br/><span data-ttu-id="5554d-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5554d-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5554d-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5554d-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5554d-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5554d-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5554d-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5554d-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5554d-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5554d-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5554d-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5554d-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="5554d-280">true</span><span class="sxs-lookup"><span data-stu-id="5554d-280">true</span></span> |<span data-ttu-id="5554d-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="5554d-281">flattenHierarchy</span></span> |<span data-ttu-id="5554d-282">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="5554d-282">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="5554d-283">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-283">Folder1</span></span><br/><span data-ttu-id="5554d-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5554d-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5554d-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5554d-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5554d-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5554d-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5554d-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5554d-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5554d-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5554d-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5554d-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5554d-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5554d-290">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="5554d-290">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="5554d-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-291">Folder1</span></span><br/><span data-ttu-id="5554d-292">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="5554d-293">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="5554d-294">&nbsp;&nbsp;&nbsp;&nbsp;File3 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="5554d-295">&nbsp;&nbsp;&nbsp;&nbsp;File4 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="5554d-296">&nbsp;&nbsp;&nbsp;&nbsp;File5 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="5554d-297">true</span><span class="sxs-lookup"><span data-stu-id="5554d-297">true</span></span> |<span data-ttu-id="5554d-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="5554d-298">mergeFiles</span></span> |<span data-ttu-id="5554d-299">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="5554d-299">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="5554d-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-300">Folder1</span></span><br/><span data-ttu-id="5554d-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5554d-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5554d-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5554d-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5554d-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5554d-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5554d-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5554d-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5554d-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5554d-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5554d-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5554d-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5554d-307">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="5554d-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="5554d-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-308">Folder1</span></span><br/><span data-ttu-id="5554d-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 的內容會合併成一個檔案，並有自動產生的檔案名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="5554d-310">false</span><span class="sxs-lookup"><span data-stu-id="5554d-310">false</span></span> |<span data-ttu-id="5554d-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="5554d-311">preserveHierarchy</span></span> |<span data-ttu-id="5554d-312">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="5554d-312">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="5554d-313">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-313">Folder1</span></span><br/><span data-ttu-id="5554d-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5554d-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5554d-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5554d-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5554d-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5554d-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5554d-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5554d-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5554d-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5554d-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5554d-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5554d-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5554d-320">會以下列結構建立目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-320">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="5554d-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-321">Folder1</span></span><br/><span data-ttu-id="5554d-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5554d-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5554d-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5554d-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="5554d-324">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="5554d-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="5554d-325">false</span><span class="sxs-lookup"><span data-stu-id="5554d-325">false</span></span> |<span data-ttu-id="5554d-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="5554d-326">flattenHierarchy</span></span> |<span data-ttu-id="5554d-327">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="5554d-327">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="5554d-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-328">Folder1</span></span><br/><span data-ttu-id="5554d-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5554d-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5554d-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5554d-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5554d-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5554d-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5554d-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5554d-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5554d-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5554d-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5554d-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5554d-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5554d-335">會以下列結構建立目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-335">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="5554d-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-336">Folder1</span></span><br/><span data-ttu-id="5554d-337">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="5554d-338">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="5554d-339">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="5554d-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="5554d-340">false</span><span class="sxs-lookup"><span data-stu-id="5554d-340">false</span></span> |<span data-ttu-id="5554d-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="5554d-341">mergeFiles</span></span> |<span data-ttu-id="5554d-342">對於有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="5554d-342">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="5554d-343">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-343">Folder1</span></span><br/><span data-ttu-id="5554d-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="5554d-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="5554d-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="5554d-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="5554d-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="5554d-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="5554d-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="5554d-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="5554d-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="5554d-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="5554d-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="5554d-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="5554d-350">會以下列結構建立目標資料夾 Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-350">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="5554d-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="5554d-351">Folder1</span></span><br/><span data-ttu-id="5554d-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 的內容會合併成一個檔案，並有自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="5554d-353">File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="5554d-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="5554d-354">系統不會挑選含有 File3、File4 和 File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="5554d-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="5554d-355">逐步解說︰使用複製精靈將資料複製到 Blob 儲存體或從此儲存體複製資料</span><span class="sxs-lookup"><span data-stu-id="5554d-355">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="5554d-356">讓我們看看如何將資料快速複製到 Azure Blob 儲存體或從此儲存體複製資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-356">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="5554d-357">在這個逐步解說中，來源和目的地資料存放區的類型都是：Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5554d-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="5554d-358">此逐步解說中的管線會將資料從一個資料夾複製到相同 Blob 容器中的另一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="5554d-358">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="5554d-359">此逐步解說刻意設計得很簡單，為的是示範使用「Blob 儲存體」作為來源或接收器時的設定或屬性。</span><span class="sxs-lookup"><span data-stu-id="5554d-359">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="5554d-360">必要條件</span><span class="sxs-lookup"><span data-stu-id="5554d-360">Prerequisites</span></span>
1. <span data-ttu-id="5554d-361">建立一個一般用途的「Azure 儲存體帳戶」(如果您還沒有此帳戶)。</span><span class="sxs-lookup"><span data-stu-id="5554d-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="5554d-362">在這個逐步解說中，您將使用 Blob 儲存體同時作為「來源」和「目的地」資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5554d-362">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="5554d-363">如果您沒有 Azure 儲存體帳戶，請參閱 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account) 一文以取得建立步驟。</span><span class="sxs-lookup"><span data-stu-id="5554d-363">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
2. <span data-ttu-id="5554d-364">在儲存體帳戶中建立一個名為 **adfblobconnector** 的 Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="5554d-364">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="5554d-365">在 **adfblobconnector** 容器中建立一個名為 **input** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5554d-365">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="5554d-366">以下列內容建立一個名為 **emp.txt** 的檔案，然後使用 [Azure 儲存體總管](https://azurestorageexplorer.codeplex.com/)之類的工具將它上傳到 [input] 資料夾</span><span class="sxs-lookup"><span data-stu-id="5554d-366">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="5554d-367">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="5554d-367">Create the data factory</span></span>
1. <span data-ttu-id="5554d-368">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="5554d-368">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5554d-369">按一下左上角的 [+ 新增]，並按一下 [智慧 + 分析]，然後按一下 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="5554d-369">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="5554d-370">在 [ **新增 Data Factory** ] 刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="5554d-370">In the **New data factory** blade:</span></span>   
    1. <span data-ttu-id="5554d-371">針對 [名稱]，輸入 **ADFBlobConnectorDF**。</span><span class="sxs-lookup"><span data-stu-id="5554d-371">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="5554d-372">Azure Data Factory 的名稱在全域必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="5554d-372">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="5554d-373">如果您收到錯誤：`*Data factory name “ADFBlobConnectorDF” is not available`，請變更 Data Factory 的名稱 (例如 yournameADFBlobConnectorDF)，然後嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="5554d-373">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="5554d-374">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="5554d-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="5554d-375">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="5554d-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="5554d-376">針對「資源群組」，選取 [使用現有的] 來選取現有的資源群組 (或) 選取 [建立新項目] 來輸入資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-376">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="5554d-377">選取 Data Factory 的 [位置]。</span><span class="sxs-lookup"><span data-stu-id="5554d-377">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="5554d-378">選取刀鋒視窗底部的 [釘選到儀表板] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="5554d-378">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="5554d-379">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5554d-379">Click **Create**.</span></span>
3. <span data-ttu-id="5554d-380">建立完成之後，您會看到 [Data Factory] 刀鋒視窗，如下圖所示：![Data Factory 首頁](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-380">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="5554d-381">複製精靈</span><span class="sxs-lookup"><span data-stu-id="5554d-381">Copy Wizard</span></span>
1. <span data-ttu-id="5554d-382">在 Data Factory 首頁上，按一下 [資料複製 (預覽)] 圖格，以在個別索引標籤中啟動 [複製精靈]。</span><span class="sxs-lookup"><span data-stu-id="5554d-382">On the Data Factory home page, click the **Copy data [PREVIEW]** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="5554d-383">如果您看到網頁瀏覽器停留在「授權中...」，請停用/取消核取 [封鎖第三方 Cookie 和站台資料] 設定 (或) 將它保持啟用並為 **login.microsoftonline.com** 建立例外狀況，然後再次嘗試啟動精靈。</span><span class="sxs-lookup"><span data-stu-id="5554d-383">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="5554d-384">在 [屬性]  頁面︰</span><span class="sxs-lookup"><span data-stu-id="5554d-384">In the **Properties** page:</span></span>
    1. <span data-ttu-id="5554d-385">針對 [工作名稱]，輸入 **CopyPipeline**。</span><span class="sxs-lookup"><span data-stu-id="5554d-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="5554d-386">工作名稱是您 Data Factory 中管線的名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-386">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="5554d-387">輸入工作的「描述」(選擇性)。</span><span class="sxs-lookup"><span data-stu-id="5554d-387">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="5554d-388">針對 [工作頻率或工作排程]，保留 [依排程定期執行] 選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-388">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="5554d-389">如果您想要僅執行此工作一次，而不要依排程重複執行，請選取 [立即執行一次]。</span><span class="sxs-lookup"><span data-stu-id="5554d-389">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="5554d-390">如果您選取 [立即執行一次] 選項，系統就會建立一個[單次管線](data-factory-create-pipelines.md#onetime-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="5554d-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="5554d-391">保留 [週期性模式] 的設定。</span><span class="sxs-lookup"><span data-stu-id="5554d-391">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="5554d-392">此工作會在您於下一個步驟中指定的開始和結束時間之間每天執行。</span><span class="sxs-lookup"><span data-stu-id="5554d-392">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="5554d-393">將 [開始日期時間] 變更為 [2017 年 4 月 21 日]。</span><span class="sxs-lookup"><span data-stu-id="5554d-393">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="5554d-394">將 [結束日期時間] 變更為 [2017 年 4 月 25 日]。</span><span class="sxs-lookup"><span data-stu-id="5554d-394">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="5554d-395">您可以輸入日期，而不瀏覽行事曆。</span><span class="sxs-lookup"><span data-stu-id="5554d-395">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="5554d-396">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5554d-396">Click **Next**.</span></span>
      <span data-ttu-id="5554d-397">![複製工具 - 屬性頁面](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="5554d-398">在 [來源資料存放區] 頁面上，按一下 [Azure Blob 儲存體] 圖格。</span><span class="sxs-lookup"><span data-stu-id="5554d-398">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="5554d-399">您可以使用此頁面來指定複製工作的來源資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5554d-399">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="5554d-400">您可以使用現有的資料存放區連結服務或指定新的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5554d-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="5554d-401">若要使用現有的已連結服務，您需選取 [從現有的連結服務]，然後選取正確的已連結服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-401">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="5554d-402">![複製工具 - 來源資料存放區頁面](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="5554d-403">在 [指定 Azure Blob 儲存體帳戶]  頁面︰</span><span class="sxs-lookup"><span data-stu-id="5554d-403">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="5554d-404">針對 [連線名稱]，保留自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-404">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="5554d-405">此連線名稱是「Azure 儲存體」類型之已連結服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-405">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="5554d-406">確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="5554d-407">針對 [Azure 訂用帳戶]，選取您的 Azure 訂用帳戶或保留 [全選]。</span><span class="sxs-lookup"><span data-stu-id="5554d-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="5554d-408">從所選訂用帳戶中可用的 Azure 儲存體帳戶清單中，選取 [Azure 儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="5554d-408">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="5554d-409">您也可以選擇手動輸入儲存體帳戶設定，方法是針對 [帳戶選取方法] 選取 [手動輸入] 選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-409">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="5554d-410">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5554d-410">Click **Next**.</span></span> 
      <span data-ttu-id="5554d-411">![複製工具 - 指定 Azure Blob 儲存體帳戶](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-411">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="5554d-412">在 [選擇輸入檔案或資料夾]  頁面︰</span><span class="sxs-lookup"><span data-stu-id="5554d-412">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="5554d-413">按兩下 [adfblobcontainer]。</span><span class="sxs-lookup"><span data-stu-id="5554d-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="5554d-414">選取 [input]，然後按一下 [選擇]。</span><span class="sxs-lookup"><span data-stu-id="5554d-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="5554d-415">在本逐步解說中，您會選取 [input] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5554d-415">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="5554d-416">您也可以改為選取資料夾中的 emp.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="5554d-416">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="5554d-417">![複製工具 - 選擇輸入檔案或資料夾](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-417">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="5554d-418">在 [選擇輸入檔案或資料夾] 頁面上︰</span><span class="sxs-lookup"><span data-stu-id="5554d-418">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="5554d-419">確定 [檔案或資料夾] 已設定為 [adfblobconnector/input]。</span><span class="sxs-lookup"><span data-stu-id="5554d-419">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="5554d-420">如果檔案位於子資料夾 (例如 2017/04/01、2017/04/02 等)，請針對檔案或資料夾輸入 adfblobconnector/input/{year}/{month}/{day}。</span><span class="sxs-lookup"><span data-stu-id="5554d-420">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="5554d-421">當您按 TAB 從文字方塊中移出時，會看到三個可供選取年 (yyyy)、月 (MM) 和日 (dd) 格式的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="5554d-421">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="5554d-422">請勿設定 [以遞迴方式複製檔案]。</span><span class="sxs-lookup"><span data-stu-id="5554d-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="5554d-423">選取此選項可以用遞迴方式周遊資料夾來尋找要複製到目的地的檔案。</span><span class="sxs-lookup"><span data-stu-id="5554d-423">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="5554d-424">請勿設定 [二進位複製] 選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-424">Do not the **binary copy** option.</span></span> <span data-ttu-id="5554d-425">選取此選項可以執行將來源檔案複製到目的地的二進位複製。</span><span class="sxs-lookup"><span data-stu-id="5554d-425">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="5554d-426">請勿為此逐步解說選取這個選項，以便您可以在後續頁面中看到更多選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-426">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="5554d-427">確認 [壓縮類型] 已設定為 [無]。</span><span class="sxs-lookup"><span data-stu-id="5554d-427">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="5554d-428">如果您的來源檔案是以其中一種支援的格式壓縮的，則請為此選項選取一個值。</span><span class="sxs-lookup"><span data-stu-id="5554d-428">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="5554d-429">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5554d-429">Click **Next**.</span></span>
    <span data-ttu-id="5554d-430">![複製工具 - 選擇輸入檔案或資料夾](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-430">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="5554d-431">在 [檔案格式設定] 頁面上，您會看到分隔符號以及精靈藉由剖析檔案自動偵測到的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5554d-431">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="5554d-432">確認下列選項：a.</span><span class="sxs-lookup"><span data-stu-id="5554d-432">Confirm the following options: a.</span></span> <span data-ttu-id="5554d-433">[檔案格式] 已設定為 [文字格式]。</span><span class="sxs-lookup"><span data-stu-id="5554d-433">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="5554d-434">您可以在下拉式清單中看到所有支援的格式。</span><span class="sxs-lookup"><span data-stu-id="5554d-434">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="5554d-435">例如：JSON、Avro、ORC、Parquet。</span><span class="sxs-lookup"><span data-stu-id="5554d-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="5554d-436">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="5554d-436">b.</span></span> <span data-ttu-id="5554d-437">[資料行分隔符號] 已設定為 [`Comma (,)`]。</span><span class="sxs-lookup"><span data-stu-id="5554d-437">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="5554d-438">您可以在下拉式清單中看到 Data Factory 支援的其他資料行分隔符號。</span><span class="sxs-lookup"><span data-stu-id="5554d-438">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="5554d-439">您也可以指定自訂的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="5554d-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="5554d-440">c.</span><span class="sxs-lookup"><span data-stu-id="5554d-440">c.</span></span> <span data-ttu-id="5554d-441">[資料列分隔符號] 已設定為 [`Carriage Return + Line feed (\r\n)`]。</span><span class="sxs-lookup"><span data-stu-id="5554d-441">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="5554d-442">您可以在下拉式清單中看到 Data Factory 支援的其他資料列分隔符號。</span><span class="sxs-lookup"><span data-stu-id="5554d-442">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="5554d-443">您也可以指定自訂的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="5554d-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="5554d-444">d.</span><span class="sxs-lookup"><span data-stu-id="5554d-444">d.</span></span> <span data-ttu-id="5554d-445">[略過行數] 已設定為 [0]。</span><span class="sxs-lookup"><span data-stu-id="5554d-445">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="5554d-446">如果您希望略過檔案開頭的幾行，則請在這裡輸入數字。</span><span class="sxs-lookup"><span data-stu-id="5554d-446">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="5554d-447">e.</span><span class="sxs-lookup"><span data-stu-id="5554d-447">e.</span></span>  <span data-ttu-id="5554d-448">未設定 [第一個資料列包含資料行名稱]。</span><span class="sxs-lookup"><span data-stu-id="5554d-448">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="5554d-449">如果來源檔案的第一個資料列包含資料行名稱，則請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-449">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="5554d-450">f.</span><span class="sxs-lookup"><span data-stu-id="5554d-450">f.</span></span> <span data-ttu-id="5554d-451">已設定 [將空白資料行值視為 Null] 選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-451">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="5554d-452">展開 [進階設定] 以查看可用的進階選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-452">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="5554d-453">在頁面底部，查看來自 emp.txt 檔案之資料的 [預覽]。</span><span class="sxs-lookup"><span data-stu-id="5554d-453">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="5554d-454">按一下底部的 [結構描述] 索引標籤，以查看複製精靈藉由查看來源檔案中的資料所推斷出的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5554d-454">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="5554d-455">檢閱分隔符號並預覽資料之後，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5554d-455">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="5554d-456">![複製工具 - 檔案格式設定](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="5554d-457">在 [目的地資料存放區] 頁面上，選取 [Azure Blob 儲存體]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5554d-457">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="5554d-458">在這個逐步解說中，您將使用「Azure Blob 儲存體」同時作為來源和目的地資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5554d-458">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="5554d-459">![複製精靈 - 選取目的地資料存放區](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="5554d-460">在 [指定 Azure Blob 儲存體帳戶] 頁面上︰</span><span class="sxs-lookup"><span data-stu-id="5554d-460">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="5554d-461">針對 [連線名稱] 欄位，輸入 **AzureStorageLinkedService**。</span><span class="sxs-lookup"><span data-stu-id="5554d-461">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="5554d-462">確認已針對 [帳戶選取方法] 選取 [從 Azure 訂用帳戶] 選項。</span><span class="sxs-lookup"><span data-stu-id="5554d-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="5554d-463">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="5554d-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="5554d-464">選取您的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5554d-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="5554d-465">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5554d-465">Click **Next**.</span></span>     
10. <span data-ttu-id="5554d-466">在 [選擇輸出檔案或資料夾] 頁面上︰</span><span class="sxs-lookup"><span data-stu-id="5554d-466">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="5554d-467">將 [資料夾路徑] 指定為 **adfblobconnector/output/{year}/{month}/{day}**。</span><span class="sxs-lookup"><span data-stu-id="5554d-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="5554d-468">輸入 **TAB**。</span><span class="sxs-lookup"><span data-stu-id="5554d-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="5554d-469">針對 [年]，選取 [yyyy]。</span><span class="sxs-lookup"><span data-stu-id="5554d-469">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="5554d-470">針對 [月]，確定它已設定為 [MM]。</span><span class="sxs-lookup"><span data-stu-id="5554d-470">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="5554d-471">針對 [日]，確定它已設定為 [dd]。</span><span class="sxs-lookup"><span data-stu-id="5554d-471">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="5554d-472">確認 [壓縮類型] 已設定為 [無]。</span><span class="sxs-lookup"><span data-stu-id="5554d-472">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="5554d-473">確認 [複製行為] 已設定為 [合併檔案]。</span><span class="sxs-lookup"><span data-stu-id="5554d-473">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="5554d-474">如果已經有同名的輸出檔案存在，則新內容會新增到該相同檔案的結尾。</span><span class="sxs-lookup"><span data-stu-id="5554d-474">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="5554d-475">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5554d-475">Click **Next**.</span></span>
    <span data-ttu-id="5554d-476">![複製工具 - 選擇輸出檔案或資料夾](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="5554d-477">在 [檔案格式設定] 頁面上，檢閱設定，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5554d-477">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="5554d-478">這裡的其中一額外選項是為輸出檔案新增標頭。</span><span class="sxs-lookup"><span data-stu-id="5554d-478">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="5554d-479">如果您選取該選項，就會新增標頭資料列，其中會含有來自來源結構描述的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-479">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="5554d-480">您可以在檢視來源的結構描述時，重新命名預設的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-480">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="5554d-481">例如，您可以將第一個資料行變更為「名字」，而將第二個資料行變更為「姓氏」。</span><span class="sxs-lookup"><span data-stu-id="5554d-481">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="5554d-482">接著，系統就會產生含有以這些名稱作為資料行名稱之標頭的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="5554d-482">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="5554d-483">![複製工具 - 目的地的檔案格式設定](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="5554d-484">在 [效能設定] 頁面上，確認 [雲端單位] 和 [平行複製] 已設定為 [自動]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5554d-484">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="5554d-485">如需有關這些設定的詳細資料，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md#parallel-copy)。</span><span class="sxs-lookup"><span data-stu-id="5554d-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="5554d-486">![複製工具 - 效能設定](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="5554d-487">在 [摘要] 頁面上，檢閱所有設定 (工作屬性、來源和目的地的設定，以及複製設定)，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5554d-487">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="5554d-488">![複製工具 - 摘要頁面](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="5554d-489">在 [摘要] 頁面中檢閱資訊，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="5554d-489">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="5554d-490">此精靈會在 Data Factory (從您啟動複製精靈的位置) 中建立兩個連結服務、兩個資料集 (輸入和輸出)，以及一個管線。</span><span class="sxs-lookup"><span data-stu-id="5554d-490">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="5554d-491">![複製工具 - 部署頁面](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="5554d-492">監視管線 (複製工作)</span><span class="sxs-lookup"><span data-stu-id="5554d-492">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="5554d-493">在 [部署] 頁面上，按一下 [`Click here to monitor copy pipeline`] 連結。</span><span class="sxs-lookup"><span data-stu-id="5554d-493">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="5554d-494">您應該會在個別的索引標籤中看到 [監視及管理應用程式]。![監視及管理應用程式](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="5554d-494">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="5554d-495">將頂端的 [開始時間] 變更為 [`04/19/2017`]，將 [結束時間] 變更為 [`04/27/2017`]，然後按一下 [套用]。</span><span class="sxs-lookup"><span data-stu-id="5554d-495">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="5554d-496">您應該會在 [活動時段] 清單中看到五個活動時段。</span><span class="sxs-lookup"><span data-stu-id="5554d-496">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="5554d-497">[時段開始] 時間應該涵蓋從管線開始到管線結束時間的所有日子。</span><span class="sxs-lookup"><span data-stu-id="5554d-497">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="5554d-498">按一下 [活動時段] 清單的 [重新整理] 按鈕幾次，直到您看到所有活動時段的狀態都設定為 [就緒] 為止。</span><span class="sxs-lookup"><span data-stu-id="5554d-498">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="5554d-499">現在，確認是否已在 adfblobconnector 容器的輸出資料夾中產生輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="5554d-499">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="5554d-500">您應該會在輸出資料夾中看到以下資料夾結構：</span><span class="sxs-lookup"><span data-stu-id="5554d-500">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="5554d-501">如需有關監視及管理 Data Factory 的詳細資訊，請參閱[監視和管理 Data Factory 管線](data-factory-monitor-manage-app.md)一文。</span><span class="sxs-lookup"><span data-stu-id="5554d-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="5554d-502">Data Factory 實體</span><span class="sxs-lookup"><span data-stu-id="5554d-502">Data Factory entities</span></span>
<span data-ttu-id="5554d-503">現在，切換回含有 Data Factory 首頁的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5554d-503">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="5554d-504">請注意，您的 Data Factory 現在有兩個已連結的服務、兩個資料集，以及一條管線。</span><span class="sxs-lookup"><span data-stu-id="5554d-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![含有實體的 Data Factory 首頁](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="5554d-506">按一下 [編寫及部署] 以啟動「Data Factory 編輯器」。</span><span class="sxs-lookup"><span data-stu-id="5554d-506">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![Data Factory 編輯器](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="5554d-508">您應該會在 Data Factory 中看到下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="5554d-508">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="5554d-509">兩個已連結的服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-509">Two linked services.</span></span> <span data-ttu-id="5554d-510">一個用於來源，另一個用於目的地。</span><span class="sxs-lookup"><span data-stu-id="5554d-510">One for the source and the other one for the destination.</span></span> <span data-ttu-id="5554d-511">在這個逐步解說中，兩個已連結的服務都參考相同的「Azure 儲存體」帳戶。</span><span class="sxs-lookup"><span data-stu-id="5554d-511">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="5554d-512">兩個資料集。</span><span class="sxs-lookup"><span data-stu-id="5554d-512">Two datasets.</span></span> <span data-ttu-id="5554d-513">一個輸入資料集和一個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="5554d-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="5554d-514">在這個逐步解說中，兩者使用相同的 Blob 容器，但參考不同的資料夾 (輸入和輸出)。</span><span class="sxs-lookup"><span data-stu-id="5554d-514">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="5554d-515">一條管線。</span><span class="sxs-lookup"><span data-stu-id="5554d-515">A pipeline.</span></span> <span data-ttu-id="5554d-516">此管線包含一個複製活動，此活動會使用 Blob 來源和 Blob 接收器，將資料從 Azure Blob 位置複製到另一個 Azure Blob 位置。</span><span class="sxs-lookup"><span data-stu-id="5554d-516">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="5554d-517">下列各節會提供關於這些實體的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5554d-517">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="5554d-518">連結的服務</span><span class="sxs-lookup"><span data-stu-id="5554d-518">Linked services</span></span>
<span data-ttu-id="5554d-519">您應該會看到兩個已連結的服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-519">You should see two linked services.</span></span> <span data-ttu-id="5554d-520">一個用於來源，另一個用於目的地。</span><span class="sxs-lookup"><span data-stu-id="5554d-520">One for the source and the other one for the destination.</span></span> <span data-ttu-id="5554d-521">在這個逐步解說中，除了名稱之外，兩個定義看起來相同。</span><span class="sxs-lookup"><span data-stu-id="5554d-521">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="5554d-522">已連結服務的 **type** 是設定為 **AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="5554d-522">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="5554d-523">已連結服務的最重要屬性是 **connectionString**，Data Factory 會使用此屬性在執行階段連接到您的「Azure 儲存體」帳戶。</span><span class="sxs-lookup"><span data-stu-id="5554d-523">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="5554d-524">請在定義中忽略 hubName 屬性。</span><span class="sxs-lookup"><span data-stu-id="5554d-524">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="5554d-525">來源 Blob 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="5554d-525">Source blob storage linked service</span></span>
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

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="5554d-526">目的地 Blob 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="5554d-526">Destination blob storage linked service</span></span>

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

<span data-ttu-id="5554d-527">如需有關「Azure 儲存體」連結服務的詳細資訊，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="5554d-528">資料集</span><span class="sxs-lookup"><span data-stu-id="5554d-528">Datasets</span></span>
<span data-ttu-id="5554d-529">有兩個資料集：一個輸入資料集和一個輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="5554d-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="5554d-530">兩者的資料集類型都設定為 **AzureBlob**。</span><span class="sxs-lookup"><span data-stu-id="5554d-530">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="5554d-531">輸入資料集會指向 **adfblobconnector** 容器的 [input] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5554d-531">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="5554d-532">此資料集的 **external** 屬性是設定為 **true**，因為產生資料的管線不是含有以此資料集作為輸入之複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="5554d-532">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="5554d-533">輸出資料集會指向相同 Blob 容器的 [output] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5554d-533">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="5554d-534">輸出資料集也使用 **SliceStart** 系統變數的年、月和日來動態評估輸出檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="5554d-534">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="5554d-535">如需 Data Factory 所支援的函式與系統變數清單，請參閱 [Data Factory 函式與系統變數](data-factory-functions-variables.md) 。</span><span class="sxs-lookup"><span data-stu-id="5554d-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="5554d-536">**external** 屬性是設定為 **false**，因為此資料集是由管線所產生。</span><span class="sxs-lookup"><span data-stu-id="5554d-536">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="5554d-537">如需有關 Azure Blob 資料集所支援屬性的詳細資訊，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="5554d-538">輸入資料集</span><span class="sxs-lookup"><span data-stu-id="5554d-538">Input dataset</span></span>

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

##### <a name="output-dataset"></a><span data-ttu-id="5554d-539">輸出資料集</span><span class="sxs-lookup"><span data-stu-id="5554d-539">Output dataset</span></span>

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

#### <a name="pipeline"></a><span data-ttu-id="5554d-540">管線</span><span class="sxs-lookup"><span data-stu-id="5554d-540">Pipeline</span></span>
<span data-ttu-id="5554d-541">此管線只有一個活動。</span><span class="sxs-lookup"><span data-stu-id="5554d-541">The pipeline has just one activity.</span></span> <span data-ttu-id="5554d-542">此活動的 **type** 是設定為 **Copy**。</span><span class="sxs-lookup"><span data-stu-id="5554d-542">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="5554d-543">在此活動類型屬性中，有兩個區段，一個用於來源，另一個用於接收器。</span><span class="sxs-lookup"><span data-stu-id="5554d-543">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="5554d-544">來源類型是設定為 **BlobSource**，因為此活動會從 Blob 儲存體複製資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-544">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="5554d-545">接收器類型是設定為 **BlobSink**，因為此活動會將資料複製到 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5554d-545">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="5554d-546">此複製活動會以 InputDataset-z4y 作為輸入，並以 OutputDataset-z4y 作為輸出。</span><span class="sxs-lookup"><span data-stu-id="5554d-546">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="5554d-547">如需有關 BlobSource 和 BlobSink 所支援屬性的詳細資訊，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="5554d-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

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

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="5554d-548">從 Blob 儲存體來回複製資料的 JSON 範例</span><span class="sxs-lookup"><span data-stu-id="5554d-548">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="5554d-549">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="5554d-549">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5554d-550">它們會示範如何將資料複製到 Azure Blob 儲存體和 Azure SQL Database，以及複製其中的資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-550">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="5554d-551">不過，您可以在 Azure Data Factory 中使用複製活動，從任何來源 **直接** 將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="5554d-551">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="5554d-552">JSON 範例：將資料從 Blob 儲存體複製到 SQL Database</span><span class="sxs-lookup"><span data-stu-id="5554d-552">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="5554d-553">下列範例顯示︰</span><span class="sxs-lookup"><span data-stu-id="5554d-553">The following sample shows:</span></span>

1. <span data-ttu-id="5554d-554">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="5554d-555">[AzureStorage](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="5554d-556">[AzureBlob](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="5554d-557">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="5554d-558">具有使用 [BlobSource](#copy-activity-properties) 和 [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5554d-559">此範例會每小時將時間序列資料從 Azure Blob 複製到 Azure SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="5554d-559">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="5554d-560">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="5554d-560">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="5554d-561">**Azure SQL 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="5554d-561">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="5554d-562">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="5554d-562">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="5554d-563">Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="5554d-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="5554d-564">對於前者指定連接字串，包含帳戶金鑰，對於後者指定共用存取簽章 (SAS) Uri。</span><span class="sxs-lookup"><span data-stu-id="5554d-564">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="5554d-565">請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="5554d-566">**Azure Blob 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="5554d-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="5554d-567">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="5554d-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5554d-568">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="5554d-568">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5554d-569">資料夾路徑使用開始時間的年、月、日部分，而檔案名稱使用開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="5554d-569">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="5554d-570">“external”: “true” 設定會通知 Data Factory：這是 Data Factory 外部的資料表而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="5554d-570">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="5554d-571">**Azure SQL 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="5554d-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="5554d-572">此範例會將資料複製到 Azure SQL Database 中名為 "MyTable" 的資料表。</span><span class="sxs-lookup"><span data-stu-id="5554d-572">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="5554d-573">請在Azure SQL Database 中建立此資料表，其資料行的數目如您預期 Blob CSV 檔案要包含的數目。</span><span class="sxs-lookup"><span data-stu-id="5554d-573">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="5554d-574">此資料表會每小時加入新的資料列。</span><span class="sxs-lookup"><span data-stu-id="5554d-574">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="5554d-575">**具有 Blob 來源和 SQL 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="5554d-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="5554d-576">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="5554d-576">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="5554d-577">在管線 JSON 定義中，**source** 類型設為 **BlobSource**，而 **sink** 類型設為 **SqlSink**。</span><span class="sxs-lookup"><span data-stu-id="5554d-577">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="5554d-578">JSON 範例：將資料從 Azure SQL 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="5554d-578">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="5554d-579">下列範例顯示︰</span><span class="sxs-lookup"><span data-stu-id="5554d-579">The following sample shows:</span></span>

1. <span data-ttu-id="5554d-580">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="5554d-581">[AzureStorage](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="5554d-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="5554d-582">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="5554d-583">[AzureBlob](#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="5554d-584">具有使用 [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) 和 [BlobSink](#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="5554d-585">此範例會每小時將時間序列資料從 Azure SQL 資料表複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="5554d-585">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="5554d-586">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="5554d-586">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="5554d-587">**Azure SQL 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="5554d-587">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="5554d-588">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="5554d-588">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="5554d-589">Azure Data Factory 支援兩種類型的 Azure 儲存體連結服務：**AzureStorage** 和 **AzureStorageSas**。</span><span class="sxs-lookup"><span data-stu-id="5554d-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="5554d-590">對於前者指定連接字串，包含帳戶金鑰，對於後者指定共用存取簽章 (SAS) Uri。</span><span class="sxs-lookup"><span data-stu-id="5554d-590">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="5554d-591">請參閱 [連結服務](#linked-service-properties) 章節以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="5554d-592">**Azure SQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="5554d-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="5554d-593">此範例假設您已在 SQL Azure 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="5554d-593">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="5554d-594">設定 “external”: ”true” 會通知 Data Factory 服務：這是 Data Factory 外部的資料表而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="5554d-594">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="5554d-595">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="5554d-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="5554d-596">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="5554d-596">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="5554d-597">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="5554d-597">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="5554d-598">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="5554d-598">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="5554d-599">**具有 SQL 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="5554d-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="5554d-600">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="5554d-600">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="5554d-601">在管線 JSON 定義中，**source** 類型設為 **SqlSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="5554d-601">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="5554d-602">針對 **SqlReaderQuery** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="5554d-602">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="5554d-603">若要將來自來源資料集的資料行與來自接收資料集的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="5554d-603">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5554d-604">效能和微調</span><span class="sxs-lookup"><span data-stu-id="5554d-604">Performance and Tuning</span></span>
<span data-ttu-id="5554d-605">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="5554d-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
