---
title: "透過 Azure Blob 儲存體來建立和使用共用存取簽章 (SAS) | Microsoft Docs"
description: "本教學課程說明如何建立搭配 Blob 儲存體使用的共用存取簽章，以及如何在用戶端應用程式中使用共用存取簽章。"
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
ms.openlocfilehash: ba78dd2bbcc68ffffeba59b1623891126baf656f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="cc213-103">共用存取簽章，第 2 部分：透過 Blob 儲存體來建立與使用 SAS</span><span class="sxs-lookup"><span data-stu-id="cc213-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="cc213-104">[第 1 部分](storage-dotnet-shared-access-signature-part-1.md)探討了共用存取簽章 (SAS)，並說明使用它們的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="cc213-104">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="cc213-105">第 2 部分顯示如何使用 Blob 儲存體產生共用存取簽章並使用。</span><span class="sxs-lookup"><span data-stu-id="cc213-105">Part 2 shows you how to generate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="cc213-106">這些範例均以 C# 撰寫，並使用 Azure Storage Client Library for .NET。</span><span class="sxs-lookup"><span data-stu-id="cc213-106">The examples are written in C# and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="cc213-107">本教學課程中的範例會：</span><span class="sxs-lookup"><span data-stu-id="cc213-107">The examples in this tutorial:</span></span>

* <span data-ttu-id="cc213-108">在容器上產生共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="cc213-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="cc213-109">在 blob 上產生共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="cc213-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="cc213-110">建立預存存取原則，以管理容器資源上的簽章</span><span class="sxs-lookup"><span data-stu-id="cc213-110">Create a stored access policy to manage signatures on a container's resources</span></span>
* <span data-ttu-id="cc213-111">在用戶端應用程式中測試共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="cc213-111">Test the shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="cc213-112">關於本教學課程</span><span class="sxs-lookup"><span data-stu-id="cc213-112">About this tutorial</span></span>
<span data-ttu-id="cc213-113">在本教學課程中，我們會建立兩個主控台應用程式，以示範如何為容器和 Blob 建立及使用共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="cc213-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="cc213-114">**應用程式 1**︰管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc213-114">**Application 1**: The management application.</span></span> <span data-ttu-id="cc213-115">為容器和 Blob 產生共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="cc213-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="cc213-116">在原始程式碼中包含儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="cc213-116">Includes the storage account access key in source code.</span></span>

<span data-ttu-id="cc213-117">**應用程式 2**︰用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc213-117">**Application 2**: The client application.</span></span> <span data-ttu-id="cc213-118">使用第一個應用程式所建立的共用存取簽章，來存取容器及 Blob 資源。</span><span class="sxs-lookup"><span data-stu-id="cc213-118">Accesses container and blob resources using the shared access signatures created with the first application.</span></span> <span data-ttu-id="cc213-119">僅使用共用存取簽章來存取容器及 Blob 資源--它「不會」包含儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="cc213-119">Uses only the shared access signatures to access container and blob resources--it does *not* include the storage account access key.</span></span>

## <a name="part-1-create-a-console-application-to-generate-shared-access-signatures"></a><span data-ttu-id="cc213-120">第 1 部份：建立主控台應用程式以產生共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="cc213-120">Part 1: Create a console application to generate shared access signatures</span></span>
<span data-ttu-id="cc213-121">首先，請確定您已安裝 Azure Storage Client Library for .NET。</span><span class="sxs-lookup"><span data-stu-id="cc213-121">First, ensure that you have the Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="cc213-122">您可以安裝含有最新用戶端程式庫組件的 [NuGet 套件](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet 套件")。</span><span class="sxs-lookup"><span data-stu-id="cc213-122">You can install the [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing the most up-to-date assemblies for the client library.</span></span> <span data-ttu-id="cc213-123">建議您這麼做，以確保您會擁有最新的修正程式。</span><span class="sxs-lookup"><span data-stu-id="cc213-123">This is the recommended method for ensuring that you have the most recent fixes.</span></span> <span data-ttu-id="cc213-124">您也可以在最新版 [Azure SDK for .NET](https://azure.microsoft.com/downloads/)中一起下載用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="cc213-124">You can also download the client library as part of the most recent version of the [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="cc213-125">在 Visual Studio 中，建立新的 Windows 主控台應用程式，並將它命名為 **GenerateSharedAccessSignatures**。</span><span class="sxs-lookup"><span data-stu-id="cc213-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="cc213-126">使用下列其中一種方法，新增對 [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) 及 [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) 的參照：</span><span class="sxs-lookup"><span data-stu-id="cc213-126">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of the following approaches:</span></span>

* <span data-ttu-id="cc213-127">在 Visual Studio 中使用 [NuGet 套件管理員](https://docs.nuget.org/consume/installing-nuget)。</span><span class="sxs-lookup"><span data-stu-id="cc213-127">Use the [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="cc213-128">選取 [專案] > [管理 NuGet 套件]，線上搜尋每個套件 (Microsoft.WindowsAzure.ConfigurationManager 和 WindowsAzure.Storage)，並加以安裝。</span><span class="sxs-lookup"><span data-stu-id="cc213-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="cc213-129">或者，在您的 Azure SDK 安裝中找到這些組件，並新增對它們的參照：</span><span class="sxs-lookup"><span data-stu-id="cc213-129">Alternatively, locate these assemblies in your installation of the Azure SDK and add references to them:</span></span>
  * <span data-ttu-id="cc213-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="cc213-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="cc213-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="cc213-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="cc213-132">在 Program.cs 檔的頂端，新增下列 **using** 指示詞：</span><span class="sxs-lookup"><span data-stu-id="cc213-132">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="cc213-133">編輯 app.config 檔，使它包含的組態設定具有指向您儲存體帳戶的連接字串。</span><span class="sxs-lookup"><span data-stu-id="cc213-133">Edit the app.config file so that it contains a configuration setting with a connection string that points to your storage account.</span></span> <span data-ttu-id="cc213-134">您的 app.config 檔案應該看起來類似如下：</span><span class="sxs-lookup"><span data-stu-id="cc213-134">Your app.config file should look similar to this one:</span></span>

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="cc213-135">為容器產生共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="cc213-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="cc213-136">一開始，我們會新增方法以在新容器上產生共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="cc213-136">To begin with, we add a method to generate a shared access signature on a new container.</span></span> <span data-ttu-id="cc213-137">在此情況中，簽章不與預存存取原則相關，因此它在 URI 上攜帶了資訊，以指出其到期時間與授與的權限。</span><span class="sxs-lookup"><span data-stu-id="cc213-137">In this case, the signature is not associated with a stored access policy, so it carries on the URI the information indicating its expiry time and the permissions it grants.</span></span>

<span data-ttu-id="cc213-138">首先，將程式碼新增至 **Main()** 方法，以驗證對儲存體帳戶的存取，並建立新的容器：</span><span class="sxs-lookup"><span data-stu-id="cc213-138">First, add code to the **Main()** method to authenticate access to your storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls to the methods created below here...

    //Require user input before closing the console window.
    Console.ReadLine();
}
```

<span data-ttu-id="cc213-139">接下來，新增方法以產生容器的共用存取簽章，並傳回簽章 URI：</span><span class="sxs-lookup"><span data-stu-id="cc213-139">Next, add a method that generates the shared access signature for the container and returns the signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set the expiry time and permissions for the container.
    //In this case no start time is specified, so the shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="cc213-140">在 **Main()** 方法的底部，對 **Console.ReadLine()** 進行呼叫之前，新增下列幾行，以呼叫 **GetContainerSasUri()** 並將簽章 URI 寫到主控台視窗：</span><span class="sxs-lookup"><span data-stu-id="cc213-140">Add the following lines at the bottom of the **Main()** method, before the call to **Console.ReadLine()**, to call **GetContainerSasUri()** and write the signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for the container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="cc213-141">編譯並執行以輸出新容器的共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="cc213-141">Compile and run to output the shared access signature URI for the new container.</span></span> <span data-ttu-id="cc213-142">URI 會類似下面範例：</span><span class="sxs-lookup"><span data-stu-id="cc213-142">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="cc213-143">在執行程式碼之後，您為容器建立的共用存取簽章將在接下來的 24 小時內有效。</span><span class="sxs-lookup"><span data-stu-id="cc213-143">Once you have run the code, the shared access signature you created for the container will be valid for the next 24 hours.</span></span> <span data-ttu-id="cc213-144">簽章會授與用戶端權限以列出容器中的 Blob，以及將新的 Blob 寫入容器。</span><span class="sxs-lookup"><span data-stu-id="cc213-144">The signature grants a client permission to list blobs in the container and to write new blobs to the container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="cc213-145">產生 Blob 的共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="cc213-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="cc213-146">接下來，我們會撰寫類似的程式碼以在容器內建立新的 Blob，並為它產生共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="cc213-146">Next, we write similar code to create a new blob within the container and generate a shared access signature for it.</span></span> <span data-ttu-id="cc213-147">此共用存取簽章不與預存存取原則相關，因此它在 URI 中包含了開始時間、到期時間及權限資訊。</span><span class="sxs-lookup"><span data-stu-id="cc213-147">This shared access signature is not associated with a stored access policy, so it includes the start time, expiry time, and permission information in the URI.</span></span>

<span data-ttu-id="cc213-148">新增新方法以建立新的 Blob 並在其中寫入一些文字，然後產生共用存取簽章並傳回簽章 URI：</span><span class="sxs-lookup"><span data-stu-id="cc213-148">Add a new method that creates a new blob and writes some text to it, then generates a shared access signature and returns the signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set the expiry time and permissions for the blob.
    //In this case, the start time is specified as a few minutes in the past, to mitigate clock skew.
    //The shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the blob, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="cc213-149">在 **Main()** 方法的底部，對 **Console.ReadLine()** 的呼叫之前，新增下列幾行，以呼叫 **GetBlobSasUri()** 並將共用存取簽章 URI 寫到主控台視窗：</span><span class="sxs-lookup"><span data-stu-id="cc213-149">At the bottom of the **Main()** method, add the following lines to call **GetBlobSasUri()**, before the call to **Console.ReadLine()**, and write the shared access signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="cc213-150">編譯並執行以輸出新 blob 的共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="cc213-150">Compile and run to output the shared access signature URI for the new blob.</span></span> <span data-ttu-id="cc213-151">URI 會類似下面範例：</span><span class="sxs-lookup"><span data-stu-id="cc213-151">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-the-container"></a><span data-ttu-id="cc213-152">在容器上建立預存存取原則</span><span class="sxs-lookup"><span data-stu-id="cc213-152">Create a stored access policy on the container</span></span>
<span data-ttu-id="cc213-153">現在，讓我們在容器上建立預存存取原則，這將為與它相關的任何共用存取簽章定義限制。</span><span class="sxs-lookup"><span data-stu-id="cc213-153">Now let's create a stored access policy on the container, which will define the constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="cc213-154">在前面的範例中，我們指定了開始時間 (隱含或明確)、到期時間，以及對共用存取簽章 URI 本身的權限。</span><span class="sxs-lookup"><span data-stu-id="cc213-154">In the previous examples, we specified the start time (implicitly or explicitly), the expiry time, and the permissions on the shared access signature URI itself.</span></span> <span data-ttu-id="cc213-155">在接下來的範例中，我們會在預存存取原則上指定這些，而不在共用存取簽章上指定。</span><span class="sxs-lookup"><span data-stu-id="cc213-155">In the following examples, we specify these on the stored access policy, not on the shared access signature.</span></span> <span data-ttu-id="cc213-156">如此做讓我們能變更這些限制，而不必重新發出共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="cc213-156">Doing so enables us to change these constraints without reissuing the shared access signature.</span></span>

<span data-ttu-id="cc213-157">在共用的存取簽章上可以有一或多個限制，其餘的則在儲存原則上。</span><span class="sxs-lookup"><span data-stu-id="cc213-157">It's possible to have one or more of the constraints on the shared access signature, and the remainder on the stored access policy.</span></span> <span data-ttu-id="cc213-158">不過，您只能在其中一個位置指定開始時間、到期時間和權限。</span><span class="sxs-lookup"><span data-stu-id="cc213-158">However, you can only specify the start time, expiry time, and permissions in one place or the other.</span></span> <span data-ttu-id="cc213-159">例如，您無法既在共用存取簽章上指定權限，又在預存存取原則上指定。</span><span class="sxs-lookup"><span data-stu-id="cc213-159">For example, you can't specify permissions on the shared access signature and also specify them on the stored access policy.</span></span>

<span data-ttu-id="cc213-160">當您新增容器的預存存取原則時，您必須取得容器的現有權限、新增新的存取原則，然後設定容器的權限。</span><span class="sxs-lookup"><span data-stu-id="cc213-160">When you add a stored access policy to a container, you must get the container's existing permissions, add the new access policy, and then set the container's permissions.</span></span>

<span data-ttu-id="cc213-161">新增可在容器上建立新預存存取原則的新方法，並傳回原則的名稱：</span><span class="sxs-lookup"><span data-stu-id="cc213-161">Add a new method that creates a new stored access policy on a container and returns the name of the policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get the container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="cc213-162">在呼叫 **Console.ReadLine()** 之前，於 **Main()** 方法底部新增下列各行，以先清除任何現有的存取原則，然後再呼叫 **CreateSharedAccessPolicy()** 方法：</span><span class="sxs-lookup"><span data-stu-id="cc213-162">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to first clear any existing access policies, and then call the **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on the container, which may be optionally used to provide constraints for
//shared access signatures on the container and the blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="cc213-163">當您清除容器的存取原則時，您必須先取得容器的現有權限、清除權限，然後再次設定權限。</span><span class="sxs-lookup"><span data-stu-id="cc213-163">When you clear the access policies on a container, you must first get the container's existing permissions, then clear the permissions, then set the permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-the-container-that-uses-an-access-policy"></a><span data-ttu-id="cc213-164">在使用存取原則的容器上產生共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="cc213-164">Generate a shared access signature URI on the container that uses an access policy</span></span>
<span data-ttu-id="cc213-165">接下來，我們會為稍早建立的容器建立另一個共用存取簽章，但這次我們會把簽章與我們在前面範例中所建立的預存存取原則相關聯。</span><span class="sxs-lookup"><span data-stu-id="cc213-165">Next, we create another shared access signature for the container that we created earlier, but this time we associate the signature with the stored access policy we created in the previous example.</span></span>

<span data-ttu-id="cc213-166">新增新方法來為容器產生另一個共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="cc213-166">Add a new method to generate another shared access signature for the container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate the shared access signature on the container. In this case, all of the constraints for the
    //shared access signature are specified on the stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="cc213-167">在 **Main()** 方法的底部，對 **Console.ReadLine()** 的呼叫之前，新增下列幾行，以呼叫 **GetContainerSasUriWithPolicy()** 方法：</span><span class="sxs-lookup"><span data-stu-id="cc213-167">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-the-blob-that-uses-an-access-policy"></a><span data-ttu-id="cc213-168">在使用存取原則的 Blob 上產生共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="cc213-168">Generate a Shared Access Signature URI on the Blob That Uses an Access Policy</span></span>
<span data-ttu-id="cc213-169">最後，我們會新增類似方法來建立另一個 Blob，並產生與預存存取原則相關聯的共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="cc213-169">Finally, we add a similar method to create another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="cc213-170">新增新方法以建立 blob 並產生共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="cc213-170">Add a new method to create a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature. " +
    "A stored access policy defines the constraints for the signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate the shared access signature on the blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="cc213-171">在 **Main()** 方法的底部，對 **Console.ReadLine()** 的呼叫之前，新增下列幾行，以呼叫 **GetBlobSasUriWithPolicy** 方法：</span><span class="sxs-lookup"><span data-stu-id="cc213-171">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="cc213-172">**Main()** 方法現在應該整體看來如此。</span><span class="sxs-lookup"><span data-stu-id="cc213-172">The **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="cc213-173">執行它以將共用存取簽章 URI 寫到主控台視窗，然後將它們複製並貼入文字檔，以便用於本教學課程的第 2 部分。</span><span class="sxs-lookup"><span data-stu-id="cc213-173">Run it to write the shared access signature URIs to the console window, then copy and paste them into a text file for use in the second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for the container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on the container, which may be optionally used to provide constraints for
    //shared access signatures on the container and the blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="cc213-174">執行 GenerateSharedAccessSignatures 主控台應用程式時，您會看到類似如下的輸出。</span><span class="sxs-lookup"><span data-stu-id="cc213-174">When you run the GenerateSharedAccessSignatures console application, you'll see output similar to the following.</span></span> <span data-ttu-id="cc213-175">這些是您會在教學課程第 2 部分使用的共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="cc213-175">These are the shared access signatures you use in Part 2 of the tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-to-test-the-shared-access-signatures"></a><span data-ttu-id="cc213-176">第 2 部份：建立主控台應用程式以測試共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="cc213-176">Part 2: Create a console application to test the shared access signatures</span></span>
<span data-ttu-id="cc213-177">為了測試前面範例中建立的共用存取簽章，我們會建立第二個主控台應用程式，使用簽章以在容器和 Blob 上執行操作。</span><span class="sxs-lookup"><span data-stu-id="cc213-177">To test the shared access signatures created in the previous examples, we create a second console application that uses the signatures to perform operations on the container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="cc213-178">如果在您完成本教學課程的第一個部分之後已超過 24 小時，您所產生的簽章將不再有效。</span><span class="sxs-lookup"><span data-stu-id="cc213-178">If more than 24 hours have passed since you completed the first part of the tutorial, the signatures you generated will no longer be valid.</span></span> <span data-ttu-id="cc213-179">在此情況下，您應該在第一個主控台應用程式中執行程式碼以產生新的共用存取簽章，並在第二個部分的教學課程中使用。</span><span class="sxs-lookup"><span data-stu-id="cc213-179">In this case, you should run the code in the first console application to generate fresh shared access signatures for use in the second part of the tutorial.</span></span>
>

<span data-ttu-id="cc213-180">在 Visual Studio 中，建立新的 Windows 主控台應用程式，並將它命名為 **ConsumeSharedAccessSignatures**。</span><span class="sxs-lookup"><span data-stu-id="cc213-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="cc213-181">如前面的作法一樣，新增對 [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) 及 [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) 的參照。</span><span class="sxs-lookup"><span data-stu-id="cc213-181">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="cc213-182">在 Program.cs 檔的頂端，新增下列 **using** 指示詞：</span><span class="sxs-lookup"><span data-stu-id="cc213-182">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="cc213-183">在 **Main()** 方法的本文中，新增下列字串限制，並將其值變更為您在教學課程第 1 部分中產生的共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="cc213-183">In the body of the **Main()** method, add the following string constants, changing their values to the shared access signatures you generated in part 1 of the tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-to-try-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="cc213-184">新增方法以嘗試使用共用存取簽章的容器操作</span><span class="sxs-lookup"><span data-stu-id="cc213-184">Add a method to try container operations using a shared access signature</span></span>
<span data-ttu-id="cc213-185">接下來我們會新增方法，以使用容器的共用存取簽章來測試某些容器操作。</span><span class="sxs-lookup"><span data-stu-id="cc213-185">Next, we add a method that tests some container operations using a shared access signature for the container.</span></span> <span data-ttu-id="cc213-186">共用存取簽章用來傳回對容器的參照，並單獨根據簽章向容器驗證存取。</span><span class="sxs-lookup"><span data-stu-id="cc213-186">The shared access signature is used to return a reference to the container, authenticating access to the container based on the signature alone.</span></span>

<span data-ttu-id="cc213-187">將下列方法新增至 Program.cs：</span><span class="sxs-lookup"><span data-stu-id="cc213-187">Add the following method to Program.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with the SAS provided.

    //Return a reference to the container using the SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list to store blob URIs returned by a listing operation on the container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob to the container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions to the container. ";
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

    //List operation: List the blobs in the container.
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

    //Read operation: Get a reference to one of the blobs in the container and read it.
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

    //Delete operation: Delete a blob in the container.
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

<span data-ttu-id="cc213-188">更新 **Main()** 方法以呼叫 **UseContainerSAS()**，並使用您在容器上建立的兩個共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="cc213-188">Update the **Main()** method to call **UseContainerSAS()** with both of the shared access signatures you created on the container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-to-try-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="cc213-189">新增方法以嘗試使用共用存取簽章的 Blob 操作</span><span class="sxs-lookup"><span data-stu-id="cc213-189">Add a method to try blob operations using a shared access signature</span></span>
<span data-ttu-id="cc213-190">最後，我們會新增方法，以使用 Blob 上的共用存取簽章來測試某些 Blob 操作。</span><span class="sxs-lookup"><span data-stu-id="cc213-190">Finally, we add a method that tests some blob operations using a shared access signature on the blob.</span></span> <span data-ttu-id="cc213-191">在此案例中，我們使用建構函式 **CloudBlockBlob(String)**，並傳入共用存取簽章，以傳回 Blob 的參照。</span><span class="sxs-lookup"><span data-stu-id="cc213-191">In this case, we use the constructor **CloudBlockBlob(String)**, passing in the shared access signature, to return a reference to the blob.</span></span> <span data-ttu-id="cc213-192">不需要其他驗證；只有根據簽章。</span><span class="sxs-lookup"><span data-stu-id="cc213-192">No other authentication is required; it's based on the signature alone.</span></span>

<span data-ttu-id="cc213-193">將下列方法新增至 Program.cs：</span><span class="sxs-lookup"><span data-stu-id="cc213-193">Add the following method to Program.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using the SAS provided.

    //Return a reference to the blob using the SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob to the container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions to the blob. ";
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

    //Read operation: Read the contents of the blob.
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

    //Delete operation: Delete the blob.
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

<span data-ttu-id="cc213-194">更新 **Main()** 方法以呼叫 **UseBlobSAS()**，並使用您在 blob 上建立的兩個共用存取簽章：</span><span class="sxs-lookup"><span data-stu-id="cc213-194">Update the **Main()** method to call **UseBlobSAS()** with both of the shared access signatures that you created on the blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call the test methods with the shared access signatures created on the blob, with and without the access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="cc213-195">執行主控台應用程式，並觀察輸出，以查看哪些簽章允許哪些操作。</span><span class="sxs-lookup"><span data-stu-id="cc213-195">Run the console application and observe the output to see which operations are permitted for which signatures.</span></span> <span data-ttu-id="cc213-196">主控台視窗中的輸出類似如下範例：</span><span class="sxs-lookup"><span data-stu-id="cc213-196">The output in the console window will look similar to the following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="cc213-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc213-197">Next Steps</span></span>

* [<span data-ttu-id="cc213-198">共用存取簽章，第 1 部分：了解 SAS 模型</span><span class="sxs-lookup"><span data-stu-id="cc213-198">Shared Access Signatures, Part 1: Understanding the SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="cc213-199">管理對容器與 Blob 的匿名讀取權限。</span><span class="sxs-lookup"><span data-stu-id="cc213-199">Manage anonymous read access to containers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="cc213-200">使用共用存取簽章 (REST API) 來委派存取權</span><span class="sxs-lookup"><span data-stu-id="cc213-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="cc213-201">資料表與佇列 SAS 簡介</span><span class="sxs-lookup"><span data-stu-id="cc213-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
