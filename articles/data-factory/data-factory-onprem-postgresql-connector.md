---
title: "使用 Azure Data Factory 從 PostgreSQL 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 PostgreSQL 資料庫移動資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: fd26f0d03f8b0b352a6544a81ad952d2e2a1b7a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="a6bf3-103">使用 Azure Data Factory 從 PostgreSQL 移動資料</span><span class="sxs-lookup"><span data-stu-id="a6bf3-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="a6bf3-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署的 PostgreSQL 資料庫移動資料。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="a6bf3-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="a6bf3-106">您可以將資料從內部部署的 PostgreSQL 資料存放區複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-106">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span></span> <span data-ttu-id="a6bf3-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="a6bf3-108">Data Factory 目前支援將資料從 PostgreSQL 資料庫移到其他資料存放區，而不支援將資料從其他資料存放區移到 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-108">Data factory currently supports moving data from a PostgreSQL database to other data stores, but not for moving data from other data stores to an PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a6bf3-109">先決條件</span><span class="sxs-lookup"><span data-stu-id="a6bf3-109">prerequisites</span></span>

<span data-ttu-id="a6bf3-110">Data Factory 服務支援使用資料管理閘道器連接至內部部署 PostgreSQL 來源。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-110">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="a6bf3-111">請參閱 [在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文來了解資料管理閘道和設定閘道的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="a6bf3-112">即使 PostgreSQL 資料庫裝載於 Azure IaaS VM 中，也必須要有閘道。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-112">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="a6bf3-113">您可以將閘道安裝在與資料存放區相同或相異的 IaaS VM 上，只要閘道可以連線到資料庫即可。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-113">You can install gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="a6bf3-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="a6bf3-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="a6bf3-115">Supported versions and installation</span></span>
<span data-ttu-id="a6bf3-116">若要讓資料管理閘道連線至 PostgreSQL 資料庫，在與資料管理閘道相同的系統上，安裝 [PostgreSQL 的 Ngpsql 資料提供者](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 或以上版本。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-116">For Data Management Gateway to connect to the PostgreSQL Database, install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="a6bf3-117">支援 PostgreSQL 版本 7.4 和以上版本。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a6bf3-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="a6bf3-118">Getting started</span></span>
<span data-ttu-id="a6bf3-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 PostgreSQL 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="a6bf3-120">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a6bf3-121">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="a6bf3-122">您也可以使用下列工具來建立管線：</span><span class="sxs-lookup"><span data-stu-id="a6bf3-122">You can also use the following tools to create a pipeline:</span></span> 
    - <span data-ttu-id="a6bf3-123">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a6bf3-123">Azure portal</span></span>
    - <span data-ttu-id="a6bf3-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6bf3-124">Visual Studio</span></span>
    - <span data-ttu-id="a6bf3-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6bf3-125">Azure PowerShell</span></span>
    - <span data-ttu-id="a6bf3-126">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="a6bf3-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="a6bf3-127">.NET API</span><span class="sxs-lookup"><span data-stu-id="a6bf3-127">.NET API</span></span>
    - <span data-ttu-id="a6bf3-128">REST API</span><span class="sxs-lookup"><span data-stu-id="a6bf3-128">REST API</span></span>

     <span data-ttu-id="a6bf3-129">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a6bf3-130">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="a6bf3-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="a6bf3-131">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a6bf3-132">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a6bf3-133">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a6bf3-134">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a6bf3-135">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a6bf3-136">如需相關範例，其中含有用來從內部部署 PostgreSQL 資料存放區複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 PostgreSQL 複製到 Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a6bf3-137">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 PostgreSQL 資料存放區特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="a6bf3-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a6bf3-138">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="a6bf3-138">Linked service properties</span></span>
<span data-ttu-id="a6bf3-139">下表提供 PostgreSQL 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-139">The following table provides description for JSON elements specific to PostgreSQL linked service.</span></span>

| <span data-ttu-id="a6bf3-140">屬性</span><span class="sxs-lookup"><span data-stu-id="a6bf3-140">Property</span></span> | <span data-ttu-id="a6bf3-141">說明</span><span class="sxs-lookup"><span data-stu-id="a6bf3-141">Description</span></span> | <span data-ttu-id="a6bf3-142">必要</span><span class="sxs-lookup"><span data-stu-id="a6bf3-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6bf3-143">類型</span><span class="sxs-lookup"><span data-stu-id="a6bf3-143">type</span></span> |<span data-ttu-id="a6bf3-144">類型屬性必須設為： **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="a6bf3-144">The type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="a6bf3-145">是</span><span class="sxs-lookup"><span data-stu-id="a6bf3-145">Yes</span></span> |
| <span data-ttu-id="a6bf3-146">伺服器</span><span class="sxs-lookup"><span data-stu-id="a6bf3-146">server</span></span> |<span data-ttu-id="a6bf3-147">PostgreSQL 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-147">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="a6bf3-148">是</span><span class="sxs-lookup"><span data-stu-id="a6bf3-148">Yes</span></span> |
| <span data-ttu-id="a6bf3-149">資料庫</span><span class="sxs-lookup"><span data-stu-id="a6bf3-149">database</span></span> |<span data-ttu-id="a6bf3-150">PostgreSQL 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-150">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="a6bf3-151">是</span><span class="sxs-lookup"><span data-stu-id="a6bf3-151">Yes</span></span> |
| <span data-ttu-id="a6bf3-152">結構描述</span><span class="sxs-lookup"><span data-stu-id="a6bf3-152">schema</span></span> |<span data-ttu-id="a6bf3-153">在資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-153">Name of the schema in the database.</span></span> <span data-ttu-id="a6bf3-154">結構描述名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-154">The schema name is case-sensitive.</span></span> |<span data-ttu-id="a6bf3-155">否</span><span class="sxs-lookup"><span data-stu-id="a6bf3-155">No</span></span> |
| <span data-ttu-id="a6bf3-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a6bf3-156">authenticationType</span></span> |<span data-ttu-id="a6bf3-157">用來連接到 PostgreSQL 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-157">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="a6bf3-158">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="a6bf3-159">是</span><span class="sxs-lookup"><span data-stu-id="a6bf3-159">Yes</span></span> |
| <span data-ttu-id="a6bf3-160">username</span><span class="sxs-lookup"><span data-stu-id="a6bf3-160">username</span></span> |<span data-ttu-id="a6bf3-161">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="a6bf3-162">否</span><span class="sxs-lookup"><span data-stu-id="a6bf3-162">No</span></span> |
| <span data-ttu-id="a6bf3-163">password</span><span class="sxs-lookup"><span data-stu-id="a6bf3-163">password</span></span> |<span data-ttu-id="a6bf3-164">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="a6bf3-165">否</span><span class="sxs-lookup"><span data-stu-id="a6bf3-165">No</span></span> |
| <span data-ttu-id="a6bf3-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a6bf3-166">gatewayName</span></span> |<span data-ttu-id="a6bf3-167">Data Factory 服務應該用來連接到內部部署 PostgreSQL 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-167">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="a6bf3-168">是</span><span class="sxs-lookup"><span data-stu-id="a6bf3-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="a6bf3-169">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="a6bf3-169">Dataset properties</span></span>
<span data-ttu-id="a6bf3-170">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a6bf3-171">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="a6bf3-172">每個資料集類型的 typeProperties 區段都不同，可提供資料存放區中資料的位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-172">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a6bf3-173">**RelationalTable** 資料集類型的 typeProperties 區段 (包含 PostgreSQL 資料集) 具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="a6bf3-173">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span></span>

| <span data-ttu-id="a6bf3-174">屬性</span><span class="sxs-lookup"><span data-stu-id="a6bf3-174">Property</span></span> | <span data-ttu-id="a6bf3-175">說明</span><span class="sxs-lookup"><span data-stu-id="a6bf3-175">Description</span></span> | <span data-ttu-id="a6bf3-176">必要</span><span class="sxs-lookup"><span data-stu-id="a6bf3-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6bf3-177">tableName</span><span class="sxs-lookup"><span data-stu-id="a6bf3-177">tableName</span></span> |<span data-ttu-id="a6bf3-178">PostgreSQL 資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-178">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="a6bf3-179">tableName 會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-179">The tableName is case-sensitive.</span></span> |<span data-ttu-id="a6bf3-180">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="a6bf3-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a6bf3-181">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="a6bf3-181">Copy activity properties</span></span>
<span data-ttu-id="a6bf3-182">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-182">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a6bf3-183">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a6bf3-184">而活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-184">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="a6bf3-185">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-185">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a6bf3-186">當來源的類型為 **RelationalSource** (包括 PostgreSQL) 時，typeProperties 區段中會有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="a6bf3-186">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a6bf3-187">屬性</span><span class="sxs-lookup"><span data-stu-id="a6bf3-187">Property</span></span> | <span data-ttu-id="a6bf3-188">說明</span><span class="sxs-lookup"><span data-stu-id="a6bf3-188">Description</span></span> | <span data-ttu-id="a6bf3-189">允許的值</span><span class="sxs-lookup"><span data-stu-id="a6bf3-189">Allowed values</span></span> | <span data-ttu-id="a6bf3-190">必要</span><span class="sxs-lookup"><span data-stu-id="a6bf3-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a6bf3-191">query</span><span class="sxs-lookup"><span data-stu-id="a6bf3-191">query</span></span> |<span data-ttu-id="a6bf3-192">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-192">Use the custom query to read data.</span></span> |<span data-ttu-id="a6bf3-193">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-193">SQL query string.</span></span> <span data-ttu-id="a6bf3-194">例如："query": "select * from \"MySchema\".\"MyTable\""。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="a6bf3-195">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="a6bf3-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="a6bf3-196">結構描述和資料表名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="a6bf3-197">在查詢中以 `""` (雙引號) 括住它們。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-197">Enclose them in `""` (double quotes) in the query.</span></span>  

<span data-ttu-id="a6bf3-198">**範例：**</span><span class="sxs-lookup"><span data-stu-id="a6bf3-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-to-azure-blob"></a><span data-ttu-id="a6bf3-199">JSON 範例：將資料從 PostgreSQL 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a6bf3-199">JSON example: Copy data from PostgreSQL to Azure Blob</span></span>
<span data-ttu-id="a6bf3-200">此範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-200">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a6bf3-201">這些範例示範如何將資料從 PostgreSQL 資料庫複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-201">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span></span> <span data-ttu-id="a6bf3-202">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-202">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="a6bf3-203">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="a6bf3-204">其中並不包含建立 Data Factory 的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-204">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="a6bf3-205">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="a6bf3-206">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="a6bf3-206">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="a6bf3-207">[OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="a6bf3-208">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a6bf3-209">[RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="a6bf3-210">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a6bf3-211">具有使用 [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-211">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a6bf3-212">此範例會每個小時將資料從 PostgreSQL 資料庫中的查詢結果複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-212">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span></span> <span data-ttu-id="a6bf3-213">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-213">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a6bf3-214">第一步是設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-214">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="a6bf3-215">如需相關指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-215">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a6bf3-216">**PostgreSQL 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="a6bf3-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="a6bf3-217">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="a6bf3-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="a6bf3-218">**PostgreSQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="a6bf3-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="a6bf3-219">此範例假設您已在 PostgreSQL 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestamp")。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-219">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="a6bf3-220">設定 `"external": true` 可讓 Data Factory 服務知道資料集是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-220">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="a6bf3-221">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="a6bf3-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="a6bf3-222">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a6bf3-223">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-223">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a6bf3-224">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="a6bf3-225">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="a6bf3-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="a6bf3-226">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="a6bf3-227">在管線 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="a6bf3-228">針對 **query** 屬性指定的 SQL 查詢會從 PostgreSQL Database 中的 public.usstates 資料表選取資料。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-228">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="a6bf3-229">PostgreSQL 的類型對應</span><span class="sxs-lookup"><span data-stu-id="a6bf3-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="a6bf3-230">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會使用下列 2 個步驟的方法，執行自動類型轉換，將來源類型轉換成接收類型：</span><span class="sxs-lookup"><span data-stu-id="a6bf3-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="a6bf3-231">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="a6bf3-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="a6bf3-232">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="a6bf3-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="a6bf3-233">將資料移到 PostgreSQL 時，下列對應會用於從 PostgreSQL 類型到 .NET 類型。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-233">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span></span>

| <span data-ttu-id="a6bf3-234">PostgreSQL 資料庫類型</span><span class="sxs-lookup"><span data-stu-id="a6bf3-234">PostgreSQL Database type</span></span> | <span data-ttu-id="a6bf3-235">PostgresSQL 別名</span><span class="sxs-lookup"><span data-stu-id="a6bf3-235">PostgresSQL aliases</span></span> | <span data-ttu-id="a6bf3-236">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="a6bf3-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6bf3-237">abstime</span><span class="sxs-lookup"><span data-stu-id="a6bf3-237">abstime</span></span> | |<span data-ttu-id="a6bf3-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="a6bf3-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="a6bf3-239">bigint</span><span class="sxs-lookup"><span data-stu-id="a6bf3-239">bigint</span></span> |<span data-ttu-id="a6bf3-240">int8</span><span class="sxs-lookup"><span data-stu-id="a6bf3-240">int8</span></span> |<span data-ttu-id="a6bf3-241">Int64</span><span class="sxs-lookup"><span data-stu-id="a6bf3-241">Int64</span></span> |
| <span data-ttu-id="a6bf3-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="a6bf3-242">bigserial</span></span> |<span data-ttu-id="a6bf3-243">serial8</span><span class="sxs-lookup"><span data-stu-id="a6bf3-243">serial8</span></span> |<span data-ttu-id="a6bf3-244">Int64</span><span class="sxs-lookup"><span data-stu-id="a6bf3-244">Int64</span></span> |
| <span data-ttu-id="a6bf3-245">位元 [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-245">bit [ (n) ]</span></span> | |<span data-ttu-id="a6bf3-246">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="a6bf3-247">位元不同 [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="a6bf3-248">varbit</span><span class="sxs-lookup"><span data-stu-id="a6bf3-248">varbit</span></span> |<span data-ttu-id="a6bf3-249">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-249">Byte[], String</span></span> |
| <span data-ttu-id="a6bf3-250">布林值</span><span class="sxs-lookup"><span data-stu-id="a6bf3-250">boolean</span></span> |<span data-ttu-id="a6bf3-251">布林</span><span class="sxs-lookup"><span data-stu-id="a6bf3-251">bool</span></span> |<span data-ttu-id="a6bf3-252">布林值</span><span class="sxs-lookup"><span data-stu-id="a6bf3-252">Boolean</span></span> |
| <span data-ttu-id="a6bf3-253">方塊</span><span class="sxs-lookup"><span data-stu-id="a6bf3-253">box</span></span> | |<span data-ttu-id="a6bf3-254">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-255">bytea</span><span class="sxs-lookup"><span data-stu-id="a6bf3-255">bytea</span></span> | |<span data-ttu-id="a6bf3-256">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-257">字元 [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-257">character [ (n) ]</span></span> |<span data-ttu-id="a6bf3-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-258">char [ (n) ]</span></span> |<span data-ttu-id="a6bf3-259">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-259">String</span></span> |
| <span data-ttu-id="a6bf3-260">字元不同 [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-260">character varying [ (n) ]</span></span> |<span data-ttu-id="a6bf3-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-261">varchar [ (n) ]</span></span> |<span data-ttu-id="a6bf3-262">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-262">String</span></span> |
| <span data-ttu-id="a6bf3-263">cid</span><span class="sxs-lookup"><span data-stu-id="a6bf3-263">cid</span></span> | |<span data-ttu-id="a6bf3-264">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-264">String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-265">cidr</span><span class="sxs-lookup"><span data-stu-id="a6bf3-265">cidr</span></span> | |<span data-ttu-id="a6bf3-266">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-266">String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-267">圓形</span><span class="sxs-lookup"><span data-stu-id="a6bf3-267">circle</span></span> | |<span data-ttu-id="a6bf3-268">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-269">日期</span><span class="sxs-lookup"><span data-stu-id="a6bf3-269">date</span></span> | |<span data-ttu-id="a6bf3-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="a6bf3-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-271">daterange</span><span class="sxs-lookup"><span data-stu-id="a6bf3-271">daterange</span></span> | |<span data-ttu-id="a6bf3-272">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-272">String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-273">雙精度</span><span class="sxs-lookup"><span data-stu-id="a6bf3-273">double precision</span></span> |<span data-ttu-id="a6bf3-274">float8</span><span class="sxs-lookup"><span data-stu-id="a6bf3-274">float8</span></span> |<span data-ttu-id="a6bf3-275">兩倍</span><span class="sxs-lookup"><span data-stu-id="a6bf3-275">Double</span></span> |
| <span data-ttu-id="a6bf3-276">inet</span><span class="sxs-lookup"><span data-stu-id="a6bf3-276">inet</span></span> | |<span data-ttu-id="a6bf3-277">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-278">intarry</span><span class="sxs-lookup"><span data-stu-id="a6bf3-278">intarry</span></span> | |<span data-ttu-id="a6bf3-279">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-279">String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-280">int4range</span><span class="sxs-lookup"><span data-stu-id="a6bf3-280">int4range</span></span> | |<span data-ttu-id="a6bf3-281">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-281">String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-282">int8range</span><span class="sxs-lookup"><span data-stu-id="a6bf3-282">int8range</span></span> | |<span data-ttu-id="a6bf3-283">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-283">String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-284">integer</span><span class="sxs-lookup"><span data-stu-id="a6bf3-284">integer</span></span> |<span data-ttu-id="a6bf3-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="a6bf3-285">int, int4</span></span> |<span data-ttu-id="a6bf3-286">Int32</span><span class="sxs-lookup"><span data-stu-id="a6bf3-286">Int32</span></span> |
| <span data-ttu-id="a6bf3-287">間隔 [ 欄位 ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="a6bf3-288">Timespan</span><span class="sxs-lookup"><span data-stu-id="a6bf3-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-289">json</span><span class="sxs-lookup"><span data-stu-id="a6bf3-289">json</span></span> | |<span data-ttu-id="a6bf3-290">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-290">String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="a6bf3-291">jsonb</span></span> | |<span data-ttu-id="a6bf3-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-293">線條</span><span class="sxs-lookup"><span data-stu-id="a6bf3-293">line</span></span> | |<span data-ttu-id="a6bf3-294">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-295">lseg</span><span class="sxs-lookup"><span data-stu-id="a6bf3-295">lseg</span></span> | |<span data-ttu-id="a6bf3-296">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="a6bf3-297">macaddr</span></span> | |<span data-ttu-id="a6bf3-298">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-299">money</span><span class="sxs-lookup"><span data-stu-id="a6bf3-299">money</span></span> | |<span data-ttu-id="a6bf3-300">十進位</span><span class="sxs-lookup"><span data-stu-id="a6bf3-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-301">數值 [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="a6bf3-302">十進位 [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="a6bf3-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="a6bf3-303">十進位</span><span class="sxs-lookup"><span data-stu-id="a6bf3-303">Decimal</span></span> |
| <span data-ttu-id="a6bf3-304">numrange</span><span class="sxs-lookup"><span data-stu-id="a6bf3-304">numrange</span></span> | |<span data-ttu-id="a6bf3-305">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-305">String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-306">oid</span><span class="sxs-lookup"><span data-stu-id="a6bf3-306">oid</span></span> | |<span data-ttu-id="a6bf3-307">Int32</span><span class="sxs-lookup"><span data-stu-id="a6bf3-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-308">路徑</span><span class="sxs-lookup"><span data-stu-id="a6bf3-308">path</span></span> | |<span data-ttu-id="a6bf3-309">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="a6bf3-310">pg_lsn</span></span> | |<span data-ttu-id="a6bf3-311">Int64</span><span class="sxs-lookup"><span data-stu-id="a6bf3-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-312">點</span><span class="sxs-lookup"><span data-stu-id="a6bf3-312">point</span></span> | |<span data-ttu-id="a6bf3-313">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-314">多邊形</span><span class="sxs-lookup"><span data-stu-id="a6bf3-314">polygon</span></span> | |<span data-ttu-id="a6bf3-315">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="a6bf3-316">real</span><span class="sxs-lookup"><span data-stu-id="a6bf3-316">real</span></span> |<span data-ttu-id="a6bf3-317">float4</span><span class="sxs-lookup"><span data-stu-id="a6bf3-317">float4</span></span> |<span data-ttu-id="a6bf3-318">單一</span><span class="sxs-lookup"><span data-stu-id="a6bf3-318">Single</span></span> |
| <span data-ttu-id="a6bf3-319">smallint</span><span class="sxs-lookup"><span data-stu-id="a6bf3-319">smallint</span></span> |<span data-ttu-id="a6bf3-320">int2</span><span class="sxs-lookup"><span data-stu-id="a6bf3-320">int2</span></span> |<span data-ttu-id="a6bf3-321">Int16</span><span class="sxs-lookup"><span data-stu-id="a6bf3-321">Int16</span></span> |
| <span data-ttu-id="a6bf3-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="a6bf3-322">smallserial</span></span> |<span data-ttu-id="a6bf3-323">serial2</span><span class="sxs-lookup"><span data-stu-id="a6bf3-323">serial2</span></span> |<span data-ttu-id="a6bf3-324">Int16</span><span class="sxs-lookup"><span data-stu-id="a6bf3-324">Int16</span></span> |
| <span data-ttu-id="a6bf3-325">serial</span><span class="sxs-lookup"><span data-stu-id="a6bf3-325">serial</span></span> |<span data-ttu-id="a6bf3-326">serial4</span><span class="sxs-lookup"><span data-stu-id="a6bf3-326">serial4</span></span> |<span data-ttu-id="a6bf3-327">Int32</span><span class="sxs-lookup"><span data-stu-id="a6bf3-327">Int32</span></span> |
| <span data-ttu-id="a6bf3-328">文字</span><span class="sxs-lookup"><span data-stu-id="a6bf3-328">text</span></span> | |<span data-ttu-id="a6bf3-329">String</span><span class="sxs-lookup"><span data-stu-id="a6bf3-329">String</span></span> |&nbsp;

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="a6bf3-330">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="a6bf3-330">Map source to sink columns</span></span>
<span data-ttu-id="a6bf3-331">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-331">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="a6bf3-332">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="a6bf3-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="a6bf3-333">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-333">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="a6bf3-334">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a6bf3-335">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a6bf3-336">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-336">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a6bf3-337">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a6bf3-338">效能和微調</span><span class="sxs-lookup"><span data-stu-id="a6bf3-338">Performance and Tuning</span></span>
<span data-ttu-id="a6bf3-339">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="a6bf3-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
