---
title: "aaaGet 開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 (ASP.NET) |Microsoft 文件"
description: "Tooget 啟動連接 tooa 使用 Visual Studio 已連接服務的儲存體帳戶之後，Visual Studio 中 ASP.NET 專案中使用 Azure 佇列儲存體的方式"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="21e14-103">開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="21e14-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="21e14-104">概觀</span><span class="sxs-lookup"><span data-stu-id="21e14-104">Overview</span></span>

<span data-ttu-id="21e14-105">Azure 佇列儲存體可提供應用程式元件之間的雲端傳訊。</span><span class="sxs-lookup"><span data-stu-id="21e14-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="21e14-106">設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。</span><span class="sxs-lookup"><span data-stu-id="21e14-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="21e14-107">佇列儲存體提供非同步傳訊應用程式元件之間的通訊是否在 hello 雲端中，在 hello 桌面上、 在內部部署伺服器上，或行動裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="21e14-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="21e14-108">佇列儲存體也支援管理非同步工作並建置處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="21e14-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="21e14-109">本教學課程會示範 toowrite ASP.NET 為使用 Azure 佇列儲存體實體一些常見案例的程式碼。</span><span class="sxs-lookup"><span data-stu-id="21e14-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="21e14-110">這些案例包括一般工作，例如建立 Azure 佇列，以及新增、修改、讀取和移除佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="21e14-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="21e14-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="21e14-111">Prerequisites</span></span>

* [<span data-ttu-id="21e14-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21e14-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="21e14-113">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="21e14-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="21e14-114">建立 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="21e14-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="21e14-115">在 hello**方案總管 中**，以滑鼠右鍵按一下**控制站**，並從 hello 內容功能表中，選取**加入控制器->** 。</span><span class="sxs-lookup"><span data-stu-id="21e14-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![加入控制器 tooan ASP.NET MVC 應用程式](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="21e14-117">在 hello**新增 Scaffold**對話方塊中，選取**MVC 5 控制器空白**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="21e14-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![指定 MVC 控制器類型](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="21e14-119">在 hello**加入控制器**對話方塊中，名稱 hello 控制器*QueuesController*，並選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="21e14-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![名稱 hello MVC 控制器](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="21e14-121">新增下列 hello*使用*指示詞 toohello`QueuesController.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="21e14-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="21e14-122">建立佇列</span><span class="sxs-lookup"><span data-stu-id="21e14-122">Create a queue</span></span>

<span data-ttu-id="21e14-123">hello 下列步驟說明如何 toocreate 佇列：</span><span class="sxs-lookup"><span data-stu-id="21e14-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="21e14-124">本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="21e14-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="21e14-125">開啟 hello`QueuesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="21e14-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="21e14-126">新增名為 **CreateQueue** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="21e14-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="21e14-127">在 hello **CreateQueue**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="21e14-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="21e14-128">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="21e14-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="21e14-129">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="21e14-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="21e14-130">取得**CloudQueue**物件，表示參考 toohello 所需的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="21e14-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="21e14-131">hello **CloudQueueClient.GetQueueReference**方法不會對佇列儲存體的要求。</span><span class="sxs-lookup"><span data-stu-id="21e14-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="21e14-132">不論是否 hello 佇列存在，則會傳回 hello 參考。</span><span class="sxs-lookup"><span data-stu-id="21e14-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="21e14-133">呼叫 hello **CloudQueue.CreateIfNotExists**方法 toocreate hello 佇列如果尚不存在。</span><span class="sxs-lookup"><span data-stu-id="21e14-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="21e14-134">hello **CloudQueue.CreateIfNotExists**方法會傳回**true**如果 hello 佇列不存在，而且已成功建立。</span><span class="sxs-lookup"><span data-stu-id="21e14-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="21e14-135">否則，會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="21e14-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="21e14-136">更新 hello **ViewBag** hello hello 佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="21e14-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="21e14-137">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="21e14-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="21e14-138">在 [hello**加入檢視**] 對話方塊中，輸入**CreateQueue** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="21e14-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="21e14-139">開啟`CreateQueue.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="21e14-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="21e14-140">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="21e14-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="21e14-141">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="21e14-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="21e14-142">執行 hello 應用程式，並選取**建立佇列**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="21e14-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![建立佇列](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="21e14-144">如先前所述，hello **CloudQueue.CreateIfNotExists**方法會傳回**true**只當 hello 佇列不存在，而且會建立。</span><span class="sxs-lookup"><span data-stu-id="21e14-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="21e14-145">因此，如果 hello 佇列存在時，您可以執行 hello 應用程式，hello 方法會傳回**false**。</span><span class="sxs-lookup"><span data-stu-id="21e14-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="21e14-146">toorun hello 應用程式多次，必須刪除 hello 佇列，才能再次執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21e14-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="21e14-147">正在刪除 hello 佇列可透過 hello **CloudQueue.Delete**方法。</span><span class="sxs-lookup"><span data-stu-id="21e14-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="21e14-148">您也可以刪除使用 hello hello 佇列[Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)或 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="21e14-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="21e14-149">新增訊息 tooa 佇列</span><span class="sxs-lookup"><span data-stu-id="21e14-149">Add a message tooa queue</span></span>

<span data-ttu-id="21e14-150">一旦您[建立佇列](#create-a-queue)，您可以新增訊息 toothat 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="21e14-151">本節將引導您完成新增訊息 tooa 佇列*測試佇列*。</span><span class="sxs-lookup"><span data-stu-id="21e14-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="21e14-152">本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="21e14-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="21e14-153">開啟 hello`QueuesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="21e14-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="21e14-154">新增名為 **AddMessage** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="21e14-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="21e14-155">在 hello **AddMessage**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="21e14-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="21e14-156">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="21e14-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="21e14-157">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="21e14-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="21e14-158">取得**CloudQueueContainer**物件，代表參考 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="21e14-159">建立 hello **CloudQueueMessage**物件，代表您想要 tooadd toohello 佇列 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="21e14-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="21e14-160">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 物件。</span><span class="sxs-lookup"><span data-stu-id="21e14-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="21e14-161">呼叫 hello **CloudQueue.AddMessage**方法 tooadd hello 依現狀 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="21e14-162">建立並設定幾個**ViewBag** hello 檢視中顯示的屬性。</span><span class="sxs-lookup"><span data-stu-id="21e14-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="21e14-163">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="21e14-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="21e14-164">在 [hello**加入檢視**] 對話方塊中，輸入**AddMessage** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="21e14-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="21e14-165">開啟`AddMessage.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="21e14-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="21e14-166">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="21e14-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="21e14-167">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="21e14-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="21e14-168">執行 hello 應用程式，並選取**新增訊息**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="21e14-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![新增訊息](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="21e14-170">hello 兩個區段-[從佇列讀取訊息，而不移除它](#read-a-message-from-a-queue-without-removing-it)和[讀取並將訊息從佇列移除](#read-and-remove-a-message-from-a-queue)-說明如何 tooread 訊息從佇列中。</span><span class="sxs-lookup"><span data-stu-id="21e14-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="21e14-171">讀取佇列中的訊息，但不移除它</span><span class="sxs-lookup"><span data-stu-id="21e14-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="21e14-172">本節說明如何 toopeek 排入佇列的訊息 （hello 讀取第一則訊息而不移除它）。</span><span class="sxs-lookup"><span data-stu-id="21e14-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="21e14-173">本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="21e14-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="21e14-174">開啟 hello`QueuesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="21e14-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="21e14-175">新增名為 **PeekMessage** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="21e14-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="21e14-176">在 hello **PeekMessage**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="21e14-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="21e14-177">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="21e14-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="21e14-178">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="21e14-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="21e14-179">取得**CloudQueueContainer**物件，代表參考 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="21e14-180">呼叫 hello **CloudQueue.PeekMessage** hello 佇列，而不需移除 hello 佇列中的方法 tooread hello 第一個訊息。</span><span class="sxs-lookup"><span data-stu-id="21e14-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="21e14-181">更新 hello **ViewBag**具有兩個值： hello 佇列名稱 」 和 「 已讀取的 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="21e14-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="21e14-182">hello **CloudQueueMessage**物件會公開兩個屬性來取得 hello 物件的值： **CloudQueueMessage.AsBytes**和**CloudQueueMessage.AsString**。</span><span class="sxs-lookup"><span data-stu-id="21e14-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="21e14-183">**AsString** (在此範例中使用) 會傳回字串，而 **AsBytes** 會傳回位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="21e14-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="21e14-184">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="21e14-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="21e14-185">在 [hello**加入檢視**] 對話方塊中，輸入**PeekMessage** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="21e14-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="21e14-186">開啟`PeekMessage.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="21e14-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="21e14-187">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="21e14-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="21e14-188">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="21e14-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="21e14-189">執行 hello 應用程式，並選取**窺視訊息**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="21e14-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![查看訊息](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="21e14-191">讀取並移除佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="21e14-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="21e14-192">在本節中，您學會如何 tooread 並從佇列移除訊息。</span><span class="sxs-lookup"><span data-stu-id="21e14-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="21e14-193">本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="21e14-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="21e14-194">開啟 hello`QueuesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="21e14-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="21e14-195">新增名為 **ReadMessage** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="21e14-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="21e14-196">在 hello **ReadMessage**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="21e14-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="21e14-197">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="21e14-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="21e14-198">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="21e14-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="21e14-199">取得**CloudQueueContainer**物件，代表參考 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="21e14-200">呼叫 hello **CloudQueue.GetMessage** hello 佇列中的方法 tooread hello 第一個訊息。</span><span class="sxs-lookup"><span data-stu-id="21e14-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="21e14-201">hello **CloudQueue.GetMessage**方法讓 hello 訊息顯示為 30 秒 （依預設） tooany 讀取訊息，讓其他程式碼可以修改或刪除 hello 訊息，您在處理時它的其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="21e14-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="21e14-202">toochange hello 數量時間 hello 訊息是不可見，請修改 hello **visibilityTimeout**參數傳入 toohello **CloudQueue.GetMessage**方法。</span><span class="sxs-lookup"><span data-stu-id="21e14-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="21e14-203">呼叫 hello **CloudQueueMessage.Delete**方法 toodelete hello 訊息從 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="21e14-204">更新 hello **ViewBag**以 hello 訊息刪除，而且 hello hello 佇列的名稱。</span><span class="sxs-lookup"><span data-stu-id="21e14-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="21e14-205">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="21e14-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="21e14-206">在 [hello**加入檢視**] 對話方塊中，輸入**ReadMessage** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="21e14-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="21e14-207">開啟`ReadMessage.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="21e14-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="21e14-208">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="21e14-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="21e14-209">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="21e14-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="21e14-210">執行 hello 應用程式，並選取**讀取/刪除訊息**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="21e14-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![讀取和刪除訊息](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="21e14-212">取得 hello 佇列長度</span><span class="sxs-lookup"><span data-stu-id="21e14-212">Get hello queue length</span></span>

<span data-ttu-id="21e14-213">本節說明如何 tooget hello 佇列長度 （訊息數目）。</span><span class="sxs-lookup"><span data-stu-id="21e14-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="21e14-214">本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="21e14-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="21e14-215">開啟 hello`QueuesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="21e14-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="21e14-216">新增名為 **GetQueueLength** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="21e14-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="21e14-217">在 hello **ReadMessage**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="21e14-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="21e14-218">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="21e14-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="21e14-219">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="21e14-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="21e14-220">取得**CloudQueueContainer**物件，代表參考 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="21e14-221">呼叫 hello **CloudQueue.FetchAttributes**方法 tooretrieve hello 佇列的屬性 （包括它的長度）。</span><span class="sxs-lookup"><span data-stu-id="21e14-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="21e14-222">存取 hello **CloudQueue.ApproximateMessageCount**屬性 tooget hello 佇列的長度。</span><span class="sxs-lookup"><span data-stu-id="21e14-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="21e14-223">更新 hello **ViewBag**具有 hello 名稱 hello 佇列和它的長度。</span><span class="sxs-lookup"><span data-stu-id="21e14-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="21e14-224">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="21e14-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="21e14-225">在 [hello**加入檢視**] 對話方塊中，輸入**GetQueueLength** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="21e14-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="21e14-226">開啟`GetQueueLengthMessage.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="21e14-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="21e14-227">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="21e14-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="21e14-228">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="21e14-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="21e14-229">執行 hello 應用程式，並選取**取得佇列長度**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="21e14-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![取得佇列長度](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="21e14-231">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="21e14-231">Delete a queue</span></span>
<span data-ttu-id="21e14-232">本節說明如何 toodelete 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="21e14-233">本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="21e14-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="21e14-234">開啟 hello`QueuesController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="21e14-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="21e14-235">新增名為 **DeleteQueue** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="21e14-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="21e14-236">在 hello **deletequeue 等**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="21e14-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="21e14-237">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="21e14-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="21e14-238">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="21e14-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="21e14-239">取得**CloudQueueContainer**物件，代表參考 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="21e14-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="21e14-240">呼叫 hello **CloudQueue.Delete**方法 toodelete hello 佇列由 hello **CloudQueue**物件。</span><span class="sxs-lookup"><span data-stu-id="21e14-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="21e14-241">更新 hello **ViewBag**具有 hello 名稱 hello 佇列和它的長度。</span><span class="sxs-lookup"><span data-stu-id="21e14-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="21e14-242">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="21e14-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="21e14-243">在 [hello**加入檢視**] 對話方塊中，輸入**deletequeue 等**hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="21e14-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="21e14-244">開啟`DeleteQueue.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="21e14-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="21e14-245">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="21e14-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="21e14-246">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="21e14-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="21e14-247">執行 hello 應用程式，並選取**取得佇列長度**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="21e14-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![刪除佇列](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="21e14-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21e14-249">Next steps</span></span>
<span data-ttu-id="21e14-250">檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。</span><span class="sxs-lookup"><span data-stu-id="21e14-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="21e14-251">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="21e14-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="21e14-252">開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="21e14-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
