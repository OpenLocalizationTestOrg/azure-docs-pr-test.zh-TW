---
title: "在 Azure 中建立會按照排程來執行的函式 | Microsoft Docs"
description: "了解如何在 Azure 中建立函式，並使其按照您定義的排程來執行。"
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
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>在 Azure 中建立由計時器觸發的函式

了解如何使用 Azure Functions 來建立函式，並使其按照您定義的排程來執行。

![在 Azure 入口網站中建立函式應用程式](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>必要條件

若要完成本教學課程：

+ 如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>建立 Azure 函數應用程式

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

接下來，您要在新的函式應用程式中建立函式。

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>建立由計時器觸發的函式

1. 展開函式應用程式，然後按一下 [Functions] 旁的 [+] 按鈕。 如果這是您函式應用程式中的第一個函式，請選取 [自訂函式]。 這會顯示一組完整的函式範本。

    ![Azure 入口網站中的 Functions 快速入門](./media/functions-create-scheduled-function/add-first-function.png)

2. 針對所需語言選取 **TimerTrigger** 的範本。 然後使用表格中所指定的設定︰

    ![在 Azure 入口網站中建立計時器觸發函式。](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | 設定 | 建議的值 | 說明 |
    |---|---|---|
    | **函式命名** | TimerTriggerCSharp1 | 定義計時器觸發函式的名稱。 |
    | **[排程](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | 含有六個欄位的 [CRON 運算式](http://en.wikipedia.org/wiki/Cron#CRON_expression)，它會將函式排程為每分鐘執行一次。 |

2. 按一下 [建立] 。 系統隨即會以您所選的語言建立函式，並讓它每分鐘執行一次。

3. 檢視寫入到記錄的追蹤資訊以確認執行情形。

    ![Azure 入口網站中的函式記錄檢視器。](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

現在，您可以變更函式的排程，使其降低執行頻率，例如降低為每小時一次。 

## <a name="update-the-timer-schedule"></a>更新計時器排程

1. 展開您的函式，然後按一下 [整合]。 您可以在這裡定義函式的輸入和輸出繫結，以及設定排程。 

2. 輸入 `0 0 */1 * * *` 作為新的 [排程] 值，然後按一下 [儲存]。  

![函式便會在 Azure 入口網站中更新計時器排程。](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

您現在已擁有每小時執行一次的函式。 

## <a name="clean-up-resources"></a>清除資源

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>後續步驟

您已建立會根據排程來執行的函式。

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

如需計時器觸發程序的詳細資訊，請參閱[使用 Azure Functions 排程程式碼執行](functions-bindings-timer.md)。