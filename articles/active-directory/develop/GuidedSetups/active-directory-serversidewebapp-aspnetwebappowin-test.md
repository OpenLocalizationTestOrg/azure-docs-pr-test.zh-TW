---
title: "aaaAzure AD v2 ASP.NET Web 伺服器快速入門-測試 |Microsoft 文件"
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
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="2c752-103">測試您的程式碼</span><span class="sxs-lookup"><span data-stu-id="2c752-103">Test your code</span></span>

<span data-ttu-id="2c752-104">按`F5`toorun Visual Studio 中的專案。</span><span class="sxs-lookup"><span data-stu-id="2c752-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="2c752-105">hello 瀏覽器會開啟並引導您太*http://localhost: {port}* ，您會看到 hello*使用 Microsoft 登入* 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2c752-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="2c752-106">請繼續進行，然後按一下它 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="2c752-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="2c752-107">當您準備好 tootest，使用工作或學校 (Azure Active Directory) 或個人 （live.com、 outlook.com） 帳戶 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="2c752-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![[使用 Microsoft 登入] 瀏覽器視窗](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![[使用 Microsoft 登入] 瀏覽器視窗](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="2c752-110">預期的結果</span><span class="sxs-lookup"><span data-stu-id="2c752-110">Expected results</span></span>
<span data-ttu-id="2c752-111">登入之後 hello 使用者是網站的您，也就是網站的 hello hello Microsoft 應用程式註冊入口網站中您的應用程式的註冊資訊中所指定的 HTTPS URL 重新導向的 toohello 首頁。</span><span class="sxs-lookup"><span data-stu-id="2c752-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="2c752-112">此頁面現在會顯示*Hello {User}*和連結 toosign 外，以及連結 toosee hello 使用者宣告 – 這是連結 toohello 授權控制站之前建立。</span><span class="sxs-lookup"><span data-stu-id="2c752-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="2c752-113">查看使用者的宣告</span><span class="sxs-lookup"><span data-stu-id="2c752-113">See user's claims</span></span>
<span data-ttu-id="2c752-114">選取 hello 超連結 toosee hello 使用者的宣告。</span><span class="sxs-lookup"><span data-stu-id="2c752-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="2c752-115">這會導致您 toohello 控制器和檢視才會進行驗證的可用 toousers。</span><span class="sxs-lookup"><span data-stu-id="2c752-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="2c752-116">預期的結果</span><span class="sxs-lookup"><span data-stu-id="2c752-116">Expected results</span></span>
 <span data-ttu-id="2c752-117">您應該會看到包含 hello 的 hello 登入使用者的基本屬性的資料表：</span><span class="sxs-lookup"><span data-stu-id="2c752-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="2c752-118">屬性</span><span class="sxs-lookup"><span data-stu-id="2c752-118">Property</span></span> | <span data-ttu-id="2c752-119">值</span><span class="sxs-lookup"><span data-stu-id="2c752-119">Value</span></span> | <span data-ttu-id="2c752-120">描述</span><span class="sxs-lookup"><span data-stu-id="2c752-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="2c752-121">名稱</span><span class="sxs-lookup"><span data-stu-id="2c752-121">Name</span></span> | <span data-ttu-id="2c752-122">{使用者完整名稱}</span><span class="sxs-lookup"><span data-stu-id="2c752-122">{User Full Name}</span></span> | <span data-ttu-id="2c752-123">hello 使用者的名字和姓氏</span><span class="sxs-lookup"><span data-stu-id="2c752-123">hello user’s first and last name</span></span>
|<span data-ttu-id="2c752-124">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="2c752-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="2c752-125">用 tooidentify hello 登入使用者的 hello 使用者名稱</span><span class="sxs-lookup"><span data-stu-id="2c752-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="2c752-126">主旨</span><span class="sxs-lookup"><span data-stu-id="2c752-126">Subject</span></span>| <span data-ttu-id="2c752-127">{主體}</span><span class="sxs-lookup"><span data-stu-id="2c752-127">{Subject}</span></span>|<span data-ttu-id="2c752-128">字串 toouniquely hello web 識別 hello 使用者登入</span><span class="sxs-lookup"><span data-stu-id="2c752-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="2c752-129">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="2c752-129">Tenant ID</span></span>| <span data-ttu-id="2c752-130">{Guid}</span><span class="sxs-lookup"><span data-stu-id="2c752-130">{Guid}</span></span>| <span data-ttu-id="2c752-131">A *guid* toouniquely 代表 hello 使用者的 Azure Active Directory 組織。</span><span class="sxs-lookup"><span data-stu-id="2c752-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="2c752-132">此外，您也會看到一個表格，其中包含驗證要求中包括的所有使用者宣告。</span><span class="sxs-lookup"><span data-stu-id="2c752-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="2c752-133">如需識別碼權杖中所有宣告的清單和說明，請參閱這篇[文章]：(https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "識別碼權杖的宣告清單")。</span><span class="sxs-lookup"><span data-stu-id="2c752-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="2c752-134">對具有 *[Authorize]* 屬性 (選用) 的方法進行存取測試</span><span class="sxs-lookup"><span data-stu-id="2c752-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="2c752-135">在此步驟中，您將測試存取 hello 驗證控制器匿名使用者的身分：</span><span class="sxs-lookup"><span data-stu-id="2c752-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="2c752-136">選取 hello 連結 toosign 外 hello 使用者和 hello 完成登出程序。</span><span class="sxs-lookup"><span data-stu-id="2c752-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="2c752-137">現在您的瀏覽器中輸入 http://localhost: {port} / 驗證 tooaccess 您 hello 受保護的控制器`[Authorize]`屬性</span><span class="sxs-lookup"><span data-stu-id="2c752-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="2c752-138">預期的結果</span><span class="sxs-lookup"><span data-stu-id="2c752-138">Expected results</span></span>
<span data-ttu-id="2c752-139">您應該會收到 hello 提示要求您 tooauthenticate toosee hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="2c752-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="2c752-140">其他資訊</span><span class="sxs-lookup"><span data-stu-id="2c752-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="2c752-141">保護您的整個網站</span><span class="sxs-lookup"><span data-stu-id="2c752-141">Protect your entire web site</span></span>
<span data-ttu-id="2c752-142">tooprotect 整個網站，新增 hello`AuthorizeAttribute`太`GlobalFilters`中`Global.asax``Application_Start`方法：</span><span class="sxs-lookup"><span data-stu-id="2c752-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="2c752-143">**如何從 tooyour 應用程式中只能有一個組織 toosign toorestrict 使用者**</span><span class="sxs-lookup"><span data-stu-id="2c752-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="2c752-144">根據預設，個人帳戶 （包括 outlook.com、 live.com 和其他項目），以及從任何的公司或組織與 Azure Active Directory 整合的公司及學校帳戶可以登入 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c752-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="2c752-145">如果您希望您的應用程式 tooaccept 登入從只有一個 Azure Active Directory 組織，取代 hello`Tenant`中的參數*web.config*從`Common`hello 組織 – toohello 租用戶名稱範例中，*contoso.onmicrosoft.com*。在這之後，變更 hello`ValidateIssuer`引數中的您*OWIN 啟動 「 類別*太`true`。</span><span class="sxs-lookup"><span data-stu-id="2c752-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="2c752-146">tooallow 一份特定組織，使用者設定`ValidateIssuer`tootrue 並用 hello`ValidIssuers`參數 toospecify 組織的清單。</span><span class="sxs-lookup"><span data-stu-id="2c752-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="2c752-147">另一個選項是使用 IssuerValidator 參數 toovalidate hello 簽發者 tooimplement 的自訂方法。</span><span class="sxs-lookup"><span data-stu-id="2c752-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="2c752-148">如需 `TokenValidationParameters` 的詳細資訊，請參閱[這篇 ](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN 文章") MSDN 文章。</span><span class="sxs-lookup"><span data-stu-id="2c752-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

