---
title: "aaaAzure Mobile Engagement iOS SDK 版本資訊 |Microsoft 文件"
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
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="06768-103">Azure Mobile Engagement iOS SDK 版本資訊</span><span class="sxs-lookup"><span data-stu-id="06768-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="06768-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="06768-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="06768-105">修正在背景清除徽章。</span><span class="sxs-lookup"><span data-stu-id="06768-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="06768-106">修正在 XCode 9 上關於 API 未在主要佇列呼叫的警告。</span><span class="sxs-lookup"><span data-stu-id="06768-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="06768-107">修正觸達輪詢中的記憶體流失。</span><span class="sxs-lookup"><span data-stu-id="06768-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="06768-108">停止支援 iOS 6.X。</span><span class="sxs-lookup"><span data-stu-id="06768-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="06768-109">從您的應用程式的這個版本 hello 部署目標開始必須至少是 iOS 7。</span><span class="sxs-lookup"><span data-stu-id="06768-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="06768-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="06768-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="06768-111">改善在背景中的記錄傳送。</span><span class="sxs-lookup"><span data-stu-id="06768-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="06768-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="06768-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="06768-113">iOS 10 裝置上有固定的通知不會採取動作。</span><span class="sxs-lookup"><span data-stu-id="06768-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="06768-114">取代 XCode 7。</span><span class="sxs-lookup"><span data-stu-id="06768-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="06768-115">3.2.4 (06/30/2016)</span><span class="sxs-lookup"><span data-stu-id="06768-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="06768-116">修正技術記錄和其他記錄之間的彙總。</span><span class="sxs-lookup"><span data-stu-id="06768-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="06768-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="06768-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="06768-118">其中傳送意見反應閘道並未回報 hello 背景應用程式時的固定的 hello bug。</span><span class="sxs-lookup"><span data-stu-id="06768-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="06768-119">最佳化的技術的記錄檔傳送 hello。</span><span class="sxs-lookup"><span data-stu-id="06768-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="06768-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="06768-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="06768-121">在 HTTP 要求取消，而有時導致 toocrash 修正的 bug。</span><span class="sxs-lookup"><span data-stu-id="06768-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="06768-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="06768-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="06768-123">深層連結的通知所觸發的新應用程式執行個體時，固定的 hello 延遲</span><span class="sxs-lookup"><span data-stu-id="06768-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="06768-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="06768-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="06768-125">它可以搭配 hello SDK toomake 中啟用 Bitcode **Xcode 7**。</span><span class="sxs-lookup"><span data-stu-id="06768-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="06768-126">已修正的 bug 相關 tooin 應用程式通知。</span><span class="sxs-lookup"><span data-stu-id="06768-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="06768-127">進行 hello 應用程式內通知發生電力偏低與其他這類案例更可靠。</span><span class="sxs-lookup"><span data-stu-id="06768-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="06768-128">移除第三方程式庫所產生的額外主控台記錄檔。</span><span class="sxs-lookup"><span data-stu-id="06768-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="06768-129">3.1.0 (2015/08/26)</span><span class="sxs-lookup"><span data-stu-id="06768-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="06768-130">搭配協力廠商程式庫修正 iOS 9 相容性錯誤。</span><span class="sxs-lookup"><span data-stu-id="06768-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="06768-131">當傳送投票結果、應用程式資訊或是額外的資料時會造成當機。</span><span class="sxs-lookup"><span data-stu-id="06768-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="06768-132">3.0.0 (2015/06/19)</span><span class="sxs-lookup"><span data-stu-id="06768-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="06768-133">Mobile Engagement 使用無聲推播通知。</span><span class="sxs-lookup"><span data-stu-id="06768-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="06768-134">停止支援 iOS 4.X。</span><span class="sxs-lookup"><span data-stu-id="06768-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="06768-135">從您的應用程式的這個版本 hello 部署目標開始必須至少是 iOS 6。</span><span class="sxs-lookup"><span data-stu-id="06768-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="06768-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="06768-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="06768-137">裝置 hello Mobile Engagement 裝置識別碼 < iOS 6 現在會根據在安裝期間所產生的 GUID。</span><span class="sxs-lookup"><span data-stu-id="06768-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="06768-138">2.1.0 (2015/04/24)</span><span class="sxs-lookup"><span data-stu-id="06768-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="06768-139">新增 Swift 相容性。</span><span class="sxs-lookup"><span data-stu-id="06768-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="06768-140">按一下通知，當 hello 現在是 URL 之後，執行的動作右邊 hello 應用程式開啟。</span><span class="sxs-lookup"><span data-stu-id="06768-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="06768-141">在 SDK 封裝中加入缺少的標頭檔案。</span><span class="sxs-lookup"><span data-stu-id="06768-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="06768-142">停用 hello Mobile Engagement 當機報告時，請修正的問題。</span><span class="sxs-lookup"><span data-stu-id="06768-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="06768-143">2.0.0 (2015/02/17)</span><span class="sxs-lookup"><span data-stu-id="06768-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="06768-144">Azure Mobile Engagement 的最初發行版本</span><span class="sxs-lookup"><span data-stu-id="06768-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="06768-145">以連接字串組態取代 appId/sdkKey 組態。</span><span class="sxs-lookup"><span data-stu-id="06768-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="06768-146">移除應用程式開發介面 toosend 和任意 XMPP 訊息接收任意 XMPP 實體。</span><span class="sxs-lookup"><span data-stu-id="06768-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="06768-147">移除應用程式開發介面 toosend 和接收裝置之間的訊息。</span><span class="sxs-lookup"><span data-stu-id="06768-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="06768-148">增強安全性。</span><span class="sxs-lookup"><span data-stu-id="06768-148">Security improvements.</span></span>
* <span data-ttu-id="06768-149">已移除 SmartAd 追蹤。</span><span class="sxs-lookup"><span data-stu-id="06768-149">SmartAd tracking removed.</span></span>
