---
title: "如何使用 Python 的佇列儲存體 | Microsoft Docs"
description: "了解如何使用 Python 的 Azure 佇列服務來建立和刪除佇列，以及插入、取得和刪除訊息。"
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 963c11acb7939993568a774cd281145a8059b5a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="5808d-103">如何使用 Python 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="5808d-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="5808d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="5808d-104">Overview</span></span>
<span data-ttu-id="5808d-105">本指南說明如何使用 Azure 佇列儲存體服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="5808d-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="5808d-106">這些範例是以 Python 所撰寫，並使用 [Microsoft Azure Storage SDK for Python (適用於 Python 的 Microsoft Azure 儲存體 SDK)]。</span><span class="sxs-lookup"><span data-stu-id="5808d-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="5808d-107">所涵蓋的案例包括「插入」、「查看」、「取得」和「刪除」佇列訊息，以及「建立和刪除佇列」。</span><span class="sxs-lookup"><span data-stu-id="5808d-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="5808d-108">如需佇列的詳細資訊，請參閱 [後續步驟] 一節。</span><span class="sxs-lookup"><span data-stu-id="5808d-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="5808d-109">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="5808d-109">How To: Create a Queue</span></span>
<span data-ttu-id="5808d-110">**QueueService** 物件可讓您操作佇列。</span><span class="sxs-lookup"><span data-stu-id="5808d-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="5808d-111">下列程式碼將建立 **QueueService** 物件。</span><span class="sxs-lookup"><span data-stu-id="5808d-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="5808d-112">將下列內容新增至您想要在其中以程式設計方式存取 Azure 儲存體之任何 Python 檔案內的頂端附近：</span><span class="sxs-lookup"><span data-stu-id="5808d-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="5808d-113">下列程式碼會使用儲存體帳戶名稱和帳戶金鑰來建立 **QueueService** 物件。</span><span class="sxs-lookup"><span data-stu-id="5808d-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="5808d-114">將 'myaccount' 和 'mykey' 取代為您的帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="5808d-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="5808d-115">作法：將訊息插入佇列中</span><span class="sxs-lookup"><span data-stu-id="5808d-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="5808d-116">若要將訊息插入佇列，請使用 **put\_message** 方法建立新訊息，並將它新增至佇列。</span><span class="sxs-lookup"><span data-stu-id="5808d-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="5808d-117">作法：預覽下一個訊息</span><span class="sxs-lookup"><span data-stu-id="5808d-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="5808d-118">透過呼叫 **peek\_messages** 方法，您可以在佇列前面查看訊息，而無需將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="5808d-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="5808d-119">**peek\_messages** 預設會查看單一訊息。</span><span class="sxs-lookup"><span data-stu-id="5808d-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="5808d-120">做法：清除佇列訊息</span><span class="sxs-lookup"><span data-stu-id="5808d-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="5808d-121">您的程式碼可以使用兩個步驟來將訊息從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="5808d-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="5808d-122">呼叫 **get\_messages** 時，您預設會取得佇列中的下一個訊息。</span><span class="sxs-lookup"><span data-stu-id="5808d-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="5808d-123">從 **get\_messages** 傳回的訊息，對於從此佇列讀取訊息的任何其他程式碼而言將會是不可見的。</span><span class="sxs-lookup"><span data-stu-id="5808d-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="5808d-124">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="5808d-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="5808d-125">若要完成從佇列中移除訊息，您還必須呼叫 **delete\_message**。</span><span class="sxs-lookup"><span data-stu-id="5808d-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="5808d-126">這個移除訊息的兩步驟程序可確保您的程式碼因為硬體或軟體故障而無法處理訊息時，另一個程式碼的執行個體可以取得相同訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="5808d-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="5808d-127">您的程式碼會在處理完訊息之後立即呼叫 **delete\_message**。</span><span class="sxs-lookup"><span data-stu-id="5808d-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="5808d-128">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="5808d-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="5808d-129">首先，您可以取得一批訊息 (最多 32 個)。</span><span class="sxs-lookup"><span data-stu-id="5808d-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="5808d-130">其次，您可以設定較長或較短的可見度逾時，讓您的程式碼有較長或較短的時間可以完全處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="5808d-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="5808d-131">下列程式碼範例將使用 **get\_messages** 方法，在一次呼叫中取得 16 個訊息。</span><span class="sxs-lookup"><span data-stu-id="5808d-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="5808d-132">接著它會使用 for 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="5808d-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="5808d-133">它也會將可見度逾時設定為每個訊息五分鐘。</span><span class="sxs-lookup"><span data-stu-id="5808d-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="5808d-134">作法：變更佇列訊息的內容</span><span class="sxs-lookup"><span data-stu-id="5808d-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="5808d-135">您可以在佇列中就地變更訊息內容。</span><span class="sxs-lookup"><span data-stu-id="5808d-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="5808d-136">如果訊息代表工作作業，則您可以使用此功能來更新工作作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="5808d-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="5808d-137">下方的程式碼使用 **update\_message** 方法來更新訊息。</span><span class="sxs-lookup"><span data-stu-id="5808d-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="5808d-138">可見度逾時設定為 0，表示會立即顯示訊息，並且會更新內容。</span><span class="sxs-lookup"><span data-stu-id="5808d-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="5808d-139">作法：取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="5808d-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="5808d-140">您可以取得佇列中的估計訊息數目。</span><span class="sxs-lookup"><span data-stu-id="5808d-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="5808d-141">**get\_queue\_metadata** 方法會要求佇列服務傳回佇列的中繼資料和 **approximate_message_count**。</span><span class="sxs-lookup"><span data-stu-id="5808d-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="5808d-142">由於佇列服務在回應您的要求之後可以新增或移除訊息，此結果僅為近似值。</span><span class="sxs-lookup"><span data-stu-id="5808d-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="5808d-143">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="5808d-143">How To: Delete a Queue</span></span>
<span data-ttu-id="5808d-144">若要刪除佇列及其內含的所有訊息，請呼叫 **delete\_queue** 方法。</span><span class="sxs-lookup"><span data-stu-id="5808d-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="5808d-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5808d-145">Next Steps</span></span>
<span data-ttu-id="5808d-146">了解佇列儲存體的基本概念之後，請使用下列連結深入了解。</span><span class="sxs-lookup"><span data-stu-id="5808d-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="5808d-147">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="5808d-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="5808d-148">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="5808d-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="5808d-149">[Azure 儲存體團隊部落格]</span><span class="sxs-lookup"><span data-stu-id="5808d-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="5808d-150">[Microsoft Azure Storage SDK for Python (適用於 Python 的 Microsoft Azure 儲存體 SDK)]</span><span class="sxs-lookup"><span data-stu-id="5808d-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure 儲存體團隊部落格]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK for Python (適用於 Python 的 Microsoft Azure 儲存體 SDK)]: https://github.com/Azure/azure-storage-python