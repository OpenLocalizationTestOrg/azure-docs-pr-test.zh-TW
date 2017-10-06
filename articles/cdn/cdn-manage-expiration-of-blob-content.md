---
title: "Azure CDN 中的 Azure 儲存體 blob aaaManage 到期 |Microsoft 文件"
description: "深入了解控制 Azure CDN 快取中的 blob 的存留時間的 hello 選項。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="1fe6b-103">在 Azure CDN 中管理 Azure 儲存體 Blob 的到期</span><span class="sxs-lookup"><span data-stu-id="1fe6b-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fe6b-104">Azure Web Apps/雲端服務、ASP.NET 或 IIS</span><span class="sxs-lookup"><span data-stu-id="1fe6b-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="1fe6b-105">Azure 儲存體 Blob 服務</span><span class="sxs-lookup"><span data-stu-id="1fe6b-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="1fe6b-106">hello [blob 服務](../storage/common/storage-introduction.md#blob-storage)中[Azure 儲存體](../storage/common/storage-introduction.md)以 Azure 為基礎的數個來源的其中一個與整合 Azure CDN。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="1fe6b-107">任何可公開存取的 Blob 內容均可在 Azure CDN 中加以快取，直到其存留時間 (TTL) 結束。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="1fe6b-108">hello TTL 由 hello [ *Cache-control*標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)hello HTTP 回應從 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="1fe6b-109">您可以選擇 tooset 的 blob 上沒有 TTL。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="1fe6b-110">在此情況下，Azure CDN 會自動套用預設為期 7 天的 TTL。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="1fe6b-111">如需有關 Azure CDN toospeed 存取 tooblobs 和其他檔案的運作方式的詳細資訊，請參閱 hello [Azure CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="1fe6b-112">如需有關 hello Azure 儲存體 blob 服務的詳細資訊，請參閱[Blob 服務概念](https://msdn.microsoft.com/library/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="1fe6b-113">本教學課程會示範數種方式，您可以在 Azure 儲存體中的 blob 上設定 hello TTL。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="1fe6b-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fe6b-114">Azure PowerShell</span></span>
<span data-ttu-id="1fe6b-115">[Azure PowerShell](/powershell/azure/overview) hello 最快速、 最強大的方式來 tooadminister 的其中一個是您的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="1fe6b-116">使用 hello `Get-AzureStorageBlob` cmdlet tooget 參考 toohello blob，然後設定 hello`.ICloudBlob.Properties.CacheControl`屬性。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="1fe6b-117">也可以使用 PowerShell 太[管理您的 CDN 設定檔和端點](cdn-manage-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="1fe6b-118">適用於 .NET 的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="1fe6b-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="1fe6b-119">tooset blob 的 TTL 使用.NET 中，使用 hello[適用於.NET 的 Azure 儲存體用戶端程式庫](../storage/blobs/storage-dotnet-how-to-use-blobs.md)tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx)屬性。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="1fe6b-120">許多其他的.NET 程式碼範例中的 hello[適用於.NET 的 Azure Blob 儲存體範例](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="1fe6b-121">其他方法</span><span class="sxs-lookup"><span data-stu-id="1fe6b-121">Other methods</span></span>
* [<span data-ttu-id="1fe6b-122">Azure 命令列介面</span><span class="sxs-lookup"><span data-stu-id="1fe6b-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="1fe6b-123">上傳時 hello blob，設定 hello *cacheControl*屬性使用 hello`-p`切換。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="1fe6b-124">此範例會設定 hello TTL tooone 小時 （3600 秒）。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="1fe6b-125">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="1fe6b-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="1fe6b-126">明確地設定 hello *x-ms-blob 的快取控制*屬性[Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx)，[放置區塊清單](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx)，或[設定 Blob 屬性](https://msdn.microsoft.com/library/azure/ee691966.aspx)要求。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="1fe6b-127">協力廠商儲存體管理工具</span><span class="sxs-lookup"><span data-stu-id="1fe6b-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="1fe6b-128">某些協力廠商 Azure 儲存體管理工具可讓您 tooset hello *CacheControl* blob 上的屬性。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="1fe6b-129">測試 hello *Cache-control*標頭</span><span class="sxs-lookup"><span data-stu-id="1fe6b-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="1fe6b-130">您可以輕鬆地確認 hello TTL 為您的 blob。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="1fe6b-131">使用您的瀏覽器[開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)，測試您的 blob 會包括 hello *Cache-control*回應標頭。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="1fe6b-132">您也可以使用這類工具**wget**，[郵差](https://www.getpostman.com/)，或[Fiddler](http://www.telerik.com/fiddler) tooexamine hello 回應標頭。</span><span class="sxs-lookup"><span data-stu-id="1fe6b-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fe6b-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1fe6b-133">Next Steps</span></span>
* [<span data-ttu-id="1fe6b-134">閱讀有關 hello *Cache-control*標頭</span><span class="sxs-lookup"><span data-stu-id="1fe6b-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="1fe6b-135">深入了解如何在 Azure CDN 中的雲端服務內容 toomanage 到期</span><span class="sxs-lookup"><span data-stu-id="1fe6b-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

