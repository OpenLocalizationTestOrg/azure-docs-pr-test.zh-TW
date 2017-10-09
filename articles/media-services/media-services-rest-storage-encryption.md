---
title: "aaaEncrypting 使用 AMS REST API 的儲存體加密內容"
description: "深入了解如何 tooencrypt 使用 AMS REST Api 的儲存體加密內容。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="6fc48-103">以儲存體加密來加密您的內容</span><span class="sxs-lookup"><span data-stu-id="6fc48-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="6fc48-104">強烈建議 tooencrypt 您使用 AES 256 在本機的內容位元加密，然後將它上傳 tooAzure 儲存體的位置儲存加密在靜止。</span><span class="sxs-lookup"><span data-stu-id="6fc48-104">It is highly recommended tooencrypt your content locally using AES-256 bit encryption and then upload it tooAzure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="6fc48-105">這篇文章提供 AMS 儲存體加密的概觀，並顯示您 tooupload hello 儲存體加密內容的方式：</span><span class="sxs-lookup"><span data-stu-id="6fc48-105">This article gives an overview of AMS storage encryption and shows you how tooupload hello storage encrypted content:</span></span>

* <span data-ttu-id="6fc48-106">建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="6fc48-106">Create a content key.</span></span>
* <span data-ttu-id="6fc48-107">建立資產。</span><span class="sxs-lookup"><span data-stu-id="6fc48-107">Create an Asset.</span></span> <span data-ttu-id="6fc48-108">建立 hello 資產時，請設定 hello AssetCreationOption tooStorageEncryption。</span><span class="sxs-lookup"><span data-stu-id="6fc48-108">Set hello AssetCreationOption tooStorageEncryption when creating hello Asset.</span></span>
  
     <span data-ttu-id="6fc48-109">加密的資產有 toobe 內容金鑰相關聯。</span><span class="sxs-lookup"><span data-stu-id="6fc48-109">Encrypted assets have toobe associated with content keys.</span></span>
* <span data-ttu-id="6fc48-110">連結 hello 內容金鑰 toohello 資產。</span><span class="sxs-lookup"><span data-stu-id="6fc48-110">Link hello content key toohello asset.</span></span>  
* <span data-ttu-id="6fc48-111">設定 hello 加密相關 hello AssetFile 實體上的參數。</span><span class="sxs-lookup"><span data-stu-id="6fc48-111">Set hello encryption related parameters on hello AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="6fc48-112">考量</span><span class="sxs-lookup"><span data-stu-id="6fc48-112">Considerations</span></span> 

<span data-ttu-id="6fc48-113">如果您想 toodeliver 儲存體加密資產時，您必須設定 hello 資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="6fc48-113">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="6fc48-114">在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="6fc48-114">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="6fc48-115">如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-rest-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc48-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="6fc48-116">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="6fc48-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="6fc48-117">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc48-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="6fc48-118">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="6fc48-118">Connect tooMedia Services</span></span>

<span data-ttu-id="6fc48-119">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc48-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="6fc48-120">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="6fc48-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="6fc48-121">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="6fc48-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="6fc48-122">儲存體加密概觀</span><span class="sxs-lookup"><span data-stu-id="6fc48-122">Storage encryption overview</span></span>
<span data-ttu-id="6fc48-123">適用於 hello AMS 儲存體加密**AES CTR**模式加密 toohello 整個檔案。</span><span class="sxs-lookup"><span data-stu-id="6fc48-123">hello AMS storage encryption applies **AES-CTR** mode encryption toohello entire file.</span></span>  <span data-ttu-id="6fc48-124">AES CTR 模式是可加密任意長度資料且不需填補的區塊編碼器。</span><span class="sxs-lookup"><span data-stu-id="6fc48-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="6fc48-125">它的運作方式與 hello AES 演算法，然後 XOR ing hello 輸出的 AES hello 資料 tooencrypt 計數器區塊的加密或解密。</span><span class="sxs-lookup"><span data-stu-id="6fc48-125">It operates by encrypting a counter block with hello AES algorithm and then XOR-ing hello output of AES with hello data tooencrypt or decrypt.</span></span>  <span data-ttu-id="6fc48-126">hello 計數器區塊由建構 hello hello InitializationVector toobytes 0 too7 hello 計數器值的值複製，hello 計數器值的 8 位元組 too15 設定 toozero。</span><span class="sxs-lookup"><span data-stu-id="6fc48-126">hello counter block used is constructed by copying hello value of hello InitializationVector toobytes 0 too7 of hello counter value and bytes 8 too15 of hello counter value are set toozero.</span></span> <span data-ttu-id="6fc48-127">Hello 16 位元組計數器區塊，too15 8 個位元組的可用如同簡單的 64 位元不帶正負號的整數，都會加一的每個後續區塊處理的資料保存在網路位元組順序 （也就是 hello 最小顯著性位元組為單位）。</span><span class="sxs-lookup"><span data-stu-id="6fc48-127">Of hello 16 byte counter block, bytes 8 too15 (i.e. hello least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="6fc48-128">請注意，如果此整數達到 hello 最大值 (0xFFFFFFFFFFFFFFFF) 再增加其重設 hello 區塊計數器 toozero (8 位元組 too15) 而不會影響其他 hello hello 計數器 (也就是 0 位元組 too7) 的 64 位元。</span><span class="sxs-lookup"><span data-stu-id="6fc48-128">Note that if this integer reaches hello maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets hello block counter toozero (bytes 8 too15) without affecting hello other 64 bits of hello counter (i.e. bytes 0 too7).</span></span>   <span data-ttu-id="6fc48-129">順序 toomaintain hello hello AES CTR 模式加密的安全性、 hello InitializationVector 值指定的索引鍵識別項的每個內容的索引鍵應該是唯一的每個檔案和檔案都必須小於 2 ^64 區塊的長度。</span><span class="sxs-lookup"><span data-stu-id="6fc48-129">In order toomaintain hello security of hello AES-CTR mode encryption, hello InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="6fc48-130">這是 tooensure 計數器值絕不會是可重複使用指定的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="6fc48-130">This is tooensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="6fc48-131">如需 hello CTR 模式的詳細資訊，請參閱[wiki 本頁](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR)（hello wiki 文章使用 hello 詞彙"Nonce"，而不是"InitializationVector"）。</span><span class="sxs-lookup"><span data-stu-id="6fc48-131">For more information about hello CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello wiki article uses hello term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="6fc48-132">使用**儲存體加密**tooencrypt 您清除的內容，在本機使用 AES 256 位元加密並再將它上傳 tooAzure 儲存體的方式予以儲存加密在靜止。</span><span class="sxs-lookup"><span data-stu-id="6fc48-132">Use **Storage Encryption** tooencrypt your clear content locally using AES-256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="6fc48-133">使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。</span><span class="sxs-lookup"><span data-stu-id="6fc48-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="6fc48-134">儲存體加密的 hello 主要使用案例是當您想的 toosecure 強式加密您高品質的輸入的媒體檔案放在磁碟。</span><span class="sxs-lookup"><span data-stu-id="6fc48-134">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="6fc48-135">在順序 toodeliver 儲存體加密資產，您必須設定 hello 資產的傳遞原則，讓媒體服務知道要如何 toodeliver 您的內容。</span><span class="sxs-lookup"><span data-stu-id="6fc48-135">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="6fc48-136">在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則 （例如 AES、 一般加密或不加密）。</span><span class="sxs-lookup"><span data-stu-id="6fc48-136">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="6fc48-137">建立要用於加密的 ContentKey</span><span class="sxs-lookup"><span data-stu-id="6fc48-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="6fc48-138">加密的資產有 toobe 與儲存體加密金鑰相關聯。</span><span class="sxs-lookup"><span data-stu-id="6fc48-138">Encrypted assets have toobe associated with Storage Encryption key.</span></span> <span data-ttu-id="6fc48-139">您必須建立 hello 內容的索引鍵 toobe 用於加密之前建立 hello 資產檔案。</span><span class="sxs-lookup"><span data-stu-id="6fc48-139">You must create hello content key toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="6fc48-140">本章節描述如何 toocreate 內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="6fc48-140">This section describes how toocreate a content key.</span></span>

<span data-ttu-id="6fc48-141">hello 以下是產生內容金鑰會與您想要 toobe 加密的資產相關聯的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="6fc48-141">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="6fc48-142">對於儲存體加密，請隨機產生 32 個位元組的 AES 金鑰。</span><span class="sxs-lookup"><span data-stu-id="6fc48-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="6fc48-143">這會成為 hello 資產，這表示相關聯的所有檔案的內容索引鍵與該資產將會需要 toouse hello 同內容金鑰解密期間。</span><span class="sxs-lookup"><span data-stu-id="6fc48-143">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="6fc48-144">呼叫 hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid)和[GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey)方法 tooget hello 正確的 X.509 憑證必須使用的 tooencrypt 將內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="6fc48-144">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="6fc48-145">將內容金鑰加密使用公開金鑰的 X.509 憑證的 hello hello。</span><span class="sxs-lookup"><span data-stu-id="6fc48-145">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="6fc48-146">Media Services.NET SDK 會使用 RSA OAEP 執行 hello 加密時。</span><span class="sxs-lookup"><span data-stu-id="6fc48-146">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="6fc48-147">您可以看到.NET 中的範例 hello [EncryptSymmetricKeyData 函式](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)。</span><span class="sxs-lookup"><span data-stu-id="6fc48-147">You can see a .NET example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="6fc48-148">建立使用 hello 金鑰識別碼和內容金鑰計算的總和檢查碼值。</span><span class="sxs-lookup"><span data-stu-id="6fc48-148">Create a checksum value calculated using hello key identifier and content key.</span></span> <span data-ttu-id="6fc48-149">下列.NET 範例 hello 計算使用 hello 金鑰識別碼 hello GUID 部分 hello 總和檢查碼，並 hello 清除內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="6fc48-149">hello following .NET example calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. <span data-ttu-id="6fc48-150">建立 hello 內容金鑰以 hello **EncryptedContentKey** （轉換 toobase64 編碼的字串） **ProtectionKeyId**， **ProtectionKeyType**， **ContentKeyType**，和**總和檢查碼**您在先前步驟中收到的值。</span><span class="sxs-lookup"><span data-stu-id="6fc48-150">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="6fc48-151">儲存體加密 hello 下列屬性應該包含 hello 要求主體中。</span><span class="sxs-lookup"><span data-stu-id="6fc48-151">For storage encryption, hello following properties should be included in hello request body.</span></span>

    <span data-ttu-id="6fc48-152">要求本文屬性</span><span class="sxs-lookup"><span data-stu-id="6fc48-152">Request body property</span></span>    | <span data-ttu-id="6fc48-153">說明</span><span class="sxs-lookup"><span data-stu-id="6fc48-153">Description</span></span>
    ---|---
    <span data-ttu-id="6fc48-154">識別碼</span><span class="sxs-lookup"><span data-stu-id="6fc48-154">Id</span></span> | <span data-ttu-id="6fc48-155">hello 我們所產生的 ContentKey 識別碼自己使用 hello 下列格式，"nb:<NEW GUID>"。</span><span class="sxs-lookup"><span data-stu-id="6fc48-155">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="6fc48-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="6fc48-156">ContentKeyType</span></span> | <span data-ttu-id="6fc48-157">這是 hello 內容金鑰類型為此內容金鑰的整數。</span><span class="sxs-lookup"><span data-stu-id="6fc48-157">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="6fc48-158">我們傳遞儲存體加密的 hello 值 1。</span><span class="sxs-lookup"><span data-stu-id="6fc48-158">We pass hello value 1 for storage encryption.</span></span>
    <span data-ttu-id="6fc48-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="6fc48-159">EncryptedContentKey</span></span> | <span data-ttu-id="6fc48-160">我們會建立新的內容金鑰值，其為 256 位元 (32 位元組) 的值。</span><span class="sxs-lookup"><span data-stu-id="6fc48-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="6fc48-161">使用 hello 儲存加密 X.509 憑證執行 hello GetProtectionKeyId 與 GetProtectionKey 方法的 HTTP GET 要求來擷取從 Microsoft Azure Media Services，hello 金鑰進行加密。</span><span class="sxs-lookup"><span data-stu-id="6fc48-161">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="6fc48-162">例如，請參閱下列.NET 程式碼的 hello: hello **EncryptSymmetricKeyData**方法定義[這裡](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)。</span><span class="sxs-lookup"><span data-stu-id="6fc48-162">As an example, see hello following .NET code: hello  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="6fc48-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="6fc48-163">ProtectionKeyId</span></span> | <span data-ttu-id="6fc48-164">這是我們的內容金鑰 hello hello 儲存加密 X.509 憑證的已使用的 tooencrypt 保護金鑰識別碼。</span><span class="sxs-lookup"><span data-stu-id="6fc48-164">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span>
    <span data-ttu-id="6fc48-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="6fc48-165">ProtectionKeyType</span></span> | <span data-ttu-id="6fc48-166">這是 hello hello 已使用的 tooencrypt hello 內容金鑰的保護金鑰的加密類型。</span><span class="sxs-lookup"><span data-stu-id="6fc48-166">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="6fc48-167">針對本文範例，此值為 StorageEncryption(1)。</span><span class="sxs-lookup"><span data-stu-id="6fc48-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="6fc48-168">Checksum</span><span class="sxs-lookup"><span data-stu-id="6fc48-168">Checksum</span></span> |<span data-ttu-id="6fc48-169">hello MD5 計算總和檢查碼 hello 內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="6fc48-169">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="6fc48-170">會透過加密 hello 內容金鑰的 hello 內容識別碼，以執行計算。</span><span class="sxs-lookup"><span data-stu-id="6fc48-170">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="6fc48-171">hello 範例程式碼會示範如何 toocalculate hello 總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="6fc48-171">hello example code demonstrates how toocalculate hello checksum.</span></span>


### <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="6fc48-172">擷取 ProtectionKeyId hello</span><span class="sxs-lookup"><span data-stu-id="6fc48-172">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="6fc48-173">hello 下列範例顯示如何 tooretrieve hello 的 hello 憑證內容金鑰加密時，您必須使用的憑證指紋 ProtectionKeyId。</span><span class="sxs-lookup"><span data-stu-id="6fc48-173">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="6fc48-174">執行這個步驟 toomake 確定您的電腦上已經有 hello 適當的憑證。</span><span class="sxs-lookup"><span data-stu-id="6fc48-174">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="6fc48-175">要求：</span><span class="sxs-lookup"><span data-stu-id="6fc48-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="6fc48-176">回應：</span><span class="sxs-lookup"><span data-stu-id="6fc48-176">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="6fc48-177">擷取 ProtectionKeyId hello ProtectionKey</span><span class="sxs-lookup"><span data-stu-id="6fc48-177">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="6fc48-178">hello 下列範例示範如何使用 hello ProtectionKeyId tooretrieve hello X.509 憑證中收到 hello 上一個步驟。</span><span class="sxs-lookup"><span data-stu-id="6fc48-178">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="6fc48-179">要求：</span><span class="sxs-lookup"><span data-stu-id="6fc48-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="6fc48-180">回應：</span><span class="sxs-lookup"><span data-stu-id="6fc48-180">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a><span data-ttu-id="6fc48-181">建立 hello 內容金鑰</span><span class="sxs-lookup"><span data-stu-id="6fc48-181">Create hello content key</span></span>
<span data-ttu-id="6fc48-182">您有擷取 hello X.509 憑證，並使用其公用金鑰 tooencrypt 將內容金鑰之後，建立**ContentKey**實體和其屬性值，據此設定。</span><span class="sxs-lookup"><span data-stu-id="6fc48-182">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="6fc48-183">其中一個 hello 值，您必須設定時建立 hello 內容金鑰是 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="6fc48-183">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="6fc48-184">發生 hello 儲存體加密，hello 值為 '1'。</span><span class="sxs-lookup"><span data-stu-id="6fc48-184">In case of hello storage encryption, hello value is '1'.</span></span> 

<span data-ttu-id="6fc48-185">下列範例會示範如何 hello toocreate **ContentKey**與**ContentKeyType**設定儲存體加密 ("1") 和 hello **ProtectionKeyType**設定太"0 的"hello 保護金鑰識別碼的 tooindicate 是 hello X.509 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="6fc48-185">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="6fc48-186">要求</span><span class="sxs-lookup"><span data-stu-id="6fc48-186">Request</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

<span data-ttu-id="6fc48-187">回應：</span><span class="sxs-lookup"><span data-stu-id="6fc48-187">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a><span data-ttu-id="6fc48-188">建立資產</span><span class="sxs-lookup"><span data-stu-id="6fc48-188">Create an asset</span></span>
<span data-ttu-id="6fc48-189">下列範例會示範如何 hello toocreate 資產。</span><span class="sxs-lookup"><span data-stu-id="6fc48-189">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="6fc48-190">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="6fc48-190">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

<span data-ttu-id="6fc48-191">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="6fc48-191">**HTTP Response**</span></span>

<span data-ttu-id="6fc48-192">如果成功，則會傳回 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="6fc48-192">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="6fc48-193">將 hello ContentKey 與資產產生關聯</span><span class="sxs-lookup"><span data-stu-id="6fc48-193">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="6fc48-194">建立 hello ContentKey 之後, 將它與關聯使用 hello $links 作業在資產中 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6fc48-194">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="6fc48-195">要求：</span><span class="sxs-lookup"><span data-stu-id="6fc48-195">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

<span data-ttu-id="6fc48-196">回應：</span><span class="sxs-lookup"><span data-stu-id="6fc48-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="6fc48-197">建立 AssetFile</span><span class="sxs-lookup"><span data-stu-id="6fc48-197">Create an AssetFile</span></span>
<span data-ttu-id="6fc48-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile)實體代表儲存在 blob 容器的視訊或音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="6fc48-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="6fc48-199">資產檔案一律會與資產相關聯，而資產可包含一或多個資產檔案。</span><span class="sxs-lookup"><span data-stu-id="6fc48-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="6fc48-200">如果資產檔案物件不是 blob 容器中的數位檔案相關聯，hello Media Services 編碼器工作會失敗。</span><span class="sxs-lookup"><span data-stu-id="6fc48-200">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="6fc48-201">請注意該 hello **AssetFile**執行個體與 hello 實際媒體檔案的兩個相異的物件。</span><span class="sxs-lookup"><span data-stu-id="6fc48-201">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="6fc48-202">hello AssetFile 執行個體包含 hello 媒體檔案的相關中繼資料，而 hello 媒體檔案包含 hello 實際的媒體內容。</span><span class="sxs-lookup"><span data-stu-id="6fc48-202">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="6fc48-203">您將數位媒體檔案上傳到 blob 容器之後，您將使用 hello**合併**HTTP 要求 tooupdate hello AssetFile （本主題中未顯示） 您的媒體檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6fc48-203">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="6fc48-204">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="6fc48-204">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="6fc48-205">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="6fc48-205">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
