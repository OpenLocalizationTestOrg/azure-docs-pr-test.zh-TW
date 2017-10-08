---
title: "aaaCreate 函式可與 Azure 邏輯應用程式整合，|Microsoft 文件"
description: "建立 Azure 邏輯應用程式和 Azure 認知服務 toocategorize 推文人氣與整合的函式和人氣很低時，傳送通知。"
services: functions, logic-apps, cognitive-services
keywords: "工作流程, 雲端應用程式, 雲端服務, 商務程序, 系統整合, 企業應用程式整合, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>建立與 Azure Logic Apps 整合的函式

Azure 邏輯應用程式與整合 hello 邏輯應用程式的設計工具中，azure 函式。 這項整合可讓您使用的運算能力函式與其他 Azure 和協力廠商服務的協調流程中的 hello。 

此教學課程會示範如何 toouse 函式與從 Twitter 文章的 Logic Apps 和 Azure 認知服務 tooanalyze 人氣。 HTTP 觸發函式將分類為綠色、 黃色或紅色 hello 人氣分數為基礎的推文。 偵測到不佳的情感時，會傳送一封電子郵件。 

![此映像顯示邏輯應用程式設計工具中應用程式的前兩個步驟](media/functions-twitter-email/designer1.png)

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立辨識服務帳戶。
> * 建立可將推文情感進行分類的函式。
> * 建立連接 tooTwitter 邏輯應用程式。
> * 加入 人氣偵測 toohello 邏輯應用程式。 
> * 連接 hello 邏輯應用程式 toohello 函式。
> * 傳送 hello 回應 hello 函式為基礎的電子郵件。

## <a name="prerequisites"></a>必要條件

+ 使用中的 [Twitter](https://twitter.com/) 帳戶。 
+ [Outlook.com](https://outlook.com/) 帳戶 (用於傳送通知)。
+ 本主題以建立其起始點 hello 資源為[從 hello Azure 入口網站中建立您的第一個函式](functions-create-first-azure-function.md)。  
如果您尚未這樣做，請完成這些步驟現在 toocreate 函式應用程式。

## <a name="create-a-cognitive-services-account"></a>建立辨識服務帳戶

認知的服務帳戶是必要的 toodetect hello 人氣的受監視的推文。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。

2. 按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。

3. 按一下 [資料 + 分析] > **辨識服務**。 使用 hello 設定為在 hello 資料表中，指定接受 hello 條款，然後檢查**Pin toodashboard**。

    ![[建立辨識帳戶] 刀鋒視窗](media/functions-twitter-email/cog_svcs_account.png)

    | 設定      |  建議的值   | 說明                                        |
    | --- | --- | --- |
    | **名稱** | MyCognitiveServicesAccnt | 請選擇唯一的帳戶名稱。 |
    | **API 類型** | 文字分析 API | 應用程式開發介面使用 tooanalyze 文字。  |
    | **位置** | 美國西部 | 目前，只有 [美國西部] 適用於文字分析。 |
    | **定價層** | F0 | 啟動與 hello 最低層。 如果您用盡呼叫時，調整 tooa 更高的層。|
    | **資源群組** | myResourceGroup | 使用 hello 相同資源群組，在本教學課程的所有服務。|

4. 按一下**建立**toocreate 您的帳戶。 建立 hello 帳戶之後，按一下 新認知的服務帳戶已釘選的 toohello 儀表板。 

5. Hello 帳戶中，按一下 **金鑰**，然後將複製的 hello 值**金鑰 1**並將其儲存。 您使用此索引鍵 tooconnect hello 邏輯應用程式 tooyour 認知的服務帳戶。 
 
    ![之間的信任](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>建立 hello 函式

函式提供了絕佳 toooffload 邏輯應用程式工作流程中的處理工作。 本教學課程會使用 HTTP 觸發函式 tooprocess 推文人氣分數認知服務及傳回分類值。  

1. 展開 應用程式函式中，按一下 hello  **+** 太下一步按鈕**函式**，按一下 hello **HTTPTrigger**範本。 型別`CategorizeSentiment`hello 函式**名稱**按一下**建立**。

    ![函式應用程式刀鋒視窗，Functions +](media/functions-twitter-email/add_fun.png)

2. Hello，下列程式碼，以取代 hello hello run.csx 檔案內容，然後按一下 **儲存**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    此函式程式碼會傳回根據收到 hello 要求中的 hello 人氣分數色彩類別目錄。 

3. tootest hello 函式中，按一下 [**測試**在 hello 最右側 tooexpand hello 測試] 索引標籤。輸入的值是`0.2`hello**要求本文**，然後按一下**執行**。 值為**紅色**hello 回應 hello 主體中傳回。 

    ![測試 hello Azure 入口網站中的 hello 函式](./media/functions-twitter-email/test.png)

現在您的函式可將情感分數進行分類。 接下來，您可以建立邏輯應用程式，將您的函式與 Twitter 和辨識服務帳戶進行。 

## <a name="create-a-logic-app"></a>建立邏輯應用程式   

1. 在 hello Azure 入口網站中按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。

2. 按一下 [企業整合] > [邏輯應用程式]。 然後，使用 hello 設定做為資料表中指定 hello，請檢查**Pin toodashboard**，然後按一下**建立**。
 
4. 然後，輸入**名稱**像`TweetSentiment`、 hello 表指定方式使用 hello 設定、 接受 hello 條款，以及檢查**Pin toodashboard**。

    ![在 hello Azure 入口網站中建立邏輯應用程式](./media/functions-twitter-email/new_logicApp.png)

    | 設定      |  建議的值   | 說明                                        |
    | ----------------- | ------------ | ------------- |
    | **名稱** | TweetSentiment | 為您的應用程式選擇適當名稱。 |
    | **資源群組** | myResourceGroup | 應用程式開發介面使用 tooanalyze 文字。  |
    | **位置** | 美國東部 | 選擇位置關閉 tooyou。 |
    | **資源群組** | myResourceGroup | 選擇與之前 hello 相同的現有資源群組。|

4. 按一下**建立**toocreate 邏輯應用程式。 建立 hello 應用程式之後，按一下 新邏輯應用程式已釘選的 toohello 儀表板。 在 hello 邏輯應用程式的設計工具中，向下捲動，然後按一下 hello**空白邏輯應用程式**範本。 

    ![空白的 Logic Apps 範本](media/functions-twitter-email/blank.png)

您現在可以使用 hello 邏輯應用程式設計師 tooadd 服務和觸發程序 tooyour 應用程式。

## <a name="connect-tootwitter"></a>連接 tooTwitter

首先，建立連接 tooyour Twitter 帳戶。 觸發 hello 應用程式 toorun 推文輪詢 hello 邏輯應用程式。

1. 在 hello 設計工具中，按一下 hello **Twitter**服務，然後按一下 hello**新推文回傳時**觸發程序。 登入 tooyour Twitter 帳戶，並授權 Logic Apps toouse 您的帳戶。

2. Hello 表指定方式使用 hello Twitter 觸發程序設定。 

    ![Twitter 連接器設定](media/functions-twitter-email/azure_tweet.png)

    | 設定      |  建議的值   | 說明                                        |
    | ----------------- | ------------ | ------------- |
    | **搜尋文字** | #Azure | 使用雜湊標記 hello 選擇間隔內的熱門的 toogenerate 新推文。 時使用 hello 免費層和您的雜湊標記太受歡迎，您可以快速地使用向上 hello 交易認知的服務帳戶中。 |
    | **頻率** | 分鐘 | 用來輪詢 Twitter hello 頻率單位。  |
    | **間隔** | 15 | 中的頻率單位的 Twitter 要求之間所經過的 hello 時間。 |

3.  按一下**儲存**tooconnect tooyour Twitter 帳戶。 

現在您的應用程式是已連線的 tooTwitter。 接下來，您可以連接 tootext 分析 toodetect hello 人氣的收集推文。

## <a name="add-sentiment-detection"></a>新增情感偵測

1. 依序按一下 [新增步驟]、[新增動作]。

    ![選取 [新增步驟]，然後選取 [新增動作]](media/functions-twitter-email/new_step.png)

2. 在**選擇動作**，按一下 **文字分析**，然後按一下hello**偵測人氣**動作。

    ![偵測情感](media/functions-twitter-email/detect_sent.png)

3. 輸入連線名稱，例如`MyCognitiveServicesConnection`，貼上 hello 金鑰，為您認知的服務帳戶儲存，然後按一下**建立**。  

4. 按一下**文字 tooanalyze** > **推文提供文字**，然後按一下**儲存**。  

    ![偵測情感](media/functions-twitter-email/ds_tta.png)

人氣偵測設定時，您可以新增取用 hello 人氣分數輸出連線 tooyour 函式。

## <a name="connect-sentiment-output-tooyour-function"></a>連接 人氣輸出 tooyour 函式

1. 在 hello 邏輯應用程式的設計工具中，按一下 **新步驟** > **將動作加入**，然後按一下 **Azure 函式**。 

2. 按一下**選擇 Azure 的函式**，選取 hello **CategorizeSentiment**您稍早建立的函式。  

    ![顯示 [選擇 Azure 函式] 的 Azure 函式方塊](media/functions-twitter-email/choose_fun.png)

3. 在**要求本文**中，依序按一下 [分數] 和 [儲存]。

    ![分數](media/functions-twitter-email/trigger_score.png)

現在，您的函式會從 hello 邏輯應用程式傳送的人氣分數時觸發。 色彩編碼的類別目錄的 hello 函式，會傳回 toohello 邏輯應用程式。 接下來，您加入的人氣值時，會傳送電子郵件通知**紅色**hello 函式會傳回。 

## <a name="add-email-notifications"></a>新增電子郵件通知

hello 最後一部分 hello 工作流程時，tootrigger 電子郵件做為計分 hello 人氣_紅色_。 本主題是使用 Outlook.com 連接器。 您可以執行類似的步驟 toouse Gmail 或 Office 365 Outlook 連接器。   

1. 在 hello 邏輯應用程式的設計工具中，按一下 **新步驟** > **加入條件**。 

2. 按一下 [選擇值]，然後按一下 [本文]。 選取 [等於]、按一下 [選擇值] 並輸入 `RED`，然後按一下 [儲存]。 

    ![加入條件 toohello 邏輯應用程式。](media/functions-twitter-email/condition.png)

3. 在**如果是，不執行任何動作**，按一下 **將動作加入**，搜尋`outlook.com`，按一下 **傳送電子郵件**，並登入 tooyour Outlook.com 帳戶。
    
    ![選擇 hello 條件的動作。](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > 如果您沒有 Outlook.com 帳戶，可以選擇另一個連接器，例如 Gmail 或 Office 365 Outlook

4. 在 hello**傳送電子郵件**hello 資料表中指定的動作，以使用 hello 電子郵件設定。 

    ![設定 hello 傳送電子郵件動作的 hello 電子郵件。](media/functions-twitter-email/sendemail.png)

    | 設定      |  建議的值   | 說明  |
    | ----------------- | ------------ | ------------- |
    | **To** | 輸入您的電子郵件地址 | 收到 hello 通知的 hello 電子郵件地址。 |
    | **主旨** | 偵測到負面的推文情感  | hello hello 電子郵件通知的主旨列。  |
    | **內文** | 推文文字、位置 | 按一下 hello**推文提供文字**和**位置**參數。 |

5.  按一下 [儲存] 。

既然 hello 工作流程已完成，您可以啟用 hello 邏輯應用程式，並查看工作的 hello 函式。

## <a name="test-hello-workflow"></a>測試 hello 工作流程

1. 在 hello 邏輯應用程式的設計工具中，按一下 **執行**toostart hello 應用程式。

2. 在 hello 左側資料行，按一下 **概觀**toosee hello hello 邏輯應用程式狀態。 
 
    ![邏輯應用程式執行狀態](media/functions-twitter-email/over1.png)

3. （選擇性）按一下其中一個 hello hello 執行的執行 toosee 詳細資料。

4. 移 tooyour 函式、 檢視 hello 記錄檔，並確認人氣值已接收及處理。
 
    ![檢視函式記錄](media/functions-twitter-email/sent.png)

5. 偵測到潛在的負面情感時，您會收到一封電子郵件。 如果您尚未收到一封電子郵件，您可以變更 hello 函式程式碼 tooreturn 紅色每次：

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    驗證電子郵件通知後，變更後 toohello 原始的程式碼：

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > 完成本教學課程之後，您應該停用 hello 邏輯應用程式。 停用 hello 應用程式，您可以避免正在充電執行，並使用向上 hello 認知的服務帳戶中的交易。

現在您已經知道是多麼的輕鬆成的 Logic Apps 工作流程的 toointegrate 函式。

## <a name="disable-hello-logic-app"></a>停用 hello 邏輯應用程式

toodisable hello 邏輯應用程式中，按一下 **概觀**，然後按一下**停用**頂端 hello 囉 」 畫面。 這會停止執行，而且會產生費用，而不刪除 hello 應用程式中的 hello 邏輯應用程式。 

![函式記錄](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 建立辨識服務帳戶。
> * 建立可將推文情感進行分類的函式。
> * 建立連接 tooTwitter 邏輯應用程式。
> * 加入 人氣偵測 toohello 邏輯應用程式。 
> * 連接 hello 邏輯應用程式 toohello 函式。
> * 傳送 hello 回應 hello 函式為基礎的電子郵件。

如何前進 toohello 下一個教學課程 toolearn toocreate 無伺服器的應用程式開發介面，針對您的函式。

> [!div class="nextstepaction"] 
> [使用 Azure Functions 建立無伺服器 API](functions-create-serverless-api.md)

toolearn 進一步了解邏輯應用程式，請參閱[Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md)。

