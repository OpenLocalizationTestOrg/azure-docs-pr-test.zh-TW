---
title: "在 Azure 佇列訊息所觸發的函式 aaaCreate |Microsoft 文件"
description: "使用 Azure 函式 toocreate 無伺服器的函式會叫用的訊息提交 tooan Azure 儲存體佇列。"
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a>新增訊息 tooan Azure 儲存體佇列函式的使用

在 Azure 功能中，輸入和輸出繫結會提供從您的函式宣告的方式來 tooconnect tooexternal 服務資料。 本主題中，了解如何 tooupdate 現有的函式所加入的繫結的輸出會傳送訊息 tooAzure 佇列儲存體。  

![Hello 記錄檔中檢視訊息。](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>必要條件 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* 安裝 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。

## <a name="add-binding"></a>新增輸出繫結
 
1. 展開函式應用程式和函式。

2. 選取 [整合] 和 [+ 新輸出]，然後選擇 [Azure 佇列儲存體] 和 [選取]。
    
    ![在 hello Azure 入口網站中加入佇列儲存體輸出繫結 tooa 函式。](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. 使用 hello hello 資料表中所指定的設定： 

    ![在 hello Azure 入口網站中加入佇列儲存體輸出繫結 tooa 函式。](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | 設定      |  建議的值   | 說明                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **佇列名稱**   | myqueue-items    | hello hello 名稱佇列 tooconnect tooin 儲存體帳戶。 |
    | **儲存體帳戶連線** | AzureWebJobStorage | 您可以使用應用程式的函式，已經使用 hello 儲存體帳戶連接或另外新建一個。  |
    | **訊息參數名稱** | outputQueueItem | hello hello 輸出繫結參數的名稱。 | 

4. 按一下**儲存**tooadd hello 繫結。
 
既然您已定義的輸出繫結時，您會需要 tooupdate hello 程式碼 toouse hello 繫結 tooadd 訊息 tooa 佇列。  

## <a name="update-hello-function-code"></a>更新 hello 函式程式碼

1. 在 hello 編輯器中選取您函式 toodisplay hello 函式的程式碼。 

2. 對於 C# 函式，更新您的函式定義，如下所示 tooadd hello **outputQueueItem**儲存繫結參數。 若為 JavaScript 函式，請略過此步驟。

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. 新增 hello hello 方法會傳回之前，下列程式碼 toohello 函式。 使用 hello 適當的程式碼片段函式的 hello 語言。

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. 選取**儲存**toosave 變更。

訊息佇列中的加入的 toohello 隨附 hello 值傳遞 toohello HTTP 觸發程序。
 
## <a name="test-hello-function"></a>測試 hello 函式 

1. 儲存 hello 程式碼變更之後，請選取**執行**。 

    ![在 hello Azure 入口網站中加入佇列儲存體輸出繫結 tooa 函式。](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. 請檢查記錄檔 hello toomake，確定 hello 函式成功。 名為的新佇列**outqueue** hello 第一次使用函式執行階段 hello 輸出繫結時所建立儲存體帳戶。

接下來，您可以連接 tooyour 儲存體帳戶 tooverify hello 新佇列和加入 tooit 的 hello 訊息。 

## <a name="connect-toohello-queue"></a>連接 toohello 佇列

如果您已安裝存放裝置總管並連接 tooyour 儲存體帳戶，略過 hello 前三個步驟。    

1. 在您的函式中，選擇 **整合**和新的 hello **Azure 佇列儲存體**輸出繫結，然後展開**文件**。 複製**帳戶名稱**和**帳戶金鑰**。 您使用這些認證 tooconnect toohello 儲存體帳戶。
 
    ![收到 hello 儲存體帳戶的連接認證。](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. 執行 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)工具、 選取 hello 連接 hello 左邊的圖示，請選擇**使用儲存體帳戶名稱和金鑰**，然後選取**下一步**。

    ![執行 hello 儲存體帳戶總管工具。](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. 貼上 hello**帳戶名稱**和**帳戶金鑰**從步驟 1 到其對應的欄位，然後選取 **下一步**，和**連接**。 
  
    ![貼上 hello 儲存體認證和連接。](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. 依序展開 hello 附加儲存體帳戶**佇列**並確認佇列名為**myqueue 項目**存在。 您也應該看到已經 hello 佇列中的訊息。  
 
    ![建立儲存體佇列。](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>清除資源

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>後續步驟

您已加入的輸出繫結 tooan 現有函式。 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

如需繫結 tooQueue 儲存體的詳細資訊，請參閱[Azure 函式儲存體佇列繫結](functions-bindings-storage-queue.md)。 



