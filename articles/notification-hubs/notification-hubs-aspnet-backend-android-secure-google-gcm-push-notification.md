---
title: "使用 Azure 通知中樞傳送安全的推播通知"
description: "了解如何從 Azure 將安全的推播通知傳送至 Android 應用程式。 程式碼範例是以 Java 及 C# 撰寫。"
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
ms.openlocfilehash: 29f8c516e611c13fb73c7edc15e7c52708c75bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="8442d-105">使用 Azure 通知中樞傳送安全的推播通知</span><span class="sxs-lookup"><span data-stu-id="8442d-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8442d-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="8442d-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="8442d-107">iOS</span><span class="sxs-lookup"><span data-stu-id="8442d-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="8442d-108">Android</span><span class="sxs-lookup"><span data-stu-id="8442d-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="8442d-109">Overview</span><span class="sxs-lookup"><span data-stu-id="8442d-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8442d-110">若要完成此教學課程，您必須具備有效的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8442d-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="8442d-111">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8442d-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8442d-112">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started)。</span><span class="sxs-lookup"><span data-stu-id="8442d-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="8442d-113">Microsoft Azure 中的推播通知支援可讓您存取易於使用、多重平台的大規模推播訊息基礎結構，因而可大幅簡化消費者和企業應用程式在行動平台上的推播通知實作。</span><span class="sxs-lookup"><span data-stu-id="8442d-113">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="8442d-114">基於法規或安全性限制，應用程式有時會想要在通知中加入無法透過標準推播通知基礎結構傳送的內容。</span><span class="sxs-lookup"><span data-stu-id="8442d-114">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="8442d-115">本教學課程說明如何透過用戶端 Android 裝置和應用程式後端之間的安全、已驗證連線來傳送敏感資訊，以達到相同體驗。</span><span class="sxs-lookup"><span data-stu-id="8442d-115">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client Android device and the app backend.</span></span>

<span data-ttu-id="8442d-116">概括而言，流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="8442d-116">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="8442d-117">應用程式後端：</span><span class="sxs-lookup"><span data-stu-id="8442d-117">The app back-end:</span></span>
   * <span data-ttu-id="8442d-118">在後端資料庫中儲存安全裝載。</span><span class="sxs-lookup"><span data-stu-id="8442d-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="8442d-119">將此通知的識別碼傳送至 Android 裝置 (不會傳送安全資訊)。</span><span class="sxs-lookup"><span data-stu-id="8442d-119">Sends the ID of this notification to the Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="8442d-120">收到通知時，裝置上的應用程式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="8442d-120">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="8442d-121">Android 裝置會連絡後端並要求安全裝載。</span><span class="sxs-lookup"><span data-stu-id="8442d-121">The Android device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="8442d-122">應用程式會以通知的形式在裝置上顯示裝載。</span><span class="sxs-lookup"><span data-stu-id="8442d-122">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="8442d-123">請務必注意在上述流程 (與本教學課程) 中，我們假設使用者登入後，裝置會將驗證權杖儲存在本機儲存體中。</span><span class="sxs-lookup"><span data-stu-id="8442d-123">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="8442d-124">由於裝置可使用此權杖擷取通知的安全裝載，因此可保證完全順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="8442d-124">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="8442d-125">如果您的應用程式沒有將驗證權杖儲存在裝置上，或如果這些權杖可能會過期，裝置應用程式應在收到推播通知時顯示一般通知，以提示使用者啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="8442d-125">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the push notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="8442d-126">應用程式會接著驗證使用者，並顯示通知裝載。</span><span class="sxs-lookup"><span data-stu-id="8442d-126">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="8442d-127">本教學課程示範如何傳送安全的推播通知。</span><span class="sxs-lookup"><span data-stu-id="8442d-127">This tutorial shows how to send secure push notifications.</span></span> <span data-ttu-id="8442d-128">本教學課程以 [通知使用者](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) 教學課程為基礎，如果您還未完成該教學課程中的步驟，請先完成。</span><span class="sxs-lookup"><span data-stu-id="8442d-128">It builds on the [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete the steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="8442d-129">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="8442d-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-android-project"></a><span data-ttu-id="8442d-130">修改 Android 專案</span><span class="sxs-lookup"><span data-stu-id="8442d-130">Modify the Android project</span></span>
<span data-ttu-id="8442d-131">現在您已將應用程式後端修改為只傳送推播通知的「識別碼」  ，就必須變更 Android 應用程式來處理該通知，並回呼後端以擷取要顯示的安全訊息。</span><span class="sxs-lookup"><span data-stu-id="8442d-131">Now that you modified your app back-end to send just the *id* of a push notification, you have to change your Android app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>
<span data-ttu-id="8442d-132">為了達成此目標，您必須確定您的 Android 應用程式知道在收到推播通知時，如何使用後端自我驗證。</span><span class="sxs-lookup"><span data-stu-id="8442d-132">To achieve this goal, you have to make sure that your Android app knows how to authenticate itself with your back-end when it receives the push notifications.</span></span>

<span data-ttu-id="8442d-133">為了將驗證標頭值儲存在您的應用程式共用喜好設定中，我們將修改 *login* 流程。</span><span class="sxs-lookup"><span data-stu-id="8442d-133">We will now modify the *login* flow in order to save the authentication header value in the shared preferences of your app.</span></span> <span data-ttu-id="8442d-134">類別機制可用來儲存任何驗證權杖 (例如 OAuth tokens)，應用程式在不需要使用者認證的情況下必須使用這些驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="8442d-134">Analogous mechanisms can be used to store any authentication token (e.g. OAuth tokens) that the app will have to use without requiring user credentials.</span></span>

1. <span data-ttu-id="8442d-135">在您的 Android 應用程式專案中，在 **MainActivity** 類別開頭處新增下列常數：</span><span class="sxs-lookup"><span data-stu-id="8442d-135">In your Android app project, add the following constants at the top of the **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="8442d-136">同樣地，在 **MainActivity** 類別中，更新 `getAuthorizationHeader()` 方法以包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8442d-136">Still in the **MainActivity** class, update the `getAuthorizationHeader()` method to contain the following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="8442d-137">在 **MainActivity** 檔案開頭處新增下列 `import` 陳述式：</span><span class="sxs-lookup"><span data-stu-id="8442d-137">Add the following `import` statements at the top of the **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="8442d-138">現在我們將變更收到通知時所呼叫的處理常式。</span><span class="sxs-lookup"><span data-stu-id="8442d-138">Now we will change the handler that is called when the notification is received.</span></span>

1. <span data-ttu-id="8442d-139">在 **MyHandler** 類別中，變更 `OnReceive()` 方法以包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8442d-139">In the **MyHandler** class change the `OnReceive()` method to contain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="8442d-140">然後新增 `retrieveNotification()` 方法，以部署後端時所取得的後端端點取代預留位置 `{back-end endpoint}`：</span><span class="sxs-lookup"><span data-stu-id="8442d-140">Then add the `retrieveNotification()` method, replacing the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                        Log.e("MainActivity", "Failed to retrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="8442d-141">本方法會呼叫應用程式後端，使用儲存在共用喜好設定中的認證來擷取通知內容，並以正常通知的方式顯示該通知。</span><span class="sxs-lookup"><span data-stu-id="8442d-141">This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="8442d-142">應用程式使用者所看到的通知會與任何其他推播通知沒有兩樣。</span><span class="sxs-lookup"><span data-stu-id="8442d-142">The notification looks to the app user exactly like any other push notification.</span></span>

<span data-ttu-id="8442d-143">請注意，比較理想的案例是處理遺失驗證標頭屬性或遭到後端拒絕的情況。</span><span class="sxs-lookup"><span data-stu-id="8442d-143">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="8442d-144">這些案例的特定處理絕大部分會依您的目標使用者經驗而定。</span><span class="sxs-lookup"><span data-stu-id="8442d-144">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="8442d-145">其中一個選項就是透過一般提示顯示通知，方便使用者進行驗證並擷取實際通知。</span><span class="sxs-lookup"><span data-stu-id="8442d-145">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="8442d-146">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="8442d-146">Run the Application</span></span>
<span data-ttu-id="8442d-147">若要執行應用程式，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="8442d-147">To run the application, do the following:</span></span>

1. <span data-ttu-id="8442d-148">確定 Azure 中已部署 **AppBackend** 。</span><span class="sxs-lookup"><span data-stu-id="8442d-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="8442d-149">如果使用 Visual Studio，則執行 **AppBackend** Web API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8442d-149">If using Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="8442d-150">[ASP.NET Web] 頁面便會隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="8442d-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="8442d-151">在 Eclipse 中，在實體 Android 裝置或模擬器上執行此應用程式。</span><span class="sxs-lookup"><span data-stu-id="8442d-151">In Eclipse, run the app on a physical Android device or the emulator.</span></span>
3. <span data-ttu-id="8442d-152">在 Android 應用程式 UI 中，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="8442d-152">In the Android app UI, enter a username and password.</span></span> <span data-ttu-id="8442d-153">這些可以是任何字串，但必須是相同值。</span><span class="sxs-lookup"><span data-stu-id="8442d-153">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="8442d-154">在 Android 應用程式 UI 中，按一下 [登入] 。</span><span class="sxs-lookup"><span data-stu-id="8442d-154">In the Android app UI, click **Log in**.</span></span> <span data-ttu-id="8442d-155">然後按一下 [傳送推播] 。</span><span class="sxs-lookup"><span data-stu-id="8442d-155">Then click **Send push**.</span></span>

