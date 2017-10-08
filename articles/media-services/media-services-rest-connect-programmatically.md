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
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="4a338-103">連接 tooMedia 使用媒體服務 REST API 的服務帳戶</span><span class="sxs-lookup"><span data-stu-id="4a338-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a338-104">.NET</span><span class="sxs-lookup"><span data-stu-id="4a338-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="4a338-105">REST</span><span class="sxs-lookup"><span data-stu-id="4a338-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="4a338-106">本主題描述如何以程式設計方式連接 tooMicrosoft 與進行程式設計時，Azure Media Services tooobtain hello 媒體服務 REST API。</span><span class="sxs-lookup"><span data-stu-id="4a338-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="4a338-107">存取 Microsoft Azure Media Services 時，有需要兩件事： 本身提供的 Azure 存取控制服務 (ACS) 和 hello 媒體服務 URI 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="4a338-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="4a338-108">您可以使用任何您想要建立這些要求，只要指定 hello 正確的標頭值，並在 hello 存取權杖中正確地呼叫時，傳遞到 Media Services 時的方式。</span><span class="sxs-lookup"><span data-stu-id="4a338-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="4a338-109">hello 下列步驟描述 hello 最常見的工作流程時使用 hello 媒體服務 REST API tooconnect tooMedia Services:</span><span class="sxs-lookup"><span data-stu-id="4a338-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="4a338-110">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="4a338-110">Getting an access token</span></span> 
2. <span data-ttu-id="4a338-111">連接 toohello 媒體服務 URI</span><span class="sxs-lookup"><span data-stu-id="4a338-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="4a338-112">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="4a338-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="4a338-113">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="4a338-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="4a338-114">您也可能會收到的 HTTP/1.1 200 回應包含 hello ODATA API 中繼資料描述。</span><span class="sxs-lookup"><span data-stu-id="4a338-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="4a338-115">Post 您後續的 API 呼叫 toohello 新的 URL。</span><span class="sxs-lookup"><span data-stu-id="4a338-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="4a338-116">比方說，如果在嘗試後 tooconnect，您會取得 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4a338-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="4a338-117">您應該張貼您後續的 API 呼叫 toohttps://wamsbayclus001rest-hs.cloudapp.net/api/。</span><span class="sxs-lookup"><span data-stu-id="4a338-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="4a338-118">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="4a338-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="4a338-119">您應該使用 hello 如果一律使用相同的原則識別碼 hello 相同天 / 存取權限，例如，原則會就地預定的 tooremain 長時間 （非上載原則） 的定位器。</span><span class="sxs-lookup"><span data-stu-id="4a338-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="4a338-120">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="4a338-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="4a338-121">存取控制服務</span><span class="sxs-lookup"><span data-stu-id="4a338-121">Access control address</span></span>
<span data-ttu-id="4a338-122">媒體服務存取控制位址是 https://wamsprodglobal001acs.accesscontrol.windows.net，中國北部區域除外，該區域是 https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn。</span><span class="sxs-lookup"><span data-stu-id="4a338-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="4a338-123">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="4a338-123">Getting an access token</span></span>
<span data-ttu-id="4a338-124">tooaccess Media Services 直接透過 hello REST API，從 ACS 擷取存取權杖和 hello 服務的每個 HTTP 要求期間使用。</span><span class="sxs-lookup"><span data-stu-id="4a338-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="4a338-125">這個語彙基元是根據 hello 標頭的 HTTP 要求，並使用 hello OAuth v2 通訊協定中提供的存取宣告的 ACS 所提供的類似 tooother 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="4a338-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="4a338-126">您不需要任何其他先決條件之前 tooMedia 服務直接連線。</span><span class="sxs-lookup"><span data-stu-id="4a338-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="4a338-127">hello 下列範例顯示 hello HTTP 要求標頭和本文使用 tooretrieve 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="4a338-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="4a338-128">**標頭**：</span><span class="sxs-lookup"><span data-stu-id="4a338-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="4a338-129">**主體**：</span><span class="sxs-lookup"><span data-stu-id="4a338-129">**Body**:</span></span>

<span data-ttu-id="4a338-130">您需要 tooprove hello client_id 與 client_secret 值 hello 這個要求主體中client_id 與 client_secret 分別對應 toohello AccountName 和 AccountKey 值。</span><span class="sxs-lookup"><span data-stu-id="4a338-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="4a338-131">這些值是由 Media Services 提供 tooyou，當您設定您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a338-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="4a338-132">媒體服務帳戶必須是 URL 編碼，請注意該 hello AccountKey (請參閱[百分比編碼](http://tools.ietf.org/html/rfc3986#section-2.1)時用它來作為您的存取權杖要求中的 hello client_secret 值。</span><span class="sxs-lookup"><span data-stu-id="4a338-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="4a338-133">例如：</span><span class="sxs-lookup"><span data-stu-id="4a338-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="4a338-134">hello 以下範例顯示 hello HTTP 回應，其中包含 hello 存取權杖 hello 回應主體中。</span><span class="sxs-lookup"><span data-stu-id="4a338-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

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
> <span data-ttu-id="4a338-135">建議 toocache hello"access_token"和"expires_in"值 tooan 外部儲存體。</span><span class="sxs-lookup"><span data-stu-id="4a338-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="4a338-136">hello 語彙基元資料無法稍後擷取自 hello 存放裝置，媒體服務 REST API 的呼叫中重複使用。</span><span class="sxs-lookup"><span data-stu-id="4a338-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="4a338-137">這是其中 hello 語彙基元可以在多個處理程序或電腦間安全共用的案例特別有用。</span><span class="sxs-lookup"><span data-stu-id="4a338-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="4a338-138">請確定 toomonitor hello"expires_in"值的 hello 存取權杖，然後視需要以新權杖更新您的 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="4a338-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="4a338-139">連接 toohello 媒體服務 URI</span><span class="sxs-lookup"><span data-stu-id="4a338-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="4a338-140">hello 根媒體服務 URI 為 https://media.windows.net/。</span><span class="sxs-lookup"><span data-stu-id="4a338-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="4a338-141">一開始，您應該連接 toothis URI，以及如果回應中出現 301 重新導向，您應該進行後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="4a338-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="4a338-142">此外，請勿在要求中使用任何自動重新導向/跟隨邏輯。</span><span class="sxs-lookup"><span data-stu-id="4a338-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="4a338-143">HTTP 動詞與要求本文不會轉送 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="4a338-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="4a338-144">請注意上, 傳與下載 Asset 檔案的 URI 是 https://yourstorageaccount.blob.core.windows.net/ 其中 hello 儲存體帳戶名稱是您的 Media Services 帳戶設定期間使用的同一個 hello 的 hello 根。</span><span class="sxs-lookup"><span data-stu-id="4a338-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="4a338-145">下列範例中的 hello 示範 HTTP 要求 toohello 媒體服務根目錄 URI (https://media.windows.net/)。</span><span class="sxs-lookup"><span data-stu-id="4a338-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="4a338-146">hello 要求會取得 301 重新導向回應中。</span><span class="sxs-lookup"><span data-stu-id="4a338-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="4a338-147">hello 後續要求使用 hello 新的 URI (https://wamsbayclus001rest-hs.cloudapp.net/api/)。</span><span class="sxs-lookup"><span data-stu-id="4a338-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="4a338-148">**HTTP 要求**：</span><span class="sxs-lookup"><span data-stu-id="4a338-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="4a338-149">**HTTP 回應**：</span><span class="sxs-lookup"><span data-stu-id="4a338-149">**HTTP Response**:</span></span>

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


<span data-ttu-id="4a338-150">**HTTP 要求**(使用 hello 新的 URI):</span><span class="sxs-lookup"><span data-stu-id="4a338-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="4a338-151">**HTTP 回應**：</span><span class="sxs-lookup"><span data-stu-id="4a338-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="4a338-152">一旦您取得 hello 新的 URI 是 hello 應該使用的 toocommunicate 使用媒體服務的 URI。</span><span class="sxs-lookup"><span data-stu-id="4a338-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="4a338-153">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="4a338-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4a338-154">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="4a338-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

