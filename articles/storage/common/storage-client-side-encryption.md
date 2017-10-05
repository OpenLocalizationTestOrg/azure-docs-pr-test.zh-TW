---
title: "Microsoft Azure 儲存體的用戶端 .NET 加密 | Microsoft Docs"
description: "Azure Storage Client Library for .NET 支援用戶端加密以及與 Azure 金鑰保存庫的整合，為您的 Azure 儲存體應用程式提供最大的安全性。"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: becfccca-510a-479e-a798-2044becd9a64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 634da215e29ede4e90f7edbef43a3be853165349
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a><span data-ttu-id="bd6fe-103">Microsoft Azure 儲存體的用戶端加密和 Azure Key Vault 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="bd6fe-103">Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="bd6fe-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bd6fe-104">Overview</span></span>
<span data-ttu-id="bd6fe-105">[適用於 .NET NuGet 封裝的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage) 支援在上傳至 Azure 儲存體之前將用戶端應用程式內的資料加密，並在下載至用戶端時解密資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-105">The [Azure Storage Client Library for .NET Nuget package](https://www.nuget.org/packages/WindowsAzure.Storage) supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="bd6fe-106">程式庫也支援與 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/) 整合，以進行儲存體帳戶金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-106">The library also supports integration with [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) for storage account key management.</span></span>

<span data-ttu-id="bd6fe-107">如需引導您進行使用用戶端加密和 Azure 金鑰保存庫來加密 Blob 的逐步教學課程，請參閱 [在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-107">For a step-by-step tutorial that leads you through the process of encrypting blobs using client-side encryption and Azure Key Vault, see [Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](../blobs/storage-encrypt-decrypt-blobs-key-vault.md).</span></span>

<span data-ttu-id="bd6fe-108">如需使用 Java 加密用戶端，請參閱 [Microsoft Azure 儲存體的用戶端 Java 加密](storage-client-side-encryption-java.md)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-108">For client-side encryption with Java, see [Client-Side Encryption with Java for Microsoft Azure Storage](storage-client-side-encryption-java.md).</span></span>

## <a name="encryption-and-decryption-via-the-envelope-technique"></a><span data-ttu-id="bd6fe-109">透過信封技術進行加密和解密</span><span class="sxs-lookup"><span data-stu-id="bd6fe-109">Encryption and decryption via the envelope technique</span></span>
<span data-ttu-id="bd6fe-110">加密和解密的程序採用信封技術。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-110">The processes of encryption and decryption follow the envelope technique.</span></span>

### <a name="encryption-via-the-envelope-technique"></a><span data-ttu-id="bd6fe-111">透過信封技術加密</span><span class="sxs-lookup"><span data-stu-id="bd6fe-111">Encryption via the envelope technique</span></span>
<span data-ttu-id="bd6fe-112">透過信封技術加密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="bd6fe-112">Encryption via the envelope technique works in the following way:</span></span>

1. <span data-ttu-id="bd6fe-113">Azure 儲存體用戶端程式庫會產生內容加密金鑰 (CEK)，這是使用一次的對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-113">The Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="bd6fe-114">使用此 CEK 加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-114">User data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="bd6fe-115">然後使用金鑰加密金鑰 (KEK) 包裝 (加密) CEK。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-115">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="bd6fe-116">KEK 由金鑰識別碼所識別，可以是非對稱金鑰組或對稱金鑰，且可以在本機管理或儲存在 Azure 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-116">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vaults.</span></span>
   
    <span data-ttu-id="bd6fe-117">儲存體用戶端程式庫本身永遠沒有 KEK 的存取權。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-117">The storage client library itself never has access to KEK.</span></span> <span data-ttu-id="bd6fe-118">程式庫會叫用金鑰保存庫所提供的金鑰包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-118">The library invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="bd6fe-119">如有需要，使用者可以選擇使用自訂提供者來包裝/取消包裝金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-119">Users can choose to use custom providers for key wrapping/unwrapping if desired.</span></span>

4. <span data-ttu-id="bd6fe-120">然後，將加密的資料上傳至 Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-120">The encrypted data is then uploaded to the Azure Storage service.</span></span> <span data-ttu-id="bd6fe-121">包裝的金鑰及一些其他加密中繼資料會儲存為中繼資料 (在 blob 上)，或插補加密的資料 (訊息佇列和資料表實體)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-121">The wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with the encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-the-envelope-technique"></a><span data-ttu-id="bd6fe-122">透過信封技術解密</span><span class="sxs-lookup"><span data-stu-id="bd6fe-122">Decryption via the envelope technique</span></span>
<span data-ttu-id="bd6fe-123">透過信封技術解密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="bd6fe-123">Decryption via the envelope technique works in the following way:</span></span>

1. <span data-ttu-id="bd6fe-124">用戶端程式庫假設使用者在本機或 Azure 金鑰保存庫中管理金鑰加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-124">The client library assumes that the user is managing the key encryption key (KEK) either locally or in Azure Key Vaults.</span></span> <span data-ttu-id="bd6fe-125">使用者不必知道用於加密的特定金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-125">The user does not need to know the specific key that was used for encryption.</span></span> <span data-ttu-id="bd6fe-126">相反地，可以設定並使用金鑰解析程式，將不同的金鑰識別碼解析成金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-126">Instead, a key resolver which resolves different key identifiers to keys can be set up and used.</span></span>
2. <span data-ttu-id="bd6fe-127">用戶端程式庫會下載加密的資料，以及儲存在服務上的任何加密資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-127">The client library downloads the encrypted data along with any encryption material that is stored on the service.</span></span>
3. <span data-ttu-id="bd6fe-128">然後，使用金鑰加密金鑰 (KEK) 將已包裝的內容加密金鑰 (CEK) 解除包裝 (解密)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-128">The wrapped content encryption key (CEK) is then unwrapped (decrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="bd6fe-129">同樣地，用戶端程式庫在此沒有 KEK 的存取權。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-129">Here again, the client library does not have access to KEK.</span></span> <span data-ttu-id="bd6fe-130">它只會叫用自訂或 Key Vault 提供者的解除包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-130">It simply invokes the custom or Key Vault provider's unwrapping algorithm.</span></span>
4. <span data-ttu-id="bd6fe-131">然後，使用內容加密金鑰 (CEK) 解密已加密的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-131">The content encryption key (CEK) is then used to decrypt the encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="bd6fe-132">加密機制</span><span class="sxs-lookup"><span data-stu-id="bd6fe-132">Encryption Mechanism</span></span>
<span data-ttu-id="bd6fe-133">儲存體用戶端程式庫會使用 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 來加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-133">The storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order to encrypt user data.</span></span> <span data-ttu-id="bd6fe-134">具體來說，就是 [加密區塊鏈結 (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 模式搭配 AES。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-134">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="bd6fe-135">每個服務的運作方式稍有不同，我們將在這裡討論每個服務。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-135">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="bd6fe-136">Blob</span><span class="sxs-lookup"><span data-stu-id="bd6fe-136">Blobs</span></span>
<span data-ttu-id="bd6fe-137">用戶端程式庫目前僅支援整個 Blob 的加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-137">The client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="bd6fe-138">更明確地說，會在使用者使用 **UploadFrom*** 方法或 **OpenWrite** 方法時支援加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-138">Specifically, encryption is supported when users use the **UploadFrom*** methods or the **OpenWrite** method.</span></span> <span data-ttu-id="bd6fe-139">針對下載，則皆支援完整與範圍下載。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-139">For downloads, both complete and range downloads are supported.</span></span>

<span data-ttu-id="bd6fe-140">在加密期間，用戶端程式庫會產生 16 位元組的隨機初始化向量 (IV)，以及 32 位元組的隨機內容加密金鑰 (CEK)，並使用這項資訊執行 blob 資料的信封加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-140">During encryption, the client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of the blob data using this information.</span></span> <span data-ttu-id="bd6fe-141">然後，已包裝的 CEK 和一些其他加密中繼資料會儲存為 blob 中繼資料，並連同加密的 blob 一起儲存在服務上。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-141">The wrapped CEK and some additional encryption metadata are then stored as blob metadata along with the encrypted blob on the service.</span></span>

> [!WARNING]
> <span data-ttu-id="bd6fe-142">如果您要為 blob 編輯或上傳您自己的中繼資料，則必須確定保留此中繼資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-142">If you are editing or uploading your own metadata for the blob, you need to ensure that this metadata is preserved.</span></span> <span data-ttu-id="bd6fe-143">如果您上傳新的中繼資料，但缺少此中繼資料，包裝的 CEK、IV 和其他中繼資料將會遺失，而且永遠無法再擷取 blob 內容。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-143">If you upload new metadata without this metadata, the wrapped CEK, IV, and other metadata will be lost and the blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="bd6fe-144">下載已加密的 Blob 牽涉到使用 **DownloadTo***/**BlobReadStream* 便利方法擷取整個 Blob 的內容。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-144">Downloading an encrypted blob involves retrieving the content of the entire blob using the **DownloadTo***/**BlobReadStream** convenience methods.</span></span> <span data-ttu-id="bd6fe-145">包裝的 CEK 會解除包裝，並與 IV (在此情況下儲存為 blob 中繼資料) 一起用來傳回解密的資料給使用者。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-145">The wrapped CEK is unwrapped and used together with the IV (stored as blob metadata in this case) to return the decrypted data to the users.</span></span>

<span data-ttu-id="bd6fe-146">在加密的 Blob 中下載任意範圍 (**DownloadRange*** 方法)，包含調整使用者所提供的範圍，藉此取得少量額外的資料以便用來成功解密所要求的範圍。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-146">Downloading an arbitrary range (**DownloadRange*** methods) in the encrypted blob involves adjusting the range provided by users in order to get a small amount of additional data that can be used to successfully decrypt the requested range.</span></span>

<span data-ttu-id="bd6fe-147">所有 Blob 類型 (區塊 Blob、頁面 Blob 和附加 Blob) 都可以使用此機制進行加密/解密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-147">All blob types (block blobs, page blobs, and append blobs) can be encrypted/decrypted using this scheme.</span></span>

### <a name="queues"></a><span data-ttu-id="bd6fe-148">佇列</span><span class="sxs-lookup"><span data-stu-id="bd6fe-148">Queues</span></span>
<span data-ttu-id="bd6fe-149">因為佇列訊息可以是任何格式，用戶端程式庫會定義自訂的格式，其中包含訊息文字中的初始化向量 (IV) 和加密的內容加密金鑰 (CEK)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-149">Since queue messages can be of any format, the client library defines a custom format that includes the Initialization Vector (IV) and the encrypted content encryption key (CEK) in the message text.</span></span>

<span data-ttu-id="bd6fe-150">在加密期間，用戶端程式庫會產生 16 位元組的隨機 IV，以及 32 位元組的隨機 CEK，並使用這項資訊執行佇列訊息文字的信封加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-150">During encryption, the client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of the queue message text using this information.</span></span> <span data-ttu-id="bd6fe-151">然後，已包裝的 CEK 和一些其他加密中繼資料會加入至已加密的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-151">The wrapped CEK and some additional encryption metadata are then added to the encrypted queue message.</span></span> <span data-ttu-id="bd6fe-152">這個修改過的訊息 (如下所示) 會儲存在服務上。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-152">This modified message (shown below) is stored on the service.</span></span>

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

<span data-ttu-id="bd6fe-153">在解密期間，從佇列訊息中擷取已包裝的金鑰，並解除包裝。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-153">During decryption, the wrapped key is extracted from the queue message and unwrapped.</span></span> <span data-ttu-id="bd6fe-154">IV 也會從佇列訊息中擷取，並與未包裝的金鑰一起用來解密佇列訊息資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-154">The IV is also extracted from the queue message and used along with the unwrapped key to decrypt the queue message data.</span></span> <span data-ttu-id="bd6fe-155">請注意，加密中繼資料很小 (小於 500 位元組)，雖然計入佇列訊息的 64KB 限制內，但影響仍在可掌控的範圍內。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-155">Note that the encryption metadata is small (under 500 bytes), so while it does count toward the 64KB limit for a queue message, the impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="bd6fe-156">資料表</span><span class="sxs-lookup"><span data-stu-id="bd6fe-156">Tables</span></span>
<span data-ttu-id="bd6fe-157">用戶端程式庫支援在插入和取代作業時進行實體屬性的加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-157">The client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="bd6fe-158">目前不支援合併。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-158">Merge is not currently supported.</span></span> <span data-ttu-id="bd6fe-159">因為屬性子集先前可能是使用不同的金鑰加密，直接合併新的屬性並更新中繼資料會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-159">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="bd6fe-160">合併可能需要額外的服務呼叫來從服務讀取預先存在的實體，或在每個屬性上都使用新的金鑰，兩者都不利用於效能。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-160">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="bd6fe-161">資料表資料加密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="bd6fe-161">Table data encryption works as follows:</span></span>  

1. <span data-ttu-id="bd6fe-162">使用者指定要加密的屬性。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-162">Users specify the properties to be encrypted.</span></span>
2. <span data-ttu-id="bd6fe-163">用戶端程式庫會針對每個實體產生 16 位元組的隨機初始化向量 (IV) 以及 32 位元組的隨機內容加密金鑰 (CEK)，並在個別屬性上執行信封加密，使每個屬性衍生新的 IV，藉此進行加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-163">The client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on the individual properties to be encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="bd6fe-164">加密的屬性會儲存為二進位資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-164">The encrypted property is stored as binary data.</span></span>
3. <span data-ttu-id="bd6fe-165">然後，已包裝的 CEK 和一些其他加密中繼資料會儲存成額外兩個保留的屬性。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-165">The wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="bd6fe-166">第一個保留的屬性 (_ClientEncryptionMetadata1) 是字串屬性，保存 IV、版本和已包裝的金鑰的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-166">The first reserved property (_ClientEncryptionMetadata1) is a string property that holds the information about IV, version, and wrapped key.</span></span> <span data-ttu-id="bd6fe-167">第二個保留的屬性 (_ClientEncryptionMetadata2) 二進位屬性，其保留已加密之屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-167">The second reserved property (_ClientEncryptionMetadata2) is a binary property that holds the information about the properties that are encrypted.</span></span> <span data-ttu-id="bd6fe-168">此第二個屬性 (_ClientEncryptionMetadata2) 中的資訊已自行加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-168">The information in this second property (_ClientEncryptionMetadata2) is itself encrypted.</span></span>
4. <span data-ttu-id="bd6fe-169">由於加密需要這些額外保留的屬性，使用者現在可能只有 250 個自訂屬性，而不是 252 個。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-169">Due to these additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="bd6fe-170">實體的總大小必須小於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-170">The total size of the entity must be less than 1 MB.</span></span>

<span data-ttu-id="bd6fe-171">請注意，只有字串屬性可以加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-171">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="bd6fe-172">如果有其他類型的屬性需要加密，則必須轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-172">If other types of properties are to be encrypted, they must be converted to strings.</span></span> <span data-ttu-id="bd6fe-173">加密的字串儲存在服務上作為二進位屬性，且解密後會轉換回字串。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-173">The encrypted strings are stored on the service as binary properties, and they are converted back to strings after decryption.</span></span>

<span data-ttu-id="bd6fe-174">針對資料表，除了加密原則之外，使用者必須指定要加密的屬性。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-174">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="bd6fe-175">作法是指定 [EncryptProperty] 屬性 (針對衍生自 TableEntity 的 POCO 實體)，或在要求選項中指定加密解析程式。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-175">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="bd6fe-176">加密解析程式是委派，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-176">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="bd6fe-177">在加密期間，用戶端程式庫會使用此資訊，決定將屬性在寫到網路時是否應該加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-177">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="bd6fe-178">委派也提供關於屬性如何加密的可能邏輯。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-178">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="bd6fe-179">(例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，讀取或查詢實體時不需要提供這項資訊。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-179">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="bd6fe-180">批次作業</span><span class="sxs-lookup"><span data-stu-id="bd6fe-180">Batch Operations</span></span>
<span data-ttu-id="bd6fe-181">在批次作業中，批次作業中的所有資料列上會使用相同的 KEK，因為用戶端程式庫只允許每個批次作業有一個選項物件 (也就是一個原則/KEK)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-181">In batch operations, the same KEK will be used across all the rows in that batch operation because the client library only allows one options object (and hence one policy/KEK) per batch operation.</span></span> <span data-ttu-id="bd6fe-182">不過，用戶端程式庫會在內部為批次中的每個資料列產生新的隨機 IV 和隨機 CEK。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-182">However, the client library will internally generate a new random IV and random CEK per row in the batch.</span></span> <span data-ttu-id="bd6fe-183">使用者也可以選擇為批次中的每個作業加密不同的屬性，作法是在加密解析程式中定義此行為。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-183">Users can also choose to encrypt different properties for every operation in the batch by defining this behavior in the encryption resolver.</span></span>

### <a name="queries"></a><span data-ttu-id="bd6fe-184">查詢</span><span class="sxs-lookup"><span data-stu-id="bd6fe-184">Queries</span></span>
<span data-ttu-id="bd6fe-185">若要執行查詢作業，您必須指定一個能夠解析結果集中的所有金鑰的金鑰解析程式。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-185">To perform query operations, you must specify a key resolver that is able to resolve all the keys in the result set.</span></span> <span data-ttu-id="bd6fe-186">如果查詢結果中包含的實體無法解析成提供者，用戶端程式庫會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-186">If an entity contained in the query result cannot be resolved to a provider, the client library will throw an error.</span></span> <span data-ttu-id="bd6fe-187">針對執行伺服器端投影的任何查詢，用戶端程式庫會依預設將特殊加密中繼資料屬性 (_ClientEncryptionMetadata1 和 _ClientEncryptionMetadata2) 加入選取的資料行。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-187">For any query that performs server-side projections, the client library will add the special encryption metadata properties (_ClientEncryptionMetadata1 and _ClientEncryptionMetadata2) by default to the selected columns.</span></span>

## <a name="azure-key-vault"></a><span data-ttu-id="bd6fe-188">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="bd6fe-188">Azure Key Vault</span></span>
<span data-ttu-id="bd6fe-189">Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-189">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span> <span data-ttu-id="bd6fe-190">使用 Azure 金鑰保存庫時，使用者可以使用受硬體安全模組 (HSM) 保護的金鑰來加密金鑰和密碼 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.PFX 檔案和密碼)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-190">By using Azure Key Vault, users can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .PFX files, and passwords) by using keys that are protected by hardware security modules (HSMs).</span></span> <span data-ttu-id="bd6fe-191">如需詳細資訊，請參閱 [什麼是 Azure 金鑰保存庫？](../../key-vault/key-vault-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-191">For more information, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="bd6fe-192">儲存體用戶端程式庫會使用金鑰保存庫核心程式庫，以提供整個 Azure 的通用架構來管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-192">The storage client library uses the Key Vault core library in order to provide a common framework across Azure for managing keys.</span></span> <span data-ttu-id="bd6fe-193">使用者也享有使用金鑰保存庫延伸模組程式庫的額外好處。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-193">Users also get the additional benefit of using the Key Vault extensions library.</span></span> <span data-ttu-id="bd6fe-194">延伸模組程式庫提供實用的功能，包括簡單又完善的對稱/RSA 本機和雲端金鑰提供者，以及彙總和快取。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-194">The extensions library provides useful functionality around simple and seamless Symmetric/RSA local and cloud key providers as well as with aggregation and caching.</span></span>

### <a name="interface-and-dependencies"></a><span data-ttu-id="bd6fe-195">介面和相依性</span><span class="sxs-lookup"><span data-stu-id="bd6fe-195">Interface and dependencies</span></span>
<span data-ttu-id="bd6fe-196">有三個金鑰保存庫封裝：</span><span class="sxs-lookup"><span data-stu-id="bd6fe-196">There are three Key Vault packages:</span></span>

* <span data-ttu-id="bd6fe-197">Microsoft.Azure.KeyVault.Core 包含 IKey 和 IKeyResolver。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-197">Microsoft.Azure.KeyVault.Core contains the IKey and IKeyResolver.</span></span> <span data-ttu-id="bd6fe-198">這是不具有相依性的小型封裝。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-198">It is a small package with no dependencies.</span></span> <span data-ttu-id="bd6fe-199">.NET 的儲存體用戶端程式庫會將其定義為相依。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-199">The storage client library for .NET defines it as a dependency.</span></span>
* <span data-ttu-id="bd6fe-200">Microsoft.Azure.KeyVault 包含金鑰保存庫 REST 用戶端。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-200">Microsoft.Azure.KeyVault contains the Key Vault REST client.</span></span>
* <span data-ttu-id="bd6fe-201">Microsoft.Azure.KeyVault.Extensions 包含延伸模組程式碼，其中包含密碼編譯演算法的實作及 RSAKey 和 SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-201">Microsoft.Azure.KeyVault.Extensions contains extension code that includes implementations of cryptographic algorithms and an RSAKey and a SymmetricKey.</span></span> <span data-ttu-id="bd6fe-202">它依賴 Core 和 KeyVault 命名空間，並提供功能來定義彙總解析程式 (當使用者想要使用多個金鑰提供者時) 和快取金鑰解析程式。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-202">It depends on the Core and KeyVault namespaces and provides functionality to define an aggregate resolver (when users want to use multiple key providers) and a caching key resolver.</span></span> <span data-ttu-id="bd6fe-203">儲存體用戶端程式庫不直接依賴這個封裝，如果使用者想要使用 Azure 金鑰保存庫來儲存其金鑰，或使用金鑰保存庫延伸模組來取用本機和雲端密碼編譯提供者，則需要此封裝。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-203">Although the storage client library does not directly depend on this package, if users wish to use Azure Key Vault to store their keys or to use the Key Vault extensions to consume the local and cloud cryptographic providers, they will need this package.</span></span>

<span data-ttu-id="bd6fe-204">金鑰保存庫是專為高價值的主要金鑰而設計，個別金鑰保存庫的節流限制都以此為設計重點。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-204">Key Vault is designed for high-value master keys, and throttling limits per Key Vault are designed with this in mind.</span></span> <span data-ttu-id="bd6fe-205">使用金鑰保存庫執行用戶端加密時，慣用的模型是使用在金鑰保存庫中儲存為密碼且在本機快取的對稱主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-205">When performing client-side encryption with Key Vault, the preferred model is to use symmetric master keys stored as secrets in Key Vault and cached locally.</span></span> <span data-ttu-id="bd6fe-206">使用者必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="bd6fe-206">Users must do the following:</span></span>

1. <span data-ttu-id="bd6fe-207">離線建立密碼，再上載至金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-207">Create a secret offline and upload it to Key Vault.</span></span>
2. <span data-ttu-id="bd6fe-208">使用密碼的基底識別碼做為參數，解析用於加密的目前密碼版本，並在本機快取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-208">Use the secret's base identifier as a parameter to resolve the current version of the secret for encryption and cache this information locally.</span></span> <span data-ttu-id="bd6fe-209">使用 CachingKeyResolver 進行快取。使用者不需要實作自己的快取邏輯。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-209">Use CachingKeyResolver for caching; users are not expected to implement their own caching logic.</span></span>
3. <span data-ttu-id="bd6fe-210">建立加密原則時，使用快取解析程式做為輸入。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-210">Use the caching resolver as an input while creating the encryption policy.</span></span>

<span data-ttu-id="bd6fe-211">有關金鑰保存庫使用方式的詳細資訊位於 [加密程式碼範例](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-211">More information regarding Key Vault usage can be found in the [encryption code samples](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples).</span></span>

## <a name="best-practices"></a><span data-ttu-id="bd6fe-212">最佳作法</span><span class="sxs-lookup"><span data-stu-id="bd6fe-212">Best practices</span></span>
<span data-ttu-id="bd6fe-213">只有 .NET 的儲存體用戶端程式庫才支援加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-213">Encryption support is available only in the storage client library for .NET.</span></span> <span data-ttu-id="bd6fe-214">Windows Phone 和 Windows 執行階段目前不支援加密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-214">Windows Phone and Windows Runtime do not currently support encryption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd6fe-215">使用用戶端加密時，請留意以下重點：</span><span class="sxs-lookup"><span data-stu-id="bd6fe-215">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="bd6fe-216">讀取或寫入加密的 Blob 時，使用整個 Blob 上傳命令及範圍/整個 Blob 下載命令。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-216">When reading from or writing to an encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="bd6fe-217">避免寫入使用通訊協定作業的加密 Blob，例如：放置區塊、放置區塊清單、寫入頁面、清除頁面或附加區塊；否則您可能會破壞加密 Blob 並使它無法讀取。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-217">Avoid writing to an encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, Clear Pages, or Append Block; otherwise you may corrupt the encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="bd6fe-218">對於資料表，存在類似的條件約束。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-218">For tables, a similar constraint exists.</span></span> <span data-ttu-id="bd6fe-219">請小心在未更新加密中繼資料時即更新加密的內容。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-219">Be careful to not update encrypted properties without updating the encryption metadata.</span></span>
> * <span data-ttu-id="bd6fe-220">如果您在加密 Blob 上設定中繼資料，您可能會覆寫加密所需的加密相關中繼資料，因為設定中繼資料不是加總解密。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-220">If you set metadata on the encrypted blob, you may overwrite the encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="bd6fe-221">快照集也是如此。在為加密的 Blob 建立快照集時，請避免指定中繼資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-221">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="bd6fe-222">如果必須設定中繼資料，請務必先呼叫 **FetchAttributes** 方法，以取得目前的加密中繼資料，並避免在設定中繼資料時並行寫入。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-222">If metadata must be set, be sure to call the **FetchAttributes** method first to get the current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>
> * <span data-ttu-id="bd6fe-223">在預設的要求選項中啟用 **RequireEncryption** 屬性，使用者就應該只能使用加密的資料。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-223">Enable the **RequireEncryption** property in the default request options for users that should work only with encrypted data.</span></span> <span data-ttu-id="bd6fe-224">如需詳細資訊請參閱下方內容。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-224">See below for more info.</span></span>
> 
> 

## <a name="client-api--interface"></a><span data-ttu-id="bd6fe-225">用戶端 API / 介面</span><span class="sxs-lookup"><span data-stu-id="bd6fe-225">Client API / Interface</span></span>
<span data-ttu-id="bd6fe-226">使用者在建立 EncryptionPolicy 物件時，可以只提供金鑰 (實作 IKey)、只提供者解析程式 (實作 IKeyResolver)，或兩者都提供。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-226">While creating an EncryptionPolicy object, users can provide only a Key (implementing IKey), only a resolver (implementing IKeyResolver), or both.</span></span> <span data-ttu-id="bd6fe-227">IKey 是以金鑰識別碼來識別的基本金鑰類型，且提供包裝/解除包裝的邏輯。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-227">IKey is the basic key type that is identified using a key identifier and that provides the logic for wrapping/unwrapping.</span></span> <span data-ttu-id="bd6fe-228">IKeyResolver 在解密程序期間用來解析金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-228">IKeyResolver is used to resolve a key during the decryption process.</span></span> <span data-ttu-id="bd6fe-229">它定義 ResolveKey 方法，可根據金鑰識別碼傳回 IKey。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-229">It defines a ResolveKey method that returns an IKey given a key identifier.</span></span> <span data-ttu-id="bd6fe-230">這可讓使用者從多個位置中管理的多個金鑰之中選擇。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-230">This provides users the ability to choose between multiple keys that are managed in multiple locations.</span></span>

* <span data-ttu-id="bd6fe-231">加密時一律使用金鑰，缺少金鑰將會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-231">For encryption, the key is used always and the absence of a key will result in an error.</span></span>
* <span data-ttu-id="bd6fe-232">解密：</span><span class="sxs-lookup"><span data-stu-id="bd6fe-232">For decryption:</span></span>
  * <span data-ttu-id="bd6fe-233">叫用金鑰解析程式 (如果指定) 以取得金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-233">The key resolver is invoked if specified to get the key.</span></span> <span data-ttu-id="bd6fe-234">如果已指定解析程式，但沒有金鑰識別碼的對應，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-234">If the resolver is specified but does not have a mapping for the key identifier, an error is thrown.</span></span>
  * <span data-ttu-id="bd6fe-235">如果未指定解析程式但指定了金鑰，則如果其識別項符合所需的金鑰識別項，就會使用該金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-235">If resolver is not specified but a key is specified, the key is used if its identifier matches the required key identifier.</span></span> <span data-ttu-id="bd6fe-236">如果識別項不符合，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-236">If the identifier does not match, an error is thrown.</span></span>

<span data-ttu-id="bd6fe-237">[加密範例](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) 會針對 Blob、佇列和資料表以及金鑰保存庫的整合，示範更詳細的端對端案例。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-237">The [encryption samples](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) demonstrate a more detailed end-to-end scenario for blobs, queues and tables, along with Key Vault integration.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="bd6fe-238">RequireEncryption 模式</span><span class="sxs-lookup"><span data-stu-id="bd6fe-238">RequireEncryption mode</span></span>
<span data-ttu-id="bd6fe-239">使用者可以針對所有上傳和下載都必須加密的作業模式，從中選擇啟用。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-239">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="bd6fe-240">在此模式中，在用戶端上嘗試上傳沒有加密原則的資料或下載未在服務上加密的資料將會失敗。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-240">In this mode, attempts to upload data without an encryption policy or download data that is not encrypted on the service will fail on the client.</span></span> <span data-ttu-id="bd6fe-241">要求選項物件的 **RequireEncryption** 屬性會控制此行為。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-241">The **RequireEncryption** property of the request options object controls this behavior.</span></span> <span data-ttu-id="bd6fe-242">如果您的應用程式會將所有儲存在 Azure 儲存體中的物件加密，則您可以在服務用戶端服務的預設要求選項上，設定 **RequireEncryption** 屬性。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-242">If your application will encrypt all objects stored in Azure Storage, then you can set the **RequireEncryption** property on the default request options for the service client object.</span></span> <span data-ttu-id="bd6fe-243">例如，將 **CloudBlobClient.DefaultRequestOptions.RequireEncryption** 設為 **true**，要求加密透過該用戶端物件所執行的所有 Blob 作業。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-243">For example, set **CloudBlobClient.DefaultRequestOptions.RequireEncryption** to **true** to require encryption for all blob operations performed through that client object.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="bd6fe-244">Blob 服務加密</span><span class="sxs-lookup"><span data-stu-id="bd6fe-244">Blob service encryption</span></span>
<span data-ttu-id="bd6fe-245">建立 **BlobEncryptionPolicy** 物件，並在要求選項中加以設定 (透過 API 或在用戶端層級使用 **DefaultRequestOptions**)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-245">Create a **BlobEncryptionPolicy** object and set it in the request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="bd6fe-246">其他一切由用戶端程式庫在內部處理。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-246">Everything else will be handled by the client library internally.</span></span>

```csharp
// Create the IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create the encryption policy to be used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set the encryption policy on the request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload the encrypted contents to the blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt the encrypted contents from the blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a><span data-ttu-id="bd6fe-247">佇列服務加密</span><span class="sxs-lookup"><span data-stu-id="bd6fe-247">Queue service encryption</span></span>
<span data-ttu-id="bd6fe-248">建立 **QueueEncryptionPolicy** 物件，並在要求選項中加以設定 (透過 API 或在用戶端層級使用 **DefaultRequestOptions**)。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-248">Create a **QueueEncryptionPolicy** object and set it in the request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="bd6fe-249">其他一切由用戶端程式庫在內部處理。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-249">Everything else will be handled by the client library internally.</span></span>

```csharp
// Create the IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create the encryption policy to be used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a><span data-ttu-id="bd6fe-250">資料表服務加密</span><span class="sxs-lookup"><span data-stu-id="bd6fe-250">Table service encryption</span></span>
<span data-ttu-id="bd6fe-251">除了建立加密原則並在要求選項上加以設定之外，您必須在 **TableRequestOptions** 中指定 **EncryptionResolver**，或在實體上設定 [EncryptProperty] 屬性。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-251">In addition to creating an encryption policy and setting it on request options, you must either specify an **EncryptionResolver** in **TableRequestOptions**, or set the [EncryptProperty] attribute on the entity.</span></span>

#### <a name="using-the-resolver"></a><span data-ttu-id="bd6fe-252">使用解析程式</span><span class="sxs-lookup"><span data-stu-id="bd6fe-252">Using the resolver</span></span>

```csharp
// Create the IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create the encryption policy to be used for upload and download.
 TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

 TableRequestOptions options = new TableRequestOptions()
 {
    EncryptionResolver = (pk, rk, propName) =>
     {
        if (propName == "foo")
         {
            return true;
         }
         return false;
     },
     EncryptionPolicy = policy
 };

 // Insert Entity
 currentTable.Execute(TableOperation.Insert(ent), options, null);

 // Retrieve Entity
 // No need to specify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a><span data-ttu-id="bd6fe-253">使用屬性</span><span class="sxs-lookup"><span data-stu-id="bd6fe-253">Using attributes</span></span>
<span data-ttu-id="bd6fe-254">如上所述，如果實體實作 TableEntity，則屬性可以使用 [EncryptProperty] 屬性裝飾，不需指定 **EncryptionResolver**。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-254">As mentioned above, if the entity implements TableEntity, then the properties can be decorated with the [EncryptProperty] attribute instead of specifying the **EncryptionResolver**.</span></span>

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a><span data-ttu-id="bd6fe-255">加密和效能</span><span class="sxs-lookup"><span data-stu-id="bd6fe-255">Encryption and performance</span></span>
<span data-ttu-id="bd6fe-256">請注意，加密您的儲存體資料會造成額外的效能負擔。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-256">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="bd6fe-257">必須產生內容金鑰和 IV，內容本身必須經過加密，而且其他中繼資料必須格式化並上傳。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-257">The content key and IV must be generated, the content itself must be encrypted, and additional meta-data must be formatted and uploaded.</span></span> <span data-ttu-id="bd6fe-258">這個額外負荷會因所加密的資料數量而有所不同。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-258">This overhead will vary depending on the quantity of data being encrypted.</span></span> <span data-ttu-id="bd6fe-259">我們建議客戶一定要在開發期間測試其應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="bd6fe-259">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd6fe-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bd6fe-260">Next steps</span></span>
* [<span data-ttu-id="bd6fe-261">教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob</span><span class="sxs-lookup"><span data-stu-id="bd6fe-261">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)
* <span data-ttu-id="bd6fe-262">下載 [適用於 .NET NuGet 封裝的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)</span><span class="sxs-lookup"><span data-stu-id="bd6fe-262">Download the [Azure Storage Client Library for .NET NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage)</span></span>
* <span data-ttu-id="bd6fe-263">下載 Azure 金鑰保存庫 NuGet 的 [Core](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/)、[Client](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/) 和 [Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) 封裝</span><span class="sxs-lookup"><span data-stu-id="bd6fe-263">Download the Azure Key Vault NuGet [Core](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [Client](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), and [Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) packages</span></span>  
* <span data-ttu-id="bd6fe-264">請瀏覽 [Azure 金鑰保存庫文件](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="bd6fe-264">Visit the [Azure Key Vault Documentation](../../key-vault/key-vault-whatis.md)</span></span>