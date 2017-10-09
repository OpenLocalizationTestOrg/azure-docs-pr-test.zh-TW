---
title: "aaaHow toouse 佇列儲存體 （c + +） |Microsoft 文件"
description: "了解如何 toouse hello azure 佇列儲存體服務。 範例是以 C++ 撰寫的。"
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 755380824890ad83774e14d258975915e10cfede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a>如何 toouse 佇列儲存體從 c + +
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>概觀
本指南將說明如何使用 tooperform 常見案例 hello Azure 佇列儲存體服務。 hello 範例以 c + + 撰寫，並使用 hello [c + + 的 Azure 儲存體用戶端程式庫](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)。 hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立及刪除佇列**。

> [!NOTE]
> 此指南的目標 hello Azure 儲存體用戶端程式庫，c + + 1.0.0 版和更新版本。 hello 建議版本是儲存體用戶端程式庫 2.2.0，也就是可透過使用[NuGet](http://www.nuget.org/packages/wastorage)或[GitHub](http://github.com/Azure/azure-storage-cpp/)。
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>建立 C++ 應用程式
在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。

toodo 因此，您將需要 tooinstall hello for c + + 的 Azure 儲存體用戶端程式庫，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。

tooinstall hello Azure 儲存體用戶端程式庫的 c + +，，您可以使用下列方法的 hello:

* **Linux:**遵循 hello 所提供的 hello 指示[for c + + 讀我檔案的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)頁面。
* **Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。 型別 hello 下列命令到 hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)按**ENTER**。

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>設定您的應用程式 tooaccess 佇列儲存體
加入 hello 下列包含您想要 toouse hello Azure 儲存體 Api tooaccess 佇列 hello c + + 檔案的陳述式 toohello 頂端：  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>設定 Azure 儲存體連接字串
Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。 用戶端應用程式中執行時，您必須提供 hello 遵循格式，並透過儲存體帳戶和 hello 儲存體存取金鑰的 hello 名稱 hello hello 中所列的儲存體帳戶中的 hello 儲存體連接字串[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。 如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md)。 此範例顯示如何宣告靜態欄位 toohold hello 連接字串：  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest 您的應用程式在本機的 Windows 電腦，您可以使用 Microsoft Azure 的 hello[儲存體模擬器](storage-use-emulator.md)會隨 hello [Azure SDK](https://azure.microsoft.com/downloads/)。 hello 儲存體模擬器是模擬 hello Blob、 佇列和表格服務在本機開發電腦上可用在 Azure 中的公用程式。 hello 下列範例顯示如何宣告靜態欄位 toohold hello 連接字串 tooyour 本機儲存體模擬器：  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure 儲存體模擬器中，選取 hello**啟動**按鈕或按 hello **Windows**索引鍵。 開始輸入**Azure 儲存體模擬器**，然後選取**Microsoft Azure 儲存體模擬器**hello 清單中的應用程式。

hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。

## <a name="retrieve-your-connection-string"></a>擷取連接字串
您可以使用 hello**驗證 cloud_storage_account**類別 toorepresent 儲存體帳戶資訊。 tooretrieve 您的儲存體帳戶資訊 hello 儲存體連接字串，您可以使用 hello**剖析**方法。

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>作法：建立佇列
**cloud_queue_client** 物件可讓您取得佇列的參考物件。 hello 下列程式碼會建立**cloud_queue_client**物件。

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

使用 hello **cloud_queue_client** tooget 想 toouse 參考 toohello 佇列的物件。 如果不存在，您可以建立 hello 佇列。

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>作法：將訊息插入佇列中
tooinsert 將訊息插入現有佇列，先建立新**cloud_queue_message**。 接下來，呼叫 hello **add_message**方法。 **cloud_queue_message** 便可以從字串或 **byte** 陣列建立。 以下是它會建立佇列 （如果存在） 並插入 hello 訊息 'Hello World' 的程式碼：

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a>如何： 檢視 hello 的下一個訊息
您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello **peek_message**方法。

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>如何： 變更 hello 的佇列訊息的內容
您可以變更訊息就地 hello 佇列中的 hello 的內容。 如果 hello 訊息代表的工作，您可以使用此功能 tooupdate hello 的 hello 工作工作狀態。 下列程式碼的 hello 更新 hello 佇列訊息與新的內容，並設定 hello 的可見性逾時 tooextend 另一個 60 秒。 這樣會節省 hello 與 hello 訊息相關聯的工作狀態，並提供 hello 用戶端 hello 訊息處理的另一個分鐘 toocontinue。 您無法使用此技巧 tootrack 多步驟工作流程佇列的訊息，而不需 toostart 透過從 hello 開頭，如果因為 toohardware 或軟體失敗的處理步驟失敗。 一般而言，您會保留重試計數，而且如果多個 n 次重試 hello 訊息，您會將它刪除。 這麼做可防止每次處理時便觸發應用程式錯誤的訊息。

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a>如何： 清除佇列 hello 下一個訊息
您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。 當您呼叫**get_message**，您會收到 hello 下一個訊息，佇列中。 傳回訊息**get_message**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。 toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**delete_message**。 這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。 您的程式碼呼叫**delete_message**處理 hello 訊息之後，以滑鼠右鍵。

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>作法：運用清除佇列訊息的其他選項
自訂從佇列中擷取訊息的方法有兩種。 首先，您可以取得一批訊息 （向上 too32)。 第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。 hello 下列程式碼範例會使用 hello **get_messages**方法 tooget 20 訊息在單一呼叫中的。 接著它會使用 **for** 迴圈處理每個訊息。 它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。 請注意該 hello 5 分鐘所有 hello 訊息啟動相同的時間，因此後 5 分鐘自以來已經過 hello 呼叫太**get_messages**，任何已被刪除的訊息一次將變成可見。

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a>如何： 取得 hello 佇列長度
您可以在佇列中取得估計的 hello 訊息數目。 hello **download_attributes**方法會要求 hello 佇列服務 tooretrieve hello 佇列屬性，包括 hello 訊息計數。 hello **approximate_message_count**方法取得 hello 佇列中的 hello 大約的訊息數目。

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a>作法：刪除佇列
佇列和所有 hello 訊息包含在它呼叫 hello toodelete **delete_queue_if_exists** hello 佇列物件上的方法。

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a>後續步驟
現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure 儲存體。

* [如何 toouse 從 c + + 的 Blob 儲存體](storage-c-plus-plus-how-to-use-blobs.md)
* [如何 toouse 從 c + + 的資料表儲存體](storage-c-plus-plus-how-to-use-tables.md)
* [以 C++ 列出 Azure 儲存體資源](storage-c-plus-plus-enumeration.md)
* [Storage Client Library for C++ 參考資料](http://azure.github.io/azure-storage-cpp)
* [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)