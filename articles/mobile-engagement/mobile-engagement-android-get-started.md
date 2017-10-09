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
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="abda9-103">開始使用適用於 Android 應用程式的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="abda9-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="abda9-104">本主題說明如何 toouse Azure Mobile Engagement toounderstand 應用程式使用量和如何 toosend 推播通知 toosegmented 使用者的 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="abda9-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of an Android application.</span></span>
<span data-ttu-id="abda9-105">本教學課程會示範簡單 hello 使用 Mobile Engagement 廣播的案例。</span><span class="sxs-lookup"><span data-stu-id="abda9-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="abda9-106">在此案例中，您先建立空白的 Android 應用程式，使用 Google 雲端通訊 (GCM) 來收集基本資料並接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="abda9-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abda9-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="abda9-107">Prerequisites</span></span>
<span data-ttu-id="abda9-108">完成本教學課程需要 hello [Android 開發人員工具](https://developer.android.com/sdk/index.html)，包括 hello Android Studio 整合式的開發環境，以及 hello 最新版的 Android 平台。</span><span class="sxs-lookup"><span data-stu-id="abda9-108">Completing this tutorial requires hello [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes hello Android Studio integrated development environment, and hello latest Android platform.</span></span>

<span data-ttu-id="abda9-109">它也需要 hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn)。</span><span class="sxs-lookup"><span data-stu-id="abda9-109">It also requires hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abda9-110">toocomplete 本教學課程中，您需要使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="abda9-110">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="abda9-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="abda9-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="abda9-112">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started)。</span><span class="sxs-lookup"><span data-stu-id="abda9-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="abda9-113">為您的 Android 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="abda9-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="abda9-114">連接您的應用程式 toohello Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="abda9-114">Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="abda9-115">此教學課程提供 < 基本整合 >，其最小的 hello 設定必要的 toocollect 資料，並傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="abda9-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="abda9-116">您可以建立基本應用程式與 Android Studio toodemonstrate hello 整合。</span><span class="sxs-lookup"><span data-stu-id="abda9-116">You create a basic app with Android Studio toodemonstrate hello integration.</span></span>

<span data-ttu-id="abda9-117">hello 完整的整合文件可以在 hello [Mobile Engagement Android SDK 整合](mobile-engagement-android-sdk-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="abda9-117">hello complete integration documentation can be found in hello [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="abda9-118">建立 Android 專案</span><span class="sxs-lookup"><span data-stu-id="abda9-118">Create an Android project</span></span>
1. <span data-ttu-id="abda9-119">啟動**Android Studio**，然後在 hello 快顯視窗中，選取**開始新的 Android Studio 專案**。</span><span class="sxs-lookup"><span data-stu-id="abda9-119">Start **Android Studio**, and in hello pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="abda9-120">提供 App 名稱與公司網域。</span><span class="sxs-lookup"><span data-stu-id="abda9-120">Provide an app name and company domain.</span></span> <span data-ttu-id="abda9-121">記下您填入的內容，因為稍後會用到。</span><span class="sxs-lookup"><span data-stu-id="abda9-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="abda9-122">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="abda9-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="abda9-123">選取目標尺寸 hello 和 API 層級，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="abda9-123">Select hello target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="abda9-124">Mobile Engagement 至少需要 API 層級 10 (Android 2.3.3)。</span><span class="sxs-lookup"><span data-stu-id="abda9-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="abda9-125">選取**空白活動**此處，也就是只有囉 」 畫面為此應用程式和按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="abda9-125">Select **Blank Activity** here, which is hello only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="abda9-126">最後，將保留 hello 預設值，並按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="abda9-126">Finally, leave hello defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="abda9-127">Android Studio 現在會建立到我們整合 Mobile Engagement hello 示範應用程式。</span><span class="sxs-lookup"><span data-stu-id="abda9-127">Android Studio now creates hello demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-hello-sdk-library-in-your-project"></a><span data-ttu-id="abda9-128">包含專案中的 hello SDK 程式庫</span><span class="sxs-lookup"><span data-stu-id="abda9-128">Include hello SDK library in your project</span></span>
1. <span data-ttu-id="abda9-129">下載 hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn)。</span><span class="sxs-lookup"><span data-stu-id="abda9-129">Download hello [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="abda9-130">擷取 hello 封存檔案 tooa 資料夾中您的電腦。</span><span class="sxs-lookup"><span data-stu-id="abda9-130">Extract hello archive file tooa folder in your computer.</span></span>
3. <span data-ttu-id="abda9-131">Hello d hello 這個 SDK 目前版本的文件庫識別，並將它複製 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="abda9-131">Identify hello .jar library for hello current version of this SDK and copy it toohello Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="abda9-132">瀏覽 toohello**專案**區段 （1） 並貼上 hello d hello (2) 的程式庫資料夾中。</span><span class="sxs-lookup"><span data-stu-id="abda9-132">Navigate toohello **Project** section (1) and paste hello .jar in hello libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="abda9-133">tooload hello 程式庫、 同步處理 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="abda9-133">tooload hello library, sync hello project .</span></span>

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a><span data-ttu-id="abda9-134">連接您的應用程式 tooMobile Engagement 後端以 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="abda9-134">Connect your app tooMobile Engagement backend with hello Connection String</span></span>
1. <span data-ttu-id="abda9-135">複製下列幾行程式碼到 hello （必須只能在一個位置的應用程式時，通常 hello 主要活動） 的活動建立 hello。</span><span class="sxs-lookup"><span data-stu-id="abda9-135">Copy hello following lines of code into hello activity creation (must be done only in one place of your application, usually hello main activity).</span></span> <span data-ttu-id="abda9-136">此範例應用程式中，開啟下 src hello MainActivity-> 主要-> java 資料夾，並加入下列 hello:</span><span class="sxs-lookup"><span data-stu-id="abda9-136">For this sample app, open up hello MainActivity under src -> main -> java folder and add hello following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="abda9-137">解析 hello 參考，請按 Alt + Enter 或加入下列 import 陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="abda9-137">Resolve hello references by pressing Alt + Enter or adding hello following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="abda9-138">返回 toohello Azure 傳統入口網站應用程式中**連接資訊**頁面，並複製 hello**連接字串**。</span><span class="sxs-lookup"><span data-stu-id="abda9-138">Go back toohello Azure Classic Portal in your app's **Connection Info** page and copy hello **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="abda9-139">將它貼到 hello`setConnectionString`參數，取代 hello 整個字串 hello 下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="abda9-139">Paste it into hello `setConnectionString` parameter, replacing hello entire string shown in hello following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="abda9-140">新增權限和服務宣告</span><span class="sxs-lookup"><span data-stu-id="abda9-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="abda9-141">加入這些權限 toohello Manifest.xml 專案的之前或之後 hello`<application>`標記：</span><span class="sxs-lookup"><span data-stu-id="abda9-141">Add these permissions toohello Manifest.xml of your project immediately before or after hello `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="abda9-142">toodeclare hello 代理程式服務中，加入下列程式碼之間 hello`<application>`和`</application>`標記：</span><span class="sxs-lookup"><span data-stu-id="abda9-142">toodeclare hello agent service, add this code between hello `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="abda9-143">在您所貼上 hello 程式碼，取代`"<Your application name>"`hello 標籤中便會顯示在 hello**設定**功能表上，您可以在其中看到 hello 裝置上執行的服務。</span><span class="sxs-lookup"><span data-stu-id="abda9-143">In hello code you pasted, replace `"<Your application name>"` in hello label, which is displayed in hello **Settings** menu where you can see services running on hello device.</span></span> <span data-ttu-id="abda9-144">您可以加入 hello word 「 服務 」，例如在該標籤。</span><span class="sxs-lookup"><span data-stu-id="abda9-144">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="abda9-145">傳送螢幕 tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="abda9-145">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="abda9-146">toostart 傳送資料，請確認 hello 使用者使用中，您必須傳送至少一個螢幕 （活動） toohello Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="abda9-146">toostart sending data and ensure that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

<span data-ttu-id="abda9-147">跳過**MainActivity.java**並新增下列 tooreplace hello 基底類別的 hello **MainActivity**太**EngagementActivity**:</span><span class="sxs-lookup"><span data-stu-id="abda9-147">Go too**MainActivity.java** and add hello following tooreplace hello base class of **MainActivity** too**EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="abda9-148">如果您的基底類別不是*活動*，請參閱[進階 Android 報告](mobile-engagement-android-advanced-reporting.md)如何 tooinherit 來自不同類別。</span><span class="sxs-lookup"><span data-stu-id="abda9-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how tooinherit from different classes.</span></span>
>
>

<span data-ttu-id="abda9-149">註解下列程式行及此簡單的範例案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="abda9-149">Comment out hello following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="abda9-150">如果您想 tookeep hello`ActionBar`中應用程式，請參閱[進階 Android 報告](mobile-engagement-android-advanced-reporting.md)。</span><span class="sxs-lookup"><span data-stu-id="abda9-150">If you want tookeep hello `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="abda9-151">將應用程式與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="abda9-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="abda9-152">啟用推播通知與應用程式內傳訊</span><span class="sxs-lookup"><span data-stu-id="abda9-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="abda9-153">活動進行期間，Mobile Engagement 可讓您透過推播通知和應用程式內傳訊與使用者互動和「觸達」。</span><span class="sxs-lookup"><span data-stu-id="abda9-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="abda9-154">此模組會呼叫觸達 hello Mobile Engagement 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="abda9-154">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="abda9-155">下列章節的 hello 設定應用程式 tooreceive 它們。</span><span class="sxs-lookup"><span data-stu-id="abda9-155">hello following section sets up your app tooreceive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="abda9-156">複製您專案中的 SDK 資源</span><span class="sxs-lookup"><span data-stu-id="abda9-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="abda9-157">瀏覽後 tooyour SDK 下載內容並複製 hello **res**資料夾。</span><span class="sxs-lookup"><span data-stu-id="abda9-157">Navigate back tooyour SDK download content and copy hello **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="abda9-158">返回 tooAndroid Studio 中，選取 hello**主要**目錄的專案檔案，然後將它貼入 tooadd hello 資源 tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="abda9-158">Go back tooAndroid Studio, select hello **main** directory of your project files, and then paste it tooadd hello resources tooyour project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="abda9-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abda9-159">Next steps</span></span>
<span data-ttu-id="abda9-160">跳過[Android SDK](mobile-engagement-android-sdk-overview.md) tooget 詳細 hello SDK 整合的相關知識。</span><span class="sxs-lookup"><span data-stu-id="abda9-160">Go too[Android SDK](mobile-engagement-android-sdk-overview.md) tooget detailed knowledge about hello SDK integration.</span></span>

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
