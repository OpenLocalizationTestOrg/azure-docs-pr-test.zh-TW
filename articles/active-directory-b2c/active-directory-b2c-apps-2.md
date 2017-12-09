---
title: "應用程式類型 - Azure AD B2C | Microsoft Docs"
description: "您在 Azure Active Directory B2C 中可建置的應用程式類型。"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: bb9d4abe-0db7-4bd9-b0c4-2f43b2c9cf33
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/06/2016
ms.author: dastrock
ms.openlocfilehash: 51001feb17ae99d3bd391a9f980d514e07f97099
ms.sourcegitcommit: dfd6f46af588d4cd9b7a11a026dd66612ce37a4e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a><span data-ttu-id="c0994-103">Azure Active Directory B2C：應用程式類型</span><span class="sxs-lookup"><span data-stu-id="c0994-103">Azure Active Directory B2C: Types of applications</span></span>
<span data-ttu-id="c0994-104">Azure Active Directory (Azure AD) B2C 支援各種現代應用程式架構的驗證。</span><span class="sxs-lookup"><span data-stu-id="c0994-104">Azure Active Directory (Azure AD) B2C supports authentication for a variety of modern app architectures.</span></span> <span data-ttu-id="c0994-105">全部都以業界標準通訊協定 [OAuth 2.0](active-directory-b2c-reference-protocols.md) 或 [OpenID Connect](active-directory-b2c-reference-protocols.md) 為基礎。</span><span class="sxs-lookup"><span data-stu-id="c0994-105">All of them are based on the industry standard protocols [OAuth 2.0](active-directory-b2c-reference-protocols.md) or [OpenID Connect](active-directory-b2c-reference-protocols.md).</span></span> <span data-ttu-id="c0994-106">此文件簡要描述您可以建置的應用程式類型，不涉及您慣用的語言或平台。</span><span class="sxs-lookup"><span data-stu-id="c0994-106">This document briefly describes the types of apps that you can build, independent of the language or platform you prefer.</span></span> <span data-ttu-id="c0994-107">在您 [開始建立應用程式](active-directory-b2c-overview.md#get-started)之前，也可協助您先了解一些高階案例。</span><span class="sxs-lookup"><span data-stu-id="c0994-107">It also helps you understand the high-level scenarios before you [start building applications](active-directory-b2c-overview.md#get-started).</span></span>

## <a name="the-basics"></a><span data-ttu-id="c0994-108">基本概念</span><span class="sxs-lookup"><span data-stu-id="c0994-108">The basics</span></span>
<span data-ttu-id="c0994-109">每個使用 Azure AD B2C 的應用程式都必須透過 [Azure 入口網站](https://portal.azure.com/)，註冊在 [B2C 目錄](active-directory-b2c-get-started.md)中。</span><span class="sxs-lookup"><span data-stu-id="c0994-109">Every app that uses Azure AD B2C must be registered in your [B2C directory](active-directory-b2c-get-started.md) via the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c0994-110">App 註冊處理序會收集與指派一些值給您的 app：</span><span class="sxs-lookup"><span data-stu-id="c0994-110">The app registration process collects and assigns a few values to your app:</span></span>

* <span data-ttu-id="c0994-111">可唯一識別應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="c0994-111">An **Application ID** that uniquely identifies your app.</span></span>
* <span data-ttu-id="c0994-112">可用來將回應導回至應用程式的 **重新導向 URI** 。</span><span class="sxs-lookup"><span data-stu-id="c0994-112">A **Redirect URI** that can be used to direct responses back to your app.</span></span>
* <span data-ttu-id="c0994-113">案例特有的其他任何值。</span><span class="sxs-lookup"><span data-stu-id="c0994-113">Any other scenario-specific values.</span></span> <span data-ttu-id="c0994-114">如需詳細資訊，請瞭解如何 [註冊應用程式](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="c0994-114">For more details, learn how to [register an app](active-directory-b2c-app-registration.md).</span></span>

<span data-ttu-id="c0994-115">註冊應用程式之後，應用程式即會向 Azure AD v2.0 端點傳送要求，以與 Azure AD 通訊：</span><span class="sxs-lookup"><span data-stu-id="c0994-115">After the app is registered, it communicates with Azure AD by sending requests to the Azure AD v2.0 endpoint:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="c0994-116">每個傳送至 Azure AD B2C 的要求都指定一個 **原則**。</span><span class="sxs-lookup"><span data-stu-id="c0994-116">Each request that is sent to Azure AD B2C specifies a **policy**.</span></span> <span data-ttu-id="c0994-117">原則控制 Azure AD 的行為。</span><span class="sxs-lookup"><span data-stu-id="c0994-117">A policy controls the behavior of Azure AD.</span></span> <span data-ttu-id="c0994-118">您也可以使用這些端點來建立一組可靈活自訂的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="c0994-118">You can also use these endpoints to create a highly customizable set of user experiences.</span></span> <span data-ttu-id="c0994-119">常見的原則包括註冊、登入和設定檔編輯原則。</span><span class="sxs-lookup"><span data-stu-id="c0994-119">Common policies include sign-up, sign-in, and profile-edit policies.</span></span> <span data-ttu-id="c0994-120">如果您不熟悉原則，在繼續之前，請參閱 Azure AD B2C 的 [可延伸原則架構](active-directory-b2c-reference-policies.md) 。</span><span class="sxs-lookup"><span data-stu-id="c0994-120">If you are not familiar with policies, you should read about the Azure AD B2C [extensible policy framework](active-directory-b2c-reference-policies.md) before you continue.</span></span>

<span data-ttu-id="c0994-121">每個應用程式與 v2.0 端點的互動都遵循類似的高階模式：</span><span class="sxs-lookup"><span data-stu-id="c0994-121">The interaction of every app with a v2.0 endpoint follows a similar high-level pattern:</span></span>

1. <span data-ttu-id="c0994-122">應用程式會將使用者導向至 v2.0 端點以執行 [原則](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="c0994-122">The app directs the user to the v2.0 endpoint to execute a [policy](active-directory-b2c-reference-policies.md).</span></span>
2. <span data-ttu-id="c0994-123">使用者完成根據原則定義來完成原則。</span><span class="sxs-lookup"><span data-stu-id="c0994-123">The user completes the policy according to the policy definition.</span></span>
3. <span data-ttu-id="c0994-124">應用程式會從 v2.0 端點接收某種安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="c0994-124">The app receives some kind of security token from the v2.0 endpoint.</span></span>
4. <span data-ttu-id="c0994-125">應用程式使用此安全性權杖存取受保護的資訊或受保護的資源。</span><span class="sxs-lookup"><span data-stu-id="c0994-125">The app uses the security token to access protected information or a protected resource.</span></span>
5. <span data-ttu-id="c0994-126">資源伺服器會驗證安全性權杖，以確認可以授與存取權。</span><span class="sxs-lookup"><span data-stu-id="c0994-126">The resource server validates the security token to verify that access can be granted.</span></span>
6. <span data-ttu-id="c0994-127">應用程式會定期重新整理安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="c0994-127">The app periodically refreshes the security token.</span></span>

<!-- TODO: Need a page for libraries to link to -->
<span data-ttu-id="c0994-128">根據您要建置的應用程式類型而定，這些步驟可能稍有不同。</span><span class="sxs-lookup"><span data-stu-id="c0994-128">These steps can differ slightly based on the type of app you're building.</span></span> <span data-ttu-id="c0994-129">開放原始碼程式庫可以為您處理細節。</span><span class="sxs-lookup"><span data-stu-id="c0994-129">Open source libraries can address the details for you.</span></span>

## <a name="web-apps"></a><span data-ttu-id="c0994-130">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c0994-130">Web apps</span></span>
<span data-ttu-id="c0994-131">對於裝載於伺服器且透過瀏覽器存取的 Web 應用程式 (包括 .NET、PHP、Java、Ruby、Python、Node.js)，Azure AD B2C 支援以 [OpenID Connect](active-directory-b2c-reference-protocols.md) 完成一切使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="c0994-131">For web apps (including .NET, PHP, Java, Ruby, Python, and Node.js) that are hosted on a server and accessed through a browser, Azure AD B2C supports [OpenID Connect](active-directory-b2c-reference-protocols.md) for all user experiences.</span></span> <span data-ttu-id="c0994-132">這包括登入、註冊和設定檔管理。</span><span class="sxs-lookup"><span data-stu-id="c0994-132">This includes sign-in, sign-up, and profile management.</span></span> <span data-ttu-id="c0994-133">在 Azure AD B2C 的 OpenID Connect 實作中，Web 應用程式會向 Azure AD 發出驗證要求，以起始這些使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="c0994-133">In the Azure AD B2C implementation of OpenID Connect, your web app initiates these user experiences by issuing authentication requests to Azure AD.</span></span> <span data-ttu-id="c0994-134">要求的結果是 `id_token`。</span><span class="sxs-lookup"><span data-stu-id="c0994-134">The result of the request is an `id_token`.</span></span> <span data-ttu-id="c0994-135">這個安全性權杖代表使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="c0994-135">This security token represents the user's identity.</span></span> <span data-ttu-id="c0994-136">它也以宣告形式提供使用者的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="c0994-136">It also provides information about the user in the form of claims:</span></span>

```
// Partial raw id_token
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6ImtyaU1QZG1Cd...

// Partial content of a decoded id_token
{
    "name": "John Smith",
    "email": "john.smith@gmail.com",
    "oid": "d9674823-dffc-4e3f-a6eb-62fe4bd48a58"
    ...
}
```

<span data-ttu-id="c0994-137">請參閱 [B2C 權杖參考](active-directory-b2c-reference-tokens.md)，以深入了解應用程式可用的權杖和宣告類型。</span><span class="sxs-lookup"><span data-stu-id="c0994-137">Learn more about the types of tokens and claims available to an app in the [B2C token reference](active-directory-b2c-reference-tokens.md).</span></span>

<span data-ttu-id="c0994-138">在 Web 應用程式中，每次執行 [原則](active-directory-b2c-reference-policies.md) 會採用下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="c0994-138">In a web app, each execution of a [policy](active-directory-b2c-reference-policies.md) takes these high-level steps:</span></span>

![Web 應用程式泳道映像](./media/active-directory-b2c-apps/webapp.png)

<span data-ttu-id="c0994-140">使用接收自 Azure AD 的公開簽署金鑰來驗證 `id_token` ，就足以驗證使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="c0994-140">Validation of the `id_token` by using a public signing key that is received from Azure AD is sufficient to verify the identity of the user.</span></span> <span data-ttu-id="c0994-141">這也會設定工作階段 Cookie，在後續頁面要求上可用來識別使用者。</span><span class="sxs-lookup"><span data-stu-id="c0994-141">This also sets a session cookie that can be used to identify the user on subsequent page requests.</span></span>

<span data-ttu-id="c0994-142">若要查看此案例的實際運作情形，請在 [使用者入門](active-directory-b2c-overview.md#get-started)一節的 Web 應用程式登入程式碼範例中擇一試用。</span><span class="sxs-lookup"><span data-stu-id="c0994-142">To see this scenario in action, try one of the web app sign-in code samples in our [Getting started section](active-directory-b2c-overview.md#get-started).</span></span>

<span data-ttu-id="c0994-143">除了讓登入更簡單，Web 伺服器應用程式可能也需要存取後端 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c0994-143">In addition to facilitating simple sign-in, a web server app might also need to access a back-end web service.</span></span> <span data-ttu-id="c0994-144">在此情況下，Web 應用程式可能執行稍有不同的 [OpenID Connect 流程](active-directory-b2c-reference-oidc.md) ，並使用授權碼和重新整理權杖來取得權杖。</span><span class="sxs-lookup"><span data-stu-id="c0994-144">In this case, the web app can perform a slightly different [OpenID Connect flow](active-directory-b2c-reference-oidc.md) and acquire tokens by using authorization codes and refresh tokens.</span></span> <span data-ttu-id="c0994-145">以下 [Web API](#web-apis)一節描述此案例。</span><span class="sxs-lookup"><span data-stu-id="c0994-145">This scenario is depicted in the following [Web APIs section](#web-apis).</span></span>

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a><span data-ttu-id="c0994-146">Web API</span><span class="sxs-lookup"><span data-stu-id="c0994-146">Web APIs</span></span>
<span data-ttu-id="c0994-147">您可以使用 Azure AD B2C 來保護 Web 服務，例如應用程式的 RESTful Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-147">You can use Azure AD B2C to secure web services such as your app's RESTful web API.</span></span> <span data-ttu-id="c0994-148">Web API 可以使用 OAuth 2.0 保護其資料，並使用權杖來驗證傳入的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="c0994-148">Web APIs can use OAuth 2.0 to secure their data, by authenticating incoming HTTP requests using tokens.</span></span> <span data-ttu-id="c0994-149">Web API 的呼叫端會在 HTTP 要求的授權標頭中附加權杖：</span><span class="sxs-lookup"><span data-stu-id="c0994-149">The caller of a web API appends a token in the authorization header of an HTTP request:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="c0994-150">然後，Web API 會使用這個權杖來驗證 API 呼叫端的身分識別，並從編碼在權杖中的宣告擷取呼叫端的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c0994-150">The web API can then use the token to verify the API caller's identity and to extract information about the caller from claims that are encoded in the token.</span></span> <span data-ttu-id="c0994-151">請參閱 [Azure AD B2C 權杖參考](active-directory-b2c-reference-tokens.md)，以深入了解應用程式可用的權杖和宣告類型。</span><span class="sxs-lookup"><span data-stu-id="c0994-151">Learn more about the types of tokens and claims available to an app in the [Azure AD B2C token reference](active-directory-b2c-reference-tokens.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c0994-152">Azure AD B2C 目前僅支援以各自已知的用戶端存取的 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-152">Azure AD B2C currently supports only web APIs that are accessed by their own well-known clients.</span></span> <span data-ttu-id="c0994-153">例如，完整的應用程式可能包括 iOS 應用程式、Android 應用程式和後端 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-153">For instance, your complete app may include an iOS app, an Android app, and a back-end web API.</span></span> <span data-ttu-id="c0994-154">完全支援這種架構。</span><span class="sxs-lookup"><span data-stu-id="c0994-154">This architecture is fully supported.</span></span> <span data-ttu-id="c0994-155">目前不支援協力廠商用戶端 (例如另一個 iOS 應用程式) 存取相同的 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-155">Allowing a partner client, such as another iOS app, to access the same web API is not currently supported.</span></span> <span data-ttu-id="c0994-156">完整應用程式的所有元件必須共用單一應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="c0994-156">All of the components of your complete app must share a single application ID.</span></span>
>
>

<span data-ttu-id="c0994-157">Web API 接收的權杖可以來自許多類型的應用程式，包括 Web 應用程式、桌面和行動應用程式、單一頁面應用程式、伺服器端精靈，以及其他 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-157">A web API can receive tokens from many types of clients, including web apps, desktop and mobile apps, single page apps, server-side daemons, and other web APIs.</span></span> <span data-ttu-id="c0994-158">以下是 Web 應用程式呼叫 Web API 的完整流程範例：</span><span class="sxs-lookup"><span data-stu-id="c0994-158">Here's an example of the complete flow for a web app that calls a web API:</span></span>

![Web 應用程式 Web API 泳道映像](./media/active-directory-b2c-apps/webapi.png)

<span data-ttu-id="c0994-160">若要深入了解授權碼、重新整理權杖和取得權杖的步驟，請參閱 [OAuth 2.0 通訊協定](active-directory-b2c-reference-oauth-code.md)。</span><span class="sxs-lookup"><span data-stu-id="c0994-160">To learn more about authorization codes, refresh tokens, and the steps for getting tokens, read about the [OAuth 2.0 protocol](active-directory-b2c-reference-oauth-code.md).</span></span>

<span data-ttu-id="c0994-161">若要了解如何使用 Azure AD B2C 保護 Web API，請查看 [使用者入門](active-directory-b2c-overview.md#get-started)一節的 Web API 教學課程。</span><span class="sxs-lookup"><span data-stu-id="c0994-161">To learn how to secure a web API by using Azure AD B2C, check out the web API tutorials in our [Getting started section](active-directory-b2c-overview.md#get-started).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="c0994-162">行動和原生應用程式</span><span class="sxs-lookup"><span data-stu-id="c0994-162">Mobile and native apps</span></span>
<span data-ttu-id="c0994-163">安裝在裝置中的應用程式 (如行動和桌面應用程式) 通常需要代替使用者存取後端服務或 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-163">Apps that are installed on devices, such as mobile and desktop apps, often need to access back-end services or web APIs on behalf of users.</span></span> <span data-ttu-id="c0994-164">您可以將自訂的身分識別管理體驗加入至原生應用程式，並使用 Azure AD B2C 和 [OAuth 2.0 授權碼流程](active-directory-b2c-reference-oauth-code.md)安全地呼叫後端服務。</span><span class="sxs-lookup"><span data-stu-id="c0994-164">You can add customized identity management experiences to your native apps and securely call back-end services by using Azure AD B2C and the [OAuth 2.0 authorization code flow](active-directory-b2c-reference-oauth-code.md).</span></span>  

<span data-ttu-id="c0994-165">在此流程中，應用程式會執行[原則](active-directory-b2c-reference-policies.md)，並在使用者完成原則之後，從 Azure AD 接收 `authorization_code`。</span><span class="sxs-lookup"><span data-stu-id="c0994-165">In this flow, the app executes [policies](active-directory-b2c-reference-policies.md) and receives an `authorization_code` from Azure AD after the user completes the policy.</span></span> <span data-ttu-id="c0994-166">`authorization_code` 代表應用程式有權限代替目前登入的使用者呼叫後端服務。</span><span class="sxs-lookup"><span data-stu-id="c0994-166">The `authorization_code` represents the app's permission to call back-end services on behalf of the user who is currently signed in.</span></span> <span data-ttu-id="c0994-167">然後應用程式就可以在背景中以 `authorization_code` 來兌換 `id_token` 和 `refresh_token`。</span><span class="sxs-lookup"><span data-stu-id="c0994-167">The app can then exchange the `authorization_code` in the background for an `id_token` and a `refresh_token`.</span></span>  <span data-ttu-id="c0994-168">應用程式可以在 HTTP 要求中使用 `id_token` 向後端 Web API 驗證。</span><span class="sxs-lookup"><span data-stu-id="c0994-168">The app can use the `id_token` to authenticate to a back-end web API in HTTP requests.</span></span> <span data-ttu-id="c0994-169">它也可以使用 `refresh_token` 來取得新的 `id_token` (當舊的已過期時)。</span><span class="sxs-lookup"><span data-stu-id="c0994-169">It can also use the `refresh_token` to get a new `id_token` when an older one expires.</span></span>

> [!NOTE]
> <span data-ttu-id="c0994-170">Azure AD B2C 目前僅支援用來存取應用程式本身的後端 Web 服務的權杖。</span><span class="sxs-lookup"><span data-stu-id="c0994-170">Azure AD B2C currently supports only tokens that are used to access an app's own back-end web service.</span></span> <span data-ttu-id="c0994-171">例如，完整的應用程式可能包括 iOS 應用程式、Android 應用程式和後端 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-171">For instance, your complete app may include an iOS app, an Android app, and a back-end web API.</span></span> <span data-ttu-id="c0994-172">完全支援這種架構。</span><span class="sxs-lookup"><span data-stu-id="c0994-172">This architecture is fully supported.</span></span> <span data-ttu-id="c0994-173">目前不支援 iOS 應用程式使用 OAuth 2.0 存取權杖來存取協力廠商 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-173">Allowing your iOS app to access a partner web API by using OAuth 2.0 access tokens is not currently supported.</span></span> <span data-ttu-id="c0994-174">完整應用程式的所有元件必須共用單一應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="c0994-174">All of the components of your complete app must share a single application ID.</span></span>
>
>

![原生應用程式泳道映像](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a><span data-ttu-id="c0994-176">目前的限制</span><span class="sxs-lookup"><span data-stu-id="c0994-176">Current limitations</span></span>
<span data-ttu-id="c0994-177">Azure AD B2C 目前不支援下列類型的應用程式，但正在規劃中。</span><span class="sxs-lookup"><span data-stu-id="c0994-177">Azure AD B2C does not currently support the following types of apps, but they are on the roadmap.</span></span> 

### <a name="daemonsserver-side-apps"></a><span data-ttu-id="c0994-178">精靈/伺服器端應用程式</span><span class="sxs-lookup"><span data-stu-id="c0994-178">Daemons/server-side apps</span></span>
<span data-ttu-id="c0994-179">如果應用程式含有長時間執行的處理序或不需要使用者操作，也仍然需要方法來存取受保護的資源，例如 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0994-179">Apps that contain long-running processes or that operate without the presence of a user also need a way to access secured resources such as web APIs.</span></span> <span data-ttu-id="c0994-180">這些應用程式可以使用應用程式身分識別 (而非使用者委派身分識別) 和使用 OAuth 2.0 用戶端認證流程，以驗證及取得權杖。</span><span class="sxs-lookup"><span data-stu-id="c0994-180">These apps can authenticate and get tokens by using the app's identity (rather than a user's delegated identity) and by using the OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="c0994-181">Azure AD B2C 目前不支援此流程。</span><span class="sxs-lookup"><span data-stu-id="c0994-181">This flow is not currently supported by Azure AD B2C.</span></span> <span data-ttu-id="c0994-182">這些應用程式只有在互動式使用者流程發生之後，才取得權杖。</span><span class="sxs-lookup"><span data-stu-id="c0994-182">These apps can get tokens only after an interactive user flow has occurred.</span></span>

### <a name="web-api-chains-on-behalf-of-flow"></a><span data-ttu-id="c0994-183">Web API 鏈結 (代理者流程)</span><span class="sxs-lookup"><span data-stu-id="c0994-183">Web API chains (on-behalf-of flow)</span></span>
<span data-ttu-id="c0994-184">許多架構中都有一個 Web API 需要呼叫另一個下游 Web API，而兩者都受 Azure AD B2C 保護。</span><span class="sxs-lookup"><span data-stu-id="c0994-184">Many architectures include a web API that needs to call another downstream web API, where both are secured by Azure AD B2C.</span></span> <span data-ttu-id="c0994-185">此案例常見於有 Web API 後端的原生用戶端。</span><span class="sxs-lookup"><span data-stu-id="c0994-185">This scenario is common in native clients that have a Web API back-end.</span></span> <span data-ttu-id="c0994-186">這接著會呼叫 Microsoft 線上服務，例如 Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="c0994-186">This then calls a Microsoft online service such as the Azure AD Graph API.</span></span>

<span data-ttu-id="c0994-187">使用 OAuth 2.0 JWT 持有人認證授與可支援此鏈結的 Web API 案例，亦稱為代理者流程。</span><span class="sxs-lookup"><span data-stu-id="c0994-187">This chained web API scenario can be supported by using the OAuth 2.0 JWT bearer credential grant, also known as the on-behalf-of flow.</span></span>  <span data-ttu-id="c0994-188">不過，Azure AD B2C 目前未實作代理者流程。</span><span class="sxs-lookup"><span data-stu-id="c0994-188">However, the on-behalf-of flow is not currently implemented in the Azure AD B2C.</span></span>
