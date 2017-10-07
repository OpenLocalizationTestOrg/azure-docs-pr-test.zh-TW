---
title: "aaaBridge Android WebView 與原生 Mobile Engagement Android SDK"
description: "描述如何 toocreate WebView 之間的橋樑執行 Javascript 以及 hello 原生 Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="8b0d1-103">將 Android WebView 與原生 Mobile Engagement Andoird SDK 橋接</span><span class="sxs-lookup"><span data-stu-id="8b0d1-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b0d1-104">Android 橋接器</span><span class="sxs-lookup"><span data-stu-id="8b0d1-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="8b0d1-105">iOS 橋接器</span><span class="sxs-lookup"><span data-stu-id="8b0d1-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="8b0d1-106">某些行動裝置應用程式被設計為混合式應用程式本身 hello 應用程式開發時使用原生 Android 開發，但是部分或甚至全部 hello 螢幕 Android 的網頁檢視中轉譯。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-106">Some mobile apps are designed as a hybrid app where hello app itself is developed using native Android development but some or even all of hello screens are rendered within an Android WebView.</span></span> <span data-ttu-id="8b0d1-107">您仍然可以在這類應用程式內使用 Mobile Engagement Android SDK，並在本教學課程說明如何 toogo 如何進行此作業。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how toogo about doing this.</span></span> <span data-ttu-id="8b0d1-108">下列的 hello 範例程式碼根據 hello Android 文件[這裡](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript)。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-108">hello sample code below is based on hello Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="8b0d1-109">它會描述如何記錄，此方法無法用於 tooimplement hello 相同，對於 Mobile Engagement Android SDK 的常用方法，從混合式應用程式的網頁檢視也可以起始要求 tootrack 事件、 工作、 錯誤、 應用程式資訊時使用它們透過管線傳送我們的 Android SDK。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-109">It describes how this documented approach could be used tooimplement hello same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests tootrack events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="8b0d1-110">首先，您必須已經完成的 tooensure 我們[快速入門教學課程](mobile-engagement-android-get-started.md)toointegrate hello Mobile Engagement Android SDK 混合式應用程式中的。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-110">First of all, you need tooensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) toointegrate hello Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="8b0d1-111">一旦您這樣做，請您`OnCreate`方法看起來像下列 hello。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-111">Once you do that, your `OnCreate` method will look like hello following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="8b0d1-112">現在請確定您的混合式應用程式上有使用 WebView 的畫面。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="8b0d1-113">hello 的程式碼，將類似 toohello 以下我們會在此載入本機的 HTML 檔**Sample.html**在 hello Webview 中 hello`onCreate`螢幕的方法。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-113">hello code for it will be similar toohello following where we are loading a local HTML file **Sample.html** in hello Webview in hello `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="8b0d1-114">現在，建立名為的橋接器檔案**WebAppInterface**的包裝函式會透過建立一些經常使用 Mobile Engagement Android SDK 方法使用 hello `@JavascriptInterface` hello 中所述的方法[Android 文件](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span><span class="sxs-lookup"><span data-stu-id="8b0d1-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using hello `@JavascriptInterface` approach described in hello [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. <span data-ttu-id="8b0d1-115">當我們建立 hello 上方橋接器檔之後時，我們需要 tooensure 是我們 Webview 相關聯。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-115">Once we have created hello above bridge file, we need tooensure that it is associated with our Webview.</span></span> <span data-ttu-id="8b0d1-116">此 toohappen，您需要 tooedit 您`SetWebview`方法，使其看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="8b0d1-116">For this toohappen, you need tooedit your `SetWebview` method so that it looks like hello following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="8b0d1-117">上述程式碼片段的 hello，稱為`addJavascriptInterface`tooassociate 我們橋接器我們 Webview 類別，也可以建立控制代碼呼叫**EngagementJs** toocall hello 方法從 hello 橋接器檔案。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-117">In hello above snippet, we called `addJavascriptInterface` tooassociate our bridge class with our Webview and also created a handle called **EngagementJs** toocall hello methods from hello bridge file.</span></span> 
6. <span data-ttu-id="8b0d1-118">現在，建立下列檔名的 hello **Sample.html**在資料夾中的專案中呼叫**資產**hello Webview 到載入的我們會在其中呼叫 hello 橋接器檔從 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-118">Now create hello following file called **Sample.html** in your project in a folder called **assets** which is loaded into hello Webview and where we will call hello methods from hello bridge file.</span></span>
   
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
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. <span data-ttu-id="8b0d1-119">請注意 hello 下列點有關上述的 hello HTML 檔案：</span><span class="sxs-lookup"><span data-stu-id="8b0d1-119">Note hello following points about hello HTML file above:</span></span>
   
   * <span data-ttu-id="8b0d1-120">它包含一組的輸入方塊，您可以在其中提供資料 toobe 做為事件、 工作、 錯誤、 應用程式資訊的名稱。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-120">It contains a set of input boxes where you can provide data toobe used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="8b0d1-121">當您按一下 hello 按鈕的下一個 tooit 時，進行呼叫，toohello Javascript 最後呼叫 hello 方法從 hello 橋接器檔案 toopass 此呼叫 toohello Mobile Engagement Android SDK。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-121">When you click on hello button next tooit, a call is made toohello Javascript which eventually calls hello methods from hello bridge file toopass this call toohello Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="8b0d1-122">我們會標記上一些額外的靜態資訊 toohello 事件、 工作以及甚至錯誤 toodemonstrate 如何這無法完成。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-122">We are tagging on some static extra info toohello events, jobs and even errors toodemonstrate how this could be done.</span></span> <span data-ttu-id="8b0d1-123">此額外資訊則會傳送 JSON 字串，若您查看 hello`WebAppInterface`檔案，會剖析並放在 Android`Bundle`並傳送錯誤事件，工作，以及傳遞。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-123">This extra info is sent as a JSON string which, if you look in hello `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="8b0d1-124">Mobile Engagement 工作會開始使用您指定在 hello 輸入方塊中，執行 10 秒，並關閉 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-124">A Mobile Engagement Job is kicked off with hello name you specify in hello input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="8b0d1-125">Mobile Engagement 應用程式資訊或標籤與一起傳遞 'customer_name' hello 靜態金鑰以及 hello 值中輸入的 hello 輸入 hello 值為 hello 標記。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as hello static key and hello value that you entered in hello input as hello value for hello tag.</span></span> 
8. <span data-ttu-id="8b0d1-126">執行的 hello 應用程式，您會看到下列 hello。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-126">Run hello app and you will see hello following.</span></span> <span data-ttu-id="8b0d1-127">現在提供一些類似下列的 hello 測試事件的名稱，然後按一下 **傳送**其下。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-127">Now provide some name for a test event like hello following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="8b0d1-128">現在，如果您移 toohello**監視器**] 索引標籤的 [應用程式，並查看**事件詳細資料]-> [**，您會看到顯示以及 hello 靜態應用程式的資訊，我們會傳送此事件。</span><span class="sxs-lookup"><span data-stu-id="8b0d1-128">Now if you go toohello **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with hello static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
