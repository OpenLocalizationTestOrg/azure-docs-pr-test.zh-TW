---
<span data-ttu-id="d9c32-101">標題： aaa"Azure Analysis Services 教學課程的補充課程： 詳細資料列 |Microsoft 文件"描述： 描述如何 toocreate 詳細資料列運算式中的 hello Azure Analysis Services 教學課程。</span><span class="sxs-lookup"><span data-stu-id="d9c32-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="d9c32-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="d9c32-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="d9c32-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="d9c32-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="d9c32-104">補充課程 - 詳細資料列</span><span class="sxs-lookup"><span data-stu-id="d9c32-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="d9c32-105">在這個補充課程中，您使用 DAX 編輯器 toodefine hello 自訂的詳細資料列運算式。</span><span class="sxs-lookup"><span data-stu-id="d9c32-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="d9c32-106">詳細資料列運算式是量值，屬性提供使用者有關 hello 彙總結果的量值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d9c32-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="d9c32-107">本課程的估計時間 toocomplete: **10 分鐘**</span><span class="sxs-lookup"><span data-stu-id="d9c32-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d9c32-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="d9c32-108">Prerequisites</span></span>  
<span data-ttu-id="d9c32-109">此補充課程主題是表格式模型教學課程的一部分。</span><span class="sxs-lookup"><span data-stu-id="d9c32-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="d9c32-110">在執行前 hello 工作這個補充課程，您應已完成所有先前的課程或已完成的 Adventure Works Internet Sales 範例模型專案。</span><span class="sxs-lookup"><span data-stu-id="d9c32-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="d9c32-111">怎麼我們需要 toosolve？</span><span class="sxs-lookup"><span data-stu-id="d9c32-111">What do we need toosolve?</span></span>
<span data-ttu-id="d9c32-112">讓我們看看 hello 詳細資料，我們 InternetTotalSales 量值，然後再加入詳細資料列運算式。</span><span class="sxs-lookup"><span data-stu-id="d9c32-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="d9c32-113">在 SSDT 中，按一下 hello**模型**功能表 >**在 Excel 中的進行分析**tooopen Excel 並建立空白的樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="d9c32-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="d9c32-114">在**樞紐分析表欄位**，新增 hello **InternetTotalSales**太量值從 hello FactInternetSales 資料表**值**， **CalendarYear**從 hello DimDate 資料表太**資料行**，和**EnglishCountryRegionName**太**列**。</span><span class="sxs-lookup"><span data-stu-id="d9c32-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="d9c32-115">我們的樞紐分析表現在可讓我們彙總結果從依區域和年份的 hello InternetTotalSales 量值。</span><span class="sxs-lookup"><span data-stu-id="d9c32-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="d9c32-117">在 hello 樞紐分析表中，按兩下彙總值的年份和地區名稱。</span><span class="sxs-lookup"><span data-stu-id="d9c32-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="d9c32-118">這裡我們按兩下澳大利亞和 hello hello 值 2014 年。</span><span class="sxs-lookup"><span data-stu-id="d9c32-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="d9c32-119">包含資料 (但非實用資料) 的新工作表隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d9c32-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="d9c32-121">什麼我們想要 toosee 這裡是包含資料行和構成 toohello 彙總結果，我們 InternetTotalSales 量值的資料列的資料表。</span><span class="sxs-lookup"><span data-stu-id="d9c32-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="d9c32-122">toodo，我們可以加入詳細資料列運算式為 hello 量值的屬性。</span><span class="sxs-lookup"><span data-stu-id="d9c32-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="d9c32-123">新增詳細資料列運算式</span><span class="sxs-lookup"><span data-stu-id="d9c32-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="d9c32-124">toocreate 詳細資料列運算式</span><span class="sxs-lookup"><span data-stu-id="d9c32-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="d9c32-125">在 SSDT 中，在 hello FactInternetSales 資料表的量值方格中，按一下 hello **InternetTotalSales**量值。</span><span class="sxs-lookup"><span data-stu-id="d9c32-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="d9c32-126">在**屬性** > **詳細資料列運算式**，按一下 hello 編輯器按鈕 tooopen hello DAX 編輯器。</span><span class="sxs-lookup"><span data-stu-id="d9c32-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="d9c32-128">在 DAX 編輯器中，輸入下列運算式 hello:</span><span class="sxs-lookup"><span data-stu-id="d9c32-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="d9c32-129">這個運算式會指定名稱，資料行，以及當使用者按兩下彙總的結果在樞紐分析表或報表中會傳回從 hello FactInternetSales 資料表和相關的資料表的量值結果。</span><span class="sxs-lookup"><span data-stu-id="d9c32-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="d9c32-130">回在 Excel 中，刪除步驟 3 中建立的 hello 工作表，然後按兩下彙總的值。</span><span class="sxs-lookup"><span data-stu-id="d9c32-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="d9c32-131">這次 hello 量值定義的詳細資料列運算式內容，新的工作表會開啟包含更多有用的資料。</span><span class="sxs-lookup"><span data-stu-id="d9c32-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="d9c32-133">重新部署您的模型。</span><span class="sxs-lookup"><span data-stu-id="d9c32-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="d9c32-134">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d9c32-134">See Also</span></span>  
<span data-ttu-id="d9c32-135">[SELECTCOLUMNS 函式 (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="d9c32-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="d9c32-136">補充課程 - 動態安全性</span><span class="sxs-lookup"><span data-stu-id="d9c32-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="d9c32-137">補充課程 - 不完全階層</span><span class="sxs-lookup"><span data-stu-id="d9c32-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
