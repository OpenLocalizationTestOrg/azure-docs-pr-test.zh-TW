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
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a>將 Android WebView 與原生 Mobile Engagement Andoird SDK 橋接
> [!div class="op_single_selector"]
> * [Android 橋接器](mobile-engagement-bridge-webview-native-android.md)
> * [iOS 橋接器](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

某些行動裝置應用程式被設計為混合式應用程式本身 hello 應用程式開發時使用原生 Android 開發，但是部分或甚至全部 hello 螢幕 Android 的網頁檢視中轉譯。 您仍然可以在這類應用程式內使用 Mobile Engagement Android SDK，並在本教學課程說明如何 toogo 如何進行此作業。 下列的 hello 範例程式碼根據 hello Android 文件[這裡](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript)。 它會描述如何記錄，此方法無法用於 tooimplement hello 相同，對於 Mobile Engagement Android SDK 的常用方法，從混合式應用程式的網頁檢視也可以起始要求 tootrack 事件、 工作、 錯誤、 應用程式資訊時使用它們透過管線傳送我們的 Android SDK。 

1. 首先，您必須已經完成的 tooensure 我們[快速入門教學課程](mobile-engagement-android-get-started.md)toointegrate hello Mobile Engagement Android SDK 混合式應用程式中的。 一旦您這樣做，請您`OnCreate`方法看起來像下列 hello。  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. 現在請確定您的混合式應用程式上有使用 WebView 的畫面。 hello 的程式碼，將類似 toohello 以下我們會在此載入本機的 HTML 檔**Sample.html**在 hello Webview 中 hello`onCreate`螢幕的方法。 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. 現在，建立名為的橋接器檔案**WebAppInterface**的包裝函式會透過建立一些經常使用 Mobile Engagement Android SDK 方法使用 hello `@JavascriptInterface` hello 中所述的方法[Android 文件](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):
   
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
4. 當我們建立 hello 上方橋接器檔之後時，我們需要 tooensure 是我們 Webview 相關聯。 此 toohappen，您需要 tooedit 您`SetWebview`方法，使其看起來像下列 hello:
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. 上述程式碼片段的 hello，稱為`addJavascriptInterface`tooassociate 我們橋接器我們 Webview 類別，也可以建立控制代碼呼叫**EngagementJs** toocall hello 方法從 hello 橋接器檔案。 
6. 現在，建立下列檔名的 hello **Sample.html**在資料夾中的專案中呼叫**資產**hello Webview 到載入的我們會在其中呼叫 hello 橋接器檔從 hello 方法。
   
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
7. 請注意 hello 下列點有關上述的 hello HTML 檔案：
   
   * 它包含一組的輸入方塊，您可以在其中提供資料 toobe 做為事件、 工作、 錯誤、 應用程式資訊的名稱。 當您按一下 hello 按鈕的下一個 tooit 時，進行呼叫，toohello Javascript 最後呼叫 hello 方法從 hello 橋接器檔案 toopass 此呼叫 toohello Mobile Engagement Android SDK。 
   * 我們會標記上一些額外的靜態資訊 toohello 事件、 工作以及甚至錯誤 toodemonstrate 如何這無法完成。 此額外資訊則會傳送 JSON 字串，若您查看 hello`WebAppInterface`檔案，會剖析並放在 Android`Bundle`並傳送錯誤事件，工作，以及傳遞。 
   * Mobile Engagement 工作會開始使用您指定在 hello 輸入方塊中，執行 10 秒，並關閉 hello 名稱。 
   * Mobile Engagement 應用程式資訊或標籤與一起傳遞 'customer_name' hello 靜態金鑰以及 hello 值中輸入的 hello 輸入 hello 值為 hello 標記。 
8. 執行的 hello 應用程式，您會看到下列 hello。 現在提供一些類似下列的 hello 測試事件的名稱，然後按一下 **傳送**其下。 
   
    ![][1]
9. 現在，如果您移 toohello**監視器**] 索引標籤的 [應用程式，並查看**事件詳細資料]-> [**，您會看到顯示以及 hello 靜態應用程式的資訊，我們會傳送此事件。 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
