---
title: "Microsoft Azure 儲存體使用 Python aaaClient 端加密 |Microsoft 文件"
description: "hello Python 的 Azure 儲存體用戶端程式庫支援用戶端加密您的 Azure 儲存體應用程式最高的安全性。"
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
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a><span data-ttu-id="f0051-103">Microsoft Azure 儲存體的用戶端 Python 加密</span><span class="sxs-lookup"><span data-stu-id="f0051-103">Client-Side Encryption with Python for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="f0051-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f0051-104">Overview</span></span>
<span data-ttu-id="f0051-105">hello [Python 的 Azure 儲存體用戶端程式庫](https://pypi.python.org/pypi/azure-storage)支援 tooAzure 存放裝置，將上傳和下載 toohello 用戶端時解密資料之前加密用戶端應用程式內的資料。</span><span class="sxs-lookup"><span data-stu-id="f0051-105">hello [Azure Storage Client Library for Python](https://pypi.python.org/pypi/azure-storage) supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span>

> [!NOTE]
> <span data-ttu-id="f0051-106">hello Azure 儲存體 Python 程式庫為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="f0051-106">hello Azure Storage Python library is in preview.</span></span>
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a><span data-ttu-id="f0051-107">加密和解密透過 hello 信封技術</span><span class="sxs-lookup"><span data-stu-id="f0051-107">Encryption and decryption via hello envelope technique</span></span>
<span data-ttu-id="f0051-108">加密和解密的 hello 處理程序遵循 hello 信封技術。</span><span class="sxs-lookup"><span data-stu-id="f0051-108">hello processes of encryption and decryption follow hello envelope technique.</span></span>

### <a name="encryption-via-hello-envelope-technique"></a><span data-ttu-id="f0051-109">加密透過 hello 信封技術</span><span class="sxs-lookup"><span data-stu-id="f0051-109">Encryption via hello envelope technique</span></span>
<span data-ttu-id="f0051-110">透過 hello 信封技術的加密方式 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="f0051-110">Encryption via hello envelope technique works in hello following way:</span></span>

1. <span data-ttu-id="f0051-111">hello Azure 儲存體用戶端程式庫產生的內容加密金鑰 (CEK)，這是一次性單次使用對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0051-111">hello Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="f0051-112">使用此 CEK 加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="f0051-112">User data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="f0051-113">hello CEK 然後再包裝 （加密） 使用 hello 金鑰的加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="f0051-113">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="f0051-114">hello KEK 索引鍵的識別項所識別，而且可以是對稱的金鑰組或對稱金鑰，本機管理。</span><span class="sxs-lookup"><span data-stu-id="f0051-114">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key, which is managed locally.</span></span>
   <span data-ttu-id="f0051-115">hello 儲存體用戶端程式庫本身完全不需要存取 tooKEK。</span><span class="sxs-lookup"><span data-stu-id="f0051-115">hello storage client library itself never has access tooKEK.</span></span> <span data-ttu-id="f0051-116">hello 程式庫會叫用 hello 金鑰包裝演算法所提供的 hello KEK。</span><span class="sxs-lookup"><span data-stu-id="f0051-116">hello library invokes hello key wrapping algorithm that is provided by hello KEK.</span></span> <span data-ttu-id="f0051-117">使用者可以選擇 toouse 為金鑰包裝/解除包裝成為必要的自訂提供者。</span><span class="sxs-lookup"><span data-stu-id="f0051-117">Users can choose toouse custom providers for key wrapping/unwrapping if desired.</span></span>
4. <span data-ttu-id="f0051-118">hello 加密的資料是然後上傳 toohello Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="f0051-118">hello encrypted data is then uploaded toohello Azure Storage service.</span></span> <span data-ttu-id="f0051-119">hello 包裝的金鑰，以及一些額外的加密中繼資料儲存為 （blob) 上的中繼資料，或與 hello 加密資料 （訊息排入佇列和資料表實體） 插補。</span><span class="sxs-lookup"><span data-stu-id="f0051-119">hello wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with hello encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-hello-envelope-technique"></a><span data-ttu-id="f0051-120">透過 hello 信封技術解密</span><span class="sxs-lookup"><span data-stu-id="f0051-120">Decryption via hello envelope technique</span></span>
<span data-ttu-id="f0051-121">解密透過 hello 信封技術的運作方式在 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="f0051-121">Decryption via hello envelope technique works in hello following way:</span></span>

1. <span data-ttu-id="f0051-122">hello 用戶端程式庫會假設該 hello 使用者在本機管理 hello 金鑰的加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="f0051-122">hello client library assumes that hello user is managing hello key encryption key (KEK) locally.</span></span> <span data-ttu-id="f0051-123">hello 使用者不需要 tooknow hello 特定金鑰用於加密。</span><span class="sxs-lookup"><span data-stu-id="f0051-123">hello user does not need tooknow hello specific key that was used for encryption.</span></span> <span data-ttu-id="f0051-124">相反地，索引鍵的解決器，解析不同的金鑰識別碼 tookeys，可以設定和使用。</span><span class="sxs-lookup"><span data-stu-id="f0051-124">Instead, a key resolver, which resolves different key identifiers tookeys, can be set up and used.</span></span>
2. <span data-ttu-id="f0051-125">hello 用戶端程式庫下載 hello 加密資料，以及儲存在 hello 服務任何加密內容。</span><span class="sxs-lookup"><span data-stu-id="f0051-125">hello client library downloads hello encrypted data along with any encryption material that is stored on hello service.</span></span>
3. <span data-ttu-id="f0051-126">未包裝 （解密） 使用 hello 金鑰的加密金鑰 (KEK) 則 hello 包裝的內容加密金鑰 (CEK)。</span><span class="sxs-lookup"><span data-stu-id="f0051-126">hello wrapped content encryption key (CEK) is then unwrapped (decrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="f0051-127">以下同樣地，hello 用戶端程式庫並沒有存取 tooKEK。</span><span class="sxs-lookup"><span data-stu-id="f0051-127">Here again, hello client library does not have access tooKEK.</span></span> <span data-ttu-id="f0051-128">只要叫用 hello 自訂提供者的解除包裝的演算法。</span><span class="sxs-lookup"><span data-stu-id="f0051-128">It simply invokes hello custom provider's unwrapping algorithm.</span></span>
4. <span data-ttu-id="f0051-129">hello 內容加密金鑰 (CEK) 是則會使用 toodecrypt hello 加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="f0051-129">hello content encryption key (CEK) is then used toodecrypt hello encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="f0051-130">加密機制</span><span class="sxs-lookup"><span data-stu-id="f0051-130">Encryption Mechanism</span></span>
<span data-ttu-id="f0051-131">hello 儲存體用戶端程式庫會使用[AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)順序 tooencrypt 使用者資料。</span><span class="sxs-lookup"><span data-stu-id="f0051-131">hello storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order tooencrypt user data.</span></span> <span data-ttu-id="f0051-132">具體來說，就是 [加密區塊鏈結 (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 模式搭配 AES。</span><span class="sxs-lookup"><span data-stu-id="f0051-132">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="f0051-133">每個服務的運作方式稍有不同，我們將在這裡討論每個服務。</span><span class="sxs-lookup"><span data-stu-id="f0051-133">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="f0051-134">Blob</span><span class="sxs-lookup"><span data-stu-id="f0051-134">Blobs</span></span>
<span data-ttu-id="f0051-135">hello 用戶端程式庫目前支援整個 blob 只的加密。</span><span class="sxs-lookup"><span data-stu-id="f0051-135">hello client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="f0051-136">當使用者使用 hello 時，特別是，支援加密**建立*** 方法。</span><span class="sxs-lookup"><span data-stu-id="f0051-136">Specifically, encryption is supported when users use hello **create*** methods.</span></span> <span data-ttu-id="f0051-137">針對下載項目同時支援完整與範圍下載，也提供上傳與下載的平行處理。</span><span class="sxs-lookup"><span data-stu-id="f0051-137">For downloads, both complete and range downloads are supported, and parallelization of both upload and download is available.</span></span>

<span data-ttu-id="f0051-138">在加密期間，會產生 16 個位元組，以及隨機內容加密金鑰 (CEK) 為 32 個位元組，隨機初始化向量 (IV) hello 用戶端程式庫，並將其執行 hello 使用這項資訊的 blob 資料的信封加密中。</span><span class="sxs-lookup"><span data-stu-id="f0051-138">During encryption, hello client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of hello blob data using this information.</span></span> <span data-ttu-id="f0051-139">hello 包裝 CEK 和一些額外的加密中繼資料會然後儲存 blob 中繼資料以及 hello hello 服務上加密的 blob。</span><span class="sxs-lookup"><span data-stu-id="f0051-139">hello wrapped CEK and some additional encryption metadata are then stored as blob metadata along with hello encrypted blob on hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="f0051-140">如果您要編輯或上傳您自己的 hello blob 的中繼資料，您會需要 tooensure 此中繼資料會保留。</span><span class="sxs-lookup"><span data-stu-id="f0051-140">If you are editing or uploading your own metadata for hello blob, you need tooensure that this metadata is preserved.</span></span> <span data-ttu-id="f0051-141">如果您上傳新的中繼資料，如果沒有這個中繼資料，hello 包裝的 CEK、 IV 和其他中繼資料將會遺失且 hello blob 內容永遠不會將可擷取一次。</span><span class="sxs-lookup"><span data-stu-id="f0051-141">If you upload new metadata without this metadata, hello wrapped CEK, IV and other metadata will be lost and hello blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="f0051-142">加密的 blob 下載牽涉到擷取的 hello 整個 blob 使用 hello hello 內容**取得*** 便利的方法。</span><span class="sxs-lookup"><span data-stu-id="f0051-142">Downloading an encrypted blob involves retrieving hello content of hello entire blob using hello **get*** convenience methods.</span></span> <span data-ttu-id="f0051-143">hello 包裝的 CEK 解除包裝，且與 hello IV 一起使用 （儲存為 blob 中繼資料在此情況下） tooreturn hello 解密資料 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="f0051-143">hello wrapped CEK is unwrapped and used together with hello IV (stored as blob metadata in this case) tooreturn hello decrypted data toohello users.</span></span>

<span data-ttu-id="f0051-144">下載任意範圍 (**取得*** 具有範圍參數的方法傳入) 在 hello 加密的 blob 會包括調整 hello 順序 tooget 少量可用的其他資料中的使用者所提供的範圍toosuccessfully 解密 hello 要求範圍。</span><span class="sxs-lookup"><span data-stu-id="f0051-144">Downloading an arbitrary range (**get*** methods with range parameters passed in) in hello encrypted blob involves adjusting hello range provided by users in order tooget a small amount of additional data that can be used toosuccessfully decrypt hello requested range.</span></span>

<span data-ttu-id="f0051-145">區塊 Blob 和分頁 Blob 只可以使用這種配置加密/解密。</span><span class="sxs-lookup"><span data-stu-id="f0051-145">Block blobs and page blobs only can be encrypted/decrypted using this scheme.</span></span> <span data-ttu-id="f0051-146">目前不支援加密附加 Blob。</span><span class="sxs-lookup"><span data-stu-id="f0051-146">There is currently no support for encrypting append blobs.</span></span>

### <a name="queues"></a><span data-ttu-id="f0051-147">佇列</span><span class="sxs-lookup"><span data-stu-id="f0051-147">Queues</span></span>
<span data-ttu-id="f0051-148">因為佇列訊息可以是任何格式，hello 用戶端程式庫會定義包含 hello 訊息文字中的 hello 初始化向量 (IV) 與 hello 加密的內容加密金鑰 (CEK) 的自訂格式。</span><span class="sxs-lookup"><span data-stu-id="f0051-148">Since queue messages can be of any format, hello client library defines a custom format that includes hello Initialization Vector (IV) and hello encrypted content encryption key (CEK) in hello message text.</span></span>

<span data-ttu-id="f0051-149">在加密期間，hello 用戶端程式庫會產生 16 個位元組，以及隨機 CEK 32 個位元組的隨機 IV，並執行信封加密 hello 佇列的訊息文字使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="f0051-149">During encryption, hello client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of hello queue message text using this information.</span></span> <span data-ttu-id="f0051-150">hello 包裝 CEK 和一些額外的加密中繼資料接著會加入 toohello 加密的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="f0051-150">hello wrapped CEK and some additional encryption metadata are then added toohello encrypted queue message.</span></span> <span data-ttu-id="f0051-151">這個修改過的訊息 （如下所示） 會儲存在 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="f0051-151">This modified message (shown below) is stored on hello service.</span></span>

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

<span data-ttu-id="f0051-152">在解密，hello 包裝的金鑰是擷取自 hello 佇列訊息，而且解除包裝。</span><span class="sxs-lookup"><span data-stu-id="f0051-152">During decryption, hello wrapped key is extracted from hello queue message and unwrapped.</span></span> <span data-ttu-id="f0051-153">hello IV 也是擷取自 hello 佇列訊息，並搭配 hello 解除包裝金鑰 toodecrypt hello 佇列訊息資料。</span><span class="sxs-lookup"><span data-stu-id="f0051-153">hello IV is also extracted from hello queue message and used along with hello unwrapped key toodecrypt hello queue message data.</span></span> <span data-ttu-id="f0051-154">請注意 hello 的加密中繼資料是小型 （下 500 個位元組），因此它沒有會計 hello 64 KB 限制的佇列訊息，而 hello 影響應該很容易管理。</span><span class="sxs-lookup"><span data-stu-id="f0051-154">Note that hello encryption metadata is small (under 500 bytes), so while it does count toward hello 64KB limit for a queue message, hello impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="f0051-155">資料表</span><span class="sxs-lookup"><span data-stu-id="f0051-155">Tables</span></span>
<span data-ttu-id="f0051-156">hello 插入的實體屬性的用戶端程式庫支援加密和取代作業。</span><span class="sxs-lookup"><span data-stu-id="f0051-156">hello client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="f0051-157">目前不支援合併。</span><span class="sxs-lookup"><span data-stu-id="f0051-157">Merge is not currently supported.</span></span> <span data-ttu-id="f0051-158">屬性的子集可能已加密先前使用不同的金鑰，因為只要合併 hello 新內容，並更新 hello 中繼資料會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="f0051-158">Since a subset of properties may have been encrypted previously using a different key, simply merging hello new properties and updating hello metadata will result in data loss.</span></span> <span data-ttu-id="f0051-159">合併 需要進行額外的服務從 hello 服務呼叫 tooread hello 預先存在的實體，或使用每個屬性的新機碼，這兩者都不適用基於效能的考量。</span><span class="sxs-lookup"><span data-stu-id="f0051-159">Merging either requires making extra service calls tooread hello pre-existing entity from hello service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="f0051-160">資料表資料加密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="f0051-160">Table data encryption works as follows:</span></span>

1. <span data-ttu-id="f0051-161">使用者指定 hello 屬性 toobe 加密。</span><span class="sxs-lookup"><span data-stu-id="f0051-161">Users specify hello properties toobe encrypted.</span></span>
2. <span data-ttu-id="f0051-162">hello 用戶端程式庫會產生 16 個位元組的隨機內容加密金鑰 (CEK) 32 個位元組，針對每個實體，以及隨機初始化向量 (IV)，並執行 hello 藉由衍生新的 IV，每個加密的個別屬性 toobe 信封加密屬性。</span><span class="sxs-lookup"><span data-stu-id="f0051-162">hello client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on hello individual properties toobe encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="f0051-163">加密的 hello 屬性會儲存為二進位資料。</span><span class="sxs-lookup"><span data-stu-id="f0051-163">hello encrypted property is stored as binary data.</span></span>
3. <span data-ttu-id="f0051-164">hello 包裝 CEK 和一些額外的加密中繼資料會儲存為兩個額外的保留屬性。</span><span class="sxs-lookup"><span data-stu-id="f0051-164">hello wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="f0051-165">hello 先保留屬性 (\_ClientEncryptionMetadata1) 是保存 hello IV、 版本和包裝的金鑰資訊的字串屬性。</span><span class="sxs-lookup"><span data-stu-id="f0051-165">hello first reserved property (\_ClientEncryptionMetadata1) is a string property that holds hello information about IV, version, and wrapped key.</span></span> <span data-ttu-id="f0051-166">hello 第二個保留的屬性 (\_ClientEncryptionMetadata2) 是保留加密的 hello 屬性的 hello 資訊的二進位屬性。</span><span class="sxs-lookup"><span data-stu-id="f0051-166">hello second reserved property (\_ClientEncryptionMetadata2) is a binary property that holds hello information about hello properties that are encrypted.</span></span> <span data-ttu-id="f0051-167">hello 這個第二個屬性中的資訊 (\_ClientEncryptionMetadata2) 本身經過加密。</span><span class="sxs-lookup"><span data-stu-id="f0051-167">hello information in this second property (\_ClientEncryptionMetadata2) is itself encrypted.</span></span>
4. <span data-ttu-id="f0051-168">Toothese 其他保留所需的內容加密，因為使用者可能現在有只 250 的自訂屬性，而不是 252。</span><span class="sxs-lookup"><span data-stu-id="f0051-168">Due toothese additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="f0051-169">hello hello 實體的大小總計必須小於 1MB。</span><span class="sxs-lookup"><span data-stu-id="f0051-169">hello total size of hello entity must be less than 1MB.</span></span>
   
   <span data-ttu-id="f0051-170">請注意，只有字串屬性可以加密。</span><span class="sxs-lookup"><span data-stu-id="f0051-170">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="f0051-171">如果其他屬性類型 toobe 加密，它們必須轉換的 toostrings。</span><span class="sxs-lookup"><span data-stu-id="f0051-171">If other types of properties are toobe encrypted, they must be converted toostrings.</span></span> <span data-ttu-id="f0051-172">hello 加密字串 hello 服務上儲存為二進位屬性，而它們會轉換後 toostrings （原始字串，不具有類型 EdmType.STRING EntityProperties） 解密之後。</span><span class="sxs-lookup"><span data-stu-id="f0051-172">hello encrypted strings are stored on hello service as binary properties, and they are converted back toostrings (raw strings, not EntityProperties with type EdmType.STRING) after decryption.</span></span>
   
   <span data-ttu-id="f0051-173">對於資料表，此外 toohello 加密原則，使用者必須指定 hello 屬性 toobe 加密。</span><span class="sxs-lookup"><span data-stu-id="f0051-173">For tables, in addition toohello encryption policy, users must specify hello properties toobe encrypted.</span></span> <span data-ttu-id="f0051-174">這可藉由在 hello 類型組 tooEdmType.STRING TableEntity 物件中任一儲存這些屬性，並將加密 hello tableservice 物件上的設定 tootrue 或設定 hello encryption_resolver_function。</span><span class="sxs-lookup"><span data-stu-id="f0051-174">This can be done by either storing these properties in TableEntity objects with hello type set tooEdmType.STRING and encrypt set tootrue or setting hello encryption_resolver_function on hello tableservice object.</span></span> <span data-ttu-id="f0051-175">加密解析程式是函式，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。</span><span class="sxs-lookup"><span data-stu-id="f0051-175">An encryption resolver is a function that takes a partition key, row key, and property name and returns a boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="f0051-176">在加密期間，是否應該加密屬性，同時寫入 toohello 網路 hello 用戶端程式庫時，會使用此資訊 toodecide。</span><span class="sxs-lookup"><span data-stu-id="f0051-176">During encryption, hello client library will use this information toodecide whether a property should be encrypted while writing toohello wire.</span></span> <span data-ttu-id="f0051-177">hello 委派也提供 hello 可能性的邏輯屬性加密的方式。</span><span class="sxs-lookup"><span data-stu-id="f0051-177">hello delegate also provides for hello possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="f0051-178">(例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，就是不必要的 tooprovide 讀取或查詢實體時此資訊。</span><span class="sxs-lookup"><span data-stu-id="f0051-178">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary tooprovide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="f0051-179">批次作業</span><span class="sxs-lookup"><span data-stu-id="f0051-179">Batch Operations</span></span>
<span data-ttu-id="f0051-180">加密原則適用於 tooall hello 批次中的資料列。</span><span class="sxs-lookup"><span data-stu-id="f0051-180">One encryption policy applies tooall rows in hello batch.</span></span> <span data-ttu-id="f0051-181">hello 用戶端程式庫在內部將會產生新的隨機 IV 和每個資料列的隨機 CEK hello 批次中。</span><span class="sxs-lookup"><span data-stu-id="f0051-181">hello client library will internally generate a new random IV and random CEK per row in hello batch.</span></span> <span data-ttu-id="f0051-182">使用者也可以選擇 tooencrypt 不同的屬性，針對每個作業 hello 批次中在 hello 加密解析程式中定義此行為。</span><span class="sxs-lookup"><span data-stu-id="f0051-182">Users can also choose tooencrypt different properties for every operation in hello batch by defining this behavior in hello encryption resolver.</span></span>
<span data-ttu-id="f0051-183">如果批次透過 hello tableservice batch() 方法建立為內容管理員，hello tableservice 加密原則會自動套用的 toohello 批次。</span><span class="sxs-lookup"><span data-stu-id="f0051-183">If a batch is created as a context manager through hello tableservice batch() method, hello tableservice's encryption policy will automatically be applied toohello batch.</span></span> <span data-ttu-id="f0051-184">藉由呼叫 hello 建構函式明確地建立批次時，如果 hello 加密原則必須傳遞為參數和 hello 存留期的 hello 批次未修改的左。</span><span class="sxs-lookup"><span data-stu-id="f0051-184">If a batch is created explicitly by calling hello constructor, hello encryption policy must be passed as a parameter and left unmodified for hello lifetime of hello batch.</span></span>
<span data-ttu-id="f0051-185">請注意到使用 hello 批次 （在認可使用 hello tableservice 加密原則的 hello 批次的 hello 階段不會加密實體） 的加密原則的 hello 批次插入時，會加密實體。</span><span class="sxs-lookup"><span data-stu-id="f0051-185">Note that entities are encrypted as they are inserted into hello batch using hello batch's encryption policy (entities are NOT encrypted at hello time of committing hello batch using hello tableservice's encryption policy).</span></span>

### <a name="queries"></a><span data-ttu-id="f0051-186">查詢</span><span class="sxs-lookup"><span data-stu-id="f0051-186">Queries</span></span>
<span data-ttu-id="f0051-187">tooperform 查詢作業，您必須指定索引鍵的解析程式所能 tooresolve 所有 hello hello 結果集中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f0051-187">tooperform query operations, you must specify a key resolver that is able tooresolve all hello keys in hello result set.</span></span> <span data-ttu-id="f0051-188">如果 hello 查詢結果中包含的實體不能是解析的 tooa 提供者，hello 用戶端程式庫會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="f0051-188">If an entity contained in hello query result cannot be resolved tooa provider, hello client library will throw an error.</span></span> <span data-ttu-id="f0051-189">對於執行伺服器端投影的任何查詢，hello 用戶端程式庫會將加入 hello 特殊加密中繼資料屬性 (\_ClientEncryptionMetadata1 和\_ClientEncryptionMetadata2) 預設 toohello 所選取的資料行.</span><span class="sxs-lookup"><span data-stu-id="f0051-189">For any query that performs server side projections, hello client library will add hello special encryption metadata properties (\_ClientEncryptionMetadata1 and \_ClientEncryptionMetadata2) by default toohello selected columns.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0051-190">使用用戶端加密時，請留意以下重點：</span><span class="sxs-lookup"><span data-stu-id="f0051-190">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="f0051-191">當從進行讀取或寫入 tooan 加密 blob、 使用完整的 blob 上傳的命令和範圍/整個 blob 下載命令。</span><span class="sxs-lookup"><span data-stu-id="f0051-191">When reading from or writing tooan encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="f0051-192">避免撰寫 tooan 加密的 blob，使用通訊協定的作業，例如將區塊、 放置區塊清單、 撰寫網頁或清除的頁面。否則，您可能會破壞 hello 加密的 blob，並使它無法讀取。</span><span class="sxs-lookup"><span data-stu-id="f0051-192">Avoid writing tooan encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, or Clear Pages; otherwise you may corrupt hello encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="f0051-193">對於資料表，存在類似的條件約束。</span><span class="sxs-lookup"><span data-stu-id="f0051-193">For tables, a similar constraint exists.</span></span> <span data-ttu-id="f0051-194">能謹慎 toonot 更新加密內容，而無須更新 hello 加密中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f0051-194">Be careful toonot update encrypted properties without updating hello encryption metadata.</span></span>
> * <span data-ttu-id="f0051-195">如果您在 hello 加密的 blob 上設定中繼資料，您可能會覆寫 hello 加密相關中繼資料所需來解密，因為設定中繼資料不是加總。</span><span class="sxs-lookup"><span data-stu-id="f0051-195">If you set metadata on hello encrypted blob, you may overwrite hello encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="f0051-196">快照集也是如此。在為加密的 Blob 建立快照集時，請避免指定中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f0051-196">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="f0051-197">如果必須設定中繼資料，是確定 toocall hello **get_blob_metadata**方法的第一個 tooget hello 目前的加密中繼資料和中繼資料在設定時，避免並行寫入。</span><span class="sxs-lookup"><span data-stu-id="f0051-197">If metadata must be set, be sure toocall hello **get_blob_metadata** method first tooget hello current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>
> * <span data-ttu-id="f0051-198">啟用 hello **require_encryption** hello 服務只應搭配加密資料的使用者物件上的旗標。</span><span class="sxs-lookup"><span data-stu-id="f0051-198">Enable hello **require_encryption** flag on hello service object for users that should work only with encrypted data.</span></span> <span data-ttu-id="f0051-199">如需詳細資訊請參閱下方內容。</span><span class="sxs-lookup"><span data-stu-id="f0051-199">See below for more info.</span></span>
> 
> 

<span data-ttu-id="f0051-200">hello 儲存體用戶端程式庫預期 hello 提供 KEK 和索引鍵的解析程式 tooimplement hello 下列介面。</span><span class="sxs-lookup"><span data-stu-id="f0051-200">hello storage client library expects hello provided KEK and key resolver tooimplement hello following interface.</span></span> <span data-ttu-id="f0051-201">[Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/) 支援尚未推出，並會在完成時整合到此程式庫。</span><span class="sxs-lookup"><span data-stu-id="f0051-201">[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) support for Python KEK management is pending and will be integrated into this library when completed.</span></span>

## <a name="client-api--interface"></a><span data-ttu-id="f0051-202">用戶端 API / 介面</span><span class="sxs-lookup"><span data-stu-id="f0051-202">Client API / Interface</span></span>
<span data-ttu-id="f0051-203">Hello 使用者已建立儲存體服務物件 (也就是 blockblobservice) 之後，可能會指派值 toohello 欄位構成加密原則： key_encryption_key，key_resolver_function，和 require_encryption。</span><span class="sxs-lookup"><span data-stu-id="f0051-203">After a storage service object (i.e. blockblobservice) has been created, hello user may assign values toohello fields that constitute an encryption policy: key_encryption_key, key_resolver_function, and require_encryption.</span></span> <span data-ttu-id="f0051-204">使用者可以僅提供 KEK、僅提供解析程式，或是兩者皆提供。</span><span class="sxs-lookup"><span data-stu-id="f0051-204">Users can provide only a KEK, only a resolver, or both.</span></span> <span data-ttu-id="f0051-205">key_encryption_key 是 hello 基本金鑰，用來識別索引鍵的識別項和類型，提供用來包裝/解除包裝的 hello 邏輯。</span><span class="sxs-lookup"><span data-stu-id="f0051-205">key_encryption_key is hello basic key type that is identified using a key identifier and that provides hello logic for wrapping/unwrapping.</span></span> <span data-ttu-id="f0051-206">key_resolver_function hello 解密程序期間會使用的 tooresolve 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f0051-206">key_resolver_function is used tooresolve a key during hello decryption process.</span></span> <span data-ttu-id="f0051-207">它會傳回指定金鑰識別碼的有效 KEK。</span><span class="sxs-lookup"><span data-stu-id="f0051-207">It returns a valid KEK given a key identifier.</span></span> <span data-ttu-id="f0051-208">這會提供使用者 hello 能力 toochoose 之間的多個位置中受管理的多個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f0051-208">This provides users hello ability toochoose between multiple keys that are managed in multiple locations.</span></span>

<span data-ttu-id="f0051-209">hello KEK 必須實作下列 hello 方法 toosuccessfully 加密資料：</span><span class="sxs-lookup"><span data-stu-id="f0051-209">hello KEK must implement hello following methods toosuccessfully encrypt data:</span></span>

* <span data-ttu-id="f0051-210">wrap_key(cek)： 包裝 hello 指定 CEK （位元組） 使用 hello 使用者選擇的演算法。</span><span class="sxs-lookup"><span data-stu-id="f0051-210">wrap_key(cek): Wraps hello specified CEK (bytes) using an algorithm of hello user's choice.</span></span> <span data-ttu-id="f0051-211">傳回 hello 的已包裝金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0051-211">Returns hello wrapped key.</span></span>
* <span data-ttu-id="f0051-212">get_key_wrap_algorithm()： 傳回 hello 演算法會使用 toowrap 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f0051-212">get_key_wrap_algorithm(): Returns hello algorithm used toowrap keys.</span></span>
* <span data-ttu-id="f0051-213">get_kid()： 針對這個 KEK 的傳回 hello 字串索引鍵識別碼。</span><span class="sxs-lookup"><span data-stu-id="f0051-213">get_kid(): Returns hello string key id for this KEK.</span></span>
  <span data-ttu-id="f0051-214">hello KEK 必須實作下列方法 toosuccessfully 解密資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="f0051-214">hello KEK must implement hello following methods toosuccessfully decrypt data:</span></span>
* <span data-ttu-id="f0051-215">unwrap_key （cek，演算法）： hello 傳回解除包裝的 hello 形式指定 CEK 使用 hello 字串指定的演算法。</span><span class="sxs-lookup"><span data-stu-id="f0051-215">unwrap_key(cek, algorithm): Returns hello unwrapped form of hello specified CEK using hello string-specified algorithm.</span></span>
* <span data-ttu-id="f0051-216">get_kid()：傳回此 KEK 的字串金鑰識別碼。</span><span class="sxs-lookup"><span data-stu-id="f0051-216">get_kid(): Returns a string key id for this KEK.</span></span>

<span data-ttu-id="f0051-217">hello 索引鍵的解析程式必須至少實作可在指定索引鍵的識別碼，傳回 hello 對應 KEK 實作 hello 介面上述的方法。</span><span class="sxs-lookup"><span data-stu-id="f0051-217">hello key resolver must at least implement a method that, given a key id, returns hello corresponding KEK implementing hello interface above.</span></span> <span data-ttu-id="f0051-218">只有這個方法是 toobe 指派 toohello key_resolver_function 屬性在 hello 服務物件。</span><span class="sxs-lookup"><span data-stu-id="f0051-218">Only this method is toobe assigned toohello key_resolver_function property on hello service object.</span></span>

* <span data-ttu-id="f0051-219">用於加密，hello 索引鍵永遠且沒有金鑰 hello 情況下會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="f0051-219">For encryption, hello key is used always and hello absence of a key will result in an error.</span></span>
* <span data-ttu-id="f0051-220">解密：</span><span class="sxs-lookup"><span data-stu-id="f0051-220">For decryption:</span></span>
  
  * <span data-ttu-id="f0051-221">如果指定 tooget hello 索引鍵，則會叫用 hello 索引鍵的解析程式。</span><span class="sxs-lookup"><span data-stu-id="f0051-221">hello key resolver is invoked if specified tooget hello key.</span></span> <span data-ttu-id="f0051-222">如果指定 hello 解析程式，但是沒有 hello 之金鑰識別碼的對應，會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="f0051-222">If hello resolver is specified but does not have a mapping for hello key identifier, an error is thrown.</span></span>
  * <span data-ttu-id="f0051-223">如果未指定解析程式，但指定的索引鍵，hello 金鑰可用如果其識別項所需的 hello 與金鑰識別碼相符。</span><span class="sxs-lookup"><span data-stu-id="f0051-223">If resolver is not specified but a key is specified, hello key is used if its identifier matches hello required key identifier.</span></span> <span data-ttu-id="f0051-224">如果 hello 識別碼不符合，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="f0051-224">If hello identifier does not match, an error is thrown.</span></span>
    
    <span data-ttu-id="f0051-225">hello azure.storage.samples 加密範例<fix URL>示範更詳細的端對端案例，適用於 blob、 佇列和資料表。</span><span class="sxs-lookup"><span data-stu-id="f0051-225">hello encryption samples in azure.storage.samples <fix URL>demonstrate a more detailed end-to-end scenario for blobs, queues and tables.</span></span>
      <span data-ttu-id="f0051-226">Hello KEK 和索引鍵的解析程式的範例實作，提供 hello 範例檔案中 KeyWrapper 和 KeyResolver 分別。</span><span class="sxs-lookup"><span data-stu-id="f0051-226">Sample implementations of hello KEK and key resolver are provided in hello sample files as KeyWrapper and KeyResolver respectively.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="f0051-227">RequireEncryption 模式</span><span class="sxs-lookup"><span data-stu-id="f0051-227">RequireEncryption mode</span></span>
<span data-ttu-id="f0051-228">使用者可以針對所有上傳和下載都必須加密的作業模式，從中選擇啟用。</span><span class="sxs-lookup"><span data-stu-id="f0051-228">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="f0051-229">在此模式中，嘗試 tooupload 資料，而不會加密 hello 服務的加密原則或下載資料不會失敗 hello 用戶端上。</span><span class="sxs-lookup"><span data-stu-id="f0051-229">In this mode, attempts tooupload data without an encryption policy or download data that is not encrypted on hello service will fail on hello client.</span></span> <span data-ttu-id="f0051-230">hello **require_encryption**旗標上 hello 服務物件控制這個行為。</span><span class="sxs-lookup"><span data-stu-id="f0051-230">hello **require_encryption** flag on hello service object controls this behavior.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="f0051-231">Blob 服務加密</span><span class="sxs-lookup"><span data-stu-id="f0051-231">Blob service encryption</span></span>
<span data-ttu-id="f0051-232">Hello blockblobservice 物件上設定 hello 加密原則欄位。</span><span class="sxs-lookup"><span data-stu-id="f0051-232">Set hello encryption policy fields on hello blockblobservice object.</span></span> <span data-ttu-id="f0051-233">所有其他項目將 hello 用戶端程式庫在內部進行處理。</span><span class="sxs-lookup"><span data-stu-id="f0051-233">Everything else will be handled by hello client library internally.</span></span>

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a><span data-ttu-id="f0051-234">佇列服務加密</span><span class="sxs-lookup"><span data-stu-id="f0051-234">Queue service encryption</span></span>
<span data-ttu-id="f0051-235">Hello queueservice 物件上設定 hello 加密原則欄位。</span><span class="sxs-lookup"><span data-stu-id="f0051-235">Set hello encryption policy fields on hello queueservice object.</span></span> <span data-ttu-id="f0051-236">所有其他項目將 hello 用戶端程式庫在內部進行處理。</span><span class="sxs-lookup"><span data-stu-id="f0051-236">Everything else will be handled by hello client library internally.</span></span>

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a><span data-ttu-id="f0051-237">資料表服務加密</span><span class="sxs-lookup"><span data-stu-id="f0051-237">Table service encryption</span></span>
<span data-ttu-id="f0051-238">此外 toocreating 加密原則和設定要求的選項，您必須指定**encryption_resolver_function**上 hello **tableservice**，或使用加密屬性上設定 hellohello EntityProperty。</span><span class="sxs-lookup"><span data-stu-id="f0051-238">In addition toocreating an encryption policy and setting it on request options, you must either specify an **encryption_resolver_function** on hello **tableservice**, or set hello encrypt attribute on hello EntityProperty.</span></span>

### <a name="using-hello-resolver"></a><span data-ttu-id="f0051-239">使用 hello 解析程式</span><span class="sxs-lookup"><span data-stu-id="f0051-239">Using hello resolver</span></span>

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a><span data-ttu-id="f0051-240">使用屬性</span><span class="sxs-lookup"><span data-stu-id="f0051-240">Using attributes</span></span>
<span data-ttu-id="f0051-241">如上面所述，屬性可能會標示為加密儲存在 EntityProperty 物件中，並設定 hello 加密欄位。</span><span class="sxs-lookup"><span data-stu-id="f0051-241">As mentioned above, a property may be marked for encryption by storing it in an EntityProperty object and setting hello encrypt field.</span></span>

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a><span data-ttu-id="f0051-242">加密和效能</span><span class="sxs-lookup"><span data-stu-id="f0051-242">Encryption and performance</span></span>
<span data-ttu-id="f0051-243">請注意，加密您的儲存體資料會造成額外的效能負擔。</span><span class="sxs-lookup"><span data-stu-id="f0051-243">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="f0051-244">hello 必須產生金鑰和 IV，hello 內容本身必須經過加密、 和其他中繼資料必須格式化，並且上傳內容。</span><span class="sxs-lookup"><span data-stu-id="f0051-244">hello content key and IV must be generated, hello content itself must be encrypted, and additional metadata must be formatted and uploaded.</span></span> <span data-ttu-id="f0051-245">這項負擔會根據 hello 所加密的資料數量而有所不同。</span><span class="sxs-lookup"><span data-stu-id="f0051-245">This overhead will vary depending on hello quantity of data being encrypted.</span></span> <span data-ttu-id="f0051-246">我們建議客戶一定要在開發期間測試其應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="f0051-246">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0051-247">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0051-247">Next steps</span></span>
* <span data-ttu-id="f0051-248">下載 hello [Java PyPi 套件的 Azure 儲存體用戶端程式庫](https://pypi.python.org/pypi/azure-storage)</span><span class="sxs-lookup"><span data-stu-id="f0051-248">Download hello [Azure Storage Client Library for Java PyPi package](https://pypi.python.org/pypi/azure-storage)</span></span>
* <span data-ttu-id="f0051-249">下載 hello [Python 從原始程式碼 GitHub 的 Azure 儲存體用戶端程式庫](https://github.com/Azure/azure-storage-python)</span><span class="sxs-lookup"><span data-stu-id="f0051-249">Download hello [Azure Storage Client Library for Python Source Code from GitHub](https://github.com/Azure/azure-storage-python)</span></span>
