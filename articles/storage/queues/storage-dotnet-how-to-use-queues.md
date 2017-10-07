---
title: "開始使用適用於.NET 的 Azure 佇列儲存體 aaaGet |Microsoft 文件"
description: "Azure 佇列可在應用程式元件之間提供可靠的非同步傳訊。 獨立雲端訊息可讓您的應用程式元件 tooscale。"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>以 .NET 開始使用 Azure 佇列儲存體
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Overview
Azure 佇列儲存體可提供應用程式元件之間的雲端傳訊。 設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。 佇列儲存體提供非同步傳訊應用程式元件之間的通訊是否在 hello 雲端中，在 hello 桌面上、 在內部部署伺服器上，或行動裝置上執行。 佇列儲存體也支援管理非同步工作並建置處理工作流程。

### <a name="about-this-tutorial"></a>關於本教學課程
本教學課程會示範如何 toowrite.NET 程式碼為使用 Azure 佇列儲存體的一些常見案例。 本文說明的案例包括建立和刪除佇列，以及新增、讀取和刪除佇列訊息。

**估計時間 toocomplete:** 45 分鐘的時間

**先決條件：**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [適用於 .NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [適用於.NET 的 Azure 設定管理員](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Azure 儲存體帳戶](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>新增 using 指示詞
新增下列 hello`using`指示詞 toohello 頂端 hello`Program.cs`檔案：

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>剖析 hello 連接字串
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>建立 hello 佇列服務用戶端
hello **CloudQueueClient**類別可讓您 tooretrieve 佇列佇列儲存體中。 以下是其中一種方式 toocreate hello 服務用戶端：

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
現在您已準備好 toowrite 讀取和寫入資料 tooQueue 儲存的程式碼。

## <a name="create-a-queue"></a>建立佇列
這個範例會示範如何 toocreate 佇列，如果不存在：

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a>將訊息插入佇列
tooinsert 將訊息插入現有佇列，先建立新**CloudQueueMessage**。 接下來，呼叫 hello **AddMessage**方法。 您可以從字串 (採用 UTF-8 格式) 或**位元組**陣列建立 **CloudQueueMessage**。 以下是它會建立佇列 （如果存在） 並插入 hello 訊息 'Hello World' 的程式碼：

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a>查看 hello 下一個訊息
您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello **PeekMessage**方法。

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a>變更佇列的訊息 hello 內容
您可以變更訊息就地 hello 佇列中的 hello 的內容。 如果訊息代表的工作，您可以使用此功能 tooupdate hello 工作工作的狀態。 下列程式碼的 hello 更新 hello 佇列訊息與新的內容，並設定 hello 的可見性逾時 tooextend 另一個 60 秒。 這樣會節省 hello 與 hello 訊息相關聯的工作狀態，並提供 hello 用戶端 hello 訊息處理的另一個分鐘 toocontinue。 您無法使用此技巧 tootrack 多步驟工作流程佇列的訊息，而不需 toostart 透過從 hello 開頭，如果因為 toohardware 或軟體失敗的處理步驟失敗。 一般而言，您會保留重試計數，而且如果 hello 訊息重試一次以上 *n* 時間，您會將它刪除。 這麼做可防止每次處理時便觸發應用程式錯誤的訊息。

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a>清除佇列 hello 下一個訊息
您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。 當您呼叫**GetMessage**，您會收到 hello 下一個訊息，佇列中。 傳回訊息**GetMessage**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。 依預設，此訊息會維持 30 秒的不可見狀態。 toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**DeleteMessage**。 這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。 您的程式碼呼叫**DeleteMessage**處理 hello 訊息之後，以滑鼠右鍵。

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>搭配通用佇列儲存體 API 使用 Async-Await 模式
這個範例會示範如何 toouse hello 非同步等候模式與一般佇列儲存體 Api。 hello 範例 hello 所示，呼叫 hello 非同步版本的每個指定方法的 hello*非同步*每一種方法的後置詞。 使用非同步方法時，hello 非同步-await 模式會暫停本機執行，直到 hello 呼叫完成。 此行為可讓目前的執行緒 toodo hello 其他工作，可以協助避免效能瓶頸並提高 hello 應用程式的整體回應性。 如需有關使用 hello.NET 中的非同步 Await 模式請參閱 < [Async 和 Await （C# 和 Visual Basic）](https://msdn.microsoft.com/library/hh191443.aspx)

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>運用清除佇列訊息的其他選項
自訂從佇列中擷取訊息的方法有兩種。
首先，您可以取得一批訊息 （向上 too32)。 第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。 hello 下列程式碼範例使用**GetMessages**方法 tooget 20 訊息在單一呼叫中的。 接著它會使用 **foreach** 迴圈處理每個訊息。 它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。 請注意該 hello 5 分鐘所有 hello 訊息啟動相同的時間，因此後 5 分鐘自以來已經過 hello 呼叫太**GetMessages**，任何已被刪除的訊息一次將變成可見。

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a>取得 hello 佇列長度
您可以在佇列中取得估計的 hello 訊息數目。 **FetchAttributes**方法會要求 hello 佇列服務，以擷取 hello 佇列屬性，包括 hello 訊息計數。 hello **ApproximateMessageCount**屬性會傳回 hello 所擷取的最後一個值**FetchAttributes**方法，而不需要呼叫 hello 佇列服務。

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a>刪除佇列
toodelete 佇列和所有 hello 訊息包含在它，請呼叫**刪除**hello 佇列物件上的方法。

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a>後續步驟
現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn。

* 檢視 hello 佇列服務參考文件，如需可用的應用程式開發介面的完整詳細資料：
  * [Storage Client Library for .NET 參考資料](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [REST API 參考資料](http://msdn.microsoft.com/library/azure/dd179355)
* 了解您所撰寫 toosimplify hello 程式碼如何使用 hello 與 Azure 儲存體 toowork [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md)。
* 檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。
  * [開始使用適用於.NET 的 Azure 資料表儲存體使用](../../cosmos-db/table-storage-how-to-use-dotnet.md)toostore 結構化資料。
  * [開始使用適用於.NET 的 Azure Blob 儲存體使用](../blobs/storage-dotnet-how-to-use-blobs.md)toostore 非結構化的資料。
  * [使用.NET (C#) 連線 tooSQL 資料庫](../../sql-database/sql-database-connect-query-dotnet-core.md)toostore 關聯式資料。

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
