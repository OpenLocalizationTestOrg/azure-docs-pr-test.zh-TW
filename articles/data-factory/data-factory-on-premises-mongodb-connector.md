---
title: "使用 Data Factory MongoDB aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從 MongoDB toomove 資料資料庫使用 Azure Data Factory。"
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
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="31e62-103">使用 Azure Data Factory 從 MongoDB 移動資料</span><span class="sxs-lookup"><span data-stu-id="31e62-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="31e62-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 MongoDB 資料庫中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="31e62-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="31e62-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="31e62-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="31e62-106">您可以從內部部署 MongoDB 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="31e62-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="31e62-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="31e62-108">目前資料處理站都會支援只移動資料的 MongoDB 資料儲存 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooan MongoDB 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="31e62-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="31e62-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="31e62-109">Prerequisites</span></span>
<span data-ttu-id="31e62-110">Hello Azure Data Factory 服務 toobe 無法 tooconnect tooyour 內部 MongoDB 資料庫中，您必須安裝下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="31e62-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="31e62-111">支援的 MongoDB 版本為︰2.4、2.6、3.0 及 3.2。</span><span class="sxs-lookup"><span data-stu-id="31e62-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="31e62-112">資料管理閘道器上 hello 的同一部電腦主機 hello 資料庫或不同的機器 tooavoid 競用資源與 hello 資料庫上。</span><span class="sxs-lookup"><span data-stu-id="31e62-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="31e62-113">資料管理閘道器是軟體保護和管理的方式連接內部部署資料來源 toocloud 服務。</span><span class="sxs-lookup"><span data-stu-id="31e62-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="31e62-114">如需資料管理閘道的詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="31e62-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="31e62-115">請參閱[將資料從內部部署 toocloud 移](data-factory-move-data-between-onprem-and-cloud.md)文件以取得有關設定 hello 閘道資料管線 toomove 資料的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="31e62-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="31e62-116">當您安裝 hello 閘道時，它會自動安裝 Microsoft MongoDB ODBC 驅動程式使用 tooconnect tooMongoDB。</span><span class="sxs-lookup"><span data-stu-id="31e62-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="31e62-117">您需要 toouse hello 閘道 tooconnect tooMongoDB，即使它裝載於 Azure IaaS Vm。</span><span class="sxs-lookup"><span data-stu-id="31e62-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="31e62-118">如果您嘗試在雲端中裝載的 MongoDB tooconnect tooan 執行個體，您也可以在 hello IaaS VM 中安裝 hello 閘道執行個體。</span><span class="sxs-lookup"><span data-stu-id="31e62-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="31e62-119">開始使用</span><span class="sxs-lookup"><span data-stu-id="31e62-119">Getting started</span></span>
<span data-ttu-id="31e62-120">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 MongoDB 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="31e62-121">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="31e62-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="31e62-122">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="31e62-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="31e62-123">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="31e62-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="31e62-124">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="31e62-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="31e62-125">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="31e62-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="31e62-126">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="31e62-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="31e62-127">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="31e62-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="31e62-128">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="31e62-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="31e62-129">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="31e62-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="31e62-130">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="31e62-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="31e62-131">具有使用的 toocopy 資料從內部部署 MongoDB 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 MongoDB tooAzure Blob 複製](#json-example-copy-data-from-mongodb-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="31e62-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="31e62-132">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooMongoDB 來源的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="31e62-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="31e62-133">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="31e62-133">Linked service properties</span></span>
<span data-ttu-id="31e62-134">hello 下表提供的 JSON 特定的項目太**OnPremisesMongoDB**連結服務。</span><span class="sxs-lookup"><span data-stu-id="31e62-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="31e62-135">屬性</span><span class="sxs-lookup"><span data-stu-id="31e62-135">Property</span></span> | <span data-ttu-id="31e62-136">說明</span><span class="sxs-lookup"><span data-stu-id="31e62-136">Description</span></span> | <span data-ttu-id="31e62-137">必要</span><span class="sxs-lookup"><span data-stu-id="31e62-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31e62-138">類型</span><span class="sxs-lookup"><span data-stu-id="31e62-138">type</span></span> |<span data-ttu-id="31e62-139">hello 類型屬性必須設定為： **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="31e62-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="31e62-140">是</span><span class="sxs-lookup"><span data-stu-id="31e62-140">Yes</span></span> |
| <span data-ttu-id="31e62-141">伺服器</span><span class="sxs-lookup"><span data-stu-id="31e62-141">server</span></span> |<span data-ttu-id="31e62-142">IP 位址或主機名稱的 hello MongoDB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="31e62-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="31e62-143">是</span><span class="sxs-lookup"><span data-stu-id="31e62-143">Yes</span></span> |
| <span data-ttu-id="31e62-144">連接埠</span><span class="sxs-lookup"><span data-stu-id="31e62-144">port</span></span> |<span data-ttu-id="31e62-145">Hello MongoDB 伺服器的 TCP 連接埠會使用用戶端連線 toolisten。</span><span class="sxs-lookup"><span data-stu-id="31e62-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="31e62-146">選用，預設值︰27017</span><span class="sxs-lookup"><span data-stu-id="31e62-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="31e62-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="31e62-147">authenticationType</span></span> |<span data-ttu-id="31e62-148">基本或匿名。</span><span class="sxs-lookup"><span data-stu-id="31e62-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="31e62-149">是</span><span class="sxs-lookup"><span data-stu-id="31e62-149">Yes</span></span> |
| <span data-ttu-id="31e62-150">username</span><span class="sxs-lookup"><span data-stu-id="31e62-150">username</span></span> |<span data-ttu-id="31e62-151">使用者帳戶 tooaccess MongoDB。</span><span class="sxs-lookup"><span data-stu-id="31e62-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="31e62-152">是 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="31e62-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="31e62-153">password</span><span class="sxs-lookup"><span data-stu-id="31e62-153">password</span></span> |<span data-ttu-id="31e62-154">Hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="31e62-154">Password for hello user.</span></span> |<span data-ttu-id="31e62-155">是 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="31e62-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="31e62-156">authSource</span><span class="sxs-lookup"><span data-stu-id="31e62-156">authSource</span></span> |<span data-ttu-id="31e62-157">您想 toouse toocheck 您的認證進行驗證的 hello MongoDB 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="31e62-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="31e62-158">選用 (如果使用基本驗證)。</span><span class="sxs-lookup"><span data-stu-id="31e62-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="31e62-159">預設值： 使用 hello 系統管理員帳戶和 hello 使用 databaseName 屬性所指定的資料庫。</span><span class="sxs-lookup"><span data-stu-id="31e62-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="31e62-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="31e62-160">databaseName</span></span> |<span data-ttu-id="31e62-161">您想 tooaccess hello MongoDB 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="31e62-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="31e62-162">是</span><span class="sxs-lookup"><span data-stu-id="31e62-162">Yes</span></span> |
| <span data-ttu-id="31e62-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="31e62-163">gatewayName</span></span> |<span data-ttu-id="31e62-164">Hello 閘道存取 hello 資料存放區的名稱。</span><span class="sxs-lookup"><span data-stu-id="31e62-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="31e62-165">是</span><span class="sxs-lookup"><span data-stu-id="31e62-165">Yes</span></span> |
| <span data-ttu-id="31e62-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="31e62-166">encryptedCredential</span></span> |<span data-ttu-id="31e62-167">由閘道加密的認證。</span><span class="sxs-lookup"><span data-stu-id="31e62-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="31e62-168">選用</span><span class="sxs-lookup"><span data-stu-id="31e62-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="31e62-169">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="31e62-169">Dataset properties</span></span>
<span data-ttu-id="31e62-170">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="31e62-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="31e62-171">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="31e62-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="31e62-172">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="31e62-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="31e62-173">hello typeProperties 區段類型的資料集**MongoDbCollection**具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="31e62-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="31e62-174">屬性</span><span class="sxs-lookup"><span data-stu-id="31e62-174">Property</span></span> | <span data-ttu-id="31e62-175">說明</span><span class="sxs-lookup"><span data-stu-id="31e62-175">Description</span></span> | <span data-ttu-id="31e62-176">必要</span><span class="sxs-lookup"><span data-stu-id="31e62-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31e62-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="31e62-177">collectionName</span></span> |<span data-ttu-id="31e62-178">MongoDB 資料庫中的 hello 集合的名稱。</span><span class="sxs-lookup"><span data-stu-id="31e62-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="31e62-179">是</span><span class="sxs-lookup"><span data-stu-id="31e62-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="31e62-180">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="31e62-180">Copy activity properties</span></span>
<span data-ttu-id="31e62-181">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="31e62-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="31e62-182">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="31e62-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="31e62-183">屬性用於 hello **typeProperties** > 一節的 hello hello 活動另一方面會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="31e62-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="31e62-184">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="31e62-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="31e62-185">當 hello 來源屬於型別**MongoDbSource** typeProperties 節中會使用下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="31e62-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="31e62-186">屬性</span><span class="sxs-lookup"><span data-stu-id="31e62-186">Property</span></span> | <span data-ttu-id="31e62-187">說明</span><span class="sxs-lookup"><span data-stu-id="31e62-187">Description</span></span> | <span data-ttu-id="31e62-188">允許的值</span><span class="sxs-lookup"><span data-stu-id="31e62-188">Allowed values</span></span> | <span data-ttu-id="31e62-189">必要</span><span class="sxs-lookup"><span data-stu-id="31e62-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="31e62-190">query</span><span class="sxs-lookup"><span data-stu-id="31e62-190">query</span></span> |<span data-ttu-id="31e62-191">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="31e62-192">SQL-92 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="31e62-192">SQL-92 query string.</span></span> <span data-ttu-id="31e62-193">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="31e62-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="31e62-194">否 (如果已指定 **dataset** 的 **collectionName**)</span><span class="sxs-lookup"><span data-stu-id="31e62-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="31e62-195">JSON 範例： 從 MongoDB tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="31e62-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="31e62-196">此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="31e62-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="31e62-197">它會顯示如何從 Azure Blob 儲存體的內部部署 MongoDB tooan toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="31e62-198">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="31e62-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="31e62-199">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="31e62-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="31e62-200">[OnPremisesMongoDb](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="31e62-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="31e62-201">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="31e62-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="31e62-202">[MongoDbCollection](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="31e62-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="31e62-203">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="31e62-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="31e62-204">具有使用 [MongoDbSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="31e62-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="31e62-205">hello 範例將資料從查詢結果 MongoDB 資料庫 tooa blob 中的每個小時。</span><span class="sxs-lookup"><span data-stu-id="31e62-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="31e62-206">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="31e62-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="31e62-207">第一個步驟中，安裝程式 hello 資料管理閘道器，根據 hello 中的 hello 指示[資料管理閘道器](data-factory-data-management-gateway.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="31e62-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="31e62-208">**MongoDB 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="31e62-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="31e62-209">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="31e62-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="31e62-210">**MongoDB 輸入資料集：**設定"external":"true"會通知 hello Data Factory 服務的 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。</span><span class="sxs-lookup"><span data-stu-id="31e62-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="31e62-211">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="31e62-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="31e62-212">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="31e62-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="31e62-213">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="31e62-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="31e62-214">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="31e62-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="31e62-215">**具有 MongoDB 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="31e62-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="31e62-216">hello 管線包含設定的 toouse hello 上方輸入和輸出資料集並為每個小時的排程的 toorun 複製活動。</span><span class="sxs-lookup"><span data-stu-id="31e62-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="31e62-217">在 hello 管線 JSON 定義中，hello**來源**類型設定得**MongoDbSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="31e62-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="31e62-218">指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="31e62-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


## <a name="schema-by-data-factory"></a><span data-ttu-id="31e62-219">Data factory 的結構描述</span><span class="sxs-lookup"><span data-stu-id="31e62-219">Schema by Data Factory</span></span>
<span data-ttu-id="31e62-220">Azure Data Factory 服務會使用 hello 集合中的 hello 最新的 100 文件推斷 MongoDB 集合的結構描述。</span><span class="sxs-lookup"><span data-stu-id="31e62-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="31e62-221">如果這些 100 的文件未包含完整的結構描述，可能會 hello 複製作業期間忽略某些資料行。</span><span class="sxs-lookup"><span data-stu-id="31e62-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="31e62-222">MongoDB 的類型對應</span><span class="sxs-lookup"><span data-stu-id="31e62-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="31e62-223">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：</span><span class="sxs-lookup"><span data-stu-id="31e62-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="31e62-224">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="31e62-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="31e62-225">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="31e62-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="31e62-226">當您移動資料 tooMongoDB hello 遵循從 MongoDB 類型 too.NET 型別會使用對應。</span><span class="sxs-lookup"><span data-stu-id="31e62-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="31e62-227">MongoDB 類型</span><span class="sxs-lookup"><span data-stu-id="31e62-227">MongoDB type</span></span> | <span data-ttu-id="31e62-228">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="31e62-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="31e62-229">Binary</span><span class="sxs-lookup"><span data-stu-id="31e62-229">Binary</span></span> |<span data-ttu-id="31e62-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="31e62-230">Byte[]</span></span> |
| <span data-ttu-id="31e62-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="31e62-231">Boolean</span></span> |<span data-ttu-id="31e62-232">Boolean</span><span class="sxs-lookup"><span data-stu-id="31e62-232">Boolean</span></span> |
| <span data-ttu-id="31e62-233">日期</span><span class="sxs-lookup"><span data-stu-id="31e62-233">Date</span></span> |<span data-ttu-id="31e62-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="31e62-234">DateTime</span></span> |
| <span data-ttu-id="31e62-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="31e62-235">NumberDouble</span></span> |<span data-ttu-id="31e62-236">兩倍</span><span class="sxs-lookup"><span data-stu-id="31e62-236">Double</span></span> |
| <span data-ttu-id="31e62-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="31e62-237">NumberInt</span></span> |<span data-ttu-id="31e62-238">Int32</span><span class="sxs-lookup"><span data-stu-id="31e62-238">Int32</span></span> |
| <span data-ttu-id="31e62-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="31e62-239">NumberLong</span></span> |<span data-ttu-id="31e62-240">Int64</span><span class="sxs-lookup"><span data-stu-id="31e62-240">Int64</span></span> |
| <span data-ttu-id="31e62-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="31e62-241">ObjectID</span></span> |<span data-ttu-id="31e62-242">String</span><span class="sxs-lookup"><span data-stu-id="31e62-242">String</span></span> |
| <span data-ttu-id="31e62-243">String</span><span class="sxs-lookup"><span data-stu-id="31e62-243">String</span></span> |<span data-ttu-id="31e62-244">String</span><span class="sxs-lookup"><span data-stu-id="31e62-244">String</span></span> |
| <span data-ttu-id="31e62-245">UUID</span><span class="sxs-lookup"><span data-stu-id="31e62-245">UUID</span></span> |<span data-ttu-id="31e62-246">Guid</span><span class="sxs-lookup"><span data-stu-id="31e62-246">Guid</span></span> |
| <span data-ttu-id="31e62-247">Object</span><span class="sxs-lookup"><span data-stu-id="31e62-247">Object</span></span> |<span data-ttu-id="31e62-248">以「_」做為巢狀分隔符號來重新標準化為壓平合併的資料行</span><span class="sxs-lookup"><span data-stu-id="31e62-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="31e62-249">關於支援使用虛擬資料表，陣列 toolearn 參照太[支援使用虛擬資料表的複雜型別的](#support-for-complex-types-using-virtual-tables)下一節。</span><span class="sxs-lookup"><span data-stu-id="31e62-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="31e62-250">目前不支援下列 MongoDB 資料類型的 hello: DBPointer、 JavaScript、 Max/Min 金鑰，規則運算式、 符號、 Timestamp、 未定義</span><span class="sxs-lookup"><span data-stu-id="31e62-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="31e62-251">使用虛擬資料表之複雜類型的支援</span><span class="sxs-lookup"><span data-stu-id="31e62-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="31e62-252">Azure Data Factory 會使用內建 ODBC 驅動程式 tooconnect tooand 複製的資料從 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="31e62-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="31e62-253">複雜類型例如陣列或物件與不同類型跨 hello 文件，hello 驅動程式重新將資料正規化成對應的虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="31e62-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="31e62-254">具體來說，如果資料表包含這類資料行，hello 驅動程式會產生下列虛擬資料表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="31e62-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="31e62-255">A**基底資料表**，其中包含 hello 與 hello hello 複雜型別資料行除外真正的資料表相同的資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="31e62-256">hello 基底資料表使用名稱相同的 hello 為 hello 它所代表的實際資料表。</span><span class="sxs-lookup"><span data-stu-id="31e62-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="31e62-257">A**虛擬資料表**每個複雜型別資料行，這樣會將巢狀的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="31e62-258">使用 hello hello 真正的資料表名稱、"_"分隔字元和 hello hello 陣列或物件名稱來命名 hello 虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="31e62-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="31e62-259">虛擬資料表，請參閱 toohello hello 真正的資料表中的資料，啟用 hello 驅動程式 tooaccess hello 非正規化的資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="31e62-260">如需詳細資訊，請參閱下方的＜範例＞一節。</span><span class="sxs-lookup"><span data-stu-id="31e62-260">See Example section below details.</span></span> <span data-ttu-id="31e62-261">您可以存取 MongoDB 陣列 hello 的內容查詢及聯結 hello 虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="31e62-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="31e62-262">您可以使用 hello[複製精靈](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity)toointuitively 檢視 hello MongoDB 資料庫包括 hello 虛擬資料表中的資料表清單，並預覽 hello 內的資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="31e62-263">您也可以建構 hello 複製精靈中的查詢，並驗證 toosee hello 結果。</span><span class="sxs-lookup"><span data-stu-id="31e62-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="31e62-264">範例</span><span class="sxs-lookup"><span data-stu-id="31e62-264">Example</span></span>
<span data-ttu-id="31e62-265">例如，下面的「ExampleTable」就是 MongoDB 資料表，其具有一個在每個儲存格中都有物件陣列的資料行 (「發票」)，以及一個具有純量類型陣列的資料行 (「評等」)。</span><span class="sxs-lookup"><span data-stu-id="31e62-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="31e62-266">_id</span><span class="sxs-lookup"><span data-stu-id="31e62-266">_id</span></span> | <span data-ttu-id="31e62-267">客戶名稱</span><span class="sxs-lookup"><span data-stu-id="31e62-267">Customer Name</span></span> | <span data-ttu-id="31e62-268">發票</span><span class="sxs-lookup"><span data-stu-id="31e62-268">Invoices</span></span> | <span data-ttu-id="31e62-269">服務等級</span><span class="sxs-lookup"><span data-stu-id="31e62-269">Service Level</span></span> | <span data-ttu-id="31e62-270">評等</span><span class="sxs-lookup"><span data-stu-id="31e62-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="31e62-271">1111</span><span class="sxs-lookup"><span data-stu-id="31e62-271">1111</span></span> |<span data-ttu-id="31e62-272">ABC</span><span class="sxs-lookup"><span data-stu-id="31e62-272">ABC</span></span> |<span data-ttu-id="31e62-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span><span class="sxs-lookup"><span data-stu-id="31e62-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="31e62-274">Silver</span><span class="sxs-lookup"><span data-stu-id="31e62-274">Silver</span></span> |<span data-ttu-id="31e62-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="31e62-275">[5,6]</span></span> |
| <span data-ttu-id="31e62-276">2222</span><span class="sxs-lookup"><span data-stu-id="31e62-276">2222</span></span> |<span data-ttu-id="31e62-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="31e62-277">XYZ</span></span> |<span data-ttu-id="31e62-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="31e62-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="31e62-279">Gold</span><span class="sxs-lookup"><span data-stu-id="31e62-279">Gold</span></span> |<span data-ttu-id="31e62-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="31e62-280">[1,2]</span></span> |

<span data-ttu-id="31e62-281">hello 驅動程式會產生多個虛擬資料表 toorepresent 這個單一資料表。</span><span class="sxs-lookup"><span data-stu-id="31e62-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="31e62-282">hello 的第一個虛擬資料表是名為"ExampleTable 」，如下所示的 hello 基底資料表。</span><span class="sxs-lookup"><span data-stu-id="31e62-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="31e62-283">hello 基底資料表包含所有 hello 資料的 hello 原始資料表中，但已省略和展開 hello 虛擬資料表中的 hello hello 陣列資料。</span><span class="sxs-lookup"><span data-stu-id="31e62-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="31e62-284">_id</span><span class="sxs-lookup"><span data-stu-id="31e62-284">_id</span></span> | <span data-ttu-id="31e62-285">客戶名稱</span><span class="sxs-lookup"><span data-stu-id="31e62-285">Customer Name</span></span> | <span data-ttu-id="31e62-286">服務等級</span><span class="sxs-lookup"><span data-stu-id="31e62-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31e62-287">1111</span><span class="sxs-lookup"><span data-stu-id="31e62-287">1111</span></span> |<span data-ttu-id="31e62-288">ABC</span><span class="sxs-lookup"><span data-stu-id="31e62-288">ABC</span></span> |<span data-ttu-id="31e62-289">Silver</span><span class="sxs-lookup"><span data-stu-id="31e62-289">Silver</span></span> |
| <span data-ttu-id="31e62-290">2222</span><span class="sxs-lookup"><span data-stu-id="31e62-290">2222</span></span> |<span data-ttu-id="31e62-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="31e62-291">XYZ</span></span> |<span data-ttu-id="31e62-292">Gold</span><span class="sxs-lookup"><span data-stu-id="31e62-292">Gold</span></span> |

<span data-ttu-id="31e62-293">hello 下列表格顯示 hello 代表 hello 範例中的 hello 原始陣列的虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="31e62-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="31e62-294">這些資料表包含下列 hello:</span><span class="sxs-lookup"><span data-stu-id="31e62-294">These tables contain hello following:</span></span>

* <span data-ttu-id="31e62-295">參考後 toohello 原始主要索引鍵資料行對應 toohello 資料列的 hello 原始陣列 （透過 hello _id 資料行）</span><span class="sxs-lookup"><span data-stu-id="31e62-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="31e62-296">Hello hello 原始陣列中的 hello 資料位置的指示</span><span class="sxs-lookup"><span data-stu-id="31e62-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="31e62-297">hello 展開每個項目 hello 陣列中的資料</span><span class="sxs-lookup"><span data-stu-id="31e62-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="31e62-298">資料表「ExampleTable_Invoices」：</span><span class="sxs-lookup"><span data-stu-id="31e62-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="31e62-299">_id</span><span class="sxs-lookup"><span data-stu-id="31e62-299">_id</span></span> | <span data-ttu-id="31e62-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="31e62-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="31e62-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="31e62-301">invoice_id</span></span> | <span data-ttu-id="31e62-302">item</span><span class="sxs-lookup"><span data-stu-id="31e62-302">item</span></span> | <span data-ttu-id="31e62-303">price</span><span class="sxs-lookup"><span data-stu-id="31e62-303">price</span></span> | <span data-ttu-id="31e62-304">折扣</span><span class="sxs-lookup"><span data-stu-id="31e62-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="31e62-305">1111</span><span class="sxs-lookup"><span data-stu-id="31e62-305">1111</span></span> |<span data-ttu-id="31e62-306">0</span><span class="sxs-lookup"><span data-stu-id="31e62-306">0</span></span> |<span data-ttu-id="31e62-307">123</span><span class="sxs-lookup"><span data-stu-id="31e62-307">123</span></span> |<span data-ttu-id="31e62-308">toaster</span><span class="sxs-lookup"><span data-stu-id="31e62-308">toaster</span></span> |<span data-ttu-id="31e62-309">456</span><span class="sxs-lookup"><span data-stu-id="31e62-309">456</span></span> |<span data-ttu-id="31e62-310">0.2</span><span class="sxs-lookup"><span data-stu-id="31e62-310">0.2</span></span> |
| <span data-ttu-id="31e62-311">1111</span><span class="sxs-lookup"><span data-stu-id="31e62-311">1111</span></span> |<span data-ttu-id="31e62-312">1</span><span class="sxs-lookup"><span data-stu-id="31e62-312">1</span></span> |<span data-ttu-id="31e62-313">124</span><span class="sxs-lookup"><span data-stu-id="31e62-313">124</span></span> |<span data-ttu-id="31e62-314">oven</span><span class="sxs-lookup"><span data-stu-id="31e62-314">oven</span></span> |<span data-ttu-id="31e62-315">1235</span><span class="sxs-lookup"><span data-stu-id="31e62-315">1235</span></span> |<span data-ttu-id="31e62-316">0.2</span><span class="sxs-lookup"><span data-stu-id="31e62-316">0.2</span></span> |
| <span data-ttu-id="31e62-317">2222</span><span class="sxs-lookup"><span data-stu-id="31e62-317">2222</span></span> |<span data-ttu-id="31e62-318">0</span><span class="sxs-lookup"><span data-stu-id="31e62-318">0</span></span> |<span data-ttu-id="31e62-319">135</span><span class="sxs-lookup"><span data-stu-id="31e62-319">135</span></span> |<span data-ttu-id="31e62-320">fridge</span><span class="sxs-lookup"><span data-stu-id="31e62-320">fridge</span></span> |<span data-ttu-id="31e62-321">12543</span><span class="sxs-lookup"><span data-stu-id="31e62-321">12543</span></span> |<span data-ttu-id="31e62-322">0.0</span><span class="sxs-lookup"><span data-stu-id="31e62-322">0.0</span></span> |

<span data-ttu-id="31e62-323">資料表「ExampleTable_Ratings」：</span><span class="sxs-lookup"><span data-stu-id="31e62-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="31e62-324">_id</span><span class="sxs-lookup"><span data-stu-id="31e62-324">_id</span></span> | <span data-ttu-id="31e62-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="31e62-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="31e62-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="31e62-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31e62-327">1111</span><span class="sxs-lookup"><span data-stu-id="31e62-327">1111</span></span> |<span data-ttu-id="31e62-328">0</span><span class="sxs-lookup"><span data-stu-id="31e62-328">0</span></span> |<span data-ttu-id="31e62-329">5</span><span class="sxs-lookup"><span data-stu-id="31e62-329">5</span></span> |
| <span data-ttu-id="31e62-330">1111</span><span class="sxs-lookup"><span data-stu-id="31e62-330">1111</span></span> |<span data-ttu-id="31e62-331">1</span><span class="sxs-lookup"><span data-stu-id="31e62-331">1</span></span> |<span data-ttu-id="31e62-332">6</span><span class="sxs-lookup"><span data-stu-id="31e62-332">6</span></span> |
| <span data-ttu-id="31e62-333">2222</span><span class="sxs-lookup"><span data-stu-id="31e62-333">2222</span></span> |<span data-ttu-id="31e62-334">0</span><span class="sxs-lookup"><span data-stu-id="31e62-334">0</span></span> |<span data-ttu-id="31e62-335">1</span><span class="sxs-lookup"><span data-stu-id="31e62-335">1</span></span> |
| <span data-ttu-id="31e62-336">2222</span><span class="sxs-lookup"><span data-stu-id="31e62-336">2222</span></span> |<span data-ttu-id="31e62-337">1</span><span class="sxs-lookup"><span data-stu-id="31e62-337">1</span></span> |<span data-ttu-id="31e62-338">2</span><span class="sxs-lookup"><span data-stu-id="31e62-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="31e62-339">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="31e62-339">Map source toosink columns</span></span>
<span data-ttu-id="31e62-340">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="31e62-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="31e62-341">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="31e62-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="31e62-342">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="31e62-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="31e62-343">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="31e62-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="31e62-344">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="31e62-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="31e62-345">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="31e62-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="31e62-346">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="31e62-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="31e62-347">效能和微調</span><span class="sxs-lookup"><span data-stu-id="31e62-347">Performance and Tuning</span></span>
<span data-ttu-id="31e62-348">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="31e62-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31e62-349">後續步驟</span><span class="sxs-lookup"><span data-stu-id="31e62-349">Next Steps</span></span>
<span data-ttu-id="31e62-350">請參閱[在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)為建立在資料管線將資料從內部部署資料存放區 tooan Azure 的資料存放區，如需逐步指示發行項。</span><span class="sxs-lookup"><span data-stu-id="31e62-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
