---
title: "aaaConnecting tooMedia 使用 REST API 的服務帳戶 |Microsoft 文件"
description: "本主題示範如何 tooconnect tooMedia 服務 uisng REST API。"
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>連接 tooMedia 使用媒體服務 REST API 的服務帳戶
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

本主題描述如何以程式設計方式連接 tooMicrosoft 與進行程式設計時，Azure Media Services tooobtain hello 媒體服務 REST API。

存取 Microsoft Azure Media Services 時，有需要兩件事： 本身提供的 Azure 存取控制服務 (ACS) 和 hello 媒體服務 URI 的存取權杖。 您可以使用任何您想要建立這些要求，只要指定 hello 正確的標頭值，並在 hello 存取權杖中正確地呼叫時，傳遞到 Media Services 時的方式。

hello 下列步驟描述 hello 最常見的工作流程時使用 hello 媒體服務 REST API tooconnect tooMedia Services:

1. 取得存取權杖 
2. 連接 toohello 媒體服務 URI 
   
   > [!NOTE]
   > 已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。
   > 您也可能會收到的 HTTP/1.1 200 回應包含 hello ODATA API 中繼資料描述。
   > 
   > 
3. Post 您後續的 API 呼叫 toohello 新的 URL。 
   
    比方說，如果在嘗試後 tooconnect，您會取得 hello 下列：
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    您應該張貼您後續的 API 呼叫 toohttps://wamsbayclus001rest-hs.cloudapp.net/api/。

    >[!NOTE]
    >對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。 您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。 如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。

## <a name="access-control-address"></a>存取控制服務
媒體服務存取控制位址是 https://wamsprodglobal001acs.accesscontrol.windows.net，中國北部區域除外，該區域是 https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn。

## <a name="getting-an-access-token"></a>取得存取權杖
tooaccess Media Services 直接透過 hello REST API，從 ACS 擷取存取權杖和 hello 服務的每個 HTTP 要求期間使用。 這個語彙基元是根據 hello 標頭的 HTTP 要求，並使用 hello OAuth v2 通訊協定中提供的存取宣告的 ACS 所提供的類似 tooother 語彙基元。 您不需要任何其他先決條件之前 tooMedia 服務直接連線。

hello 下列範例顯示 hello HTTP 要求標頭和本文使用 tooretrieve 語彙基元。

**標頭**：

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**主體**：

您需要 tooprove hello client_id 與 client_secret 值 hello 這個要求主體中client_id 與 client_secret 分別對應 toohello AccountName 和 AccountKey 值。 這些值是由 Media Services 提供 tooyou，當您設定您的帳戶。 

媒體服務帳戶必須是 URL 編碼，請注意該 hello AccountKey (請參閱[百分比編碼](http://tools.ietf.org/html/rfc3986#section-2.1)時用它來作為您的存取權杖要求中的 hello client_secret 值。

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


例如： 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


hello 以下範例顯示 hello HTTP 回應，其中包含 hello 存取權杖 hello 回應主體中。

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> 建議 toocache hello"access_token"和"expires_in"值 tooan 外部儲存體。 hello 語彙基元資料無法稍後擷取自 hello 存放裝置，媒體服務 REST API 的呼叫中重複使用。 這是其中 hello 語彙基元可以在多個處理程序或電腦間安全共用的案例特別有用。
> 
> 

請確定 toomonitor hello"expires_in"值的 hello 存取權杖，然後視需要以新權杖更新您的 REST API 呼叫。

### <a name="connecting-toohello-media-services-uri"></a>連接 toohello 媒體服務 URI
hello 根媒體服務 URI 為 https://media.windows.net/。 一開始，您應該連接 toothis URI，以及如果回應中出現 301 重新導向，您應該進行後續呼叫 toohello 新的 URI。 此外，請勿在要求中使用任何自動重新導向/跟隨邏輯。 HTTP 動詞與要求本文不會轉送 toohello 新的 URI。

請注意上, 傳與下載 Asset 檔案的 URI 是 https://yourstorageaccount.blob.core.windows.net/ 其中 hello 儲存體帳戶名稱是您的 Media Services 帳戶設定期間使用的同一個 hello 的 hello 根。

下列範例中的 hello 示範 HTTP 要求 toohello 媒體服務根目錄 URI (https://media.windows.net/)。 hello 要求會取得 301 重新導向回應中。 hello 後續要求使用 hello 新的 URI (https://wamsbayclus001rest-hs.cloudapp.net/api/)。     

**HTTP 要求**：

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**HTTP 回應**：

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


**HTTP 要求**(使用 hello 新的 URI):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**HTTP 回應**：

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> 一旦您取得 hello 新的 URI 是 hello 應該使用的 toocommunicate 使用媒體服務的 URI。 
> 
> 

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

