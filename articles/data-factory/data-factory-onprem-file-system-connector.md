---
title: "使用 Azure Data Factory 從檔案系統來回複製資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從內部部署檔案系統來回複製資料。"
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
ms.openlocfilehash: 52305e54f539de6aba2ba9cc856a09e04d608ded
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="0d3d1-103">使用 Azure Data Factory 從內部部署檔案系統來回複製資料</span><span class="sxs-lookup"><span data-stu-id="0d3d1-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="0d3d1-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署檔案系統來回複製資料。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-104">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="0d3d1-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="0d3d1-106">支援的案例</span><span class="sxs-lookup"><span data-stu-id="0d3d1-106">Supported scenarios</span></span>
<span data-ttu-id="0d3d1-107">您可以從內部部署檔案系統將資料複製到下列資料存放區：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-107">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="0d3d1-108">您可以從下列資料存放區將資料複製到內部部署檔案系統：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-108">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="0d3d1-109">來源檔案成功複製至目的地後，「複製活動」不會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="0d3d1-110">如果您需要在成功複製後刪除來源檔案，請建立自訂活動來刪除檔案，並在管道中使用該活動。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="0d3d1-111">啟用連線</span><span class="sxs-lookup"><span data-stu-id="0d3d1-111">Enabling connectivity</span></span>
<span data-ttu-id="0d3d1-112">Data Factory 支援透過「資料管理閘道」連接到內部部署的檔案系統，或從內部部署的檔案系統連出。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-112">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="0d3d1-113">您必須在內部部署環境安裝「資料管理閘道」，Data Factory 服務才能連接到任何支援的內部部署資料存放區 (包括檔案系統)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-113">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="0d3d1-114">如需有關資料管理閘道以及設定閘道的逐步指示，請參閱[利用資料管理閘道在內部部署資源和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-114">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="0d3d1-115">除了資料管理閘道，不需要安裝其他二進位檔即可和內部部署檔案系統進行通訊。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-115">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="0d3d1-116">您必須安裝和使用「資料管理閘道」，即使檔案系統位於 Azure IaaS VM 中也一樣。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-116">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="0d3d1-117">如需有關閘道的詳細資訊，請參閱[資料管理閘道](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-117">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="0d3d1-118">若要使用 Linux 檔案共用，請在 Linux 伺服器上安裝 [Samba](https://www.samba.org/)，在 Windows 伺服器上安裝「資料管理閘道」。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-118">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="0d3d1-119">不支援在 Linux 伺服器上安裝資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0d3d1-120">開始使用</span><span class="sxs-lookup"><span data-stu-id="0d3d1-120">Getting started</span></span>
<span data-ttu-id="0d3d1-121">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以將資料移進/移出檔案系統。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="0d3d1-122">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="0d3d1-123">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="0d3d1-124">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0d3d1-125">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="0d3d1-126">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="0d3d1-127">建立 **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-127">Create a **data factory**.</span></span> <span data-ttu-id="0d3d1-128">資料處理站可包含一或多個管線。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="0d3d1-129">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="0d3d1-130">例如，如果您從 Azure Blob 儲存體將資料複製到內部部署檔案系統，您會建立兩個連結服務，將內部部署檔案系統和 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-130">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="0d3d1-131">有關內部部署檔案系統專屬的連結服務屬性，請參閱[連結服務屬性](#linked-service-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-131">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="0d3d1-132">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="0d3d1-133">在上一個步驟所述的範例中，您可以建立資料集來指定包含輸入資料的 Blob 容器與資料夾。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="0d3d1-134">同時，您會建立另一個資料集來指定檔案系統中的資料夾與檔案名稱 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-134">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="0d3d1-135">針對內部部署檔案系統專屬的資料集屬性，請參閱[資料集屬性](#dataset-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-135">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="0d3d1-136">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="0d3d1-137">在稍早所述的範例中，您使用 BlobSource 作為來源，以及使用 FileSystemSink 作為複製活動的接收器。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-137">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="0d3d1-138">同樣地，如果您是從內部部署檔案系統複製到 Azure Blob 儲存體，則在複製活動中使用 FileSystemSource 和 BlobSink。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-138">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="0d3d1-139">針對內部部署檔案系統專屬的複製活動屬性，請參閱[複製活動屬性](#copy-activity-properties)一節。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-139">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="0d3d1-140">如需有關如何使用資料存放區作為來源或接收器的詳細資訊，請按一下上一節中資料存放區的連結。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="0d3d1-141">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="0d3d1-142">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="0d3d1-143">如需相關範例，其中含有用來將資料複製到檔案系統 (或從檔案系統複製資料) 之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例](#json-examples-for-copying-data-to-and-from-file-system)一節。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="0d3d1-144">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義檔案系統特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0d3d1-145">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="0d3d1-145">Linked service properties</span></span>
<span data-ttu-id="0d3d1-146">您可以利用「內部部署檔案伺服器」已連結服務，將內部部署的檔案系統連結到 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-146">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="0d3d1-147">下表說明內部部署檔案伺服器連結服務專屬的 JSON 元素。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-147">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="0d3d1-148">屬性</span><span class="sxs-lookup"><span data-stu-id="0d3d1-148">Property</span></span> | <span data-ttu-id="0d3d1-149">說明</span><span class="sxs-lookup"><span data-stu-id="0d3d1-149">Description</span></span> | <span data-ttu-id="0d3d1-150">必要</span><span class="sxs-lookup"><span data-stu-id="0d3d1-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d3d1-151">類型</span><span class="sxs-lookup"><span data-stu-id="0d3d1-151">type</span></span> |<span data-ttu-id="0d3d1-152">確保 type 屬性設為 **OnPremisesFileServer**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-152">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="0d3d1-153">是</span><span class="sxs-lookup"><span data-stu-id="0d3d1-153">Yes</span></span> |
| <span data-ttu-id="0d3d1-154">主機</span><span class="sxs-lookup"><span data-stu-id="0d3d1-154">host</span></span> |<span data-ttu-id="0d3d1-155">指定想要複製之資料夾的根路徑。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-155">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="0d3d1-156">字串中的特殊字元需使用逸出字元 ‘ \ ’。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-156">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="0d3d1-157">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="0d3d1-158">是</span><span class="sxs-lookup"><span data-stu-id="0d3d1-158">Yes</span></span> |
| <span data-ttu-id="0d3d1-159">userid</span><span class="sxs-lookup"><span data-stu-id="0d3d1-159">userid</span></span> |<span data-ttu-id="0d3d1-160">指定具有伺服器存取權之使用者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-160">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="0d3d1-161">否 (如果您選擇 encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="0d3d1-162">password</span><span class="sxs-lookup"><span data-stu-id="0d3d1-162">password</span></span> |<span data-ttu-id="0d3d1-163">指定使用者 (userid) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-163">Specify the password for the user (userid).</span></span> |<span data-ttu-id="0d3d1-164">否 (如果您選擇 encryptedCredential)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="0d3d1-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="0d3d1-165">encryptedCredential</span></span> |<span data-ttu-id="0d3d1-166">指定可以透過執行 New-AzureRmDataFactoryEncryptValue Cmdlet 來取得的加密認證。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-166">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="0d3d1-167">否 (如果您選擇以純文字指定使用者識別碼和密碼)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-167">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="0d3d1-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0d3d1-168">gatewayName</span></span> |<span data-ttu-id="0d3d1-169">指定 Data Factory 應該用來連接到內部部署檔案伺服器的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-169">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="0d3d1-170">是</span><span class="sxs-lookup"><span data-stu-id="0d3d1-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="0d3d1-171">範例連結服務和資料集定義</span><span class="sxs-lookup"><span data-stu-id="0d3d1-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="0d3d1-172">案例</span><span class="sxs-lookup"><span data-stu-id="0d3d1-172">Scenario</span></span> | <span data-ttu-id="0d3d1-173">連結服務定義中的主機</span><span class="sxs-lookup"><span data-stu-id="0d3d1-173">Host in linked service definition</span></span> | <span data-ttu-id="0d3d1-174">資料集定義中的 folderPath</span><span class="sxs-lookup"><span data-stu-id="0d3d1-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d3d1-175">資料管理閘道電腦上的本機資料夾︰</span><span class="sxs-lookup"><span data-stu-id="0d3d1-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="0d3d1-176">範例：D:\\\* 或 D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="0d3d1-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="0d3d1-177">D:\\\\ (適用於資料管理閘道 2.0 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="0d3d1-178">localhost (適用於比資料管理閘道 2.0 更早的版本)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="0d3d1-179">.\\\\ 或 folder\\\\subfolder (適用於資料管理閘道 2.0 和更新版本)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="0d3d1-180">D:\\\\ 或 D:\\\\folder\\\\subfolder (適用低於閘道 2.0 的版本)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="0d3d1-181">遠端共用資料夾︰</span><span class="sxs-lookup"><span data-stu-id="0d3d1-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="0d3d1-182">範例︰\\\\myserver\\share\\\* 或 \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="0d3d1-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="0d3d1-183">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="0d3d1-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="0d3d1-184">.\\\\ 或 folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="0d3d1-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="0d3d1-185">範例：使用純文字的使用者名稱和密碼</span><span class="sxs-lookup"><span data-stu-id="0d3d1-185">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="0d3d1-186">範例：使用 encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="0d3d1-186">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="0d3d1-187">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="0d3d1-187">Dataset properties</span></span>
<span data-ttu-id="0d3d1-188">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="0d3d1-189">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="0d3d1-190">不同類型資料集的 TypeProperties 區段不同。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-190">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="0d3d1-191">它提供各種資訊，例如資料存放區中資料的格式與位置。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-191">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="0d3d1-192">**FileShare** 類型資料集的 typeProperties 區段有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-192">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="0d3d1-193">屬性</span><span class="sxs-lookup"><span data-stu-id="0d3d1-193">Property</span></span> | <span data-ttu-id="0d3d1-194">說明</span><span class="sxs-lookup"><span data-stu-id="0d3d1-194">Description</span></span> | <span data-ttu-id="0d3d1-195">必要</span><span class="sxs-lookup"><span data-stu-id="0d3d1-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d3d1-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="0d3d1-196">folderPath</span></span> |<span data-ttu-id="0d3d1-197">指定資料夾的子路徑。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-197">Specifies the subpath to the folder.</span></span> <span data-ttu-id="0d3d1-198">字串中的特殊字元需使用逸出字元 ‘ \ ’。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-198">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="0d3d1-199">如需範例，請參閱 [範例連結服務和資料集定義](#sample-linked-service-and-dataset-definitions) 。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="0d3d1-200">您可以結合此屬性與 **partitionBy**，讓資料夾路徑以配量開始/結束日期時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-200">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="0d3d1-201">是</span><span class="sxs-lookup"><span data-stu-id="0d3d1-201">Yes</span></span> |
| <span data-ttu-id="0d3d1-202">fileName</span><span class="sxs-lookup"><span data-stu-id="0d3d1-202">fileName</span></span> |<span data-ttu-id="0d3d1-203">如果您想要資料表參考資料夾中的特定檔案，請指定 **folderPath** 中的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-203">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="0d3d1-204">如果沒有為此屬性指定任何值，資料表會指向資料夾中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-204">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="0d3d1-205">當未指定輸出資料集的 fileName，且在活動接收中未指定 preserveHierarchy 時，所產生檔案的名稱格式如下：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="0d3d1-206">`Data.<Guid>.txt` (例如： Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="0d3d1-207">否</span><span class="sxs-lookup"><span data-stu-id="0d3d1-207">No</span></span> |
| <span data-ttu-id="0d3d1-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="0d3d1-208">fileFilter</span></span> |<span data-ttu-id="0d3d1-209">指定要用來在 folderPath (而不是所有檔案) 中選取檔案子集的篩選器。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-209">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="0d3d1-210">允許的值為︰`*` (多個字元) 和 `?` (單一字元)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="0d3d1-211">範例 1："fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="0d3d1-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="0d3d1-212">範例 2："fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="0d3d1-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="0d3d1-213">請注意，fileFilter 適用於輸入 FileShare 資料集。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="0d3d1-214">否</span><span class="sxs-lookup"><span data-stu-id="0d3d1-214">No</span></span> |
| <span data-ttu-id="0d3d1-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0d3d1-215">partitionedBy</span></span> |<span data-ttu-id="0d3d1-216">您可以使用 partitionedBy 來指定時間序列資料的動態 folderPath/fileName。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-216">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="0d3d1-217">例如，folderPath 可針對每小時的資料進行參數化。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="0d3d1-218">否</span><span class="sxs-lookup"><span data-stu-id="0d3d1-218">No</span></span> |
| <span data-ttu-id="0d3d1-219">format</span><span class="sxs-lookup"><span data-stu-id="0d3d1-219">format</span></span> | <span data-ttu-id="0d3d1-220">支援下列格式類型：**TextFormat**、**JsonFormat**、**AvroFormat**、**OrcFormat**、**ParquetFormat**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-220">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0d3d1-221">將格式下的 **type** 屬性設定為這些值其中之一。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-221">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="0d3d1-222">如需詳細資訊，請參閱[文字格式](data-factory-supported-file-and-compression-formats.md#text-format)、[Json 格式](data-factory-supported-file-and-compression-formats.md#json-format)、[Avro 格式](data-factory-supported-file-and-compression-formats.md#avro-format)、[Orc 格式](data-factory-supported-file-and-compression-formats.md#orc-format)和 [Parquet 格式](data-factory-supported-file-and-compression-formats.md#parquet-format)章節。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0d3d1-223">如果您想要在以檔案為基礎的存放區之間**依原樣複製檔案** (二進位複本)，請在輸入和輸出資料集定義中略過格式區段。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-223">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0d3d1-224">否</span><span class="sxs-lookup"><span data-stu-id="0d3d1-224">No</span></span> |
| <span data-ttu-id="0d3d1-225">compression</span><span class="sxs-lookup"><span data-stu-id="0d3d1-225">compression</span></span> | <span data-ttu-id="0d3d1-226">指定此資料的壓縮類型和層級。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-226">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="0d3d1-227">支援的類型為：**GZip**、**Deflate**、**BZip2** 及 **ZipDeflate**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0d3d1-228">支援的層級為：**Optimal** 和 **Fastest**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0d3d1-229">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md#compression-support)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0d3d1-230">否</span><span class="sxs-lookup"><span data-stu-id="0d3d1-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="0d3d1-231">無法同時使用 fileName 和 fileFilter。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="0d3d1-232">使用 partitionedBy 屬性</span><span class="sxs-lookup"><span data-stu-id="0d3d1-232">Using partitionedBy property</span></span>
<span data-ttu-id="0d3d1-233">如上一節所述，您可以使用 **partitionedBy** 屬性、[Data Factory 函式及系統變數](data-factory-functions-variables.md)，來指定時間序列資料的動態 folderPath 和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-233">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="0d3d1-234">若要進一步了解時間序列資料集、排程和配量，請參閱[建立資料集](data-factory-create-datasets.md)、[排程和執行](data-factory-scheduling-and-execution.md)以及[建立管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-234">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="0d3d1-235">範例 1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="0d3d1-236">在此範例中，{Slice} 會取代成 Data Factory 系統變數 SliceStart 的值，其格式為 (YYYYMMDDHH)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-236">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="0d3d1-237">SliceStart 是指配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-237">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="0d3d1-238">每個配量的 folderPath 都不同。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-238">The folderPath is different for each slice.</span></span> <span data-ttu-id="0d3d1-239">例如：wikidatagateway/wikisampledataout/2014100103 或 wikidatagateway/wikisampledataout/2014100104。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="0d3d1-240">範例 2：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-240">Sample 2:</span></span>

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

<span data-ttu-id="0d3d1-241">在此範例中，會擷取 SliceStart 的年、月、日和時間給 folderPath 和 fileName 屬性所使用的個別變數。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="0d3d1-242">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="0d3d1-242">Copy activity properties</span></span>
<span data-ttu-id="0d3d1-243">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-243">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0d3d1-244">屬性 (例如名稱、描述、輸入和輸出資料集，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="0d3d1-245">而活動的 **typeProperties** 區段中，可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-245">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="0d3d1-246">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-246">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="0d3d1-247">如果您要從內部部署的檔案系統移動資料，需將複製活動中的來源類型設定為 **FileSystemSource**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-247">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="0d3d1-248">同樣地，如果您要將資料移到內部部署的檔案系統，則需將複製活動中的接收器類型設定為 **FileSystemSink**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-248">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="0d3d1-249">本節提供 FileSystemSource 和 FileSystemSink 所支援的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="0d3d1-250">**FileSystemSource** 支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-250">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="0d3d1-251">屬性</span><span class="sxs-lookup"><span data-stu-id="0d3d1-251">Property</span></span> | <span data-ttu-id="0d3d1-252">說明</span><span class="sxs-lookup"><span data-stu-id="0d3d1-252">Description</span></span> | <span data-ttu-id="0d3d1-253">允許的值</span><span class="sxs-lookup"><span data-stu-id="0d3d1-253">Allowed values</span></span> | <span data-ttu-id="0d3d1-254">必要</span><span class="sxs-lookup"><span data-stu-id="0d3d1-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d3d1-255">遞迴</span><span class="sxs-lookup"><span data-stu-id="0d3d1-255">recursive</span></span> |<span data-ttu-id="0d3d1-256">指出是否從子資料夾、或只有從指定的資料夾，以遞迴方式讀取資料。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-256">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="0d3d1-257">True/False (預設值為 False)</span><span class="sxs-lookup"><span data-stu-id="0d3d1-257">True, False (default)</span></span> |<span data-ttu-id="0d3d1-258">否</span><span class="sxs-lookup"><span data-stu-id="0d3d1-258">No</span></span> |

<span data-ttu-id="0d3d1-259">**FileSystemSink** 支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-259">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="0d3d1-260">屬性</span><span class="sxs-lookup"><span data-stu-id="0d3d1-260">Property</span></span> | <span data-ttu-id="0d3d1-261">說明</span><span class="sxs-lookup"><span data-stu-id="0d3d1-261">Description</span></span> | <span data-ttu-id="0d3d1-262">允許的值</span><span class="sxs-lookup"><span data-stu-id="0d3d1-262">Allowed values</span></span> | <span data-ttu-id="0d3d1-263">必要</span><span class="sxs-lookup"><span data-stu-id="0d3d1-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d3d1-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="0d3d1-264">copyBehavior</span></span> |<span data-ttu-id="0d3d1-265">當來源為 BlobSource 或 FileSystem 時，定義複製行為。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-265">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="0d3d1-266">**PreserveHierarchy：**保留目標資料夾中的檔案階層。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-266">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="0d3d1-267">亦即，來源檔案到來源資料夾的相對路徑，與目標檔案到目標資料夾的相對路徑相同。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-267">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="0d3d1-268">**FlattenHierarchy：**來源資料夾的中所有檔案都會建立在目標資料夾的第一層中。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-268">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="0d3d1-269">建立的目標檔案會具有自動產生的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-269">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="0d3d1-270">**MergeFiles：**將來源資料夾的所有檔案合併為一個檔案。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-270">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="0d3d1-271">如果有指定檔案/Blob 名稱，合併檔案的名稱會是指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-271">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="0d3d1-272">否則，就會是自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="0d3d1-273">否</span><span class="sxs-lookup"><span data-stu-id="0d3d1-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="0d3d1-274">遞迴和 copyBehavior 範例</span><span class="sxs-lookup"><span data-stu-id="0d3d1-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="0d3d1-275">本節說明 recursive 和 copyBehavior 屬性在不同組合的情況下，複製作業所產生的行為。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-275">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="0d3d1-276">recursive 值</span><span class="sxs-lookup"><span data-stu-id="0d3d1-276">recursive value</span></span> | <span data-ttu-id="0d3d1-277">copyBehavior 值</span><span class="sxs-lookup"><span data-stu-id="0d3d1-277">copyBehavior value</span></span> | <span data-ttu-id="0d3d1-278">產生的行為</span><span class="sxs-lookup"><span data-stu-id="0d3d1-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d3d1-279">true</span><span class="sxs-lookup"><span data-stu-id="0d3d1-279">true</span></span> |<span data-ttu-id="0d3d1-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="0d3d1-280">preserveHierarchy</span></span> |<span data-ttu-id="0d3d1-281">具有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-281">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="0d3d1-282">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-282">Folder1</span></span><br/><span data-ttu-id="0d3d1-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="0d3d1-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="0d3d1-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="0d3d1-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="0d3d1-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="0d3d1-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="0d3d1-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="0d3d1-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="0d3d1-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="0d3d1-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="0d3d1-289">會以與來源相同的結構，建立目標資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-289">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="0d3d1-290">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-290">Folder1</span></span><br/><span data-ttu-id="0d3d1-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="0d3d1-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="0d3d1-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="0d3d1-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="0d3d1-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="0d3d1-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="0d3d1-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="0d3d1-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="0d3d1-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="0d3d1-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="0d3d1-297">true</span><span class="sxs-lookup"><span data-stu-id="0d3d1-297">true</span></span> |<span data-ttu-id="0d3d1-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="0d3d1-298">flattenHierarchy</span></span> |<span data-ttu-id="0d3d1-299">具有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-299">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="0d3d1-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-300">Folder1</span></span><br/><span data-ttu-id="0d3d1-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="0d3d1-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="0d3d1-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="0d3d1-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="0d3d1-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="0d3d1-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="0d3d1-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="0d3d1-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="0d3d1-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="0d3d1-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="0d3d1-307">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="0d3d1-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-308">Folder1</span></span><br/><span data-ttu-id="0d3d1-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="0d3d1-310">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="0d3d1-311">&nbsp;&nbsp;&nbsp;&nbsp;File3 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="0d3d1-312">&nbsp;&nbsp;&nbsp;&nbsp;File4 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="0d3d1-313">&nbsp;&nbsp;&nbsp;&nbsp;File5 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="0d3d1-314">true</span><span class="sxs-lookup"><span data-stu-id="0d3d1-314">true</span></span> |<span data-ttu-id="0d3d1-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="0d3d1-315">mergeFiles</span></span> |<span data-ttu-id="0d3d1-316">具有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-316">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="0d3d1-317">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-317">Folder1</span></span><br/><span data-ttu-id="0d3d1-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="0d3d1-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="0d3d1-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="0d3d1-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="0d3d1-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="0d3d1-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="0d3d1-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="0d3d1-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="0d3d1-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="0d3d1-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="0d3d1-324">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-324">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="0d3d1-325">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-325">Folder1</span></span><br/><span data-ttu-id="0d3d1-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 的內容會合併成一個檔案，並有自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="0d3d1-327">false</span><span class="sxs-lookup"><span data-stu-id="0d3d1-327">false</span></span> |<span data-ttu-id="0d3d1-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="0d3d1-328">preserveHierarchy</span></span> |<span data-ttu-id="0d3d1-329">具有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-329">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="0d3d1-330">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-330">Folder1</span></span><br/><span data-ttu-id="0d3d1-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="0d3d1-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="0d3d1-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="0d3d1-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="0d3d1-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="0d3d1-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="0d3d1-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="0d3d1-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="0d3d1-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="0d3d1-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="0d3d1-337">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-337">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="0d3d1-338">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-338">Folder1</span></span><br/><span data-ttu-id="0d3d1-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="0d3d1-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="0d3d1-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="0d3d1-341">系統不會挑選含有 File3、File4、File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="0d3d1-342">false</span><span class="sxs-lookup"><span data-stu-id="0d3d1-342">false</span></span> |<span data-ttu-id="0d3d1-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="0d3d1-343">flattenHierarchy</span></span> |<span data-ttu-id="0d3d1-344">具有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-344">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="0d3d1-345">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-345">Folder1</span></span><br/><span data-ttu-id="0d3d1-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="0d3d1-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="0d3d1-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="0d3d1-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="0d3d1-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="0d3d1-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="0d3d1-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="0d3d1-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="0d3d1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="0d3d1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="0d3d1-352">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-352">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="0d3d1-353">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-353">Folder1</span></span><br/><span data-ttu-id="0d3d1-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="0d3d1-355">&nbsp;&nbsp;&nbsp;&nbsp;File2 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="0d3d1-356">系統不會挑選含有 File3、File4、File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="0d3d1-357">false</span><span class="sxs-lookup"><span data-stu-id="0d3d1-357">false</span></span> |<span data-ttu-id="0d3d1-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="0d3d1-358">mergeFiles</span></span> |<span data-ttu-id="0d3d1-359">具有下列結構的來源資料夾 Folder1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-359">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="0d3d1-360">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-360">Folder1</span></span><br/><span data-ttu-id="0d3d1-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="0d3d1-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span><span class="sxs-lookup"><span data-stu-id="0d3d1-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="0d3d1-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="0d3d1-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span><span class="sxs-lookup"><span data-stu-id="0d3d1-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="0d3d1-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="0d3d1-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="0d3d1-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="0d3d1-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="0d3d1-367">會以下列結構建立目標資料夾 1：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-367">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="0d3d1-368">Folder1</span><span class="sxs-lookup"><span data-stu-id="0d3d1-368">Folder1</span></span><br/><span data-ttu-id="0d3d1-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 的內容會合併成一個檔案，並有自動產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="0d3d1-370">&nbsp;&nbsp;&nbsp;&nbsp;File1 有自動產生的名稱</span><span class="sxs-lookup"><span data-stu-id="0d3d1-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="0d3d1-371">系統不會挑選含有 File3、File4、File5 的 Subfolder1。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="0d3d1-372">支援的檔案和壓縮格式</span><span class="sxs-lookup"><span data-stu-id="0d3d1-372">Supported file and compression formats</span></span>
<span data-ttu-id="0d3d1-373">請參閱 [Azure Data Factory 中的檔案和壓縮格式](data-factory-supported-file-and-compression-formats.md)文章以了解詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="0d3d1-374">從檔案系統來回複製資料的 JSON 範例</span><span class="sxs-lookup"><span data-stu-id="0d3d1-374">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="0d3d1-375">以下範例提供可用來使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 建立管線的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-375">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0d3d1-376">它們會示範如何將資料複製到內部部署檔案系統和 Azure Blob 儲存體，以及複製其中的資料。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-376">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="0d3d1-377">您可以使用 Azure Data Factory 中的複製活動，把資料「直接」複製到[支援的來源和接收器](data-factory-data-movement-activities.md#supported-data-stores-and-formats)一文中所述的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-377">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="0d3d1-378">範例：將資料從內部部署檔案系統複製到 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="0d3d1-378">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="0d3d1-379">此範例示範如何將資料從內部部署檔案系統複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-379">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="0d3d1-380">範例有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="0d3d1-380">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="0d3d1-381">[OnPremisesFileServer](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="0d3d1-382">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="0d3d1-383">[FileShare](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="0d3d1-384">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="0d3d1-385">具有使用 [FileSystemSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0d3d1-386">下列範例每小時都會將時間序列資料從內部部署檔案系統複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-386">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="0d3d1-387">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-387">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="0d3d1-388">首先，依照[利用資料管理閘道在內部部署來源和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)的指示設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-388">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="0d3d1-389">**內部部署檔案伺服器連結服務：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-389">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="0d3d1-390">我們建議使用 **encryptedCredential** 屬性，而不要使用 **userid** 和 **password** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-390">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="0d3d1-391">如需此連結服務的詳細資訊，請參閱[檔案系統連結服務](#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="0d3d1-392">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="0d3d1-393">**內部部署檔案系統輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="0d3d1-394">每小時從新的檔案挑選資料。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="0d3d1-395">會根據配量的開始時間來決定 folderPath 和 fileName 屬性。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-395">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="0d3d1-396">`"external": "true"` 設定會通知 Data Factory：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-396">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="0d3d1-397">**Azure Blob 儲存體資料集：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="0d3d1-398">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-398">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0d3d1-399">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-399">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="0d3d1-400">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-400">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="0d3d1-401">**具有檔案系統來源和 Blob 接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="0d3d1-402">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-402">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="0d3d1-403">在管線 JSON 定義中，**source** 類型設為 **FileSystemSource**，而 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-403">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="0d3d1-404">範例：將資料從 Azure SQL Database 複製到內部部署檔案系統</span><span class="sxs-lookup"><span data-stu-id="0d3d1-404">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="0d3d1-405">下列範例顯示︰</span><span class="sxs-lookup"><span data-stu-id="0d3d1-405">The following sample shows:</span></span>

* <span data-ttu-id="0d3d1-406">[AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 類型的已連結服務。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="0d3d1-407">[OnPremisesFileServer](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="0d3d1-408">[AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 類型的輸入資料集。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="0d3d1-409">[FileShare](#dataset-properties) 類型的輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="0d3d1-410">具有使用 [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) 和 [FileSystemSink](#copy-activity-properties) 之複製活動的管線。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="0d3d1-411">此範例會每小時將時間序列資料從 Azure SQL 資料表複製到內部部署檔案系統。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-411">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="0d3d1-412">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-412">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="0d3d1-413">**Azure SQL Database 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-413">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="0d3d1-414">**內部部署檔案伺服器連結服務：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-414">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="0d3d1-415">我們建議使用 **encryptedCredential** 屬性，而不要使用 **userid** 和 **password** 屬性。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-415">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="0d3d1-416">如需此連結服務的詳細資訊，請參閱[檔案系統連結服務](#linked-service-properties)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="0d3d1-417">**Azure SQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="0d3d1-418">此範例假設您已在 SQL Azure 中建立 "MyTable" 資料表，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-418">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="0d3d1-419">``“external”: ”true”`` 設定會通知 Data Factory：這是 Data Factory 外部的資料集而且不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-419">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="0d3d1-420">**內部部署檔案系統輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="0d3d1-421">資料會每小時複製到新的檔案。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-421">Data is copied to a new file every hour.</span></span> <span data-ttu-id="0d3d1-422">會根據配量的開始時間來決定 Blob 的 folderPath 和 fileName。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-422">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

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

<span data-ttu-id="0d3d1-423">**具有 SQL 來源和檔案系統接收器的管線中複製活動：**</span><span class="sxs-lookup"><span data-stu-id="0d3d1-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="0d3d1-424">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-424">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="0d3d1-425">在管線 JSON 定義中，**source** 類型設為 **SqlSource**，而 **sink** 類型設為 **FileSystemSink**。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-425">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="0d3d1-426">針對 **SqlReaderQuery** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-426">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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


<span data-ttu-id="0d3d1-427">您也可以在複製活動定義中，將來自來源資料集的資料行與來自接收資料集的資料行對應。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-427">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="0d3d1-428">如需詳細資料，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0d3d1-429">效能和微調</span><span class="sxs-lookup"><span data-stu-id="0d3d1-429">Performance and tuning</span></span>
 <span data-ttu-id="0d3d1-430">若要了解 Azure Data Factory 中影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法，請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="0d3d1-430">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
