---
title: "在 Azure AD 中的金鑰變換 aaaSigning |Microsoft 文件"
description: "這篇文章討論 hello Azure Active Directory 的簽署金鑰變換的最佳作法"
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
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a><span data-ttu-id="7ce9a-103">Azure Active Directory 中的簽署金鑰變換</span><span class="sxs-lookup"><span data-stu-id="7ce9a-103">Signing key rollover in Azure Active Directory</span></span>
<span data-ttu-id="7ce9a-104">本主題討論您需要 tooknow 有關 hello Azure Active Directory (Azure AD) toosign 安全性權杖中所使用的公用金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-104">This topic discusses what you need tooknow about hello public keys that are used in Azure Active Directory (Azure AD) toosign security tokens.</span></span> <span data-ttu-id="7ce9a-105">這些金鑰變換，定期執行，並在發生緊急狀況，無法回復透過立即的重要 toonote 它。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-105">It is important toonote that these keys rollover on a periodic basis and, in an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="7ce9a-106">使用 Azure AD 的所有應用程式應該可以 tooprogrammatically 控制代碼 hello 金鑰變換程序或建立定期手動變換程序。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-106">All applications that use Azure AD should be able tooprogrammatically handle hello key rollover process or establish a periodic manual rollover process.</span></span> <span data-ttu-id="7ce9a-107">繼續閱讀 toounderstand hello 金鑰的運作，如何 tooassess hello hello 變換 tooyour 應用程式的影響以及如何 tooupdate 您的應用程式或必要時，建立定期手動變換程序 toohandle 金鑰變換。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-107">Continue reading toounderstand how hello keys work, how tooassess hello impact of hello rollover tooyour application and how tooupdate your application or establish a periodic manual rollover process toohandle key rollover if necessary.</span></span>

## <a name="overview-of-signing-keys-in-azure-ad"></a><span data-ttu-id="7ce9a-108">Azure AD 中簽署金鑰的概觀</span><span class="sxs-lookup"><span data-stu-id="7ce9a-108">Overview of signing keys in Azure AD</span></span>
<span data-ttu-id="7ce9a-109">Azure AD 使用公開金鑰加密中根據業界標準 tooestablish 信任本身與 hello 之間使用它的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-109">Azure AD uses public-key cryptography built on industry standards tooestablish trust between itself and hello applications that use it.</span></span> <span data-ttu-id="7ce9a-110">實際上，這適用於下列方式 hello: Azure AD 使用公開和私密金鑰的金鑰組所組成的簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-110">In practical terms, this works in hello following way: Azure AD uses a signing key that consists of a public and private key pair.</span></span> <span data-ttu-id="7ce9a-111">當使用者登入時 tooan 應用程式使用 Azure AD 進行驗證時，Azure AD 會建立包含 hello 使用者的相關資訊的安全性權杖。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-111">When a user signs in tooan application that uses Azure AD for authentication, Azure AD creates a security token that contains information about hello user.</span></span> <span data-ttu-id="7ce9a-112">這個權杖是由 Azure AD 傳送後 toohello 應用程式之前，請使用其私密金鑰簽署。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-112">This token is signed by Azure AD using its private key before it is sent back toohello application.</span></span> <span data-ttu-id="7ce9a-113">hello 語彙基元的 tooverify 有效且確實來自 Azure AD，hello 應用程式必須驗證 hello 權杖之簽章使用 hello hello 租用戶中所包含的 Azure AD 所公開的公開金鑰[OpenID Connect 探索文件](http://openid.net/specs/openid-connect-discovery-1_0.html)或 SAML/Ws-fed[同盟中繼資料文件](active-directory-federation-metadata.md)。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-113">tooverify that hello token is valid and actually originated from Azure AD, hello application must validate hello token’s signature using hello public key exposed by Azure AD that is contained in hello tenant’s [OpenID Connect discovery document](http://openid.net/specs/openid-connect-discovery-1_0.html) or SAML/WS-Fed [federation metadata document](active-directory-federation-metadata.md).</span></span>

<span data-ttu-id="7ce9a-114">基於安全性考量，Azure AD 簽署金鑰彙定期執行，並在發生緊急狀況，hello 情況下無法回復立即。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-114">For security purposes, Azure AD’s signing key rolls on a periodic basis and, in hello case of an emergency, could be rolled over immediately.</span></span> <span data-ttu-id="7ce9a-115">任何與 Azure AD 整合的應用程式應該準備的 toohandle 金鑰變換事件無論就可能發生的頻率。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-115">Any application that integrates with Azure AD should be prepared toohandle a key rollover event no matter how frequently it may occur.</span></span> <span data-ttu-id="7ce9a-116">如果沒有，您的應用程式嘗試 toouse 權杖已過期的索引鍵 tooverify hello 簽章，hello 登入要求將會失敗。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-116">If it doesn’t, and your application attempts toouse an expired key tooverify hello signature on a token, hello sign-in request will fail.</span></span>

<span data-ttu-id="7ce9a-117">很多個有效的金鑰 hello OpenID Connect 探索文件與 hello 同盟中繼資料文件中可用。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-117">There is always more than one valid key available in hello OpenID Connect discovery document and hello federation metadata document.</span></span> <span data-ttu-id="7ce9a-118">您的應用程式應該準備的 toouse hello 機碼中任何指定的 hello 文件，由於其中一個索引鍵可能會過期，所以另一個可能是一個取代，等等。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-118">Your application should be prepared toouse any of hello keys specified in hello document, since one key may be rolled soon, another may be its replacement, and so forth.</span></span>

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a><span data-ttu-id="7ce9a-119">如何 tooassess 如果會影響您的應用程式和資訊，請參閱哪些 toodo</span><span class="sxs-lookup"><span data-stu-id="7ce9a-119">How tooassess if your application will be affected and what toodo about it</span></span>
<span data-ttu-id="7ce9a-120">您的應用程式處理金鑰變換的方式取決於變數，例如 hello 類型的應用程式，或使用何種身分識別通訊協定和文件庫。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-120">How your application handles key rollover depends on variables such as hello type of application or what identity protocol and library was used.</span></span> <span data-ttu-id="7ce9a-121">下列各節 hello 評估是否 hello 最常見的應用程式類型會受到 hello 金鑰變換並且提供指引 tooupdate hello toosupport 自動變換時，應用程式或手動更新 hello 機碼的方式。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-121">hello sections below assess whether hello most common types of applications are impacted by hello key rollover and provide guidance on how tooupdate hello application toosupport automatic rollover or manually update hello key.</span></span>

* [<span data-ttu-id="7ce9a-122">存取資源的原生用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce9a-122">Native client applications accessing resources</span></span>](#nativeclient)
* [<span data-ttu-id="7ce9a-123">存取資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-123">Web applications / APIs accessing resources</span></span>](#webclient)
* [<span data-ttu-id="7ce9a-124">保護資源且使用 Azure App Service 建置的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-124">Web applications / APIs protecting resources and built using Azure App Services</span></span>](#appservices)
* [<span data-ttu-id="7ce9a-125">使用 .NET OWIN OpenID Connect、WS-Fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-125">Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>](#owin)
* [<span data-ttu-id="7ce9a-126">使用 .NET Core OpenID Connect 或 JwtBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-126">Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>](#owincore)
* [<span data-ttu-id="7ce9a-127">使用 Node.js passport-azure-ad 模組保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-127">Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>](#passport)
* [<span data-ttu-id="7ce9a-128">保護資源且使用 Visual Studio 2015 或 Visual Studio 2017 建立的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-128">Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>](#vs2015)
* [<span data-ttu-id="7ce9a-129">保護資源且使用 Visual Studio 2013 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce9a-129">Web applications protecting resources and created with Visual Studio 2013</span></span>](#vs2013)
* [<span data-ttu-id="7ce9a-130">保護資源且使用 Visual Studio 2013 建立的 Web API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-130">Web APIs protecting resources and created with Visual Studio 2013</span></span>](#vs2013_webapi)
* [<span data-ttu-id="7ce9a-131">保護資源且使用 Visual Studio 2012 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce9a-131">Web applications protecting resources and created with Visual Studio 2012</span></span>](#vs2012)
* [<span data-ttu-id="7ce9a-132">保護資源且使用 Visual Studio 2010、2008 或使用 Windows Identity Foundation 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce9a-132">Web applications protecting resources and created with Visual Studio 2010, 2008 o using Windows Identity Foundation</span></span>](#vs2010)
* [<span data-ttu-id="7ce9a-133">Web 應用程式/保護資源的應用程式開發介面使用任何其他程式庫，或手動實作的 hello 任何支援的通訊協定</span><span class="sxs-lookup"><span data-stu-id="7ce9a-133">Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>](#other)

<span data-ttu-id="7ce9a-134">本指南 **不** 適用於︰</span><span class="sxs-lookup"><span data-stu-id="7ce9a-134">This guidance is **not** applicable for:</span></span>

* <span data-ttu-id="7ce9a-135">從 Azure AD 應用程式庫 （包括自訂） 加入的應用程式的相關事宜 toosigning 索引鍵的個別的指引。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-135">Applications added from Azure AD Application Gallery (including Custom) have separate guidance with regards toosigning keys.</span></span> [<span data-ttu-id="7ce9a-136">相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-136">More information.</span></span>](../active-directory-sso-certs.md)
* <span data-ttu-id="7ce9a-137">內部透過應用程式 proxy 發行應用程式都沒有 tooworry 有關簽署金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-137">On-premises applications published via application proxy don't have tooworry about signing keys.</span></span>

### <span data-ttu-id="7ce9a-138"><a name="nativeclient"></a>存取資源的原生用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce9a-138"><a name="nativeclient"></a>Native client applications accessing resources</span></span>
<span data-ttu-id="7ce9a-139">只存取資源 (亦即</span><span class="sxs-lookup"><span data-stu-id="7ce9a-139">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="7ce9a-140">Microsoft Graph、 KeyVault、 Outlook 應用程式開發介面和其他 Microsoft 應用程式開發介面） 通常只以取得權杖，並沿著傳遞 toohello 資源擁有者。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-140">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="7ce9a-141">假設它們沒有保護的任何資源，它們不會檢查 hello 語彙基元，並因此不需要的 tooensure 正確地簽署。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-141">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="7ce9a-142">原生用戶端應用程式，桌面或行動裝置，是否歸類到此類別，並因此不會受到 hello 換用。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-142">Native client applications, whether desktop or mobile, fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="7ce9a-143"><a name="webclient"></a>存取資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-143"><a name="webclient"></a>Web applications / APIs accessing resources</span></span>
<span data-ttu-id="7ce9a-144">只存取資源 (亦即</span><span class="sxs-lookup"><span data-stu-id="7ce9a-144">Applications that are only accessing resources (i.e</span></span> <span data-ttu-id="7ce9a-145">Microsoft Graph、 KeyVault、 Outlook 應用程式開發介面和其他 Microsoft 應用程式開發介面） 通常只以取得權杖，並沿著傳遞 toohello 資源擁有者。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-145">Microsoft Graph, KeyVault, Outlook API and other Microsoft APIs) generally only obtain a token and pass it along toohello resource owner.</span></span> <span data-ttu-id="7ce9a-146">假設它們沒有保護的任何資源，它們不會檢查 hello 語彙基元，並因此不需要的 tooensure 正確地簽署。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-146">Given that they are not protecting any resources, they do not inspect hello token and therefore do not need tooensure it is properly signed.</span></span>

<span data-ttu-id="7ce9a-147">Web 應用程式和 web 應用程式開發介面中使用 hello 僅限應用程式流程 (用戶端認證 / 用戶端憑證) 歸類到此類別，因此不會受到 hello 換用。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-147">Web applications and web APIs that are using hello app-only flow (client credentials / client certificate), fall into this category and are thus not impacted by hello rollover.</span></span>

### <span data-ttu-id="7ce9a-148"><a name="appservices"></a>保護資源且使用 Azure App Service 建置的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-148"><a name="appservices"></a>Web applications / APIs protecting resources and built using Azure App Services</span></span>
<span data-ttu-id="7ce9a-149">Azure 應用程式服務的驗證 / 授權 (EasyAuth) 功能已擁有 hello 必要的邏輯 toohandle 金鑰變換自動。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-149">Azure App Services' Authentication / Authorization (EasyAuth) functionality already has hello necessary logic toohandle key rollover automatically.</span></span>

### <span data-ttu-id="7ce9a-150"><a name="owin"></a>使用 .NET OWIN OpenID Connect、WS-Fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-150"><a name="owin"></a>Web applications / APIs protecting resources using .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware</span></span>
<span data-ttu-id="7ce9a-151">如果您的應用程式正在使用 hello.NET OWIN OpenID Connect，Ws-fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體，它已經 hello 必要的邏輯 toohandle 金鑰變換自動。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-151">If your application is using hello .NET OWIN OpenID Connect, WS-Fed or WindowsAzureActiveDirectoryBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="7ce9a-152">您可以確認您的應用程式正在使用任何這些尋找任何下列程式碼片段，在您的應用程式 Startup.cs 或 Startup.Auth.cs hello</span><span class="sxs-lookup"><span data-stu-id="7ce9a-152">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="7ce9a-153"><a name="owincore"></a>使用 .NET Core OpenID Connect 或 JwtBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-153"><a name="owincore"></a>Web applications / APIs protecting resources using .NET Core OpenID Connect or  JwtBearerAuthentication middleware</span></span>
<span data-ttu-id="7ce9a-154">如果您的應用程式使用.NET 核心 OWIN OpenID Connect 的 hello 或 JwtBearerAuthentication 中介軟體，它已經 hello 必要的邏輯 toohandle 金鑰變換自動。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-154">If your application is using hello .NET Core OWIN OpenID Connect  or JwtBearerAuthentication middleware, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="7ce9a-155">您可以確認您的應用程式正在使用任何這些尋找任何下列程式碼片段，在您的應用程式 Startup.cs 或 Startup.Auth.cs hello</span><span class="sxs-lookup"><span data-stu-id="7ce9a-155">You can confirm that your application is using any of these by looking for any of hello following snippets in your application's Startup.cs or Startup.Auth.cs</span></span>

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

### <span data-ttu-id="7ce9a-156"><a name="passport"></a>使用 Node.js passport-azure-ad 模組保護資源的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-156"><a name="passport"></a>Web applications / APIs protecting resources using Node.js passport-azure-ad module</span></span>
<span data-ttu-id="7ce9a-157">如果您的應用程式使用 hello Node.js passport ad 模組，它已經有 hello 必要的邏輯 toohandle 金鑰變換自動。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-157">If your application is using hello Node.js passport-ad module, it already has hello necessary logic toohandle key rollover automatically.</span></span>

<span data-ttu-id="7ce9a-158">您可以確認您的應用程式 passport ad 藉由搜尋下列程式碼片段，在您的應用程式 app.js hello</span><span class="sxs-lookup"><span data-stu-id="7ce9a-158">You can confirm that your application passport-ad by searching for hello following snippet in your application's app.js</span></span>

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <span data-ttu-id="7ce9a-159"><a name="vs2015"></a>保護資源且使用 Visual Studio 2015 或 Visual Studio 2017 建立的 Web 應用程式 / API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-159"><a name="vs2015"></a>Web applications / APIs protecting resources and created with Visual Studio 2015 or Visual Studio 2017</span></span>
<span data-ttu-id="7ce9a-160">如果使用 Visual Studio 2015 或 Visual Studio 2017 中的 web 應用程式範本建置您的應用程式，而且您選取**工作及學校帳戶**從 hello**變更驗證**功能表上，它已經會自動擁有 hello 必要的邏輯 toohandle 金鑰變換。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-160">If your application was built using a web application template in Visual Studio 2015 or Visual Studio 2017 and you selected **Work And School Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="7ce9a-161">這個邏輯內嵌在 hello OWIN OpenID Connect 中介軟體，擷取和快取 hello hello OpenID Connect 探索文件中的索引鍵，而且會定期重新整理。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-161">This logic, embedded in hello OWIN OpenID Connect middleware, retrieves and caches hello keys from hello OpenID Connect discovery document and periodically refreshes them.</span></span>

<span data-ttu-id="7ce9a-162">如果您手動加入驗證 tooyour 解決方案，您的應用程式可能沒有 hello 必要金鑰變換邏輯。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-162">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="7ce9a-163">您將需要 toowrite 它自己，或遵循 hello 中的步驟[Web 應用程式 / 應用程式開發介面使用任何其他程式庫，或手動實作的 hello 任何支援的通訊協定。](#other)。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-163">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

### <span data-ttu-id="7ce9a-164"><a name="vs2013"></a>保護資源且使用 Visual Studio 2013 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce9a-164"><a name="vs2013"></a>Web applications protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="7ce9a-165">如果使用 Visual Studio 2013 中的 web 應用程式範本建置您的應用程式，而且您選取**組織帳戶**從 hello**變更驗證**功能表上，已有 hello 必要邏輯 toohandle 自動金鑰變換。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-165">If your application was built using a web application template in Visual Studio 2013 and you selected **Organizational Accounts** from hello **Change Authentication** menu, it already has hello necessary logic toohandle key rollover automatically.</span></span> <span data-ttu-id="7ce9a-166">此邏輯會儲存您的組織唯一識別碼和簽署金鑰資訊與 hello 專案相關聯的兩個資料庫資料表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-166">This logic stores your organization’s unique identifier and hello signing key information in two database tables associated with hello project.</span></span> <span data-ttu-id="7ce9a-167">您可以在 hello 專案的 Web.config 檔案中找到 hello 資料庫 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-167">You can find hello connection string for hello database in hello project’s Web.config file.</span></span>

<span data-ttu-id="7ce9a-168">如果您手動加入驗證 tooyour 解決方案，您的應用程式可能沒有 hello 必要金鑰變換邏輯。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-168">If you added authentication tooyour solution manually, your application might not have hello necessary key rollover logic.</span></span> <span data-ttu-id="7ce9a-169">您將需要 toowrite 它自己，或遵循 hello 中的步驟[Web 應用程式 / 應用程式開發介面使用任何其他程式庫，或手動實作的 hello 任何支援的通訊協定。](#other)。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-169">You will need toowrite it yourself, or follow hello steps in [Web applications / APIs using any other libraries or manually implementing any of hello supported protocols.](#other).</span></span>

<span data-ttu-id="7ce9a-170">hello 下列步驟將協助您確認 hello 邏輯正常運作，您的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-170">hello following steps will help you verify that hello logic is working properly in your application.</span></span>

1. <span data-ttu-id="7ce9a-171">在 Visual Studio 2013 中，開啟 hello 方案，然後按一下 hello**伺服器總管**hello 右側視窗上的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-171">In Visual Studio 2013, open hello solution, and then click on hello **Server Explorer** tab on hello right window.</span></span>
2. <span data-ttu-id="7ce9a-172">依序展開 [資料連線]、[DefaultConnection]、[資料表]。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-172">Expand **Data Connections**, **DefaultConnection**, and then **Tables**.</span></span> <span data-ttu-id="7ce9a-173">找出 hello **IssuingAuthorityKeys**資料表，以滑鼠右鍵按一下，然後按**顯示資料表資料**。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-173">Locate hello **IssuingAuthorityKeys** table, right-click it, and then click **Show Table Data**.</span></span>
3. <span data-ttu-id="7ce9a-174">在 hello **IssuingAuthorityKeys**資料表中，會有至少一個資料列，對應 toohello hello 金鑰的憑證指紋值。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-174">In hello **IssuingAuthorityKeys** table, there will be at least one row, which corresponds toohello thumbprint value for hello key.</span></span> <span data-ttu-id="7ce9a-175">刪除 hello 資料表中的任何資料列。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-175">Delete any rows in hello table.</span></span>
4. <span data-ttu-id="7ce9a-176">以滑鼠右鍵按一下 hello**租用戶**資料表，然後按一下**顯示資料表資料**。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-176">Right-click hello **Tenants** table, and then click **Show Table Data**.</span></span>
5. <span data-ttu-id="7ce9a-177">在 hello**租用戶**資料表中，會有對應 tooa 唯一的目錄租用戶識別碼的至少一個資料列。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-177">In hello **Tenants** table, there will be at least one row, which corresponds tooa unique directory tenant identifier.</span></span> <span data-ttu-id="7ce9a-178">刪除 hello 資料表中的任何資料列。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-178">Delete any rows in hello table.</span></span> <span data-ttu-id="7ce9a-179">如果您未刪除 hello 資料列，在這兩個 hello**租用戶**資料表和**IssuingAuthorityKeys**資料表，就會在執行階段發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-179">If you don't delete hello rows in both hello **Tenants** table and **IssuingAuthorityKeys** table, you will get an error at runtime.</span></span>
6. <span data-ttu-id="7ce9a-180">建置並執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-180">Build and run hello application.</span></span> <span data-ttu-id="7ce9a-181">您已登入 tooyour 帳戶之後，您可以停止 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-181">After you have logged in tooyour account, you can stop hello application.</span></span>
7. <span data-ttu-id="7ce9a-182">傳回 toohello**伺服器總管**並查看 hello 中的 hello 值**IssuingAuthorityKeys**和**租用戶**資料表。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-182">Return toohello **Server Explorer** and look at hello values in hello **IssuingAuthorityKeys** and **Tenants** table.</span></span> <span data-ttu-id="7ce9a-183">您會發現，他們具有已自動重新擴展 hello hello 同盟中繼資料文件的適當資訊。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-183">You’ll notice that they have been automatically repopulated with hello appropriate information from hello federation metadata document.</span></span>

### <span data-ttu-id="7ce9a-184"><a name="vs2013"></a>保護資源且使用 Visual Studio 2013 建立的 Web API</span><span class="sxs-lookup"><span data-stu-id="7ce9a-184"><a name="vs2013"></a>Web APIs protecting resources and created with Visual Studio 2013</span></span>
<span data-ttu-id="7ce9a-185">如果您使用 hello Web API 範本時，Visual Studio 2013 中建立 web API 應用程式，然後選取**組織帳戶**從 hello**變更驗證**功能表上，您已擁有 hello必要應用程式中的邏輯。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-185">If you created a web API application in Visual Studio 2013 using hello Web API template, and then selected **Organizational Accounts** from hello **Change Authentication** menu, you already have hello necessary logic in your application.</span></span>

<span data-ttu-id="7ce9a-186">如果您手動設定驗證，請遵循以下 toolearn hello 指示如何 tooconfigure Web API tooautomatically 更新金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-186">If you manually configured authentication, follow hello instructions below toolearn how tooconfigure your Web API tooautomatically update its key information.</span></span>

<span data-ttu-id="7ce9a-187">hello 下列程式碼片段示範如何 tooget hello hello 同盟中繼資料文件，取得最新的金鑰，然後再使用 hello [JWT 權杖處理常式](https://msdn.microsoft.com/library/dn205065.aspx)toovalidate hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-187">hello following code snippet demonstrates how tooget hello latest keys from hello federation metadata document, and then use hello [JWT Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello token.</span></span> <span data-ttu-id="7ce9a-188">hello 程式碼片段假設您將使用您自己的快取機制來保存 hello 金鑰 toovalidate 未來語彙基元從 Azure AD，無論在資料庫、 組態檔或其他位置。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-188">hello code snippet assumes that you will use your own caching mechanism for persisting hello key toovalidate future tokens from Azure AD, whether it be in a database, configuration file, or elsewhere.</span></span>

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

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
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
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
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

### <span data-ttu-id="7ce9a-189"><a name="vs2012"></a>保護資源且使用 Visual Studio 2012 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce9a-189"><a name="vs2012"></a>Web applications protecting resources and created with Visual Studio 2012</span></span>
<span data-ttu-id="7ce9a-190">如果在 Visual Studio 2012 中建置您的應用程式時，您可能使用 hello 身分識別和存取工具 tooconfigure 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-190">If your application was built in Visual Studio 2012, you probably used hello Identity and Access Tool tooconfigure your application.</span></span> <span data-ttu-id="7ce9a-191">也很可能您使用 hello[驗證簽發者名稱登錄 (VINR)](https://msdn.microsoft.com/library/dn205067.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-191">It’s also likely that you are using hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx).</span></span> <span data-ttu-id="7ce9a-192">hello VINR 負責維護關於信任的身分識別提供者 (Azure AD) 的資訊和 hello 金鑰用於其所發行的 toovalidate 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-192">hello VINR is responsible for maintaining information about trusted identity providers (Azure AD) and hello keys used toovalidate tokens issued by them.</span></span> <span data-ttu-id="7ce9a-193">hello VINR 也很容易 tooautomatically 更新 hello 金鑰資訊儲存在 Web.config 檔案中下載 hello 最新的同盟中繼資料文件與您的目錄，檢查是否 hello 組態 hello 與最新相關聯文件和更新 hello 應用程式 toouse hello 新索引鍵為必要。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-193">hello VINR also makes it easy tooautomatically update hello key information stored in a Web.config file by downloading hello latest federation metadata document associated with your directory, checking if hello configuration is out of date with hello latest document, and updating hello application toouse hello new key as necessary.</span></span>

<span data-ttu-id="7ce9a-194">如果您建立使用 hello 程式碼範例或 Microsoft 所提供的逐步解說文任何的件應用程式，您的專案中已經包含 hello 金鑰變換邏輯。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-194">If you created your application using any of hello code samples or walkthrough documentation provided by Microsoft, hello key rollover logic is already included in your project.</span></span> <span data-ttu-id="7ce9a-195">您會發現以下的 hello 程式碼已經存在專案中。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-195">You will notice that hello code below already exists in your project.</span></span> <span data-ttu-id="7ce9a-196">如果您的應用程式尚無此邏輯，步驟 hello 下方 tooadd 它，它正常運作的 tooverify。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-196">If your application does not already have this logic, follow hello steps below tooadd it and tooverify that it’s working correctly.</span></span>

1. <span data-ttu-id="7ce9a-197">在**方案總管 中**，新增參考 toohello **System.IdentityModel** hello 適當的專案的組件。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-197">In **Solution Explorer**, add a reference toohello **System.IdentityModel** assembly for hello appropriate project.</span></span>
2. <span data-ttu-id="7ce9a-198">開啟 hello **Global.asax.cs**檔案，然後加入 hello 下列 using 指示詞：</span><span class="sxs-lookup"><span data-stu-id="7ce9a-198">Open hello **Global.asax.cs** file and add hello following using directives:</span></span>
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. <span data-ttu-id="7ce9a-199">新增下列方法 toohello hello **Global.asax.cs**檔案：</span><span class="sxs-lookup"><span data-stu-id="7ce9a-199">Add hello following method toohello **Global.asax.cs** file:</span></span>
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. <span data-ttu-id="7ce9a-200">叫用 hello **Refreshvalidationsettings**方法在 hello **application_start （)**方法中的**Global.asax.cs**所示：</span><span class="sxs-lookup"><span data-stu-id="7ce9a-200">Invoke hello **RefreshValidationSettings()** method in hello **Application_Start()** method in **Global.asax.cs** as shown:</span></span>
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

<span data-ttu-id="7ce9a-201">一旦您已遵循下列步驟，將會 hello 最新資訊 hello 同盟中繼資料文件，包括 hello 最新的金鑰更新應用程式的 Web.config。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-201">Once you have followed these steps, your application’s Web.config will be updated with hello latest information from hello federation metadata document, including hello latest keys.</span></span> <span data-ttu-id="7ce9a-202">每次應用程式集區回收 IIS; 中，會進行更新根據預設 IIS 設定 toorecycle 應用程式每 29 小時。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-202">This update will occur every time your application pool recycles in IIS; by default IIS is set toorecycle applications every 29 hours.</span></span>

<span data-ttu-id="7ce9a-203">請遵循以下 hello 金鑰變換邏輯運作的 tooverify hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-203">Follow hello steps below tooverify that hello key rollover logic is working.</span></span>

1. <span data-ttu-id="7ce9a-204">確認您的應用程式正在使用 hello 開啟 hello 上面的程式碼之後**Web.config**檔案，並瀏覽 toohello  **<issuerNameRegistry>** 區塊，並特別尋找下列幾行 hello:</span><span class="sxs-lookup"><span data-stu-id="7ce9a-204">After you have verified that your application is using hello code above, open hello **Web.config** file and navigate toohello **<issuerNameRegistry>** block, specifically looking for hello following few lines:</span></span>
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. <span data-ttu-id="7ce9a-205">在 hello  **<add thumbprint=””>** 設定，以不同的字元完全取代將 hello 指紋值。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-205">In hello **<add thumbprint=””>** setting, change hello thumbprint value by replacing any character with a different one.</span></span> <span data-ttu-id="7ce9a-206">儲存 hello **Web.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-206">Save hello **Web.config** file.</span></span>
3. <span data-ttu-id="7ce9a-207">建置 hello 應用程式，然後執行它。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-207">Build hello application, and then run it.</span></span> <span data-ttu-id="7ce9a-208">如果您可以完成 hello 登入程序，您的應用程式已成功更新 hello 金鑰您目錄中的同盟中繼資料文件下載 hello 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-208">If you can complete hello sign-in process, your application is successfully updating hello key by downloading hello required information from your directory’s federation metadata document.</span></span> <span data-ttu-id="7ce9a-209">如果您有登入的問題，請確認您的應用程式中的 hello 變更是否正確讀取 hello[加入登入 tooYour Web 應用程式使用 Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)主題，或是下載並檢查下列程式碼範例的 hello: [多租用戶雲端應用程式的 Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b)。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-209">If you are having issues signing in, ensure hello changes in your application are correct by reading hello [Adding Sign-On tooYour Web Application Using Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) topic, or downloading and inspecting hello following code sample: [Multi-Tenant Cloud Application for Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).</span></span>

### <span data-ttu-id="7ce9a-210"><a name="vs2010"></a>保護資源且使用 Visual Studio 2008 或 2010 和 Windows Identity Foundation (WIF) v1.0 for .NET 3.5 建立的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ce9a-210"><a name="vs2010"></a>Web applications protecting resources and created with Visual Studio 2008 or 2010 and Windows Identity Foundation (WIF) v1.0 for .NET 3.5</span></span>
<span data-ttu-id="7ce9a-211">如果建置 WIF v1.0 上的應用程式時，就沒有提供的機制 tooautomatically 重新整理您的應用程式組態 toouse 新的金鑰。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-211">If you built an application on WIF v1.0, there is no provided mechanism tooautomatically refresh your application’s configuration toouse a new key.</span></span>

* <span data-ttu-id="7ce9a-212">*最簡單的方式*使用 hello FedUtil 工具 hello WIF SDK，它可以擷取 hello 最新的中繼資料文件並更新您的組態中。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-212">*Easiest way* Use hello FedUtil tooling included in hello WIF SDK, which can retrieve hello latest metadata document and update your configuration.</span></span>
* <span data-ttu-id="7ce9a-213">更新您的應用程式 too.NET 4.5，其中包括 hello 位於 hello 系統命名空間的 WIF 最新版本。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-213">Update your application too.NET 4.5, which includes hello newest version of WIF located in hello System namespace.</span></span> <span data-ttu-id="7ce9a-214">然後，您可以使用 hello[驗證簽發者名稱登錄 (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform hello 應用程式之組態的自動更新。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-214">You can then use hello [Validating Issuer Name Registry (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform automatic updates of hello application’s configuration.</span></span>
* <span data-ttu-id="7ce9a-215">執行手動的換用根據 hello 指示 hello 指引文件結尾。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-215">Perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span>

<span data-ttu-id="7ce9a-216">Toouse hello FedUtil tooupdate 您設定的指示：</span><span class="sxs-lookup"><span data-stu-id="7ce9a-216">Instructions toouse hello FedUtil tooupdate your configuration:</span></span>

1. <span data-ttu-id="7ce9a-217">確認您擁有 hello WIF v1.0 SDK 開發電腦上安裝 Visual Studio 2008 或 2010年。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-217">Verify that you have hello WIF v1.0 SDK installed on your development machine for Visual Studio 2008 or 2010.</span></span> <span data-ttu-id="7ce9a-218">如果尚未安裝，您可以[從這裡下載](https://www.microsoft.com/en-us/download/details.aspx?id=4451)。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-218">You can [download it from here](https://www.microsoft.com/en-us/download/details.aspx?id=4451) if you have not yet installed it.</span></span>
2. <span data-ttu-id="7ce9a-219">在 Visual Studio 中，開啟 hello 方案然後 hello 適用的專案上按一下滑鼠右鍵並選取**更新同盟中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-219">In Visual Studio, open hello solution, and then right-click hello applicable project and select **Update federation metadata**.</span></span> <span data-ttu-id="7ce9a-220">如果不使用此選項，則尚未安裝 FedUtil 和/或 hello WIF v1.0 SDK。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-220">If this option is not available, FedUtil and/or hello WIF v1.0 SDK has not been installed.</span></span>
3. <span data-ttu-id="7ce9a-221">從 hello 提示字元中，選取**更新**toobegin 更新您的同盟中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-221">From hello prompt, select **Update** toobegin updating your federation metadata.</span></span> <span data-ttu-id="7ce9a-222">如果您有存取 toohello 伺服器環境中裝載 hello 應用程式，您可以選擇使用 FedUtil 的[中繼資料自動更新排程器](https://msdn.microsoft.com/library/ee517272.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-222">If you have access toohello server environment where hello application is hosted, you can optionally use FedUtil’s [automatic metadata update scheduler](https://msdn.microsoft.com/library/ee517272.aspx).</span></span>
4. <span data-ttu-id="7ce9a-223">按一下**完成**toocomplete hello 更新程序。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-223">Click **Finish** toocomplete hello update process.</span></span>

### <span data-ttu-id="7ce9a-224"><a name="other"></a>Web 應用程式/保護資源的應用程式開發介面使用任何其他程式庫，或手動實作的 hello 任何支援的通訊協定</span><span class="sxs-lookup"><span data-stu-id="7ce9a-224"><a name="other"></a>Web applications / APIs protecting resources using any other libraries or manually implementing any of hello supported protocols</span></span>
<span data-ttu-id="7ce9a-225">如果您使用其他程式庫，或手動實作的任何支援的 hello 通訊協定，您將需要 tooreview hello 文件庫或 hello 金鑰您實作 tooensure 會從 hello OpenID Connect 探索文件或 hello同盟中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-225">If you are using some other library or manually implemented any of hello supported protocols, you'll need tooreview hello library or your implementation tooensure that hello key is being retrieved from either hello OpenID Connect discovery document or hello federation metadata document.</span></span> <span data-ttu-id="7ce9a-226">針對這其中一種方式 toocheck 是 toodo tooeither hello OpenID 探索文件或 hello 同盟中繼資料文件的任何呼叫您的程式碼或 hello 程式庫程式碼中的搜尋。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-226">One way toocheck for this is toodo a search in your code or hello library's code for any calls out tooeither hello OpenID discovery document or hello federation metadata document.</span></span>

<span data-ttu-id="7ce9a-227">如果索引鍵某處儲存或硬式編碼應用程式中的，您可以手動擷取 hello 金鑰和它據以執行手動的換用根據 hello 指示在 hello 結尾此指引文件的更新。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-227">If they key is being stored somewhere or hardcoded in your application, you can manually retrieve hello key and update it accordingly by perform a manual rollover as per hello instructions at hello end of this guidance document.</span></span> <span data-ttu-id="7ce9a-228">**強烈鼓勵您加強您的應用程式 toosupport 自動變換**如果 Azure AD 會增加它的容錯移轉模式，或者使用任何 hello 接近這個發行項 tooavoid 未來中斷與額外負荷外的框緊急的頻外換用。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-228">**It is strongly encouraged that you enhance your application toosupport automatic rollover** using any of hello approaches outline in this article tooavoid future disruptions and overhead if Azure AD increases it's rollover cadence or has an emergency out-of-band rollover.</span></span>

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a><span data-ttu-id="7ce9a-229">如何 tootest 會受到影響，如果您的應用程式 toodetermine</span><span class="sxs-lookup"><span data-stu-id="7ce9a-229">How tootest your application toodetermine if it will be affected</span></span>
<span data-ttu-id="7ce9a-230">您可以驗證您的應用程式支援自動金鑰變換下載 hello 指令碼和中的 hello 指示是否[這個 GitHub 儲存機制。](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span><span class="sxs-lookup"><span data-stu-id="7ce9a-230">You can validate whether your application supports automatic key rollover by downloading hello scripts and following hello instructions in [this GitHub repository.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)</span></span>

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a><span data-ttu-id="7ce9a-231">如何 tooperform 手動變換，如果您的應用程式不支援自動變換</span><span class="sxs-lookup"><span data-stu-id="7ce9a-231">How tooperform a manual rollover if you application does not support automatic rollover</span></span>
<span data-ttu-id="7ce9a-232">如果應用程式**不**支援自動變換，您將需要的處理序，定期監視 Azure AD 的簽署金鑰，並執行手動的換用 tooestablish 據以。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-232">If your application does **not** support automatic rollover, you will need tooestablish a process that periodically monitors Azure AD's signing keys and performs a manual rollover accordingly.</span></span> <span data-ttu-id="7ce9a-233">[此 GitHub 儲存機制](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)包含指令碼和指示 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="7ce9a-233">[This GitHub repository](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contains scripts and instructions on how toodo this.</span></span>

