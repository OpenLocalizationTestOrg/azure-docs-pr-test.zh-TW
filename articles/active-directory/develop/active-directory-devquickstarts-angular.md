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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>使用 Azure AD 保護 AngularJS 單一頁面應用程式

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) 可讓簡單又直接的您 tooadd 登入、 登出，並安全 OAuth 應用程式開發介面呼叫 tooyour 單一頁面應用程式。  它可讓您的應用程式 tooauthenticate 使用者與他們的 Windows Server Active Directory 帳戶，並使用任何 web API，Azure AD 可協助保護，例如 Office 365 Api hello 或 hello Azure API。

對於瀏覽器中執行的 JavaScript 應用程式，Azure AD 提供 hello Active Directory 驗證程式庫 (ADAL) 或 adal.js。 adal.js hello 唯一目的是 toomake 輕鬆的應用程式 tooget 存取語彙基元。 toodemonstrate 多麼容易，所以這裡，我們將建立 AngularJS tooDo 清單應用程式的：

* 符號 hello toohello 應用程式中的使用者利用 Azure AD 作為 hello 身分識別提供者。

* 顯示 hello 使用者的一些資訊。
* 安全地呼叫 hello 應用程式的 tooDo 清單應用程式開發介面使用從 Azure AD 的持有者權杖。
* 符號 hello 使用者登出 hello 應用程式。

toobuild hello 完成之後，使用應用程式，您需要：

1. 向 Azure AD 註冊應用程式.
2. 安裝 ADAL 和設定 hello 單一頁面應用程式。
3. Hello 單一頁面應用程式中使用 ADAL toohelp 安全的網頁。

啟動，tooget[下載 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip)或[下載完成的 hello 範例](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)。 您還需要一個可以建立使用者並註冊應用程式的 Azure AD 租用戶。 如果您還沒有租用戶，[深入了解如何 tooget 一個](active-directory-howto-tenant.md)。

## <a name="step-1-register-hello-directorysearcher-application"></a>步驟 1： 註冊 hello DirectorySearcher 應用程式
tooenable 您的應用程式 tooauthenticate 使用者和 get 語彙基元，您必須先在您的 Azure AD 租用戶 tooregister:

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 如果您已登入 toomultiple 目錄，您可能需要 tooensure 您正在檢視 hello 正確的目錄。 toodo，hello 頂端列上，按一下您的帳戶。 在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。
3. 按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。
4. 按一下 [應用程式註冊]，然後選取 [新增]。
5. 請依照 hello 提示，並建立新的 web 應用程式和/或 web API:
  * **名稱**描述應用程式 toousers。
  * **重新導向 Uri** hello 位置 toowhich Azure AD 將會傳回語彙基元。 此範例中的 hello 預設位置是`https://localhost:44326/`。
6. 完成註冊之後，Azure AD 會指派唯一的應用程式識別碼 tooyour 應用程式。  您將需要此值在 hello 下一步 區段中，因此將它複製從 hello 應用程式 索引標籤。
7. Adal.js 會使用 Azure AD 中的 hello OAuth 隱含流程 toocommunicate。 您的應用程式，您必須啟用 hello 隱含流程：
  1. 按一下 hello 應用程式，然後選取**資訊清單**tooopen hello 內嵌資訊清單編輯器。
  2. 找出 hello`oauth2AllowImplicitFlow`屬性。 將其值設定為太`true`。
  3. 按一下**儲存**toosave hello 資訊清單。
8. 在您的應用程式租用戶上授予權限。 跳過**設定** > **屬性** > **必要的使用權限**，然後按一下 hello**授與權限**hello 頂端列上的按鈕。 按一下**是**tooconfirm。

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>步驟 2： 安裝 ADAL 及設定 hello 單一頁面應用程式
既然您在 Azure AD 中已有應用程式，您可以安裝 adal.js，並撰寫身分識別相關的程式碼。

### <a name="configure-hello-javascript-client"></a>Hello JavaScript 用戶端設定
開始使用 Package Manager Console hello 加入 adal.js toohello TodoSPA 專案：
  1. 下載[adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js)並將它加入 toohello`App/Scripts/`專案目錄。
  2. 下載[adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js)並將它加入 toohello`App/Scripts/`專案目錄。
  3. 載入 hello hello 結束之前的每個指令碼`</body>`中`index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Hello 後端伺服器設定
Hello 單一頁面應用程式的後端 tooDo 清單 API tooaccept 語彙基元從 hello 瀏覽器，hello 後端需要 hello 應用程式註冊的組態資訊。 在 hello TodoSPA 專案中，開啟`web.config`。 取代 hello 中的項目 hello hello 值`<appSettings>`> 一節中所用 tooreflect hello 值 hello Azure 入口網站。 每當使用 ADAL 時，您的程式碼便會參考這些值。
  * `ida:Tenant`是您的 Azure AD 租用戶-例如 contoso.onmicrosoft.com hello 網域。
  * `ida:Audience`這是您所複製的 hello 入口網站應用程式的 hello 用戶端識別碼。

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Hello 單一頁面應用程式中的步驟 3： 使用 ADAL toohelp 安全頁面
adal.js 與 AngularJS 路由和 HTTP 提供者整合，因此您可以保護單一頁面應用程式中的個別檢視。

1. 在`App/Scripts/app.js`，納入 hello adal.js 模組：

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. 初始化`adalProvider`中也使用您的應用程式註冊 hello 組態值`App/Scripts/app.js`:

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
3. 協助安全 hello `TodoList` hello 應用程式利用只有一行的程式碼中的檢視： `requireADLogin`。

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>摘要
現在，您會有安全的單一頁面應用程式可以在使用者登入和發出的持有人權杖保護要求 tooits 後端應用程式開發介面。 當使用者按一下 hello **TodoList**連結，adal.js 會自動重新導向 tooAzure AD 登入必要的。 此外，adal.js 會自動附加存取語彙基元 tooany Ajax 要求傳送 toohello 應用程式後端。  

hello 前面的步驟都 hello 裸機最小必要 toobuild 之單一頁面應用程式使用 adal.js。 但單一頁面應用程式中還有其他幾項很有用的功能︰

* tooexplicitly 發出登入和登出要求，您可以定義函式中叫用 adal.js 您控制站。  在 `App/Scripts/homeCtrl.js`中：

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
* 您可能想 toopresent hello 應用程式的 UI 中的使用者資訊。 hello ADAL 服務已經加入 toohello`userDataCtrl`控制站，以便您可以存取 hello `userInfo` hello 中的物件相關聯的檢視， `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* 有許多案例中您會想 tooknow 如果 hello 使用者登入與否。 您也可以使用 hello`userInfo`物件 toogather 這項資訊。  例如，在`index.html`，您可以顯示任一 hello**登入**或**登出**根據驗證狀態的按鈕：

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

Azure AD 整合單一頁面應用程式可以驗證使用者，安全地使用 OAuth 2.0 中，呼叫它的後端及 hello 使用者的基本資訊。 如果您還沒有這麼做，現在是 hello 時間 toopopulate 與某些使用者的租用戶。 執行 tooDo 清單單一頁面應用程式，並使用其中一個這些使用者的登入。 新增工作 toohello 使用者的待辦事項清單、 登出，再重新登入。

Adal.js 會使它輕鬆 tooincorporate 常見的身分識別功能成為您的應用程式。 它會為您的所有 hello dirty 工作負責： 快取管理、 OAuth 通訊協定支援，呈現給 hello 使用者登入 UI，重新整理過期的語彙基元等等。

參考，完成的 hello 範例 （不含您的組態值） 會提供[GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip)。

## <a name="next-steps"></a>後續步驟
您現在可以移動 tooadditional 案例。 您可能會想 tootry:[呼叫的單一頁面應用程式從 CORS web API](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet)。

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
