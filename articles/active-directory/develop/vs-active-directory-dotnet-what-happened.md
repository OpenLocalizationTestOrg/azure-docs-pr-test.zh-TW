---
title: "所做的 aaaChanges tooa MVC 專案，當您連接 tooAzure AD |Microsoft 文件"
description: "描述使用 Visual Studio 連接的服務連線 tooAzure AD 時所採取的 tooyour MVC 專案"
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="ff1c1-103">哪些情形的 toomy MVC 專案 （Visual Studio Azure Active Directory 已連線服務）？</span><span class="sxs-lookup"><span data-stu-id="ff1c1-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff1c1-104">開始使用</span><span class="sxs-lookup"><span data-stu-id="ff1c1-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="ff1c1-105">發生什麼情形</span><span class="sxs-lookup"><span data-stu-id="ff1c1-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="ff1c1-106">已加入參考</span><span class="sxs-lookup"><span data-stu-id="ff1c1-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="ff1c1-107">NuGet 封裝參考</span><span class="sxs-lookup"><span data-stu-id="ff1c1-107">NuGet package references</span></span>
* <span data-ttu-id="ff1c1-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="ff1c1-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="ff1c1-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="ff1c1-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="ff1c1-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="ff1c1-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="ff1c1-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-114">**Owin**</span></span>
* <span data-ttu-id="ff1c1-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="ff1c1-116">.NET 參考</span><span class="sxs-lookup"><span data-stu-id="ff1c1-116">.NET references</span></span>
* <span data-ttu-id="ff1c1-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="ff1c1-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="ff1c1-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="ff1c1-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="ff1c1-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="ff1c1-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="ff1c1-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-123">**Owin**</span></span>
* <span data-ttu-id="ff1c1-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="ff1c1-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="ff1c1-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="ff1c1-127">已加入程式碼</span><span class="sxs-lookup"><span data-stu-id="ff1c1-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="ff1c1-128">程式碼檔案加入 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="ff1c1-128">Code files were added tooyour project</span></span>
<span data-ttu-id="ff1c1-129">驗證啟動類別**App_Start/Startup.Auth.cs**已加入 tooyour 專案包含 Azure AD 驗證的啟動邏輯。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="ff1c1-130">另外也已加入控制器類別 Controllers/AccountController.cs，內含 **SignIn()** 和 **SignOut()** 方法。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="ff1c1-131">最後，已加入部分檢視 **Views/Shared/_LoginPartial.cshtml**，內含 SignIn/SignOut 的動作連結。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="ff1c1-132">啟始程式碼已加入 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="ff1c1-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="ff1c1-133">如果您已經在專案中啟動類別，hello**組態**方法太更新的 tooinclude 呼叫**ConfigureAuth(app)**。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="ff1c1-134">否則，請啟動類別已加入 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="ff1c1-135">app.config 或 web.config 有新的組態值</span><span class="sxs-lookup"><span data-stu-id="ff1c1-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="ff1c1-136">已加入下列組態項目 hello。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="ff1c1-137">建立 Azure Active Directory (AD) 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff1c1-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="ff1c1-138">Azure AD 應用程式已建立您 hello 精靈中選取的 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="ff1c1-139">如果在簽*停用個別使用者帳戶驗證*，toomy 專案所做其他變更？</span><span class="sxs-lookup"><span data-stu-id="ff1c1-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="ff1c1-140">NuGet 封裝參考會被移除，檔案也會移除並加以備份。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="ff1c1-141">根據您的專案 hello 狀態，您可能必須 toomanually 移除其他參考或檔案，或修改為適當的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="ff1c1-142">移除的 NuGet 封裝參考 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="ff1c1-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="ff1c1-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="ff1c1-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="ff1c1-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="ff1c1-146">備份和移除的程式碼檔案 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="ff1c1-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="ff1c1-147">每個下列檔案已備份，並且從 hello 專案中移除。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="ff1c1-148">備份檔案位於根目錄 hello hello 專案目錄的 [備份] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="ff1c1-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="ff1c1-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="ff1c1-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="ff1c1-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="ff1c1-153">備份的程式碼檔案 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="ff1c1-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="ff1c1-154">下列每個檔案會在取代之前備份。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="ff1c1-155">備份檔案位於根目錄 hello hello 專案目錄的 [備份] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="ff1c1-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-156">**Startup.cs**</span></span>
* <span data-ttu-id="ff1c1-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="ff1c1-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="ff1c1-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="ff1c1-160">如果在簽*讀取目錄資料*，toomy 專案所做其他變更？</span><span class="sxs-lookup"><span data-stu-id="ff1c1-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="ff1c1-161">已加入其他參考。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="ff1c1-162">其他 NuGet 封裝參考</span><span class="sxs-lookup"><span data-stu-id="ff1c1-162">Additional NuGet package references</span></span>
* <span data-ttu-id="ff1c1-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-163">**EntityFramework**</span></span>
* <span data-ttu-id="ff1c1-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="ff1c1-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="ff1c1-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="ff1c1-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="ff1c1-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="ff1c1-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="ff1c1-170">其他 .NET 參考</span><span class="sxs-lookup"><span data-stu-id="ff1c1-170">Additional .NET references</span></span>
* <span data-ttu-id="ff1c1-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-171">**EntityFramework**</span></span>
* <span data-ttu-id="ff1c1-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="ff1c1-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="ff1c1-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="ff1c1-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="ff1c1-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="ff1c1-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="ff1c1-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="ff1c1-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="ff1c1-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="ff1c1-180">其他的程式碼檔案加入 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="ff1c1-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="ff1c1-181">已加入兩個檔案 toosupport 權杖快取： **Models\ADALTokenCache.cs**和**Models\ApplicationDbContext.cs**。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="ff1c1-182">其他控制器和檢視已加入 tooillustrate 存取使用 Azure graph Api 的使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="ff1c1-183">這些檔案是 **Controllers\UserProfileController.cs** 和 **Views\UserProfile\Index.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="ff1c1-184">已新增其他的啟動程式碼 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="ff1c1-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="ff1c1-185">在 hello **startup.auth.cs**檔案，新**OpenIdConnectAuthenticationNotifications**物件已加入 toohello**通知**hello 的成員**OpenIdConnectAuthenticationOptions**。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="ff1c1-186">這是 tooenable 接收 hello OAuth 的程式碼和交換存取權杖。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="ff1c1-187">Tooyour app.config 或 web.config 進行其他變更</span><span class="sxs-lookup"><span data-stu-id="ff1c1-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="ff1c1-188">hello 下列額外的設定項目已加入。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="ff1c1-189">hello 下列組態區段和連接字串已加入。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-189">hello following configuration sections and connection string have been added.</span></span>

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="ff1c1-190">Azure Active Directory 應用程式已更新</span><span class="sxs-lookup"><span data-stu-id="ff1c1-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="ff1c1-191">您 Azure Active Directory 應用程式已更新的 tooinclude hello*讀取目錄資料*權限，以及其他機碼已建立的已當做 hello *ida: ClientSecret*在 hello **web.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="ff1c1-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff1c1-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff1c1-192">Next steps</span></span>
- [<span data-ttu-id="ff1c1-193">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff1c1-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

