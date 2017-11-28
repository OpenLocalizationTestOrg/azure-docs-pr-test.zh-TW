---
title: "ios 與.NET 後端 aaaAzure 通知中樞通知使用者"
description: "了解如何 toosend 推播通知 toousers 在 Azure 中。 Objective C 和 hello 後端 hello.NET API 撰寫的程式碼範例。"
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="c502a-104">Azure 通知中樞透過 .NET 後端通知 iOS 使用者</span><span class="sxs-lookup"><span data-stu-id="c502a-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="c502a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="c502a-105">Overview</span></span>
<span data-ttu-id="c502a-106">在 Azure 中的推播通知支援可讓您 tooaccess 方便使用、 多平台，並向外延展推播基礎結構，可大幅簡化 hello 實作消費者和企業行動應用程式的應用程式的推播通知平台。</span><span class="sxs-lookup"><span data-stu-id="c502a-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="c502a-107">本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa 特定的應用程式使用者在特定的裝置上。</span><span class="sxs-lookup"><span data-stu-id="c502a-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="c502a-108">ASP.NET WebAPI 後端使用的 tooauthenticate 用戶端和 toogenerate 通知中所示 hello 指引主題[從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)。</span><span class="sxs-lookup"><span data-stu-id="c502a-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="c502a-109">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="c502a-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="c502a-110">本教學課程也是 hello 必要條件 toohello[安全 Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="c502a-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="c502a-111">如果您想 toouse 行動應用程式做為後端服務時，請參閱 hello[行動應用程式開始使用推播](../app-service-mobile/app-service-mobile-ios-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="c502a-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="c502a-112">修改您的 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="c502a-112">Modify your iOS app</span></span>
1. <span data-ttu-id="c502a-113">開啟 hello 單一頁面檢視應用程式建立 hello[開始使用通知中心 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="c502a-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c502a-114">在本節中，我們假設您已使用空白組織名稱設定您的專案。</span><span class="sxs-lookup"><span data-stu-id="c502a-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="c502a-115">如果沒有，您將需要 tooprepend 組織名稱 tooall 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="c502a-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="c502a-116">在您 Main.storyboard 加入顯示 hello 以下螢幕擷取畫面來自 hello 物件程式庫中的 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="c502a-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="c502a-117">**使用者名稱**： 與預留位置文字，UITextField*輸入使用者名稱*，立即下方 hello 傳送結果標籤和受條件約束的 toohello 左和右邊界和下 hello 傳送結果的標籤。</span><span class="sxs-lookup"><span data-stu-id="c502a-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="c502a-118">**密碼**: UITextField 與預留位置文字，*輸入密碼*、 立即下方 hello username 文字欄位和受條件約束的 toohello 左和右邊界和下 hello 使用者名稱的文字欄位。</span><span class="sxs-lookup"><span data-stu-id="c502a-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="c502a-119">檢查 hello**安全文字項目**底下選項中 hello 屬性偵測器，*傳回金鑰*。</span><span class="sxs-lookup"><span data-stu-id="c502a-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="c502a-120">**登入**: UIButton 標記為立即 hello 密碼文字欄位下方，然後取消選取 hello**啟用**底下選項中 hello 屬性偵測器，*控制項內容*</span><span class="sxs-lookup"><span data-stu-id="c502a-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="c502a-121">**WNS**： 標籤和交換器 tooenable 傳送 hello 通知 Windows 通知服務是否已遭 hello 集線器上的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c502a-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="c502a-122">請參閱 hello [Windows 入門](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="c502a-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="c502a-123">**GCM**： 標籤和交換器 tooenable 傳送 hello 通知 tooGoogle Cloud Messaging 如果已經過 hello 集線器上的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="c502a-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="c502a-124">請參閱 [Android 入門](notification-hubs-android-push-notification-google-gcm-get-started.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="c502a-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="c502a-125">**APNS**： 標籤和交換器 tooenable 傳送 hello 通知 toohello Apple 平台通知服務。</span><span class="sxs-lookup"><span data-stu-id="c502a-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="c502a-126">**Recipent Username**: UITextField 與預留位置文字，*收件者的使用者名稱標記*、 立即下方 hello GCM 標籤，以及限制的 toohello 左右邊界和下 hello GCM 標籤。</span><span class="sxs-lookup"><span data-stu-id="c502a-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="c502a-127">某些元件已加入在 hello[開始使用通知中心 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="c502a-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="c502a-128">**Ctrl**拖曳 hello 檢視 tooViewController.h 中的 hello 元件，並加入這些新的插座。</span><span class="sxs-lookup"><span data-stu-id="c502a-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="c502a-129">在 ViewController.h，加入 hello 下列`#define`您匯入陳述式正下方。</span><span class="sxs-lookup"><span data-stu-id="c502a-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="c502a-130">替代 hello *< 輸入後端端點\>*預留位置 hello 使用 toodeploy 您應用程式後端 hello 前一節中的目的地 URL。</span><span class="sxs-lookup"><span data-stu-id="c502a-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="c502a-131">例如，*http://you_backend.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="c502a-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="c502a-132">在您的專案，建立新**Cocoa 觸控類別**名為**RegisterClient** toointerface 以 hello ASP.NET 後端所建立。</span><span class="sxs-lookup"><span data-stu-id="c502a-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="c502a-133">建立 hello 類別繼承自`NSObject`。</span><span class="sxs-lookup"><span data-stu-id="c502a-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="c502a-134">然後加入下列程式碼中 hello RegisterClient.h hello。</span><span class="sxs-lookup"><span data-stu-id="c502a-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="c502a-135">在 hello RegisterClient.m 更新 hello `@interface` > 一節：</span><span class="sxs-lookup"><span data-stu-id="c502a-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. <span data-ttu-id="c502a-136">取代 hello `@implementation` hello RegisterClient.m 以下列程式碼的 hello > 一節。</span><span class="sxs-lookup"><span data-stu-id="c502a-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    <span data-ttu-id="c502a-137">上述程式碼 hello 實作 hello 指引文件所述的 hello 邏輯[從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)使用 NSURLSession tooperform REST 呼叫 tooyour 應用程式後端和 NSUserDefaults toolocally 存放區 helloregistrationId 傳回 hello 通知中樞。</span><span class="sxs-lookup"><span data-stu-id="c502a-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="c502a-138">請注意，這個類別會要求其屬性**authorizationHeader** toobe 順序 toowork 中正確設定。</span><span class="sxs-lookup"><span data-stu-id="c502a-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="c502a-139">這個屬性設定的 hello **ViewController**類別之後 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="c502a-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="c502a-140">在 ViewController.h 中，為 RegisterClient.h 新增 `#import` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c502a-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="c502a-141">然後加入 hello 裝置權杖的宣告，並參考 tooa `RegisterClient` hello 中的執行個體`@interface`> 一節：</span><span class="sxs-lookup"><span data-stu-id="c502a-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="c502a-142">在 ViewController.m，加入私用方法宣告中 hello `@interface` > 一節：</span><span class="sxs-lookup"><span data-stu-id="c502a-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="c502a-143">hello 下列程式碼片段是不安全的驗證配置，則應該取代 hello hello 實作**createAndSetAuthenticationHeaderWithUsername:AndPassword:**與特定的驗證機制如此會產生供 hello 註冊用戶端類別，例如 OAuth、 Active Directory 驗證語彙基元 toobe。</span><span class="sxs-lookup"><span data-stu-id="c502a-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="c502a-144">接著在 hello `@implementation` ViewController.m 區段新增下列程式碼，這會將設定 hello 裝置權杖並驗證標頭的 hello 實作的 hello。</span><span class="sxs-lookup"><span data-stu-id="c502a-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    <span data-ttu-id="c502a-145">請注意如何設定 hello 裝置權杖讓 hello 登入 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c502a-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="c502a-146">這是因為 hello 檢視控制器註冊推播通知與 hello 應用程式後端 hello 登入動作的一部分。</span><span class="sxs-lookup"><span data-stu-id="c502a-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="c502a-147">因此，我們不會希望動作 toobe 登入存取直到 hello 裝置權杖已正確設定。</span><span class="sxs-lookup"><span data-stu-id="c502a-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="c502a-148">只要 hello 前者會發生後者 hello 之前，可以分離與 hello 推播註冊的 hello 登入。</span><span class="sxs-lookup"><span data-stu-id="c502a-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="c502a-149">在 ViewController.m，使用下列程式碼片段 tooimplement hello 動作方法的 hello 您**登入**按鈕和方法 toosend hello 通知訊息使用 hello ASP.NET 後端。</span><span class="sxs-lookup"><span data-stu-id="c502a-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="c502a-150">(IBAction)LogInAction: (id) 寄件者 {/ / 建立驗證標頭，並將其設定中註冊用戶端 NSString * 使用者名稱 = 本身。UsernameField.text;  NSString * 密碼 = 本身。PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="c502a-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="c502a-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="c502a-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="c502a-152">__weak ViewController * selfie = 本身;  [self.registerClient registerWithDeviceToken:self.deviceToken 標記： nil andCompletion:^(NSError* error){如果 (！ 錯誤) {dispatch_async(dispatch_get_main_queue()，^ {selfie。SendNotificationButton.enabled = YES;              [self MessageBox:@"Success"message:@"Registered 成功 ！"];});}}]。}</span><span class="sxs-lookup"><span data-stu-id="c502a-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="c502a-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="c502a-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="c502a-154">傳遞做為參數與 hello REST URL toohello ASP.NET 後端 NSURL * requestURL hello pns 和使用者名稱標記 = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications？ pns = %@ （& s) to_tag = %@"，BACKEND_ENDPOINT pns、 usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="c502a-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="c502a-155">NSMutableURLRequest * 要求 = [NSMutableURLRequest requestWithURL:requestURL];   [要求 setHTTPMethod:@"POST"]。</span><span class="sxs-lookup"><span data-stu-id="c502a-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="c502a-156">收到 hello 模擬或 authenticationheader hello 註冊用戶端 NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@"，self.registerClient.authenticationHeader];   [要求 setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"]。</span><span class="sxs-lookup"><span data-stu-id="c502a-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="c502a-157">新增 hello 通知訊息主體 [要求 setValue:@"application/json;charset=utf-8"forHTTPHeaderField:@"Content-Type"]。   [要求 setHTTPBody: [訊息 dataUsingEncoding:NSUTF8StringEncoding]]。</span><span class="sxs-lookup"><span data-stu-id="c502a-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="c502a-158">執行 hello 傳送通知 REST API 上 hello ASP.NET 後端 NSURLSessionDataTask * dataTask = [工作階段 dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *錯誤） {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) 回應。       如果 (錯誤 | | httpResponse.statusCode ！ = 200) {NSString*狀態 = [%NSString stringWithFormat:@"Error 狀態 @: %d\nerror: %@\n"，pns，httpResponse.statusCode、 錯誤]。           dispatch_async(dispatch_get_main_queue()，^ {/ / 附加文字，因為所有 3 PNS 呼叫可能也會有資訊 tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]]。           });           NSLog(status);       }</span><span class="sxs-lookup"><span data-stu-id="c502a-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="c502a-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="c502a-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="c502a-160">更新 hello 的 hello 動作**傳送通知**按鈕 toouse hello ASP.NET 後端和傳送 tooany PNS 啟用參數。</span><span class="sxs-lookup"><span data-stu-id="c502a-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. <span data-ttu-id="c502a-161">函式中**ViewDidLoad**、 加入 hello 遵循 tooinstantiate hello RegisterClient 執行個體，並將設定文字欄位的 hello 委派。</span><span class="sxs-lookup"><span data-stu-id="c502a-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="c502a-162">此時**d**，移除所有 hello 內容 hello 方法**應用程式： didRegisterForPushNotificationWithDeviceToken:**並取代 hello 檢視，確定下列 toomake hello控制器包含 hello APNs 從擷取最新裝置權杖：</span><span class="sxs-lookup"><span data-stu-id="c502a-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="c502a-163">最後在**d**，請確定您擁有 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="c502a-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="c502a-164">測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c502a-164">Test hello Application</span></span>
1. <span data-ttu-id="c502a-165">在 XCode 中，hello 應用程式實體 iOS 裝置上執行 (push 通知將無法運作 hello 模擬器中)。</span><span class="sxs-lookup"><span data-stu-id="c502a-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="c502a-166">在 hello iOS 應用程式 UI 中輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c502a-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="c502a-167">這些可以是任何字串，但兩者都是 hello 相同的字串值。</span><span class="sxs-lookup"><span data-stu-id="c502a-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="c502a-168">然後按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="c502a-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="c502a-169">您應該會看到註冊成功的快顯通知。</span><span class="sxs-lookup"><span data-stu-id="c502a-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="c502a-170">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="c502a-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="c502a-171">在 hello **收件者的使用者名稱標記*文字欄位中，輸入 hello 從另一個裝置 hello 註冊搭配使用的使用者名稱標記。</span><span class="sxs-lookup"><span data-stu-id="c502a-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="c502a-172">輸入通知訊息並按一下 [ **傳送通知**]。</span><span class="sxs-lookup"><span data-stu-id="c502a-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="c502a-173">僅限 hello 擁有 hello 收件者的使用者名稱標記的已註冊的裝置收到 hello 通知訊息。</span><span class="sxs-lookup"><span data-stu-id="c502a-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="c502a-174">它只會傳送 toothose 使用者。</span><span class="sxs-lookup"><span data-stu-id="c502a-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
