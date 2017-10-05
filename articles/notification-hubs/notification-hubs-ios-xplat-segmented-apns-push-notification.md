---
title: "通知中樞重大消息教學課程 - iOS"
description: "了解如何使用 Azure 服務匯流排通知中樞將本地化重大新聞通知傳送至 iOS 裝置。"
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: dc47250db6fb3a2853dae24e02bda236154d93fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="795f7-103">使用通知中心傳送即時新聞</span><span class="sxs-lookup"><span data-stu-id="795f7-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="795f7-104">Overview</span><span class="sxs-lookup"><span data-stu-id="795f7-104">Overview</span></span>
<span data-ttu-id="795f7-105">本主題將說明如何使用 Azure 通知中心，將即時新聞通知廣播至 iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="795f7-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an iOS app.</span></span> <span data-ttu-id="795f7-106">完成時，您便能夠註冊您所感興趣的即時新聞類別，並僅接收這些類別的推播通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="795f7-107">此情況是許多應用程式的共同模式，這些應用程式必須將通知傳送給先前宣告對通知有興趣的使用者群組，例如，RSS 閱讀程式、供樂迷使用的應用程式等等。</span><span class="sxs-lookup"><span data-stu-id="795f7-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="795f7-108">在通知中樞內建立註冊時，您可以透過包含一或多個 *tags* 來啟用廣播案例。</span><span class="sxs-lookup"><span data-stu-id="795f7-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="795f7-109">當標籤收到通知時，所有已註冊此標籤的裝置都會收到通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="795f7-110">由於標籤只是簡單的字串而已，您無需預先佈建標籤。</span><span class="sxs-lookup"><span data-stu-id="795f7-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="795f7-111">如需標籤的詳細資訊，請參閱 [通知中樞路由與標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="795f7-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="795f7-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="795f7-112">Prerequisites</span></span>
<span data-ttu-id="795f7-113">本主題會以您在[開始使用通知中樞][get-started]中所建立的應用程式為基礎。</span><span class="sxs-lookup"><span data-stu-id="795f7-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="795f7-114">開始本教學課程之前，您必須已完成[開始使用通知中樞][get-started]。</span><span class="sxs-lookup"><span data-stu-id="795f7-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="795f7-115">在應用程式中新增類別選項</span><span class="sxs-lookup"><span data-stu-id="795f7-115">Add category selection to the app</span></span>
<span data-ttu-id="795f7-116">第一個步驟是在您現有的腳本上新增 UI 元素，以便使用者選取要註冊的類別。</span><span class="sxs-lookup"><span data-stu-id="795f7-116">The first step is to add the UI elements to your existing storyboard that enable the user to select categories to register.</span></span> <span data-ttu-id="795f7-117">使用者所選取的類別會儲存在裝置上。</span><span class="sxs-lookup"><span data-stu-id="795f7-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="795f7-118">啟動應用程式時，您的通知中心內會建立以所選取類別作為標籤的裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="795f7-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="795f7-119">在您的 MainStoryboard_iPhone.storyboard 中，從物件程式庫新增下列元件：</span><span class="sxs-lookup"><span data-stu-id="795f7-119">In your MainStoryboard_iPhone.storyboard add the following components from the object library:</span></span>
   
   * <span data-ttu-id="795f7-120">具有「即時新聞」文字的標籤，</span><span class="sxs-lookup"><span data-stu-id="795f7-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="795f7-121">具有「世界」、「政治」、「商業」、「技術」、「科學」、「體育」等類別文字的標籤，</span><span class="sxs-lookup"><span data-stu-id="795f7-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="795f7-122">六個參數 (一個類別一個)，預設會將每個參數 [狀態] 設為 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="795f7-122">Six switches, one per category, set each switch **State** to be **Off** by default.</span></span>
   * <span data-ttu-id="795f7-123">一個標示為「訂閱」的按鈕</span><span class="sxs-lookup"><span data-stu-id="795f7-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="795f7-124">您的腳本應如下所示：</span><span class="sxs-lookup"><span data-stu-id="795f7-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="795f7-125">在輔助編輯器中，建立所有參數的出口，並將其命名為 "WorldSwitch"、"PoliticsSwitch"、"BusinessSwitch"、"TechnologySwitch"、"ScienceSwitch"、"SportsSwitch"</span><span class="sxs-lookup"><span data-stu-id="795f7-125">In the assistant editor, create outlets for all the switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="795f7-126">為名為「訂閱」的按鈕建立「動作」。</span><span class="sxs-lookup"><span data-stu-id="795f7-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="795f7-127">您的 ViewController.h 應該包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="795f7-127">Your ViewController.h should contain the following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="795f7-128">建立稱為 `Notifications` 的新 **Cocoa Touch 類別**。</span><span class="sxs-lookup"><span data-stu-id="795f7-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="795f7-129">在 Notifications.h 的介面區段中複製下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="795f7-129">Copy the following code in the interface section of the file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="795f7-130">在 Notifications.m 中新增下列 import 指示詞：</span><span class="sxs-lookup"><span data-stu-id="795f7-130">Add the following import directive to Notifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="795f7-131">複製 Notifications.m 檔案實作區段中的下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="795f7-131">Copy the following code in the implementation section of the file Notifications.m.</span></span>
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    <span data-ttu-id="795f7-132">此類別會使用本機儲存體來儲存和擷取此裝置將接收的新聞類別。</span><span class="sxs-lookup"><span data-stu-id="795f7-132">This class uses local storage to store and retrieve the categories of news that this device will receive.</span></span> <span data-ttu-id="795f7-133">此外，它也包含使用 [範本](notification-hubs-templates-cross-platform-push-messages.md) 註冊來註冊這些類別的方法。</span><span class="sxs-lookup"><span data-stu-id="795f7-133">Also, it contains a method to register for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="795f7-134">在 AppDelegate.h 檔案中，新增 Notifications.h 的匯入陳述式，並新增 Notifications 類別執行個體的屬性：</span><span class="sxs-lookup"><span data-stu-id="795f7-134">In the AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of the Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="795f7-135">在 AppDelegate.m 的 **didFinishLaunchingWithOptions** 方法中，於方法的開頭處加入程式碼來初始化通知執行個體。</span><span class="sxs-lookup"><span data-stu-id="795f7-135">In the **didFinishLaunchingWithOptions** method in AppDelegate.m, add the code to initialize the notifications instance at the beginning of the method.</span></span>  
   
    <span data-ttu-id="795f7-136">`HUBNAME` 與 `HUBLISTENACCESS` (定義於 hubinfo.h 中) 的 `<hub name>` 及 `<connection string with listen access>` 預留位置，應已用稍早取得之 *DefaultListenSharedAccessSignature* 的通知中樞名稱與連接字串所取代。</span><span class="sxs-lookup"><span data-stu-id="795f7-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have the `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="795f7-137">因為隨用戶端應用程式散佈的憑證通常不安全，您應只將接聽存取權的金鑰隨用戶端應用程式散佈。</span><span class="sxs-lookup"><span data-stu-id="795f7-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="795f7-138">您的應用程式可透過接聽存取權來註冊通知，但無法修改現有的註冊或無法傳送通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-138">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="795f7-139">在安全的後端服務中，會使用完整存取金鑰來傳送通知和變更現有的註冊。</span><span class="sxs-lookup"><span data-stu-id="795f7-139">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="795f7-140">在 AppDelegate.m 的 **didRegisterForRemoteNotificationsWithDeviceToken** 方法中，使用下列程式碼來取代方法中的程式碼，以將裝置權杖傳遞給 notifications 類別。</span><span class="sxs-lookup"><span data-stu-id="795f7-140">In the **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace the code in the method with the following code to pass the device token to the notifications class.</span></span> <span data-ttu-id="795f7-141">Notifications 類別將會執行使用類別註冊通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-141">The notifications class will perform the registering for notifications with the categories.</span></span> <span data-ttu-id="795f7-142">如果使用者變更類別選取項目，我們會呼叫 `subscribeWithCategories` 方法以回應 [訂閱] 按鈕來進行更新。</span><span class="sxs-lookup"><span data-stu-id="795f7-142">If the user changes category selections, we call the `subscribeWithCategories` method in response to the **subscribe** button to update them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="795f7-143">由於 Apple 推播通知服務 (APNS) 所指派的裝置權杖可能隨時會變更，因此您應經常註冊通知以避免通知失敗。</span><span class="sxs-lookup"><span data-stu-id="795f7-143">Because the device token assigned by the Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="795f7-144">此範例會在應用程式每次啟動時註冊通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-144">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="795f7-145">若是經常執行 (一天多次) 的應用程式，如果距離上次註冊的時間不到一天，則您可能可以略過註冊以保留頻寬。</span><span class="sxs-lookup"><span data-stu-id="795f7-145">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="795f7-146">請注意， **didRegisterForRemoteNotificationsWithDeviceToken** 方法中此時不應有其他程式碼。</span><span class="sxs-lookup"><span data-stu-id="795f7-146">Note that at this point there should be no other code in the **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="795f7-147">下列方法應該已經存在於 d 無法完成[開始使用通知中樞][ get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="795f7-147">The following methods should already be present in AppDelegate.m from completing the [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="795f7-148">否則，請予以新增。</span><span class="sxs-lookup"><span data-stu-id="795f7-148">If not, add them.</span></span>
   
    <span data-ttu-id="795f7-149">-(void) MessageBox:(NSString *) 標題訊息:(NSString *) messageText {</span><span class="sxs-lookup"><span data-stu-id="795f7-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="795f7-150">}</span><span class="sxs-lookup"><span data-stu-id="795f7-150">}</span></span>
   
   * <span data-ttu-id="795f7-151">(void) 的應用程式:(UIApplication *) 應用程式 didReceiveRemoteNotification: (NSDictionary *) 使用者資訊 {NSLog (@"%@"，所以);  [自我 MessageBox:@"Notification 」 的訊息: [[使用者資訊 objectForKey:@"aps]"valueForKey:@"alert"]]。}</span><span class="sxs-lookup"><span data-stu-id="795f7-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="795f7-152">此方法會顯示簡易 **UIAlert**，以處理應用程式執行時接收到的通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="795f7-153">在 ViewController.m 中，新增 AppDelegate.h 的匯入陳述式，並將下列程式碼複製到 XCode 產生的 **訂閱** 方法中。</span><span class="sxs-lookup"><span data-stu-id="795f7-153">In ViewController.m, add a import statement for AppDelegate.h and copy the following code into the XCode-generated **subscribe** method.</span></span> <span data-ttu-id="795f7-154">此程式碼將更新通知註冊，以使用使用者在使用者介面中選擇的新類別標記。</span><span class="sxs-lookup"><span data-stu-id="795f7-154">This code will update the notification registration to use the new category tags the user has chosen in the user interface.</span></span>
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   <span data-ttu-id="795f7-155">此方法會建立類別的 **NSMutableArray**，並使用 **Notifications** 類別在本機儲存體中儲存清單，並在您的通知中樞註冊對應標籤。</span><span class="sxs-lookup"><span data-stu-id="795f7-155">This method creates an **NSMutableArray** of categories and uses the **Notifications** class to store the list in the local storage and registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="795f7-156">變更類別時，系統會使用新類別重新建立註冊。</span><span class="sxs-lookup"><span data-stu-id="795f7-156">When categories are changed, the registration is recreated with the new categories.</span></span>
3. <span data-ttu-id="795f7-157">在 ViewController.m 中，於 **viewDidLoad** 方法中新增下列程式碼，以根據先前儲存的類別來設定使用者介面。</span><span class="sxs-lookup"><span data-stu-id="795f7-157">In ViewController.m, add the following code in the **viewDidLoad** method to set the user interface based on the previously saved categories.</span></span>

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="795f7-158">應用程式現在可以在裝置本機儲存體中儲存一組類別，以用來在每次應用程式啟動時於通知中樞註冊。</span><span class="sxs-lookup"><span data-stu-id="795f7-158">The app can now store a set of categories in the device local storage used to register with the notification hub whenever the app starts.</span></span>  <span data-ttu-id="795f7-159">使用者可以在執行階段變更選取的類別，然後按一下 [訂閱]  方法來更新裝置的註冊。</span><span class="sxs-lookup"><span data-stu-id="795f7-159">The user can change the selection of categories at runtime and click the **subscribe** method to update the registration for the device.</span></span> <span data-ttu-id="795f7-160">接下來，您將更新應用程式，以直接在應用程式本身傳送即時新聞通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-160">Next, you will update the app to send the breaking news notifications directly in the app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="795f7-161">(選擇性) 傳送加註標記的通知</span><span class="sxs-lookup"><span data-stu-id="795f7-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="795f7-162">如果您無法存取 Visual Studio，可以跳到下一節，並從應用程式本身傳送通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-162">If you don't have access to Visual Studio, you can skip to the next section and send notifications from the app itself.</span></span> <span data-ttu-id="795f7-163">您也可以使用通知中樞的 [偵錯] 索引標籤，從 [Azure 傳統入口網站] 傳送正確的範本通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-163">You can also send the proper template notification from the [Azure Classic Portal] using the debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a><span data-ttu-id="795f7-164">(選擇性) 從裝置傳送通知</span><span class="sxs-lookup"><span data-stu-id="795f7-164">(optional) Send notifications from the device</span></span>
<span data-ttu-id="795f7-165">通知通常會由後端服務傳送，但您可直接從應用程式傳送即時新聞通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from the app.</span></span> <span data-ttu-id="795f7-166">若要這樣做會更新，`SendNotificationRESTAPI`我們中定義的方法[開始使用通知中樞][ get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="795f7-166">To do this we will update the `SendNotificationRESTAPI` method that we defined in the [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="795f7-167">在 ViewController.m 中，如下更新 `SendNotificationRESTAPI` 方法，使其接受類別標記的參數，並傳送正確的 [範本](notification-hubs-templates-cross-platform-push-messages.md) 通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-167">In ViewController.m update the `SendNotificationRESTAPI` method as follows so that it accepts a parameter for the category tag and sends the proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];
   
            [dataTask resume];
        }
2. <span data-ttu-id="795f7-168">在 ViewController.m 中，更新 [傳送通知]  動作 (如下列程式碼所示)。</span><span class="sxs-lookup"><span data-stu-id="795f7-168">In ViewController.m update the **Send Notification** action as shown in the code that follows.</span></span> <span data-ttu-id="795f7-169">因此，它將使用每個標記個別傳送通知，並傳送至多個平台。</span><span class="sxs-lookup"><span data-stu-id="795f7-169">So that it will send the notifications using each tag individually and send to multiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="795f7-170">重新建置專案，並確定您沒有建置錯誤。</span><span class="sxs-lookup"><span data-stu-id="795f7-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="795f7-171">執行應用程式並產生通知</span><span class="sxs-lookup"><span data-stu-id="795f7-171">Run the app and generate notifications</span></span>
1. <span data-ttu-id="795f7-172">按 [執行] 按鈕，以建置專案並啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="795f7-172">Press the Run button to build the project and start the app.</span></span> <span data-ttu-id="795f7-173">選取要訂閱的一些即時新聞選項，然後按 [訂閱]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="795f7-173">Select some breaking news options to subscribe to and then press the **Subscribe** button.</span></span> <span data-ttu-id="795f7-174">您應該會看到一個對話方塊，表示已訂閱通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-174">You should see a dialog indicating the notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="795f7-175">當您選擇 [訂閱] 時，應用程式會將選取的類別轉換成標籤，並在通知中心內為選取的標籤要求新裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="795f7-175">When you choose **Subscribe**, the app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span>
2. <span data-ttu-id="795f7-176">輸入要以即時新聞形式傳送的訊息，然後按下 [傳送通知]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="795f7-176">Enter a message to be sent as breaking news then press the **Send Notification** button.</span></span> <span data-ttu-id="795f7-177">或者，執行.NET 主控台應用程式來產生通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-177">Alternatively, run the .NET console app to generate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="795f7-178">每個訂閱即時新聞的裝置都會收到您剛剛傳送的即時新聞通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-178">Each device subscribed to breaking news will receive the breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="795f7-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="795f7-179">Next steps</span></span>
<span data-ttu-id="795f7-180">在本教學課程中，我們了解到如何按類別廣播即時新聞。</span><span class="sxs-lookup"><span data-stu-id="795f7-180">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="795f7-181">請考慮完成下列其中一個強調其他進階通知中心案例的教學課程：</span><span class="sxs-lookup"><span data-stu-id="795f7-181">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="795f7-182">**[使用通知中樞廣播已當地語系化的即時新聞]**</span><span class="sxs-lookup"><span data-stu-id="795f7-182">**[Use Notification Hubs to broadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="795f7-183">了解如何擴充即時新聞應用程式，以啟用傳送已當地語系化的通知。</span><span class="sxs-lookup"><span data-stu-id="795f7-183">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="795f7-184">[使用通知中樞廣播已當地語系化的即時新聞]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="795f7-184">[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
<span data-ttu-id="795f7-185">[Azure 傳統入口網站]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="795f7-185">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
