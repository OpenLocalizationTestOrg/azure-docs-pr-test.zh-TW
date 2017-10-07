---
title: "使用原生 Mobile Engagement iOS SDK aaaBridge iOS WebView"
description: "描述如何 toocreate WebView 執行 Javascript 和 hello 原生 Mobile Engagement iOS SDK 之間的橋接器"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: e1d6ff6f-cd67-4131-96eb-c3d6318de752
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 089ed8484722cb5ba624e5dce0e670ab56de514d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a>將 iOS WebView 與原生 Mobile Engagement iOS SDK 橋接
> [!div class="op_single_selector"]
> * [Android 橋接器](mobile-engagement-bridge-webview-native-android.md)
> * [iOS 橋接器](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

某些行動裝置應用程式被設計為混合式應用程式本身 hello 應用程式開發時使用原生 iOS Objective C 程式開發，但是部分或甚至全部 hello 螢幕 iOS WebView 中轉譯。 您仍然可以使用這類應用程式內的 Mobile Engagement iOS SDK，並在本教學課程說明如何 toogo 如何進行此作業。 

有兩個方法 tooachieve 這兩者都未記載：

* 第一種方法是此[連結](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip)中所描述，牽涉到在您的網頁檢視上註冊 `UIWebViewDelegate`，然後以 Javascript「捕捉並立即取消」位置變更來完成。 
* 第二個其中根據這[WWDC 2013 工作階段](https://developer.apple.com/videos/play/wwdc2013/615)，這就是第一次清潔比 hello，和我們會遵循本指南中的方法。 請注意，這個方法僅適用於 iOS7 和更新版本。 

針對 hello iOS 橋接的範例，請遵循下列 hello 步驟：

1. 首先，您必須已經完成的 tooensure 我們[快速入門教學課程](mobile-engagement-ios-get-started.md)toointegrate hello Mobile Engagement iOS SDK 混合式應用程式中。 （選擇性） 您也可以啟用，讓您可以查看 hello SDK 方法，當我們從 hello webview 觸發這些測試記錄，如下所示。 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. 現在請確定您的混合式應用程式上有使用 WebView 的畫面。 您可以將它加入 toohello `Main.storyboard` hello 應用程式。 
3. 關聯與此 webview 您**ViewController**按一下並拖曳 hello webview 從 hello 檢視控制器場景 toohello`ViewController.h`編輯畫面上，將其放在正下方 hello`@interface`列。 
4. 您這麼做之後，對話方塊隨即會出現要求輸入名稱。 提供與 hello 名稱**webView**。 您`ViewController.h`檔案應該看起來像下列 hello:
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. 我們將會更新 hello`ViewController.m`稍後檔案，但首先我們要建立 hello 橋接器檔案會透過某些常用的 Mobile Engagement iOS SDK 方法建立包裝函式。 建立新的標頭檔稱為**EngagementJsExports.h**使用 hello `JSExport` hello 上述中所述的機制[工作階段](https://developer.apple.com/videos/play/wwdc2013/615)tooexpose hello 原生 iOS 方法。 
   
        #import <Foundation/Foundation.h>
        #import <JavaScriptCore/JavascriptCore.h>
   
        @protocol EngagementJsExports <JSExport>
   
        + (void) sendEngagementEvent:(NSString*) name :(NSString*)extras;
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras;
        + (void) endEngagementJob:(NSString*) name;
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras;
        + (void) sendEngagementAppInfo:(NSString*) appInfo;
   
        @end
   
        @interface EngagementJs : NSObject <EngagementJsExports>
   
        @end
6. 接下來，我們將建立 hello hello 橋接器檔第二個部分。 建立一個叫做檔案**EngagementJsExports.m**其中會包含 hello 建立 hello 實際的包裝函式，藉由呼叫 hello Mobile Engagement iOS SDK 方法的實作。 另外請注意，我們正在剖析 hello`extras`收到所傳遞的 hello webview javascript 並放入`NSMutableDictionary`物件 toobe 傳遞以 hello Engagement SDK 方法呼叫。  
   
        #import <UIKit/UIKit.h>
        #import "EngagementAgent.h"
        #import "EngagementJsExports.h"
   
        @implementation EngagementJs
   
        +(void) sendEngagementEvent:(NSString*)name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendEvent:name extras:extrasInput];
        }
   
        + (void) startEngagementJob:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] startJob:name extras:extrasInput];
        }
   
        + (void) endEngagementJob:(NSString*) name {
           [[EngagementAgent shared] endJob:name];
        }
   
        + (void) sendEngagementError:(NSString*) name :(NSString*)extras {
           NSMutableDictionary* extrasInput = [self ParseExtras:extras];
           [[EngagementAgent shared] sendError:name extras:extrasInput];
        }
   
        + (void) sendEngagementAppInfo:(NSString*) appInfo {
           NSMutableDictionary* appInfoInput = [self ParseExtras:appInfo];
           [[EngagementAgent shared] sendAppInfo:appInfoInput];
        }
   
        + (NSMutableDictionary*) ParseExtras:(NSString*) input {
           NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
           NSError* error = nil;
           NSMutableDictionary* extras = [NSJSONSerialization JSONObjectWithData:data options:0 error:&error];
   
           return extras;
        }
   
        @end
7. 現在我們後回來 toohello **ViewController.m**及更新以下列程式碼的 hello: 
   
        #import <JavaScriptCore/JavaScriptCore.h>
        #import "ViewController.h"
        #import "EngagementJsExports.h"
   
        @interface ViewController ()
   
        @end
   
        @implementation ViewController
   
        - (void)viewDidLoad
        {
           self.webView.delegate = self;
           [super viewDidLoad];
           [self loadWebView];
        }
   
        - (void)loadWebView {
           NSBundle* mainBundle = [NSBundle mainBundle];
           NSURL* htmlPage = [mainBundle URLForResource:@"LocalPage" withExtension:@"html"];
   
           NSURLRequest* urlReq = [NSURLRequest requestWithURL:htmlPage];
           [self.webView loadRequest:urlReq];
        }
   
        - (void)webViewDidFinishLoad:(UIWebView*)wv
        {
           JSContext* context = [wv valueForKeyPath:@"documentView.webView.mainFrame.javaScriptContext"];
   
           context[@"EngagementJs"] = [EngagementJs class];
        }
   
        - (void)webView:(UIWebView*)wv didFailLoadWithError:(NSError*)error
        {
           NSLog(@"Error for WEBVIEW: %@", [error description]);
        }
   
        - (void)didReceiveMemoryWarning {
           [super didReceiveMemoryWarning];
           // Dispose of any resources that can be recreated.
        }
   
        @end
8. 注意 hello 下列點有關 hello **ViewController.m**檔案：
   
   * 在 [hello`loadWebView`方法中，我們會載入本機的 HTML 檔案，稱為**LocalPage.html**接下來，我們將檢閱其程式碼。 
   * 在 [hello`webViewDidFinishLoad`方法，我們會抓取 hello`JsContext`和我們的包裝函式類別關聯。 這可讓呼叫我們的包裝函式使用 hello 控制代碼的 SDK 方法**EngagementJs** hello web 檢視。 
9. 建立一個叫做檔案**LocalPage.html**以下列程式碼的 hello:
   
        <!doctype html>
        <html>
           <head>
               <style type='text/css'>
                   html { font-family:Helvetica; color:#222; }
                   h1 { color:steelblue; font-size:22px; margin-top:16px; }
                   h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
               </style>
   
               <script type="text/javascript">
   
               window.onerror = function(err)
               {
                   alert('window.onerror: ' + err);
               }
   
               function send(inputId)
               {
                   var input = document.getElementById(inputId);
                   if(input)
                   {
                       var value = input.value;
                       // Example of how extras info can be passed with hello Engagement logs
                       var extras = '{"CustomerId":"MS290011"}';
                   }
   
                   if(value && value.length > 0)
                   {
                       switch(inputId)
                       {
                           case "event":
                           EngagementJs.sendEngagementEvent(value, extras);
                           break;
   
                           case "job":
                           EngagementJs.startEngagementJob(value, extras);
                           window.setTimeout(
                           function(){
                               EngagementJs.endEngagementJob(value);
                           }, 10000 );
                           break;
   
                           case "error":
                           EngagementJs.sendEngagementError(value, extras);
                           break;
   
                           case "appInfo":
                           var appInfo = '{"customer_name":"' + value + '"}';
                           EngagementJs.sendEngagementAppInfo(appInfo);
                           break;
                       }
                   }
               }
               </script>
   
           </head>
           <body>
               <h1>Bridge Tester</h1>
   
               <div id='engagement'>
   
                   <br/>
                   <h2>Event</h2>
                   <input type="text" id="event" size="35">
                   <button onclick="send('event')">Send</button>
   
                   <br/>
                   <h2>Job</h2>
                   <input type="text" id="job" size="35">
                   <button onclick="send('job')">Send</button>
   
                   <br/>
                   <h2>Error</h2>
                   <input type="text" id="error" size="35">
                   <button onclick="send('error')">Send</button
   
                   <br/>
                   <h2>AppInfo</h2>
                   <input type="text" id="appInfo" size="35">
                   <button onclick="send('appInfo')">Send</button>
   
               </div>
           </body>
        </html>
10. 請注意 hello 下列點有關上述的 hello HTML 檔案：
    
    * 它包含一組的輸入方塊，您可以在其中提供資料 toobe 做為事件、 工作、 錯誤、 應用程式資訊的名稱。 當您按一下 hello 按鈕的下一個 tooit 時，進行呼叫，toohello Javascript 最後呼叫 hello 方法從 hello 橋接器檔案 toopass 此呼叫 toohello Mobile Engagement iOS SDK。 
    * 我們會標記上一些額外的靜態資訊 toohello 事件、 工作以及甚至錯誤 toodemonstrate 如何這無法完成。 此額外資訊則會傳送 JSON 字串，若您查看 hello`EngagementJsExports.m`檔案、 剖析和傳送事件、 工作、 錯誤以及傳遞。 
    * Mobile Engagement 工作會開始使用您指定在 hello 輸入方塊中，執行 10 秒，並關閉 hello 名稱。 
    * Mobile Engagement 應用程式資訊或標籤與一起傳遞 'customer_name' hello 靜態金鑰以及 hello 值中輸入的 hello 輸入 hello 值為 hello 標記。 
11. 執行的 hello 應用程式，您會看到下列 hello。 現在提供一些類似下列的 hello 測試事件的名稱，然後按一下 [**傳送**tooit 下一步]。 
    
     ![][1]
12. 現在，如果您移 toohello**監視器**] 索引標籤的 [應用程式，並查看**事件詳細資料]-> [**，您會看到顯示以及 hello 靜態應用程式的資訊，我們會傳送此事件。 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
