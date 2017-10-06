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
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>在 Azure CDN 中管理 Azure 儲存體 Blob 的到期
> [!div class="op_single_selector"]
> * [Azure Web Apps/雲端服務、ASP.NET 或 IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure 儲存體 Blob 服務](cdn-manage-expiration-of-blob-content.md)
> 
> 

hello [blob 服務](../storage/common/storage-introduction.md#blob-storage)中[Azure 儲存體](../storage/common/storage-introduction.md)以 Azure 為基礎的數個來源的其中一個與整合 Azure CDN。  任何可公開存取的 Blob 內容均可在 Azure CDN 中加以快取，直到其存留時間 (TTL) 結束。  hello TTL 由 hello [ *Cache-control*標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)hello HTTP 回應從 Azure 儲存體中。

> [!TIP]
> 您可以選擇 tooset 的 blob 上沒有 TTL。  在此情況下，Azure CDN 會自動套用預設為期 7 天的 TTL。
> 
> 如需有關 Azure CDN toospeed 存取 tooblobs 和其他檔案的運作方式的詳細資訊，請參閱 hello [Azure CDN 概觀](cdn-overview.md)。
> 
> 如需有關 hello Azure 儲存體 blob 服務的詳細資訊，請參閱[Blob 服務概念](https://msdn.microsoft.com/library/dd179376.aspx)。 
> 
> 

本教學課程會示範數種方式，您可以在 Azure 儲存體中的 blob 上設定 hello TTL。  

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) hello 最快速、 最強大的方式來 tooadminister 的其中一個是您的 Azure 服務。  使用 hello `Get-AzureStorageBlob` cmdlet tooget 參考 toohello blob，然後設定 hello`.ICloudBlob.Properties.CacheControl`屬性。 

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
> 也可以使用 PowerShell 太[管理您的 CDN 設定檔和端點](cdn-manage-powershell.md)。
> 
> 

## <a name="azure-storage-client-library-for-net"></a>適用於 .NET 的 Azure 儲存體用戶端程式庫
tooset blob 的 TTL 使用.NET 中，使用 hello[適用於.NET 的 Azure 儲存體用戶端程式庫](../storage/blobs/storage-dotnet-how-to-use-blobs.md)tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx)屬性。

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
> 許多其他的.NET 程式碼範例中的 hello[適用於.NET 的 Azure Blob 儲存體範例](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)。
> 
> 

## <a name="other-methods"></a>其他方法
* [Azure 命令列介面](../cli-install-nodejs.md)
  
    上傳時 hello blob，設定 hello *cacheControl*屬性使用 hello`-p`切換。  此範例會設定 hello TTL tooone 小時 （3600 秒）。
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [Azure 儲存體服務 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    明確地設定 hello *x-ms-blob 的快取控制*屬性[Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx)，[放置區塊清單](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx)，或[設定 Blob 屬性](https://msdn.microsoft.com/library/azure/ee691966.aspx)要求。
* 協力廠商儲存體管理工具
  
    某些協力廠商 Azure 儲存體管理工具可讓您 tooset hello *CacheControl* blob 上的屬性。 

## <a name="testing-hello-cache-control-header"></a>測試 hello *Cache-control*標頭
您可以輕鬆地確認 hello TTL 為您的 blob。  使用您的瀏覽器[開發人員工具](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)，測試您的 blob 會包括 hello *Cache-control*回應標頭。  您也可以使用這類工具**wget**，[郵差](https://www.getpostman.com/)，或[Fiddler](http://www.telerik.com/fiddler) tooexamine hello 回應標頭。

## <a name="next-steps"></a>後續步驟
* [閱讀有關 hello *Cache-control*標頭](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [深入了解如何在 Azure CDN 中的雲端服務內容 toomanage 到期](cdn-manage-expiration-of-cloud-service-content.md)

