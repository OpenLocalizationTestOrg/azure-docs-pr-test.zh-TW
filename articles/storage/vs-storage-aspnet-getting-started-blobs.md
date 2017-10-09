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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="a0321-103">開始使用 Azure Blob 儲存體和 Visual Studio 已連接服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="a0321-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a0321-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a0321-104">Overview</span></span>

<span data-ttu-id="a0321-105">Azure blob 儲存體是 hello 雲端中儲存非結構化的資料，做為物件/blob 服務。</span><span class="sxs-lookup"><span data-stu-id="a0321-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="a0321-106">Blob 儲存體可以儲存任何類型的文字或二進位資料，例如文件、媒體檔案或應用程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a0321-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="a0321-107">Blob 儲存體也是參考的 tooas 物件儲存體。</span><span class="sxs-lookup"><span data-stu-id="a0321-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="a0321-108">本教學課程會示範 toowrite ASP.NET 為使用 Azure blob 儲存體的一些常見案例的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a0321-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="a0321-109">案例包括建立 blob 容器，以及上傳、列出、下載和刪除 blob。</span><span class="sxs-lookup"><span data-stu-id="a0321-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="a0321-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a0321-110">Prerequisites</span></span>

* [<span data-ttu-id="a0321-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0321-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="a0321-112">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a0321-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="a0321-113">建立 MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="a0321-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="a0321-114">在 hello**方案總管 中**，以滑鼠右鍵按一下**控制站**，並從 hello 內容功能表中，選取**加入控制器->** 。</span><span class="sxs-lookup"><span data-stu-id="a0321-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![加入控制器 tooan ASP.NET MVC 應用程式](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="a0321-116">在 hello**新增 Scaffold**對話方塊中，選取**MVC 5 控制器空白**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="a0321-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![指定 MVC 控制器類型](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="a0321-118">在 hello**加入控制器**對話方塊中，名稱 hello 控制器*BlobsController*，並選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="a0321-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![名稱 hello MVC 控制器](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="a0321-120">新增下列 hello*使用*指示詞 toohello`BlobsController.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="a0321-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="a0321-121">建立 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="a0321-121">Create a blob container</span></span>

<span data-ttu-id="a0321-122">Blob 容器是 blob 和資料夾的巢狀階層。</span><span class="sxs-lookup"><span data-stu-id="a0321-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="a0321-123">hello 下列步驟說明如何 toocreate blob 容器：</span><span class="sxs-lookup"><span data-stu-id="a0321-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a0321-124">hello 本節中的程式碼假設您已經完成 hello 區段中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="a0321-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="a0321-125">開啟 hello`BlobsController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="a0321-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="a0321-126">新增名為 **CreateBlobContainer** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="a0321-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="a0321-127">在 hello **CreateBlobContainer**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="a0321-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a0321-128">使用 hello hello Azure 服務組態中的下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="a0321-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="a0321-129">(變更*&lt;儲存體帳戶名稱 >* toohello hello 正在存取的 Azure 儲存體帳戶名稱。)</span><span class="sxs-lookup"><span data-stu-id="a0321-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="a0321-130">取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="a0321-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="a0321-131">取得**CloudBlobContainer**物件，表示參考 toohello 所需的 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="a0321-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="a0321-132">hello **CloudBlobClient.GetContainerReference**方法不會針對 blob 儲存體的要求。</span><span class="sxs-lookup"><span data-stu-id="a0321-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="a0321-133">不論是否 hello blob 容器存在，則會傳回 hello 參考。</span><span class="sxs-lookup"><span data-stu-id="a0321-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="a0321-134">呼叫 hello **CloudBlobContainer.CreateIfNotExists**方法 toocreate hello 容器如果尚不存在。</span><span class="sxs-lookup"><span data-stu-id="a0321-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="a0321-135">hello **CloudBlobContainer.CreateIfNotExists**方法會傳回**true**如果 hello 容器不存在，而且已成功建立。</span><span class="sxs-lookup"><span data-stu-id="a0321-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="a0321-136">否則，會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="a0321-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="a0321-137">更新 hello **ViewBag** hello hello blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="a0321-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="a0321-138">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**Blob**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="a0321-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a0321-139">在 [hello**加入檢視**] 對話方塊中，輸入**CreateBlobContainer** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="a0321-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="a0321-140">開啟`CreateBlobContainer.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0321-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="a0321-141">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="a0321-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a0321-142">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a0321-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="a0321-143">執行 hello 應用程式，並選取**建立 Blob 容器**toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="a0321-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![建立 Blob 容器](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="a0321-145">如先前所述，hello **CloudBlobContainer.CreateIfNotExists**方法會傳回**true**只當 hello 容器不存在，而且會建立。</span><span class="sxs-lookup"><span data-stu-id="a0321-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="a0321-146">因此，如果 hello 容器存在時，您可以執行 hello 應用程式，hello 方法會傳回**false**。</span><span class="sxs-lookup"><span data-stu-id="a0321-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="a0321-147">toorun hello 應用程式多次，必須刪除 hello 容器，才能再次執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0321-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="a0321-148">正在刪除 hello 容器可透過 hello **CloudBlobContainer.Delete**方法。</span><span class="sxs-lookup"><span data-stu-id="a0321-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="a0321-149">您也可以刪除使用 hello hello 容器[Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)或 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="a0321-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="a0321-150">將 Blob 上傳至 blob 容器</span><span class="sxs-lookup"><span data-stu-id="a0321-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="a0321-151">一旦您[建立 blob 容器](#create-a-blob-container)後，可以將檔案上傳至該容器。</span><span class="sxs-lookup"><span data-stu-id="a0321-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="a0321-152">本節將引導您透過上傳本機檔案 tooa blob 容器。</span><span class="sxs-lookup"><span data-stu-id="a0321-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="a0321-153">hello 步驟假設您已建立名為的 blob 容器*測試 blob 容器*。</span><span class="sxs-lookup"><span data-stu-id="a0321-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="a0321-154">hello 本節中的程式碼假設您已經完成 hello 區段中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="a0321-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="a0321-155">開啟 hello`BlobsController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="a0321-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="a0321-156">新增名為 **UploadBlob** 的方法，其會傳回 **EmptyResult**。</span><span class="sxs-lookup"><span data-stu-id="a0321-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="a0321-157">在 hello **UploadBlob**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="a0321-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a0321-158">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="a0321-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="a0321-159">取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="a0321-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="a0321-160">取得**CloudBlobContainer**物件，代表參考 toohello blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="a0321-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="a0321-161">如稍早所述，Azure 儲存體支援不同的 blob 類型。</span><span class="sxs-lookup"><span data-stu-id="a0321-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="a0321-162">tooretrieve 參考 tooa 分頁 blob 呼叫 hello **CloudBlobContainer.GetPageBlobReference**方法。</span><span class="sxs-lookup"><span data-stu-id="a0321-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="a0321-163">tooretrieve 參考 tooa 區塊 blob，呼叫 hello **CloudBlobContainer.GetBlockBlobReference**方法。</span><span class="sxs-lookup"><span data-stu-id="a0321-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="a0321-164">通常，區塊 blob 是建議的型別 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="a0321-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="a0321-165">(變更 < blob 名稱 > * toohello 您想要一次上傳 toogive hello blob 的名稱。)</span><span class="sxs-lookup"><span data-stu-id="a0321-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="a0321-166">Blob 參考之後，您可以上傳任何資料流 tooit 呼叫 hello blob 參考物件的**UploadFromStream**方法。</span><span class="sxs-lookup"><span data-stu-id="a0321-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="a0321-167">hello **UploadFromStream**方法會建立 hello blob 不存在，或如果存在的話，覆寫它。</span><span class="sxs-lookup"><span data-stu-id="a0321-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="a0321-168">(變更*&lt;檔案上傳至 >* tooa 完整路徑 toohello 檔案想 tooupload。)</span><span class="sxs-lookup"><span data-stu-id="a0321-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="a0321-169">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**Blob**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="a0321-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a0321-170">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="a0321-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a0321-171">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a0321-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="a0321-172">執行 hello 應用程式，並選取**上傳 blob**。</span><span class="sxs-lookup"><span data-stu-id="a0321-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="a0321-173">hello 節-[列出 blob 容器中的 hello blob](#list-the-blobs-in-a-blob-container) -說明 toolist hello blob 容器中的 blob。</span><span class="sxs-lookup"><span data-stu-id="a0321-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="a0321-174">列出 hello blob 的 blob 容器中</span><span class="sxs-lookup"><span data-stu-id="a0321-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="a0321-175">本節說明 toolist hello blob 容器中的 blob。</span><span class="sxs-lookup"><span data-stu-id="a0321-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="a0321-176">hello 範例程式碼參考 hello*測試 blob 容器*hello 區段中建立[建立 blob 容器](#create-a-blob-container)。</span><span class="sxs-lookup"><span data-stu-id="a0321-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a0321-177">hello 本節中的程式碼假設您已經完成 hello 區段中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="a0321-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="a0321-178">開啟 hello`BlobsController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="a0321-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="a0321-179">新增名為 **ListBlobs** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="a0321-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="a0321-180">在 hello **ListBlobs**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="a0321-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a0321-181">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="a0321-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="a0321-182">取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="a0321-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="a0321-183">取得**CloudBlobContainer**物件，代表參考 toohello blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="a0321-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="a0321-184">toolist hello blob，在 blob 容器中，使用 hello **CloudBlobContainer.ListBlobs**方法。</span><span class="sxs-lookup"><span data-stu-id="a0321-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="a0321-185">hello **CloudBlobContainer.ListBlobs**方法會傳回**IListBlobItem**物件轉型 tooa **CloudBlockBlob**， **CloudPageBlob**，或**CloudBlobDirectory**物件。</span><span class="sxs-lookup"><span data-stu-id="a0321-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="a0321-186">hello 下列程式碼片段列舉 blob 容器中的所有 hello blob。</span><span class="sxs-lookup"><span data-stu-id="a0321-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="a0321-187">每個 blob 是根據其類型，以及其名稱的型別轉換 toohello 適當物件 (或 URI 中的 hello 案例**CloudBlobDirectory**) 加入 tooa 清單。</span><span class="sxs-lookup"><span data-stu-id="a0321-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

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

    <span data-ttu-id="a0321-188">在加法 tooblobs blob 容器可以包含的目錄。</span><span class="sxs-lookup"><span data-stu-id="a0321-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="a0321-189">讓我們假設您有稱為的 blob 容器*測試 blob 容器*以 hello 下列階層：</span><span class="sxs-lookup"><span data-stu-id="a0321-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="a0321-190">使用上述程式碼範例的 hello，hello **blob**字串清單會包含類似 toohello 下列值：</span><span class="sxs-lookup"><span data-stu-id="a0321-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="a0321-191">如您所見，hello 清單僅包含 hello 最上層實體;不 hello 巢狀的 (*bar.png*和*baz.png*)。</span><span class="sxs-lookup"><span data-stu-id="a0321-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="a0321-192">toolist 所有 hello blob 容器內的實體，您必須呼叫 hello **CloudBlobContainer.ListBlobs**方法並傳入**true** hello **useFlatBlobListing**參數。</span><span class="sxs-lookup"><span data-stu-id="a0321-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="a0321-193">設定 hello **useFlatBlobListing**參數太**true**在 hello blob 容器中，會傳回所有實體的一般清單，並產生下列結果 hello:</span><span class="sxs-lookup"><span data-stu-id="a0321-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="a0321-194">在 hello**方案總管 中**，展開 hello**檢視**資料夾中，以滑鼠右鍵按一下**Blob**，hello 內容功能表中選取**新增-> 檢視**.</span><span class="sxs-lookup"><span data-stu-id="a0321-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="a0321-195">在 [hello**加入檢視**] 對話方塊中，輸入**ListBlobs** hello 檢視名稱，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="a0321-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="a0321-196">開啟`ListBlobs.cshtml`，並修改它，讓它看起來像下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="a0321-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="a0321-197">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="a0321-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a0321-198">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a0321-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="a0321-199">執行 hello 應用程式，並選取**列出 blob** toosee 結果類似 toohello 下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="a0321-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![blob 列表](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="a0321-201">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="a0321-201">Download blobs</span></span>

<span data-ttu-id="a0321-202">本節說明如何 toodownload blob，然後將它保存 toolocal 儲存體或讀取 hello 內容轉換為字串。</span><span class="sxs-lookup"><span data-stu-id="a0321-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="a0321-203">hello 範例程式碼參考 hello*測試 blob 容器*hello 區段中建立[建立 blob 容器](#create-a-blob-container)。</span><span class="sxs-lookup"><span data-stu-id="a0321-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="a0321-204">開啟 hello`BlobsController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="a0321-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="a0321-205">新增名為 **DownloadBlob** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="a0321-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="a0321-206">在 hello **DownloadBlob**方法，取得**CloudStorageAccount**物件，表示您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="a0321-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a0321-207">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="a0321-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="a0321-208">取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="a0321-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="a0321-209">取得**CloudBlobContainer**物件，代表參考 toohello blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="a0321-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="a0321-210">藉由呼叫 **CloudBlobContainer.GetBlockBlobReference** 或 **CloudBlobContainer.GetPageBlobReference** 方法取得 blob 參考物件。</span><span class="sxs-lookup"><span data-stu-id="a0321-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="a0321-211">(變更 *&lt;blob 名稱 >* toohello 您下載的 hello blob 名稱。)</span><span class="sxs-lookup"><span data-stu-id="a0321-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="a0321-212">toodownload blob，使用 hello **CloudBlockBlob.DownloadToStream**或**CloudPageBlob.DownloadToStream**方法，取決於 hello blob 類型。</span><span class="sxs-lookup"><span data-stu-id="a0321-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="a0321-213">hello 下列程式碼片段會使用 hello **CloudBlockBlob.DownloadToStream** blob 的內容 tooa 資料流物件的方法 tootransfer 然後保存 tooa 本機檔案: (變更*&lt;本機檔案名稱>* toohello 完整檔案名稱代表您想要下載的 hello blob。)</span><span class="sxs-lookup"><span data-stu-id="a0321-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="a0321-214">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="a0321-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a0321-215">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a0321-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="a0321-216">執行 hello 應用程式，並選取**下載 blob** toodownload hello blob。</span><span class="sxs-lookup"><span data-stu-id="a0321-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="a0321-217">指定在 hello 的 hello blob **CloudBlobContainer.GetBlockBlobReference**方法呼叫會下載您指定在 hello toohello 位置**File.OpenWrite**方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="a0321-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="a0321-218">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="a0321-218">Delete blobs</span></span>

<span data-ttu-id="a0321-219">hello 下列步驟說明如何 toodelete blob:</span><span class="sxs-lookup"><span data-stu-id="a0321-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a0321-220">hello 本節中的程式碼假設您已經完成 hello 區段中的 hello 步驟[設定 hello 開發環境](#set-up-the-development-environment)。</span><span class="sxs-lookup"><span data-stu-id="a0321-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="a0321-221">開啟 hello`BlobsController.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="a0321-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="a0321-222">新增名為 **DeleteBlob** 的方法，其會傳回 **ActionResult**。</span><span class="sxs-lookup"><span data-stu-id="a0321-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="a0321-223">取得 **CloudStorageAccount** 物件，其代表您的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="a0321-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a0321-224">使用 hello 下列程式碼 tooget hello 儲存體連接字串和儲存體帳戶資訊 hello Azure 服務組態: (變更*&lt;儲存體帳戶名稱 >* toohello hello Azure 儲存體名稱您正在存取帳戶。）</span><span class="sxs-lookup"><span data-stu-id="a0321-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="a0321-225">取得 **CloudBlobClient** 物件，代表 Blob 服務用戶端。</span><span class="sxs-lookup"><span data-stu-id="a0321-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="a0321-226">取得**CloudBlobContainer**物件，代表參考 toohello blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="a0321-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="a0321-227">藉由呼叫 **CloudBlobContainer.GetBlockBlobReference** 或 **CloudBlobContainer.GetPageBlobReference** 方法取得 blob 參考物件。</span><span class="sxs-lookup"><span data-stu-id="a0321-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="a0321-228">(變更 *&lt;blob 名稱 >* toohello 您要刪除的 hello blob 名稱。)</span><span class="sxs-lookup"><span data-stu-id="a0321-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="a0321-229">在 [hello**方案總管] 中**，展開 hello**檢視]-> [共用**資料夾，然後開啟`_Layout.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="a0321-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="a0321-230">之後 hello 最後**Html.ActionLink**，加入下列 hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="a0321-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="a0321-231">執行 hello 應用程式，並選取**刪除 blob** toodelete hello blob 中 hello 指定**CloudBlobContainer.GetBlockBlobReference**方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="a0321-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a0321-232">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0321-232">Next steps</span></span>
<span data-ttu-id="a0321-233">檢視有關將資料儲存在 Azure 中的其他選項的詳細功能指南 toolearn。</span><span class="sxs-lookup"><span data-stu-id="a0321-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="a0321-234">開始使用 Azure 資料表儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="a0321-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="a0321-235">開始使用 Azure 佇列儲存體和 Visual Studio 已連線的服務 (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="a0321-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
