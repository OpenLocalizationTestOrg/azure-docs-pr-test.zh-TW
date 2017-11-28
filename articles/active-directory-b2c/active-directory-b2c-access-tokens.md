---
title: "Azure Active Directory B2C：要求存取權杖 | Microsoft Docs"
description: "這篇文章將示範如何 toosetup 用戶端應用程式，並取得存取權杖。"
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
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a><span data-ttu-id="12431-103">Azure AD B2C︰要求存取權杖</span><span class="sxs-lookup"><span data-stu-id="12431-103">Azure AD B2C: Requesting access tokens</span></span>

<span data-ttu-id="12431-104">存取權杖 (表示為**存取\_語彙基元**從 Azure AD B2C hello 回應中) 是一種安全性權杖的用戶端可以使用 tooaccess 資源都會受到[授權伺服器](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics)，例如 web API。</span><span class="sxs-lookup"><span data-stu-id="12431-104">An access token (denoted as **access\_token** in hello responses from Azure AD B2C) is a form of security token that a client can use tooaccess resources that are secured by an [authorization server](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), such as a web API.</span></span> <span data-ttu-id="12431-105">存取權杖以[Jwt](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens)包含 hello 預期之資源伺服器與 hello 授與權限 toohello 伺服器相關資訊。</span><span class="sxs-lookup"><span data-stu-id="12431-105">Access tokens are represented as [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) and contain information about hello intended resource server and hello granted permissions toohello server.</span></span> <span data-ttu-id="12431-106">在呼叫 hello 資源伺服器，hello 存取權杖中必須要有 hello HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="12431-106">When calling hello resource server, hello access token must be present in hello HTTP request.</span></span>

<span data-ttu-id="12431-107">本文將討論 tooconfigure 用戶端應用程式和 web API 中的順序如何 tooobtain**存取\_語彙基元**。</span><span class="sxs-lookup"><span data-stu-id="12431-107">This article discusses how tooconfigure a client application and web API in order tooobtain an **access\_token**.</span></span>

> [!NOTE]
> <span data-ttu-id="12431-108">**Azure AD B2C 不支援 Web API 鏈結 (代理者)。**</span><span class="sxs-lookup"><span data-stu-id="12431-108">**Web API chains (On-Behalf-Of) is not supported by Azure AD B2C.**</span></span>
>
> <span data-ttu-id="12431-109">許多架構包含 web API 需要 toocall 另一個下游 web API，同時受到 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="12431-109">Many architectures include a web API that needs toocall another downstream web API, both secured by Azure AD B2C.</span></span> <span data-ttu-id="12431-110">這種情況下會在具有 web API 後端，依序呼叫的 Microsoft 線上服務，例如 hello Azure AD Graph API 的原生用戶端。</span><span class="sxs-lookup"><span data-stu-id="12431-110">This scenario is common in native clients that have a web API back end, which in turn calls a Microsoft online service such as hello Azure AD Graph API.</span></span>
>
> <span data-ttu-id="12431-111">這個鏈結的 web API 」 案例可支援使用 OAuth 2.0 JWT Bearer 認證授與，否則為 hello 稱為 hello 代表的流程。</span><span class="sxs-lookup"><span data-stu-id="12431-111">This chained web API scenario can be supported by using hello OAuth 2.0 JWT Bearer Credential grant, otherwise known as hello On-Behalf-Of flow.</span></span> <span data-ttu-id="12431-112">不過，hello 上-代表 」 流程目前尚未實作 Azure AD B2C 中。</span><span class="sxs-lookup"><span data-stu-id="12431-112">However, hello On-Behalf-Of flow is not currently implemented in Azure AD B2C.</span></span>

## <a name="register-a-web-api-and-publish-permissions"></a><span data-ttu-id="12431-113">註冊 Web API 與發佈權限</span><span class="sxs-lookup"><span data-stu-id="12431-113">Register a web API and publish permissions</span></span>

<span data-ttu-id="12431-114">要求存取權杖之前，首先需要 tooregister web API，並發佈 toohello 用戶端應用程式被授與的權限 （範圍）。</span><span class="sxs-lookup"><span data-stu-id="12431-114">Before requesting an access token, you first need tooregister a web API and publish permissions (scopes) that can be granted toohello client application.</span></span>

### <a name="register-a-web-api"></a><span data-ttu-id="12431-115">註冊 Web API</span><span class="sxs-lookup"><span data-stu-id="12431-115">Register a web API</span></span>

1. <span data-ttu-id="12431-116">在 [hello B2C 功能刀鋒視窗中 hello Azure 入口網站上，按一下 [**應用程式**。</span><span class="sxs-lookup"><span data-stu-id="12431-116">On hello B2C features blade on hello Azure portal, click **Applications**.</span></span>
1. <span data-ttu-id="12431-117">按一下**+ 加**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="12431-117">Click **+Add** at hello top of hello blade.</span></span>
1. <span data-ttu-id="12431-118">輸入**名稱**會描述應用程式 tooconsumers hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12431-118">Enter a **Name** for hello application that will describe your application tooconsumers.</span></span> <span data-ttu-id="12431-119">例如，您可以輸入「Contoso API」。</span><span class="sxs-lookup"><span data-stu-id="12431-119">For example, you could enter "Contoso API".</span></span>
1. <span data-ttu-id="12431-120">切換 hello**包括 web 應用程式 / web API**太切換**是**。</span><span class="sxs-lookup"><span data-stu-id="12431-120">Toggle hello **Include web app / web API** switch too**Yes**.</span></span>
1. <span data-ttu-id="12431-121">輸入代表 hello 的任意值**回覆 Url**。</span><span class="sxs-lookup"><span data-stu-id="12431-121">Enter an arbitrary value for hello **Reply URLs**.</span></span> <span data-ttu-id="12431-122">例如，輸入 `https://localhost:44316/`。</span><span class="sxs-lookup"><span data-stu-id="12431-122">For example, enter `https://localhost:44316/`.</span></span> <span data-ttu-id="12431-123">因為應用程式開發介面應該不會收到 hello 語彙基元直接從 Azure AD B2C hello 值並不重要。</span><span class="sxs-lookup"><span data-stu-id="12431-123">hello value does not matter since an API should not be receiving hello token directly from Azure AD B2C.</span></span>
1. <span data-ttu-id="12431-124">輸入 [應用程式識別碼 URI]。</span><span class="sxs-lookup"><span data-stu-id="12431-124">Enter an **App ID URI**.</span></span> <span data-ttu-id="12431-125">這是用於您的 web API 的 hello 識別碼。</span><span class="sxs-lookup"><span data-stu-id="12431-125">This is hello identifier used for your web API.</span></span> <span data-ttu-id="12431-126">例如，在 hello 方塊中輸入 「 附註 」。</span><span class="sxs-lookup"><span data-stu-id="12431-126">For example, enter 'notes' in hello box.</span></span> <span data-ttu-id="12431-127">hello**應用程式識別碼 URI**將`https://{tenantName}.onmicrosoft.com/notes`。</span><span class="sxs-lookup"><span data-stu-id="12431-127">hello **App ID URI** would then be `https://{tenantName}.onmicrosoft.com/notes`.</span></span>
1. <span data-ttu-id="12431-128">按一下**建立**tooregister 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="12431-128">Click **Create** tooregister your application.</span></span>
1. <span data-ttu-id="12431-129">按一下您剛才建立的 hello 應用程式，並複製 hello 全域唯一**應用程式用戶端識別碼**，您將使用您的程式碼中的更新版本。</span><span class="sxs-lookup"><span data-stu-id="12431-129">Click hello application that you just created and copy down hello globally unique **Application Client ID** that you'll use later in your code.</span></span>

### <a name="publishing-permissions"></a><span data-ttu-id="12431-130">發佈權限</span><span class="sxs-lookup"><span data-stu-id="12431-130">Publishing permissions</span></span>

<span data-ttu-id="12431-131">您的應用程式呼叫 API 時，所需範圍，也就是類似 toopermissions。</span><span class="sxs-lookup"><span data-stu-id="12431-131">Scopes, which are analogous toopermissions, are necessary when your app is calling an API.</span></span> <span data-ttu-id="12431-132">舉例來說，「讀取」或「寫入」即是範圍。</span><span class="sxs-lookup"><span data-stu-id="12431-132">Some examples of scopes are "read" or "write".</span></span> <span data-ttu-id="12431-133">假設您想要您的 web 或太 「 讀取 」 從 API 的原生應用程式。</span><span class="sxs-lookup"><span data-stu-id="12431-133">Suppose you want your web or native app too"read" from an API.</span></span> <span data-ttu-id="12431-134">您的應用程式會呼叫 Azure AD B2C，並要求存取權杖，提供存取 toohello 領域 「 讀取 」。</span><span class="sxs-lookup"><span data-stu-id="12431-134">Your app would call Azure AD B2C and request an access token that gives access toohello scope "read".</span></span> <span data-ttu-id="12431-135">若要讓 Azure AD B2C tooemit 存取權杖，必須授與權限太 「 讀取 」 從 hello 特定 API 的 toobe hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12431-135">In order for Azure AD B2C tooemit such an access token, hello app needs toobe granted permission too"read" from hello specific API.</span></span> <span data-ttu-id="12431-136">toodo，您的 API，首先必須 toopublish hello 「 讀取 」 的範圍。</span><span class="sxs-lookup"><span data-stu-id="12431-136">toodo this, your API first needs toopublish hello "read" scope.</span></span>

1. <span data-ttu-id="12431-137">在 Azure AD B2C hello**應用程式**刀鋒視窗中，開啟 hello web API 應用程式 ("Contoso API 」)。</span><span class="sxs-lookup"><span data-stu-id="12431-137">Within hello Azure AD B2C **Applications** blade, open hello web API application ("Contoso API").</span></span>
1. <span data-ttu-id="12431-138">按一下 [已發佈範圍]。</span><span class="sxs-lookup"><span data-stu-id="12431-138">Click on **Published scopes**.</span></span> <span data-ttu-id="12431-139">這是您用來定義 hello 權限 （領域） 可以授與 tooother 應用程式。</span><span class="sxs-lookup"><span data-stu-id="12431-139">This is where you define hello permissions (scopes) that can be granted tooother applications.</span></span>
1. <span data-ttu-id="12431-140">視需要新增 [範圍值] \(例如「讀取」)。</span><span class="sxs-lookup"><span data-stu-id="12431-140">Add **Scope Values** as necessary (for example, "read").</span></span> <span data-ttu-id="12431-141">依預設，會定義 hello"user_impersonation"範圍。</span><span class="sxs-lookup"><span data-stu-id="12431-141">By default, hello "user_impersonation" scope will be defined.</span></span> <span data-ttu-id="12431-142">想要的話，也可以忽略此步驟。</span><span class="sxs-lookup"><span data-stu-id="12431-142">You can ignore this if you wish.</span></span> <span data-ttu-id="12431-143">在 [hello 輸入 hello 範圍的描述**領域名稱**資料行。</span><span class="sxs-lookup"><span data-stu-id="12431-143">Enter a description of hello scope in hello **Scope Name** column.</span></span>
1. <span data-ttu-id="12431-144">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="12431-144">Click **Save**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12431-145">hello**領域名稱**hello hello 描述**範圍值**。</span><span class="sxs-lookup"><span data-stu-id="12431-145">hello **Scope Name** is hello description of hello **Scope Value**.</span></span> <span data-ttu-id="12431-146">當使用 hello 範圍，請確定 toouse hello**範圍值**。</span><span class="sxs-lookup"><span data-stu-id="12431-146">When using hello scope, make sure toouse hello **Scope Value**.</span></span>

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a><span data-ttu-id="12431-147">授與原生或 web 應用程式的權限 tooa web API</span><span class="sxs-lookup"><span data-stu-id="12431-147">Grant a native or web app permissions tooa web API</span></span>

<span data-ttu-id="12431-148">一旦應用程式開發介面設定的 toopublish 範圍，hello 用戶端應用程式需要 toobe 授與這些範圍透過 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="12431-148">Once an API is configured toopublish scopes, hello client application needs toobe granted those scopes via hello Azure portal.</span></span>

1. <span data-ttu-id="12431-149">瀏覽 toohello**應用程式**hello B2C 功能刀鋒視窗中的功能表。</span><span class="sxs-lookup"><span data-stu-id="12431-149">Navigate toohello **Applications** menu in hello B2C features blade.</span></span>
1. <span data-ttu-id="12431-150">如果您還沒有用戶端應用程式 ([Web 應用程式](active-directory-b2c-app-registration.md#register-a-web-app)或[原生用戶端](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app))，請註冊一個。</span><span class="sxs-lookup"><span data-stu-id="12431-150">Register a client application ([web app](active-directory-b2c-app-registration.md#register-a-web-app) or [native client](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) if you don’t have one already.</span></span> <span data-ttu-id="12431-151">如果您是依照本指南為您的起始點，您將需要 tooregister 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="12431-151">If you are following this guide as your starting point, you'll need tooregister a client application.</span></span>
1. <span data-ttu-id="12431-152">按一下 [API 存取]。</span><span class="sxs-lookup"><span data-stu-id="12431-152">Click on **API access**.</span></span>
1. <span data-ttu-id="12431-153">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="12431-153">Click on **Add**.</span></span>
1. <span data-ttu-id="12431-154">選取您 web 應用程式開發介面和 hello 範圍 （權限） （您想要 toogrant。</span><span class="sxs-lookup"><span data-stu-id="12431-154">Select your web API and hello scopes (permissions) you would like toogrant.</span></span>
1. <span data-ttu-id="12431-155">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="12431-155">Click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="12431-156">Azure AD B2C 不會要求您的用戶端應用程式使用者同意。</span><span class="sxs-lookup"><span data-stu-id="12431-156">Azure AD B2C does not ask your client application users for their consent.</span></span> <span data-ttu-id="12431-157">相反地，所有同意都係由 hello 系統管理員，根據設定 hello 上面所述的應用程式之間的 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="12431-157">Instead, all consent is provided by hello admin, based on hello permissions configured between hello applications described above.</span></span> <span data-ttu-id="12431-158">如果已撤銷的權限授與應用程式，所有使用者都已之前可以 tooacquire 該權限都將不再是無法 toodo 使。</span><span class="sxs-lookup"><span data-stu-id="12431-158">If a permission grant for an application is revoked, all users who were previously able tooacquire that permission will no longer be able toodo so.</span></span>

## <a name="requesting-a-token"></a><span data-ttu-id="12431-159">要求權杖</span><span class="sxs-lookup"><span data-stu-id="12431-159">Requesting a token</span></span>

<span data-ttu-id="12431-160">Hello 用戶端應用程式要求存取 token 時，需要 toospecify hello 所需權限，在 hello**範圍**hello 要求參數。</span><span class="sxs-lookup"><span data-stu-id="12431-160">When requesting an access token, hello client application needs toospecify hello desired permissions in hello **scope** parameter of hello request.</span></span> <span data-ttu-id="12431-161">比方說，toospecify hello**範圍值**「 讀取 」 hello API 具有 hello**應用程式識別碼 URI**的`https://contoso.onmicrosoft.com/notes`，hello 範圍會`https://contoso.onmicrosoft.com/notes/read`。</span><span class="sxs-lookup"><span data-stu-id="12431-161">For example, toospecify hello **Scope Value** “read” for hello API that has hello **App ID URI** of `https://contoso.onmicrosoft.com/notes`, hello scope would be `https://contoso.onmicrosoft.com/notes/read`.</span></span> <span data-ttu-id="12431-162">以下是範例的授權碼要求 toohello`/authorize`端點。</span><span class="sxs-lookup"><span data-stu-id="12431-162">Below is an example of an authorization code request toohello `/authorize` endpoint.</span></span>

> [!NOTE]
> <span data-ttu-id="12431-163">目前，自訂網域並未和存取權杖一起受到支援。</span><span class="sxs-lookup"><span data-stu-id="12431-163">Currently, custom domains are not supported along with access tokens.</span></span> <span data-ttu-id="12431-164">您必須使用 tenantName.onmicrosoft.com 網域 hello 要求 URL 中。</span><span class="sxs-lookup"><span data-stu-id="12431-164">You must use your tenantName.onmicrosoft.com domain in hello request URL.</span></span>

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

<span data-ttu-id="12431-165">tooacquire 相同要求中 hello 的多個權限，您可以加入多個項目在單一的 hello**範圍**參數，以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="12431-165">tooacquire multiple permissions in hello same request, you can add multiple entries in hello single **scope** parameter, separated by spaces.</span></span> <span data-ttu-id="12431-166">例如：</span><span class="sxs-lookup"><span data-stu-id="12431-166">For example:</span></span>

<span data-ttu-id="12431-167">解碼的 URL：</span><span class="sxs-lookup"><span data-stu-id="12431-167">URL decoded:</span></span>

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

<span data-ttu-id="12431-168">編碼的 URL：</span><span class="sxs-lookup"><span data-stu-id="12431-168">URL encoded:</span></span>

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

<span data-ttu-id="12431-169">您可能會要求比授與用戶端應用程式更多的資源範圍 (權限)。</span><span class="sxs-lookup"><span data-stu-id="12431-169">You may request more scopes (permissions) for a resource than what is granted for your client application.</span></span> <span data-ttu-id="12431-170">當這種情況 hello 時，hello 呼叫將會成功，如果至少一項權限會授與。</span><span class="sxs-lookup"><span data-stu-id="12431-170">When this is hello case, hello call will succeed if at least one permission is granted.</span></span> <span data-ttu-id="12431-171">hello 產生**存取\_語彙基元**必須填入唯一的 hello 權限成功授與它的"scp"宣告。</span><span class="sxs-lookup"><span data-stu-id="12431-171">hello resulting **access\_token** will have its “scp” claim populated with only hello permissions that were successfully granted.</span></span>

> [!NOTE] 
> <span data-ttu-id="12431-172">我們在 hello 不支援要求的權限，針對兩個不同的網頁資源相同的要求。</span><span class="sxs-lookup"><span data-stu-id="12431-172">We do not support requesting permissions against two different web resources in hello same request.</span></span> <span data-ttu-id="12431-173">這種要求將會失敗。</span><span class="sxs-lookup"><span data-stu-id="12431-173">This kind of request will fail.</span></span>

### <a name="special-cases"></a><span data-ttu-id="12431-174">特殊案例</span><span class="sxs-lookup"><span data-stu-id="12431-174">Special cases</span></span>

<span data-ttu-id="12431-175">hello OpenID Connect 標準指定數個特殊的 「 範圍 」 值。</span><span class="sxs-lookup"><span data-stu-id="12431-175">hello OpenID Connect standard specifies several special “scope” values.</span></span> <span data-ttu-id="12431-176">hello 太下列特殊領域代表 hello 權限 「 存取 hello 使用者設定檔 」:</span><span class="sxs-lookup"><span data-stu-id="12431-176">hello following special scopes represent hello permission too“access hello user’s profile”:</span></span>

* <span data-ttu-id="12431-177">**openid**︰這會要求識別碼權杖</span><span class="sxs-lookup"><span data-stu-id="12431-177">**openid**: This requests an ID token</span></span>
* <span data-ttu-id="12431-178">**offline\_access**︰這會要求重新整理權杖 (使用[授權碼流程](active-directory-b2c-reference-oauth-code.md))。</span><span class="sxs-lookup"><span data-stu-id="12431-178">**offline\_access**: This requests a refresh token (using [Auth Code flows](active-directory-b2c-reference-oauth-code.md)).</span></span>

<span data-ttu-id="12431-179">如果 hello`response_type`中的參數`/authorize`要求包含`token`，hello`scope`參數必須包含至少一個資源的範圍 (以外`openid`和`offline_access`)，將被授與。</span><span class="sxs-lookup"><span data-stu-id="12431-179">If hello `response_type` parameter in a `/authorize` request includes `token`, hello `scope` parameter must include at least one resource scope (other than `openid` and `offline_access`) that will be granted.</span></span> <span data-ttu-id="12431-180">否則，hello`/authorize`要求將會終止與失敗。</span><span class="sxs-lookup"><span data-stu-id="12431-180">Otherwise, hello `/authorize` request will terminate with a failure.</span></span>

## <a name="hello-returned-token"></a><span data-ttu-id="12431-181">傳回語彙基元的 hello</span><span class="sxs-lookup"><span data-stu-id="12431-181">hello returned token</span></span>

<span data-ttu-id="12431-182">在 [已成功產生**存取\_語彙基元**(從任一 hello`/authorize`或`/token`端點)，hello 下列宣告會出現：</span><span class="sxs-lookup"><span data-stu-id="12431-182">In a successfully minted **access\_token** (from either hello `/authorize` or `/token` endpoint), hello following claims will be present:</span></span>

| <span data-ttu-id="12431-183">名稱</span><span class="sxs-lookup"><span data-stu-id="12431-183">Name</span></span> | <span data-ttu-id="12431-184">宣告</span><span class="sxs-lookup"><span data-stu-id="12431-184">Claim</span></span> | <span data-ttu-id="12431-185">說明</span><span class="sxs-lookup"><span data-stu-id="12431-185">Description</span></span> |
| --- | --- | --- |
|<span data-ttu-id="12431-186">對象</span><span class="sxs-lookup"><span data-stu-id="12431-186">Audience</span></span> |`aud` |<span data-ttu-id="12431-187">hello**應用程式識別碼**hello 單一資源的 hello 權杖授與存取權。</span><span class="sxs-lookup"><span data-stu-id="12431-187">hello **application ID** of hello single resource that hello token grants access to.</span></span> |
|<span data-ttu-id="12431-188">Scope</span><span class="sxs-lookup"><span data-stu-id="12431-188">Scope</span></span> |`scp` |<span data-ttu-id="12431-189">hello 權限授與 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="12431-189">hello permissions granted toohello resource.</span></span> <span data-ttu-id="12431-190">多個授與權限將會以空格隔開。</span><span class="sxs-lookup"><span data-stu-id="12431-190">Multiple granted permissions will be separated by space.</span></span> |
|<span data-ttu-id="12431-191">授權的合作對象</span><span class="sxs-lookup"><span data-stu-id="12431-191">Authorized Party</span></span> |`azp` |<span data-ttu-id="12431-192">hello**應用程式識別碼**起始 hello 要求 hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="12431-192">hello **application ID** of hello client application that initiated hello request.</span></span> |

<span data-ttu-id="12431-193">當您的 API 收到 hello**存取\_語彙基元**，它必須[驗證 hello 權杖](active-directory-b2c-reference-tokens.md)hello 語彙基元的 tooprove 是真確的且 hello 正確宣告。</span><span class="sxs-lookup"><span data-stu-id="12431-193">When your API receives hello **access\_token**, it must [validate hello token](active-directory-b2c-reference-tokens.md) tooprove that hello token is authentic and has hello correct claims.</span></span>

<span data-ttu-id="12431-194">我們一定是開啟 toofeedback，以及建議 ！</span><span class="sxs-lookup"><span data-stu-id="12431-194">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="12431-195">如果您有本主題的任何問題，請張貼的堆疊溢位使用 hello 標記['azure-ad b2c 的'](https://stackoverflow.com/questions/tagged/azure-ad-b2c)。</span><span class="sxs-lookup"><span data-stu-id="12431-195">If you have any difficulties with this topic, please post on Stack Overflow using hello tag ['azure-ad-b2c'](https://stackoverflow.com/questions/tagged/azure-ad-b2c).</span></span> <span data-ttu-id="12431-196">功能的要求，將它們加入太[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c)。</span><span class="sxs-lookup"><span data-stu-id="12431-196">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

## <a name="next-steps"></a><span data-ttu-id="12431-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12431-197">Next steps</span></span>

* <span data-ttu-id="12431-198">使用 [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi) 建置 Web API</span><span class="sxs-lookup"><span data-stu-id="12431-198">Build a web API using [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)</span></span>
* <span data-ttu-id="12431-199">使用 [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi) 建置 Web API</span><span class="sxs-lookup"><span data-stu-id="12431-199">Build a web API using [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)</span></span>
