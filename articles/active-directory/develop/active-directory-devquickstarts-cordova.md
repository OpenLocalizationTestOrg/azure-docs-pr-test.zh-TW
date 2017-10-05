---
title: "開始使用 Azure AD Cordova | Microsoft Docs"
description: "如何建置 Cordova 應用程式來與 Azure AD 整合進行登入，並使用 OAuth 呼叫受 Azure AD 保護的 API。"
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
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="4627b-103">整合 Azure AD 與 Apache Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="4627b-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="4627b-104">您可以使用 Apache Cordova 開發 HTML5/JavaScript 應用程式，在行動裝置上當做一個完備的原生應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="4627b-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="4627b-105">Azure Active Directory (Azure AD) 可讓您將企業級的驗證功能加入 Cordova 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="4627b-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="4627b-106">iOS、Android、Windows 市集和 Windows Phone 上的 Cordova 外掛程式包裝了 Azure AD 原生 SDK。</span><span class="sxs-lookup"><span data-stu-id="4627b-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="4627b-107">使用此外掛程式，可以增強您的應用程式來支援以使用者的 Windows Server Active Director 帳戶登入、存取 Office 365 和 Azure API，甚至保護對您自己自訂的 Web API 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="4627b-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="4627b-108">在本教學課程中，我們將使用 Active Directory 驗證程式庫 (ADAL) 的 Apache Cordova 外掛程式，加入下列功能來改善一個簡單的應用程式：</span><span class="sxs-lookup"><span data-stu-id="4627b-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="4627b-109">只要短短幾行程式碼，就可驗證使用者並取得權杖。</span><span class="sxs-lookup"><span data-stu-id="4627b-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="4627b-110">使用該權杖叫用 Graph API 來查詢目錄，並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="4627b-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="4627b-111">運用 ADAL 權杖快取，將使用者的驗證提示減到最少。</span><span class="sxs-lookup"><span data-stu-id="4627b-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="4627b-112">若要實現這些強化功能，您需要︰</span><span class="sxs-lookup"><span data-stu-id="4627b-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="4627b-113">向 Azure AD 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627b-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="4627b-114">在您的應用程式中加入程式碼來要求權杖。</span><span class="sxs-lookup"><span data-stu-id="4627b-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="4627b-115">加入程式碼以使用權杖來查詢 Graph API，並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="4627b-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="4627b-116">使用您想要做為目標的所有平台建立 Cordova 部署專案，新增 Cordova ADAL 外掛程式，並在模擬器中測試解決方案。</span><span class="sxs-lookup"><span data-stu-id="4627b-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4627b-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="4627b-117">Prerequisites</span></span>
<span data-ttu-id="4627b-118">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="4627b-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="4627b-119">Azure AD 租用戶，您在其中有一個帳戶具備應用程式開發權限。</span><span class="sxs-lookup"><span data-stu-id="4627b-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="4627b-120">為了使用 Apache Cordova 而設定的開發環境。</span><span class="sxs-lookup"><span data-stu-id="4627b-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="4627b-121">如果兩者都已齊備，直接跳到步驟 1。</span><span class="sxs-lookup"><span data-stu-id="4627b-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="4627b-122">如果您沒有 Azure AD 租用戶，請使用[如何取得租用戶的指示](active-directory-howto-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="4627b-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="4627b-123">如果您的電腦上沒有安裝 Apache Cordova，請安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="4627b-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="4627b-124">Git</span><span class="sxs-lookup"><span data-stu-id="4627b-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="4627b-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="4627b-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="4627b-126">[Cordova CLI](https://cordova.apache.org/) (可以輕鬆地透過 NPM 封裝管理員來安裝：`npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="4627b-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="4627b-127">上述安裝應該在 PC 和 Mac 上都可以執行。</span><span class="sxs-lookup"><span data-stu-id="4627b-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="4627b-128">每個目標平台各有不同的必要條件：</span><span class="sxs-lookup"><span data-stu-id="4627b-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="4627b-129">建置和執行適用於 Windows 平板電腦/PC 或 Windows Phone 的應用程式：</span><span class="sxs-lookup"><span data-stu-id="4627b-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="4627b-130">安裝 [Visual Studio 2013 for Windows (含 Update 2) 或更新版本](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express 或其他版本) 或 [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community)。</span><span class="sxs-lookup"><span data-stu-id="4627b-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="4627b-131">建置和執行適用於 iOS 的應用程式：</span><span class="sxs-lookup"><span data-stu-id="4627b-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="4627b-132">安裝 Xcode 6.x 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4627b-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="4627b-133">請從 [Apple 開發人員網站](http://developer.apple.com/downloads)或 [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12) 下載。</span><span class="sxs-lookup"><span data-stu-id="4627b-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="4627b-134">安裝 [ios-sim](https://www.npmjs.org/package/ios-sim)。</span><span class="sxs-lookup"><span data-stu-id="4627b-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="4627b-135">您可以使用它在 iOS 模擬器中從命令列啟動 iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627b-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="4627b-136">(您可以透過終端機輕鬆地安裝它︰`npm install -g ios-sim`。)</span><span class="sxs-lookup"><span data-stu-id="4627b-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="4627b-137">建置和執行適用於 Android 的應用程式：</span><span class="sxs-lookup"><span data-stu-id="4627b-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="4627b-138">安裝 [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4627b-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="4627b-139">請確定 `JAVA_HOME` (環境變數) 已根據 JDK 安裝路徑 (例如 C:\Program Files\Java\jdk1.7.0_75) 正確設定。</span><span class="sxs-lookup"><span data-stu-id="4627b-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="4627b-140">安裝 [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools)，並將 `<android-sdk-location>\tools` 位置 (例如 C:\tools\Android\android-sdk\tools) 新增至 `PATH` 環境變數。</span><span class="sxs-lookup"><span data-stu-id="4627b-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="4627b-141">開啟 Android SDK Manager (例如，透過終端機：`android`)，然後安裝：</span><span class="sxs-lookup"><span data-stu-id="4627b-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="4627b-142">*Android 5.0.1 (API 21)* 平台 SDK</span><span class="sxs-lookup"><span data-stu-id="4627b-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="4627b-143">Android SDK Build Tools 19.1.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="4627b-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="4627b-144">*Android Support Repository* (Extras)</span><span class="sxs-lookup"><span data-stu-id="4627b-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="4627b-145">Android SDK 並不提供任何預設模擬器執行個體。</span><span class="sxs-lookup"><span data-stu-id="4627b-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="4627b-146">如果您想要在模擬器上執行 Android 應用程式，請從終端機執行 `android avd` 然後選取 [建立]，以建立新的模擬器執行個體。</span><span class="sxs-lookup"><span data-stu-id="4627b-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="4627b-147">我們建議 API 層級 19 或更高。</span><span class="sxs-lookup"><span data-stu-id="4627b-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="4627b-148">請參閱 Android 網站上的 [AVD Manager](http://developer.android.com/tools/help/avd-manager.html)，取得 Android 模擬器和建立選項的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4627b-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="4627b-149">步驟 1︰向 Azure AD 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="4627b-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="4627b-150">此為選用步驟。</span><span class="sxs-lookup"><span data-stu-id="4627b-150">This step is optional.</span></span> <span data-ttu-id="4627b-151">本教學課程提供預先佈建的值，您可以直接使用，完全不需要在自己的租用戶中佈建，就能看到可運作的範例。</span><span class="sxs-lookup"><span data-stu-id="4627b-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="4627b-152">不過，建議您執行這個步驟，並熟悉這個程序，因為當您建立自己的應用程式時，就需要這樣做。</span><span class="sxs-lookup"><span data-stu-id="4627b-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="4627b-153">Azure AD 只會發出權杖給已知的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627b-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="4627b-154">您必須先在租用戶中建立應用程式的項目，才能從應用程式使用 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="4627b-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="4627b-155">若要在您的租用戶中註冊新的應用程式：</span><span class="sxs-lookup"><span data-stu-id="4627b-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="4627b-156">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4627b-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4627b-157">在頂端列中，按一下您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4627b-157">On the top bar, click your account.</span></span> <span data-ttu-id="4627b-158">在 [目錄] 清單中，選擇您要註冊應用程式的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4627b-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="4627b-159">按一下左側窗格中的 [更多服務]，然後選取 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="4627b-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="4627b-160">按一下 [應用程式註冊]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4627b-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="4627b-161">遵照提示進行，並建立新的**原生用戶端應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4627b-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="4627b-162">(雖然 Cordova 應用程式是 HTML 架構，我們在此要建立的是原生用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627b-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="4627b-163">您必須選取 [原生用戶端應用程式] 選項，否則應用程式將無法運作。)</span><span class="sxs-lookup"><span data-stu-id="4627b-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="4627b-164">**名稱**向使用者描述您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627b-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="4627b-165">**重新導向 URI** 是用來將權杖傳回至您應用程式的 URI。</span><span class="sxs-lookup"><span data-stu-id="4627b-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="4627b-166">輸入 **http://MyDirectorySearcherApp**。</span><span class="sxs-lookup"><span data-stu-id="4627b-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="4627b-167">完成註冊之後，Azure AD 會指派唯一的應用程式識別碼給您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627b-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="4627b-168">您在後續章節中將會用到這個值。</span><span class="sxs-lookup"><span data-stu-id="4627b-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="4627b-169">您可以在新建立之應用程式的應用程式索引標籤中找到此值。</span><span class="sxs-lookup"><span data-stu-id="4627b-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="4627b-170">為了執行 `DirSearchClient Sample`，請為新建立的應用程式授與可查詢 Azure AD 圖形 API 的權限：</span><span class="sxs-lookup"><span data-stu-id="4627b-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="4627b-171">在 [設定] 頁面中，選取 [必要的權限]，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4627b-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="4627b-172">針對 Azure Active Directory 應用程式，選取 [Microsoft Graph] 作為 API，然後在 [委派權限] 底下新增 [以登入使用者的身分存取目錄] 權限。</span><span class="sxs-lookup"><span data-stu-id="4627b-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="4627b-173">這樣做可讓您的應用程式查詢圖形 API 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4627b-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="4627b-174">步驟 2︰複製範例應用程式存放庫</span><span class="sxs-lookup"><span data-stu-id="4627b-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="4627b-175">從 Shell 或命令列，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="4627b-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="4627b-176">步驟 3：建立 Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="4627b-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="4627b-177">有多種方式可以建立 Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4627b-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="4627b-178">在本教學課程中，我們使用 Cordova 命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="4627b-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="4627b-179">從 Shell 或命令列，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="4627b-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="4627b-180">這個命令會建立 Cordova 專案的資料夾結構和架構。</span><span class="sxs-lookup"><span data-stu-id="4627b-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="4627b-181">移至新的 DirSearchClient 資料夾：</span><span class="sxs-lookup"><span data-stu-id="4627b-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="4627b-182">使用檔案管理員或在您的殼層中使用下列命令，將入門專案的內容複製到 www 子資料夾中：</span><span class="sxs-lookup"><span data-stu-id="4627b-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="4627b-183">Windows：`xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="4627b-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="4627b-184">Mac：`cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="4627b-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="4627b-185">新增白名單外掛程式。</span><span class="sxs-lookup"><span data-stu-id="4627b-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="4627b-186">這是叫用圖形 API 所需的。</span><span class="sxs-lookup"><span data-stu-id="4627b-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="4627b-187">新增所有您想要支援的平台。</span><span class="sxs-lookup"><span data-stu-id="4627b-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="4627b-188">您至少必須執行下列其中一個命令，才能讓範例運作。</span><span class="sxs-lookup"><span data-stu-id="4627b-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="4627b-189">請注意，您無法在 Windows 上模擬 iOS，或在 Mac 上模擬 Windows。</span><span class="sxs-lookup"><span data-stu-id="4627b-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="4627b-190">將 ADAL for Cordova 外掛程式新增至您的專案：</span><span class="sxs-lookup"><span data-stu-id="4627b-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="4627b-191">步驟 4︰新增用以驗證使用者的程式碼，並從 AAD 取得權杖</span><span class="sxs-lookup"><span data-stu-id="4627b-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="4627b-192">在本教學課程，您正在開發的應用程式將提供簡單的目錄搜尋功能。</span><span class="sxs-lookup"><span data-stu-id="4627b-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="4627b-193">然後使用者可以在目錄中輸入任何使用者的別名，並以視覺化方式檢視一些基本的屬性。</span><span class="sxs-lookup"><span data-stu-id="4627b-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="4627b-194">入門專案包含應用程式基本使用者介面的定義 (在 www/index.html 中)，也包含串連基本應用程式事件系列的架構、使用者介面繫結及結果顯示邏輯 (在 www/js/index.js 中)。</span><span class="sxs-lookup"><span data-stu-id="4627b-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="4627b-195">您剩下的工作只是加入實作識別工作的邏輯。</span><span class="sxs-lookup"><span data-stu-id="4627b-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="4627b-196">您所要做的第一件事是在程式碼中加入通訊協定值，供 AAD 用於識別您的應用程式和您的目標資源。</span><span class="sxs-lookup"><span data-stu-id="4627b-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="4627b-197">稍後會使用這些值來建構權杖要求。</span><span class="sxs-lookup"><span data-stu-id="4627b-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="4627b-198">在 Index.js 檔案最上方插入下面程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="4627b-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="4627b-199">`redirectUri` 和 `clientId` 值應該符合 Azure AD 中用於描述您的應用程式的值。</span><span class="sxs-lookup"><span data-stu-id="4627b-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="4627b-200">您可以從 Azure 入口網站的 [設定] 索引標籤中找到這些值，如稍早在本教學課程的步驟 1 所述。</span><span class="sxs-lookup"><span data-stu-id="4627b-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="4627b-201">如果您選擇不在您自己的租用戶中註冊新的應用程式，您可以直接貼上預先設定的值。</span><span class="sxs-lookup"><span data-stu-id="4627b-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="4627b-202">然後您會看到範例在執行，但您仍應該為您打算實際執行的應用程式建立您自己的項目。</span><span class="sxs-lookup"><span data-stu-id="4627b-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="4627b-203">接下來，新增權杖要求程式碼。</span><span class="sxs-lookup"><span data-stu-id="4627b-203">Next, add the token request code.</span></span> <span data-ttu-id="4627b-204">在 `search` 和 `renderData` 定義之間插入下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="4627b-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="4627b-205">讓我們將該函式分成兩個主要部分來檢查一下。</span><span class="sxs-lookup"><span data-stu-id="4627b-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="4627b-206">此範例設計成可搭配任何租用戶，不受限於特定的租用戶。</span><span class="sxs-lookup"><span data-stu-id="4627b-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="4627b-207">它使用 "/common" 端點，可讓使用者在驗證時輸入任何帳戶，而且會將要求導向其所屬的租用戶。</span><span class="sxs-lookup"><span data-stu-id="4627b-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="4627b-208">此方法的第一部分會檢查 ADAL 快取，查看是否已儲存權杖。</span><span class="sxs-lookup"><span data-stu-id="4627b-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="4627b-209">如果是，此方法會使用權杖的來源租用戶，用來重新初始化 ADAL。</span><span class="sxs-lookup"><span data-stu-id="4627b-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="4627b-210">這是為了避免額外提示而必須執行的動作，因為使用 "/common" 永遠會導致要求使用者輸入新的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4627b-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="4627b-211">此方法的第二個部分會執行適當的權杖要求。</span><span class="sxs-lookup"><span data-stu-id="4627b-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="4627b-212">`acquireTokenSilentAsync` 方法會要求 ADAL 傳回指定資源的權杖，而不會顯示任何 UX。</span><span class="sxs-lookup"><span data-stu-id="4627b-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="4627b-213">如果快取中已儲存適當的存取權杖，或者如果有重新整理權杖可用來取得新的存取權杖，而不會顯示任何提示，就會發生此情況。</span><span class="sxs-lookup"><span data-stu-id="4627b-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="4627b-214">若這個做法失敗，我們就退回到 `acquireTokenAsync` -- 明顯提示使用者進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4627b-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="4627b-215">既然已取得權杖，我們終於可以叫用圖形 API，並執行我們想要的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="4627b-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="4627b-216">在 `authenticate` 定義下方，插入下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="4627b-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
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
<span data-ttu-id="4627b-217">起始點檔案提供簡易型 UX，可在文字方塊中輸入使用者的別名。</span><span class="sxs-lookup"><span data-stu-id="4627b-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="4627b-218">這個方法會使用該值來建構查詢、將它與存取權杖結合、將它傳送到 Microsoft Graph，然後剖析結果。</span><span class="sxs-lookup"><span data-stu-id="4627b-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="4627b-219">起始點檔案中已存在的 `renderData` 方法會負責呈現結果。</span><span class="sxs-lookup"><span data-stu-id="4627b-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="4627b-220">步驟 5：執行應用程式</span><span class="sxs-lookup"><span data-stu-id="4627b-220">Step 5: Run the app</span></span>
<span data-ttu-id="4627b-221">終於可以開始執行您的應用程式了。</span><span class="sxs-lookup"><span data-stu-id="4627b-221">Your app is finally ready to run.</span></span> <span data-ttu-id="4627b-222">操作很簡單：啟動應用程式後，輸入您要查閱的使用者的別名，然後按一下按鈕。</span><span class="sxs-lookup"><span data-stu-id="4627b-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="4627b-223">系統會提示您進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4627b-223">You're prompted for authentication.</span></span> <span data-ttu-id="4627b-224">在成功驗證和成功搜尋之後，將會顯示搜尋到的使用者的屬性。</span><span class="sxs-lookup"><span data-stu-id="4627b-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="4627b-225">後續執行只會執行搜尋，不會顯示任何提示，因為先前取得的權杖已存在於快取中。</span><span class="sxs-lookup"><span data-stu-id="4627b-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="4627b-226">執行應用程式的具體步驟隨著平台而不同。</span><span class="sxs-lookup"><span data-stu-id="4627b-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="4627b-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="4627b-227">Windows 10</span></span>
   <span data-ttu-id="4627b-228">平板電腦/PC： `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="4627b-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="4627b-229">行動裝置 (需要連線至 PC 的 Windows10 行動裝置)︰`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="4627b-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="4627b-230">第一次執行期間可能會要求您登入，以取得開發人員授權。</span><span class="sxs-lookup"><span data-stu-id="4627b-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="4627b-231">如需詳細資訊，請參閱[開發人員授權](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4627b-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="4627b-232">Windows 8.1 平板電腦/PC</span><span class="sxs-lookup"><span data-stu-id="4627b-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="4627b-233">第一次執行期間可能會要求您登入，以取得開發人員授權。</span><span class="sxs-lookup"><span data-stu-id="4627b-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="4627b-234">如需詳細資訊，請參閱[開發人員授權](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4627b-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="4627b-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="4627b-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="4627b-236">在已連線的裝置上執行：`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="4627b-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="4627b-237">在預設模擬器上執行：`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="4627b-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="4627b-238">使用 `cordova run windows --list -- --phone` 查看所有可用的目標，使用 `cordova run windows --target=<target_name> -- --phone` 在特定裝置或模擬器上執行應用程式 (例如，`cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`)。</span><span class="sxs-lookup"><span data-stu-id="4627b-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="4627b-239">Android</span><span class="sxs-lookup"><span data-stu-id="4627b-239">Android</span></span>
   <span data-ttu-id="4627b-240">在已連線的裝置上執行：`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="4627b-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="4627b-241">在預設模擬器上執行：`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="4627b-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="4627b-242">請確定您已如稍早＜必要條件＞一節所述，使用 AVD Manager 建立模擬器執行個體。</span><span class="sxs-lookup"><span data-stu-id="4627b-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="4627b-243">使用 `cordova run android --list` 查看所有可用的目標，使用 `cordova run android --target=<target_name>` 在特定裝置或模擬器上執行應用程式 (例如，`cordova run android --target="Nexus4_emulator"`)。</span><span class="sxs-lookup"><span data-stu-id="4627b-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="4627b-244">iOS</span><span class="sxs-lookup"><span data-stu-id="4627b-244">iOS</span></span>
   <span data-ttu-id="4627b-245">在已連線的裝置上執行：`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="4627b-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="4627b-246">在預設模擬器上執行：`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="4627b-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="4627b-247">請確定您已安裝要在模擬器上執行的 `ios-sim` 套件。</span><span class="sxs-lookup"><span data-stu-id="4627b-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="4627b-248">如需詳細資訊，請參閱＜必要條件＞一節。</span><span class="sxs-lookup"><span data-stu-id="4627b-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="4627b-249">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4627b-249">Next steps</span></span>
<span data-ttu-id="4627b-250">[GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient) 中有完整的範例供您參考 (不含您的組態值)。</span><span class="sxs-lookup"><span data-stu-id="4627b-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="4627b-251">您現在可以進入更進階 (且更有趣) 的案例。</span><span class="sxs-lookup"><span data-stu-id="4627b-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="4627b-252">您可以嘗試：[使用 Azure AD 保護 Node.js Web API](active-directory-devquickstarts-webapi-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="4627b-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
