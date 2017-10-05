---
title: "新增條件和啟動工作流程 - Azure Logic Apps | Microsoft Docs"
description: "新增條件式邏輯、觸發程序、動作和參數，以控制 Azure Logic Apps 中工作流程的執行方式。"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: e632c48ed31e82536db55a9c54438bece0c38fd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="df140-103">使用 Logic Apps 功能</span><span class="sxs-lookup"><span data-stu-id="df140-103">Use Logic Apps features</span></span>

<span data-ttu-id="df140-104">在[前面的主題](../logic-apps/logic-apps-create-a-logic-app.md)中，您已建立第一個邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="df140-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="df140-105">若要控制邏輯應用程式的工作流程，您可以指定不同的路徑以供邏輯應用程式執行，以及指定如何處理陣列、集合和批次中的資料。</span><span class="sxs-lookup"><span data-stu-id="df140-105">To control your logic app's workflow, you can specify different paths for your logic app to run and how to process data in arrays, collections, and batches.</span></span> <span data-ttu-id="df140-106">您可以將下列元素包含在邏輯應用程式的工作流程中：</span><span class="sxs-lookup"><span data-stu-id="df140-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="df140-107">條件和 [Switch 陳述式](../logic-apps/logic-apps-switch-case.md)可讓邏輯應用程式根據符合的特定條件來執行不同動作。</span><span class="sxs-lookup"><span data-stu-id="df140-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="df140-108">[迴圈](../logic-apps/logic-apps-loops-and-scopes.md)可讓邏輯應用程式重複執行步驟。</span><span class="sxs-lookup"><span data-stu-id="df140-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="df140-109">例如，使用 **For_each** 迴圈時，可以對陣列重複動作。</span><span class="sxs-lookup"><span data-stu-id="df140-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="df140-110">或者使用 **Until** 迴圈，可以在符合條件之後重複動作。</span><span class="sxs-lookup"><span data-stu-id="df140-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="df140-111">[Scope](../logic-apps/logic-apps-loops-and-scopes.md) 可讓您將一系列動作組成群組，例如用以進行例外狀況處理實作。</span><span class="sxs-lookup"><span data-stu-id="df140-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, to implement exception handling.</span></span>

* <span data-ttu-id="df140-112">使用 **SplitOn** 命令時，[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) 可讓邏輯應用程式啟動陣列中項目的個別工作流程。</span><span class="sxs-lookup"><span data-stu-id="df140-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use the **SplitOn** command.</span></span>

<span data-ttu-id="df140-113">本主題將介紹建置邏輯應用程式的其他概念：</span><span class="sxs-lookup"><span data-stu-id="df140-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="df140-114">用以編輯現有邏輯應用程式的程式碼檢視</span><span class="sxs-lookup"><span data-stu-id="df140-114">Code view to edit an existing logic app</span></span>
* <span data-ttu-id="df140-115">啟動工作流程的選項</span><span class="sxs-lookup"><span data-stu-id="df140-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="df140-116">條件：只有在符合條件後才執行步驟</span><span class="sxs-lookup"><span data-stu-id="df140-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="df140-117">若要在資料符合特定準則時，才讓邏輯應用程式執行步驟，您可以新增條件，針對特定欄位或值比較工作流程中的資料。</span><span class="sxs-lookup"><span data-stu-id="df140-117">To have your logic app run steps only when data meets specific criteria, you can add a condition that compares data in the workflow against specific fields or values.</span></span>

<span data-ttu-id="df140-118">例如，假設您的邏輯應用程式傳送過多的網站 RSS 摘要文章的電子郵件給您。</span><span class="sxs-lookup"><span data-stu-id="df140-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="df140-119">您可以新增條件，讓邏輯應用程式只有在新文章屬於特定類別時，才會傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="df140-119">You can add a condition so that your logic app sends email only when the new post belongs to a specific category.</span></span>

1. <span data-ttu-id="df140-120">在 [Azure 入口網站](https://portal.azure.com)的邏輯應用程式設計工具中，尋找並開啟邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="df140-120">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="df140-121">將條件新增至您想要的工作流程位置。</span><span class="sxs-lookup"><span data-stu-id="df140-121">Add a condition to the workflow location that you want.</span></span> 

   <span data-ttu-id="df140-122">若要在邏輯應用程式工作流程中的現有步驟之間新增條件，將指標移動至您要新增條件的箭頭處。</span><span class="sxs-lookup"><span data-stu-id="df140-122">To add the condition between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the condition.</span></span> 
   <span data-ttu-id="df140-123">選擇 **加號** \(**+**)， 然後選擇 **新增條件**。</span><span class="sxs-lookup"><span data-stu-id="df140-123">Choose the **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="df140-124">例如：</span><span class="sxs-lookup"><span data-stu-id="df140-124">For example:</span></span>

   ![將條件新增至邏輯應用程式](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="df140-126">如果想要在目前的工作流程結尾處新增條件，請移至邏輯應用程式底部，然後選擇 **+ 新增步驟**。</span><span class="sxs-lookup"><span data-stu-id="df140-126">If you want to add a condition at the end of your current workflow, go to the bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="df140-127">現在定義條件。</span><span class="sxs-lookup"><span data-stu-id="df140-127">Now define the condition.</span></span> <span data-ttu-id="df140-128">指定您想要評估的來源欄位、要執行的作業，以及目標值或欄位。</span><span class="sxs-lookup"><span data-stu-id="df140-128">Specify the source field that you want to evaluate, the operation to perform, and the target value or field.</span></span> <span data-ttu-id="df140-129">若要將現有欄位新增至條件，請從**新增動態內容清單**中選擇。</span><span class="sxs-lookup"><span data-stu-id="df140-129">To add existing fields to your condition, choose from the **Add dynamic content list**.</span></span>

   <span data-ttu-id="df140-130">例如：</span><span class="sxs-lookup"><span data-stu-id="df140-130">For example:</span></span>

   ![在基本模式中編輯條件](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="df140-132">以下是完整的條件：</span><span class="sxs-lookup"><span data-stu-id="df140-132">Here's the complete condition:</span></span>

   ![完整條件](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="df140-134">若要在程式碼中定義條件，請選擇**在進階模式中編輯**。</span><span class="sxs-lookup"><span data-stu-id="df140-134">To define the condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="df140-135">例如：</span><span class="sxs-lookup"><span data-stu-id="df140-135">For example:</span></span>
   > 
   > ![在程式碼中編輯條件](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="df140-137">在 **IF YES** 和 **IF NO** 之下，以是否符合條件為基礎，新增要執行的步驟。</span><span class="sxs-lookup"><span data-stu-id="df140-137">Under **IF YES** and **IF NO**, add the steps to perform based on whether the condition is met.</span></span>

   <span data-ttu-id="df140-138">例如：</span><span class="sxs-lookup"><span data-stu-id="df140-138">For example:</span></span>

   ![具 YES 和 NO 路徑的條件](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="df140-140">您可以將現有動作拖曳到 **IF YES** 和 **IF NO** 路徑。</span><span class="sxs-lookup"><span data-stu-id="df140-140">You can drag existing actions into the **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="df140-141">完成後，儲存邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="df140-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="df140-142">現在您只有在文章符合條件時，才會收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="df140-142">Now you get emails only when the posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="df140-143">使用 forEach 對清單重複執行動作</span><span class="sxs-lookup"><span data-stu-id="df140-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="df140-144">forEach 迴圈會指定要用來重複執行某動作的陣列。</span><span class="sxs-lookup"><span data-stu-id="df140-144">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="df140-145">如果它不是陣列，流程便會失敗。</span><span class="sxs-lookup"><span data-stu-id="df140-145">If it is not an array, the flow fails.</span></span> <span data-ttu-id="df140-146">舉例來說，如果 action1 會輸出訊息陣列，而您想要傳送每則訊息，則可以在動作的屬性中包含這個 forEach 陳述式︰`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="df140-146">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="df140-147">編輯邏輯應用程式的程式碼定義</span><span class="sxs-lookup"><span data-stu-id="df140-147">Edit the code definition for a logic app</span></span>

<span data-ttu-id="df140-148">儘管您擁有邏輯應用程式設計工具，您還是可以直接編輯定義邏輯應用程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="df140-148">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="df140-149">在命令列中，選擇 [程式碼檢視]。</span><span class="sxs-lookup"><span data-stu-id="df140-149">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="df140-150">隨即會開啟完整的編輯器，並顯示您所編輯的定義。</span><span class="sxs-lookup"><span data-stu-id="df140-150">A full editor opens and shows the definition you edited.</span></span>

    ![程式碼檢視](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="df140-152">在文字編輯器中，您可以在相同的邏輯應用程式或邏輯應用程式之間複製並貼上任何數量的動作。</span><span class="sxs-lookup"><span data-stu-id="df140-152">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="df140-153">您也可以輕鬆地在定義中新增或移除整個區段，以及與其他人共用定義。</span><span class="sxs-lookup"><span data-stu-id="df140-153">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="df140-154">若要儲存您的編輯，請選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="df140-154">To save your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="df140-155">參數</span><span class="sxs-lookup"><span data-stu-id="df140-155">Parameters</span></span>

<span data-ttu-id="df140-156">某些 Logic Apps 功能只能在程式碼檢視中取得，例如參數。</span><span class="sxs-lookup"><span data-stu-id="df140-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="df140-157">參數可讓您輕鬆地在整個邏輯應用程式中重複使用值。</span><span class="sxs-lookup"><span data-stu-id="df140-157">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="df140-158">例如，如果您想要在數個動作中使用同一個電子郵件地址，您應將該電子郵件地址定義為參數。</span><span class="sxs-lookup"><span data-stu-id="df140-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="df140-159">參數很適合用來提取您很可能經常變更的值。</span><span class="sxs-lookup"><span data-stu-id="df140-159">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="df140-160">當您需要在不同環境中覆寫參數時，參數特別有用。</span><span class="sxs-lookup"><span data-stu-id="df140-160">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="df140-161">如需如何根據環境覆寫參數的詳細資訊，請參閱[撰寫邏輯應用程式定義](../logic-apps/logic-apps-author-definitions.md)以及 [REST API 文件](https://docs.microsoft.com/rest/api/logic)。</span><span class="sxs-lookup"><span data-stu-id="df140-161">To learn how to override parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="df140-162">這個範例示範如何更新現有的邏輯應用程式，讓您可以針對查詢字詞使用參數。</span><span class="sxs-lookup"><span data-stu-id="df140-162">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="df140-163">在程式碼檢視中，尋找 `parameters : {}` 物件，並新增 `currentFeedUrl` 物件：</span><span class="sxs-lookup"><span data-stu-id="df140-163">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="df140-164">移至 `When_a_feed-item_is_published` 動作、尋找 `queries` 區段，然後以 `"feedUrl": "#@{parameters('currentFeedUrl')}"` 取代查詢值</span><span class="sxs-lookup"><span data-stu-id="df140-164">Go to the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="df140-165">若要加入兩或多個字串，您也可以使用 `concat` 函式。</span><span class="sxs-lookup"><span data-stu-id="df140-165">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="df140-166">例如，`"@concat('#',parameters('currentFeedUrl'))"`與上述相同的運作方式。</span><span class="sxs-lookup"><span data-stu-id="df140-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the above.</span></span>

3.  <span data-ttu-id="df140-167">完成之後，請選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="df140-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="df140-168">現在您可以透過 `currentFeedURL` 物件傳遞不同的 URL，藉以變更網站的 RSS 摘要。</span><span class="sxs-lookup"><span data-stu-id="df140-168">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<span data-ttu-id="df140-169">深入了解[如何撰寫邏輯應用程式定義](../logic-apps/logic-apps-author-definitions.md)。</span><span class="sxs-lookup"><span data-stu-id="df140-169">Learn more about [how to author logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="df140-170">啟動邏輯應用程式工作流程</span><span class="sxs-lookup"><span data-stu-id="df140-170">Start logic app workflows</span></span>

<span data-ttu-id="df140-171">您有數個不同的選項可用來啟動您邏輯應用程式中定義的工作流程。</span><span class="sxs-lookup"><span data-stu-id="df140-171">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="df140-172">您一律可在 [Azure 入口網站]中隨選啟動工作流程。</span><span class="sxs-lookup"><span data-stu-id="df140-172">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="df140-173">循環觸發程序</span><span class="sxs-lookup"><span data-stu-id="df140-173">Recurrence triggers</span></span>

<span data-ttu-id="df140-174">循環觸發程序會依照您指定的間隔執行。</span><span class="sxs-lookup"><span data-stu-id="df140-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="df140-175">當觸發程序具有條件式邏輯時，觸發程序會判斷工作流程是否需要執行。</span><span class="sxs-lookup"><span data-stu-id="df140-175">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="df140-176">觸發程序透過傳回 `200` 狀態碼，來指示工作流程應該執行。</span><span class="sxs-lookup"><span data-stu-id="df140-176">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="df140-177">當工作流程不需要執行時，觸發程序會傳回 `202` 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="df140-177">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="df140-178">使用 REST API 回呼</span><span class="sxs-lookup"><span data-stu-id="df140-178">Callback using REST APIs</span></span>

<span data-ttu-id="df140-179">若要啟動工作流程，服務可以呼叫邏輯應用程式端點。</span><span class="sxs-lookup"><span data-stu-id="df140-179">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="df140-180">若要隨選啟動該種邏輯應用程式，請選擇命令列上的 [立即執行]。</span><span class="sxs-lookup"><span data-stu-id="df140-180">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="df140-181">請參閱[呼叫邏輯應用程式端點做為觸發程序來啟動工作流程](../logic-apps/logic-apps-http-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="df140-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
<span data-ttu-id="df140-182">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="df140-182">[Azure portal]: https://portal.azure.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="df140-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df140-183">Next steps</span></span>

* [<span data-ttu-id="df140-184">Switch 陳述式</span><span class="sxs-lookup"><span data-stu-id="df140-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="df140-185">迴圈、範圍和解除批次處理</span><span class="sxs-lookup"><span data-stu-id="df140-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="df140-186">撰寫邏輯應用程式定義</span><span class="sxs-lookup"><span data-stu-id="df140-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)