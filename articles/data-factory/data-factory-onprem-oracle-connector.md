---
title: "aaaCopy 資料從 Oracle 使用 Data Factory 的 / |Microsoft 文件"
description: "了解如何 toocopy 資料從 Oracle 資料庫，則使用內部 Azure Data Factory。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="26df9-103">使用 Azure Data Factory 從內部部署 Oracle 來回複製資料</span><span class="sxs-lookup"><span data-stu-id="26df9-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="26df9-104">本文說明如何 toouse hello Azure Data Factory toomove 資料從內部部署 Oracle 資料庫中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="26df9-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="26df9-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="26df9-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="26df9-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="26df9-106">Supported scenarios</span></span>
<span data-ttu-id="26df9-107">您可以將資料複製**從 Oracle 資料庫**toohello 下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="26df9-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="26df9-108">您可以將資料複製下列資料存放區的 hello **tooan Oracle 資料庫**:</span><span class="sxs-lookup"><span data-stu-id="26df9-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="26df9-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="26df9-109">Prerequisites</span></span>
<span data-ttu-id="26df9-110">Data Factory 支援使用 hello 資料管理閘道的連線 tooon 內部部署 Oracle 來源。</span><span class="sxs-lookup"><span data-stu-id="26df9-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="26df9-111">請參閱[資料管理閘道器](data-factory-data-management-gateway.md)資料管理閘道的相關文章 toolearn 和[將資料從內部部署 toocloud 移](data-factory-move-data-between-onprem-and-cloud.md)文件以取得逐步指示，說明設定 hello 閘道在資料管線toomove 資料。</span><span class="sxs-lookup"><span data-stu-id="26df9-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="26df9-112">即使 hello Oracle 裝載於 Azure IaaS VM 需要閘道。</span><span class="sxs-lookup"><span data-stu-id="26df9-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="26df9-113">您可以在 hello 相同 IaaS VM 做為 hello 資料儲存或不同的 VM 只要 hello 閘道上可以連接 toohello 資料庫上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="26df9-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="26df9-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="26df9-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="26df9-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="26df9-115">Supported versions and installation</span></span>
<span data-ttu-id="26df9-116">此 Oracle 連接器支援兩種驅動程式版本︰</span><span class="sxs-lookup"><span data-stu-id="26df9-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="26df9-117">**Oracle （建議選項） 的 Microsoft 驅動程式**： 從資料管理閘道器版本 2.7，Microsoft 驅動程式安裝適用於 Oracle 的自動與 hello 閘道，所以您不需要順序的 tooadditionally 控制代碼 hello 驅動程式tooestablish 連線 tooOracle，而且您也會發生較佳複製的效能，使用此驅動程式。</span><span class="sxs-lookup"><span data-stu-id="26df9-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="26df9-118">支援以下版本的 Oracle 資料庫︰</span><span class="sxs-lookup"><span data-stu-id="26df9-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="26df9-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="26df9-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="26df9-120">Oracle 11g R1、R2 (11.1、11.2)</span><span class="sxs-lookup"><span data-stu-id="26df9-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="26df9-121">Oracle 10g R1、R2 (10.1、10.2)</span><span class="sxs-lookup"><span data-stu-id="26df9-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="26df9-122">Oracle 9i R1、R2 (9.0.1、9.2)</span><span class="sxs-lookup"><span data-stu-id="26df9-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="26df9-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="26df9-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26df9-124">目前 Oracle 的 Microsoft 驅動程式僅支援從 Oracle，但不是撰寫 tooOracle 複製資料。</span><span class="sxs-lookup"><span data-stu-id="26df9-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="26df9-125">並注意 hello 測試連線能力資料管理閘道診斷 索引標籤中的不支援此驅動程式。</span><span class="sxs-lookup"><span data-stu-id="26df9-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="26df9-126">或者，您可以使用 hello 複製精靈 toovalidate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="26df9-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="26df9-127">**適用於.NET 的 oracle 資料提供者：**您也可以選擇從 toouse Oracle 資料提供者 toocopy 資料 / tooOracle。</span><span class="sxs-lookup"><span data-stu-id="26df9-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="26df9-128">此元件包含於 [適用於 Windows 的 Oracle 資料存取元件](http://www.oracle.com/technetwork/topics/dotnet/downloads/)中。</span><span class="sxs-lookup"><span data-stu-id="26df9-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="26df9-129">Hello hello 閘道安裝所在的電腦上安裝 hello 適當版本 （32/64 位元）。</span><span class="sxs-lookup"><span data-stu-id="26df9-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="26df9-130">[Oracle 資料提供者.NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149)可以存取 tooOracle Database 10g Release 2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="26df9-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="26df9-131">如果您選擇 「 XCopy 安裝 」，請遵循 hello readme.htm 中的步驟。</span><span class="sxs-lookup"><span data-stu-id="26df9-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="26df9-132">我們建議您選擇 hello 安裝程式與 UI (非-XCopy 一個)。</span><span class="sxs-lookup"><span data-stu-id="26df9-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="26df9-133">安裝 hello 提供者之後,**重新啟動**hello 使用 [服務] 小程式 （或） 資料管理閘道組態管理員在電腦上的資料管理閘道主機服務。</span><span class="sxs-lookup"><span data-stu-id="26df9-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="26df9-134">如果您使用複製精靈 tooauthor hello 複製管線，hello 驅動程式類型將會自動決定。</span><span class="sxs-lookup"><span data-stu-id="26df9-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="26df9-135">預設將會使用 Microsoft 驅動程式，除非您的閘道版本低於 2.7 或您選擇使用 Oracle 作為接收 (Sink)。</span><span class="sxs-lookup"><span data-stu-id="26df9-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="26df9-136">開始使用</span><span class="sxs-lookup"><span data-stu-id="26df9-136">Getting started</span></span>
<span data-ttu-id="26df9-137">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出內部部署的 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="26df9-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="26df9-138">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="26df9-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="26df9-139">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="26df9-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="26df9-140">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="26df9-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="26df9-141">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="26df9-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="26df9-142">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="26df9-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="26df9-143">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="26df9-143">Create a **data factory**.</span></span> <span data-ttu-id="26df9-144">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="26df9-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="26df9-145">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="26df9-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="26df9-146">例如，如果您從 Azure blob 儲存體 Oralce 資料庫 tooan 複製資料，您建立兩個連結的服務 toolink Oracle 資料庫和 Azure 儲存體帳戶 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="26df9-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="26df9-147">連結的服務是特定 tooOracle 的內容，請參閱[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="26df9-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="26df9-148">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="26df9-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="26df9-149">在 hello hello 最後一個步驟中所述的範例，您可以建立資料集 toospecify hello 資料表包含 hello 輸入的資料的 Oracle 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="26df9-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="26df9-150">建立另一個資料集 toospecify hello blob 容器及保存 hello 資料 hello 資料夾 hello 從 Oracle 資料庫複製。</span><span class="sxs-lookup"><span data-stu-id="26df9-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="26df9-151">資料集是特定 tooOracle 的屬性，請參閱[資料集屬性](#dataset-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="26df9-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="26df9-152">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="26df9-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="26df9-153">在先前所述 hello 範例中，您使用 OracleSource 作為來源和 BlobSink 做為接收器 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="26df9-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="26df9-154">同樣地，如果您要從 Azure Blob 儲存體 tooOracle 資料庫複製，請使用 BlobSource 和 OracleSink hello 複製活動中。</span><span class="sxs-lookup"><span data-stu-id="26df9-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="26df9-155">複製活動特定 tooOracle 資料庫的內容，請參閱[複製活動屬性](#copy-activity-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="26df9-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="26df9-156">如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。</span><span class="sxs-lookup"><span data-stu-id="26df9-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="26df9-157">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="26df9-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="26df9-158">當您使用 工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="26df9-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="26df9-159">如需使用的 toocopy 資料，從內部部署 Oracle 資料庫的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-oracle-database)本文一節。</span><span class="sxs-lookup"><span data-stu-id="26df9-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="26df9-160">hello 下列各節提供有關使用的 toodefine Data Factory 實體的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="26df9-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="26df9-161">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="26df9-161">Linked service properties</span></span>
<span data-ttu-id="26df9-162">下表中的 hello 提供 JSON 項目特定 tooOracle 連結服務的描述。</span><span class="sxs-lookup"><span data-stu-id="26df9-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="26df9-163">屬性</span><span class="sxs-lookup"><span data-stu-id="26df9-163">Property</span></span> | <span data-ttu-id="26df9-164">說明</span><span class="sxs-lookup"><span data-stu-id="26df9-164">Description</span></span> | <span data-ttu-id="26df9-165">必要</span><span class="sxs-lookup"><span data-stu-id="26df9-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26df9-166">類型</span><span class="sxs-lookup"><span data-stu-id="26df9-166">type</span></span> |<span data-ttu-id="26df9-167">hello 類型屬性必須設定為： **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="26df9-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="26df9-168">是</span><span class="sxs-lookup"><span data-stu-id="26df9-168">Yes</span></span> |
| <span data-ttu-id="26df9-169">driverType</span><span class="sxs-lookup"><span data-stu-id="26df9-169">driverType</span></span> | <span data-ttu-id="26df9-170">指定從哪一個驅動程式 toouse toocopy 資料 / tooOracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="26df9-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="26df9-171">允許的值為 **Microsoft** 或 **ODP** (預設值)。</span><span class="sxs-lookup"><span data-stu-id="26df9-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="26df9-172">如需驅動程式詳細資料，請參閱[支援的版本和安裝](#supported-versions-and-installation)一節。</span><span class="sxs-lookup"><span data-stu-id="26df9-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="26df9-173">否</span><span class="sxs-lookup"><span data-stu-id="26df9-173">No</span></span> |
| <span data-ttu-id="26df9-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="26df9-174">connectionString</span></span> | <span data-ttu-id="26df9-175">指定所需的資訊 tooconnect toohello Oracle 資料庫執行個體 hello connectionString 屬性。</span><span class="sxs-lookup"><span data-stu-id="26df9-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="26df9-176">是</span><span class="sxs-lookup"><span data-stu-id="26df9-176">Yes</span></span> |
| <span data-ttu-id="26df9-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="26df9-177">gatewayName</span></span> | <span data-ttu-id="26df9-178">Hello 閘道名稱，是使用的 tooconnect toohello 在內部部署 Oracle 伺服器</span><span class="sxs-lookup"><span data-stu-id="26df9-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="26df9-179">是</span><span class="sxs-lookup"><span data-stu-id="26df9-179">Yes</span></span> |

<span data-ttu-id="26df9-180">**範例︰使用 Microsoft 驅動程式：**</span><span class="sxs-lookup"><span data-stu-id="26df9-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="26df9-181">**範例︰使用 ODP 驅動程式**</span><span class="sxs-lookup"><span data-stu-id="26df9-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="26df9-182">請參閱太[此站台](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/)hello 允許的格式。</span><span class="sxs-lookup"><span data-stu-id="26df9-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="26df9-183">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="26df9-183">Dataset properties</span></span>
<span data-ttu-id="26df9-184">區段和屬性可用來定義資料集的完整清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="26df9-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="26df9-185">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (Oracle、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="26df9-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="26df9-186">hello typeProperties 章節是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="26df9-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="26df9-187">hello 資料集 」 的型別 OracleTable 中的 hello typeProperties 區段具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="26df9-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="26df9-188">屬性</span><span class="sxs-lookup"><span data-stu-id="26df9-188">Property</span></span> | <span data-ttu-id="26df9-189">說明</span><span class="sxs-lookup"><span data-stu-id="26df9-189">Description</span></span> | <span data-ttu-id="26df9-190">必要</span><span class="sxs-lookup"><span data-stu-id="26df9-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26df9-191">tableName</span><span class="sxs-lookup"><span data-stu-id="26df9-191">tableName</span></span> |<span data-ttu-id="26df9-192">Hello hello 連結的服務的 Oracle 資料庫中的 hello 資料表名稱參考。</span><span class="sxs-lookup"><span data-stu-id="26df9-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="26df9-193">否 (如果已指定 **OracleSource** 的 **oracleReaderQuery**)</span><span class="sxs-lookup"><span data-stu-id="26df9-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="26df9-194">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="26df9-194">Copy activity properties</span></span>
<span data-ttu-id="26df9-195">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="26df9-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="26df9-196">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="26df9-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="26df9-197">hello 複製活動會採用只有 1 個輸入，並產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="26df9-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="26df9-198">而 hello 活動 hello typeProperties 區段中可用的屬性會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="26df9-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="26df9-199">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="26df9-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="26df9-200">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="26df9-200">OracleSource</span></span>
<span data-ttu-id="26df9-201">複製活動中，當 hello 來源的類型為**OracleSource** hello 下列屬性可用於**typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="26df9-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="26df9-202">屬性</span><span class="sxs-lookup"><span data-stu-id="26df9-202">Property</span></span> | <span data-ttu-id="26df9-203">說明</span><span class="sxs-lookup"><span data-stu-id="26df9-203">Description</span></span> | <span data-ttu-id="26df9-204">允許的值</span><span class="sxs-lookup"><span data-stu-id="26df9-204">Allowed values</span></span> | <span data-ttu-id="26df9-205">必要</span><span class="sxs-lookup"><span data-stu-id="26df9-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26df9-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="26df9-206">oracleReaderQuery</span></span> |<span data-ttu-id="26df9-207">使用自訂查詢 tooread hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="26df9-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="26df9-208">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="26df9-208">SQL query string.</span></span> <span data-ttu-id="26df9-209">例如：select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="26df9-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="26df9-210">如果未指定，hello 執行的 SQL 陳述式： 選取 * from MyTable</span><span class="sxs-lookup"><span data-stu-id="26df9-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="26df9-211">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="26df9-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="26df9-212">管線</span><span class="sxs-lookup"><span data-stu-id="26df9-212">OracleSink</span></span>
<span data-ttu-id="26df9-213">**OracleSink**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="26df9-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="26df9-214">屬性</span><span class="sxs-lookup"><span data-stu-id="26df9-214">Property</span></span> | <span data-ttu-id="26df9-215">說明</span><span class="sxs-lookup"><span data-stu-id="26df9-215">Description</span></span> | <span data-ttu-id="26df9-216">允許的值</span><span class="sxs-lookup"><span data-stu-id="26df9-216">Allowed values</span></span> | <span data-ttu-id="26df9-217">必要</span><span class="sxs-lookup"><span data-stu-id="26df9-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26df9-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="26df9-218">writeBatchTimeout</span></span> |<span data-ttu-id="26df9-219">在逾時之前，請等待 hello 批次插入作業 toocomplete 時間。</span><span class="sxs-lookup"><span data-stu-id="26df9-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="26df9-220">時間範圍</span><span class="sxs-lookup"><span data-stu-id="26df9-220">timespan</span></span><br/><br/> <span data-ttu-id="26df9-221">範例：00:30:00 (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="26df9-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="26df9-222">否</span><span class="sxs-lookup"><span data-stu-id="26df9-222">No</span></span> |
| <span data-ttu-id="26df9-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="26df9-223">writeBatchSize</span></span> |<span data-ttu-id="26df9-224">當 hello 緩衝區大小到達叫用 writeBatchSize 時，請將資料插入 hello SQL 資料表。</span><span class="sxs-lookup"><span data-stu-id="26df9-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="26df9-225">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="26df9-225">Integer (number of rows)</span></span> |<span data-ttu-id="26df9-226">否 (預設值：100)</span><span class="sxs-lookup"><span data-stu-id="26df9-226">No (default: 100)</span></span> |
| <span data-ttu-id="26df9-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="26df9-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="26df9-228">複製活動 tooexecute 查詢指定的特定配量的資料清除。</span><span class="sxs-lookup"><span data-stu-id="26df9-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="26df9-229">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="26df9-229">A query statement.</span></span> |<span data-ttu-id="26df9-230">否</span><span class="sxs-lookup"><span data-stu-id="26df9-230">No</span></span> |
| <span data-ttu-id="26df9-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="26df9-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="26df9-232">指定資料行名稱複製活動 toofill 與自動產生配量識別項，也就是使用的 tooclean 何時重新執行的特定配量的資料。</span><span class="sxs-lookup"><span data-stu-id="26df9-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="26df9-233">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="26df9-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="26df9-234">否</span><span class="sxs-lookup"><span data-stu-id="26df9-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="26df9-235">從 Oracle 資料庫複製資料 tooand JSON 範例</span><span class="sxs-lookup"><span data-stu-id="26df9-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="26df9-236">hello 下列範例將提供範例 JSON 定義您可以藉由使用 toocreate 管線[Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)或[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="26df9-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="26df9-237">它們會顯示如何從 toocopy 資料 / tooan Oracle 資料庫至 azure 或從 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="26df9-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="26df9-238">不過，資料可以複製的 tooany hello 接收所述的[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="26df9-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="26df9-239">範例： 從 Oracle tooAzure Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="26df9-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="26df9-240">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="26df9-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="26df9-241">[OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="26df9-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="26df9-242">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="26df9-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="26df9-243">[OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="26df9-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="26df9-244">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="26df9-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="26df9-245">具有使用 [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) 做為來源和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 做為接收之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="26df9-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="26df9-246">hello 範例從內部部署 Oracle 資料庫 tooa blob 中的資料表複製資料的每小時。</span><span class="sxs-lookup"><span data-stu-id="26df9-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="26df9-247">如需有關 hello 範例中所使用的各種屬性的詳細資訊，請參閱文件中後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="26df9-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="26df9-248">**Oracle 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="26df9-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="26df9-249">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="26df9-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="26df9-250">**Oracle 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="26df9-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="26df9-251">hello 範例假設已在 Oracle 中建立資料表"MyTable"，而且包含稱為"timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="26df9-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="26df9-252">設定"external":"true"會通知 hello Data Factory 服務的 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時。</span><span class="sxs-lookup"><span data-stu-id="26df9-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
        },
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

<span data-ttu-id="26df9-253">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="26df9-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="26df9-254">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="26df9-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="26df9-255">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="26df9-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="26df9-256">hello 資料夾路徑會使用 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="26df9-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="26df9-257">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="26df9-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="26df9-258">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為每小時排程的 toorun。</span><span class="sxs-lookup"><span data-stu-id="26df9-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="26df9-259">在 hello 管線 JSON 定義中，hello**來源**類型設定得**OracleSource**和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="26df9-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="26df9-260">使用指定的 hello SQL 查詢**oracleReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="26df9-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="26df9-261">範例： 將資料從 Azure Blob tooOracle 複製</span><span class="sxs-lookup"><span data-stu-id="26df9-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="26df9-262">這個範例示範如何從 Azure Blob 儲存體 tooan toocopy 資料內部部署 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="26df9-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="26df9-263">不過，資料可以複製**直接**從任何所述的 hello 來源[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 hello Azure Data Factory 中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="26df9-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="26df9-264">hello 範例具有下列資料 factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="26df9-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="26df9-265">[OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="26df9-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="26df9-266">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="26df9-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="26df9-267">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="26df9-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="26df9-268">[OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="26df9-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="26df9-269">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 做為來源和 [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) 做為接收之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="26df9-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="26df9-270">hello 範例將資料從內部部署 Oracle 資料庫中的 blob tooa 資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="26df9-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="26df9-271">如需有關 hello 範例中所使用的各種屬性的詳細資訊，請參閱文件中後面 hello 範例的章節。</span><span class="sxs-lookup"><span data-stu-id="26df9-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="26df9-272">**Oracle 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="26df9-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="26df9-273">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="26df9-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="26df9-274">**Azure Blob 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="26df9-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="26df9-275">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="26df9-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="26df9-276">hello 資料夾路徑和檔案名稱 hello blob 會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="26df9-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="26df9-277">年、 月和日的部分 hello 開始時間，會使用 hello 資料夾路徑和檔案名稱會使用 hello hello 開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="26df9-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="26df9-278">"external":"true"的設定會在這個資料表是外部 toohello 資料處理站，而不產生 hello data factory 中的活動時通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="26df9-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
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

<span data-ttu-id="26df9-279">**Oracle 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="26df9-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="26df9-280">hello 範例假設您有在 Oracle 中建立資料表"MyTable"。</span><span class="sxs-lookup"><span data-stu-id="26df9-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="26df9-281">建立 hello 資料表與 Oracle 中如預期般 hello Blob CSV 檔案 toocontain hello 相同數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="26df9-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="26df9-282">新的資料列會加入 toohello 資料表的每個小時。</span><span class="sxs-lookup"><span data-stu-id="26df9-282">New rows are added toohello table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="26df9-283">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="26df9-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="26df9-284">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="26df9-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="26df9-285">在 hello 管線 JSON 定義中，hello**來源**類型設定得**BlobSource**和 hello**接收**類型設定得**OracleSink**。</span><span class="sxs-lookup"><span data-stu-id="26df9-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="26df9-286">疑難排解秘訣</span><span class="sxs-lookup"><span data-stu-id="26df9-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="26df9-287">問題 1：.NET Framework Data Provider</span><span class="sxs-lookup"><span data-stu-id="26df9-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="26df9-288">您會看到下列 hello**錯誤訊息**:</span><span class="sxs-lookup"><span data-stu-id="26df9-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="26df9-289">**可能的原因：**</span><span class="sxs-lookup"><span data-stu-id="26df9-289">**Possible causes:**</span></span>

1. <span data-ttu-id="26df9-290">未安裝.NET Framework Data Provider for Oracle hello。</span><span class="sxs-lookup"><span data-stu-id="26df9-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="26df9-291">hello Oracle 的.NET Framework 資料提供者已安裝的 too.NET Framework 2.0 和.NET Framework 4.0 hello 資料夾中找不到。</span><span class="sxs-lookup"><span data-stu-id="26df9-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="26df9-292">**解析/因應措施：**</span><span class="sxs-lookup"><span data-stu-id="26df9-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="26df9-293">如果您尚未安裝 hello.NET Provider for Oracle，[安裝](http://www.oracle.com/technetwork/topics/dotnet/downloads/)，然後重試 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="26df9-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="26df9-294">如果您收到 hello 錯誤即使安裝 hello 提供者之後，請下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="26df9-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="26df9-295">從 hello 資料夾開啟的.NET 2.0 的機器組態： <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config。</span><span class="sxs-lookup"><span data-stu-id="26df9-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="26df9-296">搜尋**適用於.NET 的 Oracle 資料提供者**，而且 hello 遵循底下的範例所示，您應該要能夠 toofind 項目**system.data** -> **DbProviderFactories**:"<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="適用於.NET 的 oracle 資料提供者</span><span class="sxs-lookup"><span data-stu-id="26df9-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="26df9-297">」的作法指南。</span><span class="sxs-lookup"><span data-stu-id="26df9-297">”</span></span>
3. <span data-ttu-id="26df9-298">將這個項目 toohello machine.config 檔案複製 hello 遵循 v4.0 資料夾中： <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config，並變更 hello 版本 too4.xxx.x.x。</span><span class="sxs-lookup"><span data-stu-id="26df9-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="26df9-299">執行 hello 全域組件快取 (GAC) 中安裝 「 < ODP.NET 安裝路徑 > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" `gacutil /i [provider path]`。 # # 疑難排解秘訣</span><span class="sxs-lookup"><span data-stu-id="26df9-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="26df9-300">問題 2︰日期時間格式</span><span class="sxs-lookup"><span data-stu-id="26df9-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="26df9-301">您會看到下列 hello**錯誤訊息**:</span><span class="sxs-lookup"><span data-stu-id="26df9-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="26df9-302">**解析/因應措施：**</span><span class="sxs-lookup"><span data-stu-id="26df9-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="26df9-303">您可能需要 tooadjust hello 查詢字串，在您根據在 Oracle 資料庫中，日期的設定方式 hello 下列所示的複製活動中 （使用 hello 使用 to_date 函式） 的範例：</span><span class="sxs-lookup"><span data-stu-id="26df9-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="26df9-304">Oracle 的類型對應</span><span class="sxs-lookup"><span data-stu-id="26df9-304">Type mapping for Oracle</span></span>
<span data-ttu-id="26df9-305">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)複製活動的文件以 hello 遵循 2 步驟方法執行從來源類型 toosink 類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="26df9-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="26df9-306">從原生的來源類型 too.NET 類型轉換</span><span class="sxs-lookup"><span data-stu-id="26df9-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="26df9-307">從.NET 型別 toonative 接收器類型轉換</span><span class="sxs-lookup"><span data-stu-id="26df9-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="26df9-308">當您從 Oracle 移動資料，從 Oracle 資料型別 too.NET 型別，反之亦然，會使用下列對應的 hello。</span><span class="sxs-lookup"><span data-stu-id="26df9-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="26df9-309">Oracle 資料類型</span><span class="sxs-lookup"><span data-stu-id="26df9-309">Oracle data type</span></span> | <span data-ttu-id="26df9-310">.NET Framework 資料類型</span><span class="sxs-lookup"><span data-stu-id="26df9-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="26df9-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="26df9-311">BFILE</span></span> |<span data-ttu-id="26df9-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="26df9-312">Byte[]</span></span> |
| <span data-ttu-id="26df9-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="26df9-313">BLOB</span></span> |<span data-ttu-id="26df9-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="26df9-314">Byte[]</span></span> |
| <span data-ttu-id="26df9-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="26df9-315">CHAR</span></span> |<span data-ttu-id="26df9-316">String</span><span class="sxs-lookup"><span data-stu-id="26df9-316">String</span></span> |
| <span data-ttu-id="26df9-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="26df9-317">CLOB</span></span> |<span data-ttu-id="26df9-318">String</span><span class="sxs-lookup"><span data-stu-id="26df9-318">String</span></span> |
| <span data-ttu-id="26df9-319">日期</span><span class="sxs-lookup"><span data-stu-id="26df9-319">DATE</span></span> |<span data-ttu-id="26df9-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="26df9-320">DateTime</span></span> |
| <span data-ttu-id="26df9-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="26df9-321">FLOAT</span></span> |<span data-ttu-id="26df9-322">Decimal，字串 (如果精確度 > 28)</span><span class="sxs-lookup"><span data-stu-id="26df9-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="26df9-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="26df9-323">INTEGER</span></span> |<span data-ttu-id="26df9-324">Decimal，字串 (如果精確度 > 28)</span><span class="sxs-lookup"><span data-stu-id="26df9-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="26df9-325">間隔年 tooMONTH</span><span class="sxs-lookup"><span data-stu-id="26df9-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="26df9-326">Int32</span><span class="sxs-lookup"><span data-stu-id="26df9-326">Int32</span></span> |
| <span data-ttu-id="26df9-327">間隔日期 tooSECOND</span><span class="sxs-lookup"><span data-stu-id="26df9-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="26df9-328">時間範圍</span><span class="sxs-lookup"><span data-stu-id="26df9-328">TimeSpan</span></span> |
| <span data-ttu-id="26df9-329">長</span><span class="sxs-lookup"><span data-stu-id="26df9-329">LONG</span></span> |<span data-ttu-id="26df9-330">String</span><span class="sxs-lookup"><span data-stu-id="26df9-330">String</span></span> |
| <span data-ttu-id="26df9-331">長 RAW</span><span class="sxs-lookup"><span data-stu-id="26df9-331">LONG RAW</span></span> |<span data-ttu-id="26df9-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="26df9-332">Byte[]</span></span> |
| <span data-ttu-id="26df9-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="26df9-333">NCHAR</span></span> |<span data-ttu-id="26df9-334">String</span><span class="sxs-lookup"><span data-stu-id="26df9-334">String</span></span> |
| <span data-ttu-id="26df9-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="26df9-335">NCLOB</span></span> |<span data-ttu-id="26df9-336">String</span><span class="sxs-lookup"><span data-stu-id="26df9-336">String</span></span> |
| <span data-ttu-id="26df9-337">數字</span><span class="sxs-lookup"><span data-stu-id="26df9-337">NUMBER</span></span> |<span data-ttu-id="26df9-338">Decimal，字串 (如果精確度 > 28)</span><span class="sxs-lookup"><span data-stu-id="26df9-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="26df9-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="26df9-339">NVARCHAR2</span></span> |<span data-ttu-id="26df9-340">String</span><span class="sxs-lookup"><span data-stu-id="26df9-340">String</span></span> |
| <span data-ttu-id="26df9-341">RAW</span><span class="sxs-lookup"><span data-stu-id="26df9-341">RAW</span></span> |<span data-ttu-id="26df9-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="26df9-342">Byte[]</span></span> |
| <span data-ttu-id="26df9-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="26df9-343">ROWID</span></span> |<span data-ttu-id="26df9-344">String</span><span class="sxs-lookup"><span data-stu-id="26df9-344">String</span></span> |
| <span data-ttu-id="26df9-345">時間戳記</span><span class="sxs-lookup"><span data-stu-id="26df9-345">TIMESTAMP</span></span> |<span data-ttu-id="26df9-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="26df9-346">DateTime</span></span> |
| <span data-ttu-id="26df9-347">本地時區的時間戳記</span><span class="sxs-lookup"><span data-stu-id="26df9-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="26df9-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="26df9-348">DateTime</span></span> |
| <span data-ttu-id="26df9-349">時區的時間戳記</span><span class="sxs-lookup"><span data-stu-id="26df9-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="26df9-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="26df9-350">DateTime</span></span> |
| <span data-ttu-id="26df9-351">不帶正負號的整數</span><span class="sxs-lookup"><span data-stu-id="26df9-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="26df9-352">數字</span><span class="sxs-lookup"><span data-stu-id="26df9-352">Number</span></span> |
| <span data-ttu-id="26df9-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="26df9-353">VARCHAR2</span></span> |<span data-ttu-id="26df9-354">String</span><span class="sxs-lookup"><span data-stu-id="26df9-354">String</span></span> |
| <span data-ttu-id="26df9-355">XML</span><span class="sxs-lookup"><span data-stu-id="26df9-355">XML</span></span> |<span data-ttu-id="26df9-356">String</span><span class="sxs-lookup"><span data-stu-id="26df9-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="26df9-357">資料型別**INTERVAL YEAR tooMONTH**和**INTERVAL DAY tooSECOND**時使用 Microsoft 驅動程式不支援。</span><span class="sxs-lookup"><span data-stu-id="26df9-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="26df9-358">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="26df9-358">Map source toosink columns</span></span>
<span data-ttu-id="26df9-359">toolearn 對應中之資料行來源的資料集 toocolumns 中接收的資料集，請參閱[Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="26df9-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="26df9-360">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="26df9-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="26df9-361">複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="26df9-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="26df9-362">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="26df9-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="26df9-363">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="26df9-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="26df9-364">當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。</span><span class="sxs-lookup"><span data-stu-id="26df9-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="26df9-365">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="26df9-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="26df9-366">效能和微調</span><span class="sxs-lookup"><span data-stu-id="26df9-366">Performance and Tuning</span></span>
<span data-ttu-id="26df9-367">請參閱[複製活動效能與調整指南](data-factory-copy-activity-performance.md)toolearn 金鑰的相關因素影響效能的資料移動 （複製活動） 在 Azure Data Factory 和各種方式 toooptimize 它。</span><span class="sxs-lookup"><span data-stu-id="26df9-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
