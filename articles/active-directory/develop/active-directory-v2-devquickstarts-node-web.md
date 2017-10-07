---
title: "Node.js web 應用程式登入 aaaAzure Active Directory v2.0 |Microsoft 文件"
description: "了解如何 toobuild Node.js web 應用程式，使用個人 Microsoft 帳戶和工作或學校帳戶登入使用者。"
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a>新增登入 tooa Node.js web 應用程式

> [!NOTE]
> 並非所有的 Azure Active Directory 案例和功能搭配 hello v2.0 端點。 toodetermine 是否應該使用 hello v2.0 端點或 hello v1.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。
> 

在本教學課程中，我們使用 Passport toodo hello 下列工作：

* 在 web 應用程式中，登入 hello 使用者使用 Azure Active Directory (Azure AD) 和 hello v2.0 端點。
* 顯示 hello 使用者的相關資訊。
* 符號 hello 使用者登出 hello 應用程式。

**Passport** 是 Node.js 的驗證中介軟體。 您可以暗中將極具彈性且模組化的 Passport 放入任何 Express 架構或 resitify Web 應用程式。 在 Passport 中，一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他選項進行驗證。 我們已為 Azure AD 開發一個策略。 在本文中，我們會示範如何 tooinstall hello 模組，並再新增 hello Azure AD`passport-azure-ad`外掛程式。

## <a name="download"></a>下載
此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs)。 toofollow hello 教學課程中，您可以[下載為.zip 檔案的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip)或再製 hello 基本架構：

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

您也可以取得 hello 完成應用程式在此教學課程中的 hello 結尾處。

## <a name="1-register-an-app"></a>1：註冊應用程式
建立新的應用程式在[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或遵循[這些詳細步驟](active-directory-v2-app-registration.md)tooregister 應用程式。 請確定您已執行下列動作：

* 複製 hello**應用程式識別碼**指派 tooyour 應用程式。 您在本教學課程中會需要用到。
* 新增 hello **Web**平台應用程式。
* 複製 hello**重新導向 URI**從 hello 入口網站。 您必須使用 hello 預設 URI 值`urn:ietf:wg:oauth:2.0:oob`。

## <a name="2-add-prerequisities-tooyour-directory"></a>2： 將必要條件 tooyour 目錄
在命令提示字元中，變更目錄 toogo tooyour 根資料夾中，如果您已不存在。 執行下列命令的 hello:

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

此外，我們使用`passport-azure-ad`在 hello 基本架構中的 hello 快速入門：

* `npm install passport-azure-ad`

這會安裝 hello 程式庫，`passport-azure-ad`使用。

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3： 設定您的應用程式 toouse hello passport-節點-js 策略
設定 hello Express 中介軟體 toouse hello OpenID Connect 的驗證通訊協定。 您會使用 Passport tooissue 登入和登出要求、 管理 hello 使用者工作階段，以及取得 hello 使用者，以及其他項目相關資訊。

1.  Hello hello 專案根目錄中開啟 hello Config.js 檔案。 在 hello`exports.creds`區段中，輸入您的應用程式組態值。
  
  * `clientID`: hello**應用程式識別碼**這是指派的 tooyour hello Azure 入口網站中的應用程式。
  * `returnURL`: hello**重新導向 URI** hello 入口網站中輸入的。
  * `clientSecret`: hello hello 入口網站中產生的密碼。

2.  Hello hello 專案根目錄中開啟 hello App.js 檔案。 tooinvoke hello OIDCStrategy stratey，隨附於`passport-azure-ad`，新增下列呼叫 hello:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle 您登入的要求，使用只參考 hello 策略：

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
      process.nextTick(function () {
        findByEmail(profile.email, function(err, user) {
          if (err) {
            return done(err);
          }
          if (!user) {
            // "Auto-registration"
            users.push(profile);
            return done(null, profile);
          }
          return done(null, user);
        });
      });
    }
  ));
  ```

Passport 會針對其所有策略 (Twitter、Facebook 等) 使用類似的模式。 所有的策略寫入器會遵守 toohello 模式。 傳送嗨策略`function()`使用語彙基元和`done`做為參數。 所有其功能之後，就會傳回 hello 策略。 儲存 hello 使用者並存放 hello 語彙基元，因此您不需要為其 tooask 一次。

  > [!IMPORTANT]
  > hello 上述程式碼會採用任何使用者，可以驗證 tooyour 伺服器。 這就是所謂的自動註冊。 在實際執行伺服器上，您不想 toolet 任何人而不需要先經過您選擇註冊程序，它們。 這通常是您在取用者應用程式中看到的 hello 模式。 hello 應用程式可能會讓您與 Facebook tooregister 但然後它會要求您 tooenter 其他資訊。 如果您沒有使用命令列程式在此教學課程，您無法從 hello 傳回的語彙基元物件擷取 hello 電子郵件。 然後，您可能會要求 hello 使用者 tooenter 額外資訊。 因為這是在測試伺服器，您會加入 hello 使用者直接 toohello 記憶體中資料庫。
  > 
  > 

4.  加入您使用的登入，使用者播放軌 tookeep hello 方法依 Passport。 這包括序列化和還原序列化 hello 使用者的資訊：

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
  var users = [];

  var findByEmail = function(email, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
      var user = users[i];
      log.info('we are using user: ', user);
      if (user.email === email) {
        return fn(null, user);
      }
    }
    return fn(null, null);
  };
  ```

5.  加入 hello 載入 hello Express 引擎的程式碼。 使用 hello 預設 /views 和 Express 的 /routes 模式提供：

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  新增 hello 後傳送該遞交 hello 實際的登入要求 toohello`passport-azure-ad`引擎：

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4： 使用 Passport tooissue 登入和登出要求 tooAzure AD
您的應用程式現在設定 toocommunicate 與 hello v2.0 端點使用 hello OpenID Connect 的驗證通訊協定。 hello`passport-azure-ad`策略會負責所有 hello 詳細資料，製作驗證訊息、 驗證 Azure ad 的權杖和維護的 hello 使用者工作階段。 處於 toodo 的所有您的使用者是 toogive 方式 toosign 中的並登入和 toogather hello 使用者登入的詳細資訊。

1.  新增 hello**預設**，**登入**，**帳戶**，和**登出**方法 tooyour App.js 檔案：

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  以下是 hello 詳細資料：
    
    * hello`/`路由重新導向 toohello index.ejs 檢視。 它會傳入 hello 使用者 hello 要求 （如果有的話）。
    * hello`/account`路由先*可確保當您驗證*（您實作，在下列程式碼的 hello）。 然後，它會傳入 hello 使用者 hello 要求。 如此能讓您可以取得關於 hello 使用者的詳細資訊。
    * hello`/login`路由呼叫您`azuread-openidconnect`驗證器，從`passport-azuread`。 如果不成功的它會重新導向回到 hello 使用者太`/login`。
    * hello`/logout`路由呼叫 hello logout.ejs 檢視 （和路由）。 這會清除 cookie，然後傳回 hello 使用者回復 tooindex.ejs。

2.  新增 hello **EnsureAuthenticated**稍早在您使用的方法`/account`:

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  App.js，在建立 hello 伺服器：

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5： 建立您的使用者顯示 hello 網站上的 Express 中的 hello 檢視和路由
加入 hello 路由和顯示資訊 toohello 使用者的檢視。 hello 路由和檢視表也會處理 hello`/logout`和`/login`您所建立的路由。

1. 在 hello 根目錄中，建立 hello`/routes/index.js`路由。

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  在 hello 根目錄中，建立 hello`/routes/user.js`路由。

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`和`/routes/user.js`hello 要求 tooyour 檢視，包括 hello 使用者可傳遞的簡單路由。

3.  在 hello 根目錄中，建立 hello`/views/index.ejs`檢視。 此頁面會呼叫您的 **login** 和 **logout** 方法。 您也可以使用 hello`/views/index.ejs`檢視 toocapture 帳戶資訊。 您可以使用條件式 hello`if (!user)`身分 hello hello 要求中傳遞出去。 這可以證明您已經有使用者登入。

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  在 hello 根目錄中，建立 hello`/views/account.ejs`檢視。 hello`/views/account.ejs`檢視可讓您 tooview 其他資訊的`passport-azuread`置於 hello 使用者要求。

  ```Javascript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
  <p>displayName: <%= user.displayName %></p>
  <p>givenName: <%= user.name.givenName %></p>
  <p>familyName: <%= user.name.familyName %></p>
  <p>UPN: <%= user._json.upn %></p>
  <p>Profile ID: <%= user.id %></p>
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  新增版面配置。 在 hello 根目錄中，建立 hello`/views/layout.ejs`檢視。

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  toobuild 並執行應用程式執行`node app.js`。 然後，跳過`http://localhost:3000`。

7.  使用個人 Microsoft 帳戶或是公司或學校帳戶登入。 請注意 hello 使用者的身分識別會反映在 hello /account 清單。 

您現在已擁有使用業界標準通訊協定保護的 Web 應用程式了。 您可以在應用程式中利用使用者的個人和公司或學校帳戶驗證他們的身分。

## <a name="next-steps"></a>後續步驟
供參考，完成的 hello 範例 （不含您的組態值） 依現狀[.zip 檔案](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip)。 您也可以從 GitHub 加以複製：

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

接下來，您可以移動 toomore 進階主題上。 您可能想 tootry:

[藉由使用 hello v2.0 端點保護 Node.js web 應用程式開發介面](active-directory-v2-devquickstarts-node-api.md)

以下是一些其他資源：

* [Azure AD v2.0 開發人員指南](active-directory-appmodel-v2-overview.md)
* [Stack Overflow "azure-active-directory" 標籤 (英文)](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>取得產品的安全性更新
我們鼓勵 toosign 向上 toobe 安全性事件發生時收到通知。 在 hello [Microsoft 技術安全性通知](https://technet.microsoft.com/security/dd252948)頁面上，訂閱 tooSecurity 摘要報告警示。

