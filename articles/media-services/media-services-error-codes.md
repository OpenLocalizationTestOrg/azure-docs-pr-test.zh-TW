---
title: "媒體服務錯誤碼 aaaAzure |Microsoft 文件"
description: "hello 主題提供 Azure Media Services 錯誤碼的概觀。"
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
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a><span data-ttu-id="023b5-103">Azure 媒體服務錯誤代碼</span><span class="sxs-lookup"><span data-stu-id="023b5-103">Azure Media Services error codes</span></span>
<span data-ttu-id="023b5-104">使用 Microsoft Azure 媒體服務時，可能會從根據問題，例如驗證權杖過期 Media Services 中不支援的 tooactions hello 服務收到 HTTP 錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="023b5-104">When using Microsoft Azure Media Services, you may receive HTTP error codes from hello service depending on issues such as authentication tokens expiring tooactions that are not supported in Media Services.</span></span> <span data-ttu-id="023b5-105">hello 以下是一份**HTTP 錯誤碼**，可能會傳回由 Media Services 和 hello 可能會導致它們。</span><span class="sxs-lookup"><span data-stu-id="023b5-105">hello following is a list of **HTTP error codes** that may be returned by Media Services and hello possible causes for them.</span></span>  

## <a name="400-bad-request"></a><span data-ttu-id="023b5-106">400 不正確的要求</span><span class="sxs-lookup"><span data-stu-id="023b5-106">400 Bad Request</span></span>
<span data-ttu-id="023b5-107">hello 要求包含無效的資訊，但遭到拒絕，因為下列原因 hello 的 tooone:</span><span class="sxs-lookup"><span data-stu-id="023b5-107">hello request contains invalid information and is rejected due tooone of hello following reasons:</span></span>

* <span data-ttu-id="023b5-108">指定了不支援的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="023b5-108">An unsupported API version is specified.</span></span> <span data-ttu-id="023b5-109">Hello 最新版本，請參閱[Media Services REST API 開發的安裝程式](media-services-rest-how-to-use.md)。</span><span class="sxs-lookup"><span data-stu-id="023b5-109">For hello most current version, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="023b5-110">未指定的媒體服務的 hello API 版本。</span><span class="sxs-lookup"><span data-stu-id="023b5-110">hello API version of Media Services is not specified.</span></span> <span data-ttu-id="023b5-111">如需如何 toospecify hello API 版本資訊，請參閱[媒體服務作業的 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="023b5-111">For information on how toospecify hello API version, see [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="023b5-112">如果您使用 hello.NET 或 Java Sdk tooconnect tooMedia hello API 版本的服務會為您指定每當您再試一次，並執行某些動作，對媒體服務。</span><span class="sxs-lookup"><span data-stu-id="023b5-112">If you are using hello .NET or Java SDKs tooconnect tooMedia Services, hello API version is specified for you whenever you try and perform some action against Media Services.</span></span>
  > 
  > 
* <span data-ttu-id="023b5-113">已指定未定義的屬性。</span><span class="sxs-lookup"><span data-stu-id="023b5-113">An undefined property has been specified.</span></span> <span data-ttu-id="023b5-114">hello 屬性名稱已在 hello 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="023b5-114">hello property name is in hello error message.</span></span> <span data-ttu-id="023b5-115">只能指定屬於指定實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="023b5-115">Only those properties that are members of a given entity can be specified.</span></span> <span data-ttu-id="023b5-116">請參閱 [Azure 媒體服務 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)，以取得實體及其屬性的清單。</span><span class="sxs-lookup"><span data-stu-id="023b5-116">See [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) for a list of entities and their properties.</span></span>
* <span data-ttu-id="023b5-117">已指定無效的屬性值。</span><span class="sxs-lookup"><span data-stu-id="023b5-117">An invalid property value has been specified.</span></span> <span data-ttu-id="023b5-118">hello 屬性名稱已在 hello 錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="023b5-118">hello property name is in hello error message.</span></span> <span data-ttu-id="023b5-119">請參閱 hello 前一個連結的有效屬性類型和其值。</span><span class="sxs-lookup"><span data-stu-id="023b5-119">See hello previous link for valid property types and their values.</span></span>
* <span data-ttu-id="023b5-120">遺漏必要的屬性值。</span><span class="sxs-lookup"><span data-stu-id="023b5-120">A property value is missing and is required.</span></span>
* <span data-ttu-id="023b5-121">部分指定 hello URL 包含不正確的值。</span><span class="sxs-lookup"><span data-stu-id="023b5-121">Part of hello URL specified contains a bad value.</span></span>
* <span data-ttu-id="023b5-122">嘗試進行 tooupdate WriteOnce 屬性。</span><span class="sxs-lookup"><span data-stu-id="023b5-122">An attempt was made tooupdate a WriteOnce property.</span></span>
* <span data-ttu-id="023b5-123">嘗試進行 toocreate 具有未指定，或無法判斷主要 AssetFile 的輸入的資產的工作。</span><span class="sxs-lookup"><span data-stu-id="023b5-123">An attempt was made toocreate a Job that has an input Asset with a primary AssetFile that was not specified or could not be determined.</span></span>
* <span data-ttu-id="023b5-124">嘗試進行 tooupdate SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="023b5-124">An attempt was made tooupdate a SAS Locator.</span></span> <span data-ttu-id="023b5-125">僅能建立或刪除 SAS 定位器。</span><span class="sxs-lookup"><span data-stu-id="023b5-125">SAS locators can only be created or deleted.</span></span> <span data-ttu-id="023b5-126">可以更新串流定位器。</span><span class="sxs-lookup"><span data-stu-id="023b5-126">Streaming locators can be updated.</span></span> <span data-ttu-id="023b5-127">如需詳細資訊，請參閱[定位器](https://docs.microsoft.com/rest/api/media/operations/locator)。</span><span class="sxs-lookup"><span data-stu-id="023b5-127">For more information, see [Locators](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>
* <span data-ttu-id="023b5-128">不支援的作業或查詢已提交。</span><span class="sxs-lookup"><span data-stu-id="023b5-128">An unsupported operation or query was submitted.</span></span>

## <a name="401-unauthorized"></a><span data-ttu-id="023b5-129">401 未經授權</span><span class="sxs-lookup"><span data-stu-id="023b5-129">401 Unauthorized</span></span>
<span data-ttu-id="023b5-130">（之前會授權它），無法驗證 hello 要求到期 tooone 的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="023b5-130">hello request could not be authenticated (before it can be authorized) due tooone of hello following reasons:</span></span>

* <span data-ttu-id="023b5-131">遺失驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="023b5-131">Missing authentication header.</span></span>
* <span data-ttu-id="023b5-132">不正確的驗證標頭值。</span><span class="sxs-lookup"><span data-stu-id="023b5-132">Bad authentication header value.</span></span>
  * <span data-ttu-id="023b5-133">hello token 已過期。</span><span class="sxs-lookup"><span data-stu-id="023b5-133">hello token has expired.</span></span> 
  * <span data-ttu-id="023b5-134">hello token 包含無效的簽章。</span><span class="sxs-lookup"><span data-stu-id="023b5-134">hello token contains an invalid signature.</span></span>

## <a name="403-forbidden"></a><span data-ttu-id="023b5-135">403 禁止</span><span class="sxs-lookup"><span data-stu-id="023b5-135">403 Forbidden</span></span>
<span data-ttu-id="023b5-136">不允許到期 hello 要求 tooone 的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="023b5-136">hello request is not allowed due tooone of hello following reasons:</span></span>

* <span data-ttu-id="023b5-137">找不到 hello Media Services 帳戶，或已刪除。</span><span class="sxs-lookup"><span data-stu-id="023b5-137">hello Media Services account cannot be found or has been deleted.</span></span>
* <span data-ttu-id="023b5-138">hello Media Services 帳戶已停用，且 hello 要求類型不是 HTTP GET。</span><span class="sxs-lookup"><span data-stu-id="023b5-138">hello Media Services account is disabled and hello request type is not HTTP GET.</span></span> <span data-ttu-id="023b5-139">服務作業也會傳回 403 回應。</span><span class="sxs-lookup"><span data-stu-id="023b5-139">Service operations will return a 403 response as well.</span></span>
* <span data-ttu-id="023b5-140">hello 驗證權杖不含 hello 使用者認證資訊： AccountName 及/或訂用帳戶 Id。</span><span class="sxs-lookup"><span data-stu-id="023b5-140">hello authentication token does not contain hello user’s credential information: AccountName and/or SubscriptionId.</span></span> <span data-ttu-id="023b5-141">Hello Azure 管理入口網站中，媒體服務帳戶，您可以在 hello Media Services UI 延伸模組中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="023b5-141">You can find this information in hello Media Services UI extension for your Media Services account in hello Azure Management Portal.</span></span>
* <span data-ttu-id="023b5-142">無法存取 hello 的資源。</span><span class="sxs-lookup"><span data-stu-id="023b5-142">hello resource cannot be accessed.</span></span>
  
  * <span data-ttu-id="023b5-143">嘗試進行 toouse 不適用於您的 Media Services 帳戶 mediaprocessor 」 轉換。</span><span class="sxs-lookup"><span data-stu-id="023b5-143">An attempt was made toouse a MediaProcessor that is not available for your Media Services account.</span></span>
  * <span data-ttu-id="023b5-144">已嘗試的 tooupdate JobTemplate 定義由 Media Services。</span><span class="sxs-lookup"><span data-stu-id="023b5-144">An attempt was made tooupdate a JobTemplate defined by Media Services.</span></span>
  * <span data-ttu-id="023b5-145">嘗試進行 toooverwrite 某些其他媒體服務帳戶的定位器。</span><span class="sxs-lookup"><span data-stu-id="023b5-145">An attempt was made toooverwrite some other Media Services account's Locator.</span></span>
  * <span data-ttu-id="023b5-146">嘗試進行 toooverwrite 某些其他媒體服務帳戶的 ContentKey。</span><span class="sxs-lookup"><span data-stu-id="023b5-146">An attempt was made toooverwrite some other Media Services account's ContentKey.</span></span>
* <span data-ttu-id="023b5-147">無法建立 hello 資源，因為 tooa hello Media Services 帳戶已達到的服務配額。</span><span class="sxs-lookup"><span data-stu-id="023b5-147">hello resource could not be created due tooa service quota that was reached for hello Media Services account.</span></span> <span data-ttu-id="023b5-148">如需有關 hello 服務配額的詳細資訊，請參閱[配額和限制](media-services-quotas-and-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="023b5-148">For more information on hello service quotas, see [Quotas and Limitations](media-services-quotas-and-limitations.md).</span></span>

## <a name="404-not-found"></a><span data-ttu-id="023b5-149">404 找不到</span><span class="sxs-lookup"><span data-stu-id="023b5-149">404 Not Found</span></span>
<span data-ttu-id="023b5-150">在資源上不允許 hello 要求到期 tooone 的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="023b5-150">hello request is not allowed on a resource due tooone of hello following reasons:</span></span>

* <span data-ttu-id="023b5-151">嘗試進行 tooupdate 實體不存在。</span><span class="sxs-lookup"><span data-stu-id="023b5-151">An attempt was made tooupdate an entity that does not exist.</span></span>
* <span data-ttu-id="023b5-152">嘗試進行 toodelete 實體不存在。</span><span class="sxs-lookup"><span data-stu-id="023b5-152">An attempt was made toodelete an entity that does not exist.</span></span>
* <span data-ttu-id="023b5-153">嘗試進行 toocreate 連結 tooan 實體不存在的實體。</span><span class="sxs-lookup"><span data-stu-id="023b5-153">An attempt was made toocreate an entity that links tooan entity that does not exist.</span></span>
* <span data-ttu-id="023b5-154">嘗試進行 tooGET 實體不存在。</span><span class="sxs-lookup"><span data-stu-id="023b5-154">An attempt was made tooGET an entity that does not exist.</span></span>
* <span data-ttu-id="023b5-155">嘗試進行 toospecify 未與 hello Media Services 帳戶相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="023b5-155">An attempt was made toospecify a storage account that is not associated with hello Media Services account.</span></span>  

## <a name="409-conflict"></a><span data-ttu-id="023b5-156">409 衝突</span><span class="sxs-lookup"><span data-stu-id="023b5-156">409 Conflict</span></span>
<span data-ttu-id="023b5-157">不允許到期 hello 要求 tooone 的 hello 下列原因：</span><span class="sxs-lookup"><span data-stu-id="023b5-157">hello request is not allowed due tooone of hello following reasons:</span></span>

* <span data-ttu-id="023b5-158">一個以上的 AssetFile 有 hello hello 資產內指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="023b5-158">More than one AssetFile has hello specified name within hello Asset.</span></span>
* <span data-ttu-id="023b5-159">已嘗試第二個 toocreate 主要 AssetFile hello 資產中的。</span><span class="sxs-lookup"><span data-stu-id="023b5-159">An attempt was made toocreate a second primary AssetFile within hello Asset.</span></span>
* <span data-ttu-id="023b5-160">已嘗試 toocreate hello 與 ContentKey 指定已在使用中的識別碼。</span><span class="sxs-lookup"><span data-stu-id="023b5-160">An attempt was made toocreate a ContentKey with hello specified Id already used.</span></span>
* <span data-ttu-id="023b5-161">已嘗試 toocreate 以 hello 的定位器指定已在使用中的識別碼。</span><span class="sxs-lookup"><span data-stu-id="023b5-161">An attempt was made toocreate a Locator with hello specified Id already used.</span></span>
* <span data-ttu-id="023b5-162">一個以上的 IngestManifestFile 有 hello hello IngestManifest 中指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="023b5-162">More than one IngestManifestFile has hello specified name within hello IngestManifest.</span></span>
* <span data-ttu-id="023b5-163">嘗試進行第二個儲存體加密 ContentKey toohello toolink 儲存體加密資產。</span><span class="sxs-lookup"><span data-stu-id="023b5-163">An attempt was made toolink a second storage encryption ContentKey toohello storage-encrypted Asset.</span></span>
* <span data-ttu-id="023b5-164">已嘗試 toolink hello 相同 ContentKey toohello 資產。</span><span class="sxs-lookup"><span data-stu-id="023b5-164">An attempt was made toolink hello same ContentKey toohello Asset.</span></span>
* <span data-ttu-id="023b5-165">已嘗試的 toocreate 與 hello 資產相關聯的定位器 tooan 資產的儲存體容器遺漏或已不存在。</span><span class="sxs-lookup"><span data-stu-id="023b5-165">An attempt was made toocreate a locator tooan Asset whose storage container is missing or is no longer associated with hello Asset.</span></span>
* <span data-ttu-id="023b5-166">嘗試進行 toocreate 定位器 tooan 已經有使用中的 5 定位器的資產。</span><span class="sxs-lookup"><span data-stu-id="023b5-166">An attempt was made toocreate a locator tooan Asset which already has 5 locators in use.</span></span> <span data-ttu-id="023b5-167">（azure 儲存體會強制執行上一個儲存體容器的五個共用的存取原則的 hello 的限制）。</span><span class="sxs-lookup"><span data-stu-id="023b5-167">(Azure Storage enforces hello limit of five shared access policies on one storage container.)</span></span>
* <span data-ttu-id="023b5-168">連結的資產 tooan IngestManifestAsset 的儲存體帳戶不是 hello 父系 IngestManifest hello 相同 hello 儲存體帳戶使用。</span><span class="sxs-lookup"><span data-stu-id="023b5-168">Linking storage account of an Asset tooan IngestManifestAsset is not hello same as hello storage account used by hello parent IngestManifest.</span></span>  

## <a name="500-internal-server-error"></a><span data-ttu-id="023b5-169">500 內部伺服器錯誤</span><span class="sxs-lookup"><span data-stu-id="023b5-169">500 Internal Server Error</span></span>
<span data-ttu-id="023b5-170">Hello hello 要求處理期間 Media Services 會遇到錯誤，阻礙 hello 處理無法繼續。</span><span class="sxs-lookup"><span data-stu-id="023b5-170">During hello processing of hello request, Media Services encounters some error that prevents hello processing from continuing.</span></span> <span data-ttu-id="023b5-171">這可能是因下列原因 hello 的 tooone:</span><span class="sxs-lookup"><span data-stu-id="023b5-171">This could be due tooone of hello following reasons:</span></span>

* <span data-ttu-id="023b5-172">建立資產或作業就會失敗，因為暫時無法使用 hello Media Services 帳戶的服務配額資訊。</span><span class="sxs-lookup"><span data-stu-id="023b5-172">Creating an Asset or Job fails because hello Media Services account's service quota information is temporarily unavailable.</span></span>
* <span data-ttu-id="023b5-173">建立資產或 IngestManifest blob 儲存體容器就會失敗，因為暫時無法使用 hello 帳戶的儲存體帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="023b5-173">Creating an Asset or IngestManifest blob storage container fails because hello account's storage account information is temporarily unavailable.</span></span>
* <span data-ttu-id="023b5-174">其他未預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="023b5-174">Other unexpected error.</span></span>

## <a name="503-service-unavailable"></a><span data-ttu-id="023b5-175">503 服務無法使用</span><span class="sxs-lookup"><span data-stu-id="023b5-175">503 Service Unavailable</span></span>
<span data-ttu-id="023b5-176">目前無法 tooreceive 要求 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="023b5-176">hello server is currently unable tooreceive requests.</span></span> <span data-ttu-id="023b5-177">這個錯誤可能是過多要求 toohello 服務所造成。</span><span class="sxs-lookup"><span data-stu-id="023b5-177">This error may be caused by excessive requests toohello service.</span></span> <span data-ttu-id="023b5-178">媒體服務節流機制會限制應用程式而言過多要求 toohello 服務 hello 資源使用的狀況。</span><span class="sxs-lookup"><span data-stu-id="023b5-178">Media Services throttling mechanism restricts hello resource usage for applications that make excessive request toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="023b5-179">核取 hello 錯誤訊息和錯誤程式碼字串 tooget 所得的 hello 原因的相關資訊的詳細 hello 503 錯誤。</span><span class="sxs-lookup"><span data-stu-id="023b5-179">Check hello error message and error code string tooget more detailed information about hello reason you got hello 503 error.</span></span> <span data-ttu-id="023b5-180">此錯誤不一定表示節流。</span><span class="sxs-lookup"><span data-stu-id="023b5-180">This error does not always mean throttling.</span></span>
> 
> 

<span data-ttu-id="023b5-181">可能的狀態描述為︰</span><span class="sxs-lookup"><span data-stu-id="023b5-181">Possible status descriptions are:</span></span>

* <span data-ttu-id="023b5-182">「伺服器忙碌中。</span><span class="sxs-lookup"><span data-stu-id="023b5-182">"Server is busy.</span></span> <span data-ttu-id="023b5-183">先前執行此類型的要求超過 {0} 秒。」</span><span class="sxs-lookup"><span data-stu-id="023b5-183">Previous runs of this type of request took more than {0} seconds."</span></span>
* <span data-ttu-id="023b5-184">「伺服器忙碌中。</span><span class="sxs-lookup"><span data-stu-id="023b5-184">"Server is busy.</span></span> <span data-ttu-id="023b5-185">每秒可以節流超過 {0} 個要求。」</span><span class="sxs-lookup"><span data-stu-id="023b5-185">More than {0} requests per second can be throttled."</span></span>
* <span data-ttu-id="023b5-186">「伺服器忙碌中。</span><span class="sxs-lookup"><span data-stu-id="023b5-186">"Server is busy.</span></span> <span data-ttu-id="023b5-187">{1} 秒內可以節流超過 {0} 個要求。」</span><span class="sxs-lookup"><span data-stu-id="023b5-187">More than {0} requests within {1} seconds can be throttled."</span></span>

<span data-ttu-id="023b5-188">toohandle 這個錯誤，建議使用指數型撤退重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="023b5-188">toohandle this error, we recommend using exponential back-off retry logic.</span></span> <span data-ttu-id="023b5-189">這表示在連續錯誤回應的重試之間使用越來越久的等候。</span><span class="sxs-lookup"><span data-stu-id="023b5-189">That means using progressively longer waits between retries for consecutive error responses.</span></span>  <span data-ttu-id="023b5-190">如需詳細資訊，請參閱[暫時性錯誤處理應用程式區塊](https://msdn.microsoft.com/library/hh680905.aspx)。</span><span class="sxs-lookup"><span data-stu-id="023b5-190">For more information, see [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="023b5-191">如果您使用[Azure Media Services SDK for.Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master)，已由 hello SDK 實作 hello 503 錯誤的 hello 重試邏輯。</span><span class="sxs-lookup"><span data-stu-id="023b5-191">If you are using [Azure Media Services SDK for .Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), hello retry logic for hello 503 error has been implemented by hello SDK.</span></span>  
> 
> 

## <a name="see-also"></a><span data-ttu-id="023b5-192">另請參閱</span><span class="sxs-lookup"><span data-stu-id="023b5-192">See Also</span></span>
[<span data-ttu-id="023b5-193">媒體服務管理錯誤代碼</span><span class="sxs-lookup"><span data-stu-id="023b5-193">Media Services Management Error Codes</span></span>](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a><span data-ttu-id="023b5-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="023b5-194">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="023b5-195">提供意見反應</span><span class="sxs-lookup"><span data-stu-id="023b5-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

