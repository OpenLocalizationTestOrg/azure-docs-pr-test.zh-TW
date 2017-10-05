---
title: "使用 Web API 註冊目前使用者以取得推播通知 | Microsoft Docs"
description: "了解如何在 ASP.NET Web API 執行註冊時，在 iOS 應用程式中向 Azure 通知中樞要求推播通知註冊。"
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: fd56bb2dd627b31f00363851a4e76484aa382988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="register-the-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="1ddda-103">使用 ASP.NET 來註冊目前使用者以取得推播通知</span><span class="sxs-lookup"><span data-stu-id="1ddda-103">Register the current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ddda-104">iOS</span><span class="sxs-lookup"><span data-stu-id="1ddda-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="1ddda-105">概觀</span><span class="sxs-lookup"><span data-stu-id="1ddda-105">Overview</span></span>
<span data-ttu-id="1ddda-106">本主題將說明以 ASP.NET Web API 執行註冊時，應如何向 Azure 通知中心要求推播通知註冊。</span><span class="sxs-lookup"><span data-stu-id="1ddda-106">This topic shows you how to request push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="1ddda-107">這是 [使用通知中樞來通知使用者]教學課程的延伸主題。</span><span class="sxs-lookup"><span data-stu-id="1ddda-107">This topic extends the tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="1ddda-108">您必須已完成該教學課程中的必要步驟，才能建立已驗證的行動服務。</span><span class="sxs-lookup"><span data-stu-id="1ddda-108">You must have already completed the required steps in that tutorial to create the authenticated mobile service.</span></span> <span data-ttu-id="1ddda-109">如需通知使用者案例的詳細資訊，請參閱 [使用通知中樞來通知使用者]。</span><span class="sxs-lookup"><span data-stu-id="1ddda-109">For more information on the notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="1ddda-110">更新應用程式</span><span class="sxs-lookup"><span data-stu-id="1ddda-110">Update your app</span></span>
1. <span data-ttu-id="1ddda-111">在您的 MainStoryboard_iPhone.storyboard 中，從物件程式庫新增下列元件：</span><span class="sxs-lookup"><span data-stu-id="1ddda-111">In your MainStoryboard_iPhone.storyboard, add the following components from the object library:</span></span>
   
   * <span data-ttu-id="1ddda-112">**標籤**：「使用通知中樞推播給使用者」</span><span class="sxs-lookup"><span data-stu-id="1ddda-112">**Label**: "Push to User with Notification Hubs"</span></span>
   * <span data-ttu-id="1ddda-113">**標籤**：「安裝 ID」</span><span class="sxs-lookup"><span data-stu-id="1ddda-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="1ddda-114">**標籤**：「使用者」</span><span class="sxs-lookup"><span data-stu-id="1ddda-114">**Label**: "User"</span></span>
   * <span data-ttu-id="1ddda-115">**文字欄位**：「使用者」</span><span class="sxs-lookup"><span data-stu-id="1ddda-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="1ddda-116">**標籤**：「密碼」</span><span class="sxs-lookup"><span data-stu-id="1ddda-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="1ddda-117">**文字欄位**：「密碼」</span><span class="sxs-lookup"><span data-stu-id="1ddda-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="1ddda-118">**按鈕**：「登入」</span><span class="sxs-lookup"><span data-stu-id="1ddda-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="1ddda-119">此時，您的腳本如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ddda-119">At this point, your storyboard looks like the following:</span></span>
     
      ![][0]
2. <span data-ttu-id="1ddda-120">在輔助編輯器中，為所有切換的控制項建立出口並加以呼叫、使用檢視控制器 (委派) 連接文字欄位，然後為 [登入] 按鈕建立 [動作]。</span><span class="sxs-lookup"><span data-stu-id="1ddda-120">In the assistant editor, create outlets for all the switched controls and call them, connect the text fields with the View Controller (delegate), and create an **Action** for the **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain the following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="1ddda-121">建立名為 **DeviceInfo**的類別，然後將下列程式碼複製到 DeviceInfo.h 檔案的介面區段中：</span><span class="sxs-lookup"><span data-stu-id="1ddda-121">Create a class named **DeviceInfo**, and copy the following code into the interface section of the file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="1ddda-122">在 DeviceInfo.m 檔案的實作區段中複製下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="1ddda-122">Copy the following code in the implementation section of the DeviceInfo.m file:</span></span>
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store the install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. <span data-ttu-id="1ddda-123">在 PushToUserAppDelegate.h 中，新增下列屬性 singleton：</span><span class="sxs-lookup"><span data-stu-id="1ddda-123">In PushToUserAppDelegate.h, add the following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="1ddda-124">在 PushToUserAppDelegate.m 的 **didFinishLaunchingWithOptions** 方法中，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="1ddda-124">In the **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add the following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="1ddda-125">第一行會初始化 **DeviceInfo** singleton。</span><span class="sxs-lookup"><span data-stu-id="1ddda-125">The first line initializes the **DeviceInfo** singleton.</span></span> <span data-ttu-id="1ddda-126">第二行會啟動推播通知的註冊；如果您已完成 [開始使用通知中心] 教學課程，則會有此註冊存在。</span><span class="sxs-lookup"><span data-stu-id="1ddda-126">The second line starts the registration for push notifications, which is already present is you have already completed the [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="1ddda-127">在 PushToUserAppDelegate.m 中，在您的 AppDelegate 中實作 **didRegisterForRemoteNotificationsWithDeviceToken** 方法，並新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="1ddda-127">In PushToUserAppDelegate.m, implement the method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add the following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="1ddda-128">這會設定要求的裝置權杖。</span><span class="sxs-lookup"><span data-stu-id="1ddda-128">This sets the device token for the request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1ddda-129">此時，此方法中不應有任何其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="1ddda-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="1ddda-130">如果您已呼叫您在完成 **開始使用通知中樞** 教學課程時所新增的 [registerNativeWithDeviceToken](/manage/services/notification-hubs/get-started-notification-hubs-ios/) 方法，您必須註解化或移除該呼叫。</span><span class="sxs-lookup"><span data-stu-id="1ddda-130">If you already have a call to the **registerNativeWithDeviceToken** method that was added when you completed the [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="1ddda-131">在 PushToUserAppDelegate.m 檔案中，新增下列處理常式方法：</span><span class="sxs-lookup"><span data-stu-id="1ddda-131">In the PushToUserAppDelegate.m file, add the following handler method:</span></span>
   
   * <span data-ttu-id="1ddda-132">(void) 的應用程式:(UIApplication *) 應用程式 didReceiveRemoteNotification:(NSDictionary *) 避 {NSLog (@"%@"，所以);  UIAlertView * 警示 = [[UIAlertView 配置] initWithTitle:@"Notification 」 訊息: [使用者資訊 objectForKey:@"inAppMessage]"委派： nil cancelButtonTitle: @"OK"otherButtonTitles:nil、 nil];  [警示顯示]。}</span><span class="sxs-lookup"><span data-stu-id="1ddda-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="1ddda-133">此方法會在您執行中的應用程式接收到通知時，在 UI 中顯示警示。</span><span class="sxs-lookup"><span data-stu-id="1ddda-133">This method displays an alert in the UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="1ddda-134">開啟 PushToUserViewController.m 檔案，然後在下列實作中傳回鍵盤：</span><span class="sxs-lookup"><span data-stu-id="1ddda-134">Open the PushToUserViewController.m file, and return the keyboard in the following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="1ddda-135">在 PushToUserViewController.m 檔案的 **viewDidLoad** 方法中，初始化安裝 ID 標籤，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1ddda-135">In the **viewDidLoad** method in the PushToUserViewController.m file, initialize the installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="1ddda-136">在 PushToUserViewController.m 的介面中新增下列屬性：</span><span class="sxs-lookup"><span data-stu-id="1ddda-136">Add the following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="1ddda-137">然後，新增下列實作：</span><span class="sxs-lookup"><span data-stu-id="1ddda-137">Then, add the following implementation:</span></span>
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. <span data-ttu-id="1ddda-138">將下列程式碼複製到 XCode 所建立的 **login** 處理常式方法中：</span><span class="sxs-lookup"><span data-stu-id="1ddda-138">Copy the following code into the **login** handler method created by XCode:</span></span>
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    <span data-ttu-id="1ddda-139">This method gets both an installation ID and channel for push notifications and sends it, along with the device type, to the authenticated Web API method that creates a registration in Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="1ddda-139">This method gets both an installation ID and channel for push notifications and sends it, along with the device type, to the authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="1ddda-140">此 Web API 定義於[使用通知中樞來通知使用者]中。</span><span class="sxs-lookup"><span data-stu-id="1ddda-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="1ddda-141">現在，用戶端應用程式已更新，請回到 [使用通知中樞來通知使用者] ，並更新行動服務，以使用通知中心傳送通知。</span><span class="sxs-lookup"><span data-stu-id="1ddda-141">Now that the client app has been updated, return to the [Notify users with Notification Hubs] and update the mobile service to send notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
<span data-ttu-id="1ddda-142">[使用通知中樞來通知使用者]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="1ddda-142">[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet</span></span>

<span data-ttu-id="1ddda-143">[開始使用通知中心]: /manage/services/notification-hubs/get-started-notification-hubs-ios</span><span class="sxs-lookup"><span data-stu-id="1ddda-143">[Get Started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios</span></span>
