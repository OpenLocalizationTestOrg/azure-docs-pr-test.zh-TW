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
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="77cc1-105">使用 Azure 通知中樞傳送安全的推播通知</span><span class="sxs-lookup"><span data-stu-id="77cc1-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77cc1-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="77cc1-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="77cc1-107">iOS</span><span class="sxs-lookup"><span data-stu-id="77cc1-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="77cc1-108">Android</span><span class="sxs-lookup"><span data-stu-id="77cc1-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="77cc1-109">概觀</span><span class="sxs-lookup"><span data-stu-id="77cc1-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="77cc1-110">toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="77cc1-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="77cc1-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77cc1-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="77cc1-112">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)。</span><span class="sxs-lookup"><span data-stu-id="77cc1-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="77cc1-113">在 Microsoft Azure 推播通知支援可讓您 tooaccess 容易使用、 多平台、 向外延展的推播訊息基礎結構，可大幅簡化 hello 實作針對消費者和企業應用程式的推播通知行動平台。</span><span class="sxs-lookup"><span data-stu-id="77cc1-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="77cc1-114">有時候 tooregulatory 或安全性條件約束，因為應用程式可能會想 tooinclude 中無法透過 hello 標準的推播通知基礎結構傳送的 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="77cc1-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="77cc1-115">本教學課程描述 tooachieve 如何透過 hello 用戶端的 Android 裝置與 hello 應用程式後端之間的安全、 已驗證連線的機密資訊傳送 hello 相同的體驗。</span><span class="sxs-lookup"><span data-stu-id="77cc1-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="77cc1-116">在高層級，hello 流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="77cc1-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="77cc1-117">hello 應用程式後端：</span><span class="sxs-lookup"><span data-stu-id="77cc1-117">hello app back-end:</span></span>
   * <span data-ttu-id="77cc1-118">在後端資料庫中儲存安全裝載。</span><span class="sxs-lookup"><span data-stu-id="77cc1-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="77cc1-119">會傳送 hello （傳送不安全的資訊） 此通知的 toohello Android 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="77cc1-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="77cc1-120">hello 在裝置上，當收到 hello 通知 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="77cc1-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="77cc1-121">hello Android 裝置會連絡 hello 後端要求 hello 安全內容。</span><span class="sxs-lookup"><span data-stu-id="77cc1-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="77cc1-122">hello 應用程式可以顯示 hello 裝載為 hello 裝置上的通知。</span><span class="sxs-lookup"><span data-stu-id="77cc1-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="77cc1-123">請務必 toonote hello 上述流程中 （並在本教學課程），我們會假設該 hello 裝置會儲存在本機儲存體，驗證語彙基元之後 hello 使用者登入。</span><span class="sxs-lookup"><span data-stu-id="77cc1-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="77cc1-124">這樣可保證完全完美無瑕的體驗，如 hello 裝置可以擷取 hello 通知安全裝載使用這個語彙基元。</span><span class="sxs-lookup"><span data-stu-id="77cc1-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="77cc1-125">如果您的應用程式不會儲存驗證語彙基元 hello 在裝置上，或可以過期這些語彙基元，hello 裝置的應用程式，在收到 hello 推播通知時應該會顯示提示 hello 使用者 toolaunch hello 應用程式的一般通知。</span><span class="sxs-lookup"><span data-stu-id="77cc1-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="77cc1-126">hello 應用程式然後驗證 hello 使用者，並顯示 hello 通知裝載。</span><span class="sxs-lookup"><span data-stu-id="77cc1-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="77cc1-127">本教學課程會示範如何安全 toosend 推播通知。</span><span class="sxs-lookup"><span data-stu-id="77cc1-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="77cc1-128">它是在 hello 基礎[通知使用者](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md)教學課程中，因此，您應該完成 hello 步驟在該教學課程中第一次如果尚未這麼做。</span><span class="sxs-lookup"><span data-stu-id="77cc1-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="77cc1-129">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="77cc1-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="77cc1-130">修改 hello Android 專案</span><span class="sxs-lookup"><span data-stu-id="77cc1-130">Modify hello Android project</span></span>
<span data-ttu-id="77cc1-131">既然您已修改您應用程式後端 toosend 只 hello*識別碼*的推播通知，您有 toochange 通知和回撥後端 tooretrieve hello 安全訊息 toobe 顯示您的 Android 應用程式 toohandle。</span><span class="sxs-lookup"><span data-stu-id="77cc1-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="77cc1-132">tooachieve 達成此目標，您必須確定您的 Android 應用程式知道 toomake 如何與後端收到 hello 推播通知時 tooauthenticate 本身。</span><span class="sxs-lookup"><span data-stu-id="77cc1-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="77cc1-133">我們現在將修改 hello*登入*流程在順序 toosave hello 驗證標頭值中的 hello 共用您的應用程式喜好設定。</span><span class="sxs-lookup"><span data-stu-id="77cc1-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="77cc1-134">類似的機制可以是使用的 toostore 任何 hello 應用程式的驗證權杖 （例如 OAuth 語彙基元） 會有 toouse，而不需要使用者認證。</span><span class="sxs-lookup"><span data-stu-id="77cc1-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="77cc1-135">在 Android 應用程式專案中，加入下列常數頂端的 hello hello hello **MainActivity**類別：</span><span class="sxs-lookup"><span data-stu-id="77cc1-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="77cc1-136">仍在 hello **MainActivity**類別，更新 hello`getAuthorizationHeader()`方法 toocontain hello 下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="77cc1-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="77cc1-137">新增下列 hello`import`在 hello hello 最上方的陳述式**MainActivity**檔案：</span><span class="sxs-lookup"><span data-stu-id="77cc1-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="77cc1-138">現在我們將會變更時收到 hello 通知時所呼叫的 hello 處理常式。</span><span class="sxs-lookup"><span data-stu-id="77cc1-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="77cc1-139">在 hello **MyHandler**類別變更 hello`OnReceive()`方法 toocontain:</span><span class="sxs-lookup"><span data-stu-id="77cc1-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="77cc1-140">然後新增 hello`retrieveNotification()`方法，取代 hello 預留位置`{back-end endpoint}`與部署您的後端時所取得的 hello 後端端點：</span><span class="sxs-lookup"><span data-stu-id="77cc1-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
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

<span data-ttu-id="77cc1-141">這個方法會呼叫您的應用程式後端 tooretrieve hello 通知內容使用儲存在 hello hello 認證共用喜好設定，並將它顯示為一般通知。</span><span class="sxs-lookup"><span data-stu-id="77cc1-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="77cc1-142">hello 通知會尋找 toohello 如同任何其他的推播通知的應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="77cc1-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="77cc1-143">請注意，它比 toohandle hello 情況下，缺少驗證標頭屬性或 hello 後端拒絕動作。</span><span class="sxs-lookup"><span data-stu-id="77cc1-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="77cc1-144">hello 特定處理這些情況通常取決於您目標的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="77cc1-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="77cc1-145">其中一個選項是 toodisplay hello 使用者 tooauthenticate tooretrieve hello 實際通知的一般提示字元之下一則通知。</span><span class="sxs-lookup"><span data-stu-id="77cc1-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="77cc1-146">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="77cc1-146">Run hello Application</span></span>
<span data-ttu-id="77cc1-147">toorun hello 應用程式中，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="77cc1-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="77cc1-148">確定 Azure 中已部署 **AppBackend** 。</span><span class="sxs-lookup"><span data-stu-id="77cc1-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="77cc1-149">如果使用 Visual Studio，請執行 hello **AppBackend** Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77cc1-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="77cc1-150">[ASP.NET Web] 頁面便會隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="77cc1-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="77cc1-151">在 Eclipse 中，實體的 Android 裝置或 hello 模擬器上執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77cc1-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="77cc1-152">在 hello Android 應用程式 UI 中，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="77cc1-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="77cc1-153">這些可以是任何字串，但它們必須 hello 相同的值。</span><span class="sxs-lookup"><span data-stu-id="77cc1-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="77cc1-154">在 hello Android 應用程式 UI，按一下 **登入**。</span><span class="sxs-lookup"><span data-stu-id="77cc1-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="77cc1-155">然後按一下 [傳送推播] 。</span><span class="sxs-lookup"><span data-stu-id="77cc1-155">Then click **Send push**.</span></span>

