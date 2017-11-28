---
title: "Azure SQL 資料倉儲 aaaLoad 資料 |Microsoft 文件"
description: "了解 hello 常見的資料載入到 SQL 資料倉儲案例。 這包含使用 PolyBase、Azure Blob 儲存體、一般檔案及寄送磁碟。 您也可以使用協力廠商工具。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="b7de7-105">將資料載入 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="b7de7-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="b7de7-106">Hello 的情節選項和建議將 SQL 資料倉儲載入資料的摘要。</span><span class="sxs-lookup"><span data-stu-id="b7de7-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="b7de7-107">hello 困難的部分載入資料的通常準備 hello 資料 hello 負載。</span><span class="sxs-lookup"><span data-stu-id="b7de7-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="b7de7-108">Azure 利用 Azure blob 儲存體做為一般資料存放區，讓許多 hello 服務簡化載入和使用 Azure Data Factory tooorchestrate 之間的通訊和資料移動 hello Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="b7de7-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="b7de7-109">這些程序會與它使用大量平行處理以平行方式從 Azure blob 儲存體 (MPP) tooload 資料到 SQL 資料倉儲 PolyBase 技術整合。</span><span class="sxs-lookup"><span data-stu-id="b7de7-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="b7de7-110">如需有關載入範例資料庫的教學課程，請參閱[載入範例資料庫][Load sample databases]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="b7de7-111">從 Azure Blob 儲存體載入</span><span class="sxs-lookup"><span data-stu-id="b7de7-111">Load from Azure blob storage</span></span>
<span data-ttu-id="b7de7-112">toouse PolyBase tooload 資料從 Azure blob 儲存體 hello 最快方式 tooimport 資料到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b7de7-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="b7de7-113">PolyBase 會使用 SQL 資料倉儲的大量平行處理以平行方式從 Azure blob 儲存體 (MPP) 設計 tooload 資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="b7de7-114">toouse PolyBase，您可以使用 T-SQL 命令或 Azure Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="b7de7-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="b7de7-115">1.使用 PolyBase 和 T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7de7-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="b7de7-116">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="b7de7-116">Summary of loading process:</span></span>

1. <span data-ttu-id="b7de7-117">移動資料 tooAzure blob 儲存體或 Azure 資料湖存放區，並將它儲存在文字檔中。</span><span class="sxs-lookup"><span data-stu-id="b7de7-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="b7de7-118">設定 SQL 資料倉儲 toodefine hello 位置與格式 hello 資料中的外部物件</span><span class="sxs-lookup"><span data-stu-id="b7de7-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="b7de7-119">平行執行 T-SQL 命令 tooload hello 資料到新的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="b7de7-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="b7de7-120">如需教學課程，請參閱[資料從 Azure blob 儲存體 tooSQL 資料倉儲 (PolyBase) 載入][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="b7de7-121">2.使用 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b7de7-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="b7de7-122">更簡單的方式 toouse PolyBase，您可以建立使用 SQL 資料倉儲 PolyBase tooload 資料從 Azure blob 儲存體的 Azure Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="b7de7-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="b7de7-123">這是快速 tooconfigure，因為您不再需要 toodefine hello T-SQL 物件。</span><span class="sxs-lookup"><span data-stu-id="b7de7-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="b7de7-124">如果您未匯入需要 tooquery hello 外部資料，請使用 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="b7de7-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="b7de7-125">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="b7de7-125">Summary of loading process:</span></span>

1. <span data-ttu-id="b7de7-126">移動資料 tooAzure blob 儲存體，並將它儲存在文字檔中。</span><span class="sxs-lookup"><span data-stu-id="b7de7-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="b7de7-127">Azure Data Factory 目前不支援 ADLS 和 PolyBase 連線。</span><span class="sxs-lookup"><span data-stu-id="b7de7-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="b7de7-128">建立 Azure Data Factory 管線 tooingest hello 資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="b7de7-129">使用 hello PolyBase 選項。</span><span class="sxs-lookup"><span data-stu-id="b7de7-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="b7de7-130">排程和執行 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="b7de7-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="b7de7-131">如需教學課程，請參閱[資料從 Azure blob 儲存體 tooSQL 資料倉儲 (Azure Data Factory) 載入][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="b7de7-132">從 SQL Server 載入</span><span class="sxs-lookup"><span data-stu-id="b7de7-132">Load from SQL Server</span></span>
<span data-ttu-id="b7de7-133">tooload 資料從 SQL Server tooSQL 您可以使用 Integration Services (SSIS) 資料倉儲會傳送一般檔案，或寄送磁碟 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="b7de7-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="b7de7-134">閱讀 toosee hello 不同載入處理序和連結 tootutorials 的摘要。</span><span class="sxs-lookup"><span data-stu-id="b7de7-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="b7de7-135">tooplan 來自 SQL Server tooSQL 資料倉儲，完整的資料移轉，請參閱 hello[移轉概觀][Migration overview]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="b7de7-136">使用 Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="b7de7-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="b7de7-137">如果您已經在使用 SQL server Integration Services (SSIS) 封裝 tooload，您可以更新您為 hello 來源和 SQL 資料倉儲，做為 hello 目的地的封裝 toouse SQL Server。</span><span class="sxs-lookup"><span data-stu-id="b7de7-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="b7de7-138">這是快速和輕鬆 toodo，是不錯的選擇，如果您不想 toomigrate 您載入和處理 toouse 已經在 hello 雲端中的資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="b7de7-139">hello 代價是 hello 負載將會比使用 PolyBase，因為此 SSIS 不會以平行方式執行 hello 負載變慢。</span><span class="sxs-lookup"><span data-stu-id="b7de7-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="b7de7-140">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="b7de7-140">Summary of loading process:</span></span>

1. <span data-ttu-id="b7de7-141">請修訂您 Integration Services 封裝 toopoint toohello SQL Server 執行個體 hello 來源和目的地 hello 的 hello SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="b7de7-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="b7de7-142">如果它尚未有，移轉您的結構描述 tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b7de7-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="b7de7-143">在封裝中的變更 hello 對應僅使用 hello 資料類型所支援的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b7de7-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="b7de7-144">排程和執行 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="b7de7-144">Schedule and run hello package.</span></span>

<span data-ttu-id="b7de7-145">如需教學課程，請參閱[從 SQL Server tooAzure SQL 資料倉儲 (SSIS) 資料載入][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="b7de7-146">使用 AZCopy (建議於資料 < 10 TB 的情況使用)</span><span class="sxs-lookup"><span data-stu-id="b7de7-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="b7de7-147">如果 < 10 TB 的資料大小，您可以從 SQL Server tooflat 檔案匯出 hello 資料、 將複製 hello 檔案 tooAzure blob 儲存體，並再使用 PolyBase tooload hello 資料到 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="b7de7-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="b7de7-148">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="b7de7-148">Summary of loading process:</span></span>

1. <span data-ttu-id="b7de7-149">使用 SQL Server tooflat 檔案 hello bcp 命令列公用程式 tooexport 資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="b7de7-150">使用 hello AZCopy 命令列公用程式 toocopy 資料從一般檔案 tooAzure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="b7de7-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="b7de7-151">使用 PolyBase tooload 到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b7de7-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="b7de7-152">如需教學課程，請參閱[資料從 Azure blob 儲存體 tooSQL 資料倉儲 (PolyBase) 載入][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="b7de7-153">使用 bcp</span><span class="sxs-lookup"><span data-stu-id="b7de7-153">Use bcp</span></span>
<span data-ttu-id="b7de7-154">如果您有少量資料您可以使用 bcp tooload 直接在 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b7de7-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="b7de7-155">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="b7de7-155">Summary of loading process:</span></span>

1. <span data-ttu-id="b7de7-156">使用 SQL Server tooflat 檔案 hello bcp 命令列公用程式 tooexport 資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="b7de7-157">使用 bcp tooload 資料從一般檔案直接 tooSQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="b7de7-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="b7de7-158">如需教學課程，請參閱[資料從 SQL Server tooAzure SQL 資料倉儲 (bcp) 載入][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="b7de7-159">使用匯入/匯出 (建議於資料 > 10 TB 的情況使用)</span><span class="sxs-lookup"><span data-stu-id="b7de7-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="b7de7-160">如果您的資料大小 > 10 TB，而且您想 toomove 它 tooAzure，建議您將傳送服務我們磁碟[匯入/匯出][Import/Export]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="b7de7-161">載入流程的摘要</span><span class="sxs-lookup"><span data-stu-id="b7de7-161">Summary of loading process</span></span>

1. <span data-ttu-id="b7de7-162">使用可傳輸的磁碟上的 SQL Server tooflat 檔案 hello bcp 命令列公用程式 tooexport 資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="b7de7-163">出貨 hello 磁碟 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="b7de7-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="b7de7-164">Microsoft 會將 SQL 資料倉儲 hello 資料載入</span><span class="sxs-lookup"><span data-stu-id="b7de7-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="b7de7-165">從 HDInsight 載入</span><span class="sxs-lookup"><span data-stu-id="b7de7-165">Load from HDInsight</span></span>
<span data-ttu-id="b7de7-166">SQL 資料倉儲支援從 HDInsight 透過 PolyBase 載入資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="b7de7-167">hello 程序是 hello 與從 Azure Blob 儲存體-使用 PolyBase tooconnect tooHDInsight tooload 資料載入資料相同。</span><span class="sxs-lookup"><span data-stu-id="b7de7-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="b7de7-168">1.使用 PolyBase 和 T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7de7-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="b7de7-169">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="b7de7-169">Summary of loading process:</span></span>

1. <span data-ttu-id="b7de7-170">移動資料 tooHDInsight 並將它儲存在文字檔、 ORC 或 Parquet 格式。</span><span class="sxs-lookup"><span data-stu-id="b7de7-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="b7de7-171">SQL 資料倉儲 toodefine hello 位置及 hello 資料的格式設定外部物件。</span><span class="sxs-lookup"><span data-stu-id="b7de7-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="b7de7-172">平行執行 T-SQL 命令 tooload hello 資料到新的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="b7de7-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="b7de7-173">如需教學課程，請參閱[資料從 Azure blob 儲存體 tooSQL 資料倉儲 (PolyBase) 載入][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="b7de7-174">建議</span><span class="sxs-lookup"><span data-stu-id="b7de7-174">Recommendations</span></span>
<span data-ttu-id="b7de7-175">我們有許多合作夥伴皆提供載入解決方案。</span><span class="sxs-lookup"><span data-stu-id="b7de7-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="b7de7-176">toofind 出的詳細資訊，請參閱一份我們[解決方案合作夥伴][solution partners]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="b7de7-177">如果您的資料來自非關聯式資料來源，而且您想 tooload 到 SQL 資料倉儲您將需要 tootransform 成資料列和資料行之前將其載入它。</span><span class="sxs-lookup"><span data-stu-id="b7de7-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="b7de7-178">hello 轉換的資料不需要 toobe 儲存在資料庫中，可以將訊息儲存在文字檔中。</span><span class="sxs-lookup"><span data-stu-id="b7de7-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="b7de7-179">建立新載入資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="b7de7-180">Azure 資料倉儲尚未支援自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="b7de7-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="b7de7-181">順序 tooget hello 最佳效能降低從您的查詢，請務必 toocreate hello 之後的所有資料表的所有資料行的統計資料先載入或 hello 資料會發生任何大量變更。</span><span class="sxs-lookup"><span data-stu-id="b7de7-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="b7de7-182">如需詳細資料，請參閱[統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7de7-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7de7-183">Next steps</span></span>
<span data-ttu-id="b7de7-184">如需開發秘訣，請參閱 hello[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="b7de7-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
