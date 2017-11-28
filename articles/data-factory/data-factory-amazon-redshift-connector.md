---
title: "使用 Data Factory 的 Amazon Redshift aaaMove 資料 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 Amazon Redshift toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="58745-103">使用 Azure Data Factory 從 Amazon Redshift 移動資料</span><span class="sxs-lookup"><span data-stu-id="58745-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="58745-104">本文說明如何 toouse hello Amazon Redshift 從 Azure Data Factory toomove 資料中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="58745-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="58745-105">hello 文章是根據 hello[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="58745-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="58745-106">您可以從 Amazon Redshift tooany 支援接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="58745-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="58745-107">如需支援為接收 hello 複製活動的資料存放區的清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="58745-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="58745-108">資料處理站目前支援移動資料從 Amazon Redshift tooother 資料存放區，但不是將資料從其他資料存放區 tooAmazon Redshift 移動的資料。</span><span class="sxs-lookup"><span data-stu-id="58745-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58745-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="58745-109">Prerequisites</span></span>
* <span data-ttu-id="58745-110">如果您要移動資料 tooan 在內部部署資料存放區，安裝[資料管理閘道器](data-factory-data-management-gateway.md)在內部部署電腦上。</span><span class="sxs-lookup"><span data-stu-id="58745-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="58745-111">然後，授與資料管理閘道器 （使用 hello 機器的 IP 位址） hello 存取 tooAmazon Redshift 叢集。</span><span class="sxs-lookup"><span data-stu-id="58745-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="58745-112">請參閱[授權存取 toohello 叢集](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="58745-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="58745-113">如果您要移動資料 tooan Azure 資料存放區，請參閱[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)hello 計算 IP 位址和 hello Azure 資料中心所使用的 SQL 範圍。</span><span class="sxs-lookup"><span data-stu-id="58745-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="58745-114">開始使用</span><span class="sxs-lookup"><span data-stu-id="58745-114">Getting started</span></span>
<span data-ttu-id="58745-115">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 Amazon Redshift 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="58745-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="58745-116">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="58745-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="58745-117">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="58745-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="58745-118">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="58745-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="58745-119">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="58745-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="58745-120">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="58745-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="58745-121">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="58745-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="58745-122">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="58745-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="58745-123">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="58745-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="58745-124">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="58745-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="58745-125">當您使用 [工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="58745-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="58745-126">使用 Data Factory 實體的 Amazon Redshift 資料存放區中的使用的 toocopy 資料的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Amazon Redshift tooAzure Blob 複製](#json-example-copy-data-from-amazon-redshift-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="58745-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="58745-127">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooAmazon Redshift 的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="58745-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="58745-128">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="58745-128">Linked service properties</span></span>
<span data-ttu-id="58745-129">下表中的 hello 提供 JSON 項目特定 tooAmazon Redshift 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="58745-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="58745-130">屬性</span><span class="sxs-lookup"><span data-stu-id="58745-130">Property</span></span> | <span data-ttu-id="58745-131">說明</span><span class="sxs-lookup"><span data-stu-id="58745-131">Description</span></span> | <span data-ttu-id="58745-132">必要</span><span class="sxs-lookup"><span data-stu-id="58745-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58745-133">類型</span><span class="sxs-lookup"><span data-stu-id="58745-133">type</span></span> |<span data-ttu-id="58745-134">hello 類型屬性必須設定為： **AmazonRedshift**。</span><span class="sxs-lookup"><span data-stu-id="58745-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="58745-135">是</span><span class="sxs-lookup"><span data-stu-id="58745-135">Yes</span></span> |
| <span data-ttu-id="58745-136">伺服器</span><span class="sxs-lookup"><span data-stu-id="58745-136">server</span></span> |<span data-ttu-id="58745-137">IP 位址或主機名稱的 hello Amazon Redshift 伺服器。</span><span class="sxs-lookup"><span data-stu-id="58745-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="58745-138">是</span><span class="sxs-lookup"><span data-stu-id="58745-138">Yes</span></span> |
| <span data-ttu-id="58745-139">連接埠</span><span class="sxs-lookup"><span data-stu-id="58745-139">port</span></span> |<span data-ttu-id="58745-140">hello hello Amazon Redshift 伺服器 hello TCP 連接埠號碼使用 toolisten 用於用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="58745-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="58745-141">否，預設值︰5439</span><span class="sxs-lookup"><span data-stu-id="58745-141">No, default value: 5439</span></span> |
| <span data-ttu-id="58745-142">資料庫</span><span class="sxs-lookup"><span data-stu-id="58745-142">database</span></span> |<span data-ttu-id="58745-143">Hello Amazon Redshift 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="58745-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="58745-144">是</span><span class="sxs-lookup"><span data-stu-id="58745-144">Yes</span></span> |
| <span data-ttu-id="58745-145">username</span><span class="sxs-lookup"><span data-stu-id="58745-145">username</span></span> |<span data-ttu-id="58745-146">具有存取 toohello 資料庫使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="58745-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="58745-147">是</span><span class="sxs-lookup"><span data-stu-id="58745-147">Yes</span></span> |
| <span data-ttu-id="58745-148">password</span><span class="sxs-lookup"><span data-stu-id="58745-148">password</span></span> |<span data-ttu-id="58745-149">Hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="58745-149">Password for hello user account.</span></span> |<span data-ttu-id="58745-150">是</span><span class="sxs-lookup"><span data-stu-id="58745-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="58745-151">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="58745-151">Dataset properties</span></span>
<span data-ttu-id="58745-152">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="58745-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="58745-153">所有資料集類型 (Azure SQL、Azure Blob、Azure 資料表等) 的結構、可用性及原則等區段都相似。</span><span class="sxs-lookup"><span data-stu-id="58745-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="58745-154">hello **typeProperties**區段是不同的資料集的每個型別。</span><span class="sxs-lookup"><span data-stu-id="58745-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="58745-155">它提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="58745-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="58745-156">hello typeProperties 區段類型的資料集**RelationalTable** （包括 Amazon Redshift 資料集） 具有下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="58745-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="58745-157">屬性</span><span class="sxs-lookup"><span data-stu-id="58745-157">Property</span></span> | <span data-ttu-id="58745-158">說明</span><span class="sxs-lookup"><span data-stu-id="58745-158">Description</span></span> | <span data-ttu-id="58745-159">必要</span><span class="sxs-lookup"><span data-stu-id="58745-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58745-160">tableName</span><span class="sxs-lookup"><span data-stu-id="58745-160">tableName</span></span> |<span data-ttu-id="58745-161">連結服務的 hello Amazon Redshift 資料庫中的 hello 資料表名稱參考。</span><span class="sxs-lookup"><span data-stu-id="58745-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="58745-162">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="58745-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="58745-163">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="58745-163">Copy activity properties</span></span>
<span data-ttu-id="58745-164">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="58745-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="58745-165">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="58745-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="58745-166">而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="58745-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="58745-167">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="58745-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="58745-168">複製活動的來源時的型別**RelationalSource** （包括 Amazon Redshift），下列屬性的 hello 可用 typeProperties 區段中：</span><span class="sxs-lookup"><span data-stu-id="58745-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="58745-169">屬性</span><span class="sxs-lookup"><span data-stu-id="58745-169">Property</span></span> | <span data-ttu-id="58745-170">說明</span><span class="sxs-lookup"><span data-stu-id="58745-170">Description</span></span> | <span data-ttu-id="58745-171">允許的值</span><span class="sxs-lookup"><span data-stu-id="58745-171">Allowed values</span></span> | <span data-ttu-id="58745-172">必要</span><span class="sxs-lookup"><span data-stu-id="58745-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="58745-173">query</span><span class="sxs-lookup"><span data-stu-id="58745-173">query</span></span> |<span data-ttu-id="58745-174">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="58745-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="58745-175">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="58745-175">SQL query string.</span></span> <span data-ttu-id="58745-176">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="58745-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="58745-177">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="58745-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="58745-178">JSON 範例： 從 Amazon Redshift tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="58745-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="58745-179">這個範例會示範如何 toocopy 資料從 Amazon Redshift 資料庫 tooan Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="58745-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="58745-180">不過，資料可以複製**直接**hello 接收所述的 tooany[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="58745-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="58745-181">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="58745-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="58745-182">[AmazonRedshift](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="58745-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="58745-183">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="58745-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="58745-184">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="58745-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="58745-185">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="58745-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="58745-186">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="58745-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="58745-187">hello 範例將資料從 Amazon Redshift tooa blob 中的查詢結果的每個小時。</span><span class="sxs-lookup"><span data-stu-id="58745-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="58745-188">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="58745-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="58745-189">**Amazon Redshift 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="58745-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="58745-190">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="58745-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="58745-191">**Amazon Redshift 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="58745-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="58745-192">設定`"external": true`該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="58745-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="58745-193">設定此屬性 tootrue 上就不會產生 hello 管線中活動的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="58745-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="58745-194">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="58745-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="58745-195">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="58745-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="58745-196">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="58745-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="58745-197">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="58745-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="58745-198">**具有 Azure Redshift 來源 (RelationalSource) 和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="58745-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="58745-199">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="58745-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="58745-200">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="58745-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="58745-201">指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="58745-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="58745-202">Amazon Redshift 的類型對應</span><span class="sxs-lookup"><span data-stu-id="58745-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="58745-203">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="58745-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="58745-204">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="58745-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="58745-205">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="58745-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="58745-206">當您移動資料 tooAmazon Redshift，hello 下列對應會使用從 Amazon Redshift 類型 too.NET 型別。</span><span class="sxs-lookup"><span data-stu-id="58745-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="58745-207">Amazon Redshift 類型</span><span class="sxs-lookup"><span data-stu-id="58745-207">Amazon Redshift Type</span></span> | <span data-ttu-id="58745-208">以 .Net 為基礎的類型</span><span class="sxs-lookup"><span data-stu-id="58745-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="58745-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="58745-209">SMALLINT</span></span> |<span data-ttu-id="58745-210">Int16</span><span class="sxs-lookup"><span data-stu-id="58745-210">Int16</span></span> |
| <span data-ttu-id="58745-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="58745-211">INTEGER</span></span> |<span data-ttu-id="58745-212">Int32</span><span class="sxs-lookup"><span data-stu-id="58745-212">Int32</span></span> |
| <span data-ttu-id="58745-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="58745-213">BIGINT</span></span> |<span data-ttu-id="58745-214">Int64</span><span class="sxs-lookup"><span data-stu-id="58745-214">Int64</span></span> |
| <span data-ttu-id="58745-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="58745-215">DECIMAL</span></span> |<span data-ttu-id="58745-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="58745-216">Decimal</span></span> |
| <span data-ttu-id="58745-217">REAL</span><span class="sxs-lookup"><span data-stu-id="58745-217">REAL</span></span> |<span data-ttu-id="58745-218">單一</span><span class="sxs-lookup"><span data-stu-id="58745-218">Single</span></span> |
| <span data-ttu-id="58745-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="58745-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="58745-220">兩倍</span><span class="sxs-lookup"><span data-stu-id="58745-220">Double</span></span> |
| <span data-ttu-id="58745-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="58745-221">BOOLEAN</span></span> |<span data-ttu-id="58745-222">String</span><span class="sxs-lookup"><span data-stu-id="58745-222">String</span></span> |
| <span data-ttu-id="58745-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="58745-223">CHAR</span></span> |<span data-ttu-id="58745-224">String</span><span class="sxs-lookup"><span data-stu-id="58745-224">String</span></span> |
| <span data-ttu-id="58745-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="58745-225">VARCHAR</span></span> |<span data-ttu-id="58745-226">String</span><span class="sxs-lookup"><span data-stu-id="58745-226">String</span></span> |
| <span data-ttu-id="58745-227">日期</span><span class="sxs-lookup"><span data-stu-id="58745-227">DATE</span></span> |<span data-ttu-id="58745-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="58745-228">DateTime</span></span> |
| <span data-ttu-id="58745-229">時間戳記</span><span class="sxs-lookup"><span data-stu-id="58745-229">TIMESTAMP</span></span> |<span data-ttu-id="58745-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="58745-230">DateTime</span></span> |
| <span data-ttu-id="58745-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="58745-231">TEXT</span></span> |<span data-ttu-id="58745-232">String</span><span class="sxs-lookup"><span data-stu-id="58745-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="58745-233">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="58745-233">Map source toosink columns</span></span>
<span data-ttu-id="58745-234">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="58745-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="58745-235">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="58745-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="58745-236">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="58745-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="58745-237">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="58745-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="58745-238">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="58745-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="58745-239">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="58745-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="58745-240">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="58745-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="58745-241">效能和微調</span><span class="sxs-lookup"><span data-stu-id="58745-241">Performance and Tuning</span></span>
<span data-ttu-id="58745-242">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="58745-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58745-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58745-243">Next Steps</span></span>
<span data-ttu-id="58745-244">請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="58745-244">See hello following articles:</span></span>

* <span data-ttu-id="58745-245">[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得使用「複製活動」來建立管線的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="58745-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
