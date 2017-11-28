---
title: "aaaSwitch 陳述式，為 Azure 邏輯應用程式中的不同動作 |Microsoft 文件"
description: "選擇不同的動作 tooperform 使用 switch 陳述式，根據運算式值的邏輯應用程式中"
services: logic-apps
keywords: "Switch 陳述式"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a><span data-ttu-id="20fc4-104">使用 Switch 陳述式在邏輯應用程式中執行不同動作</span><span class="sxs-lookup"><span data-stu-id="20fc4-104">Perform different actions in logic apps with a switch statement</span></span>

<span data-ttu-id="20fc4-105">當撰寫工作流程，您通常需要 tootake 根據 hello 物件或運算式的值不同的動作。</span><span class="sxs-lookup"><span data-stu-id="20fc4-105">When authoring a workflow, you often have tootake different actions based on hello value of an object or expression.</span></span> <span data-ttu-id="20fc4-106">例如，您可以根據 hello 狀態碼的 HTTP 要求，您的邏輯應用程式 toobehave 或電子郵件中所選取的選項。</span><span class="sxs-lookup"><span data-stu-id="20fc4-106">For example, you might want your logic app toobehave differently based on hello status code of an HTTP request, or an option selected in an email.</span></span>

<span data-ttu-id="20fc4-107">您可以使用 switch 陳述式 tooimplement 這些案例。</span><span class="sxs-lookup"><span data-stu-id="20fc4-107">You can use a switch statement tooimplement these scenarios.</span></span> <span data-ttu-id="20fc4-108">邏輯應用程式可以評估語彙基元或運算式，並選擇以 hello hello 案例相同的值 tooexecute hello 指定動作。</span><span class="sxs-lookup"><span data-stu-id="20fc4-108">Your logic app can evaluate a token or expression, and choose hello case with hello same value tooexecute hello specified actions.</span></span> <span data-ttu-id="20fc4-109">只有其中一種情況應該符合 hello switch 陳述式。</span><span class="sxs-lookup"><span data-stu-id="20fc4-109">Only one case should match hello switch statement.</span></span>

> [!TIP]
> <span data-ttu-id="20fc4-110">如同所有的程式設計語言，Switch 陳述式僅支援等號比較運算子。</span><span class="sxs-lookup"><span data-stu-id="20fc4-110">Like all programming languages, switch statements support only equality operators.</span></span> <span data-ttu-id="20fc4-111">如果您需要其他關係運算子 (例如，「大於」)，請使用條件陳述式。</span><span class="sxs-lookup"><span data-stu-id="20fc4-111">If you need other relational operators, such as "greater than", use a condition statement.</span></span>
> <span data-ttu-id="20fc4-112">tooensure 具決定性的執行行為，情況下都必須包含唯一且靜態的值，而不是動態的語彙基元或運算式。</span><span class="sxs-lookup"><span data-stu-id="20fc4-112">tooensure deterministic execution behavior, cases must contain a unique and static value instead of dynamic tokens or expression.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20fc4-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="20fc4-113">Prerequisites</span></span>

- <span data-ttu-id="20fc4-114">有效的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="20fc4-114">An active Azure subscription.</span></span> <span data-ttu-id="20fc4-115">如果您沒有作用中 Azure 訂用帳戶，[請建立免費帳戶](https://azure.microsoft.com/free/)，或免費嘗試 [Logic Apps](https://tryappservice.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="20fc4-115">If you don't have an active Azure subscription, [create a free account](https://azure.microsoft.com/free/), or try [Logic Apps for free](https://tryappservice.azure.com/).</span></span>
- [<span data-ttu-id="20fc4-116">邏輯應用程式基本知識</span><span class="sxs-lookup"><span data-stu-id="20fc4-116">Basic knowledge about logic apps</span></span>](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a><span data-ttu-id="20fc4-117">加入參數的陳述式 tooyour 工作流程</span><span class="sxs-lookup"><span data-stu-id="20fc4-117">Add a switch statement tooyour workflow</span></span>

<span data-ttu-id="20fc4-118">tooshow switch 陳述式的運作方式，此範例會建立監視的檔案上傳 tooDropbox 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fc4-118">tooshow how a switch statement works, this example creates a logic app that monitors files uploaded tooDropbox.</span></span> <span data-ttu-id="20fc4-119">Hello 邏輯應用程式時 hello 新檔案上傳時，傳送電子郵件 tooan 核准者選擇是否 tootransfer 那些檔案 tooSharePoint。</span><span class="sxs-lookup"><span data-stu-id="20fc4-119">When hello new files are uploaded, hello logic app sends email tooan approver who chooses whether tootransfer those files tooSharePoint.</span></span> <span data-ttu-id="20fc4-120">hello 應用程式會使用 switch 陳述式，會執行不同動作根據 hello 值 hello 核准者選取。</span><span class="sxs-lookup"><span data-stu-id="20fc4-120">hello app uses a switch statement that performs different actions based on hello value that hello approver selects.</span></span>

1. <span data-ttu-id="20fc4-121">建立邏輯應用程式，並選取觸發程序：**Dropbox - 建立檔案時**。</span><span class="sxs-lookup"><span data-stu-id="20fc4-121">Create a logic app, and select this trigger: **Dropbox - When a file is created**.</span></span>

   ![使用 Dropbox - 建立檔案時觸發程序](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. <span data-ttu-id="20fc4-123">在 hello 觸發程序，新增這項動作： **Outlook.com-傳送核准電子郵件**</span><span class="sxs-lookup"><span data-stu-id="20fc4-123">Under hello trigger, add this action: **Outlook.com - Send approval email**</span></span>

   > [!TIP]
   > <span data-ttu-id="20fc4-124">邏輯應用程式也支援從 Office 365 Outlook 帳戶傳送核准電子郵件案例。</span><span class="sxs-lookup"><span data-stu-id="20fc4-124">Logic apps also support sending approval email scenarios from an Office 365 Outlook account.</span></span>

   - <span data-ttu-id="20fc4-125">如果您沒有現有的連接，則會提示您 toocreate 其中一個。</span><span class="sxs-lookup"><span data-stu-id="20fc4-125">If you don't have an existing connection, you're prompted toocreate one.</span></span>
   - <span data-ttu-id="20fc4-126">填寫 hello 必要欄位。</span><span class="sxs-lookup"><span data-stu-id="20fc4-126">Fill in hello required fields.</span></span> <span data-ttu-id="20fc4-127">例如，在**至**，指定用於傳送嗨核准者電子郵件的 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="20fc4-127">For example, under **To**, specify hello email address for sending hello approver email.</span></span>
   - <span data-ttu-id="20fc4-128">在 [使用者選項] 下，輸入 `Approve, Reject`。</span><span class="sxs-lookup"><span data-stu-id="20fc4-128">Under **User Options**, enter `Approve, Reject`.</span></span>

   ![設定連線](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. <span data-ttu-id="20fc4-130">新增 Switch 陳述式。</span><span class="sxs-lookup"><span data-stu-id="20fc4-130">Add a switch statement.</span></span>

   - <span data-ttu-id="20fc4-131">選取 [+ 新步驟] > ...更多 > [新增 Switch 案例]。</span><span class="sxs-lookup"><span data-stu-id="20fc4-131">Select **+ New step** > **... More** > **Add a switch case**.</span></span> 
   - <span data-ttu-id="20fc4-132">現在我們想要根據 hello tooselect hello 動作 tooperform`SelectedOptions`輸出 hello*傳送核准電子郵件*動作。</span><span class="sxs-lookup"><span data-stu-id="20fc4-132">Now we want tooselect hello action tooperform based on hello `SelectedOptions` output from hello *Send approval email* action.</span></span> 
   <span data-ttu-id="20fc4-133">您可以找到此欄位在 hello**加入動態內容**選取器。</span><span class="sxs-lookup"><span data-stu-id="20fc4-133">You can find this field in hello **Add dynamic content** selector.</span></span>
   - <span data-ttu-id="20fc4-134">使用*案例 1* toohandle 當 hello 核准者選取`Approve`。</span><span class="sxs-lookup"><span data-stu-id="20fc4-134">Use *Case 1* toohandle when hello approver selects `Approve`.</span></span>
     - <span data-ttu-id="20fc4-135">如果核准，將複製 hello 原始檔 tooSharePoint 線上以 hello [ **SharePoint Online-建立檔案**動作](../connectors/connectors-create-api-sharepointonline.md)。</span><span class="sxs-lookup"><span data-stu-id="20fc4-135">If approved, copy hello original file tooSharePoint Online with hello [**SharePoint Online - Create file** action](../connectors/connectors-create-api-sharepointonline.md).</span></span>
     - <span data-ttu-id="20fc4-136">加入另一個新的檔案是在 SharePoint 上可用的 hello 案例 toonotify 使用者動作。</span><span class="sxs-lookup"><span data-stu-id="20fc4-136">Add another action within hello case toonotify users that a new file is available on SharePoint.</span></span>
   - <span data-ttu-id="20fc4-137">當使用者選取時，加入另一個案例 toohandle `Reject`。</span><span class="sxs-lookup"><span data-stu-id="20fc4-137">Add another case toohandle when user selects `Reject`.</span></span>
     - <span data-ttu-id="20fc4-138">如果拒絕，傳送通知電子郵件通知其他核准者 hello 檔案會被拒絕，並不需要任何進一步的動作。</span><span class="sxs-lookup"><span data-stu-id="20fc4-138">If rejected, send a notification email informing other approvers that hello file is rejected and no further action is required.</span></span>
   - <span data-ttu-id="20fc4-139">`SelectedOptions`只有兩個選項，讓我們可以保留 hello**預設**空白的案例。</span><span class="sxs-lookup"><span data-stu-id="20fc4-139">`SelectedOptions` provides only two options, so we can leave hello **Default** case empty.</span></span>

   ![Switch 陳述式](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > <span data-ttu-id="20fc4-141">Switch 陳述式必須至少一個加法 toohello 預設案例中的案例。</span><span class="sxs-lookup"><span data-stu-id="20fc4-141">A switch statement needs at least one case in addition toohello default case.</span></span>

4. <span data-ttu-id="20fc4-142">Hello switch 陳述式之後, 刪除原始上傳檔案 tooDropbox hello 加入這項動作： **Dropbox-刪除檔案**</span><span class="sxs-lookup"><span data-stu-id="20fc4-142">After hello switch statement, delete hello original file uploaded tooDropbox by adding this action: **Dropbox - Delete file**</span></span>

5. <span data-ttu-id="20fc4-143">儲存您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fc4-143">Save your logic app.</span></span> <span data-ttu-id="20fc4-144">上傳檔案 tooDropbox 來測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="20fc4-144">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="20fc4-145">您應該很快就會收到核准電子郵件。</span><span class="sxs-lookup"><span data-stu-id="20fc4-145">You should receive an approval email shortly.</span></span> <span data-ttu-id="20fc4-146">選取選項，並觀察 hello 行為。</span><span class="sxs-lookup"><span data-stu-id="20fc4-146">Select an option, and observe hello behavior.</span></span>

   > [!TIP]
   > <span data-ttu-id="20fc4-147">如何查看太[監視您的 logic apps](logic-apps-monitor-your-logic-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="20fc4-147">Check out how too[monitor your logic apps](logic-apps-monitor-your-logic-apps.md).</span></span>

## <a name="understand-hello-code-behind-switch-statements"></a><span data-ttu-id="20fc4-148">了解 hello switch 陳述式後面的程式碼</span><span class="sxs-lookup"><span data-stu-id="20fc4-148">Understand hello code behind switch statements</span></span>

<span data-ttu-id="20fc4-149">既然您已成功建立使用 switch 陳述式的邏輯應用程式，讓我們看看 hello hello switch 陳述式後面的程式碼定義。</span><span class="sxs-lookup"><span data-stu-id="20fc4-149">Now that you successfully created a logic app using a switch statement, let's look at hello code definition behind hello switch statement.</span></span>

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* <span data-ttu-id="20fc4-150">`"Switch"`這是 hello hello switch 陳述式，您可以針對可讀性重新命名的名稱。</span><span class="sxs-lookup"><span data-stu-id="20fc4-150">`"Switch"` is hello name of hello switch statement, which you can rename for readability.</span></span> 
* <span data-ttu-id="20fc4-151">`"type": "Switch"`指出 hello 動作是在 switch 陳述式。</span><span class="sxs-lookup"><span data-stu-id="20fc4-151">`"type": "Switch"` indicates that hello action is a switch statement.</span></span> 
* <span data-ttu-id="20fc4-152">`"expression"`是 hello 核准者選取的選項，在此範例中，而且會評估針對宣告稍後在 hello 定義每個案例。</span><span class="sxs-lookup"><span data-stu-id="20fc4-152">`"expression"` is hello approver's selected option in this example and is evaluated against each case declared later in hello definition.</span></span> 
* <span data-ttu-id="20fc4-153">`"cases"` 可以包含任意數目的案例。</span><span class="sxs-lookup"><span data-stu-id="20fc4-153">`"cases"` can contain any number of cases.</span></span> <span data-ttu-id="20fc4-154">每個案例中，`"Case *"`是 hello hello 的情況下，您可以針對可讀性重新命名預設名稱。</span><span class="sxs-lookup"><span data-stu-id="20fc4-154">For each case, `"Case *"` is hello default name of hello case, which you can rename for readability.</span></span> 
<span data-ttu-id="20fc4-155">`"case"`指定 hello case 標籤 hello 參數運算式使用的比較，而且必須是常數且唯一的值。</span><span class="sxs-lookup"><span data-stu-id="20fc4-155">`"case"` specifies hello case label, which hello switch expression uses for comparison, and must be a constant and unique value.</span></span> <span data-ttu-id="20fc4-156">如果沒有的 hello 案例符合 hello switch 運算式，在動作`"default"`會執行。</span><span class="sxs-lookup"><span data-stu-id="20fc4-156">If none of hello cases match hello switch expression, actions under `"default"` are executed.</span></span>

## <a name="get-help"></a><span data-ttu-id="20fc4-157">取得說明</span><span class="sxs-lookup"><span data-stu-id="20fc4-157">Get help</span></span>

<span data-ttu-id="20fc4-158">tooask 問題、 解答的問題，以及執行其他 Azure 邏輯應用程式使用者，請參閱瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。</span><span class="sxs-lookup"><span data-stu-id="20fc4-158">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="20fc4-159">toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。</span><span class="sxs-lookup"><span data-stu-id="20fc4-159">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="20fc4-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20fc4-160">Next steps</span></span>

- <span data-ttu-id="20fc4-161">了解如何太[新增條件](logic-apps-use-logic-app-features.md)</span><span class="sxs-lookup"><span data-stu-id="20fc4-161">Learn how too[add conditions](logic-apps-use-logic-app-features.md)</span></span>
- <span data-ttu-id="20fc4-162">了解[錯誤和例外狀況處理](logic-apps-exception-handling.md)</span><span class="sxs-lookup"><span data-stu-id="20fc4-162">Learn about [error and exception handling](logic-apps-exception-handling.md)</span></span>
- <span data-ttu-id="20fc4-163">深入探討[工作流程語言功能](logic-apps-author-definitions.md)</span><span class="sxs-lookup"><span data-stu-id="20fc4-163">Explore more [workflow language capabilities](logic-apps-author-definitions.md)</span></span>