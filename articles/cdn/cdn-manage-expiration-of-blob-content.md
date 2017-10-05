---
title: "在 Azure CDN 中管理 Azure 儲存體 Blob 的到期 | Microsoft Docs"
description: "深入了解選項，以控制 Azure CDN 快取中的 Blob 存留時間。"
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
ms.openlocfilehash: d4741921806e443d92c385a04b781cec296c2ae8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="b686b-103">在 Azure CDN 中管理 Azure 儲存體 Blob 的到期</span><span class="sxs-lookup"><span data-stu-id="b686b-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b686b-104">Azure Web Apps/雲端服務、ASP.NET 或 IIS</span><span class="sxs-lookup"><span data-stu-id="b686b-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="b686b-105">Azure 儲存體 Blob 服務</span><span class="sxs-lookup"><span data-stu-id="b686b-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="b686b-106">[Azure 儲存體](../storage/common/storage-introduction.md)中的 [Blob 服務](../storage/common/storage-introduction.md#blob-storage)是數個已與 Azure CDN 整合之 Azure 型來源的其中一個。</span><span class="sxs-lookup"><span data-stu-id="b686b-106">The [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="b686b-107">任何可公開存取的 Blob 內容均可在 Azure CDN 中加以快取，直到其存留時間 (TTL) 結束。</span><span class="sxs-lookup"><span data-stu-id="b686b-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="b686b-108">TTL 是由來自 Azure 儲存體之 HTTP 回應中的 [ 標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) 所決定。</span><span class="sxs-lookup"><span data-stu-id="b686b-108">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="b686b-109">您可以選擇不對 Blob 設定任何 TTL。</span><span class="sxs-lookup"><span data-stu-id="b686b-109">You may choose to set no TTL on a blob.</span></span>  <span data-ttu-id="b686b-110">在此情況下，Azure CDN 會自動套用預設為期 7 天的 TTL。</span><span class="sxs-lookup"><span data-stu-id="b686b-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="b686b-111">如需 Azure CDN 如何運作以加快對 Blob 和其他檔案存取速度的詳細資訊，請參閱 [Azure CDN 概觀](cdn-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b686b-111">For more information about how Azure CDN works to speed up access to blobs and other files, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="b686b-112">如需 Azure 儲存體 Blob 服務的詳細資料，請參閱 [Blob 服務概念](https://msdn.microsoft.com/library/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b686b-112">For more details on the Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="b686b-113">本教學課程會示範幾種可對 Azure 儲存體中的 Blob 設定 TTL 的方法。</span><span class="sxs-lookup"><span data-stu-id="b686b-113">This tutorial demonstrates several ways that you can set the TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="b686b-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b686b-114">Azure PowerShell</span></span>
<span data-ttu-id="b686b-115">[Azure PowerShell](/powershell/azure/overview) 是其中一種最快速、最強大的 Azure 服務管理方式。</span><span class="sxs-lookup"><span data-stu-id="b686b-115">[Azure PowerShell](/powershell/azure/overview) is one of the quickest, most powerful ways to administer your Azure services.</span></span>  <span data-ttu-id="b686b-116">請使用 `Get-AzureStorageBlob` Cmdlet 來取得 Blob 的參考，然後設定 `.ICloudBlob.Properties.CacheControl` 屬性。</span><span class="sxs-lookup"><span data-stu-id="b686b-116">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="b686b-117">您也可以使用 PowerShell 來[管理 CDN 設定檔和端點](cdn-manage-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="b686b-117">You can also use PowerShell to [manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="b686b-118">適用於 .NET 的 Azure 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="b686b-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="b686b-119">若要使用 .NET 設定 Blob 的 TTL，請使用[適用於 .NET 的 Azure 儲存體用戶端程式庫](../storage/blobs/storage-dotnet-how-to-use-blobs.md)，來設定 [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) 屬性。</span><span class="sxs-lookup"><span data-stu-id="b686b-119">To set a blob's TTL using .NET, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="b686b-120">[適用於 .NET 的 Azure Blob 儲存體範例](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)中另外還提供了許多 .NET 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="b686b-120">There are many more .NET code samples available in the [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="b686b-121">其他方法</span><span class="sxs-lookup"><span data-stu-id="b686b-121">Other methods</span></span>
* [<span data-ttu-id="b686b-122">Azure 命令列介面</span><span class="sxs-lookup"><span data-stu-id="b686b-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="b686b-123">上傳 Blob 時，使用 `-p` 參數設定 *cacheControl* 屬性。</span><span class="sxs-lookup"><span data-stu-id="b686b-123">When uploading the blob, set the *cacheControl* property using the `-p` switch.</span></span>  <span data-ttu-id="b686b-124">本範例將 TTL 設定為一小時 (3600 秒)。</span><span class="sxs-lookup"><span data-stu-id="b686b-124">This example sets the TTL to one hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="b686b-125">Azure 儲存體服務 REST API</span><span class="sxs-lookup"><span data-stu-id="b686b-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="b686b-126">在[放置 Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx)、[放置區塊清單](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx)或[設定 Blob 屬性](https://msdn.microsoft.com/library/azure/ee691966.aspx)要求中，明確設定 *x-ms-blob-cache-control* 屬性。</span><span class="sxs-lookup"><span data-stu-id="b686b-126">Explicitly set the *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="b686b-127">協力廠商儲存體管理工具</span><span class="sxs-lookup"><span data-stu-id="b686b-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="b686b-128">某些協力廠商 Azure 儲存體管理工具可讓您對 Blob 設定「CacheControl」  屬性。</span><span class="sxs-lookup"><span data-stu-id="b686b-128">Some third-party Azure Storage management tools allow you to set the *CacheControl* property on blobs.</span></span> 

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="b686b-129">測試「Cache-Control」  標頭</span><span class="sxs-lookup"><span data-stu-id="b686b-129">Testing the *Cache-Control* header</span></span>
<span data-ttu-id="b686b-130">您可以輕鬆地確認 Blob 的 TTL。</span><span class="sxs-lookup"><span data-stu-id="b686b-130">You can easily verify the TTL of your blobs.</span></span>  <span data-ttu-id="b686b-131">使用瀏覽器的[開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)，測試 Blob 是否包含 *Cache-Control* 回應標頭。</span><span class="sxs-lookup"><span data-stu-id="b686b-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including the *Cache-Control* response header.</span></span>  <span data-ttu-id="b686b-132">您也可以使用 **wget**、[Postman](https://www.getpostman.com/) 或 [Fiddler](http://www.telerik.com/fiddler) 之類的工具來檢查回應標頭。</span><span class="sxs-lookup"><span data-stu-id="b686b-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b686b-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b686b-133">Next Steps</span></span>
* [<span data-ttu-id="b686b-134">了解 *Cache-Control* 標頭</span><span class="sxs-lookup"><span data-stu-id="b686b-134">Read about the *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="b686b-135">了解如何在 Azure CDN 中管理雲端服務內容的到期</span><span class="sxs-lookup"><span data-stu-id="b686b-135">Learn how to manage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

