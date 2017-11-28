---
title: "教學課程︰在 Azure 儲存體中使用 Azure Key Vault 加密和解密 Blob | Microsoft Docs"
description: "如何 tooencrypt 和解密使用用戶端的加密來與 Azure 金鑰保存庫的 Microsoft Azure 儲存體的 blob。"
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
ms.openlocfilehash: e387dd419a51b5b1df62d10ead97268e8295ff56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="9c8cb-103">教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob</span><span class="sxs-lookup"><span data-stu-id="9c8cb-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="9c8cb-104">簡介</span><span class="sxs-lookup"><span data-stu-id="9c8cb-104">Introduction</span></span>
<span data-ttu-id="9c8cb-105">本教學課程涵蓋 toomake 如何使用 Azure 金鑰保存庫的用戶端的儲存體加密的使用。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="9c8cb-106">它將逐步引導您 tooencrypt 和解密使用這些技術的主控台應用程式中的 blob。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="9c8cb-107">**估計時間 toocomplete:** 20 分鐘</span><span class="sxs-lookup"><span data-stu-id="9c8cb-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="9c8cb-108">如需 Azure 金鑰保存庫的概觀資訊，請參閱[什麼是 Azure 金鑰保存庫？](../../key-vault/key-vault-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="9c8cb-109">如需 Azure 儲存體用戶端加密的概觀資訊，請參閱 [Microsoft Azure 儲存體用戶端加密和 Azure 金鑰保存庫](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c8cb-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9c8cb-110">Prerequisites</span></span>
<span data-ttu-id="9c8cb-111">toocomplete 本教學課程中，您必須擁有下列 hello:</span><span class="sxs-lookup"><span data-stu-id="9c8cb-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="9c8cb-112">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="9c8cb-112">An Azure Storage account</span></span>
* <span data-ttu-id="9c8cb-113">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="9c8cb-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="9c8cb-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c8cb-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="9c8cb-115">用戶端加密概觀</span><span class="sxs-lookup"><span data-stu-id="9c8cb-115">Overview of client-side encryption</span></span>
<span data-ttu-id="9c8cb-116">如需 Azure 儲存體用戶端加密的概觀，請參閱 [Microsoft Azure 儲存體用戶端加密和 Azure 金鑰保存庫](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9c8cb-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="9c8cb-117">以下是用戶端加密運作方式的簡短描述：</span><span class="sxs-lookup"><span data-stu-id="9c8cb-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="9c8cb-118">hello Azure 儲存體用戶端 SDK 產生的內容加密金鑰 (CEK)，這是一次性單次使用對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="9c8cb-119">客戶資料是使用此 CEK 加密。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="9c8cb-120">hello CEK 然後再包裝 （加密） 使用 hello 金鑰的加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="9c8cb-121">hello KEK 索引鍵的識別項所識別，可非對稱金鑰組或對稱金鑰，可以是本機管理或儲存在 Azure 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="9c8cb-122">hello 儲存體用戶端本身完全不需要存取 toohello KEK。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="9c8cb-123">它只叫用所提供的金鑰保存庫 hello 金鑰包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="9c8cb-124">客戶可以選擇 toouse 包裝/解除包裝如果他們想要的索引鍵的自訂提供者。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="9c8cb-125">hello 加密的資料是然後上傳 toohello Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="9c8cb-126">設定 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9c8cb-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="9c8cb-127">順序 tooproceed 進行這個教學課程，您需要依照 hello 教學課程中所述的步驟 toodo hello[開始使用 Azure 金鑰保存庫](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="9c8cb-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="9c8cb-128">建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-128">Create a key vault.</span></span>
* <span data-ttu-id="9c8cb-129">新增金鑰或密碼 toohello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="9c8cb-130">向 Azure Active Directory 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="9c8cb-131">授權 hello 應用程式 toouse hello 金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="9c8cb-132">請記下 hello ClientID 和 ClientSecret 向 Azure Active Directory 註冊應用程式時所產生。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="9c8cb-133">Hello 金鑰保存庫中建立兩個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="9c8cb-134">我們假設您已使用下列名稱的 hello hello hello 教學課程的其餘部分： ContosoKeyVault 和 TestRSAKey1。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="9c8cb-135">使用封裝與 AppSettings 建立主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="9c8cb-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="9c8cb-136">在 Visual Studio 中，建立新的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="9c8cb-137">Hello Package Manager Console 中新增必要的 nuget 封裝。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="9c8cb-138">新增 AppSettings toohello App.Config。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="9c8cb-139">新增下列 hello`using`陳述式，並請確定 tooadd 參考 tooSystem.Configuration toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="9c8cb-140">加入方法 tooget 語彙基元 tooyour 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="9c8cb-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="9c8cb-141">hello 下列方法會使用需要 tooauthenticate 存取 tooyour 金鑰保存庫的金鑰保存庫類別。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="9c8cb-142">在您的程式中存取儲存體和金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="9c8cb-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="9c8cb-143">在 hello Main 函式中，加入下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="9c8cb-144">金鑰保存庫物件模型</span><span class="sxs-lookup"><span data-stu-id="9c8cb-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="9c8cb-145">務必 toounderstand 有實際的兩個金鑰保存庫物件模型 toobe 留意： 一個根據 hello REST API （KeyVault 命名空間），而且其他 hello 是用戶端加密的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="9c8cb-146">金鑰保存庫用戶端 hello hello REST API 進行互動，並了解 JSON Web 金鑰和密碼適用於 hello 兩種金鑰保存庫中所包含的項目。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="9c8cb-147">hello 金鑰保存庫延伸模組是似乎是特別針對 Azure 儲存體中的用戶端加密所建立的類別。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="9c8cb-148">它們包含索引鍵 (IKey) 和索引鍵的解析程式 hello 概念為基礎的類別的介面。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="9c8cb-149">有兩個實作的您需要 tooknow IKey: RSAKey 和 SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="9c8cb-150">現在仍發生 toocoincide 與金鑰保存庫中所包含的 hello 項目，但此時它們是獨立的類別 （因此 hello 金鑰和金鑰保存庫用戶端 hello 所擷取的密碼不會實作 IKey）。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="9c8cb-151">加密 blob 和上傳</span><span class="sxs-lookup"><span data-stu-id="9c8cb-151">Encrypt blob and upload</span></span>
<span data-ttu-id="9c8cb-152">新增 hello 下列程式碼 tooencrypt blob，並將它上傳 tooyour Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="9c8cb-153">hello **ResolveKeyAsync**用的方法會傳回 IKey。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="9c8cb-154">以下是從 hello 螢幕擷取畫面[Azure 傳統入口網站](https://manage.windowsazure.com)已透過用戶端加密與金鑰保存庫中儲存的金鑰加密的 blob。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="9c8cb-155">hello **KeyId**屬性是 hello URI 做為 hello KEK 金鑰保存庫中的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="9c8cb-156">hello **EncryptedKey**屬性包含 hello hello CEK 加密的版本。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![此螢幕擷取畫面顯示包含加密中繼資料的 Blob 中繼資料](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="9c8cb-158">如果您看一下 hello BlobEncryptionPolicy 建構函式，您會看到其可接受的索引鍵和 （或） 解析程式。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="9c8cb-159">請注意，現在您無法使用解析程式進行加密，因為它目前不支援預設金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="9c8cb-160">解密 blob 和下傳</span><span class="sxs-lookup"><span data-stu-id="9c8cb-160">Decrypt blob and download</span></span>
<span data-ttu-id="9c8cb-161">解密實際上是當使用 hello 解析程式的類別有意義。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="9c8cb-162">hello 識別碼 hello 金鑰加密所使用的是它的中繼資料中的 hello blob 相關聯，所以沒有理由您 tooretrieve hello 金鑰，並記住 hello 金鑰與 blob 之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="9c8cb-163">您只需要 toomake 確定該 hello 金鑰仍在金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="9c8cb-164">hello 私密金鑰的 RSA 金鑰會維持為在金鑰保存庫，因此的解密 toooccur hello 加密金鑰從包含傳送 tooKey 保存庫來解密 CEK 的 hello hello blob 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="9c8cb-165">新增下列 toodecrypt hello blob 剛剛上傳的 hello。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="9c8cb-166">有幾個其他種類的解析程式 toomake 金鑰管理較為簡單，包括： AggregateKeyResolver 和 CachingKeyResolver。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="9c8cb-167">使用金鑰保存庫密碼</span><span class="sxs-lookup"><span data-stu-id="9c8cb-167">Use Key Vault secrets</span></span>
<span data-ttu-id="9c8cb-168">hello 方式 toouse 用戶端加密與密碼是透過 hello SymmetricKey 類別，因為密碼基本上對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="9c8cb-169">但是，如先前所述，秘密金鑰保存庫中的沒有對應完全 tooa SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="9c8cb-170">有幾件事 toounderstand:</span><span class="sxs-lookup"><span data-stu-id="9c8cb-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="9c8cb-171">SymmetricKey 中的 hello 金鑰都有 toobe 固定的長度： 128、 192、 256、 384 或 512 位元。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="9c8cb-172">SymmetricKey 的 hello 索引鍵應該是 Base64 編碼。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="9c8cb-173">將為 SymmetricKey 使用金鑰保存庫密碼需要 toohave 」 應用程式/八位元資料流 」 金鑰保存庫中的內容類型。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="9c8cb-174">以下是在 PowerShell 中，在保存庫中建立密碼做為 SymmetricKey 的範例：</span><span class="sxs-lookup"><span data-stu-id="9c8cb-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="9c8cb-175">請注意 hello 硬式編碼值，$key，為只示範用途。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="9c8cb-176">在您自己的程式碼中您會想 toogenerate 這個機碼。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="9c8cb-177">在您的主控台應用程式，您可以使用的 hello 相同呼叫如常 tooretrieve 此密碼為 SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="9c8cb-178">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-178">That's it.</span></span> <span data-ttu-id="9c8cb-179">盡情享受！</span><span class="sxs-lookup"><span data-stu-id="9c8cb-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c8cb-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c8cb-180">Next steps</span></span>
<span data-ttu-id="9c8cb-181">如需有關搭配使用 C# 和 Microsoft Azure 儲存體的詳細資訊，請參閱[適用於 .NET 的 Microsoft Azure 儲存體用戶端程式庫](https://msdn.microsoft.com/library/azure/dn261237.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="9c8cb-182">如需 hello Blob REST API 的詳細資訊，請參閱[Blob 服務 REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="9c8cb-183">Hello 最新版 Microsoft Azure 儲存體上的資訊，請造訪 toohello [Microsoft Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。</span><span class="sxs-lookup"><span data-stu-id="9c8cb-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
