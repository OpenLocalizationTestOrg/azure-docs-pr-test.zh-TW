1. <span data-ttu-id="41923-101">在您的 **app** 專案中開啟 `AndroidManifest.xml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="41923-101">In your **app** project, open the file `AndroidManifest.xml`.</span></span> <span data-ttu-id="41923-102">在下兩個步驟的程式碼中，以專案的應用程式套件名稱取代 *`**my_app_package**`*。</span><span class="sxs-lookup"><span data-stu-id="41923-102">In the code in the next two steps, replace *`**my_app_package**`* with the name of the app package for your project.</span></span> <span data-ttu-id="41923-103">這是 `manifest` 標籤`package` 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="41923-103">This is the value of the `package` attribute of the `manifest` tag.</span></span>
2. <span data-ttu-id="41923-104">在現有 `uses-permission` 元素中新增下列新權限：</span><span class="sxs-lookup"><span data-stu-id="41923-104">Add the following new permissions after the existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="41923-105">在 `application` 起始標籤後新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="41923-105">Add the following code after the `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="41923-106">開啟 ToDoItemActivity.java 檔案，新增下列 import 陳述式：</span><span class="sxs-lookup"><span data-stu-id="41923-106">Open the file *ToDoActivity.java*, and add the following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="41923-107">將下列私用變數新增至類別。</span><span class="sxs-lookup"><span data-stu-id="41923-107">Add the following private variable to the class.</span></span> <span data-ttu-id="41923-108">以先前程序中由 Google 指派給您應用程式的專案編號取代 *`<PROJECT_NUMBER>`*。</span><span class="sxs-lookup"><span data-stu-id="41923-108">Replace *`<PROJECT_NUMBER>`* with the project number assigned by Google to your app in the preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="41923-109">將 *MobileServiceClient* 的定義從 [私用] 變更為 [公用靜態]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="41923-109">Change the definition of *MobileServiceClient* from **private** to **public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="41923-110">新增類別來處理通知。</span><span class="sxs-lookup"><span data-stu-id="41923-110">Add a new class to handle notifications.</span></span> <span data-ttu-id="41923-111">在 [專案總管] 中，開啟 **src** > **main** > **java** 節點，然後以滑鼠右鍵按一下套件名稱節點。</span><span class="sxs-lookup"><span data-stu-id="41923-111">In Project Explorer, open the **src** > **main** > **java** nodes, and right-click the package name node.</span></span> <span data-ttu-id="41923-112">按一下 [新增]，然後按一下 [Java 類別]。</span><span class="sxs-lookup"><span data-stu-id="41923-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="41923-113">在 [名稱] 中，輸入 `MyHandler`，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="41923-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="41923-114">在 MyHandler 檔案中，將類別宣告取代為：</span><span class="sxs-lookup"><span data-stu-id="41923-114">In the MyHandler file, replace the class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="41923-115">為 `MyHandler` 類別新增下列匯入陳述式：</span><span class="sxs-lookup"><span data-stu-id="41923-115">Add the following import statements for the `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="41923-116">接著，將下列成員新增至 `MyHandler` 類別：</span><span class="sxs-lookup"><span data-stu-id="41923-116">Next add this member to the `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="41923-117">在 `MyHandler` 類別中，新增下列程式碼以覆寫 **onRegistered** 方法 (向行動服務通知中樞註冊您的裝置)。</span><span class="sxs-lookup"><span data-stu-id="41923-117">In the `MyHandler` class, add the following code to override the **onRegistered** method, which registers your device with the mobile service notification hub.</span></span>

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
       <span data-ttu-id="41923-118">}</span><span class="sxs-lookup"><span data-stu-id="41923-118">}</span></span>
13. <span data-ttu-id="41923-119">在 `MyHandler` 類別中，新增下列程式碼以覆寫 **onReceive** 方法 (在收到通知時隨即顯示)。</span><span class="sxs-lookup"><span data-stu-id="41923-119">In the `MyHandler` class, add the following code to override the **onReceive** method, which causes the notification to display when it is received.</span></span>

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
       <span data-ttu-id="41923-120">}</span><span class="sxs-lookup"><span data-stu-id="41923-120">}</span></span>
14. <span data-ttu-id="41923-121">回到 TodoActivity.java 檔案，更新 **ToDoActivity** 類別的 *onCreate* 方法，以註冊通知處理常式類別。</span><span class="sxs-lookup"><span data-stu-id="41923-121">Back in the TodoActivity.java file, update the **onCreate** method of the *ToDoActivity* class to register the notification handler class.</span></span> <span data-ttu-id="41923-122">請務必在 *MobileServiceClient* 具現化之後，新增此程式碼。</span><span class="sxs-lookup"><span data-stu-id="41923-122">Make sure to add this code after the *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="41923-123">您的應用程式現在已更新為支援推播通知。</span><span class="sxs-lookup"><span data-stu-id="41923-123">Your app is now updated to support push notifications.</span></span>
