---
title: "Azure Analysis Services 教學課程第 7 課︰建立關鍵效能指標 | Microsoft Docs"
description: "說明如何在 Azure Analysis Services 教學課程專案中建立關鍵效能指標。"
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
ms.openlocfilehash: d78808421dd5acd907aa9e9000bb3b770a42c061
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="d3c12-103">第 7 課：建立關鍵效能指標</span><span class="sxs-lookup"><span data-stu-id="d3c12-103">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="d3c12-104">在這堂課中，您可以建立關鍵效能指標 (KPI)。</span><span class="sxs-lookup"><span data-stu-id="d3c12-104">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="d3c12-105">根據由量值或絕對值所定義的「目標」值，KPI 用來測量「基準」量值所定義的值效能。</span><span class="sxs-lookup"><span data-stu-id="d3c12-105">KPIs are used to gauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="d3c12-106">在報告用戶端應用程式中，KPI 可讓商務專業人士輕鬆、快速地概括了解商務成果或找出趨勢。</span><span class="sxs-lookup"><span data-stu-id="d3c12-106">In reporting client applications, KPIs can provide business professionals a quick and easy way to understand a summary of business success or to identify trends.</span></span> <span data-ttu-id="d3c12-107">若要深入了解，請參閱 [KPI](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="d3c12-107">To learn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="d3c12-108">這堂課的預估完成時間：**15 分鐘**</span><span class="sxs-lookup"><span data-stu-id="d3c12-108">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="d3c12-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="d3c12-109">Prerequisites</span></span>  
<span data-ttu-id="d3c12-110">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="d3c12-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="d3c12-111">在這堂課中執行工作之前，您必須已完成上一堂課︰[第 6 課︰建立量值](../tutorials/aas-lesson-6-create-measures.md)。</span><span class="sxs-lookup"><span data-stu-id="d3c12-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="d3c12-112">建立關鍵效能指標</span><span class="sxs-lookup"><span data-stu-id="d3c12-112">Create Key Performance Indicators</span></span>  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="d3c12-113">若要建立 InternetCurrentQuarterSalesPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="d3c12-113">To create an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="d3c12-114">在模型設計工具中，按一下 **FactInternetSales** 資料表。</span><span class="sxs-lookup"><span data-stu-id="d3c12-114">In the model designer, click the **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="d3c12-115">在量值方格中，按一下空的儲存格。</span><span class="sxs-lookup"><span data-stu-id="d3c12-115">In the measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="d3c12-116">在資料表上方的公式列中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="d3c12-116">In the formula bar, above the table, type the following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="d3c12-117">此量值作為 KPI 的基準量值。</span><span class="sxs-lookup"><span data-stu-id="d3c12-117">This measure serves as the Base measure for the KPI.</span></span>  
  
4.  <span data-ttu-id="d3c12-118">以滑鼠右鍵按一下 [InternetCurrentQuarterSalesPerformance] > [建立 KPI]。</span><span class="sxs-lookup"><span data-stu-id="d3c12-118">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="d3c12-119">在 [關鍵效能指標 (KPI)] 對話方塊中，於 [目標] 中選取 [絕對值]，然後輸入 **1.1**。</span><span class="sxs-lookup"><span data-stu-id="d3c12-119">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="d3c12-120">在左側 (低) 滑桿欄位中，輸入 **1**，然後在右側 (高) 滑桿欄位中，輸入 **1.07**。</span><span class="sxs-lookup"><span data-stu-id="d3c12-120">In the left (low) slider field, type **1**, and then in the right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="d3c12-121">在 [選取圖示樣式] 中，選取菱形 (紅色)、三角形 (黃色)、圓形 (綠色) 圖示類型。</span><span class="sxs-lookup"><span data-stu-id="d3c12-121">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="d3c12-123">請注意，可用圖示樣式下方的可展開 [描述] 標籤。</span><span class="sxs-lookup"><span data-stu-id="d3c12-123">Notice the expandable **Descriptions** label below the available icon styles.</span></span> <span data-ttu-id="d3c12-124">使用各種 KPI 元素的描述，使其更容易在用戶端應用程式中識別。</span><span class="sxs-lookup"><span data-stu-id="d3c12-124">Use descriptions for the various KPI elements to make them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="d3c12-125">按一下 [確定]  來完成 KPI。</span><span class="sxs-lookup"><span data-stu-id="d3c12-125">Click **OK** to complete the KPI.</span></span>  
  
    <span data-ttu-id="d3c12-126">在量值方格中，請注意 [InternetCurrentQuarterSalesPerformance] 量值旁邊的圖示。</span><span class="sxs-lookup"><span data-stu-id="d3c12-126">In the measure grid, notice the icon next to the **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="d3c12-127">這個圖示表示此量值做為 KPI 的基準值。</span><span class="sxs-lookup"><span data-stu-id="d3c12-127">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="d3c12-128">若要建立 InternetCurrentQuarterMarginPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="d3c12-128">To create an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="d3c12-129">在 **FactInternetSales** 資料表的量值方格中，按一下空的儲存格。</span><span class="sxs-lookup"><span data-stu-id="d3c12-129">In the measure grid for the **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="d3c12-130">在資料表上方的公式列中，輸入下列公式︰</span><span class="sxs-lookup"><span data-stu-id="d3c12-130">In the formula bar, above the table, type the following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="d3c12-131">以滑鼠右鍵按一下 [InternetCurrentQuarterMarginPerformance] > [建立 KPI]。</span><span class="sxs-lookup"><span data-stu-id="d3c12-131">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="d3c12-132">在 [關鍵效能指標 (KPI)] 對話方塊中，於 [目標] 中選取 [絕對值]，然後輸入 **1.25**。</span><span class="sxs-lookup"><span data-stu-id="d3c12-132">In the Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="d3c12-133">在左側 (低) 滑桿欄位中，滑動直到欄位顯示 **0.8** 為止，然後滑動右側 (高) 滑桿欄位，直到欄位顯示 **1.03** 為止。</span><span class="sxs-lookup"><span data-stu-id="d3c12-133">In the left (low) slider field, slide until the field displays **0.8**, and then slide the right (high) slider field, until the field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="d3c12-134">在 [選取圖示樣式] 中，選取菱形 (紅色)、三角形 (黃色)、圓形 (綠色) 圖示類型，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d3c12-134">In **Select Icon Style**, select the diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="d3c12-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3c12-135">What's next?</span></span>
<span data-ttu-id="d3c12-136">[第 8 課：建立檢視方塊](../tutorials/aas-lesson-8-create-perspectives.md)。</span><span class="sxs-lookup"><span data-stu-id="d3c12-136">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
