---
title: "使用 Node.js 的 Azure Active Directory v2.0 web API aaaSecure |Microsoft 文件"
description: "了解如何 toobuild Node.js web API 可接受同時從個人 Microsoft 帳戶和工作或學校帳戶的語彙基元。"
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
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="70a3d-103">使用 Node.js 保護 Web API 安全</span><span class="sxs-lookup"><span data-stu-id="70a3d-103">Secure a web API by using Node.js</span></span>
> [!NOTE]
> <span data-ttu-id="70a3d-104">並非所有的 Azure Active Directory 案例和功能搭配 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="70a3d-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="70a3d-105">toodetermine 是否應該使用 hello v2.0 端點或 hello v1.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="70a3d-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="70a3d-106">當您使用 hello Azure Active Directory (Azure AD) v2.0 的端點時，您可以使用[OAuth 2.0](active-directory-v2-protocols.md)存取權杖 tooprotect 您的 web API。</span><span class="sxs-lookup"><span data-stu-id="70a3d-106">When you use hello Azure Active Directory (Azure AD) v2.0 endpoint, you can use [OAuth 2.0](active-directory-v2-protocols.md) access tokens tooprotect your web API.</span></span> <span data-ttu-id="70a3d-107">如果使用者同時有個人 Microsoft 帳戶及公司或學校帳戶，只要透過 OAuth 2.0 存取權杖，就能安全地存取您的 Web API。</span><span class="sxs-lookup"><span data-stu-id="70a3d-107">With OAuth 2.0 access tokens, users who have both a personal Microsoft account and work or school accounts can securely access your web API.</span></span>

<span data-ttu-id="70a3d-108">*Passport* 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="70a3d-108">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="70a3d-109">您可以暗中將極具彈性且模組化的 Passport 放入任何 Express 架構或 resitify Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-109">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="70a3d-110">在 Passport 中，一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他選項進行驗證。</span><span class="sxs-lookup"><span data-stu-id="70a3d-110">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="70a3d-111">我們已為 Azure AD 開發一個策略。</span><span class="sxs-lookup"><span data-stu-id="70a3d-111">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="70a3d-112">在本文中，我們會示範如何 tooinstall hello 模組，並再新增 hello Azure AD`passport-azure-ad`外掛程式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-112">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="70a3d-113">下載</span><span class="sxs-lookup"><span data-stu-id="70a3d-113">Download</span></span>
<span data-ttu-id="70a3d-114">此教學課程中的 hello 程式碼會維護[GitHub 上](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs)。</span><span class="sxs-lookup"><span data-stu-id="70a3d-114">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span> <span data-ttu-id="70a3d-115">toofollow hello 教學課程中，您可以[下載為.zip 檔案的 hello 應用程式的基本架構](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip)，或再製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="70a3d-115">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="70a3d-116">您也可以取得 hello 完成應用程式在此教學課程中的 hello 結尾處。</span><span class="sxs-lookup"><span data-stu-id="70a3d-116">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="70a3d-117">1：註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="70a3d-117">1: Register an app</span></span>
<span data-ttu-id="70a3d-118">建立新的應用程式在[apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，或遵循[這些詳細步驟](active-directory-v2-app-registration.md)tooregister 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-118">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="70a3d-119">請確定您已執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="70a3d-119">Make sure you:</span></span>

* <span data-ttu-id="70a3d-120">複製 hello**應用程式識別碼**指派 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-120">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="70a3d-121">您在本教學課程中將需要用到它。</span><span class="sxs-lookup"><span data-stu-id="70a3d-121">You'll need it for this tutorial.</span></span>
* <span data-ttu-id="70a3d-122">新增 hello**行動**平台應用程式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="70a3d-123">複製 hello**重新導向 URI**從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="70a3d-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="70a3d-124">您必須使用 hello 預設 URI 值`urn:ietf:wg:oauth:2.0:oob`。</span><span class="sxs-lookup"><span data-stu-id="70a3d-124">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-install-nodejs"></a><span data-ttu-id="70a3d-125">2：安裝 Node.js</span><span class="sxs-lookup"><span data-stu-id="70a3d-125">2: Install Node.js</span></span>
<span data-ttu-id="70a3d-126">您必須在此教學課程 toouse hello 範例，[安裝 Node.js](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="70a3d-126">toouse hello sample for this tutorial, you must [install Node.js](http://nodejs.org).</span></span>

## <a name="3-install-mongodb"></a><span data-ttu-id="70a3d-127">3︰安裝 MongoDB</span><span class="sxs-lookup"><span data-stu-id="70a3d-127">3: Install MongoDB</span></span>
<span data-ttu-id="70a3d-128">toosuccessfully 使用這個範例中，您必須[安裝 MongoDB](http://www.mongodb.org)。</span><span class="sxs-lookup"><span data-stu-id="70a3d-128">toosuccessfully use this sample, you must [install MongoDB](http://www.mongodb.org).</span></span> <span data-ttu-id="70a3d-129">在此範例中，您使用 MongoDB toomake 您持續性的 REST API 在伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="70a3d-129">In this sample, you use MongoDB toomake your REST API persistent across server instances.</span></span>

> [!NOTE]
> <span data-ttu-id="70a3d-130">在本文中，我們假設您使用 MongoDB hello 預設安裝和伺服器端點： mongodb://localhost。</span><span class="sxs-lookup"><span data-stu-id="70a3d-130">In this article, we assume that you use hello default installation and server endpoints for MongoDB: mongodb://localhost.</span></span>
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="70a3d-131">4： 安裝 hello restify 模組在您的 web 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="70a3d-131">4: Install hello restify modules in your web API</span></span>
<span data-ttu-id="70a3d-132">我們使用 Resitfy toobuild REST API。</span><span class="sxs-lookup"><span data-stu-id="70a3d-132">We use Resitfy toobuild our REST API.</span></span> <span data-ttu-id="70a3d-133">Restify 是衍生自 Express 的最小且具彈性的 Node.js 應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="70a3d-133">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="70a3d-134">Restify 具有一組強固的功能，您可以使用 toobuild 連接之上的 REST Api。</span><span class="sxs-lookup"><span data-stu-id="70a3d-134">Restify has a robust set of features that you can use toobuild REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="70a3d-135">安裝 restify</span><span class="sxs-lookup"><span data-stu-id="70a3d-135">Install restify</span></span>
1.  <span data-ttu-id="70a3d-136">在命令提示字元中，變更 hello 目錄太**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="70a3d-136">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

    <span data-ttu-id="70a3d-137">如果 hello **azure ad**目錄不存在，建立它：</span><span class="sxs-lookup"><span data-stu-id="70a3d-137">If hello **azuread** directory does not exist, create it:</span></span>

    `mkdir azuread`

2.  <span data-ttu-id="70a3d-138">安裝 restify：</span><span class="sxs-lookup"><span data-stu-id="70a3d-138">Install restify:</span></span>

    `npm install restify`

    <span data-ttu-id="70a3d-139">hello 這個命令的輸出應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="70a3d-139">hello output of this command should look like this:</span></span>

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

#### <a name="did-you-get-an-error"></a><span data-ttu-id="70a3d-140">您有收到錯誤訊息嗎？</span><span class="sxs-lookup"><span data-stu-id="70a3d-140">Did you get an error?</span></span>
<span data-ttu-id="70a3d-141">某些在作業系統上，當您使用 hello`npm`命令時，您可能會看到此訊息： `Error: EPERM, chmod '/usr/local/bin/..'`。</span><span class="sxs-lookup"><span data-stu-id="70a3d-141">On some operating systems, when you use hello `npm` command, you might see this message: `Error: EPERM, chmod '/usr/local/bin/..'`.</span></span> <span data-ttu-id="70a3d-142">hello 錯誤後再次嘗試執行 hello 帳戶系統管理員身分的要求。</span><span class="sxs-lookup"><span data-stu-id="70a3d-142">hello error is followed by a request that you try running hello account as an administrator.</span></span> <span data-ttu-id="70a3d-143">如果發生這種情況，使用 hello 命令`sudo`toorun`npm`較高的權限層級。</span><span class="sxs-lookup"><span data-stu-id="70a3d-143">If this occurs, use hello command `sudo` toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-related-toodtrace"></a><span data-ttu-id="70a3d-144">您是否已取得相關的錯誤 tooDTrace？</span><span class="sxs-lookup"><span data-stu-id="70a3d-144">Did you get an error related tooDTrace?</span></span>
<span data-ttu-id="70a3d-145">當您安裝 restify 時，您可能會看到此訊息︰</span><span class="sxs-lookup"><span data-stu-id="70a3d-145">When you install restify, you might see this message:</span></span>

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

<span data-ttu-id="70a3d-146">Restify 具有強大的機制，tootrace 使用 DTrace REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="70a3d-146">Restify has a powerful mechanism tootrace REST calls by using DTrace.</span></span> <span data-ttu-id="70a3d-147">不過，在許多作業系統上無法使用 DTrace。</span><span class="sxs-lookup"><span data-stu-id="70a3d-147">However, DTrace is not available on many operating systems.</span></span> <span data-ttu-id="70a3d-148">您可以放心地忽略此錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="70a3d-148">You can safely ignore this error message.</span></span>


## <a name="5-install-passportjs-in-your-web-api"></a><span data-ttu-id="70a3d-149">5：在您的 Web API 中安裝 Passport.js</span><span class="sxs-lookup"><span data-stu-id="70a3d-149">5: Install Passport.js in your web API</span></span>
1.  <span data-ttu-id="70a3d-150">Hello 命令提示字元，變更 hello 目錄太**azure ad**。</span><span class="sxs-lookup"><span data-stu-id="70a3d-150">At hello command prompt, change hello directory too**azuread**.</span></span>

2.  <span data-ttu-id="70a3d-151">安裝 Passport.js：</span><span class="sxs-lookup"><span data-stu-id="70a3d-151">Install Passport.js:</span></span>

    `npm install passport`

    <span data-ttu-id="70a3d-152">hello hello 命令輸出應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="70a3d-152">hello output of hello command should look like this:</span></span>

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a><span data-ttu-id="70a3d-153">6： 加入 passport azure ad tooyour web API</span><span class="sxs-lookup"><span data-stu-id="70a3d-153">6: Add passport-azure-ad tooyour web API</span></span>
<span data-ttu-id="70a3d-154">接下來，加入 hello OAuth 策略中，使用 passport azure ad。</span><span class="sxs-lookup"><span data-stu-id="70a3d-154">Next, add hello OAuth strategy, by using passport-azuread.</span></span> <span data-ttu-id="70a3d-155">`passport-azuread` 是一套將 Azure AD 連線至 Passport 的策略。</span><span class="sxs-lookup"><span data-stu-id="70a3d-155">`passport-azuread` is a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="70a3d-156">在這個 Rest API 範例中，我們會對持有人權杖使用此策略。</span><span class="sxs-lookup"><span data-stu-id="70a3d-156">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="70a3d-157">雖然 OAuth2.0 提供可發行任何已知權杖類型的架構，但只有某些權杖類型經常使用。</span><span class="sxs-lookup"><span data-stu-id="70a3d-157">Although OAuth 2.0 provides a framework in which any known token type can be issued, certain token types are commonly used.</span></span> <span data-ttu-id="70a3d-158">持有者權杖是常用的 tooprotect 的端點。</span><span class="sxs-lookup"><span data-stu-id="70a3d-158">Bearer tokens are commonly used tooprotect endpoints.</span></span> <span data-ttu-id="70a3d-159">持有者權杖會在 OAuth 2.0 權杖的 hello 最廣泛發出型別。</span><span class="sxs-lookup"><span data-stu-id="70a3d-159">Bearer tokens are hello most widely issued type of token in OAuth 2.0.</span></span> <span data-ttu-id="70a3d-160">許多的 OAuth 2.0 實作假設持有者權杖是 hello 的發行權杖的唯一類型。</span><span class="sxs-lookup"><span data-stu-id="70a3d-160">Many OAuth 2.0 implementations assume that bearer tokens are hello only type of token issued.</span></span>
> 
> 

1.  <span data-ttu-id="70a3d-161">在命令提示字元中，變更 hello 目錄太**azure ad**。</span><span class="sxs-lookup"><span data-stu-id="70a3d-161">At a command prompt, change hello directory too**azuread**.</span></span>

    `cd azuread`

2.  <span data-ttu-id="70a3d-162">安裝 hello Passport.js`passport-azure-ad`模組：</span><span class="sxs-lookup"><span data-stu-id="70a3d-162">Install hello Passport.js `passport-azure-ad` module:</span></span>

    `npm install passport-azure-ad`

    <span data-ttu-id="70a3d-163">hello hello 命令輸出應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="70a3d-163">hello output of hello command should look like this:</span></span>

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

## <a name="7-add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="70a3d-164">7： 加入 MongoDB 模組 tooyour web API</span><span class="sxs-lookup"><span data-stu-id="70a3d-164">7: Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="70a3d-165">在此範例中，我們將使用 MongoDB 作為資料存放區。</span><span class="sxs-lookup"><span data-stu-id="70a3d-165">In this sample, we use MongoDB as our data store.</span></span> 

1.  <span data-ttu-id="70a3d-166">安裝 1，廣泛使用外掛程式，toomanage 模型和結構描述：</span><span class="sxs-lookup"><span data-stu-id="70a3d-166">Install Mongoose, a widely used plug-in, toomanage models and schemas:</span></span> 

    `npm install mongoose`

2.  <span data-ttu-id="70a3d-167">安裝適用於 MongoDB，這也稱為 MongoDB hello 資料庫驅動程式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-167">Install hello database driver for MongoDB, which is also called MongoDB:</span></span>

    `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="70a3d-168">8：安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="70a3d-168">8: Install additional modules</span></span>
<span data-ttu-id="70a3d-169">安裝 hello 剩餘所需的模組。</span><span class="sxs-lookup"><span data-stu-id="70a3d-169">Install hello remaining required modules.</span></span>

1.  <span data-ttu-id="70a3d-170">在命令提示字元中，變更 hello 目錄太**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="70a3d-170">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="70a3d-171">輸入下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="70a3d-171">Enter hello following commands.</span></span> <span data-ttu-id="70a3d-172">hello 命令會安裝下列 node_modules 目錄中的模組的 hello:</span><span class="sxs-lookup"><span data-stu-id="70a3d-172">hello commands install hello following modules in your node_modules directory:</span></span>

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

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a><span data-ttu-id="70a3d-173">9：為您的相依性建立 Server.js 檔案</span><span class="sxs-lookup"><span data-stu-id="70a3d-173">9: Create a Server.js file for your dependencies</span></span>
<span data-ttu-id="70a3d-174">立即轉譯 Server.js 檔案保存 hello 大部分的 web API 伺服器的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="70a3d-174">A Server.js file holds hello majority of hello functionality for your web API server.</span></span> <span data-ttu-id="70a3d-175">將大部分的程式碼 toothis 檔案。</span><span class="sxs-lookup"><span data-stu-id="70a3d-175">Add most of your code toothis file.</span></span> <span data-ttu-id="70a3d-176">生產環境中使用，您可以像重構 hello 功能較小的檔案不同的路徑及控制站。</span><span class="sxs-lookup"><span data-stu-id="70a3d-176">For production purposes, you can refactor hello functionality into smaller files, like for separate routes and controllers.</span></span> <span data-ttu-id="70a3d-177">在本文中，我們會針對此目的使用 Server.js。</span><span class="sxs-lookup"><span data-stu-id="70a3d-177">In this article, we use Server.js for this purpose.</span></span>

1.  <span data-ttu-id="70a3d-178">在命令提示字元中，變更 hello 目錄太**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="70a3d-178">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="70a3d-179">使用您選擇的編輯器，建立 Server.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="70a3d-179">Using an editor of your choice, create a Server.js file.</span></span> <span data-ttu-id="70a3d-180">新增下列資訊 toohello 檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="70a3d-180">Add hello following information toohello file:</span></span>

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

3.  <span data-ttu-id="70a3d-181">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="70a3d-181">Save hello file.</span></span> <span data-ttu-id="70a3d-182">您很快就會傳回 tooit。</span><span class="sxs-lookup"><span data-stu-id="70a3d-182">You will return tooit shortly.</span></span>

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="70a3d-183">10： 建立您的 Azure AD 設定的組態檔 toostore</span><span class="sxs-lookup"><span data-stu-id="70a3d-183">10: Create a config file toostore your Azure AD settings</span></span>
<span data-ttu-id="70a3d-184">這個程式碼檔會從您的 Azure AD 入口網站 tooPassport.js 傳遞 hello 組態參數。</span><span class="sxs-lookup"><span data-stu-id="70a3d-184">This code file passes hello configuration parameters from your Azure AD portal tooPassport.js.</span></span> <span data-ttu-id="70a3d-185">當您在 hello 文章 hello 開頭加入 hello web API toohello 入口網站，您會建立這些組態值。</span><span class="sxs-lookup"><span data-stu-id="70a3d-185">You created these configuration values when you added hello web API toohello portal at hello beginning of hello article.</span></span> <span data-ttu-id="70a3d-186">複製 hello 程式碼之後，我們將說明哪些 tooput hello 這些參數值。</span><span class="sxs-lookup"><span data-stu-id="70a3d-186">After you copy hello code, we'll explain what tooput in hello values of these parameters.</span></span>

1.  <span data-ttu-id="70a3d-187">在命令提示字元中，變更 hello 目錄太**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="70a3d-187">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="70a3d-188">在編輯器中，建立 Config.js 檔案。</span><span class="sxs-lookup"><span data-stu-id="70a3d-188">In an editor, create a Config.js file.</span></span> <span data-ttu-id="70a3d-189">新增 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="70a3d-189">Add hello following information:</span></span>

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a><span data-ttu-id="70a3d-190">必要值</span><span class="sxs-lookup"><span data-stu-id="70a3d-190">Required values</span></span>

*   <span data-ttu-id="70a3d-191">**IdentityMetadata**： 這是 where `passport-azure-ad` hello 身分識別提供者 (IDP) 和 hello 金鑰 toovalidate hello JSON Web 權杖 (Jwt) 的組態資料的外觀。</span><span class="sxs-lookup"><span data-stu-id="70a3d-191">**IdentityMetadata**: This is where `passport-azure-ad` looks for your configuration data for hello identity provider (IDP) and hello keys toovalidate hello JSON Web Tokens (JWTs).</span></span> <span data-ttu-id="70a3d-192">如果您使用 Azure AD，您可能不想 toochange 這。</span><span class="sxs-lookup"><span data-stu-id="70a3d-192">If you are using Azure AD, you probably don't want toochange this.</span></span>

*   <span data-ttu-id="70a3d-193">**對象**: hello 入口網站從您重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="70a3d-193">**audience**: Your redirect URI from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="70a3d-194">請經常變換金鑰。</span><span class="sxs-lookup"><span data-stu-id="70a3d-194">Roll your keys at frequent intervals.</span></span> <span data-ttu-id="70a3d-195">請務必一律提取從 hello"openid_keys 」 的 URL，，和該 hello 應用程式可以存取網際網路 hello。</span><span class="sxs-lookup"><span data-stu-id="70a3d-195">Be sure that you always pull from hello "openid_keys" URL, and that hello app can access hello Internet.</span></span>
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a><span data-ttu-id="70a3d-196">11： 加入 hello 組態 tooyour 立即轉譯 Server.js 檔</span><span class="sxs-lookup"><span data-stu-id="70a3d-196">11: Add hello configuration tooyour Server.js file</span></span>
<span data-ttu-id="70a3d-197">您的應用程式必須從您剛才建立的 hello 組態檔 tooread hello 值。</span><span class="sxs-lookup"><span data-stu-id="70a3d-197">Your application needs tooread hello values from hello config file you just created.</span></span> <span data-ttu-id="70a3d-198">為您的應用程式中有項必要資源新增 hello.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="70a3d-198">Add hello .config file as a required resource in your application.</span></span> <span data-ttu-id="70a3d-199">設定 hello 全域變數 toothose Config.js 中。</span><span class="sxs-lookup"><span data-stu-id="70a3d-199">Set hello global variables toothose that are in Config.js.</span></span>

1.  <span data-ttu-id="70a3d-200">Hello 命令提示字元，變更 hello 目錄太**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="70a3d-200">At hello command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="70a3d-201">在編輯器中開啟 Server.js。</span><span class="sxs-lookup"><span data-stu-id="70a3d-201">In an editor, open Server.js.</span></span> <span data-ttu-id="70a3d-202">新增 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="70a3d-202">Add hello following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```

3.  <span data-ttu-id="70a3d-203">加入新的區段 tooServer.js:</span><span class="sxs-lookup"><span data-stu-id="70a3d-203">Add a new section tooServer.js:</span></span>

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="70a3d-204">12: hello MongoDB 模型和結構描述資訊加入使用 1</span><span class="sxs-lookup"><span data-stu-id="70a3d-204">12: Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="70a3d-205">接著，在 REST API 服務中連接這三個檔案。</span><span class="sxs-lookup"><span data-stu-id="70a3d-205">Next, connect these three files in a REST API service.</span></span>

<span data-ttu-id="70a3d-206">在本文中，我們使用 MongoDB toostore 我們的工作。</span><span class="sxs-lookup"><span data-stu-id="70a3d-206">In this article, we use MongoDB toostore our tasks.</span></span> <span data-ttu-id="70a3d-207">我們在「步驟 4」中討論到這一點。</span><span class="sxs-lookup"><span data-stu-id="70a3d-207">We discuss this in *step 4*.</span></span>

<span data-ttu-id="70a3d-208">在您建立的步驟 11 hello Config.js 檔案，您的資料庫稱為*tasklist*。</span><span class="sxs-lookup"><span data-stu-id="70a3d-208">In hello Config.js file you created in step 11, your database is called *tasklist*.</span></span> <span data-ttu-id="70a3d-209">這是您放置在 hello mongoose_auth_local 連線 URL 的結尾。</span><span class="sxs-lookup"><span data-stu-id="70a3d-209">That was what you put at hello end of your mongoose_auth_local connection URL.</span></span> <span data-ttu-id="70a3d-210">您不需要 toocreate MongoDB 事先的這個資料庫。</span><span class="sxs-lookup"><span data-stu-id="70a3d-210">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="70a3d-211">hello 資料庫上建立 hello 第一次執行的伺服器應用程式 （假設 hello 資料庫尚未存在）。</span><span class="sxs-lookup"><span data-stu-id="70a3d-211">hello database is created on hello first run of your server application (assuming hello database does not already exist).</span></span>

<span data-ttu-id="70a3d-212">您告知 hello 伺服器哪些 MongoDB 資料庫 toouse。</span><span class="sxs-lookup"><span data-stu-id="70a3d-212">You've told hello server what MongoDB database toouse.</span></span> <span data-ttu-id="70a3d-213">接下來，您需要 toowrite 一些額外的程式碼 toocreate hello 模型和結構描述伺服器的工作。</span><span class="sxs-lookup"><span data-stu-id="70a3d-213">Next, you need toowrite some additional code toocreate hello model and schema for your server's tasks.</span></span>

### <a name="hello-model"></a><span data-ttu-id="70a3d-214">hello 模型</span><span class="sxs-lookup"><span data-stu-id="70a3d-214">hello model</span></span>
<span data-ttu-id="70a3d-215">hello 結構描述模型是非常基本。</span><span class="sxs-lookup"><span data-stu-id="70a3d-215">hello schema model is very basic.</span></span> <span data-ttu-id="70a3d-216">需要的話，您可以展開它。</span><span class="sxs-lookup"><span data-stu-id="70a3d-216">You can expand it if you need to.</span></span> 

<span data-ttu-id="70a3d-217">hello 結構描述模型有下列值：</span><span class="sxs-lookup"><span data-stu-id="70a3d-217">hello schema model has these values:</span></span>

*   <span data-ttu-id="70a3d-218">**NAME**。</span><span class="sxs-lookup"><span data-stu-id="70a3d-218">**NAME**.</span></span> <span data-ttu-id="70a3d-219">hello 人員指派的 toohello 工作。</span><span class="sxs-lookup"><span data-stu-id="70a3d-219">hello person assigned toohello task.</span></span> <span data-ttu-id="70a3d-220">這是**字串**值。</span><span class="sxs-lookup"><span data-stu-id="70a3d-220">This is a **string** value.</span></span>
*   <span data-ttu-id="70a3d-221">**TASK**。</span><span class="sxs-lookup"><span data-stu-id="70a3d-221">**TASK**.</span></span> <span data-ttu-id="70a3d-222">hello hello 工作名稱。</span><span class="sxs-lookup"><span data-stu-id="70a3d-222">hello name of hello task.</span></span> <span data-ttu-id="70a3d-223">這是**字串**值。</span><span class="sxs-lookup"><span data-stu-id="70a3d-223">This is a **string** value.</span></span>
*   <span data-ttu-id="70a3d-224">**DATE**。</span><span class="sxs-lookup"><span data-stu-id="70a3d-224">**DATE**.</span></span> <span data-ttu-id="70a3d-225">hello 日期該 hello 工作會到期。</span><span class="sxs-lookup"><span data-stu-id="70a3d-225">hello date that hello task is due.</span></span> <span data-ttu-id="70a3d-226">這是**日期時間**值。</span><span class="sxs-lookup"><span data-stu-id="70a3d-226">This is a **datetime** value.</span></span>
*   <span data-ttu-id="70a3d-227">**COMPLETED**。</span><span class="sxs-lookup"><span data-stu-id="70a3d-227">**COMPLETED**.</span></span> <span data-ttu-id="70a3d-228">Hello 工作是否完成。</span><span class="sxs-lookup"><span data-stu-id="70a3d-228">Whether hello task is completed.</span></span> <span data-ttu-id="70a3d-229">這是**布林**值。</span><span class="sxs-lookup"><span data-stu-id="70a3d-229">This is a **Boolean** value.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="70a3d-230">建立 hello 程式碼中的 hello 結構描述</span><span class="sxs-lookup"><span data-stu-id="70a3d-230">Create hello schema in hello code</span></span>
1.  <span data-ttu-id="70a3d-231">在命令提示字元中，變更 hello 目錄太**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="70a3d-231">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="70a3d-232">在編輯器中開啟 Server.js。</span><span class="sxs-lookup"><span data-stu-id="70a3d-232">In your editor, open Server.js.</span></span> <span data-ttu-id="70a3d-233">下方 hello 組態項目加入 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="70a3d-233">Below hello configuration entry, add hello following information:</span></span>

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

<span data-ttu-id="70a3d-234">此程式碼會 toohello MongoDB 伺服器連接。</span><span class="sxs-lookup"><span data-stu-id="70a3d-234">This code connects toohello MongoDB server.</span></span> <span data-ttu-id="70a3d-235">它也會傳回結構描述物件。</span><span class="sxs-lookup"><span data-stu-id="70a3d-235">It also returns a schema object.</span></span>

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a><span data-ttu-id="70a3d-236">使用 hello 結構描述，在 hello 程式碼中建立您的模型</span><span class="sxs-lookup"><span data-stu-id="70a3d-236">Using hello schema, create your model in hello code</span></span>
<span data-ttu-id="70a3d-237">下方 hello 前面程式碼，加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="70a3d-237">Below hello preceding code, add hello following code:</span></span>

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

<span data-ttu-id="70a3d-238">如您所見從 hello 程式碼，首先請建立您的結構描述。</span><span class="sxs-lookup"><span data-stu-id="70a3d-238">As you can tell from hello code, first you create your schema.</span></span> <span data-ttu-id="70a3d-239">接下來，您可以建立模型物件。</span><span class="sxs-lookup"><span data-stu-id="70a3d-239">Next, you create a model object.</span></span> <span data-ttu-id="70a3d-240">使用 hello 模型物件 toostore hello 整個資料程式碼，當您定義您**路由**。</span><span class="sxs-lookup"><span data-stu-id="70a3d-240">You use hello model object toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a><span data-ttu-id="70a3d-241">13：新增工作 REST API 伺服器的路由</span><span class="sxs-lookup"><span data-stu-id="70a3d-241">13: Add your routes for your task REST API server</span></span>
<span data-ttu-id="70a3d-242">現在您有與資料庫模型 toowork，新增 hello 路由，您會使用 REST API 伺服器。</span><span class="sxs-lookup"><span data-stu-id="70a3d-242">Now that you have a database model toowork with, add hello routes you'll use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="70a3d-243">關於 restify 中的路由</span><span class="sxs-lookup"><span data-stu-id="70a3d-243">About routes in restify</span></span>
<span data-ttu-id="70a3d-244">中的路由 restify 完全 hello 如此當您使用的相同方式 hello Express 堆疊的工作。</span><span class="sxs-lookup"><span data-stu-id="70a3d-244">Routes in restify work exactly hello same way they do when you use hello Express stack.</span></span> <span data-ttu-id="70a3d-245">您可以使用 hello 您預期 hello 用戶端應用程式 toocall 的 URI，以定義路由。</span><span class="sxs-lookup"><span data-stu-id="70a3d-245">You define routes by using hello URI that you expect hello client applications toocall.</span></span> <span data-ttu-id="70a3d-246">通常，您會在個別的檔案中定義您的路由。</span><span class="sxs-lookup"><span data-stu-id="70a3d-246">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="70a3d-247">在本教學課程中，我們會將路由放在 Server.js 中。</span><span class="sxs-lookup"><span data-stu-id="70a3d-247">In this tutorial, we put our routes in Server.js.</span></span> <span data-ttu-id="70a3d-248">在生產用途上，建議您將這些路由納入您自己的檔案中。</span><span class="sxs-lookup"><span data-stu-id="70a3d-248">For production use, we recommend that you factor routes into their own file.</span></span>

<span data-ttu-id="70a3d-249">Restify 路由的典型模式是：</span><span class="sxs-lookup"><span data-stu-id="70a3d-249">A typical pattern for a restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="70a3d-250">這是在 hello 最基本的層級的 hello 模式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-250">This is hello pattern at hello most basic level.</span></span> <span data-ttu-id="70a3d-251">Restify （和 Express） 提供更深層的功能，例如 hello 能力 toodefine 應用程式類型和複雜的路由，不同的端點上。</span><span class="sxs-lookup"><span data-stu-id="70a3d-251">Restify (and Express) provide much deeper functionality, like hello ability toodefine application types, and complex routing across different endpoints.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="70a3d-252">新增預設路由 tooyour 伺服器</span><span class="sxs-lookup"><span data-stu-id="70a3d-252">Add default routes tooyour server</span></span>
<span data-ttu-id="70a3d-253">新增基本 CRUD 路由 hello:**建立**，**擷取**，**更新**，和**刪除**。</span><span class="sxs-lookup"><span data-stu-id="70a3d-253">Add hello basic CRUD routes: **create**, **retrieve**, **update**, and **delete**.</span></span>

1.  <span data-ttu-id="70a3d-254">在命令提示字元中，變更 hello 目錄太**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="70a3d-254">At a command prompt, change hello directory too**azuread**:</span></span>

    `cd azuread`

2.  <span data-ttu-id="70a3d-255">在編輯器中開啟 Server.js。</span><span class="sxs-lookup"><span data-stu-id="70a3d-255">In an editor, open Server.js.</span></span> <span data-ttu-id="70a3d-256">下面 hello 您稍早建立的資料庫項目、 新增 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="70a3d-256">Below hello database entries you made earlier, add hello following information:</span></span>

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
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
    req.log.warn(err, 'createTask: unable toosave');
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
    'removeTask: unable toodelete %s',
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
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
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
    log.warn(err, "There are no tasks in hello database. Add one!");
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

### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="70a3d-257">加入 hello 路由的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="70a3d-257">Add error handling for hello routes</span></span>
<span data-ttu-id="70a3d-258">加入一些錯誤，處理讓您能夠通訊回復 toohello hello 您遇到的問題相關的用戶端。</span><span class="sxs-lookup"><span data-stu-id="70a3d-258">Add some error handling so you can communicate back toohello client about hello problem you encountered.</span></span>

<span data-ttu-id="70a3d-259">新增下列 hello 程式碼，您已經撰寫下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="70a3d-259">Add hello following code below hello code, which you've already written:</span></span>

```Javascript
///--- Errors for communicating something more information back toohello client.
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


## <a name="14-create-your-server"></a><span data-ttu-id="70a3d-260">14：建立伺服器</span><span class="sxs-lookup"><span data-stu-id="70a3d-260">14: Create your server</span></span>
<span data-ttu-id="70a3d-261">hello 最後一件事 toodo 是 tooadd 您的伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="70a3d-261">hello last thing toodo is tooadd your server instance.</span></span> <span data-ttu-id="70a3d-262">hello 伺服器執行個體都會管理您的呼叫。</span><span class="sxs-lookup"><span data-stu-id="70a3d-262">hello server instance manages your calls.</span></span>

<span data-ttu-id="70a3d-263">Restify (及 Express) 有深入的自訂功能可搭配 REST API 伺服器使用。</span><span class="sxs-lookup"><span data-stu-id="70a3d-263">Restify (and Express) have deep customization that you can use with a REST API server.</span></span> <span data-ttu-id="70a3d-264">在本教學課程中，我們使用 hello 最基本的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-264">In this tutorial, we use hello most basic setup.</span></span>

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
// Allow 5 requests/second by IP address, and burst too10.
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
## <a name="15-add-hello-routes-without-authentication-for-now"></a><span data-ttu-id="70a3d-265">15： 加入 hello 路由 （不含的立即驗證）</span><span class="sxs-lookup"><span data-stu-id="70a3d-265">15: Add hello routes (without authentication, for now)</span></span>
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
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
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a><span data-ttu-id="70a3d-266">16： 執行 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="70a3d-266">16: Run hello server</span></span>
<span data-ttu-id="70a3d-267">它是個不錯的主意 tootest 您之前加入驗證的伺服器。</span><span class="sxs-lookup"><span data-stu-id="70a3d-267">It's a good idea tootest your server before you add authentication.</span></span>

<span data-ttu-id="70a3d-268">最簡單方式 tootest hello 您的伺服器是在命令提示字元使用 curl。</span><span class="sxs-lookup"><span data-stu-id="70a3d-268">hello easiest way tootest your server is by using curl at a command prompt.</span></span> <span data-ttu-id="70a3d-269">toodo，您需要簡單的公用程式，可讓您 tooparse 輸出為 JSON。</span><span class="sxs-lookup"><span data-stu-id="70a3d-269">toodo this, you need a simple utility that you can use tooparse output as JSON.</span></span> 

1.  <span data-ttu-id="70a3d-270">安裝 hello 遵循範例中的 hello JSON 工具，我們使用：</span><span class="sxs-lookup"><span data-stu-id="70a3d-270">Install hello JSON tool that we use in hello following examples:</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="70a3d-271">這會安裝 hello JSON 工具全域。</span><span class="sxs-lookup"><span data-stu-id="70a3d-271">This installs hello JSON tool globally.</span></span>

2.  <span data-ttu-id="70a3d-272">請確定您的 MongoDB 執行個體正在執行：</span><span class="sxs-lookup"><span data-stu-id="70a3d-272">Make sure that your MongoDB instance is running:</span></span>

    `$sudo mongod`

3.  <span data-ttu-id="70a3d-273">變更 hello 目錄太**azure ad**，然後執行 curl:</span><span class="sxs-lookup"><span data-stu-id="70a3d-273">Change hello directory too**azuread**, and then run curl:</span></span>

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

4.  <span data-ttu-id="70a3d-274">tooadd 工作：</span><span class="sxs-lookup"><span data-stu-id="70a3d-274">tooadd a task:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    <span data-ttu-id="70a3d-275">應該 hello 回應：</span><span class="sxs-lookup"><span data-stu-id="70a3d-275">hello response should be:</span></span>

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

5.  <span data-ttu-id="70a3d-276">Brandon 的工作清單︰</span><span class="sxs-lookup"><span data-stu-id="70a3d-276">List tasks for Brandon:</span></span>

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="70a3d-277">如果所有這些命令會執行不會發生錯誤，您就準備好 tooadd OAuth toohello REST API 伺服器。</span><span class="sxs-lookup"><span data-stu-id="70a3d-277">If all these commands run without errors, you are ready tooadd OAuth toohello REST API server.</span></span>

<span data-ttu-id="70a3d-278">「您現在已具有 REST API 伺服器和 MongoDB！」</span><span class="sxs-lookup"><span data-stu-id="70a3d-278">*You now have a REST API server with MongoDB!*</span></span>

## <a name="17-add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="70a3d-279">17： 加入驗證 tooyour REST API 伺服器</span><span class="sxs-lookup"><span data-stu-id="70a3d-279">17: Add authentication tooyour REST API server</span></span>
<span data-ttu-id="70a3d-280">既然您已執行的 REST API 時，設定 toouse 它與 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="70a3d-280">Now that you have a running REST API, set it up toouse it with Azure AD.</span></span>

<span data-ttu-id="70a3d-281">在命令提示字元中，變更 hello 目錄太**azure ad**:</span><span class="sxs-lookup"><span data-stu-id="70a3d-281">At a command prompt, change hello directory too**azuread**:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a><span data-ttu-id="70a3d-282">使用 hello oidcbearerstrategy，並包含的 passport azure ad</span><span class="sxs-lookup"><span data-stu-id="70a3d-282">Use hello oidcbearerstrategy that's included with passport-azure-ad</span></span>
<span data-ttu-id="70a3d-283">到目前為止，您已經建置典型的 REST TODO 伺服器，且其中不含任何授權種類。</span><span class="sxs-lookup"><span data-stu-id="70a3d-283">So far, you've built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="70a3d-284">現在，新增驗證。</span><span class="sxs-lookup"><span data-stu-id="70a3d-284">Now, add authentication.</span></span>

<span data-ttu-id="70a3d-285">首先，表示您想要 toouse Passport。</span><span class="sxs-lookup"><span data-stu-id="70a3d-285">First,  indicate that you want toouse Passport.</span></span> <span data-ttu-id="70a3d-286">將這段程式碼放在緊鄰您先前的伺服器設定後面：</span><span class="sxs-lookup"><span data-stu-id="70a3d-286">Put this right after your earlier server configuration:</span></span>

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="70a3d-287">當您撰寫應用程式開發介面時，它會為從 hello 使用者的 hello 權杖的唯一資料 toosomething 無法偽造最好 tooalways 連結 hello。</span><span class="sxs-lookup"><span data-stu-id="70a3d-287">When you write APIs, it's a good idea tooalways link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="70a3d-288">當這個伺服器儲存 TODO 項目時，它會儲存根據 hello 權杖 （稱為透過 token.sub） 中的 hello 使用者訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="70a3d-288">When this server stores TODO items, it stores them based on hello user subscription ID in hello token (called through token.sub).</span></span> <span data-ttu-id="70a3d-289">您可以將 hello token.sub hello 「 擁有者 」 欄位中。</span><span class="sxs-lookup"><span data-stu-id="70a3d-289">You put hello token.sub in hello “owner” field.</span></span> <span data-ttu-id="70a3d-290">這可確保只有該使用者可以存取 hello 使用者 TODOs。</span><span class="sxs-lookup"><span data-stu-id="70a3d-290">This ensures that only that user can access hello user's TODOs.</span></span> <span data-ttu-id="70a3d-291">沒有其他人可以存取已輸入的 hello TODOs。</span><span class="sxs-lookup"><span data-stu-id="70a3d-291">No one else can access hello TODOs that were entered.</span></span> <span data-ttu-id="70a3d-292">沒有公開正在 hello 應用程式開發介面的 「 擁有者 」。</span><span class="sxs-lookup"><span data-stu-id="70a3d-292">There is no exposure in hello API for “owner.”</span></span> <span data-ttu-id="70a3d-293">外部使用者可以要求其他使用者的 TODO (即使通過驗證)。</span><span class="sxs-lookup"><span data-stu-id="70a3d-293">An external user can request other users' TODOs, even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="70a3d-294">接下來，使用隨附的 hello 開啟識別碼連接承載策略`passport-azure-ad`。</span><span class="sxs-lookup"><span data-stu-id="70a3d-294">Next, use hello Open ID Connect Bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="70a3d-295">將這段程式碼放在您稍早貼上的程式碼後面：</span><span class="sxs-lookup"><span data-stu-id="70a3d-295">Put this after what you pasted earlier:</span></span>

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
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
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
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

<span data-ttu-id="70a3d-296">Passport 會針對其所有策略 (Twitter、Facebook 等) 使用類似的模式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-296">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="70a3d-297">所有的策略寫入器會遵守 toohello 模式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-297">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="70a3d-298">傳送嗨策略`function()`使用語彙基元和`done`做為參數。</span><span class="sxs-lookup"><span data-stu-id="70a3d-298">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="70a3d-299">所有其功能之後，就會傳回 hello 策略。</span><span class="sxs-lookup"><span data-stu-id="70a3d-299">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="70a3d-300">儲存 hello 使用者並存放 hello 語彙基元，因此您不需要為其 tooask 一次。</span><span class="sxs-lookup"><span data-stu-id="70a3d-300">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70a3d-301">hello 上述程式碼會採用任何使用者，可以驗證 tooyour 伺服器。</span><span class="sxs-lookup"><span data-stu-id="70a3d-301">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="70a3d-302">這就是所謂的自動註冊。</span><span class="sxs-lookup"><span data-stu-id="70a3d-302">This is known as auto-registration.</span></span> <span data-ttu-id="70a3d-303">在實際執行伺服器上，您不想 toolet 任何人而不需要先經過您選擇註冊程序，它們。</span><span class="sxs-lookup"><span data-stu-id="70a3d-303">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="70a3d-304">這通常是您在取用者應用程式中看到的 hello 模式。</span><span class="sxs-lookup"><span data-stu-id="70a3d-304">This is usually hello pattern you see in consumer apps.</span></span> <span data-ttu-id="70a3d-305">hello 應用程式可能會讓您與 Facebook tooregister 但然後它會要求您 tooenter 其他資訊。</span><span class="sxs-lookup"><span data-stu-id="70a3d-305">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="70a3d-306">如果您沒有使用命令列程式在此教學課程，您無法從 hello 傳回的語彙基元物件擷取 hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="70a3d-306">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="70a3d-307">然後，您可能會要求 hello 使用者 tooenter 額外資訊。</span><span class="sxs-lookup"><span data-stu-id="70a3d-307">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="70a3d-308">因為這是在測試伺服器，您會加入 hello 使用者直接 toohello 記憶體中資料庫。</span><span class="sxs-lookup"><span data-stu-id="70a3d-308">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
> 
> 

### <a name="protect-endpoints"></a><span data-ttu-id="70a3d-309">保護端點</span><span class="sxs-lookup"><span data-stu-id="70a3d-309">Protect endpoints</span></span>
<span data-ttu-id="70a3d-310">藉由指定 hello 保護端點**passport.authenticate()**想 toouse hello 通訊協定呼叫。</span><span class="sxs-lookup"><span data-stu-id="70a3d-310">Protect endpoints by specifying hello **passport.authenticate()** call with hello protocol that you want toouse.</span></span>

<span data-ttu-id="70a3d-311">您可以在伺服器程式碼中編輯路由，以利用更進階的選項︰</span><span class="sxs-lookup"><span data-stu-id="70a3d-311">You can edit your route in your server code for a more advanced option:</span></span>

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

## <a name="18-run-your-server-application-again"></a><span data-ttu-id="70a3d-312">18︰再次執行伺服器應用程式</span><span class="sxs-lookup"><span data-stu-id="70a3d-312">18: Run your server application again</span></span>
<span data-ttu-id="70a3d-313">使用 curl 再次 toosee，如果您有 OAuth 2.0 保護對您的端點。</span><span class="sxs-lookup"><span data-stu-id="70a3d-313">Use curl again toosee if you have OAuth 2.0 protection against your endpoints.</span></span> <span data-ttu-id="70a3d-314">請在您針對這個端點執行任何用戶端 SDK 之前這樣做。</span><span class="sxs-lookup"><span data-stu-id="70a3d-314">Do this before you run any of your client SDKs against this endpoint.</span></span> <span data-ttu-id="70a3d-315">傳回的 hello 標頭應該告知您的驗證是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="70a3d-315">hello headers returned should tell you if your authentication is working correctly.</span></span>

1.  <span data-ttu-id="70a3d-316">請確定您的 MongoDB 執行個體正在執行：</span><span class="sxs-lookup"><span data-stu-id="70a3d-316">Make sure that your MongoDB isntance is running:</span></span>

    `$sudo mongod`

2.  <span data-ttu-id="70a3d-317">變更 toohello **azure ad**目錄，再使用 curl:</span><span class="sxs-lookup"><span data-stu-id="70a3d-317">Change toohello **azuread** directory, and then use curl:</span></span>

    `$ cd azuread`

    `$ node server.js`

3.  <span data-ttu-id="70a3d-318">嘗試基本的 POST 方法：</span><span class="sxs-lookup"><span data-stu-id="70a3d-318">Try a basic POST:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="70a3d-319">401 回應指出 hello Passport 該層正嘗試 tooredirect toohello 授權端點，而這正是您想要。</span><span class="sxs-lookup"><span data-stu-id="70a3d-319">A 401 response indicates that hello Passport layer is trying tooredirect toohello authorize endpoint, which is exactly what you want.</span></span>

<span data-ttu-id="70a3d-320">「您現在擁有一項使用 OAuth 2.0 的 REST API 服務！」</span><span class="sxs-lookup"><span data-stu-id="70a3d-320">*You now have a REST API service that uses OAuth 2.0!*</span></span>

<span data-ttu-id="70a3d-321">在未使用 OAuth 2.0 相容用戶端的情況下，您已經儘可能地使用此伺服器的所有功能。</span><span class="sxs-lookup"><span data-stu-id="70a3d-321">You've gone as far as you can with this server without using an OAuth 2.0-compatible client.</span></span> <span data-ttu-id="70a3d-322">因此，您需要 tooreview 其他教學課程。</span><span class="sxs-lookup"><span data-stu-id="70a3d-322">For that, you will need tooreview an additional tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70a3d-323">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70a3d-323">Next steps</span></span>
<span data-ttu-id="70a3d-324">供參考，完成的 hello 範例 （不含您的組態值） 依現狀[.zip 檔案](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip)。</span><span class="sxs-lookup"><span data-stu-id="70a3d-324">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="70a3d-325">您也可以從 GitHub 加以複製：</span><span class="sxs-lookup"><span data-stu-id="70a3d-325">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="70a3d-326">現在，您可以移動 toomore 進階主題上。</span><span class="sxs-lookup"><span data-stu-id="70a3d-326">Now, you can move on toomore advanced topics.</span></span> <span data-ttu-id="70a3d-327">您可能會想 tootry[安全 Node.js web 應用程式使用 hello v2.0 端點](active-directory-v2-devquickstarts-node-web.md)。</span><span class="sxs-lookup"><span data-stu-id="70a3d-327">You might want tootry [Secure a Node.js web app using hello v2.0 endpoint](active-directory-v2-devquickstarts-node-web.md).</span></span>

<span data-ttu-id="70a3d-328">以下是一些其他資源：</span><span class="sxs-lookup"><span data-stu-id="70a3d-328">Here are some additional resources:</span></span>

* [<span data-ttu-id="70a3d-329">Azure AD v2.0 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="70a3d-329">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="70a3d-330">Stack Overflow "azure-active-directory" 標籤 (英文)</span><span class="sxs-lookup"><span data-stu-id="70a3d-330">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="70a3d-331">取得產品的安全性更新</span><span class="sxs-lookup"><span data-stu-id="70a3d-331">Get security updates for our products</span></span>
<span data-ttu-id="70a3d-332">我們鼓勵 toosign 向上 toobe 安全性事件發生時收到通知。</span><span class="sxs-lookup"><span data-stu-id="70a3d-332">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="70a3d-333">在 hello [Microsoft 技術安全性通知](https://technet.microsoft.com/security/dd252948)頁面上，訂閱 tooSecurity 摘要報告警示。</span><span class="sxs-lookup"><span data-stu-id="70a3d-333">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

