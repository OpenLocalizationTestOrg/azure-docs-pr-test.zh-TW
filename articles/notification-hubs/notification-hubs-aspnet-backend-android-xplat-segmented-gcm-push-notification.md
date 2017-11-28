---
title: "通知中樞即時新聞教學課程 - Android"
description: "了解如何使用 Azure 服務匯流排通知中樞將本地化重大新聞通知傳送至 Android 裝置。"
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
ms.openlocfilehash: 76ec01c874fceedab7d76b2ef58e4b45b5489f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="bafac-103">使用通知中心傳送即時新聞</span><span class="sxs-lookup"><span data-stu-id="bafac-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="bafac-104">概觀</span><span class="sxs-lookup"><span data-stu-id="bafac-104">Overview</span></span>
<span data-ttu-id="bafac-105">本主題將說明如何使用 Azure 通知中心，將即時新聞通知廣播至 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bafac-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an Android app.</span></span> <span data-ttu-id="bafac-106">完成時，您便能夠註冊您所感興趣的即時新聞類別，並僅接收這些類別的推播通知。</span><span class="sxs-lookup"><span data-stu-id="bafac-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="bafac-107">此情況是許多應用程式的共同模式，這些應用程式必須將通知傳送給先前宣告對通知有興趣的使用者群組，例如，RSS 閱讀程式、供樂迷使用的應用程式等等。</span><span class="sxs-lookup"><span data-stu-id="bafac-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="bafac-108">在通知中樞內建立註冊時，您可以透過包含一或多個 *tags* 來啟用廣播案例。</span><span class="sxs-lookup"><span data-stu-id="bafac-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="bafac-109">當標籤收到通知時，所有已註冊此標籤的裝置都會收到通知。</span><span class="sxs-lookup"><span data-stu-id="bafac-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="bafac-110">由於標籤只是簡單的字串而已，您無需預先佈建標籤。</span><span class="sxs-lookup"><span data-stu-id="bafac-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="bafac-111">如需標籤的詳細資訊，請參閱 [通知中樞路由與標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="bafac-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bafac-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="bafac-112">Prerequisites</span></span>
<span data-ttu-id="bafac-113">本主題會以您在[開始使用通知中樞][get-started]中所建立的應用程式為基礎。</span><span class="sxs-lookup"><span data-stu-id="bafac-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="bafac-114">開始本教學課程之前，您必須已完成[開始使用通知中樞][get-started]。</span><span class="sxs-lookup"><span data-stu-id="bafac-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="bafac-115">在應用程式中新增類別選項</span><span class="sxs-lookup"><span data-stu-id="bafac-115">Add category selection to the app</span></span>
<span data-ttu-id="bafac-116">第一個步驟是在您現有的主要活動上新增 UI 元素，以便使用者選取要註冊的類別。</span><span class="sxs-lookup"><span data-stu-id="bafac-116">The first step is to add the UI elements to your existing main activity that enable the user to select categories to register.</span></span> <span data-ttu-id="bafac-117">使用者所選取的類別會儲存在裝置上。</span><span class="sxs-lookup"><span data-stu-id="bafac-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="bafac-118">啟動應用程式時，您的通知中心內會建立以所選取類別作為標籤的裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="bafac-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="bafac-119">開啟您的 res/layout/activity_main.xml 檔案，並替換成下列內容：</span><span class="sxs-lookup"><span data-stu-id="bafac-119">Open your res/layout/activity_main.xml file, and substitute the content with the following:</span></span>
   
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
2. <span data-ttu-id="bafac-120">開啟您的 res/values/strings.xml 檔案，並新增以下幾行：</span><span class="sxs-lookup"><span data-stu-id="bafac-120">Open your res/values/strings.xml file and add the following lines:</span></span>
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    <span data-ttu-id="bafac-121">您的 main_activity.xml 圖形版面配置此時應如下所示：</span><span class="sxs-lookup"><span data-stu-id="bafac-121">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
3. <span data-ttu-id="bafac-122">現在，在與 **MainActivity** 類別相同的套件中建立 **Notifications** 類別。</span><span class="sxs-lookup"><span data-stu-id="bafac-122">Now create a class **Notifications** in the same package as your **MainActivity** class.</span></span>
   
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
                            Log.e("MainActivity", "Failed to register - " + e.getMessage());
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
   
    <span data-ttu-id="bafac-123">本類別會使用本機儲存體來儲存此裝置必須接收的新聞類別。</span><span class="sxs-lookup"><span data-stu-id="bafac-123">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="bafac-124">它也包含註冊這些類別的方法。</span><span class="sxs-lookup"><span data-stu-id="bafac-124">It also contains methods to register for these categories.</span></span>
4. <span data-ttu-id="bafac-125">在您的 **MainActivity** 類別中，移除您 **NotificationHub** 和 **GoogleCloudMessaging** 的私人欄位，並新增 [通知] 的欄位：</span><span class="sxs-lookup"><span data-stu-id="bafac-125">In your **MainActivity** class remove your private fields for **NotificationHub** and **GoogleCloudMessaging**, and add a field for **Notifications**:</span></span>
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. <span data-ttu-id="bafac-126">接著，在 **onCreate** 方法中，將 **hub** 欄位的初始設定和 **registerWithNotificationHubs** 方法移除。</span><span class="sxs-lookup"><span data-stu-id="bafac-126">Then, in the **onCreate** method, remove the initialization of the **hub** field and the **registerWithNotificationHubs** method.</span></span> <span data-ttu-id="bafac-127">接著，新增以下幾行以初始化 [通知]  類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="bafac-127">Then add the following lines which initialize an instance of the **Notifications** class.</span></span> 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    <span data-ttu-id="bafac-128">`HubName` 與 `HubListenConnectionString` 應已經設定有 `<hub name>` 及 `<connection string with listen access>` 預留位置，以及您稍早取得之 *DefaultListenSharedAccessSignature* 的通知中樞名稱及連接字串。</span><span class="sxs-lookup"><span data-stu-id="bafac-128">`HubName` and `HubListenConnectionString` should already be set with the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>

    > [AZURE.NOTE] <span data-ttu-id="bafac-129">因為隨用戶端應用程式散佈的憑證通常不安全，您應只將接聽存取權的金鑰隨用戶端應用程式散佈。</span><span class="sxs-lookup"><span data-stu-id="bafac-129">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="bafac-130">您的應用程式可透過接聽存取權來註冊通知，但無法修改現有的註冊或無法傳送通知。</span><span class="sxs-lookup"><span data-stu-id="bafac-130">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="bafac-131">在安全的後端服務中，會使用完整存取金鑰來傳送通知和變更現有的註冊。</span><span class="sxs-lookup"><span data-stu-id="bafac-131">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>


1. <span data-ttu-id="bafac-132">然後，加入下列匯入及 `subscribe` 方法，以處理 [訂閱] 按鈕的 Click 事件：</span><span class="sxs-lookup"><span data-stu-id="bafac-132">Then, add the following imports and `subscribe` method to handle the subscribe button click event:</span></span>
   
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
   
    <span data-ttu-id="bafac-133">此方法會建立一份類別清單，並使用 **Notifications** 類別在本機儲存體中儲存清單，並在通知中心註冊對應標籤。</span><span class="sxs-lookup"><span data-stu-id="bafac-133">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="bafac-134">變更類別時，系統會使用新類別重新建立註冊。</span><span class="sxs-lookup"><span data-stu-id="bafac-134">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="bafac-135">您的應用程式現在可以在裝置上的本機儲存體中儲存一組類別，並在使用者每次變更類別選項時在通知中心註冊。</span><span class="sxs-lookup"><span data-stu-id="bafac-135">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="bafac-136">註冊通知</span><span class="sxs-lookup"><span data-stu-id="bafac-136">Register for notifications</span></span>
<span data-ttu-id="bafac-137">這些步驟會在啟動時，使用已儲存在本機儲存體中的類別在通知中心註冊。</span><span class="sxs-lookup"><span data-stu-id="bafac-137">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="bafac-138">由於 Google 雲端通訊 (GCM) 所指派的 registrationId 可以隨時變更，您應經常註冊通知以避免通知失敗。</span><span class="sxs-lookup"><span data-stu-id="bafac-138">Because the registrationId assigned by Google Cloud Messaging (GCM) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="bafac-139">此範例會在應用程式每次啟動時註冊通知。</span><span class="sxs-lookup"><span data-stu-id="bafac-139">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="bafac-140">若是經常執行 (一天多次) 的應用程式，如果距離上次註冊的時間不到一天，則您可能可以略過註冊以保留頻寬。</span><span class="sxs-lookup"><span data-stu-id="bafac-140">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="bafac-141">在 **MainActivity** 類別的 **onCreate** 方法結尾處，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="bafac-141">Add the following code at the end of the **onCreate** method in the **MainActivity** class:</span></span>
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    <span data-ttu-id="bafac-142">這會確保應用程式每次啟動時都會從本機儲存體擷取類別，並要求這些類別的註冊。</span><span class="sxs-lookup"><span data-stu-id="bafac-142">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> 
2. <span data-ttu-id="bafac-143">然後如下所示，更新 `MainActivity` 類別的 `onStart()` 方法：</span><span class="sxs-lookup"><span data-stu-id="bafac-143">Then update the `onStart()` method of the `MainActivity` class as follows:</span></span>
   
    <span data-ttu-id="bafac-144">@Override  protected void onStart() {</span><span class="sxs-lookup"><span data-stu-id="bafac-144">@Override  protected void onStart() {</span></span>
   
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
    <span data-ttu-id="bafac-145">}</span><span class="sxs-lookup"><span data-stu-id="bafac-145">}</span></span>
   
    <span data-ttu-id="bafac-146">這會根據原先儲存的類別狀態更新主要活動。</span><span class="sxs-lookup"><span data-stu-id="bafac-146">This updates the main activity based on the status of previously saved categories.</span></span>

<span data-ttu-id="bafac-147">現在已完成此應用程式，且可在裝置本機儲存體中儲存一組類別，以供每次使用者變更類別選項在通知中心註冊時使用。</span><span class="sxs-lookup"><span data-stu-id="bafac-147">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="bafac-148">接著，我們會定義可將類別通知傳送至此應用程式的後端。</span><span class="sxs-lookup"><span data-stu-id="bafac-148">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="bafac-149">傳送加註標記的通知</span><span class="sxs-lookup"><span data-stu-id="bafac-149">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="bafac-150">執行應用程式並產生通知</span><span class="sxs-lookup"><span data-stu-id="bafac-150">Run the app and generate notifications</span></span>
1. <span data-ttu-id="bafac-151">在 Android Studio 中建置應用程式，並在裝置或模擬器上加以啟動。</span><span class="sxs-lookup"><span data-stu-id="bafac-151">In Android Studio, build the app and start it on a device or emulator.</span></span>
   
    <span data-ttu-id="bafac-152">請注意，應用程式 UI 提供一組切換，可讓您選擇要訂閱的類別。</span><span class="sxs-lookup"><span data-stu-id="bafac-152">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="bafac-153">啟用一或多個類別切換，然後按一下 [訂閱] 。</span><span class="sxs-lookup"><span data-stu-id="bafac-153">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="bafac-154">應用程式會將選取的類別轉換成標籤，並在通知中心內為選取的標籤要求新裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="bafac-154">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="bafac-155">隨即會傳回已註冊的類別，且會顯示在快顯通知中。</span><span class="sxs-lookup"><span data-stu-id="bafac-155">The registered categories are returned and displayed in a toast notification.</span></span>
3. <span data-ttu-id="bafac-156">執行 .NET 主控台應用程式以傳送新的通知。</span><span class="sxs-lookup"><span data-stu-id="bafac-156">Send a new notification by running the .NET Console app.</span></span>  <span data-ttu-id="bafac-157">或者，可以使用 [Azure 傳統入口網站]中通知中樞的 [偵錯] 索引標籤，傳送加註標記的範本通知。</span><span class="sxs-lookup"><span data-stu-id="bafac-157">Alternatively, you can send tagged template notifications using the debug tab of your notification hub in the [Azure Classic Portal].</span></span>
   
    <span data-ttu-id="bafac-158">選取的類別通知會以快顯通知方式出現。</span><span class="sxs-lookup"><span data-stu-id="bafac-158">Notifications for the selected categories appear as toast notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bafac-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bafac-159">Next steps</span></span>
<span data-ttu-id="bafac-160">在本教學課程中，我們了解到如何按類別廣播即時新聞。</span><span class="sxs-lookup"><span data-stu-id="bafac-160">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="bafac-161">請考慮完成下列其中一個強調其他進階通知中心案例的教學課程：</span><span class="sxs-lookup"><span data-stu-id="bafac-161">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="bafac-162">[使用通知中樞廣播已當地語系化的即時新聞]</span><span class="sxs-lookup"><span data-stu-id="bafac-162">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="bafac-163">了解如何擴充即時新聞應用程式，以啟用傳送已當地語系化的通知。</span><span class="sxs-lookup"><span data-stu-id="bafac-163">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[A1]: ./media/notification-hubs-aspnet-backend-android-breaking-news/android-breaking-news1.PNG

<!-- URLs.-->
[get-started]: notification-hubs-android-push-notification-google-gcm-get-started.md
<span data-ttu-id="bafac-164">[使用通知中樞廣播已當地語系化的即時新聞]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="bafac-164">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
<span data-ttu-id="bafac-165">[Azure 傳統入口網站]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="bafac-165">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
