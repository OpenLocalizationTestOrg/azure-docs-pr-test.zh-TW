---
title: "aaaMobile Engagement 概念 |Microsoft 文件"
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
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a><span data-ttu-id="a1c70-103">Azure Mobile Engagement 概念</span><span class="sxs-lookup"><span data-stu-id="a1c70-103">Azure Mobile Engagement concepts</span></span>
<span data-ttu-id="a1c70-104">Mobile Engagement 會定義幾個概念常見 tooall 支援平台。</span><span class="sxs-lookup"><span data-stu-id="a1c70-104">Mobile Engagement defines a few concepts common tooall supported platforms.</span></span> <span data-ttu-id="a1c70-105">本文會簡短說明這些概念。</span><span class="sxs-lookup"><span data-stu-id="a1c70-105">This article briefly describes those concepts.</span></span>

<span data-ttu-id="a1c70-106">如果您是新 tooMobile Engagement 這篇文章會是不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="a1c70-106">This article is a good start if you are new tooMobile Engagement.</span></span> <span data-ttu-id="a1c70-107">也請確定 tooread hello 文件特定 toohello 平台使用，因為它會精簡 hello 概念更多詳細資料和範例，以及可能限制此文件中所述。</span><span class="sxs-lookup"><span data-stu-id="a1c70-107">Also make sure tooread hello documentation specific toohello platform you are using, as it will refine hello concepts described in this article with more details and examples as well as possible limitations.</span></span>

## <a name="devices-and-users"></a><span data-ttu-id="a1c70-108">裝置和使用者</span><span class="sxs-lookup"><span data-stu-id="a1c70-108">Devices and users</span></span>
<span data-ttu-id="a1c70-109">Mobile Engagement 藉由為每台裝置產生唯一識別碼來識別使用者。</span><span class="sxs-lookup"><span data-stu-id="a1c70-109">Mobile Engagement identifies users by generating a unique identifier for each device.</span></span> <span data-ttu-id="a1c70-110">這個識別項稱為 hello 裝置識別碼 (或`deviceid`)。</span><span class="sxs-lookup"><span data-stu-id="a1c70-110">This identifier is called hello device identifier (or `deviceid`).</span></span> <span data-ttu-id="a1c70-111">產生的所有應用程式執行 hello 相同的方式共用裝置 hello 相同裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="a1c70-111">It is generated in such a way that all applications running of hello same device share hello same device identifier.</span></span>

<span data-ttu-id="a1c70-112">隱含的這表示，Mobile Engagement 會考慮一個裝置 toobelong tooexactly 一個使用者，因此，使用者與裝置都相當的概念。</span><span class="sxs-lookup"><span data-stu-id="a1c70-112">Implicitly, it means that Mobile Engagement considers one device toobelong tooexactly one user, and thus, users and devices are equivalent concepts.</span></span>

## <a name="sessions-and-activities"></a><span data-ttu-id="a1c70-113">工作階段和活動</span><span class="sxs-lookup"><span data-stu-id="a1c70-113">Sessions and activities</span></span>
<span data-ttu-id="a1c70-114">工作階段是使用 hello hello 時間 hello 使用者的使用者，所執行的應用程式一開始使用它，直到 hello 使用者停止。</span><span class="sxs-lookup"><span data-stu-id="a1c70-114">A session is one use of hello application performed by a user, from hello time hello user starts using it, until hello user stops.</span></span>

<span data-ttu-id="a1c70-115">活動是給定的子 hello 一位使用者所執行的應用程式一部分的一個用法 （通常是畫面上，但它可以是任何項目適合 toohello 應用程式）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-115">An activity is one use of a given sub-part of hello application performed by one user (it is usually a screen, but it can be anything suitable toohello application).</span></span>

<span data-ttu-id="a1c70-116">使用者一次只能執行一個活動。</span><span class="sxs-lookup"><span data-stu-id="a1c70-116">A user can only perform one activity at a time.</span></span>

<span data-ttu-id="a1c70-117">活動由 （有限的 too64 字元） 的名稱，並可以選擇性地嵌入某些額外的資料 （hello 限制為 1024 個位元組）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-117">An activity is identified by a name (limited too64 characters) and can optionally embed some extra data (in hello limit of 1024 bytes).</span></span>

<span data-ttu-id="a1c70-118">自動計算工作階段的使用者所執行的活動 hello 序列中的資料。</span><span class="sxs-lookup"><span data-stu-id="a1c70-118">Sessions are automatically computed from hello sequence of activities performed by users.</span></span> <span data-ttu-id="a1c70-119">工作階段開始時 hello 使用者開始其第一個活動，他完成他的最後一個活動時，就會停止。</span><span class="sxs-lookup"><span data-stu-id="a1c70-119">A session starts when hello user starts his first activity and stops when he finishes his last activity.</span></span> <span data-ttu-id="a1c70-120">這表示工作階段不需要 toobe 明確啟動或停止。</span><span class="sxs-lookup"><span data-stu-id="a1c70-120">This means that a session does not need toobe explicitly started or stopped.</span></span> <span data-ttu-id="a1c70-121">相反地，活動會明確地開始或停止。</span><span class="sxs-lookup"><span data-stu-id="a1c70-121">Instead, activities are explicitly started or stopped.</span></span> <span data-ttu-id="a1c70-122">如果沒有報告任何活動，則不會報告任何工作階段。</span><span class="sxs-lookup"><span data-stu-id="a1c70-122">If no activity is reported, no session is reported.</span></span>

## <a name="events"></a><span data-ttu-id="a1c70-123">事件</span><span class="sxs-lookup"><span data-stu-id="a1c70-123">Events</span></span>
<span data-ttu-id="a1c70-124">事件是使用的 tooreport 立即動作 （例如按鈕按下或由使用者所讀取的文件）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-124">Events are used tooreport instant actions (like button pressed or articles read by users).</span></span>

<span data-ttu-id="a1c70-125">事件可能是相關的 toohello 目前工作階段，tooa 執行作業，或獨立事件。</span><span class="sxs-lookup"><span data-stu-id="a1c70-125">An event can be related toohello current session, tooa running job, or it can be a standalone event.</span></span>

<span data-ttu-id="a1c70-126">事件由 （有限的 too64 字元） 的名稱，並可以選擇性地嵌入某些額外的資料 （hello 限制為 1024 個位元組）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-126">An event is identified by a name (limited too64 characters) and can optionally embed some extra data (in hello limit of 1024 bytes).</span></span>

## <a name="error"></a><span data-ttu-id="a1c70-127">錯誤</span><span class="sxs-lookup"><span data-stu-id="a1c70-127">Error</span></span>
<span data-ttu-id="a1c70-128">錯誤是使用的 tooreport 問題正確地偵測到的 hello 應用程式 （例如不正確的使用者動作或應用程式開發介面呼叫失敗）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-128">Errors are used tooreport issues correctly detected by hello application (like incorrect user actions, or API call failures).</span></span>

<span data-ttu-id="a1c70-129">錯誤可能是相關的 toohello 目前工作階段，tooa 執行作業，或它可以是一個獨立的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a1c70-129">An error can be related toohello current session, tooa running job, or it can be a standalone error.</span></span>

<span data-ttu-id="a1c70-130">錯誤由 （有限的 too64 字元） 的名稱，並可以選擇性地嵌入某些額外的資料 （hello 限制為 1024 個位元組）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-130">An error is identified by a name (limited too64 characters) and can optionally embed some extra data (in hello limit of 1024 bytes).</span></span>

## <a name="job"></a><span data-ttu-id="a1c70-131">作業</span><span class="sxs-lookup"><span data-stu-id="a1c70-131">Job</span></span>
<span data-ttu-id="a1c70-132">作業會使用的 tooreport 動作具有持續時間 （持續時間的 API 呼叫，例如顯示的廣告時間、 持續時間的背景工作或使用者動作的持續時間）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-132">Jobs are used tooreport actions having a duration (like duration of API calls, display time of ads, duration of background tasks or duration of user actions).</span></span>

<span data-ttu-id="a1c70-133">作業不是相關的 tooa 工作階段，因為沒有任何使用者互動的 hello 背景來執行工作。</span><span class="sxs-lookup"><span data-stu-id="a1c70-133">A job is not related tooa session, because a task can be performed in hello background, without any user interaction.</span></span>

<span data-ttu-id="a1c70-134">作業由 （有限的 too64 字元） 的名稱，且可以選擇性地嵌入某些額外的資料 （hello 限制為 1024 個位元組）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-134">A job is identified by a name (limited too64 characters) and can optionally embed some extra data (in hello limit of 1024 bytes).</span></span>

## <a name="crash"></a><span data-ttu-id="a1c70-135">當機</span><span class="sxs-lookup"><span data-stu-id="a1c70-135">Crash</span></span>
<span data-ttu-id="a1c70-136">由 hello Mobile Engagement SDK tooreport 應用程式損毀的失敗而無法偵測的 hello 應用程式的問題進行它自動發出損毀。</span><span class="sxs-lookup"><span data-stu-id="a1c70-136">Crashes are issued automatically by hello Mobile Engagement SDK tooreport application failures where issues not detected by hello application make it crash.</span></span>

## <a name="application-information"></a><span data-ttu-id="a1c70-137">應用程式資訊</span><span class="sxs-lookup"><span data-stu-id="a1c70-137">Application information</span></span>
<span data-ttu-id="a1c70-138">應用程式資訊 （或應用程式資訊） 是使用的 tootag 使用者，也就是 tooassociate （不同之處在於應用程式資訊會儲存在 hello hello Azure Mobile Engagement 平台上的伺服器端上，這是類似的 tooweb cookie） 應用程式的某些資料 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="a1c70-138">Application information (or app info) is used tootag users, that is, tooassociate some data toohello users of an application (this is similar tooweb cookies, except that app info is stored on hello server side on hello Azure Mobile Engagement platform).</span></span>

<span data-ttu-id="a1c70-139">使用 hello Mobile Engagement SDK 的 API，或使用 hello Mobile Engagement 平台裝置 API，您可以註冊應用程式資訊。</span><span class="sxs-lookup"><span data-stu-id="a1c70-139">App info can be registered by using hello Mobile Engagement SDK API or by using hello Mobile Engagement platform Device API.</span></span>

<span data-ttu-id="a1c70-140">應用程式資訊是索引鍵/值組相關聯的 tooa 裝置。</span><span class="sxs-lookup"><span data-stu-id="a1c70-140">App info is a key/value pair associated tooa device.</span></span> <span data-ttu-id="a1c70-141">hello 索引鍵是 hello 名稱 hello 應用程式資訊 （有限的 too64 ASCII 字母 [的 A-ZA-Z]，[0-9] 數字和底線 [__]）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-141">hello key is hello name of hello app info (limited too64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]).</span></span> <span data-ttu-id="a1c70-142">hello 值 （有限的 too1024 字元） 可以是任何字串、 整數、 日期 (yyyy-MM-dd) 或布林值 （true 或 false）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-142">hello value (limited too1024 characters) can be any string, integer, date (yyyy-MM-dd) or Boolean (true or false).</span></span>

<span data-ttu-id="a1c70-143">任何數目的應用程式資訊可以是相關聯的 tooa 裝置，hello hello Mobile Engagement 定價條件所定義的限制範圍內。</span><span class="sxs-lookup"><span data-stu-id="a1c70-143">Any number of app info can be associated tooa device, within hello limits defined by hello Mobile Engagement pricing terms.</span></span> <span data-ttu-id="a1c70-144">一個指定的索引鍵，Mobile Engagement 只會追蹤的最新值集 hello （沒有記錄）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-144">For one given key, Mobile Engagement only keeps track of hello latest value set (no history).</span></span> <span data-ttu-id="a1c70-145">設定或變更的應用程式資訊的 hello 值強制 Mobile Engagement toore-評估此應用程式上設定的受眾準則資訊 （如果有的話） 表示該應用程式資訊為使用的 tootrigger 即時推播通知。</span><span class="sxs-lookup"><span data-stu-id="a1c70-145">Setting or changing hello value of an app info forces Mobile Engagement toore-evaluate audience criteria set on this app info (if any) meaning that app info can be used tootrigger realtime pushes.</span></span>

## <a name="extra-data"></a><span data-ttu-id="a1c70-146">額外的資料</span><span class="sxs-lookup"><span data-stu-id="a1c70-146">Extra data</span></span>
<span data-ttu-id="a1c70-147">額外的資料 （或額外項目） 會任意資料可以附加的 tooevents、 錯誤、 活動與工作。</span><span class="sxs-lookup"><span data-stu-id="a1c70-147">Extra data (or extras) is some arbitrary data that can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="a1c70-148">結構化的額外項目同樣 tooJSON 物件： 這些語言的索引鍵/值組的樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="a1c70-148">Extras are structured similarly tooJSON objects: they are made of a tree of key/value pairs.</span></span> <span data-ttu-id="a1c70-149">索引鍵是有限的 too64 ASCII 字母 [的 A-ZA-Z]、 [0-9] 數字和底線 [__]） 和 hello 的額外項目大小總計為有限的 too1024 （一次編碼字元在 JSON 中的 hello Mobile Engagement SDK）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-149">Keys are limited too64 ASCII letters [a-zA-Z], numbers [0-9] and underscores [_]) and hello total size of extras is limited too1024 characters (once encoded in JSON by hello Mobile Engagement SDK).</span></span>

<span data-ttu-id="a1c70-150">hello 的索引鍵/值組的整個樹狀結構會儲存為 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="a1c70-150">hello whole tree of key/value pairs is stored as a JSON object.</span></span> <span data-ttu-id="a1c70-151">不過，只有 hello 第一個層級索引鍵/值，會分解的 toobe 直接存取 toosome 進階函式，例如區段 （例如，您可以輕鬆地定義區段稱為 「 SciFi 風扇 」 所做的所有使用者有傳送至少 10 次 hello 事件名為"content_viewed"hello 額外金鑰 「 有效 」 組 toohello 值"scifi"hello 在上個月）。</span><span class="sxs-lookup"><span data-stu-id="a1c70-151">Nevertheless, only hello first level of keys/values is decomposed toobe directly accessible toosome advanced functions like Segments (for example, you can easily define a segment called “SciFi fans” that is made of all users having sent at least 10 times hello event named “content_viewed” with hello extra key “content_type” set toohello value “scifi” in hello last month).</span></span> <span data-ttu-id="a1c70-152">因此強烈建議使用純量值 （例如，字串、 日期、 整數或布林值） 的索引鍵/值組的簡單清單所組成 toosend 唯一額外項目。</span><span class="sxs-lookup"><span data-stu-id="a1c70-152">It is thus highly recommended toosend only extras made of simple lists of key/value pairs using scalar values (for example, strings, dates, integers or Boolean).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1c70-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1c70-153">Next steps</span></span>
* [<span data-ttu-id="a1c70-154">適用於 Azure Mobile Engagement 的 Windows 通用 SDK 概觀</span><span class="sxs-lookup"><span data-stu-id="a1c70-154">Windows Universal SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-store-sdk-overview.md)
* [<span data-ttu-id="a1c70-155">適用於 Azure Mobile Engagement 的 Windows Phone Silverlight SDK 概觀</span><span class="sxs-lookup"><span data-stu-id="a1c70-155">Windows Phone Silverlight SDK overview for Azure Mobile Engagement</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
* [<span data-ttu-id="a1c70-156">Azure Mobile Engagement iOS SDK</span><span class="sxs-lookup"><span data-stu-id="a1c70-156">iOS SDK for Azure Mobile Engagement</span></span>](mobile-engagement-ios-sdk-overview.md)
* [<span data-ttu-id="a1c70-157">適用於 Azure Mobile Engagement 的 Android SDK</span><span class="sxs-lookup"><span data-stu-id="a1c70-157">Android SDK for Azure Mobile Engagement</span></span>](mobile-engagement-android-sdk-overview.md)

