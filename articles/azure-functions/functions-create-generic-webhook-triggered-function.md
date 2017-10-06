---
title: "aaaCreate 泛型 webhook 所觸發的 Azure 中的函式 |Microsoft 文件"
description: "使用 Azure 函式 toocreate 無伺服器的函式在 Azure 中的 webhook 所叫用。"
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a>建立由泛型 Webhook 所觸發的函式

Azure 的函式可讓您在無伺服器環境中執行您的程式碼，而不需要 toofirst 建立 VM，或發行 web 應用程式。 例如，您可以設定由 Azure 監視所產生的警示觸發函式 toobe。 本主題說明如何 tooexecute C# 程式碼的資源群組時加入 tooyour 訂用帳戶。   

![泛型的 webhook 觸發 hello Azure 入口網站中的函式](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a>必要條件 

toocomplete 本教學課程：

+ 如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>建立 Azure 函數應用程式

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

接下來，您會在 hello 新函式應用程式中建立函式。

## <a name="create-function"></a>建立由泛型 Webhook 所觸發的函式

1. 展開您的函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。 如果此函式是 hello 第一個函式應用程式中的，選取**自訂函式**。 這會顯示 hello 組完整的函式樣板。

    ![在 Azure 入口網站的 hello 函式 [快速入門] 頁面](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. 選取 hello**泛型 WebHook-C#**範本。 鍵入您 C# 函式的名稱，然後選取 [建立]。

     ![在 hello Azure 入口網站中建立觸發泛型 webhook 函式](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. 在新的函數中，按一下  **<> / Get 函式 URL**，然後複製並儲存 hello 值。 您使用此值 tooconfigure hello webhook。 

    ![檢閱 hello 函式程式碼](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
接下來，您可以在 Azure 監視器的活動記錄警示中建立 Webhook 端點。 

## <a name="create-an-activity-log-alert"></a>建立活動記錄警示

1. 在 hello Azure 入口網站中瀏覽 toohello**監視器**服務中，選取**警示**，按一下**新增活動記錄檔警示**。   

    ![監視](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. 使用 hello hello 資料表中所指定的設定：

    ![建立活動記錄警示](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | 設定      |  建議的值   | 說明                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **活動記錄警示名稱** | resource-group-create-alert | Hello 活動記錄檔的警示名稱。 |
    | **訂用帳戶** | 您的訂用帳戶 | 您使用此教學課程中的 hello 訂用帳戶。 | 
    |  **資源群組** | myResourceGroup | hello hello 警示資源部署至資源群組。 使用在函式應用程式可讓您更輕鬆 tooclean 完成 hello 教學課程之後，hello 相同的資源群組。 |
    | **事件類別目錄** | 管理 | 此類別包括 tooAzure 資源所做的變更。  |
    | **資源類型** | 資源群組 | 篩選警示 tooresource 群組 」 活動。 |
    | **資源群組**<br/>和**資源** | 全部 | 監視所有資源。 |
    | **作業名稱** | 建立資源群組 | 篩選警示 toocreate 作業。 |
    | **Level** | 資訊 | 包含資訊層級警示。 | 
    | **狀態** | Succeeded | 篩選警示 tooactions 已順利完成。 |
    | **動作群組** | 新增 | 建立新的動作群組，定義 hello 動作會引發警示時。 |
    | **動作群組名稱** | function-webhook | 此名稱 tooidentify hello 動作群組。  | 
    | **簡短名稱** | funcwebhook | Hello 動作群組的簡短名稱。 |  

3. 在**動作**，加入使用 hello 設定 hello 資料表中所指定的動作： 

    ![新增動作群組](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | 設定      |  建議的值   | 說明                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **名稱** | CallFunctionWebhook | Hello 動作的名稱。 |
    | **動作類型** | Webhook | hello 回應 toohello 警示是稱為 Webhook URL。 |
    | **詳細資料** | 函式 URL | 貼上您之前複製的 hello 函式的 hello webhook URL 中。 |v

4. 按一下**確定**toocreate hello 警示和動作群組。  

您的訂用帳戶中建立資源群組時，現在稱為 hello webhook。 接下來，您可以更新 hello 程式碼中您的函式 toohandle hello JSON hello hello 要求主體中的記錄資料。   

## <a name="update-hello-function-code"></a>更新 hello 函式程式碼

1. 瀏覽後 tooyour 函式的應用程式在 hello 入口網站，然後展開您的函式。 

2. 取代下列程式碼的 hello hello 入口網站中的 hello 函式中的 hello C# 指令碼：

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

現在您可以在您的訂用帳戶中建立新的資源群組來測試 hello 函式。

## <a name="test-hello-function"></a>測試 hello 函式

1. 按一下 hello 資源群組圖示在 hello hello Azure 入口網站，選取左邊**+ 加**，輸入**資源群組名稱**，然後選取**建立**toocreate 空的資源群組。
    
    ![建立資源群組。](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. 請返回 tooyour 函式，並展開 hello**記錄**視窗。 建立 hello 資源群組之後，hello 活動記錄檔的警示觸發程序 hello webhook 和 hello 函式會執行。 您會看到 hello hello 寫入 toohello 記錄新資源群組名稱。  

    ![新增測試應用程式設定。](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. （選擇性）請返回並刪除您所建立的 hello 資源群組。 請注意，此活動不會觸發 hello 函式。 這是因為刪除作業會篩選出 hello 警示。 

## <a name="clean-up-resources"></a>清除資源

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>後續步驟

您已建立函式，此函式會在收到泛型 Webhook 所提出的要求時開始執行。 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

如需 Webhook 觸發程序的詳細資訊，請參閱 [Azure Functions HTTP 和 Webhook 繫結](functions-bindings-http-webhook.md)。 toolearn 進一步了解開發函式，在 C# 中，請參閱[Azure 函式 C# 指令碼開發人員參考](functions-reference-csharp.md)。

