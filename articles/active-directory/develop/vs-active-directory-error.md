---
title: "aaaHow toodiagnose 錯誤以 hello Azure Active Directory 連線精靈"
description: "hello active directory 連線精靈偵測到不相容的驗證類型"
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
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="72332-103">診斷錯誤以 hello Azure Active Directory 連線精靈</span><span class="sxs-lookup"><span data-stu-id="72332-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="72332-104">偵測先前的驗證程式碼，時發生 hello 精靈偵測到不相容的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="72332-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="72332-105">檢查什麼？</span><span class="sxs-lookup"><span data-stu-id="72332-105">What is being checked?</span></span>
<span data-ttu-id="72332-106">**注意：** toocorrectly 偵測先前的驗證程式碼專案中，必須建置 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="72332-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="72332-107">如果遇到這個錯誤，且您的專案中沒有先前的驗證碼，請重建並再試一次。</span><span class="sxs-lookup"><span data-stu-id="72332-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="72332-108">專案類型</span><span class="sxs-lookup"><span data-stu-id="72332-108">Project Types</span></span>
<span data-ttu-id="72332-109">hello 精靈會檢查您正在開發，它可以將 hello 正確的驗證邏輯插入 hello 專案的專案 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="72332-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="72332-110">如果沒有任何衍生自的控制站`ApiController`hello 專案視為 WebAPI 專案 hello 專案中。</span><span class="sxs-lookup"><span data-stu-id="72332-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="72332-111">如果沒有衍生自的控制器`MVC.Controller`hello 專案視為 MVC 專案 hello 專案中。</span><span class="sxs-lookup"><span data-stu-id="72332-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="72332-112">Hello 精靈不支援任何其他項目。</span><span class="sxs-lookup"><span data-stu-id="72332-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="72332-113">相容的驗證碼</span><span class="sxs-lookup"><span data-stu-id="72332-113">Compatible Authentication Code</span></span>
<span data-ttu-id="72332-114">hello 精靈也會檢查的先前設定使用 hello 精靈或 hello 精靈與相容的驗證設定。</span><span class="sxs-lookup"><span data-stu-id="72332-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="72332-115">如果所有設定都都存在，就會被視為可重新進入的情況下，，和 hello 精靈隨即開啟顯示 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="72332-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="72332-116">如果只有部分 hello 設定存在，則會視為錯誤案例。</span><span class="sxs-lookup"><span data-stu-id="72332-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="72332-117">在 MVC 專案中，hello 精靈會檢查任何 hello 遵循因 hello 精靈的先前使用的設定：</span><span class="sxs-lookup"><span data-stu-id="72332-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="72332-118">此外，hello 精靈會檢查任何 hello 下列 Web API 專案時，源自 hello 精靈的先前使用的設定：</span><span class="sxs-lookup"><span data-stu-id="72332-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="72332-119">不相容的驗證碼</span><span class="sxs-lookup"><span data-stu-id="72332-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="72332-120">最後，hello 精靈會嘗試驗證程式碼的已使用舊版 Visual Studio 的 toodetect 版本。</span><span class="sxs-lookup"><span data-stu-id="72332-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="72332-121">如果收到此錯誤，表示您的專案包含不相容的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="72332-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="72332-122">hello 精靈偵測到舊版的 Visual Studio 中的下列類型的驗證 hello:</span><span class="sxs-lookup"><span data-stu-id="72332-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="72332-123">Windows 驗證</span><span class="sxs-lookup"><span data-stu-id="72332-123">Windows Authentication</span></span> 
* <span data-ttu-id="72332-124">個別使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="72332-124">Individual User Accounts</span></span> 
* <span data-ttu-id="72332-125">組織帳戶</span><span class="sxs-lookup"><span data-stu-id="72332-125">Organizational Accounts</span></span> 

<span data-ttu-id="72332-126">toodetect MVC 專案中的 Windows 驗證，hello 精靈會尋找 hello`authentication`項目從您**web.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="72332-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="72332-127">在 Web API 專案 toodetect Windows 驗證 hello 精靈會尋找 hello`IISExpressWindowsAuthentication`從您的專案項目**.csproj**檔案：</span><span class="sxs-lookup"><span data-stu-id="72332-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="72332-128">toodetect 個別使用者帳戶驗證，hello 精靈會尋找 hello 封裝元素，從您**Packages.config**檔案。</span><span class="sxs-lookup"><span data-stu-id="72332-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="72332-129">toodetect 是舊的組織帳戶驗證形式，hello 精靈會檢查下列項目從 hello **web.config**:</span><span class="sxs-lookup"><span data-stu-id="72332-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="72332-130">toochange hello 的驗證類型，移除 hello 不相容的驗證類型，然後再次執行 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="72332-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="72332-131">如需詳細資訊，請參閱 [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="72332-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="72332-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72332-132">Next steps</span></span>
- [<span data-ttu-id="72332-133">Azure AD 的驗證案例</span><span class="sxs-lookup"><span data-stu-id="72332-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)