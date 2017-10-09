---
title: "開始使用 Android 應用程式的 Azure Mobile Engagement aaaGet"
description: "深入了解如何與 Android 應用程式的分析和推播通知的 Azure Mobile Engagement toouse。"
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>開始使用適用於 Android 應用程式的 Azure Mobile Engagement
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

本主題說明如何 toouse Azure Mobile Engagement toounderstand 應用程式使用量和如何 toosend 推播通知 toosegmented 使用者的 Android 應用程式。
本教學課程會示範簡單 hello 使用 Mobile Engagement 廣播的案例。 在此案例中，您先建立空白的 Android 應用程式，使用 Google 雲端通訊 (GCM) 來收集基本資料並接收推播通知。

## <a name="prerequisites"></a>必要條件
完成本教學課程需要 hello [Android 開發人員工具](https://developer.android.com/sdk/index.html)，包括 hello Android Studio 整合式的開發環境，以及 hello 最新版的 Android 平台。

它也需要 hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn)。

> [!IMPORTANT]
> toocomplete 本教學課程中，您需要使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started)。
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>為您的 Android 應用程式設定 Mobile Engagement
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>連接您的應用程式 toohello Mobile Engagement 後端
此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。 您可以建立基本應用程式與 Android Studio toodemonstrate hello 整合。

hello 完整的整合文件可以在 hello [Mobile Engagement Android SDK 整合](mobile-engagement-android-sdk-overview.md)。

### <a name="create-an-android-project"></a>建立 Android 專案
1. 啟動**Android Studio**，然後在 hello 快顯視窗中，選取**開始新的 Android Studio 專案**。

    ![][1]
2. 提供 App 名稱與公司網域。 記下您填入的內容，因為稍後會用到。 按一下 [下一步] 。

    ![][2]
3. 選取目標尺寸 hello 和 API 層級，然後按一下**下一步**。

   > [!NOTE]
   > Mobile Engagement 至少需要 API 層級 10 (Android 2.3.3)。
   >
   >

    ![][3]
4. 選取**空白活動**此處，也就是只有囉 」 畫面為此應用程式和按一下**下一步**。

    ![][4]
5. 最後，將保留 hello 預設值，並按一下**完成**。

    ![][5]

Android Studio 現在會建立到我們整合 Mobile Engagement hello 示範應用程式。

### <a name="include-hello-sdk-library-in-your-project"></a>包含專案中的 hello SDK 程式庫
1. 下載 hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn)。
2. 擷取 hello 封存檔案 tooa 資料夾中您的電腦。
3. Hello d hello 這個 SDK 目前版本的文件庫識別，並將它複製 toohello 剪貼簿。

      ![][6]
4. 瀏覽 toohello**專案**區段 （1） 並貼上 hello d hello (2) 的程式庫資料夾中。

      ![][7]
5. tooload hello 程式庫、 同步處理 hello 專案。

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>連接您的應用程式 tooMobile Engagement 後端以 hello 連接字串
1. 複製下列幾行程式碼到 hello （必須只能在一個位置的應用程式時，通常 hello 主要活動） 的活動建立 hello。 此範例應用程式中，開啟下 src hello MainActivity-> 主要-> java 資料夾，並加入下列 hello:

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. 解析 hello 參考，請按 Alt + Enter 或加入下列 import 陳述式的 hello:

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. 返回 toohello Azure 傳統入口網站應用程式中**連接資訊**頁面，並複製 hello**連接字串**。

      ![][9]
4. 將它貼到 hello`setConnectionString`參數，取代 hello 整個字串 hello 下列程式碼所示：

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>新增權限和服務宣告
1. 加入這些權限 toohello Manifest.xml 專案的之前或之後 hello`<application>`標記：

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare hello 代理程式服務中，加入下列程式碼之間 hello`<application>`和`</application>`標記：

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. 在您所貼上 hello 程式碼，取代`"<Your application name>"`hello 標籤中便會顯示在 hello**設定**功能表上，您可以在其中看到 hello 裝置上執行的服務。 您可以加入 hello word 「 服務 」，例如在該標籤。

### <a name="send-a-screen-toomobile-engagement"></a>傳送螢幕 tooMobile Engagement
toostart 傳送資料，請確認 hello 使用者使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。

跳過**MainActivity.java**並新增下列 tooreplace hello 基底類別的 hello **MainActivity**太**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> 如果您的基底類別不是*活動*，請參閱[進階 Android 報告](mobile-engagement-android-advanced-reporting.md)如何 tooinherit 來自不同類別。
>
>

註解下列程式行及此簡單的範例案例的 hello:

    // setSupportActionBar(toolbar);

如果您想 tookeep hello`ActionBar`中應用程式，請參閱[進階 Android 報告](mobile-engagement-android-advanced-reporting.md)。

## <a name="connect-app-with-real-time-monitoring"></a>將應用程式與即時監視連接
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>啟用推播通知與應用程式內傳訊
活動進行期間，Mobile Engagement 可讓您透過推播通知和應用程式內傳訊與使用者互動和「觸達」。 此模組會呼叫觸達 hello Mobile Engagement 入口網站中。
下列章節的 hello 設定應用程式 tooreceive 它們。

### <a name="copy-sdk-resources-in-your-project"></a>複製您專案中的 SDK 資源
1. 瀏覽後 tooyour SDK 下載內容並複製 hello **res**資料夾。

    ![][10]
2. 返回 tooAndroid Studio 中，選取 hello**主要**目錄的專案檔案，然後將它貼入 tooadd hello 資源 tooyour 專案。

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>後續步驟
跳過[Android SDK](mobile-engagement-android-sdk-overview.md) tooget 詳細 hello SDK 整合的相關知識。

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
