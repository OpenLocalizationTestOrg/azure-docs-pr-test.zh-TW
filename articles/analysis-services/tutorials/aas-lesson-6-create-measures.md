---
<span data-ttu-id="1baae-101">標題： aaa"Azure Analysis Services 教學課程第 6 課： 建立量值 |Microsoft 文件"描述： 描述 toocreate hello Azure Analysis Services 教學課程專案中的量值。</span><span class="sxs-lookup"><span data-stu-id="1baae-101">title: aaa"Azure Analysis Services tutorial lesson 6: Create measures | Microsoft Docs" description: Describes how toocreate measures in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="1baae-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="1baae-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="1baae-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="1baae-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="1baae-104">第 6 課：建立量值</span><span class="sxs-lookup"><span data-stu-id="1baae-104">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="1baae-105">在這一課，您可以建立包含在模型中的量值 toobe。</span><span class="sxs-lookup"><span data-stu-id="1baae-105">In this lesson, you create measures toobe included in your model.</span></span> <span data-ttu-id="1baae-106">類似 toohello 計算您所建立的資料行、 量值是透過使用 DAX 公式所建立的計算。</span><span class="sxs-lookup"><span data-stu-id="1baae-106">Similar toohello calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="1baae-107">不過，與計算結果欄不同，量值評估是根據使用者選取的「篩選條件」。</span><span class="sxs-lookup"><span data-stu-id="1baae-107">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="1baae-108">例如，特定資料行或交叉分析篩選器 toohello 資料列標籤欄位加入樞紐分析表中。</span><span class="sxs-lookup"><span data-stu-id="1baae-108">For example, a particular column or slicer added toohello Row Labels field in a PivotTable.</span></span> <span data-ttu-id="1baae-109">Hello 篩選中的每個儲存格的值則會計算所套用的 hello 量值中。</span><span class="sxs-lookup"><span data-stu-id="1baae-109">A value for each cell in hello filter is then calculated by hello applied measure.</span></span> <span data-ttu-id="1baae-110">量值是功能強大、 有彈性的計算，您想 tooinclude 中幾乎所有表格式模型 tooperform 動態計算數值資料上。</span><span class="sxs-lookup"><span data-stu-id="1baae-110">Measures are powerful, flexible calculations that you want tooinclude in almost all tabular models tooperform dynamic calculations on numerical data.</span></span> <span data-ttu-id="1baae-111">詳細資訊，請參閱 toolearn[量值](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="1baae-111">toolearn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="1baae-112">toocreate 量值，使用 hello*量值方格*。</span><span class="sxs-lookup"><span data-stu-id="1baae-112">toocreate measures, you use hello *Measure Grid*.</span></span> <span data-ttu-id="1baae-113">根據預設，每個資料表都有一個空白量值方格；不過，您通常不會為每個資料表建立量值。</span><span class="sxs-lookup"><span data-stu-id="1baae-113">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="1baae-114">hello 量值方格隨即出現在資料檢視中的 hello 模型設計師中的資料表下方。</span><span class="sxs-lookup"><span data-stu-id="1baae-114">hello measure grid appears below a table in hello model designer when in Data View.</span></span> <span data-ttu-id="1baae-115">toohide 或顯示 hello 量值方格資料表中，按一下 hello**資料表**功能表，然後再按一下**顯示量值方格**。</span><span class="sxs-lookup"><span data-stu-id="1baae-115">toohide or show hello measure grid for a table, click hello **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="1baae-116">您可以按一下 hello 量值方格中的空資料格，然後再 hello 公式列中輸入 DAX 公式建立量值。</span><span class="sxs-lookup"><span data-stu-id="1baae-116">You can create a measure by clicking an empty cell in hello measure grid, and then typing a DAX formula in hello formula bar.</span></span> <span data-ttu-id="1baae-117">當您按一下 ENTER toocomplete hello 公式，hello 量值，則會顯示 hello 資料格中。</span><span class="sxs-lookup"><span data-stu-id="1baae-117">When you click ENTER toocomplete hello formula, hello measure then appears in hello cell.</span></span> <span data-ttu-id="1baae-118">您也可以建立資料行，即可使用標準彙總函式的量值，然後按一下 hello 加總 按鈕 (**∑**) hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="1baae-118">You can also create measures using a standard aggregation function by clicking a column, and then clicking hello AutoSum button (**∑**) on hello toolbar.</span></span> <span data-ttu-id="1baae-119">使用 hello 自動加總 功能建立的量值會出現在 hello 量值方格資料格正下方 hello 資料行，但是可以移動。</span><span class="sxs-lookup"><span data-stu-id="1baae-119">Measures created using hello AutoSum feature appear in hello measure grid cell directly beneath hello column, but can be moved.</span></span>  
  
<span data-ttu-id="1baae-120">在這一課，您會建立量值在 hello 公式列中，這兩個輸入 DAX 公式，而藉由使用 hello 自動加總功能。</span><span class="sxs-lookup"><span data-stu-id="1baae-120">In this lesson, you create measures by both entering a DAX formula in hello formula bar, and by using hello AutoSum feature.</span></span>  
  
<span data-ttu-id="1baae-121">本課程的估計時間 toocomplete: **30 分鐘**</span><span class="sxs-lookup"><span data-stu-id="1baae-121">Estimated time toocomplete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="1baae-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="1baae-122">Prerequisites</span></span>  
<span data-ttu-id="1baae-123">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="1baae-123">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="1baae-124">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 5 課： 建立導出資料行](../tutorials/aas-lesson-5-create-calculated-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="1baae-124">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="1baae-125">建立量值</span><span class="sxs-lookup"><span data-stu-id="1baae-125">Create measures</span></span>  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a><span data-ttu-id="1baae-126">toocreate DaysCurrentQuarterToDate 中的量值 hello DimDate 資料表</span><span class="sxs-lookup"><span data-stu-id="1baae-126">toocreate a DaysCurrentQuarterToDate measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="1baae-127">在 hello 模型設計師中，按一下 hello **DimDate**資料表。</span><span class="sxs-lookup"><span data-stu-id="1baae-127">In hello model designer, click hello **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="1baae-128">在 hello 量值方格中，按一下 hello 左上方的空資料格。</span><span class="sxs-lookup"><span data-stu-id="1baae-128">In hello measure grid, click hello top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="1baae-129">Hello 公式列中輸入下列公式的 hello:</span><span class="sxs-lookup"><span data-stu-id="1baae-129">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="1baae-130">請注意 hello 左上資料格現在包含量值名稱， **DaysCurrentQuarterToDate**，後面接著 hello 結果**92**。</span><span class="sxs-lookup"><span data-stu-id="1baae-130">Notice hello top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by hello result, **92**.</span></span>
    
      ![aas 第 6 課新增量值](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="1baae-132">不同於導出資料行，量值公式與您可以輸入 hello 量值名稱，後面接著冒號，後面接著 hello 公式的運算式。</span><span class="sxs-lookup"><span data-stu-id="1baae-132">Unlike calculated columns, with measure formulas you can type hello measure name, followed by a colon, followed by hello formula expression.</span></span>

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a><span data-ttu-id="1baae-133">toocreate DaysInCurrentQuarter 中的量值 hello DimDate 資料表</span><span class="sxs-lookup"><span data-stu-id="1baae-133">toocreate a DaysInCurrentQuarter measure in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="1baae-134">以 hello **DimDate**資料表仍為使用中 hello 量值方格中的 hello 模型設計師中，按一下 hello hello 您建立的量值下方的空資料格。</span><span class="sxs-lookup"><span data-stu-id="1baae-134">With hello **DimDate** table still active in hello model designer, in hello measure grid, click hello empty cell below hello measure you created.</span></span>  
  
2.  <span data-ttu-id="1baae-135">Hello 公式列中輸入下列公式的 hello:</span><span class="sxs-lookup"><span data-stu-id="1baae-135">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="1baae-136">在前一個期間建立一個不完整期間與 hello 之間的比率。</span><span class="sxs-lookup"><span data-stu-id="1baae-136">When creating a comparison ratio between one incomplete period and hello previous period.</span></span> <span data-ttu-id="1baae-137">hello 公式必須計算 hello hello 期間已經過的比例，並比較它 toohello 相同比例 hello 中前一個期間。</span><span class="sxs-lookup"><span data-stu-id="1baae-137">hello formula must calculate hello proportion of hello period that has elapsed and compare it toohello same proportion in hello previous period.</span></span> <span data-ttu-id="1baae-138">在這種情況下，[DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 提供 hello 比例經過 hello 中目前的期間。</span><span class="sxs-lookup"><span data-stu-id="1baae-138">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives hello proportion elapsed in hello current period.</span></span>  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a><span data-ttu-id="1baae-139">toocreate hello FactInternetSales 資料表中的 InternetDistinctCountSalesOrder 量值</span><span class="sxs-lookup"><span data-stu-id="1baae-139">toocreate an InternetDistinctCountSalesOrder measure in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="1baae-140">按一下 hello **FactInternetSales**資料表。</span><span class="sxs-lookup"><span data-stu-id="1baae-140">Click hello **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="1baae-141">按一下 hello **SalesOrderNumber**資料行標題。</span><span class="sxs-lookup"><span data-stu-id="1baae-141">Click hello **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="1baae-142">Hello 工具列上，按一下 hello 向下一步 toohello 自動加總 (**∑**) 按鈕，然後再選取**DistinctCount**。</span><span class="sxs-lookup"><span data-stu-id="1baae-142">On hello toolbar, click hello down-arrow next toohello AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="1baae-143">hello 自動加總功能自動建立 hello 選資料行使用 hello DistinctCount 標準彙總公式的量值。</span><span class="sxs-lookup"><span data-stu-id="1baae-143">hello AutoSum feature automatically creates a measure for hello selected column using hello DistinctCount standard aggregation formula.</span></span>  
    
       ![aas 第 6 課新增量值 2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="1baae-145">在 hello 量值方格中，按一下 hello 新量值，然後在 hello**屬性**視窗，請在**量值名稱**，hello 量值重新命名過**InternetDistinctCountSalesOrder**。</span><span class="sxs-lookup"><span data-stu-id="1baae-145">In hello measure grid, click hello new measure, and then in hello **Properties** window, in **Measure Name**, rename hello measure too**InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a><span data-ttu-id="1baae-146">toocreate hello FactInternetSales 資料表中的其他量值</span><span class="sxs-lookup"><span data-stu-id="1baae-146">toocreate additional measures in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="1baae-147">使用 hello 自動加總功能，建立並命名下列量值的 hello:</span><span class="sxs-lookup"><span data-stu-id="1baae-147">By using hello AutoSum feature, create and name hello following measures:</span></span>  

    |<span data-ttu-id="1baae-148">資料欄</span><span class="sxs-lookup"><span data-stu-id="1baae-148">Column</span></span>|<span data-ttu-id="1baae-149">量值名稱</span><span class="sxs-lookup"><span data-stu-id="1baae-149">Measure name</span></span>|<span data-ttu-id="1baae-150">自動加總 (∑)</span><span class="sxs-lookup"><span data-stu-id="1baae-150">AutoSum (∑)</span></span>|<span data-ttu-id="1baae-151">公式</span><span class="sxs-lookup"><span data-stu-id="1baae-151">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="1baae-152">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="1baae-152">SalesOrderLineNumber</span></span>|<span data-ttu-id="1baae-153">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="1baae-153">InternetOrderLinesCount</span></span>|<span data-ttu-id="1baae-154">Count</span><span class="sxs-lookup"><span data-stu-id="1baae-154">Count</span></span>|<span data-ttu-id="1baae-155">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="1baae-155">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="1baae-156">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="1baae-156">OrderQuantity</span></span>|<span data-ttu-id="1baae-157">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="1baae-157">InternetTotalUnits</span></span>|<span data-ttu-id="1baae-158">總和</span><span class="sxs-lookup"><span data-stu-id="1baae-158">Sum</span></span>|<span data-ttu-id="1baae-159">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="1baae-159">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="1baae-160">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="1baae-160">DiscountAmount</span></span>|<span data-ttu-id="1baae-161">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="1baae-161">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="1baae-162">總和</span><span class="sxs-lookup"><span data-stu-id="1baae-162">Sum</span></span>|<span data-ttu-id="1baae-163">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="1baae-163">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="1baae-164">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="1baae-164">TotalProductCost</span></span>|<span data-ttu-id="1baae-165">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="1baae-165">InternetTotalProductCost</span></span>|<span data-ttu-id="1baae-166">總和</span><span class="sxs-lookup"><span data-stu-id="1baae-166">Sum</span></span>|<span data-ttu-id="1baae-167">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="1baae-167">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="1baae-168">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="1baae-168">SalesAmount</span></span>|<span data-ttu-id="1baae-169">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="1baae-169">InternetTotalSales</span></span>|<span data-ttu-id="1baae-170">總和</span><span class="sxs-lookup"><span data-stu-id="1baae-170">Sum</span></span>|<span data-ttu-id="1baae-171">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="1baae-171">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="1baae-172">Margin</span><span class="sxs-lookup"><span data-stu-id="1baae-172">Margin</span></span>|<span data-ttu-id="1baae-173">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="1baae-173">InternetTotalMargin</span></span>|<span data-ttu-id="1baae-174">總和</span><span class="sxs-lookup"><span data-stu-id="1baae-174">Sum</span></span>|<span data-ttu-id="1baae-175">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="1baae-175">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="1baae-176">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="1baae-176">TaxAmt</span></span>|<span data-ttu-id="1baae-177">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="1baae-177">InternetTotalTaxAmt</span></span>|<span data-ttu-id="1baae-178">總和</span><span class="sxs-lookup"><span data-stu-id="1baae-178">Sum</span></span>|<span data-ttu-id="1baae-179">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="1baae-179">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="1baae-180">Freight</span><span class="sxs-lookup"><span data-stu-id="1baae-180">Freight</span></span>|<span data-ttu-id="1baae-181">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="1baae-181">InternetTotalFreight</span></span>|<span data-ttu-id="1baae-182">總和</span><span class="sxs-lookup"><span data-stu-id="1baae-182">Sum</span></span>|<span data-ttu-id="1baae-183">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="1baae-183">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="1baae-184">按一下空白儲存格在 hello 量值方格中，而藉由使用 hello 公式列中建立，並中順序的名稱 hello 下列量值：</span><span class="sxs-lookup"><span data-stu-id="1baae-184">By clicking an empty cell in hello measure grid, and by using hello formula bar, create, and name hello following measures in order:</span></span>  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
<span data-ttu-id="1baae-185">針對 hello FactInternetSales 資料表所建立的量值也可以使用的 tooanalyze 重大財務資料，例如銷售額、 成本與 hello 使用者選取的篩選所定義的項目獲利率。</span><span class="sxs-lookup"><span data-stu-id="1baae-185">Measures created for hello FactInternetSales table can be used tooanalyze critical financial data such as sales, costs, and profit margin for items defined by hello user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="1baae-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1baae-186">What's next?</span></span>
<span data-ttu-id="1baae-187">[第 7 課：建立關鍵效能指標](../tutorials/aas-lesson-7-create-key-performance-indicators.md)。</span><span class="sxs-lookup"><span data-stu-id="1baae-187">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
