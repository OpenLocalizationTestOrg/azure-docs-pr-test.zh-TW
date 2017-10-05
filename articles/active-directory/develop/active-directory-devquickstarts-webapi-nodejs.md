---
title: "Azure AD Node.js 入門 | Microsoft Docs"
description: "如何建立可整合 Azure AD 以進行驗證的 Node.js REST Web API。"
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="7b8a4-103">開始使用適用於 Node.js 的 Web API</span><span class="sxs-lookup"><span data-stu-id="7b8a4-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="7b8a4-104">*Passport* 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="7b8a4-105">您可以暗中將極具彈性且模組化的 Passport 放入任何 Express 架構或 Restify Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="7b8a4-106">一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他等驗證。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="7b8a4-107">我們已為 Microsoft Azure Active Directory (Azure AD) 開發一項策略。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7b8a4-108">我們將安裝此模組，然後加入 Microsoft Azure Active Directory `passport-azure-ad` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="7b8a4-109">若要這樣做，您需要：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-109">To do this, you need to:</span></span>

1. <span data-ttu-id="7b8a4-110">向 Azure AD 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="7b8a4-111">設定您的應用程式來使用 Passport 的 `passport-azure-ad` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="7b8a4-112">設定用戶端應用程式呼叫待辦事項清單 Web API。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="7b8a4-113">本教學課程的程式碼保留在 [GitHub](https://github.com/Azure-Samples/active-directory-node-webapi)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="7b8a4-114">本文不涵蓋如何使用 Azure AD B2C 實作登入、註冊或管理設定檔。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="7b8a4-115">而會著重在如何在使用者已通過驗證後呼叫 Web API。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="7b8a4-116">我們建議您從[如何與 Azure Active Directory 整合文件](active-directory-how-to-integrate.md)著手，以了解 Azure Active Directory 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="7b8a4-117">我們已在 MIT 授權底下的 GitHub 中發行這個執行範例的所有原始程式碼，因此您可以隨意複製 (或更棒的是您可以分散出去) 和提供意見反應及提取要求。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="7b8a4-118">關於 Node.js 模組</span><span class="sxs-lookup"><span data-stu-id="7b8a4-118">About Node.js modules</span></span>
<span data-ttu-id="7b8a4-119">我們會在本逐步解說中使用 Node.js 模組。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="7b8a4-120">模組是指可載入的 JavaScript 封裝，可為您的應用程式提供特定功能。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="7b8a4-121">您通常可以使用 NPM 安裝目錄中的 Node.js NPM 命令列工具來安裝模組。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="7b8a4-122">但是，核心 Node.js 封裝中已包含一些模組 (例如 HTTP 模組)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="7b8a4-123">已安裝的模組會儲存在 Node.js 安裝目錄的根目錄下的 **node_modules** 目錄。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="7b8a4-124">**node_modules** 目錄下的每個模組都會維護它自己的 **node_modules** 目錄，其中包含它所依賴的任何模組。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="7b8a4-125">此外，每個必要模組都有**node_modules** 目錄。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="7b8a4-126">這個遞迴目錄結構表示相依性鏈結。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="7b8a4-127">此相依性鏈結結構會導致較高的應用程式使用量。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="7b8a4-128">但它也會保證已符合所有相依性，而且用於開發的模組版本也會用於生產環境中。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="7b8a4-129">這可讓實際執行的應用程式行為更容易預測，並防止可能會影響使用者的版本控制問題。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="7b8a4-130">步驟 1：註冊 Azure AD 租用戶</span><span class="sxs-lookup"><span data-stu-id="7b8a4-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="7b8a4-131">若要使用這個範例，您需要 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="7b8a4-132">如果您不確定什麼是租用戶或如何取得租用戶，請參閱[如何取得 Azure AD 租用戶](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="7b8a4-133">步驟 2：建立應用程式</span><span class="sxs-lookup"><span data-stu-id="7b8a4-133">Step 2: Create an application</span></span>
<span data-ttu-id="7b8a4-134">接下來，在您的目錄中建立應用程式，以提供必要資訊給 Azure AD，讓它與應用程式安全地通訊。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="7b8a4-135">在此案例中，因為用戶端應用程式和 Web API 會組成一個邏輯應用程式，所以由單一**應用程式識別碼**表示。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="7b8a4-136">如果要建立應用程式，請遵循 [這些指示](active-directory-how-applications-are-added.md)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="7b8a4-137">如果您要建置企業營運應用程式，[這些額外的指示可能很實用](../active-directory-applications-guiding-developers-for-lob-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="7b8a4-138">若要建立應用程式：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-138">To create an application:</span></span>

1. <span data-ttu-id="7b8a4-139">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7b8a4-140">在頂端功能表上，選取您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-140">On the top menu, select your account.</span></span> <span data-ttu-id="7b8a4-141">然後，在 [目錄] 清單下，選擇您要註冊應用程式的 Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="7b8a4-142">在左側功能表中選取 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="7b8a4-143">選取 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="7b8a4-144">遵照提示建立 **Web 應用程式和/或 Web API**。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="7b8a4-145">應用程式的 [名稱] 對使用者說明您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="7b8a4-146">[ **登入 URL** ] 是指應用程式的基底 URL。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="7b8a4-147">範例程式碼的預設 URL 是 `https://localhost:8080`。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="7b8a4-148">註冊之後，Azure AD 會指派唯一的應用程式識別碼給您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="7b8a4-149">您會在後續章節中用到這個值，所以請從應用程式頁面中複製此值。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="7b8a4-150">從應用程式的 [設定]  ->  [屬性] 頁面，更新應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="7b8a4-151">[ **應用程式識別碼 URI** ] 是指應用程式的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="7b8a4-152">慣例是使用 `https://<tenant-domain>/<app-name>`，例如：`https://contoso.onmicrosoft.com/my-first-aad-app`。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="7b8a4-153">從 [設定] 頁面建立應用程式的 [金鑰]，然後複製在某處。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="7b8a4-154">稍後您將會用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="7b8a4-155">步驟 3：下載您的平台適用的 Node.js</span><span class="sxs-lookup"><span data-stu-id="7b8a4-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="7b8a4-156">若要成功使用此範例，您必須具備已成功安裝的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="7b8a4-157">從 [http://nodejs.org](http://nodejs.org)安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="7b8a4-158">步驟 4：在您的平台上安裝 MongoDB</span><span class="sxs-lookup"><span data-stu-id="7b8a4-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="7b8a4-159">若要成功使用此範例，您必須具備已成功安裝的 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="7b8a4-160">您可使用 MongoDB，讓 REST API 得以在不同伺服器執行個體之間持續使用。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="7b8a4-161">從 [http://mongodb.org](http://www.mongodb.org)安裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="7b8a4-162">本逐步解說假設您會使用 MongoDB 的預設安裝和伺服器端點，在撰寫本文時為 mongodb://localhost。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="7b8a4-163">步驟 5：在您的 Web API 中安裝 Restify 模組</span><span class="sxs-lookup"><span data-stu-id="7b8a4-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="7b8a4-164">我們會使用 Resitfy 來建置 REST API。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="7b8a4-165">Restify 是衍生自 Express 的最小且具彈性的 Node.js 應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="7b8a4-166">它有一組強大的功能，可在 Connect 之上建置 REST API。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="7b8a4-167">安裝 Restify</span><span class="sxs-lookup"><span data-stu-id="7b8a4-167">Install Restify</span></span>
1. <span data-ttu-id="7b8a4-168">從命令列將目錄變更至 **azuread** 目錄。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="7b8a4-169">如果 **azuread** 目錄不存在，請予以建立。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="7b8a4-170">輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="7b8a4-171">此命令會安裝 Restify。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="7b8a4-172">您有收到錯誤訊息嗎？</span><span class="sxs-lookup"><span data-stu-id="7b8a4-172">Did you get an error?</span></span>
<span data-ttu-id="7b8a4-173">當您在某些作業系統上使用 NPM 時，可能會收到以下錯誤：**Error: EPERM, chmod '/usr/local/bin/..'**</span><span class="sxs-lookup"><span data-stu-id="7b8a4-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="7b8a4-174">，且建議您嘗試以管理員身分執行該帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="7b8a4-175">若發生這個情況，使用 sudo 命令以更高的權限層級執行 NPM。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="7b8a4-176">您有收到有關 DTRACE 的錯誤訊息嗎？</span><span class="sxs-lookup"><span data-stu-id="7b8a4-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="7b8a4-177">安裝 Restify 時，您可能會看到如下的錯誤：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-177">You might see an error like this when installing Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
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
<span data-ttu-id="7b8a4-178">Restify 提供強大機制來使用 DTrace 追蹤 REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="7b8a4-179">不過，許多作業系統沒有 DTrace。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="7b8a4-180">您可以放心地忽略這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="7b8a4-181">此命令的輸出應類似下列輸出：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-181">The output of this command should look similar to the following output:</span></span>

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
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="7b8a4-182">步驟 6：在您的 Web API 中安裝 Passport.js</span><span class="sxs-lookup"><span data-stu-id="7b8a4-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="7b8a4-183">[Passport](http://passportjs.org/) 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="7b8a4-184">您可以暗中將極具彈性且模組化的 Passport 放入任何 Express 架構或 Restify Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="7b8a4-185">一組完整的策略可支援使用使用者名稱和密碼、Facebook、Twitter 及其他等驗證。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="7b8a4-186">我們已為 Azure Active Directory 開發一個策略。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="7b8a4-187">我們會安裝此模組，然後加入 Azure Active Directory 的策略外掛程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="7b8a4-188">從命令列將目錄變更至 **azuread** 目錄。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="7b8a4-189">若要安裝 passport.js，請輸入以下命令：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="7b8a4-190">此命令的輸出應類似這樣：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="7b8a4-191">步驟 7：將 Passport-Azure-AD 新增至您的 Web API</span><span class="sxs-lookup"><span data-stu-id="7b8a4-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="7b8a4-192">接下來，我們會使用 `passport-azure-ad` 來新增 OAuth 策略，這是一套將 Azure Active Directory 連線到 Passport 的策略。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="7b8a4-193">在這個 Rest API 範例中，我們會對持有人權杖使用此策略。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="7b8a4-194">雖然 OAuth2 提供可發行任何已知權杖類型的架構，但只有某些權杖類型經常使用。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="7b8a4-195">持有人權杖是最常用於保護端點的權杖。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="7b8a4-196">這是 OAuth2 中最普遍發行的權杖類型。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="7b8a4-197">許多實作假設持有人權杖是唯一發行的權杖類型。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="7b8a4-198">從命令列將目錄變更至 **azuread** 目錄。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="7b8a4-199">輸入下列命令以安裝 Passport.js `passport-azure-ad module`：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="7b8a4-200">此命令的輸出應類似下列輸出：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-200">The output of the command should look similar to the following output:</span></span>


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



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="7b8a4-201">步驟 8：將 MongoDB 模組新增至 Web API</span><span class="sxs-lookup"><span data-stu-id="7b8a4-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="7b8a4-202">我們使用 MongoDB 做為資料存放區。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="7b8a4-203">基於這個理由，我們必須安裝廣泛使用的外掛程式 Mongoose 來管理模型與結構描述。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="7b8a4-204">我們也必須安裝 MongoDB 的資料庫驅動程式 (同樣也稱為 MongoDB)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="7b8a4-205">步驟 9：安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="7b8a4-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="7b8a4-206">接下來，我們會安裝其餘所需的模組。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="7b8a4-207">從命令列將目錄變更至 **azuread** 資料夾 (如果您尚未在此目錄中)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7b8a4-208">輸入下列命令，在您的 **node_modules** 目錄中安裝下列模組：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="7b8a4-209">步驟 10：使用您的相依性建立 server.js</span><span class="sxs-lookup"><span data-stu-id="7b8a4-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="7b8a4-210">server.js 檔案會提供 Web API 伺服器的大部分功能。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="7b8a4-211">我們會將大部分的程式碼新增至此檔案。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-211">We add most of our code to this file.</span></span> <span data-ttu-id="7b8a4-212">基於生產目的，我們建議您將功能重整成較小的檔案，例如單獨分開的路由和控制器。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="7b8a4-213">在此示範中，我們會在這項功能中使用 server.js。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="7b8a4-214">從命令列將目錄變更至 **azuread** 資料夾 (如果您尚未在此目錄中)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7b8a4-215">在喜愛的編輯器中建立 `server.js` 檔案，然後新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="7b8a4-216">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-216">Save the file.</span></span> <span data-ttu-id="7b8a4-217">我們稍後會再回到此檔案。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="7b8a4-218">步驟 11：建立可儲存您的 Azure AD 設定的組態檔</span><span class="sxs-lookup"><span data-stu-id="7b8a4-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="7b8a4-219">這個程式碼檔會將設定參數從您的 Azure Active Directory 入口網站傳遞到 Passport.js。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="7b8a4-220">您會在將 Web API 新增至入口網站 (本逐步解說的第一個部分) 時建立這些設定值。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="7b8a4-221">在您複製程式碼之後，我們會說明要放入這些參數值的內容。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="7b8a4-222">從命令列將目錄變更至 **azuread** 資料夾 (如果您尚未在此目錄中)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7b8a4-223">在喜愛的編輯器中建立 `config.js` 檔案，然後新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="7b8a4-224">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="7b8a4-225">步驟 12：將組態值新增至 server.js 檔案</span><span class="sxs-lookup"><span data-stu-id="7b8a4-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="7b8a4-226">我們必須從您跨應用程式建立的 .config 檔案中讀取這些值。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="7b8a4-227">若要這樣做，我們會將 .config 檔案新增為我們的應用程式中的必要資源。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="7b8a4-228">然後，我們會設定全域變數，以符合 config.js 文件中的變數。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="7b8a4-229">從命令列將目錄變更至 **azuread** 資料夾 (如果您尚未在此目錄中)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7b8a4-230">在喜愛的編輯器中開啟 `server.js` 檔案，然後新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="7b8a4-231">然後，使用下列程式碼在 `server.js` 中加入新的區段：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="7b8a4-232">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="7b8a4-233">步驟 13：使用 Moongoose 新增 MongoDB 模型和結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="7b8a4-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="7b8a4-234">現在，當我們將這三個檔案組合成 REST API 服務時，您便會開始看到所有準備工作的成效。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="7b8a4-235">在此逐步解說中，我們使用 MongoDB 來儲存工作，如步驟 4 所述。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="7b8a4-236">在步驟 11 中建立的 `config.js` 檔案中，我們會呼叫資料庫 **，因為那是我們放在 `tasklist`mogoose_auth_local** 連線 URL 結尾處的內容。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="7b8a4-237">您不需要在 MongoDB 中事先建立此資料庫。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="7b8a4-238">相反地，MongoDB 會在第一次執行我們的伺服器應用程式時為我們建立此資料庫 (假設此資料庫尚未存在)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="7b8a4-239">既然我們已經告訴伺服器想要使用哪個 MongoDB 資料庫，我們必須撰寫一些額外程式碼，以建立伺服器工作的模型和結構描述。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="7b8a4-240">模型的討論</span><span class="sxs-lookup"><span data-stu-id="7b8a4-240">Discussion of the model</span></span>
<span data-ttu-id="7b8a4-241">我們的結構描述模型很簡單。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-241">Our schema model is simple.</span></span> <span data-ttu-id="7b8a4-242">您可視需要加以擴充。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-242">You expand it as required.</span></span>

<span data-ttu-id="7b8a4-243">名稱：指派給工作的人員名稱。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="7b8a4-244">**字串**。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-244">A **String**.</span></span>

<span data-ttu-id="7b8a4-245">工作：工作本身。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-245">TASK: The task itself.</span></span> <span data-ttu-id="7b8a4-246">**字串**。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-246">A **String**.</span></span>

<span data-ttu-id="7b8a4-247">日期：工作到期的日期。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="7b8a4-248">**DATETIME**。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-248">A **DATETIME**.</span></span>

<span data-ttu-id="7b8a4-249">已完成：工作是否已完成。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="7b8a4-250">**布林值**。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="7b8a4-251">在程式碼中建立結構描述</span><span class="sxs-lookup"><span data-stu-id="7b8a4-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="7b8a4-252">從命令列將目錄變更至 **azuread** 資料夾 (如果您尚未在此目錄中)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7b8a4-253">在喜愛的編輯器中開啟 `server.js` 檔案，然後在組態項目下方新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
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
<span data-ttu-id="7b8a4-254">您可以從程式碼得知，我們先建立我們的結構描述。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="7b8a4-255">然後我們會建立模型物件，以在定義**路由**時用來儲存整個程式碼中的資料。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="7b8a4-256">步驟 14：新增工作 REST API 伺服器的路由</span><span class="sxs-lookup"><span data-stu-id="7b8a4-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="7b8a4-257">既然我們已經擁有可以使用的資料庫模型，讓我們新增即將用於 REST API 伺服器的路由。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="7b8a4-258">關於 Restify 中的路由</span><span class="sxs-lookup"><span data-stu-id="7b8a4-258">About routes in Restify</span></span>
<span data-ttu-id="7b8a4-259">Restify 與 Express 堆疊中的路由運作方式完全相同。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="7b8a4-260">您可以使用您預期用戶端應用程式呼叫的 URI 來定義路由。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="7b8a4-261">通常，您會在個別的檔案中定義您的路由。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="7b8a4-262">基於本文的目的，我們會將路由放在 server.js 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="7b8a4-263">在生產環境中，建議您將這些路由分散到其各自的檔案。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="7b8a4-264">Restify 路由的典型模式如下：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="7b8a4-265">這是最基本層級的模式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="7b8a4-266">Resitfy (及 Express) 可提供更深入的功能，例如定義應用程式類型和提供不同端點之間的複雜路由。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="7b8a4-267">基於本文的目的，我們會讓這些路由保持簡單。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="7b8a4-268">將預設路由加入伺服器</span><span class="sxs-lookup"><span data-stu-id="7b8a4-268">Add default routes to our server</span></span>
<span data-ttu-id="7b8a4-269">我們現在會新增建立、擷取、更新和刪除的基本 CRUD 路由。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="7b8a4-270">從命令列將目錄變更至 **azuread** 資料夾 (如果您尚未在此目錄中)：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="7b8a4-271">在喜愛的編輯器中開啟 `server.js` 檔案，然後在您先前製作的資料庫項目底下新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
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

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="7b8a4-272">在我們的 API 中新增錯誤處理</span><span class="sxs-lookup"><span data-stu-id="7b8a4-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

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


## <a name="step-15-create-your-server"></a><span data-ttu-id="7b8a4-273">步驟 15：建立伺服器</span><span class="sxs-lookup"><span data-stu-id="7b8a4-273">Step 15: Create your server</span></span>
<span data-ttu-id="7b8a4-274">我們已定義資料庫並已備妥路由。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="7b8a4-275">最後一件事是新增伺服器執行個體，以管理我們的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="7b8a4-276">在 Restify (及 Express) 中，您可以為 REST API 伺服器進行多項自訂，但再重申一次，基於本文的目的，我們即將使用最基本的設定。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="7b8a4-277">步驟 16：將路由新增至伺服器 (目前不需驗證)</span><span class="sxs-lookup"><span data-stu-id="7b8a4-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="7b8a4-278">步驟 17：執行伺服器 (在新增 OAuth 支援之前)</span><span class="sxs-lookup"><span data-stu-id="7b8a4-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="7b8a4-279">新增驗證之前，請先測試您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="7b8a4-280">測試伺服器的最簡單方式是在命令列中使用 curl。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="7b8a4-281">在執行此動作之前，我們需要一個可讓我們將輸出剖析為 JSON 的公用程式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="7b8a4-282">安裝下列 JSON 工具 (下列所有範例都會使用此工具)︰</span><span class="sxs-lookup"><span data-stu-id="7b8a4-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="7b8a4-283">這會全域安裝 JSON 工具。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="7b8a4-284">現在已完成此動作，讓我們開始使用伺服器：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="7b8a4-285">首先，確定您的 MongoDB 執行個體正在執行：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="7b8a4-286">然後，變更目錄並啟動 curling：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="7b8a4-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="7b8a4-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. <span data-ttu-id="7b8a4-288">接著，我們可以透過以下方式新增工作：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="7b8a4-289">回應應為：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-289">The response should be:</span></span>

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
    <span data-ttu-id="7b8a4-290">而且我們可以透過以下方式列出 Brandon 的工作：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="7b8a4-291">如果都沒問題，我們便可以開始將 OAuth 新增至 REST API 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="7b8a4-292">您必須將 REST API 伺服器搭配 MongoDB 使用！</span><span class="sxs-lookup"><span data-stu-id="7b8a4-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="7b8a4-293">步驟 18：將驗證新增至 REST API 伺服器</span><span class="sxs-lookup"><span data-stu-id="7b8a4-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="7b8a4-294">既然我們已有執行中的 REST API，我們就可以讓它在 Azure AD 中發揮其價值。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="7b8a4-295">從命令列將目錄變更至 **azuread** 資料夾 (如果您尚未在此目錄中)。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="7b8a4-296">使用 passport-azure-ad 隨附的 OIDCBearerStrategy</span><span class="sxs-lookup"><span data-stu-id="7b8a4-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="7b8a4-297">到目前為止，我們已經建置典型的 REST TODO 伺服器，且其中不含任何授權種類。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="7b8a4-298">這是我們將其結合在一起的起點。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="7b8a4-299">首先，需指出要使用 Passport。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="7b8a4-300">在其他伺服器設定之後緊接著執行此動作：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="7b8a4-301">撰寫 API 時，我們建議您一律將資料連結到使用者無法欺騙之權杖中唯一的項目。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="7b8a4-302">此伺服器儲存 TODO 項目時，會根據我們放在 [擁有者] 欄位的權杖 (透過 token.sub 呼叫) 中使用者的物件識別碼來儲存這些項目。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="7b8a4-303">這可確保只有該使用者可以存取自己的 TODO。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="7b8a4-304">不會在「擁有者」API 中公開，因此，外部使用者可以要求其他人的 TODO，即使它們已經過驗證也一樣。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="7b8a4-305">接下來，使用 `passport-azure-ad` 隨附的持有人策略。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="7b8a4-306">目前查看一下此程式碼，我們很快就會說明其他部分。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="7b8a4-307">將這段程式碼放在您上面所貼內容的後面：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="7b8a4-308">Passport 會使用適用於它的所有策略 (Twitter、Facebook 等) 且所有策略寫入器都依循的類似模式。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="7b8a4-309">查看此策略，您會看見我們將它當成函式來傳遞，其有一個 token 和一個 done 做為參數。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="7b8a4-310">策略完成所有工作之後會回到我們這邊。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="7b8a4-311">當它完成之後，我們會儲存使用者並存放權杖，因此不需要再次要求它。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b8a4-312">先前程式碼會讓所有使用者經歷伺服器的驗證。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="7b8a4-313">這就是所謂的自動註冊。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-313">This is known as auto-registration.</span></span> <span data-ttu-id="7b8a4-314">在生產伺服器中，我們建議您要讓所有人都必須先經歷您所決定的註冊過程。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="7b8a4-315">這通常是您在取用者應用程式中看到的模式，可讓您向 Facebook 註冊，但接著會要求您填寫其他資訊。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="7b8a4-316">如果這不是命令列程式，我們可以從傳回的權杖物件中擷取電子郵件，然後要求使用者填寫其他資訊。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="7b8a4-317">由於這是測試伺服器，因此，我們直接將它們加入記憶體中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="7b8a4-318">保護某些端點</span><span class="sxs-lookup"><span data-stu-id="7b8a4-318">Protect some endpoints</span></span>
<span data-ttu-id="7b8a4-319">透過您想要使用的通訊協定來指定 `passport.authenticate()` 呼叫，即可保護端點。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="7b8a4-320">若要讓我們的伺服器程式碼執行更有趣的作業，請編輯路由。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-320">To make our server code do something more interesting, let’s edit the route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="7b8a4-321">步驟 19：再次執行應用程式伺服器，並確保它會拒絕您的要求</span><span class="sxs-lookup"><span data-stu-id="7b8a4-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="7b8a4-322">讓我們再次使用 `curl`，以查看我們現在是否有針對端點的 OAuth2 保護。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="7b8a4-323">我們會在對此端點執行任何用戶端 SDK 之前，執行此動作。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="7b8a4-324">傳回的標頭應該足以說明我們朝著正確的路徑前進。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="7b8a4-325">首先，確定您的 MongoDB 執行個體正在執行：</span><span class="sxs-lookup"><span data-stu-id="7b8a4-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="7b8a4-326">然後，變更目錄並啟動 curling。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="7b8a4-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="7b8a4-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="7b8a4-328">嘗試基本 POST。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="7b8a4-329">此時 401 是您期待的回應。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="7b8a4-330">此回應指出 Passport 層正嘗試重新導向至已授權的端點，這正是您想要的結果。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b8a4-331">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b8a4-331">Next steps</span></span>
<span data-ttu-id="7b8a4-332">在未使用 OAuth2 相容用戶端的情況下，您已經儘可能地使用此伺服器的所有功能。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="7b8a4-333">您還必須完成其他逐步解說。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="7b8a4-334">您現在已了解如何使用 Restify 和 OAuth2 實作 REST API。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="7b8a4-335">您也已經有足夠的程式碼可以繼續開發服務，並學習如何以此範例為基礎進行建置。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="7b8a4-336">如果您對執行 ADAL 的後續步驟感興趣，以下是一些我們建議的支援 ADAL 用戶端，可供您繼續使用。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="7b8a4-337">複製到您的開發人員機器，並如本逐步解說所述進行設定即可。</span><span class="sxs-lookup"><span data-stu-id="7b8a4-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="7b8a4-338">ADAL for iOS</span><span class="sxs-lookup"><span data-stu-id="7b8a4-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="7b8a4-339">ADAL for Android</span><span class="sxs-lookup"><span data-stu-id="7b8a4-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
