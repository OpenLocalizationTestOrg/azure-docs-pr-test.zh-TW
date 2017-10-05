---
title: "Azure Active Directory v2.0 端點的應用程式類型 | Microsoft Docs"
description: "Azure Active Directory v2.0 端點所支援的應用程式類型與案例。"
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
ms.openlocfilehash: 9d59e7f0e8f326c40be86e199d7712f6c565cc13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="app-types-for-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="e3952-103">Azure Active Directory v2.0 端點的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="e3952-103">App types for the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="e3952-104">Azure Active Directory (Azure AD) v2.0 端點支援各種新型應用程式架構的驗證，它們全都以產業標準通訊協定 [OAuth 2.0 或 OpenID Connect](active-directory-v2-protocols.md) 為基準。</span><span class="sxs-lookup"><span data-stu-id="e3952-104">The Azure Active Directory (Azure AD) v2.0 endpoint supports authentication for a variety of modern app architectures, all of them based on industry-standard protocols [OAuth 2.0 or OpenID Connect](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="e3952-105">本文描述您可以使用 Azure AD v2.0 來建置的應用程式類型，不論您慣用的語言或平台是哪一種。</span><span class="sxs-lookup"><span data-stu-id="e3952-105">This article describes the types of apps that you can build by using Azure AD v2.0, regardless of your preferred language or platform.</span></span> <span data-ttu-id="e3952-106">本文中的資訊是設計來協助您在[開始使用程式碼](active-directory-appmodel-v2-overview.md#getting-started)之前，先了解概要的案例。</span><span class="sxs-lookup"><span data-stu-id="e3952-106">The information in this article is designed to help you understand high-level scenarios before you [start working with the code](active-directory-appmodel-v2-overview.md#getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="e3952-107">v2.0 端點並未支援所有的 Azure Active Directory 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="e3952-107">The v2.0 endpoint doesn't support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="e3952-108">若要判斷您是否應該使用 v2.0 端點，請參閱 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="e3952-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="the-basics"></a><span data-ttu-id="e3952-109">基本概念</span><span class="sxs-lookup"><span data-stu-id="e3952-109">The basics</span></span>
<span data-ttu-id="e3952-110">您必須在 [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com)中註冊每個使用 v2.0 端點的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3952-110">You must register each app that uses the v2.0 endpoint in the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com).</span></span> <span data-ttu-id="e3952-111">應用程式註冊程序會為您的應用程式收集和指派下列值：</span><span class="sxs-lookup"><span data-stu-id="e3952-111">The app registration process collects and assigns these values for your app:</span></span>

* <span data-ttu-id="e3952-112">可唯一識別應用程式的「應用程式識別碼」</span><span class="sxs-lookup"><span data-stu-id="e3952-112">An **Application ID** that uniquely identifies your app</span></span>
* <span data-ttu-id="e3952-113">可用來將回應導回到應用程式的「重新導向 URI」</span><span class="sxs-lookup"><span data-stu-id="e3952-113">A **Redirect URI** that you can use to direct responses back to your app</span></span>
* <span data-ttu-id="e3952-114">一些其他案例特定值</span><span class="sxs-lookup"><span data-stu-id="e3952-114">A few other scenario-specific values</span></span>

<span data-ttu-id="e3952-115">如需詳細資訊，請了解如何[註冊應用程式](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="e3952-115">For details, learn how to [register an app](active-directory-v2-app-registration.md).</span></span>

<span data-ttu-id="e3952-116">註冊應用程式之後，應用程式便可傳送要求給 Azure AD v2.0 端點來與 Azure AD 通訊。</span><span class="sxs-lookup"><span data-stu-id="e3952-116">After the app is registered, the app communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint.</span></span> <span data-ttu-id="e3952-117">我們提供開放原始碼架構，以及可處理這些要求詳細資料的程式庫。</span><span class="sxs-lookup"><span data-stu-id="e3952-117">We provide open-source frameworks and libraries that handle the details of these requests.</span></span> <span data-ttu-id="e3952-118">您也可以選擇建立對這些端點的要求，來自行實作驗證邏輯：</span><span class="sxs-lookup"><span data-stu-id="e3952-118">You also have the option to implement the authentication logic yourself by creating requests to these endpoints:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```
<!-- TODO: Need a page for libraries to link to -->

## <a name="web-apps"></a><span data-ttu-id="e3952-119">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="e3952-119">Web apps</span></span>
<span data-ttu-id="e3952-120">針對使用者透過瀏覽器存取的 Web 應用程式 (.NET、PHP、Java、Ruby、Python、Node)，您可以使用 [OpenID Connect](active-directory-v2-protocols.md) 來執行使用者登入。</span><span class="sxs-lookup"><span data-stu-id="e3952-120">For web apps (.NET, PHP, Java, Ruby, Python, Node) that the user accesses through a browser, you can use [OpenID Connect](active-directory-v2-protocols.md) for user sign-in.</span></span> <span data-ttu-id="e3952-121">在 OpenID Connect 中，Web 應用程式會收到識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="e3952-121">In OpenID Connect, the web app receives an ID token.</span></span> <span data-ttu-id="e3952-122">識別碼權杖是一個安全性權杖，可驗證使用者的身分識別並以宣告形式提供使用者的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="e3952-122">An ID token is a security token that verifies the user's identity and provides information about the user in the form of claims:</span></span>

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

<span data-ttu-id="e3952-123">若要了解應用程式可用之所有類型的權杖和宣告，請參閱 [v2.0 權杖參考](active-directory-v2-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="e3952-123">You can learn about all the types of tokens and claims that are available to an app in the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="e3952-124">在 Web 伺服器應用程式中，登入驗證流程會採用下列概要步驟：</span><span class="sxs-lookup"><span data-stu-id="e3952-124">In web server apps, the sign-in authentication flow takes these high-level steps:</span></span>

![Web 應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

<span data-ttu-id="e3952-126">您可以使用接收自 v2.0 端點的公開簽署金鑰來驗證識別碼權杖，來確保使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="e3952-126">You can ensure the user's identity by validating the ID token with a public signing key that is received from the v2.0 endpoint.</span></span> <span data-ttu-id="e3952-127">系統會設定工作階段 Cookie，這可在後續的頁面要求上用來識別使用者。</span><span class="sxs-lookup"><span data-stu-id="e3952-127">A session cookie is set, which can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="e3952-128">若要查看此案例的實際運作情形，請在 v2.0 [開始使用](active-directory-appmodel-v2-overview.md#getting-started)一節的 Web 應用程式登入程式碼範例中擇一試用。</span><span class="sxs-lookup"><span data-stu-id="e3952-128">To see this scenario in action, try one of the web app sign-in code samples in our v2.0 [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="e3952-129">除了簡易登入之外，Web 伺服器應用程式可能也需要存取其他 Web 服務，例如 REST API。</span><span class="sxs-lookup"><span data-stu-id="e3952-129">In addition to simple sign-in, a web server app might need to access another web service, such as a REST API.</span></span> <span data-ttu-id="e3952-130">在此情況下，Web 伺服器應用程式可以使用 [OAuth 2.0 授權碼流程](active-directory-v2-protocols.md)，參與結合了 OpenID Connect 與 OAuth 2.0 的流程。</span><span class="sxs-lookup"><span data-stu-id="e3952-130">In this case, the web server app engages in a combined OpenID Connect and OAuth 2.0 flow, by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md).</span></span> <span data-ttu-id="e3952-131">如需有關此案例的詳細資訊，請參閱[開始使用 Web 應用程式和 Web API](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="e3952-131">For more information about this scenario, read about [getting started with web apps and Web APIs](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md).</span></span>

## <a name="web-apis"></a><span data-ttu-id="e3952-132">Web API</span><span class="sxs-lookup"><span data-stu-id="e3952-132">Web APIs</span></span>
<span data-ttu-id="e3952-133">您可以使用 v2.0 端點來保護 Web 服務，例如應用程式的 RESTful Web API。</span><span class="sxs-lookup"><span data-stu-id="e3952-133">You can use the v2.0 endpoint to secure web services, such as your app's RESTful Web API.</span></span> <span data-ttu-id="e3952-134">Web API 使用 OAuth 2.0 存取權杖來保護其資料及驗證連入要求，而不是使用識別碼權杖和工作階段 Cookie。</span><span class="sxs-lookup"><span data-stu-id="e3952-134">Instead of ID tokens and session cookies, a Web API uses an OAuth 2.0 access token to secure its data and to authenticate incoming requests.</span></span> <span data-ttu-id="e3952-135">Web API 的呼叫端會在 HTTP 要求的授權標頭中附加存取權杖，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="e3952-135">The caller of a Web API appends an access token in the authorization header of an HTTP request, like this:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="e3952-136">Web API 會使用這個存取權杖來驗證 API 呼叫端的身分識別，並從存取權杖中所編碼的宣告擷取呼叫端的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e3952-136">The Web API uses the access token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the access token.</span></span> <span data-ttu-id="e3952-137">若要了解應用程式可用之所有類型的權杖和宣告，請參閱 [v2.0 權杖參考](active-directory-v2-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="e3952-137">To learn about all the types of tokens and claims that are available to an app, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

<span data-ttu-id="e3952-138">Web API 可透過公開權限的方式 (亦稱為[範圍](active-directory-v2-scopes.md))，讓使用者能夠選擇加入或退出特定的功能或資料。</span><span class="sxs-lookup"><span data-stu-id="e3952-138">A Web API can give users the power to opt in or opt out of specific functionality or data by exposing permissions, also known as [scopes](active-directory-v2-scopes.md).</span></span> <span data-ttu-id="e3952-139">為了讓發出呼叫的應用程式取得範圍的權限，使用者必須在流程中對範圍表示同意。</span><span class="sxs-lookup"><span data-stu-id="e3952-139">For a calling app to acquire permission to a scope, the user must consent to the scope during a flow.</span></span> <span data-ttu-id="e3952-140">v2.0 端點會向使用者要求權限，然後將這些權限記錄在 Web API 接收的所有存取權杖中。</span><span class="sxs-lookup"><span data-stu-id="e3952-140">The v2.0 endpoint asks the user for permission, and then records permissions in all access tokens that the Web API receives.</span></span> <span data-ttu-id="e3952-141">Web API 會驗證它在每次呼叫所收到的存取權杖，並執行授權檢查。</span><span class="sxs-lookup"><span data-stu-id="e3952-141">The Web API validates the access tokens it receives on each call and performs authorization checks.</span></span>

<span data-ttu-id="e3952-142">Web API 可以從所有類型的應用程式接收存取權杖，包括 Web 伺服器應用程式、傳統型應用程式和行動應用程式、單頁應用程式、伺服器端精靈，甚至是其他的 Web API。</span><span class="sxs-lookup"><span data-stu-id="e3952-142">A Web API can receive access tokens from all types of apps, including web server apps, desktop and mobile apps, single-page apps, server-side daemons, and even other Web APIs.</span></span> <span data-ttu-id="e3952-143">Web API 的概要流程看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="e3952-143">The high-level flow for a Web API looks like this:</span></span>

![Web API 驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_webapi.png)

<span data-ttu-id="e3952-145">若要了解如何使用 OAuth2 存取權杖來保護 Web API，請查看[開始使用](active-directory-appmodel-v2-overview.md#getting-started)一節中的 Web API 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="e3952-145">To learn how to secure a Web API by using OAuth2 access tokens, check out the Web API code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

<span data-ttu-id="e3952-146">在許多情況下，Web API 也需要對受 Azure Active Directory 保護的其他下游 Web API 發出傳出要求。</span><span class="sxs-lookup"><span data-stu-id="e3952-146">In many cases, web APIs also need to make outbound requests to other downstream web APIs secured by Azure Active Directory.</span></span>  <span data-ttu-id="e3952-147">若要這樣做，Web API 可以利用 Azure AD 的「代理者」流程，它能允許 Web API 將傳入存取權杖交換為要在傳出要求中使用的另一個存取權杖。</span><span class="sxs-lookup"><span data-stu-id="e3952-147">To do so, web APIs can take advantage of Azure AD's **On Behalf Of** flow, which allows the web API to exchange an incoming access token for another access token to be used in outbound requests.</span></span>  <span data-ttu-id="e3952-148">v2.0 端點的「代理者」流程已[在此詳細說明](active-directory-v2-protocols-oauth-on-behalf-of.md)。</span><span class="sxs-lookup"><span data-stu-id="e3952-148">The v2.0 endpoint's On Behalf Of flow is described in [detail here](active-directory-v2-protocols-oauth-on-behalf-of.md).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="e3952-149">行動和原生應用程式</span><span class="sxs-lookup"><span data-stu-id="e3952-149">Mobile and native apps</span></span>
<span data-ttu-id="e3952-150">裝置安裝的應用程式 (例如行動應用程式和傳統型應用程式) 通常需要存取儲存資料及代表使用者執行功能的後端服務或 Web API。</span><span class="sxs-lookup"><span data-stu-id="e3952-150">Device-installed apps, such as mobile and desktop apps, often need to access back-end services or Web APIs that store data and perform functions on behalf of a user.</span></span> <span data-ttu-id="e3952-151">這些應用程式可以使用 [OAuth 2.0 授權碼流程](active-directory-v2-protocols-oauth-code.md)，將登入和授權新增至後端服務。</span><span class="sxs-lookup"><span data-stu-id="e3952-151">These apps can add sign-in and authorization to back-end services by using the [OAuth 2.0 authorization code flow](active-directory-v2-protocols-oauth-code.md).</span></span>

<span data-ttu-id="e3952-152">在此流程中，應用程式會在使用者登入時，從 v2.0 端點接收授權碼。</span><span class="sxs-lookup"><span data-stu-id="e3952-152">In this flow, the app receives an authorization code from the v2.0 endpoint when the user signs in.</span></span> <span data-ttu-id="e3952-153">授權碼代表應用程式具備權限，可代表登入的使用者呼叫後端服務。</span><span class="sxs-lookup"><span data-stu-id="e3952-153">The authorization code represents the app's permission to call back-end services on behalf of the user who is signed in.</span></span> <span data-ttu-id="e3952-154">應用程式可以在背景中以授權碼交換 OAuth 2.0 存取權杖和重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="e3952-154">The app can exchange the authorization code in the background for an OAuth 2.0 access token and a refresh token.</span></span> <span data-ttu-id="e3952-155">應用程式可以使用存取權杖在 HTTP 要求中向 Web API 進行驗證，以及在舊存取權杖到期時，使用重新整理權杖來取得新的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="e3952-155">The app can use the access token to authenticate to Web APIs in HTTP requests, and use the refresh token to get new access tokens when older access tokens expire.</span></span>

![原生應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## <a name="single-page-apps-javascript"></a><span data-ttu-id="e3952-157">單頁應用程式 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="e3952-157">Single-page apps (JavaScript)</span></span>
<span data-ttu-id="e3952-158">許多新式應用程式都有一個單頁應用程式前端，主要是以 JavaScript 撰寫。</span><span class="sxs-lookup"><span data-stu-id="e3952-158">Many modern apps have a single-page app front end that primarily is written in JavaScript.</span></span> <span data-ttu-id="e3952-159">通常是使用 AngularJS、Ember.js、Durandal.js 等架構來撰寫它們。</span><span class="sxs-lookup"><span data-stu-id="e3952-159">Often, it's written by using a framework like AngularJS, Ember.js, or Durandal.js.</span></span> <span data-ttu-id="e3952-160">Azure AD v2.0 端點是透過使用 [OAuth 2.0 隱含流程](active-directory-v2-protocols-implicit.md)來支援這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="e3952-160">The Azure AD v2.0 endpoint supports these apps by using the [OAuth 2.0 implicit flow](active-directory-v2-protocols-implicit.md).</span></span>

<span data-ttu-id="e3952-161">在此流程中，應用程式會直接從 v2.0 授權端點接收權杖，而不需要執行任何伺服器對伺服器交換。</span><span class="sxs-lookup"><span data-stu-id="e3952-161">In this flow, the app receives tokens directly from the v2.0 authorize endpoint, without any server-to-server exchanges.</span></span> <span data-ttu-id="e3952-162">所有驗證邏輯和工作階段處理都完全在 JavaScript 用戶端中進行，而不需要執行額外的頁面重新導向。</span><span class="sxs-lookup"><span data-stu-id="e3952-162">All authentication logic and session handling takes place entirely in the JavaScript client, without extra page redirects.</span></span>

![隱含驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

<span data-ttu-id="e3952-164">若要查看此案例的實際運作情形，請在[開始使用](active-directory-appmodel-v2-overview.md#getting-started)一節的單頁應用程式程式碼範例中擇一試用。</span><span class="sxs-lookup"><span data-stu-id="e3952-164">To see this scenario in action, try one of the single-page app code samples in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section.</span></span>

## <a name="daemons-and-server-side-apps"></a><span data-ttu-id="e3952-165">精靈和伺服器端應用程式</span><span class="sxs-lookup"><span data-stu-id="e3952-165">Daemons and server-side apps</span></span>
<span data-ttu-id="e3952-166">應用程式如果含有長時間執行的程序，或其運作方式不需要與使用者互動，就也需要一個存取受保護資源 (例如 Web API) 的方法。</span><span class="sxs-lookup"><span data-stu-id="e3952-166">Apps that have long-running processes or that operate without interaction with a user also need a way to access secured resources, such as Web APIs.</span></span> <span data-ttu-id="e3952-167">這些應用程式可以使用應用程式的身分識別 (而非使用者委派的身分識別) 搭配 OAuth 2.0 用戶端認證流程，來驗證及取得權杖。</span><span class="sxs-lookup"><span data-stu-id="e3952-167">These apps can authenticate and get tokens by using the app's identity, rather than a user's delegated identity, with the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="e3952-168">在此流程中，應用程式會直接與 `/token` 端點互動來取得端點：</span><span class="sxs-lookup"><span data-stu-id="e3952-168">In this flow, the app interacts directly with the `/token` endpoint to obtain endpoints:</span></span>

![精靈應用程式驗證流程](../../media/active-directory-v2-flows/convergence_scenarios_daemon.png)

<span data-ttu-id="e3952-170">若要建置精靈應用程式，請參閱[開始使用](active-directory-appmodel-v2-overview.md#getting-started)一節中的用戶端認證文件，或試試 [.NET 範例應用程式](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2)。</span><span class="sxs-lookup"><span data-stu-id="e3952-170">To build a daemon app, see the client credentials documentation in our [Getting Started](active-directory-appmodel-v2-overview.md#getting-started) section, or try a [.NET sample app](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).</span></span>
