---
title: "連線到 Azure AD 時對 WebApi 專案所做的變更 | Microsoft Docs"
description: "說明當您使用 Visual Studio 來連線到 Azure AD 時，您的 WebApi 專案會發生什麼狀況"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 086e5a9622cad681cd282345d97e0c28ee7de2fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="d801a-103">我的 WebApi 專案發生什麼狀況 (Visual Studio Azure Active Directory 已連接服務)</span><span class="sxs-lookup"><span data-stu-id="d801a-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d801a-104">開始使用</span><span class="sxs-lookup"><span data-stu-id="d801a-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="d801a-105">發生什麼情形</span><span class="sxs-lookup"><span data-stu-id="d801a-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="d801a-106">已加入參考</span><span class="sxs-lookup"><span data-stu-id="d801a-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="d801a-107">NuGet 封裝參考</span><span class="sxs-lookup"><span data-stu-id="d801a-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="d801a-108">.NET 參考</span><span class="sxs-lookup"><span data-stu-id="d801a-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="d801a-109">程式碼變更</span><span class="sxs-lookup"><span data-stu-id="d801a-109">Code changes</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="d801a-110">程式碼檔案加入至專案</span><span class="sxs-lookup"><span data-stu-id="d801a-110">Code files were added to your project</span></span>
<span data-ttu-id="d801a-111">驗證啟動類別 **App_Start/Startup.Auth.cs** 加入至內含 Azure AD 驗證之啟動邏輯的專案。</span><span class="sxs-lookup"><span data-stu-id="d801a-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="d801a-112">啟動程式碼已加入至專案</span><span class="sxs-lookup"><span data-stu-id="d801a-112">Startup code was added to your project</span></span>
<span data-ttu-id="d801a-113">如果專案中已有啟動類別，則已更新 **Configuration`ConfigureAuth(app)` 方法來包含** 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="d801a-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span></span> <span data-ttu-id="d801a-114">否則已將啟動類別加入至專案。</span><span class="sxs-lookup"><span data-stu-id="d801a-114">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="d801a-115">app.config 或 web.config 檔案有新的組態值。</span><span class="sxs-lookup"><span data-stu-id="d801a-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="d801a-116">已加入下列組態項目。</span><span class="sxs-lookup"><span data-stu-id="d801a-116">The following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="d801a-117">已建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="d801a-117">An Azure AD App was created</span></span>
<span data-ttu-id="d801a-118">在您於精靈中選取的目錄中建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d801a-118">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

[<span data-ttu-id="d801a-119">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d801a-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="d801a-120">如果我核取了 [ *停用個別使用者帳戶驗證*]，我的專案會有什麼其他變更？</span><span class="sxs-lookup"><span data-stu-id="d801a-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="d801a-121">NuGet 封裝參考會被移除，檔案也會移除並加以備份。</span><span class="sxs-lookup"><span data-stu-id="d801a-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="d801a-122">根據您的專案狀態，您可能必須手動移除其他參考或檔案，或修改為適當的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d801a-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="d801a-123">移除的 NuGet 封裝參考 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="d801a-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="d801a-124">備份和移除的程式碼檔案 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="d801a-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="d801a-125">下列每個檔案都會備份，並且從專案中移除。</span><span class="sxs-lookup"><span data-stu-id="d801a-125">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="d801a-126">備份檔案位於專案目錄根目錄的「備份」資料夾。</span><span class="sxs-lookup"><span data-stu-id="d801a-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="d801a-127">備份的程式碼檔案 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="d801a-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="d801a-128">下列每個檔案會在取代之前備份。</span><span class="sxs-lookup"><span data-stu-id="d801a-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="d801a-129">備份檔案位於專案目錄根目錄的「備份」資料夾。</span><span class="sxs-lookup"><span data-stu-id="d801a-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="d801a-130">如果我核取了 [ *讀取目錄資料*]，我的專案會有什麼其他變更？</span><span class="sxs-lookup"><span data-stu-id="d801a-130">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="d801a-131">app.config 或 web.config 已進行其他變更</span><span class="sxs-lookup"><span data-stu-id="d801a-131">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="d801a-132">已加入下列其他組態項目。</span><span class="sxs-lookup"><span data-stu-id="d801a-132">The following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="d801a-133">Azure Active Directory 應用程式已更新</span><span class="sxs-lookup"><span data-stu-id="d801a-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="d801a-134">Azure Active Directory 應用程式已更新為包含「讀取目錄資料」權限，並已建立其他的金鑰做為 `web.config` 檔案中的 ida:Password。</span><span class="sxs-lookup"><span data-stu-id="d801a-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d801a-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d801a-135">Next steps</span></span>
- [<span data-ttu-id="d801a-136">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d801a-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

