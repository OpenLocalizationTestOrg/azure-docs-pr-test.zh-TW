---
title: "如何使用佇列儲存體 (C++) | Microsoft Docs"
description: "了解如何在 Azure 中使用佇列儲存體服務。 範例是以 C++ 撰寫的。"
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
ms.openlocfilehash: 85e4d95549ca5edd375f3b15971634e032a3962a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="721e0-104">如何使用 C++ 的佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="721e0-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="721e0-105">Overview</span><span class="sxs-lookup"><span data-stu-id="721e0-105">Overview</span></span>
<span data-ttu-id="721e0-106">本指南將示範如何使用 Azure 佇列儲存服務執行一般案例。</span><span class="sxs-lookup"><span data-stu-id="721e0-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="721e0-107">這些範例均以 C++ 撰寫，並使用 [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="721e0-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="721e0-108">所涵蓋的案例包括「插入」、「查看」、「取得」和「刪除」佇列訊息，以及「建立和刪除佇列」。</span><span class="sxs-lookup"><span data-stu-id="721e0-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="721e0-109">本指南以 Azure Storage Client Library for C++ 1.0.0 版和更新版本為對象。</span><span class="sxs-lookup"><span data-stu-id="721e0-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="721e0-110">建議的版本是 Storage Client Library 2.2.0，可透過 [NuGet](http://www.nuget.org/packages/wastorage) 或 [GitHub](http://github.com/Azure/azure-storage-cpp/) 取得。</span><span class="sxs-lookup"><span data-stu-id="721e0-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="721e0-111">建立 C++ 應用程式</span><span class="sxs-lookup"><span data-stu-id="721e0-111">Create a C++ application</span></span>
<span data-ttu-id="721e0-112">在本指南中，您將使用可以在 C++ 應用程式內執行的儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="721e0-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="721e0-113">若要這樣做，您需要安裝 Azure Storage Client Library for C++，並在 Azure 訂用帳戶中建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="721e0-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="721e0-114">若要安裝 Azure Storage Client Library for C++，您可以使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="721e0-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="721e0-115">**Linux：** 遵循 [Azure Storage Client Library for C++ 讀我檔案](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) 頁面中提供的指示進行。</span><span class="sxs-lookup"><span data-stu-id="721e0-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="721e0-116">**Windows：**在 Visual Studio 中，按一下 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="721e0-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="721e0-117">在 [NuGet 套件管理員主控台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 中輸入下列命令，然後按下 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="721e0-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="721e0-118">設定您的應用程式以存取佇列儲存體</span><span class="sxs-lookup"><span data-stu-id="721e0-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="721e0-119">在您要使用 Azure 儲存體 API 來存取佇列的 C++ 檔案頂端，加入下列 include 陳述式：</span><span class="sxs-lookup"><span data-stu-id="721e0-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="721e0-120">設定 Azure 儲存體連接字串</span><span class="sxs-lookup"><span data-stu-id="721e0-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="721e0-121">Azure 儲存體用戶端會使用儲存體連接字串來儲存存取資料管理服務時所用的端點與認證。</span><span class="sxs-lookup"><span data-stu-id="721e0-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="721e0-122">在用戶端應用程式中執行時，您必須以下列格式提供儲存體連接字串 (其中的 *AccountName* 和 *AccountKey* 值要使用您儲存體帳戶的名稱，以及在 [Azure 入口網站](https://portal.azure.com)中針對該儲存體帳戶而列出的儲存體存取金鑰)。</span><span class="sxs-lookup"><span data-stu-id="721e0-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="721e0-123">如需有關儲存體帳戶和存取金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="721e0-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="721e0-124">本範例將示範如何宣告靜態欄位來存放連接字串：</span><span class="sxs-lookup"><span data-stu-id="721e0-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="721e0-125">若要在本機 Windows 電腦中測試您的應用程式，可以使用隨 [Azure SDK](https://azure.microsoft.com/downloads/) 一起安裝的 Microsoft Azure [儲存體模擬器](storage-use-emulator.md)。</span><span class="sxs-lookup"><span data-stu-id="721e0-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="721e0-126">儲存體模擬器是一個公用程式，可在本機開發電腦上模擬 Azure 提供的 Blob、佇列和表格服務。</span><span class="sxs-lookup"><span data-stu-id="721e0-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="721e0-127">下列範例示範如何宣告靜態欄位以便將連接字串存放到本機儲存體模擬器中：</span><span class="sxs-lookup"><span data-stu-id="721e0-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="721e0-128">若要啟動 Azure 儲存體模擬器，選取 [開始] 按鈕或按下 [Windows] 鍵。</span><span class="sxs-lookup"><span data-stu-id="721e0-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="721e0-129">開始輸入 **Azure 儲存體模擬器**，然後從應用程式清單選取 [Microsoft Azure 儲存體模擬器]。</span><span class="sxs-lookup"><span data-stu-id="721e0-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="721e0-130">下列範例假設您已經使用這兩個方法之一來取得儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="721e0-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="721e0-131">擷取連接字串</span><span class="sxs-lookup"><span data-stu-id="721e0-131">Retrieve your connection string</span></span>
<span data-ttu-id="721e0-132">您可以使用 **cloud_storage_account** 類別來代表儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="721e0-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="721e0-133">若要從儲存體連接字串擷取儲存體帳戶資訊，您可以使用 **parse** 方法。</span><span class="sxs-lookup"><span data-stu-id="721e0-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="721e0-134">作法：建立佇列</span><span class="sxs-lookup"><span data-stu-id="721e0-134">How to: Create a queue</span></span>
<span data-ttu-id="721e0-135">**cloud_queue_client** 物件可讓您取得佇列的參考物件。</span><span class="sxs-lookup"><span data-stu-id="721e0-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="721e0-136">下列程式碼會建立一個 **cloud_queue_client** 物件。</span><span class="sxs-lookup"><span data-stu-id="721e0-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="721e0-137">使用 **cloud_queue_client** 物件取得想要使用的佇列的參考。</span><span class="sxs-lookup"><span data-stu-id="721e0-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="721e0-138">如果佇列不存在，您可以建立佇列。</span><span class="sxs-lookup"><span data-stu-id="721e0-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="721e0-139">作法：將訊息插入佇列中</span><span class="sxs-lookup"><span data-stu-id="721e0-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="721e0-140">若要將訊息插入現有佇列，請先建立一個新的 **cloud_queue_message**。</span><span class="sxs-lookup"><span data-stu-id="721e0-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="721e0-141">接著，呼叫 **add_message** 方法。</span><span class="sxs-lookup"><span data-stu-id="721e0-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="721e0-142">**cloud_queue_message** 便可以從字串或 **byte** 陣列建立。</span><span class="sxs-lookup"><span data-stu-id="721e0-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="721e0-143">以下是建立佇列 (如果佇列不存在) 並插入訊息 'Hello, World' 的程式碼：</span><span class="sxs-lookup"><span data-stu-id="721e0-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="721e0-144">作法：查看下一個訊息</span><span class="sxs-lookup"><span data-stu-id="721e0-144">How to: Peek at the next message</span></span>
<span data-ttu-id="721e0-145">您可以呼叫 **peek_message** 方法，以便在佇列前面查看訊息，而無需將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="721e0-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="721e0-146">作法：變更佇列訊息的內容</span><span class="sxs-lookup"><span data-stu-id="721e0-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="721e0-147">您可以在佇列中就地變更訊息內容。</span><span class="sxs-lookup"><span data-stu-id="721e0-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="721e0-148">如果訊息代表工作作業，則您可以使用此功能來更新工作作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="721e0-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="721e0-149">下列程式碼將使用新的內容更新佇列訊息，並將可見度逾時設定延長 60 秒。</span><span class="sxs-lookup"><span data-stu-id="721e0-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="721e0-150">這可儲存與訊息相關的工作狀態，並提供用戶端多一分鐘的時間繼續處理訊息。</span><span class="sxs-lookup"><span data-stu-id="721e0-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="721e0-151">您可以使用此技巧來追蹤佇列訊息上的多步驟工作流程，如果因為硬體或軟體故障而導致某個處理步驟失敗，將無需從頭開始。</span><span class="sxs-lookup"><span data-stu-id="721e0-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="721e0-152">通常，您也會保留重試計數，如果訊息重試超過 n 次，您會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="721e0-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="721e0-153">這麼做可防止每次處理時便觸發應用程式錯誤的訊息。</span><span class="sxs-lookup"><span data-stu-id="721e0-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="721e0-154">作法：在下一個訊息清除佇列</span><span class="sxs-lookup"><span data-stu-id="721e0-154">How to: De-queue the next message</span></span>
<span data-ttu-id="721e0-155">您的程式碼可以使用兩個步驟將訊息自佇列中清除佇列。</span><span class="sxs-lookup"><span data-stu-id="721e0-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="721e0-156">呼叫 **get_message** 時，您會取得佇列中的下一個訊息。</span><span class="sxs-lookup"><span data-stu-id="721e0-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="721e0-157">對於從此佇列讀取訊息的其他任何程式碼而言，將無法看到從 **get_message** 傳回的訊息。</span><span class="sxs-lookup"><span data-stu-id="721e0-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="721e0-158">若要完成從佇列中移除訊息的作業，您還必須呼叫 **delete_message**。</span><span class="sxs-lookup"><span data-stu-id="721e0-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="721e0-159">這個移除訊息的兩步驟程序可確保您的程式碼因為硬體或軟體故障而無法處理訊息時，另一個程式碼的執行個體可以取得相同訊息並再試一次。</span><span class="sxs-lookup"><span data-stu-id="721e0-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="721e0-160">您的程式碼會在處理完訊息之後立即呼叫 **delete_message**。</span><span class="sxs-lookup"><span data-stu-id="721e0-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="721e0-161">作法：運用清除佇列訊息的其他選項</span><span class="sxs-lookup"><span data-stu-id="721e0-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="721e0-162">自訂從佇列中擷取訊息的方法有兩種。</span><span class="sxs-lookup"><span data-stu-id="721e0-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="721e0-163">首先，您可以取得一批訊息 (最多 32 個)。</span><span class="sxs-lookup"><span data-stu-id="721e0-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="721e0-164">其次，您可以設定較長或較短的可見度逾時，讓您的程式碼有較長或較短的時間可以完全處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="721e0-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="721e0-165">下列程式碼範例將使用 **get_messages** 方法，在一次呼叫中取得 20 個訊息。</span><span class="sxs-lookup"><span data-stu-id="721e0-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="721e0-166">接著它會使用 **for** 迴圈處理每個訊息。</span><span class="sxs-lookup"><span data-stu-id="721e0-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="721e0-167">它也會將可見度逾時設定為每個訊息五分鐘。</span><span class="sxs-lookup"><span data-stu-id="721e0-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="721e0-168">請注意，系統會針對所有訊息同時開始計時 5 分鐘，所以從呼叫 **get_messages** 開始的 5 分鐘後，任何尚未刪除的訊息都會重新出現。</span><span class="sxs-lookup"><span data-stu-id="721e0-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="721e0-169">作法：取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="721e0-169">How to: Get the queue length</span></span>
<span data-ttu-id="721e0-170">您可以取得佇列中的估計訊息數目。</span><span class="sxs-lookup"><span data-stu-id="721e0-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="721e0-171">**download_attributes** 方法會要求佇列服務擷取佇列屬性，其中包含訊息計數。</span><span class="sxs-lookup"><span data-stu-id="721e0-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="721e0-172">**approximate_message_count** 方法會取得佇列中大約的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="721e0-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="721e0-173">作法：刪除佇列</span><span class="sxs-lookup"><span data-stu-id="721e0-173">How to: Delete a queue</span></span>
<span data-ttu-id="721e0-174">若要刪除佇列及其內含的所有訊息，請針對佇列物件呼叫 **delete_queue_if_exists** 方法。</span><span class="sxs-lookup"><span data-stu-id="721e0-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="721e0-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="721e0-175">Next steps</span></span>
<span data-ttu-id="721e0-176">了解佇列儲存體的基礎概念之後，請依照下列連結深入了解 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="721e0-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="721e0-177">如何使用 C++ 的 Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="721e0-177">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="721e0-178">如何使用 C++ 的資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="721e0-178">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="721e0-179">以 C++ 列出 Azure 儲存體資源</span><span class="sxs-lookup"><span data-stu-id="721e0-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="721e0-180">Storage Client Library for C++ 參考資料</span><span class="sxs-lookup"><span data-stu-id="721e0-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="721e0-181">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="721e0-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)