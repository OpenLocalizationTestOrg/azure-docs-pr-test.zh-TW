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
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="919ca-103">使用 .NET 開發 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="919ca-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="919ca-104">本文將說明如何 toomanage Azure 檔案儲存體.NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="919ca-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="919ca-105">toolearn 進一步了解 Azure 檔案儲存體，請參閱 hello[簡介 tooAzure 檔案儲存體](storage-files-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="919ca-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="919ca-106">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="919ca-106">About this tutorial</span></span>
<span data-ttu-id="919ca-107">本教學課程將示範 hello 使用.NET toodevelop 應用程式或服務使用 Azure 檔案儲存體 toostore 檔案資料的基本概念。</span><span class="sxs-lookup"><span data-stu-id="919ca-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="919ca-108">在本教學課程中，我們將建立簡單的主控台應用程式，並顯示如何使用.NET 和 Azure 檔案儲存體 tooperform 基本動作：</span><span class="sxs-lookup"><span data-stu-id="919ca-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="919ca-109">取得檔案的 hello 內容</span><span class="sxs-lookup"><span data-stu-id="919ca-109">Get hello contents of a file</span></span>
* <span data-ttu-id="919ca-110">設定 hello 檔案共用的 hello 配額 （最大大小）。</span><span class="sxs-lookup"><span data-stu-id="919ca-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="919ca-111">建立使用共用的存取原則，定義 hello 共用上的檔案共用的存取簽章 （SAS 索引鍵）。</span><span class="sxs-lookup"><span data-stu-id="919ca-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="919ca-112">複製檔案 tooanother hello 中相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="919ca-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="919ca-113">將檔案 tooa blob 複製 hello 中相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="919ca-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="919ca-114">使用 Azure 儲存體度量進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="919ca-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="919ca-115">因為可能透過 SMB 存取 Azure 檔案儲存體，所以可能 toowrite 簡單的應用程式存取使用的檔案 I/O hello 標準 System.IO 類別 hello Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="919ca-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="919ca-116">本文將說明如何使用 toowrite 應用程式 hello Azure 儲存體.NET SDK，它會使用 hello [Azure 檔案儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure 檔案存放裝置。</span><span class="sxs-lookup"><span data-stu-id="919ca-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="919ca-117">建立 hello 主控台應用程式，並取得 hello 組件</span><span class="sxs-lookup"><span data-stu-id="919ca-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="919ca-118">在 Visual Studio 中，建立新的 Windows 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="919ca-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="919ca-119">下列步驟的 hello 顯示 toocreate 2017，不過，hello 步驟的 Visual Studio 中的主控台應用程式的方式類似在其他版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="919ca-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="919ca-120">選取 [檔案] > [新增] > [專案]</span><span class="sxs-lookup"><span data-stu-id="919ca-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="919ca-121">選取 [安裝] > [範本] > [Visual C#] > [Windows 傳統桌面]</span><span class="sxs-lookup"><span data-stu-id="919ca-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="919ca-122">選取 **主控台應用程式 (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="919ca-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="919ca-123">輸入您的應用程式的名稱在 hello**名稱：**欄位</span><span class="sxs-lookup"><span data-stu-id="919ca-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="919ca-124">選取 [確定]</span><span class="sxs-lookup"><span data-stu-id="919ca-124">Select **OK**</span></span>

<span data-ttu-id="919ca-125">本教學課程中的所有程式碼範例可加入 toohello`Main()`的主控台應用程式的方法`Program.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="919ca-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="919ca-126">您可以在任何類型的.NET 應用程式，包括 Azure 雲端服務或 web 應用程式和桌上型電腦與行動應用程式中使用 hello Azure 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="919ca-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="919ca-127">在本指南中，為求簡化，我們會使用主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="919ca-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="919ca-128">使用 NuGet tooinstall hello 必要封裝</span><span class="sxs-lookup"><span data-stu-id="919ca-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="919ca-129">有兩個封裝，您需要 tooreference 專案 toocomplete 在本教學課程：</span><span class="sxs-lookup"><span data-stu-id="919ca-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="919ca-130">[Microsoft Azure 儲存體用戶端程式庫適用於.NET](https://www.nuget.org/packages/WindowsAzure.Storage/)： 此封裝提供以程式設計方式存取 toodata 儲存體帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="919ca-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="919ca-131">[適用於 .NET 的 Microsoft Azure Configuration Manager 程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)︰此套件提供一個類別，無論您的應用程式於何處執行，均可用來剖析組態檔中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="919ca-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="919ca-132">您可以使用 NuGet tooobtain 這兩個封裝。</span><span class="sxs-lookup"><span data-stu-id="919ca-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="919ca-133">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="919ca-133">Follow these steps:</span></span>

1. <span data-ttu-id="919ca-134">在 [方案總管] 中以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="919ca-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="919ca-135">線上搜尋"WindowsAzure.Storage"，然後按一下**安裝**tooinstall hello 儲存體用戶端程式庫和其相依性。</span><span class="sxs-lookup"><span data-stu-id="919ca-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="919ca-136">線上搜尋"WindowsAzure.ConfigurationManager 」，然後按一下**安裝**tooinstall hello Azure 組態管理員。</span><span class="sxs-lookup"><span data-stu-id="919ca-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="919ca-137">儲存儲存體帳戶認證 toohello app.config 檔案</span><span class="sxs-lookup"><span data-stu-id="919ca-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="919ca-138">接著，將您的認證儲存到專案的 app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="919ca-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="919ca-139">編輯 hello app.config 檔案，使其出現類似下列範例中，取代的 toohello`myaccount`使用儲存體帳戶名稱，和`mykey`與儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="919ca-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> hello hello Azure 儲存體模擬器最新版本不支援 Azure 檔案儲存體。 <span data-ttu-id="919ca-141">您的連接字串必須為目標 Azure 儲存體帳戶中 hello 雲端 toowork 具有 Azure 檔案存放裝置。</span><span class="sxs-lookup"><span data-stu-id="919ca-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="919ca-142">新增 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="919ca-142">Add using directives</span></span>
<span data-ttu-id="919ca-143">開啟 hello`Program.cs`檔從 [方案總管] 中，並加入下列 hello 使用指示詞 toohello hello 檔案最上方。</span><span class="sxs-lookup"><span data-stu-id="919ca-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="919ca-144">存取 hello 檔案共用以程式設計的方式</span><span class="sxs-lookup"><span data-stu-id="919ca-144">Access hello file share programmatically</span></span>
<span data-ttu-id="919ca-145">接下來，加入下列程式碼 toohello hello`Main()`方法 （在上述程式碼的 hello） 之後 tooretrieve hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="919ca-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="919ca-146">這段程式碼取得我們稍早建立的參考 toohello 檔案，並將其內容 toohello 主控台視窗輸出。</span><span class="sxs-lookup"><span data-stu-id="919ca-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

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

<span data-ttu-id="919ca-147">執行 hello 主控台應用程式 toosee hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="919ca-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="919ca-148">設定檔案共用的 hello 最大容量</span><span class="sxs-lookup"><span data-stu-id="919ca-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="919ca-149">版起 5.x 的 hello Azure 儲存體用戶端程式庫，您可以設定組 hello 配額 （或最大值） 檔案共用，以 gb 為單位。</span><span class="sxs-lookup"><span data-stu-id="919ca-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="919ca-150">您也可以檢查的 toosee 多少資料目前儲存在 hello 共用。</span><span class="sxs-lookup"><span data-stu-id="919ca-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="919ca-151">共用設定 hello 配額，您可以限制 hello 的 hello hello 共用上儲存的檔案大小總計。</span><span class="sxs-lookup"><span data-stu-id="919ca-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="919ca-152">如果 hello 的 hello 共用上的檔案大小總計超過 hello 配額設定為在 hello 共用，然後用戶端，將現有的檔案無法 tooincrease hello 大小或建立新的檔案，除非那些檔案是空的。</span><span class="sxs-lookup"><span data-stu-id="919ca-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="919ca-153">下列的 hello 範例示範如何 toocheck hello 共用所需的目前使用量以及如何 tooset hello hello 共用配額。</span><span class="sxs-lookup"><span data-stu-id="919ca-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="919ca-154">產生檔案或檔案共用的共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="919ca-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="919ca-155">版起 5.x 的 hello Azure 儲存體用戶端程式庫，您可以產生共用的存取簽章 (SAS) 的檔案共用，或針對個別檔案。</span><span class="sxs-lookup"><span data-stu-id="919ca-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="919ca-156">您也可以建立共用的存取原則在檔案共用 toomanage 共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="919ca-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="919ca-157">建立共用的存取原則被建議，因為它提供撤銷 hello SAS，如果它應該會受到危害的方法。</span><span class="sxs-lookup"><span data-stu-id="919ca-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="919ca-158">下列範例中的 hello 共用上，建立共用的存取原則，然後使用 原則 tooprovide hello 條件約束 SAS hello 中的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="919ca-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

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

<span data-ttu-id="919ca-159">如需建立與使用共用存取簽章的詳細資訊，請參閱[共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 和[透過 Azure Blob 建立與使用 SAS](storage-dotnet-shared-access-signature-part-2.md)。</span><span class="sxs-lookup"><span data-stu-id="919ca-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="919ca-160">複製檔案</span><span class="sxs-lookup"><span data-stu-id="919ca-160">Copy files</span></span>
<span data-ttu-id="919ca-161">版起 5.x 的 hello Azure 儲存體用戶端程式庫，您可以複製檔案 tooanother 檔案、 檔案 tooa blob 或 blob tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="919ca-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="919ca-162">在 hello 下一步 區段中，我們將示範如何 tooperform 這些複製作業以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="919ca-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="919ca-163">您也可以使用 AzCopy toocopy 一個檔 tooanother 或 toocopy blob tooa 檔案，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="919ca-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="919ca-164">請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="919ca-164">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="919ca-165">如果您複製 blob tooa 檔案或檔案 tooa blob，您必須使用共用的存取簽章 (SAS) tooauthenticate hello 來源物件，即使您正在複製內 hello 相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="919ca-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="919ca-166">**複製檔案 tooanother** hello 下列範例會將複製檔案 tooanother hello 中相同的共用。</span><span class="sxs-lookup"><span data-stu-id="919ca-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="919ca-167">因為之間複製此複製作業中的檔案 hello 相同儲存體帳戶，您可以使用共用金鑰驗證 tooperform hello 複製。</span><span class="sxs-lookup"><span data-stu-id="919ca-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

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

<span data-ttu-id="919ca-168">**複製檔案 tooa blob** hello 下列範例會建立檔案並將其複製內 hello tooa blob 相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="919ca-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="919ca-169">hello 範例會建立哪一種 hello 服務 hello 複製作業期間使用 tooauthenticate 存取 toohello 原始程式檔的 hello 來源檔案的 SA。</span><span class="sxs-lookup"><span data-stu-id="919ca-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

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

<span data-ttu-id="919ca-170">您可以在 hello 複製 blob tooa 檔案相同的方式。</span><span class="sxs-lookup"><span data-stu-id="919ca-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="919ca-171">如果 hello 來源物件是 blob，然後建立 SAS tooauthenticate 存取 toothat blob hello 複製作業期間。</span><span class="sxs-lookup"><span data-stu-id="919ca-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="919ca-172">使用度量針對 Azure 檔案儲存體進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="919ca-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="919ca-173">Azure 儲存體分析現在支援 Azure 檔案儲存體的度量。</span><span class="sxs-lookup"><span data-stu-id="919ca-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="919ca-174">利用度量資料，您可以追蹤要求及診斷問題。</span><span class="sxs-lookup"><span data-stu-id="919ca-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="919ca-175">您可以啟用從 hello Azure 檔案儲存體度量[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="919ca-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="919ca-176">您也可以啟用以程式設計方式呼叫 hello hello REST API，透過設定檔案服務屬性作業，或其雷同 hello 儲存體用戶端程式庫中的其中一個度量。</span><span class="sxs-lookup"><span data-stu-id="919ca-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="919ca-177">hello，下列程式碼範例示範如何 toouse hello Azure 檔案儲存體的.NET tooenable 度量的儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="919ca-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="919ca-178">首先，新增下列 hello`using`指示詞 tooyour`Program.cs`檔案，另外 toothose 上述您新增：</span><span class="sxs-lookup"><span data-stu-id="919ca-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="919ca-179">請注意，Azure Blob、 Azure 資料表及 Azure 佇列時，使用共用的 hello `ServiceProperties` hello 中的型別`Microsoft.WindowsAzure.Storage.Shared.Protocol`命名空間，Azure 檔案儲存體使用自己的型別，hello `FileServiceProperties` hello 中的型別`Microsoft.WindowsAzure.Storage.File.Protocol`命名空間。</span><span class="sxs-lookup"><span data-stu-id="919ca-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="919ca-180">兩個命名空間必須參考從程式碼，不過，如下列程式碼 toocompile hello。</span><span class="sxs-lookup"><span data-stu-id="919ca-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

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

<span data-ttu-id="919ca-181">此外，您可以使用參照太[Azure 檔案儲存體疑難排解文章](storage-troubleshoot-file-connection-problems.md)的端對端疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="919ca-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="919ca-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="919ca-182">Next steps</span></span>
<span data-ttu-id="919ca-183">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="919ca-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="919ca-184">概念性文章和影片</span><span class="sxs-lookup"><span data-stu-id="919ca-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="919ca-185">Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統</span><span class="sxs-lookup"><span data-stu-id="919ca-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="919ca-186">如何 toouse Linux 的 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="919ca-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="919ca-187">檔案儲存體的工具支援</span><span class="sxs-lookup"><span data-stu-id="919ca-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="919ca-188">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="919ca-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="919ca-189">如何 toouse AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="919ca-189">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="919ca-190">使用 Azure CLI hello 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="919ca-190">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="919ca-191">針對 Azure 檔案儲存體的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="919ca-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="919ca-192">參考</span><span class="sxs-lookup"><span data-stu-id="919ca-192">Reference</span></span>
* [<span data-ttu-id="919ca-193">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="919ca-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="919ca-194">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="919ca-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="919ca-195">部落格文章</span><span class="sxs-lookup"><span data-stu-id="919ca-195">Blog posts</span></span>
* [<span data-ttu-id="919ca-196">Azure 檔案儲存體現已公開推出</span><span class="sxs-lookup"><span data-stu-id="919ca-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="919ca-197">Azure 檔案儲存體內部</span><span class="sxs-lookup"><span data-stu-id="919ca-197">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="919ca-198">Microsoft Azure 檔案服務簡介</span><span class="sxs-lookup"><span data-stu-id="919ca-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="919ca-199">持續性連線 tooMicrosoft Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="919ca-199">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
