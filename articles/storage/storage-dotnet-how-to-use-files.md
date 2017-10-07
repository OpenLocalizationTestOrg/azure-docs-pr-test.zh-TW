---
title: "使用.NET 的 Azure 檔案儲存的 aaaDevelop |Microsoft 文件"
description: "了解 toodevelop.NET 應用程式和服務使用 Azure 檔案儲存體 toostore 檔案資料。"
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: aa8f84f1c93249055370e2a2cb33d7118b972be1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a>使用 .NET 開發 Azure 檔案儲存體 
> [!NOTE]
> 本文將說明如何 toomanage Azure 檔案儲存體.NET 程式碼。 toolearn 進一步了解 Azure 檔案儲存體，請參閱 hello[簡介 tooAzure 檔案儲存體](storage-files-introduction.md)。
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>關於本教學課程
本教學課程將示範 hello 使用.NET toodevelop 應用程式或服務使用 Azure 檔案儲存體 toostore 檔案資料的基本概念。 在本教學課程中，我們將建立簡單的主控台應用程式，並顯示如何使用.NET 和 Azure 檔案儲存體 tooperform 基本動作：

* 取得檔案的 hello 內容
* 設定 hello 檔案共用的 hello 配額 （最大大小）。
* 建立使用共用的存取原則，定義 hello 共用上的檔案共用的存取簽章 （SAS 索引鍵）。
* 複製檔案 tooanother hello 中相同的儲存體帳戶。
* 將檔案 tooa blob 複製 hello 中相同的儲存體帳戶。
* 使用 Azure 儲存體度量進行疑難排解

> [!Note]  
> 因為可能透過 SMB 存取 Azure 檔案儲存體，所以可能 toowrite 簡單的應用程式存取使用的檔案 I/O hello 標準 System.IO 類別 hello Azure 檔案共用。 本文將說明如何使用 toowrite 應用程式 hello Azure 儲存體.NET SDK，它會使用 hello [Azure 檔案儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 檔案存放裝置。 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>建立 hello 主控台應用程式，並取得 hello 組件
在 Visual Studio 中，建立新的 Windows 主控台應用程式。 下列步驟的 hello 顯示 toocreate 2017，不過，hello 步驟的 Visual Studio 中的主控台應用程式的方式類似在其他版本的 Visual Studio。

1. 選取 [檔案] > [新增] > [專案]
2. 選取 [安裝] > [範本] > [Visual C#] > [Windows 傳統桌面]
3. 選取 **主控台應用程式 (.NET Framework)**
4. 輸入您的應用程式的名稱在 hello**名稱：**欄位
5. 選取 [確定]

本教學課程中的所有程式碼範例可加入 toohello`Main()`的主控台應用程式的方法`Program.cs`檔案。

您可以在任何類型的.NET 應用程式，包括 Azure 雲端服務或 web 應用程式和桌上型電腦與行動應用程式中使用 hello Azure 儲存體用戶端程式庫。 在本指南中，為求簡化，我們會使用主控台應用程式。

## <a name="use-nuget-tooinstall-hello-required-packages"></a>使用 NuGet tooinstall hello 必要封裝
有兩個封裝，您需要 tooreference 專案 toocomplete 在本教學課程：

* [Microsoft Azure 儲存體用戶端程式庫適用於.NET](https://www.nuget.org/packages/WindowsAzure.Storage/)： 此封裝提供以程式設計方式存取 toodata 儲存體帳戶中的資源。
* [適用於 .NET 的 Microsoft Azure Configuration Manager 程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)︰此套件提供一個類別，無論您的應用程式於何處執行，均可用來剖析組態檔中的連接字串。

您可以使用 NuGet tooobtain 這兩個封裝。 請遵循下列步驟：

1. 在 [方案總管] 中以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 封裝]。
2. 線上搜尋"WindowsAzure.Storage"，然後按一下**安裝**tooinstall hello 儲存體用戶端程式庫和其相依性。
3. 線上搜尋"WindowsAzure.ConfigurationManager 」，然後按一下**安裝**tooinstall hello Azure 組態管理員。

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>儲存儲存體帳戶認證 toohello app.config 檔案
接著，將您的認證儲存到專案的 app.config 檔案。 編輯 hello app.config 檔案，使其出現類似下列範例中，取代的 toohello`myaccount`使用儲存體帳戶名稱，和`mykey`與儲存體帳戶金鑰。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> hello hello Azure 儲存體模擬器最新版本不支援 Azure 檔案儲存體。 您的連接字串必須為目標 Azure 儲存體帳戶中 hello 雲端 toowork 具有 Azure 檔案存放裝置。

## <a name="add-using-directives"></a>新增 using 指示詞
開啟 hello`Program.cs`檔從 [方案總管] 中，並加入下列 hello 使用指示詞 toohello hello 檔案最上方。

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>存取 hello 檔案共用以程式設計的方式
接下來，加入下列程式碼 toohello hello`Main()`方法 （在上述程式碼的 hello） 之後 tooretrieve hello 連接字串。 這段程式碼取得我們稍早建立的參考 toohello 檔案，並將其內容 toohello 主控台視窗輸出。

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

執行 hello 主控台應用程式 toosee hello 輸出。

## <a name="set-hello-maximum-size-for-a-file-share"></a>設定檔案共用的 hello 最大容量
版起 5.x 的 hello Azure 儲存體用戶端程式庫，您可以設定組 hello 配額 （或最大值） 檔案共用，以 gb 為單位。 您也可以檢查的 toosee 多少資料目前儲存在 hello 共用。

共用設定 hello 配額，您可以限制 hello 的 hello hello 共用上儲存的檔案大小總計。 如果 hello 的 hello 共用上的檔案大小總計超過 hello 配額設定為在 hello 共用，然後用戶端，將現有的檔案無法 tooincrease hello 大小或建立新的檔案，除非那些檔案是空的。

下列的 hello 範例示範如何 toocheck hello 共用所需的目前使用量以及如何 tooset hello hello 共用配額。

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>產生檔案或檔案共用的共用存取簽章
版起 5.x 的 hello Azure 儲存體用戶端程式庫，您可以產生共用的存取簽章 (SAS) 的檔案共用，或針對個別檔案。 您也可以建立共用的存取原則在檔案共用 toomanage 共用存取簽章。 建立共用的存取原則被建議，因為它提供撤銷 hello SAS，如果它應該會受到危害的方法。

下列範例中的 hello 共用上，建立共用的存取原則，然後使用 原則 tooprovide hello 條件約束 SAS hello 中的檔案共用。

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

如需建立與使用共用存取簽章的詳細資訊，請參閱[共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 和[透過 Azure Blob 建立與使用 SAS](storage-dotnet-shared-access-signature-part-2.md)。

## <a name="copy-files"></a>複製檔案
版起 5.x 的 hello Azure 儲存體用戶端程式庫，您可以複製檔案 tooanother 檔案、 檔案 tooa blob 或 blob tooa 檔案。 在 hello 下一步 區段中，我們將示範如何 tooperform 這些複製作業以程式設計的方式。

您也可以使用 AzCopy toocopy 一個檔 tooanother 或 toocopy blob tooa 檔案，反之亦然。 請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。

> [!NOTE]
> 如果您複製 blob tooa 檔案或檔案 tooa blob，您必須使用共用的存取簽章 (SAS) tooauthenticate hello 來源物件，即使您正在複製內 hello 相同儲存體帳戶。
> 
> 

**複製檔案 tooanother** hello 下列範例會將複製檔案 tooanother hello 中相同的共用。 因為之間複製此複製作業中的檔案 hello 相同儲存體帳戶，您可以使用共用金鑰驗證 tooperform hello 複製。

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

**複製檔案 tooa blob** hello 下列範例會建立檔案並將其複製內 hello tooa blob 相同儲存體帳戶。 hello 範例會建立哪一種 hello 服務 hello 複製作業期間使用 tooauthenticate 存取 toohello 原始程式檔的 hello 來源檔案的 SA。

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

您可以在 hello 複製 blob tooa 檔案相同的方式。 如果 hello 來源物件是 blob，然後建立 SAS tooauthenticate 存取 toothat blob hello 複製作業期間。

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>使用度量針對 Azure 檔案儲存體進行疑難排解
Azure 儲存體分析現在支援 Azure 檔案儲存體的度量。 利用度量資料，您可以追蹤要求及診斷問題。


您可以啟用從 hello Azure 檔案儲存體度量[Azure 入口網站](https://portal.azure.com)。 您也可以啟用以程式設計方式呼叫 hello hello REST API，透過設定檔案服務屬性作業，或其雷同 hello 儲存體用戶端程式庫中的其中一個度量。


hello，下列程式碼範例示範如何 toouse hello Azure 檔案儲存體的.NET tooenable 度量的儲存體用戶端程式庫。

首先，新增下列 hello`using`指示詞 tooyour`Program.cs`檔案，另外 toothose 上述您新增：

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

請注意，Azure Blob、 Azure 資料表及 Azure 佇列時，使用共用的 hello `ServiceProperties` hello 中的型別`Microsoft.WindowsAzure.Storage.Shared.Protocol`命名空間，Azure 檔案儲存體使用自己的型別，hello `FileServiceProperties` hello 中的型別`Microsoft.WindowsAzure.Storage.File.Protocol`命名空間。 兩個命名空間必須參考從程式碼，不過，如下列程式碼 toocompile hello。

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

此外，您可以使用參照太[Azure 檔案儲存體疑難排解文章](storage-troubleshoot-file-connection-problems.md)的端對端疑難排解指引。

## <a name="next-steps"></a>後續步驟
請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。

### <a name="conceptual-articles-and-videos"></a>概念性文章和影片
* [Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [如何 toouse Linux 的 Azure 檔案儲存體](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>檔案儲存體的工具支援
* [搭配使用 Azure PowerShell 與 Azure 儲存體](storage-powershell-guide-full.md)
* [如何 toouse AzCopy 與 Microsoft Azure 儲存體](storage-use-azcopy.md)
* [使用 Azure CLI hello 與 Azure 儲存體](storage-azure-cli.md#create-and-manage-file-shares)
* [針對 Azure 檔案儲存體的問題進行疑難排解](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>參考
* [Storage Client Library for .NET 參考資料](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [檔案服務 REST API 參考](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>部落格文章
* [Azure 檔案儲存體現已公開推出](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Azure 檔案儲存體內部](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Microsoft Azure 檔案服務簡介](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [持續性連線 tooMicrosoft Azure 檔案儲存體](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
