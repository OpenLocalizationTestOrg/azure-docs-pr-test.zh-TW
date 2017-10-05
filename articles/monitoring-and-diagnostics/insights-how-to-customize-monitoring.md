---
title: "Microsoft Azure 中的計量概觀 | Microsoft Docs"
description: "了解如何在 Azure 自訂監視圖表。"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 3f9ebb0f5737714dd685f0dcc1ff4b1c0c89528f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="f4b90-103">Microsoft Azure 中的計量概觀</span><span class="sxs-lookup"><span data-stu-id="f4b90-103">Overview of Metrics in Microsoft Azure</span></span>
<span data-ttu-id="f4b90-104">所有的 Azure 服務都會追蹤重要計量，可讓您監視服務的健全狀況、效能、可用性和使用情況。</span><span class="sxs-lookup"><span data-stu-id="f4b90-104">All Azure services track key metrics that allow you to monitor the health, performance, availability and usage of your services.</span></span> <span data-ttu-id="f4b90-105">您可以在 Azure 入口網站中檢視這些計量，而且您也可以使用 [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) 或 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) 以程式設計方式存取完整的計量集合。</span><span class="sxs-lookup"><span data-stu-id="f4b90-105">You can view these metrics in the Azure portal, and you can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to access the full set of metrics programmatically.</span></span>

<span data-ttu-id="f4b90-106">在某些服務中，您可能需要開啟診斷，才能查看任何計量。</span><span class="sxs-lookup"><span data-stu-id="f4b90-106">For some services, you may need to turn on diagnostics in order to see any metrics.</span></span> <span data-ttu-id="f4b90-107">在其他服務中 (例如虛擬機器)，您將會取得基本的計量集合，但需要啟用完整的高頻率計量集合。</span><span class="sxs-lookup"><span data-stu-id="f4b90-107">For others, such as virtual machines, you will get a basic set of metrics, but need to enable the full set high-frequency metrics.</span></span> <span data-ttu-id="f4b90-108">若要深入了解，請參閱 [啟用監視和診斷](insights-how-to-use-diagnostics.md) 。</span><span class="sxs-lookup"><span data-stu-id="f4b90-108">See [Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) to learn more.</span></span>

## <a name="using-monitoring-charts"></a><span data-ttu-id="f4b90-109">使用監視圖表</span><span class="sxs-lookup"><span data-stu-id="f4b90-109">Using monitoring charts</span></span>
<span data-ttu-id="f4b90-110">您可以製作任何選擇時間期間上的計量圖表。</span><span class="sxs-lookup"><span data-stu-id="f4b90-110">You can chart any of the metrics them over any time period you choose.</span></span>

1. <span data-ttu-id="f4b90-111">在 [Azure 入口網站](https://portal.azure.com/)中，按一下 [ **瀏覽**]，然後按一下您有興趣監視的資源。</span><span class="sxs-lookup"><span data-stu-id="f4b90-111">In the [Azure Portal](https://portal.azure.com/), click **Browse**, and then a resource you're interested in monitoring.</span></span>
2. <span data-ttu-id="f4b90-112">[ **監視** ] 區段中含有每個 Azure 資源最重要的計量。</span><span class="sxs-lookup"><span data-stu-id="f4b90-112">The **Monitoring** section contains the most important metrics for each Azure resource.</span></span> <span data-ttu-id="f4b90-113">例如，Web 應用程式具有**要求和錯誤**，而虛擬機器則具有 **CPU 百分比**和**磁碟讀取和寫入**：![監視透鏡](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)</span><span class="sxs-lookup"><span data-stu-id="f4b90-113">For example, a web app has **Requests and Errors**, where as a virtual machine would have **CPU percentage** and **Disk read and write**: ![Monitoring lens](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)</span></span>
3. <span data-ttu-id="f4b90-114">按一下任何一個圖表，即會顯示 [ **計量** ] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f4b90-114">Clicking on any chart will show you the **Metric** blade.</span></span> <span data-ttu-id="f4b90-115">在此刀鋒視窗上，除了一個圖形之外，還會有一個顯示這些計量彙總 (例如選擇時間範圍上的平均值、最小值和最大值) 的資料表。</span><span class="sxs-lookup"><span data-stu-id="f4b90-115">On the blade, in addition to the graph, is a table that shows you aggregations of the metrics (such as average, minimum and maximum, over the time range you chose).</span></span> <span data-ttu-id="f4b90-116">下面是資源的警示規則。</span><span class="sxs-lookup"><span data-stu-id="f4b90-116">Below that are the alert rules for the resource.</span></span>
    <span data-ttu-id="f4b90-117">![計量刀鋒視窗](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)</span><span class="sxs-lookup"><span data-stu-id="f4b90-117">![Metric blade](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)</span></span>
4. <span data-ttu-id="f4b90-118">若要自訂出現的資料行，請按一下圖表上的 [編輯] 按鈕，或按一下 [計量] 刀鋒視窗上的 [編輯圖表] 命令。</span><span class="sxs-lookup"><span data-stu-id="f4b90-118">To customize the lines that appear, click the **Edit** button on the chart, or, the **Edit chart** command on the Metric blade.</span></span>
5. <span data-ttu-id="f4b90-119">在 [編輯查詢] 刀鋒視窗上，您可以執行三個動作：</span><span class="sxs-lookup"><span data-stu-id="f4b90-119">On the Edit Query blade you can do three things:</span></span>
   
   * <span data-ttu-id="f4b90-120">變更時間範圍</span><span class="sxs-lookup"><span data-stu-id="f4b90-120">Change the time range</span></span>
   * <span data-ttu-id="f4b90-121">在長條圖與折線圖之間切換外觀</span><span class="sxs-lookup"><span data-stu-id="f4b90-121">Switch the appearance between Bar and Line</span></span>
   * <span data-ttu-id="f4b90-122">選擇不同的計量 ![編輯查詢](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)</span><span class="sxs-lookup"><span data-stu-id="f4b90-122">Choose different metics ![Edit Query](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)</span></span>
6. <span data-ttu-id="f4b90-123">變更時間範圍十分容易，只要選取不同的範圍 (例如 [Past Hour]，再按一下刀鋒視窗底部的 [儲存] 即可。</span><span class="sxs-lookup"><span data-stu-id="f4b90-123">Changing the time range is as easy as selecting a different range (such as **Past Hour**) and clicking **Save** at the bottom of the blade.</span></span> <span data-ttu-id="f4b90-124">您也可以選擇 [自訂]，這可讓您選擇過去 2 週的任何一段時間。</span><span class="sxs-lookup"><span data-stu-id="f4b90-124">You can also choose **Custom**, which allows you to choose any period of time over the past 2 weeks.</span></span> <span data-ttu-id="f4b90-125">例如，您可以完整檢視這兩週，或僅檢視昨天的某 1 小時。</span><span class="sxs-lookup"><span data-stu-id="f4b90-125">For example, you can see the whole two weeks, or, just 1 hour from yesterday.</span></span> <span data-ttu-id="f4b90-126">請在文字方塊中輸入不同的小時。</span><span class="sxs-lookup"><span data-stu-id="f4b90-126">Type in the text box to enter a different hour.</span></span>
    <span data-ttu-id="f4b90-127">![自訂時間範圍](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)</span><span class="sxs-lookup"><span data-stu-id="f4b90-127">![Custom time range](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)</span></span>
7. <span data-ttu-id="f4b90-128">在時間範圍下，您可以選擇任何要顯示在圖表上的度量數。</span><span class="sxs-lookup"><span data-stu-id="f4b90-128">Below the time range, you chan choose any number of metrics to show on the chart.</span></span>
8. <span data-ttu-id="f4b90-129">當您按一下 [儲存] 時，系統便會儲存為該特定資源所做的變更。</span><span class="sxs-lookup"><span data-stu-id="f4b90-129">When you click Save your changes will be saved for that particular resource.</span></span> <span data-ttu-id="f4b90-130">例如，如果您有兩部虛擬機器，若變更其中一部虛擬機器的圖表，它將不會影響到另一部虛擬機器的圖表。</span><span class="sxs-lookup"><span data-stu-id="f4b90-130">For example, if you have two virtual machines, and you change a chart on one, it will not impact the other.</span></span>

## <a name="creating-side-by-side-charts"></a><span data-ttu-id="f4b90-131">建立並排圖表</span><span class="sxs-lookup"><span data-stu-id="f4b90-131">Creating side-by-side charts</span></span>
<span data-ttu-id="f4b90-132">使用入口網站中的強大自訂功能，您可以新增任意數目的圖表。</span><span class="sxs-lookup"><span data-stu-id="f4b90-132">With the powerful customization in the portal you can add as many charts as you want.</span></span>

1. <span data-ttu-id="f4b90-133">在刀鋒視窗頂端的 [...] 功能表中，按一下 [新增圖格]：</span><span class="sxs-lookup"><span data-stu-id="f4b90-133">In the **...** menu at the top of the blade click **Add tiles**:</span></span>  
    <span data-ttu-id="f4b90-134">![新增功能表](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)</span><span class="sxs-lookup"><span data-stu-id="f4b90-134">![Add Menu](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)</span></span>
2. <span data-ttu-id="f4b90-135">然後，您可以從右側螢幕上的 [資源庫] 中選取圖表：![資源庫](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)</span><span class="sxs-lookup"><span data-stu-id="f4b90-135">Then, you can select select a chart from the **Gallery** on the right side of your screen:  ![Gallery](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)</span></span>
3. <span data-ttu-id="f4b90-136">如果您沒有看到所需的計量，您可以隨時新增其中一個預設計量，並 **編輯** 圖表以顯示所需的計量。</span><span class="sxs-lookup"><span data-stu-id="f4b90-136">If you don't see the metric you want, you can always add one of the preset metrics, and **Edit** the chart to show the metric that you need.</span></span>

## <a name="monitoring-usage-quotas"></a><span data-ttu-id="f4b90-137">監視使用量配額</span><span class="sxs-lookup"><span data-stu-id="f4b90-137">Monitoring usage quotas</span></span>
<span data-ttu-id="f4b90-138">大部分的計量會顯示某一段時間的趨勢，但是某些特定資料 (如使用量配額) 則會是包含臨界值的時間點資訊。</span><span class="sxs-lookup"><span data-stu-id="f4b90-138">Most metrics show you trends over time, but certain data, like usage quotas, are point-in-time information with a threshold.</span></span>

<span data-ttu-id="f4b90-139">您也可以在刀鋒視窗上查看具有配額之資源的使用量配額：</span><span class="sxs-lookup"><span data-stu-id="f4b90-139">You can also see usage quotas on the blade for resources that have quotas:</span></span>

![使用量](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

<span data-ttu-id="f4b90-141">和計量一樣，您可以使用 [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) 或 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) 以程式設計方式存取完整的使用量配額集合。</span><span class="sxs-lookup"><span data-stu-id="f4b90-141">Like with metrics, you can use the [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) to access the full set of usage quotas programmatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4b90-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4b90-142">Next steps</span></span>
* <span data-ttu-id="f4b90-143">[接收警示通知](insights-receive-alert-notifications.md) 。</span><span class="sxs-lookup"><span data-stu-id="f4b90-143">[Receive alert notifications](insights-receive-alert-notifications.md) whenever a metric crosses a threshold.</span></span>
* <span data-ttu-id="f4b90-144">[啟用監視和診斷](insights-how-to-use-diagnostics.md) 來在您服務中收集詳細的高頻率計量。</span><span class="sxs-lookup"><span data-stu-id="f4b90-144">[Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) to collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="f4b90-145">[自動調整執行個體計數](insights-how-to-scale.md) 以確保您的服務可用且可迅速回應。</span><span class="sxs-lookup"><span data-stu-id="f4b90-145">[Scale instance count automatically](insights-how-to-scale.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="f4b90-146">[監視應用程式效能](../application-insights/app-insights-azure-web-apps.md) 。</span><span class="sxs-lookup"><span data-stu-id="f4b90-146">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want to understand exactly how your code is performing in the cloud.</span></span>
* <span data-ttu-id="f4b90-147">使用 [JavaScript 應用程式和網頁適用的 Application Insights](../application-insights/app-insights-web-track-usage.md) ，以取得有關造訪網頁瀏覽器的用戶端分析。</span><span class="sxs-lookup"><span data-stu-id="f4b90-147">Use [Application Insights for JavaScript apps and web pages](../application-insights/app-insights-web-track-usage.md) to get client analytics about the browsers that visit a web page.</span></span>
* <span data-ttu-id="f4b90-148">[監視任何網頁的可用性和回應性](../application-insights/app-insights-monitor-web-app-availability.md) ，讓您可以找出您的頁面是否關閉。</span><span class="sxs-lookup"><span data-stu-id="f4b90-148">[Monitor availability and responsiveness of any web page](../application-insights/app-insights-monitor-web-app-availability.md) with Application Insights so you can find out if your page is down.</span></span>

