---
title: "如何使用 Java 的佇列儲存體 | Microsoft Docs"
description: "了解如何使用 Azure 佇列服務來建立和刪除佇列，以及插入、取得和刪除訊息。 範例以 Java 撰寫。"
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
ms.openlocfilehash: a56b345c5efb4ce9c8ee2da91b798d09d44e42be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="7a1ea-104">如何使用 Java 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="7a1ea-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="7a1ea-105">概觀</span><span class="sxs-lookup"><span data-stu-id="7a1ea-105">Overview</span></span>
<span data-ttu-id="7a1ea-106">本指南將示範如何使用 Azure 佇列儲存體服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="7a1ea-107">相關範例是以 Java 撰寫並使用 [Azure Storage SDK for Java][Azure Storage SDK for Java]。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="7a1ea-108">所涵蓋的案例包括**插入**、**查看**、**取得**和**刪除**佇列訊息，以及**建立**和**刪除**佇列。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="7a1ea-109">如需佇列的詳細資訊，請參閱[後續步驟](#Next-Steps)一節。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="7a1ea-110">注意：已發行一套 SDK 可供在 Android 裝置上使用 Azure 儲存體的開發人員使用。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="7a1ea-111">如需詳細資訊，請參閱 [Azure Storage SDK for Android][Azure Storage SDK for Android]。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="7a1ea-112">建立 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="7a1ea-112">Create a Java application</span></span>
<span data-ttu-id="7a1ea-113">在本指南中，您將使用的儲存功能可在 Java 應用程式中進行本機呼叫，或在 Azure Web 角色或背景工作角色中執行的程式碼中呼叫。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="7a1ea-114">若要這樣做，您需要安裝 Java Development Kit (JDK)，並在 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="7a1ea-115">完成此動作之後，您需要驗證開發系統符合 GitHub 上的 [Azure Storage SDK for Java][Azure Storage SDK for Java] 儲存機制中所列出的最低需求和相依性。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="7a1ea-116">如果系統符合這些需求，則您可以依照指示，從該儲存機制中下載 Azure Storage Libraries for Java 並安裝在系統上。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="7a1ea-117">完成這些工作之後，您就能夠利用本文中的範例來建立 Java 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="7a1ea-118">設定您的應用程式以存取佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="7a1ea-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="7a1ea-119">將下列 import 陳述式新增到您要在其中使用 Azure 儲存體 API 存取佇列的 Java 檔案頂端：</span><span class="sxs-lookup"><span data-stu-id="7a1ea-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="7a1ea-120">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="7a1ea-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="7a1ea-121">Azure 儲存體用戶端會使用儲存體連接字串來儲存存取資料管理服務時所用的端點與認證。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="7a1ea-122">在用戶端應用程式中執行時，您必須以下列格式提供儲存體連接字串 (其中的 AccountName 和 AccountKey 值要使用您儲存體帳戶的名稱，以及在 [Azure 入口網站](https://portal.azure.com)中針對該儲存體帳戶而列出的主要存取金鑰)。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="7a1ea-123">本範例將示範如何宣告靜態欄位來存放連接字串：</span><span class="sxs-lookup"><span data-stu-id="7a1ea-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="7a1ea-124">在 Microsoft Azure 的角色內執行的應用程式中，此字串可以儲存在服務組態檔 *ServiceConfiguration.cscfg* 裡，且可以藉由呼叫 **RoleEnvironment.getConfigurationSettings** 方法來存取。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="7a1ea-125">以下是從服務組態檔中名為 **StorageConnectionString** 的 *Setting* 元素取得連接字串的範例：</span><span class="sxs-lookup"><span data-stu-id="7a1ea-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="7a1ea-126">下列範例假設您已經使用這兩個方法之一來取得儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="7a1ea-127">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="7a1ea-127">How to: Create a queue</span></span>
<span data-ttu-id="7a1ea-128">**CloudQueueClient** 物件可讓您取得佇列的參照物件。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="7a1ea-129">下列程式碼將建立 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="7a1ea-130">(注意：還有其他方式可建立 **CloudStorageAccount** 物件。如需詳細資訊，請參閱 [Azure 儲存體用戶端 SDK 參考]中的 **CloudStorageAccount**。)</span><span class="sxs-lookup"><span data-stu-id="7a1ea-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="7a1ea-131">使用 **CloudQueueClient** 物件來取得想要使用佇列的參照。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="7a1ea-132">如果佇列不存在，您可以建立佇列。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="7a1ea-133">作法：將訊息新增至佇列</span><span class="sxs-lookup"><span data-stu-id="7a1ea-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="7a1ea-134">若要將訊息插入現有佇列，請先建立新的 **CloudQueueMessage**。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="7a1ea-135">接著，呼叫 **addMessage** 方法。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="7a1ea-136">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="7a1ea-137">以下是建立佇列 (如果佇列不存在) 並插入訊息 "Hello, World" 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="7a1ea-138">作法：查看下一個訊息</span><span class="sxs-lookup"><span data-stu-id="7a1ea-138">How to: Peek at the next message</span></span>
<span data-ttu-id="7a1ea-139">透過呼叫 **peekMessage**，您可以在佇列前面查看訊息，而無需將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="7a1ea-140">作法：變更佇列訊息的內容</span><span class="sxs-lookup"><span data-stu-id="7a1ea-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="7a1ea-141">您可以在佇列中就地變更訊息內容。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="7a1ea-142">如果訊息代表工作作業，則您可以使用此功能來更新工作作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="7a1ea-143">下列程式碼將使用新的內容更新佇列訊息，並將可見度逾時設定延長 60 秒。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="7a1ea-144">這可儲存與訊息相關的工作狀態，並提供用戶端多一分鐘的時間繼續處理訊息。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="7a1ea-145">您可以使用此技巧來追蹤佇列訊息上的多步驟工作流程，如果因為硬體或軟體故障而導致某個處理步驟失敗，將無需從頭開始。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="7a1ea-146">通常，您也會保留重試計數，如果訊息重試超過 *n* 次，您會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="7a1ea-147">這麼做可防止每次處理時便觸發應用程式錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="7a1ea-148">下列程式碼範例會在訊息佇列中搜尋，找出內容符合 "Hello, World" 的第一個訊息，然後修改訊息內容並結束。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="7a1ea-149">另外，下列程式碼範例只更新佇列上第一個可見的訊息。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="7a1ea-150">作法：取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="7a1ea-150">How to: Get the queue length</span></span>
<span data-ttu-id="7a1ea-151">您可以取得佇列中的估計訊息數目。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="7a1ea-152">**downloadAttributes** 方法會向佇列服務要求數個目前值，包括計算佇列中的訊息數。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="7a1ea-153">此計數只是一個約略值，因為在佇列服務回應您的要求之後，仍有新增或移除訊息的可能。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="7a1ea-154">**getApproximateMessageCount** 方法會傳回呼叫 **downloadAttributes** 所擷取的最後一個值，而無需呼叫佇列服務。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="7a1ea-155">作法：清除下一個佇列訊息</span><span class="sxs-lookup"><span data-stu-id="7a1ea-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="7a1ea-156">您的程式碼可以使用兩個步驟來清除佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="7a1ea-157">呼叫 **retrieveMessage**時，您會取得佇列中的下一個訊息。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="7a1ea-158">從 **retrieveMessage** 傳回的訊息，對於從此佇列讀取訊息的任何其他程式碼而言將會是不可見的。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="7a1ea-159">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="7a1ea-160">若要完成將訊息從佇列中移除，您還必須呼叫 **deleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="7a1ea-161">這個移除訊息的兩步驟程序可確保您的程式碼因為硬體或軟體故障而無法處理訊息時，另一個程式碼的執行個體可以取得相同訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="7a1ea-162">您的程式碼會在處理完訊息之後立即呼叫 **deleteMessage**。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="7a1ea-163">清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="7a1ea-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="7a1ea-164">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="7a1ea-165">首先，您可以取得一批訊息 (最多 32 個)。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="7a1ea-166">其次，您可以設定較長或較短的可見度逾時，讓您的程式碼有較長或較短的時間可以完全處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="7a1ea-167">下列程式碼範例使用 **retrieveMessages** 方法，在一次呼叫中取得 20 個訊息。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="7a1ea-168">接著它會使用 **for** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="7a1ea-169">它也會將可見度逾時設定為每個訊息五分鐘 (300 秒)。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="7a1ea-170">請注意，系統會針對所有訊息同時開始計時五分鐘，所以從呼叫 **retrieveMessages**開始的五分鐘後，任何尚未刪除的訊息都會重新出現。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="7a1ea-171">作法：列出佇列</span><span class="sxs-lookup"><span data-stu-id="7a1ea-171">How to: List the queues</span></span>
<span data-ttu-id="7a1ea-172">若要取得目前佇列的清單，請呼叫 **CloudQueueClient.listQueues()** 方法，此方法會傳回 **CloudQueue** 物件的集合。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="7a1ea-173">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="7a1ea-173">How to: Delete a queue</span></span>
<span data-ttu-id="7a1ea-174">若要刪除佇列及其內含的所有訊息，請在 **CloudQueue** 物件上呼叫 **deleteIfExists** 方法。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="7a1ea-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a1ea-175">Next steps</span></span>
<span data-ttu-id="7a1ea-176">了解佇列儲存體的基礎概念之後，請參考下列連結以了解有關更複雜的儲存工作。</span><span class="sxs-lookup"><span data-stu-id="7a1ea-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="7a1ea-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="7a1ea-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="7a1ea-178">[Azure 儲存體用戶端 SDK 參考][Azure 儲存體用戶端 SDK 參考]</span><span class="sxs-lookup"><span data-stu-id="7a1ea-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="7a1ea-179">[Azure 儲存體服務 REST API][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="7a1ea-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="7a1ea-180">[Azure 儲存體團隊部落格][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="7a1ea-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure 儲存體用戶端 SDK 參考]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
