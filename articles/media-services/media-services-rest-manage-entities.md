---
title: "aaaManaging 媒體服務實體與 REST |Microsoft 文件"
description: "了解如何 toomanage 媒體服務 REST API 的實體。"
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 95262a32-0f2a-4286-b9e2-1a1ca6399b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: bcdc5288e422ebc4e6f682a97da4e925ce237a79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="d8b5b-103">使用 REST 管理媒體服務實體</span><span class="sxs-lookup"><span data-stu-id="d8b5b-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8b5b-104">REST</span><span class="sxs-lookup"><span data-stu-id="d8b5b-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="d8b5b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d8b5b-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="d8b5b-106">Microsoft Azure 媒體服務是以 REST 為基礎的服務，內建在 OData v3 上。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="d8b5b-107">您可以新增、 查詢、 更新和刪除實體 hello 相同方式與您可以在任何其他 OData 服務。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-107">You can add, query, update, and delete entities in much hello same way as you can on any other OData service.</span></span> <span data-ttu-id="d8b5b-108">在適用時會呼叫例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="d8b5b-109">如需 OData 的詳細資訊，請參閱 [開放式資料通訊協定文件](http://www.odata.org/documentation/)。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="d8b5b-110">本主題說明如何與其他 toomanage Azure 媒體服務實體。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-110">This topic shows you how toomanage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="d8b5b-111">啟動年 4 月 1，2017，超過 90 天您帳戶中的任何工作記錄將會自動刪除，以及其相關聯的工作記錄，即使 hello 的總記錄數低於 hello 配額上限。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="d8b5b-112">例如，在 2017 年 4 月 1 日，您帳戶中任何在 2016 年 12 月 31 日以前的作業記錄將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="d8b5b-113">如果您需要 tooarchive hello 作業/工作資訊時，您可以使用本主題中所述的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-113">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="d8b5b-114">考量</span><span class="sxs-lookup"><span data-stu-id="d8b5b-114">Considerations</span></span>  

<span data-ttu-id="d8b5b-115">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d8b5b-116">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="d8b5b-117">TooMedia 服務連接</span><span class="sxs-lookup"><span data-stu-id="d8b5b-117">Connect tooMedia Services</span></span>

<span data-ttu-id="d8b5b-118">如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-118">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d8b5b-119">已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-119">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d8b5b-120">您必須進行的後續呼叫 toohello 新的 URI。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-120">You must make subsequent calls toohello new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="d8b5b-121">加入實體</span><span class="sxs-lookup"><span data-stu-id="d8b5b-121">Adding entities</span></span>
<span data-ttu-id="d8b5b-122">在 Media Services 中的每個實體會加入 tooan 實體集的資產，例如透過 POST HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-122">Every entity in Media Services is added tooan entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="d8b5b-123">下列範例會示範如何 hello toocreate AccessPolicy。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-123">hello following example shows how toocreate an AccessPolicy.</span></span>

    POST https://media.windows.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

## <a name="querying-entities"></a><span data-ttu-id="d8b5b-124">查詢實體</span><span class="sxs-lookup"><span data-stu-id="d8b5b-124">Querying entities</span></span>
<span data-ttu-id="d8b5b-125">查詢及列出實體很簡單，只牽涉到 GET HTTP 要求與選用 OData 作業。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="d8b5b-126">hello 下列範例會擷取所有 MediaProcessor 實體的清單。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-126">hello following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="d8b5b-127">您也可以擷取特定的實體或相關聯的特定實體，例如 hello 遵循範例中的所有實體集：</span><span class="sxs-lookup"><span data-stu-id="d8b5b-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in hello following examples:</span></span>

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

    GET https://media.windows.net/API/JobTemplates('nb:jtid:UUID:e81192f5-576f-b247-b781-70a790c20e7c')/TaskTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336907474&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=OpuY0CeTylqFFcFaP4pKUVGesT4PGx4CP55zDf2zXnc%3d
    Host: media.windows.net

<span data-ttu-id="d8b5b-128">hello 下列範例會傳回只 hello 狀態屬性的所有工作。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-128">hello following example returns only hello State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="d8b5b-129">hello 下列範例會傳回所有 Jobtemplate hello 名為 「 SampleTemplate。 」</span><span class="sxs-lookup"><span data-stu-id="d8b5b-129">hello following example returns all JobTemplates with hello name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="d8b5b-130">hello $expand 作業中不支援媒體服務以及 hello 不支援的 LINQ 的考量 (WCF Data Services) 中所述的 LINQ 方法。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-130">hello $expand operation is not supported in Media Services as well as hello unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="d8b5b-131">透過實體的大型集合列舉</span><span class="sxs-lookup"><span data-stu-id="d8b5b-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="d8b5b-132">當查詢實體，就會限制為 1000年因為公用 REST v2 限制查詢結果 too1000 結果一次傳回的實體。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="d8b5b-133">使用**略過**和**頂端**tooenumerate 透過 hello 大量實體的集合。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-133">Use **skip** and **top** tooenumerate through hello large collection of entities.</span></span> 

<span data-ttu-id="d8b5b-134">下列範例會示範如何 hello toouse**略過**和**頂端**tooskip hello 2000 第一次作業和 get hello 接下來 1000 個工作。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-134">hello following example shows how toouse **skip** and **top** tooskip hello first 2000 jobs and get hello next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="d8b5b-135">更新實體</span><span class="sxs-lookup"><span data-stu-id="d8b5b-135">Updating entities</span></span>
<span data-ttu-id="d8b5b-136">根據 hello 實體類型和 hello 狀態中，您可以更新屬性對該實體修補程式時，透過 PUT 或 MERGE HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-136">Depending on hello entity type and hello state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="d8b5b-137">如需這些作業的詳細資訊，請參閱 [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="d8b5b-138">hello，下列程式碼範例示範如何 tooupdate hello Asset 實體上的 [名稱] 屬性。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-138">hello following code example shows how tooupdate hello Name property on an Asset entity.</span></span>

    MERGE https://media.windows.net/API/Assets('nb:cid:UUID:80782407-3f87-4e60-a43e-5e4454232f60') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337083279&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=DMLQXWah4jO0icpfwyws5k%2b1aCDfz9KDGIGao20xk6g%3d
    Host: media.windows.net
    Content-Length: 21
    Expect: 100-continue

    {"Name" : "NewName" }

## <a name="deleting-entities"></a><span data-ttu-id="d8b5b-139">刪除實體</span><span class="sxs-lookup"><span data-stu-id="d8b5b-139">Deleting entities</span></span>
<span data-ttu-id="d8b5b-140">可以使用 DELETE HTTP 要求，在媒體服務中刪除實體。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="d8b5b-141">根據 hello 實體，您可以在其中刪除實體的 hello 順序可能很重要。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-141">Depending on hello entity, hello order in which you delete entities may be important.</span></span> <span data-ttu-id="d8b5b-142">例如，Asset 等實體，需要您撤銷 （或刪除） 然後再刪除 hello 資產參考該特定 Asset 的所有定位器。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting hello Asset.</span></span>

<span data-ttu-id="d8b5b-143">下列範例會示範如何 hello toodelete 已使用的 tooupload 檔案到 blob 儲存體的定位器。</span><span class="sxs-lookup"><span data-stu-id="d8b5b-143">hello following example shows how toodelete a Locator that was used tooupload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="d8b5b-144">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="d8b5b-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8b5b-145">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="d8b5b-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

