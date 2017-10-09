---
title: "aaaGet 開始使用 Azure blob 儲存體和 Visual Studio 已連接服務 (ASP.NET) |Microsoft 文件"
description: "Tooget 啟動連接 tooa 使用 Visual Studio 已連接服務的儲存體帳戶之後，Visual Studio 中 ASP.NET 專案中使用 Azure blob 儲存體的方式"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: eb38889f239a63852d6928e8be10c3d3f1746e9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>概觀

Azure blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。 Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。 Blob 儲存體也是參考的 tooas 物件儲存體。

本教學課程會示範 toowrite ASP.NET 為使用 Azure blob 儲存體的一些常見案例的程式碼。 案例包括建立 blob 容器，以及上傳、列出、下載和刪除 blob。

##<a name="prerequisites"></a>必要條件

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Azure 儲存體帳戶](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>建立 MVC 控制器 

1. 在 hello**方案總管 中**，以滑鼠右鍵按一下**控制站**，並從 hello 內容功能表中，選取**加入控制器->** 。

    ![加入控制器 tooan ASP.NET MVC 應用程式](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. 在 hello**新增 Scaffold**對話方塊中，選取**MVC 5 控制器空白**，然後選取**新增**。

    ![指定 MVC 控制器類型](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. 在 hello**加入控制器**對話方塊中，名稱 hello 控制器*BlobsController*，並選取**新增**。

    ![名稱 hello MVC 控制器](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. 新增下列 hello*使用*指示詞 toohello`BlobsController.cs`檔案：

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>建立 Blob 容器

Blob 容器是 blob 和資料夾的巢狀階層。 hello 下列步驟說明如何 toocreate blob 容器：

> [!NOTE]
> 
> hello 本節中的程式碼假設您已經完成 hello 區段中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`BlobsController.cs`檔案。

1. 新增名為 **CreateBlobContainer** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. 在 hello **CreateBlobContainer**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello hello Azure 服務組態中的下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊。 (變更*&lt;儲存體帳戶名稱 >* toohello hello 正在存取的 Azure 儲存體帳戶名稱。)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 取得**CloudBlobContainer**物件，表示參考 toohello 所需的 blob 容器名稱。 hello **CloudBlobClient.GetContainerReference**方法不會針對 blob 儲存體的要求。 不論是否 hello blob 容器存在，則會傳回 hello 參考。 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. 呼叫 hello **CloudBlobContainer.CreateIfNotExists**方法 toocreate hello 容器如果尚不存在。 hello **CloudBlobContainer.CreateIfNotExists**方法會傳回**true**如果 hello 容器不存在，而且已成功建立。 否則，會傳回 **false**。    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. 更新 hello **ViewBag** hello hello blob 容器名稱。

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**Blob**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**CreateBlobContainer** hello 檢視名稱，然後選取**新增**。

1. 開啟`CreateBlobContainer.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. 執行 hello 應用程式，並選取**建立 Blob 容器**toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![建立 Blob 容器](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    如先前所述，hello **CloudBlobContainer.CreateIfNotExists**方法會傳回**true**只當 hello 容器不存在，而且會建立。 因此，如果 hello 容器存在時，您可以執行 hello 應用程式，hello 方法會傳回**false**。 toorun hello 應用程式多次，必須刪除 hello 容器，才能再次執行 hello 應用程式。 正在刪除 hello 容器可透過 hello **CloudBlobContainer.Delete**方法。 您也可以刪除使用 hello hello 容器[Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)或 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。  

## <a name="upload-a-blob-into-a-blob-container"></a>將 Blob 上傳至 blob 容器

一旦您[建立 blob 容器](#create-a-blob-container)後，可以將檔案上傳至該容器。 本節將引導您透過上傳本機檔案 tooa blob 容器。 hello 步驟假設您已建立名為的 blob 容器*測試 blob 容器*。 

> [!NOTE]
> 
> hello 本節中的程式碼假設您已經完成 hello 區段中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`BlobsController.cs`檔案。

1. 新增名為 **UploadBlob** 的方法，其會傳回 **EmptyResult**。

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. 在 hello **UploadBlob**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 取得**CloudBlobContainer**物件，代表參考 toohello blob 容器名稱。 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. 如稍早所述，Azure 儲存體支援不同的 blob 類型。 tooretrieve 參考 tooa 分頁 blob 呼叫 hello **CloudBlobContainer.GetPageBlobReference**方法。 tooretrieve 參考 tooa 區塊 blob，呼叫 hello **CloudBlobContainer.GetBlockBlobReference**方法。 通常，區塊 blob 是建議的型別 toouse hello。 (變更 < blob 名稱 > * toohello 您想要一次上傳 toogive hello blob 的名稱。)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Blob 參考之後，您可以上傳任何資料流 tooit 呼叫 hello blob 參考物件的**UploadFromStream**方法。 hello **UploadFromStream**方法會建立 hello blob 不存在，或如果存在的話，覆寫它。 (變更*&lt;檔案上傳至 >* tooa 完整路徑 toohello 檔案想 tooupload。)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**Blob**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. 執行 hello 應用程式，並選取**上傳 blob**。  
  
hello 節-[列出 blob 容器中的 hello blob](#list-the-blobs-in-a-blob-container) -說明 toolist hello blob 容器中的 blob。  

## <a name="list-hello-blobs-in-a-blob-container"></a>列出 hello blob 的 blob 容器中

本節說明 toolist hello blob 容器中的 blob。 hello 範例程式碼參考 hello*測試 blob 容器*hello 區段中建立[建立 blob 容器](#create-a-blob-container)。

> [!NOTE]
> 
> hello 本節中的程式碼假設您已經完成 hello 區段中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`BlobsController.cs`檔案。

1. 新增名為 **ListBlobs** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. 在 hello **ListBlobs**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 取得**CloudBlobContainer**物件，代表參考 toohello blob 容器名稱。 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. toolist hello blob，在 blob 容器中，使用 hello **CloudBlobContainer.ListBlobs**方法。 hello **CloudBlobContainer.ListBlobs**方法會傳回**IListBlobItem**物件轉型 tooa **CloudBlockBlob**， **CloudPageBlob**，或**CloudBlobDirectory**物件。 hello 下列程式碼片段列舉 blob 容器中的所有 hello blob。 每個 blob 是根據其類型，以及其名稱的型別轉換 toohello 適當物件 (或 URI 中的 hello 案例**CloudBlobDirectory**) 加入 tooa 清單。

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    在加法 tooblobs blob 容器可以包含的目錄。 讓我們假設您有稱為的 blob 容器*測試 blob 容器*以 hello 下列階層：

        foo.png
        dir1/bar.png
        dir2/baz.png

    使用上述程式碼範例的 hello，hello **blob**字串清單會包含類似 toohello 下列值：

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    如您所見，hello 清單僅包含 hello 最上層實體;不 hello 巢狀的 (*bar.png*和*baz.png*)。 toolist 所有 hello blob 容器內的實體，您必須呼叫 hello **CloudBlobContainer.ListBlobs**方法並傳入**true** hello **useFlatBlobListing**參數。    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    設定 hello **useFlatBlobListing**參數太**true**在 hello blob 容器中，會傳回所有實體的一般清單，並產生下列結果 hello:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. 在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**Blob**，hello 內容功能表中選取**新增-> 檢視**.

1. 在 [hello**加入檢視**] 對話方塊中，輸入**ListBlobs** hello 檢視名稱，然後選取**新增**。

1. 開啟`ListBlobs.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. 執行 hello 應用程式，並選取**列出 blob** toosee 結果類似 toohello 下列螢幕擷取畫面：
  
    ![blob 列表](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>下載 Blob

本節說明如何 toodownload blob，然後將它保存 toolocal 儲存體或讀取 hello 內容轉換為字串。 hello 範例程式碼參考 hello*測試 blob 容器*hello 區段中建立[建立 blob 容器](#create-a-blob-container)。

1. 開啟 hello`BlobsController.cs`檔案。

1. 新增名為 **DownloadBlob** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. 在 hello **DownloadBlob**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 取得**CloudBlobContainer**物件，代表參考 toohello blob 容器名稱。 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. 藉由呼叫 **CloudBlobContainer.GetBlockBlobReference** 或 **CloudBlobContainer.GetPageBlobReference** 方法取得 blob 參考物件。 (變更 *&lt;blob 名稱 >* toohello 您下載的 hello blob 名稱。)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload blob，使用 hello **CloudBlockBlob.DownloadToStream**或**CloudPageBlob.DownloadToStream**方法，取決於 hello blob 類型。 hello 下列程式碼片段會使用 hello **CloudBlockBlob.DownloadToStream** blob 的內容 tooa 資料流物件的方法 tootransfer 然後保存 tooa 本機檔案: (變更*&lt;本機檔案名稱>* toohello 完整檔案名稱代表您想要下載的 hello blob。) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. 執行 hello 應用程式，並選取**下載 blob** toodownload hello blob。 指定在 hello 的 hello blob **CloudBlobContainer.GetBlockBlobReference**方法呼叫會下載您指定在 hello toohello 位置**File.OpenWrite**方法呼叫。 

## <a name="delete-blobs"></a>刪除 Blob

hello 下列步驟說明如何 toodelete blob:

> [!NOTE]
> 
> hello 本節中的程式碼假設您已經完成 hello 區段中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。 

1. 開啟 hello`BlobsController.cs`檔案。

1. 新增名為 **DeleteBlob** 的方法，其會傳回 **ActionResult**。

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. 取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。 使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. 取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 取得**CloudBlobContainer**物件，代表參考 toohello blob 容器名稱。 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. 藉由呼叫 **CloudBlobContainer.GetBlockBlobReference** 或 **CloudBlobContainer.GetPageBlobReference** 方法取得 blob 參考物件。 (變更 *&lt;blob 名稱 >* toohello 您要刪除的 hello blob 名稱。)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. 在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。

1. 之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. 執行 hello 應用程式，並選取**刪除 blob** toodelete hello blob 中 hello 指定**CloudBlobContainer.GetBlockBlobReference**方法呼叫。 

## <a name="next-steps"></a>後續步驟
檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。

  * [開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
  * [開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET)](./vs-storage-aspnet-getting-started-queues.md)
