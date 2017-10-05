---
title: "Azure AD v2 ASP.NET Web 伺服器快速入門 - 測試 | Microsoft Docs"
description: "使用 OpenID Connect 標準，搭配傳統網頁瀏覽器型應用程式，在 ASP.NET 方案上實作 Microsoft 登入"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="e9f86-103">測試您的程式碼</span><span class="sxs-lookup"><span data-stu-id="e9f86-103">Test your code</span></span>

<span data-ttu-id="e9f86-104">按 `F5` 以在 Visual Studio 中執行您的專案。</span><span class="sxs-lookup"><span data-stu-id="e9f86-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="e9f86-105">瀏覽器將會開啟並將您導向至 *http://localhost:{port}*，其中會顯示 [使用 Microsoft 登入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e9f86-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="e9f86-106">接著請按一下該按鈕來登入。</span><span class="sxs-lookup"><span data-stu-id="e9f86-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="e9f86-107">當您準備好進行測試時，請使用公司或學校 (Azure Active Directory)，或個人 (live.com、outlook.com) 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="e9f86-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![[使用 Microsoft 登入] 瀏覽器視窗](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![[使用 Microsoft 登入] 瀏覽器視窗](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="e9f86-110">預期的結果</span><span class="sxs-lookup"><span data-stu-id="e9f86-110">Expected results</span></span>
<span data-ttu-id="e9f86-111">登入之後，系統會將使用者重新導向至您網站的首頁，也就是您在 Microsoft 應用程式註冊入口網站中在應用程式註冊資訊中指定的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="e9f86-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="e9f86-112">此網頁現在會顯示「{使用者} 您好」 和一個登出連結，以及一個用於查看使用者宣告的連結 (這是之前所建立之授權控制器的連結)。</span><span class="sxs-lookup"><span data-stu-id="e9f86-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="e9f86-113">查看使用者的宣告</span><span class="sxs-lookup"><span data-stu-id="e9f86-113">See user's claims</span></span>
<span data-ttu-id="e9f86-114">選取超連結來查看使用者的宣告。</span><span class="sxs-lookup"><span data-stu-id="e9f86-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="e9f86-115">這會帶您前往只會向已驗證使用者提供的控制器和檢視。</span><span class="sxs-lookup"><span data-stu-id="e9f86-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="e9f86-116">預期的結果</span><span class="sxs-lookup"><span data-stu-id="e9f86-116">Expected results</span></span>
 <span data-ttu-id="e9f86-117">您應該會看到一個表格，其中包含已登入使用者的基本屬性：</span><span class="sxs-lookup"><span data-stu-id="e9f86-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="e9f86-118">屬性</span><span class="sxs-lookup"><span data-stu-id="e9f86-118">Property</span></span> | <span data-ttu-id="e9f86-119">值</span><span class="sxs-lookup"><span data-stu-id="e9f86-119">Value</span></span> | <span data-ttu-id="e9f86-120">描述</span><span class="sxs-lookup"><span data-stu-id="e9f86-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="e9f86-121">名稱</span><span class="sxs-lookup"><span data-stu-id="e9f86-121">Name</span></span> | <span data-ttu-id="e9f86-122">{使用者完整名稱}</span><span class="sxs-lookup"><span data-stu-id="e9f86-122">{User Full Name}</span></span> | <span data-ttu-id="e9f86-123">使用者的名字和姓氏</span><span class="sxs-lookup"><span data-stu-id="e9f86-123">The user’s first and last name</span></span>
|<span data-ttu-id="e9f86-124">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="e9f86-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="e9f86-125">用來識別已登入使用者的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="e9f86-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="e9f86-126">主體</span><span class="sxs-lookup"><span data-stu-id="e9f86-126">Subject</span></span>| <span data-ttu-id="e9f86-127">{主體}</span><span class="sxs-lookup"><span data-stu-id="e9f86-127">{Subject}</span></span>|<span data-ttu-id="e9f86-128">用來跨網站唯一識別使用者登入的字串</span><span class="sxs-lookup"><span data-stu-id="e9f86-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="e9f86-129">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e9f86-129">Tenant ID</span></span>| <span data-ttu-id="e9f86-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="e9f86-130">{Guid}</span></span>| <span data-ttu-id="e9f86-131">唯一代表使用者之 Azure Active Directory 組織的 *guid*。</span><span class="sxs-lookup"><span data-stu-id="e9f86-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="e9f86-132">此外，您也會看到一個表格，其中包含驗證要求中包括的所有使用者宣告。</span><span class="sxs-lookup"><span data-stu-id="e9f86-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="e9f86-133">如需識別碼權杖中所有宣告的清單和說明，請參閱這篇[文章]：(https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "識別碼權杖的宣告清單")。</span><span class="sxs-lookup"><span data-stu-id="e9f86-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="e9f86-134">對具有 *[Authorize]* 屬性 (選用) 的方法進行存取測試</span><span class="sxs-lookup"><span data-stu-id="e9f86-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="e9f86-135">在這個步驟中，您將會以匿名使用者的身分對已驗證的控制器進行存取測試：</span><span class="sxs-lookup"><span data-stu-id="e9f86-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="e9f86-136">選取連結以將使用者登出，並完成登出程序。</span><span class="sxs-lookup"><span data-stu-id="e9f86-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="e9f86-137">現在在您的瀏覽器中輸入 http://localhost:{port}/authenticated 來存取您使用 `[Authorize]` 屬性保護的控制器</span><span class="sxs-lookup"><span data-stu-id="e9f86-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="e9f86-138">預期的結果</span><span class="sxs-lookup"><span data-stu-id="e9f86-138">Expected results</span></span>
<span data-ttu-id="e9f86-139">您應該會收到提示，要求您進行驗證以查看檢視。</span><span class="sxs-lookup"><span data-stu-id="e9f86-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="e9f86-140">其他資訊</span><span class="sxs-lookup"><span data-stu-id="e9f86-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="e9f86-141">保護您的整個網站</span><span class="sxs-lookup"><span data-stu-id="e9f86-141">Protect your entire web site</span></span>
<span data-ttu-id="e9f86-142">若要保護您的整個網站，請將 `AuthorizeAttribute` 新增至 `Global.asax` `Application_Start` 方法中的 `GlobalFilters`：</span><span class="sxs-lookup"><span data-stu-id="e9f86-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="e9f86-143">**如何只將來自一個組織的使用者限制為登入您的應用程式**</span><span class="sxs-lookup"><span data-stu-id="e9f86-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="e9f86-144">根據預設值，下列帳戶可以登入您的應用程式：個人帳戶 (包括 outlook.com、live.com 和其他帳戶)，以及來自已經整合 Azure Active Directory 之公司或組織的公司與學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9f86-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="e9f86-145">如果您想要讓應用程式只接受來自某一個 Azure Active Directory 組織的登入，請將 *web.config* 中的 `Tenant` 參數從 `Common` 取代為組織的租用戶名稱 (例如 *contoso.onmicrosoft.com*)。</span><span class="sxs-lookup"><span data-stu-id="e9f86-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="e9f86-146">完成之後，請將您 [OWIN 啟動類別] 中的 `ValidateIssuer` 引數變更為 `true`。</span><span class="sxs-lookup"><span data-stu-id="e9f86-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="e9f86-147">若只要允許來自某一特定組織清單的使用者登入，請將 `ValidateIssuer` 設定為 true 並使用 `ValidIssuers` 參數指定組織清單。</span><span class="sxs-lookup"><span data-stu-id="e9f86-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="e9f86-148">另一個選項是實作自訂方法，使用 IssuerValidator 參數驗證簽發者。</span><span class="sxs-lookup"><span data-stu-id="e9f86-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="e9f86-149">如需 `TokenValidationParameters` 的詳細資訊，請參閱[這篇 ](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN 文章") MSDN 文章。</span><span class="sxs-lookup"><span data-stu-id="e9f86-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

