---
title: "診斷失敗 - Azure Logic Apps | Microsoft Docs"
description: "用以了解邏輯應用程式失敗所在的常見方法"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="fcb00-103">診斷邏輯應用程式失敗</span><span class="sxs-lookup"><span data-stu-id="fcb00-103">Diagnose logic app failures</span></span>
<span data-ttu-id="fcb00-104">如果您遇到關於邏輯應用程式的問題或失敗，有數種方法可協助您深入了解失敗所在之處。</span><span class="sxs-lookup"><span data-stu-id="fcb00-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="fcb00-105">Azure 入口網站工具</span><span class="sxs-lookup"><span data-stu-id="fcb00-105">Azure portal tools</span></span>
<span data-ttu-id="fcb00-106">Azure 入口網站提供許多工具，在每個步驟中診斷每個邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="fcb00-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="fcb00-107">觸發程序記錄</span><span class="sxs-lookup"><span data-stu-id="fcb00-107">Trigger history</span></span>

<span data-ttu-id="fcb00-108">每個邏輯應用程式至少會有一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="fcb00-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="fcb00-109">如果您發現無法引發應用程式，首先查看觸發程序歷程記錄以獲得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="fcb00-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="fcb00-110">您可以在邏輯應用程式的主要刀鋒視窗上存取觸發程序歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="fcb00-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![找出觸發程序歷程記錄][1]

<span data-ttu-id="fcb00-112">觸發程序歷程記錄會列出您的邏輯應用程式進行的所有觸發程序嘗試。</span><span class="sxs-lookup"><span data-stu-id="fcb00-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="fcb00-113">您可以按一下每個觸發程序嘗試，進一步探索詳細資料 (特別是觸發程序嘗試所產生的任何輸入或輸出)。</span><span class="sxs-lookup"><span data-stu-id="fcb00-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="fcb00-114">如果您發現失敗的觸發程序，請選取觸發程序嘗試並選擇 [輸出] 連結，以檢閱任何產生的錯誤訊息 (例如︰針對無效的 FTP 認證)。</span><span class="sxs-lookup"><span data-stu-id="fcb00-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="fcb00-115">您可能會看到不同的狀態：</span><span class="sxs-lookup"><span data-stu-id="fcb00-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="fcb00-116">**已略過**。</span><span class="sxs-lookup"><span data-stu-id="fcb00-116">**Skipped**.</span></span> <span data-ttu-id="fcb00-117">此端點經過輪詢以檢查資料，並收到沒有可用資料的回應。</span><span class="sxs-lookup"><span data-stu-id="fcb00-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="fcb00-118">**已成功**。</span><span class="sxs-lookup"><span data-stu-id="fcb00-118">**Succeeded**.</span></span> <span data-ttu-id="fcb00-119">觸發程序收到資料可用的回應。</span><span class="sxs-lookup"><span data-stu-id="fcb00-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="fcb00-120">此狀態的原因可能是手動觸發程序、循環觸發程序或輪詢觸發程序。</span><span class="sxs-lookup"><span data-stu-id="fcb00-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="fcb00-121">此狀態通常伴隨著 [已引發] 狀態，但如果程式碼檢視中有一個條件或 SplitOn 命令不符合，則可能不會出現。</span><span class="sxs-lookup"><span data-stu-id="fcb00-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="fcb00-122">**失敗**。</span><span class="sxs-lookup"><span data-stu-id="fcb00-122">**Failed**.</span></span> <span data-ttu-id="fcb00-123">已產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="fcb00-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="fcb00-124">手動啟動觸發程序</span><span class="sxs-lookup"><span data-stu-id="fcb00-124">Start a trigger manually</span></span>

<span data-ttu-id="fcb00-125">如果您希望邏輯應用程式立即檢查可用的觸發程序 (而不需等待下一個循環)，請按一下主要刀鋒視窗上的 [選取觸發程序]  來強制進行檢查。</span><span class="sxs-lookup"><span data-stu-id="fcb00-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="fcb00-126">例如，按一下這個包含 Dropbox 觸發程序的連結，會導致工作流程立即輪詢 Dropbox 中是否有新檔案。</span><span class="sxs-lookup"><span data-stu-id="fcb00-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="fcb00-127">執行記錄</span><span class="sxs-lookup"><span data-stu-id="fcb00-127">Run history</span></span>

<span data-ttu-id="fcb00-128">每個引發的觸發程序都會導致一次執行。</span><span class="sxs-lookup"><span data-stu-id="fcb00-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="fcb00-129">您可以從主要刀鋒視窗存取執行資訊，其中包含許多有助於了解工作流程期間發生什麼情況的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fcb00-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![找出執行記錄][2]

<span data-ttu-id="fcb00-131">一次執行會顯示下列其中一個狀態：</span><span class="sxs-lookup"><span data-stu-id="fcb00-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="fcb00-132">**已成功**。</span><span class="sxs-lookup"><span data-stu-id="fcb00-132">**Succeeded**.</span></span> <span data-ttu-id="fcb00-133">所有動作都已成功。</span><span class="sxs-lookup"><span data-stu-id="fcb00-133">All actions succeeded.</span></span> <span data-ttu-id="fcb00-134">如果發生失敗，已透過工作流程中後續發生的動作來處理。</span><span class="sxs-lookup"><span data-stu-id="fcb00-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="fcb00-135">也就是，設定為要在失敗動作後執行的動作已處理此失敗。</span><span class="sxs-lookup"><span data-stu-id="fcb00-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="fcb00-136">**失敗**。</span><span class="sxs-lookup"><span data-stu-id="fcb00-136">**Failed**.</span></span> <span data-ttu-id="fcb00-137">至少有一個動作發生了工作流程中後續的動作無法處理的失敗。</span><span class="sxs-lookup"><span data-stu-id="fcb00-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="fcb00-138">**已取消**。</span><span class="sxs-lookup"><span data-stu-id="fcb00-138">**Cancelled**.</span></span> <span data-ttu-id="fcb00-139">工作流程正執行中，但收到了取消要求。</span><span class="sxs-lookup"><span data-stu-id="fcb00-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="fcb00-140">**執行中**。</span><span class="sxs-lookup"><span data-stu-id="fcb00-140">**Running**.</span></span> <span data-ttu-id="fcb00-141">工作流程目前正在執行中。</span><span class="sxs-lookup"><span data-stu-id="fcb00-141">The workflow is currently running.</span></span> <span data-ttu-id="fcb00-142">節流處理的流程可能會出現此狀態，或者因為目前的定價方案所致。</span><span class="sxs-lookup"><span data-stu-id="fcb00-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="fcb00-143">如需詳細資訊，請參閱[定價頁面上的動作限制](https://azure.microsoft.com/pricing/details/app-service/plans/)。</span><span class="sxs-lookup"><span data-stu-id="fcb00-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="fcb00-144">設定診斷功能 (執行歷程記錄下方顯示的圖表) 也可以提供所發生的任何節流事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fcb00-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="fcb00-145">當您查看執行歷程記錄時，您可以向內切入來查看詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fcb00-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="fcb00-146">觸發程序輸出</span><span class="sxs-lookup"><span data-stu-id="fcb00-146">Trigger outputs</span></span>

<span data-ttu-id="fcb00-147">觸發程序輸出會顯示來自觸發程序的資料。</span><span class="sxs-lookup"><span data-stu-id="fcb00-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="fcb00-148">這些輸出可協助您判斷所有屬性是否如預期般傳回。</span><span class="sxs-lookup"><span data-stu-id="fcb00-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="fcb00-149">如果您看見任何不了解的內容，請了解 Azure Logic Apps 如何[處理不同的內容類型](../logic-apps/logic-apps-content-type.md)。</span><span class="sxs-lookup"><span data-stu-id="fcb00-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![觸發程序輸出範例][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="fcb00-151">動作輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="fcb00-151">Action inputs and outputs</span></span>

<span data-ttu-id="fcb00-152">您可以深入探索動作所接收的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="fcb00-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="fcb00-153">此資料有助於了解輸出的大小和圖形，而且有助於尋找任何可能產生的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="fcb00-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![動作輸入和輸出][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="fcb00-155">偵錯工作流程執行階段</span><span class="sxs-lookup"><span data-stu-id="fcb00-155">Debug workflow runtime</span></span>

<span data-ttu-id="fcb00-156">除了監視執行的輸入、輸出和觸發程序以外，您可以在工作流程中加入一些有助於偵錯的步驟。</span><span class="sxs-lookup"><span data-stu-id="fcb00-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="fcb00-157">[RequestBin](http://requestb.in) 是一個強大的工具，您可以在工作流程中將其加入為一個步驟。</span><span class="sxs-lookup"><span data-stu-id="fcb00-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="fcb00-158">使用 RequestBin，您就能設定 HTTP 要求檢查器，來判斷 HTTP 要求的確切大小、圖形和格式。</span><span class="sxs-lookup"><span data-stu-id="fcb00-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="fcb00-159">您可以建立 RequestBin 並在邏輯應用程式 HTTP POST 動作中貼上 URL，以及您想要測試的任何內文內容 (例如，運算式或另一個步驟輸出)。</span><span class="sxs-lookup"><span data-stu-id="fcb00-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="fcb00-160">執行邏輯應用程式之後，您可以重新整理 RequestBin，以查看要求從 Logic Apps 引擎產生時是如何形成的。</span><span class="sxs-lookup"><span data-stu-id="fcb00-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
