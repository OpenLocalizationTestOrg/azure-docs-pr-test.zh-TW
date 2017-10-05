---
title: "開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET) | Microsoft Docs"
description: "在使用 Visual Studio 已連接服務連接到儲存體帳戶之後，如何在 Visual Studio ASP.NET 專案中開始使用 Azure 佇列儲存體"
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
ms.openlocfilehash: 76b0d5e270e16a317ce8a7b424c06c867b537a8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="86172-103">開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="86172-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="86172-104">概觀</span><span class="sxs-lookup"><span data-stu-id="86172-104">Overview</span></span>

<span data-ttu-id="86172-105">Azure 佇列儲存體可提供應用程式元件之間的雲端傳訊。</span><span class="sxs-lookup"><span data-stu-id="86172-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="86172-106">設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。</span><span class="sxs-lookup"><span data-stu-id="86172-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="86172-107">佇列儲存體可針對應用程式元件間的通訊，提供非同步傳訊，無論應用程式元件是在雲端、桌面、內部部署伺服器或行動裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="86172-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="86172-108">佇列儲存體也支援管理非同步工作並建置處理工作流程。</span><span class="sxs-lookup"><span data-stu-id="86172-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="86172-109">本教學課程說明如何使用 Azure 佇列儲存體實體撰寫一些常見案例的 ASP.NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="86172-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="86172-110">這些案例包括一般工作，例如建立 Azure 佇列，以及新增、修改、讀取和移除佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="86172-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="86172-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="86172-111">Prerequisites</span></span>

* [<span data-ttu-id="86172-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86172-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="86172-113">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="86172-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="86172-114">建立 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="86172-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="86172-115">在 [方案總管] 中，用滑鼠右鍵按一下 [控制器]，然後從內容功能表中選取 [新增] > [控制器]。</span><span class="sxs-lookup"><span data-stu-id="86172-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![將控制器新增至 ASP.NET MVC 應用程式](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="86172-117">在 [Add Scaffold] 對話方塊中，按一下 [MVC 5 Controller - Empty]然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86172-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![指定 MVC 控制器類型](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="86172-119">在 [新增控制器] 對話方塊中，將控制器命名為 QueuesController，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86172-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![命名 MVC 控制器](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="86172-121">將下列 using 指示詞新增至 `QueuesController.cs` 檔案：</span><span class="sxs-lookup"><span data-stu-id="86172-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="86172-122">建立佇列</span><span class="sxs-lookup"><span data-stu-id="86172-122">Create a queue</span></span>

<span data-ttu-id="86172-123">下列步驟說明如何建立佇列：</span><span class="sxs-lookup"><span data-stu-id="86172-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="86172-124">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)的步驟。</span><span class="sxs-lookup"><span data-stu-id="86172-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="86172-125">開啟 `QueuesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="86172-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="86172-126">新增名為 **CreateQueue** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="86172-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="86172-127">在 **CreateQueue** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="86172-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="86172-128">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="86172-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="86172-129">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="86172-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="86172-130">取得代表所需佇列名稱參考的 **CloudQueue** 物件。</span><span class="sxs-lookup"><span data-stu-id="86172-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="86172-131">**CloudQueueClient.GetQueueReference** 方法不會進行對佇列儲存體的要求。</span><span class="sxs-lookup"><span data-stu-id="86172-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="86172-132">無論佇列是否存在都會傳回參考。</span><span class="sxs-lookup"><span data-stu-id="86172-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="86172-133">呼叫 **CloudQueue.CreateIfNotExists** 方法來建立佇列 (如果尚不存在)。</span><span class="sxs-lookup"><span data-stu-id="86172-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="86172-134">如果容器不存在且已成功建立，則 **CloudQueue.CreateIfNotExists** 方法會傳回 **true**。</span><span class="sxs-lookup"><span data-stu-id="86172-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="86172-135">否則，會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="86172-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="86172-136">使用佇列的名稱更新 **ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="86172-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="86172-137">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [佇列]，然後從內容功能表中選取 [新增] > [已連接的服務]。</span><span class="sxs-lookup"><span data-stu-id="86172-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="86172-138">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **CreateQueue**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86172-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="86172-139">開啟 `CreateQueue.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="86172-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="86172-140">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="86172-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="86172-141">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="86172-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="86172-142">執行應用程式，並選取 **Create queue** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="86172-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![建立佇列](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="86172-144">如前所述，僅當容器不存在且已建立時，**CloudQueue.CreateIfNotExists** 方法才會傳回 **true**。</span><span class="sxs-lookup"><span data-stu-id="86172-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="86172-145">因此，如果您在佇列已存在時執行應用程式，此方法會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="86172-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="86172-146">若要多次執行應用程式，您必須先刪除佇列後，才能再次執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="86172-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="86172-147">可以透過完成 **CloudQueue.Delete** 方法來刪除佇列。</span><span class="sxs-lookup"><span data-stu-id="86172-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="86172-148">您也可以使用 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)或 [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)來刪除佇列。</span><span class="sxs-lookup"><span data-stu-id="86172-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="86172-149">將訊息新增至佇列</span><span class="sxs-lookup"><span data-stu-id="86172-149">Add a message to a queue</span></span>

<span data-ttu-id="86172-150">一旦您[建立佇列](#create-a-queue)後，可以將訊息新增至該佇列。</span><span class="sxs-lookup"><span data-stu-id="86172-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="86172-151">本節將引導您完成新增訊息至佇列 test-queue。</span><span class="sxs-lookup"><span data-stu-id="86172-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="86172-152">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)的步驟。</span><span class="sxs-lookup"><span data-stu-id="86172-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="86172-153">開啟 `QueuesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="86172-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="86172-154">新增名為 **AddMessage** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="86172-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="86172-155">在 **AddMessage** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="86172-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="86172-156">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="86172-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="86172-157">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="86172-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="86172-158">取得 **CloudQueueContainer** 物件，代表佇列的參考。</span><span class="sxs-lookup"><span data-stu-id="86172-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="86172-159">建立 **CloudQueueMessage** 物件，代表您想要新增至佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="86172-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="86172-160">您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 物件。</span><span class="sxs-lookup"><span data-stu-id="86172-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="86172-161">呼叫 **CloudQueue.AddMessage** 方法，以將訊息新增至佇列。</span><span class="sxs-lookup"><span data-stu-id="86172-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="86172-162">建立並設定數個 **ViewBag** 在檢視中顯示的屬性。</span><span class="sxs-lookup"><span data-stu-id="86172-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="86172-163">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [佇列]，然後從內容功能表中選取 [新增] > [已連接的服務]。</span><span class="sxs-lookup"><span data-stu-id="86172-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="86172-164">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **AddMessage**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86172-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="86172-165">開啟 `AddMessage.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="86172-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="86172-166">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="86172-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="86172-167">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="86172-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="86172-168">執行應用程式，並選取 **Add message** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="86172-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![新增訊息](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="86172-170">兩個區段 - [讀取佇列中的訊息，但不移除它](#read-a-message-from-a-queue-without-removing-it)和[讀取並移除佇列中的訊息](#read-and-remove-a-message-from-a-queue) - 說明如何從佇列讀取訊息。</span><span class="sxs-lookup"><span data-stu-id="86172-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="86172-171">讀取佇列中的訊息，但不移除它</span><span class="sxs-lookup"><span data-stu-id="86172-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="86172-172">本章節說明如何檢視已排入佇列的訊息 (讀取第一則訊息，但不移除它)。</span><span class="sxs-lookup"><span data-stu-id="86172-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="86172-173">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)的步驟。</span><span class="sxs-lookup"><span data-stu-id="86172-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="86172-174">開啟 `QueuesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="86172-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="86172-175">新增名為 **PeekMessage** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="86172-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="86172-176">在 **PeekMessage** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="86172-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="86172-177">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="86172-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="86172-178">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="86172-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="86172-179">取得 **CloudQueueContainer** 物件，代表佇列的參考。</span><span class="sxs-lookup"><span data-stu-id="86172-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="86172-180">呼叫 **CloudQueue.PeekMessage** 方法，以讀取佇列中的第一則訊息，無需將它從佇列中移除。</span><span class="sxs-lookup"><span data-stu-id="86172-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="86172-181">以下列兩個值更新 **ViewBag**︰佇列名稱和已讀取的訊息。</span><span class="sxs-lookup"><span data-stu-id="86172-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="86172-182">**CloudQueueMessage** 物件會公開取得物件值的兩個屬性：**CloudQueueMessage.AsBytes** 和 **CloudQueueMessage.AsString**。</span><span class="sxs-lookup"><span data-stu-id="86172-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="86172-183">**AsString** (在此範例中使用) 會傳回字串，而 **AsBytes** 會傳回位元組陣列。</span><span class="sxs-lookup"><span data-stu-id="86172-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="86172-184">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [佇列]，然後從內容功能表中選取 [新增] > [已連接的服務]。</span><span class="sxs-lookup"><span data-stu-id="86172-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="86172-185">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **PeekMessage**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86172-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="86172-186">開啟 `PeekMessage.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="86172-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="86172-187">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="86172-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="86172-188">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="86172-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="86172-189">執行應用程式，並選取 **Peek message** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="86172-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![查看訊息](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="86172-191">讀取並移除佇列中的訊息</span><span class="sxs-lookup"><span data-stu-id="86172-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="86172-192">在本節中，您會了解如何從佇列讀取並移除訊息。</span><span class="sxs-lookup"><span data-stu-id="86172-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="86172-193">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)的步驟。</span><span class="sxs-lookup"><span data-stu-id="86172-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="86172-194">開啟 `QueuesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="86172-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="86172-195">新增名為 **ReadMessage** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="86172-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="86172-196">在 **ReadMessage** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="86172-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="86172-197">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="86172-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="86172-198">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="86172-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="86172-199">取得 **CloudQueueContainer** 物件，代表佇列的參考。</span><span class="sxs-lookup"><span data-stu-id="86172-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="86172-200">呼叫 **CloudQueue.AddMessage** 方法，以讀取佇列中的第一則訊息。</span><span class="sxs-lookup"><span data-stu-id="86172-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="86172-201">**CloudQueue.GetMessage** 方法可讓讀取訊息的任何其他程式碼看不見此訊息 30 秒 (預設值)，其他程式碼便無法在您處理此訊息時進行修改或刪除。</span><span class="sxs-lookup"><span data-stu-id="86172-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="86172-202">若要變更看不見訊息的時間量，請修改傳遞至 **CloudQueue.GetMessage** 方法的 **visibilityTimeout** 參數。</span><span class="sxs-lookup"><span data-stu-id="86172-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="86172-203">呼叫 **CloudQueueMessage.Delete** 方法，以刪除佇列中的訊息。</span><span class="sxs-lookup"><span data-stu-id="86172-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="86172-204">使用刪除的訊息以及佇列的名稱更新 **ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="86172-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="86172-205">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [佇列]，然後從內容功能表中選取 [新增] > [已連接的服務]。</span><span class="sxs-lookup"><span data-stu-id="86172-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="86172-206">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **ReadMessage**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86172-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="86172-207">開啟 `ReadMessage.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="86172-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="86172-208">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="86172-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="86172-209">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="86172-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="86172-210">執行應用程式，並選取 **Read/Delete message** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="86172-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![讀取和刪除訊息](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="86172-212">取得佇列長度</span><span class="sxs-lookup"><span data-stu-id="86172-212">Get the queue length</span></span>

<span data-ttu-id="86172-213">本節說明如何取得佇列長度 (訊息數目)。</span><span class="sxs-lookup"><span data-stu-id="86172-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="86172-214">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)的步驟。</span><span class="sxs-lookup"><span data-stu-id="86172-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="86172-215">開啟 `QueuesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="86172-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="86172-216">新增名為 **GetQueueLength** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="86172-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="86172-217">在 **ReadMessage** 方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="86172-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="86172-218">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="86172-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="86172-219">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="86172-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="86172-220">取得 **CloudQueueContainer** 物件，代表佇列的參考。</span><span class="sxs-lookup"><span data-stu-id="86172-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="86172-221">呼叫 **CloudQueue.FetchAttributes** 方法來擷取佇列的屬性 (包括其長度)。</span><span class="sxs-lookup"><span data-stu-id="86172-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="86172-222">存取 **CloudQueue.ApproximateMessageCount** 屬性，以取得佇列的長度。</span><span class="sxs-lookup"><span data-stu-id="86172-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="86172-223">使用佇列的名稱及其長度更新 **ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="86172-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="86172-224">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [佇列]，然後從內容功能表中選取 [新增] > [已連接的服務]。</span><span class="sxs-lookup"><span data-stu-id="86172-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="86172-225">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **GetQueueLength**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86172-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="86172-226">開啟 `GetQueueLengthMessage.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="86172-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="86172-227">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="86172-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="86172-228">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="86172-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="86172-229">執行應用程式，並選取 **Get queue length** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="86172-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![取得佇列長度](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="86172-231">刪除佇列</span><span class="sxs-lookup"><span data-stu-id="86172-231">Delete a queue</span></span>
<span data-ttu-id="86172-232">本節說明如何刪除佇列。</span><span class="sxs-lookup"><span data-stu-id="86172-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="86172-233">本章節假設您已完成[設定開發環境](#set-up-the-development-environment)的步驟。</span><span class="sxs-lookup"><span data-stu-id="86172-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="86172-234">開啟 `QueuesController.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="86172-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="86172-235">新增名為 **DeleteQueue** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="86172-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="86172-236">在 **DeleteQueue**方法內，取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="86172-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="86172-237">使用下列程式碼從 Azure 服務組態中取得儲存體連接字串和儲存體帳戶資訊：(將 &lt;storage-account-name> 變更為您要存取之 Azure 儲存體帳戶的名稱。)</span><span class="sxs-lookup"><span data-stu-id="86172-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="86172-238">取得代表佇列服務用戶端的 **CloudQueueClient** 物件。</span><span class="sxs-lookup"><span data-stu-id="86172-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="86172-239">取得 **CloudQueueContainer** 物件，代表佇列的參考。</span><span class="sxs-lookup"><span data-stu-id="86172-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="86172-240">呼叫 **CloudQueueMessage.Delete** 方法，以刪除 **CloudQueue** 物件所代表的佇列。</span><span class="sxs-lookup"><span data-stu-id="86172-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="86172-241">使用佇列的名稱及其長度更新 **ViewBag**。</span><span class="sxs-lookup"><span data-stu-id="86172-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="86172-242">在 [方案總管] 中，展開 [檢視] 資料夾、用滑鼠右鍵按一下 [佇列]，然後從內容功能表中選取 [新增] > [已連接的服務]。</span><span class="sxs-lookup"><span data-stu-id="86172-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="86172-243">在 [新增檢視] 對話方塊中，針對檢視名稱輸入 **DeleteQueue**，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="86172-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="86172-244">開啟 `DeleteQueue.cshtml` 並加以修改，以便其如下列程式碼片段所示：</span><span class="sxs-lookup"><span data-stu-id="86172-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="86172-245">在 [方案總管] 中，展開 **檢視-> 共用** 資料夾，然後開啟 `_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="86172-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="86172-246">在最後一個 **Html.ActionLink** 之後，新增下列 **Html.ActionLink**：</span><span class="sxs-lookup"><span data-stu-id="86172-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="86172-247">執行應用程式，並選取 **Get queue length** 來查看類似下列螢幕擷取畫面的結果︰</span><span class="sxs-lookup"><span data-stu-id="86172-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![刪除佇列](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="86172-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86172-249">Next steps</span></span>
<span data-ttu-id="86172-250">如需了解 Azure 中的其他資料儲存選項，請檢視更多功能指南。</span><span class="sxs-lookup"><span data-stu-id="86172-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="86172-251">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="86172-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="86172-252">開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="86172-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
