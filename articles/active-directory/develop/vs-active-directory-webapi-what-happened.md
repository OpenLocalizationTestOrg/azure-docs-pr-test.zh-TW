---
title: "連接 tooAzure AD 時所做的 aaaChanges tooa WebApi 專案 |Microsoft 文件"
description: "描述使用 Visual Studio 連接 tooAzure AD 時所採取的 tooyour WebApi 專案"
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
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="c1f10-103">哪些情形的 toomy WebApi 專案 （Visual Studio Azure Active Directory 已連線服務）</span><span class="sxs-lookup"><span data-stu-id="c1f10-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1f10-104">開始使用</span><span class="sxs-lookup"><span data-stu-id="c1f10-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="c1f10-105">發生什麼情形</span><span class="sxs-lookup"><span data-stu-id="c1f10-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="c1f10-106">已加入參考</span><span class="sxs-lookup"><span data-stu-id="c1f10-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="c1f10-107">NuGet 封裝參考</span><span class="sxs-lookup"><span data-stu-id="c1f10-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="c1f10-108">.NET 參考</span><span class="sxs-lookup"><span data-stu-id="c1f10-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="c1f10-109">程式碼變更</span><span class="sxs-lookup"><span data-stu-id="c1f10-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="c1f10-110">程式碼檔案加入 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="c1f10-110">Code files were added tooyour project</span></span>
<span data-ttu-id="c1f10-111">驗證啟動類別**App_Start/Startup.Auth.cs**已加入 tooyour 專案包含 Azure AD 驗證的啟動邏輯。</span><span class="sxs-lookup"><span data-stu-id="c1f10-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="c1f10-112">啟始程式碼已加入 tooyour 專案</span><span class="sxs-lookup"><span data-stu-id="c1f10-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="c1f10-113">如果您已經在專案中啟動類別，hello**組態**方法太更新的 tooinclude 呼叫`ConfigureAuth(app)`。</span><span class="sxs-lookup"><span data-stu-id="c1f10-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="c1f10-114">否則，請啟動類別已加入 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="c1f10-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="c1f10-115">app.config 或 web.config 檔案有新的組態值。</span><span class="sxs-lookup"><span data-stu-id="c1f10-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="c1f10-116">已加入下列組態項目 hello。</span><span class="sxs-lookup"><span data-stu-id="c1f10-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="c1f10-117">已建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="c1f10-117">An Azure AD App was created</span></span>
<span data-ttu-id="c1f10-118">Azure AD 應用程式已建立您 hello 精靈中選取的 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="c1f10-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="c1f10-119">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1f10-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="c1f10-120">如果在簽*停用個別使用者帳戶驗證*，toomy 專案所做其他變更？</span><span class="sxs-lookup"><span data-stu-id="c1f10-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="c1f10-121">NuGet 封裝參考會被移除，檔案也會移除並加以備份。</span><span class="sxs-lookup"><span data-stu-id="c1f10-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="c1f10-122">根據您的專案 hello 狀態，您可能必須 toomanually 移除其他參考或檔案，或修改為適當的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c1f10-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="c1f10-123">移除的 NuGet 封裝參考 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="c1f10-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="c1f10-124">備份和移除的程式碼檔案 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="c1f10-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="c1f10-125">每個下列檔案已備份，並且從 hello 專案中移除。</span><span class="sxs-lookup"><span data-stu-id="c1f10-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="c1f10-126">備份檔案位於根目錄 hello hello 專案目錄的 [備份] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c1f10-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="c1f10-127">備份的程式碼檔案 (如果存在)</span><span class="sxs-lookup"><span data-stu-id="c1f10-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="c1f10-128">下列每個檔案會在取代之前備份。</span><span class="sxs-lookup"><span data-stu-id="c1f10-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="c1f10-129">備份檔案位於根目錄 hello hello 專案目錄的 [備份] 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c1f10-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="c1f10-130">如果在簽*讀取目錄資料*，toomy 專案所做其他變更？</span><span class="sxs-lookup"><span data-stu-id="c1f10-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="c1f10-131">Tooyour app.config 或 web.config 進行其他變更</span><span class="sxs-lookup"><span data-stu-id="c1f10-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="c1f10-132">hello 下列額外的設定項目已加入。</span><span class="sxs-lookup"><span data-stu-id="c1f10-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="c1f10-133">Azure Active Directory 應用程式已更新</span><span class="sxs-lookup"><span data-stu-id="c1f10-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="c1f10-134">您 Azure Active Directory 應用程式已更新的 tooinclude hello*讀取目錄資料*權限，以及其他機碼已建立的已當做 hello *ida： 密碼*在 hello`web.config`檔案。</span><span class="sxs-lookup"><span data-stu-id="c1f10-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1f10-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1f10-135">Next steps</span></span>
- [<span data-ttu-id="c1f10-136">深入了解 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c1f10-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

