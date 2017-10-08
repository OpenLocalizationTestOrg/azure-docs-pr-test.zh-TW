---
title: "在 Azure 中的排程執行的函式 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate azure 中執行的函式根據您定義的排程。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>在 Azure 中建立由計時器觸發的函式

了解如何 toouse Azure 函式 toocreate 執行的函式以您定義的排程。

![在 hello Azure 入口網站中建立函式應用程式](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

+ 如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>建立 Azure 函數應用程式

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

接下來，您會在 hello 新函式應用程式中建立函式。

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>建立由計時器觸發的函式

1. 展開您的函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。 如果 hello 函式應用程式中的第一個函式，請選取**自訂函式**。 這會顯示 hello 組完整的函式樣板。

    ![在 Azure 入口網站的 hello 函式 [快速入門] 頁面](./media/functions-create-scheduled-function/add-first-function.png)

2. 選取 hello **TimerTrigger**所需語言的範本。 然後使用 hello 資料表中所指定的 hello 設定：

    ![Hello Azure 入口網站中建立計時器觸發函式。](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | 設定 | 建議的值 | 說明 |
    |---|---|---|
    | **函式命名** | TimerTriggerCSharp1 | 定義 hello 計時器觸發函式的名稱。 |
    | **[排程](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | 六個欄位[CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)，它會排程函式 toorun 每隔一分鐘。 |

2. 按一下 [建立] 。 系統隨即會以您所選的語言建立函式，並讓它每分鐘執行一次。

3. 藉由檢視追蹤資訊寫入 toohello 記錄檔，請確認執行。

    ![函式會記錄檢視器中 hello Azure 入口網站。](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

現在，您可以變更 hello 函式的排程，使其執行較少，例如每個小時一次。 

## <a name="update-hello-timer-schedule"></a>更新 hello 計時器排程

1. 展開您的函式，然後按一下 [整合]。 這是定義輸入和輸出繫結您的函式和也設定 hello 排程位置。 

2. 輸入 `0 0 */1 * * *` 作為新的 排程 值，然後按一下儲存。  

![函式會更新計時器 hello Azure 入口網站中的排程。](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

您現在已擁有每小時執行一次的函式。 

## <a name="clean-up-resources"></a>清除資源

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>後續步驟

您已建立會根據排程來執行的函式。

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

如需計時器觸發程序的詳細資訊，請參閱[使用 Azure Functions 排程程式碼執行](functions-bindings-timer.md)。