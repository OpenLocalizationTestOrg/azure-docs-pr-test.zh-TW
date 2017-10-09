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
ms.openlocfilehash: 32004d7d29a190a7ed7234513428c3c156b833b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>共用存取簽章，第 2 部分：透過 Blob 儲存體來建立與使用 SAS

[第 1 部分](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)探討了共用存取簽章 (SAS)，並說明使用它們的最佳作法。 第 2 部分會顯示您如何 toogenerate，然後使用共用存取簽章使用 Blob 儲存體。 hello 範例以 C# 所撰寫，並使用適用於.NET 的 hello Azure 儲存體用戶端程式庫。 此教學課程中的 hello 範例：

* 在容器上產生共用存取簽章
* 在 blob 上產生共用存取簽章
* 容器資源上建立的預存的存取原則 toomanage 簽章
* 在用戶端應用程式中測試 hello 共用存取簽章

## <a name="about-this-tutorial"></a>關於本教學課程
在本教學課程中，我們會建立兩個主控台應用程式，以示範如何為容器和 Blob 建立及使用共用存取簽章：

**應用程式 1**: hello 管理應用程式。 為容器和 Blob 產生共用存取簽章。 在原始程式碼中包括 hello 儲存體帳戶存取金鑰。

**應用程式 2**: hello 用戶端應用程式。 存取容器和 blob 資源使用 hello 共用存取簽章建立 hello 第一個應用程式。 它會使用唯一 hello 共用的存取簽章 tooaccess 容器和 blob 資源--*不*包含 hello 儲存體帳戶存取金鑰。

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>第 1 部分： 建立主控台應用程式 toogenerate 共用存取簽章
首先，確認您擁有 hello Azure 儲存體用戶端程式庫.NET 安裝。 您可以安裝 hello [NuGet 封裝](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet 封裝")包含 hello hello 用戶端程式庫的最新組件。 這是建議使用的方法，可確保您擁有 hello 最近修正的 hello。 您也可以在 hello hello 最新版本的一部分下載 hello 用戶端程式庫[Azure SDK for.NET](https://azure.microsoft.com/downloads/)。

在 Visual Studio 中，建立新的 Windows 主控台應用程式，並將它命名為 **GenerateSharedAccessSignatures**。 將參考加入太[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)和[WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/)使用其中一種 hello 下列方法：

* 使用 hello [NuGet 套件管理員](https://docs.nuget.org/consume/installing-nuget)Visual Studio 中。 選取 [專案] > [管理 NuGet 套件]，線上搜尋每個套件 (Microsoft.WindowsAzure.ConfigurationManager 和 WindowsAzure.Storage)，並加以安裝。
* 或者，在您安裝的 hello Azure SDK 中尋找這些組件，並加入參考 toothem:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

在 hello hello Program.cs 檔案頂端，加入下列 hello**使用**指示詞：

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

編輯 hello app.config 檔案，使其包含連接字串指向 tooyour 儲存體帳戶的組態設定。 您的 app.config 檔案看起來類似 toothis 其中一個：

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>為容器產生共用存取簽章 URI
與 toobegin，我們方法 toogenerate 共用的存取簽章上加入新的容器。 在此情況下，hello 簽章不是預存的存取原則相關聯，因此它會在 hello URI hello 資訊指出其到期時間和 hello 權限授與。

首先，加入程式碼 toohello **main （)**方法 tooauthenticate 存取 tooyour 儲存體帳戶，並建立新的容器：

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

接下來，加入的方法，會產生 hello hello 容器的共用的存取簽章，並傳回 hello 簽章 URI:

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

加入下列行底部 hello hello hello **main （)**方法之前 hello 太呼叫**main**，toocall **GetContainerSasUri()**和寫入 hello簽章 URI toohello 主控台視窗：

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

編譯並執行 toooutput hello 共用的存取簽章 URI hello 新容器。 hello URI 將類似 toohello 下列：

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

一旦您已經執行 hello 程式碼，您建立 hello 容器 hello 共用的存取簽章才有效 hello 未來 24 小時內。 hello 簽章授與用戶端 hello 容器與 toowrite 新 blob toohello 容器中的權限 toolist blob。

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>產生 Blob 的共用存取簽章 URI
接下來，我們會撰寫類似的程式碼 toocreate hello 容器內的新 blob，並產生共用的存取簽章。 此共用的存取簽章不是相關聯的預存的存取原則，使其包含在 hello URI 中的 hello 開始時間、 到期時間和權限資訊。

加入新的方法，建立新的 blob 寫入某些文字 tooit，則會產生共用的存取簽章和傳回 hello 簽章 URI:

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

在 hello 底部 hello **main （)**方法，加入下列行 toocall hello **GetBlobSasUri()**hello 太呼叫之前，先**main**，和寫入共用的 hello存取簽章 URI toohello 主控台視窗：

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

編譯並執行 toooutput hello 共用的存取簽章 URI hello 新 blob。 hello URI 將類似 toohello 下列：

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Hello 容器上建立的預存的存取原則
現在讓我們來建立 hello 容器，將會定義任何與其相關聯的共用的存取簽章的 hello 條件約束上的 預存的存取原則。

在 hello 前一個範例中，我們指定 hello 開始時間 （以隱含或明確），hello 到期時間和 hello hello 權限的共用存取簽章本身的 URI。 在 hello 遵循範例，我們指定這些 hello 預存存取原則，而非 hello 共用的存取簽章。 可讓我們 toochange 這些條件約束，而不重新發出 hello 共用存取簽章。

很可能 toohave 一或多個 hello hello 共用的存取簽章，條件約束和 hello hello 預存存取原則的其餘部分。 不過，您可以僅指定 hello 開始時間、 到期時間和權限在某一個位置或其他 hello。 例如，您無法在 hello 共用的存取簽章上指定的權限，然後也指定這些 hello 預存存取原則。

當您將預存的存取原則 tooa 容器時，您必須取得 hello 容器的現有權限，新增 hello 新存取原則，然後設定 hello 容器的權限。

加入新的方法，在容器上建立新的預存的存取原則，並傳回 hello hello 原則名稱：

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

在 hello 底部 hello **main （)**方法之前 hello 太呼叫**main**，加入下列的 hello 行 toofirst 清除任何現有的存取原則，然後呼叫 hello **CreateSharedAccessPolicy()**方法：

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

當您清除 hello 在容器上的存取原則時，您必須先取得 hello 容器的現有權限，然後清除 hello 權限，然後再次設定 hello 權限。

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>產生共用的存取簽章上使用存取原則的 hello 容器的 URI
接下來，我們會建立另一個 hello 容器我們稍早建立的共用的存取簽章，但這次我們關聯 hello 簽章與我們建立 hello 前一個範例中的 hello 預存存取原則。

加入新的方法 toogenerate hello 容器的另一個共用的存取簽章：

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

在 hello 底部 hello **main （)**方法之前 hello 太呼叫**main**，新增下列幾行 toocall hello hello **GetContainerSasUriWithPolicy**方法:

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>產生共用存取簽章 URI 上 hello Blob，所使用的存取原則
最後，我們會加入類似的方法 toocreate 另一個 blob，並產生共用的存取簽章與預存的存取原則相關聯。

加入新的方法 toocreate blob，並產生共用的存取簽章：

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

在 hello 底部 hello **main （)**方法之前 hello 太呼叫**main**，新增下列幾行 toocall hello hello **GetBlobSasUriWithPolicy**方法：

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

hello **main （)**方法現在看起來應該像這樣失真。 執行 toowrite hello 共用的存取簽章 Uri toohello 主控台視窗中，然後複製並貼入文字檔案，供 hello 本教學課程的第二個組件中使用。

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

當您執行 hello GenerateSharedAccessSignatures 主控台應用程式時，您會看到類似 toohello 下列輸出。 這些是您在 hello 教學課程的第 2 部分中使用的 hello 共用存取簽章。

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>第 2 部分︰ 建立主控台應用程式 tootest hello 共用存取簽章
tootest hello 共用存取簽章建立 hello 前一個範例中，我們會建立使用 hello 簽章 tooperform 作業 hello 容器和 blob 上的第二個主控台應用程式。

> [!NOTE]
> 如果您完成 hello hello 教學課程的第一個部分後已過了超過 24 小時，您所產生的 hello 簽章將不再有效。 在此情況下，您要執行 hello 程式碼，在第一個主控台應用程式 toogenerate hello 的 hello hello 教學課程的第二個組件中使用全新的共用的存取簽章。
>

在 Visual Studio 中，建立新的 Windows 主控台應用程式，並將它命名為 **ConsumeSharedAccessSignatures**。 將參考加入太[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)和[WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/)、 跟之前一樣。

在 hello hello Program.cs 檔案頂端，加入下列 hello**使用**指示詞：

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

中的 hello hello 主體**main （)**方法，加入下列字串常數、 變更您在 hello 教學課程的第 1 部分中產生其值 toohello 共用存取簽章的 hello。

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>新增使用共用的存取簽章方法 tootry 容器作業
接下來，我們加入測試 hello 容器使用的共用的存取簽章某些容器作業的方法。 hello 共用的存取簽章是使用的 tooreturn 驗證存取 toohello 容器，根據 hello 簽章單獨參考 toohello 容器。

加入下列方法 tooProgram.cs hello:

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

更新 hello **main （)**方法 toocall **UseContainerSAS()**與 hello 這兩個共用存取簽章您 hello 容器建立：

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

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>新增使用共用的存取簽章方法 tootry blob 作業
最後，我們加入測試某些 hello blob 上使用共用的存取簽章的 blob 作業的方法。 在此情況下，我們使用 hello 建構函式**CloudBlockBlob(String)**，並傳入 hello 共用的存取簽章，tooreturn 參考 toohello blob。 沒有其他的驗證是必要項;它根據單獨 hello 簽章。

加入下列方法 tooProgram.cs hello:

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

更新 hello **main （)**方法 toocall **UseBlobSAS()**與 hello 這兩個共用存取簽章，您建立 hello blob 上：

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

執行 hello 主控台應用程式，並觀察 hello 輸出 toosee 允許的作業的簽章。 hello 主控台視窗中的 hello 輸出看起來類似 toohello 下列：

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>後續步驟

* [共用存取簽章，第 1 部分： 了解 SAS 模型 hello](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [管理匿名讀取權限 toocontainers 和 blob](storage-manage-access-to-resources.md)
* [使用共用存取簽章 (REST API) 來委派存取權](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [資料表與佇列 SAS 簡介](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
