---
title: "aaaNotification 集線器當地語系化重大新聞教學課程適用於 iOS"
description: "了解如何 toouse Azure Service Bus 通知中樞 toosend 當地語系化重大消息通知 (iOS)。"
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>使用通知中樞 toosend 當地語系化重大消息 tooiOS 裝置
> [!div class="op_single_selector"]
> * [Windows 市集 C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>概觀
本主題說明如何 toouse hello[範本](notification-hubs-templates-cross-platform-push-messages.md)Azure 通知中樞 toobroadcast 重大消息通知已當地語系化的語言和裝置的功能。 在本教學課程就開始 hello iOS 應用程式中建立[使用通知中樞 toosend 最新消息]。 完成時，您將會為您感興趣的類別可以 tooregister，tooreceive hello 通知，在指定的語言，並接收只推播通知 hello 選取類別以該語言。

有兩個部分 toothis 案例：

* iOS 應用程式可讓用戶端裝置 toospecify 語言和 toosubscribe toodifferent 重大新聞分類。
* hello 後端廣播 hello 通知，請使用 hello**標記**和**範本**feautres Azure 通知中心。

## <a name="prerequisites"></a>必要條件
您必須已經完成 hello[使用通知中樞 toosend 最新消息]教學課程，而且有 hello 程式碼，因為本教學課程是直接在該程式碼時。

(選擇性) 需要 Visual Studio 2012 或更新版本。

## <a name="template-concepts"></a>範本概念
在[使用通知中樞 toosend 最新消息]建置的應用程式，使用**標記**toosubscribe toonotifications 不同新聞分類。
但有許多應用程式是以多個市場為目標的，因此需要當地語系化。 這表示 hello 通知會自行 hello 內容有 toobe 當地語系化，而且傳遞的 toohello 一組正確的裝置。
本主題中我們將示範如何 toouse hello**範本**tooeasily 傳遞的通知中樞的功能當地語系化重大消息通知。

注意： 其中一種方式 toosend 當地語系化通知是 toocreate 多個版本的每個標記。 比方說，toosupport 英文、 法文及中文，我們需要三個不同的標記世界新聞:"world_en"，"world_fr，"和"world_ch"。 我們必須 toosend 這些標記的 hello world 新聞 tooeach 的當地語系化的版本。 本主題中我們將會使用範本 tooavoid hello 擴散的標記以及將多個訊息傳送的 hello 需求。

在高的層級中，範本會方式 toospecify 如何特定裝置應該會收到通知。 hello 範本會指定藉由參考是由您的應用程式後端傳送 hello 訊息部分的 tooproperties hello 確切的裝載格式。 在此處的範例中，我們將傳送地區設定無從驗證、且包含所有支援語言的訊息：

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

然後我們會確保裝置註冊使用的範本，是指 toohello 正確的屬性。 比方說，iOS 應用程式的法文新聞想 tooregister 會註冊 hello 下列：

    {
        aps:{
            alert: "$(News_French)"
        }
    }

範本的功能非常強大，您可以在 [範本](notification-hubs-templates-cross-platform-push-messages.md) 一文中了解詳情。

## <a name="hello-app-user-interface"></a>hello 應用程式使用者介面
我們現在將會修改您建立 hello 主題中的 hello 即時新聞應用程式[使用通知中樞 toosend 最新消息]toosend 當地語系化使用範本的重大消息。

您 MainStoryboard_iPhone.storyboard 中新增 分割控制項與 hello 三個語言，我們將支援這些語言： 英文、 法文和中文。

![][13]

請確定 tooadd IBOutlet 中您 ViewController.h 如下所示：

![][14]

## <a name="building-hello-ios-app"></a>建置 hello iOS 應用程式
1. 在您 Notification.h 新增 hello *retrieveLocale*方法，並修改 hello 存放區和訂閱方法，如下所示：
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    在您 Notification.m 修改 hello *storeCategoriesAndSubscribe*方法，加入 hello 地區設定參數，並將其儲存在 hello 使用者預設值：
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    然後修改 hello*訂閱*方法 tooinclude hello 地區設定：
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    請注意，我們現在使用的方式 hello 方法*registerTemplateWithDeviceToken*，而不是*registerNativeWithDeviceToken*。 當我們註冊範本我們有 tooprovide hello json 範本以及 hello 範本的名稱 （如我們的應用程式可能會想 tooregister 不同的範本）。 請確定 tooregister 標記，為您分類因為我們想要這些新聞 toomake 確定 tooreceive hello notifciations。
   
    新增方法 tooretrieve hello 地區設定 hello 使用者預設值：
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. 既然我們修改通知類別時，我們有 toomake 確定我們 ViewController 可使用的 hello 新 UISegmentControl。 新增下列一行 hello hello *viewDidLoad*方法 toomake 確定 tooshow hello 地區設定目前選取：
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    然後，在您*訂閱*方法中，變更呼叫 toohello *storeCategoriesAndSubscribe* toohello 下列：
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. 最後，您有 tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken*您 d 中的方法，讓您的應用程式啟動時，您可以正確地更新您的註冊。 變更呼叫 toohello*訂閱*hello 下列通知方法：
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(選擇性) 從.NET 主控台應用程式傳送當地語系化的範本通知。
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>（選擇性）將當地語系化的範本通知從 hello 裝置傳送
如果您不具有存取 tooVisual Studio 中，或想要直接從 hello hello 裝置上的應用程式傳送嗨當地語系化範本通知 toojust 測試。  您可以簡單加入當地語系化的 hello 範本參數 toohello `SendNotificationRESTAPI` hello 上一個教學課程中所定義的方法。

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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

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




## <a name="next-steps"></a>後續步驟
如需使用範本的詳細資訊，請參閱：

* [使用通知中樞來通知使用者：ASP.NET]
* [使用通知中樞來通知使用者：行動服務]

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[使用通知中樞 toosend 最新消息]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[使用通知中樞來通知使用者：ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[使用通知中樞來通知使用者：行動服務]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
