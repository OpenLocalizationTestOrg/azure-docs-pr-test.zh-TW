---
title: "連線到 Azure SQL 資料倉儲 - VSTS | Microsoft Docs"
description: "使用 Visual Studio 查詢 SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="aa255-103">使用 Visual Studio 和 SSDT 連接到 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="aa255-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa255-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="aa255-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="aa255-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aa255-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="aa255-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aa255-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="aa255-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="aa255-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="aa255-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="aa255-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="aa255-109">使用 Visual Studio 在短短幾分鐘內查詢 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="aa255-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="aa255-110">這個方法會在 Visual Studio 中使用 SQL Server Data Tools (SSDT) 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="aa255-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="aa255-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="aa255-111">Prerequisites</span></span>
<span data-ttu-id="aa255-112">若要使用本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="aa255-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="aa255-113">現有的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="aa255-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="aa255-114">若要建立資料倉儲，請參閱 [建立 SQL 資料倉儲][Create a SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="aa255-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="aa255-115">適用於 Visual Studio 的 SSDT。</span><span class="sxs-lookup"><span data-stu-id="aa255-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="aa255-116">如果您有 Visual Studio，您可能已經有此 SSDT。</span><span class="sxs-lookup"><span data-stu-id="aa255-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="aa255-117">如需安裝指示和選項，請參閱 [安裝 Visual Studio 和 SSDT][Installing Visual Studio and SSDT]。</span><span class="sxs-lookup"><span data-stu-id="aa255-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="aa255-118">完整的 SQL 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="aa255-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="aa255-119">若要找到此名稱，請參閱 [連線至 SQL 資料倉儲][Connect to SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="aa255-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="aa255-120">1.連接到您的 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="aa255-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="aa255-121">開啟 Visual Studio 2013 或 2015。</span><span class="sxs-lookup"><span data-stu-id="aa255-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="aa255-122">開啟 [SQL Server 物件總管]。</span><span class="sxs-lookup"><span data-stu-id="aa255-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="aa255-123">若要這麼做，請選取 [檢視] > [SQL Server 物件總管]。</span><span class="sxs-lookup"><span data-stu-id="aa255-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server 物件總管][1]
3. <span data-ttu-id="aa255-125">按一下 [加入 SQL Server]  圖示。</span><span class="sxs-lookup"><span data-stu-id="aa255-125">Click the **Add SQL Server** icon.</span></span>
   
    ![加入 SQL Server][2]
4. <span data-ttu-id="aa255-127">填寫 [連線到伺服器] 視窗中的欄位。</span><span class="sxs-lookup"><span data-stu-id="aa255-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![連線到伺服器][3]
   
   * <span data-ttu-id="aa255-129">**伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="aa255-129">**Server name**.</span></span> <span data-ttu-id="aa255-130">輸入先前找到的 **伺服器名稱** 。</span><span class="sxs-lookup"><span data-stu-id="aa255-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="aa255-131">**驗證**。</span><span class="sxs-lookup"><span data-stu-id="aa255-131">**Authentication**.</span></span> <span data-ttu-id="aa255-132">選取 [SQL Server 驗證] 或 [Active Directory 整合式驗證]。</span><span class="sxs-lookup"><span data-stu-id="aa255-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="aa255-133">[使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="aa255-133">**User Name** and **Password**.</span></span> <span data-ttu-id="aa255-134">如果上面已選取 [SQL Server 驗證]，請輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="aa255-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="aa255-135">按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="aa255-135">Click **Connect**.</span></span>
5. <span data-ttu-id="aa255-136">若要瀏覽，請展開您的 Azure SQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="aa255-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="aa255-137">您可以檢視與伺服器相關聯的資料庫。</span><span class="sxs-lookup"><span data-stu-id="aa255-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="aa255-138">展開 AdventureWorksDW 以查看範例資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="aa255-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![探索 AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="aa255-140">2.執行範例查詢</span><span class="sxs-lookup"><span data-stu-id="aa255-140">2. Run a sample query</span></span>
<span data-ttu-id="aa255-141">現已建立對您的資料庫的連線，接著繼續撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="aa255-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="aa255-142">在 [SQL Server 物件總管] 中您的資料庫上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="aa255-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="aa255-143">選取 [新增查詢] 。</span><span class="sxs-lookup"><span data-stu-id="aa255-143">Select **New Query**.</span></span> <span data-ttu-id="aa255-144">新的查詢視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="aa255-144">A new query window opens.</span></span>
   
    ![新增查詢][5]
3. <span data-ttu-id="aa255-146">將此 TSQL 查詢複製到查詢視窗中：</span><span class="sxs-lookup"><span data-stu-id="aa255-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="aa255-147">執行查詢。</span><span class="sxs-lookup"><span data-stu-id="aa255-147">Run the query.</span></span> <span data-ttu-id="aa255-148">若要這麼做，請按一下綠色箭頭，或使用下列快速鍵： `CTRL`+`SHIFT`+`E`。</span><span class="sxs-lookup"><span data-stu-id="aa255-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![執行查詢][6]
5. <span data-ttu-id="aa255-150">查看查詢結果。</span><span class="sxs-lookup"><span data-stu-id="aa255-150">Look at the query results.</span></span> <span data-ttu-id="aa255-151">在此範例中，FactInternetSales 資料表有 60398 個資料列。</span><span class="sxs-lookup"><span data-stu-id="aa255-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![查詢結果][7]

## <a name="next-steps"></a><span data-ttu-id="aa255-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa255-153">Next steps</span></span>
<span data-ttu-id="aa255-154">您現在可以連線並查詢，請嘗試[使用 PowerBI 將資料視覺化][visualizing the data with PowerBI]。</span><span class="sxs-lookup"><span data-stu-id="aa255-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="aa255-155">若要針對 Azure Active Directory 驗證設定您的環境，請參閱[驗證 SQL 資料倉儲][Authenticate to SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="aa255-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
