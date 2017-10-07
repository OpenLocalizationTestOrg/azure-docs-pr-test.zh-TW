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
# <a name="use-logic-apps-features"></a>使用 Logic Apps 功能

在[前面的主題](../logic-apps/logic-apps-create-a-logic-app.md)中，您已建立第一個邏輯應用程式。 toocontrol 邏輯應用程式的工作流程，您可以為您的邏輯應用程式 toorun 指定不同的路徑，並太如何處理陣列、 集合和批次中的資料。 您可以將下列元素包含在邏輯應用程式的工作流程中：

* 條件和 [Switch 陳述式](../logic-apps/logic-apps-switch-case.md)可讓邏輯應用程式根據符合的特定條件來執行不同動作。

* [迴圈](../logic-apps/logic-apps-loops-and-scopes.md)可讓邏輯應用程式重複執行步驟。 例如，使用 **For_each** 迴圈時，可以對陣列重複動作。 或者使用 **Until** 迴圈，可以在符合條件之後重複動作。

* [範圍](../logic-apps/logic-apps-loops-and-scopes.md)可讓您一系列動作組成群組，例如 tooimplement 例外狀況處理。

* [解除批次處理即將](../logic-apps/logic-apps-loops-and-scopes.md)可讓您邏輯的應用程式啟動個別的工作流程項目的陣列中，當您使用 hello **SplitOn**命令。

本主題將介紹建置邏輯應用程式的其他概念：

* 程式碼檢視 tooedit 現有邏輯應用程式
* 啟動工作流程的選項

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>條件：只有在符合條件後才執行步驟

toohave 邏輯應用程式資料符合特定準則時，才執行的步驟，您可以加入條件比較 hello 針對特定欄位或值的工作流程中的資料。

例如，假設您的邏輯應用程式傳送過多的網站 RSS 摘要文章的電子郵件給您。 您可以加入條件，讓應用程式邏輯 hello 新文章時，才會傳送電子郵件所屬 tooa 特定類別。

1. 在 [hello [Azure 入口網站](https://portal.azure.com)、 尋找和開啟邏輯應用程式邏輯應用程式的設計工具中。

2. 新增您想要的條件 toohello 工作流程的位置。 

   hello 邏輯應用程式工作流程中的現有步驟之間 tooadd hello 條件 hello 指標移 hello 箭號想 tooadd hello 條件。 
   選擇 hello**加號**(**+**)，然後選擇 [**加入條件**。 例如：

   ![新增條件 toologic 應用程式](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > 如果您想 tooadd 條件在您目前的工作流程的 hello 結尾處，移 toohello 應用程式邏輯，底部，然後選擇**+ 新增步驟**。

3. 現在定義 hello 條件。 指定您想 tooevaluate、 hello 作業 tooperform，和 hello 目標值或欄位的 hello 來源欄位。 tooadd 現有欄位 tooyour 條件從 hello 選擇**動態內容清單中新增**。

   例如：

   ![在基本模式中編輯條件](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   以下是 hello 完成的條件：

   ![完整條件](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > toodefine hello 條件，程式碼中，選擇**在進階模式中編輯**。 例如：
   > 
   > ![在程式碼中編輯條件](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. 在下**是如果**和**如果否**，新增 hello 步驟 tooperform 根據是否滿足 hello 的條件。

   例如：

   ![具 YES 和 NO 路徑的條件](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > 您可以將現有的動作拖曳到 hello**是如果**和**IF NO**路徑。

5. 完成後，儲存邏輯應用程式。

現在 hello 文章符合條件時，才收到電子郵件。

## <a name="repeat-actions-over-a-list-with-foreach"></a>使用 forEach 對清單重複執行動作

hello forEach 迴圈會透過指定陣列 toorepeat 動作。 如果不是陣列，hello 流程將會失敗。 比方說，如果您有 action1，輸出陣列的訊息，而且您想 toosend 每則訊息，您可以將動作的 hello 屬性中包含這個 forEach 陳述式：`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>編輯 hello 邏輯應用程式的程式碼定義

雖然您擁有 hello 邏輯應用程式的設計工具，您可以直接編輯定義邏輯應用程式的 hello 程式碼。

1. 在 [hello] 命令列上選擇 [**程式碼檢視**。

    完整的編輯器隨即開啟，並顯示 hello 定義您編輯過。

    ![程式碼檢視](media/logic-apps-use-logic-app-features/codeview.png)

    Hello 文字編輯器中，您可以複製並貼上任何數目的 hello 內的動作相同邏輯應用程式或邏輯應用程式之間。 
    您也可以輕鬆地新增或移除 hello 定義的整個區段，您也可以與其他人共用定義。

2. 編輯，選擇 [toosave**儲存**。

## <a name="parameters"></a>參數

某些 Logic Apps 功能只能在程式碼檢視中取得，例如參數。 參數可讓您輕鬆 tooreuse 整個邏輯應用程式中的值。 例如，如果您想要在數個動作中使用同一個電子郵件地址，您應將該電子郵件地址定義為參數。

參數雖然適合拉出，您很可能 toochange 的值。 當您需要在不同環境 toooverride 參數時，它們時特別有用。 如何 toooverride 參數根據環境中，請參閱的 toolearn[撰寫邏輯應用程式定義](../logic-apps/logic-apps-author-definitions.md)和[REST API 文件](https://docs.microsoft.com/rest/api/logic)。

這個範例會示範如何 tooupdate 您現有的邏輯應用程式，以便您可以將參數用於 hello 查詢詞彙。

1. 在程式碼檢視中，找出 hello`parameters : {}`物件，並加入`currentFeedUrl`物件：

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. 移 toohello`When_a_feed-item_is_published`動作、 尋找 hello`queries`區段，並取代 hello 查詢值為：`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin 兩個或多個字串，您也可以使用 hello`concat`函式。 
    例如， `"@concat('#',parameters('currentFeedUrl'))"` works hello 相同為上述的 hello。

3.  完成之後，請選擇 [儲存]。 

    現在您可以變更 hello 網站的 RSS 摘要藉由傳遞不同的 URL，透過 hello`currentFeedURL`物件。

深入了解[如何 tooauthor 邏輯應用程式定義](../logic-apps/logic-apps-author-definitions.md)。

## <a name="start-logic-app-workflows"></a>啟動邏輯應用程式工作流程

您有不同的選項啟動應用程式邏輯中所定義的 hello 工作流程。 您一律可以啟動工作流程隨 hello [Azure 入口網站]。

### <a name="recurrence-triggers"></a>循環觸發程序

循環觸發程序會依照您指定的間隔執行。 當 hello 觸發程序具有條件式邏輯時，hello 觸發程序會判斷 hello 工作流程是否需要 toorun。 觸發程序指出 hello 工作流程應執行藉由傳回`200`狀態碼。 當 hello 工作流程不需要 toorun 時，hello 觸發程序傳回`202`狀態碼。

### <a name="callback-using-rest-apis"></a>使用 REST API 回呼

toostart 工作流程，服務可以呼叫邏輯應用程式端點。 這種邏輯應用程式依需求，選擇 [toostart**立即執行**hello 命令列上。 請參閱[呼叫邏輯應用程式端點做為觸發程序來啟動工作流程](../logic-apps/logic-apps-http-endpoint.md)。 

<!-- Shared links -->
[Azure 入口網站]: https://portal.azure.com

## <a name="next-steps"></a>後續步驟

* [Switch 陳述式](../logic-apps/logic-apps-switch-case.md) 
* [迴圈、範圍和解除批次處理](../logic-apps/logic-apps-loops-and-scopes.md)
* [撰寫邏輯應用程式定義](../logic-apps/logic-apps-author-definitions.md)