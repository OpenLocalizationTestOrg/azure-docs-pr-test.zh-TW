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
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="8e3b1-104">如何 toouse 佇列儲存體從 c + +</span><span class="sxs-lookup"><span data-stu-id="8e3b1-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="8e3b1-105">概觀</span><span class="sxs-lookup"><span data-stu-id="8e3b1-105">Overview</span></span>
<span data-ttu-id="8e3b1-106">本指南將說明如何使用 tooperform 常見案例 hello Azure 佇列儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="8e3b1-107">hello 範例以 c + + 撰寫，並使用 hello [c + + 的 Azure 儲存體用戶端程式庫](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="8e3b1-108">hello 涵蓋案例包括**插入**，**其內**，**取得**，和**刪除**佇列訊息，以及**建立及刪除佇列**。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="8e3b1-109">此指南的目標 hello Azure 儲存體用戶端程式庫，c + + 1.0.0 版和更新版本。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="8e3b1-110">hello 建議版本是儲存體用戶端程式庫 2.2.0，也就是可透過使用[NuGet](http://www.nuget.org/packages/wastorage)或[GitHub](http://github.com/Azure/azure-storage-cpp/)。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="8e3b1-111">建立 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="8e3b1-111">Create a C++ application</span></span>
<span data-ttu-id="8e3b1-112">在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="8e3b1-113">toodo 因此，您將需要 tooinstall hello for c + + 的 Azure 儲存體用戶端程式庫，並在您的 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="8e3b1-114">tooinstall hello Azure 儲存體用戶端程式庫的 c + +，，您可以使用下列方法的 hello:</span><span class="sxs-lookup"><span data-stu-id="8e3b1-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="8e3b1-115">**Linux:**遵循 hello 所提供的 hello 指示[for c + + 讀我檔案的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-cpp/blob/master/README.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="8e3b1-116">**Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="8e3b1-117">型別 hello 下列命令到 hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="8e3b1-118">設定您的應用程式 tooaccess 佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="8e3b1-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="8e3b1-119">加入 hello 下列包含您想要 toouse hello Azure 儲存體 Api tooaccess 佇列 hello c + + 檔案的陳述式 toohello 頂端：</span><span class="sxs-lookup"><span data-stu-id="8e3b1-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="8e3b1-120">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="8e3b1-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="8e3b1-121">Azure 儲存體用戶端會使用儲存體連接字串 toostore 端點和認證來存取資料管理服務。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8e3b1-122">用戶端應用程式中執行時，您必須提供 hello 遵循格式，並透過儲存體帳戶和 hello 儲存體存取金鑰的 hello 名稱 hello hello 中所列的儲存體帳戶中的 hello 儲存體連接字串[Azure 入口網站](https://portal.azure.com)hello *AccountName*和*AccountKey*值。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8e3b1-123">如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="8e3b1-124">此範例顯示如何宣告靜態欄位 toohold hello 連接字串：</span><span class="sxs-lookup"><span data-stu-id="8e3b1-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="8e3b1-125">tootest 您的應用程式在本機的 Windows 電腦，您可以使用 Microsoft Azure 的 hello[儲存體模擬器](storage-use-emulator.md)會隨 hello [Azure SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="8e3b1-126">hello 儲存體模擬器是模擬 hello Blob、 佇列和表格服務在本機開發電腦上可用在 Azure 中的公用程式。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="8e3b1-127">hello 下列範例顯示如何宣告靜態欄位 toohold hello 連接字串 tooyour 本機儲存體模擬器：</span><span class="sxs-lookup"><span data-stu-id="8e3b1-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="8e3b1-128">toostart hello Azure 儲存體模擬器中，選取 hello**啟動**按鈕或按 hello **Windows**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="8e3b1-129">開始輸入**Azure 儲存體模擬器**，然後選取**Microsoft Azure 儲存體模擬器**hello 清單中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="8e3b1-130">hello 下列範例假設您已使用下列兩種方法 tooget hello 儲存體連接字串的其中一個。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="8e3b1-131">擷取連接字串</span><span class="sxs-lookup"><span data-stu-id="8e3b1-131">Retrieve your connection string</span></span>
<span data-ttu-id="8e3b1-132">您可以使用 hello**驗證 cloud_storage_account**類別 toorepresent 儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="8e3b1-133">tooretrieve 您的儲存體帳戶資訊 hello 儲存體連接字串，您可以使用 hello**剖析**方法。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="8e3b1-134">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="8e3b1-134">How to: Create a queue</span></span>
<span data-ttu-id="8e3b1-135">**cloud_queue_client** 物件可讓您取得佇列的參考物件。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="8e3b1-136">hello 下列程式碼會建立**cloud_queue_client**物件。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="8e3b1-137">使用 hello **cloud_queue_client** tooget 想 toouse 參考 toohello 佇列的物件。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="8e3b1-138">如果不存在，您可以建立 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="8e3b1-139">作法：將訊息插入佇列中</span><span class="sxs-lookup"><span data-stu-id="8e3b1-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="8e3b1-140">tooinsert 將訊息插入現有佇列，先建立新**cloud_queue_message**。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="8e3b1-141">接下來，呼叫 hello **add_message**方法。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="8e3b1-142">**cloud_queue_message** 便可以從字串或 **byte** 陣列建立。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="8e3b1-143">以下是它會建立佇列 （如果存在） 並插入 hello 訊息 'Hello World' 的程式碼：</span><span class="sxs-lookup"><span data-stu-id="8e3b1-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

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

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="8e3b1-144">如何： 檢視 hello 的下一個訊息</span><span class="sxs-lookup"><span data-stu-id="8e3b1-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="8e3b1-145">您可以查看 hello 前方的佇列中的 hello 訊息而不需移除 hello 佇列中所呼叫的 hello **peek_message**方法。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="8e3b1-146">如何： 變更 hello 的佇列訊息的內容</span><span class="sxs-lookup"><span data-stu-id="8e3b1-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="8e3b1-147">您可以變更訊息就地 hello 佇列中的 hello 的內容。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="8e3b1-148">如果 hello 訊息代表的工作，您可以使用此功能 tooupdate hello 的 hello 工作工作狀態。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="8e3b1-149">下列程式碼的 hello 更新 hello 佇列訊息與新的內容，並設定 hello 的可見性逾時 tooextend 另一個 60 秒。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="8e3b1-150">這樣會節省 hello 與 hello 訊息相關聯的工作狀態，並提供 hello 用戶端 hello 訊息處理的另一個分鐘 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="8e3b1-151">您無法使用此技巧 tootrack 多步驟工作流程佇列的訊息，而不需 toostart 透過從 hello 開頭，如果因為 toohardware 或軟體失敗的處理步驟失敗。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="8e3b1-152">一般而言，您會保留重試計數，而且如果多個 n 次重試 hello 訊息，您會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="8e3b1-153">這麼做可防止每次處理時便觸發應用程式錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-153">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="8e3b1-154">如何： 清除佇列 hello 下一個訊息</span><span class="sxs-lookup"><span data-stu-id="8e3b1-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="8e3b1-155">您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="8e3b1-156">當您呼叫**get_message**，您會收到 hello 下一個訊息，佇列中。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="8e3b1-157">傳回訊息**get_message**變成不可見的 tooany 從此佇列讀取訊息的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="8e3b1-158">toofinish 移除 hello 訊息從 hello 佇列，您必須也呼叫**delete_message**。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="8e3b1-159">這兩個步驟的程序中移除訊息可確保，如果您的程式碼失敗的 tooprocess 到期 toohardware 或軟體失敗，您的程式碼的另一個執行個體訊息可以取得 hello 相同的訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="8e3b1-160">您的程式碼呼叫**delete_message**處理 hello 訊息之後，以滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="8e3b1-161">作法：運用清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="8e3b1-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="8e3b1-162">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="8e3b1-163">首先，您可以取得一批訊息 （向上 too32)。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="8e3b1-164">第二，您可以設定長或短過了隱藏逾時，可讓您的程式碼更多或較少時間 toofully 處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="8e3b1-165">hello 下列程式碼範例會使用 hello **get_messages**方法 tooget 20 訊息在單一呼叫中的。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="8e3b1-166">接著它會使用 **for** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="8e3b1-167">它也會設定 hello 過了隱藏逾時 toofive 分鐘數的每個訊息。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="8e3b1-168">請注意該 hello 5 分鐘所有 hello 訊息啟動相同的時間，因此後 5 分鐘自以來已經過 hello 呼叫太**get_messages**，任何已被刪除的訊息一次將變成可見。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

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

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="8e3b1-169">如何： 取得 hello 佇列長度</span><span class="sxs-lookup"><span data-stu-id="8e3b1-169">How to: Get hello queue length</span></span>
<span data-ttu-id="8e3b1-170">您可以在佇列中取得估計的 hello 訊息數目。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="8e3b1-171">hello **download_attributes**方法會要求 hello 佇列服務 tooretrieve hello 佇列屬性，包括 hello 訊息計數。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="8e3b1-172">hello **approximate_message_count**方法取得 hello 佇列中的 hello 大約的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

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

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="8e3b1-173">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="8e3b1-173">How to: Delete a queue</span></span>
<span data-ttu-id="8e3b1-174">佇列和所有 hello 訊息包含在它呼叫 hello toodelete **delete_queue_if_exists** hello 佇列物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8e3b1-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e3b1-175">Next steps</span></span>
<span data-ttu-id="8e3b1-176">現在，您學到的佇列儲存體的 hello 基本概念，請遵循這些連結 toolearn 深入了解 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8e3b1-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="8e3b1-177">如何 toouse 從 c + + 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="8e3b1-177">How toouse Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="8e3b1-178">如何 toouse 從 c + + 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="8e3b1-178">How toouse Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="8e3b1-179">以 C++ 列出 Azure 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="8e3b1-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="8e3b1-180">Storage Client Library for C++ 參考資料</span><span class="sxs-lookup"><span data-stu-id="8e3b1-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="8e3b1-181">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="8e3b1-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)