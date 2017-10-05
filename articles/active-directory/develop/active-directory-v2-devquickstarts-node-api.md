---
title: "使用 Node.js 保護 Azure Active Directory v2.0 Web API 安全 | Microsoft Docs"
description: "了解如何建置 .Node.js Web API 應用程式，以接受來自個人 Microsoft 帳戶及公司或學校帳戶的權杖。"
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 94e945a52b9df7c495de1611baa08083357670c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="1395e-103">使用 Node.js 保護 Web API 安全</span><span class="sxs-lookup"><span data-stu-id="1395e-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="1395e-104">並非所有的 Azure Active Directory 案例和功能都可以和 v2.0 端點搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1395e-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="1395e-105">若要判斷您應該使用 v2.0 端點或 v1.0 端點，請參閱 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="1395e-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="1395e-106">當您使用 Azure Active Directory (Azure AD) v2.0 端點時，您可以使用 [OAuth 2.0](active-directory-v2-protocols.md) 存取權杖來保護您的 Web API。</span><span class="sxs-lookup"><span data-stu-id="1395e-106">When you use the Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens to protect your web API.</span></span> <span data-ttu-id="1395e-107">如果使用者同時有個人 Microsoft 帳戶及公司或學校帳戶，只要透過 OAuth 2.0 存取權杖，就能安全地存取您的 Web API。</span><span class="sxs-lookup"><span data-stu-id="1395e-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="1395e-108">*Passport* 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="1395e-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="1395e-109">您可以暗中將極具彈性且模組化的 Passport 放入任何 Express 架構或 resitify Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1395e-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="1395e-110">在 Passport 中，一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他選項進行驗證。</span><span class="sxs-lookup"><span data-stu-id="1395e-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="1395e-111">我們已為 Azure AD 開發一個策略。</span><span class="sxs-lookup"><span data-stu-id="1395e-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="1395e-112">在本文中，我們會向您說明如何安裝模組，然後新增 Azure AD `passport-azure-ad` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="1395e-112">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="1395e-113">下載</span><span class="sxs-lookup"><span data-stu-id="1395e-113">Download</span></span>
<span data-ttu-id="1395e-114">本教學課程的程式碼保留在 [GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs)。</span><span class="sxs-lookup"><span data-stu-id="1395e-114">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="1395e-115">若要依照教學課程執行，您可以[下載應用程式基本架構的 .zip 檔](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip)，或複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="1395e-115">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="1395e-116">您也可以在本教學課程結束時取得完整的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1395e-116">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="1395e-117">1：註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="1395e-117">1: Register an app</span></span>
<span data-ttu-id="1395e-118">在 [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立新的應用程式，或遵循[這些詳細步驟](active-directory-v2-app-registration.md)來註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="1395e-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="1395e-119">請確定您已執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="1395e-119">Make sure you:</span></span>

* <span data-ttu-id="1395e-120">複製指派給您的應用程式的「應用程式識別碼」。</span><span class="sxs-lookup"><span data-stu-id="1395e-120">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="1395e-121">您在本教學課程中將需要用到它。</span><span class="sxs-lookup"><span data-stu-id="1395e-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="1395e-122">為您的應用程式新增 **行動** 平台。</span><span class="sxs-lookup"><span data-stu-id="1395e-122">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="1395e-123">複製入口網站的「重新導向 URI」  。</span><span class="sxs-lookup"><span data-stu-id="1395e-123">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="1395e-124">您必須使用預設 URI 值 `urn:ietf:wg:oauth:2.0:oob`。</span><span class="sxs-lookup"><span data-stu-id="1395e-124">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="1395e-125">2：安裝 Node.js</span><span class="sxs-lookup"><span data-stu-id="1395e-125">2: Install Node.js</span></span>
<span data-ttu-id="1395e-126">若要使用本教學課程的範例，您必須[安裝 Node.js](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="1395e-126">To use the sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="1395e-127">3︰安裝 MongoDB</span><span class="sxs-lookup"><span data-stu-id="1395e-127">3: Install MongoDB</span></span>
<span data-ttu-id="1395e-128">若要成功使用此範例，您必須[安裝 MongoDB](http://www.mongodb.org)。</span><span class="sxs-lookup"><span data-stu-id="1395e-128">To successfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="1395e-129">在此範例中，您將會使用 MongoDB，讓 REST API 得以在不同伺服器執行個體之間持續使用。</span><span class="sxs-lookup"><span data-stu-id="1395e-129">In this sample, you use MongoDB to make your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="1395e-130">在本文中，我們假設您使用 MongoDB 的預設安裝和伺服器端點︰mongodb://localhost。</span><span class="sxs-lookup"><span data-stu-id="1395e-130">In this article, we assume that you use the default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="1395e-131">4：在您的 Web API 中安裝 restify 模組</span><span class="sxs-lookup"><span data-stu-id="1395e-131">4: Install the restify modules in your web API</span></span>
<span data-ttu-id="1395e-132">我們會使用 Resitfy 來建置 REST API。</span><span class="sxs-lookup"><span data-stu-id="1395e-132">We use Resitfy to build our REST API.</span></span> <span data-ttu-id="1395e-133">Restify 是衍生自 Express 的最小且具彈性的 Node.js 應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="1395e-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="1395e-134">Restify 提供一組強大的功能，可讓您以 Connect 為基礎來建置 REST API。</span><span class="sxs-lookup"><span data-stu-id="1395e-134">Restify has a robust set of features that you can use to build REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="1395e-135">安裝 restify</span><span class="sxs-lookup"><span data-stu-id="1395e-135">Install restify</span></span>
1.  <span data-ttu-id="1395e-136">在命令提示字元中，將目錄切換至 **azuread**：</span><span class="sxs-lookup"><span data-stu-id="1395e-136">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="1395e-137">如果 **azuread** 目錄不存在，請予以建立：</span><span class="sxs-lookup"><span data-stu-id="1395e-137">If the **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="1395e-138">安裝 restify：</span><span class="sxs-lookup"><span data-stu-id="1395e-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="1395e-139">這個命令的輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="1395e-139">The output of this command should look like this:</span></span>

    ```
    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a><span data-ttu-id="1395e-140">您有收到錯誤訊息嗎？</span><span class="sxs-lookup"><span data-stu-id="1395e-140">Did you get an error?</span></span>
<span data-ttu-id="1395e-141">在某些作業系統上，當您使用 `npm` 命令時，您可能會看到此訊息︰`Error: EPERM, chmod '/usr/local/bin/..'`。</span><span class="sxs-lookup"><span data-stu-id="1395e-141">On some operating systems, when you use the `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="1395e-142">如果您嘗試要求以系統管理員身分執行帳戶，則會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1395e-142">The error is followed by a request that you try running the account as an administrator.</span></span> <span data-ttu-id="1395e-143">若發生此這個情況，請使用 `sudo` 命令，以更高的權限層級執行 `npm`。</span><span class="sxs-lookup"><span data-stu-id="1395e-143">If this occurs, use the command `sudo` to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-to-dtrace"></a><span data-ttu-id="1395e-144">您有收到 DTrace 的相關錯誤嗎？</span><span class="sxs-lookup"><span data-stu-id="1395e-144">Did you get an error related to DTrace?</span></span>
<span data-ttu-id="1395e-145">當您安裝 restify 時，您可能會看到此訊息︰</span><span class="sxs-lookup"><span data-stu-id="1395e-145">When you install restify, you might see this message:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

<span data-ttu-id="1395e-146">Restify 有強大的機制可使用 DTrace 追蹤 REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="1395e-146">Restify has a powerful mechanism to trace REST calls by using DTrace.</span></span> <span data-ttu-id="1395e-147">不過，在許多作業系統上無法使用 DTrace。</span><span class="sxs-lookup"><span data-stu-id="1395e-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="1395e-148">您可以放心地忽略此錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="1395e-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="1395e-149">5：在您的 Web API 中安裝 Passport.js</span><span class="sxs-lookup"><span data-stu-id="1395e-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="1395e-150">在命令提示字元中，將目錄切換至 **azuread**。</span><span class="sxs-lookup"><span data-stu-id="1395e-150">At the command prompt, change the directory to **azuread**.</span></span>

2.  <span data-ttu-id="1395e-151">安裝 Passport.js：</span><span class="sxs-lookup"><span data-stu-id="1395e-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="1395e-152">這個命令的輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="1395e-152">The output of the command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="1395e-153">6：將 passport-azure-ad 新增至您的 Web API</span><span class="sxs-lookup"><span data-stu-id="1395e-153">6: Add passport-azure-ad to your web API</span></span>
<span data-ttu-id="1395e-154">接下來，使用 passport-azuread 新增 OAuth 策略。</span><span class="sxs-lookup"><span data-stu-id="1395e-154">Next, add the OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="1395e-155">`passport-azuread` 是一套將 Azure AD 連線至 Passport 的策略。</span><span class="sxs-lookup"><span data-stu-id="1395e-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="1395e-156">在這個 Rest API 範例中，我們會對持有人權杖使用此策略。</span><span class="sxs-lookup"><span data-stu-id="1395e-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="1395e-157">雖然 OAuth2.0 提供可發行任何已知權杖類型的架構，但只有某些權杖類型經常使用。</span><span class="sxs-lookup"><span data-stu-id="1395e-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="1395e-158">持有人權杖通常用於保護端點。</span><span class="sxs-lookup"><span data-stu-id="1395e-158">Bearer tokens are commonly used to protect endpoints.</span></span> <span data-ttu-id="1395e-159">持有人權杖是 OAuth 2.0 中最普遍發行的權杖類型。</span><span class="sxs-lookup"><span data-stu-id="1395e-159">Bearer tokens are the most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="1395e-160">許多 OAuth 2.0 實作會假設持有者權杖是唯一發行的權杖類型。</span><span class="sxs-lookup"><span data-stu-id="1395e-160">Many OAuth 2.0 implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="1395e-161">在命令提示字元中，將目錄切換至 **azuread**。</span><span class="sxs-lookup"><span data-stu-id="1395e-161">At a command prompt, change the directory to **azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="1395e-162">安裝 Passport.js `passport-azure-ad` 模組︰</span><span class="sxs-lookup"><span data-stu-id="1395e-162">Install the Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="1395e-163">這個命令的輸出如下所示：</span><span class="sxs-lookup"><span data-stu-id="1395e-163">The output of the command should look like this:</span></span>

    ```
    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
    ```

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="1395e-164">7：將 MongoDB 模組新增至您的 Web API</span><span class="sxs-lookup"><span data-stu-id="1395e-164">7: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="1395e-165">在此範例中，我們將使用 MongoDB 作為資料存放區。</span><span class="sxs-lookup"><span data-stu-id="1395e-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="1395e-166">安裝 Mongoose (常用的外掛程式) 來管理模型和結構描述：</span><span class="sxs-lookup"><span data-stu-id="1395e-166">Install Mongoose, a widely used plug-in, to manage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="1395e-167">安裝 MongoDB 的資料庫驅動程式 (也稱為 MongoDB)：</span><span class="sxs-lookup"><span data-stu-id="1395e-167">Install the database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="1395e-168">8：安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="1395e-168">8: Install additional modules</span></span>
<span data-ttu-id="1395e-169">安裝其餘所需的模組。</span><span class="sxs-lookup"><span data-stu-id="1395e-169">Install the remaining required modules.</span></span>

1.  <span data-ttu-id="1395e-170">在命令提示字元中，將目錄切換至 **azuread**：</span><span class="sxs-lookup"><span data-stu-id="1395e-170">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="1395e-171">輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="1395e-171">Enter the following commands.</span></span> <span data-ttu-id="1395e-172">此命令會在您的 node_modules 目錄中安裝下列模組：</span><span class="sxs-lookup"><span data-stu-id="1395e-172">The commands install the following modules in your node_modules directory:</span></span>

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="1395e-173">9：為您的相依性建立 Server.js 檔案</span><span class="sxs-lookup"><span data-stu-id="1395e-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="1395e-174">您的 Web API 伺服器的大部分功能都在 Server.js 檔案中。</span><span class="sxs-lookup"><span data-stu-id="1395e-174">A Server.js file holds the majority of the functionality for your web API server.</span></span> <span data-ttu-id="1395e-175">將您的大部分程式碼新增至此檔案。</span><span class="sxs-lookup"><span data-stu-id="1395e-175">Add most of your code to this file.</span></span> <span data-ttu-id="1395e-176">基於生產目的，您可以將功能分解成較小的檔案，例如用於個別的路由和控制器。</span><span class="sxs-lookup"><span data-stu-id="1395e-176">For production purposes, you can refactor the functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="1395e-177">在本文中，我們會針對此目的使用 Server.js。</span><span class="sxs-lookup"><span data-stu-id="1395e-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="1395e-178">在命令提示字元中，將目錄切換至 **azuread**：</span><span class="sxs-lookup"><span data-stu-id="1395e-178">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="1395e-179">使用您選擇的編輯器，建立 Server.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="1395e-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="1395e-180">將下列資訊新增至此檔案：</span><span class="sxs-lookup"><span data-stu-id="1395e-180">Add the following information to the file:</span></span>

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  <span data-ttu-id="1395e-181">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="1395e-181">Save the file.</span></span> <span data-ttu-id="1395e-182">我們很快會用到此檔案。</span><span class="sxs-lookup"><span data-stu-id="1395e-182">You will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="1395e-183">10：建立可儲存 Azure AD 設定的設定檔</span><span class="sxs-lookup"><span data-stu-id="1395e-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="1395e-184">這個程式碼檔會將設定參數從您的 Azure AD 入口網站傳遞到 Passport.js。</span><span class="sxs-lookup"><span data-stu-id="1395e-184">This code file passes the configuration parameters from your Azure AD portal to Passport.js.</span></span> <span data-ttu-id="1395e-185">在本文開頭，您已在將 Web API 新增至入口網站時建立這些設定值。</span><span class="sxs-lookup"><span data-stu-id="1395e-185">You created these configuration values when you added the web API to the portal at the beginning of the article.</span></span> <span data-ttu-id="1395e-186">在您複製程式碼之後，我們將會說明這些參數應該指定的值。</span><span class="sxs-lookup"><span data-stu-id="1395e-186">After you copy the code, we'll explain what to put in the values of these parameters.</span></span>

1.  <span data-ttu-id="1395e-187">在命令提示字元中，將目錄切換至 **azuread**：</span><span class="sxs-lookup"><span data-stu-id="1395e-187">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="1395e-188">在編輯器中，建立 Config.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="1395e-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="1395e-189">加入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1395e-189">Add the following information:</span></span>

    ```Javascript
    // Don't commit this file to your public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need to change this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="1395e-190">必要值</span><span class="sxs-lookup"><span data-stu-id="1395e-190">Required values</span></span>

*   <span data-ttu-id="1395e-191">**IdentityMetadata**：`passport-azure-ad` 會在此處尋找適用於識別提供者 (IDP) 的設定資料，以及用來驗證 JSON Web 權杖 (JWT) 的金鑰。</span><span class="sxs-lookup"><span data-stu-id="1395e-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for the identity provider (IDP) and the keys to validate the JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="1395e-192">如果您使用 Azure AD，則可能不需要變更此值。</span><span class="sxs-lookup"><span data-stu-id="1395e-192">If you are using Azure AD, you probably don't want to change this.</span></span>

*   <span data-ttu-id="1395e-193">**audience**：來自入口網站的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="1395e-193">**audience**: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="1395e-194">請經常變換金鑰。</span><span class="sxs-lookup"><span data-stu-id="1395e-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="1395e-195">請確定您一律從 "openid_keys" URL 中提取，而且應用程式可以存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="1395e-195">Be sure that you always pull from the "openid_keys" URL, and that the app can access the Internet.</span></span>
> 
> 

## <a name="11-add-the-configuration-to-your-serverjs-file"></a><span data-ttu-id="1395e-196">11：將設定新增至 Server.js 檔案</span><span class="sxs-lookup"><span data-stu-id="1395e-196">11: Add the configuration to your Server.js file</span></span>
<span data-ttu-id="1395e-197">您的應用程式需要從您剛才建立的組態檔中讀取這些值。</span><span class="sxs-lookup"><span data-stu-id="1395e-197">Your application needs to read the values from the config file you just created.</span></span> <span data-ttu-id="1395e-198">在應用程式中將 .config 檔案新增為必要資源。</span><span class="sxs-lookup"><span data-stu-id="1395e-198">Add the .config file as a required resource in your application.</span></span> <span data-ttu-id="1395e-199">將全域變數設定成 Config.js 中的變數。</span><span class="sxs-lookup"><span data-stu-id="1395e-199">Set the global variables to those that are in Config.js.</span></span>

1.  <span data-ttu-id="1395e-200">在命令提示字元中，將目錄切換至 **azuread**：</span><span class="sxs-lookup"><span data-stu-id="1395e-200">At the command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="1395e-201">在編輯器中開啟 Server.js。</span><span class="sxs-lookup"><span data-stu-id="1395e-201">In an editor, open Server.js.</span></span> <span data-ttu-id="1395e-202">加入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1395e-202">Add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="1395e-203">將新的區段新增至 Server.js：</span><span class="sxs-lookup"><span data-stu-id="1395e-203">Add a new section to Server.js:</span></span>

    ```Javascript
    // Pass these options in to the ODICBearerStrategy.
    var options = {
    // The URL of the metadata document for your app. Put the keys for token validation from the URL found in the jwks_uri tag in the metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array to hold signed-in users and the current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="1395e-204">12：使用 Moongoose 新增 MongoDB 模型和結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="1395e-204">12: Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="1395e-205">接著，在 REST API 服務中連接這三個檔案。</span><span class="sxs-lookup"><span data-stu-id="1395e-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="1395e-206">在本文中，我們會使用 MongoDB 來儲存工作。</span><span class="sxs-lookup"><span data-stu-id="1395e-206">In this article, we use MongoDB to store our tasks.</span></span> <span data-ttu-id="1395e-207">我們在「步驟 4」中討論到這一點。</span><span class="sxs-lookup"><span data-stu-id="1395e-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="1395e-208">在您於步驟 11 建立的 Config.js 檔案中，您的資料庫稱為 *tasklist*。</span><span class="sxs-lookup"><span data-stu-id="1395e-208">In the Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="1395e-209">這是您在 mongoose_auth_local 連線 URL 結尾指定的資訊。</span><span class="sxs-lookup"><span data-stu-id="1395e-209">That was what you put at the end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="1395e-210">您不需要在 MongoDB 中事先建立此資料庫。</span><span class="sxs-lookup"><span data-stu-id="1395e-210">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="1395e-211">第一次執行您的伺服器應用程式時會建立資料庫 (假設資料庫尚未存在)。</span><span class="sxs-lookup"><span data-stu-id="1395e-211">The database is created on the first run of your server application (assuming the database does not already exist).</span></span>

<span data-ttu-id="1395e-212">您已經告訴伺服器要使用哪個 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1395e-212">You've told the server what MongoDB database to use.</span></span> <span data-ttu-id="1395e-213">接下來，您需要撰寫一些額外的程式碼，為您的伺服器工作建立模型和結構描述。</span><span class="sxs-lookup"><span data-stu-id="1395e-213">Next, you need to write some additional code to create the model and schema for your server's tasks.</span></span>

### <a name="the-model"></a><span data-ttu-id="1395e-214">模型</span><span class="sxs-lookup"><span data-stu-id="1395e-214">The model</span></span>
<span data-ttu-id="1395e-215">結構描述模型非常基本。</span><span class="sxs-lookup"><span data-stu-id="1395e-215">The schema model is very basic.</span></span> <span data-ttu-id="1395e-216">需要的話，您可以展開它。</span><span class="sxs-lookup"><span data-stu-id="1395e-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="1395e-217">結構描述模型有下列值︰</span><span class="sxs-lookup"><span data-stu-id="1395e-217">The schema model has these values:</span></span>

*   <span data-ttu-id="1395e-218">**NAME**。</span><span class="sxs-lookup"><span data-stu-id="1395e-218">**NAME**.</span></span> <span data-ttu-id="1395e-219">指派至工作的人員。</span><span class="sxs-lookup"><span data-stu-id="1395e-219">The person assigned to the task.</span></span> <span data-ttu-id="1395e-220">這是**字串**值。</span><span class="sxs-lookup"><span data-stu-id="1395e-220">This is a **string** value.</span></span>
*   <span data-ttu-id="1395e-221">**TASK**。</span><span class="sxs-lookup"><span data-stu-id="1395e-221">**TASK**.</span></span> <span data-ttu-id="1395e-222">工作的名稱。</span><span class="sxs-lookup"><span data-stu-id="1395e-222">The name of the task.</span></span> <span data-ttu-id="1395e-223">這是**字串**值。</span><span class="sxs-lookup"><span data-stu-id="1395e-223">This is a **string** value.</span></span>
*   <span data-ttu-id="1395e-224">**DATE**。</span><span class="sxs-lookup"><span data-stu-id="1395e-224">**DATE**.</span></span> <span data-ttu-id="1395e-225">工作到期的日期。</span><span class="sxs-lookup"><span data-stu-id="1395e-225">The date that the task is due.</span></span> <span data-ttu-id="1395e-226">這是**日期時間**值。</span><span class="sxs-lookup"><span data-stu-id="1395e-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="1395e-227">**COMPLETED**。</span><span class="sxs-lookup"><span data-stu-id="1395e-227">**COMPLETED**.</span></span> <span data-ttu-id="1395e-228">是否已完成工作。</span><span class="sxs-lookup"><span data-stu-id="1395e-228">Whether the task is completed.</span></span> <span data-ttu-id="1395e-229">這是**布林**值。</span><span class="sxs-lookup"><span data-stu-id="1395e-229">This is a **Boolean** value.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="1395e-230">在程式碼中建立結構描述</span><span class="sxs-lookup"><span data-stu-id="1395e-230">Create the schema in the code</span></span>
1.  <span data-ttu-id="1395e-231">在命令提示字元中，將目錄切換至 **azuread**：</span><span class="sxs-lookup"><span data-stu-id="1395e-231">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="1395e-232">在編輯器中開啟 Server.js。</span><span class="sxs-lookup"><span data-stu-id="1395e-232">In your editor, open Server.js.</span></span> <span data-ttu-id="1395e-233">在設定項目下方，新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1395e-233">Below the configuration entry, add the following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="1395e-234">此程式碼會連線至 MongoDB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1395e-234">This code connects to the MongoDB server.</span></span> <span data-ttu-id="1395e-235">它也會傳回結構描述物件。</span><span class="sxs-lookup"><span data-stu-id="1395e-235">It also returns a schema object.</span></span>

#### <a name="using-the-schema-create-your-model-in-the-code"></a><span data-ttu-id="1395e-236">在程式碼中使用這個結構描述建立模型</span><span class="sxs-lookup"><span data-stu-id="1395e-236">Using the schema, create your model in the code</span></span>
<span data-ttu-id="1395e-237">在上述程式碼下方，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="1395e-237">Below the preceding code, add the following code:</span></span>

```Javascript
// Create a basic schema to store your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="1395e-238">您可以從程式碼看出，您需要先建立結構描述。</span><span class="sxs-lookup"><span data-stu-id="1395e-238">As you can tell from the code, first you create your schema.</span></span> <span data-ttu-id="1395e-239">接下來，您可以建立模型物件。</span><span class="sxs-lookup"><span data-stu-id="1395e-239">Next, you create a model object.</span></span> <span data-ttu-id="1395e-240">當您定義**路由**時，您可以使用模型物件來儲存整個程式碼的資料。</span><span class="sxs-lookup"><span data-stu-id="1395e-240">You use the model object to store your data throughout the code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="1395e-241">13：新增工作 REST API 伺服器的路由</span><span class="sxs-lookup"><span data-stu-id="1395e-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="1395e-242">既然您已經有可以使用的資料庫模型，請新增要用於 REST API 伺服器的路由。</span><span class="sxs-lookup"><span data-stu-id="1395e-242">Now that you have a database model to work with, add the routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="1395e-243">關於 restify 中的路由</span><span class="sxs-lookup"><span data-stu-id="1395e-243">About routes in restify</span></span>
<span data-ttu-id="1395e-244">Restify 中的路由與您使用 Express 堆疊時，運作方式完全相同。</span><span class="sxs-lookup"><span data-stu-id="1395e-244">Routes in restify work exactly the same way they do when you use the Express stack.</span></span> <span data-ttu-id="1395e-245">您可以使用您預期用戶端應用程式呼叫的 URI 來定義路由。</span><span class="sxs-lookup"><span data-stu-id="1395e-245">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="1395e-246">通常，您會在個別的檔案中定義您的路由。</span><span class="sxs-lookup"><span data-stu-id="1395e-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="1395e-247">在本教學課程中，我們會將路由放在 Server.js 中。</span><span class="sxs-lookup"><span data-stu-id="1395e-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="1395e-248">在生產用途上，建議您將這些路由納入您自己的檔案中。</span><span class="sxs-lookup"><span data-stu-id="1395e-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="1395e-249">Restify 路由的典型模式是：</span><span class="sxs-lookup"><span data-stu-id="1395e-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep the server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="1395e-250">這是最基本層級的模式。</span><span class="sxs-lookup"><span data-stu-id="1395e-250">This is the pattern at the most basic level.</span></span> <span data-ttu-id="1395e-251">Resitfy (及 Express) 提供更深入的功能，例如能夠定義應用程式類型，以及不同端點之間的複雜路由。</span><span class="sxs-lookup"><span data-stu-id="1395e-251">Restify (and Express) provide much deeper functionality, like the ability to define application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="1395e-252">將預設路由加入伺服器</span><span class="sxs-lookup"><span data-stu-id="1395e-252">Add default routes to your server</span></span>
<span data-ttu-id="1395e-253">新增基本 CRUD 路由：**建立**、**擷取**、**更新**和**刪除**。</span><span class="sxs-lookup"><span data-stu-id="1395e-253">Add the basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="1395e-254">在命令提示字元中，將目錄切換至 **azuread**：</span><span class="sxs-lookup"><span data-stu-id="1395e-254">At a command prompt, change the directory to **azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="1395e-255">在編輯器中開啟 Server.js。</span><span class="sxs-lookup"><span data-stu-id="1395e-255">In an editor, open Server.js.</span></span> <span data-ttu-id="1395e-256">在您稍早輸入的資料庫項目底下，新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="1395e-256">Below the database entries you made earlier, add the following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow you to use MongoDB Server as your response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it to MongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();
    _task.save(function(err) {
    if (err) {
    req.log.warn(err, 'createTask: unable to save');
    next(err);
    } else {
    res.send(201, _task);
    }
    });
    return next();
    }
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable to delete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable to read %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns the list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you to set default headers.
    // These headers comply with CORS, and allow us to use MongoDB Server as our response to any origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    log.info("listTasks was called for: ", owner);
    Task.find({
    owner: owner
    }).limit(20).sort('date').exec(function(err, data) {
    if (err)
    return next(err);
    if (data.length > 0) {
    log.info(data);
    }
    if (!data.length) {
    log.warn(err, "There are no tasks in the database. Add one!");
    }
    if (!owner) {
    log.warn(err, "You did not pass an owner when listing tasks.");
    } else {
    res.json(data);
    }
    });
    return next();
    }
    ```

### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="1395e-257">新增路由的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="1395e-257">Add error handling for the routes</span></span>
<span data-ttu-id="1395e-258">新增一些錯誤處理，以便向用戶端通知您遇到的問題。</span><span class="sxs-lookup"><span data-stu-id="1395e-258">Add some error handling so you can communicate back to the client about the problem you encountered.</span></span>

<span data-ttu-id="1395e-259">在您已撰寫的程式碼下方，新增下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="1395e-259">Add the following code below the code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back to the client.
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="14-create-your-server"></a><span data-ttu-id="1395e-260">14：建立伺服器</span><span class="sxs-lookup"><span data-stu-id="1395e-260">14: Create your server</span></span>
<span data-ttu-id="1395e-261">最後一件事是新增您的伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="1395e-261">The last thing to do is to add your server instance.</span></span> <span data-ttu-id="1395e-262">伺服器執行個體會管理您的呼叫。</span><span class="sxs-lookup"><span data-stu-id="1395e-262">The server instance manages your calls.</span></span>

<span data-ttu-id="1395e-263">Restify (及 Express) 有深入的自訂功能可搭配 REST API 伺服器使用。</span><span class="sxs-lookup"><span data-stu-id="1395e-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="1395e-264">在本教學課程中，我們會使用最基本的設定。</span><span class="sxs-lookup"><span data-stu-id="1395e-264">In this tutorial, we use the most basic setup.</span></span>

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst to 10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-the-routes-without-authentication-for-now"></a><span data-ttu-id="1395e-265">15：新增路由 (目前不含驗證)</span><span class="sxs-lookup"><span data-stu-id="1395e-265">15: Add the routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD to add the real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in the pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need to maintain session state. You can experiment with removing API protection.
/* To do this, remove the passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-the-server"></a><span data-ttu-id="1395e-266">16︰執行伺服器</span><span class="sxs-lookup"><span data-stu-id="1395e-266">16: Run the server</span></span>
<span data-ttu-id="1395e-267">您最好在新增驗證之前先測試伺服器。</span><span class="sxs-lookup"><span data-stu-id="1395e-267">It's a good idea to test your server before you add authentication.</span></span>

<span data-ttu-id="1395e-268">測試伺服器最簡單方式是在命令提示字元中使用 curl。</span><span class="sxs-lookup"><span data-stu-id="1395e-268">The easiest way to test your server is by using curl at a command prompt.</span></span> <span data-ttu-id="1395e-269">若要這樣做，您只需要利用簡單的公用程式將輸出剖析為 JSON。</span><span class="sxs-lookup"><span data-stu-id="1395e-269">To do this, you need a simple utility that you can use to parse output as JSON.</span></span> 

1.  <span data-ttu-id="1395e-270">安裝我們將在下列範例中使用的 JSON 工具︰</span><span class="sxs-lookup"><span data-stu-id="1395e-270">Install the JSON tool that we use in the following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="1395e-271">這會全域安裝 JSON 工具。</span><span class="sxs-lookup"><span data-stu-id="1395e-271">This installs the JSON tool globally.</span></span>

2.  <span data-ttu-id="1395e-272">請確定您的 MongoDB 執行個體正在執行：</span><span class="sxs-lookup"><span data-stu-id="1395e-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="1395e-273">將目錄切換至 **azuread**，然後執行 curl：</span><span class="sxs-lookup"><span data-stu-id="1395e-273">Change the directory to **azuread**, and then run curl:</span></span>

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  <span data-ttu-id="1395e-274">新增工作︰</span><span class="sxs-lookup"><span data-stu-id="1395e-274">To add a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="1395e-275">回應應為：</span><span class="sxs-lookup"><span data-stu-id="1395e-275">The response should be:</span></span>

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  <span data-ttu-id="1395e-276">Brandon 的工作清單︰</span><span class="sxs-lookup"><span data-stu-id="1395e-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="1395e-277">如果所有這些命令都執行無誤，您就可以將 OAuth 新增至 REST API 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1395e-277">If all these commands run without errors, you are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="1395e-278">「您現在已具有 REST API 伺服器和 MongoDB！」</span><span class="sxs-lookup"><span data-stu-id="1395e-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-to-your-rest-api-server"></a><span data-ttu-id="1395e-279">17：將驗證新增至 REST API 伺服器</span><span class="sxs-lookup"><span data-stu-id="1395e-279">17: Add authentication to your REST API server</span></span>
<span data-ttu-id="1395e-280">現在您有一個執行中的 REST API，請設定它來搭配 Azure AD 使用。</span><span class="sxs-lookup"><span data-stu-id="1395e-280">Now that you have a running REST API, set it up to use it with Azure AD.</span></span>

<span data-ttu-id="1395e-281">在命令提示字元中，將目錄切換至 **azuread**：</span><span class="sxs-lookup"><span data-stu-id="1395e-281">At a command prompt, change the directory to **azuread**:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="1395e-282">使用 passport-azure-ad 隨附的 oidcbearerstrategy</span><span class="sxs-lookup"><span data-stu-id="1395e-282">Use the oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="1395e-283">到目前為止，您已經建置典型的 REST TODO 伺服器，且其中不含任何授權種類。</span><span class="sxs-lookup"><span data-stu-id="1395e-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="1395e-284">現在，新增驗證。</span><span class="sxs-lookup"><span data-stu-id="1395e-284">Now, add authentication.</span></span>

<span data-ttu-id="1395e-285">首先，指明您要使用 Passport。</span><span class="sxs-lookup"><span data-stu-id="1395e-285">First,  indicate that you want to use Passport.</span></span> <span data-ttu-id="1395e-286">將這段程式碼放在緊鄰您先前的伺服器設定後面：</span><span class="sxs-lookup"><span data-stu-id="1395e-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="1395e-287">撰寫 API 時，最好一律將資料連結到使用者無法證明其在權杖中是唯一的項目。</span><span class="sxs-lookup"><span data-stu-id="1395e-287">When you write APIs, it's a good idea to always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="1395e-288">當此伺服器儲存 TODO 項目時，它會根據權杖 (透過 token.sub 呼叫) 中的使用者訂用帳戶識別碼來儲存它們。</span><span class="sxs-lookup"><span data-stu-id="1395e-288">When this server stores TODO items, it stores them based on the user subscription ID in the token (called through token.sub).</span></span> <span data-ttu-id="1395e-289">您需要將 token.sub 放在 “owner” 欄位中。</span><span class="sxs-lookup"><span data-stu-id="1395e-289">You put the token.sub in the “owner” field.</span></span> <span data-ttu-id="1395e-290">這可確保只有該使用者可以存取使用者的 TODO。</span><span class="sxs-lookup"><span data-stu-id="1395e-290">This ensures that only that user can access the user's TODOs.</span></span> <span data-ttu-id="1395e-291">沒有其他人可以存取先前輸入的 TODO。</span><span class="sxs-lookup"><span data-stu-id="1395e-291">No one else can access the TODOs that were entered.</span></span> <span data-ttu-id="1395e-292">“owner” 完全不會公開在 API 中。</span><span class="sxs-lookup"><span data-stu-id="1395e-292">There is no exposure in the API for “owner.”</span></span> <span data-ttu-id="1395e-293">外部使用者可以要求其他使用者的 TODO (即使通過驗證)。</span><span class="sxs-lookup"><span data-stu-id="1395e-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="1395e-294">接下來，我們將使用隨附於 `passport-azure-ad` 的 Open ID Connect Bearer 策略。</span><span class="sxs-lookup"><span data-stu-id="1395e-294">Next, use the Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="1395e-295">將這段程式碼放在您稍早貼上的程式碼後面：</span><span class="sxs-lookup"><span data-stu-id="1395e-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users.
/*
/* Because of the Passport pattern, you need to manage users and info tokens
/* with a FindorCreate() method. The method must be provided by the implementor.
/* In the following code, you autoregister any user and implement a FindById().
/* It's a good idea to do something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying the user');
log.info(token, 'was the token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="1395e-296">Passport 會針對其所有策略 (Twitter、Facebook 等) 使用類似的模式。</span><span class="sxs-lookup"><span data-stu-id="1395e-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="1395e-297">所有策略寫入器均遵守此模式。</span><span class="sxs-lookup"><span data-stu-id="1395e-297">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="1395e-298">將使用權杖和 `done` 作為參數的 `function()` 傳遞給策略。</span><span class="sxs-lookup"><span data-stu-id="1395e-298">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="1395e-299">策略會在完成所有工作之後傳回。</span><span class="sxs-lookup"><span data-stu-id="1395e-299">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="1395e-300">請儲存使用者並隱藏權杖，這樣一來，您就不必再次要求它。</span><span class="sxs-lookup"><span data-stu-id="1395e-300">Store the user and stash the token so you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1395e-301">上述程式碼會將可通過驗證的所有使用者帶往您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1395e-301">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="1395e-302">這就是所謂的自動註冊。</span><span class="sxs-lookup"><span data-stu-id="1395e-302">This is known as auto-registration.</span></span> <span data-ttu-id="1395e-303">在生產伺服器中，您應該會想要讓所有人都必須先完成您選擇的註冊過程，才能進入您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1395e-303">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="1395e-304">這是您通常會在消費者應用程式中看到的模式。</span><span class="sxs-lookup"><span data-stu-id="1395e-304">This is usually the pattern you see in consumer apps.</span></span> <span data-ttu-id="1395e-305">應用程式可能會允許您使用 Facebook 進行註冊，但之後會要求您輸入其他資訊。</span><span class="sxs-lookup"><span data-stu-id="1395e-305">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="1395e-306">如果您沒有針對本教學課程使用命令列程式，可以從傳回的權杖物件中擷取電子郵件。</span><span class="sxs-lookup"><span data-stu-id="1395e-306">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="1395e-307">然後，您可能會要求使用者輸入其他資訊。</span><span class="sxs-lookup"><span data-stu-id="1395e-307">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="1395e-308">由於這是測試伺服器，您會將使用者直接加入記憶體中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1395e-308">Because this is a test server, you add the user directly to the in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="1395e-309">保護端點</span><span class="sxs-lookup"><span data-stu-id="1395e-309">Protect endpoints</span></span>
<span data-ttu-id="1395e-310">您可以透過想要使用的通訊協定指定 **passport.authenticate()** 呼叫，以保護端點。</span><span class="sxs-lookup"><span data-stu-id="1395e-310">Protect endpoints by specifying the **passport.authenticate()** call with the protocol that you want to use.</span></span>

<span data-ttu-id="1395e-311">您可以在伺服器程式碼中編輯路由，以利用更進階的選項︰</span><span class="sxs-lookup"><span data-stu-id="1395e-311">You can edit your route in your server code for a more advanced option:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="1395e-312">18︰再次執行伺服器應用程式</span><span class="sxs-lookup"><span data-stu-id="1395e-312">18: Run your server application again</span></span>
<span data-ttu-id="1395e-313">再次使用 curl，檢查您是否以 OAuth 2.0 保護您的端點。</span><span class="sxs-lookup"><span data-stu-id="1395e-313">Use curl again to see if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="1395e-314">請在您針對這個端點執行任何用戶端 SDK 之前這樣做。</span><span class="sxs-lookup"><span data-stu-id="1395e-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="1395e-315">傳回的標頭應該會讓您知道驗證是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="1395e-315">The headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="1395e-316">請確定您的 MongoDB 執行個體正在執行：</span><span class="sxs-lookup"><span data-stu-id="1395e-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="1395e-317">切換至 **azuread** 目錄，然後使用 curl：</span><span class="sxs-lookup"><span data-stu-id="1395e-317">Change to the **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="1395e-318">嘗試基本的 POST 方法：</span><span class="sxs-lookup"><span data-stu-id="1395e-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="1395e-319">401 回應會指出 Passport 層正嘗試重新導向至已授權的端點，這正是您想要的結果。</span><span class="sxs-lookup"><span data-stu-id="1395e-319">A 401 response indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="1395e-320">「您現在擁有一項使用 OAuth 2.0 的 REST API 服務！」</span><span class="sxs-lookup"><span data-stu-id="1395e-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="1395e-321">在未使用 OAuth 2.0 相容用戶端的情況下，您已經儘可能地使用此伺服器的所有功能。</span><span class="sxs-lookup"><span data-stu-id="1395e-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="1395e-322">在這方面，您必須檢閱其他教學課程。</span><span class="sxs-lookup"><span data-stu-id="1395e-322">For that, you will need to review an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1395e-323">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1395e-323">Next steps</span></span>
<span data-ttu-id="1395e-324">做為參考，我們以 [.zip 檔案](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip)的形式提供已完成的範例 (不含您的設定值)。</span><span class="sxs-lookup"><span data-stu-id="1395e-324">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="1395e-325">您也可以從 Github 複製它：</span><span class="sxs-lookup"><span data-stu-id="1395e-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="1395e-326">現在，您可以進入更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="1395e-326">Now, you can move on to more advanced topics.</span></span> <span data-ttu-id="1395e-327">您可以嘗試[使用 v2.0 端點保護 Node.js Web 應用程式](active-directory-v2-devquickstarts-node-web.md)。</span><span class="sxs-lookup"><span data-stu-id="1395e-327">You might want to try [Secure a Node.js web app using the v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="1395e-328">以下是一些其他資源：</span><span class="sxs-lookup"><span data-stu-id="1395e-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="1395e-329">Azure AD v2.0 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="1395e-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="1395e-330">Stack Overflow "azure-active-directory" 標籤 (英文)</span><span class="sxs-lookup"><span data-stu-id="1395e-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="1395e-331">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="1395e-331">Get security updates for our products</span></span>
<span data-ttu-id="1395e-332">我們建議您註冊，即可在發生安全性事件時收到通知。</span><span class="sxs-lookup"><span data-stu-id="1395e-332">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="1395e-333">請在 [Microsoft 技術安全性通知](https://technet.microsoft.com/security/dd252948)頁面上，訂閱資訊安全摘要報告警示。</span><span class="sxs-lookup"><span data-stu-id="1395e-333">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

