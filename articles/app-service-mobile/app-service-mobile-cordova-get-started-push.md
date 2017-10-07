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
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>加入推播通知 tooyour Apache Cordova 應用程式
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>概觀
在本教學課程中，您會新增推播通知 toohello [Apache Cordova 的快速入門] 專案，以便每次將記錄插入推播通知會傳送 toohello 裝置。

如果您不要使用 hello 下載快速入門的伺服器專案，您需要 hello 推播通知擴充套件。 如需詳細資訊，請參閱[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK][1]。

## <a name="prerequisites"></a>必要條件
本教學課程涵蓋開發使用 Visual Studio 2015 hello Google Android 模擬器、 Android 裝置、 在 Windows 裝置和 iOS 裝置上執行 Apache Cordova 應用程式。

toocomplete 本教學課程中，您需要：

* 具有 [Visual Studio Community 2015][2] 或更新版本的電腦。
* [Visual Studio Tools for Apache Cordova][4]。
* [作用中的 Azure 帳戶][3]。
* 已完成的 [Apache Cordova 快速入門][5] 專案。
* (Android) 具有已驗證電子郵件地址的 [Google 帳戶][6]。
* (iOS) [Apple Developer Program 成員資格][7]和 iOS 裝置 (iOS 模擬器不支援推播)。
* (Windows) [Windows 市集開發人員帳戶][8]和 Windows 10 裝置。

## <a name="configure-hub"></a>設定通知中樞
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[觀看示範本節步驟的視訊][9]

## <a name="update-hello-server-project"></a>更新 hello 伺服器專案
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>修改您的 Cordova 應用程式
請確定您的 Apache Cordova 應用程式專案準備 toohandle 安裝 hello Cordova 發送外掛程式; 以及任何平台專屬推入 」 服務的推播通知。

#### <a name="update-hello-cordova-version-in-your-project"></a>更新您的專案中的 hello Cordova 版本。
如果您的專案使用 Apache Cordova 的版本早於 v6.1.1，更新 hello 用戶端專案。 tooupdate hello 專案：

* 以滑鼠右鍵按一下`config.xml`tooopen hello 組態設計工具。
* 選取 hello 平台 索引標籤。
* 選擇在 hello 6.1.1 **Cordova CLI**文字方塊。
* 選擇**建置**，然後**建置方案**tooupdate hello 專案。

#### <a name="install-hello-push-plugin"></a>安裝 hello 發送外掛程式
Apache Cordova 應用程式原本就不會處理裝置或網路功能。  這些功能是由 [npm][10] 或 GitHub 上發佈的外掛程式所提供。  hello`phonegap-plugin-push`外掛程式會使用的 toohandle 網路推播通知。

您可以使用下列其中一種安裝 hello 發送外掛程式：

**從 hello 命令提示字元：**

執行下列命令的 hello:

    cordova plugin add phonegap-plugin-push

**從 Visual Studio 內：**

1. 在 方案總管 中，開啟 hello`config.xml`檔案按一下**外掛程式** > **自訂**，選取**Git**做為安裝來源，然後輸入`https://github.com/phonegap/phonegap-plugin-push`為 hello 來源。

   ![][img1]

2. 按一下 hello 箭頭下一步 toohello 安裝來源。
3. 在**SENDER_ID**，如果您已經有 hello Google 開發人員主控台專案的數字的專案 ID，您可以在此處加入。 否則，請輸入預留位置值，例如 777777。  如果您是以 Android 為目標，您可以稍後在 config.xml 中更新此值。
4. 按一下 [新增] 。

現在安裝 hello 發送外掛程式。

#### <a name="install-hello-device-plugin"></a>安裝 hello 裝置外掛程式
後續 hello 相同程序使用 tooinstall hello 發送外掛程式。  從 hello 核心外掛程式清單加入 hello 裝置外掛程式 (按一下**外掛程式** > **核心**toofind 它)。 您需要使用此外掛程式 tooobtain hello 平台名稱。

#### <a name="register-your-device-on-application-start-up"></a>在應用程式啟動時註冊您的裝置
最初，我們包含一些適用於 Android 的最少程式碼。 更新版本中，修改 hello iOS 或 Windows 10 上的應用程式 toorun。

1. 加入呼叫太**registerForPushNotifications** hello 登入程序，或在 hello 底部 hello hello 回呼期間**onDeviceReady**方法：

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

    這個範例示範在成功驗證之後呼叫 **registerForPushNotifications**。  您可以依需要經常呼叫 `registerForPushNotifications()`。

2. 新增新的 hello **registerForPushNotifications**方法，如下所示：

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
3. (Android)在上述程式碼的 hello，取代`Your_Project_ID`以 hello 的數字，請從應用程式的專案 ID [Google 開發人員主控台][18]。

## <a name="optional-configure-and-run-hello-app-on-android"></a>（選擇性）設定及在 Android 上執行 hello 應用程式
完成適用於 Android 的這個區段 tooenable 推播通知。

#### <a name="enable-gcm"></a>啟用 Firebase 雲端傳訊
因為我們的目標 hello Google Android 平台一開始，您必須啟用 Firebase Cloud Messaging。

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Hello 行動裝置應用程式後端 toosend 推播要求使用 FCM 設定
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>針對 Android 設定您的 Cordova 應用程式
Cordova 應用程式中開啟 config.xml，並取代`Your_Project_ID`以 hello 的數字，請從 hello 應用程式的專案 ID [Google 開發人員主控台][18]。

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

開啟 index.js，並更新 hello 程式碼 toouse 您數值專案識別碼。

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>設定 Android 裝置進行 USB 偵錯
您可以部署您的應用程式 tooyour Android 裝置之前，您會需要 tooenable USB 偵錯。  在您的 Android 手機上執行下列步驟：

1. 跳過**設定** > **關於電話**，然後點選 hello**組建編號**直到開發人員模式已啟用 （約七次）。
2. 回到**設定** > **開發人員選項**啟用**USB 偵錯**，然後使用 USB 纜線連接您的 Android 手機 tooyour 開發電腦。

我們測試時使用的是執行 Android 6.0 (Marshmallow) 的 Google Nexus 5 X 裝置。  不過，hello 技術是通用的任何現代的 Android 版本。

#### <a name="install-google-play-services"></a>安裝 Google Play 服務
hello 發送外掛程式依賴 Android Google Play 服務的推播通知。

1. 在 Visual Studio 中，按一下 **工具** > **Android** > **Android SDK Manager**，依序展開 hello **Extras**資料夾，然後核取 hello 方塊 toomake 確定每個 hello 下列 Sdk 已安裝。

   * Android 2.3 或更新版本
   * Google Repository 版本 27 或更高版本
   * Google Play 服務 9.0.2 或更高版本

2. 按一下**Install Packages**並等候 hello 安裝 toocomplete。

hello 目前所需的程式庫會列在 hello [phonegap 外掛程式-推入安裝的文件][19]。

#### <a name="test-push-notifications-in-hello-app-on-android"></a>在 hello 應用程式在 Android 上測試推播通知
您現在即可以藉由執行測試推播通知 hello 應用程式與 hello TodoItem 資料表中的插入項目。 您可以測試從 hello 相同的裝置，或從第二台裝置，只要您使用 hello 相同後端。 其中一種 hello 下列方式測試 hello Android 平台上的 Cordova 應用程式：

* **實體裝置上：**附加的 Android 裝置的 tooyour 開發電腦的 USB 纜線。  請選取 [裝置]，不要選取 [Google Android 模擬器]。 Visual Studio 部署 hello 應用程式 toohello 裝置，然後執行 hello 應用程式。  您可以再互動 hello hello 裝置上的應用程式。

  改善您的開發經驗。  [Mobizen] [20] 等螢幕畫面分享應用程式可協助您開發 Android 應用程式。  Mobizen 規劃您的電腦上的 Android 螢幕 tooa 網頁瀏覽器。

* **在 Android 模擬器上︰**在模擬器上執行時，還需要其他設定步驟。

    請確定您要部署 tooa hello Android Virtual Device (AVD) manager 中所示，已將設為 hello 目標的 Google Api 的虛擬裝置。

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    如果您想 toouse 更快的 x86 模擬器中，您[安裝 hello HAXM 驅動程式][ 11]及設定 hello 模擬器 toouse 它。

    按一下 新增 Google 帳戶 toohello Android 裝置**應用程式** > **設定** > **將帳戶加入**，然後依照 hello 提示。

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    執行 hello todolist 應用程式做之前，插入新的 todo 項目。 此時，通知圖示會顯示 hello 通知區域中。 您可以開啟 hello 通知抽屜 tooview hello 全文檢索的 hello 通知。

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(選擇性) 在 iOS 上設定和執行
本章節適用於 iOS 裝置上執行 hello Cordova 專案。 如果未使用 iOS 裝置，可以略過這一節。

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>安裝和遠端執行的 hello iOS 組建代理程式上的 Mac 或雲端服務
您可以使用 Visual Studio 的 iOS 上執行 Cordova 應用程式之前，請瀏覽 hello 中的 hello 步驟[iOS Setup Guide] [ 12] tooinstall 和執行的 hello 遠端組建代理程式。

請確定您可以建立 hello 適用於 iOS 的應用程式。 hello hello 安裝手冊 》 中的步驟都需要的 toobuild Visual Studio 的 ios。 如果您沒有 Mac，您可以建置適用於 iOS 等 MacInCloud 服務上使用 hello 遠端組建代理程式。 如需詳細資訊，請參閱[hello 雲端中執行您的 iOS 應用程式][21]。

> [!NOTE]
> XCode 7 或更新版本是在 iOS 上的必要的 toouse hello 發送外掛程式。

#### <a name="find-hello-id-toouse-as-your-app-id"></a>尋找 hello 識別碼 toouse 做為應用程式的識別碼
註冊您的推播通知的應用程式之前，開啟 config.xml Cordova 應用程式中，尋找 hello`id`屬性值在 hello widget 元素中，並將它複製供日後使用。 在下列 XML 的 hello，hello ID 是`io.cordova.myapp7777777`。

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

稍後，當您在 Apple 開發人員入口網站上建立應用程式識別碼時，請使用這個識別碼。 如果您建立不同的應用程式識別碼 hello 開發人員入口網站上，您必須採取一些額外的步驟，稍後在本教學課程。 widget 元素中的 hello ID 必須符合在 hello 開發人員入口網站上的應用程式識別碼 hello。

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>註冊 Apple 開發人員入口網站上的推播通知的 hello 應用程式
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[觀看示範類似步驟的影片](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>設定 Azure toosend 推播通知
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>確認您的應用程式識別碼符合 Cordova 應用程式
如果您已經在您的 Apple 開發人員帳戶中建立的應用程式識別碼 hello 符合 hello 在 config.xml 中的 hello widget 項目的 ID，您可以略過此步驟。 不過，如果 hello 識別碼不相符，採取下列步驟的 hello:

1. 從您的專案刪除 hello 平台資料夾。
2. 從您的專案刪除 hello 外掛程式資料夾。
3. 從專案刪除 hello node_modules 資料夾。
4. 更新 config.xml toouse hello Apple 開發人員帳戶中建立的應用程式識別碼中的 hello widget 元素 hello id 屬性。
5. 重建您的專案。

##### <a name="test-push-notifications-in-your-ios-app"></a>在 iOS 應用程式中測試推播通知
1. 在 Visual Studio 中，請確定**iOS** hello 部署目標，為已選取，然後選擇 **裝置**toorun 已連線的 iOS 裝置上。

    您可以在 iOS 裝置連線 tooyour 電腦上執行使用 iTunes。 hello iOS 模擬器不支援推播通知。

2. 按 hello**執行**按鈕或**F5**在 Visual Studio toobuild hello 專案並開始 hello 應用程式在 iOS 裝置，然後按一下 **確定**tooaccept 推播通知。

   > [!NOTE]
   > hello 應用程式要求您的推播通知 hello 第一次執行期間的確認。

3. 在 hello 應用程式中，輸入工作，，然後按一下hello 加號 （+） 圖示。
4. 確認通知接收，然後按一下 [確定] toodismiss hello 通知。

## <a name="optional-configure-and-run-on-windows"></a>(選擇性) 在 Windows 上設定和執行
這個區段可讓您執行 hello Apache Cordova 應用程式專案 （Windows 10 支援 hello PhoneGap 發送外掛程式） 的 Windows 10 裝置上。 如果未使用 Windows 裝置，可以略過這一節。

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>向 WNS 註冊 Windows 應用程式以使用推播通知
toouse hello 存放區選項在 Visual Studio 中，選取 Windows 目標 hello 方案平台清單中，例如**x64**或**x86** (避免**Windows AnyCPU**推播通知）。

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[觀看示範類似步驟的影片][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>WNS 設定 hello 通知中樞
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>設定 Cordova 應用程式 toosupport Windows 推播通知
開啟 hello 組態設計工具 (config.xml，並選取以滑鼠右鍵按一下**檢視表設計工具**)，請選取 hello **Windows**索引標籤，然後選擇  **Windows 10**下**Windows 目標版本**。

建置 toosupport 推播通知，在預設的 （偵錯） 中，開啟 build.json 檔案。 將複製的 「 發行 」 組態 tooyour 偵錯組態。

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Hello 更新之後，hello build.json 應該包含下列程式碼的 hello:

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

建置 hello 應用程式，並確認您有任何錯誤。 您的用戶端應用程式現在應該針對 hello 通知從 hello 行動裝置應用程式後端註冊。 針對方案中每個 Windows 專案重複操作這一節。

#### <a name="test-push-notifications-in-your-windows-app"></a>在 Windows 應用程式中測試推播通知
在 Visual Studio 中，請確定 Windows 平台這類選取做為 hello 部署目標， **x64**或**x86**。 toorun hello 應用程式裝載 Visual Studio 中，在 Windows 10 電腦上的選擇**本機**。

按 hello 執行按鈕 toobuild hello 專案，並啟動 hello 應用程式。

在 hello 應用程式中，輸入新的 todoitem 的名稱，然後按一下 hello 加號 （+） 圖示 tooadd 它。

確認新增 hello 項目時，收到通知。

## <a name="next-steps"></a>後續步驟
* 閱讀有關[通知中樞][ 17] toolearn 有關推播通知。
* 如果您尚未這樣做，繼續 hello 教學課程所[新增驗證][ 14] tooyour Apache Cordova 應用程式。

了解如何 toouse hello Sdk。

* [Apache Cordova SDK][15]
* [ASP.NET Server SDK][1]
* [Node.js Server SDK][16]

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
