---
title: "Microsoft Azure 儲存體的用戶端 Python 加密 | Microsoft Docs"
description: "適用於 Python 的 Azure 儲存體用戶端程式庫支援適用於您 Azure 儲存體應用程式的最高安全性用戶端加密。"
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 25a376b2e54953602b66abc3bae878f09a776a80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a><span data-ttu-id="e6679-103">Microsoft Azure 儲存體的用戶端 Python 加密</span><span class="sxs-lookup"><span data-stu-id="e6679-103">Client-Side Encryption with Python for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="e6679-104">Overview</span><span class="sxs-lookup"><span data-stu-id="e6679-104">Overview</span></span>
<span data-ttu-id="e6679-105">[Azure Storage Client Library for Python (適用於 Python 的 Azure 儲存體用戶端程式庫)](https://pypi.python.org/pypi/azure-storage) 支援在上傳至 Azure 儲存體之前將用戶端應用程式內的資料加密，並在下載至用戶端時解密資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-105">The [Azure Storage Client Library for Python](https://pypi.python.org/pypi/azure-storage) supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="e6679-106">Azure Storage Python 程式庫目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="e6679-106">The Azure Storage Python library is in preview.</span></span>
> 
> 

## <a name="encryption-and-decryption-via-the-envelope-technique"></a><span data-ttu-id="e6679-107">透過信封技術進行加密和解密</span><span class="sxs-lookup"><span data-stu-id="e6679-107">Encryption and decryption via the envelope technique</span></span>
<span data-ttu-id="e6679-108">加密和解密的程序採用信封技術。</span><span class="sxs-lookup"><span data-stu-id="e6679-108">The processes of encryption and decryption follow the envelope technique.</span></span>

### <a name="encryption-via-the-envelope-technique"></a><span data-ttu-id="e6679-109">透過信封技術加密</span><span class="sxs-lookup"><span data-stu-id="e6679-109">Encryption via the envelope technique</span></span>
<span data-ttu-id="e6679-110">透過信封技術加密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="e6679-110">Encryption via the envelope technique works in the following way:</span></span>

1. <span data-ttu-id="e6679-111">Azure 儲存體用戶端程式庫會產生內容加密金鑰 (CEK)，這是使用一次的對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-111">The Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="e6679-112">使用此 CEK 加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-112">User data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="e6679-113">然後使用金鑰加密金鑰 (KEK) 包裝 (加密) CEK。</span><span class="sxs-lookup"><span data-stu-id="e6679-113">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="e6679-114">KEK 是以金鑰識別碼識別，且可以是在本機管理的非對稱金鑰組或對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-114">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key, which is managed locally.</span></span>
   <span data-ttu-id="e6679-115">儲存體用戶端程式庫本身永遠沒有 KEK 的存取權。</span><span class="sxs-lookup"><span data-stu-id="e6679-115">The storage client library itself never has access to KEK.</span></span> <span data-ttu-id="e6679-116">程式庫會叫用 KEK 所提供的金鑰包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="e6679-116">The library invokes the key wrapping algorithm that is provided by the KEK.</span></span> <span data-ttu-id="e6679-117">如有需要，使用者可以選擇使用自訂提供者來包裝/取消包裝金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-117">Users can choose to use custom providers for key wrapping/unwrapping if desired.</span></span>
4. <span data-ttu-id="e6679-118">然後，將加密的資料上傳至 Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="e6679-118">The encrypted data is then uploaded to the Azure Storage service.</span></span> <span data-ttu-id="e6679-119">包裝的金鑰及一些其他加密中繼資料會儲存為中繼資料 (在 blob 上)，或插補加密的資料 (訊息佇列和資料表實體)。</span><span class="sxs-lookup"><span data-stu-id="e6679-119">The wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with the encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-the-envelope-technique"></a><span data-ttu-id="e6679-120">透過信封技術解密</span><span class="sxs-lookup"><span data-stu-id="e6679-120">Decryption via the envelope technique</span></span>
<span data-ttu-id="e6679-121">透過信封技術解密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="e6679-121">Decryption via the envelope technique works in the following way:</span></span>

1. <span data-ttu-id="e6679-122">用戶端程式庫假設使用者在本機管理金鑰加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="e6679-122">The client library assumes that the user is managing the key encryption key (KEK) locally.</span></span> <span data-ttu-id="e6679-123">使用者不必知道用於加密的特定金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-123">The user does not need to know the specific key that was used for encryption.</span></span> <span data-ttu-id="e6679-124">相反地，可以設定並使用金鑰解析程式，將不同的金鑰識別碼解析成金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-124">Instead, a key resolver, which resolves different key identifiers to keys, can be set up and used.</span></span>
2. <span data-ttu-id="e6679-125">用戶端程式庫會下載加密的資料，以及儲存在服務上的任何加密資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-125">The client library downloads the encrypted data along with any encryption material that is stored on the service.</span></span>
3. <span data-ttu-id="e6679-126">然後，使用金鑰加密金鑰 (KEK) 將已包裝的內容加密金鑰 (CEK) 解除包裝 (解密)。</span><span class="sxs-lookup"><span data-stu-id="e6679-126">The wrapped content encryption key (CEK) is then unwrapped (decrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="e6679-127">同樣地，用戶端程式庫在此沒有 KEK 的存取權。</span><span class="sxs-lookup"><span data-stu-id="e6679-127">Here again, the client library does not have access to KEK.</span></span> <span data-ttu-id="e6679-128">它只會叫用自訂提供者的解除包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="e6679-128">It simply invokes the custom provider's unwrapping algorithm.</span></span>
4. <span data-ttu-id="e6679-129">然後，使用內容加密金鑰 (CEK) 解密已加密的使用者資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-129">The content encryption key (CEK) is then used to decrypt the encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="e6679-130">加密機制</span><span class="sxs-lookup"><span data-stu-id="e6679-130">Encryption Mechanism</span></span>
<span data-ttu-id="e6679-131">儲存體用戶端程式庫會使用 [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 來加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-131">The storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order to encrypt user data.</span></span> <span data-ttu-id="e6679-132">具體來說，就是 [加密區塊鏈結 (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 模式搭配 AES。</span><span class="sxs-lookup"><span data-stu-id="e6679-132">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="e6679-133">每個服務的運作方式稍有不同，我們將在這裡討論每個服務。</span><span class="sxs-lookup"><span data-stu-id="e6679-133">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="e6679-134">Blob</span><span class="sxs-lookup"><span data-stu-id="e6679-134">Blobs</span></span>
<span data-ttu-id="e6679-135">用戶端程式庫目前僅支援整個 Blob 的加密。</span><span class="sxs-lookup"><span data-stu-id="e6679-135">The client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="e6679-136">明確地說，加密會在使用者使用 **create*** 方法時受到支援。</span><span class="sxs-lookup"><span data-stu-id="e6679-136">Specifically, encryption is supported when users use the **create*** methods.</span></span> <span data-ttu-id="e6679-137">針對下載項目同時支援完整與範圍下載，也提供上傳與下載的平行處理。</span><span class="sxs-lookup"><span data-stu-id="e6679-137">For downloads, both complete and range downloads are supported, and parallelization of both upload and download is available.</span></span>

<span data-ttu-id="e6679-138">在加密期間，用戶端程式庫會產生 16 位元組的隨機初始化向量 (IV)，以及 32 位元組的隨機內容加密金鑰 (CEK)，並使用這項資訊執行 blob 資料的信封加密。</span><span class="sxs-lookup"><span data-stu-id="e6679-138">During encryption, the client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of the blob data using this information.</span></span> <span data-ttu-id="e6679-139">然後，已包裝的 CEK 和一些其他加密中繼資料會儲存為 blob 中繼資料，並連同加密的 blob 一起儲存在服務上。</span><span class="sxs-lookup"><span data-stu-id="e6679-139">The wrapped CEK and some additional encryption metadata are then stored as blob metadata along with the encrypted blob on the service.</span></span>

> [!WARNING]
> <span data-ttu-id="e6679-140">如果您要為 blob 編輯或上傳您自己的中繼資料，則必須確定保留此中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-140">If you are editing or uploading your own metadata for the blob, you need to ensure that this metadata is preserved.</span></span> <span data-ttu-id="e6679-141">如果您上傳新的中繼資料，但缺少此中繼資料，包裝的 CEK、IV 和其他中繼資料將會遺失，而且永遠無法再擷取 blob 內容。</span><span class="sxs-lookup"><span data-stu-id="e6679-141">If you upload new metadata without this metadata, the wrapped CEK, IV and other metadata will be lost and the blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="e6679-142">下載加密的 Blob 牽涉到使用 **get*** 便利性方法擷取整個 Blob 內容。</span><span class="sxs-lookup"><span data-stu-id="e6679-142">Downloading an encrypted blob involves retrieving the content of the entire blob using the **get*** convenience methods.</span></span> <span data-ttu-id="e6679-143">包裝的 CEK 會解除包裝，並與 IV (在此情況下儲存為 blob 中繼資料) 一起用來傳回解密的資料給使用者。</span><span class="sxs-lookup"><span data-stu-id="e6679-143">The wrapped CEK is unwrapped and used together with the IV (stored as blob metadata in this case) to return the decrypted data to the users.</span></span>

<span data-ttu-id="e6679-144">在加密的 Blob 中下載任意範圍 (包含傳入的範圍參數的**get*** 方法)，牽涉到調整使用者所提供的範圍，以藉此取得少量額外的資料以便用來成功解密所要求的範圍。</span><span class="sxs-lookup"><span data-stu-id="e6679-144">Downloading an arbitrary range (**get*** methods with range parameters passed in) in the encrypted blob involves adjusting the range provided by users in order to get a small amount of additional data that can be used to successfully decrypt the requested range.</span></span>

<span data-ttu-id="e6679-145">區塊 Blob 和分頁 Blob 只可以使用這種配置加密/解密。</span><span class="sxs-lookup"><span data-stu-id="e6679-145">Block blobs and page blobs only can be encrypted/decrypted using this scheme.</span></span> <span data-ttu-id="e6679-146">目前不支援加密附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="e6679-146">There is currently no support for encrypting append blobs.</span></span>

### <a name="queues"></a><span data-ttu-id="e6679-147">佇列</span><span class="sxs-lookup"><span data-stu-id="e6679-147">Queues</span></span>
<span data-ttu-id="e6679-148">因為佇列訊息可以是任何格式，用戶端程式庫會定義自訂的格式，其中包含訊息文字中的初始化向量 (IV) 和加密的內容加密金鑰 (CEK)。</span><span class="sxs-lookup"><span data-stu-id="e6679-148">Since queue messages can be of any format, the client library defines a custom format that includes the Initialization Vector (IV) and the encrypted content encryption key (CEK) in the message text.</span></span>

<span data-ttu-id="e6679-149">在加密期間，用戶端程式庫會產生 16 位元組的隨機 IV，以及 32 位元組的隨機 CEK，並使用這項資訊執行佇列訊息文字的信封加密。</span><span class="sxs-lookup"><span data-stu-id="e6679-149">During encryption, the client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of the queue message text using this information.</span></span> <span data-ttu-id="e6679-150">然後，已包裝的 CEK 和一些其他加密中繼資料會加入至已加密的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="e6679-150">The wrapped CEK and some additional encryption metadata are then added to the encrypted queue message.</span></span> <span data-ttu-id="e6679-151">這個修改過的訊息 (如下所示) 會儲存在服務上。</span><span class="sxs-lookup"><span data-stu-id="e6679-151">This modified message (shown below) is stored on the service.</span></span>

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

<span data-ttu-id="e6679-152">在解密期間，從佇列訊息中擷取已包裝的金鑰，並解除包裝。</span><span class="sxs-lookup"><span data-stu-id="e6679-152">During decryption, the wrapped key is extracted from the queue message and unwrapped.</span></span> <span data-ttu-id="e6679-153">IV 也會從佇列訊息中擷取，並與未包裝的金鑰一起用來解密佇列訊息資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-153">The IV is also extracted from the queue message and used along with the unwrapped key to decrypt the queue message data.</span></span> <span data-ttu-id="e6679-154">請注意，加密中繼資料很小 (小於 500 位元組)，雖然計入佇列訊息的 64KB 限制內，但影響仍在可掌控的範圍內。</span><span class="sxs-lookup"><span data-stu-id="e6679-154">Note that the encryption metadata is small (under 500 bytes), so while it does count toward the 64KB limit for a queue message, the impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="e6679-155">資料表</span><span class="sxs-lookup"><span data-stu-id="e6679-155">Tables</span></span>
<span data-ttu-id="e6679-156">用戶端程式庫支援在插入和取代作業時進行實體屬性的加密。</span><span class="sxs-lookup"><span data-stu-id="e6679-156">The client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="e6679-157">目前不支援合併。</span><span class="sxs-lookup"><span data-stu-id="e6679-157">Merge is not currently supported.</span></span> <span data-ttu-id="e6679-158">因為屬性子集先前可能是使用不同的金鑰加密，直接合併新的屬性並更新中繼資料會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="e6679-158">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="e6679-159">合併可能需要額外的服務呼叫來從服務讀取預先存在的實體，或在每個屬性上都使用新的金鑰，兩者都不利用於效能。</span><span class="sxs-lookup"><span data-stu-id="e6679-159">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="e6679-160">資料表資料加密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="e6679-160">Table data encryption works as follows:</span></span>

1. <span data-ttu-id="e6679-161">使用者指定要加密的屬性。</span><span class="sxs-lookup"><span data-stu-id="e6679-161">Users specify the properties to be encrypted.</span></span>
2. <span data-ttu-id="e6679-162">用戶端程式庫會針對每個實體產生 16 位元組的隨機初始化向量 (IV) 以及 32 位元組的隨機內容加密金鑰 (CEK)，並在個別屬性上執行信封加密，使每個屬性衍生新的 IV，藉此進行加密。</span><span class="sxs-lookup"><span data-stu-id="e6679-162">The client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on the individual properties to be encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="e6679-163">加密的屬性會儲存為二進位資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-163">The encrypted property is stored as binary data.</span></span>
3. <span data-ttu-id="e6679-164">然後，已包裝的 CEK 和一些其他加密中繼資料會儲存成額外兩個保留的屬性。</span><span class="sxs-lookup"><span data-stu-id="e6679-164">The wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="e6679-165">第一個保留的屬性 (\_ClientEncryptionMetadata1) 是字串屬性，保存 IV、版本和已包裝的金鑰的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e6679-165">The first reserved property (\_ClientEncryptionMetadata1) is a string property that holds the information about IV, version, and wrapped key.</span></span> <span data-ttu-id="e6679-166">第二個保留的屬性 (\_ClientEncryptionMetadata2) 二進位屬性，其保留已加密之屬性的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e6679-166">The second reserved property (\_ClientEncryptionMetadata2) is a binary property that holds the information about the properties that are encrypted.</span></span> <span data-ttu-id="e6679-167">此第二個屬性 (\_ClientEncryptionMetadata2) 中的資訊已自行加密。</span><span class="sxs-lookup"><span data-stu-id="e6679-167">The information in this second property (\_ClientEncryptionMetadata2) is itself encrypted.</span></span>
4. <span data-ttu-id="e6679-168">由於加密需要這些額外保留的屬性，使用者現在可能只有 250 個自訂屬性，而不是 252 個。</span><span class="sxs-lookup"><span data-stu-id="e6679-168">Due to these additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="e6679-169">實體的總大小必須小於 1MB。</span><span class="sxs-lookup"><span data-stu-id="e6679-169">The total size of the entity must be less than 1MB.</span></span>
   
   <span data-ttu-id="e6679-170">請注意，只有字串屬性可以加密。</span><span class="sxs-lookup"><span data-stu-id="e6679-170">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="e6679-171">如果有其他類型的屬性需要加密，則必須轉換成字串。</span><span class="sxs-lookup"><span data-stu-id="e6679-171">If other types of properties are to be encrypted, they must be converted to strings.</span></span> <span data-ttu-id="e6679-172">加密的字串會做為二進位屬性儲存在服務上，並在解密後轉換回字串 (原始字串，而不是具有 EdmType.STRING 類型的 EntityProperties)。</span><span class="sxs-lookup"><span data-stu-id="e6679-172">The encrypted strings are stored on the service as binary properties, and they are converted back to strings (raw strings, not EntityProperties with type EdmType.STRING) after decryption.</span></span>
   
   <span data-ttu-id="e6679-173">針對資料表，除了加密原則之外，使用者必須指定要加密的屬性。</span><span class="sxs-lookup"><span data-stu-id="e6679-173">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="e6679-174">這可透過將這些屬性儲存於 TableEntity 物件中並設定類型為 EdmType.STRING 且將加密設定為 true，或是在 tableservice 物件上設定 encryption_resolver_function。</span><span class="sxs-lookup"><span data-stu-id="e6679-174">This can be done by either storing these properties in TableEntity objects with the type set to EdmType.STRING and encrypt set to true or setting the encryption_resolver_function on the tableservice object.</span></span> <span data-ttu-id="e6679-175">加密解析程式是函式，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。</span><span class="sxs-lookup"><span data-stu-id="e6679-175">An encryption resolver is a function that takes a partition key, row key, and property name and returns a boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="e6679-176">在加密期間，用戶端程式庫會使用此資訊，決定將屬性在寫到網路時是否應該加密。</span><span class="sxs-lookup"><span data-stu-id="e6679-176">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="e6679-177">委派也提供關於屬性如何加密的可能邏輯。</span><span class="sxs-lookup"><span data-stu-id="e6679-177">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="e6679-178">(例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，讀取或查詢實體時不需要提供這項資訊。</span><span class="sxs-lookup"><span data-stu-id="e6679-178">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="e6679-179">批次作業</span><span class="sxs-lookup"><span data-stu-id="e6679-179">Batch Operations</span></span>
<span data-ttu-id="e6679-180">單一加密原則適用於批次中的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="e6679-180">One encryption policy applies to all rows in the batch.</span></span> <span data-ttu-id="e6679-181">用戶端程式庫會在內部為批次中的每個資料列產生新的隨機 IV 和隨機 CEK。</span><span class="sxs-lookup"><span data-stu-id="e6679-181">The client library will internally generate a new random IV and random CEK per row in the batch.</span></span> <span data-ttu-id="e6679-182">使用者也可以選擇為批次中的每個作業加密不同的屬性，作法是在加密解析程式中定義此行為。</span><span class="sxs-lookup"><span data-stu-id="e6679-182">Users can also choose to encrypt different properties for every operation in the batch by defining this behavior in the encryption resolver.</span></span>
<span data-ttu-id="e6679-183">如果批次透過 tableservice batch() 方法建立為內容管理員，則 tableservice 加密原則會自動套用至批次。</span><span class="sxs-lookup"><span data-stu-id="e6679-183">If a batch is created as a context manager through the tableservice batch() method, the tableservice's encryption policy will automatically be applied to the batch.</span></span> <span data-ttu-id="e6679-184">如果批次是由呼叫建構函式而明確建立，則加密原則就必須做為參數傳遞，並在批次的存留期內保持未修改的狀態。</span><span class="sxs-lookup"><span data-stu-id="e6679-184">If a batch is created explicitly by calling the constructor, the encryption policy must be passed as a parameter and left unmodified for the lifetime of the batch.</span></span>
<span data-ttu-id="e6679-185">請注意，實體會在使用批次的加密原則插入批次中時受到加密 (實體在使用 tableservice 的加密原則認可批次時將不會受到加密)。</span><span class="sxs-lookup"><span data-stu-id="e6679-185">Note that entities are encrypted as they are inserted into the batch using the batch's encryption policy (entities are NOT encrypted at the time of committing the batch using the tableservice's encryption policy).</span></span>

### <a name="queries"></a><span data-ttu-id="e6679-186">查詢</span><span class="sxs-lookup"><span data-stu-id="e6679-186">Queries</span></span>
<span data-ttu-id="e6679-187">若要執行查詢作業，您必須指定一個能夠解析結果集中的所有金鑰的金鑰解析程式。</span><span class="sxs-lookup"><span data-stu-id="e6679-187">To perform query operations, you must specify a key resolver that is able to resolve all the keys in the result set.</span></span> <span data-ttu-id="e6679-188">如果查詢結果中包含的實體無法解析成提供者，用戶端程式庫會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="e6679-188">If an entity contained in the query result cannot be resolved to a provider, the client library will throw an error.</span></span> <span data-ttu-id="e6679-189">針對執行伺服器端投影的任何查詢，用戶端程式庫會依預設將特殊加密中繼資料屬性 (\_ClientEncryptionMetadata1 和 \_ClientEncryptionMetadata2) 加入選取的資料行。</span><span class="sxs-lookup"><span data-stu-id="e6679-189">For any query that performs server side projections, the client library will add the special encryption metadata properties (\_ClientEncryptionMetadata1 and \_ClientEncryptionMetadata2) by default to the selected columns.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6679-190">使用用戶端加密時，請留意以下重點：</span><span class="sxs-lookup"><span data-stu-id="e6679-190">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="e6679-191">讀取或寫入加密的 Blob 時，使用整個 Blob 上傳命令及範圍/整個 Blob 下載命令。</span><span class="sxs-lookup"><span data-stu-id="e6679-191">When reading from or writing to an encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="e6679-192">避免使用通訊協定作業寫入加密的 Blob，例如放置區塊、放置區塊清單、撰寫頁面或清除頁面；否則您可能會損毀加密的 Blob，並使它無法讀取。</span><span class="sxs-lookup"><span data-stu-id="e6679-192">Avoid writing to an encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, or Clear Pages; otherwise you may corrupt the encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="e6679-193">對於資料表，存在類似的條件約束。</span><span class="sxs-lookup"><span data-stu-id="e6679-193">For tables, a similar constraint exists.</span></span> <span data-ttu-id="e6679-194">請小心在未更新加密中繼資料時即更新加密的內容。</span><span class="sxs-lookup"><span data-stu-id="e6679-194">Be careful to not update encrypted properties without updating the encryption metadata.</span></span>
> * <span data-ttu-id="e6679-195">如果您在加密 Blob 上設定中繼資料，您可能會覆寫加密所需的加密相關中繼資料，因為設定中繼資料不是加總解密。</span><span class="sxs-lookup"><span data-stu-id="e6679-195">If you set metadata on the encrypted blob, you may overwrite the encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="e6679-196">快照集也是如此。在為加密的 Blob 建立快照集時，請避免指定中繼資料。</span><span class="sxs-lookup"><span data-stu-id="e6679-196">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="e6679-197">如果必須設定中繼資料，請務必先呼叫 **get_blob_metadata** 方法，以取得目前的加密中繼資料，並避免在設定中繼資料時並行寫入。</span><span class="sxs-lookup"><span data-stu-id="e6679-197">If metadata must be set, be sure to call the **get_blob_metadata** method first to get the current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>
> * <span data-ttu-id="e6679-198">針對僅能使用加密資料的使用者，請在服務物件上啟用 **require_encryption** 旗標。</span><span class="sxs-lookup"><span data-stu-id="e6679-198">Enable the **require_encryption** flag on the service object for users that should work only with encrypted data.</span></span> <span data-ttu-id="e6679-199">如需詳細資訊請參閱下方內容。</span><span class="sxs-lookup"><span data-stu-id="e6679-199">See below for more info.</span></span>
> 
> 

<span data-ttu-id="e6679-200">儲存體用戶端程式庫預期提供的 KEK 與金鑰解析程式會實作下列介面。</span><span class="sxs-lookup"><span data-stu-id="e6679-200">The storage client library expects the provided KEK and key resolver to implement the following interface.</span></span> <span data-ttu-id="e6679-201">[Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/) 支援尚未推出，並會在完成時整合到此程式庫。</span><span class="sxs-lookup"><span data-stu-id="e6679-201">[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) support for Python KEK management is pending and will be integrated into this library when completed.</span></span>

## <a name="client-api--interface"></a><span data-ttu-id="e6679-202">用戶端 API / 介面</span><span class="sxs-lookup"><span data-stu-id="e6679-202">Client API / Interface</span></span>
<span data-ttu-id="e6679-203">在建立儲存體服務物件 (亦即 blockblobservice) 之後，使用者可以將值指派到構成加密原則的欄位：key_encryption_key、key_resolver_function 和 require_encryption。</span><span class="sxs-lookup"><span data-stu-id="e6679-203">After a storage service object (i.e. blockblobservice) has been created, the user may assign values to the fields that constitute an encryption policy: key_encryption_key, key_resolver_function, and require_encryption.</span></span> <span data-ttu-id="e6679-204">使用者可以僅提供 KEK、僅提供解析程式，或是兩者皆提供。</span><span class="sxs-lookup"><span data-stu-id="e6679-204">Users can provide only a KEK, only a resolver, or both.</span></span> <span data-ttu-id="e6679-205">key_encryption_key 是以金鑰識別碼來識別的基本金鑰類型，且提供包裝/解除包裝的邏輯。</span><span class="sxs-lookup"><span data-stu-id="e6679-205">key_encryption_key is the basic key type that is identified using a key identifier and that provides the logic for wrapping/unwrapping.</span></span> <span data-ttu-id="e6679-206">key_resolver_function 在解密程序期間用來解析金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-206">key_resolver_function is used to resolve a key during the decryption process.</span></span> <span data-ttu-id="e6679-207">它會傳回指定金鑰識別碼的有效 KEK。</span><span class="sxs-lookup"><span data-stu-id="e6679-207">It returns a valid KEK given a key identifier.</span></span> <span data-ttu-id="e6679-208">這可讓使用者從多個位置中管理的多個金鑰之中選擇。</span><span class="sxs-lookup"><span data-stu-id="e6679-208">This provides users the ability to choose between multiple keys that are managed in multiple locations.</span></span>

<span data-ttu-id="e6679-209">KEK 必須實作下列方法以成功加密資料︰</span><span class="sxs-lookup"><span data-stu-id="e6679-209">The KEK must implement the following methods to successfully encrypt data:</span></span>

* <span data-ttu-id="e6679-210">wrap_key(cek)：使用使用者選擇的演算法包裝指定的 CEK (位元組)。</span><span class="sxs-lookup"><span data-stu-id="e6679-210">wrap_key(cek): Wraps the specified CEK (bytes) using an algorithm of the user's choice.</span></span> <span data-ttu-id="e6679-211">傳回已包裝的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-211">Returns the wrapped key.</span></span>
* <span data-ttu-id="e6679-212">get_key_wrap_algorithm()：傳回用來包裝金鑰的演算法。</span><span class="sxs-lookup"><span data-stu-id="e6679-212">get_key_wrap_algorithm(): Returns the algorithm used to wrap keys.</span></span>
* <span data-ttu-id="e6679-213">get_kid()：傳回此 KEK 的字串金鑰識別碼。</span><span class="sxs-lookup"><span data-stu-id="e6679-213">get_kid(): Returns the string key id for this KEK.</span></span>
  <span data-ttu-id="e6679-214">KEK 必須實作下列方法以成功解密資料︰</span><span class="sxs-lookup"><span data-stu-id="e6679-214">The KEK must implement the following methods to successfully decrypt data:</span></span>
* <span data-ttu-id="e6679-215">unwrap_key(cek, algorithm)：使用字串指定演算法傳回未包裝形式的指定 CEK。</span><span class="sxs-lookup"><span data-stu-id="e6679-215">unwrap_key(cek, algorithm): Returns the unwrapped form of the specified CEK using the string-specified algorithm.</span></span>
* <span data-ttu-id="e6679-216">get_kid()：傳回此 KEK 的字串金鑰識別碼。</span><span class="sxs-lookup"><span data-stu-id="e6679-216">get_kid(): Returns a string key id for this KEK.</span></span>

<span data-ttu-id="e6679-217">金鑰解析程式至少必須實作在指定金鑰識別碼的情況下會傳回實作上述介面之對應 KEK 的方法。</span><span class="sxs-lookup"><span data-stu-id="e6679-217">The key resolver must at least implement a method that, given a key id, returns the corresponding KEK implementing the interface above.</span></span> <span data-ttu-id="e6679-218">只有這個方法可以指派給服務物件上的 key_resolver_function 屬性。</span><span class="sxs-lookup"><span data-stu-id="e6679-218">Only this method is to be assigned to the key_resolver_function property on the service object.</span></span>

* <span data-ttu-id="e6679-219">加密時一律使用金鑰，缺少金鑰將會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="e6679-219">For encryption, the key is used always and the absence of a key will result in an error.</span></span>
* <span data-ttu-id="e6679-220">解密：</span><span class="sxs-lookup"><span data-stu-id="e6679-220">For decryption:</span></span>
  
  * <span data-ttu-id="e6679-221">叫用金鑰解析程式 (如果指定) 以取得金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-221">The key resolver is invoked if specified to get the key.</span></span> <span data-ttu-id="e6679-222">如果已指定解析程式，但沒有金鑰識別碼的對應，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="e6679-222">If the resolver is specified but does not have a mapping for the key identifier, an error is thrown.</span></span>
  * <span data-ttu-id="e6679-223">如果未指定解析程式但指定了金鑰，則如果其識別項符合所需的金鑰識別項，就會使用該金鑰。</span><span class="sxs-lookup"><span data-stu-id="e6679-223">If resolver is not specified but a key is specified, the key is used if its identifier matches the required key identifier.</span></span> <span data-ttu-id="e6679-224">如果識別項不符合，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="e6679-224">If the identifier does not match, an error is thrown.</span></span>
    
    <span data-ttu-id="e6679-225">azure.storage.samples <fix URL> 中的加密範例示範了針對 Blob、佇列及資料表更為詳細的端對端案例。</span><span class="sxs-lookup"><span data-stu-id="e6679-225">The encryption samples in azure.storage.samples <fix URL>demonstrate a more detailed end-to-end scenario for blobs, queues and tables.</span></span>
      <span data-ttu-id="e6679-226">KEK 與金鑰解析程式的實作範例已在範例檔案中以 KeyWrapper 和 KeyResolver 的形式個別提供。</span><span class="sxs-lookup"><span data-stu-id="e6679-226">Sample implementations of the KEK and key resolver are provided in the sample files as KeyWrapper and KeyResolver respectively.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="e6679-227">RequireEncryption 模式</span><span class="sxs-lookup"><span data-stu-id="e6679-227">RequireEncryption mode</span></span>
<span data-ttu-id="e6679-228">使用者可以針對所有上傳和下載都必須加密的作業模式，從中選擇啟用。</span><span class="sxs-lookup"><span data-stu-id="e6679-228">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="e6679-229">在此模式中，在用戶端上嘗試上傳沒有加密原則的資料或下載未在服務上加密的資料將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e6679-229">In this mode, attempts to upload data without an encryption policy or download data that is not encrypted on the service will fail on the client.</span></span> <span data-ttu-id="e6679-230">服務物件上的 **require_encryption** 旗標會控制此行為。</span><span class="sxs-lookup"><span data-stu-id="e6679-230">The **require_encryption** flag on the service object controls this behavior.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="e6679-231">Blob 服務加密</span><span class="sxs-lookup"><span data-stu-id="e6679-231">Blob service encryption</span></span>
<span data-ttu-id="e6679-232">在 blockblobservice 物件上設定加密原則欄位。</span><span class="sxs-lookup"><span data-stu-id="e6679-232">Set the encryption policy fields on the blockblobservice object.</span></span> <span data-ttu-id="e6679-233">其他一切由用戶端程式庫在內部處理。</span><span class="sxs-lookup"><span data-stu-id="e6679-233">Everything else will be handled by the client library internally.</span></span>

```python
# Create the KEK used for encryption.
# KeyWrapper is the provided sample implementation, but the user may use their own object as long as it implements the interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create the key resolver used for decryption.
# KeyResolver is the provided sample implementation, but the user may use whatever implementation they choose so long as the function set on the service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set the KEK and key resolver on the service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload the encrypted contents to the blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt the encrypted contents from the blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a><span data-ttu-id="e6679-234">佇列服務加密</span><span class="sxs-lookup"><span data-stu-id="e6679-234">Queue service encryption</span></span>
<span data-ttu-id="e6679-235">在 queueservice 物件上設定加密原則欄位。</span><span class="sxs-lookup"><span data-stu-id="e6679-235">Set the encryption policy fields on the queueservice object.</span></span> <span data-ttu-id="e6679-236">其他一切由用戶端程式庫在內部處理。</span><span class="sxs-lookup"><span data-stu-id="e6679-236">Everything else will be handled by the client library internally.</span></span>

```python
# Create the KEK used for encryption.
# KeyWrapper is the provided sample implementation, but the user may use their own object as long as it implements the interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create the key resolver used for decryption.
# KeyResolver is the provided sample implementation, but the user may use whatever implementation they choose so long as the function set on the service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set the KEK and key resolver on the service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a><span data-ttu-id="e6679-237">資料表服務加密</span><span class="sxs-lookup"><span data-stu-id="e6679-237">Table service encryption</span></span>
<span data-ttu-id="e6679-238">除了建立加密原則並在要求選項上設定它之外，您必須在 **tableservice** 上指定 **encryption_resolver_function**，或在 EntityProperty 上設定加密屬性。</span><span class="sxs-lookup"><span data-stu-id="e6679-238">In addition to creating an encryption policy and setting it on request options, you must either specify an **encryption_resolver_function** on the **tableservice**, or set the encrypt attribute on the EntityProperty.</span></span>

### <a name="using-the-resolver"></a><span data-ttu-id="e6679-239">使用解析程式</span><span class="sxs-lookup"><span data-stu-id="e6679-239">Using the resolver</span></span>

```python
# Create the KEK used for encryption.
# KeyWrapper is the provided sample implementation, but the user may use their own object as long as it implements the interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create the key resolver used for decryption.
# KeyResolver is the provided sample implementation, but the user may use whatever implementation they choose so long as the function set on the service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define the encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set the KEK and key resolver on the service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need to specify an encryption resolver for retrieve, but it is harmless to leave the property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a><span data-ttu-id="e6679-240">使用屬性</span><span class="sxs-lookup"><span data-stu-id="e6679-240">Using attributes</span></span>
<span data-ttu-id="e6679-241">如上所述，透過將屬性儲存在 EntityProperty 物件中並設定加密欄位，便可能對該屬性進行加密標記。</span><span class="sxs-lookup"><span data-stu-id="e6679-241">As mentioned above, a property may be marked for encryption by storing it in an EntityProperty object and setting the encrypt field.</span></span>

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a><span data-ttu-id="e6679-242">加密和效能</span><span class="sxs-lookup"><span data-stu-id="e6679-242">Encryption and performance</span></span>
<span data-ttu-id="e6679-243">請注意，加密您的儲存體資料會造成額外的效能負擔。</span><span class="sxs-lookup"><span data-stu-id="e6679-243">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="e6679-244">必須產生內容金鑰和 IV，內容本身必須經過加密，而且其他中繼資料必須格式化並上傳。</span><span class="sxs-lookup"><span data-stu-id="e6679-244">The content key and IV must be generated, the content itself must be encrypted, and additional metadata must be formatted and uploaded.</span></span> <span data-ttu-id="e6679-245">這個額外負荷會因所加密的資料數量而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e6679-245">This overhead will vary depending on the quantity of data being encrypted.</span></span> <span data-ttu-id="e6679-246">我們建議客戶一定要在開發期間測試其應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="e6679-246">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6679-247">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6679-247">Next steps</span></span>
* <span data-ttu-id="e6679-248">下載 [適用於 Java PyPi 封裝的 Azure 儲存體用戶端程式庫](https://pypi.python.org/pypi/azure-storage)</span><span class="sxs-lookup"><span data-stu-id="e6679-248">Download the [Azure Storage Client Library for Java PyPi package](https://pypi.python.org/pypi/azure-storage)</span></span>
* <span data-ttu-id="e6679-249">從 GitHub 下載 [適用於 Python 的 Azure 儲存體用戶端程式庫來源程式碼](https://github.com/Azure/azure-storage-python)</span><span class="sxs-lookup"><span data-stu-id="e6679-249">Download the [Azure Storage Client Library for Python Source Code from GitHub](https://github.com/Azure/azure-storage-python)</span></span>