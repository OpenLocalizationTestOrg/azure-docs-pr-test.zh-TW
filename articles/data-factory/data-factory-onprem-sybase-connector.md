---
title: "使用 Azure Data Factory 的 Sybase aaaMove 資料 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 Sybase 資料庫 toomove 資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="286f8-103">使用 Azure Data Factory 從 Sybase 移動資料</span><span class="sxs-lookup"><span data-stu-id="286f8-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="286f8-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 Sybase 資料庫中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="286f8-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="286f8-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="286f8-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="286f8-106">您可以從內部部署 Sybase 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="286f8-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="286f8-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="286f8-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="286f8-108">目前資料處理站都會支援只移動資料的 Sybase 資料儲存 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooa Sybase 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="286f8-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="286f8-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="286f8-109">Prerequisites</span></span>
<span data-ttu-id="286f8-110">資料 Factory 服務支援使用 hello 資料管理閘道的連線 tooon 內部部署 Sybase 來源。</span><span class="sxs-lookup"><span data-stu-id="286f8-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="286f8-111">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="286f8-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="286f8-112">即使 hello Sybase 資料庫裝載於 Azure IaaS VM 需要閘道。</span><span class="sxs-lookup"><span data-stu-id="286f8-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="286f8-113">您可以在 hello 相同 IaaS VM 做為 hello 資料儲存或不同的 VM 只要 hello 閘道上可以連接 toohello 資料庫上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="286f8-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="286f8-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="286f8-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="286f8-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="286f8-115">Supported versions and installation</span></span>
<span data-ttu-id="286f8-116">資料管理閘道器 tooconnect toohello Sybase 資料庫，您需要 tooinstall hello [Sybase iAnywhere.Data.SQLAnywhere 的資料提供者](http://go.microsoft.com/fwlink/?linkid=324846)16 或上方上 hello 相同系統 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="286f8-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="286f8-117">支援 Sybase 版本 16 和以上版本。</span><span class="sxs-lookup"><span data-stu-id="286f8-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="286f8-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="286f8-118">Getting started</span></span>
<span data-ttu-id="286f8-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="286f8-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="286f8-120">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="286f8-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="286f8-121">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="286f8-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="286f8-122">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="286f8-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="286f8-123">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="286f8-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="286f8-124">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="286f8-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="286f8-125">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="286f8-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="286f8-126">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="286f8-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="286f8-127">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="286f8-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="286f8-128">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="286f8-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="286f8-129">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="286f8-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="286f8-130">具有使用的 toocopy 資料從內部部署 Sybase 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Sybase tooAzure Blob 複製](#json-example-copy-data-from-sybase-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="286f8-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="286f8-131">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa Sybase 資料存放區的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="286f8-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="286f8-132">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="286f8-132">Linked service properties</span></span>
<span data-ttu-id="286f8-133">下表中的 hello 提供 JSON 項目特定 tooSybase 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="286f8-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="286f8-134">屬性</span><span class="sxs-lookup"><span data-stu-id="286f8-134">Property</span></span> | <span data-ttu-id="286f8-135">說明</span><span class="sxs-lookup"><span data-stu-id="286f8-135">Description</span></span> | <span data-ttu-id="286f8-136">必要</span><span class="sxs-lookup"><span data-stu-id="286f8-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="286f8-137">類型</span><span class="sxs-lookup"><span data-stu-id="286f8-137">type</span></span> |<span data-ttu-id="286f8-138">hello 類型屬性必須設定為： **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="286f8-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="286f8-139">是</span><span class="sxs-lookup"><span data-stu-id="286f8-139">Yes</span></span> |
| <span data-ttu-id="286f8-140">伺服器</span><span class="sxs-lookup"><span data-stu-id="286f8-140">server</span></span> |<span data-ttu-id="286f8-141">Hello Sybase 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="286f8-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="286f8-142">是</span><span class="sxs-lookup"><span data-stu-id="286f8-142">Yes</span></span> |
| <span data-ttu-id="286f8-143">資料庫</span><span class="sxs-lookup"><span data-stu-id="286f8-143">database</span></span> |<span data-ttu-id="286f8-144">Hello Sybase 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="286f8-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="286f8-145">是</span><span class="sxs-lookup"><span data-stu-id="286f8-145">Yes</span></span> |
| <span data-ttu-id="286f8-146">結構描述</span><span class="sxs-lookup"><span data-stu-id="286f8-146">schema</span></span> |<span data-ttu-id="286f8-147">Hello hello 資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="286f8-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="286f8-148">否</span><span class="sxs-lookup"><span data-stu-id="286f8-148">No</span></span> |
| <span data-ttu-id="286f8-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="286f8-149">authenticationType</span></span> |<span data-ttu-id="286f8-150">Tooconnect toohello Sybase 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="286f8-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="286f8-151">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="286f8-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="286f8-152">是</span><span class="sxs-lookup"><span data-stu-id="286f8-152">Yes</span></span> |
| <span data-ttu-id="286f8-153">username</span><span class="sxs-lookup"><span data-stu-id="286f8-153">username</span></span> |<span data-ttu-id="286f8-154">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="286f8-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="286f8-155">否</span><span class="sxs-lookup"><span data-stu-id="286f8-155">No</span></span> |
| <span data-ttu-id="286f8-156">password</span><span class="sxs-lookup"><span data-stu-id="286f8-156">password</span></span> |<span data-ttu-id="286f8-157">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="286f8-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="286f8-158">否</span><span class="sxs-lookup"><span data-stu-id="286f8-158">No</span></span> |
| <span data-ttu-id="286f8-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="286f8-159">gatewayName</span></span> |<span data-ttu-id="286f8-160">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 Sybase 資料庫。</span><span class="sxs-lookup"><span data-stu-id="286f8-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="286f8-161">是</span><span class="sxs-lookup"><span data-stu-id="286f8-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="286f8-162">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="286f8-162">Dataset properties</span></span>
<span data-ttu-id="286f8-163">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="286f8-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="286f8-164">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="286f8-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="286f8-165">hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="286f8-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="286f8-166">hello **typeProperties**類型的資料集區段**RelationalTable** （包括 Sybase 資料集） 具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="286f8-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="286f8-167">屬性</span><span class="sxs-lookup"><span data-stu-id="286f8-167">Property</span></span> | <span data-ttu-id="286f8-168">說明</span><span class="sxs-lookup"><span data-stu-id="286f8-168">Description</span></span> | <span data-ttu-id="286f8-169">必要</span><span class="sxs-lookup"><span data-stu-id="286f8-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="286f8-170">tableName</span><span class="sxs-lookup"><span data-stu-id="286f8-170">tableName</span></span> |<span data-ttu-id="286f8-171">Hello Sybase 資料庫連結的服務參考的執行個體中的 hello 資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="286f8-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="286f8-172">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="286f8-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="286f8-173">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="286f8-173">Copy activity properties</span></span>
<span data-ttu-id="286f8-174">如需可用來定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="286f8-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="286f8-175">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="286f8-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="286f8-176">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="286f8-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="286f8-177">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="286f8-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="286f8-178">當 hello 來源屬於型別**RelationalSource** （包括 Sybase） 中的下列屬性的 hello 可用**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="286f8-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="286f8-179">屬性</span><span class="sxs-lookup"><span data-stu-id="286f8-179">Property</span></span> | <span data-ttu-id="286f8-180">說明</span><span class="sxs-lookup"><span data-stu-id="286f8-180">Description</span></span> | <span data-ttu-id="286f8-181">允許的值</span><span class="sxs-lookup"><span data-stu-id="286f8-181">Allowed values</span></span> | <span data-ttu-id="286f8-182">必要</span><span class="sxs-lookup"><span data-stu-id="286f8-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="286f8-183">query</span><span class="sxs-lookup"><span data-stu-id="286f8-183">query</span></span> |<span data-ttu-id="286f8-184">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="286f8-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="286f8-185">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="286f8-185">SQL query string.</span></span> <span data-ttu-id="286f8-186">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="286f8-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="286f8-187">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="286f8-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="286f8-188">JSON 範例： 將資料從 Sybase tooAzure Blob 複製</span><span class="sxs-lookup"><span data-stu-id="286f8-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="286f8-189">hello 下列範例將提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="286f8-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="286f8-190">它們會顯示如何 toocopy 資料從 Sybase 資料庫 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="286f8-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="286f8-191">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="286f8-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="286f8-192">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="286f8-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="286f8-193">[OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="286f8-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="286f8-194">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="286f8-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="286f8-195">[RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="286f8-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="286f8-196">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="286f8-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="286f8-197">hello[管線](data-factory-create-pipelines.md)與使用複製活動[RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="286f8-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="286f8-198">hello 範例將資料從 Sybase 資料庫 tooa blob 中的查詢結果的每個小時。</span><span class="sxs-lookup"><span data-stu-id="286f8-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="286f8-199">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="286f8-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="286f8-200">第一個步驟中，安裝程式 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="286f8-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="286f8-201">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="286f8-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="286f8-202">**Sybase 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="286f8-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

<span data-ttu-id="286f8-203">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="286f8-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="286f8-204">**Sybase 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="286f8-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="286f8-205">hello 範例假設您已建立資料表"MyTable"中 Sybase 和它包含稱為"timestamp"時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="286f8-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="286f8-206">設定 「 外部 」: true 會在此資料集是外部 toohello 資料處理站，並不產生 hello data factory 中的活動時通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="286f8-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="286f8-207">請注意該 hello**類型**hello 連結的服務設定為： **RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="286f8-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="286f8-208">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="286f8-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="286f8-209">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="286f8-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="286f8-210">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="286f8-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="286f8-211">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="286f8-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="286f8-212">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="286f8-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="286f8-213">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為每小時排程的 toorun。</span><span class="sxs-lookup"><span data-stu-id="286f8-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="286f8-214">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="286f8-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="286f8-215">指定 hello SQL 查詢**查詢**屬性從 hello DBA 選取 hello 資料。Hello 資料庫中的 orders 資料表。</span><span class="sxs-lookup"><span data-stu-id="286f8-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="286f8-216">Sybase 的類型對應</span><span class="sxs-lookup"><span data-stu-id="286f8-216">Type mapping for Sybase</span></span>
<span data-ttu-id="286f8-217">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：</span><span class="sxs-lookup"><span data-stu-id="286f8-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="286f8-218">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="286f8-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="286f8-219">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="286f8-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="286f8-220">Sybase 支援 T-SQL 和 T-SQL 類型。</span><span class="sxs-lookup"><span data-stu-id="286f8-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="286f8-221">從 sql 類型 too.NET 型別對應表，請參閱[Azure SQL Connector](data-factory-azure-sql-connector.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="286f8-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="286f8-222">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="286f8-222">Map source toosink columns</span></span>
<span data-ttu-id="286f8-223">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="286f8-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="286f8-224">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="286f8-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="286f8-225">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="286f8-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="286f8-226">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="286f8-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="286f8-227">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="286f8-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="286f8-228">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="286f8-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="286f8-229">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="286f8-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="286f8-230">效能和微調</span><span class="sxs-lookup"><span data-stu-id="286f8-230">Performance and Tuning</span></span>
<span data-ttu-id="286f8-231">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="286f8-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
