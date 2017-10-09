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
# <a name="encrypting-your-content-with-storage-encryption"></a>以儲存體加密來加密您的內容

強烈建議 tooencrypt 您使用 AES 256 在本機的內容位元加密，然後將它上傳 tooAzure 儲存體的位置儲存加密在靜止。

這篇文章提供 AMS 儲存體加密的概觀，並顯示您 tooupload hello 儲存體加密內容的方式：

* 建立內容金鑰。
* 建立資產。 建立 hello 資產時，請設定 hello AssetCreationOption tooStorageEncryption。
  
     加密的資產有 toobe 內容金鑰相關聯。
* 連結 hello 內容金鑰 toohello 資產。  
* 設定 hello 加密相關 hello AssetFile 實體上的參數。

## <a name="considerations"></a>考量 

如果您想 toodeliver 儲存體加密資產時，您必須設定 hello 資產的傳遞原則。 在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則。 如需詳細資訊，請參閱 [設定資產傳遞原則](media-services-rest-configure-asset-delivery-policy.md)。

在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。 如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。 

## <a name="connect-toomedia-services"></a>TooMedia 服務連接

如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。 

>[!NOTE]
>已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。

## <a name="storage-encryption-overview"></a>儲存體加密概觀
適用於 hello AMS 儲存體加密**AES CTR**模式加密 toohello 整個檔案。  AES CTR 模式是可加密任意長度資料且不需填補的區塊編碼器。 它的運作方式與 hello AES 演算法，然後 XOR ing hello 輸出的 AES hello 資料 tooencrypt 計數器區塊的加密或解密。  hello 計數器區塊由建構 hello hello InitializationVector toobytes 0 too7 hello 計數器值的值複製，hello 計數器值的 8 位元組 too15 設定 toozero。 Hello 16 位元組計數器區塊，too15 8 個位元組的可用如同簡單的 64 位元不帶正負號的整數，都會加一的每個後續區塊處理的資料保存在網路位元組順序 （也就是 hello 最小顯著性位元組為單位）。 請注意，如果此整數達到 hello 最大值 (0xFFFFFFFFFFFFFFFF) 再增加其重設 hello 區塊計數器 toozero (8 位元組 too15) 而不會影響其他 hello hello 計數器 (也就是 0 位元組 too7) 的 64 位元。   順序 toomaintain hello hello AES CTR 模式加密的安全性、 hello InitializationVector 值指定的索引鍵識別項的每個內容的索引鍵應該是唯一的每個檔案和檔案都必須小於 2 ^64 區塊的長度。  這是 tooensure 計數器值絕不會是可重複使用指定的索引鍵。 如需 hello CTR 模式的詳細資訊，請參閱[wiki 本頁](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR)（hello wiki 文章使用 hello 詞彙"Nonce"，而不是"InitializationVector"）。

使用**儲存體加密**tooencrypt 您清除的內容，在本機使用 AES 256 位元加密並再將它上傳 tooAzure 儲存體的方式予以儲存加密在靜止。 使用儲存體加密保護的資產會自動加密，並在 「 加密的檔案系統先前 tooencoding，及選擇性地重新加密的先前 toouploading 回為新輸出資產。 儲存體加密的 hello 主要使用案例是當您想的 toosecure 強式加密您高品質的輸入的媒體檔案放在磁碟。

在順序 toodeliver 儲存體加密資產，您必須設定 hello 資產的傳遞原則，讓媒體服務知道要如何 toodeliver 您的內容。 在您的資產進行串流處理之前，請使用 hello 將內容串流伺服器移除 hello 儲存體加密和資料流的 hello 指定傳遞原則 （例如 AES、 一般加密或不加密）。

## <a name="create-contentkeys-used-for-encryption"></a>建立要用於加密的 ContentKey
加密的資產有 toobe 與儲存體加密金鑰相關聯。 您必須建立 hello 內容的索引鍵 toobe 用於加密之前建立 hello 資產檔案。 本章節描述如何 toocreate 內容金鑰。

hello 以下是產生內容金鑰會與您想要 toobe 加密的資產相關聯的一般步驟。 

1. 對於儲存體加密，請隨機產生 32 個位元組的 AES 金鑰。 
   
    這會成為 hello 資產，這表示相關聯的所有檔案的內容索引鍵與該資產將會需要 toouse hello 同內容金鑰解密期間。 
2. 呼叫 hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid)和[GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey)方法 tooget hello 正確的 X.509 憑證必須使用的 tooencrypt 將內容金鑰。
3. 將內容金鑰加密使用公開金鑰的 X.509 憑證的 hello hello。 
   
   Media Services.NET SDK 會使用 RSA OAEP 執行 hello 加密時。  您可以看到.NET 中的範例 hello [EncryptSymmetricKeyData 函式](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)。
4. 建立使用 hello 金鑰識別碼和內容金鑰計算的總和檢查碼值。 下列.NET 範例 hello 計算使用 hello 金鑰識別碼 hello GUID 部分 hello 總和檢查碼，並 hello 清除內容金鑰。

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

1. 建立 hello 內容金鑰以 hello **EncryptedContentKey** （轉換 toobase64 編碼的字串） **ProtectionKeyId**， **ProtectionKeyType**， **ContentKeyType**，和**總和檢查碼**您在先前步驟中收到的值。

    儲存體加密 hello 下列屬性應該包含 hello 要求主體中。

    要求本文屬性    | 說明
    ---|---
    識別碼 | hello 我們所產生的 ContentKey 識別碼自己使用 hello 下列格式，"nb:<NEW GUID>"。
    ContentKeyType | 這是 hello 內容金鑰類型為此內容金鑰的整數。 我們傳遞儲存體加密的 hello 值 1。
    EncryptedContentKey | 我們會建立新的內容金鑰值，其為 256 位元 (32 位元組) 的值。 使用 hello 儲存加密 X.509 憑證執行 hello GetProtectionKeyId 與 GetProtectionKey 方法的 HTTP GET 要求來擷取從 Microsoft Azure Media Services，hello 金鑰進行加密。 例如，請參閱下列.NET 程式碼的 hello: hello **EncryptSymmetricKeyData**方法定義[這裡](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs)。
    ProtectionKeyId | 這是我們的內容金鑰 hello hello 儲存加密 X.509 憑證的已使用的 tooencrypt 保護金鑰識別碼。
    ProtectionKeyType | 這是 hello hello 已使用的 tooencrypt hello 內容金鑰的保護金鑰的加密類型。 針對本文範例，此值為 StorageEncryption(1)。
    Checksum |hello MD5 計算總和檢查碼 hello 內容金鑰。 會透過加密 hello 內容金鑰的 hello 內容識別碼，以執行計算。 hello 範例程式碼會示範如何 toocalculate hello 總和檢查碼。


### <a name="retrieve-hello-protectionkeyid"></a>擷取 ProtectionKeyId hello
hello 下列範例顯示如何 tooretrieve hello 的 hello 憑證內容金鑰加密時，您必須使用的憑證指紋 ProtectionKeyId。 執行這個步驟 toomake 確定您的電腦上已經有 hello 適當的憑證。

要求：

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

回應：

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

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a>擷取 ProtectionKeyId hello ProtectionKey
hello 下列範例示範如何使用 hello ProtectionKeyId tooretrieve hello X.509 憑證中收到 hello 上一個步驟。

要求：

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

回應：

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

### <a name="create-hello-content-key"></a>建立 hello 內容金鑰
您有擷取 hello X.509 憑證，並使用其公用金鑰 tooencrypt 將內容金鑰之後，建立**ContentKey**實體和其屬性值，據此設定。

其中一個 hello 值，您必須設定時建立 hello 內容金鑰是 hello 型別。 發生 hello 儲存體加密，hello 值為 '1'。 

下列範例會示範如何 hello toocreate **ContentKey**與**ContentKeyType**設定儲存體加密 ("1") 和 hello **ProtectionKeyType**設定太"0 的"hello 保護金鑰識別碼的 tooindicate 是 hello X.509 憑證指紋。  

要求

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

回應：

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

## <a name="create-an-asset"></a>建立資產
下列範例會示範如何 hello toocreate 資產。

**HTTP 要求**

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

**HTTP 回應**

如果成功，則會傳回 hello 下列：

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

## <a name="associate-hello-contentkey-with-an-asset"></a>將 hello ContentKey 與資產產生關聯
建立 hello ContentKey 之後, 將它與關聯使用 hello $links 作業在資產中 hello 下列範例所示：

要求：

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

回應：

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a>建立 AssetFile
hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile)實體代表儲存在 blob 容器的視訊或音訊檔案。 資產檔案一律會與資產相關聯，而資產可包含一或多個資產檔案。 如果資產檔案物件不是 blob 容器中的數位檔案相關聯，hello Media Services 編碼器工作會失敗。

請注意該 hello **AssetFile**執行個體與 hello 實際媒體檔案的兩個相異的物件。 hello AssetFile 執行個體包含 hello 媒體檔案的相關中繼資料，而 hello 媒體檔案包含 hello 實際的媒體內容。

您將數位媒體檔案上傳到 blob 容器之後，您將使用 hello**合併**HTTP 要求 tooupdate hello AssetFile （本主題中未顯示） 您的媒體檔案的相關資訊。 

**HTTP 要求**

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

**HTTP 回應**

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
