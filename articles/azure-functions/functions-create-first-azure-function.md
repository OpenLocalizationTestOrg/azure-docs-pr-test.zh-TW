---
title: "您的第一個函式從 hello Azure 入口網站的 aaaCreate |Microsoft 文件"
description: "深入了解如何使用無伺服器執行的函式的第一個 Azure toocreate hello Azure 入口網站。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>在 hello Azure 入口網站中建立您的第一個函式

Azure 的函式可讓您在無伺服器環境中執行您的程式碼，而不需要 toofirst 建立 VM，或發行 web 應用程式。 本主題中，了解如何 toouse 函式 toocreate hello Azure 入口網站中的"hello world"函式。

![在 hello Azure 入口網站中建立函式應用程式](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>登入 tooAzure

登入 toohello [Azure 入口網站](https://portal.azure.com/)。

## <a name="create-a-function-app"></a>建立函數應用程式

您必須擁有您的函式的函式應用程式 toohost hello 執行。 函式應用程式可讓您將多個函式群組為邏輯單位，以方便您管理、部署和共用資源。 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

接下來，您會在 hello 新函式應用程式中建立函式。

## <a name="create-function"></a>建立由 HTTP 觸發的函式

1. 展開新函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。

2.  在 hello**快速入門**頁面上，選取**WebHook + API**，**選擇的語言**函式，然後按一下**建立此函數**. 
   
    ![在 hello Azure 入口網站中的函式快速入門。](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

函式會建立在選擇 HTTP 觸發函式使用 hello 範本的語言。 您可以藉由傳送 HTTP 要求執行 hello 新函式。

## <a name="test-hello-function"></a>測試 hello 函式

1. 在新的函式中，按一下 </> 取得函式 URL，選取 預設 (函式索引鍵)，然後按一下複製。 

    ![複製 hello Azure 入口網站中的 hello 函式 URL](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. 貼入瀏覽器的網址列中的 hello 函式的 URL。 附加 hello 查詢字串`&name=<yourname>`toothis URL 和按 hello`Enter`您鍵盤 tooexecute hello 要求金鑰。 hello 以下是 hello 回應 hello Edge 瀏覽器中的 hello 函式所傳回的範例：

    ![函式回應 hello 瀏覽器中。](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    URL 包含索引鍵所需，根據預設，tooaccess hello 要求您透過 HTTP 的函式。   

3. 當您的函式執行時，追蹤資訊會寫入 toohello 記錄檔。 toosee hello 追蹤輸出，從上一個執行 hello，tooyour 函式傳回 hello 入口網站中，按一下向上箭號，在 hello 底部 hello 螢幕 tooexpand hello**記錄**。 

   ![函式會記錄檢視器中 hello Azure 入口網站。](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>清除資源

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>後續步驟

您已使用簡單的 HTTP 觸發函式建立了函式應用程式。  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

如需詳細資訊，請參閱 [Azure Functions HTTP 和 webhook 繫結](functions-bindings-http-webhook.md)。



