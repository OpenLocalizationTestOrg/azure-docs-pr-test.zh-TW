1. 在您**應用程式**專案、 開啟 hello 檔案`AndroidManifest.xml`。 在 hello 下面兩個步驟中的 hello 程式碼，取代 *`**my_app_package**`*  hello hello 應用程式套件中的名稱為您的專案。 這是 hello hello 值`package`屬性 hello`manifest`標記。
2. 新增下列新的權限之後 hello 現有 hello`uses-permission`項目：

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. 新增下列程式碼之後 hello hello`application`開頭標記：

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. 開啟 hello 檔案*ToDoActivity.java*，並加入下列 import 陳述式的 hello:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. 加入下列私用變數 toohello 類別 hello。 取代 *`<PROJECT_NUMBER>`* 與 hello 前面程序中的 Google tooyour 應用程式所指派的 hello 專案編號。

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. 變更 hello 定義*MobileServiceClient*從**私人**太**公用靜態**，所以現在看起來像這樣：

        public static MobileServiceClient mClient;
7. 加入新的類別 toohandle 通知。 在 專案總管 中，開啟 hello **src** > **主要** > **java**節點，並以滑鼠右鍵按一下 hello 封裝名稱的節點。 按一下 新增，然後按一下Java 類別。
8. 在 名稱 中，輸入 `MyHandler`，然後按一下確定。

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. 在 hello MyHandler 檔案中，將與 hello 類別宣告：

        public class MyHandler extends NotificationsHandler {
10. 加入下列 import 陳述式的 hello hello`MyHandler`類別：

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. 接著將此成員 toohello`MyHandler`類別：

        public static final int NOTIFICATION_ID = 1;
12. 在 hello`MyHandler`類別中，加入下列程式碼 toooverride hello hello **onRegistered**方法，以與 hello 行動服務的通知中樞註冊您的裝置。

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       }
13. 在 hello`MyHandler`類別中，加入下列程式碼 toooverride hello hello **onReceive**方法，導致 hello 通知 toodisplay 接收時。

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       }
14. 在 hello TodoActivity.java 檔案中，更新 hello **onCreate**方法 hello *ToDoActivity*類別 tooregister hello 通知處理常式類別。 請確定 tooadd 這段程式碼之後 hello *MobileServiceClient*具現化。

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    您的應用程式已更新的 toosupport 推播通知。
