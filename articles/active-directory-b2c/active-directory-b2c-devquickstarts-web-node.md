---
title: "將登入功能新增至 Azure B2C 的 Node.js Web 應用程式 | Microsoft Docs"
description: "如何建置使用 B2C 租用戶登入使用者的 Node.js Web 應用程式。"
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
ms.openlocfilehash: c85b8f8434d1e837ac96ac63b9b37f990677ed6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="812b4-103">Azure AD B2C：將登入功能加入至 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="812b4-103">Azure AD B2C: Add sign-in to a Node.js web app</span></span>

<span data-ttu-id="812b4-104">**Passport** 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="812b4-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="812b4-105">您可以暗中將極具彈性且模組化的 Passport 安裝在任何 Express 或 Resitify Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="812b4-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="812b4-106">有一套完整的策略支援以使用者名稱和密碼、Facebook、Twitter 等來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="812b4-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="812b4-107">我們已為 Azure Active Directory (Azure AD) 開發一套策略。</span><span class="sxs-lookup"><span data-stu-id="812b4-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="812b4-108">您將會安裝此模組，然後加入 Azure AD `passport-azure-ad` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="812b4-108">You will install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="812b4-109">若要這樣做，您需要：</span><span class="sxs-lookup"><span data-stu-id="812b4-109">To do this, you need to:</span></span>

1. <span data-ttu-id="812b4-110">使用 Azure AD 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="812b4-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="812b4-111">設定應用程式以使用 `passport-azure-ad` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="812b4-111">Set up your app to use the `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="812b4-112">使用 Passport，向 Azure AD 發出登入和登出要求。</span><span class="sxs-lookup"><span data-stu-id="812b4-112">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="812b4-113">列印使用者資料。</span><span class="sxs-lookup"><span data-stu-id="812b4-113">Print user data.</span></span>

<span data-ttu-id="812b4-114">本教學課程的程式碼保留在 [GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS)。</span><span class="sxs-lookup"><span data-stu-id="812b4-114">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="812b4-115">若要跟著做，您可以[下載應用程式基本架構的 .zip 檔](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip)。</span><span class="sxs-lookup"><span data-stu-id="812b4-115">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="812b4-116">您也可以複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="812b4-116">You can also clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="812b4-117">本教學課程最後會提供完整的應用程式。</span><span class="sxs-lookup"><span data-stu-id="812b4-117">The completed application is provided at the end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="812b4-118">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="812b4-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="812b4-119">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="812b4-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="812b4-120">目錄是適用於所有使用者、app、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="812b4-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="812b4-121">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) ，再繼續進行本指南。</span><span class="sxs-lookup"><span data-stu-id="812b4-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="812b4-122">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="812b4-122">Create an application</span></span>

<span data-ttu-id="812b4-123">接著，您必須在 B2C 目錄中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="812b4-123">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="812b4-124">這會提供必要資訊給 Azure AD，讓它與應用程式安全地通訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-124">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="812b4-125">因為用戶端應用程式和 Web API 會組成一個邏輯應用程式，所以將由單一**應用程式識別碼**表示。</span><span class="sxs-lookup"><span data-stu-id="812b4-125">Both the client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="812b4-126">如果要建立應用程式，請遵循 [這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="812b4-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="812b4-127">請務必：</span><span class="sxs-lookup"><span data-stu-id="812b4-127">Be sure to:</span></span>

- <span data-ttu-id="812b4-128">在應用程式中納入 **Web 應用程式**/**Web API**。</span><span class="sxs-lookup"><span data-stu-id="812b4-128">Include a **web app**/**web API** in the application.</span></span>
- <span data-ttu-id="812b4-129">在 [回覆 URL] 中輸入 `http://localhost:3000/auth/openid/return`。</span><span class="sxs-lookup"><span data-stu-id="812b4-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="812b4-130">這是此程式碼範例的預設 URL。</span><span class="sxs-lookup"><span data-stu-id="812b4-130">It is the default URL for this code sample.</span></span>
- <span data-ttu-id="812b4-131">為您的應用程式建立 [應用程式密碼]  ，然後複製該密碼。</span><span class="sxs-lookup"><span data-stu-id="812b4-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="812b4-132">稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-132">You will need it later.</span></span> <span data-ttu-id="812b4-133">請注意，在您使用這個值之前，必須先讓該值經過 [XML 逸出](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) 。</span><span class="sxs-lookup"><span data-stu-id="812b4-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="812b4-134">複製指派給您的應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="812b4-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="812b4-135">稍後您也會需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="812b4-136">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="812b4-136">Create your policies</span></span>

<span data-ttu-id="812b4-137">在 Azure AD B2C 中，每個使用者經驗皆由 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="812b4-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="812b4-138">此應用程式包含三種身分識別體驗：註冊、登入，以及使用 Facebook 登入。</span><span class="sxs-lookup"><span data-stu-id="812b4-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="812b4-139">您必須為每個類型建立此原則，如 [原則參考文章](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)所述。</span><span class="sxs-lookup"><span data-stu-id="812b4-139">You need to create this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="812b4-140">建立您的三個原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="812b4-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="812b4-141">在註冊原則中，選擇 [顯示名稱]  和其他註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="812b4-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="812b4-142">在每個原則中，選擇 [顯示名稱] 和 [物件識別碼] 應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="812b4-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="812b4-143">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="812b4-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="812b4-144">在您建立每個原則之後，請複製原則的 [名稱]  。</span><span class="sxs-lookup"><span data-stu-id="812b4-144">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="812b4-145">其前置詞應該為 `b2c_1_`。</span><span class="sxs-lookup"><span data-stu-id="812b4-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="812b4-146">稍後您將需要這些原則名稱。</span><span class="sxs-lookup"><span data-stu-id="812b4-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="812b4-147">建立您的三個原則後，就可以開始建置您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="812b4-147">After you create your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="812b4-148">請注意，本文不會說明如何使用您剛才建立的原則。</span><span class="sxs-lookup"><span data-stu-id="812b4-148">Note that this article does not cover how to use the policies you just created.</span></span> <span data-ttu-id="812b4-149">如需了解 Azure AD B2C 中原則的運作方式，請從 [.NET Web 應用程式快速入門教學課程](active-directory-b2c-devquickstarts-web-dotnet.md)開始。</span><span class="sxs-lookup"><span data-stu-id="812b4-149">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-to-your-directory"></a><span data-ttu-id="812b4-150">在目錄中新增必要條件</span><span class="sxs-lookup"><span data-stu-id="812b4-150">Add prerequisites to your directory</span></span>

<span data-ttu-id="812b4-151">從命令列將目錄變更至根資料夾 (如果您尚未在此目錄下)。</span><span class="sxs-lookup"><span data-stu-id="812b4-151">From the command line, change directories to your root folder, if you're not already there.</span></span> <span data-ttu-id="812b4-152">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="812b4-152">Run the following commands:</span></span>

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

<span data-ttu-id="812b4-153">此外，我們在快速入門的基本架構中為預覽功能使用 `passport-azure-ad`。</span><span class="sxs-lookup"><span data-stu-id="812b4-153">In addition, we used `passport-azure-ad` for our preview in the skeleton of the Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="812b4-154">這會安裝 `passport-azure-ad` 所仰賴的程式庫。</span><span class="sxs-lookup"><span data-stu-id="812b4-154">This will install the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-to-use-the-passport-nodejs-strategy"></a><span data-ttu-id="812b4-155">設定您的應用程式以使用 Passport-Node.js 策略</span><span class="sxs-lookup"><span data-stu-id="812b4-155">Set up your app to use the Passport-Node.js strategy</span></span>
<span data-ttu-id="812b4-156">設定 Express 中介軟體以使用 OpenID Connect 驗證通訊協定。</span><span class="sxs-lookup"><span data-stu-id="812b4-156">Configure the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="812b4-157">Passport 會用來發出登入和登出要求、管理使用者工作階段，以及取得使用者相關資訊等其他動作。</span><span class="sxs-lookup"><span data-stu-id="812b4-157">Passport will be used to issue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="812b4-158">開啟專案根目錄中的 `config.js` 檔案，並在 `exports.creds` 區段中輸入應用程式的組態值。</span><span class="sxs-lookup"><span data-stu-id="812b4-158">Open the `config.js` file in the root of the project and enter your app's configuration values in the `exports.creds` section.</span></span>
- <span data-ttu-id="812b4-159">`clientID`：在註冊入口網站中指派給應用程式的**應用程式識別碼**。</span><span class="sxs-lookup"><span data-stu-id="812b4-159">`clientID`: The **Application ID** assigned to your app in the registration portal.</span></span>
- <span data-ttu-id="812b4-160">`returnURL`：在入口網站中輸入的**重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="812b4-160">`returnURL`: The **Redirect URI** you entered in the portal.</span></span>
- <span data-ttu-id="812b4-161">`tenantName`：應用程式的租用戶名稱，例如 **contoso.onmicrosoft.com**。</span><span class="sxs-lookup"><span data-stu-id="812b4-161">`tenantName`: The tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="812b4-162">開啟專案根目錄中的 `app.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="812b4-162">Open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="812b4-163">新增下列呼叫來叫用 `passport-azure-ad`隨附的 `OIDCStrategy` 策略。</span><span class="sxs-lookup"><span data-stu-id="812b4-163">Add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="812b4-164">使用剛剛參考的策略來處理登入要求。</span><span class="sxs-lookup"><span data-stu-id="812b4-164">Use the strategy you just referenced to handle sign-in requests.</span></span>

```JavaScript
// Use the OIDCStrategy in Passport (Section 2).
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
<span data-ttu-id="812b4-165">Passport 會對其所有策略 (包括 Twitter 和 Facebook) 所有類似的模式。</span><span class="sxs-lookup"><span data-stu-id="812b4-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="812b4-166">所有策略寫入器均遵守此模式。</span><span class="sxs-lookup"><span data-stu-id="812b4-166">All strategy writers adhere to this pattern.</span></span> <span data-ttu-id="812b4-167">當您查看策略時，您會發現您對其傳遞了以權杖和 `done` 做為參數的 `function()`。</span><span class="sxs-lookup"><span data-stu-id="812b4-167">When you look at the strategy, you can see that you pass it a `function()` that has a token and a `done` as the parameters.</span></span> <span data-ttu-id="812b4-168">策略在完成所有工作之後會回到您這邊。</span><span class="sxs-lookup"><span data-stu-id="812b4-168">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="812b4-169">請儲存使用者並隱藏權杖，這樣一來，您就不必再次索取。</span><span class="sxs-lookup"><span data-stu-id="812b4-169">Store the user and stash the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="812b4-170">上述程式碼會取得伺服器驗證的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="812b4-170">The preceding code takes all users whom the server authenticates.</span></span> <span data-ttu-id="812b4-171">這是自動註冊程序。</span><span class="sxs-lookup"><span data-stu-id="812b4-171">This is autoregistration.</span></span> <span data-ttu-id="812b4-172">當您使用實際執行伺服器時，您只會想讓已經完成您所設定之註冊程序的使用者進入。</span><span class="sxs-lookup"><span data-stu-id="812b4-172">When you use production servers, you don’t want to let in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="812b4-173">供消費者使用的應用程式經常會看見這種模式。</span><span class="sxs-lookup"><span data-stu-id="812b4-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="812b4-174">這些應用程式可讓您使用 Facebook 進行註冊，但是接著會要求您填寫其他資訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-174">These allow you to register by using Facebook, but then they ask you to fill out additional information.</span></span> <span data-ttu-id="812b4-175">如果我們的應用程式不是範例應用程式，我們可以從傳回的權杖物件中擷取電子郵件地址，然後要求使用者填寫其他資訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-175">If our application wasn’t a sample, we could extract an email address from the token object that is returned, and then ask the user to fill out additional information.</span></span> <span data-ttu-id="812b4-176">由於這是測試伺服器，因此我們只會將使用者加入記憶體中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="812b4-176">Because this is a test server, we simply add users to the in-memory database.</span></span>

<span data-ttu-id="812b4-177">新增方法以讓您可以按照 Passport 所要求地追蹤已登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="812b4-177">Add the methods that allow you to keep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="812b4-178">這包括將使用者資訊序列化和還原序列化：</span><span class="sxs-lookup"><span data-stu-id="812b4-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   To support persistent sign-in sessions, Passport needs to be able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing the user ID when Passport serializes a user
//   and finding the user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array to hold users who have signed in
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

<span data-ttu-id="812b4-179">加入可載入 Express 引擎的程式碼。</span><span class="sxs-lookup"><span data-stu-id="812b4-179">Add the code to load the Express engine.</span></span> <span data-ttu-id="812b4-180">您可以在下列命令中看到，我們使用 Express 提供的預設 `/views` 和 `/routes` 模式。</span><span class="sxs-lookup"><span data-stu-id="812b4-180">In the following, you can see that we use the default `/views` and `/routes` pattern that Express provides.</span></span>

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
  // Initialize Passport!  Also use passport.session() middleware to support
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="812b4-181">新增 `POST` 路由以將實際的登入要求遞交給 `passport-azure-ad` 引擎：</span><span class="sxs-lookup"><span data-stu-id="812b4-181">Add the `POST` routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware to authenticate the
//   request. The first step in OpenID authentication involves redirecting
//   the user to an OpenID provider. After the user is authenticated,
//   the OpenID provider redirects the user back to this application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in the Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it redirects the user to the home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it will redirect the user to the home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="812b4-182">使用 Passport，向 Azure AD 發出登入和登出要求</span><span class="sxs-lookup"><span data-stu-id="812b4-182">Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>

<span data-ttu-id="812b4-183">您的應用程式現在已正確設定，將使用 OpenID Connect 驗證通訊協定與 v2.0 端點通訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-183">Your app is now properly configured to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="812b4-184">`passport-azure-ad` 已經處理有關製作驗證訊息、驗證 Azure AD 的權杖和維護使用者工作階段的細節。</span><span class="sxs-lookup"><span data-stu-id="812b4-184">`passport-azure-ad` has taken care of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="812b4-185">剩下的工作就是讓使用者有辦法登入和登出，以及收集關於已登入使用者的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-185">All that remains is to give your users a way to sign in and sign out, and to gather additional information on users who have signed in.</span></span>

<span data-ttu-id="812b4-186">首先，在 `app.js` 檔案中加入預設、登入、帳戶和登出方法：</span><span class="sxs-lookup"><span data-stu-id="812b4-186">First, add the default, sign-in, account, and sign-out methods to your `app.js` file:</span></span>

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
    log.info('Login was called in the Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="812b4-187">若要詳細檢閱這些方法：</span><span class="sxs-lookup"><span data-stu-id="812b4-187">To review these methods in detail:</span></span>
- <span data-ttu-id="812b4-188">`/` 會在要求中傳遞使用者 (若有的話) 以將重新導向路由至 `index.ejs` 檢視。</span><span class="sxs-lookup"><span data-stu-id="812b4-188">The `/` route redirects to the `index.ejs` view by passing the user in the request (if it exists).</span></span>
- <span data-ttu-id="812b4-189">`/account` 路由會先確認您已通過驗證 (下面有這個程序的實作)。</span><span class="sxs-lookup"><span data-stu-id="812b4-189">The `/account` route first verifies that you are authenticated (the implementation for this is below).</span></span> <span data-ttu-id="812b4-190">然後在要求中傳遞使用者，以讓您取得使用者的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-190">It then passes the user in the request so that you can get additional information about the user.</span></span>
- <span data-ttu-id="812b4-191">`/login` 會從 `passport-azure-ad` 將呼叫路由到 `azuread-openidconnect` 驗證器。</span><span class="sxs-lookup"><span data-stu-id="812b4-191">The `/login` route calls the `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="812b4-192">如果沒有成功，路由便會將使用者重新導向回 `/login`。</span><span class="sxs-lookup"><span data-stu-id="812b4-192">If it doesn't succeed, the route redirects the user back to `/login`.</span></span>
- <span data-ttu-id="812b4-193">`/logout` 只會呼叫 `logout.ejs` (和其路由)。</span><span class="sxs-lookup"><span data-stu-id="812b4-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="812b4-194">這會清除 Cookie，然後讓使用者回到 `index.ejs`。</span><span class="sxs-lookup"><span data-stu-id="812b4-194">This clears cookies and then returns the user back to `index.ejs`.</span></span>


<span data-ttu-id="812b4-195">`app.js` 的最後一個部分是新增 `/account` 路由中使用的 `EnsureAuthenticated` 方法。</span><span class="sxs-lookup"><span data-stu-id="812b4-195">For the last part of `app.js`, add the `EnsureAuthenticated` method that is used in the `/account` route.</span></span>

```JavaScript

// Simple route middleware to ensure that the user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs to be protected. If
//   the request is authenticated (typically via a persistent sign-in session),
//   then the request will proceed. Otherwise, the user will be redirected to the
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="812b4-196">最後，在 `app.js` 中建立伺服器本身。</span><span class="sxs-lookup"><span data-stu-id="812b4-196">Finally, create the server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-the-views-and-routes-in-express-to-call-your-policies"></a><span data-ttu-id="812b4-197">在 Express 中建立檢視和路由以呼叫原則</span><span class="sxs-lookup"><span data-stu-id="812b4-197">Create the views and routes in Express to call your policies</span></span>

<span data-ttu-id="812b4-198">`app.js` 現已完成。</span><span class="sxs-lookup"><span data-stu-id="812b4-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="812b4-199">您只需要加入路由和檢視以讓您呼叫登入和註冊原則。</span><span class="sxs-lookup"><span data-stu-id="812b4-199">You just need to add the routes and views that allow you to call the sign-in and sign-up policies.</span></span> <span data-ttu-id="812b4-200">這些項目也會處理您所建立的 `/logout` 和 `/login` 路由。</span><span class="sxs-lookup"><span data-stu-id="812b4-200">These also handle the `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="812b4-201">在根目錄下方建立 `/routes/index.js` 路由。</span><span class="sxs-lookup"><span data-stu-id="812b4-201">Create the `/routes/index.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="812b4-202">在根目錄下方建立 `/routes/user.js` 路由。</span><span class="sxs-lookup"><span data-stu-id="812b4-202">Create the `/routes/user.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="812b4-203">這些簡單的路由會傳遞要求到您的檢視。</span><span class="sxs-lookup"><span data-stu-id="812b4-203">These simple routes pass along requests to your views.</span></span> <span data-ttu-id="812b4-204">要求中包含使用者 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="812b4-204">They include the user, if one is present.</span></span>

<span data-ttu-id="812b4-205">在根目錄底下建立 `/views/index.ejs` 檢視。</span><span class="sxs-lookup"><span data-stu-id="812b4-205">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="812b4-206">這是呼叫登入和登出原則的簡單網頁。</span><span class="sxs-lookup"><span data-stu-id="812b4-206">This is a simple page that calls policies for sign-in and sign-out.</span></span> <span data-ttu-id="812b4-207">您也可以用它來擷取帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-207">You can also use it to grab account information.</span></span> <span data-ttu-id="812b4-208">請注意，因為會在要求中傳遞使用者以提供使用者已登入的證明，因此您可以使用條件式 `if (!user)`。</span><span class="sxs-lookup"><span data-stu-id="812b4-208">Note that you can use the conditional `if (!user)` as the user is passed through in the request to provide evidence that the user is signed in.</span></span>

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

<span data-ttu-id="812b4-209">在根目錄下方建立 `/views/account.ejs` 檢視，如此即可檢視 `passport-azure-ad` 放置於使用者要求的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="812b4-209">Create the `/views/account.ejs` view under the root directory so that you can view additional information that `passport-azure-ad` put in the user request.</span></span>

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

<span data-ttu-id="812b4-210">現在您可以建立並執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="812b4-210">You can now build and run your app.</span></span>

<span data-ttu-id="812b4-211">執行 `node app.js` 並瀏覽至 `http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="812b4-211">Run `node app.js` and navigate to `http://localhost:3000`</span></span>


<span data-ttu-id="812b4-212">使用電子郵件或 Facebook 註冊或登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="812b4-212">Sign up or sign in to the app by using email or Facebook.</span></span> <span data-ttu-id="812b4-213">登出後，再以不同使用者身分重新登入。</span><span class="sxs-lookup"><span data-stu-id="812b4-213">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="812b4-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="812b4-214">Next steps</span></span>

<span data-ttu-id="812b4-215">[這裡以 .zip 檔案提供](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip)完整範例 (不含您的設定值) 供您參考。</span><span class="sxs-lookup"><span data-stu-id="812b4-215">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="812b4-216">您也可以從 Github 複製它：</span><span class="sxs-lookup"><span data-stu-id="812b4-216">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="812b4-217">您現在可以繼續前進到更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="812b4-217">You can now move on to more advanced topics.</span></span> <span data-ttu-id="812b4-218">您可以嘗試：</span><span class="sxs-lookup"><span data-stu-id="812b4-218">You might try:</span></span>

[<span data-ttu-id="812b4-219">使用 Node.js 中的 B2C 模型保護 Web API 安全</span><span class="sxs-lookup"><span data-stu-id="812b4-219">Secure a web API by using the B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on to more advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing the your B2C App's UX >>]()

-->
