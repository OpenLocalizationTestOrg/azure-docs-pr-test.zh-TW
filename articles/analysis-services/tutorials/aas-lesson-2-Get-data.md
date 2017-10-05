---
title: "Azure Analysis Services 教學課程第 2 課：取得資料 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中取得和匯入資料。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: e77de4b9a74b528fa8a7ce86424fc14628b2cacc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-2-get-data"></a><span data-ttu-id="2b31c-103">第 2 課：取得資料</span><span class="sxs-lookup"><span data-stu-id="2b31c-103">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="2b31c-104">在這堂課中，您將使用 SSDT 中的「取得資料」來連線至 AdventureWorksDW2014 範例資料庫中、選取資料、預覽和篩選，然後匯入到您的模型工作區。</span><span class="sxs-lookup"><span data-stu-id="2b31c-104">In this lesson, you use Get Data in SSDT to connect to the AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="2b31c-105">「取得資料」可讓您從各種來源匯入資料︰Azure SQL Database、Oracle、Sybase、OData 摘要、Teradata、檔案等等。</span><span class="sxs-lookup"><span data-stu-id="2b31c-105">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="2b31c-106">您也可以使用 Power Query M 公式運算式來查詢資料。</span><span class="sxs-lookup"><span data-stu-id="2b31c-106">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="2b31c-107">這堂課的預估完成時間：**10 分鐘**</span><span class="sxs-lookup"><span data-stu-id="2b31c-107">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="2b31c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="2b31c-108">Prerequisites</span></span>  
<span data-ttu-id="2b31c-109">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="2b31c-109">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="2b31c-110">在這堂課中執行工作之前，您必須已完成上一堂課︰[第 1 課︰建立新的表格式模型專案](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)。</span><span class="sxs-lookup"><span data-stu-id="2b31c-110">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="2b31c-111">建立連線</span><span class="sxs-lookup"><span data-stu-id="2b31c-111">Create a connection</span></span>  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw2014-database"></a><span data-ttu-id="2b31c-112">建立 AdventureWorksDW2014 資料庫的連線</span><span class="sxs-lookup"><span data-stu-id="2b31c-112">To create a connection to the AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="2b31c-113">在 [表格式模型總管] 中，以滑鼠右鍵按一下 [資料來源] > [從資料來源匯入]。</span><span class="sxs-lookup"><span data-stu-id="2b31c-113">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="2b31c-114">這會啟動「取得資料」，引導您連線至資料來源。</span><span class="sxs-lookup"><span data-stu-id="2b31c-114">This launches Get Data, which guides you through connecting to a data source.</span></span> <span data-ttu-id="2b31c-115">如果您沒有看到 [表格式模型總管] 中，請在 [方案總管] 中按兩下 [Model.bim]，在設計工具中開啟模型。</span><span class="sxs-lookup"><span data-stu-id="2b31c-115">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** to open the model in the designer.</span></span> 
    
    ![aas 第 2 課取得資料](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="2b31c-117">在 [取得資料] 中，按一下 [資料庫] > [SQL Server 資料庫] > [連線]。</span><span class="sxs-lookup"><span data-stu-id="2b31c-117">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="2b31c-118">在 [SQL Server 資料庫] 對話方塊的 [伺服器] 中，輸入您安裝 AdventureWorksDW2014 資料庫的伺服器名稱，然後按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="2b31c-118">In the **SQL Server Database** dialog, in **Server**, type the name of the server where you installed the AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="2b31c-119">當系統提示您輸入認證時，您必須指定 Analysis Services 在匯入和處理資料時用來連線至資料來源的認證。</span><span class="sxs-lookup"><span data-stu-id="2b31c-119">When prompted to enter credentials, you need to specify the credentials Analysis Services uses to connect to the data source when importing and processing data.</span></span> <span data-ttu-id="2b31c-120">在 [模擬模式] 中，選取 [模擬帳戶]，輸入認證，然後按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="2b31c-120">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="2b31c-121">建議您使用密碼不會過期的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b31c-121">It's recommended you use an account where the password doesn't expire.</span></span>

    ![aas 第 2 課帳戶](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="2b31c-123">使用 Windows 使用者帳戶和密碼是連線至資料來源最安全的方法。</span><span class="sxs-lookup"><span data-stu-id="2b31c-123">Using a Windows user account and password provides the most secure method of connecting to a data source.</span></span>
  
5.  <span data-ttu-id="2b31c-124">在 [導覽器] 中，選取 [AdventureWorksDW2014] 資料庫，然後按一下 [確定]。這會建立資料庫的連線。</span><span class="sxs-lookup"><span data-stu-id="2b31c-124">In Navigator, select the **AdventureWorksDW2014** database, and then click **OK**.This creates the connection to the database.</span></span> 
  
6.  <span data-ttu-id="2b31c-125">在 [導覽器] 中，選取下列資料表的核取方塊︰**DimCustomer**、**DimDate**、**DimGeography**、**DimProduct**、**DimProductCategory**、**DimProductSubcategory** 和 **FactInternetSales**。</span><span class="sxs-lookup"><span data-stu-id="2b31c-125">In Navigator, select the check box for the following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="2b31c-127">按一下 [確定] 之後，[查詢編輯器] 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2b31c-127">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="2b31c-128">在下一個區段中，您只要選取想要匯入的資料。</span><span class="sxs-lookup"><span data-stu-id="2b31c-128">In the next section, you select only the data you want to import.</span></span>

  
## <a name="filter-the-table-data"></a><span data-ttu-id="2b31c-129">篩選資料表資料</span><span class="sxs-lookup"><span data-stu-id="2b31c-129">Filter the table data</span></span>  
<span data-ttu-id="2b31c-130">AdventureWorksDW2014 範例資料庫中的資料表有不需要加入模型中的資料。</span><span class="sxs-lookup"><span data-stu-id="2b31c-130">Tables in the AdventureWorksDW2014 sample database have data that isn't necessary to include in your model.</span></span> <span data-ttu-id="2b31c-131">可能的話，建議您篩選掉不必要的資料，以節省模型所使用的記憶體內部空間。</span><span class="sxs-lookup"><span data-stu-id="2b31c-131">When possible, you want to filter out unnecessary data to save in-memory space used by the model.</span></span> <span data-ttu-id="2b31c-132">您會從資料表中篩選掉某些資料行，這樣就不會匯入工作區資料庫中或模型資料庫中 (在部署之後)。</span><span class="sxs-lookup"><span data-stu-id="2b31c-132">You filter out some of the columns from tables so they're not imported into the workspace database, or the model database after it has been deployed.</span></span> 
  
#### <a name="to-filter-the-table-data-before-importing"></a><span data-ttu-id="2b31c-133">匯入之前篩選資料表資料</span><span class="sxs-lookup"><span data-stu-id="2b31c-133">To filter the table data before importing</span></span>  
  
1.  <span data-ttu-id="2b31c-134">在 [查詢編輯器] 中，選取 [DimCustomer] 資料表。</span><span class="sxs-lookup"><span data-stu-id="2b31c-134">In Query Editor, select the **DimCustomer** table.</span></span> <span data-ttu-id="2b31c-135">將會出現資料來源 (AdventureWorksDWQ2014 範例資料庫) 上的 DimCustomer 資料表檢視。</span><span class="sxs-lookup"><span data-stu-id="2b31c-135">A view of the DimCustomer table at the datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="2b31c-136">複選 (Ctrl + 按一下) **SpanishEducation**、**FrenchEducation**、**SpanishOccupation**、**FrenchOccupation**，按一下滑鼠右鍵，然後按一下 [移除資料行]。</span><span class="sxs-lookup"><span data-stu-id="2b31c-136">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas 第 2 課移除資料行](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="2b31c-138">因為這些資料行的值與網際網路銷售分析無關，不需要匯入這些資料行。</span><span class="sxs-lookup"><span data-stu-id="2b31c-138">Since the values for these columns are not relevant to Internet sales analysis, there is no need to import these columns.</span></span> <span data-ttu-id="2b31c-139">去除不必要的資料行可讓您的模型變得更小且更有效率。</span><span class="sxs-lookup"><span data-stu-id="2b31c-139">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="2b31c-140">在每個資料表中移除下列資料行，以篩選其餘資料表︰</span><span class="sxs-lookup"><span data-stu-id="2b31c-140">Filter the remaining tables by removing the following columns in each table:</span></span>  
    
    <span data-ttu-id="2b31c-141">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="2b31c-141">**DimDate**</span></span>
    
      |<span data-ttu-id="2b31c-142">資料欄</span><span class="sxs-lookup"><span data-stu-id="2b31c-142">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="2b31c-143">DateKey</span><span class="sxs-lookup"><span data-stu-id="2b31c-143">DateKey</span></span>|  
      |<span data-ttu-id="2b31c-144">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="2b31c-144">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="2b31c-145">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="2b31c-145">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="2b31c-146">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-146">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="2b31c-147">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-147">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="2b31c-148">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="2b31c-148">**DimGeography**</span></span>
  
      |<span data-ttu-id="2b31c-149">資料欄</span><span class="sxs-lookup"><span data-stu-id="2b31c-149">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="2b31c-150">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-150">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="2b31c-151">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-151">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="2b31c-152">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="2b31c-152">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="2b31c-153">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="2b31c-153">**DimProduct**</span></span>
  
      |<span data-ttu-id="2b31c-154">資料欄</span><span class="sxs-lookup"><span data-stu-id="2b31c-154">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="2b31c-155">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-155">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="2b31c-156">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-156">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="2b31c-157">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="2b31c-157">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="2b31c-158">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="2b31c-158">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="2b31c-159">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="2b31c-159">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="2b31c-160">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="2b31c-160">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="2b31c-161">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="2b31c-161">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="2b31c-162">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="2b31c-162">**GermanDescription**</span></span>|  
      |<span data-ttu-id="2b31c-163">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="2b31c-163">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="2b31c-164">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="2b31c-164">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="2b31c-165">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="2b31c-165">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="2b31c-166">資料欄</span><span class="sxs-lookup"><span data-stu-id="2b31c-166">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="2b31c-167">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-167">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="2b31c-168">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-168">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="2b31c-169">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="2b31c-169">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="2b31c-170">資料欄</span><span class="sxs-lookup"><span data-stu-id="2b31c-170">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="2b31c-171">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-171">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="2b31c-172">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="2b31c-172">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="2b31c-173">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="2b31c-173">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="2b31c-174">資料欄</span><span class="sxs-lookup"><span data-stu-id="2b31c-174">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="2b31c-175">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="2b31c-175">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="2b31c-176">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="2b31c-176">**DueDateKey**</span></span>|  
      |<span data-ttu-id="2b31c-177">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="2b31c-177">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="2b31c-178"><a name="Import"></a>匯入選取的資料表和資料表資料</span><span class="sxs-lookup"><span data-stu-id="2b31c-178"><a name="Import"></a>Import the selected tables and column data</span></span>  
<span data-ttu-id="2b31c-179">既然您已預覽並篩選掉不必要的資料，接下來可以匯入您真正想要的其餘資料。</span><span class="sxs-lookup"><span data-stu-id="2b31c-179">Now that you've previewed and filtered out unnecessary data, you can import the rest of the data you do want.</span></span> <span data-ttu-id="2b31c-180">精靈會匯入資料表資料，以及資料表之間的任何關聯性。</span><span class="sxs-lookup"><span data-stu-id="2b31c-180">The wizard imports the table data along with any relationships between tables.</span></span> <span data-ttu-id="2b31c-181">模型中會建立新的資料表和資料行，不會匯入您已篩選掉的資料。</span><span class="sxs-lookup"><span data-stu-id="2b31c-181">New tables and columns are created in the model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a><span data-ttu-id="2b31c-182">匯入選取的資料表和資料行資料</span><span class="sxs-lookup"><span data-stu-id="2b31c-182">To import the selected tables and column data</span></span>  
  
1.  <span data-ttu-id="2b31c-183">檢閱您的選擇。</span><span class="sxs-lookup"><span data-stu-id="2b31c-183">Review your selections.</span></span> <span data-ttu-id="2b31c-184">如果一切看起來沒問題，請按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="2b31c-184">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="2b31c-185">[資料處理] 對話方塊會顯示資料從資料來源匯入工作區資料庫的狀態。</span><span class="sxs-lookup"><span data-stu-id="2b31c-185">The Data Processing dialog shows the status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas 第 2 課成功](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="2b31c-187">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="2b31c-187">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="2b31c-188">儲存模型專案</span><span class="sxs-lookup"><span data-stu-id="2b31c-188">Save your model project</span></span>  
<span data-ttu-id="2b31c-189">請務必經常儲存模型專案。</span><span class="sxs-lookup"><span data-stu-id="2b31c-189">It's important to frequently save your model project.</span></span>  
  
#### <a name="to-save-the-model-project"></a><span data-ttu-id="2b31c-190">儲存模型專案</span><span class="sxs-lookup"><span data-stu-id="2b31c-190">To save the model project</span></span>  
  
-   <span data-ttu-id="2b31c-191">按一下 [檔案] > [全部儲存]。</span><span class="sxs-lookup"><span data-stu-id="2b31c-191">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="2b31c-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b31c-192">What's next?</span></span>
<span data-ttu-id="2b31c-193">[第 3 課：標記為日期資料表](../tutorials/aas-lesson-3-mark-as-date-table.md)。</span><span class="sxs-lookup"><span data-stu-id="2b31c-193">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
