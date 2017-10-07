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
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>使用 Switch 陳述式在邏輯應用程式中執行不同動作

當撰寫工作流程，您通常需要 tootake 根據 hello 物件或運算式的值不同的動作。 例如，您可以根據 hello 狀態碼的 HTTP 要求，您的邏輯應用程式 toobehave 或電子郵件中所選取的選項。

您可以使用 switch 陳述式 tooimplement 這些案例。 邏輯應用程式可以評估語彙基元或運算式，並選擇以 hello hello 案例相同的值 tooexecute hello 指定動作。 只有其中一種情況應該符合 hello switch 陳述式。

> [!TIP]
> 如同所有的程式設計語言，Switch 陳述式僅支援等號比較運算子。 如果您需要其他關係運算子 (例如，「大於」)，請使用條件陳述式。
> tooensure 具決定性的執行行為，情況下都必須包含唯一且靜態的值，而不是動態的語彙基元或運算式。

## <a name="prerequisites"></a>必要條件

- 有效的 Azure 訂用帳戶。 如果您沒有作用中 Azure 訂用帳戶，[請建立免費帳戶](https://azure.microsoft.com/free/)，或免費嘗試 [Logic Apps](https://tryappservice.azure.com/)。
- [邏輯應用程式基本知識](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>加入參數的陳述式 tooyour 工作流程

tooshow switch 陳述式的運作方式，此範例會建立監視的檔案上傳 tooDropbox 邏輯應用程式。 Hello 邏輯應用程式時 hello 新檔案上傳時，傳送電子郵件 tooan 核准者選擇是否 tootransfer 那些檔案 tooSharePoint。 hello 應用程式會使用 switch 陳述式，會執行不同動作根據 hello 值 hello 核准者選取。

1. 建立邏輯應用程式，並選取觸發程序：**Dropbox - 建立檔案時**。

   ![使用 Dropbox - 建立檔案時觸發程序](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. 在 hello 觸發程序，新增這項動作： **Outlook.com-傳送核准電子郵件**

   > [!TIP]
   > 邏輯應用程式也支援從 Office 365 Outlook 帳戶傳送核准電子郵件案例。

   - 如果您沒有現有的連接，則會提示您 toocreate 其中一個。
   - 填寫 hello 必要欄位。 例如，在**至**，指定用於傳送嗨核准者電子郵件的 hello 電子郵件地址。
   - 在 [使用者選項] 下，輸入 `Approve, Reject`。

   ![設定連線](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. 新增 Switch 陳述式。

   - 選取 [+ 新步驟] > ...更多 > [新增 Switch 案例]。 
   - 現在我們想要根據 hello tooselect hello 動作 tooperform`SelectedOptions`輸出 hello*傳送核准電子郵件*動作。 
   您可以找到此欄位在 hello**加入動態內容**選取器。
   - 使用*案例 1* toohandle 當 hello 核准者選取`Approve`。
     - 如果核准，將複製 hello 原始檔 tooSharePoint 線上以 hello [ **SharePoint Online-建立檔案**動作](../connectors/connectors-create-api-sharepointonline.md)。
     - 加入另一個新的檔案是在 SharePoint 上可用的 hello 案例 toonotify 使用者動作。
   - 當使用者選取時，加入另一個案例 toohandle `Reject`。
     - 如果拒絕，傳送通知電子郵件通知其他核准者 hello 檔案會被拒絕，並不需要任何進一步的動作。
   - `SelectedOptions`只有兩個選項，讓我們可以保留 hello**預設**空白的案例。

   ![Switch 陳述式](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Switch 陳述式必須至少一個加法 toohello 預設案例中的案例。

4. Hello switch 陳述式之後, 刪除原始上傳檔案 tooDropbox hello 加入這項動作： **Dropbox-刪除檔案**

5. 儲存您的邏輯應用程式。 上傳檔案 tooDropbox 來測試您的應用程式。 您應該很快就會收到核准電子郵件。 選取選項，並觀察 hello 行為。

   > [!TIP]
   > 如何查看太[監視您的 logic apps](logic-apps-monitor-your-logic-apps.md)。

## <a name="understand-hello-code-behind-switch-statements"></a>了解 hello switch 陳述式後面的程式碼

既然您已成功建立使用 switch 陳述式的邏輯應用程式，讓我們看看 hello hello switch 陳述式後面的程式碼定義。

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

* `"Switch"`這是 hello hello switch 陳述式，您可以針對可讀性重新命名的名稱。 
* `"type": "Switch"`指出 hello 動作是在 switch 陳述式。 
* `"expression"`是 hello 核准者選取的選項，在此範例中，而且會評估針對宣告稍後在 hello 定義每個案例。 
* `"cases"` 可以包含任意數目的案例。 每個案例中，`"Case *"`是 hello hello 的情況下，您可以針對可讀性重新命名預設名稱。 
`"case"`指定 hello case 標籤 hello 參數運算式使用的比較，而且必須是常數且唯一的值。 如果沒有的 hello 案例符合 hello switch 運算式，在動作`"default"`會執行。

## <a name="get-help"></a>取得說明

tooask 問題、 解答的問題，以及執行其他 Azure 邏輯應用程式使用者，請參閱瀏覽 hello [Azure 邏輯應用程式論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)。

toohelp 改善 Azure 邏輯應用程式和連接器、 票選或送出意見在 hello [Azure 邏輯應用程式使用者意見反應網站](http://aka.ms/logicapps-wish)。

## <a name="next-steps"></a>後續步驟

- 了解如何太[新增條件](logic-apps-use-logic-app-features.md)
- 了解[錯誤和例外狀況處理](logic-apps-exception-handling.md)
- 深入探討[工作流程語言功能](logic-apps-author-definitions.md)