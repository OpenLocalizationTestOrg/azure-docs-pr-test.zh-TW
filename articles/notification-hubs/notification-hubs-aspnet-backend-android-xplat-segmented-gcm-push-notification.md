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
# <a name="use-notification-hubs-toosend-breaking-news"></a>使用通知中樞 toosend 最新消息
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>概觀
本主題說明如何 toouse Azure 通知中樞 toobroadcast 重大消息通知 tooan Android 應用程式。 完成時，您將會是能 tooregister 中斷您感興趣的新聞分類，並且接收只有那些類別目錄的推播通知。 這個案例是許多應用程式的常見模式，通知其中有傳送 toobe toogroups 的先前尚未宣告欄位，例如 RSS 讀取器、 應用程式等的音樂迷感興趣的使用者。

啟用廣播的案例包括下列一個或多個*標記*時建立 hello 通知中樞的註冊。 當通知傳送 tooa 標記時，所有已註冊的裝置 hello 標記會收到 hello 通知。 標記是只是字串，因為它們不需要預先佈建 toobe。 如需標記的詳細資訊，請參閱太[通知中樞路由和標記運算式](notification-hubs-tags-segment-push-message.md)。

## <a name="prerequisites"></a>必要條件
本主題是根據您在建立 hello 應用程式[開始使用通知中樞][get-started]。 開始本教學課程之前，您必須已完成[開始使用通知中樞][get-started]。

## <a name="add-category-selection-toohello-app"></a>加入類別目錄選取 toohello 應用程式
hello 第一個步驟為 tooadd hello UI 項目 tooyour 現有主要活動可讓 hello 使用者 tooselect 類別 tooregister。 使用者選取的 hello 類別會儲存在 hello 裝置。 Hello 應用程式啟動時，裝置註冊會建立您的通知中樞與 hello 選取類別目錄中，為標記。

1. 開啟您 res/layout/activity_main.xml 檔案，並取代 hello hello 下列內容：
   
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
2. 開啟 res/values/strings.xml 檔案並加入下列行 hello:
   
        <string name="button_subscribe">Subscribe</string>
        <string name="label_world">World</string>
        <string name="label_politics">Politics</string>
        <string name="label_business">Business</string>
        <string name="label_technology">Technology</string>
        <string name="label_science">Science</string>
        <string name="label_sports">Sports</string>
   
    您的 main_activity.xml 圖形版面配置此時應如下所示：
   
    ![][A1]
3. 現在建立類別**通知**相同封裝中 hello 做為您**MainActivity**類別。
   
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
   
    這個類別使用新聞此裝置有 tooreceive hello 本機儲存體 toostore hello 的類別。 它也包含這些類別的方法 tooregister。
4. 在您的 **MainActivity** 類別中，移除您 **NotificationHub** 和 **GoogleCloudMessaging** 的私人欄位，並新增 [通知] 的欄位：
   
        // private GoogleCloudMessaging gcm;
        // private NotificationHub hub;
        private Notifications notifications;
5. 然後，在 hello **onCreate**方法，移除 hello 初始化 hello**中樞**欄位和 hello **registerWithNotificationHubs**方法。 然後加入下列行初始化執行個體的 hello hello**通知**類別。 

        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
            MyHandler.mainActivity = this;

            NotificationsManager.handleNotifications(this, SENDER_ID,
                    MyHandler.class);

            notifications = new Notifications(this, SENDER_ID, HubName, HubListenConnectionString);

            notifications.subscribeToCategories(notifications.retrieveCategories());
        }

    `HubName`和`HubListenConnectionString`應該已經設定以 hello`<hub name>`和`<connection string with listen access>`預留位置取代通知中樞名稱和 hello 的連接字串*DefaultListenSharedAccessSignature*取得稍早。

    > [AZURE.NOTE] 發佈的用戶端應用程式的認證不是一般安全的因為您只應該與用戶端應用程式來散發 hello 接聽 」 存取權的索引鍵。 接聽存取啟用通知，但現有的註冊您的應用程式 tooregister 無法修改，而且無法傳送通知。 hello 完整的存取金鑰會用於傳送通知和變更現有註冊的受保護的後端服務。


1. 然後，加入下列 hello 匯入和`subscribe`方法 toohandle hello 訂閱按鈕 click 事件：
   
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
   
    這個方法會建立一份類別目錄，並使用 hello**通知**類別 toostore hello 本機儲存體中的 hello 清單，並使用您的通知中樞註冊 hello 相對應的標記。 類別目錄會變更時，重新建立 hello 註冊 hello 新類別。

您的應用程式目前處於無法 toostore 一組類別目錄 hello 裝置上的本機儲存體，並向 hello 通知中樞，每當 hello 使用者變更 hello 選取的類別。

## <a name="register-for-notifications"></a>註冊通知
這些步驟註冊在啟動時使用已儲存在本機儲存體的 hello 類別 hello 通知中樞。

> [!NOTE]
> 因為 hello registrationId 指派透過 Google Cloud Messaging (GCM) 可以在任何時間變更，您應該註冊通知經常 tooavoid 通知失敗。 每次該 hello 應用程式啟動時，這個範例會註冊通知。 針對經常執行的應用程式，一天一次以上，您可以可能略過註冊 toopreserve 頻寬如果少於一天，已經過 hello 先前的登錄。
> 
> 

1. 新增下列程式碼結尾 hello hello hello **onCreate**方法在 hello **MainActivity**類別：
   
        notifications.subscribeToCategories(notifications.retrieveCategories());
   
    這可確保，每次 hello 應用程式啟動時從本機儲存體擷取 hello 類別並要求這些分類的登錄。 
2. 然後更新 hello`onStart()`方法 hello`MainActivity`類別，如下所示：
   
    @Override  protected void onStart() {
   
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
    }
   
    這會更新依據先前儲存的類別目錄的 hello 狀態 hello 主要活動。

hello 應用程式現在已完成，而且可以是儲存一組類別目錄中與 hello 通知中樞的 hello 裝置使用的本機儲存體 tooregister，每當 hello 使用者變更 hello 選取的類別。 接下來，我們會定義可以傳送類別通知 toothis 應用程式後端。

## <a name="sending-tagged-notifications"></a>傳送加註標記的通知
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>執行 hello 應用程式，並產生通知
1. 在 Android Studio 中，建置 hello 應用程式並開始在裝置或模擬器上。
   
    Hello 應用程式 UI 提供一組切換，請注意，可讓您選擇以 hello 類別 toosubscribe。
2. 啟用一或多個類別切換，然後按一下 [訂閱] 。
   
    hello 應用程式將選取的 hello 類別轉換成標記，並從 hello 通知中樞要求新的裝置註冊 hello 選取標記。 hello 已註冊的類別會傳回並顯示在快顯通知。
3. 藉由執行 hello.NET 主控台應用程式傳送新的通知。  或者，您可以傳送 hello 中使用的通知中樞的 hello 偵錯 索引標籤的標記的範本通知[Azure 傳統入口網站]。
   
    通知 hello 選取類別目錄會顯示為快顯通知。

## <a name="next-steps"></a>後續步驟
在此教學課程中我們學到如何 toobroadcast 依類別目錄中最新消息。 完成下列其中一個 hello 下列反白顯示其他進階的通知中心案例的教學課程，請考慮：

* [使用通知中樞 toobroadcast 當地語系化重大消息]
  
    了解如何傳送 tooenable 新聞應用程式的重大 tooexpand hello 當地語系化通知。

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
