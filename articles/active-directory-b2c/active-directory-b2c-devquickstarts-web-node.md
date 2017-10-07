---
title: "aaaAdd 登入 tooa Node.js web 應用程式的 Azure B2C |Microsoft 文件"
description: "如何 toobuild Node.js web 應用程式的登入的使用者使用 B2C 租用戶。"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>Azure AD B2C： 新增登入 tooa Node.js web 應用程式

**Passport** 是 Node.js 的驗證中介軟體。 您可以暗中將極具彈性且模組化的 Passport 安裝在任何 Express 或 Resitify Web 應用程式中。 有一套完整的策略支援以使用者名稱和密碼、Facebook、Twitter 等來進行驗證。

我們已為 Azure Active Directory (Azure AD) 開發一套策略。 您將會安裝此模組，然後再新增 hello Azure AD`passport-azure-ad`外掛程式。

toodo，您需要：

1. 使用 Azure AD 註冊應用程式。
2. 設定您的應用程式 toouse hello`passport-azure-ad`外掛程式。
3. 使用 Passport tooissue 登入和登出要求 tooAzure AD。
4. 列印使用者資料。

hello 本教學課程中的程式碼[維護 GitHub 上](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS)。 您可以沿著 toofollow，[下載為.zip 檔案的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip)。 您也可以複製 hello 基本架構：

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

hello 完成應用程式會在本教學課程中的 hello 結尾處提供。

## <a name="get-an-azure-ad-b2c-directory"></a>取得 Azure AD B2C 目錄

您必須先建立目錄或租用戶，才可使用 Azure AD B2C。  目錄是適用於所有使用者、app、群組等項目的容器。 如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) ，再繼續進行本指南。

## <a name="create-an-application"></a>建立應用程式

接下來，您需要 toocreate 應用程式中 B2C 目錄。 提供 Azure AD 需要 toocommunicate 安全地與您的應用程式的資訊。 同時 hello 用戶端應用程式和 web 應用程式開發介面會由單一**應用程式識別碼**，因為它們組成一個邏輯應用程式。 toocreate 的應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。 請務必：

- 包含**web 應用程式**/**web API** hello 應用程式中。
- 在 [回覆 URL] 中輸入 `http://localhost:3000/auth/openid/return`。 它是 hello 預設 URL，此程式碼範例。
- 為您的應用程式建立 [應用程式密碼]  ，然後複製該密碼。 稍後您將會用到此資訊。 請注意，這個值需要 toobe [XML 逸出](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape)然後才能使用它。
- 複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。 稍後您也會需要此資訊。

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>建立您的原則

在 Azure AD B2C 中，每個使用者經驗皆由 [原則](active-directory-b2c-reference-policies.md)所定義。 此應用程式包含三種身分識別體驗：註冊、登入，以及使用 Facebook 登入。 您將 toocreate 需要每個型別，此原則，如中所述[原則參考文件](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)。 建立您的三個原則時，請務必：

- 選擇 hello**顯示名稱**與其他註冊的屬性，在您註冊的原則。
- 選擇 hello**顯示名稱**和**物件識別碼**中每個原則的應用程式宣告。 您也可以選擇其他宣告。
- 複製 hello**名稱**的每個原則建立之後。 就不應有 hello 前置詞`b2c_1_`。  稍後您將需要這些原則名稱。

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

建立三個原則之後，您便準備好 toobuild 您的應用程式。

請注意本文未涵蓋 toouse hello 原則您剛才建立的方式。 toolearn 有關原則的運作方式在 Azure AD B2C，啟動以 hello [.NET web 應用程式快速入門教學課程](active-directory-b2c-devquickstarts-web-dotnet.md)。

## <a name="add-prerequisites-tooyour-directory"></a>加入必要條件 tooyour 目錄

從 hello 命令列，變更目錄 tooyour 根資料夾中，如果您已經不存在。 執行下列命令的 hello:

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

此外，我們使用`passport-azure-ad`我們 preview 中的 hello 快速入門的 hello 基本架構。

- `npm install passport-azure-ad`

這將會安裝 hello 程式庫，`passport-azure-ad`而定。

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>設定您的應用程式 toouse hello Passport Node.js 策略
設定 hello Express 中介軟體 toouse hello OpenID Connect 的驗證通訊協定。 Passport 將會使用的 tooissue 登入和登出要求、 管理使用者工作階段，以及取得有關使用者，以及其他動作的資訊。

開啟 hello `config.js` hello hello 專案根目錄中的檔案，並在 hello 中輸入您的應用程式組態值`exports.creds`> 一節。
- `clientID`: hello**應用程式識別碼**指派 tooyour hello 註冊入口網站中的應用程式。
- `returnURL`: hello**重新導向 URI** hello 入口網站中輸入。
- `tenantName`: hello 租用戶應用程式名稱，例如**contoso.onmicrosoft.com**。

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

開啟 hello `app.js` hello hello 專案根目錄中的檔案。 新增下列呼叫 tooinvoke hello hello`OIDCStrategy`隨附的策略`passport-azure-ad`。


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

使用您剛才參考 toohandle 登入要求的 hello 策略。

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
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
Passport 會對其所有策略 (包括 Twitter 和 Facebook) 所有類似的模式。 所有的策略寫入器會遵守 toothis 模式。 當您查看 hello 策略時，您可以看到您傳遞`function()`具有語彙基元和`done`做為 hello 參數。 hello 策略恢復 tooyou 它所有的工作完成後。 儲存 hello 使用者，使您不需要為其 tooask 再次隱藏 hello 語彙基元。

> [!IMPORTANT]
hello 上述程式碼會 hello 伺服器會驗證所有使用者。 這是自動註冊程序。 當您使用實際執行伺服器時，您不想 toolet 中使用者，除非它們已經完成註冊程序，您已設定。 供消費者使用的應用程式經常會看見這種模式。 這些可讓您 tooregister 使用 Facebook、 但然後人員要求您 toofill 出額外的資訊。 如果我們的應用程式無法範例，我們無法擷取 hello 會傳回的權杖物件的電子郵件地址，然後要求 hello 使用者 toofill 出額外的資訊。 因為這是在測試伺服器，我們只要加入使用者 toohello 記憶體中資料庫。

新增 hello 方法可讓您的使用者登入，tookeep 追蹤依 Passport。 這包括將使用者資訊序列化和還原序列化：

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
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

新增 hello 程式碼 tooload hello Express 引擎。 在 hello 下列程式碼，您可以看到，我們會使用預設 hello`/views`和`/routes`提供快速的模式。

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

新增 hello`POST`遞交的路由 hello 實際的登入要求 toohello`passport-azure-ad`引擎：

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>使用 Passport tooissue 登入和登出要求 tooAzure AD

您的應用程式是現在已正確設定的 toocommunicate 與 hello v2.0 端點使用 hello OpenID Connect 的驗證通訊協定。 `passport-azure-ad`已處理 hello 製作驗證訊息、 驗證 Azure ad 的權杖和維護使用者工作階段的詳細資料。 所有會維持為您的使用者是 toogive 方式 toosign 中的並登入 out、 以及 toogather 其他有關已登入的使用者。

首先，新增 hello 預設、 登入、 帳戶和登出方法 tooyour`app.js`檔案：

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

tooreview 這些方法的詳細資料：
- hello`/`路由重新導向 toohello`index.ejs`檢視藉由傳遞 hello 要求中的 hello 使用者 （如果有的話）。
- hello`/account`路由會先確認您已驗證 (這是下面 hello 實作)。 接著，將 hello 使用者 hello 要求中，讓您可取得 hello 使用者的其他資訊。
- hello`/login`路由呼叫 hello`azuread-openidconnect`驗證器，從`passport-azure-ad`。 如果不成功，hello 路由 hello 將使用者重新導向回太`/login`。
- `/logout` 只會呼叫 `logout.ejs` (和其路由)。 這會清除 cookie，然後傳回 hello 回到使用者太`index.ejs`。


Hello 最後一個部分`app.js`，新增 hello`EnsureAuthenticated`方法用於 hello`/account`路由。

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

最後，建立 hello 伺服器本身在`app.js`。

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>建立 hello 檢視，並將您的原則路由 Express toocall 中

`app.js` 現已完成。 您只需要 tooadd hello 路由和 toocall hello 登入並註冊原則可讓您的檢視。 這些也處理 hello`/logout`和`/login`您所建立的路由。

建立 hello `/routes/index.js` hello 根目錄下的路由。

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

建立 hello `/routes/user.js` hello 根目錄下的路由。

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

這些簡單的路由可傳遞要求 tooyour 檢視。 如果有的話，它們就會包含 hello 使用者。

建立 hello `/views/index.ejs` hello 根目錄下的檢視。 這是呼叫登入和登出原則的簡單網頁。您也可以使用它 toograb 帳戶資訊。 請注意，您可以使用條件式 hello `if (!user)` hello 使用者透過傳入的 hello 要求 tooprovide 證據 hello 使用者已登入。

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

建立 hello`/views/account.ejs`檢視 hello 根目錄下，讓您可以檢視其他資訊的`passport-azure-ad`置於 hello 使用者要求。

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
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

現在您可以建立並執行您的應用程式。

執行`node app.js`並瀏覽過`http://localhost:3000`


註冊或使用電子郵件或 Facebook 登入 toohello 應用程式。 登出後，再以不同使用者身分重新登入。

##<a name="next-steps"></a>後續步驟

如需參考，hello 完成 （不含您的組態值） 的範例[提供成.zip 檔案](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip)。 您也可以從 Github 複製它：

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

您現在可以繼續 toomore 進階主題。 您可以嘗試：

[使用 Node.js 中 hello B2C 模型來保護 web API](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
