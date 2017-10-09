---
title: "使用.NET 的 Microsoft Azure 儲存體的 aaaClient 端加密 |Microsoft 文件"
description: "hello 適用於.NET 的 Azure 儲存體用戶端程式庫支援最高的安全性應用程式的 Azure 儲存體用戶端加密以及與 Azure 金鑰保存庫的整合。"
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
ms.openlocfilehash: e99551925069d5e05bc283039b252cffe8df5383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a><span data-ttu-id="bcf81-103">Microsoft Azure 儲存體的用戶端加密和 Azure Key Vault 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="bcf81-103">Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage</span></span>
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a><span data-ttu-id="bcf81-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bcf81-104">Overview</span></span>
<span data-ttu-id="bcf81-105">hello [.NET Nuget 套件的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)支援 tooAzure 存放裝置，將上傳和下載 toohello 用戶端時解密資料之前加密用戶端應用程式內的資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-105">hello [Azure Storage Client Library for .NET Nuget package](https://www.nuget.org/packages/WindowsAzure.Storage) supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="bcf81-106">hello 程式庫也支援與整合[Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)儲存體帳戶金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="bcf81-106">hello library also supports integration with [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) for storage account key management.</span></span>

<span data-ttu-id="bcf81-107">將引導您完成加密 blob 使用用戶端加密與 Azure 金鑰保存庫的 hello 程序的逐步教學課程，請參閱[中使用 Azure 金鑰保存庫的 Microsoft Azure 儲存體加密及解密 blob](storage-encrypt-decrypt-blobs-key-vault.md)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-107">For a step-by-step tutorial that leads you through hello process of encrypting blobs using client-side encryption and Azure Key Vault, see [Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>

<span data-ttu-id="bcf81-108">如需使用 Java 加密用戶端，請參閱 [Microsoft Azure 儲存體的用戶端 Java 加密](storage-client-side-encryption-java.md)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-108">For client-side encryption with Java, see [Client-Side Encryption with Java for Microsoft Azure Storage](storage-client-side-encryption-java.md).</span></span>

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a><span data-ttu-id="bcf81-109">加密和解密透過 hello 信封技術</span><span class="sxs-lookup"><span data-stu-id="bcf81-109">Encryption and decryption via hello envelope technique</span></span>
<span data-ttu-id="bcf81-110">加密和解密的 hello 處理程序遵循 hello 信封技術。</span><span class="sxs-lookup"><span data-stu-id="bcf81-110">hello processes of encryption and decryption follow hello envelope technique.</span></span>

### <a name="encryption-via-hello-envelope-technique"></a><span data-ttu-id="bcf81-111">加密透過 hello 信封技術</span><span class="sxs-lookup"><span data-stu-id="bcf81-111">Encryption via hello envelope technique</span></span>
<span data-ttu-id="bcf81-112">透過 hello 信封技術的加密方式 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="bcf81-112">Encryption via hello envelope technique works in hello following way:</span></span>

1. <span data-ttu-id="bcf81-113">hello Azure 儲存體用戶端程式庫產生的內容加密金鑰 (CEK)，這是一次性單次使用對稱金鑰。</span><span class="sxs-lookup"><span data-stu-id="bcf81-113">hello Azure storage client library generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="bcf81-114">使用此 CEK 加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-114">User data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="bcf81-115">hello CEK 然後再包裝 （加密） 使用 hello 金鑰的加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-115">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="bcf81-116">hello KEK 索引鍵的識別項所識別，可非對稱金鑰組或對稱金鑰，可以是本機管理或儲存在 Azure 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="bcf81-116">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vaults.</span></span>
   
    <span data-ttu-id="bcf81-117">hello 儲存體用戶端程式庫本身完全不需要存取 tooKEK。</span><span class="sxs-lookup"><span data-stu-id="bcf81-117">hello storage client library itself never has access tooKEK.</span></span> <span data-ttu-id="bcf81-118">hello 程式庫會叫用所提供的金鑰保存庫 hello 金鑰包裝演算法。</span><span class="sxs-lookup"><span data-stu-id="bcf81-118">hello library invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="bcf81-119">使用者可以選擇 toouse 為金鑰包裝/解除包裝成為必要的自訂提供者。</span><span class="sxs-lookup"><span data-stu-id="bcf81-119">Users can choose toouse custom providers for key wrapping/unwrapping if desired.</span></span>

4. <span data-ttu-id="bcf81-120">hello 加密的資料是然後上傳 toohello Azure 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="bcf81-120">hello encrypted data is then uploaded toohello Azure Storage service.</span></span> <span data-ttu-id="bcf81-121">hello 包裝的金鑰，以及一些額外的加密中繼資料儲存為 （blob) 上的中繼資料，或與 hello 加密資料 （訊息排入佇列和資料表實體） 插補。</span><span class="sxs-lookup"><span data-stu-id="bcf81-121">hello wrapped key along with some additional encryption metadata is either stored as metadata (on a blob) or interpolated with hello encrypted data (queue messages and table entities).</span></span>

### <a name="decryption-via-hello-envelope-technique"></a><span data-ttu-id="bcf81-122">透過 hello 信封技術解密</span><span class="sxs-lookup"><span data-stu-id="bcf81-122">Decryption via hello envelope technique</span></span>
<span data-ttu-id="bcf81-123">解密透過 hello 信封技術的運作方式在 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="bcf81-123">Decryption via hello envelope technique works in hello following way:</span></span>

1. <span data-ttu-id="bcf81-124">hello 用戶端程式庫會假設該 hello 使用者在本機或 Azure 金鑰保存庫中管理 hello 金鑰的加密金鑰 (KEK)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-124">hello client library assumes that hello user is managing hello key encryption key (KEK) either locally or in Azure Key Vaults.</span></span> <span data-ttu-id="bcf81-125">hello 使用者不需要 tooknow hello 特定金鑰用於加密。</span><span class="sxs-lookup"><span data-stu-id="bcf81-125">hello user does not need tooknow hello specific key that was used for encryption.</span></span> <span data-ttu-id="bcf81-126">相反地，可以設定並使用索引鍵的解析程式會解析 tookeys 不同索引鍵的識別項。</span><span class="sxs-lookup"><span data-stu-id="bcf81-126">Instead, a key resolver which resolves different key identifiers tookeys can be set up and used.</span></span>
2. <span data-ttu-id="bcf81-127">hello 用戶端程式庫下載 hello 加密資料，以及儲存在 hello 服務任何加密內容。</span><span class="sxs-lookup"><span data-stu-id="bcf81-127">hello client library downloads hello encrypted data along with any encryption material that is stored on hello service.</span></span>
3. <span data-ttu-id="bcf81-128">未包裝 （解密） 使用 hello 金鑰的加密金鑰 (KEK) 則 hello 包裝的內容加密金鑰 (CEK)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-128">hello wrapped content encryption key (CEK) is then unwrapped (decrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="bcf81-129">以下同樣地，hello 用戶端程式庫並沒有存取 tooKEK。</span><span class="sxs-lookup"><span data-stu-id="bcf81-129">Here again, hello client library does not have access tooKEK.</span></span> <span data-ttu-id="bcf81-130">它只會叫用自訂的 hello 或金鑰保存庫提供者的解除包裝的演算法。</span><span class="sxs-lookup"><span data-stu-id="bcf81-130">It simply invokes hello custom or Key Vault provider's unwrapping algorithm.</span></span>
4. <span data-ttu-id="bcf81-131">hello 內容加密金鑰 (CEK) 是則會使用 toodecrypt hello 加密使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-131">hello content encryption key (CEK) is then used toodecrypt hello encrypted user data.</span></span>

## <a name="encryption-mechanism"></a><span data-ttu-id="bcf81-132">加密機制</span><span class="sxs-lookup"><span data-stu-id="bcf81-132">Encryption Mechanism</span></span>
<span data-ttu-id="bcf81-133">hello 儲存體用戶端程式庫會使用[AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard)順序 tooencrypt 使用者資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-133">hello storage client library uses [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) in order tooencrypt user data.</span></span> <span data-ttu-id="bcf81-134">具體來說，就是 [加密區塊鏈結 (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) 模式搭配 AES。</span><span class="sxs-lookup"><span data-stu-id="bcf81-134">Specifically, [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) mode with AES.</span></span> <span data-ttu-id="bcf81-135">每個服務的運作方式稍有不同，我們將在這裡討論每個服務。</span><span class="sxs-lookup"><span data-stu-id="bcf81-135">Each service works somewhat differently, so we will discuss each of them here.</span></span>

### <a name="blobs"></a><span data-ttu-id="bcf81-136">Blob</span><span class="sxs-lookup"><span data-stu-id="bcf81-136">Blobs</span></span>
<span data-ttu-id="bcf81-137">hello 用戶端程式庫目前支援整個 blob 只的加密。</span><span class="sxs-lookup"><span data-stu-id="bcf81-137">hello client library currently supports encryption of whole blobs only.</span></span> <span data-ttu-id="bcf81-138">當使用者使用 hello 時，特別是，支援加密**UploadFrom*** 方法或 hello **OpenWrite**方法。</span><span class="sxs-lookup"><span data-stu-id="bcf81-138">Specifically, encryption is supported when users use hello **UploadFrom*** methods or hello **OpenWrite** method.</span></span> <span data-ttu-id="bcf81-139">針對下載，則皆支援完整與範圍下載。</span><span class="sxs-lookup"><span data-stu-id="bcf81-139">For downloads, both complete and range downloads are supported.</span></span>

<span data-ttu-id="bcf81-140">在加密期間，會產生 16 個位元組，以及隨機內容加密金鑰 (CEK) 為 32 個位元組，隨機初始化向量 (IV) hello 用戶端程式庫，並將其執行 hello 使用這項資訊的 blob 資料的信封加密中。</span><span class="sxs-lookup"><span data-stu-id="bcf81-140">During encryption, hello client library will generate a random Initialization Vector (IV) of 16 bytes, together with a random content encryption key (CEK) of 32 bytes, and perform envelope encryption of hello blob data using this information.</span></span> <span data-ttu-id="bcf81-141">hello 包裝 CEK 和一些額外的加密中繼資料會然後儲存 blob 中繼資料以及 hello hello 服務上加密的 blob。</span><span class="sxs-lookup"><span data-stu-id="bcf81-141">hello wrapped CEK and some additional encryption metadata are then stored as blob metadata along with hello encrypted blob on hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="bcf81-142">如果您要編輯或上傳您自己的 hello blob 的中繼資料，您會需要 tooensure 此中繼資料會保留。</span><span class="sxs-lookup"><span data-stu-id="bcf81-142">If you are editing or uploading your own metadata for hello blob, you need tooensure that this metadata is preserved.</span></span> <span data-ttu-id="bcf81-143">如果您上傳新的中繼資料，如果沒有這個中繼資料，hello 包裝的 CEK、 IV 和其他中繼資料將會遺失且 hello blob 內容永遠不會將可擷取一次。</span><span class="sxs-lookup"><span data-stu-id="bcf81-143">If you upload new metadata without this metadata, hello wrapped CEK, IV, and other metadata will be lost and hello blob content will never be retrievable again.</span></span>
> 
> 

<span data-ttu-id="bcf81-144">加密的 blob 下載牽涉到擷取的 hello 整個 blob 使用 hello hello 內容**DownloadTo***/**BlobReadStream** 方便方法。</span><span class="sxs-lookup"><span data-stu-id="bcf81-144">Downloading an encrypted blob involves retrieving hello content of hello entire blob using hello **DownloadTo***/**BlobReadStream** convenience methods.</span></span> <span data-ttu-id="bcf81-145">hello 包裝的 CEK 解除包裝，且與 hello IV 一起使用 （儲存為 blob 中繼資料在此情況下） tooreturn hello 解密資料 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="bcf81-145">hello wrapped CEK is unwrapped and used together with hello IV (stored as blob metadata in this case) tooreturn hello decrypted data toohello users.</span></span>

<span data-ttu-id="bcf81-146">下載任意範圍 (**DownloadRange*** 方法)，在 hello 加密的 blob 包含調整 hello 範圍提供的順序 tooget 使用者少量的額外的資料可以是使用的 toosuccessfully 解密 hello要求的範圍。</span><span class="sxs-lookup"><span data-stu-id="bcf81-146">Downloading an arbitrary range (**DownloadRange*** methods) in hello encrypted blob involves adjusting hello range provided by users in order tooget a small amount of additional data that can be used toosuccessfully decrypt hello requested range.</span></span>

<span data-ttu-id="bcf81-147">所有 Blob 類型 (區塊 Blob、頁面 Blob 和附加 Blob) 都可以使用此機制進行加密/解密。</span><span class="sxs-lookup"><span data-stu-id="bcf81-147">All blob types (block blobs, page blobs, and append blobs) can be encrypted/decrypted using this scheme.</span></span>

### <a name="queues"></a><span data-ttu-id="bcf81-148">佇列</span><span class="sxs-lookup"><span data-stu-id="bcf81-148">Queues</span></span>
<span data-ttu-id="bcf81-149">因為佇列訊息可以是任何格式，hello 用戶端程式庫會定義包含 hello 訊息文字中的 hello 初始化向量 (IV) 與 hello 加密的內容加密金鑰 (CEK) 的自訂格式。</span><span class="sxs-lookup"><span data-stu-id="bcf81-149">Since queue messages can be of any format, hello client library defines a custom format that includes hello Initialization Vector (IV) and hello encrypted content encryption key (CEK) in hello message text.</span></span>

<span data-ttu-id="bcf81-150">在加密期間，hello 用戶端程式庫會產生 16 個位元組，以及隨機 CEK 32 個位元組的隨機 IV，並執行信封加密 hello 佇列的訊息文字使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="bcf81-150">During encryption, hello client library generates a random IV of 16 bytes along with a random CEK of 32 bytes and performs envelope encryption of hello queue message text using this information.</span></span> <span data-ttu-id="bcf81-151">hello 包裝 CEK 和一些額外的加密中繼資料接著會加入 toohello 加密的佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="bcf81-151">hello wrapped CEK and some additional encryption metadata are then added toohello encrypted queue message.</span></span> <span data-ttu-id="bcf81-152">這個修改過的訊息 （如下所示） 會儲存在 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="bcf81-152">This modified message (shown below) is stored on hello service.</span></span>

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

<span data-ttu-id="bcf81-153">在解密，hello 包裝的金鑰是擷取自 hello 佇列訊息，而且解除包裝。</span><span class="sxs-lookup"><span data-stu-id="bcf81-153">During decryption, hello wrapped key is extracted from hello queue message and unwrapped.</span></span> <span data-ttu-id="bcf81-154">hello IV 也是擷取自 hello 佇列訊息，並搭配 hello 解除包裝金鑰 toodecrypt hello 佇列訊息資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-154">hello IV is also extracted from hello queue message and used along with hello unwrapped key toodecrypt hello queue message data.</span></span> <span data-ttu-id="bcf81-155">請注意 hello 的加密中繼資料是小型 （下 500 個位元組），因此它沒有會計 hello 64 KB 限制的佇列訊息，而 hello 影響應該很容易管理。</span><span class="sxs-lookup"><span data-stu-id="bcf81-155">Note that hello encryption metadata is small (under 500 bytes), so while it does count toward hello 64KB limit for a queue message, hello impact should be manageable.</span></span>

### <a name="tables"></a><span data-ttu-id="bcf81-156">資料表</span><span class="sxs-lookup"><span data-stu-id="bcf81-156">Tables</span></span>
<span data-ttu-id="bcf81-157">hello 插入的實體屬性的用戶端程式庫支援加密和取代作業。</span><span class="sxs-lookup"><span data-stu-id="bcf81-157">hello client library supports encryption of entity properties for insert and replace operations.</span></span>

> [!NOTE]
> <span data-ttu-id="bcf81-158">目前不支援合併。</span><span class="sxs-lookup"><span data-stu-id="bcf81-158">Merge is not currently supported.</span></span> <span data-ttu-id="bcf81-159">屬性的子集可能已加密先前使用不同的金鑰，因為只要合併 hello 新內容，並更新 hello 中繼資料會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="bcf81-159">Since a subset of properties may have been encrypted previously using a different key, simply merging hello new properties and updating hello metadata will result in data loss.</span></span> <span data-ttu-id="bcf81-160">合併 需要進行額外的服務從 hello 服務呼叫 tooread hello 預先存在的實體，或使用每個屬性的新機碼，這兩者都不適用基於效能的考量。</span><span class="sxs-lookup"><span data-stu-id="bcf81-160">Merging either requires making extra service calls tooread hello pre-existing entity from hello service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>
> 
> 

<span data-ttu-id="bcf81-161">資料表資料加密的運作方式如下：</span><span class="sxs-lookup"><span data-stu-id="bcf81-161">Table data encryption works as follows:</span></span>  

1. <span data-ttu-id="bcf81-162">使用者指定 hello 屬性 toobe 加密。</span><span class="sxs-lookup"><span data-stu-id="bcf81-162">Users specify hello properties toobe encrypted.</span></span>
2. <span data-ttu-id="bcf81-163">hello 用戶端程式庫會產生 16 個位元組的隨機內容加密金鑰 (CEK) 32 個位元組，針對每個實體，以及隨機初始化向量 (IV)，並執行 hello 藉由衍生新的 IV，每個加密的個別屬性 toobe 信封加密屬性。</span><span class="sxs-lookup"><span data-stu-id="bcf81-163">hello client library generates a random Initialization Vector (IV) of 16 bytes along with a random content encryption key (CEK) of 32 bytes for every entity, and performs envelope encryption on hello individual properties toobe encrypted by deriving a new IV per property.</span></span> <span data-ttu-id="bcf81-164">加密的 hello 屬性會儲存為二進位資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-164">hello encrypted property is stored as binary data.</span></span>
3. <span data-ttu-id="bcf81-165">hello 包裝 CEK 和一些額外的加密中繼資料會儲存為兩個額外的保留屬性。</span><span class="sxs-lookup"><span data-stu-id="bcf81-165">hello wrapped CEK and some additional encryption metadata are then stored as two additional reserved properties.</span></span> <span data-ttu-id="bcf81-166">hello 第一個保留的屬性 (_ClientEncryptionMetadata1) 是保存 hello IV、 版本和包裝的金鑰資訊的字串屬性。</span><span class="sxs-lookup"><span data-stu-id="bcf81-166">hello first reserved property (_ClientEncryptionMetadata1) is a string property that holds hello information about IV, version, and wrapped key.</span></span> <span data-ttu-id="bcf81-167">hello 第二個保留的屬性 (_ClientEncryptionMetadata2) 是保留加密的 hello 屬性的 hello 資訊的二進位屬性。</span><span class="sxs-lookup"><span data-stu-id="bcf81-167">hello second reserved property (_ClientEncryptionMetadata2) is a binary property that holds hello information about hello properties that are encrypted.</span></span> <span data-ttu-id="bcf81-168">此第二個屬性 (_ClientEncryptionMetadata2) 中的 hello 資訊本身是加密。</span><span class="sxs-lookup"><span data-stu-id="bcf81-168">hello information in this second property (_ClientEncryptionMetadata2) is itself encrypted.</span></span>
4. <span data-ttu-id="bcf81-169">Toothese 其他保留所需的內容加密，因為使用者可能現在有只 250 的自訂屬性，而不是 252。</span><span class="sxs-lookup"><span data-stu-id="bcf81-169">Due toothese additional reserved properties required for encryption, users may now have only 250 custom properties instead of 252.</span></span> <span data-ttu-id="bcf81-170">hello hello 實體的大小總計必須小於 1MB。</span><span class="sxs-lookup"><span data-stu-id="bcf81-170">hello total size of hello entity must be less than 1 MB.</span></span>

<span data-ttu-id="bcf81-171">請注意，只有字串屬性可以加密。</span><span class="sxs-lookup"><span data-stu-id="bcf81-171">Note that only string properties can be encrypted.</span></span> <span data-ttu-id="bcf81-172">如果其他屬性類型 toobe 加密，它們必須轉換的 toostrings。</span><span class="sxs-lookup"><span data-stu-id="bcf81-172">If other types of properties are toobe encrypted, they must be converted toostrings.</span></span> <span data-ttu-id="bcf81-173">hello 加密字串 hello 服務上儲存為二進位屬性，而它們會轉換後 toostrings 解密之後。</span><span class="sxs-lookup"><span data-stu-id="bcf81-173">hello encrypted strings are stored on hello service as binary properties, and they are converted back toostrings after decryption.</span></span>

<span data-ttu-id="bcf81-174">對於資料表，此外 toohello 加密原則，使用者必須指定 hello 屬性 toobe 加密。</span><span class="sxs-lookup"><span data-stu-id="bcf81-174">For tables, in addition toohello encryption policy, users must specify hello properties toobe encrypted.</span></span> <span data-ttu-id="bcf81-175">作法是指定 [EncryptProperty] 屬性 (針對衍生自 TableEntity 的 POCO 實體)，或在要求選項中指定加密解析程式。</span><span class="sxs-lookup"><span data-stu-id="bcf81-175">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="bcf81-176">加密解析程式是委派，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。</span><span class="sxs-lookup"><span data-stu-id="bcf81-176">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="bcf81-177">在加密期間，是否應該加密屬性，同時寫入 toohello 網路 hello 用戶端程式庫時，會使用此資訊 toodecide。</span><span class="sxs-lookup"><span data-stu-id="bcf81-177">During encryption, hello client library will use this information toodecide whether a property should be encrypted while writing toohello wire.</span></span> <span data-ttu-id="bcf81-178">hello 委派也提供 hello 可能性的邏輯屬性加密的方式。</span><span class="sxs-lookup"><span data-stu-id="bcf81-178">hello delegate also provides for hello possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="bcf81-179">(例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，就是不必要的 tooprovide 讀取或查詢實體時此資訊。</span><span class="sxs-lookup"><span data-stu-id="bcf81-179">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary tooprovide this information while reading or querying entities.</span></span>

### <a name="batch-operations"></a><span data-ttu-id="bcf81-180">批次作業</span><span class="sxs-lookup"><span data-stu-id="bcf81-180">Batch Operations</span></span>
<span data-ttu-id="bcf81-181">在批次作業中，hello 相同 KEK 會使用於跨所有 hello 資料列中的批次作業因為 hello 用戶端程式庫只允許一個選項物件 （並因此一個原則/KEK） 每個批次作業。</span><span class="sxs-lookup"><span data-stu-id="bcf81-181">In batch operations, hello same KEK will be used across all hello rows in that batch operation because hello client library only allows one options object (and hence one policy/KEK) per batch operation.</span></span> <span data-ttu-id="bcf81-182">不過，hello 用戶端程式庫會在內部產生新的隨機 IV 和每個資料列的隨機 CEK hello 批次中。</span><span class="sxs-lookup"><span data-stu-id="bcf81-182">However, hello client library will internally generate a new random IV and random CEK per row in hello batch.</span></span> <span data-ttu-id="bcf81-183">使用者也可以選擇 tooencrypt 不同的屬性，針對每個作業 hello 批次中在 hello 加密解析程式中定義此行為。</span><span class="sxs-lookup"><span data-stu-id="bcf81-183">Users can also choose tooencrypt different properties for every operation in hello batch by defining this behavior in hello encryption resolver.</span></span>

### <a name="queries"></a><span data-ttu-id="bcf81-184">查詢</span><span class="sxs-lookup"><span data-stu-id="bcf81-184">Queries</span></span>
<span data-ttu-id="bcf81-185">tooperform 查詢作業，您必須指定索引鍵的解析程式所能 tooresolve 所有 hello hello 結果集中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bcf81-185">tooperform query operations, you must specify a key resolver that is able tooresolve all hello keys in hello result set.</span></span> <span data-ttu-id="bcf81-186">如果 hello 查詢結果中包含的實體不能是解析的 tooa 提供者，hello 用戶端程式庫會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bcf81-186">If an entity contained in hello query result cannot be resolved tooa provider, hello client library will throw an error.</span></span> <span data-ttu-id="bcf81-187">為執行伺服器端投影的任何查詢，hello 用戶端程式庫將由預設 toohello 選取資料行加入 hello 的特殊加密中繼資料屬性 （_ClientEncryptionMetadata1 和 _ClientEncryptionMetadata2）。</span><span class="sxs-lookup"><span data-stu-id="bcf81-187">For any query that performs server-side projections, hello client library will add hello special encryption metadata properties (_ClientEncryptionMetadata1 and _ClientEncryptionMetadata2) by default toohello selected columns.</span></span>

## <a name="azure-key-vault"></a><span data-ttu-id="bcf81-188">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="bcf81-188">Azure Key Vault</span></span>
<span data-ttu-id="bcf81-189">Azure 金鑰保存庫可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="bcf81-189">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span> <span data-ttu-id="bcf81-190">使用 Azure 金鑰保存庫時，使用者可以使用受硬體安全模組 (HSM) 保護的金鑰來加密金鑰和密碼 (例如驗證金鑰、儲存體帳戶金鑰、資料加密金鑰、.PFX 檔案和密碼)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-190">By using Azure Key Vault, users can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .PFX files, and passwords) by using keys that are protected by hardware security modules (HSMs).</span></span> <span data-ttu-id="bcf81-191">如需詳細資訊，請參閱 [什麼是 Azure 金鑰保存庫？](../key-vault/key-vault-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-191">For more information, see [What is Azure Key Vault?](../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="bcf81-192">hello 儲存體用戶端程式庫會使用整個 Azure hello 金鑰保存庫核心程式庫中的順序 tooprovide 通用架構，來管理金鑰。</span><span class="sxs-lookup"><span data-stu-id="bcf81-192">hello storage client library uses hello Key Vault core library in order tooprovide a common framework across Azure for managing keys.</span></span> <span data-ttu-id="bcf81-193">使用者也會使用 hello 金鑰保存庫延伸模組程式庫的 hello 其他好處。</span><span class="sxs-lookup"><span data-stu-id="bcf81-193">Users also get hello additional benefit of using hello Key Vault extensions library.</span></span> <span data-ttu-id="bcf81-194">hello 延伸模組程式庫提供有用的功能，簡單且順暢對稱/RSA 本機和雲端金鑰提供者，以及與彙總快取。</span><span class="sxs-lookup"><span data-stu-id="bcf81-194">hello extensions library provides useful functionality around simple and seamless Symmetric/RSA local and cloud key providers as well as with aggregation and caching.</span></span>

### <a name="interface-and-dependencies"></a><span data-ttu-id="bcf81-195">介面和相依性</span><span class="sxs-lookup"><span data-stu-id="bcf81-195">Interface and dependencies</span></span>
<span data-ttu-id="bcf81-196">有三個金鑰保存庫封裝：</span><span class="sxs-lookup"><span data-stu-id="bcf81-196">There are three Key Vault packages:</span></span>

* <span data-ttu-id="bcf81-197">Microsoft.Azure.KeyVault.Core 包含 hello IKey 和 IKeyResolver。</span><span class="sxs-lookup"><span data-stu-id="bcf81-197">Microsoft.Azure.KeyVault.Core contains hello IKey and IKeyResolver.</span></span> <span data-ttu-id="bcf81-198">這是不具有相依性的小型封裝。</span><span class="sxs-lookup"><span data-stu-id="bcf81-198">It is a small package with no dependencies.</span></span> <span data-ttu-id="bcf81-199">hello.NET 的儲存體用戶端程式庫將其定義為相依性。</span><span class="sxs-lookup"><span data-stu-id="bcf81-199">hello storage client library for .NET defines it as a dependency.</span></span>
* <span data-ttu-id="bcf81-200">Microsoft.Azure.KeyVault 包含 hello 金鑰保存庫 REST 用戶端。</span><span class="sxs-lookup"><span data-stu-id="bcf81-200">Microsoft.Azure.KeyVault contains hello Key Vault REST client.</span></span>
* <span data-ttu-id="bcf81-201">Microsoft.Azure.KeyVault.Extensions 包含延伸模組程式碼，其中包含密碼編譯演算法的實作及 RSAKey 和 SymmetricKey。</span><span class="sxs-lookup"><span data-stu-id="bcf81-201">Microsoft.Azure.KeyVault.Extensions contains extension code that includes implementations of cryptographic algorithms and an RSAKey and a SymmetricKey.</span></span> <span data-ttu-id="bcf81-202">它相依於 hello 核心和 KeyVault 命名空間並提供功能 toodefine 彙總的解析程式 （當使用者想 toouse 多個索引鍵的提供者） 和快取索引鍵的解析程式。</span><span class="sxs-lookup"><span data-stu-id="bcf81-202">It depends on hello Core and KeyVault namespaces and provides functionality toodefine an aggregate resolver (when users want toouse multiple key providers) and a caching key resolver.</span></span> <span data-ttu-id="bcf81-203">雖然 hello 儲存體用戶端程式庫不會直接依賴這個封裝，如果使用者想 toouse Azure 金鑰保存庫 toostore 其索引鍵或 toouse hello 金鑰保存庫的擴充功能 tooconsume hello 本機和雲端密碼編譯提供者，它們會需要此封裝。</span><span class="sxs-lookup"><span data-stu-id="bcf81-203">Although hello storage client library does not directly depend on this package, if users wish toouse Azure Key Vault toostore their keys or toouse hello Key Vault extensions tooconsume hello local and cloud cryptographic providers, they will need this package.</span></span>

<span data-ttu-id="bcf81-204">金鑰保存庫是專為高價值的主要金鑰而設計，個別金鑰保存庫的節流限制都以此為設計重點。</span><span class="sxs-lookup"><span data-stu-id="bcf81-204">Key Vault is designed for high-value master keys, and throttling limits per Key Vault are designed with this in mind.</span></span> <span data-ttu-id="bcf81-205">執行時用戶端加密與金鑰保存庫，hello 慣用的模型會 toouse 對稱主要金鑰儲存為金鑰保存庫中的機密資料，並在本機快取。</span><span class="sxs-lookup"><span data-stu-id="bcf81-205">When performing client-side encryption with Key Vault, hello preferred model is toouse symmetric master keys stored as secrets in Key Vault and cached locally.</span></span> <span data-ttu-id="bcf81-206">使用者必須進行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="bcf81-206">Users must do hello following:</span></span>

1. <span data-ttu-id="bcf81-207">建立密碼離線，並將它上傳 tooKey 保存庫。</span><span class="sxs-lookup"><span data-stu-id="bcf81-207">Create a secret offline and upload it tooKey Vault.</span></span>
2. <span data-ttu-id="bcf81-208">參數 tooresolve hello hello 密碼加密的目前版本，並快取這項資訊在本機使用 hello 密碼的基底識別碼。</span><span class="sxs-lookup"><span data-stu-id="bcf81-208">Use hello secret's base identifier as a parameter tooresolve hello current version of hello secret for encryption and cache this information locally.</span></span> <span data-ttu-id="bcf81-209">用於 CachingKeyResolver 快取。使用者是未預期的 tooimplement 自己的快取邏輯。</span><span class="sxs-lookup"><span data-stu-id="bcf81-209">Use CachingKeyResolver for caching; users are not expected tooimplement their own caching logic.</span></span>
3. <span data-ttu-id="bcf81-210">建立 hello 加密原則時，使用 hello 快取解析程式做為輸入。</span><span class="sxs-lookup"><span data-stu-id="bcf81-210">Use hello caching resolver as an input while creating hello encryption policy.</span></span>

<span data-ttu-id="bcf81-211">金鑰保存庫的使用方式的更多關於位於 hello[加密程式碼範例](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-211">More information regarding Key Vault usage can be found in hello [encryption code samples](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples).</span></span>

## <a name="best-practices"></a><span data-ttu-id="bcf81-212">最佳作法</span><span class="sxs-lookup"><span data-stu-id="bcf81-212">Best practices</span></span>
<span data-ttu-id="bcf81-213">加密已支援只能在 hello.NET 的儲存體用戶端程式庫中。</span><span class="sxs-lookup"><span data-stu-id="bcf81-213">Encryption support is available only in hello storage client library for .NET.</span></span> <span data-ttu-id="bcf81-214">Windows Phone 和 Windows 執行階段目前不支援加密。</span><span class="sxs-lookup"><span data-stu-id="bcf81-214">Windows Phone and Windows Runtime do not currently support encryption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcf81-215">使用用戶端加密時，請留意以下重點：</span><span class="sxs-lookup"><span data-stu-id="bcf81-215">Be aware of these important points when using client-side encryption:</span></span>
> 
> * <span data-ttu-id="bcf81-216">當從進行讀取或寫入 tooan 加密 blob、 使用完整的 blob 上傳的命令和範圍/整個 blob 下載命令。</span><span class="sxs-lookup"><span data-stu-id="bcf81-216">When reading from or writing tooan encrypted blob, use whole blob upload commands and range/whole blob download commands.</span></span> <span data-ttu-id="bcf81-217">避免撰寫 tooan 加密的 blob，使用通訊協定作業，例如將區塊、 放置區塊清單、 寫入的頁面，清除頁面或附加區塊;否則，您可能會破壞 hello 加密的 blob，並使它無法讀取。</span><span class="sxs-lookup"><span data-stu-id="bcf81-217">Avoid writing tooan encrypted blob using protocol operations such as Put Block, Put Block List, Write Pages, Clear Pages, or Append Block; otherwise you may corrupt hello encrypted blob and make it unreadable.</span></span>
> * <span data-ttu-id="bcf81-218">對於資料表，存在類似的條件約束。</span><span class="sxs-lookup"><span data-stu-id="bcf81-218">For tables, a similar constraint exists.</span></span> <span data-ttu-id="bcf81-219">能謹慎 toonot 更新加密內容，而無須更新 hello 加密中繼資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-219">Be careful toonot update encrypted properties without updating hello encryption metadata.</span></span>
> * <span data-ttu-id="bcf81-220">如果您在 hello 加密的 blob 上設定中繼資料，您可能會覆寫 hello 加密相關中繼資料所需來解密，因為設定中繼資料不是加總。</span><span class="sxs-lookup"><span data-stu-id="bcf81-220">If you set metadata on hello encrypted blob, you may overwrite hello encryption-related metadata required for decryption, since setting metadata is not additive.</span></span> <span data-ttu-id="bcf81-221">快照集也是如此。在為加密的 Blob 建立快照集時，請避免指定中繼資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-221">This is also true for snapshots; avoid specifying metadata while creating a snapshot of an encrypted blob.</span></span> <span data-ttu-id="bcf81-222">如果必須設定中繼資料，是確定 toocall hello **FetchAttributes**方法的第一個 tooget hello 目前的加密中繼資料和中繼資料在設定時，避免並行寫入。</span><span class="sxs-lookup"><span data-stu-id="bcf81-222">If metadata must be set, be sure toocall hello **FetchAttributes** method first tooget hello current encryption metadata, and avoid concurrent writes while metadata is being set.</span></span>
> * <span data-ttu-id="bcf81-223">啟用 hello **RequireEncryption** hello 應該僅適用於的使用者的預設要求選項中的屬性是否已加密資料。</span><span class="sxs-lookup"><span data-stu-id="bcf81-223">Enable hello **RequireEncryption** property in hello default request options for users that should work only with encrypted data.</span></span> <span data-ttu-id="bcf81-224">如需詳細資訊請參閱下方內容。</span><span class="sxs-lookup"><span data-stu-id="bcf81-224">See below for more info.</span></span>
> 
> 

## <a name="client-api--interface"></a><span data-ttu-id="bcf81-225">用戶端 API / 介面</span><span class="sxs-lookup"><span data-stu-id="bcf81-225">Client API / Interface</span></span>
<span data-ttu-id="bcf81-226">使用者在建立 EncryptionPolicy 物件時，可以只提供金鑰 (實作 IKey)、只提供者解析程式 (實作 IKeyResolver)，或兩者都提供。</span><span class="sxs-lookup"><span data-stu-id="bcf81-226">While creating an EncryptionPolicy object, users can provide only a Key (implementing IKey), only a resolver (implementing IKeyResolver), or both.</span></span> <span data-ttu-id="bcf81-227">IKey 是 hello 基本金鑰，用來識別索引鍵的識別項和類型，提供用來包裝/解除包裝的 hello 邏輯。</span><span class="sxs-lookup"><span data-stu-id="bcf81-227">IKey is hello basic key type that is identified using a key identifier and that provides hello logic for wrapping/unwrapping.</span></span> <span data-ttu-id="bcf81-228">IKeyResolver hello 解密程序期間會使用的 tooresolve 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bcf81-228">IKeyResolver is used tooresolve a key during hello decryption process.</span></span> <span data-ttu-id="bcf81-229">它定義 ResolveKey 方法，可根據金鑰識別碼傳回 IKey。</span><span class="sxs-lookup"><span data-stu-id="bcf81-229">It defines a ResolveKey method that returns an IKey given a key identifier.</span></span> <span data-ttu-id="bcf81-230">這會提供使用者 hello 能力 toochoose 之間的多個位置中受管理的多個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="bcf81-230">This provides users hello ability toochoose between multiple keys that are managed in multiple locations.</span></span>

* <span data-ttu-id="bcf81-231">用於加密，hello 索引鍵永遠且沒有金鑰 hello 情況下會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="bcf81-231">For encryption, hello key is used always and hello absence of a key will result in an error.</span></span>
* <span data-ttu-id="bcf81-232">解密：</span><span class="sxs-lookup"><span data-stu-id="bcf81-232">For decryption:</span></span>
  * <span data-ttu-id="bcf81-233">如果指定 tooget hello 索引鍵，則會叫用 hello 索引鍵的解析程式。</span><span class="sxs-lookup"><span data-stu-id="bcf81-233">hello key resolver is invoked if specified tooget hello key.</span></span> <span data-ttu-id="bcf81-234">如果指定 hello 解析程式，但是沒有 hello 之金鑰識別碼的對應，會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bcf81-234">If hello resolver is specified but does not have a mapping for hello key identifier, an error is thrown.</span></span>
  * <span data-ttu-id="bcf81-235">如果未指定解析程式，但指定的索引鍵，hello 金鑰可用如果其識別項所需的 hello 與金鑰識別碼相符。</span><span class="sxs-lookup"><span data-stu-id="bcf81-235">If resolver is not specified but a key is specified, hello key is used if its identifier matches hello required key identifier.</span></span> <span data-ttu-id="bcf81-236">如果 hello 識別碼不符合，則會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="bcf81-236">If hello identifier does not match, an error is thrown.</span></span>

<span data-ttu-id="bcf81-237">hello[加密範例](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples)示範更詳細的端對端案例，適用於 blob、 佇列和資料表，以及與金鑰保存庫整合。</span><span class="sxs-lookup"><span data-stu-id="bcf81-237">hello [encryption samples](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) demonstrate a more detailed end-to-end scenario for blobs, queues and tables, along with Key Vault integration.</span></span>

### <a name="requireencryption-mode"></a><span data-ttu-id="bcf81-238">RequireEncryption 模式</span><span class="sxs-lookup"><span data-stu-id="bcf81-238">RequireEncryption mode</span></span>
<span data-ttu-id="bcf81-239">使用者可以針對所有上傳和下載都必須加密的作業模式，從中選擇啟用。</span><span class="sxs-lookup"><span data-stu-id="bcf81-239">Users can optionally enable a mode of operation where all uploads and downloads must be encrypted.</span></span> <span data-ttu-id="bcf81-240">在此模式中，嘗試 tooupload 資料，而不會加密 hello 服務的加密原則或下載資料不會失敗 hello 用戶端上。</span><span class="sxs-lookup"><span data-stu-id="bcf81-240">In this mode, attempts tooupload data without an encryption policy or download data that is not encrypted on hello service will fail on hello client.</span></span> <span data-ttu-id="bcf81-241">hello **RequireEncryption** hello 要求選項物件的屬性會控制此行為。</span><span class="sxs-lookup"><span data-stu-id="bcf81-241">hello **RequireEncryption** property of hello request options object controls this behavior.</span></span> <span data-ttu-id="bcf81-242">如果您的應用程式將會加密儲存在 Azure 儲存體中的所有物件，則您可以將 hello **RequireEncryption** hello hello 服務用戶端物件的預設要求選項上的屬性。</span><span class="sxs-lookup"><span data-stu-id="bcf81-242">If your application will encrypt all objects stored in Azure Storage, then you can set hello **RequireEncryption** property on hello default request options for hello service client object.</span></span> <span data-ttu-id="bcf81-243">例如，設定**CloudBlobClient.DefaultRequestOptions.RequireEncryption**太**true** toorequire 加密所有的 blob 作業透過該用戶端物件來執行。</span><span class="sxs-lookup"><span data-stu-id="bcf81-243">For example, set **CloudBlobClient.DefaultRequestOptions.RequireEncryption** too**true** toorequire encryption for all blob operations performed through that client object.</span></span>

### <a name="blob-service-encryption"></a><span data-ttu-id="bcf81-244">Blob 服務加密</span><span class="sxs-lookup"><span data-stu-id="bcf81-244">Blob service encryption</span></span>
<span data-ttu-id="bcf81-245">建立**BlobEncryptionPolicy**物件，並將它設定在 hello 要求選項 (每個應用程式開發介面或使用用戶端層級**DefaultRequestOptions**)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-245">Create a **BlobEncryptionPolicy** object and set it in hello request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="bcf81-246">所有其他項目將 hello 用戶端程式庫在內部進行處理。</span><span class="sxs-lookup"><span data-stu-id="bcf81-246">Everything else will be handled by hello client library internally.</span></span>

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set hello encryption policy on hello request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload hello encrypted contents toohello blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt hello encrypted contents from hello blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a><span data-ttu-id="bcf81-247">佇列服務加密</span><span class="sxs-lookup"><span data-stu-id="bcf81-247">Queue service encryption</span></span>
<span data-ttu-id="bcf81-248">建立**QueueEncryptionPolicy**物件，並將它設定在 hello 要求選項 (每個應用程式開發介面或使用用戶端層級**DefaultRequestOptions**)。</span><span class="sxs-lookup"><span data-stu-id="bcf81-248">Create a **QueueEncryptionPolicy** object and set it in hello request options (per API or at a client level by using **DefaultRequestOptions**).</span></span> <span data-ttu-id="bcf81-249">所有其他項目將 hello 用戶端程式庫在內部進行處理。</span><span class="sxs-lookup"><span data-stu-id="bcf81-249">Everything else will be handled by hello client library internally.</span></span>

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a><span data-ttu-id="bcf81-250">資料表服務加密</span><span class="sxs-lookup"><span data-stu-id="bcf81-250">Table service encryption</span></span>
<span data-ttu-id="bcf81-251">此外 toocreating 加密原則和設定要求的選項，您必須指定**EncryptionResolver**中**TableRequestOptions**，或在 hello [EncryptProperty] 屬性hello 實體。</span><span class="sxs-lookup"><span data-stu-id="bcf81-251">In addition toocreating an encryption policy and setting it on request options, you must either specify an **EncryptionResolver** in **TableRequestOptions**, or set hello [EncryptProperty] attribute on hello entity.</span></span>

#### <a name="using-hello-resolver"></a><span data-ttu-id="bcf81-252">使用 hello 解析程式</span><span class="sxs-lookup"><span data-stu-id="bcf81-252">Using hello resolver</span></span>

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
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
 // No need toospecify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a><span data-ttu-id="bcf81-253">使用屬性</span><span class="sxs-lookup"><span data-stu-id="bcf81-253">Using attributes</span></span>
<span data-ttu-id="bcf81-254">如前所述，如果 hello 實體實作 TableEntity，然後 hello 屬性可以以裝飾 hello [EncryptProperty] 屬性，而不是指定 hello **EncryptionResolver**。</span><span class="sxs-lookup"><span data-stu-id="bcf81-254">As mentioned above, if hello entity implements TableEntity, then hello properties can be decorated with hello [EncryptProperty] attribute instead of specifying hello **EncryptionResolver**.</span></span>

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a><span data-ttu-id="bcf81-255">加密和效能</span><span class="sxs-lookup"><span data-stu-id="bcf81-255">Encryption and performance</span></span>
<span data-ttu-id="bcf81-256">請注意，加密您的儲存體資料會造成額外的效能負擔。</span><span class="sxs-lookup"><span data-stu-id="bcf81-256">Note that encrypting your storage data results in additional performance overhead.</span></span> <span data-ttu-id="bcf81-257">hello 必須產生金鑰和 IV，hello 內容本身必須經過加密、 和其他中繼資料必須格式化，並且上傳內容。</span><span class="sxs-lookup"><span data-stu-id="bcf81-257">hello content key and IV must be generated, hello content itself must be encrypted, and additional meta-data must be formatted and uploaded.</span></span> <span data-ttu-id="bcf81-258">這項負擔會根據 hello 所加密的資料數量而有所不同。</span><span class="sxs-lookup"><span data-stu-id="bcf81-258">This overhead will vary depending on hello quantity of data being encrypted.</span></span> <span data-ttu-id="bcf81-259">我們建議客戶一定要在開發期間測試其應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="bcf81-259">We recommend that customers always test their applications for performance during development.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcf81-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcf81-260">Next steps</span></span>
* [<span data-ttu-id="bcf81-261">教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob</span><span class="sxs-lookup"><span data-stu-id="bcf81-261">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>](storage-encrypt-decrypt-blobs-key-vault.md)
* <span data-ttu-id="bcf81-262">下載 hello [.NET NuGet 套件的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)</span><span class="sxs-lookup"><span data-stu-id="bcf81-262">Download hello [Azure Storage Client Library for .NET NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage)</span></span>
* <span data-ttu-id="bcf81-263">下載 Azure 金鑰保存庫 NuGet hello[核心](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/)，[用戶端](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/)，和[延伸](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/)封裝</span><span class="sxs-lookup"><span data-stu-id="bcf81-263">Download hello Azure Key Vault NuGet [Core](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [Client](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), and [Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) packages</span></span>  
* <span data-ttu-id="bcf81-264">請瀏覽 hello [Azure 金鑰保存庫文件](../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="bcf81-264">Visit hello [Azure Key Vault Documentation](../key-vault/key-vault-whatis.md)</span></span>
