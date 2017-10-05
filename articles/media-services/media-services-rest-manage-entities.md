---
title: "使用 REST 管理媒體服務實體 | Microsoft Docs"
description: "深入了解如何使用 REST API 管理媒體服務實體。"
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
ms.openlocfilehash: a336907b605da962f835b8057ac6071f480cd85e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="managing-media-services-entities-with-rest"></a><span data-ttu-id="99d8f-103">使用 REST 管理媒體服務實體</span><span class="sxs-lookup"><span data-stu-id="99d8f-103">Managing Media Services entities with REST</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99d8f-104">REST</span><span class="sxs-lookup"><span data-stu-id="99d8f-104">REST</span></span>](media-services-rest-manage-entities.md)
> * [<span data-ttu-id="99d8f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="99d8f-105">.NET</span></span>](media-services-dotnet-manage-entities.md)
> 
> 

<span data-ttu-id="99d8f-106">Microsoft Azure 媒體服務是以 REST 為基礎的服務，內建在 OData v3 上。</span><span class="sxs-lookup"><span data-stu-id="99d8f-106">Microsoft Azure Media Services is a REST-based service built on OData v3.</span></span> <span data-ttu-id="99d8f-107">您可以使用與任何其他 OData 服務上的相同方式，新增、查詢、更新和刪除實體。</span><span class="sxs-lookup"><span data-stu-id="99d8f-107">You can add, query, update, and delete entities in much the same way as you can on any other OData service.</span></span> <span data-ttu-id="99d8f-108">在適用時會呼叫例外狀況。</span><span class="sxs-lookup"><span data-stu-id="99d8f-108">Exceptions will be called out when applicable.</span></span> <span data-ttu-id="99d8f-109">如需 OData 的詳細資訊，請參閱 [開放式資料通訊協定文件](http://www.odata.org/documentation/)。</span><span class="sxs-lookup"><span data-stu-id="99d8f-109">For more information on OData, see [Open Data Protocol documentation](http://www.odata.org/documentation/).</span></span>

<span data-ttu-id="99d8f-110">本主題說明如何使用 REST 管理 Azure 媒體服務實體。</span><span class="sxs-lookup"><span data-stu-id="99d8f-110">This topic shows you how to manage Azure Media Services entities with REST.</span></span>

>[!NOTE]
> <span data-ttu-id="99d8f-111">從 2017 年 4 月 1 日起，您的帳戶中任何超過 90 天的作業記錄以及其相關工作記錄都會自動刪除，即使記錄總數低於配額上限亦然。</span><span class="sxs-lookup"><span data-stu-id="99d8f-111">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if the total number of records is below the maximum quota.</span></span> <span data-ttu-id="99d8f-112">例如，在 2017 年 4 月 1 日，您帳戶中任何在 2016 年 12 月 31 日以前的作業記錄將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="99d8f-112">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="99d8f-113">如果您需要封存作業/工作資訊，您可以使用本主題中所述的程式碼。</span><span class="sxs-lookup"><span data-stu-id="99d8f-113">If you need to archive the job/task information, you can use the code described in this topic.</span></span>

## <a name="considerations"></a><span data-ttu-id="99d8f-114">考量</span><span class="sxs-lookup"><span data-stu-id="99d8f-114">Considerations</span></span>  

<span data-ttu-id="99d8f-115">在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。</span><span class="sxs-lookup"><span data-stu-id="99d8f-115">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="99d8f-116">如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="99d8f-116">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="99d8f-117">連線到媒體服務</span><span class="sxs-lookup"><span data-stu-id="99d8f-117">Connect to Media Services</span></span>

<span data-ttu-id="99d8f-118">如需連線至 AMS API 的詳細資訊，請參閱[使用 Azure AD 驗證存取 Azure 媒體服務 API](media-services-use-aad-auth-to-access-ams-api.md)。</span><span class="sxs-lookup"><span data-stu-id="99d8f-118">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="99d8f-119">順利連接到 https://media.windows.net 之後，您會收到 301 重新導向，指定另一個媒體服務 URI。</span><span class="sxs-lookup"><span data-stu-id="99d8f-119">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="99d8f-120">後續的呼叫必須送到新的 URI。</span><span class="sxs-lookup"><span data-stu-id="99d8f-120">You must make subsequent calls to the new URI.</span></span>

## <a name="adding-entities"></a><span data-ttu-id="99d8f-121">加入實體</span><span class="sxs-lookup"><span data-stu-id="99d8f-121">Adding entities</span></span>
<span data-ttu-id="99d8f-122">媒體服務中的每個實體會透過 POST HTTP 要求加入至實體集 (例如資產)。</span><span class="sxs-lookup"><span data-stu-id="99d8f-122">Every entity in Media Services is added to an entity set, such as Assets, through a POST HTTP request.</span></span>

<span data-ttu-id="99d8f-123">下列範例示範如何建立 AccessPolicy。</span><span class="sxs-lookup"><span data-stu-id="99d8f-123">The following example shows how to create an AccessPolicy.</span></span>

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

## <a name="querying-entities"></a><span data-ttu-id="99d8f-124">查詢實體</span><span class="sxs-lookup"><span data-stu-id="99d8f-124">Querying entities</span></span>
<span data-ttu-id="99d8f-125">查詢及列出實體很簡單，只牽涉到 GET HTTP 要求與選用 OData 作業。</span><span class="sxs-lookup"><span data-stu-id="99d8f-125">Querying and listing entities is straightforward and only involves a GET HTTP request and optional OData operations.</span></span>
<span data-ttu-id="99d8f-126">下列範例會擷取所有 MediaProcessor 實體的清單。</span><span class="sxs-lookup"><span data-stu-id="99d8f-126">The following example retrieves a list of all MediaProcessor entities.</span></span>

    GET https://media.windows.net/API/MediaProcessors HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="99d8f-127">您也可以擷取特定實體或與特定實體相關聯的所有實體集，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="99d8f-127">You can also retrieve a specific entity or all entity sets associated with a specific entity, such as in the following examples:</span></span>

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

<span data-ttu-id="99d8f-128">下列範例僅會傳回所有工作的狀態屬性。</span><span class="sxs-lookup"><span data-stu-id="99d8f-128">The following example returns only the State property of all Jobs.</span></span>

    GET https://media.windows.net/API/Jobs?$select=State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

<span data-ttu-id="99d8f-129">以下範例會傳回名為 "SampleTemplate" 的所有 JobTemplates。</span><span class="sxs-lookup"><span data-stu-id="99d8f-129">The following example returns all JobTemplates with the name "SampleTemplate."</span></span>

    GET https://media.windows.net/API/JobTemplates?$filter=startswith(Name,%20'SampleTemplate') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

> [!NOTE]
> <span data-ttu-id="99d8f-130">媒體服務中不支援 $Expand 作業，以及 LINQ 考量 (WCF 資料服務) 中所述之不支援的 LINQ 方法。</span><span class="sxs-lookup"><span data-stu-id="99d8f-130">The $expand operation is not supported in Media Services as well as the unsupported LINQ methods described in LINQ Considerations (WCF Data Services).</span></span>
> 
> 

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="99d8f-131">透過實體的大型集合列舉</span><span class="sxs-lookup"><span data-stu-id="99d8f-131">Enumerating through large collections of entities</span></span>
<span data-ttu-id="99d8f-132">查詢項目時，有一次最多傳回 1000 個實體的限制，因為公用 REST v2 有 1000 個查詢結果數目的限制。</span><span class="sxs-lookup"><span data-stu-id="99d8f-132">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results to 1000 results.</span></span> <span data-ttu-id="99d8f-133">使用 **skip** 和 **top** 來透過實體的大型集合列舉。</span><span class="sxs-lookup"><span data-stu-id="99d8f-133">Use **skip** and **top** to enumerate through the large collection of entities.</span></span> 

<span data-ttu-id="99d8f-134">以下範例說明如何使用 **skip** 和 **top** 來略過最前面 2000 項作業並取得接下來的 1000 項作業。</span><span class="sxs-lookup"><span data-stu-id="99d8f-134">The following example shows how to use **skip** and **top** to skip the first 2000 jobs and get the next 1000 jobs.</span></span>  

    GET https://media.windows.net/api/Jobs()?$skip=2000&$top=1000 HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337078831&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=suFkxhvPWxQVMjOYelOJfYEWkyTWJCBc02pF0N7NghI%3d
    Host: media.windows.net

## <a name="updating-entities"></a><span data-ttu-id="99d8f-135">更新實體</span><span class="sxs-lookup"><span data-stu-id="99d8f-135">Updating entities</span></span>
<span data-ttu-id="99d8f-136">根據實體類型及其所處狀態，您可以透過 PATCH、PUT 或 MERGE HTTP 要求，更新該實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="99d8f-136">Depending on the entity type and the state that it is in, you can update properties on that entity through a PATCH, PUT, or MERGE HTTP requests.</span></span> <span data-ttu-id="99d8f-137">如需這些作業的詳細資訊，請參閱 [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99d8f-137">For more information about these operations, see [PATCH/PUT/MERGE](https://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="99d8f-138">下列程式碼範例示範如何更新資產實體上的 [名稱] 屬性。</span><span class="sxs-lookup"><span data-stu-id="99d8f-138">The following code example shows how to update the Name property on an Asset entity.</span></span>

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

## <a name="deleting-entities"></a><span data-ttu-id="99d8f-139">刪除實體</span><span class="sxs-lookup"><span data-stu-id="99d8f-139">Deleting entities</span></span>
<span data-ttu-id="99d8f-140">可以使用 DELETE HTTP 要求，在媒體服務中刪除實體。</span><span class="sxs-lookup"><span data-stu-id="99d8f-140">Entities can be deleted in Media Services by using a DELETE HTTP request.</span></span> <span data-ttu-id="99d8f-141">根據實體，您刪除實體的順序可能很重要。</span><span class="sxs-lookup"><span data-stu-id="99d8f-141">Depending on the entity, the order in which you delete entities may be important.</span></span> <span data-ttu-id="99d8f-142">例如，資產等實體需要您撤銷 (或刪除) 參考該特定資產的所有定位器，然後再刪除資產。</span><span class="sxs-lookup"><span data-stu-id="99d8f-142">For example, entities such as Assets require that you revoke (or delete) all Locators that reference that particular Asset before deleting the Asset.</span></span>

<span data-ttu-id="99d8f-143">下列範例示範如何刪除用於將檔案上傳至 Blob 儲存體的定位器。</span><span class="sxs-lookup"><span data-stu-id="99d8f-143">The following example shows how to delete a Locator that was used to upload a file into blob storage.</span></span>

    DELETE https://media.windows.net/API/Locators('nb:lid:UUID:76dcc8e8-4230-463d-97b0-ce25c41b5c8d') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: media.windows.net
    Content-Length: 0

## <a name="media-services-learning-paths"></a><span data-ttu-id="99d8f-144">媒體服務學習路徑</span><span class="sxs-lookup"><span data-stu-id="99d8f-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="99d8f-145">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="99d8f-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

