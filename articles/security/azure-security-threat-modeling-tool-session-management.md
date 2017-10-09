---
title: "Azure 管理-Microsoft 威脅模型化工具-aaaSession |Microsoft 文件"
description: "hello 威脅模型化工具中公開的威脅防護功能"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="ea1e5-103">安全性架構︰工作階段管理 | 文章</span><span class="sxs-lookup"><span data-stu-id="ea1e5-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="ea1e5-104">產品/服務</span><span class="sxs-lookup"><span data-stu-id="ea1e5-104">Product/Service</span></span> | <span data-ttu-id="ea1e5-105">文章</span><span class="sxs-lookup"><span data-stu-id="ea1e5-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="ea1e5-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="ea1e5-107">在使用 Azure AD 時以 ADAL 方法實作適當的登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="ea1e5-108">IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="ea1e5-109">為產生的 SaS 權杖使用有限的存留期</span><span class="sxs-lookup"><span data-stu-id="ea1e5-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="ea1e5-110">**Azure Document DB**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="ea1e5-111">為產生的資源權杖使用最短的權杖存留期</span><span class="sxs-lookup"><span data-stu-id="ea1e5-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="ea1e5-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="ea1e5-113">在使用 ADFS 時以 WsFederation 方法實作適當的登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="ea1e5-114">**Identity Server**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="ea1e5-115">在使用 Identity Server 時實作適當的登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="ea1e5-116">**Web 應用程式**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="ea1e5-117">透過 HTTPS 使用的應用程式必須使用安全 Cookie</span><span class="sxs-lookup"><span data-stu-id="ea1e5-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="ea1e5-118">所有 http 型應用程式只應在定義 Cookie 時指定 http</span><span class="sxs-lookup"><span data-stu-id="ea1e5-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="ea1e5-119">避免 ASP.NET 網頁上發生跨網站偽造要求 (CSRF) 攻擊</span><span class="sxs-lookup"><span data-stu-id="ea1e5-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="ea1e5-120">設定工作階段的閒置存留期</span><span class="sxs-lookup"><span data-stu-id="ea1e5-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="ea1e5-121">實作從 hello 應用程式的適當登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="ea1e5-122">**Web API**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="ea1e5-123">避免 ASP.NET Web API 上發生跨網站偽造要求 (CSRF) 攻擊</span><span class="sxs-lookup"><span data-stu-id="ea1e5-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="ea1e5-124"><a id="logout-adal"></a>在使用 Azure AD 時以 ADAL 方法實作適當的登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="ea1e5-125">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-125">Title</span></span>                   | <span data-ttu-id="ea1e5-126">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-127">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-127">**Component**</span></span>               | <span data-ttu-id="ea1e5-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea1e5-128">Azure AD</span></span> | 
| <span data-ttu-id="ea1e5-129">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-129">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-130">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-130">Build</span></span> |  
| <span data-ttu-id="ea1e5-131">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-131">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-132">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-132">Generic</span></span> |
| <span data-ttu-id="ea1e5-133">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-133">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-134">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-134">N/A</span></span>  |
| <span data-ttu-id="ea1e5-135">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-135">**References**</span></span>              | <span data-ttu-id="ea1e5-136">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-136">N/A</span></span>  |
| <span data-ttu-id="ea1e5-137">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-137">**Steps**</span></span> | <span data-ttu-id="ea1e5-138">Hello 應用程式依賴 Azure AD 所發出存取權杖，如果應該呼叫 hello 登出事件處理常式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="ea1e5-139">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="ea1e5-140">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-140">Example</span></span>
<span data-ttu-id="ea1e5-141">它應該也會藉由呼叫 Session.Abandon() 方法終結使用者的工作階段。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="ea1e5-142">下列方法顯示使用者登出的安全實作︰</span><span class="sxs-lookup"><span data-stu-id="ea1e5-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="ea1e5-143"><a id="finite-tokens"></a>為產生的 SaS 權杖使用有限的存留期</span><span class="sxs-lookup"><span data-stu-id="ea1e5-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="ea1e5-144">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-144">Title</span></span>                   | <span data-ttu-id="ea1e5-145">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-146">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-146">**Component**</span></span>               | <span data-ttu-id="ea1e5-147">IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-147">IoT Device</span></span> | 
| <span data-ttu-id="ea1e5-148">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-148">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-149">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-149">Build</span></span> |  
| <span data-ttu-id="ea1e5-150">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-150">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-151">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-151">Generic</span></span> |
| <span data-ttu-id="ea1e5-152">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-152">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-153">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-153">N/A</span></span>  |
| <span data-ttu-id="ea1e5-154">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-154">**References**</span></span>              | <span data-ttu-id="ea1e5-155">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-155">N/A</span></span>  |
| <span data-ttu-id="ea1e5-156">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-156">**Steps**</span></span> | <span data-ttu-id="ea1e5-157">產生驗證 tooAzure IoT 中樞的 SaS 權杖應具有有限到期時間。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="ea1e5-158">保留 hello SaS 權杖存留期 tooa 最小 toolimit hello 一段時間就可以重新執行以防 hello 語彙基元會隨即受到危害。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="ea1e5-159"><a id="resource-tokens"></a>為產生的資源權杖使用最短的權杖存留期</span><span class="sxs-lookup"><span data-stu-id="ea1e5-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="ea1e5-160">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-160">Title</span></span>                   | <span data-ttu-id="ea1e5-161">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-162">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-162">**Component**</span></span>               | <span data-ttu-id="ea1e5-163">Azure Document DB</span><span class="sxs-lookup"><span data-stu-id="ea1e5-163">Azure Document DB</span></span> | 
| <span data-ttu-id="ea1e5-164">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-164">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-165">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-165">Build</span></span> |  
| <span data-ttu-id="ea1e5-166">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-166">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-167">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-167">Generic</span></span> |
| <span data-ttu-id="ea1e5-168">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-168">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-169">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-169">N/A</span></span>  |
| <span data-ttu-id="ea1e5-170">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-170">**References**</span></span>              | <span data-ttu-id="ea1e5-171">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-171">N/A</span></span>  |
| <span data-ttu-id="ea1e5-172">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-172">**Steps**</span></span> | <span data-ttu-id="ea1e5-173">減少 hello timespan 的所需的資源權杖 tooa 最小值。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="ea1e5-174">資源權杖有 1 小時的預設有效時間範圍。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="ea1e5-175"><a id="wsfederation-logout"></a>在使用 ADFS 時以 WsFederation 方法實作適當的登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="ea1e5-176">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-176">Title</span></span>                   | <span data-ttu-id="ea1e5-177">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-178">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-178">**Component**</span></span>               | <span data-ttu-id="ea1e5-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="ea1e5-179">ADFS</span></span> | 
| <span data-ttu-id="ea1e5-180">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-180">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-181">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-181">Build</span></span> |  
| <span data-ttu-id="ea1e5-182">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-182">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-183">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-183">Generic</span></span> |
| <span data-ttu-id="ea1e5-184">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-184">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-185">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-185">N/A</span></span>  |
| <span data-ttu-id="ea1e5-186">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-186">**References**</span></span>              | <span data-ttu-id="ea1e5-187">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-187">N/A</span></span>  |
| <span data-ttu-id="ea1e5-188">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-188">**Steps**</span></span> | <span data-ttu-id="ea1e5-189">如果 hello 應用程式依賴 ADFS 所發出的 STS 權杖，hello 登出事件處理常式應該呼叫 WSFederationAuthenticationModule.FederatedSignOut() 方法 toolog 出 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="ea1e5-190">也 hello 目前工作階段應該予以終結，且應重設並 nullified hello 工作階段語彙基元值。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="ea1e5-191">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="ea1e5-192"><a id="proper-logout"></a>在使用 Identity Server 時實作適當的登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="ea1e5-193">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-193">Title</span></span>                   | <span data-ttu-id="ea1e5-194">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-195">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-195">**Component**</span></span>               | <span data-ttu-id="ea1e5-196">Identity Server</span><span class="sxs-lookup"><span data-stu-id="ea1e5-196">Identity Server</span></span> | 
| <span data-ttu-id="ea1e5-197">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-197">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-198">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-198">Build</span></span> |  
| <span data-ttu-id="ea1e5-199">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-199">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-200">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-200">Generic</span></span> |
| <span data-ttu-id="ea1e5-201">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-201">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-202">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-202">N/A</span></span>  |
| <span data-ttu-id="ea1e5-203">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-203">**References**</span></span>              | [<span data-ttu-id="ea1e5-204">IdentityServer3-同盟登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="ea1e5-205">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-205">**Steps**</span></span> | <span data-ttu-id="ea1e5-206">IdentityServer 支援 hello 能力 toofederate 外部識別提供者。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="ea1e5-207">當使用者登出上游的身分識別提供者時，根據 hello 通訊協定，它可能 tooreceive 通知時可能 hello 使用者登出時。它可讓 IdentityServer toonotify 讓它們也可以登入其用戶端 hello 使用者登出。請檢查 hello hello 實作詳細資料的參考 > 一節中的 hello 文件集。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="ea1e5-208"><a id="https-secure-cookies"></a>透過 HTTPS 使用的應用程式必須使用安全 Cookie</span><span class="sxs-lookup"><span data-stu-id="ea1e5-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="ea1e5-209">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-209">Title</span></span>                   | <span data-ttu-id="ea1e5-210">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-211">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-211">**Component**</span></span>               | <span data-ttu-id="ea1e5-212">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-212">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-213">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-213">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-214">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-214">Build</span></span> |  
| <span data-ttu-id="ea1e5-215">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-215">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-216">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-216">Generic</span></span> |
| <span data-ttu-id="ea1e5-217">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-217">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="ea1e5-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="ea1e5-219">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-219">**References**</span></span>              | <span data-ttu-id="ea1e5-220">[httpCookies 元素 (ASP.NET 設定結構描述)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx)、[HttpCookie.Secure 屬性](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="ea1e5-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="ea1e5-221">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-221">**Steps**</span></span> | <span data-ttu-id="ea1e5-222">Cookie 通常是只會存取 toohello 才權杖的網域。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="ea1e5-223">不幸的是，hello 的 「 網域 」 的定義不包含 hello 通訊協定，因此透過 HTTP 存取是透過 HTTPS 的 cookie。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="ea1e5-224">hello 「 安全 」 屬性會指出 toohello hello cookie 的瀏覽器只應該可以使用透過 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="ea1e5-225">請透過 HTTPS 設定的所有 cookie 都使用 hello**安全**屬性。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="ea1e5-226">hello 需求可以藉由設定 hello requireSSL 屬性 tootrue 強制 hello web.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="ea1e5-227">它是 hello 慣用的方法，因為它將會強制執行 hello**安全**屬性的所有目前和未來 cookie hello 需要 toomake 沒有任何額外的程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="ea1e5-228">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="ea1e5-229">即使 HTTP 是使用的 tooaccess hello 應用程式會強制執行 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="ea1e5-230">如果使用 HTTP tooaccess hello 應用程式，並且讓 hello hello 應用程式因為 hello cookie 會以 hello 安全屬性和 hello 瀏覽器設定不會傳送它們的設定符號 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="ea1e5-231">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-231">Title</span></span>                   | <span data-ttu-id="ea1e5-232">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-233">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-233">**Component**</span></span>               | <span data-ttu-id="ea1e5-234">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-234">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-235">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-235">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-236">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-236">Build</span></span> |  
| <span data-ttu-id="ea1e5-237">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-237">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-238">Web Form、MVC5</span><span class="sxs-lookup"><span data-stu-id="ea1e5-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="ea1e5-239">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-239">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="ea1e5-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="ea1e5-241">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-241">**References**</span></span>              | <span data-ttu-id="ea1e5-242">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-242">N/A</span></span>  |
| <span data-ttu-id="ea1e5-243">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-243">**Steps**</span></span> | <span data-ttu-id="ea1e5-244">設定中的 requireSSL tooTrue 當 hello web 應用程式是 hello 信賴憑證者的合作對象，而且 hello IdP ADFS 伺服器時，可以設定 hello FedAuth 語彙基元的安全屬性`system.identityModel.services`web.config 的區段：</span><span class="sxs-lookup"><span data-stu-id="ea1e5-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="ea1e5-245">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="ea1e5-246"><a id="cookie-definition"></a>所有 http 型應用程式只應在定義 Cookie 時指定 http</span><span class="sxs-lookup"><span data-stu-id="ea1e5-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="ea1e5-247">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-247">Title</span></span>                   | <span data-ttu-id="ea1e5-248">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-249">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-249">**Component**</span></span>               | <span data-ttu-id="ea1e5-250">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-250">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-251">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-251">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-252">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-252">Build</span></span> |  
| <span data-ttu-id="ea1e5-253">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-253">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-254">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-254">Generic</span></span> |
| <span data-ttu-id="ea1e5-255">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-255">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-256">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-256">N/A</span></span>  |
| <span data-ttu-id="ea1e5-257">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-257">**References**</span></span>              | [<span data-ttu-id="ea1e5-258">安全 Cookie 屬性</span><span class="sxs-lookup"><span data-stu-id="ea1e5-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="ea1e5-259">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-259">**Steps**</span></span> | <span data-ttu-id="ea1e5-260">toomitigate hello 風險資訊洩露跨網站指令碼 (XSS) 攻擊的新屬性-httpOnly-已導入了的 toocookies 和支援的所有主要瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="ea1e5-261">hello 屬性會指定 cookie 不是可透過指令碼存取。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="ea1e5-262">藉由使用 HttpOnly cookie，web 應用程式會降低 hello 可能性 hello cookie 中包含機密資訊可以透過指令碼遭竊，並且傳送 tooan 攻擊者的網站。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="ea1e5-263">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-263">Example</span></span>
<span data-ttu-id="ea1e5-264">所有以 HTTP 為基礎的應用程式使用 cookie 應該在 hello cookie 定義中，指定 HttpOnly 藉由實作下列 web.config 中的組態：</span><span class="sxs-lookup"><span data-stu-id="ea1e5-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="ea1e5-265">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-265">Title</span></span>                   | <span data-ttu-id="ea1e5-266">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-267">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-267">**Component**</span></span>               | <span data-ttu-id="ea1e5-268">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-268">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-269">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-269">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-270">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-270">Build</span></span> |  
| <span data-ttu-id="ea1e5-271">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-271">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-272">Web Form</span><span class="sxs-lookup"><span data-stu-id="ea1e5-272">Web Forms</span></span> |
| <span data-ttu-id="ea1e5-273">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-273">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-274">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-274">N/A</span></span>  |
| <span data-ttu-id="ea1e5-275">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-275">**References**</span></span>              | [<span data-ttu-id="ea1e5-276">FormsAuthentication.RequireSSL 屬性</span><span class="sxs-lookup"><span data-stu-id="ea1e5-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="ea1e5-277">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-277">**Steps**</span></span> | <span data-ttu-id="ea1e5-278">hello RequireSSL 屬性值是使用 hello requireSSL 屬性 hello 組態項目之 hello ASP.NET 應用程式的組態檔中設定。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="ea1e5-279">您可以指定 hello Web.config 檔案中的 ASP.NET 應用程式是否 SSL （安全通訊端層） 是必要的 tooreturn hello 表單驗證 cookie toohello 伺服器設定 hello requireSSL 屬性。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="ea1e5-280">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-280">Example</span></span> 
<span data-ttu-id="ea1e5-281">hello 下列程式碼範例會設定 hello requireSSL 屬性 hello Web.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="ea1e5-282">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-282">Title</span></span>                   | <span data-ttu-id="ea1e5-283">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-284">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-284">**Component**</span></span>               | <span data-ttu-id="ea1e5-285">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-285">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-286">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-286">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-287">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-287">Build</span></span> |  
| <span data-ttu-id="ea1e5-288">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-288">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="ea1e5-289">MVC5</span></span> |
| <span data-ttu-id="ea1e5-290">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-290">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="ea1e5-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="ea1e5-292">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-292">**References**</span></span>              | [<span data-ttu-id="ea1e5-293">Windows Identity Foundation (WIF) 組態 - 單元二</span><span class="sxs-lookup"><span data-stu-id="ea1e5-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="ea1e5-294">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-294">**Steps**</span></span> | <span data-ttu-id="ea1e5-295">FedAuth cookie 的 tooset httpOnly 屬性 hideFromCsript 屬性值應該設定 tooTrue。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="ea1e5-296">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-296">Example</span></span>
<span data-ttu-id="ea1e5-297">下列組態會顯示 hello 正確的組態：</span><span class="sxs-lookup"><span data-stu-id="ea1e5-297">Following configuration shows hello correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="ea1e5-298"><a id="csrf-asp"></a>避免 ASP.NET 網頁上發生跨網站偽造要求 (CSRF) 攻擊</span><span class="sxs-lookup"><span data-stu-id="ea1e5-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="ea1e5-299">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-299">Title</span></span>                   | <span data-ttu-id="ea1e5-300">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-301">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-301">**Component**</span></span>               | <span data-ttu-id="ea1e5-302">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-302">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-303">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-303">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-304">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-304">Build</span></span> |  
| <span data-ttu-id="ea1e5-305">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-305">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-306">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-306">Generic</span></span> |
| <span data-ttu-id="ea1e5-307">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-307">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-308">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-308">N/A</span></span>  |
| <span data-ttu-id="ea1e5-309">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-309">**References**</span></span>              | <span data-ttu-id="ea1e5-310">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-310">N/A</span></span>  |
| <span data-ttu-id="ea1e5-311">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-311">**Steps**</span></span> | <span data-ttu-id="ea1e5-312">跨站台要求偽造 （CSRF 或 XSRF） 是一種攻擊，攻擊者可以按照 hello 安全性內容中的網站上不同的使用者建立之工作階段的動作。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="ea1e5-313">hello 目標 toomodify 或刪除的內容，如果目標的網站 hello 完全依賴工作階段 cookie tooauthenticate 接收的要求。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="ea1e5-314">攻擊者取得不同使用者的瀏覽器 tooload 命令使用的 URL 從易受攻擊的站台所在 hello 使用者已經登入，以利用這項弱點。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="ea1e5-315">有很多種，例如藉由主控不同的網站，載入資源從 hello 弱點的伺服器或取得 hello 使用者 tooclick 連結攻擊者 toodo 的。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="ea1e5-316">如果 hello 伺服器傳送其他語彙基元 toohello 用戶端，需要 hello 用戶端 tooinclude 中所有未來的要求，該語彙基元，並確認所有未來的要求，包括相關 toohello 目前工作階段，例如由語彙基元，就可以避免 hello 攻擊使用 ASP.NET AntiForgeryToken hello 或 ViewState。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="ea1e5-317">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-317">Title</span></span>                   | <span data-ttu-id="ea1e5-318">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-319">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-319">**Component**</span></span>               | <span data-ttu-id="ea1e5-320">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-320">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-321">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-321">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-322">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-322">Build</span></span> |  
| <span data-ttu-id="ea1e5-323">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-323">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-324">MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="ea1e5-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="ea1e5-325">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-325">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-326">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-326">N/A</span></span>  |
| <span data-ttu-id="ea1e5-327">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-327">**References**</span></span>              | [<span data-ttu-id="ea1e5-328">在 ASP.NET MVC 和網頁中防止 XSRF/CSRF</span><span class="sxs-lookup"><span data-stu-id="ea1e5-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="ea1e5-329">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-329">**Steps**</span></span> | <span data-ttu-id="ea1e5-330">反 CSRF 和 ASP.NET MVC form-使用 hello`AntiForgeryToken`檢視上的協助程式方法; put `Html.AntiForgeryToken()` hello 表單，例如，</span><span class="sxs-lookup"><span data-stu-id="ea1e5-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="ea1e5-331">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="ea1e5-332">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="ea1e5-333">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-333">Example</span></span>
<span data-ttu-id="ea1e5-334">在 hello 相同的時間，Html.AntiForgeryToken() 提供 hello 訪客 cookie 呼叫 __RequestVerificationToken，以相同的值 hello 隨機的 hidden 值如上所示為 hello。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="ea1e5-335">接下來，toovalidate 連入的表單張貼加入 hello [ValidateAntiForgeryToken] 篩選 toohello 目標動作方法。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="ea1e5-336">例如：</span><span class="sxs-lookup"><span data-stu-id="ea1e5-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="ea1e5-337">授權篩選會確認︰</span><span class="sxs-lookup"><span data-stu-id="ea1e5-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="ea1e5-338">hello 連入要求具有稱為 __RequestVerificationToken cookie</span><span class="sxs-lookup"><span data-stu-id="ea1e5-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="ea1e5-339">hello 傳入的要求有`Request.Form`呼叫 __RequestVerificationToken 的項目</span><span class="sxs-lookup"><span data-stu-id="ea1e5-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="ea1e5-340">這些 cookie 和`Request.Form`假設所有的值符合目前、 hello 要求會透過正常。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="ea1e5-341">但如果沒有，則授權會失敗並出現訊息「未提供必要的防偽權杖或權杖無效」。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="ea1e5-342">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-342">Example</span></span>
<span data-ttu-id="ea1e5-343">反 CSRF 和 AJAX: hello 表單語彙基元可能 AJAX 要求的問題，因為 AJAX 要求可能會傳送 JSON 資料，HTML 表單資料。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="ea1e5-344">一個解決方案是自訂的 HTTP 標頭中的 toosend hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="ea1e5-345">hello 下列程式碼會使用 Razor 語法 toogenerate hello token，然後新增 hello 語彙基元 tooan AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="ea1e5-346">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-346">Example</span></span>
<span data-ttu-id="ea1e5-347">當您處理 hello 要求時，請從 hello 要求標頭中擷取 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="ea1e5-348">然後呼叫 hello AntiForgery.Validate 方法 toovalidate hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="ea1e5-349">hello Validate 方法會擲回例外狀況，如果 hello 語彙基元無效。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="ea1e5-350">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-350">Title</span></span>                   | <span data-ttu-id="ea1e5-351">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-352">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-352">**Component**</span></span>               | <span data-ttu-id="ea1e5-353">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-353">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-354">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-354">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-355">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-355">Build</span></span> |  
| <span data-ttu-id="ea1e5-356">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-356">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-357">Web Form</span><span class="sxs-lookup"><span data-stu-id="ea1e5-357">Web Forms</span></span> |
| <span data-ttu-id="ea1e5-358">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-358">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-359">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-359">N/A</span></span>  |
| <span data-ttu-id="ea1e5-360">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-360">**References**</span></span>              | [<span data-ttu-id="ea1e5-361">需要利用的 ASP.NET 內建功能 tooFend 關閉 Web 攻擊</span><span class="sxs-lookup"><span data-stu-id="ea1e5-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="ea1e5-362">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-362">**Steps**</span></span> | <span data-ttu-id="ea1e5-363">藉由設定 ViewStateUserKey tooa 隨機字串而異的每個使用者-使用者識別碼，就可以緩解 CSRF 攻擊 WebForm 基礎應用程式中的，或更棒的是，工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="ea1e5-364">基於諸多技術和社交方面的原因，工作階段識別碼會比較適合，因為工作階段識別碼無法預料、會逾時，而且會隨每個使用者而有所不同。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="ea1e5-365">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-365">Example</span></span>
<span data-ttu-id="ea1e5-366">以下是您在所有的網頁需要 toohave hello 程式碼：</span><span class="sxs-lookup"><span data-stu-id="ea1e5-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="ea1e5-367"><a id="inactivity-lifetime"></a>設定工作階段的閒置存留期</span><span class="sxs-lookup"><span data-stu-id="ea1e5-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="ea1e5-368">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-368">Title</span></span>                   | <span data-ttu-id="ea1e5-369">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-370">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-370">**Component**</span></span>               | <span data-ttu-id="ea1e5-371">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-371">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-372">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-372">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-373">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-373">Build</span></span> |  
| <span data-ttu-id="ea1e5-374">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-374">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-375">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-375">Generic</span></span> |
| <span data-ttu-id="ea1e5-376">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-376">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-377">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-377">N/A</span></span>  |
| <span data-ttu-id="ea1e5-378">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-378">**References**</span></span>              | <span data-ttu-id="ea1e5-379">[HttpSessionState.Timeout 屬性](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="ea1e5-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="ea1e5-380">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-380">**Steps**</span></span> | <span data-ttu-id="ea1e5-381">工作階段逾時表示 hello 事件時所發生使用者不會執行任何動作在網站上在間隔內 （web 伺服器所定義）。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="ea1e5-382">hello 事件，在伺服器端上的，變更 hello 使用者工作階段 too'invalid hello 狀態 ' （例如 「 不使用不再 」），並指示 hello web 伺服器 toodestroy 它 （刪除到它所包含的所有資料）。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="ea1e5-383">hello 下列程式碼範例會設定 hello 逾時工作階段屬性 too15 分鐘數 hello Web.config 檔案中。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="ea1e5-384">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-384">Example</span></span>
<span data-ttu-id="ea1e5-385">``\`XML 程式碼 <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span><span class="sxs-lookup"><span data-stu-id="ea1e5-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="ea1e5-386">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-386">Title</span></span>                   | <span data-ttu-id="ea1e5-387">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-388">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-388">**Component**</span></span>               | <span data-ttu-id="ea1e5-389">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-389">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-390">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-390">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-391">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-391">Build</span></span> |  
| <span data-ttu-id="ea1e5-392">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-392">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-393">Web Form</span><span class="sxs-lookup"><span data-stu-id="ea1e5-393">Web Forms</span></span> |
| <span data-ttu-id="ea1e5-394">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-394">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-395">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-395">N/A</span></span>  |
| <span data-ttu-id="ea1e5-396">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-396">**References**</span></span>              | <span data-ttu-id="ea1e5-397">[用於驗證的表單元素 (ASP.NET 設定結構描述)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="ea1e5-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="ea1e5-398">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-398">**Steps**</span></span> | <span data-ttu-id="ea1e5-399">設定表單驗證票證 cookie 逾時 too15 hello 分鐘</span><span class="sxs-lookup"><span data-stu-id="ea1e5-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="ea1e5-400">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-400">Example</span></span>
<span data-ttu-id="ea1e5-401">``\`XML 程式碼 <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="ea1e5-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="ea1e5-402">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-402">Example</span></span>
<span data-ttu-id="ea1e5-403">也 hello too15 應該設定發行 SAML 宣告權杖的存留期的 ADFS 分鐘，執行下列 powershell 命令 hello ADFS 伺服器上的 hello:</span><span class="sxs-lookup"><span data-stu-id="ea1e5-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="ea1e5-404"><a id="proper-app-logout"></a>實作從 hello 應用程式的適當登出</span><span class="sxs-lookup"><span data-stu-id="ea1e5-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="ea1e5-405">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-405">Title</span></span>                   | <span data-ttu-id="ea1e5-406">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-407">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-407">**Component**</span></span>               | <span data-ttu-id="ea1e5-408">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea1e5-408">Web Application</span></span> | 
| <span data-ttu-id="ea1e5-409">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-409">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-410">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-410">Build</span></span> |  
| <span data-ttu-id="ea1e5-411">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-411">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-412">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-412">Generic</span></span> |
| <span data-ttu-id="ea1e5-413">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-413">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-414">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-414">N/A</span></span>  |
| <span data-ttu-id="ea1e5-415">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-415">**References**</span></span>              | <span data-ttu-id="ea1e5-416">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-416">N/A</span></span>  |
| <span data-ttu-id="ea1e5-417">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-417">**Steps**</span></span> | <span data-ttu-id="ea1e5-418">當使用者按下登出按鈕時執行適當登出從 hello 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="ea1e5-419">在登出時，應用程式應終結使用者的工作階段，同時重設工作階段 Cookie 值並讓其變成空值，以及重設驗證 cookie 值並讓其變成空值。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="ea1e5-420">此外，當多個工作階段繫結的 tooa 單一使用者身分識別時，它們必須共同結束 hello 伺服器端逾時或登出。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="ea1e5-421">最後，請確定每個頁面都可使用登出功能。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="ea1e5-422"><a id="csrf-api"></a>避免 ASP.NET Web API 上發生跨網站偽造要求 (CSRF) 攻擊</span><span class="sxs-lookup"><span data-stu-id="ea1e5-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="ea1e5-423">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-423">Title</span></span>                   | <span data-ttu-id="ea1e5-424">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-425">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-425">**Component**</span></span>               | <span data-ttu-id="ea1e5-426">Web API</span><span class="sxs-lookup"><span data-stu-id="ea1e5-426">Web API</span></span> | 
| <span data-ttu-id="ea1e5-427">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-427">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-428">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-428">Build</span></span> |  
| <span data-ttu-id="ea1e5-429">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-429">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-430">泛型</span><span class="sxs-lookup"><span data-stu-id="ea1e5-430">Generic</span></span> |
| <span data-ttu-id="ea1e5-431">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-431">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-432">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-432">N/A</span></span>  |
| <span data-ttu-id="ea1e5-433">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-433">**References**</span></span>              | <span data-ttu-id="ea1e5-434">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-434">N/A</span></span>  |
| <span data-ttu-id="ea1e5-435">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-435">**Steps**</span></span> | <span data-ttu-id="ea1e5-436">跨站台要求偽造 （CSRF 或 XSRF） 是一種攻擊，攻擊者可以按照 hello 安全性內容中的網站上不同的使用者建立之工作階段的動作。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="ea1e5-437">hello 目標 toomodify 或刪除的內容，如果目標的網站 hello 完全依賴工作階段 cookie tooauthenticate 接收的要求。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="ea1e5-438">攻擊者取得不同使用者的瀏覽器 tooload 命令使用的 URL 從易受攻擊的站台所在 hello 使用者已經登入，以利用這項弱點。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="ea1e5-439">有很多種，例如藉由主控不同的網站，載入資源從 hello 弱點的伺服器或取得 hello 使用者 tooclick 連結攻擊者 toodo 的。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="ea1e5-440">如果 hello 伺服器傳送其他語彙基元 toohello 用戶端，需要 hello 用戶端 tooinclude 中所有未來的要求，該語彙基元，並確認所有未來的要求，包括相關 toohello 目前工作階段，例如由語彙基元，就可以避免 hello 攻擊使用 ASP.NET AntiForgeryToken hello 或 ViewState。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="ea1e5-441">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-441">Title</span></span>                   | <span data-ttu-id="ea1e5-442">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-443">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-443">**Component**</span></span>               | <span data-ttu-id="ea1e5-444">Web API</span><span class="sxs-lookup"><span data-stu-id="ea1e5-444">Web API</span></span> | 
| <span data-ttu-id="ea1e5-445">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-445">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-446">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-446">Build</span></span> |  
| <span data-ttu-id="ea1e5-447">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-447">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-448">MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="ea1e5-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="ea1e5-449">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-449">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-450">N/A</span><span class="sxs-lookup"><span data-stu-id="ea1e5-450">N/A</span></span>  |
| <span data-ttu-id="ea1e5-451">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-451">**References**</span></span>              | [<span data-ttu-id="ea1e5-452">避免 ASP.NET Web API 中發生跨網站偽造要求 (CSRF) 攻擊</span><span class="sxs-lookup"><span data-stu-id="ea1e5-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="ea1e5-453">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-453">**Steps**</span></span> | <span data-ttu-id="ea1e5-454">反 CSRF 和 AJAX: hello 表單語彙基元可能 AJAX 要求的問題，因為 AJAX 要求可能會傳送 JSON 資料，HTML 表單資料。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="ea1e5-455">一個解決方案是自訂的 HTTP 標頭中的 toosend hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="ea1e5-456">hello 下列程式碼會使用 Razor 語法 toogenerate hello token，然後新增 hello 語彙基元 tooan AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="ea1e5-457">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="ea1e5-458">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-458">Example</span></span>
<span data-ttu-id="ea1e5-459">當您處理 hello 要求時，請從 hello 要求標頭中擷取 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="ea1e5-460">然後呼叫 hello AntiForgery.Validate 方法 toovalidate hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="ea1e5-461">hello Validate 方法會擲回例外狀況，如果 hello 語彙基元無效。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="ea1e5-462">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-462">Example</span></span>
<span data-ttu-id="ea1e5-463">反 CSRF 和 ASP.NET MVC form-使用 hello AntiForgeryToken 檢視; 上的協助程式方法例如，將 Html.AntiForgeryToken() 放入 hello 表單</span><span class="sxs-lookup"><span data-stu-id="ea1e5-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="ea1e5-464">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-464">Example</span></span>
<span data-ttu-id="ea1e5-465">hello 上述範例中會輸出 hello 下列類似：</span><span class="sxs-lookup"><span data-stu-id="ea1e5-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="ea1e5-466">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-466">Example</span></span>
<span data-ttu-id="ea1e5-467">在 hello 相同的時間，Html.AntiForgeryToken() 提供 hello 訪客 cookie 呼叫 __RequestVerificationToken，以相同的值 hello 隨機的 hidden 值如上所示為 hello。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="ea1e5-468">接下來，toovalidate 連入的表單張貼加入 hello [ValidateAntiForgeryToken] 篩選 toohello 目標動作方法。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="ea1e5-469">例如：</span><span class="sxs-lookup"><span data-stu-id="ea1e5-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="ea1e5-470">授權篩選會確認︰</span><span class="sxs-lookup"><span data-stu-id="ea1e5-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="ea1e5-471">hello 連入要求具有稱為 __RequestVerificationToken cookie</span><span class="sxs-lookup"><span data-stu-id="ea1e5-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="ea1e5-472">hello 傳入的要求有`Request.Form`呼叫 __RequestVerificationToken 的項目</span><span class="sxs-lookup"><span data-stu-id="ea1e5-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="ea1e5-473">這些 cookie 和`Request.Form`假設所有的值符合目前、 hello 要求會透過正常。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="ea1e5-474">但如果沒有，則授權會失敗並出現訊息「未提供必要的防偽權杖或權杖無效」。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="ea1e5-475">Title</span><span class="sxs-lookup"><span data-stu-id="ea1e5-475">Title</span></span>                   | <span data-ttu-id="ea1e5-476">詳細資料</span><span class="sxs-lookup"><span data-stu-id="ea1e5-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="ea1e5-477">**元件**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-477">**Component**</span></span>               | <span data-ttu-id="ea1e5-478">Web API</span><span class="sxs-lookup"><span data-stu-id="ea1e5-478">Web API</span></span> | 
| <span data-ttu-id="ea1e5-479">**SDL 階段**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-479">**SDL Phase**</span></span>               | <span data-ttu-id="ea1e5-480">建置</span><span class="sxs-lookup"><span data-stu-id="ea1e5-480">Build</span></span> |  
| <span data-ttu-id="ea1e5-481">**適用的技術**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-481">**Applicable Technologies**</span></span> | <span data-ttu-id="ea1e5-482">MVC5、MVC6</span><span class="sxs-lookup"><span data-stu-id="ea1e5-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="ea1e5-483">**屬性**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-483">**Attributes**</span></span>              | <span data-ttu-id="ea1e5-484">識別提供者 - ADFS、識別提供者 - Azure AD</span><span class="sxs-lookup"><span data-stu-id="ea1e5-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="ea1e5-485">**參考**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-485">**References**</span></span>              | [<span data-ttu-id="ea1e5-486">在 ASP.NET Web API 2.2 中使用個別帳戶和本機登入保護 Web API</span><span class="sxs-lookup"><span data-stu-id="ea1e5-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="ea1e5-487">**步驟**</span><span class="sxs-lookup"><span data-stu-id="ea1e5-487">**Steps**</span></span> | <span data-ttu-id="ea1e5-488">如果 hello Web API 受到使用 OAuth 2.0，則預期持有人權杖授權要求標頭和授與存取 toohello 要求中，只有當 hello 權杖是有效的。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="ea1e5-489">不同於以 cookie 為基礎的驗證，瀏覽器不要附加 hello 持有人權杖 toorequests。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="ea1e5-490">hello 要求用戶端必須 tooexplicitly 附加 hello 要求標頭中的 hello 持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="ea1e5-491">因此，對於使用 OAuth 2.0 來保護的 ASP.NET Web API，會將持有人權杖視為 CSRF 攻擊的防禦手段。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="ea1e5-492">請注意，是否 hello MVC 部分 hello 應用程式會使用表單驗證 (也就是使用 cookie)，防偽語彙基元會有 toobe hello MVC web 應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="ea1e5-493">範例</span><span class="sxs-lookup"><span data-stu-id="ea1e5-493">Example</span></span>
<span data-ttu-id="ea1e5-494">hello Web API 有 toobe 通知 toorely 僅限持有者權杖，而不是在 cookie。</span><span class="sxs-lookup"><span data-stu-id="ea1e5-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="ea1e5-495">由下列組態中的 hello`WebApiConfig.Register`方法: '' C-sharp 程式碼設定。SuppressDefaultHostAuthentication();組態。Filters.Add (新 HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="ea1e5-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
