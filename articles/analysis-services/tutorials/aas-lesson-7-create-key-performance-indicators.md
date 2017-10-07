---
<span data-ttu-id="f30d4-101">標題： aaa"Azure Analysis Services 教學課程第 7 課： 建立關鍵效能指標 |Microsoft 文件"描述： 描述如何在 toocreate 關鍵效能指標 hello Azure Analysis Services 教學課程專案。</span><span class="sxs-lookup"><span data-stu-id="f30d4-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="f30d4-102">服務： analysis services documentationcenter: '作者： minewiskan 管理員： erikre 編輯器:' 標記: '</span><span class="sxs-lookup"><span data-stu-id="f30d4-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="f30d4-103">ms.assetid: ms.service: analysis services ms.devlang: NA ms.topic: get 啟動文章 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="f30d4-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="f30d4-104">第 7 課：建立關鍵效能指標</span><span class="sxs-lookup"><span data-stu-id="f30d4-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="f30d4-105">在這堂課中，您可以建立關鍵效能指標 (KPI)。</span><span class="sxs-lookup"><span data-stu-id="f30d4-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="f30d4-106">Kpi 是所定義的值使用的 toogauge 效能*基底*量值，針對*目標*由量值或絕對值定義的值。</span><span class="sxs-lookup"><span data-stu-id="f30d4-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="f30d4-107">在報表用戶端應用程式中，Kpi 可以商務專業人士提供快速簡便方式 toounderstand 商務成功或 tooidentify 趨勢的摘要。</span><span class="sxs-lookup"><span data-stu-id="f30d4-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="f30d4-108">詳細資訊，請參閱 toolearn [Kpi](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="f30d4-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="f30d4-109">本課程的估計時間 toocomplete: **15 分鐘**</span><span class="sxs-lookup"><span data-stu-id="f30d4-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="f30d4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f30d4-110">Prerequisites</span></span>  
<span data-ttu-id="f30d4-111">本主題是表格式模型教學課程的一部分，請依序完成。</span><span class="sxs-lookup"><span data-stu-id="f30d4-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="f30d4-112">在執行之前 hello 工作在這一課，您應已完成上一課 hello:[第 6 課： 建立量值](../tutorials/aas-lesson-6-create-measures.md)。</span><span class="sxs-lookup"><span data-stu-id="f30d4-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="f30d4-113">建立關鍵效能指標</span><span class="sxs-lookup"><span data-stu-id="f30d4-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="f30d4-114">toocreate InternetCurrentQuarterSalesPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="f30d4-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="f30d4-115">在 hello 模型設計師中，按一下 hello **FactInternetSales**資料表。</span><span class="sxs-lookup"><span data-stu-id="f30d4-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="f30d4-116">在 hello 量值方格中，按一下空白儲存格。</span><span class="sxs-lookup"><span data-stu-id="f30d4-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="f30d4-117">在 hello 上方公式列 hello 資料表中，輸入下列公式的 hello:</span><span class="sxs-lookup"><span data-stu-id="f30d4-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="f30d4-118">此量值做為 hello hello KPI 的基底量值。</span><span class="sxs-lookup"><span data-stu-id="f30d4-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="f30d4-119">以滑鼠右鍵按一下 [InternetCurrentQuarterSalesPerformance] > [建立 KPI]。</span><span class="sxs-lookup"><span data-stu-id="f30d4-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="f30d4-120">在 hello 關鍵效能指標 (KPI) 對話方塊中，在**目標**選取**絕對值**，然後輸入**1.1**。</span><span class="sxs-lookup"><span data-stu-id="f30d4-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="f30d4-121">在 [hello] 左側 （下） 滑動軸欄位中，輸入**1**，然後在 hello 右側 （上） 滑動軸欄位中，輸入**1.07**。</span><span class="sxs-lookup"><span data-stu-id="f30d4-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="f30d4-122">在**選取圖示樣式**、 選取 hello 菱形 （紅色）、 三角形 （黃色）、 圓形 （綠色） 圖示類型。</span><span class="sxs-lookup"><span data-stu-id="f30d4-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="f30d4-124">請注意 hello 可展開**描述**hello 可用圖示樣式下方的標籤。</span><span class="sxs-lookup"><span data-stu-id="f30d4-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="f30d4-125">描述用於 hello 各種 KPI 元素 toomake 它們更容易識別用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f30d4-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="f30d4-126">按一下**確定**toocomplete hello KPI。</span><span class="sxs-lookup"><span data-stu-id="f30d4-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="f30d4-127">在 hello 量值方格中，請注意 hello 圖示下一步 toohello **InternetCurrentQuarterSalesPerformance**量值。</span><span class="sxs-lookup"><span data-stu-id="f30d4-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="f30d4-128">這個圖示表示此量值做為 KPI 的基準值。</span><span class="sxs-lookup"><span data-stu-id="f30d4-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="f30d4-129">toocreate InternetCurrentQuarterMarginPerformance KPI</span><span class="sxs-lookup"><span data-stu-id="f30d4-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="f30d4-130">在 hello 量值方格中的 hello **FactInternetSales**資料表中，按一下空白儲存格。</span><span class="sxs-lookup"><span data-stu-id="f30d4-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="f30d4-131">在 hello 上方公式列 hello 資料表中，輸入下列公式的 hello:</span><span class="sxs-lookup"><span data-stu-id="f30d4-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="f30d4-132">以滑鼠右鍵按一下 [InternetCurrentQuarterMarginPerformance] > [建立 KPI]。</span><span class="sxs-lookup"><span data-stu-id="f30d4-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="f30d4-133">在 hello 關鍵效能指標 (KPI) 對話方塊中，在**目標**選取**絕對值**，然後輸入**1.25**。</span><span class="sxs-lookup"><span data-stu-id="f30d4-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="f30d4-134">在 hello 左側 （下） 滑動軸欄位中，投影片直到 hello 欄位會顯示**0.8**，然後投影片 hello 在直到 hello 欄位會顯示，以滑鼠右鍵 （高） 滑動軸欄位，和**1.03**。</span><span class="sxs-lookup"><span data-stu-id="f30d4-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="f30d4-135">在**選取圖示樣式**hello 菱形 （紅色）、 三角形 （黃色）、 圓形 （綠色） 圖示類型，選取，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="f30d4-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="f30d4-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f30d4-136">What's next?</span></span>
<span data-ttu-id="f30d4-137">[第 8 課：建立檢視方塊](../tutorials/aas-lesson-8-create-perspectives.md)。</span><span class="sxs-lookup"><span data-stu-id="f30d4-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
