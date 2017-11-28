---
title: "Azure AD B2C：使用 Node.js 保護 Web API 安全 | Microsoft Docs"
description: "如何 toobuild Node.js web 應用程式開發介面可接受來自 B2C 租用戶的權杖"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="f2a38-103">Azure AD B2C：使用 Node.js 保護 Web API 安全</span><span class="sxs-lookup"><span data-stu-id="f2a38-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="f2a38-104">透過 Azure Active Directory (Azure AD) B2C，您可以使用 OAuth 2.0 存取權杖來保護 Web API。</span><span class="sxs-lookup"><span data-stu-id="f2a38-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="f2a38-105">這些語彙基元可讓您使用 Azure AD B2C tooauthenticate toohello API 的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="f2a38-106">本文章將示範如何 toocreate 「 待辦事項清單 」 的應用程式開發介面可讓使用者在 tooadd 和清單的工作。</span><span class="sxs-lookup"><span data-stu-id="f2a38-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="f2a38-107">hello web API 使用 Azure AD B2C 保護，並且只允許已驗證的使用者 toomanage 其待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="f2a38-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="f2a38-108">此範例寫入 toobe 連接 tooby 使用我們[iOS B2C 範例應用程式](active-directory-b2c-devquickstarts-ios.md)。</span><span class="sxs-lookup"><span data-stu-id="f2a38-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="f2a38-109">首先，hello 目前逐步解說作業，並再依照該範例。</span><span class="sxs-lookup"><span data-stu-id="f2a38-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="f2a38-110">**Passport** 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="f2a38-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="f2a38-111">您可以暗中將具有彈性且模組化的 Passport 安裝在任何 Express 或 Resitify Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f2a38-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="f2a38-112">有一套完整的策略支援以使用者名稱和密碼、Facebook、Twitter 等來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="f2a38-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="f2a38-113">我們已為 Azure Active Directory (Azure AD) 開發一套策略。</span><span class="sxs-lookup"><span data-stu-id="f2a38-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f2a38-114">您安裝此模組，然後再新增 hello Azure AD`passport-azure-ad`外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="f2a38-115">toodo 此範例中，您需要：</span><span class="sxs-lookup"><span data-stu-id="f2a38-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="f2a38-116">向 Azure AD 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="f2a38-117">設定您的應用程式 toouse Passport 的`azure-ad-passport`外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="f2a38-118">設定用戶端應用程式 toocall hello 「 待辦事項清單 」 web API。</span><span class="sxs-lookup"><span data-stu-id="f2a38-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="f2a38-119">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="f2a38-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="f2a38-120">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="f2a38-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="f2a38-121">目錄就是所有使用者、應用程式、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="f2a38-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="f2a38-122">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) 再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="f2a38-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="f2a38-123">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="f2a38-123">Create an application</span></span>
<span data-ttu-id="f2a38-124">接下來，您需要的 toocreate B2C 目錄，它需要 toosecurely 部分資訊可讓 Azure AD 中的應用程式進行通訊與您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="f2a38-125">在此情況下，hello 用戶端應用程式和 web API 由單一**應用程式識別碼**，因為它們組成一個邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="f2a38-126">toocreate 的應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="f2a38-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="f2a38-127">請務必：</span><span class="sxs-lookup"><span data-stu-id="f2a38-127">Be sure to:</span></span>

* <span data-ttu-id="f2a38-128">包含**web 應用程式/web api** hello 應用程式中</span><span class="sxs-lookup"><span data-stu-id="f2a38-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="f2a38-129">在 [回覆 URL] 中輸入 `http://localhost/TodoListService`。</span><span class="sxs-lookup"><span data-stu-id="f2a38-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="f2a38-130">它是 hello 預設 URL，此程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="f2a38-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="f2a38-131">為您的應用程式建立 [應用程式密碼]  ，然後複製該密碼。</span><span class="sxs-lookup"><span data-stu-id="f2a38-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="f2a38-132">您稍後需要此資料。</span><span class="sxs-lookup"><span data-stu-id="f2a38-132">You need this data later.</span></span> <span data-ttu-id="f2a38-133">請注意，這個值需要 toobe [XML 逸出](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape)然後才能使用它。</span><span class="sxs-lookup"><span data-stu-id="f2a38-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="f2a38-134">複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="f2a38-135">您稍後需要此資料。</span><span class="sxs-lookup"><span data-stu-id="f2a38-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="f2a38-136">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="f2a38-136">Create your policies</span></span>
<span data-ttu-id="f2a38-137">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="f2a38-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="f2a38-138">此應用程式包含兩種身分識別體驗：註冊和登入。</span><span class="sxs-lookup"><span data-stu-id="f2a38-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="f2a38-139">您需要的每個類型，toocreate 一個原則中所述[原則參考文件](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)。</span><span class="sxs-lookup"><span data-stu-id="f2a38-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="f2a38-140">建立您的三個原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="f2a38-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="f2a38-141">選擇 hello**顯示名稱**與其他註冊的屬性，在您註冊的原則。</span><span class="sxs-lookup"><span data-stu-id="f2a38-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="f2a38-142">選擇 hello**顯示名稱**和**物件識別碼**中每個原則的應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="f2a38-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="f2a38-143">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="f2a38-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="f2a38-144">複製下 hello**名稱**的每個原則建立之後。</span><span class="sxs-lookup"><span data-stu-id="f2a38-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="f2a38-145">就不應有 hello 前置詞`b2c_1_`。</span><span class="sxs-lookup"><span data-stu-id="f2a38-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="f2a38-146">您稍後需要這些原則名稱。</span><span class="sxs-lookup"><span data-stu-id="f2a38-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="f2a38-147">您已建立您的三個原則之後，您便準備好 toobuild 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="f2a38-148">toolearn 有關原則的運作方式在 Azure AD B2C，啟動以 hello [.NET web 應用程式快速入門教學課程](active-directory-b2c-devquickstarts-web-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="f2a38-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="f2a38-149">下載 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="f2a38-149">Download hello code</span></span>
<span data-ttu-id="f2a38-150">hello 本教學課程中的程式碼[維護 GitHub 上](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS)。</span><span class="sxs-lookup"><span data-stu-id="f2a38-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="f2a38-151">移 toobuild hello 範例時，您可以[下載為.zip 檔案的基本架構專案](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip)。</span><span class="sxs-lookup"><span data-stu-id="f2a38-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="f2a38-152">您也可以複製 hello 基本架構：</span><span class="sxs-lookup"><span data-stu-id="f2a38-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="f2a38-153">hello 完成應用程式也是[可以做為.zip 檔案](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip)或 hello `complete` hello 分支相同的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="f2a38-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="f2a38-154">下載適用於您平台的 Node.js</span><span class="sxs-lookup"><span data-stu-id="f2a38-154">Download Node.js for your platform</span></span>
<span data-ttu-id="f2a38-155">toosuccessfully 使用這個範例中，您需要使用中的安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="f2a38-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="f2a38-156">從 [nodejs.org](http://nodejs.org)安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="f2a38-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="f2a38-157">安裝適用於您平台的 MongoDB</span><span class="sxs-lookup"><span data-stu-id="f2a38-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="f2a38-158">toosuccessfully 使用這個範例，您需要使用中的 MongoDB 的安裝。</span><span class="sxs-lookup"><span data-stu-id="f2a38-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="f2a38-159">我們使用 MongoDB toomake 您持續性的 REST API 在伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="f2a38-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="f2a38-160">從 [mongodb.org](http://www.mongodb.org)安裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="f2a38-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="f2a38-161">本逐步解說假設您使用 MongoDB，這在撰寫本文 hello 階段是 hello 預設安裝和伺服器端點`mongodb://localhost`。</span><span class="sxs-lookup"><span data-stu-id="f2a38-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="f2a38-162">安裝在您的 web 應用程式開發介面中的 hello Restify 模組</span><span class="sxs-lookup"><span data-stu-id="f2a38-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="f2a38-163">我們使用 Restify toobuild REST API。</span><span class="sxs-lookup"><span data-stu-id="f2a38-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="f2a38-164">Restify 是衍生自 Express 的最小且具彈性的 Node.js 應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="f2a38-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="f2a38-165">它有一組強大的功能，可在 Connect 之上建置 REST API。</span><span class="sxs-lookup"><span data-stu-id="f2a38-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="f2a38-166">安裝 Restify</span><span class="sxs-lookup"><span data-stu-id="f2a38-166">Install Restify</span></span>
<span data-ttu-id="f2a38-167">從 hello 命令列，將目錄變更為太`azuread`。</span><span class="sxs-lookup"><span data-stu-id="f2a38-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="f2a38-168">如果 hello`azuread`目錄不存在，請建立它。</span><span class="sxs-lookup"><span data-stu-id="f2a38-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="f2a38-169">`cd azuread` 或 `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="f2a38-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="f2a38-170">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2a38-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="f2a38-171">此命令會安裝 Restify。</span><span class="sxs-lookup"><span data-stu-id="f2a38-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="f2a38-172">您有收到錯誤訊息嗎？</span><span class="sxs-lookup"><span data-stu-id="f2a38-172">Did you get an error?</span></span>
<span data-ttu-id="f2a38-173">某些作業系統中，當您使用`npm`，您可能會收到 hello 錯誤`Error: EPERM, chmod '/usr/local/bin/..'`和系統管理員身分執行 hello 帳戶的要求。</span><span class="sxs-lookup"><span data-stu-id="f2a38-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="f2a38-174">如果發生這個問題，請使用 hello`sudo`命令 toorun`npm`較高的權限層級。</span><span class="sxs-lookup"><span data-stu-id="f2a38-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="f2a38-175">有發生 DTrace 錯誤嗎？</span><span class="sxs-lookup"><span data-stu-id="f2a38-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="f2a38-176">安裝 Restify 時，您可能會看到類似下面的文字：</span><span class="sxs-lookup"><span data-stu-id="f2a38-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="f2a38-177">Restify 提供強大機制來使用 DTrace 追蹤 REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f2a38-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="f2a38-178">不過，許多作業系統沒有 DTrace 可以使用。</span><span class="sxs-lookup"><span data-stu-id="f2a38-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="f2a38-179">您可以放心地忽略這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="f2a38-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="f2a38-180">hello hello 命令輸出應該會出現類似 toothis 文字：</span><span class="sxs-lookup"><span data-stu-id="f2a38-180">hello output of hello command should appear similar toothis text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="f2a38-181">在您的 Web API 中安裝 Passport</span><span class="sxs-lookup"><span data-stu-id="f2a38-181">Install Passport in your web API</span></span>
<span data-ttu-id="f2a38-182">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在。</span><span class="sxs-lookup"><span data-stu-id="f2a38-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="f2a38-183">安裝 Passport 使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2a38-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="f2a38-184">hello hello 命令輸出應該類似 toothis 文字：</span><span class="sxs-lookup"><span data-stu-id="f2a38-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="f2a38-185">將 passport azure ad tooyour web API</span><span class="sxs-lookup"><span data-stu-id="f2a38-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="f2a38-186">接下來，使用新增 hello OAuth 策略`passport-azuread`，一套連接 Azure AD 與 Passport 的策略。</span><span class="sxs-lookup"><span data-stu-id="f2a38-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="f2a38-187">使用這個策略在 hello REST API 範例的承載權杖。</span><span class="sxs-lookup"><span data-stu-id="f2a38-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="f2a38-188">雖然 OAuth2 提供可發行任何已知權杖類型的架構，但只會普遍使用特定的權杖類型。</span><span class="sxs-lookup"><span data-stu-id="f2a38-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="f2a38-189">保護端點 hello 權杖是持有人權杖。</span><span class="sxs-lookup"><span data-stu-id="f2a38-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="f2a38-190">這些類型的語彙基元是最廣泛發出的 OAuth2 hello。</span><span class="sxs-lookup"><span data-stu-id="f2a38-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="f2a38-191">許多實作假設持有者權杖是 hello 的發行權杖的唯一類型。</span><span class="sxs-lookup"><span data-stu-id="f2a38-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="f2a38-192">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在。</span><span class="sxs-lookup"><span data-stu-id="f2a38-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="f2a38-193">安裝 hello Passport`passport-azure-ad`模組使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="f2a38-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="f2a38-194">hello hello 命令輸出應該類似 toothis 文字：</span><span class="sxs-lookup"><span data-stu-id="f2a38-194">hello output of hello command should be similar toothis text:</span></span>

``
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
``

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="f2a38-195">新增 MongoDB 模組 tooyour web API</span><span class="sxs-lookup"><span data-stu-id="f2a38-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="f2a38-196">此範例會使用 MongoDB 作為資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f2a38-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="f2a38-197">為此安裝 Mongoose，這是廣泛用於管理模型和結構描述的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="f2a38-198">安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="f2a38-198">Install additional modules</span></span>
<span data-ttu-id="f2a38-199">接下來，安裝 hello 剩餘所需的模組。</span><span class="sxs-lookup"><span data-stu-id="f2a38-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="f2a38-200">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在：</span><span class="sxs-lookup"><span data-stu-id="f2a38-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="f2a38-201">安裝中的 hello 模組您`node_modules`目錄：</span><span class="sxs-lookup"><span data-stu-id="f2a38-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="f2a38-202">使用您的相依性建立 server.js 檔案</span><span class="sxs-lookup"><span data-stu-id="f2a38-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="f2a38-203">hello`server.js`檔案 hello 大部分的 hello 功能提供您的 Web API 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f2a38-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="f2a38-204">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在：</span><span class="sxs-lookup"><span data-stu-id="f2a38-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="f2a38-205">在編輯器中建立 `server.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2a38-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="f2a38-206">新增 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="f2a38-206">Add hello following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="f2a38-207">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2a38-207">Save hello file.</span></span> <span data-ttu-id="f2a38-208">您要稍後再回來 tooit。</span><span class="sxs-lookup"><span data-stu-id="f2a38-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="f2a38-209">建立您的 Azure AD 設定 config.js 檔案 toostore</span><span class="sxs-lookup"><span data-stu-id="f2a38-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="f2a38-210">這個程式碼檔從您的 Azure AD 入口網站 toohello 傳遞 hello 組態參數`Passport.js`檔案。</span><span class="sxs-lookup"><span data-stu-id="f2a38-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="f2a38-211">當您新增 hello 的 hello 逐步解說的第一個部分中的 hello web API toohello 入口網站時，您會建立這些組態值。</span><span class="sxs-lookup"><span data-stu-id="f2a38-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="f2a38-212">在複製 hello 程式碼之後，我們會說明哪些 tooput hello 這些參數值。</span><span class="sxs-lookup"><span data-stu-id="f2a38-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="f2a38-213">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在：</span><span class="sxs-lookup"><span data-stu-id="f2a38-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="f2a38-214">在編輯器中建立 `config.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="f2a38-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="f2a38-215">新增 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="f2a38-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="f2a38-216">必要值</span><span class="sxs-lookup"><span data-stu-id="f2a38-216">Required values</span></span>
<span data-ttu-id="f2a38-217">`clientID`: hello 的 Web API 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="f2a38-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="f2a38-218">`IdentityMetadata`： 這是 where`passport-azure-ad`尋找 hello 身分識別提供者將組態資料。</span><span class="sxs-lookup"><span data-stu-id="f2a38-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="f2a38-219">它也會尋找 hello 金鑰 toovalidate hello JSON web 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="f2a38-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="f2a38-220">`audience`: hello 從識別您的應用程式的 hello 入口網站的統一資源識別元 (URI)。</span><span class="sxs-lookup"><span data-stu-id="f2a38-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="f2a38-221">`tenantName`：您的租用戶名稱 (例如 **contoso.onmicrosoft.com**)。</span><span class="sxs-lookup"><span data-stu-id="f2a38-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="f2a38-222">`policyName`: hello 想 toovalidate hello 權杖 tooyour server 中的原則。</span><span class="sxs-lookup"><span data-stu-id="f2a38-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="f2a38-223">此原則應該 hello 登入上 hello 用戶端應用程式所使用的相同原則。</span><span class="sxs-lookup"><span data-stu-id="f2a38-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="f2a38-224">現在，使用 hello 相同跨用戶端和伺服器的安裝程式的原則。</span><span class="sxs-lookup"><span data-stu-id="f2a38-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="f2a38-225">如果您已經完成逐步解說，並且建立這些原則，您不需要 toodo 因此一次。</span><span class="sxs-lookup"><span data-stu-id="f2a38-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="f2a38-226">由於您完成 hello 逐步解說，您不應該 hello 站台上的用戶端逐步解說需要 tooset 註冊新的原則。</span><span class="sxs-lookup"><span data-stu-id="f2a38-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="f2a38-227">加入組態 tooyour 立即轉譯 server.js 檔</span><span class="sxs-lookup"><span data-stu-id="f2a38-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="f2a38-228">從 hello tooread hello 值`config.js`檔案所建立，請新增 hello`.config`檔案做為應用程式中所需的資源，並在 hello 將 hello 全域變數 toothose`config.js`文件。</span><span class="sxs-lookup"><span data-stu-id="f2a38-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="f2a38-229">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在：</span><span class="sxs-lookup"><span data-stu-id="f2a38-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="f2a38-230">開啟 hello`server.js`在編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f2a38-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="f2a38-231">新增 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="f2a38-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="f2a38-232">加入新的區段太`server.js`，其中包含下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2a38-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="f2a38-233">接下來，讓我們加入一些預留位置的 hello 我們收到來自我們呼叫的應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="f2a38-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="f2a38-234">不用猶豫，讓我們同時建立記錄器。</span><span class="sxs-lookup"><span data-stu-id="f2a38-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="f2a38-235">使用 1 將 hello MongoDB 模型和結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="f2a38-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="f2a38-236">hello 早準備卓著，同時整合在一起的 REST API 服務這三個檔案。</span><span class="sxs-lookup"><span data-stu-id="f2a38-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="f2a38-237">本逐步解說中，使用 MongoDB toostore 您的工作，如同先前討論一般。</span><span class="sxs-lookup"><span data-stu-id="f2a38-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="f2a38-238">在 hello`config.js`呼叫您的資料庫檔案， **tasklist**。</span><span class="sxs-lookup"><span data-stu-id="f2a38-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="f2a38-239">該名稱也是您放置在 hello 結尾 hello`mongoose_auth_local`連接 URL。</span><span class="sxs-lookup"><span data-stu-id="f2a38-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="f2a38-240">您不需要 toocreate MongoDB 事先的這個資料庫。</span><span class="sxs-lookup"><span data-stu-id="f2a38-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="f2a38-241">它會為您建立 hello 資料庫 hello 第一次執行應用程式伺服器上。</span><span class="sxs-lookup"><span data-stu-id="f2a38-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="f2a38-242">哪些 MongoDB 資料庫 toouse 告訴 hello 伺服器之後，您需要 toowrite 一些額外的程式碼 toocreate hello 模型和結構描述為您伺服器的工作。</span><span class="sxs-lookup"><span data-stu-id="f2a38-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="f2a38-243">展開 hello 模型</span><span class="sxs-lookup"><span data-stu-id="f2a38-243">Expand hello model</span></span>
<span data-ttu-id="f2a38-244">此結構描述模型很簡單。</span><span class="sxs-lookup"><span data-stu-id="f2a38-244">This schema model is simple.</span></span> <span data-ttu-id="f2a38-245">您可以視需要來擴充它。</span><span class="sxs-lookup"><span data-stu-id="f2a38-245">You can expand it as required.</span></span>

<span data-ttu-id="f2a38-246">`owner`： 指派使用者，方法是 toohello 工作。</span><span class="sxs-lookup"><span data-stu-id="f2a38-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="f2a38-247">此物件是 **字串**。</span><span class="sxs-lookup"><span data-stu-id="f2a38-247">This object is a **string**.</span></span>  

<span data-ttu-id="f2a38-248">`Text`: hello 工作本身。</span><span class="sxs-lookup"><span data-stu-id="f2a38-248">`Text`: hello task itself.</span></span> <span data-ttu-id="f2a38-249">此物件是 **字串**。</span><span class="sxs-lookup"><span data-stu-id="f2a38-249">This object is a **string**.</span></span>

<span data-ttu-id="f2a38-250">`date`: hello 日期該 hello 工作會到期。</span><span class="sxs-lookup"><span data-stu-id="f2a38-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="f2a38-251">此物件是 **日期時間**。</span><span class="sxs-lookup"><span data-stu-id="f2a38-251">This object is a **datetime**.</span></span>

<span data-ttu-id="f2a38-252">`completed`： 如果 hello 工作已完成。</span><span class="sxs-lookup"><span data-stu-id="f2a38-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="f2a38-253">此物件是 **布林值**。</span><span class="sxs-lookup"><span data-stu-id="f2a38-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="f2a38-254">建立 hello 程式碼中的 hello 結構描述</span><span class="sxs-lookup"><span data-stu-id="f2a38-254">Create hello schema in hello code</span></span>
<span data-ttu-id="f2a38-255">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在：</span><span class="sxs-lookup"><span data-stu-id="f2a38-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="f2a38-256">開啟 hello`server.js`在編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f2a38-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="f2a38-257">新增下列資訊 hello 組態項目下方的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2a38-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="f2a38-258">您第一次建立 hello 結構描述，然後建立使用的 toostore hello 整個資料程式碼，當您定義的模型物件您**路由**。</span><span class="sxs-lookup"><span data-stu-id="f2a38-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="f2a38-259">新增 REST API 工作伺服器的路由</span><span class="sxs-lookup"><span data-stu-id="f2a38-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="f2a38-260">現在您有與資料庫模型 toowork，新增用於 REST API 伺服器 hello 路由。</span><span class="sxs-lookup"><span data-stu-id="f2a38-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="f2a38-261">關於 Restify 中的路由</span><span class="sxs-lookup"><span data-stu-id="f2a38-261">About routes in Restify</span></span>
<span data-ttu-id="f2a38-262">路由在 Restify hello 中一樣使用 hello Express 堆疊時，其運作的方式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="f2a38-263">您可以使用 hello 您預期 hello 用戶端應用程式 toocall 的 URI，以定義路由。</span><span class="sxs-lookup"><span data-stu-id="f2a38-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="f2a38-264">Restify 路由的典型模式是：</span><span class="sxs-lookup"><span data-stu-id="f2a38-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="f2a38-265">Resitfy 及 Express 可提供更深入的功能，例如定義應用程式類型和執行不同端點之間的複雜路由。</span><span class="sxs-lookup"><span data-stu-id="f2a38-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="f2a38-266">基於 hello 本教學課程中，我們簡化這些路由。</span><span class="sxs-lookup"><span data-stu-id="f2a38-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="f2a38-267">新增預設路由 tooyour 伺服器</span><span class="sxs-lookup"><span data-stu-id="f2a38-267">Add default routes tooyour server</span></span>
<span data-ttu-id="f2a38-268">您現在將加入的 hello 基本 CRUD 路由**建立**和**清單**我們 REST api。</span><span class="sxs-lookup"><span data-stu-id="f2a38-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="f2a38-269">可以找到其他路由，在 hello `complete` hello 範例的分支。</span><span class="sxs-lookup"><span data-stu-id="f2a38-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="f2a38-270">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在：</span><span class="sxs-lookup"><span data-stu-id="f2a38-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="f2a38-271">開啟 hello`server.js`在編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f2a38-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="f2a38-272">Hello 資料庫項目下方由上方新增下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2a38-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="f2a38-273">加入 hello 路由的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="f2a38-273">Add error handling for hello routes</span></span>
<span data-ttu-id="f2a38-274">讓您能夠通訊會遇到可以了解的方式回復 toohello 用戶端的任何問題，請加入一些錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="f2a38-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="f2a38-275">加入下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2a38-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="f2a38-276">建立伺服器</span><span class="sxs-lookup"><span data-stu-id="f2a38-276">Create your server</span></span>
<span data-ttu-id="f2a38-277">您現在已定義資料庫並備妥路由。</span><span class="sxs-lookup"><span data-stu-id="f2a38-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="f2a38-278">針對您 toodo hello 最後是 tooadd hello 伺服器執行個體管理您的呼叫。</span><span class="sxs-lookup"><span data-stu-id="f2a38-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="f2a38-279">Restify 和 Express 提供深層的自訂功能的 REST API 伺服器，但我們在此使用 hello 最基本的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="f2a38-280">新增 hello 路由 toohello 伺服器 （不含驗證）</span><span class="sxs-lookup"><span data-stu-id="f2a38-280">Add hello routes toohello server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="f2a38-281">新增驗證 tooyour REST API 伺服器</span><span class="sxs-lookup"><span data-stu-id="f2a38-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="f2a38-282">既然您已經有執行中的 REST API 伺服器，您可以讓它在 Azure AD 中發揮價值。</span><span class="sxs-lookup"><span data-stu-id="f2a38-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="f2a38-283">從 hello 命令列，將目錄變更為太`azuread`，如果它已經不存在：</span><span class="sxs-lookup"><span data-stu-id="f2a38-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="f2a38-284">使用 hello OIDCBearerStrategy 所包含的 passport azure ad</span><span class="sxs-lookup"><span data-stu-id="f2a38-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="f2a38-285">當您撰寫應用程式開發介面，您應該一律連結 hello 資料 toosomething 與 hello 使用者的 hello 語彙基元無法偽造。</span><span class="sxs-lookup"><span data-stu-id="f2a38-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="f2a38-286">當 hello 伺服器儲存 ToDo 項目時，它會因此根據 hello **oid**的 hello 使用者在 hello 權杖中 （透過 token.oid 呼叫），則是放在 hello 「 擁有者 」 欄位。</span><span class="sxs-lookup"><span data-stu-id="f2a38-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="f2a38-287">此值可確保只有該使用者可以存取自己的 ToDo 項目。</span><span class="sxs-lookup"><span data-stu-id="f2a38-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="f2a38-288">讓外部使用者可以要求其他人的 ToDo 項目，即使它們驗證 hello 應用程式開發介面的 「 擁有者 」 中沒有任何風險。</span><span class="sxs-lookup"><span data-stu-id="f2a38-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="f2a38-289">接下來，使用隨附的 hello 承載策略`passport-azure-ad`。</span><span class="sxs-lookup"><span data-stu-id="f2a38-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="f2a38-290">Passport 會使用其所有的策略 hello 相同模式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="f2a38-291">您需要傳遞以 `token` 和 `done` 為參數的 `function()` 給它。</span><span class="sxs-lookup"><span data-stu-id="f2a38-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="f2a38-292">hello 策略恢復 tooyou 它所有的工作完成後。</span><span class="sxs-lookup"><span data-stu-id="f2a38-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="f2a38-293">您應該儲存 hello 使用者，然後儲存 hello 語彙基元，讓您不需要為其 tooask 一次。</span><span class="sxs-lookup"><span data-stu-id="f2a38-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2a38-294">hello 上述的程式碼會採用任何發生 tooauthenticate tooyour 伺服器的使用者。</span><span class="sxs-lookup"><span data-stu-id="f2a38-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="f2a38-295">此程序稱為自動註冊。</span><span class="sxs-lookup"><span data-stu-id="f2a38-295">This process is known as autoregistration.</span></span> <span data-ttu-id="f2a38-296">在實際執行伺服器，不要讓任何使用者存取 hello API 中而不需要先加以完成註冊程序。</span><span class="sxs-lookup"><span data-stu-id="f2a38-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="f2a38-297">此程序通常是您在允許使用 Facebook 的 tooregister 但然後要求 toofill 外的其他資訊的取用者應用程式中看到的 hello 模式。</span><span class="sxs-lookup"><span data-stu-id="f2a38-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="f2a38-298">如果此程式無法命令列程式，我們無法從傳回並再要求其他資訊的使用者 toofill hello 權杖物件擷取已 hello 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f2a38-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="f2a38-299">因為這是範例，我們將其加入 tooan 記憶體中資料庫。</span><span class="sxs-lookup"><span data-stu-id="f2a38-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="f2a38-300">執行您的伺服器應用程式 tooverify，就會拒絕您</span><span class="sxs-lookup"><span data-stu-id="f2a38-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="f2a38-301">您可以使用`curl`toosee，如果您現在有 OAuth2 保護對您的端點。</span><span class="sxs-lookup"><span data-stu-id="f2a38-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="f2a38-302">hello 傳回標頭應為足夠 tootell 您要在 hello 正確的路徑。</span><span class="sxs-lookup"><span data-stu-id="f2a38-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="f2a38-303">請確定您的 MongoDB 執行個體正在執行：</span><span class="sxs-lookup"><span data-stu-id="f2a38-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="f2a38-304">變更 toohello 目錄和執行的 hello 伺服器：</span><span class="sxs-lookup"><span data-stu-id="f2a38-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="f2a38-305">在新的終端機視窗中，執行 `curl`</span><span class="sxs-lookup"><span data-stu-id="f2a38-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="f2a38-306">嘗試基本的 POST 方法：</span><span class="sxs-lookup"><span data-stu-id="f2a38-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="f2a38-307">401 錯誤是您想要的 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="f2a38-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="f2a38-308">它會指出 hello Passport 該層正嘗試 tooredirect toohello 授權端點。</span><span class="sxs-lookup"><span data-stu-id="f2a38-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="f2a38-309">您現在擁有一項使用 OAuth2 的 REST API 服務</span><span class="sxs-lookup"><span data-stu-id="f2a38-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="f2a38-310">您已使用 Restify 和 OAuth 實作 REST API！</span><span class="sxs-lookup"><span data-stu-id="f2a38-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="f2a38-311">現在您有足夠的程式碼，讓您可以繼續 toodevelop 服務和此範例上建置。</span><span class="sxs-lookup"><span data-stu-id="f2a38-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="f2a38-312">在未使用 OAuth2 相容用戶端的情況下，您已經儘可能地使用此伺服器的所有功能。</span><span class="sxs-lookup"><span data-stu-id="f2a38-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="f2a38-313">進行的下一個步驟中，使用類似其他逐步解說我們[連接 tooa web 應用程式開發介面透過 iOS 與 B2C](active-directory-b2c-devquickstarts-ios.md)逐步解說。</span><span class="sxs-lookup"><span data-stu-id="f2a38-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2a38-314">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2a38-314">Next steps</span></span>
<span data-ttu-id="f2a38-315">您現在可以移動 toomore 進階主題，例如：</span><span class="sxs-lookup"><span data-stu-id="f2a38-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="f2a38-316">使用 iOS B2C 與連線 tooa web API</span><span class="sxs-lookup"><span data-stu-id="f2a38-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
