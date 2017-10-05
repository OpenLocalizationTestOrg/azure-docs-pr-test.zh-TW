---
title: "將資料載入 Azure SQL 資料倉儲 | Microsoft Docs"
description: "了解將資料載入 SQL 資料倉儲的常見案例 這包含使用 PolyBase、Azure Blob 儲存體、一般檔案及寄送磁碟。 您也可以使用協力廠商工具。"
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
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="9db3a-105">將資料載入 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9db3a-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9db3a-106">將資料載入 SQL 資料倉儲之案例選項和建議的摘要。</span><span class="sxs-lookup"><span data-stu-id="9db3a-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="9db3a-107">為載入準備資料通常是載入資料最困難的部分。</span><span class="sxs-lookup"><span data-stu-id="9db3a-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="9db3a-108">Azure 可將 Azure Blob 儲存體做為許多服務的一般資料存放區使用，並使用 Azure Data Factory 來協調 Azure 服務之間的通訊和資料移動來簡化載入。</span><span class="sxs-lookup"><span data-stu-id="9db3a-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="9db3a-109">這些程序會與 PolyBase 技術整合，該技術使用巨量平行處理 (MPP) 來從 Azure Blob 儲存體將資料平行載入到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="9db3a-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="9db3a-110">如需有關載入範例資料庫的教學課程，請參閱[載入範例資料庫][Load sample databases]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="9db3a-111">從 Azure Blob 儲存體載入</span><span class="sxs-lookup"><span data-stu-id="9db3a-111">Load from Azure blob storage</span></span>
<span data-ttu-id="9db3a-112">將資料匯入 SQL 資料倉儲的最快方式，是使用 PolyBase 從 Azure Blob 儲存體載入資料。</span><span class="sxs-lookup"><span data-stu-id="9db3a-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="9db3a-113">PolyBase 使用 SQL 資料倉儲的巨型平行處理 (MPP) 設計，來從 Azure Blob 儲存體平行載入資料。</span><span class="sxs-lookup"><span data-stu-id="9db3a-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="9db3a-114">若要使用 PolyBase，您可以使用 T-SQL 命令或 Azure Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="9db3a-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="9db3a-115">1.使用 PolyBase 和 T-SQL</span><span class="sxs-lookup"><span data-stu-id="9db3a-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="9db3a-116">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="9db3a-116">Summary of loading process:</span></span>

1. <span data-ttu-id="9db3a-117">將您的資料移到 Azure Blob 儲存體或 Azure Data Lake Store，並儲存於文字檔。</span><span class="sxs-lookup"><span data-stu-id="9db3a-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="9db3a-118">設定 SQL 資料倉儲中的外部物件，以定義資料的位置和格式</span><span class="sxs-lookup"><span data-stu-id="9db3a-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="9db3a-119">執行 T-SQL 命令以將資料平行載入新的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="9db3a-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="9db3a-120">如需教學課程，請參閱[從 Azure Blob 儲存體將資料載入 SQL 資料倉儲 (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="9db3a-121">2.使用 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9db3a-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="9db3a-122">如需使用 PolyBase 較簡易的方法，您可以建立使用 PolyBase 將資料從 Azure Blob 儲存體載入 SQL 資料倉儲的 Azure Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="9db3a-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="9db3a-123">由於您不需要定義 T-SQL 物件，使您可以快速完成設定。</span><span class="sxs-lookup"><span data-stu-id="9db3a-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="9db3a-124">如果您需要在不匯入外部資料之下對它做出查詢，請使用 T-SQL。</span><span class="sxs-lookup"><span data-stu-id="9db3a-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="9db3a-125">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="9db3a-125">Summary of loading process:</span></span>

1. <span data-ttu-id="9db3a-126">將您的資料移到 Azure Blob 儲存體，並將它儲存於文字檔中。</span><span class="sxs-lookup"><span data-stu-id="9db3a-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="9db3a-127">Azure Data Factory 目前不支援 ADLS 和 PolyBase 連線。</span><span class="sxs-lookup"><span data-stu-id="9db3a-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="9db3a-128">建立 Azure Data Factory 管線以內嵌資料。</span><span class="sxs-lookup"><span data-stu-id="9db3a-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="9db3a-129">使用 PolyBase 選項。</span><span class="sxs-lookup"><span data-stu-id="9db3a-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="9db3a-130">排程並執行管線。</span><span class="sxs-lookup"><span data-stu-id="9db3a-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="9db3a-131">如需教學課程，請參閱[從 Azure Blob 儲存體將資料載入 SQL 資料倉儲 (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="9db3a-132">從 SQL Server 載入</span><span class="sxs-lookup"><span data-stu-id="9db3a-132">Load from SQL Server</span></span>
<span data-ttu-id="9db3a-133">若要將資料從 SQL Server 載入 SQL 資料倉儲，您可以使用 Integration Services (SSIS)、傳輸一般檔案，或寄送磁碟給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="9db3a-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="9db3a-134">繼續閱讀以查看不同載入程序的摘要，以及教學課程的連結。</span><span class="sxs-lookup"><span data-stu-id="9db3a-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="9db3a-135">若要規劃從 SQL Server 到 SQL 資料倉儲的完整資料移轉，請參閱[移轉概觀][Migration overview]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="9db3a-136">使用 Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="9db3a-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="9db3a-137">如果您已經在使用 Integration Services (SSIS) 套件來載入至 SQL Server，您可以更新套件以使用 SQL Server 做為來源，並使用 SQL 資料倉儲做為目的地。</span><span class="sxs-lookup"><span data-stu-id="9db3a-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="9db3a-138">這是一項快速且簡單的作業，也很適合在您不想移轉載入程序以使用已存在於雲端中之資料的情況下使用。</span><span class="sxs-lookup"><span data-stu-id="9db3a-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="9db3a-139">缺點是載入的速度將會比使用 PolyBase 的情況還慢，因為此 SSIS 並不會以平行的方式執行載入。</span><span class="sxs-lookup"><span data-stu-id="9db3a-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="9db3a-140">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="9db3a-140">Summary of loading process:</span></span>

1. <span data-ttu-id="9db3a-141">修改您的 Integration Services 套件以將來源指向 SQL Server 執行個體，並將目的地指向 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="9db3a-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="9db3a-142">如果您的結構描述尚未移轉至 SQL 資料倉儲，請執行此動作。</span><span class="sxs-lookup"><span data-stu-id="9db3a-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="9db3a-143">將您套件中的對應變更為僅使用 SQL 資料倉儲所支援的資料類型。</span><span class="sxs-lookup"><span data-stu-id="9db3a-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="9db3a-144">排程並執行套件。</span><span class="sxs-lookup"><span data-stu-id="9db3a-144">Schedule and run the package.</span></span>

<span data-ttu-id="9db3a-145">如需教學課程，請參閱[從 SQL Server 將資料載入 Azure SQL 資料倉儲 (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="9db3a-146">使用 AZCopy (建議於資料 < 10 TB 的情況使用)</span><span class="sxs-lookup"><span data-stu-id="9db3a-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="9db3a-147">如果您的資料大小 < 10 TB，您可以從 SQL Server 將資料匯出成一般檔案，將檔案複製到 Azure Blob 儲存體，然後使用 PolyBase 將資料載入至 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9db3a-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="9db3a-148">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="9db3a-148">Summary of loading process:</span></span>

1. <span data-ttu-id="9db3a-149">使用 bcp 命令列公用程式從 SQL Server 將資料匯出成一般檔案。</span><span class="sxs-lookup"><span data-stu-id="9db3a-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="9db3a-150">使用 AZCopy 命令列公用程式將資料從一般檔案複製到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9db3a-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="9db3a-151">使用 PolyBase 來載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="9db3a-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="9db3a-152">如需教學課程，請參閱[從 Azure Blob 儲存體將資料載入 SQL 資料倉儲 (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="9db3a-153">使用 bcp</span><span class="sxs-lookup"><span data-stu-id="9db3a-153">Use bcp</span></span>
<span data-ttu-id="9db3a-154">如果您只有少量的資料，您可以使用 bcp 將資料直接載入至 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="9db3a-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="9db3a-155">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="9db3a-155">Summary of loading process:</span></span>

1. <span data-ttu-id="9db3a-156">使用 bcp 命令列公用程式從 SQL Server 將資料匯出成一般檔案。</span><span class="sxs-lookup"><span data-stu-id="9db3a-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="9db3a-157">使用 bcp 將資料從一般檔案直接載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="9db3a-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="9db3a-158">如需教學課程，請參閱[從 SQL Server 將資料載入 Azure SQL 資料倉儲 (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="9db3a-159">使用匯入/匯出 (建議於資料 > 10 TB 的情況使用)</span><span class="sxs-lookup"><span data-stu-id="9db3a-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="9db3a-160">如果您的資料大小 > 10 TB，且您想將它移至 Azure，我們建議您使用我們的磁碟寄送服務：[匯入/匯出][Import/Export]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="9db3a-161">載入流程的摘要</span><span class="sxs-lookup"><span data-stu-id="9db3a-161">Summary of loading process</span></span>

1. <span data-ttu-id="9db3a-162">使用 bcp 命令列公用程式從 SQL Server 將資料以一般檔案的形式匯出至可轉移磁碟上。</span><span class="sxs-lookup"><span data-stu-id="9db3a-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="9db3a-163">將磁碟寄送給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="9db3a-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="9db3a-164">Microsoft 將資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="9db3a-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="9db3a-165">從 HDInsight 載入</span><span class="sxs-lookup"><span data-stu-id="9db3a-165">Load from HDInsight</span></span>
<span data-ttu-id="9db3a-166">SQL 資料倉儲支援從 HDInsight 透過 PolyBase 載入資料。</span><span class="sxs-lookup"><span data-stu-id="9db3a-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="9db3a-167">此程序和從 Azure Blob 儲存體載入資料相同 - 使用 PolyBase 連接到 HDInsight 以載入資料。</span><span class="sxs-lookup"><span data-stu-id="9db3a-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="9db3a-168">1.使用 PolyBase 和 T-SQL</span><span class="sxs-lookup"><span data-stu-id="9db3a-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="9db3a-169">載入流程的摘要：</span><span class="sxs-lookup"><span data-stu-id="9db3a-169">Summary of loading process:</span></span>

1. <span data-ttu-id="9db3a-170">將您的資料移到 HDInsight，並將它儲存為文字檔、ORC 或 Parquet 格式。</span><span class="sxs-lookup"><span data-stu-id="9db3a-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="9db3a-171">設定 SQL 資料倉儲中的外部物件，以定義資料的位置和格式。</span><span class="sxs-lookup"><span data-stu-id="9db3a-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="9db3a-172">執行 T-SQL 命令以將資料平行載入新的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="9db3a-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="9db3a-173">如需教學課程，請參閱[從 Azure Blob 儲存體將資料載入 SQL 資料倉儲 (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="9db3a-174">建議</span><span class="sxs-lookup"><span data-stu-id="9db3a-174">Recommendations</span></span>
<span data-ttu-id="9db3a-175">我們有許多合作夥伴皆提供載入解決方案。</span><span class="sxs-lookup"><span data-stu-id="9db3a-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="9db3a-176">若要深入了解，請參閱我們的[解決方案合作夥伴][solution partners]清單。</span><span class="sxs-lookup"><span data-stu-id="9db3a-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="9db3a-177">如果您的資料是來自非關聯式來源，且您想要將它載入 SQL 資料倉儲，您在載入之前必須先將它轉換成資料列和資料行。</span><span class="sxs-lookup"><span data-stu-id="9db3a-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="9db3a-178">已轉換的資料並不需要儲存在資料庫中，而可以儲存在文字檔案中。</span><span class="sxs-lookup"><span data-stu-id="9db3a-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="9db3a-179">建立新載入資料的統計資料。</span><span class="sxs-lookup"><span data-stu-id="9db3a-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="9db3a-180">Azure 資料倉儲尚未支援自動建立或自動更新統計資料。</span><span class="sxs-lookup"><span data-stu-id="9db3a-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="9db3a-181">為了獲得查詢的最佳效能，在首次載入資料，或是資料中發生重大變更之後，建立所有資料表的所有資料行統計資料非常重要。</span><span class="sxs-lookup"><span data-stu-id="9db3a-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="9db3a-182">如需詳細資料，請參閱[統計資料][Statistics]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="9db3a-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9db3a-183">Next steps</span></span>
<span data-ttu-id="9db3a-184">如需更多開發祕訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="9db3a-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
