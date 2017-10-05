---
title: "使用 AD FS 驗證建立企業營運 Azure 應用程式 | Microsoft Docs"
description: "了解如何在 Azure App Service 中建立使用內部部署 STS 進行驗證的企業營運應用程式。 本教學課程將 AD FS 選為內部部署 STS。"
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
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="fea9a-104">使用 AD FS 驗證建立企業營運 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="fea9a-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="fea9a-105">本文說明如何使用內部部署 [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) 做為識別提供者，在 [Azure App Service](../app-service/app-service-value-prop-what-is.md) 中建立 ASP.NET MVC 企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="fea9a-105">This article shows you how to create an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as the identity provider.</span></span> <span data-ttu-id="fea9a-106">當您想要在 Azure App Service 中建立企業營運應用程式，但您的組織需要在內部儲存目錄資料時，此案例可以發揮作用。</span><span class="sxs-lookup"><span data-stu-id="fea9a-106">This scenario can work when you want to create line-of-business applications in Azure App Service but your organization requires directory data to be stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="fea9a-107">如需 Azure App Service 不同的企業驗證和授權選項的概觀，請參閱 [在 Azure 應用程式中使用內部部署 Active Directory 進行驗證](web-sites-authentication-authorization.md)。</span><span class="sxs-lookup"><span data-stu-id="fea9a-107">For an overview of the different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="fea9a-108">將建置的項目</span><span class="sxs-lookup"><span data-stu-id="fea9a-108">What you will build</span></span>
<span data-ttu-id="fea9a-109">您將在 Azure 應用程式服務 Web 應用程式中建置具備下列功能的基本 ASP.NET 應用程式：</span><span class="sxs-lookup"><span data-stu-id="fea9a-109">You will build a basic ASP.NET application in Azure App Service Web Apps with the following features:</span></span>

* <span data-ttu-id="fea9a-110">根據 AD FS 驗證使用者</span><span class="sxs-lookup"><span data-stu-id="fea9a-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="fea9a-111">使用 `[Authorize]` 來授權使用者使用不同的動作</span><span class="sxs-lookup"><span data-stu-id="fea9a-111">Uses `[Authorize]` to authorize users for different actions</span></span>
* <span data-ttu-id="fea9a-112">在 Visual Studio 中偵錯和發行至 Azure 應用程式服務 Web 應用程式的靜態設定 (設定一次，隨時偵錯和發行)</span><span class="sxs-lookup"><span data-stu-id="fea9a-112">Static configuration for both debugging in Visual Studio and publishing to App Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="fea9a-113">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="fea9a-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="fea9a-114">您需要下列項目完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="fea9a-114">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="fea9a-115">內部部署 AD FS 部署 (如需本教學課程所使用之測試實驗室的端對端逐步解說，請參閱 [測試實驗室：搭配 Azure VM 中 AD FS 的獨立 STS (僅適用於測試)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="fea9a-115">An on-premises AD FS deployment (for an end-to-end walkthrough of the test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="fea9a-116">在 AD FS 管理中建立信賴憑證者信任的權限</span><span class="sxs-lookup"><span data-stu-id="fea9a-116">Permissions to create relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="fea9a-117">Visual Studio 2013 Update 4 或更新版本</span><span class="sxs-lookup"><span data-stu-id="fea9a-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="fea9a-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) 或更新版本</span><span class="sxs-lookup"><span data-stu-id="fea9a-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="fea9a-119">使用特定業務範本的範例應用程式</span><span class="sxs-lookup"><span data-stu-id="fea9a-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="fea9a-120">本教學課程中的範例應用程式 [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet)是由 Azure Active Directory 團隊所建立。</span><span class="sxs-lookup"><span data-stu-id="fea9a-120">The sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by the Azure Active Directory team.</span></span> <span data-ttu-id="fea9a-121">由於 AD FS 支援 WS-同盟，因此您可將其用作範本，輕鬆地建立企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="fea9a-121">Since AD FS supports WS-Federation, you can use it as a template to create line-of-business applications with ease.</span></span> <span data-ttu-id="fea9a-122">它有下列功能：</span><span class="sxs-lookup"><span data-stu-id="fea9a-122">It has the following features:</span></span>

* <span data-ttu-id="fea9a-123">使用 [WS-同盟](http://msdn.microsoft.com/library/bb498017.aspx) 驗證內部部署 AD FS 部署</span><span class="sxs-lookup"><span data-stu-id="fea9a-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) to authenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="fea9a-124">登入和登出功能</span><span class="sxs-lookup"><span data-stu-id="fea9a-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="fea9a-125">使用 ASP.NET 的明日之星 [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (而不是 Windows Identity Foundation) 進行驗證和授權的設定，會比使用 WIF 容易得多</span><span class="sxs-lookup"><span data-stu-id="fea9a-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is the future of ASP.NET and much simpler to set up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a><span data-ttu-id="fea9a-126">設定範例應用程式</span><span class="sxs-lookup"><span data-stu-id="fea9a-126">Set up the sample application</span></span>
1. <span data-ttu-id="fea9a-127">將 [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) 上的範例解決方案複製或下載至您的本機目錄。</span><span class="sxs-lookup"><span data-stu-id="fea9a-127">Clone or download the sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) to your local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fea9a-128">[README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) 中的指示會說明如何使用 Azure Active Directory 設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="fea9a-128">The instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how to set up the application with Azure Active Directory.</span></span> <span data-ttu-id="fea9a-129">但在本教學課程中，您是使用 AD FS 進行設定，因此請改為遵循此處的步驟。</span><span class="sxs-lookup"><span data-stu-id="fea9a-129">But in this tutorial, you set it up with AD FS, so follow the steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="fea9a-130">開啟解決方案，然後在 [方案總管] 中開啟 Controllers\AccountController.cs。</span><span class="sxs-lookup"><span data-stu-id="fea9a-130">Open the solution, and then open Controllers\AccountController.cs in the **Solution Explorer**.</span></span>
   
   <span data-ttu-id="fea9a-131">您會看到程式碼只是發出驗證挑戰，以使用 WS-同盟來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="fea9a-131">You will see that the code simply issues an authentication challenge to authenticate the user using WS-Federation.</span></span> <span data-ttu-id="fea9a-132">所有驗證都是在 App_Start\Startup.Auth.cs 中設定。</span><span class="sxs-lookup"><span data-stu-id="fea9a-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="fea9a-133">開啟 App_Start\Startup.Auth.cs。</span><span class="sxs-lookup"><span data-stu-id="fea9a-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="fea9a-134">在 `ConfigureAuth` 方法中，請注意下列重點：</span><span class="sxs-lookup"><span data-stu-id="fea9a-134">In the `ConfigureAuth` method, note the line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="fea9a-135">在 OWIN 世界中，此程式碼片段實際上就是您需要設定 WS-同盟驗證的最低限度。</span><span class="sxs-lookup"><span data-stu-id="fea9a-135">In the OWIN world, this snippet is really the bare minimum you need to configure WS-Federation authentication.</span></span> <span data-ttu-id="fea9a-136">它比 WIF 簡單且簡潔得多，其中 Web.config 會在各處插入 XML。</span><span class="sxs-lookup"><span data-stu-id="fea9a-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over the place.</span></span> <span data-ttu-id="fea9a-137">您需要的唯一資訊是信賴憑證者的 (RP) 識別碼和 AD FS 服務的中繼資料檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="fea9a-137">The only information you need is the relying party's (RP) identifier and the URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="fea9a-138">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="fea9a-138">Here's an example:</span></span>
   
   * <span data-ttu-id="fea9a-139">RP 識別碼： `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="fea9a-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="fea9a-140">中繼資料位址：`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="fea9a-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="fea9a-141">在 App_Start\Startup.Auth.cs 中變更下列靜態字串定義：</span><span class="sxs-lookup"><span data-stu-id="fea9a-141">In App_Start\Startup.Auth.cs, change the following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="fea9a-142">現在，在 Web.config 中進行對應的變更。</span><span class="sxs-lookup"><span data-stu-id="fea9a-142">Now, make the corresponding changes in Web.config.</span></span> <span data-ttu-id="fea9a-143">開啟 Web.config 並修改下列應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="fea9a-143">Open the Web.config and modify the following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="fea9a-144">根據您的對應環境填寫索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="fea9a-144">Fill in the key values based on your respective environment.</span></span>
6. <span data-ttu-id="fea9a-145">建置應用程式，確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="fea9a-145">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="fea9a-146">就這麼簡單。</span><span class="sxs-lookup"><span data-stu-id="fea9a-146">That's it.</span></span> <span data-ttu-id="fea9a-147">範例應用程式現在已準備好要使用 AD FS。</span><span class="sxs-lookup"><span data-stu-id="fea9a-147">Now the sample application is ready to work with AD FS.</span></span> <span data-ttu-id="fea9a-148">您稍後仍然必須在 AD FS 中，使用此應用程式設定 RP 信任。</span><span class="sxs-lookup"><span data-stu-id="fea9a-148">You still need to configure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a><span data-ttu-id="fea9a-149">將範例應用程式部署到 Azure 應用程式服務 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="fea9a-149">Deploy the sample application to Azure App Service Web Apps</span></span>
<span data-ttu-id="fea9a-150">在這裡，您會將應用程式發佈到 App Service Web Apps 中的 Web 應用程式，同時保留偵錯環境。</span><span class="sxs-lookup"><span data-stu-id="fea9a-150">Here, you publish the application to a web app in App Service Web Apps while preserving the debug environment.</span></span> <span data-ttu-id="fea9a-151">請注意，您即將發行應用程式，但應用程式沒有 AD FS 授予的 RP 信任，所以還是無法執行驗證。</span><span class="sxs-lookup"><span data-stu-id="fea9a-151">Note that you're going to publish the application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="fea9a-152">不過，如果您現在這樣做，您可以擁有 Web 應用程式 URL，以供稍後用來設定 RP 信任。</span><span class="sxs-lookup"><span data-stu-id="fea9a-152">However, if you do it now you can have the web app URL that you can use to configure the RP trust later.</span></span>

1. <span data-ttu-id="fea9a-153">以滑鼠右鍵按一下專案，然後選取 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-153">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="fea9a-154">選取 [ **Microsoft Azure App Service**]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-154">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="fea9a-155">如果您還沒有登入 Azure，請按一下 [登入]  並使用您 Azure 訂用帳戶的 Microsoft 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="fea9a-155">If you haven't signed in to Azure, click **Sign In** and use the Microsoft account for your Azure subscription to sign in.</span></span>
4. <span data-ttu-id="fea9a-156">登入之後，按一下 [新增]  來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fea9a-156">Once signed in, click **New** to create a web app.</span></span>
5. <span data-ttu-id="fea9a-157">填寫所有必要欄位。</span><span class="sxs-lookup"><span data-stu-id="fea9a-157">Fill in all required fields.</span></span> <span data-ttu-id="fea9a-158">您稍後即將連線到內部部署資料，因此請勿建立此 Web 應用程式的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fea9a-158">You are going to connect to on-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="fea9a-159">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-159">Click **Create**.</span></span> <span data-ttu-id="fea9a-160">一旦建立 Web 應用程式後，會開啟 [發行 Web] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="fea9a-160">Once the web app is created, the Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="fea9a-161">在 [目的地 URL] 中，將 **http** 變更為 **https**。</span><span class="sxs-lookup"><span data-stu-id="fea9a-161">In **Destination URL**, change **http** to **https**.</span></span> <span data-ttu-id="fea9a-162">將完整的 URL 複製到文字編輯器以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="fea9a-162">Copy the entire URL to a text editor for later use.</span></span> <span data-ttu-id="fea9a-163">然後按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-163">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="fea9a-164">在 Visual Studio 中，開啟專案中的 **Web.Release.config** 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-164">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="fea9a-165">將下列 XML 插入 `<configuration>` 標記，並使用發佈 Web 應用程式的 URL 取代索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="fea9a-165">Insert the following XML into the `<configuration>` tag, and replace the key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="fea9a-166">當您完成時，您會在專案中設定兩個 RP 識別碼，一個適用於 Visual Studio 中的偵錯環境，另一個適用於 Azure 中的已發行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fea9a-166">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for the published web app in Azure.</span></span> <span data-ttu-id="fea9a-167">您會在 AD FS 中，為兩種環境的每種環境設定一個 RP 信任。</span><span class="sxs-lookup"><span data-stu-id="fea9a-167">You will set up an RP trust for each of the two environments in AD FS.</span></span> <span data-ttu-id="fea9a-168">在偵錯期間，Web.config 中的應用程式設定可用來讓 **偵錯** 組態與 AD FS 搭配運作。</span><span class="sxs-lookup"><span data-stu-id="fea9a-168">During debugging, the app settings in Web.config are used to make your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="fea9a-169">在發佈後 (預設會發佈 **版本** 組態)，會上傳轉換的 Web.config，其中包含 Web.Release.config 的應用程式設定變更。</span><span class="sxs-lookup"><span data-stu-id="fea9a-169">When it's published (by default, the **Release** configuration is published), a transformed Web.config is uploaded that incorporates the app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="fea9a-170">如果您想要將在 Azure 發行的 Web 應用程式附加到偵錯工具 (也就是您必須上傳已發行 Web 應用程式中的程式碼偵錯符號)，您可以建立偵錯組態的複本進行 Azure 偵錯，但使用其自訂的 Web.config 轉換 (例如 Web.AzureDebug.config)，從 Web.Release.config 使用應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="fea9a-170">If you want to attach the published web app in Azure to the debugger (i.e. you must upload debug symbols of your code in the published web app), you can create a clone of the Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses the app settings from Web.Release.config.</span></span> <span data-ttu-id="fea9a-171">這可讓您跨不同的環境維護靜態組態。</span><span class="sxs-lookup"><span data-stu-id="fea9a-171">This allows you to maintain a static configuration across the different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="fea9a-172">在 AD FS 管理中設定信賴憑證者信任</span><span class="sxs-lookup"><span data-stu-id="fea9a-172">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="fea9a-173">現在您需要先在 AD FS 管理中設定 RP 信任，然後您才可以使用範例應用程式並透過 AD FS 實際驗證。</span><span class="sxs-lookup"><span data-stu-id="fea9a-173">Now you need to configure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="fea9a-174">您必須設定兩個不同的 RP 信任，一個用於偵錯環境，另一個用於您發行的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fea9a-174">You will need to set up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="fea9a-175">請確定為您的兩個環境重複下列步驟。</span><span class="sxs-lookup"><span data-stu-id="fea9a-175">Make sure that you repeat the following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="fea9a-176">在 AD FS 伺服器上，使用具有 AD FS 之管理權限的認證登入。</span><span class="sxs-lookup"><span data-stu-id="fea9a-176">On your AD FS server, log in with credentials that have management rights to AD FS.</span></span>
2. <span data-ttu-id="fea9a-177">開啟 [AD FS 管理]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-177">Open AD FS Management.</span></span> <span data-ttu-id="fea9a-178">以滑鼠右鍵按一下 [AD FS]\[信任的關係]\[信賴憑證者信任]，然後選取 [新增信賴憑證者信任]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-178">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="fea9a-179">在 [選取資料來源] 頁面上，選取 [手動輸入信賴憑證者的相關資料]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-179">In the **Select Data Source** page, select **Enter data about the relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="fea9a-180">在 [指定顯示名稱] 頁面上，輸入應用程式的顯示名稱，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-180">In the **Specify Display Name** page, type a display name for the application and click **Next**.</span></span>
5. <span data-ttu-id="fea9a-181">在 [選擇通訊協定] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-181">In the **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="fea9a-182">在 [設定憑證] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-182">In the **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fea9a-183">由於您應該已在使用 HTTPS，因此可選擇是否使用加密的權杖。</span><span class="sxs-lookup"><span data-stu-id="fea9a-183">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="fea9a-184">如果您真的想要在這個頁面上加密 AD FS 的權杖，您也必須在程式碼中新增權杖解密的邏輯。</span><span class="sxs-lookup"><span data-stu-id="fea9a-184">If you really want to encrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="fea9a-185">如需詳細資訊，請參閱 [手動設定 OWIN WS-同盟中介軟體和接受加密權杖](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fea9a-185">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="fea9a-186">前進至下一個步驟之前，您需從 Visual Studio 專案準備一段資訊。</span><span class="sxs-lookup"><span data-stu-id="fea9a-186">Before you move onto the next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="fea9a-187">在專案屬性中，記下應用程式的 [SSL URL]  。</span><span class="sxs-lookup"><span data-stu-id="fea9a-187">In the project properties, note the **SSL URL** of the application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="fea9a-188">返回 [AD FS 管理]，在 [新增信賴憑證者信任精靈] 的 [設定 URL] 頁面中，選取 [啟用 WS-同盟被動式通訊協定的支援] 並輸入您在上一個步驟記下 Visual Studio 專案的 SSL URL。</span><span class="sxs-lookup"><span data-stu-id="fea9a-188">Back in AD FS Management, in the **Configure URL** page of the **Add Relying Party Trust Wizard**, select **Enable support for the WS-Federation Passive protocol** and type in the SSL URL of your Visual Studio project that you noted in the previous step.</span></span> <span data-ttu-id="fea9a-189">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-189">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="fea9a-190">驗證成功後，URL 會指定將用戶端傳送到的位置。</span><span class="sxs-lookup"><span data-stu-id="fea9a-190">URL specifies where to send the client after authentication succeeds.</span></span> <span data-ttu-id="fea9a-191">若為偵錯環境，其應該是 <code>https://localhost:&lt;port&gt;/</code>。</span><span class="sxs-lookup"><span data-stu-id="fea9a-191">For the debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="fea9a-192">已發行的 Web 應用程式中，它應該是 Web 應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="fea9a-192">For the published web app, it should be the web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="fea9a-193">在 [設定識別碼] 頁面上，確認已列出專案 SSL URL，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-193">In the **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="fea9a-194">按 [下一步]  並選取預設選取項目，一直到精靈結束。</span><span class="sxs-lookup"><span data-stu-id="fea9a-194">Click **Next** all the way to the end of the wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fea9a-195">在 Visual Studio 專案的 App_Start\Startup.Auth.cs 中，此識別碼會在同盟驗證期間比對 <code>WsFederationAuthenticationOptions.Wtrealm</code> 的值。</span><span class="sxs-lookup"><span data-stu-id="fea9a-195">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against the value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="fea9a-196">根據預設，會加入上一個步驟的應用程式 URL 做為 RP 識別碼。</span><span class="sxs-lookup"><span data-stu-id="fea9a-196">By default, the application's URL from the previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="fea9a-197">您現在已經在 AD FS 中完成專案的 RP 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="fea9a-197">You have now finished configuring the RP application for your project in AD FS.</span></span> <span data-ttu-id="fea9a-198">接下來，您會設定此應用程式來傳送應用程式所需的宣告。</span><span class="sxs-lookup"><span data-stu-id="fea9a-198">Next, you configure this application to send the claims needed by your application.</span></span> <span data-ttu-id="fea9a-199">[編輯宣告規則]  對話方塊預設會在精靈結束時開啟，以便讓您立即啟動。</span><span class="sxs-lookup"><span data-stu-id="fea9a-199">The **Edit Claim Rules** dialog is opened by default for you at the end of the wizard so you can start immediately.</span></span> <span data-ttu-id="fea9a-200">讓我們至少設定下列宣告 (使用括號括住結構描述)：</span><span class="sxs-lookup"><span data-stu-id="fea9a-200">Let's configure at least the following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="fea9a-201">名稱 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - 用於 ASP.NET 以序列化 `User.Identity.Name`。</span><span class="sxs-lookup"><span data-stu-id="fea9a-201">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET to hydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="fea9a-202">使用者主要名稱 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - 用來唯一識別組織中的使用者。</span><span class="sxs-lookup"><span data-stu-id="fea9a-202">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used to uniquely identify users in the organization.</span></span>
    * <span data-ttu-id="fea9a-203">群組為角色的成員資格 (http://schemas.microsoft.com/ws/2008/06/identity/claims/role)- 可以搭配使用 `[Authorize(Roles="role1, role2,...")]` 裝飾來授權控制站/動作。</span><span class="sxs-lookup"><span data-stu-id="fea9a-203">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration to authorize controllers/actions.</span></span> <span data-ttu-id="fea9a-204">事實上，這可能不是角色授權的最有效方法。</span><span class="sxs-lookup"><span data-stu-id="fea9a-204">In reality, this approach may not be the most performant for role authorization.</span></span> <span data-ttu-id="fea9a-205">如果 AD 使用者屬於數百個安全性群組，他們會變成 SAML 權杖中的數百個角色宣告。</span><span class="sxs-lookup"><span data-stu-id="fea9a-205">If your AD users belong to hundreds of security groups, they become hundreds of role claims in the SAML token.</span></span> <span data-ttu-id="fea9a-206">替代方式是根據特定群組中的使用者成員資格，有條件地傳送單一角色宣告。</span><span class="sxs-lookup"><span data-stu-id="fea9a-206">An alternative approach is to send a single role claim conditionally depending on the user's membership in a particular group.</span></span> <span data-ttu-id="fea9a-207">不過，我們會在本教學課程中簡化該作業。</span><span class="sxs-lookup"><span data-stu-id="fea9a-207">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="fea9a-208">名稱識別碼 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - 可用於防偽驗證。</span><span class="sxs-lookup"><span data-stu-id="fea9a-208">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="fea9a-209">如需有關如何讓其使用防偽驗證的詳細資訊，請參閱 **使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式** 的 [新增企業營運功能](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud)一節。</span><span class="sxs-lookup"><span data-stu-id="fea9a-209">For more information on how to make it work with anti-forgery validation, see the **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fea9a-210">您必須為應用程式設定的宣告類型取決於您的應用程式需求。</span><span class="sxs-lookup"><span data-stu-id="fea9a-210">The claim types you need to configure for your application is determined by your application's needs.</span></span> <span data-ttu-id="fea9a-211">例如，如需 Azure Active Directory 應用程式 (也就是 RP 信任) 所支援的宣告清單，請參閱 [支援的權杖和宣告類型](http://msdn.microsoft.com/library/azure/dn195587.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fea9a-211">For the list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="fea9a-212">在 [編輯宣告規則] 對話方塊中，按一下 [新增規則] 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-212">In the Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="fea9a-213">如螢幕擷取畫面所示設定名稱、UPN 和角色宣告，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-213">Configure the name, UPN, and role claims as shown in the screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="fea9a-214">接下來，您會使用 [SAML 判斷提示中的名稱識別碼](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)中示範的步驟來建立暫時性的名稱識別碼宣告。</span><span class="sxs-lookup"><span data-stu-id="fea9a-214">Next, you create a transient name ID claim using the steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="fea9a-215">再按一下 [新增規則]  。</span><span class="sxs-lookup"><span data-stu-id="fea9a-215">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="fea9a-216">選取 [使用自訂規則傳送宣告] 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-216">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="fea9a-217">將下列規則語言貼到 [自訂規則] 方塊，將規則命名為 [每個工作階段識別碼] 並按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-217">Paste the following rule language into the **Custom rule** box, name the rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="fea9a-218">您的自訂規則看起來應該類似下列螢幕擷取畫面︰</span><span class="sxs-lookup"><span data-stu-id="fea9a-218">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="fea9a-219">再按一下 [新增規則]  。</span><span class="sxs-lookup"><span data-stu-id="fea9a-219">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="fea9a-220">選取 [傳輸傳入宣告] 並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-220">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="fea9a-221">如螢幕擷取畫面所示設定規則 (使用您在自訂規則中建立的宣告類型)，按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-221">Configure the rule as shown in the screenshot (using the claim type you created in the custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="fea9a-222">如需暫時性名稱識別碼宣告之步驟的詳細資訊，請參閱 [SAML 判斷提示中的名稱識別碼](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fea9a-222">For detailed information on the steps for the transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="fea9a-223">按一下 [編輯宣告規則] 對話方塊中的 [套用]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-223">Click **Apply** in the **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="fea9a-224">它現在看起來應該類似下列螢幕擷取畫面︰</span><span class="sxs-lookup"><span data-stu-id="fea9a-224">It should now look like the following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="fea9a-225">同樣地，請確定為偵錯環境和已發行的 Web 應用程式重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="fea9a-225">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="fea9a-226">測試應用程式的同盟驗證</span><span class="sxs-lookup"><span data-stu-id="fea9a-226">Test federated authentication for your application</span></span>
<span data-ttu-id="fea9a-227">您已準備好針對 AD FS 測試應用程式的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="fea9a-227">You are ready to test your application's authentication logic against AD FS.</span></span> <span data-ttu-id="fea9a-228">在我的 AD FS 實驗室環境中，我有一名測試使用者屬於 Active Directory (AD) 中的測試群組。</span><span class="sxs-lookup"><span data-stu-id="fea9a-228">In my AD FS lab environment, I have a test user that belongs to a test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="fea9a-229">若要在偵錯工具中測試驗證，您現在只需要按下 `F5`。</span><span class="sxs-lookup"><span data-stu-id="fea9a-229">To test authentication in the debugger, all you need to do now is type `F5`.</span></span> <span data-ttu-id="fea9a-230">如果您想要在已發行的 Web 應用程式中測試驗證，請巡覽至 URL。</span><span class="sxs-lookup"><span data-stu-id="fea9a-230">If you want to test authentication in the published web app, navigate to the URL.</span></span>

<span data-ttu-id="fea9a-231">載入 Web 應用程式之後，請按一下 [登入] 。</span><span class="sxs-lookup"><span data-stu-id="fea9a-231">After the web application loads, click **Sign In**.</span></span> <span data-ttu-id="fea9a-232">您現在應取得登入對話方塊，或 AD FS 所提供的登入頁面，視 AD FS 所選擇的驗證方法而定。</span><span class="sxs-lookup"><span data-stu-id="fea9a-232">You should now get either a login dialog or the login page served by AD FS, depending on the authentication method chosen by AD FS.</span></span> <span data-ttu-id="fea9a-233">以下是我在 Internet Explorer 11 中看到的畫面。</span><span class="sxs-lookup"><span data-stu-id="fea9a-233">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="fea9a-234">一旦您以 AD FS 部署的 AD 網域中使用者身分登入，您現在應該會再看到首頁，首頁的角落為「您好，**Hello, <User Name>！**</span><span class="sxs-lookup"><span data-stu-id="fea9a-234">Once you log in with a user in the AD domain of the AD FS deployment, you should now see the homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="fea9a-235">。</span><span class="sxs-lookup"><span data-stu-id="fea9a-235">in the corner.</span></span> <span data-ttu-id="fea9a-236">以下是我看到的內容。</span><span class="sxs-lookup"><span data-stu-id="fea9a-236">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="fea9a-237">到目前為止，您已經成功地完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="fea9a-237">So far, you've succeeded in the following ways:</span></span>

* <span data-ttu-id="fea9a-238">您的應用程式已成功連線 AD FS，並在 AD FS 資料庫中找到相符的 RP 識別碼</span><span class="sxs-lookup"><span data-stu-id="fea9a-238">Your application has successfully reached AD FS and a matching RP identifier is found in the AD FS database</span></span>
* <span data-ttu-id="fea9a-239">AD FS 已成功驗證 AD 使用者，並將您重新導向回應用程式的首頁</span><span class="sxs-lookup"><span data-stu-id="fea9a-239">AD FS has successfully authenticated an AD user and redirect you back to the application's homepage</span></span>
* <span data-ttu-id="fea9a-240">AD FS 已將名稱宣告 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) 成功傳送到您的應用程式，並在角落顯示使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="fea9a-240">AD FS as successfully sent the name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) to your application, as indicated by the fact that the user name is displayed in the corner.</span></span> 

<span data-ttu-id="fea9a-241">如果缺少名稱宣告，您應該會看到「**您好！**」。</span><span class="sxs-lookup"><span data-stu-id="fea9a-241">If the name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="fea9a-242">如果您看一下 Views\Shared\_LoginPartial.cshtml，您會發現其使用 `User.Identity.Name` 來顯示使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="fea9a-242">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` to display the user name.</span></span> <span data-ttu-id="fea9a-243">如前所述，若可在 SAML 權杖中取得已驗證使用者的名稱宣告，ASP.NET 會使用它來產生這個屬性。</span><span class="sxs-lookup"><span data-stu-id="fea9a-243">As mentioned previously, if the name claim of the authenticated user is available in the SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="fea9a-244">若要查看 AD FS 傳送的所有宣告，請將中斷點放在索引動作方法的 Controllers\HomeController.cs 中。</span><span class="sxs-lookup"><span data-stu-id="fea9a-244">To see all the claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in the Index action method.</span></span> <span data-ttu-id="fea9a-245">驗證使用者後，檢查 `System.Security.Claims.Current.Claims` 集合。</span><span class="sxs-lookup"><span data-stu-id="fea9a-245">After the user is authenticated, inspect the `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="fea9a-246">授權使用者使用特定的控制器或動作</span><span class="sxs-lookup"><span data-stu-id="fea9a-246">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="fea9a-247">由於您已在 RP 信任組態中加入做為角色宣告的群組成員資格，因此您現在可以在 `[Authorize(Roles="...")]` 裝飾中，直接將這些成員資格運用於控制器和動作。</span><span class="sxs-lookup"><span data-stu-id="fea9a-247">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in the `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="fea9a-248">在使用建立-讀取-更新-刪除 (CRUD) 模式的特定業務應用程式中，您可以授權特定角色來存取每個動作。</span><span class="sxs-lookup"><span data-stu-id="fea9a-248">In a line-of-business application with the Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles to access each action.</span></span> <span data-ttu-id="fea9a-249">現在，您只要在現有的主控制器上嘗試這項功能。</span><span class="sxs-lookup"><span data-stu-id="fea9a-249">For now, you will just try out this feature on the existing Home controller.</span></span>

1. <span data-ttu-id="fea9a-250">開啟 Controllers\HomeController.cs。</span><span class="sxs-lookup"><span data-stu-id="fea9a-250">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="fea9a-251">使用已驗證使用者擁有的安全性群組成員資格來裝飾 `About` 和 `Contact` 動作方法 (類似下列程式碼)。</span><span class="sxs-lookup"><span data-stu-id="fea9a-251">Decorate the `About` and `Contact` action methods similar to the following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="fea9a-252">由於我在 AD FS 實驗室環境中將**「測試使用者」**新增至**「測試群組」**，我將在 `About` 上使用測試群組來測試授權。</span><span class="sxs-lookup"><span data-stu-id="fea9a-252">Since I added **Test User** to **Test Group** in my AD FS lab environment, I'll use Test Group to test authorization on `About`.</span></span> <span data-ttu-id="fea9a-253">若為 `Contact`，我將測試**「測試使用者」**不屬於之 **Domain Admins** 的負面案例。</span><span class="sxs-lookup"><span data-stu-id="fea9a-253">For `Contact`, I'll test the negative case of **Domain Admins**, to which **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="fea9a-254">輸入 `F5` 開始偵錯工具並登入，然後按一下 [關於]。</span><span class="sxs-lookup"><span data-stu-id="fea9a-254">Start the debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="fea9a-255">如果該動作已授權給已驗證的使用者，您現在應可順利檢視 `~/About/Index` 頁面。</span><span class="sxs-lookup"><span data-stu-id="fea9a-255">You should now be viewing the `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="fea9a-256">現在按一下 [連絡人]，在我的案例中應該不會將該動作授權給**「測試使用者」**。</span><span class="sxs-lookup"><span data-stu-id="fea9a-256">Now click **Contact**, which in my case should not authorize **Test User** for the action.</span></span> <span data-ttu-id="fea9a-257">不過，瀏覽器會重新導向至 AD FS，最後會顯示這則訊息：</span><span class="sxs-lookup"><span data-stu-id="fea9a-257">However, the browser is redirected to AD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="fea9a-258">如果您在 AD FS 伺服器的事件檢視器中調查此錯誤，您會看到這則例外狀況訊息：</span><span class="sxs-lookup"><span data-stu-id="fea9a-258">If you investigate this error in Event Viewer on the AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="fea9a-259">此錯誤的原因是，在未授權使用者的角色時，MVC 預設會傳回「401 未授權」。</span><span class="sxs-lookup"><span data-stu-id="fea9a-259">The reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="fea9a-260">這樣會針對您的身分識別提供者 (AD FS) 觸發重新驗證要求。</span><span class="sxs-lookup"><span data-stu-id="fea9a-260">This triggers a reauthentication request to your identity provider (AD FS).</span></span> <span data-ttu-id="fea9a-261">因為使用者已通過驗證，AD FS 會返回相同的頁面，然後發出另一個 401，從而建立重新導向迴圈。</span><span class="sxs-lookup"><span data-stu-id="fea9a-261">Since the user is already authenticated, AD FS returns to the same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="fea9a-262">您會使用簡單的邏輯來覆寫 AuthorizeAttribute 的 `HandleUnauthorizedRequest` 方法，從而顯示有意義的資訊而非持續出現重新導向迴圈。</span><span class="sxs-lookup"><span data-stu-id="fea9a-262">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic to show something that makes sense instead of continuing the redirect loop.</span></span>
5. <span data-ttu-id="fea9a-263">在稱為 AuthorizeAttribute.cs 的專案中建立檔案，並將下列程式碼貼至其中。</span><span class="sxs-lookup"><span data-stu-id="fea9a-263">Create a file in the project called AuthorizeAttribute.cs, and paste the following code into it.</span></span>
   
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
   
    <span data-ttu-id="fea9a-264">覆寫程式碼會在驗證的情況下 (未經授權的情況除外) 傳送 HTTP 403 (禁止) 而非 HTTP 401 (未授權)。</span><span class="sxs-lookup"><span data-stu-id="fea9a-264">The override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="fea9a-265">按 `F5`再次執行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="fea9a-265">Run the debugger again with `F5`.</span></span> <span data-ttu-id="fea9a-266">現在按一下 [連絡人]  會顯示更具參考性的 (雖然不討喜) 錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="fea9a-266">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="fea9a-267">再次將應用程式發行至 Azure 應用程式服務 Web 應用程式，並測試即時應用程式的行為。</span><span class="sxs-lookup"><span data-stu-id="fea9a-267">Publish the application to Azure App Service Web Apps again, and test the behavior of the live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a><span data-ttu-id="fea9a-268">連線至內部部署資料</span><span class="sxs-lookup"><span data-stu-id="fea9a-268">Connect to on-premises data</span></span>
<span data-ttu-id="fea9a-269">您會想要使用 AD FS (而不是使用 Azure Active Directory) 來實作特定業務應用程式的原因是，遵守在外部部署保存組織資料的法規需求。</span><span class="sxs-lookup"><span data-stu-id="fea9a-269">A reason that you would want to implement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="fea9a-270">這也表示您在 Azure 中的 Web 應用程式必須存取內部部署資料庫，因為您無法使用 [SQL Database](/services/sql-database/) 作為您 Web 應用程式的資料層。</span><span class="sxs-lookup"><span data-stu-id="fea9a-270">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed to use [SQL Database](/services/sql-database/) as the data tier for your web apps.</span></span>

<span data-ttu-id="fea9a-271">Azure App Service Web Apps 可透過兩種方式支援存取內部部署資料庫：[混合式連線](../biztalk-services/integration-hybrid-connection-overview.md)和[虛擬網路](web-sites-integrate-with-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="fea9a-271">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="fea9a-272">如需詳細資訊，請參閱 [使用 VNET 整合和混合式連線搭配 Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/)。</span><span class="sxs-lookup"><span data-stu-id="fea9a-272">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="fea9a-273">進一步資源</span><span class="sxs-lookup"><span data-stu-id="fea9a-273">Further resources</span></span>
* [<span data-ttu-id="fea9a-274">在 Azure 應用程式中使用內部部署 Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="fea9a-274">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="fea9a-275">使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="fea9a-275">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="fea9a-276">在 Visual Studio 2013 中搭配使用內部部署組織驗證選項 (ADFS) 與 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="fea9a-276">Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="fea9a-277">將 VS2013 Web 專案從 WIF 移轉到 Katana</span><span class="sxs-lookup"><span data-stu-id="fea9a-277">Migrate a VS2013 Web Project From WIF to Katana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="fea9a-278">Active Directory Federation Services 概觀</span><span class="sxs-lookup"><span data-stu-id="fea9a-278">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="fea9a-279">WS-同盟 1.1 規格</span><span class="sxs-lookup"><span data-stu-id="fea9a-279">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

