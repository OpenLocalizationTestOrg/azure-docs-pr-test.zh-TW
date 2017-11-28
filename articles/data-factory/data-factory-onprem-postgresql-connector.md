---
title: "aaaMove 資料從 PostgreSQL 使用 Azure Data Factory |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory PostgreSQL 資料庫 toomove 資料。"
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
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="7ced6-103">使用 Azure Data Factory 從 PostgreSQL 移動資料</span><span class="sxs-lookup"><span data-stu-id="7ced6-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="7ced6-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 PostgreSQL 資料庫中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="7ced6-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="7ced6-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="7ced6-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="7ced6-106">您可以從內部部署 PostgreSQL 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="7ced6-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="7ced6-107">如需支援為接收 hello 複製活動的資料存放區的清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="7ced6-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7ced6-108">資料處理站目前支援將資料從 PostgreSQL 資料庫 tooother 資料存放區，但是不會將資料從其他資料儲存 tooan PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7ced6-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7ced6-109">先決條件</span><span class="sxs-lookup"><span data-stu-id="7ced6-109">prerequisites</span></span>

<span data-ttu-id="7ced6-110">資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 PostgreSQL 來源。</span><span class="sxs-lookup"><span data-stu-id="7ced6-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="7ced6-111">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="7ced6-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="7ced6-112">即使 hello PostgreSQL 資料庫裝載於 Azure IaaS VM 需要閘道。</span><span class="sxs-lookup"><span data-stu-id="7ced6-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="7ced6-113">您可以在 hello 相同 IaaS VM 做為 hello 資料儲存或不同的 VM 只要 hello 閘道上可以連接 toohello 資料庫上安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="7ced6-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="7ced6-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="7ced6-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="7ced6-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="7ced6-115">Supported versions and installation</span></span>
<span data-ttu-id="7ced6-116">資料管理閘道器 tooconnect toohello PostgreSQL 資料庫，如安裝 hello [PostgreSQL Ngpsql 資料提供者](http://go.microsoft.com/fwlink/?linkid=282716)2.0.12 或上方上 hello 相同系統 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="7ced6-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="7ced6-117">支援 PostgreSQL 版本 7.4 和以上版本。</span><span class="sxs-lookup"><span data-stu-id="7ced6-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7ced6-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="7ced6-118">Getting started</span></span>
<span data-ttu-id="7ced6-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 PostgreSQL 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="7ced6-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="7ced6-120">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="7ced6-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="7ced6-121">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="7ced6-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="7ced6-122">您也可以使用下列工具 toocreate 管線 hello:</span><span class="sxs-lookup"><span data-stu-id="7ced6-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="7ced6-123">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="7ced6-123">Azure portal</span></span>
    - <span data-ttu-id="7ced6-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7ced6-124">Visual Studio</span></span>
    - <span data-ttu-id="7ced6-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ced6-125">Azure PowerShell</span></span>
    - <span data-ttu-id="7ced6-126">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="7ced6-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="7ced6-127">.NET API</span><span class="sxs-lookup"><span data-stu-id="7ced6-127">.NET API</span></span>
    - <span data-ttu-id="7ced6-128">REST API</span><span class="sxs-lookup"><span data-stu-id="7ced6-128">REST API</span></span>

     <span data-ttu-id="7ced6-129">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="7ced6-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="7ced6-130">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ced6-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="7ced6-131">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="7ced6-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="7ced6-132">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="7ced6-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="7ced6-133">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="7ced6-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="7ced6-134">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="7ced6-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="7ced6-135">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="7ced6-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="7ced6-136">具有使用的 toocopy 資料從內部部署 PostgreSQL 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 PostgreSQL tooAzure Blob 複製](#json-example-copy-data-from-postgresql-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="7ced6-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="7ced6-137">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa PostgreSQL 資料存放區的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="7ced6-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7ced6-138">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="7ced6-138">Linked service properties</span></span>
<span data-ttu-id="7ced6-139">下表中的 hello 提供 JSON 項目特定 tooPostgreSQL 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="7ced6-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="7ced6-140">屬性</span><span class="sxs-lookup"><span data-stu-id="7ced6-140">Property</span></span> | <span data-ttu-id="7ced6-141">說明</span><span class="sxs-lookup"><span data-stu-id="7ced6-141">Description</span></span> | <span data-ttu-id="7ced6-142">必要</span><span class="sxs-lookup"><span data-stu-id="7ced6-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ced6-143">類型</span><span class="sxs-lookup"><span data-stu-id="7ced6-143">type</span></span> |<span data-ttu-id="7ced6-144">hello 類型屬性必須設定為： **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="7ced6-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="7ced6-145">是</span><span class="sxs-lookup"><span data-stu-id="7ced6-145">Yes</span></span> |
| <span data-ttu-id="7ced6-146">伺服器</span><span class="sxs-lookup"><span data-stu-id="7ced6-146">server</span></span> |<span data-ttu-id="7ced6-147">Hello PostgreSQL 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ced6-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="7ced6-148">是</span><span class="sxs-lookup"><span data-stu-id="7ced6-148">Yes</span></span> |
| <span data-ttu-id="7ced6-149">資料庫</span><span class="sxs-lookup"><span data-stu-id="7ced6-149">database</span></span> |<span data-ttu-id="7ced6-150">Hello PostgreSQL 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ced6-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="7ced6-151">是</span><span class="sxs-lookup"><span data-stu-id="7ced6-151">Yes</span></span> |
| <span data-ttu-id="7ced6-152">結構描述</span><span class="sxs-lookup"><span data-stu-id="7ced6-152">schema</span></span> |<span data-ttu-id="7ced6-153">Hello hello 資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="7ced6-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="7ced6-154">hello 結構描述名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7ced6-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="7ced6-155">否</span><span class="sxs-lookup"><span data-stu-id="7ced6-155">No</span></span> |
| <span data-ttu-id="7ced6-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="7ced6-156">authenticationType</span></span> |<span data-ttu-id="7ced6-157">Tooconnect toohello PostgreSQL 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="7ced6-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="7ced6-158">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="7ced6-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="7ced6-159">是</span><span class="sxs-lookup"><span data-stu-id="7ced6-159">Yes</span></span> |
| <span data-ttu-id="7ced6-160">username</span><span class="sxs-lookup"><span data-stu-id="7ced6-160">username</span></span> |<span data-ttu-id="7ced6-161">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="7ced6-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="7ced6-162">否</span><span class="sxs-lookup"><span data-stu-id="7ced6-162">No</span></span> |
| <span data-ttu-id="7ced6-163">password</span><span class="sxs-lookup"><span data-stu-id="7ced6-163">password</span></span> |<span data-ttu-id="7ced6-164">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="7ced6-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="7ced6-165">否</span><span class="sxs-lookup"><span data-stu-id="7ced6-165">No</span></span> |
| <span data-ttu-id="7ced6-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7ced6-166">gatewayName</span></span> |<span data-ttu-id="7ced6-167">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7ced6-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="7ced6-168">是</span><span class="sxs-lookup"><span data-stu-id="7ced6-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="7ced6-169">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="7ced6-169">Dataset properties</span></span>
<span data-ttu-id="7ced6-170">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7ced6-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7ced6-171">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="7ced6-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="7ced6-172">hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ced6-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="7ced6-173">hello typeProperties 區段類型的資料集**RelationalTable** （包括 PostgreSQL 資料集） 具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ced6-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="7ced6-174">屬性</span><span class="sxs-lookup"><span data-stu-id="7ced6-174">Property</span></span> | <span data-ttu-id="7ced6-175">說明</span><span class="sxs-lookup"><span data-stu-id="7ced6-175">Description</span></span> | <span data-ttu-id="7ced6-176">必要</span><span class="sxs-lookup"><span data-stu-id="7ced6-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ced6-177">tableName</span><span class="sxs-lookup"><span data-stu-id="7ced6-177">tableName</span></span> |<span data-ttu-id="7ced6-178">Hello PostgreSQL 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="7ced6-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="7ced6-179">hello tableName 是區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7ced6-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="7ced6-180">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="7ced6-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="7ced6-181">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="7ced6-181">Copy activity properties</span></span>
<span data-ttu-id="7ced6-182">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7ced6-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7ced6-183">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="7ced6-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="7ced6-184">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="7ced6-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="7ced6-185">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="7ced6-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="7ced6-186">當來源屬於型別**RelationalSource** （包括 PostgreSQL），下列屬性的 hello 可用 typeProperties 區段中：</span><span class="sxs-lookup"><span data-stu-id="7ced6-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="7ced6-187">屬性</span><span class="sxs-lookup"><span data-stu-id="7ced6-187">Property</span></span> | <span data-ttu-id="7ced6-188">說明</span><span class="sxs-lookup"><span data-stu-id="7ced6-188">Description</span></span> | <span data-ttu-id="7ced6-189">允許的值</span><span class="sxs-lookup"><span data-stu-id="7ced6-189">Allowed values</span></span> | <span data-ttu-id="7ced6-190">必要</span><span class="sxs-lookup"><span data-stu-id="7ced6-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7ced6-191">query</span><span class="sxs-lookup"><span data-stu-id="7ced6-191">query</span></span> |<span data-ttu-id="7ced6-192">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="7ced6-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="7ced6-193">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="7ced6-193">SQL query string.</span></span> <span data-ttu-id="7ced6-194">例如："query": "select * from \"MySchema\".\"MyTable\""。</span><span class="sxs-lookup"><span data-stu-id="7ced6-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="7ced6-195">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="7ced6-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="7ced6-196">結構描述和資料表名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7ced6-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="7ced6-197">括住在`""`（雙引號） hello 查詢中。</span><span class="sxs-lookup"><span data-stu-id="7ced6-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="7ced6-198">**範例：**</span><span class="sxs-lookup"><span data-stu-id="7ced6-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="7ced6-199">JSON 範例： 從 PostgreSQL tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="7ced6-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="7ced6-200">此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="7ced6-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7ced6-201">它們會顯示如何 toocopy 資料從 PostgreSQL 資料庫 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7ced6-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="7ced6-202">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="7ced6-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="7ced6-203">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="7ced6-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="7ced6-204">它不包含建立 hello 資料處理站的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="7ced6-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="7ced6-205">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="7ced6-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="7ced6-206">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="7ced6-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="7ced6-207">[OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="7ced6-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="7ced6-208">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="7ced6-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7ced6-209">[RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="7ced6-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="7ced6-210">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="7ced6-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7ced6-211">hello[管線](data-factory-create-pipelines.md)與使用複製活動[RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="7ced6-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7ced6-212">hello 範例將資料從 PostgreSQL 資料庫 tooa blob 中的查詢結果的每個小時。</span><span class="sxs-lookup"><span data-stu-id="7ced6-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="7ced6-213">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="7ced6-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="7ced6-214">第一個步驟中，安裝程式 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="7ced6-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="7ced6-215">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="7ced6-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="7ced6-216">**PostgreSQL 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="7ced6-216">**PostgreSQL linked service:**</span></span>

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
<span data-ttu-id="7ced6-217">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="7ced6-217">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="7ced6-218">**PostgreSQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="7ced6-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="7ced6-219">hello 範例假設您已建立資料表"MyTable"中 PostgreSQL 而且包含稱為"timestamp"時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="7ced6-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="7ced6-220">設定`"external": true`該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="7ced6-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="7ced6-221">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="7ced6-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="7ced6-222">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="7ced6-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="7ced6-223">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="7ced6-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="7ced6-224">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="7ced6-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="7ced6-225">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="7ced6-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="7ced6-226">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為每小時排程的 toorun。</span><span class="sxs-lookup"><span data-stu-id="7ced6-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="7ced6-227">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="7ced6-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="7ced6-228">指定 hello SQL 查詢**查詢**屬性選取 hello PostgreSQL 資料庫中的 hello public.usstates 資料表中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7ced6-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

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
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="7ced6-229">PostgreSQL 的類型對應</span><span class="sxs-lookup"><span data-stu-id="7ced6-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="7ced6-230">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)複製活動的文件以 hello 遵循 2 步驟方法執行從來源類型 toosink 類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="7ced6-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="7ced6-231">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="7ced6-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="7ced6-232">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="7ced6-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="7ced6-233">當您移動資料 tooPostgreSQL，hello 下列會使用對應從 PostgreSQL 類型 too.NET 型別。</span><span class="sxs-lookup"><span data-stu-id="7ced6-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="7ced6-234">PostgreSQL 資料庫類型</span><span class="sxs-lookup"><span data-stu-id="7ced6-234">PostgreSQL Database type</span></span> | <span data-ttu-id="7ced6-235">PostgresSQL 別名</span><span class="sxs-lookup"><span data-stu-id="7ced6-235">PostgresSQL aliases</span></span> | <span data-ttu-id="7ced6-236">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="7ced6-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7ced6-237">abstime</span><span class="sxs-lookup"><span data-stu-id="7ced6-237">abstime</span></span> | |<span data-ttu-id="7ced6-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="7ced6-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="7ced6-239">bigint</span><span class="sxs-lookup"><span data-stu-id="7ced6-239">bigint</span></span> |<span data-ttu-id="7ced6-240">int8</span><span class="sxs-lookup"><span data-stu-id="7ced6-240">int8</span></span> |<span data-ttu-id="7ced6-241">Int64</span><span class="sxs-lookup"><span data-stu-id="7ced6-241">Int64</span></span> |
| <span data-ttu-id="7ced6-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="7ced6-242">bigserial</span></span> |<span data-ttu-id="7ced6-243">serial8</span><span class="sxs-lookup"><span data-stu-id="7ced6-243">serial8</span></span> |<span data-ttu-id="7ced6-244">Int64</span><span class="sxs-lookup"><span data-stu-id="7ced6-244">Int64</span></span> |
| <span data-ttu-id="7ced6-245">位元 [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-245">bit [ (n) ]</span></span> | |<span data-ttu-id="7ced6-246">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="7ced6-247">位元不同 [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="7ced6-248">varbit</span><span class="sxs-lookup"><span data-stu-id="7ced6-248">varbit</span></span> |<span data-ttu-id="7ced6-249">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-249">Byte[], String</span></span> |
| <span data-ttu-id="7ced6-250">布林值</span><span class="sxs-lookup"><span data-stu-id="7ced6-250">boolean</span></span> |<span data-ttu-id="7ced6-251">布林</span><span class="sxs-lookup"><span data-stu-id="7ced6-251">bool</span></span> |<span data-ttu-id="7ced6-252">布林值</span><span class="sxs-lookup"><span data-stu-id="7ced6-252">Boolean</span></span> |
| <span data-ttu-id="7ced6-253">方塊</span><span class="sxs-lookup"><span data-stu-id="7ced6-253">box</span></span> | |<span data-ttu-id="7ced6-254">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-255">bytea</span><span class="sxs-lookup"><span data-stu-id="7ced6-255">bytea</span></span> | |<span data-ttu-id="7ced6-256">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-257">字元 [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-257">character [ (n) ]</span></span> |<span data-ttu-id="7ced6-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-258">char [ (n) ]</span></span> |<span data-ttu-id="7ced6-259">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-259">String</span></span> |
| <span data-ttu-id="7ced6-260">字元不同 [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-260">character varying [ (n) ]</span></span> |<span data-ttu-id="7ced6-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-261">varchar [ (n) ]</span></span> |<span data-ttu-id="7ced6-262">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-262">String</span></span> |
| <span data-ttu-id="7ced6-263">cid</span><span class="sxs-lookup"><span data-stu-id="7ced6-263">cid</span></span> | |<span data-ttu-id="7ced6-264">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-264">String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-265">cidr</span><span class="sxs-lookup"><span data-stu-id="7ced6-265">cidr</span></span> | |<span data-ttu-id="7ced6-266">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-266">String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-267">圓形</span><span class="sxs-lookup"><span data-stu-id="7ced6-267">circle</span></span> | |<span data-ttu-id="7ced6-268">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-269">日期</span><span class="sxs-lookup"><span data-stu-id="7ced6-269">date</span></span> | |<span data-ttu-id="7ced6-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="7ced6-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="7ced6-271">daterange</span><span class="sxs-lookup"><span data-stu-id="7ced6-271">daterange</span></span> | |<span data-ttu-id="7ced6-272">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-272">String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-273">雙精度</span><span class="sxs-lookup"><span data-stu-id="7ced6-273">double precision</span></span> |<span data-ttu-id="7ced6-274">float8</span><span class="sxs-lookup"><span data-stu-id="7ced6-274">float8</span></span> |<span data-ttu-id="7ced6-275">兩倍</span><span class="sxs-lookup"><span data-stu-id="7ced6-275">Double</span></span> |
| <span data-ttu-id="7ced6-276">inet</span><span class="sxs-lookup"><span data-stu-id="7ced6-276">inet</span></span> | |<span data-ttu-id="7ced6-277">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-278">intarry</span><span class="sxs-lookup"><span data-stu-id="7ced6-278">intarry</span></span> | |<span data-ttu-id="7ced6-279">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-279">String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-280">int4range</span><span class="sxs-lookup"><span data-stu-id="7ced6-280">int4range</span></span> | |<span data-ttu-id="7ced6-281">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-281">String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-282">int8range</span><span class="sxs-lookup"><span data-stu-id="7ced6-282">int8range</span></span> | |<span data-ttu-id="7ced6-283">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-283">String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-284">integer</span><span class="sxs-lookup"><span data-stu-id="7ced6-284">integer</span></span> |<span data-ttu-id="7ced6-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="7ced6-285">int, int4</span></span> |<span data-ttu-id="7ced6-286">Int32</span><span class="sxs-lookup"><span data-stu-id="7ced6-286">Int32</span></span> |
| <span data-ttu-id="7ced6-287">間隔 [ 欄位 ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="7ced6-288">Timespan</span><span class="sxs-lookup"><span data-stu-id="7ced6-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="7ced6-289">json</span><span class="sxs-lookup"><span data-stu-id="7ced6-289">json</span></span> | |<span data-ttu-id="7ced6-290">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-290">String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="7ced6-291">jsonb</span></span> | |<span data-ttu-id="7ced6-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7ced6-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="7ced6-293">線條</span><span class="sxs-lookup"><span data-stu-id="7ced6-293">line</span></span> | |<span data-ttu-id="7ced6-294">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-295">lseg</span><span class="sxs-lookup"><span data-stu-id="7ced6-295">lseg</span></span> | |<span data-ttu-id="7ced6-296">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="7ced6-297">macaddr</span></span> | |<span data-ttu-id="7ced6-298">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-299">money</span><span class="sxs-lookup"><span data-stu-id="7ced6-299">money</span></span> | |<span data-ttu-id="7ced6-300">十進位</span><span class="sxs-lookup"><span data-stu-id="7ced6-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="7ced6-301">數值 [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="7ced6-302">十進位 [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="7ced6-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="7ced6-303">十進位</span><span class="sxs-lookup"><span data-stu-id="7ced6-303">Decimal</span></span> |
| <span data-ttu-id="7ced6-304">numrange</span><span class="sxs-lookup"><span data-stu-id="7ced6-304">numrange</span></span> | |<span data-ttu-id="7ced6-305">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-305">String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-306">oid</span><span class="sxs-lookup"><span data-stu-id="7ced6-306">oid</span></span> | |<span data-ttu-id="7ced6-307">Int32</span><span class="sxs-lookup"><span data-stu-id="7ced6-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="7ced6-308">路徑</span><span class="sxs-lookup"><span data-stu-id="7ced6-308">path</span></span> | |<span data-ttu-id="7ced6-309">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="7ced6-310">pg_lsn</span></span> | |<span data-ttu-id="7ced6-311">Int64</span><span class="sxs-lookup"><span data-stu-id="7ced6-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="7ced6-312">點</span><span class="sxs-lookup"><span data-stu-id="7ced6-312">point</span></span> | |<span data-ttu-id="7ced6-313">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-314">多邊形</span><span class="sxs-lookup"><span data-stu-id="7ced6-314">polygon</span></span> | |<span data-ttu-id="7ced6-315">Byte[]、String</span><span class="sxs-lookup"><span data-stu-id="7ced6-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="7ced6-316">real</span><span class="sxs-lookup"><span data-stu-id="7ced6-316">real</span></span> |<span data-ttu-id="7ced6-317">float4</span><span class="sxs-lookup"><span data-stu-id="7ced6-317">float4</span></span> |<span data-ttu-id="7ced6-318">單一</span><span class="sxs-lookup"><span data-stu-id="7ced6-318">Single</span></span> |
| <span data-ttu-id="7ced6-319">smallint</span><span class="sxs-lookup"><span data-stu-id="7ced6-319">smallint</span></span> |<span data-ttu-id="7ced6-320">int2</span><span class="sxs-lookup"><span data-stu-id="7ced6-320">int2</span></span> |<span data-ttu-id="7ced6-321">Int16</span><span class="sxs-lookup"><span data-stu-id="7ced6-321">Int16</span></span> |
| <span data-ttu-id="7ced6-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="7ced6-322">smallserial</span></span> |<span data-ttu-id="7ced6-323">serial2</span><span class="sxs-lookup"><span data-stu-id="7ced6-323">serial2</span></span> |<span data-ttu-id="7ced6-324">Int16</span><span class="sxs-lookup"><span data-stu-id="7ced6-324">Int16</span></span> |
| <span data-ttu-id="7ced6-325">serial</span><span class="sxs-lookup"><span data-stu-id="7ced6-325">serial</span></span> |<span data-ttu-id="7ced6-326">serial4</span><span class="sxs-lookup"><span data-stu-id="7ced6-326">serial4</span></span> |<span data-ttu-id="7ced6-327">Int32</span><span class="sxs-lookup"><span data-stu-id="7ced6-327">Int32</span></span> |
| <span data-ttu-id="7ced6-328">文字</span><span class="sxs-lookup"><span data-stu-id="7ced6-328">text</span></span> | |<span data-ttu-id="7ced6-329">String</span><span class="sxs-lookup"><span data-stu-id="7ced6-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="7ced6-330">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="7ced6-330">Map source toosink columns</span></span>
<span data-ttu-id="7ced6-331">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="7ced6-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="7ced6-332">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="7ced6-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="7ced6-333">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="7ced6-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="7ced6-334">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="7ced6-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="7ced6-335">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="7ced6-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="7ced6-336">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="7ced6-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="7ced6-337">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="7ced6-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7ced6-338">效能和微調</span><span class="sxs-lookup"><span data-stu-id="7ced6-338">Performance and Tuning</span></span>
<span data-ttu-id="7ced6-339">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="7ced6-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
