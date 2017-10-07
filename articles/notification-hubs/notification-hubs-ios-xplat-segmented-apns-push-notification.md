---
title: "aaaNotification 中樞中斷新聞教學課程-iOS"
description: "深入了解如何 toouse Azure Service Bus 通知中樞 toosend 重大消息通知 tooiOS 裝置。"
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
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="942ca-103">使用通知中樞 toosend 最新消息</span><span class="sxs-lookup"><span data-stu-id="942ca-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="942ca-104">概觀</span><span class="sxs-lookup"><span data-stu-id="942ca-104">Overview</span></span>
<span data-ttu-id="942ca-105">本主題說明如何 toouse Azure 通知中樞 toobroadcast 重大消息通知 tooan iOS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="942ca-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="942ca-106">完成時，您將會是能 tooregister 中斷您感興趣的新聞分類，並且接收只有那些類別目錄的推播通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="942ca-107">這個案例是許多應用程式的常見模式，通知其中有傳送 toobe toogroups 的先前尚未宣告欄位，例如 RSS 讀取器、 應用程式等的音樂迷感興趣的使用者。</span><span class="sxs-lookup"><span data-stu-id="942ca-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="942ca-108">啟用廣播的案例包括下列一個或多個*標記*時建立 hello 通知中樞的註冊。</span><span class="sxs-lookup"><span data-stu-id="942ca-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="942ca-109">當通知傳送 tooa 標記時，所有已註冊的裝置 hello 標記會收到 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="942ca-110">標記是只是字串，因為它們不需要預先佈建 toobe。</span><span class="sxs-lookup"><span data-stu-id="942ca-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="942ca-111">如需標記的詳細資訊，請參閱太[通知中樞路由和標記運算式](notification-hubs-tags-segment-push-message.md)。</span><span class="sxs-lookup"><span data-stu-id="942ca-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="942ca-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="942ca-112">Prerequisites</span></span>
<span data-ttu-id="942ca-113">本主題是根據您在建立 hello 應用程式[開始使用通知中樞][get-started]。</span><span class="sxs-lookup"><span data-stu-id="942ca-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="942ca-114">開始本教學課程之前，您必須已完成[開始使用通知中樞][get-started]。</span><span class="sxs-lookup"><span data-stu-id="942ca-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="942ca-115">加入類別目錄選取 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="942ca-115">Add category selection toohello app</span></span>
<span data-ttu-id="942ca-116">hello 第一個步驟是 tooadd hello UI 項目 tooyour 現有分鏡腳本可讓 hello 使用者 tooselect 類別 tooregister。</span><span class="sxs-lookup"><span data-stu-id="942ca-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="942ca-117">使用者選取的 hello 類別會儲存在 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="942ca-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="942ca-118">Hello 應用程式啟動時，裝置註冊會建立您的通知中樞與 hello 選取類別目錄中，為標記。</span><span class="sxs-lookup"><span data-stu-id="942ca-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="942ca-119">在您 MainStoryboard_iPhone.storyboard 加入 hello hello 物件程式庫中的下列元件：</span><span class="sxs-lookup"><span data-stu-id="942ca-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="942ca-120">具有「即時新聞」文字的標籤，</span><span class="sxs-lookup"><span data-stu-id="942ca-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="942ca-121">具有「世界」、「政治」、「商業」、「技術」、「科學」、「體育」等類別文字的標籤，</span><span class="sxs-lookup"><span data-stu-id="942ca-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="942ca-122">六個參數，其中每個類別，設定每個交換器**狀態**toobe**關閉**預設。</span><span class="sxs-lookup"><span data-stu-id="942ca-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="942ca-123">一個標示為「訂閱」的按鈕</span><span class="sxs-lookup"><span data-stu-id="942ca-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="942ca-124">您的腳本應如下所示：</span><span class="sxs-lookup"><span data-stu-id="942ca-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="942ca-125">在 hello 助理編輯器中，建立所有 hello 交換器插座，並呼叫它們"WorldSwitch"，"PoliticsSwitch"、"BusinessSwitch"、"TechnologySwitch"、"ScienceSwitch"、"SportsSwitch"</span><span class="sxs-lookup"><span data-stu-id="942ca-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="942ca-126">為名為「訂閱」的按鈕建立「動作」。</span><span class="sxs-lookup"><span data-stu-id="942ca-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="942ca-127">您 ViewController.h 應該包含 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="942ca-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="942ca-128">建立稱為 `Notifications` 的新 **Cocoa Touch 類別**。</span><span class="sxs-lookup"><span data-stu-id="942ca-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="942ca-129">複製下列程式碼 hello 檔案 Notifications.h hello 介面區段中的 hello:</span><span class="sxs-lookup"><span data-stu-id="942ca-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="942ca-130">加入下列匯入指示詞 tooNotifications.m hello:</span><span class="sxs-lookup"><span data-stu-id="942ca-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="942ca-131">複製下列程式碼 hello 檔案 Notifications.m hello 實作區段中的 hello。</span><span class="sxs-lookup"><span data-stu-id="942ca-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
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



    <span data-ttu-id="942ca-132">這個類別會使用本機儲存體 toostore 並擷取此裝置將會收到的新聞 hello 類別。</span><span class="sxs-lookup"><span data-stu-id="942ca-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="942ca-133">此外，它包含使用這些類別的方法 tooregister[範本](notification-hubs-templates-cross-platform-push-messages.md)註冊。</span><span class="sxs-lookup"><span data-stu-id="942ca-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="942ca-134">在 hello h 檔案，如 Notifications.h 新增匯入陳述式，並加入 hello 通知類別的執行個體的屬性：</span><span class="sxs-lookup"><span data-stu-id="942ca-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="942ca-135">在 hello **didFinishLaunchingWithOptions** d 中的方法在 hello 方法 hello 開頭加入 hello 程式碼 tooinitialize hello 通知執行個體。</span><span class="sxs-lookup"><span data-stu-id="942ca-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="942ca-136">`HUBNAME`和`HUBLISTENACCESS`（定義於 hubinfo.h） 應該已經有 hello`<hub name>`和`<connection string with listen access>`預留位置將取代通知中樞名稱和 hello 的連接字串*DefaultListenSharedAccessSignature*您稍早取得</span><span class="sxs-lookup"><span data-stu-id="942ca-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="942ca-137">發佈的用戶端應用程式的認證不是一般安全的因為您只應該與用戶端應用程式來散發 hello 接聽 」 存取權的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="942ca-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="942ca-138">接聽存取啟用通知，但現有的註冊您的應用程式 tooregister 無法修改，而且無法傳送通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="942ca-139">hello 完整的存取金鑰會用於傳送通知和變更現有註冊的受保護的後端服務。</span><span class="sxs-lookup"><span data-stu-id="942ca-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="942ca-140">在 hello **didRegisterForRemoteNotificationsWithDeviceToken** d 中的方法取代下列程式碼 toopass hello 裝置權杖 toohello 通知類別 hello hello hello 方法中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="942ca-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="942ca-141">hello 通知類別將會執行 hello 註冊與 hello 分類通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="942ca-142">如果 hello 使用者變更選取類別目錄項目，我們會呼叫 hello`subscribeWithCategories`中回應 toohello 方法**訂閱**按鈕 tooupdate 它們。</span><span class="sxs-lookup"><span data-stu-id="942ca-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="942ca-143">因為 hello hello Apple Push Notification Service (APNS) 所指派的裝置權杖可以隨時可能發生的您應該註冊通知經常 tooavoid 通知失敗。</span><span class="sxs-lookup"><span data-stu-id="942ca-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="942ca-144">每次該 hello 應用程式啟動時，這個範例會註冊通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="942ca-145">針對經常執行的應用程式，一天一次以上，您可以可能略過註冊 toopreserve 頻寬如果少於一天，已經過 hello 先前的登錄。</span><span class="sxs-lookup"><span data-stu-id="942ca-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="942ca-146">請注意，此時應該沒有其他程式碼中 hello **didRegisterForRemoteNotificationsWithDeviceToken**方法。</span><span class="sxs-lookup"><span data-stu-id="942ca-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="942ca-147">hello 下列方法應該是已經存在於 d 完成 hello[開始使用通知中樞][ get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="942ca-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="942ca-148">否則，請予以新增。</span><span class="sxs-lookup"><span data-stu-id="942ca-148">If not, add them.</span></span>
   
    <span data-ttu-id="942ca-149">-(void) MessageBox:(NSString *) 標題訊息:(NSString *) messageText {</span><span class="sxs-lookup"><span data-stu-id="942ca-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="942ca-150">}</span><span class="sxs-lookup"><span data-stu-id="942ca-150">}</span></span>
   
   * <span data-ttu-id="942ca-151">(void) 的應用程式:(UIApplication *) 應用程式 didReceiveRemoteNotification: (NSDictionary *) 使用者資訊 {NSLog (@"%@"，所以);  [自我 MessageBox:@"Notification 」 的訊息: [[使用者資訊 objectForKey:@"aps]"valueForKey:@"alert"]]。}</span><span class="sxs-lookup"><span data-stu-id="942ca-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="942ca-152">這個方法會處理透過顯示簡單 hello 應用程式執行時收到通知**UIAlert**。</span><span class="sxs-lookup"><span data-stu-id="942ca-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="942ca-153">在 ViewController.m，加入下列程式碼到 hello h 和複製 hello 匯入陳述式產生的 XCode**訂閱**方法。</span><span class="sxs-lookup"><span data-stu-id="942ca-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="942ca-154">此程式碼會更新 hello 通知註冊 toouse hello 新分類標記 hello 使用者已選擇 hello 使用者介面中。</span><span class="sxs-lookup"><span data-stu-id="942ca-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
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
   
   <span data-ttu-id="942ca-155">這個方法會建立**NSMutableArray**的類別，並使用 hello**通知**hello 本機儲存體和暫存器 hello 相對應的標記與您的通知中樞中的類別 toostore hello 清單。</span><span class="sxs-lookup"><span data-stu-id="942ca-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="942ca-156">類別目錄會變更時，重新建立 hello 註冊 hello 新類別。</span><span class="sxs-lookup"><span data-stu-id="942ca-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="942ca-157">中 ViewController.m，加入下列程式碼中 hello hello **viewDidLoad** hello 先前儲存的類別為基礎的方法 tooset hello 使用者介面。</span><span class="sxs-lookup"><span data-stu-id="942ca-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="942ca-158">每次 hello 應用程式啟動時 hello 應用程式現在可以在 hello 裝置使用的本機儲存體 tooregister hello 通知中樞與儲存一組類別目錄。</span><span class="sxs-lookup"><span data-stu-id="942ca-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="942ca-159">hello 使用者可以在執行階段類別 hello 選取範圍，然後按一下 hello**訂閱**方法 tooupdate hello 註冊 hello 裝置。</span><span class="sxs-lookup"><span data-stu-id="942ca-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="942ca-160">接下來，您將更新直接 hello 應用程式本身的重大消息 hello 應用程式 toosend hello。</span><span class="sxs-lookup"><span data-stu-id="942ca-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="942ca-161">(選擇性) 傳送加註標記的通知</span><span class="sxs-lookup"><span data-stu-id="942ca-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="942ca-162">如果您沒有存取 tooVisual Studio，則可以略過 toohello 下一節，並從 hello 應用程式本身傳送通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="942ca-163">您也可以從 hello 傳送嗨適當範本通知[Azure 傳統入口網站]使用通知中樞的 hello 偵錯 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="942ca-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="942ca-164">（選擇性）從 hello 裝置傳送通知</span><span class="sxs-lookup"><span data-stu-id="942ca-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="942ca-165">通常會由後端服務傳送通知，但您可以傳送重大消息直接從 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="942ca-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="942ca-166">toodo 這我們將會更新 hello`SendNotificationRESTAPI`我們 hello 中定義的方法[開始使用通知中樞][ get-started]教學課程。</span><span class="sxs-lookup"><span data-stu-id="942ca-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="942ca-167">在 ViewController.m 更新 hello`SendNotificationRESTAPI`做的方法會依循，以便接受 hello 類別標記的參數，並傳送嗨適當[範本](notification-hubs-templates-cross-platform-push-messages.md)通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
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
2. <span data-ttu-id="942ca-168">在 ViewController.m 更新 hello**傳送通知**hello 後面的程式碼所示的動作。</span><span class="sxs-lookup"><span data-stu-id="942ca-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="942ca-169">因此，它會傳送 hello 通知個別使用每個標記，並傳送 toomultiple 平台。</span><span class="sxs-lookup"><span data-stu-id="942ca-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="942ca-170">重新建置專案，並確定您沒有建置錯誤。</span><span class="sxs-lookup"><span data-stu-id="942ca-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="942ca-171">執行 hello 應用程式，並產生通知</span><span class="sxs-lookup"><span data-stu-id="942ca-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="942ca-172">按 hello 執行按鈕 toobuild hello 專案，並啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="942ca-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="942ca-173">選取一些重大消息選項 toosubscribe tooand，然後按下 hello**訂閱** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="942ca-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="942ca-174">您應該會看到對話方塊，表示已訂閱通知的 hello。</span><span class="sxs-lookup"><span data-stu-id="942ca-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="942ca-175">當您選擇**訂閱**、 標記成 hello 應用程式將選取的 hello 類別和從 hello 通知中樞要求新的裝置註冊 hello 選取標記。</span><span class="sxs-lookup"><span data-stu-id="942ca-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="942ca-176">輸入傳送重大消息然後按下 hello 訊息 toobe**傳送通知** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="942ca-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="942ca-177">或者，執行 hello.NET 主控台應用程式 toogenerate 通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="942ca-178">每個訂閱的裝置 toobreaking 新聞會接收您傳送的 hello 重大新聞通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="942ca-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="942ca-179">Next steps</span></span>
<span data-ttu-id="942ca-180">在此教學課程中我們學到如何 toobroadcast 依類別目錄中最新消息。</span><span class="sxs-lookup"><span data-stu-id="942ca-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="942ca-181">完成下列其中一個 hello 下列反白顯示其他進階的通知中心案例的教學課程，請考慮：</span><span class="sxs-lookup"><span data-stu-id="942ca-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="942ca-182">**[使用通知中樞 toobroadcast 當地語系化重大消息]**</span><span class="sxs-lookup"><span data-stu-id="942ca-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="942ca-183">了解如何傳送 tooenable 新聞應用程式的重大 tooexpand hello 當地語系化通知。</span><span class="sxs-lookup"><span data-stu-id="942ca-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[使用通知中樞 toobroadcast 當地語系化重大消息]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[Azure 傳統入口網站]: https://manage.windowsazure.com
