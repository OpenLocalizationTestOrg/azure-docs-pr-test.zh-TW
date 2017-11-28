---
title: "使用 Azure Data Factory 的 Teradata aaaMove 資料 |Microsoft 文件"
description: "了解 Teradata 連接器 hello Data Factory 服務，可讓您從 Teradata 資料庫資料"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="c72b2-103">使用 Azure Data Factory 從 Teradata 移動資料</span><span class="sxs-lookup"><span data-stu-id="c72b2-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="c72b2-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 Teradata 資料庫中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="c72b2-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="c72b2-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="c72b2-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="c72b2-106">您可以從內部部署 Teradata 資料存放區支援 tooany 接收資料存放區複製資料。</span><span class="sxs-lookup"><span data-stu-id="c72b2-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="c72b2-107">取得一份資料存放區支援接收由 hello 複製活動時，請參閱 hello[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)資料表。</span><span class="sxs-lookup"><span data-stu-id="c72b2-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c72b2-108">目前資料處理站都會支援只移動從 Teradata 資料的資料存放區 tooother 資料存放區，但不適用於將資料從其他資料存放區 tooa Teradata 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="c72b2-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c72b2-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="c72b2-109">Prerequisites</span></span>
<span data-ttu-id="c72b2-110">資料處理站都會支援透過 hello 資料管理閘道的連線 tooon 內部部署 Teradata 來源。</span><span class="sxs-lookup"><span data-stu-id="c72b2-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="c72b2-111">請參閱[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)文章 toolearn 有關資料管理閘道器和 hello 閘道設定的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="c72b2-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="c72b2-112">即使 hello Teradata 裝載於 Azure IaaS VM 需要閘道。</span><span class="sxs-lookup"><span data-stu-id="c72b2-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="c72b2-113">您可以在 hello 相同 IaaS VM 做為 hello 資料儲存或不同的 VM 只要 hello 閘道上可以連接 toohello 資料庫上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="c72b2-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="c72b2-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="c72b2-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="c72b2-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="c72b2-115">Supported versions and installation</span></span>
<span data-ttu-id="c72b2-116">資料管理閘道器 tooconnect toohello Teradata 資料庫，您需要 tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) 14 版或以上上 hello 相同系統 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="c72b2-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="c72b2-117">支援 Teradata 版本 12 和以上版本。</span><span class="sxs-lookup"><span data-stu-id="c72b2-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c72b2-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="c72b2-118">Getting started</span></span>
<span data-ttu-id="c72b2-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="c72b2-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="c72b2-120">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="c72b2-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c72b2-121">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="c72b2-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="c72b2-122">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="c72b2-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c72b2-123">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="c72b2-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c72b2-124">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="c72b2-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="c72b2-125">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="c72b2-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="c72b2-126">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="c72b2-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="c72b2-127">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="c72b2-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c72b2-128">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="c72b2-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="c72b2-129">當您使用 [工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="c72b2-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="c72b2-130">具有使用的 toocopy 資料從內部部署 Teradata 資料存放區的 Data Factory 實體的 JSON 定義中的範例，請參閱[JSON 範例： 將資料從 Teradata tooAzure Blob 複製](#json-example-copy-data-from-teradata-to-azure-blob)本文一節。</span><span class="sxs-lookup"><span data-stu-id="c72b2-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c72b2-131">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 tooa Teradata 資料存放區的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="c72b2-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c72b2-132">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="c72b2-132">Linked service properties</span></span>
<span data-ttu-id="c72b2-133">下表中的 hello 提供 JSON 項目特定 tooTeradata 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="c72b2-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="c72b2-134">屬性</span><span class="sxs-lookup"><span data-stu-id="c72b2-134">Property</span></span> | <span data-ttu-id="c72b2-135">說明</span><span class="sxs-lookup"><span data-stu-id="c72b2-135">Description</span></span> | <span data-ttu-id="c72b2-136">必要</span><span class="sxs-lookup"><span data-stu-id="c72b2-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c72b2-137">類型</span><span class="sxs-lookup"><span data-stu-id="c72b2-137">type</span></span> |<span data-ttu-id="c72b2-138">hello 類型屬性必須設定為： **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="c72b2-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="c72b2-139">是</span><span class="sxs-lookup"><span data-stu-id="c72b2-139">Yes</span></span> |
| <span data-ttu-id="c72b2-140">伺服器</span><span class="sxs-lookup"><span data-stu-id="c72b2-140">server</span></span> |<span data-ttu-id="c72b2-141">Hello Teradata 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c72b2-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="c72b2-142">是</span><span class="sxs-lookup"><span data-stu-id="c72b2-142">Yes</span></span> |
| <span data-ttu-id="c72b2-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c72b2-143">authenticationType</span></span> |<span data-ttu-id="c72b2-144">Tooconnect toohello Teradata 資料庫使用的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="c72b2-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="c72b2-145">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="c72b2-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="c72b2-146">是</span><span class="sxs-lookup"><span data-stu-id="c72b2-146">Yes</span></span> |
| <span data-ttu-id="c72b2-147">username</span><span class="sxs-lookup"><span data-stu-id="c72b2-147">username</span></span> |<span data-ttu-id="c72b2-148">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c72b2-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="c72b2-149">否</span><span class="sxs-lookup"><span data-stu-id="c72b2-149">No</span></span> |
| <span data-ttu-id="c72b2-150">password</span><span class="sxs-lookup"><span data-stu-id="c72b2-150">password</span></span> |<span data-ttu-id="c72b2-151">指定 hello hello 使用者名稱所指定的使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="c72b2-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="c72b2-152">否</span><span class="sxs-lookup"><span data-stu-id="c72b2-152">No</span></span> |
| <span data-ttu-id="c72b2-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c72b2-153">gatewayName</span></span> |<span data-ttu-id="c72b2-154">Hello Data Factory 服務的 hello 閘道的名稱應該使用 tooconnect toohello 在內部部署 Teradata 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c72b2-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="c72b2-155">是</span><span class="sxs-lookup"><span data-stu-id="c72b2-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c72b2-156">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="c72b2-156">Dataset properties</span></span>
<span data-ttu-id="c72b2-157">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="c72b2-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c72b2-158">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="c72b2-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c72b2-159">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c72b2-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="c72b2-160">目前沒有任何支援 hello Teradata 資料集的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="c72b2-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c72b2-161">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="c72b2-161">Copy activity properties</span></span>
<span data-ttu-id="c72b2-162">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="c72b2-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c72b2-163">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="c72b2-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="c72b2-164">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="c72b2-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="c72b2-165">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="c72b2-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="c72b2-166">當 hello 來源屬於型別**RelationalSource** （包括 Teradata） 中的下列屬性的 hello 可用**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="c72b2-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="c72b2-167">屬性</span><span class="sxs-lookup"><span data-stu-id="c72b2-167">Property</span></span> | <span data-ttu-id="c72b2-168">說明</span><span class="sxs-lookup"><span data-stu-id="c72b2-168">Description</span></span> | <span data-ttu-id="c72b2-169">允許的值</span><span class="sxs-lookup"><span data-stu-id="c72b2-169">Allowed values</span></span> | <span data-ttu-id="c72b2-170">必要</span><span class="sxs-lookup"><span data-stu-id="c72b2-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c72b2-171">query</span><span class="sxs-lookup"><span data-stu-id="c72b2-171">query</span></span> |<span data-ttu-id="c72b2-172">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="c72b2-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="c72b2-173">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="c72b2-173">SQL query string.</span></span> <span data-ttu-id="c72b2-174">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="c72b2-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="c72b2-175">是</span><span class="sxs-lookup"><span data-stu-id="c72b2-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="c72b2-176">JSON 範例： 從 Teradata tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="c72b2-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="c72b2-177">hello 下列範例將提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="c72b2-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c72b2-178">它們會顯示如何從 Teradata tooAzure Blob 儲存體 toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="c72b2-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="c72b2-179">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="c72b2-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="c72b2-180">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="c72b2-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="c72b2-181">[OnPremisesTeradata](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="c72b2-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="c72b2-182">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="c72b2-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c72b2-183">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="c72b2-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="c72b2-184">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="c72b2-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c72b2-185">hello[管線](data-factory-create-pipelines.md)與使用複製活動[RelationalSource](#copy-activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)。</span><span class="sxs-lookup"><span data-stu-id="c72b2-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c72b2-186">hello 範例將資料從 Teradata 資料庫 tooa blob 中的查詢結果的每個小時。</span><span class="sxs-lookup"><span data-stu-id="c72b2-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="c72b2-187">這些範例中使用的 hello JSON 內容所述後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="c72b2-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="c72b2-188">第一個步驟中，安裝程式 hello 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="c72b2-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="c72b2-189">hello 中的 hello 指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="c72b2-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c72b2-190">**Teradata 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="c72b2-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="c72b2-191">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="c72b2-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="c72b2-192">**Teradata 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="c72b2-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="c72b2-193">hello 範例假設您已建立資料表"MyTable"中 Teradata 和它包含稱為"timestamp"時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="c72b2-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="c72b2-194">設定 「 外部 」: true 會在該 hello 資料表是外部 toohello 資料處理站並不產生 hello data factory 中的活動時通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="c72b2-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
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

<span data-ttu-id="c72b2-195">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="c72b2-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c72b2-196">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="c72b2-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c72b2-197">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="c72b2-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="c72b2-198">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="c72b2-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="c72b2-199">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="c72b2-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="c72b2-200">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為每小時排程的 toorun。</span><span class="sxs-lookup"><span data-stu-id="c72b2-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="c72b2-201">在 hello 管線 JSON 定義中，hello**來源**類型設定得**RelationalSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="c72b2-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="c72b2-202">指定 hello SQL 查詢**查詢**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="c72b2-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="c72b2-203">Teradata 的類型對應</span><span class="sxs-lookup"><span data-stu-id="c72b2-203">Type mapping for Teradata</span></span>
<span data-ttu-id="c72b2-204">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會執行自動類型轉換來源類型 toosink 類型以 hello 遵循 2 步驟方法：</span><span class="sxs-lookup"><span data-stu-id="c72b2-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="c72b2-205">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="c72b2-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="c72b2-206">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="c72b2-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="c72b2-207">當您移動資料 tooTeradata，hello 下列會使用對應從 Teradata 類型 too.NET 型別。</span><span class="sxs-lookup"><span data-stu-id="c72b2-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="c72b2-208">Teradata 資料庫類型</span><span class="sxs-lookup"><span data-stu-id="c72b2-208">Teradata Database type</span></span> | <span data-ttu-id="c72b2-209">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="c72b2-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="c72b2-210">Char</span><span class="sxs-lookup"><span data-stu-id="c72b2-210">Char</span></span> |<span data-ttu-id="c72b2-211">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-211">String</span></span> |
| <span data-ttu-id="c72b2-212">Clob</span><span class="sxs-lookup"><span data-stu-id="c72b2-212">Clob</span></span> |<span data-ttu-id="c72b2-213">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-213">String</span></span> |
| <span data-ttu-id="c72b2-214">圖形</span><span class="sxs-lookup"><span data-stu-id="c72b2-214">Graphic</span></span> |<span data-ttu-id="c72b2-215">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-215">String</span></span> |
| <span data-ttu-id="c72b2-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="c72b2-216">VarChar</span></span> |<span data-ttu-id="c72b2-217">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-217">String</span></span> |
| <span data-ttu-id="c72b2-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="c72b2-218">VarGraphic</span></span> |<span data-ttu-id="c72b2-219">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-219">String</span></span> |
| <span data-ttu-id="c72b2-220">Blob</span><span class="sxs-lookup"><span data-stu-id="c72b2-220">Blob</span></span> |<span data-ttu-id="c72b2-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c72b2-221">Byte[]</span></span> |
| <span data-ttu-id="c72b2-222">位元組</span><span class="sxs-lookup"><span data-stu-id="c72b2-222">Byte</span></span> |<span data-ttu-id="c72b2-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c72b2-223">Byte[]</span></span> |
| <span data-ttu-id="c72b2-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="c72b2-224">VarByte</span></span> |<span data-ttu-id="c72b2-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c72b2-225">Byte[]</span></span> |
| <span data-ttu-id="c72b2-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="c72b2-226">BigInt</span></span> |<span data-ttu-id="c72b2-227">Int64</span><span class="sxs-lookup"><span data-stu-id="c72b2-227">Int64</span></span> |
| <span data-ttu-id="c72b2-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="c72b2-228">ByteInt</span></span> |<span data-ttu-id="c72b2-229">Int16</span><span class="sxs-lookup"><span data-stu-id="c72b2-229">Int16</span></span> |
| <span data-ttu-id="c72b2-230">十進位</span><span class="sxs-lookup"><span data-stu-id="c72b2-230">Decimal</span></span> |<span data-ttu-id="c72b2-231">十進位</span><span class="sxs-lookup"><span data-stu-id="c72b2-231">Decimal</span></span> |
| <span data-ttu-id="c72b2-232">兩倍</span><span class="sxs-lookup"><span data-stu-id="c72b2-232">Double</span></span> |<span data-ttu-id="c72b2-233">兩倍</span><span class="sxs-lookup"><span data-stu-id="c72b2-233">Double</span></span> |
| <span data-ttu-id="c72b2-234">Integer</span><span class="sxs-lookup"><span data-stu-id="c72b2-234">Integer</span></span> |<span data-ttu-id="c72b2-235">Int32</span><span class="sxs-lookup"><span data-stu-id="c72b2-235">Int32</span></span> |
| <span data-ttu-id="c72b2-236">Number</span><span class="sxs-lookup"><span data-stu-id="c72b2-236">Number</span></span> |<span data-ttu-id="c72b2-237">兩倍</span><span class="sxs-lookup"><span data-stu-id="c72b2-237">Double</span></span> |
| <span data-ttu-id="c72b2-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="c72b2-238">SmallInt</span></span> |<span data-ttu-id="c72b2-239">Int16</span><span class="sxs-lookup"><span data-stu-id="c72b2-239">Int16</span></span> |
| <span data-ttu-id="c72b2-240">Date</span><span class="sxs-lookup"><span data-stu-id="c72b2-240">Date</span></span> |<span data-ttu-id="c72b2-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="c72b2-241">DateTime</span></span> |
| <span data-ttu-id="c72b2-242">時間</span><span class="sxs-lookup"><span data-stu-id="c72b2-242">Time</span></span> |<span data-ttu-id="c72b2-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c72b2-243">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-244">時區的時間</span><span class="sxs-lookup"><span data-stu-id="c72b2-244">Time With Time Zone</span></span> |<span data-ttu-id="c72b2-245">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-245">String</span></span> |
| <span data-ttu-id="c72b2-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="c72b2-246">Timestamp</span></span> |<span data-ttu-id="c72b2-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="c72b2-247">DateTime</span></span> |
| <span data-ttu-id="c72b2-248">時區的時間戳記</span><span class="sxs-lookup"><span data-stu-id="c72b2-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="c72b2-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="c72b2-249">DateTimeOffset</span></span> |
| <span data-ttu-id="c72b2-250">間隔日</span><span class="sxs-lookup"><span data-stu-id="c72b2-250">Interval Day</span></span> |<span data-ttu-id="c72b2-251">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-251">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-252">間隔日期 tooHour</span><span class="sxs-lookup"><span data-stu-id="c72b2-252">Interval Day tooHour</span></span> |<span data-ttu-id="c72b2-253">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-253">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-254">間隔日期 tooMinute</span><span class="sxs-lookup"><span data-stu-id="c72b2-254">Interval Day tooMinute</span></span> |<span data-ttu-id="c72b2-255">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-255">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-256">間隔日期 tooSecond</span><span class="sxs-lookup"><span data-stu-id="c72b2-256">Interval Day tooSecond</span></span> |<span data-ttu-id="c72b2-257">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-257">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-258">間隔小時</span><span class="sxs-lookup"><span data-stu-id="c72b2-258">Interval Hour</span></span> |<span data-ttu-id="c72b2-259">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-259">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-260">間隔小時 tooMinute</span><span class="sxs-lookup"><span data-stu-id="c72b2-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="c72b2-261">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-261">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-262">間隔小時 tooSecond</span><span class="sxs-lookup"><span data-stu-id="c72b2-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="c72b2-263">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-263">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-264">間隔分鐘</span><span class="sxs-lookup"><span data-stu-id="c72b2-264">Interval Minute</span></span> |<span data-ttu-id="c72b2-265">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-265">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-266">間隔分鐘數 tooSecond</span><span class="sxs-lookup"><span data-stu-id="c72b2-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="c72b2-267">時間範圍</span><span class="sxs-lookup"><span data-stu-id="c72b2-267">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-268">間隔第二</span><span class="sxs-lookup"><span data-stu-id="c72b2-268">Interval Second</span></span> |<span data-ttu-id="c72b2-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c72b2-269">TimeSpan</span></span> |
| <span data-ttu-id="c72b2-270">間隔年</span><span class="sxs-lookup"><span data-stu-id="c72b2-270">Interval Year</span></span> |<span data-ttu-id="c72b2-271">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-271">String</span></span> |
| <span data-ttu-id="c72b2-272">間隔年 tooMonth</span><span class="sxs-lookup"><span data-stu-id="c72b2-272">Interval Year tooMonth</span></span> |<span data-ttu-id="c72b2-273">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-273">String</span></span> |
| <span data-ttu-id="c72b2-274">間隔月</span><span class="sxs-lookup"><span data-stu-id="c72b2-274">Interval Month</span></span> |<span data-ttu-id="c72b2-275">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-275">String</span></span> |
| <span data-ttu-id="c72b2-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="c72b2-276">Period(Date)</span></span> |<span data-ttu-id="c72b2-277">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-277">String</span></span> |
| <span data-ttu-id="c72b2-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="c72b2-278">Period(Time)</span></span> |<span data-ttu-id="c72b2-279">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-279">String</span></span> |
| <span data-ttu-id="c72b2-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="c72b2-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="c72b2-281">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-281">String</span></span> |
| <span data-ttu-id="c72b2-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="c72b2-282">Period(Timestamp)</span></span> |<span data-ttu-id="c72b2-283">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-283">String</span></span> |
| <span data-ttu-id="c72b2-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="c72b2-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="c72b2-285">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-285">String</span></span> |
| <span data-ttu-id="c72b2-286">Xml</span><span class="sxs-lookup"><span data-stu-id="c72b2-286">Xml</span></span> |<span data-ttu-id="c72b2-287">String</span><span class="sxs-lookup"><span data-stu-id="c72b2-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="c72b2-288">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="c72b2-288">Map source toosink columns</span></span>
<span data-ttu-id="c72b2-289">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="c72b2-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c72b2-290">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="c72b2-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="c72b2-291">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="c72b2-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="c72b2-292">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="c72b2-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c72b2-293">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="c72b2-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c72b2-294">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="c72b2-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c72b2-295">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="c72b2-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c72b2-296">效能和微調</span><span class="sxs-lookup"><span data-stu-id="c72b2-296">Performance and Tuning</span></span>
<span data-ttu-id="c72b2-297">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="c72b2-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
