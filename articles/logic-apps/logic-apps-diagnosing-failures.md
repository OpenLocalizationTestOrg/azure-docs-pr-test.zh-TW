---
title: "aaaDiagnose 失敗-Azure 邏輯應用程式 |Microsoft 文件"
description: "常見的方式 toounderstand 邏輯應用程式失敗的位置"
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
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="5d0e0-103">診斷邏輯應用程式失敗</span><span class="sxs-lookup"><span data-stu-id="5d0e0-103">Diagnose logic app failures</span></span>
<span data-ttu-id="5d0e0-104">如果您在與邏輯應用程式遇到問題或失敗，有幾個方法可協助您深入了解 hello 失敗所在。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="5d0e0-105">Azure 入口網站工具</span><span class="sxs-lookup"><span data-stu-id="5d0e0-105">Azure portal tools</span></span>
<span data-ttu-id="5d0e0-106">hello Azure 入口網站提供許多工具 toodiagnose 在每個步驟的每個邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="5d0e0-107">觸發程序記錄</span><span class="sxs-lookup"><span data-stu-id="5d0e0-107">Trigger history</span></span>

<span data-ttu-id="5d0e0-108">每個邏輯應用程式至少會有一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="5d0e0-109">如果您注意到未引發應用程式，看起來 hello 觸發程序的詳細資訊記錄在第一個項目。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="5d0e0-110">您可以存取 hello hello 邏輯 app'ss 主要刀鋒視窗上的觸發程序歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![找出 hello 觸發程序的歷程記錄][1]

<span data-ttu-id="5d0e0-112">hello 觸發程序記錄列出的應用程式邏輯所做的所有觸發程序嘗試。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="5d0e0-113">您可以按一下 每個觸發程序嘗試 toodrill 到 hello 詳細資料，特別是，任何輸入或輸出，hello 觸發程序嘗試產生。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="5d0e0-114">如果您尋找失敗的觸發程序，請選取 hello 觸發程序嘗試並選擇 hello**輸出**連結的 tooreview 任何產生的錯誤訊息，例如，不是有效的 FTP 認證。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="5d0e0-115">hello 不同的狀態，您可能會看到如下：</span><span class="sxs-lookup"><span data-stu-id="5d0e0-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="5d0e0-116">**已略過**。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-116">**Skipped**.</span></span> <span data-ttu-id="5d0e0-117">hello 端點輪詢的 toocheck 資料並收到回應，無可用的資料。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="5d0e0-118">**已成功**。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-118">**Succeeded**.</span></span> <span data-ttu-id="5d0e0-119">hello 觸發程序接收到回應，可用的資料。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="5d0e0-120">此狀態的原因可能是手動觸發程序、循環觸發程序或輪詢觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="5d0e0-121">這個狀態通常會伴隨 hello**引發**狀態，但可能不是如果您有條件或 SplitOn 命令未滿足的程式碼檢視中。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="5d0e0-122">**失敗**。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-122">**Failed**.</span></span> <span data-ttu-id="5d0e0-123">已產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="5d0e0-124">手動啟動觸發程序</span><span class="sxs-lookup"><span data-stu-id="5d0e0-124">Start a trigger manually</span></span>

<span data-ttu-id="5d0e0-125">如果您想 hello 邏輯應用程式 toocheck 立即不會等候 hello 下一個循環使用觸發程序時，按一下**選取的觸發程序**hello 主要刀鋒視窗 tooforce 核取上。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="5d0e0-126">例如，按一下此連結與 Dropbox 觸發程序會造成 hello 工作流程 tooimmediately 輪詢 Dropbox 對新檔案。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="5d0e0-127">執行記錄</span><span class="sxs-lookup"><span data-stu-id="5d0e0-127">Run history</span></span>

<span data-ttu-id="5d0e0-128">每個引發的觸發程序都會導致一次執行。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="5d0e0-129">您可以存取執行的資訊從 hello 主要刀鋒視窗中，其中包含許多可協助您了解 hello 工作流程期間發生什麼事的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![找出 hello 執行歷程記錄][2]

<span data-ttu-id="5d0e0-131">執行顯示 hello 下列狀態其中之一：</span><span class="sxs-lookup"><span data-stu-id="5d0e0-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="5d0e0-132">**已成功**。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-132">**Succeeded**.</span></span> <span data-ttu-id="5d0e0-133">所有動作都已成功。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-133">All actions succeeded.</span></span> <span data-ttu-id="5d0e0-134">如果發生失敗，稍後在 hello 工作流程中發生的動作已處理該失敗。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="5d0e0-135">也就被處理 hello 失敗狀況 toorun 設定失敗的動作之後的動作。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="5d0e0-136">**失敗**。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-136">**Failed**.</span></span> <span data-ttu-id="5d0e0-137">至少一個動作會在未處理的更新版本中 hello 工作流程的動作失敗。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="5d0e0-138">**已取消**。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-138">**Cancelled**.</span></span> <span data-ttu-id="5d0e0-139">hello 工作流程已執行但卻收到取消要求。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="5d0e0-140">**執行中**。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-140">**Running**.</span></span> <span data-ttu-id="5d0e0-141">目前正在執行 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-141">hello workflow is currently running.</span></span> <span data-ttu-id="5d0e0-142">節流的工作流程，或因為 hello 目前定價方案，可能會發生這個狀態。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="5d0e0-143">如需詳細資訊，請參閱[hello 定價頁面上的動作限制](https://azure.microsoft.com/pricing/details/app-service/plans/)。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="5d0e0-144">設定診斷功能 （出現在 hello 執行歷程記錄 hello 圖表） 也可以提供所發生的任何節流事件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="5d0e0-145">當您查看執行歷程記錄時，您可以向內切入來查看詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="5d0e0-146">觸發程序輸出</span><span class="sxs-lookup"><span data-stu-id="5d0e0-146">Trigger outputs</span></span>

<span data-ttu-id="5d0e0-147">觸發程序輸出顯示 hello 資料來自 hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="5d0e0-148">這些輸出可協助您判斷所有屬性是否如預期般傳回。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="5d0e0-149">如果您看見任何不了解的內容，請了解 Azure Logic Apps 如何[處理不同的內容類型](../logic-apps/logic-apps-content-type.md)。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![觸發程序輸出範例][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="5d0e0-151">動作輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="5d0e0-151">Action inputs and outputs</span></span>

<span data-ttu-id="5d0e0-152">您可以切入 hello 輸入和輸出接收動作。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="5d0e0-153">此資料是適合用來了解在 hello 大小和形狀 hello 輸出，以及找出可能產生任何錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![動作輸入和輸出][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="5d0e0-155">偵錯工作流程執行階段</span><span class="sxs-lookup"><span data-stu-id="5d0e0-155">Debug workflow runtime</span></span>

<span data-ttu-id="5d0e0-156">監視 hello 輸入、 輸出和執行中的觸發程序，以及您可以加入一些協助偵錯的步驟 tooa 工作流程。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="5d0e0-157">[RequestBin](http://requestb.in) 是一個強大的工具，您可以在工作流程中將其加入為一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="5d0e0-158">藉由使用 RequestBin，您可以設定的 HTTP 要求 inspector toodetermine hello 確切的大小、 圖形與 HTTP 要求的格式。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="5d0e0-159">您可以建立 RequestBin，並將 hello URL 貼在邏輯應用程式與您想 tootest，例如本文內容、 運算式或另一個步驟輸出的 HTTP POST 動作。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="5d0e0-160">執行 hello 邏輯應用程式之後，您可以重新整理產生從 hello Logic Apps 引擎時，如何形成 hello 要求您 RequestBin toosee。</span><span class="sxs-lookup"><span data-stu-id="5d0e0-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
