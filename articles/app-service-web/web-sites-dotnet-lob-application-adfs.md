---
title: "aaaCreate 具有 AD FS 驗證的特定業務 Azure 應用程式 |Microsoft 文件"
description: "了解如何 toocreate 向的 Azure App Service 中的特定業務應用程式在內部部署 STS。 本教學課程的目標為 hello 內部部署 STS 的 AD FS。"
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="5d778-104">使用 AD FS 驗證建立企業營運 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="5d778-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="5d778-105">本文章將示範如何 toocreate ASP.NET MVC 的特定業務應用程式中[Azure App Service](../app-service/app-service-value-prop-what-is.md)使用內部[Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx)為 hello 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="5d778-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="5d778-106">您希望 toocreate Azure App Service 中的特定業務應用程式，而您的組織需要離站儲存目錄資料 toobe 時，可以處理此案例中。</span><span class="sxs-lookup"><span data-stu-id="5d778-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="5d778-107">如需 hello 不同的企業驗證和授權選項的 Azure 應用程式服務的概觀，請參閱[與 Azure 應用程式中的內部部署 Active Directory 驗證](web-sites-authentication-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="5d778-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="5d778-108">將建置的項目</span><span class="sxs-lookup"><span data-stu-id="5d778-108">What you will build</span></span>
<span data-ttu-id="5d778-109">您會建立基本的 ASP.NET 應用程式在 Azure App Service Web 應用程式中以 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="5d778-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="5d778-110">根據 AD FS 驗證使用者</span><span class="sxs-lookup"><span data-stu-id="5d778-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="5d778-111">使用`[Authorize]`tooauthorize 使用者不同的動作</span><span class="sxs-lookup"><span data-stu-id="5d778-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="5d778-112">在 Visual Studio 中偵錯和發行 tooApp Service Web 應用程式的靜態設定 （一次設定、 偵錯及發行任何時間）</span><span class="sxs-lookup"><span data-stu-id="5d778-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="5d778-113">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="5d778-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="5d778-114">本教學課程，您需要 hello 下列 toocomplete 中：</span><span class="sxs-lookup"><span data-stu-id="5d778-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="5d778-115">內部部署 AD FS 部署 (如 hello 這個教學課程中使用的測試實驗室的端對端逐步解說，請參閱[測試實驗室： 獨立 STS 使用 AD FS （適用於僅限於測試） 的 Azure VM 中](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="5d778-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="5d778-116">中 AD FS 管理的權限 toocreate 信賴憑證者信任</span><span class="sxs-lookup"><span data-stu-id="5d778-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="5d778-117">Visual Studio 2013 Update 4 或更新版本</span><span class="sxs-lookup"><span data-stu-id="5d778-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="5d778-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) 或更新版本</span><span class="sxs-lookup"><span data-stu-id="5d778-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="5d778-119">使用特定業務範本的範例應用程式</span><span class="sxs-lookup"><span data-stu-id="5d778-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="5d778-120">hello 範例應用程式，在本教學課程， [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet)，hello Azure Active Directory 團隊所建立。</span><span class="sxs-lookup"><span data-stu-id="5d778-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="5d778-121">由於 AD FS 支援 WS-同盟，您可以使用它做為範本 toocreate 特定業務應用程式就能輕鬆。</span><span class="sxs-lookup"><span data-stu-id="5d778-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="5d778-122">它有下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d778-122">It has hello following features:</span></span>

* <span data-ttu-id="5d778-123">使用[WS-同盟](http://msdn.microsoft.com/library/bb498017.aspx)tooauthenticate 與內部部署 AD FS 部署</span><span class="sxs-lookup"><span data-stu-id="5d778-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="5d778-124">登入和登出功能</span><span class="sxs-lookup"><span data-stu-id="5d778-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="5d778-125">使用[Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana)是 （而不是 Windows Identity Foundation)，其中 hello 未來的 ASP.NET 和更簡單 tooset 進行驗證和授權比 WIF</span><span class="sxs-lookup"><span data-stu-id="5d778-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="5d778-126">設定 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="5d778-126">Set up hello sample application</span></span>
1. <span data-ttu-id="5d778-127">複製或下載 hello 範例解決方案在[WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="5d778-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5d778-128">hello 指示[README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md)告訴您如何 tooset hello 與 Azure Active Directory 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d778-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="5d778-129">但在本教學課程中，使用 AD FS 進行設定，因此請改為遵循此處 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="5d778-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="5d778-130">開啟 hello 方案，然後開啟 hello 中的 [Controllers\AccountController.cs**方案總管] 中**。</span><span class="sxs-lookup"><span data-stu-id="5d778-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="5d778-131">您會看見 hello 程式碼只是發出使用 WS-同盟驗證挑戰 tooauthenticate hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="5d778-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="5d778-132">所有驗證都是在 App_Start\Startup.Auth.cs 中設定。</span><span class="sxs-lookup"><span data-stu-id="5d778-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="5d778-133">開啟 App_Start\Startup.Auth.cs。</span><span class="sxs-lookup"><span data-stu-id="5d778-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="5d778-134">在 hello`ConfigureAuth`方法，請注意 hello 行：</span><span class="sxs-lookup"><span data-stu-id="5d778-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="5d778-135">在 hello OWIN 世界中，此程式碼片段，實際上是 hello 裸機您需要 tooconfigure WS-同盟驗證最小值。</span><span class="sxs-lookup"><span data-stu-id="5d778-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="5d778-136">它是更為簡單且更有質感比 WIF，其中 Web.config 會插入 XML 與整個 hello 的地方。</span><span class="sxs-lookup"><span data-stu-id="5d778-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="5d778-137">hello 只有您所需要的資訊為 hello 信賴憑證者合作對象的 (RP) 的 AD FS 服務的中繼資料檔中的識別項和 hello URL。</span><span class="sxs-lookup"><span data-stu-id="5d778-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="5d778-138">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="5d778-138">Here's an example:</span></span>
   
   * <span data-ttu-id="5d778-139">RP 識別碼： `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="5d778-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="5d778-140">中繼資料位址：`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="5d778-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="5d778-141">在 App_Start\Startup.Auth.cs，來變更下列靜態字串定義 hello:</span><span class="sxs-lookup"><span data-stu-id="5d778-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="5d778-142">現在，在 Web.config 中請 hello 相對應的變更。開啟 hello Web.config 並修改下列應用程式設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d778-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="5d778-143">填滿根據個別環境的 hello 機碼值。</span><span class="sxs-lookup"><span data-stu-id="5d778-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="5d778-144">建置應用程式 hello toomake，確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="5d778-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="5d778-145">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="5d778-145">That's it.</span></span> <span data-ttu-id="5d778-146">Hello 範例應用程式已準備好 toowork 與 AD FS。</span><span class="sxs-lookup"><span data-stu-id="5d778-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="5d778-147">您仍然需要 tooconfigure RP trust，稍後在 AD FS 中此應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d778-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="5d778-148">部署 hello 範例應用程式 tooAzure App Service Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5d778-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="5d778-149">在這裡，您發行 hello 應用程式 tooa web 應用程式在 App Service Web 應用程式中同時保留 hello 偵錯環境。</span><span class="sxs-lookup"><span data-stu-id="5d778-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="5d778-150">請注意，您將 toopublish hello 應用程式之前，驗證仍無法運作尚未有與 AD FS RP trust。</span><span class="sxs-lookup"><span data-stu-id="5d778-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="5d778-151">不過，如果您這樣做現在您可以有您可以稍後使用 tooconfigure hello RP trust hello web 應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="5d778-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="5d778-152">以滑鼠右鍵按一下專案，然後選取 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="5d778-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="5d778-153">選取 [ **Microsoft Azure App Service**]。</span><span class="sxs-lookup"><span data-stu-id="5d778-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="5d778-154">如果您尚未 tooAzure 中，按一下**登入**hello Microsoft 帳戶以用於您的 Azure 訂用帳戶 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="5d778-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="5d778-155">一旦登入，請按一下**新增**toocreate web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d778-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="5d778-156">填寫所有必要欄位。</span><span class="sxs-lookup"><span data-stu-id="5d778-156">Fill in all required fields.</span></span> <span data-ttu-id="5d778-157">您即將 tooconnect tooon 內部部署資料更新版本中，因此不會建立此 web 應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="5d778-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="5d778-158">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5d778-158">Click **Create**.</span></span> <span data-ttu-id="5d778-159">一旦建立 hello web 應用程式時，會開啟 hello 發行 Web 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5d778-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="5d778-160">在**目的地 URL**，變更**http**太**https**。</span><span class="sxs-lookup"><span data-stu-id="5d778-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="5d778-161">複製 hello 整個 URL tooa 文字編輯器以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="5d778-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="5d778-162">然後按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="5d778-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="5d778-163">在 Visual Studio 中，開啟專案中的 **Web.Release.config** 。</span><span class="sxs-lookup"><span data-stu-id="5d778-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="5d778-164">插入下列 XML 到 hello hello`<configuration>`標記，並以發行 web 應用程式的 URL 取代 hello 索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="5d778-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="5d778-165">當您完成時，您有兩個 RP 識別項在您的專案，一個用於您在 Visual Studio 中的偵錯環境中設定，一個用於 hello 發行 web 應用程式在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="5d778-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="5d778-166">您會設定 RP trust 每個 AD FS 中的 hello 兩個環境。</span><span class="sxs-lookup"><span data-stu-id="5d778-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="5d778-167">偵錯期間，在 Web.config 中的 hello 應用程式設定為使用的 toomake 您**偵錯**與 AD FS 組態工作。</span><span class="sxs-lookup"><span data-stu-id="5d778-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="5d778-168">發行時 (根據預設，hello**發行**發行組態)，已轉換的 Web.config 上傳，其中包含 Web.Release.config hello 應用程式設定變更。</span><span class="sxs-lookup"><span data-stu-id="5d778-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="5d778-169">如果您想 tooattach hello 已發佈的 web 應用程式 Azure toohello 偵錯工具 （也就是您必須上傳 hello 已發佈的 web 應用程式中的程式碼的偵錯符號），您可以建立複本的 hello 偵錯組態 azure 偵錯，但與它自己的自訂 Web.config 轉換 （例如 Web.AzureDebug.config)，會使用從 Web.Release.config hello 應用程式設定。這可讓您 toomaintain 靜態設定 hello 不同環境下。</span><span class="sxs-lookup"><span data-stu-id="5d778-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="5d778-170">在 AD FS 管理中設定信賴憑證者信任</span><span class="sxs-lookup"><span data-stu-id="5d778-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="5d778-171">現在您需要 tooconfigure RP 中信任 AD FS 管理，才能使用的範例應用程式和實際使用 AD FS 驗證。</span><span class="sxs-lookup"><span data-stu-id="5d778-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="5d778-172">您必須設定兩個不同的 RP 信任 tooset 偵錯環境，一個已發行的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d778-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="5d778-173">請確定您重複下列步驟，這兩個環境的 hello。</span><span class="sxs-lookup"><span data-stu-id="5d778-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="5d778-174">在您的 AD FS 伺服器上的認證登入具有管理 rights tooAD FS。</span><span class="sxs-lookup"><span data-stu-id="5d778-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="5d778-175">開啟 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="5d778-175">Open AD FS Management.</span></span> <span data-ttu-id="5d778-176">以滑鼠右鍵按一下 [AD FS]\[信任的關係]\[信賴憑證者信任]，然後選取 [新增信賴憑證者信任]。</span><span class="sxs-lookup"><span data-stu-id="5d778-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="5d778-177">在 hello**選取資料來源**頁面上，選取**手動輸入 hello 信賴憑證者的合作對象相關資料**。</span><span class="sxs-lookup"><span data-stu-id="5d778-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="5d778-178">在 hello**指定顯示名稱**頁面上，輸入 hello 應用程式的顯示名稱，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5d778-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="5d778-179">在 hello**選擇通訊協定**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5d778-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="5d778-180">在 hello**設定憑證**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5d778-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5d778-181">由於您應該已在使用 HTTPS，因此可選擇是否使用加密的權杖。</span><span class="sxs-lookup"><span data-stu-id="5d778-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="5d778-182">如果您真的想 tooencrypt 語彙基元從這個頁面上的 AD FS，您也必須在程式碼中，將權杖解密的邏輯。</span><span class="sxs-lookup"><span data-stu-id="5d778-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="5d778-183">如需詳細資訊，請參閱 [手動設定 OWIN WS-同盟中介軟體和接受加密權杖](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d778-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="5d778-184">在移動到 hello 下一個步驟之前，您需要一段資訊從您的 Visual Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="5d778-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="5d778-185">在 hello 專案屬性中，記下 hello **SSL URL** hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d778-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="5d778-186">在 AD FS 管理，請在 hello**設定 URL**頁面 hello**新增信賴憑證者信任精靈**，選取**啟用 hello WS-同盟被動式通訊協定的支援**和輸入您記下 hello 上一個步驟中 hello Visual Studio 專案的 SSL URL。</span><span class="sxs-lookup"><span data-stu-id="5d778-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="5d778-187">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="5d778-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="5d778-188">URL 指定 toosend hello 用戶端，在驗證後的成功的位置。</span><span class="sxs-lookup"><span data-stu-id="5d778-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="5d778-189">Hello 偵錯環境中，它應該是<code>https://localhost:&lt;port&gt;/</code>。</span><span class="sxs-lookup"><span data-stu-id="5d778-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="5d778-190">Hello 已發佈的 web 應用程式中，它應該是 hello web 應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="5d778-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="5d778-191">在 hello**設定識別碼**頁面上，確認已列出 您的專案 SSL URL，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5d778-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="5d778-192">按一下**下一步**所有 hello 方式 toohello 結尾 hello 精靈預設選取項目。</span><span class="sxs-lookup"><span data-stu-id="5d778-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5d778-193">在 Visual Studio 專案 App_Start\Startup.Auth.cs，這個識別碼比對 hello 值<code>WsFederationAuthenticationOptions.Wtrealm</code>期間同盟驗證。</span><span class="sxs-lookup"><span data-stu-id="5d778-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="5d778-194">根據預設，hello 先前步驟中的 hello 應用程式的 URL 會加入做為 RP 識別項。</span><span class="sxs-lookup"><span data-stu-id="5d778-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="5d778-195">您現在已經完成設定 AD FS 中的 hello RP 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="5d778-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="5d778-196">接下來，您可以設定此應用程式 toosend hello 應用程式所需的宣告。</span><span class="sxs-lookup"><span data-stu-id="5d778-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="5d778-197">hello**編輯宣告規則**對話方塊預設會開啟為您在 hello hello 精靈結尾處，您可以立即啟動。</span><span class="sxs-lookup"><span data-stu-id="5d778-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="5d778-198">讓我們設定至少 hello 下列宣告 （使用括號括住的結構描述）：</span><span class="sxs-lookup"><span data-stu-id="5d778-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="5d778-199">ASP.NET toohydrate 所使用的名稱 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name)- `User.Identity.Name`。</span><span class="sxs-lookup"><span data-stu-id="5d778-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="5d778-200">使用者主要名稱 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn)-使用 toouniquely 識別 hello 組織中的使用者。</span><span class="sxs-lookup"><span data-stu-id="5d778-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="5d778-201">可以搭配群組成員資格與角色 (http://schemas.microsoft.com/ws/2008/06/identity/claims/role)-`[Authorize(Roles="role1, role2,...")]`裝飾 tooauthorize 控制器/動作。</span><span class="sxs-lookup"><span data-stu-id="5d778-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="5d778-202">事實上，這種方法可能不是 hello 進行角色授權的最高效能。</span><span class="sxs-lookup"><span data-stu-id="5d778-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="5d778-203">如果您的 AD 使用者所屬的安全性群組 toohundreds，它們就會變成數百個 hello SAML 權杖中的角色宣告。</span><span class="sxs-lookup"><span data-stu-id="5d778-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="5d778-204">另一個方法是的 toosend 單一角色宣告有條件地根據特定群組中的 hello 使用者的成員資格。</span><span class="sxs-lookup"><span data-stu-id="5d778-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="5d778-205">不過，我們會在本教學課程中簡化該作業。</span><span class="sxs-lookup"><span data-stu-id="5d778-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="5d778-206">名稱識別碼 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - 可用於防偽驗證。</span><span class="sxs-lookup"><span data-stu-id="5d778-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="5d778-207">如需有關如何 toomake 它搭配防偽驗證的詳細資訊，請參閱 hello**新增的業務功能**區段[建立業務的 Azure 應用程式與 Azure Active Directory 驗證](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="5d778-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5d778-208">hello 宣告類型與您需要 tooconfigure，您的應用程式由應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="5d778-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="5d778-209">Hello 清單中的 Azure Active Directory 應用程式 （亦即 RP 的信任） 支援的宣告，例如，請參閱[支援權杖和宣告類型](http://msdn.microsoft.com/library/azure/dn195587.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d778-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="5d778-210">在 hello 編輯宣告規則 對話方塊中，按一下 **加入規則**。</span><span class="sxs-lookup"><span data-stu-id="5d778-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="5d778-211">設定名稱、 UPN 和角色宣告的 hello hello 螢幕擷取畫面所示，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="5d778-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="5d778-212">接下來，您建立暫時性的名稱識別碼宣告中使用 hello 步驟示範[SAML 判斷提示中的名稱識別項](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d778-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="5d778-213">再按一下 [新增規則]  。</span><span class="sxs-lookup"><span data-stu-id="5d778-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="5d778-214">選取 [使用自訂規則傳送宣告] 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5d778-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="5d778-215">貼上 hello 下列規則語言到 hello**自訂規則** 方塊中，名稱 hello 規則**每個工作階段識別碼**按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="5d778-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="5d778-216">您的自訂規則看起來應該類似下列螢幕擷取畫面︰</span><span class="sxs-lookup"><span data-stu-id="5d778-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="5d778-217">再按一下 [新增規則]  。</span><span class="sxs-lookup"><span data-stu-id="5d778-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="5d778-218">選取 [傳輸傳入宣告] 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="5d778-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="5d778-219">（使用您建立 hello 自訂規則中的 hello 宣告型別） 的 hello 螢幕擷取畫面所示設定 hello 規則，按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="5d778-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="5d778-220">Hello 暫時性名稱識別碼宣告 hello 步驟的詳細資訊，請參閱[SAML 判斷提示中的名稱識別項](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5d778-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="5d778-221">按一下**套用**在 hello**編輯宣告規則**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5d778-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="5d778-222">它現在應該看起來像下列螢幕擷取畫面的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d778-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="5d778-223">同樣地，請確定為偵錯環境和已發行的 Web 應用程式重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5d778-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="5d778-224">測試應用程式的同盟驗證</span><span class="sxs-lookup"><span data-stu-id="5d778-224">Test federated authentication for your application</span></span>
<span data-ttu-id="5d778-225">您已準備好 tootest 針對 AD FS 的應用程式的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="5d778-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="5d778-226">在我 AD FS 實驗室環境中，我有所屬 tooa 測試群組在 Active Directory (AD) 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5d778-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="5d778-227">在 hello 偵錯工具，現在您只需要 toodo tootest 驗證是型別`F5`。</span><span class="sxs-lookup"><span data-stu-id="5d778-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="5d778-228">如果您想 tootest 驗證 hello 已發佈的 web 應用程式中，瀏覽 toohello URL。</span><span class="sxs-lookup"><span data-stu-id="5d778-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="5d778-229">Hello web 應用程式載入之後，請按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="5d778-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="5d778-230">您現在應該取得登入對話方塊或 hello 登入頁面由 AD FS 中，根據選擇的 AD FS 的 hello 驗證方法。</span><span class="sxs-lookup"><span data-stu-id="5d778-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="5d778-231">以下是我在 Internet Explorer 11 中看到的畫面。</span><span class="sxs-lookup"><span data-stu-id="5d778-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="5d778-232">一旦您登入的 hello AD FS 部署的 hello AD 網域中的使用者，您現在應該會看到一次與 hello 首頁**Hello， <User Name>！**</span><span class="sxs-lookup"><span data-stu-id="5d778-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="5d778-233">hello 角。</span><span class="sxs-lookup"><span data-stu-id="5d778-233">in hello corner.</span></span> <span data-ttu-id="5d778-234">以下是我看到的內容。</span><span class="sxs-lookup"><span data-stu-id="5d778-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="5d778-235">目前為止，您已經成功地 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="5d778-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="5d778-236">您的應用程式已順利達到 AD FS，並且在 hello AD FS 資料庫中找到相符的 RP 識別項</span><span class="sxs-lookup"><span data-stu-id="5d778-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="5d778-237">AD FS 已成功驗證的 AD 使用者和重新導向回 toohello 應用程式的首頁</span><span class="sxs-lookup"><span data-stu-id="5d778-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="5d778-238">做為已成功傳送的嗨名稱的 AD FS 的宣告 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour 應用程式中，由該 hello 使用者 hello 事實 hello 角會顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="5d778-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="5d778-239">如果遺失 hello 名稱宣告，您應該會看到**Hello，！**。</span><span class="sxs-lookup"><span data-stu-id="5d778-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="5d778-240">如果您看一下 _layout.cshtml\_LoginPartial.cshtml，您會發現它會使用`User.Identity.Name`toodisplay hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="5d778-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="5d778-241">如前所述，如果 hello 名稱宣告 hello 驗證的使用者可在 hello SAML 權杖中，ASP.NET hydrates 與其這個屬性。</span><span class="sxs-lookup"><span data-stu-id="5d778-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="5d778-242">所有 hello 的 toosee 宣告傳送由 AD FS 在 hello，將中斷點放在 Controllers\HomeController.cs，索引動作方法。</span><span class="sxs-lookup"><span data-stu-id="5d778-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="5d778-243">Hello 使用者經過驗證之後，檢查 hello`System.Security.Claims.Current.Claims`集合。</span><span class="sxs-lookup"><span data-stu-id="5d778-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="5d778-244">授權使用者使用特定的控制器或動作</span><span class="sxs-lookup"><span data-stu-id="5d778-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="5d778-245">因為您要加入群組成員資格做為角色宣告您 RP 信任設定，您現在可以使用它們直接在 hello`[Authorize(Roles="...")]`裝飾控制器和動作。</span><span class="sxs-lookup"><span data-stu-id="5d778-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="5d778-246">在 hello 建立讀取更新與刪除 (CRUD) 模式的特定業務應用程式，您可以授權特定角色 tooaccess 每個動作。</span><span class="sxs-lookup"><span data-stu-id="5d778-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="5d778-247">現在，您將只試用 hello 現有主控制器上的這項功能。</span><span class="sxs-lookup"><span data-stu-id="5d778-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="5d778-248">開啟 Controllers\HomeController.cs。</span><span class="sxs-lookup"><span data-stu-id="5d778-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="5d778-249">裝飾 hello`About`和`Contact`動作方法類似 toohello 下列程式碼，請使用您已驗證的使用者具有的安全性群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="5d778-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="5d778-250">因為我加入**測試使用者**太**測試群組**我將我的 AD FS 實驗室環境中使用測試群組 tootest 授權上`About`。</span><span class="sxs-lookup"><span data-stu-id="5d778-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="5d778-251">如`Contact`，測試 hello 負的大小寫**Domain Admins**，toowhich**測試使用者**不屬於。</span><span class="sxs-lookup"><span data-stu-id="5d778-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="5d778-252">輸入啟動 hello 偵錯工具`F5`並登入，然後按一下 **有關**。</span><span class="sxs-lookup"><span data-stu-id="5d778-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="5d778-253">您應該立即檢視 hello`~/About/Index`頁面成功，如果您已驗證的使用者已獲得授權，該動作。</span><span class="sxs-lookup"><span data-stu-id="5d778-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="5d778-254">現在按一下**連絡人**，其在這個案例中應該不會授權**測試使用者**hello 動作。</span><span class="sxs-lookup"><span data-stu-id="5d778-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="5d778-255">不過，hello 瀏覽器會重新導向的 tooAD FS，最後會顯示此訊息：</span><span class="sxs-lookup"><span data-stu-id="5d778-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="5d778-256">如果您要調查 hello AD FS 伺服器上的事件檢視器中此錯誤，您會看到這個例外狀況訊息：</span><span class="sxs-lookup"><span data-stu-id="5d778-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="5d778-257">hello 這個錯誤的原因是根據預設，MVC 會傳回 401 未授權時未獲授權的使用者角色。</span><span class="sxs-lookup"><span data-stu-id="5d778-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="5d778-258">這會觸發重新驗證要求 tooyour 身分識別提供者 (AD FS)。</span><span class="sxs-lookup"><span data-stu-id="5d778-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="5d778-259">AD FS hello 使用者已經過驗證，因為傳回 toohello 相同頁面上，然後發出另一個 401，建立重新導向迴圈。</span><span class="sxs-lookup"><span data-stu-id="5d778-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="5d778-260">您將會覆寫 AuthorizeAttribute 的`HandleUnauthorizedRequest`具有簡單的邏輯 tooshow 方法而不是持續的 hello 重新導向迴圈有意義的項目。</span><span class="sxs-lookup"><span data-stu-id="5d778-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="5d778-261">呼叫 AuthorizeAttribute.cs，並貼上下列程式碼中的 hello hello 專案中建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="5d778-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="5d778-262">hello 覆寫程式碼傳送 HTTP 403 （禁止） 而不是 HTTP 401 （未經授權） 中已驗證，但未經授權的情況。</span><span class="sxs-lookup"><span data-stu-id="5d778-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="5d778-263">Hello 偵錯工具使用，然後再次執行`F5`。</span><span class="sxs-lookup"><span data-stu-id="5d778-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="5d778-264">現在按一下 [連絡人]  會顯示更具參考性的 (雖然不討喜) 錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="5d778-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="5d778-265">同樣地，發行 hello 應用程式 tooAzure App Service Web 應用程式，並測試 hello hello 即時應用程式行為。</span><span class="sxs-lookup"><span data-stu-id="5d778-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="5d778-266">Tooon 內部部署資料連接</span><span class="sxs-lookup"><span data-stu-id="5d778-266">Connect tooon-premises data</span></span>
<span data-ttu-id="5d778-267">您會想 tooimplement 特定業務應用程式與 AD FS，而不是 Azure Active Directory 的原因，是保持組織資料外部部署的相容性問題。</span><span class="sxs-lookup"><span data-stu-id="5d778-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="5d778-268">這也表示您在 Azure 中的 web 應用程式必須存取內部部署資料庫，因為不允許 toouse [SQL Database](/services/sql-database/)做為您的 web 應用程式的 hello 資料層。</span><span class="sxs-lookup"><span data-stu-id="5d778-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="5d778-269">Azure App Service Web Apps 可透過兩種方式支援存取內部部署資料庫：[混合式連線](../biztalk-services/integration-hybrid-connection-overview.md)和[虛擬網路](web-sites-integrate-with-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="5d778-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="5d778-270">如需詳細資訊，請參閱 [使用 VNET 整合和混合式連線搭配 Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/)。</span><span class="sxs-lookup"><span data-stu-id="5d778-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="5d778-271">進一步資源</span><span class="sxs-lookup"><span data-stu-id="5d778-271">Further resources</span></span>
* [<span data-ttu-id="5d778-272">在 Azure 應用程式中使用內部部署 Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="5d778-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="5d778-273">使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="5d778-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="5d778-274">使用 Visual Studio 2013 中的 hello 與 ASP.NET 在內部部署組織的驗證選項 (ADFS)</span><span class="sxs-lookup"><span data-stu-id="5d778-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="5d778-275">移轉 VS2013 Web 專案從 WIF tooKatana</span><span class="sxs-lookup"><span data-stu-id="5d778-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="5d778-276">Active Directory Federation Services 概觀</span><span class="sxs-lookup"><span data-stu-id="5d778-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="5d778-277">WS-同盟 1.1 規格</span><span class="sxs-lookup"><span data-stu-id="5d778-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

