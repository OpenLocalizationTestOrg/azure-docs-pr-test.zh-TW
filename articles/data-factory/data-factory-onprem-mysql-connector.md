---
title: "從使用 Azure Data Factory 的 MySQL aaaMove 資料 |Microsoft 文件"
description: "深入了解如何 toomove 資料從 MySQL 資料庫使用 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="35220-103">使用 Azure Data Factory 從 MySQL 移動資料</span><span class="sxs-lookup"><span data-stu-id="35220-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="35220-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 MySQL 資料庫中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="35220-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="35220-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="35220-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="35220-106">您可以從內部部署 MySQL 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="35220-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="35220-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="35220-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="35220-108">目前資料處理站都會支援只移動資料的 MySQL 資料儲存 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooan MySQL 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="35220-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="35220-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="35220-109">Prerequisites</span></span>
<span data-ttu-id="35220-110">資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 MySQL 來源。</span><span class="sxs-lookup"><span data-stu-id="35220-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="35220-111">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="35220-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="35220-112">即使 hello MySQL 資料庫裝載於 Azure IaaS 虛擬機器 (VM) 需要閘道。</span><span class="sxs-lookup"><span data-stu-id="35220-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="35220-113">您可以在相同的 VM 為 hello 資料儲存，或在不同的 VM 只要 hello 閘道可以連接 toohello 資料庫 hello 安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="35220-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="35220-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="35220-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="35220-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="35220-115">Supported versions and installation</span></span>
<span data-ttu-id="35220-116">資料管理閘道器 tooconnect toohello MySQL 資料庫，您需要 tooinstall hello [Microsoft Windows 的 MySQL Connector/Net](https://dev.mysql.com/downloads/connector/net/) (6.6.5 版本或更新版本) 在 hello 相同系統 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="35220-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="35220-117">支援 MySQL 版本 5.1 和以上版本。</span><span class="sxs-lookup"><span data-stu-id="35220-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="35220-118">如果您在上叫用錯誤"驗證失敗，因為 hello 遠端群體已經關閉 hello 傳輸資料流。 」，請考慮 tooupgrade hello MySQL Connector/Net toohigher 版本。</span><span class="sxs-lookup"><span data-stu-id="35220-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="35220-119">開始使用</span><span class="sxs-lookup"><span data-stu-id="35220-119">Getting started</span></span>
<span data-ttu-id="35220-120">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="35220-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="35220-121">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="35220-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="35220-122">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="35220-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="35220-123">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="35220-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="35220-124">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="35220-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="35220-125">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="35220-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="35220-126">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="35220-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="35220-127">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="35220-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="35220-128">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="35220-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="35220-129">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="35220-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="35220-130">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="35220-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="35220-131">具有使用的 toocopy 資料從內部部署 MySQL 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 MySQL tooAzure Blob 複製](#json-example-copy-data-from-mysql-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="35220-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="35220-132">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa MySQL 資料存放區的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="35220-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="35220-133">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="35220-133">Linked service properties</span></span>
<span data-ttu-id="35220-134">下表中的 hello 提供 JSON 項目特定 tooMySQL 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="35220-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="35220-135">屬性</span><span class="sxs-lookup"><span data-stu-id="35220-135">Property</span></span> | <span data-ttu-id="35220-136">說明</span><span class="sxs-lookup"><span data-stu-id="35220-136">Description</span></span> | <span data-ttu-id="35220-137">必要</span><span class="sxs-lookup"><span data-stu-id="35220-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35220-138">類型</span><span class="sxs-lookup"><span data-stu-id="35220-138">type</span></span> |<span data-ttu-id="35220-139">hello 類型屬性必須設定為： **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="35220-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="35220-140">是</span><span class="sxs-lookup"><span data-stu-id="35220-140">Yes</span></span> |
| <span data-ttu-id="35220-141">伺服器</span><span class="sxs-lookup"><span data-stu-id="35220-141">server</span></span> |<span data-ttu-id="35220-142">Hello MySQL 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="35220-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="35220-143">是</span><span class="sxs-lookup"><span data-stu-id="35220-143">Yes</span></span> |
| <span data-ttu-id="35220-144">資料庫</span><span class="sxs-lookup"><span data-stu-id="35220-144">database</span></span> |<span data-ttu-id="35220-145">Hello MySQL 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="35220-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="35220-146">是</span><span class="sxs-lookup"><span data-stu-id="35220-146">Yes</span></span> |
| <span data-ttu-id="35220-147">結構描述</span><span class="sxs-lookup"><span data-stu-id="35220-147">schema</span></span> |<span data-ttu-id="35220-148">Hello hello 資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="35220-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="35220-149">否</span><span class="sxs-lookup"><span data-stu-id="35220-149">No</span></span> |
| <span data-ttu-id="35220-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="35220-150">authenticationType</span></span> |<span data-ttu-id="35220-151">Tooconnect toohello MySQL 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="35220-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="35220-152">可能的值為：`Basic`。</span><span class="sxs-lookup"><span data-stu-id="35220-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="35220-153">是</span><span class="sxs-lookup"><span data-stu-id="35220-153">Yes</span></span> |
| <span data-ttu-id="35220-154">username</span><span class="sxs-lookup"><span data-stu-id="35220-154">username</span></span> |<span data-ttu-id="35220-155">指定使用者名稱 tooconnect toohello MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="35220-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="35220-156">是</span><span class="sxs-lookup"><span data-stu-id="35220-156">Yes</span></span> |
| <span data-ttu-id="35220-157">password</span><span class="sxs-lookup"><span data-stu-id="35220-157">password</span></span> |<span data-ttu-id="35220-158">指定您所指定的 hello 使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="35220-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="35220-159">是</span><span class="sxs-lookup"><span data-stu-id="35220-159">Yes</span></span> |
| <span data-ttu-id="35220-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="35220-160">gatewayName</span></span> |<span data-ttu-id="35220-161">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="35220-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="35220-162">是</span><span class="sxs-lookup"><span data-stu-id="35220-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="35220-163">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="35220-163">Dataset properties</span></span>
<span data-ttu-id="35220-164">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="35220-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="35220-165">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="35220-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="35220-166">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="35220-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="35220-167">hello typeProperties 區段類型的資料集**RelationalTable** （包括 MySQL 資料集） 具有下列屬性的 hello</span><span class="sxs-lookup"><span data-stu-id="35220-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="35220-168">屬性</span><span class="sxs-lookup"><span data-stu-id="35220-168">Property</span></span> | <span data-ttu-id="35220-169">說明</span><span class="sxs-lookup"><span data-stu-id="35220-169">Description</span></span> | <span data-ttu-id="35220-170">必要</span><span class="sxs-lookup"><span data-stu-id="35220-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="35220-171">tableName</span><span class="sxs-lookup"><span data-stu-id="35220-171">tableName</span></span> |<span data-ttu-id="35220-172">在 hello MySQL 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="35220-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="35220-173">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="35220-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="35220-174">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="35220-174">Copy activity properties</span></span>
<span data-ttu-id="35220-175">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="35220-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="35220-176">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="35220-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="35220-177">而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="35220-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="35220-178">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="35220-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="35220-179">複製活動中的來源時的型別**RelationalSource** （包括 MySQL），下列屬性的 hello 可用 typeProperties 區段中：</span><span class="sxs-lookup"><span data-stu-id="35220-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="35220-180">屬性</span><span class="sxs-lookup"><span data-stu-id="35220-180">Property</span></span> | <span data-ttu-id="35220-181">說明</span><span class="sxs-lookup"><span data-stu-id="35220-181">Description</span></span> | <span data-ttu-id="35220-182">允許的值</span><span class="sxs-lookup"><span data-stu-id="35220-182">Allowed values</span></span> | <span data-ttu-id="35220-183">必要</span><span class="sxs-lookup"><span data-stu-id="35220-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="35220-184">query</span><span class="sxs-lookup"><span data-stu-id="35220-184">query</span></span> |<span data-ttu-id="35220-185">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="35220-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="35220-186">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="35220-186">SQL query string.</span></span> <span data-ttu-id="35220-187">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="35220-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="35220-188">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="35220-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="35220-189">JSON 範例： 將資料從 MySQL tooAzure Blob 複製</span><span class="sxs-lookup"><span data-stu-id="35220-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="35220-190">此範例中提供的範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="35220-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="35220-191">它會顯示如何 toocopy 資料從內部部署 MySQL 資料庫 tooan Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="35220-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="35220-192">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="35220-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="35220-193">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="35220-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="35220-194">它不包含建立 hello 資料處理站的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="35220-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="35220-195">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="35220-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="35220-196">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="35220-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="35220-197">[OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="35220-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="35220-198">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="35220-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="35220-199">[RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="35220-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="35220-200">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="35220-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="35220-201">具有使用 [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="35220-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="35220-202">hello 範例從 MySQL 資料庫 tooa blob 中的查詢結果複製資料的每小時。</span><span class="sxs-lookup"><span data-stu-id="35220-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="35220-203">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="35220-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="35220-204">第一個步驟中，安裝程式 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="35220-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="35220-205">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="35220-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="35220-206">**MySQL 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="35220-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="35220-207">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="35220-207">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="35220-208">**MySQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="35220-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="35220-209">hello 範例假設您已建立資料表"MyTable"MySQL 中，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="35220-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="35220-210">設定"external":"true"會通知 hello Data Factory 服務的 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。</span><span class="sxs-lookup"><span data-stu-id="35220-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
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

<span data-ttu-id="35220-211">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="35220-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="35220-212">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="35220-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="35220-213">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="35220-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="35220-214">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="35220-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="35220-215">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="35220-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="35220-216">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="35220-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="35220-217">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="35220-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="35220-218">指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="35220-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
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
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="35220-219">MySQL 的類型對應</span><span class="sxs-lookup"><span data-stu-id="35220-219">Type mapping for MySQL</span></span>
<span data-ttu-id="35220-220">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="35220-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="35220-221">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="35220-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="35220-222">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="35220-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="35220-223">當您移動資料 tooMySQL，hello 下列會使用對應從 MySQL 類型 too.NET 型別。</span><span class="sxs-lookup"><span data-stu-id="35220-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="35220-224">MySQL 資料庫類型</span><span class="sxs-lookup"><span data-stu-id="35220-224">MySQL Database type</span></span> | <span data-ttu-id="35220-225">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="35220-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="35220-226">不帶正負號的 bigint</span><span class="sxs-lookup"><span data-stu-id="35220-226">bigint unsigned</span></span> |<span data-ttu-id="35220-227">十進位</span><span class="sxs-lookup"><span data-stu-id="35220-227">Decimal</span></span> |
| <span data-ttu-id="35220-228">bigint</span><span class="sxs-lookup"><span data-stu-id="35220-228">bigint</span></span> |<span data-ttu-id="35220-229">Int64</span><span class="sxs-lookup"><span data-stu-id="35220-229">Int64</span></span> |
| <span data-ttu-id="35220-230">bit</span><span class="sxs-lookup"><span data-stu-id="35220-230">bit</span></span> |<span data-ttu-id="35220-231">十進位</span><span class="sxs-lookup"><span data-stu-id="35220-231">Decimal</span></span> |
| <span data-ttu-id="35220-232">blob</span><span class="sxs-lookup"><span data-stu-id="35220-232">blob</span></span> |<span data-ttu-id="35220-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="35220-233">Byte[]</span></span> |
| <span data-ttu-id="35220-234">布林</span><span class="sxs-lookup"><span data-stu-id="35220-234">bool</span></span> |<span data-ttu-id="35220-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="35220-235">Boolean</span></span> |
| <span data-ttu-id="35220-236">char</span><span class="sxs-lookup"><span data-stu-id="35220-236">char</span></span> |<span data-ttu-id="35220-237">String</span><span class="sxs-lookup"><span data-stu-id="35220-237">String</span></span> |
| <span data-ttu-id="35220-238">日期</span><span class="sxs-lookup"><span data-stu-id="35220-238">date</span></span> |<span data-ttu-id="35220-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="35220-239">Datetime</span></span> |
| <span data-ttu-id="35220-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="35220-240">datetime</span></span> |<span data-ttu-id="35220-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="35220-241">Datetime</span></span> |
| <span data-ttu-id="35220-242">十進位</span><span class="sxs-lookup"><span data-stu-id="35220-242">decimal</span></span> |<span data-ttu-id="35220-243">十進位</span><span class="sxs-lookup"><span data-stu-id="35220-243">Decimal</span></span> |
| <span data-ttu-id="35220-244">雙精度</span><span class="sxs-lookup"><span data-stu-id="35220-244">double precision</span></span> |<span data-ttu-id="35220-245">兩倍</span><span class="sxs-lookup"><span data-stu-id="35220-245">Double</span></span> |
| <span data-ttu-id="35220-246">兩倍</span><span class="sxs-lookup"><span data-stu-id="35220-246">double</span></span> |<span data-ttu-id="35220-247">兩倍</span><span class="sxs-lookup"><span data-stu-id="35220-247">Double</span></span> |
| <span data-ttu-id="35220-248">列舉</span><span class="sxs-lookup"><span data-stu-id="35220-248">enum</span></span> |<span data-ttu-id="35220-249">String</span><span class="sxs-lookup"><span data-stu-id="35220-249">String</span></span> |
| <span data-ttu-id="35220-250">float</span><span class="sxs-lookup"><span data-stu-id="35220-250">float</span></span> |<span data-ttu-id="35220-251">單一</span><span class="sxs-lookup"><span data-stu-id="35220-251">Single</span></span> |
| <span data-ttu-id="35220-252">不帶正負號的 int</span><span class="sxs-lookup"><span data-stu-id="35220-252">int unsigned</span></span> |<span data-ttu-id="35220-253">Int64</span><span class="sxs-lookup"><span data-stu-id="35220-253">Int64</span></span> |
| <span data-ttu-id="35220-254">int</span><span class="sxs-lookup"><span data-stu-id="35220-254">int</span></span> |<span data-ttu-id="35220-255">Int32</span><span class="sxs-lookup"><span data-stu-id="35220-255">Int32</span></span> |
| <span data-ttu-id="35220-256">不帶正負號的整數</span><span class="sxs-lookup"><span data-stu-id="35220-256">integer unsigned</span></span> |<span data-ttu-id="35220-257">Int64</span><span class="sxs-lookup"><span data-stu-id="35220-257">Int64</span></span> |
| <span data-ttu-id="35220-258">integer</span><span class="sxs-lookup"><span data-stu-id="35220-258">integer</span></span> |<span data-ttu-id="35220-259">Int32</span><span class="sxs-lookup"><span data-stu-id="35220-259">Int32</span></span> |
| <span data-ttu-id="35220-260">長 varbinary</span><span class="sxs-lookup"><span data-stu-id="35220-260">long varbinary</span></span> |<span data-ttu-id="35220-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="35220-261">Byte[]</span></span> |
| <span data-ttu-id="35220-262">長 varchar</span><span class="sxs-lookup"><span data-stu-id="35220-262">long varchar</span></span> |<span data-ttu-id="35220-263">String</span><span class="sxs-lookup"><span data-stu-id="35220-263">String</span></span> |
| <span data-ttu-id="35220-264">longblob</span><span class="sxs-lookup"><span data-stu-id="35220-264">longblob</span></span> |<span data-ttu-id="35220-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="35220-265">Byte[]</span></span> |
| <span data-ttu-id="35220-266">longtext</span><span class="sxs-lookup"><span data-stu-id="35220-266">longtext</span></span> |<span data-ttu-id="35220-267">String</span><span class="sxs-lookup"><span data-stu-id="35220-267">String</span></span> |
| <span data-ttu-id="35220-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="35220-268">mediumblob</span></span> |<span data-ttu-id="35220-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="35220-269">Byte[]</span></span> |
| <span data-ttu-id="35220-270">不帶正負號的 mediumint</span><span class="sxs-lookup"><span data-stu-id="35220-270">mediumint unsigned</span></span> |<span data-ttu-id="35220-271">Int64</span><span class="sxs-lookup"><span data-stu-id="35220-271">Int64</span></span> |
| <span data-ttu-id="35220-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="35220-272">mediumint</span></span> |<span data-ttu-id="35220-273">Int32</span><span class="sxs-lookup"><span data-stu-id="35220-273">Int32</span></span> |
| <span data-ttu-id="35220-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="35220-274">mediumtext</span></span> |<span data-ttu-id="35220-275">String</span><span class="sxs-lookup"><span data-stu-id="35220-275">String</span></span> |
| <span data-ttu-id="35220-276">numeric</span><span class="sxs-lookup"><span data-stu-id="35220-276">numeric</span></span> |<span data-ttu-id="35220-277">十進位</span><span class="sxs-lookup"><span data-stu-id="35220-277">Decimal</span></span> |
| <span data-ttu-id="35220-278">real</span><span class="sxs-lookup"><span data-stu-id="35220-278">real</span></span> |<span data-ttu-id="35220-279">兩倍</span><span class="sxs-lookup"><span data-stu-id="35220-279">Double</span></span> |
| <span data-ttu-id="35220-280">set</span><span class="sxs-lookup"><span data-stu-id="35220-280">set</span></span> |<span data-ttu-id="35220-281">String</span><span class="sxs-lookup"><span data-stu-id="35220-281">String</span></span> |
| <span data-ttu-id="35220-282">不帶正負號的 smallint</span><span class="sxs-lookup"><span data-stu-id="35220-282">smallint unsigned</span></span> |<span data-ttu-id="35220-283">Int32</span><span class="sxs-lookup"><span data-stu-id="35220-283">Int32</span></span> |
| <span data-ttu-id="35220-284">smallint</span><span class="sxs-lookup"><span data-stu-id="35220-284">smallint</span></span> |<span data-ttu-id="35220-285">Int16</span><span class="sxs-lookup"><span data-stu-id="35220-285">Int16</span></span> |
| <span data-ttu-id="35220-286">文字</span><span class="sxs-lookup"><span data-stu-id="35220-286">text</span></span> |<span data-ttu-id="35220-287">String</span><span class="sxs-lookup"><span data-stu-id="35220-287">String</span></span> |
| <span data-ttu-id="35220-288">分析</span><span class="sxs-lookup"><span data-stu-id="35220-288">time</span></span> |<span data-ttu-id="35220-289">時間範圍</span><span class="sxs-lookup"><span data-stu-id="35220-289">TimeSpan</span></span> |
| <span data-ttu-id="35220-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="35220-290">timestamp</span></span> |<span data-ttu-id="35220-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="35220-291">Datetime</span></span> |
| <span data-ttu-id="35220-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="35220-292">tinyblob</span></span> |<span data-ttu-id="35220-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="35220-293">Byte[]</span></span> |
| <span data-ttu-id="35220-294">不帶正負號的 tinyint</span><span class="sxs-lookup"><span data-stu-id="35220-294">tinyint unsigned</span></span> |<span data-ttu-id="35220-295">Int16</span><span class="sxs-lookup"><span data-stu-id="35220-295">Int16</span></span> |
| <span data-ttu-id="35220-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="35220-296">tinyint</span></span> |<span data-ttu-id="35220-297">Int16</span><span class="sxs-lookup"><span data-stu-id="35220-297">Int16</span></span> |
| <span data-ttu-id="35220-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="35220-298">tinytext</span></span> |<span data-ttu-id="35220-299">String</span><span class="sxs-lookup"><span data-stu-id="35220-299">String</span></span> |
| <span data-ttu-id="35220-300">varchar</span><span class="sxs-lookup"><span data-stu-id="35220-300">varchar</span></span> |<span data-ttu-id="35220-301">String</span><span class="sxs-lookup"><span data-stu-id="35220-301">String</span></span> |
| <span data-ttu-id="35220-302">年</span><span class="sxs-lookup"><span data-stu-id="35220-302">year</span></span> |<span data-ttu-id="35220-303">int</span><span class="sxs-lookup"><span data-stu-id="35220-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="35220-304">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="35220-304">Map source toosink columns</span></span>
<span data-ttu-id="35220-305">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="35220-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="35220-306">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="35220-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="35220-307">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="35220-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="35220-308">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="35220-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="35220-309">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="35220-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="35220-310">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="35220-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="35220-311">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="35220-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="35220-312">效能和微調</span><span class="sxs-lookup"><span data-stu-id="35220-312">Performance and Tuning</span></span>
<span data-ttu-id="35220-313">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="35220-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
