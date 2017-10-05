---
title: "Azure Active Directory v2.0 Node.js Web 應用程式登入 | Microsoft Docs"
description: "了解如何建置可使用個人 Microsoft 帳戶及公司或學校帳戶將使用者登入的 Node.js Web 應用程式。"
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
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="6bdec-103">將登入新增至 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6bdec-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="6bdec-104">並非所有的 Azure Active Directory 案例和功能都可以和 v2.0 端點搭配使用。</span><span class="sxs-lookup"><span data-stu-id="6bdec-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="6bdec-105">若要判斷您應該使用 v2.0 端點或 v1.0 端點，請參閱 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="6bdec-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="6bdec-106">在本教學課程中，我們會使用 Passport 執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="6bdec-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="6bdec-107">在 Web 應用程式中，使用 Azure Active Directory (Azure AD) 和 v2.0 端點將使用者登入。</span><span class="sxs-lookup"><span data-stu-id="6bdec-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="6bdec-108">顯示使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-108">Display information about the user.</span></span>
* <span data-ttu-id="6bdec-109">讓使用者登出 App。</span><span class="sxs-lookup"><span data-stu-id="6bdec-109">Sign the user out of the app.</span></span>

<span data-ttu-id="6bdec-110">**Passport** 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="6bdec-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="6bdec-111">您可以暗中將極具彈性且模組化的 Passport 放入任何 Express 架構或 resitify Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bdec-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="6bdec-112">在 Passport 中，一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他選項進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6bdec-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="6bdec-113">我們已為 Azure AD 開發一個策略。</span><span class="sxs-lookup"><span data-stu-id="6bdec-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="6bdec-114">在本文中，我們會向您說明如何安裝模組，然後新增 Azure AD `passport-azure-ad` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="6bdec-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="6bdec-115">下載</span><span class="sxs-lookup"><span data-stu-id="6bdec-115">Download</span></span>
<span data-ttu-id="6bdec-116">本教學課程的程式碼保留在 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs)。</span><span class="sxs-lookup"><span data-stu-id="6bdec-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="6bdec-117">若要依照教學課程執行，您可以[下載應用程式基本架構的 .zip 檔案](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip)，或複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="6bdec-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="6bdec-118">您也可以在本教學課程結束時取得完整的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bdec-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="6bdec-119">1：註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="6bdec-119">1: Register an app</span></span>
<span data-ttu-id="6bdec-120">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循[這些詳細步驟](active-directory-v2-app-registration.md)來註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bdec-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="6bdec-121">請確定您已執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6bdec-121">Make sure you:</span></span>

* <span data-ttu-id="6bdec-122">複製指派給您應用程式的「應用程式識別碼」。</span><span class="sxs-lookup"><span data-stu-id="6bdec-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="6bdec-123">您在本教學課程中會需要用到。</span><span class="sxs-lookup"><span data-stu-id="6bdec-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="6bdec-124">為您的應用程式新增 **Web** 平台。</span><span class="sxs-lookup"><span data-stu-id="6bdec-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="6bdec-125">複製入口網站的「重新導向 URI」  。</span><span class="sxs-lookup"><span data-stu-id="6bdec-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="6bdec-126">您必須使用預設 URI 值：`urn:ietf:wg:oauth:2.0:oob`。</span><span class="sxs-lookup"><span data-stu-id="6bdec-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="6bdec-127">2：將必要條件新增至目錄</span><span class="sxs-lookup"><span data-stu-id="6bdec-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="6bdec-128">在命令提示字元中，將目錄變更至根資料夾 (如果您尚未在此目錄下)。</span><span class="sxs-lookup"><span data-stu-id="6bdec-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="6bdec-129">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="6bdec-129">Run the following commands:</span></span>

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

<span data-ttu-id="6bdec-130">此外，我們會在快速入門的基本架構中使用 `passport-azure-ad`：</span><span class="sxs-lookup"><span data-stu-id="6bdec-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="6bdec-131">這會安裝 `passport-azure-ad` 所使用的程式庫。</span><span class="sxs-lookup"><span data-stu-id="6bdec-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="6bdec-132">3：設定您的應用程式以使用 passport-node-js 策略</span><span class="sxs-lookup"><span data-stu-id="6bdec-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="6bdec-133">設定 Express 中介軟體以使用 OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="6bdec-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6bdec-134">您會使用 Passport 來發出登入和登出要求、管理使用者的工作階段，以及取得使用者相關資訊等作業。</span><span class="sxs-lookup"><span data-stu-id="6bdec-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="6bdec-135">開啟專案根目錄中的 Config.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="6bdec-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="6bdec-136">在 `exports.creds` 區段中，輸入您應用程式的設定值。</span><span class="sxs-lookup"><span data-stu-id="6bdec-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="6bdec-137">`clientID`：在 Azure 入口網站中指派給您應用程式的「應用程式識別碼」。</span><span class="sxs-lookup"><span data-stu-id="6bdec-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="6bdec-138">`returnURL`：您在入口網站中輸入的「重新導向 URI」。</span><span class="sxs-lookup"><span data-stu-id="6bdec-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="6bdec-139">`clientSecret`：您在入口網站中產生的密碼。</span><span class="sxs-lookup"><span data-stu-id="6bdec-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="6bdec-140">開啟專案根目錄中的 App.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="6bdec-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="6bdec-141">若要叫用隨附於 `passport-azure-ad` 的 OIDCStrategy 策略，請新增以下呼叫：</span><span class="sxs-lookup"><span data-stu-id="6bdec-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="6bdec-142">若要處理登入要求，請使用剛剛參考的策略：</span><span class="sxs-lookup"><span data-stu-id="6bdec-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
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

<span data-ttu-id="6bdec-143">Passport 會針對其所有策略 (Twitter、Facebook 等) 使用類似的模式。</span><span class="sxs-lookup"><span data-stu-id="6bdec-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="6bdec-144">所有策略寫入器均遵守此模式。</span><span class="sxs-lookup"><span data-stu-id="6bdec-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="6bdec-145">將使用權杖和 `done` 作為參數的 `function()` 傳遞給策略。</span><span class="sxs-lookup"><span data-stu-id="6bdec-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="6bdec-146">策略會在完成所有工作之後傳回。</span><span class="sxs-lookup"><span data-stu-id="6bdec-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="6bdec-147">請儲存使用者並隱藏權杖，這樣一來，您就不必再次要求它。</span><span class="sxs-lookup"><span data-stu-id="6bdec-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="6bdec-148">上述程式碼會將可通過驗證的所有使用者帶往您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6bdec-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="6bdec-149">這就是所謂的自動註冊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-149">This is known as auto-registration.</span></span> <span data-ttu-id="6bdec-150">在生產伺服器中，您應該會想要讓所有人都必須先完成您選擇的註冊過程，才能進入您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6bdec-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="6bdec-151">這是您通常會在消費者應用程式中看到的模式。</span><span class="sxs-lookup"><span data-stu-id="6bdec-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="6bdec-152">應用程式可能會允許您使用 Facebook 進行註冊，但之後會要求您輸入其他資訊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="6bdec-153">如果您沒有針對本教學課程使用命令列程式，可以從傳回的權杖物件中擷取電子郵件。</span><span class="sxs-lookup"><span data-stu-id="6bdec-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="6bdec-154">然後，您可能會要求使用者輸入其他資訊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="6bdec-155">由於這是測試伺服器，您會將使用者直接加入記憶體中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6bdec-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="6bdec-156">按照 Passport 的要求，新增可用來追蹤已登入使用者的方法。</span><span class="sxs-lookup"><span data-stu-id="6bdec-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="6bdec-157">這包括將使用者資訊序列化和還原序列化：</span><span class="sxs-lookup"><span data-stu-id="6bdec-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
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

5.  <span data-ttu-id="6bdec-158">新增可載入 Express 引擎的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bdec-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="6bdec-159">您可以使用 Express 所提供的預設 /views 和 /routes 模式：</span><span class="sxs-lookup"><span data-stu-id="6bdec-159">You use the default /views and /routes pattern that Express provides:</span></span>

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
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="6bdec-160">新增 POST 路由以將實際的登入要求遞交給 `passport-azure-ad` 引擎：</span><span class="sxs-lookup"><span data-stu-id="6bdec-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="6bdec-161">4：使用 Passport，向 Azure AD 發出登入和登出要求</span><span class="sxs-lookup"><span data-stu-id="6bdec-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="6bdec-162">您的應用程式現在已設定為可使用 OpenID Connect 驗證通訊協定與 v2.0 端點通訊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6bdec-163">`passport-azure-ad` 策略會處理有關製作驗證訊息、驗證來自 Azure AD 的權杖，以及維護使用者工作階段的所有細節。</span><span class="sxs-lookup"><span data-stu-id="6bdec-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="6bdec-164">剩下的工作就是提供使用者登入和登出的方法，以及收集關於已登入使用者的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="6bdec-165">首先，將 **default**、**login**、**account** 及 **logout** 方法加入 App.js 檔案：</span><span class="sxs-lookup"><span data-stu-id="6bdec-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

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
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="6bdec-166">詳細資料如下：</span><span class="sxs-lookup"><span data-stu-id="6bdec-166">Here are the details:</span></span>
    
    * <span data-ttu-id="6bdec-167">`/` 路由會重新導向到 index.ejs 檢視。</span><span class="sxs-lookup"><span data-stu-id="6bdec-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="6bdec-168">它會在要求 (如果有的話) 中傳遞使用者。</span><span class="sxs-lookup"><span data-stu-id="6bdec-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="6bdec-169">`/account` 路由會先「確保您已通過驗證」 (您會在以下程式碼中實作此功能)。</span><span class="sxs-lookup"><span data-stu-id="6bdec-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="6bdec-170">然後，它會在要求中傳遞使用者。</span><span class="sxs-lookup"><span data-stu-id="6bdec-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="6bdec-171">這可讓您取得更多有關該使用者的資訊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="6bdec-172">`/login` 路由會從 `passport-azuread` 呼叫您的 `azuread-openidconnect` 驗證器。</span><span class="sxs-lookup"><span data-stu-id="6bdec-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="6bdec-173">如果沒有成功，路由便會將使用者重新導向回 `/login`。</span><span class="sxs-lookup"><span data-stu-id="6bdec-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="6bdec-174">`/logout` 路由會呼叫 logout.ejs 檢視 (並進行路由)。</span><span class="sxs-lookup"><span data-stu-id="6bdec-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="6bdec-175">這會清除 Cookie，然後讓使用者回到 index.ejs。</span><span class="sxs-lookup"><span data-stu-id="6bdec-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="6bdec-176">新增您之前在 `/account` 中使用的 **EnsureAuthenticated** 方法：</span><span class="sxs-lookup"><span data-stu-id="6bdec-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="6bdec-177">在 App.js 中建立伺服器：</span><span class="sxs-lookup"><span data-stu-id="6bdec-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="6bdec-178">5：在 Express 中建立會在網站中向使用者顯示的檢視與路由</span><span class="sxs-lookup"><span data-stu-id="6bdec-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="6bdec-179">新增向使用者顯示資訊的路由和檢視。</span><span class="sxs-lookup"><span data-stu-id="6bdec-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="6bdec-180">路由和檢視也會處理您建立的 `/logout` 和 `/login` 路由。</span><span class="sxs-lookup"><span data-stu-id="6bdec-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="6bdec-181">在根目錄中建立 `/routes/index.js` 路由。</span><span class="sxs-lookup"><span data-stu-id="6bdec-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="6bdec-182">在根目錄中建立 `/routes/user.js` 路由。</span><span class="sxs-lookup"><span data-stu-id="6bdec-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="6bdec-183">`/routes/index.js` 和 `/routes/user.js` 為簡易路由，會將要求 (如果有的話) 一起傳遞至您的檢視，包括使用者。</span><span class="sxs-lookup"><span data-stu-id="6bdec-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="6bdec-184">在根目錄中建立 `/views/index.ejs` 檢視。</span><span class="sxs-lookup"><span data-stu-id="6bdec-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="6bdec-185">此頁面會呼叫您的 **login** 和 **logout** 方法。</span><span class="sxs-lookup"><span data-stu-id="6bdec-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="6bdec-186">您也會使用 `/views/index.ejs` 檢視來擷取帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="6bdec-187">您可以使用條件式 `if (!user)` 做為在要求中傳遞的使用者。</span><span class="sxs-lookup"><span data-stu-id="6bdec-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="6bdec-188">這可以證明您已經有使用者登入。</span><span class="sxs-lookup"><span data-stu-id="6bdec-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="6bdec-189">在根目錄中建立 `/views/account.ejs` 檢視。</span><span class="sxs-lookup"><span data-stu-id="6bdec-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="6bdec-190">`/views/account.ejs` 檢視可允許您檢視 `passport-azuread` 置於使用者要求中的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="6bdec-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

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

5.  <span data-ttu-id="6bdec-191">新增版面配置。</span><span class="sxs-lookup"><span data-stu-id="6bdec-191">Add a layout.</span></span> <span data-ttu-id="6bdec-192">在根目錄中建立 `/views/layout.ejs` 檢視。</span><span class="sxs-lookup"><span data-stu-id="6bdec-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="6bdec-193">若要建置並執行您的應用程式，請執行 `node app.js`。</span><span class="sxs-lookup"><span data-stu-id="6bdec-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="6bdec-194">然後前往 `http://localhost:3000`。</span><span class="sxs-lookup"><span data-stu-id="6bdec-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="6bdec-195">使用個人 Microsoft 帳戶或是公司或學校帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="6bdec-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="6bdec-196">請注意，使用者的身分識別會反映在 /account 清單中。</span><span class="sxs-lookup"><span data-stu-id="6bdec-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="6bdec-197">您現在已擁有使用業界標準通訊協定保護的 Web 應用程式了。</span><span class="sxs-lookup"><span data-stu-id="6bdec-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="6bdec-198">您可以在應用程式中利用使用者的個人和公司或學校帳戶驗證他們的身分。</span><span class="sxs-lookup"><span data-stu-id="6bdec-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bdec-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bdec-199">Next steps</span></span>
<span data-ttu-id="6bdec-200">做為參考，我們以 [.zip 檔案](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip)的形式提供已完成的範例 (不含您的設定值)。</span><span class="sxs-lookup"><span data-stu-id="6bdec-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="6bdec-201">您也可以從 GitHub 加以複製：</span><span class="sxs-lookup"><span data-stu-id="6bdec-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="6bdec-202">接下來，您可以進入更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="6bdec-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="6bdec-203">您可能想嘗試：</span><span class="sxs-lookup"><span data-stu-id="6bdec-203">You might want to try:</span></span>

[<span data-ttu-id="6bdec-204">使用 v2.0 端點保護 Node.js Web API</span><span class="sxs-lookup"><span data-stu-id="6bdec-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="6bdec-205">以下是一些其他資源：</span><span class="sxs-lookup"><span data-stu-id="6bdec-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="6bdec-206">Azure AD v2.0 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="6bdec-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="6bdec-207">Stack Overflow "azure-active-directory" 標籤 (英文)</span><span class="sxs-lookup"><span data-stu-id="6bdec-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="6bdec-208">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="6bdec-208">Get security updates for our products</span></span>
<span data-ttu-id="6bdec-209">我們建議您註冊，即可在發生安全性事件時收到通知。</span><span class="sxs-lookup"><span data-stu-id="6bdec-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="6bdec-210">請在 [Microsoft 技術安全性通知](https://technet.microsoft.com/security/dd252948)頁面上，訂閱資訊安全摘要報告警示。</span><span class="sxs-lookup"><span data-stu-id="6bdec-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

