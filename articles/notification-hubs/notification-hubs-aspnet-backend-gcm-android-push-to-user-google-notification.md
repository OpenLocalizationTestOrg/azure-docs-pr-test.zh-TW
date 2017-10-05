---
title: "Azure 通知中樞透過 .NET 後端通知 Android 使用者"
description: "了解如何在 Azure 中將推播通知傳送給使用者。 程式碼範例是以適用於 Android 的 Java 撰寫。"
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
ms.openlocfilehash: 418a4b638dfaa3fee33a7a7242433699205c79f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-android-with-net-backend"></a><span data-ttu-id="51c07-104">Azure 通知中樞透過 .NET 後端通知 Android 使用者</span><span class="sxs-lookup"><span data-stu-id="51c07-104">Azure Notification Hubs Notify Users for Android with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="51c07-105">Overview</span><span class="sxs-lookup"><span data-stu-id="51c07-105">Overview</span></span>
<span data-ttu-id="51c07-106">Azure 中的推播通知支援可讓您存取易於使用、多重平台的大規模推播基礎結構，而大幅簡化消費者和企業應用程式在行動平台上的推播通知實作。</span><span class="sxs-lookup"><span data-stu-id="51c07-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="51c07-107">本教學課程將示範如何使用 Azure 通知中心，來將推播通知傳送到特定裝置上的特定應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="51c07-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="51c07-108">ASP.NET WebAPI 後端可用來驗證用戶端並產生通知，如指引主題[從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)中所示。</span><span class="sxs-lookup"><span data-stu-id="51c07-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="51c07-109">本教學課程以您在 [開始使用通知中樞 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) 教學課程中建立的通知中樞為基礎。</span><span class="sxs-lookup"><span data-stu-id="51c07-109">This tutorial builds on the notification hub that you created in the [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="51c07-110">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="51c07-110">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-the-android-project"></a><span data-ttu-id="51c07-111">建立 Android 專案</span><span class="sxs-lookup"><span data-stu-id="51c07-111">Create the Android Project</span></span>
<span data-ttu-id="51c07-112">下一個步驟說明如何建立 Android 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51c07-112">The next step is to create the Android application.</span></span>

1. <span data-ttu-id="51c07-113">依照 [開始使用通知中心 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) 教學課程來建立並設定您的應用程式，以接收來自 GCM 的推播通知。</span><span class="sxs-lookup"><span data-stu-id="51c07-113">Follow the [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial to create and configure your app to receive push notifications from GCM.</span></span>
2. <span data-ttu-id="51c07-114">開啟您的 **res/layout/activity_main.xml** 檔案，並以下列內容定義取代。</span><span class="sxs-lookup"><span data-stu-id="51c07-114">Open your **res/layout/activity_main.xml** file, replace the with the following content definitions.</span></span>
   
    <span data-ttu-id="51c07-115">這會加入新的 EditText 控制項，以便以使用者身分登入。</span><span class="sxs-lookup"><span data-stu-id="51c07-115">This adds new EditText controls for logging in as a user.</span></span> <span data-ttu-id="51c07-116">此外，也會針對將成為您傳送的通知一部分的使用者名稱標記加入欄位：</span><span class="sxs-lookup"><span data-stu-id="51c07-116">Also a field is added for a username tag that will be part of notifications you send:</span></span>
   
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
3. <span data-ttu-id="51c07-117">開啟 **res/values/strings.xml** 檔案，並以下列幾行程式碼取代 `send_button` 定義，這幾行程式碼可重新定義 `send_button` 的字串並新增其他控制項的字串：</span><span class="sxs-lookup"><span data-stu-id="51c07-117">Open your **res/values/strings.xml** file and replace the `send_button` definition with the following lines that redefine the string for the `send_button` and add strings for the other controls:</span></span>
   
        <string name="usernameHint">Username</string>
        <string name="passwordHint">Password</string>
        <string name="loginButton">1. Log in</string>
        <string name="send_button">2. Send Notification</string>
        <string name="notification_message_tag_hint">
            Recipient username tag
        </string>
   
    <span data-ttu-id="51c07-118">您的 main_activity.xml 圖形版面配置此時應如下所示：</span><span class="sxs-lookup"><span data-stu-id="51c07-118">Your main_activity.xml graphical layout should now look like this:</span></span>
   
    ![][A1]
4. <span data-ttu-id="51c07-119">在與 `MainActivity` 類別相同的套件中，建立名為 **RegisterClient** 的新類別。</span><span class="sxs-lookup"><span data-stu-id="51c07-119">Create a new class named **RegisterClient** in the same package as your `MainActivity` class.</span></span> <span data-ttu-id="51c07-120">將下列程式碼使用於新的類別檔案。</span><span class="sxs-lookup"><span data-stu-id="51c07-120">Use the code below for the new class file.</span></span>
   
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
   
    <span data-ttu-id="51c07-121">為註冊推播通知，此元件會實作連絡應用程式後端所需的 REST 呼叫。</span><span class="sxs-lookup"><span data-stu-id="51c07-121">This component implements the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="51c07-122">它也會在本機儲存通知中心所建立的 *registrationIds* ，如 [從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)中的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="51c07-122">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span> <span data-ttu-id="51c07-123">請注意，當您按一下 [ **登入** ] 按鈕時，系統便會使用儲存在本機儲存體中的授權權杖。</span><span class="sxs-lookup"><span data-stu-id="51c07-123">Note that it uses an authorization token stored in local storage when you click the **Log in** button.</span></span>
5. <span data-ttu-id="51c07-124">在 `MainActivity` 類別中，針對 `NotificationHub` 移除或註解排除您的私用欄位，並對 `RegisterClient` 類別新增一個欄位，以及對 ASP.NET 後端端點新增一個字串。</span><span class="sxs-lookup"><span data-stu-id="51c07-124">In your `MainActivity` class remove or comment out your private field for `NotificationHub`, and add a field for the `RegisterClient` class and a string for your ASP.NET backend's endpoint.</span></span> <span data-ttu-id="51c07-125">請務必使用先前取得的實際後端端點來取代 `<Enter Your Backend Endpoint>`：</span><span class="sxs-lookup"><span data-stu-id="51c07-125">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="51c07-126">例如， `http://mybackend.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="51c07-126">For example, `http://mybackend.azurewebsites.net`.</span></span>

        //private NotificationHub hub;
        private RegisterClient registerClient;
        private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";


1. <span data-ttu-id="51c07-127">在 `MainActivity` 類別的 `onCreate` 方法中，移除或註解排除 `hub` 欄位的初始化和 `registerWithNotificationHubs` 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="51c07-127">In your `MainActivity` class, in the `onCreate` method, remove or comment out the initialization of the `hub` field and the call to the `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="51c07-128">然後加入程式碼以初始化 `RegisterClient` 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="51c07-128">Then add code to initialize an instance of the `RegisterClient` class.</span></span> <span data-ttu-id="51c07-129">此方法應包含下列程式碼行：</span><span class="sxs-lookup"><span data-stu-id="51c07-129">The method should contain the following lines:</span></span>
   
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
2. <span data-ttu-id="51c07-130">在 `MainActivity` 類別中，刪除或註解排除整個 `registerWithNotificationHubs` 方法。</span><span class="sxs-lookup"><span data-stu-id="51c07-130">In your `MainActivity` class, delete or comment out the entire `registerWithNotificationHubs` method.</span></span> <span data-ttu-id="51c07-131">本教學課程不會使用此方法。</span><span class="sxs-lookup"><span data-stu-id="51c07-131">It will not be used in this tutorial.</span></span>
3. <span data-ttu-id="51c07-132">在 **MainActivity.java** 檔案中新增下列 `import` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="51c07-132">Add the following `import` statements to your **MainActivity.java** file.</span></span>
   
        import android.widget.Button;
        import java.io.UnsupportedEncodingException;
        import android.content.Context;
        import java.util.HashSet;
        import android.widget.Toast;
        import org.apache.http.client.ClientProtocolException;
        import java.io.IOException;
        import org.apache.http.HttpStatus;
4. <span data-ttu-id="51c07-133">然後，新增下列方法來處理 [ **登入** ] 按鈕 click 事件及傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="51c07-133">Then, add the following methods to handle the **Log in** button click event and sending push notifications.</span></span>
   
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
                        DialogNotify("MainActivity - Failed to register", e.getMessage());
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
         * This method calls the ASP.NET WebAPI backend to send the notification message
         * to the platform notification service based on the pns parameter.
         *
         * @param pns     The platform notification service to send the notification message to. Must
         *                be one of the following ("wns", "gcm", "apns").
         * @param userTag The tag for the user who will receive the notification message. This string
         *                must not contain spaces or special characters.
         * @param message The notification message string. This string must include the double quotes
         *                to be used as JSON content.
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
                        DialogNotify("MainActivity - Failed to send " + pns + " notification ", e.getMessage());
                        return e;
                    }
   
                    return null;
                }
            }.execute(null, null, null);
        }

    <span data-ttu-id="51c07-134">[登入] 按鈕的 `login` 處理常式會使用輸入使用者名稱和密碼 (請注意，這代表驗證結構描述使用的任何權杖) 產生基本驗證權杖，然後使用 `RegisterClient` 呼叫後端進行註冊。</span><span class="sxs-lookup"><span data-stu-id="51c07-134">The `login` handler for the **Log in** button generates a basic authentication token using on the input username and password (note that this represents any token your authentication scheme uses), then it uses `RegisterClient` to call the backend for registration.</span></span>

    <span data-ttu-id="51c07-135">`sendPush` 方法會呼叫後端，以根據使用者標記觸發使用者的安全通知。</span><span class="sxs-lookup"><span data-stu-id="51c07-135">The `sendPush` method calls the backend to trigger a secure notification to the user based on the user tag.</span></span> <span data-ttu-id="51c07-136">`sendPush` 鎖定目標的平台通知服務取決於傳入的 `pns` 字串。</span><span class="sxs-lookup"><span data-stu-id="51c07-136">The platform notification service that `sendPush` targets depends on the `pns` string passed in.</span></span>

1. <span data-ttu-id="51c07-137">在 `MainActivity` 類別中，更新 `sendNotificationButtonOnClick` 方法以透過使用者選取的平台通知服務呼叫 `sendPush` 方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="51c07-137">In your `MainActivity` class, update the `sendNotificationButtonOnClick` method to call the `sendPush` method with the user's selected platform notification services as follows.</span></span>
   
       /**
        * Send Notification button click handler. This method sends the push notification
        * message to each platform selected.
        *
        * @param v The view
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

## <a name="run-the-application"></a><span data-ttu-id="51c07-138">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="51c07-138">Run the Application</span></span>
1. <span data-ttu-id="51c07-139">在使用 Android Studio 的裝置或模擬器上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="51c07-139">Run the application on a device or an emulator using Android Studio.</span></span>
2. <span data-ttu-id="51c07-140">在 Android 應用程式中，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="51c07-140">In the Android app, enter a username and password.</span></span> <span data-ttu-id="51c07-141">兩者必須是相同的字串值，而且不得包含空格或特殊字元。</span><span class="sxs-lookup"><span data-stu-id="51c07-141">They must both be the same string value and they must not contain spaces or special characters.</span></span>
3. <span data-ttu-id="51c07-142">在 Android 應用程式中，按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="51c07-142">In the Android app, click **Log in**.</span></span> <span data-ttu-id="51c07-143">等待快顯訊息出現，指出 [ **已登入並註冊**]。</span><span class="sxs-lookup"><span data-stu-id="51c07-143">Wait for a toast message that states **Logged in and registered**.</span></span> <span data-ttu-id="51c07-144">這會啟用 [ **傳送通知** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51c07-144">This will enable the **Send Notification** button.</span></span>
   
    ![][A2]
4. <span data-ttu-id="51c07-145">按一下切換按鈕，啟用您已執行應用程式並註冊使用者的所有平台。</span><span class="sxs-lookup"><span data-stu-id="51c07-145">Click the toggle buttons to enable all platforms where you have ran the app and registered a user.</span></span>
5. <span data-ttu-id="51c07-146">輸入將會收到通知訊息的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="51c07-146">Enter the user's name that will receive the notification message.</span></span> <span data-ttu-id="51c07-147">該使用者必須在目標裝置上註冊通知。</span><span class="sxs-lookup"><span data-stu-id="51c07-147">That user must be registered for notifications on the target devices.</span></span>
6. <span data-ttu-id="51c07-148">輸入做為推播通知訊息的訊息，以便使用者接收。</span><span class="sxs-lookup"><span data-stu-id="51c07-148">Enter a message for the user to receive as a push notification message.</span></span>
7. <span data-ttu-id="51c07-149">按一下 [ **傳送通知**]。</span><span class="sxs-lookup"><span data-stu-id="51c07-149">Click **Send Notification**.</span></span>  <span data-ttu-id="51c07-150">每個具有相符使用者名稱標記之註冊的裝置都會收到推播通知。</span><span class="sxs-lookup"><span data-stu-id="51c07-150">Each device that has a registration with the matching username tag will receive the push notification.</span></span>

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
