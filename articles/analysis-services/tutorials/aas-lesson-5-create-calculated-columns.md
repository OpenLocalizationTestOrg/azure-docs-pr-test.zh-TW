---
<span data-ttu-id="d21e1-101">標題： aaa"Azure Analysis Services 教學課程第 5 課： 建立導出資料行 |Microsoft 文件"描述： 說明如何 toocreate 算出 hello Azure Analysis Services 教學課程專案中的資料行。</span><span class="sxs-lookup"><span data-stu-id="d21e1-101">title: aaa"Azure Analysis Services tutorial lesson 5: Create calculated columns | Microsoft Docs" description: Describes how toocreate calculated columns in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="d21e1-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="d21e1-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="d21e1-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="d21e1-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend</span></span>
---
# <a name="lesson-5-create-calculated-columns"></a><span data-ttu-id="d21e1-104">第 5 課：建立計算結果欄</span><span class="sxs-lookup"><span data-stu-id="d21e1-104">Lesson 5: Create calculated columns</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="d21e1-105">在這堂課中，您會在模型中新增計算結果欄來建立資料。</span><span class="sxs-lookup"><span data-stu-id="d21e1-105">In this lesson, you create data in your model by adding calculated columns.</span></span> <span data-ttu-id="d21e1-106">您可以建立導出資料行 （做為自訂的資料行） 時使用 取得資料，使用 hello 查詢編輯器中，或稍後在 hello 模型設計工具類似您執行以下。</span><span class="sxs-lookup"><span data-stu-id="d21e1-106">You can create calculated columns (as custom columns) when using Get Data, by using hello Query Editor, or later in hello model designer like you do here.</span></span> <span data-ttu-id="d21e1-107">詳細資訊，請參閱 toolearn[導出資料行](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns)。</span><span class="sxs-lookup"><span data-stu-id="d21e1-107">toolearn more, see [Calculated columns](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns).</span></span>
  
<span data-ttu-id="d21e1-108">您會在三個不同的資料表中建立五個新的計算結果欄。</span><span class="sxs-lookup"><span data-stu-id="d21e1-108">You create five new calculated columns in three different tables.</span></span> <span data-ttu-id="d21e1-109">hello 步驟會稍有不同的每個工作顯示有許多種 toocreate 資料行、 重新命名，並將它們放在不同資料表中的位置。</span><span class="sxs-lookup"><span data-stu-id="d21e1-109">hello steps are slightly different for each task showing there are several ways toocreate columns, rename them, and place them in various locations in a table.</span></span>  

<span data-ttu-id="d21e1-110">您會在這堂課中第一次使用 Data Analysis Expressions (DAX)。</span><span class="sxs-lookup"><span data-stu-id="d21e1-110">This lesson is also where you first use Data Analysis Expressions (DAX).</span></span> <span data-ttu-id="d21e1-111">DAX 是一種特殊語言，可以為表格式模型建立可靈活自訂的公式運算式。</span><span class="sxs-lookup"><span data-stu-id="d21e1-111">DAX is a special language for creating highly customizable formula expressions for tabular models.</span></span> <span data-ttu-id="d21e1-112">在本教學課程中，您可以使用 DAX toocreate 導出資料行、 量值和角色篩選。</span><span class="sxs-lookup"><span data-stu-id="d21e1-112">In this tutorial, you use DAX toocreate calculated columns, measures, and role filters.</span></span> <span data-ttu-id="d21e1-113">詳細資訊，請參閱 toolearn[表格式模型中的 DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular)。</span><span class="sxs-lookup"><span data-stu-id="d21e1-113">toolearn more, see [DAX in tabular models](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular).</span></span> 
  
<span data-ttu-id="d21e1-114">本課程的估計時間 toocomplete: **15 分鐘**</span><span class="sxs-lookup"><span data-stu-id="d21e1-114">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d21e1-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="d21e1-115">Prerequisites</span></span>  
<span data-ttu-id="d21e1-116">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="d21e1-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="d21e1-117">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 4 課： 建立關聯性](../tutorials/aas-lesson-4-create-relationships.md)。</span><span class="sxs-lookup"><span data-stu-id="d21e1-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span> 
  
## <a name="create-calculated-columns"></a><span data-ttu-id="d21e1-118">建立計算結果欄</span><span class="sxs-lookup"><span data-stu-id="d21e1-118">Create calculated columns</span></span>  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="d21e1-119">建立 hello DimDate 資料表中的 MonthCalendar 導出資料行</span><span class="sxs-lookup"><span data-stu-id="d21e1-119">Create a MonthCalendar calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="d21e1-120">按一下 hello**模型**功能表 >**模型檢視** > **資料檢視**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-120">Click hello **Model** menu > **Model View** > **Data View**.</span></span>  
  
    <span data-ttu-id="d21e1-121">導出資料行只可以建立使用資料檢視中的 hello 模型設計師。</span><span class="sxs-lookup"><span data-stu-id="d21e1-121">Calculated columns can only be created by using hello model designer in Data View.</span></span>  
  
2.  <span data-ttu-id="d21e1-122">在 hello 模型設計師中，按一下 hello **DimDate**資料表 （標籤）。</span><span class="sxs-lookup"><span data-stu-id="d21e1-122">In hello model designer, click hello **DimDate** table (tab).</span></span>  
  
3.  <span data-ttu-id="d21e1-123">以滑鼠右鍵按一下 hello **CalendarQuarter**資料行標頭，然後再按一下**插入資料行**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-123">Right-click hello **CalendarQuarter** column header, and then click **Insert Column**.</span></span>  
  
    <span data-ttu-id="d21e1-124">新的資料行名為**導出資料行 1**插入的 toohello 剩下的 hello**日曆季**資料行。</span><span class="sxs-lookup"><span data-stu-id="d21e1-124">A new column named **Calculated Column 1** is inserted toohello left of hello **Calendar Quarter** column.</span></span>  
  
4.  <span data-ttu-id="d21e1-125">在 hello hello 資料表上方的公式列中輸入下列 DAX 公式的 hello： 自動完成可協助您輸入 hello 完整限定的名稱的資料行和資料表，並列出 hello 可用函式。</span><span class="sxs-lookup"><span data-stu-id="d21e1-125">In hello formula bar above hello table, type hello following DAX formula: AutoComplete helps you type hello fully qualified names of columns and tables, and lists hello functions that are available.</span></span>  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    <span data-ttu-id="d21e1-126">Hello 導出資料行中的所有 hello 資料列就會都填入值。</span><span class="sxs-lookup"><span data-stu-id="d21e1-126">Values are then populated for all hello rows in hello calculated column.</span></span> <span data-ttu-id="d21e1-127">如果您向下捲動 hello 資料表，您會看到資料列可以有不同的值，這個資料行，根據每個資料列中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="d21e1-127">If you scroll down through hello table, you see rows can have different values for this column, based on hello data in each row.</span></span>    
  
5.  <span data-ttu-id="d21e1-128">重新命名此資料行太**MonthCalendar**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-128">Rename this column too**MonthCalendar**.</span></span> 

    ![aas 第 5 課新增資料行](../tutorials/media/aas-lesson5-newcolumn.png) 
  
<span data-ttu-id="d21e1-130">hello MonthCalendar 導出資料行會提供可排序月份名稱。</span><span class="sxs-lookup"><span data-stu-id="d21e1-130">hello MonthCalendar calculated column provides a sortable name for Month.</span></span>  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a><span data-ttu-id="d21e1-131">在 hello DimDate 資料表中建立 DayOfWeek 導出資料行</span><span class="sxs-lookup"><span data-stu-id="d21e1-131">Create a DayOfWeek calculated column in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="d21e1-132">以 hello **DimDate**資料表仍為使用中，按一下 hello**資料行**功能表，然後再按一下**加入資料行**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-132">With hello **DimDate** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="d21e1-133">Hello 公式列中輸入下列公式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d21e1-133">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    <span data-ttu-id="d21e1-134">當您完成建立 hello 公式時，請按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="d21e1-134">When you've finished building hello formula, press ENTER.</span></span> <span data-ttu-id="d21e1-135">toohello hello 資料表的最右邊加入 hello 新資料行。</span><span class="sxs-lookup"><span data-stu-id="d21e1-135">hello new column is added toohello far right of hello table.</span></span>  
  
3.  <span data-ttu-id="d21e1-136">Hello 資料行重新命名過**DayOfWeek**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-136">Rename hello column too**DayOfWeek**.</span></span>  
  
4.  <span data-ttu-id="d21e1-137">按一下 hello 欄標題，並拖曳 hello 資料行之間 hello **EnglishDayNameOfWeek**資料行和 hello **DayNumberOfMonth**資料行。</span><span class="sxs-lookup"><span data-stu-id="d21e1-137">Click hello column heading, and then drag hello column between hello **EnglishDayNameOfWeek** column and hello **DayNumberOfMonth** column.</span></span>  
  
    > [!TIP]  
    > <span data-ttu-id="d21e1-138">移動資料表中的資料行可讓您更輕鬆 toonavigate。</span><span class="sxs-lookup"><span data-stu-id="d21e1-138">Moving columns in your table makes it easier toonavigate.</span></span>  
  
<span data-ttu-id="d21e1-139">hello DayOfWeek 導出資料行提供可排序的 hello 週間日名稱。</span><span class="sxs-lookup"><span data-stu-id="d21e1-139">hello DayOfWeek calculated column provides a sortable name for hello day of week.</span></span>  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="d21e1-140">建立 hello DimProduct 資料表內的 ProductSubcategoryName 導出資料行</span><span class="sxs-lookup"><span data-stu-id="d21e1-140">Create a ProductSubcategoryName calculated column in hello DimProduct table</span></span>  
  
  
1.  <span data-ttu-id="d21e1-141">在 hello **DimProduct**資料表中，捲動 toohello hello 資料表的最右邊。</span><span class="sxs-lookup"><span data-stu-id="d21e1-141">In hello **DimProduct** table, scroll toohello far right of hello table.</span></span> <span data-ttu-id="d21e1-142">請注意 hello 最右側資料行名為**加入資料行**（斜體），請按一下 hello 資料行標題。</span><span class="sxs-lookup"><span data-stu-id="d21e1-142">Notice hello right-most column is named **Add Column** (italicized), click hello column heading.</span></span>  
  
2.  <span data-ttu-id="d21e1-143">Hello 公式列中輸入下列公式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d21e1-143">In hello formula bar, type hello following formula:</span></span>  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  <span data-ttu-id="d21e1-144">Hello 資料行重新命名過**ProductSubcategoryName**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-144">Rename hello column too**ProductSubcategoryName**.</span></span>  
  
<span data-ttu-id="d21e1-145">hello ProductSubcategoryName 導出資料行是使用的 toocreate hello DimProduct 資料表，其中包括 hello DimProductSubcategory 資料表中從 hello [englishproductsubcategoryname] 資料行的資料中的階層。</span><span class="sxs-lookup"><span data-stu-id="d21e1-145">hello ProductSubcategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductSubcategoryName column in hello DimProductSubcategory table.</span></span> <span data-ttu-id="d21e1-146">階層不可跨越多個資料表。</span><span class="sxs-lookup"><span data-stu-id="d21e1-146">Hierarchies cannot span more than one table.</span></span> <span data-ttu-id="d21e1-147">稍後您會在第 9 課中建立階層。</span><span class="sxs-lookup"><span data-stu-id="d21e1-147">You create hierarchies later in Lesson 9.</span></span>  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a><span data-ttu-id="d21e1-148">建立 hello DimProduct 資料表內的 ProductCategoryName 導出資料行</span><span class="sxs-lookup"><span data-stu-id="d21e1-148">Create a ProductCategoryName calculated column in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="d21e1-149">以 hello **DimProduct**資料表仍為使用中，按一下 hello**資料行**功能表，然後再按一下**加入資料行**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-149">With hello **DimProduct** table still active, click hello **Column** menu, and then click **Add Column**.</span></span>  
  
2.  <span data-ttu-id="d21e1-150">Hello 公式列中輸入下列公式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d21e1-150">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  <span data-ttu-id="d21e1-151">Hello 資料行重新命名過**ProductCategoryName**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-151">Rename hello column too**ProductCategoryName**.</span></span>  
  
<span data-ttu-id="d21e1-152">hello ProductCategoryName 導出資料行是使用的 toocreate hello DimProduct 資料表，其中包括 hello DimProductCategory 資料表中從 hello [englishproductcategoryname] 資料行的資料中的階層。</span><span class="sxs-lookup"><span data-stu-id="d21e1-152">hello ProductCategoryName calculated column is used toocreate a hierarchy in hello DimProduct table, which includes data from hello EnglishProductCategoryName column in hello DimProductCategory table.</span></span> <span data-ttu-id="d21e1-153">階層不可跨越多個資料表。</span><span class="sxs-lookup"><span data-stu-id="d21e1-153">Hierarchies cannot span more than one table.</span></span>  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a><span data-ttu-id="d21e1-154">在 hello FactInternetSales 資料表中建立 Margin 導出資料行</span><span class="sxs-lookup"><span data-stu-id="d21e1-154">Create a Margin calculated column in hello FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="d21e1-155">在 hello 模型設計師中，選取 hello **FactInternetSales**資料表。</span><span class="sxs-lookup"><span data-stu-id="d21e1-155">In hello model designer, select hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="d21e1-156">建立新的導出資料行之間 hello **SalesAmount**資料行和 hello **TaxAmt**資料行。</span><span class="sxs-lookup"><span data-stu-id="d21e1-156">Create a new calculated column between hello **SalesAmount** column and hello **TaxAmt** column.</span></span>  
  
3.  <span data-ttu-id="d21e1-157">Hello 公式列中輸入下列公式的 hello:</span><span class="sxs-lookup"><span data-stu-id="d21e1-157">In hello formula bar, type hello following formula:</span></span>  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  <span data-ttu-id="d21e1-158">Hello 資料行重新命名過**邊界**。</span><span class="sxs-lookup"><span data-stu-id="d21e1-158">Rename hello column too**Margin**.</span></span>  
 
      ![aas 第 5 課新增獲利率](../tutorials/media/aas-lesson5-newmargin.png)
      
    <span data-ttu-id="d21e1-160">hello Margin 導出資料行是每個銷售的使用的 tooanalyze 利率。</span><span class="sxs-lookup"><span data-stu-id="d21e1-160">hello Margin calculated column is used tooanalyze profit margins for each sale.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="d21e1-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d21e1-161">What's next?</span></span>
<span data-ttu-id="d21e1-162">[第 6 課：建立量值](../tutorials/aas-lesson-6-create-measures.md)。</span><span class="sxs-lookup"><span data-stu-id="d21e1-162">[Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>
  
  
  
