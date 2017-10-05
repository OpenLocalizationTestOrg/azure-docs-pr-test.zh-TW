---
title: "Mobile Engagement 概念 | Microsoft Docs"
description: "Azure Mobile Engagement 概念"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 8450651528007b4527366b89a6ad7615169f93c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-concepts"></a><span data-ttu-id="c4ee2-103">Azure Mobile Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="c4ee2-103">Azure Mobile Engagement concepts</span></span>
<span data-ttu-id="c4ee2-104">Mobile Engagement 定義所有支援平台共同的一些概念。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-104">Mobile Engagement defines a few concepts common to all supported platforms.</span></span> <span data-ttu-id="c4ee2-105">本文會簡短說明這些概念。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-105">This article briefly describes those concepts.</span></span>

<span data-ttu-id="c4ee2-106">如果您不熟悉 Mobile Engagement，本文會是一個不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-106">This article is a good start if you are new to Mobile Engagement.</span></span> <span data-ttu-id="c4ee2-107">也請務必閱讀您所使用平台的專屬文件，因為它會精簡本文中所述概念的更多詳細資料和範例，以及可能的限制。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-107">Also make sure to read the documentation specific to the platform you are using, as it will refine the concepts described in this article with more details and examples as well as possible limitations.</span></span>

## <a name="devices-and-users"></a><span data-ttu-id="c4ee2-108">裝置和使用者</span><span class="sxs-lookup"><span data-stu-id="c4ee2-108">Devices and users</span></span>
<span data-ttu-id="c4ee2-109">Mobile Engagement 藉由為每台裝置產生唯一識別碼來識別使用者。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-109">Mobile Engagement identifies users by generating a unique identifier for each device.</span></span> <span data-ttu-id="c4ee2-110">這個識別碼稱為裝置識別碼 (或 `deviceid`)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-110">This identifier is called the device identifier (or `deviceid`).</span></span> <span data-ttu-id="c4ee2-111">它產生的方式會讓相同裝置的所有執行中應用程式共用相同的裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-111">It is generated in such a way that all applications running of the same device share the same device identifier.</span></span>

<span data-ttu-id="c4ee2-112">這隱含地表示，Mobile Engagement 會將一台裝置視為只屬於一位使用者，因此，使用者和裝置是對等概念。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-112">Implicitly, it means that Mobile Engagement considers one device to belong to exactly one user, and thus, users and devices are equivalent concepts.</span></span>

## <a name="sessions-and-activities"></a><span data-ttu-id="c4ee2-113">工作階段和活動</span><span class="sxs-lookup"><span data-stu-id="c4ee2-113">Sessions and activities</span></span>
<span data-ttu-id="c4ee2-114">工作階段是由使用者執行的一次應用程式使用，從使用者開始使用的時間，直到使用者停止的時間為止。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-114">A session is one use of the application performed by a user, from the time the user starts using it, until the user stops.</span></span>

<span data-ttu-id="c4ee2-115">活動是一位使用者所執行的應用程式特定子部分的一次使用 (通常是一個畫面，但可以是任何適合該應用程式的東西)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-115">An activity is one use of a given sub-part of the application performed by one user (it is usually a screen, but it can be anything suitable to the application).</span></span>

<span data-ttu-id="c4ee2-116">使用者一次只能執行一個活動。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-116">A user can only perform one activity at a time.</span></span>

<span data-ttu-id="c4ee2-117">活動是以名稱來識別 (限制為 64 個字元)，而且可以選擇性地嵌入一些額外的資料 (在 1024 個位元組的限制內)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-117">An activity is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

<span data-ttu-id="c4ee2-118">工作階段會自動從使用者執行的活動序列運算。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-118">Sessions are automatically computed from the sequence of activities performed by users.</span></span> <span data-ttu-id="c4ee2-119">工作階段會在使用者開始他的第一個活動時開始，在他完成他的最後一個活動時停止。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-119">A session starts when the user starts his first activity and stops when he finishes his last activity.</span></span> <span data-ttu-id="c4ee2-120">這表示工作階段不需要明確地開始或停止。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-120">This means that a session does not need to be explicitly started or stopped.</span></span> <span data-ttu-id="c4ee2-121">相反地，活動會明確地開始或停止。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-121">Instead, activities are explicitly started or stopped.</span></span> <span data-ttu-id="c4ee2-122">如果沒有報告任何活動，則不會報告任何工作階段。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-122">If no activity is reported, no session is reported.</span></span>

## <a name="events"></a><span data-ttu-id="c4ee2-123">事件</span><span class="sxs-lookup"><span data-stu-id="c4ee2-123">Events</span></span>
<span data-ttu-id="c4ee2-124">事件用來報告立即動作 (像是按下按鈕或是使用者閱讀了文章)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-124">Events are used to report instant actions (like button pressed or articles read by users).</span></span>

<span data-ttu-id="c4ee2-125">事件可以與目前工作階段或執行中的工作相關，也可以是獨立存在的事件。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-125">An event can be related to the current session, to a running job, or it can be a standalone event.</span></span>

<span data-ttu-id="c4ee2-126">事件是以名稱來識別 (限制為 64 個字元)，而且可以選擇性地嵌入一些額外的資料 (在 1024 個位元組的限制內)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-126">An event is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="error"></a><span data-ttu-id="c4ee2-127">錯誤</span><span class="sxs-lookup"><span data-stu-id="c4ee2-127">Error</span></span>
<span data-ttu-id="c4ee2-128">錯誤用來報告應用程式正確偵測到的問題 (例如不正確的使用者動作，或 API 呼叫失敗)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-128">Errors are used to report issues correctly detected by the application (like incorrect user actions, or API call failures).</span></span>

<span data-ttu-id="c4ee2-129">錯誤可以與目前工作階段或執行中的工作相關，也可以是獨立存在的錯誤。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-129">An error can be related to the current session, to a running job, or it can be a standalone error.</span></span>

<span data-ttu-id="c4ee2-130">錯誤是以名稱來識別 (限制為 64 個字元)，而且可以選擇性地嵌入一些額外的資料 (在 1024 個位元組的限制內)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-130">An error is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="job"></a><span data-ttu-id="c4ee2-131">工作 (Job)</span><span class="sxs-lookup"><span data-stu-id="c4ee2-131">Job</span></span>
<span data-ttu-id="c4ee2-132">工作用來報告具有持續時間的動作 (像是 API 呼叫持續時間、廣告的顯示時間、背景工作的持續時間，或使用者動作的持續時間)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-132">Jobs are used to report actions having a duration (like duration of API calls, display time of ads, duration of background tasks or duration of user actions).</span></span>

<span data-ttu-id="c4ee2-133">工作與工作階段無關，因為可以在背景執行工作，而沒有任何使用者互動。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-133">A job is not related to a session, because a task can be performed in the background, without any user interaction.</span></span>

<span data-ttu-id="c4ee2-134">工作是以名稱來識別 (限制為 64 個字元)，而且可以選擇性地嵌入一些額外的資料 (在 1024 個位元組的限制內)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-134">A job is identified by a name (limited to 64 characters) and can optionally embed some extra data (in the limit of 1024 bytes).</span></span>

## <a name="crash"></a><span data-ttu-id="c4ee2-135">當機</span><span class="sxs-lookup"><span data-stu-id="c4ee2-135">Crash</span></span>
<span data-ttu-id="c4ee2-136">當機是由 Mobile Engagement SDK 自動發出以報告應用程式失敗，其中是由應用程式未偵測到的問題使它當機的。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-136">Crashes are issued automatically by the Mobile Engagement SDK to report application failures where issues not detected by the application make it crash.</span></span>

## <a name="application-information"></a><span data-ttu-id="c4ee2-137">應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="c4ee2-137">Application information</span></span>
<span data-ttu-id="c4ee2-138">應用程式資訊 (或應用程式資訊 (app info)) 可用來標記使用者，也就是將一些資料與應用程式的使用者建立關聯 (這點類似於 Web Cookie，不過應用程式資訊會儲存在 Azure Mobile Engagement 平台上的伺服器端)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-138">Application information (or app info) is used to tag users, that is, to associate some data to the users of an application (this is similar to web cookies, except that app info is stored on the server side on the Azure Mobile Engagement platform).</span></span>

<span data-ttu-id="c4ee2-139">應用程式資訊可以使用 Mobile Engagement SDK API 或使用 Mobile Engagement 平台裝置 API 來登記。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-139">App info can be registered by using the Mobile Engagement SDK API or by using the Mobile Engagement platform Device API.</span></span>

<span data-ttu-id="c4ee2-140">應用程式資訊是與裝置相關聯的索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-140">App info is a key/value pair associated to a device.</span></span> <span data-ttu-id="c4ee2-141">索引鍵是應用程式資訊的名稱 (限制為 64 個 ASCII 字元 [zA-A-Z]、數字 [0-9] 和底線 [__])。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-141">The key is the name of the app info (limited to 64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]).</span></span> <span data-ttu-id="c4ee2-142">值 (限制為 1024 個字元) 可以是任何字串、整數、日期 (-yyyy-mm-dd) 或布林值 (true 或 false)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-142">The value (limited to 1024 characters) can be any string, integer, date (yyyy-MM-dd) or Boolean (true or false).</span></span>

<span data-ttu-id="c4ee2-143">任何數目的應用程式資訊可以與裝置相關聯，只要在 Mobile Engagement 定價條件所定義的限制內即可。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-143">Any number of app info can be associated to a device, within the limits defined by the Mobile Engagement pricing terms.</span></span> <span data-ttu-id="c4ee2-144">針對一個指定的索引鍵，Mobile Engagement 只會追蹤最新設定的值 (沒有記錄)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-144">For one given key, Mobile Engagement only keeps track of the latest value set (no history).</span></span> <span data-ttu-id="c4ee2-145">設定或變更應用程式資訊的值會強制 Mobile Engagement 重新評估此應用程式資訊上設定的對象準則 (如果有的話)，這表示應用程式資訊可以用來觸發即時推送。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-145">Setting or changing the value of an app info forces Mobile Engagement to re-evaluate audience criteria set on this app info (if any) meaning that app info can be used to trigger realtime pushes.</span></span>

## <a name="extra-data"></a><span data-ttu-id="c4ee2-146">額外的資料</span><span class="sxs-lookup"><span data-stu-id="c4ee2-146">Extra data</span></span>
<span data-ttu-id="c4ee2-147">額外的資料 (或額外項目) 是一些可以附加到事件、錯誤、活動和工作的任意資料。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-147">Extra data (or extras) is some arbitrary data that can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="c4ee2-148">額外項目的結構與 JSON 物件類似：包含索引鍵/值組的樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-148">Extras are structured similarly to JSON objects: they are made of a tree of key/value pairs.</span></span> <span data-ttu-id="c4ee2-149">索引鍵限制為 64 個 ASCII 字母 [a A-ZA-Z]、數字 [0-9] 和底線 [__])，而額外項目的總大小則限制為 1024 個字元 (由 Mobile Engagement SDK 以 JSON 編碼之後)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-149">Keys are limited to 64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]) and the total size of extras is limited to 1024 characters (once encoded in JSON by the Mobile Engagement SDK).</span></span>

<span data-ttu-id="c4ee2-150">索引鍵/值組的整個樹狀結構會儲存為 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-150">The whole tree of key/value pairs is stored as a JSON object.</span></span> <span data-ttu-id="c4ee2-151">不過，只有索引鍵/值的第一個層級會分解以便可供一些進階的函式直接存取，例如 Segments (例如，您可以輕鬆地定義稱為 "SciFi fans" 的區段，它是由上個月傳送至少 10 次事件名為 "content_viewed" 事件的所有使用者所構成，且額外的索引鍵 "content_type" 設定為 "scifi" 值)。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-151">Nevertheless, only the first level of keys/values is decomposed to be directly accessible to some advanced functions like Segments (for example, you can easily define a segment called “SciFi fans” that is made of all users having sent at least 10 times the event named “content_viewed” with the extra key “content_type” set to the value “scifi” in the last month).</span></span> <span data-ttu-id="c4ee2-152">因此強烈建議只傳送使用純量值 (例如字串、日期、整數或布林值) 的索引鍵/值組簡單清單所組成的額外項目。</span><span class="sxs-lookup"><span data-stu-id="c4ee2-152">It is thus highly recommended to send only extras made of simple lists of key/value pairs using scalar values (for example, strings, dates, integers or Boolean).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4ee2-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4ee2-153">Next steps</span></span>
* [<span data-ttu-id="c4ee2-154">適用於 Azure Mobile Engagement 的 Windows 通用 SDK 概觀</span><span class="sxs-lookup"><span data-stu-id="c4ee2-154">Windows Universal SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-store-sdk-overview.md)
* [<span data-ttu-id="c4ee2-155">適用於 Azure Mobile Engagement 的 Windows Phone Silverlight SDK 概觀</span><span class="sxs-lookup"><span data-stu-id="c4ee2-155">Windows Phone Silverlight SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
* [<span data-ttu-id="c4ee2-156">Azure Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="c4ee2-156">iOS SDK for Azure Mobile Engagement</span></span>](mobile-engagement-ios-sdk-overview.md)
* [<span data-ttu-id="c4ee2-157">適用於 Azure Mobile Engagement 的 Android SDK</span><span class="sxs-lookup"><span data-stu-id="c4ee2-157">Android SDK for Azure Mobile Engagement</span></span>](mobile-engagement-android-sdk-overview.md)

