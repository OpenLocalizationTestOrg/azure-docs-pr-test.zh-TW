---
title: "aaaHow toouse 以 hello WebJobs SDK 的 Azure blob 儲存體"
description: "了解如何 toouse Azure blob 儲存體與 hello WebJobs SDK。 在容器中出現新的 Blob 時觸發程序並處理「有害 Blob」 。"
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a>如何 toouse Azure blob 儲存體與 hello WebJobs SDK
## <a name="overview"></a>概觀
本指南提供 C# 程式碼範例會顯示如何 tootrigger 處理程序時建立或更新 Azure blob。 hello 程式碼範例使用[WebJobs SDK](websites-dotnet-webjobs-sdk.md)版本 1.x。

如需顯示 toocreate 的 blob 的程式碼範例，請參閱[如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。 

hello 指南假設您知道[toocreate WebJob 專案在 Visual Studio 中使用連接字串該點 tooyour 儲存體帳戶的方式](websites-dotnet-webjobs-sdk-get-started.md)或太[多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)。

## <a id="trigger"></a>如何 tootrigger 時建立或更新 blob 的函式
此區段會顯示如何 toouse hello`BlobTrigger`屬性。 

> [!NOTE]
> hello WebJobs SDK 掃描記錄檔 toowatch 的新增或變更的 blob。 此程序不是即時;函式可能不會觸發直到幾分鐘的時間或更久之後建立 hello 的 blob。 此外， [儲存體記錄檔建立在「竭盡所能」](https://msdn.microsoft.com/library/azure/hh343262.aspx) 的基礎上；並不保證會擷取所有事件。 在某些情況下可能會遺失記錄檔。 如果 hello blob 觸發程序的速度和可靠性限制不適用於您的應用程式，hello 建議的方法是 toocreate 佇列訊息，當您建立 hello blob，並使用 hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger)屬性，而非hello`BlobTrigger`處理 hello blob 的 hello 函式上的屬性。
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>適用於含有副檔名之 Blob 名稱的單一預留位置
hello 下列程式碼範例顯示的文字 blob 中複製 hello*輸入*容器 toohello*輸出*容器：

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

hello 屬性建構函式接受字串參數，指定 hello 容器名稱和 hello blob 名稱的預留位置。 在此範例中，如果 blob 名稱*Blob1.txt*會建立在 hello*輸入*容器，hello 函式會建立名為 blob *Blob1.txt*在 hello*輸出*容器。 

Hello，下列程式碼範例所示，您可以指定 hello blob 名稱的預留位置，以名稱模式：

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

此程式碼只會複製以 "original-" 做為名稱開頭的 Blob。 例如，*原始 Blob1.txt*在 hello*輸入*太複製容器*複製 Blob1.txt*在 hello*輸出*容器。

如果您需要 toospecify 名稱模式的 blob 名稱 hello 名稱中有大括號時，請按兩下 hello 大括號。 例如，如果您想要在 hello toofind blob*映像*容器名稱如下：

        {20140101}-soundfile.mp3

針對您的模式使用下一行程式碼：

        images/{{20140101}}-{name}

在 hello 範例 hello*名稱*預留位置的值會是*soundfile.mp3*。 

### <a name="separate-blob-name-and-extension-placeholders"></a>個別的 Blob 名稱和副檔名預留位置
hello 下列程式碼範例會變更 hello 副檔名為複製 blob 出現在 hello*輸入*容器 toohello*輸出*容器。 hello 程式碼會記錄 hello 延伸模組的 hello*輸入*blob 和設定 hello 延伸模組的 hello*輸出*太 blob*.txt*。

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a id="types"></a>您可以繫結 tooblobs 類型
您可以使用 hello `BlobTrigger` hello 下列類型的屬性：

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* 透過 [ICloudBlobStreamBinder](#icbsb) 

如果您想 toowork 直接與 hello Azure 儲存體帳戶，您也可以加入`CloudStorageAccount`參數 toohello 方法簽章。

如需範例，請參閱 hello [blob 上 GitHub.com hello azure-webjobs-sdk 儲存機制中的繫結程式碼](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs)。

## <a id="string"></a>取得繫結 toostring 文字 blob 內容
如果預期文字 blob，`BlobTrigger`可以套用的 tooa`string`參數。 hello 下列程式碼範例會將繫結文字 blob tooa`string`參數名為`logMessage`。 hello 函式會使用該參數 toowrite hello 的內容 hello blob toohello WebJobs SDK 儀表板。 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a> 使用 ICloudBlobStreamBinder 來取得序列化的 Blob 內容
hello 下列程式碼範例會使用類別可實作`ICloudBlobStreamBinder`tooenable hello`BlobTrigger`屬性 toobind blob toohello`WebImage`型別。

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

hello`WebImage`繫結程式碼中提供`WebImageBinder`類別衍生自`ICloudBlobStreamBinder`。

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a>取得觸發 blob hello hello blob 路徑
tooget hello 容器名稱和 blob 名稱的 hello blob 的已觸發 hello 函式，包括`blobTrigger`字串 hello 函式簽章中的參數。

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Toohandle 有害的 blob
當`BlobTrigger`函式失敗，hello SDK 呼叫它一次，以防 hello 失敗由暫時性錯誤所造成。 如果 hello 失敗因為 hello 的 hello blob 的內容，hello 函式會失敗，每次嘗試 tooprocess hello blob。 根據預設，hello SDK 會呼叫 too5 時間的函式，針對指定的 blob。 Hello SDK 如果 hello 第五個再試一次失敗時，加入名為訊息 tooa 佇列*webjobs-blobtrigger-有害*。

hello 重試次數上限是可設定的。 hello 相同[MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue)設定用於有害的 blob 處理和有害佇列訊息處理。 

hello 佇列訊息的有害的 blob 是 JSON 物件，包含下列屬性的 hello:

* FunctionId (hello 格式*{web 工作名稱}*。函式。*{函式名稱}*，例如： WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" 或 "PageBlob")
* ContainerName
* BlobName
* ETag (Blob 版本識別碼，例如："0x8D1DC6E70A277EF")

在 hello 下列程式碼範例，hello`CopyBlob`函式有造成 toofail 每次呼叫時的程式碼。 Hello SDK 呼叫它的 hello 重試次數上限，訊息會建立 hello blob 有害佇列，而且 hello 處理該訊息之後`LogPoisonBlob`函式。 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

hello SDK 自動還原序列化 hello JSON 訊息。 以下是 hello`PoisonBlobMessage`類別： 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a> Blob 輪詢演算法
hello WebJobs SDK 會掃描所指定的所有容器`BlobTrigger`於應用程式啟動的屬性。 在大型儲存體帳戶中，這個掃描需要花費一些時間，因此，可能需要一段時間才能找到新的 Blob 以及執行 `BlobTrigger` 函數。

toodetect 新增或變更 blob 應用程式啟動之後，hello SDK 定期從 hello blob 儲存體讀取記錄。 或 hello blob 記錄檔會進行緩衝處理，只取得實際寫入每隔 10 分鐘，因此可能有明顯的延遲後建立或更新之前 hello 對應 blob`BlobTrigger`函式會執行。 

發生例外狀況的 blob，您使用建立的 hello`Blob`屬性。 當 hello WebJobs SDK 建立新的 blob 時，它會立即傳 hello 新 blob tooany 比對`BlobTrigger`函式。 因此如果您有 blob 輸入和輸出的鏈結，hello SDK 可以處理這些有效率。 但是，如果您想要降低在針對透過其他方法建立或更新的 Blob 執行 Blob 處理函數時的延遲，建議使用 `QueueTrigger` 而非 `BlobTrigger`。

### <a id="receipts"></a> Blob 回條
hello WebJobs SDK 可確保沒有`BlobTrigger`函式會呼叫一次以上 hello 相同新增或更新 blob。 其做法是維護*blob 回條*順序 toodetermine 如果已處理指定的 blob 版本中。

Blob 的回條會儲存在名為容器*azure webjobs 託管*hello hello AzureWebJobsStorage 連接字串所指定的 Azure 儲存體帳戶中。 Blob 的回條具有 hello 下列資訊：

* hello hello blob 所呼叫函式 (「*{web 工作名稱}*。函式。*{函式名稱}*"，例如:"WebJob1.Functions.CopyBlob")
* hello 容器名稱
* hello blob 類型 （"BlockBlob"或"PageBlob"）
* hello blob 名稱
* hello ETag (例如 blob 版本識別碼:"0x8D1DC6E70A277EF")

如果您想 tooforce 重新處理的 blob，您可以手動刪除該 blob 的 hello blob 回條 hello *azure webjobs 託管*容器。

## <a id="queues"></a>Hello 佇列文章所涵蓋的相關的主題
如需如何 toohandle blob 處理觸發佇列訊息，或 WebJobs SDK 案例不特定 tooblob 處理，請參閱[如何 toouse Azure 佇列儲存體與 hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)。 

在該文件中涵蓋的相關的主題 hello 如下：

* Async 函數
* 多個執行個體
* 正常關機
* 使用 WebJobs SDK hello 函式主體中的屬性
* 程式碼中設定 hello SDK 連接字串。
* 在程式碼中設定 WebJobs SDK 建構函式參數的值
* 設定 `MaxDequeueCount` 來處理有害的 Blob。
* 手動觸發函式
* 寫入記錄檔

## <a id="nextsteps"></a> 後續步驟
本指南提供的程式碼範例，顯示 toohandle 常見的案例來處理 Azure 的 blob。 如需有關如何 toouse Azure WebJobs 和 hello WebJobs SDK，請參閱[Azure WebJobs 建議資源](http://go.microsoft.com/fwlink/?linkid=390226)。

