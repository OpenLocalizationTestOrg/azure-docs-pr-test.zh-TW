---
title: "Azure 媒體服務錯誤代碼 | Microsoft Docs"
description: "本主題提供 Azure 媒體服務錯誤代碼的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 39886a955124429302609dd9d5a7c20ae7f498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-media-services-error-codes"></a><span data-ttu-id="a32ac-103">Azure 媒體服務錯誤代碼</span><span class="sxs-lookup"><span data-stu-id="a32ac-103">Azure Media Services error codes</span></span>
<span data-ttu-id="a32ac-104">使用 Microsoft Azure 媒體服務時，您可能會根據問題從服務收到 HTTP 錯誤代碼，例如驗證權杖過期到媒體服務中不支援的動作。</span><span class="sxs-lookup"><span data-stu-id="a32ac-104">When using Microsoft Azure Media Services, you may receive HTTP error codes from the service depending on issues such as authentication tokens expiring to actions that are not supported in Media Services.</span></span> <span data-ttu-id="a32ac-105">以下是媒體服務可能會傳回的「HTTP 錯誤代碼」的清單，以及其可能原因。</span><span class="sxs-lookup"><span data-stu-id="a32ac-105">The following is a list of **HTTP error codes** that may be returned by Media Services and the possible causes for them.</span></span>  

## <a name="400-bad-request"></a><span data-ttu-id="a32ac-106">400 不正確的要求</span><span class="sxs-lookup"><span data-stu-id="a32ac-106">400 Bad Request</span></span>
<span data-ttu-id="a32ac-107">要求包含無效的資訊，並且因為下列其中一個原因遭到拒絕︰</span><span class="sxs-lookup"><span data-stu-id="a32ac-107">The request contains invalid information and is rejected due to one of the following reasons:</span></span>

* <span data-ttu-id="a32ac-108">指定了不支援的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="a32ac-108">An unsupported API version is specified.</span></span> <span data-ttu-id="a32ac-109">如需最新版本，請參閱[媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="a32ac-109">For the most current version, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="a32ac-110">未指定媒體服務的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="a32ac-110">The API version of Media Services is not specified.</span></span> <span data-ttu-id="a32ac-111">如需如何指定 API 版本的詳細資訊，請參閱[媒體服務作業 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="a32ac-111">For information on how to specify the API version, see [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a32ac-112">如果您使用 .NET 或 Java SDK 來連接到媒體服務，每當您針對媒體服務嘗試和執行某些動作時，會為您指定 API 版本。</span><span class="sxs-lookup"><span data-stu-id="a32ac-112">If you are using the .NET or Java SDKs to connect to Media Services, the API version is specified for you whenever you try and perform some action against Media Services.</span></span>
  > 
  > 
* <span data-ttu-id="a32ac-113">已指定未定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="a32ac-113">An undefined property has been specified.</span></span> <span data-ttu-id="a32ac-114">屬性名稱在錯誤訊息中。</span><span class="sxs-lookup"><span data-stu-id="a32ac-114">The property name is in the error message.</span></span> <span data-ttu-id="a32ac-115">只能指定屬於指定實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="a32ac-115">Only those properties that are members of a given entity can be specified.</span></span> <span data-ttu-id="a32ac-116">請參閱 [Azure 媒體服務 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)，以取得實體及其屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="a32ac-116">See [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) for a list of entities and their properties.</span></span>
* <span data-ttu-id="a32ac-117">已指定無效的屬性值。</span><span class="sxs-lookup"><span data-stu-id="a32ac-117">An invalid property value has been specified.</span></span> <span data-ttu-id="a32ac-118">屬性名稱在錯誤訊息中。</span><span class="sxs-lookup"><span data-stu-id="a32ac-118">The property name is in the error message.</span></span> <span data-ttu-id="a32ac-119">請參閱先前連結以取得有效屬性類型及其值。</span><span class="sxs-lookup"><span data-stu-id="a32ac-119">See the previous link for valid property types and their values.</span></span>
* <span data-ttu-id="a32ac-120">遺漏必要的屬性值。</span><span class="sxs-lookup"><span data-stu-id="a32ac-120">A property value is missing and is required.</span></span>
* <span data-ttu-id="a32ac-121">指定 URL 的一部分包含不正確的值。</span><span class="sxs-lookup"><span data-stu-id="a32ac-121">Part of the URL specified contains a bad value.</span></span>
* <span data-ttu-id="a32ac-122">嘗試更新 WriteOnce 屬性。</span><span class="sxs-lookup"><span data-stu-id="a32ac-122">An attempt was made to update a WriteOnce property.</span></span>
* <span data-ttu-id="a32ac-123">嘗試使用主要 AssetFile (未指定或無法決定) 建立具有輸入資產的作業。</span><span class="sxs-lookup"><span data-stu-id="a32ac-123">An attempt was made to create a Job that has an input Asset with a primary AssetFile that was not specified or could not be determined.</span></span>
* <span data-ttu-id="a32ac-124">嘗試更新 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="a32ac-124">An attempt was made to update a SAS Locator.</span></span> <span data-ttu-id="a32ac-125">僅能建立或刪除 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="a32ac-125">SAS locators can only be created or deleted.</span></span> <span data-ttu-id="a32ac-126">可以更新串流定位器。</span><span class="sxs-lookup"><span data-stu-id="a32ac-126">Streaming locators can be updated.</span></span> <span data-ttu-id="a32ac-127">如需詳細資訊，請參閱[定位器](https://docs.microsoft.com/rest/api/media/operations/locator)。</span><span class="sxs-lookup"><span data-stu-id="a32ac-127">For more information, see [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>
* <span data-ttu-id="a32ac-128">不支援的作業或查詢已提交。</span><span class="sxs-lookup"><span data-stu-id="a32ac-128">An unsupported operation or query was submitted.</span></span>

## <a name="401-unauthorized"></a><span data-ttu-id="a32ac-129">401 未經授權</span><span class="sxs-lookup"><span data-stu-id="a32ac-129">401 Unauthorized</span></span>
<span data-ttu-id="a32ac-130">由於下列其中一個原因，要求無法驗證 (在可授權之前)︰</span><span class="sxs-lookup"><span data-stu-id="a32ac-130">The request could not be authenticated (before it can be authorized) due to one of the following reasons:</span></span>

* <span data-ttu-id="a32ac-131">遺失驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="a32ac-131">Missing authentication header.</span></span>
* <span data-ttu-id="a32ac-132">不正確的驗證標頭值。</span><span class="sxs-lookup"><span data-stu-id="a32ac-132">Bad authentication header value.</span></span>
  * <span data-ttu-id="a32ac-133">權杖已過期。</span><span class="sxs-lookup"><span data-stu-id="a32ac-133">The token has expired.</span></span> 
  * <span data-ttu-id="a32ac-134">權杖包含無效的簽章。</span><span class="sxs-lookup"><span data-stu-id="a32ac-134">The token contains an invalid signature.</span></span>

## <a name="403-forbidden"></a><span data-ttu-id="a32ac-135">403 禁止</span><span class="sxs-lookup"><span data-stu-id="a32ac-135">403 Forbidden</span></span>
<span data-ttu-id="a32ac-136">基於下列原因之一不允許此要求：</span><span class="sxs-lookup"><span data-stu-id="a32ac-136">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="a32ac-137">找不到媒體服務帳戶，或已被刪除。</span><span class="sxs-lookup"><span data-stu-id="a32ac-137">The Media Services account cannot be found or has been deleted.</span></span>
* <span data-ttu-id="a32ac-138">媒體服務帳戶已停用，且要求類型並非 HTTP GET。</span><span class="sxs-lookup"><span data-stu-id="a32ac-138">The Media Services account is disabled and the request type is not HTTP GET.</span></span> <span data-ttu-id="a32ac-139">服務作業也會傳回 403 回應。</span><span class="sxs-lookup"><span data-stu-id="a32ac-139">Service operations will return a 403 response as well.</span></span>
* <span data-ttu-id="a32ac-140">驗證權杖不包含使用者的認證資訊︰AccountName 和/或 SubscriptionId。</span><span class="sxs-lookup"><span data-stu-id="a32ac-140">The authentication token does not contain the user’s credential information: AccountName and/or SubscriptionId.</span></span> <span data-ttu-id="a32ac-141">您可以在 Azure 管理入口網站中，媒體服務帳戶的媒體服務 UI 延伸模組中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="a32ac-141">You can find this information in the Media Services UI extension for your Media Services account in the Azure Management Portal.</span></span>
* <span data-ttu-id="a32ac-142">無法存取該資源。</span><span class="sxs-lookup"><span data-stu-id="a32ac-142">The resource cannot be accessed.</span></span>
  
  * <span data-ttu-id="a32ac-143">嘗試使用無法用於媒體服務帳戶的 MediaProcessor。</span><span class="sxs-lookup"><span data-stu-id="a32ac-143">An attempt was made to use a MediaProcessor that is not available for your Media Services account.</span></span>
  * <span data-ttu-id="a32ac-144">嘗試更新媒體服務所定義的 JobTemplate。</span><span class="sxs-lookup"><span data-stu-id="a32ac-144">An attempt was made to update a JobTemplate defined by Media Services.</span></span>
  * <span data-ttu-id="a32ac-145">嘗試覆寫某些其他媒體服務帳戶的定位器。</span><span class="sxs-lookup"><span data-stu-id="a32ac-145">An attempt was made to overwrite some other Media Services account's Locator.</span></span>
  * <span data-ttu-id="a32ac-146">嘗試覆寫某些其他媒體服務帳戶的 ContentKey。</span><span class="sxs-lookup"><span data-stu-id="a32ac-146">An attempt was made to overwrite some other Media Services account's ContentKey.</span></span>
* <span data-ttu-id="a32ac-147">無法建立資源，因為已達到媒體服務帳戶的服務配額。</span><span class="sxs-lookup"><span data-stu-id="a32ac-147">The resource could not be created due to a service quota that was reached for the Media Services account.</span></span> <span data-ttu-id="a32ac-148">如需服務配額的詳細資訊，請參閱[配額和限制](media-services-quotas-and-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="a32ac-148">For more information on the service quotas, see [Quotas and Limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="404-not-found"></a><span data-ttu-id="a32ac-149">404 找不到</span><span class="sxs-lookup"><span data-stu-id="a32ac-149">404 Not Found</span></span>
<span data-ttu-id="a32ac-150">基於下列原因之一不允許資源的要求：</span><span class="sxs-lookup"><span data-stu-id="a32ac-150">The request is not allowed on a resource due to one of the following reasons:</span></span>

* <span data-ttu-id="a32ac-151">嘗試更新不存在的實體。</span><span class="sxs-lookup"><span data-stu-id="a32ac-151">An attempt was made to update an entity that does not exist.</span></span>
* <span data-ttu-id="a32ac-152">嘗試刪除不存在的實體。</span><span class="sxs-lookup"><span data-stu-id="a32ac-152">An attempt was made to delete an entity that does not exist.</span></span>
* <span data-ttu-id="a32ac-153">嘗試建立實體，連結至不存在的實體。</span><span class="sxs-lookup"><span data-stu-id="a32ac-153">An attempt was made to create an entity that links to an entity that does not exist.</span></span>
* <span data-ttu-id="a32ac-154">嘗試取得不存在的實體。</span><span class="sxs-lookup"><span data-stu-id="a32ac-154">An attempt was made to GET an entity that does not exist.</span></span>
* <span data-ttu-id="a32ac-155">嘗試指定未與媒體服務帳戶相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a32ac-155">An attempt was made to specify a storage account that is not associated with the Media Services account.</span></span>  

## <a name="409-conflict"></a><span data-ttu-id="a32ac-156">409 衝突</span><span class="sxs-lookup"><span data-stu-id="a32ac-156">409 Conflict</span></span>
<span data-ttu-id="a32ac-157">基於下列原因之一不允許此要求：</span><span class="sxs-lookup"><span data-stu-id="a32ac-157">The request is not allowed due to one of the following reasons:</span></span>

* <span data-ttu-id="a32ac-158">多個 AssetFile 在資產內具有指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="a32ac-158">More than one AssetFile has the specified name within the Asset.</span></span>
* <span data-ttu-id="a32ac-159">嘗試建立資產中的第二個主要 AssetFile。</span><span class="sxs-lookup"><span data-stu-id="a32ac-159">An attempt was made to create a second primary AssetFile within the Asset.</span></span>
* <span data-ttu-id="a32ac-160">嘗試建立已使用指定識別碼的 ContentKey。</span><span class="sxs-lookup"><span data-stu-id="a32ac-160">An attempt was made to create a ContentKey with the specified Id already used.</span></span>
* <span data-ttu-id="a32ac-161">嘗試建立已使用指定識別碼的定位器。</span><span class="sxs-lookup"><span data-stu-id="a32ac-161">An attempt was made to create a Locator with the specified Id already used.</span></span>
* <span data-ttu-id="a32ac-162">多個 IngestManifestFile 具有 IngestManifest 中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="a32ac-162">More than one IngestManifestFile has the specified name within the IngestManifest.</span></span>
* <span data-ttu-id="a32ac-163">嘗試將第二個儲存體加密 ContentKey 連結至儲存體加密資產。</span><span class="sxs-lookup"><span data-stu-id="a32ac-163">An attempt was made to link a second storage encryption ContentKey to the storage-encrypted Asset.</span></span>
* <span data-ttu-id="a32ac-164">嘗試將相同的 ContentKey 連結到資產。</span><span class="sxs-lookup"><span data-stu-id="a32ac-164">An attempt was made to link the same ContentKey to the Asset.</span></span>
* <span data-ttu-id="a32ac-165">嘗試建立資產的定位器，其儲存體容器已遺失或已不再與資產相關聯。</span><span class="sxs-lookup"><span data-stu-id="a32ac-165">An attempt was made to create a locator to an Asset whose storage container is missing or is no longer associated with the Asset.</span></span>
* <span data-ttu-id="a32ac-166">嘗試建立資產的定位器，該資產已經有 5 個正在使用中的定位器。</span><span class="sxs-lookup"><span data-stu-id="a32ac-166">An attempt was made to create a locator to an Asset which already has 5 locators in use.</span></span> <span data-ttu-id="a32ac-167">(Azure 儲存體強制一個儲存體容器上有五個共用存取原則的限制。)</span><span class="sxs-lookup"><span data-stu-id="a32ac-167">(Azure Storage enforces the limit of five shared access policies on one storage container.)</span></span>
* <span data-ttu-id="a32ac-168">將資產的儲存體帳戶連結到 IngestManifestAsset，與父項 IngestManifest 所使用的儲存體帳戶不相同。</span><span class="sxs-lookup"><span data-stu-id="a32ac-168">Linking storage account of an Asset to an IngestManifestAsset is not the same as the storage account used by the parent IngestManifest.</span></span>  

## <a name="500-internal-server-error"></a><span data-ttu-id="a32ac-169">500 內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="a32ac-169">500 Internal Server Error</span></span>
<span data-ttu-id="a32ac-170">在處理要求時，媒體服務遇到錯誤，而導致無法繼續處理。</span><span class="sxs-lookup"><span data-stu-id="a32ac-170">During the processing of the request, Media Services encounters some error that prevents the processing from continuing.</span></span> <span data-ttu-id="a32ac-171">這可能是下列其中一個原因所造成：</span><span class="sxs-lookup"><span data-stu-id="a32ac-171">This could be due to one of the following reasons:</span></span>

* <span data-ttu-id="a32ac-172">無法建立資產或作業，因為媒體服務帳戶的服務配額資訊暫時無法使用。</span><span class="sxs-lookup"><span data-stu-id="a32ac-172">Creating an Asset or Job fails because the Media Services account's service quota information is temporarily unavailable.</span></span>
* <span data-ttu-id="a32ac-173">無法建立資產或 IngestManifest blob 儲存體容器，因為帳戶的儲存體帳戶資訊暫時無法使用。</span><span class="sxs-lookup"><span data-stu-id="a32ac-173">Creating an Asset or IngestManifest blob storage container fails because the account's storage account information is temporarily unavailable.</span></span>
* <span data-ttu-id="a32ac-174">其他未預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a32ac-174">Other unexpected error.</span></span>

## <a name="503-service-unavailable"></a><span data-ttu-id="a32ac-175">503 服務無法使用</span><span class="sxs-lookup"><span data-stu-id="a32ac-175">503 Service Unavailable</span></span>
<span data-ttu-id="a32ac-176">伺服器目前無法接收要求。</span><span class="sxs-lookup"><span data-stu-id="a32ac-176">The server is currently unable to receive requests.</span></span> <span data-ttu-id="a32ac-177">此錯誤可能是由於對服務的大量要求所造成。</span><span class="sxs-lookup"><span data-stu-id="a32ac-177">This error may be caused by excessive requests to the service.</span></span> <span data-ttu-id="a32ac-178">媒體服務節流機制會針對向服務發出過多要求的應用程式限制資源使用量。</span><span class="sxs-lookup"><span data-stu-id="a32ac-178">Media Services throttling mechanism restricts the resource usage for applications that make excessive request to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="a32ac-179">請檢查錯誤訊息和錯誤代碼字串，以取得您得到 503 錯誤原因的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a32ac-179">Check the error message and error code string to get more detailed information about the reason you got the 503 error.</span></span> <span data-ttu-id="a32ac-180">此錯誤不一定表示節流。</span><span class="sxs-lookup"><span data-stu-id="a32ac-180">This error does not always mean throttling.</span></span>
> 
> 

<span data-ttu-id="a32ac-181">可能的狀態描述為︰</span><span class="sxs-lookup"><span data-stu-id="a32ac-181">Possible status descriptions are:</span></span>

* <span data-ttu-id="a32ac-182">「伺服器忙碌中。</span><span class="sxs-lookup"><span data-stu-id="a32ac-182">"Server is busy.</span></span> <span data-ttu-id="a32ac-183">先前執行此類型的要求超過 {0} 秒。」</span><span class="sxs-lookup"><span data-stu-id="a32ac-183">Previous runs of this type of request took more than {0} seconds."</span></span>
* <span data-ttu-id="a32ac-184">「伺服器忙碌中。</span><span class="sxs-lookup"><span data-stu-id="a32ac-184">"Server is busy.</span></span> <span data-ttu-id="a32ac-185">每秒可以節流超過 {0} 個要求。」</span><span class="sxs-lookup"><span data-stu-id="a32ac-185">More than {0} requests per second can be throttled."</span></span>
* <span data-ttu-id="a32ac-186">「伺服器忙碌中。</span><span class="sxs-lookup"><span data-stu-id="a32ac-186">"Server is busy.</span></span> <span data-ttu-id="a32ac-187">{1} 秒內可以節流超過 {0} 個要求。」</span><span class="sxs-lookup"><span data-stu-id="a32ac-187">More than {0} requests within {1} seconds can be throttled."</span></span>

<span data-ttu-id="a32ac-188">若要處理此錯誤，我們建議使用指數輪詢重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="a32ac-188">To handle this error, we recommend using exponential back-off retry logic.</span></span> <span data-ttu-id="a32ac-189">這表示在連續錯誤回應的重試之間使用越來越久的等候。</span><span class="sxs-lookup"><span data-stu-id="a32ac-189">That means using progressively longer waits between retries for consecutive error responses.</span></span>  <span data-ttu-id="a32ac-190">如需詳細資訊，請參閱[暫時性錯誤處理應用程式區塊](https://msdn.microsoft.com/library/hh680905.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a32ac-190">For more information, see [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="a32ac-191">如果您使用 [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master)，已由 SDK 實作 503 錯誤的重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="a32ac-191">If you are using [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), the retry logic for the 503 error has been implemented by the SDK.</span></span>  
> 
> 

## <a name="see-also"></a><span data-ttu-id="a32ac-192">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a32ac-192">See Also</span></span>
[<span data-ttu-id="a32ac-193">媒體服務管理錯誤代碼</span><span class="sxs-lookup"><span data-stu-id="a32ac-193">Media Services Management Error Codes</span></span>](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a><span data-ttu-id="a32ac-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a32ac-194">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a32ac-195">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="a32ac-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

