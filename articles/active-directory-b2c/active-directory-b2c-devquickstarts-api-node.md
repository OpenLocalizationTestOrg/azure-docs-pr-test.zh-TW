---
title: "Azure AD B2C：使用 Node.js 保護 Web API 安全 | Microsoft Docs"
description: "如何建置可接受來自 B2C 租用戶之權杖的 Node.js Web API"
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
ms.openlocfilehash: 6480be75c314ede1b786e959a79c0385dd2edea8
ms.sourcegitcommit: 73f159cdbc122ffe42f3e1f7a3de05f77b6a4725
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="8ed1b-103">Azure AD B2C：使用 Node.js 保護 Web API 安全</span><span class="sxs-lookup"><span data-stu-id="8ed1b-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="8ed1b-104">透過 Azure Active Directory (Azure AD) B2C，您可以使用 OAuth 2.0 存取權杖來保護 Web API。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="8ed1b-105">這些權杖可讓您的用戶端 app 使用 Azure AD B2C 來對 API 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-105">These tokens allow your client apps that use Azure AD B2C to authenticate to the API.</span></span> <span data-ttu-id="8ed1b-106">本文說明如何建立「待辦事項清單」API，以便使用者新增和列出工作。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-106">This article shows you how to create a "to-do list" API that allows users to add and list tasks.</span></span> <span data-ttu-id="8ed1b-107">Web API 會使用 Azure AD B2C 進行保護，只允許已驗證的使用者管理他們的待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed1b-108">此範例設計為使用我們的 [iOS B2C 範例應用程式](active-directory-b2c-devquickstarts-ios.md)來連接。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-108">This sample was written to be connected to by using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="8ed1b-109">請先執行目前的逐步解說，然後遵循該範例操作。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-109">Do the current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="8ed1b-110">**Passport** 是 Node.js 的驗證中介軟體。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="8ed1b-111">您可以暗中將具有彈性且模組化的 Passport 安裝在任何 Express 或 Resitify Web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="8ed1b-112">有一套完整的策略支援以使用者名稱和密碼、Facebook、Twitter 等來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="8ed1b-113">我們已為 Azure Active Directory (Azure AD) 開發一套策略。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8ed1b-114">您會安裝此模組，然後新增 Azure AD `passport-azure-ad` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-114">You install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="8ed1b-115">若要執行此範例，您需要：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-115">To do this sample, you need to:</span></span>

1. <span data-ttu-id="8ed1b-116">向 Azure AD 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="8ed1b-117">設定您的應用程式來使用 Passport 的 `azure-ad-passport` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-117">Set up your application to use Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="8ed1b-118">設定用戶端應用程式呼叫「待辦事項清單」Web API。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-118">Configure a client application to call the "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="8ed1b-119">取得 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="8ed1b-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="8ed1b-120">您必須先建立目錄或租用戶，才可使用 Azure AD B2C。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="8ed1b-121">目錄就是所有使用者、應用程式、群組等項目的容器。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="8ed1b-122">如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) 再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="8ed1b-123">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="8ed1b-123">Create an application</span></span>
<span data-ttu-id="8ed1b-124">接下來，您需要在 B2C 目錄中建立應用程式，以提供一些必要資訊給 Azure AD，讓它與應用程式安全地通訊。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-124">Next, you need to create an app in your B2C directory that gives Azure AD some information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="8ed1b-125">在此案例中，因為用戶端應用程式和 Web API 會組成一個邏輯應用程式，所以由單一 **應用程式識別碼**表示。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-125">In this case, both the client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="8ed1b-126">如果要建立應用程式，請遵循 [這些指示](active-directory-b2c-app-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="8ed1b-127">請務必：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-127">Be sure to:</span></span>

* <span data-ttu-id="8ed1b-128">在應用程式中加入 **Web 應用程式/Web API**</span><span class="sxs-lookup"><span data-stu-id="8ed1b-128">Include a **web app/web api** in the application</span></span>
* <span data-ttu-id="8ed1b-129">在 [回覆 URL] 中輸入 `http://localhost/TodoListService`。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="8ed1b-130">這是此程式碼範例的預設 URL。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-130">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="8ed1b-131">為您的應用程式建立 **應用程式密碼** ，並複製起來。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="8ed1b-132">您稍後需要此資料。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-132">You need this data later.</span></span> <span data-ttu-id="8ed1b-133">請注意，這個值在使用之前必須經過 [XML 逸出](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) 。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="8ed1b-134">複製指派給您的應用程式的 **應用程式識別碼** 。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="8ed1b-135">您稍後需要此資料。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="8ed1b-136">建立您的原則</span><span class="sxs-lookup"><span data-stu-id="8ed1b-136">Create your policies</span></span>
<span data-ttu-id="8ed1b-137">在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="8ed1b-138">此應用程式包含兩種身分識別體驗：註冊和登入。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="8ed1b-139">您必須為每個類型建立一個原則，如 [原則參考文章](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)所述。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-139">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="8ed1b-140">建立您的三個原則時，請務必：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="8ed1b-141">在註冊原則中，選擇 [顯示名稱]  和其他註冊屬性。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="8ed1b-142">在每個原則中，選擇 [顯示名稱] 和 [物件識別碼] 應用程式宣告。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="8ed1b-143">您也可以選擇其他宣告。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="8ed1b-144">建立每個原則後，請複製原則的 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-144">Copy down the **Name** of each policy after you create it.</span></span> <span data-ttu-id="8ed1b-145">其前置詞應該為 `b2c_1_`。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="8ed1b-146">您稍後需要這些原則名稱。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="8ed1b-147">建立您的三個原則後，就可以開始建置您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-147">After you have created your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="8ed1b-148">如需了解 Azure AD B2C 中原則的運作方式，請從 [.NET Web 應用程式快速入門教學課程](active-directory-b2c-devquickstarts-web-dotnet.md)開始。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-148">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-the-code"></a><span data-ttu-id="8ed1b-149">下載程式碼</span><span class="sxs-lookup"><span data-stu-id="8ed1b-149">Download the code</span></span>
<span data-ttu-id="8ed1b-150">本教學課程的程式碼保留在 [GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS)。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-150">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="8ed1b-151">如要依照指示建置範例，請 [下載 .zip 檔案格式的基本架構專案](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip)。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-151">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="8ed1b-152">您也可以複製基本架構：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-152">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="8ed1b-153">完整的 App 也[提供 .zip 檔案格式](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip)，或放在相同儲存機制的 `complete` 分支中。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-153">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="8ed1b-154">下載適用於您平台的 Node.js</span><span class="sxs-lookup"><span data-stu-id="8ed1b-154">Download Node.js for your platform</span></span>
<span data-ttu-id="8ed1b-155">若要成功使用此範例，您需要已成功安裝的 Node.js。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-155">To successfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="8ed1b-156">從 [nodejs.org](http://nodejs.org)安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="8ed1b-157">安裝適用於您平台的 MongoDB</span><span class="sxs-lookup"><span data-stu-id="8ed1b-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="8ed1b-158">若要成功使用此範例，您需要已成功安裝的 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-158">To successfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="8ed1b-159">您會使用 MongoDB，讓 REST API 得以在不同伺服器執行個體之間持續使用。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-159">We use MongoDB to make your REST API persistent across server instances.</span></span>

<span data-ttu-id="8ed1b-160">從 [mongodb.org](http://www.mongodb.org)安裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="8ed1b-161">本逐步解說假設您會使用 MongoDB 的預設安裝和伺服器端點，在撰寫本文時為 `mongodb://localhost`。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-161">This walk-through assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="8ed1b-162">在您的 Web API 中安裝 Restify 模組</span><span class="sxs-lookup"><span data-stu-id="8ed1b-162">Install the Restify modules in your web API</span></span>
<span data-ttu-id="8ed1b-163">您會使用 Restify 來建置 REST API。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-163">We use Restify to build your REST API.</span></span> <span data-ttu-id="8ed1b-164">Restify 是衍生自 Express 的最小且具彈性的 Node.js 應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="8ed1b-165">它有一組強大的功能，可在 Connect 之上建置 REST API。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="8ed1b-166">安裝 Restify</span><span class="sxs-lookup"><span data-stu-id="8ed1b-166">Install Restify</span></span>
<span data-ttu-id="8ed1b-167">從命令列，切換至 `azuread`目錄。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-167">From the command line, change your directory to `azuread`.</span></span> <span data-ttu-id="8ed1b-168">如果 `azuread` 目錄不存在，請建立一個。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-168">If the `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="8ed1b-169">`cd azuread` 或 `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="8ed1b-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="8ed1b-170">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-170">Enter the following command:</span></span>

`npm install restify`

<span data-ttu-id="8ed1b-171">此命令會安裝 Restify。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="8ed1b-172">您有收到錯誤訊息嗎？</span><span class="sxs-lookup"><span data-stu-id="8ed1b-172">Did you get an error?</span></span>
<span data-ttu-id="8ed1b-173">在某些作業系統上使用 `npm` 時，您可能會收到 `Error: EPERM, chmod '/usr/local/bin/..'` 的錯誤，並且要求您以系統管理員身分執行帳戶。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-173">In some operating systems, when you use `npm`, you may receive the error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run the account as an administrator.</span></span> <span data-ttu-id="8ed1b-174">若發生此問題，請使用 `sudo` 命令，以更高的權限層級執行 `npm`。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-174">If this problem occurs, use the `sudo` command to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="8ed1b-175">有發生 DTrace 錯誤嗎？</span><span class="sxs-lookup"><span data-stu-id="8ed1b-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="8ed1b-176">安裝 Restify 時，您可能會看到類似下面的文字：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="8ed1b-177">Restify 提供強大機制來使用 DTrace 追蹤 REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="8ed1b-178">不過，許多作業系統沒有 DTrace 可以使用。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="8ed1b-179">您可以放心地忽略這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="8ed1b-180">此命令的輸出應類似以下文字：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-180">The output of the command should appear similar to this text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="8ed1b-181">在您的 Web API 中安裝 Passport</span><span class="sxs-lookup"><span data-stu-id="8ed1b-181">Install Passport in your web API</span></span>
<span data-ttu-id="8ed1b-182">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-182">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="8ed1b-183">使用下列命令安裝 Passport：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-183">Install Passport using the following command:</span></span>

`npm install passport`

<span data-ttu-id="8ed1b-184">此命令的輸出應類似以下文字：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-184">The output of the command should be similar to this text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-to-your-web-api"></a><span data-ttu-id="8ed1b-185">將 passport-azuread 加入您的 Web API</span><span class="sxs-lookup"><span data-stu-id="8ed1b-185">Add passport-azuread to your web API</span></span>
<span data-ttu-id="8ed1b-186">接下來，使用 `passport-azuread`來新增 OAuth 策略，這是一套將 Azure AD 連接到 Passport 的策略。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-186">Next, add the OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="8ed1b-187">在這個 Rest API 範例中，請針對持有人權杖使用此策略。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-187">Use this strategy for bearer tokens in the REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed1b-188">雖然 OAuth2 提供可發行任何已知權杖類型的架構，但只會普遍使用特定的權杖類型。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="8ed1b-189">用於保護端點的權杖是持有者權杖。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-189">The tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="8ed1b-190">這些是 OAuth2 中最普遍發行的權杖類型。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-190">These types of tokens are the most widely issued in OAuth2.</span></span> <span data-ttu-id="8ed1b-191">許多實作假設持有者權杖會是唯一發行的權杖類型。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-191">Many implementations assume that bearer tokens are the only type of token issued.</span></span>
>
>

<span data-ttu-id="8ed1b-192">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-192">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="8ed1b-193">使用下列命令安裝 Passport `passport-azure-ad` 模組：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-193">Install the Passport `passport-azure-ad` module using the following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="8ed1b-194">此命令的輸出應類似以下文字：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-194">The output of the command should be similar to this text:</span></span>

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

## <a name="add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="8ed1b-195">將 MongoDB 模組加入您的 Web API</span><span class="sxs-lookup"><span data-stu-id="8ed1b-195">Add MongoDB modules to your web API</span></span>
<span data-ttu-id="8ed1b-196">此範例會使用 MongoDB 作為資料存放區。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="8ed1b-197">為此安裝 Mongoose，這是廣泛用於管理模型和結構描述的外掛程式。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="8ed1b-198">安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="8ed1b-198">Install additional modules</span></span>
<span data-ttu-id="8ed1b-199">接下來，安裝其餘所需的模組。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-199">Next, install the remaining required modules.</span></span>

<span data-ttu-id="8ed1b-200">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-200">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="8ed1b-201">在您的 `node_modules` 目錄中安裝模組：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-201">Install the modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="8ed1b-202">使用您的相依性建立 server.js 檔案</span><span class="sxs-lookup"><span data-stu-id="8ed1b-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="8ed1b-203">`server.js` 檔案會提供您的 Web API 伺服器的大部分功能。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-203">The `server.js` file provides the majority of the functionality for your Web API server.</span></span>

<span data-ttu-id="8ed1b-204">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-204">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="8ed1b-205">在編輯器中建立 `server.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="8ed1b-206">加入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-206">Add the following information:</span></span>

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

<span data-ttu-id="8ed1b-207">儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-207">Save the file.</span></span> <span data-ttu-id="8ed1b-208">您稍後會回到此檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-208">You return to it later.</span></span>

## <a name="create-a-configjs-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="8ed1b-209">建立 config.js 檔案來儲存您的 Azure AD 設定</span><span class="sxs-lookup"><span data-stu-id="8ed1b-209">Create a config.js file to store your Azure AD settings</span></span>
<span data-ttu-id="8ed1b-210">這個程式碼檔會將設定參數從您的 Azure AD 入口網站傳遞到 `Passport.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-210">This code file passes the configuration parameters from your Azure AD Portal to the `Passport.js` file.</span></span> <span data-ttu-id="8ed1b-211">在本逐步解說的第一個部分，您在將 Web API 加入入口網站時已建立這些組態值。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-211">You created these configuration values when you added the web API to the portal in the first part of the walk-through.</span></span> <span data-ttu-id="8ed1b-212">在您複製程式碼之後，我們會說明要放入這些參數值的內容。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-212">We explain what to put in the values of these parameters after you copy the code.</span></span>

<span data-ttu-id="8ed1b-213">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-213">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="8ed1b-214">在編輯器中建立 `config.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="8ed1b-215">加入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-215">Add the following information:</span></span>

```Javascript
// Don't commit this file to your public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in the portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // the Client ID of the application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add the B2C tenant name in the <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is the policy you'll want to validate against in B2C. Usually this is your Sign-in policy (as users sign in to this API)
passReqToCallback: false // This is a node.js construct that lets you pass the req all the way back to any upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="8ed1b-216">必要值</span><span class="sxs-lookup"><span data-stu-id="8ed1b-216">Required values</span></span>
<span data-ttu-id="8ed1b-217">`clientID`您的 Web API 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-217">`clientID`: The client ID of your Web API application.</span></span>

<span data-ttu-id="8ed1b-218">`IdentityMetadata`：`passport-azure-ad` 會在這裡尋找識別提供者的組態資料。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for the identity provider.</span></span> <span data-ttu-id="8ed1b-219">它也會尋找金鑰以驗證 JSON Web 權杖。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-219">It also looks for the keys to validate the JSON web tokens.</span></span>

<span data-ttu-id="8ed1b-220">`audience`：入口網站上的統一資源識別項 (URI)，用於識別您的呼叫端應用程式。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-220">`audience`: The uniform resource identifier (URI) from the portal that identifies your calling application.</span></span>

<span data-ttu-id="8ed1b-221">`tenantName`：您的租用戶名稱 (例如 **contoso.onmicrosoft.com**)。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="8ed1b-222">`policyName`：您想用來驗證傳入伺服器之權杖的原則。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-222">`policyName`: The policy that you want to validate the tokens coming in to your server.</span></span> <span data-ttu-id="8ed1b-223">此原則應與您針對用戶端應用程式登入所用的原則相同。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-223">This policy should be the same policy that you use on the client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="8ed1b-224">現在，請將相同的原則用於用戶端與伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-224">For now, use the same policies across both client and server setup.</span></span> <span data-ttu-id="8ed1b-225">如果您已完成逐步解說並建立這些原則，則不需要再做一次。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-225">If you have already completed a walk-through and created these policies, you don't need to do so again.</span></span> <span data-ttu-id="8ed1b-226">由於您已完成此逐步解說，您應該不需要在網站上為用戶端逐步解說建立新的原則。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-226">Because you completed the walk-through, you shouldn't need to set up new policies for client walk-throughs on the site.</span></span>
>
>

## <a name="add-configuration-to-your-serverjs-file"></a><span data-ttu-id="8ed1b-227">將設定加入 server.js 檔案</span><span class="sxs-lookup"><span data-stu-id="8ed1b-227">Add configuration to your server.js file</span></span>
<span data-ttu-id="8ed1b-228">若要從您建立的 `config.js`檔案讀取值，請在應用程式中新增 `.config` 檔案作為必要資源，然後將全域變數設定為 `config.js` 文件中的那些值。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-228">To read the values from the `config.js` file you created, add the `.config` file as a required resource in your application, and then set the global variables to those in the `config.js` document.</span></span>

<span data-ttu-id="8ed1b-229">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-229">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="8ed1b-230">在編輯器中開啟 `server.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-230">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="8ed1b-231">加入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-231">Add the following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="8ed1b-232">將包含下列程式碼的新區段新增至 `server.js` ：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-232">Add a new section to `server.js` that includes the following code:</span></span>

```Javascript
// We pass these options in to the ODICBearerStrategy.

var options = {
    // The URL of the metadata document for your app. We put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="8ed1b-233">接下來，我們會為使用者新增一些從呼叫端應用程式收到的預留位置。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-233">Next, let's add some placeholders for the users we receive from our calling applications.</span></span>

```Javascript
// array to hold logged in users and the current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="8ed1b-234">不用猶豫，讓我們同時建立記錄器。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="8ed1b-235">使用 Moongoose 新增 MongoDB 模型和結構描述資訊</span><span class="sxs-lookup"><span data-stu-id="8ed1b-235">Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="8ed1b-236">及早準備有助於在 REST API 服務中組合這三個檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-236">The earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="8ed1b-237">在此逐步解說中，請使用 MongoDB 來儲存工作，稍早所述。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-237">For this walk-through, use MongoDB to store your tasks, as discussed earlier.</span></span>

<span data-ttu-id="8ed1b-238">在 `config.js` 檔案中，您將資料庫命名為 **tasklist**。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-238">In the `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="8ed1b-239">該名稱也是您在 `mongoose_auth_local` 連線 URL 結尾處輸入的內容。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-239">That name was also what you put at the end of the `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="8ed1b-240">您不需要在 MongoDB 中事先建立此資料庫。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-240">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="8ed1b-241">第一次執行應用程式伺服器時，它會為您建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-241">It creates the database for you on the first run of your server application.</span></span>

<span data-ttu-id="8ed1b-242">在您告訴伺服器要使用哪個 MongoDB 資料庫之後，您必須撰寫一些額外程式碼，以建立伺服器工作的模型和結構描述。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-242">After you tell the server which MongoDB database to use, you need to write some additional code to create the model and schema for your server tasks.</span></span>

### <a name="expand-the-model"></a><span data-ttu-id="8ed1b-243">擴充模型</span><span class="sxs-lookup"><span data-stu-id="8ed1b-243">Expand the model</span></span>
<span data-ttu-id="8ed1b-244">此結構描述模型很簡單。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-244">This schema model is simple.</span></span> <span data-ttu-id="8ed1b-245">您可以視需要來擴充它。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-245">You can expand it as required.</span></span>

<span data-ttu-id="8ed1b-246">`owner`：指派給工作的人員。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-246">`owner`: Who is assigned to the task.</span></span> <span data-ttu-id="8ed1b-247">此物件是 **字串**。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-247">This object is a **string**.</span></span>  

<span data-ttu-id="8ed1b-248">`Text`：工作本身。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-248">`Text`: The task itself.</span></span> <span data-ttu-id="8ed1b-249">此物件是 **字串**。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-249">This object is a **string**.</span></span>

<span data-ttu-id="8ed1b-250">`date`：工作到期的日期。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-250">`date`: The date that the task is due.</span></span> <span data-ttu-id="8ed1b-251">此物件是 **日期時間**。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-251">This object is a **datetime**.</span></span>

<span data-ttu-id="8ed1b-252">`completed`：工作是否已完成。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-252">`completed`: If the task is complete.</span></span> <span data-ttu-id="8ed1b-253">此物件是 **布林值**。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-253">This object is a **Boolean**.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="8ed1b-254">在程式碼中建立結構描述</span><span class="sxs-lookup"><span data-stu-id="8ed1b-254">Create the schema in the code</span></span>
<span data-ttu-id="8ed1b-255">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-255">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="8ed1b-256">在編輯器中開啟 `server.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-256">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="8ed1b-257">在組態項目下方加入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-257">Add the following information below the configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect to MongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema to store our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use the schema to register a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="8ed1b-258">您首先建立結構描述，然後建立模型物件，在您定義 **路由**時用來儲存整個程式碼中的資料。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-258">You first create the schema, and then you create a model object that you use to store your data throughout the code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="8ed1b-259">新增 REST API 工作伺服器的路由</span><span class="sxs-lookup"><span data-stu-id="8ed1b-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="8ed1b-260">既然您已經有可以使用的資料庫模型，請新增要用於 REST API 伺服器的路由。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-260">Now that you have a database model to work with, add the routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="8ed1b-261">關於 Restify 中的路由</span><span class="sxs-lookup"><span data-stu-id="8ed1b-261">About routes in Restify</span></span>
<span data-ttu-id="8ed1b-262">路由在 Restify 中的運作與它們使用 Express 堆疊時的運作方式相同。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-262">Routes work in Restify in the same way that they work when they use the Express stack.</span></span> <span data-ttu-id="8ed1b-263">您可以使用您預期用戶端應用程式呼叫的 URI 來定義路由。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-263">You define routes by using the URI that you expect the client applications to call.</span></span>

<span data-ttu-id="8ed1b-264">Restify 路由的典型模式是：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep the server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="8ed1b-265">Resitfy 及 Express 可提供更深入的功能，例如定義應用程式類型和執行不同端點之間的複雜路由。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="8ed1b-266">基於本教學課程的目的，我們會將這些路由保持簡單。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-266">For the purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="8ed1b-267">將預設路由加入伺服器</span><span class="sxs-lookup"><span data-stu-id="8ed1b-267">Add default routes to your server</span></span>
<span data-ttu-id="8ed1b-268">您現在可為 REST API 新增 **create** 和 **list** 的基本 CRUD 路由。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-268">You now add the basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="8ed1b-269">在範例的 `complete` 分支中可以找到其他路由。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-269">Other routes can be found in the `complete` branch of the sample.</span></span>

<span data-ttu-id="8ed1b-270">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-270">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="8ed1b-271">在編輯器中開啟 `server.js` 檔案。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-271">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="8ed1b-272">在您先前輸入的資料庫項目底下，新增下列資訊：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-272">Below the database entries you made above add the following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it to Mongodb
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
            req.log.warn(err, 'createTask: unable to save');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

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
            log.warn(err, "There is no tasks in the database. Add one!");
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


#### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="8ed1b-273">新增路由的錯誤處理</span><span class="sxs-lookup"><span data-stu-id="8ed1b-273">Add error handling for the routes</span></span>
<span data-ttu-id="8ed1b-274">新增一些錯誤處理，以便您將遇到的任何問題，以用戶端可了解的方式傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-274">Add some error handling so that you can communicate any problems you encounter back to the client in a way that it can understand.</span></span>

<span data-ttu-id="8ed1b-275">新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-275">Add the following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back to the client
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


## <a name="create-your-server"></a><span data-ttu-id="8ed1b-276">建立伺服器</span><span class="sxs-lookup"><span data-stu-id="8ed1b-276">Create your server</span></span>
<span data-ttu-id="8ed1b-277">您現在已定義資料庫並備妥路由。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="8ed1b-278">最後一件事是新增伺服器執行個體，以管理您的呼叫。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-278">The last thing for you to do is to add the server instance that manages your calls.</span></span>

<span data-ttu-id="8ed1b-279">Restify 及 Express 為 REST API 伺服器提供進階的自訂功能，但我們會使用最基本的設定。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-279">Restify and Express provide deep customization for a REST API server, but we use the most basic setup here.</span></span>

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

// Allow 5 requests/second by IP, and burst to 10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping to REST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-the-routes-to-the-server-without-authentication"></a><span data-ttu-id="8ed1b-280">將路由加入伺服器 (不含驗證)</span><span class="sxs-lookup"><span data-stu-id="8ed1b-280">Add the routes to the server (without authentication)</span></span>
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
    consoleMessage += '\n Open your browser to %s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-to-your-rest-api-server"></a><span data-ttu-id="8ed1b-281">將驗證加入 REST API 伺服器</span><span class="sxs-lookup"><span data-stu-id="8ed1b-281">Add authentication to your REST API server</span></span>
<span data-ttu-id="8ed1b-282">既然您已經有執行中的 REST API 伺服器，您可以讓它在 Azure AD 中發揮價值。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="8ed1b-283">從命令列，切換至 `azuread`目錄 (如果還不在此目錄下)：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-283">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="8ed1b-284">使用 passport-azure-ad 隨附的 OIDCBearerStrategy</span><span class="sxs-lookup"><span data-stu-id="8ed1b-284">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="8ed1b-285">撰寫 API 時，您應一律將資料連結到使用者無法證明其在權杖中是唯一的項目。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-285">When you write APIs, you should always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="8ed1b-286">伺服器儲存 ToDo 項目時，它會根據放在 [擁有者] 欄位的權杖 (透過 token.oid 呼叫) 中使用者的 **oid** 來儲存這些項目。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-286">When the server stores ToDo items, it does so based on the **oid** of the user in the token (called through token.oid), which goes in the “owner” field.</span></span> <span data-ttu-id="8ed1b-287">此值可確保只有該使用者可以存取自己的 ToDo 項目。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="8ed1b-288">不會在「擁有者」API 中公開，因此，外部使用者可以要求其他人的 ToDo 項目，即使它們已經過驗證也一樣。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-288">There is no exposure in the API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="8ed1b-289">接下來，使用隨附於 `passport-azure-ad`的持有人策略。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-289">Next, use the bearer strategy that comes with `passport-azure-ad`.</span></span>

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
        log.info('verifying the user');
        log.info(token, 'was the token retreived');
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

<span data-ttu-id="8ed1b-290">Passport 對其所有的策略使用相同的模式。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-290">Passport uses the same pattern for all its strategies.</span></span> <span data-ttu-id="8ed1b-291">您需要傳遞以 `token` 和 `done` 為參數的 `function()` 給它。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="8ed1b-292">策略在完成所有工作之後會回到您這邊。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-292">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="8ed1b-293">然後，您應該儲存使用者和權杖，如此就不需再次要求它。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-293">You should then store the user and save the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ed1b-294">上述程式碼會接受正好向您的伺服器驗證的任何使用者。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-294">The code above takes any user who happens to authenticate to your server.</span></span> <span data-ttu-id="8ed1b-295">此程序稱為自動註冊。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-295">This process is known as autoregistration.</span></span> <span data-ttu-id="8ed1b-296">在生產伺服器中，除非使用者先完成註冊程序，否則不要讓他們存取 API。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-296">In production servers, don't let in any users access the API without first having them go through a registration process.</span></span> <span data-ttu-id="8ed1b-297">此程序常見於一些取用者應用程式中，先是可讓您使用 Facebook 來註冊，但接著會要求您填寫其他資訊。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-297">This process is usually the pattern you see in consumer apps that allow you to register by using Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="8ed1b-298">如果此程式不是命令列程式，我們可以從傳回的權杖物件中擷取電子郵件，然後要求使用者填寫其他資訊。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-298">If this program wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked users to fill out additional information.</span></span> <span data-ttu-id="8ed1b-299">因為這是範例，所以我們會將其新增至記憶體中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-299">Because this is a sample, we add them to an in-memory database.</span></span>
>
>

## <a name="run-your-server-application-to-verify-that-it-rejects-you"></a><span data-ttu-id="8ed1b-300">執行伺服器應用程式，確認它會拒絕您的要求</span><span class="sxs-lookup"><span data-stu-id="8ed1b-300">Run your server application to verify that it rejects you</span></span>
<span data-ttu-id="8ed1b-301">您可以使用 `curl` ，檢查現在是否以 OAuth2 保護您的端點。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-301">You can use `curl` to see if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="8ed1b-302">傳回的標頭應該足以說明您執行的作業正確無誤。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-302">The headers returned should be enough to tell you that you are on the right path.</span></span>

<span data-ttu-id="8ed1b-303">請確定您的 MongoDB 執行個體正在執行：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="8ed1b-304">切換至目錄，然後執行伺服器：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-304">Change to the directory and run the server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="8ed1b-305">在新的終端機視窗中，執行 `curl`</span><span class="sxs-lookup"><span data-stu-id="8ed1b-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="8ed1b-306">嘗試基本的 POST 方法：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="8ed1b-307">401 錯誤是您想要的回應。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-307">A 401 error is the response you want.</span></span> <span data-ttu-id="8ed1b-308">它指出 Passport 層正嘗試重新導向到授權端點。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-308">It indicates that the Passport layer is trying to redirect to the authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="8ed1b-309">您現在擁有一項使用 OAuth2 的 REST API 服務</span><span class="sxs-lookup"><span data-stu-id="8ed1b-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="8ed1b-310">您已使用 Restify 和 OAuth 實作 REST API！</span><span class="sxs-lookup"><span data-stu-id="8ed1b-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="8ed1b-311">您現在已經有足夠的程式碼可以繼續開發服務，並以此範例為基礎進行建置。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-311">You now have sufficient code so that you can continue to develop your service and build on this example.</span></span> <span data-ttu-id="8ed1b-312">在未使用 OAuth2 相容用戶端的情況下，您已經儘可能地使用此伺服器的所有功能。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="8ed1b-313">接下來使用其他逐步解說，例如我們的 [使用 iOS 搭配 B2C 連線至 Web API](active-directory-b2c-devquickstarts-ios.md) 逐步解說。</span><span class="sxs-lookup"><span data-stu-id="8ed1b-313">For that next step use an additional walk-through like our [Connect to a web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ed1b-314">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8ed1b-314">Next steps</span></span>
<span data-ttu-id="8ed1b-315">您現在可以進入更進階的主題，例如：</span><span class="sxs-lookup"><span data-stu-id="8ed1b-315">You can now move to more advanced topics, such as:</span></span>

[<span data-ttu-id="8ed1b-316">使用 iOS 搭配 B2C 連線至 Web API</span><span class="sxs-lookup"><span data-stu-id="8ed1b-316">Connect to a web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
