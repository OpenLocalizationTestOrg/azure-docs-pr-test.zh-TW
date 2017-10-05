---
title: "Azure Analysis Services 教學課程第 5 課：建立計算結果欄 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中建立計算結果欄。"
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
ms.openlocfilehash: 893371145d77e156843271907aeef0c3756d0403
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="3b176-103">第 5 課：建立計算結果欄</span><span class="sxs-lookup"><span data-stu-id="3b176-103">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="3b176-104">在這堂課中，您會在模型中新增計算結果欄來建立資料。</span><span class="sxs-lookup"><span data-stu-id="3b176-104">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="3b176-105">您可以在使用「取得資料」(使用查詢編輯器) 時建立計算結果欄 (作為自訂資料行)，或稍後在模型設計師中再如法泡製。</span><span class="sxs-lookup"><span data-stu-id="3b176-105">You can create calculated columns (as custom columns) when using Get Data, by using the Query Editor, or later in the model designer like you do here.</span></span> <span data-ttu-id="3b176-106">若要深入了解，請參閱[計算結果欄](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns)。</span><span class="sxs-lookup"><span data-stu-id="3b176-106">To learn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="3b176-107">您會在三個不同的資料表中建立五個新的計算結果欄。</span><span class="sxs-lookup"><span data-stu-id="3b176-107">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="3b176-108">每個工作的步驟稍有不同，以顯示有數種方式可建立資料行、重新命名資料行，並將它們放在資料表中的不同位置。</span><span class="sxs-lookup"><span data-stu-id="3b176-108">The steps are slightly different for each task showing there are several ways to create columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="3b176-109">您會在這堂課中第一次使用 Data Analysis Expressions (DAX)。</span><span class="sxs-lookup"><span data-stu-id="3b176-109">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="3b176-110">DAX 是一種特殊語言，可以為表格式模型建立可靈活自訂的公式運算式。</span><span class="sxs-lookup"><span data-stu-id="3b176-110">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="3b176-111">在本教學課程中，您會使用 DAX 來建立計算結果欄、量值和角色篩選條件。</span><span class="sxs-lookup"><span data-stu-id="3b176-111">In this tutorial, you use DAX to create calculated columns, measures, and role filters.</span></span> <span data-ttu-id="3b176-112">若要深入了解，請參閱[表格式模型中的 DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="3b176-112">To learn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="3b176-113">這堂課的預估完成時間：**15 分鐘**</span><span class="sxs-lookup"><span data-stu-id="3b176-113">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="3b176-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="3b176-114">Prerequisites</span></span>  
<span data-ttu-id="3b176-115">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="3b176-115">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="3b176-116">在這堂課中執行工作之前，您必須已完成上一堂課︰[第 4 課︰建立關聯性](../tutorials/aas-lesson-4-create-relationships.md)。</span><span class="sxs-lookup"><span data-stu-id="3b176-116">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="3b176-117">建立計算結果欄</span><span class="sxs-lookup"><span data-stu-id="3b176-117">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="3b176-118">在 DimDate 資料表中建立 MonthCalendar 計算結果欄</span><span class="sxs-lookup"><span data-stu-id="3b176-118">Create a MonthCalendar calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="3b176-119">按一下 [模型] 功能表 > [模型檢視] > [資料檢視]。</span><span class="sxs-lookup"><span data-stu-id="3b176-119">Click the **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="3b176-120">只有在資料檢視中使用模型設計師，才能建立計算結果欄。</span><span class="sxs-lookup"><span data-stu-id="3b176-120">Calculated columns can only be created by using the model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="3b176-121">在模型設計師中，按一下 [DimDate] 資料表 (索引標籤)。</span><span class="sxs-lookup"><span data-stu-id="3b176-121">In the model designer, click the **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="3b176-122">以滑鼠右鍵按一下 [CalendarQuarter] 資料行標頭，然後按一下 [插入資料行]。</span><span class="sxs-lookup"><span data-stu-id="3b176-122">Right-click the **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="3b176-123">[日曆季] 資料行左側會插入名為 [計算結果欄 1] 的新資料行。</span><span class="sxs-lookup"><span data-stu-id="3b176-123">A new column named **Calculated Column 1** is inserted to the left of the **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="3b176-124">在資料表上方的公式列中，輸入下列 DAX 公式：「自動完成」會協助您輸入資料行和資料表的完整名稱，並列出可用的函式。</span><span class="sxs-lookup"><span data-stu-id="3b176-124">In the formula bar above the table, type the following DAX formula: AutoComplete helps you type the fully qualified names of columns and tables, and lists the functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="3b176-125">接著，計算結果欄的所有資料列就會填入值。</span><span class="sxs-lookup"><span data-stu-id="3b176-125">Values are then populated for all the rows in the calculated column.</span></span> <span data-ttu-id="3b176-126">如果您在資料表中向下捲動，根據每個資料列中的資料，您會看到各資料列在此資料行中會有不同的值。</span><span class="sxs-lookup"><span data-stu-id="3b176-126">If you scroll down through the table, you see rows can have different values for this column, based on the data in each row.</span></span>    
  
5.  <span data-ttu-id="3b176-127">將此資料行重新命名為 **MonthCalendar**。</span><span class="sxs-lookup"><span data-stu-id="3b176-127">Rename this column to **MonthCalendar**.</span></span> 

    ![aas 第 5 課新增資料行](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="3b176-129">MonthCalendar 計算結果欄提供可排序的月份名稱。</span><span class="sxs-lookup"><span data-stu-id="3b176-129">The MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a><span data-ttu-id="3b176-130">在 DimDate 資料表中建立 DayOfWeek 計算結果欄</span><span class="sxs-lookup"><span data-stu-id="3b176-130">Create a DayOfWeek calculated column in the DimDate table</span></span>  
  
1.  <span data-ttu-id="3b176-131">繼續使用 **DimDate** 資料表，按一下 [資料行] 功能表，然後按一下 [新增資料行]。</span><span class="sxs-lookup"><span data-stu-id="3b176-131">With the **DimDate** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="3b176-132">在公式列中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="3b176-132">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="3b176-133">當您完成建立公式時，請按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="3b176-133">When you've finished building the formula, press ENTER.</span></span> <span data-ttu-id="3b176-134">新的資料行會新增至資料表的最右邊。</span><span class="sxs-lookup"><span data-stu-id="3b176-134">The new column is added to the far right of the table.</span></span>  
  
3.  <span data-ttu-id="3b176-135">將資料行重新命名為 **DayOfWeek**。</span><span class="sxs-lookup"><span data-stu-id="3b176-135">Rename the column to **DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="3b176-136">按一下資料行標題，然後將資料行拖曳到 **EnglishDayNameOfWeek** 資料行和 **DayNumberOfMonth** 資料行之間。</span><span class="sxs-lookup"><span data-stu-id="3b176-136">Click the column heading, and then drag the column between the **EnglishDayNameOfWeek** column and the **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="3b176-137">移動資料表中的資料行可讓您更輕鬆地瀏覽。</span><span class="sxs-lookup"><span data-stu-id="3b176-137">Moving columns in your table makes it easier to navigate.</span></span>  
  
<span data-ttu-id="3b176-138">DayOfWeek 計算結果欄提供可排序的星期幾名稱。</span><span class="sxs-lookup"><span data-stu-id="3b176-138">The DayOfWeek calculated column provides a sortable name for the day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="3b176-139">在 DimProduct 資料表中建立 ProductSubcategoryName 計算結果欄</span><span class="sxs-lookup"><span data-stu-id="3b176-139">Create a ProductSubcategoryName calculated column in the DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="3b176-140">在 **DimProduct** 資料表中，捲動到資料表最右邊。</span><span class="sxs-lookup"><span data-stu-id="3b176-140">In the **DimProduct** table, scroll to the far right of the table.</span></span> <span data-ttu-id="3b176-141">請注意，最右邊的資料行名為 **[新增資料行]** \(斜體)，請按一下資料行標題。</span><span class="sxs-lookup"><span data-stu-id="3b176-141">Notice the right-most column is named **Add Column** (italicized), click the column heading.</span></span>  
  
2.  <span data-ttu-id="3b176-142">在公式列中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="3b176-142">In the formula bar, type the following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="3b176-143">將資料行重新命名為 **ProductSubcategoryName**。</span><span class="sxs-lookup"><span data-stu-id="3b176-143">Rename the column to **ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="3b176-144">ProductSubcategoryName 計算結果欄用於在 DimProduct 資料表中建立階層，此階層包含來自 DimProductSubcategory 資料表之 EnglishProductSubcategoryName 資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="3b176-144">The ProductSubcategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductSubcategoryName column in the DimProductSubcategory table.</span></span> <span data-ttu-id="3b176-145">階層不可跨越多個資料表。</span><span class="sxs-lookup"><span data-stu-id="3b176-145">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="3b176-146">稍後您會在第 9 課中建立階層。</span><span class="sxs-lookup"><span data-stu-id="3b176-146">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a><span data-ttu-id="3b176-147">在 DimProduct 資料表中建立 ProductCategoryName 計算結果欄</span><span class="sxs-lookup"><span data-stu-id="3b176-147">Create a ProductCategoryName calculated column in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="3b176-148">繼續使用 **DimProduct** 資料表，按一下 [資料行] 功能表，然後按一下 [新增資料行]。</span><span class="sxs-lookup"><span data-stu-id="3b176-148">With the **DimProduct** table still active, click the **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="3b176-149">在公式列中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="3b176-149">In the formula bar, type the following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="3b176-150">將資料行重新命名為 **ProductCategoryName**。</span><span class="sxs-lookup"><span data-stu-id="3b176-150">Rename the column to **ProductCategoryName**.</span></span>  
  
<span data-ttu-id="3b176-151">ProductCategoryName 計算結果欄用於在 DimProduct 資料表中建立階層，此階層包含來自 DimProductCategory 資料表之 EnglishProductCategoryName 資料行的資料。</span><span class="sxs-lookup"><span data-stu-id="3b176-151">The ProductCategoryName calculated column is used to create a hierarchy in the DimProduct table, which includes data from the EnglishProductCategoryName column in the DimProductCategory table.</span></span> <span data-ttu-id="3b176-152">階層不可跨越多個資料表。</span><span class="sxs-lookup"><span data-stu-id="3b176-152">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a><span data-ttu-id="3b176-153">在 FactInternetSales 資料表中建立 Margin 計算結果欄</span><span class="sxs-lookup"><span data-stu-id="3b176-153">Create a Margin calculated column in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="3b176-154">在模型設計師中，選取 [FactInternetSales] 資料表。</span><span class="sxs-lookup"><span data-stu-id="3b176-154">In the model designer, select the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="3b176-155">在 **SalesAmount** 資料行和 **TaxAmt** 資料行之間建立新的計算結果欄。</span><span class="sxs-lookup"><span data-stu-id="3b176-155">Create a new calculated column between the **SalesAmount** column and the **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="3b176-156">在公式列中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="3b176-156">In the formula bar, type the following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="3b176-157">將資料行重新命名為 **Margin**。</span><span class="sxs-lookup"><span data-stu-id="3b176-157">Rename the column to **Margin**.</span></span>  
 
      ![aas 第 5 課新增獲利率](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="3b176-159">Margin 計算結果欄用來分析每一筆銷售的獲利率。</span><span class="sxs-lookup"><span data-stu-id="3b176-159">The Margin calculated column is used to analyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="3b176-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b176-160">What's next?</span></span>
<span data-ttu-id="3b176-161">[第 6 課：建立量值](../tutorials/aas-lesson-6-create-measures.md)。</span><span class="sxs-lookup"><span data-stu-id="3b176-161">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
