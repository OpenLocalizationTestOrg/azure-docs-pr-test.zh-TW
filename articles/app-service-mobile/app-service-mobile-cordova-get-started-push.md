---
title: "aaaAdd 推播通知 tooApache Cordova 應用程式與 Azure 行動應用程式 |Microsoft 文件"
description: "了解如何 toouse Azure 行動應用程式 toosend 推播通知 tooyour Apache Cordova 應用程式。"
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
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="25919-103">加入推播通知 tooyour Apache Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="25919-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="25919-104">概觀</span><span class="sxs-lookup"><span data-stu-id="25919-104">Overview</span></span>
<span data-ttu-id="25919-105">在本教學課程中，您會新增推播通知 toohello [Apache Cordova 的快速入門] 專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="25919-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="25919-106">如果您不要使用 hello 下載快速入門的伺服器專案，您需要 hello 推播通知擴充套件。</span><span class="sxs-lookup"><span data-stu-id="25919-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="25919-107">如需詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK][1]。</span><span class="sxs-lookup"><span data-stu-id="25919-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="25919-108"><a name="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="25919-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="25919-109">本教學課程涵蓋開發使用 Visual Studio 2015 hello Google Android 模擬器、 Android 裝置、 在 Windows 裝置和 iOS 裝置上執行 Apache Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25919-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="25919-110">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="25919-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="25919-111">具有 [Visual Studio Community 2015][2] 或更新版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="25919-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="25919-112">[Visual Studio Tools for Apache Cordova][4]。</span><span class="sxs-lookup"><span data-stu-id="25919-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="25919-113">[作用中的 Azure 帳戶][3]。</span><span class="sxs-lookup"><span data-stu-id="25919-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="25919-114">已完成的 [Apache Cordova 快速入門][5] 專案。</span><span class="sxs-lookup"><span data-stu-id="25919-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="25919-115">(Android) 具有已驗證電子郵件地址的 [Google 帳戶][6]。</span><span class="sxs-lookup"><span data-stu-id="25919-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="25919-116">(iOS) [Apple Developer Program 成員資格][7]和 iOS 裝置 (iOS 模擬器不支援推播)。</span><span class="sxs-lookup"><span data-stu-id="25919-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="25919-117">(Windows) [Windows 市集開發人員帳戶][8]和 Windows 10 裝置。</span><span class="sxs-lookup"><span data-stu-id="25919-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="25919-118"><a name="configure-hub"></a>設定通知中樞</span><span class="sxs-lookup"><span data-stu-id="25919-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="25919-119">[觀看示範本節步驟的視訊][9]</span><span class="sxs-lookup"><span data-stu-id="25919-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="25919-120">更新 hello 伺服器專案</span><span class="sxs-lookup"><span data-stu-id="25919-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="25919-121"><a name="add-push-to-app"></a>修改您的 Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="25919-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="25919-122">請確定您的 Apache Cordova 應用程式專案準備 toohandle 安裝 hello Cordova 發送外掛程式; 以及任何平台專屬推入 」 服務的推播通知。</span><span class="sxs-lookup"><span data-stu-id="25919-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="25919-123">更新您的專案中的 hello Cordova 版本。</span><span class="sxs-lookup"><span data-stu-id="25919-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="25919-124">如果您的專案使用 Apache Cordova 的版本早於 v6.1.1，更新 hello 用戶端專案。</span><span class="sxs-lookup"><span data-stu-id="25919-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="25919-125">tooupdate hello 專案：</span><span class="sxs-lookup"><span data-stu-id="25919-125">tooupdate hello project:</span></span>

* <span data-ttu-id="25919-126">以滑鼠右鍵按一下`config.xml`tooopen hello 組態設計工具。</span><span class="sxs-lookup"><span data-stu-id="25919-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="25919-127">選取 hello 平台 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="25919-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="25919-128">選擇在 hello 6.1.1 **Cordova CLI**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="25919-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="25919-129">選擇**建置**，然後**建置方案**tooupdate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="25919-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="25919-130">安裝 hello 發送外掛程式</span><span class="sxs-lookup"><span data-stu-id="25919-130">Install hello push plugin</span></span>
<span data-ttu-id="25919-131">Apache Cordova 應用程式原本就不會處理裝置或網路功能。</span><span class="sxs-lookup"><span data-stu-id="25919-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="25919-132">這些功能是由 [npm][10] 或 GitHub 上發佈的外掛程式所提供。</span><span class="sxs-lookup"><span data-stu-id="25919-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="25919-133">hello`phonegap-plugin-push`外掛程式會使用的 toohandle 網路推播通知。</span><span class="sxs-lookup"><span data-stu-id="25919-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="25919-134">您可以使用下列其中一種安裝 hello 發送外掛程式：</span><span class="sxs-lookup"><span data-stu-id="25919-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="25919-135">**從 hello 命令提示字元：**</span><span class="sxs-lookup"><span data-stu-id="25919-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="25919-136">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="25919-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="25919-137">**從 Visual Studio 內：**</span><span class="sxs-lookup"><span data-stu-id="25919-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="25919-138">在 方案總管 中，開啟 hello`config.xml`檔案按一下**外掛程式** > **自訂**，選取**Git**做為安裝來源，然後輸入`https://github.com/phonegap/phonegap-plugin-push`為 hello 來源。</span><span class="sxs-lookup"><span data-stu-id="25919-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="25919-139">按一下 hello 箭頭下一步 toohello 安裝來源。</span><span class="sxs-lookup"><span data-stu-id="25919-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="25919-140">在**SENDER_ID**，如果您已經有 hello Google 開發人員主控台專案的數字的專案 ID，您可以在此處加入。</span><span class="sxs-lookup"><span data-stu-id="25919-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="25919-141">否則，請輸入預留位置值，例如 777777。</span><span class="sxs-lookup"><span data-stu-id="25919-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="25919-142">如果您是以 Android 為目標，您可以稍後在 config.xml 中更新此值。</span><span class="sxs-lookup"><span data-stu-id="25919-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="25919-143">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="25919-143">Click **Add**.</span></span>

<span data-ttu-id="25919-144">現在安裝 hello 發送外掛程式。</span><span class="sxs-lookup"><span data-stu-id="25919-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="25919-145">安裝 hello 裝置外掛程式</span><span class="sxs-lookup"><span data-stu-id="25919-145">Install hello device plugin</span></span>
<span data-ttu-id="25919-146">後續 hello 相同程序使用 tooinstall hello 發送外掛程式。</span><span class="sxs-lookup"><span data-stu-id="25919-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="25919-147">從 hello 核心外掛程式清單加入 hello 裝置外掛程式 (按一下**外掛程式** > **核心**toofind 它)。</span><span class="sxs-lookup"><span data-stu-id="25919-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="25919-148">您需要使用此外掛程式 tooobtain hello 平台名稱。</span><span class="sxs-lookup"><span data-stu-id="25919-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="25919-149">在應用程式啟動時註冊您的裝置</span><span class="sxs-lookup"><span data-stu-id="25919-149">Register your device on application start-up</span></span>
<span data-ttu-id="25919-150">最初，我們包含一些適用於 Android 的最少程式碼。</span><span class="sxs-lookup"><span data-stu-id="25919-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="25919-151">更新版本中，修改 hello iOS 或 Windows 10 上的應用程式 toorun。</span><span class="sxs-lookup"><span data-stu-id="25919-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="25919-152">加入呼叫太**registerForPushNotifications** hello 登入程序，或在 hello 底部 hello hello 回呼期間**onDeviceReady**方法：</span><span class="sxs-lookup"><span data-stu-id="25919-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="25919-153">這個範例示範在成功驗證之後呼叫 **registerForPushNotifications**。</span><span class="sxs-lookup"><span data-stu-id="25919-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="25919-154">您可以依需要經常呼叫 `registerForPushNotifications()`。</span><span class="sxs-lookup"><span data-stu-id="25919-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="25919-155">新增新的 hello **registerForPushNotifications**方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="25919-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
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
3. <span data-ttu-id="25919-156">(Android)在上述程式碼的 hello，取代`Your_Project_ID`以 hello 的數字，請從應用程式的專案 ID [Google 開發人員主控台][18]。</span><span class="sxs-lookup"><span data-stu-id="25919-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="25919-157">（選擇性）設定及在 Android 上執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="25919-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="25919-158">完成適用於 Android 的這個區段 tooenable 推播通知。</span><span class="sxs-lookup"><span data-stu-id="25919-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="25919-159"><a name="enable-gcm"></a>啟用 Firebase 雲端傳訊</span><span class="sxs-lookup"><span data-stu-id="25919-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="25919-160">因為我們的目標 hello Google Android 平台一開始，您必須啟用 Firebase Cloud Messaging。</span><span class="sxs-lookup"><span data-stu-id="25919-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="25919-161"><a name="configure-backend"></a>Hello 行動裝置應用程式後端 toosend 推播要求使用 FCM 設定</span><span class="sxs-lookup"><span data-stu-id="25919-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="25919-162">針對 Android 設定您的 Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="25919-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="25919-163">Cordova 應用程式中開啟 config.xml，並取代`Your_Project_ID`以 hello 的數字，請從 hello 應用程式的專案 ID [Google 開發人員主控台][18]。</span><span class="sxs-lookup"><span data-stu-id="25919-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="25919-164">開啟 index.js，並更新 hello 程式碼 toouse 您數值專案識別碼。</span><span class="sxs-lookup"><span data-stu-id="25919-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="25919-165"><a name="configure-device"></a>設定 Android 裝置進行 USB 偵錯</span><span class="sxs-lookup"><span data-stu-id="25919-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="25919-166">您可以部署您的應用程式 tooyour Android 裝置之前，您會需要 tooenable USB 偵錯。</span><span class="sxs-lookup"><span data-stu-id="25919-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="25919-167">在您的 Android 手機上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="25919-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="25919-168">跳過**設定** > **關於電話**，然後點選 hello**組建編號**直到開發人員模式已啟用 （約七次）。</span><span class="sxs-lookup"><span data-stu-id="25919-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="25919-169">回到**設定** > **開發人員選項**啟用**USB 偵錯**，然後使用 USB 纜線連接您的 Android 手機 tooyour 開發電腦。</span><span class="sxs-lookup"><span data-stu-id="25919-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="25919-170">我們測試時使用的是執行 Android 6.0 (Marshmallow) 的 Google Nexus 5 X 裝置。</span><span class="sxs-lookup"><span data-stu-id="25919-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="25919-171">不過，hello 技術是通用的任何現代的 Android 版本。</span><span class="sxs-lookup"><span data-stu-id="25919-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="25919-172">安裝 Google Play 服務</span><span class="sxs-lookup"><span data-stu-id="25919-172">Install Google Play Services</span></span>
<span data-ttu-id="25919-173">hello 發送外掛程式依賴 Android Google Play 服務的推播通知。</span><span class="sxs-lookup"><span data-stu-id="25919-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="25919-174">在 Visual Studio 中，按一下 **工具** > **Android** > **Android SDK Manager**，依序展開 hello **Extras**資料夾，然後核取 hello 方塊 toomake 確定每個 hello 下列 Sdk 已安裝。</span><span class="sxs-lookup"><span data-stu-id="25919-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="25919-175">Android 2.3 或更新版本</span><span class="sxs-lookup"><span data-stu-id="25919-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="25919-176">Google Repository 版本 27 或更高版本</span><span class="sxs-lookup"><span data-stu-id="25919-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="25919-177">Google Play 服務 9.0.2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="25919-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="25919-178">按一下**Install Packages**並等候 hello 安裝 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="25919-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="25919-179">hello 目前所需的程式庫會列在 hello [phonegap 外掛程式-推入安裝的文件][19]。</span><span class="sxs-lookup"><span data-stu-id="25919-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="25919-180">在 hello 應用程式在 Android 上測試推播通知</span><span class="sxs-lookup"><span data-stu-id="25919-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="25919-181">您現在即可以藉由執行測試推播通知 hello 應用程式與 hello TodoItem 資料表中的插入項目。</span><span class="sxs-lookup"><span data-stu-id="25919-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="25919-182">您可以測試從 hello 相同的裝置，或從第二台裝置，只要您使用 hello 相同後端。</span><span class="sxs-lookup"><span data-stu-id="25919-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="25919-183">其中一種 hello 下列方式測試 hello Android 平台上的 Cordova 應用程式：</span><span class="sxs-lookup"><span data-stu-id="25919-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="25919-184">**實體裝置上：**附加的 Android 裝置的 tooyour 開發電腦的 USB 纜線。</span><span class="sxs-lookup"><span data-stu-id="25919-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="25919-185">請選取 [裝置]，不要選取 [Google Android 模擬器]。</span><span class="sxs-lookup"><span data-stu-id="25919-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="25919-186">Visual Studio 部署 hello 應用程式 toohello 裝置，然後執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25919-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="25919-187">您可以再互動 hello hello 裝置上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="25919-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="25919-188">改善您的開發經驗。</span><span class="sxs-lookup"><span data-stu-id="25919-188">Improve your development experience.</span></span>  <span data-ttu-id="25919-189">[Mobizen] [20] 等螢幕畫面分享應用程式可協助您開發 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25919-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="25919-190">Mobizen 規劃您的電腦上的 Android 螢幕 tooa 網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="25919-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="25919-191">**在 Android 模擬器上︰**在模擬器上執行時，還需要其他設定步驟。</span><span class="sxs-lookup"><span data-stu-id="25919-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="25919-192">請確定您要部署 tooa hello Android Virtual Device (AVD) manager 中所示，已將設為 hello 目標的 Google Api 的虛擬裝置。</span><span class="sxs-lookup"><span data-stu-id="25919-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="25919-193">如果您想 toouse 更快的 x86 模擬器中，您[安裝 hello HAXM 驅動程式][ 11]及設定 hello 模擬器 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="25919-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="25919-194">按一下 新增 Google 帳戶 toohello Android 裝置**應用程式** > **設定** > **將帳戶加入**，然後依照 hello 提示。</span><span class="sxs-lookup"><span data-stu-id="25919-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="25919-195">執行 hello todolist 應用程式做之前，插入新的 todo 項目。</span><span class="sxs-lookup"><span data-stu-id="25919-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="25919-196">此時，通知圖示會顯示 hello 通知區域中。</span><span class="sxs-lookup"><span data-stu-id="25919-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="25919-197">您可以開啟 hello 通知抽屜 tooview hello 全文檢索的 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="25919-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="25919-198">(選擇性) 在 iOS 上設定和執行</span><span class="sxs-lookup"><span data-stu-id="25919-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="25919-199">本章節適用於 iOS 裝置上執行 hello Cordova 專案。</span><span class="sxs-lookup"><span data-stu-id="25919-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="25919-200">如果未使用 iOS 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="25919-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="25919-201">安裝和遠端執行的 hello iOS 組建代理程式上的 Mac 或雲端服務</span><span class="sxs-lookup"><span data-stu-id="25919-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="25919-202">您可以使用 Visual Studio 的 iOS 上執行 Cordova 應用程式之前，請瀏覽 hello 中的 hello 步驟[iOS Setup Guide] [ 12] tooinstall 和執行的 hello 遠端組建代理程式。</span><span class="sxs-lookup"><span data-stu-id="25919-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="25919-203">請確定您可以建立 hello 適用於 iOS 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="25919-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="25919-204">hello hello 安裝手冊 》 中的步驟都需要的 toobuild Visual Studio 的 ios。</span><span class="sxs-lookup"><span data-stu-id="25919-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="25919-205">如果您沒有 Mac，您可以建置適用於 iOS 等 MacInCloud 服務上使用 hello 遠端組建代理程式。</span><span class="sxs-lookup"><span data-stu-id="25919-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="25919-206">如需詳細資訊，請參閱[hello 雲端中執行您的 iOS 應用程式][21]。</span><span class="sxs-lookup"><span data-stu-id="25919-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="25919-207">XCode 7 或更新版本是在 iOS 上的必要的 toouse hello 發送外掛程式。</span><span class="sxs-lookup"><span data-stu-id="25919-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="25919-208">尋找 hello 識別碼 toouse 做為應用程式的識別碼</span><span class="sxs-lookup"><span data-stu-id="25919-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="25919-209">註冊您的推播通知的應用程式之前，開啟 config.xml Cordova 應用程式中，尋找 hello`id`屬性值在 hello widget 元素中，並將它複製供日後使用。</span><span class="sxs-lookup"><span data-stu-id="25919-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="25919-210">在下列 XML 的 hello，hello ID 是`io.cordova.myapp7777777`。</span><span class="sxs-lookup"><span data-stu-id="25919-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="25919-211">稍後，當您在 Apple 開發人員入口網站上建立應用程式識別碼時，請使用這個識別碼。</span><span class="sxs-lookup"><span data-stu-id="25919-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="25919-212">如果您建立不同的應用程式識別碼 hello 開發人員入口網站上，您必須採取一些額外的步驟，稍後在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="25919-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="25919-213">widget 元素中的 hello ID 必須符合在 hello 開發人員入口網站上的應用程式識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="25919-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="25919-214">註冊 Apple 開發人員入口網站上的推播通知的 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="25919-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="25919-215">觀看示範類似步驟的影片</span><span class="sxs-lookup"><span data-stu-id="25919-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="25919-216">設定 Azure toosend 推播通知</span><span class="sxs-lookup"><span data-stu-id="25919-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="25919-217">確認您的應用程式識別碼符合 Cordova 應用程式</span><span class="sxs-lookup"><span data-stu-id="25919-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="25919-218">如果您已經在您的 Apple 開發人員帳戶中建立的應用程式識別碼 hello 符合 hello 在 config.xml 中的 hello widget 項目的 ID，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="25919-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="25919-219">不過，如果 hello 識別碼不相符，採取下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="25919-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="25919-220">從您的專案刪除 hello 平台資料夾。</span><span class="sxs-lookup"><span data-stu-id="25919-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="25919-221">從您的專案刪除 hello 外掛程式資料夾。</span><span class="sxs-lookup"><span data-stu-id="25919-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="25919-222">從專案刪除 hello node_modules 資料夾。</span><span class="sxs-lookup"><span data-stu-id="25919-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="25919-223">更新 config.xml toouse hello Apple 開發人員帳戶中建立的應用程式識別碼中的 hello widget 元素 hello id 屬性。</span><span class="sxs-lookup"><span data-stu-id="25919-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="25919-224">重建您的專案。</span><span class="sxs-lookup"><span data-stu-id="25919-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="25919-225">在 iOS 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="25919-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="25919-226">在 Visual Studio 中，請確定**iOS** hello 部署目標，為已選取，然後選擇 **裝置**toorun 已連線的 iOS 裝置上。</span><span class="sxs-lookup"><span data-stu-id="25919-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="25919-227">您可以在 iOS 裝置連線 tooyour 電腦上執行使用 iTunes。</span><span class="sxs-lookup"><span data-stu-id="25919-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="25919-228">hello iOS 模擬器不支援推播通知。</span><span class="sxs-lookup"><span data-stu-id="25919-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="25919-229">按 hello**執行**按鈕或**F5**在 Visual Studio toobuild hello 專案並開始 hello 應用程式在 iOS 裝置，然後按一下 **確定**tooaccept 推播通知。</span><span class="sxs-lookup"><span data-stu-id="25919-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="25919-230">hello 應用程式要求您的推播通知 hello 第一次執行期間的確認。</span><span class="sxs-lookup"><span data-stu-id="25919-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="25919-231">在 hello 應用程式中，輸入工作，，然後按一下hello 加號 （+） 圖示。</span><span class="sxs-lookup"><span data-stu-id="25919-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="25919-232">確認通知接收，然後按一下 [確定] toodismiss hello 通知。</span><span class="sxs-lookup"><span data-stu-id="25919-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="25919-233">(選擇性) 在 Windows 上設定和執行</span><span class="sxs-lookup"><span data-stu-id="25919-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="25919-234">這個區段可讓您執行 hello Apache Cordova 應用程式專案 （Windows 10 支援 hello PhoneGap 發送外掛程式） 的 Windows 10 裝置上。</span><span class="sxs-lookup"><span data-stu-id="25919-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="25919-235">如果未使用 Windows 裝置，可以略過這一節。</span><span class="sxs-lookup"><span data-stu-id="25919-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="25919-236">向 WNS 註冊 Windows 應用程式以使用推播通知</span><span class="sxs-lookup"><span data-stu-id="25919-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="25919-237">toouse hello 存放區選項在 Visual Studio 中，選取 Windows 目標 hello 方案平台清單中，例如**x64**或**x86** (避免**Windows AnyCPU**推播通知）。</span><span class="sxs-lookup"><span data-stu-id="25919-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="25919-238">[觀看示範類似步驟的影片][13]</span><span class="sxs-lookup"><span data-stu-id="25919-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="25919-239">WNS 設定 hello 通知中樞</span><span class="sxs-lookup"><span data-stu-id="25919-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="25919-240">設定 Cordova 應用程式 toosupport Windows 推播通知</span><span class="sxs-lookup"><span data-stu-id="25919-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="25919-241">開啟 hello 組態設計工具 (config.xml，並選取以滑鼠右鍵按一下**檢視表設計工具**)，請選取 hello **Windows**索引標籤，然後選擇  **Windows 10**下**Windows 目標版本**。</span><span class="sxs-lookup"><span data-stu-id="25919-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="25919-242">建置 toosupport 推播通知，在預設的 （偵錯） 中，開啟 build.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="25919-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="25919-243">將複製的 「 發行 」 組態 tooyour 偵錯組態。</span><span class="sxs-lookup"><span data-stu-id="25919-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="25919-244">Hello 更新之後，hello build.json 應該包含下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="25919-244">After hello update, hello build.json should contain hello following code:</span></span>

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

<span data-ttu-id="25919-245">建置 hello 應用程式，並確認您有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="25919-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="25919-246">您的用戶端應用程式現在應該針對 hello 通知從 hello 行動裝置應用程式後端註冊。</span><span class="sxs-lookup"><span data-stu-id="25919-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="25919-247">針對方案中每個 Windows 專案重複操作這一節。</span><span class="sxs-lookup"><span data-stu-id="25919-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="25919-248">在 Windows 應用程式中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="25919-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="25919-249">在 Visual Studio 中，請確定 Windows 平台這類選取做為 hello 部署目標， **x64**或**x86**。</span><span class="sxs-lookup"><span data-stu-id="25919-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="25919-250">toorun hello 應用程式裝載 Visual Studio 中，在 Windows 10 電腦上的選擇**本機**。</span><span class="sxs-lookup"><span data-stu-id="25919-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="25919-251">按 hello 執行按鈕 toobuild hello 專案，並啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25919-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="25919-252">在 hello 應用程式中，輸入新的 todoitem 的名稱，然後按一下 hello 加號 （+） 圖示 tooadd 它。</span><span class="sxs-lookup"><span data-stu-id="25919-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="25919-253">確認新增 hello 項目時，收到通知。</span><span class="sxs-lookup"><span data-stu-id="25919-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="25919-254"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="25919-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="25919-255">閱讀有關[通知中樞][ 17] toolearn 有關推播通知。</span><span class="sxs-lookup"><span data-stu-id="25919-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="25919-256">如果您尚未這樣做，繼續 hello 教學課程所[新增驗證][ 14] tooyour Apache Cordova 應用程式。</span><span class="sxs-lookup"><span data-stu-id="25919-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="25919-257">了解如何 toouse hello Sdk。</span><span class="sxs-lookup"><span data-stu-id="25919-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="25919-258">[Apache Cordova SDK][15]</span><span class="sxs-lookup"><span data-stu-id="25919-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="25919-259">[ASP.NET Server SDK][1]</span><span class="sxs-lookup"><span data-stu-id="25919-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="25919-260">[Node.js Server SDK][16]</span><span class="sxs-lookup"><span data-stu-id="25919-260">[Node.js Server SDK][16]</span></span>

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
