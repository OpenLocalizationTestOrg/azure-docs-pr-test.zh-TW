---
title: "使用 AMS REST API 以儲存體加密來加密您的內容"
description: "了解如何使用 AMS REST API 以儲存體加密來加密您的內容。"
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
ms.openlocfilehash: 1979f5bf5e8cab88dab5fba49018afacf24504b3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="59f14-103">以儲存體加密來加密您的內容</span><span class="sxs-lookup"><span data-stu-id="59f14-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="59f14-104">高度建議使用 AES-256 位元加密對您的內容進行本機加密，然後將其上傳到將靜止加密儲存的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="59f14-104">It is highly recommended to encrypt your content locally using AES-256 bit encryption and then upload it to Azure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="59f14-105">本文概述 AMS 儲存體加密，並說明如何上傳儲存體加密內容︰</span><span class="sxs-lookup"><span data-stu-id="59f14-105">This article gives an overview of AMS storage encryption and shows you how to upload the storage encrypted content:</span></span>

* <span data-ttu-id="59f14-106">建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="59f14-106">Create a content key.</span></span>
* <span data-ttu-id="59f14-107">建立資產。</span><span class="sxs-lookup"><span data-stu-id="59f14-107">Create an Asset.</span></span> <span data-ttu-id="59f14-108">建立資產時，請將 AssetCreationOption 設為 StorageEncryption。</span><span class="sxs-lookup"><span data-stu-id="59f14-108">Set the AssetCreationOption to StorageEncryption when creating the Asset.</span></span>
  
     <span data-ttu-id="59f14-109">加密的資產必須與內容金鑰相關聯。</span><span class="sxs-lookup"><span data-stu-id="59f14-109">Encrypted assets have to be associated with content keys.</span></span>
* <span data-ttu-id="59f14-110">將內容金鑰連結到資產。</span><span class="sxs-lookup"><span data-stu-id="59f14-110">Link the content key to the asset.</span></span>  
* <span data-ttu-id="59f14-111">在 AssetFile 實體上設定加密相關的參數。</span><span class="sxs-lookup"><span data-stu-id="59f14-111">Set the encryption related parameters on the AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="59f14-112">考量</span><span class="sxs-lookup"><span data-stu-id="59f14-112">Considerations</span></span> 

<span data-ttu-id="59f14-113">如果您想要傳遞儲存體加密資產，就必須設定資產的傳遞原則。</span><span class="sxs-lookup"><span data-stu-id="59f14-113">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="59f14-114">資產可以串流處理之前，串流伺服器會移除儲存體加密，並使用指定的傳遞原則來串流您的內容。</span><span class="sxs-lookup"><span data-stu-id="59f14-114">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="59f14-115">如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-rest-configure-asset-delivery-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="59f14-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="59f14-116">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="59f14-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="59f14-117">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="59f14-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-to-media-services"></a><span data-ttu-id="59f14-118">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="59f14-118">Connect to Media Services</span></span>

<span data-ttu-id="59f14-119">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="59f14-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="59f14-120">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="59f14-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="59f14-121">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="59f14-121">You must make subsequent calls to the new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="59f14-122">儲存體加密概觀</span><span class="sxs-lookup"><span data-stu-id="59f14-122">Storage encryption overview</span></span>
<span data-ttu-id="59f14-123">AMS 儲存體加密會將 **AES-CTR** 模式加密套用至整個檔案。</span><span class="sxs-lookup"><span data-stu-id="59f14-123">The AMS storage encryption applies **AES-CTR** mode encryption to the entire file.</span></span>  <span data-ttu-id="59f14-124">AES CTR 模式是可加密任意長度資料且不需填補的區塊編碼器。</span><span class="sxs-lookup"><span data-stu-id="59f14-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="59f14-125">其作業方式是使用 AES 演算法加密計數器區塊，並且對要加密或解密資料的 AES 輸出進行 XOR 處理。</span><span class="sxs-lookup"><span data-stu-id="59f14-125">It operates by encrypting a counter block with the AES algorithm and then XOR-ing the output of AES with the data to encrypt or decrypt.</span></span>  <span data-ttu-id="59f14-126">所使用計數器區塊的建構方式是將 InitializationVector 的值複製到計數器值的位元組 0 到 7，而且計數器值的位元組 8 到 15 設定為零。</span><span class="sxs-lookup"><span data-stu-id="59f14-126">The counter block used is constructed by copying the value of the InitializationVector to bytes 0 to 7 of the counter value and bytes 8 to 15 of the counter value are set to zero.</span></span> <span data-ttu-id="59f14-127">在 16 位元組的計數器區塊中，位元組 8 到 15 (即最低位元組) 是用作簡單 64 位元不帶正負號的整數，而且每個後續處理的資料區塊都會加一，並會保持網路位元組順序。</span><span class="sxs-lookup"><span data-stu-id="59f14-127">Of the 16 byte counter block, bytes 8 to 15 (i.e. the least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="59f14-128">請注意，如果此整數達到最大值 (0xFFFFFFFFFFFFFFFF)，則增加它時會將區塊計數器重設為零 (位元組 8 到 15)，而不影響計數器的其他 64 位元 (即位元組 0 到 7)。</span><span class="sxs-lookup"><span data-stu-id="59f14-128">Note that if this integer reaches the maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets the block counter to zero (bytes 8 to 15) without affecting the other 64 bits of the counter (i.e. bytes 0 to 7).</span></span>   <span data-ttu-id="59f14-129">為了維護 AES CTR 模式加密的安全性，對每個檔案而言，每個內容金鑰的指定金鑰識別碼應該為唯一，而且檔案的長度應該小於 2^64 個區塊。</span><span class="sxs-lookup"><span data-stu-id="59f14-129">In order to maintain the security of the AES-CTR mode encryption, the InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="59f14-130">這是為了確保計數器值絕不會與指定的索引鍵重複使用。</span><span class="sxs-lookup"><span data-stu-id="59f14-130">This is to ensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="59f14-131">如需 CTR 模式的詳細資訊，請參閱 [此 Wiki 頁面](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (Wiki 文章使用 "Nonce" 這個字，而非 "InitializationVector")。</span><span class="sxs-lookup"><span data-stu-id="59f14-131">For more information about the CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (the wiki article uses the term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="59f14-132">使用 **儲存體加密** ，使用 AES-256 位元加密對您的純文字內容進行本機加密，然後將其上傳到已靜止加密儲存的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="59f14-132">Use **Storage Encryption** to encrypt your clear content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="59f14-133">使用儲存體加密保護的資產會在編碼之前自動解除加密並放在加密的檔案系統中，並且選擇性地在上傳為新的輸出資產之前重新加密。</span><span class="sxs-lookup"><span data-stu-id="59f14-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="59f14-134">儲存體加密的主要使用案例是當您想要使用強式加密保護靜止在磁碟上的高品質輸入媒體檔案時。</span><span class="sxs-lookup"><span data-stu-id="59f14-134">The primary use case for storage encryption is when you want to secure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="59f14-135">若要傳遞儲存體加密資產，您必須設定資產的傳遞原則，讓媒體服務知道您的內容傳遞方式。</span><span class="sxs-lookup"><span data-stu-id="59f14-135">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="59f14-136">串流處理資產之前，串流伺服器會移除儲存體加密，並使用指定的傳遞原則來串流處理您的內容 (例如，AES、一般加密或不加密)。</span><span class="sxs-lookup"><span data-stu-id="59f14-136">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="59f14-137">建立要用於加密的 ContentKey</span><span class="sxs-lookup"><span data-stu-id="59f14-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="59f14-138">加密的資產必須與儲存體加密金鑰相關聯。</span><span class="sxs-lookup"><span data-stu-id="59f14-138">Encrypted assets have to be associated with Storage Encryption key.</span></span> <span data-ttu-id="59f14-139">您必須先建立要用於加密的內容金鑰，再建立資產檔案。</span><span class="sxs-lookup"><span data-stu-id="59f14-139">You must create the content key to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="59f14-140">本節說明如何建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="59f14-140">This section describes how to create a content key.</span></span>

<span data-ttu-id="59f14-141">以下是產生您將與要加密資產相關聯的內容金鑰的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="59f14-141">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="59f14-142">對於儲存體加密，請隨機產生 32 個位元組的 AES 金鑰。</span><span class="sxs-lookup"><span data-stu-id="59f14-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="59f14-143">這是您資產的內容金鑰，這表示與該資產相關聯的所有檔案都必須在解密期間使用相同的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="59f14-143">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="59f14-144">呼叫 [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) 和 [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) 方法，以取得用來將內容金鑰加密時必須使用的正確 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="59f14-144">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="59f14-145">使用 X.509 憑證的公開金鑰將您的內容金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="59f14-145">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="59f14-146">媒體服務 .NET SDK 會使用 RSA 和 OAEP 來執行加密作業。</span><span class="sxs-lookup"><span data-stu-id="59f14-146">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="59f14-147">您可以在 [EncryptSymmetricKeyData 函式](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)中查看 .NET 範例。</span><span class="sxs-lookup"><span data-stu-id="59f14-147">You can see a .NET example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="59f14-148">建立使用金鑰識別碼和內容金鑰計算的總和檢查碼值。</span><span class="sxs-lookup"><span data-stu-id="59f14-148">Create a checksum value calculated using the key identifier and content key.</span></span> <span data-ttu-id="59f14-149">下列 .NET 範例會使用金鑰識別碼和明文內容金鑰的 GUID 部分計算總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="59f14-149">The following .NET example calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting the KID
            // with the content key.
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

1. <span data-ttu-id="59f14-150">用您在先前步驟中收到的 **EncryptedContentKey** (轉換為 base64 編碼的字串)、**ProtectionKeyId**、**ProtectionKeyType**、**ContentKeyType** 和 **Checksum** 值建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="59f14-150">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="59f14-151">對於儲存體加密，要求本文中應該包含下列屬性。</span><span class="sxs-lookup"><span data-stu-id="59f14-151">For storage encryption, the following properties should be included in the request body.</span></span>

    <span data-ttu-id="59f14-152">要求本文屬性</span><span class="sxs-lookup"><span data-stu-id="59f14-152">Request body property</span></span>    | <span data-ttu-id="59f14-153">說明</span><span class="sxs-lookup"><span data-stu-id="59f14-153">Description</span></span>
    ---|---
    <span data-ttu-id="59f14-154">識別碼</span><span class="sxs-lookup"><span data-stu-id="59f14-154">Id</span></span> | <span data-ttu-id="59f14-155">我們使用下列格式自行產生的 ContentKey 識別碼："nb:kid:UUID:<NEW GUID>"。</span><span class="sxs-lookup"><span data-stu-id="59f14-155">The ContentKey Id which we generate ourselves using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="59f14-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="59f14-156">ContentKeyType</span></span> | <span data-ttu-id="59f14-157">這是針對此內容金鑰以整數表示的內容金鑰類型。</span><span class="sxs-lookup"><span data-stu-id="59f14-157">This is the content key type as an integer for this content key.</span></span> <span data-ttu-id="59f14-158">我們會傳遞值 1 來進行儲存體加密。</span><span class="sxs-lookup"><span data-stu-id="59f14-158">We pass the value 1 for storage encryption.</span></span>
    <span data-ttu-id="59f14-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="59f14-159">EncryptedContentKey</span></span> | <span data-ttu-id="59f14-160">我們會建立新的內容金鑰值，其為 256 位元 (32 位元組) 的值。</span><span class="sxs-lookup"><span data-stu-id="59f14-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="59f14-161">此金鑰是藉由針對 GetProtectionKeyId 與 GetProtectionKey 方法執行 HTTP GET 要求，使用我們從 Microsoft Azure 媒體服務擷取的儲存體加密 X.509 憑證來加密的。</span><span class="sxs-lookup"><span data-stu-id="59f14-161">The key is encrypted using the storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="59f14-162">範例請參閱下列 .NET 程式碼︰[這裡](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)定義的 **EncryptSymmetricKeyData**方法。</span><span class="sxs-lookup"><span data-stu-id="59f14-162">As an example, see the following .NET code: the  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="59f14-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="59f14-163">ProtectionKeyId</span></span> | <span data-ttu-id="59f14-164">這是適用於儲存體加密 X.509 憑證的保護金鑰識別碼，可用來加密我們的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="59f14-164">This is the protection key id for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span>
    <span data-ttu-id="59f14-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="59f14-165">ProtectionKeyType</span></span> | <span data-ttu-id="59f14-166">這是適用於保護金鑰的加密類型，可用來將內容金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="59f14-166">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="59f14-167">針對本文範例，此值為 StorageEncryption(1)。</span><span class="sxs-lookup"><span data-stu-id="59f14-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="59f14-168">Checksum</span><span class="sxs-lookup"><span data-stu-id="59f14-168">Checksum</span></span> |<span data-ttu-id="59f14-169">MD5 會針對內容金鑰計算出總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="59f14-169">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="59f14-170">它是使用內容金鑰來將內容識別碼加密計算而得的。</span><span class="sxs-lookup"><span data-stu-id="59f14-170">It is computed by encrypting the content Id with the content key.</span></span> <span data-ttu-id="59f14-171">範例程式碼示範如何計算總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="59f14-171">The example code demonstrates how to calculate the checksum.</span></span>


### <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="59f14-172">擷取 ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="59f14-172">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="59f14-173">下列範例示範如何為加密內容金鑰時您必須使用的憑證擷取 ProtectionKeyId (憑證指紋)。</span><span class="sxs-lookup"><span data-stu-id="59f14-173">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="59f14-174">執行此步驟，以確定您的電腦上已經有適當的憑證。</span><span class="sxs-lookup"><span data-stu-id="59f14-174">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="59f14-175">要求：</span><span class="sxs-lookup"><span data-stu-id="59f14-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="59f14-176">回應：</span><span class="sxs-lookup"><span data-stu-id="59f14-176">Response:</span></span>

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

### <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="59f14-177">擷取 ProtectionKeyId 的 ProtectionKey</span><span class="sxs-lookup"><span data-stu-id="59f14-177">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="59f14-178">下列範例顯示如何使用您在上一個步驟中收到的 ProtectionKeyId 擷取 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="59f14-178">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="59f14-179">要求：</span><span class="sxs-lookup"><span data-stu-id="59f14-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="59f14-180">回應：</span><span class="sxs-lookup"><span data-stu-id="59f14-180">Response:</span></span>

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

### <a name="create-the-content-key"></a><span data-ttu-id="59f14-181">建立內容金鑰</span><span class="sxs-lookup"><span data-stu-id="59f14-181">Create the content key</span></span>
<span data-ttu-id="59f14-182">在擷取 X.509 憑證並使用其公開金鑰將內容金鑰加密之後，建立 **ContentKey** 實體並據以設定其屬性值。</span><span class="sxs-lookup"><span data-stu-id="59f14-182">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="59f14-183">建立內容金鑰時必須設定的其中一個值是類型。</span><span class="sxs-lookup"><span data-stu-id="59f14-183">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="59f14-184">若為儲存體加密，值會是 '1'。</span><span class="sxs-lookup"><span data-stu-id="59f14-184">In case of the storage encryption, the value is '1'.</span></span> 

<span data-ttu-id="59f14-185">下列範例示範如何建立 **ContentKey** 且針對儲存體加密設定 **ContentKeyType** ("1")，**ProtectionKeyType** 則設定為 "0"，表示保護金鑰識別碼是 X.509 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="59f14-185">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="59f14-186">要求</span><span class="sxs-lookup"><span data-stu-id="59f14-186">Request</span></span>

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

<span data-ttu-id="59f14-187">回應：</span><span class="sxs-lookup"><span data-stu-id="59f14-187">Response:</span></span>

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

## <a name="create-an-asset"></a><span data-ttu-id="59f14-188">建立資產</span><span class="sxs-lookup"><span data-stu-id="59f14-188">Create an asset</span></span>
<span data-ttu-id="59f14-189">下列範例示範如何建立資產。</span><span class="sxs-lookup"><span data-stu-id="59f14-189">The following example shows how to create an asset.</span></span>

<span data-ttu-id="59f14-190">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="59f14-190">**HTTP Request**</span></span>

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

<span data-ttu-id="59f14-191">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="59f14-191">**HTTP Response**</span></span>

<span data-ttu-id="59f14-192">如果成功，則會傳回下列內容：</span><span class="sxs-lookup"><span data-stu-id="59f14-192">If successful, the following is returned:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="59f14-193">將 ContentKey 與資產產生關聯</span><span class="sxs-lookup"><span data-stu-id="59f14-193">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="59f14-194">建立 ContentKey 之後, ，使用 $links 作業將其與資產產生關聯，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="59f14-194">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="59f14-195">要求：</span><span class="sxs-lookup"><span data-stu-id="59f14-195">Request:</span></span>

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

<span data-ttu-id="59f14-196">回應：</span><span class="sxs-lookup"><span data-stu-id="59f14-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="59f14-197">建立 AssetFile</span><span class="sxs-lookup"><span data-stu-id="59f14-197">Create an AssetFile</span></span>
<span data-ttu-id="59f14-198">[AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) 實體代表儲存在 blob 容器中的視訊或音訊檔案。</span><span class="sxs-lookup"><span data-stu-id="59f14-198">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="59f14-199">資產檔案一律會與資產相關聯，而資產可包含一或多個資產檔案。</span><span class="sxs-lookup"><span data-stu-id="59f14-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="59f14-200">如果資產檔案物件並未與 blob 容器中的數位檔案相關聯，媒體服務編碼器工作將會失敗。</span><span class="sxs-lookup"><span data-stu-id="59f14-200">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="59f14-201">請注意， **AssetFile** 執行個體和實際的媒體檔案是兩個不同的物件。</span><span class="sxs-lookup"><span data-stu-id="59f14-201">Note that the **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="59f14-202">AssetFile 執行個體包含媒體檔案的相關中繼資料，而媒體檔案包含實際的媒體內容。</span><span class="sxs-lookup"><span data-stu-id="59f14-202">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="59f14-203">當您將數位媒體檔案上傳至 Blob 容器之後，您將使用 **MERGE** HTTP 要求，以媒體檔案的相關資訊來更新 AssetFile (未顯示在本主題中)。</span><span class="sxs-lookup"><span data-stu-id="59f14-203">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="59f14-204">**HTTP 要求**</span><span class="sxs-lookup"><span data-stu-id="59f14-204">**HTTP Request**</span></span>

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

<span data-ttu-id="59f14-205">**HTTP 回應**</span><span class="sxs-lookup"><span data-stu-id="59f14-205">**HTTP Response**</span></span>

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