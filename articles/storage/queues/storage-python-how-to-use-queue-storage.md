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
# <a name="how-toouse-queue-storage-from-python"></a>如何 toouse 來自 Python 的佇列儲存體
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>概觀
本指南也說明如何使用 tooperform 常見案例 hello Azure 佇列儲存體服務。 hello 範例撰寫的 Python 和使用 hello [Microsoft Azure 儲存體 SDK for Python]。 hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立及刪除佇列**。 如需有關佇列的詳細資訊，請參閱 toohello [下一步] 區段。

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>作法：建立佇列
hello **QueueService**物件可讓您使用佇列。 hello 下列程式碼會建立**QueueService**物件。 加入要在其中任何 Python 檔案 tooprogrammatically 存取 Azure 儲存體的 hello 頂端附近的 hello 下列：

```python
from azure.storage.queue import QueueService
```

hello 下列程式碼會建立**QueueService**使用 hello 儲存體帳戶名稱和帳戶金鑰的物件。 將 'myaccount' 和 'mykey' 取代為您的帳戶名稱和金鑰。

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>作法：將訊息插入佇列中
將訊息插入佇列中，使用 hello tooinsert**放\_訊息**方法來建立新的訊息，並將它加入 toohello 佇列。

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>如何： 檢視 hello 下一個訊息
您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello**查看\_訊息**方法。 **peek\_messages** 預設會查看單一訊息。

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>做法：清除佇列訊息
您的程式碼可以使用兩個步驟來將訊息從佇列中移除。 當您呼叫**取得\_訊息**，預設會取得 hello 下一個訊息佇列中。 傳回訊息**取得\_訊息**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。 依預設，此訊息會維持 30 秒的不可見狀態。 toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**刪除\_訊息**。 這兩個步驟的程序中移除訊息可確保當您的程式碼無法 tooprocess 訊息，因為硬體或軟體失敗時，程式碼的另一個執行個體可以取得相同的訊息並再試一次。 您的程式碼呼叫**刪除\_訊息**處理 hello 訊息之後，以滑鼠右鍵。

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

自訂從佇列中擷取訊息的方法有兩種。
首先，您可以取得一批訊息 （向上 too32)。 第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。 hello 下列程式碼範例使用**取得\_訊息**方法 tooget 16 訊息在單一呼叫中的。 接著它會使用 for 迴圈處理每個訊息。 它也會設定每個訊息的五分鐘的 hello 過了隱藏逾時。

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>如何： 變更 hello 排入佇列的訊息內容
您可以變更訊息就地 hello 佇列中的 hello 的內容。 如果訊息代表的工作，您可以使用此功能 tooupdate hello 工作工作的狀態。 下列程式碼 hello 使用 hello**更新\_訊息**方法 tooupdate 訊息。 hello 可見度逾時設定 too0，這表示會立即出現此訊息，而且會更新 hello 內容。

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>如何： 取得 hello 佇列長度
您可以在佇列中取得估計的 hello 訊息數目。 **取得\_佇列\_中繼資料**方法將會詢問 hello hello 佇列的相關佇列服務 tooreturn 中繼資料、 hello **approximate_message_count**。 hello 結果只是近似的因為可以新增或移除之後佇列服務會回應 tooyour 要求訊息。

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>作法：刪除佇列
toodelete 佇列和所有 hello 訊息包含在它，請呼叫**刪除\_佇列**方法。

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>後續步驟
現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些連結 toolearn 更多。

* [Python 開發人員中心](/develop/python/)
* [Azure 儲存體服務 REST API](http://msdn.microsoft.com/library/azure/dd179355)
* [Azure 儲存體團隊部落格]
* [Microsoft Azure 儲存體 SDK for Python]

[Azure 儲存體團隊部落格]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure 儲存體 SDK for Python]: https://github.com/Azure/azure-storage-python