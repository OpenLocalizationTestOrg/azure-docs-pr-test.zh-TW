---
title: "開始使用 Azure AD AngularJS | Microsoft Docs"
description: "如何建置 AngularJS 單一頁面應用程式來與 Azure AD 整合進行登入，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
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
ms.openlocfilehash: 4153910bc03f112f84c26cda6f9c78f11028b934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="e61b6-103">使用 Azure AD 保護 AngularJS 單一頁面應用程式</span><span class="sxs-lookup"><span data-stu-id="e61b6-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="e61b6-104">Azure Active Directory (Azure AD) 可讓您簡單又直截了當地新增登入、登出，並保護對單一頁面應用程式的 OAuth API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="e61b6-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="e61b6-105">它也可讓您的應用程式以使用者的 Windows Server Active Directory 帳戶來驗證使用者，並取用 Azure AD 保護的任何 Web API，例如 Office 365 API 或 Azure API。</span><span class="sxs-lookup"><span data-stu-id="e61b6-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="e61b6-106">對於在瀏覽器中執行的 JavaScript 應用程式，Azure AD 提供 Active Directory 驗證程式庫 (ADAL)，又稱為 adal.js。</span><span class="sxs-lookup"><span data-stu-id="e61b6-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="e61b6-107">adal.js 的唯一目的是為了讓您的應用程式輕鬆取得存取權杖。</span><span class="sxs-lookup"><span data-stu-id="e61b6-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="e61b6-108">為了示範究竟多麼簡單，我們將建置一個執行下列動作的 AngularJS 待辦事項清單應用程式：</span><span class="sxs-lookup"><span data-stu-id="e61b6-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="e61b6-109">使用 Azure AD 做為身分識別提供者，將使用者登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="e61b6-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="e61b6-110">顯示使用者的一些相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e61b6-110">Displays some information about the user.</span></span>
* <span data-ttu-id="e61b6-111">使用 Azure AD 簽發的持有人權杖，安全地呼叫應用程式的待辦事項清單 API。</span><span class="sxs-lookup"><span data-stu-id="e61b6-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="e61b6-112">將使用者登出應用程式。</span><span class="sxs-lookup"><span data-stu-id="e61b6-112">Signs the user out of the app.</span></span>

<span data-ttu-id="e61b6-113">若要建立可完整運作的應用程式，您必須：</span><span class="sxs-lookup"><span data-stu-id="e61b6-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="e61b6-114">向 Azure AD 註冊應用程式.</span><span class="sxs-lookup"><span data-stu-id="e61b6-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="e61b6-115">安裝 ADAL 並設定單一頁面應用程式。</span><span class="sxs-lookup"><span data-stu-id="e61b6-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="e61b6-116">使用 ADAL 來保護單一頁面應用程式中的頁面。</span><span class="sxs-lookup"><span data-stu-id="e61b6-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="e61b6-117">若要開始使用，請[下載應用程式基本架構](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip)或[下載完整的範例](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="e61b6-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="e61b6-118">您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e61b6-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="e61b6-119">如果您還沒有租用戶， [了解如何取得租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="e61b6-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="e61b6-120">步驟 1：註冊 DirectorySearcher 應用程式</span><span class="sxs-lookup"><span data-stu-id="e61b6-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="e61b6-121">若要讓應用程式能夠驗證使用者並取得權杖，您必須先在 Azure AD 租用戶中註冊這個應用程式：</span><span class="sxs-lookup"><span data-stu-id="e61b6-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="e61b6-122">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e61b6-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e61b6-123">如果登入多個目錄，您可能需要確定檢視正確的目錄。</span><span class="sxs-lookup"><span data-stu-id="e61b6-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="e61b6-124">若要這樣做，請在頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e61b6-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="e61b6-125">在 [目錄] 清單下，選擇您要註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e61b6-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="e61b6-126">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="e61b6-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="e61b6-127">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e61b6-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="e61b6-128">遵照提示進行，並建立新的 Web 應用程式和/或 Web API：</span><span class="sxs-lookup"><span data-stu-id="e61b6-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="e61b6-129">**名稱**向使用者描述您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e61b6-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="e61b6-130">**重新導向 URI** 是供 Azure AD 傳回權杖的位置。</span><span class="sxs-lookup"><span data-stu-id="e61b6-130">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="e61b6-131">此範例中的預設位置是 `https://localhost:44326/`。</span><span class="sxs-lookup"><span data-stu-id="e61b6-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="e61b6-132">完成註冊之後，Azure AD 會指派唯一的應用程式識別碼給您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e61b6-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="e61b6-133">您會在後續小節中用到這個值，所以請從應用程式索引標籤中複製此值。</span><span class="sxs-lookup"><span data-stu-id="e61b6-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="e61b6-134">Adal.js 會使用 OAuth 隱含流程來與 Azure AD 通訊。</span><span class="sxs-lookup"><span data-stu-id="e61b6-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="e61b6-135">您必須為您的應用程式啟用隱含流程：</span><span class="sxs-lookup"><span data-stu-id="e61b6-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="e61b6-136">按一下應用程式，選取 [資訊清單] 以開啟內嵌資訊清單編輯器。</span><span class="sxs-lookup"><span data-stu-id="e61b6-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="e61b6-137">找出 `oauth2AllowImplicitFlow` 屬性。</span><span class="sxs-lookup"><span data-stu-id="e61b6-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="e61b6-138">將值設為 `true`。</span><span class="sxs-lookup"><span data-stu-id="e61b6-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="e61b6-139">按一下 [儲存]  以儲存資訊清單。</span><span class="sxs-lookup"><span data-stu-id="e61b6-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="e61b6-140">在您的應用程式租用戶上授予權限。</span><span class="sxs-lookup"><span data-stu-id="e61b6-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="e61b6-141">前往 [設定]  >  [屬性]  >  [必要的權限]，並按一下頂端列中的 [授與權限] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e61b6-141">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="e61b6-142">按一下 [ **是** ] 以確認。</span><span class="sxs-lookup"><span data-stu-id="e61b6-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="e61b6-143">步驟 2︰安裝 ADAL 並設定單一頁面應用程式</span><span class="sxs-lookup"><span data-stu-id="e61b6-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="e61b6-144">既然您在 Azure AD 中已有應用程式，您可以安裝 adal.js，並撰寫身分識別相關的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e61b6-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="e61b6-145">設定 JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="e61b6-145">Configure the JavaScript client</span></span>
<span data-ttu-id="e61b6-146">首先，使用 [套件管理主控台] 將 adal.js 新增至 TodoSPA 專案：</span><span class="sxs-lookup"><span data-stu-id="e61b6-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="e61b6-147">下載 [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) 並將它新增至 `App/Scripts/` 專案目錄。</span><span class="sxs-lookup"><span data-stu-id="e61b6-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="e61b6-148">下載 [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) 並將它新增至 `App/Scripts/` 專案目錄。</span><span class="sxs-lookup"><span data-stu-id="e61b6-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="e61b6-149">在 `index.html` 中的 `</body>` 結尾之前，載入每個指令碼：</span><span class="sxs-lookup"><span data-stu-id="e61b6-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="e61b6-150">設定後端伺服器</span><span class="sxs-lookup"><span data-stu-id="e61b6-150">Configure the back end server</span></span>
<span data-ttu-id="e61b6-151">為了讓單一頁面應用程式的後端待辦事項清單 API 從瀏覽器接受權杖，後端需要應用程式註冊的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="e61b6-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="e61b6-152">在 TodoSPA 專案中，開啟 `web.config`。</span><span class="sxs-lookup"><span data-stu-id="e61b6-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="e61b6-153">取代 `<appSettings>` 區段中的元素值，以反映您在 Azure 入口網站中所使用的值。</span><span class="sxs-lookup"><span data-stu-id="e61b6-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="e61b6-154">每當使用 ADAL 時，您的程式碼便會參考這些值。</span><span class="sxs-lookup"><span data-stu-id="e61b6-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="e61b6-155">`ida:Tenant` 是指您的 Azure AD 租用戶網域，例如 contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="e61b6-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="e61b6-156">`ida:Audience` 是您從入口網站複製的應用程式用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="e61b6-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="e61b6-157">步驟 3︰使用 ADAL 來保護單一頁面應用程式中的頁面</span><span class="sxs-lookup"><span data-stu-id="e61b6-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="e61b6-158">adal.js 與 AngularJS 路由和 HTTP 提供者整合，因此您可以保護單一頁面應用程式中的個別檢視。</span><span class="sxs-lookup"><span data-stu-id="e61b6-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="e61b6-159">在 `App/Scripts/app.js` 中，載入 adal.js 模組：</span><span class="sxs-lookup"><span data-stu-id="e61b6-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="e61b6-160">使用應用程式註冊的組態值將 `adalProvider` 初始化 (也在 `App/Scripts/app.js` 中)：</span><span class="sxs-lookup"><span data-stu-id="e61b6-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="e61b6-161">只需要一行程式碼 - `requireADLogin`，就能保護應用程式中的 `TodoList` 檢視。</span><span class="sxs-lookup"><span data-stu-id="e61b6-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="e61b6-162">摘要</span><span class="sxs-lookup"><span data-stu-id="e61b6-162">Summary</span></span>
<span data-ttu-id="e61b6-163">您現在有了一個安全的單一頁面應用程式，能夠將使用者登入，並將以持有人權杖保護的要求發給其後端 API。</span><span class="sxs-lookup"><span data-stu-id="e61b6-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="e61b6-164">當使用者按一下 **TodoList** 連結時，需要的話，adal.js 會自動重新導向至 Azure AD 進行登入。</span><span class="sxs-lookup"><span data-stu-id="e61b6-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="e61b6-165">此外，adal.js 將會自動將 access_token 附加至任何傳送至應用程式後端的 Ajax 要求。</span><span class="sxs-lookup"><span data-stu-id="e61b6-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="e61b6-166">前述步驟是使用 adal.js 建置單一頁面應用程式的最低必要程序。</span><span class="sxs-lookup"><span data-stu-id="e61b6-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="e61b6-167">但單一頁面應用程式中還有其他幾項很有用的功能︰</span><span class="sxs-lookup"><span data-stu-id="e61b6-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="e61b6-168">若要明確發出登入和登出要求，您可以在控制器中定義函式來叫用 adal.js。</span><span class="sxs-lookup"><span data-stu-id="e61b6-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="e61b6-169">在 `App/Scripts/homeCtrl.js`中：</span><span class="sxs-lookup"><span data-stu-id="e61b6-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="e61b6-170">您可以在應用程式的 UI 中顯示使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="e61b6-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="e61b6-171">ADAL 服務已經加入 `userDataCtrl` 控制器，您現在可以在相關聯檢視 `App/Views/UserData.html` 中存取 `userInfo` 物件：</span><span class="sxs-lookup"><span data-stu-id="e61b6-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="e61b6-172">在許多情況下，您也可能想知道使用者是否已登入。</span><span class="sxs-lookup"><span data-stu-id="e61b6-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="e61b6-173">您也可以使用 `userInfo` 物件來收集此資訊。</span><span class="sxs-lookup"><span data-stu-id="e61b6-173">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="e61b6-174">例如，在 `index.html` 中，您可以根據驗證狀態顯示 [登入] 或 [登出] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="e61b6-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="e61b6-175">您的已整合 Azure AD 的單一頁面應用程式可以驗證使用者、使用 OAuth 2.0 安全地呼叫其後端，以及取得使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="e61b6-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="e61b6-176">如果您還沒有這麼做，現在是將一些使用者植入租用戶的時候。</span><span class="sxs-lookup"><span data-stu-id="e61b6-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="e61b6-177">執行待辦事項清單單一頁面應用程式，並使用其中一個使用者登入。</span><span class="sxs-lookup"><span data-stu-id="e61b6-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="e61b6-178">將工作新增至使用者的待辦事項清單、登出，再重新登入。</span><span class="sxs-lookup"><span data-stu-id="e61b6-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="e61b6-179">adal.js 可讓您輕鬆地將常見的身分識別功能納入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e61b6-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="e61b6-180">它會為您處理一切麻煩的事：快取管理、OAuth 通訊協定支援、向使用者顯示登入 UI、重新整理過期權杖等等。</span><span class="sxs-lookup"><span data-stu-id="e61b6-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="e61b6-181">[GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip) 中有完整的範例供您參考 (不含您的組態值)。</span><span class="sxs-lookup"><span data-stu-id="e61b6-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e61b6-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e61b6-182">Next steps</span></span>
<span data-ttu-id="e61b6-183">您現在可以繼續探索其他案例。</span><span class="sxs-lookup"><span data-stu-id="e61b6-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="e61b6-184">您可以嘗試︰[從單一頁面應用程式呼叫 CORS Web API](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet)。</span><span class="sxs-lookup"><span data-stu-id="e61b6-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
