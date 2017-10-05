---
title: "Azure 服務健康情況概觀 | Microsoft Docs"
description: "目前和未來的 Azure 服務問題和維修如何影響 Azure 應用程式的個人化資訊。"
services: Resource health
documentationcenter: 
author: rboucher
manager: 
editor: 
ms.assetid: 
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/07/2017
ms.author: robb
ms.openlocfilehash: 001dc1fa2a0fd7e132101944a87be3f8552d8738
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="azure-service-health"></a><span data-ttu-id="b69c3-103">Azure 服務健康情況</span><span class="sxs-lookup"><span data-stu-id="b69c3-103">Azure Service Health</span></span>
<span data-ttu-id="b69c3-104">Azure 服務的問題影響您的服務時，Azure 服務健康情況將提供適時的個人化資訊。</span><span class="sxs-lookup"><span data-stu-id="b69c3-104">Azure Service Health provides timely and personalized information when problems in Azure services impact your services.</span></span>  <span data-ttu-id="b69c3-105">它也可協助您準備好後續的預定維修。</span><span class="sxs-lookup"><span data-stu-id="b69c3-105">It also helps you prepare for upcoming planned maintenance.</span></span>

## <a name="service-health-events"></a><span data-ttu-id="b69c3-106">服務健康情況事件</span><span class="sxs-lookup"><span data-stu-id="b69c3-106">Service Health Events</span></span>
<span data-ttu-id="b69c3-107">服務健康情況會追蹤三種可能影響資源的健康情況事件：</span><span class="sxs-lookup"><span data-stu-id="b69c3-107">Service Health tracks three types of health events that may impact your resources:</span></span>
1. <span data-ttu-id="b69c3-108">**服務的問題** - 立即影響 Azure 服務的問題。</span><span class="sxs-lookup"><span data-stu-id="b69c3-108">**Service issues** - Problems in the Azure services that affect you right now.</span></span> 
2. <span data-ttu-id="b69c3-109">**規劃的維護** - 未來可能影響服務可用性的後續維修。</span><span class="sxs-lookup"><span data-stu-id="b69c3-109">**Planned maintenance** - Upcoming maintenance that can affect the availability of your services in the future.</span></span>  
3. <span data-ttu-id="b69c3-110">**健康情況摘要報告** - 需要注意的 Azure 服務變更。</span><span class="sxs-lookup"><span data-stu-id="b69c3-110">**Health advisories** - Changes in Azure services that require your attention.</span></span> <span data-ttu-id="b69c3-111">範例包括取代 Azure 功能，或超過使用量配額。</span><span class="sxs-lookup"><span data-stu-id="b69c3-111">Examples include when Azure features are deprecated or if you exceed a usage quota.</span></span>

    ![服務健康情況事件](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a><span data-ttu-id="b69c3-113">開始使用服務健康情況</span><span class="sxs-lookup"><span data-stu-id="b69c3-113">Get started with Service Health</span></span>
<span data-ttu-id="b69c3-114">若要啟動服務健康情況儀表板，請選取入口網站儀表板上的 [服務健康情況] 圖格。</span><span class="sxs-lookup"><span data-stu-id="b69c3-114">To launch your Service Health dashboard, select the Service Health tile on your portal dashboard.</span></span> <span data-ttu-id="b69c3-115">如果您先前已移除圖格，或您正在使用自訂的儀表板，搜尋「更多服務」(儀表板的左下方) 中的服務健康情況服務。</span><span class="sxs-lookup"><span data-stu-id="b69c3-115">If you have previously removed the tile or you're using custom dashboard, search for Service Health service in "More services" (bottom left on your dashboard).</span></span>
<span data-ttu-id="b69c3-116">![開始使用服務健康情況](./media/service-health-overview/azure-service-health-overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="b69c3-116">![Get started with Service Health](./media/service-health-overview/azure-service-health-overview-1.png)</span></span>

## <a name="see-current-issues-which-impact-your-services"></a><span data-ttu-id="b69c3-117">查看影響服務的目前問題</span><span class="sxs-lookup"><span data-stu-id="b69c3-117">See current issues which impact your services</span></span>
<span data-ttu-id="b69c3-118">**服務問題**檢視會顯示 Azure 服務中任何正在發生並影響資源的問題。</span><span class="sxs-lookup"><span data-stu-id="b69c3-118">The **Service issues** view shows any ongoing problems in Azure services that are impacting your resources.</span></span> <span data-ttu-id="b69c3-119">您可以了解問題開始發生的時間，以及受影響的服務和區域。</span><span class="sxs-lookup"><span data-stu-id="b69c3-119">You can understand when the issue began, and what services and regions are impacted.</span></span> <span data-ttu-id="b69c3-120">您也可以參閱最新的更新，以了解 Azure 如何解決問題。</span><span class="sxs-lookup"><span data-stu-id="b69c3-120">You can also read the most recent update to understand what Azure is doing to resolve the issue.</span></span> 
<span data-ttu-id="b69c3-121">![管理服務問題](./media/service-health-overview/azure-service-health-overview-2.png)</span><span class="sxs-lookup"><span data-stu-id="b69c3-121">![Manage service issue](./media/service-health-overview/azure-service-health-overview-2.png)</span></span>

<span data-ttu-id="b69c3-122">選擇 [潛在影響] 索引標籤，查看將受問題影響而且您擁有的資源列出的特定清單。</span><span class="sxs-lookup"><span data-stu-id="b69c3-122">Choose the **Potential impact** tab to see the specific list of resources you own that might be impacted by the issue.</span></span> <span data-ttu-id="b69c3-123">您可以下載這些資源的 CSV 清單，以便與小組共用。</span><span class="sxs-lookup"><span data-stu-id="b69c3-123">You can  download a CSV list of these resources to share with your team.</span></span>
<span data-ttu-id="b69c3-124">![管理服務問題 - 影響](./media/service-health-overview/azure-service-health-overview-4.png)</span><span class="sxs-lookup"><span data-stu-id="b69c3-124">![Manage service issue - Impact](./media/service-health-overview/azure-service-health-overview-4.png)</span></span>

## <a name="get-links-and-downloadable-explanations"></a><span data-ttu-id="b69c3-125">取得連結和可下載的說明</span><span class="sxs-lookup"><span data-stu-id="b69c3-125">Get links and downloadable explanations</span></span> 
<span data-ttu-id="b69c3-126">您可以取得問題的連結，以便在您的問題管理系統中使用。</span><span class="sxs-lookup"><span data-stu-id="b69c3-126">You can get a link for the issue to use in your problem management system.</span></span> <span data-ttu-id="b69c3-127">您可以下載 PDF，有時可以下載 CSV 檔案，以便與無法存取 Azure 入口網站的使用者共用。</span><span class="sxs-lookup"><span data-stu-id="b69c3-127">You can download PDF and sometimes CSV files to share with people who don’t have access to the Azure portal.</span></span>   
![管理服務問題 - 問題管理](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a><span data-ttu-id="b69c3-129">獲得 Microsoft 的支援</span><span class="sxs-lookup"><span data-stu-id="b69c3-129">Get support from Microsoft</span></span>
<span data-ttu-id="b69c3-130">若解決問題後您的資源仍處於不正常的狀態，請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="b69c3-130">Contact support if your resource is left in a bad state even after the issue is resolved.</span></span>  <span data-ttu-id="b69c3-131">使用頁面右邊的支援連結。</span><span class="sxs-lookup"><span data-stu-id="b69c3-131">Use the support links on the right of the page.</span></span>  

## <a name="pin-a-personalized-health-map-to-your-dashboard"></a><span data-ttu-id="b69c3-132">將個人化健康情況地圖釘選在儀表板</span><span class="sxs-lookup"><span data-stu-id="b69c3-132">Pin a personalized health map to your dashboard</span></span>
<span data-ttu-id="b69c3-133">篩選服務健康情況，以便顯示您的商務關鍵訂用帳戶、區域和資源類型。</span><span class="sxs-lookup"><span data-stu-id="b69c3-133">Filter Service Health to show your business-critical subscriptions, regions, and resource types.</span></span> <span data-ttu-id="b69c3-134">儲存篩選條件，並將個人化健康情況世界地圖釘選在入口網站儀表板。</span><span class="sxs-lookup"><span data-stu-id="b69c3-134">Save the filter and pin a personalized health world map to your portal dashboard.</span></span> 
<span data-ttu-id="b69c3-135">![篩選個人化健康情況地圖](./media/service-health-overview/azure-service-health-overview-6a.png)
![釘選個人化健康情況地圖](./media/service-health-overview/azure-service-health-overview-6b.png)</span><span class="sxs-lookup"><span data-stu-id="b69c3-135">![Filter personalized health map](./media/service-health-overview/azure-service-health-overview-6a.png)
![Pin a personalized health map](./media/service-health-overview/azure-service-health-overview-6b.png)</span></span>

## <a name="configure-service-health-alerts"></a><span data-ttu-id="b69c3-136">設定服務健康情況警示</span><span class="sxs-lookup"><span data-stu-id="b69c3-136">Configure Service Health alerts</span></span>
<span data-ttu-id="b69c3-137">Azure 服務健康情況已整合 Azure 監視器，當您的業務關鍵資源受到影響時，就會透過電子郵件、簡訊和 Webhook 通知向您發出警示。</span><span class="sxs-lookup"><span data-stu-id="b69c3-137">Azure Service Health integrates with Azure Monitor to alert you via emails, text messages, and webhook notifications when your business-critical resources are impacted.</span></span> <span data-ttu-id="b69c3-138">設定適當服務健康情況事件的活動記錄警示。</span><span class="sxs-lookup"><span data-stu-id="b69c3-138">Set up an activity log alert for the appropriate Service Health event.</span></span> <span data-ttu-id="b69c3-139">使用動作群組，將該警示傳送給組織中的適當人員。</span><span class="sxs-lookup"><span data-stu-id="b69c3-139">Route that alert to the appropriate people in your organization using Action Groups.</span></span> <span data-ttu-id="b69c3-140">如需詳細資訊，請參閱[設定適用於服務健康情況的警示](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="b69c3-140">For more information, see [Configure Alerts for Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)</span></span>

# <a name="next-steps"></a><span data-ttu-id="b69c3-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b69c3-141">Next Steps</span></span>
<span data-ttu-id="b69c3-142">設定警示，如此就能收到健康情況問題的通知。</span><span class="sxs-lookup"><span data-stu-id="b69c3-142">Set up alerts so you are notified of health issues.</span></span> <span data-ttu-id="b69c3-143">如需詳細資訊，請參閱[設定適用於服務健康情況的警示](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="b69c3-143">For more information, see [Configure Alerts for Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md).</span></span> 