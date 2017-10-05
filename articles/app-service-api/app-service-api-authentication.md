---
title: "Azure App Service 中的 API Apps 驗證與授權 | Microsoft Docs"
description: "了解 Azure App Service 針對 API Apps 所提供的驗證和授權服務。"
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
ms.openlocfilehash: f9fd533dfbd54517232f9dae5000ed4779baebd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-api-apps-in-azure-app-service"></a><span data-ttu-id="a914c-103">Azure App Service 中的 API Apps 驗證與授權</span><span class="sxs-lookup"><span data-stu-id="a914c-103">Authentication and authorization for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="a914c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="a914c-104">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="a914c-105">本主題將移轉至合併的 [App Service 驗證/授權](../app-service/app-service-authentication-overview.md) 主題，其中涵蓋 Web、Mobile 和 API Apps。</span><span class="sxs-lookup"><span data-stu-id="a914c-105">This topic will be migrated to a consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="a914c-106">Azure App Service 提供內建的驗證與授權服務，可實作 [OAuth 2.0](#oauth) 和 [OpenID Connect](#oauth)。</span><span class="sxs-lookup"><span data-stu-id="a914c-106">Azure App Service offers built-in authentication and authorization services that implement [OAuth 2.0](#oauth) and [OpenID Connect](#oauth).</span></span> <span data-ttu-id="a914c-107">本文描述 Azure App Service 中的 API Apps 可用的服務和選項。</span><span class="sxs-lookup"><span data-stu-id="a914c-107">This article describes the services and options that are available for API Apps in Azure App Service.</span></span>

<span data-ttu-id="a914c-108">下圖說明 App Service 驗證的幾個重要特性：</span><span class="sxs-lookup"><span data-stu-id="a914c-108">The following diagram illustrates some key characteristics of App Service authentication:</span></span>

* <span data-ttu-id="a914c-109">它會前置處理傳入的 API 要求，這表示它能使用 App Service 所支援的任何語言或架構。</span><span class="sxs-lookup"><span data-stu-id="a914c-109">It preprocesses incoming API requests, which means it works with any language or framework supported by App Service.</span></span>
* <span data-ttu-id="a914c-110">它會提供您幾個選項讓您決定要在自有程式碼中進行多少驗證工作。</span><span class="sxs-lookup"><span data-stu-id="a914c-110">It gives you several options for how much authentication work you want to do in your own code.</span></span>
* <span data-ttu-id="a914c-111">它適用於使用者與服務帳戶驗證。</span><span class="sxs-lookup"><span data-stu-id="a914c-111">It works for both end user and service account authentication.</span></span> 
* <span data-ttu-id="a914c-112">它支援五個識別提供者：Azure Active Directory、Facebook、Google、Twitter 和 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a914c-112">It supports five identity providers: Azure Active Directory, Facebook, Google, Twitter, and Microsoft Account.</span></span>
* <span data-ttu-id="a914c-113">它在 API Apps、Web Apps 和 Mobile Apps 的作用都相同。</span><span class="sxs-lookup"><span data-stu-id="a914c-113">It works the same for API Apps, Web Apps, and Mobile Apps.</span></span>

![](./media/app-service-api-authentication/api-apps-overview.png)

## <a name="language-agnostic"></a><span data-ttu-id="a914c-114">不限語言</span><span class="sxs-lookup"><span data-stu-id="a914c-114">Language agnostic</span></span>
<span data-ttu-id="a914c-115">App Service 驗證處理程序是在要求進入 API 應用程式之前進行，這表示不管 API 應用程式是以任何語言或架構所撰寫，都能適用驗證功能。</span><span class="sxs-lookup"><span data-stu-id="a914c-115">App Service authentication processing happens before requests reach your API app, which means that the authentication features work for API apps written in any language or framework.</span></span>  <span data-ttu-id="a914c-116">您可以根據 ASP.NET、Java、Node.js 或任何 App Service 所支援的架構建立 API。</span><span class="sxs-lookup"><span data-stu-id="a914c-116">Your API can be based on ASP.NET, Java, Node.js, or any framework that App Service supports.</span></span>

<span data-ttu-id="a914c-117">App Service 會在 HTTP 要求的授權標頭中傳遞 JSON Web 權杖 (JWT)，以任何語言或架構撰寫的程式碼都可以從權杖中取得所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="a914c-117">App Service passes on the JSON web token (JWT) in the Authorization header of an HTTP request, and code written in any language or framework can get the information it needs from the token.</span></span> <span data-ttu-id="a914c-118">此外，App Service 會透過設定某些特殊標頭 (如下所示)，讓您更容易地存取最常使用的宣告：</span><span class="sxs-lookup"><span data-stu-id="a914c-118">In addition, App Service gives you easier access to the most commonly used claims by setting some special headers, such as the following:</span></span>

* <span data-ttu-id="a914c-119">X-MS-CLIENT-PRINCIPAL-NAME</span><span class="sxs-lookup"><span data-stu-id="a914c-119">X-MS-CLIENT-PRINCIPAL-NAME</span></span>
* <span data-ttu-id="a914c-120">X-MS-CLIENT-PRINCIPAL-ID</span><span class="sxs-lookup"><span data-stu-id="a914c-120">X-MS-CLIENT-PRINCIPAL-ID</span></span>
* <span data-ttu-id="a914c-121">X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN</span><span class="sxs-lookup"><span data-stu-id="a914c-121">X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN</span></span>
* <span data-ttu-id="a914c-122">X-MS-TOKEN-FACEBOOK-EXPIRES-ON</span><span class="sxs-lookup"><span data-stu-id="a914c-122">X-MS-TOKEN-FACEBOOK-EXPIRES-ON</span></span>

<span data-ttu-id="a914c-123">在 .NET API 中，您可以使用 `Authorize` 屬性，而且如果您需要更精細的授權，也能輕易地根據宣告來撰寫程式碼，因為它已為您在 .NET 類別中填入宣告資訊。</span><span class="sxs-lookup"><span data-stu-id="a914c-123">In a .NET API, you can use the `Authorize` attribute, and for fine-grained authorization you can easily write code based on claims because claims information is populated for you in .NET classes.</span></span>

## <a name="multiple-protection-options"></a><span data-ttu-id="a914c-124">多個保護選項</span><span class="sxs-lookup"><span data-stu-id="a914c-124">Multiple protection options</span></span>
<span data-ttu-id="a914c-125">App Service 可以防止匿名 HTTP 要求進入您的 API 應用程式、傳遞所有要求並驗證要求中所包含的權杖，或是不採取任何動作就放行所有要求：</span><span class="sxs-lookup"><span data-stu-id="a914c-125">App Service can prevent anonymous HTTP requests from reaching your API app, it can pass on all requests and validate tokens for requests that include them, or it can let through all requests without taking any action on them:</span></span>

1. <span data-ttu-id="a914c-126">只允許通過驗證的要求進入 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a914c-126">Allow only authenticated requests to reach your API app.</span></span>
   
    <span data-ttu-id="a914c-127">如果 App Service 收到來自瀏覽器的匿名要求，便會將其重新導向至您所選驗證提供者 (Azure AD、Google、Twitter 等) 的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="a914c-127">If an anonymous request is received from a browser, App Service will redirect to a logon page for the authentication provider (Azure AD, Google, Twitter, etc.) that you choose.</span></span> 
   
    <span data-ttu-id="a914c-128">使用此選項時，您不需要在應用程式中撰寫任何驗證程式碼，並且因為 HTTP 標頭中已提供最重要的宣告，所以授權碼會變得相當簡單。</span><span class="sxs-lookup"><span data-stu-id="a914c-128">With this option, you don't need to write any authentication code at all in your app, and authorization code is simplified because the most important claims are provided in the HTTP headers.</span></span>
2. <span data-ttu-id="a914c-129">允許所有要求進入 API 應用程式，但只讓通過驗證的要求生效，並在 HTTP 標頭中傳遞驗證資訊。</span><span class="sxs-lookup"><span data-stu-id="a914c-129">Allow all requests to reach your API app, but validate authenticated requests and pass along authentication information in the HTTP headers.</span></span>
   
    <span data-ttu-id="a914c-130">此選項可讓您更彈性地處理匿名要求，但如果想要防止匿名使用者使用您的 API，則必須撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="a914c-130">This option gives you more flexibility in handling anonymous requests, but you have to write code if you want to prevent anonymous users from using your API.</span></span> <span data-ttu-id="a914c-131">因為最受歡迎的宣告會在 HTTP 要求的標頭中傳遞，所以授權碼相對簡單。</span><span class="sxs-lookup"><span data-stu-id="a914c-131">Since the most popular claims are passed in the headers of HTTP requests, authorization code is relatively simple.</span></span>
3. <span data-ttu-id="a914c-132">允許所有要求進入 API，不對要求中的驗證資訊採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="a914c-132">Allow all requests to reach your API, take no action on authentication information in the requests.</span></span>
   
    <span data-ttu-id="a914c-133">這個選項會將驗證和授權工作全部交由應用程式程式碼來處理。</span><span class="sxs-lookup"><span data-stu-id="a914c-133">This option leaves the tasks of authentication and authorization entirely up to your application code.</span></span>

<span data-ttu-id="a914c-134">在 [Azure 入口網站](https://portal.azure.com/)中，請在 [驗證/授權] 刀鋒視窗中選取您要的選項。</span><span class="sxs-lookup"><span data-stu-id="a914c-134">In the [Azure portal](https://portal.azure.com/), you select the option you want on the **Authentication / Authorization** blade.</span></span>

![](./media/app-service-api-authentication/authblade.png)

<span data-ttu-id="a914c-135">如果使用選項 1 和 2，請開啟 [App Service 驗證]，然後在 [要求未通過驗證時所要採取的動作] 下拉式清單中，選擇 [登入] 或 [允許要求 (無動作)]。</span><span class="sxs-lookup"><span data-stu-id="a914c-135">For options 1 and 2, turn on **App Service Authentication**, and in the **Action to take when request is not authenticated** drop-down list choose **Log in** or **Allow request (no action)**.</span></span>  <span data-ttu-id="a914c-136">如果您選擇 [登入] ，就必須選擇驗證提供者，並設定該提供者。</span><span class="sxs-lookup"><span data-stu-id="a914c-136">If you choose **Log in**, you have to choose an authentication provider and configure that provider.</span></span>

![](./media/app-service-api-authentication/actiontotake.png)

<span data-ttu-id="a914c-137">如需如何設定驗證的詳細資訊，請參閱 [如何設定 App Service 應用程式使用 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="a914c-137">For detailed information about how to configure authentication, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="a914c-138">本文適用於 API 應用程式和行動應用程式，而且會連結到關於其他驗證提供者的其他文章。</span><span class="sxs-lookup"><span data-stu-id="a914c-138">The article applies to API apps as well as mobile apps, and it links to other articles for the other authentication providers.</span></span>

## <span data-ttu-id="a914c-139"><a id="internal"></a> 服務帳戶驗證</span><span class="sxs-lookup"><span data-stu-id="a914c-139"><a id="internal"></a> Service account authentication</span></span>
<span data-ttu-id="a914c-140">App Service 驗證適用於從某個 API 應用程式呼叫另一個 API 應用程式之類的內部案例。</span><span class="sxs-lookup"><span data-stu-id="a914c-140">App Service authentication works for internal scenarios such as for calling from one API app to another API app.</span></span> <span data-ttu-id="a914c-141">在此案例中，您可以使用服務帳戶認證 (而非使用者認證) 來取得權杖。</span><span class="sxs-lookup"><span data-stu-id="a914c-141">In this scenario you get a token by using credentials for a service account instead of end user credentials.</span></span> <span data-ttu-id="a914c-142">服務帳戶在 Azure Active Directory 中也稱為 *服務主體* ，使用這類帳戶的驗證也稱為服務對服務案例。</span><span class="sxs-lookup"><span data-stu-id="a914c-142">A service account is also known as a *service principal* in Azure Active Directory, and authentication using such an account is also known as a service-to-service scenario.</span></span> 

<span data-ttu-id="a914c-143">若為服務對服務案例，則請使用 Azure Active Directory 保護所呼叫的 API 應用程式，並在呼叫 API 應用程式時提供 AAD 服務主體授權權杖。</span><span class="sxs-lookup"><span data-stu-id="a914c-143">For service-to-service scenarios, protect the called API app by using Azure Active Directory, and provide an AAD service principal authorization token when you call the API app.</span></span> <span data-ttu-id="a914c-144">透過提供用戶端識別碼和用戶端密碼，您就可以從 AAD 應用程式取得此權杖。</span><span class="sxs-lookup"><span data-stu-id="a914c-144">You get a token by providing the client ID and client secret from the AAD application.</span></span> <span data-ttu-id="a914c-145">不需要特殊的僅 Azure 適用的程式碼，例如在處理行動服務 Zumo 權杖時為 true。</span><span class="sxs-lookup"><span data-stu-id="a914c-145">No special Azure-only code is required, such as used to be true for handling the Mobile Services Zumo token.</span></span> <span data-ttu-id="a914c-146">[API Apps 的服務主體驗證](app-service-api-dotnet-service-principal-auth.md)教學課程中有講述這個使用 ASP.NET API 應用程式之案例的範例。</span><span class="sxs-lookup"><span data-stu-id="a914c-146">An example of this scenario using ASP.NET API apps is covered by the tutorial [Service principal authentication for API Apps](app-service-api-dotnet-service-principal-auth.md).</span></span>

<span data-ttu-id="a914c-147">如果您想要處理服務對服務案例，但不要使用 App Service 驗證，請使用用戶端憑證或基本驗證。</span><span class="sxs-lookup"><span data-stu-id="a914c-147">If you want to handle a service-to-service scenario without using App Service authentication, you can use client certificates or basic authentication.</span></span> <span data-ttu-id="a914c-148">如需 Azure 中用戶端憑證的詳細資訊，請參閱 [如何設定 Web Apps 的 TLS 相互驗證](../app-service-web/app-service-web-configure-tls-mutual-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="a914c-148">For information about client certificates in Azure, see [How To Configure TLS Mutual Authentication for Web Apps](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span> <span data-ttu-id="a914c-149">如需 ASP.NET 中的基本驗證相關資訊，請參閱 [ASP.NET Web API 2 中的驗證篩選](http://www.asp.net/web-api/overview/security/authentication-filters)。</span><span class="sxs-lookup"><span data-stu-id="a914c-149">For information about basic authentication in ASP.NET, see [Authentication Filters in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/authentication-filters).</span></span>

<span data-ttu-id="a914c-150">App Service 邏輯應用程式至 API 應用程式的服務帳戶驗證屬於特殊案例， [將您裝載在 App Service 上的自訂 API 與邏輯應用程式一起使用](../logic-apps/logic-apps-custom-hosted-api.md)中有關於此案例的說明。</span><span class="sxs-lookup"><span data-stu-id="a914c-150">Service account authentication from an App Service logic app to an API app is a special case that is explained in [Using your custom API hosted on App Service with Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).</span></span>

## <a name="mobile-client-authentication"></a><span data-ttu-id="a914c-151">行動用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="a914c-151">Mobile client authentication</span></span>
<span data-ttu-id="a914c-152">如需如何處理來自行動用戶端之驗證的相關資訊，請參閱 [關於行動應用程式驗證的說明文件](../app-service-mobile/app-service-mobile-ios-get-started-users.md)。</span><span class="sxs-lookup"><span data-stu-id="a914c-152">For information about how to handle authentication from mobile clients, see the [documentation on authentication for mobile apps](../app-service-mobile/app-service-mobile-ios-get-started-users.md).</span></span> <span data-ttu-id="a914c-153">行動應用程式和 API 應用程式的 App Service 驗證具有相同的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a914c-153">App Service authentication works the same way for mobile apps and API apps.</span></span>

## <a name="more-information"></a><span data-ttu-id="a914c-154">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a914c-154">More information</span></span>
<span data-ttu-id="a914c-155">如需 Azure App Service 中的驗證與授權的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="a914c-155">For more information about authentication and authorization in Azure App Service, see the following resources:</span></span>

* [<span data-ttu-id="a914c-156">擴充 App Service 驗證/授權</span><span class="sxs-lookup"><span data-stu-id="a914c-156">Expanding App Service authentication / authorization</span></span>](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)
* <span data-ttu-id="a914c-157">[如何設定 App Service 應用程式使用 Azure Active Directory 登入](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (頁面頂端有其他驗證提供者的連結)。</span><span class="sxs-lookup"><span data-stu-id="a914c-157">[How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md) (Includes links for other authentication providers at the top of the page.)</span></span> 

<span data-ttu-id="a914c-158">如需 OAuth 2.0、OpenID Connect 和 JSON Web 權杖 (JWT) 的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="a914c-158">For more information about OAuth 2.0, OpenID Connect, and JSON Web Tokens (JWT), see the following resources.</span></span>

* [<span data-ttu-id="a914c-159">開始使用 OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="a914c-159">Getting started with OAuth 2.0</span></span>](http://shop.oreilly.com/product/0636920021810.do "Getting Started with OAuth 2.0") 
* [<span data-ttu-id="a914c-160">OAuth2、OpenID Connect 和 JSON Web 權杖 (JWT) 簡介 - Pluralsight 課程</span><span class="sxs-lookup"><span data-stu-id="a914c-160">Introduction to OAuth2, OpenID Connect and JSON Web Tokens (JWT) - Pluralsight Course</span></span>](http://www.pluralsight.com/courses/oauth2-json-web-tokens-openid-connect-introduction) 
* [<span data-ttu-id="a914c-161">在 ASP.NET 中建置和保護多個用戶端的 RESTful API - Pluralsight 課程</span><span class="sxs-lookup"><span data-stu-id="a914c-161">Building and Securing a RESTful API for Multiple Clients in ASP.NET - Pluralsight course</span></span>](http://www.pluralsight.com/courses/building-securing-restful-api-aspdotnet)

<span data-ttu-id="a914c-162">如需 Azure Active Directory 的詳細資訊，請參閱下列資源。</span><span class="sxs-lookup"><span data-stu-id="a914c-162">For more information about Azure Active Directory, see the following resources.</span></span>

* [<span data-ttu-id="a914c-163">Azure AD 案例</span><span class="sxs-lookup"><span data-stu-id="a914c-163">Azure AD scenarios</span></span>](http://aka.ms/aadscenarios)
* [<span data-ttu-id="a914c-164">Azure AD 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="a914c-164">Azure AD developers' guide</span></span>](http://aka.ms/aaddev)
* [<span data-ttu-id="a914c-165">Azure AD 範例</span><span class="sxs-lookup"><span data-stu-id="a914c-165">Azure AD samples</span></span>](http://aka.ms/aadsamples)

## <a name="next-steps"></a><span data-ttu-id="a914c-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a914c-166">Next steps</span></span>
<span data-ttu-id="a914c-167">本文說明了可用於 API 應用程式之 App Service 的驗證和授權功能。</span><span class="sxs-lookup"><span data-stu-id="a914c-167">This article has explained authentication and authorization features of App Service that you can use for API apps.</span></span> <span data-ttu-id="a914c-168">在下一個快速入門系列教學課程中，會說明如何實作 [App Service API Apps 中的使用者驗證](app-service-api-dotnet-user-principal-auth.md)。</span><span class="sxs-lookup"><span data-stu-id="a914c-168">The next tutorial in the getting started series shows how to implement [user authentication in App Service API Apps](app-service-api-dotnet-user-principal-auth.md).</span></span>

