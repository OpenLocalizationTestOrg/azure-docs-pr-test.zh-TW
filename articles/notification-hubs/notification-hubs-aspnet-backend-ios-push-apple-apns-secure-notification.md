---
title: "aaaAzure 集線器安全推播通知"
description: "了解如何安全 toosend 推播通知 tooan iOS 應用程式從 Azure。 程式碼範例是以 Objective-C 及 C# 撰寫。"
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
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure 通知中心安全推播
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>概觀
在 Microsoft Azure 推播通知支援可讓您 tooaccess 方便使用、 多平台、 向外延展的推播基礎結構，可大幅簡化 hello 實作消費者和企業行動應用程式的應用程式的推播通知平台。

有時候 tooregulatory 或安全性條件約束，因為應用程式可能會想 tooinclude 中無法透過 hello 標準的推播通知基礎結構傳送的 hello 通知。 本教學課程描述 tooachieve 如何透過 hello 用戶端裝置與 hello 應用程式後端之間的安全、 已驗證連線的機密資訊傳送 hello 相同的體驗。

在高層級，hello 流程如下所示：

1. hello 應用程式後端：
   * 在後端資料庫中儲存安全裝載。
   * 會傳送 hello （傳送不安全的資訊） 此通知 toohello 裝置識別碼。
2. hello 在裝置上，當收到 hello 通知 hello 應用程式：
   * hello 裝置會連絡 hello 後端要求 hello 安全內容。
   * hello 應用程式可以顯示 hello 裝載為 hello 裝置上的通知。

請務必 toonote hello 上述流程中 （並在本教學課程），我們會假設該 hello 裝置會儲存在本機儲存體，驗證語彙基元之後 hello 使用者登入。 這樣可保證完全完美無瑕的體驗，如 hello 裝置可以擷取 hello 通知安全裝載使用這個語彙基元。 如果您的應用程式不會儲存驗證語彙基元 hello 在裝置上，或可以過期這些語彙基元，hello 裝置的應用程式，並收到 hello 通知應該會顯示提示 hello 使用者 toolaunch hello 應用程式的一般通知。 hello 應用程式然後驗證 hello 使用者，並顯示 hello 通知裝載。

此安全發送教學課程會示範如何 toosend 推播通知安全的方式。 hello 教學課程是 hello[通知使用者](notification-hubs-aspnet-backend-ios-apple-apns-notification.md)教學課程中，因此，您應該完成 hello 步驟在該教學課程中第一次。

> [!NOTE]
> 本教學課程假設您已建立並設定通知中樞，如 [開始使用通知中樞 (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)中所述。
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>修改 hello iOS 專案
既然您已修改您應用程式後端 toosend 只 hello*識別碼*的通知，您有 toochange 通知和回撥後端 tooretrieve hello 安全訊息 toobe 顯示您 iOS 應用程式 toohandle。

tooachieve 此目標中，我們有 toowrite hello 邏輯 tooretrieve hello 安全內容從 hello 應用程式後端。

1. 在**d**，請確定 hello 應用程式暫存器，無訊息的通知，以便在處理傳送嗨後端的通知識別碼 hello。 新增 hello **UIRemoteNotificationTypeNewsstandContentAvailability** didFinishLaunchingWithOptions 中的選項：
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. 在您**d** hello 頂端新增實作區段，以宣告之後的 hello:
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. 然後，加入下列程式碼，以取代 hello 預留位置 hello 實作區段 hello`{back-end endpoint}`與後端先前取得的 hello 端點：

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

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. 現在我們有 toohandle hello 內送通知，並利用上述 tooretrieve hello 內容 toodisplay hello 方法。 首先，我們有 tooenable 您的 iOS 應用程式 toorun hello 背景中接收推播通知時。 在**XCode**，選取應用程式專案 hello 左面板中，然後按一下您主要的應用程式中的目標 hello**目標**hello 中央窗格中的區段。
2. 然後按一下您**功能**hello 頂端中央窗格中，在索引標籤，並檢查 hello**遠端通知**核取方塊。
   
    ![][IOS1]
3. 在**d**新增下列方法 toohandle 推播通知的 hello:
   
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
   
    請注意，它比 toohandle hello 情況下，缺少驗證標頭屬性或 hello 後端拒絕動作。 hello 特定處理這些情況通常取決於您目標的使用者經驗。 其中一個選項是 toodisplay hello 使用者 tooauthenticate tooretrieve hello 實際通知的一般提示字元之下一則通知。

## <a name="run-hello-application"></a>執行 hello 應用程式
toorun hello 應用程式中，執行下列 hello:

1. 在 XCode 中，hello 應用程式實體 iOS 裝置上執行 (push 通知將無法運作 hello 模擬器中)。
2. 在 hello iOS 應用程式 UI 中輸入使用者名稱和密碼。 這些可以是任何字串，但它們必須 hello 相同的值。
3. 在 hello iOS 應用程式 UI 中按一下**登入**。 然後按一下 [傳送推播] 。 您應該會看到顯示在通知中心中的 hello 安全通知。

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
