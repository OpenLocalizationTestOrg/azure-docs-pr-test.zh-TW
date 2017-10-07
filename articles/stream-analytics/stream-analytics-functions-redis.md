---
title: "Azure 函式的 aaaStream 分析即時處理 |Microsoft 文件"
description: "了解如何 toouse Azure 函式連接的服務匯流排佇列，toopopulate hello 輸出資料流分析工作的 Azure Redis 快取。"
keywords: "data stream, redis cache, service bus queue, 資料流, redis 快取, 服務匯流排佇列"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>如何從 Azure Redis 快取 Azure 函式的使用中的 Azure Stream Analytics toostore 資料
Azure 串流分析可讓您快速開發和部署的低成本的解決方案 toogain 即時深入資訊從裝置、 感應器、 基礎結構，和應用程式或資料的任何資料流。 它可啟用不同的使用案例，例如即時管理與監視、命令與控制、詐騙偵測、Connected Cars 等等。 在許多這類案例中，您可能想 toostore Azure 串流分析輸出到分散式的資料存放區，例如 Azure Redis 快取的資料。

假設您是電信公司的員工。 您嘗試 toodetect SIM 詐騙，其中來自多個呼叫 hello 相同的識別、 在 hello 相同的時間，但在不同地理位置。 您負責 Azure Redis 快取中儲存所有 hello 潛在詐騙撥打電話。 在此部落格中，我們將提供如何輕鬆地完成此工作的指引。 

## <a name="prerequisites"></a>必要條件
完整的 hello[即時詐騙偵測][ fraud-detection] ASA 的逐步解說

## <a name="architecture-overview"></a>架構概觀
![架構的螢幕擷取畫面](./media/stream-analytics-functions-redis/architecture-overview.png)

Hello 前圖所示，資料流分析可讓資料流的輸入的資料 toobe 查詢和傳送 tooan 輸出。 根據 hello 輸出，Azure 函式可以接著會觸發某些類型事件。 

在這篇部落格，我們將重點放在此管線 hello Azure 函式部分或更明確地說 hello 觸發的事件儲存到 hello 快取的詐騙資料。
完成 hello 之後[即時詐騙偵測][ fraud-detection]教學課程中，您已輸入 （事件中心）、 查詢，以及輸出 （blob 儲存） 已設定及執行。 在這篇部落格，我們，改為變更 hello 輸出 toouse 服務匯流排佇列。 在這之後，我們連接 Azure 函式 toothis 佇列。 

## <a name="create-and-connect-a-service-bus-queue-output"></a>建立並連接服務匯流排佇列輸出
toocreate 服務匯流排佇列，請依照下列步驟 1 和 2 中的 hello.NET 區段[開始使用 Service Bus 佇列][servicebus-getstarted]。
現在讓我們將連接 hello 佇列 toohello 資料流分析工作所建立 hello 早詐騙偵測逐步解說。

1. 在 hello Azure 入口網站，移 toohello**輸出**刀鋒視窗中的工作，然後選取**新增**hello 頁面頂端的 hello。
   
    ![加入輸出](./media/stream-analytics-functions-redis/adding-outputs.png)
2. 選擇**服務匯流排佇列**為 hello **Sink**依照囉 」 畫面上 hello 指示。 確定 toochoose hello 命名空間的 hello 服務匯流排佇列中您建立[開始使用 Service Bus 佇列][servicebus-getstarted]。 當您完成時，請按一下 hello 「 右邊 」 按鈕。
3. 指定下列值的 hello:
   
   * **事件序列化程式格式**：JSON
   * **編碼**：UTF8
   * **格式**：列分隔
4. 按一下 hello**建立**按鈕 tooadd 這個來源和 tooverify 資料流分析可以成功連線 toohello 儲存體帳戶。
5. 在 hello**查詢**索引標籤上，取代 hello 下列中的 hello 目前的查詢。 取代 * [您的服務匯流排名稱] * 與您在步驟 3 中建立的 hello 輸出名稱。 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a>建立 Azure Redis 快取
依照下列中的 hello.NET 一節建立的 Azure Redis 快取[如何 tooUse Azure Redis 快取][ use-rediscache]之前稱為 hello 區段***設定 hello 快取用戶端***。
完成後，您將具有新的 Redis 快取。 在下**所有設定**，選取**存取金鑰**並記下 hello***主要連接字串***。

![架構的螢幕擷取畫面](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>建立 Azure 函式
請遵循[建立您的第一個 Azure 函式][ functions-getstarted]教學課程 tooget 開始使用 Azure 函式。 如果您已經有 Azure 的函式就像 toouse，然後跳過[撰寫 tooRedis 快取](#Writing-to-Redis-Cache)

1. 在 hello 入口網站選取應用程式服務從 hello 左側瀏覽，然後按一下 Azure 函式應用程式名稱 tooget toohello 函式的應用程式的網站。
    ![應用程式服務函式清單的螢幕擷取畫面](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. 按一下 [新增函式] > [ServiceBusQueueTrigger – C#]。 Hello 下列欄位，請遵循這些指示：
   
   * **佇列名稱**： 名稱為您輸入當您建立 hello 佇列中的 hello 名稱相同的 hello[開始使用 Service Bus 佇列][ servicebus-getstarted] （非 hello service bus 的 hello 名稱）。 請確定您使用之輸出資料流分析連線的 toohello hello 佇列。
   * **服務匯流排連接**︰選取 [加入連接字串]。 toofind hello 連接字串中，移 toohello 傳統入口網站，選取**Service Bus**，hello 您所建立的服務匯流排和**連接資訊**在 hello 囉 」 畫面底部。 請確定您是在此頁面上的 hello 主畫面上。 複製並貼上 hello 連接字串。 您可用 tooenter 任何連接的名稱。
     
       ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **AccessRights**︰選擇 [管理]
3. 按一下 [建立] 

## <a name="writing-tooredis-cache"></a>寫入 tooRedis 快取
我們現在已經建立一個可從服務匯流排佇列進行讀取的 Azure 函式。 Toodo 剩下的就是使用我們的函式 toowrite 此資料 toohello Redis 快取。 

1. 選取您新建**ServiceBusQueueTrigger**，然後按一下**函式應用程式設定**hello 最上層顯示右下角。 選取**移 tooApp 服務設定 > 設定 > 應用程式設定**
2. 在 hello 連接字串區段，會建立 hello 中的名稱**名稱**> 一節。 貼上您在 hello 找到 hello 主要連接字串**建立 Redis 快取**逐步執行 hello**值**> 一節。 在 [SQL 資料庫]的位置選取 [自訂]。
3. 按一下**儲存**hello 頂端。
   
    ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/function-connection-string.png)
4. 現在返回 toohello 應用程式服務設定，並選取**工具 > 應用程式服務編輯器 （預覽） > 上 > 移**。
   
    ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/app-service-editor.png)
5. 在您選擇的編輯器，建立名為 JSON 檔案**project.json**與 hello 後面，並將它儲存 tooyour 本機磁碟。
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. 此檔案上傳至您的函式 (不 WWWROOT) hello 根目錄。 您應該會看到名為**project.lock.json**自動出現，請確認該 hello Nuget"StackExchange.Redis"和"Newtonsoft.Json"封裝已匯入。
7. 在 hello **run.csx**檔案時，請取代下列程式碼的 hello hello 預先產生的程式碼。 在 hello lazyConnection 函式，取代您在步驟 2 中建立的 hello 名稱"CONN NAME"**資料儲存到 hello Redis 快取**。

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a>啟動 hello 資料流分析工作
1. 啟動 hello telcodatagen.exe 應用程式。 hello 用法如下所示：````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. 從 hello hello 入口網站中的資料流分析工作刀鋒視窗，按一下 **啟動**hello 頁面頂端的 hello。
   
    ![開始工作的螢幕擷取畫面](./media/stream-analytics-functions-redis/starting-job.png)
3. 在 hello**開始工作**刀鋒視窗中，選取**現在**然後按一下hello**啟動**在 hello 囉 」 畫面底部的按鈕。 hello 作業狀態變更 tooStarting 後一些時間變更 tooRunning。
   
    ![開始工作時間範圍的螢幕擷取畫面](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>執行解決方案並檢查結果
返回 tooyour **ServiceBusQueueTrigger**頁面上，您現在應該會看到記錄陳述式。 這些記錄檔會顯示 hello 服務匯流排佇列，放入 hello 資料庫中取得的項目，提取出使用 hello 時間當做 hello 機碼 ！

tooverify 您資料的 Redis 快取中，移至 tooyour Redis 快取頁面 hello 新入口網站 (hello 前面所示[建立 Azure Redis 快取](#Create-an-Azure-Redis-Cache)步驟)，選取 [主控台]。

現在您可以撰寫 Redis 命令 tooconfirm 資料實際上位於 hello 快取。

![Redis 主控台的螢幕擷取畫面](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>後續步驟
我們很高興解 hello 新項目的 Azure 函式和資料流分析可以一起執行，我們希望這帶來新的可能性的。 如果您有任何意見反應上您想要接下來，則可以免費 toouse hello [Azure UserVoice 網站](https://feedback.azure.com/forums/270577-stream-analytics)。

如果您是新的 Microsoft Azure 時，我們邀請您 tootry 它編寫透過註冊[免費試用的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。 如果您是新 tooStream 分析，則太邀請[建立第一個資料流分析工作](stream-analytics-create-a-job.md)。

如果您需要任何協助或有任何問題，請在 [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) 或 [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) 論壇中提出。 

您也可以查看下列資源的 hello:

* [Azure Functions 開發人員參考](../azure-functions/functions-reference.md)
* [Azure Functions C# 開發人員參考](../azure-functions/functions-reference-csharp.md)
* [Azure Functions F# 開發人員參考](../azure-functions/functions-reference-fsharp.md)
* [Azure Functions NodeJS 開發人員參考](../azure-functions/functions-reference.md)
* [Azure Functions 觸發程序和繫結](../azure-functions/functions-triggers-bindings.md)
* [如何 toomonitor Azure Redis 快取](../redis-cache/cache-how-to-monitor.md)

toostay 最新的所有 hello 最新消息和功能，請遵循[ @AzureStreaming ](https://twitter.com/AzureStreaming) Twitter 上。

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
