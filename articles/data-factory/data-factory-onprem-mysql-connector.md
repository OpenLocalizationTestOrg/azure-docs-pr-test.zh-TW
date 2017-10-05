---
title: "使用 Azure Data Factory 從 MySQL 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 MySQL Database 移動資料。"
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
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="84abf-103">使用 Azure Data Factory 從 MySQL 移動資料</span><span class="sxs-lookup"><span data-stu-id="84abf-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="84abf-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署的 MySQL 資料庫移動資料。</span><span class="sxs-lookup"><span data-stu-id="84abf-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="84abf-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="84abf-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="84abf-106">您可以將資料從內部部署的 MySQL 資料存放區複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="84abf-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="84abf-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="84abf-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="84abf-108">Data Factory 目前只支援將資料從 MySQL 資料存放區移到其他資料存放區，而不支援將資料從其他資料存放區移到 MySQL 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="84abf-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="84abf-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="84abf-109">Prerequisites</span></span>
<span data-ttu-id="84abf-110">Data Factory 服務支援使用資料管理閘道器連接至內部部署 MySQL 來源。</span><span class="sxs-lookup"><span data-stu-id="84abf-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="84abf-111">請參閱 [在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文來了解資料管理閘道和設定閘道的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="84abf-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="84abf-112">即使 MySQL 資料庫裝載於 Azure IaaS 虛擬機器 (VM) 中，也必須要有閘道。</span><span class="sxs-lookup"><span data-stu-id="84abf-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="84abf-113">您可以將閘道安裝在與資料存放區相同或相異的 VM 上，只要閘道可以連線到資料庫即可。</span><span class="sxs-lookup"><span data-stu-id="84abf-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="84abf-114">如需連接/閘道器相關問題的疑難排解秘訣，請參閱 [針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 。</span><span class="sxs-lookup"><span data-stu-id="84abf-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="84abf-115">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="84abf-115">Supported versions and installation</span></span>
<span data-ttu-id="84abf-116">若要讓資料管理閘道連線至 MySQL 資料庫，您必須在與資料管理閘道相同的系統上，安裝 [MySQL 連接器/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (6.6.5 版或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="84abf-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="84abf-117">支援 MySQL 版本 5.1 和以上版本。</span><span class="sxs-lookup"><span data-stu-id="84abf-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="84abf-118">如果您遇到錯誤「驗證失敗，因為遠端合作對象已關閉傳輸串流」，請考慮將 MySQL 連接器/Net 更新為更高版本。</span><span class="sxs-lookup"><span data-stu-id="84abf-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="84abf-119">開始使用</span><span class="sxs-lookup"><span data-stu-id="84abf-119">Getting started</span></span>
<span data-ttu-id="84abf-120">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="84abf-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="84abf-121">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="84abf-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="84abf-122">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="84abf-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="84abf-123">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="84abf-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="84abf-124">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="84abf-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="84abf-125">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="84abf-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="84abf-126">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="84abf-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="84abf-127">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="84abf-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="84abf-128">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="84abf-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="84abf-129">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="84abf-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="84abf-130">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="84abf-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="84abf-131">如需相關範例，其中含有用來從內部部署 MySQL 資料存放區複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 MySQL 複製到 Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="84abf-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="84abf-132">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 MySQL 資料存放區特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="84abf-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="84abf-133">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="84abf-133">Linked service properties</span></span>
<span data-ttu-id="84abf-134">下表提供 MySQL 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="84abf-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="84abf-135">屬性</span><span class="sxs-lookup"><span data-stu-id="84abf-135">Property</span></span> | <span data-ttu-id="84abf-136">說明</span><span class="sxs-lookup"><span data-stu-id="84abf-136">Description</span></span> | <span data-ttu-id="84abf-137">必要</span><span class="sxs-lookup"><span data-stu-id="84abf-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84abf-138">類型</span><span class="sxs-lookup"><span data-stu-id="84abf-138">type</span></span> |<span data-ttu-id="84abf-139">類型屬性必須設為： **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="84abf-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="84abf-140">是</span><span class="sxs-lookup"><span data-stu-id="84abf-140">Yes</span></span> |
| <span data-ttu-id="84abf-141">伺服器</span><span class="sxs-lookup"><span data-stu-id="84abf-141">server</span></span> |<span data-ttu-id="84abf-142">MySQL 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="84abf-142">Name of the MySQL server.</span></span> |<span data-ttu-id="84abf-143">是</span><span class="sxs-lookup"><span data-stu-id="84abf-143">Yes</span></span> |
| <span data-ttu-id="84abf-144">資料庫</span><span class="sxs-lookup"><span data-stu-id="84abf-144">database</span></span> |<span data-ttu-id="84abf-145">MySQL 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="84abf-145">Name of the MySQL database.</span></span> |<span data-ttu-id="84abf-146">是</span><span class="sxs-lookup"><span data-stu-id="84abf-146">Yes</span></span> |
| <span data-ttu-id="84abf-147">結構描述</span><span class="sxs-lookup"><span data-stu-id="84abf-147">schema</span></span> |<span data-ttu-id="84abf-148">在資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="84abf-148">Name of the schema in the database.</span></span> |<span data-ttu-id="84abf-149">否</span><span class="sxs-lookup"><span data-stu-id="84abf-149">No</span></span> |
| <span data-ttu-id="84abf-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="84abf-150">authenticationType</span></span> |<span data-ttu-id="84abf-151">用來連接到 MySQL 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="84abf-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="84abf-152">可能的值為：`Basic`。</span><span class="sxs-lookup"><span data-stu-id="84abf-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="84abf-153">是</span><span class="sxs-lookup"><span data-stu-id="84abf-153">Yes</span></span> |
| <span data-ttu-id="84abf-154">username</span><span class="sxs-lookup"><span data-stu-id="84abf-154">username</span></span> |<span data-ttu-id="84abf-155">指定要連線到 MySQL 資料庫的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="84abf-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="84abf-156">是</span><span class="sxs-lookup"><span data-stu-id="84abf-156">Yes</span></span> |
| <span data-ttu-id="84abf-157">password</span><span class="sxs-lookup"><span data-stu-id="84abf-157">password</span></span> |<span data-ttu-id="84abf-158">指定您所指定使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="84abf-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="84abf-159">是</span><span class="sxs-lookup"><span data-stu-id="84abf-159">Yes</span></span> |
| <span data-ttu-id="84abf-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="84abf-160">gatewayName</span></span> |<span data-ttu-id="84abf-161">Data Factory 服務應該用來連接到內部部署 MySQL 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="84abf-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="84abf-162">是</span><span class="sxs-lookup"><span data-stu-id="84abf-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="84abf-163">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="84abf-163">Dataset properties</span></span>
<span data-ttu-id="84abf-164">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="84abf-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="84abf-165">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="84abf-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="84abf-166">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="84abf-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="84abf-167">**RelationalTable** 資料集類型的 typeProperties 區段 (包含 MySQL 資料集) 具有下列屬性</span><span class="sxs-lookup"><span data-stu-id="84abf-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="84abf-168">屬性</span><span class="sxs-lookup"><span data-stu-id="84abf-168">Property</span></span> | <span data-ttu-id="84abf-169">說明</span><span class="sxs-lookup"><span data-stu-id="84abf-169">Description</span></span> | <span data-ttu-id="84abf-170">必要</span><span class="sxs-lookup"><span data-stu-id="84abf-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84abf-171">tableName</span><span class="sxs-lookup"><span data-stu-id="84abf-171">tableName</span></span> |<span data-ttu-id="84abf-172">MySQL 資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="84abf-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="84abf-173">否 (如果已指定 **RelationalSource** 的 **query**)</span><span class="sxs-lookup"><span data-stu-id="84abf-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="84abf-174">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="84abf-174">Copy activity properties</span></span>
<span data-ttu-id="84abf-175">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="84abf-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="84abf-176">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="84abf-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="84abf-177">而活動的 **typeProperties** 區段中，可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="84abf-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="84abf-178">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="84abf-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="84abf-179">當複製活動中的來源類型為 **RelationalSource** (包括 MySQL) 時，typeProperties 區段中會有下列可用屬性：</span><span class="sxs-lookup"><span data-stu-id="84abf-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="84abf-180">屬性</span><span class="sxs-lookup"><span data-stu-id="84abf-180">Property</span></span> | <span data-ttu-id="84abf-181">說明</span><span class="sxs-lookup"><span data-stu-id="84abf-181">Description</span></span> | <span data-ttu-id="84abf-182">允許的值</span><span class="sxs-lookup"><span data-stu-id="84abf-182">Allowed values</span></span> | <span data-ttu-id="84abf-183">必要</span><span class="sxs-lookup"><span data-stu-id="84abf-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="84abf-184">query</span><span class="sxs-lookup"><span data-stu-id="84abf-184">query</span></span> |<span data-ttu-id="84abf-185">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="84abf-185">Use the custom query to read data.</span></span> |<span data-ttu-id="84abf-186">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="84abf-186">SQL query string.</span></span> <span data-ttu-id="84abf-187">例如：select * from MyTable。</span><span class="sxs-lookup"><span data-stu-id="84abf-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="84abf-188">否 (如果已指定 **dataset** 的 **tableName**)</span><span class="sxs-lookup"><span data-stu-id="84abf-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="84abf-189">JSON 範例：將資料從 MySQL 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="84abf-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="84abf-190">此範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="84abf-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="84abf-191">它示範如何將資料從內部部署的 MySQL 資料庫複製到「Azure Blob 儲存體」。</span><span class="sxs-lookup"><span data-stu-id="84abf-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="84abf-192">不過，您可以在 Azure Data Factory 中使用複製活動，將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="84abf-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84abf-193">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="84abf-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="84abf-194">其中並不包含建立 Data Factory 的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="84abf-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="84abf-195">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="84abf-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="84abf-196">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="84abf-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="84abf-197">[OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="84abf-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="84abf-198">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="84abf-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="84abf-199">[RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="84abf-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="84abf-200">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="84abf-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="84abf-201">具有使用 [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="84abf-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="84abf-202">此範例會每個小時將資料從 MySQL 資料庫中的查詢結果複製到 Blob。</span><span class="sxs-lookup"><span data-stu-id="84abf-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="84abf-203">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="84abf-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="84abf-204">第一步是設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="84abf-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="84abf-205">如需相關指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="84abf-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="84abf-206">**MySQL 已連結的服務：**</span><span class="sxs-lookup"><span data-stu-id="84abf-206">**MySQL linked service:**</span></span>

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

<span data-ttu-id="84abf-207">**Azure 儲存體連結服務：**</span><span class="sxs-lookup"><span data-stu-id="84abf-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="84abf-208">**MySQL 輸入資料集：**</span><span class="sxs-lookup"><span data-stu-id="84abf-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="84abf-209">此範例假設您已在 MySQL 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestampcolumn")。</span><span class="sxs-lookup"><span data-stu-id="84abf-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="84abf-210">設定 “external”: ”true” 可讓 Data Factory 服務知道資料表是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="84abf-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="84abf-211">**Azure Blob 輸出資料集：**</span><span class="sxs-lookup"><span data-stu-id="84abf-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="84abf-212">資料會每小時寫入至新的 Blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="84abf-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="84abf-213">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="84abf-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="84abf-214">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="84abf-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="84abf-215">**具有複製活動的管線：**</span><span class="sxs-lookup"><span data-stu-id="84abf-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="84abf-216">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="84abf-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="84abf-217">在管線 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="84abf-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="84abf-218">針對 **query** 屬性指定的 SQL 查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="84abf-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="84abf-219">MySQL 的類型對應</span><span class="sxs-lookup"><span data-stu-id="84abf-219">Type mapping for MySQL</span></span>
<span data-ttu-id="84abf-220">如 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會藉由下列含有兩個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="84abf-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="84abf-221">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="84abf-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="84abf-222">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="84abf-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="84abf-223">將資料移到 MySQL 時，會使用下列從 MySQL 類型到 .NET 類型的對應。</span><span class="sxs-lookup"><span data-stu-id="84abf-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="84abf-224">MySQL 資料庫類型</span><span class="sxs-lookup"><span data-stu-id="84abf-224">MySQL Database type</span></span> | <span data-ttu-id="84abf-225">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="84abf-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="84abf-226">不帶正負號的 bigint</span><span class="sxs-lookup"><span data-stu-id="84abf-226">bigint unsigned</span></span> |<span data-ttu-id="84abf-227">十進位</span><span class="sxs-lookup"><span data-stu-id="84abf-227">Decimal</span></span> |
| <span data-ttu-id="84abf-228">bigint</span><span class="sxs-lookup"><span data-stu-id="84abf-228">bigint</span></span> |<span data-ttu-id="84abf-229">Int64</span><span class="sxs-lookup"><span data-stu-id="84abf-229">Int64</span></span> |
| <span data-ttu-id="84abf-230">bit</span><span class="sxs-lookup"><span data-stu-id="84abf-230">bit</span></span> |<span data-ttu-id="84abf-231">十進位</span><span class="sxs-lookup"><span data-stu-id="84abf-231">Decimal</span></span> |
| <span data-ttu-id="84abf-232">blob</span><span class="sxs-lookup"><span data-stu-id="84abf-232">blob</span></span> |<span data-ttu-id="84abf-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="84abf-233">Byte[]</span></span> |
| <span data-ttu-id="84abf-234">布林</span><span class="sxs-lookup"><span data-stu-id="84abf-234">bool</span></span> |<span data-ttu-id="84abf-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="84abf-235">Boolean</span></span> |
| <span data-ttu-id="84abf-236">char</span><span class="sxs-lookup"><span data-stu-id="84abf-236">char</span></span> |<span data-ttu-id="84abf-237">String</span><span class="sxs-lookup"><span data-stu-id="84abf-237">String</span></span> |
| <span data-ttu-id="84abf-238">日期</span><span class="sxs-lookup"><span data-stu-id="84abf-238">date</span></span> |<span data-ttu-id="84abf-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="84abf-239">Datetime</span></span> |
| <span data-ttu-id="84abf-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="84abf-240">datetime</span></span> |<span data-ttu-id="84abf-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="84abf-241">Datetime</span></span> |
| <span data-ttu-id="84abf-242">十進位</span><span class="sxs-lookup"><span data-stu-id="84abf-242">decimal</span></span> |<span data-ttu-id="84abf-243">十進位</span><span class="sxs-lookup"><span data-stu-id="84abf-243">Decimal</span></span> |
| <span data-ttu-id="84abf-244">雙精度</span><span class="sxs-lookup"><span data-stu-id="84abf-244">double precision</span></span> |<span data-ttu-id="84abf-245">兩倍</span><span class="sxs-lookup"><span data-stu-id="84abf-245">Double</span></span> |
| <span data-ttu-id="84abf-246">兩倍</span><span class="sxs-lookup"><span data-stu-id="84abf-246">double</span></span> |<span data-ttu-id="84abf-247">兩倍</span><span class="sxs-lookup"><span data-stu-id="84abf-247">Double</span></span> |
| <span data-ttu-id="84abf-248">列舉</span><span class="sxs-lookup"><span data-stu-id="84abf-248">enum</span></span> |<span data-ttu-id="84abf-249">String</span><span class="sxs-lookup"><span data-stu-id="84abf-249">String</span></span> |
| <span data-ttu-id="84abf-250">float</span><span class="sxs-lookup"><span data-stu-id="84abf-250">float</span></span> |<span data-ttu-id="84abf-251">單一</span><span class="sxs-lookup"><span data-stu-id="84abf-251">Single</span></span> |
| <span data-ttu-id="84abf-252">不帶正負號的 int</span><span class="sxs-lookup"><span data-stu-id="84abf-252">int unsigned</span></span> |<span data-ttu-id="84abf-253">Int64</span><span class="sxs-lookup"><span data-stu-id="84abf-253">Int64</span></span> |
| <span data-ttu-id="84abf-254">int</span><span class="sxs-lookup"><span data-stu-id="84abf-254">int</span></span> |<span data-ttu-id="84abf-255">Int32</span><span class="sxs-lookup"><span data-stu-id="84abf-255">Int32</span></span> |
| <span data-ttu-id="84abf-256">不帶正負號的整數</span><span class="sxs-lookup"><span data-stu-id="84abf-256">integer unsigned</span></span> |<span data-ttu-id="84abf-257">Int64</span><span class="sxs-lookup"><span data-stu-id="84abf-257">Int64</span></span> |
| <span data-ttu-id="84abf-258">integer</span><span class="sxs-lookup"><span data-stu-id="84abf-258">integer</span></span> |<span data-ttu-id="84abf-259">Int32</span><span class="sxs-lookup"><span data-stu-id="84abf-259">Int32</span></span> |
| <span data-ttu-id="84abf-260">長 varbinary</span><span class="sxs-lookup"><span data-stu-id="84abf-260">long varbinary</span></span> |<span data-ttu-id="84abf-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="84abf-261">Byte[]</span></span> |
| <span data-ttu-id="84abf-262">長 varchar</span><span class="sxs-lookup"><span data-stu-id="84abf-262">long varchar</span></span> |<span data-ttu-id="84abf-263">String</span><span class="sxs-lookup"><span data-stu-id="84abf-263">String</span></span> |
| <span data-ttu-id="84abf-264">longblob</span><span class="sxs-lookup"><span data-stu-id="84abf-264">longblob</span></span> |<span data-ttu-id="84abf-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="84abf-265">Byte[]</span></span> |
| <span data-ttu-id="84abf-266">longtext</span><span class="sxs-lookup"><span data-stu-id="84abf-266">longtext</span></span> |<span data-ttu-id="84abf-267">String</span><span class="sxs-lookup"><span data-stu-id="84abf-267">String</span></span> |
| <span data-ttu-id="84abf-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="84abf-268">mediumblob</span></span> |<span data-ttu-id="84abf-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="84abf-269">Byte[]</span></span> |
| <span data-ttu-id="84abf-270">不帶正負號的 mediumint</span><span class="sxs-lookup"><span data-stu-id="84abf-270">mediumint unsigned</span></span> |<span data-ttu-id="84abf-271">Int64</span><span class="sxs-lookup"><span data-stu-id="84abf-271">Int64</span></span> |
| <span data-ttu-id="84abf-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="84abf-272">mediumint</span></span> |<span data-ttu-id="84abf-273">Int32</span><span class="sxs-lookup"><span data-stu-id="84abf-273">Int32</span></span> |
| <span data-ttu-id="84abf-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="84abf-274">mediumtext</span></span> |<span data-ttu-id="84abf-275">String</span><span class="sxs-lookup"><span data-stu-id="84abf-275">String</span></span> |
| <span data-ttu-id="84abf-276">numeric</span><span class="sxs-lookup"><span data-stu-id="84abf-276">numeric</span></span> |<span data-ttu-id="84abf-277">十進位</span><span class="sxs-lookup"><span data-stu-id="84abf-277">Decimal</span></span> |
| <span data-ttu-id="84abf-278">real</span><span class="sxs-lookup"><span data-stu-id="84abf-278">real</span></span> |<span data-ttu-id="84abf-279">兩倍</span><span class="sxs-lookup"><span data-stu-id="84abf-279">Double</span></span> |
| <span data-ttu-id="84abf-280">set</span><span class="sxs-lookup"><span data-stu-id="84abf-280">set</span></span> |<span data-ttu-id="84abf-281">String</span><span class="sxs-lookup"><span data-stu-id="84abf-281">String</span></span> |
| <span data-ttu-id="84abf-282">不帶正負號的 smallint</span><span class="sxs-lookup"><span data-stu-id="84abf-282">smallint unsigned</span></span> |<span data-ttu-id="84abf-283">Int32</span><span class="sxs-lookup"><span data-stu-id="84abf-283">Int32</span></span> |
| <span data-ttu-id="84abf-284">smallint</span><span class="sxs-lookup"><span data-stu-id="84abf-284">smallint</span></span> |<span data-ttu-id="84abf-285">Int16</span><span class="sxs-lookup"><span data-stu-id="84abf-285">Int16</span></span> |
| <span data-ttu-id="84abf-286">文字</span><span class="sxs-lookup"><span data-stu-id="84abf-286">text</span></span> |<span data-ttu-id="84abf-287">String</span><span class="sxs-lookup"><span data-stu-id="84abf-287">String</span></span> |
| <span data-ttu-id="84abf-288">分析</span><span class="sxs-lookup"><span data-stu-id="84abf-288">time</span></span> |<span data-ttu-id="84abf-289">時間範圍</span><span class="sxs-lookup"><span data-stu-id="84abf-289">TimeSpan</span></span> |
| <span data-ttu-id="84abf-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="84abf-290">timestamp</span></span> |<span data-ttu-id="84abf-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="84abf-291">Datetime</span></span> |
| <span data-ttu-id="84abf-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="84abf-292">tinyblob</span></span> |<span data-ttu-id="84abf-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="84abf-293">Byte[]</span></span> |
| <span data-ttu-id="84abf-294">不帶正負號的 tinyint</span><span class="sxs-lookup"><span data-stu-id="84abf-294">tinyint unsigned</span></span> |<span data-ttu-id="84abf-295">Int16</span><span class="sxs-lookup"><span data-stu-id="84abf-295">Int16</span></span> |
| <span data-ttu-id="84abf-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="84abf-296">tinyint</span></span> |<span data-ttu-id="84abf-297">Int16</span><span class="sxs-lookup"><span data-stu-id="84abf-297">Int16</span></span> |
| <span data-ttu-id="84abf-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="84abf-298">tinytext</span></span> |<span data-ttu-id="84abf-299">String</span><span class="sxs-lookup"><span data-stu-id="84abf-299">String</span></span> |
| <span data-ttu-id="84abf-300">varchar</span><span class="sxs-lookup"><span data-stu-id="84abf-300">varchar</span></span> |<span data-ttu-id="84abf-301">String</span><span class="sxs-lookup"><span data-stu-id="84abf-301">String</span></span> |
| <span data-ttu-id="84abf-302">年</span><span class="sxs-lookup"><span data-stu-id="84abf-302">year</span></span> |<span data-ttu-id="84abf-303">int</span><span class="sxs-lookup"><span data-stu-id="84abf-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="84abf-304">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="84abf-304">Map source to sink columns</span></span>
<span data-ttu-id="84abf-305">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="84abf-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="84abf-306">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="84abf-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="84abf-307">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="84abf-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="84abf-308">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="84abf-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="84abf-309">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="84abf-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="84abf-310">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="84abf-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="84abf-311">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="84abf-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="84abf-312">效能和微調</span><span class="sxs-lookup"><span data-stu-id="84abf-312">Performance and Tuning</span></span>
<span data-ttu-id="84abf-313">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="84abf-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
