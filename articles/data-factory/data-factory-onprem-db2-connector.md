---
title: "使用 Azure Data Factory 從 DB2 移動資料 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 複製活動從內部部署 DB2 資料庫移動資料"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="7fd02-103">使用 Azure Data Factory 複製活動從 DB2 移動資料</span><span class="sxs-lookup"><span data-stu-id="7fd02-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="7fd02-104">本文將說明如何使用 Azure Data Factory 中的複製活動將內部部署 DB2 資料庫的資料複製到資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7fd02-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="7fd02-105">您可以將資料複製到在[Data Factory 資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)發行項中列為支援接收的任何存放區。</span><span class="sxs-lookup"><span data-stu-id="7fd02-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="7fd02-106">本文以「資料處理站」一文為基礎，該文呈現使用複製活動移動資料的概觀，並列出支援的資料存放區組合。</span><span class="sxs-lookup"><span data-stu-id="7fd02-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="7fd02-107">資料處理站目前僅支援資料從 DB2 資料庫移至[支援的接收資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="7fd02-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7fd02-108">不支援資料從其他資料存放區移至 DB2 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7fd02-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fd02-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="7fd02-109">Prerequisites</span></span>
<span data-ttu-id="7fd02-110">資料處理站支援使用[資料管理閘道](data-factory-data-management-gateway.md)連接至內部部署 DB2 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7fd02-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="7fd02-111">如需有關設定閘道資料管線來移動資料的逐步指示，請參閱[將資料從內部部署移到雲端](data-factory-move-data-between-onprem-and-cloud.md)一文。</span><span class="sxs-lookup"><span data-stu-id="7fd02-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="7fd02-112">即使 DB2 裝載於 Azure IaaS VM 中，也必須要有閘道。</span><span class="sxs-lookup"><span data-stu-id="7fd02-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="7fd02-113">您可以在資料存放區所在的 IaaS VM 上安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="7fd02-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="7fd02-114">如果閘道可以連線到資料庫，您可以在不同的 VM 上安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="7fd02-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="7fd02-115">資料管理閘道提供內建的 DB2 驅動程式，因此，不需要手動安裝任何驅動程式，即可從 DB2 複製資料。</span><span class="sxs-lookup"><span data-stu-id="7fd02-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="7fd02-116">如需連線和閘道器問題的疑難排解秘訣，請參閱[針對閘道問題進行疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues)一文。</span><span class="sxs-lookup"><span data-stu-id="7fd02-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="7fd02-117">支援的版本</span><span class="sxs-lookup"><span data-stu-id="7fd02-117">Supported versions</span></span>
<span data-ttu-id="7fd02-118">此資料處理站 DB2 連接器支援以下 IBM DB2 平台和版本，以及支援分散式關聯資料庫架構 (DRDA) SQL 存取管理員版本 9、10 和 11：</span><span class="sxs-lookup"><span data-stu-id="7fd02-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="7fd02-119">IBM DB2 for z/OS 版本 11.1</span><span class="sxs-lookup"><span data-stu-id="7fd02-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="7fd02-120">IBM DB2 for z/OS 版本 10.1</span><span class="sxs-lookup"><span data-stu-id="7fd02-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="7fd02-121">IBM DB2 for i (AS400) 版本 7.2</span><span class="sxs-lookup"><span data-stu-id="7fd02-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="7fd02-122">IBM DB2 for i (AS400) 版本 7.1</span><span class="sxs-lookup"><span data-stu-id="7fd02-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="7fd02-123">IBM DB2 for Linux, UNIX, and Windows (LUW) 版本 11</span><span class="sxs-lookup"><span data-stu-id="7fd02-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="7fd02-124">IBM DB2 for LUW 版本 10.5</span><span class="sxs-lookup"><span data-stu-id="7fd02-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="7fd02-125">IBM DB2 for LUW 版本 10.1</span><span class="sxs-lookup"><span data-stu-id="7fd02-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="7fd02-126">如果收到錯誤訊息「找不到對應至 SQL 陳述式執行要求的套件。</span><span class="sxs-lookup"><span data-stu-id="7fd02-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="7fd02-127">SQLSTATE=51002 SQLCODE=-805」，原因是作業系統上未針對一般使用者建立所需的套件。</span><span class="sxs-lookup"><span data-stu-id="7fd02-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="7fd02-128">若要解決此問題，請針對 DB2 伺服器類型遵循這些指示：</span><span class="sxs-lookup"><span data-stu-id="7fd02-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="7fd02-129">DB2 for i (AS400)：進行複製活動之前，讓進階使用者建立一般使用者的集合。</span><span class="sxs-lookup"><span data-stu-id="7fd02-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="7fd02-130">若要建立集合，請使用命令：`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="7fd02-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="7fd02-131">DB2 for z/OS 或 LUW：使用高權限帳戶 -- 具有套件授權單位與 BIND、BINDADD、GRANT EXECUTE TO PUBLIC 權限的進階使用者 -- 執行一次複製。</span><span class="sxs-lookup"><span data-stu-id="7fd02-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="7fd02-132">在複製期間，會自動建立所需的套件。</span><span class="sxs-lookup"><span data-stu-id="7fd02-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="7fd02-133">之後，您可以切換至一般使用者，來執行後續的複製。</span><span class="sxs-lookup"><span data-stu-id="7fd02-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7fd02-134">開始使用</span><span class="sxs-lookup"><span data-stu-id="7fd02-134">Getting started</span></span>
<span data-ttu-id="7fd02-135">您可以藉由使用不同的工具和 API，建立內含複製活動的管線，以從內部部署的 DB2 資料存放區移動資料：</span><span class="sxs-lookup"><span data-stu-id="7fd02-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="7fd02-136">建立管線的最簡單方式就是使用「Azure Data Factory 複製精靈」。</span><span class="sxs-lookup"><span data-stu-id="7fd02-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="7fd02-137">如需使用複製精靈建立管線的快速逐步解說，請參閱 [教學課程︰使用複製精靈建立管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="7fd02-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="7fd02-138">您也可以使工具來建立管線，包括 Azure 入口網站、Visual Studio、Azure PowerShell、Azure Resource Manager 範本、.NET API 及 REST API。</span><span class="sxs-lookup"><span data-stu-id="7fd02-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="7fd02-139">如需建立內含複製活動之管線的逐步指示，請參閱[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="7fd02-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="7fd02-140">不論您是使用工具還是 API，都需執行下列步驟來建立將資料從來源資料存放區移到接收資料存放區的管線：</span><span class="sxs-lookup"><span data-stu-id="7fd02-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="7fd02-141">建立連結服務，將輸入和輸出資料存放區連結到資料處理站。</span><span class="sxs-lookup"><span data-stu-id="7fd02-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="7fd02-142">建立資料集，代表複製作業的輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="7fd02-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="7fd02-143">建立管線，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="7fd02-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="7fd02-144">使用複製精靈時，精靈會自動為您建立已連結 Data Factory 之服務、資料集及管線實體的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="7fd02-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="7fd02-145">使用工具或 API (.NET API 除外) 時，您需使用 JSON 格式來定義資料處理站實體。</span><span class="sxs-lookup"><span data-stu-id="7fd02-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="7fd02-146">[JSON 範例：將資料從 DB2 複製到 Azure Blob 儲存體](#json-example-copy-data-from-db2-to-azure-blob)顯示用來從內部部署 DB2 資料存放區複製資料的 Data Factory 實體本身的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="7fd02-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="7fd02-147">下列各節提供 JSON 屬性的相關詳細資料，這些屬性是用來定義 DB2 資料存放區特定的 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="7fd02-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="7fd02-148">DB2 連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="7fd02-148">DB2 linked service properties</span></span>
<span data-ttu-id="7fd02-149">下表列出 DB2 連結服務特定的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="7fd02-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="7fd02-150">屬性</span><span class="sxs-lookup"><span data-stu-id="7fd02-150">Property</span></span> | <span data-ttu-id="7fd02-151">說明</span><span class="sxs-lookup"><span data-stu-id="7fd02-151">Description</span></span> | <span data-ttu-id="7fd02-152">必要</span><span class="sxs-lookup"><span data-stu-id="7fd02-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fd02-153">**type**</span><span class="sxs-lookup"><span data-stu-id="7fd02-153">**type**</span></span> |<span data-ttu-id="7fd02-154">此屬性必須設為：**OnPremisesDB2**。</span><span class="sxs-lookup"><span data-stu-id="7fd02-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="7fd02-155">是</span><span class="sxs-lookup"><span data-stu-id="7fd02-155">Yes</span></span> |
| <span data-ttu-id="7fd02-156">**server**</span><span class="sxs-lookup"><span data-stu-id="7fd02-156">**server**</span></span> |<span data-ttu-id="7fd02-157">DB2 伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="7fd02-157">The name of the DB2 server.</span></span> |<span data-ttu-id="7fd02-158">是</span><span class="sxs-lookup"><span data-stu-id="7fd02-158">Yes</span></span> |
| <span data-ttu-id="7fd02-159">**database**</span><span class="sxs-lookup"><span data-stu-id="7fd02-159">**database**</span></span> |<span data-ttu-id="7fd02-160">DB2 資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="7fd02-160">The name of the DB2 database.</span></span> |<span data-ttu-id="7fd02-161">是</span><span class="sxs-lookup"><span data-stu-id="7fd02-161">Yes</span></span> |
| <span data-ttu-id="7fd02-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="7fd02-162">**schema**</span></span> |<span data-ttu-id="7fd02-163">在 DB2 資料庫中的結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="7fd02-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="7fd02-164">此屬性必須區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7fd02-164">This property is case-sensitive.</span></span> |<span data-ttu-id="7fd02-165">否</span><span class="sxs-lookup"><span data-stu-id="7fd02-165">No</span></span> |
| <span data-ttu-id="7fd02-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="7fd02-166">**authenticationType**</span></span> |<span data-ttu-id="7fd02-167">用來連接到 DB2 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="7fd02-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="7fd02-168">可能的值為：匿名、基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="7fd02-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="7fd02-169">是</span><span class="sxs-lookup"><span data-stu-id="7fd02-169">Yes</span></span> |
| <span data-ttu-id="7fd02-170">**username**</span><span class="sxs-lookup"><span data-stu-id="7fd02-170">**username**</span></span> |<span data-ttu-id="7fd02-171">使用者帳戶的名稱 (如果您使用基本或 Windows 驗證)。</span><span class="sxs-lookup"><span data-stu-id="7fd02-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="7fd02-172">否</span><span class="sxs-lookup"><span data-stu-id="7fd02-172">No</span></span> |
| <span data-ttu-id="7fd02-173">**password**</span><span class="sxs-lookup"><span data-stu-id="7fd02-173">**password**</span></span> |<span data-ttu-id="7fd02-174">使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="7fd02-174">The password for the user account.</span></span> |<span data-ttu-id="7fd02-175">否</span><span class="sxs-lookup"><span data-stu-id="7fd02-175">No</span></span> |
| <span data-ttu-id="7fd02-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="7fd02-176">**gatewayName**</span></span> |<span data-ttu-id="7fd02-177">Data Factory 服務應該用來連接到內部部署 DB2 資料庫的閘道器名稱。</span><span class="sxs-lookup"><span data-stu-id="7fd02-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="7fd02-178">是</span><span class="sxs-lookup"><span data-stu-id="7fd02-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="7fd02-179">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="7fd02-179">Dataset properties</span></span>
<span data-ttu-id="7fd02-180">如需定義資料集的區段和屬性清單，請參閱[建立資料集](data-factory-create-datasets.md)一文。</span><span class="sxs-lookup"><span data-stu-id="7fd02-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7fd02-181">資料集 JSON 的**結構**、**可用性**和**原則**等區段類似於所有的資料集類型 (Azure SQL、Azure Blob 儲存體、Azure 資料表儲存體等)。</span><span class="sxs-lookup"><span data-stu-id="7fd02-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="7fd02-182">每個資料集類型的 **typeProperties** 區段都不同，可提供資料存放區中的資料位置資訊。</span><span class="sxs-lookup"><span data-stu-id="7fd02-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="7fd02-183">**RelationalTable** 類型資料集的 **typeProperties** 區段 (包含 DB2 資料集) 具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="7fd02-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="7fd02-184">屬性</span><span class="sxs-lookup"><span data-stu-id="7fd02-184">Property</span></span> | <span data-ttu-id="7fd02-185">說明</span><span class="sxs-lookup"><span data-stu-id="7fd02-185">Description</span></span> | <span data-ttu-id="7fd02-186">必要</span><span class="sxs-lookup"><span data-stu-id="7fd02-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fd02-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="7fd02-187">**tableName**</span></span> |<span data-ttu-id="7fd02-188">DB2 資料庫執行個體中連結服務所參照的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="7fd02-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="7fd02-189">此屬性必須區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7fd02-189">This property is case-sensitive.</span></span> |<span data-ttu-id="7fd02-190">否 (如果指定 **RelationalSource** 類型複製活動的**查詢**屬性)</span><span class="sxs-lookup"><span data-stu-id="7fd02-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="7fd02-191">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="7fd02-191">Copy Activity properties</span></span>
<span data-ttu-id="7fd02-192">如需定義複製活動的區段和屬性清單，請參閱[建立管線](data-factory-create-pipelines.md)一文。</span><span class="sxs-lookup"><span data-stu-id="7fd02-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7fd02-193">複製活動屬性 (例如**名稱**、**描述**、**輸入**資料表、**輸出**資料表，以及**原則**) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="7fd02-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="7fd02-194">每個活動類型的活動 **typeProperties** 區段中可用的屬性。</span><span class="sxs-lookup"><span data-stu-id="7fd02-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="7fd02-195">就複製活動而言，屬性會根據資料來源和接收的類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="7fd02-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="7fd02-196">在複製活動中，如果來源類型為 **RelationalSource** (包含 DB2)，則 **typeProperties** 區段可使用下列屬性：</span><span class="sxs-lookup"><span data-stu-id="7fd02-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="7fd02-197">屬性</span><span class="sxs-lookup"><span data-stu-id="7fd02-197">Property</span></span> | <span data-ttu-id="7fd02-198">說明</span><span class="sxs-lookup"><span data-stu-id="7fd02-198">Description</span></span> | <span data-ttu-id="7fd02-199">允許的值</span><span class="sxs-lookup"><span data-stu-id="7fd02-199">Allowed values</span></span> | <span data-ttu-id="7fd02-200">必要</span><span class="sxs-lookup"><span data-stu-id="7fd02-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7fd02-201">**查詢**</span><span class="sxs-lookup"><span data-stu-id="7fd02-201">**query**</span></span> |<span data-ttu-id="7fd02-202">使用自訂查詢來讀取資料。</span><span class="sxs-lookup"><span data-stu-id="7fd02-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="7fd02-203">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="7fd02-203">SQL query string.</span></span> <span data-ttu-id="7fd02-204">例如：`"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="7fd02-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="7fd02-205">否 (如果已指定資料集的 **tableName** 屬性)</span><span class="sxs-lookup"><span data-stu-id="7fd02-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="7fd02-206">結構描述和資料表名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7fd02-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="7fd02-207">在查詢陳述式中，使用 "" (雙引號) 括住屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="7fd02-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="7fd02-208">例如：</span><span class="sxs-lookup"><span data-stu-id="7fd02-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="7fd02-209">JSON 範例：將資料從 DB2 複製到 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="7fd02-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="7fd02-210">此範例提供您使用 [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)、[Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 或 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md) 來建立管線時，可使用的範例 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="7fd02-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7fd02-211">此範例示範如何將資料從 DB2 資料庫複製到 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7fd02-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="7fd02-212">不過，可以使用 Azure Data Factory 複製活動，將資料複製到[任何支援的資料存放區接收類型](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="7fd02-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="7fd02-213">範例有下列 Data Factory 實體：</span><span class="sxs-lookup"><span data-stu-id="7fd02-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="7fd02-214">[OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)類型的 DB2 連結服務</span><span class="sxs-lookup"><span data-stu-id="7fd02-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="7fd02-215">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的 Azure Blob 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="7fd02-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="7fd02-216">[RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="7fd02-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="7fd02-217">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="7fd02-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="7fd02-218">具有使用 [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) 和 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) 屬性之複製活動的[管線](data-factory-create-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="7fd02-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="7fd02-219">此範例會每個小時將資料從 DB2 資料庫中的查詢結果複製到 Azure Blob。</span><span class="sxs-lookup"><span data-stu-id="7fd02-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="7fd02-220">實體定義後面的各節會說明範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="7fd02-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="7fd02-221">第一個步驟是安裝和設定資料閘道。</span><span class="sxs-lookup"><span data-stu-id="7fd02-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="7fd02-222">如需相關指示，請參閱[在內部部署位置和雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)一文。</span><span class="sxs-lookup"><span data-stu-id="7fd02-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="7fd02-223">**DB2 連結服務**</span><span class="sxs-lookup"><span data-stu-id="7fd02-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

<span data-ttu-id="7fd02-224">**Azure Blob 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="7fd02-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="7fd02-225">**DB2 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="7fd02-225">**DB2 input dataset**</span></span>

<span data-ttu-id="7fd02-226">此範例假設您已在 DB2 中建立資料表 "MyTable"，其中包含時間序列資料的資料行 (名稱為 "timestamp")。</span><span class="sxs-lookup"><span data-stu-id="7fd02-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="7fd02-227">**外部**屬性是設定為 "true"。</span><span class="sxs-lookup"><span data-stu-id="7fd02-227">The **external** property is set to "true."</span></span> <span data-ttu-id="7fd02-228">此設定可讓 Data Factory 服務知道資料集是在 Data Factory 外部，而不是由 Data Factory 中的活動所產生。</span><span class="sxs-lookup"><span data-stu-id="7fd02-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="7fd02-229">請注意，**類型**屬性是設定為 **RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="7fd02-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

<span data-ttu-id="7fd02-230">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="7fd02-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="7fd02-231">藉由將 **frequency** 屬性設定 "Hour"，並將 **interval** 屬性設定為 1，資料會每小時寫入到新的 Blob。</span><span class="sxs-lookup"><span data-stu-id="7fd02-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="7fd02-232">根據正在處理之配量的開始時間，以動態方式評估 Blob 的 **folderPath** 屬性。</span><span class="sxs-lookup"><span data-stu-id="7fd02-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="7fd02-233">資料夾路徑會使用開始時間的年、月、日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="7fd02-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="7fd02-234">**複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="7fd02-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="7fd02-235">此管線包含複製活動，該活動已設定為使用指定的輸入和輸出資料集並排定為每小時執行。</span><span class="sxs-lookup"><span data-stu-id="7fd02-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="7fd02-236">在管線的 JSON 定義中，已將 **source** 類型設為 **RelationalSource**，並將 **sink** 類型設為 **BlobSink**。</span><span class="sxs-lookup"><span data-stu-id="7fd02-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="7fd02-237">針對 **query** 屬性指定的 SQL 查詢會從 "Orders" 資料表選取資料。</span><span class="sxs-lookup"><span data-stu-id="7fd02-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="7fd02-238">DB2 的類型對應</span><span class="sxs-lookup"><span data-stu-id="7fd02-238">Type mapping for DB2</span></span>
<span data-ttu-id="7fd02-239">如 [資料移動活動](data-factory-data-movement-activities.md) 一文所述，複製活動會使用下列含有兩個步驟的方法，執行從來源類型轉換成接收類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="7fd02-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="7fd02-240">從原生來源類型轉換成 .NET 類型</span><span class="sxs-lookup"><span data-stu-id="7fd02-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="7fd02-241">從 .NET 類型轉換成原生接收類型</span><span class="sxs-lookup"><span data-stu-id="7fd02-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="7fd02-242">複製活動將資料從 DB2 類型轉換成.NET 型別時，會使用下列對應：</span><span class="sxs-lookup"><span data-stu-id="7fd02-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="7fd02-243">DB2 資料庫類型</span><span class="sxs-lookup"><span data-stu-id="7fd02-243">DB2 database type</span></span> | <span data-ttu-id="7fd02-244">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="7fd02-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="7fd02-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="7fd02-245">SmallInt</span></span> |<span data-ttu-id="7fd02-246">Int16</span><span class="sxs-lookup"><span data-stu-id="7fd02-246">Int16</span></span> |
| <span data-ttu-id="7fd02-247">Integer</span><span class="sxs-lookup"><span data-stu-id="7fd02-247">Integer</span></span> |<span data-ttu-id="7fd02-248">Int32</span><span class="sxs-lookup"><span data-stu-id="7fd02-248">Int32</span></span> |
| <span data-ttu-id="7fd02-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="7fd02-249">BigInt</span></span> |<span data-ttu-id="7fd02-250">Int64</span><span class="sxs-lookup"><span data-stu-id="7fd02-250">Int64</span></span> |
| <span data-ttu-id="7fd02-251">Real</span><span class="sxs-lookup"><span data-stu-id="7fd02-251">Real</span></span> |<span data-ttu-id="7fd02-252">單一</span><span class="sxs-lookup"><span data-stu-id="7fd02-252">Single</span></span> |
| <span data-ttu-id="7fd02-253">兩倍</span><span class="sxs-lookup"><span data-stu-id="7fd02-253">Double</span></span> |<span data-ttu-id="7fd02-254">兩倍</span><span class="sxs-lookup"><span data-stu-id="7fd02-254">Double</span></span> |
| <span data-ttu-id="7fd02-255">Float</span><span class="sxs-lookup"><span data-stu-id="7fd02-255">Float</span></span> |<span data-ttu-id="7fd02-256">兩倍</span><span class="sxs-lookup"><span data-stu-id="7fd02-256">Double</span></span> |
| <span data-ttu-id="7fd02-257">十進位</span><span class="sxs-lookup"><span data-stu-id="7fd02-257">Decimal</span></span> |<span data-ttu-id="7fd02-258">十進位</span><span class="sxs-lookup"><span data-stu-id="7fd02-258">Decimal</span></span> |
| <span data-ttu-id="7fd02-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="7fd02-259">DecimalFloat</span></span> |<span data-ttu-id="7fd02-260">十進位</span><span class="sxs-lookup"><span data-stu-id="7fd02-260">Decimal</span></span> |
| <span data-ttu-id="7fd02-261">數值</span><span class="sxs-lookup"><span data-stu-id="7fd02-261">Numeric</span></span> |<span data-ttu-id="7fd02-262">十進位</span><span class="sxs-lookup"><span data-stu-id="7fd02-262">Decimal</span></span> |
| <span data-ttu-id="7fd02-263">Date</span><span class="sxs-lookup"><span data-stu-id="7fd02-263">Date</span></span> |<span data-ttu-id="7fd02-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="7fd02-264">DateTime</span></span> |
| <span data-ttu-id="7fd02-265">時間</span><span class="sxs-lookup"><span data-stu-id="7fd02-265">Time</span></span> |<span data-ttu-id="7fd02-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="7fd02-266">TimeSpan</span></span> |
| <span data-ttu-id="7fd02-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="7fd02-267">Timestamp</span></span> |<span data-ttu-id="7fd02-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="7fd02-268">DateTime</span></span> |
| <span data-ttu-id="7fd02-269">xml</span><span class="sxs-lookup"><span data-stu-id="7fd02-269">Xml</span></span> |<span data-ttu-id="7fd02-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7fd02-270">Byte[]</span></span> |
| <span data-ttu-id="7fd02-271">Char</span><span class="sxs-lookup"><span data-stu-id="7fd02-271">Char</span></span> |<span data-ttu-id="7fd02-272">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-272">String</span></span> |
| <span data-ttu-id="7fd02-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="7fd02-273">VarChar</span></span> |<span data-ttu-id="7fd02-274">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-274">String</span></span> |
| <span data-ttu-id="7fd02-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="7fd02-275">LongVarChar</span></span> |<span data-ttu-id="7fd02-276">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-276">String</span></span> |
| <span data-ttu-id="7fd02-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="7fd02-277">DB2DynArray</span></span> |<span data-ttu-id="7fd02-278">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-278">String</span></span> |
| <span data-ttu-id="7fd02-279">Binary</span><span class="sxs-lookup"><span data-stu-id="7fd02-279">Binary</span></span> |<span data-ttu-id="7fd02-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7fd02-280">Byte[]</span></span> |
| <span data-ttu-id="7fd02-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="7fd02-281">VarBinary</span></span> |<span data-ttu-id="7fd02-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7fd02-282">Byte[]</span></span> |
| <span data-ttu-id="7fd02-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="7fd02-283">LongVarBinary</span></span> |<span data-ttu-id="7fd02-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7fd02-284">Byte[]</span></span> |
| <span data-ttu-id="7fd02-285">圖形</span><span class="sxs-lookup"><span data-stu-id="7fd02-285">Graphic</span></span> |<span data-ttu-id="7fd02-286">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-286">String</span></span> |
| <span data-ttu-id="7fd02-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="7fd02-287">VarGraphic</span></span> |<span data-ttu-id="7fd02-288">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-288">String</span></span> |
| <span data-ttu-id="7fd02-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="7fd02-289">LongVarGraphic</span></span> |<span data-ttu-id="7fd02-290">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-290">String</span></span> |
| <span data-ttu-id="7fd02-291">Clob</span><span class="sxs-lookup"><span data-stu-id="7fd02-291">Clob</span></span> |<span data-ttu-id="7fd02-292">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-292">String</span></span> |
| <span data-ttu-id="7fd02-293">Blob</span><span class="sxs-lookup"><span data-stu-id="7fd02-293">Blob</span></span> |<span data-ttu-id="7fd02-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7fd02-294">Byte[]</span></span> |
| <span data-ttu-id="7fd02-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="7fd02-295">DbClob</span></span> |<span data-ttu-id="7fd02-296">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-296">String</span></span> |
| <span data-ttu-id="7fd02-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="7fd02-297">SmallInt</span></span> |<span data-ttu-id="7fd02-298">Int16</span><span class="sxs-lookup"><span data-stu-id="7fd02-298">Int16</span></span> |
| <span data-ttu-id="7fd02-299">Integer</span><span class="sxs-lookup"><span data-stu-id="7fd02-299">Integer</span></span> |<span data-ttu-id="7fd02-300">Int32</span><span class="sxs-lookup"><span data-stu-id="7fd02-300">Int32</span></span> |
| <span data-ttu-id="7fd02-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="7fd02-301">BigInt</span></span> |<span data-ttu-id="7fd02-302">Int64</span><span class="sxs-lookup"><span data-stu-id="7fd02-302">Int64</span></span> |
| <span data-ttu-id="7fd02-303">Real</span><span class="sxs-lookup"><span data-stu-id="7fd02-303">Real</span></span> |<span data-ttu-id="7fd02-304">單一</span><span class="sxs-lookup"><span data-stu-id="7fd02-304">Single</span></span> |
| <span data-ttu-id="7fd02-305">兩倍</span><span class="sxs-lookup"><span data-stu-id="7fd02-305">Double</span></span> |<span data-ttu-id="7fd02-306">兩倍</span><span class="sxs-lookup"><span data-stu-id="7fd02-306">Double</span></span> |
| <span data-ttu-id="7fd02-307">Float</span><span class="sxs-lookup"><span data-stu-id="7fd02-307">Float</span></span> |<span data-ttu-id="7fd02-308">兩倍</span><span class="sxs-lookup"><span data-stu-id="7fd02-308">Double</span></span> |
| <span data-ttu-id="7fd02-309">十進位</span><span class="sxs-lookup"><span data-stu-id="7fd02-309">Decimal</span></span> |<span data-ttu-id="7fd02-310">十進位</span><span class="sxs-lookup"><span data-stu-id="7fd02-310">Decimal</span></span> |
| <span data-ttu-id="7fd02-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="7fd02-311">DecimalFloat</span></span> |<span data-ttu-id="7fd02-312">十進位</span><span class="sxs-lookup"><span data-stu-id="7fd02-312">Decimal</span></span> |
| <span data-ttu-id="7fd02-313">數值</span><span class="sxs-lookup"><span data-stu-id="7fd02-313">Numeric</span></span> |<span data-ttu-id="7fd02-314">十進位</span><span class="sxs-lookup"><span data-stu-id="7fd02-314">Decimal</span></span> |
| <span data-ttu-id="7fd02-315">Date</span><span class="sxs-lookup"><span data-stu-id="7fd02-315">Date</span></span> |<span data-ttu-id="7fd02-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="7fd02-316">DateTime</span></span> |
| <span data-ttu-id="7fd02-317">時間</span><span class="sxs-lookup"><span data-stu-id="7fd02-317">Time</span></span> |<span data-ttu-id="7fd02-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="7fd02-318">TimeSpan</span></span> |
| <span data-ttu-id="7fd02-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="7fd02-319">Timestamp</span></span> |<span data-ttu-id="7fd02-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="7fd02-320">DateTime</span></span> |
| <span data-ttu-id="7fd02-321">xml</span><span class="sxs-lookup"><span data-stu-id="7fd02-321">Xml</span></span> |<span data-ttu-id="7fd02-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="7fd02-322">Byte[]</span></span> |
| <span data-ttu-id="7fd02-323">Char</span><span class="sxs-lookup"><span data-stu-id="7fd02-323">Char</span></span> |<span data-ttu-id="7fd02-324">String</span><span class="sxs-lookup"><span data-stu-id="7fd02-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="7fd02-325">將來源對應到接收資料行</span><span class="sxs-lookup"><span data-stu-id="7fd02-325">Map source to sink columns</span></span>
<span data-ttu-id="7fd02-326">若要了解如何將來源資料集內的資料行與接收資料集內的資料行對應，請參閱[在 Azure Data Factory 中對應資料集資料行](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="7fd02-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="7fd02-327">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="7fd02-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="7fd02-328">從關聯式資料存放區複製資料時，請留意可重複性，以避免產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="7fd02-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="7fd02-329">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="7fd02-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="7fd02-330">您也可以為資料集設定重試**原則**屬性，使得在發生失敗時，重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="7fd02-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="7fd02-331">確定無論配量將執行多少次，而且無論如何重新執行配量，均讀取相同的資料。</span><span class="sxs-lookup"><span data-stu-id="7fd02-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="7fd02-332">如需詳細資訊，請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="7fd02-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7fd02-333">效能和微調</span><span class="sxs-lookup"><span data-stu-id="7fd02-333">Performance and tuning</span></span>
<span data-ttu-id="7fd02-334">請參閱[複製活動的效能及微調指南](data-factory-copy-activity-performance.md)，了解影響複製活動效能的重要因素，以及達到最佳效能的各種方法。</span><span class="sxs-lookup"><span data-stu-id="7fd02-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>