---
title: "aaaAzure Mobile Engagement Android SDK 整合"
description: "Android SDK for Azure Mobile Engagement 的最新更新和程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a><span data-ttu-id="27d58-103">版本資訊</span><span class="sxs-lookup"><span data-stu-id="27d58-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="27d58-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="27d58-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="27d58-105">修正損毀時，可能很少發生呼叫`EngagementAgentUtils.isInDedicatedEngagementProcess`，也可由 hello`EngagementApplication`類別。</span><span class="sxs-lookup"><span data-stu-id="27d58-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="27d58-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="27d58-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="27d58-107">Android 8 支援 （舊版本的 SDK 不適用於 Android 8 hello）。</span><span class="sxs-lookup"><span data-stu-id="27d58-107">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="27d58-108">不再依賴支援程式庫。</span><span class="sxs-lookup"><span data-stu-id="27d58-108">No more dependency on support library.</span></span>
* <span data-ttu-id="27d58-109">移除 `EngagementFragmentActivity` 類別。</span><span class="sxs-lookup"><span data-stu-id="27d58-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="27d58-110">因為太[背景執行限制](https://developer.android.com/preview/features/background.html)Android 8，在背景中的記錄檔可能會延遲，直到 hello 使用者與 hello 裝置互動，這會影響的推送活動**Delivered**和**系統通知顯示**而延遲，如果 hello 裝置已進入休眠狀態的統計資料 （hello 通知仍會顯示，將信號和震動而不發生問題的即時）。</span><span class="sxs-lookup"><span data-stu-id="27d58-110">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="27d58-111">因為太[背景的位置限制](https://developer.android.com/preview/features/background-location-limits.html)，hello 即時位置，在背景中的將不會更新經常在 Android 8。</span><span class="sxs-lookup"><span data-stu-id="27d58-111">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="27d58-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="27d58-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="27d58-113">修正應用程式內通知 Android 7 toobe 上的文字色彩 hello 相同較舊的 Android 版本。</span><span class="sxs-lookup"><span data-stu-id="27d58-113">Fix in-app notification text colors on Android 7 toobe hello same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="27d58-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="27d58-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="27d58-115">不會再鎖定 WIFI。</span><span class="sxs-lookup"><span data-stu-id="27d58-115">No more WIFI lock.</span></span>
* <span data-ttu-id="27d58-116">修正在 init 之前呼叫 getDeviceId 時的死結問題 (4.2.0 中引進的錯誤)。</span><span class="sxs-lookup"><span data-stu-id="27d58-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="27d58-117">4.2.2 (2016/05/17)</span><span class="sxs-lookup"><span data-stu-id="27d58-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="27d58-118">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="27d58-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="27d58-119">4.2.1 (2016/05/10)</span><span class="sxs-lookup"><span data-stu-id="27d58-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="27d58-120">安全性︰停用 Web 檢視本機檔案存取權限。</span><span class="sxs-lookup"><span data-stu-id="27d58-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="27d58-121">安全性︰移除 `EngagementPreferenceActivity` 類別，其可擴充過時且不安全的 `PreferenceActivity` 類別。</span><span class="sxs-lookup"><span data-stu-id="27d58-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="27d58-122">安全性： 觸達活動現在已記載 toouse `exported="false"`，此旗標也可用在先前的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="27d58-122">Security: reach activities are now documented toouse `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="27d58-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="27d58-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="27d58-124">hello SDK 現在是 MIT 授權。</span><span class="sxs-lookup"><span data-stu-id="27d58-124">hello SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="27d58-125">允許在 SDK 初始化階段指定自訂裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="27d58-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="27d58-126">4.1.5 (02/01/2016)</span><span class="sxs-lookup"><span data-stu-id="27d58-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="27d58-127">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="27d58-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="27d58-128">4.1.4 (01/26/2016)</span><span class="sxs-lookup"><span data-stu-id="27d58-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="27d58-129">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="27d58-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="27d58-130">4.1.3 (12/9/2015)</span><span class="sxs-lookup"><span data-stu-id="27d58-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="27d58-131">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="27d58-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="27d58-132">4.1.2 (11/25/2015)</span><span class="sxs-lookup"><span data-stu-id="27d58-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="27d58-133">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="27d58-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="27d58-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="27d58-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="27d58-135">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="27d58-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="27d58-136">4.1.0 (2015/08/25)</span><span class="sxs-lookup"><span data-stu-id="27d58-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="27d58-137">處理 Android M 的新權限模型。</span><span class="sxs-lookup"><span data-stu-id="27d58-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="27d58-138">除了使用 `AndroidManifest.xml` 之外，現在可以在執行階段設定定位功能。</span><span class="sxs-lookup"><span data-stu-id="27d58-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="27d58-139">修正權限錯誤：如果您使用 `ACCESS_FINE_LOCATION`，就不再需要 `ACCESS_COARSE_LOCATION`。</span><span class="sxs-lookup"><span data-stu-id="27d58-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="27d58-140">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="27d58-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="27d58-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="27d58-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="27d58-142">內部通訊協定變更 toomake 分析及推播更可靠。</span><span class="sxs-lookup"><span data-stu-id="27d58-142">Internal protocol changes toomake analytics and push more reliable.</span></span>
* <span data-ttu-id="27d58-143">原生推送 (GCM/ADM) 現在也用於應用程式內通知，您必須設定為任何類型的推播宣傳活動 hello 原生推送認證。</span><span class="sxs-lookup"><span data-stu-id="27d58-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure hello native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="27d58-144">修正大圖片通知：它們只會在推播之後顯示 10 秒。</span><span class="sxs-lookup"><span data-stu-id="27d58-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="27d58-145">在 web 檢視中修正的 bug： 的連結也執行 hello 預設動作 URL。</span><span class="sxs-lookup"><span data-stu-id="27d58-145">Fix a bug in web view: clicking on a link was also executing hello default action URL.</span></span>
* <span data-ttu-id="27d58-146">修正極少數的損毀相關 toolocal 存放裝置管理。</span><span class="sxs-lookup"><span data-stu-id="27d58-146">Fix a rare crash related toolocal storage management.</span></span>
* <span data-ttu-id="27d58-147">修正動態組態字串管理。</span><span class="sxs-lookup"><span data-stu-id="27d58-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="27d58-148">更新 EULA。</span><span class="sxs-lookup"><span data-stu-id="27d58-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="27d58-149">3.0.0 (2015/02/17)</span><span class="sxs-lookup"><span data-stu-id="27d58-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="27d58-150">Azure Mobile Engagement 的最初發行版本</span><span class="sxs-lookup"><span data-stu-id="27d58-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="27d58-151">appId 組態取代為連接字串組態。</span><span class="sxs-lookup"><span data-stu-id="27d58-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="27d58-152">移除應用程式開發介面 toosend 和任意 XMPP 訊息接收任意 XMPP 實體。</span><span class="sxs-lookup"><span data-stu-id="27d58-152">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="27d58-153">移除應用程式開發介面 toosend 和接收裝置之間的訊息。</span><span class="sxs-lookup"><span data-stu-id="27d58-153">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="27d58-154">增強安全性。</span><span class="sxs-lookup"><span data-stu-id="27d58-154">Security improvements.</span></span>
* <span data-ttu-id="27d58-155">已移除 Google Play 和 SmartAd 追蹤。</span><span class="sxs-lookup"><span data-stu-id="27d58-155">Google Play and SmartAd tracking removed.</span></span>

