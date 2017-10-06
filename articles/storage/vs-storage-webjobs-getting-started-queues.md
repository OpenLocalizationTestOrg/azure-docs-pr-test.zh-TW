---
title: "開始使用佇列儲存體和 Visual Studio 已連線的服務 （WebJob 專案） 的 aaaGetting |Microsoft 文件"
description: "如何 tooget 啟動 WebJob 專案中使用 Azure 佇列儲存體之後連接 tooa 儲存體帳戶，使用 Visual Studio 已連接服務。"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 (WebJob 專案)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>概觀
本文說明如何開始使用 Azure 佇列中的 Visual Studio Azure WebJob 專案之後，您建立或使用參考 Azure 儲存體帳戶的儲存體 hello Visual Studio**加入已連接服務** 對話方塊。 當您使用 Visual Studio hello 新增儲存體帳戶 tooa WebJob 專案**加入已連接服務** 對話方塊中，hello 適當的 Azure 儲存體 NuGet 封裝已安裝，不會加入的 toohello hello 適當的.NET 參考專案和 hello 儲存體帳戶的連接字串會更新在 hello App.config 檔案中。  

本文章提供 C# 程式碼範例，示範如何 toouse hello Azure WebJobs SDK 版本 1.x 以 hello Azure 佇列儲存體服務。

Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。 單一佇列訊息可以是總 too64 KB 的大小，並佇列可以包含數百萬個訊息，向上 toohello 總容量限制的儲存體帳戶。 如需詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](storage-dotnet-how-to-use-queues.md) 。 如需 ASP.NET 的詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>如何 tootrigger 接收佇列訊息時的函式
toowrite hello WebJobs SDK 的函式呼叫接收佇列訊息時，請使用 hello **QueueTrigger**屬性。 hello 屬性建構函式接受字串參數，指定 hello 佇列 toopoll hello 名稱。 toosee 如何 tooset hello 佇列名稱，以動態方式簽出[如何 tooset 組態選項](#how-to-set-configuration-options)。

### <a name="string-queue-messages"></a>字串佇列訊息
在下列範例的 hello，hello 佇列包含字串訊息，因此**QueueTrigger**是套用的 tooa 字串參數名稱為**logMessage**包含 hello hello 佇列訊息內容。 hello 函式[寫入記錄檔訊息 toohello 儀表板](#how-to-write-logs)。

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

除了**字串**，hello 參數可以是位元組陣列， **CloudQueueMessage**物件或您定義 POCO。

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息
在下列範例的 hello，hello 佇列訊息包含的 JSON **BlobInformation**物件，其中包括**BlobName**屬性。 hello SDK 會自動將 hello 物件還原序列化。

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

hello SDK 會使用 hello [Newtonsoft.Json NuGet 套件](http://www.nuget.org/packages/Newtonsoft.Json)tooserialize 和還原序列化訊息。 如果您未使用 hello WebJobs SDK 的程式中建立訊息排入佇列，您可以撰寫程式碼，如下列範例 toocreate POCO 佇列訊息的 hello SDK 可以剖析該 hello。

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Async 函數
遵循 async 函式的 hello[寫入記錄檔 toohello 儀表板](#how-to-write-logs)。

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

非同步函式可能需要[取消語彙基元](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)，如下列範例複製 blob 的 hello 所示。 (如需說明的 hello **queueTrigger**預留位置，請參閱 hello [Blob](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) > 一節。)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>適用於類型 hello QueueTrigger 屬性
您可以使用**QueueTrigger**以 hello 下列類型：

* **字串**
* 序列化為 JSON 的 POCO 型別
* **byte[]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>輪詢演算法
hello SDK 實作閒置佇列輪詢對於儲存體交易成本的隨機指數型撤退演算法 tooreduce hello 的效果。  Hello SDK 找到訊息時，會等待兩秒，並且接著會檢查其他訊息;找到沒有訊息時它會等候大約四個秒後再試一次。 後續的嘗試失敗的 tooget 佇列訊息之後, hello 等候時間持續 tooincrease 直到達到 hello 最長等待時間的預設值 tooone 分鐘。 [hello 最長等待時間是可設定](#how-to-set-configuration-options)。

## <a name="multiple-instances"></a>多個執行個體
如果您的 web 應用程式在多個執行個體上執行，每個電腦上執行的連續 web 工作和每一部機器將會等候觸發程序，並嘗試 toorun 函式。 在某些情況下，這可能會導致 toosome 函式處理 hello 相同的資料兩次，因此函式應該具有等冪性 （寫入因此重複呼叫以 hello 不會產生相同的輸入的資料重複的結果）。  

## <a name="parallel-execution"></a>平行執行
如果您有多個函式在不同的佇列上接聽，hello SDK 會呼叫它們以平行方式同時接收訊息時。

hello 也是如此單一佇列接收多個訊息時。 根據預設，hello SDK 取得 16 的佇列訊息的批次，一次，並執行以平行方式處理它們的 hello 函式。 [hello 批次大小是可設定](#how-to-set-configuration-options)。 當正在處理的 hello 數目取得 toohalf hello 批次大小的清單時，hello SDK 取得另一個批次，並開始處理這些訊息。 因此 hello 的並行處理每個函式的訊息數目上限是一倍半 hello 批次大小。 這項限制會分別套用 tooeach 函式具有**QueueTrigger**屬性。 如果您不想平行執行的上一個佇列接收訊息，設定 hello 批次大小 too1。

## <a name="get-queue-or-queue-message-metadata"></a>取得佇列或佇列訊息中繼資料
您可以取得下列訊息屬性加入參數 toohello 方法簽章的 hello:

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **string** queueTrigger (包含訊息文字)
* **string** id
* **string** popReceipt
* **int** dequeueCount

如果您想 toowork 直接與 hello Azure 儲存體 API，您也可以加入**CloudStorageAccount**參數。

hello 下列範例會將所有寫入此中繼資料 tooan 資訊應用程式記錄檔。 在 hello 範例中，則為 logMessage 和 queueTrigger 包含 hello hello 佇列訊息內容。

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

以下是範例記錄檔寫入 hello 範例程式碼：

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a>正常關機
在連續 web 工作執行的函式可以接受**CancellationToken**參數可讓 hello 作業系統 toonotify hello 函式時 hello WebJob 即將 toobe 終止。 您可以使用此通知 toomake 確定 hello 函式不會意外終止，使資料處於不一致狀態的方式。

下列範例會示範如何 hello toocheck 即將發生的 WebJob 終止函式中。

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**注意：** hello 儀表板，可能無法正確顯示 hello 狀態和已關閉的函式的輸出。

如需詳細資訊，請參閱 [WebJobs 正常關機](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR)。   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>Toocreate 佇列處理的佇列訊息時訊息的方式
toowrite 函式會建立新的佇列訊息，使用 hello**佇列**屬性。 像**QueueTrigger**、 您要傳入 hello 佇列名稱做為字串，或您可以[動態設定 hello 佇列名稱](#how-to-set-configuration-options)。

### <a name="string-queue-messages"></a>字串佇列訊息
hello 下列非非同步程式碼範例會建立新的佇列訊息，名為"outputqueue"hello 佇列中以內容為 hello 佇列訊息相同收到 hello 佇列名為"inputqueue 」 中的 hello。 (如需非同步函式，請使用 **IAsyncCollector<T>**，如本節後續內容所示。)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息
toocreate 包含 POCO，而不是字串時，傳遞 hello POCO 的佇列訊息型別作為輸出參數 toohello**佇列**屬性建構函式。

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

hello SDK 自動序列化 hello 物件 tooJSON。 一律建立佇列訊息，即使 hello 物件為 null。

### <a name="create-multiple-messages-or-in-async-functions"></a>建立多個訊息或使用非同步函式
toocreate 多則訊息，請 hello 輸出佇列的 hello 參數類型**ICollector<T>** 或**IAsyncCollector<T>**hello 下列範例所示。

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

每個佇列的訊息建立時立即 hello**新增**方法呼叫。

### <a name="types-that-hello-queue-attribute-works-with"></a>型別適用於該 hello 佇列屬性
您可以使用 hello**佇列**hello 下列參數類型的屬性：

* **字串**（如果參數值為非 null，hello 函式結束時，會建立佇列訊息）
* **out byte[]** (運作方式類似 **字串**)
* **out CloudQueueMessage** (運作方式類似 **字串**)
* **POCO 出**（可序列化的型別，如果會建立訊息的 null 物件 hello 參數為 null，hello 函式結束時）
* **ICollector**
* **IAsyncCollector**
* **CloudQueue** (手動建立訊息使用 hello Azure 儲存體 API 直接)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>使用 WebJobs SDK hello 函式主體中的屬性
如果您需要 toodo 一些適用於您的函式之前使用 WebJobs SDK 屬性，例如**佇列**， **Blob**，或**資料表**，您可以使用 hello **IBinder**介面。

hello 下列範例會採用輸入的佇列訊息，並以相同的內容中輸出佇列的 hello 建立新的訊息。 hello 輸出佇列名稱是由 hello hello 函式主體中的程式碼設定。

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

hello **IBinder**介面也可以搭配 hello**資料表**和**Blob**屬性。

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>Tooread 和寫入的 blob 和資料表處理佇列訊息時
hello **Blob**和**資料表**屬性 tooread 可讓您和寫入 blob 和資料表。 本節中的 hello 範例套用 tooblobs。 程式碼範例，示範如何 tootrigger 處理當建立或更新的 blob 時，請參閱[toouse Azure blob 儲存體與 hello WebJobs SDK 的方式](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)，以及讀取和寫入資料表的程式碼範例，請參閱[如何 toouse Azure 資料表儲存體與 hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md)。

### <a name="string-queue-messages-triggering-blob-operations"></a>觸發 Blob 作業的字串佇列訊息
包含字串，佇列訊息**queueTrigger**是的預留位置，您可以使用在 hello **Blob**屬性的**blobPath**包含 hello 內容參數hello 訊息。

hello 下列範例會使用**資料流**物件 tooread 和寫入 blob。 hello 佇列訊息是 blob 的 hello 位於 hello textblobs 容器中名稱。 一份 hello blob"-新 「 附加的 toohello 名稱中建立 hello 相同容器。

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

hello **Blob**屬性建構函式會採用**blobPath**指定 hello 容器和 blob 名稱的參數。 如需這個預留位置的詳細資訊，請參閱[如何 toouse Azure blob 儲存體與 hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)。

當 hello 屬性裝飾**資料流**物件，另一個建構函式參數指定 hello **FileAccess**為讀取、 寫入或讀取/寫入模式。

hello 下列範例會使用**CloudBlockBlob**物件 toodelete blob。 hello 佇列訊息是 hello hello blob 名稱。

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息
POCO，以 JSON 格式儲存在 hello 佇列訊息，您可以使用該名稱在 hello 的 hello 物件內容的預留位置**佇列**屬性的**blobPath**參數。 您也可以使用佇列中繼資料屬性名稱做為預留位置。 請參閱 [取得佇列或佇列訊息中繼資料](#get-queue-or-queue-message-metadata)。

hello 下列範例會複製不同的擴充功能的 blob tooa 新 blob。 hello 佇列訊息是**BlobInformation**物件，其中包含**BlobName**和**BlobNameWithoutExtension**屬性。 hello 屬性名稱作為 hello blob 路徑中的預留位置 hello **Blob**屬性。

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

hello SDK 會使用 hello [Newtonsoft.Json NuGet 套件](http://www.nuget.org/packages/Newtonsoft.Json)tooserialize 和還原序列化訊息。 如果您未使用 hello WebJobs SDK 的程式中建立訊息排入佇列，您可以撰寫程式碼，如下列範例 toocreate POCO 佇列訊息的 hello SDK 可以剖析該 hello。

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

如果您需要函式中的某些工作的 toodo 繫結 blob tooan 物件之前，您可以使用 hello hello 函式，主體中的 hello 屬性中所示[hello 函式主體中的使用 WebJobs SDK 屬性](#use-webjobs-sdk-attributes-in-the-body-of-a-function)。

### <a name="types-you-can-use-hello-blob-attribute-with"></a>您可以使用 hello 類型 Blob 屬性
hello **Blob**屬性可用以 hello 下列類型：

* **資料流**（讀取或寫入使用 hello FileAccess 建構函式參數所指定）
* **TextReader**
* **TextWriter**
* **string** (讀取)
* **字串**（寫入; hello 字串參數為非 null，當 hello 函式傳回時，才會建立 blob）
* POCO (讀取)
* POCO 出撰寫; 一律建立的 blob (如果 POCO 參數為 null，hello 函式傳回時，會建立為 null 的物件）
* **CloudBlobStream** (寫入)
* **ICloudBlob** (讀取或寫入)
* **CloudBlockBlob** (讀取或寫入)
* **CloudPageBlob** (讀取或寫入)

## <a name="how-toohandle-poison-messages"></a>如何 toohandle 有害訊息
訊息內容會導致函式 toofail 稱為*有害訊息*。 Hello 函式失敗時，不會刪除 hello 佇列訊息，且最終會收取一次，導致 hello 循環 toobe 重複。 hello SDK 可以自動中斷 hello 循環之後有限數目的反覆項目，或手動進行。

### <a name="automatic-poison-message-handling"></a>自動處理有害訊息
hello SDK 會呼叫向上 too5 時間 tooprocess 佇列訊息的函式。 如果 hello 第五個再試一次失敗，hello 訊息是移動的 tooa 有害佇列。 您可以查看如何 tooconfigure hello 中重試次數上限[如何 tooset 組態選項](#how-to-set-configuration-options)。

hello 有害佇列名為*{originalqueuename}*-有害。 您可以撰寫函式 tooprocess 訊息從 hello 有害佇列記錄或傳送通知，需要進行手動處理。

在下列範例 hello hello **copyblob 應用程式開發**佇列訊息包含 hello 名稱不存在的 blob 時，函式將會失敗。 當發生這種情況時，hello 訊息移動 hello copyblobqueue 佇列 toohello copyblobqueue 有害佇列中。 hello **ProcessPoisonMessage**則記錄檔 hello 有害訊息。

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

hello 如下圖所示這些函式的主控台的輸出處理有害訊息時。

![主控台輸出中的有害訊息處理](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>手動處理有害訊息
您可以新增取得 hello 取用訊息的次數處理**int**參數名為**dequeueCount** tooyour 函式。 接著，您可以核取 hello 清除佇列計數在函式程式碼和執行您自己有害訊息處理時所 hello 超過臨界值，如 hello 下列範例所示。

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a>如何 tooset 組態選項
您可以使用 hello **JobHostConfiguration**類型 tooset hello 下列組態選項：

* 程式碼中設定 hello SDK 連接字串。
* 配置 **QueueTrigger** 設定，例如清除佇列計數上限。
* 從組態取得佇列名稱。

### <a name="set-sdk-connection-strings-in-code"></a>在程式碼中設定 SDK 連接字串
程式碼中設定 hello SDK 連接字串可讓您 toouse 自己組態檔或環境變數中的連接字串名稱 hello 下列範例所示。

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a>設定 QueueTrigger 設定
您可以設定下列設定適用於 toohello 佇列的訊息處理 hello:

* hello 同時平行執行的 toobe 會收取的佇列訊息的最大數目 （預設值為 16）。
* hello 佇列訊息傳送 tooa 有害佇列之前的重試次數上限 （預設值為 5）。
* hello 最長等待時間之前再次輪詢佇列空的時 （預設值為 1 分鐘）。

下列範例會示範如何 hello tooconfigure 這些設定：

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>在程式碼中設定 WebJobs SDK 建構函式參數的值
有時候您會想 toospecify 佇列名稱、 blob 名稱或容器，或資料表名稱在程式碼，而不是硬式編碼它。 例如，您可能會想 toospecify hello 佇列名稱**QueueTrigger**組態檔或環境變數中。

您可以執行此動作，傳遞**NameResolver**物件 toohello **JobHostConfiguration**型別。 您加入特殊的預留位置包圍百分比 （%） 符號 WebJobs SDK 屬性建構函式參數，而您**NameResolver**程式碼會指定用來取代這些預留位置 hello 實際值 toobe。

例如，假設您想要 toouse 佇列名為 logqueuetest hello 測試環境和生產環境中的一個具名的 logqueueprod。 而不是硬式編碼的佇列名稱，您會想 toospecify hello hello 中的項目名稱**appSettings**必須 hello 實際的佇列名稱的集合。 如果 hello **appSettings**索引鍵是 logqueue、 您的函式可能看起來像下列範例中的 hello。

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

您**NameResolver**類別無法再取得 hello 佇列名稱，從**appSettings** hello 下列範例所示：

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

您傳遞 hello **NameResolver**類別中 toohello **JobHost**物件 hello 下列範例所示。

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**注意：**佇列、 資料表和 blob 名稱，會解析每次呼叫函式，但 hello 應用程式啟動時，才解析 blob 容器名稱。 Hello 作業執行時，您無法變更 blob 容器名稱。

## <a name="how-tootrigger-a-function-manually"></a>如何 tootrigger 函式以手動方式
tootrigger 函式以手動方式，使用 hello**呼叫**或**CallAsync**方法上 hello **JobHost**物件和 hello **NoAutomaticTrigger**在 hello 函式，如下列範例中的 hello 中所示的屬性。

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-toowrite-logs"></a>Toowrite 的記錄檔
hello 儀表板會顯示記錄檔中兩個地方： hello 分頁的 hello WebJob 及在特定的 WebJob 呼叫 hello 頁面。

![WebJob 頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![函式引動過程頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

從主控台的方法，讓您呼叫的函式中或在 hello 輸出**main （)**方法會出現，而非在特定的方法引動過程的 hello 頁面中的 hello WebJob hello 儀表板頁面。 從您自參數取得您的方法簽章中的 hello TextWriter 物件的輸出會出現在方法引動過程的 hello 儀表板頁面。

主控台輸出無法連結的 tooa 特定的方法引動過程，因為 hello 主控台時，單一執行緒，可能會在 hello 執行許多工作函式相同的時間。 這就是為什麼 hello SDK 提供與它自己唯一的記錄寫入器物件的每個函式引動過程。

toowrite[應用程式的追蹤記錄檔](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview)，使用**Console.Out** （建立標示為資訊的記錄檔） 和**Console.Error** （建立標示為錯誤記錄檔）。 替代方式是 toouse[追蹤或 TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)、 提供詳細資訊，警告和嚴重層級中加入 tooInfo 和錯誤。 應用程式的追蹤記錄檔會出現在 hello web 應用程式記錄檔，Azure 資料表，或 Azure blob，根據您設定您的 Azure web 應用程式的方式。 如為 true 的所有主控台輸出，hello 最近 100 應用程式記錄檔也會出現在 hello WebJob，不 hello 頁面函式的引動過程的 hello 儀表板頁面。

主控台輸出會出現在 hello 儀表板才 hello 程式執行 Azure WebJob，除非 hello 程式在本機執行或某些其他環境中。

您可以藉由設定 hello 儀表板連線字串 toonull 停用記錄。 如需詳細資訊，請參閱[如何 tooset 組態選項](#how-to-set-configuration-options)。

hello 下列範例顯示數種方式 toowrite 記錄檔：

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

Hello WebJobs SDK 儀表板，在 hello 輸出 hello **TextWriter**物件顯示當您移至特定的 toohello 頁面函式引動過程，並選取**切換輸出**:

![叫用連結](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![函式引動過程頁面中的記錄檔](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Hello WebJobs SDK 儀表板，在主控台的最新的 100 hello 行時，將輸出顯示向上移至 toohello 頁面 hello WebJob （不適用於 hello 函式引動過程），然後選取**切換輸出**。

![TextWriter](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

在連續的 WebJob，應用程式記錄檔中顯示/資料/工作/連續/*{webjobname}*/job_log.txt hello web 應用程式檔案系統中的。

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

在 Azure blob hello 應用程式記錄檔，看起來像這樣： 2014年-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write-Hello world ！、 2014年-09-26T21:01:13，錯誤，contosoadsnew，491e54，635473620738373502,0,17404,19,Console.Error-Hello world ！、 2014年-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out-Hello world ！，

在 Azure 資料表 hello **Console.Out**和**Console.Error**記錄看起來像這樣：

![在資料表中的資訊記錄檔](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![在資料表中的錯誤記錄檔](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>後續步驟
本文提供的程式碼範例會顯示如何以使用 Azure 佇列 toohandle 常見案例。 如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?linkid=390226)。

