---
title: "Azure Mobile Engagement iOS SDK 版本資訊 | Microsoft Docs"
description: "Azure Mobile Engagement iOS SDK 的最新更新與程序"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 9bdaa57f9902373ccf796ff109332b64c66bf9e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="7d7af-103">Azure Mobile Engagement iOS SDK 版本資訊</span><span class="sxs-lookup"><span data-stu-id="7d7af-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="7d7af-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="7d7af-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="7d7af-105">修正在背景清除徽章。</span><span class="sxs-lookup"><span data-stu-id="7d7af-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="7d7af-106">修正在 XCode 9 上關於 API 未在主要佇列呼叫的警告。</span><span class="sxs-lookup"><span data-stu-id="7d7af-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="7d7af-107">修正觸達輪詢中的記憶體流失。</span><span class="sxs-lookup"><span data-stu-id="7d7af-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="7d7af-108">停止支援 iOS 6.X。</span><span class="sxs-lookup"><span data-stu-id="7d7af-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="7d7af-109">從此版本開始，您的應用程式部署目標必須至少為 iOS 7。</span><span class="sxs-lookup"><span data-stu-id="7d7af-109">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="7d7af-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="7d7af-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="7d7af-111">改善在背景中的記錄傳送。</span><span class="sxs-lookup"><span data-stu-id="7d7af-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="7d7af-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="7d7af-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="7d7af-113">iOS 10 裝置上有固定的通知不會採取動作。</span><span class="sxs-lookup"><span data-stu-id="7d7af-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="7d7af-114">取代 XCode 7。</span><span class="sxs-lookup"><span data-stu-id="7d7af-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="7d7af-115">3.2.4 (06/30/2016)</span><span class="sxs-lookup"><span data-stu-id="7d7af-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="7d7af-116">修正技術記錄和其他記錄之間的彙總。</span><span class="sxs-lookup"><span data-stu-id="7d7af-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="7d7af-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="7d7af-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="7d7af-118">修正當應用程式在背景時不回報傳遞回饋的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d7af-118">Fixed the bug where delivery feedback is not reported when app is in the background.</span></span>
* <span data-ttu-id="7d7af-119">將技術記錄的傳送最佳化。</span><span class="sxs-lookup"><span data-stu-id="7d7af-119">Optimized the sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="7d7af-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="7d7af-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="7d7af-121">修正 HTTP 要求取消有時會導致損毀的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d7af-121">Fixed bug on HTTP request cancellation which sometimes leads to crash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="7d7af-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="7d7af-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="7d7af-123">修正當新應用程式執行個體由具有深度連結的通知觸發時造成的延遲。</span><span class="sxs-lookup"><span data-stu-id="7d7af-123">Fixed the delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="7d7af-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="7d7af-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="7d7af-125">啟用 SDK 中的 Bitcode 以便使用 **Xcode 7**。</span><span class="sxs-lookup"><span data-stu-id="7d7af-125">Enabled Bitcode in the SDK to make it work with **Xcode 7**.</span></span>
* <span data-ttu-id="7d7af-126">已修正與應用程式內通知相關的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d7af-126">Fixed bugs related to in-app notifications.</span></span>
* <span data-ttu-id="7d7af-127">讓應用程式內通知在發生電池電力不足與其他這類案例時更可靠。</span><span class="sxs-lookup"><span data-stu-id="7d7af-127">Made the in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="7d7af-128">移除第三方程式庫所產生的額外主控台記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7d7af-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="7d7af-129">3.1.0 (2015/08/26)</span><span class="sxs-lookup"><span data-stu-id="7d7af-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="7d7af-130">搭配協力廠商程式庫修正 iOS 9 相容性錯誤。</span><span class="sxs-lookup"><span data-stu-id="7d7af-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="7d7af-131">當傳送投票結果、應用程式資訊或是額外的資料時會造成當機。</span><span class="sxs-lookup"><span data-stu-id="7d7af-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="7d7af-132">3.0.0 (2015/06/19)</span><span class="sxs-lookup"><span data-stu-id="7d7af-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="7d7af-133">Mobile Engagement 使用無聲推播通知。</span><span class="sxs-lookup"><span data-stu-id="7d7af-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="7d7af-134">停止支援 iOS 4.X。</span><span class="sxs-lookup"><span data-stu-id="7d7af-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="7d7af-135">從此版本開始，您的應用程式部署目標必須至少為 iOS 6。</span><span class="sxs-lookup"><span data-stu-id="7d7af-135">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="7d7af-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="7d7af-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="7d7af-137">針對 < iOS 6 之裝置的 Mobile Engagement 裝置識別碼現在是根據在安裝時產生的 GUID。</span><span class="sxs-lookup"><span data-stu-id="7d7af-137">The Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="7d7af-138">2.1.0 (2015/04/24)</span><span class="sxs-lookup"><span data-stu-id="7d7af-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="7d7af-139">新增 Swift 相容性。</span><span class="sxs-lookup"><span data-stu-id="7d7af-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="7d7af-140">現在按一下通知時，動作 URL 會在應用程式開啟後立即執行。</span><span class="sxs-lookup"><span data-stu-id="7d7af-140">When clicking on a notification, the action URL is now executed right after the application is opened.</span></span>
* <span data-ttu-id="7d7af-141">在 SDK 封裝中加入缺少的標頭檔案。</span><span class="sxs-lookup"><span data-stu-id="7d7af-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="7d7af-142">已修正 Mobile Engagement 當機報告程式停用時的問題。</span><span class="sxs-lookup"><span data-stu-id="7d7af-142">Fixed an issue when the Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="7d7af-143">2.0.0 (2015/02/17)</span><span class="sxs-lookup"><span data-stu-id="7d7af-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="7d7af-144">Azure Mobile Engagement 的最初發行版本</span><span class="sxs-lookup"><span data-stu-id="7d7af-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="7d7af-145">以連接字串組態取代 appId/sdkKey 組態。</span><span class="sxs-lookup"><span data-stu-id="7d7af-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="7d7af-146">已移除從任意 XMPP 實體傳送與接收任意 XMPP 訊息的 API。</span><span class="sxs-lookup"><span data-stu-id="7d7af-146">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="7d7af-147">已移除在裝置之間傳送與接收訊息的 API。</span><span class="sxs-lookup"><span data-stu-id="7d7af-147">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="7d7af-148">增強安全性。</span><span class="sxs-lookup"><span data-stu-id="7d7af-148">Security improvements.</span></span>
* <span data-ttu-id="7d7af-149">已移除 SmartAd 追蹤。</span><span class="sxs-lookup"><span data-stu-id="7d7af-149">SmartAd tracking removed.</span></span>
