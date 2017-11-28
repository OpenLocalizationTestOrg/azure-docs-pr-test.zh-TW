---
<span data-ttu-id="85443-101">標題： aaa"Azure Analysis Services 教學課程第 10 課： 建立資料分割 |Microsoft 文件"描述： 描述 toocreate hello Azure Analysis Services 教學課程專案中的資料分割。</span><span class="sxs-lookup"><span data-stu-id="85443-101">title: aaa"Azure Analysis Services tutorial lesson 10: Create partitions | Microsoft Docs" description: Describes how toocreate partitions in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="85443-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="85443-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="85443-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="85443-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="85443-104">第 10 課：建立分割區</span><span class="sxs-lookup"><span data-stu-id="85443-104">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="85443-105">在這一課，您可以建立資料分割 toodivide hello FactInternetSales 資料表分成較小的邏輯部分可以是其他資料分割的處理 （重新整理） 獨立的。</span><span class="sxs-lookup"><span data-stu-id="85443-105">In this lesson, you create partitions toodivide hello FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="85443-106">根據預設，您在模型中包含每個資料表會有一個資料分割，其中包含所有 hello 資料表的資料行和資料列。</span><span class="sxs-lookup"><span data-stu-id="85443-106">By default, every table you include in your model has one partition, which includes all hello table’s columns and rows.</span></span> <span data-ttu-id="85443-107">Hello FactInternetSales 資料表中，我們想 toodivide hello 資料依年份。hello 資料表的五年的每一個資料分割。</span><span class="sxs-lookup"><span data-stu-id="85443-107">For hello FactInternetSales table, we want toodivide hello data by year; one partition for each of hello table’s five years.</span></span> <span data-ttu-id="85443-108">然後就可以獨立處理每個分割區。</span><span class="sxs-lookup"><span data-stu-id="85443-108">Each partition can then be processed independently.</span></span> <span data-ttu-id="85443-109">詳細資訊，請參閱 toolearn[分割](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="85443-109">toolearn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="85443-110">本課程的估計時間 toocomplete: **15 分鐘**</span><span class="sxs-lookup"><span data-stu-id="85443-110">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="85443-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="85443-111">Prerequisites</span></span>  
<span data-ttu-id="85443-112">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="85443-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="85443-113">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 9 課： 建立階層](../tutorials/aas-lesson-9-create-hierarchies.md)。</span><span class="sxs-lookup"><span data-stu-id="85443-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="85443-114">建立分割區</span><span class="sxs-lookup"><span data-stu-id="85443-114">Create partitions</span></span>  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a><span data-ttu-id="85443-115">toocreate hello FactInternetSales 資料表中的資料分割</span><span class="sxs-lookup"><span data-stu-id="85443-115">toocreate partitions in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="85443-116">在 [表格式模型總管] 中，展開 [資料表]，然後以滑鼠右鍵按一下 [FactInternetSales] > [分割區]。</span><span class="sxs-lookup"><span data-stu-id="85443-116">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="85443-117">在 [資料分割管理員] 中，按一下**複製**，然後變更太 hello 名稱**FactInternetSales2010**。</span><span class="sxs-lookup"><span data-stu-id="85443-117">In Partition Manager, click **Copy**, and then change hello name too**FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="85443-118">因為要 hello 分割 tooinclude 那些資料列中的特定期間，hello 年度 2010，您必須修改 hello 查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="85443-118">Because you want hello partition tooinclude only those rows within a certain period, for hello year 2010, you must modify hello query expression.</span></span>
  
4.  <span data-ttu-id="85443-119">按一下**設計**tooopen 查詢編輯器，然後按一下hello **FactInternetSales2010**查詢。</span><span class="sxs-lookup"><span data-stu-id="85443-119">Click **Design** tooopen Query Editor, and then click hello **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="85443-120">在預覽中，按一下向下箭號，在 hello hello **OrderDate**資料行標題，然後按一下**日期/時間篩選器** > **之間**。</span><span class="sxs-lookup"><span data-stu-id="85443-120">In preview, click hello down arrow in hello **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas 第 10 課查詢編輯器](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="85443-122">在 hello 篩選的資料列 對話方塊中**顯示資料列，其中： OrderDate**，保留**之後或等於**，然後在 hello 日期欄位中，輸入**1/1/2010年**。</span><span class="sxs-lookup"><span data-stu-id="85443-122">In hello Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in hello date field, enter **1/1/2010**.</span></span> <span data-ttu-id="85443-123">保留 hello**和**運算子選取，然後選取**之前**，然後在 hello 日期欄位中，輸入**2011 年 1 月 1 日**，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="85443-123">Leave hello **And** operator selected, then select **is before**, then in hello date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="85443-125">請注意，在查詢編輯器的 APPLIED STEPS 中，您會看到另一個名為 Filtered Rows 步驟。</span><span class="sxs-lookup"><span data-stu-id="85443-125">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="85443-126">此篩選器是從 2010 tooselect 唯一訂單日期。</span><span class="sxs-lookup"><span data-stu-id="85443-126">This filter is tooselect only order dates from 2010.</span></span>

8.  <span data-ttu-id="85443-127">按一下 [匯入] 。</span><span class="sxs-lookup"><span data-stu-id="85443-127">Click **Import**.</span></span>

    <span data-ttu-id="85443-128">在 [資料分割管理員] 中，請注意 hello 運算式現在具有篩選資料列的額外子句的查詢。</span><span class="sxs-lookup"><span data-stu-id="85443-128">In Partition Manager, notice hello query expression now has an additional Filtered Rows clause.</span></span>

    ![aas 第 10 課查詢](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="85443-130">這個陳述式會指定此分割區應該包括只有 hello 資料 hello OrderDate 所在 hello 2010 日曆年度 hello 資料列篩選的子句中所指定資料列中。</span><span class="sxs-lookup"><span data-stu-id="85443-130">This statement specifies this partition should include only hello data in those rows where hello OrderDate is in hello 2010 calendar year as specified in hello filtered rows clause.</span></span>  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a><span data-ttu-id="85443-131">toocreate hello 2011 年的資料分割</span><span class="sxs-lookup"><span data-stu-id="85443-131">toocreate a partition for hello 2011 year</span></span>  
  
1.  <span data-ttu-id="85443-132">在 hello 資料分割清單中，按一下 hello **FactInternetSales2010**您所建立，資料分割，然後按一下**複製**。</span><span class="sxs-lookup"><span data-stu-id="85443-132">In hello partitions list, click hello **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="85443-133">Hello 磁碟分割名稱變更太**FactInternetSales2011**。</span><span class="sxs-lookup"><span data-stu-id="85443-133">Change hello partition name too**FactInternetSales2011**.</span></span> 

    <span data-ttu-id="85443-134">您不需要 toouse 查詢編輯器 toocreate 新的資料列篩選的子句。</span><span class="sxs-lookup"><span data-stu-id="85443-134">You do not need toouse Query Editor toocreate a new filtered rows clause.</span></span> <span data-ttu-id="85443-135">因為您可以建立一份 hello 查詢 2010，您只需要 toodo 是 2011 在 hello 查詢中有些微變更。</span><span class="sxs-lookup"><span data-stu-id="85443-135">Because you created a copy of hello query for 2010, all you need toodo is make a slight change in hello query for 2011.</span></span>
  
2.  <span data-ttu-id="85443-136">在**查詢運算式**、 為了讓這個資料分割 tooinclude 只有這些資料列中的 hello 2011 年、 取代 hello 子句篩選資料列中的 hello 年**2011年**和**2012**分別，例如：</span><span class="sxs-lookup"><span data-stu-id="85443-136">In **Query Expression**, in-order for this partition tooinclude only those rows for hello 2011 year, replace hello years in hello Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="85443-137">針對 2013、 2012年和 2014 toocreate 分割區。</span><span class="sxs-lookup"><span data-stu-id="85443-137">toocreate partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="85443-138">請遵循 hello 先前步驟中，為 2012年、 2013年和 2014，變更該年份的 hello 年 hello 篩選資料列子句 tooinclude 唯一資料列中建立資料分割。</span><span class="sxs-lookup"><span data-stu-id="85443-138">Follow hello previous steps, creating partitions for 2012, 2013, and 2014, changing hello years in hello Filtered Rows clause tooinclude only rows for that year.</span></span> 
  

## <a name="delete-hello-factinternetsales-partition"></a><span data-ttu-id="85443-139">刪除 hello FactInternetSales 磁碟分割</span><span class="sxs-lookup"><span data-stu-id="85443-139">Delete hello FactInternetSales partition</span></span>
<span data-ttu-id="85443-140">現在，您會有每年的資料分割，您可以刪除 hello FactInternetSales 磁碟分割。處理資料分割時，選擇所有的程序時，請避免重疊。</span><span class="sxs-lookup"><span data-stu-id="85443-140">Now that you have partitions for each year, you can delete hello FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="toodelete-hello-factinternetsales-partition"></a><span data-ttu-id="85443-141">toodelete hello FactInternetSales 磁碟分割</span><span class="sxs-lookup"><span data-stu-id="85443-141">toodelete hello FactInternetSales partition</span></span>
-  <span data-ttu-id="85443-142">按一下 hello FactInternetSales 磁碟分割，然後再按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="85443-142">Click hello FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="85443-143">處理分割區</span><span class="sxs-lookup"><span data-stu-id="85443-143">Process partitions</span></span>  
<span data-ttu-id="85443-144">在 [資料分割管理員] 中，請注意 hello**最後一個處理**hello 建立的顯示絕對不會處理這些資料分割的新資料分割的每個資料行。</span><span class="sxs-lookup"><span data-stu-id="85443-144">In Partition Manager, notice hello **Last Processed** column for each of hello new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="85443-145">當您建立資料分割時，則您應該執行處理資料分割或處理程序的資料表作業 toorefresh hello 資料，這些資料分割中。</span><span class="sxs-lookup"><span data-stu-id="85443-145">When you create partitions, you should run a Process Partitions or Process Table operation toorefresh hello data in those partitions.</span></span>  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a><span data-ttu-id="85443-146">tooprocess hello FactInternetSales 資料分割</span><span class="sxs-lookup"><span data-stu-id="85443-146">tooprocess hello FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="85443-147">按一下**確定**tooclose 資料分割管理員。</span><span class="sxs-lookup"><span data-stu-id="85443-147">Click **OK** tooclose Partition Manager.</span></span>  
  
2.  <span data-ttu-id="85443-148">按一下 hello **FactInternetSales**資料表，然後按一下 hello**模型**功能表 >**程序** > **處理資料分割**。</span><span class="sxs-lookup"><span data-stu-id="85443-148">Click hello **FactInternetSales** table, then click hello **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="85443-149">在 hello 處理資料分割對話方塊中，確認**模式**設定得**處理預設**。</span><span class="sxs-lookup"><span data-stu-id="85443-149">In hello Process Partitions dialog box, verify **Mode** is set too**Process Default**.</span></span>  
  
4.  <span data-ttu-id="85443-150">選取 hello hello 核取**程序**每 hello 五個資料行資料分割，您所建立，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="85443-150">Select hello checkbox in hello **Process** column for each of hello five partitions you created, and then click **OK**.</span></span>  

    ![aas 第 10 課處理分割區](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="85443-152">如果系統提示您輸入模擬認證，請輸入 hello Windows 使用者名稱和您在第 2 課中指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="85443-152">If you're prompted for Impersonation credentials, enter hello Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="85443-153">hello**資料處理**對話方塊隨即出現並顯示每個資料分割的處理序詳細資料。</span><span class="sxs-lookup"><span data-stu-id="85443-153">hello **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="85443-154">請注意，傳送給每個分割區的資料列數目都不同。</span><span class="sxs-lookup"><span data-stu-id="85443-154">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="85443-155">每個資料分割包含 hello 年 hello hello SQL 陳述式中 WHERE 子句中指定的資料列。</span><span class="sxs-lookup"><span data-stu-id="85443-155">Each partition includes only those rows for hello year specified in hello WHERE clause in hello SQL Statement.</span></span> <span data-ttu-id="85443-156">當處理完成時，請繼續並關閉 hello 資料處理 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="85443-156">When processing is finished, go ahead and close hello Data Processing dialog box.</span></span>  
  
    ![aas 第 10 課處理完成](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="85443-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85443-158">What's next?</span></span>
<span data-ttu-id="85443-159">下一課中移 toohello:[第 11 課： 建立角色](../tutorials/aas-lesson-11-create-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="85443-159">Go toohello next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
