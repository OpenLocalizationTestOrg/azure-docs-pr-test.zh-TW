---
title: "使用 Azure Data Factory 從 Teradata 移動資料 | Microsoft Docs"
description: "了解 Data Factory 服務的 Teradata 連接器，其可讓您從 Teradata 資料庫移動資料"
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
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="e1c69-103">使用 Azure Data Factory 從 Teradata 移動資料</span><span class="sxs-lookup"><span data-stu-id="e1c69-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="e1c69-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署的 Teradata 資料庫移動資料。</span><span class="sxs-lookup"><span data-stu-id="e1c69-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="e1c69-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="e1c69-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="e1c69-106">您可以將資料從內部部署的 Teradata 資料存放區複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="e1c69-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="e1c69-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="e1c69-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="e1c69-108">Data Factory 目前只支援將資料從 Teradata 資料存放區移到其他資料存放區，而不支援將資料從其他資料存放區移到 Teradata 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="e1c69-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e1c69-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="e1c69-109">Prerequisites</span></span>
<span data-ttu-id="e1c69-110">資料處理站支援透過資料管理閘道器連接至內部部署 Teradata 來源。</span><span class="sxs-lookup"><span data-stu-id="e1c69-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="e1c69-111">請參閱 [在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文來了解資料管理閘道和設定閘道的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="e1c69-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="e1c69-112">即使 Teradata 裝載於 Azure IaaS VM 中，也必須要有閘道。</span><span class="sxs-lookup"><span data-stu-id="e1c69-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="e1c69-113">您可以將閘道安裝在與資料存放區相同或相異的 IaaS VM 上，只要閘道可以連線到資料庫即可。</span><span class="sxs-lookup"><span data-stu-id="e1c69-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c69-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="e1c69-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="e1c69-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="e1c69-115">Supported versions and installation</span></span>
<span data-ttu-id="e1c69-116">若要讓資料管理閘道連接至 Teradata 資料庫，您必須在與資料管理閘道相同的系統上，安裝 [Teradata 的 .NET 資料提供者](http://go.microsoft.com/fwlink/?LinkId=278886)版本 14 或以上版本。</span><span class="sxs-lookup"><span data-stu-id="e1c69-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="e1c69-117">支援 Teradata 版本 12 和以上版本。</span><span class="sxs-lookup"><span data-stu-id="e1c69-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e1c69-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="e1c69-118">Getting started</span></span>
<span data-ttu-id="e1c69-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="e1c69-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="e1c69-120">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="e1c69-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="e1c69-121">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="e1c69-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="e1c69-122">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="e1c69-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e1c69-123">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c69-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e1c69-124">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="e1c69-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="e1c69-125">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="e1c69-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="e1c69-126">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="e1c69-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="e1c69-127">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="e1c69-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e1c69-128">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="e1c69-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="e1c69-129">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="e1c69-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="e1c69-130">如需相關範例，其中含有用來從內部部署 Teradata 資料存放區複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 Teradata 複製到 Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="e1c69-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e1c69-131">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Teradata 資料存放區特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="e1c69-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e1c69-132">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="e1c69-132">Linked service properties</span></span>
<span data-ttu-id="e1c69-133">下表提供 Teradata 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="e1c69-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="e1c69-134">屬性</span><span class="sxs-lookup"><span data-stu-id="e1c69-134">Property</span></span> | <span data-ttu-id="e1c69-135">說明</span><span class="sxs-lookup"><span data-stu-id="e1c69-135">Description</span></span> | <span data-ttu-id="e1c69-136">必要</span><span class="sxs-lookup"><span data-stu-id="e1c69-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e1c69-137">類型</span><span class="sxs-lookup"><span data-stu-id="e1c69-137">type</span></span> |<span data-ttu-id="e1c69-138">類型屬性必須設為： **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="e1c69-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="e1c69-139">是</span><span class="sxs-lookup"><span data-stu-id="e1c69-139">Yes</span></span> |
| <span data-ttu-id="e1c69-140">伺服器</span><span class="sxs-lookup"><span data-stu-id="e1c69-140">server</span></span> |<span data-ttu-id="e1c69-141">Teradata 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c69-141">Name of the Teradata server.</span></span> |<span data-ttu-id="e1c69-142">是</span><span class="sxs-lookup"><span data-stu-id="e1c69-142">Yes</span></span> |
| <span data-ttu-id="e1c69-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e1c69-143">authenticationType</span></span> |<span data-ttu-id="e1c69-144">用來連接到 Teradata 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="e1c69-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="e1c69-145">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="e1c69-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e1c69-146">是</span><span class="sxs-lookup"><span data-stu-id="e1c69-146">Yes</span></span> |
| <span data-ttu-id="e1c69-147">username</span><span class="sxs-lookup"><span data-stu-id="e1c69-147">username</span></span> |<span data-ttu-id="e1c69-148">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c69-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="e1c69-149">否</span><span class="sxs-lookup"><span data-stu-id="e1c69-149">No</span></span> |
| <span data-ttu-id="e1c69-150">password</span><span class="sxs-lookup"><span data-stu-id="e1c69-150">password</span></span> |<span data-ttu-id="e1c69-151">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c69-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="e1c69-152">否</span><span class="sxs-lookup"><span data-stu-id="e1c69-152">No</span></span> |
| <span data-ttu-id="e1c69-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e1c69-153">gatewayName</span></span> |<span data-ttu-id="e1c69-154">Data Factory 服務應該用來連接到內部部署 Teradata 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c69-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="e1c69-155">是</span><span class="sxs-lookup"><span data-stu-id="e1c69-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="e1c69-156">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="e1c69-156">Dataset properties</span></span>
<span data-ttu-id="e1c69-157">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e1c69-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e1c69-158">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="e1c69-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e1c69-159">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="e1c69-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="e1c69-160">目前沒有支援 Teradata 資料集的類型屬性。</span><span class="sxs-lookup"><span data-stu-id="e1c69-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="e1c69-161">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="e1c69-161">Copy activity properties</span></span>
<span data-ttu-id="e1c69-162">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="e1c69-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e1c69-163">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="e1c69-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="e1c69-164">而活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e1c69-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="e1c69-165">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e1c69-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="e1c69-166">當來源的類型為 **RelationalSource** (包括 Teradata) 時，**typeProperties** 區段中會有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="e1c69-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e1c69-167">屬性</span><span class="sxs-lookup"><span data-stu-id="e1c69-167">Property</span></span> | <span data-ttu-id="e1c69-168">說明</span><span class="sxs-lookup"><span data-stu-id="e1c69-168">Description</span></span> | <span data-ttu-id="e1c69-169">允許的值</span><span class="sxs-lookup"><span data-stu-id="e1c69-169">Allowed values</span></span> | <span data-ttu-id="e1c69-170">必要</span><span class="sxs-lookup"><span data-stu-id="e1c69-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e1c69-171">query</span><span class="sxs-lookup"><span data-stu-id="e1c69-171">query</span></span> |<span data-ttu-id="e1c69-172">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="e1c69-172">Use the custom query to read data.</span></span> |<span data-ttu-id="e1c69-173">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="e1c69-173">SQL query string.</span></span> <span data-ttu-id="e1c69-174">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="e1c69-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="e1c69-175">是</span><span class="sxs-lookup"><span data-stu-id="e1c69-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="e1c69-176">JSON 範例：將資料從 Teradata 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e1c69-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="e1c69-177">下列範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="e1c69-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e1c69-178">這些範例示範如何將資料從 Teradata 複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e1c69-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="e1c69-179">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="e1c69-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="e1c69-180">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="e1c69-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="e1c69-181">[OnPremisesTeradata](#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="e1c69-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="e1c69-182">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="e1c69-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e1c69-183">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c69-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="e1c69-184">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c69-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e1c69-185">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c69-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e1c69-186">此範例會每個小時將資料從 Teradata 資料庫中的查詢結果複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="e1c69-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="e1c69-187">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="e1c69-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="e1c69-188">第一步是設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="e1c69-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="e1c69-189">如需相關指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="e1c69-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="e1c69-190">**Teradata 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="e1c69-190">**Teradata linked service:**</span></span>

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

<span data-ttu-id="e1c69-191">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="e1c69-191">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="e1c69-192">**Teradata 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="e1c69-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="e1c69-193">此範例假設您已在 Teradata 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestamp")。</span><span class="sxs-lookup"><span data-stu-id="e1c69-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="e1c69-194">設定 “external”: true 可讓 Data Factory 服務知道資料表是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="e1c69-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="e1c69-195">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="e1c69-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e1c69-196">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="e1c69-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e1c69-197">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="e1c69-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e1c69-198">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="e1c69-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="e1c69-199">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="e1c69-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="e1c69-200">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="e1c69-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="e1c69-201">在管線 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="e1c69-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="e1c69-202">針對 **query** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="e1c69-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="e1c69-203">Teradata 的類型對應</span><span class="sxs-lookup"><span data-stu-id="e1c69-203">Type mapping for Teradata</span></span>
<span data-ttu-id="e1c69-204">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，「複製活動」會藉由含有下列 2 個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="e1c69-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="e1c69-205">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="e1c69-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="e1c69-206">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="e1c69-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="e1c69-207">將資料移到 Teradata 時，下列對應會用於從 Teradata 類型到 .NET 類型。</span><span class="sxs-lookup"><span data-stu-id="e1c69-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="e1c69-208">Teradata 資料庫類型</span><span class="sxs-lookup"><span data-stu-id="e1c69-208">Teradata Database type</span></span> | <span data-ttu-id="e1c69-209">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="e1c69-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="e1c69-210">Char</span><span class="sxs-lookup"><span data-stu-id="e1c69-210">Char</span></span> |<span data-ttu-id="e1c69-211">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-211">String</span></span> |
| <span data-ttu-id="e1c69-212">Clob</span><span class="sxs-lookup"><span data-stu-id="e1c69-212">Clob</span></span> |<span data-ttu-id="e1c69-213">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-213">String</span></span> |
| <span data-ttu-id="e1c69-214">圖形</span><span class="sxs-lookup"><span data-stu-id="e1c69-214">Graphic</span></span> |<span data-ttu-id="e1c69-215">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-215">String</span></span> |
| <span data-ttu-id="e1c69-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="e1c69-216">VarChar</span></span> |<span data-ttu-id="e1c69-217">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-217">String</span></span> |
| <span data-ttu-id="e1c69-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="e1c69-218">VarGraphic</span></span> |<span data-ttu-id="e1c69-219">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-219">String</span></span> |
| <span data-ttu-id="e1c69-220">Blob</span><span class="sxs-lookup"><span data-stu-id="e1c69-220">Blob</span></span> |<span data-ttu-id="e1c69-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e1c69-221">Byte[]</span></span> |
| <span data-ttu-id="e1c69-222">位元組</span><span class="sxs-lookup"><span data-stu-id="e1c69-222">Byte</span></span> |<span data-ttu-id="e1c69-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e1c69-223">Byte[]</span></span> |
| <span data-ttu-id="e1c69-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="e1c69-224">VarByte</span></span> |<span data-ttu-id="e1c69-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e1c69-225">Byte[]</span></span> |
| <span data-ttu-id="e1c69-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="e1c69-226">BigInt</span></span> |<span data-ttu-id="e1c69-227">Int64</span><span class="sxs-lookup"><span data-stu-id="e1c69-227">Int64</span></span> |
| <span data-ttu-id="e1c69-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="e1c69-228">ByteInt</span></span> |<span data-ttu-id="e1c69-229">Int16</span><span class="sxs-lookup"><span data-stu-id="e1c69-229">Int16</span></span> |
| <span data-ttu-id="e1c69-230">十進位</span><span class="sxs-lookup"><span data-stu-id="e1c69-230">Decimal</span></span> |<span data-ttu-id="e1c69-231">十進位</span><span class="sxs-lookup"><span data-stu-id="e1c69-231">Decimal</span></span> |
| <span data-ttu-id="e1c69-232">兩倍</span><span class="sxs-lookup"><span data-stu-id="e1c69-232">Double</span></span> |<span data-ttu-id="e1c69-233">兩倍</span><span class="sxs-lookup"><span data-stu-id="e1c69-233">Double</span></span> |
| <span data-ttu-id="e1c69-234">Integer</span><span class="sxs-lookup"><span data-stu-id="e1c69-234">Integer</span></span> |<span data-ttu-id="e1c69-235">Int32</span><span class="sxs-lookup"><span data-stu-id="e1c69-235">Int32</span></span> |
| <span data-ttu-id="e1c69-236">Number</span><span class="sxs-lookup"><span data-stu-id="e1c69-236">Number</span></span> |<span data-ttu-id="e1c69-237">兩倍</span><span class="sxs-lookup"><span data-stu-id="e1c69-237">Double</span></span> |
| <span data-ttu-id="e1c69-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="e1c69-238">SmallInt</span></span> |<span data-ttu-id="e1c69-239">Int16</span><span class="sxs-lookup"><span data-stu-id="e1c69-239">Int16</span></span> |
| <span data-ttu-id="e1c69-240">Date</span><span class="sxs-lookup"><span data-stu-id="e1c69-240">Date</span></span> |<span data-ttu-id="e1c69-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="e1c69-241">DateTime</span></span> |
| <span data-ttu-id="e1c69-242">時間</span><span class="sxs-lookup"><span data-stu-id="e1c69-242">Time</span></span> |<span data-ttu-id="e1c69-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-243">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-244">時區的時間</span><span class="sxs-lookup"><span data-stu-id="e1c69-244">Time With Time Zone</span></span> |<span data-ttu-id="e1c69-245">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-245">String</span></span> |
| <span data-ttu-id="e1c69-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="e1c69-246">Timestamp</span></span> |<span data-ttu-id="e1c69-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="e1c69-247">DateTime</span></span> |
| <span data-ttu-id="e1c69-248">時區的時間戳記</span><span class="sxs-lookup"><span data-stu-id="e1c69-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="e1c69-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="e1c69-249">DateTimeOffset</span></span> |
| <span data-ttu-id="e1c69-250">間隔日</span><span class="sxs-lookup"><span data-stu-id="e1c69-250">Interval Day</span></span> |<span data-ttu-id="e1c69-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-251">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-252">間隔日至小時</span><span class="sxs-lookup"><span data-stu-id="e1c69-252">Interval Day To Hour</span></span> |<span data-ttu-id="e1c69-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-253">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-254">間隔日至分鐘</span><span class="sxs-lookup"><span data-stu-id="e1c69-254">Interval Day To Minute</span></span> |<span data-ttu-id="e1c69-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-255">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-256">間隔日至秒鐘</span><span class="sxs-lookup"><span data-stu-id="e1c69-256">Interval Day To Second</span></span> |<span data-ttu-id="e1c69-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-257">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-258">間隔小時</span><span class="sxs-lookup"><span data-stu-id="e1c69-258">Interval Hour</span></span> |<span data-ttu-id="e1c69-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-259">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-260">間隔小時至分鐘</span><span class="sxs-lookup"><span data-stu-id="e1c69-260">Interval Hour To Minute</span></span> |<span data-ttu-id="e1c69-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-261">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-262">間隔小時至秒鐘</span><span class="sxs-lookup"><span data-stu-id="e1c69-262">Interval Hour To Second</span></span> |<span data-ttu-id="e1c69-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-263">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-264">間隔分鐘</span><span class="sxs-lookup"><span data-stu-id="e1c69-264">Interval Minute</span></span> |<span data-ttu-id="e1c69-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-265">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-266">間隔分鐘至秒鐘</span><span class="sxs-lookup"><span data-stu-id="e1c69-266">Interval Minute To Second</span></span> |<span data-ttu-id="e1c69-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-267">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-268">間隔第二</span><span class="sxs-lookup"><span data-stu-id="e1c69-268">Interval Second</span></span> |<span data-ttu-id="e1c69-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e1c69-269">TimeSpan</span></span> |
| <span data-ttu-id="e1c69-270">間隔年</span><span class="sxs-lookup"><span data-stu-id="e1c69-270">Interval Year</span></span> |<span data-ttu-id="e1c69-271">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-271">String</span></span> |
| <span data-ttu-id="e1c69-272">間隔年至月</span><span class="sxs-lookup"><span data-stu-id="e1c69-272">Interval Year To Month</span></span> |<span data-ttu-id="e1c69-273">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-273">String</span></span> |
| <span data-ttu-id="e1c69-274">間隔月</span><span class="sxs-lookup"><span data-stu-id="e1c69-274">Interval Month</span></span> |<span data-ttu-id="e1c69-275">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-275">String</span></span> |
| <span data-ttu-id="e1c69-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="e1c69-276">Period(Date)</span></span> |<span data-ttu-id="e1c69-277">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-277">String</span></span> |
| <span data-ttu-id="e1c69-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="e1c69-278">Period(Time)</span></span> |<span data-ttu-id="e1c69-279">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-279">String</span></span> |
| <span data-ttu-id="e1c69-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="e1c69-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="e1c69-281">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-281">String</span></span> |
| <span data-ttu-id="e1c69-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="e1c69-282">Period(Timestamp)</span></span> |<span data-ttu-id="e1c69-283">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-283">String</span></span> |
| <span data-ttu-id="e1c69-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="e1c69-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="e1c69-285">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-285">String</span></span> |
| <span data-ttu-id="e1c69-286">Xml</span><span class="sxs-lookup"><span data-stu-id="e1c69-286">Xml</span></span> |<span data-ttu-id="e1c69-287">String</span><span class="sxs-lookup"><span data-stu-id="e1c69-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="e1c69-288">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="e1c69-288">Map source to sink columns</span></span>
<span data-ttu-id="e1c69-289">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c69-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e1c69-290">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="e1c69-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="e1c69-291">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="e1c69-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="e1c69-292">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="e1c69-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e1c69-293">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="e1c69-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e1c69-294">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="e1c69-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e1c69-295">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="e1c69-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e1c69-296">效能和微調</span><span class="sxs-lookup"><span data-stu-id="e1c69-296">Performance and Tuning</span></span>
<span data-ttu-id="e1c69-297">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="e1c69-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
