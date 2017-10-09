---
title: "aaaAzure CDN 規則引擎功能 |Microsoft 文件"
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
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a><span data-ttu-id="5ba58-103">Azure CDN 規則引擎功能</span><span class="sxs-lookup"><span data-stu-id="5ba58-103">Azure CDN rules engine features</span></span>
<span data-ttu-id="5ba58-104">本主題列出的詳細的描述 hello 可用功能的 Azure 內容傳遞網路 (CDN)[規則引擎](cdn-rules-engine.md)。</span><span class="sxs-lookup"><span data-stu-id="5ba58-104">This topic lists detailed descriptions of hello available features for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="5ba58-105">規則的 hello 第三個部分是 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-105">hello third part of a rule is hello feature.</span></span> <span data-ttu-id="5ba58-106">一個功能可定義 hello 類型的動作將會套用 toohello 類型的一組符合條件所識別的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-106">A feature defines hello type of action that will be applied toohello type of request identified by a set of match conditions.</span></span>

## <a name="access"></a><span data-ttu-id="5ba58-107">Access</span><span class="sxs-lookup"><span data-stu-id="5ba58-107">Access</span></span>

<span data-ttu-id="5ba58-108">這些功能是設計的 toocontrol 存取 toocontent。</span><span class="sxs-lookup"><span data-stu-id="5ba58-108">These features are designed toocontrol access toocontent.</span></span>


<span data-ttu-id="5ba58-109">名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-109">Name</span></span> | <span data-ttu-id="5ba58-110">目的</span><span class="sxs-lookup"><span data-stu-id="5ba58-110">Purpose</span></span>
-----|--------
<span data-ttu-id="5ba58-111">拒絕存取</span><span class="sxs-lookup"><span data-stu-id="5ba58-111">Deny Access</span></span> | <span data-ttu-id="5ba58-112">判斷所有要求是否已遭拒絕且含有 [403 禁止] 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-112">Determines whether all requests are rejected with a 403 Forbidden response.</span></span>
<span data-ttu-id="5ba58-113">權杖驗證</span><span class="sxs-lookup"><span data-stu-id="5ba58-113">Token Auth</span></span> | <span data-ttu-id="5ba58-114">決定是否權杖型驗證會套用的 tooa 要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-114">Determines whether Token-Based Authentication will be applied tooa request.</span></span>
<span data-ttu-id="5ba58-115">權杖驗證拒絕代碼</span><span class="sxs-lookup"><span data-stu-id="5ba58-115">Token Auth Denial Code</span></span> | <span data-ttu-id="5ba58-116">決定時，會傳回 tooa 使用者要求遭到拒絕因為 tooToken 型驗證的回應 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="5ba58-116">Determines hello type of response that will be returned tooa user when a request is denied due tooToken-Based Authentication.</span></span>
<span data-ttu-id="5ba58-117">權杖驗證會忽略 URL 的大小寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-117">Token Auth Ignore URL Case</span></span> | <span data-ttu-id="5ba58-118">判斷透過權杖型驗證所做的 URL 比較是否會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5ba58-118">Determines whether URL comparisons made by Token-Based Authentication will be case-sensitive.</span></span>
<span data-ttu-id="5ba58-119">權杖驗證參數</span><span class="sxs-lookup"><span data-stu-id="5ba58-119">Token Auth Parameter</span></span> | <span data-ttu-id="5ba58-120">決定是否應該重新命名 hello 權杖型驗證查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-120">Determines whether hello Token-Based Authentication query string parameter should be renamed.</span></span>

### <a name="deny-access"></a><span data-ttu-id="5ba58-121">拒絕存取</span><span class="sxs-lookup"><span data-stu-id="5ba58-121">Deny Access</span></span>
<span data-ttu-id="5ba58-122">**目的**：判斷所有要求是否已遭拒且含有 [403 禁止] 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-122">**Purpose**: Determines whether all requests are rejected with a 403 Forbidden response.</span></span>

<span data-ttu-id="5ba58-123">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-123">Value</span></span> | <span data-ttu-id="5ba58-124">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-124">Result</span></span>
------|-------
<span data-ttu-id="5ba58-125">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-125">Enabled</span></span>| <span data-ttu-id="5ba58-126">會導致滿足 hello 403 禁止回應以拒絕比對準則 toobe 的所有要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-126">Causes all requests that satisfy hello matching criteria toobe rejected with a 403 Forbidden response.</span></span>
<span data-ttu-id="5ba58-127">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-127">Disabled</span></span>| <span data-ttu-id="5ba58-128">還原 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-128">Restores hello default behavior.</span></span> <span data-ttu-id="5ba58-129">hello 預設行為是回應的 tooallow hello 原始伺服器 toodetermine hello 類型將傳回。</span><span class="sxs-lookup"><span data-stu-id="5ba58-129">hello default behavior is tooallow hello origin server toodetermine hello type of response that will be returned.</span></span>

<span data-ttu-id="5ba58-130">**預設行為**：已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-130">**Default Behavior**: Disabled</span></span>

> [!TIP]
   > <span data-ttu-id="5ba58-131">這項功能的其中一個可能的使用是 tooassociate 它具有要求標頭比對條件 tooblock 存取 tooHTTP 推薦者 」 使用內嵌連結 tooyour 內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-131">One possible use for this feature is tooassociate it with a Request Header match condition tooblock access tooHTTP referrers that are using inline links tooyour content.</span></span>

### <a name="token-auth"></a><span data-ttu-id="5ba58-132">權杖驗證</span><span class="sxs-lookup"><span data-stu-id="5ba58-132">Token Auth</span></span>
<span data-ttu-id="5ba58-133">**用途：**判斷權杖型驗證是否會套用的 tooa 要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-133">**Purpose:** Determines whether Token-Based Authentication will be applied tooa request.</span></span>

<span data-ttu-id="5ba58-134">如果已啟用權杖型驗證，則採用提供加密的權杖，且必須符合該語彙基元指定 toohello 需求的唯一要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-134">If Token-Based Authentication is enabled, then only requests that provide an encrypted token and comply toohello requirements specified by that token will be honored.</span></span>

<span data-ttu-id="5ba58-135">hello 加密金鑰，將會使用的 tooencrypt 和解密的語彙基元值取決於主索引鍵和權杖驗證頁面上的備份金鑰選項。</span><span class="sxs-lookup"><span data-stu-id="5ba58-135">hello encryption key that will be used tooencrypt and decrypt token values is determined by the Primary Key and the Backup Key options on the Token Auth page.</span></span> <span data-ttu-id="5ba58-136">請記住，加密金鑰是特定平台的。</span><span class="sxs-lookup"><span data-stu-id="5ba58-136">Keep in mind that encryption keys are platform-specific.</span></span>

<span data-ttu-id="5ba58-137">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-137">Value</span></span> | <span data-ttu-id="5ba58-138">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-138">Result</span></span>
------|---------
<span data-ttu-id="5ba58-139">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-139">Enabled</span></span> | <span data-ttu-id="5ba58-140">保護 hello 要求使用權杖型驗證的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-140">Protects hello requested content with Token-Based Authentication.</span></span> <span data-ttu-id="5ba58-141">只接受來自用戶端且可提供有效權杖並符合其需求的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-141">Only requests from clients that provide a valid token and meet its requirements will be honored.</span></span> <span data-ttu-id="5ba58-142">FTP 交易會從權杖型驗證中排除。</span><span class="sxs-lookup"><span data-stu-id="5ba58-142">FTP transactions are excluded from Token-Based Authentication.</span></span>
<span data-ttu-id="5ba58-143">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-143">Disabled</span></span>| <span data-ttu-id="5ba58-144">還原 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-144">Restores hello default behavior.</span></span> <span data-ttu-id="5ba58-145">hello 預設行為是 tooallow 您權杖為基礎的驗證組態 toodetermine 是否要求將會受到保護。</span><span class="sxs-lookup"><span data-stu-id="5ba58-145">hello default behavior is tooallow your Token-Based Authentication configuration toodetermine whether a request will be secured.</span></span>

<span data-ttu-id="5ba58-146">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-146">**Default Behavior:** Disabled.</span></span>

###<a name="token-auth-denial-code"></a><span data-ttu-id="5ba58-147">權杖驗證拒絕代碼</span><span class="sxs-lookup"><span data-stu-id="5ba58-147">Token Auth Denial Code</span></span>
<span data-ttu-id="5ba58-148">**用途：**判斷 hello 回應時，會傳回 tooa 使用者要求遭到拒絕因為 tooToken 為基礎的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="5ba58-148">**Purpose:** Determines hello type of response that will be returned tooa user when a request is denied due tooToken-Based Authentication.</span></span>

<span data-ttu-id="5ba58-149">hello 可用的回應碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ba58-149">hello available response codes are listed below.</span></span>

<span data-ttu-id="5ba58-150">回應碼</span><span class="sxs-lookup"><span data-stu-id="5ba58-150">Response Code</span></span>|<span data-ttu-id="5ba58-151">回應名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-151">Response Name</span></span>|<span data-ttu-id="5ba58-152">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-152">Description</span></span>
----------------|-----------|--------
<span data-ttu-id="5ba58-153">301</span><span class="sxs-lookup"><span data-stu-id="5ba58-153">301</span></span>|<span data-ttu-id="5ba58-154">已永久移動</span><span class="sxs-lookup"><span data-stu-id="5ba58-154">Moved Permanently</span></span>|<span data-ttu-id="5ba58-155">此狀態碼會重新導向位置標頭中指定的未經授權的使用者 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-155">This status code redirects unauthorized users toohello URL specified in the Location header.</span></span>
<span data-ttu-id="5ba58-156">302</span><span class="sxs-lookup"><span data-stu-id="5ba58-156">302</span></span>|<span data-ttu-id="5ba58-157">已找到</span><span class="sxs-lookup"><span data-stu-id="5ba58-157">Found</span></span>|<span data-ttu-id="5ba58-158">此狀態碼會重新導向位置標頭中指定的未經授權的使用者 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-158">This status code redirects unauthorized users toohello URL specified in the Location header.</span></span> <span data-ttu-id="5ba58-159">此狀態碼是 hello 執行重新導向的業界標準方法。</span><span class="sxs-lookup"><span data-stu-id="5ba58-159">This status code is hello industry standard method of performing a redirect.</span></span>
<span data-ttu-id="5ba58-160">307</span><span class="sxs-lookup"><span data-stu-id="5ba58-160">307</span></span>|<span data-ttu-id="5ba58-161">暫時重新導向</span><span class="sxs-lookup"><span data-stu-id="5ba58-161">Temporary Redirect</span></span>|<span data-ttu-id="5ba58-162">此狀態碼會重新導向位置標頭中指定的未經授權的使用者 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-162">This status code redirects unauthorized users toohello URL specified in the Location header.</span></span>
<span data-ttu-id="5ba58-163">401</span><span class="sxs-lookup"><span data-stu-id="5ba58-163">401</span></span>|<span data-ttu-id="5ba58-164">未經授權</span><span class="sxs-lookup"><span data-stu-id="5ba58-164">Unauthorized</span></span>|<span data-ttu-id="5ba58-165">此狀態碼結合 WWW 驗證回應標頭可讓您 tooprompt 用於驗證的使用者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-165">Combining this status code with the WWW-Authenticate response header allows you tooprompt a user for authentication.</span></span>
<span data-ttu-id="5ba58-166">403</span><span class="sxs-lookup"><span data-stu-id="5ba58-166">403</span></span>|<span data-ttu-id="5ba58-167">禁止</span><span class="sxs-lookup"><span data-stu-id="5ba58-167">Forbidden</span></span>|<span data-ttu-id="5ba58-168">這是 hello 標準 403 禁止狀態訊息未經授權的使用者會看到當嘗試 tooaccess 受保護的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-168">This is hello standard 403 Forbidden status message that an unauthorized user will see when trying tooaccess protected content.</span></span>
<span data-ttu-id="5ba58-169">404</span><span class="sxs-lookup"><span data-stu-id="5ba58-169">404</span></span>|<span data-ttu-id="5ba58-170">找不到檔案</span><span class="sxs-lookup"><span data-stu-id="5ba58-170">File Not Found</span></span>|<span data-ttu-id="5ba58-171">此狀態碼表示 hello HTTP 用戶端可以 toocommunicate 與 hello 伺服器，但找不到內容的 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-171">This status code indicates that hello HTTP client was able toocommunicate with hello server, but hello requested content was not found.</span></span>

#### <a name="url-redirection"></a><span data-ttu-id="5ba58-172">URL 重新導向</span><span class="sxs-lookup"><span data-stu-id="5ba58-172">URL Redirection</span></span>

<span data-ttu-id="5ba58-173">此功能支援 URL 重新導向 tooa 使用者定義的 URL 時設定的 tooreturn 3xx 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-173">This feature supports URL redirection tooa user-defined URL when it is configured tooreturn a 3xx status code.</span></span> <span data-ttu-id="5ba58-174">藉由執行下列步驟的 hello，您可以指定這個使用者定義的 URL:</span><span class="sxs-lookup"><span data-stu-id="5ba58-174">This user-defined URL can be specified by performing hello following steps:</span></span>

1. <span data-ttu-id="5ba58-175">選取 hello 權杖驗證拒絕程式碼功能的 3xx 回應碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-175">Select a 3xx response code for hello Token Auth Denial Code feature.</span></span>
2. <span data-ttu-id="5ba58-176">從 [選用標頭名稱] 選項中選取 [位置]。</span><span class="sxs-lookup"><span data-stu-id="5ba58-176">Select "Location" from the Optional Header Name option.</span></span>
3. <span data-ttu-id="5ba58-177">選擇性標頭值選項 toohello 集所需的 URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-177">Set the Optional Header Value option toohello desired URL.</span></span>

<span data-ttu-id="5ba58-178">如果未針對 3xx 狀態碼定義 URL，然後 hello 3xx 狀態碼的標準回應頁面將會傳回 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-178">If a URL is not defined for a 3xx status code, then hello standard response page for a 3xx status code will be returned toohello user.</span></span>

<span data-ttu-id="5ba58-179">URL 重新導向只適用於 3xx 回應碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-179">URL redirection is only applicable for 3xx response codes.</span></span>

<span data-ttu-id="5ba58-180">[選用標頭值] 選項支援英數字元、引號和空格。</span><span class="sxs-lookup"><span data-stu-id="5ba58-180">The Optional Header Value option supports alphanumeric characters, quotation marks, and spaces.</span></span>

#### <a name="authentication"></a><span data-ttu-id="5ba58-181">驗證</span><span class="sxs-lookup"><span data-stu-id="5ba58-181">Authentication</span></span>

<span data-ttu-id="5ba58-182">回應 tooan 未經授權之要求的權杖型驗證所保護的內容時，此功能支援 hello 功能 tooinclude WWW 驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-182">This feature supports hello capability tooinclude the WWW-Authenticate header when responding tooan unauthorized request for content protected by Token-Based Authentication.</span></span> <span data-ttu-id="5ba58-183">Www-authenticate 標頭已設定太 「 基本 」 組態中，如果 hello 未經授權的使用者將會提示帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="5ba58-183">If the WWW-Authenticate header has been set too"basic" in your configuration, then hello unauthorized user will be prompted for account credentials.</span></span>

<span data-ttu-id="5ba58-184">上述組態的 hello 可藉由執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-184">hello above configuration can be achieved by performing hello following steps:</span></span>

1. <span data-ttu-id="5ba58-185">選取 「 401 」 做為 hello 回應 hello 權杖驗證拒絕程式碼功能程式碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-185">Select "401" as hello response code for hello Token Auth Denial Code feature.</span></span>
2. <span data-ttu-id="5ba58-186">從 [選用標頭名稱] 選項中選取 [WWW-Authenticate]。</span><span class="sxs-lookup"><span data-stu-id="5ba58-186">Select "WWW-Authenticate" from the Optional Header Name option.</span></span>
3. <span data-ttu-id="5ba58-187">將選擇性標頭值選項設定為太 「 基本。 」</span><span class="sxs-lookup"><span data-stu-id="5ba58-187">Set the Optional Header Value option too"basic."</span></span>

<span data-ttu-id="5ba58-188">WWW-Authenticate 標頭只適用於 401 回應碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-188">The WWW-Authenticate header is only applicable for 401 response codes.</span></span>

### <a name="token-auth-ignore-url-case"></a><span data-ttu-id="5ba58-189">權杖驗證會忽略 URL 的大小寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-189">Token Auth Ignore URL Case</span></span>
<span data-ttu-id="5ba58-190">**目的：**判斷透過權杖型驗證所做的 URL 比較是否會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5ba58-190">**Purpose:** Determines whether URL comparisons made by Token-Based Authentication will be case-sensitive.</span></span>

<span data-ttu-id="5ba58-191">這項功能會受到 hello 參數如下：</span><span class="sxs-lookup"><span data-stu-id="5ba58-191">hello parameters affected by this feature are:</span></span>

- <span data-ttu-id="5ba58-192">ec_url_allow</span><span class="sxs-lookup"><span data-stu-id="5ba58-192">ec_url_allow</span></span>
- <span data-ttu-id="5ba58-193">ec_ref_allow</span><span class="sxs-lookup"><span data-stu-id="5ba58-193">ec_ref_allow</span></span>
- <span data-ttu-id="5ba58-194">ec_ref_deny</span><span class="sxs-lookup"><span data-stu-id="5ba58-194">ec_ref_deny</span></span>

<span data-ttu-id="5ba58-195">有效值為：</span><span class="sxs-lookup"><span data-stu-id="5ba58-195">Valid values are:</span></span>

<span data-ttu-id="5ba58-196">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-196">Value</span></span>|<span data-ttu-id="5ba58-197">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-197">Result</span></span>
---|----
<span data-ttu-id="5ba58-198">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-198">Enabled</span></span>|<span data-ttu-id="5ba58-199">時，讓我們的邊緣伺服器 tooignore 案例比較權杖型驗證參數的 Url。</span><span class="sxs-lookup"><span data-stu-id="5ba58-199">Causes our edge server tooignore case when comparing URLs for Token-Based Authentication parameters.</span></span>
<span data-ttu-id="5ba58-200">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-200">Disabled</span></span>|<span data-ttu-id="5ba58-201">還原 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-201">Restores hello default behavior.</span></span> <span data-ttu-id="5ba58-202">hello 預設行為是讓 URL 權杖驗證 toobe 區分大小寫的比較。</span><span class="sxs-lookup"><span data-stu-id="5ba58-202">hello default behavior is for URL comparisons for Token Authentication toobe case-sensitive.</span></span>

<span data-ttu-id="5ba58-203">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-203">**Default Behavior:** Disabled.</span></span>
 
### <a name="token-auth-parameter"></a><span data-ttu-id="5ba58-204">權杖驗證參數</span><span class="sxs-lookup"><span data-stu-id="5ba58-204">Token Auth Parameter</span></span>
<span data-ttu-id="5ba58-205">**用途：**決定是否應該重新命名 hello 權杖型驗證查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-205">**Purpose:** Determines whether hello Token-Based Authentication query string parameter should be renamed.</span></span>

<span data-ttu-id="5ba58-206">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-206">Key information:</span></span>

- <span data-ttu-id="5ba58-207">[值] 選項定義可能會指定權杖的 hello 查詢字串參數名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-207">The Value option defines hello query string parameter name through which a token may be specified.</span></span>
- <span data-ttu-id="5ba58-208">[值] 選項無法設定得 「 ec_token。 」</span><span class="sxs-lookup"><span data-stu-id="5ba58-208">The Value option cannot be set too"ec_token."</span></span>
- <span data-ttu-id="5ba58-209">請確定 [值] 選項只有在定義該 hello 名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-209">Make sure that hello name defined in the Value option only</span></span> 
- <span data-ttu-id="5ba58-210">包含有效的 URL 字元。</span><span class="sxs-lookup"><span data-stu-id="5ba58-210">contains valid URL characters.</span></span>

<span data-ttu-id="5ba58-211">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-211">Value</span></span>|<span data-ttu-id="5ba58-212">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-212">Result</span></span>
----|----
<span data-ttu-id="5ba58-213">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-213">Enabled</span></span>|<span data-ttu-id="5ba58-214">[值] 選項定義 hello 查詢字串參數名稱應該要定義語彙基元。</span><span class="sxs-lookup"><span data-stu-id="5ba58-214">The Value option defines hello query string parameter name through which tokens should be defined.</span></span>
<span data-ttu-id="5ba58-215">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-215">Disabled</span></span>|<span data-ttu-id="5ba58-216">語彙基元可指定為 hello 要求 URL 中未定義的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-216">A token may be specified as an undefined query string parameter in hello request URL.</span></span>

<span data-ttu-id="5ba58-217">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-217">**Default Behavior:** Disabled.</span></span> <span data-ttu-id="5ba58-218">語彙基元可指定為 hello 要求 URL 中未定義的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-218">A token may be specified as an undefined query string parameter in hello request URL.</span></span>

## <a name="caching"></a><span data-ttu-id="5ba58-219">快取</span><span class="sxs-lookup"><span data-stu-id="5ba58-219">Caching</span></span>

<span data-ttu-id="5ba58-220">這些功能是設計的 toocustomize 何時及如何快取的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-220">These features are designed toocustomize when and how content is cached.</span></span>

<span data-ttu-id="5ba58-221">名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-221">Name</span></span> | <span data-ttu-id="5ba58-222">目的</span><span class="sxs-lookup"><span data-stu-id="5ba58-222">Purpose</span></span>
-----|--------
<span data-ttu-id="5ba58-223">頻寬參數</span><span class="sxs-lookup"><span data-stu-id="5ba58-223">Bandwidth Parameters</span></span> | <span data-ttu-id="5ba58-224">判斷是否將會使用頻寬節流設定參數 (例如 ec_rate 和 ec_prebuf)。</span><span class="sxs-lookup"><span data-stu-id="5ba58-224">Determines whether bandwidth throttling parameters (i.e., ec_rate and ec_prebuf) will be active.</span></span>
<span data-ttu-id="5ba58-225">頻寬節流設定</span><span class="sxs-lookup"><span data-stu-id="5ba58-225">Bandwidth Throttling</span></span> | <span data-ttu-id="5ba58-226">我們的邊緣伺服器所提供的 hello 回應 hello 頻寬節流同時間。</span><span class="sxs-lookup"><span data-stu-id="5ba58-226">Throttles hello bandwidth for hello response provided by our edge servers.</span></span>
<span data-ttu-id="5ba58-227">略過快取</span><span class="sxs-lookup"><span data-stu-id="5ba58-227">Bypass Cache</span></span> | <span data-ttu-id="5ba58-228">決定 hello 要求是否可以利用我們的快取技術。</span><span class="sxs-lookup"><span data-stu-id="5ba58-228">Determines whether hello request can leverage our caching technology.</span></span>
<span data-ttu-id="5ba58-229">Cache-Control 標頭處理</span><span class="sxs-lookup"><span data-stu-id="5ba58-229">Cache-Control Header Treatment</span></span> | <span data-ttu-id="5ba58-230">控制項 hello hello 邊緣伺服器所產生的快取控制標頭，外部 Max-age 功能正在作用中時。</span><span class="sxs-lookup"><span data-stu-id="5ba58-230">Controls hello generation of Cache-Control headers by hello edge server when External Max-Age feature is active.</span></span>
<span data-ttu-id="5ba58-231">快取索引鍵查詢字串</span><span class="sxs-lookup"><span data-stu-id="5ba58-231">Cache-Key Query String</span></span> | <span data-ttu-id="5ba58-232">決定 hello 快取索引鍵是否會包含或排除與要求相關聯的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-232">Determines whether hello cache-key will include or exclude query string parameters associated with a request.</span></span>
<span data-ttu-id="5ba58-233">快取索引鍵重寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-233">Cache-Key Rewrite</span></span> | <span data-ttu-id="5ba58-234">重寫 hello 快取索引鍵與要求相關聯。</span><span class="sxs-lookup"><span data-stu-id="5ba58-234">Rewrites hello cache-key associated with a request.</span></span>
<span data-ttu-id="5ba58-235">完成快取填滿</span><span class="sxs-lookup"><span data-stu-id="5ba58-235">Complete Cache Fill</span></span> | <span data-ttu-id="5ba58-236">判斷在要求於 Edge Server 上產生部分快取遺失時會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="5ba58-236">Determines what happens when a request results in a partial cache miss on an edge server.</span></span>
<span data-ttu-id="5ba58-237">壓縮檔案類型</span><span class="sxs-lookup"><span data-stu-id="5ba58-237">Compress File Types</span></span> | <span data-ttu-id="5ba58-238">Hello 伺服器上定義 hello 將壓縮的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-238">Defines hello file formats that will be compressed on hello server.</span></span>
<span data-ttu-id="5ba58-239">預設的內部最大壽命</span><span class="sxs-lookup"><span data-stu-id="5ba58-239">Default Internal Max-Age</span></span> | <span data-ttu-id="5ba58-240">決定 hello 預設保留時間上限的間隔 edge server tooorigin 伺服器快取重新驗證。</span><span class="sxs-lookup"><span data-stu-id="5ba58-240">Determines hello default max-age interval for edge server tooorigin server cache revalidation.</span></span>
<span data-ttu-id="5ba58-241">Expires 標頭處理</span><span class="sxs-lookup"><span data-stu-id="5ba58-241">Expires Header Treatment</span></span> | <span data-ttu-id="5ba58-242">控制項的邊緣伺服器 hello Expires 標頭產生 hello 外部 Max-age 功能正在作用中時。</span><span class="sxs-lookup"><span data-stu-id="5ba58-242">Controls hello generation of Expires headers by an edge server when hello External Max-Age feature is active.</span></span>
<span data-ttu-id="5ba58-243">外部最大壽命</span><span class="sxs-lookup"><span data-stu-id="5ba58-243">External Max-Age</span></span> | <span data-ttu-id="5ba58-244">決定瀏覽器 tooedge 伺服器快取重新驗證的 hello 最大時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-244">Determines hello max-age interval for browser tooedge server cache revalidation.</span></span>
<span data-ttu-id="5ba58-245">強制執行內部最大壽命</span><span class="sxs-lookup"><span data-stu-id="5ba58-245">Force Internal Max-Age</span></span> | <span data-ttu-id="5ba58-246">決定 edge server tooorigin 伺服器快取重新驗證的 hello 最大時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-246">Determines hello max-age interval for edge server tooorigin server cache revalidation.</span></span>
<span data-ttu-id="5ba58-247">H.264 支援 (HTTP 漸進式下載)</span><span class="sxs-lookup"><span data-stu-id="5ba58-247">H.264 Support (HTTP Progressive Download)</span></span> | <span data-ttu-id="5ba58-248">決定 hello H.264 種檔案格式，可能會使用的 toostream 內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-248">Determines hello types of H.264 file formats that may be used toostream content.</span></span>
<span data-ttu-id="5ba58-249">接受 No-Cache 要求</span><span class="sxs-lookup"><span data-stu-id="5ba58-249">Honor No-Cache Request</span></span> | <span data-ttu-id="5ba58-250">決定是否轉寄 HTTP 用戶端的無快取要求將會是 toohello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-250">Determines whether an HTTP client's no-cache requests will be forwarded toohello origin server.</span></span>
<span data-ttu-id="5ba58-251">忽略原始的 No-Cache</span><span class="sxs-lookup"><span data-stu-id="5ba58-251">Ignore Origin No-Cache</span></span> | <span data-ttu-id="5ba58-252">判斷我們的 CDN 是否將忽略原始伺服器所提供的特定指示詞。</span><span class="sxs-lookup"><span data-stu-id="5ba58-252">Determines whether our CDN will ignore certain directives served from an origin server.</span></span>
<span data-ttu-id="5ba58-253">忽略無法滿足的範圍</span><span class="sxs-lookup"><span data-stu-id="5ba58-253">Ignore Unsatisfiable Ranges</span></span> | <span data-ttu-id="5ba58-254">決定時，會傳回 tooclients 要求會產生 416 的範圍無法滿足的要求狀態碼的 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-254">Determines hello response that will be returned tooclients when a request generates a 416 Requested Range Not Satisfiable status code.</span></span>
<span data-ttu-id="5ba58-255">內部最大過時</span><span class="sxs-lookup"><span data-stu-id="5ba58-255">Internal Max-Stale</span></span> | <span data-ttu-id="5ba58-256">控制多久的時間超過快取的資產可能會提供服務的 hello 正常的到期時間的邊緣伺服器 hello 邊緣伺服器時無法 toorevalidate hello hello 來源伺服器的快取的資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-256">Controls how long past hello normal expiration time a cached asset may be served from an edge server when hello edge server is unable toorevalidate hello cached asset with hello origin server.</span></span>
<span data-ttu-id="5ba58-257">部分快取共用</span><span class="sxs-lookup"><span data-stu-id="5ba58-257">Partial Cache Sharing</span></span> | <span data-ttu-id="5ba58-258">判斷要求是否可以產生部分快取的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-258">Determines whether a request can generate partially cached content.</span></span>
<span data-ttu-id="5ba58-259">預先驗證快取的內容</span><span class="sxs-lookup"><span data-stu-id="5ba58-259">Prevalidate Cached Content</span></span> | <span data-ttu-id="5ba58-260">在快取內容的 TTL 到期之前，判斷其是否適用進行早期重新驗證。</span><span class="sxs-lookup"><span data-stu-id="5ba58-260">Determines whether cached content will be eligible for early revalidation before its TTL expires.</span></span>
<span data-ttu-id="5ba58-261">重新整理零位元組的快取檔案</span><span class="sxs-lookup"><span data-stu-id="5ba58-261">Refresh Zero-Byte Cache Files</span></span> | <span data-ttu-id="5ba58-262">判斷如何透過我們的 Edge Server 來處理 HTTP 用戶端對於 0 位元組快取資產的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-262">Determines how an HTTP client's request for a 0-byte cache asset is handled by our edge servers.</span></span>
<span data-ttu-id="5ba58-263">設定可快取的狀態碼</span><span class="sxs-lookup"><span data-stu-id="5ba58-263">Set Cacheable Status Codes</span></span> | <span data-ttu-id="5ba58-264">定義 hello 組可能會導致快取內容的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-264">Defines hello set of status codes that can result in cached content.</span></span>
<span data-ttu-id="5ba58-265">發生錯誤時傳遞過時的內容</span><span class="sxs-lookup"><span data-stu-id="5ba58-265">Stale Content Delivery on Error</span></span> | <span data-ttu-id="5ba58-266">判斷是否已過期期間快取重新驗證，或擷取 hello hello 客戶原始伺服器要求內容時，發生錯誤時，將會傳遞快取的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-266">Determines whether expired cached content will be delivered when an error occurs during cache revalidation or when retrieving hello requested content from hello customer origin server.</span></span>
<span data-ttu-id="5ba58-267">在重新驗證時過期</span><span class="sxs-lookup"><span data-stu-id="5ba58-267">Stale While Revalidate</span></span> | <span data-ttu-id="5ba58-268">藉由使用我們的邊緣伺服器 tooserve 過時的用戶端 toohello 要求者重新驗證時，可以改善效能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-268">Improves performance by allowing our edge servers tooserve stale client toohello requester while revalidation takes place.</span></span>
<span data-ttu-id="5ba58-269">註解</span><span class="sxs-lookup"><span data-stu-id="5ba58-269">Comment</span></span> | <span data-ttu-id="5ba58-270">hello 註解功能可讓規則中新增附註 toobe。</span><span class="sxs-lookup"><span data-stu-id="5ba58-270">hello Comment feature allows a note toobe added within a rule.</span></span>

###<a name="bandwidth-parameters"></a><span data-ttu-id="5ba58-271">頻寬參數</span><span class="sxs-lookup"><span data-stu-id="5ba58-271">Bandwidth Parameters</span></span>
<span data-ttu-id="5ba58-272">**目的：**判斷是否將使用頻寬節流設定參數 (例如 ec_rate 和 ec_prebuf)。</span><span class="sxs-lookup"><span data-stu-id="5ba58-272">**Purpose:** Determines whether bandwidth throttling parameters (i.e., ec_rate and ec_prebuf) will be active.</span></span>

<span data-ttu-id="5ba58-273">頻寬節流參數判斷 hello 資料傳輸速率為用戶端的要求是否會限制的 tooa 自訂速率。</span><span class="sxs-lookup"><span data-stu-id="5ba58-273">Bandwidth throttling parameters determine whether hello data transfer rate for a client's request will be limited tooa custom rate.</span></span>

<span data-ttu-id="5ba58-274">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-274">Value</span></span>|<span data-ttu-id="5ba58-275">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-275">Result</span></span>
--|--
<span data-ttu-id="5ba58-276">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-276">Enabled</span></span>|<span data-ttu-id="5ba58-277">可讓我們的邊緣伺服器 toohonor 頻寬節流的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-277">Allows our edge servers toohonor bandwidth throttling requests.</span></span>
<span data-ttu-id="5ba58-278">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-278">Disabled</span></span>|<span data-ttu-id="5ba58-279">讓我們的邊緣伺服器 tooignore 頻寬節流參數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-279">Causes our edge servers tooignore bandwidth throttling parameters.</span></span> <span data-ttu-id="5ba58-280">hello 要求內容系統將會正常處理 （亦即，不含頻寬節流設定）。</span><span class="sxs-lookup"><span data-stu-id="5ba58-280">hello requested content will be served normally (i.e., without bandwidth throttling).</span></span>

<span data-ttu-id="5ba58-281">**預設行為：**已啟用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-281">**Default Behavior:** Enabled.</span></span>

###<a name="bandwidth-throttling"></a><span data-ttu-id="5ba58-282">頻寬節流設定</span><span class="sxs-lookup"><span data-stu-id="5ba58-282">Bandwidth Throttling</span></span>
<span data-ttu-id="5ba58-283">**用途：**流速 hello hello 回應我們的邊緣伺服器所提供的頻寬。</span><span class="sxs-lookup"><span data-stu-id="5ba58-283">**Purpose:** Throttles hello bandwidth for hello response provided by our edge servers.</span></span>

<span data-ttu-id="5ba58-284">這兩個下列選項的 hello 必須定義的 tooproperly 設定頻寬節流設定。</span><span class="sxs-lookup"><span data-stu-id="5ba58-284">Both of hello following options must be defined tooproperly set up bandwidth throttling.</span></span>

<span data-ttu-id="5ba58-285">選項</span><span class="sxs-lookup"><span data-stu-id="5ba58-285">Option</span></span>|<span data-ttu-id="5ba58-286">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-286">Description</span></span>
--|--
<span data-ttu-id="5ba58-287">每秒 KB 數</span><span class="sxs-lookup"><span data-stu-id="5ba58-287">Kbytes per second</span></span>|<span data-ttu-id="5ba58-288">設定此選項 toohello 最大頻寬 (每秒 Kb) 可能會使用的 toodeliver hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-288">Set this option toohello maximum bandwidth (Kb per second) that may be used toodeliver hello response.</span></span>
<span data-ttu-id="5ba58-289">Prebuf 秒</span><span class="sxs-lookup"><span data-stu-id="5ba58-289">Prebuf seconds</span></span>|<span data-ttu-id="5ba58-290">設定此選項 toohello 秒數，我們的邊緣伺服器會等到節流的頻寬。</span><span class="sxs-lookup"><span data-stu-id="5ba58-290">Set this option toohello number of seconds that our edge servers will wait until throttling bandwidth.</span></span> <span data-ttu-id="5ba58-291">這段期間，不受限制的 hello 用途是頻寬的 tooprevent 媒體播放 」 發生間斷或緩衝到期 toobandwidth 節流的問題。</span><span class="sxs-lookup"><span data-stu-id="5ba58-291">hello purpose of this time period of unrestricted bandwidth is tooprevent a media player from experiencing stuttering or buffering issues due toobandwidth throttling.</span></span>

<span data-ttu-id="5ba58-292">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-292">**Default Behavior:** Disabled.</span></span>

###<a name="bypass-cache"></a><span data-ttu-id="5ba58-293">略過快取</span><span class="sxs-lookup"><span data-stu-id="5ba58-293">Bypass Cache</span></span>
<span data-ttu-id="5ba58-294">**用途：**決定 hello 要求是否可以利用我們的快取技術。</span><span class="sxs-lookup"><span data-stu-id="5ba58-294">**Purpose:** Determines whether hello request can leverage our caching technology.</span></span>

<span data-ttu-id="5ba58-295">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-295">Value</span></span>|<span data-ttu-id="5ba58-296">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-296">Result</span></span>
--|--
<span data-ttu-id="5ba58-297">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-297">Enabled</span></span>|<span data-ttu-id="5ba58-298">即使 hello 內容先前快取，在 edge 伺服器上，會導致透過 toohello 原始伺服器的所有要求 toofall。</span><span class="sxs-lookup"><span data-stu-id="5ba58-298">Causes all requests toofall through toohello origin server, even if hello content was previously cached on edge servers.</span></span>
<span data-ttu-id="5ba58-299">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-299">Disabled</span></span>|<span data-ttu-id="5ba58-300">根據其回應標頭中定義的 toohello 快取原則 toocache 資產導致邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-300">Causes edge servers toocache assets according toohello cache policy defined in its response headers.</span></span>

<span data-ttu-id="5ba58-301">**預設行為：**</span><span class="sxs-lookup"><span data-stu-id="5ba58-301">**Default Behavior:**</span></span>

- <span data-ttu-id="5ba58-302">**HTTP 大型︰**已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-302">**HTTP Large:** Disabled</span></span>

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a><span data-ttu-id="5ba58-303">Cache-Control 標頭處理</span><span class="sxs-lookup"><span data-stu-id="5ba58-303">Cache Control Header Treatment</span></span>
<span data-ttu-id="5ba58-304">**用途：**外部 Max-age 功能正在作用中時，控制 hello 產生快取控制標頭的 hello 邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-304">**Purpose:** Controls hello generation of Cache-Control headers by hello edge server when External Max-Age Feature is active.</span></span>

<span data-ttu-id="5ba58-305">hello tooplace hello 外部 Max-age 和中的 hello 快取控制標頭處理功能，是這種設定的最簡單方式 tooachieve hello 相同的陳述式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-305">hello easiest way tooachieve this type of configuration is tooplace hello External Max-Age and hello Cache-Control Header Treatment features in hello same statement.</span></span>

<span data-ttu-id="5ba58-306">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-306">Value</span></span>|<span data-ttu-id="5ba58-307">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-307">Result</span></span>
--|--
<span data-ttu-id="5ba58-308">覆寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-308">Overwrite</span></span>|<span data-ttu-id="5ba58-309">可確保會進行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-309">Ensures that hello following actions will take place:</span></span><br/> <span data-ttu-id="5ba58-310">-會覆寫 hello 原始伺服器所產生的快取控制標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-310">- Overwrites the Cache-Control header generated by hello origin server.</span></span> <br/><span data-ttu-id="5ba58-311">-加入 hello 外部 Max-age 功能 toohello 回應所產生的快取控制標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-311">- Adds the Cache-Control header produced by hello External Max-Age feature toohello response.</span></span>
<span data-ttu-id="5ba58-312">傳遞</span><span class="sxs-lookup"><span data-stu-id="5ba58-312">Pass Through</span></span>|<span data-ttu-id="5ba58-313">可確保 hello 外部 Max-age 功能所產生的快取控制標頭會永遠不會加入 toohello 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-313">Ensures that the Cache-Control header produced by hello External Max-Age feature is never added toohello response.</span></span> <br/> <span data-ttu-id="5ba58-314">Hello 原始伺服器就會產生快取控制標頭，它會通過 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-314">If hello origin server produces a Cache-Control header, it will pass through toohello end-user.</span></span> <br/> <span data-ttu-id="5ba58-315">如果快取控制標頭，則此選項將不會產生 hello 原始伺服器原因 hello 回應標頭 toonot 可能包含快取控制標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-315">If hello origin server does not produce a Cache-Control header, then this option may cause hello response header toonot contain a Cache-Control header.</span></span>
<span data-ttu-id="5ba58-316">如果遺失則加入</span><span class="sxs-lookup"><span data-stu-id="5ba58-316">Add if Missing</span></span>|<span data-ttu-id="5ba58-317">如果快取控制標頭不來自 hello 原始伺服器，此選項會新增 hello 外部 Max-age 功能所產生的快取控制標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-317">If a Cache-Control header was not received from hello origin server, then this option adds the Cache-Control header produced by hello External Max-Age feature.</span></span> <span data-ttu-id="5ba58-318">若要確保會為所有資產指派 Cache-Control 標頭，此選項非常有用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-318">This option is useful for ensuring that all assets will be assigned a Cache-Control header.</span></span>
<span data-ttu-id="5ba58-319">移除</span><span class="sxs-lookup"><span data-stu-id="5ba58-319">Remove</span></span>| <span data-ttu-id="5ba58-320">此選項可確保快取控制標頭不含 hello 標頭的回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-320">This option ensures that a Cache-Control header is not included with hello header response.</span></span> <span data-ttu-id="5ba58-321">如果已指派給快取控制標頭，它將會移除從 hello 標頭回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-321">If a Cache-Control header has already been assigned, then it will be stripped from hello header response.</span></span>

<span data-ttu-id="5ba58-322">**預設行為：**覆寫。</span><span class="sxs-lookup"><span data-stu-id="5ba58-322">**Default Behavior:** Overwrite.</span></span>

###<a name="cache-key-query-string"></a><span data-ttu-id="5ba58-323">快取索引鍵查詢字串</span><span class="sxs-lookup"><span data-stu-id="5ba58-323">Cache-Key Query String</span></span>
<span data-ttu-id="5ba58-324">**目的：**判斷快取索引鍵是否將包含或排除與要求相關聯的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-324">**Purpose:** Determines whether the cache-key will include or exclude query string parameters associated with a request.</span></span>

<span data-ttu-id="5ba58-325">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-325">Key information:</span></span>

- <span data-ttu-id="5ba58-326">指定一或多個查詢字串參數名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-326">Specify one or more query string parameter name(s).</span></span> <span data-ttu-id="5ba58-327">每個參數名稱都應以單一空格分隔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-327">Each parameter name should be delimited with a single space.</span></span>
- <span data-ttu-id="5ba58-328">這項功能會決定是否將包含或排除 hello 快取索引鍵的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-328">This feature determines whether query string parameters will be included or excluded from hello cache-key.</span></span> <span data-ttu-id="5ba58-329">以下提供每個選項的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="5ba58-329">Additional information is provided for each option below.</span></span>

<span data-ttu-id="5ba58-330">類型</span><span class="sxs-lookup"><span data-stu-id="5ba58-330">Type</span></span>|<span data-ttu-id="5ba58-331">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-331">Description</span></span>
--|--
 <span data-ttu-id="5ba58-332">包含</span><span class="sxs-lookup"><span data-stu-id="5ba58-332">Include</span></span>|  <span data-ttu-id="5ba58-333">指出指定的每個參數應該併入 hello 快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5ba58-333">Indicates that each specified parameter should be included in hello cache-key.</span></span> <span data-ttu-id="5ba58-334">系統將針對每個要求產生唯一的快取索引鍵，其中包含此功能中所定義之查詢字串參數的唯一值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-334">A unique cache-key will be generated for each request that contains a unique value for a query string parameter defined in this feature.</span></span> 
 <span data-ttu-id="5ba58-335">全部包含</span><span class="sxs-lookup"><span data-stu-id="5ba58-335">Include All</span></span>  |<span data-ttu-id="5ba58-336">表示，將會建立包含唯一的查詢字串每個要求 tooan 資產的唯一快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5ba58-336">Indicates that a unique cache-key will be created for each request tooan asset that includes a unique query string.</span></span> <span data-ttu-id="5ba58-337">不通常建議這種設定，因為它可能會導致快取點擊 tooa 小比例。</span><span class="sxs-lookup"><span data-stu-id="5ba58-337">This type of configuration is not typically recommended since it may lead tooa small percentage of cache hits.</span></span> <span data-ttu-id="5ba58-338">這會增加 hello 負載 hello 原始伺服器，因為它會包含 tooserve 更多的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-338">This will increase hello load on hello origin server, since it will have tooserve more requests.</span></span> <span data-ttu-id="5ba58-339">此設定會複製 hello 快取行為稱為 「 唯一快取"查詢字串快取 頁面上。</span><span class="sxs-lookup"><span data-stu-id="5ba58-339">This configuration duplicates hello caching behavior known as "unique-cache" on the Query-String Caching page.</span></span> 
 <span data-ttu-id="5ba58-340">排除</span><span class="sxs-lookup"><span data-stu-id="5ba58-340">Exclude</span></span> | <span data-ttu-id="5ba58-341">表示該只有 hello 可讓您指定參數將會排除 hello 快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5ba58-341">Indicates that only hello specified parameter(s) will be excluded from hello cache-key.</span></span> <span data-ttu-id="5ba58-342">所有其他的查詢字串參數將會包含在 hello 快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5ba58-342">All other query string parameters will be included in hello cache-key.</span></span> 
 <span data-ttu-id="5ba58-343">全部排除</span><span class="sxs-lookup"><span data-stu-id="5ba58-343">Exclude All</span></span>  |<span data-ttu-id="5ba58-344">表示所有查詢字串參數將會都排除 hello 快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5ba58-344">Indicates that all query string parameters will be excluded from hello cache-key.</span></span> <span data-ttu-id="5ba58-345">此設定會複製 hello 預設快取行為，也稱為 「 標準快取 」 用在查詢字串快取 頁面上。</span><span class="sxs-lookup"><span data-stu-id="5ba58-345">This configuration duplicates hello default caching behavior, which is known as "standard-cache" on the Query-String Caching page.</span></span> 

<span data-ttu-id="5ba58-346">hello 冪 HTTP 規則引擎可讓您在此實作查詢字串快取 toocustomize hello 方式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-346">hello power of HTTP Rules Engine allows you toocustomize hello manner in which query string caching is implemented.</span></span> <span data-ttu-id="5ba58-347">例如，您可以指定查詢字串快取只會在特定位置或檔案類型上執行。</span><span class="sxs-lookup"><span data-stu-id="5ba58-347">For example, you can specify that query string caching only be performed on certain locations or file types.</span></span>

<span data-ttu-id="5ba58-348">如果您想要 tooduplicate hello 查詢字串快取行為稱為 「 無快取"查詢字串快取 頁面上，您將需要 toocreate 包含 URL 查詢萬用字元比對條件和略過快取功能的規則。</span><span class="sxs-lookup"><span data-stu-id="5ba58-348">If you would like tooduplicate hello query string caching behavior known as "no-cache" on the Query-String Caching page, then you will need toocreate a rule that contains a URL Query Wildcard match condition and a Bypass Cache feature.</span></span> <span data-ttu-id="5ba58-349">hello URL 查詢萬用字元比對條件應該設定 tooan 星號 （*）。</span><span class="sxs-lookup"><span data-stu-id="5ba58-349">hello URL Query Wildcard match condition should be set tooan asterisk (*).</span></span>

#### <a name="sample-scenarios"></a><span data-ttu-id="5ba58-350">範例案例</span><span class="sxs-lookup"><span data-stu-id="5ba58-350">Sample Scenarios</span></span>

<span data-ttu-id="5ba58-351">此功能的範例使用方式如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ba58-351">Sample usage for this feature is provided below.</span></span> <span data-ttu-id="5ba58-352">範例要求和 hello 預設快取索引鍵如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ba58-352">A sample request and hello default cache-key are provided below.</span></span>

- <span data-ttu-id="5ba58-353">**範例要求︰**http://wpc.0001.&lt;網域&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01</span><span class="sxs-lookup"><span data-stu-id="5ba58-353">**Sample request:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01</span></span>
- <span data-ttu-id="5ba58-354">**預設的快取索引鍵︰**/800001/Origin/folder/asset.htm</span><span class="sxs-lookup"><span data-stu-id="5ba58-354">**Default cache-key:** /800001/Origin/folder/asset.htm</span></span>

##### <a name="include"></a><span data-ttu-id="5ba58-355">包含</span><span class="sxs-lookup"><span data-stu-id="5ba58-355">Include</span></span>

<span data-ttu-id="5ba58-356">範例組態：</span><span class="sxs-lookup"><span data-stu-id="5ba58-356">Sample configuration:</span></span>

- <span data-ttu-id="5ba58-357">**類型︰**包括</span><span class="sxs-lookup"><span data-stu-id="5ba58-357">**Type:** Include</span></span>
- <span data-ttu-id="5ba58-358">**參數︰**語言</span><span class="sxs-lookup"><span data-stu-id="5ba58-358">**Parameter(s):** language</span></span>

<span data-ttu-id="5ba58-359">這種設定會產生下列查詢字串參數快取索引鍵的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-359">This type of configuration would generate hello following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a><span data-ttu-id="5ba58-360">全部包含</span><span class="sxs-lookup"><span data-stu-id="5ba58-360">Include All</span></span>

<span data-ttu-id="5ba58-361">範例組態：</span><span class="sxs-lookup"><span data-stu-id="5ba58-361">Sample configuration:</span></span>

- <span data-ttu-id="5ba58-362">**類型︰**全部包括</span><span class="sxs-lookup"><span data-stu-id="5ba58-362">**Type:** Include All</span></span>

<span data-ttu-id="5ba58-363">這種設定會產生下列查詢字串參數快取索引鍵的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-363">This type of configuration would generate hello following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a><span data-ttu-id="5ba58-364">排除</span><span class="sxs-lookup"><span data-stu-id="5ba58-364">Exclude</span></span>

<span data-ttu-id="5ba58-365">範例組態：</span><span class="sxs-lookup"><span data-stu-id="5ba58-365">Sample configuration:</span></span>

- <span data-ttu-id="5ba58-366">**類型︰**排除</span><span class="sxs-lookup"><span data-stu-id="5ba58-366">**Type:** Exclude</span></span>
- <span data-ttu-id="5ba58-367">**參數︰**工作階段識別碼的使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="5ba58-367">**Parameter(s):** sessionid userid</span></span>

<span data-ttu-id="5ba58-368">這種設定會產生下列查詢字串參數快取索引鍵的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-368">This type of configuration would generate hello following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a><span data-ttu-id="5ba58-369">全部排除</span><span class="sxs-lookup"><span data-stu-id="5ba58-369">Exclude All</span></span>

<span data-ttu-id="5ba58-370">範例組態：</span><span class="sxs-lookup"><span data-stu-id="5ba58-370">Sample configuration:</span></span>

- <span data-ttu-id="5ba58-371">**類型︰**全部排除</span><span class="sxs-lookup"><span data-stu-id="5ba58-371">**Type:** Exclude All</span></span>

<span data-ttu-id="5ba58-372">這種設定會產生下列查詢字串參數快取索引鍵的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-372">This type of configuration would generate hello following query string parameter cache-key:</span></span>

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a><span data-ttu-id="5ba58-373">快取索引鍵重寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-373">Cache-Key Rewrite</span></span>
<span data-ttu-id="5ba58-374">**用途：**撰寫 hello 快取索引鍵與要求相關聯。</span><span class="sxs-lookup"><span data-stu-id="5ba58-374">**Purpose:** Rewrites hello cache-key associated with a request.</span></span>

<span data-ttu-id="5ba58-375">快取索引鍵是識別快取的 hello 基於資產的 hello 相對路徑。</span><span class="sxs-lookup"><span data-stu-id="5ba58-375">A cache-key is hello relative path that identifies an asset for hello purposes of caching.</span></span> <span data-ttu-id="5ba58-376">換句話說，我們的伺服器會檢查根據 tooits 路徑其快取索引鍵所定義的資產的快取版本。</span><span class="sxs-lookup"><span data-stu-id="5ba58-376">In other words, our servers will check for a cached version of an asset according tooits path as defined by its cache-key.</span></span>

<span data-ttu-id="5ba58-377">設定這項功能，藉由定義兩個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="5ba58-377">Configure this feature by defining both of hello following options:</span></span>

<span data-ttu-id="5ba58-378">選項</span><span class="sxs-lookup"><span data-stu-id="5ba58-378">Option</span></span>|<span data-ttu-id="5ba58-379">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-379">Description</span></span>
--|--
<span data-ttu-id="5ba58-380">原始路徑</span><span class="sxs-lookup"><span data-stu-id="5ba58-380">Original Path</span></span>| <span data-ttu-id="5ba58-381">定義 hello 相對路徑 toohello 類型的要求將會重新寫入其快取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5ba58-381">Define hello relative path toohello types of requests whose cache-key will be rewritten.</span></span> <span data-ttu-id="5ba58-382">相對路徑可藉由選取基底原始路徑，然後定義規則運算式模式來定義。</span><span class="sxs-lookup"><span data-stu-id="5ba58-382">A relative path can be defined by selecting a base origin path and then defining a regular expression pattern.</span></span>
<span data-ttu-id="5ba58-383">新路徑</span><span class="sxs-lookup"><span data-stu-id="5ba58-383">New Path</span></span>|<span data-ttu-id="5ba58-384">定義 hello hello 新快取金鑰的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="5ba58-384">Define hello relative path for hello new cache-key.</span></span> <span data-ttu-id="5ba58-385">相對路徑可藉由選取基底原始路徑，然後定義規則運算式模式來定義。</span><span class="sxs-lookup"><span data-stu-id="5ba58-385">A relative path can be defined by selecting a base origin path and then defining a regular expression pattern.</span></span> <span data-ttu-id="5ba58-386">此相對路徑可以透過 HTTP 變數 hello 使用動態建構</span><span class="sxs-lookup"><span data-stu-id="5ba58-386">This relative path can be dynamically constructed through hello use of HTTP variables</span></span>
<span data-ttu-id="5ba58-387">**預設行為：**要求的快取索引鍵由 hello 要求 URI。</span><span class="sxs-lookup"><span data-stu-id="5ba58-387">**Default Behavior:** A request's cache-key is determined by hello request URI.</span></span>

###<a name="complete-cache-fill"></a><span data-ttu-id="5ba58-388">完成快取填滿</span><span class="sxs-lookup"><span data-stu-id="5ba58-388">Complete Cache Fill</span></span>
<span data-ttu-id="5ba58-389">**目的：**判斷在要求於 Edge Server 上產生部分快取遺失時會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="5ba58-389">**Purpose:** Determines what happens when a request results in a partial cache miss on an edge server.</span></span>

<span data-ttu-id="5ba58-390">部分快取遺漏說明 hello 未完全下載的 tooan 邊緣伺服器資產的快取狀態。</span><span class="sxs-lookup"><span data-stu-id="5ba58-390">A partial cache miss describes hello cache status for an asset that was not completely downloaded tooan edge server.</span></span> <span data-ttu-id="5ba58-391">如果 edge server 僅部分快取資產，然後 hello 資產的下一個要求將會轉送一次 toohello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-391">If an asset is only partially cached on an edge server, then hello next request for that asset will be forwarded again toohello origin server.</span></span>
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
<span data-ttu-id="5ba58-392">部分快取遺失通常發生於使用者中止下載之後，或發生於只要求使用 HTTP 範圍要求的資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-392">A partial cache miss typically occurs after a user aborts a download or for assets that are solely requested using HTTP range requests.</span></span> <span data-ttu-id="5ba58-393">這項功能是最適合用於大型的資產，使用者將不通常它們從下載開始 toofinish （例如，視訊）。</span><span class="sxs-lookup"><span data-stu-id="5ba58-393">This feature is most useful for large assets where users will not typically download them from start toofinish (e.g., videos).</span></span> <span data-ttu-id="5ba58-394">如此一來，hello HTTP 大型平台上預設會啟用這項功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-394">As a result, this feature is enabled by default on hello HTTP Large platform.</span></span> <span data-ttu-id="5ba58-395">所有其他平台上則會加以停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-395">It is disabled on all other platforms.</span></span>

<span data-ttu-id="5ba58-396">建議 tooleave hello 預設組態對於 hello HTTP 大型平台，因為它會減少您客戶的原始伺服器上的 hello 負載，而且增加 hello 速度的客戶會下載您的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-396">It is recommended tooleave hello default configuration for hello HTTP Large platform, since it will reduce hello load on your customer origin server and increase hello speed at which your customers download your content.</span></span>

<span data-ttu-id="5ba58-397">Toohello 追蹤哪一個快取設定的方式，因為這項功能不能關聯以下列比對條件 hello： 邊緣 Cname、 常值要求標頭、 要求標頭萬用字元、 URL 查詢常值，和 URL 查詢萬用字元。</span><span class="sxs-lookup"><span data-stu-id="5ba58-397">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following Match conditions: Edge Cname, Request Header Literal, Request Header Wildcard, URL Query Literal, and URL Query Wildcard.</span></span>

<span data-ttu-id="5ba58-398">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-398">Value</span></span>|<span data-ttu-id="5ba58-399">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-399">Result</span></span>
--|--
<span data-ttu-id="5ba58-400">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-400">Enabled</span></span>|<span data-ttu-id="5ba58-401">還原 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-401">Restores hello default behavior.</span></span> <span data-ttu-id="5ba58-402">hello 預設行為是 tooforce hello edge server tooinitiate hello 資產的背景擷取從 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-402">hello default behavior is tooforce hello edge server tooinitiate a background fetch of hello asset from hello origin server.</span></span> <span data-ttu-id="5ba58-403">在那之後，hello 資產將會在 hello 邊緣伺服器的本機快取。</span><span class="sxs-lookup"><span data-stu-id="5ba58-403">After which, hello asset will be in hello edge server's local cache.</span></span>
<span data-ttu-id="5ba58-404">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-404">Disabled</span></span>|<span data-ttu-id="5ba58-405">防止邊緣伺服器 hello 資產執行背景擷取。</span><span class="sxs-lookup"><span data-stu-id="5ba58-405">Prevents an edge server from performing a background fetch for hello asset.</span></span> <span data-ttu-id="5ba58-406">這表示該 hello 下次要求該地區該資產便會將 edge server toorequest 從 hello 客戶原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-406">This means that hello next request for that asset from that region will cause an edge server toorequest it from hello customer origin server.</span></span>

<span data-ttu-id="5ba58-407">**預設行為：**已啟用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-407">**Default Behavior:** Enabled.</span></span>

###<a name="compress-file-types"></a><span data-ttu-id="5ba58-408">壓縮檔案類型</span><span class="sxs-lookup"><span data-stu-id="5ba58-408">Compress File Types</span></span>
<span data-ttu-id="5ba58-409">**用途：** hello 伺服器上定義 hello 將壓縮的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-409">**Purpose:** Defines hello file formats that will be compressed on hello server.</span></span>

<span data-ttu-id="5ba58-410">您可以使用檔案格式的網際網路媒體類型 (亦即，內容類型) 來指定檔案格式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-410">A file format can be specified using its Internet media type (i.e., Content-Type).</span></span> <span data-ttu-id="5ba58-411">網際網路媒體類型為平台無關的中繼資料，可讓特定資產我們伺服器 tooidentify hello 檔案格式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-411">Internet media type is platform-independent metadata that allows our servers tooidentify hello file format of a particular asset.</span></span> <span data-ttu-id="5ba58-412">以下提供常用的網際網路媒體類型清單。</span><span class="sxs-lookup"><span data-stu-id="5ba58-412">A list of common Internet media types is provided below.</span></span>

<span data-ttu-id="5ba58-413">網際網路媒體類型</span><span class="sxs-lookup"><span data-stu-id="5ba58-413">Internet Media Type</span></span>|<span data-ttu-id="5ba58-414">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-414">Description</span></span>
--|--
<span data-ttu-id="5ba58-415">text/plain</span><span class="sxs-lookup"><span data-stu-id="5ba58-415">text/plain</span></span>|<span data-ttu-id="5ba58-416">純文字檔案</span><span class="sxs-lookup"><span data-stu-id="5ba58-416">Plain text files</span></span>
<span data-ttu-id="5ba58-417">text/html</span><span class="sxs-lookup"><span data-stu-id="5ba58-417">text/html</span></span>| <span data-ttu-id="5ba58-418">HTML 檔案</span><span class="sxs-lookup"><span data-stu-id="5ba58-418">HTML files</span></span>
<span data-ttu-id="5ba58-419">text/css</span><span class="sxs-lookup"><span data-stu-id="5ba58-419">text/css</span></span>|<span data-ttu-id="5ba58-420">階層式樣式表 (CSS)</span><span class="sxs-lookup"><span data-stu-id="5ba58-420">Cascading Style Sheets (CSS)</span></span>
<span data-ttu-id="5ba58-421">application/x-javascript</span><span class="sxs-lookup"><span data-stu-id="5ba58-421">application/x-javascript</span></span>|<span data-ttu-id="5ba58-422">Javascript</span><span class="sxs-lookup"><span data-stu-id="5ba58-422">Javascript</span></span>
<span data-ttu-id="5ba58-423">application/javascript</span><span class="sxs-lookup"><span data-stu-id="5ba58-423">application/javascript</span></span>|<span data-ttu-id="5ba58-424">Javascript</span><span class="sxs-lookup"><span data-stu-id="5ba58-424">Javascript</span></span>
<span data-ttu-id="5ba58-425">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-425">Key information:</span></span>

- <span data-ttu-id="5ba58-426">使用單一空格來分隔每個網際網路媒體類型，藉以指定多個類型。</span><span class="sxs-lookup"><span data-stu-id="5ba58-426">Specify multiple Internet media types by delimiting each one with a single space.</span></span> 
- <span data-ttu-id="5ba58-427">此功能將只會壓縮大小小於 1 MB 的資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-427">This feature will only compress assets whose size is less than 1 MB.</span></span> <span data-ttu-id="5ba58-428">我們的伺服器將不會壓縮較大型的資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-428">Larger assets will not be compressed by our servers.</span></span>
- <span data-ttu-id="5ba58-429">諸如影像、視訊和音訊媒體資產 (例如 JPG、MP3、MP4 等) 之類的特定類型內容均已壓縮。</span><span class="sxs-lookup"><span data-stu-id="5ba58-429">Certain types of content, such as images, video, and audio media assets (e.g., JPG, MP3, MP4, etc.), are already compressed.</span></span> <span data-ttu-id="5ba58-430">這些類型資產上的額外壓縮將不會顯著降低檔案大小。</span><span class="sxs-lookup"><span data-stu-id="5ba58-430">Additional compression on these types of assets will not significantly diminish file size.</span></span> <span data-ttu-id="5ba58-431">因此，建議您不要在這些類型的資產上啟用壓縮。</span><span class="sxs-lookup"><span data-stu-id="5ba58-431">Therefore, it is recommended that you do not enable compression on these types of assets.</span></span>
- <span data-ttu-id="5ba58-432">不支援萬用字元 (例如星號)。</span><span class="sxs-lookup"><span data-stu-id="5ba58-432">Wildcard characters, such as asterisks, are not supported.</span></span>
- <span data-ttu-id="5ba58-433">再新增此功能 tooa 規則，請確定 tooset 壓縮頁面上的此規則將套用的 hello 平台 toowhich 壓縮已停用的選項。</span><span class="sxs-lookup"><span data-stu-id="5ba58-433">Before adding this feature tooa rule, make sure tooset the Compression Disabled option on the Compression page for hello platform toowhich this rule will be applied.</span></span>

###<a name="default-internal-max-age"></a><span data-ttu-id="5ba58-434">預設的內部最大壽命</span><span class="sxs-lookup"><span data-stu-id="5ba58-434">Default Internal Max-Age</span></span>
<span data-ttu-id="5ba58-435">**用途：**判斷 hello 預設保留時間上限的間隔 edge server tooorigin 伺服器快取重新驗證。</span><span class="sxs-lookup"><span data-stu-id="5ba58-435">**Purpose:** Determines hello default max-age interval for edge server tooorigin server cache revalidation.</span></span> <span data-ttu-id="5ba58-436">換句話說，hello 邊緣伺服器之前，所經歷的時間量會檢查快取的資產是否符合儲存在 hello 原始伺服器上的 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-436">In other words, hello amount of time that will pass before an edge server will check whether a cached asset matches hello asset stored on hello origin server.</span></span>

<span data-ttu-id="5ba58-437">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-437">Key information:</span></span>

- <span data-ttu-id="5ba58-438">只有原始伺服器未在 Cache-Control 或 Expires 標頭中指派最大壽命指示時，此動作才會針對來自該原始伺服器的回應加以執行。</span><span class="sxs-lookup"><span data-stu-id="5ba58-438">This action will only take place for responses from an origin server that did not assign a max-age indication in the Cache-Control or Expires header.</span></span>
- <span data-ttu-id="5ba58-439">此動作將不會針對未被視為可快取的資產加以執行。</span><span class="sxs-lookup"><span data-stu-id="5ba58-439">This action will not take place for assets that are not deemed cacheable.</span></span>
- <span data-ttu-id="5ba58-440">此動作不會影響瀏覽器 tooedge 伺服器快取 revalidations。</span><span class="sxs-lookup"><span data-stu-id="5ba58-440">This action does not affect browser tooedge server cache revalidations.</span></span> <span data-ttu-id="5ba58-441">這種 revalidations 取決於快取控制或 Expires 標頭傳送 toohello 瀏覽器，可以使用外部 Max-age 功能自訂。</span><span class="sxs-lookup"><span data-stu-id="5ba58-441">These types of revalidations are determined by the Cache-Control or Expires headers sent toohello browser, which can be customized with the External Max-Age feature.</span></span>
- <span data-ttu-id="5ba58-442">hello 此動作結果並沒有顯著的影響 hello 回應標頭和邊緣伺服器適用於您的內容，從傳回的 hello 內容，但是它可能有傳送的邊緣伺服器 tooyour 原始伺服器的重新驗證流量的 hello 量影響。</span><span class="sxs-lookup"><span data-stu-id="5ba58-442">hello results of this action do not have an observable effect on hello response headers and hello content returned from edge servers for your content, but it may have an effect on hello amount of revalidation traffic sent from edge servers tooyour origin server.</span></span>
- <span data-ttu-id="5ba58-443">以下列方式設定此功能：</span><span class="sxs-lookup"><span data-stu-id="5ba58-443">Configure this feature by:</span></span>
    - <span data-ttu-id="5ba58-444">選取用於預設內部的保留時間上限的 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-444">Selecting hello status code for which a default internal max-age can be applied.</span></span>
    - <span data-ttu-id="5ba58-445">指定的整數值，然後選取 hello 所需的時間單位 （也就是，秒、 分鐘、 小時等等）。</span><span class="sxs-lookup"><span data-stu-id="5ba58-445">Specifying an integer value and then selecting hello desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="5ba58-446">此值會定義 hello 預設內部的最大時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-446">This value defines hello default internal max-age interval.</span></span>

- <span data-ttu-id="5ba58-447">設定 hello 時間單位太 「 關閉 」 將會指派預設內部保留時間上限的間隔要求沒有被指派其 Cache-control 或 Expires 標頭中的保留時間上限指示為 7 天。</span><span class="sxs-lookup"><span data-stu-id="5ba58-447">Setting hello time unit too"Off" will assign a default internal max-age interval of 7 days for requests that have not been assigned a max-age indication in their Cache-Control or Expires header.</span></span>
- <span data-ttu-id="5ba58-448">Toohello 追蹤哪一個快取設定的方式，因為這項功能無法關聯以 hello 下列比對條件：</span><span class="sxs-lookup"><span data-stu-id="5ba58-448">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following match conditions:</span></span> 
    - <span data-ttu-id="5ba58-449">Edge</span><span class="sxs-lookup"><span data-stu-id="5ba58-449">Edge</span></span> 
    - <span data-ttu-id="5ba58-450">Cname</span><span class="sxs-lookup"><span data-stu-id="5ba58-450">Cname</span></span>
    - <span data-ttu-id="5ba58-451">要求標頭常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-451">Request Header Literal</span></span>
    - <span data-ttu-id="5ba58-452">要求標頭萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-452">Request Header Wildcard</span></span>
    - <span data-ttu-id="5ba58-453">要求方法</span><span class="sxs-lookup"><span data-stu-id="5ba58-453">Request Method</span></span>
    - <span data-ttu-id="5ba58-454">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-454">URL Query Literal</span></span>
    - <span data-ttu-id="5ba58-455">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-455">URL Query Wildcard</span></span>

<span data-ttu-id="5ba58-456">**預設值：**7 天</span><span class="sxs-lookup"><span data-stu-id="5ba58-456">**Default Value:** 7 days</span></span>

###<a name="expires-header-treatment"></a><span data-ttu-id="5ba58-457">Expires 標頭處理</span><span class="sxs-lookup"><span data-stu-id="5ba58-457">Expires Header Treatment</span></span>
<span data-ttu-id="5ba58-458">**用途：**外部 Max-age 功能正在作用中時，控制 hello 產生 Expires 標頭的邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-458">**Purpose:** Controls hello generation of Expires headers by an edge server when the External Max-Age feature is active.</span></span>

<span data-ttu-id="5ba58-459">hello tooplace hello 外部 Max-age 和中的 hello 到期標頭處理功能，這種設定是最簡單的方式 tooachieve hello 相同的陳述式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-459">hello easiest way tooachieve this type of configuration is tooplace hello External Max-Age and hello Expires Header Treatment features in hello same statement.</span></span>

<span data-ttu-id="5ba58-460">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-460">Value</span></span>|<span data-ttu-id="5ba58-461">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-461">Result</span></span>
--|--
<span data-ttu-id="5ba58-462">覆寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-462">Overwrite</span></span>|<span data-ttu-id="5ba58-463">可確保會進行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-463">Ensures that hello following actions will take place:</span></span><br/><span data-ttu-id="5ba58-464">-會覆寫 hello 原始伺服器所產生的 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-464">- Overwrites the Expires header generated by hello origin server.</span></span><br/><span data-ttu-id="5ba58-465">-加入 hello 外部 Max-age 功能 toohello 回應所產生的 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-465">- Adds the Expires header produced by hello External Max-Age feature toohello response.</span></span>
<span data-ttu-id="5ba58-466">傳遞</span><span class="sxs-lookup"><span data-stu-id="5ba58-466">Pass Through</span></span>|<span data-ttu-id="5ba58-467">可確保 Expires 標頭所產生的 hello 外部 Max-age 功能永遠不會新增 toohello 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-467">Ensures that the Expires header produced by hello External Max-Age feature is never added toohello response.</span></span> <br/> <span data-ttu-id="5ba58-468">Hello 原始伺服器就會產生 Expires 標頭，它會通過 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-468">If hello origin server produces an Expires header, it will pass through toohello end-user.</span></span> <br/><span data-ttu-id="5ba58-469">如果 hello 原始伺服器不會產生 Expires 標頭，則此選項可能的原因 hello 回應標頭 toonot 可能包含 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-469">If hello origin server does not produce an Expires header, then this option may cause hello response header toonot contain an Expires header.</span></span>
<span data-ttu-id="5ba58-470">如果遺失則加入</span><span class="sxs-lookup"><span data-stu-id="5ba58-470">Add if Missing</span></span>| <span data-ttu-id="5ba58-471">如果 Expires 標頭不來自 hello 原始伺服器，此選項會新增 hello 外部 Max-age 功能所產生的 Expires 標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-471">If an Expires header was not received from hello origin server, then this option adds the Expires header produced by hello External Max-Age feature.</span></span> <span data-ttu-id="5ba58-472">若要確保會為所有資產指派 Expires 標頭，此選項非常有用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-472">This option is useful for ensuring that all assets will be assigned an Expires header.</span></span>
<span data-ttu-id="5ba58-473">移除</span><span class="sxs-lookup"><span data-stu-id="5ba58-473">Remove</span></span>| <span data-ttu-id="5ba58-474">可確保 Expires 標頭不含 hello 標頭的回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-474">Ensures that an Expires header is not included with hello header response.</span></span> <span data-ttu-id="5ba58-475">如果已指派給 Expires 標頭，它將會移除從 hello 標頭回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-475">If an Expires header has already been assigned, then it will be stripped from hello header response.</span></span>

<span data-ttu-id="5ba58-476">**預設行為：**覆寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-476">**Default Behavior:** Overwrite</span></span>

###<a name="external-max-age"></a><span data-ttu-id="5ba58-477">外部最大壽命</span><span class="sxs-lookup"><span data-stu-id="5ba58-477">External Max-Age</span></span>
<span data-ttu-id="5ba58-478">**用途：**瀏覽器 tooedge 伺服器快取重新驗證判斷 hello 最大時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-478">**Purpose:** Determines hello max-age interval for browser tooedge server cache revalidation.</span></span> <span data-ttu-id="5ba58-479">換句話說，新版本的邊緣伺服器從資產可以檢查 hello 瀏覽器之前，所經歷的時間量。</span><span class="sxs-lookup"><span data-stu-id="5ba58-479">In other words, hello amount of time that will pass before a browser can check for a new version of an asset from an edge server.</span></span>

<span data-ttu-id="5ba58-480">啟用這項功能將會產生快取的控制項： 最大的保留期限和到期標頭從我們的邊緣伺服器並將它們傳送 toohello HTTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5ba58-480">Enabling this feature will generate Cache-Control:max-age and Expires headers from our edge servers and send them toohello HTTP client.</span></span> <span data-ttu-id="5ba58-481">根據預設，這些標頭會覆寫所建立的 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-481">By default, these headers will overwrite those created by hello origin server.</span></span> <span data-ttu-id="5ba58-482">不過，快取控制標頭的處理方式，而到期標頭處理功能可能會使用的 tooalter 這種行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-482">However, the Cache-Control Header Treatment and the Expires Header Treatment features may be used tooalter this behavior.</span></span>

<span data-ttu-id="5ba58-483">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-483">Key information:</span></span>

- <span data-ttu-id="5ba58-484">此動作不會影響 edge server tooorigin 伺服器快取 revalidations。</span><span class="sxs-lookup"><span data-stu-id="5ba58-484">This action does not affect edge server tooorigin server cache revalidations.</span></span> <span data-ttu-id="5ba58-485">這種 revalidations 會取決於收到 hello 原始伺服器，從快取-控制項/Expires 標頭，而且可以自訂預設內部 Max-age 與 Force 內部 Max-age 功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-485">These types of revalidations are determined by the Cache-Control/Expires headers received from hello origin server, and can be customized with the Default Internal Max-Age and the Force Internal Max-Age features.</span></span>
- <span data-ttu-id="5ba58-486">設定指定整數值，然後選取 hello 所需的時間單位 （也就是，秒、 分鐘、 小時等） 的這項功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-486">Configure this feature by specifying an integer value and selecting hello desired time unit (i.e., seconds, minutes, hours, etc.).</span></span>
- <span data-ttu-id="5ba58-487">設定此功能 tooa 負值會導致我們的邊緣伺服器 toosend 快取的控制項： 沒有-快取和設定在 hello 截止時間過去的每個回應 toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-487">Setting this feature tooa negative value causes our edge servers toosend a Cache-Control:no-cache and an Expires time that is set in hello past with each response toohello browser.</span></span> <span data-ttu-id="5ba58-488">HTTP 用戶端並不會快取 hello 回應，雖然這項設定不會影響我們的邊緣伺服器的能力 toocache hello 回應 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-488">Although an HTTP client will not cache hello response, this setting will not affect our edge servers' ability toocache hello response from hello origin server.</span></span>
- <span data-ttu-id="5ba58-489">設定 hello 時間單位太 「 關閉 」 將會停用這項功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-489">Setting hello time unit too"Off" will disable this feature.</span></span> <span data-ttu-id="5ba58-490">使用 hello 回應 hello 原始伺服器的快取的快取-控制項/Expires 標頭會傳遞 toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-490">The Cache-Control/Expires headers cached with hello response of hello origin server will pass through toohello browser.</span></span>

<span data-ttu-id="5ba58-491">**預設行為：**關閉</span><span class="sxs-lookup"><span data-stu-id="5ba58-491">**Default Behavior:** Off</span></span>

###<a name="force-internal-max-age"></a><span data-ttu-id="5ba58-492">強制執行內部最大壽命</span><span class="sxs-lookup"><span data-stu-id="5ba58-492">Force Internal Max-Age</span></span>
<span data-ttu-id="5ba58-493">**用途：** edge server tooorigin 伺服器快取重新驗證判斷 hello 最大時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-493">**Purpose:** Determines hello max-age interval for edge server tooorigin server cache revalidation.</span></span> <span data-ttu-id="5ba58-494">換句話說，hello 邊緣伺服器之前，所經歷的時間量可以檢查快取的資產是否符合儲存在 hello 原始伺服器上的 hello 資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-494">In other words, hello amount of time that will pass before an edge server can check whether a cached asset matches hello asset stored on hello origin server.</span></span>

<span data-ttu-id="5ba58-495">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-495">Key information:</span></span>

- <span data-ttu-id="5ba58-496">這項功能將會覆寫 Cache-control 或 Expires 標頭產生從來源伺服器中定義的 hello 最大時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-496">This feature will override hello max-age interval defined in Cache-Control or Expires headers generated from an origin server.</span></span>
- <span data-ttu-id="5ba58-497">這項功能不會影響瀏覽器 tooedge 伺服器快取 revalidations。</span><span class="sxs-lookup"><span data-stu-id="5ba58-497">This feature does not affect browser tooedge server cache revalidations.</span></span> <span data-ttu-id="5ba58-498">Revalidations 這些類型由 Cache-control 或 Expires 標頭傳送 toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-498">These types of revalidations are determined by the Cache-Control or Expires headers sent toohello browser.</span></span>
- <span data-ttu-id="5ba58-499">這項功能並沒有顯著的影響，在 edge server toohello 要求者所傳遞的 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-499">This feature does not have an observable effect on hello response delivered by an edge server toohello requester.</span></span> <span data-ttu-id="5ba58-500">不過，它可能會重新驗證流量從我們的邊緣伺服器 toohello 原始伺服器傳送的 hello 量影響。</span><span class="sxs-lookup"><span data-stu-id="5ba58-500">However, it may have an effect on hello amount of revalidation traffic sent from our edge servers toohello origin server.</span></span>
- <span data-ttu-id="5ba58-501">以下列方式設定此功能：</span><span class="sxs-lookup"><span data-stu-id="5ba58-501">Configure this feature by:</span></span>
    - <span data-ttu-id="5ba58-502">選取會套用內部的最大年齡 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-502">Selecting hello status code for which an internal max-age will be applied.</span></span>
    - <span data-ttu-id="5ba58-503">指定整數值，然後選取 hello 所需的時間單位 （也就是，秒、 分鐘、 小時等等）。</span><span class="sxs-lookup"><span data-stu-id="5ba58-503">Specifying an integer value and selecting hello desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="5ba58-504">這個值定義 hello 要求的最大時間間隔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-504">This value defines hello request's max-age interval.</span></span>

- <span data-ttu-id="5ba58-505">設定 hello 時間單位太 「 關閉 」 時停用此功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-505">Setting hello time unit too"Off" disables this feature.</span></span> <span data-ttu-id="5ba58-506">內部的最大時間間隔將不會指派 toorequested 資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-506">An internal max-age interval will not be assigned toorequested assets.</span></span> <span data-ttu-id="5ba58-507">如果 hello 原始的標頭不包含快取的指示，然後 hello 資產會快取，根據 toohello 預設內部 Max-age 功能中的使用中設定。</span><span class="sxs-lookup"><span data-stu-id="5ba58-507">If hello original header does not contain caching instructions, then hello asset will be cached according toohello active setting in the Default Internal Max-Age feature.</span></span>
- <span data-ttu-id="5ba58-508">Toohello 追蹤哪一個快取設定的方式，因為這項功能無法關聯以 hello 下列比對條件：</span><span class="sxs-lookup"><span data-stu-id="5ba58-508">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following match conditions:</span></span> 
    - <span data-ttu-id="5ba58-509">Edge</span><span class="sxs-lookup"><span data-stu-id="5ba58-509">Edge</span></span> 
    - <span data-ttu-id="5ba58-510">Cname</span><span class="sxs-lookup"><span data-stu-id="5ba58-510">Cname</span></span>
    - <span data-ttu-id="5ba58-511">要求標頭常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-511">Request Header Literal</span></span>
    - <span data-ttu-id="5ba58-512">要求標頭萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-512">Request Header Wildcard</span></span>
    - <span data-ttu-id="5ba58-513">要求方法</span><span class="sxs-lookup"><span data-stu-id="5ba58-513">Request Method</span></span>
    - <span data-ttu-id="5ba58-514">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-514">URL Query Literal</span></span>
    - <span data-ttu-id="5ba58-515">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-515">URL Query Wildcard</span></span>

<span data-ttu-id="5ba58-516">**預設行為：**關閉</span><span class="sxs-lookup"><span data-stu-id="5ba58-516">**Default Behavior:** Off</span></span>

###<a name="h264-support-http-progressive-download"></a><span data-ttu-id="5ba58-517">H.264 支援 (HTTP 漸進式下載)</span><span class="sxs-lookup"><span data-stu-id="5ba58-517">H.264 Support (HTTP Progressive Download)</span></span>
<span data-ttu-id="5ba58-518">**用途：** H.264 判斷 hello 種檔案格式，可能會使用的 toostream 內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-518">**Purpose:** Determines hello types of H.264 file formats that may be used toostream content.</span></span>

<span data-ttu-id="5ba58-519">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-519">Key information:</span></span>

- <span data-ttu-id="5ba58-520">在 [副檔名] 選項中，定義一組允許的 H.264 副檔名 (以空格分隔)。</span><span class="sxs-lookup"><span data-stu-id="5ba58-520">Define a space-delimited set of allowed H.264 filename extensions in the File Extensions option.</span></span> <span data-ttu-id="5ba58-521">檔案副檔名選項會覆寫 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-521">The File Extensions option will override hello default behavior.</span></span> <span data-ttu-id="5ba58-522">在設定此選項時包括這些副檔名，藉以保有 MP4 和 F4V 支援。</span><span class="sxs-lookup"><span data-stu-id="5ba58-522">Maintain MP4 and F4V support by including those filename extensions when setting this option.</span></span> 
- <span data-ttu-id="5ba58-523">請確定 tooinclude 句號時指定每個檔案的副檔名 (例如.mp4.f4v)。</span><span class="sxs-lookup"><span data-stu-id="5ba58-523">Make sure tooinclude a period when specifying each filename extension (e.g., .mp4 .f4v).</span></span>

<span data-ttu-id="5ba58-524">**預設行為︰**HTTP 漸進式下載預設支援 MP4 和 F4V 媒體。</span><span class="sxs-lookup"><span data-stu-id="5ba58-524">**Default Behavior:** HTTP Progressive Download supports MP4 and F4V media by default.</span></span>

###<a name="honor-no-cache-request"></a><span data-ttu-id="5ba58-525">接受 No-Cache 要求</span><span class="sxs-lookup"><span data-stu-id="5ba58-525">Honor no-cache request</span></span>
<span data-ttu-id="5ba58-526">**用途：**決定 HTTP 用戶端的無快取要求是否會轉送 toohello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-526">**Purpose:** Determines whether an HTTP client's no-cache requests will be forwarded toohello origin server.</span></span>

<span data-ttu-id="5ba58-527">無快取要求發生於 hello HTTP 用戶端會傳送快取的控制項： 沒有-快取和/或 Pragma:no-hello HTTP 要求中的快取標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-527">A no-cache request occurs when hello HTTP client sends a Cache-Control:no-cache and/or Pragma:no-cache header in hello HTTP request.</span></span>

<span data-ttu-id="5ba58-528">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-528">Value</span></span>|<span data-ttu-id="5ba58-529">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-529">Result</span></span>
--|--
<span data-ttu-id="5ba58-530">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-530">Enabled</span></span>|<span data-ttu-id="5ba58-531">允許 HTTP 用戶端的無快取要求 toobe 轉送的 toohello 原始伺服器，並 hello 原始伺服器將會傳回 hello 回應標頭和透過 hello 邊緣伺服器 hello 主體回復 toohello HTTP 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5ba58-531">Allows an HTTP client's no-cache requests toobe forwarded toohello origin server, and hello origin server will return hello response headers and hello body through hello edge server back toohello HTTP client.</span></span>
<span data-ttu-id="5ba58-532">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-532">Disabled</span></span>|<span data-ttu-id="5ba58-533">還原 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-533">Restores hello default behavior.</span></span> <span data-ttu-id="5ba58-534">hello 預設行為是從轉遞 toohello 原始伺服器的 tooprevent 無快取要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-534">hello default behavior is tooprevent no-cache requests from being forwarded toohello origin server.</span></span>

<span data-ttu-id="5ba58-535">對所有的生產流量很高建議 tooleave 這項功能預設為停用狀態。</span><span class="sxs-lookup"><span data-stu-id="5ba58-535">For all production traffic, it is highly recommended tooleave this feature in its default disabled state.</span></span> <span data-ttu-id="5ba58-536">否則，原始伺服器將未受防護的重新整理網頁時不小心可能會觸發多無快取要求的使用者或 hello 從許多熱門的媒體播放程式的自動程式化 toosend 無快取標頭與每個視訊的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-536">Otherwise, origin servers will not be shielded from end-users who may inadvertently trigger many no-cache requests when refreshing web pages, or from hello many popular media players that are coded toosend a no-cache header with every video request.</span></span> <span data-ttu-id="5ba58-537">儘管如此，這個功能便相當有用 tooapply toocertain 非生產臨時或順序 tooallow 全新內容 toobe 中測試的目錄，視取自 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-537">Nevertheless, this feature can be useful tooapply toocertain non-production staging or testing directories, in order tooallow fresh content toobe pulled on-demand from hello origin server.</span></span>

<span data-ttu-id="5ba58-538">將報告轉寄 toobe tooan 原始伺服器，因為 toothis 功能 TCP_Client_Refresh_Miss 允許要求的 hello 快取狀態。</span><span class="sxs-lookup"><span data-stu-id="5ba58-538">hello cache status that will be reported for a request that is allowed toobe forwarded tooan origin server due toothis feature is TCP_Client_Refresh_Miss.</span></span> <span data-ttu-id="5ba58-539">快取狀態報告，可用於在 hello 核心報告模組中，提供依快取狀態的統計資訊。</span><span class="sxs-lookup"><span data-stu-id="5ba58-539">The Cache Statuses report, which is available in hello Core reporting module, provides statistical information by cache status.</span></span> <span data-ttu-id="5ba58-540">這可讓您 tootrack hello 數目以及 tooan 原始伺服器，因為 toothis 功能正在轉送的要求百分比。</span><span class="sxs-lookup"><span data-stu-id="5ba58-540">This allows you tootrack hello number and percentage of requests that are being forwarded tooan origin server due toothis feature.</span></span>

<span data-ttu-id="5ba58-541">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-541">**Default Behavior:** Disabled.</span></span>

###<a name="ignore-origin-no-cache"></a><span data-ttu-id="5ba58-542">忽略原始的 No-Cache</span><span class="sxs-lookup"><span data-stu-id="5ba58-542">Ignore Origin no-cache</span></span>
<span data-ttu-id="5ba58-543">**用途：**決定是否我們 CDN 將會忽略下列指示詞從來源伺服器提供服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-543">**Purpose:** Determines whether our CDN will ignore hello following directives served from an origin server:</span></span>

- <span data-ttu-id="5ba58-544">Cache-Control: private</span><span class="sxs-lookup"><span data-stu-id="5ba58-544">Cache-Control: private</span></span>
- <span data-ttu-id="5ba58-545">Cache-Control: no-store</span><span class="sxs-lookup"><span data-stu-id="5ba58-545">Cache-Control: no-store</span></span>
- <span data-ttu-id="5ba58-546">Cache-Control: no-cache</span><span class="sxs-lookup"><span data-stu-id="5ba58-546">Cache-Control: no-cache</span></span>
- <span data-ttu-id="5ba58-547">Pragma: no-cache</span><span class="sxs-lookup"><span data-stu-id="5ba58-547">Pragma: no-cache</span></span>

<span data-ttu-id="5ba58-548">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-548">Key information:</span></span>

- <span data-ttu-id="5ba58-549">設定這項功能所定義的狀態碼將會忽略指示詞上方 hello 以空格分隔的清單。</span><span class="sxs-lookup"><span data-stu-id="5ba58-549">Configure this feature by defining a space-delimited list of status codes for which hello above directives will be ignored.</span></span>
- <span data-ttu-id="5ba58-550">hello 一組有效狀態碼，這項功能是： 200、 203、 300、 301、 302、 305、 307、 400、 401、 402、 403、 404、 405、 406、 407、 408、 409、 410、 411、 412、 413、 414、 415、 416、 417、 500、 501、 502、 503、 504 和 505。</span><span class="sxs-lookup"><span data-stu-id="5ba58-550">hello set of valid status codes for this feature are: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, and 505.</span></span>
- <span data-ttu-id="5ba58-551">停用此功能，以設定 tooa 空白值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-551">Disable this feature by setting it tooa blank value.</span></span>
- <span data-ttu-id="5ba58-552">Toohello 追蹤哪一個快取設定的方式，因為這項功能無法關聯以 hello 下列比對條件：</span><span class="sxs-lookup"><span data-stu-id="5ba58-552">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following match conditions:</span></span> 
    - <span data-ttu-id="5ba58-553">Edge</span><span class="sxs-lookup"><span data-stu-id="5ba58-553">Edge</span></span> 
    - <span data-ttu-id="5ba58-554">Cname</span><span class="sxs-lookup"><span data-stu-id="5ba58-554">Cname</span></span>
    - <span data-ttu-id="5ba58-555">要求標頭常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-555">Request Header Literal</span></span>
    - <span data-ttu-id="5ba58-556">要求標頭萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-556">Request Header Wildcard</span></span>
    - <span data-ttu-id="5ba58-557">要求方法</span><span class="sxs-lookup"><span data-stu-id="5ba58-557">Request Method</span></span>
    - <span data-ttu-id="5ba58-558">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-558">URL Query Literal</span></span>
    - <span data-ttu-id="5ba58-559">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-559">URL Query Wildcard</span></span>

<span data-ttu-id="5ba58-560">**預設行為：**的預設行為是 toohonor hello 上述指示詞。</span><span class="sxs-lookup"><span data-stu-id="5ba58-560">**Default Behavior:** The default behavior is toohonor hello above directives.</span></span>

###<a name="ignore-unsatisfiable-ranges"></a><span data-ttu-id="5ba58-561">忽略無法滿足的範圍</span><span class="sxs-lookup"><span data-stu-id="5ba58-561">Ignore Unsatisfiable Ranges</span></span> 
<span data-ttu-id="5ba58-562">**用途：**決定時，會傳回 tooclients 要求會產生 416 的範圍無法滿足的要求狀態碼的 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-562">**Purpose:** Determines hello response that will be returned tooclients when a request generates a 416 Requested Range Not Satisfiable status code.</span></span>

<span data-ttu-id="5ba58-563">根據預設，hello 指定位元組範圍要求無法滿足 edge server，而且如果範圍要求標頭欄位沒有指定時，會傳回此狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-563">By default, this status code is returned when hello specified byte-range request cannot be satisfied by an edge server and an If-Range request header field was not specified.</span></span>

<span data-ttu-id="5ba58-564">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-564">Value</span></span>|<span data-ttu-id="5ba58-565">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-565">Result</span></span>
-|-
<span data-ttu-id="5ba58-566">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-566">Enabled</span></span>|<span data-ttu-id="5ba58-567">可防止從 416 的範圍無法滿足的要求狀態碼回應 tooan 無效的位元組範圍要求我們邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-567">Prevents our edge servers from responding tooan invalid byte-range request with a 416 Requested Range Not Satisfiable status code.</span></span> <span data-ttu-id="5ba58-568">我們的伺服器會傳送 hello 要求的資產而傳回 200 確定 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5ba58-568">Instead our servers will deliver hello requested asset and return a 200 OK to hello client.</span></span>
<span data-ttu-id="5ba58-569">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-569">Disabled</span></span>|<span data-ttu-id="5ba58-570">還原 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-570">Restores hello default behavior.</span></span> <span data-ttu-id="5ba58-571">hello 預設行為是 toohonor 416 的範圍無法滿足的要求狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-571">hello default behavior is toohonor the 416 Requested Range Not Satisfiable status code.</span></span>

<span data-ttu-id="5ba58-572">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-572">**Default Behavior:** Disabled.</span></span>

###<a name="internal-max-stale"></a><span data-ttu-id="5ba58-573">內部最大過時</span><span class="sxs-lookup"><span data-stu-id="5ba58-573">Internal Max-Stale</span></span>
<span data-ttu-id="5ba58-574">**用途：**控制多久過去的 hello 正常的到期時間，可能會從邊緣伺服器提供的快取的資產，hello 邊緣伺服器時無法 toorevalidate hello 快取資產 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-574">**Purpose:** Controls how long past hello normal expiration time a cached asset may be served from an edge server when hello edge server is unable toorevalidate hello cached asset with hello origin server.</span></span>

<span data-ttu-id="5ba58-575">一般來說，當資產的保留時間上限已逾期，hello 邊緣伺服器會傳送重新驗證要求 toohello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-575">Normally, when an asset's max-age time expires, hello edge server will send a revalidation request toohello origin server.</span></span> <span data-ttu-id="5ba58-576">hello 原始伺服器將會再回應 304 不修改成 hello 邊緣為伺服器提供全新租用 hello 快取資產，或以其他方式與 200 [確定] 以提供更新版的 hello 快取資產 hello 邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-576">hello origin server will then respond with either a 304 Not Modified to give hello edge server a fresh lease on hello cached asset, or else with 200 OK to provide hello edge server with an updated version of hello cached asset.</span></span>

<span data-ttu-id="5ba58-577">如果 hello 邊緣伺服器無法 tooestablish hello 原始伺服器的連線嘗試重新驗證時，然後此內部的最大過時功能可控制是否，以及多久，hello 邊緣伺服器可能會繼續 tooserve hello 現在過時資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-577">If hello edge server is unable tooestablish a connection with hello origin server while attempting such a revalidation, then this Internal Max-Stale feature controls whether, and for how long, hello edge server may continue tooserve hello now-stale asset.</span></span>

<span data-ttu-id="5ba58-578">請注意，此時間間隔內啟動 hello 資產的最大期限過期時，不會在 hello 失敗的重新驗證，就會發生。</span><span class="sxs-lookup"><span data-stu-id="5ba58-578">Note that this time interval starts when hello asset's max-age expires, not when hello failed revalidation occurs.</span></span> <span data-ttu-id="5ba58-579">因此，在可提供資產不成功的重新驗證的 hello 最長為 hello 的保留時間上限加上最大過時的 hello 組合所指定的時間量。</span><span class="sxs-lookup"><span data-stu-id="5ba58-579">Therefore, hello maximum period during which an asset can be served without successful revalidation is hello amount of time specified by hello combination of max-age plus max-stale.</span></span> <span data-ttu-id="5ba58-580">例如，如果資產快取的 9:00 過時 max 15 分鐘、 30 分鐘的最大存留期與失敗的重新驗證嘗試在 9:44 會導致使用者接收 hello 過時快取資產，而 9:46 失敗的重新驗證嘗試會導致hello 終端使用者接收 504 閘道逾時。</span><span class="sxs-lookup"><span data-stu-id="5ba58-580">For example, if an asset was cached at 9:00 with a max-age of 30 minutes and a max-stale of 15 minutes, then a failed revalidation attempt at 9:44 would result in an end-user receiving hello stale cached asset, while a failed revalidation attempt at 9:46 would result in hello end user receiving a 504 Gateway Timeout.</span></span>

<span data-ttu-id="5ba58-581">針對這項功能已被取代快取所設定的任何值的控制項： 必須-重新驗證，或是快取-控制： proxy-重新驗證從 hello 原始伺服器收到的標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-581">Any value configured for this feature is superseded by Cache-Control:must-revalidate or Cache-Control:proxy-revalidate headers received from hello origin server.</span></span> <span data-ttu-id="5ba58-582">如果任一這些標頭收到 hello 原始伺服器從一開始快取資產時，hello 邊緣伺服器將不會提供過時的快取的資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-582">If either of those headers is received from hello origin server when an asset is initially cached, then hello edge server will not serve a stale cached asset.</span></span> <span data-ttu-id="5ba58-583">在這種情況下，如果 hello 邊緣伺服器時，無法與 hello 原點 toorevalidate hello 資產的最大時間間隔已過期，然後 hello 邊緣伺服器會傳回 504 閘道逾時。</span><span class="sxs-lookup"><span data-stu-id="5ba58-583">In such a case, if hello edge server is unable toorevalidate with hello origin when hello asset's max-age interval has expired, then hello edge server will return a 504 Gateway Timeout.</span></span>

<span data-ttu-id="5ba58-584">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-584">Key information:</span></span>

- <span data-ttu-id="5ba58-585">以下列方式設定此功能：</span><span class="sxs-lookup"><span data-stu-id="5ba58-585">Configure this feature by:</span></span>
    - <span data-ttu-id="5ba58-586">選取會套用最大過時 hello 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-586">Selecting hello status code for which a max-stale will be applied.</span></span>
    - <span data-ttu-id="5ba58-587">指定的整數值，然後選取 hello 所需的時間單位 （也就是，秒、 分鐘、 小時等等）。</span><span class="sxs-lookup"><span data-stu-id="5ba58-587">Specifying an integer value and then selecting hello desired time unit (i.e., seconds, minutes, hours, etc.).</span></span> <span data-ttu-id="5ba58-588">此值會定義 hello 內部 max 過時，將會套用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-588">This value defines hello internal max-stale that will be applied.</span></span>

- <span data-ttu-id="5ba58-589">設定 hello 時間單位太 「 關閉 」 將會停用這項功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-589">Setting hello time unit too"Off" will disable this feature.</span></span> <span data-ttu-id="5ba58-590">系統將不會在快取的資產超過一般到期時間之後為其提供服務。</span><span class="sxs-lookup"><span data-stu-id="5ba58-590">A cached asset will not be served beyond its normal expiration time.</span></span>
- <span data-ttu-id="5ba58-591">Toohello 追蹤哪一個快取設定的方式，因為這項功能無法關聯以 hello 下列比對條件：</span><span class="sxs-lookup"><span data-stu-id="5ba58-591">Due toohello manner in which cache settings are tracked, this feature cannot be associated with hello following match conditions:</span></span> 
    - <span data-ttu-id="5ba58-592">Edge</span><span class="sxs-lookup"><span data-stu-id="5ba58-592">Edge</span></span> 
    - <span data-ttu-id="5ba58-593">Cname</span><span class="sxs-lookup"><span data-stu-id="5ba58-593">Cname</span></span>
    - <span data-ttu-id="5ba58-594">要求標頭常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-594">Request Header Literal</span></span>
    - <span data-ttu-id="5ba58-595">要求標頭萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-595">Request Header Wildcard</span></span>
    - <span data-ttu-id="5ba58-596">要求方法</span><span class="sxs-lookup"><span data-stu-id="5ba58-596">Request Method</span></span>
    - <span data-ttu-id="5ba58-597">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-597">URL Query Literal</span></span>
    - <span data-ttu-id="5ba58-598">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-598">URL Query Wildcard</span></span>

<span data-ttu-id="5ba58-599">**預設行為：**2 分鐘</span><span class="sxs-lookup"><span data-stu-id="5ba58-599">**Default Behavior:** 2 minutes</span></span>

###<a name="partial-cache-sharing"></a><span data-ttu-id="5ba58-600">部分快取共用</span><span class="sxs-lookup"><span data-stu-id="5ba58-600">Partial Cache Sharing</span></span>
<span data-ttu-id="5ba58-601">**目的：**判斷要求是否可以產生部分快取的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-601">**Purpose:** Determines whether a request can generate partially cached content.</span></span>

<span data-ttu-id="5ba58-602">Hello 要求完整快取內容之前，此部分快取可能則是使用的 toofulfill 新要求該內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-602">This partial cache may then be used toofulfill new requests for that content until hello requested content is fully cached.</span></span>

<span data-ttu-id="5ba58-603">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-603">Value</span></span>|<span data-ttu-id="5ba58-604">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-604">Result</span></span>
-|-
<span data-ttu-id="5ba58-605">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-605">Enabled</span></span>|<span data-ttu-id="5ba58-606">要求可以產生部分快取的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-606">Requests can generate partially cached content.</span></span>
<span data-ttu-id="5ba58-607">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-607">Disabled</span></span>|<span data-ttu-id="5ba58-608">要求只會產生完整快取版的 hello 要求內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-608">Requests can only generate a fully cached version of hello requested content.</span></span>

<span data-ttu-id="5ba58-609">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-609">**Default Behavior:** Disabled.</span></span>

###<a name="prevalidate-cached-content"></a><span data-ttu-id="5ba58-610">預先驗證快取的內容</span><span class="sxs-lookup"><span data-stu-id="5ba58-610">Prevalidate Cached Content</span></span>
<span data-ttu-id="5ba58-611">**目的：**在快取內容的 TTL 到期之前，判斷其是否適用進行早期重新驗證。</span><span class="sxs-lookup"><span data-stu-id="5ba58-611">**Purpose:** Determines whether cached content will be eligible for early revalidation before its TTL expires.</span></span>

<span data-ttu-id="5ba58-612">定義 hello 一段時間的 hello 先前 toohello 到期要求內容的 TTL 期間會很適合早期重新驗證。</span><span class="sxs-lookup"><span data-stu-id="5ba58-612">Define hello amount of time prior toohello expiration of hello requested content's TTL during which it will be eligible for early revalidation.</span></span>

<span data-ttu-id="5ba58-613">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-613">Key information:</span></span>

- <span data-ttu-id="5ba58-614">Hello 快取內容的 TTL 過期後選取 「 關閉 」 hello 時間單位為需要重新驗證 tootake 位置。</span><span class="sxs-lookup"><span data-stu-id="5ba58-614">Selecting "Off" as hello time unit requires revalidation tootake place after hello cached content's TTL has expired.</span></span> <span data-ttu-id="5ba58-615">不應指定時間，且將會予以忽略。</span><span class="sxs-lookup"><span data-stu-id="5ba58-615">Time should not be specified and it will be ignored.</span></span>

<span data-ttu-id="5ba58-616">**預設行為：**關閉。</span><span class="sxs-lookup"><span data-stu-id="5ba58-616">**Default Behavior:** Off.</span></span> <span data-ttu-id="5ba58-617">重新驗證快取的內容 TTL 過期的 hello 之後，可能只會發生。</span><span class="sxs-lookup"><span data-stu-id="5ba58-617">Revalidation may only take place after hello cached content's TTL has expired.</span></span>

###<a name="refresh-zero-byte-cache-files"></a><span data-ttu-id="5ba58-618">重新整理零位元組的快取檔案</span><span class="sxs-lookup"><span data-stu-id="5ba58-618">Refresh Zero Byte Cache Files</span></span>
<span data-ttu-id="5ba58-619">**目的：**判斷如何透過 Edge Server 來處理 HTTP 用戶端對於 0 位元組快取資產的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-619">**Purpose:** Determines how an HTTP client's request for a 0-byte cache asset is handled by our edge servers.</span></span>

<span data-ttu-id="5ba58-620">有效值為：</span><span class="sxs-lookup"><span data-stu-id="5ba58-620">Valid values are:</span></span>

<span data-ttu-id="5ba58-621">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-621">Value</span></span>|<span data-ttu-id="5ba58-622">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-622">Result</span></span>
--|--
<span data-ttu-id="5ba58-623">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-623">Enabled</span></span>|<span data-ttu-id="5ba58-624">Edge server toore 提取 hello 資產，讓從 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-624">Causes our edge server toore-fetch hello asset from hello origin server.</span></span>
<span data-ttu-id="5ba58-625">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-625">Disabled</span></span>|<span data-ttu-id="5ba58-626">還原 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-626">Restores hello default behavior.</span></span> <span data-ttu-id="5ba58-627">hello 預設行為是 tooserve 向上收到要求時有效的快取資產。</span><span class="sxs-lookup"><span data-stu-id="5ba58-627">hello default behavior is tooserve up valid cache assets upon request.</span></span>
<span data-ttu-id="5ba58-628">不需要此功能即可進行正確的快取和內容傳遞，但此功能可能有助於解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="5ba58-628">This feature is not required for correct caching and content delivery, but may be useful as a workaround.</span></span> <span data-ttu-id="5ba58-629">比方說，在來源伺服器上的動態內容產生器不小心造成位元組 0 回應傳送 toohello 邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-629">For example, dynamic content generators on origin servers can inadvertently result in 0-byte responses being sent toohello edge servers.</span></span> <span data-ttu-id="5ba58-630">我們的 Edge Server 通常會快取這些類型的回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-630">These types of responses are typically cached by our edge servers.</span></span> <span data-ttu-id="5ba58-631">如果您知道對於這類內容而言，0 位元組的回應絕對不是有效的回應，</span><span class="sxs-lookup"><span data-stu-id="5ba58-631">If you know that a 0-byte response is never a valid response</span></span> 

<span data-ttu-id="5ba58-632">如需這類的內容，然後這項功能可避免這些類型的資產提供 tooyour 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5ba58-632">for such content, then this feature can prevent these types of assets from being served tooyour clients.</span></span>

<span data-ttu-id="5ba58-633">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-633">**Default Behavior:** Disabled.</span></span>

###<a name="set-cacheable-status-codes"></a><span data-ttu-id="5ba58-634">設定可快取的狀態碼</span><span class="sxs-lookup"><span data-stu-id="5ba58-634">Set Cacheable Status Codes</span></span>
<span data-ttu-id="5ba58-635">**用途：**定義 hello 組可能會導致快取內容的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-635">**Purpose:** Defines hello set of status codes that can result in cached content.</span></span>

<span data-ttu-id="5ba58-636">根據預設，只會針對 [200 確定] 回應啟用快取。</span><span class="sxs-lookup"><span data-stu-id="5ba58-636">By default, caching is only enabled for 200 OK responses.</span></span>

<span data-ttu-id="5ba58-637">定義以空格分隔組 hello 預期的狀態碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-637">Define a space-delimited set of hello desired status codes.</span></span>

<span data-ttu-id="5ba58-638">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-638">Key information:</span></span>

- <span data-ttu-id="5ba58-639">另請啟用 [忽略原始的 No-Cache] 功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-639">Please also enable the Ignore Origin No-Cache feature.</span></span> <span data-ttu-id="5ba58-640">如果未啟用該功能，則可能不會快取非 [200 確定] 的回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-640">If that feature is not enabled, then non-200 OK responses may not be cached.</span></span>
- <span data-ttu-id="5ba58-641">hello 一組有效狀態碼，這項功能是： 203、 300、 301、 302、 305、 307、 400、 401、 402、 403、 404、 405、 406、 407、 408、 409、 410、 411、 412、 413、 414、 415、 416、 417、 500、 501、 502、 503、 504 和 505。</span><span class="sxs-lookup"><span data-stu-id="5ba58-641">hello set of valid status codes for this feature are: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504, and 505.</span></span>
- <span data-ttu-id="5ba58-642">這項功能不能使用的 toodisable 產生 200 OK 狀態碼的回應的快取。</span><span class="sxs-lookup"><span data-stu-id="5ba58-642">This feature cannot be used toodisable caching for responses that generate a 200 OK status code.</span></span>

<span data-ttu-id="5ba58-643">**預設行為︰**只會針對產生 [200 確定] 狀態碼的回應啟用快取。</span><span class="sxs-lookup"><span data-stu-id="5ba58-643">**Default Behavior:** Caching is only enabled for responses that generate a 200 OK status code.</span></span>
###<a name="stale-content-delivery-on-error"></a><span data-ttu-id="5ba58-644">發生錯誤時傳遞過時的內容</span><span class="sxs-lookup"><span data-stu-id="5ba58-644">Stale Content Delivery on Error</span></span>
<span data-ttu-id="5ba58-645">**目的：**</span><span class="sxs-lookup"><span data-stu-id="5ba58-645">**Purpose:**</span></span> 

<span data-ttu-id="5ba58-646">判斷是否已過期期間快取重新驗證，或擷取 hello hello 客戶原始伺服器要求內容時，發生錯誤時，將會傳遞快取的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-646">Determines whether expired cached content will be delivered when an error occurs during cache revalidation or when retrieving hello requested content from hello customer origin server.</span></span>

<span data-ttu-id="5ba58-647">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-647">Value</span></span>|<span data-ttu-id="5ba58-648">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-648">Result</span></span>
-|-
<span data-ttu-id="5ba58-649">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-649">Enabled</span></span>|<span data-ttu-id="5ba58-650">連接 tooan 原始伺服器期間發生錯誤時，過時的內容會提供 toohello 要求者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-650">Stale content will be served toohello requester when an error occurs during a connection tooan origin server.</span></span>
<span data-ttu-id="5ba58-651">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-651">Disabled</span></span>|<span data-ttu-id="5ba58-652">hello 原始伺服器的錯誤將會轉送 toohello 要求者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-652">hello origin server's error will be forwarded toohello requester.</span></span>

<span data-ttu-id="5ba58-653">**預設行為：**已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-653">**Default Behavior:** Disabled</span></span>

###<a name="stale-while-revalidate"></a><span data-ttu-id="5ba58-654">在重新驗證時過期</span><span class="sxs-lookup"><span data-stu-id="5ba58-654">Stale While Revalidate</span></span>
<span data-ttu-id="5ba58-655">**用途：**藉由使用我們的邊緣伺服器 tooserve 過時內容 toohello 要求者重新驗證時，可以改善效能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-655">**Purpose:** Improves performance by allowing our edge servers tooserve stale content toohello requester while revalidation takes place.</span></span>

<span data-ttu-id="5ba58-656">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-656">Key information:</span></span>

- <span data-ttu-id="5ba58-657">這項功能的 hello 行為有所不同相應 toohello 選取的時間單位。</span><span class="sxs-lookup"><span data-stu-id="5ba58-657">hello behavior of this feature varies according toohello selected time unit.</span></span>
    - <span data-ttu-id="5ba58-658">**時間單位：**指定的時間長度，然後選取時間單位 （例如秒、 分鐘、 小時等等） tooallow 過時內容傳遞。</span><span class="sxs-lookup"><span data-stu-id="5ba58-658">**Time Unit:** Specify a length of time and select a time unit (e.g., Seconds, Minutes, Hours, etc.) tooallow stale content delivery.</span></span> <span data-ttu-id="5ba58-659">此類型的安裝程式允許 hello CDN tooextend hello 段期間內，可能會傳遞內容之前需要驗證，根據下列公式 toohello:**TTL** + **過時時重新驗證時間**</span><span class="sxs-lookup"><span data-stu-id="5ba58-659">This type of setup allows hello CDN tooextend hello length of time that it may deliver content before requiring validation according toohello following formula:**TTL** + **Stale While Revalidate Time**</span></span> 
    - <span data-ttu-id="5ba58-660">**關閉：**選取 「 關閉 」 toorequire 重新驗證的要求之前可能會提供過時的內容。</span><span class="sxs-lookup"><span data-stu-id="5ba58-660">**Off:** Select "Off" toorequire revalidation before a request for stale content may be served.</span></span>
        - <span data-ttu-id="5ba58-661">請勿指定時間長度，因為它不適用且將會遭到忽略。</span><span class="sxs-lookup"><span data-stu-id="5ba58-661">Do not specify a length of time since it is inapplicable and will be ignored.</span></span>

<span data-ttu-id="5ba58-662">**預設行為：**關閉。</span><span class="sxs-lookup"><span data-stu-id="5ba58-662">**Default Behavior:** Off.</span></span> <span data-ttu-id="5ba58-663">重新驗證 hello 要求可以提供內容之前，必須先完成。</span><span class="sxs-lookup"><span data-stu-id="5ba58-663">Revalidation must take place before hello requested content can be served.</span></span>

###<a name="comment"></a><span data-ttu-id="5ba58-664">註解</span><span class="sxs-lookup"><span data-stu-id="5ba58-664">Comment</span></span>
<span data-ttu-id="5ba58-665">**用途：**允許規則中新增附註 toobe。</span><span class="sxs-lookup"><span data-stu-id="5ba58-665">**Purpose:** Allows a note toobe added within a rule.</span></span>

<span data-ttu-id="5ba58-666">這項功能的其中一個使用 tooprovide hello 一般用途的規則上的其他資訊或特定原因符合條件或功能已加入 toohello 規則。</span><span class="sxs-lookup"><span data-stu-id="5ba58-666">One use for this feature is tooprovide additional information on hello general purpose of a rule or why a particular match condition or feature was added toohello rule.</span></span>

<span data-ttu-id="5ba58-667">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-667">Key information:</span></span>

- <span data-ttu-id="5ba58-668">您最多可以指定 150 個字元。</span><span class="sxs-lookup"><span data-stu-id="5ba58-668">A maximum of 150 characters may be specified.</span></span>
- <span data-ttu-id="5ba58-669">請確定 tooonly 使用英數字元。</span><span class="sxs-lookup"><span data-stu-id="5ba58-669">Make sure tooonly use alphanumeric characters.</span></span>
- <span data-ttu-id="5ba58-670">這項功能不會影響 hello 規則的 hello 行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-670">This feature does not affect hello behavior of hello rule.</span></span> <span data-ttu-id="5ba58-671">它只是用的 tooprovide 疑難排解 hello 規則時，可協助您可以提供位置資訊供未來參考或的區域。</span><span class="sxs-lookup"><span data-stu-id="5ba58-671">It is merely meant tooprovide an area where you can provide information for future reference or that may help when troubleshooting hello rule.</span></span>
 
## <a name="headers"></a><span data-ttu-id="5ba58-672">headers</span><span class="sxs-lookup"><span data-stu-id="5ba58-672">Headers</span></span>

<span data-ttu-id="5ba58-673">這些功能是設計的 tooadd、 修改或刪除 hello 要求或回應的標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-673">These features are designed tooadd, modify, or delete headers from hello request or response.</span></span>

<span data-ttu-id="5ba58-674">名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-674">Name</span></span> | <span data-ttu-id="5ba58-675">目的</span><span class="sxs-lookup"><span data-stu-id="5ba58-675">Purpose</span></span>
-----|--------
<span data-ttu-id="5ba58-676">Age 回應標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-676">Age Response Header</span></span> | <span data-ttu-id="5ba58-677">決定是否將傳送 toohello 要求者的 hello 回應中包含的 Age 回應標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-677">Determines whether an Age response header will be included in hello response sent toohello requester.</span></span>
<span data-ttu-id="5ba58-678">偵錯快取回應標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-678">Debug Cache Response Headers</span></span> | <span data-ttu-id="5ba58-679">決定是否回應可能包括 hello 偵錯 EC 月 X 日回應標頭提供 hello hello 要求資產的快取原則的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="5ba58-679">Determines whether a response may include hello X-EC-Debug response header which provides information on hello cache policy for hello requested asset.</span></span>
<span data-ttu-id="5ba58-680">修改用戶端要求標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-680">Modify Client Request Header</span></span> | <span data-ttu-id="5ba58-681">覆寫、附加或刪除要求的標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-681">Overwrites, appends, or deletes a header from a request.</span></span>
<span data-ttu-id="5ba58-682">修改用戶端回應標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-682">Modify Client Response Header</span></span> | <span data-ttu-id="5ba58-683">覆寫、附加或刪除回應的標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-683">Overwrites, appends, or deletes a header from a response.</span></span>
<span data-ttu-id="5ba58-684">設定用戶端 IP 自訂標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-684">Set Client IP Custom Header</span></span> | <span data-ttu-id="5ba58-685">可讓 toobe 加入的 toohello 要求 hello hello 提出要求的用戶端 IP 位址做為自訂要求標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-685">Allows hello IP address of hello requesting client toobe added toohello request as a custom request header.</span></span>

###<a name="age-response-header"></a><span data-ttu-id="5ba58-686">Age 回應標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-686">Age Response Header</span></span>
<span data-ttu-id="5ba58-687">**目的**： 決定是否要 Age 回應標頭包含在 hello 傳送回應 toohello 要求者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-687">**Purpose**: Determines whether an Age response header will be included in hello response sent toohello requester.</span></span>
<span data-ttu-id="5ba58-688">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-688">Value</span></span>|<span data-ttu-id="5ba58-689">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-689">Result</span></span>
--|--
<span data-ttu-id="5ba58-690">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-690">Enabled</span></span> | <span data-ttu-id="5ba58-691">hello Age 回應標頭將包含在傳送 toohello 要求者的 hello 回應中。</span><span class="sxs-lookup"><span data-stu-id="5ba58-691">hello Age response header will be included in hello response sent toohello requester.</span></span>
<span data-ttu-id="5ba58-692">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-692">Disabled</span></span> | <span data-ttu-id="5ba58-693">hello Age 回應標頭將排除 hello 回應傳送 toohello 要求者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-693">hello Age response header will be excluded from hello response sent toohello requester.</span></span>

<span data-ttu-id="5ba58-694">**預設行為**：已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-694">**Default Behavior**: Disabled.</span></span>

###<a name="debug-cache-response-headers"></a><span data-ttu-id="5ba58-695">偵錯快取回應標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-695">Debug Cache Response Headers</span></span>
<span data-ttu-id="5ba58-696">**用途：**決定是否回應可能會包含提供 hello hello 要求資產的快取原則的相關資訊的偵錯 EC 月 X 日回應標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-696">**Purpose:** Determines whether a response may include the X-EC-Debug response header which provides information on hello cache policy for hello requested asset.</span></span>

<span data-ttu-id="5ba58-697">偵錯快取的回應標頭會包含在 hello 回應 hello 下列都為 true 時：</span><span class="sxs-lookup"><span data-stu-id="5ba58-697">Debug cache response headers will be included in hello response when both of hello following are true:</span></span>

- <span data-ttu-id="5ba58-698">hello 偵錯快取的回應標頭功能已啟用在 hello 所要的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-698">hello Debug Cache Response Headers Feature has been enabled on hello desired request.</span></span>
- <span data-ttu-id="5ba58-699">上述要求 hello 定義偵錯快取的回應標頭會包含在 hello 回應 hello 組。</span><span class="sxs-lookup"><span data-stu-id="5ba58-699">hello above request defines hello set of debug cache response headers that will be included in hello response.</span></span>

<span data-ttu-id="5ba58-700">偵錯快取的回應標頭可能會要求包含下列標頭的 hello 和 hello hello 要求中所需的指示詞：</span><span class="sxs-lookup"><span data-stu-id="5ba58-700">Debug cache response headers may be requested by including hello following header and hello desired directives in hello request:</span></span>

<span data-ttu-id="5ba58-701">X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_</span><span class="sxs-lookup"><span data-stu-id="5ba58-701">X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_</span></span>

<span data-ttu-id="5ba58-702">**範例：**</span><span class="sxs-lookup"><span data-stu-id="5ba58-702">**Example:**</span></span>

<span data-ttu-id="5ba58-703">X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state</span><span class="sxs-lookup"><span data-stu-id="5ba58-703">X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state</span></span>

<span data-ttu-id="5ba58-704">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-704">Value</span></span>|<span data-ttu-id="5ba58-705">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-705">Result</span></span>
-|-
<span data-ttu-id="5ba58-706">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-706">Enabled</span></span>|<span data-ttu-id="5ba58-707">偵錯快取回應標頭的要求將傳回包含 X-EC-Debug 標頭的回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-707">Requests for debug cache response headers will return a response that includes the X-EC-Debug header.</span></span>
<span data-ttu-id="5ba58-708">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-708">Disabled</span></span>|<span data-ttu-id="5ba58-709">偵錯 EC 月 X 日回應標頭將排除 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-709">The X-EC-Debug response header will be excluded from hello response.</span></span>

<span data-ttu-id="5ba58-710">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-710">**Default Behavior:** Disabled.</span></span>

###<a name="modify-client-response-header"></a><span data-ttu-id="5ba58-711">修改用戶端回應標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-711">Modify Client Response Header</span></span>
<span data-ttu-id="5ba58-712">**目的︰**每個要求都會包含一組說明其本身的 [要求標頭]()。</span><span class="sxs-lookup"><span data-stu-id="5ba58-712">**Purpose:** Each request contains a set of [request headers]() that describe it.</span></span> <span data-ttu-id="5ba58-713">此功能可以：</span><span class="sxs-lookup"><span data-stu-id="5ba58-713">This feature can either:</span></span>

- <span data-ttu-id="5ba58-714">附加或覆寫 hello 分派 tooa 要求標頭的值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-714">Append or overwrite hello value assigned tooa request header.</span></span> <span data-ttu-id="5ba58-715">如果 hello 指定的要求標頭不存在，然後這項功能會將它 toohello 要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-715">If hello specified request header does not exist, then this feature will add it toohello request.</span></span>
- <span data-ttu-id="5ba58-716">刪除 hello 要求的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-716">Delete a request header from hello request.</span></span>

<span data-ttu-id="5ba58-717">轉送 tooan 原始伺服器的要求將會反映這項功能所做的 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="5ba58-717">Requests that are forwarded tooan origin server will reflect hello changes made by this feature.</span></span>

<span data-ttu-id="5ba58-718">要求標頭上，可以執行其中一個 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="5ba58-718">One of hello following actions can be performed on a request header:</span></span>

<span data-ttu-id="5ba58-719">選項</span><span class="sxs-lookup"><span data-stu-id="5ba58-719">Option</span></span>|<span data-ttu-id="5ba58-720">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-720">Description</span></span>|<span data-ttu-id="5ba58-721">範例</span><span class="sxs-lookup"><span data-stu-id="5ba58-721">Example</span></span>
-|-|-
<span data-ttu-id="5ba58-722">Append</span><span class="sxs-lookup"><span data-stu-id="5ba58-722">Append</span></span>|<span data-ttu-id="5ba58-723">hello 指定 hello 現有的要求標頭值的 toend 不會加入值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-723">hello specified value will be added toend of hello existing request header value.</span></span>|<span data-ttu-id="5ba58-724">**要求標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="5ba58-724">**Request header value (Client):**Value1</span></span> <br/> <span data-ttu-id="5ba58-725">**要求標頭值 (HTTP 規則引擎)：**Value2</span><span class="sxs-lookup"><span data-stu-id="5ba58-725">**Request header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="5ba58-726">**新的要求標頭值：**Value1Value2</span><span class="sxs-lookup"><span data-stu-id="5ba58-726">**New request header value:** Value1Value2</span></span>
<span data-ttu-id="5ba58-727">覆寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-727">Overwrite</span></span>|<span data-ttu-id="5ba58-728">標頭的值會設定 toohello hello 要求指定的值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-728">hello request header value will be set toohello specified value.</span></span>|<span data-ttu-id="5ba58-729">**要求標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="5ba58-729">**Request header value (Client):**Value1</span></span> <br/><span data-ttu-id="5ba58-730">**要求標頭值 (HTTP 規則引擎)：**Value2</span><span class="sxs-lookup"><span data-stu-id="5ba58-730">**Request header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="5ba58-731">**新的要求標頭值：**Value2</span><span class="sxs-lookup"><span data-stu-id="5ba58-731">**New request header value:** Value2</span></span> <br/>
<span data-ttu-id="5ba58-732">刪除</span><span class="sxs-lookup"><span data-stu-id="5ba58-732">Delete</span></span>|<span data-ttu-id="5ba58-733">刪除 hello 指定的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-733">Deletes hello specified request header.</span></span>|<span data-ttu-id="5ba58-734">**要求標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="5ba58-734">**Request header value (Client):**Value1</span></span> <br/> <span data-ttu-id="5ba58-735">**修改用戶端要求標頭設定：**刪除 hello 要求標頭有問題。</span><span class="sxs-lookup"><span data-stu-id="5ba58-735">**Modify Client Request Header configuration:** Delete hello request header in question.</span></span> <br/><span data-ttu-id="5ba58-736">**結果：** hello 可讓您指定的要求標頭不會轉送 toohello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-736">**Result:** hello specified request header will not be forwarded toohello origin server.</span></span>

<span data-ttu-id="5ba58-737">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-737">Key information:</span></span>

- <span data-ttu-id="5ba58-738">請確定在 [名稱] 選項中指定的 hello 值完全相符的 hello 所要的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-738">Make sure that hello value specified in the Name option is an exact match for hello desired request header.</span></span>
- <span data-ttu-id="5ba58-739">案例不會列入 hello 目的標頭用來識別的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ba58-739">Case is not taken into account for hello purpose of identifying a header.</span></span> <span data-ttu-id="5ba58-740">例如，任何下列快取控制標頭名稱變化的 hello 可以使用的 tooidentify 它：</span><span class="sxs-lookup"><span data-stu-id="5ba58-740">For example, any of hello following variations of the Cache-Control header name can be used tooidentify it:</span></span>
    - <span data-ttu-id="5ba58-741">cache-control</span><span class="sxs-lookup"><span data-stu-id="5ba58-741">cache-control</span></span>
    - <span data-ttu-id="5ba58-742">CACHE-CONTROL</span><span class="sxs-lookup"><span data-stu-id="5ba58-742">CACHE-CONTROL</span></span>
    - <span data-ttu-id="5ba58-743">cachE-Control</span><span class="sxs-lookup"><span data-stu-id="5ba58-743">cachE-Control</span></span>
- <span data-ttu-id="5ba58-744">請確定 tooonly 指定標頭名稱時，使用英數字元、 虛線或底線。</span><span class="sxs-lookup"><span data-stu-id="5ba58-744">Make sure tooonly use alphanumeric characters, dashes, or underscores when specifying a header name.</span></span>
- <span data-ttu-id="5ba58-745">刪除標頭讓它從轉遞 tooan 原始伺服器，我們的邊緣伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-745">Deleting a header will prevent it from being forwarded tooan origin server by our edge servers.</span></span>
- <span data-ttu-id="5ba58-746">hello 下列標頭是保留字，無法修改這項功能：</span><span class="sxs-lookup"><span data-stu-id="5ba58-746">hello following headers are reserved and cannot be modified by this feature:</span></span>
    - <span data-ttu-id="5ba58-747">forwarded</span><span class="sxs-lookup"><span data-stu-id="5ba58-747">forwarded</span></span>
    - <span data-ttu-id="5ba58-748">主機</span><span class="sxs-lookup"><span data-stu-id="5ba58-748">host</span></span>
    - <span data-ttu-id="5ba58-749">via</span><span class="sxs-lookup"><span data-stu-id="5ba58-749">via</span></span>
    - <span data-ttu-id="5ba58-750">警告</span><span class="sxs-lookup"><span data-stu-id="5ba58-750">warning</span></span>
    - <span data-ttu-id="5ba58-751">x-forwarded-for</span><span class="sxs-lookup"><span data-stu-id="5ba58-751">x-forwarded-for</span></span>
    - <span data-ttu-id="5ba58-752">以「x-ec」開頭的所有標頭名稱都會保留。</span><span class="sxs-lookup"><span data-stu-id="5ba58-752">All header names that start with "x-ec" are reserved.</span></span>

###<a name="modify-client-response-header"></a><span data-ttu-id="5ba58-753">修改用戶端回應標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-753">Modify Client Response Header</span></span>
<span data-ttu-id="5ba58-754">每個回應都包含一組說明其本身的 [回應標頭]()。</span><span class="sxs-lookup"><span data-stu-id="5ba58-754">Each response contains a set of [response headers]() that describe it.</span></span> <span data-ttu-id="5ba58-755">此功能可以：</span><span class="sxs-lookup"><span data-stu-id="5ba58-755">This feature can either:</span></span>

- <span data-ttu-id="5ba58-756">附加或覆寫 hello 分派 tooa 回應標頭的值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-756">Append or overwrite hello value assigned tooa response header.</span></span> <span data-ttu-id="5ba58-757">如果 hello 指定的要求標頭不存在，然後這項功能會將它加入 toohello 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-757">If hello specified request header does not exist, then this feature will add it toohello response.</span></span>
- <span data-ttu-id="5ba58-758">刪除 hello 回應的回應標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-758">Delete a response header from hello response.</span></span>

<span data-ttu-id="5ba58-759">根據預設，回應標頭值是由原始伺服器和 Edge Server 所定義。</span><span class="sxs-lookup"><span data-stu-id="5ba58-759">By default, response header values are defined by an origin server and by our edge servers.</span></span>

<span data-ttu-id="5ba58-760">回應標頭上，可以執行其中一個 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="5ba58-760">One of hello following actions can be performed on a response header:</span></span>

<span data-ttu-id="5ba58-761">選項</span><span class="sxs-lookup"><span data-stu-id="5ba58-761">Option</span></span>|<span data-ttu-id="5ba58-762">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-762">Description</span></span>|<span data-ttu-id="5ba58-763">範例</span><span class="sxs-lookup"><span data-stu-id="5ba58-763">Example</span></span>
-|-|-
<span data-ttu-id="5ba58-764">Append</span><span class="sxs-lookup"><span data-stu-id="5ba58-764">Append</span></span>|<span data-ttu-id="5ba58-765">hello 指定 hello 現有的要求標頭值的 toend 不會加入值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-765">hello specified value will be added toend of hello existing request header value.</span></span>|<span data-ttu-id="5ba58-766">**回應標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="5ba58-766">**Response header value (Client):**Value1</span></span> <br/> <span data-ttu-id="5ba58-767">**回應標頭值 (HTTP 規則引擎)：**Value2</span><span class="sxs-lookup"><span data-stu-id="5ba58-767">**Response header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="5ba58-768">**新的回應標頭值：**Value1Value2</span><span class="sxs-lookup"><span data-stu-id="5ba58-768">**New Response header value:** Value1Value2</span></span>
<span data-ttu-id="5ba58-769">覆寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-769">Overwrite</span></span>|<span data-ttu-id="5ba58-770">標頭的值會設定 toohello hello 要求指定的值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-770">hello request header value will be set toohello specified value.</span></span>|<span data-ttu-id="5ba58-771">**回應標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="5ba58-771">**Response header value (Client):**Value1</span></span> <br/><span data-ttu-id="5ba58-772">**回應標頭值 (HTTP 規則引擎)：**Value2</span><span class="sxs-lookup"><span data-stu-id="5ba58-772">**Response header value (HTTP Rules Engine):** Value2</span></span> <br/><span data-ttu-id="5ba58-773">**新的回應標頭值：**Value2</span><span class="sxs-lookup"><span data-stu-id="5ba58-773">**New response header value:** Value2</span></span> <br/>
<span data-ttu-id="5ba58-774">刪除</span><span class="sxs-lookup"><span data-stu-id="5ba58-774">Delete</span></span>|<span data-ttu-id="5ba58-775">刪除 hello 指定的要求標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-775">Deletes hello specified request header.</span></span>|<span data-ttu-id="5ba58-776">**要求標頭值 (用戶端)：**Value1</span><span class="sxs-lookup"><span data-stu-id="5ba58-776">**Request header value (Client):** Value1</span></span> <br/> <span data-ttu-id="5ba58-777">**修改用戶端要求標頭設定：**刪除 hello 回應標頭有問題。</span><span class="sxs-lookup"><span data-stu-id="5ba58-777">**Modify Client Request Header configuration:** Delete hello response header in question.</span></span> <br/><span data-ttu-id="5ba58-778">**結果：** hello 指定回應標頭不會轉送 toohello 要求者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-778">**Result:** hello specified response header will not be forwarded toohello requester.</span></span>

<span data-ttu-id="5ba58-779">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-779">Key information:</span></span>

- <span data-ttu-id="5ba58-780">請確定在 [名稱] 選項中指定的 hello 值完全相符的 hello 所需的回應標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-780">Make sure that hello value specified in the Name option is an exact match for hello desired response header.</span></span> 
- <span data-ttu-id="5ba58-781">案例不會列入 hello 目的標頭用來識別的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5ba58-781">Case is not taken into account for hello purpose of identifying a header.</span></span> <span data-ttu-id="5ba58-782">例如，任何下列快取控制標頭名稱變化的 hello 可以使用的 tooidentify 它：</span><span class="sxs-lookup"><span data-stu-id="5ba58-782">For example, any of hello following variations of the Cache-Control header name can be used tooidentify it:</span></span>
    - <span data-ttu-id="5ba58-783">cache-control</span><span class="sxs-lookup"><span data-stu-id="5ba58-783">cache-control</span></span>
    - <span data-ttu-id="5ba58-784">CACHE-CONTROL</span><span class="sxs-lookup"><span data-stu-id="5ba58-784">CACHE-CONTROL</span></span>
    - <span data-ttu-id="5ba58-785">cachE-Control</span><span class="sxs-lookup"><span data-stu-id="5ba58-785">cachE-Control</span></span>
- <span data-ttu-id="5ba58-786">刪除標頭讓它從轉遞 toohello 要求者。</span><span class="sxs-lookup"><span data-stu-id="5ba58-786">Deleting a header will prevent it from being forwarded toohello requester.</span></span>
- <span data-ttu-id="5ba58-787">hello 下列標頭是保留字，無法修改這項功能：</span><span class="sxs-lookup"><span data-stu-id="5ba58-787">hello following headers are reserved and cannot be modified by this feature:</span></span>
    - <span data-ttu-id="5ba58-788">accept-encoding</span><span class="sxs-lookup"><span data-stu-id="5ba58-788">accept-encoding</span></span>
    - <span data-ttu-id="5ba58-789">age</span><span class="sxs-lookup"><span data-stu-id="5ba58-789">age</span></span>
    - <span data-ttu-id="5ba58-790">connection</span><span class="sxs-lookup"><span data-stu-id="5ba58-790">connection</span></span>
    - <span data-ttu-id="5ba58-791">content-encoding</span><span class="sxs-lookup"><span data-stu-id="5ba58-791">content-encoding</span></span>
    - <span data-ttu-id="5ba58-792">content-length</span><span class="sxs-lookup"><span data-stu-id="5ba58-792">content-length</span></span>
    - <span data-ttu-id="5ba58-793">content-range</span><span class="sxs-lookup"><span data-stu-id="5ba58-793">content-range</span></span>
    - <span data-ttu-id="5ba58-794">日期</span><span class="sxs-lookup"><span data-stu-id="5ba58-794">date</span></span>
    - <span data-ttu-id="5ba58-795">伺服器</span><span class="sxs-lookup"><span data-stu-id="5ba58-795">server</span></span>
    - <span data-ttu-id="5ba58-796">trailer</span><span class="sxs-lookup"><span data-stu-id="5ba58-796">trailer</span></span>
    - <span data-ttu-id="5ba58-797">transfer-encoding</span><span class="sxs-lookup"><span data-stu-id="5ba58-797">transfer-encoding</span></span>
    - <span data-ttu-id="5ba58-798">升級</span><span class="sxs-lookup"><span data-stu-id="5ba58-798">upgrade</span></span>
    - <span data-ttu-id="5ba58-799">vary</span><span class="sxs-lookup"><span data-stu-id="5ba58-799">vary</span></span>
    - <span data-ttu-id="5ba58-800">via</span><span class="sxs-lookup"><span data-stu-id="5ba58-800">via</span></span>
    - <span data-ttu-id="5ba58-801">警告</span><span class="sxs-lookup"><span data-stu-id="5ba58-801">warning</span></span>
    - <span data-ttu-id="5ba58-802">以「x-ec」開頭的所有標頭名稱都會保留。</span><span class="sxs-lookup"><span data-stu-id="5ba58-802">All header names that start with "x-ec" are reserved.</span></span>

###<a name="set-client-ip-custom-header"></a><span data-ttu-id="5ba58-803">設定用戶端 IP 自訂標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-803">Set Client IP Custom Header</span></span>
<span data-ttu-id="5ba58-804">**用途：**新增 IP 位址 toohello 要求識別 hello 要求的用戶端的自訂標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-804">**Purpose:** Adds a custom header that identifies hello requesting client by IP address toohello request.</span></span>

<span data-ttu-id="5ba58-805">標頭名稱選項定義 hello hello hello 用戶端的 IP 位址的儲存位置的自訂要求標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-805">The Header name option defines hello name of hello custom request header where hello client's IP address will be stored.</span></span>

<span data-ttu-id="5ba58-806">這項功能可讓客戶透過自訂要求標頭的用戶端 IP 位址時的來源伺服器 toofind。</span><span class="sxs-lookup"><span data-stu-id="5ba58-806">This feature allows a customer origin server toofind out client IP addresses through a custom request header.</span></span> <span data-ttu-id="5ba58-807">如果 hello 要求從快取服務，然後 hello 原始伺服器將不會收到通知的 hello 用戶端的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5ba58-807">If hello request is served from cache, then hello origin server will not be informed of hello client's IP address.</span></span> <span data-ttu-id="5ba58-808">因此，建議將此功能與 ADN 或不會快取的資產搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-808">Therefore, it is recommended that this feature be used with ADN or assets that will not be cached.</span></span>

<span data-ttu-id="5ba58-809">請確定該 hello 指定的標頭名稱不符合 hello 下列任何一項：</span><span class="sxs-lookup"><span data-stu-id="5ba58-809">Please make sure that hello specified header name does not match any of hello following:</span></span>

- <span data-ttu-id="5ba58-810">標準要求標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-810">Standard request header names.</span></span> <span data-ttu-id="5ba58-811">您可以在 [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) 中找到標準標頭名稱清單。</span><span class="sxs-lookup"><span data-stu-id="5ba58-811">A list of standard header names can be found in [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).</span></span>
- <span data-ttu-id="5ba58-812">保留的標頭名稱：</span><span class="sxs-lookup"><span data-stu-id="5ba58-812">Reserved header names:</span></span>
    - <span data-ttu-id="5ba58-813">forwarded-for</span><span class="sxs-lookup"><span data-stu-id="5ba58-813">forwarded-for</span></span>
    - <span data-ttu-id="5ba58-814">主機</span><span class="sxs-lookup"><span data-stu-id="5ba58-814">host</span></span>
    - <span data-ttu-id="5ba58-815">vary</span><span class="sxs-lookup"><span data-stu-id="5ba58-815">vary</span></span>
    - <span data-ttu-id="5ba58-816">via</span><span class="sxs-lookup"><span data-stu-id="5ba58-816">via</span></span>
    - <span data-ttu-id="5ba58-817">警告</span><span class="sxs-lookup"><span data-stu-id="5ba58-817">warning</span></span>
    - <span data-ttu-id="5ba58-818">x-forwarded-for</span><span class="sxs-lookup"><span data-stu-id="5ba58-818">x-forwarded-for</span></span>
    - <span data-ttu-id="5ba58-819">以「x-ec」開頭的所有標頭名稱都會保留。</span><span class="sxs-lookup"><span data-stu-id="5ba58-819">All header names that start with "x-ec" are reserved.</span></span>
 
## <a name="logs"></a><span data-ttu-id="5ba58-820">記錄檔</span><span class="sxs-lookup"><span data-stu-id="5ba58-820">Logs</span></span>

<span data-ttu-id="5ba58-821">這些功能都是設計的 toocustomize hello 資料儲存在原始記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-821">These features are designed toocustomize hello data stored in raw log files.</span></span>

<span data-ttu-id="5ba58-822">名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-822">Name</span></span> | <span data-ttu-id="5ba58-823">目的</span><span class="sxs-lookup"><span data-stu-id="5ba58-823">Purpose</span></span>
-----|--------
<span data-ttu-id="5ba58-824">自訂記錄欄位 1</span><span class="sxs-lookup"><span data-stu-id="5ba58-824">Custom Log Field 1</span></span> | <span data-ttu-id="5ba58-825">決定 hello 格式和 hello 內容將會指派 toohello 原始記錄檔中的自訂記錄欄位。</span><span class="sxs-lookup"><span data-stu-id="5ba58-825">Determines hello format and hello content that will be assigned toohello custom log field in a raw log file.</span></span>
<span data-ttu-id="5ba58-826">記錄查詢字串</span><span class="sxs-lookup"><span data-stu-id="5ba58-826">Log Query String</span></span> | <span data-ttu-id="5ba58-827">決定是否將儲存的查詢字串以及存取記錄檔中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-827">Determines whether a query string will be stored along with hello URL in access logs.</span></span>

###<a name="custom-log-field-1"></a><span data-ttu-id="5ba58-828">自訂記錄欄位 1</span><span class="sxs-lookup"><span data-stu-id="5ba58-828">Custom Log Field 1</span></span>
<span data-ttu-id="5ba58-829">**用途：**決定 hello 格式和 hello 內容將會指派 toohello 原始記錄檔中的自訂記錄欄位。</span><span class="sxs-lookup"><span data-stu-id="5ba58-829">**Purpose:** Determines hello format and hello content that will be assigned toohello custom log field in a raw log file.</span></span>

<span data-ttu-id="5ba58-830">hello 這個自訂欄位背後的主要用途是 tooallow 您 toodetermine 哪些要求和回應標頭值會儲存在記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5ba58-830">hello main purpose behind this custom field is tooallow you toodetermine which request and response header values will be stored in your log files.</span></span>

<span data-ttu-id="5ba58-831">根據預設，hello 自訂記錄檔的欄位稱為 「 x-ec_custom-1"。</span><span class="sxs-lookup"><span data-stu-id="5ba58-831">By default, hello custom log field is called "x-ec_custom-1."</span></span> <span data-ttu-id="5ba58-832">不過，您可以自訂 hello 這個欄位的名稱從[未經處理的記錄檔設定 頁面]()。</span><span class="sxs-lookup"><span data-stu-id="5ba58-832">However, hello name of this field can be customized from the [Raw Log Settings page]().</span></span>

<span data-ttu-id="5ba58-833">hello 格式，您應該使用 toospecify 要求和回應標頭的定義如下。</span><span class="sxs-lookup"><span data-stu-id="5ba58-833">hello formatting that you should use toospecify request and response headers is defined below.</span></span>

<span data-ttu-id="5ba58-834">標頭類型</span><span class="sxs-lookup"><span data-stu-id="5ba58-834">Header Type</span></span>|<span data-ttu-id="5ba58-835">格式</span><span class="sxs-lookup"><span data-stu-id="5ba58-835">Format</span></span>|<span data-ttu-id="5ba58-836">範例</span><span class="sxs-lookup"><span data-stu-id="5ba58-836">Examples</span></span>
-|-|-
<span data-ttu-id="5ba58-837">要求標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-837">Request Header</span></span>|<span data-ttu-id="5ba58-838">%{[RequestHeader]()}[i]()</span><span class="sxs-lookup"><span data-stu-id="5ba58-838">%{[RequestHeader]()}[i]()</span></span> | <span data-ttu-id="5ba58-839">%{Accept-Encoding}i</span><span class="sxs-lookup"><span data-stu-id="5ba58-839">%{Accept-Encoding}i</span></span> <br/> <span data-ttu-id="5ba58-840">{Referer}i</span><span class="sxs-lookup"><span data-stu-id="5ba58-840">{Referer}i</span></span> <br/> <span data-ttu-id="5ba58-841">%{Authorization}i</span><span class="sxs-lookup"><span data-stu-id="5ba58-841">%{Authorization}i</span></span>
<span data-ttu-id="5ba58-842">回應標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-842">Response Header</span></span>|<span data-ttu-id="5ba58-843">%{[ResponseHeader]()}[o]()</span><span class="sxs-lookup"><span data-stu-id="5ba58-843">%{[ResponseHeader]()}[o]()</span></span>| <span data-ttu-id="5ba58-844">%{Age}o</span><span class="sxs-lookup"><span data-stu-id="5ba58-844">%{Age}o</span></span> <br/> <span data-ttu-id="5ba58-845">%{Content-Type}o</span><span class="sxs-lookup"><span data-stu-id="5ba58-845">%{Content-Type}o</span></span> <br/> <span data-ttu-id="5ba58-846">%{Cookie}o</span><span class="sxs-lookup"><span data-stu-id="5ba58-846">%{Cookie}o</span></span>

<span data-ttu-id="5ba58-847">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-847">Key information:</span></span>

- <span data-ttu-id="5ba58-848">自訂記錄欄位可包含標頭欄位和純文字的任意組合。</span><span class="sxs-lookup"><span data-stu-id="5ba58-848">A custom log field can contain any combination of header fields and plain text.</span></span>
- <span data-ttu-id="5ba58-849">這個欄位的有效字元包括 hello 下列： 英數字元 (也就是 0-9、 a 到 z、 和 A-Z)、 連字號、 冒號、 分號、 所有格符號、 逗號、 句號、 底線、 等號、 括號、 方括號和空格。</span><span class="sxs-lookup"><span data-stu-id="5ba58-849">Valid characters for this field include hello following: alphanumeric (i.e., 0-9, a-z, and A-Z), dashes, colons, semi-colons, apostrophes, commas, periods, underscores, equal signs, parentheses, brackets, and spaces.</span></span> <span data-ttu-id="5ba58-850">hello 百分比符號和大括號時，便只允許使用 toospecify 標頭欄位。</span><span class="sxs-lookup"><span data-stu-id="5ba58-850">hello percentage symbol and curly braces are only allowed when used toospecify a header field.</span></span>
- <span data-ttu-id="5ba58-851">每個指定的標頭欄位的 hello 拼字必須符合 hello 所需的要求/回應標頭名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-851">hello spelling for each specified header field must match hello desired request/response header name.</span></span>
- <span data-ttu-id="5ba58-852">如果您想要 toospecify 多個標頭，則建議您使用分隔符號 tooindicate 每個標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-852">If you would like toospecify multiple headers, then it is recommended that you use a separator tooindicate each header.</span></span> <span data-ttu-id="5ba58-853">例如，您可以針對每個標頭使用縮寫。</span><span class="sxs-lookup"><span data-stu-id="5ba58-853">For example, you could use an abbreviation for each header.</span></span> <span data-ttu-id="5ba58-854">範例語法如下所示。</span><span class="sxs-lookup"><span data-stu-id="5ba58-854">Sample syntax is provided below.</span></span>
    - <span data-ttu-id="5ba58-855">AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o</span><span class="sxs-lookup"><span data-stu-id="5ba58-855">AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o</span></span> 

<span data-ttu-id="5ba58-856">**預設值：** -</span><span class="sxs-lookup"><span data-stu-id="5ba58-856">**Default Value:** -</span></span>

###<a name="log-query-string"></a><span data-ttu-id="5ba58-857">記錄查詢字串</span><span class="sxs-lookup"><span data-stu-id="5ba58-857">Log Query String</span></span>
<span data-ttu-id="5ba58-858">**用途：**決定是否要儲存的查詢字串以及存取記錄檔中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-858">**Purpose:** Determines whether a query string will be stored along with hello URL in access logs.</span></span>

<span data-ttu-id="5ba58-859">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-859">Value</span></span>|<span data-ttu-id="5ba58-860">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-860">Result</span></span>
-|-
<span data-ttu-id="5ba58-861">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-861">Enabled</span></span>|<span data-ttu-id="5ba58-862">存取記錄檔中記錄 Url 時，可讓 hello 的查詢字串的儲存體。</span><span class="sxs-lookup"><span data-stu-id="5ba58-862">Allows hello storage of query strings when recording URLs in an access log.</span></span> <span data-ttu-id="5ba58-863">如果 URL 未包含查詢字串，則此選項將不會有任何作用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-863">If a URL does not contain a query string, then this option will not have an effect.</span></span>
<span data-ttu-id="5ba58-864">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-864">Disabled</span></span>|<span data-ttu-id="5ba58-865">還原 hello 預設行為。</span><span class="sxs-lookup"><span data-stu-id="5ba58-865">Restores hello default behavior.</span></span> <span data-ttu-id="5ba58-866">存取記錄檔中記錄 Url 時，hello 預設行為是 tooignore 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="5ba58-866">hello default behavior is tooignore query strings when recording URLs in an access log.</span></span>

<span data-ttu-id="5ba58-867">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-867">**Default Behavior:** Disabled.</span></span>

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a><span data-ttu-id="5ba58-868">來源</span><span class="sxs-lookup"><span data-stu-id="5ba58-868">Origin</span></span>

<span data-ttu-id="5ba58-869">這些功能是設計的 toocontrol hello CDN 與來源伺服器的通訊方式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-869">These features are designed toocontrol how hello CDN communicates with an origin server.</span></span>

<span data-ttu-id="5ba58-870">名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-870">Name</span></span> | <span data-ttu-id="5ba58-871">目的</span><span class="sxs-lookup"><span data-stu-id="5ba58-871">Purpose</span></span>
-----|--------
<span data-ttu-id="5ba58-872">Keep-Alive 要求的最大值</span><span class="sxs-lookup"><span data-stu-id="5ba58-872">Maximum Keep-Alive Requests</span></span> | <span data-ttu-id="5ba58-873">它已關閉之前，請定義 hello 保持連線的要求數目上限。</span><span class="sxs-lookup"><span data-stu-id="5ba58-873">Defines hello maximum number of requests for a Keep-Alive connection before it is closed.</span></span>
<span data-ttu-id="5ba58-874">Proxy 特定的標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-874">Proxy Special Headers</span></span> | <span data-ttu-id="5ba58-875">定義 hello 組會從邊緣伺服器 tooan 原始伺服器轉送的 CDN 專屬要求標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-875">Defines hello set of CDN-specific request headers that will be forwarded from an edge server tooan origin server.</span></span>


###<a name="maximum-keep-alive-requests"></a><span data-ttu-id="5ba58-876">Keep-Alive 要求的最大值</span><span class="sxs-lookup"><span data-stu-id="5ba58-876">Maximum Keep-Alive Requests</span></span>
<span data-ttu-id="5ba58-877">**用途：**定義 hello 保持連線的要求數目上限之前它已關閉。</span><span class="sxs-lookup"><span data-stu-id="5ba58-877">**Purpose:** Defines hello maximum number of requests for a Keep-Alive connection before it is closed.</span></span>

<span data-ttu-id="5ba58-878">強烈建議您不要設定 hello tooa 低值時，要求的數目上限，並可能導致效能變差。</span><span class="sxs-lookup"><span data-stu-id="5ba58-878">Setting hello maximum number of requests tooa low value is strongly discouraged and may result in performance degradation.</span></span>

<span data-ttu-id="5ba58-879">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-879">Key information:</span></span>

- <span data-ttu-id="5ba58-880">將此值指定為整數。</span><span class="sxs-lookup"><span data-stu-id="5ba58-880">Specify this value as a whole integer.</span></span>
- <span data-ttu-id="5ba58-881">不包含逗號或句號中指定的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-881">Do not include commas or periods in hello specified value.</span></span>

<span data-ttu-id="5ba58-882">**預設值︰**10,000 個要求</span><span class="sxs-lookup"><span data-stu-id="5ba58-882">**Default Value:** 10,000 requests</span></span>

###<a name="proxy-special-headers"></a><span data-ttu-id="5ba58-883">Proxy 特定的標頭</span><span class="sxs-lookup"><span data-stu-id="5ba58-883">Proxy Special Headers</span></span>
<span data-ttu-id="5ba58-884">**用途：**定義 hello 組[CDN 特定要求標頭]()，將會轉送從 edge server tooan 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-884">**Purpose:** Defines hello set of [CDN-specific request headers]() that will be forwarded from an edge server tooan origin server.</span></span>

<span data-ttu-id="5ba58-885">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-885">Key information:</span></span>

- <span data-ttu-id="5ba58-886">這項功能中定義的每個 CDN 專屬要求標頭會轉送 tooan 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-886">Each CDN-specific request header defined in this feature will be forwarded tooan origin server.</span></span>
- <span data-ttu-id="5ba58-887">防止 CDN 專屬的要求標頭，藉由移除此清單從轉遞 tooan 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-887">Prevent a CDN-specific request header from being forwarded tooan origin server by removing it from this list.</span></span>

<span data-ttu-id="5ba58-888">**預設行為：**所有[CDN 特定要求標頭]()轉送 toohello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ba58-888">**Default Behavior:** All [CDN-specific request headers]() will be forwarded toohello origin server.</span></span>

## <a name="specialty"></a><span data-ttu-id="5ba58-889">特殊性</span><span class="sxs-lookup"><span data-stu-id="5ba58-889">Specialty</span></span>

<span data-ttu-id="5ba58-890">這些功能提供的進階功能僅可供進階使用者使用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-890">These features provide advanced functionality that should only be used by advanced users.</span></span>

<span data-ttu-id="5ba58-891">名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-891">Name</span></span> | <span data-ttu-id="5ba58-892">目的</span><span class="sxs-lookup"><span data-stu-id="5ba58-892">Purpose</span></span>
-----|--------
<span data-ttu-id="5ba58-893">可快取的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="5ba58-893">Cacheable HTTP Methods</span></span> | <span data-ttu-id="5ba58-894">決定 hello 組可以快取在我們的網路的其他 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="5ba58-894">Determines hello set of additional HTTP methods that can be cached on our network.</span></span>
<span data-ttu-id="5ba58-895">可快取的要求主體大小</span><span class="sxs-lookup"><span data-stu-id="5ba58-895">Cacheable Request Body Size</span></span> | <span data-ttu-id="5ba58-896">定義判斷是否可以快取 POST 回應 hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-896">Defines hello threshold for determining whether a POST response can be cached.</span></span>

###<a name="cacheable-http-methods"></a><span data-ttu-id="5ba58-897">可快取的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="5ba58-897">Cacheable HTTP Methods</span></span>
<span data-ttu-id="5ba58-898">**用途：**決定 hello 組可以快取在我們的網路的其他 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="5ba58-898">**Purpose:** Determines hello set of additional HTTP methods that can be cached on our network.</span></span>

<span data-ttu-id="5ba58-899">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-899">Key information:</span></span>

- <span data-ttu-id="5ba58-900">此功能假設應一律快取 GET 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-900">This feature assumes that GET responses should always be cached.</span></span> <span data-ttu-id="5ba58-901">如此一來，hello GET HTTP 方法應該不會包含設定這項功能時。</span><span class="sxs-lookup"><span data-stu-id="5ba58-901">As a result, hello GET HTTP method should not be included when setting this feature.</span></span>
- <span data-ttu-id="5ba58-902">這項功能僅支援 hello POST HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="5ba58-902">This feature only supports hello POST HTTP method.</span></span> <span data-ttu-id="5ba58-903">將此功能設定為：POST，藉以啟用 POST 回應快取</span><span class="sxs-lookup"><span data-stu-id="5ba58-903">Enable POST response caching by setting this feature to:POST</span></span> 
- <span data-ttu-id="5ba58-904">根據預設，只會快取主體小於 14 Kb 的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-904">By default, only requests whose body is smaller than 14 Kb will be cached.</span></span> <span data-ttu-id="5ba58-905">您可以使用可快取的要求主體大小功能來設定 hello 要求主體大小上限。</span><span class="sxs-lookup"><span data-stu-id="5ba58-905">Use the Cacheable Request Body Size Feature to set hello maximum request body size.</span></span>

<span data-ttu-id="5ba58-906">**預設行為︰**只會快取 GET 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-906">**Default Behavior:** Only GET responses will be cached.</span></span>

###<a name="cacheable-request-body-size"></a><span data-ttu-id="5ba58-907">可快取的要求主體大小</span><span class="sxs-lookup"><span data-stu-id="5ba58-907">Cacheable Request Body Size</span></span>

<span data-ttu-id="5ba58-908">**用途：**定義 hello 臨界值，以判斷是否可以快取 POST 回應。</span><span class="sxs-lookup"><span data-stu-id="5ba58-908">**Purpose:** Defines hello threshold for determining whether a POST response can be cached.</span></span>

<span data-ttu-id="5ba58-909">此臨界值是藉由指定要求主體大小上限來決定。</span><span class="sxs-lookup"><span data-stu-id="5ba58-909">This threshold is determined by specifying a maximum request body size.</span></span> <span data-ttu-id="5ba58-910">系統將不會快取包含較大要求主體的要求。</span><span class="sxs-lookup"><span data-stu-id="5ba58-910">Requests that contain a larger request body will not be cached.</span></span>

<span data-ttu-id="5ba58-911">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-911">Key information:</span></span>

- <span data-ttu-id="5ba58-912">只有在 POST 回應適合用來快取時，才適用此功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-912">This Feature is only applicable when POST responses are eligible for caching.</span></span> <span data-ttu-id="5ba58-913">若要啟用 POST 要求快取使用 hello 可快取 HTTP 方法的功能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-913">Use hello Cacheable HTTP Methods Feature to enable POST request caching.</span></span>
- <span data-ttu-id="5ba58-914">hello 要求主體會列入考量：</span><span class="sxs-lookup"><span data-stu-id="5ba58-914">hello request body is taken into consideration for:</span></span>
    - <span data-ttu-id="5ba58-915">x-www-form-urlencoded 值</span><span class="sxs-lookup"><span data-stu-id="5ba58-915">x-www-form-urlencoded values</span></span>
    - <span data-ttu-id="5ba58-916">確保唯一的快取索引鍵</span><span class="sxs-lookup"><span data-stu-id="5ba58-916">Ensuring a unique cache-key</span></span>
- <span data-ttu-id="5ba58-917">定義大型的要求主體大小上限可能會影響資料傳遞效能。</span><span class="sxs-lookup"><span data-stu-id="5ba58-917">Defining a large maximum request body size may impact data delivery performance.</span></span>
    - <span data-ttu-id="5ba58-918">**建議值：**14 Kb</span><span class="sxs-lookup"><span data-stu-id="5ba58-918">**Recommended Value:** 14 Kb</span></span>
    - <span data-ttu-id="5ba58-919">**最小值︰**1 Kb</span><span class="sxs-lookup"><span data-stu-id="5ba58-919">**Minimum Value:** 1 Kb</span></span>

<span data-ttu-id="5ba58-920">**預設行為︰**14 Kb</span><span class="sxs-lookup"><span data-stu-id="5ba58-920">**Default Behavior:** 14 Kb</span></span>
 
## <a name="url"></a><span data-ttu-id="5ba58-921">URL</span><span class="sxs-lookup"><span data-stu-id="5ba58-921">URL</span></span>

<span data-ttu-id="5ba58-922">這些功能可讓要求 toobe 重新導向，或重寫 tooa 不同的 URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-922">These features allow a request toobe redirected or rewritten tooa different URL.</span></span>

<span data-ttu-id="5ba58-923">名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-923">Name</span></span> | <span data-ttu-id="5ba58-924">目的</span><span class="sxs-lookup"><span data-stu-id="5ba58-924">Purpose</span></span>
-----|--------
<span data-ttu-id="5ba58-925">遵循重新導向</span><span class="sxs-lookup"><span data-stu-id="5ba58-925">Follow Redirects</span></span> | <span data-ttu-id="5ba58-926">判斷要求是否可以在 hello 客戶原始伺服器所傳回的位置標頭中定義的重新導向的 toohello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-926">Determines whether requests can be redirected toohello hostname defined in hello Location header returned by a customer origin server.</span></span>
<span data-ttu-id="5ba58-927">[URL 重新導向]</span><span class="sxs-lookup"><span data-stu-id="5ba58-927">URL Redirect</span></span> | <span data-ttu-id="5ba58-928">將要求重新導向透過 hello 位置標頭。</span><span class="sxs-lookup"><span data-stu-id="5ba58-928">Redirects requests via hello Location header.</span></span>
<span data-ttu-id="5ba58-929">URL 重寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-929">URL Rewrite</span></span>  | <span data-ttu-id="5ba58-930">重寫 hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-930">Rewrites hello request URL.</span></span>

###<a name="follow-redirects"></a><span data-ttu-id="5ba58-931">遵循重新導向</span><span class="sxs-lookup"><span data-stu-id="5ba58-931">Follow Redirects</span></span>
<span data-ttu-id="5ba58-932">**用途：**決定要求是否可為客戶原始伺服器所傳回之位置標頭中定義的重新導向的 toohello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-932">**Purpose:** Determines whether requests can be redirected toohello hostname defined in the Location header returned by a customer origin server.</span></span>

<span data-ttu-id="5ba58-933">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-933">Key information:</span></span>

- <span data-ttu-id="5ba58-934">要求只能重新導向的 tooedge Cname 對應 toohello 相同的平台。</span><span class="sxs-lookup"><span data-stu-id="5ba58-934">Requests can only be redirected tooedge CNAMEs that correspond toohello same platform.</span></span>

<span data-ttu-id="5ba58-935">值</span><span class="sxs-lookup"><span data-stu-id="5ba58-935">Value</span></span>|<span data-ttu-id="5ba58-936">結果</span><span class="sxs-lookup"><span data-stu-id="5ba58-936">Result</span></span>
-|-
<span data-ttu-id="5ba58-937">已啟用</span><span class="sxs-lookup"><span data-stu-id="5ba58-937">Enabled</span></span>|<span data-ttu-id="5ba58-938">要求可重新導向。</span><span class="sxs-lookup"><span data-stu-id="5ba58-938">Requests can be redirected.</span></span>
<span data-ttu-id="5ba58-939">已停用</span><span class="sxs-lookup"><span data-stu-id="5ba58-939">Disabled</span></span>|<span data-ttu-id="5ba58-940">要求將不會重新導向。</span><span class="sxs-lookup"><span data-stu-id="5ba58-940">Requests will not be redirected.</span></span>

<span data-ttu-id="5ba58-941">**預設行為：**已停用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-941">**Default Behavior:** Disabled.</span></span>
###<a name="url-redirect"></a><span data-ttu-id="5ba58-942">[URL 重新導向]</span><span class="sxs-lookup"><span data-stu-id="5ba58-942">URL Redirect</span></span>
<span data-ttu-id="5ba58-943">**目的：**透過位置標頭來將要求重新導向。</span><span class="sxs-lookup"><span data-stu-id="5ba58-943">**Purpose:** Redirects requests via the Location header.</span></span>

<span data-ttu-id="5ba58-944">這項功能的 hello 組態設定需要設定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-944">hello configuration of this feature requires setting hello following options:</span></span>

<span data-ttu-id="5ba58-945">選項</span><span class="sxs-lookup"><span data-stu-id="5ba58-945">Option</span></span>|<span data-ttu-id="5ba58-946">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-946">Description</span></span>
-|-
<span data-ttu-id="5ba58-947">代碼</span><span class="sxs-lookup"><span data-stu-id="5ba58-947">Code</span></span>|<span data-ttu-id="5ba58-948">選取將會傳回 toohello 要求者的 hello 回應程式碼。</span><span class="sxs-lookup"><span data-stu-id="5ba58-948">Select hello response code that will be returned toohello requester.</span></span>
<span data-ttu-id="5ba58-949">來源與模式</span><span class="sxs-lookup"><span data-stu-id="5ba58-949">Source & Pattern</span></span>| <span data-ttu-id="5ba58-950">這些設定定義識別 hello 可能會重新導向的要求類型的要求 URI 模式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-950">These settings define a request URI pattern that identifies hello type of requests that may be redirected.</span></span> <span data-ttu-id="5ba58-951">只有其 URL 符合這兩個 hello 下列準則的要求會被重新導向：</span><span class="sxs-lookup"><span data-stu-id="5ba58-951">Only requests whose URL satisfies both of hello following criteria will be redirected:</span></span> <br/> <br/> <span data-ttu-id="5ba58-952">**來源︰**(或內容存取點) 選取識別原始伺服器的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="5ba58-952">**Source :** (or content access point) Select a relative path that identifies an origin server.</span></span> <span data-ttu-id="5ba58-953">這是 hello"/XXXX/ 」 一節和端點名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-953">This is hello  "/XXXX/" section and your endpoint name.</span></span> <br/> <span data-ttu-id="5ba58-954">**來源 (模式)︰**必須定義依相對路徑識別要求的模式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-954">**Source (pattern):** A pattern that identifies requests by relative path must be defined.</span></span> <span data-ttu-id="5ba58-955">這個規則運算式模式必須定義會直接啟動 hello 先前選取的內容存取點 （如上述） 之後的路徑。</span><span class="sxs-lookup"><span data-stu-id="5ba58-955">This regular expression pattern must define a path that starts directly after hello previously selected content access point (see above).</span></span> <br/> <span data-ttu-id="5ba58-956">-請確定上述定義 hello 要求 URI 準則 （亦即，來源和模式） 不定義這項功能的任何比對條件相衝突。</span><span class="sxs-lookup"><span data-stu-id="5ba58-956">- Make sure that hello request URI criteria (i.e., Source & Pattern) defined above doesn't conflict with any match conditions defined for this feature.</span></span> <br/> <span data-ttu-id="5ba58-957">-請確定 toospecify 模式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-957">- Make sure toospecify a pattern.</span></span> <span data-ttu-id="5ba58-958">使用空白的值為 hello 模式只會符合 hello 選取的來源伺服器 (例如 http://cdn.mydomain.com/) 要求 toohello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="5ba58-958">Using a blank value as hello pattern will only match requests toohello root folder of hello selected origin server (e.g., http://cdn.mydomain.com/).</span></span>
<span data-ttu-id="5ba58-959">目的地</span><span class="sxs-lookup"><span data-stu-id="5ba58-959">Destination</span></span>| <span data-ttu-id="5ba58-960">定義 hello URL toowhich hello 上方要求會被重新導向。</span><span class="sxs-lookup"><span data-stu-id="5ba58-960">Define hello URL toowhich hello above requests will be redirected.</span></span> <br/> <span data-ttu-id="5ba58-961">使用下列方式來動態建構此 URL：</span><span class="sxs-lookup"><span data-stu-id="5ba58-961">Dynamically construct this URL using:</span></span> <br/> <span data-ttu-id="5ba58-962">- 規則運算式模式</span><span class="sxs-lookup"><span data-stu-id="5ba58-962">- A regular expression pattern</span></span> <br/><span data-ttu-id="5ba58-963">- HTTP 變數</span><span class="sxs-lookup"><span data-stu-id="5ba58-963">- HTTP variables</span></span> <br/> <span data-ttu-id="5ba58-964">替換圖樣 hello 目的地使用 $ 擷取 hello 來源模式中的 hello 值_n_ 其中 _n_  hello 順序它擷取識別值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-964">Substitute hello values captured in hello source pattern into hello destination pattern using $_n_ where _n_ identifies a value by hello order in which it was captured.</span></span> <span data-ttu-id="5ba58-965">例如，$1 代表 hello hello 來源模式，而 $2 代表 hello 第二個值所擷取的第一個值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-965">For example, $1 represents hello first value captured in hello source pattern, while $2 represents hello second value.</span></span> <br/> 
<span data-ttu-id="5ba58-966">它強烈建議 toouse 絕對 URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-966">It is highly recommended toouse an absolute URL.</span></span> <span data-ttu-id="5ba58-967">hello 使用相對的 URL 可能會重新導向 CDN Url tooan 無效的路徑。</span><span class="sxs-lookup"><span data-stu-id="5ba58-967">hello use of a relative URL may redirect CDN URLs tooan invalid path.</span></span>

<span data-ttu-id="5ba58-968">**範例案例**</span><span class="sxs-lookup"><span data-stu-id="5ba58-968">**Sample Scenario**</span></span>

<span data-ttu-id="5ba58-969">在此範例中，我們將示範如何 tooredirect 邊緣解析 toothis CNAME URL 基底 CDN URL: http://marketing.azureedge.net/brochures</span><span class="sxs-lookup"><span data-stu-id="5ba58-969">In this example, we will demonstrate how tooredirect an edge CNAME URL that resolves toothis base CDN URL: http://marketing.azureedge.net/brochures</span></span>

<span data-ttu-id="5ba58-970">限定要求將會是基底邊緣 CNAME 的 URL 重新導向的 toothis: http://cdn.mydomain.com/resources</span><span class="sxs-lookup"><span data-stu-id="5ba58-970">Qualifying requests will be redirected toothis base edge CNAME URL: http://cdn.mydomain.com/resources</span></span>

<span data-ttu-id="5ba58-971">此 URL 重新導向可能透過 hello 下列組態來完成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)</span><span class="sxs-lookup"><span data-stu-id="5ba58-971">This URL redirection may be achieved through hello following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)</span></span>

<span data-ttu-id="5ba58-972">**重點︰**</span><span class="sxs-lookup"><span data-stu-id="5ba58-972">**Key points:**</span></span>

- <span data-ttu-id="5ba58-973">hello URL 重新導向功能可定義 hello 要求會被重新導向的 Url。</span><span class="sxs-lookup"><span data-stu-id="5ba58-973">hello URL Redirect feature defines hello request URLs that will be redirected.</span></span> <span data-ttu-id="5ba58-974">如此一來，就不需要額外的比對條件。</span><span class="sxs-lookup"><span data-stu-id="5ba58-974">As a result, additional match conditions are not required.</span></span> <span data-ttu-id="5ba58-975">雖然 hello 比對條件定義為 「 永遠 」，只會要求該點 toohello"冊"hello"marketing"客戶來源上的資料夾會被重新導向。</span><span class="sxs-lookup"><span data-stu-id="5ba58-975">Although hello match condition was defined as "Always," only requests that point toohello "brochures" folder on hello "marketing" customer origin will be redirected.</span></span> 
- <span data-ttu-id="5ba58-976">所有相符的要求將會定義目的地選項中的 CNAME 的 URL 重新導向的 toohello 邊緣。</span><span class="sxs-lookup"><span data-stu-id="5ba58-976">All matching requests will be redirected toohello edge CNAME URL defined in the Destination option.</span></span> 
    - <span data-ttu-id="5ba58-977">範例案例 1：</span><span class="sxs-lookup"><span data-stu-id="5ba58-977">Sample scenario #1:</span></span> 
        - <span data-ttu-id="5ba58-978">範例要求 (CDN URL)：http://marketing.azureedge.net/brochures/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="5ba58-978">Sample request (CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf</span></span> 
        - <span data-ttu-id="5ba58-979">要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="5ba58-979">Request URL (after redirect): http://cdn.mydomain.com/resources/widgets.pdf</span></span>  
    - <span data-ttu-id="5ba58-980">範例案例 2：</span><span class="sxs-lookup"><span data-stu-id="5ba58-980">Sample scenario #2:</span></span> 
        - <span data-ttu-id="5ba58-981">範例要求 (Edge CNAME URL)：http://marketing.mydomain.com/brochures/widgets.pdf</span><span class="sxs-lookup"><span data-stu-id="5ba58-981">Sample request (Edge CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf</span></span> 
        - <span data-ttu-id="5ba58-982">要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/widgets.pdf 範例案例</span><span class="sxs-lookup"><span data-stu-id="5ba58-982">Request URL (after redirect): http://cdn.mydomain.com/resources/widgets.pdf  Sample scenario</span></span>
    - <span data-ttu-id="5ba58-983">範例案例 3：</span><span class="sxs-lookup"><span data-stu-id="5ba58-983">Sample scenario #3:</span></span> 
        - <span data-ttu-id="5ba58-984">範例要求 (Edge CNAME URL)：http://brochures.mydomain.com/campaignA/final/productC.ppt</span><span class="sxs-lookup"><span data-stu-id="5ba58-984">Sample request (Edge CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt</span></span> 
        - <span data-ttu-id="5ba58-985">要求 URL (重新導向之後)：http://cdn.mydomain.com/resources/campaignA/final/productC.ppt</span><span class="sxs-lookup"><span data-stu-id="5ba58-985">Request URL (after redirect): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt</span></span>  
- <span data-ttu-id="5ba58-986">hello 要求配置 （%{配置}） 的變數已在目的地選項可用。</span><span class="sxs-lookup"><span data-stu-id="5ba58-986">hello Request Scheme (%{scheme}) variable was leveraged in the Destination option.</span></span> <span data-ttu-id="5ba58-987">這可確保該 hello 要求的配置會重新導向之後維持不變。</span><span class="sxs-lookup"><span data-stu-id="5ba58-987">This ensures that hello request's scheme remains unchanged after redirection.</span></span>
- <span data-ttu-id="5ba58-988">hello hello 要求中所擷取的 URL 區段是附加的 toohello"$1"。 透過新的 URL</span><span class="sxs-lookup"><span data-stu-id="5ba58-988">hello URL segments that were captured from hello request are appended toohello new URL via "$1."</span></span>
 
###<a name="url-rewrite"></a><span data-ttu-id="5ba58-989">URL 重寫</span><span class="sxs-lookup"><span data-stu-id="5ba58-989">URL Rewrite</span></span>
<span data-ttu-id="5ba58-990">**用途：**重寫 hello 要求 URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-990">**Purpose:** Rewrites hello request URL.</span></span>

<span data-ttu-id="5ba58-991">重要資訊：</span><span class="sxs-lookup"><span data-stu-id="5ba58-991">Key information:</span></span>

- <span data-ttu-id="5ba58-992">這項功能的 hello 組態設定需要設定下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-992">hello configuration of this feature requires setting hello following options:</span></span>

<span data-ttu-id="5ba58-993">選項</span><span class="sxs-lookup"><span data-stu-id="5ba58-993">Option</span></span>|<span data-ttu-id="5ba58-994">說明</span><span class="sxs-lookup"><span data-stu-id="5ba58-994">Description</span></span>
-|-
 <span data-ttu-id="5ba58-995">來源與模式</span><span class="sxs-lookup"><span data-stu-id="5ba58-995">Source & Pattern</span></span> | <span data-ttu-id="5ba58-996">這些設定定義識別 hello 可能重寫的要求類型的要求 URI 模式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-996">These settings define a request URI pattern that identifies hello type of requests that may be rewritten.</span></span> <span data-ttu-id="5ba58-997">只有其 URL 符合這兩個 hello 下列準則的要求將會重新寫入：</span><span class="sxs-lookup"><span data-stu-id="5ba58-997">Only requests whose URL satisfies both of hello following criteria will be rewritten:</span></span> <br/>     <span data-ttu-id="5ba58-998">- **來源 (或內容存取點)：**選取識別原始伺服器的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="5ba58-998">- **Source (or content access point):** Select a relative path that identifies an origin server.</span></span> <span data-ttu-id="5ba58-999">這是 hello"/XXXX/ 」 一節和端點名稱。</span><span class="sxs-lookup"><span data-stu-id="5ba58-999">This is hello  "/XXXX/" section and your endpoint name.</span></span> <br/> <span data-ttu-id="5ba58-1000">- **來源 (模式)︰**必須定義依相對路徑識別要求的模式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1000">- **Source (pattern):** A pattern that identifies requests by relative path must be defined.</span></span> <span data-ttu-id="5ba58-1001">這個規則運算式模式必須定義會直接啟動 hello 先前選取的內容存取點 （如上述） 之後的路徑。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1001">This regular expression pattern must define a path that starts directly after hello previously selected content access point (see above).</span></span> <br/> <span data-ttu-id="5ba58-1002">請確定 hello 要求 URI （亦即，來源和模式） 所定義準則上面沒有與這項功能所定義的 hello 符合任何的條件衝突。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1002">Make sure that hello request URI criteria (i.e., Source & Pattern) defined above doesn't conflict with any of hello match conditions defined for this feature.</span></span> <span data-ttu-id="5ba58-1003">請確定 toospecify 模式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1003">Make sure toospecify a pattern.</span></span> <span data-ttu-id="5ba58-1004">使用空白的值為 hello 模式只會符合 hello 選取的來源伺服器 (例如 http://cdn.mydomain.com/) 要求 toohello 根資料夾。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1004">Using a blank value as hello pattern will only match requests toohello root folder of hello selected origin server (e.g., http://cdn.mydomain.com/).</span></span> 
 <span data-ttu-id="5ba58-1005">目的地</span><span class="sxs-lookup"><span data-stu-id="5ba58-1005">Destination</span></span>  |<span data-ttu-id="5ba58-1006">定義 hello 相對 URL 將來重新撰寫上面要求 toowhich hello:</span><span class="sxs-lookup"><span data-stu-id="5ba58-1006">Define hello relative URL toowhich hello above requests will be rewritten by:</span></span> <br/>    <span data-ttu-id="5ba58-1007">1.選取可識別原始伺服器的內容存取點。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1007">1. Selecting a content access point that identifies an origin server.</span></span> <br/>    <span data-ttu-id="5ba58-1008">2.使用下列方式來定義相對路徑：</span><span class="sxs-lookup"><span data-stu-id="5ba58-1008">2. Defining a relative path using:</span></span> <br/>        <span data-ttu-id="5ba58-1009">- 規則運算式模式</span><span class="sxs-lookup"><span data-stu-id="5ba58-1009">- A regular expression pattern</span></span> <br/>        <span data-ttu-id="5ba58-1010">- HTTP 變數</span><span class="sxs-lookup"><span data-stu-id="5ba58-1010">- HTTP variables</span></span> <br/> <br/> <span data-ttu-id="5ba58-1011">替換圖樣 hello 目的地使用 $ 擷取 hello 來源模式中的 hello 值_n_ 其中 _n_  hello 順序它擷取識別值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1011">Substitute hello values captured in hello source pattern into hello destination pattern using $_n_ where _n_ identifies a value by hello order in which it was captured.</span></span> <span data-ttu-id="5ba58-1012">例如，$1 代表 hello hello 來源模式，而 $2 代表 hello 第二個值所擷取的第一個值。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1012">For example, $1 represents hello first value captured in hello source pattern, while $2 represents hello second value.</span></span> 
 <span data-ttu-id="5ba58-1013">這項功能可讓我們的邊緣伺服器 toorewrite hello URL 而不需執行傳統的重新導向。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1013">This feature allows our edge servers toorewrite hello URL without performing a traditional redirect.</span></span> <span data-ttu-id="5ba58-1014">這表示該 hello 要求者會收到的 hello 相同的回應程式碼，因為如果有要求 hello 重寫 URL。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1014">This means that hello requester will receive hello same response code as if hello rewritten URL had been requested.</span></span>

<span data-ttu-id="5ba58-1015">**範例案例 1**</span><span class="sxs-lookup"><span data-stu-id="5ba58-1015">**Sample Scenario 1**</span></span>

<span data-ttu-id="5ba58-1016">在此範例中，我們將示範如何 tooredirect 邊緣解析 toothis CNAME URL 基底 CDN URL: http://marketing.azureedge.net/brochures/</span><span class="sxs-lookup"><span data-stu-id="5ba58-1016">In this example, we will demonstrate how tooredirect an edge CNAME URL that resolves toothis base CDN URL: http://marketing.azureedge.net/brochures/</span></span>

<span data-ttu-id="5ba58-1017">限定要求將會是基底邊緣 CNAME 的 URL 重新導向的 toothis: http://MyOrigin.azureedge.net/resources/</span><span class="sxs-lookup"><span data-stu-id="5ba58-1017">Qualifying requests will be redirected toothis base edge CNAME URL: http://MyOrigin.azureedge.net/resources/</span></span>

<span data-ttu-id="5ba58-1018">此 URL 重新導向可能透過 hello 下列組態來完成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)</span><span class="sxs-lookup"><span data-stu-id="5ba58-1018">This URL redirection may be achieved through hello following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)</span></span>

<span data-ttu-id="5ba58-1019">**範例案例 2**</span><span class="sxs-lookup"><span data-stu-id="5ba58-1019">**Sample Scenario 2**</span></span>

<span data-ttu-id="5ba58-1020">在此範例中，我們將示範如何 tooredirect 邊緣 CNAME URL 從大寫 toolowercase 使用規則運算式。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1020">In this example, we will demonstrate how tooredirect an edge CNAME URL from UPPERCASE toolowercase using regular expressions.</span></span>

<span data-ttu-id="5ba58-1021">此 URL 重新導向可能透過 hello 下列組態來完成：![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)</span><span class="sxs-lookup"><span data-stu-id="5ba58-1021">This URL redirection may be achieved through hello following configuration: ![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)</span></span>


<span data-ttu-id="5ba58-1022">**重點︰**</span><span class="sxs-lookup"><span data-stu-id="5ba58-1022">**Key points:**</span></span>

- <span data-ttu-id="5ba58-1023">hello URL 重寫功能可定義 hello 要求將會重寫的 Url。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1023">hello URL Rewrite feature defines hello request URLs that will be rewritten.</span></span> <span data-ttu-id="5ba58-1024">如此一來，就不需要額外的比對條件。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1024">As a result, additional match conditions are not required.</span></span> <span data-ttu-id="5ba58-1025">雖然 hello 比對條件定義為 「 永遠 」，只會要求該點 toohello"冊"hello"marketing"客戶來源上的資料夾將會重新寫入。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1025">Although hello match condition was defined as "Always," only requests that point toohello "brochures" folder on hello "marketing" customer origin will be rewritten.</span></span>

- <span data-ttu-id="5ba58-1026">hello hello 要求中所擷取的 URL 區段是附加的 toohello"$1"。 透過新的 URL</span><span class="sxs-lookup"><span data-stu-id="5ba58-1026">hello URL segments that were captured from hello request are appended toohello new URL via "$1."</span></span>



###<a name="compatibility"></a><span data-ttu-id="5ba58-1027">相容性</span><span class="sxs-lookup"><span data-stu-id="5ba58-1027">Compatibility</span></span>

<span data-ttu-id="5ba58-1028">這項功能，包括它可以套用的 tooa 要求之前，必須符合的準則相符的。</span><span class="sxs-lookup"><span data-stu-id="5ba58-1028">This feature includes matching criteria that must be met before it can be applied tooa request.</span></span> <span data-ttu-id="5ba58-1029">順序 tooprevent 設定衝突的比對準則，這項功能是與 hello 下列比對條件不相容：</span><span class="sxs-lookup"><span data-stu-id="5ba58-1029">In order tooprevent setting up conflicting match criteria, this feature is incompatible with hello following match conditions:</span></span>

- <span data-ttu-id="5ba58-1030">AS 號碼</span><span class="sxs-lookup"><span data-stu-id="5ba58-1030">AS Number</span></span>
- <span data-ttu-id="5ba58-1031">CDN 原點</span><span class="sxs-lookup"><span data-stu-id="5ba58-1031">CDN Origin</span></span>
- <span data-ttu-id="5ba58-1032">用戶端 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5ba58-1032">Client IP Address</span></span>
- <span data-ttu-id="5ba58-1033">客戶原點</span><span class="sxs-lookup"><span data-stu-id="5ba58-1033">Customer Origin</span></span>
- <span data-ttu-id="5ba58-1034">要求配置</span><span class="sxs-lookup"><span data-stu-id="5ba58-1034">Request Scheme</span></span>
- <span data-ttu-id="5ba58-1035">URL 路徑目錄</span><span class="sxs-lookup"><span data-stu-id="5ba58-1035">URL Path Directory</span></span>
- <span data-ttu-id="5ba58-1036">URL 路徑的副檔名</span><span class="sxs-lookup"><span data-stu-id="5ba58-1036">URL Path Extension</span></span>
- <span data-ttu-id="5ba58-1037">URL 路徑的檔案名稱</span><span class="sxs-lookup"><span data-stu-id="5ba58-1037">URL Path Filename</span></span>
- <span data-ttu-id="5ba58-1038">URL 路徑常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-1038">URL Path Literal</span></span>
- <span data-ttu-id="5ba58-1039">URL 路徑 Regex</span><span class="sxs-lookup"><span data-stu-id="5ba58-1039">URL Path Regex</span></span>
- <span data-ttu-id="5ba58-1040">URL 路徑萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-1040">URL Path Wildcard</span></span>
- <span data-ttu-id="5ba58-1041">URL 查詢常值</span><span class="sxs-lookup"><span data-stu-id="5ba58-1041">URL Query Literal</span></span>
- <span data-ttu-id="5ba58-1042">URL 查詢參數</span><span class="sxs-lookup"><span data-stu-id="5ba58-1042">URL Query Parameter</span></span>
- <span data-ttu-id="5ba58-1043">URL 查詢 Regex</span><span class="sxs-lookup"><span data-stu-id="5ba58-1043">URL Query Regex</span></span>
- <span data-ttu-id="5ba58-1044">URL 查詢萬用字元</span><span class="sxs-lookup"><span data-stu-id="5ba58-1044">URL Query Wildcard</span></span>


## <a name="next-steps"></a><span data-ttu-id="5ba58-1045">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ba58-1045">Next Steps</span></span>
* [<span data-ttu-id="5ba58-1046">規則引擎參考 (英文)</span><span class="sxs-lookup"><span data-stu-id="5ba58-1046">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="5ba58-1047">規則引擎條件式運算式 (英文)</span><span class="sxs-lookup"><span data-stu-id="5ba58-1047">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="5ba58-1048">規則引擎比對條件</span><span class="sxs-lookup"><span data-stu-id="5ba58-1048">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="5ba58-1049">覆寫使用 hello 規則引擎的預設 HTTP 行為</span><span class="sxs-lookup"><span data-stu-id="5ba58-1049">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* [<span data-ttu-id="5ba58-1050">Azure CDN 概觀</span><span class="sxs-lookup"><span data-stu-id="5ba58-1050">Azure CDN Overview</span></span>](cdn-overview.md)
