---
title: "如何透過 WebJobs SDK 使用 Azure 佇列儲存體"
description: "了解如何透過 WebJobs SDK 使用 Azure 佇列儲存體。 建立和刪除查詢、插入、查看、取得和刪除佇列訊息等。"
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 63b987a2c9471f2929b8d2dd605323910d2ad43b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a>如何透過 WebJobs SDK 使用 Azure 佇列儲存體
## <a name="overview"></a>概觀
本指南提供了 C# 程式碼範例，示範如何透過 Azure 佇列儲存體服務使用 Azure WebJobs SDK 1.x 版。

本指南假設您知道[如何使用指向您儲存體帳戶的連接字串，在 Visual Studio 中建立 WebJob 專案](websites-dotnet-webjobs-sdk-get-started.md)，或是使用指向[多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)的連接字串來建立該專案。

大部分的程式碼片段只會顯示函數，不會顯示建立 `JobHost` 物件的程式碼，如此範例所示：

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

本指南包含下列主題：

* [如何在接收到佇列訊息時觸發函數](#trigger)
  * 字串佇列訊息
  * POCO 佇列訊息
  * Async 函數
  * 適用於 QueueTrigger 屬性的型別
  * 輪詢演算法
  * 多個執行個體
  * 平行執行
  * 取得佇列或佇列訊息中繼資料
  * 正常關機
* [如何在處理佇列訊息時建立佇列訊息](#createqueue)
  * 字串佇列訊息
  * POCO 佇列訊息
  * 建立多個訊息或使用非同步函式
  * 適用於 Queue 屬性的型別
  * 在函式主體中使用 WebJobs SDK 屬性
* [如何在處理佇列訊息時讀取及寫入 Blob](#blobs)
  * 字串佇列訊息
  * POCO 佇列訊息
  * 適用於 Blob 屬性的型別
* [如何處理有害訊息](#poison)
  * 自動處理有害訊息
  * 手動處理有害訊息
* [如何設定組態選項](#config)
  * 在程式碼中設定 SDK 連接字串
  * 設定 QueueTrigger 設定
  * 在程式碼中設定 WebJobs SDK 建構函式參數的值
* [如何手動觸發函數](#manual)
* [如何寫入記錄檔](#logs)
* [如何處理錯誤及設定逾時](#errors)
* [後續步驟](#nextsteps)

## <a id="trigger"></a> 如何在接收到佇列訊息時觸發函數
若要撰寫 WebJobs SDK 在收到佇列訊息時所呼叫的函數，請使用 `QueueTrigger` 屬性。 屬性建構函式採用字串參數，來指定要輪詢的佇列名稱。 您也可以 [動態設定佇列名稱](#config)。

### <a name="string-queue-messages"></a>字串佇列訊息
在下列範例中，佇列包含字串訊息，以便 套用 `QueueTrigger` 至名為 `logMessage` 的字串參數，其中包含佇列訊息的內容。 函數會 [將記錄訊息寫入儀表板](#logs)。

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

除了 `string` 之外，參數也可以是一個位元組陣列、一個 `CloudQueueMessage` 物件，或一個您定義的 POCO。

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息
在下列範例中，佇列訊息會包含 `BlobInformation` 物件的 JSON，其中包含 `BlobName` 屬性。 SDK 會自動將物件還原序列化。

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

SDK 會使用 [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) 封裝來序列化和還原序列化訊息。 如果您在不使用 WebJobs SDK 的程式中建立佇列訊息，您可以撰寫和下面範例類似的程式碼來建立 SDK 能夠剖析的 POCO 佇列訊息。

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Async 函數
下面的非同步函式會 [將記錄檔寫入儀表板](#logs)。

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Async 函數可能需要取 [消語彙基元](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)，如下列範例所示 (會複製 Blob)。 (如需 `queueTrigger` 預留位置的說明，請參閱 [Blobs](#blobs) 一節。)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a> 適用於 QueueTrigger 屬性的型別
您可以將 `QueueTrigger` 與下列型別搭配使用：

* `string`
* 序列化為 JSON 的 POCO 型別
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a> 輪詢演算法
SDK 會實作隨機指數型倒退演算法，以降低閒置佇列輪詢對儲存體交易成本的影響。  找到訊息時，SDK 會等待兩秒，然後檢查的另一個訊息；當找不到任何訊息時，它會等候大約四秒，然後再試一次。 連續嘗試取得佇列訊息失敗後，等候時間會持續增加，直到它到達等待時間上限 (預設值為一分鐘)。 [您可以設定等待時間上限](#config)。

### <a id="instances"></a> 多個執行個體
如果您的 Web 應用程式是在多個執行個體上執行，則會有一個連續的 WebJob 在每部機器上執行，而每部機器將會等待觸發程序，才嘗試執行函式。 WebJobs SDK 佇列觸發程序會自動防止函式處理佇列訊息多次；不需將函式撰寫成等冪函式。 不過，如果您想要確保在即使有多個主 Web 應用程式執行個體的情況下，仍然只有一個函式執行個體會執行，則您可以使用 `Singleton` 屬性。

### <a id="parallel"></a> 平行執行
如果您有多個函數在不同的佇列上接聽，則同時接收到訊息時，SDK 會以平行方式呼叫它們。

收到單一佇列的多個訊息時也是如此。 根據預設，SDK 會一次取得一批 (16 個) 佇列訊息，並執行以平行方式處理它們的函數。 [您可以設定批次大小](#config)。 當要處理的訊息數目減少到批次大小 (該批訊息數目) 的一半時，SDK 就會取得另一批訊息並開始處理那些訊息。 因此，每個函數並行處理之訊息的上限數目為批次大小 (該批訊息數目) 的 1.5 倍。 這項限制個別套用至具有 `QueueTrigger` 屬性的每個函式。

如果您不想要平行執行在單一佇列上收到的訊息，您可以將批次大小設定為 1。 另請參閱 **Azure WebJobs SDK 1.1.0 RTM** 中的 [更充分掌控佇列處理](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)。

### <a id="queuemetadata"></a>取得佇列或佇列訊息中繼資料
您可以透過新增參數至方法簽章來取得下列訊息屬性：

* `DateTimeOffset` expirationTime
* `DateTimeOffset` insertionTime
* `DateTimeOffset` nextVisibleTime
* `string` queueTrigger (包含訊息文字)
* `string` id
* `string` popReceipt
* `int` dequeueCount

如果您想要直接使用 Azure 儲存體 API，您也可以加入 `CloudStorageAccount` 參數。

下列範例會將此中繼資料全部寫入至 INFO 應用程式記錄檔。 在範例中，logMessage 和 queueTrigger 包含佇列訊息的內容。

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

以下是範例程式碼所寫入的範例記錄：

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <a id="graceful"></a>順利關機
在連續 WebJob 中執行的函數可以接受 `CancellationToken` 參數，該參數可讓作業系統在 WebJob 即將終止時通知函數。 您可以使用此通知來確保函數不會在讓資料維持不一致狀態的情況下意外終止。

下列範例示範如何透過函數檢查即將終止的 WebJob。

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

**注意：** 儀表板可能不會正確顯示已關閉之函數的狀態與輸出。

如需詳細資訊，請參閱 [WebJobs 正常關機](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR)。   

## <a id="createqueue"></a> 如何在處理佇列訊息時建立佇列訊息
若要編寫會建立新佇列訊息的函數，請使用 `Queue` 屬性。 就像 `QueueTrigger`一樣，您可以用字串的方式傳入佇列名稱，或者您可以 [動態設定佇列名稱](#config)。

### <a name="string-queue-messages"></a>字串佇列訊息
下面的非同步程式碼範例會在名稱為 "outputqueue" 的佇列中建立一個新的佇列訊息，其內容與名為 "inputqueue" 的佇列中收到的佇列訊息相同。 (如需非同步函式，請使用 `IAsyncCollector<T>`，如本節後續內容所示。)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息
若要建立包含 POCO 物件 (而非字串) 的佇列訊息，請將 POCO 做為輸出參數傳送至 `Queue` 屬性建構函式。

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

SDK 會自動將物件序列化為 JSON。 即使物件是空值，也一律會建立佇列訊息。

### <a name="create-multiple-messages-or-in-async-functions"></a>建立多個訊息或使用非同步函式
若要建立多個訊息，請將輸出佇列的參數型別設為 `ICollector<T>` 或 `IAsyncCollector<T>`，如下面範例所示。

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

呼叫 `Add` 方法時，就會立即建立每個佇列訊息。

### <a name="types-that-the-queue-attribute-works-with"></a>適用於 Queue 屬性的型別
您可以在下列參數型別使用 `Queue` 屬性：

* `out string` (函式結束時，如果參數值非 Null，就會建立佇列訊息)
* `out byte[]` (作用就像是 `string`)
* `out CloudQueueMessage` (作用就像是 `string`)
* `out POCO` (可序列化型別，當函式結束時，如果參數為 Null，就會使用 Null 物件建立訊息)
* `ICollector`
* `IAsyncCollector`
* `CloudQueue` (用於直接使用 Azure 儲存體 API 手動建立訊息)

### <a id="ibinder"></a>在函式主體中使用 WebJobs SDK 屬性
如果您需要先在函式中執行部分工作，然後再使用 WebJobs SDK 屬性，例如 `Queue`、`Blob`  或 `Table`，您可以使用 `IBinder` 介面。

下列範例會使用輸入佇列訊息，並在輸出佇列中建立含有相同內容的新訊息。 輸出佇列名稱會由函數主體中的程式碼設定。

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

`IBinder` 介面也能與 `Table` 和 `Blob` 屬性搭配使用。

## <a id="blobs"></a> 如何在處理佇列訊息時讀取及寫入 Blob 與表格
`Blob` 與 `Table` 屬性可讓您讀取和寫入 Blob 與資料表。 本節中的範例適用於 Blob。 如需示範如何在建立或更新 Blob 時觸發程序的程式碼範例，請參閱[如何透過 WebJobs SDK 使用 Azure Blob 儲存體](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)，若需讀取和撰寫資料表的程式碼範例，請參閱[如何透過 WebJobs SDK 使用 Azure 資料表儲存體](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)。

### <a name="string-queue-messages-triggering-blob-operations"></a>觸發 Blob 作業的字串佇列訊息
對於包含字串的佇列訊息，您可以在 `Blob` 屬性的 `blobPath` 參數中使用 `queueTrigger` 預留位置，它包含了訊息的內容。

下列範例使用 `Stream` 物件來讀取及寫入 Blob。 佇列訊息提供位於 textblobs 容器中 Blob 的名稱。 會在相同的容器中建立 Blob 的複本，並在其名稱中附加 "-new"。

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

`Blob` 屬性建構函式採用 `blobPath` 參數來指定容器與 Blob 名稱。 如需此預留位置的詳細資訊，請參閱 [如何透過 WebJobs SDK 使用 Azure Blob 儲存體](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)。

當這個屬性裝飾 `Stream` 物件，另一個建構函式參數會將 `FileAccess` 模式指定為讀取、 寫入或讀取/寫入。

下列範例使用 `CloudBlockBlob` 物件來刪除 Blob。 佇列訊息就是 Blob 的名稱。

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a> POCO ( [純舊 CLR 物件](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) 佇列訊息
對於在佇列訊息中儲存為 JSON 的 POCO 物件，您可以在 `Queue` 屬性的 `blobPath` 參數中使用指定物件屬性的預留位置。 您也可以使用 [佇列中繼資料屬性名稱](#queuemetadata) 做為預留位置。

下列範例會將 Blob 複製到具有不同副檔名的新 Blob。 佇列訊息就是包含 `BlobName` 與 `BlobNameWithoutExtension` 屬性的 `BlobInformation` 物件。 在 `Blob` 屬性的 Blob 路徑中使用屬性名稱做為預留位置。

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

SDK 會使用 [Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) 封裝來序列化和還原序列化訊息。 如果您在不使用 WebJobs SDK 的程式中建立佇列訊息，您可以撰寫和下面範例類似的程式碼來建立 SDK 能夠剖析的 POCO 佇列訊息。

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

如果您需要先在函數中執行部分工作，然後再將 Blob 繫結至物件，您可以在函數主體中使用屬性， [如之前所示的佇列屬性](#ibinder)。

### <a id="blobattributetypes"></a> 可以與 Blob 屬性搭配使用的型別
`Blob` 屬性能與下列型別搭配使用：

* `Stream` (讀取或寫入，可使用 FileAccess 建構函式參數指定)
* `TextReader`
* `TextWriter`
* `string` (讀取)
* `out string` (寫入；當函式傳回時，如果字串參數非 Null，就只會建立 Blob)
* POCO (讀取)
* out POCO (寫入；一律會建立 Blob，當函式傳回時，如果 POCO 參數為 Null，就建立為 Null 物件)
* `CloudBlobStream` (寫入)
* `ICloudBlob` (讀取或寫入)
* `CloudBlockBlob` (讀取或寫入)
* `CloudPageBlob` (讀取或寫入)

## <a id="poison"></a> 如何處理有害訊息
內容會導致函數失敗的訊息稱為「有害訊息」 。 當函數失敗時不會刪除佇列訊息，最後會再度挑選到該訊息，造成重複循環。 SDK 可在有限的反覆次數之後自動中斷循環，或者您可以手動中斷循環。

### <a name="automatic-poison-message-handling"></a>自動處理有害訊息
SDK 將會呼叫函數最多 5 次以處理佇列訊息。 如果第五次嘗試失敗，訊息便會移到有害佇列中。 [您可以設定重試次數上限](#config)。

有害佇列名為 *{originalqueuename}*-poison。 您可以撰寫函數，透過記錄或傳送通知表示需要手動處理，來處理有害佇列中的訊息。

在下列範例中，當佇列訊息包含不存在的 Blob 名稱時， `CopyBlob` 函式將會失敗。 發生時，就會從 copyblobqueue 佇列將訊息移至 copyblobqueue-poison 佇列。 `ProcessPoisonMessage` 接著會記錄有害訊息。

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
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

下圖顯示這些函數處理有害訊息之後的主控台輸出。

![主控台輸出中的有害訊息處理](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a>手動處理有害訊息
您可以將名為 `dequeueCount` 的 `int` 參數加入到函式中，來取得訊息已被挑選來處理的次數。 然後您可以檢查函數程式碼中的清除佇列計數，並在數目超出臨界值時自行執行有害訊息處理，如下面的範例所示。

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a id="config"></a> 如何設定組態選項
您可以使用 `JobHostConfiguration` 型別來設定下列組態選項：

* 在程式碼中設定 SDK 連接字串。
* 設定 `QueueTrigger` 設定，例如清除佇列計數上限。
* 從組態取得佇列名稱。

### <a id="setconnstr"></a>在程式碼中設定 SDK 連接字串
在程式碼中設定 SDK 連接字串可讓您在組態檔或環境變數中使用您自己的連接字串名稱，如下面範例所示。

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

### <a id="configqueue"></a>設定 QueueTrigger 設定
您可以配置會套用至佇列訊息處理的下列設定：

* 挑選以同時平行執行的佇列訊息數目上限 (預設值為 16)。
* 將佇列訊息傳送到有害佇列之前的重試次數上限 (預設值為 5)。
* 佇列為空的時，要再次輪詢前的等待時間上限 (預設值為 1 分鐘)。

下列範例示範如何配置這些設定：

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="setnamesincode"></a>在程式碼中設定 WebJobs SDK 建構函式參數的值
有時候您不想要採取硬式編碼的方式，而是在程式碼中指定佇列名稱、Blob 名稱或容器或資料表名稱。 例如，您可能想要在組態檔或環境變數中指定 `QueueTrigger` 的佇列名稱。

方法是將 `NameResolver` 物件傳入 `JobHostConfiguration` 型別。 在 WebJobs SDK 屬性建構函式參數中包含以百分比 (%) 符號括住的特殊預留位置，然後 `NameResolver` 程式碼會指定實際要用以取代那些預留位置的值。

例如，假設您想要在測試環境中使用名為 logqueuetest 的佇列，和在生產環境中使用名為 logqueueprod 的佇列。 您不想使用硬式編碼的佇列名稱，而想要在會有實際佇列名稱的 `appSettings` 集合中指定項目的名稱。 如果 `appSettings` 索引鍵為 logqueue，您的函式看起來可能像下面的範例。

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

`NameResolver` 類別接著可以從 `appSettings` 取得佇列名稱，如下面範例所示：

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

您將 `NameResolver` 類別傳入 `JobHost` 物件，如下面範例所示。

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**注意：** 每次呼叫函式時，都會解析佇列、資料表及 Blob 名稱，但只有在應用程式啟動時才會解析 Blob 容器名稱。 您無法在執行工作時，變更 Blob 容器名稱。

## <a id="manual"></a>如何手動觸發函數
若要手動觸發函式，請在函式的 `JobHost` 物件與 `NoAutomaticTrigger` 屬性上使用 `Call` 或 `CallAsync` 方法，如下列範例所示。

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

## <a id="logs"></a>如何寫入記錄檔
儀表板會在兩個地方顯示記錄檔：WebJob 的頁面與特定 WebJob 引動過程的頁面。

![WebJob 頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![函式引動過程頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

您在函式或在 `Main()` 方法中所呼叫主控台方法的輸出會顯示在 WebJob 的 [儀表板] 頁面，而不是特定方法引動過程的頁面。 您從方法簽章的參數所取得 TextWriter 物件的輸出會顯示在方法引動過程的 [儀表板] 頁面。

因為主控台屬於單一執行緒，無法同時執行許多工作函式，所以主控台輸出無法連結到特定的方法引動過程。 這就是 SDK 提供的每個函式引動過程都使用自己專屬的記錄寫入器物件的原因。

若要寫入[應用程式追蹤記錄](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview)，請使用 `Console.Out` (建立標示為 INFO 的記錄檔) 與 `Console.Error` (建立標示為 ERROR 的記錄檔)。 替代方法是使用 [Trace 或 TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)，除了資訊與錯誤之外，還能提供詳細資訊、警告及嚴重層級。 視您設定 Azure 網頁應用程式的方式而定，應用程式追蹤記錄檔會出現在網頁應用程式記錄檔、Azure 資料表或 Azure Blob 中。 所有主控台輸出的應用程式記錄檔裡最近的 100 筆記錄也同樣會顯示在 WebJob 的 [儀表板] 頁面，而不是函式引動過程的頁面。

只有當程式是以 Azure WebJob 執行時，主控台輸出才會顯示在儀表板，而不是在本機或在某些其他環境中執行時。

停用針對高輸送量的儀表板記錄。 根據預設，SDK 會將記錄寫入儲存體，而且在處理許多訊息時，這項活動可能會降低效能。 若要停用記錄，請將儀表板連接字串設定為 null，如下列範例所示。

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

下列範例示範寫入記錄檔的數種方式：

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

在 WebJobs SDK 儀表板中，當您移到某個特定函式引動過程的頁面並按一下 [切換輸出] 時，就會顯示來自 `TextWriter` 物件的輸出：

![按一下函式引動過程連結](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![函式引動過程頁面中的記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

在 WebJobs SDK 儀表板中，當您移到 WebJob (而非函式引動過程) 的頁面並按一下 [切換輸出] 時，則會顯示主控台輸出最近的 100 行。

![按一下切換輸出](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

在連續的 WebJob 中，應用程式記錄檔顯示在 Web 應用程式檔案系統中的 /data/jobs/continuous/*{webjobname}*/job_log.txt。

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

在 Azure Blob 中，應用程式記錄檔看起來如下所示：2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,

而在 Azure 資料表中，`Console.Out` 和 `Console.Error` 記錄檔看起來像這樣：

![在資料表中的資訊記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![在資料表中的錯誤記錄檔](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

如果您想要插入自己的記錄器，請參閱 [這個範例](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs)。

## <a id="errors"></a>如何處理錯誤及設定逾時
WebJobs SDK 也包含 [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) 屬性，您可以使用此屬性讓函式在未於指定的時間長度內完成時取消執行。 而如果您想要在於一段指定的時間內有太多錯誤發生時引發警示，則可以使用 `ErrorTrigger` 屬性。 以下是一個 [ErrorTrigger 範例](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring)。

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

您也可以藉由使用組態參數 (可以是應用程式設定或環境變數名稱)，動態停用和啟用函式來控制是否可以觸發這些函式。 如需範例程式碼，請參閱 [WebJobs SDK 範例儲存機制](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs)中的 `Disable` 屬性。

## <a id="nextsteps"></a> 後續步驟
本指南提供的程式碼範例示範如何處理使用 Azure 佇列的常見案例。 如需 Azure WebJobs 和 WebJobs SDK 的詳細資訊，請參閱 [Azure WebJobs 建議使用的資源](http://go.microsoft.com/fwlink/?linkid=390226)。
