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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Azure 通知中樞透過 .NET 後端通知 iOS 使用者
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>概觀
在 Azure 中的推播通知支援可讓您 tooaccess 方便使用、 多平台，並向外延展推播基礎結構，可大幅簡化 hello 實作消費者和企業行動應用程式的應用程式的推播通知平台。 本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooa 特定的應用程式使用者在特定的裝置上。 ASP.NET WebAPI 後端使用的 tooauthenticate 用戶端和 toogenerate 通知中所示 hello 指引主題[從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)。

> [!NOTE]
> 本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)中所述。 本教學課程也是 hello 必要條件 toohello[安全 Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)教學課程。
> 如果您想 toouse 行動應用程式做為後端服務時，請參閱 hello[行動應用程式開始使用推播](../app-service-mobile/app-service-mobile-ios-get-started-push.md)。
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>修改您的 iOS 應用程式
1. 開啟 hello 單一頁面檢視應用程式建立 hello[開始使用通知中心 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)教學課程。
   
   > [!NOTE]
   > 在本節中，我們假設您已使用空白組織名稱設定您的專案。 如果沒有，您將需要 tooprepend 組織名稱 tooall 類別名稱。
   > 
   > 
2. 在您 Main.storyboard 加入顯示 hello 以下螢幕擷取畫面來自 hello 物件程式庫中的 hello 元件。
   
    ![][1]
   
   * **使用者名稱**： 與預留位置文字，UITextField*輸入使用者名稱*，立即下方 hello 傳送結果標籤和受條件約束的 toohello 左和右邊界和下 hello 傳送結果的標籤。
   * **密碼**: UITextField 與預留位置文字，*輸入密碼*、 立即下方 hello username 文字欄位和受條件約束的 toohello 左和右邊界和下 hello 使用者名稱的文字欄位。 檢查 hello**安全文字項目**底下選項中 hello 屬性偵測器，*傳回金鑰*。
   * **登入**: UIButton 標記為立即 hello 密碼文字欄位下方，然後取消選取 hello**啟用**底下選項中 hello 屬性偵測器，*控制項內容*
   * **WNS**： 標籤和交換器 tooenable 傳送 hello 通知 Windows 通知服務是否已遭 hello 集線器上的安裝程式。 請參閱 hello [Windows 入門](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)教學課程。
   * **GCM**： 標籤和交換器 tooenable 傳送 hello 通知 tooGoogle Cloud Messaging 如果已經過 hello 集線器上的安裝程式。 請參閱 [Android 入門](notification-hubs-android-push-notification-google-gcm-get-started.md) 教學課程。
   * **APNS**： 標籤和交換器 tooenable 傳送 hello 通知 toohello Apple 平台通知服務。
   * **Recipent Username**: UITextField 與預留位置文字，*收件者的使用者名稱標記*、 立即下方 hello GCM 標籤，以及限制的 toohello 左右邊界和下 hello GCM 標籤。

    某些元件已加入在 hello[開始使用通知中心 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)教學課程。

1. **Ctrl**拖曳 hello 檢視 tooViewController.h 中的 hello 元件，並加入這些新的插座。
   
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
2. 在 ViewController.h，加入 hello 下列`#define`您匯入陳述式正下方。 替代 hello *< 輸入後端端點\>*預留位置 hello 使用 toodeploy 您應用程式後端 hello 前一節中的目的地 URL。 例如，*http://you_backend.azurewebsites.net*。
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. 在您的專案，建立新**Cocoa 觸控類別**名為**RegisterClient** toointerface 以 hello ASP.NET 後端所建立。 建立 hello 類別繼承自`NSObject`。 然後加入下列程式碼中 hello RegisterClient.h hello。
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. 在 hello RegisterClient.m 更新 hello `@interface` > 一節：
   
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
5. 取代 hello `@implementation` hello RegisterClient.m 以下列程式碼的 hello > 一節。

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

    上述程式碼 hello 實作 hello 指引文件所述的 hello 邏輯[從您的應用程式後端註冊](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)使用 NSURLSession tooperform REST 呼叫 tooyour 應用程式後端和 NSUserDefaults toolocally 存放區 helloregistrationId 傳回 hello 通知中樞。

    請注意，這個類別會要求其屬性**authorizationHeader** toobe 順序 toowork 中正確設定。 這個屬性設定的 hello **ViewController**類別之後 hello 登入。

1. 在 ViewController.h 中，為 RegisterClient.h 新增 `#import` 陳述式。 然後加入 hello 裝置權杖的宣告，並參考 tooa `RegisterClient` hello 中的執行個體`@interface`> 一節：
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. 在 ViewController.m，加入私用方法宣告中 hello `@interface` > 一節：
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> hello 下列程式碼片段是不安全的驗證配置，則應該取代 hello hello 實作**createAndSetAuthenticationHeaderWithUsername:AndPassword:**與特定的驗證機制如此會產生供 hello 註冊用戶端類別，例如 OAuth、 Active Directory 驗證語彙基元 toobe。
> 
> 

1. 接著在 hello `@implementation` ViewController.m 區段新增下列程式碼，這會將設定 hello 裝置權杖並驗證標頭的 hello 實作的 hello。
   
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
   
    請注意如何設定 hello 裝置權杖讓 hello 登入 按鈕。 這是因為 hello 檢視控制器註冊推播通知與 hello 應用程式後端 hello 登入動作的一部分。 因此，我們不會希望動作 toobe 登入存取直到 hello 裝置權杖已正確設定。 只要 hello 前者會發生後者 hello 之前，可以分離與 hello 推播註冊的 hello 登入。
2. 在 ViewController.m，使用下列程式碼片段 tooimplement hello 動作方法的 hello 您**登入**按鈕和方法 toosend hello 通知訊息使用 hello ASP.NET 後端。
   
       - (IBAction)LogInAction: (id) 寄件者 {/ / 建立驗證標頭，並將其設定中註冊用戶端 NSString * 使用者名稱 = 本身。UsernameField.text;  NSString * 密碼 = 本身。PasswordField.text;
   
           [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie = 本身;  [self.registerClient registerWithDeviceToken:self.deviceToken 標記： nil andCompletion:^(NSError* error){如果 (！ 錯誤) {dispatch_async(dispatch_get_main_queue()，^ {selfie。SendNotificationButton.enabled = YES;              [self MessageBox:@"Success"message:@"Registered 成功 ！"];});}}]。}

        - (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];

            傳遞做為參數與 hello REST URL toohello ASP.NET 後端 NSURL * requestURL hello pns 和使用者名稱標記 = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications？ pns = %@ （& s) to_tag = %@"，BACKEND_ENDPOINT pns、 usernameTag]];

            NSMutableURLRequest * 要求 = [NSMutableURLRequest requestWithURL:requestURL];   [要求 setHTTPMethod:@"POST"]。

            收到 hello 模擬或 authenticationheader hello 註冊用戶端 NSString * authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@"，self.registerClient.authenticationHeader];   [要求 setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"]。

            新增 hello 通知訊息主體 [要求 setValue:@"application/json;charset=utf-8"forHTTPHeaderField:@"Content-Type"]。   [要求 setHTTPBody: [訊息 dataUsingEncoding:NSUTF8StringEncoding]]。

            執行 hello 傳送通知 REST API 上 hello ASP.NET 後端 NSURLSessionDataTask * dataTask = [工作階段 dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *錯誤） {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) 回應。       如果 (錯誤 | | httpResponse.statusCode ！ = 200) {NSString*狀態 = [%NSString stringWithFormat:@"Error 狀態 @: %d\nerror: %@\n"，pns，httpResponse.statusCode、 錯誤]。           dispatch_async(dispatch_get_main_queue()，^ {/ / 附加文字，因為所有 3 PNS 呼叫可能也會有資訊 tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]]。           });           NSLog(status);       }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask resume]; }


1. 更新 hello 的 hello 動作**傳送通知**按鈕 toouse hello ASP.NET 後端和傳送 tooany PNS 啟用參數。

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



1. 函式中**ViewDidLoad**、 加入 hello 遵循 tooinstantiate hello RegisterClient 執行個體，並將設定文字欄位的 hello 委派。
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. 此時**d**，移除所有 hello 內容 hello 方法**應用程式： didRegisterForPushNotificationWithDeviceToken:**並取代 hello 檢視，確定下列 toomake hello控制器包含 hello APNs 從擷取最新裝置權杖：
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. 最後在**d**，請確定您擁有 hello 下列方法：
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>測試 hello 應用程式
1. 在 XCode 中，hello 應用程式實體 iOS 裝置上執行 (push 通知將無法運作 hello 模擬器中)。
2. 在 hello iOS 應用程式 UI 中輸入使用者名稱和密碼。 這些可以是任何字串，但兩者都是 hello 相同的字串值。 然後按一下 [ **登入**]。
   
    ![][2]
3. 您應該會看到註冊成功的快顯通知。 按一下 [確定] 。
   
    ![][3]
4. 在 hello **收件者的使用者名稱標記*文字欄位中，輸入 hello 從另一個裝置 hello 註冊搭配使用的使用者名稱標記。
5. 輸入通知訊息並按一下 [ **傳送通知**]。  僅限 hello 擁有 hello 收件者的使用者名稱標記的已註冊的裝置收到 hello 通知訊息。  它只會傳送 toothose 使用者。
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
