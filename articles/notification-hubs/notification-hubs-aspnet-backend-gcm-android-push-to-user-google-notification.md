---
title: "與.NET 後端 aaaAzure 通知中樞通知使用者 for Android"
description: "了解如何 toosend 推播通知 toousers 在 Azure 中。 程式碼範例是以適用於 Android 的 Java 撰寫。"
documentationcenter: android
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: b042d2e6fb7f7c861c378526a8a0d59ab75beef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="fb32c-104">Azure 通知中樞透過 .NET 後端通知 Android 使用者</span><span class="sxs-lookup"><span data-stu-id="fb32c-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="fb32c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="fb32c-105">Overview</span></span>
<span data-ttu-id="fb32c-106">在 Azure 中的推播通知支援可讓您 tooaccess 方便使用、 多平台，並向外延展推播基礎結構，可大幅簡化 hello 實作消費者和企業行動應用程式的應用程式的推播通知平台。</span><span class="sxs-lookup"><span data-stu-id="fb32c-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="fb32c-107">本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa 特定的應用程式使用者在特定的裝置上。</span><span class="sxs-lookup"><span data-stu-id="fb32c-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="fb32c-108">ASP.NET WebAPI 後端使用的 tooauthenticate 用戶端和 toogenerate 通知中所示 hello 指引主題[從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)。</span><span class="sxs-lookup"><span data-stu-id="fb32c-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="fb32c-109">本教學課程是您在 hello hello 通知中樞[開始使用通知中心 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="fb32c-109">This tutorial builds on hello notification hub that you created in hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="fb32c-110">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="fb32c-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-hello-android-project"></a><span data-ttu-id="fb32c-111">建立 hello Android 專案</span><span class="sxs-lookup"><span data-stu-id="fb32c-111">Create hello Android Project</span></span>
<span data-ttu-id="fb32c-112">hello 下一個步驟是 toocreate hello Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb32c-112">hello next step is toocreate hello Android application.</span></span>

1. <span data-ttu-id="fb32c-113">請遵循 hello[開始使用通知中心 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)教學課程 toocreate 及設定應用程式 tooreceive 推播通知從 GCM。</span><span class="sxs-lookup"><span data-stu-id="fb32c-113">Follow hello [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial toocreate and configure your app tooreceive push notifications from GCM.</span></span>
2. <span data-ttu-id="fb32c-114">開啟您**res/layout/activity_main.xml**檔案時，請取代下列內容定義的 hello hello。</span><span class="sxs-lookup"><span data-stu-id="fb32c-114">Open your **res/layout/activity_main.xml** file, replace hello with hello following content definitions.</span></span>
   
    <span data-ttu-id="fb32c-115">這會加入新的 EditText 控制項，以便以使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="fb32c-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="fb32c-116">此外，也會針對將成為您傳送的通知一部分的使用者名稱標記加入欄位：</span><span class="sxs-lookup"><span data-stu-id="fb32c-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
            android:layout_height="match_parent" android:paddingLeft="@dimen/activity_horizontal_margin"
            android:paddingRight="@dimen/activity_horizontal_margin"
            android:paddingTop="@dimen/activity_vertical_margin"
            android:paddingBottom="@dimen/activity_vertical_margin" tools:context=".MainActivity">
   
        <EditText
            android:id="@+id/usernameText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/usernameHint"
            android:layout_above="@+id/passwordText"
            android:layout_alignParentEnd="true" />
        <EditText
            android:id="@+id/passwordText"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:ems="10"
            android:hint="@string/passwordHint"
            android:inputType="textPassword"
            android:layout_above="@+id/buttonLogin"
            android:layout_alignParentEnd="true" />
        <Button
            android:id="@+id/buttonLogin"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/loginButton"
            android:onClick="login"
            android:layout_above="@+id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:layout_marginBottom="24dp" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="WNS on"
            android:textOff="WNS off"
            android:id="@+id/toggleButtonWNS"
            android:layout_toLeftOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="GCM on"
            android:textOff="GCM off"
            android:id="@+id/toggleButtonGCM"
            android:checked="true"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true" />
        <ToggleButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textOn="APNS on"
            android:textOff="APNS off"
            android:id="@+id/toggleButtonAPNS"
            android:layout_toRightOf="@id/toggleButtonGCM"
            android:layout_centerVertical="true" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessageTag"
            android:layout_below="@id/toggleButtonGCM"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_tag_hint" />
        <EditText
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/editTextNotificationMessage"
            android:layout_below="@+id/editTextNotificationMessageTag"
            android:layout_centerHorizontal="true"
            android:hint="@string/notification_message_hint" />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/send_button"
            android:id="@+id/sendbutton"
            android:onClick="sendNotificationButtonOnClick"
            android:layout_below="@+id/editTextNotificationMessage"
            android:layout_centerHorizontal="true" />
        </RelativeLayout>
3. <span data-ttu-id="fb32c-117">開啟您**res/values/strings.xml**檔案，並將 hello`send_button`定義 hello 下列各行重新定義 hello 字串 hello`send_button`並加入其他控制項的字串 hello:</span><span class="sxs-lookup"><span data-stu-id="fb32c-117">Open your **res/values/strings.xml** file and replace hello `send_button` definition with hello following lines that redefine hello string for hello `send_button` and add strings for hello other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="fb32c-118">您的 main_activity.xml 圖形版面配置此時應如下所示：</span><span class="sxs-lookup"><span data-stu-id="fb32c-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="fb32c-119">建立新的類別，名為**RegisterClient**相同封裝中 hello 做為您`MainActivity`類別。</span><span class="sxs-lookup"><span data-stu-id="fb32c-119">Create a new class named **RegisterClient** in hello same package as your `MainActivity` class.</span></span> <span data-ttu-id="fb32c-120">下列程式碼會 hello hello 新類別檔案使用。</span><span class="sxs-lookup"><span data-stu-id="fb32c-120">Use hello code below for hello new class file.</span></span>
   
        import java.io.IOException;
        import java.io.UnsupportedEncodingException;
        import java.util.Set;
   
        import org.apache.http.HttpResponse;
        import org.apache.http.HttpStatus;
        import org.apache.http.client.ClientProtocolException;
        import org.apache.http.client.HttpClient;
        import org.apache.http.client.methods.HttpPost;
        import org.apache.http.client.methods.HttpPut;
        import org.apache.http.client.methods.HttpUriRequest;
        import org.apache.http.entity.StringEntity;
        import org.apache.http.impl.client.DefaultHttpClient;
        import org.apache.http.util.EntityUtils;
        import org.json.JSONArray;
        import org.json.JSONException;
        import org.json.JSONObject;
   
        import android.content.Context;
        import android.content.SharedPreferences;
        import android.util.Log;
   
        public class RegisterClient {
            private static final String PREFS_NAME = "ANHSettings";
            private static final String REGID_SETTING_NAME = "ANHRegistrationId";
            private String Backend_Endpoint;
            SharedPreferences settings;
            protected HttpClient httpClient;
            private String authorizationHeader;
   
            public RegisterClient(Context context, String backendEnpoint) {
                super();
                this.settings = context.getSharedPreferences(PREFS_NAME, 0);
                httpClient =  new DefaultHttpClient();
                Backend_Endpoint = backendEnpoint + "/api/register";
            }
   
            public String getAuthorizationHeader() {
                return authorizationHeader;
            }
   
            public void setAuthorizationHeader(String authorizationHeader) {
                this.authorizationHeader = authorizationHeader;
            }
   
            public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
                String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
   
                JSONObject deviceInfo = new JSONObject();
                deviceInfo.put("Platform", "gcm");
                deviceInfo.put("Handle", handle);
                deviceInfo.put("Tags", new JSONArray(tags));
   
                int statusCode = upsertRegistration(registrationId, deviceInfo);
   
                if (statusCode == HttpStatus.SC_OK) {
                    return;
                } else if (statusCode == HttpStatus.SC_GONE){
                    settings.edit().remove(REGID_SETTING_NAME).commit();
                    registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                    statusCode = upsertRegistration(registrationId, deviceInfo);
                    if (statusCode != HttpStatus.SC_OK) {
                        Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                        throw new RuntimeException("Error upserting registration");
                    }
                } else {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            }
   
            private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                    throws UnsupportedEncodingException, IOException,
                    ClientProtocolException {
                HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
                request.setEntity(new StringEntity(deviceInfo.toString()));
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                request.addHeader("Content-Type", "application/json");
                HttpResponse response = httpClient.execute(request);
                int statusCode = response.getStatusLine().getStatusCode();
                return statusCode;
            }
   
            private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
                if (settings.contains(REGID_SETTING_NAME))
                    return settings.getString(REGID_SETTING_NAME, null);
   
                HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
                request.addHeader("Authorization", "Basic "+authorizationHeader);
                HttpResponse response = httpClient.execute(request);
                if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                    throw new RuntimeException("Error creating Notification Hubs registrationId");
                }
                String registrationId = EntityUtils.toString(response.getEntity());
                registrationId = registrationId.substring(1, registrationId.length()-1);
   
                settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
   
                return registrationId;
            }
        }
   
    <span data-ttu-id="fb32c-121">此元件會實作推播通知的順序 tooregister hello REST 呼叫需要的 toocontact hello 應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="fb32c-121">This component implements hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="fb32c-122">它也在本機儲存 hello *Registrationid*中所述的通知中樞建立 hello[從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)。</span><span class="sxs-lookup"><span data-stu-id="fb32c-122">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="fb32c-123">請注意，它會使用儲存在本機儲存體，當您按一下 hello 授權權杖**登入** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb32c-123">Note that it uses an authorization token stored in local storage when you click hello **Log in** button.</span></span>
5. <span data-ttu-id="fb32c-124">在您`MainActivity`類別移除或註解您的私用欄位來`NotificationHub`，並加入一個欄位 hello`RegisterClient`類別和您的 ASP.NET 後端端點的字串。</span><span class="sxs-lookup"><span data-stu-id="fb32c-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for hello `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="fb32c-125">要確定 tooreplace `<Enter Your Backend Endpoint>` hello 與實際的後端端點先前取得。</span><span class="sxs-lookup"><span data-stu-id="fb32c-125">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="fb32c-126">例如： `http://mybackend.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="fb32c-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="fb32c-127">在您`MainActivity`類別，在 hello`onCreate`方法中，移除或註解的 hello hello 初始化`hub`欄位和 hello 呼叫 toohello`registerWithNotificationHubs`方法。</span><span class="sxs-lookup"><span data-stu-id="fb32c-127">In your `MainActivity` class, in hello `onCreate` method, remove or comment out hello initialization of hello `hub` field and hello call toohello `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="fb32c-128">然後加入程式碼 tooinitialize hello 的執行個體`RegisterClient`類別。</span><span class="sxs-lookup"><span data-stu-id="fb32c-128">Then add code tooinitialize an instance of hello `RegisterClient` class.</span></span> <span data-ttu-id="fb32c-129">hello 方法應該包含下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="fb32c-129">hello method should contain hello following lines:</span></span>
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
   
            MyHandler.mainActivity = this;
            NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);
            gcm = GoogleCloudMessaging.getInstance(this);
   
            //hub = new NotificationHub(HubName, HubListenConnectionString, this);
            //registerWithNotificationHubs();
   
            registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
   
            setContentView(R.layout.activity_main);
        }
2. <span data-ttu-id="fb32c-130">在您`MainActivity`類別、 刪除或標記為註解整個 hello`registerWithNotificationHubs`方法。</span><span class="sxs-lookup"><span data-stu-id="fb32c-130">In your `MainActivity` class, delete or comment out hello entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="fb32c-131">本教學課程不會使用此方法。</span><span class="sxs-lookup"><span data-stu-id="fb32c-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="fb32c-132">新增下列 hello`import`陳述式 tooyour **MainActivity.java**檔案。</span><span class="sxs-lookup"><span data-stu-id="fb32c-132">Add hello following `import` statements tooyour **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="fb32c-133">然後，加入下列方法 toohandle hello hello**登入**按鈕點選事件及傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="fb32c-133">Then, add hello following methods toohandle hello **Log in** button click event and sending push notifications.</span></span>
   
        @Override
        protected void onStart() {
            super.onStart();
            Button sendPush = (Button) findViewById(R.id.sendbutton);
            sendPush.setEnabled(false);
        }
   
        public void login(View view) throws UnsupportedEncodingException {
            this.registerClient.setAuthorizationHeader(getAuthorizationHeader());
   
            final Context context = this;
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        String regid = gcm.register(SENDER_ID);
                        registerClient.register(regid, new HashSet<String>());
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed tooregister", e.getMessage());
                        return e;
                    }
                    return null;
                }
   
                protected void onPostExecute(Object result) {
                    Button sendPush = (Button) findViewById(R.id.sendbutton);
                    sendPush.setEnabled(true);
                    Toast.makeText(context, "Logged in and registered.",
                            Toast.LENGTH_LONG).show();
                }
            }.execute(null, null, null);
        }
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
            return basicAuthHeader;
        }
   
        /**
         * This method calls hello ASP.NET WebAPI backend toosend hello notification message
         * toohello platform notification service based on hello pns parameter.
         *
         * @param pns     hello platform notification service toosend hello notification message to. Must
         *                be one of hello following ("wns", "gcm", "apns").
         * @param userTag hello tag for hello user who will receive hello notification message. This string
         *                must not contain spaces or special characters.
         * @param message hello notification message string. This string must include hello double quotes
         *                toobe used as JSON content.
         */
        public void sendPush(final String pns, final String userTag, final String message)
                throws ClientProtocolException, IOException {
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
   
                        String uri = BACKEND_ENDPOINT + "/api/notifications";
                        uri += "?pns=" + pns;
                        uri += "&to_tag=" + userTag;
   
                        HttpPost request = new HttpPost(uri);
                        request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                        request.setEntity(new StringEntity(message));
                        request.addHeader("Content-Type", "application/json");
   
                        HttpResponse response = new DefaultHttpClient().execute(request);
   
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                            throw new RuntimeException("Error sending notification");
                        }
                    } catch (Exception e) {
                        DialogNotify("MainActivity - Failed toosend " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    <span data-ttu-id="fb32c-134">hello `login` hello 的處理常式**登入**按鈕會產生基本驗證語彙基元 using hello 輸入使用者名稱和密碼 （注意，這表示您的驗證配置會使用語彙基元），然後它會使用`RegisterClient`toocall hello 後的端註冊。</span><span class="sxs-lookup"><span data-stu-id="fb32c-134">hello `login` handler for hello **Log in** button generates a basic authentication token using on hello input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` toocall hello backend for registration.</span></span>

    <span data-ttu-id="fb32c-135">hello`sendPush`方法呼叫 hello 後端 tootrigger 安全通知 toohello 使用者根據 hello 使用者標記。</span><span class="sxs-lookup"><span data-stu-id="fb32c-135">hello `sendPush` method calls hello backend tootrigger a secure notification toohello user based on hello user tag.</span></span> <span data-ttu-id="fb32c-136">hello 平台通知服務`sendPush`目標取決於 hello`pns`傳入的字串。</span><span class="sxs-lookup"><span data-stu-id="fb32c-136">hello platform notification service that `sendPush` targets depends on hello `pns` string passed in.</span></span>

1. <span data-ttu-id="fb32c-137">在您`MainActivity`類別，更新 hello`sendNotificationButtonOnClick`方法 toocall hello`sendPush`方法與 hello 使用者選取的平台通知服務，如下所示。</span><span class="sxs-lookup"><span data-stu-id="fb32c-137">In your `MainActivity` class, update hello `sendNotificationButtonOnClick` method toocall hello `sendPush` method with hello user's selected platform notification services as follows.</span></span>
   
       /**
        * Send Notification button click handler. This method sends hello push notification
        * message tooeach platform selected.
        *
        * @param v hello view
        */
       public void sendNotificationButtonOnClick(View v)
               throws ClientProtocolException, IOException {
   
           String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                   .getText().toString();
           String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                   .getText().toString();
   
           // JSON String
           nhMessage = "\"" + nhMessage + "\"";
   
           if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
           {
               sendPush("wns", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonGCM)).isChecked())
           {
               sendPush("gcm", nhMessageTag, nhMessage);
           }
           if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
           {
               sendPush("apns", nhMessageTag, nhMessage);
           }
       }

## <a name="run-hello-application"></a><span data-ttu-id="fb32c-138">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="fb32c-138">Run hello Application</span></span>
1. <span data-ttu-id="fb32c-139">裝置或使用 Android Studio 模擬器上執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fb32c-139">Run hello application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="fb32c-140">在 hello Android 應用程式中，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="fb32c-140">In hello Android app, enter a username and password.</span></span> <span data-ttu-id="fb32c-141">兩者都是 hello 相同字串值，而且它們不能包含空格或特殊字元。</span><span class="sxs-lookup"><span data-stu-id="fb32c-141">They must both be hello same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="fb32c-142">在 hello Android 應用程式中，按一下 **登入**。</span><span class="sxs-lookup"><span data-stu-id="fb32c-142">In hello Android app, click **Log in**.</span></span> <span data-ttu-id="fb32c-143">等待快顯訊息出現，指出 [ **已登入並註冊**]。</span><span class="sxs-lookup"><span data-stu-id="fb32c-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="fb32c-144">這會讓 hello**傳送通知** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fb32c-144">This will enable hello **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="fb32c-145">按一下 hello 切換按鈕 tooenable 您擁有的所有平台執行 hello 應用程式和註冊的使用者。</span><span class="sxs-lookup"><span data-stu-id="fb32c-145">Click hello toggle buttons tooenable all platforms where you have ran hello app and registered a user.</span></span>
5. <span data-ttu-id="fb32c-146">輸入將會收到 hello 通知訊息的 hello 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="fb32c-146">Enter hello user's name that will receive hello notification message.</span></span> <span data-ttu-id="fb32c-147">該使用者必須註冊 hello 目標裝置上的通知。</span><span class="sxs-lookup"><span data-stu-id="fb32c-147">That user must be registered for notifications on hello target devices.</span></span>
6. <span data-ttu-id="fb32c-148">輸入 hello 使用者 tooreceive 為推播通知訊息的訊息。</span><span class="sxs-lookup"><span data-stu-id="fb32c-148">Enter a message for hello user tooreceive as a push notification message.</span></span>
7. <span data-ttu-id="fb32c-149">按一下 [ **傳送通知**]。</span><span class="sxs-lookup"><span data-stu-id="fb32c-149">Click **Send Notification**.</span></span>  <span data-ttu-id="fb32c-150">每個 hello 比對的使用者名稱標記的已註冊的裝置將會收到 hello 推播通知。</span><span class="sxs-lookup"><span data-stu-id="fb32c-150">Each device that has a registration with hello matching username tag will receive hello push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
