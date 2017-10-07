---
title: "與 Azure 通知中心 aaaSending 推播通知 tooiOS |Microsoft 文件"
description: "在此教學課程中，您學會如何 toouse Azure 通知中樞 toosend 推播通知 tooan iOS 應用程式。"
services: notification-hubs
documentationcenter: ios
keywords: "推播通知,推播通知,ios 推播通知"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a>使用 Azure 通知中樞傳送推播通知 tooiOS
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>概觀
> [!NOTE]
> toocomplete 本教學課程中，您必須擁有有效的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started)。
> 
> 

本教學課程會示範如何 toouse Azure 通知中樞 toosend 推播通知 tooan iOS 應用程式。 您將建立空白 iOS 應用程式透過使用 hello 接收推播通知[Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html)。 

完成之後，您應該能夠 toouse 您的通知中樞 toobroadcast 推播通知 tooall hello 裝置執行您的應用程式。

## <a name="before-you-begin"></a>開始之前
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

此教學課程中的 hello 完成程式碼可以找到[GitHub 上](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted)。 

## <a name="prerequisites"></a>必要條件
本教學課程必須 hello 下列需求：

* [行動服務 iOS SDK 版本 1.2.4]
* 最新版的 [Xcode]
* 支援 iOS 8 (或更新版本) 的裝置
* [Apple Developer Program](https://developer.apple.com/programs/) 成員資格。
  
  > [!NOTE]
  > 由於推播通知的設定需求，您必須部署並測試實體 iOS 裝置 （iPhone 或 iPad） 上的推播通知，而不是 hello iOS 模擬器。
  > 
  > 

完成本教學課程是參加 iOS app 所有其他通知中樞教學課程的先決條件。

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a>針對 iOS 推播通知設定您的通知中樞
本節將引導您建立新的通知中樞及與使用 hello APNS 設定驗證**.p12**您所建立的推播憑證。 如果您想 toouse 您已經建立通知中樞，您可以略過 toostep 5。

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p>按一下 hello <b>Notification Services</b>按鈕在 hello<b>設定</b>刀鋒視窗中，然後選取<b>Apple (APNS)</b>。 按一下<b>上傳憑證</b>和選取 hello <b>.p12</b>您稍早匯出的檔案。 請確定您也可以指定 hello 正確的密碼。</p>

<p>請確定 tooselect<b>沙箱</b>模式，因為這是進行開發。 只使用 hello<b>生產</b>如果您想 toosend 推播通知 toousers 購買您的應用程式從 hello 存放區。</p>
</li>
</ol>
&emsp;&emsp;&emsp;&emsp;![在 Azure 入口網站中設定 APNS](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)

&emsp;&emsp;&emsp;&emsp;![在 Azure 入口網站中設定 APNS 憑證](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

您的通知中樞現在是設定的 toowork 使用 APNS，而且您擁有 hello 連接字串 tooregister 您的應用程式，並傳送推播通知。

## <a name="connect-your-ios-app-toonotification-hubs"></a>連接您的 iOS 應用程式 tooNotification 集線器
1. 在 Xcode 中，建立新的 iOS 專案，並選取 hello**單一檢視應用程式**範本。
   
    ![Xcode - 單一檢視應用程式][8]
    
2. 當設定為新專案的 hello 選項，請確定 toouse hello 相同**產品名稱**和**組織識別碼**時您先前為設定 hello 套件組合識別碼 hello Apple 開發人員使用入口網站。
   
    ![Xcode - 專案選項][11]
    
3. 下**目標**，按一下您的專案名稱，按一下 hello**組建設定**索引標籤上，展開 **程式碼簽署識別**，然後在**偵錯**，設定您的程式碼簽署識別。 切換**層級**從**基本**太**所有**，並設定**佈建設定檔**toohello 佈建您先前建立的設定檔.
   
    如果您沒有看到 hello 新佈建在 Xcode 中所建立的設定檔，請嘗試重新整理您的簽署識別的 hello 設定檔。 按一下**Xcode** hello 功能表列上，按一下 [**喜好設定**，按一下 hello**帳戶**索引標籤上，按一下 hello**檢視詳細資料**按鈕上，按一下您簽署身分識別，然後按一下hello 右下角 hello 重新整理] 按鈕。
   
    ![Xcode - 佈建設定檔][9]
4. 下載 hello[行動服務 iOS SDK 版本 1.2.4]並解壓縮 hello 檔案。 在 Xcode 中，以滑鼠右鍵按一下您的專案，按一下 hello**將檔案新增至**選項 tooadd hello **WindowsAzureMessaging.framework**資料夾 tooyour Xcode 專案。 選取 必要時複製項目，然後按一下新增。
   
   > [!NOTE]
   > hello 通知中樞 SDK 目前不支援 bitcode Xcode 7 上。  您必須設定**啟用 Bitcode**太**否**在 hello**建置選項**為您的專案。
   > 
   > 
   
    ![解壓縮 Azure SDK][10]
5. 新標頭檔 tooyour 將專案加入名為`HubInfo.h`。 這個檔案會保留您的通知中樞的 hello 常數。  新增下列定義 hello 和 hello 與字串常值預留位置取代您*中樞名稱*和 hello *DefaultListenSharedAccessSignature*您先前記下。
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. 開啟您`AppDelegate.h`檔案新增下列 import 指示詞的 hello:
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. 在您`AppDelegate.m file`，加入下列程式碼中 hello hello`didFinishLaunchingWithOptions`方法會根據您的 iOS 版本。 此程式碼會向 APN 註冊裝置控制代碼：
   
    對於 iOS 8：
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    針對 iOS 版本先前 too8:
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. 在 hello 同一個檔案中新增下列方法 hello。 此程式碼會連接 toohello 通知中樞使用 hello HubInfo.h 中所指定的連接資訊。 它接著會給予發生 hello 裝置權杖 toohello 通知中樞讓 hello 通知中樞可以傳送通知：
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. 在 hello 同一個檔案中新增下列方法 toodisplay hello **UIAlert**如果 hello 應用程式作用中時，會收到 hello 通知：

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. 建置並執行您不有任何失敗的裝置 tooverify 上 hello 應用程式。

## <a name="send-test-push-notifications"></a>傳送測試推播通知
您可以測試應用程式中接收通知，傳送推播通知給 hello 以[Azure 入口網站]透過 hello**疑難排解**hello 中樞刀鋒視窗中的區段 (使用 hello*測試傳送*選項)。

![Azure 入口網站 - 測試傳送][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a>（選擇性）從 hello 應用程式中傳送推播通知
> [!IMPORTANT]
> 基於學習的目的只提供這個範例的 hello 用戶端應用程式從傳送通知。 因為這將需要 hello `DefaultFullSharedAccessSignature` toobe 在於 hello 用戶端應用程式，它會公開使用者會獲得存取未經授權的 toosend 通知 tooyour 用戶端通知中樞 toohello 風險。
> 
> 

如果您想 toosend 推播通知從應用程式中的，本節提供如何的範例 toodo 此使用 hello REST 介面。

1. 在 Xcode 中，開啟`Main.storyboard`和新增 hello hello 物件程式庫 tooallow hello 使用者 toosend 推播通知 hello 應用程式中的下列 UI 元件：
   
   * 沒有標籤文字的標籤。 它將會使用的 tooreport 傳送通知的錯誤。 hello**行**屬性應該設定太**0** ，讓它將會自動調整的大小限制的 toohello 右邊和左邊的界和 hello hello 檢視的頂端。
   * 文字欄位與**預留位置**太設定文字**輸入通知訊息**。 限制 hello hello 標籤，如下所示的正下方的欄位。 將 hello 檢視控制站設定為 hello 插座委派。
   * 標題按鈕**傳送通知**限制 hello 文字欄位的正下方且在 hello 水平置中。
     
     hello 檢視應如下所示：
     
     ![Xcode 設計工具][32]
2. [新增插座](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html)hello 標籤和文字欄位已連接您的檢視，並更新您`interface`定義 toosupport`UITextFieldDelegate`和`NSXMLParserDelegate`。 新增 hello toohelp 支援呼叫 REST API hello 和剖析 hello 回應如下所示三個屬性宣告。
   
    您的 ViewController.h 檔案應該類似下列內容：
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. 開啟`HubInfo.h`並新增下列常數用於傳送通知 tooyour 中樞 hello。 以您實際取代預留位置字串常值 hello *DefaultFullSharedAccessSignature*連接字串。
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. 新增下列 hello`#import`陳述式 tooyour`ViewController.h`檔案。
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. 在`ViewController.m`新增下列程式碼 toohello 介面實作的 hello。 此程式碼將會剖析您的 *DefaultFullSharedAccessSignature* 連接字串。 Hello 中所述[REST API 參考](http://msdn.microsoft.com/library/azure/dn495627.aspx)，這個已剖析的資訊將會使用的 toogenerate hello 的 SaS token**授權**要求標頭。
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. 在`ViewController.m`，更新 hello`viewDidLoad`方法 tooparse hello 連接字串 hello 檢視載入時。 也新增 hello 公用程式方法，如下所示 toohello 介面實作。  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. 在`ViewController.m`，加入下列程式碼 toohello 介面實作 toogenerate hello SaS 授權權杖，而將提供在 hello hello**授權**標頭，hello 中所述[REST API參考](http://msdn.microsoft.com/library/azure/dn495627.aspx)。
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. Ctrl + 拖曳從 hello**傳送通知**太按鈕`ViewController.m`tooadd 名為動作**SendNotificationMessage** hello**觸控向**事件。 下列程式碼 toosend hello 通知使用 hello REST API 的 hello 與更新方法。
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. 在`ViewController.m`，加入下列委派方法 toosupport 關閉 hello 文字欄位的 hello 鍵盤 hello。 Ctrl + 拖曳從 hello 文字欄位 toohello 檢視控制器中圖示 hello 介面設計工具 tooset hello 檢視控制站與 hello 插座委派。
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. 在`ViewController.m`，加入下列 hello 使用委派方法 toosupport 剖析 hello 回應`NSXMLParser`。
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. 建置 hello 專案並確認沒有任何錯誤。

> [!NOTE]
> 如果您遇到有關 bitcode 支援 Xcode7 中的建置錯誤，您應該變更 hello**組建設定** > **啟用 Bitcode (ENABLE_BITCODE)**太**否**在 Xcode 中。 hello 通知中樞 SDK 目前不支援 bitcode。 
> 
> 

您可以在 hello Apple 找到所有 hello 可能通知裝載[本機和推播通知程式設計指南]。

## <a name="checking-if-your-app-can-receive-push-notifications"></a>檢查您的應用程式是否可接收推播通知
在 iOS 上的 tootest 推播通知，您必須部署 hello 應用程式 tooa 實體 iOS 裝置。 您無法使用 hello iOS 模擬器來傳送 Apple 推播通知。

1. 執行 hello 應用程式，並確認登錄成功，然後按下**確定**。
   
    ![iOS 應用程式推播通知註冊測試][33]
2. 您可以傳送測試推播通知從 hello [Azure 入口網站]，如上面所述。 如果您加入程式碼，以便在 hello 應用程式中傳送推播通知，觸控內 hello 文字欄位 tooenter 通知訊息。 然後按 hello**傳送**hello 鍵盤或 hello 按鈕**傳送通知**hello 檢視 toosend hello 通知訊息中的按鈕。
   
    ![iOS 應用程式推播通知傳送測試][34]
3. hello 推播通知傳送 tooall 的裝置已註冊的 tooreceive hello 通知 hello 特定通知中樞。
   
    ![iOS 應用程式推播通知接收測試][35]

## <a name="next-steps"></a>後續步驟
在這個簡單的範例中，您傳播推播通知 tooall 已註冊的 iOS 裝置。 我們建議您繼續 toohello 您了解下一個步驟[Azure 通知中樞通知使用者與.NET 後端 ios]教學課程，將引導您完成建立後端 toosend 推播通知使用標記。 

如果您想 toosegment 您感興趣群組的使用者，您可以另外將移 toohello[使用通知中樞 toosend 最新消息]教學課程。 

如需有關通知中樞的一般資訊，請參閱 [通知中樞指引]。

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[行動服務 iOS SDK 版本 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[通知中樞指引]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure 通知中樞通知使用者與.NET 後端 ios]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[使用通知中樞 toosend 最新消息]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[本機和推播通知程式設計指南]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure 入口網站]: https://portal.azure.com
