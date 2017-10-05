---
title: "使用 Redgate 將資料載入至 Azure 資料倉儲 | Microsoft Docs"
description: "了解如何針對資料倉儲案例使用 Redgate 的資料平台 Studio。"
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
ms.openlocfilehash: a38b237d5bfc0450c1ca79b53a5784dbb9bf8602
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="75a83-103">使用 Redgate 資料平台 Studio 載入資料</span><span class="sxs-lookup"><span data-stu-id="75a83-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75a83-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="75a83-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="75a83-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="75a83-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="75a83-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="75a83-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="75a83-107">BCP</span><span class="sxs-lookup"><span data-stu-id="75a83-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="75a83-108">本教學課程會示範如何使用 [Redgate 的資料平台 Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) 將資料從內部部署 SQL Server 移至 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="75a83-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premises SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="75a83-109">資料平台 Studio 會套用最適當的相容性修正檔與最佳化，因此它是開始使用 SQL 資料倉儲最快的方式。</span><span class="sxs-lookup"><span data-stu-id="75a83-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="75a83-110">[Redgate](http://www.red-gate.com) 是長期的 Microsoft 合作夥伴，提供各種 SQL Server 工具。</span><span class="sxs-lookup"><span data-stu-id="75a83-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="75a83-111">在資料平台 Studio 中的這項功能已免費提供商業和非商業使用。</span><span class="sxs-lookup"><span data-stu-id="75a83-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="75a83-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="75a83-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="75a83-113">建立或識別資源</span><span class="sxs-lookup"><span data-stu-id="75a83-113">Create or identify resources</span></span>
<span data-ttu-id="75a83-114">開始進行本教學課程之前，您需要有：</span><span class="sxs-lookup"><span data-stu-id="75a83-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="75a83-115">**內部部署 SQL Server 資料庫**︰您要匯入至 SQL 資料倉儲的資料必須來自內部部署 SQL Server (2008R2 版或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="75a83-115">**on-premises SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="75a83-116">資料平台 Studio 無法直接從 Azure SQL Database 或文字檔匯入資料。</span><span class="sxs-lookup"><span data-stu-id="75a83-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="75a83-117">**Azure 儲存體帳戶**︰資料平台 Studio 在將資料載入 SQL 資料倉儲之前會設置 Azure Blob 儲存體中的資料。</span><span class="sxs-lookup"><span data-stu-id="75a83-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="75a83-118">儲存體帳戶必須使用「Resource Manager」部署模型 (預設值) 而非「傳統」部署模型。</span><span class="sxs-lookup"><span data-stu-id="75a83-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="75a83-119">如果您沒有儲存體帳戶，請參閱如何建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="75a83-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="75a83-120">**SQL 資料倉儲**︰本教學課程中會將資料從內部部署 SQL Server 移動到 SQL 資料倉儲，因此您在線上需要有資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="75a83-120">**SQL Data Warehouse**: This tutorial moves the data from on-premises SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="75a83-121">如果您還沒有資料倉儲，請了解如何建立 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="75a83-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="75a83-122">如果在相同區域中建立儲存體帳戶和資料倉儲，則會改進效能。</span><span class="sxs-lookup"><span data-stu-id="75a83-122">Performance is improved if the storage account and the data warehouse are created in the same region.</span></span>
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="75a83-123">步驟 1︰使用您的 Azure 帳戶登入資料平台 Studio</span><span class="sxs-lookup"><span data-stu-id="75a83-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="75a83-124">開啟網頁瀏覽器並瀏覽至[資料平台 Studio](https://www.dataplatformstudio.com/) 網站。</span><span class="sxs-lookup"><span data-stu-id="75a83-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="75a83-125">使用您用來建立儲存體帳戶和資料倉儲的相同 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="75a83-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="75a83-126">如果您的電子郵件地址與工作或學校帳戶和 Microsoft 帳戶相關聯，請務必選擇擁有資源存取權的帳戶。</span><span class="sxs-lookup"><span data-stu-id="75a83-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> <span data-ttu-id="75a83-127">如果這是您第一次使用資料平台 Studio，系統會要求您授與應用程式權限以管理您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="75a83-127">If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="75a83-128">步驟 2︰開始匯入精靈</span><span class="sxs-lookup"><span data-stu-id="75a83-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="75a83-129">從 DPS 主畫面中，選取 [匯入至 Azure SQL 資料倉儲連結] 以啟動匯入精靈。</span><span class="sxs-lookup"><span data-stu-id="75a83-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="75a83-130">步驟 3︰安裝資料平台 Studio 閘道器</span><span class="sxs-lookup"><span data-stu-id="75a83-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="75a83-131">若要連線到您的內部部署 SQL Server 資料庫，您需要安裝 DPS 閘道器。</span><span class="sxs-lookup"><span data-stu-id="75a83-131">To connect to your on-premises SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="75a83-132">閘道器是用戶端代理程式，可提供您內部部署環境的存取權、擷取資料，並將它上傳至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="75a83-132">The gateway is a client agent that provides access to your on-premises environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="75a83-133">您的資料永遠不會通過 Redgate 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="75a83-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="75a83-134">若要安裝閘道器：</span><span class="sxs-lookup"><span data-stu-id="75a83-134">To install the Gateway:</span></span>

1. <span data-ttu-id="75a83-135">按一下 [建立閘道器] 連結</span><span class="sxs-lookup"><span data-stu-id="75a83-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="75a83-136">使用所提供的安裝程式下載並安裝閘道器</span><span class="sxs-lookup"><span data-stu-id="75a83-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="75a83-137">可以在具有來源 SQL Server 資料庫網路存取的任何電腦上安裝閘道。</span><span class="sxs-lookup"><span data-stu-id="75a83-137">The Gateway can be installed on any machine with network access to the source SQL Server database.</span></span> <span data-ttu-id="75a83-138">它會使用 Windows 驗證與目前使用者的認證存取 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a83-138">It accesses the SQL Server database using Windows authentication with the credentials of the current user.</span></span>
> 
> 

<span data-ttu-id="75a83-139">安裝之後，閘道器狀態會變更為 [已連接]，而您可以選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="75a83-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="75a83-140">步驟 4︰識別來源資料庫</span><span class="sxs-lookup"><span data-stu-id="75a83-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="75a83-141">在 [輸入伺服器名稱]文字方塊中，輸入裝載資料庫的伺服器名稱，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="75a83-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="75a83-142">然後，從下拉式功能表中，選取您想要匯入資料的來源資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a83-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="75a83-143">DPS 會檢查選取的資料庫以找到要匯入的資料表。</span><span class="sxs-lookup"><span data-stu-id="75a83-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="75a83-144">依預設，DPS 會匯入資料庫中的所有資料表。</span><span class="sxs-lookup"><span data-stu-id="75a83-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="75a83-145">您可以展開 [所有資料表] 連結來選取或取消選取資料表。</span><span class="sxs-lookup"><span data-stu-id="75a83-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="75a83-146">選取 [下一步] 按鈕以向前移動。</span><span class="sxs-lookup"><span data-stu-id="75a83-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="75a83-147">步驟 5︰選擇要將資料暫存的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="75a83-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="75a83-148">DPS 會提示您要將資料暫存的位置。</span><span class="sxs-lookup"><span data-stu-id="75a83-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="75a83-149">從您的訂用帳戶選擇現有的儲存體帳戶，並選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="75a83-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="75a83-150">DPS 會在選擇的儲存體帳戶中建立新的 blob 容器，並針對每個匯入使用不同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="75a83-150">DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="75a83-151">步驟 6：建立資料倉儲</span><span class="sxs-lookup"><span data-stu-id="75a83-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="75a83-152">接下來，選取要匯入資料的線上 [Azure SQL 資料倉儲](http://aka.ms/sqldw)資料庫。</span><span class="sxs-lookup"><span data-stu-id="75a83-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="75a83-153">一旦您已選取您的資料庫後，需要輸入認證以連接到資料庫，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="75a83-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="75a83-154">DPS 會將來源資料的資料表合併到資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="75a83-154">DPS merges the source data tables into the data warehouse.</span></span> <span data-ttu-id="75a83-155">如果資料表名稱需要 DPS 以在資料倉儲中覆寫現有的資料表，則 DPS 會警告您。</span><span class="sxs-lookup"><span data-stu-id="75a83-155">DPS warns you if the table name requires it to overwrite existing tables in the data warehouse.</span></span> <span data-ttu-id="75a83-156">您可以點選 [在匯入之前刪除所有現有的物件]，選擇性地在資料倉儲中刪除任何現有的物件。</span><span class="sxs-lookup"><span data-stu-id="75a83-156">You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="75a83-157">步驟 7︰將資料匯入</span><span class="sxs-lookup"><span data-stu-id="75a83-157">Step 7: Import the data</span></span>
<span data-ttu-id="75a83-158">DPS 會確認您想要匯入資料。</span><span class="sxs-lookup"><span data-stu-id="75a83-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="75a83-159">只要按一下 [開始匯入] 按鈕即可開始匯入資料。</span><span class="sxs-lookup"><span data-stu-id="75a83-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="75a83-160">DPS 會顯示視覺效果，顯示從內部部署 SQL Server 擷取和上傳資料的進度，以及匯入 SQL 資料倉儲的進度。</span><span class="sxs-lookup"><span data-stu-id="75a83-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premises SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="75a83-161">一旦匯入完成後，DPS 會顯示資料匯入的摘要，以及已執行之相容性修正的變更報告。</span><span class="sxs-lookup"><span data-stu-id="75a83-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="75a83-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75a83-162">Next steps</span></span>
<span data-ttu-id="75a83-163">若要瀏覽您在 SQL 資料倉儲內的資料，請先檢視︰</span><span class="sxs-lookup"><span data-stu-id="75a83-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="75a83-164">[查詢 Azure SQL 資料倉儲 (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="75a83-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="75a83-165">[使用 Power BI 視覺化資料][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="75a83-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="75a83-166">若要深入了解 Redgate 的資料平台 Studio：</span><span class="sxs-lookup"><span data-stu-id="75a83-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="75a83-167">瀏覽 DPS 首頁</span><span class="sxs-lookup"><span data-stu-id="75a83-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="75a83-168">在 Channel9 上觀看 DPS 的示範</span><span class="sxs-lookup"><span data-stu-id="75a83-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="75a83-169">如需在 SQL 資料倉儲中移轉及載入資料之其他方式的概觀，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="75a83-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="75a83-170">[將您的解決方案移轉至 SQL 資料倉儲][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="75a83-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* [<span data-ttu-id="75a83-171">將資料載入 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="75a83-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="75a83-172">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀](sql-data-warehouse-overview-develop.md)。</span><span class="sxs-lookup"><span data-stu-id="75a83-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

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
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
