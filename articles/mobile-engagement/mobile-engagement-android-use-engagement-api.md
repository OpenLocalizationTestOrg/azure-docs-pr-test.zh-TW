---
title: "如何在 Android 上使用 Engagement API"
description: "最新 Android SDK - 如何在 Android 上使用 Engagement API"
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
ms.openlocfilehash: d353cd2fe47c54a0282cc5bb1b22b4a56e0cd82c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-android"></a><span data-ttu-id="1072e-103">如何在 Android 上使用 Engagement API</span><span class="sxs-lookup"><span data-stu-id="1072e-103">How to Use the Engagement API on Android</span></span>
<span data-ttu-id="1072e-104">此文件是 [Android Mobile Engagement SDK 的進階報告選項](mobile-engagement-android-advanced-reporting.md)文件的補充。</span><span class="sxs-lookup"><span data-stu-id="1072e-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="1072e-105">它會提供關於如何使用 Engagement API 來回報您應用程式的統計資料之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1072e-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="1072e-106">請記住，如果您只想要 Engagement 向您報告應用程式的工作階段、活動、當機和技術資訊，那麼最簡單的方法是讓所有 `Activity` 子類別繼承自對應的 `EngagementActivity` 類別。</span><span class="sxs-lookup"><span data-stu-id="1072e-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="1072e-107">如果您想要執行更多工作 (例如，若您需要報告應用程式的特定事件、錯誤和作業，或者您需要以不同於 `EngagementActivity` 類別中的方式來報告應用程式的活動)，則您需要使用 Engagement API。</span><span class="sxs-lookup"><span data-stu-id="1072e-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="1072e-108">Engagement API 是由 `EngagementAgent` 類別提供。</span><span class="sxs-lookup"><span data-stu-id="1072e-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="1072e-109">此類別的執行個體，可以藉由呼叫 `EngagementAgent.getInstance(Context)` 靜態方法 (請注意，傳回的 `EngagementAgent` 物件為單一值) 來擷取。</span><span class="sxs-lookup"><span data-stu-id="1072e-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="1072e-110">Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="1072e-110">Engagement concepts</span></span>
<span data-ttu-id="1072e-111">以下部分簡要說明適用於 Android 平台的一般 [Mobile Engagement 概念](mobile-engagement-concepts.md)。</span><span class="sxs-lookup"><span data-stu-id="1072e-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="1072e-112">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="1072e-112">`Session` and `Activity`</span></span>
<span data-ttu-id="1072e-113">如果使用者在兩個活動之間維持閒置超過幾秒鐘，其活動序列會分割成兩個相異的工作階段。</span><span class="sxs-lookup"><span data-stu-id="1072e-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="1072e-114">這幾秒稱為「工作階段逾時」。</span><span class="sxs-lookup"><span data-stu-id="1072e-114">These few seconds are called the "session timeout".</span></span>

<span data-ttu-id="1072e-115">活動通常會與應用程式的某個畫面相關聯，也就是說，活動會在畫面顯示時啟動，並在畫面關閉時停止：這是使用 `EngagementActivity` 類別整合 Engagement SDK 時的情況。</span><span class="sxs-lookup"><span data-stu-id="1072e-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span></span>

<span data-ttu-id="1072e-116">但您也可以透過 Engagement API 手動控制「活動」  。</span><span class="sxs-lookup"><span data-stu-id="1072e-116">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="1072e-117">這樣可以將指定的畫面分隔為數個子部分，以取得關於此畫面使用方式的詳細資料 (例如，可了解此畫面內對話方塊的使用頻率與使用時間長度)。</span><span class="sxs-lookup"><span data-stu-id="1072e-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="1072e-118">報告活動</span><span class="sxs-lookup"><span data-stu-id="1072e-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1072e-119">如果您依照＜如何在 Android 上整合 Engagement＞文件所述使用 `EngagementActivity` 類別與變體，您就不需要報告本節所述的各項活動。</span><span class="sxs-lookup"><span data-stu-id="1072e-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="1072e-120">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="1072e-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="1072e-121">每當使用者活動變更，您就需要呼叫 `startActivity()` 。</span><span class="sxs-lookup"><span data-stu-id="1072e-121">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="1072e-122">第一次呼叫此函式會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="1072e-122">The first call to this function starts a new user session.</span></span>

<span data-ttu-id="1072e-123">呼叫此函式的最佳位置是在每個活動 `onResume` 回呼。</span><span class="sxs-lookup"><span data-stu-id="1072e-123">The best place to call this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="1072e-124">使用者結束其目前的活動</span><span class="sxs-lookup"><span data-stu-id="1072e-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="1072e-125">使用者完成最後一個活動時，您至少需要呼叫 `endActivity()` 一次。</span><span class="sxs-lookup"><span data-stu-id="1072e-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="1072e-126">這會通知 Engagement SDK，說明使用者目前處於閒置狀態，且工作階段逾時到期時就得關閉使用者工作階段 (如果您在工作階段逾時到期前就呼叫 `startActivity()` ，工作階段只會繼續)。</span><span class="sxs-lookup"><span data-stu-id="1072e-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span></span>

<span data-ttu-id="1072e-127">呼叫此函式的最佳位置是在每個活動 `onPause` 回呼。</span><span class="sxs-lookup"><span data-stu-id="1072e-127">The best place to call this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="1072e-128">報告事件</span><span class="sxs-lookup"><span data-stu-id="1072e-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="1072e-129">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="1072e-129">Session events</span></span>
<span data-ttu-id="1072e-130">工作階段事件通常用來報告在其工作階段期間由使用者所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="1072e-130">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="1072e-131">**不含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="1072e-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="1072e-132">**含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="1072e-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="1072e-133">獨立事件</span><span class="sxs-lookup"><span data-stu-id="1072e-133">Standalone Events</span></span>
<span data-ttu-id="1072e-134">與工作階段事件相反，獨立的事件可能發生在工作階段的內容之外。</span><span class="sxs-lookup"><span data-stu-id="1072e-134">Contrary to session events, standalone events can occur outside of the context of a session.</span></span>

<span data-ttu-id="1072e-135">**範例：**</span><span class="sxs-lookup"><span data-stu-id="1072e-135">**Example:**</span></span>

<span data-ttu-id="1072e-136">假設您想要在觸發廣播接收器時，報告發生事件：</span><span class="sxs-lookup"><span data-stu-id="1072e-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="1072e-137">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="1072e-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="1072e-138">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="1072e-138">Session errors</span></span>
<span data-ttu-id="1072e-139">工作階段錯誤通常用來報告在其工作階段期間影響使用者的錯誤。</span><span class="sxs-lookup"><span data-stu-id="1072e-139">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="1072e-140">**範例：**</span><span class="sxs-lookup"><span data-stu-id="1072e-140">**Example:**</span></span>

            /** The user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* The user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="1072e-141">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="1072e-141">Standalone errors</span></span>
<span data-ttu-id="1072e-142">不同於工作階段錯誤，獨立錯誤可以出現在工作階段的內容之外。</span><span class="sxs-lookup"><span data-stu-id="1072e-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

<span data-ttu-id="1072e-143">**範例：**</span><span class="sxs-lookup"><span data-stu-id="1072e-143">**Example:**</span></span>

<span data-ttu-id="1072e-144">下列範例示範如何在應用程式處理程序執行時，每當手機記憶體不足時便報告錯誤。</span><span class="sxs-lookup"><span data-stu-id="1072e-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="1072e-145">報告工作</span><span class="sxs-lookup"><span data-stu-id="1072e-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="1072e-146">範例</span><span class="sxs-lookup"><span data-stu-id="1072e-146">Example</span></span>
<span data-ttu-id="1072e-147">假設您想要報告登入程序持續時間：</span><span class="sxs-lookup"><span data-stu-id="1072e-147">Suppose you want to report the duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="1072e-148">報告工作期間的錯誤</span><span class="sxs-lookup"><span data-stu-id="1072e-148">Report Errors during a Job</span></span>
<span data-ttu-id="1072e-149">錯誤可能與正在執行的工作關聯，而不是與目前的使用者工作階段關聯。</span><span class="sxs-lookup"><span data-stu-id="1072e-149">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="1072e-150">**範例：**</span><span class="sxs-lookup"><span data-stu-id="1072e-150">**Example:**</span></span>

<span data-ttu-id="1072e-151">假設您想要報告登入程序期間的錯誤：</span><span class="sxs-lookup"><span data-stu-id="1072e-151">Suppose you want to report an error during you login process:</span></span>

<span data-ttu-id="1072e-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="1072e-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try to sign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report the error to Engagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="1072e-153">在工作期間報告事件</span><span class="sxs-lookup"><span data-stu-id="1072e-153">Reporting Events during a job</span></span>
<span data-ttu-id="1072e-154">事件可以與執行中的工作相關，而不是與目前的使用者工作階段相關。</span><span class="sxs-lookup"><span data-stu-id="1072e-154">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="1072e-155">**範例：**</span><span class="sxs-lookup"><span data-stu-id="1072e-155">**Example:**</span></span>

<span data-ttu-id="1072e-156">假設我們有社交網路，且使用工作來報告使用者連線到伺服器這段期間的總時間。</span><span class="sxs-lookup"><span data-stu-id="1072e-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="1072e-157">使用者可以在使用另一個應用程式或行動電話在休眠狀態時，保持在背景中連線，因此沒有工作階段。</span><span class="sxs-lookup"><span data-stu-id="1072e-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="1072e-158">使用者可以接收來自朋友的訊息，這就是工作事件。</span><span class="sxs-lookup"><span data-stu-id="1072e-158">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="1072e-159">額外的參數</span><span class="sxs-lookup"><span data-stu-id="1072e-159">Extra parameters</span></span>
<span data-ttu-id="1072e-160">可以將任意資料附加到事件、錯誤、活動及工作。</span><span class="sxs-lookup"><span data-stu-id="1072e-160">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="1072e-161">此資料可以結構化，它會使用 Android 的組合類別 (事實上，它的運作方式如同在 Android Intents 的額外參數)。</span><span class="sxs-lookup"><span data-stu-id="1072e-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="1072e-162">請注意，組合可以包含陣列或另一個組合執行個體。</span><span class="sxs-lookup"><span data-stu-id="1072e-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1072e-163">如果您放入 parcelable 或 serializable 參數，請確定已實作其 `toString()` 方法，以傳回使用者可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="1072e-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span></span> <span data-ttu-id="1072e-164">包含無法序列化之非暫時性欄位的 serializable 類別，會使 Android 在您呼叫 `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="1072e-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="1072e-165">不支援額外參數中的疏鬆陣列，也就是它不會序列化為陣列。</span><span class="sxs-lookup"><span data-stu-id="1072e-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="1072e-166">您應該將它們轉換成標準的陣列，然後才用於額外的參數。</span><span class="sxs-lookup"><span data-stu-id="1072e-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="1072e-167">範例</span><span class="sxs-lookup"><span data-stu-id="1072e-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="1072e-168">限制</span><span class="sxs-lookup"><span data-stu-id="1072e-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="1072e-169">之間的信任</span><span class="sxs-lookup"><span data-stu-id="1072e-169">Keys</span></span>
<span data-ttu-id="1072e-170">`Bundle` 中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="1072e-170">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="1072e-171">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="1072e-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="1072e-172">大小</span><span class="sxs-lookup"><span data-stu-id="1072e-172">Size</span></span>
<span data-ttu-id="1072e-173">額外項目限制為一次呼叫 **1024** 個字元 (由 Engagement 服務以 JSON 編碼之後)。</span><span class="sxs-lookup"><span data-stu-id="1072e-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="1072e-174">在上述範例中，傳送到伺服器的 JSON 會是 58 個字元：</span><span class="sxs-lookup"><span data-stu-id="1072e-174">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="1072e-175">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="1072e-175">Reporting Application Information</span></span>
<span data-ttu-id="1072e-176">您可以使用 `sendAppInfo()` 函式手動報告追蹤資訊 (或是任何其他應用程式特定資訊)。</span><span class="sxs-lookup"><span data-stu-id="1072e-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="1072e-177">請注意，這些資訊可以累加地傳送：只有指定的索引鍵的最新值會保留給指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="1072e-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="1072e-178">就像事件的額外項目，Bundle 類別用來摘要應用程式資訊，請注意陣列或子組合會被視為一般字串 (使用 JSON 序列化)。</span><span class="sxs-lookup"><span data-stu-id="1072e-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="1072e-179">範例</span><span class="sxs-lookup"><span data-stu-id="1072e-179">Example</span></span>
<span data-ttu-id="1072e-180">以下是傳送使用者性別和出生日期的程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="1072e-180">Here is a code sample to send user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="1072e-181">限制</span><span class="sxs-lookup"><span data-stu-id="1072e-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="1072e-182">之間的信任</span><span class="sxs-lookup"><span data-stu-id="1072e-182">Keys</span></span>
<span data-ttu-id="1072e-183">`Bundle` 中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="1072e-183">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="1072e-184">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="1072e-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="1072e-185">大小</span><span class="sxs-lookup"><span data-stu-id="1072e-185">Size</span></span>
<span data-ttu-id="1072e-186">應用程式資訊限制為一次呼叫 **1024** 個字元 (由 Engagement 服務以 JSON 編碼之後)。</span><span class="sxs-lookup"><span data-stu-id="1072e-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="1072e-187">在上述範例中，傳送到伺服器的 JSON 會是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="1072e-187">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
