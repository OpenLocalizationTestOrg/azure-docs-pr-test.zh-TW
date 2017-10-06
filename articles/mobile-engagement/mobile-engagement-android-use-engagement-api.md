---
title: "aaaHow tooUse hello 在 Android 上的行動應用程式開發介面"
description: "最新版的 Android SDK-tooUse hello Engagement API，在 Android 上的方式"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a>TooUse hello Engagement API，在 Android 上的方式
這份文件是附加元件 toohello 文件[Android Mobile Engagement SDK 的進階報告選項](mobile-engagement-android-advanced-reporting.md)。 它提供有關如何 toouse 會 hello Engagement API tooreport 您的應用程式統計資料的深入詳細資訊。

請記住，如果您只想 Engagement tooreport 應用程式的工作階段、 活動、 當機以及技術資訊，然後 hello 最簡單的方法是 toomake 所有您`Activity`子類別是繼承自 hello 對應`EngagementActivity`類別。

如果您想 toodo 更多，例如，如果您需要 tooreport 應用程式特定事件、 錯誤與工作，或如果您在非 hello hello 中實作的其中一個 tooreport 應用程式的活動有不同的方式`EngagementActivity`類別，則您需要 toouse helloEngagement 應用程式開發介面。

hello Engagement 應用程式開發介面由提供 hello`EngagementAgent`類別。 這個類別的執行個體可以擷取由呼叫 hello`EngagementAgent.getInstance(Context)`靜態方法 (請注意該 hello`EngagementAgent`傳回的物件是單一值)。

## <a name="engagement-concepts"></a>Engagement 概念
hello 下列部分精簡 hello 常見[Mobile Engagement 概念](mobile-engagement-concepts.md)，hello Android 平台。

### <a name="session-and-activity"></a>`Session`和`Activity`
如果 hello 使用者停留超過幾秒鐘的兩個閒置*活動*，然後此順序的*活動*分割成兩個相異*工作階段*。 這些幾秒鐘的時間稱為 hello 「 工作階段逾時 」。

*活動*通常都與一個螢幕的 hello 應用程式，為 toosay hello*活動*時囉 」 畫面隨即出現，並停止囉 」 畫面關閉時啟動： 這是 hello 情況hello Engagement SDK 整合使用 hello`EngagementActivity`類別。

但是*活動*可以也使用來控制手動 hello Engagement 應用程式開發介面。 這可以讓 toosplit 指定的螢幕詳細 hello 這個畫面 （例如 tooknown 頻率和時間長度對話方塊內使用，則此畫面） 的使用方式的數個子組件 tooget。

## <a name="reporting-activities"></a>報告活動
> [!IMPORTANT]
> 您不需要與類似 tooreport 活動，這一節所述，如果您使用 hello`EngagementActivity`類別和其變數中所述 hello 如何 tooIntegrate Engagement Android 文件上的。
> 
> 

### <a name="user-starts-a-new-activity"></a>使用者啟動新的活動
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

您需要 toocall`startActivity()`變更每個階段 hello 使用者活動。 hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。

hello 此函式是在每個活動的最佳地方 toocall`onResume`回呼。

### <a name="user-ends-his-current-activity"></a>使用者結束其目前的活動
            EngagementAgent.getInstance(this).endActivity();

您需要 toocall`endActivity()`至少一次當 hello 使用者完成其最後一個活動。 這會通知的 hello 逾期 Engagement SDK hello 使用者目前閒置，並 hello 使用者工作階段需要 toobe 關閉一次 hello 工作階段逾時 (如果您呼叫`startActivity()`hello 工作階段逾時到期前，只需繼續 hello 工作階段時)。

hello 此函式是在每個活動的最佳地方 toocall`onPause`回呼。

## <a name="reporting-events"></a>報告事件
### <a name="session-events"></a>工作階段事件
工作階段事件是他的工作階段期間執行使用者通常使用的 tooreport hello 動作。

**不含額外資料的範例：**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**含額外資料的範例：**

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a>獨立事件
反對 toosession，獨立事件發生的事件工作階段的 hello 環境之外。

**範例：**

假設您要 tooreport 廣播的接收者，就會觸發時所發生的事件：

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>報告錯誤
### <a name="session-errors"></a>工作階段錯誤
工作階段錯誤是在他的工作階段期間影響 hello 使用者通常使用的 tooreport hello 錯誤。

**範例：**

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a>獨立錯誤
反對 toosession，獨立錯誤可能會發生錯誤的工作階段的 hello 內容之外。

**範例：**

hello 下列範例顯示如何執行 tooreport 每當 hello 記憶體變少時 hello 電話，您的應用程式處理序時發生錯誤。

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>報告作業
### <a name="example"></a>範例
假設您要登入程序的 tooreport hello 持續時間：

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a>報告工作期間的錯誤
錯誤可能是正在執行而不是工作的相關的 tooa 相關 toohello 目前使用者工作階段。

**範例：**

假設您想要 tooreport 時發生登入程序：

[...] public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a>在工作期間報告事件
事件可能會執行作業，而不是相關的 tooa 相關 toohello 目前使用者工作階段。

**範例：**

假設我們有社交網路，而且我們使用工作 tooreport hello 總時間期間的 hello 使用者是連接的 toohello 伺服器。 hello 使用者可以保持連線在背景中或睡眠 hello 電話、 他使用另一個應用程式時，即使因此沒有任何工作階段。

hello 使用者可以從他的朋友接收訊息，這是作業的事件。

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a>額外的參數
附加的 tooevents、 錯誤、 活動與工作，可以是任意的資料。

此資料可以結構化，它會使用 Android 的組合類別 (事實上，它的運作方式如同在 Android Intents 的額外參數)。 請注意，組合可以包含陣列或另一個組合執行個體。

> [!IMPORTANT]
> 如果您將放在 parcelable 或可序列化參數，請確定其`toString()`方法是實作的 tooreturn 人類看得懂的字串。 包含無法序列化之非暫時性欄位的 serializable 類別，會使 Android 在您呼叫 `bundle.putSerializable("key",value);`
> 
> [!WARNING]
> 不支援額外參數中的疏鬆陣列，也就是它不會序列化為陣列。 您應該將它們轉換成標準的陣列，然後才用於額外的參數。
> 
> 

### <a name="example"></a>範例
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>限制
#### <a name="keys"></a>之間的信任
每個索引鍵中 hello`Bundle`必須符合下列規則運算式的 hello:

`^[a-zA-Z][a-zA-Z_0-9]*`

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
額外項目會受到限制太**1024年**每個呼叫 （一次編碼的 JSON 中的 hello Engagement 服務） 的字元。

在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 會是 58 字元：

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>報告應用程式資訊
您可以手動報告追蹤資訊 （或任何其他應用程式特定資訊） 使用 hello`sendAppInfo()`函式。

請注意，這些資訊可傳送以累加方式： 只 hello 最新的值指定索引鍵將會保留指定的裝置。

事件的額外功能，例如 hello 組合類別使用的 tooabstract 應用程式資訊，請注意，陣列或子包裹在一起會被視為一般字串 （使用 JSON 序列化）。

### <a name="example"></a>範例
以下是程式碼範例 toosend 使用者性別和出生日期：

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>限制
#### <a name="keys"></a>之間的信任
每個索引鍵中 hello`Bundle`必須符合下列規則運算式的 hello:

`^[a-zA-Z][a-zA-Z_0-9]*`

這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。

#### <a name="size"></a>大小
應用程式資訊受到太**1024年**每個呼叫 （一次編碼的 JSON 中的 hello Engagement 服務） 的字元。

在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 是 44 個字元：

            {"expiration":"2016-12-07","status":"premium"}
