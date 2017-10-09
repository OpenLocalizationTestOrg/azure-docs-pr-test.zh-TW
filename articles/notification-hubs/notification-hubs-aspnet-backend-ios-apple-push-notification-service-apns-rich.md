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
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="85dfb-104">Azure 通知中心豐富內容推播</span><span class="sxs-lookup"><span data-stu-id="85dfb-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="85dfb-105">概觀</span><span class="sxs-lookup"><span data-stu-id="85dfb-105">Overview</span></span>
<span data-ttu-id="85dfb-106">具有即時的豐富內容的順序 tooengage 使用者，在應用程式可能想 toopush 超出純文字。</span><span class="sxs-lookup"><span data-stu-id="85dfb-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="85dfb-107">這些通知可提高使用者互動，並呈現如 URL、音效、影像/優待券等內容。</span><span class="sxs-lookup"><span data-stu-id="85dfb-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="85dfb-108">本教學課程是 hello[通知使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)主題，並示範如何 toosend 推播通知加入裝載 （例如影像）。</span><span class="sxs-lookup"><span data-stu-id="85dfb-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="85dfb-109">本教學課程適用於 iOS 7 和 8。</span><span class="sxs-lookup"><span data-stu-id="85dfb-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="85dfb-110">概括而言：</span><span class="sxs-lookup"><span data-stu-id="85dfb-110">At a high level:</span></span>

1. <span data-ttu-id="85dfb-111">hello 應用程式後端：</span><span class="sxs-lookup"><span data-stu-id="85dfb-111">hello app backend:</span></span>
   * <span data-ttu-id="85dfb-112">存放區 hello 豐富的裝載 （在此情況下，影像） 在 hello 後端資料庫/本機儲存體</span><span class="sxs-lookup"><span data-stu-id="85dfb-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="85dfb-113">傳送這個通知豐富 toohello 裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="85dfb-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="85dfb-114">Hello 裝置上的應用程式：</span><span class="sxs-lookup"><span data-stu-id="85dfb-114">App on hello device:</span></span>
   * <span data-ttu-id="85dfb-115">連絡人 hello 後端要求收到 hello 識別碼 hello 豐富型裝載</span><span class="sxs-lookup"><span data-stu-id="85dfb-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="85dfb-116">傳送 hello 裝置上的使用者通知，當資料擷取已完成，而且只有在使用者點選 toolearn 詳細時立即顯示 hello 裝載</span><span class="sxs-lookup"><span data-stu-id="85dfb-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="85dfb-117">WebAPI 專案</span><span class="sxs-lookup"><span data-stu-id="85dfb-117">WebAPI Project</span></span>
1. <span data-ttu-id="85dfb-118">在 Visual Studio 中，開啟 hello **AppBackend** hello 中建立的專案[通知使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="85dfb-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="85dfb-119">取得映像，toonotify 使用者，然後將它放入**img**專案目錄中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="85dfb-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="85dfb-120">按一下**顯示所有檔案**hello 中的 [方案總管] 中，按一下滑鼠右鍵 hello 資料夾太**包含在專案**。</span><span class="sxs-lookup"><span data-stu-id="85dfb-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="85dfb-121">選取 hello 映像，以變更其屬性] 視窗中 [建置動作太**內嵌資源**。</span><span class="sxs-lookup"><span data-stu-id="85dfb-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="85dfb-122">在**Notifications.cs**，新增 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="85dfb-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="85dfb-123">更新 hello 整個**通知**以下列程式碼的 hello 的類別。</span><span class="sxs-lookup"><span data-stu-id="85dfb-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="85dfb-124">為確定 tooreplace hello 與您的通知中樞認證映像檔案名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="85dfb-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
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
   > <span data-ttu-id="85dfb-125">（選擇性）參照太[如何使用 Visual C# tooembed 及存取資源](http://support.microsoft.com/kb/319292)如需有關如何 tooadd 並取得專案的資源。</span><span class="sxs-lookup"><span data-stu-id="85dfb-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="85dfb-126">在**NotificationsController.cs**，重新定義**NotificationsController**以下列程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="85dfb-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="85dfb-127">這會傳送初始無訊息的豐富通知識別碼 toodevice，並可讓用戶端擷取的映像：</span><span class="sxs-lookup"><span data-stu-id="85dfb-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
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
8. <span data-ttu-id="85dfb-128">現在我們將會重新部署此應用程式 tooan Azure 網站順序 toomake 中的所有的裝置可以存取它。</span><span class="sxs-lookup"><span data-stu-id="85dfb-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="85dfb-129">以滑鼠右鍵按一下 hello **AppBackend**專案，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="85dfb-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="85dfb-130">選取 Azure 網站作為您的發行目標。</span><span class="sxs-lookup"><span data-stu-id="85dfb-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="85dfb-131">登入您的 Azure 帳戶並選取現有或新網站，並記下 hello**目的地 URL**屬性在 hello**連接** 索引標籤。我們將 toothis URL 做為您*後端端點*稍後在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="85dfb-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="85dfb-132">按一下 [發行] 。</span><span class="sxs-lookup"><span data-stu-id="85dfb-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="85dfb-133">修改 hello iOS 專案</span><span class="sxs-lookup"><span data-stu-id="85dfb-133">Modify hello iOS project</span></span>
<span data-ttu-id="85dfb-134">既然您已修改您應用程式後端 toosend 只 hello*識別碼*的通知，您將會變更您的 iOS 應用程式 toohandle 該識別碼，並從您的後端擷取 hello 豐富的訊息。</span><span class="sxs-lookup"><span data-stu-id="85dfb-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="85dfb-135">開啟您的 iOS 專案，並依照移 tooyour 主應用程式目標 hello 啟用遠端通知**目標**> 一節。</span><span class="sxs-lookup"><span data-stu-id="85dfb-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="85dfb-136">按一下**功能**，開啟**背景模式**，並檢查 hello**遠端通知**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="85dfb-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="85dfb-137">跳過**Main.storyboard**，並確定您有檢視控制器 (來參考 tooas 首頁檢視控制器在此教學課程) 從[通知使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="85dfb-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="85dfb-138">新增**導覽控制站**tooyour 分鏡腳本，以及控制項拖放到它 hello tooHome 檢視控制器 toomake**根檢視**的巡覽。</span><span class="sxs-lookup"><span data-stu-id="85dfb-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="85dfb-139">請確定 hello**是初始檢視控制器**在屬性偵測器會選取只 hello 導覽控制站。</span><span class="sxs-lookup"><span data-stu-id="85dfb-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="85dfb-140">新增**檢視控制器**toostoryboard 並加入**影像檢視**。</span><span class="sxs-lookup"><span data-stu-id="85dfb-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="85dfb-141">這是使用者會看到一旦他們選擇 toolearn hello notifiication 上的 更多的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="85dfb-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="85dfb-142">您的腳本應如下所示：</span><span class="sxs-lookup"><span data-stu-id="85dfb-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="85dfb-143">按一下 hello**首頁檢視控制器**在分鏡腳本，並確定它具有**homeViewController**做為其**自訂類別**和**分鏡腳本識別碼**下 hello 身分識別檢查。</span><span class="sxs-lookup"><span data-stu-id="85dfb-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="85dfb-144">請勿 hello 相同映像檢視控制站指定為**imageViewController**。</span><span class="sxs-lookup"><span data-stu-id="85dfb-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="85dfb-145">接著，建立名為的新檢視控制器類別**imageViewController** toohandle hello 您剛才建立的 UI。</span><span class="sxs-lookup"><span data-stu-id="85dfb-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="85dfb-146">在**imageViewController.h**，新增下列 toohello 控制器的介面宣告的 hello。</span><span class="sxs-lookup"><span data-stu-id="85dfb-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="85dfb-147">請確定 toocontrol-拖曳從 hello 分鏡腳本映像檢視 toothese 屬性 toolink hello 兩個：</span><span class="sxs-lookup"><span data-stu-id="85dfb-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="85dfb-148">在**imageViewController.m**，hello 結尾處新增 hello 下列**viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="85dfb-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="85dfb-149">在**d**，匯入 hello 影像控制站所建立：</span><span class="sxs-lookup"><span data-stu-id="85dfb-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="85dfb-150">加入介面 > 一節以 hello 下列宣告：</span><span class="sxs-lookup"><span data-stu-id="85dfb-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="85dfb-151">在 **AppDelegate** 中，確定您的應用程式已在 **application: didFinishLaunchingWithOptions** 中註冊無訊息通知：</span><span class="sxs-lookup"><span data-stu-id="85dfb-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="85dfb-152">在下列實作 hello Subsitute**應用程式： didRegisterForRemoteNotificationsWithDeviceToken** tootake hello 分鏡腳本 UI 變更納入考量：</span><span class="sxs-lookup"><span data-stu-id="85dfb-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="85dfb-153">然後，新增下列方法太的 hello**d** tooretrieve hello 映像從您的端點，並擷取完成時傳送本機的通知。</span><span class="sxs-lookup"><span data-stu-id="85dfb-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="85dfb-154">請確定 toosubstitute hello 預留位置`{backend endpoint}`與後端端點：</span><span class="sxs-lookup"><span data-stu-id="85dfb-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
3. <span data-ttu-id="85dfb-155">藉由開啟中的 hello 映像檢視控制器處理 hello 本機通知上面**d**以 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="85dfb-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
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

## <a name="run-hello-application"></a><span data-ttu-id="85dfb-156">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="85dfb-156">Run hello Application</span></span>
1. <span data-ttu-id="85dfb-157">在 XCode 中，hello 應用程式實體 iOS 裝置上執行 (push 通知將無法運作 hello 模擬器中)。</span><span class="sxs-lookup"><span data-stu-id="85dfb-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="85dfb-158">在 hello iOS 應用程式 UI 中輸入使用者名稱和密碼相同的驗證值，並按一下的 hello**登入**。</span><span class="sxs-lookup"><span data-stu-id="85dfb-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="85dfb-159">按一下 [傳送推播]  ，您應該會看到一則應用程式內部警示。</span><span class="sxs-lookup"><span data-stu-id="85dfb-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="85dfb-160">如果您按一下**詳細**，您將會回到 toohello tooinclude 選擇您的應用程式後端中的映像。</span><span class="sxs-lookup"><span data-stu-id="85dfb-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="85dfb-161">您也可以按一下**傳送推播**立即按 hello 裝置的 [首頁] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="85dfb-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="85dfb-162">在幾分鐘的時間內，您就會收到推播通知。</span><span class="sxs-lookup"><span data-stu-id="85dfb-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="85dfb-163">如果您在其上點選或按一下 更多，您將會處於 tooyour 應用程式與 hello 豐富的映像內容。</span><span class="sxs-lookup"><span data-stu-id="85dfb-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
