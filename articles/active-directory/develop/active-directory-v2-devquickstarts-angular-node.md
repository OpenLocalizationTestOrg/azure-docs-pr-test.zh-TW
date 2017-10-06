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
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a>新增登入 tooan AngularJS 單一頁面應用程式： NodeJS
在本文中，我們會將新增使用電源的 Microsoft 帳戶 tooan AngularJS 應用程式使用 hello Azure Active Directory v2.0 端點登入。 hello v2.0 端點 tooperform 應用程式中的單一整合可讓您，而且驗證使用者使用個人和工作/學校帳戶。

這個範例是簡單的待辦事項清單單一頁面應用程式，在後端 REST API 儲存工作、使用 NodeJS 撰寫，並且使用 Azure AD 的 OAuth 持有人權杖進行保護。  hello AngularJS 應用程式會使用我們的開放原始碼 JavaScript 驗證程式庫[adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello 整個登入程序，並取得呼叫 hello REST API 的語彙基元。  hello 相同的模式可以是套用的 tooauthenticate tooother REST Api，像是 hello [Microsoft Graph](https://graph.microsoft.com)或 hello Azure 資源管理員 Api。

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。  toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 
> 

## <a name="download"></a>下載
您將需要啟動 tooget，toodownload & 安裝[node.js](https://nodejs.org)。  然後您可以複製或 [下載](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) 基本架構應用程式：

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

hello 基本架構應用程式包含簡單的 AngularJS 應用程式中，所有 hello 未定案程式碼，但是遺漏之所有 hello 身分識別相關的片段。  若您不想沿著 toofollow，可改為複製或[下載](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip)hello 完成範例。

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a>註冊應用程式
首先，建立應用程式在 hello[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或請遵循這些[詳細步驟](active-directory-v2-app-registration.md)。  請確定：

* 新增 hello **Web**平台應用程式。
* 輸入正確的 hello**重新導向 URI**。 此範例的 hello 預設值是`http://localhost:8080`。
* 保留 hello**允許隱含流程**啟用的核取方塊。 

複製下 hello**應用程式識別碼**指派的 tooyour 應用程式，您將在稍後需要。 

## <a name="install-adaljs"></a>安裝 adal.js
toostart，瀏覽的 tooproject 您下載並安裝 adal.js。  如果您已安裝 [bower](http://bower.io/) ，您只要執行這個命令即可。  任何相依性版本不符，只要選擇 hello 更高的版本。

```
bower install adal-angular#experimental
```

或者，您可以手動下載 [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) 和 [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js)。  加入兩個檔案 toohello`app/lib/adal-angular-experimental/dist`目錄。

現在 hello 專案您慣用的文字在編輯器中開啟，並載入 adal.js 結尾 hello hello 頁面主體：

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>設定 hello REST API
雖然我們正在進行設定，可讓 get hello 後端 REST API 可以運作。  在命令提示字元中安裝所有的 hello 必要的封裝執行 （請確定您在 hello hello 專案的最上層的目錄）：

```
npm install
```

現在開啟`config.js`和取代 hello`audience`值：

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

hello REST API 將會使用在收到 hello 角度應用程式的 AJAX 要求此值 toovalidate 語彙基元。  請注意，這個簡單的 REST API 將儲存記憶體中資料-因此每個時間 toostop hello 伺服器，您將會遺失所有先前建立的工作。

這就是我們要討論 hello REST API 的運作方式的 toospend hello 時間。  感覺的免費 toopoke hello 程式碼中，但如果您想 toolearn 深入了解保護的 web Api 與 Azure AD，請參閱[本文](active-directory-v2-devquickstarts-node-api.md)。 

## <a name="sign-users-in"></a>將使用者登入
時間 toowrite 一些識別程式碼。  您可能已經發現 adal.js 包含 AngularJS 提供者，它運用 Angular 路由機制相當良好。  啟動新增 hello adal 模組 toohello 應用程式：

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

您現在可以初始化 hello`adalProvider`以您的應用程式 ID:

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

太好，現在 adal.js 具有 hello 的所有資訊需要 toosecure 中您的應用程式並登入的使用者。  將登入 tooforce 的 hello，應用程式中所有所需的特定路由是一行程式碼：

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

現在當使用者按一下 hello`TodoList`連結，adal.js 會自動重新導向 tooAzure AD 登入必要的。  您也可以藉由在控制器中叫用 adal.js，明確傳送登入和登出要求：

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

## <a name="display-user-info"></a>顯示使用者資訊
既然 hello 使用者登入，您可能需要 tooaccess hello 登入使用者的驗證資料在應用程式中。  Adal.js 會公開這項資訊在 hello`userInfo`物件。  tooaccess 在檢視中，這個物件會先加入 adal.js toohello 根範圍 hello 相對應的控制項：

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

然後您可以直接定址 hello`userInfo`在檢視中的物件： 

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

您也可以使用 hello`userInfo`物件 toodetermine 如果 hello 使用者登入與否。

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

## <a name="call-hello-rest-api"></a>呼叫 hello REST API
最後，它是時間 tooget 某些語彙基元並呼叫 hello REST API toocreate、 讀取、 更新和刪除的工作。  您知道嗎？  您不需要 toodo*事*。  Adal.js 會自動為您取得、快取和重新整理權杖。  它也會負責的附加 toooutgoing AJAX 要求您傳送 toohello REST API 的語彙基元。  

到底是如何運作的呢？ 它是所有的感謝您 toohello 魔力[AngularJS 攔截器](https://docs.angularjs.org/api/ng/service/$http)，可讓 adal.js tootransform 傳出和傳入的 http 訊息。  此外，adal.js 會假設任何要求傳送 toohello 相同的網域為 hello 視窗應該使用適用於語彙基元 hello 相同的應用程式識別碼為 hello AngularJS 應用程式。  這就是為什麼我們使用 hello hello NodeJS REST API 和這兩個 hello 角度的應用程式中的相同應用程式識別碼。  當然，您可以覆寫這個行為，並告訴 adal.js tooget 語彙基元的其他 REST Api，如有必要-但這個簡單案例 hello 將進行的預設值。

以下是示範是多麼的輕鬆 toosend 要求，以從 Azure AD 的承載權杖的程式碼片段：

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

恭喜！  您的 Azure AD 整合式單一頁面應用程式現在已完成。  佩服吧！  它可以驗證使用者、 安全地呼叫它的後端 REST API 使用 OpenID Connect，並取得 hello 使用者的基本資訊。  預設 hello 方塊中，它可支援具有個人 Microsoft 帳戶或工作/學校帳戶向 Azure AD 的任何使用者。  試試 hello 應用程式執行：

```
node server.js
```

在瀏覽器中瀏覽過`http://localhost:8080`。  使用個人 Microsoft 帳戶或工作/學校帳戶登入。  新增工作 toohello 使用者的待辦事項清單，並登出。再試一次登入的 hello 其他類型的帳戶。 如果您需要 Azure AD 租用戶 toocreate 工作/學校 users，[深入了解如何 tooget 一個這裡](active-directory-howto-tenant.md)（它是免費的）。

深入了解 hello toocontinue hello v2.0 端點、 head 後 tooour [v2.0 開發人員指南](active-directory-appmodel-v2-overview.md)。  如需其他資源，請參閱：

* [GitHub 上的 Azure 範例 >>](https://github.com/Azure-Samples)
* [Stack Overflow 上的 Azure AD >>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* [Azure.com 上的 Azure AD 文件 >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>取得產品的安全性更新
我們建議您造訪的安全性事件發生時的 tooget 通知[本頁](https://technet.microsoft.com/security/dd252948)及訂閱 tooSecurity 諮詢警示。

