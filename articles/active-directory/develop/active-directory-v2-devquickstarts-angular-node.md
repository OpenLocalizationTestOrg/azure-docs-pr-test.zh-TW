---
title: "aaaAzure AD v2.0 NodeJS AngularJS 單一頁面應用程式使用者入門 |Microsoft 文件"
description: "如何 toobuild 角度 JS 單一頁面應用程式登入使用者使用個人 Microsoft 帳戶和工作或學校帳戶。"
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="f093e-103">新增登入 tooan AngularJS 單一頁面應用程式： NodeJS</span><span class="sxs-lookup"><span data-stu-id="f093e-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="f093e-104">在本文中，我們會將新增使用電源的 Microsoft 帳戶 tooan AngularJS 應用程式使用 hello Azure Active Directory v2.0 端點登入。</span><span class="sxs-lookup"><span data-stu-id="f093e-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="f093e-105">hello v2.0 端點 tooperform 應用程式中的單一整合可讓您，而且驗證使用者使用個人和工作/學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="f093e-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="f093e-106">這個範例是簡單的待辦事項清單單一頁面應用程式，在後端 REST API 儲存工作、使用 NodeJS 撰寫，並且使用 Azure AD 的 OAuth 持有人權杖進行保護。</span><span class="sxs-lookup"><span data-stu-id="f093e-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="f093e-107">hello AngularJS 應用程式會使用我們的開放原始碼 JavaScript 驗證程式庫[adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello 整個登入程序，並取得呼叫 hello REST API 的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f093e-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="f093e-108">hello 相同的模式可以是套用的 tooauthenticate tooother REST Api，像是 hello [Microsoft Graph](https://graph.microsoft.com)或 hello Azure 資源管理員 Api。</span><span class="sxs-lookup"><span data-stu-id="f093e-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="f093e-109">並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="f093e-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="f093e-110">toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="f093e-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="f093e-111">下載</span><span class="sxs-lookup"><span data-stu-id="f093e-111">Download</span></span>
<span data-ttu-id="f093e-112">您將需要啟動 tooget，toodownload & 安裝[node.js](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="f093e-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="f093e-113">然後您可以複製或 [下載](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) 基本架構應用程式：</span><span class="sxs-lookup"><span data-stu-id="f093e-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="f093e-114">hello 基本架構應用程式包含簡單的 AngularJS 應用程式中，所有 hello 未定案程式碼，但是遺漏之所有 hello 身分識別相關的片段。</span><span class="sxs-lookup"><span data-stu-id="f093e-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="f093e-115">若您不想沿著 toofollow，可改為複製或[下載](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip)hello 完成範例。</span><span class="sxs-lookup"><span data-stu-id="f093e-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="f093e-116">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="f093e-116">Register an app</span></span>
<span data-ttu-id="f093e-117">首先，建立應用程式在 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或請遵循這些[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="f093e-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f093e-118">請確定：</span><span class="sxs-lookup"><span data-stu-id="f093e-118">Make sure to:</span></span>

* <span data-ttu-id="f093e-119">新增 hello **Web**平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f093e-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="f093e-120">輸入正確的 hello**重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="f093e-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="f093e-121">此範例的 hello 預設值是`http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="f093e-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="f093e-122">保留 hello**允許隱含流程**啟用的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f093e-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="f093e-123">複製下 hello**應用程式識別碼**指派的 tooyour 應用程式，您將在稍後需要。</span><span class="sxs-lookup"><span data-stu-id="f093e-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="f093e-124">安裝 adal.js</span><span class="sxs-lookup"><span data-stu-id="f093e-124">Install adal.js</span></span>
<span data-ttu-id="f093e-125">toostart，瀏覽的 tooproject 您下載並安裝 adal.js。</span><span class="sxs-lookup"><span data-stu-id="f093e-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="f093e-126">如果您已安裝 [bower](http://bower.io/) ，您只要執行這個命令即可。</span><span class="sxs-lookup"><span data-stu-id="f093e-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="f093e-127">任何相依性版本不符，只要選擇 hello 更高的版本。</span><span class="sxs-lookup"><span data-stu-id="f093e-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="f093e-128">或者，您可以手動下載 [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) 和 [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js)。</span><span class="sxs-lookup"><span data-stu-id="f093e-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="f093e-129">加入兩個檔案 toohello`app/lib/adal-angular-experimental/dist`目錄。</span><span class="sxs-lookup"><span data-stu-id="f093e-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="f093e-130">現在 hello 專案您慣用的文字在編輯器中開啟，並載入 adal.js 結尾 hello hello 頁面主體：</span><span class="sxs-lookup"><span data-stu-id="f093e-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="f093e-131">設定 hello REST API</span><span class="sxs-lookup"><span data-stu-id="f093e-131">Set up hello REST API</span></span>
<span data-ttu-id="f093e-132">雖然我們正在進行設定，可讓 get hello 後端 REST API 可以運作。</span><span class="sxs-lookup"><span data-stu-id="f093e-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="f093e-133">在命令提示字元中安裝所有的 hello 必要的封裝執行 （請確定您在 hello hello 專案的最上層的目錄）：</span><span class="sxs-lookup"><span data-stu-id="f093e-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="f093e-134">現在開啟`config.js`和取代 hello`audience`值：</span><span class="sxs-lookup"><span data-stu-id="f093e-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="f093e-135">hello REST API 將會使用在收到 hello 角度應用程式的 AJAX 要求此值 toovalidate 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f093e-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="f093e-136">請注意，這個簡單的 REST API 將儲存記憶體中資料-因此每個時間 toostop hello 伺服器，您將會遺失所有先前建立的工作。</span><span class="sxs-lookup"><span data-stu-id="f093e-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="f093e-137">這就是我們要討論 hello REST API 的運作方式的 toospend hello 時間。</span><span class="sxs-lookup"><span data-stu-id="f093e-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="f093e-138">感覺的免費 toopoke hello 程式碼中，但如果您想 toolearn 深入了解保護的 web Api 與 Azure AD，請參閱[本文](active-directory-v2-devquickstarts-node-api.md)。</span><span class="sxs-lookup"><span data-stu-id="f093e-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="f093e-139">將使用者登入</span><span class="sxs-lookup"><span data-stu-id="f093e-139">Sign users in</span></span>
<span data-ttu-id="f093e-140">時間 toowrite 一些識別程式碼。</span><span class="sxs-lookup"><span data-stu-id="f093e-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="f093e-141">您可能已經發現 adal.js 包含 AngularJS 提供者，它運用 Angular 路由機制相當良好。</span><span class="sxs-lookup"><span data-stu-id="f093e-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="f093e-142">啟動新增 hello adal 模組 toohello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f093e-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="f093e-143">您現在可以初始化 hello`adalProvider`以您的應用程式 ID:</span><span class="sxs-lookup"><span data-stu-id="f093e-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="f093e-144">太好，現在 adal.js 具有 hello 的所有資訊需要 toosecure 中您的應用程式並登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="f093e-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="f093e-145">將登入 tooforce 的 hello，應用程式中所有所需的特定路由是一行程式碼：</span><span class="sxs-lookup"><span data-stu-id="f093e-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

<span data-ttu-id="f093e-146">現在當使用者按一下 hello`TodoList`連結，adal.js 會自動重新導向 tooAzure AD 登入必要的。</span><span class="sxs-lookup"><span data-stu-id="f093e-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="f093e-147">您也可以藉由在控制器中叫用 adal.js，明確傳送登入和登出要求：</span><span class="sxs-lookup"><span data-stu-id="f093e-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="f093e-148">顯示使用者資訊</span><span class="sxs-lookup"><span data-stu-id="f093e-148">Display user info</span></span>
<span data-ttu-id="f093e-149">既然 hello 使用者登入，您可能需要 tooaccess hello 登入使用者的驗證資料在應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f093e-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="f093e-150">Adal.js 會公開這項資訊在 hello`userInfo`物件。</span><span class="sxs-lookup"><span data-stu-id="f093e-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="f093e-151">tooaccess 在檢視中，這個物件會先加入 adal.js toohello 根範圍 hello 相對應的控制項：</span><span class="sxs-lookup"><span data-stu-id="f093e-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="f093e-152">然後您可以直接定址 hello`userInfo`在檢視中的物件：</span><span class="sxs-lookup"><span data-stu-id="f093e-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="f093e-153">您也可以使用 hello`userInfo`物件 toodetermine 如果 hello 使用者登入與否。</span><span class="sxs-lookup"><span data-stu-id="f093e-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a><span data-ttu-id="f093e-154">呼叫 hello REST API</span><span class="sxs-lookup"><span data-stu-id="f093e-154">Call hello REST API</span></span>
<span data-ttu-id="f093e-155">最後，它是時間 tooget 某些語彙基元並呼叫 hello REST API toocreate、 讀取、 更新和刪除的工作。</span><span class="sxs-lookup"><span data-stu-id="f093e-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="f093e-156">您知道嗎？</span><span class="sxs-lookup"><span data-stu-id="f093e-156">Well guess what?</span></span>  <span data-ttu-id="f093e-157">您不需要 toodo*事*。</span><span class="sxs-lookup"><span data-stu-id="f093e-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="f093e-158">Adal.js 會自動為您取得、快取和重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="f093e-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="f093e-159">它也會負責的附加 toooutgoing AJAX 要求您傳送 toohello REST API 的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f093e-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="f093e-160">到底是如何運作的呢？</span><span class="sxs-lookup"><span data-stu-id="f093e-160">How exactly does this work?</span></span> <span data-ttu-id="f093e-161">它是所有的感謝您 toohello 魔力[AngularJS 攔截器](https://docs.angularjs.org/api/ng/service/$http)，可讓 adal.js tootransform 傳出和傳入的 http 訊息。</span><span class="sxs-lookup"><span data-stu-id="f093e-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="f093e-162">此外，adal.js 會假設任何要求傳送 toohello 相同的網域為 hello 視窗應該使用適用於語彙基元 hello 相同的應用程式識別碼為 hello AngularJS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f093e-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="f093e-163">這就是為什麼我們使用 hello hello NodeJS REST API 和這兩個 hello 角度的應用程式中的相同應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="f093e-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="f093e-164">當然，您可以覆寫這個行為，並告訴 adal.js tooget 語彙基元的其他 REST Api，如有必要-但這個簡單案例 hello 將進行的預設值。</span><span class="sxs-lookup"><span data-stu-id="f093e-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="f093e-165">以下是示範是多麼的輕鬆 toosend 要求，以從 Azure AD 的承載權杖的程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="f093e-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="f093e-166">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f093e-166">Congratulations!</span></span>  <span data-ttu-id="f093e-167">您的 Azure AD 整合式單一頁面應用程式現在已完成。</span><span class="sxs-lookup"><span data-stu-id="f093e-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="f093e-168">佩服吧！</span><span class="sxs-lookup"><span data-stu-id="f093e-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="f093e-169">它可以驗證使用者、 安全地呼叫它的後端 REST API 使用 OpenID Connect，並取得 hello 使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="f093e-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="f093e-170">預設 hello 方塊中，它可支援具有個人 Microsoft 帳戶或工作/學校帳戶向 Azure AD 的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="f093e-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="f093e-171">試試 hello 應用程式執行：</span><span class="sxs-lookup"><span data-stu-id="f093e-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="f093e-172">在瀏覽器中瀏覽過`http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="f093e-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="f093e-173">使用個人 Microsoft 帳戶或工作/學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="f093e-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="f093e-174">新增工作 toohello 使用者的待辦事項清單，並登出。再試一次登入的 hello 其他類型的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f093e-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="f093e-175">如果您需要 Azure AD 租用戶 toocreate 工作/學校 users，[深入了解如何 tooget 一個這裡](active-directory-howto-tenant.md)（它是免費的）。</span><span class="sxs-lookup"><span data-stu-id="f093e-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="f093e-176">深入了解 hello toocontinue hello v2.0 端點、 head 後 tooour [v2.0 開發人員指南](active-directory-appmodel-v2-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f093e-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="f093e-177">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f093e-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="f093e-178">GitHub 上的 Azure 範例 >></span><span class="sxs-lookup"><span data-stu-id="f093e-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="f093e-179">Stack Overflow 上的 Azure AD >></span><span class="sxs-lookup"><span data-stu-id="f093e-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="f093e-180">[Azure.com 上的 Azure AD 文件 >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="f093e-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="f093e-181">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="f093e-181">Get security updates for our products</span></span>
<span data-ttu-id="f093e-182">我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。</span><span class="sxs-lookup"><span data-stu-id="f093e-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

