---
title: "aaaSchema 更新年 6 月 1 2016-Azure 邏輯應用程式 |Microsoft 文件"
description: "使用結構描述 2016-06-01 版本建立 Azure Logic Apps 的 JSON 定義"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="26b48-103">Azure Logic Apps 的結構描述更新 - 2016 年 6 月 1 日</span><span class="sxs-lookup"><span data-stu-id="26b48-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="26b48-104">這個新的結構描述和 API 版本 Azure 邏輯應用程式包含多個製作邏輯應用程式的重要改良 toouse 可靠且更容易：</span><span class="sxs-lookup"><span data-stu-id="26b48-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

* <span data-ttu-id="26b48-105">[範圍](#scopes)可讓您建立動作的巢狀或群組做為動作集合。</span><span class="sxs-lookup"><span data-stu-id="26b48-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="26b48-106">[條件和迴圈](#conditions-loops)現在是第一級動作。</span><span class="sxs-lookup"><span data-stu-id="26b48-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="26b48-107">更精確的順序執行動作以 hello`runAfter`屬性，取代`dependsOn`</span><span class="sxs-lookup"><span data-stu-id="26b48-107">More precise ordering for running actions with hello `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="26b48-108">從您的 logic apps hello 2015 年 8 月 1 日的 tooupgrade 預覽結構描述 toohello 2016 年 6 月 1 日的結構描述，[簽出 hello 升級] 區段](##upgrade-your-schema)。</span><span class="sxs-lookup"><span data-stu-id="26b48-108">tooupgrade your logic apps from hello August 1, 2015 preview schema toohello June 1, 2016 schema, [check out hello upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="26b48-109">範圍</span><span class="sxs-lookup"><span data-stu-id="26b48-109">Scopes</span></span>

<span data-ttu-id="26b48-110">這個結構描述包含可讓您將動作群組在一起或在彼此內巢狀動作的範圍。</span><span class="sxs-lookup"><span data-stu-id="26b48-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="26b48-111">例如，條件可包含另一個條件。</span><span class="sxs-lookup"><span data-stu-id="26b48-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="26b48-112">深入了解[範圍語法](../logic-apps/logic-apps-loops-and-scopes.md)，或檢閱此基本範圍範例︰</span><span class="sxs-lookup"><span data-stu-id="26b48-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="26b48-113">條件和迴圈的變更</span><span class="sxs-lookup"><span data-stu-id="26b48-113">Conditions and loops changes</span></span>

<span data-ttu-id="26b48-114">在舊版結構描述中，條件和迴圈是與單一動作相關聯的參數。</span><span class="sxs-lookup"><span data-stu-id="26b48-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="26b48-115">此結構描述拿起這項限制，因此條件和迴圈現在會顯示為動作類型。</span><span class="sxs-lookup"><span data-stu-id="26b48-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="26b48-116">深入了解[迴圈和範圍](../logic-apps/logic-apps-loops-and-scopes.md)，或檢閱此基本範例的條件動作︰</span><span class="sxs-lookup"><span data-stu-id="26b48-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="26b48-117">'runAfter' 屬性</span><span class="sxs-lookup"><span data-stu-id="26b48-117">'runAfter' property</span></span>

<span data-ttu-id="26b48-118">hello`runAfter`屬性取代`dependsOn`、 提供更多有效位數，當您指定動作的 hello 執行順序是根據 hello 狀態的上一個動作。</span><span class="sxs-lookup"><span data-stu-id="26b48-118">hello `runAfter` property replaces `dependsOn`, providing more precision when you specify hello run order for actions based on hello status of previous actions.</span></span>

<span data-ttu-id="26b48-119">hello`dependsOn`屬性為 「 hello 動作執行和已順利完成 」 的同義詞，無論多少次想 tooexecute 動作，根據是否成功，hello 上一個動作失敗，或略過。</span><span class="sxs-lookup"><span data-stu-id="26b48-119">hello `dependsOn` property was synonymous with "hello action ran and was successful", no matter how many times you wanted tooexecute an action, based on whether hello previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="26b48-120">hello`runAfter`屬性提供該物件，指定所有 hello 之後 hello 物件會執行的動作名稱為的彈性。</span><span class="sxs-lookup"><span data-stu-id="26b48-120">hello `runAfter` property provides that flexibility as an object that specifies all hello action names after which hello object runs.</span></span> <span data-ttu-id="26b48-121">這個屬性也會定義可接受做為觸發程序狀態的陣列。</span><span class="sxs-lookup"><span data-stu-id="26b48-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="26b48-122">例如，如果您想 toorun 步驟的成功，並也之後步驟 B 成功或失敗之後，您建構這個`runAfter`屬性：</span><span class="sxs-lookup"><span data-stu-id="26b48-122">For example, if you wanted toorun after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="26b48-123">升級您的結構描述</span><span class="sxs-lookup"><span data-stu-id="26b48-123">Upgrade your schema</span></span>

<span data-ttu-id="26b48-124">升級 toohello 新的結構描述只需要幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="26b48-124">Upgrading toohello new schema only takes a few steps.</span></span> <span data-ttu-id="26b48-125">hello 升級程序包含執行 hello 升級指令碼，將儲存為新的邏輯應用程式，和如果想要的話，可能會覆寫 hello 先前邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26b48-125">hello upgrade process includes running hello upgrade script, saving as a new logic app, and if you want, possibly overwriting hello previous logic app.</span></span>

1. <span data-ttu-id="26b48-126">在 [hello Azure 入口網站，開啟邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26b48-126">In hello Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="26b48-127">跳過**概觀**。</span><span class="sxs-lookup"><span data-stu-id="26b48-127">Go too**Overview**.</span></span> <span data-ttu-id="26b48-128">Hello 邏輯應用程式工具列上，選擇**更新結構描述**。</span><span class="sxs-lookup"><span data-stu-id="26b48-128">On hello logic app toolbar, choose **Update Schema**.</span></span>
   
    ![選擇 [更新結構描述]][1]
   
    <span data-ttu-id="26b48-130">hello 升級的定義傳回時，您可以複製並貼到資源定義，如有必要的。</span><span class="sxs-lookup"><span data-stu-id="26b48-130">hello upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="26b48-131">不過，我們**強烈建議**您選擇**存**toomake 確定所有連接參考都是有效 hello 中升級邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26b48-131">However, we **strongly recommend** you choose **Save As** toomake sure that all connection references are valid in hello upgraded logic app.</span></span>

3. <span data-ttu-id="26b48-132">在 [hello 升級刀鋒視窗的工具列上，選擇 [**存**。</span><span class="sxs-lookup"><span data-stu-id="26b48-132">In hello upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="26b48-133">輸入 hello 邏輯名稱和狀態。</span><span class="sxs-lookup"><span data-stu-id="26b48-133">Enter hello logic name and status.</span></span> <span data-ttu-id="26b48-134">toodeploy 升級的邏輯應用程式，然後選擇 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="26b48-134">toodeploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="26b48-135">確認升級的邏輯應用程式如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="26b48-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="26b48-136">如果您使用手動或要求的觸發程序，hello 回呼 URL 會變更在新的邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="26b48-136">If you are using a manual or request trigger, hello callback URL changes in your new logic app.</span></span> <span data-ttu-id="26b48-137">測試 hello 新 URL toomake 確定 hello 端對端體驗運作。</span><span class="sxs-lookup"><span data-stu-id="26b48-137">Test hello new URL toomake sure hello end-to-end experience works.</span></span> <span data-ttu-id="26b48-138">toopreserve 前一個 Url，您可以複製現有的邏輯應用程式透過。</span><span class="sxs-lookup"><span data-stu-id="26b48-138">toopreserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="26b48-139">*選擇性*toooverwrite 先前邏輯應用程式與 hello 新結構描述版本，在 [hello] 工具列上選擇**複製**、 下一步太**更新結構描述**。</span><span class="sxs-lookup"><span data-stu-id="26b48-139">*Optional* toooverwrite your previous logic app with hello new schema version, on hello toolbar, choose **Clone**, next too**Update Schema**.</span></span> <span data-ttu-id="26b48-140">這個步驟是應用的必要 tookeep 只有當您想 hello 相同資源識別碼或要求觸發程序 URL 程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="26b48-140">This step is necessary only if you want tookeep hello same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="26b48-141">升級工具注意事項</span><span class="sxs-lookup"><span data-stu-id="26b48-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="26b48-142">對應條件</span><span class="sxs-lookup"><span data-stu-id="26b48-142">Mapping conditions</span></span>

<span data-ttu-id="26b48-143">在升級的 hello 定義 hello 工具會盡力在為範圍群組，則為 true 和 false 分支動作。</span><span class="sxs-lookup"><span data-stu-id="26b48-143">In hello upgraded definition, hello tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="26b48-144">具體來說，hello 設計工具模式`@equals(actions('a').status, 'Skipped')`應該會顯示為`else`動作。</span><span class="sxs-lookup"><span data-stu-id="26b48-144">Specifically, hello designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="26b48-145">不過，如果 hello 工具偵測到無法辨識的圖樣，hello 工具可能會建立 hello true 和 false 分支的 hello 不同的條件。</span><span class="sxs-lookup"><span data-stu-id="26b48-145">However, if hello tool detects unrecognizable patterns, hello tool might create separate conditions for both hello true and hello false branch.</span></span> <span data-ttu-id="26b48-146">如有必要，您可以在升級之後重新對應動作。</span><span class="sxs-lookup"><span data-stu-id="26b48-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="26b48-147">'foreach' 迴圈與條件</span><span class="sxs-lookup"><span data-stu-id="26b48-147">'foreach' loop with condition</span></span>

<span data-ttu-id="26b48-148">在 hello 新結構描述，您可以使用 hello 篩選器動作 tooreplicate hello 模式`foreach`迴圈的條件，每個項目，但當您升級時，應該會自動發生這項變更。</span><span class="sxs-lookup"><span data-stu-id="26b48-148">In hello new schema, you can use hello filter action tooreplicate hello pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="26b48-149">hello 條件變成之前傳回只符合 hello 條件的項目陣列 hello foreach 迴圈 」 篩選器動作，該陣列傳遞到 hello foreach 動作。</span><span class="sxs-lookup"><span data-stu-id="26b48-149">hello condition becomes a filter action before hello foreach loop for returning only an array of items that match hello condition, and that array is passed into hello foreach action.</span></span> <span data-ttu-id="26b48-150">如需範例，請參閱[迴圈和範圍](../logic-apps/logic-apps-loops-and-scopes.md)。</span><span class="sxs-lookup"><span data-stu-id="26b48-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="26b48-151">資源標籤</span><span class="sxs-lookup"><span data-stu-id="26b48-151">Resource tags</span></span>

<span data-ttu-id="26b48-152">在升級之後，會移除資源標記，因此您必須加以重設 hello 升級工作流程。</span><span class="sxs-lookup"><span data-stu-id="26b48-152">After you upgrade, resource tags are removed, so you must reset them for hello upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="26b48-153">其他變更</span><span class="sxs-lookup"><span data-stu-id="26b48-153">Other changes</span></span>

### <a name="renamed-manual-trigger-toorequest-trigger"></a><span data-ttu-id="26b48-154">重新命名 'manual' 觸發程序 too'request' 觸發程序</span><span class="sxs-lookup"><span data-stu-id="26b48-154">Renamed 'manual' trigger too'request' trigger</span></span>

<span data-ttu-id="26b48-155">hello`manual`觸發類型已被取代，重新命名太`request`類型`http`。</span><span class="sxs-lookup"><span data-stu-id="26b48-155">hello `manual` trigger type was deprecated and renamed too`request` with type `http`.</span></span> <span data-ttu-id="26b48-156">這項變更會建立 hello 種 hello 觸發程序的模式，則使用的 toobuild 較佳的一致性。</span><span class="sxs-lookup"><span data-stu-id="26b48-156">This change creates more consistency for hello kind of pattern that hello trigger is used toobuild.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="26b48-157">新的「篩選」動作</span><span class="sxs-lookup"><span data-stu-id="26b48-157">New 'filter' action</span></span>

<span data-ttu-id="26b48-158">toofilter 大型陣列向 tooa 組較小的項目，新 hello`filter`類型陣列和條件接受、 評估 hello 條件，針對每個項目，並傳回符合 hello 條件的項目陣列。</span><span class="sxs-lookup"><span data-stu-id="26b48-158">toofilter a large array down tooa smaller set of items, hello new `filter` type accepts an array and a condition, evaluates hello condition for each item, and returns an array with items meeting hello condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="26b48-159">'foreach' 和 'until' 動作限制</span><span class="sxs-lookup"><span data-stu-id="26b48-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="26b48-160">hello`foreach`和`until`迴圈會限制的 tooa 單一動作。</span><span class="sxs-lookup"><span data-stu-id="26b48-160">hello `foreach` and `until` loop are restricted tooa single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="26b48-161">動作的新 'trackedProperties'</span><span class="sxs-lookup"><span data-stu-id="26b48-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="26b48-162">動作現在可以有一個額外的屬性稱為`trackedProperties`，也就是同層級 toohello`runAfter`和`type`屬性。</span><span class="sxs-lookup"><span data-stu-id="26b48-162">Actions can now have an additional property called `trackedProperties`, which is sibling toohello `runAfter` and `type` properties.</span></span> <span data-ttu-id="26b48-163">此物件會指定特定動作的輸入或輸出的 tooinclude hello Azure 診斷遙測，發出工作流程中。</span><span class="sxs-lookup"><span data-stu-id="26b48-163">This object specifies certain action inputs or outputs that you want tooinclude in hello Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="26b48-164">例如：</span><span class="sxs-lookup"><span data-stu-id="26b48-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="26b48-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26b48-165">Next Steps</span></span>
* [<span data-ttu-id="26b48-166">建立邏輯應用程式的工作流程定義</span><span class="sxs-lookup"><span data-stu-id="26b48-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="26b48-167">建立 Logic Apps 的部署範本</span><span class="sxs-lookup"><span data-stu-id="26b48-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
