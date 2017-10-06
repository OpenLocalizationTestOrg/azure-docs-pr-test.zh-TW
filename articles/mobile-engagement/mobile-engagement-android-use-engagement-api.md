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
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="43a0d-103">TooUse hello Engagement API，在 Android 上的方式</span><span class="sxs-lookup"><span data-stu-id="43a0d-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="43a0d-104">這份文件是附加元件 toohello 文件[Android Mobile Engagement SDK 的進階報告選項](mobile-engagement-android-advanced-reporting.md)。</span><span class="sxs-lookup"><span data-stu-id="43a0d-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="43a0d-105">它提供有關如何 toouse 會 hello Engagement API tooreport 您的應用程式統計資料的深入詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="43a0d-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="43a0d-106">請記住，如果您只想 Engagement tooreport 應用程式的工作階段、 活動、 當機以及技術資訊，然後 hello 最簡單的方法是 toomake 所有您`Activity`子類別是繼承自 hello 對應`EngagementActivity`類別。</span><span class="sxs-lookup"><span data-stu-id="43a0d-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="43a0d-107">如果您想 toodo 更多，例如，如果您需要 tooreport 應用程式特定事件、 錯誤與工作，或如果您在非 hello hello 中實作的其中一個 tooreport 應用程式的活動有不同的方式`EngagementActivity`類別，則您需要 toouse helloEngagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="43a0d-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="43a0d-108">hello Engagement 應用程式開發介面由提供 hello`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="43a0d-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="43a0d-109">這個類別的執行個體可以擷取由呼叫 hello`EngagementAgent.getInstance(Context)`靜態方法 (請注意該 hello`EngagementAgent`傳回的物件是單一值)。</span><span class="sxs-lookup"><span data-stu-id="43a0d-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="43a0d-110">Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="43a0d-110">Engagement concepts</span></span>
<span data-ttu-id="43a0d-111">hello 下列部分精簡 hello 常見[Mobile Engagement 概念](mobile-engagement-concepts.md)，hello Android 平台。</span><span class="sxs-lookup"><span data-stu-id="43a0d-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="43a0d-112">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="43a0d-112">`Session` and `Activity`</span></span>
<span data-ttu-id="43a0d-113">如果 hello 使用者停留超過幾秒鐘的兩個閒置*活動*，然後此順序的*活動*分割成兩個相異*工作階段*。</span><span class="sxs-lookup"><span data-stu-id="43a0d-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="43a0d-114">這些幾秒鐘的時間稱為 hello 「 工作階段逾時 」。</span><span class="sxs-lookup"><span data-stu-id="43a0d-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="43a0d-115">*活動*通常都與一個螢幕的 hello 應用程式，為 toosay hello*活動*時囉 」 畫面隨即出現，並停止囉 」 畫面關閉時啟動： 這是 hello 情況hello Engagement SDK 整合使用 hello`EngagementActivity`類別。</span><span class="sxs-lookup"><span data-stu-id="43a0d-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="43a0d-116">但是*活動*可以也使用來控制手動 hello Engagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="43a0d-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="43a0d-117">這可以讓 toosplit 指定的螢幕詳細 hello 這個畫面 （例如 tooknown 頻率和時間長度對話方塊內使用，則此畫面） 的使用方式的數個子組件 tooget。</span><span class="sxs-lookup"><span data-stu-id="43a0d-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="43a0d-118">報告活動</span><span class="sxs-lookup"><span data-stu-id="43a0d-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="43a0d-119">您不需要與類似 tooreport 活動，這一節所述，如果您使用 hello`EngagementActivity`類別和其變數中所述 hello 如何 tooIntegrate Engagement Android 文件上的。</span><span class="sxs-lookup"><span data-stu-id="43a0d-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="43a0d-120">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="43a0d-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="43a0d-121">您需要 toocall`startActivity()`變更每個階段 hello 使用者活動。</span><span class="sxs-lookup"><span data-stu-id="43a0d-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="43a0d-122">hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="43a0d-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="43a0d-123">hello 此函式是在每個活動的最佳地方 toocall`onResume`回呼。</span><span class="sxs-lookup"><span data-stu-id="43a0d-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="43a0d-124">使用者結束其目前的活動</span><span class="sxs-lookup"><span data-stu-id="43a0d-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="43a0d-125">您需要 toocall`endActivity()`至少一次當 hello 使用者完成其最後一個活動。</span><span class="sxs-lookup"><span data-stu-id="43a0d-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="43a0d-126">這會通知的 hello 逾期 Engagement SDK hello 使用者目前閒置，並 hello 使用者工作階段需要 toobe 關閉一次 hello 工作階段逾時 (如果您呼叫`startActivity()`hello 工作階段逾時到期前，只需繼續 hello 工作階段時)。</span><span class="sxs-lookup"><span data-stu-id="43a0d-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="43a0d-127">hello 此函式是在每個活動的最佳地方 toocall`onPause`回呼。</span><span class="sxs-lookup"><span data-stu-id="43a0d-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="43a0d-128">報告事件</span><span class="sxs-lookup"><span data-stu-id="43a0d-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="43a0d-129">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="43a0d-129">Session events</span></span>
<span data-ttu-id="43a0d-130">工作階段事件是他的工作階段期間執行使用者通常使用的 tooreport hello 動作。</span><span class="sxs-lookup"><span data-stu-id="43a0d-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="43a0d-131">**不含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="43a0d-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="43a0d-132">**含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="43a0d-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="43a0d-133">獨立事件</span><span class="sxs-lookup"><span data-stu-id="43a0d-133">Standalone Events</span></span>
<span data-ttu-id="43a0d-134">反對 toosession，獨立事件發生的事件工作階段的 hello 環境之外。</span><span class="sxs-lookup"><span data-stu-id="43a0d-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="43a0d-135">**範例：**</span><span class="sxs-lookup"><span data-stu-id="43a0d-135">**Example:**</span></span>

<span data-ttu-id="43a0d-136">假設您要 tooreport 廣播的接收者，就會觸發時所發生的事件：</span><span class="sxs-lookup"><span data-stu-id="43a0d-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="43a0d-137">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="43a0d-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="43a0d-138">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="43a0d-138">Session errors</span></span>
<span data-ttu-id="43a0d-139">工作階段錯誤是在他的工作階段期間影響 hello 使用者通常使用的 tooreport hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="43a0d-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="43a0d-140">**範例：**</span><span class="sxs-lookup"><span data-stu-id="43a0d-140">**Example:**</span></span>

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

### <a name="standalone-errors"></a><span data-ttu-id="43a0d-141">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="43a0d-141">Standalone errors</span></span>
<span data-ttu-id="43a0d-142">反對 toosession，獨立錯誤可能會發生錯誤的工作階段的 hello 內容之外。</span><span class="sxs-lookup"><span data-stu-id="43a0d-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="43a0d-143">**範例：**</span><span class="sxs-lookup"><span data-stu-id="43a0d-143">**Example:**</span></span>

<span data-ttu-id="43a0d-144">hello 下列範例顯示如何執行 tooreport 每當 hello 記憶體變少時 hello 電話，您的應用程式處理序時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="43a0d-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="43a0d-145">報告作業</span><span class="sxs-lookup"><span data-stu-id="43a0d-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="43a0d-146">範例</span><span class="sxs-lookup"><span data-stu-id="43a0d-146">Example</span></span>
<span data-ttu-id="43a0d-147">假設您要登入程序的 tooreport hello 持續時間：</span><span class="sxs-lookup"><span data-stu-id="43a0d-147">Suppose you want tooreport hello duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="43a0d-148">報告工作期間的錯誤</span><span class="sxs-lookup"><span data-stu-id="43a0d-148">Report Errors during a Job</span></span>
<span data-ttu-id="43a0d-149">錯誤可能是正在執行而不是工作的相關的 tooa 相關 toohello 目前使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="43a0d-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="43a0d-150">**範例：**</span><span class="sxs-lookup"><span data-stu-id="43a0d-150">**Example:**</span></span>

<span data-ttu-id="43a0d-151">假設您想要 tooreport 時發生登入程序：</span><span class="sxs-lookup"><span data-stu-id="43a0d-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="43a0d-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="43a0d-152">[...] public void signIn(Context context, ...) {</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="43a0d-153">在工作期間報告事件</span><span class="sxs-lookup"><span data-stu-id="43a0d-153">Reporting Events during a job</span></span>
<span data-ttu-id="43a0d-154">事件可能會執行作業，而不是相關的 tooa 相關 toohello 目前使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="43a0d-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="43a0d-155">**範例：**</span><span class="sxs-lookup"><span data-stu-id="43a0d-155">**Example:**</span></span>

<span data-ttu-id="43a0d-156">假設我們有社交網路，而且我們使用工作 tooreport hello 總時間期間的 hello 使用者是連接的 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="43a0d-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="43a0d-157">hello 使用者可以保持連線在背景中或睡眠 hello 電話、 他使用另一個應用程式時，即使因此沒有任何工作階段。</span><span class="sxs-lookup"><span data-stu-id="43a0d-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="43a0d-158">hello 使用者可以從他的朋友接收訊息，這是作業的事件。</span><span class="sxs-lookup"><span data-stu-id="43a0d-158">hello user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="43a0d-159">額外的參數</span><span class="sxs-lookup"><span data-stu-id="43a0d-159">Extra parameters</span></span>
<span data-ttu-id="43a0d-160">附加的 tooevents、 錯誤、 活動與工作，可以是任意的資料。</span><span class="sxs-lookup"><span data-stu-id="43a0d-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="43a0d-161">此資料可以結構化，它會使用 Android 的組合類別 (事實上，它的運作方式如同在 Android Intents 的額外參數)。</span><span class="sxs-lookup"><span data-stu-id="43a0d-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="43a0d-162">請注意，組合可以包含陣列或另一個組合執行個體。</span><span class="sxs-lookup"><span data-stu-id="43a0d-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43a0d-163">如果您將放在 parcelable 或可序列化參數，請確定其`toString()`方法是實作的 tooreturn 人類看得懂的字串。</span><span class="sxs-lookup"><span data-stu-id="43a0d-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="43a0d-164">包含無法序列化之非暫時性欄位的 serializable 類別，會使 Android 在您呼叫 `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="43a0d-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="43a0d-165">不支援額外參數中的疏鬆陣列，也就是它不會序列化為陣列。</span><span class="sxs-lookup"><span data-stu-id="43a0d-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="43a0d-166">您應該將它們轉換成標準的陣列，然後才用於額外的參數。</span><span class="sxs-lookup"><span data-stu-id="43a0d-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="43a0d-167">範例</span><span class="sxs-lookup"><span data-stu-id="43a0d-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="43a0d-168">限制</span><span class="sxs-lookup"><span data-stu-id="43a0d-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="43a0d-169">之間的信任</span><span class="sxs-lookup"><span data-stu-id="43a0d-169">Keys</span></span>
<span data-ttu-id="43a0d-170">每個索引鍵中 hello`Bundle`必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="43a0d-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="43a0d-171">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="43a0d-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="43a0d-172">大小</span><span class="sxs-lookup"><span data-stu-id="43a0d-172">Size</span></span>
<span data-ttu-id="43a0d-173">額外項目會受到限制太**1024年**每個呼叫 （一次編碼的 JSON 中的 hello Engagement 服務） 的字元。</span><span class="sxs-lookup"><span data-stu-id="43a0d-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="43a0d-174">在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 會是 58 字元：</span><span class="sxs-lookup"><span data-stu-id="43a0d-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="43a0d-175">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="43a0d-175">Reporting Application Information</span></span>
<span data-ttu-id="43a0d-176">您可以手動報告追蹤資訊 （或任何其他應用程式特定資訊） 使用 hello`sendAppInfo()`函式。</span><span class="sxs-lookup"><span data-stu-id="43a0d-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="43a0d-177">請注意，這些資訊可傳送以累加方式： 只 hello 最新的值指定索引鍵將會保留指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="43a0d-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="43a0d-178">事件的額外功能，例如 hello 組合類別使用的 tooabstract 應用程式資訊，請注意，陣列或子包裹在一起會被視為一般字串 （使用 JSON 序列化）。</span><span class="sxs-lookup"><span data-stu-id="43a0d-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="43a0d-179">範例</span><span class="sxs-lookup"><span data-stu-id="43a0d-179">Example</span></span>
<span data-ttu-id="43a0d-180">以下是程式碼範例 toosend 使用者性別和出生日期：</span><span class="sxs-lookup"><span data-stu-id="43a0d-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="43a0d-181">限制</span><span class="sxs-lookup"><span data-stu-id="43a0d-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="43a0d-182">之間的信任</span><span class="sxs-lookup"><span data-stu-id="43a0d-182">Keys</span></span>
<span data-ttu-id="43a0d-183">每個索引鍵中 hello`Bundle`必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="43a0d-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="43a0d-184">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="43a0d-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="43a0d-185">大小</span><span class="sxs-lookup"><span data-stu-id="43a0d-185">Size</span></span>
<span data-ttu-id="43a0d-186">應用程式資訊受到太**1024年**每個呼叫 （一次編碼的 JSON 中的 hello Engagement 服務） 的字元。</span><span class="sxs-lookup"><span data-stu-id="43a0d-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="43a0d-187">在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="43a0d-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
