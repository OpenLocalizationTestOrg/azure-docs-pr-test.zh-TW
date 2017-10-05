---
title: "Azure CDN 規則引擎功能 | Microsoft Docs"
description: "Azure CDN 規則引擎比對條件和功能的參考文件。"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 6703247aa8b4a6d53ff22ea2d4f22eb4a746e370
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-features"></a><span data-ttu-id="3d02c-103">Azure CDN 規則引擎功能</span><span class="sxs-lookup"><span data-stu-id="3d02c-103">Azure CDN rules engine features</span></span>
<span data-ttu-id="3d02c-104">本主題會針對 Azure 內容傳遞網路 (CDN) [規則引擎](cdn-rules-engine.md)列出可用功能的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="3d02c-104">This topic lists detailed descriptions of the available features for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="3d02c-105">規則的第三個部分是功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-105">The third part of a rule is the feature.</span></span> <span data-ttu-id="3d02c-106">功能會定義動作類型，其將套用到透過一組比對條件來識別的要求類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-106">A feature defines the type of action that will be applied to the type of request identified by a set of match conditions.</span></span>

## <a name="access"></a><span data-ttu-id="3d02c-107">Access</span><span class="sxs-lookup"><span data-stu-id="3d02c-107">Access</span></span>

<span data-ttu-id="3d02c-108">這些功能是設計來控制內容的存取權。</span><span class="sxs-lookup"><span data-stu-id="3d02c-108">These features are designed to control access to content.</span></span>


<span data-ttu-id="3d02c-109">名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-109">Name</span></span> | <span data-ttu-id="3d02c-110">目的</span><span class="sxs-lookup"><span data-stu-id="3d02c-110">Purpose</span></span>
-----|--------
<span data-ttu-id="3d02c-111">拒絕存取</span><span class="sxs-lookup"><span data-stu-id="3d02c-111">Deny Access</span></span> | <span data-ttu-id="3d02c-112">判斷所有要求是否已遭拒絕且含有 [403 禁止] 回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-112">Determines whether all requests are rejected with a 403 Forbidden response.</span></span>
<span data-ttu-id="3d02c-113">權杖驗證</span><span class="sxs-lookup"><span data-stu-id="3d02c-113">Token Auth</span></span> | <span data-ttu-id="3d02c-114">判斷是否要將權杖型驗證套用到要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-114">Determines whether Token-Based Authentication will be applied to a request.</span></span>
<span data-ttu-id="3d02c-115">權杖驗證拒絕代碼</span><span class="sxs-lookup"><span data-stu-id="3d02c-115">Token Auth Denial Code</span></span> | <span data-ttu-id="3d02c-116">判斷在要求因權杖型驗證而遭到拒絕時將傳回給使用者的回應類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-116">Determines the type of response that will be returned to a user when a request is denied due to Token-Based Authentication.</span></span>
<span data-ttu-id="3d02c-117">權杖驗證會忽略 URL 的大小寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-117">Token Auth Ignore URL Case</span></span> | <span data-ttu-id="3d02c-118">判斷透過權杖型驗證所做的 URL 比較是否會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="3d02c-118">Determines whether URL comparisons made by Token-Based Authentication will be case-sensitive.</span></span>
<span data-ttu-id="3d02c-119">權杖驗證參數</span><span class="sxs-lookup"><span data-stu-id="3d02c-119">Token Auth Parameter</span></span> | <span data-ttu-id="3d02c-120">判斷是否應將權杖型驗證查詢字串參數重新命名。</span><span class="sxs-lookup"><span data-stu-id="3d02c-120">Determines whether the Token-Based Authentication query string parameter should be renamed.</span></span>

### <a name="deny-access"></a><span data-ttu-id="3d02c-121">拒絕存取</span><span class="sxs-lookup"><span data-stu-id="3d02c-121">Deny Access</span></span>
<span data-ttu-id="3d02c-122">**目的**：判斷所有要求是否已遭拒且含有 [403 禁止] 回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-122">**Purpose**: Determines whether all requests are rejected with a 403 Forbidden response.</span></span>

<span data-ttu-id="3d02c-123">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-123">Value</span></span> | <span data-ttu-id="3d02c-124">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-124">Result</span></span>
------|-------
<span data-ttu-id="3d02c-125">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-125">Enabled</span></span>| <span data-ttu-id="3d02c-126">導致所有滿足比對準則的要求遭拒，且具有 [403 禁止] 回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-126">Causes all requests that satisfy the matching criteria to be rejected with a 403 Forbidden response.</span></span>
<span data-ttu-id="3d02c-127">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-127">Disabled</span></span>| <span data-ttu-id="3d02c-128">還原預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-128">Restores the default behavior.</span></span> <span data-ttu-id="3d02c-129">預設行為是讓原始伺服器能夠判斷將傳回的回應類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-129">The default behavior is to allow the origin server to determine the type of response that will be returned.</span></span>

<span data-ttu-id="3d02c-130">**預設行為**：已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-130">**Default Behavior**: Disabled</span></span>

> [!TIP]
   > <span data-ttu-id="3d02c-131">此功能的可能用法之一是將它關聯至 [要求標頭] 比對條件，以封鎖存取使用內嵌連結連至您內容的 HTTP 推薦者。</span><span class="sxs-lookup"><span data-stu-id="3d02c-131">One possible use for this feature is to associate it with a Request Header match condition to block access to HTTP referrers that are using inline links to your content.</span></span>

### <a name="token-auth"></a><span data-ttu-id="3d02c-132">權杖驗證</span><span class="sxs-lookup"><span data-stu-id="3d02c-132">Token Auth</span></span>
<span data-ttu-id="3d02c-133">**目的**：判斷是否要將權杖型驗證套用到要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-133">**Purpose:** Determines whether Token-Based Authentication will be applied to a request.</span></span>

<span data-ttu-id="3d02c-134">如果啟用權杖型驗證，則只會接受提供加密權杖且符合該權杖所指定需求的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-134">If Token-Based Authentication is enabled, then only requests that provide an encrypted token and comply to the requirements specified by that token will be honored.</span></span>

<span data-ttu-id="3d02c-135">將用於加密和解密權杖值的加密金鑰，是根據 [權杖驗證] 頁面上的 [主要金鑰] 和 [備份金鑰] 選項來決定。</span><span class="sxs-lookup"><span data-stu-id="3d02c-135">The encryption key that will be used to encrypt and decrypt token values is determined by the Primary Key and the Backup Key options on the Token Auth page.</span></span> <span data-ttu-id="3d02c-136">請記住，加密金鑰是特定平台的。</span><span class="sxs-lookup"><span data-stu-id="3d02c-136">Keep in mind that encryption keys are platform-specific.</span></span>

<span data-ttu-id="3d02c-137">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-137">Value</span></span> | <span data-ttu-id="3d02c-138">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-138">Result</span></span>
------|---------
<span data-ttu-id="3d02c-139">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-139">Enabled</span></span> | <span data-ttu-id="3d02c-140">使用權杖型驗證保護要求的內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-140">Protects the requested content with Token-Based Authentication.</span></span> <span data-ttu-id="3d02c-141">只接受來自用戶端且可提供有效權杖並符合其需求的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-141">Only requests from clients that provide a valid token and meet its requirements will be honored.</span></span> <span data-ttu-id="3d02c-142">FTP 交易會從權杖型驗證中排除。</span><span class="sxs-lookup"><span data-stu-id="3d02c-142">FTP transactions are excluded from Token-Based Authentication.</span></span>
<span data-ttu-id="3d02c-143">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-143">Disabled</span></span>| <span data-ttu-id="3d02c-144">還原預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-144">Restores the default behavior.</span></span> <span data-ttu-id="3d02c-145">預設行為是讓您的權杖型驗證組態能夠判斷要求是否將會受到保護。</span><span class="sxs-lookup"><span data-stu-id="3d02c-145">The default behavior is to allow your Token-Based Authentication configuration to determine whether a request will be secured.</span></span>

<span data-ttu-id="3d02c-146">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-146">**Default Behavior:** Disabled.</span></span>

###<a name="token-auth-denial-code"></a><span data-ttu-id="3d02c-147">權杖驗證拒絕代碼</span><span class="sxs-lookup"><span data-stu-id="3d02c-147">Token Auth Denial Code</span></span>
<span data-ttu-id="3d02c-148">**目的：**判斷在要求因權杖型驗證而遭到拒絕時將傳回給使用者的回應類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-148">**Purpose:** Determines the type of response that will be returned to a user when a request is denied due to Token-Based Authentication.</span></span>

<span data-ttu-id="3d02c-149">以下列出可用的回應碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-149">The available response codes are listed below.</span></span>

<span data-ttu-id="3d02c-150">回應碼</span><span class="sxs-lookup"><span data-stu-id="3d02c-150">Response Code</span></span>|<span data-ttu-id="3d02c-151">回應名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-151">Response Name</span></span>|<span data-ttu-id="3d02c-152">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-152">Description</span></span>
----------------|-----------|--------
<span data-ttu-id="3d02c-153">301</span><span class="sxs-lookup"><span data-stu-id="3d02c-153">301</span></span>|<span data-ttu-id="3d02c-154">已永久移動</span><span class="sxs-lookup"><span data-stu-id="3d02c-154">Moved Permanently</span></span>|<span data-ttu-id="3d02c-155">此狀態碼會將未經授權的使用者重新導向至位置標頭中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-155">This status code redirects unauthorized users to the URL specified in the Location header.</span></span>
<span data-ttu-id="3d02c-156">302</span><span class="sxs-lookup"><span data-stu-id="3d02c-156">302</span></span>|<span data-ttu-id="3d02c-157">已找到</span><span class="sxs-lookup"><span data-stu-id="3d02c-157">Found</span></span>|<span data-ttu-id="3d02c-158">此狀態碼會將未經授權的使用者重新導向至位置標頭中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-158">This status code redirects unauthorized users to the URL specified in the Location header.</span></span> <span data-ttu-id="3d02c-159">此狀態碼是執行重新導向的業界標準方法。</span><span class="sxs-lookup"><span data-stu-id="3d02c-159">This status code is the industry standard method of performing a redirect.</span></span>
<span data-ttu-id="3d02c-160">307</span><span class="sxs-lookup"><span data-stu-id="3d02c-160">307</span></span>|<span data-ttu-id="3d02c-161">暫時重新導向</span><span class="sxs-lookup"><span data-stu-id="3d02c-161">Temporary Redirect</span></span>|<span data-ttu-id="3d02c-162">此狀態碼會將未經授權的使用者重新導向至位置標頭中指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-162">This status code redirects unauthorized users to the URL specified in the Location header.</span></span>
<span data-ttu-id="3d02c-163">401</span><span class="sxs-lookup"><span data-stu-id="3d02c-163">401</span></span>|<span data-ttu-id="3d02c-164">未經授權</span><span class="sxs-lookup"><span data-stu-id="3d02c-164">Unauthorized</span></span>|<span data-ttu-id="3d02c-165">將此狀態碼與 WWW 驗證回應標頭相結合，讓您能夠提示使用者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-165">Combining this status code with the WWW-Authenticate response header allows you to prompt a user for authentication.</span></span>
<span data-ttu-id="3d02c-166">403</span><span class="sxs-lookup"><span data-stu-id="3d02c-166">403</span></span>|<span data-ttu-id="3d02c-167">禁止</span><span class="sxs-lookup"><span data-stu-id="3d02c-167">Forbidden</span></span>|<span data-ttu-id="3d02c-168">這是標準的 [403 禁止] 狀態訊息，未經授權的使用者將會在嘗試存取受保護的內容時看見此訊息。</span><span class="sxs-lookup"><span data-stu-id="3d02c-168">This is the standard 403 Forbidden status message that an unauthorized user will see when trying to access protected content.</span></span>
<span data-ttu-id="3d02c-169">404</span><span class="sxs-lookup"><span data-stu-id="3d02c-169">404</span></span>|<span data-ttu-id="3d02c-170">找不到檔案</span><span class="sxs-lookup"><span data-stu-id="3d02c-170">File Not Found</span></span>|<span data-ttu-id="3d02c-171">此狀態碼表示 HTTP 用戶端能夠與伺服器通訊，但找不到要求的內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-171">This status code indicates that the HTTP client was able to communicate with the server, but the requested content was not found.</span></span>

#### <a name="url-redirection"></a><span data-ttu-id="3d02c-172">URL 重新導向</span><span class="sxs-lookup"><span data-stu-id="3d02c-172">URL Redirection</span></span>

<span data-ttu-id="3d02c-173">將此功能設為傳回 3xx 狀態碼時，此功能支援將 URL 重新導向至使用者定義的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-173">This feature supports URL redirection to a user-defined URL when it is configured to return a 3xx status code.</span></span> <span data-ttu-id="3d02c-174">執行下列步驟，即可指定此使用者定義的 URL：</span><span class="sxs-lookup"><span data-stu-id="3d02c-174">This user-defined URL can be specified by performing the following steps:</span></span>

1. <span data-ttu-id="3d02c-175">針對 [權杖驗證拒絕代碼] 功能選取 3xx 回應碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-175">Select a 3xx response code for the Token Auth Denial Code feature.</span></span>
2. <span data-ttu-id="3d02c-176">從 [選用標頭名稱] 選項中選取 [位置]。</span><span class="sxs-lookup"><span data-stu-id="3d02c-176">Select "Location" from the Optional Header Name option.</span></span>
3. <span data-ttu-id="3d02c-177">將 [選用標頭值] 選項設為所需的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-177">Set the Optional Header Value option to the desired URL.</span></span>

<span data-ttu-id="3d02c-178">如果未定義適用於 3xx 狀態碼的 URL，則會將適用於 3xx 狀態碼的標準回應頁面傳回給使用者。</span><span class="sxs-lookup"><span data-stu-id="3d02c-178">If a URL is not defined for a 3xx status code, then the standard response page for a 3xx status code will be returned to the user.</span></span>

<span data-ttu-id="3d02c-179">URL 重新導向只適用於 3xx 回應碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-179">URL redirection is only applicable for 3xx response codes.</span></span>

<span data-ttu-id="3d02c-180">[選用標頭值] 選項支援英數字元、引號和空格。</span><span class="sxs-lookup"><span data-stu-id="3d02c-180">The Optional Header Value option supports alphanumeric characters, quotation marks, and spaces.</span></span>

#### <a name="authentication"></a><span data-ttu-id="3d02c-181">驗證</span><span class="sxs-lookup"><span data-stu-id="3d02c-181">Authentication</span></span>

<span data-ttu-id="3d02c-182">此功能支援的功能可在針對權杖型驗證所保護的內容回應未經授權的要求時包含 WWW-Authenticate 標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-182">This feature supports the capability to include the WWW-Authenticate header when responding to an unauthorized request for content protected by Token-Based Authentication.</span></span> <span data-ttu-id="3d02c-183">如果您的設定中已將 WWW-Authenticate 標頭設為「basic」，則會提示未經授權的使用者提供帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-183">If the WWW-Authenticate header has been set to "basic" in your configuration, then the unauthorized user will be prompted for account credentials.</span></span>

<span data-ttu-id="3d02c-184">您可以藉由執行下列步驟來完成上述組態：</span><span class="sxs-lookup"><span data-stu-id="3d02c-184">The above configuration can be achieved by performing the following steps:</span></span>

1. <span data-ttu-id="3d02c-185">針對 [權杖驗證拒絕代碼] 功能選取 [401] 做為回應碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-185">Select "401" as the response code for the Token Auth Denial Code feature.</span></span>
2. <span data-ttu-id="3d02c-186">從 [選用標頭名稱] 選項中選取 [WWW-Authenticate]。</span><span class="sxs-lookup"><span data-stu-id="3d02c-186">Select "WWW-Authenticate" from the Optional Header Name option.</span></span>
3. <span data-ttu-id="3d02c-187">將 [選用標頭值] 選項設為 [basic]。</span><span class="sxs-lookup"><span data-stu-id="3d02c-187">Set the Optional Header Value option to "basic."</span></span>

<span data-ttu-id="3d02c-188">WWW-Authenticate 標頭只適用於 401 回應碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-188">The WWW-Authenticate header is only applicable for 401 response codes.</span></span>

### <a name="token-auth-ignore-url-case"></a><span data-ttu-id="3d02c-189">權杖驗證會忽略 URL 的大小寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-189">Token Auth Ignore URL Case</span></span>
<span data-ttu-id="3d02c-190">**目的：**判斷透過權杖型驗證所做的 URL 比較是否會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="3d02c-190">**Purpose:** Determines whether URL comparisons made by Token-Based Authentication will be case-sensitive.</span></span>

<span data-ttu-id="3d02c-191">受此功能影響的參數如下：</span><span class="sxs-lookup"><span data-stu-id="3d02c-191">The parameters affected by this feature are:</span></span>

- <span data-ttu-id="3d02c-192">ec_url_allow</span><span class="sxs-lookup"><span data-stu-id="3d02c-192">ec_url_allow</span></span>
- <span data-ttu-id="3d02c-193">ec_ref_allow</span><span class="sxs-lookup"><span data-stu-id="3d02c-193">ec_ref_allow</span></span>
- <span data-ttu-id="3d02c-194">ec_ref_deny</span><span class="sxs-lookup"><span data-stu-id="3d02c-194">ec_ref_deny</span></span>

<span data-ttu-id="3d02c-195">有效值為：</span><span class="sxs-lookup"><span data-stu-id="3d02c-195">Valid values are:</span></span>

<span data-ttu-id="3d02c-196">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-196">Value</span></span>|<span data-ttu-id="3d02c-197">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-197">Result</span></span>
---|----
<span data-ttu-id="3d02c-198">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-198">Enabled</span></span>|<span data-ttu-id="3d02c-199">導致 Edge Server 會在比較權杖型驗證參數的 URL 時忽略大小寫。</span><span class="sxs-lookup"><span data-stu-id="3d02c-199">Causes our edge server to ignore case when comparing URLs for Token-Based Authentication parameters.</span></span>
<span data-ttu-id="3d02c-200">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-200">Disabled</span></span>|<span data-ttu-id="3d02c-201">還原預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-201">Restores the default behavior.</span></span> <span data-ttu-id="3d02c-202">預設行為是在進行權杖型驗證的 URL 比較時會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="3d02c-202">The default behavior is for URL comparisons for Token Authentication to be case-sensitive.</span></span>

<span data-ttu-id="3d02c-203">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-203">**Default Behavior:** Disabled.</span></span>
 
### <a name="token-auth-parameter"></a><span data-ttu-id="3d02c-204">權杖驗證參數</span><span class="sxs-lookup"><span data-stu-id="3d02c-204">Token Auth Parameter</span></span>
<span data-ttu-id="3d02c-205">**目的：**判斷是否應將權杖型驗證查詢字串參數重新命名。</span><span class="sxs-lookup"><span data-stu-id="3d02c-205">**Purpose:** Determines whether the Token-Based Authentication query string parameter should be renamed.</span></span>

<span data-ttu-id="3d02c-206">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-206">Key information:</span></span>

- <span data-ttu-id="3d02c-207">[值] 選項會定義可能要透過其指定權杖的查詢字串參數名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-207">The Value option defines the query string parameter name through which a token may be specified.</span></span>
- <span data-ttu-id="3d02c-208">[值] 選項不能設定為 [ec_token]。</span><span class="sxs-lookup"><span data-stu-id="3d02c-208">The Value option cannot be set to "ec_token."</span></span>
- <span data-ttu-id="3d02c-209">確定只會在 [值] 選項中定義名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-209">Make sure that the name defined in the Value option only</span></span> 
- <span data-ttu-id="3d02c-210">包含有效的 URL 字元。</span><span class="sxs-lookup"><span data-stu-id="3d02c-210">contains valid URL characters.</span></span>

<span data-ttu-id="3d02c-211">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-211">Value</span></span>|<span data-ttu-id="3d02c-212">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-212">Result</span></span>
----|----
<span data-ttu-id="3d02c-213">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-213">Enabled</span></span>|<span data-ttu-id="3d02c-214">[值] 選項會定義應透過其定義權杖的查詢字串參數名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-214">The Value option defines the query string parameter name through which tokens should be defined.</span></span>
<span data-ttu-id="3d02c-215">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-215">Disabled</span></span>|<span data-ttu-id="3d02c-216">您可以指定權杖做為要求 URL 中未定義的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-216">A token may be specified as an undefined query string parameter in the request URL.</span></span>

<span data-ttu-id="3d02c-217">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-217">**Default Behavior:** Disabled.</span></span> <span data-ttu-id="3d02c-218">您可以指定權杖做為要求 URL 中未定義的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-218">A token may be specified as an undefined query string parameter in the request URL.</span></span>

## <a name="caching"></a><span data-ttu-id="3d02c-219">快取</span><span class="sxs-lookup"><span data-stu-id="3d02c-219">Caching</span></span>

<span data-ttu-id="3d02c-220">這些功能是設計來自訂快取內容的時機和方法。</span><span class="sxs-lookup"><span data-stu-id="3d02c-220">These features are designed to customize when and how content is cached.</span></span>

<span data-ttu-id="3d02c-221">名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-221">Name</span></span> | <span data-ttu-id="3d02c-222">目的</span><span class="sxs-lookup"><span data-stu-id="3d02c-222">Purpose</span></span>
-----|--------
<span data-ttu-id="3d02c-223">頻寬參數</span><span class="sxs-lookup"><span data-stu-id="3d02c-223">Bandwidth Parameters</span></span> | <span data-ttu-id="3d02c-224">判斷是否將會使用頻寬節流設定參數 (例如 ec_rate 和 ec_prebuf)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-224">Determines whether bandwidth throttling parameters (i.e., ec_rate and ec_prebuf) will be active.</span></span>
<span data-ttu-id="3d02c-225">頻寬節流設定</span><span class="sxs-lookup"><span data-stu-id="3d02c-225">Bandwidth Throttling</span></span> | <span data-ttu-id="3d02c-226">針對我們的 Edge Server 所提供的回應進行頻寬節流設定。</span><span class="sxs-lookup"><span data-stu-id="3d02c-226">Throttles the bandwidth for the response provided by our edge servers.</span></span>
<span data-ttu-id="3d02c-227">略過快取</span><span class="sxs-lookup"><span data-stu-id="3d02c-227">Bypass Cache</span></span> | <span data-ttu-id="3d02c-228">判斷要求是否可以利用我們的快取技術。</span><span class="sxs-lookup"><span data-stu-id="3d02c-228">Determines whether the request can leverage our caching technology.</span></span>
<span data-ttu-id="3d02c-229">Cache-Control 標頭處理</span><span class="sxs-lookup"><span data-stu-id="3d02c-229">Cache-Control Header Treatment</span></span> | <span data-ttu-id="3d02c-230">當 [外部最大壽命] 功能為作用中時，透過 Edge Server 來控制 Cache-Control 標頭的產生。</span><span class="sxs-lookup"><span data-stu-id="3d02c-230">Controls the generation of Cache-Control headers by the edge server when External Max-Age feature is active.</span></span>
<span data-ttu-id="3d02c-231">快取索引鍵查詢字串</span><span class="sxs-lookup"><span data-stu-id="3d02c-231">Cache-Key Query String</span></span> | <span data-ttu-id="3d02c-232">判斷快取索引鍵是否將包含或排除與要求相關聯的佇列字串參數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-232">Determines whether the cache-key will include or exclude query string parameters associated with a request.</span></span>
<span data-ttu-id="3d02c-233">快取索引鍵重寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-233">Cache-Key Rewrite</span></span> | <span data-ttu-id="3d02c-234">重寫與要求相關聯的快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3d02c-234">Rewrites the cache-key associated with a request.</span></span>
<span data-ttu-id="3d02c-235">完成快取填滿</span><span class="sxs-lookup"><span data-stu-id="3d02c-235">Complete Cache Fill</span></span> | <span data-ttu-id="3d02c-236">判斷在要求於 Edge Server 上產生部分快取遺失時會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="3d02c-236">Determines what happens when a request results in a partial cache miss on an edge server.</span></span>
<span data-ttu-id="3d02c-237">壓縮檔案類型</span><span class="sxs-lookup"><span data-stu-id="3d02c-237">Compress File Types</span></span> | <span data-ttu-id="3d02c-238">定義將在伺服器上壓縮的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-238">Defines the file formats that will be compressed on the server.</span></span>
<span data-ttu-id="3d02c-239">預設的內部最大壽命</span><span class="sxs-lookup"><span data-stu-id="3d02c-239">Default Internal Max-Age</span></span> | <span data-ttu-id="3d02c-240">判斷 Edge Server 到原始伺服器快取重新驗證之間的預設最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-240">Determines the default max-age interval for edge server to origin server cache revalidation.</span></span>
<span data-ttu-id="3d02c-241">Expires 標頭處理</span><span class="sxs-lookup"><span data-stu-id="3d02c-241">Expires Header Treatment</span></span> | <span data-ttu-id="3d02c-242">當 [外部最大壽命] 功能為作用中時，透過 Edge Server 來控制 Expires 標頭的產生。</span><span class="sxs-lookup"><span data-stu-id="3d02c-242">Controls the generation of Expires headers by an edge server when the External Max-Age feature is active.</span></span>
<span data-ttu-id="3d02c-243">外部最大壽命</span><span class="sxs-lookup"><span data-stu-id="3d02c-243">External Max-Age</span></span> | <span data-ttu-id="3d02c-244">判斷瀏覽器到 Edge Server 快取重新驗證之間的最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-244">Determines the max-age interval for browser to edge server cache revalidation.</span></span>
<span data-ttu-id="3d02c-245">強制執行內部最大壽命</span><span class="sxs-lookup"><span data-stu-id="3d02c-245">Force Internal Max-Age</span></span> | <span data-ttu-id="3d02c-246">判斷 Edge Server 到原始伺服器快取重新驗證之間的最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-246">Determines the max-age interval for edge server to origin server cache revalidation.</span></span>
<span data-ttu-id="3d02c-247">H.264 支援 (HTTP 漸進式下載)</span><span class="sxs-lookup"><span data-stu-id="3d02c-247">H.264 Support (HTTP Progressive Download)</span></span> | <span data-ttu-id="3d02c-248">判斷可能用於串流處理內容的 H.264 檔案格式類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-248">Determines the types of H.264 file formats that may be used to stream content.</span></span>
<span data-ttu-id="3d02c-249">接受 No-Cache 要求</span><span class="sxs-lookup"><span data-stu-id="3d02c-249">Honor No-Cache Request</span></span> | <span data-ttu-id="3d02c-250">判斷是否要將 HTTP 用戶端的 no-cache 要求轉送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-250">Determines whether an HTTP client's no-cache requests will be forwarded to the origin server.</span></span>
<span data-ttu-id="3d02c-251">忽略原始的 No-Cache</span><span class="sxs-lookup"><span data-stu-id="3d02c-251">Ignore Origin No-Cache</span></span> | <span data-ttu-id="3d02c-252">判斷我們的 CDN 是否將忽略原始伺服器所提供的特定指示詞。</span><span class="sxs-lookup"><span data-stu-id="3d02c-252">Determines whether our CDN will ignore certain directives served from an origin server.</span></span>
<span data-ttu-id="3d02c-253">忽略無法滿足的範圍</span><span class="sxs-lookup"><span data-stu-id="3d02c-253">Ignore Unsatisfiable Ranges</span></span> | <span data-ttu-id="3d02c-254">判斷在要求產生「416 無法滿足的要求範圍」狀態代碼時將傳回用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-254">Determines the response that will be returned to clients when a request generates a 416 Requested Range Not Satisfiable status code.</span></span>
<span data-ttu-id="3d02c-255">內部最大過時</span><span class="sxs-lookup"><span data-stu-id="3d02c-255">Internal Max-Stale</span></span> | <span data-ttu-id="3d02c-256">控制當 Edge Server 無法使用原始伺服器重新驗證快取的資產時，從 Edge Server 所提供的快取資產可能會經歷多長的標準到期時間。</span><span class="sxs-lookup"><span data-stu-id="3d02c-256">Controls how long past the normal expiration time a cached asset may be served from an edge server when the edge server is unable to revalidate the cached asset with the origin server.</span></span>
<span data-ttu-id="3d02c-257">部分快取共用</span><span class="sxs-lookup"><span data-stu-id="3d02c-257">Partial Cache Sharing</span></span> | <span data-ttu-id="3d02c-258">判斷要求是否可以產生部分快取的內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-258">Determines whether a request can generate partially cached content.</span></span>
<span data-ttu-id="3d02c-259">預先驗證快取的內容</span><span class="sxs-lookup"><span data-stu-id="3d02c-259">Prevalidate Cached Content</span></span> | <span data-ttu-id="3d02c-260">在快取內容的 TTL 到期之前，判斷其是否適用進行早期重新驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-260">Determines whether cached content will be eligible for early revalidation before its TTL expires.</span></span>
<span data-ttu-id="3d02c-261">重新整理零位元組的快取檔案</span><span class="sxs-lookup"><span data-stu-id="3d02c-261">Refresh Zero-Byte Cache Files</span></span> | <span data-ttu-id="3d02c-262">判斷如何透過我們的 Edge Server 來處理 HTTP 用戶端對於 0 位元組快取資產的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-262">Determines how an HTTP client's request for a 0-byte cache asset is handled by our edge servers.</span></span>
<span data-ttu-id="3d02c-263">設定可快取的狀態碼</span><span class="sxs-lookup"><span data-stu-id="3d02c-263">Set Cacheable Status Codes</span></span> | <span data-ttu-id="3d02c-264">定義一組可產生快取內容的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-264">Defines the set of status codes that can result in cached content.</span></span>
<span data-ttu-id="3d02c-265">發生錯誤時傳遞過時的內容</span><span class="sxs-lookup"><span data-stu-id="3d02c-265">Stale Content Delivery on Error</span></span> | <span data-ttu-id="3d02c-266">判斷在快取重新驗證期間發生錯誤時，或者在接收到來自客戶原始伺服器的要求內容時，是否要傳遞到期的快取內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-266">Determines whether expired cached content will be delivered when an error occurs during cache revalidation or when retrieving the requested content from the customer origin server.</span></span>
<span data-ttu-id="3d02c-267">在重新驗證時過期</span><span class="sxs-lookup"><span data-stu-id="3d02c-267">Stale While Revalidate</span></span> | <span data-ttu-id="3d02c-268">允許我們的 Edge Server 在進行重新驗證時提供過時的用戶端給要求者，藉以改善效能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-268">Improves performance by allowing our edge servers to serve stale client to the requester while revalidation takes place.</span></span>
<span data-ttu-id="3d02c-269">註解</span><span class="sxs-lookup"><span data-stu-id="3d02c-269">Comment</span></span> | <span data-ttu-id="3d02c-270">「註解」功能能夠在規則中新增附註。</span><span class="sxs-lookup"><span data-stu-id="3d02c-270">The Comment feature allows a note to be added within a rule.</span></span>

###<a name="bandwidth-parameters"></a><span data-ttu-id="3d02c-271">頻寬參數</span><span class="sxs-lookup"><span data-stu-id="3d02c-271">Bandwidth Parameters</span></span>
<span data-ttu-id="3d02c-272">**目的：**判斷是否將使用頻寬節流設定參數 (例如 ec_rate 和 ec_prebuf)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-272">**Purpose:** Determines whether bandwidth throttling parameters (i.e., ec_rate and ec_prebuf) will be active.</span></span>

<span data-ttu-id="3d02c-273">頻寬節流設定參數會判斷是否要將用戶端要求的資料傳輸速率限制為自訂的速率。</span><span class="sxs-lookup"><span data-stu-id="3d02c-273">Bandwidth throttling parameters determine whether the data transfer rate for a client's request will be limited to a custom rate.</span></span>

<span data-ttu-id="3d02c-274">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-274">Value</span></span>|<span data-ttu-id="3d02c-275">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-275">Result</span></span>
--|--
<span data-ttu-id="3d02c-276">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-276">Enabled</span></span>|<span data-ttu-id="3d02c-277">允許 Edge Server 接受頻寬節流設定要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-277">Allows our edge servers to honor bandwidth throttling requests.</span></span>
<span data-ttu-id="3d02c-278">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-278">Disabled</span></span>|<span data-ttu-id="3d02c-279">導致 Edge Server 忽略頻寬節流設定參數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-279">Causes our edge servers to ignore bandwidth throttling parameters.</span></span> <span data-ttu-id="3d02c-280">通常將會提供要求的內容 (亦即，不需頻寬節流設定)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-280">The requested content will be served normally (i.e., without bandwidth throttling).</span></span>

<span data-ttu-id="3d02c-281">**預設行為：**已啟用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-281">**Default Behavior:** Enabled.</span></span>

###<a name="bandwidth-throttling"></a><span data-ttu-id="3d02c-282">頻寬節流設定</span><span class="sxs-lookup"><span data-stu-id="3d02c-282">Bandwidth Throttling</span></span>
<span data-ttu-id="3d02c-283">**目的：**針對 Edge Server 所提供的回應進行頻寬節流設定。</span><span class="sxs-lookup"><span data-stu-id="3d02c-283">**Purpose:** Throttles the bandwidth for the response provided by our edge servers.</span></span>

<span data-ttu-id="3d02c-284">您必須定義下列這兩個選項，才能正確設定頻寬節流設定。</span><span class="sxs-lookup"><span data-stu-id="3d02c-284">Both of the following options must be defined to properly set up bandwidth throttling.</span></span>

<span data-ttu-id="3d02c-285">選項</span><span class="sxs-lookup"><span data-stu-id="3d02c-285">Option</span></span>|<span data-ttu-id="3d02c-286">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-286">Description</span></span>
--|--
<span data-ttu-id="3d02c-287">每秒 KB 數</span><span class="sxs-lookup"><span data-stu-id="3d02c-287">Kbytes per second</span></span>|<span data-ttu-id="3d02c-288">將此選項設定為可能用來傳遞回應的最大頻寬 (每秒 KB 數)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-288">Set this option to the maximum bandwidth (Kb per second) that may be used to deliver the response.</span></span>
<span data-ttu-id="3d02c-289">Prebuf 秒</span><span class="sxs-lookup"><span data-stu-id="3d02c-289">Prebuf seconds</span></span>|<span data-ttu-id="3d02c-290">將此選項設定為 Edge Server 在進行頻寬節流設定之前將等候的秒數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-290">Set this option to the number of seconds that our edge servers will wait until throttling bandwidth.</span></span> <span data-ttu-id="3d02c-291">這段不受頻寬限制之期間的用意是防止媒體播放器因為頻寬節流設定而遇到間斷或緩衝處理問題。</span><span class="sxs-lookup"><span data-stu-id="3d02c-291">The purpose of this time period of unrestricted bandwidth is to prevent a media player from experiencing stuttering or buffering issues due to bandwidth throttling.</span></span>

<span data-ttu-id="3d02c-292">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-292">**Default Behavior:** Disabled.</span></span>

###<a name="bypass-cache"></a><span data-ttu-id="3d02c-293">略過快取</span><span class="sxs-lookup"><span data-stu-id="3d02c-293">Bypass Cache</span></span>
<span data-ttu-id="3d02c-294">**目的：**判斷要求是否可以利用我們的快取技術。</span><span class="sxs-lookup"><span data-stu-id="3d02c-294">**Purpose:** Determines whether the request can leverage our caching technology.</span></span>

<span data-ttu-id="3d02c-295">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-295">Value</span></span>|<span data-ttu-id="3d02c-296">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-296">Result</span></span>
--|--
<span data-ttu-id="3d02c-297">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-297">Enabled</span></span>|<span data-ttu-id="3d02c-298">導致所有對原始伺服器的要求都失敗，即使先前已在 Edge Server 上快取內容也一樣。</span><span class="sxs-lookup"><span data-stu-id="3d02c-298">Causes all requests to fall through to the origin server, even if the content was previously cached on edge servers.</span></span>
<span data-ttu-id="3d02c-299">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-299">Disabled</span></span>|<span data-ttu-id="3d02c-300">導致 Edge Server 會根據其回應標頭中定義的快取原則來快取資產。</span><span class="sxs-lookup"><span data-stu-id="3d02c-300">Causes edge servers to cache assets according to the cache policy defined in its response headers.</span></span>

<span data-ttu-id="3d02c-301">**預設行為：**</span><span class="sxs-lookup"><span data-stu-id="3d02c-301">**Default Behavior:**</span></span>

- <span data-ttu-id="3d02c-302">**HTTP 大型︰**已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-302">**HTTP Large:** Disabled</span></span>

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a><span data-ttu-id="3d02c-303">Cache-Control 標頭處理</span><span class="sxs-lookup"><span data-stu-id="3d02c-303">Cache Control Header Treatment</span></span>
<span data-ttu-id="3d02c-304">**目的：**當 [外部最大壽命] 功能為作用中時，透過 Edge Server 來控制 Cache-Control 標頭的產生。</span><span class="sxs-lookup"><span data-stu-id="3d02c-304">**Purpose:** Controls the generation of Cache-Control headers by the edge server when External Max-Age Feature is active.</span></span>

<span data-ttu-id="3d02c-305">完成這類型組態的最簡單方式是將 [外部最大壽命] 和 [Cache-Control 標頭處理] 功能放在同一個陳述式中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-305">The easiest way to achieve this type of configuration is to place the External Max-Age and the Cache-Control Header Treatment features in the same statement.</span></span>

<span data-ttu-id="3d02c-306">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-306">Value</span></span>|<span data-ttu-id="3d02c-307">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-307">Result</span></span>
--|--
<span data-ttu-id="3d02c-308">覆寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-308">Overwrite</span></span>|<span data-ttu-id="3d02c-309">確保將會進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="3d02c-309">Ensures that the following actions will take place:</span></span><br/> <span data-ttu-id="3d02c-310">- 覆寫原始伺服器所產生的 Cache-Control 標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-310">- Overwrites the Cache-Control header generated by the origin server.</span></span> <br/><span data-ttu-id="3d02c-311">- 將 [外部最大壽命] 功能所產生的 Cache-Control 標頭加入至回應中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-311">- Adds the Cache-Control header produced by the External Max-Age feature to the response.</span></span>
<span data-ttu-id="3d02c-312">傳遞</span><span class="sxs-lookup"><span data-stu-id="3d02c-312">Pass Through</span></span>|<span data-ttu-id="3d02c-313">確保永遠不會將 [外部最大壽命] 功能所產生的 Cache-Control 標頭加入至回應中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-313">Ensures that the Cache-Control header produced by the External Max-Age feature is never added to the response.</span></span> <br/> <span data-ttu-id="3d02c-314">如果原始伺服器會產生 Cache-Control 標頭，則它將會傳遞給使用者。</span><span class="sxs-lookup"><span data-stu-id="3d02c-314">If the origin server produces a Cache-Control header, it will pass through to the end-user.</span></span> <br/> <span data-ttu-id="3d02c-315">如果原始伺服器未產生 Cache-Control 標頭，則此選項可能導致 Cache-Control 標頭不會包含回應標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-315">If the origin server does not produce a Cache-Control header, then this option may cause the response header to not contain a Cache-Control header.</span></span>
<span data-ttu-id="3d02c-316">如果遺失則加入</span><span class="sxs-lookup"><span data-stu-id="3d02c-316">Add if Missing</span></span>|<span data-ttu-id="3d02c-317">如果 Cache-Control 標頭不是接收自原始伺服器，則此選項會加入 [外部最大壽命] 功能所產生的 Cache-Control 標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-317">If a Cache-Control header was not received from the origin server, then this option adds the Cache-Control header produced by the External Max-Age feature.</span></span> <span data-ttu-id="3d02c-318">若要確保會為所有資產指派 Cache-Control 標頭，此選項非常有用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-318">This option is useful for ensuring that all assets will be assigned a Cache-Control header.</span></span>
<span data-ttu-id="3d02c-319">移除</span><span class="sxs-lookup"><span data-stu-id="3d02c-319">Remove</span></span>| <span data-ttu-id="3d02c-320">此選項可確保標頭回應中不會包含 Cache-Control 標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-320">This option ensures that a Cache-Control header is not included with the header response.</span></span> <span data-ttu-id="3d02c-321">如果已經指派 Cache-Control 標頭，則會從標頭回應中加以移除。</span><span class="sxs-lookup"><span data-stu-id="3d02c-321">If a Cache-Control header has already been assigned, then it will be stripped from the header response.</span></span>

<span data-ttu-id="3d02c-322">**預設行為：**覆寫。</span><span class="sxs-lookup"><span data-stu-id="3d02c-322">**Default Behavior:** Overwrite.</span></span>

###<a name="cache-key-query-string"></a><span data-ttu-id="3d02c-323">快取索引鍵查詢字串</span><span class="sxs-lookup"><span data-stu-id="3d02c-323">Cache-Key Query String</span></span>
<span data-ttu-id="3d02c-324">**目的：**判斷快取索引鍵是否將包含或排除與要求相關聯的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-324">**Purpose:** Determines whether the cache-key will include or exclude query string parameters associated with a request.</span></span>

<span data-ttu-id="3d02c-325">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-325">Key information:</span></span>

- <span data-ttu-id="3d02c-326">指定一或多個查詢字串參數名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-326">Specify one or more query string parameter name(s).</span></span> <span data-ttu-id="3d02c-327">每個參數名稱都應以單一空格分隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-327">Each parameter name should be delimited with a single space.</span></span>
- <span data-ttu-id="3d02c-328">此功能會判斷是否要在快取索引鍵中包含查詢字串參數或從中排除。</span><span class="sxs-lookup"><span data-stu-id="3d02c-328">This feature determines whether query string parameters will be included or excluded from the cache-key.</span></span> <span data-ttu-id="3d02c-329">以下提供每個選項的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="3d02c-329">Additional information is provided for each option below.</span></span>

<span data-ttu-id="3d02c-330">類型</span><span class="sxs-lookup"><span data-stu-id="3d02c-330">Type</span></span>|<span data-ttu-id="3d02c-331">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-331">Description</span></span>
--|--
 <span data-ttu-id="3d02c-332">包含</span><span class="sxs-lookup"><span data-stu-id="3d02c-332">Include</span></span>|  <span data-ttu-id="3d02c-333">指出應該在快取索引鍵中包含每個指定的參數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-333">Indicates that each specified parameter should be included in the cache-key.</span></span> <span data-ttu-id="3d02c-334">系統將針對每個要求產生唯一的快取索引鍵，其中包含此功能中所定義之查詢字串參數的唯一值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-334">A unique cache-key will be generated for each request that contains a unique value for a query string parameter defined in this feature.</span></span> 
 <span data-ttu-id="3d02c-335">全部包含</span><span class="sxs-lookup"><span data-stu-id="3d02c-335">Include All</span></span>  |<span data-ttu-id="3d02c-336">指出將針對每個包含唯一查詢字串的資產要求建立唯一的快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3d02c-336">Indicates that a unique cache-key will be created for each request to an asset that includes a unique query string.</span></span> <span data-ttu-id="3d02c-337">通常不建議使用此類型的組態，因為它可能會導致一小部分的快取命中數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-337">This type of configuration is not typically recommended since it may lead to a small percentage of cache hits.</span></span> <span data-ttu-id="3d02c-338">這將會增加原始伺服器上的負載，因為它必須為更多要求提供服務。</span><span class="sxs-lookup"><span data-stu-id="3d02c-338">This will increase the load on the origin server, since it will have to serve more requests.</span></span> <span data-ttu-id="3d02c-339">這個組態會複製 [查詢字串快取] 頁面上名為「unique-cache」的快取行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-339">This configuration duplicates the caching behavior known as "unique-cache" on the Query-String Caching page.</span></span> 
 <span data-ttu-id="3d02c-340">排除</span><span class="sxs-lookup"><span data-stu-id="3d02c-340">Exclude</span></span> | <span data-ttu-id="3d02c-341">指出只會從快取索引鍵中排除指定的參數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-341">Indicates that only the specified parameter(s) will be excluded from the cache-key.</span></span> <span data-ttu-id="3d02c-342">所有的其他查詢字串參數都將包含於快取索引鍵中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-342">All other query string parameters will be included in the cache-key.</span></span> 
 <span data-ttu-id="3d02c-343">全部排除</span><span class="sxs-lookup"><span data-stu-id="3d02c-343">Exclude All</span></span>  |<span data-ttu-id="3d02c-344">指出將從快取索引鍵中排除所有查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-344">Indicates that all query string parameters will be excluded from the cache-key.</span></span> <span data-ttu-id="3d02c-345">這個組態會複製 [查詢字串快取] 頁面上名為「standard-cache」的預設快取行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-345">This configuration duplicates the default caching behavior, which is known as "standard-cache" on the Query-String Caching page.</span></span> 

<span data-ttu-id="3d02c-346">HTTP 規則引擎的強大功能可讓您自訂實作查詢字串快取的行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-346">The power of HTTP Rules Engine allows you to customize the manner in which query string caching is implemented.</span></span> <span data-ttu-id="3d02c-347">例如，您可以指定查詢字串快取只會在特定位置或檔案類型上執行。</span><span class="sxs-lookup"><span data-stu-id="3d02c-347">For example, you can specify that query string caching only be performed on certain locations or file types.</span></span>

<span data-ttu-id="3d02c-348">如果您想要複製 [查詢字串快取] 頁面上名為「no-cache」的查詢字串快取行為，則您必須建立規則，其中包含 [URL 查詢萬用字元] 比對條件和 [略過快取] 功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-348">If you would like to duplicate the query string caching behavior known as "no-cache" on the Query-String Caching page, then you will need to create a rule that contains a URL Query Wildcard match condition and a Bypass Cache feature.</span></span> <span data-ttu-id="3d02c-349">[URL 查詢萬用字元] 比對條件應設為星號 (*)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-349">The URL Query Wildcard match condition should be set to an asterisk (*).</span></span>

#### <a name="sample-scenarios"></a><span data-ttu-id="3d02c-350">範例案例</span><span class="sxs-lookup"><span data-stu-id="3d02c-350">Sample Scenarios</span></span>

<span data-ttu-id="3d02c-351">此功能的範例使用方式如下所示。</span><span class="sxs-lookup"><span data-stu-id="3d02c-351">Sample usage for this feature is provided below.</span></span> <span data-ttu-id="3d02c-352">以下提供範例要求和預設快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3d02c-352">A sample request and the default cache-key are provided below.</span></span>

- <span data-ttu-id="3d02c-353">**範例要求︰**http://wpc.0001.&lt;網域&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01</span><span class="sxs-lookup"><span data-stu-id="3d02c-353">**Sample request:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01</span></span>
- <span data-ttu-id="3d02c-354">**預設的快取索引鍵︰**/800001/Origin/folder/asset.htm</span><span class="sxs-lookup"><span data-stu-id="3d02c-354">**Default cache-key:** /800001/Origin/folder/asset.htm</span></span>

##### <a name="include"></a><span data-ttu-id="3d02c-355">包含</span><span class="sxs-lookup"><span data-stu-id="3d02c-355">Include</span></span>

<span data-ttu-id="3d02c-356">範例組態：</span><span class="sxs-lookup"><span data-stu-id="3d02c-356">Sample configuration:</span></span>

- <span data-ttu-id="3d02c-357">**類型︰**包括</span><span class="sxs-lookup"><span data-stu-id="3d02c-357">**Type:** Include</span></span>
- <span data-ttu-id="3d02c-358">**參數︰**語言</span><span class="sxs-lookup"><span data-stu-id="3d02c-358">**Parameter(s):** language</span></span>

<span data-ttu-id="3d02c-359">這類型的組態會產生下列查詢字串參數快取索引鍵：</span><span class="sxs-lookup"><span data-stu-id="3d02c-359">This type of configuration would generate the following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a><span data-ttu-id="3d02c-360">全部包含</span><span class="sxs-lookup"><span data-stu-id="3d02c-360">Include All</span></span>

<span data-ttu-id="3d02c-361">範例組態：</span><span class="sxs-lookup"><span data-stu-id="3d02c-361">Sample configuration:</span></span>

- <span data-ttu-id="3d02c-362">**類型︰**全部包括</span><span class="sxs-lookup"><span data-stu-id="3d02c-362">**Type:** Include All</span></span>

<span data-ttu-id="3d02c-363">這類型的組態會產生下列查詢字串參數快取索引鍵：</span><span class="sxs-lookup"><span data-stu-id="3d02c-363">This type of configuration would generate the following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a><span data-ttu-id="3d02c-364">排除</span><span class="sxs-lookup"><span data-stu-id="3d02c-364">Exclude</span></span>

<span data-ttu-id="3d02c-365">範例組態：</span><span class="sxs-lookup"><span data-stu-id="3d02c-365">Sample configuration:</span></span>

- <span data-ttu-id="3d02c-366">**類型︰**排除</span><span class="sxs-lookup"><span data-stu-id="3d02c-366">**Type:** Exclude</span></span>
- <span data-ttu-id="3d02c-367">**參數︰**工作階段識別碼的使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="3d02c-367">**Parameter(s):** sessionid userid</span></span>

<span data-ttu-id="3d02c-368">這類型的組態會產生下列查詢字串參數快取索引鍵：</span><span class="sxs-lookup"><span data-stu-id="3d02c-368">This type of configuration would generate the following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a><span data-ttu-id="3d02c-369">全部排除</span><span class="sxs-lookup"><span data-stu-id="3d02c-369">Exclude All</span></span>

<span data-ttu-id="3d02c-370">範例組態：</span><span class="sxs-lookup"><span data-stu-id="3d02c-370">Sample configuration:</span></span>

- <span data-ttu-id="3d02c-371">**類型︰**全部排除</span><span class="sxs-lookup"><span data-stu-id="3d02c-371">**Type:** Exclude All</span></span>

<span data-ttu-id="3d02c-372">這類型的組態會產生下列查詢字串參數快取索引鍵：</span><span class="sxs-lookup"><span data-stu-id="3d02c-372">This type of configuration would generate the following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a><span data-ttu-id="3d02c-373">快取索引鍵重寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-373">Cache-Key Rewrite</span></span>
<span data-ttu-id="3d02c-374">**目的：**重寫與要求相關聯的快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3d02c-374">**Purpose:** Rewrites the cache-key associated with a request.</span></span>

<span data-ttu-id="3d02c-375">快取索引鍵是基於快取目的識別資產的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="3d02c-375">A cache-key is the relative path that identifies an asset for the purposes of caching.</span></span> <span data-ttu-id="3d02c-376">換句話說，我們的伺服器將根據資產的路徑 (如其快取索引鍵所定義) 來檢查它的快取版本。</span><span class="sxs-lookup"><span data-stu-id="3d02c-376">In other words, our servers will check for a cached version of an asset according to its path as defined by its cache-key.</span></span>

<span data-ttu-id="3d02c-377">藉由定義兩個下列選項來設定此功能：</span><span class="sxs-lookup"><span data-stu-id="3d02c-377">Configure this feature by defining both of the following options:</span></span>

<span data-ttu-id="3d02c-378">選項</span><span class="sxs-lookup"><span data-stu-id="3d02c-378">Option</span></span>|<span data-ttu-id="3d02c-379">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-379">Description</span></span>
--|--
<span data-ttu-id="3d02c-380">原始路徑</span><span class="sxs-lookup"><span data-stu-id="3d02c-380">Original Path</span></span>| <span data-ttu-id="3d02c-381">定義將重寫快取索引鍵之快取類型的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="3d02c-381">Define the relative path to the types of requests whose cache-key will be rewritten.</span></span> <span data-ttu-id="3d02c-382">相對路徑可藉由選取基底原始路徑，然後定義規則運算式模式來定義。</span><span class="sxs-lookup"><span data-stu-id="3d02c-382">A relative path can be defined by selecting a base origin path and then defining a regular expression pattern.</span></span>
<span data-ttu-id="3d02c-383">新路徑</span><span class="sxs-lookup"><span data-stu-id="3d02c-383">New Path</span></span>|<span data-ttu-id="3d02c-384">定義新快取索引鍵的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="3d02c-384">Define the relative path for the new cache-key.</span></span> <span data-ttu-id="3d02c-385">相對路徑可藉由選取基底原始路徑，然後定義規則運算式模式來定義。</span><span class="sxs-lookup"><span data-stu-id="3d02c-385">A relative path can be defined by selecting a base origin path and then defining a regular expression pattern.</span></span> <span data-ttu-id="3d02c-386">此相對路徑可使用 HTTP 變數來動態建構</span><span class="sxs-lookup"><span data-stu-id="3d02c-386">This relative path can be dynamically constructed through the use of HTTP variables</span></span>
<span data-ttu-id="3d02c-387">**預設行為︰**要求的快取索引鍵是依要求 URI 來判斷。</span><span class="sxs-lookup"><span data-stu-id="3d02c-387">**Default Behavior:** A request's cache-key is determined by the request URI.</span></span>

###<a name="complete-cache-fill"></a><span data-ttu-id="3d02c-388">完成快取填滿</span><span class="sxs-lookup"><span data-stu-id="3d02c-388">Complete Cache Fill</span></span>
<span data-ttu-id="3d02c-389">**目的：**判斷在要求於 Edge Server 上產生部分快取遺失時會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="3d02c-389">**Purpose:** Determines what happens when a request results in a partial cache miss on an edge server.</span></span>

<span data-ttu-id="3d02c-390">部分快取遺失會說明未完全下載至 Edge Server 之資產的快取狀態。</span><span class="sxs-lookup"><span data-stu-id="3d02c-390">A partial cache miss describes the cache status for an asset that was not completely downloaded to an edge server.</span></span> <span data-ttu-id="3d02c-391">如果只在 Edge Server 上部分快取了資產，則會將該資產的下一個要求再次轉送至原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-391">If an asset is only partially cached on an edge server, then the next request for that asset will be forwarded again to the origin server.</span></span>
<!---
This feature is not available for the ADN platform. The typical traffic on this platform consists of relatively small assets. The size of the assets served through these platforms helps mitigate the effects of partial cache misses, since the next request will typically result in the asset being cached on that POP.
--->
<span data-ttu-id="3d02c-392">部分快取遺失通常發生於使用者中止下載之後，或發生於只要求使用 HTTP 範圍要求的資產。</span><span class="sxs-lookup"><span data-stu-id="3d02c-392">A partial cache miss typically occurs after a user aborts a download or for assets that are solely requested using HTTP range requests.</span></span> <span data-ttu-id="3d02c-393">對於使用者通常不會完整下載的大型資產 (例如影片) 而言，此功能非常實用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-393">This feature is most useful for large assets where users will not typically download them from start to finish (e.g., videos).</span></span> <span data-ttu-id="3d02c-394">因此，HTTP 大型平台上預設會啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-394">As a result, this feature is enabled by default on the HTTP Large platform.</span></span> <span data-ttu-id="3d02c-395">所有其他平台上則會加以停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-395">It is disabled on all other platforms.</span></span>

<span data-ttu-id="3d02c-396">建議您針對 HTTP 大型平台保留預設組態，因為它將可減少客戶原始伺服器上的負載，並提高客戶下載內容的速度。</span><span class="sxs-lookup"><span data-stu-id="3d02c-396">It is recommended to leave the default configuration for the HTTP Large platform, since it will reduce the load on your customer origin server and increase the speed at which your customers download your content.</span></span>

<span data-ttu-id="3d02c-397">由於追蹤快取設定的方式，因而導致此功能無法與下列比對條件產生關聯︰Edge Cname、要求標頭常值、要求標頭萬用字元、URL 查詢常值和 URL 查詢萬用字元。</span><span class="sxs-lookup"><span data-stu-id="3d02c-397">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following Match conditions: Edge Cname, Request Header Literal, Request Header Wildcard, URL Query Literal, and URL Query Wildcard.</span></span>

<span data-ttu-id="3d02c-398">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-398">Value</span></span>|<span data-ttu-id="3d02c-399">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-399">Result</span></span>
--|--
<span data-ttu-id="3d02c-400">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-400">Enabled</span></span>|<span data-ttu-id="3d02c-401">還原預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-401">Restores the default behavior.</span></span> <span data-ttu-id="3d02c-402">預設行為是強制 Edge Server 從原始伺服器起始資產的背景擷取。</span><span class="sxs-lookup"><span data-stu-id="3d02c-402">The default behavior is to force the edge server to initiate a background fetch of the asset from the origin server.</span></span> <span data-ttu-id="3d02c-403">在那之後，資產將位於 Edge Server 的本機快取中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-403">After which, the asset will be in the edge server's local cache.</span></span>
<span data-ttu-id="3d02c-404">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-404">Disabled</span></span>|<span data-ttu-id="3d02c-405">防止 Edge Server 執行資產的背景擷取。</span><span class="sxs-lookup"><span data-stu-id="3d02c-405">Prevents an edge server from performing a background fetch for the asset.</span></span> <span data-ttu-id="3d02c-406">這表示來自該地區中該資產的下一個要求將導致 Edge Server 向客戶原始伺服器要求它。</span><span class="sxs-lookup"><span data-stu-id="3d02c-406">This means that the next request for that asset from that region will cause an edge server to request it from the customer origin server.</span></span>

<span data-ttu-id="3d02c-407">**預設行為：**已啟用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-407">**Default Behavior:** Enabled.</span></span>

###<a name="compress-file-types"></a><span data-ttu-id="3d02c-408">壓縮檔案類型</span><span class="sxs-lookup"><span data-stu-id="3d02c-408">Compress File Types</span></span>
<span data-ttu-id="3d02c-409">**目的：**定義將在伺服器上壓縮的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-409">**Purpose:** Defines the file formats that will be compressed on the server.</span></span>

<span data-ttu-id="3d02c-410">您可以使用檔案格式的網際網路媒體類型 (亦即，內容類型) 來指定檔案格式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-410">A file format can be specified using its Internet media type (i.e., Content-Type).</span></span> <span data-ttu-id="3d02c-411">網際網路媒體類型是與平台無關的中繼資料，讓我們的伺服器能夠識別特定資產的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-411">Internet media type is platform-independent metadata that allows our servers to identify the file format of a particular asset.</span></span> <span data-ttu-id="3d02c-412">以下提供常用的網際網路媒體類型清單。</span><span class="sxs-lookup"><span data-stu-id="3d02c-412">A list of common Internet media types is provided below.</span></span>

<span data-ttu-id="3d02c-413">網際網路媒體類型</span><span class="sxs-lookup"><span data-stu-id="3d02c-413">Internet Media Type</span></span>|<span data-ttu-id="3d02c-414">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-414">Description</span></span>
--|--
<span data-ttu-id="3d02c-415">text/plain</span><span class="sxs-lookup"><span data-stu-id="3d02c-415">text/plain</span></span>|<span data-ttu-id="3d02c-416">純文字檔案</span><span class="sxs-lookup"><span data-stu-id="3d02c-416">Plain text files</span></span>
<span data-ttu-id="3d02c-417">text/html</span><span class="sxs-lookup"><span data-stu-id="3d02c-417">text/html</span></span>| <span data-ttu-id="3d02c-418">HTML 檔案</span><span class="sxs-lookup"><span data-stu-id="3d02c-418">HTML files</span></span>
<span data-ttu-id="3d02c-419">text/css</span><span class="sxs-lookup"><span data-stu-id="3d02c-419">text/css</span></span>|<span data-ttu-id="3d02c-420">階層式樣式表 (CSS)</span><span class="sxs-lookup"><span data-stu-id="3d02c-420">Cascading Style Sheets (CSS)</span></span>
<span data-ttu-id="3d02c-421">application/x-javascript</span><span class="sxs-lookup"><span data-stu-id="3d02c-421">application/x-javascript</span></span>|<span data-ttu-id="3d02c-422">Javascript</span><span class="sxs-lookup"><span data-stu-id="3d02c-422">Javascript</span></span>
<span data-ttu-id="3d02c-423">application/javascript</span><span class="sxs-lookup"><span data-stu-id="3d02c-423">application/javascript</span></span>|<span data-ttu-id="3d02c-424">Javascript</span><span class="sxs-lookup"><span data-stu-id="3d02c-424">Javascript</span></span>
<span data-ttu-id="3d02c-425">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-425">Key information:</span></span>

- <span data-ttu-id="3d02c-426">使用單一空格來分隔每個網際網路媒體類型，藉以指定多個類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-426">Specify multiple Internet media types by delimiting each one with a single space.</span></span> 
- <span data-ttu-id="3d02c-427">此功能將只會壓縮大小小於 1 MB 的資產。</span><span class="sxs-lookup"><span data-stu-id="3d02c-427">This feature will only compress assets whose size is less than 1 MB.</span></span> <span data-ttu-id="3d02c-428">我們的伺服器將不會壓縮較大型的資產。</span><span class="sxs-lookup"><span data-stu-id="3d02c-428">Larger assets will not be compressed by our servers.</span></span>
- <span data-ttu-id="3d02c-429">諸如影像、視訊和音訊媒體資產 (例如 JPG、MP3、MP4 等) 之類的特定類型內容均已壓縮。</span><span class="sxs-lookup"><span data-stu-id="3d02c-429">Certain types of content, such as images, video, and audio media assets (e.g., JPG, MP3, MP4, etc.), are already compressed.</span></span> <span data-ttu-id="3d02c-430">這些類型資產上的額外壓縮將不會顯著降低檔案大小。</span><span class="sxs-lookup"><span data-stu-id="3d02c-430">Additional compression on these types of assets will not significantly diminish file size.</span></span> <span data-ttu-id="3d02c-431">因此，建議您不要在這些類型的資產上啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="3d02c-431">Therefore, it is recommended that you do not enable compression on these types of assets.</span></span>
- <span data-ttu-id="3d02c-432">不支援萬用字元 (例如星號)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-432">Wildcard characters, such as asterisks, are not supported.</span></span>
- <span data-ttu-id="3d02c-433">將此功能加入規則之前，請確定會針對將套用此規則的平台，在 [壓縮] 頁面上設定 [壓縮已停用] 選項。</span><span class="sxs-lookup"><span data-stu-id="3d02c-433">Before adding this feature to a rule, make sure to set the Compression Disabled option on the Compression page for the platform to which this rule will be applied.</span></span>

###<a name="default-internal-max-age"></a><span data-ttu-id="3d02c-434">預設的內部最大壽命</span><span class="sxs-lookup"><span data-stu-id="3d02c-434">Default Internal Max-Age</span></span>
<span data-ttu-id="3d02c-435">**目的：**判斷 Edge Server 到原始伺服器快取重新驗證之間預設的最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-435">**Purpose:** Determines the default max-age interval for edge server to origin server cache revalidation.</span></span> <span data-ttu-id="3d02c-436">換句話說，就是 Edge Server 將檢查快取的資產是否符合原始伺服器上儲存的資產之前所經過的時間長度。</span><span class="sxs-lookup"><span data-stu-id="3d02c-436">In other words, the amount of time that will pass before an edge server will check whether a cached asset matches the asset stored on the origin server.</span></span>

<span data-ttu-id="3d02c-437">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-437">Key information:</span></span>

- <span data-ttu-id="3d02c-438">只有原始伺服器未在 Cache-Control 或 Expires 標頭中指派最大壽命指示時，此動作才會針對來自該原始伺服器的回應加以執行。</span><span class="sxs-lookup"><span data-stu-id="3d02c-438">This action will only take place for responses from an origin server that did not assign a max-age indication in the Cache-Control or Expires header.</span></span>
- <span data-ttu-id="3d02c-439">此動作將不會針對未被視為可快取的資產加以執行。</span><span class="sxs-lookup"><span data-stu-id="3d02c-439">This action will not take place for assets that are not deemed cacheable.</span></span>
- <span data-ttu-id="3d02c-440">此動作不會影響瀏覽器對 Edge Server 快取重新驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-440">This action does not affect browser to edge server cache revalidations.</span></span> <span data-ttu-id="3d02c-441">這些類型的重新驗證取決於傳送到瀏覽器的 Cache-Control 或 Expires 標頭，而其可使用 [外部最大壽命] 功能來自訂。</span><span class="sxs-lookup"><span data-stu-id="3d02c-441">These types of revalidations are determined by the Cache-Control or Expires headers sent to the browser, which can be customized with the External Max-Age feature.</span></span>
- <span data-ttu-id="3d02c-442">此動作的結果對於回應標頭以及針對您的內容從 Edge Server 傳回的內容並無顯著影響，但它可能會影響從 Edge Server 傳送至原始伺服器的重新驗證流量。</span><span class="sxs-lookup"><span data-stu-id="3d02c-442">The results of this action do not have an observable effect on the response headers and the content returned from edge servers for your content, but it may have an effect on the amount of revalidation traffic sent from edge servers to your origin server.</span></span>
- <span data-ttu-id="3d02c-443">以下列方式設定此功能：</span><span class="sxs-lookup"><span data-stu-id="3d02c-443">Configure this feature by:</span></span>
    - <span data-ttu-id="3d02c-444">選取可套用預設內部最大壽命的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-444">Selecting the status code for which a default internal max-age can be applied.</span></span>
    - <span data-ttu-id="3d02c-445">指定整數值，然後選取所需的時間單位 (亦即，秒、分鐘、小時等)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-445">Specifying an integer value and then selecting the desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="3d02c-446">此值會定義預設的內部最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-446">This value defines the default internal max-age interval.</span></span>

- <span data-ttu-id="3d02c-447">設定為「關閉」的時間單位，將針對未在其 Cache-Control 或 Expires 標頭中指派最大壽命指示的要求，指派 7 天的預設內部最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-447">Setting the time unit to "Off" will assign a default internal max-age interval of 7 days for requests that have not been assigned a max-age indication in their Cache-Control or Expires header.</span></span>
- <span data-ttu-id="3d02c-448">由於追蹤快取設定的行為，因而導致此功能無法與下列比對條件產生關聯：</span><span class="sxs-lookup"><span data-stu-id="3d02c-448">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following match conditions:</span></span> 
    - <span data-ttu-id="3d02c-449">Edge</span><span class="sxs-lookup"><span data-stu-id="3d02c-449">Edge</span></span> 
    - <span data-ttu-id="3d02c-450">Cname</span><span class="sxs-lookup"><span data-stu-id="3d02c-450">Cname</span></span>
    - <span data-ttu-id="3d02c-451">要求標頭常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-451">Request Header Literal</span></span>
    - <span data-ttu-id="3d02c-452">要求標頭萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-452">Request Header Wildcard</span></span>
    - <span data-ttu-id="3d02c-453">要求方法</span><span class="sxs-lookup"><span data-stu-id="3d02c-453">Request Method</span></span>
    - <span data-ttu-id="3d02c-454">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-454">URL Query Literal</span></span>
    - <span data-ttu-id="3d02c-455">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-455">URL Query Wildcard</span></span>

<span data-ttu-id="3d02c-456">**預設值：**7 天</span><span class="sxs-lookup"><span data-stu-id="3d02c-456">**Default Value:** 7 days</span></span>

###<a name="expires-header-treatment"></a><span data-ttu-id="3d02c-457">Expires 標頭處理</span><span class="sxs-lookup"><span data-stu-id="3d02c-457">Expires Header Treatment</span></span>
<span data-ttu-id="3d02c-458">**目的：**當 [外部最大壽命] 功能為作用中時，透過 Edge Server 來控制 Expires 標頭的產生。</span><span class="sxs-lookup"><span data-stu-id="3d02c-458">**Purpose:** Controls the generation of Expires headers by an edge server when the External Max-Age feature is active.</span></span>

<span data-ttu-id="3d02c-459">完成這類型組態的最簡單方式是將 [外部最大壽命] 和 [Expires 標頭處理] 功能放在同一個陳述式中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-459">The easiest way to achieve this type of configuration is to place the External Max-Age and the Expires Header Treatment features in the same statement.</span></span>

<span data-ttu-id="3d02c-460">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-460">Value</span></span>|<span data-ttu-id="3d02c-461">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-461">Result</span></span>
--|--
<span data-ttu-id="3d02c-462">覆寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-462">Overwrite</span></span>|<span data-ttu-id="3d02c-463">確保將會進行下列動作：</span><span class="sxs-lookup"><span data-stu-id="3d02c-463">Ensures that the following actions will take place:</span></span><br/><span data-ttu-id="3d02c-464">- 覆寫原始伺服器所產生的 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-464">- Overwrites the Expires header generated by the origin server.</span></span><br/><span data-ttu-id="3d02c-465">- 將 [外部最大壽命] 功能所產生的 Expires 標頭加入至回應中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-465">- Adds the Expires header produced by the External Max-Age feature to the response.</span></span>
<span data-ttu-id="3d02c-466">傳遞</span><span class="sxs-lookup"><span data-stu-id="3d02c-466">Pass Through</span></span>|<span data-ttu-id="3d02c-467">確保永遠不會將 [外部最大壽命] 功能所產生的 Expires 標頭加入至回應中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-467">Ensures that the Expires header produced by the External Max-Age feature is never added to the response.</span></span> <br/> <span data-ttu-id="3d02c-468">如果原始伺服器會產生 Expires 標頭，則它將會傳遞給使用者。</span><span class="sxs-lookup"><span data-stu-id="3d02c-468">If the origin server produces an Expires header, it will pass through to the end-user.</span></span> <br/><span data-ttu-id="3d02c-469">如果原始伺服器未產生 Expires 標頭，則此選項可能導致 Expires 標頭不會包含回應標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-469">If the origin server does not produce an Expires header, then this option may cause the response header to not contain an Expires header.</span></span>
<span data-ttu-id="3d02c-470">如果遺失則加入</span><span class="sxs-lookup"><span data-stu-id="3d02c-470">Add if Missing</span></span>| <span data-ttu-id="3d02c-471">如果 Expires 標頭不是接收自原始伺服器，則此選項會加入 [外部最大壽命] 功能所產生的 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-471">If an Expires header was not received from the origin server, then this option adds the Expires header produced by the External Max-Age feature.</span></span> <span data-ttu-id="3d02c-472">若要確保會為所有資產指派 Expires 標頭，此選項非常有用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-472">This option is useful for ensuring that all assets will be assigned an Expires header.</span></span>
<span data-ttu-id="3d02c-473">移除</span><span class="sxs-lookup"><span data-stu-id="3d02c-473">Remove</span></span>| <span data-ttu-id="3d02c-474">確保標頭回應中不會包含 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-474">Ensures that an Expires header is not included with the header response.</span></span> <span data-ttu-id="3d02c-475">如果已經指派 Expires 標頭，則會從標頭回應中加以移除。</span><span class="sxs-lookup"><span data-stu-id="3d02c-475">If an Expires header has already been assigned, then it will be stripped from the header response.</span></span>

<span data-ttu-id="3d02c-476">**預設行為：**覆寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-476">**Default Behavior:** Overwrite</span></span>

###<a name="external-max-age"></a><span data-ttu-id="3d02c-477">外部最大壽命</span><span class="sxs-lookup"><span data-stu-id="3d02c-477">External Max-Age</span></span>
<span data-ttu-id="3d02c-478">**目的：**判斷瀏覽器到 Edge Server 快取重新驗證之間的最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-478">**Purpose:** Determines the max-age interval for browser to edge server cache revalidation.</span></span> <span data-ttu-id="3d02c-479">換句話說，就是瀏覽器可以檢查來自 Edge Server 的新版本資產之前所經歷的時間長度。</span><span class="sxs-lookup"><span data-stu-id="3d02c-479">In other words, the amount of time that will pass before a browser can check for a new version of an asset from an edge server.</span></span>

<span data-ttu-id="3d02c-480">啟用此功能將會從我們的 Edge Server 產生 Cache-Control:max-age 和 Expires 標頭，並將它們傳送至 HTTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3d02c-480">Enabling this feature will generate Cache-Control:max-age and Expires headers from our edge servers and send them to the HTTP client.</span></span> <span data-ttu-id="3d02c-481">根據預設，這些標頭將會覆寫原始伺服器所建立的標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-481">By default, these headers will overwrite those created by the origin server.</span></span> <span data-ttu-id="3d02c-482">不過，可能會使用 [Cache-Control 標頭處理] 和 [Expires 標頭處理] 功能來改變此行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-482">However, the Cache-Control Header Treatment and the Expires Header Treatment features may be used to alter this behavior.</span></span>

<span data-ttu-id="3d02c-483">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-483">Key information:</span></span>

- <span data-ttu-id="3d02c-484">此動作不會影響 Edge Server 對原始伺服器的快取重新驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-484">This action does not affect edge server to origin server cache revalidations.</span></span> <span data-ttu-id="3d02c-485">這些類型的重新驗證取決於接收自原始伺服器的 Cache-Control/Expires 標頭，並可使用 [預設的內部最大壽命] 和 [強制執行內部最大壽命] 功能來自訂。</span><span class="sxs-lookup"><span data-stu-id="3d02c-485">These types of revalidations are determined by the Cache-Control/Expires headers received from the origin server, and can be customized with the Default Internal Max-Age and the Force Internal Max-Age features.</span></span>
- <span data-ttu-id="3d02c-486">指定整數值，然後選取所需的時間單位 (亦即，秒、分鐘、小時等)，藉以設定此功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-486">Configure this feature by specifying an integer value and selecting the desired time unit (i.e., seconds, minutes, hours, etc.).</span></span>
- <span data-ttu-id="3d02c-487">將此功能設為負數值，會導致 Edge Server 將過去利用每個回應設定的 Cache-Control:no-cache 和 Expires 時間傳送到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-487">Setting this feature to a negative value causes our edge servers to send a Cache-Control:no-cache and an Expires time that is set in the past with each response to the browser.</span></span> <span data-ttu-id="3d02c-488">儘管 HTTP 用戶端將不會快取回應，但此設定將不會影響 Edge Server 從原始伺服器快取回應的能力。</span><span class="sxs-lookup"><span data-stu-id="3d02c-488">Although an HTTP client will not cache the response, this setting will not affect our edge servers' ability to cache the response from the origin server.</span></span>
- <span data-ttu-id="3d02c-489">將時間單位設為「關閉」，即會停用此功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-489">Setting the time unit to "Off" will disable this feature.</span></span> <span data-ttu-id="3d02c-490">使用原始伺服器回應快取的 Cache-Control/Expires 標頭將會傳遞到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-490">The Cache-Control/Expires headers cached with the response of the origin server will pass through to the browser.</span></span>

<span data-ttu-id="3d02c-491">**預設行為：**關閉</span><span class="sxs-lookup"><span data-stu-id="3d02c-491">**Default Behavior:** Off</span></span>

###<a name="force-internal-max-age"></a><span data-ttu-id="3d02c-492">強制執行內部最大壽命</span><span class="sxs-lookup"><span data-stu-id="3d02c-492">Force Internal Max-Age</span></span>
<span data-ttu-id="3d02c-493">**目的：**判斷 Edge Server 到原始伺服器快取重新驗證之間的最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-493">**Purpose:** Determines the max-age interval for edge server to origin server cache revalidation.</span></span> <span data-ttu-id="3d02c-494">換句話說，就是 Edge Server 可以檢查快取的資產是否符合原始伺服器上儲存的資產之前所經過的時間長度。</span><span class="sxs-lookup"><span data-stu-id="3d02c-494">In other words, the amount of time that will pass before an edge server can check whether a cached asset matches the asset stored on the origin server.</span></span>

<span data-ttu-id="3d02c-495">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-495">Key information:</span></span>

- <span data-ttu-id="3d02c-496">此功能將會覆寫從原始伺服器產生之 Cache-Control 或 Expires 標頭中所定義的最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-496">This feature will override the max-age interval defined in Cache-Control or Expires headers generated from an origin server.</span></span>
- <span data-ttu-id="3d02c-497">此功能不會影響瀏覽器對 Edge Server 的快取重新驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-497">This feature does not affect browser to edge server cache revalidations.</span></span> <span data-ttu-id="3d02c-498">這些類型的重新驗證取決於傳送至瀏覽器的 Cache-Control 或 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-498">These types of revalidations are determined by the Cache-Control or Expires headers sent to the browser.</span></span>
- <span data-ttu-id="3d02c-499">此功能對於由 Edge Server 傳遞給要求者的回應並沒有顯著的影響。</span><span class="sxs-lookup"><span data-stu-id="3d02c-499">This feature does not have an observable effect on the response delivered by an edge server to the requester.</span></span> <span data-ttu-id="3d02c-500">不過，可能會對從 Edge Server 傳送至原始伺服器的重新驗證流量產生作用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-500">However, it may have an effect on the amount of revalidation traffic sent from our edge servers to the origin server.</span></span>
- <span data-ttu-id="3d02c-501">以下列方式設定此功能：</span><span class="sxs-lookup"><span data-stu-id="3d02c-501">Configure this feature by:</span></span>
    - <span data-ttu-id="3d02c-502">選取將套用內部最大壽命的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-502">Selecting the status code for which an internal max-age will be applied.</span></span>
    - <span data-ttu-id="3d02c-503">指定整數值，然後選取所需的時間單位 (亦即，秒、分鐘、小時等)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-503">Specifying an integer value and selecting the desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="3d02c-504">此值會定義要求的最大壽命間隔。</span><span class="sxs-lookup"><span data-stu-id="3d02c-504">This value defines the request's max-age interval.</span></span>

- <span data-ttu-id="3d02c-505">將時間單位設為「關閉」，即會停用此功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-505">Setting the time unit to "Off" disables this feature.</span></span> <span data-ttu-id="3d02c-506">系統不會將內部最大壽命間隔指派給要求的資產。</span><span class="sxs-lookup"><span data-stu-id="3d02c-506">An internal max-age interval will not be assigned to requested assets.</span></span> <span data-ttu-id="3d02c-507">如果原始標頭未包含快取指示，則將根據 [預設內部最大壽命] 功能的作用中設定來快取資產。</span><span class="sxs-lookup"><span data-stu-id="3d02c-507">If the original header does not contain caching instructions, then the asset will be cached according to the active setting in the Default Internal Max-Age feature.</span></span>
- <span data-ttu-id="3d02c-508">由於追蹤快取設定的行為，因而導致此功能無法與下列比對條件產生關聯：</span><span class="sxs-lookup"><span data-stu-id="3d02c-508">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following match conditions:</span></span> 
    - <span data-ttu-id="3d02c-509">Edge</span><span class="sxs-lookup"><span data-stu-id="3d02c-509">Edge</span></span> 
    - <span data-ttu-id="3d02c-510">Cname</span><span class="sxs-lookup"><span data-stu-id="3d02c-510">Cname</span></span>
    - <span data-ttu-id="3d02c-511">要求標頭常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-511">Request Header Literal</span></span>
    - <span data-ttu-id="3d02c-512">要求標頭萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-512">Request Header Wildcard</span></span>
    - <span data-ttu-id="3d02c-513">要求方法</span><span class="sxs-lookup"><span data-stu-id="3d02c-513">Request Method</span></span>
    - <span data-ttu-id="3d02c-514">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-514">URL Query Literal</span></span>
    - <span data-ttu-id="3d02c-515">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-515">URL Query Wildcard</span></span>

<span data-ttu-id="3d02c-516">**預設行為：**關閉</span><span class="sxs-lookup"><span data-stu-id="3d02c-516">**Default Behavior:** Off</span></span>

###<a name="h264-support-http-progressive-download"></a><span data-ttu-id="3d02c-517">H.264 支援 (HTTP 漸進式下載)</span><span class="sxs-lookup"><span data-stu-id="3d02c-517">H.264 Support (HTTP Progressive Download)</span></span>
<span data-ttu-id="3d02c-518">**目的：**判斷可能用於串流處理內容的 H.264 檔案格式類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-518">**Purpose:** Determines the types of H.264 file formats that may be used to stream content.</span></span>

<span data-ttu-id="3d02c-519">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-519">Key information:</span></span>

- <span data-ttu-id="3d02c-520">在 [副檔名] 選項中，定義一組允許的 H.264 副檔名 (以空格分隔)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-520">Define a space-delimited set of allowed H.264 filename extensions in the File Extensions option.</span></span> <span data-ttu-id="3d02c-521">[副檔名] 選項將會覆寫預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-521">The File Extensions option will override the default behavior.</span></span> <span data-ttu-id="3d02c-522">在設定此選項時包括這些副檔名，藉以保有 MP4 和 F4V 支援。</span><span class="sxs-lookup"><span data-stu-id="3d02c-522">Maintain MP4 and F4V support by including those filename extensions when setting this option.</span></span> 
- <span data-ttu-id="3d02c-523">指定每個副檔名時，務必包含句點 (例如 .mp4 .f4v)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-523">Make sure to include a period when specifying each filename extension (e.g., .mp4 .f4v).</span></span>

<span data-ttu-id="3d02c-524">**預設行為︰**HTTP 漸進式下載預設支援 MP4 和 F4V 媒體。</span><span class="sxs-lookup"><span data-stu-id="3d02c-524">**Default Behavior:** HTTP Progressive Download supports MP4 and F4V media by default.</span></span>

###<a name="honor-no-cache-request"></a><span data-ttu-id="3d02c-525">接受 No-Cache 要求</span><span class="sxs-lookup"><span data-stu-id="3d02c-525">Honor no-cache request</span></span>
<span data-ttu-id="3d02c-526">**目的：**判斷是否要將 HTTP 用戶端的 no-cache 要求轉送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-526">**Purpose:** Determines whether an HTTP client's no-cache requests will be forwarded to the origin server.</span></span>

<span data-ttu-id="3d02c-527">當 HTTP 用戶端在 HTTP 要求中傳送 Cache-Control:no-cache 和/或 Pragma:no-cache 要求時，即會發生 no-cache 要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-527">A no-cache request occurs when the HTTP client sends a Cache-Control:no-cache and/or Pragma:no-cache header in the HTTP request.</span></span>

<span data-ttu-id="3d02c-528">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-528">Value</span></span>|<span data-ttu-id="3d02c-529">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-529">Result</span></span>
--|--
<span data-ttu-id="3d02c-530">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-530">Enabled</span></span>|<span data-ttu-id="3d02c-531">允許將 HTTP 用戶端的 no-cache 要求轉送到原始伺服器，而原始伺服器會透過 Edge Server 將回應標頭和主體傳回 HTTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3d02c-531">Allows an HTTP client's no-cache requests to be forwarded to the origin server, and the origin server will return the response headers and the body through the edge server back to the HTTP client.</span></span>
<span data-ttu-id="3d02c-532">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-532">Disabled</span></span>|<span data-ttu-id="3d02c-533">還原預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-533">Restores the default behavior.</span></span> <span data-ttu-id="3d02c-534">預設行為是防止將 no-cache 要求轉送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-534">The default behavior is to prevent no-cache requests from being forwarded to the origin server.</span></span>

<span data-ttu-id="3d02c-535">針對所有生產環境的流量，強烈建議將此功能保留為其預設的停用狀態。</span><span class="sxs-lookup"><span data-stu-id="3d02c-535">For all production traffic, it is highly recommended to leave this feature in its default disabled state.</span></span> <span data-ttu-id="3d02c-536">否則，將無法為原始伺服器提供防護，來防範可能會在重新整理網頁時不小心觸發許多 no-cache 要求的使用者，或者許多已編碼為要透過每個視訊要求傳送 no-cache 標題的熱門媒體播放器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-536">Otherwise, origin servers will not be shielded from end-users who may inadvertently trigger many no-cache requests when refreshing web pages, or from the many popular media players that are coded to send a no-cache header with every video request.</span></span> <span data-ttu-id="3d02c-537">不過，此功能非常適合用來套用至特定的非生產環境暫存或測試目錄，以便隨時從原始伺服器提取隨最新內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-537">Nevertheless, this feature can be useful to apply to certain non-production staging or testing directories, in order to allow fresh content to be pulled on-demand from the origin server.</span></span>

<span data-ttu-id="3d02c-538">將針對因此功能而允許轉送至原始伺服器的要求報告的快取狀態為 TCP_Client_Refresh_Miss。</span><span class="sxs-lookup"><span data-stu-id="3d02c-538">The cache status that will be reported for a request that is allowed to be forwarded to an origin server due to this feature is TCP_Client_Refresh_Miss.</span></span> <span data-ttu-id="3d02c-539">快取狀態報表 (可在 [核心報告] 模組中取得) 會依快取狀態提供統計資訊。</span><span class="sxs-lookup"><span data-stu-id="3d02c-539">The Cache Statuses report, which is available in the Core reporting module, provides statistical information by cache status.</span></span> <span data-ttu-id="3d02c-540">這讓您能夠追蹤因此功能而轉送至原始伺服器的要求數目和百分比。</span><span class="sxs-lookup"><span data-stu-id="3d02c-540">This allows you to track the number and percentage of requests that are being forwarded to an origin server due to this feature.</span></span>

<span data-ttu-id="3d02c-541">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-541">**Default Behavior:** Disabled.</span></span>

###<a name="ignore-origin-no-cache"></a><span data-ttu-id="3d02c-542">忽略原始的 No-Cache</span><span class="sxs-lookup"><span data-stu-id="3d02c-542">Ignore Origin no-cache</span></span>
<span data-ttu-id="3d02c-543">**目的：**判斷我們的 CDN 是否將忽略原始伺服器所提供的特定指示詞：</span><span class="sxs-lookup"><span data-stu-id="3d02c-543">**Purpose:** Determines whether our CDN will ignore the following directives served from an origin server:</span></span>

- <span data-ttu-id="3d02c-544">Cache-Control: private</span><span class="sxs-lookup"><span data-stu-id="3d02c-544">Cache-Control: private</span></span>
- <span data-ttu-id="3d02c-545">Cache-Control: no-store</span><span class="sxs-lookup"><span data-stu-id="3d02c-545">Cache-Control: no-store</span></span>
- <span data-ttu-id="3d02c-546">Cache-Control: no-cache</span><span class="sxs-lookup"><span data-stu-id="3d02c-546">Cache-Control: no-cache</span></span>
- <span data-ttu-id="3d02c-547">Pragma: no-cache</span><span class="sxs-lookup"><span data-stu-id="3d02c-547">Pragma: no-cache</span></span>

<span data-ttu-id="3d02c-548">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-548">Key information:</span></span>

- <span data-ttu-id="3d02c-549">定義將忽略上述指示詞的狀態碼清單 (以空格分隔)，藉以設定此功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-549">Configure this feature by defining a space-delimited list of status codes for which the above directives will be ignored.</span></span>
- <span data-ttu-id="3d02c-550">以下是此功能的有效狀態碼集合︰200、203、300、301、302、305、307、400、401、402、403、404、405、406、407、408、409、410、411、412、413、414、415、416、417、500、501、502、503、504 和 505。</span><span class="sxs-lookup"><span data-stu-id="3d02c-550">The set of valid status codes for this feature are: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, and 505.</span></span>
- <span data-ttu-id="3d02c-551">藉由將其設為空白值來停用此功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-551">Disable this feature by setting it to a blank value.</span></span>
- <span data-ttu-id="3d02c-552">由於追蹤快取設定的行為，因而導致此功能無法與下列比對條件產生關聯：</span><span class="sxs-lookup"><span data-stu-id="3d02c-552">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following match conditions:</span></span> 
    - <span data-ttu-id="3d02c-553">Edge</span><span class="sxs-lookup"><span data-stu-id="3d02c-553">Edge</span></span> 
    - <span data-ttu-id="3d02c-554">Cname</span><span class="sxs-lookup"><span data-stu-id="3d02c-554">Cname</span></span>
    - <span data-ttu-id="3d02c-555">要求標頭常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-555">Request Header Literal</span></span>
    - <span data-ttu-id="3d02c-556">要求標頭萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-556">Request Header Wildcard</span></span>
    - <span data-ttu-id="3d02c-557">要求方法</span><span class="sxs-lookup"><span data-stu-id="3d02c-557">Request Method</span></span>
    - <span data-ttu-id="3d02c-558">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-558">URL Query Literal</span></span>
    - <span data-ttu-id="3d02c-559">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-559">URL Query Wildcard</span></span>

<span data-ttu-id="3d02c-560">**預設行為︰**預設行為是採用上述指示詞。</span><span class="sxs-lookup"><span data-stu-id="3d02c-560">**Default Behavior:** The default behavior is to honor the above directives.</span></span>

###<a name="ignore-unsatisfiable-ranges"></a><span data-ttu-id="3d02c-561">忽略無法滿足的範圍</span><span class="sxs-lookup"><span data-stu-id="3d02c-561">Ignore Unsatisfiable Ranges</span></span> 
<span data-ttu-id="3d02c-562">**目的：**判斷在要求產生 [416 無法滿足的要求範圍] 狀態代碼時將傳回用戶端的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-562">**Purpose:** Determines the response that will be returned to clients when a request generates a 416 Requested Range Not Satisfiable status code.</span></span>

<span data-ttu-id="3d02c-563">根據預設，當 Edge Server 無法滿足指定的位元組範圍要求，且未指定 If-Range 要求標頭欄位時，即會傳回此狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-563">By default, this status code is returned when the specified byte-range request cannot be satisfied by an edge server and an If-Range request header field was not specified.</span></span>

<span data-ttu-id="3d02c-564">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-564">Value</span></span>|<span data-ttu-id="3d02c-565">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-565">Result</span></span>
-|-
<span data-ttu-id="3d02c-566">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-566">Enabled</span></span>|<span data-ttu-id="3d02c-567">防止 Edge Server 使用 [416 無法滿足的要求範圍] 狀態碼來回應不正確的位元組範圍要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-567">Prevents our edge servers from responding to an invalid byte-range request with a 416 Requested Range Not Satisfiable status code.</span></span> <span data-ttu-id="3d02c-568">我們的伺服器將改為傳遞要求的資產，並將 [200 確定] 傳回用戶端。</span><span class="sxs-lookup"><span data-stu-id="3d02c-568">Instead our servers will deliver the requested asset and return a 200 OK to the client.</span></span>
<span data-ttu-id="3d02c-569">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-569">Disabled</span></span>|<span data-ttu-id="3d02c-570">還原預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-570">Restores the default behavior.</span></span> <span data-ttu-id="3d02c-571">預設行為是接受 [416 無法滿足的要求範圍] 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-571">The default behavior is to honor the 416 Requested Range Not Satisfiable status code.</span></span>

<span data-ttu-id="3d02c-572">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-572">**Default Behavior:** Disabled.</span></span>

###<a name="internal-max-stale"></a><span data-ttu-id="3d02c-573">內部最大過時</span><span class="sxs-lookup"><span data-stu-id="3d02c-573">Internal Max-Stale</span></span>
<span data-ttu-id="3d02c-574">**目的：**控制當 Edge Server 無法使用原始伺服器重新驗證快取的資產時，從 Edge Server 所提供的快取資產可能會經歷多長的標準到期時間。</span><span class="sxs-lookup"><span data-stu-id="3d02c-574">**Purpose:** Controls how long past the normal expiration time a cached asset may be served from an edge server when the edge server is unable to revalidate the cached asset with the origin server.</span></span>

<span data-ttu-id="3d02c-575">一般來說，當資產的最大壽命時間過期時，Edge Server 會將重新驗證要求傳送至原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-575">Normally, when an asset's max-age time expires, the edge server will send a revalidation request to the origin server.</span></span> <span data-ttu-id="3d02c-576">原始伺服器接著會使用 [304 未修改] 來回應，以便為 Edge Server 提供所快取資產上的全新租用，或使用 [200 確定] 來提供具備更新快取資產版本的 Edge Server。</span><span class="sxs-lookup"><span data-stu-id="3d02c-576">The origin server will then respond with either a 304 Not Modified to give the edge server a fresh lease on the cached asset, or else with 200 OK to provide the edge server with an updated version of the cached asset.</span></span>

<span data-ttu-id="3d02c-577">如果 Edge Server 在嘗試進行這類重新驗證時無法建立與原始伺服器的連線，則這個 [內部最大過時] 功能就會控制 Edge Server 是否可能要繼續提供現已過時的資產，以及提供多久時間。</span><span class="sxs-lookup"><span data-stu-id="3d02c-577">If the edge server is unable to establish a connection with the origin server while attempting such a revalidation, then this Internal Max-Stale feature controls whether, and for how long, the edge server may continue to serve the now-stale asset.</span></span>

<span data-ttu-id="3d02c-578">請注意，這個時間間隔是從資產的最大壽命到期時開始，而不是從發生失敗的重新驗證時開始。</span><span class="sxs-lookup"><span data-stu-id="3d02c-578">Note that this time interval starts when the asset's max-age expires, not when the failed revalidation occurs.</span></span> <span data-ttu-id="3d02c-579">因此，在未成功重新驗證的情況下可為資產提供服務的最長期間，是由 max-age 加上 max-stale 的組合所指定的時間長度。</span><span class="sxs-lookup"><span data-stu-id="3d02c-579">Therefore, the maximum period during which an asset can be served without successful revalidation is the amount of time specified by the combination of max-age plus max-stale.</span></span> <span data-ttu-id="3d02c-580">例如，如果資產是在 9:00 快取，而 max-age 為 30 分鐘且 max-stale 為 15 分鐘，則在 9:44 進行的失敗重新驗證嘗試會導致使用者接收到過時的快取資產，而在 9:46 進行的失敗重新驗證嘗試則會導致使用者接收到 [504 閘道逾時]。</span><span class="sxs-lookup"><span data-stu-id="3d02c-580">For example, if an asset was cached at 9:00 with a max-age of 30 minutes and a max-stale of 15 minutes, then a failed revalidation attempt at 9:44 would result in an end-user receiving the stale cached asset, while a failed revalidation attempt at 9:46 would result in the end user receiving a 504 Gateway Timeout.</span></span>

<span data-ttu-id="3d02c-581">任何針對此功能設定的值都會由接收自原始伺服器的 Cache-Control:must-revalidate 或 Cache-Control:proxy-revalidate 標頭所取代。</span><span class="sxs-lookup"><span data-stu-id="3d02c-581">Any value configured for this feature is superseded by Cache-Control:must-revalidate or Cache-Control:proxy-revalidate headers received from the origin server.</span></span> <span data-ttu-id="3d02c-582">如果在一開始快取資產時從原始伺服器接收到這其中一個標頭，則 Edge Server 將不會為過時的快取資產提供服務。</span><span class="sxs-lookup"><span data-stu-id="3d02c-582">If either of those headers is received from the origin server when an asset is initially cached, then the edge server will not serve a stale cached asset.</span></span> <span data-ttu-id="3d02c-583">在這種情況下，如果 Edge Server 無法在資產的最大壽命間隔到期時利用原始伺服器進行重新驗證，則 Edge Server 將會傳回 [504 閘道逾時]。</span><span class="sxs-lookup"><span data-stu-id="3d02c-583">In such a case, if the edge server is unable to revalidate with the origin when the asset's max-age interval has expired, then the edge server will return a 504 Gateway Timeout.</span></span>

<span data-ttu-id="3d02c-584">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-584">Key information:</span></span>

- <span data-ttu-id="3d02c-585">以下列方式設定此功能：</span><span class="sxs-lookup"><span data-stu-id="3d02c-585">Configure this feature by:</span></span>
    - <span data-ttu-id="3d02c-586">選取將套用 max-stale 的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-586">Selecting the status code for which a max-stale will be applied.</span></span>
    - <span data-ttu-id="3d02c-587">指定整數值，然後選取所需的時間單位 (亦即，秒、分鐘、小時等)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-587">Specifying an integer value and then selecting the desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="3d02c-588">此值可定義將套用的內部 max-stale。</span><span class="sxs-lookup"><span data-stu-id="3d02c-588">This value defines the internal max-stale that will be applied.</span></span>

- <span data-ttu-id="3d02c-589">將時間單位設為「關閉」，即會停用此功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-589">Setting the time unit to "Off" will disable this feature.</span></span> <span data-ttu-id="3d02c-590">系統將不會在快取的資產超過一般到期時間之後為其提供服務。</span><span class="sxs-lookup"><span data-stu-id="3d02c-590">A cached asset will not be served beyond its normal expiration time.</span></span>
- <span data-ttu-id="3d02c-591">由於追蹤快取設定的行為，因而導致此功能無法與下列比對條件產生關聯：</span><span class="sxs-lookup"><span data-stu-id="3d02c-591">Due to the manner in which cache settings are tracked, this feature cannot be associated with the following match conditions:</span></span> 
    - <span data-ttu-id="3d02c-592">Edge</span><span class="sxs-lookup"><span data-stu-id="3d02c-592">Edge</span></span> 
    - <span data-ttu-id="3d02c-593">Cname</span><span class="sxs-lookup"><span data-stu-id="3d02c-593">Cname</span></span>
    - <span data-ttu-id="3d02c-594">要求標頭常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-594">Request Header Literal</span></span>
    - <span data-ttu-id="3d02c-595">要求標頭萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-595">Request Header Wildcard</span></span>
    - <span data-ttu-id="3d02c-596">要求方法</span><span class="sxs-lookup"><span data-stu-id="3d02c-596">Request Method</span></span>
    - <span data-ttu-id="3d02c-597">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-597">URL Query Literal</span></span>
    - <span data-ttu-id="3d02c-598">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-598">URL Query Wildcard</span></span>

<span data-ttu-id="3d02c-599">**預設行為：**2 分鐘</span><span class="sxs-lookup"><span data-stu-id="3d02c-599">**Default Behavior:** 2 minutes</span></span>

###<a name="partial-cache-sharing"></a><span data-ttu-id="3d02c-600">部分快取共用</span><span class="sxs-lookup"><span data-stu-id="3d02c-600">Partial Cache Sharing</span></span>
<span data-ttu-id="3d02c-601">**目的：**判斷要求是否可以產生部分快取的內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-601">**Purpose:** Determines whether a request can generate partially cached content.</span></span>

<span data-ttu-id="3d02c-602">接著可能會使用這個部分快取來滿足該內容的新要求，直到完全快取要求的內容為止。</span><span class="sxs-lookup"><span data-stu-id="3d02c-602">This partial cache may then be used to fulfill new requests for that content until the requested content is fully cached.</span></span>

<span data-ttu-id="3d02c-603">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-603">Value</span></span>|<span data-ttu-id="3d02c-604">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-604">Result</span></span>
-|-
<span data-ttu-id="3d02c-605">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-605">Enabled</span></span>|<span data-ttu-id="3d02c-606">要求可以產生部分快取的內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-606">Requests can generate partially cached content.</span></span>
<span data-ttu-id="3d02c-607">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-607">Disabled</span></span>|<span data-ttu-id="3d02c-608">要求只能產生所要求內容的完整快取版本。</span><span class="sxs-lookup"><span data-stu-id="3d02c-608">Requests can only generate a fully cached version of the requested content.</span></span>

<span data-ttu-id="3d02c-609">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-609">**Default Behavior:** Disabled.</span></span>

###<a name="prevalidate-cached-content"></a><span data-ttu-id="3d02c-610">預先驗證快取的內容</span><span class="sxs-lookup"><span data-stu-id="3d02c-610">Prevalidate Cached Content</span></span>
<span data-ttu-id="3d02c-611">**目的：**在快取內容的 TTL 到期之前，判斷其是否適用進行早期重新驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-611">**Purpose:** Determines whether cached content will be eligible for early revalidation before its TTL expires.</span></span>

<span data-ttu-id="3d02c-612">定義在要求內容的 TTL 到期之前的時間長度，而要求的內容在這段期間將適用進行早期驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-612">Define the amount of time prior to the expiration of the requested content's TTL during which it will be eligible for early revalidation.</span></span>

<span data-ttu-id="3d02c-613">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-613">Key information:</span></span>

- <span data-ttu-id="3d02c-614">選取「關閉」做為時間單位，需要在快取內容的 TTL 到期之後進行重新驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-614">Selecting "Off" as the time unit requires revalidation to take place after the cached content's TTL has expired.</span></span> <span data-ttu-id="3d02c-615">不應指定時間，且將會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="3d02c-615">Time should not be specified and it will be ignored.</span></span>

<span data-ttu-id="3d02c-616">**預設行為：**關閉。</span><span class="sxs-lookup"><span data-stu-id="3d02c-616">**Default Behavior:** Off.</span></span> <span data-ttu-id="3d02c-617">重新驗證可能只會在快取內容的 TTL 到期之後進行。</span><span class="sxs-lookup"><span data-stu-id="3d02c-617">Revalidation may only take place after the cached content's TTL has expired.</span></span>

###<a name="refresh-zero-byte-cache-files"></a><span data-ttu-id="3d02c-618">重新整理零位元組的快取檔案</span><span class="sxs-lookup"><span data-stu-id="3d02c-618">Refresh Zero Byte Cache Files</span></span>
<span data-ttu-id="3d02c-619">**目的：**判斷如何透過 Edge Server 來處理 HTTP 用戶端對於 0 位元組快取資產的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-619">**Purpose:** Determines how an HTTP client's request for a 0-byte cache asset is handled by our edge servers.</span></span>

<span data-ttu-id="3d02c-620">有效值為：</span><span class="sxs-lookup"><span data-stu-id="3d02c-620">Valid values are:</span></span>

<span data-ttu-id="3d02c-621">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-621">Value</span></span>|<span data-ttu-id="3d02c-622">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-622">Result</span></span>
--|--
<span data-ttu-id="3d02c-623">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-623">Enabled</span></span>|<span data-ttu-id="3d02c-624">導致 Edge Server 重新擷取原始伺服器的資產。</span><span class="sxs-lookup"><span data-stu-id="3d02c-624">Causes our edge server to re-fetch the asset from the origin server.</span></span>
<span data-ttu-id="3d02c-625">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-625">Disabled</span></span>|<span data-ttu-id="3d02c-626">還原預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-626">Restores the default behavior.</span></span> <span data-ttu-id="3d02c-627">預設行為是根據要求提供有效的快取資產。</span><span class="sxs-lookup"><span data-stu-id="3d02c-627">The default behavior is to serve up valid cache assets upon request.</span></span>
<span data-ttu-id="3d02c-628">不需要此功能即可進行正確的快取和內容傳遞，但此功能可能有助於解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="3d02c-628">This feature is not required for correct caching and content delivery, but may be useful as a workaround.</span></span> <span data-ttu-id="3d02c-629">例如，原始伺服器上的動態內容產生器不慎產生了要傳送到 Edge Server 的 0 位元組回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-629">For example, dynamic content generators on origin servers can inadvertently result in 0-byte responses being sent to the edge servers.</span></span> <span data-ttu-id="3d02c-630">我們的 Edge Server 通常會快取這些類型的回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-630">These types of responses are typically cached by our edge servers.</span></span> <span data-ttu-id="3d02c-631">如果您知道對於這類內容而言，0 位元組的回應絕對不是有效的回應，</span><span class="sxs-lookup"><span data-stu-id="3d02c-631">If you know that a 0-byte response is never a valid response</span></span> 

<span data-ttu-id="3d02c-632">則此功能可防止將這些類型的資產提供給用戶端。</span><span class="sxs-lookup"><span data-stu-id="3d02c-632">for such content, then this feature can prevent these types of assets from being served to your clients.</span></span>

<span data-ttu-id="3d02c-633">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-633">**Default Behavior:** Disabled.</span></span>

###<a name="set-cacheable-status-codes"></a><span data-ttu-id="3d02c-634">設定可快取的狀態碼</span><span class="sxs-lookup"><span data-stu-id="3d02c-634">Set Cacheable Status Codes</span></span>
<span data-ttu-id="3d02c-635">**目的：**定義一組可產生快取內容的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-635">**Purpose:** Defines the set of status codes that can result in cached content.</span></span>

<span data-ttu-id="3d02c-636">根據預設，只會針對 [200 確定] 回應啟用快取。</span><span class="sxs-lookup"><span data-stu-id="3d02c-636">By default, caching is only enabled for 200 OK responses.</span></span>

<span data-ttu-id="3d02c-637">定義一組所需的狀態碼 (以空格分隔)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-637">Define a space-delimited set of the desired status codes.</span></span>

<span data-ttu-id="3d02c-638">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-638">Key information:</span></span>

- <span data-ttu-id="3d02c-639">另請啟用 [忽略原始的 No-Cache] 功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-639">Please also enable the Ignore Origin No-Cache feature.</span></span> <span data-ttu-id="3d02c-640">如果未啟用該功能，則可能不會快取非 [200 確定] 的回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-640">If that feature is not enabled, then non-200 OK responses may not be cached.</span></span>
- <span data-ttu-id="3d02c-641">以下是此功能的有效狀態碼集合︰203、300、301、302、305、307、400、401、402、403、404、405、406、407、408、409、410、411、412、413、414、415、416、417、500、501、502、503、504 和 505。</span><span class="sxs-lookup"><span data-stu-id="3d02c-641">The set of valid status codes for this feature are: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, and 505.</span></span>
- <span data-ttu-id="3d02c-642">此功能無法用來針對產生 [200 確定] 狀態碼的回應停用快取。</span><span class="sxs-lookup"><span data-stu-id="3d02c-642">This feature cannot be used to disable caching for responses that generate a 200 OK status code.</span></span>

<span data-ttu-id="3d02c-643">**預設行為︰**只會針對產生 [200 確定] 狀態碼的回應啟用快取。</span><span class="sxs-lookup"><span data-stu-id="3d02c-643">**Default Behavior:** Caching is only enabled for responses that generate a 200 OK status code.</span></span>
###<a name="stale-content-delivery-on-error"></a><span data-ttu-id="3d02c-644">發生錯誤時傳遞過時的內容</span><span class="sxs-lookup"><span data-stu-id="3d02c-644">Stale Content Delivery on Error</span></span>
<span data-ttu-id="3d02c-645">**目的：**</span><span class="sxs-lookup"><span data-stu-id="3d02c-645">**Purpose:**</span></span> 

<span data-ttu-id="3d02c-646">判斷在快取重新驗證期間發生錯誤時，或者在接收到來自客戶原始伺服器的要求內容時，是否要傳遞到期的快取內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-646">Determines whether expired cached content will be delivered when an error occurs during cache revalidation or when retrieving the requested content from the customer origin server.</span></span>

<span data-ttu-id="3d02c-647">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-647">Value</span></span>|<span data-ttu-id="3d02c-648">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-648">Result</span></span>
-|-
<span data-ttu-id="3d02c-649">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-649">Enabled</span></span>|<span data-ttu-id="3d02c-650">與原始伺服器連接期間發生錯誤時，即會將過時的內容提供給要求者。</span><span class="sxs-lookup"><span data-stu-id="3d02c-650">Stale content will be served to the requester when an error occurs during a connection to an origin server.</span></span>
<span data-ttu-id="3d02c-651">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-651">Disabled</span></span>|<span data-ttu-id="3d02c-652">系統會將原始伺服器的錯誤轉送給要求者。</span><span class="sxs-lookup"><span data-stu-id="3d02c-652">The origin server's error will be forwarded to the requester.</span></span>

<span data-ttu-id="3d02c-653">**預設行為：**已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-653">**Default Behavior:** Disabled</span></span>

###<a name="stale-while-revalidate"></a><span data-ttu-id="3d02c-654">在重新驗證時過期</span><span class="sxs-lookup"><span data-stu-id="3d02c-654">Stale While Revalidate</span></span>
<span data-ttu-id="3d02c-655">**目的：**允許 Edge Server 在進行重新驗證時提供過時的用戶端給要求者，藉以改善效能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-655">**Purpose:** Improves performance by allowing our edge servers to serve stale content to the requester while revalidation takes place.</span></span>

<span data-ttu-id="3d02c-656">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-656">Key information:</span></span>

- <span data-ttu-id="3d02c-657">此功能的行為會根據選取的時間單位而不同。</span><span class="sxs-lookup"><span data-stu-id="3d02c-657">The behavior of this feature varies according to the selected time unit.</span></span>
    - <span data-ttu-id="3d02c-658">**時間單位︰**指定的時間長度，然後選取允許過時內容傳遞的時間單位 (例如秒、分鐘、小時等)。</span><span class="sxs-lookup"><span data-stu-id="3d02c-658">**Time Unit:** Specify a length of time and select a time unit (e.g., Seconds, Minutes, Hours, etc.) to allow stale content delivery.</span></span> <span data-ttu-id="3d02c-659">這種類型的安裝程式可讓 CDN 根據下列公式，延伸可能要在要求驗證之前傳遞內容的時間長度：**TTL** + **重新驗證時間時過時**</span><span class="sxs-lookup"><span data-stu-id="3d02c-659">This type of setup allows the CDN to extend the length of time that it may deliver content before requiring validation according to the following formula:**TTL** + **Stale While Revalidate Time**</span></span> 
    - <span data-ttu-id="3d02c-660">**關閉：**選取「關閉」，以便在可能提供過時內容的要求之前，要求重新驗證。</span><span class="sxs-lookup"><span data-stu-id="3d02c-660">**Off:** Select "Off" to require revalidation before a request for stale content may be served.</span></span>
        - <span data-ttu-id="3d02c-661">請勿指定時間長度，因為它不適用且將會遭到忽略。</span><span class="sxs-lookup"><span data-stu-id="3d02c-661">Do not specify a length of time since it is inapplicable and will be ignored.</span></span>

<span data-ttu-id="3d02c-662">**預設行為：**關閉。</span><span class="sxs-lookup"><span data-stu-id="3d02c-662">**Default Behavior:** Off.</span></span> <span data-ttu-id="3d02c-663">重新驗證必須在可提供要求的內容之前進行。</span><span class="sxs-lookup"><span data-stu-id="3d02c-663">Revalidation must take place before the requested content can be served.</span></span>

###<a name="comment"></a><span data-ttu-id="3d02c-664">註解</span><span class="sxs-lookup"><span data-stu-id="3d02c-664">Comment</span></span>
<span data-ttu-id="3d02c-665">**目的：**能夠在規則中加入附註。</span><span class="sxs-lookup"><span data-stu-id="3d02c-665">**Purpose:** Allows a note to be added within a rule.</span></span>

<span data-ttu-id="3d02c-666">此功能的用途之一是提供一般用途的規則，或是為何要將特定比對條件或功能加入至規則的其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3d02c-666">One use for this feature is to provide additional information on the general purpose of a rule or why a particular match condition or feature was added to the rule.</span></span>

<span data-ttu-id="3d02c-667">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-667">Key information:</span></span>

- <span data-ttu-id="3d02c-668">您最多可以指定 150 個字元。</span><span class="sxs-lookup"><span data-stu-id="3d02c-668">A maximum of 150 characters may be specified.</span></span>
- <span data-ttu-id="3d02c-669">務必只使用英數字元。</span><span class="sxs-lookup"><span data-stu-id="3d02c-669">Make sure to only use alphanumeric characters.</span></span>
- <span data-ttu-id="3d02c-670">此功能不會影響規則的行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-670">This feature does not affect the behavior of the rule.</span></span> <span data-ttu-id="3d02c-671">這只表示會提供一個區域，讓您可在其中提供資訊以供未來參考之用，或是有助於疑難排解規則的資訊。</span><span class="sxs-lookup"><span data-stu-id="3d02c-671">It is merely meant to provide an area where you can provide information for future reference or that may help when troubleshooting the rule.</span></span>
 
## <a name="headers"></a><span data-ttu-id="3d02c-672">標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-672">Headers</span></span>

<span data-ttu-id="3d02c-673">這些功能是設計來新增、修改或刪除要求或回應的標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-673">These features are designed to add, modify, or delete headers from the request or response.</span></span>

<span data-ttu-id="3d02c-674">名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-674">Name</span></span> | <span data-ttu-id="3d02c-675">目的</span><span class="sxs-lookup"><span data-stu-id="3d02c-675">Purpose</span></span>
-----|--------
<span data-ttu-id="3d02c-676">Age 回應標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-676">Age Response Header</span></span> | <span data-ttu-id="3d02c-677">判斷 Age 回應標頭是否將包含於傳送到要求者的回應中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-677">Determines whether an Age response header will be included in the response sent to the requester.</span></span>
<span data-ttu-id="3d02c-678">偵錯快取回應標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-678">Debug Cache Response Headers</span></span> | <span data-ttu-id="3d02c-679">判斷回應是否會包含於 X-EC-Debug 回應標頭中，其會在快取原則上提供要求資產的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3d02c-679">Determines whether a response may include the X-EC-Debug response header which provides information on the cache policy for the requested asset.</span></span>
<span data-ttu-id="3d02c-680">修改用戶端要求標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-680">Modify Client Request Header</span></span> | <span data-ttu-id="3d02c-681">覆寫、附加或刪除要求的標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-681">Overwrites, appends, or deletes a header from a request.</span></span>
<span data-ttu-id="3d02c-682">修改用戶端回應標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-682">Modify Client Response Header</span></span> | <span data-ttu-id="3d02c-683">覆寫、附加或刪除回應的標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-683">Overwrites, appends, or deletes a header from a response.</span></span>
<span data-ttu-id="3d02c-684">設定用戶端 IP 自訂標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-684">Set Client IP Custom Header</span></span> | <span data-ttu-id="3d02c-685">允許將要新增到要求的要求用戶端 IP 位址做為自訂要求標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-685">Allows the IP address of the requesting client to be added to the request as a custom request header.</span></span>

###<a name="age-response-header"></a><span data-ttu-id="3d02c-686">Age 回應標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-686">Age Response Header</span></span>
<span data-ttu-id="3d02c-687">**目的：**判斷 Age 回應標頭是否將包含於傳送給要求者的回應中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-687">**Purpose**: Determines whether an Age response header will be included in the response sent to the requester.</span></span>
<span data-ttu-id="3d02c-688">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-688">Value</span></span>|<span data-ttu-id="3d02c-689">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-689">Result</span></span>
--|--
<span data-ttu-id="3d02c-690">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-690">Enabled</span></span> | <span data-ttu-id="3d02c-691">Age 回應標頭將包含於傳送給要求者的回應中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-691">The Age response header will be included in the response sent to the requester.</span></span>
<span data-ttu-id="3d02c-692">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-692">Disabled</span></span> | <span data-ttu-id="3d02c-693">Age 回應標頭將會從傳送給要求者的回應中排除。</span><span class="sxs-lookup"><span data-stu-id="3d02c-693">The Age response header will be excluded from the response sent to the requester.</span></span>

<span data-ttu-id="3d02c-694">**預設行為**：已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-694">**Default Behavior**: Disabled.</span></span>

###<a name="debug-cache-response-headers"></a><span data-ttu-id="3d02c-695">偵錯快取回應標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-695">Debug Cache Response Headers</span></span>
<span data-ttu-id="3d02c-696">**目的：**判斷回應是否會包含 X-EC-Debug 回應標頭，其可在快取原則上提供要求資產的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3d02c-696">**Purpose:** Determines whether a response may include the X-EC-Debug response header which provides information on the cache policy for the requested asset.</span></span>

<span data-ttu-id="3d02c-697">符合下列兩種情況時，將會在回應中包含偵錯快取回應標頭：</span><span class="sxs-lookup"><span data-stu-id="3d02c-697">Debug cache response headers will be included in the response when both of the following are true:</span></span>

- <span data-ttu-id="3d02c-698">已在所需的要求上啟用 [偵錯快取回應標頭] 功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-698">The Debug Cache Response Headers Feature has been enabled on the desired request.</span></span>
- <span data-ttu-id="3d02c-699">上述要求會定義一組將包含於回應中的偵錯快取回應標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-699">The above request defines the set of debug cache response headers that will be included in the response.</span></span>

<span data-ttu-id="3d02c-700">偵錯快取回應標頭可能是藉由在要求中包含下列標頭和所需指示詞來要求：</span><span class="sxs-lookup"><span data-stu-id="3d02c-700">Debug cache response headers may be requested by including the following header and the desired directives in the request:</span></span>

<span data-ttu-id="3d02c-701">X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_</span><span class="sxs-lookup"><span data-stu-id="3d02c-701">X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_</span></span>

<span data-ttu-id="3d02c-702">**範例：**</span><span class="sxs-lookup"><span data-stu-id="3d02c-702">**Example:**</span></span>

<span data-ttu-id="3d02c-703">X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state</span><span class="sxs-lookup"><span data-stu-id="3d02c-703">X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state</span></span>

<span data-ttu-id="3d02c-704">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-704">Value</span></span>|<span data-ttu-id="3d02c-705">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-705">Result</span></span>
-|-
<span data-ttu-id="3d02c-706">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-706">Enabled</span></span>|<span data-ttu-id="3d02c-707">偵錯快取回應標頭的要求將傳回包含 X-EC-Debug 標頭的回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-707">Requests for debug cache response headers will return a response that includes the X-EC-Debug header.</span></span>
<span data-ttu-id="3d02c-708">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-708">Disabled</span></span>|<span data-ttu-id="3d02c-709">X-EC-Debug 回應標頭將會從回應中排除。</span><span class="sxs-lookup"><span data-stu-id="3d02c-709">The X-EC-Debug response header will be excluded from the response.</span></span>

<span data-ttu-id="3d02c-710">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-710">**Default Behavior:** Disabled.</span></span>

###<a name="modify-client-response-header"></a><span data-ttu-id="3d02c-711">修改用戶端回應標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-711">Modify Client Response Header</span></span>
<span data-ttu-id="3d02c-712">**目的︰**每個要求都會包含一組說明其本身的 [要求標頭]()。</span><span class="sxs-lookup"><span data-stu-id="3d02c-712">**Purpose:** Each request contains a set of [request headers]() that describe it.</span></span> <span data-ttu-id="3d02c-713">此功能可以：</span><span class="sxs-lookup"><span data-stu-id="3d02c-713">This feature can either:</span></span>

- <span data-ttu-id="3d02c-714">附加或覆寫指派給要求標頭的值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-714">Append or overwrite the value assigned to a request header.</span></span> <span data-ttu-id="3d02c-715">如果指定的要求標頭不存在，則此功能會將其加入至要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-715">If the specified request header does not exist, then this feature will add it to the request.</span></span>
- <span data-ttu-id="3d02c-716">刪除要求的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-716">Delete a request header from the request.</span></span>

<span data-ttu-id="3d02c-717">要轉送到原始伺服器的要求將會反映此功能所做的變更。</span><span class="sxs-lookup"><span data-stu-id="3d02c-717">Requests that are forwarded to an origin server will reflect the changes made by this feature.</span></span>

<span data-ttu-id="3d02c-718">您可以在要求標頭上執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="3d02c-718">One of the following actions can be performed on a request header:</span></span>

<span data-ttu-id="3d02c-719">選項</span><span class="sxs-lookup"><span data-stu-id="3d02c-719">Option</span></span>|<span data-ttu-id="3d02c-720">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-720">Description</span></span>|<span data-ttu-id="3d02c-721">範例</span><span class="sxs-lookup"><span data-stu-id="3d02c-721">Example</span></span>
-|-|-
<span data-ttu-id="3d02c-722">Append</span><span class="sxs-lookup"><span data-stu-id="3d02c-722">Append</span></span>|<span data-ttu-id="3d02c-723">指定的值將會加入至現有要求標頭值的結尾。</span><span class="sxs-lookup"><span data-stu-id="3d02c-723">The specified value will be added toend of the existing request header value.</span></span>|<span data-ttu-id="3d02c-724">**要求標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="3d02c-724">**Request header value (Client):**Value1</span></span> <br/> <span data-ttu-id="3d02c-725">**要求標頭值 (HTTP 規則引擎)：**Value2</span><span class="sxs-lookup"><span data-stu-id="3d02c-725">**Request header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="3d02c-726">**新的要求標頭值：**Value1Value2</span><span class="sxs-lookup"><span data-stu-id="3d02c-726">**New request header value:** Value1Value2</span></span>
<span data-ttu-id="3d02c-727">覆寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-727">Overwrite</span></span>|<span data-ttu-id="3d02c-728">要求標頭值將會設定為指定的值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-728">The request header value will be set to the specified value.</span></span>|<span data-ttu-id="3d02c-729">**要求標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="3d02c-729">**Request header value (Client):**Value1</span></span> <br/><span data-ttu-id="3d02c-730">**要求標頭值 (HTTP 規則引擎)：**Value2</span><span class="sxs-lookup"><span data-stu-id="3d02c-730">**Request header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="3d02c-731">**新的要求標頭值：**Value2</span><span class="sxs-lookup"><span data-stu-id="3d02c-731">**New request header value:** Value2</span></span> <br/>
<span data-ttu-id="3d02c-732">刪除</span><span class="sxs-lookup"><span data-stu-id="3d02c-732">Delete</span></span>|<span data-ttu-id="3d02c-733">刪除指定的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-733">Deletes the specified request header.</span></span>|<span data-ttu-id="3d02c-734">**要求標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="3d02c-734">**Request header value (Client):**Value1</span></span> <br/> <span data-ttu-id="3d02c-735">**修改用戶端要求標頭組態：**刪除有問題的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-735">**Modify Client Request Header configuration:** Delete the request header in question.</span></span> <br/><span data-ttu-id="3d02c-736">**結果︰**指定的要求標頭將不會轉送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-736">**Result:** The specified request header will not be forwarded to the origin server.</span></span>

<span data-ttu-id="3d02c-737">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-737">Key information:</span></span>

- <span data-ttu-id="3d02c-738">確定 [名稱] 選項中指定的值完全相符所需的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-738">Make sure that the value specified in the Name option is an exact match for the desired request header.</span></span>
- <span data-ttu-id="3d02c-739">基於識別標頭的目的，不會將大小寫納入考量。</span><span class="sxs-lookup"><span data-stu-id="3d02c-739">Case is not taken into account for the purpose of identifying a header.</span></span> <span data-ttu-id="3d02c-740">例如，可以使用 Cache-Control 標頭名稱的下列任一個變化來識別它：</span><span class="sxs-lookup"><span data-stu-id="3d02c-740">For example, any of the following variations of the Cache-Control header name can be used to identify it:</span></span>
    - <span data-ttu-id="3d02c-741">cache-control</span><span class="sxs-lookup"><span data-stu-id="3d02c-741">cache-control</span></span>
    - <span data-ttu-id="3d02c-742">CACHE-CONTROL</span><span class="sxs-lookup"><span data-stu-id="3d02c-742">CACHE-CONTROL</span></span>
    - <span data-ttu-id="3d02c-743">cachE-Control</span><span class="sxs-lookup"><span data-stu-id="3d02c-743">cachE-Control</span></span>
- <span data-ttu-id="3d02c-744">確定在指定標頭名稱時，只會使用英數字元、連字號或底線。</span><span class="sxs-lookup"><span data-stu-id="3d02c-744">Make sure to only use alphanumeric characters, dashes, or underscores when specifying a header name.</span></span>
- <span data-ttu-id="3d02c-745">刪除標頭，可防止 Edge Server 將它轉送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-745">Deleting a header will prevent it from being forwarded to an origin server by our edge servers.</span></span>
- <span data-ttu-id="3d02c-746">以下為保留的標頭，且此功能無法加以修改：</span><span class="sxs-lookup"><span data-stu-id="3d02c-746">The following headers are reserved and cannot be modified by this feature:</span></span>
    - <span data-ttu-id="3d02c-747">forwarded</span><span class="sxs-lookup"><span data-stu-id="3d02c-747">forwarded</span></span>
    - <span data-ttu-id="3d02c-748">主機</span><span class="sxs-lookup"><span data-stu-id="3d02c-748">host</span></span>
    - <span data-ttu-id="3d02c-749">via</span><span class="sxs-lookup"><span data-stu-id="3d02c-749">via</span></span>
    - <span data-ttu-id="3d02c-750">警告</span><span class="sxs-lookup"><span data-stu-id="3d02c-750">warning</span></span>
    - <span data-ttu-id="3d02c-751">x-forwarded-for</span><span class="sxs-lookup"><span data-stu-id="3d02c-751">x-forwarded-for</span></span>
    - <span data-ttu-id="3d02c-752">以「x-ec」開頭的所有標頭名稱都會保留。</span><span class="sxs-lookup"><span data-stu-id="3d02c-752">All header names that start with "x-ec" are reserved.</span></span>

###<a name="modify-client-response-header"></a><span data-ttu-id="3d02c-753">修改用戶端回應標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-753">Modify Client Response Header</span></span>
<span data-ttu-id="3d02c-754">每個回應都包含一組說明其本身的 [回應標頭]()。</span><span class="sxs-lookup"><span data-stu-id="3d02c-754">Each response contains a set of [response headers]() that describe it.</span></span> <span data-ttu-id="3d02c-755">此功能可以：</span><span class="sxs-lookup"><span data-stu-id="3d02c-755">This feature can either:</span></span>

- <span data-ttu-id="3d02c-756">附加或覆寫指派給回應標頭的值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-756">Append or overwrite the value assigned to a response header.</span></span> <span data-ttu-id="3d02c-757">如果指定的要求標頭不存在，則此功能會將其加入至回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-757">If the specified request header does not exist, then this feature will add it to the response.</span></span>
- <span data-ttu-id="3d02c-758">刪除回應的回應標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-758">Delete a response header from the response.</span></span>

<span data-ttu-id="3d02c-759">根據預設，回應標頭值是由原始伺服器和 Edge Server 所定義。</span><span class="sxs-lookup"><span data-stu-id="3d02c-759">By default, response header values are defined by an origin server and by our edge servers.</span></span>

<span data-ttu-id="3d02c-760">您可以在回應標頭上執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="3d02c-760">One of the following actions can be performed on a response header:</span></span>

<span data-ttu-id="3d02c-761">選項</span><span class="sxs-lookup"><span data-stu-id="3d02c-761">Option</span></span>|<span data-ttu-id="3d02c-762">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-762">Description</span></span>|<span data-ttu-id="3d02c-763">範例</span><span class="sxs-lookup"><span data-stu-id="3d02c-763">Example</span></span>
-|-|-
<span data-ttu-id="3d02c-764">Append</span><span class="sxs-lookup"><span data-stu-id="3d02c-764">Append</span></span>|<span data-ttu-id="3d02c-765">指定的值將會加入至現有要求標頭值的結尾。</span><span class="sxs-lookup"><span data-stu-id="3d02c-765">The specified value will be added toend of the existing request header value.</span></span>|<span data-ttu-id="3d02c-766">**回應標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="3d02c-766">**Response header value (Client):**Value1</span></span> <br/> <span data-ttu-id="3d02c-767">**回應標頭值 (HTTP 規則引擎)：**Value2</span><span class="sxs-lookup"><span data-stu-id="3d02c-767">**Response header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="3d02c-768">**新的回應標頭值：**Value1Value2</span><span class="sxs-lookup"><span data-stu-id="3d02c-768">**New Response header value:** Value1Value2</span></span>
<span data-ttu-id="3d02c-769">覆寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-769">Overwrite</span></span>|<span data-ttu-id="3d02c-770">要求標頭值將會設定為指定的值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-770">The request header value will be set to the specified value.</span></span>|<span data-ttu-id="3d02c-771">**回應標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="3d02c-771">**Response header value (Client):**Value1</span></span> <br/><span data-ttu-id="3d02c-772">**回應標頭值 (HTTP 規則引擎)：**Value2</span><span class="sxs-lookup"><span data-stu-id="3d02c-772">**Response header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="3d02c-773">**新的回應標頭值：**Value2</span><span class="sxs-lookup"><span data-stu-id="3d02c-773">**New response header value:** Value2</span></span> <br/>
<span data-ttu-id="3d02c-774">刪除</span><span class="sxs-lookup"><span data-stu-id="3d02c-774">Delete</span></span>|<span data-ttu-id="3d02c-775">刪除指定的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-775">Deletes the specified request header.</span></span>|<span data-ttu-id="3d02c-776">**要求標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="3d02c-776">**Request header value (Client):** Value1</span></span> <br/> <span data-ttu-id="3d02c-777">**修改用戶端要求標頭組態：**刪除有問題的回應標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-777">**Modify Client Request Header configuration:** Delete the response header in question.</span></span> <br/><span data-ttu-id="3d02c-778">**結果︰**指定的回應標頭將不會轉送給要求者。</span><span class="sxs-lookup"><span data-stu-id="3d02c-778">**Result:** The specified response header will not be forwarded to the requester.</span></span>

<span data-ttu-id="3d02c-779">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-779">Key information:</span></span>

- <span data-ttu-id="3d02c-780">確定 [名稱] 選項中指定的值完全相符所需的回應標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-780">Make sure that the value specified in the Name option is an exact match for the desired response header.</span></span> 
- <span data-ttu-id="3d02c-781">基於識別標頭的目的，不會將大小寫納入考量。</span><span class="sxs-lookup"><span data-stu-id="3d02c-781">Case is not taken into account for the purpose of identifying a header.</span></span> <span data-ttu-id="3d02c-782">例如，可以使用 Cache-Control 標頭名稱的下列任一個變化來識別它：</span><span class="sxs-lookup"><span data-stu-id="3d02c-782">For example, any of the following variations of the Cache-Control header name can be used to identify it:</span></span>
    - <span data-ttu-id="3d02c-783">cache-control</span><span class="sxs-lookup"><span data-stu-id="3d02c-783">cache-control</span></span>
    - <span data-ttu-id="3d02c-784">CACHE-CONTROL</span><span class="sxs-lookup"><span data-stu-id="3d02c-784">CACHE-CONTROL</span></span>
    - <span data-ttu-id="3d02c-785">cachE-Control</span><span class="sxs-lookup"><span data-stu-id="3d02c-785">cachE-Control</span></span>
- <span data-ttu-id="3d02c-786">刪除標頭可防止它被轉送給要求者。</span><span class="sxs-lookup"><span data-stu-id="3d02c-786">Deleting a header will prevent it from being forwarded to the requester.</span></span>
- <span data-ttu-id="3d02c-787">以下為保留的標頭，且此功能無法加以修改：</span><span class="sxs-lookup"><span data-stu-id="3d02c-787">The following headers are reserved and cannot be modified by this feature:</span></span>
    - <span data-ttu-id="3d02c-788">accept-encoding</span><span class="sxs-lookup"><span data-stu-id="3d02c-788">accept-encoding</span></span>
    - <span data-ttu-id="3d02c-789">age</span><span class="sxs-lookup"><span data-stu-id="3d02c-789">age</span></span>
    - <span data-ttu-id="3d02c-790">connection</span><span class="sxs-lookup"><span data-stu-id="3d02c-790">connection</span></span>
    - <span data-ttu-id="3d02c-791">content-encoding</span><span class="sxs-lookup"><span data-stu-id="3d02c-791">content-encoding</span></span>
    - <span data-ttu-id="3d02c-792">content-length</span><span class="sxs-lookup"><span data-stu-id="3d02c-792">content-length</span></span>
    - <span data-ttu-id="3d02c-793">content-range</span><span class="sxs-lookup"><span data-stu-id="3d02c-793">content-range</span></span>
    - <span data-ttu-id="3d02c-794">日期</span><span class="sxs-lookup"><span data-stu-id="3d02c-794">date</span></span>
    - <span data-ttu-id="3d02c-795">伺服器</span><span class="sxs-lookup"><span data-stu-id="3d02c-795">server</span></span>
    - <span data-ttu-id="3d02c-796">trailer</span><span class="sxs-lookup"><span data-stu-id="3d02c-796">trailer</span></span>
    - <span data-ttu-id="3d02c-797">transfer-encoding</span><span class="sxs-lookup"><span data-stu-id="3d02c-797">transfer-encoding</span></span>
    - <span data-ttu-id="3d02c-798">升級</span><span class="sxs-lookup"><span data-stu-id="3d02c-798">upgrade</span></span>
    - <span data-ttu-id="3d02c-799">vary</span><span class="sxs-lookup"><span data-stu-id="3d02c-799">vary</span></span>
    - <span data-ttu-id="3d02c-800">via</span><span class="sxs-lookup"><span data-stu-id="3d02c-800">via</span></span>
    - <span data-ttu-id="3d02c-801">警告</span><span class="sxs-lookup"><span data-stu-id="3d02c-801">warning</span></span>
    - <span data-ttu-id="3d02c-802">以「x-ec」開頭的所有標頭名稱都會保留。</span><span class="sxs-lookup"><span data-stu-id="3d02c-802">All header names that start with "x-ec" are reserved.</span></span>

###<a name="set-client-ip-custom-header"></a><span data-ttu-id="3d02c-803">設定用戶端 IP 自訂標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-803">Set Client IP Custom Header</span></span>
<span data-ttu-id="3d02c-804">**目的︰**依 IP 位址識別要求用戶端的自訂標頭加入至要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-804">**Purpose:** Adds a custom header that identifies the requesting client by IP address to the request.</span></span>

<span data-ttu-id="3d02c-805">[標頭名稱] 選項會定義將儲存用戶端 IP 位址的自訂要求標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-805">The Header name option defines the name of the custom request header where the client's IP address will be stored.</span></span>

<span data-ttu-id="3d02c-806">此功能讓客戶原始伺服器能夠透過自訂要求標頭找出用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3d02c-806">This feature allows a customer origin server to find out client IP addresses through a custom request header.</span></span> <span data-ttu-id="3d02c-807">如果是從快取提供要求，則不會將用戶端的 IP 位址告知原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-807">If the request is served from cache, then the origin server will not be informed of the client's IP address.</span></span> <span data-ttu-id="3d02c-808">因此，建議將此功能與 ADN 或不會快取的資產搭配使用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-808">Therefore, it is recommended that this feature be used with ADN or assets that will not be cached.</span></span>

<span data-ttu-id="3d02c-809">請確定指定的標頭名稱不會符合下列任一項：</span><span class="sxs-lookup"><span data-stu-id="3d02c-809">Please make sure that the specified header name does not match any of the following:</span></span>

- <span data-ttu-id="3d02c-810">標準要求標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-810">Standard request header names.</span></span> <span data-ttu-id="3d02c-811">您可以在 [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) 中找到標準標頭名稱清單。</span><span class="sxs-lookup"><span data-stu-id="3d02c-811">A list of standard header names can be found in [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span></span>
- <span data-ttu-id="3d02c-812">保留的標頭名稱：</span><span class="sxs-lookup"><span data-stu-id="3d02c-812">Reserved header names:</span></span>
    - <span data-ttu-id="3d02c-813">forwarded-for</span><span class="sxs-lookup"><span data-stu-id="3d02c-813">forwarded-for</span></span>
    - <span data-ttu-id="3d02c-814">主機</span><span class="sxs-lookup"><span data-stu-id="3d02c-814">host</span></span>
    - <span data-ttu-id="3d02c-815">vary</span><span class="sxs-lookup"><span data-stu-id="3d02c-815">vary</span></span>
    - <span data-ttu-id="3d02c-816">via</span><span class="sxs-lookup"><span data-stu-id="3d02c-816">via</span></span>
    - <span data-ttu-id="3d02c-817">警告</span><span class="sxs-lookup"><span data-stu-id="3d02c-817">warning</span></span>
    - <span data-ttu-id="3d02c-818">x-forwarded-for</span><span class="sxs-lookup"><span data-stu-id="3d02c-818">x-forwarded-for</span></span>
    - <span data-ttu-id="3d02c-819">以「x-ec」開頭的所有標頭名稱都會保留。</span><span class="sxs-lookup"><span data-stu-id="3d02c-819">All header names that start with "x-ec" are reserved.</span></span>
 
## <a name="logs"></a><span data-ttu-id="3d02c-820">記錄檔</span><span class="sxs-lookup"><span data-stu-id="3d02c-820">Logs</span></span>

<span data-ttu-id="3d02c-821">這些功能是設計來自訂儲存於原始記錄檔中的資料。</span><span class="sxs-lookup"><span data-stu-id="3d02c-821">These features are designed to customize the data stored in raw log files.</span></span>

<span data-ttu-id="3d02c-822">名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-822">Name</span></span> | <span data-ttu-id="3d02c-823">目的</span><span class="sxs-lookup"><span data-stu-id="3d02c-823">Purpose</span></span>
-----|--------
<span data-ttu-id="3d02c-824">自訂記錄欄位 1</span><span class="sxs-lookup"><span data-stu-id="3d02c-824">Custom Log Field 1</span></span> | <span data-ttu-id="3d02c-825">判斷將指派給原始記錄檔中自訂記錄欄位的格式和內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-825">Determines the format and the content that will be assigned to the custom log field in a raw log file.</span></span>
<span data-ttu-id="3d02c-826">記錄查詢字串</span><span class="sxs-lookup"><span data-stu-id="3d02c-826">Log Query String</span></span> | <span data-ttu-id="3d02c-827">判斷查詢字串以及 URL 是否將一起儲存於存取記錄中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-827">Determines whether a query string will be stored along with the URL in access logs.</span></span>

###<a name="custom-log-field-1"></a><span data-ttu-id="3d02c-828">自訂記錄欄位 1</span><span class="sxs-lookup"><span data-stu-id="3d02c-828">Custom Log Field 1</span></span>
<span data-ttu-id="3d02c-829">**目的：**判斷將指派給原始記錄檔中自訂記錄欄位的格式和內容。</span><span class="sxs-lookup"><span data-stu-id="3d02c-829">**Purpose:** Determines the format and the content that will be assigned to the custom log field in a raw log file.</span></span>

<span data-ttu-id="3d02c-830">此自訂欄位背後的主要目的是讓您能夠判斷哪些要求和回應標頭值將儲存於記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-830">The main purpose behind this custom field is to allow you to determine which request and response header values will be stored in your log files.</span></span>

<span data-ttu-id="3d02c-831">根據預設，自訂記錄欄位稱為「x-ec_custom-1」。</span><span class="sxs-lookup"><span data-stu-id="3d02c-831">By default, the custom log field is called "x-ec_custom-1."</span></span> <span data-ttu-id="3d02c-832">不過，您可以從 [未經處理記錄設定]() 頁面自訂此欄位的名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-832">However, the name of this field can be customized from the [Raw Log Settings page]().</span></span>

<span data-ttu-id="3d02c-833">您應該用來指定要求和回應標頭格式設定的定義如下。</span><span class="sxs-lookup"><span data-stu-id="3d02c-833">The formatting that you should use to specify request and response headers is defined below.</span></span>

<span data-ttu-id="3d02c-834">標頭類型</span><span class="sxs-lookup"><span data-stu-id="3d02c-834">Header Type</span></span>|<span data-ttu-id="3d02c-835">格式</span><span class="sxs-lookup"><span data-stu-id="3d02c-835">Format</span></span>|<span data-ttu-id="3d02c-836">範例</span><span class="sxs-lookup"><span data-stu-id="3d02c-836">Examples</span></span>
-|-|-
<span data-ttu-id="3d02c-837">要求標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-837">Request Header</span></span>|<span data-ttu-id="3d02c-838">%{[RequestHeader]()}[i]()</span><span class="sxs-lookup"><span data-stu-id="3d02c-838">%{[RequestHeader]()}[i]()</span></span> | <span data-ttu-id="3d02c-839">%{Accept-Encoding}i</span><span class="sxs-lookup"><span data-stu-id="3d02c-839">%{Accept-Encoding}i</span></span> <br/> <span data-ttu-id="3d02c-840">{Referer}i</span><span class="sxs-lookup"><span data-stu-id="3d02c-840">{Referer}i</span></span> <br/> <span data-ttu-id="3d02c-841">%{Authorization}i</span><span class="sxs-lookup"><span data-stu-id="3d02c-841">%{Authorization}i</span></span>
<span data-ttu-id="3d02c-842">回應標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-842">Response Header</span></span>|<span data-ttu-id="3d02c-843">%{[ResponseHeader]()}[o]()</span><span class="sxs-lookup"><span data-stu-id="3d02c-843">%{[ResponseHeader]()}[o]()</span></span>| <span data-ttu-id="3d02c-844">%{Age}o</span><span class="sxs-lookup"><span data-stu-id="3d02c-844">%{Age}o</span></span> <br/> <span data-ttu-id="3d02c-845">%{Content-Type}o</span><span class="sxs-lookup"><span data-stu-id="3d02c-845">%{Content-Type}o</span></span> <br/> <span data-ttu-id="3d02c-846">%{Cookie}o</span><span class="sxs-lookup"><span data-stu-id="3d02c-846">%{Cookie}o</span></span>

<span data-ttu-id="3d02c-847">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-847">Key information:</span></span>

- <span data-ttu-id="3d02c-848">自訂記錄欄位可包含標頭欄位和純文字的任意組合。</span><span class="sxs-lookup"><span data-stu-id="3d02c-848">A custom log field can contain any combination of header fields and plain text.</span></span>
- <span data-ttu-id="3d02c-849">此欄位的有效字元包括下列各項：英數字元 (亦即，0-9、a-z 和 A-Z)、連字號、冒號、分號、單引號、逗號、句號、底線、等號、括弧、中括弧和空格。</span><span class="sxs-lookup"><span data-stu-id="3d02c-849">Valid characters for this field include the following: alphanumeric (i.e., 0-9, a-z, and A-Z), dashes, colons, semi-colons, apostrophes, commas, periods, underscores, equal signs, parentheses, brackets, and spaces.</span></span> <span data-ttu-id="3d02c-850">只有在用於指定標頭欄位時，才能使用百分比符號和大括弧。</span><span class="sxs-lookup"><span data-stu-id="3d02c-850">The percentage symbol and curly braces are only allowed when used to specify a header field.</span></span>
- <span data-ttu-id="3d02c-851">每個指定標頭欄位的拼字都必須符合所需的要求/回應標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-851">The spelling for each specified header field must match the desired request/response header name.</span></span>
- <span data-ttu-id="3d02c-852">如果您想要指定多個標頭，則建議您使用分隔符號來表示每個標頭。</span><span class="sxs-lookup"><span data-stu-id="3d02c-852">If you would like to specify multiple headers, then it is recommended that you use a separator to indicate each header.</span></span> <span data-ttu-id="3d02c-853">例如，您可以針對每個標頭使用縮寫。</span><span class="sxs-lookup"><span data-stu-id="3d02c-853">For example, you could use an abbreviation for each header.</span></span> <span data-ttu-id="3d02c-854">範例語法如下所示。</span><span class="sxs-lookup"><span data-stu-id="3d02c-854">Sample syntax is provided below.</span></span>
    - <span data-ttu-id="3d02c-855">AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o</span><span class="sxs-lookup"><span data-stu-id="3d02c-855">AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o</span></span> 

<span data-ttu-id="3d02c-856">**預設值：** -</span><span class="sxs-lookup"><span data-stu-id="3d02c-856">**Default Value:** -</span></span>

###<a name="log-query-string"></a><span data-ttu-id="3d02c-857">記錄查詢字串</span><span class="sxs-lookup"><span data-stu-id="3d02c-857">Log Query String</span></span>
<span data-ttu-id="3d02c-858">**目的：**判斷查詢字串是否將與 URL 一起儲存於存取記錄中。</span><span class="sxs-lookup"><span data-stu-id="3d02c-858">**Purpose:** Determines whether a query string will be stored along with the URL in access logs.</span></span>

<span data-ttu-id="3d02c-859">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-859">Value</span></span>|<span data-ttu-id="3d02c-860">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-860">Result</span></span>
-|-
<span data-ttu-id="3d02c-861">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-861">Enabled</span></span>|<span data-ttu-id="3d02c-862">在存取記錄中記錄 URL 時，允許儲存查詢字串。</span><span class="sxs-lookup"><span data-stu-id="3d02c-862">Allows the storage of query strings when recording URLs in an access log.</span></span> <span data-ttu-id="3d02c-863">如果 URL 未包含查詢字串，則此選項將不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-863">If a URL does not contain a query string, then this option will not have an effect.</span></span>
<span data-ttu-id="3d02c-864">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-864">Disabled</span></span>|<span data-ttu-id="3d02c-865">還原預設行為。</span><span class="sxs-lookup"><span data-stu-id="3d02c-865">Restores the default behavior.</span></span> <span data-ttu-id="3d02c-866">預設行為是在存取記錄中記錄 URL 時忽略查詢字串。</span><span class="sxs-lookup"><span data-stu-id="3d02c-866">The default behavior is to ignore query strings when recording URLs in an access log.</span></span>

<span data-ttu-id="3d02c-867">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-867">**Default Behavior:** Disabled.</span></span>

<!---
## Optimize

These features determine whether a request will undergo the optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied to a request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates the Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied to a request.

If this feature has been enabled, then the following criteria must also be met before the request will be processed by Edge Optimizer:

- The requested content must use an edge CNAME URL.
- The edge CNAME referenced in the URL must correspond to a site whose configuration has been activated in a rule.

This feature requires the ADN platform and the Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that the request is eligible for Edge Optimizer processing.
Disabled|Restores the default behavior. The default behavior is to deliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates the Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and the Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests to the corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs to be performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until the Edge Optimizer – Instantiate Configuration feature that references it is removed from the rule.
- The instantiation of a site configuration does not mean that all requests to the corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If the desired site does not appear in the list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a><span data-ttu-id="3d02c-868">來源</span><span class="sxs-lookup"><span data-stu-id="3d02c-868">Origin</span></span>

<span data-ttu-id="3d02c-869">這些功能是設計來控制 CDN 與原始伺服器通訊的方式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-869">These features are designed to control how the CDN communicates with an origin server.</span></span>

<span data-ttu-id="3d02c-870">名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-870">Name</span></span> | <span data-ttu-id="3d02c-871">目的</span><span class="sxs-lookup"><span data-stu-id="3d02c-871">Purpose</span></span>
-----|--------
<span data-ttu-id="3d02c-872">Keep-Alive 要求的最大值</span><span class="sxs-lookup"><span data-stu-id="3d02c-872">Maximum Keep-Alive Requests</span></span> | <span data-ttu-id="3d02c-873">判斷在關閉 Keep-Alive 連線之前，適用於該連線的最大要求數目。</span><span class="sxs-lookup"><span data-stu-id="3d02c-873">Defines the maximum number of requests for a Keep-Alive connection before it is closed.</span></span>
<span data-ttu-id="3d02c-874">Proxy 特定的標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-874">Proxy Special Headers</span></span> | <span data-ttu-id="3d02c-875">定義將從 Edge Server 轉送到原始伺服器之 CDN 特定的要求標頭組。</span><span class="sxs-lookup"><span data-stu-id="3d02c-875">Defines the set of CDN-specific request headers that will be forwarded from an edge server to an origin server.</span></span>


###<a name="maximum-keep-alive-requests"></a><span data-ttu-id="3d02c-876">Keep-Alive 要求的最大值</span><span class="sxs-lookup"><span data-stu-id="3d02c-876">Maximum Keep-Alive Requests</span></span>
<span data-ttu-id="3d02c-877">**目的：**判斷在關閉 Keep-Alive 連線之前，適用於該連線的最大要求數目。</span><span class="sxs-lookup"><span data-stu-id="3d02c-877">**Purpose:** Defines the maximum number of requests for a Keep-Alive connection before it is closed.</span></span>

<span data-ttu-id="3d02c-878">強烈建議您不要將要求數目上限設為較低的值，這樣可能會導致效能變差。</span><span class="sxs-lookup"><span data-stu-id="3d02c-878">Setting the maximum number of requests to a low value is strongly discouraged and may result in performance degradation.</span></span>

<span data-ttu-id="3d02c-879">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-879">Key information:</span></span>

- <span data-ttu-id="3d02c-880">將此值指定為整數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-880">Specify this value as a whole integer.</span></span>
- <span data-ttu-id="3d02c-881">請勿在指定的值中包含逗號或句號。</span><span class="sxs-lookup"><span data-stu-id="3d02c-881">Do not include commas or periods in the specified value.</span></span>

<span data-ttu-id="3d02c-882">**預設值︰**10,000 個要求</span><span class="sxs-lookup"><span data-stu-id="3d02c-882">**Default Value:** 10,000 requests</span></span>

###<a name="proxy-special-headers"></a><span data-ttu-id="3d02c-883">Proxy 特定的標頭</span><span class="sxs-lookup"><span data-stu-id="3d02c-883">Proxy Special Headers</span></span>
<span data-ttu-id="3d02c-884">**目的：**定義一組將從 Edge Server 轉送到原始伺服器之 [CDN 特定的要求標頭]()。</span><span class="sxs-lookup"><span data-stu-id="3d02c-884">**Purpose:** Defines the set of [CDN-specific request headers]() that will be forwarded from an edge server to an origin server.</span></span>

<span data-ttu-id="3d02c-885">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-885">Key information:</span></span>

- <span data-ttu-id="3d02c-886">此功能中定義的每個 CDN 特定要求標頭都將轉送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-886">Each CDN-specific request header defined in this feature will be forwarded to an origin server.</span></span>
- <span data-ttu-id="3d02c-887">從此清單中移除 CDN 特定的要求標頭，藉以防止將其轉送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-887">Prevent a CDN-specific request header from being forwarded to an origin server by removing it from this list.</span></span>

<span data-ttu-id="3d02c-888">**預設行為︰**所有 [CDN 特定的要求標頭]() 都將轉送到原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="3d02c-888">**Default Behavior:** All [CDN-specific request headers]() will be forwarded to the origin server.</span></span>

## <a name="specialty"></a><span data-ttu-id="3d02c-889">特殊性</span><span class="sxs-lookup"><span data-stu-id="3d02c-889">Specialty</span></span>

<span data-ttu-id="3d02c-890">這些功能提供的進階功能僅可供進階使用者使用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-890">These features provide advanced functionality that should only be used by advanced users.</span></span>

<span data-ttu-id="3d02c-891">名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-891">Name</span></span> | <span data-ttu-id="3d02c-892">目的</span><span class="sxs-lookup"><span data-stu-id="3d02c-892">Purpose</span></span>
-----|--------
<span data-ttu-id="3d02c-893">可快取的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="3d02c-893">Cacheable HTTP Methods</span></span> | <span data-ttu-id="3d02c-894">判斷可在我們的網路上快取的其他 HTTP 方法組。</span><span class="sxs-lookup"><span data-stu-id="3d02c-894">Determines the set of additional HTTP methods that can be cached on our network.</span></span>
<span data-ttu-id="3d02c-895">可快取的要求主體大小</span><span class="sxs-lookup"><span data-stu-id="3d02c-895">Cacheable Request Body Size</span></span> | <span data-ttu-id="3d02c-896">定義用以判斷是否可快取 POST 回應的臨界值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-896">Defines the threshold for determining whether a POST response can be cached.</span></span>

###<a name="cacheable-http-methods"></a><span data-ttu-id="3d02c-897">可快取的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="3d02c-897">Cacheable HTTP Methods</span></span>
<span data-ttu-id="3d02c-898">**目的：**判斷一組可在網路上快取的其他 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="3d02c-898">**Purpose:** Determines the set of additional HTTP methods that can be cached on our network.</span></span>

<span data-ttu-id="3d02c-899">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-899">Key information:</span></span>

- <span data-ttu-id="3d02c-900">此功能假設應一律快取 GET 回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-900">This feature assumes that GET responses should always be cached.</span></span> <span data-ttu-id="3d02c-901">如此一來，在設定此功能時，就不應包含 GET HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="3d02c-901">As a result, the GET HTTP method should not be included when setting this feature.</span></span>
- <span data-ttu-id="3d02c-902">此功能僅支援 POST HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="3d02c-902">This feature only supports the POST HTTP method.</span></span> <span data-ttu-id="3d02c-903">將此功能設定為：POST，藉以啟用 POST 回應快取</span><span class="sxs-lookup"><span data-stu-id="3d02c-903">Enable POST response caching by setting this feature to:POST</span></span> 
- <span data-ttu-id="3d02c-904">根據預設，只會快取主體小於 14 Kb 的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-904">By default, only requests whose body is smaller than 14 Kb will be cached.</span></span> <span data-ttu-id="3d02c-905">使用 [可快取的要求主體大小] 功能來設定要求主體大小上限。</span><span class="sxs-lookup"><span data-stu-id="3d02c-905">Use the Cacheable Request Body Size Feature to set the maximum request body size.</span></span>

<span data-ttu-id="3d02c-906">**預設行為︰**只會快取 GET 回應。</span><span class="sxs-lookup"><span data-stu-id="3d02c-906">**Default Behavior:** Only GET responses will be cached.</span></span>

###<a name="cacheable-request-body-size"></a><span data-ttu-id="3d02c-907">可快取的要求主體大小</span><span class="sxs-lookup"><span data-stu-id="3d02c-907">Cacheable Request Body Size</span></span>

<span data-ttu-id="3d02c-908">**目的：**定義用以判斷是否可快取 POST 回應的臨界值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-908">**Purpose:** Defines the threshold for determining whether a POST response can be cached.</span></span>

<span data-ttu-id="3d02c-909">此臨界值是藉由指定要求主體大小上限來決定。</span><span class="sxs-lookup"><span data-stu-id="3d02c-909">This threshold is determined by specifying a maximum request body size.</span></span> <span data-ttu-id="3d02c-910">系統將不會快取包含較大要求主體的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-910">Requests that contain a larger request body will not be cached.</span></span>

<span data-ttu-id="3d02c-911">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-911">Key information:</span></span>

- <span data-ttu-id="3d02c-912">只有在 POST 回應適合用來快取時，才適用此功能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-912">This Feature is only applicable when POST responses are eligible for caching.</span></span> <span data-ttu-id="3d02c-913">使用 [可快取的 HTTP 方法] 功能來啟用 POST 要求快取。</span><span class="sxs-lookup"><span data-stu-id="3d02c-913">Use the Cacheable HTTP Methods Feature to enable POST request caching.</span></span>
- <span data-ttu-id="3d02c-914">已針對下列項目將要求主體納入考量：</span><span class="sxs-lookup"><span data-stu-id="3d02c-914">The request body is taken into consideration for:</span></span>
    - <span data-ttu-id="3d02c-915">x-www-form-urlencoded 值</span><span class="sxs-lookup"><span data-stu-id="3d02c-915">x-www-form-urlencoded values</span></span>
    - <span data-ttu-id="3d02c-916">確保唯一的快取索引鍵</span><span class="sxs-lookup"><span data-stu-id="3d02c-916">Ensuring a unique cache-key</span></span>
- <span data-ttu-id="3d02c-917">定義大型的要求主體大小上限可能會影響資料傳遞效能。</span><span class="sxs-lookup"><span data-stu-id="3d02c-917">Defining a large maximum request body size may impact data delivery performance.</span></span>
    - <span data-ttu-id="3d02c-918">**建議值：**14 Kb</span><span class="sxs-lookup"><span data-stu-id="3d02c-918">**Recommended Value:** 14 Kb</span></span>
    - <span data-ttu-id="3d02c-919">**最小值︰**1 Kb</span><span class="sxs-lookup"><span data-stu-id="3d02c-919">**Minimum Value:** 1 Kb</span></span>

<span data-ttu-id="3d02c-920">**預設行為︰**14 Kb</span><span class="sxs-lookup"><span data-stu-id="3d02c-920">**Default Behavior:** 14 Kb</span></span>
 
## <a name="url"></a><span data-ttu-id="3d02c-921">URL</span><span class="sxs-lookup"><span data-stu-id="3d02c-921">URL</span></span>

<span data-ttu-id="3d02c-922">這些功能可讓要求重新導向至不同的 URL 或重寫為不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-922">These features allow a request to be redirected or rewritten to a different URL.</span></span>

<span data-ttu-id="3d02c-923">名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-923">Name</span></span> | <span data-ttu-id="3d02c-924">目的</span><span class="sxs-lookup"><span data-stu-id="3d02c-924">Purpose</span></span>
-----|--------
<span data-ttu-id="3d02c-925">遵循重新導向</span><span class="sxs-lookup"><span data-stu-id="3d02c-925">Follow Redirects</span></span> | <span data-ttu-id="3d02c-926">判斷要求是否可以重新導向至定義於客戶原始伺服器所傳回之位置標頭中的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-926">Determines whether requests can be redirected to the hostname defined in the Location header returned by a customer origin server.</span></span>
<span data-ttu-id="3d02c-927">[URL 重新導向]</span><span class="sxs-lookup"><span data-stu-id="3d02c-927">URL Redirect</span></span> | <span data-ttu-id="3d02c-928">透過位置標頭將要求重新導向。</span><span class="sxs-lookup"><span data-stu-id="3d02c-928">Redirects requests via the Location header.</span></span>
<span data-ttu-id="3d02c-929">URL 重寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-929">URL Rewrite</span></span>  | <span data-ttu-id="3d02c-930">重寫要求 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-930">Rewrites the request URL.</span></span>

###<a name="follow-redirects"></a><span data-ttu-id="3d02c-931">遵循重新導向</span><span class="sxs-lookup"><span data-stu-id="3d02c-931">Follow Redirects</span></span>
<span data-ttu-id="3d02c-932">**目的：**判斷是否可將要求重新導向至定義於客戶原始伺服器所傳回之位置標頭中的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-932">**Purpose:** Determines whether requests can be redirected to the hostname defined in the Location header returned by a customer origin server.</span></span>

<span data-ttu-id="3d02c-933">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-933">Key information:</span></span>

- <span data-ttu-id="3d02c-934">您只能將要求重新導向至對應到相同平台的 Edge CNAME。</span><span class="sxs-lookup"><span data-stu-id="3d02c-934">Requests can only be redirected to edge CNAMEs that correspond to the same platform.</span></span>

<span data-ttu-id="3d02c-935">值</span><span class="sxs-lookup"><span data-stu-id="3d02c-935">Value</span></span>|<span data-ttu-id="3d02c-936">結果</span><span class="sxs-lookup"><span data-stu-id="3d02c-936">Result</span></span>
-|-
<span data-ttu-id="3d02c-937">已啟用</span><span class="sxs-lookup"><span data-stu-id="3d02c-937">Enabled</span></span>|<span data-ttu-id="3d02c-938">要求可重新導向。</span><span class="sxs-lookup"><span data-stu-id="3d02c-938">Requests can be redirected.</span></span>
<span data-ttu-id="3d02c-939">已停用</span><span class="sxs-lookup"><span data-stu-id="3d02c-939">Disabled</span></span>|<span data-ttu-id="3d02c-940">要求將不會重新導向。</span><span class="sxs-lookup"><span data-stu-id="3d02c-940">Requests will not be redirected.</span></span>

<span data-ttu-id="3d02c-941">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="3d02c-941">**Default Behavior:** Disabled.</span></span>
###<a name="url-redirect"></a><span data-ttu-id="3d02c-942">[URL 重新導向]</span><span class="sxs-lookup"><span data-stu-id="3d02c-942">URL Redirect</span></span>
<span data-ttu-id="3d02c-943">**目的：**透過位置標頭來將要求重新導向。</span><span class="sxs-lookup"><span data-stu-id="3d02c-943">**Purpose:** Redirects requests via the Location header.</span></span>

<span data-ttu-id="3d02c-944">此功能的組態必須設定下列選項：</span><span class="sxs-lookup"><span data-stu-id="3d02c-944">The configuration of this feature requires setting the following options:</span></span>

<span data-ttu-id="3d02c-945">選項</span><span class="sxs-lookup"><span data-stu-id="3d02c-945">Option</span></span>|<span data-ttu-id="3d02c-946">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-946">Description</span></span>
-|-
<span data-ttu-id="3d02c-947">代碼</span><span class="sxs-lookup"><span data-stu-id="3d02c-947">Code</span></span>|<span data-ttu-id="3d02c-948">選取將傳回給要求者的回應碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-948">Select the response code that will be returned to the requester.</span></span>
<span data-ttu-id="3d02c-949">來源與模式</span><span class="sxs-lookup"><span data-stu-id="3d02c-949">Source & Pattern</span></span>| <span data-ttu-id="3d02c-950">這些設定會定義要求 URI 模式，此模式會識別可能要重新導向的要求類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-950">These settings define a request URI pattern that identifies the type of requests that may be redirected.</span></span> <span data-ttu-id="3d02c-951">只會重新導向 URL 符合下列這兩個準則的要求：</span><span class="sxs-lookup"><span data-stu-id="3d02c-951">Only requests whose URL satisfies both of the following criteria will be redirected:</span></span> <br/> <br/> <span data-ttu-id="3d02c-952">**來源︰**(或內容存取點) 選取識別原始伺服器的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="3d02c-952">**Source :** (or content access point) Select a relative path that identifies an origin server.</span></span> <span data-ttu-id="3d02c-953">這是「/XXXX/」區段和您的端點名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-953">This is the  "/XXXX/" section and your endpoint name.</span></span> <br/> <span data-ttu-id="3d02c-954">**來源 (模式)︰**必須定義依相對路徑識別要求的模式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-954">**Source (pattern):** A pattern that identifies requests by relative path must be defined.</span></span> <span data-ttu-id="3d02c-955">這個規則運算式模式必須定義一個路徑，該路徑會在先前選取的內容存取點 (請參閱上述內容) 之後直接啟動。</span><span class="sxs-lookup"><span data-stu-id="3d02c-955">This regular expression pattern must define a path that starts directly after the previously selected content access point (see above).</span></span> <br/> <span data-ttu-id="3d02c-956">- 確定上述定義的要求 URI 準則 (例如 [來源與模式]) 不會與針對此功能所定義的任何比對條件相衝突。</span><span class="sxs-lookup"><span data-stu-id="3d02c-956">- Make sure that the request URI criteria (i.e., Source & Pattern) defined above doesn't conflict with any match conditions defined for this feature.</span></span> <br/> <span data-ttu-id="3d02c-957">- 務必指定模式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-957">- Make sure to specify a pattern.</span></span> <span data-ttu-id="3d02c-958">使用空白值做為模式，只會將要求與所選取原始伺服器的根資料夾 (例如 http://cdn.mydomain.com/) 進行比對。</span><span class="sxs-lookup"><span data-stu-id="3d02c-958">Using a blank value as the pattern will only match requests to the root folder of the selected origin server (e.g., http://cdn.mydomain.com/).</span></span>
<span data-ttu-id="3d02c-959">目的地</span><span class="sxs-lookup"><span data-stu-id="3d02c-959">Destination</span></span>| <span data-ttu-id="3d02c-960">定義要將上述要求重新導向至其中的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-960">Define the URL to which the above requests will be redirected.</span></span> <br/> <span data-ttu-id="3d02c-961">使用下列方式來動態建構此 URL：</span><span class="sxs-lookup"><span data-stu-id="3d02c-961">Dynamically construct this URL using:</span></span> <br/> <span data-ttu-id="3d02c-962">- 規則運算式模式</span><span class="sxs-lookup"><span data-stu-id="3d02c-962">- A regular expression pattern</span></span> <br/><span data-ttu-id="3d02c-963">- HTTP 變數</span><span class="sxs-lookup"><span data-stu-id="3d02c-963">- HTTP variables</span></span> <br/> <span data-ttu-id="3d02c-964">替代擷取的來源模式中使用 $ 目的圖樣值_n_ 其中 _n_ 識別值，由它所擷取的順序。</span><span class="sxs-lookup"><span data-stu-id="3d02c-964">Substitute the values captured in the source pattern into the destination pattern using $_n_ where _n_ identifies a value by the order in which it was captured.</span></span> <span data-ttu-id="3d02c-965">例如，$1 表示擷取自來源模式的第一個值，而 $2 代表第二個值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-965">For example, $1 represents the first value captured in the source pattern, while $2 represents the second value.</span></span> <br/> 
<span data-ttu-id="3d02c-966">強烈建議使用絕對 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-966">It is highly recommended to use an absolute URL.</span></span> <span data-ttu-id="3d02c-967">使用相對 URL 可能會將 CDN URL 重新導向至不正確的路徑。</span><span class="sxs-lookup"><span data-stu-id="3d02c-967">The use of a relative URL may redirect CDN URLs to an invalid path.</span></span>

<span data-ttu-id="3d02c-968">**範例案例**</span><span class="sxs-lookup"><span data-stu-id="3d02c-968">**Sample Scenario**</span></span>

<span data-ttu-id="3d02c-969">在此範例中，我們會示範如何將解析為下列基底 CDN URL 的 Edge CNAME URL 重新導向：http://marketing.azureedge.net/brochures</span><span class="sxs-lookup"><span data-stu-id="3d02c-969">In this example, we will demonstrate how to redirect an edge CNAME URL that resolves to this base CDN URL: http://marketing.azureedge.net/brochures</span></span>

<span data-ttu-id="3d02c-970">符合資格的要求將會重新導向至此基底 Edge CNAME URL：http://cdn.mydomain.com/resources</span><span class="sxs-lookup"><span data-stu-id="3d02c-970">Qualifying requests will be redirected to this base edge CNAME URL: http://cdn.mydomain.com/resources</span></span>

<span data-ttu-id="3d02c-971">此 URL 重新導向可透過下列組態來達成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)</span><span class="sxs-lookup"><span data-stu-id="3d02c-971">This URL redirection may be achieved through the following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)</span></span>

<span data-ttu-id="3d02c-972">**重點︰**</span><span class="sxs-lookup"><span data-stu-id="3d02c-972">**Key points:**</span></span>

- <span data-ttu-id="3d02c-973">[URL 重新導向] 功能會定義將重新導向的要求 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-973">The URL Redirect feature defines the request URLs that will be redirected.</span></span> <span data-ttu-id="3d02c-974">如此一來，就不需要額外的比對條件。</span><span class="sxs-lookup"><span data-stu-id="3d02c-974">As a result, additional match conditions are not required.</span></span> <span data-ttu-id="3d02c-975">雖然將比對條件定義為 [一律]，但只會重新導向指向 [marketing] 客戶原始伺服器上 [brochures] 資料夾的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-975">Although the match condition was defined as "Always," only requests that point to the "brochures" folder on the "marketing" customer origin will be redirected.</span></span> 
- <span data-ttu-id="3d02c-976">所有相符的要求都將重新導向到 [目的地] 選項中所定義的 Edge CNAME URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-976">All matching requests will be redirected to the edge CNAME URL defined in the Destination option.</span></span> 
    - <span data-ttu-id="3d02c-977">範例案例 1：</span><span class="sxs-lookup"><span data-stu-id="3d02c-977">Sample scenario #1:</span></span> 
        - <span data-ttu-id="3d02c-978">範例要求 (CDN URL)：http://marketing.azureedge.net/brochures/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="3d02c-978">Sample request (CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf</span></span> 
        - <span data-ttu-id="3d02c-979">要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="3d02c-979">Request URL (after redirect): http://cdn.mydomain.com/resources/widgets.pdf</span></span>  
    - <span data-ttu-id="3d02c-980">範例案例 2：</span><span class="sxs-lookup"><span data-stu-id="3d02c-980">Sample scenario #2:</span></span> 
        - <span data-ttu-id="3d02c-981">範例要求 (Edge CNAME URL)：http://marketing.mydomain.com/brochures/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="3d02c-981">Sample request (Edge CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf</span></span> 
        - <span data-ttu-id="3d02c-982">要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/widgets.pdf 範例案例</span><span class="sxs-lookup"><span data-stu-id="3d02c-982">Request URL (after redirect): http://cdn.mydomain.com/resources/widgets.pdf  Sample scenario</span></span>
    - <span data-ttu-id="3d02c-983">範例案例 3：</span><span class="sxs-lookup"><span data-stu-id="3d02c-983">Sample scenario #3:</span></span> 
        - <span data-ttu-id="3d02c-984">範例要求 (Edge CNAME URL)：http://brochures.mydomain.com/campaignA/final/productC.ppt</span><span class="sxs-lookup"><span data-stu-id="3d02c-984">Sample request (Edge CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt</span></span> 
        - <span data-ttu-id="3d02c-985">要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/campaignA/final/productC.ppt</span><span class="sxs-lookup"><span data-stu-id="3d02c-985">Request URL (after redirect): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt</span></span>  
- <span data-ttu-id="3d02c-986">已在 [目的地] 選項中運用要求配置 (%{scheme}) 變數。</span><span class="sxs-lookup"><span data-stu-id="3d02c-986">The Request Scheme (%{scheme}) variable was leveraged in the Destination option.</span></span> <span data-ttu-id="3d02c-987">這可確保要求的配置在重新導向之後仍會維持不變。</span><span class="sxs-lookup"><span data-stu-id="3d02c-987">This ensures that the request's scheme remains unchanged after redirection.</span></span>
- <span data-ttu-id="3d02c-988">擷取自要求的 URL 區段會透過「$1」附加到新的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-988">The URL segments that were captured from the request are appended to the new URL via "$1."</span></span>
 
###<a name="url-rewrite"></a><span data-ttu-id="3d02c-989">URL 重寫</span><span class="sxs-lookup"><span data-stu-id="3d02c-989">URL Rewrite</span></span>
<span data-ttu-id="3d02c-990">**目的：**重寫要求 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-990">**Purpose:** Rewrites the request URL.</span></span>

<span data-ttu-id="3d02c-991">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="3d02c-991">Key information:</span></span>

- <span data-ttu-id="3d02c-992">此功能的組態必須設定下列選項：</span><span class="sxs-lookup"><span data-stu-id="3d02c-992">The configuration of this feature requires setting the following options:</span></span>

<span data-ttu-id="3d02c-993">選項</span><span class="sxs-lookup"><span data-stu-id="3d02c-993">Option</span></span>|<span data-ttu-id="3d02c-994">說明</span><span class="sxs-lookup"><span data-stu-id="3d02c-994">Description</span></span>
-|-
 <span data-ttu-id="3d02c-995">來源與模式</span><span class="sxs-lookup"><span data-stu-id="3d02c-995">Source & Pattern</span></span> | <span data-ttu-id="3d02c-996">這些設定會定義要求 URI 模式，此模式會識別可能要重寫的要求類型。</span><span class="sxs-lookup"><span data-stu-id="3d02c-996">These settings define a request URI pattern that identifies the type of requests that may be rewritten.</span></span> <span data-ttu-id="3d02c-997">只會重寫 URL 符合下列這兩個準則的要求：</span><span class="sxs-lookup"><span data-stu-id="3d02c-997">Only requests whose URL satisfies both of the following criteria will be rewritten:</span></span> <br/>     <span data-ttu-id="3d02c-998">- **來源 (或內容存取點)：**選取識別原始伺服器的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="3d02c-998">- **Source (or content access point):** Select a relative path that identifies an origin server.</span></span> <span data-ttu-id="3d02c-999">這是「/XXXX/」區段和您的端點名稱。</span><span class="sxs-lookup"><span data-stu-id="3d02c-999">This is the  "/XXXX/" section and your endpoint name.</span></span> <br/> <span data-ttu-id="3d02c-1000">- **來源 (模式)︰**必須定義依相對路徑識別要求的模式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1000">- **Source (pattern):** A pattern that identifies requests by relative path must be defined.</span></span> <span data-ttu-id="3d02c-1001">這個規則運算式模式必須定義一個路徑，該路徑會在先前選取的內容存取點 (請參閱上述內容) 之後直接啟動。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1001">This regular expression pattern must define a path that starts directly after the previously selected content access point (see above).</span></span> <br/> <span data-ttu-id="3d02c-1002">確定上述定義的要求 URI 準則 (例如 [來源與模式]) 不會與針對此功能所定義的任何比對條件相衝突。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1002">Make sure that the request URI criteria (i.e., Source & Pattern) defined above doesn't conflict with any of the match conditions defined for this feature.</span></span> <span data-ttu-id="3d02c-1003">務必指定模式。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1003">Make sure to specify a pattern.</span></span> <span data-ttu-id="3d02c-1004">使用空白值做為模式，只會將要求與所選取原始伺服器的根資料夾 (例如 http://cdn.mydomain.com/) 進行比對。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1004">Using a blank value as the pattern will only match requests to the root folder of the selected origin server (e.g., http://cdn.mydomain.com/).</span></span> 
 <span data-ttu-id="3d02c-1005">目的地</span><span class="sxs-lookup"><span data-stu-id="3d02c-1005">Destination</span></span>  |<span data-ttu-id="3d02c-1006">使用下列方式來定義要將上述要求重寫至其中的相對 URL：</span><span class="sxs-lookup"><span data-stu-id="3d02c-1006">Define the relative URL to which the above requests will be rewritten by:</span></span> <br/>    <span data-ttu-id="3d02c-1007">1.選取可識別原始伺服器的內容存取點。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1007">1. Selecting a content access point that identifies an origin server.</span></span> <br/>    <span data-ttu-id="3d02c-1008">2.使用下列方式來定義相對路徑：</span><span class="sxs-lookup"><span data-stu-id="3d02c-1008">2. Defining a relative path using:</span></span> <br/>        <span data-ttu-id="3d02c-1009">- 規則運算式模式</span><span class="sxs-lookup"><span data-stu-id="3d02c-1009">- A regular expression pattern</span></span> <br/>        <span data-ttu-id="3d02c-1010">- HTTP 變數</span><span class="sxs-lookup"><span data-stu-id="3d02c-1010">- HTTP variables</span></span> <br/> <br/> <span data-ttu-id="3d02c-1011">替代擷取的來源模式中使用 $ 目的圖樣值_n_ 其中 _n_ 識別值，由它所擷取的順序。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1011">Substitute the values captured in the source pattern into the destination pattern using $_n_ where _n_ identifies a value by the order in which it was captured.</span></span> <span data-ttu-id="3d02c-1012">例如，$1 表示擷取自來源模式的第一個值，而 $2 代表第二個值。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1012">For example, $1 represents the first value captured in the source pattern, while $2 represents the second value.</span></span> 
 <span data-ttu-id="3d02c-1013">此功能讓 Edge Server 不需執行傳統的重新導向就能重寫 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1013">This feature allows our edge servers to rewrite the URL without performing a traditional redirect.</span></span> <span data-ttu-id="3d02c-1014">這表示，如果收到重寫 URL 的要求，要求者將會收到相同的回應碼。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1014">This means that the requester will receive the same response code as if the rewritten URL had been requested.</span></span>

<span data-ttu-id="3d02c-1015">**範例案例 1**</span><span class="sxs-lookup"><span data-stu-id="3d02c-1015">**Sample Scenario 1**</span></span>

<span data-ttu-id="3d02c-1016">在此範例中，我們會示範如何將解析為下列基底 CDN URL 的 Edge CNAME URL 重新導向：http://marketing.azureedge.net/brochures/</span><span class="sxs-lookup"><span data-stu-id="3d02c-1016">In this example, we will demonstrate how to redirect an edge CNAME URL that resolves to this base CDN URL: http://marketing.azureedge.net/brochures/</span></span>

<span data-ttu-id="3d02c-1017">符合資格的要求將會重新導向至此基底 Edge CNAME URL：http://MyOrigin.azureedge.net/resources/</span><span class="sxs-lookup"><span data-stu-id="3d02c-1017">Qualifying requests will be redirected to this base edge CNAME URL: http://MyOrigin.azureedge.net/resources/</span></span>

<span data-ttu-id="3d02c-1018">此 URL 重新導向可透過下列組態來達成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)</span><span class="sxs-lookup"><span data-stu-id="3d02c-1018">This URL redirection may be achieved through the following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)</span></span>

<span data-ttu-id="3d02c-1019">**範例案例 2**</span><span class="sxs-lookup"><span data-stu-id="3d02c-1019">**Sample Scenario 2**</span></span>

<span data-ttu-id="3d02c-1020">在此範例中，我們將示範如何使用規則運算式，將邊緣 CNAME URL 從「大寫」重新導向到小寫。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1020">In this example, we will demonstrate how to redirect an edge CNAME URL from UPPERCASE to lowercase using regular expressions.</span></span>

<span data-ttu-id="3d02c-1021">此 URL 重新導向可透過下列組態來達成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)</span><span class="sxs-lookup"><span data-stu-id="3d02c-1021">This URL redirection may be achieved through the following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)</span></span>


<span data-ttu-id="3d02c-1022">**重點︰**</span><span class="sxs-lookup"><span data-stu-id="3d02c-1022">**Key points:**</span></span>

- <span data-ttu-id="3d02c-1023">[URL 重寫] 功能會定義將要重寫的要求 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1023">The URL Rewrite feature defines the request URLs that will be rewritten.</span></span> <span data-ttu-id="3d02c-1024">如此一來，就不需要額外的比對條件。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1024">As a result, additional match conditions are not required.</span></span> <span data-ttu-id="3d02c-1025">雖然將比對條件定義為 [一律]，但只會重寫指向 [marketing] 客戶原始伺服器上 [brochures] 資料夾的要求。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1025">Although the match condition was defined as "Always," only requests that point to the "brochures" folder on the "marketing" customer origin will be rewritten.</span></span>

- <span data-ttu-id="3d02c-1026">擷取自要求的 URL 區段會透過「$1」附加到新的 URL。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1026">The URL segments that were captured from the request are appended to the new URL via "$1."</span></span>



###<a name="compatibility"></a><span data-ttu-id="3d02c-1027">相容性</span><span class="sxs-lookup"><span data-stu-id="3d02c-1027">Compatibility</span></span>

<span data-ttu-id="3d02c-1028">此功能包括必須符合才能套用到要求的比對準則。</span><span class="sxs-lookup"><span data-stu-id="3d02c-1028">This feature includes matching criteria that must be met before it can be applied to a request.</span></span> <span data-ttu-id="3d02c-1029">為了防止設定衝突的比對準則，此功能與下列比對條件不相容：</span><span class="sxs-lookup"><span data-stu-id="3d02c-1029">In order to prevent setting up conflicting match criteria, this feature is incompatible with the following match conditions:</span></span>

- <span data-ttu-id="3d02c-1030">AS 號碼</span><span class="sxs-lookup"><span data-stu-id="3d02c-1030">AS Number</span></span>
- <span data-ttu-id="3d02c-1031">CDN 原點</span><span class="sxs-lookup"><span data-stu-id="3d02c-1031">CDN Origin</span></span>
- <span data-ttu-id="3d02c-1032">用戶端 IP 位址</span><span class="sxs-lookup"><span data-stu-id="3d02c-1032">Client IP Address</span></span>
- <span data-ttu-id="3d02c-1033">客戶原點</span><span class="sxs-lookup"><span data-stu-id="3d02c-1033">Customer Origin</span></span>
- <span data-ttu-id="3d02c-1034">要求配置</span><span class="sxs-lookup"><span data-stu-id="3d02c-1034">Request Scheme</span></span>
- <span data-ttu-id="3d02c-1035">URL 路徑目錄</span><span class="sxs-lookup"><span data-stu-id="3d02c-1035">URL Path Directory</span></span>
- <span data-ttu-id="3d02c-1036">URL 路徑的副檔名</span><span class="sxs-lookup"><span data-stu-id="3d02c-1036">URL Path Extension</span></span>
- <span data-ttu-id="3d02c-1037">URL 路徑的檔案名稱</span><span class="sxs-lookup"><span data-stu-id="3d02c-1037">URL Path Filename</span></span>
- <span data-ttu-id="3d02c-1038">URL 路徑常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-1038">URL Path Literal</span></span>
- <span data-ttu-id="3d02c-1039">URL 路徑 Regex</span><span class="sxs-lookup"><span data-stu-id="3d02c-1039">URL Path Regex</span></span>
- <span data-ttu-id="3d02c-1040">URL 路徑萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-1040">URL Path Wildcard</span></span>
- <span data-ttu-id="3d02c-1041">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="3d02c-1041">URL Query Literal</span></span>
- <span data-ttu-id="3d02c-1042">URL 查詢參數</span><span class="sxs-lookup"><span data-stu-id="3d02c-1042">URL Query Parameter</span></span>
- <span data-ttu-id="3d02c-1043">URL 查詢 Regex</span><span class="sxs-lookup"><span data-stu-id="3d02c-1043">URL Query Regex</span></span>
- <span data-ttu-id="3d02c-1044">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="3d02c-1044">URL Query Wildcard</span></span>


## <a name="next-steps"></a><span data-ttu-id="3d02c-1045">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d02c-1045">Next Steps</span></span>
* [<span data-ttu-id="3d02c-1046">規則引擎參考 (英文)</span><span class="sxs-lookup"><span data-stu-id="3d02c-1046">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="3d02c-1047">規則引擎條件式運算式 (英文)</span><span class="sxs-lookup"><span data-stu-id="3d02c-1047">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="3d02c-1048">規則引擎比對條件 (英文)</span><span class="sxs-lookup"><span data-stu-id="3d02c-1048">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="3d02c-1049">使用規則引擎覆寫預設的 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="3d02c-1049">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* [<span data-ttu-id="3d02c-1050">Azure CDN 概觀</span><span class="sxs-lookup"><span data-stu-id="3d02c-1050">Azure CDN Overview</span></span>](cdn-overview.md)
