1. <span data-ttu-id="25667-101">在您**應用程式**專案、 開啟 hello 檔案`AndroidManifest.xml`。</span><span class="sxs-lookup"><span data-stu-id="25667-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="25667-102">在 hello 下面兩個步驟中的 hello 程式碼，取代 *`**my_app_package**`*  hello hello 應用程式套件中的名稱為您的專案。</span><span class="sxs-lookup"><span data-stu-id="25667-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="25667-103">這是 hello hello 值`package`屬性 hello`manifest`標記。</span><span class="sxs-lookup"><span data-stu-id="25667-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="25667-104">新增下列新的權限之後 hello 現有 hello`uses-permission`項目：</span><span class="sxs-lookup"><span data-stu-id="25667-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="25667-105">新增下列程式碼之後 hello hello`application`開頭標記：</span><span class="sxs-lookup"><span data-stu-id="25667-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="25667-106">開啟 hello 檔案*ToDoActivity.java*，並加入下列 import 陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="25667-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="25667-107">加入下列私用變數 toohello 類別 hello。</span><span class="sxs-lookup"><span data-stu-id="25667-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="25667-108">取代 *`<PROJECT_NUMBER>`* 與 hello 前面程序中的 Google tooyour 應用程式所指派的 hello 專案編號。</span><span class="sxs-lookup"><span data-stu-id="25667-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="25667-109">變更 hello 定義*MobileServiceClient*從**私人**太**公用靜態**，所以現在看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="25667-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="25667-110">加入新的類別 toohandle 通知。</span><span class="sxs-lookup"><span data-stu-id="25667-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="25667-111">在 專案總管 中，開啟 hello **src** > **主要** > **java**節點，並以滑鼠右鍵按一下 hello 封裝名稱的節點。</span><span class="sxs-lookup"><span data-stu-id="25667-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="25667-112">按一下 新增，然後按一下Java 類別。</span><span class="sxs-lookup"><span data-stu-id="25667-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="25667-113">在 名稱 中，輸入 `MyHandler`，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="25667-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="25667-114">在 hello MyHandler 檔案中，將與 hello 類別宣告：</span><span class="sxs-lookup"><span data-stu-id="25667-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="25667-115">加入下列 import 陳述式的 hello hello`MyHandler`類別：</span><span class="sxs-lookup"><span data-stu-id="25667-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="25667-116">接著將此成員 toohello`MyHandler`類別：</span><span class="sxs-lookup"><span data-stu-id="25667-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="25667-117">在 hello`MyHandler`類別中，加入下列程式碼 toooverride hello hello **onRegistered**方法，以與 hello 行動服務的通知中樞註冊您的裝置。</span><span class="sxs-lookup"><span data-stu-id="25667-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

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
       <span data-ttu-id="25667-118">}</span><span class="sxs-lookup"><span data-stu-id="25667-118">}</span></span>
13. <span data-ttu-id="25667-119">在 hello`MyHandler`類別中，加入下列程式碼 toooverride hello hello **onReceive**方法，導致 hello 通知 toodisplay 接收時。</span><span class="sxs-lookup"><span data-stu-id="25667-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

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
       <span data-ttu-id="25667-120">}</span><span class="sxs-lookup"><span data-stu-id="25667-120">}</span></span>
14. <span data-ttu-id="25667-121">在 hello TodoActivity.java 檔案中，更新 hello **onCreate**方法 hello *ToDoActivity*類別 tooregister hello 通知處理常式類別。</span><span class="sxs-lookup"><span data-stu-id="25667-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="25667-122">請確定 tooadd 這段程式碼之後 hello *MobileServiceClient*具現化。</span><span class="sxs-lookup"><span data-stu-id="25667-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="25667-123">您的應用程式已更新的 toosupport 推播通知。</span><span class="sxs-lookup"><span data-stu-id="25667-123">Your app is now updated toosupport push notifications.</span></span>
