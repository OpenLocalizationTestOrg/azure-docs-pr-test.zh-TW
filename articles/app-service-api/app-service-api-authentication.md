---
title: "aaaAuthentication 和 Azure App Service 中的應用程式開發介面應用程式的授權 |Microsoft 文件"
description: "深入了解 Azure App Service API 應用程式提供的 hello 驗證和授權服務。"
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: d620b53a-5a6f-41c9-84c7-f7ef5ff02ae7
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: alkarche
ms.openlocfilehash: 6d26754b8b606ec232a74768787922ea80577c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a><span data-ttu-id="c3196-103">Azure App Service 中的 API Apps 驗證與授權</span><span class="sxs-lookup"><span data-stu-id="c3196-103">Authentication and authorization for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="c3196-104">概觀</span><span class="sxs-lookup"><span data-stu-id="c3196-104">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="c3196-105">本主題將會移轉的 tooa 合併[應用程式服務驗證 / 授權](../app-service/app-service-authentication-overview.md)主題，其中涵蓋了網頁、 行動裝置版及 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3196-105">This topic will be migrated tooa consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="c3196-106">Azure App Service 提供內建的驗證與授權服務，可實作 [OAuth 2.0](#oauth) 和 [OpenID Connect](#oauth)。</span><span class="sxs-lookup"><span data-stu-id="c3196-106">Azure App Service offers built-in authentication and authorization services that implement [OAuth 2.0](#oauth) and [OpenID Connect](#oauth).</span></span> <span data-ttu-id="c3196-107">本文說明 hello 和服務可供 Azure App Service 中的應用程式開發介面應用程式的選項。</span><span class="sxs-lookup"><span data-stu-id="c3196-107">This article describes hello services and options that are available for API Apps in Azure App Service.</span></span>

<span data-ttu-id="c3196-108">hello 下列圖表將說明幾個重要特性的應用程式服務驗證：</span><span class="sxs-lookup"><span data-stu-id="c3196-108">hello following diagram illustrates some key characteristics of App Service authentication:</span></span>

* <span data-ttu-id="c3196-109">它會前置處理傳入的 API 要求，這表示它能使用 App Service 所支援的任何語言或架構。</span><span class="sxs-lookup"><span data-stu-id="c3196-109">It preprocesses incoming API requests, which means it works with any language or framework supported by App Service.</span></span>
* <span data-ttu-id="c3196-110">它提供幾個選項用於多少驗證正常運作，您想要 toodo 自己的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="c3196-110">It gives you several options for how much authentication work you want toodo in your own code.</span></span>
* <span data-ttu-id="c3196-111">它適用於使用者與服務帳戶驗證。</span><span class="sxs-lookup"><span data-stu-id="c3196-111">It works for both end user and service account authentication.</span></span> 
* <span data-ttu-id="c3196-112">它支援五個識別提供者：Azure Active Directory、Facebook、Google、Twitter 和 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c3196-112">It supports five identity providers: Azure Active Directory, Facebook, Google, Twitter, and Microsoft Account.</span></span>
* <span data-ttu-id="c3196-113">它適用於 hello 相同應用程式開發介面應用程式、 Web 應用程式，和行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3196-113">It works hello same for API Apps, Web Apps, and Mobile Apps.</span></span>

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a><span data-ttu-id="c3196-114">不限語言</span><span class="sxs-lookup"><span data-stu-id="c3196-114">Language agnostic</span></span>
<span data-ttu-id="c3196-115">要求到達應用程式開發介面應用程式，這表示任何語言或架構所撰寫的應用程式開發介面應用程式的 hello 驗證功能的運作之前，就會發生應用程式服務驗證處理。</span><span class="sxs-lookup"><span data-stu-id="c3196-115">App Service authentication processing happens before requests reach your API app, which means that hello authentication features work for API apps written in any language or framework.</span></span>  <span data-ttu-id="c3196-116">您可以根據 ASP.NET、Java、Node.js 或任何 App Service 所支援的架構建立 API。</span><span class="sxs-lookup"><span data-stu-id="c3196-116">Your API can be based on ASP.NET, Java, Node.js, or any framework that App Service supports.</span></span>

<span data-ttu-id="c3196-117">應用程式服務傳送的 hello JSON web 權杖 (JWT) 的 HTTP 要求，hello 授權標頭中，並以任何語言或架構所撰寫的程式碼可以取得 hello 所需要的資訊從 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c3196-117">App Service passes on hello JSON web token (JWT) in hello Authorization header of an HTTP request, and code written in any language or framework can get hello information it needs from hello token.</span></span> <span data-ttu-id="c3196-118">此外，應用程式服務可讓您更容易存取 toohello 最常使用的宣告設定特殊的標頭，hello 如下：</span><span class="sxs-lookup"><span data-stu-id="c3196-118">In addition, App Service gives you easier access toohello most commonly used claims by setting some special headers, such as hello following:</span></span>

* <span data-ttu-id="c3196-119">X-MS-CLIENT-PRINCIPAL-NAME</span><span class="sxs-lookup"><span data-stu-id="c3196-119">X-MS-CLIENT-PRINCIPAL-NAME</span></span>
* <span data-ttu-id="c3196-120">X-MS-CLIENT-PRINCIPAL-ID</span><span class="sxs-lookup"><span data-stu-id="c3196-120">X-MS-CLIENT-PRINCIPAL-ID</span></span>
* <span data-ttu-id="c3196-121">X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN</span><span class="sxs-lookup"><span data-stu-id="c3196-121">X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN</span></span>
* <span data-ttu-id="c3196-122">X-MS-TOKEN-FACEBOOK-EXPIRES-ON</span><span class="sxs-lookup"><span data-stu-id="c3196-122">X-MS-TOKEN-FACEBOOK-EXPIRES-ON</span></span>

<span data-ttu-id="c3196-123">在.NET API 中，您可以使用 hello`Authorize`屬性，然後更細緻的授權，您可以輕鬆地撰寫程式碼根據的宣告的宣告資訊會為您填入.NET 類別中。</span><span class="sxs-lookup"><span data-stu-id="c3196-123">In a .NET API, you can use hello `Authorize` attribute, and for fine-grained authorization you can easily write code based on claims because claims information is populated for you in .NET classes.</span></span>

## <a name="multiple-protection-options"></a><span data-ttu-id="c3196-124">多個保護選項</span><span class="sxs-lookup"><span data-stu-id="c3196-124">Multiple protection options</span></span>
<span data-ttu-id="c3196-125">App Service 可以防止匿名 HTTP 要求進入您的 API 應用程式、傳遞所有要求並驗證要求中所包含的權杖，或是不採取任何動作就放行所有要求：</span><span class="sxs-lookup"><span data-stu-id="c3196-125">App Service can prevent anonymous HTTP requests from reaching your API app, it can pass on all requests and validate tokens for requests that include them, or it can let through all requests without taking any action on them:</span></span>

1. <span data-ttu-id="c3196-126">只有已驗證的要求 tooreach 可讓您 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3196-126">Allow only authenticated requests tooreach your API app.</span></span>
   
    <span data-ttu-id="c3196-127">如果從瀏覽器中收到的匿名要求，則應用程式服務將會重新導向 tooa hello 驗證提供者的登入頁面 (Azure AD、 Google、 Twitter 等)，您選擇。</span><span class="sxs-lookup"><span data-stu-id="c3196-127">If an anonymous request is received from a browser, App Service will redirect tooa logon page for hello authentication provider (Azure AD, Google, Twitter, etc.) that you choose.</span></span> 
   
    <span data-ttu-id="c3196-128">使用此選項，您不再需要 toowrite 任何驗證程式碼完全應用程式中，而授權程式碼已經過簡化，因為 hello HTTP 標頭中所提供的 hello 最重要的宣告。</span><span class="sxs-lookup"><span data-stu-id="c3196-128">With this option, you don't need toowrite any authentication code at all in your app, and authorization code is simplified because hello most important claims are provided in hello HTTP headers.</span></span>
2. <span data-ttu-id="c3196-129">允許所有要求 tooreach 應用程式的應用程式開發介面，但驗證已驗證的要求，並傳遞 hello HTTP 標頭中的驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="c3196-129">Allow all requests tooreach your API app, but validate authenticated requests and pass along authentication information in hello HTTP headers.</span></span>
   
    <span data-ttu-id="c3196-130">此選項可讓您更有彈性地處理匿名要求，但是您有 toowrite 程式碼，如果您希望 tooprevent 匿名使用者使用您的 API。</span><span class="sxs-lookup"><span data-stu-id="c3196-130">This option gives you more flexibility in handling anonymous requests, but you have toowrite code if you want tooprevent anonymous users from using your API.</span></span> <span data-ttu-id="c3196-131">Hello 最受歡迎的宣告會傳入 hello 標頭的 HTTP 要求，因為授權碼是相當簡單。</span><span class="sxs-lookup"><span data-stu-id="c3196-131">Since hello most popular claims are passed in hello headers of HTTP requests, authorization code is relatively simple.</span></span>
3. <span data-ttu-id="c3196-132">允許所有要求 tooreach 您的 API，hello 要求中的驗證資訊採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="c3196-132">Allow all requests tooreach your API, take no action on authentication information in hello requests.</span></span>
   
    <span data-ttu-id="c3196-133">這個選項會將驗證與授權完全向上 tooyour 應用程式程式碼的 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="c3196-133">This option leaves hello tasks of authentication and authorization entirely up tooyour application code.</span></span>

<span data-ttu-id="c3196-134">在 hello [Azure 入口網站](https://portal.azure.com/)，選取您想要在 hello 的 hello 選項**驗證 / 授權**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c3196-134">In hello [Azure portal](https://portal.azure.com/), you select hello option you want on hello **Authentication / Authorization** blade.</span></span>

![](./media/app-service-api-authentication/authblade.png)

<span data-ttu-id="c3196-135">使用選項 1 和 2，請開啟**應用程式服務驗證**，在 hello**當要求未經驗證的動作 tootake**下拉式清單中選擇**登入**或**允許要求 （無動作）**。</span><span class="sxs-lookup"><span data-stu-id="c3196-135">For options 1 and 2, turn on **App Service Authentication**, and in hello **Action tootake when request is not authenticated** drop-down list choose **Log in** or **Allow request (no action)**.</span></span>  <span data-ttu-id="c3196-136">如果您選擇**登入**，您有 toochoose 驗證提供者，並設定該提供者。</span><span class="sxs-lookup"><span data-stu-id="c3196-136">If you choose **Log in**, you have toochoose an authentication provider and configure that provider.</span></span>

![](./media/app-service-api-authentication/actiontotake.png)

<span data-ttu-id="c3196-137">如需詳細資訊 tooconfigure 驗證，請參閱[如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="c3196-137">For detailed information about how tooconfigure authentication, see [How tooconfigure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="c3196-138">hello 文章適用 tooAPI 應用程式，以及行動裝置的應用程式，而且連結 tooother 文章中的 hello 其他驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="c3196-138">hello article applies tooAPI apps as well as mobile apps, and it links tooother articles for hello other authentication providers.</span></span>

## <span data-ttu-id="c3196-139"><a id="internal"></a> 服務帳戶驗證</span><span class="sxs-lookup"><span data-stu-id="c3196-139"><a id="internal"></a> Service account authentication</span></span>
<span data-ttu-id="c3196-140">應用程式服務驗證適用於這類內部案例從一個應用程式開發介面應用程式 tooanother API 應用程式呼叫。</span><span class="sxs-lookup"><span data-stu-id="c3196-140">App Service authentication works for internal scenarios such as for calling from one API app tooanother API app.</span></span> <span data-ttu-id="c3196-141">在此案例中，您可以使用服務帳戶認證 (而非使用者認證) 來取得權杖。</span><span class="sxs-lookup"><span data-stu-id="c3196-141">In this scenario you get a token by using credentials for a service account instead of end user credentials.</span></span> <span data-ttu-id="c3196-142">服務帳戶在 Azure Active Directory 中也稱為 *服務主體* ，使用這類帳戶的驗證也稱為服務對服務案例。</span><span class="sxs-lookup"><span data-stu-id="c3196-142">A service account is also known as a *service principal* in Azure Active Directory, and authentication using such an account is also known as a service-to-service scenario.</span></span> 

<span data-ttu-id="c3196-143">服務對服務案例中，保護 hello 呼叫 API 應用程式使用 Azure Active Directory，並提供 AAD 服務主體的授權權杖，當您呼叫 hello API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3196-143">For service-to-service scenarios, protect hello called API app by using Azure Active Directory, and provide an AAD service principal authorization token when you call hello API app.</span></span> <span data-ttu-id="c3196-144">您可以取得權杖，以提供 hello 用戶端識別碼和機密的 hello AAD 應用程式的用戶端。</span><span class="sxs-lookup"><span data-stu-id="c3196-144">You get a token by providing hello client ID and client secret from hello AAD application.</span></span> <span data-ttu-id="c3196-145">沒有特殊的僅限 Azure 程式碼是必要項目，例如使用的 toobe true，表示處理 hello 行動服務 Zumo 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="c3196-145">No special Azure-only code is required, such as used toobe true for handling hello Mobile Services Zumo token.</span></span> <span data-ttu-id="c3196-146">此案例中使用 ASP.NET 應用程式開發介面應用程式的範例 hello 教學課程涵蓋[API 應用程式的服務主體驗證](app-service-api-dotnet-service-principal-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="c3196-146">An example of this scenario using ASP.NET API apps is covered by hello tutorial [Service principal authentication for API Apps](app-service-api-dotnet-service-principal-auth.md).</span></span>

<span data-ttu-id="c3196-147">如果您想 toohandle 服務對服務案例不會使用應用程式服務驗證時，您可以使用用戶端憑證驗證或基本驗證。</span><span class="sxs-lookup"><span data-stu-id="c3196-147">If you want toohandle a service-to-service scenario without using App Service authentication, you can use client certificates or basic authentication.</span></span> <span data-ttu-id="c3196-148">在 Azure 中的用戶端憑證的相關資訊，請參閱[如何 tooConfigure TLS 相互驗證 Web 應用程式](../app-service-web/app-service-web-configure-tls-mutual-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="c3196-148">For information about client certificates in Azure, see [How tooConfigure TLS Mutual Authentication for Web Apps](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span> <span data-ttu-id="c3196-149">如需 ASP.NET 中的基本驗證相關資訊，請參閱 [ASP.NET Web API 2 中的驗證篩選](http://www.asp.net/web-api/overview/security/authentication-filters)。</span><span class="sxs-lookup"><span data-stu-id="c3196-149">For information about basic authentication in ASP.NET, see [Authentication Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).</span></span>

<span data-ttu-id="c3196-150">從應用程式服務的邏輯應用程式 tooan API 應用程式的服務帳戶驗證是特殊案例，說明在[使用您裝載邏輯應用程式的 App Service 上的自訂 API](../logic-apps/logic-apps-custom-hosted-api.md)。</span><span class="sxs-lookup"><span data-stu-id="c3196-150">Service account authentication from an App Service logic app tooan API app is a special case that is explained in [Using your custom API hosted on App Service with Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).</span></span>

## <a name="mobile-client-authentication"></a><span data-ttu-id="c3196-151">行動用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="c3196-151">Mobile client authentication</span></span>
<span data-ttu-id="c3196-152">如需有關資訊 toohandle 驗證來自行動用戶端，請參閱 hello[驗證行動裝置應用程式的文件](../app-service-mobile/app-service-mobile-ios-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="c3196-152">For information about how toohandle authentication from mobile clients, see hello [documentation on authentication for mobile apps](../app-service-mobile/app-service-mobile-ios-get-started-users.md).</span></span> <span data-ttu-id="c3196-153">應用程式服務驗證的運作方式 hello 行動裝置應用程式及 API 應用程式相同的方式。</span><span class="sxs-lookup"><span data-stu-id="c3196-153">App Service authentication works hello same way for mobile apps and API apps.</span></span>

## <a name="more-information"></a><span data-ttu-id="c3196-154">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c3196-154">More information</span></span>
<span data-ttu-id="c3196-155">如需驗證和授權的 Azure 應用程式服務的詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="c3196-155">For more information about authentication and authorization in Azure App Service, see hello following resources:</span></span>

* [<span data-ttu-id="c3196-156">擴充 App Service 驗證/授權</span><span class="sxs-lookup"><span data-stu-id="c3196-156">Expanding App Service authentication / authorization</span></span>](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* <span data-ttu-id="c3196-157">[如何 tooconfigure 您 App Service 應用程式 toouse 的 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)（包括連結在 hello hello 頁面最上方的其他驗證提供者）。</span><span class="sxs-lookup"><span data-stu-id="c3196-157">[How tooconfigure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (Includes links for other authentication providers at hello top of hello page.)</span></span> 

<span data-ttu-id="c3196-158">如需 OAuth 2.0、 OpenID Connect 和 JSON Web Token (JWT) 的詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="c3196-158">For more information about OAuth 2.0, OpenID Connect, and JSON Web Tokens (JWT), see hello following resources.</span></span>

* [<span data-ttu-id="c3196-159">開始使用 OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="c3196-159">Getting started with OAuth 2.0</span></span>](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [<span data-ttu-id="c3196-160">簡介 tooOAuth2 OpenID Connect 和 JSON Web 權杖 (JWT)-Pluralsight 課程</span><span class="sxs-lookup"><span data-stu-id="c3196-160">Introduction tooOAuth2, OpenID Connect and JSON Web Tokens (JWT) - Pluralsight Course</span></span>](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [<span data-ttu-id="c3196-161">在 ASP.NET 中建置和保護多個用戶端的 RESTful API - Pluralsight 課程</span><span class="sxs-lookup"><span data-stu-id="c3196-161">Building and Securing a RESTful API for Multiple Clients in ASP.NET - Pluralsight course</span></span>](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

<span data-ttu-id="c3196-162">如需 Azure Active Directory 的詳細資訊，請參閱下列資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="c3196-162">For more information about Azure Active Directory, see hello following resources.</span></span>

* [<span data-ttu-id="c3196-163">Azure AD 案例</span><span class="sxs-lookup"><span data-stu-id="c3196-163">Azure AD scenarios</span></span>](http://aka.ms/aadscenarios)
* [<span data-ttu-id="c3196-164">Azure AD 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="c3196-164">Azure AD developers' guide</span></span>](http://aka.ms/aaddev)
* [<span data-ttu-id="c3196-165">Azure AD 範例</span><span class="sxs-lookup"><span data-stu-id="c3196-165">Azure AD samples</span></span>](http://aka.ms/aadsamples)

## <a name="next-steps"></a><span data-ttu-id="c3196-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3196-166">Next steps</span></span>
<span data-ttu-id="c3196-167">本文說明了可用於 API 應用程式之 App Service 的驗證和授權功能。</span><span class="sxs-lookup"><span data-stu-id="c3196-167">This article has explained authentication and authorization features of App Service that you can use for API apps.</span></span> <span data-ttu-id="c3196-168">hello hello 取得下一個教學課程如何啟動系列的節目 tooimplement [App Service API 應用程式中的使用者驗證](app-service-api-dotnet-user-principal-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="c3196-168">hello next tutorial in hello getting started series shows how tooimplement [user authentication in App Service API Apps](app-service-api-dotnet-user-principal-auth.md).</span></span>

