---
title: "將 SQL 資料倉儲資料的 aaaLoad tb |Microsoft 文件"
description: "示範如何使用 Azure Data Factory 在 15 分鐘內將 1 TB 的資料載入至 Azure SQL 資料倉儲"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="d8621-103">使用 Data Factory 在 15 分鐘內將 1 TB 載入至 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="d8621-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="d8621-104">[Azure SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)是一種雲端架構、相應放大的資料庫，可處理巨量關聯式與非關聯式資料。</span><span class="sxs-lookup"><span data-stu-id="d8621-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="d8621-105">SQL 資料倉儲是以巨量平行處理 (MPP) 架構為基礎，最適用於企業資料倉儲工作負載。</span><span class="sxs-lookup"><span data-stu-id="d8621-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="d8621-106">它提供彈性與 hello 彈性 tooscale 存放裝置的雲端及獨立計算。</span><span class="sxs-lookup"><span data-stu-id="d8621-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="d8621-107">現在，使用 Azure SQL 資料倉儲比之前使用 **Azure Data Factory** 還要簡單。</span><span class="sxs-lookup"><span data-stu-id="d8621-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="d8621-108">Azure Data Factory 是完全受管理的雲端式資料的整合服務，它可以是使用的 toopopulate SQL 資料倉儲的 hello 資料，從您現有的系統，並節省您寶貴的時間時評估 SQL 資料倉儲和建置您的分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="d8621-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="d8621-109">以下是 hello 的資料載入到 Azure SQL 資料倉儲使用 Azure Data Factory 的主要優點：</span><span class="sxs-lookup"><span data-stu-id="d8621-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="d8621-110">**向上輕鬆 tooset**: 5 步驟直覺式精靈沒有需要的指令碼。</span><span class="sxs-lookup"><span data-stu-id="d8621-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="d8621-111">**豐富的資料存放區支援**︰一組豐富內部部署和雲端架構資料存放區的內部支援。</span><span class="sxs-lookup"><span data-stu-id="d8621-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="d8621-112">**安全且相容**： 資料經由 HTTPS 或 ExpressRoute，傳送和全域服務組態選項可確保您的資料永遠不會離開 hello 地理界限</span><span class="sxs-lookup"><span data-stu-id="d8621-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="d8621-113">**前所未有的效能，使用 PolyBase** – 使用 Polybase 是 hello 最有效率的方式 toomove 資料到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="d8621-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="d8621-114">您可以使用 hello 暫存 blob 」 功能，來達到高負載速度從 hello Polybase 支援預設的 Azure Blob 儲存體，以外的資料存放區的所有類型。</span><span class="sxs-lookup"><span data-stu-id="d8621-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="d8621-115">本文章將示範如何 toouse 資料 Factory 複製精靈 tooload 1 TB 資料從 Azure Blob 儲存體到 Azure SQL 資料倉儲中在 15 分鐘，超過 1.2 GBps 輸送量。</span><span class="sxs-lookup"><span data-stu-id="d8621-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="d8621-116">本文章提供將資料移到 Azure SQL 資料倉儲中，使用 hello 複製精靈的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="d8621-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="d8621-117">一般功能相關資訊的 Data Factory 中將資料移至 azure 或從 Azure SQL 資料倉儲，請參閱[從 Azure SQL 資料倉儲使用 Azure Data Factory 中移動資料 tooand](data-factory-azure-sql-data-warehouse-connector.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="d8621-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="d8621-118">您也可以使用 Azure 入口網站、Visual Studio、PowerShell 等來建置管線。請參閱[教學課程： 將資料從 Azure Blob tooAzure SQL Database 複製](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)快速逐步解說中，使用 Azure Data Factory 中的 hello 複製活動的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="d8621-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="d8621-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="d8621-119">Prerequisites</span></span>
* <span data-ttu-id="d8621-120">Azure Blob 儲存體︰這項實驗使用 Azure Blob 儲存體 (GRS) 來儲存 TPC-H 測試資料集。</span><span class="sxs-lookup"><span data-stu-id="d8621-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="d8621-121">如果您沒有 Azure 儲存體帳戶，了解[如何 toocreate 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="d8621-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="d8621-122">[-](http://www.tpc.org/tpch/)資料： 我們 toouse-因為 hello 測試資料集內。</span><span class="sxs-lookup"><span data-stu-id="d8621-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="d8621-123">您需要 toouse toodo `dbgen` TPC H toolkit，這可協助您產生 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="d8621-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="d8621-124">您可以下載原始程式碼`dbgen`從[TPC 工具](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp)自己，或從下載 hello 編譯二進位檔進行編譯[GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools)。</span><span class="sxs-lookup"><span data-stu-id="d8621-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="d8621-125">執行的 dbgen.exe hello 下列命令為 toogenerate 1TB 一般檔案`lineitem`資料表散佈跨 10 個檔案：</span><span class="sxs-lookup"><span data-stu-id="d8621-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="d8621-126">…</span><span class="sxs-lookup"><span data-stu-id="d8621-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="d8621-127">目前複製 hello 產生檔案 tooAzure Blob。</span><span class="sxs-lookup"><span data-stu-id="d8621-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="d8621-128">參照太[使用 Azure Data Factory，從內部部署檔案系統移動資料 tooand](data-factory-onprem-file-system-connector.md)如何 toodo，使用 ADF 複製。</span><span class="sxs-lookup"><span data-stu-id="d8621-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="d8621-129">Azure SQL 資料倉儲︰這項實驗會將資料載入至使用 6,000 個 DWU 所建立的 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="d8621-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="d8621-130">請參閱太[建立 Azure SQL 資料倉儲](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md)如詳細說明如何 toocreate SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8621-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="d8621-131">tooget hello 最佳可能的負載效能到使用 Polybase 的 SQL 資料倉儲，我們選擇的資料倉儲單位 (Dwu) hello 效能設定，也就是 6000 的 Dwu 中允許的數目上限。</span><span class="sxs-lookup"><span data-stu-id="d8621-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d8621-132">載入時從 Azure Blob，hello 資料載入效能是與呈現直接正比 toohello Dwu hello SQL 資料倉儲設定的數目：</span><span class="sxs-lookup"><span data-stu-id="d8621-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="d8621-133">將 1 TB 載入至 1,000 個 DWU SQL 資料倉儲需要 87 分鐘 (~200MBps 輸送量) 將 1 TB 載入至 2,000 個 DWU SQL 資料倉儲需要 46 分鐘 (~380MBps 輸送量) 將 1 TB 載入至 6,000 個 DWU SQL 資料倉儲需要 14 分鐘 (~1.2GBps 輸送量)</span><span class="sxs-lookup"><span data-stu-id="d8621-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="d8621-134">SQL 資料倉儲與 6000 的 Dwu toocreate hello 效能滑桿所有 hello 方式 toohello 向右移動：</span><span class="sxs-lookup"><span data-stu-id="d8621-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![效能滑桿](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="d8621-136">針對未設定 6,000 個 DWU 的現有資料庫，您可以使用 Azure 入口網站相應進行增加。</span><span class="sxs-lookup"><span data-stu-id="d8621-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="d8621-137">瀏覽 toohello 在 Azure 入口網站的資料庫，而且沒有**標尺**按鈕在 hello**概觀**面板 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="d8621-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![[調整] 按鈕](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="d8621-139">按一下 hello**標尺**按鈕 tooopen hello 下列 面板，移動滑桿 toohello 最大值 hello，然後按一下**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d8621-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![[調整] 對話方塊](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="d8621-141">這項實驗會將資料載入至使用 `xlargerc` 資源類別的 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="d8621-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="d8621-142">tooachieve 最佳可能輸送量，複本需要 toobe 執行使用 SQL 資料倉儲使用者屬於太`xlargerc`資源類別。</span><span class="sxs-lookup"><span data-stu-id="d8621-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="d8621-143">深入了解如何 toodo，依照[變更使用者資源類別範例](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example)。</span><span class="sxs-lookup"><span data-stu-id="d8621-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="d8621-144">執行 DDL 陳述式之後的 hello Azure SQL 資料倉儲資料庫中建立目的地資料表的結構描述：</span><span class="sxs-lookup"><span data-stu-id="d8621-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="d8621-145">有了 hello 先決條件步驟完成，我們現在都會使用 hello 複製精靈 」 準備好 tooconfigure hello 複製活動。</span><span class="sxs-lookup"><span data-stu-id="d8621-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="d8621-146">啟動複製精靈</span><span class="sxs-lookup"><span data-stu-id="d8621-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="d8621-147">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d8621-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d8621-148">按一下**+ 新增**從 hello 左上角，按一下 **智慧 + 分析**，然後按一下**Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="d8621-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="d8621-149">在 hello**新的 data factory**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="d8621-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="d8621-150">輸入**LoadIntoSQLDWDataFactory** hello**名稱**。</span><span class="sxs-lookup"><span data-stu-id="d8621-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="d8621-151">hello hello Azure data factory 的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="d8621-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="d8621-152">如果您收到 hello 錯誤： **Data factory 名稱"LoadIntoSQLDWDataFactory"不是使用**、 變更 hello hello data factory (例如，yournameLoadIntoSQLDWDataFactory) 名稱，然後再次嘗試重新建立。</span><span class="sxs-lookup"><span data-stu-id="d8621-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="d8621-153">請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。</span><span class="sxs-lookup"><span data-stu-id="d8621-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="d8621-154">選取您的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d8621-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="d8621-155">資源群組，請執行步驟的 hello 其中一項：</span><span class="sxs-lookup"><span data-stu-id="d8621-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="d8621-156">選取**使用現有**tooselect 現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d8621-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="d8621-157">選取**建立新**tooenter 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="d8621-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="d8621-158">選取**位置**hello data factory。</span><span class="sxs-lookup"><span data-stu-id="d8621-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="d8621-159">選取**Pin toodashboard**在 hello hello 刀鋒視窗底部的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d8621-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="d8621-160">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d8621-160">Click **Create**.</span></span>
4. <span data-ttu-id="d8621-161">Hello 建立完成之後，您會看到 hello **Data Factory**刀鋒視窗中 hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="d8621-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Data Factory 首頁](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="d8621-163">在 hello Data Factory 首頁上，按一下 hello**將資料複製**磚 toolaunch**複製精靈**。</span><span class="sxs-lookup"><span data-stu-id="d8621-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d8621-164">如果您看到該 hello 網頁瀏覽器卡在 [授權]，停用/取消核取**封鎖第三方 cookie 和站台資料**設定 （或） 保留啟用它，並建立的例外狀況**login.microsoftonline.com**，然後再次嘗試重新啟動 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="d8621-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="d8621-165">步驟 1︰設定資料載入排程</span><span class="sxs-lookup"><span data-stu-id="d8621-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="d8621-166">hello 第一個步驟是 tooconfigure hello 資料載入排程。</span><span class="sxs-lookup"><span data-stu-id="d8621-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="d8621-167">在 hello**屬性**頁面：</span><span class="sxs-lookup"><span data-stu-id="d8621-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="d8621-168">輸入 **CopyFromBlobToAzureSqlDataWarehouse** 作為 [工作名稱]</span><span class="sxs-lookup"><span data-stu-id="d8621-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="d8621-169">選取 [立即執行一次] 選項。</span><span class="sxs-lookup"><span data-stu-id="d8621-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="d8621-170">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d8621-170">Click **Next**.</span></span>  

    ![複製精靈 - 屬性頁面](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="d8621-172">步驟 2：設定來源</span><span class="sxs-lookup"><span data-stu-id="d8621-172">Step 2: Configure source</span></span>
<span data-ttu-id="d8621-173">此區段會顯示 hello 步驟 tooconfigure hello 來源： Azure Blob 包含 hello 1 TB TPC-H 明細項目檔案。</span><span class="sxs-lookup"><span data-stu-id="d8621-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="d8621-174">選取 hello **Azure Blob 儲存體**hello 資料存放區，並按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d8621-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![複製精靈 - 選取來源頁面](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="d8621-176">填寫 hello 連線資訊 hello Azure Blob 儲存體帳戶，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d8621-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![複製精靈 - 來源連接資訊](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="d8621-178">選擇 hello**資料夾**包含 hello TPC H 行項目檔案並按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d8621-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![複製精靈 - 選取輸入資料夾](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="d8621-180">按一下後**下一步**，系統會自動偵測 hello 檔案格式設定。</span><span class="sxs-lookup"><span data-stu-id="d8621-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="d8621-181">請確定該資料行分隔符號是 toomake ' | '而不是 hello 預設逗號'，'。</span><span class="sxs-lookup"><span data-stu-id="d8621-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="d8621-182">按一下**下一步**預覽 hello 資料之後。</span><span class="sxs-lookup"><span data-stu-id="d8621-182">Click **Next** after you have previewed hello data.</span></span>

    ![複製精靈 - 檔案格式設定](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="d8621-184">步驟 3︰設定目的地</span><span class="sxs-lookup"><span data-stu-id="d8621-184">Step 3: Configure destination</span></span>
<span data-ttu-id="d8621-185">此區段會顯示您如何 tooconfigure hello 目的地： `lineitem` hello Azure SQL 資料倉儲資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="d8621-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="d8621-186">選擇**Azure SQL 資料倉儲**做為 hello 目的地存放區，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d8621-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![複製精靈 - 選取目的地資料存放區](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="d8621-188">填寫 hello Azure SQL 資料倉儲的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="d8621-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="d8621-189">請確定您指定 hello 使用者 hello 角色的成員`xlargerc`(請參閱 hello**必要條件**一節以取得詳細指示)，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d8621-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![複製精靈 - 目的地連接資訊](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="d8621-191">選擇 hello 目的地資料表，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="d8621-191">Choose hello destination table and click **Next**.</span></span>

    ![複製精靈 - 資料表對應頁面](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="d8621-193">在 [結構描述對應] 頁面中，將 [套用資料行對應] 選項保持不選取，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d8621-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="d8621-194">步驟 4：效能設定</span><span class="sxs-lookup"><span data-stu-id="d8621-194">Step 4: Performance settings</span></span>

<span data-ttu-id="d8621-195">預設會核取 [允許 Polybase]。</span><span class="sxs-lookup"><span data-stu-id="d8621-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="d8621-196">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="d8621-196">Click **Next**.</span></span>

![複製精靈 - 結構描述對應頁面](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="d8621-198">步驟 5︰部署和監視載入結果</span><span class="sxs-lookup"><span data-stu-id="d8621-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="d8621-199">按一下**完成**按鈕 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="d8621-199">Click **Finish** button toodeploy.</span></span>

    ![複製精靈 - 摘要頁面](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="d8621-201">Hello 部署完成後，按一下`Click here toomonitor copy pipeline`toomonitor hello 複製執行進度。</span><span class="sxs-lookup"><span data-stu-id="d8621-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="d8621-202">您建立在 hello 選取 hello 複製管線**活動 Windows**清單。</span><span class="sxs-lookup"><span data-stu-id="d8621-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![複製精靈 - 摘要頁面](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="d8621-204">您可以檢視詳細資料以 hello hello 複製**活動視窗總管**在 hello 右面板中，包括 hello 資料磁碟區從來源讀取和寫入目的地、 期間與 hello hello 執行的平均輸送量。</span><span class="sxs-lookup"><span data-stu-id="d8621-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="d8621-205">您可以從下列螢幕擷取畫面中，將 1 TB 從 Azure Blob 儲存體複製到 SQL 資料倉儲的 hello 看到花費了 14 分鐘，有效地達成需要 1.22 GBps 輸送量 ！</span><span class="sxs-lookup"><span data-stu-id="d8621-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![複製精靈 - 成功對話方塊](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="d8621-207">最佳作法</span><span class="sxs-lookup"><span data-stu-id="d8621-207">Best practices</span></span>
<span data-ttu-id="d8621-208">以下是執行 Azure SQL 資料倉儲資料庫的一些最佳作法：</span><span class="sxs-lookup"><span data-stu-id="d8621-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="d8621-209">載入至 CLUSTERED COLUMNSTORE INDEX 時，請使用較大的資源類別。</span><span class="sxs-lookup"><span data-stu-id="d8621-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="d8621-210">對於更有效率的聯結，請考慮透過選取資料行使用雜湊散發，而不是預設循環配置資源散發。</span><span class="sxs-lookup"><span data-stu-id="d8621-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="d8621-211">若要更快的載入速度，請考慮使用暫時性資料的堆積。</span><span class="sxs-lookup"><span data-stu-id="d8621-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="d8621-212">在您完成載入 Azure SQL 資料倉儲之後，請建立統計資料。</span><span class="sxs-lookup"><span data-stu-id="d8621-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="d8621-213">如需詳細資料，請參閱 [Azure SQL 資料倉儲最佳作法](../sql-data-warehouse/sql-data-warehouse-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="d8621-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8621-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8621-214">Next steps</span></span>
* <span data-ttu-id="d8621-215">[資料處理站的複製精靈](data-factory-copy-wizard.md)-本文章提供有關 hello 複製精靈的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d8621-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="d8621-216">[複製活動效能及微調指南](data-factory-copy-activity-performance.md)-本文章包含 hello 參考效能測量和微調指南。</span><span class="sxs-lookup"><span data-stu-id="d8621-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
