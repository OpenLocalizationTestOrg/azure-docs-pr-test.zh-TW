---
title: "Azure Mobile Engagement Android SDK 整合"
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
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="657b8-103">版本資訊</span><span class="sxs-lookup"><span data-stu-id="657b8-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="657b8-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="657b8-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="657b8-105">修正在呼叫 `EngagementAgentUtils.isInDedicatedEngagementProcess` (也由 `EngagementApplication` 類別使用) 時可能罕見發生的損毀。</span><span class="sxs-lookup"><span data-stu-id="657b8-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="657b8-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="657b8-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="657b8-107">Android 8 支援 (舊版 SDK 不適用於 Android 8)。</span><span class="sxs-lookup"><span data-stu-id="657b8-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="657b8-108">不再依賴支援程式庫。</span><span class="sxs-lookup"><span data-stu-id="657b8-108">No more dependency on support library.</span></span>
* <span data-ttu-id="657b8-109">移除 `EngagementFragmentActivity` 類別。</span><span class="sxs-lookup"><span data-stu-id="657b8-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="657b8-110">由於 Android 8 上的[背景執行限制](https://developer.android.com/preview/features/background.html)，在背景中的記錄檔可能會延遲，直到使用者與裝置互動之時，這會影響推送活動**已傳遞**和**系統通知顯示**統計資料延遲，如果裝置已進入休眠狀態的話 (通知仍會顯示、且仍會即時響鈴和震動)。</span><span class="sxs-lookup"><span data-stu-id="657b8-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="657b8-111">由於[背景位置限制](https://developer.android.com/preview/features/background-location-limits.html)，背景的即時位置將不會在 Android 8 上經常更新。</span><span class="sxs-lookup"><span data-stu-id="657b8-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="657b8-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="657b8-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="657b8-113">修正 Android 7 上的應用程式內通知文字色彩，使其與舊版 Android 上的色彩相同。</span><span class="sxs-lookup"><span data-stu-id="657b8-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="657b8-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="657b8-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="657b8-115">不會再鎖定 WIFI。</span><span class="sxs-lookup"><span data-stu-id="657b8-115">No more WIFI lock.</span></span>
* <span data-ttu-id="657b8-116">修正在 init 之前呼叫 getDeviceId 時的死結問題 (4.2.0 中引進的錯誤)。</span><span class="sxs-lookup"><span data-stu-id="657b8-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="657b8-117">4.2.2 (2016/05/17)</span><span class="sxs-lookup"><span data-stu-id="657b8-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="657b8-118">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="657b8-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="657b8-119">4.2.1 (2016/05/10)</span><span class="sxs-lookup"><span data-stu-id="657b8-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="657b8-120">安全性︰停用 Web 檢視本機檔案存取權限。</span><span class="sxs-lookup"><span data-stu-id="657b8-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="657b8-121">安全性︰移除 `EngagementPreferenceActivity` 類別，其可擴充過時且不安全的 `PreferenceActivity` 類別。</span><span class="sxs-lookup"><span data-stu-id="657b8-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="657b8-122">安全性︰現在會記載觸達活動以使用 `exported="false"`，此旗標也可用於先前的 SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="657b8-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="657b8-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="657b8-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="657b8-124">SDK 現在是在 MIT 中授權的。</span><span class="sxs-lookup"><span data-stu-id="657b8-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="657b8-125">允許在 SDK 初始化階段指定自訂裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="657b8-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="657b8-126">4.1.5 (02/01/2016)</span><span class="sxs-lookup"><span data-stu-id="657b8-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="657b8-127">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="657b8-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="657b8-128">4.1.4 (01/26/2016)</span><span class="sxs-lookup"><span data-stu-id="657b8-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="657b8-129">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="657b8-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="657b8-130">4.1.3 (12/9/2015)</span><span class="sxs-lookup"><span data-stu-id="657b8-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="657b8-131">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="657b8-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="657b8-132">4.1.2 (11/25/2015)</span><span class="sxs-lookup"><span data-stu-id="657b8-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="657b8-133">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="657b8-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="657b8-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="657b8-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="657b8-135">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="657b8-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="657b8-136">4.1.0 (2015/08/25)</span><span class="sxs-lookup"><span data-stu-id="657b8-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="657b8-137">處理 Android M 的新權限模型。</span><span class="sxs-lookup"><span data-stu-id="657b8-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="657b8-138">除了使用 `AndroidManifest.xml` 之外，現在可以在執行階段設定定位功能。</span><span class="sxs-lookup"><span data-stu-id="657b8-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="657b8-139">修正權限錯誤：如果您使用 `ACCESS_FINE_LOCATION`，就不再需要 `ACCESS_COARSE_LOCATION`。</span><span class="sxs-lookup"><span data-stu-id="657b8-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="657b8-140">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="657b8-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="657b8-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="657b8-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="657b8-142">內部通訊協定會變更以讓分析和推播更可靠。</span><span class="sxs-lookup"><span data-stu-id="657b8-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="657b8-143">原生推送 (GCM/ADM) 現在也用於應用程式通知，因此您必須為任何類型的推送行銷活動設定原生推送認證。</span><span class="sxs-lookup"><span data-stu-id="657b8-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="657b8-144">修正大圖片通知：它們只會在推播之後顯示 10 秒。</span><span class="sxs-lookup"><span data-stu-id="657b8-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="657b8-145">修正網頁檢視中的錯誤：按一下連結也會執行預設動作 URL。</span><span class="sxs-lookup"><span data-stu-id="657b8-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="657b8-146">修正與本機儲存體管理相關的罕見損毀。</span><span class="sxs-lookup"><span data-stu-id="657b8-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="657b8-147">修正動態組態字串管理。</span><span class="sxs-lookup"><span data-stu-id="657b8-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="657b8-148">更新 EULA。</span><span class="sxs-lookup"><span data-stu-id="657b8-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="657b8-149">3.0.0 (2015/02/17)</span><span class="sxs-lookup"><span data-stu-id="657b8-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="657b8-150">Azure Mobile Engagement 的最初發行版本</span><span class="sxs-lookup"><span data-stu-id="657b8-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="657b8-151">appId 組態取代為連接字串組態。</span><span class="sxs-lookup"><span data-stu-id="657b8-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="657b8-152">已移除從傳送與接收任意 XMPP 實體之任意 XMPP 訊息的 API。</span><span class="sxs-lookup"><span data-stu-id="657b8-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="657b8-153">已移除在裝置之間傳送與接收訊息的 API。</span><span class="sxs-lookup"><span data-stu-id="657b8-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="657b8-154">增強安全性。</span><span class="sxs-lookup"><span data-stu-id="657b8-154">Security improvements.</span></span>
* <span data-ttu-id="657b8-155">已移除 Google Play 和 SmartAd 追蹤。</span><span class="sxs-lookup"><span data-stu-id="657b8-155">Google Play and SmartAd tracking removed.</span></span>

