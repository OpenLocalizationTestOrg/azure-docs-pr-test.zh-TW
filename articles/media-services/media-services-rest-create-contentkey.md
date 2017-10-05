---
title: "使用 REST 建立內容金鑰 | Microsoft Docs"
description: "了解如何建立提供資產安全存取的內容金鑰。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95e9322b-168e-4a9d-8d5d-d7c946103745
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: ece09277d26fafb7c0eebf62730031c4dc01bfe0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-content-keys-with-rest"></a><span data-ttu-id="ea7d4-103">使用 REST 建立內容金鑰</span><span class="sxs-lookup"><span data-stu-id="ea7d4-103">Create content keys with REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea7d4-104">REST</span><span class="sxs-lookup"><span data-stu-id="ea7d4-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="ea7d4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ea7d4-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="ea7d4-106">媒體服務可讓您建立新的資產及傳遞已加密的資產。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-106">Media Services enables you to create new and deliver encrypted assets.</span></span> <span data-ttu-id="ea7d4-107">**ContentKey** 提供**資產**的安全存取。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="ea7d4-108">當您建立新的資產時 (例如，[將檔案上傳](media-services-rest-upload-files.md)之前)，您可以指定下列加密選項：**StorageEncrypted**、**CommonEncryptionProtected** 或 **EnvelopeEncryptionProtected**。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-108">When you create a new asset (for example, before you [upload files](media-services-rest-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="ea7d4-109">當您將資產傳遞至您的用戶端時，您可以使用下列兩個加密的其中一個[設定動態加密的資產](media-services-rest-configure-asset-delivery-policy.md)：**DynamicEnvelopeEncryption** 或 **DynamicCommonEncryption**。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-rest-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="ea7d4-110">加密的資產必須與 **ContentKey**相關聯。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="ea7d4-111">本文說明如何建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-111">This article describes how to create a content key.</span></span>

<span data-ttu-id="ea7d4-112">以下是產生您將與要加密資產相關聯的內容金鑰的一般步驟。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-112">The following are general steps for generating content keys that you will associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="ea7d4-113">隨機產生 16 位元組 AES 金鑰 (適用於一般加密以及信封加密) 或 32 位元組 AES 金鑰 (適用於儲存體加密)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-113">Randomly generate a 16-byte AES key (for common and envelope encryption) or a 32-byte AES key (for storage encryption).</span></span> 
   
    <span data-ttu-id="ea7d4-114">這是您資產的內容金鑰，這表示與該資產相關聯的所有檔案都必須在解密期間使用相同的內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-114">This will be the content key for your asset, which means all files associated with that asset will need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="ea7d4-115">呼叫 [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) 和 [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) 方法，以取得用來將內容金鑰加密時必須使用的正確 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-115">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="ea7d4-116">使用 X.509 憑證的公開金鑰將您的內容金鑰加密。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-116">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="ea7d4-117">媒體服務 .NET SDK 會使用 RSA 和 OAEP 來執行加密作業。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-117">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="ea7d4-118">您可以在 [EncryptSymmetricKeyData 函式](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)中查看範例。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-118">You can see an example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="ea7d4-119">建立使用金鑰識別碼和內容金鑰計算的總和檢查碼值 (根據 PlayReady AES 金鑰總和檢查碼演算法)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-119">Create a checksum value (based on the PlayReady AES key checksum algorithm) calculated using the key identifier and content key.</span></span> <span data-ttu-id="ea7d4-120">如需詳細資訊，請參閱位於 [這裡](http://www.microsoft.com/playready/documents/)的 PlayReady 標頭物件文件的＜PlayReady AES 金鑰總和檢查碼演算法＞一節。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-120">For more information, see the “PlayReady AES Key Checksum Algorithm” section of the PlayReady Header Object document located [here](http://www.microsoft.com/playready/documents/).</span></span>
   
   <span data-ttu-id="ea7d4-121">下列 .NET 範例會使用金鑰識別碼和明文內容金鑰的 GUID 部分計算總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-121">The following is a .NET example that calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

         public static string CalculateChecksum(byte[] contentKey, Guid keyId)
         {

            byte[] array = null;
            using (AesCryptoServiceProvider aesCryptoServiceProvider = new AesCryptoServiceProvider())
            {
                aesCryptoServiceProvider.Mode = CipherMode.ECB;
                aesCryptoServiceProvider.Key = contentKey;
                aesCryptoServiceProvider.Padding = PaddingMode.None;
                ICryptoTransform cryptoTransform = aesCryptoServiceProvider.CreateEncryptor();
                array = new byte[16];
                cryptoTransform.TransformBlock(keyId.ToByteArray(), 0, 16, array, 0);
            }
            byte[] array2 = new byte[8];
            Array.Copy(array, array2, 8);
            return Convert.ToBase64String(array2);
         }
5. <span data-ttu-id="ea7d4-122">用您在先前步驟中收到的 **EncryptedContentKey** (轉換為 base64 編碼的字串)、**ProtectionKeyId**、**ProtectionKeyType**、**ContentKeyType** 和 **Checksum** 值建立內容金鑰。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-122">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>
6. <span data-ttu-id="ea7d4-123">透過 $links 作業建立 **ContentKey** 實體與您 **Asset** 實體的關聯。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-123">Associate the **ContentKey** entity with your **Asset** entity through the $links operation.</span></span>

<span data-ttu-id="ea7d4-124">請注意，本主題不會示範如何產生 AES 金鑰、加密金鑰，以及計算總和檢查碼。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-124">Note that this topic does not show how to generate an AES key, encrypt the key, and calculate the checksum.</span></span> 

>[!NOTE]

><span data-ttu-id="ea7d4-125">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-125">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ea7d4-126">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-126">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="ea7d4-127">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="ea7d4-127">Connect to Media Services</span></span>

<span data-ttu-id="ea7d4-128">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-128">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ea7d4-129">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-129">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ea7d4-130">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-130">You must make subsequent calls to the new URI.</span></span>

## <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="ea7d4-131">擷取 ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="ea7d4-131">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="ea7d4-132">下列範例示範如何為加密內容金鑰時您必須使用的憑證擷取 ProtectionKeyId (憑證指紋)。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-132">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="ea7d4-133">執行此步驟，以確定您的電腦上已經有適當的憑證。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-133">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="ea7d4-134">要求：</span><span class="sxs-lookup"><span data-stu-id="ea7d4-134">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net


<span data-ttu-id="ea7d4-135">回應：</span><span class="sxs-lookup"><span data-stu-id="ea7d4-135">Response:</span></span>

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

## <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="ea7d4-136">擷取 ProtectionKeyId 的 ProtectionKey</span><span class="sxs-lookup"><span data-stu-id="ea7d4-136">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="ea7d4-137">下列範例顯示如何使用您在上一個步驟中收到的 ProtectionKeyId 擷取 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-137">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="ea7d4-138">要求：</span><span class="sxs-lookup"><span data-stu-id="ea7d4-138">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net



<span data-ttu-id="ea7d4-139">回應：</span><span class="sxs-lookup"><span data-stu-id="ea7d4-139">Response:</span></span>

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

## <a name="create-the-contentkey"></a><span data-ttu-id="ea7d4-140">建立 ContentKey</span><span class="sxs-lookup"><span data-stu-id="ea7d4-140">Create the ContentKey</span></span>
<span data-ttu-id="ea7d4-141">在擷取 X.509 憑證並使用其公開金鑰將內容金鑰加密之後，建立 **ContentKey** 實體並據以設定其屬性值。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-141">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="ea7d4-142">建立內容金鑰時必須設定的其中一個值是類型。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-142">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="ea7d4-143">選擇下列值之一。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-143">Choose from one of the following values.</span></span>

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }


<span data-ttu-id="ea7d4-144">下列範例示範如何建立 **ContentKey** 且針對儲存體加密設定 **ContentKeyType** ("1")，**ProtectionKeyType** 則設定為 "0"，表示保護金鑰識別碼是 X.509 憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="ea7d4-144">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key Id is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="ea7d4-145">要求</span><span class="sxs-lookup"><span data-stu-id="ea7d4-145">Request</span></span>

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


<span data-ttu-id="ea7d4-146">回應：</span><span class="sxs-lookup"><span data-stu-id="ea7d4-146">Response:</span></span>

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

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="ea7d4-147">將 ContentKey 與資產產生關聯</span><span class="sxs-lookup"><span data-stu-id="ea7d4-147">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="ea7d4-148">建立 ContentKey 之後, ，使用 $links 作業將其與資產產生關聯，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ea7d4-148">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="ea7d4-149">要求：</span><span class="sxs-lookup"><span data-stu-id="ea7d4-149">Request:</span></span>

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

<span data-ttu-id="ea7d4-150">回應：</span><span class="sxs-lookup"><span data-stu-id="ea7d4-150">Response:</span></span>

    HTTP/1.1 204 No Content 


## <a name="media-services-learning-paths"></a><span data-ttu-id="ea7d4-151">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="ea7d4-151">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ea7d4-152">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="ea7d4-152">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

