---
title: "使用 REST API 連接到媒體服務帳戶 | Microsoft Docs"
description: "本主題示範如何使用 REST API 連接到媒體服務。"
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
ms.openlocfilehash: 4feb0eb81823835e8e0b701463d85b27f5598019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connecting-to-media-services-account-using-media-services-rest-api"></a><span data-ttu-id="01f56-103">使用媒體服務 REST API 連接到媒體服務帳戶</span><span class="sxs-lookup"><span data-stu-id="01f56-103">Connecting to Media Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01f56-104">.NET</span><span class="sxs-lookup"><span data-stu-id="01f56-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="01f56-105">REST</span><span class="sxs-lookup"><span data-stu-id="01f56-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="01f56-106">本主題描述如何在使用媒體服務 REST API 進行程式設計時，取得 Microsoft Azure 媒體服務的程式設計連線。</span><span class="sxs-lookup"><span data-stu-id="01f56-106">This topic describes how to obtain a programmatic connection to Microsoft Azure Media Services when you are programming with the Media Services REST API.</span></span>

<span data-ttu-id="01f56-107">存取 Microsoft Azure 媒體服務時需要兩件事：由 Azure 存取控制服務 (ACS) 提供的存取權杖，以及媒體服務本身的 URI。</span><span class="sxs-lookup"><span data-stu-id="01f56-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and the URI of Media Services itself.</span></span> <span data-ttu-id="01f56-108">建立這些要求時可以使用任何方式，前提是您指定正確的標頭值，並在呼叫媒體服務時正確傳入存取權杖。</span><span class="sxs-lookup"><span data-stu-id="01f56-108">You can use any means you want when creating these requests as long as you specify the correct header values and pass in the access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="01f56-109">當您使用媒體服務 REST API 連接到媒體服務時，下列步驟將說明最常見的工作流程：</span><span class="sxs-lookup"><span data-stu-id="01f56-109">The following steps describe the most common workflow when using the Media Services REST API to connect to Media Services:</span></span>

1. <span data-ttu-id="01f56-110">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="01f56-110">Getting an access token</span></span> 
2. <span data-ttu-id="01f56-111">連接至媒體服務 URI</span><span class="sxs-lookup"><span data-stu-id="01f56-111">Connecting to the Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="01f56-112">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="01f56-112">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="01f56-113">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="01f56-113">You must make subsequent calls to the new URI.</span></span>
   > <span data-ttu-id="01f56-114">您也可能會收到 HTTP/1.1 200 回應，其中包含 ODATA API 中繼資料描述。</span><span class="sxs-lookup"><span data-stu-id="01f56-114">You may also receive a HTTP/1.1 200 response that contains the ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="01f56-115">將後續的 API 呼叫張貼到新的 URL。</span><span class="sxs-lookup"><span data-stu-id="01f56-115">Post your subsequent API calls to the new URL.</span></span> 
   
    <span data-ttu-id="01f56-116">例如，如果您在嘗試進行連接之後得到下列結果：</span><span class="sxs-lookup"><span data-stu-id="01f56-116">For example, if after trying to connect, you got the following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="01f56-117">您應該將後續的 API 呼叫張貼到 https://wamsbayclus001rest-hs.cloudapp.net/api/。</span><span class="sxs-lookup"><span data-stu-id="01f56-117">You should post your subsequent API calls to https://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="01f56-118">對於不同的 AMS 原則 (例如 Locator 原則或 ContentKeyAuthorizationPolicy) 有 1,000,000 個原則的限制。</span><span class="sxs-lookup"><span data-stu-id="01f56-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="01f56-119">如果您一律使用相同的日期 / 存取權限，例如，要長時間維持就地 (非上載原則) 的定位器原則，您應該使用相同的原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="01f56-119">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="01f56-120">如需詳細資訊，請參閱 [這個](media-services-dotnet-manage-entities.md#limit-access-policies) 主題。</span><span class="sxs-lookup"><span data-stu-id="01f56-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="01f56-121">存取控制服務</span><span class="sxs-lookup"><span data-stu-id="01f56-121">Access control address</span></span>
<span data-ttu-id="01f56-122">媒體服務存取控制位址是 https://wamsprodglobal001acs.accesscontrol.windows.net，中國北部區域除外，該區域是 https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn。</span><span class="sxs-lookup"><span data-stu-id="01f56-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="01f56-123">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="01f56-123">Getting an access token</span></span>
<span data-ttu-id="01f56-124">若要直接透過 REST API 存取媒體服務，從 ACS 擷取存取權杖，並在每個您對服務提出的 HTTP 要求中使用它。</span><span class="sxs-lookup"><span data-stu-id="01f56-124">To access Media Services directly through the REST API, retrieve an access token from ACS and use it during every HTTP request you make into the service.</span></span> <span data-ttu-id="01f56-125">這個權杖類似於 ACS 根據 HTTP 要求標頭中提供的存取宣告而提供的其他權杖，以及使用 OAuth v2 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="01f56-125">This token is similar to other tokens provided by ACS based on access claims provided in the header of an HTTP request and using the OAuth v2 protocol.</span></span> <span data-ttu-id="01f56-126">直接連接到媒體服務之前，您不需要其他任何必要條件。</span><span class="sxs-lookup"><span data-stu-id="01f56-126">You do not need any other prerequisites before directly connecting to Media Services.</span></span>

<span data-ttu-id="01f56-127">下列範例會顯示用來擷取權杖的 HTTP 要求標頭和主體。</span><span class="sxs-lookup"><span data-stu-id="01f56-127">The following example shows the HTTP request header and body used to retrieve a token.</span></span>

<span data-ttu-id="01f56-128">**標頭**：</span><span class="sxs-lookup"><span data-stu-id="01f56-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="01f56-129">**主體**：</span><span class="sxs-lookup"><span data-stu-id="01f56-129">**Body**:</span></span>

<span data-ttu-id="01f56-130">您需要在這個要求的主體中證明 client_id 與 client_secret 值；client_id 與 client_secret 分別對應到 AccountName 與 AccountKey 值。</span><span class="sxs-lookup"><span data-stu-id="01f56-130">You need to prove the client_id and client_secret values in the body of this request; client_id and client_secret correspond to the AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="01f56-131">當您設定帳戶時，媒體服務會提供這些值給您。</span><span class="sxs-lookup"><span data-stu-id="01f56-131">These values are provided to you by Media Services when you set up your account.</span></span> 

<span data-ttu-id="01f56-132">請注意，您的媒體服務帳戶的 AccountKey 在使用它做為存取權杖要求中 client_secret 值時必須已編碼 URL (請參閱 [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1))。</span><span class="sxs-lookup"><span data-stu-id="01f56-132">Note that the AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as the client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="01f56-133">例如：</span><span class="sxs-lookup"><span data-stu-id="01f56-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="01f56-134">下列範例會顯示在回應主體中包含存取權杖的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="01f56-134">The following example shows the HTTP response that contains the access token in the response body.</span></span>

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
> <span data-ttu-id="01f56-135">建議您將 "access_token" 和 "expires_in" 值快取到外部儲存體。</span><span class="sxs-lookup"><span data-stu-id="01f56-135">It is recommended to cache the "access_token " and "expires_in " values to an external storage.</span></span> <span data-ttu-id="01f56-136">稍後可以從儲存體擷取權杖資料，然後重複使用在媒體服務 REST API 呼叫中。</span><span class="sxs-lookup"><span data-stu-id="01f56-136">The token data could later be retrieved from the storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="01f56-137">這特別適用於權杖可以在多個處理程序或電腦之間安全共用的情況。</span><span class="sxs-lookup"><span data-stu-id="01f56-137">This is especially useful for scenarios where the token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="01f56-138">請務必監控存取權杖的 "expires_in" 值，並視需要以新權杖更新您的 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="01f56-138">Make sure to monitor the "expires_in" value of the access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-to-the-media-services-uri"></a><span data-ttu-id="01f56-139">連接至媒體服務 URI</span><span class="sxs-lookup"><span data-stu-id="01f56-139">Connecting to the Media Services URI</span></span>
<span data-ttu-id="01f56-140">根媒體服務 URI 為 https://media.windows.net/。</span><span class="sxs-lookup"><span data-stu-id="01f56-140">The root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="01f56-141">您應該一開始會連接到此 URI，而且如果回應中出現 301 重新導向，您應該將後續呼叫送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="01f56-141">You should initially connect to this URI, and if you get a 301 redirect back in response, you should make subsequent calls to the new URI.</span></span> <span data-ttu-id="01f56-142">此外，請勿在要求中使用任何自動重新導向/跟隨邏輯。</span><span class="sxs-lookup"><span data-stu-id="01f56-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="01f56-143">HTTP 指令動詞與要求主體不會轉送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="01f56-143">HTTP verbs and request bodies will not be forwarded to the new URI.</span></span>

<span data-ttu-id="01f56-144">請注意，上傳與下載資產檔案的根 URI 是 https://yourstorageaccount.blob.core.windows.net/，其中儲存體帳戶名稱是您在媒體服務帳戶設定期間所用的相同名稱。</span><span class="sxs-lookup"><span data-stu-id="01f56-144">Note that the root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where the storage account name is the same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="01f56-145">下列範例示範對媒體服務根 URI 的 HTTP 要求 (https://media.windows.net/)。</span><span class="sxs-lookup"><span data-stu-id="01f56-145">The following example demonstrates HTTP request to the Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="01f56-146">此要求會在回應中得到 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="01f56-146">The request gets a 301 redirect back in response.</span></span> <span data-ttu-id="01f56-147">後續要求是使用新的 URI (https://wamsbayclus001rest-hs.cloudapp.net/api/)。</span><span class="sxs-lookup"><span data-stu-id="01f56-147">The subsequent request is using the new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="01f56-148">**HTTP 要求**：</span><span class="sxs-lookup"><span data-stu-id="01f56-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="01f56-149">**HTTP 回應**：</span><span class="sxs-lookup"><span data-stu-id="01f56-149">**HTTP Response**:</span></span>

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
    <h2>Object moved to <a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="01f56-150">**HTTP 要求** (使用新的 URI)：</span><span class="sxs-lookup"><span data-stu-id="01f56-150">**HTTP Request** (using the new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="01f56-151">**HTTP 回應**：</span><span class="sxs-lookup"><span data-stu-id="01f56-151">**HTTP Response**:</span></span>

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
> <span data-ttu-id="01f56-152">取得新的 URI 之後，便應該使用此 URI 來與媒體服務通訊。</span><span class="sxs-lookup"><span data-stu-id="01f56-152">Once you get the new URI, that is the URI that should be used to communicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="01f56-153">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="01f56-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="01f56-154">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="01f56-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

