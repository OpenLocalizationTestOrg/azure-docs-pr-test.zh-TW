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
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Azure Logic Apps 的結構描述更新 - 2016 年 6 月 1 日

這個新的結構描述和 API 版本 Azure 邏輯應用程式包含多個製作邏輯應用程式的重要改良 toouse 可靠且更容易：

* [範圍](#scopes)可讓您建立動作的巢狀或群組做為動作集合。
* [條件和迴圈](#conditions-loops)現在是第一級動作。
* 更精確的順序執行動作以 hello`runAfter`屬性，取代`dependsOn`

從您的 logic apps hello 2015 年 8 月 1 日的 tooupgrade 預覽結構描述 toohello 2016 年 6 月 1 日的結構描述，[簽出 hello 升級] 區段](##upgrade-your-schema)。

<a name="scopes"></a>
## <a name="scopes"></a>範圍

這個結構描述包含可讓您將動作群組在一起或在彼此內巢狀動作的範圍。 例如，條件可包含另一個條件。 深入了解[範圍語法](../logic-apps/logic-apps-loops-and-scopes.md)，或檢閱此基本範圍範例︰

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
## <a name="conditions-and-loops-changes"></a>條件和迴圈的變更

在舊版結構描述中，條件和迴圈是與單一動作相關聯的參數。 此結構描述拿起這項限制，因此條件和迴圈現在會顯示為動作類型。 深入了解[迴圈和範圍](../logic-apps/logic-apps-loops-and-scopes.md)，或檢閱此基本範例的條件動作︰

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
## <a name="runafter-property"></a>'runAfter' 屬性

hello`runAfter`屬性取代`dependsOn`、 提供更多有效位數，當您指定動作的 hello 執行順序是根據 hello 狀態的上一個動作。

hello`dependsOn`屬性為 「 hello 動作執行和已順利完成 」 的同義詞，無論多少次想 tooexecute 動作，根據是否成功，hello 上一個動作失敗，或略過。 hello`runAfter`屬性提供該物件，指定所有 hello 之後 hello 物件會執行的動作名稱為的彈性。 這個屬性也會定義可接受做為觸發程序狀態的陣列。 例如，如果您想 toorun 步驟的成功，並也之後步驟 B 成功或失敗之後，您建構這個`runAfter`屬性：

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>升級您的結構描述

升級 toohello 新的結構描述只需要幾個步驟。 hello 升級程序包含執行 hello 升級指令碼，將儲存為新的邏輯應用程式，和如果想要的話，可能會覆寫 hello 先前邏輯應用程式。

1. 在 [hello Azure 入口網站，開啟邏輯應用程式。

2. 跳過**概觀**。 Hello 邏輯應用程式工具列上，選擇**更新結構描述**。
   
    ![選擇 [更新結構描述]][1]
   
    hello 升級的定義傳回時，您可以複製並貼到資源定義，如有必要的。 
    不過，我們**強烈建議**您選擇**存**toomake 確定所有連接參考都是有效 hello 中升級邏輯應用程式。

3. 在 [hello 升級刀鋒視窗的工具列上，選擇 [**存**。

4. 輸入 hello 邏輯名稱和狀態。 toodeploy 升級的邏輯應用程式，然後選擇 [**建立**。

5. 確認升級的邏輯應用程式如預期般運作。
   
   > [!NOTE]
   > 如果您使用手動或要求的觸發程序，hello 回呼 URL 會變更在新的邏輯應用程式中。 測試 hello 新 URL toomake 確定 hello 端對端體驗運作。 toopreserve 前一個 Url，您可以複製現有的邏輯應用程式透過。

6. *選擇性*toooverwrite 先前邏輯應用程式與 hello 新結構描述版本，在 [hello] 工具列上選擇**複製**、 下一步太**更新結構描述**。 這個步驟是應用的必要 tookeep 只有當您想 hello 相同資源識別碼或要求觸發程序 URL 程式邏輯。

### <a name="upgrade-tool-notes"></a>升級工具注意事項

#### <a name="mapping-conditions"></a>對應條件

在升級的 hello 定義 hello 工具會盡力在為範圍群組，則為 true 和 false 分支動作。 具體來說，hello 設計工具模式`@equals(actions('a').status, 'Skipped')`應該會顯示為`else`動作。 不過，如果 hello 工具偵測到無法辨識的圖樣，hello 工具可能會建立 hello true 和 false 分支的 hello 不同的條件。 如有必要，您可以在升級之後重新對應動作。

#### <a name="foreach-loop-with-condition"></a>'foreach' 迴圈與條件

在 hello 新結構描述，您可以使用 hello 篩選器動作 tooreplicate hello 模式`foreach`迴圈的條件，每個項目，但當您升級時，應該會自動發生這項變更。 hello 條件變成之前傳回只符合 hello 條件的項目陣列 hello foreach 迴圈 」 篩選器動作，該陣列傳遞到 hello foreach 動作。 如需範例，請參閱[迴圈和範圍](../logic-apps/logic-apps-loops-and-scopes.md)。

#### <a name="resource-tags"></a>資源標籤

在升級之後，會移除資源標記，因此您必須加以重設 hello 升級工作流程。

## <a name="other-changes"></a>其他變更

### <a name="renamed-manual-trigger-toorequest-trigger"></a>重新命名 'manual' 觸發程序 too'request' 觸發程序

hello`manual`觸發類型已被取代，重新命名太`request`類型`http`。 這項變更會建立 hello 種 hello 觸發程序的模式，則使用的 toobuild 較佳的一致性。

### <a name="new-filter-action"></a>新的「篩選」動作

toofilter 大型陣列向 tooa 組較小的項目，新 hello`filter`類型陣列和條件接受、 評估 hello 條件，針對每個項目，並傳回符合 hello 條件的項目陣列。

### <a name="restrictions-for-foreach-and-until-actions"></a>'foreach' 和 'until' 動作限制

hello`foreach`和`until`迴圈會限制的 tooa 單一動作。

### <a name="new-trackedproperties-for-actions"></a>動作的新 'trackedProperties'

動作現在可以有一個額外的屬性稱為`trackedProperties`，也就是同層級 toohello`runAfter`和`type`屬性。 此物件會指定特定動作的輸入或輸出的 tooinclude hello Azure 診斷遙測，發出工作流程中。 例如：

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

## <a name="next-steps"></a>後續步驟
* [建立邏輯應用程式的工作流程定義](../logic-apps/logic-apps-author-definitions.md)
* [建立 Logic Apps 的部署範本](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
