---
title: "aaaAzure AD B2C |Microsoft 文件"
description: "您可以在 hello Azure Active Directory B2C 建置 hello 類型的應用程式。"
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
ms.openlocfilehash: 7dd3dac781fb7e1553dd0f2d112b1956489a7dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-types-of-applications"></a><span data-ttu-id="b6e6b-103">Azure Active Directory B2C：應用程式類型</span><span class="sxs-lookup"><span data-stu-id="b6e6b-103">Azure Active Directory B2C: Types of applications</span></span>
<span data-ttu-id="b6e6b-104">Azure Active Directory (Azure AD) B2C 支援各種現代應用程式架構的驗證。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-104">Azure Active Directory (Azure AD) B2C supports authentication for a variety of modern app architectures.</span></span> <span data-ttu-id="b6e6b-105">全部都根據 hello 業界標準通訊協定[OAuth 2.0](active-directory-b2c-reference-protocols.md)或[OpenID Connect](active-directory-b2c-reference-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-105">All of them are based on hello industry standard protocols [OAuth 2.0](active-directory-b2c-reference-protocols.md) or [OpenID Connect](active-directory-b2c-reference-protocols.md).</span></span> <span data-ttu-id="b6e6b-106">本文件簡要描述 hello 可以建置的應用程式類型，與 hello 語言或平台無關您偏好。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-106">This document briefly describes hello types of apps that you can build, independent of hello language or platform you prefer.</span></span> <span data-ttu-id="b6e6b-107">也可協助您了解 hello 高階案例才能[開始建置應用程式](active-directory-b2c-overview.md#get-started)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-107">It also helps you understand hello high-level scenarios before you [start building applications](active-directory-b2c-overview.md#get-started).</span></span>

## <a name="hello-basics"></a><span data-ttu-id="b6e6b-108">hello 基本概念</span><span class="sxs-lookup"><span data-stu-id="b6e6b-108">hello basics</span></span>
<span data-ttu-id="b6e6b-109">使用 Azure AD B2C 每個應用程式必須在中註冊您[B2C 目錄](active-directory-b2c-get-started.md)透過 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-109">Every app that uses Azure AD B2C must be registered in your [B2C directory](active-directory-b2c-get-started.md) via hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="b6e6b-110">hello 應用程式登錄程序會收集，並將幾個值 tooyour 應用程式：</span><span class="sxs-lookup"><span data-stu-id="b6e6b-110">hello app registration process collects and assigns a few values tooyour app:</span></span>

* <span data-ttu-id="b6e6b-111">可唯一識別應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-111">An **Application ID** that uniquely identifies your app.</span></span>
* <span data-ttu-id="b6e6b-112">A**重新導向 URI**可以使用的 toodirect 回應後 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-112">A **Redirect URI** that can be used toodirect responses back tooyour app.</span></span>
* <span data-ttu-id="b6e6b-113">案例特有的其他任何值。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-113">Any other scenario-specific values.</span></span> <span data-ttu-id="b6e6b-114">如需詳細資訊，了解如何太[註冊應用程式](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-114">For more details, learn how too[register an app](active-directory-b2c-app-registration.md).</span></span>

<span data-ttu-id="b6e6b-115">Hello 應用程式的註冊後，通訊與 Azure AD 傳送要求 Azure AD toohello v2.0 端點：</span><span class="sxs-lookup"><span data-stu-id="b6e6b-115">After hello app is registered, it communicates with Azure AD by sending requests toohello Azure AD v2.0 endpoint:</span></span>

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize
https://login.microsoftonline.com/common/oauth2/v2.0/token
```

<span data-ttu-id="b6e6b-116">指定每個要求傳送 tooAzure AD B2C**原則**。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-116">Each request that is sent tooAzure AD B2C specifies a **policy**.</span></span> <span data-ttu-id="b6e6b-117">原則控制 Azure AD 的 hello 的行為。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-117">A policy controls hello behavior of Azure AD.</span></span> <span data-ttu-id="b6e6b-118">您也可以使用這些端點 toocreate 一組高度可自訂的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-118">You can also use these endpoints toocreate a highly customizable set of user experiences.</span></span> <span data-ttu-id="b6e6b-119">常見的原則包括註冊、登入和設定檔編輯原則。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-119">Common policies include sign-up, sign-in, and profile-edit policies.</span></span> <span data-ttu-id="b6e6b-120">如果您不熟悉原則，您應該閱讀 hello Azure AD B2C[可延伸原則架構](active-directory-b2c-reference-policies.md)繼續進行之前。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-120">If you are not familiar with policies, you should read about hello Azure AD B2C [extensible policy framework](active-directory-b2c-reference-policies.md) before you continue.</span></span>

<span data-ttu-id="b6e6b-121">與 2.0 版端點的 hello 互動的每個應用程式遵循類似的高層級模式：</span><span class="sxs-lookup"><span data-stu-id="b6e6b-121">hello interaction of every app with a v2.0 endpoint follows a similar high-level pattern:</span></span>

1. <span data-ttu-id="b6e6b-122">hello 應用程式會引導 hello 使用者 toohello v2.0 端點 tooexecute[原則](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-122">hello app directs hello user toohello v2.0 endpoint tooexecute a [policy](active-directory-b2c-reference-policies.md).</span></span>
2. <span data-ttu-id="b6e6b-123">hello 使用者完成 hello 原則根據 toohello 原則定義。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-123">hello user completes hello policy according toohello policy definition.</span></span>
3. <span data-ttu-id="b6e6b-124">hello 應用程式會收到 hello v2.0 端點某種類型的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-124">hello app receives some kind of security token from hello v2.0 endpoint.</span></span>
4. <span data-ttu-id="b6e6b-125">hello 應用程式會使用 hello 安全性語彙基元 tooaccess 受保護的資訊或受保護的資源。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-125">hello app uses hello security token tooaccess protected information or a protected resource.</span></span>
5. <span data-ttu-id="b6e6b-126">hello 資源伺服器會驗證 hello 安全性語彙基元 tooverify，授與存取權。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-126">hello resource server validates hello security token tooverify that access can be granted.</span></span>
6. <span data-ttu-id="b6e6b-127">hello 應用程式會定期重新整理 hello 安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-127">hello app periodically refreshes hello security token.</span></span>

<!-- TODO: Need a page for libraries toolink too-->
<span data-ttu-id="b6e6b-128">這些步驟可能稍有根據您要建置的應用程式的 hello 類型會不同。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-128">These steps can differ slightly based on hello type of app you're building.</span></span> <span data-ttu-id="b6e6b-129">開放原始碼程式庫可以讓您解決 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-129">Open source libraries can address hello details for you.</span></span>

## <a name="web-apps"></a><span data-ttu-id="b6e6b-130">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b6e6b-130">Web apps</span></span>
<span data-ttu-id="b6e6b-131">對於裝載於伺服器且透過瀏覽器存取的 Web 應用程式 (包括 .NET、PHP、Java、Ruby、Python、Node.js)，Azure AD B2C 支援以 [OpenID Connect](active-directory-b2c-reference-protocols.md) 完成一切使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-131">For web apps (including .NET, PHP, Java, Ruby, Python, and Node.js) that are hosted on a server and accessed through a browser, Azure AD B2C supports [OpenID Connect](active-directory-b2c-reference-protocols.md) for all user experiences.</span></span> <span data-ttu-id="b6e6b-132">這包括登入、註冊和設定檔管理。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-132">This includes sign-in, sign-up, and profile management.</span></span> <span data-ttu-id="b6e6b-133">在 Azure AD B2C hello 實作中的 OpenID Connect，您 web 應用程式會藉由發出驗證要求 tooAzure AD 起始這些使用者的體驗。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-133">In hello Azure AD B2C implementation of OpenID Connect, your web app initiates these user experiences by issuing authentication requests tooAzure AD.</span></span> <span data-ttu-id="b6e6b-134">hello 要求的 hello 結果是`id_token`。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-134">hello result of hello request is an `id_token`.</span></span> <span data-ttu-id="b6e6b-135">這個安全性權杖表示 hello 使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-135">This security token represents hello user's identity.</span></span> <span data-ttu-id="b6e6b-136">它也提供的宣告 hello 表單中的 hello 使用者的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="b6e6b-136">It also provides information about hello user in hello form of claims:</span></span>

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

<span data-ttu-id="b6e6b-137">深入了解 hello 類型的權杖與宣告的可用 tooan 應用程式在 hello [B2C 權杖參照](active-directory-b2c-reference-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-137">Learn more about hello types of tokens and claims available tooan app in hello [B2C token reference](active-directory-b2c-reference-tokens.md).</span></span>

<span data-ttu-id="b6e6b-138">在 Web 應用程式中，每次執行 [原則](active-directory-b2c-reference-policies.md) 會採用下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="b6e6b-138">In a web app, each execution of a [policy](active-directory-b2c-reference-policies.md) takes these high-level steps:</span></span>

![Web 應用程式泳道映像](./media/active-directory-b2c-apps/webapp.png)

<span data-ttu-id="b6e6b-140">驗證的 hello`id_token`使用接收自 Azure AD 的公開金鑰簽署金鑰是 hello 使用者足夠 tooverify hello 識別。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-140">Validation of hello `id_token` by using a public signing key that is received from Azure AD is sufficient tooverify hello identity of hello user.</span></span> <span data-ttu-id="b6e6b-141">這也可以設定可以在後續頁面要求上的使用的 tooidentify hello 使用者工作階段 cookie。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-141">This also sets a session cookie that can be used tooidentify hello user on subsequent page requests.</span></span>

<span data-ttu-id="b6e6b-142">toosee 此案例中的動作，再試一次的其中一個 hello web 應用程式登入程式碼範例中我們[開始使用 > 一節](active-directory-b2c-overview.md#get-started)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-142">toosee this scenario in action, try one of hello web app sign-in code samples in our [Getting started section](active-directory-b2c-overview.md#get-started).</span></span>

<span data-ttu-id="b6e6b-143">加法 toofacilitating 簡單登入，在 web 伺服器應用程式可能也需要 tooaccess 後端 web 服務。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-143">In addition toofacilitating simple sign-in, a web server app might also need tooaccess a back-end web service.</span></span> <span data-ttu-id="b6e6b-144">在此情況下，hello web 應用程式可以執行稍有不同[OpenID Connect 流程](active-directory-b2c-reference-oidc.md)和使用授權碼取得權杖和重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-144">In this case, hello web app can perform a slightly different [OpenID Connect flow](active-directory-b2c-reference-oidc.md) and acquire tokens by using authorization codes and refresh tokens.</span></span> <span data-ttu-id="b6e6b-145">此案例中所述 hello 下列[Web 應用程式開發介面 > 一節](#web-apis)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-145">This scenario is depicted in hello following [Web APIs section](#web-apis).</span></span>

<!--, and in our [WebApp-WebAPI Getting started topic](active-directory-b2c-devquickstarts-web-api-dotnet.md).-->

## <a name="web-apis"></a><span data-ttu-id="b6e6b-146">Web API</span><span class="sxs-lookup"><span data-stu-id="b6e6b-146">Web APIs</span></span>
<span data-ttu-id="b6e6b-147">您可以使用 Azure AD B2C toosecure web 服務，例如您的應用程式 rest 式 web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-147">You can use Azure AD B2C toosecure web services such as your app's RESTful web API.</span></span> <span data-ttu-id="b6e6b-148">Web Api 可以使用 OAuth 2.0 toosecure 其資料，使用語彙基元的內送 HTTP 要求時進行驗證。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-148">Web APIs can use OAuth 2.0 toosecure their data, by authenticating incoming HTTP requests using tokens.</span></span> <span data-ttu-id="b6e6b-149">hello 的 web API 的呼叫端將附加 hello 授權標頭的 HTTP 要求中的語彙基元：</span><span class="sxs-lookup"><span data-stu-id="b6e6b-149">hello caller of a web API appends a token in hello authorization header of an HTTP request:</span></span>

```
GET /api/items HTTP/1.1
Host: www.mywebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6...
Accept: application/json
...
```

<span data-ttu-id="b6e6b-150">hello web API 可以使用 hello 語彙基元 tooverify hello API 呼叫者的身分識別與 tooextract 資訊編碼 hello 權杖中的宣告中的 hello 呼叫端。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-150">hello web API can then use hello token tooverify hello API caller's identity and tooextract information about hello caller from claims that are encoded in hello token.</span></span> <span data-ttu-id="b6e6b-151">深入了解 hello 類型的權杖與宣告的可用 tooan 應用程式在 hello [Azure AD B2C 權杖參照](active-directory-b2c-reference-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-151">Learn more about hello types of tokens and claims available tooan app in hello [Azure AD B2C token reference](active-directory-b2c-reference-tokens.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b6e6b-152">Azure AD B2C 目前僅支援以各自已知的用戶端存取的 Web API。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-152">Azure AD B2C currently supports only web APIs that are accessed by their own well-known clients.</span></span> <span data-ttu-id="b6e6b-153">例如，完整的應用程式可能包括 iOS 應用程式、Android 應用程式和後端 Web API。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-153">For instance, your complete app may include an iOS app, an Android app, and a back-end web API.</span></span> <span data-ttu-id="b6e6b-154">完全支援這種架構。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-154">This architecture is fully supported.</span></span> <span data-ttu-id="b6e6b-155">可讓協力廠商用戶端，例如另一個 iOS 應用程式、 tooaccess hello 相同的 web API 目前不支援。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-155">Allowing a partner client, such as another iOS app, tooaccess hello same web API is not currently supported.</span></span> <span data-ttu-id="b6e6b-156">所有應用程式完整 hello 元件必須共用單一應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-156">All of hello components of your complete app must share a single application ID.</span></span>
>
>

<span data-ttu-id="b6e6b-157">Web API 接收的權杖可以來自許多類型的應用程式，包括 Web 應用程式、桌面和行動應用程式、單一頁面應用程式、伺服器端精靈，以及其他 Web API。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-157">A web API can receive tokens from many types of clients, including web apps, desktop and mobile apps, single page apps, server-side daemons, and other web APIs.</span></span> <span data-ttu-id="b6e6b-158">Web 應用程式中呼叫 web API 的 hello 完整流程的範例如下：</span><span class="sxs-lookup"><span data-stu-id="b6e6b-158">Here's an example of hello complete flow for a web app that calls a web API:</span></span>

![Web 應用程式 Web API 泳道映像](./media/active-directory-b2c-apps/webapi.png)

<span data-ttu-id="b6e6b-160">深入了解授權碼、 重新整理權杖和 hello 步驟來取得權杖，toolearn 閱讀 hello [OAuth 2.0 通訊協定](active-directory-b2c-reference-oauth-code.md)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-160">toolearn more about authorization codes, refresh tokens, and hello steps for getting tokens, read about hello [OAuth 2.0 protocol](active-directory-b2c-reference-oauth-code.md).</span></span>

<span data-ttu-id="b6e6b-161">如何使用 Azure AD B2C 簽出 hello toosecure web API web 應用程式開發介面中的教學課程的 toolearn 我們[開始使用 > 一節](active-directory-b2c-overview.md#get-started)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-161">toolearn how toosecure a web API by using Azure AD B2C, check out hello web API tutorials in our [Getting started section](active-directory-b2c-overview.md#get-started).</span></span>

## <a name="mobile-and-native-apps"></a><span data-ttu-id="b6e6b-162">行動和原生應用程式</span><span class="sxs-lookup"><span data-stu-id="b6e6b-162">Mobile and native apps</span></span>
<span data-ttu-id="b6e6b-163">在裝置，行動和桌面應用程式，例如安裝應用程式通常需要 tooaccess 後端服務或代表使用者的 web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-163">Apps that are installed on devices, such as mobile and desktop apps, often need tooaccess back-end services or web APIs on behalf of users.</span></span> <span data-ttu-id="b6e6b-164">您可以加入自訂身分識別管理體驗 tooyour 原生應用程式，並安全地呼叫後端服務使用 Azure AD B2C 和 hello [OAuth 2.0 授權碼流程](active-directory-b2c-reference-oauth-code.md)。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-164">You can add customized identity management experiences tooyour native apps and securely call back-end services by using Azure AD B2C and hello [OAuth 2.0 authorization code flow](active-directory-b2c-reference-oauth-code.md).</span></span>  

<span data-ttu-id="b6e6b-165">此流程，在 hello 應用程式會執行[原則](active-directory-b2c-reference-policies.md)並接收`authorization_code`從 Azure AD 之後 hello 使用者完成 hello 原則。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-165">In this flow, hello app executes [policies](active-directory-b2c-reference-policies.md) and receives an `authorization_code` from Azure AD after hello user completes hello policy.</span></span> <span data-ttu-id="b6e6b-166">hello`authorization_code`代表 hello 代表 hello 使用者目前登入應用程式的權限 toocall 後端服務。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-166">hello `authorization_code` represents hello app's permission toocall back-end services on behalf of hello user who is currently signed in.</span></span> <span data-ttu-id="b6e6b-167">hello 應用程式可以接著交換 hello`authorization_code`在 hello 幕後`id_token`和`refresh_token`。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-167">hello app can then exchange hello `authorization_code` in hello background for an `id_token` and a `refresh_token`.</span></span>  <span data-ttu-id="b6e6b-168">hello 應用程式可以使用 hello `id_token` tooauthenticate tooa 後端中的 web API HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-168">hello app can use hello `id_token` tooauthenticate tooa back-end web API in HTTP requests.</span></span> <span data-ttu-id="b6e6b-169">它也可以使用 hello`refresh_token`新 tooget`id_token`舊何時到期。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-169">It can also use hello `refresh_token` tooget a new `id_token` when an older one expires.</span></span>

> [!NOTE]
> <span data-ttu-id="b6e6b-170">Azure AD B2C 目前支援權杖，這是使用的 tooaccess 應用程式本身的後端 web 服務。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-170">Azure AD B2C currently supports only tokens that are used tooaccess an app's own back-end web service.</span></span> <span data-ttu-id="b6e6b-171">例如，完整的應用程式可能包括 iOS 應用程式、Android 應用程式和後端 Web API。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-171">For instance, your complete app may include an iOS app, an Android app, and a back-end web API.</span></span> <span data-ttu-id="b6e6b-172">完全支援這種架構。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-172">This architecture is fully supported.</span></span> <span data-ttu-id="b6e6b-173">目前不支援可讓您的 iOS 應用程式 tooaccess 協力廠商 web API，使用 OAuth 2.0 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-173">Allowing your iOS app tooaccess a partner web API by using OAuth 2.0 access tokens is not currently supported.</span></span> <span data-ttu-id="b6e6b-174">所有應用程式完整 hello 元件必須共用單一應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-174">All of hello components of your complete app must share a single application ID.</span></span>
>
>

![原生應用程式泳道映像](./media/active-directory-b2c-apps/native.png)

## <a name="current-limitations"></a><span data-ttu-id="b6e6b-176">目前的限制</span><span class="sxs-lookup"><span data-stu-id="b6e6b-176">Current limitations</span></span>
<span data-ttu-id="b6e6b-177">Azure AD B2C 目前不支援下列類型的應用程式，hello，但是可以在 hello 藍圖。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-177">Azure AD B2C does not currently support hello following types of apps, but they are on hello roadmap.</span></span> 

### <a name="daemonsserver-side-apps"></a><span data-ttu-id="b6e6b-178">精靈/伺服器端應用程式</span><span class="sxs-lookup"><span data-stu-id="b6e6b-178">Daemons/server-side apps</span></span>
<span data-ttu-id="b6e6b-179">應用程式包含長時間執行的處理序，或沒有 hello 使用者存在，運作也需要 tooaccess 保護的資源，例如 web 應用程式開發介面的方法。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-179">Apps that contain long-running processes or that operate without hello presence of a user also need a way tooaccess secured resources such as web APIs.</span></span> <span data-ttu-id="b6e6b-180">這些應用程式可驗證及使用 hello 應用程式的身分識別 （而非使用者的委派的識別），並使用 hello OAuth 2.0 用戶端認證流程取得的權杖。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-180">These apps can authenticate and get tokens by using hello app's identity (rather than a user's delegated identity) and by using hello OAuth 2.0 client credentials flow.</span></span>

<span data-ttu-id="b6e6b-181">Azure AD B2C 目前不支援此流程。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-181">This flow is not currently supported by Azure AD B2C.</span></span> <span data-ttu-id="b6e6b-182">這些應用程式只有在互動式使用者流程發生之後，才取得權杖。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-182">These apps can get tokens only after an interactive user flow has occurred.</span></span>

### <a name="web-api-chains-on-behalf-of-flow"></a><span data-ttu-id="b6e6b-183">Web API 鏈結 (代理者流程)</span><span class="sxs-lookup"><span data-stu-id="b6e6b-183">Web API chains (on-behalf-of flow)</span></span>
<span data-ttu-id="b6e6b-184">許多架構包含 web API 需要 toocall 另一個下游 web API，其中同時受到 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-184">Many architectures include a web API that needs toocall another downstream web API, where both are secured by Azure AD B2C.</span></span> <span data-ttu-id="b6e6b-185">此案例常見於有 Web API 後端的原生用戶端。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-185">This scenario is common in native clients that have a Web API back-end.</span></span> <span data-ttu-id="b6e6b-186">然後，這會呼叫 Microsoft 線上服務，例如 hello Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-186">This then calls a Microsoft online service such as hello Azure AD Graph API.</span></span>

<span data-ttu-id="b6e6b-187">使用 hello OAuth 2.0 JWT bearer 認證授與，也稱為 hello 代表的流程，可以支援此鏈結的 web API 」 案例。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-187">This chained web API scenario can be supported by using hello OAuth 2.0 JWT bearer credential grant, also known as hello on-behalf-of flow.</span></span>  <span data-ttu-id="b6e6b-188">不過，hello 上-代表 」 流程目前尚未實作 Azure AD B2C hello 中。</span><span class="sxs-lookup"><span data-stu-id="b6e6b-188">However, hello on-behalf-of flow is not currently implemented in hello Azure AD B2C.</span></span>
