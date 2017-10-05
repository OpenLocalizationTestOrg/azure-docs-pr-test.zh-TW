---
title: "Azure Analysis Services 教學課程第 6 課：建立量值 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中建立量值。"
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
ms.openlocfilehash: 90833fa9744eac298b0da82cd3d12f27cc237510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-6-create-measures"></a><span data-ttu-id="21ceb-103">第 6 課：建立量值</span><span class="sxs-lookup"><span data-stu-id="21ceb-103">Lesson 6: Create measures</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="21ceb-104">在這堂課中，您將會建立要加入模型中的量值。</span><span class="sxs-lookup"><span data-stu-id="21ceb-104">In this lesson, you create measures to be included in your model.</span></span> <span data-ttu-id="21ceb-105">類似於您所建立的計算結果欄，量值是利用 DAX 公式所建立的計算結果。</span><span class="sxs-lookup"><span data-stu-id="21ceb-105">Similar to the calculated columns you created, a measure is a calculation created by using a DAX formula.</span></span> <span data-ttu-id="21ceb-106">不過，與計算結果欄不同，量值評估是根據使用者選取的「篩選條件」。</span><span class="sxs-lookup"><span data-stu-id="21ceb-106">However, unlike calculated columns, measures are evaluated based on a user selected *filter*.</span></span> <span data-ttu-id="21ceb-107">例如，在樞紐分析表的 [資料列標籤] 欄位中新增的特定資料行或交叉分析篩選器。</span><span class="sxs-lookup"><span data-stu-id="21ceb-107">For example, a particular column or slicer added to the Row Labels field in a PivotTable.</span></span> <span data-ttu-id="21ceb-108">然後會以套用的量值，計算篩選條件中每個資料格的值。</span><span class="sxs-lookup"><span data-stu-id="21ceb-108">A value for each cell in the filter is then calculated by the applied measure.</span></span> <span data-ttu-id="21ceb-109">量值是功能強大又靈活的計算，在幾乎所有表格式模型中都會派上用場，可以對數值資料執行動態計算。</span><span class="sxs-lookup"><span data-stu-id="21ceb-109">Measures are powerful, flexible calculations that you want to include in almost all tabular models to perform dynamic calculations on numerical data.</span></span> <span data-ttu-id="21ceb-110">若要深入了解，請參閱[量值](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="21ceb-110">To learn more, see [Measures](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).</span></span>
  
<span data-ttu-id="21ceb-111">若要建立量值，您需要使用「量值方格」。</span><span class="sxs-lookup"><span data-stu-id="21ceb-111">To create measures, you use the *Measure Grid*.</span></span> <span data-ttu-id="21ceb-112">根據預設，每個資料表都有一個空白量值方格；不過，您通常不會為每個資料表建立量值。</span><span class="sxs-lookup"><span data-stu-id="21ceb-112">By default, each table has an empty measure grid; however, you typically do not create measures for every table.</span></span> <span data-ttu-id="21ceb-113">在資料檢視中，量值方格中會出現在模型設計師中的資料表下方。</span><span class="sxs-lookup"><span data-stu-id="21ceb-113">The measure grid appears below a table in the model designer when in Data View.</span></span> <span data-ttu-id="21ceb-114">若要隱藏或顯示資料表的量值方格，請按一下 [資料表] 功能表，然後按一下 [顯示量值方格]。</span><span class="sxs-lookup"><span data-stu-id="21ceb-114">To hide or show the measure grid for a table, click the **Table** menu, and then click **Show Measure Grid**.</span></span>  
  
<span data-ttu-id="21ceb-115">若要建立量值，您可以按一下量值方格中的空資料格，然後在公式列中輸入 DAX 公式。</span><span class="sxs-lookup"><span data-stu-id="21ceb-115">You can create a measure by clicking an empty cell in the measure grid, and then typing a DAX formula in the formula bar.</span></span> <span data-ttu-id="21ceb-116">當您按 ENTER 完成公式時，量值就會出現在資料格中。</span><span class="sxs-lookup"><span data-stu-id="21ceb-116">When you click ENTER to complete the formula, the measure then appears in the cell.</span></span> <span data-ttu-id="21ceb-117">您也可以按一下資料行，然後按一下工具列上的 [自動加總] 按鈕 (**∑**)，利用標準彙總函式建立量值。</span><span class="sxs-lookup"><span data-stu-id="21ceb-117">You can also create measures using a standard aggregation function by clicking a column, and then clicking the AutoSum button (**∑**) on the toolbar.</span></span> <span data-ttu-id="21ceb-118">使用「自動加總」功能所建立的量值會出現在資料行正下方的量值方格資料格中，但是可以移動。</span><span class="sxs-lookup"><span data-stu-id="21ceb-118">Measures created using the AutoSum feature appear in the measure grid cell directly beneath the column, but can be moved.</span></span>  
  
<span data-ttu-id="21ceb-119">在這堂課中，您會在公式列中輸入 DAX 公式和使用「自動加總」功能來建立量值。</span><span class="sxs-lookup"><span data-stu-id="21ceb-119">In this lesson, you create measures by both entering a DAX formula in the formula bar, and by using the AutoSum feature.</span></span>  
  
<span data-ttu-id="21ceb-120">這堂課的預估完成時間：**30 分鐘**</span><span class="sxs-lookup"><span data-stu-id="21ceb-120">Estimated time to complete this lesson: **30 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="21ceb-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="21ceb-121">Prerequisites</span></span>  
<span data-ttu-id="21ceb-122">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="21ceb-122">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="21ceb-123">在這堂課中執行工作之前，您必須已完成上一堂課︰[第 5 課︰建立計算結果欄](../tutorials/aas-lesson-5-create-calculated-columns.md)。</span><span class="sxs-lookup"><span data-stu-id="21ceb-123">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 5: Create calculated columns](../tutorials/aas-lesson-5-create-calculated-columns.md).</span></span>  
  
## <a name="create-measures"></a><span data-ttu-id="21ceb-124">建立量值</span><span class="sxs-lookup"><span data-stu-id="21ceb-124">Create measures</span></span>  
  
#### <a name="to-create-a-dayscurrentquartertodate-measure-in-the-dimdate-table"></a><span data-ttu-id="21ceb-125">在 DimDate 資料表中建立 DaysCurrentQuarterToDate 量值</span><span class="sxs-lookup"><span data-stu-id="21ceb-125">To create a DaysCurrentQuarterToDate measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="21ceb-126">在模型設計師中，按一下 [DimDate] 資料表。</span><span class="sxs-lookup"><span data-stu-id="21ceb-126">In the model designer, click the **DimDate** table.</span></span>  
  
2.  <span data-ttu-id="21ceb-127">在量值方格中，按一下左上方的空資料格。</span><span class="sxs-lookup"><span data-stu-id="21ceb-127">In the measure grid, click the top-left empty cell.</span></span>  
  
3.  <span data-ttu-id="21ceb-128">在公式列中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="21ceb-128">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    <span data-ttu-id="21ceb-129">請注意，左上方的資料格現在包含量值名稱 **DaysCurrentQuarterToDate**，後面接著結果 **92**。</span><span class="sxs-lookup"><span data-stu-id="21ceb-129">Notice the top-left cell now contains a measure name, **DaysCurrentQuarterToDate**, followed by the result, **92**.</span></span>
    
      ![aas 第 6 課新增量值](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    <span data-ttu-id="21ceb-131">不同於計算結果欄，量值公式可讓您輸入量值名稱，後面接著一個冒號，最後再接著公式運算式。</span><span class="sxs-lookup"><span data-stu-id="21ceb-131">Unlike calculated columns, with measure formulas you can type the measure name, followed by a colon, followed by the formula expression.</span></span>

  
#### <a name="to-create-a-daysincurrentquarter-measure-in-the-dimdate-table"></a><span data-ttu-id="21ceb-132">在 DimDate 資料表中建立 DaysInCurrentQuarter 量值</span><span class="sxs-lookup"><span data-stu-id="21ceb-132">To create a DaysInCurrentQuarter measure in the DimDate table</span></span>  
  
1.  <span data-ttu-id="21ceb-133">在模型設計師中繼續使用 **DimDate** 資料表，然後在量值方格中，按一下您建立之量值下方的空資料格。</span><span class="sxs-lookup"><span data-stu-id="21ceb-133">With the **DimDate** table still active in the model designer, in the measure grid, click the empty cell below the measure you created.</span></span>  
  
2.  <span data-ttu-id="21ceb-134">在公式列中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="21ceb-134">In the formula bar, type the following formula:</span></span>  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    <span data-ttu-id="21ceb-135">在一個不完整期間與前一個期間之間建立比率時，</span><span class="sxs-lookup"><span data-stu-id="21ceb-135">When creating a comparison ratio between one incomplete period and the previous period.</span></span> <span data-ttu-id="21ceb-136">此公式必須計算該期間已流逝的比例，並與前一個期間的相同比例做比較。</span><span class="sxs-lookup"><span data-stu-id="21ceb-136">The formula must calculate the proportion of the period that has elapsed and compare it to the same proportion in the previous period.</span></span> <span data-ttu-id="21ceb-137">在此案例中，[DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] 計算出目前期間已流逝的比例。</span><span class="sxs-lookup"><span data-stu-id="21ceb-137">In this case, [DaysCurrentQuarterToDate]/[DaysInCurrentQuarter] gives the proportion elapsed in the current period.</span></span>  
  
#### <a name="to-create-an-internetdistinctcountsalesorder-measure-in-the-factinternetsales-table"></a><span data-ttu-id="21ceb-138">在 FactInternetSales 資料表中建立 InternetDistinctCountSalesOrder 量值</span><span class="sxs-lookup"><span data-stu-id="21ceb-138">To create an InternetDistinctCountSalesOrder measure in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="21ceb-139">按一下 [FactInternetSales] 資料表。</span><span class="sxs-lookup"><span data-stu-id="21ceb-139">Click the **FactInternetSales** table.</span></span>   
  
2.  <span data-ttu-id="21ceb-140">按一下 [SalesOrderNumber] 資料行標題。</span><span class="sxs-lookup"><span data-stu-id="21ceb-140">Click the **SalesOrderNumber** column heading.</span></span>  
  
3.  <span data-ttu-id="21ceb-141">在工具列上，按一下 [自動加總] \(**∑**) 按鈕旁的向下箭號，然後選取 [DistinctCount]。</span><span class="sxs-lookup"><span data-stu-id="21ceb-141">On the toolbar, click the down-arrow next to the AutoSum (**∑**) button, and then select **DistinctCount**.</span></span>  
  
    <span data-ttu-id="21ceb-142">「自動加總」功能會使用 DistinctCount 標準彙總公式，自動為選取的資料行建立量值。</span><span class="sxs-lookup"><span data-stu-id="21ceb-142">The AutoSum feature automatically creates a measure for the selected column using the DistinctCount standard aggregation formula.</span></span>  
    
       ![aas 第 6 課新增量值 2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  <span data-ttu-id="21ceb-144">在量值方格中，按一下新量值，然後在 [屬性] 視窗的 [量值名稱] 中，將量值重新命名為 **InternetDistinctCountSalesOrder**。</span><span class="sxs-lookup"><span data-stu-id="21ceb-144">In the measure grid, click the new measure, and then in the **Properties** window, in **Measure Name**, rename the measure to **InternetDistinctCountSalesOrder**.</span></span> 
 
  
#### <a name="to-create-additional-measures-in-the-factinternetsales-table"></a><span data-ttu-id="21ceb-145">在 FactInternetSales 資料表中建立其他量值</span><span class="sxs-lookup"><span data-stu-id="21ceb-145">To create additional measures in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="21ceb-146">使用「自動加總」功能建立並命名下列量值︰</span><span class="sxs-lookup"><span data-stu-id="21ceb-146">By using the AutoSum feature, create and name the following measures:</span></span>  

    |<span data-ttu-id="21ceb-147">資料欄</span><span class="sxs-lookup"><span data-stu-id="21ceb-147">Column</span></span>|<span data-ttu-id="21ceb-148">量值名稱</span><span class="sxs-lookup"><span data-stu-id="21ceb-148">Measure name</span></span>|<span data-ttu-id="21ceb-149">自動加總 (∑)</span><span class="sxs-lookup"><span data-stu-id="21ceb-149">AutoSum (∑)</span></span>|<span data-ttu-id="21ceb-150">公式</span><span class="sxs-lookup"><span data-stu-id="21ceb-150">Formula</span></span>|  
    |----------------|----------|-----------------|-----------|  
    |<span data-ttu-id="21ceb-151">SalesOrderLineNumber</span><span class="sxs-lookup"><span data-stu-id="21ceb-151">SalesOrderLineNumber</span></span>|<span data-ttu-id="21ceb-152">InternetOrderLinesCount</span><span class="sxs-lookup"><span data-stu-id="21ceb-152">InternetOrderLinesCount</span></span>|<span data-ttu-id="21ceb-153">Count</span><span class="sxs-lookup"><span data-stu-id="21ceb-153">Count</span></span>|<span data-ttu-id="21ceb-154">=COUNTA([SalesOrderLineNumber])</span><span class="sxs-lookup"><span data-stu-id="21ceb-154">=COUNTA([SalesOrderLineNumber])</span></span>|  
    |<span data-ttu-id="21ceb-155">OrderQuantity</span><span class="sxs-lookup"><span data-stu-id="21ceb-155">OrderQuantity</span></span>|<span data-ttu-id="21ceb-156">InternetTotalUnits</span><span class="sxs-lookup"><span data-stu-id="21ceb-156">InternetTotalUnits</span></span>|<span data-ttu-id="21ceb-157">總和</span><span class="sxs-lookup"><span data-stu-id="21ceb-157">Sum</span></span>|<span data-ttu-id="21ceb-158">=SUM([OrderQuantity])</span><span class="sxs-lookup"><span data-stu-id="21ceb-158">=SUM([OrderQuantity])</span></span>|  
    |<span data-ttu-id="21ceb-159">DiscountAmount</span><span class="sxs-lookup"><span data-stu-id="21ceb-159">DiscountAmount</span></span>|<span data-ttu-id="21ceb-160">InternetTotalDiscountAmount</span><span class="sxs-lookup"><span data-stu-id="21ceb-160">InternetTotalDiscountAmount</span></span>|<span data-ttu-id="21ceb-161">總和</span><span class="sxs-lookup"><span data-stu-id="21ceb-161">Sum</span></span>|<span data-ttu-id="21ceb-162">=SUM([DiscountAmount])</span><span class="sxs-lookup"><span data-stu-id="21ceb-162">=SUM([DiscountAmount])</span></span>|  
    |<span data-ttu-id="21ceb-163">TotalProductCost</span><span class="sxs-lookup"><span data-stu-id="21ceb-163">TotalProductCost</span></span>|<span data-ttu-id="21ceb-164">InternetTotalProductCost</span><span class="sxs-lookup"><span data-stu-id="21ceb-164">InternetTotalProductCost</span></span>|<span data-ttu-id="21ceb-165">總和</span><span class="sxs-lookup"><span data-stu-id="21ceb-165">Sum</span></span>|<span data-ttu-id="21ceb-166">=SUM([TotalProductCost])</span><span class="sxs-lookup"><span data-stu-id="21ceb-166">=SUM([TotalProductCost])</span></span>|  
    |<span data-ttu-id="21ceb-167">SalesAmount</span><span class="sxs-lookup"><span data-stu-id="21ceb-167">SalesAmount</span></span>|<span data-ttu-id="21ceb-168">InternetTotalSales</span><span class="sxs-lookup"><span data-stu-id="21ceb-168">InternetTotalSales</span></span>|<span data-ttu-id="21ceb-169">總和</span><span class="sxs-lookup"><span data-stu-id="21ceb-169">Sum</span></span>|<span data-ttu-id="21ceb-170">=SUM([SalesAmount])</span><span class="sxs-lookup"><span data-stu-id="21ceb-170">=SUM([SalesAmount])</span></span>|  
    |<span data-ttu-id="21ceb-171">Margin</span><span class="sxs-lookup"><span data-stu-id="21ceb-171">Margin</span></span>|<span data-ttu-id="21ceb-172">InternetTotalMargin</span><span class="sxs-lookup"><span data-stu-id="21ceb-172">InternetTotalMargin</span></span>|<span data-ttu-id="21ceb-173">總和</span><span class="sxs-lookup"><span data-stu-id="21ceb-173">Sum</span></span>|<span data-ttu-id="21ceb-174">=SUM([Margin])</span><span class="sxs-lookup"><span data-stu-id="21ceb-174">=SUM([Margin])</span></span>|  
    |<span data-ttu-id="21ceb-175">TaxAmt</span><span class="sxs-lookup"><span data-stu-id="21ceb-175">TaxAmt</span></span>|<span data-ttu-id="21ceb-176">InternetTotalTaxAmt</span><span class="sxs-lookup"><span data-stu-id="21ceb-176">InternetTotalTaxAmt</span></span>|<span data-ttu-id="21ceb-177">總和</span><span class="sxs-lookup"><span data-stu-id="21ceb-177">Sum</span></span>|<span data-ttu-id="21ceb-178">=SUM([TaxAmt])</span><span class="sxs-lookup"><span data-stu-id="21ceb-178">=SUM([TaxAmt])</span></span>|  
    |<span data-ttu-id="21ceb-179">Freight</span><span class="sxs-lookup"><span data-stu-id="21ceb-179">Freight</span></span>|<span data-ttu-id="21ceb-180">InternetTotalFreight</span><span class="sxs-lookup"><span data-stu-id="21ceb-180">InternetTotalFreight</span></span>|<span data-ttu-id="21ceb-181">總和</span><span class="sxs-lookup"><span data-stu-id="21ceb-181">Sum</span></span>|<span data-ttu-id="21ceb-182">=SUM([Freight])</span><span class="sxs-lookup"><span data-stu-id="21ceb-182">=SUM([Freight])</span></span>|  
  
2.  <span data-ttu-id="21ceb-183">按一下量值方格中的空資料格並使用公式列，依序建立和命名下列量值︰</span><span class="sxs-lookup"><span data-stu-id="21ceb-183">By clicking an empty cell in the measure grid, and by using the formula bar, create, and name the following measures in order:</span></span>  
  
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
  
<span data-ttu-id="21ceb-184">針對 FactInternetSales 資料表所建立的量值可用來分析重要財務資料，例如，使用者選取的篩選條件所定義之商品的銷售額、成本和獲利率。</span><span class="sxs-lookup"><span data-stu-id="21ceb-184">Measures created for the FactInternetSales table can be used to analyze critical financial data such as sales, costs, and profit margin for items defined by the user selected filter.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="21ceb-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21ceb-185">What's next?</span></span>
<span data-ttu-id="21ceb-186">[第 7 課：建立關鍵效能指標](../tutorials/aas-lesson-7-create-key-performance-indicators.md)。</span><span class="sxs-lookup"><span data-stu-id="21ceb-186">[Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  

  
