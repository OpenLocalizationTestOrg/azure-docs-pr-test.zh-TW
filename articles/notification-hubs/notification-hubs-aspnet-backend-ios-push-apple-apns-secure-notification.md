---
title: "Azure 通知中心安全推播"
description: "了解如何從 Azure 將安全的推播通知傳送至 iOS 應用程式。 程式碼範例是以 Objective-C 及 C# 撰寫。"
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="61483-104">Azure 通知中心安全推播</span><span class="sxs-lookup"><span data-stu-id="61483-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61483-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="61483-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="61483-106">iOS</span><span class="sxs-lookup"><span data-stu-id="61483-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="61483-107">Android</span><span class="sxs-lookup"><span data-stu-id="61483-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="61483-108">Overview</span><span class="sxs-lookup"><span data-stu-id="61483-108">Overview</span></span>
<span data-ttu-id="61483-109">Microsoft Azure 中的推播通知支援可讓您存取易於使用、多重平台的大規模推播基礎結構，因而可大幅簡化消費者和企業應用程式在行動平台上的推播通知實作。</span><span class="sxs-lookup"><span data-stu-id="61483-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="61483-110">基於法規或安全性限制，應用程式有時會想要在通知中加入無法透過標準推播通知基礎結構傳送的內容。</span><span class="sxs-lookup"><span data-stu-id="61483-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="61483-111">本教學課程說明如何透過用戶端裝置和應用程式後端之間的安全、已驗證連線來傳送敏感資訊，以達到相同體驗。</span><span class="sxs-lookup"><span data-stu-id="61483-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="61483-112">概括而言，流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="61483-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="61483-113">應用程式後端：</span><span class="sxs-lookup"><span data-stu-id="61483-113">The app back-end:</span></span>
   * <span data-ttu-id="61483-114">在後端資料庫中儲存安全裝載。</span><span class="sxs-lookup"><span data-stu-id="61483-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="61483-115">將此通知的識別碼傳送至裝置 (不會傳送安全資訊)。</span><span class="sxs-lookup"><span data-stu-id="61483-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="61483-116">收到通知時，裝置上的應用程式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="61483-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="61483-117">裝置會連絡後端並要求安全裝載。</span><span class="sxs-lookup"><span data-stu-id="61483-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="61483-118">應用程式會以通知的形式在裝置上顯示裝載。</span><span class="sxs-lookup"><span data-stu-id="61483-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="61483-119">請務必注意在上述流程 (與本教學課程) 中，我們假設使用者登入後，裝置會將驗證權杖儲存在本機儲存體中。</span><span class="sxs-lookup"><span data-stu-id="61483-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="61483-120">由於裝置可使用此權杖擷取通知的安全裝載，因此可保證完全順暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="61483-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="61483-121">如果您的應用程式沒有將驗證權杖儲存在裝置上，或如果這些權杖可能會過期，裝置應用程式應在收到通知時顯示一般通知，以提示使用者啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="61483-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="61483-122">應用程式會接著驗證使用者，並顯示通知裝載。</span><span class="sxs-lookup"><span data-stu-id="61483-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="61483-123">本安全推播教學課程說明如何以安全的方式傳送推播通知。</span><span class="sxs-lookup"><span data-stu-id="61483-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="61483-124">本教學課程會以 [通知使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) 教學課程為基礎，因此您應先完成該教學課程中的步驟。</span><span class="sxs-lookup"><span data-stu-id="61483-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="61483-125">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="61483-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="61483-126">修改 iOS 專案</span><span class="sxs-lookup"><span data-stu-id="61483-126">Modify the iOS project</span></span>
<span data-ttu-id="61483-127">現在，您已修改應用程式後端將只傳送通知的 *id* ，您必須變更 iOS 應用程式來處理該通知，並回呼後端以擷取要顯示的安全訊息。</span><span class="sxs-lookup"><span data-stu-id="61483-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="61483-128">若要達到此目標，我們必須撰寫可從應用程式後端擷取安全內容的邏輯。</span><span class="sxs-lookup"><span data-stu-id="61483-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="61483-129">在 **AppDelegate.m**中，請確定應用程式已註冊無訊息通知，以便處理從後端傳送出來的通知識別碼。</span><span class="sxs-lookup"><span data-stu-id="61483-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="61483-130">在 didFinishLaunchingWithOptions 中新增 **UIRemoteNotificationTypeNewsstandContentAvailability** 選項：</span><span class="sxs-lookup"><span data-stu-id="61483-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="61483-131">在 **AppDelegate.m** 的開頭處，新增包含下列宣告的實作區段：</span><span class="sxs-lookup"><span data-stu-id="61483-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="61483-132">然後在實作區段中新增下列程式碼，並以先前為後端取得的端點取代預留位置 `{back-end endpoint}` ：</span><span class="sxs-lookup"><span data-stu-id="61483-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="61483-133">現在，我們必須處理內送通知，並使用上述方法擷取要顯示的內容。</span><span class="sxs-lookup"><span data-stu-id="61483-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="61483-134">首先，我們必須啟用您的 iOS 應用程式，可在接收推播通知時於背景中執行。</span><span class="sxs-lookup"><span data-stu-id="61483-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="61483-135">在 **XCode** 中，在左側面板中選取您的應用程式專案，然後在中央窗格的 [目標] 區段中，按一下您的主要應用程式目標。</span><span class="sxs-lookup"><span data-stu-id="61483-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="61483-136">接著按一下中央窗格頂端的 [功能] 索引標籤，並核取 [遠端通知] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="61483-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="61483-137">在 **AppDelegate.m** 中，新增下列可處理推播通知的方法：</span><span class="sxs-lookup"><span data-stu-id="61483-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    <span data-ttu-id="61483-138">請注意，比較理想的案例是處理遺失驗證標頭屬性或遭到後端拒絕的情況。</span><span class="sxs-lookup"><span data-stu-id="61483-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="61483-139">這些案例的特定處理絕大部分會依您的目標使用者經驗而定。</span><span class="sxs-lookup"><span data-stu-id="61483-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="61483-140">其中一個選項就是透過一般提示顯示通知，方便使用者進行驗證並擷取實際通知。</span><span class="sxs-lookup"><span data-stu-id="61483-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="61483-141">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="61483-141">Run the Application</span></span>
<span data-ttu-id="61483-142">若要執行應用程式，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="61483-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="61483-143">在 XCode 中，在實體 iOS 裝置上執行應用程式 (推播通知無法在模擬器中運作)。</span><span class="sxs-lookup"><span data-stu-id="61483-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="61483-144">在 iOS 應用程式 UI 中，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="61483-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="61483-145">這些可以是任何字串，但必須是相同值。</span><span class="sxs-lookup"><span data-stu-id="61483-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="61483-146">在 iOS 應用程式 UI 中，按一下 [登入] 。</span><span class="sxs-lookup"><span data-stu-id="61483-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="61483-147">然後按一下 [傳送推播] 。</span><span class="sxs-lookup"><span data-stu-id="61483-147">Then click **Send push**.</span></span> <span data-ttu-id="61483-148">您應該會在您的通知中心內看見安全通知。</span><span class="sxs-lookup"><span data-stu-id="61483-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
