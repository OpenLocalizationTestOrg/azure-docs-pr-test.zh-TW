---
title: "aaaHow toouse 來自 Python 的佇列儲存體 |Microsoft 文件"
description: "了解如何 toouse hello Python toocreate 從 Azure 佇列服務及刪除佇列，並插入、 取得，和刪除訊息。"
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
ms.openlocfilehash: f4f902a2c314401e5c1768fbc80566c8ba25c058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="3c925-103">如何 toouse 來自 Python 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="3c925-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="3c925-104">概觀</span><span class="sxs-lookup"><span data-stu-id="3c925-104">Overview</span></span>
<span data-ttu-id="3c925-105">本指南也說明如何使用 tooperform 常見案例 hello Azure 佇列儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="3c925-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="3c925-106">hello 範例撰寫的 Python 和使用 hello [Microsoft Azure 儲存體 SDK for Python]。</span><span class="sxs-lookup"><span data-stu-id="3c925-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="3c925-107">hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立及刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="3c925-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="3c925-108">如需有關佇列的詳細資訊，請參閱 toohello [下一步] 區段。</span><span class="sxs-lookup"><span data-stu-id="3c925-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="3c925-109">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="3c925-109">How To: Create a Queue</span></span>
<span data-ttu-id="3c925-110">hello **QueueService**物件可讓您使用佇列。</span><span class="sxs-lookup"><span data-stu-id="3c925-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="3c925-111">hello 下列程式碼會建立**QueueService**物件。</span><span class="sxs-lookup"><span data-stu-id="3c925-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="3c925-112">加入要在其中任何 Python 檔案 tooprogrammatically 存取 Azure 儲存體的 hello 頂端附近的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="3c925-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="3c925-113">hello 下列程式碼會建立**QueueService**使用 hello 儲存體帳戶名稱和帳戶金鑰的物件。</span><span class="sxs-lookup"><span data-stu-id="3c925-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="3c925-114">將 'myaccount' 和 'mykey' 取代為您的帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="3c925-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="3c925-115">作法：將訊息插入佇列中</span><span class="sxs-lookup"><span data-stu-id="3c925-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="3c925-116">將訊息插入佇列中，使用 hello tooinsert**放\_訊息**方法來建立新的訊息，並將它加入 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="3c925-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="3c925-117">如何： 檢視 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="3c925-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="3c925-118">您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello**查看\_訊息**方法。</span><span class="sxs-lookup"><span data-stu-id="3c925-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="3c925-119">**peek\_messages** 預設會查看單一訊息。</span><span class="sxs-lookup"><span data-stu-id="3c925-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="3c925-120">做法：清除佇列訊息</span><span class="sxs-lookup"><span data-stu-id="3c925-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="3c925-121">您的程式碼可以使用兩個步驟來將訊息從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="3c925-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="3c925-122">當您呼叫**取得\_訊息**，預設會取得 hello 下一個訊息佇列中。</span><span class="sxs-lookup"><span data-stu-id="3c925-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="3c925-123">傳回訊息**取得\_訊息**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="3c925-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="3c925-124">依預設，此訊息會維持 30 秒的不可見狀態。</span><span class="sxs-lookup"><span data-stu-id="3c925-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="3c925-125">toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**刪除\_訊息**。</span><span class="sxs-lookup"><span data-stu-id="3c925-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="3c925-126">這兩個步驟的程序中移除訊息可確保當您的程式碼無法 tooprocess 訊息，因為硬體或軟體失敗時，程式碼的另一個執行個體可以取得相同的訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="3c925-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="3c925-127">您的程式碼呼叫**刪除\_訊息**處理 hello 訊息之後，以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="3c925-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="3c925-128">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="3c925-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="3c925-129">首先，您可以取得一批訊息 （向上 too32)。</span><span class="sxs-lookup"><span data-stu-id="3c925-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="3c925-130">第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="3c925-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="3c925-131">hello 下列程式碼範例使用**取得\_訊息**方法 tooget 16 訊息在單一呼叫中的。</span><span class="sxs-lookup"><span data-stu-id="3c925-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="3c925-132">接著它會使用 for 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="3c925-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="3c925-133">它也會設定每個訊息的五分鐘的 hello 過了隱藏逾時。</span><span class="sxs-lookup"><span data-stu-id="3c925-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="3c925-134">如何： 變更 hello 排入佇列的訊息內容</span><span class="sxs-lookup"><span data-stu-id="3c925-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="3c925-135">您可以變更訊息就地 hello 佇列中的 hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="3c925-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="3c925-136">如果訊息代表的工作，您可以使用此功能 tooupdate hello 工作工作的狀態。</span><span class="sxs-lookup"><span data-stu-id="3c925-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="3c925-137">下列程式碼 hello 使用 hello**更新\_訊息**方法 tooupdate 訊息。</span><span class="sxs-lookup"><span data-stu-id="3c925-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="3c925-138">hello 可見度逾時設定 too0，這表示會立即出現此訊息，而且會更新 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="3c925-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="3c925-139">如何： 取得 hello 佇列長度</span><span class="sxs-lookup"><span data-stu-id="3c925-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="3c925-140">您可以在佇列中取得估計的 hello 訊息數目。</span><span class="sxs-lookup"><span data-stu-id="3c925-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="3c925-141">**取得\_佇列\_中繼資料**方法將會詢問 hello hello 佇列的相關佇列服務 tooreturn 中繼資料、 hello **approximate_message_count**。</span><span class="sxs-lookup"><span data-stu-id="3c925-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="3c925-142">hello 結果只是近似的因為可以新增或移除之後佇列服務會回應 tooyour 要求訊息。</span><span class="sxs-lookup"><span data-stu-id="3c925-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="3c925-143">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="3c925-143">How To: Delete a Queue</span></span>
<span data-ttu-id="3c925-144">toodelete 佇列和所有 hello 訊息包含在它，請呼叫**刪除\_佇列**方法。</span><span class="sxs-lookup"><span data-stu-id="3c925-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="3c925-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c925-145">Next Steps</span></span>
<span data-ttu-id="3c925-146">現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些連結 toolearn 更多。</span><span class="sxs-lookup"><span data-stu-id="3c925-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="3c925-147">Python 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="3c925-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="3c925-148">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="3c925-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="3c925-149">[Azure 儲存體團隊部落格]</span><span class="sxs-lookup"><span data-stu-id="3c925-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="3c925-150">[Microsoft Azure 儲存體 SDK for Python]</span><span class="sxs-lookup"><span data-stu-id="3c925-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure 儲存體團隊部落格]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure 儲存體 SDK for Python]: https://github.com/Azure/azure-storage-python