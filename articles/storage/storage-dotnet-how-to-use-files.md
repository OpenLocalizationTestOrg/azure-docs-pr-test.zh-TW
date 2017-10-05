---
title: "使用 .NET 開發 Azure 檔案儲存體 | Microsoft Docs"
description: "了解如何開發使用 Azure 檔案儲存體來儲存檔案資料的 .NET 應用程式和服務。"
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
ms.openlocfilehash: e26da88ef1803d47d7286c5ae836ac9c041dadd1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="0c17c-103">使用 .NET 開發 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="0c17c-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="0c17c-104">本文將說明如何使用 .NET 程式碼管理 Azure 檔案儲存體。</span><span class="sxs-lookup"><span data-stu-id="0c17c-104">This article shows how to manage Azure File storage with .NET code.</span></span> <span data-ttu-id="0c17c-105">若要深入了解 Azure 檔案儲存體，請參閱 [Azure 檔案儲存體簡介](storage-files-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="0c17c-105">To learn more about Azure File storage, please see the [Introduction to Azure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="0c17c-106">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="0c17c-106">About this tutorial</span></span>
<span data-ttu-id="0c17c-107">本教學課程將示範使用 .NET 來開發使用 Azure 檔案儲存體來儲存檔案資料的應用程式和服務之基本概念。</span><span class="sxs-lookup"><span data-stu-id="0c17c-107">This tutorial will demonstrate the basics of using .NET to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="0c17c-108">在本教學課程中，我們將建立簡單的主控台應用程式，並說明如何執行 .NET 和 Azure 檔案儲存體的基本動作：</span><span class="sxs-lookup"><span data-stu-id="0c17c-108">In this tutorial, we will create a simple console application and show how to perform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="0c17c-109">取得檔案的內容</span><span class="sxs-lookup"><span data-stu-id="0c17c-109">Get the contents of a file</span></span>
* <span data-ttu-id="0c17c-110">設定檔案共用的配額 (大小上限)。</span><span class="sxs-lookup"><span data-stu-id="0c17c-110">Set the quota (maximum size) for the file share.</span></span>
* <span data-ttu-id="0c17c-111">為使用共用上所定義之共用存取原則的檔案建立共用存取簽章 (SAS 金鑰)。</span><span class="sxs-lookup"><span data-stu-id="0c17c-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>
* <span data-ttu-id="0c17c-112">將檔案複製到相同儲存體帳戶中的另一個檔案。</span><span class="sxs-lookup"><span data-stu-id="0c17c-112">Copy a file to another file in the same storage account.</span></span>
* <span data-ttu-id="0c17c-113">將檔案複製到相同儲存體帳戶中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="0c17c-113">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="0c17c-114">使用 Azure 儲存體度量進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0c17c-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="0c17c-115">由於 Azure 檔案儲存體可透過 SMB 存取，因此便可使用檔案 I/O 的標準 System.IO 類別撰寫簡單的應用程式以存取 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="0c17c-115">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard System.IO classes for File I/O.</span></span> <span data-ttu-id="0c17c-116">本文將說明如何撰寫使用 Azure 儲存體 .NET SDK 的應用程式，它會使用 [Azure 檔案儲存體 REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) 與 Azure 檔案儲存體通訊。</span><span class="sxs-lookup"><span data-stu-id="0c17c-116">This article will describe how to write applications that use the Azure Storage .NET SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span> 


## <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="0c17c-117">建立主控台應用程式並取得組件</span><span class="sxs-lookup"><span data-stu-id="0c17c-117">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="0c17c-118">在 Visual Studio 中，建立新的 Windows 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c17c-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="0c17c-119">下列步驟示範如何在 Visual Studio 2017 中建立主控台應用程式，但步驟類似其他版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0c17c-119">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="0c17c-120">選取 [檔案] > [新增] > [專案]</span><span class="sxs-lookup"><span data-stu-id="0c17c-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="0c17c-121">選取 [安裝] > [範本] > [Visual C#] > [Windows 傳統桌面]</span><span class="sxs-lookup"><span data-stu-id="0c17c-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="0c17c-122">選取 **主控台應用程式 (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="0c17c-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="0c17c-123">在 [名稱：] 欄位中輸入應用程式的名稱</span><span class="sxs-lookup"><span data-stu-id="0c17c-123">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="0c17c-124">選取 [確定]</span><span class="sxs-lookup"><span data-stu-id="0c17c-124">Select **OK**</span></span>

<span data-ttu-id="0c17c-125">本教學課程中的所有程式碼範例均可新增至您主控台應用程式的 `Program.cs` 檔案中的 `Main()` 方法。</span><span class="sxs-lookup"><span data-stu-id="0c17c-125">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="0c17c-126">您可以在任何類型的 .NET 應用程式 (包括 Azure 雲端服務或 Web 應用程式和桌面與行動應用程式) 中使用 Azure Storage Client Library。</span><span class="sxs-lookup"><span data-stu-id="0c17c-126">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="0c17c-127">在本指南中，為求簡化，我們會使用主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0c17c-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="0c17c-128">使用 NuGet 來安裝必要的封裝</span><span class="sxs-lookup"><span data-stu-id="0c17c-128">Use NuGet to install the required packages</span></span>
<span data-ttu-id="0c17c-129">您必須在您的專案中參考下列兩個套件，才能完成本教學課程︰</span><span class="sxs-lookup"><span data-stu-id="0c17c-129">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="0c17c-130">[適用於 .NET 的 Microsoft Azure 儲存體用戶端資源庫](https://www.nuget.org/packages/WindowsAzure.Storage/)︰此封裝可供以程式設計方式存取儲存體帳戶中的資料資源。</span><span class="sxs-lookup"><span data-stu-id="0c17c-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="0c17c-131">[適用於 .NET 的 Microsoft Azure Configuration Manager 程式庫](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)︰此套件提供一個類別，無論您的應用程式於何處執行，均可用來剖析組態檔中的連接字串。</span><span class="sxs-lookup"><span data-stu-id="0c17c-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="0c17c-132">您可以使用 NuGet 來取得這兩個封裝。</span><span class="sxs-lookup"><span data-stu-id="0c17c-132">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="0c17c-133">請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0c17c-133">Follow these steps:</span></span>

1. <span data-ttu-id="0c17c-134">在 [方案總管] 中以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 封裝]。</span><span class="sxs-lookup"><span data-stu-id="0c17c-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="0c17c-135">在線上搜尋 "WindowsAzure.Storage"，然後按一下 [安裝]  以安裝 Storage Client Library 與其相依項目。</span><span class="sxs-lookup"><span data-stu-id="0c17c-135">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="0c17c-136">在線上搜尋 "WindowsAzure.ConfigurationManager"，然後按一下 [安裝]  以安裝 Azure Configuration Manager。</span><span class="sxs-lookup"><span data-stu-id="0c17c-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="0c17c-137">將您的儲存體帳戶認證儲存到 app.config 檔案</span><span class="sxs-lookup"><span data-stu-id="0c17c-137">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="0c17c-138">接著，將您的認證儲存到專案的 app.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="0c17c-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="0c17c-139">編輯 app.config 檔案，使其看起來類似下列範例，並使用您的儲存體帳戶名稱來取代 `myaccount`，以及使用您的儲存體帳戶金鑰來取代 `mykey`。</span><span class="sxs-lookup"><span data-stu-id="0c17c-139">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> 最新版本的 Azure 儲存體模擬器不支援 Azure 檔案儲存體。 <span data-ttu-id="0c17c-141">您的連接字串必須以雲端中的 Azure 儲存體帳戶為目標，才能與 Azure 檔案儲存體搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0c17c-141">Your connection string must target an Azure Storage Account in the cloud to work with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="0c17c-142">新增 using 指示詞</span><span class="sxs-lookup"><span data-stu-id="0c17c-142">Add using directives</span></span>
<span data-ttu-id="0c17c-143">在 [方案總管] 中開啟 `Program.cs` 檔案，並在檔案的開頭處新增下列 using 指示詞。</span><span class="sxs-lookup"><span data-stu-id="0c17c-143">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a><span data-ttu-id="0c17c-144">以程式設計方式存取檔案共用</span><span class="sxs-lookup"><span data-stu-id="0c17c-144">Access the file share programmatically</span></span>
<span data-ttu-id="0c17c-145">接著，在 `Main()` 方法 (上述程式碼後面) 加入下列程式碼，以擷取連接字串。</span><span class="sxs-lookup"><span data-stu-id="0c17c-145">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="0c17c-146">此程式碼會取得稍早所建立檔案的參考，並將其內容輸出到主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="0c17c-146">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="0c17c-147">執行主控台應用程式以查看此輸出。</span><span class="sxs-lookup"><span data-stu-id="0c17c-147">Run the console application to see the output.</span></span>

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="0c17c-148">設定檔案共用的大小上限</span><span class="sxs-lookup"><span data-stu-id="0c17c-148">Set the maximum size for a file share</span></span>
<span data-ttu-id="0c17c-149">從 Azure 儲存體用戶端程式庫 5.x 版開始，您可以設定以 GB 為單位的檔案共用配額 (或大小上限)。</span><span class="sxs-lookup"><span data-stu-id="0c17c-149">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="0c17c-150">您也可以檢查有多少資料目前儲存在共用上。</span><span class="sxs-lookup"><span data-stu-id="0c17c-150">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="0c17c-151">藉由設定共用的配額，您可以限制儲存在共用上的檔案大小總計。</span><span class="sxs-lookup"><span data-stu-id="0c17c-151">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="0c17c-152">如果共用上的檔案大小總計超過共用上設定的配額，則用戶端將無法增加現有檔案的大小或建立新的檔案 (除非這些檔案為空白)。</span><span class="sxs-lookup"><span data-stu-id="0c17c-152">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="0c17c-153">下列範例示範如何檢查共用的目前使用狀況，以及如何設定共用的配額。</span><span class="sxs-lookup"><span data-stu-id="0c17c-153">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="0c17c-154">產生檔案或檔案共用的共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="0c17c-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="0c17c-155">從 Azure 儲存體用戶端程式庫 5.x 版開始，您可以產生檔案共用或個別檔案的共用存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="0c17c-155">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="0c17c-156">您也可以在檔案共用上建立共用存取原則，以管理共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="0c17c-156">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="0c17c-157">建議您建立共用存取原則，因為如果必須洩漏 SAS，它提供了一種撤銷 SAS 的方式。</span><span class="sxs-lookup"><span data-stu-id="0c17c-157">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="0c17c-158">下列範例會在共用上建立共用存取原則，然後使用該原則為共用中檔案上的 SAS 提供條件約束。</span><span class="sxs-lookup"><span data-stu-id="0c17c-158">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="0c17c-159">如需建立與使用共用存取簽章的詳細資訊，請參閱[共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 和[透過 Azure Blob 建立與使用 SAS](storage-dotnet-shared-access-signature-part-2.md)。</span><span class="sxs-lookup"><span data-stu-id="0c17c-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="0c17c-160">複製檔案</span><span class="sxs-lookup"><span data-stu-id="0c17c-160">Copy files</span></span>
<span data-ttu-id="0c17c-161">從 Azure 儲存體用戶端程式庫 5.x 版開始，您可以將檔案複製到另一個檔案、將檔案複製到 Blob 或將 Blob 複製到檔案。</span><span class="sxs-lookup"><span data-stu-id="0c17c-161">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="0c17c-162">在後續各節中，我們將示範如何以程式設計方式執行這些複製作業。</span><span class="sxs-lookup"><span data-stu-id="0c17c-162">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="0c17c-163">您也可以使用 AzCopy 將檔案複製到另一個檔案，或將 Blob 複製到檔案或反向操作。</span><span class="sxs-lookup"><span data-stu-id="0c17c-163">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="0c17c-164">請參閱 [使用 AzCopy 命令列公用程式傳輸資料](storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="0c17c-164">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0c17c-165">如果要將 Blob 複製到檔案，或將檔案複製到 Blob，您必須使用共用存取簽章 (SAS) 驗證來源物件，即使是在相同的儲存體帳戶內進行複製也一樣。</span><span class="sxs-lookup"><span data-stu-id="0c17c-165">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="0c17c-166">**將檔案複製到另一個檔案** 下列範例會將檔案複製到相同共用中的另一個檔案。</span><span class="sxs-lookup"><span data-stu-id="0c17c-166">**Copy a file to another file** The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="0c17c-167">由於此複製作業是在相同儲存體帳戶中的檔案間進行複製，所以您可以使用共用金鑰驗證執行複製。</span><span class="sxs-lookup"><span data-stu-id="0c17c-167">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="0c17c-168">**將檔案複製到 Blob** 下列範例會建立檔案，並將其複製到相同儲存體帳戶內的 Blob。</span><span class="sxs-lookup"><span data-stu-id="0c17c-168">**Copy a file to a blob** The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="0c17c-169">此範例會建立來源檔案的 SAS，供服務用來在複製作業期間驗證來源檔案存取權。</span><span class="sxs-lookup"><span data-stu-id="0c17c-169">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="0c17c-170">您可以用相同方式將 Blob 複製到檔案。</span><span class="sxs-lookup"><span data-stu-id="0c17c-170">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="0c17c-171">如果來源物件為 Blob，則請建立 SAS，以便在複製作業期間驗證該 Blob 存取權。</span><span class="sxs-lookup"><span data-stu-id="0c17c-171">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="0c17c-172">使用度量針對 Azure 檔案儲存體進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0c17c-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="0c17c-173">Azure 儲存體分析現在支援 Azure 檔案儲存體的度量。</span><span class="sxs-lookup"><span data-stu-id="0c17c-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="0c17c-174">利用度量資料，您可以追蹤要求及診斷問題。</span><span class="sxs-lookup"><span data-stu-id="0c17c-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="0c17c-175">您可以透過 [Azure 入口網站](https://portal.azure.com)啟用 Azure 檔案儲存體度量。</span><span class="sxs-lookup"><span data-stu-id="0c17c-175">You can enable metrics for Azure File storage from the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="0c17c-176">您也可以透過 REST API 或儲存體用戶端程式庫中的其中一個同類工具來呼叫設定檔案服務屬性作業，以程式設計方式啟用度量。</span><span class="sxs-lookup"><span data-stu-id="0c17c-176">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>


<span data-ttu-id="0c17c-177">下列程式碼範例會示範如何使用適用於 .NET 的儲存體用戶端程式庫，啟用 Azure 檔案儲存體的計量。</span><span class="sxs-lookup"><span data-stu-id="0c17c-177">The following code example shows how to use the Storage Client Library for .NET to enable metrics for Azure File storage.</span></span>

<span data-ttu-id="0c17c-178">首先，將下列 `using` 指示詞新增您的 `Program.cs` 檔案中，連同上述所新增的陳述式︰</span><span class="sxs-lookup"><span data-stu-id="0c17c-178">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="0c17c-179">請注意，雖然 Azure Blob、表格以及 Azure 佇列會在 `Microsoft.WindowsAzure.Storage.Shared.Protocol` 命名空間中使用共用的 `ServiceProperties` 類型，但 Azure 檔案儲存體會使用自己的類型，其會在 `Microsoft.WindowsAzure.Storage.File.Protocol` 命名空間中使用 `FileServiceProperties` 類型。</span><span class="sxs-lookup"><span data-stu-id="0c17c-179">Note that while Azure Blobs, Azure Table, and Azure Queues use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="0c17c-180">不過，這兩個命名空間都必須從您的程式碼加以參考，以供下列程式碼進行編譯。</span><span class="sxs-lookup"><span data-stu-id="0c17c-180">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
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

// Read the metrics properties we just set.
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

<span data-ttu-id="0c17c-181">此外，您可以參考 [Azure 檔案儲存體疑難排解文章](storage-troubleshoot-file-connection-problems.md)以取得端對端疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="0c17c-181">Also, you can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c17c-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c17c-182">Next steps</span></span>
<span data-ttu-id="0c17c-183">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0c17c-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="0c17c-184">概念性文章和影片</span><span class="sxs-lookup"><span data-stu-id="0c17c-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="0c17c-185">Azure 檔案儲存體：適用於 Windows 和 Linux 的無摩擦雲端 SMB 檔案系統</span><span class="sxs-lookup"><span data-stu-id="0c17c-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="0c17c-186">如何搭配使用 Azure 檔案儲存體與 Linux</span><span class="sxs-lookup"><span data-stu-id="0c17c-186">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="0c17c-187">檔案儲存體的工具支援</span><span class="sxs-lookup"><span data-stu-id="0c17c-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="0c17c-188">搭配使用 Azure PowerShell 與 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0c17c-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="0c17c-189">如何搭配使用 AzCopy 與 Microsoft Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0c17c-189">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="0c17c-190">使用 Azure CLI 搭配 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0c17c-190">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="0c17c-191">針對 Azure 檔案儲存體的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="0c17c-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="0c17c-192">參考</span><span class="sxs-lookup"><span data-stu-id="0c17c-192">Reference</span></span>
* [<span data-ttu-id="0c17c-193">Storage Client Library for .NET 參考資料</span><span class="sxs-lookup"><span data-stu-id="0c17c-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="0c17c-194">檔案服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="0c17c-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="0c17c-195">部落格文章</span><span class="sxs-lookup"><span data-stu-id="0c17c-195">Blog posts</span></span>
* [<span data-ttu-id="0c17c-196">Azure 檔案儲存體現已公開推出</span><span class="sxs-lookup"><span data-stu-id="0c17c-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="0c17c-197">Azure 檔案儲存體內部</span><span class="sxs-lookup"><span data-stu-id="0c17c-197">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="0c17c-198">Microsoft Azure 檔案服務簡介</span><span class="sxs-lookup"><span data-stu-id="0c17c-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="0c17c-199">保留與 Microsoft Azure 檔案儲存體的連線</span><span class="sxs-lookup"><span data-stu-id="0c17c-199">Persisting connections to Microsoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)