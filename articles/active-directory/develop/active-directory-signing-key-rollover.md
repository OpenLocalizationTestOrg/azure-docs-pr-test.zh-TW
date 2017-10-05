---
title: "Azure AD 中的簽署金鑰變換 | Microsoft Docs"
description: "本文討論 Azure Active directory 的簽署金鑰變換最佳做法"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 228bb9058537af1e4eb38207c376c2eb86aee68c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="0415e-103">Azure Active Directory 中的簽署金鑰變換</span><span class="sxs-lookup"><span data-stu-id="0415e-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="0415e-104">本主題討論 Azure Active Directory (Azure AD) 中用來簽署安全性權杖的公開金鑰須知事項。</span><span class="sxs-lookup"><span data-stu-id="0415e-104">This topic discusses what you need to know about the public keys that are used in Azure Active Directory (Azure AD) to sign security tokens.</span></span> <span data-ttu-id="0415e-105">請務必注意這些金鑰會定期變換，且在緊急狀況下可以立即變換。</span><span class="sxs-lookup"><span data-stu-id="0415e-105">It is important to note that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="0415e-106">所有使用 Azure AD 的應用程式都應該能夠以程式設計方式處理金鑰變換程序或建立定期手動變換程序。</span><span class="sxs-lookup"><span data-stu-id="0415e-106">All applications that use Azure AD should be able to programmatically handle the key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="0415e-107">請繼續閱讀以了解金鑰的運作方式、如何評估變換對應用程式的影響，以及必要時如何更新應用程式或建立定期手動變換程序來處理金鑰變換。</span><span class="sxs-lookup"><span data-stu-id="0415e-107">Continue reading to understand how the keys work, how to assess the impact of the rollover to your application and how to update your application or establish a periodic manual rollover process to handle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="0415e-108">Azure AD 中簽署金鑰的概觀</span><span class="sxs-lookup"><span data-stu-id="0415e-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="0415e-109">Azure AD 會使用根據業界標準所建置的公開金鑰加密技術，建立 Azure AD 本身和使用 Azure AD 的應用程式之間的信任。</span><span class="sxs-lookup"><span data-stu-id="0415e-109">Azure AD uses public-key cryptography built on industry standards to establish trust between itself and the applications that use it.</span></span> <span data-ttu-id="0415e-110">實際上，其運作方式如下：Azure AD 使用由公開和私密金鑰組所組成的簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-110">In practical terms, this works in the following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="0415e-111">當使用者登入使用 Azure AD 來進行驗證的應用程式時，Azure AD 會建立包含使用者相關資訊的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="0415e-111">When a user signs in to an application that uses Azure AD for authentication, Azure AD creates a security token that contains information about the user.</span></span> <span data-ttu-id="0415e-112">此權杖會先由 Azure AD 使用其私密金鑰進行簽署，再傳送回到應用程式。</span><span class="sxs-lookup"><span data-stu-id="0415e-112">This token is signed by Azure AD using its private key before it is sent back to the application.</span></span> <span data-ttu-id="0415e-113">若要確認該權杖有效且確實來自 Azure AD，應用程式必須使用由 Azure AD 公開且包含在租用戶的 [OpenID Connect 探索文件](http://openid.net/specs/openid-connect-discovery-1_0.html)或 SAML/WS-Fed [同盟中繼資料文件](active-directory-federation-metadata.md)中的公開金鑰來驗證權杖的簽章。</span><span class="sxs-lookup"><span data-stu-id="0415e-113">To verify that the token is valid and actually originated from Azure AD, the application must validate the token’s signature using the public key exposed by Azure AD that is contained in the tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="0415e-114">基於安全考量，Azure AD 的簽署金鑰會定期變換，且在緊急情況下可以立即變換。</span><span class="sxs-lookup"><span data-stu-id="0415e-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in the case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="0415e-115">任何與 Azure AD 整合的應用程式均應準備好處理金鑰變換事件，不論其可能發生頻率為何。</span><span class="sxs-lookup"><span data-stu-id="0415e-115">Any application that integrates with Azure AD should be prepared to handle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="0415e-116">如果沒有，應用程式又嘗試使用過期的金鑰來驗證權杖上的簽章，登入要求便會失敗。</span><span class="sxs-lookup"><span data-stu-id="0415e-116">If it doesn’t, and your application attempts to use an expired key to verify the signature on a token, the sign-in request will fail.</span></span>

<span data-ttu-id="0415e-117">OpenID Connect 探索文件和同盟中繼資料文件中永遠有一個以上的有效金鑰可用。</span><span class="sxs-lookup"><span data-stu-id="0415e-117">There is always more than one valid key available in the OpenID Connect discovery document and the federation metadata document.</span></span> <span data-ttu-id="0415e-118">應用程式應該要已準備好使用文件中指定的任何金鑰，因為某個金鑰可能很快就得要替換，而另一個可能會取代它，依此類推。</span><span class="sxs-lookup"><span data-stu-id="0415e-118">Your application should be prepared to use any of the keys specified in the document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-to-assess-if-your-application-will-be-affected-and-what-to-do-about-it"></a><span data-ttu-id="0415e-119">如何評估您的應用程式是否會受到影響，以及如何因應</span><span class="sxs-lookup"><span data-stu-id="0415e-119">How to assess if your application will be affected and what to do about it</span></span>
<span data-ttu-id="0415e-120">應用程式處理金鑰變換的方式取決於各種變數，例如應用程式類型或使用的身分識別通訊協定和程式庫。</span><span class="sxs-lookup"><span data-stu-id="0415e-120">How your application handles key rollover depends on variables such as the type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="0415e-121">下列各節會評估最常見的應用程式類型是否會受到金鑰變換所影響，並提供如何更新應用程式以支援自動變換或手動更新金鑰的指引。</span><span class="sxs-lookup"><span data-stu-id="0415e-121">The sections below assess whether the most common types of applications are impacted by the key rollover and provide guidance on how to update the application to support automatic rollover or manually update the key.</span></span>

* [<span data-ttu-id="0415e-122">存取資源的原生用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="0415e-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="0415e-123">存取資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="0415e-124">保護資源且使用 Azure App Service 建置的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="0415e-125">使用 .NET OWIN OpenID Connect、WS-Fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="0415e-126">使用 .NET Core OpenID Connect 或 JwtBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="0415e-127">使用 Node.js passport-azure-ad 模組保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="0415e-128">保護資源且使用 Visual Studio 2015 或 Visual Studio 2017 建立的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="0415e-129">保護資源且使用 Visual Studio 2013 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0415e-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="0415e-130">保護資源且使用 Visual Studio 2013 建立的 Web API</span><span class="sxs-lookup"><span data-stu-id="0415e-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="0415e-131">保護資源且使用 Visual Studio 2012 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0415e-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="0415e-132">保護資源且使用 Visual Studio 2010、2008 或使用 Windows Identity Foundation 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0415e-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="0415e-133">保護資源且使用任何其他程式庫或手動實作任何支援的通訊協定的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>](#other)

<span data-ttu-id="0415e-134">本指南 **不** 適用於︰</span><span class="sxs-lookup"><span data-stu-id="0415e-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="0415e-135">從 Azure AD 應用程式資源庫 (包括自訂) 新增的應用程式有個別的簽署金鑰指引。</span><span class="sxs-lookup"><span data-stu-id="0415e-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards to signing keys.</span></span> [<span data-ttu-id="0415e-136">相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0415e-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="0415e-137">透過應用程式 proxy 發佈的內部部署應用程式不需要擔心簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-137">On-premises applications published via application proxy don't have to worry about signing keys.</span></span>

### <span data-ttu-id="0415e-138"><a name="nativeclient"></a>存取資源的原生用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="0415e-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="0415e-139">只存取資源 (亦即</span><span class="sxs-lookup"><span data-stu-id="0415e-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="0415e-140">Microsoft Graph、KeyVault、Outlook API 及其他 Microsoft API) 的應用程式通常只會取得權杖並將它傳遞給資源擁有者。</span><span class="sxs-lookup"><span data-stu-id="0415e-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="0415e-141">假設它們並未保護任何資源，它們就不會檢查權杖，因此不需要確定已正確簽署。</span><span class="sxs-lookup"><span data-stu-id="0415e-141">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="0415e-142">原生用戶端應用程式 (不論是桌上型或行動) 屬於此分類，因此不受變換影響。</span><span class="sxs-lookup"><span data-stu-id="0415e-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="0415e-143"><a name="webclient"></a>存取資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="0415e-144">只存取資源 (亦即</span><span class="sxs-lookup"><span data-stu-id="0415e-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="0415e-145">Microsoft Graph、KeyVault、Outlook API 及其他 Microsoft API) 的應用程式通常只會取得權杖並將它傳遞給資源擁有者。</span><span class="sxs-lookup"><span data-stu-id="0415e-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along to the resource owner.</span></span> <span data-ttu-id="0415e-146">假設它們並未保護任何資源，它們就不會檢查權杖，因此不需要確定已正確簽署。</span><span class="sxs-lookup"><span data-stu-id="0415e-146">Given that they are not protecting any resources, they do not inspect the token and therefore do not need to ensure it is properly signed.</span></span>

<span data-ttu-id="0415e-147">使用應用程式專用流程 (用戶端認證 / 用戶端憑證) 的 Web 應用程式和 web API 屬於此類型，因此不受變換影響。</span><span class="sxs-lookup"><span data-stu-id="0415e-147">Web applications and web APIs that are using the app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by the rollover.</span></span>

### <span data-ttu-id="0415e-148"><a name="appservices"></a>保護資源且使用 Azure App Service 建置的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="0415e-149">Azure App Service 的驗證/授權 (EasyAuth) 功能已經具有必要的邏輯可自動處理金鑰變換。</span><span class="sxs-lookup"><span data-stu-id="0415e-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has the necessary logic to handle key rollover automatically.</span></span>

### <span data-ttu-id="0415e-150"><a name="owin"></a>使用 .NET OWIN OpenID Connect、WS-Fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="0415e-151">如果您的應用程式使用 .NET OWIN OpenID Connect、WS-Fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體，則它已經具有必要的邏輯可自動處理金鑰變換。</span><span class="sxs-lookup"><span data-stu-id="0415e-151">If your application is using the .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="0415e-152">您可以應用程式的 Startup.cs 或 Startup.Auth.cs 中尋找下列任何程式碼片段，以確認您的應用程式使用任何這些項目</span><span class="sxs-lookup"><span data-stu-id="0415e-152">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <span data-ttu-id="0415e-153"><a name="owincore"></a>使用 .NET Core OpenID Connect 或 JwtBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="0415e-154">如果您的應用程式使用 .NET Core OWIN OpenID Connect 或 JwtBearerAuthentication 中介軟體，則它已經具有自動處理金鑰變換的必要邏輯。</span><span class="sxs-lookup"><span data-stu-id="0415e-154">If your application is using the .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="0415e-155">您可以應用程式的 Startup.cs 或 Startup.Auth.cs 中尋找下列任何程式碼片段，以確認您的應用程式使用任何這些項目</span><span class="sxs-lookup"><span data-stu-id="0415e-155">You can confirm that your application is using any of these by looking for any of the following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <span data-ttu-id="0415e-156"><a name="passport"></a>使用 Node.js passport-azure-ad 模組保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="0415e-157">如果您的應用程式使用 Node.js passport-ad 模組，則它已經具有必要的邏輯可自動處理金鑰變換。</span><span class="sxs-lookup"><span data-stu-id="0415e-157">If your application is using the Node.js passport-ad module, it already has the necessary logic to handle key rollover automatically.</span></span>

<span data-ttu-id="0415e-158">您可以在應用程式的 app.js 中搜尋下列程式碼片段，以確認您的應用程式使用 passport-ad</span><span class="sxs-lookup"><span data-stu-id="0415e-158">You can confirm that your application passport-ad by searching for the following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="0415e-159"><a name="vs2015"></a>保護資源且使用 Visual Studio 2015 或 Visual Studio 2017 建立的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="0415e-160">如果應用程式是使用 Visual Studio 2015 或 Visual Studio 2017 中的 Web 應用程式範本所建置，而且您已從 [變更驗證] 功能表中選取 [公司和學校帳戶]，則它已經具有自動處理金鑰變換的必要邏輯。</span><span class="sxs-lookup"><span data-stu-id="0415e-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="0415e-161">這個內嵌在 OWIN OpenID Connect 中介軟體中的邏輯會從 OpenID Connect 探索文件擷取並快取金鑰，還會定期重新整理金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-161">This logic, embedded in the OWIN OpenID Connect middleware, retrieves and caches the keys from the OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="0415e-162">如果您是以手動方式在方案中加入驗證，應用程式可能不會有所需的金鑰變換邏輯。</span><span class="sxs-lookup"><span data-stu-id="0415e-162">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="0415e-163">您必須自行撰寫，或依照 [使用任何其他程式庫或手動實作任何支援的通訊協定的 Web 應用程式 / API](#other)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="0415e-163">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

### <span data-ttu-id="0415e-164"><a name="vs2013"></a>保護資源且使用 Visual Studio 2013 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0415e-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="0415e-165">如果應用程式是使用 Visual Studio 2013 中的 Web 應用程式範本所建置，而且您已從 [變更驗證] 功能表中選取 [組織帳戶]，則它已經具有自動處理金鑰變換的必要邏輯。</span><span class="sxs-lookup"><span data-stu-id="0415e-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from the **Change Authentication** menu, it already has the necessary logic to handle key rollover automatically.</span></span> <span data-ttu-id="0415e-166">此邏輯會將組織的唯一識別碼和簽署金鑰資訊儲存在兩個與專案相關聯的資料庫資料表中。</span><span class="sxs-lookup"><span data-stu-id="0415e-166">This logic stores your organization’s unique identifier and the signing key information in two database tables associated with the project.</span></span> <span data-ttu-id="0415e-167">您可以在專案的 Web.config 檔案中找到資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="0415e-167">You can find the connection string for the database in the project’s Web.config file.</span></span>

<span data-ttu-id="0415e-168">如果您是以手動方式在方案中加入驗證，應用程式可能不會有所需的金鑰變換邏輯。</span><span class="sxs-lookup"><span data-stu-id="0415e-168">If you added authentication to your solution manually, your application might not have the necessary key rollover logic.</span></span> <span data-ttu-id="0415e-169">您必須自行撰寫，或依照 [使用任何其他程式庫或手動實作任何支援的通訊協定的 Web 應用程式 / API](#other)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="0415e-169">You will need to write it yourself, or follow the steps in [Web applications / APIs using any other libraries or manually implementing any of the supported protocols.](#other).</span></span>

<span data-ttu-id="0415e-170">下列步驟將協助您確認應用程式中的邏輯能正常運作。</span><span class="sxs-lookup"><span data-stu-id="0415e-170">The following steps will help you verify that the logic is working properly in your application.</span></span>

1. <span data-ttu-id="0415e-171">在 Visual Studio 2013 中開啟方案，然後按一下右側視窗上的 [伺服器 Explorer]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0415e-171">In Visual Studio 2013, open the solution, and then click on the **Server Explorer** tab on the right window.</span></span>
2. <span data-ttu-id="0415e-172">依序展開 [資料連線]、[DefaultConnection]、[資料表]。</span><span class="sxs-lookup"><span data-stu-id="0415e-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="0415e-173">找出 [IssuingAuthorityKeys] 資料表並以滑鼠右鍵按一下，然後按一下 [顯示資料表資料]。</span><span class="sxs-lookup"><span data-stu-id="0415e-173">Locate the **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="0415e-174">[IssuingAuthorityKeys]  資料表中會有至少一個對應至金鑰指紋值的資料列。</span><span class="sxs-lookup"><span data-stu-id="0415e-174">In the **IssuingAuthorityKeys** table, there will be at least one row, which corresponds to the thumbprint value for the key.</span></span> <span data-ttu-id="0415e-175">刪除資料表中的任何資料列。</span><span class="sxs-lookup"><span data-stu-id="0415e-175">Delete any rows in the table.</span></span>
4. <span data-ttu-id="0415e-176">在 [租用戶] 資料表上按一下滑鼠右鍵，然後按一下 [顯示資料表資料]。</span><span class="sxs-lookup"><span data-stu-id="0415e-176">Right-click the **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="0415e-177">[租用戶]  資料表中會有至少一個對應至唯一目錄租用戶識別碼的資料列。</span><span class="sxs-lookup"><span data-stu-id="0415e-177">In the **Tenants** table, there will be at least one row, which corresponds to a unique directory tenant identifier.</span></span> <span data-ttu-id="0415e-178">刪除資料表中的任何資料列。</span><span class="sxs-lookup"><span data-stu-id="0415e-178">Delete any rows in the table.</span></span> <span data-ttu-id="0415e-179">如果您未刪除 [租用戶] 資料表和 [IssuingAuthorityKeys] 資料表中的資料列，您就會在執行階段收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="0415e-179">If you don't delete the rows in both the **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="0415e-180">建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0415e-180">Build and run the application.</span></span> <span data-ttu-id="0415e-181">在登入帳戶之後，即可停止應用程式。</span><span class="sxs-lookup"><span data-stu-id="0415e-181">After you have logged in to your account, you can stop the application.</span></span>
7. <span data-ttu-id="0415e-182">返回 [伺服器總管]，然後查看 [IssuingAuthorityKeys] 和 [租用戶] 資料表中的值。</span><span class="sxs-lookup"><span data-stu-id="0415e-182">Return to the **Server Explorer** and look at the values in the **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="0415e-183">您將會發現，它們已自動重新填入同盟中繼資料文件中的適當資訊。</span><span class="sxs-lookup"><span data-stu-id="0415e-183">You’ll notice that they have been automatically repopulated with the appropriate information from the federation metadata document.</span></span>

### <span data-ttu-id="0415e-184"><a name="vs2013"></a>保護資源且使用 Visual Studio 2013 建立的 Web API</span><span class="sxs-lookup"><span data-stu-id="0415e-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="0415e-185">如果您使用 Web API 範本在 Visual Studio 2013 中建置了 Web API 應用程式，然後從 [變更驗證] 功能表中選取了 [組織帳戶]，則應用程式已經具有所需的邏輯。</span><span class="sxs-lookup"><span data-stu-id="0415e-185">If you created a web API application in Visual Studio 2013 using the Web API template, and then selected **Organizational Accounts** from the **Change Authentication** menu, you already have the necessary logic in your application.</span></span>

<span data-ttu-id="0415e-186">如果您以手動方式設定了驗證，請依照下列指示來了解如何設定 Web API 以自動更新其金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="0415e-186">If you manually configured authentication, follow the instructions below to learn how to configure your Web API to automatically update its key information.</span></span>

<span data-ttu-id="0415e-187">下列程式碼片段示範如何從同盟中繼資料文件取得最新的金鑰，然後使用 [JWT 權杖處理常式](https://msdn.microsoft.com/library/dn205065.aspx) 來驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="0415e-187">The following code snippet demonstrates how to get the latest keys from the federation metadata document, and then use the [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) to validate the token.</span></span> <span data-ttu-id="0415e-188">此程式碼片段假設您將會使用自己的快取機制來保留金鑰，以驗證日後來自 Azure AD 的權杖，不論它位於資料庫、組態檔或其他位置。</span><span class="sxs-lookup"><span data-stu-id="0415e-188">The code snippet assumes that you will use your own caching mechanism for persisting the key to validate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates the JWT Token that's part of the Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in the Azure Classic Portal]",
                ValidIssuer = "[The issuer for the token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache the signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from the specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in the metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <span data-ttu-id="0415e-189"><a name="vs2012"></a>保護資源且使用 Visual Studio 2012 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0415e-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="0415e-190">如果應用程式是在 Visual Studio 2012 中建置的，您大概是使用身分識別與存取工具來設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="0415e-190">If your application was built in Visual Studio 2012, you probably used the Identity and Access Tool to configure your application.</span></span> <span data-ttu-id="0415e-191">您也可能是使用 [驗證簽發者名稱登錄 (VINR)](https://msdn.microsoft.com/library/dn205067.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0415e-191">It’s also likely that you are using the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="0415e-192">VINR 負責維護信任的識別提供者 (Azure AD) 的相關資訊以及用來驗證其所簽發之權杖的金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-192">The VINR is responsible for maintaining information about trusted identity providers (Azure AD) and the keys used to validate tokens issued by them.</span></span> <span data-ttu-id="0415e-193">VINR 也可透過下載與目錄相關聯的最新同盟中繼資料文件、使用最新文件檢查組態是否過期，以及視需要讓應用程式更新為使用新金鑰，讓您輕鬆地自動更新 Web.config 檔案中儲存的金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="0415e-193">The VINR also makes it easy to automatically update the key information stored in a Web.config file by downloading the latest federation metadata document associated with your directory, checking if the configuration is out of date with the latest document, and updating the application to use the new key as necessary.</span></span>

<span data-ttu-id="0415e-194">如果您是使用 Microsoft 所提供的任何程式碼範例或逐步解說文件建立應用程式，則專案中已含有金鑰變換邏輯。</span><span class="sxs-lookup"><span data-stu-id="0415e-194">If you created your application using any of the code samples or walkthrough documentation provided by Microsoft, the key rollover logic is already included in your project.</span></span> <span data-ttu-id="0415e-195">您會發現專案中已存在下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="0415e-195">You will notice that the code below already exists in your project.</span></span> <span data-ttu-id="0415e-196">如果應用程式還沒有此邏輯，請遵循下列步驟，以新增此邏輯並確認它能正常運作。</span><span class="sxs-lookup"><span data-stu-id="0415e-196">If your application does not already have this logic, follow the steps below to add it and to verify that it’s working correctly.</span></span>

1. <span data-ttu-id="0415e-197">在 [方案總管] 中，針對適當的專案新增對 **System.IdentityModel** 組件的參考。</span><span class="sxs-lookup"><span data-stu-id="0415e-197">In **Solution Explorer**, add a reference to the **System.IdentityModel** assembly for the appropriate project.</span></span>
2. <span data-ttu-id="0415e-198">開啟 **Global.asax.cs** 檔案，並新增下列 using 指示詞：</span><span class="sxs-lookup"><span data-stu-id="0415e-198">Open the **Global.asax.cs** file and add the following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="0415e-199">在 **Global.asax.cs** 檔案中新增下列方法：</span><span class="sxs-lookup"><span data-stu-id="0415e-199">Add the following method to the **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="0415e-200">在 **Global.asax.cs** 的 **Application_Start()** 方法中，叫用 **RefreshValidationSettings()** 方法，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="0415e-200">Invoke the **RefreshValidationSettings()** method in the **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="0415e-201">在遵循這些步驟之後，應用程式的 Web.config 將會以同盟中繼資料文件中的最新資訊進行更新，其中也包括最新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-201">Once you have followed these steps, your application’s Web.config will be updated with the latest information from the federation metadata document, including the latest keys.</span></span> <span data-ttu-id="0415e-202">此更新會在每次 IIS 回收應用程式集區時進行；依預設，IIS 設定為每隔 29 小時回收應用程式一次。</span><span class="sxs-lookup"><span data-stu-id="0415e-202">This update will occur every time your application pool recycles in IIS; by default IIS is set to recycle applications every 29 hours.</span></span>

<span data-ttu-id="0415e-203">請遵循下列步驟來確認金鑰變換邏輯是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0415e-203">Follow the steps below to verify that the key rollover logic is working.</span></span>

1. <span data-ttu-id="0415e-204">在確認應用程式是使用上述程式碼之後，開啟 **Web.config** 檔案並瀏覽至 **<issuerNameRegistry>** 區塊，具體而言，請尋找下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="0415e-204">After you have verified that your application is using the code above, open the **Web.config** file and navigate to the **<issuerNameRegistry>** block, specifically looking for the following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="0415e-205">[IssuingAuthorityKeys] **<add thumbprint=””>** 設定中，將任何字元替換為其他字元以變更指紋值。</span><span class="sxs-lookup"><span data-stu-id="0415e-205">In the **<add thumbprint=””>** setting, change the thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="0415e-206">儲存 **Web.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="0415e-206">Save the **Web.config** file.</span></span>
3. <span data-ttu-id="0415e-207">建置應用程式，然後加以執行。</span><span class="sxs-lookup"><span data-stu-id="0415e-207">Build the application, and then run it.</span></span> <span data-ttu-id="0415e-208">如果您可以完成登入程序，則應用程式已從目錄的同盟中繼資料文件下載所需資訊，而成功地更新金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-208">If you can complete the sign-in process, your application is successfully updating the key by downloading the required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="0415e-209">如果您在登入時發生問題，請閱讀[使用 Azure AD 為 Web 應用程式新增登入](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)主題，或是下載並檢查下列程式碼範例︰[Azure Active Directory 的多租用戶雲端應用程式](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b)，以確定應用程式中的變更是否正確。</span><span class="sxs-lookup"><span data-stu-id="0415e-209">If you are having issues signing in, ensure the changes in your application are correct by reading the [Adding Sign-On to Your Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting the following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="0415e-210"><a name="vs2010"></a>保護資源且使用 Visual Studio 2008 或 2010 和 Windows Identity Foundation (WIF) v1.0 for .NET 3.5 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0415e-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="0415e-211">如果您在 WIF v1.0 上建置應用程式，則沒有提供相關機制來將應用程式的組態自動重新整理為使用新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-211">If you built an application on WIF v1.0, there is no provided mechanism to automatically refresh your application’s configuration to use a new key.</span></span>

* <span data-ttu-id="0415e-212"> 使用 WIF SDK 中內含的 FedUtil 工具，它可以擷取最新的中繼資料文件並更新組態。</span><span class="sxs-lookup"><span data-stu-id="0415e-212">*Easiest way* Use the FedUtil tooling included in the WIF SDK, which can retrieve the latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="0415e-213">將應用程式更新至 .NET 4.5，其包含位於「系統」命名空間中的 WIF 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="0415e-213">Update your application to .NET 4.5, which includes the newest version of WIF located in the System namespace.</span></span> <span data-ttu-id="0415e-214">然後，您可以使用 [驗證簽發者名稱登錄 (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) 來執行應用程式組態的自動更新。</span><span class="sxs-lookup"><span data-stu-id="0415e-214">You can then use the [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) to perform automatic updates of the application’s configuration.</span></span>
* <span data-ttu-id="0415e-215">根據本指導文件結尾的指示執行手動變換。</span><span class="sxs-lookup"><span data-stu-id="0415e-215">Perform a manual rollover as per the instructions at the end of this guidance document.</span></span>

<span data-ttu-id="0415e-216">使用 FedUtil 來更新組態的指示︰</span><span class="sxs-lookup"><span data-stu-id="0415e-216">Instructions to use the FedUtil to update your configuration:</span></span>

1. <span data-ttu-id="0415e-217">確認 Visual Studio 2008 或 2010 的開發電腦上已安裝 WIF v1.0 SDK。</span><span class="sxs-lookup"><span data-stu-id="0415e-217">Verify that you have the WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="0415e-218">如果尚未安裝，您可以[從這裡下載](https://www.microsoft.com/en-us/download/details.aspx?id=4451)。</span><span class="sxs-lookup"><span data-stu-id="0415e-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="0415e-219">在 Visual Studio 中開啟方案，然後以滑鼠右鍵按一下適用的專案，並選取 [更新同盟中繼資料] 。</span><span class="sxs-lookup"><span data-stu-id="0415e-219">In Visual Studio, open the solution, and then right-click the applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="0415e-220">如果無法使用此選項，則表示尚未安裝 FedUtil 和/或 WIF v1.0 SDK。</span><span class="sxs-lookup"><span data-stu-id="0415e-220">If this option is not available, FedUtil and/or the WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="0415e-221">在提示中選取 [更新]  ，開始更新同盟中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0415e-221">From the prompt, select **Update** to begin updating your federation metadata.</span></span> <span data-ttu-id="0415e-222">如果您可以存取裝載應用程式的伺服器環境，則可以選擇性地使用 FedUtil 的 [自動中繼資料更新排程器](https://msdn.microsoft.com/library/ee517272.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0415e-222">If you have access to the server environment where the application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="0415e-223">按一下 [完成]  以完成更新程序。</span><span class="sxs-lookup"><span data-stu-id="0415e-223">Click **Finish** to complete the update process.</span></span>

### <span data-ttu-id="0415e-224"><a name="other"></a>保護資源且使用任何其他程式庫或手動實作任何支援的通訊協定的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="0415e-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of the supported protocols</span></span>
<span data-ttu-id="0415e-225">如果您使用其他程式庫，或手動實作任何支援的通訊協定，您必須檢閱文件庫或您的實作，以確保從 OpenID Connect 探索文件或同盟中繼資料文件擷取金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-225">If you are using some other library or manually implemented any of the supported protocols, you'll need to review the library or your implementation to ensure that the key is being retrieved from either the OpenID Connect discovery document or the federation metadata document.</span></span> <span data-ttu-id="0415e-226">檢查的方法之一是在您的程式碼或程式庫的程式碼中，搜尋是否有任何呼叫 OpenID 探索文件或同盟中繼資料文件的情況。</span><span class="sxs-lookup"><span data-stu-id="0415e-226">One way to check for this is to do a search in your code or the library's code for any calls out to either the OpenID discovery document or the federation metadata document.</span></span>

<span data-ttu-id="0415e-227">如果金鑰儲存在某處或硬式編碼在您的應用程式中，您可以手動擷取金鑰並根據本指導文件結尾的指示執行手動變換來更新金鑰。</span><span class="sxs-lookup"><span data-stu-id="0415e-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve the key and update it accordingly by perform a manual rollover as per the instructions at the end of this guidance document.</span></span> <span data-ttu-id="0415e-228">**強烈建議您增強應用程式來支援自動變換** 時使用本文描述的任何方法，以免未來如果 Azure AD 提高變換頻率或臨時需要緊急變換時，造成運作中斷和超出負荷。</span><span class="sxs-lookup"><span data-stu-id="0415e-228">**It is strongly encouraged that you enhance your application to support automatic rollover** using any of the approaches outline in this article to avoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-to-test-your-application-to-determine-if-it-will-be-affected"></a><span data-ttu-id="0415e-229">如何測試您的應用程式，以判斷其是否會受影響</span><span class="sxs-lookup"><span data-stu-id="0415e-229">How to test your application to determine if it will be affected</span></span>
<span data-ttu-id="0415e-230">下載指令碼並依照 [此 GitHub 儲存機制](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="0415e-230">You can validate whether your application supports automatic key rollover by downloading the scripts and following the instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-to-perform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="0415e-231">如果應用程式不支援自動變換，如何執行手動變換</span><span class="sxs-lookup"><span data-stu-id="0415e-231">How to perform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="0415e-232">如果您的應用程式 **不** 支援自動變換，您必須先建立程序，該程序會定期監視 Azure AD 的簽署金鑰，並據此執行手動變換。</span><span class="sxs-lookup"><span data-stu-id="0415e-232">If your application does **not** support automatic rollover, you will need to establish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="0415e-233">[此 GitHub 儲存機制](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) 包含指令碼和如何執行這項操作的指示。</span><span class="sxs-lookup"><span data-stu-id="0415e-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how to do this.</span></span>

