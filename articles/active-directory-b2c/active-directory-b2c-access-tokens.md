---
title: "Azure Active Directory B2C：要求存取權杖 | Microsoft Docs"
description: "本文將說明如何設定用戶端應用程式，並取得存取權杖。"
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 4b361a8e69f885d5b89ac9b2086e2731ee4d8b48
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a><span data-ttu-id="acc32-103">Azure AD B2C︰要求存取權杖</span><span class="sxs-lookup"><span data-stu-id="acc32-103">Azure AD B2C: Requesting access tokens</span></span>

<span data-ttu-id="acc32-104">存取權杖 (在 Azure AD B2C 的回應中表示為 **access\_token**) 是一種安全性權杖形式，用戶端可用來存取受[授權伺服器](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics)保護的資源，例如 web API。</span><span class="sxs-lookup"><span data-stu-id="acc32-104">An access token (denoted as **access\_token** in the responses from Azure AD B2C) is a form of security token that a client can use to access resources that are secured by an [authorization server](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), such as a web API.</span></span> <span data-ttu-id="acc32-105">存取權杖統稱為[JWT](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens)，且包含關於預期資源伺服器和伺服器授與權限的資訊。</span><span class="sxs-lookup"><span data-stu-id="acc32-105">Access tokens are represented as [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) and contain information about the intended resource server and the granted permissions to the server.</span></span> <span data-ttu-id="acc32-106">在呼叫資源伺服器時，存取權杖必須出現在 HTTP 要求中。</span><span class="sxs-lookup"><span data-stu-id="acc32-106">When calling the resource server, the access token must be present in the HTTP request.</span></span>

<span data-ttu-id="acc32-107">本文將討論如何設定用戶端應用程式與 Web API 以取得 **access\_token**。</span><span class="sxs-lookup"><span data-stu-id="acc32-107">This article discusses how to configure a client application and web API in order to obtain an **access\_token**.</span></span>

> [!NOTE]
> <span data-ttu-id="acc32-108">**Azure AD B2C 不支援 Web API 鏈結 (代理者)。**</span><span class="sxs-lookup"><span data-stu-id="acc32-108">**Web API chains (On-Behalf-Of) is not supported by Azure AD B2C.**</span></span>
>
> <span data-ttu-id="acc32-109">許多架構中都有一個 Web API 需要呼叫另一個下游 Web API，而兩者都受 Azure AD B2C 保護。</span><span class="sxs-lookup"><span data-stu-id="acc32-109">Many architectures include a web API that needs to call another downstream web API, both secured by Azure AD B2C.</span></span> <span data-ttu-id="acc32-110">此情況常見於有 Web API 後端的原生用戶端，而後端會再呼叫 Azure AD 圖形 API 等 Microsoft 線上服務。</span><span class="sxs-lookup"><span data-stu-id="acc32-110">This scenario is common in native clients that have a web API back end, which in turn calls a Microsoft online service such as the Azure AD Graph API.</span></span>
>
> <span data-ttu-id="acc32-111">使用 OAuth 2.0 JWT 持有人認證授與可支援此鏈結的 Web API 案例，亦稱為「代理者流程」。</span><span class="sxs-lookup"><span data-stu-id="acc32-111">This chained web API scenario can be supported by using the OAuth 2.0 JWT Bearer Credential grant, otherwise known as the On-Behalf-Of flow.</span></span> <span data-ttu-id="acc32-112">不過，Azure AD B2C 目前未實作代理者流程。</span><span class="sxs-lookup"><span data-stu-id="acc32-112">However, the On-Behalf-Of flow is not currently implemented in Azure AD B2C.</span></span>

## <a name="register-a-web-api-and-publish-permissions"></a><span data-ttu-id="acc32-113">註冊 Web API 與發佈權限</span><span class="sxs-lookup"><span data-stu-id="acc32-113">Register a web API and publish permissions</span></span>

<span data-ttu-id="acc32-114">要求存取權杖之前，您必須先註冊 Web API 和發佈可以授與用戶端應用程式的權限 (範圍)。</span><span class="sxs-lookup"><span data-stu-id="acc32-114">Before requesting an access token, you first need to register a web API and publish permissions (scopes) that can be granted to the client application.</span></span>

### <a name="register-a-web-api"></a><span data-ttu-id="acc32-115">註冊 Web API</span><span class="sxs-lookup"><span data-stu-id="acc32-115">Register a web API</span></span>

1. <span data-ttu-id="acc32-116">在 Azure 入口網站的 B2C 功能刀鋒視窗中，按一下 [應用程式] 。</span><span class="sxs-lookup"><span data-stu-id="acc32-116">On the B2C features blade on the Azure portal, click **Applications**.</span></span>
1. <span data-ttu-id="acc32-117">按一下刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="acc32-117">Click **+Add** at the top of the blade.</span></span>
1. <span data-ttu-id="acc32-118">輸入應用程式的 **名稱** ，此名稱將會為取用者說明您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc32-118">Enter a **Name** for the application that will describe your application to consumers.</span></span> <span data-ttu-id="acc32-119">例如，您可以輸入「Contoso API」。</span><span class="sxs-lookup"><span data-stu-id="acc32-119">For example, you could enter "Contoso API".</span></span>
1. <span data-ttu-id="acc32-120">將 [包括 web 應用程式 / web API] 切換為 [是]。</span><span class="sxs-lookup"><span data-stu-id="acc32-120">Toggle the **Include web app / web API** switch to **Yes**.</span></span>
1. <span data-ttu-id="acc32-121">在 [回覆 URL] 輸入任意值。</span><span class="sxs-lookup"><span data-stu-id="acc32-121">Enter an arbitrary value for the **Reply URLs**.</span></span> <span data-ttu-id="acc32-122">例如，輸入 `https://localhost:44316/`。</span><span class="sxs-lookup"><span data-stu-id="acc32-122">For example, enter `https://localhost:44316/`.</span></span> <span data-ttu-id="acc32-123">這個值無關緊要，因為 API 不應該直接從 Azure AD B2C 接收權杖。</span><span class="sxs-lookup"><span data-stu-id="acc32-123">The value does not matter since an API should not be receiving the token directly from Azure AD B2C.</span></span>
1. <span data-ttu-id="acc32-124">輸入 [應用程式識別碼 URI]。</span><span class="sxs-lookup"><span data-stu-id="acc32-124">Enter an **App ID URI**.</span></span> <span data-ttu-id="acc32-125">這是您的 Web API 所使用的識別碼。</span><span class="sxs-lookup"><span data-stu-id="acc32-125">This is the identifier used for your web API.</span></span> <span data-ttu-id="acc32-126">例如，在方塊中輸入「notes」。</span><span class="sxs-lookup"><span data-stu-id="acc32-126">For example, enter 'notes' in the box.</span></span> <span data-ttu-id="acc32-127">[App ID URI] 即會顯示為 `https://{tenantName}.onmicrosoft.com/notes`。</span><span class="sxs-lookup"><span data-stu-id="acc32-127">The **App ID URI** would then be `https://{tenantName}.onmicrosoft.com/notes`.</span></span>
1. <span data-ttu-id="acc32-128">按一下 [建立]  以註冊您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc32-128">Click **Create** to register your application.</span></span>
1. <span data-ttu-id="acc32-129">按一下您剛才建立的應用程式，並複製稍後要在程式碼中使用的全域唯一 **應用程式用戶端識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="acc32-129">Click the application that you just created and copy down the globally unique **Application Client ID** that you'll use later in your code.</span></span>

### <a name="publishing-permissions"></a><span data-ttu-id="acc32-130">發佈權限</span><span class="sxs-lookup"><span data-stu-id="acc32-130">Publishing permissions</span></span>

<span data-ttu-id="acc32-131">範圍類似權限，當應用程式在呼叫 API 時，範圍是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="acc32-131">Scopes, which are analogous to permissions, are necessary when your app is calling an API.</span></span> <span data-ttu-id="acc32-132">舉例來說，「讀取」或「寫入」即是範圍。</span><span class="sxs-lookup"><span data-stu-id="acc32-132">Some examples of scopes are "read" or "write".</span></span> <span data-ttu-id="acc32-133">假設您想要您的 Web 或原生應用程式從 API 「讀取」。</span><span class="sxs-lookup"><span data-stu-id="acc32-133">Suppose you want your web or native app to "read" from an API.</span></span> <span data-ttu-id="acc32-134">您的應用程式會呼叫 Azure AD B2C 並要求一個存取權杖，該權杖會將存取權授與「讀取」範圍。</span><span class="sxs-lookup"><span data-stu-id="acc32-134">Your app would call Azure AD B2C and request an access token that gives access to the scope "read".</span></span> <span data-ttu-id="acc32-135">為了讓 Azure AD B2C 發出這類存取權杖，必須將可從特定 API 「讀取」的權限授與該應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc32-135">In order for Azure AD B2C to emit such an access token, the app needs to be granted permission to "read" from the specific API.</span></span> <span data-ttu-id="acc32-136">因此，您的 API 必須先發佈「讀取」範圍。</span><span class="sxs-lookup"><span data-stu-id="acc32-136">To do this, your API first needs to publish the "read" scope.</span></span>

1. <span data-ttu-id="acc32-137">在 Azure AD B2C [應用程式] 刀鋒視窗中，開啟 Web API 應用程式 (「Contoso API」)。</span><span class="sxs-lookup"><span data-stu-id="acc32-137">Within the Azure AD B2C **Applications** blade, open the web API application ("Contoso API").</span></span>
1. <span data-ttu-id="acc32-138">按一下 [已發佈範圍]。</span><span class="sxs-lookup"><span data-stu-id="acc32-138">Click on **Published scopes**.</span></span> <span data-ttu-id="acc32-139">您會在此定義可授予其他應用程式的權限 (範圍)。</span><span class="sxs-lookup"><span data-stu-id="acc32-139">This is where you define the permissions (scopes) that can be granted to other applications.</span></span>
1. <span data-ttu-id="acc32-140">視需要新增 [範圍值] \(例如「讀取」)。</span><span class="sxs-lookup"><span data-stu-id="acc32-140">Add **Scope Values** as necessary (for example, "read").</span></span> <span data-ttu-id="acc32-141">根據預設，將會定義 "user_impersonation" 範圍。</span><span class="sxs-lookup"><span data-stu-id="acc32-141">By default, the "user_impersonation" scope will be defined.</span></span> <span data-ttu-id="acc32-142">想要的話，也可以忽略此步驟。</span><span class="sxs-lookup"><span data-stu-id="acc32-142">You can ignore this if you wish.</span></span> <span data-ttu-id="acc32-143">在 [範圍名稱] 資料行中輸入範圍的描述。</span><span class="sxs-lookup"><span data-stu-id="acc32-143">Enter a description of the scope in the **Scope Name** column.</span></span>
1. <span data-ttu-id="acc32-144">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="acc32-144">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acc32-145">[範圍名稱] 是 [範圍值] 的描述。</span><span class="sxs-lookup"><span data-stu-id="acc32-145">The **Scope Name** is the description of the **Scope Value**.</span></span> <span data-ttu-id="acc32-146">當使用範圍時，請務必使用 [範圍值]。</span><span class="sxs-lookup"><span data-stu-id="acc32-146">When using the scope, make sure to use the **Scope Value**.</span></span>

## <a name="grant-a-native-or-web-app-permissions-to-a-web-api"></a><span data-ttu-id="acc32-147">將原生或 Web 應用程式的權限授與 Web API</span><span class="sxs-lookup"><span data-stu-id="acc32-147">Grant a native or web app permissions to a web API</span></span>

<span data-ttu-id="acc32-148">設定好 API 發佈範圍後，必須透過 Azure 入口網站將這些範圍授與用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc32-148">Once an API is configured to publish scopes, the client application needs to be granted those scopes via the Azure portal.</span></span>

1. <span data-ttu-id="acc32-149">瀏覽至 B2C 功能刀鋒視窗中的**應用程式**功能表。</span><span class="sxs-lookup"><span data-stu-id="acc32-149">Navigate to the **Applications** menu in the B2C features blade.</span></span>
1. <span data-ttu-id="acc32-150">如果您還沒有用戶端應用程式 ([Web 應用程式](active-directory-b2c-app-registration.md#register-a-web-app)或[原生用戶端](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app))，請註冊一個。</span><span class="sxs-lookup"><span data-stu-id="acc32-150">Register a client application ([web app](active-directory-b2c-app-registration.md#register-a-web-app) or [native client](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) if you don’t have one already.</span></span> <span data-ttu-id="acc32-151">如果您一開始便是跟隨本指南的說明進行，則需要註冊用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="acc32-151">If you are following this guide as your starting point, you'll need to register a client application.</span></span>
1. <span data-ttu-id="acc32-152">按一下 [API 存取]。</span><span class="sxs-lookup"><span data-stu-id="acc32-152">Click on **API access**.</span></span>
1. <span data-ttu-id="acc32-153">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="acc32-153">Click on **Add**.</span></span>
1. <span data-ttu-id="acc32-154">選取您的 web API，以及您想要授與的範圍 (權限)。</span><span class="sxs-lookup"><span data-stu-id="acc32-154">Select your web API and the scopes (permissions) you would like to grant.</span></span>
1. <span data-ttu-id="acc32-155">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="acc32-155">Click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="acc32-156">Azure AD B2C 不會要求您的用戶端應用程式使用者同意。</span><span class="sxs-lookup"><span data-stu-id="acc32-156">Azure AD B2C does not ask your client application users for their consent.</span></span> <span data-ttu-id="acc32-157">相反地，根據上述應用程式之間設定的權限，所有同意都係由系統管理員提供。</span><span class="sxs-lookup"><span data-stu-id="acc32-157">Instead, all consent is provided by the admin, based on the permissions configured between the applications described above.</span></span> <span data-ttu-id="acc32-158">如果已撤銷應用程式的權限授與，所有先前能夠取得該權限的使用者將不再能夠執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="acc32-158">If a permission grant for an application is revoked, all users who were previously able to acquire that permission will no longer be able to do so.</span></span>

## <a name="requesting-a-token"></a><span data-ttu-id="acc32-159">要求權杖</span><span class="sxs-lookup"><span data-stu-id="acc32-159">Requesting a token</span></span>

<span data-ttu-id="acc32-160">在要求存取權杖時，用戶端應用程式必須在要求的 [scope] 參數中指定所需的權限。</span><span class="sxs-lookup"><span data-stu-id="acc32-160">When requesting an access token, the client application needs to specify the desired permissions in the **scope** parameter of the request.</span></span> <span data-ttu-id="acc32-161">例如，若要將 [App ID URI] 為 `https://contoso.onmicrosoft.com/notes` 的 API 的 [範圍值] 指定為 [read]，則範圍為 `https://contoso.onmicrosoft.com/notes/read`。</span><span class="sxs-lookup"><span data-stu-id="acc32-161">For example, to specify the **Scope Value** “read” for the API that has the **App ID URI** of `https://contoso.onmicrosoft.com/notes`, the scope would be `https://contoso.onmicrosoft.com/notes/read`.</span></span> <span data-ttu-id="acc32-162">以下是對 `/authorize` 端點授權碼要求的範例。</span><span class="sxs-lookup"><span data-stu-id="acc32-162">Below is an example of an authorization code request to the `/authorize` endpoint.</span></span>

> [!NOTE]
> <span data-ttu-id="acc32-163">目前，自訂網域並未和存取權杖一起受到支援。</span><span class="sxs-lookup"><span data-stu-id="acc32-163">Currently, custom domains are not supported along with access tokens.</span></span> <span data-ttu-id="acc32-164">您必須在要求 URL 中使用您的 tenantName.onmicrosoft.com 網域。</span><span class="sxs-lookup"><span data-stu-id="acc32-164">You must use your tenantName.onmicrosoft.com domain in the request URL.</span></span>

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

<span data-ttu-id="acc32-165">要在相同的要求中取得多個權限，您可以在單一**範圍**參數中新增多個項目，以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="acc32-165">To acquire multiple permissions in the same request, you can add multiple entries in the single **scope** parameter, separated by spaces.</span></span> <span data-ttu-id="acc32-166">例如：</span><span class="sxs-lookup"><span data-stu-id="acc32-166">For example:</span></span>

<span data-ttu-id="acc32-167">解碼的 URL：</span><span class="sxs-lookup"><span data-stu-id="acc32-167">URL decoded:</span></span>

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

<span data-ttu-id="acc32-168">編碼的 URL：</span><span class="sxs-lookup"><span data-stu-id="acc32-168">URL encoded:</span></span>

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

<span data-ttu-id="acc32-169">您可能會要求比授與用戶端應用程式更多的資源範圍 (權限)。</span><span class="sxs-lookup"><span data-stu-id="acc32-169">You may request more scopes (permissions) for a resource than what is granted for your client application.</span></span> <span data-ttu-id="acc32-170">在此情況時，如果至少授與一個權限，則呼叫會成功。</span><span class="sxs-lookup"><span data-stu-id="acc32-170">When this is the case, the call will succeed if at least one permission is granted.</span></span> <span data-ttu-id="acc32-171">所產生的**存取\_權杖**會僅使用已成功授與的權限填入其 “scp” 宣告。</span><span class="sxs-lookup"><span data-stu-id="acc32-171">The resulting **access\_token** will have its “scp” claim populated with only the permissions that were successfully granted.</span></span>

> [!NOTE] 
> <span data-ttu-id="acc32-172">我們在相同的要求中不支援兩個不同 web 資源要求的權限。</span><span class="sxs-lookup"><span data-stu-id="acc32-172">We do not support requesting permissions against two different web resources in the same request.</span></span> <span data-ttu-id="acc32-173">這種要求將會失敗。</span><span class="sxs-lookup"><span data-stu-id="acc32-173">This kind of request will fail.</span></span>

### <a name="special-cases"></a><span data-ttu-id="acc32-174">特殊案例</span><span class="sxs-lookup"><span data-stu-id="acc32-174">Special cases</span></span>

<span data-ttu-id="acc32-175">OpenID Connect 標準會指定數個特殊的「範圍」值。</span><span class="sxs-lookup"><span data-stu-id="acc32-175">The OpenID Connect standard specifies several special “scope” values.</span></span> <span data-ttu-id="acc32-176">下列特殊範圍代表「存取使用者設定檔」的權限︰</span><span class="sxs-lookup"><span data-stu-id="acc32-176">The following special scopes represent the permission to “access the user’s profile”:</span></span>

* <span data-ttu-id="acc32-177">**openid**︰這會要求識別碼權杖</span><span class="sxs-lookup"><span data-stu-id="acc32-177">**openid**: This requests an ID token</span></span>
* <span data-ttu-id="acc32-178">**offline\_access**︰這會要求重新整理權杖 (使用[授權碼流程](active-directory-b2c-reference-oauth-code.md))。</span><span class="sxs-lookup"><span data-stu-id="acc32-178">**offline\_access**: This requests a refresh token (using [Auth Code flows](active-directory-b2c-reference-oauth-code.md)).</span></span>

<span data-ttu-id="acc32-179">如果 `/authorize` 要求中的 `response_type` 參數包含 `token`，則 `scope` 參數必須包含至少一個會授與的資源範圍 (`openid` 與 `offline_access` 以外)。</span><span class="sxs-lookup"><span data-stu-id="acc32-179">If the `response_type` parameter in a `/authorize` request includes `token`, the `scope` parameter must include at least one resource scope (other than `openid` and `offline_access`) that will be granted.</span></span> <span data-ttu-id="acc32-180">否則，`/authorize` 要求將會結束並發生失敗。</span><span class="sxs-lookup"><span data-stu-id="acc32-180">Otherwise, the `/authorize` request will terminate with a failure.</span></span>

## <a name="the-returned-token"></a><span data-ttu-id="acc32-181">傳回的權杖</span><span class="sxs-lookup"><span data-stu-id="acc32-181">The returned token</span></span>

<span data-ttu-id="acc32-182">在成功產生**存取\_權杖** (從 `/authorize` 或 `/token` 端點)，會出現下列宣告︰</span><span class="sxs-lookup"><span data-stu-id="acc32-182">In a successfully minted **access\_token** (from either the `/authorize` or `/token` endpoint), the following claims will be present:</span></span>

| <span data-ttu-id="acc32-183">名稱</span><span class="sxs-lookup"><span data-stu-id="acc32-183">Name</span></span> | <span data-ttu-id="acc32-184">宣告</span><span class="sxs-lookup"><span data-stu-id="acc32-184">Claim</span></span> | <span data-ttu-id="acc32-185">說明</span><span class="sxs-lookup"><span data-stu-id="acc32-185">Description</span></span> |
| --- | --- | --- |
|<span data-ttu-id="acc32-186">對象</span><span class="sxs-lookup"><span data-stu-id="acc32-186">Audience</span></span> |`aud` |<span data-ttu-id="acc32-187">權杖授與存取權的單一資源之應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="acc32-187">The **application ID** of the single resource that the token grants access to.</span></span> |
|<span data-ttu-id="acc32-188">Scope</span><span class="sxs-lookup"><span data-stu-id="acc32-188">Scope</span></span> |`scp` |<span data-ttu-id="acc32-189">授與給資源的權限。</span><span class="sxs-lookup"><span data-stu-id="acc32-189">The permissions granted to the resource.</span></span> <span data-ttu-id="acc32-190">多個授與權限將會以空格隔開。</span><span class="sxs-lookup"><span data-stu-id="acc32-190">Multiple granted permissions will be separated by space.</span></span> |
|<span data-ttu-id="acc32-191">授權的合作對象</span><span class="sxs-lookup"><span data-stu-id="acc32-191">Authorized Party</span></span> |`azp` |<span data-ttu-id="acc32-192">起始要求之用戶端應用程式的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="acc32-192">The **application ID** of the client application that initiated the request.</span></span> |

<span data-ttu-id="acc32-193">當您的 API 收到**存取\_權杖**時，它必須[驗證權杖](active-directory-b2c-reference-tokens.md)以證明權杖的真實性，並具有正確的宣告。</span><span class="sxs-lookup"><span data-stu-id="acc32-193">When your API receives the **access\_token**, it must [validate the token](active-directory-b2c-reference-tokens.md) to prove that the token is authentic and has the correct claims.</span></span>

<span data-ttu-id="acc32-194">我們歡迎意見反應和建議！</span><span class="sxs-lookup"><span data-stu-id="acc32-194">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="acc32-195">如果您對本主題有任何問題，請利用標記 ['azure-ad-b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c) 並張貼至 Stack Overflow。</span><span class="sxs-lookup"><span data-stu-id="acc32-195">If you have any difficulties with this topic, please post on Stack Overflow using the tag ['azure-ad-b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c).</span></span> <span data-ttu-id="acc32-196">對於功能要求，請將它們新增到 [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。</span><span class="sxs-lookup"><span data-stu-id="acc32-196">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

## <a name="next-steps"></a><span data-ttu-id="acc32-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="acc32-197">Next steps</span></span>

* <span data-ttu-id="acc32-198">使用 [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi) 建置 Web API</span><span class="sxs-lookup"><span data-stu-id="acc32-198">Build a web API using [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)</span></span>
* <span data-ttu-id="acc32-199">使用 [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) 建置 Web API</span><span class="sxs-lookup"><span data-stu-id="acc32-199">Build a web API using [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)</span></span>
