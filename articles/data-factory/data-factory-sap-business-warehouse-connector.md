---
title: "使用 Azure Data Factory 從 SAP Business Warehouse 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 從 SAP Business Warehouse 移動資料。"
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
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="c5c40-103">使用 Azure Data Factory 從 SAP Business Warehouse 移動資料</span><span class="sxs-lookup"><span data-stu-id="c5c40-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="c5c40-104">本文說明如何使用 Azure Data Factory 中的「複製活動」，從內部部署的 SAP Business Warehouse (BW) 移動資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="c5c40-105">本文是根據[資料移動活動](data-factory-data-movement-activities.md)一文，該文提供使用複製活動來移動資料的一般概觀。</span><span class="sxs-lookup"><span data-stu-id="c5c40-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c5c40-106">您可以將資料從內部部署的 SAP Business Warehouse 資料存放區複製到任何支援的接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="c5c40-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="c5c40-107">如需複製活動所支援作為接收器的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)表格。</span><span class="sxs-lookup"><span data-stu-id="c5c40-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c5c40-108">Data Factory 目前只支援將資料從 SAP Business Warehouse 移到其他資料存放區，而不支援將資料從其他資料存放區移到 SAP Business Warehouse。</span><span class="sxs-lookup"><span data-stu-id="c5c40-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="c5c40-109">支援的版本和安裝</span><span class="sxs-lookup"><span data-stu-id="c5c40-109">Supported versions and installation</span></span>
<span data-ttu-id="c5c40-110">此連接器支援 SAP Business Warehouse 7.x 版。</span><span class="sxs-lookup"><span data-stu-id="c5c40-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="c5c40-111">它支援使用 MDX 查詢從 Infocube 和 QueryCubes (包括 BEx 查詢) 複製資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="c5c40-112">若要啟用 SAP BW 執行個體的連線，請安裝下列元件︰</span><span class="sxs-lookup"><span data-stu-id="c5c40-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="c5c40-113">**資料管理閘道**：資料處理站服務支援使用稱為資料管理閘道的元件，以連線至內部部署資料存放區 (包括 SAP Business Warehouse)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="c5c40-114">若要了解資料管理閘道和設定閘道的逐步指示，請參閱[在內部部署資料存放區和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)一文。</span><span class="sxs-lookup"><span data-stu-id="c5c40-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="c5c40-115">即使 SAP Business Warehouse 裝載於 Azure IaaS 虛擬機器 (VM) 中，也需要有閘道器。</span><span class="sxs-lookup"><span data-stu-id="c5c40-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="c5c40-116">您可以將閘道安裝在與資料存放區相同或相異的 VM 上，只要閘道可以連線到資料庫即可。</span><span class="sxs-lookup"><span data-stu-id="c5c40-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="c5c40-117">閘道電腦上的 **SAP NetWeaver 程式庫**。</span><span class="sxs-lookup"><span data-stu-id="c5c40-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="c5c40-118">您可以從 SAP 系統管理員那裡取得 SAP Netweaver 程式庫，或直接從 [SAP 軟體下載中心](https://support.sap.com/swdc)取得。</span><span class="sxs-lookup"><span data-stu-id="c5c40-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="c5c40-119">搜尋 **SAP 附註 #1025361** 以取得最新版本的下載位置。</span><span class="sxs-lookup"><span data-stu-id="c5c40-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="c5c40-120">請確定 SAP NetWeaver 程式庫 (32 位元或 64 位元) 的架構符合您的閘道器安裝。</span><span class="sxs-lookup"><span data-stu-id="c5c40-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="c5c40-121">然後根據 SAP 附註，安裝 SAP NetWeaver RFC SDK 中包含的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="c5c40-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="c5c40-122">SAP NetWeaver 程式庫也隨附於 SAP 用戶端工具安裝。</span><span class="sxs-lookup"><span data-stu-id="c5c40-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="c5c40-123">將從 NetWeaver RFC SDK 解壓縮的 dlls 放至 system32 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c5c40-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c5c40-124">開始使用</span><span class="sxs-lookup"><span data-stu-id="c5c40-124">Getting started</span></span>
<span data-ttu-id="c5c40-125">您可以藉由使用不同的工具/API，建立內含複製活動的管線，以從內部部署的 Cassandra 資料存放區移動資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="c5c40-126">建立管線的最簡單方式就是使用「複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="c5c40-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c5c40-127">如需使用複製資料精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md) 。</span><span class="sxs-lookup"><span data-stu-id="c5c40-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="c5c40-128">您也可以使用下列工具來建立管線︰**Azure 入口網站**、**Visual Studio**、**Azure PowerShell**、**Azure Resource Manager 範本**、**.NET API** 及 **REST API**。</span><span class="sxs-lookup"><span data-stu-id="c5c40-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c5c40-129">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c5c40-130">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="c5c40-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c5c40-131">建立**連結服務**，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="c5c40-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c5c40-132">建立**資料集**，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c5c40-133">建立**管線**，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="c5c40-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c5c40-134">使用精靈時，精靈會自動為您建立這些 Data Factory 實體 (已連結的服務、資料集及管線) 的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="c5c40-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c5c40-135">使用工具/API (.NET API 除外) 時，您需使用 JSON 格式來定義這些 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="c5c40-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c5c40-136">如需相關範例，其中含有用來從內部部署 SAP Business Warehouse 複製資料之 Data Factory 實體的 JSON 定義，請參閱本文的 [JSON 範例：將資料從 SAP Business Warehouse 複製到 Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) 一節。</span><span class="sxs-lookup"><span data-stu-id="c5c40-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c5c40-137">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 SAP BW 資料存放區特定的 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="c5c40-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c5c40-138">連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="c5c40-138">Linked service properties</span></span>
<span data-ttu-id="c5c40-139">下表提供 SAP Business Warehouse (BW) 連結服務專屬 JSON 元素的描述。</span><span class="sxs-lookup"><span data-stu-id="c5c40-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="c5c40-140">屬性</span><span class="sxs-lookup"><span data-stu-id="c5c40-140">Property</span></span> | <span data-ttu-id="c5c40-141">說明</span><span class="sxs-lookup"><span data-stu-id="c5c40-141">Description</span></span> | <span data-ttu-id="c5c40-142">允許的值</span><span class="sxs-lookup"><span data-stu-id="c5c40-142">Allowed values</span></span> | <span data-ttu-id="c5c40-143">必要</span><span class="sxs-lookup"><span data-stu-id="c5c40-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="c5c40-144">伺服器</span><span class="sxs-lookup"><span data-stu-id="c5c40-144">server</span></span> | <span data-ttu-id="c5c40-145">SAP BW 執行個體所在之伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="c5c40-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="c5c40-146">字串</span><span class="sxs-lookup"><span data-stu-id="c5c40-146">string</span></span> | <span data-ttu-id="c5c40-147">是</span><span class="sxs-lookup"><span data-stu-id="c5c40-147">Yes</span></span>
<span data-ttu-id="c5c40-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="c5c40-148">systemNumber</span></span> | <span data-ttu-id="c5c40-149">SAP BW 系統的系統編號。</span><span class="sxs-lookup"><span data-stu-id="c5c40-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="c5c40-150">以字串表示的二位數十進位數字。</span><span class="sxs-lookup"><span data-stu-id="c5c40-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="c5c40-151">是</span><span class="sxs-lookup"><span data-stu-id="c5c40-151">Yes</span></span>
<span data-ttu-id="c5c40-152">clientId</span><span class="sxs-lookup"><span data-stu-id="c5c40-152">clientId</span></span> | <span data-ttu-id="c5c40-153">SAP W 系統中用戶端的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="c5c40-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="c5c40-154">以字串表示的三位數十進位數字。</span><span class="sxs-lookup"><span data-stu-id="c5c40-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="c5c40-155">是</span><span class="sxs-lookup"><span data-stu-id="c5c40-155">Yes</span></span>
<span data-ttu-id="c5c40-156">username</span><span class="sxs-lookup"><span data-stu-id="c5c40-156">username</span></span> | <span data-ttu-id="c5c40-157">具有 SAP 伺服器存取權之使用者的名稱</span><span class="sxs-lookup"><span data-stu-id="c5c40-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="c5c40-158">字串</span><span class="sxs-lookup"><span data-stu-id="c5c40-158">string</span></span> | <span data-ttu-id="c5c40-159">是</span><span class="sxs-lookup"><span data-stu-id="c5c40-159">Yes</span></span>
<span data-ttu-id="c5c40-160">password</span><span class="sxs-lookup"><span data-stu-id="c5c40-160">password</span></span> | <span data-ttu-id="c5c40-161">使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="c5c40-161">Password for the user.</span></span> | <span data-ttu-id="c5c40-162">字串</span><span class="sxs-lookup"><span data-stu-id="c5c40-162">string</span></span> | <span data-ttu-id="c5c40-163">是</span><span class="sxs-lookup"><span data-stu-id="c5c40-163">Yes</span></span>
<span data-ttu-id="c5c40-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c5c40-164">gatewayName</span></span> | <span data-ttu-id="c5c40-165">資料處理站服務應該用來連線至內部部署 SAP BW 執行個體的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="c5c40-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="c5c40-166">字串</span><span class="sxs-lookup"><span data-stu-id="c5c40-166">string</span></span> | <span data-ttu-id="c5c40-167">是</span><span class="sxs-lookup"><span data-stu-id="c5c40-167">Yes</span></span>
<span data-ttu-id="c5c40-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c5c40-168">encryptedCredential</span></span> | <span data-ttu-id="c5c40-169">加密的認證字串。</span><span class="sxs-lookup"><span data-stu-id="c5c40-169">The encrypted credential string.</span></span> | <span data-ttu-id="c5c40-170">string</span><span class="sxs-lookup"><span data-stu-id="c5c40-170">string</span></span> | <span data-ttu-id="c5c40-171">否</span><span class="sxs-lookup"><span data-stu-id="c5c40-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="c5c40-172">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="c5c40-172">Dataset properties</span></span>
<span data-ttu-id="c5c40-173">如需定義資料集的區段和屬性完整清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="c5c40-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c5c40-174">資料集 JSON 的結構、可用性和原則等區段類似於所有的資料集類型 (SQL Azure、Azure Blob、Azure 資料表等)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c5c40-175">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="c5c40-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c5c40-176">**RelationalTable** 類型的 SAP BW 資料集不支援類型專用的屬性。</span><span class="sxs-lookup"><span data-stu-id="c5c40-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="c5c40-177">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="c5c40-177">Copy activity properties</span></span>
<span data-ttu-id="c5c40-178">如需定義活動的區段和屬性完整清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="c5c40-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c5c40-179">屬性 (例如名稱、描述、輸入和輸出資料表，以及原則) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="c5c40-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="c5c40-180">而活動的 **typeProperties** 區段中，可用的屬性會隨著每個活動類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="c5c40-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="c5c40-181">就「複製活動」而言，這些屬性會根據來源和接收器的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="c5c40-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c5c40-182">當複製活動中的來源類型為 **RelationalSource** 時 (包括 SAP BW)，typeProperties 區段中會有下列屬性可用：</span><span class="sxs-lookup"><span data-stu-id="c5c40-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c5c40-183">屬性</span><span class="sxs-lookup"><span data-stu-id="c5c40-183">Property</span></span> | <span data-ttu-id="c5c40-184">說明</span><span class="sxs-lookup"><span data-stu-id="c5c40-184">Description</span></span> | <span data-ttu-id="c5c40-185">允許的值</span><span class="sxs-lookup"><span data-stu-id="c5c40-185">Allowed values</span></span> | <span data-ttu-id="c5c40-186">必要</span><span class="sxs-lookup"><span data-stu-id="c5c40-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c5c40-187">query</span><span class="sxs-lookup"><span data-stu-id="c5c40-187">query</span></span> | <span data-ttu-id="c5c40-188">指定 MDX 查詢從 SAP BW 執行個體讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="c5c40-189">MDX 查詢。</span><span class="sxs-lookup"><span data-stu-id="c5c40-189">MDX query.</span></span> | <span data-ttu-id="c5c40-190">是</span><span class="sxs-lookup"><span data-stu-id="c5c40-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="c5c40-191">JSON 範例：將資料從 SAP Business Warehouse 複製到 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="c5c40-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="c5c40-192">下列範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="c5c40-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c5c40-193">此範例示範如何將資料從內部部署 SAP Business Warehouse 複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c5c40-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="c5c40-194">不過，您可以在 Azure Data Factory 中使用複製活動， **直接** 將資料複製到 [這裡](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 所說的任何接收器。</span><span class="sxs-lookup"><span data-stu-id="c5c40-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c5c40-195">此範例提供 JSON 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="c5c40-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="c5c40-196">其中並不包含建立 Data Factory 的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="c5c40-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="c5c40-197">如需逐步指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="c5c40-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="c5c40-198">此範例具有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="c5c40-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="c5c40-199">[SapBw](#linked-service-properties) 類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="c5c40-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="c5c40-200">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)類型的連結服務。</span><span class="sxs-lookup"><span data-stu-id="c5c40-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c5c40-201">[RelationalTable](#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="c5c40-202">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c5c40-203">具有使用 [RelationalSource](#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 之複製活動的[管線](data-factory-create-pipelines.md)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c5c40-204">範例會每小時將資料從 SAP Business Warehouse 執行個體複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="c5c40-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="c5c40-205">範例後面的各節會說明這些範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="c5c40-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c5c40-206">第一步是設定資料管理閘道。</span><span class="sxs-lookup"><span data-stu-id="c5c40-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="c5c40-207">如需相關指示，請參閱 [在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 。</span><span class="sxs-lookup"><span data-stu-id="c5c40-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="c5c40-208">SAP Business Warehouse 連結服務</span><span class="sxs-lookup"><span data-stu-id="c5c40-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="c5c40-209">此連結服務會將您的 SAP BW 執行個體連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="c5c40-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="c5c40-210">Type 屬性設為 **SapBw**。</span><span class="sxs-lookup"><span data-stu-id="c5c40-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="c5c40-211">typeProperties 區段提供 SAP BW 執行個體的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="c5c40-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="c5c40-212">Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="c5c40-212">Azure Storage linked service</span></span>
<span data-ttu-id="c5c40-213">此連結服務會將您的 Azure 儲存體帳戶連結至資料處理站。</span><span class="sxs-lookup"><span data-stu-id="c5c40-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="c5c40-214">Type 屬性設為 **AzureStorage**。</span><span class="sxs-lookup"><span data-stu-id="c5c40-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="c5c40-215">typeProperties 區段提供 Azure 儲存體帳戶的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="c5c40-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="c5c40-216">SAP BW 輸入資料集</span><span class="sxs-lookup"><span data-stu-id="c5c40-216">SAP BW input dataset</span></span>
<span data-ttu-id="c5c40-217">此資料集定義 SAP Business Warehouse 資料集。</span><span class="sxs-lookup"><span data-stu-id="c5c40-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="c5c40-218">將資料處理站資料集的類型設定為 **RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="c5c40-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="c5c40-219">目前，您未指定 SAP BW 資料集的任何類型特定屬性。</span><span class="sxs-lookup"><span data-stu-id="c5c40-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="c5c40-220">複製活動定義中的查詢指定要從 SAP BW 執行個體讀取的資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="c5c40-221">將 external 屬性設定為 true 會通知 Data Factory 服務，指出資料表是在資料處理站外部，不是由資料處理站中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="c5c40-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="c5c40-222">頻率和間隔屬性會定義排程。</span><span class="sxs-lookup"><span data-stu-id="c5c40-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="c5c40-223">在此案例中，每小時會從 SAP BW 執行個體讀取資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c5c40-224">Azure Blob 輸出資料集</span><span class="sxs-lookup"><span data-stu-id="c5c40-224">Azure Blob output dataset</span></span>
<span data-ttu-id="c5c40-225">此資料集會定義輸出 Azure Blob 資料集。</span><span class="sxs-lookup"><span data-stu-id="c5c40-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="c5c40-226">Type 屬性設為 AzureBlob。</span><span class="sxs-lookup"><span data-stu-id="c5c40-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="c5c40-227">TypeProperties 區段提供從 SAP BW 執行個體複製的資料要儲存在何處。</span><span class="sxs-lookup"><span data-stu-id="c5c40-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="c5c40-228">資料會每小時寫入新的 blob (頻率：小時，間隔：1)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c5c40-229">根據正在處理之配量的開始時間，以動態方式評估 Blob 的資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="c5c40-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c5c40-230">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="c5c40-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="c5c40-231">具有複製活動的管線</span><span class="sxs-lookup"><span data-stu-id="c5c40-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="c5c40-232">此管線包含複製活動，該活動已設定為使用輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="c5c40-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="c5c40-233">在管線 JSON 定義中，**source** 類型設為 **RelationalSource** (適用於 SAP BW 來源)，**sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="c5c40-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c5c40-234">針對 **query** 屬性指定的查詢會選取過去一小時內要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="c5c40-235">SAP BW 的類型對應</span><span class="sxs-lookup"><span data-stu-id="c5c40-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="c5c40-236">如 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會藉由下列含有兩個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="c5c40-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="c5c40-237">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="c5c40-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="c5c40-238">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="c5c40-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="c5c40-239">從 SAP BW 移動資料時，SAP BW 類型至 .NET 類型會使用下列對應。</span><span class="sxs-lookup"><span data-stu-id="c5c40-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="c5c40-240">ABAP 字典中的資料類型</span><span class="sxs-lookup"><span data-stu-id="c5c40-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="c5c40-241">.Net 資料類型</span><span class="sxs-lookup"><span data-stu-id="c5c40-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="c5c40-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="c5c40-242">ACCP</span></span> |  <span data-ttu-id="c5c40-243">int</span><span class="sxs-lookup"><span data-stu-id="c5c40-243">Int</span></span>
<span data-ttu-id="c5c40-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="c5c40-244">CHAR</span></span> | <span data-ttu-id="c5c40-245">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-245">String</span></span>
<span data-ttu-id="c5c40-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="c5c40-246">CLNT</span></span> | <span data-ttu-id="c5c40-247">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-247">String</span></span>
<span data-ttu-id="c5c40-248">CURR</span><span class="sxs-lookup"><span data-stu-id="c5c40-248">CURR</span></span> | <span data-ttu-id="c5c40-249">十進位</span><span class="sxs-lookup"><span data-stu-id="c5c40-249">Decimal</span></span>
<span data-ttu-id="c5c40-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="c5c40-250">CUKY</span></span> | <span data-ttu-id="c5c40-251">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-251">String</span></span>
<span data-ttu-id="c5c40-252">DEC</span><span class="sxs-lookup"><span data-stu-id="c5c40-252">DEC</span></span> | <span data-ttu-id="c5c40-253">十進位</span><span class="sxs-lookup"><span data-stu-id="c5c40-253">Decimal</span></span>
<span data-ttu-id="c5c40-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="c5c40-254">FLTP</span></span> | <span data-ttu-id="c5c40-255">兩倍</span><span class="sxs-lookup"><span data-stu-id="c5c40-255">Double</span></span>
<span data-ttu-id="c5c40-256">INT1</span><span class="sxs-lookup"><span data-stu-id="c5c40-256">INT1</span></span> | <span data-ttu-id="c5c40-257">位元組</span><span class="sxs-lookup"><span data-stu-id="c5c40-257">Byte</span></span>
<span data-ttu-id="c5c40-258">INT2</span><span class="sxs-lookup"><span data-stu-id="c5c40-258">INT2</span></span> | <span data-ttu-id="c5c40-259">Int16</span><span class="sxs-lookup"><span data-stu-id="c5c40-259">Int16</span></span>
<span data-ttu-id="c5c40-260">INT4</span><span class="sxs-lookup"><span data-stu-id="c5c40-260">INT4</span></span> | <span data-ttu-id="c5c40-261">int</span><span class="sxs-lookup"><span data-stu-id="c5c40-261">Int</span></span>
<span data-ttu-id="c5c40-262">LANG</span><span class="sxs-lookup"><span data-stu-id="c5c40-262">LANG</span></span> | <span data-ttu-id="c5c40-263">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-263">String</span></span>
<span data-ttu-id="c5c40-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="c5c40-264">LCHR</span></span> | <span data-ttu-id="c5c40-265">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-265">String</span></span>
<span data-ttu-id="c5c40-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="c5c40-266">LRAW</span></span> | <span data-ttu-id="c5c40-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c5c40-267">Byte[]</span></span>
<span data-ttu-id="c5c40-268">PREC</span><span class="sxs-lookup"><span data-stu-id="c5c40-268">PREC</span></span> | <span data-ttu-id="c5c40-269">Int16</span><span class="sxs-lookup"><span data-stu-id="c5c40-269">Int16</span></span>
<span data-ttu-id="c5c40-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="c5c40-270">QUAN</span></span> | <span data-ttu-id="c5c40-271">十進位</span><span class="sxs-lookup"><span data-stu-id="c5c40-271">Decimal</span></span>
<span data-ttu-id="c5c40-272">RAW</span><span class="sxs-lookup"><span data-stu-id="c5c40-272">RAW</span></span> | <span data-ttu-id="c5c40-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c5c40-273">Byte[]</span></span>
<span data-ttu-id="c5c40-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="c5c40-274">RAWSTRING</span></span> | <span data-ttu-id="c5c40-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="c5c40-275">Byte[]</span></span>
<span data-ttu-id="c5c40-276">STRING</span><span class="sxs-lookup"><span data-stu-id="c5c40-276">STRING</span></span> | <span data-ttu-id="c5c40-277">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-277">String</span></span>
<span data-ttu-id="c5c40-278">單位</span><span class="sxs-lookup"><span data-stu-id="c5c40-278">UNIT</span></span> | <span data-ttu-id="c5c40-279">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-279">String</span></span>
<span data-ttu-id="c5c40-280">DATS</span><span class="sxs-lookup"><span data-stu-id="c5c40-280">DATS</span></span> | <span data-ttu-id="c5c40-281">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-281">String</span></span>
<span data-ttu-id="c5c40-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="c5c40-282">NUMC</span></span> | <span data-ttu-id="c5c40-283">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-283">String</span></span>
<span data-ttu-id="c5c40-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="c5c40-284">TIMS</span></span> | <span data-ttu-id="c5c40-285">String</span><span class="sxs-lookup"><span data-stu-id="c5c40-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="c5c40-286">若要將來自來源資料集的資料行與來自接收資料集的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="c5c40-287">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="c5c40-287">Map source to sink columns</span></span>
<span data-ttu-id="c5c40-288">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="c5c40-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c5c40-289">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="c5c40-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="c5c40-290">從關聯式資料存放區複製資料時，請將可重複性謹記在心，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="c5c40-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c5c40-291">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="c5c40-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c5c40-292">您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="c5c40-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c5c40-293">以上述任一方式重新執行配量時，您必須確保不論將配量執行多少次，都會讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="c5c40-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c5c40-294">請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="c5c40-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c5c40-295">效能和微調</span><span class="sxs-lookup"><span data-stu-id="c5c40-295">Performance and Tuning</span></span>
<span data-ttu-id="c5c40-296">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)一文，以了解在 Azure Data Factory 中會影響資料移動 (複製活動) 效能的重要因素，以及各種最佳化的方法。</span><span class="sxs-lookup"><span data-stu-id="c5c40-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
