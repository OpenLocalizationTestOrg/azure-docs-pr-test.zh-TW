---
title: "Azure Mobile Engagement Windows 通用 app SDK 版本資訊 | Microsoft Docs"
description: "Azure Mobile Engagement - Windows 通用 app SDK 版本資訊"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: de938ce5-93d5-4218-9e33-10eef102bd61
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: dc5529a9e8f4eba867732f719ca8fff718c00d5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-release-notes"></a><span data-ttu-id="25d6d-103">Windows 通用 app SDK 版本資訊</span><span class="sxs-lookup"><span data-stu-id="25d6d-103">Windows Universal Apps SDK Release Notes</span></span>
## <a name="341-11032016"></a><span data-ttu-id="25d6d-104">3.4.1 (11/03/2016)</span><span class="sxs-lookup"><span data-stu-id="25d6d-104">3.4.1 (11/03/2016)</span></span>

* <span data-ttu-id="25d6d-105">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="25d6d-105">Stability improvements.</span></span>

## <a name="340-04192016"></a><span data-ttu-id="25d6d-106">3.4.0 (04/19/2016)</span><span class="sxs-lookup"><span data-stu-id="25d6d-106">3.4.0 (04/19/2016)</span></span>
* <span data-ttu-id="25d6d-107">Reach 重疊增強功能。</span><span class="sxs-lookup"><span data-stu-id="25d6d-107">Reach overlay improvements.</span></span>
* <span data-ttu-id="25d6d-108">已加入 "TestLogLevel" API 來啟用/停用/篩選 SDK 所發出的主控台記錄檔。</span><span class="sxs-lookup"><span data-stu-id="25d6d-108">Added "TestLogLevel" API to enable/disable/filter console logs emitted by the SDK.</span></span>
* <span data-ttu-id="25d6d-109">已修正活動中通知目標設定為應用程式啟動時未顯示的第一個活動。</span><span class="sxs-lookup"><span data-stu-id="25d6d-109">Fixed in-activity notifications targeting the first activity not displayed on App start.</span></span>

## <a name="331-02182016"></a><span data-ttu-id="25d6d-110">3.3.1 (02/18/2016)</span><span class="sxs-lookup"><span data-stu-id="25d6d-110">3.3.1 (02/18/2016)</span></span>
* <span data-ttu-id="25d6d-111">已修正 Web 通知的 HTML 內容與 SDK HTML 頁面之間的衝突。</span><span class="sxs-lookup"><span data-stu-id="25d6d-111">Fixed conflicts between web announcement's HTML content and SDK's HTML page.</span></span>
* <span data-ttu-id="25d6d-112">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="25d6d-112">Stability improvements.</span></span>

## <a name="330-01222016"></a><span data-ttu-id="25d6d-113">3.3.0 (01/22/2016)</span><span class="sxs-lookup"><span data-stu-id="25d6d-113">3.3.0 (01/22/2016)</span></span>
* <span data-ttu-id="25d6d-114">已修正在格式化以發行模式執行的 UWP 應用程式時當機的問題。</span><span class="sxs-lookup"><span data-stu-id="25d6d-114">Fixed crash formatting on UWP apps running in release mode.</span></span>
* <span data-ttu-id="25d6d-115">已修正 Universal 8.1 應用程式的通知中 1 像素邊界的問題。</span><span class="sxs-lookup"><span data-stu-id="25d6d-115">Fixed 1px margin on notifications for Universal 8.1 apps.</span></span>
* <span data-ttu-id="25d6d-116">動作 URL 現在可使用 ms-appx 及 ms-appdata 配置。</span><span class="sxs-lookup"><span data-stu-id="25d6d-116">ms-appx and ms-appdata schemes available on action urls.</span></span>
* <span data-ttu-id="25d6d-117">穩定性改進。</span><span class="sxs-lookup"><span data-stu-id="25d6d-117">Stability improvements.</span></span>

## <a name="320-11202015"></a><span data-ttu-id="25d6d-118">3.2.0 (11/20/2015)</span><span class="sxs-lookup"><span data-stu-id="25d6d-118">3.2.0 (11/20/2015)</span></span>
* <span data-ttu-id="25d6d-119">新增對 Windows 10 通用 Windows 平台應用程式的支援。</span><span class="sxs-lookup"><span data-stu-id="25d6d-119">Added support for Windows 10 Universal Windows Platform applications.</span></span>
* <span data-ttu-id="25d6d-120">新增推播通到共用功能，以修正通道衝突 (現已與 Azure 通知中樞相容)。</span><span class="sxs-lookup"><span data-stu-id="25d6d-120">Added push channel sharing feature to fix channel conflicts (now compatible with Azure Notification Hubs).</span></span>
* <span data-ttu-id="25d6d-121">修正初始化之後立即要求裝置 ID 時發生的當機。</span><span class="sxs-lookup"><span data-stu-id="25d6d-121">Fixed crash while requesting the device id just after the initialization.</span></span>
* <span data-ttu-id="25d6d-122">主控台記錄檔改善。</span><span class="sxs-lookup"><span data-stu-id="25d6d-122">Console logs improvements.</span></span>
* <span data-ttu-id="25d6d-123">修正解析未處理的例外狀況時發生的當機。</span><span class="sxs-lookup"><span data-stu-id="25d6d-123">Fixed crash while parsing some unhandled exceptions.</span></span>

## <a name="310-05212015"></a><span data-ttu-id="25d6d-124">3.1.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="25d6d-124">3.1.0 (05/21/2015)</span></span>
* <span data-ttu-id="25d6d-125">Mobile Engagement 裝置識別碼現在是根據在安裝時產生的 GUID。</span><span class="sxs-lookup"><span data-stu-id="25d6d-125">The Mobile Engagement device id is now based on a GUID generated at installation time.</span></span>

## <a name="301-04292015"></a><span data-ttu-id="25d6d-126">3.0.1 (2015/04//29)</span><span class="sxs-lookup"><span data-stu-id="25d6d-126">3.0.1 (04/29/2015)</span></span>
* <span data-ttu-id="25d6d-127">已修復影響 SDK 在部分 Windows Phone WinRT 應用程式上的初始化錯誤。</span><span class="sxs-lookup"><span data-stu-id="25d6d-127">Fixed a bug affecting the SDK initialization on some Windows Phone WinRT apps.</span></span>

## <a name="300-04032015"></a><span data-ttu-id="25d6d-128">3.0.0 (2015/04/03)</span><span class="sxs-lookup"><span data-stu-id="25d6d-128">3.0.0 (04/03/2015)</span></span>
* <span data-ttu-id="25d6d-129">導入了跨平台 app (Windows 和 Windows Phone WinRT) 的 Mobile Engagement SDK。</span><span class="sxs-lookup"><span data-stu-id="25d6d-129">Introducing the Mobile Engagement SDK for Universal App (Windows and Windows Phone WinRT).</span></span>
* <span data-ttu-id="25d6d-130">預設通知圖示已更新。</span><span class="sxs-lookup"><span data-stu-id="25d6d-130">Default notification icon updated.</span></span>
* <span data-ttu-id="25d6d-131">按一下通知時，會傳回系統通知動作回饋。</span><span class="sxs-lookup"><span data-stu-id="25d6d-131">Send back system notification action feedback when a notification is clicked.</span></span>
* <span data-ttu-id="25d6d-132">已修復系統通知有時在點選後於應用程式內重播的狀況。</span><span class="sxs-lookup"><span data-stu-id="25d6d-132">Fixed system notification which is sometimes replayed in-app after being clicked.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="25d6d-133">2.0.0 (2015/02/17)</span><span class="sxs-lookup"><span data-stu-id="25d6d-133">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="25d6d-134">Azure Mobile Engagement 的最初發行版本</span><span class="sxs-lookup"><span data-stu-id="25d6d-134">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="25d6d-135">以連接字串組態取代 appId/sdkKey 組態。</span><span class="sxs-lookup"><span data-stu-id="25d6d-135">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="25d6d-136">增強安全性。</span><span class="sxs-lookup"><span data-stu-id="25d6d-136">Security improvements.</span></span>

