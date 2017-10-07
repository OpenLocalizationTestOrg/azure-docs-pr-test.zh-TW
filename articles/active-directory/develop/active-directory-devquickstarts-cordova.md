---
title: "開始使用 AD Cordova aaaAzure |Microsoft 文件"
description: "如何 toobuild Cordova 應用程式的整合 Azure AD 進行登入及使用 OAuth 呼叫 Azure AD 保護應用程式開發介面。"
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="27030-103">整合 Azure AD 與 Apache Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="27030-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="27030-104">您可以使用 Apache Cordova toodevelop HTML5/JavaScript 應用程式可以在單純的原生應用程式的行動裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="27030-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="27030-105">與 Azure Active Directory (Azure AD)，您可以加入企業等級驗證功能 tooyour Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27030-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="27030-106">iOS、Android、Windows 市集和 Windows Phone 上的 Cordova 外掛程式包裝了 Azure AD 原生 SDK。</span><span class="sxs-lookup"><span data-stu-id="27030-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="27030-107">使用的外掛程式，您可以增強您的應用程式登入與使用者的 Windows Server Active Directory 帳戶、 改善存取 tooOffice 365 及 Azure 應用程式開發介面，而且甚至 toosupport 保護呼叫 tooyour 自己自訂的 web 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="27030-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="27030-108">在本教學課程中，我們將藉由新增下列功能的 hello hello Apache Cordova 外掛程式使用的 Active Directory 驗證程式庫 (ADAL) tooimprove 簡單的應用程式：</span><span class="sxs-lookup"><span data-stu-id="27030-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="27030-109">只要短短幾行程式碼，就可驗證使用者並取得權杖。</span><span class="sxs-lookup"><span data-stu-id="27030-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="27030-110">使用該語彙基元 tooinvoke hello Graph API tooquery 該目錄，並顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="27030-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="27030-111">使用 hello ADAL 權杖快取 toominimize 驗證提示 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="27030-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="27030-112">toomake 這些增強功能，您需要：</span><span class="sxs-lookup"><span data-stu-id="27030-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="27030-113">向 Azure AD 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="27030-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="27030-114">加入程式碼 tooyour 應用程式 toorequest 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="27030-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="27030-115">加入程式碼來查詢 Graph API hello toouse hello 語彙基元，並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="27030-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="27030-116">建立 hello Cordova 部署專案與所有 hello 平台 tootarget，新增 hello Cordova ADAL 外掛程式，然後在模擬器中測試 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="27030-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27030-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="27030-117">Prerequisites</span></span>
<span data-ttu-id="27030-118">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="27030-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="27030-119">Azure AD 租用戶，您在其中有一個帳戶具備應用程式開發權限。</span><span class="sxs-lookup"><span data-stu-id="27030-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="27030-120">已設定 toouse Apache Cordova 開發環境。</span><span class="sxs-lookup"><span data-stu-id="27030-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="27030-121">如果您已經有同時設定，直接繼續 toostep 1。</span><span class="sxs-lookup"><span data-stu-id="27030-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="27030-122">如果您沒有 Azure AD 租用戶，請使用 hello[指示一個 tooget](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="27030-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="27030-123">如果您沒有在您的電腦上設定的 Apache Cordova，安裝 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="27030-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="27030-124">Git</span><span class="sxs-lookup"><span data-stu-id="27030-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="27030-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="27030-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="27030-126">[Cordova CLI](https://cordova.apache.org/) (可以輕鬆地透過 NPM 封裝管理員來安裝：`npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="27030-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="27030-127">hello PC 與 hello mac 上，應該運作之前安裝的 hello</span><span class="sxs-lookup"><span data-stu-id="27030-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="27030-128">每個目標平台各有不同的必要條件：</span><span class="sxs-lookup"><span data-stu-id="27030-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="27030-129">toobuild 和執行應用程式 Windows 平板電腦或 Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="27030-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="27030-130">安裝 [Visual Studio 2013 for Windows (含 Update 2) 或更新版本](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express 或其他版本) 或 [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community)。</span><span class="sxs-lookup"><span data-stu-id="27030-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="27030-131">toobuild 並執行 iOS 應用程式：</span><span class="sxs-lookup"><span data-stu-id="27030-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="27030-132">安裝 Xcode 6.x 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="27030-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="27030-133">下載從 hello [Apple 開發人員網站](http://developer.apple.com/downloads)或 hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12)。</span><span class="sxs-lookup"><span data-stu-id="27030-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="27030-134">安裝 [ios-sim](https://www.npmjs.org/package/ios-sim)。</span><span class="sxs-lookup"><span data-stu-id="27030-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="27030-135">您可以使用它 toostart iOS 應用程式中 hello 命令列上的 iOS 模擬器。</span><span class="sxs-lookup"><span data-stu-id="27030-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="27030-136">(您可以輕鬆地將它安裝透過終端機 hello: `npm install -g ios-sim`。)</span><span class="sxs-lookup"><span data-stu-id="27030-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="27030-137">toobuild 和適用於 Android 的應用程式執行：</span><span class="sxs-lookup"><span data-stu-id="27030-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="27030-138">安裝 [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="27030-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="27030-139">請確定`JAVA_HOME`根據 toohello JDK 安裝路徑 (例如，C:\Program Files\Java\jdk1.7.0_75) 正確設定 （環境變數）。</span><span class="sxs-lookup"><span data-stu-id="27030-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="27030-140">安裝[Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools)和新增 hello`<android-sdk-location>\tools`位置 (例如，C:\tools\Android\android-sdk\tools) tooyour`PATH`環境變數。</span><span class="sxs-lookup"><span data-stu-id="27030-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="27030-141">開啟 Android SDK 管理員 (例如，透過終端機 hello: `android`) 並安裝：</span><span class="sxs-lookup"><span data-stu-id="27030-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="27030-142">*Android 5.0.1 (API 21)* 平台 SDK</span><span class="sxs-lookup"><span data-stu-id="27030-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="27030-143">Android SDK Build Tools 19.1.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="27030-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="27030-144">*Android Support Repository* (Extras)</span><span class="sxs-lookup"><span data-stu-id="27030-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="27030-145">hello Android SDK 不提供任何預設模擬器執行個體。</span><span class="sxs-lookup"><span data-stu-id="27030-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="27030-146">建立一個執行`android avd`hello 終端機，然後選取 從**建立**，如果您想 toorun hello Android 應用程式在模擬器上的。</span><span class="sxs-lookup"><span data-stu-id="27030-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="27030-147">我們建議 API 層級 19 或更高。</span><span class="sxs-lookup"><span data-stu-id="27030-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="27030-148">如需 hello Android 模擬器和建立選項的詳細資訊，請參閱[AVD Manager](http://developer.android.com/tools/help/avd-manager.html) hello Android 網站上。</span><span class="sxs-lookup"><span data-stu-id="27030-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="27030-149">步驟 1︰向 Azure AD 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="27030-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="27030-150">此為選用步驟。</span><span class="sxs-lookup"><span data-stu-id="27030-150">This step is optional.</span></span> <span data-ttu-id="27030-151">本教學課程提供您可以使用 toosee 預先佈建的值而不需要執行任何佈建在自己的租用戶 hello 動作中的範例。</span><span class="sxs-lookup"><span data-stu-id="27030-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="27030-152">不過，我們建議您不要執行這個步驟，並熟悉 hello 程序，因為它會在必要時建立自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="27030-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="27030-153">Azure AD 發出權杖 tooonly 已知的應用程式。</span><span class="sxs-lookup"><span data-stu-id="27030-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="27030-154">您可以使用 Azure AD 從您的應用程式之前，您需要 toocreate 項目，在您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="27030-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="27030-155">tooregister 租用戶中新的應用程式：</span><span class="sxs-lookup"><span data-stu-id="27030-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="27030-156">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="27030-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27030-157">Hello 頂端列上，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="27030-157">On hello top bar, click your account.</span></span> <span data-ttu-id="27030-158">在 hello**目錄**清單中，選擇您想要 tooregister hello Azure AD 租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="27030-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="27030-159">按一下**更服務**在 hello 左的窗格，然後選取  **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="27030-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="27030-160">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="27030-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="27030-161">依照 hello 提示，並建立**原生用戶端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="27030-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="27030-162">(雖然 Cordova 應用程式是 HTML 架構，我們在此要建立的是原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="27030-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="27030-163">hello**原生用戶端應用程式**必須選取選項，或 hello 應用程式將無法運作。)</span><span class="sxs-lookup"><span data-stu-id="27030-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="27030-164">**名稱**描述應用程式 toousers。</span><span class="sxs-lookup"><span data-stu-id="27030-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="27030-165">**重新導向 URI**為 hello 已使用 tooreturn 語彙基元 tooyour 應用程式的 URI。</span><span class="sxs-lookup"><span data-stu-id="27030-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="27030-166">輸入 **http://MyDirectorySearcherApp**。</span><span class="sxs-lookup"><span data-stu-id="27030-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="27030-167">完成註冊之後，Azure AD 會指派唯一的應用程式識別碼 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27030-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="27030-168">您必須以 hello 下一節中的值。</span><span class="sxs-lookup"><span data-stu-id="27030-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="27030-169">您可以將它找到新建立的應用程式的 hello hello 應用程式 索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="27030-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="27030-170">toorun `DirSearchClient Sample`，授與 hello 新建立的應用程式的權限 tooquery hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="27030-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="27030-171">從 hello**設定**頁面上，選取**必要的使用權限**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="27030-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="27030-172">Hello Azure Active Directory 應用程式中，選取**Microsoft Graph**為 hello 應用程式開發介面，並加入 hello **hello 登入的使用者身分存取 hello 目錄**權限下的**委派權限**。</span><span class="sxs-lookup"><span data-stu-id="27030-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="27030-173">這可讓使用者您應用程式 tooquery hello Graph API。</span><span class="sxs-lookup"><span data-stu-id="27030-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="27030-174">步驟 2： 複製 hello 範例應用程式儲存機制</span><span class="sxs-lookup"><span data-stu-id="27030-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="27030-175">從殼層或命令列中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="27030-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="27030-176">步驟 3： 建立 hello Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="27030-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="27030-177">有多個方式 toocreate Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27030-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="27030-178">在本教學課程中，我們將使用 hello Cordova 命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="27030-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="27030-179">從殼層或命令列中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="27030-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="27030-180">該命令會建立 hello 資料夾結構和 scaffolding hello Cordova 專案。</span><span class="sxs-lookup"><span data-stu-id="27030-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="27030-181">移動 toohello 新 DirSearchClient 資料夾：</span><span class="sxs-lookup"><span data-stu-id="27030-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="27030-182">使用檔案管理員或使用下列命令，在您的 shell 中的 hello hello www 子資料夾中複製 hello hello 入門專案內容：</span><span class="sxs-lookup"><span data-stu-id="27030-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="27030-183">Windows：`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="27030-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="27030-184">Mac：`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="27030-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="27030-185">新增 hello 白名單外掛程式。</span><span class="sxs-lookup"><span data-stu-id="27030-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="27030-186">這是必要的叫用 hello Graph API。</span><span class="sxs-lookup"><span data-stu-id="27030-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="27030-187">新增所有您想 toosupport hello 平台。</span><span class="sxs-lookup"><span data-stu-id="27030-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="27030-188">toohave 工作範例，您需要下列命令的 hello 的 tooexecute 至少一個。</span><span class="sxs-lookup"><span data-stu-id="27030-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="27030-189">請注意，將不會在 Windows 上的無法 tooemulate iOS 或模擬在 mac 上的 Windows</span><span class="sxs-lookup"><span data-stu-id="27030-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="27030-190">加入 Cordova 外掛程式 tooyour 專案 hello ADAL:</span><span class="sxs-lookup"><span data-stu-id="27030-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="27030-191">步驟 4： 加入程式碼 tooauthenticate 使用者，並從 Azure AD 取得權杖</span><span class="sxs-lookup"><span data-stu-id="27030-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="27030-192">在本教學課程，您正在開發的 hello 應用程式會提供簡單的目錄搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="27030-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="27030-193">hello 使用者即可輸入 hello 目錄中的 hello 別名的任何使用者或以視覺化方式檢視一些基本的屬性。</span><span class="sxs-lookup"><span data-stu-id="27030-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="27030-194">hello 入門專案包含 hello hello 基本使用者介面 （在 www/index.html) hello 應用程式的定義和基本應用程式事件繫結在一起的 hello scaffolding 循環，使用者介面的繫結，並產生顯示邏輯 （在 www/js/index.js)。</span><span class="sxs-lookup"><span data-stu-id="27030-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="27030-195">hello 留下您的唯一工作是 tooadd hello 邏輯實作識別工作。</span><span class="sxs-lookup"><span data-stu-id="27030-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="27030-196">hello 第一件事您在程式碼中需要 toodo 是導入 hello Azure AD 來識別您的應用程式所使用的通訊協定值與 hello 您設定為目標的資源。</span><span class="sxs-lookup"><span data-stu-id="27030-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="27030-197">這些值將在稍後會使用的 tooconstruct hello 權杖要求。</span><span class="sxs-lookup"><span data-stu-id="27030-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="27030-198">插入下列程式碼片段在 hello hello index.js 檔案最上方的 hello:</span><span class="sxs-lookup"><span data-stu-id="27030-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="27030-199">hello`redirectUri`和`clientId`值應符合您的應用程式描述 Azure AD 中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="27030-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="27030-200">您可以找到與 hello**設定**hello Azure 入口網站中索引標籤，如稍早在本教學課程步驟 1 中所述。</span><span class="sxs-lookup"><span data-stu-id="27030-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="27030-201">如果您選擇不在您自己的租用戶中註冊新的應用程式，您只可以貼上 hello 預先設定的值。</span><span class="sxs-lookup"><span data-stu-id="27030-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="27030-202">您可以看見 hello 範例執行，但您應該一律適用於實際執行的應用程式建立自己的項目。</span><span class="sxs-lookup"><span data-stu-id="27030-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="27030-203">接下來，加入 hello 權杖要求程式碼。</span><span class="sxs-lookup"><span data-stu-id="27030-203">Next, add hello token request code.</span></span> <span data-ttu-id="27030-204">插入下列程式碼片段之間 hello hello`search`和`renderData`定義：</span><span class="sxs-lookup"><span data-stu-id="27030-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="27030-205">讓我們將該函式分成兩個主要部分來檢查一下。</span><span class="sxs-lookup"><span data-stu-id="27030-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="27030-206">這個範例是設計的 toowork 搭配任何租用戶，但不要的 toobeing 繫結 tooa 特定的。</span><span class="sxs-lookup"><span data-stu-id="27030-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="27030-207">它會使用 hello"/ 常見"的端點，這可讓 hello 使用者 tooenter 任何帳戶，在驗證階段，並指示 hello 要求 toohello 租用戶所屬的位置。</span><span class="sxs-lookup"><span data-stu-id="27030-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="27030-208">Hello 方法的第一部分會檢查 hello ADAL 快取 toosee，如果已儲存的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="27030-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="27030-209">如果是這樣，hello 方法會使用 hello 租用戶 hello 語彙基元來自何處來重新初始化 ADAL。</span><span class="sxs-lookup"><span data-stu-id="27030-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="27030-210">這是必要 tooavoid 額外的提示，因為 hello 使用的"/ 常見"永遠會導致詢問 hello 使用者 tooenter 新帳戶。</span><span class="sxs-lookup"><span data-stu-id="27030-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="27030-211">hello 的 hello 方法的第二個部分執行 hello 適當的權杖要求。</span><span class="sxs-lookup"><span data-stu-id="27030-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="27030-212">hello`acquireTokenSilentAsync`方法要求 ADAL tooreturn 語彙基元 hello 指定資源不會顯示任何 UX</span><span class="sxs-lookup"><span data-stu-id="27030-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="27030-213">如果 hello 快取中已經有適當的存取語彙基元儲存，可以發生的如果可以在重新整理權杖用 tooget 新存取權杖，而不會顯示任何提示。</span><span class="sxs-lookup"><span data-stu-id="27030-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="27030-214">如果該嘗試失敗，我們會切換回`acquireTokenAsync`-這會明顯地提示 hello 使用者 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="27030-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="27030-215">現在，我們已經 hello 語彙基元，但我們最後會叫用 hello Graph API，並執行 hello 我們想要的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="27030-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="27030-216">插入下列程式碼片段如下 hello hello`authenticate`定義：</span><span class="sxs-lookup"><span data-stu-id="27030-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="27030-217">hello 起點檔案提供簡單的 UX 在文字方塊中輸入使用者的別名。</span><span class="sxs-lookup"><span data-stu-id="27030-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="27030-218">這個方法會使用該值 tooconstruct 查詢、 結合 hello 存取語彙基元、 將它送出 tooMicrosoft 圖形，和剖析 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="27030-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="27030-219">hello`renderData`已經存在於 hello 起點檔案，方法會負責視覺化 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="27030-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="27030-220">步驟 5： 執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="27030-220">Step 5: Run hello app</span></span>
<span data-ttu-id="27030-221">您的應用程式是最後準備 toorun。</span><span class="sxs-lookup"><span data-stu-id="27030-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="27030-222">作業系統就相當簡單： hello 應用程式啟動時，輸入您想 toolook，hello 使用者 hello 別名，然後再按一下 [hello] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27030-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="27030-223">系統會提示您進行驗證。</span><span class="sxs-lookup"><span data-stu-id="27030-223">You're prompted for authentication.</span></span> <span data-ttu-id="27030-224">在驗證成功，成功的搜尋會顯示 hello hello 搜尋使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="27030-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="27030-225">後續執行將不會顯示任何提示字元執行 hello 搜尋，這 toohello 與否 hello 先前取得快取中的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="27030-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="27030-226">hello 執行 hello 應用程式的具象步驟會因平台而異。</span><span class="sxs-lookup"><span data-stu-id="27030-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="27030-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="27030-227">Windows 10</span></span>
   <span data-ttu-id="27030-228">平板電腦/PC： `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="27030-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="27030-229">行動 （需要 Windows 10 行動裝置版 」 裝置連接 tooa PC）：`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="27030-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="27030-230">在第一次執行的 hello，可能會要求您在 toosign 的開發人員授權。</span><span class="sxs-lookup"><span data-stu-id="27030-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="27030-231">如需詳細資訊，請參閱[開發人員授權](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)。</span><span class="sxs-lookup"><span data-stu-id="27030-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="27030-232">Windows 8.1 平板電腦/PC</span><span class="sxs-lookup"><span data-stu-id="27030-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="27030-233">在第一次執行的 hello，可能會要求您在 toosign 的開發人員授權。</span><span class="sxs-lookup"><span data-stu-id="27030-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="27030-234">如需詳細資訊，請參閱[開發人員授權](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)。</span><span class="sxs-lookup"><span data-stu-id="27030-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="27030-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="27030-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="27030-236">toorun 連線的裝置上：`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="27030-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="27030-237">toorun hello 預設模擬器上：`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="27030-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="27030-238">使用`cordova run windows --list -- --phone`toosee 所有可用的目標和`cordova run windows --target=<target_name> -- --phone`toorun hello 應用程式的特定裝置或模擬器上 (例如， `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`)。</span><span class="sxs-lookup"><span data-stu-id="27030-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="27030-239">Android</span><span class="sxs-lookup"><span data-stu-id="27030-239">Android</span></span>
   <span data-ttu-id="27030-240">toorun 連線的裝置上：`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="27030-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="27030-241">toorun hello 預設模擬器上：`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="27030-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="27030-242">請確定您已使用 AVD Manager 建立的模擬器執行個體，如稍早在 hello < 先決條件 > 一節中所述。</span><span class="sxs-lookup"><span data-stu-id="27030-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="27030-243">使用`cordova run android --list`toosee 所有可用的目標和`cordova run android --target=<target_name>`toorun hello 應用程式的特定裝置或模擬器上 (例如， `cordova run android --target="Nexus4_emulator"`)。</span><span class="sxs-lookup"><span data-stu-id="27030-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="27030-244">iOS</span><span class="sxs-lookup"><span data-stu-id="27030-244">iOS</span></span>
   <span data-ttu-id="27030-245">toorun 連線的裝置上：`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="27030-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="27030-246">toorun hello 預設模擬器上：`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="27030-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="27030-247">請確定您擁有 hello `ios-sim` hello 模擬器上的安裝套件 toorun。</span><span class="sxs-lookup"><span data-stu-id="27030-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="27030-248">如需詳細資訊，請參閱 hello < 先決條件 > 一節。</span><span class="sxs-lookup"><span data-stu-id="27030-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="27030-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27030-249">Next steps</span></span>
<span data-ttu-id="27030-250">參考，完成的 hello 範例 （不含您的組態值） 會提供[GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient)。</span><span class="sxs-lookup"><span data-stu-id="27030-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="27030-251">您可以現在移動 toomore 進階 （以及更多有趣） 案例。</span><span class="sxs-lookup"><span data-stu-id="27030-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="27030-252">您可能會想 tootry:[安全與 Azure AD Node.js Web API](active-directory-devquickstarts-webapi-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="27030-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
