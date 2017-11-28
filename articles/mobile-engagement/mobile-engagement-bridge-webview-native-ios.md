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
# <a name="bridge-ios-webview-with-native-mobile-engagement-ios-sdk"></a><span data-ttu-id="eb70c-103">將 iOS WebView 與原生 Mobile Engagement iOS SDK 橋接</span><span class="sxs-lookup"><span data-stu-id="eb70c-103">Bridge iOS WebView with native Mobile Engagement iOS SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb70c-104">Android 橋接器</span><span class="sxs-lookup"><span data-stu-id="eb70c-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="eb70c-105">iOS 橋接器</span><span class="sxs-lookup"><span data-stu-id="eb70c-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="eb70c-106">某些行動裝置應用程式被設計為混合式應用程式本身 hello 應用程式開發時使用原生 iOS Objective C 程式開發，但是部分或甚至全部 hello 螢幕 iOS WebView 中轉譯。</span><span class="sxs-lookup"><span data-stu-id="eb70c-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native iOS Objective-C development but some or even all of hello screens are rendered within an iOS WebView.</span></span> <span data-ttu-id="eb70c-107">您仍然可以使用這類應用程式內的 Mobile Engagement iOS SDK，並在本教學課程說明如何 toogo 如何進行此作業。</span><span class="sxs-lookup"><span data-stu-id="eb70c-107">You can still consume Mobile Engagement iOS SDK within such apps and this tutorial describes how toogo about doing this.</span></span> 

<span data-ttu-id="eb70c-108">有兩個方法 tooachieve 這兩者都未記載：</span><span class="sxs-lookup"><span data-stu-id="eb70c-108">There are two approaches tooachieve this though both are undocumented:</span></span>

* <span data-ttu-id="eb70c-109">第一種方法是此[連結](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip)中所描述，牽涉到在您的網頁檢視上註冊 `UIWebViewDelegate`，然後以 Javascript「捕捉並立即取消」位置變更來完成。</span><span class="sxs-lookup"><span data-stu-id="eb70c-109">First one is described on this [link](http://stackoverflow.com/questions/9826792/how-to-invoke-objective-c-method-from-javascript-and-send-back-data-to-javascrip) which involves registering a `UIWebViewDelegate` on your web view and catch-and-immediatly-cancel a location change done in Javascript.</span></span> 
* <span data-ttu-id="eb70c-110">第二個其中根據這[WWDC 2013 工作階段](https://developer.apple.com/videos/play/wwdc2013/615)，這就是第一次清潔比 hello，和我們會遵循本指南中的方法。</span><span class="sxs-lookup"><span data-stu-id="eb70c-110">Second one is based on this [WWDC 2013 session](https://developer.apple.com/videos/play/wwdc2013/615), an approach which is cleaner than hello first and which we will follow for this guide.</span></span> <span data-ttu-id="eb70c-111">請注意，這個方法僅適用於 iOS7 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="eb70c-111">Note that this approach only works on iOS7 and above.</span></span> 

<span data-ttu-id="eb70c-112">針對 hello iOS 橋接的範例，請遵循下列 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="eb70c-112">Follow hello steps below for hello iOS bridge sample:</span></span>

1. <span data-ttu-id="eb70c-113">首先，您必須已經完成的 tooensure 我們[快速入門教學課程](mobile-engagement-ios-get-started.md)toointegrate hello Mobile Engagement iOS SDK 混合式應用程式中。</span><span class="sxs-lookup"><span data-stu-id="eb70c-113">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-ios-get-started.md) toointegrate hello Mobile Engagement iOS SDK in your hybrid app.</span></span> <span data-ttu-id="eb70c-114">（選擇性） 您也可以啟用，讓您可以查看 hello SDK 方法，當我們從 hello webview 觸發這些測試記錄，如下所示。</span><span class="sxs-lookup"><span data-stu-id="eb70c-114">Optionally, you can also enable test logging as follows so that you can see hello SDK methods as we trigger them from hello webview.</span></span> 
   
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
           ....
             [EngagementAgent setTestLogEnabled:YES];
           ....
        }
2. <span data-ttu-id="eb70c-115">現在請確定您的混合式應用程式上有使用 WebView 的畫面。</span><span class="sxs-lookup"><span data-stu-id="eb70c-115">Now make sure that your hybrid app has a screen with a webview on it.</span></span> <span data-ttu-id="eb70c-116">您可以將它加入 toohello `Main.storyboard` hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eb70c-116">You can add it toohello `Main.storyboard` of hello app.</span></span> 
3. <span data-ttu-id="eb70c-117">關聯與此 webview 您**ViewController**按一下並拖曳 hello webview 從 hello 檢視控制器場景 toohello`ViewController.h`編輯畫面上，將其放在正下方 hello`@interface`列。</span><span class="sxs-lookup"><span data-stu-id="eb70c-117">Associate this webview with your **ViewController** by clicking and dragging hello webview from hello View Controller Scene toohello `ViewController.h` edit screen, placing it just below hello `@interface` line.</span></span> 
4. <span data-ttu-id="eb70c-118">您這麼做之後，對話方塊隨即會出現要求輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="eb70c-118">Once you do this, a dialog box will pop up asking for a name.</span></span> <span data-ttu-id="eb70c-119">提供與 hello 名稱**webView**。</span><span class="sxs-lookup"><span data-stu-id="eb70c-119">Provide hello name as **webView**.</span></span> <span data-ttu-id="eb70c-120">您`ViewController.h`檔案應該看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="eb70c-120">Your `ViewController.h` file should look like hello following:</span></span>
   
        #import <UIKit/UIKit.h>
        #import "EngagementViewController.h"
   
        @interface ViewController : EngagementViewController
        @property (strong, nonatomic) IBOutlet UIWebView *webView;
   
        @end
5. <span data-ttu-id="eb70c-121">我們將會更新 hello`ViewController.m`稍後檔案，但首先我們要建立 hello 橋接器檔案會透過某些常用的 Mobile Engagement iOS SDK 方法建立包裝函式。</span><span class="sxs-lookup"><span data-stu-id="eb70c-121">We will update hello `ViewController.m` file later but first we will create hello bridge file which creates a wrapper over some commonly used Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="eb70c-122">建立新的標頭檔稱為**EngagementJsExports.h**使用 hello `JSExport` hello 上述中所述的機制[工作階段](https://developer.apple.com/videos/play/wwdc2013/615)tooexpose hello 原生 iOS 方法。</span><span class="sxs-lookup"><span data-stu-id="eb70c-122">Create a new header file called **EngagementJsExports.h** which uses hello `JSExport` mechanism described in hello aforementioned [session](https://developer.apple.com/videos/play/wwdc2013/615) tooexpose hello native iOS methods.</span></span> 
   
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
6. <span data-ttu-id="eb70c-123">接下來，我們將建立 hello hello 橋接器檔第二個部分。</span><span class="sxs-lookup"><span data-stu-id="eb70c-123">Next we will create hello second part of hello bridge file.</span></span> <span data-ttu-id="eb70c-124">建立一個叫做檔案**EngagementJsExports.m**其中會包含 hello 建立 hello 實際的包裝函式，藉由呼叫 hello Mobile Engagement iOS SDK 方法的實作。</span><span class="sxs-lookup"><span data-stu-id="eb70c-124">Create a file called **EngagementJsExports.m** which will contain hello implementation creating hello actual wrappers by calling hello Mobile Engagement iOS SDK methods.</span></span> <span data-ttu-id="eb70c-125">另外請注意，我們正在剖析 hello`extras`收到所傳遞的 hello webview javascript 並放入`NSMutableDictionary`物件 toobe 傳遞以 hello Engagement SDK 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="eb70c-125">Also note that we are parsing hello `extras` being passed from hello webview javascript and putting that into an `NSMutableDictionary` object toobe passed with hello Engagement SDK method calls.</span></span>  
   
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
7. <span data-ttu-id="eb70c-126">現在我們後回來 toohello **ViewController.m**及更新以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb70c-126">Now we come back toohello **ViewController.m** and update it with hello following code:</span></span> 
   
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
8. <span data-ttu-id="eb70c-127">注意 hello 下列點有關 hello **ViewController.m**檔案：</span><span class="sxs-lookup"><span data-stu-id="eb70c-127">Note hello following points about hello **ViewController.m** file:</span></span>
   
   * <span data-ttu-id="eb70c-128">在 [hello`loadWebView`方法中，我們會載入本機的 HTML 檔案，稱為**LocalPage.html**接下來，我們將檢閱其程式碼。</span><span class="sxs-lookup"><span data-stu-id="eb70c-128">In hello `loadWebView` method, we are loading a local HTML file called **LocalPage.html** whose code we will review next.</span></span> 
   * <span data-ttu-id="eb70c-129">在 [hello`webViewDidFinishLoad`方法，我們會抓取 hello`JsContext`和我們的包裝函式類別關聯。</span><span class="sxs-lookup"><span data-stu-id="eb70c-129">In hello `webViewDidFinishLoad` method, we are grabbing hello `JsContext` and associating our wrapper class with it.</span></span> <span data-ttu-id="eb70c-130">這可讓呼叫我們的包裝函式使用 hello 控制代碼的 SDK 方法**EngagementJs** hello web 檢視。</span><span class="sxs-lookup"><span data-stu-id="eb70c-130">This will allow calling our wrapper SDK methods using hello handle **EngagementJs** from hello webView.</span></span> 
9. <span data-ttu-id="eb70c-131">建立一個叫做檔案**LocalPage.html**以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="eb70c-131">Create a file called **LocalPage.html** with hello following code:</span></span>
   
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
10. <span data-ttu-id="eb70c-132">請注意 hello 下列點有關上述的 hello HTML 檔案：</span><span class="sxs-lookup"><span data-stu-id="eb70c-132">Note hello following points about hello HTML file above:</span></span>
    
    * <span data-ttu-id="eb70c-133">它包含一組的輸入方塊，您可以在其中提供資料 toobe 做為事件、 工作、 錯誤、 應用程式資訊的名稱。</span><span class="sxs-lookup"><span data-stu-id="eb70c-133">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="eb70c-134">當您按一下 hello 按鈕的下一個 tooit 時，進行呼叫，toohello Javascript 最後呼叫 hello 方法從 hello 橋接器檔案 toopass 此呼叫 toohello Mobile Engagement iOS SDK。</span><span class="sxs-lookup"><span data-stu-id="eb70c-134">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement iOS SDK.</span></span> 
    * <span data-ttu-id="eb70c-135">我們會標記上一些額外的靜態資訊 toohello 事件、 工作以及甚至錯誤 toodemonstrate 如何這無法完成。</span><span class="sxs-lookup"><span data-stu-id="eb70c-135">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="eb70c-136">此額外資訊則會傳送 JSON 字串，若您查看 hello`EngagementJsExports.m`檔案、 剖析和傳送事件、 工作、 錯誤以及傳遞。</span><span class="sxs-lookup"><span data-stu-id="eb70c-136">This extra info is sent as a JSON string which, if you look in hello `EngagementJsExports.m` file, is parsed and passed along with sending Events, Jobs, Errors.</span></span> 
    * <span data-ttu-id="eb70c-137">Mobile Engagement 工作會開始使用您指定在 hello 輸入方塊中，執行 10 秒，並關閉 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="eb70c-137">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
    * <span data-ttu-id="eb70c-138">Mobile Engagement 應用程式資訊或標籤與一起傳遞 'customer_name' hello 靜態金鑰以及 hello 值中輸入的 hello 輸入 hello 值為 hello 標記。</span><span class="sxs-lookup"><span data-stu-id="eb70c-138">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
11. <span data-ttu-id="eb70c-139">執行的 hello 應用程式，您會看到下列 hello。</span><span class="sxs-lookup"><span data-stu-id="eb70c-139">Run hello app and you will see hello following.</span></span> <span data-ttu-id="eb70c-140">現在提供一些類似下列的 hello 測試事件的名稱，然後按一下 [**傳送**tooit 下一步]。</span><span class="sxs-lookup"><span data-stu-id="eb70c-140">Now provide some name for a test event like hello following and click **Send** next tooit.</span></span> 
    
     ![][1]
12. <span data-ttu-id="eb70c-141">現在，如果您移 toohello**監視器**] 索引標籤的 [應用程式，並查看**事件詳細資料]-> [**，您會看到顯示以及 hello 靜態應用程式的資訊，我們會傳送此事件。</span><span class="sxs-lookup"><span data-stu-id="eb70c-141">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
    
    ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-ios/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-ios/event-output.png
