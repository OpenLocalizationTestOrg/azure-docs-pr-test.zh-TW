---
title: "aaaHow tooUse hello Engagement 通用 Windows API"
description: "如何 tooUse hello Engagement 通用 Windows API"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="bcbe8-103">如何 tooUse hello Engagement 通用 Windows API</span><span class="sxs-lookup"><span data-stu-id="bcbe8-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="bcbe8-104">這份文件是附加元件 toohello 文件[如何 tooIntegrate Engagement 上 Windows 通用](mobile-engagement-windows-store-integrate-engagement.md)： 它會提供有關如何 toouse 會 hello Engagement API tooreport 您的應用程式統計資料的深入詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="bcbe8-105">請記住，如果您只想 Engagement tooreport 應用程式的工作階段、 活動、 當機以及技術資訊，然後 hello 最簡單的方法是 toomake 所有您`Page`子類別是繼承自 hello`EngagementPage`類別。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="bcbe8-106">如果您想 toodo 更多，例如，如果您需要 tooreport 應用程式特定事件、 錯誤與工作，或如果您在非 hello hello 中實作的其中一個 tooreport 應用程式的活動有不同的方式`EngagementPage`類別，則您需要 toouse helloEngagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="bcbe8-107">hello Engagement 應用程式開發介面由提供 hello`EngagementAgent`類別。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="bcbe8-108">您可以存取透過 toothose 方法`EngagementAgent.Instance`。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="bcbe8-109">即使尚未初始化 hello 代理程式的模組，每個呼叫 toohello API 會延後和 hello 代理程式可用時再重新執行。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="bcbe8-110">Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="bcbe8-110">Engagement concepts</span></span>
<span data-ttu-id="bcbe8-111">hello 下列部分精簡 hello 常見[Mobile Engagement 概念](mobile-engagement-concepts.md)hello 通用 Windows 平台。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="bcbe8-112">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="bcbe8-112">`Session` and `Activity`</span></span>
<span data-ttu-id="bcbe8-113">*活動*通常都與一頁的 hello 應用程式，為 toosay hello*活動*hello 頁面隨即出現，而 hello 頁已關閉時停止時啟動： 這是 hello 的情況下如果 helloEngagement SDK 整合使用 hello`EngagementPage`類別。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="bcbe8-114">但是*活動*可以也使用來控制手動 hello Engagement 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="bcbe8-115">這可讓您指定的頁面，在幾個子組件 tooget hello 使用量 （例如 tooknow 頻率和時間的對話方塊內使用，則此頁面） 此頁面的更多詳細的 toosplit。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="bcbe8-116">報告活動</span><span class="sxs-lookup"><span data-stu-id="bcbe8-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="bcbe8-117">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="bcbe8-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-118">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bcbe8-119">您需要 toocall`StartActivity()`變更每個階段 hello 使用者活動。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="bcbe8-120">hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcbe8-121">hello SDK hello 應用程式關閉時，會自動呼叫 hello EndActivity 方法。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="bcbe8-122">因此，強烈建議 toocall hello StartActivity 方法 hello 活動 hello 使用者的變更，以及 hello EndActivity 方法，因為呼叫這個方法會強制 hello 目前工作階段 toobe tooNEVER 呼叫結束時。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="bcbe8-123">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="bcbe8-124">使用者結束其目前的活動</span><span class="sxs-lookup"><span data-stu-id="bcbe8-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-125">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="bcbe8-126">這樣會結束 hello 活動與 hello 工作階段。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="bcbe8-127">除非您真的清楚您的目的，否則不應該呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-128">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="bcbe8-129">報告作業</span><span class="sxs-lookup"><span data-stu-id="bcbe8-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="bcbe8-130">啟動作業</span><span class="sxs-lookup"><span data-stu-id="bcbe8-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-131">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bcbe8-132">經過一段時間，您可以使用 hello tootrack certains 的工作。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-133">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="bcbe8-134">結束作業</span><span class="sxs-lookup"><span data-stu-id="bcbe8-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-135">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="bcbe8-136">只要已終止工作所追蹤的工作，您應該呼叫此作業，hello EndJob 方法藉由提供 hello 作業名稱。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-137">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="bcbe8-138">報告事件</span><span class="sxs-lookup"><span data-stu-id="bcbe8-138">Reporting Events</span></span>
<span data-ttu-id="bcbe8-139">事件有三種類型：</span><span class="sxs-lookup"><span data-stu-id="bcbe8-139">There is three types of events :</span></span>

* <span data-ttu-id="bcbe8-140">獨立事件</span><span class="sxs-lookup"><span data-stu-id="bcbe8-140">Standalone events</span></span>
* <span data-ttu-id="bcbe8-141">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="bcbe8-141">Session events</span></span>
* <span data-ttu-id="bcbe8-142">作業事件</span><span class="sxs-lookup"><span data-stu-id="bcbe8-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="bcbe8-143">獨立事件</span><span class="sxs-lookup"><span data-stu-id="bcbe8-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-144">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bcbe8-145">工作階段的 hello 環境之外發生獨立事件。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-146">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="bcbe8-147">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="bcbe8-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-148">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bcbe8-149">工作階段事件是他的工作階段期間執行使用者通常使用的 tooreport hello 動作。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-150">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-150">Example</span></span>
<span data-ttu-id="bcbe8-151">**沒有資料：**</span><span class="sxs-lookup"><span data-stu-id="bcbe8-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="bcbe8-152">**有資料：**</span><span class="sxs-lookup"><span data-stu-id="bcbe8-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="bcbe8-153">作業事件</span><span class="sxs-lookup"><span data-stu-id="bcbe8-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-154">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="bcbe8-155">作業事件是在作業期間執行使用者通常使用的 tooreport hello 動作。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-156">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="bcbe8-157">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="bcbe8-157">Reporting Errors</span></span>
<span data-ttu-id="bcbe8-158">有三種錯誤類型：</span><span class="sxs-lookup"><span data-stu-id="bcbe8-158">There are three types of errors :</span></span>

* <span data-ttu-id="bcbe8-159">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="bcbe8-159">Standalone errors</span></span>
* <span data-ttu-id="bcbe8-160">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="bcbe8-160">Session errors</span></span>
* <span data-ttu-id="bcbe8-161">作業錯誤</span><span class="sxs-lookup"><span data-stu-id="bcbe8-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="bcbe8-162">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="bcbe8-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-163">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bcbe8-164">反對 toosession，獨立錯誤可能會發生錯誤的工作階段的 hello 內容之外。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-165">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="bcbe8-166">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="bcbe8-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-167">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bcbe8-168">工作階段錯誤是在他的工作階段期間影響 hello 使用者通常使用的 tooreport hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-169">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="bcbe8-170">作業錯誤</span><span class="sxs-lookup"><span data-stu-id="bcbe8-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-171">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="bcbe8-172">錯誤可能是正在執行而不是工作的相關的 tooa 相關 toohello 目前使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-173">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="bcbe8-174">報告當機</span><span class="sxs-lookup"><span data-stu-id="bcbe8-174">Reporting Crashes</span></span>
<span data-ttu-id="bcbe8-175">hello 代理程式會將兩個方法 toodeal 提供當機。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="bcbe8-176">傳送例外狀況</span><span class="sxs-lookup"><span data-stu-id="bcbe8-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-177">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="bcbe8-178">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-178">Example</span></span>
<span data-ttu-id="bcbe8-179">透過呼叫下列函式您可以隨時傳送例外狀況：</span><span class="sxs-lookup"><span data-stu-id="bcbe8-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="bcbe8-180">您也可以使用選擇性參數 tooterminate hello 參與工作階段在 hello 相同的時間比傳送嗨損毀。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="bcbe8-181">因此，呼叫 toodo:</span><span class="sxs-lookup"><span data-stu-id="bcbe8-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="bcbe8-182">如果您這樣做，請只在傳送嗨損毀之後將關閉 hello 工作階段和工作。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="bcbe8-183">傳送未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="bcbe8-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="bcbe8-184">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="bcbe8-185">Engagement 也提供方法 toosend 未處理的例外狀況，如果您有**已停用**Engagement 自動**損毀**報告。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="bcbe8-186">這是 hello 應用程式 UnhandledException 事件處理常式內使用時特別有用。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="bcbe8-187">這個方法將**永遠**呼叫後終止 hello 參與工作階段和工作。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="bcbe8-188">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-188">Example</span></span>
<span data-ttu-id="bcbe8-189">您可以使用它 tooimplement UnhandledExceptionEventArgs 處理常式。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="bcbe8-190">例如，新增 hello`Current_UnhandledException`方法 hello`App.xaml.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="bcbe8-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="bcbe8-191">在 App.xaml.cs 中的 "Public App(){}" 新增：</span><span class="sxs-lookup"><span data-stu-id="bcbe8-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="bcbe8-192">裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="bcbe8-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="bcbe8-193">您可以藉由呼叫這個方法來取得 hello engagement 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="bcbe8-194">額外的參數</span><span class="sxs-lookup"><span data-stu-id="bcbe8-194">Extras parameters</span></span>
<span data-ttu-id="bcbe8-195">附加的 tooan 事件、 錯誤、 活動或工作，可以是任意的資料。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="bcbe8-196">可以使用字典來結構化這些資料。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="bcbe8-197">索引鍵和值可以是任何型別。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="bcbe8-198">額外項目資料會序列化，因此如果您想 tooinsert 自己的額外項目中的型別必須 tooadd 這種類型的資料合約。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="bcbe8-199">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-199">Example</span></span>
<span data-ttu-id="bcbe8-200">我們建立一個新的類別叫 "Person"。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="bcbe8-201">然後，我們會加入`Person`額外的執行個體 tooan。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="bcbe8-202">如果您將其他類型的物件，請確定其 tostring （） 方法是實作的 tooreturn 人類可讀取的字串。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="bcbe8-203">限制</span><span class="sxs-lookup"><span data-stu-id="bcbe8-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="bcbe8-204">之間的信任</span><span class="sxs-lookup"><span data-stu-id="bcbe8-204">Keys</span></span>
<span data-ttu-id="bcbe8-205">Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="bcbe8-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="bcbe8-206">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="bcbe8-207">大小</span><span class="sxs-lookup"><span data-stu-id="bcbe8-207">Size</span></span>
<span data-ttu-id="bcbe8-208">額外項目會受到限制太**1024年**呼叫每個字元。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="bcbe8-209">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="bcbe8-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="bcbe8-210">參考</span><span class="sxs-lookup"><span data-stu-id="bcbe8-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="bcbe8-211">您可以手動報告追蹤資訊 （或任何其他應用程式特定資訊） 使用 hello SendAppInfo() 函式。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="bcbe8-212">請注意，此資料可以累加地傳送： 只有 hello 最新的值指定索引鍵將會保留指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="bcbe8-213">事件的額外功能，例如使用字典\<物件，物件\>tooattach 資料。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="bcbe8-214">範例</span><span class="sxs-lookup"><span data-stu-id="bcbe8-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="bcbe8-215">限制</span><span class="sxs-lookup"><span data-stu-id="bcbe8-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="bcbe8-216">之間的信任</span><span class="sxs-lookup"><span data-stu-id="bcbe8-216">Keys</span></span>
<span data-ttu-id="bcbe8-217">Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="bcbe8-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="bcbe8-218">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="bcbe8-219">大小</span><span class="sxs-lookup"><span data-stu-id="bcbe8-219">Size</span></span>
<span data-ttu-id="bcbe8-220">應用程式的資訊也很有限**1024年**呼叫每個字元。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="bcbe8-221">在 hello 上述範例中，JSON 傳送 toohello 伺服器 hello 是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="bcbe8-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="bcbe8-222">記錄</span><span class="sxs-lookup"><span data-stu-id="bcbe8-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="bcbe8-223">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="bcbe8-223">Enable Logging</span></span>
<span data-ttu-id="bcbe8-224">hello SDK 可設定的 tooproduce hello IDE 主控台中的測試記錄。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="bcbe8-225">預設不會啟用這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="bcbe8-225">These logs are not activated by default.</span></span> <span data-ttu-id="bcbe8-226">toocustomize，更新 hello 屬性`EngagementAgent.Instance.TestLogEnabled`hello 值可從 hello 的 tooone`EngagementTestLogLevel`列舉型別，例如：</span><span class="sxs-lookup"><span data-stu-id="bcbe8-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

