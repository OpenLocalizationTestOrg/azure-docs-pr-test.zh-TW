---
title: "推播通知中樞豐富 aaaAzure"
description: "了解如何 toosend 豐富的推播通知 tooan iOS 應用程式從 Azure。 程式碼範例是以 Objective-C 及 C# 撰寫。"
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a>Azure 通知中心豐富內容推播
## <a name="overview"></a>概觀
具有即時的豐富內容的順序 tooengage 使用者，在應用程式可能想 toopush 超出純文字。 這些通知可提高使用者互動，並呈現如 URL、音效、影像/優待券等內容。 本教學課程是 hello[通知使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)主題，並示範如何 toosend 推播通知加入裝載 （例如影像）。

本教學課程適用於 iOS 7 和 8。

  ![][IOS1]

概括而言：

1. hello 應用程式後端：
   * 存放區 hello 豐富的裝載 （在此情況下，影像） 在 hello 後端資料庫/本機儲存體
   * 傳送這個通知豐富 toohello 裝置識別碼
2. Hello 裝置上的應用程式：
   * 連絡人 hello 後端要求收到 hello 識別碼 hello 豐富型裝載
   * 傳送 hello 裝置上的使用者通知，當資料擷取已完成，而且只有在使用者點選 toolearn 詳細時立即顯示 hello 裝載

## <a name="webapi-project"></a>WebAPI 專案
1. 在 Visual Studio 中，開啟 hello **AppBackend** hello 中建立的專案[通知使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)教學課程。
2. 取得映像，toonotify 使用者，然後將它放入**img**專案目錄中的資料夾。
3. 按一下**顯示所有檔案**hello 中的 [方案總管] 中，按一下滑鼠右鍵 hello 資料夾太**包含在專案**。
4. 選取 hello 映像，以變更其屬性] 視窗中 [建置動作太**內嵌資源**。
   
    ![][IOS2]
5. 在**Notifications.cs**，新增 hello 下列 using 陳述式：
   
        using System.Reflection;
6. 更新 hello 整個**通知**以下列程式碼的 hello 的類別。 為確定 tooreplace hello 與您的通知中樞認證映像檔案名稱的預留位置。
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > （選擇性）參照太[如何使用 Visual C# tooembed 及存取資源](http://support.microsoft.com/kb/319292)如需有關如何 tooadd 並取得專案的資源。
   > 
   > 
7. 在**NotificationsController.cs**，重新定義**NotificationsController**以下列程式碼片段的 hello。 這會傳送初始無訊息的豐富通知識別碼 toodevice，並可讓用戶端擷取的映像：
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. 現在我們將會重新部署此應用程式 tooan Azure 網站順序 toomake 中的所有的裝置可以存取它。 以滑鼠右鍵按一下 hello **AppBackend**專案，然後選取**發行**。
9. 選取 Azure 網站作為您的發行目標。 登入您的 Azure 帳戶並選取現有或新網站，並記下 hello**目的地 URL**屬性在 hello**連接** 索引標籤。我們將 toothis URL 做為您*後端端點*稍後在本教學課程。 按一下 [發行] 。

## <a name="modify-hello-ios-project"></a>修改 hello iOS 專案
既然您已修改您應用程式後端 toosend 只 hello*識別碼*的通知，您將會變更您的 iOS 應用程式 toohandle 該識別碼，並從您的後端擷取 hello 豐富的訊息。

1. 開啟您的 iOS 專案，並依照移 tooyour 主應用程式目標 hello 啟用遠端通知**目標**> 一節。
2. 按一下**功能**，開啟**背景模式**，並檢查 hello**遠端通知**核取方塊。
   
    ![][IOS3]
3. 跳過**Main.storyboard**，並確定您有檢視控制器 (來參考 tooas 首頁檢視控制器在此教學課程) 從[通知使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)教學課程。
4. 新增**導覽控制站**tooyour 分鏡腳本，以及控制項拖放到它 hello tooHome 檢視控制器 toomake**根檢視**的巡覽。 請確定 hello**是初始檢視控制器**在屬性偵測器會選取只 hello 導覽控制站。
5. 新增**檢視控制器**toostoryboard 並加入**影像檢視**。 這是使用者會看到一旦他們選擇 toolearn hello notifiication 上的 更多的 hello 頁面。 您的腳本應如下所示：
   
    ![][IOS4]
6. 按一下 hello**首頁檢視控制器**在分鏡腳本，並確定它具有**homeViewController**做為其**自訂類別**和**分鏡腳本識別碼**下 hello 身分識別檢查。
7. 請勿 hello 相同映像檢視控制站指定為**imageViewController**。
8. 接著，建立名為的新檢視控制器類別**imageViewController** toohandle hello 您剛才建立的 UI。
9. 在**imageViewController.h**，新增下列 toohello 控制器的介面宣告的 hello。 請確定 toocontrol-拖曳從 hello 分鏡腳本映像檢視 toothese 屬性 toolink hello 兩個：
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. 在**imageViewController.m**，hello 結尾處新增 hello 下列**viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. 在**d**，匯入 hello 影像控制站所建立：
    
        #import "imageViewController.h"
12. 加入介面 > 一節以 hello 下列宣告：
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. 在 **AppDelegate** 中，確定您的應用程式已在 **application: didFinishLaunchingWithOptions** 中註冊無訊息通知：
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. 在下列實作 hello Subsitute**應用程式： didRegisterForRemoteNotificationsWithDeviceToken** tootake hello 分鏡腳本 UI 變更納入考量：
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. 然後，新增下列方法太的 hello**d** tooretrieve hello 映像從您的端點，並擷取完成時傳送本機的通知。 請確定 toosubstitute hello 預留位置`{backend endpoint}`與後端端點：
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. 藉由開啟中的 hello 映像檢視控制器處理 hello 本機通知上面**d**以 hello 下列方法：
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a>執行 hello 應用程式
1. 在 XCode 中，hello 應用程式實體 iOS 裝置上執行 (push 通知將無法運作 hello 模擬器中)。
2. 在 hello iOS 應用程式 UI 中輸入使用者名稱和密碼相同的驗證值，並按一下的 hello**登入**。
3. 按一下 [傳送推播]  ，您應該會看到一則應用程式內部警示。 如果您按一下**詳細**，您將會回到 toohello tooinclude 選擇您的應用程式後端中的映像。
4. 您也可以按一下**傳送推播**立即按 hello 裝置的 [首頁] 按鈕。 在幾分鐘的時間內，您就會收到推播通知。 如果您在其上點選或按一下 更多，您將會處於 tooyour 應用程式與 hello 豐富的映像內容。

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
