---
title: "Azure 通知中樞透過 .NET 後端通知 iOS 使用者"
description: "了解如何在 Azure 中將推播通知傳送給使用者。 程式碼範例是以 Objective-C 撰寫並以 .NET API 作為後端。"
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
ms.openlocfilehash: 0fa7a886e1ecb0a90b6aebc1dbf9ef0c6ce1acf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="7ff8d-104">Azure 通知中樞透過 .NET 後端通知 iOS 使用者</span><span class="sxs-lookup"><span data-stu-id="7ff8d-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="7ff8d-105">概觀</span><span class="sxs-lookup"><span data-stu-id="7ff8d-105">Overview</span></span>
<span data-ttu-id="7ff8d-106">Azure 中的推播通知支援可讓您存取易於使用、多重平台的大規模推播基礎結構，而大幅簡化消費者和企業應用程式在行動平台上的推播通知實作。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="7ff8d-107">本教學課程將示範如何使用 Azure 通知中心，來將推播通知傳送到特定裝置上的特定應用程式使用者。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="7ff8d-108">ASP.NET WebAPI 後端可用來驗證用戶端並產生通知，如指引主題[從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)中所示。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="7ff8d-109">本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="7ff8d-110">本教學課程還是 [安全推播 (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) 教學課程的必要條件。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-110">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="7ff8d-111">如果您想要使用 Mobile Apps 作為您的後端服務，請參閱 [開始使用 Mobile Apps 推播](../app-service-mobile/app-service-mobile-ios-get-started-push.md)。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-111">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="7ff8d-112">修改您的 iOS 應用程式</span><span class="sxs-lookup"><span data-stu-id="7ff8d-112">Modify your iOS app</span></span>
1. <span data-ttu-id="7ff8d-113">開啟您在 [開始使用通知中心 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) 教學課程中建立的 [單頁] 檢視應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-113">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7ff8d-114">在本節中，我們假設您已使用空白組織名稱設定您的專案。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="7ff8d-115">否則，您需要針對所有類別名稱預先考量您的組織名稱。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-115">If not, you will need to prepend your organization name to all class names.</span></span>
   > 
   > 
2. <span data-ttu-id="7ff8d-116">在您的 Main.storyboard 中從物件程式庫新增下面的螢幕擷取畫面中顯示的元件。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-116">In your Main.storyboard add the components shown in the screenshot below from the object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="7ff8d-117">**使用者名稱**：含有預留位置文字 ( *輸入使用者名稱*) 的 UITextField，位於傳送結果標籤正下方且受到左右邊界限制並位於傳送結果標籤正下方。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="7ff8d-118">**密碼**：含有預留位置文字 ( *輸入密碼*) 的 UITextField，位於使用者名稱文字欄位正下方且受到左右邊界限制並位於使用者文字欄位正下方。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="7ff8d-119">勾選 [ **傳回金鑰** ] 底下屬性偵測器中的 [ *安全文字輸入*] 選項。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-119">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="7ff8d-120">**登入**：密碼文字欄位正下方標記的 UIButton，並取消勾選 [控制項內容] 底下屬性偵測器中的 [啟用] 選項。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-120">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="7ff8d-121">**WNS**：當中樞中已設定 Windows 通知服務時，用來啟用傳送通知功能的標籤與開關。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-121">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been setup on the hub.</span></span> <span data-ttu-id="7ff8d-122">請參閱 [Windows 入門](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-122">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="7ff8d-123">**GCM**：當中樞中已設定 Google Cloud Messaging 時，用來啟用傳送通知功能的標籤與開關。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-123">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been setup on the hub.</span></span> <span data-ttu-id="7ff8d-124">請參閱 [Android 入門](notification-hubs-android-push-notification-google-gcm-get-started.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="7ff8d-125">**APNS**：啟用傳送通知給 Apple 平台通知服務之功能的標籤與開關。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-125">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="7ff8d-126">**收件者使用者名稱**：含有預留位置文字 ( *收件者使用者名稱標記*) 的 UITextField，位於 GCM 標籤正下方且受到左右邊界限制並位於 GCM 正下方。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="7ff8d-127">在 [開始使用通知中心 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) 教學課程中已經新增一些元件。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-127">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="7ff8d-128">**Ctrl** 可拖曳檢視中的元件到 ViewController.h，並新增這些新的輸出。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-128">**Ctrl** drag from the components in the view to ViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used to enable the buttons on the UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used to enabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="7ff8d-129">請在 ViewController.h 中，在您的匯入陳述式正下方新增以下的 `#define` 。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-129">In ViewController.h, add the following `#define` just below your import statements.</span></span> <span data-ttu-id="7ff8d-130">將 *<輸入您的後端端點\>* 預留位置替換成上一節中用來部署應用程式後端的目的地 URL。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-130">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="7ff8d-131">例如，*http://you_backend.azurewebsites.net*。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="7ff8d-132">在您的專案中，建立一個名為 **RegisterClient** 的新 **Cocoa Touch class** 作為與您建立之 ASP.NET 後端互動的介面。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="7ff8d-133">建立繼承自 `NSObject`的類別。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-133">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="7ff8d-134">然後在 RegisterClient.h 中新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-134">Then add the following code in the RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="7ff8d-135">在 RegisterClient.m 中，更新 `@interface` 區段：</span><span class="sxs-lookup"><span data-stu-id="7ff8d-135">In the RegisterClient.m update the `@interface` section:</span></span>
   
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
5. <span data-ttu-id="7ff8d-136">使用以下程式碼取代 RegisterClient.m 中的 `@implementation` 區段。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-136">Replace the `@implementation` section in the RegisterClient.m with the following code.</span></span>

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

    <span data-ttu-id="7ff8d-137">上面的程式碼會實作指引文章 [從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) 中所說明的邏輯，方法是使用 NSURLSession 來對您的應用程式後端執行 REST 呼叫，然後使用 NSUserDefaults 來本機儲存通知中心傳回的 registrationId。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-137">The code above implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="7ff8d-138">請注意，此類別需要設定 **authorizationHeader** 屬性，才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-138">Note that this class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="7ff8d-139">您可以在登入後，透過 **ViewController** 類別設定此屬性。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-139">This property is set by the **ViewController** class after the log in.</span></span>

1. <span data-ttu-id="7ff8d-140">在 ViewController.h 中，為 RegisterClient.h 新增 `#import` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="7ff8d-141">然後為裝置權杖新增宣告，並參照 `@interface` 區段中的 `RegisterClient` 執行個體：</span><span class="sxs-lookup"><span data-stu-id="7ff8d-141">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="7ff8d-142">在 ViewController.m 中，於 `@interface` 區段中新增私用方法宣告：</span><span class="sxs-lookup"><span data-stu-id="7ff8d-142">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create the Authorization header to perform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="7ff8d-143">下列片段不是安全驗證結構描述，您應將 **createAndSetAuthenticationHeaderWithUsername:AndPassword:** 的實作替代成特定的驗證機制，使該機制產生註冊用戶端類別所利用的驗證權杖，例如 OAuth、Active Directory。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-143">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="7ff8d-144">然後在 ViewController.m 的 `@implementation` 區段中新增以下程式碼，這會新增實作以設定裝置權杖與驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-144">Then in the `@implementation` section of ViewController.m add the following code which adds the implementation for setting the device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="7ff8d-145">請留意設定裝置權杖如何啟用登入按鈕。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-145">Note how setting the device token enables the log in button.</span></span> <span data-ttu-id="7ff8d-146">這是因為檢視控制器會向應用程式後端註冊推播通知 (作為登入動作的一部分)。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-146">This is becasue as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="7ff8d-147">因此，在裝置權杖已正確設定之前，我們不希望有人能夠存取登入動作。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-147">Hence, we do not want Log In action to be accessible till the device token has been properly set up.</span></span> <span data-ttu-id="7ff8d-148">只要登入在推播註冊之前發生，您可能就會想要將前者與後者分開。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-148">You can decouple the log in from the push registration as long as the former happens before the latter.</span></span>
2. <span data-ttu-id="7ff8d-149">在 ViewController.m 中，使用以下程式碼片段為您的 [ **登入** ] 按鈕實作動作方法，以及實作一個方法來使用 ASP.NET 後端傳送通知訊息。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-149">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>
   
       - <span data-ttu-id="7ff8d-150">(IBAction)LogInAction: (id) 寄件者 {/ / 建立驗證標頭，並將其設定中註冊用戶端 NSString * 使用者名稱 = 本身。UsernameField.text;  NSString * 密碼 = 本身。PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="7ff8d-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="7ff8d-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="7ff8d-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="7ff8d-152">__weak ViewController * selfie = 本身;  [self.registerClient registerWithDeviceToken:self.deviceToken 標記： nil andCompletion:^(NSError* error){如果 (！ 錯誤) {dispatch_async(dispatch_get_main_queue()，^ {selfie。SendNotificationButton.enabled = YES;              [self MessageBox:@"Success"message:@"Registered 成功 ！"];});}}]。}</span><span class="sxs-lookup"><span data-stu-id="7ff8d-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="7ff8d-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="7ff8d-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="7ff8d-154">將 pns 和使用者名稱標記為 REST url 參數傳遞給 ASP.NET 後端 NSURL * requestURL = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications？ pns = %@ （& s) to_tag = %@"，BACKEND_ENDPOINT pns、 usernameTag]]。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-154">// Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="7ff8d-155">NSMutableURLRequest * 要求 = [NSMutableURLRequest requestWithURL:requestURL];   [要求 setHTTPMethod:@"POST"]。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="7ff8d-156">註冊用戶端從 NSString * authorizationHeaderValue 取得模擬或 authenticationheader = [NSString stringWithFormat:@"Basic %@"，self.registerClient.authenticationHeader];   [要求 setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"]。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-156">// Get the mock authenticationheader from the register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="7ff8d-157">將通知訊息主體 [要求 setValue:@"application/json;charset=utf-8"forHTTPHeaderField:@"Content-Type"]。   [要求 setHTTPBody: [訊息 dataUsingEncoding:NSUTF8StringEncoding]]。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-157">//Add the notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="7ff8d-158">傳送通知 REST API 執行 ASP.NET 後端 NSURLSessionDataTask * dataTask = [工作階段 dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) 回應。       如果 (錯誤 | | httpResponse.statusCode ！ = 200) {NSString*狀態 = [%NSString stringWithFormat:@"Error 狀態 @: %d\nerror: %@\n"，pns，httpResponse.statusCode、 錯誤]。           dispatch_async(dispatch_get_main_queue()，^ {/ / 附加文字，因為所有 3 PNS 呼叫可能也有到 [self.sendResults setText:[self.sendResults.text stringByAppendingString:status] 檢視的資訊]。           });           NSLog(status);       }</span><span class="sxs-lookup"><span data-stu-id="7ff8d-158">// Execute the send notification REST API on the ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information to view                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="7ff8d-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="7ff8d-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="7ff8d-160">更新 [ **傳送通知** ] 按鈕的動作來使用 ASP.NET 後端，並傳送至由任何開關啟用的任何 PNS。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-160">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="7ff8d-161">在 **ViewDidLoad**函數中，新增下列內容以具現化 RegisterClient 執行個體，並設定文字欄位的委派。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-161">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="7ff8d-162">現在於 **AppDelegate.m** 中，移除 **application:didRegisterForPushNotificationWithDeviceToken:** 方法的所有內容，並使用下列內容取代它，確定檢視控制器包含從 APN 擷取的最新裝置權杖：</span><span class="sxs-lookup"><span data-stu-id="7ff8d-162">Now in **AppDelegate.m**, remove all the content of the method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>
   
       // Add import to the top of the file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="7ff8d-163">最後，在 **AppDelegate.m**中，確定您有下列方法：</span><span class="sxs-lookup"><span data-stu-id="7ff8d-163">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-the-application"></a><span data-ttu-id="7ff8d-164">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="7ff8d-164">Test the Application</span></span>
1. <span data-ttu-id="7ff8d-165">在 XCode 中，在實體 iOS 裝置上執行應用程式 (推播通知無法在模擬器中運作)。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-165">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="7ff8d-166">在 iOS 應用程式 UI 中，輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-166">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="7ff8d-167">這些可以是任何字串，但兩個必須是相同的字串值。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-167">These can be any string, but they must both be the same string value.</span></span> <span data-ttu-id="7ff8d-168">然後按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="7ff8d-169">您應該會看到註冊成功的快顯通知。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="7ff8d-170">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="7ff8d-171">在 **收件者使用者名稱標記* 文字欄位中，輸入從其他裝置註冊時搭配使用的使用者名稱標記。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-171">In the **Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="7ff8d-172">輸入通知訊息並按一下 [ **傳送通知**]。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="7ff8d-173">只有已經使用收件者使用者名稱標記註冊的裝置才會收到通知訊息。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-173">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span>  <span data-ttu-id="7ff8d-174">通知訊息只會傳送給那些使用者。</span><span class="sxs-lookup"><span data-stu-id="7ff8d-174">It is only sent to those users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
