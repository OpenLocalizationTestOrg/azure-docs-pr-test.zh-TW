---
title: "Microsoft Azure 儲存體的用戶端 Java 加密 | Microsoft Docs"
description: "Azure Storage Client Library for Java 支援用戶端加密以及與 Azure 金鑰保存庫的整合，為您的 Azure 儲存體應用程式提供最大的安全性。"
services: storage
documentationcenter: java
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 3df49907-554c-404a-9b0c-b3e3269ad04f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: c4ed9a073d4323ed79c4ad9f9e8082d23b970ccf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="client-side-encryption-and-azure-key-vault-with-java-for-microsoft-azure-storage"></a><span data-ttu-id="207d4-103">Microsoft Azure 儲存體搭配 Java 的用戶端加密和 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="207d4-103">Client-Side Encryption and Azure Key Vault with Java for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="207d4-104">概觀</span><span class="sxs-lookup"><span data-stu-id="207d4-104">Overview</span></span>
<span data-ttu-id="207d4-105">[Azure Storage Client Library for Java](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) 支援在上傳至 Azure 儲存體之前將用戶端應用程式內的資料加密，並在下載至用戶端時解密資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-105">The [Azure Storage Client Library for Java](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage) supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="207d4-106">程式庫也支援與 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/) 整合，以進行儲存體帳戶金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="207d4-106">The library also supports integration with [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) for storage account key management.</span></span>

## <a name="encryption-and-decryption-via-the-envelope-technique"></a><span data-ttu-id="207d4-107">透過信封技術進行加密和解密</span><span class="sxs-lookup"><span data-stu-id="207d4-107">Encryption and decryption via the envelope technique</span></span>
<span data-ttu-id="207d4-108">加密和解密的程序採用信封技術。</span><span class="sxs-lookup"><span data-stu-id="207d4-108">The processes of encryption and decryption follow the envelope technique.</span></span>  

### <a name="encryption-via-the-envelope-technique"></a><span data-ttu-id="207d4-109">透過信封技術加密</span><span class="sxs-lookup"><span data-stu-id="207d4-109">Encryption via the envelope technique</span></span>
<span data-ttu-id="207d4-110">透過信封技術加密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="207d4-110">Encryption via the envelope technique works in the following way:</span></span>  

1. <span data-ttu-id="207d4-111">Azure 儲存體用戶端程式庫會產生內容加密金鑰 (CEK)，這是使用一次的對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-111">The Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>  
2. <span data-ttu-id="207d4-112">使用此 CEK 加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-112">User data is encrypted using this CEK.</span></span>   
3. <span data-ttu-id="207d4-113">然後使用金鑰加密金鑰 (KEK) 包裝 (加密) CEK。</span><span class="sxs-lookup"><span data-stu-id="207d4-113">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="207d4-114">KEK 由金鑰識別碼所識別，可以是非對稱金鑰組或對稱金鑰，且可以在本機管理或儲存在 Azure 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="207d4-114">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vaults.</span></span>  
   <span data-ttu-id="207d4-115">儲存體用戶端程式庫本身永遠沒有 KEK 的存取權。</span><span class="sxs-lookup"><span data-stu-id="207d4-115">The storage client library itself never has access to KEK.</span></span> <span data-ttu-id="207d4-116">程式庫會叫用金鑰保存庫所提供的金鑰包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="207d4-116">The library invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="207d4-117">如有需要，使用者可以選擇使用自訂提供者來包裝/取消包裝金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-117">Users can choose to use custom providers for key wrapping/unwrapping if desired.</span></span>  
4. <span data-ttu-id="207d4-118">然後，將加密的資料上傳至 Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="207d4-118">The encrypted data is then uploaded to the Azure Storage service.</span></span> <span data-ttu-id="207d4-119">包裝的金鑰及一些其他加密中繼資料會儲存為中繼資料 (在 blob 上)，或插補加密的資料 (訊息佇列和資料表實體)。</span><span class="sxs-lookup"><span data-stu-id="207d4-119">The wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with the encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-the-envelope-technique"></a><span data-ttu-id="207d4-120">透過信封技術解密</span><span class="sxs-lookup"><span data-stu-id="207d4-120">Decryption via the envelope technique</span></span>
<span data-ttu-id="207d4-121">透過信封技術解密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="207d4-121">Decryption via the envelope technique works in the following way:</span></span>  

1. <span data-ttu-id="207d4-122">用戶端程式庫假設使用者在本機或 Azure 金鑰保存庫中管理金鑰加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="207d4-122">The client library assumes that the user is managing the key encryption key (KEK) either locally or in Azure Key Vaults.</span></span> <span data-ttu-id="207d4-123">使用者不必知道用於加密的特定金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-123">The user does not need to know the specific key that was used for encryption.</span></span> <span data-ttu-id="207d4-124">相反地，可以設定並使用金鑰解析程式，將不同的金鑰識別碼解析成金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-124">Instead, a key resolver which resolves different key identifiers to keys can be set up and used.</span></span>  
2. <span data-ttu-id="207d4-125">用戶端程式庫會下載加密的資料，以及儲存在服務上的任何加密資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-125">The client library downloads the encrypted data along with any encryption material that is stored on the service.</span></span>  
3. <span data-ttu-id="207d4-126">然後，使用金鑰加密金鑰 (KEK) 將已包裝的內容加密金鑰 (CEK) 解除包裝 (解密)。</span><span class="sxs-lookup"><span data-stu-id="207d4-126">The wrapped content encryption key (CEK) is then unwrapped (decrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="207d4-127">同樣地，用戶端程式庫在此沒有 KEK 的存取權。</span><span class="sxs-lookup"><span data-stu-id="207d4-127">Here again, the client library does not have access to KEK.</span></span> <span data-ttu-id="207d4-128">它只會叫用自訂或 Key Vault 提供者的解除包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="207d4-128">It simply invokes the custom or Key Vault provider's unwrapping algorithm.</span></span>  
4. <span data-ttu-id="207d4-129">然後，使用內容加密金鑰 (CEK) 解密已加密的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-129">The content encryption key (CEK) is then used to decrypt the encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="207d4-130">加密機制</span><span class="sxs-lookup"><span data-stu-id="207d4-130">Encryption Mechanism</span></span>
<span data-ttu-id="207d4-131">儲存體用戶端程式庫會使用 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 來加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-131">The storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order to encrypt user data.</span></span> <span data-ttu-id="207d4-132">具體來說，就是 [加密區塊鏈結 (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 模式搭配 AES。</span><span class="sxs-lookup"><span data-stu-id="207d4-132">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="207d4-133">每個服務的運作方式稍有不同，我們將在這裡討論每個服務。</span><span class="sxs-lookup"><span data-stu-id="207d4-133">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="207d4-134">Blob</span><span class="sxs-lookup"><span data-stu-id="207d4-134">Blobs</span></span>
<span data-ttu-id="207d4-135">用戶端程式庫目前僅支援整個 Blob 的加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-135">The client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="207d4-136">更明確地說，會在使用者使用 **upload*** 方法或 **openOutputStream** 方法時支援加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-136">Specifically, encryption is supported when users use the **upload*** methods or the **openOutputStream** method.</span></span> <span data-ttu-id="207d4-137">針對下載，則皆支援完整與範圍下載。</span><span class="sxs-lookup"><span data-stu-id="207d4-137">For downloads, both complete and range downloads are supported.</span></span>  

<span data-ttu-id="207d4-138">在加密期間，用戶端程式庫會產生 16 位元組的隨機初始化向量 (IV)，以及 32 位元組的隨機內容加密金鑰 (CEK)，並使用這項資訊執行 blob 資料的信封加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-138">During encryption, the client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of the blob data using this information.</span></span> <span data-ttu-id="207d4-139">然後，已包裝的 CEK 和一些其他加密中繼資料會儲存為 blob 中繼資料，並連同加密的 blob 一起儲存在服務上。</span><span class="sxs-lookup"><span data-stu-id="207d4-139">The wrapped CEK and some additional encryption metadata are then stored as blob metadata along with the encrypted blob on the service.</span></span>

> [!WARNING]
> <span data-ttu-id="207d4-140">如果您要為 blob 編輯或上傳您自己的中繼資料，則必須確定保留此中繼資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-140">If you are editing or uploading your own metadata for the blob, you need to ensure that this metadata is preserved.</span></span> <span data-ttu-id="207d4-141">如果您上傳新的中繼資料，但缺少此中繼資料，包裝的 CEK、IV 和其他中繼資料將會遺失，而且永遠無法再擷取 blob 內容。</span><span class="sxs-lookup"><span data-stu-id="207d4-141">If you upload new metadata without this metadata, the wrapped CEK, IV and other metadata will be lost and the blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="207d4-142">下載已加密的 blob 牽涉到使用 download/openInputStream 便利方法來擷取整個 blob 的內容。</span><span class="sxs-lookup"><span data-stu-id="207d4-142">Downloading an encrypted blob involves retrieving the content of the entire blob using the **download*/openInputStream** convenience methods.</span></span> <span data-ttu-id="207d4-143">包裝的 CEK 會解除包裝，並與 IV (在此情況下儲存為 blob 中繼資料) 一起用來傳回解密的資料給使用者。</span><span class="sxs-lookup"><span data-stu-id="207d4-143">The wrapped CEK is unwrapped and used together with the IV (stored as blob metadata in this case) to return the decrypted data to the users.</span></span>

<span data-ttu-id="207d4-144">在加密的 Blob 中下載任意範圍 (**downloadRange*** 方法)，包含調整使用者所提供的範圍，藉此取得少量額外的資料以便用來成功解密所要求的範圍。</span><span class="sxs-lookup"><span data-stu-id="207d4-144">Downloading an arbitrary range (**downloadRange*** methods) in the encrypted blob involves adjusting the range provided by users in order to get a small amount of additional data that can be used to successfully decrypt the requested range.</span></span>  

<span data-ttu-id="207d4-145">所有 Blob 類型 (區塊 Blob、頁面 Blob 和附加 Blob) 都可以使用此機制進行加密/解密。</span><span class="sxs-lookup"><span data-stu-id="207d4-145">All blob types (block blobs, page blobs, and append blobs) can be encrypted/decrypted using this scheme.</span></span>

### <a name="queues"></a><span data-ttu-id="207d4-146">佇列</span><span class="sxs-lookup"><span data-stu-id="207d4-146">Queues</span></span>
<span data-ttu-id="207d4-147">因為佇列訊息可以是任何格式，用戶端程式庫會定義自訂的格式，其中包含訊息文字中的初始化向量 (IV) 和加密的內容加密金鑰 (CEK)。</span><span class="sxs-lookup"><span data-stu-id="207d4-147">Since queue messages can be of any format, the client library defines a custom format that includes the Initialization Vector (IV) and the encrypted content encryption key (CEK) in the message text.</span></span>  

<span data-ttu-id="207d4-148">在加密期間，用戶端程式庫會產生 16 位元組的隨機 IV，以及 32 位元組的隨機 CEK，並使用這項資訊執行佇列訊息文字的信封加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-148">During encryption, the client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of the queue message text using this information.</span></span> <span data-ttu-id="207d4-149">然後，已包裝的 CEK 和一些其他加密中繼資料會加入至已加密的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="207d4-149">The wrapped CEK and some additional encryption metadata are then added to the encrypted queue message.</span></span> <span data-ttu-id="207d4-150">這個修改過的訊息 (如下所示) 會儲存在服務上。</span><span class="sxs-lookup"><span data-stu-id="207d4-150">This modified message (shown below) is stored on the service.</span></span>

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

<span data-ttu-id="207d4-151">在解密期間，從佇列訊息中擷取已包裝的金鑰，並解除包裝。</span><span class="sxs-lookup"><span data-stu-id="207d4-151">During decryption, the wrapped key is extracted from the queue message and unwrapped.</span></span> <span data-ttu-id="207d4-152">IV 也會從佇列訊息中擷取，並與未包裝的金鑰一起用來解密佇列訊息資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-152">The IV is also extracted from the queue message and used along with the unwrapped key to decrypt the queue message data.</span></span> <span data-ttu-id="207d4-153">請注意，加密中繼資料很小 (小於 500 位元組)，雖然計入佇列訊息的 64KB 限制內，但影響仍在可掌控的範圍內。</span><span class="sxs-lookup"><span data-stu-id="207d4-153">Note that the encryption metadata is small (under 500 bytes), so while it does count toward the 64KB limit for a queue message, the impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="207d4-154">資料表</span><span class="sxs-lookup"><span data-stu-id="207d4-154">Tables</span></span>
<span data-ttu-id="207d4-155">用戶端程式庫支援在插入和取代作業時進行實體屬性的加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-155">The client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="207d4-156">目前不支援合併。</span><span class="sxs-lookup"><span data-stu-id="207d4-156">Merge is not currently supported.</span></span> <span data-ttu-id="207d4-157">因為屬性子集先前可能是使用不同的金鑰加密，直接合併新的屬性並更新中繼資料會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="207d4-157">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="207d4-158">合併可能需要額外的服務呼叫來從服務讀取預先存在的實體，或在每個屬性上都使用新的金鑰，兩者都不利用於效能。</span><span class="sxs-lookup"><span data-stu-id="207d4-158">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="207d4-159">資料表資料加密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="207d4-159">Table data encryption works as follows:</span></span>  

1. <span data-ttu-id="207d4-160">使用者指定要加密的屬性。</span><span class="sxs-lookup"><span data-stu-id="207d4-160">Users specify the properties to be encrypted.</span></span>  
2. <span data-ttu-id="207d4-161">用戶端程式庫會針對每個實體產生 16 位元組的隨機初始化向量 (IV) 以及 32 位元組的隨機內容加密金鑰 (CEK)，並在個別屬性上執行信封加密，使每個屬性衍生新的 IV，藉此進行加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-161">The client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on the individual properties to be encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="207d4-162">加密的屬性會儲存為二進位資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-162">The encrypted property is stored as binary data.</span></span>  
3. <span data-ttu-id="207d4-163">然後，已包裝的 CEK 和一些其他加密中繼資料會儲存成額外兩個保留的屬性。</span><span class="sxs-lookup"><span data-stu-id="207d4-163">The wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="207d4-164">第一個保留的屬性 (_ClientEncryptionMetadata1) 是字串屬性，保存 IV、版本和已包裝的金鑰的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="207d4-164">The first reserved property (_ClientEncryptionMetadata1) is a string property that holds the information about IV, version, and wrapped key.</span></span> <span data-ttu-id="207d4-165">第二個保留的屬性 (_ClientEncryptionMetadata2) 二進位屬性，其保留已加密之屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="207d4-165">The second reserved property (_ClientEncryptionMetadata2) is a binary property that holds the information about the properties that are encrypted.</span></span> <span data-ttu-id="207d4-166">此第二個屬性 (_ClientEncryptionMetadata2) 中的資訊已自行加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-166">The information in this second property (_ClientEncryptionMetadata2) is itself encrypted.</span></span>  
4. <span data-ttu-id="207d4-167">由於加密需要這些額外保留的屬性，使用者現在可能只有 250 個自訂屬性，而不是 252 個。</span><span class="sxs-lookup"><span data-stu-id="207d4-167">Due to these additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="207d4-168">實體的總大小必須小於 1MB。</span><span class="sxs-lookup"><span data-stu-id="207d4-168">The total size of the entity must be less than 1MB.</span></span>  
   
   <span data-ttu-id="207d4-169">請注意，只有字串屬性可以加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-169">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="207d4-170">如果有其他類型的屬性需要加密，則必須轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="207d4-170">If other types of properties are to be encrypted, they must be converted to strings.</span></span> <span data-ttu-id="207d4-171">加密的字串儲存在服務上作為二進位屬性，且解密後會轉換回字串。</span><span class="sxs-lookup"><span data-stu-id="207d4-171">The encrypted strings are stored on the service as binary properties, and they are converted back to strings after decryption.</span></span>
   
   <span data-ttu-id="207d4-172">針對資料表，除了加密原則之外，使用者必須指定要加密的屬性。</span><span class="sxs-lookup"><span data-stu-id="207d4-172">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="207d4-173">作法是指定 [Encrypt] 屬性 (針對衍生自 TableEntity 的 POCO 實體)，或在要求選項中指定加密解析程式。</span><span class="sxs-lookup"><span data-stu-id="207d4-173">This can be done by either specifying an [Encrypt] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="207d4-174">加密解析程式是委派，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。</span><span class="sxs-lookup"><span data-stu-id="207d4-174">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="207d4-175">在加密期間，用戶端程式庫會使用此資訊，決定將屬性在寫到網路時是否應該加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-175">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="207d4-176">委派也提供關於屬性如何加密的可能邏輯。</span><span class="sxs-lookup"><span data-stu-id="207d4-176">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="207d4-177">(例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，讀取或查詢實體時不需要提供這項資訊。</span><span class="sxs-lookup"><span data-stu-id="207d4-177">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="207d4-178">批次作業</span><span class="sxs-lookup"><span data-stu-id="207d4-178">Batch Operations</span></span>
<span data-ttu-id="207d4-179">在批次作業中，批次作業中的所有資料列上會使用相同的 KEK，因為用戶端程式庫只允許每個批次作業有一個選項物件 (也就是一個原則/KEK)。</span><span class="sxs-lookup"><span data-stu-id="207d4-179">In batch operations, the same KEK will be used across all the rows in that batch operation because the client library only allows one options object (and hence one policy/KEK) per batch operation.</span></span> <span data-ttu-id="207d4-180">不過，用戶端程式庫會在內部為批次中的每個資料列產生新的隨機 IV 和隨機 CEK。</span><span class="sxs-lookup"><span data-stu-id="207d4-180">However, the client library will internally generate a new random IV and random CEK per row in the batch.</span></span> <span data-ttu-id="207d4-181">使用者也可以選擇為批次中的每個作業加密不同的屬性，作法是在加密解析程式中定義此行為。</span><span class="sxs-lookup"><span data-stu-id="207d4-181">Users can also choose to encrypt different properties for every operation in the batch by defining this behavior in the encryption resolver.</span></span>

### <a name="queries"></a><span data-ttu-id="207d4-182">查詢</span><span class="sxs-lookup"><span data-stu-id="207d4-182">Queries</span></span>
<span data-ttu-id="207d4-183">若要執行查詢作業，您必須指定一個能夠解析結果集中的所有金鑰的金鑰解析程式。</span><span class="sxs-lookup"><span data-stu-id="207d4-183">To perform query operations, you must specify a key resolver that is able to resolve all the keys in the result set.</span></span> <span data-ttu-id="207d4-184">如果查詢結果中包含的實體無法解析成提供者，用戶端程式庫會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="207d4-184">If an entity contained in the query result cannot be resolved to a provider, the client library will throw an error.</span></span> <span data-ttu-id="207d4-185">針對執行伺服器端投影的任何查詢，用戶端程式庫會依預設將特殊加密中繼資料屬性 (_ClientEncryptionMetadata1 和 _ClientEncryptionMetadata2) 加入選取的資料行。</span><span class="sxs-lookup"><span data-stu-id="207d4-185">For any query that performs server side projections, the client library will add the special encryption metadata properties (_ClientEncryptionMetadata1 and _ClientEncryptionMetadata2) by default to the selected columns.</span></span>

## <a name="azure-key-vault"></a><span data-ttu-id="207d4-186">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="207d4-186">Azure Key Vault</span></span>
<span data-ttu-id="207d4-187">Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="207d4-187">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span> <span data-ttu-id="207d4-188">使用 Azure 金鑰保存庫時，使用者可以使用受硬體安全模組 (HSM) 保護的金鑰來加密金鑰和密碼 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.PFX 檔案和密碼)。</span><span class="sxs-lookup"><span data-stu-id="207d4-188">By using Azure Key Vault, users can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .PFX files, and passwords) by using keys that are protected by hardware security modules (HSMs).</span></span> <span data-ttu-id="207d4-189">如需詳細資訊，請參閱 [什麼是 Azure 金鑰保存庫？](../key-vault/key-vault-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="207d4-189">For more information, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="207d4-190">儲存體用戶端程式庫會使用金鑰保存庫核心程式庫，以提供整個 Azure 的通用架構來管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-190">The storage client library uses the Key Vault core library in order to provide a common framework across Azure for managing keys.</span></span> <span data-ttu-id="207d4-191">使用者也享有使用金鑰保存庫延伸模組程式庫的額外好處。</span><span class="sxs-lookup"><span data-stu-id="207d4-191">Users also get the additional benefit of using the Key Vault extensions library.</span></span> <span data-ttu-id="207d4-192">延伸模組程式庫提供實用的功能，包括簡單又完善的對稱/RSA 本機和雲端金鑰提供者，以及彙總和快取。</span><span class="sxs-lookup"><span data-stu-id="207d4-192">The extensions library provides useful functionality around simple and seamless Symmetric/RSA local and cloud key providers as well as with aggregation and caching.</span></span>

### <a name="interface-and-dependencies"></a><span data-ttu-id="207d4-193">介面和相依性</span><span class="sxs-lookup"><span data-stu-id="207d4-193">Interface and dependencies</span></span>
<span data-ttu-id="207d4-194">有三個金鑰保存庫封裝：</span><span class="sxs-lookup"><span data-stu-id="207d4-194">There are three Key Vault packages:</span></span>  

* <span data-ttu-id="207d4-195">azure-keyvault-core 包含 IKey 和 IKeyResolver。</span><span class="sxs-lookup"><span data-stu-id="207d4-195">azure-keyvault-core contains the IKey and IKeyResolver.</span></span> <span data-ttu-id="207d4-196">這是不具有相依性的小型封裝。</span><span class="sxs-lookup"><span data-stu-id="207d4-196">It is a small package with no dependencies.</span></span> <span data-ttu-id="207d4-197">Java 的儲存體用戶端程式庫會將其定義為相依。</span><span class="sxs-lookup"><span data-stu-id="207d4-197">The storage client library for Java defines it as a dependency.</span></span>
* <span data-ttu-id="207d4-198">azure-keyvault 包含金鑰保存庫 REST 用戶端。</span><span class="sxs-lookup"><span data-stu-id="207d4-198">azure-keyvault contains the Key Vault REST client.</span></span>  
* <span data-ttu-id="207d4-199">azure-keyvault-extensions 包含延伸模組程式碼，其中包含密碼編譯演算法的實作及 RSAKey 和 SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="207d4-199">azure-keyvault-extensions contains extension code that includes implementations of cryptographic algorithms and an RSAKey and a SymmetricKey.</span></span> <span data-ttu-id="207d4-200">它依賴 Core 和 KeyVault 命名空間，並提供功能來定義彙總解析程式 (當使用者想要使用多個金鑰提供者時) 和快取金鑰解析程式。</span><span class="sxs-lookup"><span data-stu-id="207d4-200">It depends on the Core and KeyVault namespaces and provides functionality to define an aggregate resolver (when users want to use multiple key providers) and a caching key resolver.</span></span> <span data-ttu-id="207d4-201">儲存體用戶端程式庫不直接依賴這個封裝，如果使用者想要使用 Azure 金鑰保存庫來儲存其金鑰，或使用金鑰保存庫延伸模組來取用本機和雲端密碼編譯提供者，則需要此封裝。</span><span class="sxs-lookup"><span data-stu-id="207d4-201">Although the storage client library does not directly depend on this package, if users wish to use Azure Key Vault to store their keys or to use the Key Vault extensions to consume the local and cloud cryptographic providers, they will need this package.</span></span>  
  
  <span data-ttu-id="207d4-202">金鑰保存庫是專為高價值的主要金鑰而設計，個別金鑰保存庫的節流限制都以此為設計重點。</span><span class="sxs-lookup"><span data-stu-id="207d4-202">Key Vault is designed for high-value master keys, and throttling limits per Key Vault are designed with this in mind.</span></span> <span data-ttu-id="207d4-203">使用金鑰保存庫執行用戶端加密時，慣用的模型是使用在金鑰保存庫中儲存為密碼且在本機快取的對稱主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-203">When performing client-side encryption with Key Vault, the preferred model is to use symmetric master keys stored as secrets in Key Vault and cached locally.</span></span> <span data-ttu-id="207d4-204">使用者必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="207d4-204">Users must do the following:</span></span>  

1. <span data-ttu-id="207d4-205">離線建立密碼，再上載至金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="207d4-205">Create a secret offline and upload it to Key Vault.</span></span>  
2. <span data-ttu-id="207d4-206">使用密碼的基底識別碼做為參數，解析用於加密的目前密碼版本，並在本機快取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="207d4-206">Use the secret's base identifier as a parameter to resolve the current version of the secret for encryption and cache this information locally.</span></span> <span data-ttu-id="207d4-207">使用 CachingKeyResolver 進行快取。使用者不需要實作自己的快取邏輯。</span><span class="sxs-lookup"><span data-stu-id="207d4-207">Use CachingKeyResolver for caching; users are not expected to implement their own caching logic.</span></span>  
3. <span data-ttu-id="207d4-208">建立加密原則時，使用快取解析程式做為輸入。</span><span class="sxs-lookup"><span data-stu-id="207d4-208">Use the caching resolver as an input while creating the encryption policy.</span></span>
   <span data-ttu-id="207d4-209">如需有關「金鑰保存庫」使用方式的詳細資訊，請參閱加密程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="207d4-209">More information regarding Key Vault usage can be found in the encryption code samples.</span></span> <fix URL>  

## <a name="best-practices"></a><span data-ttu-id="207d4-210">最佳作法</span><span class="sxs-lookup"><span data-stu-id="207d4-210">Best practices</span></span>
<span data-ttu-id="207d4-211">只有 Java 的儲存體用戶端程式庫才支援加密。</span><span class="sxs-lookup"><span data-stu-id="207d4-211">Encryption support is available only in the storage client library for Java.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="207d4-212">使用用戶端加密時，請留意以下重點：</span><span class="sxs-lookup"><span data-stu-id="207d4-212">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="207d4-213">讀取或寫入加密的 Blob 時，使用整個 Blob 上傳命令及範圍/整個 Blob 下載命令。</span><span class="sxs-lookup"><span data-stu-id="207d4-213">When reading from or writing to an encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="207d4-214">避免寫入使用通訊協定作業的加密 Blob，例如：放置區塊、放置區塊清單、寫入頁面、清除頁面或附加區塊；否則您可能會破壞加密 Blob 並使它無法讀取。</span><span class="sxs-lookup"><span data-stu-id="207d4-214">Avoid writing to an encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, Clear Pages, or Append Block; otherwise you may corrupt the encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="207d4-215">對於資料表，存在類似的條件約束。</span><span class="sxs-lookup"><span data-stu-id="207d4-215">For tables, a similar constraint exists.</span></span> <span data-ttu-id="207d4-216">請小心在未更新加密中繼資料時即更新加密的內容。</span><span class="sxs-lookup"><span data-stu-id="207d4-216">Be careful to not update encrypted properties without updating the encryption metadata.</span></span>  
> * <span data-ttu-id="207d4-217">如果您在加密 Blob 上設定中繼資料，您可能會覆寫加密所需的加密相關中繼資料，因為設定中繼資料不是加總解密。</span><span class="sxs-lookup"><span data-stu-id="207d4-217">If you set metadata on the encrypted blob, you may overwrite the encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="207d4-218">快照集也是如此。在為加密的 Blob 建立快照集時，請避免指定中繼資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-218">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="207d4-219">如果必須設定中繼資料，請務必先呼叫 **downloadAttributes** 方法，以取得目前的加密中繼資料，並避免在設定中繼資料時並行寫入。</span><span class="sxs-lookup"><span data-stu-id="207d4-219">If metadata must be set, be sure to call the **downloadAttributes** method first to get the current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>  
> * <span data-ttu-id="207d4-220">在預設的要求選項中啟用 **requireEncryption** 旗標，使用者就應該只能使用加密的資料。</span><span class="sxs-lookup"><span data-stu-id="207d4-220">Enable the **requireEncryption** flag in the default request options for users that should work only with encrypted data.</span></span> <span data-ttu-id="207d4-221">如需詳細資訊請參閱下方內容。</span><span class="sxs-lookup"><span data-stu-id="207d4-221">See below for more info.</span></span>  
> 
> 

## <a name="client-api--interface"></a><span data-ttu-id="207d4-222">用戶端 API / 介面</span><span class="sxs-lookup"><span data-stu-id="207d4-222">Client API / Interface</span></span>
<span data-ttu-id="207d4-223">使用者在建立 EncryptionPolicy 物件時，可以只提供金鑰 (實作 IKey)、只提供者解析程式 (實作 IKeyResolver)，或兩者都提供。</span><span class="sxs-lookup"><span data-stu-id="207d4-223">While creating an EncryptionPolicy object, users can provide only a Key (implementing IKey), only a resolver (implementing IKeyResolver), or both.</span></span> <span data-ttu-id="207d4-224">IKey 是以金鑰識別碼來識別的基本金鑰類型，且提供包裝/解除包裝的邏輯。</span><span class="sxs-lookup"><span data-stu-id="207d4-224">IKey is the basic key type that is identified using a key identifier and that provides the logic for wrapping/unwrapping.</span></span> <span data-ttu-id="207d4-225">IKeyResolver 在解密程序期間用來解析金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-225">IKeyResolver is used to resolve a key during the decryption process.</span></span> <span data-ttu-id="207d4-226">它定義 ResolveKey 方法，可根據金鑰識別碼傳回 IKey。</span><span class="sxs-lookup"><span data-stu-id="207d4-226">It defines a ResolveKey method that returns an IKey given a key identifier.</span></span> <span data-ttu-id="207d4-227">這可讓使用者從多個位置中管理的多個金鑰之中選擇。</span><span class="sxs-lookup"><span data-stu-id="207d4-227">This provides users the ability to choose between multiple keys that are managed in multiple locations.</span></span>

* <span data-ttu-id="207d4-228">加密時一律使用金鑰，缺少金鑰將會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="207d4-228">For encryption, the key is used always and the absence of a key will result in an error.</span></span>  
* <span data-ttu-id="207d4-229">解密：</span><span class="sxs-lookup"><span data-stu-id="207d4-229">For decryption:</span></span>  
  
  * <span data-ttu-id="207d4-230">叫用金鑰解析程式 (如果指定) 以取得金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-230">The key resolver is invoked if specified to get the key.</span></span> <span data-ttu-id="207d4-231">如果已指定解析程式，但沒有金鑰識別碼的對應，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="207d4-231">If the resolver is specified but does not have a mapping for the key identifier, an error is thrown.</span></span>  
  * <span data-ttu-id="207d4-232">如果未指定解析程式但指定了金鑰，則如果其識別項符合所需的金鑰識別項，就會使用該金鑰。</span><span class="sxs-lookup"><span data-stu-id="207d4-232">If resolver is not specified but a key is specified, the key is used if its identifier matches the required key identifier.</span></span> <span data-ttu-id="207d4-233">如果識別項不符合，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="207d4-233">If the identifier does not match, an error is thrown.</span></span>  
    
    <span data-ttu-id="207d4-234">[加密範例](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) <fix URL> 會針對 Blob、佇列和資料表以及金鑰保存庫的整合，示範更詳細的端對端案例。</span><span class="sxs-lookup"><span data-stu-id="207d4-234">The [encryption samples](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) <fix URL>demonstrate a more detailed end-to-end scenario for blobs, queues and tables, along with Key Vault integration.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="207d4-235">RequireEncryption 模式</span><span class="sxs-lookup"><span data-stu-id="207d4-235">RequireEncryption mode</span></span>
<span data-ttu-id="207d4-236">使用者可以針對所有上傳和下載都必須加密的作業模式，從中選擇啟用。</span><span class="sxs-lookup"><span data-stu-id="207d4-236">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="207d4-237">在此模式中，在用戶端上嘗試上傳沒有加密原則的資料或下載未在服務上加密的資料將會失敗。</span><span class="sxs-lookup"><span data-stu-id="207d4-237">In this mode, attempts to upload data without an encryption policy or download data that is not encrypted on the service will fail on the client.</span></span> <span data-ttu-id="207d4-238">要求選項物件的 **requireEncryption** 旗標會控制此行為。</span><span class="sxs-lookup"><span data-stu-id="207d4-238">The **requireEncryption** flag of the request options object controls this behavior.</span></span> <span data-ttu-id="207d4-239">如果您的應用程式會將所有儲存在 Azure 儲存體中的物件加密，則您可以在服務用戶端服務的預設要求選項上，設定 **requireEncryption** 屬性。</span><span class="sxs-lookup"><span data-stu-id="207d4-239">If your application will encrypt all objects stored in Azure Storage, then you can set the **requireEncryption** property on the default request options for the service client object.</span></span>   

<span data-ttu-id="207d4-240">例如，使用 **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** 要求加密透過該用戶端物件所執行的所有 Blob 作業。</span><span class="sxs-lookup"><span data-stu-id="207d4-240">For example, use **CloudBlobClient.getDefaultRequestOptions().setRequireEncryption(true)** to require encryption for all blob operations performed through that client object.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="207d4-241">Blob 服務加密</span><span class="sxs-lookup"><span data-stu-id="207d4-241">Blob service encryption</span></span>
<span data-ttu-id="207d4-242">建立 **BlobEncryptionPolicy** 物件，並在要求選項中加以設定 (透過 API 或在用戶端層級使用 **DefaultRequestOptions**)。</span><span class="sxs-lookup"><span data-stu-id="207d4-242">Create a **BlobEncryptionPolicy** object and set it in the request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="207d4-243">其他一切由用戶端程式庫在內部處理。</span><span class="sxs-lookup"><span data-stu-id="207d4-243">Everything else will be handled by the client library internally.</span></span>

```java
// Create the IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create the encryption policy to be used for upload and download.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

// Set the encryption policy on the request options.
BlobRequestOptions options = new BlobRequestOptions();
options.setEncryptionPolicy(policy);

// Upload the encrypted contents to the blob.
blob.upload(stream, size, null, options, null);

// Download and decrypt the encrypted contents from the blob.
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
blob.download(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a><span data-ttu-id="207d4-244">佇列服務加密</span><span class="sxs-lookup"><span data-stu-id="207d4-244">Queue service encryption</span></span>
<span data-ttu-id="207d4-245">建立 **QueueEncryptionPolicy** 物件，並在要求選項中加以設定 (透過 API 或在用戶端層級使用 **DefaultRequestOptions**)。</span><span class="sxs-lookup"><span data-stu-id="207d4-245">Create a **QueueEncryptionPolicy** object and set it in the request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="207d4-246">其他一切由用戶端程式庫在內部處理。</span><span class="sxs-lookup"><span data-stu-id="207d4-246">Everything else will be handled by the client library internally.</span></span>

```java
// Create the IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create the encryption policy to be used for upload and download.
QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

// Add message
QueueRequestOptions options = new QueueRequestOptions();
options.setEncryptionPolicy(policy);

queue.addMessage(message, 0, 0, options, null);

// Retrieve message
CloudQueueMessage retrMessage = queue.retrieveMessage(30, options, null);
```

### <a name="table-service-encryption"></a><span data-ttu-id="207d4-247">資料表服務加密</span><span class="sxs-lookup"><span data-stu-id="207d4-247">Table service encryption</span></span>
<span data-ttu-id="207d4-248">除了建立加密原則並在要求選項上加以設定之外，您必須在 **TableRequestOptions** 中指定 **EncryptionResolver**，或在實體的 getter 與 setter 上設定 [Encrypt] 屬性。</span><span class="sxs-lookup"><span data-stu-id="207d4-248">In addition to creating an encryption policy and setting it on request options, you must either specify an **EncryptionResolver** in **TableRequestOptions**, or set the [Encrypt] attribute on the entity's getter and setter.</span></span>

### <a name="using-the-resolver"></a><span data-ttu-id="207d4-249">使用解析程式</span><span class="sxs-lookup"><span data-stu-id="207d4-249">Using the resolver</span></span>

```java
// Create the IKey used for encryption.
RsaKey key = new RsaKey("private:key1" /* key identifier */);

// Create the encryption policy to be used for upload and download.
TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

TableRequestOptions options = new TableRequestOptions()
options.setEncryptionPolicy(policy);
options.setEncryptionResolver(new EncryptionResolver() {
    public boolean encryptionResolver(String pk, String rk, String key) {
        if (key == "foo")
        {
            return true;
        }
        return false;
    }
});

// Insert Entity
currentTable.execute(TableOperation.insert(ent), options, null);

// Retrieve Entity
// No need to specify an encryption resolver for retrieve
TableRequestOptions retrieveOptions = new TableRequestOptions()
retrieveOptions.setEncryptionPolicy(policy);

TableOperation operation = TableOperation.retrieve(ent.PartitionKey, ent.RowKey, DynamicTableEntity.class);
TableResult result = currentTable.execute(operation, retrieveOptions, null);
```

### <a name="using-attributes"></a><span data-ttu-id="207d4-250">使用屬性</span><span class="sxs-lookup"><span data-stu-id="207d4-250">Using attributes</span></span>
<span data-ttu-id="207d4-251">如上所述，如果實體實作 TableEntity，則屬性可以使用 [Encrypt] 屬性裝飾 getter 與 setter 屬性，不需指定 **EncryptionResolver**。</span><span class="sxs-lookup"><span data-stu-id="207d4-251">As mentioned above, if the entity implements TableEntity, then the properties getter and setter can be decorated with the [Encrypt] attribute instead of specifying the **EncryptionResolver**.</span></span>

```java
private string encryptedProperty1;

@Encrypt
public String getEncryptedProperty1 () {
    return this.encryptedProperty1;
}

@Encrypt
public void setEncryptedProperty1(final String encryptedProperty1) {
    this.encryptedProperty1 = encryptedProperty1;
}
```

## <a name="encryption-and-performance"></a><span data-ttu-id="207d4-252">加密和效能</span><span class="sxs-lookup"><span data-stu-id="207d4-252">Encryption and performance</span></span>
<span data-ttu-id="207d4-253">請注意，加密您的儲存體資料會造成額外的效能負擔。</span><span class="sxs-lookup"><span data-stu-id="207d4-253">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="207d4-254">必須產生內容金鑰和 IV，內容本身必須經過加密，而且其他中繼資料必須格式化並上傳。</span><span class="sxs-lookup"><span data-stu-id="207d4-254">The content key and IV must be generated, the content itself must be encrypted, and additional meta-data must be formatted and uploaded.</span></span> <span data-ttu-id="207d4-255">這個額外負荷會因所加密的資料數量而有所不同。</span><span class="sxs-lookup"><span data-stu-id="207d4-255">This overhead will vary depending on the quantity of data being encrypted.</span></span> <span data-ttu-id="207d4-256">我們建議客戶一定要在開發期間測試其應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="207d4-256">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="207d4-257">後續步驟</span><span class="sxs-lookup"><span data-stu-id="207d4-257">Next steps</span></span>
* <span data-ttu-id="207d4-258">下載 [Azure Storage Client Library for Java Maven package (適用於 Java Maven 封裝的 Azure 儲存體用戶端程式庫)](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)</span><span class="sxs-lookup"><span data-stu-id="207d4-258">Download the [Azure Storage Client Library for Java Maven package](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage)</span></span>  
* <span data-ttu-id="207d4-259">從 GitHub 下載 [Azure Storage Client Library for Java Source Code (適用於 Java 原始程式碼的 Azure 儲存體用戶端程式庫)](https://github.com/Azure/azure-storage-java)</span><span class="sxs-lookup"><span data-stu-id="207d4-259">Download the [Azure Storage Client Library for Java Source Code from GitHub](https://github.com/Azure/azure-storage-java)</span></span>   
* <span data-ttu-id="207d4-260">下載適用於 Java Maven 的 Azure 金鑰保存庫 Maven 程式庫封裝：</span><span class="sxs-lookup"><span data-stu-id="207d4-260">Download the Azure Key Vault Maven Library for Java Maven packages:</span></span>
  * <span data-ttu-id="207d4-261">[核心](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) 封裝</span><span class="sxs-lookup"><span data-stu-id="207d4-261">[Core](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault-core) package</span></span>
  * <span data-ttu-id="207d4-262">[用戶端](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) 封裝</span><span class="sxs-lookup"><span data-stu-id="207d4-262">[Client](http://mvnrepository.com/artifact/com.microsoft.azure/azure-keyvault) package</span></span>
* <span data-ttu-id="207d4-263">請瀏覽 [Azure 金鑰保存庫文件](../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="207d4-263">Visit the [Azure Key Vault Documentation](../key-vault/key-vault-whatis.md)</span></span>