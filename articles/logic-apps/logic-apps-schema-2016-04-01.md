---
title: "June-1-2016 結構描述更新 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 43df04d6478e44c82c88b17d916cfc9fe4afc03e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="50c4e-103">Azure Logic Apps 的結構描述更新 - 2016 年 6 月 1 日</span><span class="sxs-lookup"><span data-stu-id="50c4e-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="50c4e-104">這個新的結構描述和 Azure Logic Apps 的 API 版本包含重要的改良功能，讓邏輯應用程式更可靠且更輕鬆地使用︰</span><span class="sxs-lookup"><span data-stu-id="50c4e-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="50c4e-105">[範圍](#scopes)可讓您建立動作的巢狀或群組做為動作集合。</span><span class="sxs-lookup"><span data-stu-id="50c4e-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="50c4e-106">[條件和迴圈](#conditions-loops)現在是第一級動作。</span><span class="sxs-lookup"><span data-stu-id="50c4e-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="50c4e-107">執行動作的更精確順序與 `runAfter` 屬性，取代 `dependsOn`</span><span class="sxs-lookup"><span data-stu-id="50c4e-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="50c4e-108">如需從 2015 年 8 月 1 日預覽結構描述的邏輯應用程式升級為 2016 年 6 月 1 日結構描述，[請查看升級章節](##upgrade-your-schema)。</span><span class="sxs-lookup"><span data-stu-id="50c4e-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="50c4e-109">範圍</span><span class="sxs-lookup"><span data-stu-id="50c4e-109">Scopes</span></span>

<span data-ttu-id="50c4e-110">這個結構描述包含可讓您將動作群組在一起或在彼此內巢狀動作的範圍。</span><span class="sxs-lookup"><span data-stu-id="50c4e-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="50c4e-111">例如，條件可包含另一個條件。</span><span class="sxs-lookup"><span data-stu-id="50c4e-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="50c4e-112">深入了解[範圍語法](../logic-apps/logic-apps-loops-and-scopes.md)，或檢閱此基本範圍範例︰</span><span class="sxs-lookup"><span data-stu-id="50c4e-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

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
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="50c4e-113">條件和迴圈的變更</span><span class="sxs-lookup"><span data-stu-id="50c4e-113">Conditions and loops changes</span></span>

<span data-ttu-id="50c4e-114">在舊版結構描述中，條件和迴圈是與單一動作相關聯的參數。</span><span class="sxs-lookup"><span data-stu-id="50c4e-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="50c4e-115">此結構描述拿起這項限制，因此條件和迴圈現在會顯示為動作類型。</span><span class="sxs-lookup"><span data-stu-id="50c4e-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="50c4e-116">深入了解[迴圈和範圍](../logic-apps/logic-apps-loops-and-scopes.md)，或檢閱此基本範例的條件動作︰</span><span class="sxs-lookup"><span data-stu-id="50c4e-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

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
## <a name="runafter-property"></a><span data-ttu-id="50c4e-117">'runAfter' 屬性</span><span class="sxs-lookup"><span data-stu-id="50c4e-117">'runAfter' property</span></span>

<span data-ttu-id="50c4e-118">`runAfter` 屬性會取代 `dependsOn`，當您根據先前動作的狀態指定動作的執行順序時提供更高的精確度。</span><span class="sxs-lookup"><span data-stu-id="50c4e-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span></span>

<span data-ttu-id="50c4e-119">無論您需要執行動作幾次，根據前一個動作是否成功、失敗或略過，`dependsOn` 屬性是「動作已執行並成功」的代名詞。</span><span class="sxs-lookup"><span data-stu-id="50c4e-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="50c4e-120">`runAfter` 屬性提供這樣的彈性，做為指定物件會在其後執行的所有動作名稱之物件。</span><span class="sxs-lookup"><span data-stu-id="50c4e-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span></span> <span data-ttu-id="50c4e-121">這個屬性也會定義可接受做為觸發程序狀態的陣列。</span><span class="sxs-lookup"><span data-stu-id="50c4e-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="50c4e-122">例如，如果您想要在步驟 A 成功後，且在步驟 B 成功或失敗之後執行，您建構此 `runAfter` 屬性︰</span><span class="sxs-lookup"><span data-stu-id="50c4e-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="50c4e-123">升級您的結構描述</span><span class="sxs-lookup"><span data-stu-id="50c4e-123">Upgrade your schema</span></span>

<span data-ttu-id="50c4e-124">升級為新的結構描述只需要幾個步驟。</span><span class="sxs-lookup"><span data-stu-id="50c4e-124">Upgrading to the new schema only takes a few steps.</span></span> <span data-ttu-id="50c4e-125">升級程序包含執行升級指令碼、儲存為新的邏輯應用程式，以及如果想要的話，可能會覆寫先前的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="50c4e-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span></span>

1. <span data-ttu-id="50c4e-126">在 Azure 入口網站中，開啟邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="50c4e-126">In the Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="50c4e-127">移至**概觀**。</span><span class="sxs-lookup"><span data-stu-id="50c4e-127">Go to **Overview**.</span></span> <span data-ttu-id="50c4e-128">在邏輯應用程式工具列上，選擇 [更新結構描述]。</span><span class="sxs-lookup"><span data-stu-id="50c4e-128">On the logic app toolbar, choose **Update Schema**.</span></span>
   
    ![選擇 [更新結構描述]][1]
   
    <span data-ttu-id="50c4e-130">會傳回升級的定義，您可以將其複製並貼到資源定義 (如有必要)。</span><span class="sxs-lookup"><span data-stu-id="50c4e-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="50c4e-131">不過，我們**強烈建議**您選擇 [另存新檔]，以確定所有連線參考在升級的邏輯應用程式中都有效。</span><span class="sxs-lookup"><span data-stu-id="50c4e-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span></span>

3. <span data-ttu-id="50c4e-132">在升級的刀鋒視窗工具列中，選擇 [另存新檔]。</span><span class="sxs-lookup"><span data-stu-id="50c4e-132">In the upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="50c4e-133">輸入邏輯名稱和狀態。</span><span class="sxs-lookup"><span data-stu-id="50c4e-133">Enter the logic name and status.</span></span> <span data-ttu-id="50c4e-134">若要部署已升級的邏輯應用程式，選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="50c4e-134">To deploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="50c4e-135">確認升級的邏輯應用程式如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="50c4e-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="50c4e-136">如果您要使用手動或要求觸發程序，新的邏輯應用程式中的回呼 URL 將會變更。</span><span class="sxs-lookup"><span data-stu-id="50c4e-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span></span> <span data-ttu-id="50c4e-137">測試新的 URL 以確定端對端經驗運作。</span><span class="sxs-lookup"><span data-stu-id="50c4e-137">Test the new URL to make sure the end-to-end experience works.</span></span> <span data-ttu-id="50c4e-138">若要保留先前的 URL，您可以在現有邏輯應用程式上複製。</span><span class="sxs-lookup"><span data-stu-id="50c4e-138">To preserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="50c4e-139">選擇性 若要使用新的結構描述版本覆寫先前的邏輯應用程式，請在工具列上選擇 [更新結構描述] 旁的 [複製]。</span><span class="sxs-lookup"><span data-stu-id="50c4e-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span></span> <span data-ttu-id="50c4e-140">如果您想要保留邏輯應用程式的相同資源識別碼，或要求觸發程序 URL，此步驟才有必要。</span><span class="sxs-lookup"><span data-stu-id="50c4e-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="50c4e-141">升級工具注意事項</span><span class="sxs-lookup"><span data-stu-id="50c4e-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="50c4e-142">對應條件</span><span class="sxs-lookup"><span data-stu-id="50c4e-142">Mapping conditions</span></span>

<span data-ttu-id="50c4e-143">在升級的定義中，此工具會盡力將 true 和 false 分支的動作一起分組在範圍內。</span><span class="sxs-lookup"><span data-stu-id="50c4e-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="50c4e-144">明確地說，`@equals(actions('a').status, 'Skipped')` 的設計工具模式應顯示為 `else` 動作。</span><span class="sxs-lookup"><span data-stu-id="50c4e-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="50c4e-145">不過，如果工具偵測到無法辨識的模式，則工具可能會為 true 和 false 分支建立不同的條件。</span><span class="sxs-lookup"><span data-stu-id="50c4e-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span></span> <span data-ttu-id="50c4e-146">如有必要，您可以在升級之後重新對應動作。</span><span class="sxs-lookup"><span data-stu-id="50c4e-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="50c4e-147">'foreach' 迴圈與條件</span><span class="sxs-lookup"><span data-stu-id="50c4e-147">'foreach' loop with condition</span></span>

<span data-ttu-id="50c4e-148">在新的結構描述中，您可以使用篩選器動作來針對每個項目複寫 `foreach` 迴圈與條件的模式，但當您升級時，這項變更應該會自動發生。</span><span class="sxs-lookup"><span data-stu-id="50c4e-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="50c4e-149">條件會在 foreach 迴圈之前變成篩選動作，以便只傳回符合條件的項目陣列，而且該陣列會傳遞至 foreach 動作。</span><span class="sxs-lookup"><span data-stu-id="50c4e-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span></span> <span data-ttu-id="50c4e-150">如需範例，請參閱[迴圈和範圍](../logic-apps/logic-apps-loops-and-scopes.md)。</span><span class="sxs-lookup"><span data-stu-id="50c4e-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="50c4e-151">資源標籤</span><span class="sxs-lookup"><span data-stu-id="50c4e-151">Resource tags</span></span>

<span data-ttu-id="50c4e-152">在升級之後，會移除資源標籤，因此您必須加以重設以升級工作流程。</span><span class="sxs-lookup"><span data-stu-id="50c4e-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="50c4e-153">其他變更</span><span class="sxs-lookup"><span data-stu-id="50c4e-153">Other changes</span></span>

### <a name="renamed-manual-trigger-to-request-trigger"></a><span data-ttu-id="50c4e-154">將 'manual' 觸發程序重新命名為 'request' 觸發程序</span><span class="sxs-lookup"><span data-stu-id="50c4e-154">Renamed 'manual' trigger to 'request' trigger</span></span>

<span data-ttu-id="50c4e-155">`manual` 觸發程序類型已被取代，並重新命名為 `request` 類型 `http`。</span><span class="sxs-lookup"><span data-stu-id="50c4e-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span></span> <span data-ttu-id="50c4e-156">這項變更會針對觸發程序用來建置的模式類型建立較佳的一致性。</span><span class="sxs-lookup"><span data-stu-id="50c4e-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="50c4e-157">新的「篩選」動作</span><span class="sxs-lookup"><span data-stu-id="50c4e-157">New 'filter' action</span></span>

<span data-ttu-id="50c4e-158">若要將大型陣列篩選至較少的項目集，新的 `filter` 類型會接受陣列和條件、評估每個項目的條件，並傳回具有符合條件之項目的陣列。</span><span class="sxs-lookup"><span data-stu-id="50c4e-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="50c4e-159">'foreach' 和 'until' 動作限制</span><span class="sxs-lookup"><span data-stu-id="50c4e-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="50c4e-160">`foreach` 和 `until` 迴圈僅限用於單一動作。</span><span class="sxs-lookup"><span data-stu-id="50c4e-160">The `foreach` and `until` loop are restricted to a single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="50c4e-161">動作的新 'trackedProperties'</span><span class="sxs-lookup"><span data-stu-id="50c4e-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="50c4e-162">動作現在可以有一個額外的屬性，稱為 `trackedProperties`，這是 `runAfter` 和 `type` 屬性的同層級。</span><span class="sxs-lookup"><span data-stu-id="50c4e-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span></span> <span data-ttu-id="50c4e-163">此物件會指定要包含在工作流程期間所發出的 Azure 診斷遙測之特定動作的輸入或輸出。</span><span class="sxs-lookup"><span data-stu-id="50c4e-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="50c4e-164">例如：</span><span class="sxs-lookup"><span data-stu-id="50c4e-164">For example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="50c4e-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50c4e-165">Next Steps</span></span>
* [<span data-ttu-id="50c4e-166">建立邏輯應用程式的工作流程定義</span><span class="sxs-lookup"><span data-stu-id="50c4e-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="50c4e-167">建立 Logic Apps 的部署範本</span><span class="sxs-lookup"><span data-stu-id="50c4e-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
