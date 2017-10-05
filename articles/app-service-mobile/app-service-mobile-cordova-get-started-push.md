---
title: "使用 Azure Mobile Apps 將推播通知新增至 Apache Cordova 應用程式| Microsoft Docs"
description: "了解如何使用 Azure Mobile Apps 將推播通知傳送至 Apache Cordova 應用程式。"
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: dc3cab0a6a8b4a56ab0fba1a02e5bba9d0ed1b1f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-apache-cordova-app"></a><span data-ttu-id="f791f-103">新增推播通知至您的 Apache Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="f791f-103">Add push notifications to your Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="f791f-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f791f-104">Overview</span></span>
<span data-ttu-id="f791f-105">在本教學課程中，您會將推播通知新增至 [Apache Cordova 快速入門] 專案，以便在每次插入一筆記錄時，將推播通知傳送至裝置。</span><span class="sxs-lookup"><span data-stu-id="f791f-105">In this tutorial, you add push notifications to the [Apache Cordova quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="f791f-106">如果您不要使用下載的快速入門伺服器專案，則需要推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="f791f-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="f791f-107">如需詳細資訊，請參閱[使用適用於 Azure Mobile Apps 的 .NET 後端伺服器 SDK][1]。</span><span class="sxs-lookup"><span data-stu-id="f791f-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="f791f-108"><a name="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="f791f-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="f791f-109">本教學課程涵蓋使用 Visual Studio 2015 開發且在 Google Android 模擬器、Android 裝置、Windows 裝置和 iOS 裝置上執行的 Apache Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f791f-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on the Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="f791f-110">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="f791f-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="f791f-111">具有 [Visual Studio Community 2015][2] 或更新版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="f791f-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="f791f-112">[Visual Studio Tools for Apache Cordova][4]。</span><span class="sxs-lookup"><span data-stu-id="f791f-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="f791f-113">[作用中的 Azure 帳戶][3]。</span><span class="sxs-lookup"><span data-stu-id="f791f-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="f791f-114">已完成的 [Apache Cordova 快速入門][5] 專案。</span><span class="sxs-lookup"><span data-stu-id="f791f-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="f791f-115">(Android) 具有已驗證電子郵件地址的 [Google 帳戶][6]。</span><span class="sxs-lookup"><span data-stu-id="f791f-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="f791f-116">(iOS) [Apple Developer Program 成員資格][7]和 iOS 裝置 (iOS 模擬器不支援推播)。</span><span class="sxs-lookup"><span data-stu-id="f791f-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="f791f-117">(Windows) [Windows 市集開發人員帳戶][8]和 Windows 10 裝置。</span><span class="sxs-lookup"><span data-stu-id="f791f-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="f791f-118"><a name="configure-hub"></a>設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="f791f-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="f791f-119">[觀看示範本節步驟的視訊][9]</span><span class="sxs-lookup"><span data-stu-id="f791f-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-the-server-project"></a><span data-ttu-id="f791f-120">更新伺服器專案</span><span class="sxs-lookup"><span data-stu-id="f791f-120">Update the server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="f791f-121"><a name="add-push-to-app"></a>修改您的 Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="f791f-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="f791f-122">安裝 Cordova 推播外掛程式，還有平台特定的任何推播服務，確保您的 Apache Cordova 應用程式專案能夠處理推播通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-122">Ensure your Apache Cordova app project is ready to handle push notifications by installing the Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-the-cordova-version-in-your-project"></a><span data-ttu-id="f791f-123">更新您的專案中的 Cordova 版本。</span><span class="sxs-lookup"><span data-stu-id="f791f-123">Update the Cordova version in your project.</span></span>
<span data-ttu-id="f791f-124">如果您的專案使用 6.1.1 版以前的 Apache Cordova，請更新用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="f791f-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update the client project.</span></span> <span data-ttu-id="f791f-125">若要更新專案︰</span><span class="sxs-lookup"><span data-stu-id="f791f-125">To update the project:</span></span>

* <span data-ttu-id="f791f-126">以滑鼠右鍵按一下 `config.xml` 開啟組態設計工具。</span><span class="sxs-lookup"><span data-stu-id="f791f-126">Right-click `config.xml` to open the configuration designer.</span></span>
* <span data-ttu-id="f791f-127">選取 [平台] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="f791f-127">Select the Platforms tab.</span></span>
* <span data-ttu-id="f791f-128">在 [Cordova CLI] 文字方塊中選擇 6.1.1。</span><span class="sxs-lookup"><span data-stu-id="f791f-128">Choose 6.1.1 in the **Cordova CLI** text box.</span></span>
* <span data-ttu-id="f791f-129">依序選擇 [建置] 和 [建置方案] 來更新專案。</span><span class="sxs-lookup"><span data-stu-id="f791f-129">Choose **Build**, then **Build Solution** to update the project.</span></span>

#### <a name="install-the-push-plugin"></a><span data-ttu-id="f791f-130">安裝推播外掛程式</span><span class="sxs-lookup"><span data-stu-id="f791f-130">Install the push plugin</span></span>
<span data-ttu-id="f791f-131">Apache Cordova 應用程式原本就不會處理裝置或網路功能。</span><span class="sxs-lookup"><span data-stu-id="f791f-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="f791f-132">這些功能是由 [npm][10] 或 GitHub 上發佈的外掛程式所提供。</span><span class="sxs-lookup"><span data-stu-id="f791f-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="f791f-133">`phonegap-plugin-push` 外掛程式是用來處理網路推播通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-133">The `phonegap-plugin-push` plugin is used to handle network push notifications.</span></span>

<span data-ttu-id="f791f-134">您可透過下列其中一種方式安裝推撥外掛程式：</span><span class="sxs-lookup"><span data-stu-id="f791f-134">You can install the push plugin in one of these ways:</span></span>

<span data-ttu-id="f791f-135">**從命令提示：**</span><span class="sxs-lookup"><span data-stu-id="f791f-135">**From the command-prompt:**</span></span>

<span data-ttu-id="f791f-136">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="f791f-136">Execute the following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="f791f-137">**從 Visual Studio 內：**</span><span class="sxs-lookup"><span data-stu-id="f791f-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="f791f-138">在方案總管中開啟 `config.xml` 檔案，按一下 [外掛程式] > [自訂]，選取 [Git] 作為安裝來源，然後輸入 `https://github.com/phonegap/phonegap-plugin-push` 作為來源。</span><span class="sxs-lookup"><span data-stu-id="f791f-138">In Solution Explorer, open the `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as the source.</span></span>

   ![][img1]

2. <span data-ttu-id="f791f-139">按一下安裝來源旁邊的箭頭。</span><span class="sxs-lookup"><span data-stu-id="f791f-139">Click the arrow next to the installation source.</span></span>
3. <span data-ttu-id="f791f-140">在 **SENDER_ID** 中，如果您已經有 Google 開發人員主控台專案的數值專案識別碼，您可以在此將它新增。</span><span class="sxs-lookup"><span data-stu-id="f791f-140">In **SENDER_ID**, if you already have a numeric project ID for the Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="f791f-141">否則，請輸入預留位置值，例如 777777。</span><span class="sxs-lookup"><span data-stu-id="f791f-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="f791f-142">如果您是以 Android 為目標，您可以稍後在 config.xml 中更新此值。</span><span class="sxs-lookup"><span data-stu-id="f791f-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="f791f-143">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="f791f-143">Click **Add**.</span></span>

<span data-ttu-id="f791f-144">推撥外掛程式現已安裝。</span><span class="sxs-lookup"><span data-stu-id="f791f-144">The push plugin is now installed.</span></span>

#### <a name="install-the-device-plugin"></a><span data-ttu-id="f791f-145">安裝裝置外掛程式</span><span class="sxs-lookup"><span data-stu-id="f791f-145">Install the device plugin</span></span>
<span data-ttu-id="f791f-146">遵循您安裝推播外掛程式時的相同程序。</span><span class="sxs-lookup"><span data-stu-id="f791f-146">Follow the same procedure you used to install the push plugin.</span></span>  <span data-ttu-id="f791f-147">從核心外掛程式清單中新增裝置外掛程式 (按一下 [外掛程式] > [核心]找到它)。</span><span class="sxs-lookup"><span data-stu-id="f791f-147">Add the Device plugin from the Core plugins list (click **Plugins** > **Core** to find it).</span></span> <span data-ttu-id="f791f-148">您需要此外掛程式才能取得平台名稱。</span><span class="sxs-lookup"><span data-stu-id="f791f-148">You need this plugin to obtain the platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="f791f-149">在應用程式啟動時註冊您的裝置</span><span class="sxs-lookup"><span data-stu-id="f791f-149">Register your device on application start-up</span></span>
<span data-ttu-id="f791f-150">最初，我們包含一些適用於 Android 的最少程式碼。</span><span class="sxs-lookup"><span data-stu-id="f791f-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="f791f-151">之後，將應用程式修改為在 iOS 或 Windows 10 上執行。</span><span class="sxs-lookup"><span data-stu-id="f791f-151">Later, modify the app to run on iOS or Windows 10.</span></span>

1. <span data-ttu-id="f791f-152">在登入程序的回呼期間或在 **onDeviceReady** 方法的底部，新增 **registerForPushNotifications** 的呼叫：</span><span class="sxs-lookup"><span data-stu-id="f791f-152">Add a call to **registerForPushNotifications** during the callback for the login process, or at the bottom of  the **onDeviceReady** method:</span></span>

        // Login to the service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh the todoItems
                refreshDisplay();

                // Wire up the UI Event Handler for the Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added to register for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="f791f-153">這個範例示範在成功驗證之後呼叫 **registerForPushNotifications**。</span><span class="sxs-lookup"><span data-stu-id="f791f-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="f791f-154">您可以依需要經常呼叫 `registerForPushNotifications()`。</span><span class="sxs-lookup"><span data-stu-id="f791f-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="f791f-155">加入新的 **registerForPushNotifications** 方法，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f791f-155">Add the new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle the registration event.
        pushRegistration.on('registration', function (data) {
          // Get the native platform of the device.
          var platform = device.platform;
          // Get the handle returned during registration.
          var handle = data.registrationId;
          // Set the device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="f791f-156">(Android) 在上述程式碼中，從 [Google Developer Console][18] 使用應用程式的數字專案識別碼取代 `Your_Project_ID`。</span><span class="sxs-lookup"><span data-stu-id="f791f-156">(Android) In the preceding code, replace `Your_Project_ID` with the numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-the-app-on-android"></a><span data-ttu-id="f791f-157">(選擇性) 在 Android 上設定和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f791f-157">(Optional) Configure and run the app on Android</span></span>
<span data-ttu-id="f791f-158">完成本節可以為 Android 啟用推播通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-158">Complete this section to enable push notifications for Android.</span></span>

#### <span data-ttu-id="f791f-159"><a name="enable-gcm"></a>啟用 Firebase 雲端傳訊</span><span class="sxs-lookup"><span data-stu-id="f791f-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="f791f-160">因為我們一開始是以 Google Android 平台為目標，所以您必須啟用 Firebase 雲端通訊。</span><span class="sxs-lookup"><span data-stu-id="f791f-160">Since we are targeting the Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="f791f-161"><a name="configure-backend"></a>設定行動應用程式後端以使用 FCM 傳送推送要求</span><span class="sxs-lookup"><span data-stu-id="f791f-161"><a name="configure-backend"></a>Configure the Mobile App backend to send push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="f791f-162">針對 Android 設定您的 Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="f791f-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="f791f-163">在 Cordova 應用程式中，開啟 config.xml，然後從 [Google Developer Console] 使用應用程式的數字專案識別碼取代 `Your_Project_ID`[18]。</span><span class="sxs-lookup"><span data-stu-id="f791f-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with the numeric project ID for your app from the [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="f791f-164">開啟 index.js，並更新程式碼以使用您的數值專案識別碼。</span><span class="sxs-lookup"><span data-stu-id="f791f-164">Open index.js and update the code to use your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="f791f-165"><a name="configure-device"></a>設定 Android 裝置進行 USB 偵錯</span><span class="sxs-lookup"><span data-stu-id="f791f-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="f791f-166">在您可以將應用程式部署到您的 Android 裝置之前，您需要啟用 USB 偵錯。</span><span class="sxs-lookup"><span data-stu-id="f791f-166">Before you can deploy your application to your Android Device, you need to enable USB Debugging.</span></span>  <span data-ttu-id="f791f-167">在您的 Android 手機上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f791f-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="f791f-168">移至 [設定] > [關於手機]，然後點選 [組建編號]，直到啟用開發人員模式為止 (大約七次)。</span><span class="sxs-lookup"><span data-stu-id="f791f-168">Go to **Settings** > **About phone**, then tap the **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="f791f-169">回到 [設定] > [開發人員選項]，啟用 [USB 偵錯]，然後使用 USB 纜線將 Android 手機連接至開發電腦。</span><span class="sxs-lookup"><span data-stu-id="f791f-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  to your development PC with a USB Cable.</span></span>

<span data-ttu-id="f791f-170">我們測試時使用的是執行 Android 6.0 (Marshmallow) 的 Google Nexus 5 X 裝置。</span><span class="sxs-lookup"><span data-stu-id="f791f-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="f791f-171">不過，這些技術在任何現代化 Android 版本中都是相同的。</span><span class="sxs-lookup"><span data-stu-id="f791f-171">However, the techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="f791f-172">安裝 Google Play 服務</span><span class="sxs-lookup"><span data-stu-id="f791f-172">Install Google Play Services</span></span>
<span data-ttu-id="f791f-173">推播外掛程式仰賴 Android Google Play 服務來進行推播通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-173">The push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="f791f-174">在 Visual Studio 中，按一下 [工具] > [Android] > [Android SDK 管理員]，然後展開 [Extras] 資料夾並核取方塊，以確定安裝下列所有 SDK。</span><span class="sxs-lookup"><span data-stu-id="f791f-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand the **Extras** folder and  check the box to make sure that each of the following SDKs is installed.</span></span>

   * <span data-ttu-id="f791f-175">Android 2.3 或更新版本</span><span class="sxs-lookup"><span data-stu-id="f791f-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="f791f-176">Google Repository 版本 27 或更高版本</span><span class="sxs-lookup"><span data-stu-id="f791f-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="f791f-177">Google Play 服務 9.0.2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="f791f-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="f791f-178">按一下 [安裝套件]，等待安裝完成。</span><span class="sxs-lookup"><span data-stu-id="f791f-178">Click **Install Packages** and wait for the installation to complete.</span></span>

<span data-ttu-id="f791f-179">[phonegap-plugin-push 安裝文件][19]中列出目前必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="f791f-179">The current required libraries are listed in the [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-the-app-on-android"></a><span data-ttu-id="f791f-180">在 Android 上的應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="f791f-180">Test push notifications in the app on Android</span></span>
<span data-ttu-id="f791f-181">您現在可以執行應用程式，在 TodoItem 資料表中插入項目，以測試推播通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-181">You can now test push notifications by running the app and inserting items in the TodoItem table.</span></span> <span data-ttu-id="f791f-182">只要是使用相同的後端，您可以從相同的裝置或第二部裝置來測試。</span><span class="sxs-lookup"><span data-stu-id="f791f-182">You can test from the same device or from a second device, as long as you are using the same backend.</span></span> <span data-ttu-id="f791f-183">以下列方法之一在 Android 平台上測試 Cordova 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="f791f-183">Test your Cordova app on the Android platform in one of the following ways:</span></span>

* <span data-ttu-id="f791f-184">**在實體裝置上︰**使用 USB 纜線將 Android 裝置連接至開發電腦。</span><span class="sxs-lookup"><span data-stu-id="f791f-184">**On a physical device:** Attach your Android device to your development computer with a USB cable.</span></span>  <span data-ttu-id="f791f-185">請選取 [裝置]，不要選取 [Google Android 模擬器]。</span><span class="sxs-lookup"><span data-stu-id="f791f-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="f791f-186">Visual Studio 會將應用程式部署至裝置，然後執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f791f-186">Visual Studio deploys the application to the device and then runs the application.</span></span>  <span data-ttu-id="f791f-187">您接著可以在裝置上與應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="f791f-187">You can then interact with the application on the device.</span></span>

  <span data-ttu-id="f791f-188">改善您的開發經驗。</span><span class="sxs-lookup"><span data-stu-id="f791f-188">Improve your development experience.</span></span>  <span data-ttu-id="f791f-189">[Mobizen] [20] 等螢幕畫面分享應用程式可協助您開發 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f791f-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="f791f-190">Mobizen 會將您的 Android 畫面投射至電腦上的網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="f791f-190">Mobizen projects your Android screen to a web browser on your PC.</span></span>

* <span data-ttu-id="f791f-191">**在 Android 模擬器上︰**在模擬器上執行時，還需要其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="f791f-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="f791f-192">請確定您是部署至已將 Google API 設為目標的虛擬裝置，如 Android 虛擬裝置 (AVD) 管理員中所示。</span><span class="sxs-lookup"><span data-stu-id="f791f-192">Make sure you are deploying to a virtual device that has Google APIs set as the target, as shown in the Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="f791f-193">如果您想要使用更快速的 x86 模擬器，請[安裝 HAXM 驅動程式][11]，並設定模擬器來使用它。</span><span class="sxs-lookup"><span data-stu-id="f791f-193">If you want to use a faster x86 emulator, you [install the HAXM driver][11] and configure the emulator to use it.</span></span>

    <span data-ttu-id="f791f-194">按一下 [應用程式] > [設定] > [新增帳戶] 將 Google 帳戶加入 Android 裝置，然後遵循提示。</span><span class="sxs-lookup"><span data-stu-id="f791f-194">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="f791f-195">按照先前的方法執行 todolist 應用程式，然後插入新的 todo 項目。</span><span class="sxs-lookup"><span data-stu-id="f791f-195">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="f791f-196">這次，通知圖示會顯示在通知區域中。</span><span class="sxs-lookup"><span data-stu-id="f791f-196">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="f791f-197">您可以開啟通知抽屜來檢視通知的完整內容。</span><span class="sxs-lookup"><span data-stu-id="f791f-197">You can open the notification drawer to view the full text of the notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="f791f-198">(選擇性) 在 iOS 上設定和執行</span><span class="sxs-lookup"><span data-stu-id="f791f-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="f791f-199">本節適用於在 iOS 裝置上執行 Cordova 專案。</span><span class="sxs-lookup"><span data-stu-id="f791f-199">This section is for running the Cordova project on iOS devices.</span></span> <span data-ttu-id="f791f-200">如果未使用 iOS 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="f791f-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-the-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="f791f-201">在 Mac 或雲端服務上安裝及執行 iOS 遠端組建代理程式</span><span class="sxs-lookup"><span data-stu-id="f791f-201">Install and run the iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="f791f-202">您必須先進行 [iOS 安裝指南][12]中的步驟來安裝和執行遠端組建代理程式，才可以使用 Visual Studio 在 iOS 上執行 Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f791f-202">Before you can run a Cordova app on iOS using Visual Studio, go through the steps in the [iOS Setup Guide][12] to install and run the remote build agent.</span></span>

<span data-ttu-id="f791f-203">確定您可以建置適用於 iOS 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f791f-203">Make sure you can build the app for iOS.</span></span> <span data-ttu-id="f791f-204">必須執行安裝指南中的步驟才能從 Visual Studio 針對 iOS 建置。</span><span class="sxs-lookup"><span data-stu-id="f791f-204">The steps in the setup guide are required to build for iOS from Visual Studio.</span></span> <span data-ttu-id="f791f-205">如果您沒有 Mac，您可以在 MacInCloud 之類的服務上使用遠端組建代理程式來針對 iOS 建置。</span><span class="sxs-lookup"><span data-stu-id="f791f-205">If you do not have a Mac, you can build for iOS using the remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="f791f-206">如需詳細資訊，請參閱[在雲端中執行 iOS 應用程式][21]。</span><span class="sxs-lookup"><span data-stu-id="f791f-206">For more info, see [Run your iOS app in the cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="f791f-207">必須有 XCode 7 或更新版本，才能在 iOS 上使用推播外掛程式。</span><span class="sxs-lookup"><span data-stu-id="f791f-207">XCode 7 or greater is required to use the push plugin on iOS.</span></span>

#### <a name="find-the-id-to-use-as-your-app-id"></a><span data-ttu-id="f791f-208">尋找要做為應用程式識別碼的識別碼</span><span class="sxs-lookup"><span data-stu-id="f791f-208">Find the ID to use as your App ID</span></span>
<span data-ttu-id="f791f-209">在針對推播通知註冊您的應用程式之前，在 Cordova 應用程式中開啟 config.xml，在 widget 元素中尋找 `id` 屬性值，並加以複製以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="f791f-209">Before you register your app for push notifications, open config.xml in your Cordova app, find the `id` attribute value in the widget element, and copy it for later use.</span></span> <span data-ttu-id="f791f-210">在下列 XML 中，識別碼為 `io.cordova.myapp7777777`。</span><span class="sxs-lookup"><span data-stu-id="f791f-210">In the following XML, the ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="f791f-211">稍後，當您在 Apple 開發人員入口網站上建立應用程式識別碼時，請使用這個識別碼。</span><span class="sxs-lookup"><span data-stu-id="f791f-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="f791f-212">如果您在開發人員入口網站上建立不同的應用程式識別碼，在本教學課程稍後，您必須採取一些額外的步驟。</span><span class="sxs-lookup"><span data-stu-id="f791f-212">If you create a different App ID on the developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="f791f-213">Widget 元素中的識別碼必須符合開發人員入口網站上的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="f791f-213">The ID in the widget element must match the App ID on the developer portal.</span></span>

#### <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="f791f-214">在 Apple 的開發人員入口網站註冊應用程式以取得推播通知</span><span class="sxs-lookup"><span data-stu-id="f791f-214">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="f791f-215">觀看示範類似步驟的影片</span><span class="sxs-lookup"><span data-stu-id="f791f-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="f791f-216">設定 Azure 來傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="f791f-216">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="f791f-217">確認您的應用程式識別碼符合 Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="f791f-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="f791f-218">如果您在 Apple 開發人員帳戶中建立的應用程式識別碼已經符合 config.xml 中 widget 元素的識別碼，您即可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="f791f-218">If the App ID you created in your Apple Developer Account already matches the ID of the widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="f791f-219">不過，如果識別碼不相符，請採取下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="f791f-219">However, if the IDs don't match, take the following steps:</span></span>

1. <span data-ttu-id="f791f-220">從您的專案中刪除 platforms 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f791f-220">Delete the platforms folder from your project.</span></span>
2. <span data-ttu-id="f791f-221">從您的專案中刪除 plugins 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f791f-221">Delete the plugins folder from your project.</span></span>
3. <span data-ttu-id="f791f-222">從您的專案中刪除 node_modules 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f791f-222">Delete the node_modules folder from your project.</span></span>
4. <span data-ttu-id="f791f-223">在 config.xml 中更新 widget 元素的 id 屬性，以使用您在 Apple 開發人員帳戶中建立的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="f791f-223">Update the id attribute of the widget element in config.xml to use the App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="f791f-224">重建您的專案。</span><span class="sxs-lookup"><span data-stu-id="f791f-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="f791f-225">在 iOS 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="f791f-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="f791f-226">在 Visual Studio 中，確定已選取 **iOS** 做為部署目標，然後選擇 [裝置] 以在連線的 iOS 裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="f791f-226">In Visual Studio, make sure that **iOS** is selected as the deployment target, and then choose **Device** to run on your connected iOS device.</span></span>

    <span data-ttu-id="f791f-227">您可以在使用 iTunes 連線至您的 PC 的 iOS 裝置上執行。</span><span class="sxs-lookup"><span data-stu-id="f791f-227">You can run on an iOS device connected to your PC using iTunes.</span></span> <span data-ttu-id="f791f-228">iOS 模擬器不支援推播通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-228">The iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="f791f-229">在 Visual Studio 中，按下 [執行] 按鈕或 **F5** 以建置專案，並在 iOS 裝置上啟動應用程式，然後按一下 [確定] 以接受推播通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-229">Press the **Run** button or **F5** in Visual Studio to build the project and start the app in an iOS  device, then click **OK** to accept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f791f-230">應用程式在第一次執行期間會要求您確認推播通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-230">The app requests confirmation for push notifications during the first run.</span></span>

3. <span data-ttu-id="f791f-231">在應用程式中輸入一項工作，然後按一下加號 (+) 圖示。</span><span class="sxs-lookup"><span data-stu-id="f791f-231">In the app, type a task, and then click the plus (+) icon.</span></span>
4. <span data-ttu-id="f791f-232">確認您已接收到通知，然後按一下 [確定] 以關閉通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-232">Verify that a notification is received, then click OK to dismiss the notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="f791f-233">(選擇性) 在 Windows 上設定和執行</span><span class="sxs-lookup"><span data-stu-id="f791f-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="f791f-234">本節適用於在 Windows 10 裝置 (Windows 10 支援 PhoneGap 推播外掛程式) 上執行 Apache Cordova 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="f791f-234">This section is for running the Apache Cordova app project on Windows 10 devices (the PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="f791f-235">如果未使用 Windows 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="f791f-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="f791f-236">向 WNS 註冊 Windows 應用程式以使用推播通知</span><span class="sxs-lookup"><span data-stu-id="f791f-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="f791f-237">若要使用 Visual Studio 中的 [存放區] 選項，請從 [方案平台] 清單中選取 Windows 目標，例如 **Windows-x64** 或 **Windows-x86** (避免 **Windows-AnyCPU** 使用推播通知)。</span><span class="sxs-lookup"><span data-stu-id="f791f-237">To use the Store options in Visual Studio, select a Windows target from the Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="f791f-238">[觀看示範類似步驟的影片][13]</span><span class="sxs-lookup"><span data-stu-id="f791f-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-the-notification-hub-for-wns"></a><span data-ttu-id="f791f-239">設定 WNS 的通知中樞</span><span class="sxs-lookup"><span data-stu-id="f791f-239">Configure the notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-to-support-windows-push-notifications"></a><span data-ttu-id="f791f-240">設定 Cordova 應用程式以支援 Windows 推播通知</span><span class="sxs-lookup"><span data-stu-id="f791f-240">Configure your Cordova app to support Windows push notifications</span></span>
<span data-ttu-id="f791f-241">開啟組態設計工具 (以滑鼠右鍵按一下 config.xml 並選取 [檢視表設計工具])，選取 [Windows] 索引標籤，然後選擇 [Windows 目標版本] 下的 [Windows 10]。</span><span class="sxs-lookup"><span data-stu-id="f791f-241">Open the configuration designer (right-click on config.xml and select **View Designer**), select the **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="f791f-242">若要在您的預設 (偵錯) 組建中支援推播通知，請開啟 build.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="f791f-242">To support push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="f791f-243">將 "release" 組態複製到您的偵錯組態。</span><span class="sxs-lookup"><span data-stu-id="f791f-243">Copy the "release" configuration to your debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="f791f-244">更新之後，build.json 應該包含下列程式碼︰</span><span class="sxs-lookup"><span data-stu-id="f791f-244">After the update, the build.json should contain the following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="f791f-245">建置應用程式並確認沒有錯誤。</span><span class="sxs-lookup"><span data-stu-id="f791f-245">Build the app and verify that you have no errors.</span></span> <span data-ttu-id="f791f-246">您的用戶端應用程式現在應該註冊來自行動應用程式後端的通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-246">Your client app should now register for the notifications from the Mobile App backend.</span></span> <span data-ttu-id="f791f-247">針對方案中每個 Windows 專案重複操作這一節。</span><span class="sxs-lookup"><span data-stu-id="f791f-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="f791f-248">在 Windows 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="f791f-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="f791f-249">在 Visual Studio 中，確定已選取 Windows 平台做為部署目標，例如 **Windows-x64** 或 **Windows-x86**。</span><span class="sxs-lookup"><span data-stu-id="f791f-249">In Visual Studio, make sure that a Windows platform is selected as the deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="f791f-250">若要在裝載 Visual Studio 的 Windows 10 電腦上執行應用程式，請選擇 [本機電腦] 。</span><span class="sxs-lookup"><span data-stu-id="f791f-250">To run the app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="f791f-251">按 [執行] 按鈕，以建置專案並啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="f791f-251">Press the Run button to build the project and start the app.</span></span>

<span data-ttu-id="f791f-252">在應用程式中輸入新 todoitem 的名稱，然後按一下加號 (+) 圖示來加入它。</span><span class="sxs-lookup"><span data-stu-id="f791f-252">In the app, type a name for a new todoitem, and then click the plus (+) icon to add it.</span></span>

<span data-ttu-id="f791f-253">確認在加入項目時收到通知。</span><span class="sxs-lookup"><span data-stu-id="f791f-253">Verify that a notification is received when the item is added.</span></span>

## <span data-ttu-id="f791f-254"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="f791f-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="f791f-255">請參閱[通知中樞][17]，以了解推播通知的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f791f-255">Read about [Notification Hubs][17] to learn about push notifications.</span></span>
* <span data-ttu-id="f791f-256">繼續教學課程，在 Apache Cordova 應用程式中[新增驗證][14] (如果尚未這麼做)。</span><span class="sxs-lookup"><span data-stu-id="f791f-256">If you have not already done so, continue the tutorial by [Adding Authentication][14] to your Apache Cordova app.</span></span>

<span data-ttu-id="f791f-257">了解如何使用 SDK。</span><span class="sxs-lookup"><span data-stu-id="f791f-257">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="f791f-258">[Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="f791f-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="f791f-259">[ASP.NET Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="f791f-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="f791f-260">[Node.js Server SDK][16]</span><span class="sxs-lookup"><span data-stu-id="f791f-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
