---
title: "使用 Data Factory 從 Amazon Redshift 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Amazon Redshift 移動資料。"
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
ms.openlocfilehash: bccb941363952bb2251629240a88148a6527d62e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="6d060-103">使用 Azure Data Factory 從 Amazon Redshift 移動資料</span><span class="sxs-lookup"><span data-stu-id="6d060-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="6d060-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從 Amazon Redshift 移動資料。</span><span class="sxs-lookup"><span data-stu-id="6d060-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="6d060-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="6d060-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="6d060-106">您可以將資料從 Amazon Redshift 複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="6d060-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="6d060-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="6d060-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="6d060-108">Data Factory 目前支援將資料從 Amazon Redshift 移到其他資料存放區，而不支援將資料從其他資料存放區移到 Amazon Redshift。</span><span class="sxs-lookup"><span data-stu-id="6d060-108">Data factory currently supports moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d060-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="6d060-109">Prerequisites</span></span>
* <span data-ttu-id="6d060-110">如果您要將資料移到內部部署的資料存放區，請在內部部署的電腦上安裝[資料管理閘道](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="6d060-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="6d060-111">接著，將 Amazon Redshift 叢集的存取權授與「資料管理閘道」(使用該電腦的 IP 位址)。</span><span class="sxs-lookup"><span data-stu-id="6d060-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="6d060-112">如需相關指示，請參閱 [授權存取叢集](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) 。</span><span class="sxs-lookup"><span data-stu-id="6d060-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="6d060-113">如果您要移動資料到 Azure 資料存放區，請參閱 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653) 以取得 Azure 資料中心所使用的計算 IP 位址和 SQL 範圍。</span><span class="sxs-lookup"><span data-stu-id="6d060-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6d060-114">開始使用</span><span class="sxs-lookup"><span data-stu-id="6d060-114">Getting started</span></span>
<span data-ttu-id="6d060-115">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從 Amazon Redshift 來源移動資料。</span><span class="sxs-lookup"><span data-stu-id="6d060-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="6d060-116">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="6d060-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6d060-117">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="6d060-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="6d060-118">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="6d060-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6d060-119">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="6d060-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6d060-120">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="6d060-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="6d060-121">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="6d060-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6d060-122">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="6d060-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="6d060-123">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="6d060-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6d060-124">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="6d060-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6d060-125">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="6d060-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6d060-126">如需相關範例，其中含有用來從 Amazon Redshift 資料存放區複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 Amazon Redshift 複製到 Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="6d060-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6d060-127">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Amazon Redshift 特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="6d060-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="6d060-128">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="6d060-128">Linked service properties</span></span>
<span data-ttu-id="6d060-129">下表提供 Amazon Redshift 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="6d060-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="6d060-130">屬性</span><span class="sxs-lookup"><span data-stu-id="6d060-130">Property</span></span> | <span data-ttu-id="6d060-131">說明</span><span class="sxs-lookup"><span data-stu-id="6d060-131">Description</span></span> | <span data-ttu-id="6d060-132">必要</span><span class="sxs-lookup"><span data-stu-id="6d060-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d060-133">類型</span><span class="sxs-lookup"><span data-stu-id="6d060-133">type</span></span> |<span data-ttu-id="6d060-134">類型屬性必須設為： **AmazonRedshift**。</span><span class="sxs-lookup"><span data-stu-id="6d060-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="6d060-135">是</span><span class="sxs-lookup"><span data-stu-id="6d060-135">Yes</span></span> |
| <span data-ttu-id="6d060-136">伺服器</span><span class="sxs-lookup"><span data-stu-id="6d060-136">server</span></span> |<span data-ttu-id="6d060-137">Amazon Redshift 伺服器的 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6d060-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="6d060-138">是</span><span class="sxs-lookup"><span data-stu-id="6d060-138">Yes</span></span> |
| <span data-ttu-id="6d060-139">連接埠</span><span class="sxs-lookup"><span data-stu-id="6d060-139">port</span></span> |<span data-ttu-id="6d060-140">Amazon Redshift 伺服器用來接聽用戶端連線的 TCP 連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="6d060-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="6d060-141">否，預設值︰5439</span><span class="sxs-lookup"><span data-stu-id="6d060-141">No, default value: 5439</span></span> |
| <span data-ttu-id="6d060-142">資料庫</span><span class="sxs-lookup"><span data-stu-id="6d060-142">database</span></span> |<span data-ttu-id="6d060-143">Amazon Redshift 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d060-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="6d060-144">是</span><span class="sxs-lookup"><span data-stu-id="6d060-144">Yes</span></span> |
| <span data-ttu-id="6d060-145">username</span><span class="sxs-lookup"><span data-stu-id="6d060-145">username</span></span> |<span data-ttu-id="6d060-146">可存取資料庫之使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d060-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="6d060-147">是</span><span class="sxs-lookup"><span data-stu-id="6d060-147">Yes</span></span> |
| <span data-ttu-id="6d060-148">password</span><span class="sxs-lookup"><span data-stu-id="6d060-148">password</span></span> |<span data-ttu-id="6d060-149">使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="6d060-149">Password for the user account.</span></span> |<span data-ttu-id="6d060-150">是</span><span class="sxs-lookup"><span data-stu-id="6d060-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="6d060-151">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="6d060-151">Dataset properties</span></span>
<span data-ttu-id="6d060-152">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="6d060-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6d060-153">所有資料集類型 (Azure SQL、Azure Blob、Azure 資料表等) 的結構、可用性及原則等區段都相似。</span><span class="sxs-lookup"><span data-stu-id="6d060-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6d060-154">不同類型資料集的 **typeProperties** 區段不同。</span><span class="sxs-lookup"><span data-stu-id="6d060-154">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="6d060-155">它提供資料存放區中資料的位置之相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6d060-155">It provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6d060-156">**RelationalTable** 資料集類型的 typeProperties 區段 (包含 Amazon Redshift 資料集) 具有下列屬性</span><span class="sxs-lookup"><span data-stu-id="6d060-156">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="6d060-157">屬性</span><span class="sxs-lookup"><span data-stu-id="6d060-157">Property</span></span> | <span data-ttu-id="6d060-158">說明</span><span class="sxs-lookup"><span data-stu-id="6d060-158">Description</span></span> | <span data-ttu-id="6d060-159">必要</span><span class="sxs-lookup"><span data-stu-id="6d060-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6d060-160">tableName</span><span class="sxs-lookup"><span data-stu-id="6d060-160">tableName</span></span> |<span data-ttu-id="6d060-161">Amazon Redshift 資料庫中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="6d060-161">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="6d060-162">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="6d060-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6d060-163">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="6d060-163">Copy activity properties</span></span>
<span data-ttu-id="6d060-164">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="6d060-164">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6d060-165">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="6d060-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="6d060-166">而活動的 **typeProperties** 區段中，可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="6d060-166">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="6d060-167">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="6d060-167">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6d060-168">當複製活動的來源是 **RelationalSource** 類型 (包含 Amazon Redshift) 時，typeProperties 區段可使用下列屬性：</span><span class="sxs-lookup"><span data-stu-id="6d060-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="6d060-169">屬性</span><span class="sxs-lookup"><span data-stu-id="6d060-169">Property</span></span> | <span data-ttu-id="6d060-170">說明</span><span class="sxs-lookup"><span data-stu-id="6d060-170">Description</span></span> | <span data-ttu-id="6d060-171">允許的值</span><span class="sxs-lookup"><span data-stu-id="6d060-171">Allowed values</span></span> | <span data-ttu-id="6d060-172">必要</span><span class="sxs-lookup"><span data-stu-id="6d060-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6d060-173">query</span><span class="sxs-lookup"><span data-stu-id="6d060-173">query</span></span> |<span data-ttu-id="6d060-174">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="6d060-174">Use the custom query to read data.</span></span> |<span data-ttu-id="6d060-175">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="6d060-175">SQL query string.</span></span> <span data-ttu-id="6d060-176">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="6d060-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="6d060-177">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="6d060-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="6d060-178">JSON 範例：將資料從 Amazon Redshift 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="6d060-178">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="6d060-179">此範例示範如何將資料從 Amazon Redshift 資料庫複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="6d060-179">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="6d060-180">不過，您可以在 Azure Data Factory 中使用複製活動， **直接** 將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="6d060-180">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="6d060-181">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="6d060-181">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="6d060-182">[AmazonRedshift](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="6d060-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="6d060-183">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="6d060-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="6d060-184">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="6d060-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="6d060-185">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="6d060-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="6d060-186">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="6d060-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="6d060-187">此範例會每個小時將資料從 Amazon Redshift 中的查詢結果複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="6d060-187">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="6d060-188">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="6d060-188">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="6d060-189">**Amazon Redshift 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="6d060-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="6d060-190">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="6d060-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="6d060-191">**Amazon Redshift 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="6d060-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="6d060-192">設定 `"external": true` 可讓 Data Factory 服務知道資料集是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="6d060-192">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="6d060-193">在不是由管線中的活動所產生的輸入資料集上，請將此屬性設定為 true。</span><span class="sxs-lookup"><span data-stu-id="6d060-193">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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

<span data-ttu-id="6d060-194">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="6d060-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6d060-195">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="6d060-195">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6d060-196">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="6d060-196">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="6d060-197">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="6d060-197">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="6d060-198">**具有 Azure Redshift 來源 (RelationalSource) 和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="6d060-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="6d060-199">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="6d060-199">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6d060-200">在管線 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="6d060-200">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="6d060-201">針對 **query** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="6d060-201">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="6d060-202">Amazon Redshift 的類型對應</span><span class="sxs-lookup"><span data-stu-id="6d060-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="6d060-203">如 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會藉由下列含有兩個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="6d060-203">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="6d060-204">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="6d060-204">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="6d060-205">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="6d060-205">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="6d060-206">將資料移到 Amazon Redshift 時，下列對應將用於從 Amazon Redshift 類型到 .NET 類型。</span><span class="sxs-lookup"><span data-stu-id="6d060-206">When moving data to Amazon Redshift, the following mappings are used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="6d060-207">Amazon Redshift 類型</span><span class="sxs-lookup"><span data-stu-id="6d060-207">Amazon Redshift Type</span></span> | <span data-ttu-id="6d060-208">以 .Net 為基礎的類型</span><span class="sxs-lookup"><span data-stu-id="6d060-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="6d060-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="6d060-209">SMALLINT</span></span> |<span data-ttu-id="6d060-210">Int16</span><span class="sxs-lookup"><span data-stu-id="6d060-210">Int16</span></span> |
| <span data-ttu-id="6d060-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="6d060-211">INTEGER</span></span> |<span data-ttu-id="6d060-212">Int32</span><span class="sxs-lookup"><span data-stu-id="6d060-212">Int32</span></span> |
| <span data-ttu-id="6d060-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="6d060-213">BIGINT</span></span> |<span data-ttu-id="6d060-214">Int64</span><span class="sxs-lookup"><span data-stu-id="6d060-214">Int64</span></span> |
| <span data-ttu-id="6d060-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="6d060-215">DECIMAL</span></span> |<span data-ttu-id="6d060-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="6d060-216">Decimal</span></span> |
| <span data-ttu-id="6d060-217">REAL</span><span class="sxs-lookup"><span data-stu-id="6d060-217">REAL</span></span> |<span data-ttu-id="6d060-218">單一</span><span class="sxs-lookup"><span data-stu-id="6d060-218">Single</span></span> |
| <span data-ttu-id="6d060-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="6d060-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="6d060-220">兩倍</span><span class="sxs-lookup"><span data-stu-id="6d060-220">Double</span></span> |
| <span data-ttu-id="6d060-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="6d060-221">BOOLEAN</span></span> |<span data-ttu-id="6d060-222">String</span><span class="sxs-lookup"><span data-stu-id="6d060-222">String</span></span> |
| <span data-ttu-id="6d060-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="6d060-223">CHAR</span></span> |<span data-ttu-id="6d060-224">String</span><span class="sxs-lookup"><span data-stu-id="6d060-224">String</span></span> |
| <span data-ttu-id="6d060-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="6d060-225">VARCHAR</span></span> |<span data-ttu-id="6d060-226">String</span><span class="sxs-lookup"><span data-stu-id="6d060-226">String</span></span> |
| <span data-ttu-id="6d060-227">日期</span><span class="sxs-lookup"><span data-stu-id="6d060-227">DATE</span></span> |<span data-ttu-id="6d060-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="6d060-228">DateTime</span></span> |
| <span data-ttu-id="6d060-229">時間戳記</span><span class="sxs-lookup"><span data-stu-id="6d060-229">TIMESTAMP</span></span> |<span data-ttu-id="6d060-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="6d060-230">DateTime</span></span> |
| <span data-ttu-id="6d060-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="6d060-231">TEXT</span></span> |<span data-ttu-id="6d060-232">String</span><span class="sxs-lookup"><span data-stu-id="6d060-232">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="6d060-233">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="6d060-233">Map source to sink columns</span></span>
<span data-ttu-id="6d060-234">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="6d060-234">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6d060-235">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="6d060-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="6d060-236">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="6d060-236">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="6d060-237">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="6d060-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6d060-238">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="6d060-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6d060-239">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="6d060-239">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6d060-240">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="6d060-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6d060-241">效能和微調</span><span class="sxs-lookup"><span data-stu-id="6d060-241">Performance and Tuning</span></span>
<span data-ttu-id="6d060-242">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="6d060-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d060-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d060-243">Next Steps</span></span>
<span data-ttu-id="6d060-244">請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="6d060-244">See the following articles:</span></span>

* <span data-ttu-id="6d060-245">[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ，以取得使用「複製活動」來建立管線的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="6d060-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
