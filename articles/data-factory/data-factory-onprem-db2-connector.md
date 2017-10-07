---
title: "將資料從 DB2 aaaMove 使用 Azure Data Factory |Microsoft 文件"
description: "了解如何使用 Azure 資料 Factory 複製活動 toomove 資料從內部部署 DB2 資料庫"
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
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="5bc07-103">使用 Azure Data Factory 複製活動從 DB2 移動資料</span><span class="sxs-lookup"><span data-stu-id="5bc07-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="5bc07-104">本文說明如何使用複製活動，以及在 Azure Data Factory toocopy 資料從內部部署 DB2 資料庫 tooa 資料存放區中。</span><span class="sxs-lookup"><span data-stu-id="5bc07-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="5bc07-105">您可以複製資料 tooany 存放區中 hello 支援接收已列為[Data Factory 資料移動活動](data-factory-data-movement-activities.md#supported-data-stores-and-formats)發行項。</span><span class="sxs-lookup"><span data-stu-id="5bc07-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="5bc07-106">本主題是根據 hello Data Factory 發行項，這會使用複製活動中呈現資料移動的概觀，並列出支援的 hello 資料存放區的組合。</span><span class="sxs-lookup"><span data-stu-id="5bc07-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="5bc07-107">Data Factory 目前支援從 DB2 資料庫 tooa 只移動資料[支援的接收資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。</span><span class="sxs-lookup"><span data-stu-id="5bc07-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="5bc07-108">將資料從其他資料會儲存 tooa DB2 資料庫不支援。</span><span class="sxs-lookup"><span data-stu-id="5bc07-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bc07-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="5bc07-109">Prerequisites</span></span>
<span data-ttu-id="5bc07-110">Data Factory 支援連接 tooan 在內部部署 DB2 資料庫使用 hello[資料管理閘道器](data-factory-data-management-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc07-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="5bc07-111">Hello 閘道資料的逐步指示 tooset 管線 toomove 您的資料，請參閱 hello[將資料從內部部署 toocloud 移](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="5bc07-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="5bc07-112">即使 hello DB2 裝載於 Azure IaaS VM，就需要閘道。</span><span class="sxs-lookup"><span data-stu-id="5bc07-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="5bc07-113">您可以在 hello 安裝 hello 閘道相同的 IaaS VM 做為 hello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="5bc07-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="5bc07-114">如果 hello 閘道可以連接 toohello 資料庫，您可以在不同的 VM 上安裝 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="5bc07-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="5bc07-115">hello 資料管理閘道器提供內建的 DB2 驅動程式，因此您不需要 toomanually 安裝驅動程式 toocopy 資料從 DB2。</span><span class="sxs-lookup"><span data-stu-id="5bc07-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc07-116">如需連接與閘道問題的疑難排解秘訣，請參閱 hello[閘道問題的疑難排解](data-factory-data-management-gateway.md#troubleshooting-gateway-issues)發行項。</span><span class="sxs-lookup"><span data-stu-id="5bc07-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="5bc07-117">支援的版本</span><span class="sxs-lookup"><span data-stu-id="5bc07-117">Supported versions</span></span>
<span data-ttu-id="5bc07-118">hello 資料 Factory DB2 連接器支援下列 IBM DB2 平台和版本與分散式關聯式資料庫架構 (DRDA) SQL Access Manager 版本 9、 10 和 11 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc07-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="5bc07-119">IBM DB2 for z/OS 版本 11.1</span><span class="sxs-lookup"><span data-stu-id="5bc07-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="5bc07-120">IBM DB2 for z/OS 版本 10.1</span><span class="sxs-lookup"><span data-stu-id="5bc07-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="5bc07-121">IBM DB2 for i (AS400) 版本 7.2</span><span class="sxs-lookup"><span data-stu-id="5bc07-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="5bc07-122">IBM DB2 for i (AS400) 版本 7.1</span><span class="sxs-lookup"><span data-stu-id="5bc07-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="5bc07-123">IBM DB2 for Linux, UNIX, and Windows (LUW) 版本 11</span><span class="sxs-lookup"><span data-stu-id="5bc07-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="5bc07-124">IBM DB2 for LUW 版本 10.5</span><span class="sxs-lookup"><span data-stu-id="5bc07-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="5bc07-125">IBM DB2 for LUW 版本 10.1</span><span class="sxs-lookup"><span data-stu-id="5bc07-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="5bc07-126">如果您收到 hello 錯誤訊息 「 hello 套件對應 tooan SQL 陳述式執行的要求已找不到。</span><span class="sxs-lookup"><span data-stu-id="5bc07-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="5bc07-127">SQLSTATE = 51002 SQLCODE =-805，"hello 原因是 hello hello OS 上的一般使用者不會建立所需的套件。</span><span class="sxs-lookup"><span data-stu-id="5bc07-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="5bc07-128">tooresolve 這個問題，請遵循這些指示適用於您的 DB2 伺服器類型：</span><span class="sxs-lookup"><span data-stu-id="5bc07-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="5bc07-129">DB2 for i (AS400): 可讓建立 hello 一般使用者的 hello 集合，才能執行複製活動的進階使用者。</span><span class="sxs-lookup"><span data-stu-id="5bc07-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="5bc07-130">使用 hello 命令 toocreate hello 集合：`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="5bc07-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="5bc07-131">DB2 for z/OS 或 LUW： 使用高的權限的帳戶-進階使用者或系統管理員具有封裝授權單位和繫結，BINDADD，授與 EXECUTE tooPUBLIC 權限-toorun hello 複製一次。</span><span class="sxs-lookup"><span data-stu-id="5bc07-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="5bc07-132">hello 複製期間，會自動建立 hello 所需的套件。</span><span class="sxs-lookup"><span data-stu-id="5bc07-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="5bc07-133">之後，您可以在後續複製回合切換後 toohello 一般使用者。</span><span class="sxs-lookup"><span data-stu-id="5bc07-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5bc07-134">開始使用</span><span class="sxs-lookup"><span data-stu-id="5bc07-134">Getting started</span></span>
<span data-ttu-id="5bc07-135">您可以使用不同的工具和 Api，與從內部部署 DB2 資料存放區的複製活動 toomove 資料建立管線：</span><span class="sxs-lookup"><span data-stu-id="5bc07-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="5bc07-136">最簡單方式 toocreate hello 管線為 toouse hello Azure 資料 Factory 複製精靈。</span><span class="sxs-lookup"><span data-stu-id="5bc07-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="5bc07-137">如需使用 hello 複製精靈建立管線的快速逐步解說，請參閱 hello[教學課程： 使用 hello 複製精靈建立的管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc07-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="5bc07-138">您也可以使用工具 toocreate 管線，包括 hello Azure 入口網站、 Visual Studio、 Azure PowerShell、 Azure Resource Manager 範本、 hello.NET API 和 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="5bc07-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="5bc07-139">如需逐步指示 toocreate 具有複製活動的管線，請參閱 hello[複製活動教學課程](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc07-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="5bc07-140">無論您是使用 hello 工具或 Api，會執行下列步驟 toocreate 移動來源資料中的資料存放區 tooa 接收資料存放區的管線的 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc07-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="5bc07-141">建立連結的服務 toolink 輸入和輸出資料存放區 tooyour 資料處理站。</span><span class="sxs-lookup"><span data-stu-id="5bc07-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="5bc07-142">建立資料集 toorepresent 輸入和輸出 hello 複製作業的資料。</span><span class="sxs-lookup"><span data-stu-id="5bc07-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="5bc07-143">建立管線，其中含有以一個資料集作為輸入、一個資料集作為輸出的複製活動。</span><span class="sxs-lookup"><span data-stu-id="5bc07-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5bc07-144">當您使用 hello 複製精靈，hello 連結的 Data Factory 服務的 JSON 定義資料集和管線實體會自動為您建立。</span><span class="sxs-lookup"><span data-stu-id="5bc07-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="5bc07-145">當您使用工具或 Api （除了 hello.NET 應用程式開發介面) 時，您會定義使用 hello JSON 格式的 hello Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="5bc07-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="5bc07-146">hello [JSON 範例： 將資料從 DB2 tooAzure Blob 儲存體複製](#json-example-copy-data-from-db2-to-azure-blob)顯示 hello hello JSON 定義是使用的 toocopy 資料從內部部署 DB2 資料存放區的 Data Factory 實體。</span><span class="sxs-lookup"><span data-stu-id="5bc07-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="5bc07-147">hello 下列各節提供 hello 詳細資料會使用的 toodefine hello Data Factory 實體的特定 tooa DB2 資料存放區的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="5bc07-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="5bc07-148">DB2 連結服務屬性</span><span class="sxs-lookup"><span data-stu-id="5bc07-148">DB2 linked service properties</span></span>
<span data-ttu-id="5bc07-149">hello 下表列出特定 tooa DB2 連結服務的 hello JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="5bc07-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="5bc07-150">屬性</span><span class="sxs-lookup"><span data-stu-id="5bc07-150">Property</span></span> | <span data-ttu-id="5bc07-151">說明</span><span class="sxs-lookup"><span data-stu-id="5bc07-151">Description</span></span> | <span data-ttu-id="5bc07-152">必要</span><span class="sxs-lookup"><span data-stu-id="5bc07-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5bc07-153">**type**</span><span class="sxs-lookup"><span data-stu-id="5bc07-153">**type**</span></span> |<span data-ttu-id="5bc07-154">這個屬性必須設定太**OnPremisesDB2**。</span><span class="sxs-lookup"><span data-stu-id="5bc07-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="5bc07-155">是</span><span class="sxs-lookup"><span data-stu-id="5bc07-155">Yes</span></span> |
| <span data-ttu-id="5bc07-156">**server**</span><span class="sxs-lookup"><span data-stu-id="5bc07-156">**server**</span></span> |<span data-ttu-id="5bc07-157">hello hello DB2 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="5bc07-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="5bc07-158">是</span><span class="sxs-lookup"><span data-stu-id="5bc07-158">Yes</span></span> |
| <span data-ttu-id="5bc07-159">**database**</span><span class="sxs-lookup"><span data-stu-id="5bc07-159">**database**</span></span> |<span data-ttu-id="5bc07-160">hello hello DB2 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="5bc07-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="5bc07-161">是</span><span class="sxs-lookup"><span data-stu-id="5bc07-161">Yes</span></span> |
| <span data-ttu-id="5bc07-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="5bc07-162">**schema**</span></span> |<span data-ttu-id="5bc07-163">hello hello DB2 資料庫中的 hello 結構描述名稱。</span><span class="sxs-lookup"><span data-stu-id="5bc07-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="5bc07-164">此屬性必須區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5bc07-164">This property is case-sensitive.</span></span> |<span data-ttu-id="5bc07-165">否</span><span class="sxs-lookup"><span data-stu-id="5bc07-165">No</span></span> |
| <span data-ttu-id="5bc07-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="5bc07-166">**authenticationType**</span></span> |<span data-ttu-id="5bc07-167">hello 使用的 tooconnect toohello DB2 資料庫的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="5bc07-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="5bc07-168">hello 可能的值為： 匿名、 基本和 Windows。</span><span class="sxs-lookup"><span data-stu-id="5bc07-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="5bc07-169">是</span><span class="sxs-lookup"><span data-stu-id="5bc07-169">Yes</span></span> |
| <span data-ttu-id="5bc07-170">**username**</span><span class="sxs-lookup"><span data-stu-id="5bc07-170">**username**</span></span> |<span data-ttu-id="5bc07-171">如果您使用基本或 Windows 驗證的 hello 的使用者帳戶的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="5bc07-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="5bc07-172">否</span><span class="sxs-lookup"><span data-stu-id="5bc07-172">No</span></span> |
| <span data-ttu-id="5bc07-173">**password**</span><span class="sxs-lookup"><span data-stu-id="5bc07-173">**password**</span></span> |<span data-ttu-id="5bc07-174">hello hello 使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="5bc07-174">hello password for hello user account.</span></span> |<span data-ttu-id="5bc07-175">否</span><span class="sxs-lookup"><span data-stu-id="5bc07-175">No</span></span> |
| <span data-ttu-id="5bc07-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="5bc07-176">**gatewayName**</span></span> |<span data-ttu-id="5bc07-177">hello hello Data Factory 服務的 hello 閘道名稱應該使用 tooconnect toohello 在內部部署 DB2 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5bc07-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="5bc07-178">是</span><span class="sxs-lookup"><span data-stu-id="5bc07-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="5bc07-179">資料集屬性</span><span class="sxs-lookup"><span data-stu-id="5bc07-179">Dataset properties</span></span>
<span data-ttu-id="5bc07-180">如需 hello 區段和屬性都可用來定義資料集的清單，請參閱 hello[建立資料集](data-factory-create-datasets.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="5bc07-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5bc07-181">區段，例如**結構**，**可用性**，和 hello**原則**資料集 JSON，就是類似的所有資料集類型 (Azure SQL，Azure Blob 儲存體，Azure 資料表儲存體，等等）。</span><span class="sxs-lookup"><span data-stu-id="5bc07-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="5bc07-182">hello **typeProperties**區段是不同的資料集的每個型別，並提供 hello hello 資料存放區中的 hello 資料位置相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5bc07-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="5bc07-183">hello **typeProperties**類型的資料集區段**RelationalTable**，其中包含 hello DB2 資料集，具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc07-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="5bc07-184">屬性</span><span class="sxs-lookup"><span data-stu-id="5bc07-184">Property</span></span> | <span data-ttu-id="5bc07-185">說明</span><span class="sxs-lookup"><span data-stu-id="5bc07-185">Description</span></span> | <span data-ttu-id="5bc07-186">必要</span><span class="sxs-lookup"><span data-stu-id="5bc07-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5bc07-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="5bc07-187">**tableName**</span></span> |<span data-ttu-id="5bc07-188">hello 名稱 hello 連結的服務的 hello DB2 資料庫執行個體中的 hello 資料表的參考。</span><span class="sxs-lookup"><span data-stu-id="5bc07-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="5bc07-189">此屬性必須區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5bc07-189">This property is case-sensitive.</span></span> |<span data-ttu-id="5bc07-190">否 (如果 hello**查詢**複製活動的型別屬性**RelationalSource**指定)</span><span class="sxs-lookup"><span data-stu-id="5bc07-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="5bc07-191">複製活動屬性</span><span class="sxs-lookup"><span data-stu-id="5bc07-191">Copy Activity properties</span></span>
<span data-ttu-id="5bc07-192">如需 hello 區段和屬性都可用來定義複製活動的清單，請參閱 hello[建立管線](data-factory-create-pipelines.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="5bc07-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5bc07-193">複製活動屬性 (例如**名稱**、**描述**、**輸入**資料表、**輸出**資料表，以及**原則**) 適用於所有類型的活動。</span><span class="sxs-lookup"><span data-stu-id="5bc07-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="5bc07-194">hello，就可以在 hello 屬性**typeProperties** hello 活動的每個活動類型的區段。</span><span class="sxs-lookup"><span data-stu-id="5bc07-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="5bc07-195">複製活動，根據 hello 類型的資料來源與接收 hello 屬性而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5bc07-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="5bc07-196">複製活動，當 hello 來源類型的**RelationalSource** （包括 DB2），下列屬性的 hello 位於 hello **typeProperties** > 一節：</span><span class="sxs-lookup"><span data-stu-id="5bc07-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="5bc07-197">屬性</span><span class="sxs-lookup"><span data-stu-id="5bc07-197">Property</span></span> | <span data-ttu-id="5bc07-198">說明</span><span class="sxs-lookup"><span data-stu-id="5bc07-198">Description</span></span> | <span data-ttu-id="5bc07-199">允許的值</span><span class="sxs-lookup"><span data-stu-id="5bc07-199">Allowed values</span></span> | <span data-ttu-id="5bc07-200">必要</span><span class="sxs-lookup"><span data-stu-id="5bc07-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5bc07-201">**查詢**</span><span class="sxs-lookup"><span data-stu-id="5bc07-201">**query**</span></span> |<span data-ttu-id="5bc07-202">使用 hello 自訂查詢 tooread hello 資料。</span><span class="sxs-lookup"><span data-stu-id="5bc07-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="5bc07-203">SQL 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="5bc07-203">SQL query string.</span></span> <span data-ttu-id="5bc07-204">例如：`"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="5bc07-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="5bc07-205">否 (如果 hello **tableName**指定屬性的資料集)</span><span class="sxs-lookup"><span data-stu-id="5bc07-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="5bc07-206">結構描述和資料表名稱會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5bc07-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="5bc07-207">Hello 查詢陳述式中，括住屬性名稱使用""（雙引號）。</span><span class="sxs-lookup"><span data-stu-id="5bc07-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="5bc07-208">例如：</span><span class="sxs-lookup"><span data-stu-id="5bc07-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="5bc07-209">JSON 範例： 將資料從 DB2 tooAzure Blob 儲存體複製</span><span class="sxs-lookup"><span data-stu-id="5bc07-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="5bc07-210">此範例中提供的範例 JSON 定義，您可以使用 toocreate 管線使用 hello [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)， [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)，或[Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc07-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5bc07-211">hello 範例將示範如何 toocopy 資料從 DB2 資料庫 tooBlob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5bc07-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="5bc07-212">但是，太複製資料[任何支援的資料儲存接收器類型](data-factory-data-movement-activities.md#supported-data-stores-and-formats)使用 Azure 資料 Factory 複製活動。</span><span class="sxs-lookup"><span data-stu-id="5bc07-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="5bc07-213">hello 範例有下列 Data Factory 實體的 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc07-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="5bc07-214">[OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)類型的 DB2 連結服務</span><span class="sxs-lookup"><span data-stu-id="5bc07-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="5bc07-215">[AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 類型的 Azure Blob 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="5bc07-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="5bc07-216">[RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties) 類型的輸入[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="5bc07-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="5bc07-217">[AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 類型的輸出[資料集](data-factory-create-datasets.md)</span><span class="sxs-lookup"><span data-stu-id="5bc07-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="5bc07-218">A[管線](data-factory-create-pipelines.md)與使用 hello 複製活動[RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties)和[BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)屬性</span><span class="sxs-lookup"><span data-stu-id="5bc07-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="5bc07-219">hello 範例從查詢結果中的 DB2 資料庫 tooan Azure blob 複製資料的每小時。</span><span class="sxs-lookup"><span data-stu-id="5bc07-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="5bc07-220">hello 以下各節 hello 實體定義說明 hello hello 範例中使用的 JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="5bc07-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="5bc07-221">第一個步驟是安裝和設定資料閘道。</span><span class="sxs-lookup"><span data-stu-id="5bc07-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="5bc07-222">Hello 中會有指示[在內部部署位置與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="5bc07-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="5bc07-223">**DB2 連結服務**</span><span class="sxs-lookup"><span data-stu-id="5bc07-223">**DB2 linked service**</span></span>

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

<span data-ttu-id="5bc07-224">**Azure Blob 儲存體連結服務**</span><span class="sxs-lookup"><span data-stu-id="5bc07-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="5bc07-225">**DB2 輸入資料集**</span><span class="sxs-lookup"><span data-stu-id="5bc07-225">**DB2 input dataset**</span></span>

<span data-ttu-id="5bc07-226">hello 範例假設您已在名為"MyTable"已標示為"timestamp"hello 時間序列資料的資料行的 DB2 中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="5bc07-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="5bc07-227">hello**外部**屬性設定太"，則為 true。 」</span><span class="sxs-lookup"><span data-stu-id="5bc07-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="5bc07-228">此資料集是外部 toohello 資料處理站，並不產生 hello data factory 中的活動時，此設定就會通知 hello Data Factory 服務。</span><span class="sxs-lookup"><span data-stu-id="5bc07-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="5bc07-229">請注意該 hello**類型**屬性設定太**RelationalTable**。</span><span class="sxs-lookup"><span data-stu-id="5bc07-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


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

<span data-ttu-id="5bc07-230">**Azure Blob 輸出資料集**</span><span class="sxs-lookup"><span data-stu-id="5bc07-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="5bc07-231">資料寫入 tooa 新 blob 的每個小時設定 hello**頻率**屬性太 「 小時 」 和 hello**間隔**too1 屬性。</span><span class="sxs-lookup"><span data-stu-id="5bc07-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="5bc07-232">hello **folderPath**屬性會動態評估 hello blob 依據 hello 正在處理的 hello 配量的開始時間。</span><span class="sxs-lookup"><span data-stu-id="5bc07-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="5bc07-233">hello 資料夾路徑會使用 hello 的 hello 開始時間的年、 月、 日和小時部分。</span><span class="sxs-lookup"><span data-stu-id="5bc07-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

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

<span data-ttu-id="5bc07-234">**Hello 複製活動的管線**</span><span class="sxs-lookup"><span data-stu-id="5bc07-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="5bc07-235">hello 管線包含設定的複製活動 toouse 指定輸入和輸出資料集，而且是每小時排程的 toorun。</span><span class="sxs-lookup"><span data-stu-id="5bc07-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="5bc07-236">Hello hello 管線 JSON 定義中，在 hello**來源**類型設定得**RelationalSource**和 hello**接收**類型設定得**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5bc07-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="5bc07-237">指定 hello SQL 查詢**查詢**屬性選取 hello 「 訂單 」 資料表中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="5bc07-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
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

## <a name="type-mapping-for-db2"></a><span data-ttu-id="5bc07-238">DB2 的類型對應</span><span class="sxs-lookup"><span data-stu-id="5bc07-238">Type mapping for DB2</span></span>
<span data-ttu-id="5bc07-239">Hello 中所述[資料移動活動](data-factory-data-movement-activities.md)文件，複製活動使用 hello 下列兩個步驟的方法，執行從來源類型 toosink 類型的自動類型轉換：</span><span class="sxs-lookup"><span data-stu-id="5bc07-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="5bc07-240">從原生的來源類型 tooa.NET 型別轉換</span><span class="sxs-lookup"><span data-stu-id="5bc07-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="5bc07-241">從.NET 型別 tooa 原生接收類型轉換</span><span class="sxs-lookup"><span data-stu-id="5bc07-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="5bc07-242">hello 下列的對應會使用複製活動資料轉換時 hello 從 DB2 類型 tooa.NET 類型：</span><span class="sxs-lookup"><span data-stu-id="5bc07-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="5bc07-243">DB2 資料庫類型</span><span class="sxs-lookup"><span data-stu-id="5bc07-243">DB2 database type</span></span> | <span data-ttu-id="5bc07-244">.NET Framework 類型</span><span class="sxs-lookup"><span data-stu-id="5bc07-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="5bc07-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="5bc07-245">SmallInt</span></span> |<span data-ttu-id="5bc07-246">Int16</span><span class="sxs-lookup"><span data-stu-id="5bc07-246">Int16</span></span> |
| <span data-ttu-id="5bc07-247">Integer</span><span class="sxs-lookup"><span data-stu-id="5bc07-247">Integer</span></span> |<span data-ttu-id="5bc07-248">Int32</span><span class="sxs-lookup"><span data-stu-id="5bc07-248">Int32</span></span> |
| <span data-ttu-id="5bc07-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="5bc07-249">BigInt</span></span> |<span data-ttu-id="5bc07-250">Int64</span><span class="sxs-lookup"><span data-stu-id="5bc07-250">Int64</span></span> |
| <span data-ttu-id="5bc07-251">Real</span><span class="sxs-lookup"><span data-stu-id="5bc07-251">Real</span></span> |<span data-ttu-id="5bc07-252">單一</span><span class="sxs-lookup"><span data-stu-id="5bc07-252">Single</span></span> |
| <span data-ttu-id="5bc07-253">兩倍</span><span class="sxs-lookup"><span data-stu-id="5bc07-253">Double</span></span> |<span data-ttu-id="5bc07-254">兩倍</span><span class="sxs-lookup"><span data-stu-id="5bc07-254">Double</span></span> |
| <span data-ttu-id="5bc07-255">Float</span><span class="sxs-lookup"><span data-stu-id="5bc07-255">Float</span></span> |<span data-ttu-id="5bc07-256">兩倍</span><span class="sxs-lookup"><span data-stu-id="5bc07-256">Double</span></span> |
| <span data-ttu-id="5bc07-257">十進位</span><span class="sxs-lookup"><span data-stu-id="5bc07-257">Decimal</span></span> |<span data-ttu-id="5bc07-258">十進位</span><span class="sxs-lookup"><span data-stu-id="5bc07-258">Decimal</span></span> |
| <span data-ttu-id="5bc07-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="5bc07-259">DecimalFloat</span></span> |<span data-ttu-id="5bc07-260">十進位</span><span class="sxs-lookup"><span data-stu-id="5bc07-260">Decimal</span></span> |
| <span data-ttu-id="5bc07-261">數值</span><span class="sxs-lookup"><span data-stu-id="5bc07-261">Numeric</span></span> |<span data-ttu-id="5bc07-262">十進位</span><span class="sxs-lookup"><span data-stu-id="5bc07-262">Decimal</span></span> |
| <span data-ttu-id="5bc07-263">Date</span><span class="sxs-lookup"><span data-stu-id="5bc07-263">Date</span></span> |<span data-ttu-id="5bc07-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="5bc07-264">DateTime</span></span> |
| <span data-ttu-id="5bc07-265">時間</span><span class="sxs-lookup"><span data-stu-id="5bc07-265">Time</span></span> |<span data-ttu-id="5bc07-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="5bc07-266">TimeSpan</span></span> |
| <span data-ttu-id="5bc07-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="5bc07-267">Timestamp</span></span> |<span data-ttu-id="5bc07-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="5bc07-268">DateTime</span></span> |
| <span data-ttu-id="5bc07-269">xml</span><span class="sxs-lookup"><span data-stu-id="5bc07-269">Xml</span></span> |<span data-ttu-id="5bc07-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5bc07-270">Byte[]</span></span> |
| <span data-ttu-id="5bc07-271">Char</span><span class="sxs-lookup"><span data-stu-id="5bc07-271">Char</span></span> |<span data-ttu-id="5bc07-272">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-272">String</span></span> |
| <span data-ttu-id="5bc07-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="5bc07-273">VarChar</span></span> |<span data-ttu-id="5bc07-274">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-274">String</span></span> |
| <span data-ttu-id="5bc07-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="5bc07-275">LongVarChar</span></span> |<span data-ttu-id="5bc07-276">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-276">String</span></span> |
| <span data-ttu-id="5bc07-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="5bc07-277">DB2DynArray</span></span> |<span data-ttu-id="5bc07-278">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-278">String</span></span> |
| <span data-ttu-id="5bc07-279">Binary</span><span class="sxs-lookup"><span data-stu-id="5bc07-279">Binary</span></span> |<span data-ttu-id="5bc07-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5bc07-280">Byte[]</span></span> |
| <span data-ttu-id="5bc07-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="5bc07-281">VarBinary</span></span> |<span data-ttu-id="5bc07-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5bc07-282">Byte[]</span></span> |
| <span data-ttu-id="5bc07-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="5bc07-283">LongVarBinary</span></span> |<span data-ttu-id="5bc07-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5bc07-284">Byte[]</span></span> |
| <span data-ttu-id="5bc07-285">圖形</span><span class="sxs-lookup"><span data-stu-id="5bc07-285">Graphic</span></span> |<span data-ttu-id="5bc07-286">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-286">String</span></span> |
| <span data-ttu-id="5bc07-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="5bc07-287">VarGraphic</span></span> |<span data-ttu-id="5bc07-288">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-288">String</span></span> |
| <span data-ttu-id="5bc07-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="5bc07-289">LongVarGraphic</span></span> |<span data-ttu-id="5bc07-290">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-290">String</span></span> |
| <span data-ttu-id="5bc07-291">Clob</span><span class="sxs-lookup"><span data-stu-id="5bc07-291">Clob</span></span> |<span data-ttu-id="5bc07-292">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-292">String</span></span> |
| <span data-ttu-id="5bc07-293">Blob</span><span class="sxs-lookup"><span data-stu-id="5bc07-293">Blob</span></span> |<span data-ttu-id="5bc07-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5bc07-294">Byte[]</span></span> |
| <span data-ttu-id="5bc07-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="5bc07-295">DbClob</span></span> |<span data-ttu-id="5bc07-296">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-296">String</span></span> |
| <span data-ttu-id="5bc07-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="5bc07-297">SmallInt</span></span> |<span data-ttu-id="5bc07-298">Int16</span><span class="sxs-lookup"><span data-stu-id="5bc07-298">Int16</span></span> |
| <span data-ttu-id="5bc07-299">Integer</span><span class="sxs-lookup"><span data-stu-id="5bc07-299">Integer</span></span> |<span data-ttu-id="5bc07-300">Int32</span><span class="sxs-lookup"><span data-stu-id="5bc07-300">Int32</span></span> |
| <span data-ttu-id="5bc07-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="5bc07-301">BigInt</span></span> |<span data-ttu-id="5bc07-302">Int64</span><span class="sxs-lookup"><span data-stu-id="5bc07-302">Int64</span></span> |
| <span data-ttu-id="5bc07-303">Real</span><span class="sxs-lookup"><span data-stu-id="5bc07-303">Real</span></span> |<span data-ttu-id="5bc07-304">單一</span><span class="sxs-lookup"><span data-stu-id="5bc07-304">Single</span></span> |
| <span data-ttu-id="5bc07-305">兩倍</span><span class="sxs-lookup"><span data-stu-id="5bc07-305">Double</span></span> |<span data-ttu-id="5bc07-306">兩倍</span><span class="sxs-lookup"><span data-stu-id="5bc07-306">Double</span></span> |
| <span data-ttu-id="5bc07-307">Float</span><span class="sxs-lookup"><span data-stu-id="5bc07-307">Float</span></span> |<span data-ttu-id="5bc07-308">兩倍</span><span class="sxs-lookup"><span data-stu-id="5bc07-308">Double</span></span> |
| <span data-ttu-id="5bc07-309">十進位</span><span class="sxs-lookup"><span data-stu-id="5bc07-309">Decimal</span></span> |<span data-ttu-id="5bc07-310">十進位</span><span class="sxs-lookup"><span data-stu-id="5bc07-310">Decimal</span></span> |
| <span data-ttu-id="5bc07-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="5bc07-311">DecimalFloat</span></span> |<span data-ttu-id="5bc07-312">十進位</span><span class="sxs-lookup"><span data-stu-id="5bc07-312">Decimal</span></span> |
| <span data-ttu-id="5bc07-313">數值</span><span class="sxs-lookup"><span data-stu-id="5bc07-313">Numeric</span></span> |<span data-ttu-id="5bc07-314">十進位</span><span class="sxs-lookup"><span data-stu-id="5bc07-314">Decimal</span></span> |
| <span data-ttu-id="5bc07-315">Date</span><span class="sxs-lookup"><span data-stu-id="5bc07-315">Date</span></span> |<span data-ttu-id="5bc07-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="5bc07-316">DateTime</span></span> |
| <span data-ttu-id="5bc07-317">時間</span><span class="sxs-lookup"><span data-stu-id="5bc07-317">Time</span></span> |<span data-ttu-id="5bc07-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="5bc07-318">TimeSpan</span></span> |
| <span data-ttu-id="5bc07-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="5bc07-319">Timestamp</span></span> |<span data-ttu-id="5bc07-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="5bc07-320">DateTime</span></span> |
| <span data-ttu-id="5bc07-321">xml</span><span class="sxs-lookup"><span data-stu-id="5bc07-321">Xml</span></span> |<span data-ttu-id="5bc07-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5bc07-322">Byte[]</span></span> |
| <span data-ttu-id="5bc07-323">Char</span><span class="sxs-lookup"><span data-stu-id="5bc07-323">Char</span></span> |<span data-ttu-id="5bc07-324">String</span><span class="sxs-lookup"><span data-stu-id="5bc07-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="5bc07-325">將來源 toosink 資料行對應</span><span class="sxs-lookup"><span data-stu-id="5bc07-325">Map source toosink columns</span></span>
<span data-ttu-id="5bc07-326">如何 toomap 資料行中 hello 來源資料集 toocolumns hello 接收的資料集，請參閱的 toolearn [Azure Data Factory 中的資料集資料行對應](data-factory-map-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc07-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="5bc07-327">從關聯式來源進行可重複的讀取</span><span class="sxs-lookup"><span data-stu-id="5bc07-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="5bc07-328">時，您從關聯式資料存放區複製資料，請注意注意 tooavoid 重複性非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="5bc07-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="5bc07-329">在 Azure Data Factory 中，您可以手動重新執行配量。</span><span class="sxs-lookup"><span data-stu-id="5bc07-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5bc07-330">您也可以設定 hello 重試**原則**屬性的資料集 toorerun 配量時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bc07-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="5bc07-331">請確定的 hello 相同資料如何讀取無論多次 hello 配量是重新執行，以及如何重新執行 hello 配量而定。</span><span class="sxs-lookup"><span data-stu-id="5bc07-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="5bc07-332">如需詳細資訊，請參閱[從關聯式來源進行可重複的讀取](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)。</span><span class="sxs-lookup"><span data-stu-id="5bc07-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5bc07-333">效能和微調</span><span class="sxs-lookup"><span data-stu-id="5bc07-333">Performance and tuning</span></span>
<span data-ttu-id="5bc07-334">深入了解會影響在 hello 複製活動以及方式 toooptimize 效能 hello 效能的關鍵因素[複製活動效能和調整指南](data-factory-copy-activity-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc07-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
