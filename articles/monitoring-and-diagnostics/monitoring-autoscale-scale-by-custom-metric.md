---
title: "aaaGet 入門可藉由在 Azure 中的自訂度量來自動調整規模 |Microsoft 文件"
description: "深入了解如何 tooscale 您依在 Azure 中的自訂度量的資源。"
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
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="6cd6c-103">開始在 Azure 中依自訂計量自動調整規模</span><span class="sxs-lookup"><span data-stu-id="6cd6c-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="6cd6c-104">本文說明如何 tooscale 您透過 Azure 入口網站中的自訂度量的資源。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="6cd6c-105">只有 tooVirtual 機器規模集 (VMSS)、 雲端服務、 應用程式服務方案和應用程式服務環境，適用於 azure 監視的自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="6cd6c-106">開始使用</span><span class="sxs-lookup"><span data-stu-id="6cd6c-106">Lets get started</span></span>
<span data-ttu-id="6cd6c-107">本文假設您的 Web 應用程式已設定 Application Insights。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="6cd6c-108">如果您還沒有，則可[設定 ASP.NET 網站的 Application Insights][1]</span><span class="sxs-lookup"><span data-stu-id="6cd6c-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="6cd6c-109">開啟 [Azure 入口網站][2]</span><span class="sxs-lookup"><span data-stu-id="6cd6c-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="6cd6c-110">按一下 Azure 監視器 hello 左側的導覽窗格中的圖示。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="6cd6c-111">![啟動 Azure 監視器][3]</span><span class="sxs-lookup"><span data-stu-id="6cd6c-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="6cd6c-112">按一下 自動調整規模設定 tooview 自動標尺會針對適用的以及其目前的自動調整狀態的所有 hello 資源![探索 Azure 監視的自動調整規模][4]</span><span class="sxs-lookup"><span data-stu-id="6cd6c-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="6cd6c-113">開啟 Azure 監視器中的 '自動調整規模 刀鋒視窗，然後選取您想要 tooscale 的資源</span><span class="sxs-lookup"><span data-stu-id="6cd6c-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="6cd6c-114">注意： hello 執行下列步驟使用已設定的 app insights web 應用程式相關聯的應用程式服務計劃。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="6cd6c-115">在 hello hello 資源的小數位數設定刀鋒視窗，請注意 hello 目前執行個體計數為 1。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="6cd6c-116">按一下 [啟用自動調整規模]。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="6cd6c-117">![適用於新 Web 應用程式的調整規模設定][5]</span><span class="sxs-lookup"><span data-stu-id="6cd6c-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="6cd6c-118">提供名稱的 hello 縮放設定及 hello 請按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="6cd6c-119">請注意 hello 小數位數的規則選項，為 hello 右手邊的內容窗格隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="6cd6c-120">根據預設，它會設定您的執行個體計數 1，如果 hello 資源的 hello CPU percetage 超過 70%的 hello 選項 tooscale。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="6cd6c-121">變更 hello 度量來源 hello 頂端太選取"Application Insights"hello 在 hello 'Resource' 下拉式清單中，然後選取 hello 自訂度量以基礎的應用程式 insights 資源想 tooscale。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="6cd6c-122">![依自訂計量調整規模][6]</span><span class="sxs-lookup"><span data-stu-id="6cd6c-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="6cd6c-123">上述的類似 toohello 步驟會將調整規模規則將在縮放及 hello 擴充計數減 1，如果 hello 自訂公制低於臨界值。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="6cd6c-124">![根據 CPU 調整規模][7]</span><span class="sxs-lookup"><span data-stu-id="6cd6c-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="6cd6c-125">設定執行個體限制的 hello。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-125">Set hello you instance limits.</span></span> <span data-ttu-id="6cd6c-126">比方說，如果您想 tooscale 2-5 根據 hello 自訂度量波動的執行個體之間，設定 [最低] 太 '2'，'最大值' 得 '5' 和 'default' 太 '2 的'</span><span class="sxs-lookup"><span data-stu-id="6cd6c-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="6cd6c-127">附註： 讀取 hello 資源度量的問題，而且 hello 目前容量低於 hello 預設容量，然後 tooensure hello 可用性 hello 資源的自動調整規模將會向外延展 toohello 預設值。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="6cd6c-128">如果已經大於預設容量 hello 目前的容量，並不會將自動調整縮放中。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="6cd6c-129">按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="6cd6c-129">Click on 'Save'</span></span>

<span data-ttu-id="6cd6c-130">恭喜！</span><span class="sxs-lookup"><span data-stu-id="6cd6c-130">Congratulations.</span></span> <span data-ttu-id="6cd6c-131">您現在已成功建立您的自訂公制為基礎的 web 應用程式設定 tooauto 標尺的標尺。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="6cd6c-132">注意： hello 相同的步驟都適用 tooget 入門 VMSS 或雲端服務角色。</span><span class="sxs-lookup"><span data-stu-id="6cd6c-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
