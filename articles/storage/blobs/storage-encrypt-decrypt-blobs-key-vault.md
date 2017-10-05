---
title: "教學課程︰在 Azure 儲存體中使用 Azure Key Vault 加密和解密 Blob | Microsoft Docs"
description: "如何使用 Microsoft Azure 儲存體的用戶端加密並搭配 Azure Key Vault 來加密和解密 Blob。"
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: a2a3a4773d33fe6b8589ad8d9d219acda4d1015e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="f32f8-103">教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob</span><span class="sxs-lookup"><span data-stu-id="f32f8-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="f32f8-104">簡介</span><span class="sxs-lookup"><span data-stu-id="f32f8-104">Introduction</span></span>
<span data-ttu-id="f32f8-105">本教學課程涵蓋如何搭配使用用戶端儲存體加密和 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f32f8-105">This tutorial covers how to make use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="f32f8-106">其中告訴您如何在主控台應用程式中使用這些技術加密和解密 blob。</span><span class="sxs-lookup"><span data-stu-id="f32f8-106">It walks you through how to encrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="f32f8-107">**預估完成時間：** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="f32f8-107">**Estimated time to complete:** 20 minutes</span></span>

<span data-ttu-id="f32f8-108">如需 Azure 金鑰保存庫的概觀資訊，請參閱[什麼是 Azure 金鑰保存庫？](../../key-vault/key-vault-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f32f8-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="f32f8-109">如需 Azure 儲存體用戶端加密的概觀資訊，請參閱 [Microsoft Azure 儲存體用戶端加密和 Azure 金鑰保存庫](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f32f8-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f32f8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f32f8-110">Prerequisites</span></span>
<span data-ttu-id="f32f8-111">若要完成本教學課程，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="f32f8-111">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="f32f8-112">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f32f8-112">An Azure Storage account</span></span>
* <span data-ttu-id="f32f8-113">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="f32f8-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="f32f8-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f32f8-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="f32f8-115">用戶端加密概觀</span><span class="sxs-lookup"><span data-stu-id="f32f8-115">Overview of client-side encryption</span></span>
<span data-ttu-id="f32f8-116">如需 Azure 儲存體用戶端加密的概觀，請參閱 [Microsoft Azure 儲存體用戶端加密和 Azure 金鑰保存庫](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f32f8-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="f32f8-117">以下是用戶端加密運作方式的簡短描述：</span><span class="sxs-lookup"><span data-stu-id="f32f8-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="f32f8-118">Azure 儲存體用戶端 SDK 會產生內容加密金鑰 (CEK)，這是使用一次的對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="f32f8-118">The Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="f32f8-119">客戶資料是使用此 CEK 加密。</span><span class="sxs-lookup"><span data-stu-id="f32f8-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="f32f8-120">然後使用金鑰加密金鑰 (KEK) 包裝 (加密) CEK。</span><span class="sxs-lookup"><span data-stu-id="f32f8-120">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="f32f8-121">KEK 由金鑰識別碼所識別，可以是非對稱金鑰組或對稱金鑰，且可以在本機管理或儲存在 Azure 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="f32f8-121">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="f32f8-122">儲存體用戶端本身永遠沒有 KEK 的存取權。</span><span class="sxs-lookup"><span data-stu-id="f32f8-122">The Storage client itself never has access to the KEK.</span></span> <span data-ttu-id="f32f8-123">它只是叫用金鑰保存庫所提供的金鑰包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="f32f8-123">It just invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="f32f8-124">如有需要，客戶可以選擇使用自訂提供者來包裝/取消包裝金鑰。</span><span class="sxs-lookup"><span data-stu-id="f32f8-124">Customers can choose to use custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="f32f8-125">然後，將加密的資料上傳至 Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="f32f8-125">The encrypted data is then uploaded to the Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="f32f8-126">設定 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f32f8-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="f32f8-127">若要繼續進行本教學課程，您必須執行以下在教學課程[開始使用 Azure 金鑰保存庫](../../key-vault/key-vault-get-started.md)中所述的步驟：</span><span class="sxs-lookup"><span data-stu-id="f32f8-127">In order to proceed with this tutorial, you need to do the following steps, which are outlined in the tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="f32f8-128">建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f32f8-128">Create a key vault.</span></span>
* <span data-ttu-id="f32f8-129">新增金鑰或密碼至金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="f32f8-129">Add a key or secret to the key vault.</span></span>
* <span data-ttu-id="f32f8-130">向 Azure Active Directory 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="f32f8-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="f32f8-131">授權應用程式使用金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="f32f8-131">Authorize the application to use the key or secret.</span></span>

<span data-ttu-id="f32f8-132">請記下向 Azure Active Directory 註冊應用程式時所產生的 ClientID 和 ClientSecret。</span><span class="sxs-lookup"><span data-stu-id="f32f8-132">Make note of the ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="f32f8-133">在金鑰保存庫中建立這兩個金鑰。</span><span class="sxs-lookup"><span data-stu-id="f32f8-133">Create both keys in the key vault.</span></span> <span data-ttu-id="f32f8-134">我們在教學課程的其餘部分假設您已使用下列名稱：ContosoKeyVault 和 TestRSAKey1。</span><span class="sxs-lookup"><span data-stu-id="f32f8-134">We assume for the rest of the tutorial that you have used the following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="f32f8-135">使用封裝與 AppSettings 建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="f32f8-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="f32f8-136">在 Visual Studio 中，建立新的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f32f8-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="f32f8-137">在封裝管理員主控台中加入必要的 nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="f32f8-137">Add necessary nuget packages in the Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is the latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="f32f8-138">將 AppSettings 加入至 App.Config。</span><span class="sxs-lookup"><span data-stu-id="f32f8-138">Add AppSettings to the App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="f32f8-139">新增下列 `using` 陳述式，並確定將 System.Configuration 的參考加入至專案。</span><span class="sxs-lookup"><span data-stu-id="f32f8-139">Add the following `using` statements and make sure to add a reference to System.Configuration to the project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-to-get-a-token-to-your-console-application"></a><span data-ttu-id="f32f8-140">新增方法以取得給主控台應用程式的權杖</span><span class="sxs-lookup"><span data-stu-id="f32f8-140">Add a method to get a token to your console application</span></span>
<span data-ttu-id="f32f8-141">需要驗證以存取您的金鑰保存庫的金鑰保存庫類別會使用下列方法。</span><span class="sxs-lookup"><span data-stu-id="f32f8-141">The following method is used by Key Vault classes that need to authenticate for access to your key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="f32f8-142">在您的程式中存取儲存體和金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f32f8-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="f32f8-143">在 Main 函式中，加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f32f8-143">In the Main function, add the following code.</span></span>

```csharp
// This is standard code to interact with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// The Resolver object is used to interact with Key Vault for Azure Storage.
// This is where the GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="f32f8-144">金鑰保存庫物件模型</span><span class="sxs-lookup"><span data-stu-id="f32f8-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="f32f8-145">務必了解，實際上有兩個金鑰保存庫物件模型需要注意：一個是根據 REST API (KeyVault 命名空間)，另一個是用戶端加密的延伸。</span><span class="sxs-lookup"><span data-stu-id="f32f8-145">It is important to understand that there are actually two Key Vault object models to be aware of: one is based on the REST API (KeyVault namespace) and the other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="f32f8-146">金鑰保存庫用戶端會與 REST API 互動，並了解金鑰保存庫中包含的兩種項目的 JSON Web 金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="f32f8-146">The Key Vault Client interacts with the REST API and understands JSON Web Keys and secrets for the two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="f32f8-147">金鑰保存庫延伸模組似乎是特別為 Azure 儲存體中的用戶端加密而建立的類別。</span><span class="sxs-lookup"><span data-stu-id="f32f8-147">The Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="f32f8-148">它們根據金鑰解析程式的概念，包含金鑰 (IKey) 和類別的介面。</span><span class="sxs-lookup"><span data-stu-id="f32f8-148">They contain an interface for keys (IKey) and classes based on the concept of a Key Resolver.</span></span> <span data-ttu-id="f32f8-149">您需要知道 IKey 的兩個實作：RSAKey 和 SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="f32f8-149">There are two implementations of IKey that you need to know: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="f32f8-150">現在，它們剛好與金鑰保存庫中所包含的項目重疊，但目前是獨立的類別 (因此，金鑰保存庫用戶端所擷取的金鑰和密碼不實作 IKey)。</span><span class="sxs-lookup"><span data-stu-id="f32f8-150">Now they happen to coincide with the things that are contained in a Key Vault, but at this point they are independent classes (so the Key and Secret retrieved by the Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="f32f8-151">加密 blob 和上傳</span><span class="sxs-lookup"><span data-stu-id="f32f8-151">Encrypt blob and upload</span></span>
<span data-ttu-id="f32f8-152">加入下列程式碼來加密 Blob 並上傳至 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f32f8-152">Add the following code to encrypt a blob and upload it to your Azure storage account.</span></span> <span data-ttu-id="f32f8-153">使用的 **ResolveKeyAsync** 方法會傳回 IKey。</span><span class="sxs-lookup"><span data-stu-id="f32f8-153">The **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve the key that you created previously.
// The IKey that is returned here is an RsaKey.
// Remember that we used the names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use the RSA key to encrypt by setting it in the BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using the UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="f32f8-154">以下是目前 [Azure 傳統入口網站](https://manage.windowsazure.com)的螢幕擷取畫面，其中使用用戶端加密與金鑰保存庫中儲存的金鑰來加密 blob。</span><span class="sxs-lookup"><span data-stu-id="f32f8-154">Following is a screenshot from the [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="f32f8-155">**KeyId** 屬性是金鑰保存庫中做為 KEK 的金鑰的 URI。</span><span class="sxs-lookup"><span data-stu-id="f32f8-155">The **KeyId** property is the URI for the key in Key Vault that acts as the KEK.</span></span> <span data-ttu-id="f32f8-156">**EncryptedKey** 屬性包含 CEK 的加密版本。</span><span class="sxs-lookup"><span data-stu-id="f32f8-156">The **EncryptedKey** property contains the encrypted version of the CEK.</span></span>

![此螢幕擷取畫面顯示包含加密中繼資料的 Blob 中繼資料](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="f32f8-158">如果您查看 BlobEncryptionPolicy 建構函式，您會看到它可接受金鑰和 (或) 解析程式。</span><span class="sxs-lookup"><span data-stu-id="f32f8-158">If you look at the BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="f32f8-159">請注意，現在您無法使用解析程式進行加密，因為它目前不支援預設金鑰。</span><span class="sxs-lookup"><span data-stu-id="f32f8-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="f32f8-160">解密 blob 和下傳</span><span class="sxs-lookup"><span data-stu-id="f32f8-160">Decrypt blob and download</span></span>
<span data-ttu-id="f32f8-161">解密其實就是解析程式類別存在的價值。</span><span class="sxs-lookup"><span data-stu-id="f32f8-161">Decryption is really when using the Resolver classes make sense.</span></span> <span data-ttu-id="f32f8-162">加密金鑰的識別碼與它的中繼資料裡的 Blob 相關聯，因此，沒有理由讓您擷取金鑰，並記住金鑰與 blob 之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="f32f8-162">The ID of the key used for encryption is associated with the blob in its metadata, so there is no reason for you to retrieve the key and remember the association between key and blob.</span></span> <span data-ttu-id="f32f8-163">您只需要確定金鑰仍在金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="f32f8-163">You just have to make sure that the key remains in Key Vault.</span></span>   

<span data-ttu-id="f32f8-164">RSA 金鑰的私密金鑰保留在保存庫金鑰中，為了進行解密，從包含 CEK 的 blob 中繼資料，加密的金鑰會傳送至金鑰保存庫進行解密。</span><span class="sxs-lookup"><span data-stu-id="f32f8-164">The private key of an RSA Key remains in Key Vault, so for decryption to occur, the Encrypted Key from the blob metadata that contains the CEK is sent to Key Vault for decryption.</span></span>

<span data-ttu-id="f32f8-165">加入下列內容以解密您剛才上傳的 blob。</span><span class="sxs-lookup"><span data-stu-id="f32f8-165">Add the following to decrypt the blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass the resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="f32f8-166">有幾個其他種類的解析程式可簡化金鑰管理，包括：AggregateKeyResolver 和 CachingKeyResolver。</span><span class="sxs-lookup"><span data-stu-id="f32f8-166">There are a couple of other kinds of resolvers to make key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="f32f8-167">使用金鑰保存庫密碼</span><span class="sxs-lookup"><span data-stu-id="f32f8-167">Use Key Vault secrets</span></span>
<span data-ttu-id="f32f8-168">搭配用戶端加密來使用密碼的方式是透過 SymmetricKey 類別，因為密碼基本上是一種對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="f32f8-168">The way to use a secret with client-side encryption is via the SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="f32f8-169">但是，如上所述，金鑰保存庫中的密碼未完全對應到 SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="f32f8-169">But, as noted above, a secret in Key Vault does not map exactly to a SymmetricKey.</span></span> <span data-ttu-id="f32f8-170">有幾件事必須了解：</span><span class="sxs-lookup"><span data-stu-id="f32f8-170">There are a few things to understand:</span></span>

* <span data-ttu-id="f32f8-171">SymmetricKey 中的金鑰必須是固定的長度：128、192、256、384 或 512 位元。</span><span class="sxs-lookup"><span data-stu-id="f32f8-171">The key in a SymmetricKey has to be a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="f32f8-172">SymmetricKey 中的金鑰應該為 Base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="f32f8-172">The key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="f32f8-173">用來做為 SymmetricKey 的金鑰保存庫密碼，在金鑰保存庫中必須具有 "application/octet-stream" 內容類型。</span><span class="sxs-lookup"><span data-stu-id="f32f8-173">A Key Vault secret that will be used as a SymmetricKey needs to have a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="f32f8-174">以下是在 PowerShell 中，在保存庫中建立密碼做為 SymmetricKey 的範例：</span><span class="sxs-lookup"><span data-stu-id="f32f8-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="f32f8-175">請注意，硬式編碼的值 ($key) 僅用於示範目的。</span><span class="sxs-lookup"><span data-stu-id="f32f8-175">Please note that the hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="f32f8-176">在自己的程式碼中，您會想要產生此金鑰。</span><span class="sxs-lookup"><span data-stu-id="f32f8-176">In your own code you'll want to generate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     The characters are in the ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute the VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="f32f8-177">在主控台應用程式中，您可以使用像以前一樣的呼叫來擷取這個密碼做為 SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="f32f8-177">In your console application, you can use the same call as before to retrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="f32f8-178">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="f32f8-178">That's it.</span></span> <span data-ttu-id="f32f8-179">盡情享受！</span><span class="sxs-lookup"><span data-stu-id="f32f8-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f32f8-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f32f8-180">Next steps</span></span>
<span data-ttu-id="f32f8-181">如需有關搭配使用 C# 和 Microsoft Azure 儲存體的詳細資訊，請參閱[適用於 .NET 的 Microsoft Azure 儲存體用戶端程式庫](https://msdn.microsoft.com/library/azure/dn261237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f32f8-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="f32f8-182">如需 Blob REST API 的詳細資訊，請參閱 [Blob 服務 REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f32f8-182">For more information about the Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="f32f8-183">如需 Microsoft Azure 儲存體的最新資訊，請移至 [Microsoft Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。</span><span class="sxs-lookup"><span data-stu-id="f32f8-183">For the latest information on Microsoft Azure Storage, go to the [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
