---
title: "aaaAdd 狀況，並啟動工作流程-Azure 邏輯應用程式 |Microsoft 文件"
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
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="118b0-103">使用 Logic Apps 功能</span><span class="sxs-lookup"><span data-stu-id="118b0-103">Use Logic Apps features</span></span>

<span data-ttu-id="118b0-104">在[前面的主題](../logic-apps/logic-apps-create-a-logic-app.md)中，您已建立第一個邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="118b0-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="118b0-105">toocontrol 邏輯應用程式的工作流程，您可以為您的邏輯應用程式 toorun 指定不同的路徑，並太如何處理陣列、 集合和批次中的資料。</span><span class="sxs-lookup"><span data-stu-id="118b0-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="118b0-106">您可以將下列元素包含在邏輯應用程式的工作流程中：</span><span class="sxs-lookup"><span data-stu-id="118b0-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="118b0-107">條件和 [Switch 陳述式](../logic-apps/logic-apps-switch-case.md)可讓邏輯應用程式根據符合的特定條件來執行不同動作。</span><span class="sxs-lookup"><span data-stu-id="118b0-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="118b0-108">[迴圈](../logic-apps/logic-apps-loops-and-scopes.md)可讓邏輯應用程式重複執行步驟。</span><span class="sxs-lookup"><span data-stu-id="118b0-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="118b0-109">例如，使用 **For_each** 迴圈時，可以對陣列重複動作。</span><span class="sxs-lookup"><span data-stu-id="118b0-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="118b0-110">或者使用 **Until** 迴圈，可以在符合條件之後重複動作。</span><span class="sxs-lookup"><span data-stu-id="118b0-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="118b0-111">[範圍](../logic-apps/logic-apps-loops-and-scopes.md)可讓您一系列動作組成群組，例如 tooimplement 例外狀況處理。</span><span class="sxs-lookup"><span data-stu-id="118b0-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="118b0-112">[解除批次處理即將](../logic-apps/logic-apps-loops-and-scopes.md)可讓您邏輯的應用程式啟動個別的工作流程項目的陣列中，當您使用 hello **SplitOn**命令。</span><span class="sxs-lookup"><span data-stu-id="118b0-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="118b0-113">本主題將介紹建置邏輯應用程式的其他概念：</span><span class="sxs-lookup"><span data-stu-id="118b0-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="118b0-114">程式碼檢視 tooedit 現有邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="118b0-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="118b0-115">啟動工作流程的選項</span><span class="sxs-lookup"><span data-stu-id="118b0-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="118b0-116">條件：只有在符合條件後才執行步驟</span><span class="sxs-lookup"><span data-stu-id="118b0-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="118b0-117">toohave 邏輯應用程式資料符合特定準則時，才執行的步驟，您可以加入條件比較 hello 針對特定欄位或值的工作流程中的資料。</span><span class="sxs-lookup"><span data-stu-id="118b0-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="118b0-118">例如，假設您的邏輯應用程式傳送過多的網站 RSS 摘要文章的電子郵件給您。</span><span class="sxs-lookup"><span data-stu-id="118b0-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="118b0-119">您可以加入條件，讓應用程式邏輯 hello 新文章時，才會傳送電子郵件所屬 tooa 特定類別。</span><span class="sxs-lookup"><span data-stu-id="118b0-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="118b0-120">在 [hello [Azure 入口網站](https://portal.azure.com)、 尋找和開啟邏輯應用程式邏輯應用程式的設計工具中。</span><span class="sxs-lookup"><span data-stu-id="118b0-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="118b0-121">新增您想要的條件 toohello 工作流程的位置。</span><span class="sxs-lookup"><span data-stu-id="118b0-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="118b0-122">hello 邏輯應用程式工作流程中的現有步驟之間 tooadd hello 條件 hello 指標移 hello 箭號想 tooadd hello 條件。</span><span class="sxs-lookup"><span data-stu-id="118b0-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="118b0-123">選擇 hello**加號**(**+**)，然後選擇 [**加入條件**。</span><span class="sxs-lookup"><span data-stu-id="118b0-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="118b0-124">例如：</span><span class="sxs-lookup"><span data-stu-id="118b0-124">For example:</span></span>

   ![新增條件 toologic 應用程式](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="118b0-126">如果您想 tooadd 條件在您目前的工作流程的 hello 結尾處，移 toohello 應用程式邏輯，底部，然後選擇**+ 新增步驟**。</span><span class="sxs-lookup"><span data-stu-id="118b0-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="118b0-127">現在定義 hello 條件。</span><span class="sxs-lookup"><span data-stu-id="118b0-127">Now define hello condition.</span></span> <span data-ttu-id="118b0-128">指定您想 tooevaluate、 hello 作業 tooperform，和 hello 目標值或欄位的 hello 來源欄位。</span><span class="sxs-lookup"><span data-stu-id="118b0-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="118b0-129">tooadd 現有欄位 tooyour 條件從 hello 選擇**動態內容清單中新增**。</span><span class="sxs-lookup"><span data-stu-id="118b0-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="118b0-130">例如：</span><span class="sxs-lookup"><span data-stu-id="118b0-130">For example:</span></span>

   ![在基本模式中編輯條件](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="118b0-132">以下是 hello 完成的條件：</span><span class="sxs-lookup"><span data-stu-id="118b0-132">Here's hello complete condition:</span></span>

   ![完整條件](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="118b0-134">toodefine hello 條件，程式碼中，選擇**在進階模式中編輯**。</span><span class="sxs-lookup"><span data-stu-id="118b0-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="118b0-135">例如：</span><span class="sxs-lookup"><span data-stu-id="118b0-135">For example:</span></span>
   > 
   > ![在程式碼中編輯條件](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="118b0-137">在下**是如果**和**如果否**，新增 hello 步驟 tooperform 根據是否滿足 hello 的條件。</span><span class="sxs-lookup"><span data-stu-id="118b0-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="118b0-138">例如：</span><span class="sxs-lookup"><span data-stu-id="118b0-138">For example:</span></span>

   ![具 YES 和 NO 路徑的條件](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="118b0-140">您可以將現有的動作拖曳到 hello**是如果**和**IF NO**路徑。</span><span class="sxs-lookup"><span data-stu-id="118b0-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="118b0-141">完成後，儲存邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="118b0-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="118b0-142">現在 hello 文章符合條件時，才收到電子郵件。</span><span class="sxs-lookup"><span data-stu-id="118b0-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="118b0-143">使用 forEach 對清單重複執行動作</span><span class="sxs-lookup"><span data-stu-id="118b0-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="118b0-144">hello forEach 迴圈會透過指定陣列 toorepeat 動作。</span><span class="sxs-lookup"><span data-stu-id="118b0-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="118b0-145">如果不是陣列，hello 流程將會失敗。</span><span class="sxs-lookup"><span data-stu-id="118b0-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="118b0-146">比方說，如果您有 action1，輸出陣列的訊息，而且您想 toosend 每則訊息，您可以將動作的 hello 屬性中包含這個 forEach 陳述式：`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="118b0-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="118b0-147">編輯 hello 邏輯應用程式的程式碼定義</span><span class="sxs-lookup"><span data-stu-id="118b0-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="118b0-148">雖然您擁有 hello 邏輯應用程式的設計工具，您可以直接編輯定義邏輯應用程式的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="118b0-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="118b0-149">在 [hello] 命令列上選擇 [**程式碼檢視**。</span><span class="sxs-lookup"><span data-stu-id="118b0-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="118b0-150">完整的編輯器隨即開啟，並顯示 hello 定義您編輯過。</span><span class="sxs-lookup"><span data-stu-id="118b0-150">A full editor opens and shows hello definition you edited.</span></span>

    ![程式碼檢視](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="118b0-152">Hello 文字編輯器中，您可以複製並貼上任何數目的 hello 內的動作相同邏輯應用程式或邏輯應用程式之間。</span><span class="sxs-lookup"><span data-stu-id="118b0-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="118b0-153">您也可以輕鬆地新增或移除 hello 定義的整個區段，您也可以與其他人共用定義。</span><span class="sxs-lookup"><span data-stu-id="118b0-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="118b0-154">編輯，選擇 [toosave**儲存**。</span><span class="sxs-lookup"><span data-stu-id="118b0-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="118b0-155">參數</span><span class="sxs-lookup"><span data-stu-id="118b0-155">Parameters</span></span>

<span data-ttu-id="118b0-156">某些 Logic Apps 功能只能在程式碼檢視中取得，例如參數。</span><span class="sxs-lookup"><span data-stu-id="118b0-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="118b0-157">參數可讓您輕鬆 tooreuse 整個邏輯應用程式中的值。</span><span class="sxs-lookup"><span data-stu-id="118b0-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="118b0-158">例如，如果您想要在數個動作中使用同一個電子郵件地址，您應將該電子郵件地址定義為參數。</span><span class="sxs-lookup"><span data-stu-id="118b0-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="118b0-159">參數雖然適合拉出，您很可能 toochange 的值。</span><span class="sxs-lookup"><span data-stu-id="118b0-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="118b0-160">當您需要在不同環境 toooverride 參數時，它們時特別有用。</span><span class="sxs-lookup"><span data-stu-id="118b0-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="118b0-161">如何 toooverride 參數根據環境中，請參閱的 toolearn[撰寫邏輯應用程式定義](../logic-apps/logic-apps-author-definitions.md)和[REST API 文件](https://docs.microsoft.com/rest/api/logic)。</span><span class="sxs-lookup"><span data-stu-id="118b0-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="118b0-162">這個範例會示範如何 tooupdate 您現有的邏輯應用程式，以便您可以將參數用於 hello 查詢詞彙。</span><span class="sxs-lookup"><span data-stu-id="118b0-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="118b0-163">在程式碼檢視中，找出 hello`parameters : {}`物件，並加入`currentFeedUrl`物件：</span><span class="sxs-lookup"><span data-stu-id="118b0-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="118b0-164">移 toohello`When_a_feed-item_is_published`動作、 尋找 hello`queries`區段，並取代 hello 查詢值為：`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="118b0-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="118b0-165">toojoin 兩個或多個字串，您也可以使用 hello`concat`函式。</span><span class="sxs-lookup"><span data-stu-id="118b0-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="118b0-166">例如， `"@concat('#',parameters('currentFeedUrl'))"` works hello 相同為上述的 hello。</span><span class="sxs-lookup"><span data-stu-id="118b0-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="118b0-167">完成之後，請選擇 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="118b0-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="118b0-168">現在您可以變更 hello 網站的 RSS 摘要藉由傳遞不同的 URL，透過 hello`currentFeedURL`物件。</span><span class="sxs-lookup"><span data-stu-id="118b0-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="118b0-169">深入了解[如何 tooauthor 邏輯應用程式定義](../logic-apps/logic-apps-author-definitions.md)。</span><span class="sxs-lookup"><span data-stu-id="118b0-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="118b0-170">啟動邏輯應用程式工作流程</span><span class="sxs-lookup"><span data-stu-id="118b0-170">Start logic app workflows</span></span>

<span data-ttu-id="118b0-171">您有不同的選項啟動應用程式邏輯中所定義的 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="118b0-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="118b0-172">您一律可以啟動工作流程隨 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="118b0-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="118b0-173">循環觸發程序</span><span class="sxs-lookup"><span data-stu-id="118b0-173">Recurrence triggers</span></span>

<span data-ttu-id="118b0-174">循環觸發程序會依照您指定的間隔執行。</span><span class="sxs-lookup"><span data-stu-id="118b0-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="118b0-175">當 hello 觸發程序具有條件式邏輯時，hello 觸發程序會判斷 hello 工作流程是否需要 toorun。</span><span class="sxs-lookup"><span data-stu-id="118b0-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="118b0-176">觸發程序指出 hello 工作流程應執行藉由傳回`200`狀態碼。</span><span class="sxs-lookup"><span data-stu-id="118b0-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="118b0-177">當 hello 工作流程不需要 toorun 時，hello 觸發程序傳回`202`狀態碼。</span><span class="sxs-lookup"><span data-stu-id="118b0-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="118b0-178">使用 REST API 回呼</span><span class="sxs-lookup"><span data-stu-id="118b0-178">Callback using REST APIs</span></span>

<span data-ttu-id="118b0-179">toostart 工作流程，服務可以呼叫邏輯應用程式端點。</span><span class="sxs-lookup"><span data-stu-id="118b0-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="118b0-180">這種邏輯應用程式依需求，選擇 [toostart**立即執行**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="118b0-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="118b0-181">請參閱[呼叫邏輯應用程式端點做為觸發程序來啟動工作流程](../logic-apps/logic-apps-http-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="118b0-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[Azure 入口網站]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="118b0-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="118b0-183">Next steps</span></span>

* [<span data-ttu-id="118b0-184">Switch 陳述式</span><span class="sxs-lookup"><span data-stu-id="118b0-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="118b0-185">迴圈、範圍和解除批次處理</span><span class="sxs-lookup"><span data-stu-id="118b0-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="118b0-186">撰寫邏輯應用程式定義</span><span class="sxs-lookup"><span data-stu-id="118b0-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)