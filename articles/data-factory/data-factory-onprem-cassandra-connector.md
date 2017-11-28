---
title: "使用 Data Factory Cassandra aaaMove 資料 |Microsoft 文件"
description: "深入了解如何從內部部署 Cassandra toomove 資料資料庫使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="128c3-103">使用 Azure Data Factory 從內部部署的 Cassandra 資料庫移動資料</span><span class="sxs-lookup"><span data-stu-id="128c3-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="128c3-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 Cassandra 資料庫中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="128c3-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="128c3-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="128c3-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="128c3-106">您可以從內部部署 Cassandra 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="128c3-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="128c3-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="128c3-108">目前資料處理站都會支援只移動資料的 Cassandra 資料儲存 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooa Cassandra 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="128c3-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="128c3-109">支援的版本</span><span class="sxs-lookup"><span data-stu-id="128c3-109">Supported versions</span></span>
<span data-ttu-id="128c3-110">hello Cassandra 連接器支援下列版本的 Cassandra hello: 2.X。</span><span class="sxs-lookup"><span data-stu-id="128c3-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="128c3-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="128c3-111">Prerequisites</span></span>
<span data-ttu-id="128c3-112">Hello Azure Data Factory 服務 toobe 無法 tooconnect tooyour 內部 Cassandra 資料庫中，您必須安裝資料管理閘道器上 hello 相同機器該主機 hello 資料庫或不同的機器 tooavoid 競用資源以 hello資料庫。</span><span class="sxs-lookup"><span data-stu-id="128c3-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="128c3-113">資料管理閘道器是安全、 受管理的方式連接到內部部署資料來源 toocloud 服務。</span><span class="sxs-lookup"><span data-stu-id="128c3-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="128c3-114">如需資料管理閘道的詳細資料，請參閱 [資料管理閘道](data-factory-data-management-gateway.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="128c3-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="128c3-115">請參閱[將資料從內部部署 toocloud 移](data-factory-move-data-between-onprem-and-cloud.md)文件以取得有關設定 hello 閘道資料管線 toomove 資料的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="128c3-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="128c3-116">即使 hello 資料庫裝載於 hello 雲端，例如，在 Azure IaaS VM 上，您必須使用 hello 閘道 tooconnect tooa Cassandra 資料庫。</span><span class="sxs-lookup"><span data-stu-id="128c3-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="128c3-117">您可以在擁有 hello 閘道的 Y hello 相同的 VM 主機 hello 資料庫或個別 VM 只要 hello 閘道上可以連接 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="128c3-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="128c3-118">當您安裝 hello 閘道時，它會自動安裝 Microsoft Cassandra ODBC 驅動程式使用 tooconnect tooCassandra 資料庫。</span><span class="sxs-lookup"><span data-stu-id="128c3-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="128c3-119">因此，您不需要 toomanually hello 閘道機器上安裝任何驅動程式從 hello Cassandra 資料庫複製資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="128c3-120">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="128c3-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="128c3-121">開始使用</span><span class="sxs-lookup"><span data-stu-id="128c3-121">Getting started</span></span>
<span data-ttu-id="128c3-122">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="128c3-123">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="128c3-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="128c3-124">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="128c3-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="128c3-125">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="128c3-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="128c3-126">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="128c3-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="128c3-127">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="128c3-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="128c3-128">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="128c3-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="128c3-129">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="128c3-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="128c3-130">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="128c3-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="128c3-131">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="128c3-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="128c3-132">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="128c3-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="128c3-133">具有使用的 toocopy 資料從內部部署 Cassandra 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Cassandra tooAzure Blob 複製](#json-example-copy-data-from-cassandra-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="128c3-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="128c3-134">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa Cassandra 資料存放區的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="128c3-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="128c3-135">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="128c3-135">Linked service properties</span></span>
<span data-ttu-id="128c3-136">下表中的 hello 提供 JSON 項目特定 tooCassandra 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="128c3-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="128c3-137">屬性</span><span class="sxs-lookup"><span data-stu-id="128c3-137">Property</span></span> | <span data-ttu-id="128c3-138">說明</span><span class="sxs-lookup"><span data-stu-id="128c3-138">Description</span></span> | <span data-ttu-id="128c3-139">必要</span><span class="sxs-lookup"><span data-stu-id="128c3-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="128c3-140">類型</span><span class="sxs-lookup"><span data-stu-id="128c3-140">type</span></span> |<span data-ttu-id="128c3-141">hello 類型屬性必須設定為： **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="128c3-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="128c3-142">是</span><span class="sxs-lookup"><span data-stu-id="128c3-142">Yes</span></span> |
| <span data-ttu-id="128c3-143">主機</span><span class="sxs-lookup"><span data-stu-id="128c3-143">host</span></span> |<span data-ttu-id="128c3-144">一或多個 Cassandra 伺服器 IP 位址或主機名稱。</span><span class="sxs-lookup"><span data-stu-id="128c3-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="128c3-145">同時指定以逗號分隔的 IP 位址或主機名稱 tooconnect tooall 伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="128c3-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="128c3-146">是</span><span class="sxs-lookup"><span data-stu-id="128c3-146">Yes</span></span> |
| <span data-ttu-id="128c3-147">連接埠</span><span class="sxs-lookup"><span data-stu-id="128c3-147">port</span></span> |<span data-ttu-id="128c3-148">hello hello Cassandra 伺服器的 TCP 連接埠會使用用戶端連線 toolisten。</span><span class="sxs-lookup"><span data-stu-id="128c3-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="128c3-149">否，預設值：9042</span><span class="sxs-lookup"><span data-stu-id="128c3-149">No, default value: 9042</span></span> |
| <span data-ttu-id="128c3-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="128c3-150">authenticationType</span></span> |<span data-ttu-id="128c3-151">基本或匿名</span><span class="sxs-lookup"><span data-stu-id="128c3-151">Basic, or Anonymous</span></span> |<span data-ttu-id="128c3-152">是</span><span class="sxs-lookup"><span data-stu-id="128c3-152">Yes</span></span> |
| <span data-ttu-id="128c3-153">username</span><span class="sxs-lookup"><span data-stu-id="128c3-153">username</span></span> |<span data-ttu-id="128c3-154">指定 hello 使用者帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="128c3-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="128c3-155">是，如果設定 tooBasic authenticationType。</span><span class="sxs-lookup"><span data-stu-id="128c3-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="128c3-156">password</span><span class="sxs-lookup"><span data-stu-id="128c3-156">password</span></span> |<span data-ttu-id="128c3-157">指定 hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="128c3-157">Specify password for hello user account.</span></span> |<span data-ttu-id="128c3-158">是，如果設定 tooBasic authenticationType。</span><span class="sxs-lookup"><span data-stu-id="128c3-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="128c3-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="128c3-159">gatewayName</span></span> |<span data-ttu-id="128c3-160">hello hello 閘道所使用的 tooconnect toohello 內部 Cassandra 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="128c3-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="128c3-161">是</span><span class="sxs-lookup"><span data-stu-id="128c3-161">Yes</span></span> |
| <span data-ttu-id="128c3-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="128c3-162">encryptedCredential</span></span> |<span data-ttu-id="128c3-163">加密的 hello 閘道的認證。</span><span class="sxs-lookup"><span data-stu-id="128c3-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="128c3-164">否</span><span class="sxs-lookup"><span data-stu-id="128c3-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="128c3-165">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="128c3-165">Dataset properties</span></span>
<span data-ttu-id="128c3-166">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="128c3-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="128c3-167">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="128c3-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="128c3-168">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="128c3-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="128c3-169">hello typeProperties 區段類型的資料集**CassandraTable**具有下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="128c3-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="128c3-170">屬性</span><span class="sxs-lookup"><span data-stu-id="128c3-170">Property</span></span> | <span data-ttu-id="128c3-171">說明</span><span class="sxs-lookup"><span data-stu-id="128c3-171">Description</span></span> | <span data-ttu-id="128c3-172">必要</span><span class="sxs-lookup"><span data-stu-id="128c3-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="128c3-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="128c3-173">keyspace</span></span> |<span data-ttu-id="128c3-174">Hello keyspace 或 Cassandra 資料庫中的結構描述的名稱。</span><span class="sxs-lookup"><span data-stu-id="128c3-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="128c3-175">是 (如果未定義 **CassandraSource** 的**查詢**)。</span><span class="sxs-lookup"><span data-stu-id="128c3-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="128c3-176">tableName</span><span class="sxs-lookup"><span data-stu-id="128c3-176">tableName</span></span> |<span data-ttu-id="128c3-177">Cassandra 資料庫中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="128c3-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="128c3-178">是 (如果未定義 **CassandraSource** 的**查詢**)。</span><span class="sxs-lookup"><span data-stu-id="128c3-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="128c3-179">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="128c3-179">Copy activity properties</span></span>
<span data-ttu-id="128c3-180">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="128c3-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="128c3-181">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="128c3-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="128c3-182">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="128c3-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="128c3-183">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="128c3-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="128c3-184">當來源屬於型別**CassandraSource**，typeProperties 節中會使用下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="128c3-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="128c3-185">屬性</span><span class="sxs-lookup"><span data-stu-id="128c3-185">Property</span></span> | <span data-ttu-id="128c3-186">說明</span><span class="sxs-lookup"><span data-stu-id="128c3-186">Description</span></span> | <span data-ttu-id="128c3-187">允許的值</span><span class="sxs-lookup"><span data-stu-id="128c3-187">Allowed values</span></span> | <span data-ttu-id="128c3-188">必要</span><span class="sxs-lookup"><span data-stu-id="128c3-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="128c3-189">query</span><span class="sxs-lookup"><span data-stu-id="128c3-189">query</span></span> |<span data-ttu-id="128c3-190">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="128c3-191">SQL-92 查詢或 CQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="128c3-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="128c3-192">請參閱 [CQL 參考資料](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)。</span><span class="sxs-lookup"><span data-stu-id="128c3-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="128c3-193">當使用 SQL 查詢，指定**keyspace name.table 名稱**想 tooquery toorepresent hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="128c3-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="128c3-194">否 (如果已定義資料集上的 tableName 和 keyspace)。</span><span class="sxs-lookup"><span data-stu-id="128c3-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="128c3-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="128c3-195">consistencyLevel</span></span> |<span data-ttu-id="128c3-196">hello 一致性層級指定幾個複本必須回應 tooa 讀取的要求傳回資料 toohello 用戶端應用程式之前。</span><span class="sxs-lookup"><span data-stu-id="128c3-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="128c3-197">Cassandra 檢查 hello 複本的指定的數目的資料 toosatisfy hello 讀取的要求。</span><span class="sxs-lookup"><span data-stu-id="128c3-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="128c3-198">ONE、TWO、THREE、QUORUM、ALL、LOCAL_QUORUM、EACH_QUORUM、LOCAL_ONE。</span><span class="sxs-lookup"><span data-stu-id="128c3-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="128c3-199">如需詳細資訊，請參閱 [設定資料一致性](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 。</span><span class="sxs-lookup"><span data-stu-id="128c3-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="128c3-200">否。</span><span class="sxs-lookup"><span data-stu-id="128c3-200">No.</span></span> <span data-ttu-id="128c3-201">預設值為 ONE。</span><span class="sxs-lookup"><span data-stu-id="128c3-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="128c3-202">JSON 範例： 從 Cassandra tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="128c3-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="128c3-203">此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="128c3-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="128c3-204">它會顯示如何從內部部署 Cassandra toocopy 資料資料庫 tooan Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="128c3-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="128c3-205">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="128c3-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="128c3-206">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="128c3-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="128c3-207">它不包含建立 hello 資料處理站的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="128c3-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="128c3-208">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="128c3-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="128c3-209">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="128c3-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="128c3-210">[OnPremisesCassandra](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="128c3-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="128c3-211">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="128c3-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="128c3-212">[CassandraTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="128c3-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="128c3-213">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="128c3-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="128c3-214">具有使用 [CassandraSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="128c3-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="128c3-215">**Cassandra 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="128c3-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="128c3-216">這個範例會使用 hello **Cassandra**連結服務。</span><span class="sxs-lookup"><span data-stu-id="128c3-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="128c3-217">請參閱[Cassandra 連結服務](#linked-service-properties)支援這項連結服務的 hello 屬性區段。</span><span class="sxs-lookup"><span data-stu-id="128c3-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="128c3-218">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="128c3-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="128c3-219">**Cassandra 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="128c3-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
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

<span data-ttu-id="128c3-220">設定**外部**太**true**該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="128c3-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="128c3-221">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="128c3-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="128c3-222">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="128c3-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="128c3-223">**具有 Cassandra 來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="128c3-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="128c3-224">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="128c3-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="128c3-225">在 hello 管線 JSON 定義中，hello**來源**類型設定得**CassandraSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="128c3-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="128c3-226">請參閱[RelationalSource 類型屬性](#copy-activity-properties)hello hello RelationalSource 支援之屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="128c3-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="128c3-227">Cassandra 的類型對應</span><span class="sxs-lookup"><span data-stu-id="128c3-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="128c3-228">Cassandra 類型</span><span class="sxs-lookup"><span data-stu-id="128c3-228">Cassandra Type</span></span> | <span data-ttu-id="128c3-229">以 .Net 為基礎的類型</span><span class="sxs-lookup"><span data-stu-id="128c3-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="128c3-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="128c3-230">ASCII</span></span> |<span data-ttu-id="128c3-231">String</span><span class="sxs-lookup"><span data-stu-id="128c3-231">String</span></span> |
| <span data-ttu-id="128c3-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="128c3-232">BIGINT</span></span> |<span data-ttu-id="128c3-233">Int64</span><span class="sxs-lookup"><span data-stu-id="128c3-233">Int64</span></span> |
| <span data-ttu-id="128c3-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="128c3-234">BLOB</span></span> |<span data-ttu-id="128c3-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="128c3-235">Byte[]</span></span> |
| <span data-ttu-id="128c3-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="128c3-236">BOOLEAN</span></span> |<span data-ttu-id="128c3-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="128c3-237">Boolean</span></span> |
| <span data-ttu-id="128c3-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="128c3-238">DECIMAL</span></span> |<span data-ttu-id="128c3-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="128c3-239">Decimal</span></span> |
| <span data-ttu-id="128c3-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="128c3-240">DOUBLE</span></span> |<span data-ttu-id="128c3-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="128c3-241">Double</span></span> |
| <span data-ttu-id="128c3-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="128c3-242">FLOAT</span></span> |<span data-ttu-id="128c3-243">單一</span><span class="sxs-lookup"><span data-stu-id="128c3-243">Single</span></span> |
| <span data-ttu-id="128c3-244">INET</span><span class="sxs-lookup"><span data-stu-id="128c3-244">INET</span></span> |<span data-ttu-id="128c3-245">String</span><span class="sxs-lookup"><span data-stu-id="128c3-245">String</span></span> |
| <span data-ttu-id="128c3-246">INT</span><span class="sxs-lookup"><span data-stu-id="128c3-246">INT</span></span> |<span data-ttu-id="128c3-247">Int32</span><span class="sxs-lookup"><span data-stu-id="128c3-247">Int32</span></span> |
| <span data-ttu-id="128c3-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="128c3-248">TEXT</span></span> |<span data-ttu-id="128c3-249">String</span><span class="sxs-lookup"><span data-stu-id="128c3-249">String</span></span> |
| <span data-ttu-id="128c3-250">時間戳記</span><span class="sxs-lookup"><span data-stu-id="128c3-250">TIMESTAMP</span></span> |<span data-ttu-id="128c3-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="128c3-251">DateTime</span></span> |
| <span data-ttu-id="128c3-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="128c3-252">TIMEUUID</span></span> |<span data-ttu-id="128c3-253">Guid</span><span class="sxs-lookup"><span data-stu-id="128c3-253">Guid</span></span> |
| <span data-ttu-id="128c3-254">UUID</span><span class="sxs-lookup"><span data-stu-id="128c3-254">UUID</span></span> |<span data-ttu-id="128c3-255">Guid</span><span class="sxs-lookup"><span data-stu-id="128c3-255">Guid</span></span> |
| <span data-ttu-id="128c3-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="128c3-256">VARCHAR</span></span> |<span data-ttu-id="128c3-257">String</span><span class="sxs-lookup"><span data-stu-id="128c3-257">String</span></span> |
| <span data-ttu-id="128c3-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="128c3-258">VARINT</span></span> |<span data-ttu-id="128c3-259">十進位</span><span class="sxs-lookup"><span data-stu-id="128c3-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="128c3-260">集合型別 （地圖、 設定、 清單、 等等），請參閱太[使用 Cassandra 集合類型使用的虛擬資料表](#work-with-collections-using-virtual-table)> 一節。</span><span class="sxs-lookup"><span data-stu-id="128c3-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="128c3-261">不支援使用者定義的類型。</span><span class="sxs-lookup"><span data-stu-id="128c3-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="128c3-262">hello 長度的 Binary 資料行和字串資料行的長度不能大於 4000。</span><span class="sxs-lookup"><span data-stu-id="128c3-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="128c3-263">使用虛擬資料表處理集合</span><span class="sxs-lookup"><span data-stu-id="128c3-263">Work with collections using virtual table</span></span>
<span data-ttu-id="128c3-264">Azure Data Factory 會使用內建 ODBC 驅動程式 tooconnect tooand 複製的資料從 Cassandra 資料庫。</span><span class="sxs-lookup"><span data-stu-id="128c3-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="128c3-265">包括地圖、 集合和清單的集合類型，hello 驅動程式會重新 hello 資料正規化成對應的虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="128c3-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="128c3-266">具體來說，如果資料表包含集合中的任何資料行，hello 驅動程式會產生下列虛擬資料表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="128c3-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="128c3-267">A**基底資料表**，其中包含 hello 與 hello hello 集合的資料行除外真正的資料表相同的資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="128c3-268">hello 基底資料表使用名稱相同的 hello 為 hello 它所代表的實際資料表。</span><span class="sxs-lookup"><span data-stu-id="128c3-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="128c3-269">A**虛擬資料表**針對每個集合的資料行，這樣會將巢狀的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="128c3-270">代表集合的 hello 虛擬資料表使用 hello 真正的資料表，來區隔 hello 名稱來命名"*vt*」 以及 hello hello 資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="128c3-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="128c3-271">虛擬資料表，請參閱 toohello hello 真正的資料表中的資料，啟用 hello 驅動程式 tooaccess hello 非正規化的資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="128c3-272">如需詳細資訊，請參閱＜範例＞一節。</span><span class="sxs-lookup"><span data-stu-id="128c3-272">See Example section for details.</span></span> <span data-ttu-id="128c3-273">您可以存取 Cassandra 集合 hello 的內容查詢及聯結 hello 虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="128c3-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="128c3-274">您可以使用 hello[複製精靈](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity)toointuitively 檢視 hello Cassandra 資料庫包括 hello 虛擬資料表中的資料表清單，並預覽 hello 內的資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="128c3-275">您也可以建構 hello 複製精靈中的查詢，並驗證 toosee hello 結果。</span><span class="sxs-lookup"><span data-stu-id="128c3-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="128c3-276">範例</span><span class="sxs-lookup"><span data-stu-id="128c3-276">Example</span></span>
<span data-ttu-id="128c3-277">例如，hello 下列"ExampleTable 」 是 Cassandra 資料庫資料表，其中包含名為"pk_int 」、 名為值的文字資料行、 清單資料行，對應資料行和集資料行 （名為"StringSet 」） 整數主索引鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="128c3-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="128c3-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="128c3-278">pk_int</span></span> | <span data-ttu-id="128c3-279">值</span><span class="sxs-lookup"><span data-stu-id="128c3-279">Value</span></span> | <span data-ttu-id="128c3-280">列出</span><span class="sxs-lookup"><span data-stu-id="128c3-280">List</span></span> | <span data-ttu-id="128c3-281">對應</span><span class="sxs-lookup"><span data-stu-id="128c3-281">Map</span></span> | <span data-ttu-id="128c3-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="128c3-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="128c3-283">1</span><span class="sxs-lookup"><span data-stu-id="128c3-283">1</span></span> |<span data-ttu-id="128c3-284">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="128c3-284">"sample value 1"</span></span> |<span data-ttu-id="128c3-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="128c3-285">["1", "2", "3"]</span></span> |<span data-ttu-id="128c3-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="128c3-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="128c3-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="128c3-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="128c3-288">3</span><span class="sxs-lookup"><span data-stu-id="128c3-288">3</span></span> |<span data-ttu-id="128c3-289">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="128c3-289">"sample value 3"</span></span> |<span data-ttu-id="128c3-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="128c3-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="128c3-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="128c3-291">{"S1": "t"}</span></span> |<span data-ttu-id="128c3-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="128c3-292">{"A", "E"}</span></span> |

<span data-ttu-id="128c3-293">hello 驅動程式會產生多個虛擬資料表 toorepresent 這個單一資料表。</span><span class="sxs-lookup"><span data-stu-id="128c3-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="128c3-294">hello hello 虛擬資料表中的外部索引鍵資料行參考 hello 主索引鍵資料行中 hello 真正的資料表，並指出哪些真實資料表資料列 hello 虛擬資料表資料列對應至。</span><span class="sxs-lookup"><span data-stu-id="128c3-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="128c3-295">hello 的第一個虛擬資料表是 hello 下表會顯示名為"ExampleTable"hello 基底資料表。</span><span class="sxs-lookup"><span data-stu-id="128c3-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="128c3-296">hello 基底資料表包含 hello 與 hello 原始資料庫的資料表除外 hello 集合，也就是省略這個資料表中，然後其他虛擬資料表中，展開節點相同的資料。</span><span class="sxs-lookup"><span data-stu-id="128c3-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="128c3-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="128c3-297">pk_int</span></span> | <span data-ttu-id="128c3-298">值</span><span class="sxs-lookup"><span data-stu-id="128c3-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="128c3-299">1</span><span class="sxs-lookup"><span data-stu-id="128c3-299">1</span></span> |<span data-ttu-id="128c3-300">"sample value 1"</span><span class="sxs-lookup"><span data-stu-id="128c3-300">"sample value 1"</span></span> |
| <span data-ttu-id="128c3-301">3</span><span class="sxs-lookup"><span data-stu-id="128c3-301">3</span></span> |<span data-ttu-id="128c3-302">"sample value 3"</span><span class="sxs-lookup"><span data-stu-id="128c3-302">"sample value 3"</span></span> |

<span data-ttu-id="128c3-303">hello 下列表格顯示 hello renormalize hello hello 清單、 地圖和 StringSet 資料行資料的虛擬資料表。</span><span class="sxs-lookup"><span data-stu-id="128c3-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="128c3-304">名稱結尾是"_index"或"（_k） 」 的 hello 資料行會指出 hello hello 原始清單或地圖中的 hello 資料位置。</span><span class="sxs-lookup"><span data-stu-id="128c3-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="128c3-305">名稱結尾是"_value"hello 資料行包含 hello 展開資料 hello 集合。</span><span class="sxs-lookup"><span data-stu-id="128c3-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="128c3-306">資料表「ExampleTable_vt_List」：</span><span class="sxs-lookup"><span data-stu-id="128c3-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="128c3-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="128c3-307">pk_int</span></span> | <span data-ttu-id="128c3-308">List_index</span><span class="sxs-lookup"><span data-stu-id="128c3-308">List_index</span></span> | <span data-ttu-id="128c3-309">List_value</span><span class="sxs-lookup"><span data-stu-id="128c3-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="128c3-310">1</span><span class="sxs-lookup"><span data-stu-id="128c3-310">1</span></span> |<span data-ttu-id="128c3-311">0</span><span class="sxs-lookup"><span data-stu-id="128c3-311">0</span></span> |<span data-ttu-id="128c3-312">1</span><span class="sxs-lookup"><span data-stu-id="128c3-312">1</span></span> |
| <span data-ttu-id="128c3-313">1</span><span class="sxs-lookup"><span data-stu-id="128c3-313">1</span></span> |<span data-ttu-id="128c3-314">1</span><span class="sxs-lookup"><span data-stu-id="128c3-314">1</span></span> |<span data-ttu-id="128c3-315">2</span><span class="sxs-lookup"><span data-stu-id="128c3-315">2</span></span> |
| <span data-ttu-id="128c3-316">1</span><span class="sxs-lookup"><span data-stu-id="128c3-316">1</span></span> |<span data-ttu-id="128c3-317">2</span><span class="sxs-lookup"><span data-stu-id="128c3-317">2</span></span> |<span data-ttu-id="128c3-318">3</span><span class="sxs-lookup"><span data-stu-id="128c3-318">3</span></span> |
| <span data-ttu-id="128c3-319">3</span><span class="sxs-lookup"><span data-stu-id="128c3-319">3</span></span> |<span data-ttu-id="128c3-320">0</span><span class="sxs-lookup"><span data-stu-id="128c3-320">0</span></span> |<span data-ttu-id="128c3-321">100</span><span class="sxs-lookup"><span data-stu-id="128c3-321">100</span></span> |
| <span data-ttu-id="128c3-322">3</span><span class="sxs-lookup"><span data-stu-id="128c3-322">3</span></span> |<span data-ttu-id="128c3-323">1</span><span class="sxs-lookup"><span data-stu-id="128c3-323">1</span></span> |<span data-ttu-id="128c3-324">101</span><span class="sxs-lookup"><span data-stu-id="128c3-324">101</span></span> |
| <span data-ttu-id="128c3-325">3</span><span class="sxs-lookup"><span data-stu-id="128c3-325">3</span></span> |<span data-ttu-id="128c3-326">2</span><span class="sxs-lookup"><span data-stu-id="128c3-326">2</span></span> |<span data-ttu-id="128c3-327">102</span><span class="sxs-lookup"><span data-stu-id="128c3-327">102</span></span> |
| <span data-ttu-id="128c3-328">3</span><span class="sxs-lookup"><span data-stu-id="128c3-328">3</span></span> |<span data-ttu-id="128c3-329">3</span><span class="sxs-lookup"><span data-stu-id="128c3-329">3</span></span> |<span data-ttu-id="128c3-330">103</span><span class="sxs-lookup"><span data-stu-id="128c3-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="128c3-331">資料表「ExampleTable_vt_Map」：</span><span class="sxs-lookup"><span data-stu-id="128c3-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="128c3-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="128c3-332">pk_int</span></span> | <span data-ttu-id="128c3-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="128c3-333">Map_key</span></span> | <span data-ttu-id="128c3-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="128c3-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="128c3-335">1</span><span class="sxs-lookup"><span data-stu-id="128c3-335">1</span></span> |<span data-ttu-id="128c3-336">S1</span><span class="sxs-lookup"><span data-stu-id="128c3-336">S1</span></span> |<span data-ttu-id="128c3-337">具有使用 </span><span class="sxs-lookup"><span data-stu-id="128c3-337">A</span></span> |
| <span data-ttu-id="128c3-338">1</span><span class="sxs-lookup"><span data-stu-id="128c3-338">1</span></span> |<span data-ttu-id="128c3-339">S2</span><span class="sxs-lookup"><span data-stu-id="128c3-339">S2</span></span> |<span data-ttu-id="128c3-340">b</span><span class="sxs-lookup"><span data-stu-id="128c3-340">b</span></span> |
| <span data-ttu-id="128c3-341">3</span><span class="sxs-lookup"><span data-stu-id="128c3-341">3</span></span> |<span data-ttu-id="128c3-342">S1</span><span class="sxs-lookup"><span data-stu-id="128c3-342">S1</span></span> |<span data-ttu-id="128c3-343">t</span><span class="sxs-lookup"><span data-stu-id="128c3-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="128c3-344">資料表「ExampleTable_vt_StringSet」：</span><span class="sxs-lookup"><span data-stu-id="128c3-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="128c3-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="128c3-345">pk_int</span></span> | <span data-ttu-id="128c3-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="128c3-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="128c3-347">1</span><span class="sxs-lookup"><span data-stu-id="128c3-347">1</span></span> |<span data-ttu-id="128c3-348">具有使用 </span><span class="sxs-lookup"><span data-stu-id="128c3-348">A</span></span> |
| <span data-ttu-id="128c3-349">1</span><span class="sxs-lookup"><span data-stu-id="128c3-349">1</span></span> |<span data-ttu-id="128c3-350">b</span><span class="sxs-lookup"><span data-stu-id="128c3-350">B</span></span> |
| <span data-ttu-id="128c3-351">1</span><span class="sxs-lookup"><span data-stu-id="128c3-351">1</span></span> |<span data-ttu-id="128c3-352">C</span><span class="sxs-lookup"><span data-stu-id="128c3-352">C</span></span> |
| <span data-ttu-id="128c3-353">3</span><span class="sxs-lookup"><span data-stu-id="128c3-353">3</span></span> |<span data-ttu-id="128c3-354">具有使用 </span><span class="sxs-lookup"><span data-stu-id="128c3-354">A</span></span> |
| <span data-ttu-id="128c3-355">3</span><span class="sxs-lookup"><span data-stu-id="128c3-355">3</span></span> |<span data-ttu-id="128c3-356">E</span><span class="sxs-lookup"><span data-stu-id="128c3-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="128c3-357">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="128c3-357">Map source toosink columns</span></span>
<span data-ttu-id="128c3-358">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="128c3-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="128c3-359">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="128c3-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="128c3-360">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="128c3-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="128c3-361">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="128c3-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="128c3-362">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="128c3-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="128c3-363">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="128c3-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="128c3-364">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="128c3-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="128c3-365">效能和微調</span><span class="sxs-lookup"><span data-stu-id="128c3-365">Performance and Tuning</span></span>
<span data-ttu-id="128c3-366">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="128c3-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
