---
title: "aaaSending 安全推播通知與 Azure 通知中心"
description: "了解如何安全 toosend 推播通知 tooan Android 應用程式從 Azure。 程式碼範例是以 Java 及 C# 撰寫。"
documentationcenter: android
keywords: "推播通知,推播訊息,android 推播通知"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a>使用 Azure 通知中樞傳送安全的推播通知
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>概觀
> [!IMPORTANT]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)。
> 
> 

在 Microsoft Azure 推播通知支援可讓您 tooaccess 容易使用、 多平台、 向外延展的推播訊息基礎結構，可大幅簡化 hello 實作針對消費者和企業應用程式的推播通知行動平台。

有時候 tooregulatory 或安全性條件約束，因為應用程式可能會想 tooinclude 中無法透過 hello 標準的推播通知基礎結構傳送的 hello 通知。 本教學課程描述 tooachieve 如何透過 hello 用戶端的 Android 裝置與 hello 應用程式後端之間的安全、 已驗證連線的機密資訊傳送 hello 相同的體驗。

在高層級，hello 流程如下所示：

1. hello 應用程式後端：
   * 在後端資料庫中儲存安全裝載。
   * 會傳送 hello （傳送不安全的資訊） 此通知的 toohello Android 裝置識別碼。
2. hello 在裝置上，當收到 hello 通知 hello 應用程式：
   * hello Android 裝置會連絡 hello 後端要求 hello 安全內容。
   * hello 應用程式可以顯示 hello 裝載為 hello 裝置上的通知。

請務必 toonote hello 上述流程中 （並在本教學課程），我們會假設該 hello 裝置會儲存在本機儲存體，驗證語彙基元之後 hello 使用者登入。 這樣可保證完全完美無瑕的體驗，如 hello 裝置可以擷取 hello 通知安全裝載使用這個語彙基元。 如果您的應用程式不會儲存驗證語彙基元 hello 在裝置上，或可以過期這些語彙基元，hello 裝置的應用程式，在收到 hello 推播通知時應該會顯示提示 hello 使用者 toolaunch hello 應用程式的一般通知。 hello 應用程式然後驗證 hello 使用者，並顯示 hello 通知裝載。

本教學課程會示範如何安全 toosend 推播通知。 它是在 hello 基礎[通知使用者](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md)教學課程中，因此，您應該完成 hello 步驟在該教學課程中第一次如果尚未這麼做。

> [!NOTE]
> 本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)中所述。
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a>修改 hello Android 專案
既然您已修改您應用程式後端 toosend 只 hello*識別碼*的推播通知，您有 toochange 通知和回撥後端 tooretrieve hello 安全訊息 toobe 顯示您的 Android 應用程式 toohandle。
tooachieve 達成此目標，您必須確定您的 Android 應用程式知道 toomake 如何與後端收到 hello 推播通知時 tooauthenticate 本身。

我們現在將修改 hello*登入*流程在順序 toosave hello 驗證標頭值中的 hello 共用您的應用程式喜好設定。 類似的機制可以是使用的 toostore 任何 hello 應用程式的驗證權杖 （例如 OAuth 語彙基元） 會有 toouse，而不需要使用者認證。

1. 在 Android 應用程式專案中，加入下列常數頂端的 hello hello hello **MainActivity**類別：
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. 仍在 hello **MainActivity**類別，更新 hello`getAuthorizationHeader()`方法 toocontain hello 下列程式碼：
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. 新增下列 hello`import`在 hello hello 最上方的陳述式**MainActivity**檔案：
   
        import android.content.SharedPreferences;

現在我們將會變更時收到 hello 通知時所呼叫的 hello 處理常式。

1. 在 hello **MyHandler**類別變更 hello`OnReceive()`方法 toocontain:
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. 然後新增 hello`retrieveNotification()`方法，取代 hello 預留位置`{back-end endpoint}`與部署您的後端時所取得的 hello 後端端點：
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

這個方法會呼叫您的應用程式後端 tooretrieve hello 通知內容使用儲存在 hello hello 認證共用喜好設定，並將它顯示為一般通知。 hello 通知會尋找 toohello 如同任何其他的推播通知的應用程式使用者。

請注意，它比 toohandle hello 情況下，缺少驗證標頭屬性或 hello 後端拒絕動作。 hello 特定處理這些情況通常取決於您目標的使用者經驗。 其中一個選項是 toodisplay hello 使用者 tooauthenticate tooretrieve hello 實際通知的一般提示字元之下一則通知。

## <a name="run-hello-application"></a>執行 hello 應用程式
toorun hello 應用程式中，執行下列 hello:

1. 確定 Azure 中已部署 **AppBackend** 。 如果使用 Visual Studio，請執行 hello **AppBackend** Web API 應用程式。 [ASP.NET Web] 頁面便會隨即顯示。
2. 在 Eclipse 中，實體的 Android 裝置或 hello 模擬器上執行 hello 應用程式。
3. 在 hello Android 應用程式 UI 中，輸入使用者名稱和密碼。 這些可以是任何字串，但它們必須 hello 相同的值。
4. 在 hello Android 應用程式 UI，按一下 **登入**。 然後按一下 [傳送推播] 。

