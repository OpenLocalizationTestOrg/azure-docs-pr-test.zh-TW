---
title: "如何在 Windows 通用上使用 Engagement API"
description: "如何在 Windows 通用上使用 Engagement API"
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
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="00410-103">如何在 Windows 通用上使用 Engagement API</span><span class="sxs-lookup"><span data-stu-id="00410-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="00410-104">此文件為 [如何在 Windows 通用上整合 Engagement](mobile-engagement-windows-store-integrate-engagement.md)的附加說明：它提供有關如何使用 Engagement API 來報告應用程式的統計資料之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="00410-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="00410-105">請記住，如果您只想要 Engagement 向您報告應用程式的工作階段、活動、當機和技術資訊，那麼最簡單的方法是讓所有 `Page` 子類別繼承自 `EngagementPage` 類別。</span><span class="sxs-lookup"><span data-stu-id="00410-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="00410-106">如果您想要執行更多工作 (例如，若您需要報告應用程式的特定事件、錯誤和作業，或者您需要以不同於 `EngagementPage` 類別中的方式來報告應用程式的活動)，則您需要使用 Engagement API。</span><span class="sxs-lookup"><span data-stu-id="00410-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="00410-107">Engagement API 是由 `EngagementAgent` 類別提供。</span><span class="sxs-lookup"><span data-stu-id="00410-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="00410-108">您可以透過 `EngagementAgent.Instance`取得這些方法。</span><span class="sxs-lookup"><span data-stu-id="00410-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="00410-109">檔代理程式模組尚未初始化時，每個對 API 的呼叫會被延後，並且將於代理程式可使用時再次執行。</span><span class="sxs-lookup"><span data-stu-id="00410-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="00410-110">Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="00410-110">Engagement concepts</span></span>
<span data-ttu-id="00410-111">以下部分簡要說明適用於 Windows 通用平台的常見 [Mobile Engagement 概念](mobile-engagement-concepts.md) 。</span><span class="sxs-lookup"><span data-stu-id="00410-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="00410-112">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="00410-112">`Session` and `Activity`</span></span>
<span data-ttu-id="00410-113">「活動」通常與應用程式的某個頁面關聯，也就是說，「活動」會在頁面顯示時啟動，當頁面關閉時就停止：使用 `EngagementPage` 類別來整合 Engagement SDK 的情況便是如此。</span><span class="sxs-lookup"><span data-stu-id="00410-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="00410-114">但您也可以透過 Engagement API 手動控制「活動」  。</span><span class="sxs-lookup"><span data-stu-id="00410-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="00410-115">這樣可允許您將指定的頁面分割成多個部分，以獲得有關該頁面使用方式的詳細資訊 (例如，對話方塊在此頁面的使用平率和使用時間)。</span><span class="sxs-lookup"><span data-stu-id="00410-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="00410-116">報告活動</span><span class="sxs-lookup"><span data-stu-id="00410-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="00410-117">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="00410-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-118">參考</span><span class="sxs-lookup"><span data-stu-id="00410-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="00410-119">每當使用者活動變更，您就需要呼叫 `StartActivity()` 。</span><span class="sxs-lookup"><span data-stu-id="00410-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="00410-120">第一次呼叫此函數會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="00410-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00410-121">當應用程式關閉時，SDK 會自動呼叫 EndActivity 方法。</span><span class="sxs-lookup"><span data-stu-id="00410-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="00410-122">因此，「強烈」建議每當使用者的活動變更時便叫呼叫 StartActivity 方法，並且「絕對不要」呼叫 EndActivity 方法，因為呼叫此方法會強制結束目前的工作階段。</span><span class="sxs-lookup"><span data-stu-id="00410-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="00410-123">範例</span><span class="sxs-lookup"><span data-stu-id="00410-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="00410-124">使用者結束其目前的活動</span><span class="sxs-lookup"><span data-stu-id="00410-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-125">參考</span><span class="sxs-lookup"><span data-stu-id="00410-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="00410-126">這樣會結束活動和工作階段。</span><span class="sxs-lookup"><span data-stu-id="00410-126">This ends the activity and the session.</span></span> <span data-ttu-id="00410-127">除非您真的清楚您的目的，否則不應該呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="00410-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-128">範例</span><span class="sxs-lookup"><span data-stu-id="00410-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="00410-129">報告作業</span><span class="sxs-lookup"><span data-stu-id="00410-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="00410-130">啟動作業</span><span class="sxs-lookup"><span data-stu-id="00410-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-131">參考</span><span class="sxs-lookup"><span data-stu-id="00410-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="00410-132">您可以使用作業在一段時間內追蹤某些工作。</span><span class="sxs-lookup"><span data-stu-id="00410-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-133">範例</span><span class="sxs-lookup"><span data-stu-id="00410-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="00410-134">結束作業</span><span class="sxs-lookup"><span data-stu-id="00410-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-135">參考</span><span class="sxs-lookup"><span data-stu-id="00410-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="00410-136">一旦作業追蹤的工作被終止，您就應該針對該作業呼叫 EndJob 方法 (透過提供該作業名稱)。</span><span class="sxs-lookup"><span data-stu-id="00410-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-137">範例</span><span class="sxs-lookup"><span data-stu-id="00410-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="00410-138">報告事件</span><span class="sxs-lookup"><span data-stu-id="00410-138">Reporting Events</span></span>
<span data-ttu-id="00410-139">事件有三種類型：</span><span class="sxs-lookup"><span data-stu-id="00410-139">There is three types of events :</span></span>

* <span data-ttu-id="00410-140">獨立事件</span><span class="sxs-lookup"><span data-stu-id="00410-140">Standalone events</span></span>
* <span data-ttu-id="00410-141">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="00410-141">Session events</span></span>
* <span data-ttu-id="00410-142">作業事件</span><span class="sxs-lookup"><span data-stu-id="00410-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="00410-143">獨立事件</span><span class="sxs-lookup"><span data-stu-id="00410-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-144">參考</span><span class="sxs-lookup"><span data-stu-id="00410-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="00410-145">獨立事件可以出現在工作階段的內容之外。</span><span class="sxs-lookup"><span data-stu-id="00410-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-146">範例</span><span class="sxs-lookup"><span data-stu-id="00410-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="00410-147">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="00410-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-148">參考</span><span class="sxs-lookup"><span data-stu-id="00410-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="00410-149">工作階段事件通常用來報告在其工作階段期間由使用者所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="00410-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-150">範例</span><span class="sxs-lookup"><span data-stu-id="00410-150">Example</span></span>
<span data-ttu-id="00410-151">**沒有資料：**</span><span class="sxs-lookup"><span data-stu-id="00410-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="00410-152">**有資料：**</span><span class="sxs-lookup"><span data-stu-id="00410-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="00410-153">作業事件</span><span class="sxs-lookup"><span data-stu-id="00410-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-154">參考</span><span class="sxs-lookup"><span data-stu-id="00410-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="00410-155">作業事件通常用來報告在作業期間由使用者所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="00410-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-156">範例</span><span class="sxs-lookup"><span data-stu-id="00410-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="00410-157">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="00410-157">Reporting Errors</span></span>
<span data-ttu-id="00410-158">有三種錯誤類型：</span><span class="sxs-lookup"><span data-stu-id="00410-158">There are three types of errors :</span></span>

* <span data-ttu-id="00410-159">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="00410-159">Standalone errors</span></span>
* <span data-ttu-id="00410-160">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="00410-160">Session errors</span></span>
* <span data-ttu-id="00410-161">作業錯誤</span><span class="sxs-lookup"><span data-stu-id="00410-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="00410-162">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="00410-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-163">參考</span><span class="sxs-lookup"><span data-stu-id="00410-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="00410-164">不同於工作階段錯誤，獨立錯誤可以出現在工作階段的內容之外。</span><span class="sxs-lookup"><span data-stu-id="00410-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-165">範例</span><span class="sxs-lookup"><span data-stu-id="00410-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="00410-166">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="00410-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-167">參考</span><span class="sxs-lookup"><span data-stu-id="00410-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="00410-168">工作階段錯誤通常用來報告在其工作階段期間影響使用者的錯誤。</span><span class="sxs-lookup"><span data-stu-id="00410-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-169">範例</span><span class="sxs-lookup"><span data-stu-id="00410-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="00410-170">作業錯誤</span><span class="sxs-lookup"><span data-stu-id="00410-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-171">參考</span><span class="sxs-lookup"><span data-stu-id="00410-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="00410-172">錯誤可能與正在執行的工作關聯，而不是與目前的使用者工作階段關聯。</span><span class="sxs-lookup"><span data-stu-id="00410-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-173">範例</span><span class="sxs-lookup"><span data-stu-id="00410-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="00410-174">報告當機</span><span class="sxs-lookup"><span data-stu-id="00410-174">Reporting Crashes</span></span>
<span data-ttu-id="00410-175">代理程式提供兩種處理當機的方法。</span><span class="sxs-lookup"><span data-stu-id="00410-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="00410-176">傳送例外狀況</span><span class="sxs-lookup"><span data-stu-id="00410-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-177">參考</span><span class="sxs-lookup"><span data-stu-id="00410-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="00410-178">範例</span><span class="sxs-lookup"><span data-stu-id="00410-178">Example</span></span>
<span data-ttu-id="00410-179">透過呼叫下列函式您可以隨時傳送例外狀況：</span><span class="sxs-lookup"><span data-stu-id="00410-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="00410-180">您也可以使用選擇性的參數來同時結束參與工作階段並傳送當機。</span><span class="sxs-lookup"><span data-stu-id="00410-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="00410-181">若要這樣做，請呼叫：</span><span class="sxs-lookup"><span data-stu-id="00410-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="00410-182">如果您這樣做，工作階段和作業將於傳送當機後立即關閉。</span><span class="sxs-lookup"><span data-stu-id="00410-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="00410-183">傳送未處理的例外狀況</span><span class="sxs-lookup"><span data-stu-id="00410-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="00410-184">參考</span><span class="sxs-lookup"><span data-stu-id="00410-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="00410-185">如果您「已經停用」Engagement 自動當機報告，Engagement 也會提供傳送未處理例外狀況的方法。</span><span class="sxs-lookup"><span data-stu-id="00410-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="00410-186">在應用程式的 UnhandledException 事件處理常式內此方法特別有用。</span><span class="sxs-lookup"><span data-stu-id="00410-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="00410-187">此方法「一律」  會在被呼叫之後終止 Engagement 工作階段和作業。</span><span class="sxs-lookup"><span data-stu-id="00410-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="00410-188">範例</span><span class="sxs-lookup"><span data-stu-id="00410-188">Example</span></span>
<span data-ttu-id="00410-189">您可以使用它來實作您自己的 UnhandledExceptionEventArgs 處理常式。</span><span class="sxs-lookup"><span data-stu-id="00410-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="00410-190">例如，新增 `App.xaml.cs` 檔案的 `Current_UnhandledException` 方法：</span><span class="sxs-lookup"><span data-stu-id="00410-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="00410-191">在 App.xaml.cs 中的 "Public App(){}" 新增：</span><span class="sxs-lookup"><span data-stu-id="00410-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="00410-192">裝置識別碼</span><span class="sxs-lookup"><span data-stu-id="00410-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="00410-193">您可以藉由呼叫這個方法來取得 Egagement 的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="00410-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="00410-194">額外的參數</span><span class="sxs-lookup"><span data-stu-id="00410-194">Extras parameters</span></span>
<span data-ttu-id="00410-195">可以附加任意資料到事件、錯誤、活動或作業。</span><span class="sxs-lookup"><span data-stu-id="00410-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="00410-196">可以使用字典來結構化這些資料。</span><span class="sxs-lookup"><span data-stu-id="00410-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="00410-197">索引鍵和值可以是任何型別。</span><span class="sxs-lookup"><span data-stu-id="00410-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="00410-198">額外的資料已經序列化，因此如果您想要在額外資料中插入您自己的型別，您必須針對此型別新增資料合約。</span><span class="sxs-lookup"><span data-stu-id="00410-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="00410-199">範例</span><span class="sxs-lookup"><span data-stu-id="00410-199">Example</span></span>
<span data-ttu-id="00410-200">我們建立一個新的類別叫 "Person"。</span><span class="sxs-lookup"><span data-stu-id="00410-200">We create a new class "Person".</span></span>

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

<span data-ttu-id="00410-201">然後將 `Person` 執行個體新增至額外資料。</span><span class="sxs-lookup"><span data-stu-id="00410-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="00410-202">如果您新增其他類型的物件，請確定已實作它們的 ToString() 方法，以傳回使用者可閱讀的字串。</span><span class="sxs-lookup"><span data-stu-id="00410-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="00410-203">限制</span><span class="sxs-lookup"><span data-stu-id="00410-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="00410-204">之間的信任</span><span class="sxs-lookup"><span data-stu-id="00410-204">Keys</span></span>
<span data-ttu-id="00410-205">物件中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="00410-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="00410-206">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="00410-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="00410-207">大小</span><span class="sxs-lookup"><span data-stu-id="00410-207">Size</span></span>
<span data-ttu-id="00410-208">每次呼叫的額外資料限制為 **1024** 個字元。</span><span class="sxs-lookup"><span data-stu-id="00410-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="00410-209">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="00410-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="00410-210">參考</span><span class="sxs-lookup"><span data-stu-id="00410-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="00410-211">您可以使用 SendAppInfo() 函式來報告追蹤資訊 (或任何其他應用程式相關的資訊)。</span><span class="sxs-lookup"><span data-stu-id="00410-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="00410-212">請注意，此項資料可以累加地傳送：只有指定的索引鍵的最新值會保留給指定的裝置。</span><span class="sxs-lookup"><span data-stu-id="00410-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="00410-213">和事件額外資料一樣，請使用 Dictionary\<object, object\> 來附加資料。</span><span class="sxs-lookup"><span data-stu-id="00410-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="00410-214">範例</span><span class="sxs-lookup"><span data-stu-id="00410-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="00410-215">限制</span><span class="sxs-lookup"><span data-stu-id="00410-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="00410-216">之間的信任</span><span class="sxs-lookup"><span data-stu-id="00410-216">Keys</span></span>
<span data-ttu-id="00410-217">物件中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="00410-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="00410-218">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="00410-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="00410-219">大小</span><span class="sxs-lookup"><span data-stu-id="00410-219">Size</span></span>
<span data-ttu-id="00410-220">每次呼叫的應用程式資訊限制為 **1024** 個字元。</span><span class="sxs-lookup"><span data-stu-id="00410-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="00410-221">在上述範例中，傳送到伺服器的 JSON 會是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="00410-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="00410-222">記錄</span><span class="sxs-lookup"><span data-stu-id="00410-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="00410-223">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="00410-223">Enable Logging</span></span>
<span data-ttu-id="00410-224">SDK 可以設定為在 IDE 主控台中產生測試記錄檔。</span><span class="sxs-lookup"><span data-stu-id="00410-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="00410-225">預設不會啟用這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="00410-225">These logs are not activated by default.</span></span> <span data-ttu-id="00410-226">若要自訂這種情況，請將屬性 `EngagementAgent.Instance.TestLogEnabled` 更新為 `EngagementTestLogLevel` 列舉的其中一個可用值，例如︰</span><span class="sxs-lookup"><span data-stu-id="00410-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

