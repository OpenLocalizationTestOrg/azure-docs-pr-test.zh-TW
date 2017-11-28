---
title: "aaaConnect tooAzure SQL 資料倉儲-SSMS |Microsoft 文件"
description: "使用 SQL Server Management Studio (SSMS) tooconnect tooand 查詢 Azure SQL 資料倉儲。"
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
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="6f0b4-103">使用 SQL Server Management Studio (SSMS) 連接 tooSQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="6f0b4-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f0b4-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="6f0b4-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="6f0b4-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="6f0b4-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="6f0b4-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f0b4-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="6f0b4-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="6f0b4-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="6f0b4-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="6f0b4-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="6f0b4-109">使用 SQL Server Management Studio (SSMS) tooconnect tooand 查詢 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6f0b4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6f0b4-110">Prerequisites</span></span>
<span data-ttu-id="6f0b4-111">toouse 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="6f0b4-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="6f0b4-112">現有的 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="6f0b4-113">toocreate 其中一個，請參閱[建立 SQL 資料倉儲][Create a SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="6f0b4-114">SQL Server Management Studio (SSMS) 已安裝。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="6f0b4-115">如果您尚未安裝，可以免費[安裝 SSMS][Install SSMS]。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="6f0b4-116">hello 完整 SQL server 名稱。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="6f0b4-117">toofind，請參閱[連接 tooSQL 資料倉儲][Connect tooSQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="6f0b4-118">1.連接 tooyour SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="6f0b4-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="6f0b4-119">開啟 SSMS。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-119">Open SSMS.</span></span>
2. <span data-ttu-id="6f0b4-120">開啟物件總管。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-120">Open Object Explorer.</span></span> <span data-ttu-id="6f0b4-121">toodo 這個，請選取**檔案** > **連接物件總管**。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![SQL Server 物件總管][1]
3. <span data-ttu-id="6f0b4-123">填寫 hello 連接 tooServer 視窗中的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![連接 tooServer][2]
   
   * <span data-ttu-id="6f0b4-125">**伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-125">**Server name**.</span></span> <span data-ttu-id="6f0b4-126">輸入 hello**伺服器名稱**先前所識別。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="6f0b4-127">**驗證**。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-127">**Authentication**.</span></span> <span data-ttu-id="6f0b4-128">選取 [SQL Server 驗證] 或 [Active Directory 整合式驗證]。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="6f0b4-129">[使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-129">**User Name** and **Password**.</span></span> <span data-ttu-id="6f0b4-130">如果上面已選取 [SQL Server 驗證]，請輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="6f0b4-131">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-131">Click **Connect**.</span></span>
4. <span data-ttu-id="6f0b4-132">tooexplore，展開您的 Azure SQL server。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="6f0b4-133">您可以檢視 hello hello 伺服器相關聯的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="6f0b4-134">展開範例資料庫 AdventureWorksDW toosee hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![探索 AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="6f0b4-136">2.執行範例查詢</span><span class="sxs-lookup"><span data-stu-id="6f0b4-136">2. Run a sample query</span></span>
<span data-ttu-id="6f0b4-137">現在，連線已建立的 tooyour 資料庫，讓我們來撰寫查詢。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="6f0b4-138">在 [SQL Server 物件總管] 中您的資料庫上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="6f0b4-139">選取 [新增查詢] 。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-139">Select **New Query**.</span></span> <span data-ttu-id="6f0b4-140">新的查詢視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-140">A new query window opens.</span></span>
   
    ![新增查詢][4]
3. <span data-ttu-id="6f0b4-142">將這個 TSQL 查詢複製到查詢視窗中 hello:</span><span class="sxs-lookup"><span data-stu-id="6f0b4-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="6f0b4-143">執行 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-143">Run hello query.</span></span> <span data-ttu-id="6f0b4-144">toodo 此，依序按一下`Execute`或使用 hello 下列快顯： `F5`。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![執行查詢][5]
5. <span data-ttu-id="6f0b4-146">查看 hello 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-146">Look at hello query results.</span></span> <span data-ttu-id="6f0b4-147">在此範例中，hello FactInternetSales 資料表會有 60398 資料列。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![查詢結果][6]

## <a name="next-steps"></a><span data-ttu-id="6f0b4-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f0b4-149">Next steps</span></span>
<span data-ttu-id="6f0b4-150">現在，您可以連接並查詢，再試一次[視覺化 hello 資料與 PowerBI][visualizing hello data with PowerBI]。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="6f0b4-151">tooconfigure 環境以使用 Azure Active Directory 驗證，請參閱[驗證資料倉儲 tooSQL][Authenticate tooSQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="6f0b4-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

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
