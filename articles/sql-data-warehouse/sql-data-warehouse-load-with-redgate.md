---
title: "aaaUse Redgate tooload 資料 tooyour Azure 資料倉儲 |Microsoft 文件"
description: "深入了解如何針對資料倉儲案例 toouse Redgate 資料平台 Studio。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="e999a-103">使用 Redgate 資料平台 Studio 載入資料</span><span class="sxs-lookup"><span data-stu-id="e999a-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e999a-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="e999a-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="e999a-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="e999a-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="e999a-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="e999a-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="e999a-107">BCP</span><span class="sxs-lookup"><span data-stu-id="e999a-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="e999a-108">本教學課程示範如何 toouse [Redgate 的資料平台 Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DP) toomove 資料從內部部署 SQL Server tooAzure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e999a-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="e999a-109">資料平台 Studio 套用 hello 最適當的相容性修正程式，並最佳化，所以其 quickest hello 方式 tooget 開始使用 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e999a-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="e999a-110">[Redgate](http://www.red-gate.com) 是長期的 Microsoft 合作夥伴，提供各種 SQL Server 工具。</span><span class="sxs-lookup"><span data-stu-id="e999a-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="e999a-111">在資料平台 Studio 中的這項功能已免費提供商業和非商業使用。</span><span class="sxs-lookup"><span data-stu-id="e999a-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="e999a-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="e999a-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="e999a-113">建立或識別資源</span><span class="sxs-lookup"><span data-stu-id="e999a-113">Create or identify resources</span></span>
<span data-ttu-id="e999a-114">開始之前本教學課程，您需要 toohave:</span><span class="sxs-lookup"><span data-stu-id="e999a-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="e999a-115">**在內部部署 SQL Server 資料庫**: hello 想 tooimport tooSQL 資料倉儲需要從內部部署 SQL Server toocome 資料 (版本 2008 r2 或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="e999a-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="e999a-116">資料平台 Studio 無法直接從 Azure SQL Database 或文字檔匯入資料。</span><span class="sxs-lookup"><span data-stu-id="e999a-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="e999a-117">**Azure 儲存體帳戶**： 資料平台 Studio 設置 hello Azure Blob 儲存體中的資料載入到 SQL 資料倉儲之前。</span><span class="sxs-lookup"><span data-stu-id="e999a-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="e999a-118">hello 儲存體帳戶都必須使用 hello 「 資源管理員 」 部署模型 （hello 預設值） 而不 hello 「 傳統 」 部署模型。</span><span class="sxs-lookup"><span data-stu-id="e999a-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="e999a-119">如果您沒有儲存體帳戶，了解如何 tooCreate 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e999a-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="e999a-120">**SQL 資料倉儲**： 本教學課程移動 hello 資料從內部部署 SQL Server tooSQL 資料倉儲，因此您需要 toohave 資料倉儲線上。</span><span class="sxs-lookup"><span data-stu-id="e999a-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="e999a-121">如果您已經沒有資料倉儲，了解如何 tooCreate Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e999a-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="e999a-122">如果 hello 儲存體帳戶和 hello 資料倉儲中建立 hello 相同提升的效能區域。</span><span class="sxs-lookup"><span data-stu-id="e999a-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="e999a-123">步驟 1： 登入 tooData Studio 平台與 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e999a-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="e999a-124">開啟網頁瀏覽器並瀏覽 toohello[資料平台 Studio](https://www.dataplatformstudio.com/)網站。</span><span class="sxs-lookup"><span data-stu-id="e999a-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="e999a-125">登入與 hello 相同 Azure 帳戶，您使用的 toocreate hello 儲存體帳戶和資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="e999a-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="e999a-126">如果您的電子郵件地址是工作或學校帳戶和 Microsoft 帳戶相關聯，是確定 toochoose hello 帳戶具有存取 tooyour 資源。</span><span class="sxs-lookup"><span data-stu-id="e999a-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="e999a-127">這是您第一次使用的資料平台 Studio 時，如果您是系統 toogrant hello 應用程式的權限 toomanage 要求您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="e999a-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="e999a-128">步驟 2： 開始 hello 匯入精靈</span><span class="sxs-lookup"><span data-stu-id="e999a-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="e999a-129">在 hello DP 主畫面上，選取 [hello 匯入 tooAzure SQL 資料倉儲連結 toostart hello 匯入精靈]。</span><span class="sxs-lookup"><span data-stu-id="e999a-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="e999a-130">步驟 3： 安裝 hello 資料平台 Studio 閘道</span><span class="sxs-lookup"><span data-stu-id="e999a-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="e999a-131">tooconnect tooyour 在內部部署 SQL Server 資料庫，您必須 tooinstall hello DP 閘道。</span><span class="sxs-lookup"><span data-stu-id="e999a-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="e999a-132">hello 閘道是用戶端代理程式，提供存取 tooyour 在內部部署環境中，擷取 hello 資料，然後將它上載 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e999a-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="e999a-133">您的資料永遠不會通過 Redgate 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e999a-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="e999a-134">tooinstall hello 閘道：</span><span class="sxs-lookup"><span data-stu-id="e999a-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="e999a-135">按一下 hello**建立閘道**連結</span><span class="sxs-lookup"><span data-stu-id="e999a-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="e999a-136">下載並安裝 hello 閘道使用 hello 提供安裝程式</span><span class="sxs-lookup"><span data-stu-id="e999a-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="e999a-137">hello 閘道可以安裝在與網路存取 toohello 來源 SQL Server 資料庫的任何電腦上。</span><span class="sxs-lookup"><span data-stu-id="e999a-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="e999a-138">它會存取 hello hello hello 目前使用者的認證搭配使用 Windows 驗證的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e999a-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="e999a-139">安裝之後，hello 閘道狀態變更 tooConnected，您可以選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="e999a-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="e999a-140">步驟 4： 識別 hello 來源資料庫</span><span class="sxs-lookup"><span data-stu-id="e999a-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="e999a-141">在 hello*輸入伺服器名稱*文字方塊中，輸入 hello hello 伺服器裝載您的資料庫名稱，然後選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e999a-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="e999a-142">然後，從 hello 下拉式選單，選取您想要從 tooimport 資料 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e999a-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="e999a-143">DP 會檢查資料表 tooimport hello 選取的資料庫。</span><span class="sxs-lookup"><span data-stu-id="e999a-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="e999a-144">根據預設，DP 匯入 hello 資料庫中的所有 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="e999a-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="e999a-145">您可以選取或取消選取資料表，方法是展開的 hello 所有資料表的都連結。</span><span class="sxs-lookup"><span data-stu-id="e999a-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="e999a-146">選取 hello 下一步 按鈕 toomove 向前復原。</span><span class="sxs-lookup"><span data-stu-id="e999a-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="e999a-147">步驟 5： 選擇儲存體帳戶 toostage hello 資料</span><span class="sxs-lookup"><span data-stu-id="e999a-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="e999a-148">DP 會提示您輸入位置 toostage hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e999a-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="e999a-149">從您的訂用帳戶選擇現有的儲存體帳戶，並選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="e999a-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="e999a-150">DP 會在 hello 選擇儲存體帳戶中建立新的 blob 容器，並使用每個匯入不同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e999a-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="e999a-151">步驟 6：建立資料倉儲</span><span class="sxs-lookup"><span data-stu-id="e999a-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="e999a-152">接下來，選取線上[Azure SQL 資料倉儲](http://aka.ms/sqldw)資料庫 tooimport hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e999a-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="e999a-153">一旦您已選取您的資料庫，您需要 tooenter hello 認證 tooconnect toohello 資料庫，並選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="e999a-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="e999a-154">DP 合併到 hello 資料倉儲的 hello 來源資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="e999a-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="e999a-155">DP 會警告您如果 hello 資料表名稱需要 toooverwrite hello 資料倉儲中現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="e999a-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="e999a-156">您可以選擇性地刪除 hello 資料倉儲中的任何現有物件的計時刪除之前匯入所有現有的物件。</span><span class="sxs-lookup"><span data-stu-id="e999a-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="e999a-157">步驟 7: Hello 資料匯入</span><span class="sxs-lookup"><span data-stu-id="e999a-157">Step 7: Import hello data</span></span>
<span data-ttu-id="e999a-158">DP 確認您想要 tooimport hello 資料。</span><span class="sxs-lookup"><span data-stu-id="e999a-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="e999a-159">只要按一下 hello 開始匯入 按鈕 toobegin hello 資料匯入。</span><span class="sxs-lookup"><span data-stu-id="e999a-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="e999a-160">DP 顯示視覺效果顯示 hello 進行擷取，並上傳 hello hello 在內部部署 SQL Server 和 hello 的進度 hello 匯入至 SQL 資料倉儲的資料。</span><span class="sxs-lookup"><span data-stu-id="e999a-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="e999a-161">Hello 匯入完成之後，DP 顯示 hello 資料匯入的摘要以及變更報表已執行之 hello 相容性修正程式。</span><span class="sxs-lookup"><span data-stu-id="e999a-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="e999a-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e999a-162">Next steps</span></span>
<span data-ttu-id="e999a-163">tooexplore 藉由檢視啟動 SQL 資料倉儲中的資料：</span><span class="sxs-lookup"><span data-stu-id="e999a-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="e999a-164">[查詢 Azure SQL 資料倉儲 (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="e999a-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="e999a-165">[使用 Power BI 視覺化資料][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="e999a-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="e999a-166">深入了解 Redgate 的資料平台 Studio toolearn:</span><span class="sxs-lookup"><span data-stu-id="e999a-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="e999a-167">請瀏覽 hello DP 首頁</span><span class="sxs-lookup"><span data-stu-id="e999a-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="e999a-168">在 Channel9 上觀看 DPS 的示範</span><span class="sxs-lookup"><span data-stu-id="e999a-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="e999a-169">如需的其他方式 toomigrate 和負載概觀請參閱 SQL 資料倉儲中的資料：</span><span class="sxs-lookup"><span data-stu-id="e999a-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="e999a-170">[移轉您的方案 tooSQL 資料倉儲][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="e999a-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="e999a-171">將資料載入 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="e999a-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="e999a-172">如需開發秘訣，請參閱 hello [SQL 資料倉儲開發概觀](sql-data-warehouse-overview-develop.md)。</span><span class="sxs-lookup"><span data-stu-id="e999a-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
