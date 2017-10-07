---
title: "hello Azure Active Directory v2.0 端點 aaaApp 類型 |Microsoft 文件"
description: "hello 類型的應用程式和 hello Azure Active Directory v2.0 端點所支援的案例。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 494a06b8-0f9b-44e1-a7a2-d728cf2077ae
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: db95c88d6865abac8ce80378ccd6b63cb38e0a01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-types-for-hello-azure-active-directory-v20-endpoint"></a><span data-ttu-id="d6072-103">Hello Azure Active Directory v2.0 端點的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="d6072-103">App types for hello Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="d6072-104">hello Azure Active Directory (Azure AD) v2.0 端點支援驗證的各種不同的現代化應用程式架構，全部都根據業界標準通訊協定[OAuth 2.0 或 OpenID Connect](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-104">hello Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="d6072-105">本文說明 hello 種您可以使用 Azure AD v2.0，不論您偏好的語言或平台建置的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d6072-105">This article describes hello types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="d6072-106">hello 這篇文章中的資訊是您了解高階案例才能設計的 toohelp[開始 hello 程式碼的使用](active-directory-appmodel-v2-overview.md#getting-started)。</span><span class="sxs-lookup"><span data-stu-id="d6072-106">hello information in this article is designed toohelp you understand high-level scenarios before you [start working with hello code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="d6072-107">hello v2.0 端點不支援所有的 Azure Active Directory 的案例和功能。</span><span class="sxs-lookup"><span data-stu-id="d6072-107">hello v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="d6072-108">toodetermine 是否應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-108">toodetermine whether you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="hello-basics"></a><span data-ttu-id="d6072-109">hello 基本概念</span><span class="sxs-lookup"><span data-stu-id="d6072-109">hello basics</span></span>
<span data-ttu-id="d6072-110">您必須註冊每個應用程式中，使用 hello v2.0 端點 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="d6072-110">You must register each app that uses hello v2.0 endpoint in hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="d6072-111">hello 應用程式登錄程序會收集，並將您的應用程式的這些值：</span><span class="sxs-lookup"><span data-stu-id="d6072-111">hello app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="d6072-112">可唯一識別應用程式的「應用程式識別碼」</span><span class="sxs-lookup"><span data-stu-id="d6072-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="d6072-113">A**重新導向 URI** ，您可以使用 toodirect 回應後 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="d6072-113">A **Redirect URI** that you can use toodirect responses back tooyour app</span></span>
* <span data-ttu-id="d6072-114">一些其他案例特定值</span><span class="sxs-lookup"><span data-stu-id="d6072-114">A few other scenario-specific values</span></span>

<span data-ttu-id="d6072-115">如需詳細資訊，了解如何太[註冊應用程式](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-115">For details, learn how too[register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="d6072-116">Hello 應用程式註冊之後，hello 應用程式將會傳送要求 Azure AD toohello v2.0 端點通訊與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d6072-116">After hello app is registered, hello app communicates with Azure AD by sending requests toohello Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="d6072-117">我們提供開放原始碼架構和處理這些要求的 hello 詳細資料的程式庫。</span><span class="sxs-lookup"><span data-stu-id="d6072-117">We provide open-source frameworks and libraries that handle hello details of these requests.</span></span> <span data-ttu-id="d6072-118">您也可以 hello 選項 tooimplement hello 驗證邏輯自行建立要求 toothese 端點：</span><span class="sxs-lookup"><span data-stu-id="d6072-118">You also have hello option tooimplement hello authentication logic yourself by creating requests toothese endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries toolink too-->

## <a name="web-apps"></a><span data-ttu-id="d6072-119">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d6072-119">Web apps</span></span>
<span data-ttu-id="d6072-120">針對 web 應用程式 （.NET、 PHP、 Java、 Ruby、 Python、 節點） 的 hello 透過瀏覽器的使用者存取，您可以使用[OpenID Connect](active-directory-v2-protocols.md)使用者登入。</span><span class="sxs-lookup"><span data-stu-id="d6072-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that hello user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="d6072-121">在 OpenID Connect，hello web 應用程式接收的 ID 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="d6072-121">In OpenID Connect, hello web app receives an ID token.</span></span> <span data-ttu-id="d6072-122">ID 權杖是安全性權杖驗證 hello 使用者的身分識別，並提供 hello 形式的宣告中的 hello 使用者的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="d6072-122">An ID token is a security token that verifies hello user's identity and provides information about hello user in hello form of claims:</span></span>

```
// Partial raw ID token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded ID token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

<span data-ttu-id="d6072-123">您可以了解的權杖與宣告的 hello 可用 tooan 應用程式的所有 hello 類型[v2.0 權杖參考](active-directory-v2-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-123">You can learn about all hello types of tokens and claims that are available tooan app in hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="d6072-124">在 web 伺服器應用程式，hello 登入驗證流程會採用下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="d6072-124">In web server apps, hello sign-in authentication flow takes these high-level steps:</span></span>

![Web 應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="d6072-126">您可以使用收到來自 hello v2.0 端點公開簽署金鑰驗證 hello 的 ID 語彙基元，以確保 hello 使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="d6072-126">You can ensure hello user's identity by validating hello ID token with a public signing key that is received from hello v2.0 endpoint.</span></span> <span data-ttu-id="d6072-127">已設定的工作階段 cookie，可能會在後續頁面要求上的使用的 tooidentify hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="d6072-127">A session cookie is set, which can be used tooidentify hello user on subsequent page requests.</span></span>

<span data-ttu-id="d6072-128">toosee 此案例中的動作，再試一次一個 hello web 應用程式登入程式碼範例中我們 v2.0[入門](active-directory-appmodel-v2-overview.md#getting-started)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d6072-128">toosee this scenario in action, try one of hello web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="d6072-129">此外 toosimple 登入，web 伺服器應用程式可能需要 tooaccess 另一個 web 服務，例如 REST API。</span><span class="sxs-lookup"><span data-stu-id="d6072-129">In addition toosimple sign-in, a web server app might need tooaccess another web service, such as a REST API.</span></span> <span data-ttu-id="d6072-130">在此情況下，hello web 伺服器應用程式會結合 OpenID Connect 和 OAuth 2.0 資料流程，使用 hello [OAuth 2.0 授權碼流程](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-130">In this case, hello web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="d6072-131">如需有關此案例的詳細資訊，請參閱[開始使用 Web 應用程式和 Web API](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="d6072-132">Web API</span><span class="sxs-lookup"><span data-stu-id="d6072-132">Web APIs</span></span>
<span data-ttu-id="d6072-133">您可以使用 hello v2.0 端點 toosecure web 服務，例如您的應用程式 RESTful Web API。</span><span class="sxs-lookup"><span data-stu-id="d6072-133">You can use hello v2.0 endpoint toosecure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="d6072-134">而不是 ID 語彙基元和工作階段 cookie，Web API 所使用的 OAuth 2.0 存取權杖 toosecure 其資料和 tooauthenticate 連入要求。</span><span class="sxs-lookup"><span data-stu-id="d6072-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token toosecure its data and tooauthenticate incoming requests.</span></span> <span data-ttu-id="d6072-135">hello Web api 的呼叫端將附加 hello 的 HTTP 要求，就像這樣的授權標頭中的存取權杖：</span><span class="sxs-lookup"><span data-stu-id="d6072-135">hello caller of a Web API appends an access token in hello authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="d6072-136">hello Web API 會使用有關 hello 呼叫端被編碼 hello 存取權杖中的宣告中的 hello 存取語彙基元 tooverify hello API 呼叫者的身分識別與 tooextract 資訊。</span><span class="sxs-lookup"><span data-stu-id="d6072-136">hello Web API uses hello access token tooverify hello API caller's identity and tooextract information about hello caller from claims that are encoded in hello access token.</span></span> <span data-ttu-id="d6072-137">toolearn hello 類型的權杖與宣告的可用 tooan 應用程式，請參閱 hello [v2.0 權杖參考](active-directory-v2-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-137">toolearn about all hello types of tokens and claims that are available tooan app, see hello [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="d6072-138">Web API 可以提供使用者 hello 電源 tooopt 或退出特有的功能或資料所公開的權限，也稱為[範圍](active-directory-v2-scopes.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-138">A Web API can give users hello power tooopt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="d6072-139">呼叫應用程式 tooacquire 權限 tooa 範圍，hello 使用者必須同意 toohello 範圍流程期間。</span><span class="sxs-lookup"><span data-stu-id="d6072-139">For a calling app tooacquire permission tooa scope, hello user must consent toohello scope during a flow.</span></span> <span data-ttu-id="d6072-140">hello v2.0 端點 hello 使用者要求權限，而且然後權限中記錄所有存取權杖 Web 應用程式開發介面會接收該 hello。</span><span class="sxs-lookup"><span data-stu-id="d6072-140">hello v2.0 endpoint asks hello user for permission, and then records permissions in all access tokens that hello Web API receives.</span></span> <span data-ttu-id="d6072-141">hello Web API 驗證 hello 存取權杖，它在每個呼叫上接收及執行授權檢查。</span><span class="sxs-lookup"><span data-stu-id="d6072-141">hello Web API validates hello access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="d6072-142">Web API 可以從所有類型的應用程式接收存取權杖，包括 Web 伺服器應用程式、傳統型應用程式和行動應用程式、單頁應用程式、伺服器端精靈，甚至是其他的 Web API。</span><span class="sxs-lookup"><span data-stu-id="d6072-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="d6072-143">Web API 的 hello 高階流程看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="d6072-143">hello high-level flow for a Web API looks like this:</span></span>

![Web API 驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="d6072-145">toolearn 如何 toosecure Web API 使用 OAuth2 存取權杖，簽出 hello Web API 的程式碼範例中我們[入門](active-directory-appmodel-v2-overview.md#getting-started)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d6072-145">toolearn how toosecure a Web API by using OAuth2 access tokens, check out hello Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="d6072-146">在許多情況下，web 應用程式開發介面，也需要 toomake 輸出 tooother 下游 web Api 受到 Azure Active Directory 的要求。</span><span class="sxs-lookup"><span data-stu-id="d6072-146">In many cases, web APIs also need toomake outbound requests tooother downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="d6072-147">toodo，web Api 可以利用 Azure AD 的**上代表的**流程，可讓 hello web API tooexchange 另一個用於輸出要求存取權杖 toobe 的傳入存取權杖。</span><span class="sxs-lookup"><span data-stu-id="d6072-147">toodo so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows hello web API tooexchange an incoming access token for another access token toobe used in outbound requests.</span></span>  <span data-ttu-id="d6072-148">hello v2.0 端點的流量代表述[詳](active-directory-v2-protocols-oauth-on-behalf-of.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-148">hello v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="d6072-149">行動和原生應用程式</span><span class="sxs-lookup"><span data-stu-id="d6072-149">Mobile and native apps</span></span>
<span data-ttu-id="d6072-150">裝置安裝的應用程式，例如行動及桌面應用程式，通常需要 tooaccess 後端服務或 Web Api，將資料儲存和執行代表使用者的功能。</span><span class="sxs-lookup"><span data-stu-id="d6072-150">Device-installed apps, such as mobile and desktop apps, often need tooaccess back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="d6072-151">這些應用程式可以使用 hello 新增登入和授權 tooback 後端服務[OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-151">These apps can add sign-in and authorization tooback-end services by using hello [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="d6072-152">在此流程中，hello 應用程式授權程式碼從 hello v2.0 端點時收到 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="d6072-152">In this flow, hello app receives an authorization code from hello v2.0 endpoint when hello user signs in.</span></span> <span data-ttu-id="d6072-153">hello 授權碼代表 hello hello 使用者身分登入應用程式的權限 toocall 後端服務。</span><span class="sxs-lookup"><span data-stu-id="d6072-153">hello authorization code represents hello app's permission toocall back-end services on behalf of hello user who is signed in.</span></span> <span data-ttu-id="d6072-154">hello 應用程式可以交換 hello hello 背景的 OAuth 2.0 存取權杖和重新整理權杖的授權碼。</span><span class="sxs-lookup"><span data-stu-id="d6072-154">hello app can exchange hello authorization code in hello background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="d6072-155">hello 應用程式可以使用 hello 存取語彙基元 tooauthenticate tooWeb 在 HTTP 要求中，應用程式開發介面，並使用 hello 重新整理語彙基元 tooget 新存取權杖，較舊的存取權杖到期時間。</span><span class="sxs-lookup"><span data-stu-id="d6072-155">hello app can use hello access token tooauthenticate tooWeb APIs in HTTP requests, and use hello refresh token tooget new access tokens when older access tokens expire.</span></span>

![原生應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="d6072-157">單頁應用程式 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="d6072-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="d6072-158">許多新式應用程式都有一個單頁應用程式前端，主要是以 JavaScript 撰寫。</span><span class="sxs-lookup"><span data-stu-id="d6072-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="d6072-159">通常是使用 AngularJS、Ember.js、Durandal.js 等架構來撰寫它們。</span><span class="sxs-lookup"><span data-stu-id="d6072-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="d6072-160">hello Azure AD v2.0 端點支援這些應用程式使用 hello [OAuth 2.0 隱含流程](active-directory-v2-protocols-implicit.md)。</span><span class="sxs-lookup"><span data-stu-id="d6072-160">hello Azure AD v2.0 endpoint supports these apps by using hello [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="d6072-161">Hello 應用程式在此流程中，直接從 hello 接收權杖 v2.0 授權端點，沒有任何伺服器對伺服器交換。</span><span class="sxs-lookup"><span data-stu-id="d6072-161">In this flow, hello app receives tokens directly from hello v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="d6072-162">所有的驗證邏輯和工作階段處理會置於完全 hello JavaScript 用戶端，沒有額外的頁面重新導向。</span><span class="sxs-lookup"><span data-stu-id="d6072-162">All authentication logic and session handling takes place entirely in hello JavaScript client, without extra page redirects.</span></span>

![隱含驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="d6072-164">toosee 此案例中的動作，再試一次的其中一個 hello 單一頁面應用程式程式碼範例中我們[入門](active-directory-appmodel-v2-overview.md#getting-started)> 一節。</span><span class="sxs-lookup"><span data-stu-id="d6072-164">toosee this scenario in action, try one of hello single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="d6072-165">精靈和伺服器端應用程式</span><span class="sxs-lookup"><span data-stu-id="d6072-165">Daemons and server-side apps</span></span>
<span data-ttu-id="d6072-166">應用程式具有長時間執行的程序或運作而不需與使用者互動所也需要 tooaccess 保護的資源，例如 Web 應用程式開發介面的方法。</span><span class="sxs-lookup"><span data-stu-id="d6072-166">Apps that have long-running processes or that operate without interaction with a user also need a way tooaccess secured resources, such as Web APIs.</span></span> <span data-ttu-id="d6072-167">這些應用程式可驗證及使用 hello 應用程式識別來取得權杖而非使用者的委派識別 hello OAuth 2.0 用戶端認證流程。</span><span class="sxs-lookup"><span data-stu-id="d6072-167">These apps can authenticate and get tokens by using hello app's identity, rather than a user's delegated identity, with hello OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="d6072-168">此流程，hello 應用程式會直接與 hello 互動`/token`端點 tooobtain 端點：</span><span class="sxs-lookup"><span data-stu-id="d6072-168">In this flow, hello app interacts directly with hello `/token` endpoint tooobtain endpoints:</span></span>

![精靈應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="d6072-170">toobuild 的精靈應用程式，請參閱中的 hello 用戶端認證文件我們[入門](active-directory-appmodel-v2-overview.md#getting-started)區段，或嘗試[.NET 範例應用程式](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2)。</span><span class="sxs-lookup"><span data-stu-id="d6072-170">toobuild a daemon app, see hello client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
