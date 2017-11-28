---
title: "使用 Azure 通知中樞和 Firebase 雲端通訊將推播通知傳送至 Android | Microsoft Docs"
description: "在本教學課程中，您會了解如何使用 Azure 通知中樞和 Firebase 雲端通訊，將通知推播到 Android 裝置。"
services: notification-hubs
documentationcenter: android
keywords: "推播通知,推播通知,android 推播通知,fcm,firebase 雲端通訊"
author: ysxu
manager: erikre
editor: 
ms.assetid: 02298560-da61-4bbb-b07c-e79bd520e420
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/14/2016
ms.author: yuaxu
ms.openlocfilehash: 45a3fa5c7190e039fd637c78a41eeb3f6ede9bc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a><span data-ttu-id="8decc-104">使用 Azure 通知中樞將推播通知傳送至 Android</span><span class="sxs-lookup"><span data-stu-id="8decc-104">Sending push notifications to Android with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="8decc-105">概觀</span><span class="sxs-lookup"><span data-stu-id="8decc-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8decc-106">本主題示範使用 Google Firebase 雲端通訊 (FCM) 的推播通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-106">This topic demonstrates push notifications with Google Firebase Cloud Messaging (FCM).</span></span> <span data-ttu-id="8decc-107">如果您仍然使用 Google 雲端通訊 (GCM)，請參閱 [使用 Azure 通知中樞和 GCM 將推播通知傳送至 Android](notification-hubs-android-push-notification-google-gcm-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8decc-107">If you are still using Google Cloud Messaging (GCM), see [Sending push notifications to Android with Azure Notification Hubs and GCM](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

<span data-ttu-id="8decc-108">本教學課程說明如何使用 Azure 通知中樞和 Firebase 雲端通訊，將推播通知傳送到 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8decc-108">This tutorial shows you how to use Azure Notification Hubs and Firebase Cloud Messaging to send push notifications to an Android application.</span></span>
<span data-ttu-id="8decc-109">您將建立空白 Android 應用程式，其可使用 Firebase 雲端通訊 (FCM) 接收推播通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-109">You'll create a blank Android app that receives push notifications by using Firebase Cloud Messaging (FCM).</span></span>

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="8decc-110">您可以從 [此處](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase)的 GitHub 下載本教學課程的完整程式碼。</span><span class="sxs-lookup"><span data-stu-id="8decc-110">The completed code for this tutorial can be downloaded from GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStartedFirebase).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8decc-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="8decc-111">Prerequisites</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8decc-112">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8decc-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8decc-113">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8decc-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8decc-114">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started)。</span><span class="sxs-lookup"><span data-stu-id="8decc-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).</span></span>
> 
> 

* <span data-ttu-id="8decc-115">除了上述的作用中 Azure 帳戶，本教學課程需要最新版的 [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)。</span><span class="sxs-lookup"><span data-stu-id="8decc-115">In addition to an active Azure account mentioned above, this tutorial requires the latest version of [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).</span></span>
* <span data-ttu-id="8decc-116">適用於 Firebase 雲端通訊的 Android 2.3 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8decc-116">Android 2.3 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="8decc-117">適用於 Firebase 雲端通訊的 Google Repository 修訂版本 27 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8decc-117">Google Repository revision 27 or higher is required for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="8decc-118">適用於 Firebase 雲端通訊的 Google Play Services 9.0.2 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8decc-118">Google Play Services 9.0.2 or higher for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="8decc-119">完成本教學課程是 Android app 所有其他通知中樞教學課程的先決條件。</span><span class="sxs-lookup"><span data-stu-id="8decc-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Android apps.</span></span>

## <a name="create-a-new-android-studio-project"></a><span data-ttu-id="8decc-120">建立新的 Android Studio 專案</span><span class="sxs-lookup"><span data-stu-id="8decc-120">Create a new Android Studio Project</span></span>
1. <span data-ttu-id="8decc-121">在 Android Studio 中，啟動新的 Android Studio 專案。</span><span class="sxs-lookup"><span data-stu-id="8decc-121">In Android Studio, start a new Android Studio project.</span></span>
   
       ![Android Studio - new project](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-new-project.png)
2. <span data-ttu-id="8decc-122">選擇 [電話和平板電腦] 板型規格和您要支援的 [Minimum SDK]。</span><span class="sxs-lookup"><span data-stu-id="8decc-122">Choose the **Phone and Tablet** form factor and the **Minimum SDK** that you want to support.</span></span> <span data-ttu-id="8decc-123">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="8decc-123">Then click **Next**.</span></span>
   
       ![Android Studio - project creation workflow](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-choose-form-factor.png)
3. <span data-ttu-id="8decc-124">為主要活動選擇 [空白活動]，並按 [下一步]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="8decc-124">Choose **Empty Activity** for the main activity, click **Next**, and then click **Finish**.</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="8decc-125">建立支援 Firebase 雲端通訊的專案</span><span class="sxs-lookup"><span data-stu-id="8decc-125">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a><span data-ttu-id="8decc-126">設定新的通知中樞</span><span class="sxs-lookup"><span data-stu-id="8decc-126">Configure a new notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="8decc-127">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="8decc-127">&emsp;&emsp;6.</span></span> <span data-ttu-id="8decc-128">在通知中樞的 [設定] 刀鋒視窗中，選取 [通知服務]，然後選取 [Google (GCM)]。</span><span class="sxs-lookup"><span data-stu-id="8decc-128">In the **Settings** blade of your notification hub, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="8decc-129">輸入您先前從 [Firebase 主控台](https://firebase.google.com/console/)複製的 FCM 伺服器金鑰，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="8decc-129">Enter the FCM server key you copied earlier from the [Firebase console](https://firebase.google.com/console/) and click **Save**.</span></span>

&emsp;&emsp;![Azure 通知中樞 - Google (GCM)](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-gcm-api.png)

<span data-ttu-id="8decc-131">現在已將您的通知中樞設定成使用 Firebase Cloud Messagin，而且您已擁有可用來註冊應用程式以接收和傳送推播通知的連接字串。</span><span class="sxs-lookup"><span data-stu-id="8decc-131">Your notification hub is now configured to work with Firebase Cloud Messagin, and you have the connection strings to both register your app to receive and send push notifications.</span></span>

## <span data-ttu-id="8decc-132"><a id="connecting-app"></a>將您的應用程式連接到通知中樞</span><span class="sxs-lookup"><span data-stu-id="8decc-132"><a id="connecting-app"></a>Connect your app to the notification hub</span></span>
### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="8decc-133">新增 Google Play 服務至專案</span><span class="sxs-lookup"><span data-stu-id="8decc-133">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a><span data-ttu-id="8decc-134">新增 Azure 通知中樞程式庫</span><span class="sxs-lookup"><span data-stu-id="8decc-134">Adding Azure Notification Hubs libraries</span></span>
1. <span data-ttu-id="8decc-135">在 **app** 的 `Build.Gradle` 檔案中，於 **dependencies** 區段中新增下列數行。</span><span class="sxs-lookup"><span data-stu-id="8decc-135">In the `Build.Gradle` file for the **app**, add the following lines in the **dependencies** section.</span></span>
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. <span data-ttu-id="8decc-136">加入下列儲存機制到 **dependencies** 一節之後。</span><span class="sxs-lookup"><span data-stu-id="8decc-136">Add the following repository after the **dependencies** section.</span></span>
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a><span data-ttu-id="8decc-137">更新 AndroidManifest.xml。</span><span class="sxs-lookup"><span data-stu-id="8decc-137">Updating the AndroidManifest.xml.</span></span>
1. <span data-ttu-id="8decc-138">若要支援 FCM，我們必須在程式碼中實作執行個體識別碼接聽程式服務，以便使用 [Google 的 FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId) 來[取得註冊權杖](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register)。</span><span class="sxs-lookup"><span data-stu-id="8decc-138">To support FCM, we must implement a Instance ID listener service in our code which is used to [obtain registration tokens](https://firebase.google.com/docs/cloud-messaging/android/client#sample-register) using [Google's FirebaseInstanceId API](https://firebase.google.com/docs/reference/android/com/google/firebase/iid/FirebaseInstanceId).</span></span> <span data-ttu-id="8decc-139">在本教學課程中，我們將此類別命名為 `MyInstanceIDService`。</span><span class="sxs-lookup"><span data-stu-id="8decc-139">In this tutorial we will name the class `MyInstanceIDService`.</span></span> 
   
    <span data-ttu-id="8decc-140">將下列服務定義新增至 AndroidManifest.xml 檔案的 `<application>` 標籤內。</span><span class="sxs-lookup"><span data-stu-id="8decc-140">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service android:name=".MyInstanceIDService">
            <intent-filter>
                <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
            </intent-filter>
        </service>
2. <span data-ttu-id="8decc-141">一旦從 FirebaseInstanceId API 收到 FCM 註冊權杖，我們會將它用來 [向 Azure 通知中樞註冊](notification-hubs-push-notification-registration-management.md)。</span><span class="sxs-lookup"><span data-stu-id="8decc-141">Once we have received our FCM registration token from the FirebaseInstanceId API, we will use it to [register with the Azure Notification Hub](notification-hubs-push-notification-registration-management.md).</span></span> <span data-ttu-id="8decc-142">我們將使用名為 `RegistrationIntentService` 的 `IntentService` 在背景支援此註冊。</span><span class="sxs-lookup"><span data-stu-id="8decc-142">We will support this registration in the background using an `IntentService` named `RegistrationIntentService`.</span></span> <span data-ttu-id="8decc-143">此服務也會負責重新整理我們的 GCM 註冊權杖。</span><span class="sxs-lookup"><span data-stu-id="8decc-143">This service will also be responsible for refreshing our FCM registration token.</span></span>
   
    <span data-ttu-id="8decc-144">將下列服務定義新增至 AndroidManifest.xml 檔案的 `<application>` 標籤內。</span><span class="sxs-lookup"><span data-stu-id="8decc-144">Add the following service definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> 
   
        <service
            android:name=".RegistrationIntentService"
            android:exported="false">
        </service>
3. <span data-ttu-id="8decc-145">我們也會定義要接收通知的接收者。</span><span class="sxs-lookup"><span data-stu-id="8decc-145">We will also define a receiver to receive notifications.</span></span> <span data-ttu-id="8decc-146">將下列接收者定義新增至 AndroidManifest.xml 檔案的 `<application>` 標籤內。</span><span class="sxs-lookup"><span data-stu-id="8decc-146">Add the following receiver definition to the AndroidManifest.xml file, inside the `<application>` tag.</span></span> <span data-ttu-id="8decc-147">以 `AndroidManifest.xml` 檔案頂端顯示的實際封裝名稱取代 `<your package>` 預留位置。</span><span class="sxs-lookup"><span data-stu-id="8decc-147">Replace the `<your package>` placeholder with the your actual package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="8decc-148">在 `</application>` 標籤下面新增下列必要的 FCM 相關權限。</span><span class="sxs-lookup"><span data-stu-id="8decc-148">Add the following necessary FCM related permissions below the  `</application>` tag.</span></span> <span data-ttu-id="8decc-149">請務必以 `AndroidManifest.xml` 檔案頂端顯示的封裝名稱取代 `<your package>`。</span><span class="sxs-lookup"><span data-stu-id="8decc-149">Make sure to replace `<your package>` with the package name shown at the top of the `AndroidManifest.xml` file.</span></span>
   
    <span data-ttu-id="8decc-150">如需這些權限的詳細資訊，請參閱[設定適用於 Android 的 GCM 用戶端應用程式](https://developers.google.com/cloud-messaging/android/client#manifest)和[將適用於 Android 的 GCM 用戶端應用程式移轉至 Firebase 雲端通訊](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm)。</span><span class="sxs-lookup"><span data-stu-id="8decc-150">For more information on these permissions, see [Setup a GCM Client app for Android](https://developers.google.com/cloud-messaging/android/client#manifest) and [Migrate a GCM Client App for Android to Firebase Cloud Messaging](https://developers.google.com/cloud-messaging/android/android-migrate-fcm#remove_the_permissions_required_by_gcm).</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />

### <a name="adding-code"></a><span data-ttu-id="8decc-151">加入程式碼</span><span class="sxs-lookup"><span data-stu-id="8decc-151">Adding code</span></span>
1. <span data-ttu-id="8decc-152">在 [專案檢視] 中，展開 [app] > [src] > [main] > [java]。</span><span class="sxs-lookup"><span data-stu-id="8decc-152">In the Project View, expand **app** > **src** > **main** > **java**.</span></span> <span data-ttu-id="8decc-153">以滑鼠右鍵按一下 **java** 底下您的套件資料夾，並按一下 [新增]，然後按一下 [Java 類別]。</span><span class="sxs-lookup"><span data-stu-id="8decc-153">Right-click your package folder under **java**, click **New**, and then click **Java Class**.</span></span> <span data-ttu-id="8decc-154">新增名為 `NotificationSettings` 的新類別。</span><span class="sxs-lookup"><span data-stu-id="8decc-154">Add a new class named `NotificationSettings`.</span></span> 
   
    ![Android Studio - 新增 Java 類別](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hub-android-new-class.png)
   
    <span data-ttu-id="8decc-156">請務必在 `NotificationSettings` 類別的下列程式碼中更新這三個預留位置：</span><span class="sxs-lookup"><span data-stu-id="8decc-156">Make sure to update the these three placeholders in the following code for the `NotificationSettings` class:</span></span>
   
   * <span data-ttu-id="8decc-157">**SenderId**︰您稍早在 [Firebase 主控台](https://firebase.google.com/console/)專案設定的 [雲端通訊] 索引標籤中取得的寄件者識別碼。</span><span class="sxs-lookup"><span data-stu-id="8decc-157">**SenderId**: The Sender Id you obtained earlier in the **Cloud Messaging** tab of your project settings in the [Firebase console](https://firebase.google.com/console/).</span></span>
   * <span data-ttu-id="8decc-158">**HubListenConnectionString**：中樞的 **DefaultListenAccessSignature** 連接字串。</span><span class="sxs-lookup"><span data-stu-id="8decc-158">**HubListenConnectionString**: The **DefaultListenAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="8decc-159">在 [Azure 入口網站]中，按一下中樞 [設定] 刀鋒視窗上的 [存取原則]，即可複製該連接字串。</span><span class="sxs-lookup"><span data-stu-id="8decc-159">You can copy that connection string by clicking **Access Policies** on the **Settings** blade of your hub on the [Azure Portal].</span></span>
   * <span data-ttu-id="8decc-160">**HubName**︰使用出現在 [Azure 入口網站]中樞刀鋒視窗中的通知中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="8decc-160">**HubName**: Use the name of your notification hub that appears in the hub blade in the [Azure Portal].</span></span>
     
     <span data-ttu-id="8decc-161">`NotificationSettings` 程式碼︰</span><span class="sxs-lookup"><span data-stu-id="8decc-161">`NotificationSettings` code:</span></span>
     
       <span data-ttu-id="8decc-162">public class NotificationSettings {</span><span class="sxs-lookup"><span data-stu-id="8decc-162">public class NotificationSettings {</span></span>
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Enter your DefaultListenSharedAccessSignature connection string>";
       <span data-ttu-id="8decc-163">}</span><span class="sxs-lookup"><span data-stu-id="8decc-163">}</span></span>
2. <span data-ttu-id="8decc-164">使用上述步驟，加入另一個名為 `MyInstanceIDService`的新類別。</span><span class="sxs-lookup"><span data-stu-id="8decc-164">Using the steps above, add another new class named `MyInstanceIDService`.</span></span> <span data-ttu-id="8decc-165">這會是我們的執行個體識別碼接聽程式服務實作。</span><span class="sxs-lookup"><span data-stu-id="8decc-165">This will be our Instance ID listener service implementation.</span></span>
   
    <span data-ttu-id="8decc-166">此類別的程式碼會呼叫 `IntentService` 以在背景 [重新整理 FCM 權杖](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) 。</span><span class="sxs-lookup"><span data-stu-id="8decc-166">The code for this class will call our `IntentService` to [refresh the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) in the background.</span></span>
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.firebase.iid.FirebaseInstanceIdService;

        public class MyInstanceIDService extends FirebaseInstanceIdService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.d(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. <span data-ttu-id="8decc-167">將另一個新類別新增至名為 `RegistrationIntentService`的專案。</span><span class="sxs-lookup"><span data-stu-id="8decc-167">Add another new class to your project named, `RegistrationIntentService`.</span></span> <span data-ttu-id="8decc-168">這會是我們的 `IntentService` 實作，以便處理[重新整理 FCM 權杖](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens)和[向通知中樞註冊](notification-hubs-push-notification-registration-management.md)。</span><span class="sxs-lookup"><span data-stu-id="8decc-168">This will be the implementation for our `IntentService` that will handle [refreshing the FCM token](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) and [registering with the notification hub](notification-hubs-push-notification-registration-management.md).</span></span>
   
    <span data-ttu-id="8decc-169">針對此類別使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="8decc-169">Use the following code for this class.</span></span>
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;        
        import com.google.firebase.iid.FirebaseInstanceId;
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
                String storedToken = null;
   
                try {
                    String FCM_token = FirebaseInstanceId.getInstance().getToken();
                    Log.d(TAG, "FCM Registration Token: " + FCM_token);
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if (((regID=sharedPreferences.getString("registrationID", null)) == null)){
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "Attempting a new registration with NH using FCM token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    // Check if the token may have been compromised and needs refreshing.
                    else if ((storedToken=sharedPreferences.getString("FCMtoken", "")) != FCM_token) {
   
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.d(TAG, "NH Registration refreshing with token : " + FCM_token);
                        regID = hub.register(FCM_token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1,tag2").getRegistrationId();
   
                        resultString = "New NH Registration Successfully - RegId : " + regID;
                        Log.d(TAG, resultString);
   
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                        sharedPreferences.edit().putString("FCMtoken", FCM_token ).apply();
                    }
   
                    else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete registration", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. <span data-ttu-id="8decc-170">在 `MainActivity` 類別中，在類別宣告上面新增下列 `import` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8decc-170">In your `MainActivity` class, add the following `import` statements above the class declaration.</span></span>
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.content.Intent;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. <span data-ttu-id="8decc-171">在類別頂端新增下列 Private 成員。</span><span class="sxs-lookup"><span data-stu-id="8decc-171">Add the following private members at the top of the class.</span></span> <span data-ttu-id="8decc-172">我們將使用這些來 [檢查 Google 所建議的 Google Play 服務可用性](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk)。</span><span class="sxs-lookup"><span data-stu-id="8decc-172">We will use these [check the availability of Google Play Services as recommended by Google](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).</span></span>
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private static final String TAG = "MainActivity";
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. <span data-ttu-id="8decc-173">在 `MainActivity` 類別中，將下列方法新增至 Google Play 服務的可用性。</span><span class="sxs-lookup"><span data-stu-id="8decc-173">In your `MainActivity` class, add the following method to the availability of Google Play Services.</span></span> 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
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
5. <span data-ttu-id="8decc-174">在 `MainActivity` 類別中加入下列程式碼，以在呼叫 `IntentService` 之前檢查 Google Play 服務，進而取得 FCM 註冊權杖並向通知中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="8decc-174">In your `MainActivity` class, add the following code that will check for Google Play Services before calling your `IntentService` to get your FCM registration token and register with your notification hub.</span></span>
   
        public void registerWithNotificationHubs()
        {
            if (checkPlayServices()) {
                // Start IntentService to register this application with FCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. <span data-ttu-id="8decc-175">在 `MainActivity` 類別的 `OnCreate` 方法中，加入下列程式碼以便在活動建立時開始註冊程序。</span><span class="sxs-lookup"><span data-stu-id="8decc-175">In the `OnCreate` method of the `MainActivity` class, add the following code to start the registration process when activity is created.</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. <span data-ttu-id="8decc-176">將上述其他方法新增至 `MainActivity` ，以驗證應用程式狀態及報告您的應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="8decc-176">Add these additional methods to the `MainActivity` to verify app state and report status in your app.</span></span>
   
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
8. <span data-ttu-id="8decc-177">`ToastNotify` 方法會使用 *"Hello World"* `TextView` 控制項持續在應用程式中報告狀態和通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-177">The `ToastNotify` method uses the *"Hello World"* `TextView` control to report status and notifications persistently in the app.</span></span> <span data-ttu-id="8decc-178">在 activity_main.xml 配置中，為該控制項加入下列識別碼。</span><span class="sxs-lookup"><span data-stu-id="8decc-178">In your activity_main.xml layout, add the following id for that control.</span></span>
   
       android:id="@+id/text_hello"
9. <span data-ttu-id="8decc-179">接下來，我們將為在 AndroidManifest.xml 中定義的接收者加入一個子類別。</span><span class="sxs-lookup"><span data-stu-id="8decc-179">Next we will add a subclass for our receiver we defined in the AndroidManifest.xml.</span></span> <span data-ttu-id="8decc-180">將另一個新類別新增至名為 `MyHandler`的專案。</span><span class="sxs-lookup"><span data-stu-id="8decc-180">Add another new class to your project named `MyHandler`.</span></span>
10. <span data-ttu-id="8decc-181">在 `MyHandler.java` 頂端新增下列 import 陳述式：</span><span class="sxs-lookup"><span data-stu-id="8decc-181">Add the following import statements at the top of `MyHandler.java`:</span></span>
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.media.RingtoneManager;
        import android.net.Uri;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. <span data-ttu-id="8decc-182">在 `MyHandler` 類別中新增下列程式碼，使其成為 `com.microsoft.windowsazure.notifications.NotificationsHandler` 的子類別。</span><span class="sxs-lookup"><span data-stu-id="8decc-182">Add the following code for the `MyHandler` class making it a subclass of `com.microsoft.windowsazure.notifications.NotificationsHandler`.</span></span>
    
    <span data-ttu-id="8decc-183">此程式碼會覆寫 `OnReceive` 方法，所以處理常式會報告所收到的通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-183">This code overrides the `OnReceive` method, so the handler will report notifications that are received.</span></span> <span data-ttu-id="8decc-184">處理常式也會使用 `sendNotification()` 方法，將推播通知傳送給 Android 通知管理員。</span><span class="sxs-lookup"><span data-stu-id="8decc-184">The handler also sends the push notification to the Android notification manager by using the `sendNotification()` method.</span></span> <span data-ttu-id="8decc-185">當應用程式不在執行中並收到通知時，應該執行 `sendNotification()` 方法。</span><span class="sxs-lookup"><span data-stu-id="8decc-185">The `sendNotification()` method should be executed when the app is not running and a notification is received.</span></span>
    
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
12. <span data-ttu-id="8decc-186">在 Android Studio 的功能表列上，按一下 [建置] > [重新建置專案]，確保您的程式碼中未沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="8decc-186">In Android Studio on the menu bar, click **Build** > **Rebuild Project** to make sure that no errors are present in your code.</span></span>
13. <span data-ttu-id="8decc-187">在您的裝置上執行應用程式，並確認該應用程式已向通知中心註冊成功。</span><span class="sxs-lookup"><span data-stu-id="8decc-187">Run the app on your device and verify it registers successfully with the notification hub.</span></span> 
    
    > [!NOTE]
    > <span data-ttu-id="8decc-188">註冊可能會在初始啟動時失敗，直到呼叫執行個體 Id 服務的 `onTokenRefresh()` 方法為止。</span><span class="sxs-lookup"><span data-stu-id="8decc-188">Registration may fail on the initial launch until the `onTokenRefresh()` method of instance Id service is called.</span></span> <span data-ttu-id="8decc-189">重新整理應起始向通知中心的成功註冊。</span><span class="sxs-lookup"><span data-stu-id="8decc-189">The refresh should intiate a successful registration with the notification hub.</span></span>
    > 
    > 

## <a name="sending-push-notifications"></a><span data-ttu-id="8decc-190">傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="8decc-190">Sending push notifications</span></span>
<span data-ttu-id="8decc-191">透過 [Azure 入口網站]傳送推播通知，即可在您的應用程式中測試接收推播通知 - 尋找中樞刀鋒視窗中的 [疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="8decc-191">You can test receiving push notifications in your app by sending them via the [Azure Portal] - look for the **Troubleshooting** Section in the hub blade, as shown below.</span></span>

![Azure 通知中樞 - 測試傳送](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a><span data-ttu-id="8decc-193">(選擇性) 從應用程式直接傳送推播通知</span><span class="sxs-lookup"><span data-stu-id="8decc-193">(Optional) Send push notifications directly from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8decc-194">此從用戶端應用程式傳送通知的範例僅供學習之用。</span><span class="sxs-lookup"><span data-stu-id="8decc-194">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="8decc-195">由於這需要 `DefaultFullSharedAccessSignature` 存在用戶端應用程式上，通知中樞可能的風險為使用者可以取得存取傳送未經授權的通知至您的用戶端。</span><span class="sxs-lookup"><span data-stu-id="8decc-195">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="8decc-196">一般來說，您會使用後端伺服器傳送通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-196">Normally, you would send notifications using a backend server.</span></span> <span data-ttu-id="8decc-197">在某些情況下，您可能希望能夠直接從用戶端應用程式傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-197">For some cases, you might want to be able to send push notifications directly from the client application.</span></span> <span data-ttu-id="8decc-198">本節說明如何使用 [Azure 通知中樞 REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx)從用戶端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-198">This section explains how to send notifications from the client using the [Azure Notification Hub REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).</span></span>

1. <span data-ttu-id="8decc-199">在 [Android Studio 專案檢視] 中，展開 [App] > [src] > [main] > [res] > [layout]。</span><span class="sxs-lookup"><span data-stu-id="8decc-199">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **layout**.</span></span> <span data-ttu-id="8decc-200">開啟 `activity_main.xml` 配置檔案，然後按一下 [文字] 索引標籤以更新檔案的文字內容。</span><span class="sxs-lookup"><span data-stu-id="8decc-200">Open the `activity_main.xml` layout file and click the **Text** tab to update the text contents of the file.</span></span> <span data-ttu-id="8decc-201">以下列程式碼進行更新，這會加入新的 `Button` 和 `EditText` 控制項，以便將推播通知訊息傳送至通知中樞。</span><span class="sxs-lookup"><span data-stu-id="8decc-201">Update it with the code below, which adds new `Button` and `EditText` controls for sending push notification messages to the notification hub.</span></span> <span data-ttu-id="8decc-202">在底部將此程式碼加在 `</RelativeLayout>`之前。</span><span class="sxs-lookup"><span data-stu-id="8decc-202">Add this code at the bottom, just before `</RelativeLayout>`.</span></span>
   
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
2. <span data-ttu-id="8decc-203">在 [Android Studio 專案檢視] 中，展開 [App] > [src] > [main] > [res] > [values]。</span><span class="sxs-lookup"><span data-stu-id="8decc-203">In Android Studio Project View, expand **App** > **src** > **main** > **res** > **values**.</span></span> <span data-ttu-id="8decc-204">開啟 `strings.xml` 檔案並加入新的 `Button` 和 `EditText` 控制項所參考的字串值。</span><span class="sxs-lookup"><span data-stu-id="8decc-204">Open the `strings.xml` file and add the string values that are referenced by the new `Button` and `EditText` controls.</span></span> <span data-ttu-id="8decc-205">在檔案底部將這些值加在 `</resources>`之前。</span><span class="sxs-lookup"><span data-stu-id="8decc-205">Add these at the bottom of the file, just before `</resources>`.</span></span>
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. <span data-ttu-id="8decc-206">在 `NotificationSetting.java` 檔案中，將下列設定新增至 `NotificationSettings` 類別。</span><span class="sxs-lookup"><span data-stu-id="8decc-206">In your `NotificationSetting.java` file, add the following setting to the `NotificationSettings` class.</span></span>
   
    <span data-ttu-id="8decc-207">使用中樞的 **DefaultFullSharedAccessSignature** 連接字串更新 `HubFullAccess`。</span><span class="sxs-lookup"><span data-stu-id="8decc-207">Update `HubFullAccess` with the **DefaultFullSharedAccessSignature** connection string for your hub.</span></span> <span data-ttu-id="8decc-208">按一下通知中樞 [設定] 刀鋒視窗上的 [存取原則]，即可從 [Azure 入口網站]複製此連接字串。</span><span class="sxs-lookup"><span data-stu-id="8decc-208">This connection string can be copied from the [Azure Portal] by clicking **Access Policies** on the **Settings** blade for your notification hub.</span></span>
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccessSignature Connection string>";
4. <span data-ttu-id="8decc-209">在 `MainActivity.java` 檔案中，將下列 `import` 陳述式加在 `MainActivity` 類別之上。</span><span class="sxs-lookup"><span data-stu-id="8decc-209">In your `MainActivity.java` file, add the following `import` statements above the `MainActivity` class.</span></span>
   
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
5. <span data-ttu-id="8decc-210">在 `MainActivity.java` 檔案中，將下列成員加在 `MainActivity` 類別的最上方。</span><span class="sxs-lookup"><span data-stu-id="8decc-210">In your `MainActivity.java` file, add the following members at the top of the `MainActivity` class.</span></span>    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. <span data-ttu-id="8decc-211">您必須建立軟體存取簽章 (SaS) 權杖來驗證 POST 要求，以將訊息傳送至您的通知中樞。</span><span class="sxs-lookup"><span data-stu-id="8decc-211">You must create a Software Access Signature (SaS) token to authenticate a POST request to send messages to your notification hub.</span></span> <span data-ttu-id="8decc-212">剖析連接字串中的金鑰資料，然後建立 [一般概念](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API 參考中所提的 SaS Token，即可完成此作業。</span><span class="sxs-lookup"><span data-stu-id="8decc-212">This is done by parsing the key data from the connection string and then creating the SaS token, as mentioned in the [Common Concepts](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API reference.</span></span> <span data-ttu-id="8decc-213">下列程式碼是範例實作。</span><span class="sxs-lookup"><span data-stu-id="8decc-213">The following code is an example implementation.</span></span>
   
    <span data-ttu-id="8decc-214">在 `MainActivity.java` 中，將下列方法加入至 `MainActivity` 類別，以剖析連接字串。</span><span class="sxs-lookup"><span data-stu-id="8decc-214">In `MainActivity.java`, add the following method to the `MainActivity` class to parse your connection string.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
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
7. <span data-ttu-id="8decc-215">在 `MainActivity.java` 中，將下列方法加入至 `MainActivity` 類別，以建立 SaS 驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="8decc-215">In `MainActivity.java`, add the following method to the `MainActivity` class to create a SaS authentication token.</span></span>
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
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
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
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
8. <span data-ttu-id="8decc-216">在 `MainActivity.java` 中，將下列方法新增至 `MainActivity` 類別，以使用內建 REST API 處理 [傳送通知] 按鈕點選，並將推播通知訊息傳送至中樞。</span><span class="sxs-lookup"><span data-stu-id="8decc-216">In `MainActivity.java`, add the following method to the `MainActivity` class to handle the **Send Notification** button click and send the push notification message to the hub by using the built-in REST API.</span></span>
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
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
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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

## <a name="testing-your-app"></a><span data-ttu-id="8decc-217">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="8decc-217">Testing your app</span></span>
#### <a name="push-notifications-in-the-emulator"></a><span data-ttu-id="8decc-218">在模擬器中測試推播通知</span><span class="sxs-lookup"><span data-stu-id="8decc-218">Push notifications in the emulator</span></span>
<span data-ttu-id="8decc-219">如果您要在模擬器中測試推播通知，請確定您的模擬器映像支援您為應用程式選擇的 Google API 層級。</span><span class="sxs-lookup"><span data-stu-id="8decc-219">If you want to test push notifications inside an emulator, make sure that your emulator image supports the Google API level that you chose for your app.</span></span> <span data-ttu-id="8decc-220">如果您的映像不支援原生 Google API，最後會發生 **SERVICE\_NOT\_AVAILABLE** 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8decc-220">If your image doesn't support native Google APIs, you will end up with the **SERVICE\_NOT\_AVAILABLE** exception.</span></span>

<span data-ttu-id="8decc-221">除此之外，請確定已將 Google 帳戶新增至執行中模擬器的 [設定] > [帳戶] 之下。</span><span class="sxs-lookup"><span data-stu-id="8decc-221">In addition to the above, ensure that you have added your Google account to your running emulator under **Settings** > **Accounts**.</span></span> <span data-ttu-id="8decc-222">否則，嘗試向 GCM 註冊可能會導致 **AUTHENTICATION\_FAILED** 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8decc-222">Otherwise, your attempts to register with GCM may result in the **AUTHENTICATION\_FAILED** exception.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="8decc-223">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="8decc-223">Running the application</span></span>
1. <span data-ttu-id="8decc-224">執行 app，並注意已回報註冊成功的註冊識別碼。</span><span class="sxs-lookup"><span data-stu-id="8decc-224">Run the app and notice that the registration ID is reported for a successful registration.</span></span>
   
       ![Testing on Android - Channel registration](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-registered.png)
2. <span data-ttu-id="8decc-225">輸入通知訊息，以傳送給已向中心註冊的所有 Android 裝置。</span><span class="sxs-lookup"><span data-stu-id="8decc-225">Enter a notification message to be sent to all Android devices that have registered with the hub.</span></span>
   
       ![Testing on Android - sending a message](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-set-message.png)
3. <span data-ttu-id="8decc-226">按 [ **傳送通知**]。</span><span class="sxs-lookup"><span data-stu-id="8decc-226">Press **Send Notification**.</span></span> <span data-ttu-id="8decc-227">任何執行應用程式的裝置都會顯示含推播通知訊息的 `AlertDialog` 執行個體。</span><span class="sxs-lookup"><span data-stu-id="8decc-227">Any devices that have the app running will show an `AlertDialog` instance with the push notification message.</span></span> <span data-ttu-id="8decc-228">未執行應用程式但先前已註冊推播通知的裝置，將會收到 Android 通知管理員的通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-228">Devices that don't have the app running but were previously registered for push notifications will receive a notification in the Android Notification Manager.</span></span> <span data-ttu-id="8decc-229">從左上角往下撥動，即可檢視通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-229">Those can be viewed by swiping down from the upper-left corner.</span></span>
   
       ![Testing on Android - notifications](./media/notification-hubs-android-push-notification-google-fcm-get-started/notification-hubs-android-studio-received-message.png)

## <a name="next-steps"></a><span data-ttu-id="8decc-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8decc-230">Next steps</span></span>
<span data-ttu-id="8decc-231">我們建議以 [使用通知中樞將通知推播給使用者] 教學課程做為下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="8decc-231">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="8decc-232">它會示範如何使用標記以特定使用者為目標，從 ASP.NET 後端傳送通知。</span><span class="sxs-lookup"><span data-stu-id="8decc-232">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="8decc-233">如果您想要依興趣群組分隔使用者，請查看 [使用通知中樞傳送即時新聞] 教學課程。</span><span class="sxs-lookup"><span data-stu-id="8decc-233">If you want to segment your users by interest groups, check out the [Use Notification Hubs to send breaking news] tutorial.</span></span>

<span data-ttu-id="8decc-234">若要深入了解通知中樞的一般資訊，請參閱 [通知中樞指引]。</span><span class="sxs-lookup"><span data-stu-id="8decc-234">To learn more general information about Notification Hubs, see our [Notification Hubs Guidance].</span></span>

<!-- Images. -->



<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="8decc-235">[通知中樞指引]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="8decc-235">[Notification Hubs Guidance]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="8decc-236">[使用通知中樞將通知推播給使用者]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span><span class="sxs-lookup"><span data-stu-id="8decc-236">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md</span></span>
<span data-ttu-id="8decc-237">[使用通知中樞傳送即時新聞]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="8decc-237">[Use Notification Hubs to send breaking news]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md</span></span>
<span data-ttu-id="8decc-238">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="8decc-238">[Azure Portal]: https://portal.azure.com</span></span>
