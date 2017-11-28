---
title: "如何在 Windows Phone Silverlight 上使用 Engagement API"
description: "如何在 Windows Phone Silverlight 上使用 Engagement API"
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
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="14728-103">如何在 Windows Phone Silverlight 上使用 Engagement API</span><span class="sxs-lookup"><span data-stu-id="14728-103">How to Use the Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="14728-104">此文件是 [如何在 Windows Phone Silverlight 應用程式中整合 Mobile Engagement](mobile-engagement-windows-phone-integrate-engagement.md)文件的附加說明。</span><span class="sxs-lookup"><span data-stu-id="14728-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="14728-105">它會提供關於如何使用 Engagement API 來回報您應用程式的統計資料之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="14728-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="14728-106">如果您只想要 Engagement 報告應用程式的工作階段、活動、當機和技術資訊，最簡單的方式就是讓您所有的 `PhoneApplicationPage` 子類別繼承自 `EngagementPage` 類別。</span><span class="sxs-lookup"><span data-stu-id="14728-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="14728-107">如果您想要執行更多工作 (例如，若您需要報告應用程式的特定事件、錯誤和作業，或者您需要以不同於 `EngagementPage` 類別中的方式來報告應用程式的活動)，則您需要使用 Engagement API。</span><span class="sxs-lookup"><span data-stu-id="14728-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="14728-108">Engagement API 是由 `EngagementAgent` 類別提供。</span><span class="sxs-lookup"><span data-stu-id="14728-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="14728-109">您可以透過 `EngagementAgent.Instance`取得這些方法。</span><span class="sxs-lookup"><span data-stu-id="14728-109">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="14728-110">檔代理程式模組尚未初始化時，每個對 API 的呼叫會被延後，並且將於代理程式可使用時再次執行。</span><span class="sxs-lookup"><span data-stu-id="14728-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="14728-111">Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="14728-111">Engagement concepts</span></span>
<span data-ttu-id="14728-112">以下部分簡要說明適用於 Windows Phone 平台的 Mobile Engagement 概念。</span><span class="sxs-lookup"><span data-stu-id="14728-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="14728-113">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="14728-113">`Session` and `Activity`</span></span>
<span data-ttu-id="14728-114">「活動」通常與應用程式的某個頁面關聯，也就是說，「活動」會在頁面顯示時啟動，當頁面關閉時就停止：使用 `EngagementPage` 類別來整合 Engagement SDK 的情況便是如此。</span><span class="sxs-lookup"><span data-stu-id="14728-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="14728-115">但您也可以透過 Engagement API 手動控制「活動」  。</span><span class="sxs-lookup"><span data-stu-id="14728-115">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="14728-116">這樣可允許將指定的頁面分割成多個部分，以獲得有關該頁面使用方式的詳細資訊 (例如，對話方塊在此頁面的使用平率和使用時間)。</span><span class="sxs-lookup"><span data-stu-id="14728-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="14728-117">報告活動</span><span class="sxs-lookup"><span data-stu-id="14728-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="14728-118">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="14728-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-119">參考</span><span class="sxs-lookup"><span data-stu-id="14728-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14728-120">每當使用者活動變更，您就需要呼叫 `StartActivity()` 。</span><span class="sxs-lookup"><span data-stu-id="14728-120">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="14728-121">第一次呼叫此函式會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="14728-121">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14728-122">當應用程式關閉時，SDK 會自動呼叫 EndActivity 方法。</span><span class="sxs-lookup"><span data-stu-id="14728-122">The SDK automatically call the EndActivity method when the application is closed.</span></span> <span data-ttu-id="14728-123">因此，「強烈」建議每當使用者的活動變更時便叫呼叫 StartActivity 方法，並且「絕對不要」呼叫 EndActivity 方法，因為呼叫此方法會強制結束目前的工作階段。</span><span class="sxs-lookup"><span data-stu-id="14728-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="14728-124">範例</span><span class="sxs-lookup"><span data-stu-id="14728-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="14728-125">使用者結束其目前的活動</span><span class="sxs-lookup"><span data-stu-id="14728-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-126">參考</span><span class="sxs-lookup"><span data-stu-id="14728-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="14728-127">使用者完成最後一個活動時，您至少需要呼叫 `EndActivity()` 一次。</span><span class="sxs-lookup"><span data-stu-id="14728-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="14728-128">這會通知 Engagement SDK，說明使用者目前處於閒置狀態，且工作階段逾時到期時就得關閉使用者工作階段 (如果您在工作階段逾時到期前就呼叫 `StartActivity()` ，工作階段只會繼續)。</span><span class="sxs-lookup"><span data-stu-id="14728-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="14728-129">範例</span><span class="sxs-lookup"><span data-stu-id="14728-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="14728-130">報告作業</span><span class="sxs-lookup"><span data-stu-id="14728-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="14728-131">啟動作業</span><span class="sxs-lookup"><span data-stu-id="14728-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-132">參考</span><span class="sxs-lookup"><span data-stu-id="14728-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14728-133">您可以使用作業在一段時間內追蹤某些工作。</span><span class="sxs-lookup"><span data-stu-id="14728-133">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-134">範例</span><span class="sxs-lookup"><span data-stu-id="14728-134">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="14728-135">結束作業</span><span class="sxs-lookup"><span data-stu-id="14728-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-136">參考</span><span class="sxs-lookup"><span data-stu-id="14728-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="14728-137">一旦作業追蹤的工作被終止，您就應該針對該作業呼叫 EndJob 方法 (透過提供該作業名稱)。</span><span class="sxs-lookup"><span data-stu-id="14728-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-138">範例</span><span class="sxs-lookup"><span data-stu-id="14728-138">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="14728-139">報告事件</span><span class="sxs-lookup"><span data-stu-id="14728-139">Reporting Events</span></span>
<span data-ttu-id="14728-140">事件有三種類型：</span><span class="sxs-lookup"><span data-stu-id="14728-140">There is three types of events :</span></span>

* <span data-ttu-id="14728-141">獨立事件</span><span class="sxs-lookup"><span data-stu-id="14728-141">Standalone events</span></span>
* <span data-ttu-id="14728-142">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="14728-142">Session events</span></span>
* <span data-ttu-id="14728-143">作業事件</span><span class="sxs-lookup"><span data-stu-id="14728-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="14728-144">獨立事件</span><span class="sxs-lookup"><span data-stu-id="14728-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-145">參考</span><span class="sxs-lookup"><span data-stu-id="14728-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14728-146">獨立事件可以出現在工作階段的內容之外。</span><span class="sxs-lookup"><span data-stu-id="14728-146">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-147">範例</span><span class="sxs-lookup"><span data-stu-id="14728-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="14728-148">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="14728-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-149">參考</span><span class="sxs-lookup"><span data-stu-id="14728-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14728-150">工作階段事件通常用來報告在其工作階段期間由使用者所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="14728-150">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-151">範例</span><span class="sxs-lookup"><span data-stu-id="14728-151">Example</span></span>
<span data-ttu-id="14728-152">**沒有資料：**</span><span class="sxs-lookup"><span data-stu-id="14728-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="14728-153">**有資料：**</span><span class="sxs-lookup"><span data-stu-id="14728-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="14728-154">作業事件</span><span class="sxs-lookup"><span data-stu-id="14728-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-155">參考</span><span class="sxs-lookup"><span data-stu-id="14728-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="14728-156">作業事件通常用來報告在作業期間由使用者所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="14728-156">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-157">範例</span><span class="sxs-lookup"><span data-stu-id="14728-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="14728-158">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="14728-158">Reporting Errors</span></span>
<span data-ttu-id="14728-159">錯誤有三種類型：</span><span class="sxs-lookup"><span data-stu-id="14728-159">There is three types of errors :</span></span>

* <span data-ttu-id="14728-160">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="14728-160">Standalone errors</span></span>
* <span data-ttu-id="14728-161">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="14728-161">Session errors</span></span>
* <span data-ttu-id="14728-162">作業錯誤</span><span class="sxs-lookup"><span data-stu-id="14728-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="14728-163">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="14728-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-164">參考</span><span class="sxs-lookup"><span data-stu-id="14728-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14728-165">不同於工作階段錯誤，獨立錯誤可以出現在工作階段的內容之外。</span><span class="sxs-lookup"><span data-stu-id="14728-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-166">範例</span><span class="sxs-lookup"><span data-stu-id="14728-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="14728-167">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="14728-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-168">參考</span><span class="sxs-lookup"><span data-stu-id="14728-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14728-169">工作階段錯誤通常用來報告在其工作階段期間影響使用者的錯誤。</span><span class="sxs-lookup"><span data-stu-id="14728-169">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-170">範例</span><span class="sxs-lookup"><span data-stu-id="14728-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="14728-171">作業錯誤</span><span class="sxs-lookup"><span data-stu-id="14728-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-172">參考</span><span class="sxs-lookup"><span data-stu-id="14728-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="14728-173">錯誤可能與正在執行的工作關聯，而不是與目前的使用者工作階段關聯。</span><span class="sxs-lookup"><span data-stu-id="14728-173">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-174">範例</span><span class="sxs-lookup"><span data-stu-id="14728-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="14728-175">報告當機</span><span class="sxs-lookup"><span data-stu-id="14728-175">Reporting Crashes</span></span>
<span data-ttu-id="14728-176">代理程式提供兩種處理當機的方法。</span><span class="sxs-lookup"><span data-stu-id="14728-176">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="14728-177">傳送例外狀況</span><span class="sxs-lookup"><span data-stu-id="14728-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-178">參考</span><span class="sxs-lookup"><span data-stu-id="14728-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="14728-179">範例</span><span class="sxs-lookup"><span data-stu-id="14728-179">Example</span></span>
<span data-ttu-id="14728-180">透過呼叫下列函式您可以隨時傳送例外狀況：</span><span class="sxs-lookup"><span data-stu-id="14728-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="14728-181">您也可以使用選擇性的參數來同時結束參與工作階段並傳送當機。</span><span class="sxs-lookup"><span data-stu-id="14728-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="14728-182">若要這樣做，請呼叫：</span><span class="sxs-lookup"><span data-stu-id="14728-182">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="14728-183">如果您這樣做，工作階段和作業將於傳送當機後立即關閉。</span><span class="sxs-lookup"><span data-stu-id="14728-183">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="14728-184">傳送未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="14728-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="14728-185">參考</span><span class="sxs-lookup"><span data-stu-id="14728-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="14728-186">Engagement 也提供將傳送未處理的例外狀況之方法。</span><span class="sxs-lookup"><span data-stu-id="14728-186">Engagement also provides a method to send unhandled exceptions.</span></span> <span data-ttu-id="14728-187">在 Silverlight 的 UnhandledException 事件處理常式內此方法特別有用。</span><span class="sxs-lookup"><span data-stu-id="14728-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="14728-188">此方法「一律」  會在被呼叫之後終止 Engagement 工作階段和作業。</span><span class="sxs-lookup"><span data-stu-id="14728-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="14728-189">範例</span><span class="sxs-lookup"><span data-stu-id="14728-189">Example</span></span>
<span data-ttu-id="14728-190">您可以使用它來實作您自己的 UnhandledException 處理常式 (尤其是如果您已停用 Engagement 的自動損毀報告功能)。</span><span class="sxs-lookup"><span data-stu-id="14728-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="14728-191">例如在 `App.xaml.cs` 檔案的 `Application_UnhandledException` 方法中：</span><span class="sxs-lookup"><span data-stu-id="14728-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="14728-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="14728-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="14728-193">參考</span><span class="sxs-lookup"><span data-stu-id="14728-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="14728-194">當使用者繼續瀏覽並離開應用程式的時候，作業系統會在 Deactivated 事件引發之後嘗試讓應用程式進入休眠狀態。</span><span class="sxs-lookup"><span data-stu-id="14728-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span></span> <span data-ttu-id="14728-195">然後該應用程式會被加上刪除標記。</span><span class="sxs-lookup"><span data-stu-id="14728-195">Then, the application is Tombstoning.</span></span> <span data-ttu-id="14728-196">此程序中的映欲程式會被終止，但會保留某些和應用程式狀態與個別頁面有關的資料。</span><span class="sxs-lookup"><span data-stu-id="14728-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span></span>

<span data-ttu-id="14728-197">您必須將 `EngagementAgent.Instance.OnActivated(e)` 插入來自 App.xaml.cs 檔案的 `Application_Activated` 方法中，以在應用程式被加上刪除標記時重設 Engagement 代理程式。</span><span class="sxs-lookup"><span data-stu-id="14728-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="14728-198">範例</span><span class="sxs-lookup"><span data-stu-id="14728-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="14728-199">裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="14728-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="14728-200">您可以藉由呼叫這個方法來取得 Egagement 的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="14728-200">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="14728-201">額外的參數</span><span class="sxs-lookup"><span data-stu-id="14728-201">Extras parameters</span></span>
<span data-ttu-id="14728-202">可以附加任意資料到事件、錯誤、活動或作業。</span><span class="sxs-lookup"><span data-stu-id="14728-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="14728-203">可以使用字典來結構化這些資料。</span><span class="sxs-lookup"><span data-stu-id="14728-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="14728-204">索引鍵和值可以是任何型別。</span><span class="sxs-lookup"><span data-stu-id="14728-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="14728-205">額外的資料已經序列化，因此如果您想要在額外資料中插入您自己的型別，您必須針對此型別新增資料合約。</span><span class="sxs-lookup"><span data-stu-id="14728-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="14728-206">範例</span><span class="sxs-lookup"><span data-stu-id="14728-206">Example</span></span>
<span data-ttu-id="14728-207">我們建立一個新的類別叫 "Person"。</span><span class="sxs-lookup"><span data-stu-id="14728-207">We create a new class "Person".</span></span>

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

<span data-ttu-id="14728-208">然後將 `Person` 執行個體新增至額外資料。</span><span class="sxs-lookup"><span data-stu-id="14728-208">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="14728-209">如果您新增其他類型的物件，請確定已實作它們的 ToString() 方法，以傳回使用者可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="14728-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="14728-210">限制</span><span class="sxs-lookup"><span data-stu-id="14728-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="14728-211">之間的信任</span><span class="sxs-lookup"><span data-stu-id="14728-211">Keys</span></span>
<span data-ttu-id="14728-212">物件中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="14728-212">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="14728-213">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="14728-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="14728-214">大小</span><span class="sxs-lookup"><span data-stu-id="14728-214">Size</span></span>
<span data-ttu-id="14728-215">每次呼叫的額外資料限制為 **1024** 個字元。</span><span class="sxs-lookup"><span data-stu-id="14728-215">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="14728-216">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="14728-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="14728-217">參考</span><span class="sxs-lookup"><span data-stu-id="14728-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="14728-218">您可以使用 SendAppInfo() 函式來報告追蹤資訊 (或任何其他應用程式相關的資訊)。</span><span class="sxs-lookup"><span data-stu-id="14728-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="14728-219">請注意，這些資訊可以累加地傳送：只有指定的索引鍵的最新值會保留給指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="14728-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="14728-220">和事件額外資料一樣，請使用 Dictionary\<object, object\> 來附加資訊。</span><span class="sxs-lookup"><span data-stu-id="14728-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span></span>

### <a name="example"></a><span data-ttu-id="14728-221">範例</span><span class="sxs-lookup"><span data-stu-id="14728-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="14728-222">限制</span><span class="sxs-lookup"><span data-stu-id="14728-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="14728-223">之間的信任</span><span class="sxs-lookup"><span data-stu-id="14728-223">Keys</span></span>
<span data-ttu-id="14728-224">物件中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="14728-224">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="14728-225">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="14728-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="14728-226">大小</span><span class="sxs-lookup"><span data-stu-id="14728-226">Size</span></span>
<span data-ttu-id="14728-227">每次呼叫的應用程式資訊限制為 **1024** 個字元。</span><span class="sxs-lookup"><span data-stu-id="14728-227">Application information are limited to **1024** characters per call.</span></span>

<span data-ttu-id="14728-228">在上述範例中，傳送到伺服器的 JSON 會是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="14728-228">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="14728-229">記錄</span><span class="sxs-lookup"><span data-stu-id="14728-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="14728-230">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="14728-230">Enable Logging</span></span>
<span data-ttu-id="14728-231">SDK 可以設定為在 IDE 主控台中產生測試記錄檔。</span><span class="sxs-lookup"><span data-stu-id="14728-231">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="14728-232">預設不會啟用這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="14728-232">These logs are not activated by default.</span></span> <span data-ttu-id="14728-233">若要自訂這種情況，請將屬性 `EngagementAgent.Instance.TestLogEnabled` 更新為 `EngagementTestLogLevel` 列舉的其中一個可用值，例如︰</span><span class="sxs-lookup"><span data-stu-id="14728-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
