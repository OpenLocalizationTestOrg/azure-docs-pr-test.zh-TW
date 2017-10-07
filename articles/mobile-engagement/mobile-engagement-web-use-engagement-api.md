---
title: "Mobile Engagement Web SDK Api aaaAzure |Microsoft 文件"
description: "Azure Mobile Engagement hello 最新更新和 hello Web SDK 的程序"
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
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="56231-103">使用 web 應用程式中的 hello Azure Mobile Engagement 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="56231-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="56231-104">這份文件是加法 toohello 文件，告訴您如何太[web 應用程式中整合 Mobile Engagement](mobile-engagement-web-integrate-engagement.md)。</span><span class="sxs-lookup"><span data-stu-id="56231-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="56231-105">它提供有關如何 toouse hello tooreport Azure Mobile Engagement 應用程式開發介面的詳細資料您的應用程式統計資料。</span><span class="sxs-lookup"><span data-stu-id="56231-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="56231-106">hello Mobile Engagement 應用程式開發介面由提供 hello`engagement.agent`物件。</span><span class="sxs-lookup"><span data-stu-id="56231-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="56231-107">hello Azure Mobile Engagement Web SDK 別名是的預設`engagement`。</span><span class="sxs-lookup"><span data-stu-id="56231-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="56231-108">您可以重新定義從 hello SDK 設定此別名。</span><span class="sxs-lookup"><span data-stu-id="56231-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="56231-109">Mobile Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="56231-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="56231-110">hello 下列部分精簡常見[Mobile Engagement 概念](mobile-engagement-concepts.md)hello web 平台。</span><span class="sxs-lookup"><span data-stu-id="56231-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="56231-111">`Session`和`Activity`</span><span class="sxs-lookup"><span data-stu-id="56231-111">`Session` and `Activity`</span></span>
<span data-ttu-id="56231-112">如果兩個活動之間的多個數秒鐘，hello 使用者停留閒置，hello 使用者的活動順序分成兩個不同的工作階段。</span><span class="sxs-lookup"><span data-stu-id="56231-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="56231-113">這些幾秒鐘的時間稱為 hello 工作階段逾時。</span><span class="sxs-lookup"><span data-stu-id="56231-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="56231-114">如果 web 應用程式不會宣告 hello 結束使用者活動本身 (透過呼叫 hello`engagement.agent.endActivity`函式)，hello Mobile Engagement 伺服器自動到期 hello hello 應用程式頁面上關閉後的 3 分鐘內的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="56231-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="56231-115">這稱為 hello 伺服器工作階段逾時。</span><span class="sxs-lookup"><span data-stu-id="56231-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="56231-116">根據預設，不會建立無法攔截的 JavaScript 例外狀況的自動報告。</span><span class="sxs-lookup"><span data-stu-id="56231-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="56231-117">不過，您也可以回報當機的 hello`sendCrash`函式 （請參閱報告損毀的 hello > 一節）。</span><span class="sxs-lookup"><span data-stu-id="56231-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="56231-118">報告活動</span><span class="sxs-lookup"><span data-stu-id="56231-118">Reporting activities</span></span>
<span data-ttu-id="56231-119">使用者活動上的報告包括當使用者啟動新的活動與 hello 使用者結束 hello 目前活動時。</span><span class="sxs-lookup"><span data-stu-id="56231-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="56231-120">使用者啟動新的活動</span><span class="sxs-lookup"><span data-stu-id="56231-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="56231-121">您需要 toocall`startActivity()`變更每個階段的使用者活動。</span><span class="sxs-lookup"><span data-stu-id="56231-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="56231-122">hello 第一個呼叫 toothis 函式會啟動新的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="56231-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="56231-123">使用者結束 hello 目前活動</span><span class="sxs-lookup"><span data-stu-id="56231-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="56231-124">您需要 toocall`endActivity()`至少一次當 hello 使用者完成其最後一個活動。</span><span class="sxs-lookup"><span data-stu-id="56231-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="56231-125">這會通知 hello Mobile Engagement Web SDK hello 使用者目前閒置，並 hello 使用者工作階段需要 toobe hello 工作階段逾時過期之後關閉。</span><span class="sxs-lookup"><span data-stu-id="56231-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="56231-126">如果您呼叫`startActivity()`hello 工作階段逾時到期前，只要繼續進行 hello 工作階段。</span><span class="sxs-lookup"><span data-stu-id="56231-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="56231-127">因為沒有可靠的 hello 導覽器] 視窗已關閉時呼叫，通常很難或是無法 toocatch hello 結尾 web 環境內的使用者活動。</span><span class="sxs-lookup"><span data-stu-id="56231-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="56231-128">原因是 hello 伺服器自動到期的 Mobile Engagement hello hello 應用程式頁面上關閉後的 3 分鐘內的使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="56231-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="56231-129">報告事件</span><span class="sxs-lookup"><span data-stu-id="56231-129">Reporting events</span></span>
<span data-ttu-id="56231-130">報告事件涵蓋了工作階段事件和獨立事件。</span><span class="sxs-lookup"><span data-stu-id="56231-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="56231-131">工作階段事件</span><span class="sxs-lookup"><span data-stu-id="56231-131">Session events</span></span>
<span data-ttu-id="56231-132">工作階段事件通常是使用者執行的 hello 使用者工作階段期間使用的 tooreport hello 動作。</span><span class="sxs-lookup"><span data-stu-id="56231-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="56231-133">**不含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="56231-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="56231-134">**含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="56231-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="56231-135">獨立事件</span><span class="sxs-lookup"><span data-stu-id="56231-135">Standalone events</span></span>
<span data-ttu-id="56231-136">不同於工作階段事件獨立發生的事件工作階段的 hello 內容之外。</span><span class="sxs-lookup"><span data-stu-id="56231-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="56231-137">針對那種情況，請使用 ``engagement.agent.sendEvent``，而不是 ``engagement.agent.sendSessionEvent``。</span><span class="sxs-lookup"><span data-stu-id="56231-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="56231-138">報告錯誤</span><span class="sxs-lookup"><span data-stu-id="56231-138">Reporting errors</span></span>
<span data-ttu-id="56231-139">報告錯誤涵蓋了工作階段錯誤和獨立錯誤。</span><span class="sxs-lookup"><span data-stu-id="56231-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="56231-140">工作階段錯誤</span><span class="sxs-lookup"><span data-stu-id="56231-140">Session errors</span></span>
<span data-ttu-id="56231-141">工作階段錯誤通常是影響的 hello 使用者 hello 使用者工作階段期間的使用的 tooreport hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="56231-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="56231-142">**不含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="56231-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="56231-143">**含額外資料的範例：**</span><span class="sxs-lookup"><span data-stu-id="56231-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="56231-144">獨立錯誤</span><span class="sxs-lookup"><span data-stu-id="56231-144">Standalone errors</span></span>
<span data-ttu-id="56231-145">不同於工作階段錯誤，可能會發生工作階段的 hello 內容以外的獨立錯誤。</span><span class="sxs-lookup"><span data-stu-id="56231-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="56231-146">針對那種情況，請使用 `engagement.agent.sendError`，而不是 `engagement.agent.sendSessionError`。</span><span class="sxs-lookup"><span data-stu-id="56231-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="56231-147">報告工作</span><span class="sxs-lookup"><span data-stu-id="56231-147">Reporting jobs</span></span>
<span data-ttu-id="56231-148">報告作業涵蓋報告在作業期間發生的錯誤和事件，以及報告當機。</span><span class="sxs-lookup"><span data-stu-id="56231-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="56231-149">**範例：**</span><span class="sxs-lookup"><span data-stu-id="56231-149">**Example:**</span></span>

<span data-ttu-id="56231-150">如果您想 toomonitor AJAX 要求時，您可以使用下列 hello:</span><span class="sxs-lookup"><span data-stu-id="56231-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="56231-151">報告於作業期間發生的錯誤</span><span class="sxs-lookup"><span data-stu-id="56231-151">Reporting errors during a job</span></span>
<span data-ttu-id="56231-152">錯誤可能是相關的 tooa 執行而不是 toohello 目前使用者工作階段的作業。</span><span class="sxs-lookup"><span data-stu-id="56231-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="56231-153">**範例：**</span><span class="sxs-lookup"><span data-stu-id="56231-153">**Example:**</span></span>

<span data-ttu-id="56231-154">如果您想要 tooreport 錯誤如果 AJAX 要求，失敗：</span><span class="sxs-lookup"><span data-stu-id="56231-154">If you want tooreport an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="56231-155">在作業期間報告事件</span><span class="sxs-lookup"><span data-stu-id="56231-155">Reporting events during a job</span></span>
<span data-ttu-id="56231-156">事件可能會執行作業，而不是目前使用者工作階段 toohello，這 toohello 相關的 tooa`engagement.agent.sendJobEvent`函式。</span><span class="sxs-lookup"><span data-stu-id="56231-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="56231-157">此函式的運作方式與 `engagement.agent.sendJobError`完全相同。</span><span class="sxs-lookup"><span data-stu-id="56231-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="56231-158">報告當機</span><span class="sxs-lookup"><span data-stu-id="56231-158">Reporting crashes</span></span>
<span data-ttu-id="56231-159">使用 hello`sendCrash`函式 tooreport 手動損毀。</span><span class="sxs-lookup"><span data-stu-id="56231-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="56231-160">hello`crashid`引數是可識別 hello 損毀類型的字串。</span><span class="sxs-lookup"><span data-stu-id="56231-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="56231-161">hello`crash`引數通常是做為字串 hello 損毀 hello 堆疊追蹤。</span><span class="sxs-lookup"><span data-stu-id="56231-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="56231-162">額外的參數</span><span class="sxs-lookup"><span data-stu-id="56231-162">Extra parameters</span></span>
<span data-ttu-id="56231-163">您可以附加任意資料 tooan 事件、 錯誤、 活動或工作。</span><span class="sxs-lookup"><span data-stu-id="56231-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="56231-164">hello 資料可以是任何的 JSON 物件 （但不是陣列或基本類型）。</span><span class="sxs-lookup"><span data-stu-id="56231-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="56231-165">**範例：**</span><span class="sxs-lookup"><span data-stu-id="56231-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="56231-166">限制</span><span class="sxs-lookup"><span data-stu-id="56231-166">Limits</span></span>
<span data-ttu-id="56231-167">套用 tooextra 參數的限制是在規則運算式的索引鍵、 值類型和大小的 hello 部分。</span><span class="sxs-lookup"><span data-stu-id="56231-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="56231-168">之間的信任</span><span class="sxs-lookup"><span data-stu-id="56231-168">Keys</span></span>
<span data-ttu-id="56231-169">Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="56231-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="56231-170">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="56231-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="56231-171">值</span><span class="sxs-lookup"><span data-stu-id="56231-171">Values</span></span>
<span data-ttu-id="56231-172">值為有限的 toostring、 數字和 Boolean 類型。</span><span class="sxs-lookup"><span data-stu-id="56231-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="56231-173">大小</span><span class="sxs-lookup"><span data-stu-id="56231-173">Size</span></span>
<span data-ttu-id="56231-174">額外項目是限制的 too1，024 每個呼叫 （在 hello Mobile Engagement Web SDK 會將其編碼 JSON 中） 之後的字元。</span><span class="sxs-lookup"><span data-stu-id="56231-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="56231-175">報告應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="56231-175">Reporting application information</span></span>
<span data-ttu-id="56231-176">您可以手動追蹤資訊 （或任何其他應用程式特定資訊） 使用報告 hello`sendAppInfo()`函式。</span><span class="sxs-lookup"><span data-stu-id="56231-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="56231-177">請注意，這項資訊可以累加方式傳送。</span><span class="sxs-lookup"><span data-stu-id="56231-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="56231-178">只有 hello 最新值的特定索引鍵會保留特定裝置。</span><span class="sxs-lookup"><span data-stu-id="56231-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="56231-179">類似事件的額外功能，您可以使用任何 JSON 物件 tooabstract 應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="56231-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="56231-180">請注意，陣列或子物件會視為一般字串 (使用 JSON 序列化)。</span><span class="sxs-lookup"><span data-stu-id="56231-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="56231-181">**範例：**</span><span class="sxs-lookup"><span data-stu-id="56231-181">**Example:**</span></span>

<span data-ttu-id="56231-182">以下是針對傳送嗨使用者的性別和生日的程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="56231-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="56231-183">限制</span><span class="sxs-lookup"><span data-stu-id="56231-183">Limits</span></span>
<span data-ttu-id="56231-184">Tooapplication 資訊適用於的限制是 hello 區域的金鑰和大小的規則運算式中。</span><span class="sxs-lookup"><span data-stu-id="56231-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="56231-185">之間的信任</span><span class="sxs-lookup"><span data-stu-id="56231-185">Keys</span></span>
<span data-ttu-id="56231-186">Hello 物件中的每個索引鍵必須符合下列規則運算式的 hello:</span><span class="sxs-lookup"><span data-stu-id="56231-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="56231-187">這表示索引鍵必須至少以一個字母開頭，後面連接字母、數字或底線 (\_)。</span><span class="sxs-lookup"><span data-stu-id="56231-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="56231-188">大小</span><span class="sxs-lookup"><span data-stu-id="56231-188">Size</span></span>
<span data-ttu-id="56231-189">應用程式的資訊是有限的 too1，024 每個呼叫 （在 hello Mobile Engagement Web SDK 會將其編碼 JSON 中） 之後的字元。</span><span class="sxs-lookup"><span data-stu-id="56231-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="56231-190">在上述範例中的 hello，hello JSON 傳送 toohello 伺服器是 44 個字元：</span><span class="sxs-lookup"><span data-stu-id="56231-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
