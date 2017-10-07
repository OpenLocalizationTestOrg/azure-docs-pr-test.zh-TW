---
title: "aaaCreate GitHub webhook 所觸發的 Azure 中的函式 |Microsoft 文件"
description: "使用 Azure 函式 toocreate GitHub webhook 所叫用的無伺服器函式。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>建立由 GitHub Webhook 所觸發的函式

深入了解如何 toocreate webhook GitHub 特定裝載與 HTTP 要求所觸發的函式。

![Github Webhook 觸發 hello Azure 入口網站中的函式](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>必要條件

+ 一個 GitHub 帳戶至少要有一個專案。
+ Azure 訂用帳戶。 如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>建立 Azure 函數應用程式

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

接下來，您會在 hello 新函式應用程式中建立函式。

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>建立 GitHub webhook 觸發函式

1. 展開您的函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。 如果 hello 函式應用程式中的第一個函式，請選取**自訂函式**。 這會顯示 hello 組完整的函式樣板。

    ![在 Azure 入口網站的 hello 函式 [快速入門] 頁面](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. 選取 hello **GitHub WebHook**所需語言的範本。 **為您的函式命名**，然後選取 [建立]。

     ![在 hello Azure 入口網站中建立 GitHub webhook 觸發函式](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. 在新的函數中，按一下  **<> / Get 函式 URL**，然後複製並儲存 hello 值。 請勿 hello 相同的動作，如**<> / 取得 GitHub 密碼**。 您可以使用這些值 tooconfigure hello webhook GitHub 中。

    ![檢閱 hello 函式程式碼](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

接下來，您會在 GitHub 存放庫中建立 Webhook。

## <a name="configure-hello-webhook"></a>設定 hello webhook

1. 在 GitHub 中瀏覽您所擁有的 tooa 儲存機制。 您也可以使用已分歧的任何存放庫。 如果您需要 toofork 儲存機制，使用<https://github.com/Azure-Samples/functions-quickstart>。

1. 按一下 [設定]，然後按一下 [Webhook] 和 [新增 Webhook]。

    ![新增 GitHub webhook](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. 使用 hello 資料表中所指定的設定，然後按一下 **新增 webhook**。

    ![設定 hello webhook URL 和密碼](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| 設定 | 建議的值 | 說明 |
|---|---|---|
| **承載 URL** | 複製的值 | 使用所傳回的 hello 值**<> / Get 函式 URL**。 |
| **祕密**   | 複製的值 | 使用所傳回的 hello 值**<> / 取得 GitHub 密碼**。 |
| **內容類型** | application/json | hello 函式必須要有 JSON 裝載。 |
| 事件觸發程序 | 讓我選取個別事件 | 我們只想 tootrigger 問題註解的事件。  |
| | 問題註解 |  |

現在，hello webhook 加入新的問題註解的使用者設定的 tootrigger 是您的函式。

## <a name="test-hello-function"></a>測試 hello 函式

1. 在您的 GitHub 儲存機制，開啟 hello**問題**新的瀏覽器視窗中索引標籤。

1. 在 hello 新視窗中，按一下 **新議題**，請輸入標題，然後按一下**提交新議題**。

1. Hello 問題輸入註解，然後按一下**註解**。

    ![新增 GitHub 問題註解。](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. 返回 toohello 入口網站，並檢視 hello 記錄檔。 您應該會看到 hello 新註解文字的追蹤項目。

     ![檢視 hello hello 記錄檔中的註解文字。](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>清除資源

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>後續步驟

您已建立函式，此函式會在收到 GitHub Webhook 所提出的要求時開始執行。

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

如需 Webhook 觸發程序的詳細資訊，請參閱 [Azure Functions HTTP 和 Webhook 繫結](functions-bindings-http-webhook.md)。
