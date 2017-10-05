---
title: "連線到 Azure SQL 資料倉儲 - SSMS | Microsoft Docs"
description: "使用 SQL Server Management Studio (SSMS) 連接及查詢 Azure SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 207fb9fd861c66039fbde89681aed3df3a2f4021
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="f29f0-103">連接 SQL 資料倉儲與 SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="f29f0-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f29f0-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="f29f0-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="f29f0-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f29f0-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="f29f0-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f29f0-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="f29f0-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="f29f0-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="f29f0-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="f29f0-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="f29f0-109">使用 SQL Server Management Studio (SSMS) 連接及查詢 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="f29f0-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f29f0-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f29f0-110">Prerequisites</span></span>
<span data-ttu-id="f29f0-111">若要使用本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="f29f0-111">To use this tutorial, you need:</span></span>

* <span data-ttu-id="f29f0-112">現有的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="f29f0-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="f29f0-113">若要建立資料倉儲，請參閱 [建立 SQL 資料倉儲][Create a SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="f29f0-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="f29f0-114">SQL Server Management Studio (SSMS) 已安裝。</span><span class="sxs-lookup"><span data-stu-id="f29f0-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="f29f0-115">如果您尚未安裝，可以免費[安裝 SSMS][Install SSMS]。</span><span class="sxs-lookup"><span data-stu-id="f29f0-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="f29f0-116">完整的 SQL 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="f29f0-116">The fully qualified SQL server name.</span></span> <span data-ttu-id="f29f0-117">若要找到此名稱，請參閱 [連線至 SQL 資料倉儲][Connect to SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="f29f0-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="f29f0-118">1.連接到您的 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="f29f0-118">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="f29f0-119">開啟 SSMS。</span><span class="sxs-lookup"><span data-stu-id="f29f0-119">Open SSMS.</span></span>
2. <span data-ttu-id="f29f0-120">開啟物件總管。</span><span class="sxs-lookup"><span data-stu-id="f29f0-120">Open Object Explorer.</span></span> <span data-ttu-id="f29f0-121">若要這樣做，請選取 [檔案]  >  [連接物件總管]。</span><span class="sxs-lookup"><span data-stu-id="f29f0-121">To do this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![SQL Server 物件總管][1]
3. <span data-ttu-id="f29f0-123">填寫 [連線到伺服器] 視窗中的欄位。</span><span class="sxs-lookup"><span data-stu-id="f29f0-123">Fill in the fields in the Connect to Server window.</span></span>
   
    ![連線到伺服器][2]
   
   * <span data-ttu-id="f29f0-125">**伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="f29f0-125">**Server name**.</span></span> <span data-ttu-id="f29f0-126">輸入先前找到的 **伺服器名稱** 。</span><span class="sxs-lookup"><span data-stu-id="f29f0-126">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="f29f0-127">**驗證**。</span><span class="sxs-lookup"><span data-stu-id="f29f0-127">**Authentication**.</span></span> <span data-ttu-id="f29f0-128">選取 [SQL Server 驗證] 或 [Active Directory 整合式驗證]。</span><span class="sxs-lookup"><span data-stu-id="f29f0-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="f29f0-129">[使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="f29f0-129">**User Name** and **Password**.</span></span> <span data-ttu-id="f29f0-130">如果上面已選取 [SQL Server 驗證]，請輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="f29f0-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="f29f0-131">按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="f29f0-131">Click **Connect**.</span></span>
4. <span data-ttu-id="f29f0-132">若要瀏覽，請展開您的 Azure SQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f29f0-132">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="f29f0-133">您可以檢視與伺服器相關聯的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f29f0-133">You can view the databases associated with the server.</span></span> <span data-ttu-id="f29f0-134">展開 AdventureWorksDW 以查看範例資料庫中的資料表。</span><span class="sxs-lookup"><span data-stu-id="f29f0-134">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![探索 AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="f29f0-136">2.執行範例查詢</span><span class="sxs-lookup"><span data-stu-id="f29f0-136">2. Run a sample query</span></span>
<span data-ttu-id="f29f0-137">現已建立對您的資料庫的連線，接著繼續撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="f29f0-137">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="f29f0-138">在 [SQL Server 物件總管] 中您的資料庫上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="f29f0-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="f29f0-139">選取 [新增查詢] 。</span><span class="sxs-lookup"><span data-stu-id="f29f0-139">Select **New Query**.</span></span> <span data-ttu-id="f29f0-140">新的查詢視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f29f0-140">A new query window opens.</span></span>
   
    ![新增查詢][4]
3. <span data-ttu-id="f29f0-142">將此 TSQL 查詢複製到查詢視窗中：</span><span class="sxs-lookup"><span data-stu-id="f29f0-142">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="f29f0-143">執行查詢。</span><span class="sxs-lookup"><span data-stu-id="f29f0-143">Run the query.</span></span> <span data-ttu-id="f29f0-144">若要這麼做，請按一下 `Execute`，或使用下列快速鍵：`F5`。</span><span class="sxs-lookup"><span data-stu-id="f29f0-144">To do this, click `Execute` or use the following shortcut: `F5`.</span></span>
   
    ![執行查詢][5]
5. <span data-ttu-id="f29f0-146">查看查詢結果。</span><span class="sxs-lookup"><span data-stu-id="f29f0-146">Look at the query results.</span></span> <span data-ttu-id="f29f0-147">在此範例中，FactInternetSales 資料表有 60398 個資料列。</span><span class="sxs-lookup"><span data-stu-id="f29f0-147">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![查詢結果][6]

## <a name="next-steps"></a><span data-ttu-id="f29f0-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f29f0-149">Next steps</span></span>
<span data-ttu-id="f29f0-150">您現在可以連線並查詢，請嘗試[使用 PowerBI 將資料視覺化][visualizing the data with PowerBI]。</span><span class="sxs-lookup"><span data-stu-id="f29f0-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="f29f0-151">若要針對 Azure Active Directory 驗證設定您的環境，請參閱[驗證 SQL 資料倉儲][Authenticate to SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="f29f0-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
