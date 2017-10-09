---
title: "使用 Azure Stream Analytics aaaReal 時間 Twitter 情緒分析 |Microsoft 文件"
description: "深入了解如何 toouse 資料流分析的即時 Twitter 情緒分析。 從即時儀表板上的事件產生 toodata 的逐步指引。"
keywords: "即時的 twitter 趨勢分析, 情感分析, 社交媒體分析, 趨勢分析範例"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Azure 串流分析中的即時 Twitter 情感分析

深入了解如何 toobuild 社交媒體分析透過將即時的人氣分析解決方案 Twitter 到 Azure 事件中心的事件。 然後您可以撰寫 Azure Stream Analytics 查詢 tooanalyze hello 資料和其中一個存放區 hello 結果以供稍後使用，或使用 儀表板和[Power BI](https://powerbi.com/) tooprovide 即時的深入資訊。

社交媒體分析工具可協助組織了解熱門話題。 熱門話題就是在社交媒體中有大量文章的話題及意見。 情緒分析，也稱為*意見採礦*，會使用社交媒體分析工具 toodetermine 態度產品、 概念，和等等。 

即時 Twitter 趨勢分析會分析工具的絕佳範例，因為 hello 雜湊標記訂閱模型可讓您 toolisten toospecific 關鍵字 （雜湊標記），並開發情緒分析的 hello 摘要。

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>案例：即時的社交媒體情感分析

具有新聞媒體網站的公司有興趣，藉以沿用立即相關 tooits 讀取器的站台內容取得競爭對手與眾不同的優勢。 hello 公司使用社交媒體分析上執行的 Twitter 資料的即時情緒分析 tooreaders 相關的主題。

在 Twitter 上的即時 tooidentify 趨勢主題 hello hello 推文中的磁碟區和人氣的重要主題的相關公司需求即時分析。 換句話說，hello 需要是此摘要的社交媒體為基礎的人氣分析分析引擎。

## <a name="prerequisites"></a>必要條件
在本教學課程中，您可以使用用戶端應用程式的連接 tooTwitter，尋找具有特定雜湊標記 （此您可以設定） 推文。 順序 toorun hello 應用程式，並分析使用 Azure 串流分析推文，您必須擁有 hello 下列 hello:

* Azure 訂用帳戶
* Twitter 帳戶 
* Twitter 應用程式和 hello [OAuth 存取權杖](https://dev.twitter.com/oauth/overview/application-owner-access-tokens)該應用程式。 我們提供高層級的相關指示如何 toocreate Twitter 應用程式更新版本。
* hello TwitterWPFClient 應用程式，它會讀取 hello Twitter 摘要。 tooget 此應用程式，下載 hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip)從 GitHub 檔案，然後再將 hello 封裝解壓縮至您的電腦上的資料夾。 如果您想 toosee hello 原始程式碼和 hello 中執行應用程式偵錯工具，就可以從 hello 原始程式碼[GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)。 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>建立串流分析輸入的事件中樞

hello 範例應用程式會產生事件，並將它們推送 tooan Azure 事件中樞。 Azure 事件中心是事件擷取的資料流分析 hello 慣用方法。 如需詳細資訊，請參閱 hello [Azure 事件中心文件](../event-hubs/event-hubs-what-is-event-hubs.md)。


### <a name="create-an-event-hub-namespace-and-event-hub"></a>建立事件中樞命名空間和事件中樞
在此程序，您先建立事件中樞命名空間中，並將事件中樞 toothat 命名空間。 事件中樞命名空間用 toologically 群組相關的事件匯流排執行個體。 

1. 登入 toohello Azure 入口網站，然後按一下**新增** > **物聯網** > **事件中心**。 

2. 在 hello**建立命名空間**刀鋒視窗中，輸入命名空間名稱，例如`<yourname>-socialtwitter-eh-ns`。 您可以使用任何名稱，如 hello 命名空間，但是 hello 名稱必須是有效的 URL，而且它必須是唯一的 Azure。 
    
3. 選取訂用帳戶並建立或選擇資源群組，然後按一下 [建立]。 

    ![建立事件中樞命名空間](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. 當部署完成 hello 命名空間時，尋找 hello 事件中樞命名空間清單中的 Azure 資源。 

5. 按一下 hello 新命名空間，然後在 hello 命名空間刀鋒視窗中，按一下 **+&nbsp;事件中心**。 

    ![hello 新增事件中樞按鈕建立新的事件中樞 ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. 名稱資料行 hello 新的事件中樞`socialtwitter-eh`。 您可以使用不同的名稱。 如果您這樣做，請記錄下來，因為您稍後需要 hello 名稱。 您不需要 tooset 任何其他選項，hello 事件中心。

    ![建立新事件中樞的刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. 按一下 [建立] 。


### <a name="grant-access-toohello-event-hub"></a>授與存取 toohello 事件中樞

處理程序可以傳送資料 tooan 事件中心之前，hello 事件中心必須要有原則，可讓適當的存取權。 hello 存取原則會產生包含授權資訊的連接字串。

1.  在 hello 事件命名空間刀鋒視窗中，按一下 **事件中心**，然後按一下新的事件中樞的 hello 名稱。

2.  在 hello 事件中樞刀鋒視窗中，按一下 **共用存取原則**，然後按一下  **+&nbsp;新增**。

    >[!NOTE]
    >請確定您正在使用 hello 事件中心不 hello 事件中樞命名空間。

3.  新增名為 `socialtwitter-access` 的原則，然後在 [宣告] 中，選取 [管理]。

    ![建立新事件中樞存取原則的刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  按一下 [建立] 。

5.  Hello 原則已部署之後，請按一下它在 hello 清單中的共用的存取原則。

6.  尋找 hello 方塊標示為**連接字串-主索引鍵**按一下 hello 複製按鈕下一步 toohello 連接字串。 
    
    ![複製 hello 主要連接字串索引鍵與 hello 存取原則](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  貼入文字編輯器中的 hello 連接字串。 Hello 下一節中，進行一些稍微修改 tooit 之後，您需要開啟這個連接字串。

    hello 連接字串看起來像這樣：

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    請注意 hello 連接字串包含多個索引鍵-值組，並以分號分隔： `Endpoint`， `SharedAccessKeyName`， `SharedAccessKey`，和`EntityPath`。  

    > [!NOTE]
    > 為了安全性，已移除 hello hello 範例中的連接字串部分。

8.  Hello 文字編輯器中，移除 hello`EntityPath`組來自 hello 連接字串 （別忘了在它之前的 tooremove hello 分號）。 當您完成時，hello 連接字串看起來像這樣：

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>設定並啟動 hello Twitter 用戶端應用程式
hello 用戶端應用程式直接從 Twitter 取得推文中的事件。 在順序 toodo 因此，它需要的權限 toocall hello Twitter 串流處理應用程式開發介面。 tooconfigure 權限，您的應用程式中建立 Twitter，會產生唯一的認證 （例如 OAuth 語彙基元）。 您可以設定 hello 用戶端應用程式 toouse 這些認證時讓它在應用程式開發介面呼叫。 

### <a name="create-a-twitter-application"></a>建立 Twitter 應用程式
如果您還沒有可用於本教學課程的 Twitter 應用程式，您可以建立一個。 您必須已經有 Twitter 帳戶。

> [!NOTE]
> 在 Twitter 來建立應用程式，並取得 hello 金鑰、 密碼和語彙基元 hello 確切的程序可能會變更。 如果這些指示不符合 hello Twitter 網站上看到的內容，請參閱 toohello Twitter 開發人員文件。

1. 移 toohello [Twitter 應用程式管理頁面](https://apps.twitter.com/)。 

2. 建立新的應用程式。 

    * 對於 hello 網站 URL，請指定有效的 URL。 它並沒有 toobe 即時網站。 (您不能只指定 `localhost`。)
    * 將 hello 回呼欄位保留空白。 您使用此教學課程中的 hello 用戶端應用程式不需要的回呼。

    ![在 Twitter 中建立應用程式](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. （選擇性） 變更 tooread 專用的 hello 應用程式的權限。

4. 建立 hello 應用程式時，請移 toohello**機碼和存取權杖**頁面。

5. 按一下 [hello] 按鈕 toogenerate 存取權杖和存取語彙基元秘項。

請保留這項資訊很方便，因為 hello 下一個程序中需要它。

>[!NOTE]
>hello 金鑰和秘密 hello Twitter 應用程式提供存取 tooyour Twitter 帳戶。 這項資訊視為機密，就像是您的 Twitter 密碼 hello 相同。 例如，不要內嵌應用程式中的，您必須提供 tooothers 此資訊。 


### <a name="configure-hello-client-application"></a>Hello 用戶端應用程式設定
我們建立了連接 tooTwitter 資料使用的用戶端應用程式[Twitter 的資料流 Api](https://dev.twitter.com/streaming/overview) toocollect 推文中事件的相關一組特定的主題。 hello 應用程式會使用 hello [Sentiment140](http://help.sentiment140.com/)開放原始碼工具，指派下列人氣值 tooeach 推文中的 hello:

* 0 = 負值
* 2 = 中性
* 4 = 正值

Hello 推文事件已指派給人氣值之後，它們會推送至您稍早建立的 toohello 事件中心。

Hello 應用程式執行之前，它會需要某些您的資訊，例如 hello Twitter 索引鍵和 hello 事件中樞連接字串。 您可以提供下列方式 hello 組態資訊：

* 執行 hello 應用程式，，，然後使用 hello 應用程式的 UI tooenter hello 金鑰、 密碼和連接字串。 如果您這樣做，hello 組態資訊用於目前的工作階段，但它不會儲存。
* 編輯 hello 應用程式的.config 檔案和設定 hello 值。 這種方式保存 hello 組態資訊，但這也表示，此潛在的敏感資訊會儲存在您的電腦上以純文字。

hello 下列程序說明這兩種方法。 

1. 請確定您已下載並解壓縮 hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip)應用程式，如下所示 hello 必要條件。

2. tooset hello 值在執行階段 （並僅針對 hello 目前工作階段），執行 hello`TwitterWPFClient.exe`應用程式。 當 hello 應用程式會提示您時，請輸入下列值的 hello:

    * hello Twitter 取用者金鑰 （應用程式開發介面）。
    * hello Twitter 使用者密碼 （應用程式開發介面機密）。
    * hello Twitter 存取語彙基元。
    * hello Twitter 存取語彙基元秘項。
    * 您稍早儲存 hello 連接字串資訊。 請確定您使用 hello 連接字串移除 hello`EntityPath`從索引鍵-值組。
    * 您想要針對 toodetermine 人氣的 hello Twitter 關鍵字。

   ![執行中的 TwitterWpfClient 應用程式，顯示隱藏的設定](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. tooset hello 值持續，使用文字編輯器 tooopen hello TwitterWpfClient.exe.config 檔案。 接著在 hello`<appSettings>`項目，執行這項操作：

    * 設定`oauth_consumer_key`toohello Twitter 取用者金鑰 （應用程式開發介面）。 
    * 設定`oauth_consumer_secret`toohello Twitter 使用者密碼 （應用程式開發介面機密）。
    * 設定`oauth_token`toohello Twitter 存取語彙基元。
    * 設定`oauth_token_secret`toohello Twitter 存取語彙基元秘項。

    稍後 hello`<appSettings>`項目，進行這些變更：

    * 設定`EventHubName`toohello 事件中樞名稱 （也就是 toohello 值 hello 實體路徑）。
    * 設定`EventHubNameConnectionString`toohello 連接字串。 請確定您使用 hello 連接字串移除 hello`EntityPath`從索引鍵-值組。

    hello`<appSettings>`區段看起來像下列範例中的 hello。 (為了清楚起見和基於安全考量，我們已遮蔽幾行並移除某些字元。)

    ![在文字編輯器中，顯示 hello Twitter 金鑰及密碼，以及 hello 事件中樞連接字串資訊 TwitterWpfClient 應用程式組態檔](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. 如果您已經沒有啟動 hello 應用程式，現在就執行 TwitterWpfClient.exe。 

5. 按一下 hello 綠色開始按鈕 toocollect 社交人氣。 您會看到推文事件以 hello **CreatedAt**，**主題**，和**SentimentScore**傳送 tooyour 事件中心的值。

    ![執行中的 TwitterWpfClient 應用程式，顯示推文清單](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >如果您看到錯誤，而且您沒有看到推文顯示 hello hello 視窗下半部中的資料流，請仔細檢查 hello 金鑰和密碼。 也請檢查 hello 連接字串 (請確定它不包含 hello`EntityPath`索引鍵和值。)


## <a name="create-a-stream-analytics-job"></a>建立串流分析工作

既然推文中的事件會從 Twitter 即時資料流處理，您可以設定串流分析工作 tooanalyze 這些事件即時。

1. 在 hello Azure 入口網站，按一下 **新增** > **物聯網** > **資料流分析工作**。

2. 名稱 hello 工作`socialtwitter-sa-job`和指定的訂用帳戶、 資源群組和位置。

    它是個不錯的主意 tooplace hello 作業和 hello 事件中樞 hello，以免付出 tootransfer 資料區域之間的最佳效能，所以相同的區域。

    ![建立新的串流分析作業](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. 按一下 [建立] 。

    建立 hello 工作，而 hello 入口網站會顯示工作詳細資料。


## <a name="specify-hello-job-input"></a>指定 hello 作業輸入

1. 串流分析工作，在底下**作業拓撲**hello 中間的 hello 作業] 刀鋒視窗中，按一下 [**輸入**。 

2. 在 hello**輸入**刀鋒視窗中，按一下 **+&nbsp;新增**然後填入 hello 刀鋒視窗包含下列值：

    * **輸入的別名**： 使用 hello 名稱`TwitterStream`。 如果使用不同的名稱，請記下來，因為稍後需要用到。
    * **來源類型**：選取 [資料流]。
    * **來源**：選取 [事件中樞]。
    * **匯入選項**：選取 [使用目前訂用帳戶的事件中樞]。 
    * **服務匯流排命名空間**： 選取 hello 事件中樞命名空間您稍早建立 (`<yourname>-socialtwitter-eh-ns`)。
    * **事件中心**: hello 選取您稍早建立的事件中心 (`socialtwitter-eh`)。
    * **事件中樞原則名稱**： 選取您稍早建立的 hello 存取原則 (`socialtwitter-access`)。

    ![建立串流分析作業的新輸入](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. 按一下 [建立] 。


## <a name="specify-hello-job-query"></a>指定 hello 工作查詢

串流分析支援說明轉換的簡單、宣告式查詢模型。 toolearn 進一步了解 hello 語言，請參閱 hello [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)。  本教學課程可協助您撰寫以及測試數個 Twitter 資料查詢。

您可以使用 toocompare hello 數目在主題之間提到，[輪轉視窗](https://msdn.microsoft.com/library/azure/dn835055.aspx)tooget hello 計數每五秒主題所提及。

1. 關閉 hello**輸入**刀鋒視窗，如果您還沒有這麼做。

2. 在 hello 作業刀鋒視窗中，按一下 hello**查詢**方塊。 Azure 會列出 hello 輸入及輸出，已設定為 hello 工作，並可讓您建立查詢，可讓您轉換 hello 輸入資料流傳送 toohello 輸出。

3. 請確定該 hello TwitterWpfClient 應用程式正在執行。 

3. 在 hello**查詢**刀鋒視窗中，按一下 下一步 toohello 的 hello 點`TwitterStream`輸入，然後選取 **範例從輸入資料**。

    ![功能表選項 toouse 的範例資料 hello 串流分析工作項目，如 「 範例資料從輸入 」 選取](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    這會開啟可讓您指定以 tooread hello 多久輸入資料流定義多少範例資料 tooget 刀鋒視窗。

4. 設定**分鐘**too3，然後按一下**確定**。 
    
    ![取樣 hello 輸入資料流，與 「 3 分鐘 」，選取選項。](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure 範例 3 分鐘 hello 輸入資料流中的資料量與 hello 範例資料已就緒時通知您。 (這需要等一下。) 

    hello 範例資料會暫時存放，可同時有 hello 查詢視窗中開啟。 如果您關閉 hello 查詢視窗中，會捨棄 hello 範例資料，並可 toocreate 一組新的範例資料。 

5. 變更 hello 編輯器 toohello 後面的程式碼中的 hello 查詢：

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    如果沒有使用`TwitterStream`hello hello 輸入的別名，以取代您別名`TwitterStream`hello 查詢中。  

    此查詢會使用 hello **TIMESTAMP BY**關鍵字 toospecify hello 裝載 toobe hello 時態計算中使用的時間戳記欄位。 如果未指定此欄位，hello 視窗化作業會使用每個事件抵達 hello 事件中心的 hello 時間執行。 進一步了解 hello < 抵達時間與比較應用程式時間 > 一節中[串流分析查詢參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)。

    此查詢同時存取每個視窗的 hello 結束的時間戳記使用 hello **System.Timestamp**屬性。

5. 按一下 [ **測試**]。 hello 查詢會執行您所取樣的 hello 資料。
    
6. 按一下 [儲存] 。 這可以節省 hello 查詢 hello 串流分析工作的一部分。 （它不會儲存 hello 範例資料）。


## <a name="experiment-using-different-fields-from-hello-stream"></a>嘗試使用不同的欄位從 hello 資料流 

hello 下表列出屬於 hello JSON 資料流資料的 hello 欄位。 您可用 tooexperiment hello 查詢編輯器中。

|JSON 屬性 | 定義|
|--- | ---|
|CreatedAt | hello 時間建立該 hello 推文|
|主題 | 符合 hello hello 主題指定關鍵字|
|SentimentScore | 從 Sentiment140 hello 人氣分數|
|作者 | 傳送嗨推文中的 hello Twitter 控點|
|文字 | hello 推文中的 hello 完整主體|


## <a name="create-an-output-sink"></a>建立輸出接收器

現在您已經定義的事件資料流、 事件中樞輸入的 tooingest 事件，以及查詢 tooperform 轉換 hello 資料流上。 hello 最後一個步驟是 toodefine hello 工作的輸出接收。  

在本教學課程中，寫入彙總的 hello 推文事件從 hello 工作查詢 tooAzure Blob 儲存體。  您也可以推送您的結果 tooAzure SQL Database、 Azure 資料表儲存體，事件中心或 Power BI 中，根據您的應用程式的需求。

## <a name="specify-hello-job-output"></a>指定 hello 作業輸出

1. 在 hello**作業拓撲**區段中，按一下 hello**輸出**方塊。 

2. 在 hello**輸出**刀鋒視窗中，按一下 **+&nbsp;新增**然後填入 hello 刀鋒視窗包含下列值：

    * **輸出別名**： 使用 hello 名稱`TwitterStream-Output`。 
    * **接收器**：選取 [Blob 儲存體]。
    * **匯入選項**：選取 [使用來自目前訂用帳戶的 Blob 儲存體]。
    * **儲存體帳戶**。 選取 [建立新儲存體帳戶]。
    * **儲存體帳戶** (第二個方塊)。 輸入 `YOURNAMEsa`，其中 `YOURNAME` 是您的名稱或另一個唯一字串。 hello 名稱可以使用小寫字母和數字，而且它必須是唯一整個 Azure。 
    * **容器**。 輸入 `socialtwitter`。
    hello 儲存體帳戶名稱及容器名稱是使用同時 tooprovide hello blob 儲存體，像這樣的 URI: 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![串流分析作業的 [新輸出] 刀鋒視窗](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. 按一下 [建立] 。 

    Azure 會建立 hello 儲存體帳戶，並會自動產生索引鍵。 

5. 關閉 hello**輸出**刀鋒視窗。 


## <a name="start-hello-job"></a>啟動 hello 工作

已指定作業輸入、查詢和輸出。 您已準備好 toostart hello 資料流分析工作。

1. 請確定該 hello TwitterWpfClient 應用程式正在執行。 

2. 在 hello 作業刀鋒視窗中，按一下 **啟動**。

    ![啟動 hello 資料流分析工作](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. 在 hello**開始工作**刀鋒視窗中，針對**作業輸出的開始時間**，選取**現在**，然後按一下**啟動**。 

    ![「 啟動工作 」 刀鋒視窗中的 hello 資料流分析工作](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure 通知您，當 hello 作業已啟動，而且 hello 作業刀鋒視窗中，在 hello 狀態會顯示為**執行**。

    ![工作正在執行](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>檢視情感分析輸出

您的工作已開始執行，且正在處理 hello 即時 Twitter 資料流之後，您可以檢視 hello 情緒分析輸出。

您可以使用這類工具[Azure 儲存體總管](https://http://storageexplorer.com/)或[Azure 總管](http://www.cerebrata.com/products/azure-explorer/introduction)tooview 即時輸出您的工作。 從這裡，您可以使用[Power BI](https://powerbi.com/) tooextend 您自訂的儀表板的應用程式 tooinclude 喜歡 hello hello 下列螢幕擷取畫面所示：

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>建立另一個查詢 tooidentify 趨勢主題

您可以使用 toounderstand Twitter 情緒的另一個查詢根據[滑動視窗](https://msdn.microsoft.com/library/azure/dn835051.aspx)。 tooidentify 趨勢的主題，您尋找跨提及中指定的時間量的臨界值的主題。

基於 hello 本教學課程，您檢查主題所述 20 倍以上 hello 最後 5 秒。

1. 在 hello 作業刀鋒視窗中，按一下 **停止**toostop hello 作業。 

2. 在 hello**作業拓撲**區段中，按一下 hello**查詢**方塊。 

3. 變更 hello 查詢 toohello 下列：

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. 按一下 [儲存] 。

5. 請確定該 hello TwitterWpfClient 應用程式正在執行。 

6. 按一下**啟動**toorestart hello 作業使用 hello 新查詢。


## <a name="get-support"></a>取得支援
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
