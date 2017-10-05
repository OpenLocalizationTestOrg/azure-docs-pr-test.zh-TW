---
title: "Azure Analysis Services 教學課程補充課程：詳細資料列 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程中建立詳細資料列運算式。"
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: fde5cd9a9efc3a13e731a91962ced5c086a72355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="079ae-103">補充課程 - 詳細資料列</span><span class="sxs-lookup"><span data-stu-id="079ae-103">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="079ae-104">在此補充課程中，您會使用 DAX 編輯器來定義自訂詳細資料列運算式。</span><span class="sxs-lookup"><span data-stu-id="079ae-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="079ae-105">詳細資料列運算式是一個量值屬性，可提供使用者有關量值彙總結果的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="079ae-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="079ae-106">這堂課的預估完成時間：**10 分鐘**</span><span class="sxs-lookup"><span data-stu-id="079ae-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="079ae-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="079ae-107">Prerequisites</span></span>  
<span data-ttu-id="079ae-108">此補充課程主題是表格式模型教學課程的一部分。</span><span class="sxs-lookup"><span data-stu-id="079ae-108">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="079ae-109">在此補充課程中執行工作之前，您應已完成所有先前的課程或已完成 Adventure Works 網際網路銷售範例模型專案。</span><span class="sxs-lookup"><span data-stu-id="079ae-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-to-solve"></a><span data-ttu-id="079ae-110">我們需要解決什麼？</span><span class="sxs-lookup"><span data-stu-id="079ae-110">What do we need to solve?</span></span>
<span data-ttu-id="079ae-111">讓我們先看看 InternetTotalSales 量值的詳細資料，再新增詳細資料列運算式。</span><span class="sxs-lookup"><span data-stu-id="079ae-111">Let's look at the details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="079ae-112">在 SSDT 中，按一下 [模型] 功能表 > [使用 Excel 分析] 以開啟 Excel 並建立空白的樞紐分析表。</span><span class="sxs-lookup"><span data-stu-id="079ae-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="079ae-113">在 [樞紐分析表欄位] 中，將 FactInternetSales 資料表中的 [InternetTotalSales] 量值新增至 [值]，將 DimDate 資料表中的 [CalendarYear] 新增至 [資料行]，以即將 [EnglishCountryRegionName] 新增至 [資料列]。</span><span class="sxs-lookup"><span data-stu-id="079ae-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="079ae-114">我們的樞紐分析表現在會依照區域和年度提供 InternetTotalSales 量值的彙總結果。</span><span class="sxs-lookup"><span data-stu-id="079ae-114">Our PivotTable now gives us aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="079ae-116">在樞紐分析表中，按兩下某個年度和區域名稱的彙總值。</span><span class="sxs-lookup"><span data-stu-id="079ae-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="079ae-117">我們在此按兩下澳洲 2014 年的值。</span><span class="sxs-lookup"><span data-stu-id="079ae-117">Here we double-clicked the value for Australia and the year 2014.</span></span> <span data-ttu-id="079ae-118">包含資料 (但非實用資料) 的新工作表隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="079ae-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="079ae-120">我們想要在此查看一個資料表，其中包含構成 InternetTotalSales 量值彙總結果的資料行和資料列。</span><span class="sxs-lookup"><span data-stu-id="079ae-120">What we would like to see here is a table containing columns and rows of data that contribute to the aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="079ae-121">若要這麼做，我們可以新增詳細資料列運算式做為量值的屬性。</span><span class="sxs-lookup"><span data-stu-id="079ae-121">To do that, we can add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="079ae-122">新增詳細資料列運算式</span><span class="sxs-lookup"><span data-stu-id="079ae-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="079ae-123">若要新增詳細資料列運算式</span><span class="sxs-lookup"><span data-stu-id="079ae-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="079ae-124">在 SSDT 中，於 FactInternetSales 資料表的量值方格中，按一下 [InternetTotalSales] 量值。</span><span class="sxs-lookup"><span data-stu-id="079ae-124">In SSDT, in the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="079ae-125">在 [屬性] > [詳細資料列運算式] 中，按一下編輯器按鈕以開啟 DAX 編輯器。</span><span class="sxs-lookup"><span data-stu-id="079ae-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="079ae-127">在 DAX 編輯器中，輸入下列運算式︰</span><span class="sxs-lookup"><span data-stu-id="079ae-127">In DAX Editor, enter the following expression:</span></span>

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

    <span data-ttu-id="079ae-128">此運算式可指定 FactInternetSales 資料表中的名稱、資料行和量值結果，而當使用者按兩下樞紐分析表或報告中的彙總結果時，就會傳回相關資料表。</span><span class="sxs-lookup"><span data-stu-id="079ae-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="079ae-129">回到 Excel，刪除在步驟 3 中建立的工作表，然後按兩下彙總值。</span><span class="sxs-lookup"><span data-stu-id="079ae-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="079ae-130">此時，使用針對量值定義的詳細資料列運算式屬性，包含許多實用資料的新工作表隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="079ae-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="079ae-132">重新部署您的模型。</span><span class="sxs-lookup"><span data-stu-id="079ae-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="079ae-133">另請參閱</span><span class="sxs-lookup"><span data-stu-id="079ae-133">See Also</span></span>  
<span data-ttu-id="079ae-134">[SELECTCOLUMNS 函式 (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="079ae-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="079ae-135">補充課程 - 動態安全性</span><span class="sxs-lookup"><span data-stu-id="079ae-135">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="079ae-136">補充課程 - 不完全階層</span><span class="sxs-lookup"><span data-stu-id="079ae-136">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
