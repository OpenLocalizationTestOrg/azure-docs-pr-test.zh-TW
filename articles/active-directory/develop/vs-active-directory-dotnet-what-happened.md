---
title: "連線到 Azure AD 時對 MVC 專案所做的變更 | Microsoft Docs"
description: "說明您使用 Visual Studio 已連線服務連線至 Azure AD 時，MVC 專案會有何狀況"
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
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="46be9-103">我的 MVC 專案 (Visual Studio Azure Active Directory 已連線服務) 發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="46be9-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46be9-104">開始使用</span><span class="sxs-lookup"><span data-stu-id="46be9-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="46be9-105">發生什麼情形</span><span class="sxs-lookup"><span data-stu-id="46be9-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="46be9-106">已加入參考</span><span class="sxs-lookup"><span data-stu-id="46be9-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="46be9-107">NuGet 封裝參考</span><span class="sxs-lookup"><span data-stu-id="46be9-107">NuGet package references</span></span>
* <span data-ttu-id="46be9-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="46be9-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="46be9-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="46be9-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="46be9-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="46be9-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="46be9-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="46be9-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="46be9-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="46be9-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="46be9-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="46be9-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="46be9-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="46be9-114">**Owin**</span></span>
* <span data-ttu-id="46be9-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="46be9-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="46be9-116">.NET 參考</span><span class="sxs-lookup"><span data-stu-id="46be9-116">.NET references</span></span>
* <span data-ttu-id="46be9-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="46be9-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="46be9-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="46be9-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="46be9-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="46be9-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="46be9-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="46be9-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="46be9-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="46be9-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="46be9-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="46be9-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="46be9-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="46be9-123">**Owin**</span></span>
* <span data-ttu-id="46be9-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="46be9-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="46be9-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="46be9-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="46be9-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="46be9-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="46be9-127">已加入程式碼</span><span class="sxs-lookup"><span data-stu-id="46be9-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="46be9-128">程式碼檔案加入至專案</span><span class="sxs-lookup"><span data-stu-id="46be9-128">Code files were added to your project</span></span>
<span data-ttu-id="46be9-129">驗證啟動類別 **App_Start/Startup.Auth.cs** 加入至內含 Azure AD 驗證之啟動邏輯的專案。</span><span class="sxs-lookup"><span data-stu-id="46be9-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="46be9-130">另外也已加入控制器類別 Controllers/AccountController.cs，內含 **SignIn()** 和 **SignOut()** 方法。</span><span class="sxs-lookup"><span data-stu-id="46be9-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="46be9-131">最後，已加入部分檢視 **Views/Shared/_LoginPartial.cshtml**，內含 SignIn/SignOut 的動作連結。</span><span class="sxs-lookup"><span data-stu-id="46be9-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="46be9-132">啟動程式碼已加入至專案</span><span class="sxs-lookup"><span data-stu-id="46be9-132">Startup code was added to your project</span></span>
<span data-ttu-id="46be9-133">如果專案中已有啟動類別，則已更新 **Configuration** 方法來包含 **ConfigureAuth(app)** 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="46be9-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="46be9-134">否則已將啟動類別加入至專案。</span><span class="sxs-lookup"><span data-stu-id="46be9-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="46be9-135">app.config 或 web.config 有新的組態值</span><span class="sxs-lookup"><span data-stu-id="46be9-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="46be9-136">已加入下列組態項目。</span><span class="sxs-lookup"><span data-stu-id="46be9-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="46be9-137">建立 Azure Active Directory (AD) 應用程式</span><span class="sxs-lookup"><span data-stu-id="46be9-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="46be9-138">在您於精靈中選取的目錄中建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="46be9-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="46be9-139">如果我核取了 [停用個別使用者帳戶驗證] ，我的專案會有什麼其他變更？</span><span class="sxs-lookup"><span data-stu-id="46be9-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="46be9-140">NuGet 封裝參考會被移除，檔案也會移除並加以備份。</span><span class="sxs-lookup"><span data-stu-id="46be9-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="46be9-141">根據您的專案狀態，您可能必須手動移除其他參考或檔案，或修改為適當的程式碼。</span><span class="sxs-lookup"><span data-stu-id="46be9-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="46be9-142">移除的 NuGet 封裝參考 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="46be9-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="46be9-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="46be9-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="46be9-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="46be9-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="46be9-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="46be9-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="46be9-146">備份和移除的程式碼檔案 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="46be9-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="46be9-147">下列每個檔案都會備份，並且從專案中移除。</span><span class="sxs-lookup"><span data-stu-id="46be9-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="46be9-148">備份檔案位於專案目錄根目錄的「備份」資料夾。</span><span class="sxs-lookup"><span data-stu-id="46be9-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="46be9-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="46be9-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="46be9-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="46be9-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="46be9-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="46be9-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="46be9-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="46be9-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="46be9-153">備份的程式碼檔案 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="46be9-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="46be9-154">下列每個檔案會在取代之前備份。</span><span class="sxs-lookup"><span data-stu-id="46be9-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="46be9-155">備份檔案位於專案目錄根目錄的「備份」資料夾。</span><span class="sxs-lookup"><span data-stu-id="46be9-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="46be9-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="46be9-156">**Startup.cs**</span></span>
* <span data-ttu-id="46be9-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="46be9-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="46be9-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="46be9-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="46be9-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="46be9-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="46be9-160">如果我核取了 [ *讀取目錄資料*]，我的專案會有什麼其他變更？</span><span class="sxs-lookup"><span data-stu-id="46be9-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="46be9-161">已加入其他參考。</span><span class="sxs-lookup"><span data-stu-id="46be9-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="46be9-162">其他 NuGet 封裝參考</span><span class="sxs-lookup"><span data-stu-id="46be9-162">Additional NuGet package references</span></span>
* <span data-ttu-id="46be9-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="46be9-163">**EntityFramework**</span></span>
* <span data-ttu-id="46be9-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="46be9-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="46be9-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="46be9-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="46be9-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="46be9-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="46be9-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="46be9-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="46be9-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="46be9-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="46be9-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="46be9-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="46be9-170">其他 .NET 參考</span><span class="sxs-lookup"><span data-stu-id="46be9-170">Additional .NET references</span></span>
* <span data-ttu-id="46be9-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="46be9-171">**EntityFramework**</span></span>
* <span data-ttu-id="46be9-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="46be9-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="46be9-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="46be9-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="46be9-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="46be9-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="46be9-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="46be9-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="46be9-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="46be9-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="46be9-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="46be9-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="46be9-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="46be9-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="46be9-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="46be9-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="46be9-180">其他程式碼檔案已加入至專案</span><span class="sxs-lookup"><span data-stu-id="46be9-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="46be9-181">兩個檔案已加入以支援 Token 快取：**Models\ADALTokenCache.cs** 和 **Models\ApplicationDbContext.cs**。</span><span class="sxs-lookup"><span data-stu-id="46be9-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="46be9-182">已加入其他控制器和檢視，以說明使用 Azure 圖形 API 存取使用者設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="46be9-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="46be9-183">這些檔案是 **Controllers\UserProfileController.cs** 和 **Views\UserProfile\Index.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="46be9-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="46be9-184">其他啟動程式碼已加入至專案</span><span class="sxs-lookup"><span data-stu-id="46be9-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="46be9-185">在 **startup.auth.cs** 檔案中，新的 **OpenIdConnectAuthenticationNotifications** 物件已加入 **OpenIdConnectAuthenticationOptions** 的 **Notifications** 成員。</span><span class="sxs-lookup"><span data-stu-id="46be9-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="46be9-186">這是為了啟用接收 OAuth 程式碼，並用它交換存取權杖。</span><span class="sxs-lookup"><span data-stu-id="46be9-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="46be9-187">app.config 或 web.config 已進行其他變更</span><span class="sxs-lookup"><span data-stu-id="46be9-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="46be9-188">已加入下列其他組態項目。</span><span class="sxs-lookup"><span data-stu-id="46be9-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="46be9-189">已加入下列組態區段和連接字串。</span><span class="sxs-lookup"><span data-stu-id="46be9-189">The following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="46be9-190">Azure Active Directory 應用程式已更新</span><span class="sxs-lookup"><span data-stu-id="46be9-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="46be9-191">Azure Active Directory 應用程式已更新為包含「讀取目錄資料」權限，並已建立其他的金鑰做為 **web.config** 檔案中的 ida:ClientSecret。</span><span class="sxs-lookup"><span data-stu-id="46be9-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46be9-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46be9-192">Next steps</span></span>
- [<span data-ttu-id="46be9-193">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46be9-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

