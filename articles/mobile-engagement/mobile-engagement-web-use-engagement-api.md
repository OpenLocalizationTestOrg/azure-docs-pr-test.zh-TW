---
title: Azure Mobile Engagement Web SDK API | Microsoft Docs
description: "Azure Mobile Engagement Web SDK 的最新更新與程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="af3f8-103">在 Web 應用程式中使用 Azure Mobile Engagement API</span><span class="sxs-lookup"><span data-stu-id="af3f8-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="af3f8-104">此文件是文件的補充，說明如何 [在您的 Web 應用程式中整合 Mobile Engagement](mobile-engagement-web-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="af3f8-105">它會提供關於如何使用 Azure Mobile Engagement API 來回報您應用程式的統計資料之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="af3f8-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="af3f8-106">Mobile Engagement API 是由 `engagement.agent` 物件提供。</span><span class="sxs-lookup"><span data-stu-id="af3f8-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="af3f8-107">預設 Azure Mobile Engagement Web SDK 別名是 `engagement`。</span><span class="sxs-lookup"><span data-stu-id="af3f8-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="af3f8-108">您可以從 SDK 組態來重新定義此別名。</span><span class="sxs-lookup"><span data-stu-id="af3f8-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="af3f8-109">Mobile Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="af3f8-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="af3f8-110">以下部分簡要說明適用於 Web 平台的 [Mobile Engagement 概念](mobile-engagement-concepts.md) 。</span><span class="sxs-lookup"><span data-stu-id="af3f8-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="af3f8-111">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="af3f8-111">`Session` and `Activity`</span></span>
<span data-ttu-id="af3f8-112">如果使用者在兩個活動之間維持閒置超過幾秒鐘，其活動序列會分割成兩個相異的工作階段。</span><span class="sxs-lookup"><span data-stu-id="af3f8-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="af3f8-113">這幾秒被稱為工作階段逾時。</span><span class="sxs-lookup"><span data-stu-id="af3f8-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="af3f8-114">如果您的 Web 應用程式不自行宣告使用者活動的結束 (透過呼叫 `engagement.agent.endActivity` 函式)，Mobile Engagement 伺服器將會在應用程式頁面關閉後的 3 分鐘之內自動讓使用者工作階段到期。</span><span class="sxs-lookup"><span data-stu-id="af3f8-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="af3f8-115">這被稱為伺服器工作階段逾時。</span><span class="sxs-lookup"><span data-stu-id="af3f8-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="af3f8-116">根據預設，不會建立無法攔截的 JavaScript 例外狀況的自動報告。</span><span class="sxs-lookup"><span data-stu-id="af3f8-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="af3f8-117">不過，您可以透過使用 `sendCrash` 函式來手動報告當機 (請參閱報告當機的章節)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="af3f8-118">報告活動</span><span class="sxs-lookup"><span data-stu-id="af3f8-118">Reporting activities</span></span>
<span data-ttu-id="af3f8-119">使用者啟動新的活動以及使用者結束目前活動時報告使用者活動。</span><span class="sxs-lookup"><span data-stu-id="af3f8-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="af3f8-120">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="af3f8-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="af3f8-121">每當使用者活動變更，您就需要呼叫 `startActivity()` 。</span><span class="sxs-lookup"><span data-stu-id="af3f8-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="af3f8-122">第一次呼叫此函數會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="af3f8-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="af3f8-123">使用者結束目前的活動</span><span class="sxs-lookup"><span data-stu-id="af3f8-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="af3f8-124">使用者完成最後一個活動時，您至少需要呼叫 `endActivity()` 一次。</span><span class="sxs-lookup"><span data-stu-id="af3f8-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="af3f8-125">這會通知 Mobile Engagement Web SDK，說明使用者目前處於閒置狀態，且工作階段逾時到期之後就必須關閉使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="af3f8-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="af3f8-126">如果您在工作階段逾時到期之前呼叫 `startActivity()` ，工作階段只會繼續。</span><span class="sxs-lookup"><span data-stu-id="af3f8-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="af3f8-127">因為當導覽視窗關閉時沒有可靠呼叫，在 Web 環境內攔截使用者活動的結束通常很困難或無法達成。</span><span class="sxs-lookup"><span data-stu-id="af3f8-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="af3f8-128">這就是為什麼 Mobile Engagement 伺服器會在應用程式頁面關閉後，於 3 分鐘之內自動讓使用者工作階段到期。</span><span class="sxs-lookup"><span data-stu-id="af3f8-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="af3f8-129">報告事件</span><span class="sxs-lookup"><span data-stu-id="af3f8-129">Reporting events</span></span>
<span data-ttu-id="af3f8-130">報告事件涵蓋了工作階段事件和獨立事件。</span><span class="sxs-lookup"><span data-stu-id="af3f8-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="af3f8-131">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="af3f8-131">Session events</span></span>
<span data-ttu-id="af3f8-132">工作階段事件通常用來報告在使用者工作階段期間由使用者所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="af3f8-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="af3f8-133">**不含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="af3f8-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="af3f8-134">**含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="af3f8-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="af3f8-135">獨立事件</span><span class="sxs-lookup"><span data-stu-id="af3f8-135">Standalone events</span></span>
<span data-ttu-id="af3f8-136">與工作階段事件不同，獨立的事件可能發生在工作階段的內容之外。</span><span class="sxs-lookup"><span data-stu-id="af3f8-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="af3f8-137">針對那種情況，請使用 ``engagement.agent.sendEvent``，而不是 ``engagement.agent.sendSessionEvent``。</span><span class="sxs-lookup"><span data-stu-id="af3f8-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="af3f8-138">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="af3f8-138">Reporting errors</span></span>
<span data-ttu-id="af3f8-139">報告錯誤涵蓋了工作階段錯誤和獨立錯誤。</span><span class="sxs-lookup"><span data-stu-id="af3f8-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="af3f8-140">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="af3f8-140">Session errors</span></span>
<span data-ttu-id="af3f8-141">工作階段錯誤通常用來報告在使用者工作階段期間影響使用者的錯誤。</span><span class="sxs-lookup"><span data-stu-id="af3f8-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="af3f8-142">**不含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="af3f8-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="af3f8-143">**含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="af3f8-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="af3f8-144">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="af3f8-144">Standalone errors</span></span>
<span data-ttu-id="af3f8-145">不同於工作階段錯誤，獨立錯誤可以出現在工作階段的內容之外。</span><span class="sxs-lookup"><span data-stu-id="af3f8-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="af3f8-146">針對那種情況，請使用 `engagement.agent.sendError`，而不是 `engagement.agent.sendSessionError`。</span><span class="sxs-lookup"><span data-stu-id="af3f8-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="af3f8-147">報告工作</span><span class="sxs-lookup"><span data-stu-id="af3f8-147">Reporting jobs</span></span>
<span data-ttu-id="af3f8-148">報告作業涵蓋報告在作業期間發生的錯誤和事件，以及報告當機。</span><span class="sxs-lookup"><span data-stu-id="af3f8-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="af3f8-149">**範例：**</span><span class="sxs-lookup"><span data-stu-id="af3f8-149">**Example:**</span></span>

<span data-ttu-id="af3f8-150">如果您想要監視 AJAX 要求，可以使用下列項目：</span><span class="sxs-lookup"><span data-stu-id="af3f8-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="af3f8-151">報告於作業期間發生的錯誤</span><span class="sxs-lookup"><span data-stu-id="af3f8-151">Reporting errors during a job</span></span>
<span data-ttu-id="af3f8-152">錯誤可能與正在執行的作業關聯，而不是與目前的使用者作業階段關聯。</span><span class="sxs-lookup"><span data-stu-id="af3f8-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="af3f8-153">**範例：**</span><span class="sxs-lookup"><span data-stu-id="af3f8-153">**Example:**</span></span>

<span data-ttu-id="af3f8-154">如果您想要在 AJAX 要求失敗時報告錯誤：</span><span class="sxs-lookup"><span data-stu-id="af3f8-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="af3f8-155">在作業期間報告事件</span><span class="sxs-lookup"><span data-stu-id="af3f8-155">Reporting events during a job</span></span>
<span data-ttu-id="af3f8-156">透過 `engagement.agent.sendJobEvent` 函式，事件可以與執行中的作業相關，而不是與目前的使用者工作階段相關。</span><span class="sxs-lookup"><span data-stu-id="af3f8-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="af3f8-157">此函式的運作方式與 `engagement.agent.sendJobError`完全相同。</span><span class="sxs-lookup"><span data-stu-id="af3f8-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="af3f8-158">報告當機</span><span class="sxs-lookup"><span data-stu-id="af3f8-158">Reporting crashes</span></span>
<span data-ttu-id="af3f8-159">使用 `sendCrash` 函式來手動報告當機。</span><span class="sxs-lookup"><span data-stu-id="af3f8-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="af3f8-160">`crashid` 引數是識別當機類型的字串。</span><span class="sxs-lookup"><span data-stu-id="af3f8-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="af3f8-161">`crash` 引數通常是字串格式的當機的堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="af3f8-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="af3f8-162">額外的參數</span><span class="sxs-lookup"><span data-stu-id="af3f8-162">Extra parameters</span></span>
<span data-ttu-id="af3f8-163">您可以將任意資料附加到事件、錯誤、活動或作業。</span><span class="sxs-lookup"><span data-stu-id="af3f8-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="af3f8-164">此資料可以是任何 JSON 物件 (但是不是陣列或基本類型)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="af3f8-165">**範例：**</span><span class="sxs-lookup"><span data-stu-id="af3f8-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="af3f8-166">限制</span><span class="sxs-lookup"><span data-stu-id="af3f8-166">Limits</span></span>
<span data-ttu-id="af3f8-167">套用至額外參數的限制是在索引鍵、值類型和大小的規則運算式的領域。</span><span class="sxs-lookup"><span data-stu-id="af3f8-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="af3f8-168">之間的信任</span><span class="sxs-lookup"><span data-stu-id="af3f8-168">Keys</span></span>
<span data-ttu-id="af3f8-169">物件中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="af3f8-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="af3f8-170">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="af3f8-171">值</span><span class="sxs-lookup"><span data-stu-id="af3f8-171">Values</span></span>
<span data-ttu-id="af3f8-172">值被限制為字串、數字及布林類型。</span><span class="sxs-lookup"><span data-stu-id="af3f8-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="af3f8-173">大小</span><span class="sxs-lookup"><span data-stu-id="af3f8-173">Size</span></span>
<span data-ttu-id="af3f8-174">額外項目限制為一次呼叫 1024 個字元 (在 Mobile Engagement Web SDK 以 JSON 編碼之後)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="af3f8-175">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="af3f8-175">Reporting application information</span></span>
<span data-ttu-id="af3f8-176">您可以使用 `sendAppInfo()` 函式手動報告追蹤資訊 (或是任何其他應用程式特定資訊)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="af3f8-177">請注意，這項資訊可以累加方式傳送。</span><span class="sxs-lookup"><span data-stu-id="af3f8-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="af3f8-178">只會針對特定裝置保留特定索引鍵的最新值。</span><span class="sxs-lookup"><span data-stu-id="af3f8-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="af3f8-179">和事件額外資料一樣，您可以使用任何 JSON 物件來摘錄應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="af3f8-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="af3f8-180">請注意，陣列或子物件會視為一般字串 (使用 JSON 序列化)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="af3f8-181">**範例：**</span><span class="sxs-lookup"><span data-stu-id="af3f8-181">**Example:**</span></span>

<span data-ttu-id="af3f8-182">以下是傳送使用者性別和出生日期的程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="af3f8-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="af3f8-183">限制</span><span class="sxs-lookup"><span data-stu-id="af3f8-183">Limits</span></span>
<span data-ttu-id="af3f8-184">套用至應用程式資訊的限制是在索引鍵和大小的規則運算式的領域。</span><span class="sxs-lookup"><span data-stu-id="af3f8-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="af3f8-185">之間的信任</span><span class="sxs-lookup"><span data-stu-id="af3f8-185">Keys</span></span>
<span data-ttu-id="af3f8-186">物件中的每個索引鍵都必須符合下列規則運算式：</span><span class="sxs-lookup"><span data-stu-id="af3f8-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="af3f8-187">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="af3f8-188">大小</span><span class="sxs-lookup"><span data-stu-id="af3f8-188">Size</span></span>
<span data-ttu-id="af3f8-189">應用程式資訊限制為一次呼叫 1024 個字元 (在 Mobile Engagement Web SDK 以 JSON 編碼之後)。</span><span class="sxs-lookup"><span data-stu-id="af3f8-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="af3f8-190">在上述範例中，傳送到伺服器的 JSON 會是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="af3f8-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
