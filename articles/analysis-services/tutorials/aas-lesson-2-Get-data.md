---
<span data-ttu-id="da7e3-101">標題： aaa"Azure Analysis Services 教學課程第 2 課： 取得資料 |Microsoft 文件"描述： 描述 tooget 和匯入資料如何 hello Azure Analysis Services 教學課程專案。</span><span class="sxs-lookup"><span data-stu-id="da7e3-101">title: aaa"Azure Analysis Services tutorial lesson 2: Get data | Microsoft Docs" description: Describes how tooget and import data in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="da7e3-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="da7e3-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="da7e3-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="da7e3-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---

# <a name="lesson-2-get-data"></a><span data-ttu-id="da7e3-104">第 2 課：取得資料</span><span class="sxs-lookup"><span data-stu-id="da7e3-104">Lesson 2: Get data</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="da7e3-105">在這一課，您可以在 SSDT tooconnect toohello AdventureWorksDW2014 範例資料庫、 選取資料、 預覽和篩選器，使用 取得資料並再匯入您的模型工作空間。</span><span class="sxs-lookup"><span data-stu-id="da7e3-105">In this lesson, you use Get Data in SSDT tooconnect toohello AdventureWorksDW2014 sample database, select data, preview and filter, and then import into your model workspace.</span></span>  
  
<span data-ttu-id="da7e3-106">「取得資料」可讓您從各種來源匯入資料︰Azure SQL Database、Oracle、Sybase、OData 摘要、Teradata、檔案等等。</span><span class="sxs-lookup"><span data-stu-id="da7e3-106">By using Get Data, you can import data from a wide variety of sources: Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, files and more.</span></span> <span data-ttu-id="da7e3-107">您也可以使用 Power Query M 公式運算式來查詢資料。</span><span class="sxs-lookup"><span data-stu-id="da7e3-107">Data can also be queried using a Power Query M formula expression.</span></span>
  
<span data-ttu-id="da7e3-108">本課程的估計時間 toocomplete: **10 分鐘**</span><span class="sxs-lookup"><span data-stu-id="da7e3-108">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="da7e3-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="da7e3-109">Prerequisites</span></span>  
<span data-ttu-id="da7e3-110">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="da7e3-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="da7e3-111">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 1 課： 建立新的表格式模型專案](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)。</span><span class="sxs-lookup"><span data-stu-id="da7e3-111">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 1: Create a new tabular model project](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).</span></span>  
  
## <a name="create-a-connection"></a><span data-ttu-id="da7e3-112">建立連線</span><span class="sxs-lookup"><span data-stu-id="da7e3-112">Create a connection</span></span>  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a><span data-ttu-id="da7e3-113">toocreate 連線 toohello AdventureWorksDW2014 資料庫</span><span class="sxs-lookup"><span data-stu-id="da7e3-113">toocreate a connection toohello AdventureWorksDW2014 database</span></span>  
  
1.  <span data-ttu-id="da7e3-114">在 [表格式模型總管] 中，以滑鼠右鍵按一下 [資料來源] > [從資料來源匯入]。</span><span class="sxs-lookup"><span data-stu-id="da7e3-114">In Tabular Model Explorer, right-click **Data Sources** > **Import from Data Source**.</span></span>  
  
    <span data-ttu-id="da7e3-115">這會啟動 取得資料，將引導您完成連接 tooa 資料來源。</span><span class="sxs-lookup"><span data-stu-id="da7e3-115">This launches Get Data, which guides you through connecting tooa data source.</span></span> <span data-ttu-id="da7e3-116">如果您沒有看到表格式模型總管 中，在**方案總管 中**，連按兩下**Model.bim** tooopen hello 設計工具中的 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="da7e3-116">If you don't see Tabular Model Explorer, in **Solution Explorer**, double-click **Model.bim** tooopen hello model in hello designer.</span></span> 
    
    ![aas 第 2 課取得資料](../tutorials/media/aas-lesson2-getdata.png)
  
2.  <span data-ttu-id="da7e3-118">在 [取得資料] 中，按一下 [資料庫] > [SQL Server 資料庫] > [連線]。</span><span class="sxs-lookup"><span data-stu-id="da7e3-118">In Get Data, click **Database** > **SQL Server Database** > **Connect**.</span></span>  
  
3.  <span data-ttu-id="da7e3-119">在 hello **SQL Server 資料庫**對話方塊，請在**伺服器**，輸入 hello hello hello AdventureWorksDW2014 資料庫的安裝所在的伺服器名稱，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="da7e3-119">In hello **SQL Server Database** dialog, in **Server**, type hello name of hello server where you installed hello AdventureWorksDW2014 database, and then click **Connect**.</span></span>  

4.  <span data-ttu-id="da7e3-120">出現提示時 tooenter 認證，需要 Analysis Services 會使用 tooconnect toohello 資料來源匯入和處理資料時的 toospecify hello 認證。</span><span class="sxs-lookup"><span data-stu-id="da7e3-120">When prompted tooenter credentials, you need toospecify hello credentials Analysis Services uses tooconnect toohello data source when importing and processing data.</span></span> <span data-ttu-id="da7e3-121">在 模擬模式 中，選取 模擬帳戶，輸入認證，然後按一下連線。</span><span class="sxs-lookup"><span data-stu-id="da7e3-121">In **Impersonation Mode**, select **Impersonate Account**, then enter credentials, and then click **Connect**.</span></span> <span data-ttu-id="da7e3-122">建議您使用的帳戶其中 hello 密碼尚未過期。</span><span class="sxs-lookup"><span data-stu-id="da7e3-122">It's recommended you use an account where hello password doesn't expire.</span></span>

    ![aas 第 2 課帳戶](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > <span data-ttu-id="da7e3-124">使用 Windows 使用者帳戶和密碼提供 hello 連接 tooa 資料來源的最安全的方法。</span><span class="sxs-lookup"><span data-stu-id="da7e3-124">Using a Windows user account and password provides hello most secure method of connecting tooa data source.</span></span>
  
5.  <span data-ttu-id="da7e3-125">在導覽中，選取 hello **AdventureWorksDW2014**資料庫，然後再按一下**確定**。這會建立 hello 連線 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="da7e3-125">In Navigator, select hello **AdventureWorksDW2014** database, and then click **OK**.This creates hello connection toohello database.</span></span> 
  
6.  <span data-ttu-id="da7e3-126">在導覽中，選取 hello hello 下列資料表的核取方塊： **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，和**FactInternetSales**。</span><span class="sxs-lookup"><span data-stu-id="da7e3-126">In Navigator, select hello check box for hello following tables: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales**.</span></span>  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
<span data-ttu-id="da7e3-128">按一下 [確定] 之後，[查詢編輯器] 隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="da7e3-128">After you click OK, Query Editor opens.</span></span> <span data-ttu-id="da7e3-129">Hello 下一節，您可以選取只想 tooimport hello 資料。</span><span class="sxs-lookup"><span data-stu-id="da7e3-129">In hello next section, you select only hello data you want tooimport.</span></span>

  
## <a name="filter-hello-table-data"></a><span data-ttu-id="da7e3-130">篩選 hello 資料表的資料</span><span class="sxs-lookup"><span data-stu-id="da7e3-130">Filter hello table data</span></span>  
<span data-ttu-id="da7e3-131">Hello AdventureWorksDW2014 範例資料庫中的資料表具有不必要 tooinclude 模型中的資料。</span><span class="sxs-lookup"><span data-stu-id="da7e3-131">Tables in hello AdventureWorksDW2014 sample database have data that isn't necessary tooinclude in your model.</span></span> <span data-ttu-id="da7e3-132">如果可能的話，您會想 toofilter 出 hello 模型所使用的不必要的資料 toosave 記憶體空間。</span><span class="sxs-lookup"><span data-stu-id="da7e3-132">When possible, you want toofilter out unnecessary data toosave in-memory space used by hello model.</span></span> <span data-ttu-id="da7e3-133">您篩選出部分 hello 資料表之資料行，所以未匯入至 hello 工作空間資料庫或 hello 模型資料庫之後已部署。</span><span class="sxs-lookup"><span data-stu-id="da7e3-133">You filter out some of hello columns from tables so they're not imported into hello workspace database, or hello model database after it has been deployed.</span></span> 
  
#### <a name="toofilter-hello-table-data-before-importing"></a><span data-ttu-id="da7e3-134">匯入之前 toofilter hello 資料表資料</span><span class="sxs-lookup"><span data-stu-id="da7e3-134">toofilter hello table data before importing</span></span>  
  
1.  <span data-ttu-id="da7e3-135">在 [查詢編輯器] 中，選取 hello **DimCustomer**資料表。</span><span class="sxs-lookup"><span data-stu-id="da7e3-135">In Query Editor, select hello **DimCustomer** table.</span></span> <span data-ttu-id="da7e3-136">在 hello 資料來源 （AdventureWorksDWQ2014 範例資料庫） 的 hello DimCustomer 資料表的檢視會顯示。</span><span class="sxs-lookup"><span data-stu-id="da7e3-136">A view of hello DimCustomer table at hello datasource (your AdventureWorksDWQ2014 sample database) appears.</span></span> 
  
2.  <span data-ttu-id="da7e3-137">複選 (Ctrl + 按一下) **SpanishEducation**、**FrenchEducation**、**SpanishOccupation**、**FrenchOccupation**，按一下滑鼠右鍵，然後按一下移除資料行。</span><span class="sxs-lookup"><span data-stu-id="da7e3-137">Multi-select (Ctrl + click) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, then right-click, and then click **Remove Columns**.</span></span> 

    ![aas 第 2 課移除資料行](../tutorials/media/aas-lesson2-remove-columns.png)
  
    <span data-ttu-id="da7e3-139">由於這些資料行的 hello 值相關的 tooInternet 銷售分析，沒有任何需要 tooimport 這些資料行。</span><span class="sxs-lookup"><span data-stu-id="da7e3-139">Since hello values for these columns are not relevant tooInternet sales analysis, there is no need tooimport these columns.</span></span> <span data-ttu-id="da7e3-140">去除不必要的資料行可讓您的模型變得更小且更有效率。</span><span class="sxs-lookup"><span data-stu-id="da7e3-140">Eliminating unnecessary columns makes your model smaller and more efficient.</span></span>  
  
4.  <span data-ttu-id="da7e3-141">篩選其餘資料表移除下列資料行，每個資料表中的 hello hello:</span><span class="sxs-lookup"><span data-stu-id="da7e3-141">Filter hello remaining tables by removing hello following columns in each table:</span></span>  
    
    <span data-ttu-id="da7e3-142">**DimDate**</span><span class="sxs-lookup"><span data-stu-id="da7e3-142">**DimDate**</span></span>
    
      |<span data-ttu-id="da7e3-143">資料欄</span><span class="sxs-lookup"><span data-stu-id="da7e3-143">Column</span></span>|  
      |--------|  
      |<span data-ttu-id="da7e3-144">DateKey</span><span class="sxs-lookup"><span data-stu-id="da7e3-144">DateKey</span></span>|  
      |<span data-ttu-id="da7e3-145">**SpanishDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="da7e3-145">**SpanishDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="da7e3-146">**FrenchDayNameOfWeek**</span><span class="sxs-lookup"><span data-stu-id="da7e3-146">**FrenchDayNameOfWeek**</span></span>|  
      |<span data-ttu-id="da7e3-147">**SpanishMonthName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-147">**SpanishMonthName**</span></span>|  
      |<span data-ttu-id="da7e3-148">**FrenchMonthName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-148">**FrenchMonthName**</span></span>|  
  
    <span data-ttu-id="da7e3-149">**DimGeography**</span><span class="sxs-lookup"><span data-stu-id="da7e3-149">**DimGeography**</span></span>
  
      |<span data-ttu-id="da7e3-150">資料欄</span><span class="sxs-lookup"><span data-stu-id="da7e3-150">Column</span></span>|  
      |-------------|  
      |<span data-ttu-id="da7e3-151">**SpanishCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-151">**SpanishCountryRegionName**</span></span>|  
      |<span data-ttu-id="da7e3-152">**FrenchCountryRegionName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-152">**FrenchCountryRegionName**</span></span>|  
      |<span data-ttu-id="da7e3-153">**IpAddressLocator**</span><span class="sxs-lookup"><span data-stu-id="da7e3-153">**IpAddressLocator**</span></span>|  
  
    <span data-ttu-id="da7e3-154">**DimProduct**</span><span class="sxs-lookup"><span data-stu-id="da7e3-154">**DimProduct**</span></span>
  
      |<span data-ttu-id="da7e3-155">資料欄</span><span class="sxs-lookup"><span data-stu-id="da7e3-155">Column</span></span>|  
      |-----------|  
      |<span data-ttu-id="da7e3-156">**SpanishProductName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-156">**SpanishProductName**</span></span>|  
      |<span data-ttu-id="da7e3-157">**FrenchProductName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-157">**FrenchProductName**</span></span>|  
      |<span data-ttu-id="da7e3-158">**FrenchDescription**</span><span class="sxs-lookup"><span data-stu-id="da7e3-158">**FrenchDescription**</span></span>|  
      |<span data-ttu-id="da7e3-159">**ChineseDescription**</span><span class="sxs-lookup"><span data-stu-id="da7e3-159">**ChineseDescription**</span></span>|  
      |<span data-ttu-id="da7e3-160">**ArabicDescription**</span><span class="sxs-lookup"><span data-stu-id="da7e3-160">**ArabicDescription**</span></span>|  
      |<span data-ttu-id="da7e3-161">**HebrewDescription**</span><span class="sxs-lookup"><span data-stu-id="da7e3-161">**HebrewDescription**</span></span>|  
      |<span data-ttu-id="da7e3-162">**ThaiDescription**</span><span class="sxs-lookup"><span data-stu-id="da7e3-162">**ThaiDescription**</span></span>|  
      |<span data-ttu-id="da7e3-163">**GermanDescription**</span><span class="sxs-lookup"><span data-stu-id="da7e3-163">**GermanDescription**</span></span>|  
      |<span data-ttu-id="da7e3-164">**JapaneseDescription**</span><span class="sxs-lookup"><span data-stu-id="da7e3-164">**JapaneseDescription**</span></span>|  
      |<span data-ttu-id="da7e3-165">**TurkishDescription**</span><span class="sxs-lookup"><span data-stu-id="da7e3-165">**TurkishDescription**</span></span>|  
  
    <span data-ttu-id="da7e3-166">**DimProductCategory**</span><span class="sxs-lookup"><span data-stu-id="da7e3-166">**DimProductCategory**</span></span>
  
      |<span data-ttu-id="da7e3-167">資料欄</span><span class="sxs-lookup"><span data-stu-id="da7e3-167">Column</span></span>|  
      |--------------------|  
      |<span data-ttu-id="da7e3-168">**SpanishProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-168">**SpanishProductCategoryName**</span></span>|  
      |<span data-ttu-id="da7e3-169">**FrenchProductCategoryName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-169">**FrenchProductCategoryName**</span></span>|  
  
    <span data-ttu-id="da7e3-170">**DimProductSubcategory**</span><span class="sxs-lookup"><span data-stu-id="da7e3-170">**DimProductSubcategory**</span></span>
  
      |<span data-ttu-id="da7e3-171">資料欄</span><span class="sxs-lookup"><span data-stu-id="da7e3-171">Column</span></span>|  
      |-----------------------|  
      |<span data-ttu-id="da7e3-172">**SpanishProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-172">**SpanishProductSubcategoryName**</span></span>|  
      |<span data-ttu-id="da7e3-173">**FrenchProductSubcategoryName**</span><span class="sxs-lookup"><span data-stu-id="da7e3-173">**FrenchProductSubcategoryName**</span></span>|  
  
    <span data-ttu-id="da7e3-174">**FactInternetSales**</span><span class="sxs-lookup"><span data-stu-id="da7e3-174">**FactInternetSales**</span></span>
  
      |<span data-ttu-id="da7e3-175">資料欄</span><span class="sxs-lookup"><span data-stu-id="da7e3-175">Column</span></span>|  
      |------------------|  
      |<span data-ttu-id="da7e3-176">**OrderDateKey**</span><span class="sxs-lookup"><span data-stu-id="da7e3-176">**OrderDateKey**</span></span>|  
      |<span data-ttu-id="da7e3-177">**DueDateKey**</span><span class="sxs-lookup"><span data-stu-id="da7e3-177">**DueDateKey**</span></span>|  
      |<span data-ttu-id="da7e3-178">**ShipDateKey**</span><span class="sxs-lookup"><span data-stu-id="da7e3-178">**ShipDateKey**</span></span>|   
  
## <span data-ttu-id="da7e3-179"><a name="Import"></a>匯入 hello 選取資料表和資料行的資料</span><span class="sxs-lookup"><span data-stu-id="da7e3-179"><a name="Import"></a>Import hello selected tables and column data</span></span>  
<span data-ttu-id="da7e3-180">現在，您已預覽並篩選掉不必要的資料，您可以匯入 hello 其他您想 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="da7e3-180">Now that you've previewed and filtered out unnecessary data, you can import hello rest of hello data you do want.</span></span> <span data-ttu-id="da7e3-181">hello 精靈匯入 hello 資料表資料，以及資料表之間的任何關聯性。</span><span class="sxs-lookup"><span data-stu-id="da7e3-181">hello wizard imports hello table data along with any relationships between tables.</span></span> <span data-ttu-id="da7e3-182">Hello 模型中建立新的資料表和資料行並不會匯入您篩選掉的資料。</span><span class="sxs-lookup"><span data-stu-id="da7e3-182">New tables and columns are created in hello model and data that you filtered out is not be imported.</span></span>  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a><span data-ttu-id="da7e3-183">tooimport hello 選取資料表和資料行的資料</span><span class="sxs-lookup"><span data-stu-id="da7e3-183">tooimport hello selected tables and column data</span></span>  
  
1.  <span data-ttu-id="da7e3-184">檢閱您的選擇。</span><span class="sxs-lookup"><span data-stu-id="da7e3-184">Review your selections.</span></span> <span data-ttu-id="da7e3-185">如果一切看起來沒問題，請按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="da7e3-185">If everything looks okay, click **Import**.</span></span> <span data-ttu-id="da7e3-186">hello 資料處理 對話方塊會顯示 hello 狀態正在從您的資料來源匯入至工作空間資料庫的資料。</span><span class="sxs-lookup"><span data-stu-id="da7e3-186">hello Data Processing dialog shows hello status of data being imported from your datasource into your workspace database.</span></span>
  
    ![aas 第 2 課成功](../tutorials/media/aas-lesson2-success.png) 
  
2.  <span data-ttu-id="da7e3-188">按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="da7e3-188">Click **Close**.</span></span>  

  
## <a name="save-your-model-project"></a><span data-ttu-id="da7e3-189">儲存模型專案</span><span class="sxs-lookup"><span data-stu-id="da7e3-189">Save your model project</span></span>  
<span data-ttu-id="da7e3-190">請務必 toofrequently 儲存模型專案。</span><span class="sxs-lookup"><span data-stu-id="da7e3-190">It's important toofrequently save your model project.</span></span>  
  
#### <a name="toosave-hello-model-project"></a><span data-ttu-id="da7e3-191">toosave hello 模型專案</span><span class="sxs-lookup"><span data-stu-id="da7e3-191">toosave hello model project</span></span>  
  
-   <span data-ttu-id="da7e3-192">按一下 [檔案] > [全部儲存]。</span><span class="sxs-lookup"><span data-stu-id="da7e3-192">Click **File** > **Save All**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="da7e3-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da7e3-193">What's next?</span></span>
<span data-ttu-id="da7e3-194">[第 3 課：標記為日期資料表](../tutorials/aas-lesson-3-mark-as-date-table.md)。</span><span class="sxs-lookup"><span data-stu-id="da7e3-194">[Lesson 3: Mark as Date Table](../tutorials/aas-lesson-3-mark-as-date-table.md).</span></span>

  
  
