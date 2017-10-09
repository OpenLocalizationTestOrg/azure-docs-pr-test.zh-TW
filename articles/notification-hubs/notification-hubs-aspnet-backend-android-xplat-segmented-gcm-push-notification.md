---
title: "aaaNotification 中樞中斷新聞教學課程-Android"
description: "深入了解如何 toouse Azure Service Bus 通知中樞 toosend 重大消息通知 tooAndroid 裝置。"
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 3c23cb80-9d35-4dde-b26d-a7bfd4cb8f81
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e6eb41bec95c67d7dc059f560194966d04400494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="cda6b-103">使用通知中樞 toosend 最新消息</span><span class="sxs-lookup"><span data-stu-id="cda6b-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="cda6b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="cda6b-104">Overview</span></span>
<span data-ttu-id="cda6b-105">本主題說明如何 toouse Azure 通知中樞 toobroadcast 重大消息通知 tooan Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cda6b-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan Android app.</span></span> <span data-ttu-id="cda6b-106">完成時，您將會是能 tooregister 中斷您感興趣的新聞分類，並且接收只有那些類別目錄的推播通知。</span><span class="sxs-lookup"><span data-stu-id="cda6b-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="cda6b-107">這個案例是許多應用程式的常見模式，通知其中有傳送 toobe toogroups 的先前尚未宣告欄位，例如 RSS 讀取器、 應用程式等的音樂迷感興趣的使用者。</span><span class="sxs-lookup"><span data-stu-id="cda6b-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="cda6b-108">啟用廣播的案例包括下列一個或多個*標記*時建立 hello 通知中樞的註冊。</span><span class="sxs-lookup"><span data-stu-id="cda6b-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="cda6b-109">當通知傳送 tooa 標記時，所有已註冊的裝置 hello 標記會收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="cda6b-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="cda6b-110">標記是只是字串，因為它們不需要預先佈建 toobe。</span><span class="sxs-lookup"><span data-stu-id="cda6b-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="cda6b-111">如需標記的詳細資訊，請參閱太[通知中樞路由和標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="cda6b-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cda6b-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="cda6b-112">Prerequisites</span></span>
<span data-ttu-id="cda6b-113">本主題是根據您在建立 hello 應用程式[開始使用通知中樞][get-started]。</span><span class="sxs-lookup"><span data-stu-id="cda6b-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="cda6b-114">開始本教學課程之前，您必須已完成[開始使用通知中樞][get-started]。</span><span class="sxs-lookup"><span data-stu-id="cda6b-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="cda6b-115">加入類別目錄選取 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="cda6b-115">Add category selection toohello app</span></span>
<span data-ttu-id="cda6b-116">hello 第一個步驟為 tooadd hello UI 項目 tooyour 現有主要活動可讓 hello 使用者 tooselect 類別 tooregister。</span><span class="sxs-lookup"><span data-stu-id="cda6b-116">hello first step is tooadd hello UI elements tooyour existing main activity that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="cda6b-117">使用者選取的 hello 類別會儲存在 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="cda6b-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="cda6b-118">Hello 應用程式啟動時，裝置註冊會建立您的通知中樞與 hello 選取類別目錄中，為標記。</span><span class="sxs-lookup"><span data-stu-id="cda6b-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="cda6b-119">開啟您 res/layout/activity_main.xml 檔案，並取代 hello hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="cda6b-119">Open your res/layout/activity_main.xml file, and substitute hello content with hello following:</span></span>
   
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:paddingBottom="@dimen/activity_vertical_margin"
            android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            tools:context="com.example.breakingnews.MainActivity"
            android:orientation="vertical">
   
                <CheckBox
                    android:id="@+id/worldBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_world" />
                <CheckBox
                    android:id="@+id/politicsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_politics" />
                <CheckBox
                    android:id="@+id/businessBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_business" />
                <CheckBox
                    android:id="@+id/technologyBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_technology" />
                <CheckBox
                    android:id="@+id/scienceBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_science" />
                <CheckBox
                    android:id="@+id/sportsBox"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="@string/label_sports" />
                <Button
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:onClick="subscribe"
                    android:text="@string/button_subscribe" />
        </LinearLayout>
2. <span data-ttu-id="cda6b-120">開啟 res/values/strings.xml 檔案並加入下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="cda6b-120">Open your res/values/strings.xml file and add hello following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="cda6b-121">您的 main_activity.xml 圖形版面配置此時應如下所示：</span><span class="sxs-lookup"><span data-stu-id="cda6b-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="cda6b-122">現在建立類別**通知**相同封裝中 hello 做為您**MainActivity**類別。</span><span class="sxs-lookup"><span data-stu-id="cda6b-122">Now create a class **Notifications** in hello same package as your **MainActivity** class.</span></span>
   
        import java.util.HashSet;
        import java.util.Set;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.os.AsyncTask;
        import android.util.Log;
        import android.widget.Toast;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class Notifications {
            private static final String PREFS_NAME = "BreakingNewsCategories";
            private GoogleCloudMessaging gcm;
            private NotificationHub hub;
            private Context context;
            private String senderId;
   
            public Notifications(Context context, String senderId, String hubName, 
                                    String listenConnectionString) {
                this.context = context;
                this.senderId = senderId;
   
                gcm = GoogleCloudMessaging.getInstance(context);
                hub = new NotificationHub(hubName, listenConnectionString, context);
            }
   
            public void storeCategoriesAndSubscribe(Set<String> categories)
            {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                settings.edit().putStringSet("categories", categories).commit();
                subscribeToCategories(categories);
            }
   
            public Set<String> retrieveCategories() {
                SharedPreferences settings = context.getSharedPreferences(PREFS_NAME, 0);
                return settings.getStringSet("categories", new HashSet<String>());
            }
   
            public void subscribeToCategories(final Set<String> categories) {
                new AsyncTask<Object, Object, Object>() {
                    @Override
                    protected Object doInBackground(Object... params) {
                        try {
                            String regid = gcm.register(senderId);
   
                            String templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
                            hub.registerTemplate(regid,"simpleGCMTemplate", templateBodyGCM, 
                                categories.toArray(new String[categories.size()]));
                        } catch (Exception e) {
                            Log.e("MainActivity", "Failed tooregister - " + e.getMessage());
                            return e;
                        }
                        return null;
                    }
   
                    protected void onPostExecute(Object result) {
                        String message = "Subscribed for categories: "
                                + categories.toString();
                        Toast.makeText(context, message,
                                Toast.LENGTH_LONG).show();
                    }
                }.execute(null, null, null);
            }
   
        }
   
    <span data-ttu-id="cda6b-123">這個類別使用新聞此裝置有 tooreceive hello 本機儲存體 toostore hello 的類別。</span><span class="sxs-lookup"><span data-stu-id="cda6b-123">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="cda6b-124">它也包含這些類別的方法 tooregister。</span><span class="sxs-lookup"><span data-stu-id="cda6b-124">It also contains methods tooregister for these categories.</span></span>
4. <span data-ttu-id="cda6b-125">在您的 **MainActivity** 類別中，移除您 **NotificationHub** 和 **GoogleCloudMessaging** 的私人欄位，並新增 [通知] 的欄位：</span><span class="sxs-lookup"><span data-stu-id="cda6b-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="cda6b-126">然後，在 hello **onCreate**方法，移除 hello 初始化 hello**中樞**欄位和 hello **registerWithNotificationHubs**方法。</span><span class="sxs-lookup"><span data-stu-id="cda6b-126">Then, in hello **onCreate** method, remove hello initialization of hello **hub** field and hello **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="cda6b-127">然後加入下列行初始化執行個體的 hello hello**通知**類別。</span><span class="sxs-lookup"><span data-stu-id="cda6b-127">Then add hello following lines which initialize an instance of hello **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="cda6b-128">`HubName`和`HubListenConnectionString`應該已經設定以 hello`<hub name>`和`<connection string with listen access>`預留位置取代通知中樞名稱和 hello 的連接字串*DefaultListenSharedAccessSignature*取得稍早。</span><span class="sxs-lookup"><span data-stu-id="cda6b-128">`HubName` and `HubListenConnectionString` should already be set with hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="cda6b-129">發佈的用戶端應用程式的認證不是一般安全的因為您只應該與用戶端應用程式來散發 hello 接聽 」 存取權的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="cda6b-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="cda6b-130">接聽存取啟用通知，但現有的註冊您的應用程式 tooregister 無法修改，而且無法傳送通知。</span><span class="sxs-lookup"><span data-stu-id="cda6b-130">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="cda6b-131">hello 完整的存取金鑰會用於傳送通知和變更現有註冊的受保護的後端服務。</span><span class="sxs-lookup"><span data-stu-id="cda6b-131">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="cda6b-132">然後，加入下列 hello 匯入和`subscribe`方法 toohandle hello 訂閱按鈕 click 事件：</span><span class="sxs-lookup"><span data-stu-id="cda6b-132">Then, add hello following imports and `subscribe` method toohandle hello subscribe button click event:</span></span>
   
        import android.widget.CheckBox;
        import java.util.HashSet;
        import java.util.Set;
   
        public void subscribe(View sender) {
            final Set<String> categories = new HashSet<String>();
   
            CheckBox world = (CheckBox) findViewById(R.id.worldBox);
            if (world.isChecked())
                categories.add("world");
            CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
            if (politics.isChecked())
                categories.add("politics");
            CheckBox business = (CheckBox) findViewById(R.id.businessBox);
            if (business.isChecked())
                categories.add("business");
            CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
            if (technology.isChecked())
                categories.add("technology");
            CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
            if (science.isChecked())
                categories.add("science");
            CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
            if (sports.isChecked())
                categories.add("sports");
   
            notifications.storeCategoriesAndSubscribe(categories);
        }
   
    <span data-ttu-id="cda6b-133">這個方法會建立一份類別目錄，並使用 hello**通知**類別 toostore hello 本機儲存體中的 hello 清單，並使用您的通知中樞註冊 hello 相對應的標記。</span><span class="sxs-lookup"><span data-stu-id="cda6b-133">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="cda6b-134">類別目錄會變更時，重新建立 hello 註冊 hello 新類別。</span><span class="sxs-lookup"><span data-stu-id="cda6b-134">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="cda6b-135">您的應用程式目前處於無法 toostore 一組類別目錄 hello 裝置上的本機儲存體，並向 hello 通知中樞，每當 hello 使用者變更 hello 選取的類別。</span><span class="sxs-lookup"><span data-stu-id="cda6b-135">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="cda6b-136">註冊通知</span><span class="sxs-lookup"><span data-stu-id="cda6b-136">Register for notifications</span></span>
<span data-ttu-id="cda6b-137">這些步驟註冊在啟動時使用已儲存在本機儲存體的 hello 類別 hello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="cda6b-137">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="cda6b-138">因為 hello registrationId 指派透過 Google Cloud Messaging (GCM) 可以在任何時間變更，您應該註冊通知經常 tooavoid 通知失敗。</span><span class="sxs-lookup"><span data-stu-id="cda6b-138">Because hello registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="cda6b-139">每次該 hello 應用程式啟動時，這個範例會註冊通知。</span><span class="sxs-lookup"><span data-stu-id="cda6b-139">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="cda6b-140">針對經常執行的應用程式，一天一次以上，您可以可能略過註冊 toopreserve 頻寬如果少於一天，已經過 hello 先前的登錄。</span><span class="sxs-lookup"><span data-stu-id="cda6b-140">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="cda6b-141">新增下列程式碼結尾 hello hello hello **onCreate**方法在 hello **MainActivity**類別：</span><span class="sxs-lookup"><span data-stu-id="cda6b-141">Add hello following code at hello end of hello **onCreate** method in hello **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="cda6b-142">這可確保，每次 hello 應用程式啟動時從本機儲存體擷取 hello 類別並要求這些分類的登錄。</span><span class="sxs-lookup"><span data-stu-id="cda6b-142">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="cda6b-143">然後更新 hello`onStart()`方法 hello`MainActivity`類別，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cda6b-143">Then update hello `onStart()` method of hello `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="cda6b-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="cda6b-144">@Override  protected void onStart() {</span></span>
   
        super.onStart();
        isVisible = true;
   
        Set<String> categories = notifications.retrieveCategories();
   
        CheckBox world = (CheckBox) findViewById(R.id.worldBox);
        world.setChecked(categories.contains("world"));
        CheckBox politics = (CheckBox) findViewById(R.id.politicsBox);
        politics.setChecked(categories.contains("politics"));
        CheckBox business = (CheckBox) findViewById(R.id.businessBox);
        business.setChecked(categories.contains("business"));
        CheckBox technology = (CheckBox) findViewById(R.id.technologyBox);
        technology.setChecked(categories.contains("technology"));
        CheckBox science = (CheckBox) findViewById(R.id.scienceBox);
        science.setChecked(categories.contains("science"));
        CheckBox sports = (CheckBox) findViewById(R.id.sportsBox);
        sports.setChecked(categories.contains("sports"));
    <span data-ttu-id="cda6b-145">}</span><span class="sxs-lookup"><span data-stu-id="cda6b-145">}</span></span>
   
    <span data-ttu-id="cda6b-146">這會更新依據先前儲存的類別目錄的 hello 狀態 hello 主要活動。</span><span class="sxs-lookup"><span data-stu-id="cda6b-146">This updates hello main activity based on hello status of previously saved categories.</span></span>

<span data-ttu-id="cda6b-147">hello 應用程式現在已完成，而且可以是儲存一組類別目錄中與 hello 通知中樞的 hello 裝置使用的本機儲存體 tooregister，每當 hello 使用者變更 hello 選取的類別。</span><span class="sxs-lookup"><span data-stu-id="cda6b-147">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="cda6b-148">接下來，我們會定義可以傳送類別通知 toothis 應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="cda6b-148">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="cda6b-149">傳送加註標記的通知</span><span class="sxs-lookup"><span data-stu-id="cda6b-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="cda6b-150">執行 hello 應用程式，並產生通知</span><span class="sxs-lookup"><span data-stu-id="cda6b-150">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="cda6b-151">在 Android Studio 中，建置 hello 應用程式並開始在裝置或模擬器上。</span><span class="sxs-lookup"><span data-stu-id="cda6b-151">In Android Studio, build hello app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="cda6b-152">Hello 應用程式 UI 提供一組切換，請注意，可讓您選擇以 hello 類別 toosubscribe。</span><span class="sxs-lookup"><span data-stu-id="cda6b-152">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="cda6b-153">啟用一或多個類別切換，然後按一下 [訂閱] 。</span><span class="sxs-lookup"><span data-stu-id="cda6b-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="cda6b-154">hello 應用程式將選取的 hello 類別轉換成標記，並從 hello 通知中樞要求新的裝置註冊 hello 選取標記。</span><span class="sxs-lookup"><span data-stu-id="cda6b-154">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="cda6b-155">hello 已註冊的類別會傳回並顯示在快顯通知。</span><span class="sxs-lookup"><span data-stu-id="cda6b-155">hello registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="cda6b-156">藉由執行 hello.NET 主控台應用程式傳送新的通知。</span><span class="sxs-lookup"><span data-stu-id="cda6b-156">Send a new notification by running hello .NET Console app.</span></span>  <span data-ttu-id="cda6b-157">或者，您可以傳送 hello 中使用的通知中樞的 hello 偵錯 索引標籤的標記的範本通知[Azure 傳統入口網站]。</span><span class="sxs-lookup"><span data-stu-id="cda6b-157">Alternatively, you can send tagged template notifications using hello debug tab of your notification hub in hello [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="cda6b-158">通知 hello 選取類別目錄會顯示為快顯通知。</span><span class="sxs-lookup"><span data-stu-id="cda6b-158">Notifications for hello selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cda6b-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cda6b-159">Next steps</span></span>
<span data-ttu-id="cda6b-160">在此教學課程中我們學到如何 toobroadcast 依類別目錄中最新消息。</span><span class="sxs-lookup"><span data-stu-id="cda6b-160">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="cda6b-161">完成下列其中一個 hello 下列反白顯示其他進階的通知中心案例的教學課程，請考慮：</span><span class="sxs-lookup"><span data-stu-id="cda6b-161">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="cda6b-162">[使用通知中樞 toobroadcast 當地語系化重大消息]</span><span class="sxs-lookup"><span data-stu-id="cda6b-162">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="cda6b-163">了解如何傳送 tooenable 新聞應用程式的重大 tooexpand hello 當地語系化通知。</span><span class="sxs-lookup"><span data-stu-id="cda6b-163">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
[使用通知中樞 toobroadcast 當地語系化重大消息]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Azure 傳統入口網站]: https://manage.windowsazure.com
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
