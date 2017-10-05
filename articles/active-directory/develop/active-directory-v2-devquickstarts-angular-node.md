---
title: "Azure AD v2.0 NodeJS AngularJS 單一頁面應用程式入門 | Microsoft Docs"
description: "如何建置可在個人 Microsoft 帳戶及工作或學校帳戶登入使用者的 Angular JS 單一頁面應用程式。"
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
ms.openlocfilehash: 0e90171afd9c4c782fbb18375ab2d147497ef442
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---nodejs"></a><span data-ttu-id="8c734-103">將登入新增至 AngularJS 單一頁面應用程式 - NodeJS</span><span class="sxs-lookup"><span data-stu-id="8c734-103">Add sign-in to an AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="8c734-104">在本文中，我們將使用 Azure Active Directory v2.0 端點，將 Microsoft 帳戶登入新增至 AngularJS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c734-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="8c734-105">v2.0 端點可讓您在您的應用程式中執行單一的整合，以及以個人和工作/學校帳戶驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="8c734-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="8c734-106">這個範例是簡單的待辦事項清單單一頁面應用程式，在後端 REST API 儲存工作、使用 NodeJS 撰寫，並且使用 Azure AD 的 OAuth 持有人權杖進行保護。</span><span class="sxs-lookup"><span data-stu-id="8c734-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="8c734-107">AngularJS 應用程式會使用我們的開放原始碼 JavaScript 驗證程式庫 [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) 以處理整個登入程序，並且取得用以呼叫 REST API 的權杖。</span><span class="sxs-lookup"><span data-stu-id="8c734-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="8c734-108">相同的模式可以套用以驗證其他 REST API，例如 [Microsoft Graph](https://graph.microsoft.com) 或 Azure Resource Manager API。</span><span class="sxs-lookup"><span data-stu-id="8c734-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="8c734-109">v2.0 端點並非支援每個 Azure Active Directory 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="8c734-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="8c734-110">如果要判斷是否應該使用 v2.0 端點，請閱讀 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="8c734-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="8c734-111">下載</span><span class="sxs-lookup"><span data-stu-id="8c734-111">Download</span></span>
<span data-ttu-id="8c734-112">若要開始，您必須下載並安裝 [node.js](https://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="8c734-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="8c734-113">然後您可以複製或 [下載](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) 基本架構應用程式：</span><span class="sxs-lookup"><span data-stu-id="8c734-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="8c734-114">基本架構應用程式包含簡單的 AngularJS 應用程式的重複使用程式碼，但是會遺漏所有身分識別相關的部分。</span><span class="sxs-lookup"><span data-stu-id="8c734-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="8c734-115">如果您不想要跟著做，您可以改為複製或 [下載](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) 完成的範例。</span><span class="sxs-lookup"><span data-stu-id="8c734-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="8c734-116">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="8c734-116">Register an app</span></span>
<span data-ttu-id="8c734-117">首先，在[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)中建立應用程式，或者遵循下列[詳細步驟](active-directory-v2-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="8c734-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="8c734-118">請確定：</span><span class="sxs-lookup"><span data-stu-id="8c734-118">Make sure to:</span></span>

* <span data-ttu-id="8c734-119">為您的應用程式新增 **Web** 平台。</span><span class="sxs-lookup"><span data-stu-id="8c734-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="8c734-120">輸入正確的 **重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="8c734-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="8c734-121">此範例的預設值是 `http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="8c734-121">The default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="8c734-122">保留 [允許隱含流程]  核取方塊啟用。</span><span class="sxs-lookup"><span data-stu-id="8c734-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="8c734-123">將指派給您應用程式的「應用程式識別碼」  複製起來，您很快會需要用到這些識別碼。</span><span class="sxs-lookup"><span data-stu-id="8c734-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="8c734-124">安裝 adal.js</span><span class="sxs-lookup"><span data-stu-id="8c734-124">Install adal.js</span></span>
<span data-ttu-id="8c734-125">若要開始，請瀏覽至您下載並安裝 adal.js 的專案。</span><span class="sxs-lookup"><span data-stu-id="8c734-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="8c734-126">如果您已安裝 [bower](http://bower.io/) ，您只要執行這個命令即可。</span><span class="sxs-lookup"><span data-stu-id="8c734-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="8c734-127">對於任何相依性版本不符，請選擇較高的版本。</span><span class="sxs-lookup"><span data-stu-id="8c734-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="8c734-128">或者，您可以手動下載 [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) 和 [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js)。</span><span class="sxs-lookup"><span data-stu-id="8c734-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="8c734-129">將這兩個檔案新增至 `app/lib/adal-angular-experimental/dist` 目錄。</span><span class="sxs-lookup"><span data-stu-id="8c734-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="8c734-130">現在在慣用的文字編輯器中開啟專案，並於頁面本文的結尾載入 adal.js：</span><span class="sxs-lookup"><span data-stu-id="8c734-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="8c734-131">設定 REST API</span><span class="sxs-lookup"><span data-stu-id="8c734-131">Set up the REST API</span></span>
<span data-ttu-id="8c734-132">在我們進行設定的同時，讓後端 REST API 運作。</span><span class="sxs-lookup"><span data-stu-id="8c734-132">While we're setting things up, lets get the backend REST API working.</span></span>  <span data-ttu-id="8c734-133">在命令提示字元中執行下列命令，安裝所有必要的封裝 (請確定您在專案的最上層目錄)：</span><span class="sxs-lookup"><span data-stu-id="8c734-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span></span>

```
npm install
```

<span data-ttu-id="8c734-134">現在開啟 `config.js` 並取代 `audience` 值：</span><span class="sxs-lookup"><span data-stu-id="8c734-134">Now open `config.js` and replace the `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with the Application ID from the registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="8c734-135">REST API 會使用此值來驗證在 AJAX 要求時從 Angular 應用程式收到的權杖。</span><span class="sxs-lookup"><span data-stu-id="8c734-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>  <span data-ttu-id="8c734-136">請注意，這個簡單的 REST API 會將資料儲存在記憶體中 - 因此，每次停止伺服器，您將會遺失所有先前建立的工作。</span><span class="sxs-lookup"><span data-stu-id="8c734-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="8c734-137">這是我們討論 REST API 運作方式所花費的所有時間。</span><span class="sxs-lookup"><span data-stu-id="8c734-137">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="8c734-138">您可以自由摸索程式碼，但是如果您想要深入了解使用 Azure AD 保護 Web API，請參閱 [這篇文章](active-directory-v2-devquickstarts-node-api.md)。</span><span class="sxs-lookup"><span data-stu-id="8c734-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="8c734-139">將使用者登入</span><span class="sxs-lookup"><span data-stu-id="8c734-139">Sign users in</span></span>
<span data-ttu-id="8c734-140">撰寫一些身分識別程式碼。</span><span class="sxs-lookup"><span data-stu-id="8c734-140">Time to write some identity code.</span></span>  <span data-ttu-id="8c734-141">您可能已經發現 adal.js 包含 AngularJS 提供者，它運用 Angular 路由機制相當良好。</span><span class="sxs-lookup"><span data-stu-id="8c734-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="8c734-142">從將 adal 模組新增至應用程式開始：</span><span class="sxs-lookup"><span data-stu-id="8c734-142">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="8c734-143">您現在可以使用您的應用程式識別碼初始化 `adalProvider` ：</span><span class="sxs-lookup"><span data-stu-id="8c734-143">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="8c734-144">太棒了，現在 adal.js 有了保護您的應用程式並且登入使用者所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="8c734-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="8c734-145">若要對應用程式中的特定路由強制登入，它只需要一行程式碼：</span><span class="sxs-lookup"><span data-stu-id="8c734-145">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="8c734-146">現在，當使用者按一下 `TodoList` 連結時，需要的話，adal.js 會自動重新導向至 Azure AD 進行登入。</span><span class="sxs-lookup"><span data-stu-id="8c734-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="8c734-147">您也可以藉由在控制器中叫用 adal.js，明確傳送登入和登出要求：</span><span class="sxs-lookup"><span data-stu-id="8c734-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="8c734-148">顯示使用者資訊</span><span class="sxs-lookup"><span data-stu-id="8c734-148">Display user info</span></span>
<span data-ttu-id="8c734-149">現在使用者已登入，您可能需要存取您的應用程式中已登入使用者的驗證資料。</span><span class="sxs-lookup"><span data-stu-id="8c734-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="8c734-150">Adal.js 會在 `userInfo` 物件中為您公開這項資訊。</span><span class="sxs-lookup"><span data-stu-id="8c734-150">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="8c734-151">若要在檢視中存取此物件，首先將 adal.js 新增至對應控制器的根範圍：</span><span class="sxs-lookup"><span data-stu-id="8c734-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="8c734-152">然後您可以直接在檢視中定址 `userInfo` 物件：</span><span class="sxs-lookup"><span data-stu-id="8c734-152">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="8c734-153">您也可以使用 `userInfo` 物件，以判斷使用者登入或登出。</span><span class="sxs-lookup"><span data-stu-id="8c734-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="8c734-154">呼叫 REST API</span><span class="sxs-lookup"><span data-stu-id="8c734-154">Call the REST API</span></span>
<span data-ttu-id="8c734-155">最後，取得某些權杖並且呼叫 REST API，以建立、讀取、更新和刪除工作。</span><span class="sxs-lookup"><span data-stu-id="8c734-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="8c734-156">您知道嗎？</span><span class="sxs-lookup"><span data-stu-id="8c734-156">Well guess what?</span></span>  <span data-ttu-id="8c734-157">您「什麼事」 都不必做。</span><span class="sxs-lookup"><span data-stu-id="8c734-157">You don't have to do *a thing*.</span></span>  <span data-ttu-id="8c734-158">Adal.js 會自動為您取得、快取和重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="8c734-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="8c734-159">它也會將這些權杖附加至您傳送至 REST API 的傳出 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="8c734-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="8c734-160">到底是如何運作的呢？</span><span class="sxs-lookup"><span data-stu-id="8c734-160">How exactly does this work?</span></span> <span data-ttu-id="8c734-161">都是因為神奇的 [AngularJS 攔截器](https://docs.angularjs.org/api/ng/service/$http)，它可讓 adal.js 轉換傳出和傳入的 http 訊息。</span><span class="sxs-lookup"><span data-stu-id="8c734-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="8c734-162">此外，adal.js 會假設傳送至相同網域做為視窗的任何要求，應該使用適用於相同應用程式識別碼的權杖做為 AngularJS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c734-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="8c734-163">這就是為什麼我們在 Angular 應用程式和 NodeJS REST API 中使用相同的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="8c734-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="8c734-164">當然，您可以覆寫這個行為，並且視需要告知 adal.js 取得其他 REST API 的權杖 - 但是對於這個簡單的案例，使用預設值即可。</span><span class="sxs-lookup"><span data-stu-id="8c734-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="8c734-165">以下是程式碼片段，說明從 Azure AD 傳送具有持有人權杖的要求有多輕鬆：</span><span class="sxs-lookup"><span data-stu-id="8c734-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="8c734-166">恭喜！</span><span class="sxs-lookup"><span data-stu-id="8c734-166">Congratulations!</span></span>  <span data-ttu-id="8c734-167">您的 Azure AD 整合式單一頁面應用程式現在已完成。</span><span class="sxs-lookup"><span data-stu-id="8c734-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="8c734-168">佩服吧！</span><span class="sxs-lookup"><span data-stu-id="8c734-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="8c734-169">它可以驗證使用者、使用 OpenID Connect 安全地呼叫其後端 REST API，以及取得使用者的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="8c734-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="8c734-170">根據預設，它支援來自 Azure AD 具有個人 Microsoft 帳戶或工作/學校帳戶的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="8c734-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="8c734-171">執行下列命令試用應用程式：</span><span class="sxs-lookup"><span data-stu-id="8c734-171">Give the app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="8c734-172">在瀏覽器中，瀏覽至 `http://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="8c734-172">In a browser navigate to `http://localhost:8080`.</span></span>  <span data-ttu-id="8c734-173">使用個人 Microsoft 帳戶或工作/學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="8c734-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="8c734-174">將工作新增至使用者待辦事項清單，然後登出。</span><span class="sxs-lookup"><span data-stu-id="8c734-174">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="8c734-175">嘗試使用其他類型的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="8c734-175">Try signing in with the other type of account.</span></span> <span data-ttu-id="8c734-176">如果您需要 Azure AD 租用戶以建立工作/學校使用者， [在這裡了解如何取得](active-directory-howto-tenant.md) (免費)。</span><span class="sxs-lookup"><span data-stu-id="8c734-176">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="8c734-177">如果要繼續了解 v2.0 端點，請返回我們的《 [v2.0 開發人員指南](active-directory-appmodel-v2-overview.md)》。</span><span class="sxs-lookup"><span data-stu-id="8c734-177">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="8c734-178">如需其他資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="8c734-178">For additional resources, check out:</span></span>

* [<span data-ttu-id="8c734-179">GitHub 上的 Azure 範例 >></span><span class="sxs-lookup"><span data-stu-id="8c734-179">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="8c734-180">Stack Overflow 上的 Azure AD >></span><span class="sxs-lookup"><span data-stu-id="8c734-180">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="8c734-181">[Azure.com 上的 Azure AD 文件 >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="8c734-181">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="8c734-182">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="8c734-182">Get security updates for our products</span></span>
<span data-ttu-id="8c734-183">我們鼓勵您造訪 [此頁面](https://technet.microsoft.com/security/dd252948) 並訂閱資訊安全摘要報告警示，以在安全性事件發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="8c734-183">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

