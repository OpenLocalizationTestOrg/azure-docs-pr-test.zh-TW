---
title: "開始使用 Azure Mobile Engagement for Cordova/Phonegap"
description: "了解如何使用 Cordova/Phonegap 應用程式的 Azure Mobile Engagement 與分析和推播通知。"
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
ms.openlocfilehash: d7a761310782faab1dda023785f93cf90742e2ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="2ae93-103">開始使用 Azure Mobile Engagement for Cordova/Phonegap</span><span class="sxs-lookup"><span data-stu-id="2ae93-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="2ae93-104">此主題說明如何使用 Azure Mobile Engagement 了解您的應用程式使用狀況，以及傳送推播通知給以 Cordova 開發之行動應用程式的特定使用者。</span><span class="sxs-lookup"><span data-stu-id="2ae93-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="2ae93-105">在本教學課程中，我們將會使用 Mac 建立空白的 Cordova 應用程式，然後整合 Mobile Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="2ae93-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="2ae93-106">它會收集基本分析資料，並針對 iOS 使用 Apple Push Notification System (APNS)、針對 Android 使用 Google Cloud Messaging (GCM) 接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="2ae93-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="2ae93-107">我們會將它部署到 iOS 或 Android 裝置以進行測試。</span><span class="sxs-lookup"><span data-stu-id="2ae93-107">We will deploy this to an iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="2ae93-108">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ae93-108">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2ae93-109">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2ae93-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2ae93-110">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started)。</span><span class="sxs-lookup"><span data-stu-id="2ae93-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="2ae93-111">本教學課程需要下列各項：</span><span class="sxs-lookup"><span data-stu-id="2ae93-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="2ae93-112">XCode，您可以從您的 Mac App Store 安裝 (適用於部署到 iOS)</span><span class="sxs-lookup"><span data-stu-id="2ae93-112">XCode, which you can install from Mac App Store (for deploying to iOS)</span></span>
* <span data-ttu-id="2ae93-113">[Android SDK 和模擬器](http://developer.android.com/sdk/installing/index.html) (適用於部署到 Android)</span><span class="sxs-lookup"><span data-stu-id="2ae93-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying to Android)</span></span>
* <span data-ttu-id="2ae93-114">推播通知憑證 (.p12)，您可以在 Apple Dev Center for APNS 取得</span><span class="sxs-lookup"><span data-stu-id="2ae93-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="2ae93-115">您可以從您的 Google Developer Console for GCM 取得的 GCM 專案編號</span><span class="sxs-lookup"><span data-stu-id="2ae93-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="2ae93-116">Mobile Engagement Cordova 外掛程式</span><span class="sxs-lookup"><span data-stu-id="2ae93-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="2ae93-117">您可以在 [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova) 上找到原始程式碼和 ReadMe for the Cordova 外掛程式</span><span class="sxs-lookup"><span data-stu-id="2ae93-117">You can find the source code and the ReadMe for the Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="2ae93-118"><a id="setup-azme"></a>為您的 Cordova App 設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2ae93-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="2ae93-119"><a id="connecting-app"></a>將您的應用程式連接至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="2ae93-119"><a id="connecting-app"></a>Connecting your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="2ae93-120">本教學課程將說明「基本整合」，這是收集資料及傳送推播通知時必要的最低設定。</span><span class="sxs-lookup"><span data-stu-id="2ae93-120">This tutorial presents a "basic integration" which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="2ae93-121">我們將會使用 Cordova 建立基本應用程式來示範整合：</span><span class="sxs-lookup"><span data-stu-id="2ae93-121">We will create a basic app with Cordova to demonstrate the integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="2ae93-122">建立新的 Cordova 專案</span><span class="sxs-lookup"><span data-stu-id="2ae93-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="2ae93-123">啟動 Mac 電腦上的 *Terminal* 視窗，並輸入下列內容，其將會從預設範本中建立新的 Cordova 專案。</span><span class="sxs-lookup"><span data-stu-id="2ae93-123">Launch *Terminal* window on your Mac machine and type the following which will create a new Cordova project from the default template.</span></span> <span data-ttu-id="2ae93-124">請確定您最後用來部署您的 iOS 應用程式的發行設定檔是使用 'com.mycompany.myapp' 做為應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="2ae93-124">Make sure that the publishing profile you eventually use to deploy your iOS app is using 'com.mycompany.myapp' as the App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="2ae93-125">執行下列動作來設定 **iOS** 的專案，並在 iOS 模擬器中執行它：</span><span class="sxs-lookup"><span data-stu-id="2ae93-125">Execute the following to configure your project for **iOS** and run it in the iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="2ae93-126">執行下列命令來設定您的 **Android** 專案，並在 Android 模擬器中執行它。</span><span class="sxs-lookup"><span data-stu-id="2ae93-126">Execute the following to configure your project for **Android** and run it in the Android emulator.</span></span> <span data-ttu-id="2ae93-127">在您的 Android SDK 模擬器設定中，請確定目標為 Google API (Google Inc.)，而 CPU / ABI 為 Google API ARM。</span><span class="sxs-lookup"><span data-stu-id="2ae93-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with the CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="2ae93-128">新增 Cordova 主控台外掛程式。</span><span class="sxs-lookup"><span data-stu-id="2ae93-128">Add the Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="2ae93-129">將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="2ae93-129">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="2ae93-130">安裝 Azure Mobile Engagement Cordova 外掛程式，同時提供變數值以設定外掛程式：</span><span class="sxs-lookup"><span data-stu-id="2ae93-130">Install the Azure Mobile Engagement Cordova plugin while providing the variable values to configure the plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers the app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="2ae93-131">*Android 觸達圖示* ：必須是不含任何副檔名的資源名稱，也不含可繪製的前置詞 (例如：mynotificationicon)，而且必須將圖示檔複製到您的 android 專案 (platforms/android/res/drawable)</span><span class="sxs-lookup"><span data-stu-id="2ae93-131">*Android Reach Icon* : must be the name of the resource without any extension, nor drawable prefix (ex: mynotificationicon), and the icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="2ae93-132">*iOS 觸達圖示*：必須是具有副檔名的資源名稱 (例如：mynotificationicon.png)，而且必須將圖示檔新增到含有 XCode 的 iOS 專案 (使用 [新增檔案] 功能表)</span><span class="sxs-lookup"><span data-stu-id="2ae93-132">*iOS Reach Icon*  : must be the name of the resource with its extension (ex:  mynotificationicon.png), and the icon file must be added into your iOS project with XCode (using the Add Files Menu)</span></span>

## <span data-ttu-id="2ae93-133"><a id="monitor"></a>啟用即時監視</span><span class="sxs-lookup"><span data-stu-id="2ae93-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="2ae93-134">在 Cordova 專案中，編輯 **www/js/index.js** ，將呼叫加入至 Mobile Engagement，以便在收到 *deviceReady* 事件之後宣告新活動。</span><span class="sxs-lookup"><span data-stu-id="2ae93-134">In the Cordova project - edit **www/js/index.js** to add the call to Mobile Engagement to declare a new activity once the *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="2ae93-135">執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="2ae93-135">Run the application:</span></span>
   
   * <span data-ttu-id="2ae93-136">**對於 iOS**</span><span class="sxs-lookup"><span data-stu-id="2ae93-136">**For iOS**</span></span>
     
       <span data-ttu-id="2ae93-137">藉由執行下列動作，在 `Terminal` 視窗的新模擬器執行個體中啟動您的 App：</span><span class="sxs-lookup"><span data-stu-id="2ae93-137">In `Terminal` window launch your app in a new Simulator instance by executing the following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="2ae93-138">**對於 Android**</span><span class="sxs-lookup"><span data-stu-id="2ae93-138">**For Android**</span></span>
     
       <span data-ttu-id="2ae93-139">藉由執行下列動作，在 `Terminal` 視窗的新模擬器執行個體中啟動您的 App：</span><span class="sxs-lookup"><span data-stu-id="2ae93-139">In `Terminal` window launch your app in a new emulator instance by executing the following:</span></span>
     
           cordova run android
3. <span data-ttu-id="2ae93-140">您可以在主控台記錄檔中看到下列項目：</span><span class="sxs-lookup"><span data-stu-id="2ae93-140">You can see the following in the console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="2ae93-141"><a id="monitor"></a>將 App 與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="2ae93-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="2ae93-142"><a id="integrate-push"></a>啟用推播通知與應用程式內傳訊</span><span class="sxs-lookup"><span data-stu-id="2ae93-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="2ae93-143">Mobile Engagement 可讓您使用「推播通知」和「應用程式內傳訊」，於活動進行時與使用者互動。</span><span class="sxs-lookup"><span data-stu-id="2ae93-143">Mobile Engagement allows you to interact with your users using Push Notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="2ae93-144">此模組在 Mobile Engagement 入口網站中稱為觸達 (REACH)。</span><span class="sxs-lookup"><span data-stu-id="2ae93-144">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="2ae93-145">以下各節將設定您的應用程式來接收它們。</span><span class="sxs-lookup"><span data-stu-id="2ae93-145">The following sections will setup your app to receive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="2ae93-146">設定 Mobile Engagement 的推播認證</span><span class="sxs-lookup"><span data-stu-id="2ae93-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="2ae93-147">若要讓 Mobile Engagement 以您的名義傳送推播通知，您需要授與它對您的 Apple iOS 憑證或 GCM Server API 金鑰的存取權。</span><span class="sxs-lookup"><span data-stu-id="2ae93-147">To allow Mobile Engagement to send Push Notifications on your behalf, you need to grant it access to your Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="2ae93-148">瀏覽至您的 Mobile Engagement 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2ae93-148">Navigate to your Mobile Engagement portal.</span></span> <span data-ttu-id="2ae93-149">確認您正位在用於此專案的 App 內，然後按一下底部的 [接洽]  按鈕：</span><span class="sxs-lookup"><span data-stu-id="2ae93-149">Ensure you're in the app we're using for this project and then click on the **Engage** button at the bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="2ae93-150">您將登陸在 Engagement 入口網站的 [設定] 頁面中。</span><span class="sxs-lookup"><span data-stu-id="2ae93-150">You will land in the settings page in your Engagement Portal.</span></span> <span data-ttu-id="2ae93-151">在該處按一下 [原生推送]  區段：</span><span class="sxs-lookup"><span data-stu-id="2ae93-151">From there click on the **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="2ae93-152">設定 iOS 憑證/GCM Server API 金鑰</span><span class="sxs-lookup"><span data-stu-id="2ae93-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="2ae93-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="2ae93-153">**[iOS]**</span></span>
   
    <span data-ttu-id="2ae93-154">a.</span><span class="sxs-lookup"><span data-stu-id="2ae93-154">a.</span></span> <span data-ttu-id="2ae93-155">選取您的 .p12、將它上傳並輸入您的密碼：</span><span class="sxs-lookup"><span data-stu-id="2ae93-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="2ae93-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="2ae93-156">**[Android]**</span></span>
   
    <span data-ttu-id="2ae93-157">a.</span><span class="sxs-lookup"><span data-stu-id="2ae93-157">a.</span></span> <span data-ttu-id="2ae93-158">在 [GCM 設定] 區段中按一下 [API 金鑰] 前面的編輯圖示，並在出現的快顯視窗中貼上 GCM 伺服器金鑰，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2ae93-158">Click the edit icon in front of **API Key** in the GCM Settings section and in the popup which shows up, paste the GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-the-cordova-app"></a><span data-ttu-id="2ae93-159">在 Cordova 應用程式中啟用推播通知</span><span class="sxs-lookup"><span data-stu-id="2ae93-159">Enable push notifications in the Cordova app</span></span>
<span data-ttu-id="2ae93-160">編輯 **www/js/index.js** ，將呼叫加入至 Mobile Engagement 以要求推播通知，並宣告處理常式：</span><span class="sxs-lookup"><span data-stu-id="2ae93-160">Edit **www/js/index.js** to add the call to Mobile Engagement to request push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-the-app"></a><span data-ttu-id="2ae93-161">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="2ae93-161">Run the app</span></span>
<span data-ttu-id="2ae93-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="2ae93-162">**[iOS]**</span></span>

1. <span data-ttu-id="2ae93-163">我們將使用 XCode 在裝置上建置及部署應用程式，以測試推播通知，因為 iOS 只允許推播通知到實際裝置。</span><span class="sxs-lookup"><span data-stu-id="2ae93-163">We will use XCode to build and deploy the app on the device to test push notifications since iOS only allows push notifications to an actual device.</span></span> <span data-ttu-id="2ae93-164">移至您建立 Cordova 專案的位置，然後瀏覽至 **...\platforms\ios** 位置。</span><span class="sxs-lookup"><span data-stu-id="2ae93-164">Go to the location where your Cordova project is created and navigate to **...\platforms\ios** location.</span></span> <span data-ttu-id="2ae93-165">在 XCode 中開啟原生 .xcodeproj 檔案。</span><span class="sxs-lookup"><span data-stu-id="2ae93-165">Open up the native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="2ae93-166">建置 Cordova 應用程式並部署至 iOS 裝置，方法是使用具有佈建設定檔的帳戶，該設定檔包含憑證 (您剛剛上傳至 Mobile Engagement 入口網站) 和應用程式識別碼 (符合您在建立 Cordova 應用程式時提供的識別碼)。</span><span class="sxs-lookup"><span data-stu-id="2ae93-166">Build and deploy the Cordova app to the iOS device using the account which has the provisioning profile containing the certificate you just uploaded to the Mobile Engagement portal and the App Id which matches the one you provided while creating the Cordova app.</span></span> <span data-ttu-id="2ae93-167">您可以在 XCode 的 **Resources\*-info.plist** 檔案中檢查「套件組合識別碼」來進行配對。</span><span class="sxs-lookup"><span data-stu-id="2ae93-167">You can check out the *Bundle identifier* in your **Resources\*-info.plist** file in XCode to match it up.</span></span> 
3. <span data-ttu-id="2ae93-168">您會在您的裝置上看到標準 iOS 快顯視窗，上面顯示應用程式要求傳送通知的權限。</span><span class="sxs-lookup"><span data-stu-id="2ae93-168">You will see the standard iOS popup on your device saying that the app requests permission to send notifications.</span></span> <span data-ttu-id="2ae93-169">授與權限。</span><span class="sxs-lookup"><span data-stu-id="2ae93-169">Grant the permission.</span></span> 

<span data-ttu-id="2ae93-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="2ae93-170">**[Android]**</span></span>

<span data-ttu-id="2ae93-171">您只能使用模擬器執行 Android 應用程式，因為 GCM 通知只在 Android 模擬器上受到支援。</span><span class="sxs-lookup"><span data-stu-id="2ae93-171">You can simply use the emulator to run the Android app as GCM notifications are supported on the Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="2ae93-172"><a id="send"></a>傳送通知至應用程式</span><span class="sxs-lookup"><span data-stu-id="2ae93-172"><a id="send"></a>Send a notification to your app</span></span>
<span data-ttu-id="2ae93-173">現在，我們將建立簡單的推播通知行銷活動，它會傳送推播到裝置上執行中的應用程式：</span><span class="sxs-lookup"><span data-stu-id="2ae93-173">We will now create a simple Push Notification campaign that will send a push to your app running on the device:</span></span>

1. <span data-ttu-id="2ae93-174">瀏覽至您的 Mobile Engagement 入口網站中的 [觸達]  索引標籤</span><span class="sxs-lookup"><span data-stu-id="2ae93-174">Navigate to the **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="2ae93-175">按一下 [新增宣告]  來建立您的推播行銷活動</span><span class="sxs-lookup"><span data-stu-id="2ae93-175">Click **New Announcement** to create your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="2ae93-176">提供輸入來建立您的行銷活動 **[Android]**</span><span class="sxs-lookup"><span data-stu-id="2ae93-176">Provide inputs to create your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="2ae93-177">為您的行銷活動提供 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="2ae93-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="2ae93-178">針對 [傳遞類型] 選取 [系統通知] [簡易]</span><span class="sxs-lookup"><span data-stu-id="2ae93-178">Select the **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="2ae93-179">針對 [傳遞時間] 選取 [任何時間]</span><span class="sxs-lookup"><span data-stu-id="2ae93-179">Select the **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="2ae93-180">提供通知的 **標題** ，這將是推播中的第一行。</span><span class="sxs-lookup"><span data-stu-id="2ae93-180">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="2ae93-181">提供通知的 **訊息** ，這將做為訊息內文。</span><span class="sxs-lookup"><span data-stu-id="2ae93-181">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="2ae93-182">提供輸入來建立您的行銷活動 **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="2ae93-182">Provide inputs to create your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="2ae93-183">為您的行銷活動提供 **名稱** 。</span><span class="sxs-lookup"><span data-stu-id="2ae93-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="2ae93-184">針對 [傳遞時間] 選取 [僅限應用程式外]</span><span class="sxs-lookup"><span data-stu-id="2ae93-184">Select the **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="2ae93-185">提供通知的 **標題** ，這將是推播中的第一行。</span><span class="sxs-lookup"><span data-stu-id="2ae93-185">Provide a **Title** for your notification which will be the first line in the push.</span></span>
   * <span data-ttu-id="2ae93-186">提供通知的 **訊息** ，這將做為訊息內文。</span><span class="sxs-lookup"><span data-stu-id="2ae93-186">Provide a **Message** for your notification which will serve as the message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="2ae93-187">向下捲動，在 [內容] 區段中選取 [僅限通知] </span><span class="sxs-lookup"><span data-stu-id="2ae93-187">Scroll down, and in the content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="2ae93-188">[選用] 您也可以提供動作 URL。</span><span class="sxs-lookup"><span data-stu-id="2ae93-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="2ae93-189">請確定它會使用在設定外掛程式的 **AZME\_REDIRECT\_URL** 變數 (例如 *myapp://test*) 時提供的 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="2ae93-189">Make sure that it uses a URL scheme provided while configuring the plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="2ae93-190">您已完成能做的最基本活動設定。</span><span class="sxs-lookup"><span data-stu-id="2ae93-190">You're done setting the most basic campaign possible.</span></span> <span data-ttu-id="2ae93-191">現在再次向下捲動，並按一下 [建立]  按鈕來儲存行銷活動。</span><span class="sxs-lookup"><span data-stu-id="2ae93-191">Now scroll down again and click the **Create** button to save your campaign.</span></span>
8. <span data-ttu-id="2ae93-192">最後 **啟用** 您的行銷活動</span><span class="sxs-lookup"><span data-stu-id="2ae93-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="2ae93-193">您現在應該會在裝置或模擬器上看到推播通知，做為此行銷活動的一部分。</span><span class="sxs-lookup"><span data-stu-id="2ae93-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="2ae93-194"><a id="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="2ae93-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="2ae93-195">可用於 Cordova Mobile Engagement SDK 之所有方法的概觀</span><span class="sxs-lookup"><span data-stu-id="2ae93-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

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

