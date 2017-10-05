---
title: "使用 Data Factory 從 Oracle 來回複製資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從內部部署 Oracle 資料庫來回複製資料。"
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
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="4b57b-103">使用 Azure Data Factory 從內部部署 Oracle 來回複製資料</span><span class="sxs-lookup"><span data-stu-id="4b57b-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="4b57b-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，將資料移進/移出內部部署的 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4b57b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="4b57b-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="4b57b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="4b57b-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="4b57b-106">Supported scenarios</span></span>
<span data-ttu-id="4b57b-107">您可以**從 Oracle 資料庫**將資料複製到下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="4b57b-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="4b57b-108">您可以從下列資料存放區將資料複製**到 Oracle 資料庫**：</span><span class="sxs-lookup"><span data-stu-id="4b57b-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="4b57b-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="4b57b-109">Prerequisites</span></span>
<span data-ttu-id="4b57b-110">Data Factory 支援使用資料管理閘道連接至內部部署 Oracle 來源。</span><span class="sxs-lookup"><span data-stu-id="4b57b-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="4b57b-111">請參閱[資料管理閘道](data-factory-data-management-gateway.md)一文來了解資料管理閘道，以及[將資料從內部部署移動到雲端](data-factory-move-data-between-onprem-and-cloud.md)一文來取得設定資料管線的閘道以移動資料的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="4b57b-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="4b57b-112">即使 Oracle 裝載於 Azure IaaS VM 中，也必須要有閘道。</span><span class="sxs-lookup"><span data-stu-id="4b57b-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="4b57b-113">您可以將閘道安裝在與資料存放區相同或相異的 IaaS VM 上，只要閘道可以連線到資料庫即可。</span><span class="sxs-lookup"><span data-stu-id="4b57b-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="4b57b-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="4b57b-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="4b57b-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="4b57b-115">Supported versions and installation</span></span>
<span data-ttu-id="4b57b-116">此 Oracle 連接器支援兩種驅動程式版本︰</span><span class="sxs-lookup"><span data-stu-id="4b57b-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="4b57b-117">**適用於 Oracle 的 Microsoft 驅動程式 (建議)**：從資料管理閘道 2.7 版開始，適用於 Oracle 的 Microsoft 驅動程式會自動隨閘道安裝，因此您不需要另行處理驅動程式，即能建立與 Oracle 的連線，而且使用此驅動程式時您也可以體驗到更好的複製效能。</span><span class="sxs-lookup"><span data-stu-id="4b57b-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="4b57b-118">支援以下版本的 Oracle 資料庫︰</span><span class="sxs-lookup"><span data-stu-id="4b57b-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="4b57b-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="4b57b-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="4b57b-120">Oracle 11g R1、R2 (11.1、11.2)</span><span class="sxs-lookup"><span data-stu-id="4b57b-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="4b57b-121">Oracle 10g R1、R2 (10.1、10.2)</span><span class="sxs-lookup"><span data-stu-id="4b57b-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="4b57b-122">Oracle 9i R1、R2 (9.0.1、9.2)</span><span class="sxs-lookup"><span data-stu-id="4b57b-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="4b57b-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="4b57b-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b57b-124">目前適用於 Oracle 的 Microsoft 驅動程式僅支援從 Oracle 複製資料，但不支援將資料寫入 Oracle。</span><span class="sxs-lookup"><span data-stu-id="4b57b-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="4b57b-125">請注意，[資料管理閘道診斷] 索引標籤中的測試連線功能不支援此驅動程式。</span><span class="sxs-lookup"><span data-stu-id="4b57b-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="4b57b-126">您可以選擇使用複製精靈來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="4b57b-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="4b57b-127">**.NET 的 Oracle 資料提供者︰**您也可以選擇使用 Oracle 資料提供者，從 Oracle 複製資料/將資料複製到 Oracle。</span><span class="sxs-lookup"><span data-stu-id="4b57b-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="4b57b-128">此元件包含於 [適用於 Windows 的 Oracle 資料存取元件](http://www.oracle.com/technetwork/topics/dotnet/downloads/)中。</span><span class="sxs-lookup"><span data-stu-id="4b57b-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="4b57b-129">在安裝閘道的電腦上安裝適當版本 (32/64 位元)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="4b57b-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) 可以存取 Oracle Database 10g Release 2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4b57b-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="4b57b-131">如果您選擇「XCopy 安裝」，請依照 readme.htm 中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="4b57b-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="4b57b-132">建議您選擇含有 UI 的安裝程式 (非 XCopy 安裝)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="4b57b-133">安裝提供者之後，請使用 [服務] 小程式 (或) 資料管理閘道組態管理員，「重新啟動」您電腦上的資料管理閘道主機服務。</span><span class="sxs-lookup"><span data-stu-id="4b57b-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="4b57b-134">若使用複製精靈來建立複製管線，系統將會自動決定驅動程式類型。</span><span class="sxs-lookup"><span data-stu-id="4b57b-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="4b57b-135">預設將會使用 Microsoft 驅動程式，除非您的閘道版本低於 2.7 或您選擇使用 Oracle 作為接收 (Sink)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4b57b-136">開始使用</span><span class="sxs-lookup"><span data-stu-id="4b57b-136">Getting started</span></span>
<span data-ttu-id="4b57b-137">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出內部部署的 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4b57b-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="4b57b-138">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="4b57b-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="4b57b-139">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="4b57b-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="4b57b-140">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="4b57b-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4b57b-141">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="4b57b-142">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="4b57b-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="4b57b-143">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="4b57b-143">Create a **data factory**.</span></span> <span data-ttu-id="4b57b-144">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="4b57b-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="4b57b-145">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="4b57b-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="4b57b-146">例如，如果您從 Oralce 資料庫將資料複製到 Azure Blob 儲存體，您會建立兩個連結服務，將 Oracle 資料庫和 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="4b57b-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="4b57b-147">針對 Oracle 專屬的連結服務屬性，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="4b57b-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="4b57b-148">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="4b57b-149">在上一個步驟所述的範例中，您可以建立資料集來指定包含輸入資料之 Oracle 資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="4b57b-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="4b57b-150">同時建立另一個資料集來指定 blob 容器和資料夾，該資料夾會保存從 Oracle 資料庫複製的資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="4b57b-151">針對 Oracle 專屬的資料集屬性，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="4b57b-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="4b57b-152">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="4b57b-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="4b57b-153">在稍早所述的範例中，您使用 OracleSource 作為來源，以及使用 BlobSink 作為複製活動的接收器。</span><span class="sxs-lookup"><span data-stu-id="4b57b-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="4b57b-154">同樣地，如果您是從 Azure Blob 儲存體複製到 Oracle 資料庫，則在複製活動中使用 BlobSource 和 OracleSink。</span><span class="sxs-lookup"><span data-stu-id="4b57b-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="4b57b-155">針對 Oracle 資料庫專屬的複製活動屬性，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="4b57b-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="4b57b-156">如需有關如何使用資料存放區作為來源或接收器的詳細資訊，按一下上一節中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="4b57b-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="4b57b-157">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="4b57b-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="4b57b-158">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="4b57b-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="4b57b-159">如需相關範例，其中含有用來將資料複製到內部部署 Oracle 資料庫 (或從內部部署 Oracle 資料庫複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples-for-copying-data-to-and-from-oracle-database)一節。</span><span class="sxs-lookup"><span data-stu-id="4b57b-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="4b57b-160">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="4b57b-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4b57b-161">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="4b57b-161">Linked service properties</span></span>
<span data-ttu-id="4b57b-162">下表提供 Oracle 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="4b57b-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="4b57b-163">屬性</span><span class="sxs-lookup"><span data-stu-id="4b57b-163">Property</span></span> | <span data-ttu-id="4b57b-164">說明</span><span class="sxs-lookup"><span data-stu-id="4b57b-164">Description</span></span> | <span data-ttu-id="4b57b-165">必要</span><span class="sxs-lookup"><span data-stu-id="4b57b-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4b57b-166">類型</span><span class="sxs-lookup"><span data-stu-id="4b57b-166">type</span></span> |<span data-ttu-id="4b57b-167">類型屬性必須設為： **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="4b57b-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="4b57b-168">是</span><span class="sxs-lookup"><span data-stu-id="4b57b-168">Yes</span></span> |
| <span data-ttu-id="4b57b-169">driverType</span><span class="sxs-lookup"><span data-stu-id="4b57b-169">driverType</span></span> | <span data-ttu-id="4b57b-170">指定要用來從 Oracle 複製資料/將資料複製到 Oracle 資料庫的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="4b57b-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="4b57b-171">允許的值為 **Microsoft** 或 **ODP** (預設值)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="4b57b-172">如需驅動程式詳細資料，請參閱[支援的版本和安裝](#supported-versions-and-installation)一節。</span><span class="sxs-lookup"><span data-stu-id="4b57b-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="4b57b-173">否</span><span class="sxs-lookup"><span data-stu-id="4b57b-173">No</span></span> |
| <span data-ttu-id="4b57b-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="4b57b-174">connectionString</span></span> | <span data-ttu-id="4b57b-175">針對 connectionString 屬性指定連接到 Oracle 資料庫執行個體所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="4b57b-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="4b57b-176">是</span><span class="sxs-lookup"><span data-stu-id="4b57b-176">Yes</span></span> |
| <span data-ttu-id="4b57b-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4b57b-177">gatewayName</span></span> | <span data-ttu-id="4b57b-178">用來連接到內部部署 Oracle 伺服器的閘道器名稱</span><span class="sxs-lookup"><span data-stu-id="4b57b-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="4b57b-179">是</span><span class="sxs-lookup"><span data-stu-id="4b57b-179">Yes</span></span> |

<span data-ttu-id="4b57b-180">**範例︰使用 Microsoft 驅動程式：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="4b57b-181">**範例︰使用 ODP 驅動程式**</span><span class="sxs-lookup"><span data-stu-id="4b57b-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="4b57b-182">如需了解有哪些允許的格式，請參閱[此網站 (英文)](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="4b57b-183">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="4b57b-183">Dataset properties</span></span>
<span data-ttu-id="4b57b-184">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="4b57b-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4b57b-185">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (Oracle、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="4b57b-186">每個資料集類型的 typeProperties 區段都不同，可提供資料存放區中資料的位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4b57b-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="4b57b-187">OracleTable 資料集類型的 typeProperties 區段具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="4b57b-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="4b57b-188">屬性</span><span class="sxs-lookup"><span data-stu-id="4b57b-188">Property</span></span> | <span data-ttu-id="4b57b-189">說明</span><span class="sxs-lookup"><span data-stu-id="4b57b-189">Description</span></span> | <span data-ttu-id="4b57b-190">必要</span><span class="sxs-lookup"><span data-stu-id="4b57b-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4b57b-191">tableName</span><span class="sxs-lookup"><span data-stu-id="4b57b-191">tableName</span></span> |<span data-ttu-id="4b57b-192">Oracle 資料庫中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="4b57b-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="4b57b-193">否 (如果已指定 **OracleSource** 的 **oracleReaderQuery**)</span><span class="sxs-lookup"><span data-stu-id="4b57b-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="4b57b-194">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="4b57b-194">Copy activity properties</span></span>
<span data-ttu-id="4b57b-195">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="4b57b-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4b57b-196">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="4b57b-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="4b57b-197">複製活動只會採用一個輸入，而且只產生一個輸出。</span><span class="sxs-lookup"><span data-stu-id="4b57b-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="4b57b-198">而活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4b57b-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="4b57b-199">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="4b57b-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="4b57b-200">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="4b57b-200">OracleSource</span></span>
<span data-ttu-id="4b57b-201">在複製活動中，如果來源的類型為 **OracleSource**，則 **typeProperties** 區段有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="4b57b-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="4b57b-202">屬性</span><span class="sxs-lookup"><span data-stu-id="4b57b-202">Property</span></span> | <span data-ttu-id="4b57b-203">說明</span><span class="sxs-lookup"><span data-stu-id="4b57b-203">Description</span></span> | <span data-ttu-id="4b57b-204">允許的值</span><span class="sxs-lookup"><span data-stu-id="4b57b-204">Allowed values</span></span> | <span data-ttu-id="4b57b-205">必要</span><span class="sxs-lookup"><span data-stu-id="4b57b-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b57b-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="4b57b-206">oracleReaderQuery</span></span> |<span data-ttu-id="4b57b-207">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-207">Use the custom query to read data.</span></span> |<span data-ttu-id="4b57b-208">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="4b57b-208">SQL query string.</span></span> <span data-ttu-id="4b57b-209">例如：select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="4b57b-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="4b57b-210">如果未指定，則為所執行的 SQL 陳述式：select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="4b57b-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="4b57b-211">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="4b57b-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="4b57b-212">管線</span><span class="sxs-lookup"><span data-stu-id="4b57b-212">OracleSink</span></span>
<span data-ttu-id="4b57b-213">**OracleSink** 支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="4b57b-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="4b57b-214">屬性</span><span class="sxs-lookup"><span data-stu-id="4b57b-214">Property</span></span> | <span data-ttu-id="4b57b-215">說明</span><span class="sxs-lookup"><span data-stu-id="4b57b-215">Description</span></span> | <span data-ttu-id="4b57b-216">允許的值</span><span class="sxs-lookup"><span data-stu-id="4b57b-216">Allowed values</span></span> | <span data-ttu-id="4b57b-217">必要</span><span class="sxs-lookup"><span data-stu-id="4b57b-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b57b-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="4b57b-218">writeBatchTimeout</span></span> |<span data-ttu-id="4b57b-219">在逾時前等待批次插入作業完成的時間。</span><span class="sxs-lookup"><span data-stu-id="4b57b-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="4b57b-220">時間範圍</span><span class="sxs-lookup"><span data-stu-id="4b57b-220">timespan</span></span><br/><br/> <span data-ttu-id="4b57b-221">範例：00:30:00 (30 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="4b57b-222">否</span><span class="sxs-lookup"><span data-stu-id="4b57b-222">No</span></span> |
| <span data-ttu-id="4b57b-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="4b57b-223">writeBatchSize</span></span> |<span data-ttu-id="4b57b-224">當緩衝區大小達到 writeBatchSize 時，將資料插入 SQL 資料表中</span><span class="sxs-lookup"><span data-stu-id="4b57b-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="4b57b-225">整數 (資料列數目)</span><span class="sxs-lookup"><span data-stu-id="4b57b-225">Integer (number of rows)</span></span> |<span data-ttu-id="4b57b-226">否 (預設值：100)</span><span class="sxs-lookup"><span data-stu-id="4b57b-226">No (default: 100)</span></span> |
| <span data-ttu-id="4b57b-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="4b57b-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="4b57b-228">指定要讓「複製活動」執行的查詢，以便清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="4b57b-229">查詢陳述式。</span><span class="sxs-lookup"><span data-stu-id="4b57b-229">A query statement.</span></span> |<span data-ttu-id="4b57b-230">否</span><span class="sxs-lookup"><span data-stu-id="4b57b-230">No</span></span> |
| <span data-ttu-id="4b57b-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="4b57b-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="4b57b-232">指定要讓「複製活動」以自動產生的分割識別碼填入的資料行名稱，這可在重新執行時用來清除特定分割的資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="4b57b-233">資料類型為 binary(32) 之資料行的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="4b57b-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="4b57b-234">否</span><span class="sxs-lookup"><span data-stu-id="4b57b-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="4b57b-235">從 Oracle 資料庫複製資料以及將資料複製到其中的 JSON 範例</span><span class="sxs-lookup"><span data-stu-id="4b57b-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="4b57b-236">下列範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="4b57b-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4b57b-237">這些範例示範如何將資料從 Oracle 資料庫複製到 Azure Blob 儲存體，以及複製其中的資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="4b57b-238">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="4b57b-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="4b57b-239">範例：將資料從 Oracle 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="4b57b-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="4b57b-240">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="4b57b-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="4b57b-241">[OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="4b57b-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="4b57b-242">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="4b57b-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4b57b-243">[OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="4b57b-244">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4b57b-245">具有使用 [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) 做為來源和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 做為接收之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="4b57b-246">此範例會每小時將資料從內部部署 Oracle 資料庫中的資料表移動到 Blob。</span><span class="sxs-lookup"><span data-stu-id="4b57b-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="4b57b-247">如需範例中使用的各種屬性的詳細資訊，請參閱範例後面幾節中的文件。</span><span class="sxs-lookup"><span data-stu-id="4b57b-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="4b57b-248">**Oracle 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="4b57b-249">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="4b57b-250">**Oracle 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="4b57b-251">此範例假設您已在 Oracle 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="4b57b-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="4b57b-252">設定 “external”: ”true” 會通知 Data Factory 服務：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="4b57b-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="4b57b-253">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="4b57b-254">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4b57b-255">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="4b57b-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="4b57b-256">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="4b57b-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="4b57b-257">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="4b57b-258">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="4b57b-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="4b57b-259">在管線 JSON 定義中，**source** 類型設為 **OracleSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="4b57b-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="4b57b-260">利用 **oracleReaderQuery** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="4b57b-261">範例：將資料從 Azure Blob 複製到 Oracle</span><span class="sxs-lookup"><span data-stu-id="4b57b-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="4b57b-262">此範例示範如何將資料從 Azure Blob 儲存體複製到內部部署 Oracle 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4b57b-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="4b57b-263">不過，您可以在 Azure Data Factory 中使用複製活動，**直接**從[這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats)所說的任何來源複製資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="4b57b-264">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="4b57b-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="4b57b-265">[OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="4b57b-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="4b57b-266">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="4b57b-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4b57b-267">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="4b57b-268">[OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4b57b-269">具有使用 [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) 做為來源和 [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) 做為接收之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="4b57b-270">此範例會每小時將資料從 Blob移動到內部部署 Oracle 資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="4b57b-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="4b57b-271">如需範例中使用的各種屬性的詳細資訊，請參閱範例後面幾節中的文件。</span><span class="sxs-lookup"><span data-stu-id="4b57b-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="4b57b-272">**Oracle 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="4b57b-273">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="4b57b-274">**Azure Blob 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="4b57b-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="4b57b-275">每小時從新的 Blob 挑選資料 (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4b57b-276">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="4b57b-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="4b57b-277">資料夾路徑使用開始時間的年、月、日部分，而檔案名稱使用開始時間的小時部分。</span><span class="sxs-lookup"><span data-stu-id="4b57b-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="4b57b-278">“external”: “true” 設定會通知 Data Factory 服務：這是 Data Factory 外部的資料表而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="4b57b-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="4b57b-279">**Oracle 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="4b57b-280">此範例假設您已在 Oracle 資料表中建立資料表 "MyTable"。</span><span class="sxs-lookup"><span data-stu-id="4b57b-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="4b57b-281">請在 Oracle 中建立此資料表，其資料行的數目如您預期 Blob CSV 檔案要包含的數目。</span><span class="sxs-lookup"><span data-stu-id="4b57b-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="4b57b-282">此資料表會每小時加入新的資料列。</span><span class="sxs-lookup"><span data-stu-id="4b57b-282">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="4b57b-283">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="4b57b-284">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="4b57b-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="4b57b-285">在管線 JSON 定義中，**source** 類型設為 **BlobSource**，而 **sink** 類型設為 **OracleSink**。</span><span class="sxs-lookup"><span data-stu-id="4b57b-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="4b57b-286">疑難排解秘訣</span><span class="sxs-lookup"><span data-stu-id="4b57b-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="4b57b-287">問題 1：.NET Framework Data Provider</span><span class="sxs-lookup"><span data-stu-id="4b57b-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="4b57b-288">您看到下列「錯誤訊息」：</span><span class="sxs-lookup"><span data-stu-id="4b57b-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="4b57b-289">**可能的原因：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-289">**Possible causes:**</span></span>

1. <span data-ttu-id="4b57b-290">未安裝 .NET Framework Data Provider for Oracle。</span><span class="sxs-lookup"><span data-stu-id="4b57b-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="4b57b-291">.NET Framework Data Provider for Oracle 已安裝於 .NET Framework 2.0，而且在 .NET Framework 4.0 資料夾中找不到。</span><span class="sxs-lookup"><span data-stu-id="4b57b-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="4b57b-292">**解析/因應措施：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="4b57b-293">如果您尚未安裝 .NET Provider for Oracle，請 [安裝它](http://www.oracle.com/technetwork/topics/dotnet/downloads/) ，然後重試此案例。</span><span class="sxs-lookup"><span data-stu-id="4b57b-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="4b57b-294">如果您即使在安裝提供者之後還是會收到錯誤訊息，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b57b-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="4b57b-295">從資料夾開啟 .NET 2.0 的電腦組態：<system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config。</span><span class="sxs-lookup"><span data-stu-id="4b57b-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="4b57b-296">搜尋 **Oracle Data Provider for .NET**，而您應該能夠在 **system.data** -> **DbProviderFactories** 下方，找到如下列範例所示的項目：“<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="4b57b-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="4b57b-297">」的作法指南。</span><span class="sxs-lookup"><span data-stu-id="4b57b-297">”</span></span>
3. <span data-ttu-id="4b57b-298">將此項目複製到下列 v4.0 資料夾中的 machine.config 檔案 : <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config，並將版本變更為 4.xxx.x.x。</span><span class="sxs-lookup"><span data-stu-id="4b57b-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="4b57b-299">執行 `gacutil /i [provider path]`，將 “<ODP.NET 安裝路徑>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” 安裝到全域組件快取 (GAC)。## 疑難排解祕訣</span><span class="sxs-lookup"><span data-stu-id="4b57b-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="4b57b-300">問題 2︰日期時間格式</span><span class="sxs-lookup"><span data-stu-id="4b57b-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="4b57b-301">您看到下列「錯誤訊息」：</span><span class="sxs-lookup"><span data-stu-id="4b57b-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="4b57b-302">**解析/因應措施：**</span><span class="sxs-lookup"><span data-stu-id="4b57b-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="4b57b-303">您可能需要根據 Oracle 資料庫中日期的設定方式，調整複製活動中的查詢字串，如下列範例 (使用 to_date 函式) 所示︰</span><span class="sxs-lookup"><span data-stu-id="4b57b-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="4b57b-304">Oracle 的類型對應</span><span class="sxs-lookup"><span data-stu-id="4b57b-304">Type mapping for Oracle</span></span>
<span data-ttu-id="4b57b-305">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會使用下列 2 個步驟的方法，執行自動類型轉換，將來源類型轉換成接收類型：</span><span class="sxs-lookup"><span data-stu-id="4b57b-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="4b57b-306">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="4b57b-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="4b57b-307">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="4b57b-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="4b57b-308">從 Oracle 移動資料時，會使用下列從 Oracle 資料類型到 .NET 類型的對應，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="4b57b-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="4b57b-309">Oracle 資料類型</span><span class="sxs-lookup"><span data-stu-id="4b57b-309">Oracle data type</span></span> | <span data-ttu-id="4b57b-310">.NET Framework 資料類型</span><span class="sxs-lookup"><span data-stu-id="4b57b-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="4b57b-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="4b57b-311">BFILE</span></span> |<span data-ttu-id="4b57b-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4b57b-312">Byte[]</span></span> |
| <span data-ttu-id="4b57b-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="4b57b-313">BLOB</span></span> |<span data-ttu-id="4b57b-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4b57b-314">Byte[]</span></span> |
| <span data-ttu-id="4b57b-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="4b57b-315">CHAR</span></span> |<span data-ttu-id="4b57b-316">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-316">String</span></span> |
| <span data-ttu-id="4b57b-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="4b57b-317">CLOB</span></span> |<span data-ttu-id="4b57b-318">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-318">String</span></span> |
| <span data-ttu-id="4b57b-319">日期</span><span class="sxs-lookup"><span data-stu-id="4b57b-319">DATE</span></span> |<span data-ttu-id="4b57b-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="4b57b-320">DateTime</span></span> |
| <span data-ttu-id="4b57b-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="4b57b-321">FLOAT</span></span> |<span data-ttu-id="4b57b-322">Decimal，字串 (如果精確度 > 28)</span><span class="sxs-lookup"><span data-stu-id="4b57b-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4b57b-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="4b57b-323">INTEGER</span></span> |<span data-ttu-id="4b57b-324">Decimal，字串 (如果精確度 > 28)</span><span class="sxs-lookup"><span data-stu-id="4b57b-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4b57b-325">間隔年至月</span><span class="sxs-lookup"><span data-stu-id="4b57b-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="4b57b-326">Int32</span><span class="sxs-lookup"><span data-stu-id="4b57b-326">Int32</span></span> |
| <span data-ttu-id="4b57b-327">間隔日至秒鐘</span><span class="sxs-lookup"><span data-stu-id="4b57b-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="4b57b-328">時間範圍</span><span class="sxs-lookup"><span data-stu-id="4b57b-328">TimeSpan</span></span> |
| <span data-ttu-id="4b57b-329">長</span><span class="sxs-lookup"><span data-stu-id="4b57b-329">LONG</span></span> |<span data-ttu-id="4b57b-330">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-330">String</span></span> |
| <span data-ttu-id="4b57b-331">長 RAW</span><span class="sxs-lookup"><span data-stu-id="4b57b-331">LONG RAW</span></span> |<span data-ttu-id="4b57b-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4b57b-332">Byte[]</span></span> |
| <span data-ttu-id="4b57b-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="4b57b-333">NCHAR</span></span> |<span data-ttu-id="4b57b-334">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-334">String</span></span> |
| <span data-ttu-id="4b57b-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="4b57b-335">NCLOB</span></span> |<span data-ttu-id="4b57b-336">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-336">String</span></span> |
| <span data-ttu-id="4b57b-337">數字</span><span class="sxs-lookup"><span data-stu-id="4b57b-337">NUMBER</span></span> |<span data-ttu-id="4b57b-338">Decimal，字串 (如果精確度 > 28)</span><span class="sxs-lookup"><span data-stu-id="4b57b-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="4b57b-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="4b57b-339">NVARCHAR2</span></span> |<span data-ttu-id="4b57b-340">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-340">String</span></span> |
| <span data-ttu-id="4b57b-341">RAW</span><span class="sxs-lookup"><span data-stu-id="4b57b-341">RAW</span></span> |<span data-ttu-id="4b57b-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="4b57b-342">Byte[]</span></span> |
| <span data-ttu-id="4b57b-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="4b57b-343">ROWID</span></span> |<span data-ttu-id="4b57b-344">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-344">String</span></span> |
| <span data-ttu-id="4b57b-345">時間戳記</span><span class="sxs-lookup"><span data-stu-id="4b57b-345">TIMESTAMP</span></span> |<span data-ttu-id="4b57b-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="4b57b-346">DateTime</span></span> |
| <span data-ttu-id="4b57b-347">本地時區的時間戳記</span><span class="sxs-lookup"><span data-stu-id="4b57b-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="4b57b-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="4b57b-348">DateTime</span></span> |
| <span data-ttu-id="4b57b-349">時區的時間戳記</span><span class="sxs-lookup"><span data-stu-id="4b57b-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="4b57b-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="4b57b-350">DateTime</span></span> |
| <span data-ttu-id="4b57b-351">不帶正負號的整數</span><span class="sxs-lookup"><span data-stu-id="4b57b-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="4b57b-352">數字</span><span class="sxs-lookup"><span data-stu-id="4b57b-352">Number</span></span> |
| <span data-ttu-id="4b57b-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="4b57b-353">VARCHAR2</span></span> |<span data-ttu-id="4b57b-354">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-354">String</span></span> |
| <span data-ttu-id="4b57b-355">XML</span><span class="sxs-lookup"><span data-stu-id="4b57b-355">XML</span></span> |<span data-ttu-id="4b57b-356">String</span><span class="sxs-lookup"><span data-stu-id="4b57b-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="4b57b-357">使用 Microsoft 驅動程式時，不支援資料類型 **INTERVAL YEAR TO MONTH** 和 **INTERVAL DAY TO SECOND**。</span><span class="sxs-lookup"><span data-stu-id="4b57b-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="4b57b-358">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="4b57b-358">Map source to sink columns</span></span>
<span data-ttu-id="4b57b-359">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="4b57b-360">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="4b57b-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="4b57b-361">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="4b57b-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="4b57b-362">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="4b57b-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="4b57b-363">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="4b57b-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="4b57b-364">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="4b57b-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="4b57b-365">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="4b57b-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4b57b-366">效能和微調</span><span class="sxs-lookup"><span data-stu-id="4b57b-366">Performance and Tuning</span></span>
<span data-ttu-id="4b57b-367">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="4b57b-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
