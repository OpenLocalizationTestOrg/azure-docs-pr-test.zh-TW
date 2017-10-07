---
title: "開始使用 Azure 中的自動調整規模的 aaaGet |Microsoft 文件"
description: "深入了解如何 tooscale 您在 Azure 中的資源。"
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="62684-103">開始在 Azure 中自動調整規模</span><span class="sxs-lookup"><span data-stu-id="62684-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="62684-104">本文說明如何 tooset 您 hello Microsoft Azure 入口網站中資源的自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="62684-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="62684-105">只有 toovirtual 機器擴展集、 雲端服務、 Azure App Service 方案和應用程式服務環境，適用於 azure 監視的自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="62684-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="62684-106">探索您的訂用帳戶中的 hello 自動調整規模設定</span><span class="sxs-lookup"><span data-stu-id="62684-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="62684-107">您可以探索所有自動調整會針對適用的 Azure 監視中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="62684-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="62684-108">使用下列逐步解說的步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="62684-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="62684-109">開啟 hello [Azure 入口網站。][1]</span><span class="sxs-lookup"><span data-stu-id="62684-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="62684-110">按一下 hello 左窗格中的 hello Azure 監視器圖示。</span><span class="sxs-lookup"><span data-stu-id="62684-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="62684-111">![開啟 Azure 監視器][2]</span><span class="sxs-lookup"><span data-stu-id="62684-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="62684-112">按一下**自動調整規模**tooview 所有 hello 資源的自動調整規模都是適用的資源，以及其目前的自動調整狀態。</span><span class="sxs-lookup"><span data-stu-id="62684-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="62684-113">![探索 Azure 監視器中的自動調整規模][3]</span><span class="sxs-lookup"><span data-stu-id="62684-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="62684-114">您可以使用 hello 向特定的資源群組、 特定的資源類型或特定的資源中的 hello 清單 tooselect 資源的最上層 tooscope hello 篩選 窗格。</span><span class="sxs-lookup"><span data-stu-id="62684-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="62684-115">每個資源，您會發現 hello 目前執行個體計數和 hello 自動調整狀態。</span><span class="sxs-lookup"><span data-stu-id="62684-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="62684-116">hello 自動調整狀態可以是：</span><span class="sxs-lookup"><span data-stu-id="62684-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="62684-117">**未設定**︰您尚未針對此資源啟用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="62684-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="62684-118">**已啟用**：您已針對此資源啟用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="62684-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="62684-119">**已停用**：您已針對此資源停用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="62684-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="62684-120">建立您的第一個自動調整規模設定</span><span class="sxs-lookup"><span data-stu-id="62684-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="62684-121">我們現在，請透過簡單的逐步解說 toocreate 第一次的自動調整規模設定。</span><span class="sxs-lookup"><span data-stu-id="62684-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="62684-122">開啟 hello**自動調整規模**刀鋒視窗中 Azure 監視器，然後選取您想要 tooscale 的資源。</span><span class="sxs-lookup"><span data-stu-id="62684-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="62684-123">（hello 下列步驟使用 web 應用程式相關聯的應用程式服務計劃。</span><span class="sxs-lookup"><span data-stu-id="62684-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="62684-124">您可以[在 5 分鐘內，將您的第一個 ASP.NET Web 應用程式建立在 Azure 中][4])</span><span class="sxs-lookup"><span data-stu-id="62684-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="62684-125">請注意 hello 目前執行個體計數為 1。</span><span class="sxs-lookup"><span data-stu-id="62684-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="62684-126">按一下 [啟用自動調整規模]。</span><span class="sxs-lookup"><span data-stu-id="62684-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="62684-127">![適用於新 Web 應用程式的調整規模設定][5]</span><span class="sxs-lookup"><span data-stu-id="62684-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="62684-128">提供設定，hello 標尺的名稱，然後按**新增規則**。</span><span class="sxs-lookup"><span data-stu-id="62684-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="62684-129">請注意 hello 右側的 [內容] 窗格為開啟的 hello 調整規則選項。</span><span class="sxs-lookup"><span data-stu-id="62684-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="62684-130">根據預設，這會設定您的執行個體計數 1，如果 hello hello 資源的 CPU 百分比超過 70%的 hello 選項 tooscale。</span><span class="sxs-lookup"><span data-stu-id="62684-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="62684-131">將其保留為預設值，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="62684-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="62684-132">![建立 Web 應用程式的調整規模設定][6]</span><span class="sxs-lookup"><span data-stu-id="62684-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="62684-133">您現在已建立第一個調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="62684-133">You've now created your first scale rule.</span></span> <span data-ttu-id="62684-134">請注意 UX 建議最佳作法，並指出該 hello"建議 toohave 規則中的至少一個小數位數。"</span><span class="sxs-lookup"><span data-stu-id="62684-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="62684-135">toodo 因此：</span><span class="sxs-lookup"><span data-stu-id="62684-135">toodo so:</span></span>
  
    <span data-ttu-id="62684-136">a.</span><span class="sxs-lookup"><span data-stu-id="62684-136">a.</span></span> <span data-ttu-id="62684-137">按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="62684-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="62684-138">b.</span><span class="sxs-lookup"><span data-stu-id="62684-138">b.</span></span> <span data-ttu-id="62684-139">設定**運算子**太**小於**。</span><span class="sxs-lookup"><span data-stu-id="62684-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="62684-140">c.</span><span class="sxs-lookup"><span data-stu-id="62684-140">c.</span></span> <span data-ttu-id="62684-141">設定**閾值**太**20**。</span><span class="sxs-lookup"><span data-stu-id="62684-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="62684-142">d.</span><span class="sxs-lookup"><span data-stu-id="62684-142">d.</span></span> <span data-ttu-id="62684-143">設定**作業**太**減少計數所依據**。</span><span class="sxs-lookup"><span data-stu-id="62684-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="62684-144">您現在應該會有一個調整規模設定，其會根據 CPU 使用量進行相應放大/相應縮小。</span><span class="sxs-lookup"><span data-stu-id="62684-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="62684-145">![根據 CPU 調整規模][8]</span><span class="sxs-lookup"><span data-stu-id="62684-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="62684-146">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="62684-146">Click **Save**.</span></span>

<span data-ttu-id="62684-147">恭喜！</span><span class="sxs-lookup"><span data-stu-id="62684-147">Congratulations!</span></span> <span data-ttu-id="62684-148">現在您已成功建立 web 應用程式根據 CPU 使用量您第一個小數位數設定 tooautoscale。</span><span class="sxs-lookup"><span data-stu-id="62684-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="62684-149">hello 相同的步驟都適用 tooget 開始使用的虛擬機器擴展集或雲端服務角色。</span><span class="sxs-lookup"><span data-stu-id="62684-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="62684-150">其他考量</span><span class="sxs-lookup"><span data-stu-id="62684-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="62684-151">根據排程進行調整</span><span class="sxs-lookup"><span data-stu-id="62684-151">Scale based on a schedule</span></span>
<span data-ttu-id="62684-152">此外 tooscale 根據 CPU，您可以設定您的標尺不同的 hello 一週的特定幾天。</span><span class="sxs-lookup"><span data-stu-id="62684-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="62684-153">按一下 [新增調整規模的條件]。</span><span class="sxs-lookup"><span data-stu-id="62684-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="62684-154">設定模式和 hello 規則 hello 小數位數是 hello 相同當做 hello 預設條件。</span><span class="sxs-lookup"><span data-stu-id="62684-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="62684-155">選取**重複特定幾天**hello 排程。</span><span class="sxs-lookup"><span data-stu-id="62684-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="62684-156">選取 hello 天和 hello 開始/結束時間應套用 hello 小數位數的條件。</span><span class="sxs-lookup"><span data-stu-id="62684-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![根據排程調整規模的條件][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="62684-158">在特定日期以不同方式調整規模</span><span class="sxs-lookup"><span data-stu-id="62684-158">Scale differently on specific dates</span></span>
<span data-ttu-id="62684-159">此外 tooscale 根據 CPU，您可以設定您的標尺以不同方式的特定日期。</span><span class="sxs-lookup"><span data-stu-id="62684-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="62684-160">按一下 [新增調整規模的條件]。</span><span class="sxs-lookup"><span data-stu-id="62684-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="62684-161">設定模式和 hello 規則 hello 小數位數是 hello 相同當做 hello 預設條件。</span><span class="sxs-lookup"><span data-stu-id="62684-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="62684-162">選取**指定開始/結束日期**hello 排程。</span><span class="sxs-lookup"><span data-stu-id="62684-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="62684-163">選取 hello 開始/結束日期和 hello 開始/結束時間應套用 hello 小數位數的條件。</span><span class="sxs-lookup"><span data-stu-id="62684-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![根據日期調整規模的條件][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="62684-165">檢視您資源的 hello 標尺歷程記錄</span><span class="sxs-lookup"><span data-stu-id="62684-165">View hello scale history of your resource</span></span>
<span data-ttu-id="62684-166">每當您的資源縮放向上或向下，事件會記錄在 hello 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="62684-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="62684-167">您可以檢視 hello 標尺記錄之資源的 hello 過去 24 小時內切換 toohello**執行歷程記錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="62684-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![執行記錄][11]

<span data-ttu-id="62684-169">如果您想 tooview hello 完成延展歷程記錄 (如向上 too90 天)，請選取**按一下這裡 toosee 更多詳細資料**。</span><span class="sxs-lookup"><span data-stu-id="62684-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="62684-170">hello 活動記錄檔會開啟，預先選取您的資源和類別目錄的自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="62684-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="62684-171">檢視您資源的 hello 小數位數定義</span><span class="sxs-lookup"><span data-stu-id="62684-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="62684-172">自動調整規模是 Azure Resource Manager 的資源。</span><span class="sxs-lookup"><span data-stu-id="62684-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="62684-173">您可以在 JSON 中檢視 hello 小數位數的定義，藉由切換 toohello **JSON**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="62684-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![調整規模定義][12]

<span data-ttu-id="62684-175">您可以視需要直接在 JSON 中進行變更。</span><span class="sxs-lookup"><span data-stu-id="62684-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="62684-176">變更將在儲存後生效。</span><span class="sxs-lookup"><span data-stu-id="62684-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="62684-177">停用自動調整規模並手動調整執行個體規模</span><span class="sxs-lookup"><span data-stu-id="62684-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="62684-178">可能會有時間，當您想 toodisable 目前的調整規模設定並手動調整您的資源。</span><span class="sxs-lookup"><span data-stu-id="62684-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="62684-179">按一下 hello**停用自動調整規模**hello 頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="62684-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="62684-180">![停用自動調整規模][13]</span><span class="sxs-lookup"><span data-stu-id="62684-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="62684-181">此選項會停用您的設定。</span><span class="sxs-lookup"><span data-stu-id="62684-181">This option disables your configuration.</span></span> <span data-ttu-id="62684-182">不過，您可以取得 tooit 之後重新啟用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="62684-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="62684-183">您現在可以設定您想 tooscale toomanually 的執行個體的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="62684-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![設定手動調整規模][14]

<span data-ttu-id="62684-185">您可以按一下傳回 tooAutoscale**啟用自動調整規模**然後**儲存**。</span><span class="sxs-lookup"><span data-stu-id="62684-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62684-186">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62684-186">Next steps</span></span>
- [<span data-ttu-id="62684-187">建立活動記錄警示 toomonitor 訂用帳戶上的所有自動調整引擎作業</span><span class="sxs-lookup"><span data-stu-id="62684-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="62684-188">建立活動記錄警示 toomonitor 訂用帳戶所有失敗的自動調整標尺輸入/向外作業</span><span class="sxs-lookup"><span data-stu-id="62684-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

