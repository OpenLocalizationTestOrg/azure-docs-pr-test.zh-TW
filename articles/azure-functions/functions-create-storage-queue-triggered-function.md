---
title: "在 Azure 佇列訊息所觸發的函式 aaaCreate |Microsoft 文件"
description: "使用 Azure 函式 toocreate 無伺服器的函式會叫用的訊息提交 tooan Azure 儲存體佇列。"
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>建立 Azure 佇列儲存體所觸發的函式

了解如何 toocreate 郵件時所觸發的函式提交 tooan Azure 儲存體佇列。

![Hello 記錄檔中檢視訊息。](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>必要條件

- 下載並安裝 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。

- Azure 訂用帳戶。 如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>建立 Azure 函數應用程式

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

接下來，您會在 hello 新函式應用程式中建立函式。

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>建立由佇列觸發的函式

1. 展開您的函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。 如果 hello 函式應用程式中的第一個函式，請選取**自訂函式**。 這會顯示 hello 組完整的函式樣板。

    ![在 Azure 入口網站的 hello 函式 [快速入門] 頁面](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. 選取 hello **QueueTrigger**您想要的語言，以及使用 hello 類似設定 hello 表中所指定的範本。

    ![建立 hello 儲存觸發佇列函式。](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | 設定 | 建議的值 | 說明 |
    |---|---|---|
    | **佇列名稱**   | myqueue-items    | 名稱的 hello 佇列 tooconnect tooin 儲存體帳戶。 |
    | **儲存體帳戶連線** | AzureWebJobStorage | 您可以使用應用程式的函式，已經使用 hello 儲存體帳戶連接或另外新建一個。  |
    | **函式命名** | 函式應用程式中的唯一名稱 | 這個由佇列所觸發之函式的名稱。 |

3. 按一下**建立**toocreate 您的函式。

接下來，您連接 tooyour Azure 儲存體帳戶，並建立 hello **myqueue 項目**儲存體佇列。

## <a name="create-hello-queue"></a>建立 hello 佇列

1. 在您的函式中，按一下 [整合]，展開 [文件]，然後複製**帳戶名稱**和**帳戶金鑰**。 您使用這些認證 tooconnect toohello 儲存體帳戶。 如果您已連接儲存體帳戶，略過 toostep 4。

    ![收到 hello 儲存體帳戶的連接認證。](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. 執行 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)工具，請按一下 hello 連接 hello 左邊的圖示，請選擇**使用儲存體帳戶名稱和金鑰**，然後按一下**下一步**。

    ![執行 hello 儲存體帳戶總管工具。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. 輸入 hello**帳戶名稱**和**帳戶金鑰**從步驟 1 中，按一下 **下一步**然後**連接**。

    ![輸入 hello 儲存體認證和連接。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. 展開 hello 附加儲存體帳戶，以滑鼠右鍵按一下**佇列**，按一下 **建立佇列**，型別`myqueue-items`，然後按下 enter。

    ![建立儲存體佇列。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

您已經有儲存體佇列，您可以藉由新增訊息 toohello 佇列測試 hello 函式。

## <a name="test-hello-function"></a>測試 hello 函式

1. 在 hello Azure 入口網站，瀏覽 tooyour 函式展開 hello**記錄**底部 hello hello 頁面，並確定該記錄檔資料流不已暫停。

1. 在儲存體總管中，依序展開您的儲存體帳戶、[佇列] 和 [myqueue-items]，然後按一下 [新增訊息]。

    ![新增訊息 toohello 佇列。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. 將您的 "Hello World!" 輸入 在 [訊息文字] 訊息中，然後按一下 [確定]。

1. 等候數秒鐘，然後返回 tooyour 函數記錄檔並確認已從 hello 佇列讀取該 hello 新訊息。

    ![Hello 記錄檔中檢視訊息。](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. 在 儲存體總管 中，按一下 **重新整理**並確認該 hello 訊息已處理，而且已不存在於 hello 佇列。

## <a name="clean-up-resources"></a>清除資源

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>後續步驟

您已建立執行時加入 tooa 儲存體佇列訊息的函式。

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

如需佇列儲存體觸發程序的詳細資訊，請參閱 [Azure Functions 儲存體佇列繫結](functions-bindings-storage-queue.md)。