---
title: "aaaHow tooUse hello Engagement API 在 Windows Phone Silverlight 上"
description: "如何 tooUse hello Engagement API 在 Windows Phone Silverlight 上"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="fc634-103">如何 tooUse hello Engagement API 在 Windows Phone Silverlight 上</span><span class="sxs-lookup"><span data-stu-id="fc634-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="fc634-104">這份文件是附加元件 toohello 文件[如何在 Windows Phone Silverlight 應用程式中的 toointegrate Mobile Engagement](mobile-engagement-windows-phone-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="fc634-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="fc634-105">它提供有關如何 toouse 會 hello Engagement API tooreport 您的應用程式統計資料的深入詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fc634-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="fc634-106">如果您的應用程式工作階段、 活動、 當機以及技術資訊，請只想 Engagement tooreport 則 hello 最簡單的方式是 toomake 所有您`PhoneApplicationPage`子類別是繼承自 hello`EngagementPage`類別。</span><span class="sxs-lookup"><span data-stu-id="fc634-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="fc634-107">如果您想 toodo 更多，例如，如果您需要 tooreport 應用程式特定事件、 錯誤與工作，或如果您在非 hello hello 中實作的其中一個 tooreport 應用程式的活動有不同的方式`EngagementPage`類別，則您需要 toouse helloEngagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="fc634-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="fc634-108">hello Engagement 應用程式開發介面由提供 hello`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="fc634-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="fc634-109">您可以存取透過 toothose 方法`EngagementAgent.Instance`。</span><span class="sxs-lookup"><span data-stu-id="fc634-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="fc634-110">即使尚未初始化 hello 代理程式的模組，每個呼叫 toohello API 會延後和 hello 代理程式可用時再重新執行。</span><span class="sxs-lookup"><span data-stu-id="fc634-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="fc634-111">Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="fc634-111">Engagement concepts</span></span>
<span data-ttu-id="fc634-112">下列組件的 hello 精簡 hello Mobile Engagement 概念 hello Windows Phone 平台。</span><span class="sxs-lookup"><span data-stu-id="fc634-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="fc634-113">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="fc634-113">`Session` and `Activity`</span></span>
<span data-ttu-id="fc634-114">*活動*通常都與一頁的 hello 應用程式，為 toosay hello*活動*hello 頁面隨即出現，而 hello 頁已關閉時停止時啟動： 這是 hello 的情況下如果 helloEngagement SDK 整合使用 hello`EngagementPage`類別。</span><span class="sxs-lookup"><span data-stu-id="fc634-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="fc634-115">但是*活動*可以也使用來控制手動 hello Engagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="fc634-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="fc634-116">這可以讓 toosplit 指定的頁面數個子組件 tooget 詳細 hello 使用量 （例如 tooknown 頻率和時間的對話方塊內使用，則此頁面） 此頁面。</span><span class="sxs-lookup"><span data-stu-id="fc634-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="fc634-117">報告活動</span><span class="sxs-lookup"><span data-stu-id="fc634-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="fc634-118">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="fc634-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-119">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="fc634-120">您需要 toocall`StartActivity()`變更每個階段 hello 使用者活動。</span><span class="sxs-lookup"><span data-stu-id="fc634-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="fc634-121">hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="fc634-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc634-122">hello SDK hello 應用程式關閉時，會自動呼叫 hello EndActivity 方法。</span><span class="sxs-lookup"><span data-stu-id="fc634-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="fc634-123">因此，強烈建議 toocall hello StartActivity 方法時的 hello 使用者變更與 hello EndActivity 方法，因為呼叫這個方法會強制 hello 目前工作階段 toobe tooNEVER 呼叫 hello 活動已結束。</span><span class="sxs-lookup"><span data-stu-id="fc634-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="fc634-124">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="fc634-125">使用者結束其目前的活動</span><span class="sxs-lookup"><span data-stu-id="fc634-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-126">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="fc634-127">您需要 toocall`EndActivity()`至少一次當 hello 使用者完成其最後一個活動。</span><span class="sxs-lookup"><span data-stu-id="fc634-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="fc634-128">這會通知的 hello 逾期 Engagement SDK hello 使用者目前閒置，並 hello 使用者工作階段需要 toobe 關閉一次 hello 工作階段逾時 (如果您呼叫`StartActivity()`hello 工作階段逾時到期前，只需繼續 hello 工作階段的)。</span><span class="sxs-lookup"><span data-stu-id="fc634-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-129">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="fc634-130">報告作業</span><span class="sxs-lookup"><span data-stu-id="fc634-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="fc634-131">啟動作業</span><span class="sxs-lookup"><span data-stu-id="fc634-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-132">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="fc634-133">經過一段時間，您可以使用 hello tootrack certains 的工作。</span><span class="sxs-lookup"><span data-stu-id="fc634-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-134">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="fc634-135">結束作業</span><span class="sxs-lookup"><span data-stu-id="fc634-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-136">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="fc634-137">只要已終止工作所追蹤的工作，您應該呼叫此作業，hello EndJob 方法藉由提供 hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="fc634-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-138">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="fc634-139">報告事件</span><span class="sxs-lookup"><span data-stu-id="fc634-139">Reporting Events</span></span>
<span data-ttu-id="fc634-140">事件有三種類型：</span><span class="sxs-lookup"><span data-stu-id="fc634-140">There is three types of events :</span></span>

* <span data-ttu-id="fc634-141">獨立事件</span><span class="sxs-lookup"><span data-stu-id="fc634-141">Standalone events</span></span>
* <span data-ttu-id="fc634-142">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="fc634-142">Session events</span></span>
* <span data-ttu-id="fc634-143">作業事件</span><span class="sxs-lookup"><span data-stu-id="fc634-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="fc634-144">獨立事件</span><span class="sxs-lookup"><span data-stu-id="fc634-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-145">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="fc634-146">工作階段的 hello 環境之外發生獨立事件。</span><span class="sxs-lookup"><span data-stu-id="fc634-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-147">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="fc634-148">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="fc634-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-149">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="fc634-150">工作階段事件是他的工作階段期間執行使用者通常使用的 tooreport hello 動作。</span><span class="sxs-lookup"><span data-stu-id="fc634-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-151">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-151">Example</span></span>
<span data-ttu-id="fc634-152">**沒有資料：**</span><span class="sxs-lookup"><span data-stu-id="fc634-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="fc634-153">**有資料：**</span><span class="sxs-lookup"><span data-stu-id="fc634-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="fc634-154">作業事件</span><span class="sxs-lookup"><span data-stu-id="fc634-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-155">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="fc634-156">作業事件是在作業期間執行使用者通常使用的 tooreport hello 動作。</span><span class="sxs-lookup"><span data-stu-id="fc634-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-157">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="fc634-158">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="fc634-158">Reporting Errors</span></span>
<span data-ttu-id="fc634-159">錯誤有三種類型：</span><span class="sxs-lookup"><span data-stu-id="fc634-159">There is three types of errors :</span></span>

* <span data-ttu-id="fc634-160">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="fc634-160">Standalone errors</span></span>
* <span data-ttu-id="fc634-161">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="fc634-161">Session errors</span></span>
* <span data-ttu-id="fc634-162">作業錯誤</span><span class="sxs-lookup"><span data-stu-id="fc634-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="fc634-163">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="fc634-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-164">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="fc634-165">反對 toosession，獨立錯誤可能會發生錯誤的工作階段的 hello 內容之外。</span><span class="sxs-lookup"><span data-stu-id="fc634-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-166">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="fc634-167">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="fc634-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-168">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="fc634-169">工作階段錯誤是在他的工作階段期間影響 hello 使用者通常使用的 tooreport hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="fc634-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-170">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="fc634-171">作業錯誤</span><span class="sxs-lookup"><span data-stu-id="fc634-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-172">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="fc634-173">錯誤可能是正在執行而不是工作的相關的 tooa 相關 toohello 目前使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="fc634-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-174">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="fc634-175">報告當機</span><span class="sxs-lookup"><span data-stu-id="fc634-175">Reporting Crashes</span></span>
<span data-ttu-id="fc634-176">hello 代理程式會將兩個方法 toodeal 提供當機。</span><span class="sxs-lookup"><span data-stu-id="fc634-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="fc634-177">傳送例外狀況</span><span class="sxs-lookup"><span data-stu-id="fc634-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-178">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="fc634-179">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-179">Example</span></span>
<span data-ttu-id="fc634-180">透過呼叫下列函式您可以隨時傳送例外狀況：</span><span class="sxs-lookup"><span data-stu-id="fc634-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="fc634-181">您也可以使用選擇性參數 tooterminate hello 參與工作階段在 hello 相同的時間比傳送嗨損毀。</span><span class="sxs-lookup"><span data-stu-id="fc634-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="fc634-182">因此，呼叫 toodo:</span><span class="sxs-lookup"><span data-stu-id="fc634-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="fc634-183">如果您這樣做，請只在傳送嗨損毀之後將關閉 hello 工作階段和工作。</span><span class="sxs-lookup"><span data-stu-id="fc634-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="fc634-184">傳送未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="fc634-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="fc634-185">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="fc634-186">Engagement 也會提供方法 toosend 未處理的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="fc634-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="fc634-187">這是 hello silverlight UnhandledException 事件處理常式內使用時特別有用。</span><span class="sxs-lookup"><span data-stu-id="fc634-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="fc634-188">這個方法將**永遠**呼叫後終止 hello 參與工作階段和工作。</span><span class="sxs-lookup"><span data-stu-id="fc634-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="fc634-189">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-189">Example</span></span>
<span data-ttu-id="fc634-190">您可以使用它 tooimplement 自己 UnhandledException 處理常式 （特別是如果您已停用報告功能的 Engagement hello 自動損毀）。</span><span class="sxs-lookup"><span data-stu-id="fc634-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="fc634-191">例如，在 hello`Application_UnhandledException`方法 hello`App.xaml.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="fc634-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="fc634-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="fc634-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="fc634-193">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="fc634-194">Hello 使用者向前巡覽，遠離應用程式之後就會引發 hello 停用事件，, hello 作業系統會進入休眠狀態的 tooput hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc634-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="fc634-195">接著，hello 應用程式是正在標記要刪除。</span><span class="sxs-lookup"><span data-stu-id="fc634-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="fc634-196">應用程式已終止這個處理序中，但會保留一些 hello 應用程式和 hello hello 應用程式內的個別頁面 hello 狀態相關的資料。</span><span class="sxs-lookup"><span data-stu-id="fc634-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="fc634-197">您有 tooinsert`EngagementAgent.Instance.OnActivated(e)`在 hello `Application_Activated` hello App.xaml.cs 檔案 tooreset hello Engagement 代理程式時 hello 應用程式是否已 Tombstoned 方法。</span><span class="sxs-lookup"><span data-stu-id="fc634-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="fc634-198">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="fc634-199">裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="fc634-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="fc634-200">您可以藉由呼叫這個方法來取得 hello engagement 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="fc634-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="fc634-201">額外的參數</span><span class="sxs-lookup"><span data-stu-id="fc634-201">Extras parameters</span></span>
<span data-ttu-id="fc634-202">附加的 tooan 事件、 錯誤、 活動或工作，可以是任意的資料。</span><span class="sxs-lookup"><span data-stu-id="fc634-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="fc634-203">可以使用字典來結構化這些資料。</span><span class="sxs-lookup"><span data-stu-id="fc634-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="fc634-204">索引鍵和值可以是任何型別。</span><span class="sxs-lookup"><span data-stu-id="fc634-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="fc634-205">額外項目資料會序列化，因此如果您想 tooinsert 自己的額外項目中的型別必須 tooadd 這種類型的資料合約。</span><span class="sxs-lookup"><span data-stu-id="fc634-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="fc634-206">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-206">Example</span></span>
<span data-ttu-id="fc634-207">我們建立一個新的類別叫 "Person"。</span><span class="sxs-lookup"><span data-stu-id="fc634-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="fc634-208">然後，我們會加入`Person`額外的執行個體 tooan。</span><span class="sxs-lookup"><span data-stu-id="fc634-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="fc634-209">如果您將其他類型的物件，請確定其 tostring （） 方法是實作的 tooreturn 人類可讀取的字串。</span><span class="sxs-lookup"><span data-stu-id="fc634-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="fc634-210">限制</span><span class="sxs-lookup"><span data-stu-id="fc634-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="fc634-211">之間的信任</span><span class="sxs-lookup"><span data-stu-id="fc634-211">Keys</span></span>
<span data-ttu-id="fc634-212">Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc634-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="fc634-213">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="fc634-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="fc634-214">大小</span><span class="sxs-lookup"><span data-stu-id="fc634-214">Size</span></span>
<span data-ttu-id="fc634-215">額外項目會受到限制太**1024年**呼叫每個字元。</span><span class="sxs-lookup"><span data-stu-id="fc634-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="fc634-216">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="fc634-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="fc634-217">參考</span><span class="sxs-lookup"><span data-stu-id="fc634-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="fc634-218">您可以手動報告追蹤資訊 （或任何其他應用程式特定資訊） 使用 hello SendAppInfo() 函式。</span><span class="sxs-lookup"><span data-stu-id="fc634-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="fc634-219">請注意，這些資訊可傳送以累加方式： 只 hello 最新的值指定索引鍵將會保留指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="fc634-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="fc634-220">事件的額外功能，例如使用字典\<物件，物件\>tooattach 資訊。</span><span class="sxs-lookup"><span data-stu-id="fc634-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="fc634-221">範例</span><span class="sxs-lookup"><span data-stu-id="fc634-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="fc634-222">限制</span><span class="sxs-lookup"><span data-stu-id="fc634-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="fc634-223">之間的信任</span><span class="sxs-lookup"><span data-stu-id="fc634-223">Keys</span></span>
<span data-ttu-id="fc634-224">Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc634-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="fc634-225">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="fc634-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="fc634-226">大小</span><span class="sxs-lookup"><span data-stu-id="fc634-226">Size</span></span>
<span data-ttu-id="fc634-227">應用程式資訊受到太**1024年**呼叫每個字元。</span><span class="sxs-lookup"><span data-stu-id="fc634-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="fc634-228">在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="fc634-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="fc634-229">記錄</span><span class="sxs-lookup"><span data-stu-id="fc634-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="fc634-230">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="fc634-230">Enable Logging</span></span>
<span data-ttu-id="fc634-231">hello SDK 可設定的 tooproduce hello IDE 主控台中的測試記錄。</span><span class="sxs-lookup"><span data-stu-id="fc634-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="fc634-232">預設不會啟用這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="fc634-232">These logs are not activated by default.</span></span> <span data-ttu-id="fc634-233">toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`hello 值可從 hello 的 tooone`EngagementTestLogLevel`列舉型別，例如：</span><span class="sxs-lookup"><span data-stu-id="fc634-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
