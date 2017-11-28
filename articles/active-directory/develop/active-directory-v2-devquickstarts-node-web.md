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
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="d2580-103">新增登入 tooa Node.js web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d2580-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="d2580-104">並非所有的 Azure Active Directory 案例和功能搭配 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="d2580-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="d2580-105">toodetermine 是否應該使用 hello v2.0 端點或 hello v1.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="d2580-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="d2580-106">在本教學課程中，我們使用 Passport toodo hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="d2580-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="d2580-107">在 web 應用程式中，登入 hello 使用者使用 Azure Active Directory (Azure AD) 和 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="d2580-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="d2580-108">顯示 hello 使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d2580-108">Display information about hello user.</span></span>
* <span data-ttu-id="d2580-109">符號 hello 使用者登出 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2580-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="d2580-110">**Passport** 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="d2580-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="d2580-111">您可以暗中將極具彈性且模組化的 Passport 放入任何 Express 架構或 resitify Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2580-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="d2580-112">在 Passport 中，一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他選項進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d2580-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="d2580-113">我們已為 Azure AD 開發一個策略。</span><span class="sxs-lookup"><span data-stu-id="d2580-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="d2580-114">在本文中，我們會示範如何 tooinstall hello 模組，並再新增 hello Azure AD`passport-azure-ad`外掛程式。</span><span class="sxs-lookup"><span data-stu-id="d2580-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="d2580-115">下載</span><span class="sxs-lookup"><span data-stu-id="d2580-115">Download</span></span>
<span data-ttu-id="d2580-116">此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs)。</span><span class="sxs-lookup"><span data-stu-id="d2580-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="d2580-117">toofollow hello 教學課程中，您可以[下載為.zip 檔案的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip)或再製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="d2580-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="d2580-118">您也可以取得 hello 完成應用程式在此教學課程中的 hello 結尾處。</span><span class="sxs-lookup"><span data-stu-id="d2580-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="d2580-119">1：註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="d2580-119">1: Register an app</span></span>
<span data-ttu-id="d2580-120">建立新的應用程式在[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或遵循[這些詳細步驟](active-directory-v2-app-registration.md)tooregister 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2580-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="d2580-121">請確定您已執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d2580-121">Make sure you:</span></span>

* <span data-ttu-id="d2580-122">複製 hello**應用程式識別碼**指派 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2580-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="d2580-123">您在本教學課程中會需要用到。</span><span class="sxs-lookup"><span data-stu-id="d2580-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="d2580-124">新增 hello **Web**平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2580-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="d2580-125">複製 hello**重新導向 URI**從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d2580-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="d2580-126">您必須使用 hello 預設 URI 值`urn:ietf:wg:oauth:2.0:oob`。</span><span class="sxs-lookup"><span data-stu-id="d2580-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="d2580-127">2： 將必要條件 tooyour 目錄</span><span class="sxs-lookup"><span data-stu-id="d2580-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="d2580-128">在命令提示字元中，變更目錄 toogo tooyour 根資料夾中，如果您已不存在。</span><span class="sxs-lookup"><span data-stu-id="d2580-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="d2580-129">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d2580-129">Run hello following commands:</span></span>

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

<span data-ttu-id="d2580-130">此外，我們使用`passport-azure-ad`在 hello 基本架構中的 hello 快速入門：</span><span class="sxs-lookup"><span data-stu-id="d2580-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="d2580-131">這會安裝 hello 程式庫，`passport-azure-ad`使用。</span><span class="sxs-lookup"><span data-stu-id="d2580-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="d2580-132">3： 設定您的應用程式 toouse hello passport-節點-js 策略</span><span class="sxs-lookup"><span data-stu-id="d2580-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="d2580-133">設定 hello Express 中介軟體 toouse hello OpenID Connect 的驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d2580-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="d2580-134">您會使用 Passport tooissue 登入和登出要求、 管理 hello 使用者工作階段，以及取得 hello 使用者，以及其他項目相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d2580-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="d2580-135">Hello hello 專案根目錄中開啟 hello Config.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="d2580-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="d2580-136">在 hello`exports.creds`區段中，輸入您的應用程式組態值。</span><span class="sxs-lookup"><span data-stu-id="d2580-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="d2580-137">`clientID`: hello**應用程式識別碼**這是指派的 tooyour hello Azure 入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2580-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="d2580-138">`returnURL`: hello**重新導向 URI** hello 入口網站中輸入的。</span><span class="sxs-lookup"><span data-stu-id="d2580-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="d2580-139">`clientSecret`: hello hello 入口網站中產生的密碼。</span><span class="sxs-lookup"><span data-stu-id="d2580-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="d2580-140">Hello hello 專案根目錄中開啟 hello App.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="d2580-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="d2580-141">tooinvoke hello OIDCStrategy stratey，隨附於`passport-azure-ad`，新增下列呼叫 hello:</span><span class="sxs-lookup"><span data-stu-id="d2580-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="d2580-142">toohandle 您登入的要求，使用只參考 hello 策略：</span><span class="sxs-lookup"><span data-stu-id="d2580-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

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

<span data-ttu-id="d2580-143">Passport 會針對其所有策略 (Twitter、Facebook 等) 使用類似的模式。</span><span class="sxs-lookup"><span data-stu-id="d2580-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="d2580-144">所有的策略寫入器會遵守 toohello 模式。</span><span class="sxs-lookup"><span data-stu-id="d2580-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="d2580-145">傳送嗨策略`function()`使用語彙基元和`done`做為參數。</span><span class="sxs-lookup"><span data-stu-id="d2580-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="d2580-146">所有其功能之後，就會傳回 hello 策略。</span><span class="sxs-lookup"><span data-stu-id="d2580-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="d2580-147">儲存 hello 使用者並存放 hello 語彙基元，因此您不需要為其 tooask 一次。</span><span class="sxs-lookup"><span data-stu-id="d2580-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d2580-148">hello 上述程式碼會採用任何使用者，可以驗證 tooyour 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d2580-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="d2580-149">這就是所謂的自動註冊。</span><span class="sxs-lookup"><span data-stu-id="d2580-149">This is known as auto-registration.</span></span> <span data-ttu-id="d2580-150">在實際執行伺服器上，您不想 toolet 任何人而不需要先經過您選擇註冊程序，它們。</span><span class="sxs-lookup"><span data-stu-id="d2580-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="d2580-151">這通常是您在取用者應用程式中看到的 hello 模式。</span><span class="sxs-lookup"><span data-stu-id="d2580-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="d2580-152">hello 應用程式可能會讓您與 Facebook tooregister 但然後它會要求您 tooenter 其他資訊。</span><span class="sxs-lookup"><span data-stu-id="d2580-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="d2580-153">如果您沒有使用命令列程式在此教學課程，您無法從 hello 傳回的語彙基元物件擷取 hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="d2580-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="d2580-154">然後，您可能會要求 hello 使用者 tooenter 額外資訊。</span><span class="sxs-lookup"><span data-stu-id="d2580-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="d2580-155">因為這是在測試伺服器，您會加入 hello 使用者直接 toohello 記憶體中資料庫。</span><span class="sxs-lookup"><span data-stu-id="d2580-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="d2580-156">加入您使用的登入，使用者播放軌 tookeep hello 方法依 Passport。</span><span class="sxs-lookup"><span data-stu-id="d2580-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="d2580-157">這包括序列化和還原序列化 hello 使用者的資訊：</span><span class="sxs-lookup"><span data-stu-id="d2580-157">This includes serializing and deserializing hello user's information:</span></span>

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

5.  <span data-ttu-id="d2580-158">加入 hello 載入 hello Express 引擎的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d2580-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="d2580-159">使用 hello 預設 /views 和 Express 的 /routes 模式提供：</span><span class="sxs-lookup"><span data-stu-id="d2580-159">You use hello default /views and /routes pattern that Express provides:</span></span>

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

6.  <span data-ttu-id="d2580-160">新增 hello 後傳送該遞交 hello 實際的登入要求 toohello`passport-azure-ad`引擎：</span><span class="sxs-lookup"><span data-stu-id="d2580-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="d2580-161">4： 使用 Passport tooissue 登入和登出要求 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="d2580-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="d2580-162">您的應用程式現在設定 toocommunicate 與 hello v2.0 端點使用 hello OpenID Connect 的驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d2580-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="d2580-163">hello`passport-azure-ad`策略會負責所有 hello 詳細資料，製作驗證訊息、 驗證 Azure ad 的權杖和維護的 hello 使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="d2580-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="d2580-164">處於 toodo 的所有您的使用者是 toogive 方式 toosign 中的並登入和 toogather hello 使用者登入的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d2580-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="d2580-165">新增 hello**預設**，**登入**，**帳戶**，和**登出**方法 tooyour App.js 檔案：</span><span class="sxs-lookup"><span data-stu-id="d2580-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

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

  <span data-ttu-id="d2580-166">以下是 hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="d2580-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="d2580-167">hello`/`路由重新導向 toohello index.ejs 檢視。</span><span class="sxs-lookup"><span data-stu-id="d2580-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="d2580-168">它會傳入 hello 使用者 hello 要求 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="d2580-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="d2580-169">hello`/account`路由先*可確保當您驗證*（您實作，在下列程式碼的 hello）。</span><span class="sxs-lookup"><span data-stu-id="d2580-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="d2580-170">然後，它會傳入 hello 使用者 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="d2580-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="d2580-171">如此能讓您可以取得關於 hello 使用者的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d2580-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="d2580-172">hello`/login`路由呼叫您`azuread-openidconnect`驗證器，從`passport-azuread`。</span><span class="sxs-lookup"><span data-stu-id="d2580-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="d2580-173">如果不成功的它會重新導向回到 hello 使用者太`/login`。</span><span class="sxs-lookup"><span data-stu-id="d2580-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="d2580-174">hello`/logout`路由呼叫 hello logout.ejs 檢視 （和路由）。</span><span class="sxs-lookup"><span data-stu-id="d2580-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="d2580-175">這會清除 cookie，然後傳回 hello 使用者回復 tooindex.ejs。</span><span class="sxs-lookup"><span data-stu-id="d2580-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="d2580-176">新增 hello **EnsureAuthenticated**稍早在您使用的方法`/account`:</span><span class="sxs-lookup"><span data-stu-id="d2580-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

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

3.  <span data-ttu-id="d2580-177">App.js，在建立 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="d2580-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="d2580-178">5： 建立您的使用者顯示 hello 網站上的 Express 中的 hello 檢視和路由</span><span class="sxs-lookup"><span data-stu-id="d2580-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="d2580-179">加入 hello 路由和顯示資訊 toohello 使用者的檢視。</span><span class="sxs-lookup"><span data-stu-id="d2580-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="d2580-180">hello 路由和檢視表也會處理 hello`/logout`和`/login`您所建立的路由。</span><span class="sxs-lookup"><span data-stu-id="d2580-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="d2580-181">在 hello 根目錄中，建立 hello`/routes/index.js`路由。</span><span class="sxs-lookup"><span data-stu-id="d2580-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="d2580-182">在 hello 根目錄中，建立 hello`/routes/user.js`路由。</span><span class="sxs-lookup"><span data-stu-id="d2580-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="d2580-183">`/routes/index.js`和`/routes/user.js`hello 要求 tooyour 檢視，包括 hello 使用者可傳遞的簡單路由。</span><span class="sxs-lookup"><span data-stu-id="d2580-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="d2580-184">在 hello 根目錄中，建立 hello`/views/index.ejs`檢視。</span><span class="sxs-lookup"><span data-stu-id="d2580-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="d2580-185">此頁面會呼叫您的 **login** 和 **logout** 方法。</span><span class="sxs-lookup"><span data-stu-id="d2580-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="d2580-186">您也可以使用 hello`/views/index.ejs`檢視 toocapture 帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="d2580-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="d2580-187">您可以使用條件式 hello`if (!user)`身分 hello hello 要求中傳遞出去。</span><span class="sxs-lookup"><span data-stu-id="d2580-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="d2580-188">這可以證明您已經有使用者登入。</span><span class="sxs-lookup"><span data-stu-id="d2580-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="d2580-189">在 hello 根目錄中，建立 hello`/views/account.ejs`檢視。</span><span class="sxs-lookup"><span data-stu-id="d2580-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="d2580-190">hello`/views/account.ejs`檢視可讓您 tooview 其他資訊的`passport-azuread`置於 hello 使用者要求。</span><span class="sxs-lookup"><span data-stu-id="d2580-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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

5.  <span data-ttu-id="d2580-191">新增版面配置。</span><span class="sxs-lookup"><span data-stu-id="d2580-191">Add a layout.</span></span> <span data-ttu-id="d2580-192">在 hello 根目錄中，建立 hello`/views/layout.ejs`檢視。</span><span class="sxs-lookup"><span data-stu-id="d2580-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="d2580-193">toobuild 並執行應用程式執行`node app.js`。</span><span class="sxs-lookup"><span data-stu-id="d2580-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="d2580-194">然後，跳過`http://localhost:3000`。</span><span class="sxs-lookup"><span data-stu-id="d2580-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="d2580-195">使用個人 Microsoft 帳戶或是公司或學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="d2580-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="d2580-196">請注意 hello 使用者的身分識別會反映在 hello /account 清單。</span><span class="sxs-lookup"><span data-stu-id="d2580-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="d2580-197">您現在已擁有使用業界標準通訊協定保護的 Web 應用程式了。</span><span class="sxs-lookup"><span data-stu-id="d2580-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="d2580-198">您可以在應用程式中利用使用者的個人和公司或學校帳戶驗證他們的身分。</span><span class="sxs-lookup"><span data-stu-id="d2580-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2580-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2580-199">Next steps</span></span>
<span data-ttu-id="d2580-200">供參考，完成的 hello 範例 （不含您的組態值） 依現狀[.zip 檔案](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="d2580-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="d2580-201">您也可以從 GitHub 加以複製：</span><span class="sxs-lookup"><span data-stu-id="d2580-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="d2580-202">接下來，您可以移動 toomore 進階主題上。</span><span class="sxs-lookup"><span data-stu-id="d2580-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="d2580-203">您可能想 tootry:</span><span class="sxs-lookup"><span data-stu-id="d2580-203">You might want tootry:</span></span>

[<span data-ttu-id="d2580-204">藉由使用 hello v2.0 端點保護 Node.js web 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="d2580-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="d2580-205">以下是一些其他資源：</span><span class="sxs-lookup"><span data-stu-id="d2580-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="d2580-206">Azure AD v2.0 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="d2580-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="d2580-207">Stack Overflow "azure-active-directory" 標籤 (英文)</span><span class="sxs-lookup"><span data-stu-id="d2580-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d2580-208">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="d2580-208">Get security updates for our products</span></span>
<span data-ttu-id="d2580-209">我們鼓勵 toosign 向上 toobe 安全性事件發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="d2580-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="d2580-210">在 hello [Microsoft 技術安全性通知](https://technet.microsoft.com/security/dd252948)頁面上，訂閱 tooSecurity 摘要報告警示。</span><span class="sxs-lookup"><span data-stu-id="d2580-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

