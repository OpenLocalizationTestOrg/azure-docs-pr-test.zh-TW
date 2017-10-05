---
title: "Azure Mobile Engagement 的 Android SDK 整合"
description: "描述如何整合 Azure Mobile Engagement SDK 至 Android 應用程式"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 35935e911f1f17989beb71978396c6d1b7d601d6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="4fd04-103">Azure Mobile Engagement 的 Android SDK 整合</span><span class="sxs-lookup"><span data-stu-id="4fd04-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fd04-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="4fd04-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="4fd04-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="4fd04-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="4fd04-106">iOS</span><span class="sxs-lookup"><span data-stu-id="4fd04-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="4fd04-107">Android</span><span class="sxs-lookup"><span data-stu-id="4fd04-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="4fd04-108">此文件說明適用於 Azure Mobile Engagement Android SDK 的所有整合及組態選項。</span><span class="sxs-lookup"><span data-stu-id="4fd04-108">This document describes all the integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fd04-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="4fd04-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="4fd04-110">進階功能</span><span class="sxs-lookup"><span data-stu-id="4fd04-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="4fd04-111">報告功能</span><span class="sxs-lookup"><span data-stu-id="4fd04-111">Reporting Features</span></span>
<span data-ttu-id="4fd04-112">您可以新增這些功能：</span><span class="sxs-lookup"><span data-stu-id="4fd04-112">You can add these features:</span></span>

1. [<span data-ttu-id="4fd04-113">進階報告選項</span><span class="sxs-lookup"><span data-stu-id="4fd04-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="4fd04-114">位置報告選項</span><span class="sxs-lookup"><span data-stu-id="4fd04-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="4fd04-115">進階組態選項</span><span class="sxs-lookup"><span data-stu-id="4fd04-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="4fd04-116">通知:</span><span class="sxs-lookup"><span data-stu-id="4fd04-116">Notifications:</span></span>
[<span data-ttu-id="4fd04-117">如何將 Reach (通知) 整合在 Android 應用程式中</span><span class="sxs-lookup"><span data-stu-id="4fd04-117">How to integrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="4fd04-118">Google 雲端通訊 (GCM)： [如何整合 GCM 與 Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="4fd04-118">Google Cloud Messaging (GCM): [How to Integrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="4fd04-119">Amazon 裝置傳訊 (ADM)： [如何整合 ADM 與 Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="4fd04-119">Amazon Device Messaging (ADM): [How to Integrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="4fd04-120">標記計畫實作：</span><span class="sxs-lookup"><span data-stu-id="4fd04-120">Tag plan implementation:</span></span>
[<span data-ttu-id="4fd04-121">如何在 Android 應用程式中使用進階 Mobile Engagement 標記 API</span><span class="sxs-lookup"><span data-stu-id="4fd04-121">How to use the advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="4fd04-122">版本資訊</span><span class="sxs-lookup"><span data-stu-id="4fd04-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="4fd04-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="4fd04-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="4fd04-124">修正在呼叫 `EngagementAgentUtils.isInDedicatedEngagementProcess` (也由 `EngagementApplication` 類別使用) 時可能罕見發生的損毀。</span><span class="sxs-lookup"><span data-stu-id="4fd04-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="4fd04-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="4fd04-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="4fd04-126">Android 8 支援 (舊版 SDK 不適用於 Android 8)。</span><span class="sxs-lookup"><span data-stu-id="4fd04-126">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="4fd04-127">不再依賴支援程式庫。</span><span class="sxs-lookup"><span data-stu-id="4fd04-127">No more dependency on support library.</span></span>
* <span data-ttu-id="4fd04-128">移除 `EngagementFragmentActivity` 類別。</span><span class="sxs-lookup"><span data-stu-id="4fd04-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="4fd04-129">由於 Android 8 上的[背景執行限制](https://developer.android.com/preview/features/background.html)，在背景中的記錄檔可能會延遲，直到使用者與裝置互動之時，這會影響推送活動**已傳遞**和**系統通知顯示**統計資料延遲，如果裝置已進入休眠狀態的話 (通知仍會顯示、且仍會即時響鈴和震動)。</span><span class="sxs-lookup"><span data-stu-id="4fd04-129">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="4fd04-130">由於[背景位置限制](https://developer.android.com/preview/features/background-location-limits.html)，背景的即時位置將不會在 Android 8 上經常更新。</span><span class="sxs-lookup"><span data-stu-id="4fd04-130">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="4fd04-131">如需所有版本，請參閱 [完整版本資訊](mobile-engagement-android-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="4fd04-131">For all versions, see the [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="4fd04-132">升級程序</span><span class="sxs-lookup"><span data-stu-id="4fd04-132">Upgrade procedures</span></span>
<span data-ttu-id="4fd04-133">如果您已經將較舊版的 SDK 整合到應用程式中，請參閱 [升級程序](mobile-engagement-android-upgrade-procedure.md)。</span><span class="sxs-lookup"><span data-stu-id="4fd04-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

