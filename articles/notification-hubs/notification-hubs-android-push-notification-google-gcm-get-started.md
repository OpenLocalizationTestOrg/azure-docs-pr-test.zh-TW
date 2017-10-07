---
title: "與 Azure 通知中心 aaaSending 推播通知 tooAndroid |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toopush 通知 tooAndroid 裝置。"
services: notification-hubs
documentationcenter: android
keywords: "推播通知,推播通知,android 推播通知"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a><span data-ttu-id="e1ef4-104">使用 Azure 通知中樞傳送推播通知 tooAndroid</span><span class="sxs-lookup"><span data-stu-id="e1ef4-104">Sending push notifications tooAndroid with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="e1ef4-105">概觀</span><span class="sxs-lookup"><span data-stu-id="e1ef4-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e1ef4-106">本主題示範使用 Google 雲端通訊 (GCM) 的推播通知。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-106">This topic demonstrates push notifications with Google Cloud Messaging (GCM).</span></span> <span data-ttu-id="e1ef4-107">如果您使用 Google Firebase 雲端傳訊 (FCM)，請參閱[FCM 與 Azure 通知中樞傳送推播通知 tooAndroid](notification-hubs-android-push-notification-google-fcm-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-107">If you are using Google's Firebase Cloud Messaging (FCM), see [Sending push notifications tooAndroid with Azure Notification Hubs and FCM](notification-hubs-android-push-notification-google-fcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="e1ef4-108">本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooan Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-108">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan Android application.</span></span>
<span data-ttu-id="e1ef4-109">您將建立可使用 Google Cloud Messaging (GCM) 接收推播通知的空白 Android app。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-109">You'll create a blank Android app that receives push notifications by using Google Cloud Messaging (GCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="e1ef4-110">此教學課程中的 hello 完成程式碼可以從 GitHub 下載[這裡](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-110">hello completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1ef4-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="e1ef4-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e1ef4-112">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e1ef4-113">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e1ef4-114">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

<span data-ttu-id="e1ef4-115">此外 tooan 有效的 Azure 帳戶先前所述，本教學課程只需要 hello 最新版本的[Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-115">In addition tooan active Azure account mentioned above, this tutorial only requires hello latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>

<span data-ttu-id="e1ef4-116">完成本教學課程是 Android app 所有其他通知中樞教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-116">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a><span data-ttu-id="e1ef4-117">建立支援 Google 雲端通訊的專案</span><span class="sxs-lookup"><span data-stu-id="e1ef4-117">Creating a project that supports Google Cloud Messaging</span></span>
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="e1ef4-118">設定新的通知中樞</span><span class="sxs-lookup"><span data-stu-id="e1ef4-118">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="e1ef4-119">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="e1ef4-119">&emsp;&emsp;6.</span></span>   <span data-ttu-id="e1ef4-120">在 hello**設定**刀鋒視窗中，選取**Notification Services**然後**Google (GCM)**。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-120">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="e1ef4-121">輸入 hello API 金鑰，然後按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-121">Enter hello API key and click **Save**.</span></span>

&emsp;&emsp;![Azure 通知中樞 - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="e1ef4-123">您的通知中樞現在是設定的 toowork 與 GCM，而且您擁有 hello 的連接字串 tooboth 註冊您的應用程式 tooreceive 及傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-123">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooboth register your app tooreceive and send push notifications.</span></span>

## <span data-ttu-id="e1ef4-124"><a id="connecting-app"></a>連接您的應用程式 toohello 通知中樞</span><span class="sxs-lookup"><span data-stu-id="e1ef4-124"><a id="connecting-app"></a>Connect your app toohello notification hub</span></span>
### <a name="create-a-new-android-project"></a><span data-ttu-id="e1ef4-125">建立新的 Android 專案</span><span class="sxs-lookup"><span data-stu-id="e1ef4-125">Create a new Android project</span></span>
1. <span data-ttu-id="e1ef4-126">在 Android Studio 中，啟動新的 Android Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-126">In Android Studio, start a new Android Studio project.</span></span>
   
   ![Android Studio - 新增專案][13]
2. <span data-ttu-id="e1ef4-128">選擇 hello**電話和平板電腦**構成要素和 hello**最低 SDK**想 toosupport。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-128">Choose hello **Phone and Tablet** form factor and hello **Minimum SDK** that you want toosupport.</span></span> <span data-ttu-id="e1ef4-129">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-129">Then click **Next**.</span></span>
   
   ![Android Studio - 專案建立工作流程][14]
3. <span data-ttu-id="e1ef4-131">選擇**空的活動**hello 主要活動，請按一下**下一步**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-131">Choose **Empty Activity** for hello main activity, click **Next**, and then click **Finish**.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="e1ef4-132">將 Google Play 服務 toohello 專案</span><span class="sxs-lookup"><span data-stu-id="e1ef4-132">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="e1ef4-133">新增 Azure 通知中樞程式庫</span><span class="sxs-lookup"><span data-stu-id="e1ef4-133">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="e1ef4-134">在 hello`Build.Gradle`檔案 hello**應用程式**，加入下列行 hello hello**相依性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-134">In hello `Build.Gradle` file for hello **app**, add hello following lines in hello **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="e1ef4-135">新增下列儲存機制之後 hello hello**相依性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-135">Add hello following repository after hello **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a><span data-ttu-id="e1ef4-136">正在更新 hello AndroidManifest.xml。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-136">Updating hello AndroidManifest.xml.</span></span>
1. <span data-ttu-id="e1ef4-137">toosupport GCM，我們必須在用過的程式碼中實作的執行個體識別碼的接聽程式服務[取得註冊權杖](https://developers.google.com/cloud-messaging/android/client#sample-register)使用[Google 的執行個體識別碼 API](https://developers.google.com/instance-id/)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-137">toosupport GCM, we must implement a Instance ID listener service in our code which is used too[obtain registration tokens](https://developers.google.com/cloud-messaging/android/client#sample-register) using [Google's Instance ID API](https://developers.google.com/instance-id/).</span></span> <span data-ttu-id="e1ef4-138">在本教學課程中，我們會命名 hello 類別`MyInstanceIDService`。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-138">In this tutorial we will name hello class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="e1ef4-139">新增下列服務定義 toohello AndroidManifest.xml 檔中的，內部 hello hello`<application>`標記。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-139">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="e1ef4-140">取代 hello`<your package>`預留位置 hello 您在 hello hello 最上方顯示的實際封裝名稱`AndroidManifest.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-140">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="e1ef4-141">一旦我們有我們 GCM 註冊語彙基元收到 hello 執行個體識別碼的 API，將會使用此太[hello Azure 通知中樞註冊](notification-hubs-push-notification-registration-management.md)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-141">Once we have received our GCM registration token from hello Instance ID API, we will use it too[register with hello Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="e1ef4-142">我們將在背景中使用 hello 支援此註冊`IntentService`名為`RegistrationIntentService`。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-142">We will support this registration in hello background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="e1ef4-143">此服務也會負責 [重新整理我們的 GCM 註冊權杖](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-143">This service will also be responsible for [refreshing our GCM registration token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens).</span></span>
   
    <span data-ttu-id="e1ef4-144">新增下列服務定義 toohello AndroidManifest.xml 檔中的，內部 hello hello`<application>`標記。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-144">Add hello following service definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="e1ef4-145">取代 hello`<your package>`預留位置 hello 您在 hello hello 最上方顯示的實際封裝名稱`AndroidManifest.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-145">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span> 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="e1ef4-146">我們也會定義接收者 tooreceive 通知。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-146">We will also define a receiver tooreceive notifications.</span></span> <span data-ttu-id="e1ef4-147">新增下列收件者定義 toohello AndroidManifest.xml 檔中的，內部 hello hello`<application>`標記。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-147">Add hello following receiver definition toohello AndroidManifest.xml file, inside hello `<application>` tag.</span></span> <span data-ttu-id="e1ef4-148">取代 hello`<your package>`預留位置 hello 您在 hello hello 最上方顯示的實際封裝名稱`AndroidManifest.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-148">Replace hello `<your package>` placeholder with hello your actual package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="e1ef4-149">新增下列必要的 GCM hello 相關權限下 hello`</application>`標記。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-149">Add hello following necessary GCM related permissions below hello  `</application>` tag.</span></span> <span data-ttu-id="e1ef4-150">請確定 tooreplace`<your package>`與 hello 套件名稱顯示在 hello hello 頂端`AndroidManifest.xml`檔案。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-150">Make sure tooreplace `<your package>` with hello package name shown at hello top of hello `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="e1ef4-151">如需這些權限的詳細資訊，請參閱 [設定適用於 Android 的 GCM 用戶端應用程式](https://developers.google.com/cloud-messaging/android/client#manifest)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-151">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a><span data-ttu-id="e1ef4-152">加入程式碼</span><span class="sxs-lookup"><span data-stu-id="e1ef4-152">Adding code</span></span>
1. <span data-ttu-id="e1ef4-153">在 hello 專案檢視，展開**應用程式** > **src** > **主要** > **java**。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-153">In hello Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="e1ef4-154">以滑鼠右鍵按一下 **java** 底下您的套件資料夾，並按一下 新增，然後按一下Java 類別。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-154">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="e1ef4-155">新增名為 `NotificationSettings` 的新類別。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-155">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - 新增 Java 類別][6]
   
    <span data-ttu-id="e1ef4-157">請確定 tooupdate hello 這些 hello 遵循 hello 的程式碼中的三個預留位置`NotificationSettings`類別：</span><span class="sxs-lookup"><span data-stu-id="e1ef4-157">Make sure tooupdate hello these three placeholders in hello following code for hello `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="e1ef4-158">**SenderId**: hello 您稍早在 hello 中取得的專案數目[Google 雲端主控台](http://cloud.google.com/console)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-158">**SenderId**: hello project number you obtained earlier in hello [Google Cloud Console](http://cloud.google.com/console).</span></span>
   * <span data-ttu-id="e1ef4-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature**中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-159">**HubListenConnectionString**: hello **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="e1ef4-160">您可以將該連接字串複製按一下**存取原則**上 hello**設定**刀鋒視窗上 hello 中樞[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-160">You can copy that connection string by clicking **Access Policies** on hello **Settings** blade of your hub on hello [Azure Portal].</span></span>
   * <span data-ttu-id="e1ef4-161">**HubName**: hello 的 hello 中樞 刀鋒視窗中會出現在通知中樞的使用 hello 名稱[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-161">**HubName**: Use hello name of your notification hub that appears in hello hub blade in hello [Azure Portal].</span></span>
     
     <span data-ttu-id="e1ef4-162">`NotificationSettings` 程式碼︰</span><span class="sxs-lookup"><span data-stu-id="e1ef4-162">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="e1ef4-163">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="e1ef4-163">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       <span data-ttu-id="e1ef4-164">}</span><span class="sxs-lookup"><span data-stu-id="e1ef4-164">}</span></span>
2. <span data-ttu-id="e1ef4-165">使用上述的 hello 步驟，加入另一個名為的新類別`MyInstanceIDService`。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-165">Using hello steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="e1ef4-166">這會是我們的執行個體識別碼接聽程式服務實作。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-166">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="e1ef4-167">此類別的 hello 程式碼會呼叫我們`IntentService`太[重新整理 hello GCM 權杖](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)hello 背景。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-167">hello code for this class will call our `IntentService` too[refresh hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in hello background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="e1ef4-168">加入另一個新的類別 tooyour 專案命名， `RegistrationIntentService`。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-168">Add another new class tooyour project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="e1ef4-169">這會是 hello 實作我們`IntentService`處理[重新整理 hello GCM 語彙基元](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)和[hello 通知中樞註冊](notification-hubs-push-notification-registration-management.md)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-169">This will be hello implementation for our `IntentService` that will handle [refreshing hello GCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with hello notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="e1ef4-170">使用下列程式碼，這個類別的 hello。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-170">Use hello following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="e1ef4-171">在您`MainActivity`類別中，加入下列 hello `import` hello 上面的陳述式的類別宣告。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-171">In your `MainActivity` class, add hello following `import` statements above hello class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="e1ef4-172">加入下列私用成員在 hello hello 類別頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-172">Add hello following private members at hello top of hello class.</span></span> <span data-ttu-id="e1ef4-173">我們會使用這些[Google 依照建議，請檢查 Google Play 服務的 hello 可用性](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-173">We will use these [check hello availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="e1ef4-174">在您`MainActivity`類別中，新增下列方法 toohello 可用性的 Google Play 服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-174">In your `MainActivity` class, add hello following method toohello availability of Google Play Services.</span></span> 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. <span data-ttu-id="e1ef4-175">在您`MainActivity`類別中，加入下列程式碼會檢查之前先呼叫 Google Play 服務的 hello 您`IntentService`tooget 您 GCM 註冊語彙基元及與您的通知中樞的註冊。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-175">In your `MainActivity` class, add hello following code that will check for Google Play Services before calling your `IntentService` tooget your GCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="e1ef4-176">在 hello `OnCreate` hello 方法`MainActivity`類別中，新增 hello 建立活動時，下列程式碼 toostart hello 註冊程序。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-176">In hello `OnCreate` method of hello `MainActivity` class, add hello following code toostart hello registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="e1ef4-177">新增這些其他方法 toohello `MainActivity` tooverify prb： 應用程式中的發生應用程式狀態及報告狀態。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-177">Add these additional methods toohello `MainActivity` tooverify app state and report status in your app.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. <span data-ttu-id="e1ef4-178">hello`ToastNotify`方法會使用 hello *"Hello World"* `TextView`控制 tooreport 狀態和持續中 hello 應用程式的通知。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-178">hello `ToastNotify` method uses hello *"Hello World"* `TextView` control tooreport status and notifications persistently in hello app.</span></span> <span data-ttu-id="e1ef4-179">在 activity_main.xml 配置中，加入下列控制項的識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-179">In your activity_main.xml layout, add hello following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="e1ef4-180">接下來，我們將我們我們 hello AndroidManifest.xml 中定義的收件者加入子類別。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-180">Next we will add a subclass for our receiver we defined in hello AndroidManifest.xml.</span></span> <span data-ttu-id="e1ef4-181">加入另一個新的類別 tooyour 專案名為`MyHandler`。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-181">Add another new class tooyour project named `MyHandler`.</span></span>
10. <span data-ttu-id="e1ef4-182">加入下列 import 陳述式在 hello 最上方的 hello `MyHandler.java`:</span><span class="sxs-lookup"><span data-stu-id="e1ef4-182">Add hello following import statements at hello top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="e1ef4-183">新增下列程式碼 hello hello`MyHandler`讓它的子類別的類別`com.microsoft.windowsazure.notifications.NotificationsHandler`。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-183">Add hello following code for hello `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="e1ef4-184">此程式碼會覆寫 hello`OnReceive`方法，所以 hello 處理常式會報告所接收的通知。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-184">This code overrides hello `OnReceive` method, so hello handler will report notifications that are received.</span></span> <span data-ttu-id="e1ef4-185">hello 處理常式也會將傳送嗨推播通知 toohello Android 的通知管理員使用 hello`sendNotification()`方法。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-185">hello handler also sends hello push notification toohello Android notification manager by using hello `sendNotification()` method.</span></span> <span data-ttu-id="e1ef4-186">hello`sendNotification()`方法應該在執行時收到通知，而且 hello 應用程式未執行。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-186">hello `sendNotification()` method should be executed when hello app is not running and a notification is received.</span></span>
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. <span data-ttu-id="e1ef4-187">在 Android Studio 中 hello 功能表列上，按一下 **建置** > **重建專案**toomake 確定任何錯誤會出現在您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-187">In Android Studio on hello menu bar, click **Build** > **Rebuild Project** toomake sure that no errors are present in your code.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="e1ef4-188">傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="e1ef4-188">Sending push notifications</span></span>
<span data-ttu-id="e1ef4-189">您可以測試應用程式中接收推播通知傳送嗨透過[Azure 入口網站]-尋找 hello**疑難排解**區段在 hello 中樞刀鋒視窗中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-189">You can test receiving push notifications in your app by sending them via hello [Azure Portal] - look for hello **Troubleshooting** Section in hello hub blade, as shown below.</span></span>

![Azure 通知中樞 - 測試傳送](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a><span data-ttu-id="e1ef4-191">（選擇性）直接從 hello 應用程式中傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="e1ef4-191">(Optional) Send push notifications directly from hello app</span></span>
<span data-ttu-id="e1ef4-192">一般來說，您會使用後端伺服器傳送通知。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-192">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="e1ef4-193">在某些情況下，您可能想直接從 hello 用戶端應用程式的 toobe 無法 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-193">For some cases, you might want toobe able toosend push notifications directly from hello client application.</span></span> <span data-ttu-id="e1ef4-194">本章節將說明如何 toosend 通知 hello 使用從用戶端 hello [Azure 通知中樞 REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-194">This section explains how toosend notifications from hello client using hello [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="e1ef4-195">在 [Android Studio 專案檢視] 中，展開 [App] > [src] > [main] > [res] > [layout]。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-195">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="e1ef4-196">開啟 hello`activity_main.xml`配置檔案，然後按一下 hello**文字**hello 檔案 tooupdate hello 文字內容索引標籤上。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-196">Open hello `activity_main.xml` layout file and click hello **Text** tab tooupdate hello text contents of hello file.</span></span> <span data-ttu-id="e1ef4-197">它與 hello 的下列程式碼將新的更新`Button`和`EditText`控制項傳送推播通知訊息 toohello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-197">Update it with hello code below, which adds new `Button` and `EditText` controls for sending push notification messages toohello notification hub.</span></span> <span data-ttu-id="e1ef4-198">之前加入這個程式碼在 hello 下方`</RelativeLayout>`。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-198">Add this code at hello bottom, just before `</RelativeLayout>`.</span></span>
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. <span data-ttu-id="e1ef4-199">在 [Android Studio 專案檢視] 中，展開 [App] > [src] > [main] > [res] > [values]。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="e1ef4-200">開啟 hello`strings.xml`檔案，然後加入新的 hello 所參考的 hello 字串值`Button`和`EditText`控制項。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-200">Open hello `strings.xml` file and add hello string values that are referenced by hello new `Button` and `EditText` controls.</span></span> <span data-ttu-id="e1ef4-201">之前加入下列底部 hello hello 檔案`</resources>`。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-201">Add these at hello bottom of hello file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="e1ef4-202">在您`NotificationSetting.java`檔案中，新增下列設定 toohello hello`NotificationSettings`類別。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-202">In your `NotificationSetting.java` file, add hello following setting toohello `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="e1ef4-203">更新`HubFullAccess`以 hello **DefaultFullSharedAccessSignature**中樞連接字串。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-203">Update `HubFullAccess` with hello **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="e1ef4-204">這個連接字串可以從 hello 複製[Azure 入口網站]按一下**存取原則**上 hello**設定**通知中樞的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-204">This connection string can be copied from hello [Azure Portal] by clicking **Access Policies** on hello **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. <span data-ttu-id="e1ef4-205">在您`MainActivity.java`file、 add hello 下列`import`hello 上面的陳述式`MainActivity`類別。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-205">In your `MainActivity.java` file, add hello following `import` statements above hello `MainActivity` class.</span></span>
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. <span data-ttu-id="e1ef4-206">在您`MainActivity.java`檔案中加入下列成員在 hello hello 最上方的 hello`MainActivity`類別。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-206">In your `MainActivity.java` file, add hello following members at hello top of hello `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="e1ef4-207">您必須建立軟體存取簽章 (SaS) 權杖的 tooauthenticate POST 要求 toosend 訊息 tooyour 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-207">You must create a Software Access Signature (SaS) token tooauthenticate a POST request toosend messages tooyour notification hub.</span></span> <span data-ttu-id="e1ef4-208">這是藉由剖析 hello hello 連接字串中的索引鍵資料和 hello 中所述，然後建立 hello SaS 權杖[Common 概念](http://msdn.microsoft.com/library/azure/dn495627.aspx)REST API 參考。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-208">This is done by parsing hello key data from hello connection string and then creating hello SaS token, as mentioned in hello [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="e1ef4-209">下列程式碼的 hello 是範例實作。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-209">hello following code is an example implementation.</span></span>
   
    <span data-ttu-id="e1ef4-210">在`MainActivity.java`，新增下列方法 toohello hello`MainActivity`類別 tooparse 連接字串。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-210">In `MainActivity.java`, add hello following method toohello `MainActivity` class tooparse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. <span data-ttu-id="e1ef4-211">在`MainActivity.java`，新增下列方法 toohello hello`MainActivity`類別 toocreate SaS 驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-211">In `MainActivity.java`, add hello following method toohello `MainActivity` class toocreate a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. <span data-ttu-id="e1ef4-212">在`MainActivity.java`，新增下列方法 toohello hello`MainActivity`類別 toohandle hello**傳送通知**按鈕按一下，然後傳送 hello 訊息 toohello 集線器使用 hello 內建的 REST API 的推播通知。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-212">In `MainActivity.java`, add hello following method toohello `MainActivity` class toohandle hello **Send Notification** button click and send hello push notification message toohello hub by using hello built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a><span data-ttu-id="e1ef4-213">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="e1ef4-213">Testing your app</span></span>
#### <a name="push-notifications-in-hello-emulator"></a><span data-ttu-id="e1ef4-214">Hello 模擬器中的推播通知</span><span class="sxs-lookup"><span data-stu-id="e1ef4-214">Push notifications in hello emulator</span></span>
<span data-ttu-id="e1ef4-215">如果您想在模擬器 tootest 推播通知，請確定模擬器映像支援您選擇您的應用程式的 hello Google API 層級。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-215">If you want tootest push notifications inside an emulator, make sure that your emulator image supports hello Google API level that you chose for your app.</span></span> <span data-ttu-id="e1ef4-216">如果您的映像不支援原生的 Google Api，您會得到 hello**服務\_不\_可用**例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-216">If your image doesn't support native Google APIs, you will end up with hello **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="e1ef4-217">此外 toohello 上述項目，確定您已加入執行模擬器，在您 Google 帳戶 tooyour**設定** > **帳戶**。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-217">In addition toohello above, ensure that you have added your Google account tooyour running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="e1ef4-218">否則，GCM 與您嘗試 tooregister 可能導致 hello**驗證\_失敗**例外狀況。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-218">Otherwise, your attempts tooregister with GCM may result in hello **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-hello-application"></a><span data-ttu-id="e1ef4-219">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1ef4-219">Running hello application</span></span>
1. <span data-ttu-id="e1ef4-220">執行 hello 應用程式，並注意 hello 註冊 ID 會報告成功註冊。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-220">Run hello app and notice that hello registration ID is reported for a successful registration.</span></span>
   
      ![在 Android 上測試 - 通道註冊][18]
2. <span data-ttu-id="e1ef4-222">輸入通知訊息 toobe 傳送 tooall hello 集線器與已註冊的 Android 裝置。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-222">Enter a notification message toobe sent tooall Android devices that have registered with hello hub.</span></span>
   
      ![在 Android 上測試 - 傳送訊息][19]

3. <span data-ttu-id="e1ef4-224">按 [ **傳送通知**]。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-224">Press **Send Notification**.</span></span> <span data-ttu-id="e1ef4-225">任何具有 hello 應用程式執行的裝置將會顯示`AlertDialog`與 hello 推播通知訊息的執行個體。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-225">Any devices that have hello app running will show an `AlertDialog` instance with hello push notification message.</span></span> <span data-ttu-id="e1ef4-226">沒有 hello 應用程式執行，但先前註冊推播通知將會收到通知 hello Android 通知管理員中的裝置。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-226">Devices that don't have hello app running but were previously registered for push notifications will receive a notification in hello Android Notification Manager.</span></span> <span data-ttu-id="e1ef4-227">可以檢視這些撥動往下從 hello 左上角。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-227">Those can be viewed by swiping down from hello upper-left corner.</span></span>
   
      ![在 Android 上測試 - 通知][21]

## <a name="next-steps"></a><span data-ttu-id="e1ef4-229">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1ef4-229">Next steps</span></span>
<span data-ttu-id="e1ef4-230">我們建議 hello[使用通知中樞 toopush 通知 toousers] hello 下一個步驟的教學課程。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-230">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="e1ef4-231">它會顯示如何從 ASP.NET 後端使用 toosend 通知標記 tootarget 特定使用者。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-231">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="e1ef4-232">如果您希望 toosegment 使用者感興趣的群組，請參閱 hello[使用通知中樞 toosend 最新消息]教學課程。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-232">If you want toosegment your users by interest groups, check out hello [Use Notification Hubs toosend breaking news] tutorial.</span></span>

<span data-ttu-id="e1ef4-233">toolearn 通知中樞的相關詳細資訊，請參閱我們[通知中樞指引]。</span><span class="sxs-lookup"><span data-stu-id="e1ef4-233">toolearn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
[使用通知中樞 toopush 通知 toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[使用通知中樞 toosend 最新消息]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure 入口網站]: https://portal.azure.com
