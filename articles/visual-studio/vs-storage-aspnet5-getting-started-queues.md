---
title: "使用佇列儲存體和 Visual Studio 啟動 aaaGet 已連線的服務 (ASP.NET Core) |Microsoft 文件"
description: "Tooget 啟動 Visual Studio 中的 ASP.NET Core 專案中使用 Azure 佇列儲存體的方式"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 90c1ebcb6a2eac6bc4f6b69133bdf3135d359a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>開始使用佇列儲存體和 Visual Studio 已連接服務 (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>概觀
本文說明如何 tooget 啟動 Visual Studio 中使用 Azure 佇列儲存體之後您建立或使用 Visual Studio hello 參考 Azure 儲存體帳戶中的 ASP.NET Core 專案,**加入已連接服務**對話方塊。 hello**加入已連接服務**作業安裝在您的專案中的適當 NuGet 封裝 tooaccess hello Azure 儲存體，並新增 hello 連接字串，hello 儲存體帳戶 tooyour 專案組態檔。

Azure 佇列儲存體是用於儲存大量訊息，可透過使用 HTTP 或 HTTPS 驗證呼叫的 hello world 中從任何地方存取服務。 單一佇列訊息可以是總 too64 (kb) 的大小，並佇列可以包含數百萬個訊息，向上 toohello 總容量限制的儲存體帳戶。

tooget 開始，您必須先 toocreate Azure 佇列儲存體帳戶中。 我們將為您示範如何 toocreate 程式碼中的佇列。 我們也會顯示您如何 tooperform 基本佇列作業，例如加入、 修改、 讀取，以及移除佇列的訊息。 hello 範例以 C 撰寫\#程式碼和使用適用於.NET 的 hello Azure 儲存體用戶端程式庫。 如需 ASP.NET 的詳細資訊，請參閱 [ASP.NET](http://www.asp.net)。

**注意：** hello 執行呼叫 tooAzure 儲存體中 ASP.NET Core Api 部分都是非同步。 如需詳細資訊，請參閱 [使用 Async 和 Await 進行非同步程式設計](http://msdn.microsoft.com/library/hh191443.aspx) 。 下列程式碼 hello 假設正在使用非同步程式設計的方法。

* 如需以程式設計方式處理佇列的詳細資訊，請參閱 [以 .NET 開始使用 Azure 佇列儲存體](../storage/queues/storage-dotnet-how-to-use-queues.md) 。
* 如需 Azure 儲存體的一般資訊，請參閱 [儲存體文件](https://azure.microsoft.com/documentation/services/storage/) 。
* 如需 Azure 雲端服務的一般資訊，請參閱 [雲端服務文件](https://azure.microsoft.com/documentation/services/cloud-services/) 。
* 若需要如何編寫 ASP.NET 應用程式的詳細資訊，請參閱 [ASP.NET](http://www.asp.net) 。

## <a name="access-queues-in-code"></a>在程式碼中存取佇列
tooaccess 佇列 ASP.NET Core 專案中的，您需要 tooinclude hello 下列存取 Azure 佇列儲存體的項目 tooany C# 原始程式檔。

1. 請確定在 hello hello C# 檔案最上方的 hello 命名空間宣告包括**使用**陳述式。
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. 取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。 下列程式碼 tooget 使用 hello hello 您的儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態。
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. 取得**CloudQueueClient** tooreference hello 佇列物件儲存體帳戶中的物件。  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. 取得**CloudQueue** tooreference 特定佇列的物件。
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**注意：** hello 遵循範例中使用所有 hello hello 程式碼前面的程式碼上方。

### <a name="create-a-queue-in-code"></a>在程式碼中建立佇列
toocreate hello Azure 佇列中的程式碼，只要加入呼叫太**CreateIfNotExistsAsync**。

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>新增訊息 tooa 佇列
tooinsert 將訊息插入現有佇列，建立新**CloudQueueMessage**物件，然後呼叫 hello **AddMessageAsync**方法。

您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 物件。

以下是範例插入 'Hello World' hello 訊息。

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>讀取佇列中的訊息
您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello **PeekMessageAsync**方法。

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>讀取並移除佇列中的訊息
您的程式碼可以使用兩個步驟將訊息從佇列中移除 (清除佇列)。

1. 呼叫**GetMessageAsync** tooget hello 中的下一個訊息佇列。 傳回訊息**GetMessageAsync**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。 依預設，此訊息會維持 30 秒的不可見狀態。
2. 移除 hello 佇列、 呼叫 hello 訊息 toofinish **DeleteMessageAsync**。

這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。 hello 下列程式碼呼叫**DeleteMessageAsync**處理 hello 訊息之後，以滑鼠右鍵。

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>運用清除佇列訊息的其他選項
自訂從佇列中擷取訊息的方法有兩種。
首先，您可以取得一批訊息 （向上 too32)。 第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。 hello 下列程式碼範例使用**GetMessages**方法 tooget 20 訊息在單一呼叫中的。 接著它會使用 **foreach** 迴圈處理每個訊息。 它也會設定 hello 過了隱藏逾時 too5 分鐘數的每個訊息。 請注意，所有的 hello 5 分鐘開始訊息在 hello 相同時間，因此後 5 分鐘已經太過 hello 呼叫之後**GetMessages**，已被刪除的任何訊息會顯示一次。

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>取得 hello 佇列長度
您可以在佇列中取得估計的 hello 訊息數目。 **FetchAttributes**方法會要求 hello 佇列服務，以擷取 hello 佇列屬性，包括 hello 訊息計數。 hello **ApproximateMethodCount**屬性會傳回 hello 所擷取的最後一個值**FetchAttributes**方法，而不需要呼叫 hello 佇列服務。

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>使用非同步等候 hello 模式，其一般佇列應用程式開發介面
這個範例會示範如何 toouse hello 非同步等候模式與一般佇列應用程式開發介面。 hello 範例呼叫 hello 非同步版本的每個指定方法的 hello。 這可以看見 hello 非同步後修正每個方法。 使用非同步方法時，hello 非同步等候模式會暫停本機執行，直到 hello 呼叫完成也一樣。 此行為可讓目前的執行緒 toodo hello 其他工作，這有助於避免效能瓶頸並改善 hello 應用程式的整體回應性。 如需有關使用 hello.NET 中的非同步 Await 模式，請參閱 < [Async 和 Await （C# 和 Visual Basic）](https://msdn.microsoft.com/library/hh191443.aspx)

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a>刪除佇列
toodelete 佇列和所有 hello 訊息包含在它，請呼叫**刪除**hello 佇列物件上的方法。

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>後續步驟
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

