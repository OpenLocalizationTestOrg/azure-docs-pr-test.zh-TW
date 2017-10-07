---
title: "aaaCopy 資料，從檔案系統，使用 Azure Data Factory |Microsoft 文件"
description: "深入了解如何從內部部署檔案系統使用 Azure Data Factory toocopy 資料 tooand。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="004a4-103">從內部部署檔案系統複製資料 tooand，使用 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="004a4-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="004a4-104">本文說明如何 toouse hello Azure Data Factory toocopy 資料從內部部署檔案系統中的複製活動。</span><span class="sxs-lookup"><span data-stu-id="004a4-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="004a4-105">它是在 hello 基礎[資料移動活動](data-factory-data-movement-activities.md)文件： hello 複製活動會提供資料移動的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="004a4-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="004a4-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="004a4-106">Supported scenarios</span></span>
<span data-ttu-id="004a4-107">您可以將資料複製**從內部部署檔案系統**toohello 下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="004a4-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="004a4-108">您可以將資料複製下列資料存放區的 hello **tooan 內部檔案系統**:</span><span class="sxs-lookup"><span data-stu-id="004a4-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="004a4-109">複製活動不會刪除 hello 原始程式檔之後順利複製的 toohello 目的地。</span><span class="sxs-lookup"><span data-stu-id="004a4-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="004a4-110">如果您需要 toodelete hello 原始程式檔複製成功之後，建立自訂活動 toodelete hello 檔案，並使用 hello 管線中的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="004a4-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="004a4-111">啟用連線</span><span class="sxs-lookup"><span data-stu-id="004a4-111">Enabling connectivity</span></span>
<span data-ttu-id="004a4-112">Data Factory 支援透過在內部部署檔案系統中的連接 tooand**資料管理閘道器**。</span><span class="sxs-lookup"><span data-stu-id="004a4-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="004a4-113">您必須安裝 hello 資料管理閘道器在內部部署環境的 hello Data Factory 服務 tooconnect tooany 支援在內部部署資料存放區包括檔案系統中。</span><span class="sxs-lookup"><span data-stu-id="004a4-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="004a4-114">請參閱 toolearn 有關資料管理閘道器以及如需 hello 閘道設定的逐步指示[在內部部署來源和資料管理閘道與 hello 雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="004a4-115">資料管理閘道器，除了其他二進位檔案需要安裝 toobe toocommunicate tooand 從內部部署檔案系統。</span><span class="sxs-lookup"><span data-stu-id="004a4-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="004a4-116">您必須安裝並使用 hello 資料管理閘道，即使是在 Azure IaaS VM 的 hello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="004a4-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="004a4-117">如需 hello 閘道的詳細資訊，請參閱[資料管理閘道器](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="004a4-118">安裝 Linux 檔案共用，toouse [Samba](https://www.samba.org/) Linux 伺服器和 Windows server 上的安裝資料管理閘道器上。</span><span class="sxs-lookup"><span data-stu-id="004a4-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="004a4-119">不支援在 Linux 伺服器上安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="004a4-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="004a4-120">開始使用</span><span class="sxs-lookup"><span data-stu-id="004a4-120">Getting started</span></span>
<span data-ttu-id="004a4-121">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出檔案系統。</span><span class="sxs-lookup"><span data-stu-id="004a4-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="004a4-122">最簡單方式 toocreate hello 管線為 toouse hello**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="004a4-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="004a4-123">請參閱[教學課程： 建立管線，使用複製精靈](data-factory-copy-data-wizard-tutorial.md)快速逐步解說中建立管線中使用 hello 複製資料精靈 」。</span><span class="sxs-lookup"><span data-stu-id="004a4-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="004a4-124">您也可以使用下列工具 toocreate 管線 hello: **Azure 入口網站**， **Visual Studio**， **Azure PowerShell**， **Azure Resource Manager 範本**， **.NET API**，和**REST API**。</span><span class="sxs-lookup"><span data-stu-id="004a4-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="004a4-125">請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)的逐步指示 toocreate 具有複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="004a4-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="004a4-126">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="004a4-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="004a4-127">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="004a4-127">Create a **data factory**.</span></span> <span data-ttu-id="004a4-128">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="004a4-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="004a4-129">建立**連結的服務**toolink 輸入和輸出資料存放區 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="004a4-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="004a4-130">例如，如果您從 Azure blob 儲存體 tooan 在內部部署檔案系統複製資料，您建立兩個連結的服務 toolink 在內部部署檔案系統與 Azure 儲存體帳戶 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="004a4-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="004a4-131">對於特定 tooan 在內部部署檔案系統連結的服務屬性，請參閱[連結服務屬性](#linked-service-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="004a4-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="004a4-132">建立**資料集**toorepresent 輸入和輸出 hello 的資料複製作業。</span><span class="sxs-lookup"><span data-stu-id="004a4-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="004a4-133">在 hello hello 最後一個步驟中所述的範例中，您可以建立資料集 toospecify hello blob 容器和包含 hello 輸入的資料的資料夾。</span><span class="sxs-lookup"><span data-stu-id="004a4-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="004a4-134">此外，您會建立另一個資料集 toospecify hello 資料夾和檔案名稱 （選擇性） 在檔案系統。</span><span class="sxs-lookup"><span data-stu-id="004a4-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="004a4-135">為特定 tooon 內部的資料集屬性的檔案系統，請參閱[資料集屬性](#dataset-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="004a4-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="004a4-136">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="004a4-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="004a4-137">在先前所述 hello 範例中，您使用 BlobSource 作為來源和使用 FileSystemSink 做為接收器 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="004a4-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="004a4-138">同樣地，如果您要從內部部署檔案系統 tooAzure Blob 儲存體複製，則使用 FileSystemSource 和 BlobSink 的 hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="004a4-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="004a4-139">複製活動內容特定 tooon 內部檔案系統，請參閱[複製活動屬性](#copy-activity-properties)> 一節。</span><span class="sxs-lookup"><span data-stu-id="004a4-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="004a4-140">如需如何 toouse 的資料存放區做為來源或接收的詳細資訊，按一下 hello hello 資料存放區上一節中的連結。</span><span class="sxs-lookup"><span data-stu-id="004a4-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="004a4-141">當您使用 hello 精靈時，會自動為您建立這些 Data Factory 實體 （連結的服務、 資料集和 hello 管線） 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="004a4-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="004a4-142">當您使用 [工具/Api （除了.NET 應用程式開發介面） 時，您會定義這些 Data Factory 實體使用 hello JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="004a4-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="004a4-143">如需使用的 toocopy 資料，從檔案系統的 Data Factory 實體的 JSON 定義的範例，請參閱[JSON 範例](#json-examples-for-copying-data-to-and-from-file-system)本文一節。</span><span class="sxs-lookup"><span data-stu-id="004a4-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="004a4-144">hello 下列各節提供有關使用的 toodefine Data Factory 實體特定 toofile 系統的 JSON 屬性的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="004a4-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="004a4-145">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="004a4-145">Linked service properties</span></span>
<span data-ttu-id="004a4-146">您可以連結在內部部署檔案系統 tooan Azure data factory 以 hello**在內部部署檔案伺服器**連結服務。</span><span class="sxs-lookup"><span data-stu-id="004a4-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="004a4-147">hello 下表提供說明屬於特定 toohello 連結在內部部署檔案伺服器服務的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="004a4-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="004a4-148">屬性</span><span class="sxs-lookup"><span data-stu-id="004a4-148">Property</span></span> | <span data-ttu-id="004a4-149">說明</span><span class="sxs-lookup"><span data-stu-id="004a4-149">Description</span></span> | <span data-ttu-id="004a4-150">必要</span><span class="sxs-lookup"><span data-stu-id="004a4-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="004a4-151">類型</span><span class="sxs-lookup"><span data-stu-id="004a4-151">type</span></span> |<span data-ttu-id="004a4-152">請確定 hello type 屬性設定太**OnPremisesFileServer**。</span><span class="sxs-lookup"><span data-stu-id="004a4-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="004a4-153">是</span><span class="sxs-lookup"><span data-stu-id="004a4-153">Yes</span></span> |
| <span data-ttu-id="004a4-154">主機</span><span class="sxs-lookup"><span data-stu-id="004a4-154">host</span></span> |<span data-ttu-id="004a4-155">指定您想 toocopy hello 資料夾 hello 根路徑。</span><span class="sxs-lookup"><span data-stu-id="004a4-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="004a4-156">使用 hello 逸出字元 '\' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="004a4-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="004a4-157">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="004a4-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="004a4-158">是</span><span class="sxs-lookup"><span data-stu-id="004a4-158">Yes</span></span> |
| <span data-ttu-id="004a4-159">userid</span><span class="sxs-lookup"><span data-stu-id="004a4-159">userid</span></span> |<span data-ttu-id="004a4-160">指定具有存取 toohello 伺服器 hello 使用者識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="004a4-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="004a4-161">否 (如果您選擇 encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="004a4-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="004a4-162">password</span><span class="sxs-lookup"><span data-stu-id="004a4-162">password</span></span> |<span data-ttu-id="004a4-163">指定 hello hello 使用者 (userid) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="004a4-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="004a4-164">否 (如果您選擇 encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="004a4-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="004a4-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="004a4-165">encryptedCredential</span></span> |<span data-ttu-id="004a4-166">指定您可以藉由執行 hello 新增 AzureRmDataFactoryEncryptValue cmdlet 取得的 hello 加密認證。</span><span class="sxs-lookup"><span data-stu-id="004a4-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="004a4-167">否 （如果您選擇 toospecify 使用者識別碼和密碼以純文字）</span><span class="sxs-lookup"><span data-stu-id="004a4-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="004a4-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="004a4-168">gatewayName</span></span> |<span data-ttu-id="004a4-169">指定 hello hello 閘道的 Data Factory 應該使用 tooconnect toohello 在內部部署檔案伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="004a4-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="004a4-170">是</span><span class="sxs-lookup"><span data-stu-id="004a4-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="004a4-171">範例連結服務和資料集定義</span><span class="sxs-lookup"><span data-stu-id="004a4-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="004a4-172">案例</span><span class="sxs-lookup"><span data-stu-id="004a4-172">Scenario</span></span> | <span data-ttu-id="004a4-173">連結服務定義中的主機</span><span class="sxs-lookup"><span data-stu-id="004a4-173">Host in linked service definition</span></span> | <span data-ttu-id="004a4-174">資料集定義中的 folderPath</span><span class="sxs-lookup"><span data-stu-id="004a4-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="004a4-175">資料管理閘道電腦上的本機資料夾︰</span><span class="sxs-lookup"><span data-stu-id="004a4-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="004a4-176">範例：D:\\\* 或 D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="004a4-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="004a4-177">D:\\\\ (適用於資料管理閘道 2.0 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="004a4-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="004a4-178">localhost (適用於比資料管理閘道 2.0 更早的版本)</span><span class="sxs-lookup"><span data-stu-id="004a4-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="004a4-179">.\\\\ 或 folder\\\\subfolder (適用於資料管理閘道 2.0 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="004a4-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="004a4-180">D:\\\\ 或 D:\\\\folder\\\\subfolder (適用低於閘道 2.0 的版本)</span><span class="sxs-lookup"><span data-stu-id="004a4-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="004a4-181">遠端共用資料夾︰</span><span class="sxs-lookup"><span data-stu-id="004a4-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="004a4-182">範例︰\\\\myserver\\share\\\* 或 \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="004a4-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="004a4-183">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="004a4-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="004a4-184">.\\\\ 或 folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="004a4-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="004a4-185">範例：使用純文字的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="004a4-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="004a4-186">範例：使用 encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="004a4-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="004a4-187">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="004a4-187">Dataset properties</span></span>
<span data-ttu-id="004a4-188">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="004a4-189">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="004a4-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="004a4-190">hello typeProperties 區段是不同的資料集的每個型別。</span><span class="sxs-lookup"><span data-stu-id="004a4-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="004a4-191">它提供資訊，例如 hello 位置和 hello 資料存放區中的 hello 資料格式。</span><span class="sxs-lookup"><span data-stu-id="004a4-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="004a4-192">hello typeProperties 區段 hello 資料集型別的**FileShare**具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="004a4-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="004a4-193">屬性</span><span class="sxs-lookup"><span data-stu-id="004a4-193">Property</span></span> | <span data-ttu-id="004a4-194">說明</span><span class="sxs-lookup"><span data-stu-id="004a4-194">Description</span></span> | <span data-ttu-id="004a4-195">必要</span><span class="sxs-lookup"><span data-stu-id="004a4-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="004a4-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="004a4-196">folderPath</span></span> |<span data-ttu-id="004a4-197">指定 hello 子路徑 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="004a4-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="004a4-198">使用 hello 逸出字元 ' \' hello 字串中的特殊字元。</span><span class="sxs-lookup"><span data-stu-id="004a4-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="004a4-199">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="004a4-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="004a4-200">您可以結合此屬性與**partitionBy** toohave 資料夾路徑根據配量開始/結束日期時間。</span><span class="sxs-lookup"><span data-stu-id="004a4-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="004a4-201">是</span><span class="sxs-lookup"><span data-stu-id="004a4-201">Yes</span></span> |
| <span data-ttu-id="004a4-202">fileName</span><span class="sxs-lookup"><span data-stu-id="004a4-202">fileName</span></span> |<span data-ttu-id="004a4-203">在 [hello 指定 hello hello 檔案名稱**folderPath**如果您想 hello 資料表 toorefer tooa 特定檔案 hello 資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="004a4-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="004a4-204">如果您未指定任何值，這個屬性，hello 資料表會指向 tooall hello 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="004a4-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="004a4-205">當**fileName**未指定輸出資料集和**preserveHierarchy**中未指定活動接收 hello hello 產生檔案名稱是以下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="004a4-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="004a4-206">`Data.<Guid>.txt` (例如： Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="004a4-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="004a4-207">否</span><span class="sxs-lookup"><span data-stu-id="004a4-207">No</span></span> |
| <span data-ttu-id="004a4-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="004a4-208">fileFilter</span></span> |<span data-ttu-id="004a4-209">指定篩選 toobe 使用 tooselect hello folderPath 中檔案的子集，而不是所有的檔案。</span><span class="sxs-lookup"><span data-stu-id="004a4-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="004a4-210">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="004a4-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="004a4-211">範例 1："fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="004a4-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="004a4-212">範例 2："fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="004a4-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="004a4-213">請注意，fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="004a4-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="004a4-214">否</span><span class="sxs-lookup"><span data-stu-id="004a4-214">No</span></span> |
| <span data-ttu-id="004a4-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="004a4-215">partitionedBy</span></span> |<span data-ttu-id="004a4-216">您可以使用 partitionedBy toospecify 動態 folderPath/檔名，時間序列資料。</span><span class="sxs-lookup"><span data-stu-id="004a4-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="004a4-217">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="004a4-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="004a4-218">否</span><span class="sxs-lookup"><span data-stu-id="004a4-218">No</span></span> |
| <span data-ttu-id="004a4-219">format</span><span class="sxs-lookup"><span data-stu-id="004a4-219">format</span></span> | <span data-ttu-id="004a4-220">支援下列格式類型的 hello: **TextFormat**， **JsonFormat**， **AvroFormat**， **OrcFormat**， **ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="004a4-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="004a4-221">設定 hello**類型**下格式 tooone 這些值的屬性。</span><span class="sxs-lookup"><span data-stu-id="004a4-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="004a4-222">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="004a4-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="004a4-223">如果您想太**複製檔做為-是**之間以檔案為基礎存放區 （二進位複製），略過這兩個輸入和輸出資料集定義中的 hello 格式 > 一節。</span><span class="sxs-lookup"><span data-stu-id="004a4-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="004a4-224">否</span><span class="sxs-lookup"><span data-stu-id="004a4-224">No</span></span> |
| <span data-ttu-id="004a4-225">compression</span><span class="sxs-lookup"><span data-stu-id="004a4-225">compression</span></span> | <span data-ttu-id="004a4-226">指定 hello 類型和層級的 hello 資料壓縮。</span><span class="sxs-lookup"><span data-stu-id="004a4-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="004a4-227">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="004a4-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="004a4-228">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="004a4-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="004a4-229">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="004a4-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="004a4-230">否</span><span class="sxs-lookup"><span data-stu-id="004a4-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="004a4-231">無法同時使用 fileName 和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="004a4-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="004a4-232">使用 partitionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="004a4-232">Using partitionedBy property</span></span>
<span data-ttu-id="004a4-233">當 hello 上一節中所述，您可指定動態 folderPath 和 filename 時間序列資料的 hello **partitionedBy**屬性， [Data Factory 函數與 hello 系統變數](data-factory-functions-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="004a4-234">toounderstand 更多詳細資料，在時間序列資料集、 排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)，[排程與執行](data-factory-scheduling-and-execution.md)，和[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="004a4-235">範例 1：</span><span class="sxs-lookup"><span data-stu-id="004a4-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="004a4-236">在此範例中，hello hello Data Factory 系統變數 SliceStart hello 格式 (YYYYMMDDHH) 值會取代 {Slice}。</span><span class="sxs-lookup"><span data-stu-id="004a4-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="004a4-237">SliceStart 是指配 toostart hello 配量時間。</span><span class="sxs-lookup"><span data-stu-id="004a4-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="004a4-238">hello folderPath 是不同的每個配量。</span><span class="sxs-lookup"><span data-stu-id="004a4-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="004a4-239">例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。</span><span class="sxs-lookup"><span data-stu-id="004a4-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="004a4-240">範例 2：</span><span class="sxs-lookup"><span data-stu-id="004a4-240">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="004a4-241">在此範例中，年、 月、 日和時間的 SliceStart 會擷取到個別 hello folderPath 和 fileName 屬性所使用的變數。</span><span class="sxs-lookup"><span data-stu-id="004a4-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="004a4-242">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="004a4-242">Copy activity properties</span></span>
<span data-ttu-id="004a4-243">區段和屬性可用來定義活動的完整清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="004a4-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="004a4-244">屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="004a4-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="004a4-245">而 hello 中可用屬性**typeProperties** hello 活動的區段會隨每個活動類型。</span><span class="sxs-lookup"><span data-stu-id="004a4-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="004a4-246">複製活動它們而異的來源與接收的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="004a4-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="004a4-247">如果您要從內部部署檔案系統中移動資料，您設定 hello 來源類型 hello 複製活動中太**FileSystemSource**。</span><span class="sxs-lookup"><span data-stu-id="004a4-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="004a4-248">同樣地，如果您要移動資料 tooan 在內部部署檔案系統，hello 接收器類型中設定 hello 複製活動太**使用 FileSystemSink**。</span><span class="sxs-lookup"><span data-stu-id="004a4-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="004a4-249">本節提供 FileSystemSource 和 FileSystemSink 所支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="004a4-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="004a4-250">**FileSystemSource**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="004a4-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="004a4-251">屬性</span><span class="sxs-lookup"><span data-stu-id="004a4-251">Property</span></span> | <span data-ttu-id="004a4-252">說明</span><span class="sxs-lookup"><span data-stu-id="004a4-252">Description</span></span> | <span data-ttu-id="004a4-253">允許的值</span><span class="sxs-lookup"><span data-stu-id="004a4-253">Allowed values</span></span> | <span data-ttu-id="004a4-254">必要</span><span class="sxs-lookup"><span data-stu-id="004a4-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="004a4-255">遞迴</span><span class="sxs-lookup"><span data-stu-id="004a4-255">recursive</span></span> |<span data-ttu-id="004a4-256">指出是否 hello 讀取資料以遞迴方式從 hello 子資料夾，或只能從 hello 指定的資料夾。</span><span class="sxs-lookup"><span data-stu-id="004a4-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="004a4-257">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="004a4-257">True, False (default)</span></span> |<span data-ttu-id="004a4-258">否</span><span class="sxs-lookup"><span data-stu-id="004a4-258">No</span></span> |

<span data-ttu-id="004a4-259">**使用 FileSystemSink**支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="004a4-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="004a4-260">屬性</span><span class="sxs-lookup"><span data-stu-id="004a4-260">Property</span></span> | <span data-ttu-id="004a4-261">說明</span><span class="sxs-lookup"><span data-stu-id="004a4-261">Description</span></span> | <span data-ttu-id="004a4-262">允許的值</span><span class="sxs-lookup"><span data-stu-id="004a4-262">Allowed values</span></span> | <span data-ttu-id="004a4-263">必要</span><span class="sxs-lookup"><span data-stu-id="004a4-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="004a4-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="004a4-264">copyBehavior</span></span> |<span data-ttu-id="004a4-265">Hello 來源 BlobSource 或檔案系統時，請定義 hello 複製行為。</span><span class="sxs-lookup"><span data-stu-id="004a4-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="004a4-266">**PreserveHierarchy:**保留 hello hello 目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="004a4-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="004a4-267">也就是說，hello hello 來源檔案 toohello 來源資料夾的相對路徑是 hello 與 hello 相對路徑的 hello 目標檔案 toohello 目標資料夾相同。</span><span class="sxs-lookup"><span data-stu-id="004a4-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="004a4-268">**FlattenHierarchy:** hello 第一個層級的目標資料夾中建立 hello 來源資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="004a4-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="004a4-269">會使用自動產生名稱建立 hello 目標檔案。</span><span class="sxs-lookup"><span data-stu-id="004a4-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="004a4-270">**MergeFiles:**合併 hello 來源資料夾 tooone 檔案中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="004a4-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="004a4-271">如果指定 hello 檔案名稱/blob 名稱，則 hello 合併的檔案名稱是 hello 指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="004a4-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="004a4-272">否則，就會是自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="004a4-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="004a4-273">否</span><span class="sxs-lookup"><span data-stu-id="004a4-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="004a4-274">遞迴和 copyBehavior 範例</span><span class="sxs-lookup"><span data-stu-id="004a4-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="004a4-275">本章節描述 hello 產生不同的值為 hello 遞迴和 copyBehavior 屬性組合的 hello 複製作業的行為。</span><span class="sxs-lookup"><span data-stu-id="004a4-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="004a4-276">recursive 值</span><span class="sxs-lookup"><span data-stu-id="004a4-276">recursive value</span></span> | <span data-ttu-id="004a4-277">copyBehavior 值</span><span class="sxs-lookup"><span data-stu-id="004a4-277">copyBehavior value</span></span> | <span data-ttu-id="004a4-278">產生的行為</span><span class="sxs-lookup"><span data-stu-id="004a4-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="004a4-279">true</span><span class="sxs-lookup"><span data-stu-id="004a4-279">true</span></span> |<span data-ttu-id="004a4-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="004a4-280">preserveHierarchy</span></span> |<span data-ttu-id="004a4-281">來源資料夾 Folder1 以 hello 下列結構，</span><span class="sxs-lookup"><span data-stu-id="004a4-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="004a4-282">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-282">Folder1</span></span><br/><span data-ttu-id="004a4-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="004a4-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="004a4-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="004a4-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="004a4-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="004a4-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="004a4-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="004a4-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="004a4-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="004a4-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="004a4-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="004a4-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="004a4-289">建立 hello 目標資料夾 Folder1 hello 相同結構為 hello 來源：</span><span class="sxs-lookup"><span data-stu-id="004a4-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="004a4-290">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-290">Folder1</span></span><br/><span data-ttu-id="004a4-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="004a4-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="004a4-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="004a4-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="004a4-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="004a4-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="004a4-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="004a4-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="004a4-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="004a4-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="004a4-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="004a4-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="004a4-297">true</span><span class="sxs-lookup"><span data-stu-id="004a4-297">true</span></span> |<span data-ttu-id="004a4-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="004a4-298">flattenHierarchy</span></span> |<span data-ttu-id="004a4-299">來源資料夾 Folder1 以 hello 下列結構，</span><span class="sxs-lookup"><span data-stu-id="004a4-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="004a4-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-300">Folder1</span></span><br/><span data-ttu-id="004a4-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="004a4-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="004a4-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="004a4-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="004a4-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="004a4-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="004a4-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="004a4-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="004a4-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="004a4-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="004a4-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="004a4-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="004a4-307">使用下列結構的 hello 建立 hello 目標 Folder1:</span><span class="sxs-lookup"><span data-stu-id="004a4-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="004a4-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-308">Folder1</span></span><br/><span data-ttu-id="004a4-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="004a4-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="004a4-310">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="004a4-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="004a4-311">&nbsp;&nbsp;&nbsp;&nbsp;File3 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="004a4-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="004a4-312">&nbsp;&nbsp;&nbsp;&nbsp;File4 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="004a4-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="004a4-313">&nbsp;&nbsp;&nbsp;&nbsp;File5 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="004a4-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="004a4-314">true</span><span class="sxs-lookup"><span data-stu-id="004a4-314">true</span></span> |<span data-ttu-id="004a4-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="004a4-315">mergeFiles</span></span> |<span data-ttu-id="004a4-316">來源資料夾 Folder1 以 hello 下列結構，</span><span class="sxs-lookup"><span data-stu-id="004a4-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="004a4-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-317">Folder1</span></span><br/><span data-ttu-id="004a4-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="004a4-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="004a4-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="004a4-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="004a4-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="004a4-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="004a4-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="004a4-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="004a4-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="004a4-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="004a4-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="004a4-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="004a4-324">使用下列結構的 hello 建立 hello 目標 Folder1:</span><span class="sxs-lookup"><span data-stu-id="004a4-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="004a4-325">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-325">Folder1</span></span><br/><span data-ttu-id="004a4-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 的內容會合併成一個檔案，並有自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="004a4-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="004a4-327">false</span><span class="sxs-lookup"><span data-stu-id="004a4-327">false</span></span> |<span data-ttu-id="004a4-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="004a4-328">preserveHierarchy</span></span> |<span data-ttu-id="004a4-329">來源資料夾 Folder1 以 hello 下列結構，</span><span class="sxs-lookup"><span data-stu-id="004a4-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="004a4-330">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-330">Folder1</span></span><br/><span data-ttu-id="004a4-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="004a4-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="004a4-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="004a4-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="004a4-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="004a4-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="004a4-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="004a4-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="004a4-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="004a4-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="004a4-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="004a4-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="004a4-337">使用下列結構的 hello 建立 hello 目標資料夾 Folder1:</span><span class="sxs-lookup"><span data-stu-id="004a4-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="004a4-338">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-338">Folder1</span></span><br/><span data-ttu-id="004a4-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="004a4-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="004a4-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="004a4-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="004a4-341">系統不會挑選含有 File3、File4、File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="004a4-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="004a4-342">false</span><span class="sxs-lookup"><span data-stu-id="004a4-342">false</span></span> |<span data-ttu-id="004a4-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="004a4-343">flattenHierarchy</span></span> |<span data-ttu-id="004a4-344">來源資料夾 Folder1 以 hello 下列結構，</span><span class="sxs-lookup"><span data-stu-id="004a4-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="004a4-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-345">Folder1</span></span><br/><span data-ttu-id="004a4-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="004a4-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="004a4-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="004a4-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="004a4-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="004a4-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="004a4-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="004a4-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="004a4-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="004a4-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="004a4-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="004a4-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="004a4-352">使用下列結構的 hello 建立 hello 目標資料夾 Folder1:</span><span class="sxs-lookup"><span data-stu-id="004a4-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="004a4-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-353">Folder1</span></span><br/><span data-ttu-id="004a4-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="004a4-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="004a4-355">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="004a4-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="004a4-356">系統不會挑選含有 File3、File4、File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="004a4-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="004a4-357">false</span><span class="sxs-lookup"><span data-stu-id="004a4-357">false</span></span> |<span data-ttu-id="004a4-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="004a4-358">mergeFiles</span></span> |<span data-ttu-id="004a4-359">來源資料夾 Folder1 以 hello 下列結構，</span><span class="sxs-lookup"><span data-stu-id="004a4-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="004a4-360">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-360">Folder1</span></span><br/><span data-ttu-id="004a4-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="004a4-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="004a4-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="004a4-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="004a4-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="004a4-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="004a4-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="004a4-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="004a4-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="004a4-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="004a4-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="004a4-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="004a4-367">使用下列結構的 hello 建立 hello 目標資料夾 Folder1:</span><span class="sxs-lookup"><span data-stu-id="004a4-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="004a4-368">Folder1</span><span class="sxs-lookup"><span data-stu-id="004a4-368">Folder1</span></span><br/><span data-ttu-id="004a4-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 的內容會合併成一個檔案，並有自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="004a4-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="004a4-370">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="004a4-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="004a4-371">系統不會挑選含有 File3、File4、File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="004a4-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="004a4-372">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="004a4-372">Supported file and compression formats</span></span>
<span data-ttu-id="004a4-373">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="004a4-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="004a4-374">從檔案系統複製資料 tooand JSON 範例</span><span class="sxs-lookup"><span data-stu-id="004a4-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="004a4-375">hello 下列範例會提供範例 JSON 定義，您可以使用 toocreate 管線使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="004a4-376">它們會顯示如何從內部部署檔案系統和 Azure Blob 儲存體 toocopy 資料 tooand。</span><span class="sxs-lookup"><span data-stu-id="004a4-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="004a4-377">不過，您可以將資料複製*直接*從 hello 來源 tooany hello 接收中列出的任一[支援來源與接收](data-factory-data-movement-activities.md#supported-data-stores-and-formats)Azure Data Factory 中使用複製活動。</span><span class="sxs-lookup"><span data-stu-id="004a4-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="004a4-378">範例： 將資料從內部部署檔案系統 tooAzure Blob 儲存體複製</span><span class="sxs-lookup"><span data-stu-id="004a4-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="004a4-379">這個範例示範如何從內部部署檔案系統 tooAzure Blob 儲存體 toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="004a4-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="004a4-380">hello 範例有下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="004a4-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="004a4-381">[OnPremisesFileServer](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="004a4-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="004a4-382">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="004a4-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="004a4-383">[FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="004a4-384">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="004a4-385">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="004a4-386">下列範例中的 hello 複製時間序列資料從內部部署檔案系統 tooAzure Blob 儲存體每小時。</span><span class="sxs-lookup"><span data-stu-id="004a4-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="004a4-387">這些範例中所使用的 hello JSON 屬性 hello 各節所述之後 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="004a4-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="004a4-388">第一個步驟中，設定資料管理閘道器中的 hello 指示根據[在內部部署來源和資料管理閘道與 hello 雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="004a4-389">**內部部署檔案伺服器連結服務：**</span><span class="sxs-lookup"><span data-stu-id="004a4-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="004a4-390">我們建議您使用 hello **encryptedCredential**屬性改為 hello **userid**和**密碼**屬性。</span><span class="sxs-lookup"><span data-stu-id="004a4-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="004a4-391">如需此連結服務的詳細資訊，請參閱[檔案系統連結服務](#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="004a4-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="004a4-392">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="004a4-392">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="004a4-393">**內部部署檔案系統輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="004a4-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="004a4-394">每小時從新的檔案挑選資料。</span><span class="sxs-lookup"><span data-stu-id="004a4-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="004a4-395">hello folderPath 和 fileName 屬性由決定依據 hello hello 配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="004a4-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="004a4-396">設定`"external": "true"`該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="004a4-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
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

<span data-ttu-id="004a4-397">**Azure Blob 儲存體資料集：**</span><span class="sxs-lookup"><span data-stu-id="004a4-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="004a4-398">資料會寫入 tooa 新 blob 的每個小時 (頻率： 小時、 interval: 1)。</span><span class="sxs-lookup"><span data-stu-id="004a4-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="004a4-399">hello blob 的 hello 資料夾路徑會動態評估 hello 正在處理的 hello 配量的開始時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="004a4-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="004a4-400">hello 資料夾路徑會使用 hello 的 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="004a4-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="004a4-401">**具有檔案系統來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="004a4-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="004a4-402">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="004a4-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="004a4-403">在 hello 管線 JSON 定義中，hello**來源**類型設定得**FileSystemSource**，和**接收**類型設定得**BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="004a4-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="004a4-404">範例： 將資料從 Azure SQL Database tooan 在內部部署檔案系統複製</span><span class="sxs-lookup"><span data-stu-id="004a4-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="004a4-405">下列範例會示範 hello:</span><span class="sxs-lookup"><span data-stu-id="004a4-405">hello following sample shows:</span></span>

* <span data-ttu-id="004a4-406">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 類型的已連結服務。</span><span class="sxs-lookup"><span data-stu-id="004a4-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="004a4-407">[OnPremisesFileServer](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="004a4-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="004a4-408">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="004a4-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="004a4-409">[FileShare](#dataset-properties) 類型的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="004a4-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="004a4-410">具有使用 [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) 和 [FileSystemSink](#copy-activity-properties) 之複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="004a4-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="004a4-411">hello 範例將時間序列資料從 Azure SQL 資料表 tooan 在內部部署檔案系統每小時。</span><span class="sxs-lookup"><span data-stu-id="004a4-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="004a4-412">這些範例中所使用的 hello JSON 屬性各節所述之後 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="004a4-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="004a4-413">**Azure SQL Database 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="004a4-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="004a4-414">**內部部署檔案伺服器連結服務：**</span><span class="sxs-lookup"><span data-stu-id="004a4-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="004a4-415">我們建議您使用 hello **encryptedCredential**屬性，而不要使用 hello **userid**和**密碼**屬性。</span><span class="sxs-lookup"><span data-stu-id="004a4-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="004a4-416">如需此連結服務的詳細資訊，請參閱[檔案系統連結服務](#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="004a4-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="004a4-417">**Azure SQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="004a4-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="004a4-418">hello 範例假設您已建立資料表"MyTable"Azure SQL 中和它包含稱為"timestampcolumn 「 時間序列資料的資料行。</span><span class="sxs-lookup"><span data-stu-id="004a4-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="004a4-419">設定``“external”: ”true”``該 hello 集外部 toohello 資料處理站，且不產生 hello data factory 中的活動時，會通知 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="004a4-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
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

<span data-ttu-id="004a4-420">**內部部署檔案系統輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="004a4-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="004a4-421">資料是每小時的複製的 tooa 新檔案。</span><span class="sxs-lookup"><span data-stu-id="004a4-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="004a4-422">hello folderPath 和 fileName hello blob 決定依據 hello hello 配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="004a4-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
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

<span data-ttu-id="004a4-423">**具有 SQL 來源和檔案系統接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="004a4-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="004a4-424">hello 管線包含設定的 toouse 複製活動 hello 輸入和輸出資料集，並為排程的 toorun 每個小時。</span><span class="sxs-lookup"><span data-stu-id="004a4-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="004a4-425">在 hello 管線 JSON 定義中，hello**來源**類型設定得**SqlSource**，和 hello**接收**類型設定得**使用 FileSystemSink**。</span><span class="sxs-lookup"><span data-stu-id="004a4-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="004a4-426">hello SQL 查詢，以指定的 hello **SqlReaderQuery**屬性選取 hello 資料在過去小時 toocopy hello。</span><span class="sxs-lookup"><span data-stu-id="004a4-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="004a4-427">您也可以將對應從來源資料集 toocolumns 接收 hello 複製活動定義中的資料集的資料行。</span><span class="sxs-lookup"><span data-stu-id="004a4-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="004a4-428">如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="004a4-429">效能和微調</span><span class="sxs-lookup"><span data-stu-id="004a4-429">Performance and tuning</span></span>
 <span data-ttu-id="004a4-430">關於金鑰 toolearn 因素影響 hello 效能的 Azure Data Factory 和各種方式 toooptimize 中的資料移動 （複製活動），請參閱 hello[複製活動效能及微調指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="004a4-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
