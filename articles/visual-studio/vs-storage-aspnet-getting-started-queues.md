---
title: "aaaGet 開始使用 Azure 佇列儲存體和 Visual Studio 已連接服務 (ASP.NET) |Microsoft 文件"
description: "Tooget 啟動連接 tooa 使用 Visual Studio 已連接服務的儲存體帳戶之後，Visual Studio 中 ASP.NET 專案中使用 Azure 佇列儲存體的方式"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 415a437c4ce60b1e2e328f8e937c73b0d5c50e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>概觀

Azure 佇列儲存體可提供應用程式元件之間的雲端傳訊。 設計擴充性的應用程式時，會經常分離應用程式元件，以便進行個別擴充。 佇列儲存體提供非同步傳訊應用程式元件之間的通訊是否在 hello 雲端中，在 hello 桌面上、 在內部部署伺服器上，或行動裝置上執行。 佇列儲存體也支援管理非同步工作並建置處理工作流程。

本教學課程會示範 toowrite ASP.NET 為使用 Azure 佇列儲存體實體一些常見案例的程式碼。 這些案例包括一般工作，例如建立 Azure 佇列，以及新增、修改、讀取和移除佇列訊息。

##<a name="prerequisites"></a>必要條件

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>建立 MVC 控制器 

1. 在 hello**方案總管 中**，以滑鼠右鍵按一下**控制站**，並從 hello 內容功能表中，選取**加入控制器->** 。

    ![加入控制器 tooan ASP.NET MVC 應用程式](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. 在 hello**新增 Scaffold**對話方塊中，選取**MVC 5 控制器空白**，然後選取**新增**。

    ![指定 MVC 控制器類型](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. 在 hello**加入控制器**對話方塊中，名稱 hello 控制器*QueuesController*，並選取**新增**。

    ![名稱 hello MVC 控制器](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. 新增下列 hello*使用*指示詞 toohello`QueuesController.cs`檔案：

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>建立佇列

hello 下列步驟說明如何 toocreate 佇列：

> [!NOTE]
> 
> 本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`QueuesController.cs`檔案。 

1. 新增名為 **CreateQueue** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. 在 hello **CreateQueue**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. 取得代表佇列服務用戶端的 **CloudQueueClient** 物件。
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. 取得**CloudQueue**物件，表示參考 toohello 所需的佇列名稱。 hello **CloudQueueClient.GetQueueReference**方法不會對佇列儲存體的要求。 不論是否 hello 佇列存在，則會傳回 hello 參考。 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. 呼叫 hello **CloudQueue.CreateIfNotExists**方法 toocreate hello 佇列如果尚不存在。 hello **CloudQueue.CreateIfNotExists**方法會傳回**true**如果 hello 佇列不存在，而且已成功建立。 否則，會傳回 **false**。    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. 更新 hello **ViewBag** hello hello 佇列名稱。

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**CreateQueue** hello 檢視名稱，然後選取**新增**。

1. 開啟`CreateQueue.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. 執行 hello 應用程式，並選取**建立佇列**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![建立佇列](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    如先前所述，hello **CloudQueue.CreateIfNotExists**方法會傳回**true**只當 hello 佇列不存在，而且會建立。 因此，如果 hello 佇列存在時，您可以執行 hello 應用程式，hello 方法會傳回**false**。 toorun hello 應用程式多次，必須刪除 hello 佇列，才能再次執行 hello 應用程式。 正在刪除 hello 佇列可透過 hello **CloudQueue.Delete**方法。 您也可以刪除使用 hello hello 佇列[Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)或 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。  

## <a name="add-a-message-tooa-queue"></a>新增訊息 tooa 佇列

一旦您[建立佇列](#create-a-queue)，您可以新增訊息 toothat 佇列。 本節將引導您完成新增訊息 tooa 佇列*測試佇列*。 

> [!NOTE]
> 
> 本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`QueuesController.cs`檔案。

1. 新增名為 **AddMessage** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. 在 hello **AddMessage**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得代表佇列服務用戶端的 **CloudQueueClient** 物件。
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 取得**CloudQueueContainer**物件，代表參考 toohello 佇列。 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. 建立 hello **CloudQueueMessage**物件，代表您想要 tooadd toohello 佇列 hello 訊息。 您可以從字串 (採用 UTF-8 格式) 或位元組陣列建立 **CloudQueueMessage** 物件。

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. 呼叫 hello **CloudQueue.AddMessage**方法 tooadd hello 依現狀 toohello 佇列。

    ```csharp
    queue.AddMessage(message);
    ```

1. 建立並設定幾個**ViewBag** hello 檢視中顯示的屬性。

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**AddMessage** hello 檢視名稱，然後選取**新增**。

1. 開啟`AddMessage.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. 執行 hello 應用程式，並選取**新增訊息**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![新增訊息](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

hello 兩個區段-[從佇列讀取訊息，而不移除它](#read-a-message-from-a-queue-without-removing-it)和[讀取並將訊息從佇列移除](#read-and-remove-a-message-from-a-queue)-說明如何 tooread 訊息從佇列中。  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>讀取佇列中的訊息，但不移除它

本節說明如何 toopeek 排入佇列的訊息 （hello 讀取第一則訊息而不移除它）。  

> [!NOTE]
> 
> 本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`QueuesController.cs`檔案。

1. 新增名為 **PeekMessage** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. 在 hello **PeekMessage**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得代表佇列服務用戶端的 **CloudQueueClient** 物件。
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 取得**CloudQueueContainer**物件，代表參考 toohello 佇列。 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. 呼叫 hello **CloudQueue.PeekMessage** hello 佇列，而不需移除 hello 佇列中的方法 tooread hello 第一個訊息。 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. 更新 hello **ViewBag**具有兩個值： hello 佇列名稱 」 和 「 已讀取的 hello 訊息。 hello **CloudQueueMessage**物件會公開兩個屬性來取得 hello 物件的值： **CloudQueueMessage.AsBytes**和**CloudQueueMessage.AsString**。 **AsString** (在此範例中使用) 會傳回字串，而 **AsBytes** 會傳回位元組陣列。

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**PeekMessage** hello 檢視名稱，然後選取**新增**。

1. 開啟`PeekMessage.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

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

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. 執行 hello 應用程式，並選取**窺視訊息**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![查看訊息](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>讀取並移除佇列中的訊息

在本節中，您學會如何 tooread 並從佇列移除訊息。   

> [!NOTE]
> 
> 本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`QueuesController.cs`檔案。

1. 新增名為 **ReadMessage** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. 在 hello **ReadMessage**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得代表佇列服務用戶端的 **CloudQueueClient** 物件。
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 取得**CloudQueueContainer**物件，代表參考 toohello 佇列。 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. 呼叫 hello **CloudQueue.GetMessage** hello 佇列中的方法 tooread hello 第一個訊息。 hello **CloudQueue.GetMessage**方法讓 hello 訊息顯示為 30 秒 （依預設） tooany 讀取訊息，讓其他程式碼可以修改或刪除 hello 訊息，您在處理時它的其他程式碼。 toochange hello 數量時間 hello 訊息是不可見，請修改 hello **visibilityTimeout**參數傳入 toohello **CloudQueue.GetMessage**方法。

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. 呼叫 hello **CloudQueueMessage.Delete**方法 toodelete hello 訊息從 hello 佇列。

    ```csharp
    queue.DeleteMessage(message);
    ```

1. 更新 hello **ViewBag**以 hello 訊息刪除，而且 hello hello 佇列的名稱。

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**ReadMessage** hello 檢視名稱，然後選取**新增**。

1. 開啟`ReadMessage.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

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

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. 執行 hello 應用程式，並選取**讀取/刪除訊息**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![讀取和刪除訊息](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>取得 hello 佇列長度

本節說明如何 tooget hello 佇列長度 （訊息數目）。 

> [!NOTE]
> 
> 本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`QueuesController.cs`檔案。

1. 新增名為 **GetQueueLength** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. 在 hello **ReadMessage**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得代表佇列服務用戶端的 **CloudQueueClient** 物件。
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 取得**CloudQueueContainer**物件，代表參考 toohello 佇列。 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. 呼叫 hello **CloudQueue.FetchAttributes**方法 tooretrieve hello 佇列的屬性 （包括它的長度）。 

    ```csharp
    queue.FetchAttributes();
    ```

6. 存取 hello **CloudQueue.ApproximateMessageCount**屬性 tooget hello 佇列的長度。
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. 更新 hello **ViewBag**具有 hello 名稱 hello 佇列和它的長度。

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**GetQueueLength** hello 檢視名稱，然後選取**新增**。

1. 開啟`GetQueueLengthMessage.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. 執行 hello 應用程式，並選取**取得佇列長度**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![取得佇列長度](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>刪除佇列
本節說明如何 toodelete 佇列。 

> [!NOTE]
> 
> 本節假設您已經完成 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`QueuesController.cs`檔案。

1. 新增名為 **DeleteQueue** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. 在 hello **deletequeue 等**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得代表佇列服務用戶端的 **CloudQueueClient** 物件。
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. 取得**CloudQueueContainer**物件，代表參考 toohello 佇列。 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. 呼叫 hello **CloudQueue.Delete**方法 toodelete hello 佇列由 hello **CloudQueue**物件。

    ```csharp
    queue.Delete();
    ```

1. 更新 hello **ViewBag**具有 hello 名稱 hello 佇列和它的長度。

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**佇列**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**deletequeue 等**hello 檢視名稱，然後選取**新增**。

1. 開啟`DeleteQueue.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. 執行 hello 應用程式，並選取**取得佇列長度**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![刪除佇列](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>後續步驟
檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。

  * [開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
