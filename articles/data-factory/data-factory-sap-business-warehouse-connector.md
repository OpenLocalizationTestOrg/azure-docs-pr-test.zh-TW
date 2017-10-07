---
title: "使用 Azure Data Factory 的 SAP Business Warehouse aaaMove 資料 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 SAP Business Warehouse toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="ec7ec-103">使用 Azure Data Factory 從 SAP Business Warehouse 移動資料</span><span class="sxs-lookup"><span data-stu-id="ec7ec-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="ec7ec-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 SAP Business 倉儲 (BW) 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="ec7ec-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="ec7ec-106">您可以從內部部署 SAP Business Warehouse 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="ec7ec-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ec7ec-108">資料處理站目前只支援將資料從 SAP Business Warehouse tooother 資料存放區，但不是會將資料從其他資料儲存 tooan SAP Business Warehouse 的。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="ec7ec-109">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="ec7ec-109">Supported versions and installation</span></span>
<span data-ttu-id="ec7ec-110">此連接器支援 SAP Business Warehouse 7.x 版。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="ec7ec-111">它支援使用 MDX 查詢從 Infocube 和 QueryCubes (包括 BEx 查詢) 複製資料。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="ec7ec-112">tooenable hello 連線 toohello SAP BW 的執行個體，安裝下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec7ec-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="ec7ec-113">**資料管理閘道器**: tooon 內部部署資料連接的 Data Factory 服務支援 （包括 SAP Business Warehouse） 存放區使用的元件稱為 「 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="ec7ec-114">請參閱有關資料管理閘道器和 hello 閘道設定的逐步指示 toolearn [toocloud 資料存放區的內部部署資料之間移動資料存放區](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="ec7ec-115">即使 hello SAP Business Warehouse 裝載於 Azure IaaS 虛擬機器 (VM) 需要閘道。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="ec7ec-116">您可以在相同的 VM 為 hello 資料儲存，或在不同的 VM 只要 hello 閘道可以連接 toohello 資料庫 hello 安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="ec7ec-117">**SAP NetWeaver 程式庫**hello 閘道機器上。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="ec7ec-118">您可以取得 hello SAP Netweaver 程式庫，從 SAP 管理員，或直接從 hello [SAP 軟體下載中心](https://support.sap.com/swdc)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="ec7ec-119">搜尋 hello **SAP 附註 #1025361** tooget hello 下載位置 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="ec7ec-120">請確定 hello 架構 hello SAP NetWeaver 程式庫 （32 位元或 64 位元） 符合您的閘道安裝。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="ec7ec-121">接著，安裝包含在 hello SAP NetWeaver RFC SDK 相應 toohello SAP 附註的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="ec7ec-122">hello SAP NetWeaver 程式庫也會包含在 hello SAP 用戶端工具安裝中。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="ec7ec-123">將擷取自 hello NetWeaver RFC SDK 至 system32 資料夾中的 hello dll。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ec7ec-124">開始使用</span><span class="sxs-lookup"><span data-stu-id="ec7ec-124">Getting started</span></span>
<span data-ttu-id="ec7ec-125">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="ec7ec-126">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ec7ec-127">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="ec7ec-128">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ec7ec-129">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ec7ec-130">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec7ec-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="ec7ec-131">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ec7ec-132">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="ec7ec-133">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ec7ec-134">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ec7ec-135">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ec7ec-136">具有使用的 toocopy 資料從內部部署 SAP Business Warehouse 的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 SAP Business Warehouse tooAzure Blob 複製](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="ec7ec-137">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooan SAP BW 資料存放區的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="ec7ec-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ec7ec-138">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="ec7ec-138">Linked service properties</span></span>
<span data-ttu-id="ec7ec-139">下表中的 hello 提供 JSON 項目特定 tooSAP 商務倉儲 (BW) 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="ec7ec-140">屬性</span><span class="sxs-lookup"><span data-stu-id="ec7ec-140">Property</span></span> | <span data-ttu-id="ec7ec-141">說明</span><span class="sxs-lookup"><span data-stu-id="ec7ec-141">Description</span></span> | <span data-ttu-id="ec7ec-142">允許的值</span><span class="sxs-lookup"><span data-stu-id="ec7ec-142">Allowed values</span></span> | <span data-ttu-id="ec7ec-143">必要</span><span class="sxs-lookup"><span data-stu-id="ec7ec-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="ec7ec-144">伺服器</span><span class="sxs-lookup"><span data-stu-id="ec7ec-144">server</span></span> | <span data-ttu-id="ec7ec-145">執行個體所在的 hello SAP BW 的 hello 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="ec7ec-146">字串</span><span class="sxs-lookup"><span data-stu-id="ec7ec-146">string</span></span> | <span data-ttu-id="ec7ec-147">是</span><span class="sxs-lookup"><span data-stu-id="ec7ec-147">Yes</span></span>
<span data-ttu-id="ec7ec-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="ec7ec-148">systemNumber</span></span> | <span data-ttu-id="ec7ec-149">Hello SAP BW 系統的系統編號。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="ec7ec-150">以字串表示的二位數十進位數字。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="ec7ec-151">是</span><span class="sxs-lookup"><span data-stu-id="ec7ec-151">Yes</span></span>
<span data-ttu-id="ec7ec-152">clientId</span><span class="sxs-lookup"><span data-stu-id="ec7ec-152">clientId</span></span> | <span data-ttu-id="ec7ec-153">Hello W SAP 系統中的 hello 用戶端的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="ec7ec-154">以字串表示的三位數十進位數字。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="ec7ec-155">是</span><span class="sxs-lookup"><span data-stu-id="ec7ec-155">Yes</span></span>
<span data-ttu-id="ec7ec-156">username</span><span class="sxs-lookup"><span data-stu-id="ec7ec-156">username</span></span> | <span data-ttu-id="ec7ec-157">Hello 使用者具有存取 toohello SAP 伺服器的名稱</span><span class="sxs-lookup"><span data-stu-id="ec7ec-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="ec7ec-158">字串</span><span class="sxs-lookup"><span data-stu-id="ec7ec-158">string</span></span> | <span data-ttu-id="ec7ec-159">是</span><span class="sxs-lookup"><span data-stu-id="ec7ec-159">Yes</span></span>
<span data-ttu-id="ec7ec-160">password</span><span class="sxs-lookup"><span data-stu-id="ec7ec-160">password</span></span> | <span data-ttu-id="ec7ec-161">Hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-161">Password for hello user.</span></span> | <span data-ttu-id="ec7ec-162">字串</span><span class="sxs-lookup"><span data-stu-id="ec7ec-162">string</span></span> | <span data-ttu-id="ec7ec-163">是</span><span class="sxs-lookup"><span data-stu-id="ec7ec-163">Yes</span></span>
<span data-ttu-id="ec7ec-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ec7ec-164">gatewayName</span></span> | <span data-ttu-id="ec7ec-165">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SAP BW 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="ec7ec-166">字串</span><span class="sxs-lookup"><span data-stu-id="ec7ec-166">string</span></span> | <span data-ttu-id="ec7ec-167">是</span><span class="sxs-lookup"><span data-stu-id="ec7ec-167">Yes</span></span>
<span data-ttu-id="ec7ec-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ec7ec-168">encryptedCredential</span></span> | <span data-ttu-id="ec7ec-169">hello 加密認證的字串。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-169">hello encrypted credential string.</span></span> | <span data-ttu-id="ec7ec-170">字串</span><span class="sxs-lookup"><span data-stu-id="ec7ec-170">string</span></span> | <span data-ttu-id="ec7ec-171">否</span><span class="sxs-lookup"><span data-stu-id="ec7ec-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ec7ec-172">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="ec7ec-172">Dataset properties</span></span>
<span data-ttu-id="ec7ec-173">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ec7ec-174">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ec7ec-175">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ec7ec-176">支援的型別 hello SAP BW 資料集沒有特定型別的屬性**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="ec7ec-177">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="ec7ec-177">Copy activity properties</span></span>
<span data-ttu-id="ec7ec-178">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ec7ec-179">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="ec7ec-180">而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="ec7ec-181">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ec7ec-182">複製活動中的來源時的型別**RelationalSource** （包含 SAP BW），下列屬性的 hello 可用 typeProperties 區段中：</span><span class="sxs-lookup"><span data-stu-id="ec7ec-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="ec7ec-183">屬性</span><span class="sxs-lookup"><span data-stu-id="ec7ec-183">Property</span></span> | <span data-ttu-id="ec7ec-184">說明</span><span class="sxs-lookup"><span data-stu-id="ec7ec-184">Description</span></span> | <span data-ttu-id="ec7ec-185">允許的值</span><span class="sxs-lookup"><span data-stu-id="ec7ec-185">Allowed values</span></span> | <span data-ttu-id="ec7ec-186">必要</span><span class="sxs-lookup"><span data-stu-id="ec7ec-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ec7ec-187">query</span><span class="sxs-lookup"><span data-stu-id="ec7ec-187">query</span></span> | <span data-ttu-id="ec7ec-188">指定 hello MDX 查詢 tooread 資料從 hello SAP BW 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="ec7ec-189">MDX 查詢。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-189">MDX query.</span></span> | <span data-ttu-id="ec7ec-190">是</span><span class="sxs-lookup"><span data-stu-id="ec7ec-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="ec7ec-191">JSON 範例： 從 SAP Business Warehouse tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="ec7ec-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="ec7ec-192">hello 下列範例將提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ec7ec-193">這個範例示範如何從 Azure Blob 儲存體的內部部署 SAP Business Warehouse tooan toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="ec7ec-194">不過，資料可以複製**直接**hello 接收所述的 tooany[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ec7ec-195">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="ec7ec-196">它不包含建立 hello 資料處理站的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="ec7ec-197">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="ec7ec-198">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec7ec-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="ec7ec-199">[SapBw](#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="ec7ec-200">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ec7ec-201">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ec7ec-202">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ec7ec-203">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ec7ec-204">hello 範例從 SAP Business Warehouse 執行個體 tooan Azure blob 複製資料的每小時。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="ec7ec-205">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ec7ec-206">第一個步驟中，安裝程式 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="ec7ec-207">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="ec7ec-208">SAP Business Warehouse 連結服務</span><span class="sxs-lookup"><span data-stu-id="ec7ec-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="ec7ec-209">此連結服務連結您的 SAP BW 執行個體 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="ec7ec-210">hello type 屬性設定太**SapBw**。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="ec7ec-211">hello typeProperties > 一節提供 hello SAP BW 的執行個體的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="ec7ec-212">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="ec7ec-212">Azure Storage linked service</span></span>
<span data-ttu-id="ec7ec-213">此連結服務連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="ec7ec-214">hello type 屬性設定太**AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="ec7ec-215">hello typeProperties > 一節提供 hello Azure 儲存體帳戶的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="ec7ec-216">SAP BW 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="ec7ec-216">SAP BW input dataset</span></span>
<span data-ttu-id="ec7ec-217">此資料集定義 hello SAP Business Warehouse 的資料集。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="ec7ec-218">您設定的 hello Data Factory 資料集的 hello 類型太**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="ec7ec-219">目前，您未指定 SAP BW 資料集的任何類型特定屬性。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="ec7ec-220">hello 複製活動定義中的 hello 查詢指定了哪些資料 tooread，從 hello SAP BW 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="ec7ec-221">設定外部屬性 tootrue 通知 hello Data Factory 服務，該 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="ec7ec-222">頻率和間隔 屬性定義 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="ec7ec-223">在此情況下，hello 資料是從讀取 hello SAP BW 的執行個體每小時。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="ec7ec-224">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="ec7ec-224">Azure Blob output dataset</span></span>
<span data-ttu-id="ec7ec-225">此資料集定義 hello 輸出 Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="ec7ec-226">hello type 屬性設定 tooAzureBlob。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="ec7ec-227">hello typeProperties 區段提供從 hello SAP BW 的執行個體複製 hello 資料的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="ec7ec-228">hello 資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ec7ec-229">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ec7ec-230">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="ec7ec-231">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="ec7ec-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="ec7ec-232">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ec7ec-233">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource** （適用於 SAP BW 來源） 和**接收**類型設定得**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ec7ec-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ec7ec-234">指定的 hello hello 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="ec7ec-235">SAP BW 的類型對應</span><span class="sxs-lookup"><span data-stu-id="ec7ec-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="ec7ec-236">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec7ec-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="ec7ec-237">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="ec7ec-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="ec7ec-238">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="ec7ec-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="ec7ec-239">從 SAP BW 資料時，下列對應的 hello 可用從 SAP BW 類型 too.NET 型別。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="ec7ec-240">Hello ABAP 字典中的資料類型</span><span class="sxs-lookup"><span data-stu-id="ec7ec-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="ec7ec-241">.Net 資料類型</span><span class="sxs-lookup"><span data-stu-id="ec7ec-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="ec7ec-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="ec7ec-242">ACCP</span></span> |  <span data-ttu-id="ec7ec-243">int</span><span class="sxs-lookup"><span data-stu-id="ec7ec-243">Int</span></span>
<span data-ttu-id="ec7ec-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="ec7ec-244">CHAR</span></span> | <span data-ttu-id="ec7ec-245">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-245">String</span></span>
<span data-ttu-id="ec7ec-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="ec7ec-246">CLNT</span></span> | <span data-ttu-id="ec7ec-247">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-247">String</span></span>
<span data-ttu-id="ec7ec-248">CURR</span><span class="sxs-lookup"><span data-stu-id="ec7ec-248">CURR</span></span> | <span data-ttu-id="ec7ec-249">十進位</span><span class="sxs-lookup"><span data-stu-id="ec7ec-249">Decimal</span></span>
<span data-ttu-id="ec7ec-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="ec7ec-250">CUKY</span></span> | <span data-ttu-id="ec7ec-251">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-251">String</span></span>
<span data-ttu-id="ec7ec-252">DEC</span><span class="sxs-lookup"><span data-stu-id="ec7ec-252">DEC</span></span> | <span data-ttu-id="ec7ec-253">十進位</span><span class="sxs-lookup"><span data-stu-id="ec7ec-253">Decimal</span></span>
<span data-ttu-id="ec7ec-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="ec7ec-254">FLTP</span></span> | <span data-ttu-id="ec7ec-255">兩倍</span><span class="sxs-lookup"><span data-stu-id="ec7ec-255">Double</span></span>
<span data-ttu-id="ec7ec-256">INT1</span><span class="sxs-lookup"><span data-stu-id="ec7ec-256">INT1</span></span> | <span data-ttu-id="ec7ec-257">位元組</span><span class="sxs-lookup"><span data-stu-id="ec7ec-257">Byte</span></span>
<span data-ttu-id="ec7ec-258">INT2</span><span class="sxs-lookup"><span data-stu-id="ec7ec-258">INT2</span></span> | <span data-ttu-id="ec7ec-259">Int16</span><span class="sxs-lookup"><span data-stu-id="ec7ec-259">Int16</span></span>
<span data-ttu-id="ec7ec-260">INT4</span><span class="sxs-lookup"><span data-stu-id="ec7ec-260">INT4</span></span> | <span data-ttu-id="ec7ec-261">int</span><span class="sxs-lookup"><span data-stu-id="ec7ec-261">Int</span></span>
<span data-ttu-id="ec7ec-262">LANG</span><span class="sxs-lookup"><span data-stu-id="ec7ec-262">LANG</span></span> | <span data-ttu-id="ec7ec-263">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-263">String</span></span>
<span data-ttu-id="ec7ec-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="ec7ec-264">LCHR</span></span> | <span data-ttu-id="ec7ec-265">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-265">String</span></span>
<span data-ttu-id="ec7ec-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="ec7ec-266">LRAW</span></span> | <span data-ttu-id="ec7ec-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ec7ec-267">Byte[]</span></span>
<span data-ttu-id="ec7ec-268">PREC</span><span class="sxs-lookup"><span data-stu-id="ec7ec-268">PREC</span></span> | <span data-ttu-id="ec7ec-269">Int16</span><span class="sxs-lookup"><span data-stu-id="ec7ec-269">Int16</span></span>
<span data-ttu-id="ec7ec-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="ec7ec-270">QUAN</span></span> | <span data-ttu-id="ec7ec-271">十進位</span><span class="sxs-lookup"><span data-stu-id="ec7ec-271">Decimal</span></span>
<span data-ttu-id="ec7ec-272">RAW</span><span class="sxs-lookup"><span data-stu-id="ec7ec-272">RAW</span></span> | <span data-ttu-id="ec7ec-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ec7ec-273">Byte[]</span></span>
<span data-ttu-id="ec7ec-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="ec7ec-274">RAWSTRING</span></span> | <span data-ttu-id="ec7ec-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ec7ec-275">Byte[]</span></span>
<span data-ttu-id="ec7ec-276">STRING</span><span class="sxs-lookup"><span data-stu-id="ec7ec-276">STRING</span></span> | <span data-ttu-id="ec7ec-277">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-277">String</span></span>
<span data-ttu-id="ec7ec-278">單位</span><span class="sxs-lookup"><span data-stu-id="ec7ec-278">UNIT</span></span> | <span data-ttu-id="ec7ec-279">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-279">String</span></span>
<span data-ttu-id="ec7ec-280">DATS</span><span class="sxs-lookup"><span data-stu-id="ec7ec-280">DATS</span></span> | <span data-ttu-id="ec7ec-281">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-281">String</span></span>
<span data-ttu-id="ec7ec-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="ec7ec-282">NUMC</span></span> | <span data-ttu-id="ec7ec-283">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-283">String</span></span>
<span data-ttu-id="ec7ec-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="ec7ec-284">TIMS</span></span> | <span data-ttu-id="ec7ec-285">String</span><span class="sxs-lookup"><span data-stu-id="ec7ec-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="ec7ec-286">toomap 資料行從來源資料集 toocolumns 從接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="ec7ec-287">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="ec7ec-287">Map source toosink columns</span></span>
<span data-ttu-id="ec7ec-288">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="ec7ec-289">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="ec7ec-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="ec7ec-290">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="ec7ec-291">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ec7ec-292">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ec7ec-293">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ec7ec-294">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="ec7ec-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ec7ec-295">效能和微調</span><span class="sxs-lookup"><span data-stu-id="ec7ec-295">Performance and Tuning</span></span>
<span data-ttu-id="ec7ec-296">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="ec7ec-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
