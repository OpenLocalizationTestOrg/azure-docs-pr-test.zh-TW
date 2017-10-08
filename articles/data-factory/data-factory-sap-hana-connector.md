---
title: "使用 Azure Data Factory 的 SAP HANA aaaMove 資料 |Microsoft 文件"
description: "深入了解如何使用 Azure Data Factory 的 SAP HANA toomove 資料。"
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="3965e-103">使用 Azure Data Factory 從 SAP Hana 移動資料</span><span class="sxs-lookup"><span data-stu-id="3965e-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="3965e-104">本文說明 toouse 如何在 Azure Data Factory toomove 資料從內部部署 SAP HANA hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="3965e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="3965e-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="3965e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="3965e-106">您可以從內部部署 SAP HANA 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="3965e-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="3965e-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="3965e-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3965e-108">資料處理站目前只支援將資料從 SAP HANA tooother 資料存放區，但不是會將資料從其他資料儲存 tooan SAP HANA 的。</span><span class="sxs-lookup"><span data-stu-id="3965e-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="3965e-109">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="3965e-109">Supported versions and installation</span></span>
<span data-ttu-id="3965e-110">此連接器支援任何版本的 SAP HANA 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3965e-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="3965e-111">它支援從 HANA 資訊模型 (例如分析和計算檢視) 及使用 SQL 查詢資料列/資料行資料表複製資料。</span><span class="sxs-lookup"><span data-stu-id="3965e-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="3965e-112">tooenable hello 連線 toohello SAP HANA 的執行個體，安裝下列元件的 hello:</span><span class="sxs-lookup"><span data-stu-id="3965e-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="3965e-113">**資料管理閘道器**: tooon 內部部署資料連接的 Data Factory 服務支援 （包括 SAP HANA） 存放區使用的元件稱為 「 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="3965e-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="3965e-114">請參閱有關資料管理閘道器和 hello 閘道設定的逐步指示 toolearn [toocloud 資料存放區的內部部署資料之間移動資料存放區](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="3965e-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="3965e-115">即使 hello SAP HANA 裝載於 Azure IaaS 虛擬機器 (VM) 需要閘道。</span><span class="sxs-lookup"><span data-stu-id="3965e-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="3965e-116">您可以在相同的 VM 為 hello 資料儲存，或在不同的 VM 只要 hello 閘道可以連接 toohello 資料庫 hello 安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="3965e-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="3965e-117">**SAP HANA ODBC 驅動程式**hello 閘道機器上。</span><span class="sxs-lookup"><span data-stu-id="3965e-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="3965e-118">您可以下載 hello SAP HANA ODBC 驅動程式從 hello [SAP 軟體下載中心](https://support.sap.com/swdc)。</span><span class="sxs-lookup"><span data-stu-id="3965e-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="3965e-119">搜尋與 hello 關鍵字**SAP HANA CLIENT for Windows**。</span><span class="sxs-lookup"><span data-stu-id="3965e-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="3965e-120">開始使用</span><span class="sxs-lookup"><span data-stu-id="3965e-120">Getting started</span></span>
<span data-ttu-id="3965e-121">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="3965e-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="3965e-122">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="3965e-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="3965e-123">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="3965e-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="3965e-124">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="3965e-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3965e-125">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="3965e-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3965e-126">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="3965e-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="3965e-127">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="3965e-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="3965e-128">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="3965e-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="3965e-129">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="3965e-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3965e-130">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="3965e-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="3965e-131">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="3965e-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="3965e-132">具有使用的 toocopy 資料從內部部署 SAP HANA 的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 SAP HANA tooAzure Blob 複製](#json-example-copy-data-from-sap-hana-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="3965e-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3965e-133">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooan SAP HANA 資料存放區的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="3965e-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3965e-134">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="3965e-134">Linked service properties</span></span>
<span data-ttu-id="3965e-135">hello 下表提供的 JSON 元素特定 tooSAP HANA 連結服務。</span><span class="sxs-lookup"><span data-stu-id="3965e-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="3965e-136">屬性</span><span class="sxs-lookup"><span data-stu-id="3965e-136">Property</span></span> | <span data-ttu-id="3965e-137">說明</span><span class="sxs-lookup"><span data-stu-id="3965e-137">Description</span></span> | <span data-ttu-id="3965e-138">允許的值</span><span class="sxs-lookup"><span data-stu-id="3965e-138">Allowed values</span></span> | <span data-ttu-id="3965e-139">必要</span><span class="sxs-lookup"><span data-stu-id="3965e-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="3965e-140">伺服器</span><span class="sxs-lookup"><span data-stu-id="3965e-140">server</span></span> | <span data-ttu-id="3965e-141">執行個體所在的 hello SAP HANA hello 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="3965e-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="3965e-142">如果您的伺服器使用自訂連接埠，指定 `server:port`。</span><span class="sxs-lookup"><span data-stu-id="3965e-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="3965e-143">字串</span><span class="sxs-lookup"><span data-stu-id="3965e-143">string</span></span> | <span data-ttu-id="3965e-144">是</span><span class="sxs-lookup"><span data-stu-id="3965e-144">Yes</span></span>
<span data-ttu-id="3965e-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3965e-145">authenticationType</span></span> | <span data-ttu-id="3965e-146">驗證類型。</span><span class="sxs-lookup"><span data-stu-id="3965e-146">Type of authentication.</span></span> | <span data-ttu-id="3965e-147">字串。</span><span class="sxs-lookup"><span data-stu-id="3965e-147">string.</span></span> <span data-ttu-id="3965e-148">"Basic" 或 "Windows"</span><span class="sxs-lookup"><span data-stu-id="3965e-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="3965e-149">是</span><span class="sxs-lookup"><span data-stu-id="3965e-149">Yes</span></span> 
<span data-ttu-id="3965e-150">username</span><span class="sxs-lookup"><span data-stu-id="3965e-150">username</span></span> | <span data-ttu-id="3965e-151">Hello 使用者具有存取 toohello SAP 伺服器的名稱</span><span class="sxs-lookup"><span data-stu-id="3965e-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="3965e-152">字串</span><span class="sxs-lookup"><span data-stu-id="3965e-152">string</span></span> | <span data-ttu-id="3965e-153">是</span><span class="sxs-lookup"><span data-stu-id="3965e-153">Yes</span></span>
<span data-ttu-id="3965e-154">password</span><span class="sxs-lookup"><span data-stu-id="3965e-154">password</span></span> | <span data-ttu-id="3965e-155">Hello 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="3965e-155">Password for hello user.</span></span> | <span data-ttu-id="3965e-156">字串</span><span class="sxs-lookup"><span data-stu-id="3965e-156">string</span></span> | <span data-ttu-id="3965e-157">是</span><span class="sxs-lookup"><span data-stu-id="3965e-157">Yes</span></span>
<span data-ttu-id="3965e-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3965e-158">gatewayName</span></span> | <span data-ttu-id="3965e-159">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 SAP HANA 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="3965e-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="3965e-160">字串</span><span class="sxs-lookup"><span data-stu-id="3965e-160">string</span></span> | <span data-ttu-id="3965e-161">是</span><span class="sxs-lookup"><span data-stu-id="3965e-161">Yes</span></span>
<span data-ttu-id="3965e-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3965e-162">encryptedCredential</span></span> | <span data-ttu-id="3965e-163">hello 加密認證的字串。</span><span class="sxs-lookup"><span data-stu-id="3965e-163">hello encrypted credential string.</span></span> | <span data-ttu-id="3965e-164">字串</span><span class="sxs-lookup"><span data-stu-id="3965e-164">string</span></span> | <span data-ttu-id="3965e-165">否</span><span class="sxs-lookup"><span data-stu-id="3965e-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="3965e-166">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="3965e-166">Dataset properties</span></span>
<span data-ttu-id="3965e-167">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="3965e-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3965e-168">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="3965e-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3965e-169">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3965e-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="3965e-170">支援的型別 hello SAP HANA 資料集沒有特定型別的屬性**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="3965e-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="3965e-171">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="3965e-171">Copy activity properties</span></span>
<span data-ttu-id="3965e-172">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="3965e-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3965e-173">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="3965e-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="3965e-174">而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="3965e-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="3965e-175">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="3965e-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="3965e-176">複製活動中的來源時的型別**RelationalSource** （包括 SAP HANA），下列屬性的 hello 可用 typeProperties 區段中：</span><span class="sxs-lookup"><span data-stu-id="3965e-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="3965e-177">屬性</span><span class="sxs-lookup"><span data-stu-id="3965e-177">Property</span></span> | <span data-ttu-id="3965e-178">說明</span><span class="sxs-lookup"><span data-stu-id="3965e-178">Description</span></span> | <span data-ttu-id="3965e-179">允許的值</span><span class="sxs-lookup"><span data-stu-id="3965e-179">Allowed values</span></span> | <span data-ttu-id="3965e-180">必要</span><span class="sxs-lookup"><span data-stu-id="3965e-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3965e-181">query</span><span class="sxs-lookup"><span data-stu-id="3965e-181">query</span></span> | <span data-ttu-id="3965e-182">指定 hello SQL 查詢 tooread 資料從 hello SAP HANA 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3965e-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="3965e-183">SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="3965e-183">SQL query.</span></span> | <span data-ttu-id="3965e-184">是</span><span class="sxs-lookup"><span data-stu-id="3965e-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="3965e-185">JSON 範例： 從 SAP HANA tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="3965e-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="3965e-186">hello 下列範例會提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="3965e-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3965e-187">這個範例示範如何從 Azure Blob 儲存體的內部部署 SAP HANA tooan toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="3965e-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="3965e-188">不過，資料可以複製**直接**hello 接收所列的 tooany[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="3965e-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3965e-189">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="3965e-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="3965e-190">它不包含建立 hello 資料處理站的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="3965e-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="3965e-191">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="3965e-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="3965e-192">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="3965e-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="3965e-193">[SapHana](#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="3965e-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="3965e-194">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="3965e-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3965e-195">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3965e-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="3965e-196">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="3965e-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3965e-197">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="3965e-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3965e-198">hello 範例將資料從 Azure blob 的 SAP HANA 執行個體 tooan 每小時。</span><span class="sxs-lookup"><span data-stu-id="3965e-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="3965e-199">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="3965e-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="3965e-200">第一個步驟中，安裝程式 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="3965e-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="3965e-201">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="3965e-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="3965e-202">SAP HANA 連結服務</span><span class="sxs-lookup"><span data-stu-id="3965e-202">SAP HANA linked service</span></span>
<span data-ttu-id="3965e-203">此連結服務連結您 SAP HANA 執行個體 toohello 的 data factory。</span><span class="sxs-lookup"><span data-stu-id="3965e-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="3965e-204">hello type 屬性設定太**SapHana**。</span><span class="sxs-lookup"><span data-stu-id="3965e-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="3965e-205">hello typeProperties > 一節提供 hello SAP HANA 執行個體的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="3965e-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="3965e-206">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="3965e-206">Azure Storage linked service</span></span>
<span data-ttu-id="3965e-207">此連結服務連結您的 Azure 儲存體帳戶 toohello data factory。</span><span class="sxs-lookup"><span data-stu-id="3965e-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="3965e-208">hello type 屬性設定太**AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="3965e-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="3965e-209">hello typeProperties > 一節提供 hello Azure 儲存體帳戶的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="3965e-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="3965e-210">SAP HANA 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="3965e-210">SAP HANA input dataset</span></span>

<span data-ttu-id="3965e-211">此資料集定義 hello SAP HANA 資料集。</span><span class="sxs-lookup"><span data-stu-id="3965e-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="3965e-212">您設定的 hello Data Factory 資料集的 hello 類型太**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="3965e-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="3965e-213">目前，您不指定任何特定類型的 SAP HANA 資料集屬性。</span><span class="sxs-lookup"><span data-stu-id="3965e-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="3965e-214">hello 複製活動定義中的 hello 查詢指定了哪些資料 tooread，從 hello SAP HANA 執行個體。</span><span class="sxs-lookup"><span data-stu-id="3965e-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="3965e-215">設定外部屬性 tootrue 通知 hello Data Factory 服務，該 hello 資料表是外部 toohello 資料處理站，就不會產生 hello data factory 中活動。</span><span class="sxs-lookup"><span data-stu-id="3965e-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="3965e-216">頻率和間隔 屬性定義 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="3965e-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="3965e-217">在此情況下，hello 資料是從讀取 hello SAP HANA 執行個體每小時。</span><span class="sxs-lookup"><span data-stu-id="3965e-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="3965e-218">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="3965e-218">Azure Blob output dataset</span></span>
<span data-ttu-id="3965e-219">此資料集定義 hello 輸出 Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="3965e-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="3965e-220">hello type 屬性設定 tooAzureBlob。</span><span class="sxs-lookup"><span data-stu-id="3965e-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="3965e-221">hello typeProperties 區段提供從 hello SAP HANA 執行個體複製 hello 資料的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="3965e-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="3965e-222">hello 資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="3965e-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3965e-223">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="3965e-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="3965e-224">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="3965e-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="3965e-225">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="3965e-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="3965e-226">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="3965e-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="3965e-227">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource** （適用於 SAP HANA 來源） 和**接收**類型設定得**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3965e-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="3965e-228">指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="3965e-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="3965e-229">SAP Hana 的類型對應</span><span class="sxs-lookup"><span data-stu-id="3965e-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="3965e-230">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)發行項，複製活動會執行自動類型轉換來源類型 toosink 類型以下列兩種方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="3965e-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="3965e-231">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="3965e-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="3965e-232">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="3965e-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="3965e-233">從 SAP HANA 資料時，下列對應的 hello 可用從 SAP HANA 類型 too.NET 型別。</span><span class="sxs-lookup"><span data-stu-id="3965e-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="3965e-234">SAP Hana 類型</span><span class="sxs-lookup"><span data-stu-id="3965e-234">SAP HANA Type</span></span> | <span data-ttu-id="3965e-235">以 .Net 為基礎的類型</span><span class="sxs-lookup"><span data-stu-id="3965e-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="3965e-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="3965e-236">TINYINT</span></span> | <span data-ttu-id="3965e-237">位元組</span><span class="sxs-lookup"><span data-stu-id="3965e-237">Byte</span></span>
<span data-ttu-id="3965e-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="3965e-238">SMALLINT</span></span> | <span data-ttu-id="3965e-239">Int16</span><span class="sxs-lookup"><span data-stu-id="3965e-239">Int16</span></span>
<span data-ttu-id="3965e-240">INT</span><span class="sxs-lookup"><span data-stu-id="3965e-240">INT</span></span> | <span data-ttu-id="3965e-241">Int32</span><span class="sxs-lookup"><span data-stu-id="3965e-241">Int32</span></span>
<span data-ttu-id="3965e-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="3965e-242">BIGINT</span></span> | <span data-ttu-id="3965e-243">Int64</span><span class="sxs-lookup"><span data-stu-id="3965e-243">Int64</span></span>
<span data-ttu-id="3965e-244">REAL</span><span class="sxs-lookup"><span data-stu-id="3965e-244">REAL</span></span> | <span data-ttu-id="3965e-245">單一</span><span class="sxs-lookup"><span data-stu-id="3965e-245">Single</span></span>
<span data-ttu-id="3965e-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="3965e-246">DOUBLE</span></span> | <span data-ttu-id="3965e-247">單一</span><span class="sxs-lookup"><span data-stu-id="3965e-247">Single</span></span>
<span data-ttu-id="3965e-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="3965e-248">DECIMAL</span></span> | <span data-ttu-id="3965e-249">十進位</span><span class="sxs-lookup"><span data-stu-id="3965e-249">Decimal</span></span>
<span data-ttu-id="3965e-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="3965e-250">BOOLEAN</span></span> | <span data-ttu-id="3965e-251">位元組</span><span class="sxs-lookup"><span data-stu-id="3965e-251">Byte</span></span>
<span data-ttu-id="3965e-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="3965e-252">VARCHAR</span></span> | <span data-ttu-id="3965e-253">String</span><span class="sxs-lookup"><span data-stu-id="3965e-253">String</span></span>
<span data-ttu-id="3965e-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="3965e-254">NVARCHAR</span></span> | <span data-ttu-id="3965e-255">String</span><span class="sxs-lookup"><span data-stu-id="3965e-255">String</span></span>
<span data-ttu-id="3965e-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="3965e-256">CLOB</span></span> | <span data-ttu-id="3965e-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="3965e-257">Byte[]</span></span>
<span data-ttu-id="3965e-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="3965e-258">ALPHANUM</span></span> | <span data-ttu-id="3965e-259">String</span><span class="sxs-lookup"><span data-stu-id="3965e-259">String</span></span>
<span data-ttu-id="3965e-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="3965e-260">BLOB</span></span> | <span data-ttu-id="3965e-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="3965e-261">Byte[]</span></span>
<span data-ttu-id="3965e-262">日期</span><span class="sxs-lookup"><span data-stu-id="3965e-262">DATE</span></span> | <span data-ttu-id="3965e-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="3965e-263">DateTime</span></span>
<span data-ttu-id="3965e-264">TIME</span><span class="sxs-lookup"><span data-stu-id="3965e-264">TIME</span></span> | <span data-ttu-id="3965e-265">時間範圍</span><span class="sxs-lookup"><span data-stu-id="3965e-265">TimeSpan</span></span>
<span data-ttu-id="3965e-266">時間戳記</span><span class="sxs-lookup"><span data-stu-id="3965e-266">TIMESTAMP</span></span> | <span data-ttu-id="3965e-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="3965e-267">DateTime</span></span>
<span data-ttu-id="3965e-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="3965e-268">SECONDDATE</span></span> | <span data-ttu-id="3965e-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="3965e-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="3965e-270">已知限制</span><span class="sxs-lookup"><span data-stu-id="3965e-270">Known limitations</span></span>
<span data-ttu-id="3965e-271">從 SAP HANA 複製資料時，有幾個已知的限制︰</span><span class="sxs-lookup"><span data-stu-id="3965e-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="3965e-272">NVARCHAR 字串會截斷的 toomaximum 長度 4000 個 Unicode 字元</span><span class="sxs-lookup"><span data-stu-id="3965e-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="3965e-273">不支援 SMALLDECIMAL</span><span class="sxs-lookup"><span data-stu-id="3965e-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="3965e-274">不支援 VARBINARY</span><span class="sxs-lookup"><span data-stu-id="3965e-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="3965e-275">有效日期為 1899/12/30 到 9999/12/31 之間</span><span class="sxs-lookup"><span data-stu-id="3965e-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="3965e-276">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="3965e-276">Map source toosink columns</span></span>
<span data-ttu-id="3965e-277">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="3965e-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3965e-278">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="3965e-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="3965e-279">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="3965e-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="3965e-280">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="3965e-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3965e-281">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="3965e-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3965e-282">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="3965e-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3965e-283">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="3965e-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3965e-284">效能和微調</span><span class="sxs-lookup"><span data-stu-id="3965e-284">Performance and Tuning</span></span>
<span data-ttu-id="3965e-285">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="3965e-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
