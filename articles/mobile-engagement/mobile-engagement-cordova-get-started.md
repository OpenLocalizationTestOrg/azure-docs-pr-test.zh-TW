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
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>開始使用 Azure Mobile Engagement for Cordova/Phonegap
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand cordova 開發應用程式使用方式及傳送推播通知 toosegmented 使用者的行動應用程式。

在本教學課程中，我們將會使用 Mac 建立空白的 Cordova 應用程式，然後整合 Mobile Engagement SDK。 它會收集基本分析資料，並針對 iOS 使用 Apple Push Notification System (APNS)、針對 Android 使用 Google Cloud Messaging (GCM) 接收推播通知。 我們將會部署這個 tooan iOS 或 Android 裝置上的進行測試。 

> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started)。
> 
> 

本教學課程必須 hello 下列需求：

* 您可以從 Mac App Store （適用於部署 tooiOS） 安裝 XCode
* [Android SDK 及模擬器](http://developer.android.com/sdk/installing/index.html)（適用於部署 tooAndroid）
* 推播通知憑證 (.p12)，您可以在 Apple Dev Center for APNS 取得
* 您可以從您的 Google Developer Console for GCM 取得的 GCM 專案編號
* [Mobile Engagement Cordova 外掛程式](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> 您可以尋找 hello 原始碼並在 hello Cordova 外掛程式 hello 讀我檔案[GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>為您的 Cordova App 設定 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 < 基本整合 > hello 最小設定必要的 toocollect 資料及傳送推播通知。 

我們將使用 Cordova toodemonstrate hello 整合，以建立基本應用程式：

### <a name="create-a-new-cordova-project"></a>建立新的 Cordova 專案
1. 啟動*終端機*視窗上遵循這將會從 hello 預設範本來建立新的 Cordova 專案您 Mac 電腦，然後輸入 hello。 請確定該 hello 發行設定檔，您最終使用 toodeploy iOS 應用程式使用 'com.mycompany.myapp' hello 應用程式識別碼。 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. 執行下列 tooconfigure hello 專案**iOS**和 hello iOS 模擬器中執行它：
   
        $ cordova platform add ios 
        $ cordova run ios
3. 執行下列 tooconfigure hello 專案**Android**和 hello Android 模擬器中執行程式。 請確定您的 Android SDK 模擬器設定有其目標為 Google Api (Google Inc.) 與 hello CPU / ABI 為 Google Api ARM。  
   
        $ cordova platform add android
        $ cordova run android
4. 新增 hello Cordova 主控台外掛程式。 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>連接您的應用程式 tooMobile Engagement 後端
1. 同時提供 hello 變數值 tooconfigure hello 外掛程式安裝 hello Azure Mobile Engagement Cordova 外掛程式：
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Android 到達圖示*： 必須是不含任何擴充功能，也不 drawable 前置詞的 hello 資源 hello 名稱 (例如： mynotificationicon)，和 hello 圖示檔案必須複製到您的 android 專案 (平台/android/res/drawable)

*iOS 到達圖示*： 必須是 hello hello 其副檔名的資源名稱 (ex: mynotificationicon.png)，和 hello 圖示檔必須加入至您的 iOS 專案，使用 XCode （使用 hello 加入 [檔案] 功能表）

## <a id="monitor"></a>啟用即時監視
1. 在 [hello Cordova 專案-編輯**www/js/index.js** tooadd hello 呼叫一次 hello tooMobile Engagement toodeclare 新活動*deviceReady*在接收到事件。
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. 執行 hello 應用程式：
   
   * **對於 iOS**
     
       在`Terminal`視窗啟動新的模擬器執行個體中的應用程式藉由執行下列 hello:
     
           cordova run ios
   * **對於 Android**
     
       在`Terminal`視窗啟動新的模擬器執行個體中的應用程式藉由執行下列 hello:
     
           cordova run android
3. 您可以看到 hello 主控台記錄檔中的 hello 下列：
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>將 App 與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>啟用推播通知與應用程式內傳訊
Mobile Engagement 可讓您 toointeract 與您使用推播通知及應用程式內訊息的活動 hello 內容中的使用者。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
hello 下列各節將會安裝應用程式 tooreceive 它們。

### <a name="configure-push-credentials-for-mobile-engagement"></a>設定 Mobile Engagement 的推播認證
tooallow Mobile Engagement toosend 推播通知您的身分，您需要 toogrant 它存取 tooyour Apple iOS 憑證或 GCM 伺服器 API 金鑰。 

1. 瀏覽 tooyour Mobile Engagement 入口網站。 請確定您在 hello 應用程式，我們正在使用此專案，然後按一下 [hello **Engage** hello 底部的按鈕：
   
    ![][1]
2. 在您 Engagement 入口網站中，您將登陸 hello 設定] 頁面中。 從該處，按一下 [hello**原生推送**> 一節：
   
    ![][2]
3. 設定 iOS 憑證/GCM Server API 金鑰
   
    **[iOS]**
   
    a. 選取您的 .p12、將它上傳並輸入您的密碼：
   
    ![][3]
   
    **[Android]**
   
    a. 按一下編輯 hello] 圖示的前面**API 金鑰**hello GCM 設定] 區段中，而且其中會顯示 hello 快顯視窗中，貼 hello GCM 伺服器金鑰，然後按一下**確定**。 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>啟用 hello Cordova 應用程式中的推播通知
編輯**www/js/index.js** tooadd hello 呼叫 tooMobile Engagement toorequest 推播通知，並宣告處理常式：

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>執行 hello 應用程式
**[iOS]**

1. 我們將使用 XCode toobuild 和部署 hello hello 裝置 tootest 推播通知上的應用程式，因為 iOS 只允許推播通知 tooan 實際裝置。 請移 toohello 位置建立您的 Cordova 專案的位置，並瀏覽過**...\platforms\ios**位置。 Hello 原生的.xcodeproj 檔案，即可在 XCode 中開啟。 
2. 建置和部署的 hello Cordova 應用程式 toohello iOS 裝置使用有 hello 佈建設定檔將包含您剛剛上傳 toohello Mobile Engagement 入口網站和應用程式識別碼比對符合您在建立時所提供的其中一個 hello hello hello 憑證 hello 帳戶hello Cordova 應用程式。 您可以簽出 hello*配套識別碼*中您**資源\*-info.plist**檔案在 XCode toomatch 它註冊。 
3. 您會看見 hello 標準 iOS 快顯視窗指出該 hello 應用程式在裝置上的要求權限 toosend 通知。 授與 hello 權限。 

**[Android]**

GCM 通知支援 hello Android 模擬器上時，您可以直接使用 hello 模擬器 toorun hello Android 應用程式。 

    cordova run android

## <a id="send"></a>傳送通知 tooyour 應用程式
現在，我們將建立簡單的推播通知活動將傳送嗨裝置上執行的推播 tooyour 應用程式：

1. 瀏覽 toohello**到達**] 索引標籤中您的 Mobile Engagement 入口網站
2. 按一下**新的 Announcement** toocreate 您的推播宣傳活動
   
    ![][6]
3. 您的活動提供輸入 toocreate **[Android]**
   
   * 為您的行銷活動提供 **名稱** 。 
   * 選取 hello**傳遞類型**為*系統通知**簡單*
   * 選取 hello**傳遞時間**為*「 任何時間 」*
   * 提供**標題**您為 hello 第一行 hello 推播通知。
   * 提供**訊息**針對您要做為 hello 訊息內文的通知。 
     
     ![][11]
4. 您的活動提供輸入 toocreate **[iOS]**
   
   * 為您的行銷活動提供 **名稱** 。 
   * 選取 hello**傳遞時間**為*「 不足應用程式只"*
   * 提供**標題**您為 hello 第一行 hello 推播通知。
   * 提供**訊息**針對您要做為 hello 訊息內文的通知。 
     
     ![][12]
5. 向下捲動，並在 hello 內容區段選取**僅限通知**
   
    ![][8]
6. [選用] 您也可以提供動作 URL。 請確定它會使用設定 hello 外掛程式時，提供的 URL 配置**AZME\_重新導向\_URL**變數例如*myapp://test*。  
7. 您已完成設定 hello 最基本活動可能。 現在，向下捲動並按一下 hello**建立**按鈕 toosave 您的活動。
8. 最後 **啟用** 您的行銷活動
   
    ![][10]
9. 您現在應該會在裝置或模擬器上看到推播通知，做為此行銷活動的一部分。 

## <a id="next-steps"></a>後續步驟
[可用於 Cordova Mobile Engagement SDK 之所有方法的概觀](https://github.com/Azure/azure-mobile-engagement-cordova)

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

