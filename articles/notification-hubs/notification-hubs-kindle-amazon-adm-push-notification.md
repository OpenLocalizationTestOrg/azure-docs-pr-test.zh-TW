---
title: "aaaGet Kindle 應用程式啟動了 Azure 通知中心 |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toosend 推播通知 tooa Kindle 應用程式。"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="5c270-103">開始使用適用於 Kindle 應用程式的通知中樞</span><span class="sxs-lookup"><span data-stu-id="5c270-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5c270-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5c270-104">Overview</span></span>
<span data-ttu-id="5c270-105">本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa Kindle 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c270-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="5c270-106">您將使用 Amazon 裝置傳訊 (ADM)，建立可接收推播通知的空白 Kindle app。</span><span class="sxs-lookup"><span data-stu-id="5c270-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c270-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="5c270-107">Prerequisites</span></span>
<span data-ttu-id="5c270-108">本教學課程必須 hello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="5c270-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="5c270-109">收到 hello hello （我們假設您將使用 Eclipse） 的 Android SDK <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android 的站台</a>。</span><span class="sxs-lookup"><span data-stu-id="5c270-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="5c270-110">中的 hello 步驟<a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">工作開發環境上設定</a>tooset 適用於 Kindle 開發環境。</span><span class="sxs-lookup"><span data-stu-id="5c270-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="5c270-111">加入新的應用程式 toohello 開發人員入口網站</span><span class="sxs-lookup"><span data-stu-id="5c270-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="5c270-112">首先，建立應用程式在 hello [Amazon 開發人員入口網站]。</span><span class="sxs-lookup"><span data-stu-id="5c270-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="5c270-113">複製 hello**應用程式金鑰**。</span><span class="sxs-lookup"><span data-stu-id="5c270-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="5c270-114">在 hello 入口網站按一下 [hello 應用程式的名稱，然後按一下hello**裝置傳訊**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5c270-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="5c270-115">按一下 [建立新的安全性設定檔]，然後建立新的安全性設定檔 (例如 **TestAdm 安全性設定檔**)。</span><span class="sxs-lookup"><span data-stu-id="5c270-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="5c270-116">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5c270-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="5c270-117">按一下**安全性設定檔**tooview hello 安全性您剛建立設定檔。</span><span class="sxs-lookup"><span data-stu-id="5c270-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="5c270-118">複製 hello**用戶端識別碼**和**用戶端密碼**值供日後使用。</span><span class="sxs-lookup"><span data-stu-id="5c270-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="5c270-119">建立 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="5c270-119">Create an API key</span></span>
1. <span data-ttu-id="5c270-120">以系統管理員權限開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="5c270-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="5c270-121">瀏覽 toohello Android SDK 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c270-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="5c270-122">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="5c270-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="5c270-123">Hello **keystore**密碼、 型別**android**。</span><span class="sxs-lookup"><span data-stu-id="5c270-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="5c270-124">複製 hello **MD5**指紋。</span><span class="sxs-lookup"><span data-stu-id="5c270-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="5c270-125">在 hello 開發人員入口網站，在 hello**傳訊**索引標籤上，按一下  **Android/Kindle**並輸入您的應用程式的 hello 套件 hello 名稱 (比方說， **com.sample.notificationhubtest**)和 hello **MD5**值，然後按一下**產生 API 金鑰**。</span><span class="sxs-lookup"><span data-stu-id="5c270-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="5c270-126">新增認證 toohello 中樞</span><span class="sxs-lookup"><span data-stu-id="5c270-126">Add credentials toohello hub</span></span>
<span data-ttu-id="5c270-127">在 [hello 入口網站中，新增 hello 用戶端密碼和用戶端識別碼 toohello**設定**通知中樞] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5c270-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="5c270-128">設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="5c270-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="5c270-129">建立應用程式時，至少應使用 API 層級 17。</span><span class="sxs-lookup"><span data-stu-id="5c270-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="5c270-130">加入 hello ADM 文件庫 tooyour Eclipse 專案：</span><span class="sxs-lookup"><span data-stu-id="5c270-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="5c270-131">tooobtain hello ADM 程式庫[下載 hello SDK]。</span><span class="sxs-lookup"><span data-stu-id="5c270-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="5c270-132">Hello SDK zip 檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="5c270-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="5c270-133">在 Eclipse 中，以滑鼠右鍵按一下您的專案，然後按一下屬性 。</span><span class="sxs-lookup"><span data-stu-id="5c270-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="5c270-134">選取**Java 組建路徑**hello 左、，然後選取 hello 上 * * 程式庫 * * 在 hello 最上方的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5c270-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="5c270-135">按一下**新增外部 Jar**，和選取 hello 檔案`\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar`從 hello 目錄，您可以在其中解壓縮 hello Amazon SDK。</span><span class="sxs-lookup"><span data-stu-id="5c270-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="5c270-136">下載 hello 通知中樞 Android SDK （連結）。</span><span class="sxs-lookup"><span data-stu-id="5c270-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="5c270-137">解壓縮 hello 封裝，然後將拖曳 hello 檔案`notification-hubs-sdk.jar`到 hello`libs`在 Eclipse 中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5c270-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="5c270-138">編輯您的應用程式資訊清單 toosupport ADM:</span><span class="sxs-lookup"><span data-stu-id="5c270-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="5c270-139">新增 hello 根資訊清單項目中的 hello Amazon 命名空間：</span><span class="sxs-lookup"><span data-stu-id="5c270-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="5c270-140">將權限新增為 hello hello 資訊清單項目下的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="5c270-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="5c270-141">替代**[您的封裝名稱]**與 hello 封裝，您使用 toocreate 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c270-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="5c270-142">插入 hello hello hello 應用程式項目的第一個子系為下列項目。</span><span class="sxs-lookup"><span data-stu-id="5c270-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="5c270-143">請記住 toosubstitute **[您的服務名稱]** hello 名稱，為您建立 hello 下一節 （包括 hello 封裝），並取代您 ADM 訊息處理常式**[您的封裝名稱]**以 hello您用來建立您的應用程式封裝名稱。</span><span class="sxs-lookup"><span data-stu-id="5c270-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="5c270-144">建立您的 ADM 訊息處理常式</span><span class="sxs-lookup"><span data-stu-id="5c270-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="5c270-145">建立新的類別繼承自`com.amazon.device.messaging.ADMMessageHandlerBase`並將其命名`MyADMMessageHandler`hello 遵循圖所示：</span><span class="sxs-lookup"><span data-stu-id="5c270-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="5c270-146">新增下列 hello`import`陳述式：</span><span class="sxs-lookup"><span data-stu-id="5c270-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="5c270-147">新增下列程式碼，您所建立的 hello 類別中的 hello。</span><span class="sxs-lookup"><span data-stu-id="5c270-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="5c270-148">請記住 toosubstitute hello 中樞名稱和連接字串 （待命）：</span><span class="sxs-lookup"><span data-stu-id="5c270-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. <span data-ttu-id="5c270-149">新增下列程式碼 toohello hello`OnMessage()`方法：</span><span class="sxs-lookup"><span data-stu-id="5c270-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="5c270-150">新增下列程式碼 toohello hello`OnRegistered`方法：</span><span class="sxs-lookup"><span data-stu-id="5c270-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="5c270-151">新增下列程式碼 toohello hello`OnUnregistered`方法：</span><span class="sxs-lookup"><span data-stu-id="5c270-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="5c270-152">在 hello`MainActivity`方法，加入下列 import 陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="5c270-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="5c270-153">新增下列程式碼結尾 hello hello hello`OnCreate`方法：</span><span class="sxs-lookup"><span data-stu-id="5c270-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="5c270-154">加入您的 API 金鑰 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="5c270-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="5c270-155">在 Eclipse 中，建立新的檔案命名為**api_key.txt** hello 目錄資產，您的專案中。</span><span class="sxs-lookup"><span data-stu-id="5c270-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="5c270-156">開啟 hello 檔案，並複製 hello API 金鑰，您在 hello Amazon 開發人員入口網站中產生。</span><span class="sxs-lookup"><span data-stu-id="5c270-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="5c270-157">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="5c270-157">Run hello app</span></span>
1. <span data-ttu-id="5c270-158">啟動 hello 模擬器。</span><span class="sxs-lookup"><span data-stu-id="5c270-158">Start hello emulator.</span></span>
2. <span data-ttu-id="5c270-159">從 hello 頂端向撥動 hello 模擬器中，按一下 **設定**，然後按一下**我的帳戶**並使用有效的 Amazon 帳戶註冊。</span><span class="sxs-lookup"><span data-stu-id="5c270-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="5c270-160">在 Eclipse 中，執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5c270-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="5c270-161">如果發生問題，請檢查 hello 時間 hello 模擬器 （或裝置）。</span><span class="sxs-lookup"><span data-stu-id="5c270-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="5c270-162">hello 時間值必須是正確的。</span><span class="sxs-lookup"><span data-stu-id="5c270-162">hello time value must be accurate.</span></span> <span data-ttu-id="5c270-163">toochange hello hello Kindle 模擬器時，您可以執行下列命令，從您的 Android SDK 平台工具目錄 hello:</span><span class="sxs-lookup"><span data-stu-id="5c270-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="5c270-164">傳送訊息</span><span class="sxs-lookup"><span data-stu-id="5c270-164">Send a message</span></span>
<span data-ttu-id="5c270-165">toosend 使用.NET 訊息：</span><span class="sxs-lookup"><span data-stu-id="5c270-165">toosend a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[Amazon 開發人員入口網站]: https://developer.amazon.com/home.html
[下載 hello SDK]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
