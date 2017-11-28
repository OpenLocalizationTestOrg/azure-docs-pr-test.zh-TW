---
title: "aaaCreate，使用 Azure Blob 儲存體的共用的存取簽章 (SAS) |Microsoft 文件"
description: "本教學課程告訴您如何 toocreate 共用存取簽章用於使用 Blob 儲存體，以及如何 tooconsume 中用戶端應用程式。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="e14b5-103">共用存取簽章，第 2 部分：透過 Blob 儲存體來建立與使用 SAS</span><span class="sxs-lookup"><span data-stu-id="e14b5-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="e14b5-104">[第 1 部分](storage-dotnet-shared-access-signature-part-1.md)探討了共用存取簽章 (SAS)，並說明使用它們的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="e14b5-104">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="e14b5-105">第 2 部分會顯示您如何 toogenerate，然後使用共用存取簽章使用 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e14b5-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="e14b5-106">hello 範例以 C# 所撰寫，並使用適用於.NET 的 hello Azure 儲存體用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="e14b5-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="e14b5-107">此教學課程中的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="e14b5-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="e14b5-108">在容器上產生共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="e14b5-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="e14b5-109">在 blob 上產生共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="e14b5-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="e14b5-110">容器資源上建立的預存的存取原則 toomanage 簽章</span><span class="sxs-lookup"><span data-stu-id="e14b5-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="e14b5-111">在用戶端應用程式中測試 hello 共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="e14b5-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="e14b5-112">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="e14b5-112">About this tutorial</span></span>
<span data-ttu-id="e14b5-113">在本教學課程中，我們會建立兩個主控台應用程式，以示範如何為容器和 Blob 建立及使用共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="e14b5-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="e14b5-114">**應用程式 1**: hello 管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="e14b5-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="e14b5-115">為容器和 Blob 產生共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="e14b5-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="e14b5-116">在原始程式碼中包括 hello 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="e14b5-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="e14b5-117">**應用程式 2**: hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="e14b5-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="e14b5-118">存取容器和 blob 資源使用 hello 共用存取簽章建立 hello 第一個應用程式。</span><span class="sxs-lookup"><span data-stu-id="e14b5-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="e14b5-119">它會使用唯一 hello 共用的存取簽章 tooaccess 容器和 blob 資源--*不*包含 hello 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="e14b5-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="e14b5-120">第 1 部分： 建立主控台應用程式 toogenerate 共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="e14b5-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="e14b5-121">首先，確認您擁有 hello Azure 儲存體用戶端程式庫.NET 安裝。</span><span class="sxs-lookup"><span data-stu-id="e14b5-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="e14b5-122">您可以安裝 hello [NuGet 封裝](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet 封裝")包含 hello hello 用戶端程式庫的最新組件。</span><span class="sxs-lookup"><span data-stu-id="e14b5-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="e14b5-123">這是建議使用的方法，可確保您擁有 hello 最近修正的 hello。</span><span class="sxs-lookup"><span data-stu-id="e14b5-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="e14b5-124">您也可以在 hello hello 最新版本的一部分下載 hello 用戶端程式庫[Azure SDK for.NET](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="e14b5-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="e14b5-125">在 Visual Studio 中，建立新的 Windows 主控台應用程式，並將它命名為 **GenerateSharedAccessSignatures**。</span><span class="sxs-lookup"><span data-stu-id="e14b5-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="e14b5-126">將參考加入太[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)和[WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/)使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="e14b5-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="e14b5-127">使用 hello [NuGet 套件管理員](https://docs.nuget.org/consume/installing-nuget)Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="e14b5-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="e14b5-128">選取 [專案] > [管理 NuGet 套件]，線上搜尋每個套件 (Microsoft.WindowsAzure.ConfigurationManager 和 WindowsAzure.Storage)，並加以安裝。</span><span class="sxs-lookup"><span data-stu-id="e14b5-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="e14b5-129">或者，在您安裝的 hello Azure SDK 中尋找這些組件，並加入參考 toothem:</span><span class="sxs-lookup"><span data-stu-id="e14b5-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="e14b5-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="e14b5-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="e14b5-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="e14b5-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="e14b5-132">在 hello hello Program.cs 檔案頂端，加入下列 hello**使用**指示詞：</span><span class="sxs-lookup"><span data-stu-id="e14b5-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="e14b5-133">編輯 hello app.config 檔案，使其包含連接字串指向 tooyour 儲存體帳戶的組態設定。</span><span class="sxs-lookup"><span data-stu-id="e14b5-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="e14b5-134">您的 app.config 檔案看起來類似 toothis 其中一個：</span><span class="sxs-lookup"><span data-stu-id="e14b5-134">Your app.config file should look similar toothis one:</span></span>

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="e14b5-135">為容器產生共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="e14b5-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="e14b5-136">與 toobegin，我們方法 toogenerate 共用的存取簽章上加入新的容器。</span><span class="sxs-lookup"><span data-stu-id="e14b5-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="e14b5-137">在此情況下，hello 簽章不是預存的存取原則相關聯，因此它會在 hello URI hello 資訊指出其到期時間和 hello 權限授與。</span><span class="sxs-lookup"><span data-stu-id="e14b5-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="e14b5-138">首先，加入程式碼 toohello **main （)**方法 tooauthenticate 存取 tooyour 儲存體帳戶，並建立新的容器：</span><span class="sxs-lookup"><span data-stu-id="e14b5-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

<span data-ttu-id="e14b5-139">接下來，加入的方法，會產生 hello hello 容器的共用的存取簽章，並傳回 hello 簽章 URI:</span><span class="sxs-lookup"><span data-stu-id="e14b5-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="e14b5-140">加入下列行底部 hello hello hello **main （)**方法之前 hello 太呼叫**main**，toocall **GetContainerSasUri()**和寫入 hello簽章 URI toohello 主控台視窗：</span><span class="sxs-lookup"><span data-stu-id="e14b5-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="e14b5-141">編譯並執行 toooutput hello 共用的存取簽章 URI hello 新容器。</span><span class="sxs-lookup"><span data-stu-id="e14b5-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="e14b5-142">hello URI 將類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="e14b5-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="e14b5-143">一旦您已經執行 hello 程式碼，您建立 hello 容器 hello 共用的存取簽章才有效 hello 未來 24 小時內。</span><span class="sxs-lookup"><span data-stu-id="e14b5-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="e14b5-144">hello 簽章授與用戶端 hello 容器與 toowrite 新 blob toohello 容器中的權限 toolist blob。</span><span class="sxs-lookup"><span data-stu-id="e14b5-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="e14b5-145">產生 Blob 的共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="e14b5-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="e14b5-146">接下來，我們會撰寫類似的程式碼 toocreate hello 容器內的新 blob，並產生共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="e14b5-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="e14b5-147">此共用的存取簽章不是相關聯的預存的存取原則，使其包含在 hello URI 中的 hello 開始時間、 到期時間和權限資訊。</span><span class="sxs-lookup"><span data-stu-id="e14b5-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="e14b5-148">加入新的方法，建立新的 blob 寫入某些文字 tooit，則會產生共用的存取簽章和傳回 hello 簽章 URI:</span><span class="sxs-lookup"><span data-stu-id="e14b5-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="e14b5-149">在 hello 底部 hello **main （)**方法，加入下列行 toocall hello **GetBlobSasUri()**hello 太呼叫之前，先**main**，和寫入共用的 hello存取簽章 URI toohello 主控台視窗：</span><span class="sxs-lookup"><span data-stu-id="e14b5-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="e14b5-150">編譯並執行 toooutput hello 共用的存取簽章 URI hello 新 blob。</span><span class="sxs-lookup"><span data-stu-id="e14b5-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="e14b5-151">hello URI 將類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="e14b5-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="e14b5-152">Hello 容器上建立的預存的存取原則</span><span class="sxs-lookup"><span data-stu-id="e14b5-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="e14b5-153">現在讓我們來建立 hello 容器，將會定義任何與其相關聯的共用的存取簽章的 hello 條件約束上的 預存的存取原則。</span><span class="sxs-lookup"><span data-stu-id="e14b5-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="e14b5-154">在 hello 前一個範例中，我們指定 hello 開始時間 （以隱含或明確），hello 到期時間和 hello hello 權限的共用存取簽章本身的 URI。</span><span class="sxs-lookup"><span data-stu-id="e14b5-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="e14b5-155">在 hello 遵循範例，我們指定這些 hello 預存存取原則，而非 hello 共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="e14b5-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="e14b5-156">可讓我們 toochange 這些條件約束，而不重新發出 hello 共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="e14b5-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="e14b5-157">很可能 toohave 一或多個 hello hello 共用的存取簽章，條件約束和 hello hello 預存存取原則的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="e14b5-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="e14b5-158">不過，您可以僅指定 hello 開始時間、 到期時間和權限在某一個位置或其他 hello。</span><span class="sxs-lookup"><span data-stu-id="e14b5-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="e14b5-159">例如，您無法在 hello 共用的存取簽章上指定的權限，然後也指定這些 hello 預存存取原則。</span><span class="sxs-lookup"><span data-stu-id="e14b5-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="e14b5-160">當您將預存的存取原則 tooa 容器時，您必須取得 hello 容器的現有權限，新增 hello 新存取原則，然後設定 hello 容器的權限。</span><span class="sxs-lookup"><span data-stu-id="e14b5-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="e14b5-161">加入新的方法，在容器上建立新的預存的存取原則，並傳回 hello hello 原則名稱：</span><span class="sxs-lookup"><span data-stu-id="e14b5-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="e14b5-162">在 hello 底部 hello **main （)**方法之前 hello 太呼叫**main**，加入下列的 hello 行 toofirst 清除任何現有的存取原則，然後呼叫 hello **CreateSharedAccessPolicy()**方法：</span><span class="sxs-lookup"><span data-stu-id="e14b5-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="e14b5-163">當您清除 hello 在容器上的存取原則時，您必須先取得 hello 容器的現有權限，然後清除 hello 權限，然後再次設定 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="e14b5-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="e14b5-164">產生共用的存取簽章上使用存取原則的 hello 容器的 URI</span><span class="sxs-lookup"><span data-stu-id="e14b5-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="e14b5-165">接下來，我們會建立另一個 hello 容器我們稍早建立的共用的存取簽章，但這次我們關聯 hello 簽章與我們建立 hello 前一個範例中的 hello 預存存取原則。</span><span class="sxs-lookup"><span data-stu-id="e14b5-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="e14b5-166">加入新的方法 toogenerate hello 容器的另一個共用的存取簽章：</span><span class="sxs-lookup"><span data-stu-id="e14b5-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="e14b5-167">在 hello 底部 hello **main （)**方法之前 hello 太呼叫**main**，新增下列幾行 toocall hello hello **GetContainerSasUriWithPolicy**方法:</span><span class="sxs-lookup"><span data-stu-id="e14b5-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="e14b5-168">產生共用存取簽章 URI 上 hello Blob，所使用的存取原則</span><span class="sxs-lookup"><span data-stu-id="e14b5-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="e14b5-169">最後，我們會加入類似的方法 toocreate 另一個 blob，並產生共用的存取簽章與預存的存取原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="e14b5-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="e14b5-170">加入新的方法 toocreate blob，並產生共用的存取簽章：</span><span class="sxs-lookup"><span data-stu-id="e14b5-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="e14b5-171">在 hello 底部 hello **main （)**方法之前 hello 太呼叫**main**，新增下列幾行 toocall hello hello **GetBlobSasUriWithPolicy**方法：</span><span class="sxs-lookup"><span data-stu-id="e14b5-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="e14b5-172">hello **main （)**方法現在看起來應該像這樣失真。</span><span class="sxs-lookup"><span data-stu-id="e14b5-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="e14b5-173">執行 toowrite hello 共用的存取簽章 Uri toohello 主控台視窗中，然後複製並貼入文字檔案，供 hello 本教學課程的第二個組件中使用。</span><span class="sxs-lookup"><span data-stu-id="e14b5-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="e14b5-174">當您執行 hello GenerateSharedAccessSignatures 主控台應用程式時，您會看到類似 toohello 下列輸出。</span><span class="sxs-lookup"><span data-stu-id="e14b5-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="e14b5-175">這些是您在 hello 教學課程的第 2 部分中使用的 hello 共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="e14b5-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="e14b5-176">第 2 部分︰ 建立主控台應用程式 tootest hello 共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="e14b5-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="e14b5-177">tootest hello 共用存取簽章建立 hello 前一個範例中，我們會建立使用 hello 簽章 tooperform 作業 hello 容器和 blob 上的第二個主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e14b5-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="e14b5-178">如果您完成 hello hello 教學課程的第一個部分後已過了超過 24 小時，您所產生的 hello 簽章將不再有效。</span><span class="sxs-lookup"><span data-stu-id="e14b5-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="e14b5-179">在此情況下，您要執行 hello 程式碼，在第一個主控台應用程式 toogenerate hello 的 hello hello 教學課程的第二個組件中使用全新的共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="e14b5-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="e14b5-180">在 Visual Studio 中，建立新的 Windows 主控台應用程式，並將它命名為 **ConsumeSharedAccessSignatures**。</span><span class="sxs-lookup"><span data-stu-id="e14b5-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="e14b5-181">將參考加入太[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)和[WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/)、 跟之前一樣。</span><span class="sxs-lookup"><span data-stu-id="e14b5-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="e14b5-182">在 hello hello Program.cs 檔案頂端，加入下列 hello**使用**指示詞：</span><span class="sxs-lookup"><span data-stu-id="e14b5-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="e14b5-183">中的 hello hello 主體**main （)**方法，加入下列字串常數、 變更您在 hello 教學課程的第 1 部分中產生其值 toohello 共用存取簽章的 hello。</span><span class="sxs-lookup"><span data-stu-id="e14b5-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="e14b5-184">新增使用共用的存取簽章方法 tootry 容器作業</span><span class="sxs-lookup"><span data-stu-id="e14b5-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="e14b5-185">接下來，我們加入測試 hello 容器使用的共用的存取簽章某些容器作業的方法。</span><span class="sxs-lookup"><span data-stu-id="e14b5-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="e14b5-186">hello 共用的存取簽章是使用的 tooreturn 驗證存取 toohello 容器，根據 hello 簽章單獨參考 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="e14b5-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="e14b5-187">加入下列方法 tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="e14b5-187">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="e14b5-188">更新 hello **main （)**方法 toocall **UseContainerSAS()**與 hello 這兩個共用存取簽章您 hello 容器建立：</span><span class="sxs-lookup"><span data-stu-id="e14b5-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="e14b5-189">新增使用共用的存取簽章方法 tootry blob 作業</span><span class="sxs-lookup"><span data-stu-id="e14b5-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="e14b5-190">最後，我們加入測試某些 hello blob 上使用共用的存取簽章的 blob 作業的方法。</span><span class="sxs-lookup"><span data-stu-id="e14b5-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="e14b5-191">在此情況下，我們使用 hello 建構函式**CloudBlockBlob(String)**，並傳入 hello 共用的存取簽章，tooreturn 參考 toohello blob。</span><span class="sxs-lookup"><span data-stu-id="e14b5-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="e14b5-192">沒有其他的驗證是必要項;它根據單獨 hello 簽章。</span><span class="sxs-lookup"><span data-stu-id="e14b5-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="e14b5-193">加入下列方法 tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="e14b5-193">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="e14b5-194">更新 hello **main （)**方法 toocall **UseBlobSAS()**與 hello 這兩個共用存取簽章，您建立 hello blob 上：</span><span class="sxs-lookup"><span data-stu-id="e14b5-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="e14b5-195">執行 hello 主控台應用程式，並觀察 hello 輸出 toosee 允許的作業的簽章。</span><span class="sxs-lookup"><span data-stu-id="e14b5-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="e14b5-196">hello 主控台視窗中的 hello 輸出看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="e14b5-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="e14b5-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e14b5-197">Next Steps</span></span>

* [<span data-ttu-id="e14b5-198">共用存取簽章，第 1 部分： 了解 SAS 模型 hello</span><span class="sxs-lookup"><span data-stu-id="e14b5-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="e14b5-199">管理匿名讀取權限 toocontainers 和 blob</span><span class="sxs-lookup"><span data-stu-id="e14b5-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="e14b5-200">使用共用存取簽章 (REST API) 來委派存取權</span><span class="sxs-lookup"><span data-stu-id="e14b5-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="e14b5-201">資料表與佇列 SAS 簡介</span><span class="sxs-lookup"><span data-stu-id="e14b5-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
