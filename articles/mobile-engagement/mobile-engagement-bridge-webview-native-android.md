---
title: "將 Android WebView 與原生 Mobile Engagement Andoird SDK 橋接"
description: "說明如何在執行 Javascript 的 WebView 與原生的 Mobile Engagement Android SDK 之間建立橋接器"
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
ms.openlocfilehash: f4fc7b3c81747ec80974a99084eeb1acc311f11f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a><span data-ttu-id="b37d1-103">將 Android WebView 與原生 Mobile Engagement Andoird SDK 橋接</span><span class="sxs-lookup"><span data-stu-id="b37d1-103">Bridge Android WebView with native Mobile Engagement Android SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b37d1-104">Android 橋接器</span><span class="sxs-lookup"><span data-stu-id="b37d1-104">Android Bridge</span></span>](mobile-engagement-bridge-webview-native-android.md)
> * [<span data-ttu-id="b37d1-105">iOS 橋接器</span><span class="sxs-lookup"><span data-stu-id="b37d1-105">iOS Bridge</span></span>](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

<span data-ttu-id="b37d1-106">某些行動應用程式設計為混合式應用程式，其中應用程式本身使用原生 Android 開發方式開發，但部份或甚至所有的畫面是在 Android WebView 中轉譯。</span><span class="sxs-lookup"><span data-stu-id="b37d1-106">Some mobile apps are designed as a hybrid app where the app itself is developed using native Android development but some or even all of the screens are rendered within an Android WebView.</span></span> <span data-ttu-id="b37d1-107">您仍然可以在這類應用程式中使用 Mobile Engagement Android SDK，而本教學課程將說明做法。</span><span class="sxs-lookup"><span data-stu-id="b37d1-107">You can still consume Mobile Engagement Android SDK within such apps and this tutorial describes how to go about doing this.</span></span> <span data-ttu-id="b37d1-108">下列的範例程式碼是以 [這裡](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript)的 Android 文件為基礎。</span><span class="sxs-lookup"><span data-stu-id="b37d1-108">The sample code below is based on the Android documentation [here](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript).</span></span> <span data-ttu-id="b37d1-109">它說明此記載的方法如何用於實作同樣的 Mobile Engagement Android SDK 常用方法，例如混合式應用程式的 Webview 同時可以初始化要求以追蹤事件、工作、錯誤、應用程式資訊，並同時透過我們的 Android SDK 傳遞它們。</span><span class="sxs-lookup"><span data-stu-id="b37d1-109">It describes how this documented approach could be used to implement the same for Mobile Engagement Android SDK's commonly used methods such that a Webview from a hybrid app can also initiate requests to track events, jobs, errors, app-info while piping them via our Android SDK.</span></span> 

1. <span data-ttu-id="b37d1-110">首先，您必須確定您已經完成我們的 [快速入門教學課程](mobile-engagement-android-get-started.md) 以在您的混合式應用程式中整合 Mobile Engagement Android SDK。</span><span class="sxs-lookup"><span data-stu-id="b37d1-110">First of all, you need to ensure that you have gone through our [Getting Started tutorial](mobile-engagement-android-get-started.md) to integrate the Mobile Engagement Android SDK in your hybrid app.</span></span> <span data-ttu-id="b37d1-111">這麼做之後，您的 `OnCreate` 方法會看起來如下。</span><span class="sxs-lookup"><span data-stu-id="b37d1-111">Once you do that, your `OnCreate` method will look like the following.</span></span>  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. <span data-ttu-id="b37d1-112">現在請確定您的混合式應用程式上有使用 WebView 的畫面。</span><span class="sxs-lookup"><span data-stu-id="b37d1-112">Now make sure that your hybrid app has a screen with a WebView on it.</span></span> <span data-ttu-id="b37d1-113">它的程式碼看起來會如下，我們會在您畫面中 `onCreate` 方法的 WebView 中載入本機 HTML 檔案 **Sample.html**。</span><span class="sxs-lookup"><span data-stu-id="b37d1-113">The code for it will be similar to the following where we are loading a local HTML file **Sample.html** in the Webview in the `onCreate` method of your screen.</span></span> 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. <span data-ttu-id="b37d1-114">現在建立名為 **WebAppInterface** 的橋接器檔案，它會利用 [Android 文件](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript)中描述的 `@JavascriptInterface` 方法，透過一些常用的 Mobile Engagement Android SDK 方法來建立包裝函式：</span><span class="sxs-lookup"><span data-stu-id="b37d1-114">Now create a bridge file called **WebAppInterface** which creates a wrapper over some commonly used Mobile Engagement Android SDK methods using the `@JavascriptInterface` approach described in the [Android documentation](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):</span></span>
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate the interface and set the context */
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
4. <span data-ttu-id="b37d1-115">當我們建立了上述的橋接器檔案後，必須確定它與我們的 WebView 相關聯。</span><span class="sxs-lookup"><span data-stu-id="b37d1-115">Once we have created the above bridge file, we need to ensure that it is associated with our Webview.</span></span> <span data-ttu-id="b37d1-116">為了達成此目的，您必須編輯 `SetWebview` 方法，使它看起來如下：</span><span class="sxs-lookup"><span data-stu-id="b37d1-116">For this to happen, you need to edit your `SetWebview` method so that it looks like the following:</span></span>
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. <span data-ttu-id="b37d1-117">在上述的程式碼片段中，我們呼叫 `addJavascriptInterface` 以將我們的橋接類別與 WebView 關聯，並同時建立名為 **EngagementJs** 的控制代碼，以從橋接器檔案呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="b37d1-117">In the above snippet, we called `addJavascriptInterface` to associate our bridge class with our Webview and also created a handle called **EngagementJs** to call the methods from the bridge file.</span></span> 
6. <span data-ttu-id="b37d1-118">現在，在您專案中名為 **assets** 的資料夾內建立名為 **Sample.html** 的下列檔案，它會載入到 WebView 中，我們也將會在其中從橋接器檔案呼叫方法。</span><span class="sxs-lookup"><span data-stu-id="b37d1-118">Now create the following file called **Sample.html** in your project in a folder called **assets** which is loaded into the Webview and where we will call the methods from the bridge file.</span></span>
   
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
                            // Example of how extras info can be passed with the Engagement logs
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
7. <span data-ttu-id="b37d1-119">請注意有關上述 HTML 檔案的重點：</span><span class="sxs-lookup"><span data-stu-id="b37d1-119">Note the following points about the HTML file above:</span></span>
   
   * <span data-ttu-id="b37d1-120">它包含一組輸入方塊，您可以在當中提供資料，用來做為事件、工作、錯誤，應用程式資訊的名稱。</span><span class="sxs-lookup"><span data-stu-id="b37d1-120">It contains a set of input boxes where you can provide data to be used as names for your Event, Job, Error, AppInfo.</span></span> <span data-ttu-id="b37d1-121">當您按一下它旁邊的按鈕，便會向 Javascript 進行呼叫，這通常會從橋接器檔案中呼叫方法，以將此呼叫傳遞到 Mobile Engagement Android SDK。</span><span class="sxs-lookup"><span data-stu-id="b37d1-121">When you click on the button next to it, a call is made to the Javascript which eventually calls the methods from the bridge file to pass this call to the Mobile Engagement Android SDK.</span></span> 
   * <span data-ttu-id="b37d1-122">我們將一些額外的資訊標記到事件、工作，甚至是錯誤，來示範這是如何完成的。</span><span class="sxs-lookup"><span data-stu-id="b37d1-122">We are tagging on some static extra info to the events, jobs and even errors to demonstrate how this could be done.</span></span> <span data-ttu-id="b37d1-123">此額外資訊會以 JSON 字串傳送，它 (如果您查看 `WebAppInterface` 檔案) 可被解析並放入 Android `Bundle` 中，並隨傳送的事件、工作、錯誤傳遞。</span><span class="sxs-lookup"><span data-stu-id="b37d1-123">This extra info is sent as a JSON string which, if you look in the `WebAppInterface` file, is parsed and put in an Android `Bundle` and is passed along with sending Events, Jobs, Errors.</span></span> 
   * <span data-ttu-id="b37d1-124">Mobile Engagement 工作會以您在輸入方塊中指定的名稱開始工作，執行 10 秒鐘之後關閉。</span><span class="sxs-lookup"><span data-stu-id="b37d1-124">A Mobile Engagement Job is kicked off with the name you specify in the input box, run for 10 seconds and shut down.</span></span> 
   * <span data-ttu-id="b37d1-125">Mobile Engagement 應用程式資訊或標記會以 'customer_name' 傳遞作為靜態索引鍵，且您在輸入方塊輸入的值會作為此標記的值。</span><span class="sxs-lookup"><span data-stu-id="b37d1-125">A Mobile Engagement appinfo or tag is passed with 'customer_name' as the static key and the value that you entered in the input as the value for the tag.</span></span> 
8. <span data-ttu-id="b37d1-126">執行應用程式，然後您會看到下列畫面。</span><span class="sxs-lookup"><span data-stu-id="b37d1-126">Run the app and you will see the following.</span></span> <span data-ttu-id="b37d1-127">現在為測試事件提供一些名稱，如下所示，然後按一下它下方的 [傳送]  。</span><span class="sxs-lookup"><span data-stu-id="b37d1-127">Now provide some name for a test event like the following and click **Send** below it.</span></span> 
   
    ![][1]
9. <span data-ttu-id="b37d1-128">現在，如果您移至應用程式的 [監視] 索引標籤，並查看 [事件] -> [詳細資料] 底下，您會看到此事件與我們傳送的靜態應用程式資訊一起顯示。</span><span class="sxs-lookup"><span data-stu-id="b37d1-128">Now if you go to the **Monitor** tab of your app and look under **Events -> Details**, you will see this event show up along with the static app-info that we are sending.</span></span> 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
