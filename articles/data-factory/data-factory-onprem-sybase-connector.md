---
title: "使用 Azure Data Factory 從 Sybase 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 Sybase 資料庫移動資料。"
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
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="abed8-103">使用 Azure Data Factory 從 Sybase 移動資料</span><span class="sxs-lookup"><span data-stu-id="abed8-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="abed8-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署的 Sybase 資料庫移動資料。</span><span class="sxs-lookup"><span data-stu-id="abed8-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="abed8-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="abed8-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="abed8-106">您可以將資料從內部部署的 Sybase 資料存放區複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="abed8-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="abed8-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="abed8-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="abed8-108">Data Factory 目前只支援將資料從 Sybase 資料存放區移到其他資料存放區，而不支援將資料從其他資料存放區移到 Sybase 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="abed8-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="abed8-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="abed8-109">Prerequisites</span></span>
<span data-ttu-id="abed8-110">Data Factory 服務支援使用資料管理閘道器連接至內部部署 Sybase 來源。</span><span class="sxs-lookup"><span data-stu-id="abed8-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="abed8-111">請參閱 [在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文來了解資料管理閘道和設定閘道的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="abed8-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="abed8-112">即使 Sybase 資料庫裝載於 Azure IaaS VM 中，也必須要有閘道。</span><span class="sxs-lookup"><span data-stu-id="abed8-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="abed8-113">您可以將閘道安裝在與資料存放區相同或相異的 IaaS VM 上，只要閘道可以連線到資料庫即可。</span><span class="sxs-lookup"><span data-stu-id="abed8-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="abed8-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="abed8-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="abed8-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="abed8-115">Supported versions and installation</span></span>
<span data-ttu-id="abed8-116">若要讓資料管理閘道連接至 Sybase 資料庫，您必須在與資料管理閘道相同的系統上，安裝 [Sybase 的資料提供者 iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 或以上版本。</span><span class="sxs-lookup"><span data-stu-id="abed8-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="abed8-117">支援 Sybase 版本 16 和以上版本。</span><span class="sxs-lookup"><span data-stu-id="abed8-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="abed8-118">開始使用</span><span class="sxs-lookup"><span data-stu-id="abed8-118">Getting started</span></span>
<span data-ttu-id="abed8-119">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="abed8-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="abed8-120">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="abed8-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="abed8-121">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="abed8-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="abed8-122">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="abed8-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="abed8-123">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="abed8-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="abed8-124">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="abed8-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="abed8-125">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="abed8-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="abed8-126">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="abed8-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="abed8-127">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="abed8-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="abed8-128">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="abed8-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="abed8-129">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="abed8-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="abed8-130">如需相關範例，其中含有用來從內部部署 Sybase 資料存放區複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 Sybase 複製到 Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="abed8-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="abed8-131">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 Sybase 資料存放區特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="abed8-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="abed8-132">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="abed8-132">Linked service properties</span></span>
<span data-ttu-id="abed8-133">下表提供 Sybase 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="abed8-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="abed8-134">屬性</span><span class="sxs-lookup"><span data-stu-id="abed8-134">Property</span></span> | <span data-ttu-id="abed8-135">說明</span><span class="sxs-lookup"><span data-stu-id="abed8-135">Description</span></span> | <span data-ttu-id="abed8-136">必要</span><span class="sxs-lookup"><span data-stu-id="abed8-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="abed8-137">類型</span><span class="sxs-lookup"><span data-stu-id="abed8-137">type</span></span> |<span data-ttu-id="abed8-138">類型屬性必須設為： **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="abed8-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="abed8-139">是</span><span class="sxs-lookup"><span data-stu-id="abed8-139">Yes</span></span> |
| <span data-ttu-id="abed8-140">伺服器</span><span class="sxs-lookup"><span data-stu-id="abed8-140">server</span></span> |<span data-ttu-id="abed8-141">Sybase 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="abed8-141">Name of the Sybase server.</span></span> |<span data-ttu-id="abed8-142">是</span><span class="sxs-lookup"><span data-stu-id="abed8-142">Yes</span></span> |
| <span data-ttu-id="abed8-143">資料庫</span><span class="sxs-lookup"><span data-stu-id="abed8-143">database</span></span> |<span data-ttu-id="abed8-144">Sybase 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="abed8-144">Name of the Sybase database.</span></span> |<span data-ttu-id="abed8-145">是</span><span class="sxs-lookup"><span data-stu-id="abed8-145">Yes</span></span> |
| <span data-ttu-id="abed8-146">結構描述</span><span class="sxs-lookup"><span data-stu-id="abed8-146">schema</span></span> |<span data-ttu-id="abed8-147">在資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="abed8-147">Name of the schema in the database.</span></span> |<span data-ttu-id="abed8-148">否</span><span class="sxs-lookup"><span data-stu-id="abed8-148">No</span></span> |
| <span data-ttu-id="abed8-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="abed8-149">authenticationType</span></span> |<span data-ttu-id="abed8-150">用來連接到 Sybase 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="abed8-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="abed8-151">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="abed8-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="abed8-152">是</span><span class="sxs-lookup"><span data-stu-id="abed8-152">Yes</span></span> |
| <span data-ttu-id="abed8-153">username</span><span class="sxs-lookup"><span data-stu-id="abed8-153">username</span></span> |<span data-ttu-id="abed8-154">如果您使用基本或 Windows 驗證，請指定使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="abed8-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="abed8-155">否</span><span class="sxs-lookup"><span data-stu-id="abed8-155">No</span></span> |
| <span data-ttu-id="abed8-156">password</span><span class="sxs-lookup"><span data-stu-id="abed8-156">password</span></span> |<span data-ttu-id="abed8-157">指定您為使用者名稱所指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="abed8-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="abed8-158">否</span><span class="sxs-lookup"><span data-stu-id="abed8-158">No</span></span> |
| <span data-ttu-id="abed8-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="abed8-159">gatewayName</span></span> |<span data-ttu-id="abed8-160">Data Factory 服務應該用來連接到內部部署 Sybase 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="abed8-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="abed8-161">是</span><span class="sxs-lookup"><span data-stu-id="abed8-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="abed8-162">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="abed8-162">Dataset properties</span></span>
<span data-ttu-id="abed8-163">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="abed8-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="abed8-164">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="abed8-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="abed8-165">每個資料集類型的 typeProperties 區段都不同，可提供資料存放區中資料的位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abed8-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="abed8-166">**RelationalTable** 資料集類型的 **typeProperties** 區段 (包含 Sybase 資料集) 具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="abed8-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="abed8-167">屬性</span><span class="sxs-lookup"><span data-stu-id="abed8-167">Property</span></span> | <span data-ttu-id="abed8-168">說明</span><span class="sxs-lookup"><span data-stu-id="abed8-168">Description</span></span> | <span data-ttu-id="abed8-169">必要</span><span class="sxs-lookup"><span data-stu-id="abed8-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="abed8-170">tableName</span><span class="sxs-lookup"><span data-stu-id="abed8-170">tableName</span></span> |<span data-ttu-id="abed8-171">Sybase 資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="abed8-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="abed8-172">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="abed8-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="abed8-173">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="abed8-173">Copy activity properties</span></span>
<span data-ttu-id="abed8-174">如需可用來定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="abed8-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="abed8-175">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="abed8-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="abed8-176">而活動的 typeProperties 區段中可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="abed8-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="abed8-177">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="abed8-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="abed8-178">當來源的類型為 **RelationalSource** (包括 Sybase) 時，**typeProperties** 區段中會有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="abed8-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="abed8-179">屬性</span><span class="sxs-lookup"><span data-stu-id="abed8-179">Property</span></span> | <span data-ttu-id="abed8-180">說明</span><span class="sxs-lookup"><span data-stu-id="abed8-180">Description</span></span> | <span data-ttu-id="abed8-181">允許的值</span><span class="sxs-lookup"><span data-stu-id="abed8-181">Allowed values</span></span> | <span data-ttu-id="abed8-182">必要</span><span class="sxs-lookup"><span data-stu-id="abed8-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="abed8-183">query</span><span class="sxs-lookup"><span data-stu-id="abed8-183">query</span></span> |<span data-ttu-id="abed8-184">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="abed8-184">Use the custom query to read data.</span></span> |<span data-ttu-id="abed8-185">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="abed8-185">SQL query string.</span></span> <span data-ttu-id="abed8-186">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="abed8-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="abed8-187">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="abed8-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="abed8-188">JSON 範例：將資料從 Sybase 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="abed8-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="abed8-189">下列範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="abed8-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="abed8-190">這些範例示範如何將資料從 Sybase 資料庫複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="abed8-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="abed8-191">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="abed8-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="abed8-192">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="abed8-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="abed8-193">[OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="abed8-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="abed8-194">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="abed8-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="abed8-195">[RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="abed8-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="abed8-196">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="abed8-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="abed8-197">具有使用 [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="abed8-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="abed8-198">此範例會每個小時將資料從 Sybase 資料庫中的查詢結果複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="abed8-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="abed8-199">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="abed8-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="abed8-200">第一步是設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="abed8-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="abed8-201">如需相關指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="abed8-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="abed8-202">**Sybase 連結服務：**</span><span class="sxs-lookup"><span data-stu-id="abed8-202">**Sybase linked service:**</span></span>

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

<span data-ttu-id="abed8-203">**Azure Blob 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="abed8-203">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="abed8-204">**Sybase 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="abed8-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="abed8-205">此範例假設您已在 Sybase 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestamp")。</span><span class="sxs-lookup"><span data-stu-id="abed8-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="abed8-206">設定 “external”: true 可讓 Data Factory 服務知道此資料集是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="abed8-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="abed8-207">請注意，連結服務的**類型**需設為：**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="abed8-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

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

<span data-ttu-id="abed8-208">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="abed8-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="abed8-209">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="abed8-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="abed8-210">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="abed8-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="abed8-211">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="abed8-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="abed8-212">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="abed8-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="abed8-213">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="abed8-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="abed8-214">在管線 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="abed8-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="abed8-215">針對 **query** 屬性指定的 SQL 查詢會從資料庫中的 DBA.Orders 資料表選取資料。</span><span class="sxs-lookup"><span data-stu-id="abed8-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

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

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="abed8-216">Sybase 的類型對應</span><span class="sxs-lookup"><span data-stu-id="abed8-216">Type mapping for Sybase</span></span>
<span data-ttu-id="abed8-217">如同 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，「複製活動」會藉由含有下列 2 個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="abed8-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="abed8-218">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="abed8-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="abed8-219">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="abed8-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="abed8-220">Sybase 支援 T-SQL 和 T-SQL 類型。</span><span class="sxs-lookup"><span data-stu-id="abed8-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="abed8-221">如需從 sql 類型到.NET 類型的對應資料表，請參閱 [Azure SQL 連接器](data-factory-azure-sql-connector.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="abed8-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="abed8-222">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="abed8-222">Map source to sink columns</span></span>
<span data-ttu-id="abed8-223">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="abed8-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="abed8-224">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="abed8-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="abed8-225">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="abed8-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="abed8-226">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="abed8-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="abed8-227">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="abed8-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="abed8-228">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="abed8-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="abed8-229">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="abed8-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="abed8-230">效能和微調</span><span class="sxs-lookup"><span data-stu-id="abed8-230">Performance and Tuning</span></span>
<span data-ttu-id="abed8-231">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="abed8-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
