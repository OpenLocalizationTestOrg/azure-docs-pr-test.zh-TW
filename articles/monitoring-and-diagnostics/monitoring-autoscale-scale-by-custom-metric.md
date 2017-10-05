---
title: "開始在 Azure 中依自訂計量自動調整規模 | Microsoft Docs"
description: "了解如何在 Azure 中依自訂計量調整資源的規模。"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: de8f7acadc282e4b81c657b1723f00fd3e5fd4f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="1b3e6-103">開始在 Azure 中依自訂計量自動調整規模</span><span class="sxs-lookup"><span data-stu-id="1b3e6-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="1b3e6-104">本文說明如何在 Azure 入口網站中依自訂計量調整您資源的規模。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-104">This article describes how to scale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="1b3e6-105">Azure 監視器自動調整規模僅適用於虛擬機器擴展集 (VMSS)、雲端服務、App Service 方案及 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="1b3e6-106">開始使用</span><span class="sxs-lookup"><span data-stu-id="1b3e6-106">Lets get started</span></span>
<span data-ttu-id="1b3e6-107">本文假設您的 Web 應用程式已設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="1b3e6-108">如果您還沒有，則可[設定 ASP.NET 網站的 Application Insights][1]</span><span class="sxs-lookup"><span data-stu-id="1b3e6-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="1b3e6-109">開啟 [Azure 入口網站][2]</span><span class="sxs-lookup"><span data-stu-id="1b3e6-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="1b3e6-110">按一下左側導覽窗格中的 [Azure 監視器] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-110">Click on Azure Monitor icon in the left navigation pane.</span></span>
  <span data-ttu-id="1b3e6-111">![啟動 Azure 監視器][3]</span><span class="sxs-lookup"><span data-stu-id="1b3e6-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="1b3e6-112">按一下 [自動調整規模] 設定，以檢視適用於自動調整規模的所有資源及其目前的自動調整規模狀態![探索 Azure 監視器中的自動調整規模][4]</span><span class="sxs-lookup"><span data-stu-id="1b3e6-112">Click on Autoscale setting to view all the resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="1b3e6-113">開啟 Azure 監視器中的 [自動調整規模] 刀鋒視窗，然後選取您想要調整的資源</span><span class="sxs-lookup"><span data-stu-id="1b3e6-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want to scale</span></span>
> <span data-ttu-id="1b3e6-114">注意︰下列步驟會使用與已設定 App Insights 之 Web 應用程式相關聯的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-114">Note: The steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="1b3e6-115">在資源的 [調整規模設定] 刀鋒視窗中，注意目前的執行個體計數為 1。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-115">In the scale setting blade for the resource, notice that the current instance count is 1.</span></span> <span data-ttu-id="1b3e6-116">按一下 [啟用自動調整規模]。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="1b3e6-117">![適用於新 Web 應用程式的調整規模設定][5]</span><span class="sxs-lookup"><span data-stu-id="1b3e6-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="1b3e6-118">提供調整規模設定的名稱，然後按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-118">Provide a name for the scale setting, and the click on "Add a rule".</span></span> <span data-ttu-id="1b3e6-119">請注意，調整規模規則選項會在右邊開啟為內容窗格。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-119">Notice the scale rule options that opens as a context pane in the right hand side.</span></span> <span data-ttu-id="1b3e6-120">預設會將選項設定為如果資源的 CPU 百分比超過 70%，就會將您的執行個體計數相應增加 1。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-120">By default, it sets the option to scale your instance count by 1 if the CPU percetage of the resource exceeds 70%.</span></span> <span data-ttu-id="1b3e6-121">變更 [Application Insights] 頂端的計量來源、選取 [資源] 下拉式清單中的 App Insights 資源，然後根據您想要調整規模的項目來選取自訂計量。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-121">Change the metric source at the top to "Application Insights", select the app insights resource in the 'Resource' dropdown and then select the custom metric based on which you want to scale.</span></span>
  <span data-ttu-id="1b3e6-122">![依自訂計量調整規模][6]</span><span class="sxs-lookup"><span data-stu-id="1b3e6-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="1b3e6-123">與上述步驟類似，新增一個將會相應縮小的調整規模規則，如果自訂計量低於臨界值，即會將調整規模計數減 1。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-123">Similar to the step above, add a scale rule that will scale in and decrease the scale count by 1 if the custom metric is below a threshold.</span></span>
  <span data-ttu-id="1b3e6-124">![根據 CPU 調整規模][7]</span><span class="sxs-lookup"><span data-stu-id="1b3e6-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="1b3e6-125">設定您的執行個體限制。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-125">Set the you instance limits.</span></span> <span data-ttu-id="1b3e6-126">例如，如果您想要根據自訂計量波動，在 2-5 個執行個體之間調整規模，可將 [最小值] 設為 2、將 [最大值] 設為 5，以及將 [預設值] 設為 2</span><span class="sxs-lookup"><span data-stu-id="1b3e6-126">For example, if you want to scale between 2-5 instances depending on the custom metric fluctuations, set 'minimum' to '2', 'maximum' to '5' and 'default' to '2'</span></span>
> <span data-ttu-id="1b3e6-127">注意︰萬一在讀取資源計量時發生問題，而且目前的容量低於預設容量，則為了確保資源的可用性，自動調整規模將會相應放大為預設值。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-127">Note: In case there is a problem reading the resource metrics and the current capacity is below the default capacity, then to ensure the availability of the resource, Autoscale will scale out to the default value.</span></span> <span data-ttu-id="1b3e6-128">如果目前的容量已超過預設容量，自動調整規模將不會進行相應縮小。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-128">If the current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="1b3e6-129">按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="1b3e6-129">Click on 'Save'</span></span>

<span data-ttu-id="1b3e6-130">恭喜！</span><span class="sxs-lookup"><span data-stu-id="1b3e6-130">Congratulations.</span></span> <span data-ttu-id="1b3e6-131">您現在已成功建立調整規模設定，可根據自訂計量自動調整 Web 應用程式的規模。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-131">You now now succesfully created your scale setting to auto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="1b3e6-132">注意︰相同的步驟都適用於開始使用 VMSS 或雲端服務角色。</span><span class="sxs-lookup"><span data-stu-id="1b3e6-132">Note: The same steps are applicable to get started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
