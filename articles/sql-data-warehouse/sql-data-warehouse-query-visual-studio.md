---
title: "aaaConnect tooAzure SQL 資料倉儲-VSTS |Microsoft 文件"
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
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="4f883-103">與 Visual Studio 和 SSDT 連接 tooSQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="4f883-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f883-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="4f883-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="4f883-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4f883-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="4f883-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4f883-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="4f883-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="4f883-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="4f883-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="4f883-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="4f883-109">使用 Visual Studio tooquery Azure SQL 資料倉儲短短幾分鐘內。</span><span class="sxs-lookup"><span data-stu-id="4f883-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="4f883-110">這個方法會使用 Visual Studio 中的 hello SQL Server Data Tools (SSDT) 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="4f883-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4f883-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="4f883-111">Prerequisites</span></span>
<span data-ttu-id="4f883-112">toouse 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="4f883-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="4f883-113">現有的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="4f883-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="4f883-114">toocreate 其中一個，請參閱[建立 SQL 資料倉儲][Create a SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="4f883-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="4f883-115">適用於 Visual Studio 的 SSDT。</span><span class="sxs-lookup"><span data-stu-id="4f883-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="4f883-116">如果您有 Visual Studio，您可能已經有此 SSDT。</span><span class="sxs-lookup"><span data-stu-id="4f883-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="4f883-117">如需安裝指示和選項，請參閱 [安裝 Visual Studio 和 SSDT][Installing Visual Studio and SSDT]。</span><span class="sxs-lookup"><span data-stu-id="4f883-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="4f883-118">hello 完整 SQL server 名稱。</span><span class="sxs-lookup"><span data-stu-id="4f883-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="4f883-119">toofind，請參閱[連接 tooSQL 資料倉儲][Connect tooSQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="4f883-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="4f883-120">1.連接 tooyour SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="4f883-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="4f883-121">開啟 Visual Studio 2013 或 2015。</span><span class="sxs-lookup"><span data-stu-id="4f883-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="4f883-122">開啟 [SQL Server 物件總管]。</span><span class="sxs-lookup"><span data-stu-id="4f883-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="4f883-123">toodo 這個，請選取**檢視** > **SQL Server 物件總管**。</span><span class="sxs-lookup"><span data-stu-id="4f883-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server 物件總管][1]
3. <span data-ttu-id="4f883-125">按一下 hello**加入 SQL Server**圖示。</span><span class="sxs-lookup"><span data-stu-id="4f883-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![加入 SQL Server][2]
4. <span data-ttu-id="4f883-127">填寫 hello 連接 tooServer 視窗中的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="4f883-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![連接 tooServer][3]
   
   * <span data-ttu-id="4f883-129">**伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="4f883-129">**Server name**.</span></span> <span data-ttu-id="4f883-130">輸入 hello**伺服器名稱**先前所識別。</span><span class="sxs-lookup"><span data-stu-id="4f883-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="4f883-131">**驗證**。</span><span class="sxs-lookup"><span data-stu-id="4f883-131">**Authentication**.</span></span> <span data-ttu-id="4f883-132">選取 [SQL Server 驗證] 或 [Active Directory 整合式驗證]。</span><span class="sxs-lookup"><span data-stu-id="4f883-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="4f883-133">[使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="4f883-133">**User Name** and **Password**.</span></span> <span data-ttu-id="4f883-134">如果上面已選取 [SQL Server 驗證]，請輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="4f883-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="4f883-135">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="4f883-135">Click **Connect**.</span></span>
5. <span data-ttu-id="4f883-136">tooexplore，展開您的 Azure SQL server。</span><span class="sxs-lookup"><span data-stu-id="4f883-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="4f883-137">您可以檢視 hello hello 伺服器相關聯的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4f883-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="4f883-138">展開範例資料庫 AdventureWorksDW toosee hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="4f883-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![探索 AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="4f883-140">2.執行範例查詢</span><span class="sxs-lookup"><span data-stu-id="4f883-140">2. Run a sample query</span></span>
<span data-ttu-id="4f883-141">現在，連線已建立的 tooyour 資料庫，讓我們來撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="4f883-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="4f883-142">在 [SQL Server 物件總管] 中您的資料庫上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="4f883-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="4f883-143">選取 [新增查詢] 。</span><span class="sxs-lookup"><span data-stu-id="4f883-143">Select **New Query**.</span></span> <span data-ttu-id="4f883-144">新的查詢視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="4f883-144">A new query window opens.</span></span>
   
    ![新增查詢][5]
3. <span data-ttu-id="4f883-146">將這個 TSQL 查詢複製到查詢視窗中 hello:</span><span class="sxs-lookup"><span data-stu-id="4f883-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="4f883-147">執行 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="4f883-147">Run hello query.</span></span> <span data-ttu-id="4f883-148">toodo，按一下 hello 綠色箭號，或使用下列捷徑 hello: `CTRL` + `SHIFT` + `E`。</span><span class="sxs-lookup"><span data-stu-id="4f883-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![執行查詢][6]
5. <span data-ttu-id="4f883-150">查看 hello 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="4f883-150">Look at hello query results.</span></span> <span data-ttu-id="4f883-151">在此範例中，hello FactInternetSales 資料表會有 60398 資料列。</span><span class="sxs-lookup"><span data-stu-id="4f883-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![查詢結果][7]

## <a name="next-steps"></a><span data-ttu-id="4f883-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f883-153">Next steps</span></span>
<span data-ttu-id="4f883-154">現在，您可以連接並查詢，再試一次[視覺化 hello 資料與 PowerBI][visualizing hello data with PowerBI]。</span><span class="sxs-lookup"><span data-stu-id="4f883-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="4f883-155">tooconfigure 環境以使用 Azure Active Directory 驗證，請參閱[驗證資料倉儲 tooSQL][Authenticate tooSQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="4f883-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
