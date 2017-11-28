---
title: "開始使用 Azure AD 登入和登出使用 Node.js aaaGetting |Microsoft 文件"
description: "了解如何 toobuild Node.js Express MVC web 應用程式整合與 Azure AD 進行登入。"
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="d1af2-103">搭配 Azure AD 的 Node.js Web 應用程式登入和登出</span><span class="sxs-lookup"><span data-stu-id="d1af2-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="d1af2-104">在此我們使用 Passport 來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="d1af2-104">Here we use Passport to:</span></span>

* <span data-ttu-id="d1af2-105">符號 hello toohello 應用程式與 Azure Active Directory (Azure AD) 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="d1af2-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="d1af2-106">顯示 hello 使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d1af2-106">Display information about hello user.</span></span>
* <span data-ttu-id="d1af2-107">符號 hello 使用者登出 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="d1af2-108">Passport 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="d1af2-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="d1af2-109">彈性和模組化，在 tooany 暗中卸除 Passport Express 為基礎或 restify web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="d1af2-110">一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他驗證方法。</span><span class="sxs-lookup"><span data-stu-id="d1af2-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="d1af2-111">我們已為 Microsoft Azure Active Directory 開發一項策略。</span><span class="sxs-lookup"><span data-stu-id="d1af2-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="d1af2-112">我們安裝此模組，然後新增 Microsoft Azure Active Directory hello`passport-azure-ad`外掛程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="d1af2-113">toodo 下列步驟，採用 hello:</span><span class="sxs-lookup"><span data-stu-id="d1af2-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="d1af2-114">註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-114">Register an app.</span></span>
2. <span data-ttu-id="d1af2-115">設定您的應用程式 toouse hello`passport-azure-ad`策略。</span><span class="sxs-lookup"><span data-stu-id="d1af2-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="d1af2-116">使用 Passport tooissue 登入和登出要求 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="d1af2-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="d1af2-117">列印 hello 使用者的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d1af2-117">Print data about hello user.</span></span>

<span data-ttu-id="d1af2-118">此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS)。</span><span class="sxs-lookup"><span data-stu-id="d1af2-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="d1af2-119">您可以沿著 toofollow，[下載為.zip 檔案的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip)或再製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="d1af2-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="d1af2-120">hello 完成應用程式會在本教學課程的 hello 結尾處提供。</span><span class="sxs-lookup"><span data-stu-id="d1af2-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="d1af2-121">步驟 1：註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="d1af2-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="d1af2-122">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d1af2-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="d1af2-123">在 hello 頁面頂端的 hello hello 功能表上，選取您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1af2-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="d1af2-124">在 hello**目錄**清單中，選擇您想要 tooregister hello Active Directory 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="d1af2-125">選取**更服務**hello hello 功能表留 hello 螢幕的側邊，然後選取**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="d1af2-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="d1af2-126">選取 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d1af2-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="d1af2-127">請遵循 hello 提示 toocreate **Web 應用程式**及/或**WebAPI**。</span><span class="sxs-lookup"><span data-stu-id="d1af2-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="d1af2-128">hello**名稱**hello 的應用程式描述應用程式 toousers。</span><span class="sxs-lookup"><span data-stu-id="d1af2-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="d1af2-129">hello**登入 URL**是 hello 基底 URL 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="d1af2-130">hello 基本架構的預設值是 ' http://localhost:3000/auth/openid/傳回 '。</span><span class="sxs-lookup"><span data-stu-id="d1af2-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="d1af2-131">註冊之後，Azure AD 會指派唯一的應用程式識別碼給您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="d1af2-132">您需要這個值在 hello 下列各節，因此將它從複製 hello 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="d1af2-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="d1af2-133">從 hello**設定** -> **屬性**應用程式頁面上，更新 hello 應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="d1af2-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="d1af2-134">hello**應用程式識別碼 URI**是您的應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="d1af2-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="d1af2-135">hello 慣例是 toouse hello 格式`https://<tenant-domain>/<app-name>`，例如： `https://contoso.onmicrosoft.com/my-first-aad-app`。</span><span class="sxs-lookup"><span data-stu-id="d1af2-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="d1af2-136">步驟 2： 新增必要條件 tooyour 目錄</span><span class="sxs-lookup"><span data-stu-id="d1af2-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="d1af2-137">從 hello 命令列，變更目錄 tooyour 根資料夾如果您已經不存在，然後執行的 hello 遵從命令：</span><span class="sxs-lookup"><span data-stu-id="d1af2-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="d1af2-138">此外，您需要 `passport-azure-ad`：</span><span class="sxs-lookup"><span data-stu-id="d1af2-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="d1af2-139">這會安裝 hello 程式庫，`passport-azure-ad`而定。</span><span class="sxs-lookup"><span data-stu-id="d1af2-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="d1af2-140">步驟 3： 設定您的應用程式 toouse hello passport-節點-js 策略</span><span class="sxs-lookup"><span data-stu-id="d1af2-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="d1af2-141">在這裡，我們設定 Express toouse hello OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d1af2-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="d1af2-142">Passport 是使用的 toodo 各種項目，包括問題登入和登出要求管理 hello 使用者工作階段，並取得 hello 使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d1af2-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="d1af2-143">toobegin，開啟 hello`config.js`根目錄 hello hello 專案檔案，然後輸入 hello 中的 應用程式的組態值`exports.creds`> 一節。</span><span class="sxs-lookup"><span data-stu-id="d1af2-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="d1af2-144">hello`clientID`為 hello**應用程式識別碼**這是指派的 tooyour hello 註冊入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="d1af2-145">hello`returnURL`為 hello**重新導向 Uri** hello 入口網站中輸入的。</span><span class="sxs-lookup"><span data-stu-id="d1af2-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="d1af2-146">hello`clientSecret`是您在 hello 入口網站中產生的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="d1af2-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="d1af2-147">接下來，開啟 hello `app.js` hello hello 專案根目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d1af2-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="d1af2-148">然後加入下列呼叫 tooinvoke hello hello`OIDCStrategy`隨附的策略`passport-azure-ad`。</span><span class="sxs-lookup"><span data-stu-id="d1af2-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="d1af2-149">在這之後，使用我們剛才參考 toohandle 我們登入要求的 hello 策略。</span><span class="sxs-lookup"><span data-stu-id="d1af2-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
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
<span data-ttu-id="d1af2-150">Passport 會使用適用於它的所有策略 (Twitter、Facebook 等) 且所有策略寫入器都依循的類似模式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="d1af2-151">查看 hello 策略，您會看到，我們將它傳遞具有語彙基元和完成的函式做為 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="d1af2-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="d1af2-152">其功能之後，來自回 toous hello 策略。</span><span class="sxs-lookup"><span data-stu-id="d1af2-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="d1af2-153">然後我們想要 toostore hello 使用者並存放 hello 語彙基元所以我們不需要為其 tooask 一次。</span><span class="sxs-lookup"><span data-stu-id="d1af2-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="d1af2-154">hello 先前的程式碼會發生 tooauthenticate tooour 伺服器的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="d1af2-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="d1af2-155">這就是所謂的自動註冊。</span><span class="sxs-lookup"><span data-stu-id="d1af2-155">This is known as auto-registration.</span></span> <span data-ttu-id="d1af2-156">我們建議您不要讓任何人 tooa 實際執行伺服器驗證而不需要先處理程序，當您決定透過註冊它們。</span><span class="sxs-lookup"><span data-stu-id="d1af2-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="d1af2-157">這通常是您在取用者應用程式，這可讓您與 Facebook tooregister 但然後要求 tooprovide 其他資訊，請參閱 hello 模式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="d1af2-158">如果這不範例應用程式時，我們無法從傳回並再要求其他資訊的 hello 使用者 toofill hello 權杖物件擷取有 hello 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d1af2-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="d1af2-159">因為這是在測試伺服器，我們將其加入 toohello 記憶體中資料庫。</span><span class="sxs-lookup"><span data-stu-id="d1af2-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="d1af2-160">接下來，讓我們加入可讓我們 tootrack hello 登入的使用者，所需的 Passport hello 方法。</span><span class="sxs-lookup"><span data-stu-id="d1af2-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="d1af2-161">這些方法包括序列化和還原序列化 hello 使用者的資訊。</span><span class="sxs-lookup"><span data-stu-id="d1af2-161">These methods include serializing and deserializing hello user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  <span data-ttu-id="d1af2-162">接下來，讓我們加入 hello 程式碼 tooload hello Express 引擎。</span><span class="sxs-lookup"><span data-stu-id="d1af2-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="d1af2-163">我們在此使用 hello 預設 /views 和 Express 的 /routes 模式會提供。</span><span class="sxs-lookup"><span data-stu-id="d1af2-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

    ```JavaScript

        // configure Express (section 2)

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

6. <span data-ttu-id="d1af2-164">最後，讓我們加入 hello 路由傳送該遞交 hello 實際的登入要求 toohello`passport-azure-ad`引擎：</span><span class="sxs-lookup"><span data-stu-id="d1af2-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="d1af2-165">步驟 4： 使用 Passport tooissue 登入和登出要求 tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="d1af2-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="d1af2-166">您的應用程式是現在已正確設定的 toocommunicate 與 hello 端點使用 hello OpenID Connect 的驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d1af2-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="d1af2-167">`passport-azure-ad`已處理的製作驗證訊息、 驗證 Azure ad 的權杖和維護使用者工作階段的所有 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d1af2-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="d1af2-168">所有保留是為使用者提供的方法中的 toosign 和登出，並收集 hello 登入使用者的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="d1af2-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="d1af2-169">首先，讓我們加入 hello 預設、 登入、 帳戶和登出方法 tooour`app.js`檔案：</span><span class="sxs-lookup"><span data-stu-id="d1af2-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="d1af2-170">讓我們詳細檢閱這些方法：</span><span class="sxs-lookup"><span data-stu-id="d1af2-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="d1af2-171">hello`/`路由重新導向 toohello index.ejs 檢視中，傳遞 hello 要求中的 hello 使用者 （如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="d1af2-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="d1af2-172">hello`/account`路由先*可確保我們驗證*（我們實作，在下列範例中的 hello），並傳遞然後 hello hello 要求中的使用者，以便我們可以得到 hello 使用者的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="d1af2-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="d1af2-173">hello`/login`路由呼叫我們的 azure ad openidconnect 驗證器，從`passport-azuread`。</span><span class="sxs-lookup"><span data-stu-id="d1af2-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="d1af2-174">如果不成功的它會重新導向 hello 使用者回復太/登入。</span><span class="sxs-lookup"><span data-stu-id="d1af2-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="d1af2-175">hello`/logout`路由僅呼叫 hello logout.ejs （和路由） 的清除 cookie，然後傳回 hello 使用者回復 tooindex.ejs。</span><span class="sxs-lookup"><span data-stu-id="d1af2-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="d1af2-176">Hello 最後一個部分`app.js`，讓我們加入 hello **EnsureAuthenticated**方法中使用`/account`，如稍早所示。</span><span class="sxs-lookup"><span data-stu-id="d1af2-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="d1af2-177">最後，讓我們來建立 hello 伺服器本身在`app.js`:</span><span class="sxs-lookup"><span data-stu-id="d1af2-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="d1af2-178">步驟 5: toodisplay 我們在 hello 網站上的使用者建立 hello 檢視和路由 Express</span><span class="sxs-lookup"><span data-stu-id="d1af2-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="d1af2-179">現在，`app.js` 已經完成。</span><span class="sxs-lookup"><span data-stu-id="d1af2-179">Now `app.js` is complete.</span></span> <span data-ttu-id="d1af2-180">我們只需要 tooadd hello 路由，並檢視該顯示 hello 資訊我們取得 toohello 使用者，以及處理 hello`/logout`和`/login`我們建立的路由。</span><span class="sxs-lookup"><span data-stu-id="d1af2-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="d1af2-181">建立 hello `/routes/index.js` hello 根目錄下的路由。</span><span class="sxs-lookup"><span data-stu-id="d1af2-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="d1af2-182">建立 hello `/routes/user.js` hello 根目錄下的路由。</span><span class="sxs-lookup"><span data-stu-id="d1af2-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="d1af2-183">這些可傳遞 hello 要求 tooour 檢視，包括 hello 使用者，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="d1af2-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="d1af2-184">建立 hello `/views/index.ejs` hello 根目錄下的檢視。</span><span class="sxs-lookup"><span data-stu-id="d1af2-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="d1af2-185">這是一個簡單的網頁呼叫之我們登入和登出的方法，可讓我們 toograb 帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="d1af2-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="d1af2-186">請注意，我們可以使用 hello 條件`if (!user)`由於通過 hello 要求中的 hello 使用者屬於已登入使用者的辨識項。</span><span class="sxs-lookup"><span data-stu-id="d1af2-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. <span data-ttu-id="d1af2-187">建立 hello`/views/account.ejs`檢視 hello 根目錄下，讓我們可以檢視其他資訊的`passport-azuread`已放入 hello 使用者要求。</span><span class="sxs-lookup"><span data-stu-id="d1af2-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. <span data-ttu-id="d1af2-188">新增版面配置，使它看起來更美觀。</span><span class="sxs-lookup"><span data-stu-id="d1af2-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="d1af2-189">建立 hello ' / views/layout.ejs' hello 下的檢視是根目錄。</span><span class="sxs-lookup"><span data-stu-id="d1af2-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a><span data-ttu-id="d1af2-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1af2-190">Next steps</span></span>
<span data-ttu-id="d1af2-191">最後，建置並執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1af2-191">Finally, build and run your app.</span></span> <span data-ttu-id="d1af2-192">執行`node app.js`，然後前往太`http://localhost:3000`。</span><span class="sxs-lookup"><span data-stu-id="d1af2-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="d1af2-193">使用個人 Microsoft 帳戶或是工作或學校帳戶，登入，並注意如何反映 hello /account 清單中的 hello 使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="d1af2-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="d1af2-194">您的 Web 應用程式現在使用業界標準的通訊協定保護，可以使用個人與工作/學校帳戶來驗證使用者。</span><span class="sxs-lookup"><span data-stu-id="d1af2-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="d1af2-195">如需參考，hello 完成 （不含您的組態值） 的範例[提供成.zip 檔案](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="d1af2-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="d1af2-196">或者，您也可以從 Github 複製它：</span><span class="sxs-lookup"><span data-stu-id="d1af2-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="d1af2-197">您現在可以進入更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="d1af2-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="d1af2-198">您可能想 tootry:</span><span class="sxs-lookup"><span data-stu-id="d1af2-198">You might want tootry:</span></span>

[<span data-ttu-id="d1af2-199">使用 Azure AD 保護 Web API</span><span class="sxs-lookup"><span data-stu-id="d1af2-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
