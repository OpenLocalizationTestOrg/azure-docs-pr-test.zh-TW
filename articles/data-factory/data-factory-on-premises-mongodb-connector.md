---
title: "使用 Data Factory 從 MongoDB 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 MongoDB 資料庫移動資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: ac4ff55c765a5b874b81714c3d0063a5b4765a05
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="82f6d-103">使用 Azure Data Factory 從 MongoDB 移動資料</span><span class="sxs-lookup"><span data-stu-id="82f6d-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="82f6d-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署的 MongoDB 資料庫移動資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MongoDB database.</span></span> <span data-ttu-id="82f6d-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="82f6d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="82f6d-106">您可以將資料從內部部署的 MongoDB 資料存放區複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="82f6d-106">You can copy data from an on-premises MongoDB data store to any supported sink data store.</span></span> <span data-ttu-id="82f6d-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="82f6d-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="82f6d-108">Data Factory 目前只支援將資料從 MongoDB 資料存放區移到其他資料存放區，而不支援將資料從其他資料存放區移到 MongoDB 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="82f6d-108">Data factory currently supports only moving data from a MongoDB data store to other data stores, but not for moving data from other data stores to an MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="82f6d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="82f6d-109">Prerequisites</span></span>
<span data-ttu-id="82f6d-110">如果是能夠連接到您內部部署 MongoDB 資料庫的 Azure Data Factory 服務，您就必須安裝下列元件：</span><span class="sxs-lookup"><span data-stu-id="82f6d-110">For the Azure Data Factory service to be able to connect to your on-premises MongoDB database, you must install the following components:</span></span>

- <span data-ttu-id="82f6d-111">支援的 MongoDB 版本為︰2.4、2.6、3.0 及 3.2。</span><span class="sxs-lookup"><span data-stu-id="82f6d-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="82f6d-112">位於裝載資料庫的同一部電腦上或個別電腦上的資料管理閘道，可避免與資料庫競用資源。</span><span class="sxs-lookup"><span data-stu-id="82f6d-112">Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="82f6d-113">資料管理閘道是一套透過安全且可管理的方式，將內部部署資料來源連結至雲端服務的軟體。</span><span class="sxs-lookup"><span data-stu-id="82f6d-113">Data Management Gateway is a software that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="82f6d-114">如需資料管理閘道的詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="82f6d-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="82f6d-115">如需有關為閘道設定資料管線來移動資料的逐步指示，請參閱[將資料從內部部署移到雲端](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

    <span data-ttu-id="82f6d-116">當您安裝閘道時，它會自動安裝用來連線至 MongoDB 的 Microsoft MongoDB ODBC 驅動程式。</span><span class="sxs-lookup"><span data-stu-id="82f6d-116">When you install the gateway, it automatically installs a Microsoft MongoDB ODBC driver used to connect to MongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="82f6d-117">即使 MongoDB 是裝載在 Azure IaaS VM 中，您還是需要使用閘道與其連接。</span><span class="sxs-lookup"><span data-stu-id="82f6d-117">You need to use the gateway to connect to MongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="82f6d-118">如果您正嘗試連接到裝載於雲端中的 MongoDB 執行個體，您也可以在 IaaS VM 中安裝閘道器執行個體。</span><span class="sxs-lookup"><span data-stu-id="82f6d-118">If you are trying to connect to an instance of MongoDB hosted in cloud, you can also install the gateway instance in the IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="82f6d-119">開始使用</span><span class="sxs-lookup"><span data-stu-id="82f6d-119">Getting started</span></span>
<span data-ttu-id="82f6d-120">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 MongoDB 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="82f6d-121">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="82f6d-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="82f6d-122">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="82f6d-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="82f6d-123">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="82f6d-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="82f6d-124">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="82f6d-125">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="82f6d-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="82f6d-126">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="82f6d-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="82f6d-127">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="82f6d-128">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="82f6d-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="82f6d-129">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="82f6d-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="82f6d-130">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="82f6d-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="82f6d-131">如需相關範例，其中含有用來從內部部署 MongoDB 資料存放區複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 MongoDB 複製到 Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="82f6d-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB to Azure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="82f6d-132">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 MongoDB 來源特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="82f6d-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to MongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="82f6d-133">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="82f6d-133">Linked service properties</span></span>
<span data-ttu-id="82f6d-134">下表提供 **OnPremisesMongoDB** 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="82f6d-134">The following table provides description for JSON elements specific to **OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="82f6d-135">屬性</span><span class="sxs-lookup"><span data-stu-id="82f6d-135">Property</span></span> | <span data-ttu-id="82f6d-136">說明</span><span class="sxs-lookup"><span data-stu-id="82f6d-136">Description</span></span> | <span data-ttu-id="82f6d-137">必要</span><span class="sxs-lookup"><span data-stu-id="82f6d-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82f6d-138">類型</span><span class="sxs-lookup"><span data-stu-id="82f6d-138">type</span></span> |<span data-ttu-id="82f6d-139">類型屬性必須設為： **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="82f6d-139">The type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="82f6d-140">是</span><span class="sxs-lookup"><span data-stu-id="82f6d-140">Yes</span></span> |
| <span data-ttu-id="82f6d-141">伺服器</span><span class="sxs-lookup"><span data-stu-id="82f6d-141">server</span></span> |<span data-ttu-id="82f6d-142">MongoDB 伺服器的 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="82f6d-142">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="82f6d-143">是</span><span class="sxs-lookup"><span data-stu-id="82f6d-143">Yes</span></span> |
| <span data-ttu-id="82f6d-144">連接埠</span><span class="sxs-lookup"><span data-stu-id="82f6d-144">port</span></span> |<span data-ttu-id="82f6d-145">MongoDB 伺服器用來接聽用戶端連線的 TCP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="82f6d-145">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="82f6d-146">選用，預設值︰27017</span><span class="sxs-lookup"><span data-stu-id="82f6d-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="82f6d-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="82f6d-147">authenticationType</span></span> |<span data-ttu-id="82f6d-148">基本或匿名。</span><span class="sxs-lookup"><span data-stu-id="82f6d-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="82f6d-149">是</span><span class="sxs-lookup"><span data-stu-id="82f6d-149">Yes</span></span> |
| <span data-ttu-id="82f6d-150">username</span><span class="sxs-lookup"><span data-stu-id="82f6d-150">username</span></span> |<span data-ttu-id="82f6d-151">用來存取 MongoDB 的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="82f6d-151">User account to access MongoDB.</span></span> |<span data-ttu-id="82f6d-152">是 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="82f6d-153">password</span><span class="sxs-lookup"><span data-stu-id="82f6d-153">password</span></span> |<span data-ttu-id="82f6d-154">使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="82f6d-154">Password for the user.</span></span> |<span data-ttu-id="82f6d-155">是 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="82f6d-156">authSource</span><span class="sxs-lookup"><span data-stu-id="82f6d-156">authSource</span></span> |<span data-ttu-id="82f6d-157">您想要用來檢查驗證所用之認證的 MongoDB 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="82f6d-157">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="82f6d-158">選用 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="82f6d-159">預設值︰使用以 databaseName 屬性指定的系統管理員帳戶和資料庫。</span><span class="sxs-lookup"><span data-stu-id="82f6d-159">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="82f6d-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="82f6d-160">databaseName</span></span> |<span data-ttu-id="82f6d-161">您想要存取之 MongoDB 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="82f6d-161">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="82f6d-162">是</span><span class="sxs-lookup"><span data-stu-id="82f6d-162">Yes</span></span> |
| <span data-ttu-id="82f6d-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="82f6d-163">gatewayName</span></span> |<span data-ttu-id="82f6d-164">存取資料存放區之閘道的名稱。</span><span class="sxs-lookup"><span data-stu-id="82f6d-164">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="82f6d-165">是</span><span class="sxs-lookup"><span data-stu-id="82f6d-165">Yes</span></span> |
| <span data-ttu-id="82f6d-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="82f6d-166">encryptedCredential</span></span> |<span data-ttu-id="82f6d-167">由閘道加密的認證。</span><span class="sxs-lookup"><span data-stu-id="82f6d-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="82f6d-168">選用</span><span class="sxs-lookup"><span data-stu-id="82f6d-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="82f6d-169">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="82f6d-169">Dataset properties</span></span>
<span data-ttu-id="82f6d-170">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="82f6d-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="82f6d-171">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="82f6d-172">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="82f6d-172">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="82f6d-173">**MongoDbCollection** 類型資料集的 typeProperties 區段具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="82f6d-173">The typeProperties section for dataset of type **MongoDbCollection** has the following properties:</span></span>

| <span data-ttu-id="82f6d-174">屬性</span><span class="sxs-lookup"><span data-stu-id="82f6d-174">Property</span></span> | <span data-ttu-id="82f6d-175">說明</span><span class="sxs-lookup"><span data-stu-id="82f6d-175">Description</span></span> | <span data-ttu-id="82f6d-176">必要</span><span class="sxs-lookup"><span data-stu-id="82f6d-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82f6d-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="82f6d-177">collectionName</span></span> |<span data-ttu-id="82f6d-178">MongoDB 資料庫中集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="82f6d-178">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="82f6d-179">是</span><span class="sxs-lookup"><span data-stu-id="82f6d-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="82f6d-180">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="82f6d-180">Copy activity properties</span></span>
<span data-ttu-id="82f6d-181">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="82f6d-181">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="82f6d-182">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="82f6d-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="82f6d-183">另一方面，活動的 **typeProperties** 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="82f6d-183">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="82f6d-184">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="82f6d-184">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="82f6d-185">如果來源類型為 **MongoDbSource** ，則 typeProperties 區段可使用下列屬性：</span><span class="sxs-lookup"><span data-stu-id="82f6d-185">When the source is of type **MongoDbSource** the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="82f6d-186">屬性</span><span class="sxs-lookup"><span data-stu-id="82f6d-186">Property</span></span> | <span data-ttu-id="82f6d-187">說明</span><span class="sxs-lookup"><span data-stu-id="82f6d-187">Description</span></span> | <span data-ttu-id="82f6d-188">允許的值</span><span class="sxs-lookup"><span data-stu-id="82f6d-188">Allowed values</span></span> | <span data-ttu-id="82f6d-189">必要</span><span class="sxs-lookup"><span data-stu-id="82f6d-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="82f6d-190">query</span><span class="sxs-lookup"><span data-stu-id="82f6d-190">query</span></span> |<span data-ttu-id="82f6d-191">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-191">Use the custom query to read data.</span></span> |<span data-ttu-id="82f6d-192">SQL-92 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="82f6d-192">SQL-92 query string.</span></span> <span data-ttu-id="82f6d-193">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="82f6d-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="82f6d-194">否 (如果已指定 **dataset** 的 **collectionName**)</span><span class="sxs-lookup"><span data-stu-id="82f6d-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-to-azure-blob"></a><span data-ttu-id="82f6d-195">JSON 範例：將資料從 MongoDB 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="82f6d-195">JSON example: Copy data from MongoDB to Azure Blob</span></span>
<span data-ttu-id="82f6d-196">此範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="82f6d-196">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="82f6d-197">它示範如何將資料從內部部署的 MongoDB 複製到「Azure Blob 儲存體」。</span><span class="sxs-lookup"><span data-stu-id="82f6d-197">It shows how to copy data from an on-premises MongoDB to an Azure Blob Storage.</span></span> <span data-ttu-id="82f6d-198">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="82f6d-198">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="82f6d-199">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="82f6d-199">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="82f6d-200">[OnPremisesMongoDb](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="82f6d-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="82f6d-201">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="82f6d-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="82f6d-202">[MongoDbCollection](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="82f6d-203">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="82f6d-204">具有使用 [MongoDbSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="82f6d-205">此範例會每個小時將資料從 MongoDB 資料庫中的查詢結果複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="82f6d-205">The sample copies data from a query result in MongoDB database to a blob every hour.</span></span> <span data-ttu-id="82f6d-206">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="82f6d-206">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="82f6d-207">第一個步驟是根據 [資料管理閘道](data-factory-data-management-gateway.md) 一文中的指示設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="82f6d-207">As a first step, setup the data management gateway as per the instructions in the [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="82f6d-208">**MongoDB 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="82f6d-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",  
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="82f6d-209">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="82f6d-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="82f6d-210">**MongoDB 輸入資料集：**設定 “external”: ”true” 可告知 Data Factory 服務該資料表是 Data Factory 外部的資料表，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="82f6d-210">**MongoDB input dataset:** Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="82f6d-211">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="82f6d-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="82f6d-212">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="82f6d-213">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="82f6d-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="82f6d-214">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="82f6d-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="82f6d-215">**具有 MongoDB 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="82f6d-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="82f6d-216">此管線包含複製活動，該活動已設定為使用上述輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="82f6d-216">The pipeline contains a Copy Activity that is configured to use the above input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="82f6d-217">在管線 JSON 定義中，**source** 類型設定為 **MongoDbSource**，且 **sink** 類型設定為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="82f6d-217">In the pipeline JSON definition, the **source** type is set to **MongoDbSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="82f6d-218">針對 **query** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="82f6d-219">Data factory 的結構描述</span><span class="sxs-lookup"><span data-stu-id="82f6d-219">Schema by Data Factory</span></span>
<span data-ttu-id="82f6d-220">Azure Data Factory 服務會使用 MongoDB 集合中最新的 100 份文件，從該集合推斷結構描述。</span><span class="sxs-lookup"><span data-stu-id="82f6d-220">Azure Data Factory service infers schema from a MongoDB collection by using the latest 100 documents in the collection.</span></span> <span data-ttu-id="82f6d-221">如果這 100 份文件未包含完整結構描述，則在複製作業期間可能會忽略某些資料行。</span><span class="sxs-lookup"><span data-stu-id="82f6d-221">If these 100 documents do not contain full schema, some columns may be ignored during the copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="82f6d-222">MongoDB 的類型對應</span><span class="sxs-lookup"><span data-stu-id="82f6d-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="82f6d-223">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會使用下列 2 個步驟的方法，執行自動類型轉換，將來源類型轉換成接收類型：</span><span class="sxs-lookup"><span data-stu-id="82f6d-223">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="82f6d-224">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="82f6d-224">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="82f6d-225">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="82f6d-225">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="82f6d-226">將資料移到 MongoDB 時，下列對應會用於從 MongoDB 類型對應至 .NET 類型。</span><span class="sxs-lookup"><span data-stu-id="82f6d-226">When moving data to MongoDB the following mappings are used from MongoDB types to .NET types.</span></span>

| <span data-ttu-id="82f6d-227">MongoDB 類型</span><span class="sxs-lookup"><span data-stu-id="82f6d-227">MongoDB type</span></span> | <span data-ttu-id="82f6d-228">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="82f6d-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="82f6d-229">Binary</span><span class="sxs-lookup"><span data-stu-id="82f6d-229">Binary</span></span> |<span data-ttu-id="82f6d-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="82f6d-230">Byte[]</span></span> |
| <span data-ttu-id="82f6d-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="82f6d-231">Boolean</span></span> |<span data-ttu-id="82f6d-232">Boolean</span><span class="sxs-lookup"><span data-stu-id="82f6d-232">Boolean</span></span> |
| <span data-ttu-id="82f6d-233">日期</span><span class="sxs-lookup"><span data-stu-id="82f6d-233">Date</span></span> |<span data-ttu-id="82f6d-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="82f6d-234">DateTime</span></span> |
| <span data-ttu-id="82f6d-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="82f6d-235">NumberDouble</span></span> |<span data-ttu-id="82f6d-236">兩倍</span><span class="sxs-lookup"><span data-stu-id="82f6d-236">Double</span></span> |
| <span data-ttu-id="82f6d-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="82f6d-237">NumberInt</span></span> |<span data-ttu-id="82f6d-238">Int32</span><span class="sxs-lookup"><span data-stu-id="82f6d-238">Int32</span></span> |
| <span data-ttu-id="82f6d-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="82f6d-239">NumberLong</span></span> |<span data-ttu-id="82f6d-240">Int64</span><span class="sxs-lookup"><span data-stu-id="82f6d-240">Int64</span></span> |
| <span data-ttu-id="82f6d-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="82f6d-241">ObjectID</span></span> |<span data-ttu-id="82f6d-242">String</span><span class="sxs-lookup"><span data-stu-id="82f6d-242">String</span></span> |
| <span data-ttu-id="82f6d-243">String</span><span class="sxs-lookup"><span data-stu-id="82f6d-243">String</span></span> |<span data-ttu-id="82f6d-244">String</span><span class="sxs-lookup"><span data-stu-id="82f6d-244">String</span></span> |
| <span data-ttu-id="82f6d-245">UUID</span><span class="sxs-lookup"><span data-stu-id="82f6d-245">UUID</span></span> |<span data-ttu-id="82f6d-246">Guid</span><span class="sxs-lookup"><span data-stu-id="82f6d-246">Guid</span></span> |
| <span data-ttu-id="82f6d-247">Object</span><span class="sxs-lookup"><span data-stu-id="82f6d-247">Object</span></span> |<span data-ttu-id="82f6d-248">以「_」做為巢狀分隔符號來重新標準化為壓平合併的資料行</span><span class="sxs-lookup"><span data-stu-id="82f6d-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="82f6d-249">若要了解使用虛擬資料表之陣列的支援，請參閱下面的 [使用虛擬資料表之複雜類型的支援](#support-for-complex-types-using-virtual-tables) 一節。</span><span class="sxs-lookup"><span data-stu-id="82f6d-249">To learn about support for arrays using virtual tables, refer to [Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="82f6d-250">目前不支援下列 MongoDB 資料類型︰DBPointer、JavaScript、Max/Min 索引鍵、規則運算式、符號、時間戳記、未定義</span><span class="sxs-lookup"><span data-stu-id="82f6d-250">Currently, the following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="82f6d-251">使用虛擬資料表之複雜類型的支援</span><span class="sxs-lookup"><span data-stu-id="82f6d-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="82f6d-252">Azure Data Factory 會使用內建的 ODBC 驅動程式來連線到 MongoDB 資料庫並從中複製資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-252">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your MongoDB database.</span></span> <span data-ttu-id="82f6d-253">對於其類型會跨文件而不同的陣列或物件等複雜類型，驅動程式會將資料重新標準化為對應的虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="82f6d-253">For complex types such as arrays or objects with different types across the documents, the driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="82f6d-254">具體來說，如果資料表包含這類資料行，則驅動程式會產生下列虛擬資料表︰</span><span class="sxs-lookup"><span data-stu-id="82f6d-254">Specifically, if a table contains such columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="82f6d-255">**基底資料表**，其中包含與實際資料表相同的資料 (複雜類型資料行除外)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-255">A **base table**, which contains the same data as the real table except for the complex type columns.</span></span> <span data-ttu-id="82f6d-256">基底資料表使用與它所代表的實際資料表相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="82f6d-256">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="82f6d-257">每個複雜類型資料行的 **虛擬資料表** ，以展開巢狀資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-257">A **virtual table** for each complex type column, which expands the nested data.</span></span> <span data-ttu-id="82f6d-258">虛擬資料表會使用實際資料表名稱、分隔字元「_」和陣列或物件的名稱來命名。</span><span class="sxs-lookup"><span data-stu-id="82f6d-258">The virtual tables are named using the name of the real table, a separator “_” and the name of the array or object.</span></span>

<span data-ttu-id="82f6d-259">虛擬資料表會參考實際資料表中的資料，讓驅動程式得以存取反正規化的資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-259">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="82f6d-260">如需詳細資訊，請參閱下方的＜範例＞一節。</span><span class="sxs-lookup"><span data-stu-id="82f6d-260">See Example section below details.</span></span> <span data-ttu-id="82f6d-261">您可以藉由查詢和聯結虛擬資料表來存取 MongoDB 陣列的內容。</span><span class="sxs-lookup"><span data-stu-id="82f6d-261">You can access the content of MongoDB arrays by querying and joining the virtual tables.</span></span>

<span data-ttu-id="82f6d-262">您可以使用 [複製精靈](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) ，以直觀方式檢視 MongoDB 資料庫中的資料表清單 (包括虛擬資料表)，並預覽其中的資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-262">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in MongoDB database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="82f6d-263">您也可以在複製精靈中建構查詢，並進行驗證以查看結果。</span><span class="sxs-lookup"><span data-stu-id="82f6d-263">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="82f6d-264">範例</span><span class="sxs-lookup"><span data-stu-id="82f6d-264">Example</span></span>
<span data-ttu-id="82f6d-265">例如，下面的「ExampleTable」就是 MongoDB 資料表，其具有一個在每個儲存格中都有物件陣列的資料行 (「發票」)，以及一個具有純量類型陣列的資料行 (「評等」)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="82f6d-266">_id</span><span class="sxs-lookup"><span data-stu-id="82f6d-266">_id</span></span> | <span data-ttu-id="82f6d-267">客戶名稱</span><span class="sxs-lookup"><span data-stu-id="82f6d-267">Customer Name</span></span> | <span data-ttu-id="82f6d-268">發票</span><span class="sxs-lookup"><span data-stu-id="82f6d-268">Invoices</span></span> | <span data-ttu-id="82f6d-269">服務等級</span><span class="sxs-lookup"><span data-stu-id="82f6d-269">Service Level</span></span> | <span data-ttu-id="82f6d-270">評等</span><span class="sxs-lookup"><span data-stu-id="82f6d-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="82f6d-271">1111</span><span class="sxs-lookup"><span data-stu-id="82f6d-271">1111</span></span> |<span data-ttu-id="82f6d-272">ABC</span><span class="sxs-lookup"><span data-stu-id="82f6d-272">ABC</span></span> |<span data-ttu-id="82f6d-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="82f6d-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="82f6d-274">Silver</span><span class="sxs-lookup"><span data-stu-id="82f6d-274">Silver</span></span> |<span data-ttu-id="82f6d-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="82f6d-275">[5,6]</span></span> |
| <span data-ttu-id="82f6d-276">2222</span><span class="sxs-lookup"><span data-stu-id="82f6d-276">2222</span></span> |<span data-ttu-id="82f6d-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="82f6d-277">XYZ</span></span> |<span data-ttu-id="82f6d-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="82f6d-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="82f6d-279">Gold</span><span class="sxs-lookup"><span data-stu-id="82f6d-279">Gold</span></span> |<span data-ttu-id="82f6d-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="82f6d-280">[1,2]</span></span> |

<span data-ttu-id="82f6d-281">驅動程式會產生多個代表這個單一資料表的虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="82f6d-281">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="82f6d-282">第一個虛擬資料表是名為「ExampleTable」的基底資料表，如下所示。</span><span class="sxs-lookup"><span data-stu-id="82f6d-282">The first virtual table is the base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="82f6d-283">基底資料表包含原始資料表的所有資料，但來自陣列的資料已省略，並且會在虛擬資料表中展開。</span><span class="sxs-lookup"><span data-stu-id="82f6d-283">The base table contains all the data of the original table, but the data from the arrays has been omitted and is expanded in the virtual tables.</span></span>

| <span data-ttu-id="82f6d-284">_id</span><span class="sxs-lookup"><span data-stu-id="82f6d-284">_id</span></span> | <span data-ttu-id="82f6d-285">客戶名稱</span><span class="sxs-lookup"><span data-stu-id="82f6d-285">Customer Name</span></span> | <span data-ttu-id="82f6d-286">服務等級</span><span class="sxs-lookup"><span data-stu-id="82f6d-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82f6d-287">1111</span><span class="sxs-lookup"><span data-stu-id="82f6d-287">1111</span></span> |<span data-ttu-id="82f6d-288">ABC</span><span class="sxs-lookup"><span data-stu-id="82f6d-288">ABC</span></span> |<span data-ttu-id="82f6d-289">Silver</span><span class="sxs-lookup"><span data-stu-id="82f6d-289">Silver</span></span> |
| <span data-ttu-id="82f6d-290">2222</span><span class="sxs-lookup"><span data-stu-id="82f6d-290">2222</span></span> |<span data-ttu-id="82f6d-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="82f6d-291">XYZ</span></span> |<span data-ttu-id="82f6d-292">Gold</span><span class="sxs-lookup"><span data-stu-id="82f6d-292">Gold</span></span> |

<span data-ttu-id="82f6d-293">下表顯示代表範例中原始陣列的虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="82f6d-293">The following tables show the virtual tables that represent the original arrays in the example.</span></span> <span data-ttu-id="82f6d-294">這些資料表包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="82f6d-294">These tables contain the following:</span></span>

* <span data-ttu-id="82f6d-295">對應到原始陣列資料列 (透過 _id 資料行) 之原始主要索引鍵資料行的往回參考</span><span class="sxs-lookup"><span data-stu-id="82f6d-295">A reference back to the original primary key column corresponding to the row of the original array (via the _id column)</span></span>
* <span data-ttu-id="82f6d-296">資料在原始陣列之位置的指示</span><span class="sxs-lookup"><span data-stu-id="82f6d-296">An indication of the position of the data within the original array</span></span>
* <span data-ttu-id="82f6d-297">陣列內每個元素的展開資料</span><span class="sxs-lookup"><span data-stu-id="82f6d-297">The expanded data for each element within the array</span></span>

<span data-ttu-id="82f6d-298">資料表「ExampleTable_Invoices」：</span><span class="sxs-lookup"><span data-stu-id="82f6d-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="82f6d-299">_id</span><span class="sxs-lookup"><span data-stu-id="82f6d-299">_id</span></span> | <span data-ttu-id="82f6d-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="82f6d-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="82f6d-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="82f6d-301">invoice_id</span></span> | <span data-ttu-id="82f6d-302">item</span><span class="sxs-lookup"><span data-stu-id="82f6d-302">item</span></span> | <span data-ttu-id="82f6d-303">price</span><span class="sxs-lookup"><span data-stu-id="82f6d-303">price</span></span> | <span data-ttu-id="82f6d-304">折扣</span><span class="sxs-lookup"><span data-stu-id="82f6d-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="82f6d-305">1111</span><span class="sxs-lookup"><span data-stu-id="82f6d-305">1111</span></span> |<span data-ttu-id="82f6d-306">0</span><span class="sxs-lookup"><span data-stu-id="82f6d-306">0</span></span> |<span data-ttu-id="82f6d-307">123</span><span class="sxs-lookup"><span data-stu-id="82f6d-307">123</span></span> |<span data-ttu-id="82f6d-308">toaster</span><span class="sxs-lookup"><span data-stu-id="82f6d-308">toaster</span></span> |<span data-ttu-id="82f6d-309">456</span><span class="sxs-lookup"><span data-stu-id="82f6d-309">456</span></span> |<span data-ttu-id="82f6d-310">0.2</span><span class="sxs-lookup"><span data-stu-id="82f6d-310">0.2</span></span> |
| <span data-ttu-id="82f6d-311">1111</span><span class="sxs-lookup"><span data-stu-id="82f6d-311">1111</span></span> |<span data-ttu-id="82f6d-312">1</span><span class="sxs-lookup"><span data-stu-id="82f6d-312">1</span></span> |<span data-ttu-id="82f6d-313">124</span><span class="sxs-lookup"><span data-stu-id="82f6d-313">124</span></span> |<span data-ttu-id="82f6d-314">oven</span><span class="sxs-lookup"><span data-stu-id="82f6d-314">oven</span></span> |<span data-ttu-id="82f6d-315">1235</span><span class="sxs-lookup"><span data-stu-id="82f6d-315">1235</span></span> |<span data-ttu-id="82f6d-316">0.2</span><span class="sxs-lookup"><span data-stu-id="82f6d-316">0.2</span></span> |
| <span data-ttu-id="82f6d-317">2222</span><span class="sxs-lookup"><span data-stu-id="82f6d-317">2222</span></span> |<span data-ttu-id="82f6d-318">0</span><span class="sxs-lookup"><span data-stu-id="82f6d-318">0</span></span> |<span data-ttu-id="82f6d-319">135</span><span class="sxs-lookup"><span data-stu-id="82f6d-319">135</span></span> |<span data-ttu-id="82f6d-320">fridge</span><span class="sxs-lookup"><span data-stu-id="82f6d-320">fridge</span></span> |<span data-ttu-id="82f6d-321">12543</span><span class="sxs-lookup"><span data-stu-id="82f6d-321">12543</span></span> |<span data-ttu-id="82f6d-322">0.0</span><span class="sxs-lookup"><span data-stu-id="82f6d-322">0.0</span></span> |

<span data-ttu-id="82f6d-323">資料表「ExampleTable_Ratings」：</span><span class="sxs-lookup"><span data-stu-id="82f6d-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="82f6d-324">_id</span><span class="sxs-lookup"><span data-stu-id="82f6d-324">_id</span></span> | <span data-ttu-id="82f6d-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="82f6d-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="82f6d-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="82f6d-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82f6d-327">1111</span><span class="sxs-lookup"><span data-stu-id="82f6d-327">1111</span></span> |<span data-ttu-id="82f6d-328">0</span><span class="sxs-lookup"><span data-stu-id="82f6d-328">0</span></span> |<span data-ttu-id="82f6d-329">5</span><span class="sxs-lookup"><span data-stu-id="82f6d-329">5</span></span> |
| <span data-ttu-id="82f6d-330">1111</span><span class="sxs-lookup"><span data-stu-id="82f6d-330">1111</span></span> |<span data-ttu-id="82f6d-331">1</span><span class="sxs-lookup"><span data-stu-id="82f6d-331">1</span></span> |<span data-ttu-id="82f6d-332">6</span><span class="sxs-lookup"><span data-stu-id="82f6d-332">6</span></span> |
| <span data-ttu-id="82f6d-333">2222</span><span class="sxs-lookup"><span data-stu-id="82f6d-333">2222</span></span> |<span data-ttu-id="82f6d-334">0</span><span class="sxs-lookup"><span data-stu-id="82f6d-334">0</span></span> |<span data-ttu-id="82f6d-335">1</span><span class="sxs-lookup"><span data-stu-id="82f6d-335">1</span></span> |
| <span data-ttu-id="82f6d-336">2222</span><span class="sxs-lookup"><span data-stu-id="82f6d-336">2222</span></span> |<span data-ttu-id="82f6d-337">1</span><span class="sxs-lookup"><span data-stu-id="82f6d-337">1</span></span> |<span data-ttu-id="82f6d-338">2</span><span class="sxs-lookup"><span data-stu-id="82f6d-338">2</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="82f6d-339">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="82f6d-339">Map source to sink columns</span></span>
<span data-ttu-id="82f6d-340">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-340">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="82f6d-341">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="82f6d-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="82f6d-342">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="82f6d-342">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="82f6d-343">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="82f6d-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="82f6d-344">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="82f6d-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="82f6d-345">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="82f6d-345">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="82f6d-346">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="82f6d-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="82f6d-347">效能和微調</span><span class="sxs-lookup"><span data-stu-id="82f6d-347">Performance and Tuning</span></span>
<span data-ttu-id="82f6d-348">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="82f6d-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82f6d-349">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82f6d-349">Next Steps</span></span>
<span data-ttu-id="82f6d-350">請參閱 [在內部部署和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文，以取得如何建立資料管線以將資料從內部部署資料存放區移動至 Azure 資料存放區的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="82f6d-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store to an Azure data store.</span></span>
