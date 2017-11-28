---
title: "開始使用 AD AngularJS aaaAzure |Microsoft 文件"
description: "如何 toobuild AngularJS 單一頁面應用程式的整合 Azure AD 進行登入及使用 OAuth 呼叫 Azure AD 保護應用程式開發介面。"
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="4e709-103">使用 Azure AD 保護 AngularJS 單一頁面應用程式</span><span class="sxs-lookup"><span data-stu-id="4e709-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="4e709-104">Azure Active Directory (Azure AD) 可讓簡單又直接的您 tooadd 登入、 登出，並安全 OAuth 應用程式開發介面呼叫 tooyour 單一頁面應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e709-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="4e709-105">它可讓您的應用程式 tooauthenticate 使用者與他們的 Windows Server Active Directory 帳戶，並使用任何 web API，Azure AD 可協助保護，例如 Office 365 Api hello 或 hello Azure API。</span><span class="sxs-lookup"><span data-stu-id="4e709-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="4e709-106">對於瀏覽器中執行的 JavaScript 應用程式，Azure AD 提供 hello Active Directory 驗證程式庫 (ADAL) 或 adal.js。</span><span class="sxs-lookup"><span data-stu-id="4e709-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="4e709-107">adal.js hello 唯一目的是 toomake 輕鬆的應用程式 tooget 存取語彙基元。</span><span class="sxs-lookup"><span data-stu-id="4e709-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="4e709-108">toodemonstrate 多麼容易，所以這裡，我們將建立 AngularJS tooDo 清單應用程式的：</span><span class="sxs-lookup"><span data-stu-id="4e709-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="4e709-109">符號 hello toohello 應用程式中的使用者利用 Azure AD 作為 hello 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="4e709-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="4e709-110">顯示 hello 使用者的一些資訊。</span><span class="sxs-lookup"><span data-stu-id="4e709-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="4e709-111">安全地呼叫 hello 應用程式的 tooDo 清單應用程式開發介面使用從 Azure AD 的持有者權杖。</span><span class="sxs-lookup"><span data-stu-id="4e709-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="4e709-112">符號 hello 使用者登出 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e709-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="4e709-113">toobuild hello 完成之後，使用應用程式，您需要：</span><span class="sxs-lookup"><span data-stu-id="4e709-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="4e709-114">向 Azure AD 註冊應用程式.</span><span class="sxs-lookup"><span data-stu-id="4e709-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="4e709-115">安裝 ADAL 和設定 hello 單一頁面應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e709-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="4e709-116">Hello 單一頁面應用程式中使用 ADAL toohelp 安全的網頁。</span><span class="sxs-lookup"><span data-stu-id="4e709-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="4e709-117">啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="4e709-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="4e709-118">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4e709-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="4e709-119">如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="4e709-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="4e709-120">步驟 1： 註冊 hello DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="4e709-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="4e709-121">tooenable 您的應用程式 tooauthenticate 使用者和 get 語彙基元，您必須先在您的 Azure AD 租用戶 tooregister:</span><span class="sxs-lookup"><span data-stu-id="4e709-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="4e709-122">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4e709-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4e709-123">如果您已登入 toomultiple 目錄，您可能需要 tooensure 您正在檢視 hello 正確的目錄。</span><span class="sxs-lookup"><span data-stu-id="4e709-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="4e709-124">toodo，hello 頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e709-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="4e709-125">在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e709-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="4e709-126">按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="4e709-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4e709-127">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4e709-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="4e709-128">請依照 hello 提示，並建立新的 web 應用程式和/或 web API:</span><span class="sxs-lookup"><span data-stu-id="4e709-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="4e709-129">**名稱**描述應用程式 toousers。</span><span class="sxs-lookup"><span data-stu-id="4e709-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="4e709-130">**重新導向 Uri** hello 位置 toowhich Azure AD 將會傳回語彙基元。</span><span class="sxs-lookup"><span data-stu-id="4e709-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="4e709-131">此範例中的 hello 預設位置是`https://localhost:44326/`。</span><span class="sxs-lookup"><span data-stu-id="4e709-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="4e709-132">完成註冊之後，Azure AD 會指派唯一的應用程式識別碼 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e709-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="4e709-133">您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4e709-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="4e709-134">Adal.js 會使用 Azure AD 中的 hello OAuth 隱含流程 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="4e709-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="4e709-135">您的應用程式，您必須啟用 hello 隱含流程：</span><span class="sxs-lookup"><span data-stu-id="4e709-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="4e709-136">按一下 hello 應用程式，然後選取**資訊清單**tooopen hello 內嵌資訊清單編輯器。</span><span class="sxs-lookup"><span data-stu-id="4e709-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="4e709-137">找出 hello`oauth2AllowImplicitFlow`屬性。</span><span class="sxs-lookup"><span data-stu-id="4e709-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="4e709-138">將其值設定為太`true`。</span><span class="sxs-lookup"><span data-stu-id="4e709-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="4e709-139">按一下**儲存**toosave hello 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="4e709-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="4e709-140">在您的應用程式租用戶上授予權限。</span><span class="sxs-lookup"><span data-stu-id="4e709-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="4e709-141">跳過**設定** > **屬性** > **必要的使用權限**，然後按一下 hello**授與權限**hello 頂端列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4e709-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="4e709-142">按一下**是**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="4e709-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="4e709-143">步驟 2： 安裝 ADAL 及設定 hello 單一頁面應用程式</span><span class="sxs-lookup"><span data-stu-id="4e709-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="4e709-144">既然您在 Azure AD 中已有應用程式，您可以安裝 adal.js，並撰寫身分識別相關的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4e709-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="4e709-145">Hello JavaScript 用戶端設定</span><span class="sxs-lookup"><span data-stu-id="4e709-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="4e709-146">開始使用 Package Manager Console hello 加入 adal.js toohello TodoSPA 專案：</span><span class="sxs-lookup"><span data-stu-id="4e709-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="4e709-147">下載[adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js)並將它加入 toohello`App/Scripts/`專案目錄。</span><span class="sxs-lookup"><span data-stu-id="4e709-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="4e709-148">下載[adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js)並將它加入 toohello`App/Scripts/`專案目錄。</span><span class="sxs-lookup"><span data-stu-id="4e709-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="4e709-149">載入 hello hello 結束之前的每個指令碼`</body>`中`index.html`:</span><span class="sxs-lookup"><span data-stu-id="4e709-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="4e709-150">Hello 後端伺服器設定</span><span class="sxs-lookup"><span data-stu-id="4e709-150">Configure hello back end server</span></span>
<span data-ttu-id="4e709-151">Hello 單一頁面應用程式的後端 tooDo 清單 API tooaccept 語彙基元從 hello 瀏覽器，hello 後端需要 hello 應用程式註冊的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="4e709-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="4e709-152">在 hello TodoSPA 專案中，開啟`web.config`。</span><span class="sxs-lookup"><span data-stu-id="4e709-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="4e709-153">取代 hello 中的項目 hello hello 值`<appSettings>`> 一節中所用 tooreflect hello 值 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4e709-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="4e709-154">每當使用 ADAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="4e709-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="4e709-155">`ida:Tenant`是您的 Azure AD 租用戶-例如 contoso.onmicrosoft.com hello 網域。</span><span class="sxs-lookup"><span data-stu-id="4e709-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="4e709-156">`ida:Audience`這是您所複製的 hello 入口網站應用程式的 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e709-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="4e709-157">Hello 單一頁面應用程式中的步驟 3： 使用 ADAL toohelp 安全頁面</span><span class="sxs-lookup"><span data-stu-id="4e709-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="4e709-158">adal.js 與 AngularJS 路由和 HTTP 提供者整合，因此您可以保護單一頁面應用程式中的個別檢視。</span><span class="sxs-lookup"><span data-stu-id="4e709-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="4e709-159">在`App/Scripts/app.js`，納入 hello adal.js 模組：</span><span class="sxs-lookup"><span data-stu-id="4e709-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="4e709-160">初始化`adalProvider`中也使用您的應用程式註冊 hello 組態值`App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="4e709-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. <span data-ttu-id="4e709-161">協助安全 hello `TodoList` hello 應用程式利用只有一行的程式碼中的檢視： `requireADLogin`。</span><span class="sxs-lookup"><span data-stu-id="4e709-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="4e709-162">摘要</span><span class="sxs-lookup"><span data-stu-id="4e709-162">Summary</span></span>
<span data-ttu-id="4e709-163">現在，您會有安全的單一頁面應用程式可以在使用者登入和發出的持有人權杖保護要求 tooits 後端應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="4e709-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="4e709-164">當使用者按一下 hello **TodoList**連結，adal.js 會自動重新導向 tooAzure AD 登入必要的。</span><span class="sxs-lookup"><span data-stu-id="4e709-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="4e709-165">此外，adal.js 會自動附加存取語彙基元 tooany Ajax 要求傳送 toohello 應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="4e709-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="4e709-166">hello 前面的步驟都 hello 裸機最小必要 toobuild 之單一頁面應用程式使用 adal.js。</span><span class="sxs-lookup"><span data-stu-id="4e709-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="4e709-167">但單一頁面應用程式中還有其他幾項很有用的功能︰</span><span class="sxs-lookup"><span data-stu-id="4e709-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="4e709-168">tooexplicitly 發出登入和登出要求，您可以定義函式中叫用 adal.js 您控制站。</span><span class="sxs-lookup"><span data-stu-id="4e709-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="4e709-169">在 `App/Scripts/homeCtrl.js`中：</span><span class="sxs-lookup"><span data-stu-id="4e709-169">In `App/Scripts/homeCtrl.js`:</span></span>

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* <span data-ttu-id="4e709-170">您可能想 toopresent hello 應用程式的 UI 中的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="4e709-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="4e709-171">hello ADAL 服務已經加入 toohello`userDataCtrl`控制站，以便您可以存取 hello `userInfo` hello 中的物件相關聯的檢視， `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="4e709-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="4e709-172">有許多案例中您會想 tooknow 如果 hello 使用者登入與否。</span><span class="sxs-lookup"><span data-stu-id="4e709-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="4e709-173">您也可以使用 hello`userInfo`物件 toogather 這項資訊。</span><span class="sxs-lookup"><span data-stu-id="4e709-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="4e709-174">例如，在`index.html`，您可以顯示任一 hello**登入**或**登出**根據驗證狀態的按鈕：</span><span class="sxs-lookup"><span data-stu-id="4e709-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="4e709-175">Azure AD 整合單一頁面應用程式可以驗證使用者，安全地使用 OAuth 2.0 中，呼叫它的後端及 hello 使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="4e709-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="4e709-176">如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。</span><span class="sxs-lookup"><span data-stu-id="4e709-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="4e709-177">執行 tooDo 清單單一頁面應用程式，並使用其中一個這些使用者的登入。</span><span class="sxs-lookup"><span data-stu-id="4e709-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="4e709-178">新增工作 toohello 使用者的待辦事項清單、 登出，再重新登入。</span><span class="sxs-lookup"><span data-stu-id="4e709-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="4e709-179">Adal.js 會使它輕鬆 tooincorporate 常見的身分識別功能成為您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e709-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="4e709-180">它會為您的所有 hello dirty 工作負責： 快取管理、 OAuth 通訊協定支援，呈現給 hello 使用者登入 UI，重新整理過期的語彙基元等等。</span><span class="sxs-lookup"><span data-stu-id="4e709-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="4e709-181">參考，完成的 hello 範例 （不含您的組態值） 會提供[GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="4e709-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e709-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e709-182">Next steps</span></span>
<span data-ttu-id="4e709-183">您現在可以移動 tooadditional 案例。</span><span class="sxs-lookup"><span data-stu-id="4e709-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="4e709-184">您可能會想 tootry:[呼叫的單一頁面應用程式從 CORS web API](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="4e709-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
