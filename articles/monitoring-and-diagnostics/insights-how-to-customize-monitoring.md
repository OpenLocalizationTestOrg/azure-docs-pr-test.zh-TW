---
title: "在 Microsoft Azure 中的度量的 aaaOverview |Microsoft 文件"
description: "了解如何監視 toocustomize 圖表顯示在 Azure 中。"
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
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a><span data-ttu-id="f5149-103">Microsoft Azure 中的計量概觀</span><span class="sxs-lookup"><span data-stu-id="f5149-103">Overview of Metrics in Microsoft Azure</span></span>
<span data-ttu-id="f5149-104">所有 Azure 服務，來追蹤 toomonitor hello 健全狀況、 效能、 可用性和使用方式，您的服務可讓您的關鍵計量。</span><span class="sxs-lookup"><span data-stu-id="f5149-104">All Azure services track key metrics that allow you toomonitor hello health, performance, availability and usage of your services.</span></span> <span data-ttu-id="f5149-105">您可以在 hello Azure 入口網站中檢視這些度量資訊，而且您也可以使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx)或[.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello 組完整的度量以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="f5149-105">You can view these metrics in hello Azure portal, and you can also use hello [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello full set of metrics programmatically.</span></span>

<span data-ttu-id="f5149-106">某些服務，您可能需要的任何度量 tooturn toosee 順序中的診斷。</span><span class="sxs-lookup"><span data-stu-id="f5149-106">For some services, you may need tooturn on diagnostics in order toosee any metrics.</span></span> <span data-ttu-id="f5149-107">對於其他人使用，例如虛擬機器，您會收到一組基本度量，但需要 tooenable hello 完整集頻率高的度量。</span><span class="sxs-lookup"><span data-stu-id="f5149-107">For others, such as virtual machines, you will get a basic set of metrics, but need tooenable hello full set high-frequency metrics.</span></span> <span data-ttu-id="f5149-108">請參閱[啟用監視和診斷](insights-how-to-use-diagnostics.md)toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="f5149-108">See [Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) toolearn more.</span></span>

## <a name="using-monitoring-charts"></a><span data-ttu-id="f5149-109">使用監視圖表</span><span class="sxs-lookup"><span data-stu-id="f5149-109">Using monitoring charts</span></span>
<span data-ttu-id="f5149-110">您可以將任何 hello 計量圖表需要將任何您選擇的時間週期內。</span><span class="sxs-lookup"><span data-stu-id="f5149-110">You can chart any of hello metrics them over any time period you choose.</span></span>

1. <span data-ttu-id="f5149-111">在 [hello [Azure 入口網站](https://portal.azure.com/)，按一下**瀏覽**，然後資源您感興趣監視。</span><span class="sxs-lookup"><span data-stu-id="f5149-111">In hello [Azure Portal](https://portal.azure.com/), click **Browse**, and then a resource you're interested in monitoring.</span></span>
2. <span data-ttu-id="f5149-112">hello**監視**章節包含的每個 Azure 資源 hello 最重要的指標。</span><span class="sxs-lookup"><span data-stu-id="f5149-112">hello **Monitoring** section contains hello most important metrics for each Azure resource.</span></span> <span data-ttu-id="f5149-113">例如，Web 應用程式具有**要求和錯誤**，而虛擬機器則具有 **CPU 百分比**和**磁碟讀取和寫入**：![監視透鏡](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)</span><span class="sxs-lookup"><span data-stu-id="f5149-113">For example, a web app has **Requests and Errors**, where as a virtual machine would have **CPU percentage** and **Disk read and write**: ![Monitoring lens](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)</span></span>
3. <span data-ttu-id="f5149-114">按一下任何圖上，會顯示您 hello**度量**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f5149-114">Clicking on any chart will show you hello **Metric** blade.</span></span> <span data-ttu-id="f5149-115">Hello 刀鋒視窗中，此外 toohello 圖形是顯示 hello 度量 （例如平均值、 最小和最大，您所選擇的 hello 時間範圍內） 的彙總的資料表。</span><span class="sxs-lookup"><span data-stu-id="f5149-115">On hello blade, in addition toohello graph, is a table that shows you aggregations of hello metrics (such as average, minimum and maximum, over hello time range you chose).</span></span> <span data-ttu-id="f5149-116">請在下方是 hello hello 資源的警示規則。</span><span class="sxs-lookup"><span data-stu-id="f5149-116">Below that are hello alert rules for hello resource.</span></span>
    <span data-ttu-id="f5149-117">![計量刀鋒視窗](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)</span><span class="sxs-lookup"><span data-stu-id="f5149-117">![Metric blade](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)</span></span>
4. <span data-ttu-id="f5149-118">toocustomize hello 行出現之後，按一下 hello**編輯**hello 圖表上的按鈕，或 hello**編輯圖表**hello 計量刀鋒伺服器上的命令。</span><span class="sxs-lookup"><span data-stu-id="f5149-118">toocustomize hello lines that appear, click hello **Edit** button on hello chart, or, hello **Edit chart** command on hello Metric blade.</span></span>
5. <span data-ttu-id="f5149-119">Hello 編輯查詢] 刀鋒視窗中，您可以執行三件事：</span><span class="sxs-lookup"><span data-stu-id="f5149-119">On hello Edit Query blade you can do three things:</span></span>
   
   * <span data-ttu-id="f5149-120">變更 hello 時間範圍</span><span class="sxs-lookup"><span data-stu-id="f5149-120">Change hello time range</span></span>
   * <span data-ttu-id="f5149-121">切換 hello 外觀之間列和行</span><span class="sxs-lookup"><span data-stu-id="f5149-121">Switch hello appearance between Bar and Line</span></span>
   * <span data-ttu-id="f5149-122">選擇不同的計量 ![編輯查詢](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)</span><span class="sxs-lookup"><span data-stu-id="f5149-122">Choose different metics ![Edit Query](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)</span></span>
6. <span data-ttu-id="f5149-123">變更 hello 時間範圍非常簡單，只要選取不同的範圍 (例如**過去一小時**)，然後按一下**儲存**在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="f5149-123">Changing hello time range is as easy as selecting a different range (such as **Past Hour**) and clicking **Save** at hello bottom of hello blade.</span></span> <span data-ttu-id="f5149-124">您也可以選擇**自訂**，可讓您 toochoose 任何時段透過 hello 過去 2 週。</span><span class="sxs-lookup"><span data-stu-id="f5149-124">You can also choose **Custom**, which allows you toochoose any period of time over hello past 2 weeks.</span></span> <span data-ttu-id="f5149-125">例如，您可以看到 hello 整個兩週，或只昨天 1 小時內。</span><span class="sxs-lookup"><span data-stu-id="f5149-125">For example, you can see hello whole two weeks, or, just 1 hour from yesterday.</span></span> <span data-ttu-id="f5149-126">輸入 hello 文字方塊 tooenter 中不同的小時。</span><span class="sxs-lookup"><span data-stu-id="f5149-126">Type in hello text box tooenter a different hour.</span></span>
    <span data-ttu-id="f5149-127">![自訂時間範圍](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)</span><span class="sxs-lookup"><span data-stu-id="f5149-127">![Custom time range](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)</span></span>
7. <span data-ttu-id="f5149-128">以下 hello 時間範圍，您將會選擇任意數目的度量 tooshow hello 圖表上。</span><span class="sxs-lookup"><span data-stu-id="f5149-128">Below hello time range, you chan choose any number of metrics tooshow on hello chart.</span></span>
8. <span data-ttu-id="f5149-129">當您按一下 [儲存] 時，系統便會儲存為該特定資源所做的變更。</span><span class="sxs-lookup"><span data-stu-id="f5149-129">When you click Save your changes will be saved for that particular resource.</span></span> <span data-ttu-id="f5149-130">例如，如果您有兩個虛擬機器，而且您變更其中一個圖表，它不會影響其他 hello。</span><span class="sxs-lookup"><span data-stu-id="f5149-130">For example, if you have two virtual machines, and you change a chart on one, it will not impact hello other.</span></span>

## <a name="creating-side-by-side-charts"></a><span data-ttu-id="f5149-131">建立並排圖表</span><span class="sxs-lookup"><span data-stu-id="f5149-131">Creating side-by-side charts</span></span>
<span data-ttu-id="f5149-132">與 hello hello 入口網站中功能強大的自訂，您可以新增您想要的許多圖表。</span><span class="sxs-lookup"><span data-stu-id="f5149-132">With hello powerful customization in hello portal you can add as many charts as you want.</span></span>

1. <span data-ttu-id="f5149-133">在 [hello **...**功能表頂端的 hello 刀鋒視窗中按一下 hello**新增磚**:</span><span class="sxs-lookup"><span data-stu-id="f5149-133">In hello **...** menu at hello top of hello blade click **Add tiles**:</span></span>  
    <span data-ttu-id="f5149-134">![新增功能表](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)</span><span class="sxs-lookup"><span data-stu-id="f5149-134">![Add Menu](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)</span></span>
2. <span data-ttu-id="f5149-135">然後，您可以選取 [選取圖表從 hello**圖庫**螢幕 hello 右側：![組件庫](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)</span><span class="sxs-lookup"><span data-stu-id="f5149-135">Then, you can select select a chart from hello **Gallery** on hello right side of your screen:  ![Gallery](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)</span></span>
3. <span data-ttu-id="f5149-136">如果您沒有看到您想要的 hello 度量，您可以新增的其中一個 hello 預先設定的度量，和**編輯**hello 您需要的圖表 tooshow hello 度量。</span><span class="sxs-lookup"><span data-stu-id="f5149-136">If you don't see hello metric you want, you can always add one of hello preset metrics, and **Edit** hello chart tooshow hello metric that you need.</span></span>

## <a name="monitoring-usage-quotas"></a><span data-ttu-id="f5149-137">監視使用量配額</span><span class="sxs-lookup"><span data-stu-id="f5149-137">Monitoring usage quotas</span></span>
<span data-ttu-id="f5149-138">大部分的計量會顯示某一段時間的趨勢，但是某些特定資料 (如使用量配額) 則會是包含臨界值的時間點資訊。</span><span class="sxs-lookup"><span data-stu-id="f5149-138">Most metrics show you trends over time, but certain data, like usage quotas, are point-in-time information with a threshold.</span></span>

<span data-ttu-id="f5149-139">您也可以看到 hello 刀鋒視窗中有配額的資源使用量配額：</span><span class="sxs-lookup"><span data-stu-id="f5149-139">You can also see usage quotas on hello blade for resources that have quotas:</span></span>

![使用量](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

<span data-ttu-id="f5149-141">像度量，您可以使用 hello [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx)或[.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello 整組使用量配額以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="f5149-141">Like with metrics, you can use hello [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) or [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello full set of usage quotas programmatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5149-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f5149-142">Next steps</span></span>
* <span data-ttu-id="f5149-143">[接收警示通知](insights-receive-alert-notifications.md) 。</span><span class="sxs-lookup"><span data-stu-id="f5149-143">[Receive alert notifications](insights-receive-alert-notifications.md) whenever a metric crosses a threshold.</span></span>
* <span data-ttu-id="f5149-144">[啟用監視和診斷](insights-how-to-use-diagnostics.md)toocollect 詳細高頻率度量，您的服務。</span><span class="sxs-lookup"><span data-stu-id="f5149-144">[Enable monitoring and diagnostics](insights-how-to-use-diagnostics.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="f5149-145">[自動調整執行個體計數](insights-how-to-scale.md)toomake 確定您的服務可用，並能繼續回應。</span><span class="sxs-lookup"><span data-stu-id="f5149-145">[Scale instance count automatically](insights-how-to-scale.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="f5149-146">[監視應用程式效能](../application-insights/app-insights-azure-web-apps.md)如果您想 toounderstand 完全如何您的程式碼執行 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="f5149-146">[Monitor application performance](../application-insights/app-insights-azure-web-apps.md) if you want toounderstand exactly how your code is performing in hello cloud.</span></span>
* <span data-ttu-id="f5149-147">使用[Application Insights for JavaScript 應用程式及網頁](../application-insights/app-insights-web-track-usage.md)tooget 用戶端分析有關 hello 瀏覽器瀏覽網頁。</span><span class="sxs-lookup"><span data-stu-id="f5149-147">Use [Application Insights for JavaScript apps and web pages](../application-insights/app-insights-web-track-usage.md) tooget client analytics about hello browsers that visit a web page.</span></span>
* <span data-ttu-id="f5149-148">[監視任何網頁的可用性和回應性](../application-insights/app-insights-monitor-web-app-availability.md) ，讓您可以找出您的頁面是否關閉。</span><span class="sxs-lookup"><span data-stu-id="f5149-148">[Monitor availability and responsiveness of any web page](../application-insights/app-insights-monitor-web-app-availability.md) with Application Insights so you can find out if your page is down.</span></span>

