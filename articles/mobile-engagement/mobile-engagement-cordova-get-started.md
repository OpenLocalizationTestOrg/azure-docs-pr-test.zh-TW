---
title: "開始使用 Cordova/Phonegap 的 Azure Mobile Engagement aaaGet"
description: "深入了解如何 toouse 與分析及推播通知的 Azure Mobile Engagement Cordova/Phonegap 應用程式。"
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="e8dab-103">開始使用 Azure Mobile Engagement for Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="e8dab-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e8dab-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand cordova 開發應用程式使用方式及傳送推播通知 toosegmented 使用者的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8dab-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="e8dab-105">在本教學課程中，我們將會使用 Mac 建立空白的 Cordova 應用程式，然後整合 Mobile Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="e8dab-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="e8dab-106">它會收集基本分析資料，並針對 iOS 使用 Apple Push Notification System (APNS)、針對 Android 使用 Google Cloud Messaging (GCM) 接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="e8dab-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="e8dab-107">我們將會部署這個 tooan iOS 或 Android 裝置上的進行測試。</span><span class="sxs-lookup"><span data-stu-id="e8dab-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="e8dab-108">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8dab-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e8dab-109">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8dab-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e8dab-110">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started)。</span><span class="sxs-lookup"><span data-stu-id="e8dab-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="e8dab-111">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="e8dab-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="e8dab-112">您可以從 Mac App Store （適用於部署 tooiOS） 安裝 XCode</span><span class="sxs-lookup"><span data-stu-id="e8dab-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="e8dab-113">[Android SDK 及模擬器](http://developer.android.com/sdk/installing/index.html)（適用於部署 tooAndroid）</span><span class="sxs-lookup"><span data-stu-id="e8dab-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="e8dab-114">推播通知憑證 (.p12)，您可以在 Apple Dev Center for APNS 取得</span><span class="sxs-lookup"><span data-stu-id="e8dab-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="e8dab-115">您可以從您的 Google Developer Console for GCM 取得的 GCM 專案編號</span><span class="sxs-lookup"><span data-stu-id="e8dab-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="e8dab-116">Mobile Engagement Cordova 外掛程式</span><span class="sxs-lookup"><span data-stu-id="e8dab-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="e8dab-117">您可以尋找 hello 原始碼並在 hello Cordova 外掛程式 hello 讀我檔案[GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="e8dab-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="e8dab-118"><a id="setup-azme"></a>為您的 Cordova App 設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e8dab-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e8dab-119"><a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="e8dab-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="e8dab-120">此教學課程提供 < 基本整合 > hello 最小設定必要的 toocollect 資料及傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="e8dab-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="e8dab-121">我們將使用 Cordova toodemonstrate hello 整合，以建立基本應用程式：</span><span class="sxs-lookup"><span data-stu-id="e8dab-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="e8dab-122">建立新的 Cordova 專案</span><span class="sxs-lookup"><span data-stu-id="e8dab-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="e8dab-123">啟動*終端機*視窗上遵循這將會從 hello 預設範本來建立新的 Cordova 專案您 Mac 電腦，然後輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="e8dab-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="e8dab-124">請確定該 hello 發行設定檔，您最終使用 toodeploy iOS 應用程式使用 'com.mycompany.myapp' hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="e8dab-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="e8dab-125">執行下列 tooconfigure hello 專案**iOS**和 hello iOS 模擬器中執行它：</span><span class="sxs-lookup"><span data-stu-id="e8dab-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="e8dab-126">執行下列 tooconfigure hello 專案**Android**和 hello Android 模擬器中執行程式。</span><span class="sxs-lookup"><span data-stu-id="e8dab-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="e8dab-127">請確定您的 Android SDK 模擬器設定有其目標為 Google Api (Google Inc.) 與 hello CPU / ABI 為 Google Api ARM。</span><span class="sxs-lookup"><span data-stu-id="e8dab-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="e8dab-128">新增 hello Cordova 主控台外掛程式。</span><span class="sxs-lookup"><span data-stu-id="e8dab-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="e8dab-129">連接您的應用程式 tooMobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="e8dab-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="e8dab-130">同時提供 hello 變數值 tooconfigure hello 外掛程式安裝 hello Azure Mobile Engagement Cordova 外掛程式：</span><span class="sxs-lookup"><span data-stu-id="e8dab-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="e8dab-131">*Android 到達圖示*： 必須是不含任何擴充功能，也不 drawable 前置詞的 hello 資源 hello 名稱 (例如： mynotificationicon)，和 hello 圖示檔案必須複製到您的 android 專案 (平台/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="e8dab-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="e8dab-132">*iOS 到達圖示*： 必須是 hello hello 其副檔名的資源名稱 (ex: mynotificationicon.png)，和 hello 圖示檔必須加入至您的 iOS 專案，使用 XCode （使用 hello 加入 [檔案] 功能表）</span><span class="sxs-lookup"><span data-stu-id="e8dab-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="e8dab-133"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="e8dab-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="e8dab-134">在 [hello Cordova 專案-編輯**www/js/index.js** tooadd hello 呼叫一次 hello tooMobile Engagement toodeclare 新活動*deviceReady*在接收到事件。</span><span class="sxs-lookup"><span data-stu-id="e8dab-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="e8dab-135">執行 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="e8dab-135">Run hello application:</span></span>
   
   * <span data-ttu-id="e8dab-136">**對於 iOS**</span><span class="sxs-lookup"><span data-stu-id="e8dab-136">**For iOS**</span></span>
     
       <span data-ttu-id="e8dab-137">在`Terminal`視窗啟動新的模擬器執行個體中的應用程式藉由執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="e8dab-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="e8dab-138">**對於 Android**</span><span class="sxs-lookup"><span data-stu-id="e8dab-138">**For Android**</span></span>
     
       <span data-ttu-id="e8dab-139">在`Terminal`視窗啟動新的模擬器執行個體中的應用程式藉由執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="e8dab-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="e8dab-140">您可以看到 hello 主控台記錄檔中的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e8dab-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="e8dab-141"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="e8dab-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e8dab-142"><a id="integrate-push"></a>啟用推播通知與應用程式內傳訊</span><span class="sxs-lookup"><span data-stu-id="e8dab-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="e8dab-143">Mobile Engagement 可讓您 toointeract 與您使用推播通知及應用程式內訊息的活動 hello 內容中的使用者。</span><span class="sxs-lookup"><span data-stu-id="e8dab-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="e8dab-144">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="e8dab-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="e8dab-145">hello 下列各節將會安裝應用程式 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="e8dab-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="e8dab-146">設定 Mobile Engagement 的推播認證</span><span class="sxs-lookup"><span data-stu-id="e8dab-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="e8dab-147">tooallow Mobile Engagement toosend 推播通知您的身分，您需要 toogrant 它存取 tooyour Apple iOS 憑證或 GCM 伺服器 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e8dab-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="e8dab-148">瀏覽 tooyour Mobile Engagement 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e8dab-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="e8dab-149">請確定您在 hello 應用程式，我們正在使用此專案，然後按一下 [hello **Engage** hello 底部的按鈕：</span><span class="sxs-lookup"><span data-stu-id="e8dab-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="e8dab-150">在您 Engagement 入口網站中，您將登陸 hello 設定] 頁面中。</span><span class="sxs-lookup"><span data-stu-id="e8dab-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="e8dab-151">從該處，按一下 [hello**原生推送**> 一節：</span><span class="sxs-lookup"><span data-stu-id="e8dab-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="e8dab-152">設定 iOS 憑證/GCM Server API 金鑰</span><span class="sxs-lookup"><span data-stu-id="e8dab-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="e8dab-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="e8dab-153">**[iOS]**</span></span>
   
    <span data-ttu-id="e8dab-154">a.</span><span class="sxs-lookup"><span data-stu-id="e8dab-154">a.</span></span> <span data-ttu-id="e8dab-155">選取您的 .p12、將它上傳並輸入您的密碼：</span><span class="sxs-lookup"><span data-stu-id="e8dab-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="e8dab-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="e8dab-156">**[Android]**</span></span>
   
    <span data-ttu-id="e8dab-157">a.</span><span class="sxs-lookup"><span data-stu-id="e8dab-157">a.</span></span> <span data-ttu-id="e8dab-158">按一下編輯 hello] 圖示的前面**API 金鑰**hello GCM 設定] 區段中，而且其中會顯示 hello 快顯視窗中，貼 hello GCM 伺服器金鑰，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e8dab-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="e8dab-159">啟用 hello Cordova 應用程式中的推播通知</span><span class="sxs-lookup"><span data-stu-id="e8dab-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="e8dab-160">編輯**www/js/index.js** tooadd hello 呼叫 tooMobile Engagement toorequest 推播通知，並宣告處理常式：</span><span class="sxs-lookup"><span data-stu-id="e8dab-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="e8dab-161">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e8dab-161">Run hello app</span></span>
<span data-ttu-id="e8dab-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="e8dab-162">**[iOS]**</span></span>

1. <span data-ttu-id="e8dab-163">我們將使用 XCode toobuild 和部署 hello hello 裝置 tootest 推播通知上的應用程式，因為 iOS 只允許推播通知 tooan 實際裝置。</span><span class="sxs-lookup"><span data-stu-id="e8dab-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="e8dab-164">請移 toohello 位置建立您的 Cordova 專案的位置，並瀏覽過**...\platforms\ios**位置。</span><span class="sxs-lookup"><span data-stu-id="e8dab-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="e8dab-165">Hello 原生的.xcodeproj 檔案，即可在 XCode 中開啟。</span><span class="sxs-lookup"><span data-stu-id="e8dab-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="e8dab-166">建置和部署的 hello Cordova 應用程式 toohello iOS 裝置使用有 hello 佈建設定檔將包含您剛剛上傳 toohello Mobile Engagement 入口網站和應用程式識別碼比對符合您在建立時所提供的其中一個 hello hello hello 憑證 hello 帳戶hello Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8dab-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="e8dab-167">您可以簽出 hello*配套識別碼*中您**資源\*-info.plist**檔案在 XCode toomatch 它註冊。</span><span class="sxs-lookup"><span data-stu-id="e8dab-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="e8dab-168">您會看見 hello 標準 iOS 快顯視窗指出該 hello 應用程式在裝置上的要求權限 toosend 通知。</span><span class="sxs-lookup"><span data-stu-id="e8dab-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="e8dab-169">授與 hello 權限。</span><span class="sxs-lookup"><span data-stu-id="e8dab-169">Grant hello permission.</span></span> 

<span data-ttu-id="e8dab-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="e8dab-170">**[Android]**</span></span>

<span data-ttu-id="e8dab-171">GCM 通知支援 hello Android 模擬器上時，您可以直接使用 hello 模擬器 toorun hello Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e8dab-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="e8dab-172"><a id="send"></a>傳送通知 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="e8dab-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="e8dab-173">現在，我們將建立簡單的推播通知活動將傳送嗨裝置上執行的推播 tooyour 應用程式：</span><span class="sxs-lookup"><span data-stu-id="e8dab-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="e8dab-174">瀏覽 toohello**到達**] 索引標籤中您的 Mobile Engagement 入口網站</span><span class="sxs-lookup"><span data-stu-id="e8dab-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="e8dab-175">按一下**新的 Announcement** toocreate 您的推播宣傳活動</span><span class="sxs-lookup"><span data-stu-id="e8dab-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="e8dab-176">您的活動提供輸入 toocreate **[Android]**</span><span class="sxs-lookup"><span data-stu-id="e8dab-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="e8dab-177">為您的行銷活動提供 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="e8dab-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="e8dab-178">選取 hello**傳遞類型**為*系統通知**簡單*</span><span class="sxs-lookup"><span data-stu-id="e8dab-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="e8dab-179">選取 hello**傳遞時間**為*「 任何時間 」*</span><span class="sxs-lookup"><span data-stu-id="e8dab-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="e8dab-180">提供**標題**您為 hello 第一行 hello 推播通知。</span><span class="sxs-lookup"><span data-stu-id="e8dab-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="e8dab-181">提供**訊息**針對您要做為 hello 訊息內文的通知。</span><span class="sxs-lookup"><span data-stu-id="e8dab-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="e8dab-182">您的活動提供輸入 toocreate **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="e8dab-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="e8dab-183">為您的行銷活動提供 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="e8dab-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="e8dab-184">選取 hello**傳遞時間**為*「 不足應用程式只"*</span><span class="sxs-lookup"><span data-stu-id="e8dab-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="e8dab-185">提供**標題**您為 hello 第一行 hello 推播通知。</span><span class="sxs-lookup"><span data-stu-id="e8dab-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="e8dab-186">提供**訊息**針對您要做為 hello 訊息內文的通知。</span><span class="sxs-lookup"><span data-stu-id="e8dab-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="e8dab-187">向下捲動，並在 hello 內容區段選取**僅限通知**</span><span class="sxs-lookup"><span data-stu-id="e8dab-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="e8dab-188">[選用] 您也可以提供動作 URL。</span><span class="sxs-lookup"><span data-stu-id="e8dab-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="e8dab-189">請確定它會使用設定 hello 外掛程式時，提供的 URL 配置**AZME\_重新導向\_URL**變數例如*myapp://test*。</span><span class="sxs-lookup"><span data-stu-id="e8dab-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="e8dab-190">您已完成設定 hello 最基本活動可能。</span><span class="sxs-lookup"><span data-stu-id="e8dab-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="e8dab-191">現在，向下捲動並按一下 hello**建立**按鈕 toosave 您的活動。</span><span class="sxs-lookup"><span data-stu-id="e8dab-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="e8dab-192">最後 **啟用** 您的行銷活動</span><span class="sxs-lookup"><span data-stu-id="e8dab-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="e8dab-193">您現在應該會在裝置或模擬器上看到推播通知，做為此行銷活動的一部分。</span><span class="sxs-lookup"><span data-stu-id="e8dab-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="e8dab-194"><a id="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8dab-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="e8dab-195">可用於 Cordova Mobile Engagement SDK 之所有方法的概觀</span><span class="sxs-lookup"><span data-stu-id="e8dab-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

