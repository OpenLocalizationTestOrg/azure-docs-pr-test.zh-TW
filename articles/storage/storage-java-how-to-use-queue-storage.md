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
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="9509c-104">如何從 Java 佇列儲存體 toouse</span><span class="sxs-lookup"><span data-stu-id="9509c-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="9509c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="9509c-105">Overview</span></span>
<span data-ttu-id="9509c-106">本指南將說明如何使用 tooperform 常見案例 hello Azure 佇列儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="9509c-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="9509c-107">hello 範例以 Java 撰寫，並使用 hello [for Java 的 Azure 儲存體 SDK][Azure Storage SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="9509c-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="9509c-108">hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立**和**刪除**佇列。</span><span class="sxs-lookup"><span data-stu-id="9509c-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="9509c-109">如需有關佇列的詳細資訊，請參閱 hello[後續步驟](#Next-Steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="9509c-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="9509c-110">注意：已發行一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="9509c-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="9509c-111">如需詳細資訊，請參閱 hello[適用於 Android 的 Azure 儲存體 SDK][Azure Storage SDK for Android]。</span><span class="sxs-lookup"><span data-stu-id="9509c-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="9509c-112">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="9509c-112">Create a Java application</span></span>
<span data-ttu-id="9509c-113">在本指南中，您將使用的儲存功能可在 Java 應用程式中進行本機呼叫，或在 Azure Web 角色或背景工作角色中執行的程式碼中呼叫。</span><span class="sxs-lookup"><span data-stu-id="9509c-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="9509c-114">toodo 因此，您將需要 tooinstall hello Java Development Kit (JDK)，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9509c-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="9509c-115">一旦您這樣做，您必須開發系統符合 hello 最低需求和相依性的 hello 中所列的 tooverify [for Java 的 Azure 儲存體 SDK] [ Azure Storage SDK for Java] GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9509c-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="9509c-116">如果您的系統符合這些需求，您可以遵循下載並安裝在您從該儲存機制的系統上的 hello Azure 儲存體 Libraries for Java 的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="9509c-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="9509c-117">當您完成這些工作時，您就會無法 toocreate hello 範例會使用這份文件中的 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9509c-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="9509c-118">設定您的應用程式 tooaccess 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="9509c-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="9509c-119">新增下列匯入陳述式 toohello 想 toouse Azure 儲存體 Api tooaccess 佇列 hello Java 檔案頂端的 hello:</span><span class="sxs-lookup"><span data-stu-id="9509c-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="9509c-120">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="9509c-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="9509c-121">Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。</span><span class="sxs-lookup"><span data-stu-id="9509c-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="9509c-122">用戶端應用程式中執行時，您必須提供 hello 遵循格式，請使用 hello 您的儲存體帳戶名稱中的 hello 儲存體連接字串和 hello hello hello 中所列的儲存體帳戶的主要存取金鑰[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。</span><span class="sxs-lookup"><span data-stu-id="9509c-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="9509c-123">此範例顯示如何宣告靜態欄位 toohold hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="9509c-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="9509c-124">在應用程式中執行 Microsoft Azure 中的角色，這個字串可以儲存在 hello 服務組態檔， *ServiceConfiguration.cscfg*，而且可以存取與呼叫 toohello **RoleEnvironment.getConfigurationSettings**方法。</span><span class="sxs-lookup"><span data-stu-id="9509c-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="9509c-125">以下是取得 hello 連接字串的範例**設定**名*StorageConnectionString* hello 服務組態檔中：</span><span class="sxs-lookup"><span data-stu-id="9509c-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="9509c-126">hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。</span><span class="sxs-lookup"><span data-stu-id="9509c-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="9509c-127">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="9509c-127">How to: Create a queue</span></span>
<span data-ttu-id="9509c-128">**CloudQueueClient** 物件可讓您取得佇列的參照物件。</span><span class="sxs-lookup"><span data-stu-id="9509c-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="9509c-129">hello 下列程式碼會建立**CloudQueueClient**物件。</span><span class="sxs-lookup"><span data-stu-id="9509c-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="9509c-130">(注意： 有其他方式 toocreate **CloudStorageAccount**物件; 如需詳細資訊，請參閱**CloudStorageAccount**在 hello [Azure 儲存體用戶端 SDK 參考].)</span><span class="sxs-lookup"><span data-stu-id="9509c-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="9509c-131">使用 hello **CloudQueueClient** tooget 想 toouse 參考 toohello 佇列的物件。</span><span class="sxs-lookup"><span data-stu-id="9509c-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="9509c-132">如果不存在，您可以建立 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="9509c-132">You can create hello queue if it doesn't exist.</span></span>

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

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="9509c-133">如何： 新增訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="9509c-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="9509c-134">tooinsert 將訊息插入現有佇列，先建立新**CloudQueueMessage**。</span><span class="sxs-lookup"><span data-stu-id="9509c-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="9509c-135">接下來，呼叫 hello **addMessage**方法。</span><span class="sxs-lookup"><span data-stu-id="9509c-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="9509c-136">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 。</span><span class="sxs-lookup"><span data-stu-id="9509c-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="9509c-137">以下是 程式碼可建立佇列 （如果存在） 並插入 hello 訊息"Hello，World"。</span><span class="sxs-lookup"><span data-stu-id="9509c-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

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

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="9509c-138">如何： 檢視 hello 的下一個訊息</span><span class="sxs-lookup"><span data-stu-id="9509c-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="9509c-139">您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中藉由呼叫**peekMessage**。</span><span class="sxs-lookup"><span data-stu-id="9509c-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="9509c-140">如何： 變更 hello 的佇列訊息的內容</span><span class="sxs-lookup"><span data-stu-id="9509c-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="9509c-141">您可以變更訊息就地 hello 佇列中的 hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="9509c-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="9509c-142">如果 hello 訊息代表的工作，您可以使用此功能 tooupdate hello 的 hello 工作工作狀態。</span><span class="sxs-lookup"><span data-stu-id="9509c-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="9509c-143">下列程式碼的 hello 更新 hello 佇列訊息與新的內容，並設定 hello 的可見性逾時 tooextend 另一個 60 秒。</span><span class="sxs-lookup"><span data-stu-id="9509c-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="9509c-144">這樣會節省 hello 與 hello 訊息相關聯的工作狀態，並提供 hello 用戶端 hello 訊息處理的另一個分鐘 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="9509c-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="9509c-145">您無法使用此技巧 tootrack 多步驟工作流程佇列的訊息，而不需 toostart 透過從 hello 開頭，如果因為 toohardware 或軟體失敗的處理步驟失敗。</span><span class="sxs-lookup"><span data-stu-id="9509c-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="9509c-146">一般而言，您會保留重試計數，而且如果 hello 訊息重試一次以上 *n* 時間，您會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="9509c-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="9509c-147">這麼做可防止每次處理時便觸發應用程式錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="9509c-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="9509c-148">hello 下列程式碼範例搜尋 hello 訊息佇列中，找出符合"Hello，World"hello 內容，然後修改內容的 hello 訊息並結束 hello 第一個訊息。</span><span class="sxs-lookup"><span data-stu-id="9509c-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

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

<span data-ttu-id="9509c-149">或者，hello 下列程式碼範例會更新只 hello 第一個出現的訊息 hello 佇列上。</span><span class="sxs-lookup"><span data-stu-id="9509c-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="9509c-150">如何： 取得 hello 佇列長度</span><span class="sxs-lookup"><span data-stu-id="9509c-150">How to: Get hello queue length</span></span>
<span data-ttu-id="9509c-151">您可以在佇列中取得估計的 hello 訊息數目。</span><span class="sxs-lookup"><span data-stu-id="9509c-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="9509c-152">hello **downloadAttributes**方法會要求 hello 佇列服務的數個目前的值，包括佇列中訊息數目的計數。</span><span class="sxs-lookup"><span data-stu-id="9509c-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="9509c-153">hello 計數只是近似的因為可以新增或移除之後 hello 佇列服務會回應 tooyour 要求訊息。</span><span class="sxs-lookup"><span data-stu-id="9509c-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="9509c-154">hello **getApproximateMessageCount**方法會傳回 hello 太 hello 呼叫所擷取的最後一個值**downloadAttributes**，而不需要呼叫 hello 佇列服務。</span><span class="sxs-lookup"><span data-stu-id="9509c-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

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

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="9509c-155">如何： 清除佇列 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="9509c-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="9509c-156">您的程式碼可以使用兩個步驟來清除佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="9509c-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="9509c-157">當您呼叫**retrieveMessage**，您會收到 hello 下一個訊息，佇列中。</span><span class="sxs-lookup"><span data-stu-id="9509c-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="9509c-158">傳回訊息**retrieveMessage**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="9509c-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="9509c-159">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="9509c-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="9509c-160">toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**deleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="9509c-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="9509c-161">這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="9509c-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="9509c-162">您的程式碼呼叫**deleteMessage**處理 hello 訊息之後，以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="9509c-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="9509c-163">清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="9509c-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="9509c-164">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="9509c-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="9509c-165">首先，您可以取得一批訊息 （向上 too32)。</span><span class="sxs-lookup"><span data-stu-id="9509c-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="9509c-166">第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="9509c-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="9509c-167">hello 下列程式碼範例會使用 hello **retrieveMessages**方法 tooget 20 訊息在單一呼叫中的。</span><span class="sxs-lookup"><span data-stu-id="9509c-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="9509c-168">接著它會使用 **for** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="9509c-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="9509c-169">它也會設定 hello 過了隱藏逾時 toofive 分鐘 （300 秒） 的每個訊息。</span><span class="sxs-lookup"><span data-stu-id="9509c-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="9509c-170">請注意該 hello 五分鐘啟動所有訊息在 hello 相同時間，所以在五分鐘自以來已經過 hello 呼叫太**retrieveMessages**，任何已被刪除的訊息一次將變成可見。</span><span class="sxs-lookup"><span data-stu-id="9509c-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

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

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="9509c-171">如何： 列出 hello 佇列</span><span class="sxs-lookup"><span data-stu-id="9509c-171">How to: List hello queues</span></span>
<span data-ttu-id="9509c-172">一份 hello 目前佇列，呼叫 hello tooobtain **CloudQueueClient.listQueues()**方法，將會傳回的集合**CloudQueue**物件。</span><span class="sxs-lookup"><span data-stu-id="9509c-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

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

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="9509c-173">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="9509c-173">How to: Delete a queue</span></span>
<span data-ttu-id="9509c-174">toodelete 佇列和所有 hello 訊息包含在它呼叫 hello **deleteIfExists**方法上 hello **CloudQueue**物件。</span><span class="sxs-lookup"><span data-stu-id="9509c-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9509c-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9509c-175">Next steps</span></span>
<span data-ttu-id="9509c-176">現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些有關更複雜的儲存體工作的連結 toolearn。</span><span class="sxs-lookup"><span data-stu-id="9509c-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="9509c-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="9509c-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="9509c-178">[Azure 儲存體用戶端 SDK 參考][Azure 儲存體用戶端 SDK 參考]</span><span class="sxs-lookup"><span data-stu-id="9509c-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="9509c-179">[Azure 儲存體服務 REST API][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="9509c-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="9509c-180">[Azure 儲存體團隊部落格][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="9509c-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 儲存體用戶端 SDK 參考]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
