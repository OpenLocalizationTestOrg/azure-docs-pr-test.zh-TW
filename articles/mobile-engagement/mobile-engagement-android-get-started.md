---
title: "開始使用 Android 應用程式 Azure Mobile Engagement"
description: "了解如何使用 Android 應用程式的 Azure Mobile Engagement 與分析和推播通知。"
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
ms.openlocfilehash: dc255a930bf71e6ef6d964bc5e3472a38ce4e467
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a><span data-ttu-id="2f10c-103">開始使用適用於 Android 應用程式的 Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2f10c-103">Get started with Azure Mobile Engagement for Android apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="2f10c-104">本主題說明如何使用 Azure Mobile Engagement 來了解您應用程式的使用情形，以及如何將推播通知傳送給 Android 應用程式的分段使用者。</span><span class="sxs-lookup"><span data-stu-id="2f10c-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of an Android application.</span></span>
<span data-ttu-id="2f10c-105">本教學課程將示範使用 Mobile Engagement 的簡單廣播案例。</span><span class="sxs-lookup"><span data-stu-id="2f10c-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="2f10c-106">在此案例中，您先建立空白的 Android 應用程式，使用 Google 雲端通訊 (GCM) 來收集基本資料並接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="2f10c-106">In it, you create a blank Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f10c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="2f10c-107">Prerequisites</span></span>
<span data-ttu-id="2f10c-108">完成本教學課程需要 [Android Developer Tools](https://developer.android.com/sdk/index.html)，其中包括 Android Studio 整合式開發環境，以及最新的 Android 平台。</span><span class="sxs-lookup"><span data-stu-id="2f10c-108">Completing this tutorial requires the [Android Developer Tools](https://developer.android.com/sdk/index.html), which includes the Android Studio integrated development environment, and the latest Android platform.</span></span>

<span data-ttu-id="2f10c-109">還需要 [Mobile Engagement Android SDK](https://aka.ms/vq9mfn)。</span><span class="sxs-lookup"><span data-stu-id="2f10c-109">It also requires the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f10c-110">若要完成此教學課程，您需要一個有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2f10c-110">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="2f10c-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2f10c-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2f10c-112">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started)。</span><span class="sxs-lookup"><span data-stu-id="2f10c-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).</span></span>
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a><span data-ttu-id="2f10c-113">為您的 Android 應用程式設定 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2f10c-113">Set up Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="2f10c-114">將您的應用程式連線至 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="2f10c-114">Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="2f10c-115">本教學課程將說明「基本整合」，這是收集資料及傳送推播通知時必要的最低設定。</span><span class="sxs-lookup"><span data-stu-id="2f10c-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="2f10c-116">您使用 Android Studio 建立一個基本應用程式來示範整合。</span><span class="sxs-lookup"><span data-stu-id="2f10c-116">You create a basic app with Android Studio to demonstrate the integration.</span></span>

<span data-ttu-id="2f10c-117">完整的整合文件位於 [Mobile Engagement Android SDK 整合](mobile-engagement-android-sdk-overview.md)中。</span><span class="sxs-lookup"><span data-stu-id="2f10c-117">The complete integration documentation can be found in the [Mobile Engagement Android SDK integration](mobile-engagement-android-sdk-overview.md).</span></span>

### <a name="create-an-android-project"></a><span data-ttu-id="2f10c-118">建立 Android 專案</span><span class="sxs-lookup"><span data-stu-id="2f10c-118">Create an Android project</span></span>
1. <span data-ttu-id="2f10c-119">啟動 **Android Studio**，然後在快顯視窗中選取 [開始新的 Android Studio 專案]。</span><span class="sxs-lookup"><span data-stu-id="2f10c-119">Start **Android Studio**, and in the pop-up, select **Start a new Android Studio project**.</span></span>

    ![][1]
2. <span data-ttu-id="2f10c-120">提供 App 名稱與公司網域。</span><span class="sxs-lookup"><span data-stu-id="2f10c-120">Provide an app name and company domain.</span></span> <span data-ttu-id="2f10c-121">記下您填入的內容，因為稍後會用到。</span><span class="sxs-lookup"><span data-stu-id="2f10c-121">Make a note of what you are filling, because you need it later.</span></span> <span data-ttu-id="2f10c-122">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2f10c-122">Click **Next**.</span></span>

    ![][2]
3. <span data-ttu-id="2f10c-123">選取目標尺寸和 API 層級，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2f10c-123">Select the target form factor and API level, and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f10c-124">Mobile Engagement 至少需要 API 層級 10 (Android 2.3.3)。</span><span class="sxs-lookup"><span data-stu-id="2f10c-124">Mobile Engagement requires API level 10 minimum (Android 2.3.3).</span></span>
   >
   >

    ![][3]
4. <span data-ttu-id="2f10c-125">在此處選取 [空白活動]，這是此應用程式唯一的畫面，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2f10c-125">Select **Blank Activity** here, which is the only screen for this app and click **Next**.</span></span>

    ![][4]
5. <span data-ttu-id="2f10c-126">最後，依原樣保留預設值，然後按一下 [完成] 。</span><span class="sxs-lookup"><span data-stu-id="2f10c-126">Finally, leave the defaults as is and click **Finish**.</span></span>

    ![][5]

<span data-ttu-id="2f10c-127">Android Studio 現在要建立會和 Mobile Engagement 整合的示範應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f10c-127">Android Studio now creates the demo app into which we integrate Mobile Engagement.</span></span>

### <a name="include-the-sdk-library-in-your-project"></a><span data-ttu-id="2f10c-128">在您的專案中包含 SDK 程式庫</span><span class="sxs-lookup"><span data-stu-id="2f10c-128">Include the SDK library in your project</span></span>
1. <span data-ttu-id="2f10c-129">下載 [Mobile Engagement Android SDK](https://aka.ms/vq9mfn)。</span><span class="sxs-lookup"><span data-stu-id="2f10c-129">Download the [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).</span></span>
2. <span data-ttu-id="2f10c-130">將封存檔案解壓縮至電腦中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2f10c-130">Extract the archive file to a folder in your computer.</span></span>
3. <span data-ttu-id="2f10c-131">找出此 SDK 目前版本的 .jar 程式庫，並將它複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="2f10c-131">Identify the .jar library for the current version of this SDK and copy it to the Clipboard.</span></span>

      ![][6]
4. <span data-ttu-id="2f10c-132">瀏覽到 [專案]  區段 (1)，然後將 .jar 貼到 libs 資料夾 (2)。</span><span class="sxs-lookup"><span data-stu-id="2f10c-132">Navigate to the **Project** section (1) and paste the .jar in the libs folder (2).</span></span>

      ![][7]
5. <span data-ttu-id="2f10c-133">若要載入程式庫，請同步處理專案。</span><span class="sxs-lookup"><span data-stu-id="2f10c-133">To load the library, sync the project .</span></span>

      ![][8]

### <a name="connect-your-app-to-mobile-engagement-backend-with-the-connection-string"></a><span data-ttu-id="2f10c-134">使用「連線字串」將您的應用程式連線到 Mobile Engagement 後端</span><span class="sxs-lookup"><span data-stu-id="2f10c-134">Connect your app to Mobile Engagement backend with the Connection String</span></span>
1. <span data-ttu-id="2f10c-135">將下列程式碼行複製到活動建立中 (必須只在應用程式中的一個位置完成，通常是主要活動)。</span><span class="sxs-lookup"><span data-stu-id="2f10c-135">Copy the following lines of code into the activity creation (must be done only in one place of your application, usually the main activity).</span></span> <span data-ttu-id="2f10c-136">針對此範例 App，開啟 src -> main -> java 資料夾下方的 MainActivity，然後新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="2f10c-136">For this sample app, open up the MainActivity under src -> main -> java folder and add the following:</span></span>

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. <span data-ttu-id="2f10c-137">按 Alt + Enter 鍵或新增下列匯入陳述式來解析參考：</span><span class="sxs-lookup"><span data-stu-id="2f10c-137">Resolve the references by pressing Alt + Enter or adding the following import statements:</span></span>

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. <span data-ttu-id="2f10c-138">回到 Azure 傳統入口網站中您應用程式的 [連線資訊] 頁面，並複製 [連接字串]。</span><span class="sxs-lookup"><span data-stu-id="2f10c-138">Go back to the Azure Classic Portal in your app's **Connection Info** page and copy the **Connection String**.</span></span>

      ![][9]
4. <span data-ttu-id="2f10c-139">將它貼到 `setConnectionString` 參數內，取代如下列程式碼所示的整個字串︰</span><span class="sxs-lookup"><span data-stu-id="2f10c-139">Paste it into the `setConnectionString` parameter, replacing the entire string shown in the following code:</span></span>

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="2f10c-140">新增權限和服務宣告</span><span class="sxs-lookup"><span data-stu-id="2f10c-140">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="2f10c-141">將這些權限加入至您專案的 Manifest.xml 中，緊接在 `<application>` 標記之前或之後：</span><span class="sxs-lookup"><span data-stu-id="2f10c-141">Add these permissions to the Manifest.xml of your project immediately before or after the `<application>` tag:</span></span>

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. <span data-ttu-id="2f10c-142">若要宣告代理程式服務，在 `<application>` 和 `</application>` 標籤之間新增此程式碼：</span><span class="sxs-lookup"><span data-stu-id="2f10c-142">To declare the agent service, add this code between the `<application>` and `</application>` tags:</span></span>

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. <span data-ttu-id="2f10c-143">在您貼上的程式碼內，取代標籤中的 `"<Your application name>"`，標籤會顯示在 [設定] 功能表中，該處可以看到裝置上執行的服務。</span><span class="sxs-lookup"><span data-stu-id="2f10c-143">In the code you pasted, replace `"<Your application name>"` in the label, which is displayed in the **Settings** menu where you can see services running on the device.</span></span> <span data-ttu-id="2f10c-144">例如，您可以在該標籤中加入「服務」這個字。</span><span class="sxs-lookup"><span data-stu-id="2f10c-144">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="2f10c-145">傳送畫面到 Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="2f10c-145">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="2f10c-146">若要開始傳送資料並確定使用者正在使用，您必須至少將一個畫面 (活動) 傳送到 Mobile Engagement 後端。</span><span class="sxs-lookup"><span data-stu-id="2f10c-146">To start sending data and ensure that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

<span data-ttu-id="2f10c-147">請前往 **MainActivity.java**，然後新增下列項目，以便將 **MainActivity** 的基底類別取代為 **EngagementActivity**：</span><span class="sxs-lookup"><span data-stu-id="2f10c-147">Go to **MainActivity.java** and add the following to replace the base class of **MainActivity** to **EngagementActivity**:</span></span>

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> <span data-ttu-id="2f10c-148">如果基底類別不是 *Activity*，請參閱[進階 Android 報告](mobile-engagement-android-advanced-reporting.md)以了解如何從不同的類別繼承。</span><span class="sxs-lookup"><span data-stu-id="2f10c-148">If your base class is not *Activity*, consult [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md) for how to inherit from different classes.</span></span>
>
>

<span data-ttu-id="2f10c-149">針對此簡單範例案例，在下一行進行註解：</span><span class="sxs-lookup"><span data-stu-id="2f10c-149">Comment out the following line for this simple sample scenario:</span></span>

    // setSupportActionBar(toolbar);

<span data-ttu-id="2f10c-150">如果您想要將 `ActionBar` 保留在應用程式中，請參閱 [進階 Android 報告](mobile-engagement-android-advanced-reporting.md)。</span><span class="sxs-lookup"><span data-stu-id="2f10c-150">If you want to keep the `ActionBar` in your app, see [Advanced Android Reporting](mobile-engagement-android-advanced-reporting.md).</span></span>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="2f10c-151">將應用程式與即時監視連接</span><span class="sxs-lookup"><span data-stu-id="2f10c-151">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a><span data-ttu-id="2f10c-152">啟用推播通知與應用程式內傳訊</span><span class="sxs-lookup"><span data-stu-id="2f10c-152">Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="2f10c-153">活動進行期間，Mobile Engagement 可讓您透過推播通知和應用程式內傳訊與使用者互動和「觸達」。</span><span class="sxs-lookup"><span data-stu-id="2f10c-153">During a campaign, Mobile Engagement lets you interact with and REACH your users with push notifications and in-app messaging.</span></span> <span data-ttu-id="2f10c-154">此模組在 Mobile Engagement 入口網站中稱為觸達 (REACH)。</span><span class="sxs-lookup"><span data-stu-id="2f10c-154">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="2f10c-155">接下來的一節將設定您的應用程式來接收它們。</span><span class="sxs-lookup"><span data-stu-id="2f10c-155">The following section sets up your app to receive them.</span></span>

### <a name="copy-sdk-resources-in-your-project"></a><span data-ttu-id="2f10c-156">複製您專案中的 SDK 資源</span><span class="sxs-lookup"><span data-stu-id="2f10c-156">Copy SDK resources in your project</span></span>
1. <span data-ttu-id="2f10c-157">瀏覽回您的 SDK 下載內容，並且複製 **res** 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2f10c-157">Navigate back to your SDK download content and copy the **res** folder.</span></span>

    ![][10]
2. <span data-ttu-id="2f10c-158">返回 Android Studio，選取專案檔案的 **main** 目錄，然後貼上以將資源加入您的專案。</span><span class="sxs-lookup"><span data-stu-id="2f10c-158">Go back to Android Studio, select the **main** directory of your project files, and then paste it to add the resources to your project.</span></span>

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="2f10c-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f10c-159">Next steps</span></span>
<span data-ttu-id="2f10c-160">移至 [Android SDK](mobile-engagement-android-sdk-overview.md) 以取得有關 SDK 整合的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2f10c-160">Go to [Android SDK](mobile-engagement-android-sdk-overview.md) to get detailed knowledge about the SDK integration.</span></span>

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
