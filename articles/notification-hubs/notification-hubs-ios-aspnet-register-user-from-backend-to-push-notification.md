---
title: "使用 Web API 的推播通知的 aaaRegister hello 目前使用者 |Microsoft 文件"
description: "了解如何 toorequest 推播通知登錄中 iOS 應用程式與 Azure 通知中心時登錄由 ASP.NET Web API。"
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
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>使用 ASP.NET 註冊 hello 目前使用者的推播通知
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>概觀
本主題說明如何 toorequest 推播通知登錄了 Azure 通知中心註冊由 ASP.NET Web API 時。 本主題會延伸 hello 教學課程[向使用者通知中樞通知]。 必須完成 該教學課程 toocreate hello 驗證行動服務中的 hello 必要步驟。 如需 hello 通知使用者案例，請參閱 <<c0> [向使用者通知中樞通知]。

## <a name="update-your-app"></a>更新應用程式
1. 在您 MainStoryboard_iPhone.storyboard 加入 hello hello 物件程式庫中的下列元件：
   
   * **標籤**: 「 推入 tooUser 與通知中心 」
   * **標籤**：「安裝 ID」
   * **標籤**：「使用者」
   * **文字欄位**：「使用者」
   * **標籤**：「密碼」
   * **文字欄位**：「密碼」
   * **按鈕**：「登入」
     
     此時，將分鏡腳本看起來像下列 hello:
     
      ![][0]
2. 在 hello 助理編輯器中，建立所有 hello 切換控制項插座及呼叫它們，連接 hello 文字欄位以 hello 檢視控制器 （委派），並建立**動作**hello**登入** 按鈕。
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. 建立一個名為**DeviceInfo**，並複製 hello 遵循程式碼插入 hello 檔 DeviceInfo.h hello 介面區段：
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. 複製下列程式碼 hello DeviceInfo.m 檔案 hello 實作區段中的 hello:
   
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
   
                    //store hello install ID so we don't generate a new one next time
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
5. 在 PushToUserAppDelegate.h，加入下列屬性的單一 hello:
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. 在 hello **didFinishLaunchingWithOptions** PushToUserAppDelegate.m，在方法中加入下列程式碼的 hello:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    hello 第一行會初始化 hello **DeviceInfo** singleton。 hello 第二個列啟動 hello 註冊推播通知已存在於這是您已經完成 hello[開始使用通知中樞]教學課程。
7. 在 PushToUserAppDelegate.m，實作 hello 方法**didRegisterForRemoteNotificationsWithDeviceToken**中您 AppDelegate 並加入下列程式碼的 hello:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    這會設定為 hello 要求 hello 裝置權杖。
   
   > [!NOTE]
   > 此時，此方法中不應有任何其他程式碼。 如果您已經有呼叫 toohello **registerNativeWithDeviceToken**完成 hello 時所加入的方法[開始使用通知中樞](/manage/services/notification-hubs/get-started-notification-hubs-ios/)教學課程，您必須向外註解或移除，呼叫。
   > 
   > 
8. 在 hello PushToUserAppDelegate.m 檔案中，加入下列處理常式方法的 hello:
   
   * (void) 的應用程式:(UIApplication *) 應用程式 didReceiveRemoteNotification:(NSDictionary *) 避 {NSLog (@"%@"，所以);  UIAlertView * 警示 = [[UIAlertView 配置] initWithTitle:@"Notification 」 訊息: [使用者資訊 objectForKey:@"inAppMessage]"委派： nil cancelButtonTitle: @"OK"otherButtonTitles:nil、 nil];  [警示顯示]。}
   
   您的應用程式執行時，收到通知時，這個方法會顯示警示 hello UI 中。
9. 開啟 hello PushToUserViewController.m 檔案，並傳回 hello 鍵盤在 hello 下列實作：
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. 在 hello **viewDidLoad** hello PushToUserViewController.m 檔案中的方法初始化 hello installationId 標籤，如下所示：
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. 加入下列屬性介面中 PushToUserViewController.m hello:
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. 然後，加入下列實作 hello:
    
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
13. 複製 hello 下列程式碼到 hello**登入**XCode 所建立的處理常式方法：
    
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
    
    這個方法會取得同時安裝識別碼和通道的推播通知，並將它，傳送 hello 裝置類型以及，toohello 驗證 Web 應用程式開發介面方法，在通知中樞建立註冊。 此 Web API 定義於[向使用者通知中樞通知]中。

既然 hello 已更新用戶端應用程式，則傳回 toohello[向使用者通知中樞通知]和 hello 行動服務 toosend 通知使用更新的通知中樞。

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[向使用者通知中樞通知]: /manage/services/notification-hubs/notify-users-aspnet

[開始使用通知中樞]: /manage/services/notification-hubs/get-started-notification-hubs-ios
