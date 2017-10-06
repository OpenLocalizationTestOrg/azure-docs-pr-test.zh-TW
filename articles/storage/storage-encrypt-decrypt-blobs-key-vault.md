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
ms.openlocfilehash: 3eb64f104f378dd09ef295c94e03167655883391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob
## <a name="introduction"></a>簡介
本教學課程涵蓋 toomake 如何使用 Azure 金鑰保存庫的用戶端的儲存體加密的使用。 它將逐步引導您 tooencrypt 和解密使用這些技術的主控台應用程式中的 blob。

**估計時間 toocomplete:** 20 分鐘

如需 Azure 金鑰保存庫的概觀資訊，請參閱[什麼是 Azure 金鑰保存庫？](../key-vault/key-vault-whatis.md)。

如需 Azure 儲存體用戶端加密的概觀資訊，請參閱 [Microsoft Azure 儲存體用戶端加密和 Azure 金鑰保存庫](storage-client-side-encryption.md)。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您必須擁有下列 hello:

* Azure 儲存體帳戶
* Visual Studio 2013 或更新版本
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>用戶端加密概觀
如需 Azure 儲存體用戶端加密的概觀，請參閱 [Microsoft Azure 儲存體用戶端加密和 Azure 金鑰保存庫](storage-client-side-encryption.md)

以下是用戶端加密運作方式的簡短描述：

1. hello Azure 儲存體用戶端 SDK 產生的內容加密金鑰 (CEK)，這是一次性單次使用對稱金鑰。
2. 客戶資料是使用此 CEK 加密。
3. hello CEK 然後再包裝 （加密） 使用 hello 金鑰的加密金鑰 (KEK)。 hello KEK 索引鍵的識別項所識別，可非對稱金鑰組或對稱金鑰，可以是本機管理或儲存在 Azure 金鑰保存庫中。 hello 儲存體用戶端本身完全不需要存取 toohello KEK。 它只叫用所提供的金鑰保存庫 hello 金鑰包裝演算法。 客戶可以選擇 toouse 包裝/解除包裝如果他們想要的索引鍵的自訂提供者。
4. hello 加密的資料是然後上傳 toohello Azure 儲存體服務。

## <a name="set-up-your-azure-key-vault"></a>設定 Azure 金鑰保存庫
順序 tooproceed 進行這個教學課程，您需要依照 hello 教學課程中所述的步驟 toodo hello[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md):

* 建立金鑰保存庫。
* 新增金鑰或密碼 toohello 金鑰保存庫。
* 向 Azure Active Directory 註冊應用程式。
* 授權 hello 應用程式 toouse hello 金鑰或密碼。

請記下 hello ClientID 和 ClientSecret 向 Azure Active Directory 註冊應用程式時所產生。

Hello 金鑰保存庫中建立兩個索引鍵。 我們假設您已使用下列名稱的 hello hello hello 教學課程的其餘部分： ContosoKeyVault 和 TestRSAKey1。

## <a name="create-a-console-application-with-packages-and-appsettings"></a>使用封裝與 AppSettings 建立主控台應用程式
在 Visual Studio 中，建立新的主控台應用程式。

Hello Package Manager Console 中新增必要的 nuget 封裝。

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

新增 AppSettings toohello App.Config。

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

新增下列 hello`using`陳述式，並請確定 tooadd 參考 tooSystem.Configuration toohello 專案。

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>加入方法 tooget 語彙基元 tooyour 主控台應用程式
hello 下列方法會使用需要 tooauthenticate 存取 tooyour 金鑰保存庫的金鑰保存庫類別。

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

## <a name="access-storage-and-key-vault-in-your-program"></a>在您的程式中存取儲存體和金鑰保存庫
在 hello Main 函式中，加入下列程式碼的 hello。

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
> 金鑰保存庫物件模型
> 
> 務必 toounderstand 有實際的兩個金鑰保存庫物件模型 toobe 留意： 一個根據 hello REST API （KeyVault 命名空間），而且其他 hello 是用戶端加密的擴充功能。
> 
> 金鑰保存庫用戶端 hello hello REST API 進行互動，並了解 JSON Web 金鑰和密碼適用於 hello 兩種金鑰保存庫中所包含的項目。
> 
> hello 金鑰保存庫延伸模組是似乎是特別針對 Azure 儲存體中的用戶端加密所建立的類別。 它們包含索引鍵 (IKey) 和索引鍵的解析程式 hello 概念為基礎的類別的介面。 有兩個實作的您需要 tooknow IKey: RSAKey 和 SymmetricKey。 現在仍發生 toocoincide 與金鑰保存庫中所包含的 hello 項目，但此時它們是獨立的類別 （因此 hello 金鑰和金鑰保存庫用戶端 hello 所擷取的密碼不會實作 IKey）。
> 
> 

## <a name="encrypt-blob-and-upload"></a>加密 blob 和上傳
新增 hello 下列程式碼 tooencrypt blob，並將它上傳 tooyour Azure 儲存體帳戶。 hello **ResolveKeyAsync**用的方法會傳回 IKey。

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

以下是從 hello 螢幕擷取畫面[Azure 傳統入口網站](https://manage.windowsazure.com)已透過用戶端加密與金鑰保存庫中儲存的金鑰加密的 blob。 hello **KeyId**屬性是 hello URI 做為 hello KEK 金鑰保存庫中的 hello 索引鍵。 hello **EncryptedKey**屬性包含 hello hello CEK 加密的版本。

![此螢幕擷取畫面顯示包含加密中繼資料的 Blob 中繼資料](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> 如果您看一下 hello BlobEncryptionPolicy 建構函式，您會看到其可接受的索引鍵和 （或） 解析程式。 請注意，現在您無法使用解析程式進行加密，因為它目前不支援預設金鑰。
> 
> 

## <a name="decrypt-blob-and-download"></a>解密 blob 和下傳
解密實際上是當使用 hello 解析程式的類別有意義。 hello 識別碼 hello 金鑰加密所使用的是它的中繼資料中的 hello blob 相關聯，所以沒有理由您 tooretrieve hello 金鑰，並記住 hello 金鑰與 blob 之間的關聯。 您只需要 toomake 確定該 hello 金鑰仍在金鑰保存庫。   

hello 私密金鑰的 RSA 金鑰會維持為在金鑰保存庫，因此的解密 toooccur hello 加密金鑰從包含傳送 tooKey 保存庫來解密 CEK 的 hello hello blob 中繼資料。

新增下列 toodecrypt hello blob 剛剛上傳的 hello。

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> 有幾個其他種類的解析程式 toomake 金鑰管理較為簡單，包括： AggregateKeyResolver 和 CachingKeyResolver。
> 
> 

## <a name="use-key-vault-secrets"></a>使用金鑰保存庫密碼
hello 方式 toouse 用戶端加密與密碼是透過 hello SymmetricKey 類別，因為密碼基本上對稱金鑰。 但是，如先前所述，秘密金鑰保存庫中的沒有對應完全 tooa SymmetricKey。 有幾件事 toounderstand:

* SymmetricKey 中的 hello 金鑰都有 toobe 固定的長度： 128、 192、 256、 384 或 512 位元。
* SymmetricKey 的 hello 索引鍵應該是 Base64 編碼。
* 將為 SymmetricKey 使用金鑰保存庫密碼需要 toohave 」 應用程式/八位元資料流 」 金鑰保存庫中的內容類型。

以下是在 PowerShell 中，在保存庫中建立密碼做為 SymmetricKey 的範例：
請注意 hello 硬式編碼值，$key，為只示範用途。 在您自己的程式碼中您會想 toogenerate 這個機碼。

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

在您的主控台應用程式，您可以使用的 hello 相同呼叫如常 tooretrieve 此密碼為 SymmetricKey。

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
就這麼簡單。 盡情享受！

## <a name="next-steps"></a>後續步驟
如需有關搭配使用 C# 和 Microsoft Azure 儲存體的詳細資訊，請參閱[適用於 .NET 的 Microsoft Azure 儲存體用戶端程式庫](https://msdn.microsoft.com/library/azure/dn261237.aspx)。

如需 hello Blob REST API 的詳細資訊，請參閱[Blob 服務 REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx)。

Hello 最新版 Microsoft Azure 儲存體上的資訊，請造訪 toohello [Microsoft Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。
