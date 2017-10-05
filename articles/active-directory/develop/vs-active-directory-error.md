---
title: "如何使用 Azure Active Directory 連線精靈診斷錯誤"
description: "Active directory 連線精靈偵測到不相容的驗證類型"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 4f29f62b2996cae98b02c1ed5fcb59eca09301ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a><span data-ttu-id="07ba7-103">使用 Azure Active Directory 連線精靈診斷錯誤</span><span class="sxs-lookup"><span data-stu-id="07ba7-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="07ba7-104">偵測先前的驗證程式碼時，精靈偵測到不相容的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="07ba7-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="07ba7-105">檢查什麼？</span><span class="sxs-lookup"><span data-stu-id="07ba7-105">What is being checked?</span></span>
<span data-ttu-id="07ba7-106">**注意：**必須建置專案，才能正確偵測該專案中先前的驗證碼。</span><span class="sxs-lookup"><span data-stu-id="07ba7-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="07ba7-107">如果遇到這個錯誤，且您的專案中沒有先前的驗證碼，請重建並再試一次。</span><span class="sxs-lookup"><span data-stu-id="07ba7-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="07ba7-108">專案類型</span><span class="sxs-lookup"><span data-stu-id="07ba7-108">Project Types</span></span>
<span data-ttu-id="07ba7-109">精靈會檢查您正在開發的專案類型，使其可將正確的驗證邏輯插入專案。</span><span class="sxs-lookup"><span data-stu-id="07ba7-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span>  <span data-ttu-id="07ba7-110">如果專案中有任何衍生自 `ApiController` 的控制器，則該專案會被視為 WebAPI 專案。</span><span class="sxs-lookup"><span data-stu-id="07ba7-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span>  <span data-ttu-id="07ba7-111">如果專案中只有衍生自 `MVC.Controller` 的控制器，則該專案會被視為 MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="07ba7-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span>  <span data-ttu-id="07ba7-112">精靈不支援其他類型的專案。</span><span class="sxs-lookup"><span data-stu-id="07ba7-112">Anything else is not supported by the wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="07ba7-113">相容的驗證碼</span><span class="sxs-lookup"><span data-stu-id="07ba7-113">Compatible Authentication Code</span></span>
<span data-ttu-id="07ba7-114">精靈也會檢查先前對精靈設定或與精靈相容的驗證設定。</span><span class="sxs-lookup"><span data-stu-id="07ba7-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span></span>  <span data-ttu-id="07ba7-115">如果所有設定皆存在，則會將它視為可重新進入的情況，而精靈會開啟並顯示設定。</span><span class="sxs-lookup"><span data-stu-id="07ba7-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span></span>  <span data-ttu-id="07ba7-116">如果只有部分設定存在，則會將它視為錯誤情況。</span><span class="sxs-lookup"><span data-stu-id="07ba7-116">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="07ba7-117">在 MVC 專案中，精靈會檢查先前使用此精靈所產生的以下任何設定：</span><span class="sxs-lookup"><span data-stu-id="07ba7-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="07ba7-118">此外，精靈會檢查先前使用此精靈所產生 Web API 專案中的以下任何設定：</span><span class="sxs-lookup"><span data-stu-id="07ba7-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="07ba7-119">不相容的驗證碼</span><span class="sxs-lookup"><span data-stu-id="07ba7-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="07ba7-120">最後，精靈會嘗試偵測舊版 Visual Studio 所設定的驗證碼版本。</span><span class="sxs-lookup"><span data-stu-id="07ba7-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="07ba7-121">如果收到此錯誤，表示您的專案包含不相容的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="07ba7-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="07ba7-122">精靈會從舊版 Visual Studio 中偵測下列驗證類型：</span><span class="sxs-lookup"><span data-stu-id="07ba7-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="07ba7-123">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="07ba7-123">Windows Authentication</span></span> 
* <span data-ttu-id="07ba7-124">個別使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="07ba7-124">Individual User Accounts</span></span> 
* <span data-ttu-id="07ba7-125">組織帳戶</span><span class="sxs-lookup"><span data-stu-id="07ba7-125">Organizational Accounts</span></span> 

<span data-ttu-id="07ba7-126">為偵測 MVC 專案中的「Windows 驗證」，精靈會在您的 **web.config** 檔案中尋找 `authentication` 元素。</span><span class="sxs-lookup"><span data-stu-id="07ba7-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="07ba7-127">為偵測 Web API 專案中的「Windows 驗證」，精靈會在您專案的 **.csproj** 檔案中尋找 `IISExpressWindowsAuthentication` 元素：</span><span class="sxs-lookup"><span data-stu-id="07ba7-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="07ba7-128">為偵測「個別使用者帳戶」驗證，精靈會在您的 **Packages.config** 檔案中尋找 package 元素。</span><span class="sxs-lookup"><span data-stu-id="07ba7-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="07ba7-129">為偵測舊式「組織帳戶」驗證，精靈會在 **web.config**中尋找下列元素：</span><span class="sxs-lookup"><span data-stu-id="07ba7-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="07ba7-130">若要變更驗證類型，請移除不相容的驗證類型，然後重新執行精靈。</span><span class="sxs-lookup"><span data-stu-id="07ba7-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span></span>

<span data-ttu-id="07ba7-131">如需詳細資訊，請參閱 [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="07ba7-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="07ba7-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07ba7-132">Next steps</span></span>
- [<span data-ttu-id="07ba7-133">Azure AD 的驗證案例</span><span class="sxs-lookup"><span data-stu-id="07ba7-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)