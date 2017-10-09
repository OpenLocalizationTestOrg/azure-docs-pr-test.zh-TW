---
title: "aaaHow toouse 佇列儲存體從 Java |Microsoft 文件"
description: "了解 toouse hello Azure 佇列服務 toocreate 和刪除佇列，以及插入、 取得，並刪除訊息。 範例以 Java 撰寫。"
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 297f89c9d21a38d2b4a5f4346f66f59f9d487010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a>如何從 Java 佇列儲存體 toouse
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>概觀
本指南將說明如何使用 tooperform 常見案例 hello Azure 佇列儲存體服務。 hello 範例以 Java 撰寫，並使用 hello [for Java 的 Azure 儲存體 SDK][Azure Storage SDK for Java]。 hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立**和**刪除**佇列。 如需有關佇列的詳細資訊，請參閱 hello[後續步驟](#Next-Steps)> 一節。

注意：已發行一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。 如需詳細資訊，請參閱 hello[適用於 Android 的 Azure 儲存體 SDK][Azure Storage SDK for Android]。

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>建立 Java 應用程式
在本指南中，您將使用的儲存功能可在 Java 應用程式中進行本機呼叫，或在 Azure Web 角色或背景工作角色中執行的程式碼中呼叫。

toodo 因此，您將需要 tooinstall hello Java Development Kit (JDK)，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。 一旦您這樣做，您必須開發系統符合 hello 最低需求和相依性的 hello 中所列的 tooverify [for Java 的 Azure 儲存體 SDK] [ Azure Storage SDK for Java] GitHub 上的儲存機制。 如果您的系統符合這些需求，您可以遵循下載並安裝在您從該儲存機制的系統上的 hello Azure 儲存體 Libraries for Java 的 hello 指示。 當您完成這些工作時，您就會無法 toocreate hello 範例會使用這份文件中的 Java 應用程式。

## <a name="configure-your-application-tooaccess-queue-storage"></a>設定您的應用程式 tooaccess 佇列儲存體
新增下列匯入陳述式 toohello 想 toouse Azure 儲存體 Api tooaccess 佇列 hello Java 檔案頂端的 hello:

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。 用戶端應用程式中執行時，您必須提供 hello 遵循格式，請使用 hello 您的儲存體帳戶名稱中的 hello 儲存體連接字串和 hello hello hello 中所列的儲存體帳戶的主要存取金鑰[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。 此範例顯示如何宣告靜態欄位 toohold hello 連接字串：

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

在應用程式中執行 Microsoft Azure 中的角色，這個字串可以儲存在 hello 服務組態檔， *ServiceConfiguration.cscfg*，而且可以存取與呼叫 toohello **RoleEnvironment.getConfigurationSettings**方法。 以下是取得 hello 連接字串的範例**設定**名*StorageConnectionString* hello 服務組態檔中：

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。

## <a name="how-to-create-a-queue"></a>作法：建立佇列
**CloudQueueClient** 物件可讓您取得佇列的參照物件。 hello 下列程式碼會建立**CloudQueueClient**物件。 (注意： 有其他方式 toocreate **CloudStorageAccount**物件; 如需詳細資訊，請參閱**CloudStorageAccount**在 hello [Azure 儲存體用戶端 SDK 參考].)

使用 hello **CloudQueueClient** tooget 想 toouse 參考 toohello 佇列的物件。 如果不存在，您可以建立 hello 佇列。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a>如何： 新增訊息 tooa 佇列
tooinsert 將訊息插入現有佇列，先建立新**CloudQueueMessage**。 接下來，呼叫 hello **addMessage**方法。 您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 。 以下是 程式碼可建立佇列 （如果存在） 並插入 hello 訊息"Hello，World"。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a>如何： 檢視 hello 的下一個訊息
您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中藉由呼叫**peekMessage**。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>如何： 變更 hello 的佇列訊息的內容
您可以變更訊息就地 hello 佇列中的 hello 的內容。 如果 hello 訊息代表的工作，您可以使用此功能 tooupdate hello 的 hello 工作工作狀態。 下列程式碼的 hello 更新 hello 佇列訊息與新的內容，並設定 hello 的可見性逾時 tooextend 另一個 60 秒。 這樣會節省 hello 與 hello 訊息相關聯的工作狀態，並提供 hello 用戶端 hello 訊息處理的另一個分鐘 toocontinue。 您無法使用此技巧 tootrack 多步驟工作流程佇列的訊息，而不需 toostart 透過從 hello 開頭，如果因為 toohardware 或軟體失敗的處理步驟失敗。 一般而言，您會保留重試計數，而且如果 hello 訊息重試一次以上 *n* 時間，您會將它刪除。 這麼做可防止每次處理時便觸發應用程式錯誤的訊息。

hello 下列程式碼範例搜尋 hello 訊息佇列中，找出符合"Hello，World"hello 內容，然後修改內容的 hello 訊息並結束 hello 第一個訊息。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

或者，hello 下列程式碼範例會更新只 hello 第一個出現的訊息 hello 佇列上。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a>如何： 取得 hello 佇列長度
您可以在佇列中取得估計的 hello 訊息數目。 hello **downloadAttributes**方法會要求 hello 佇列服務的數個目前的值，包括佇列中訊息數目的計數。 hello 計數只是近似的因為可以新增或移除之後 hello 佇列服務會回應 tooyour 要求訊息。 hello **getApproximateMessageCount**方法會傳回 hello 太 hello 呼叫所擷取的最後一個值**downloadAttributes**，而不需要呼叫 hello 佇列服務。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a>如何： 清除佇列 hello 下一個訊息
您的程式碼可以使用兩個步驟來清除佇列訊息。 當您呼叫**retrieveMessage**，您會收到 hello 下一個訊息，佇列中。 傳回訊息**retrieveMessage**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。 依預設，此訊息會維持 30 秒的不可見狀態。 toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**deleteMessage**。 這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。 您的程式碼呼叫**deleteMessage**處理 hello 訊息之後，以滑鼠右鍵。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a>清除佇列訊息的其他選項
自訂從佇列中擷取訊息的方法有兩種。 首先，您可以取得一批訊息 （向上 too32)。 第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。

hello 下列程式碼範例會使用 hello **retrieveMessages**方法 tooget 20 訊息在單一呼叫中的。 接著它會使用 **for** 迴圈處理每個訊息。 它也會設定 hello 過了隱藏逾時 toofive 分鐘 （300 秒） 的每個訊息。 請注意該 hello 五分鐘啟動所有訊息在 hello 相同時間，所以在五分鐘自以來已經過 hello 呼叫太**retrieveMessages**，任何已被刪除的訊息一次將變成可見。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a>如何： 列出 hello 佇列
一份 hello 目前佇列，呼叫 hello tooobtain **CloudQueueClient.listQueues()**方法，將會傳回的集合**CloudQueue**物件。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a>作法：刪除佇列
toodelete 佇列和所有 hello 訊息包含在它呼叫 hello **deleteIfExists**方法上 hello **CloudQueue**物件。

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>後續步驟
現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn。

* [Azure Storage SDK for Java][Azure Storage SDK for Java]
* [Azure 儲存體用戶端 SDK 參考][Azure 儲存體用戶端 SDK 參考]
* [Azure 儲存體服務 REST API][Azure Storage Services REST API]
* [Azure 儲存體團隊部落格][Azure Storage Team Blog]

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 儲存體用戶端 SDK 參考]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
