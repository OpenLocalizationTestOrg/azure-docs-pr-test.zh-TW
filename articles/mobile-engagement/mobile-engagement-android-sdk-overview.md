---
title: "aaaAndroid Azure Mobile Engagement SDK 整合"
description: "描述如何在 Android 應用程式中的 Azure Mobile Engagement SDK toointegrate"
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
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a><span data-ttu-id="1f461-103">Azure Mobile Engagement 的 Android SDK 整合</span><span class="sxs-lookup"><span data-stu-id="1f461-103">Android SDK Integration for Azure Mobile Engagement</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f461-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="1f461-104">Universal Windows</span></span>](mobile-engagement-windows-store-sdk-overview.md)
> * [<span data-ttu-id="1f461-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1f461-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-sdk-overview.md)
> * [<span data-ttu-id="1f461-106">iOS</span><span class="sxs-lookup"><span data-stu-id="1f461-106">iOS</span></span>](mobile-engagement-ios-sdk-overview.md)
> * [<span data-ttu-id="1f461-107">Android</span><span class="sxs-lookup"><span data-stu-id="1f461-107">Android</span></span>](mobile-engagement-android-sdk-overview.md)
> 
> 

<span data-ttu-id="1f461-108">本文件說明所有 hello 整合和組態選項可用的 Azure Mobile Engagement Android SDK。</span><span class="sxs-lookup"><span data-stu-id="1f461-108">This document describes all hello integration and configuration options available for Azure Mobile Engagement Android SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f461-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="1f461-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a><span data-ttu-id="1f461-110">進階功能</span><span class="sxs-lookup"><span data-stu-id="1f461-110">Advanced Features</span></span>
### <a name="reporting-features"></a><span data-ttu-id="1f461-111">報告功能</span><span class="sxs-lookup"><span data-stu-id="1f461-111">Reporting Features</span></span>
<span data-ttu-id="1f461-112">您可以新增這些功能：</span><span class="sxs-lookup"><span data-stu-id="1f461-112">You can add these features:</span></span>

1. [<span data-ttu-id="1f461-113">進階報告選項</span><span class="sxs-lookup"><span data-stu-id="1f461-113">Advanced reporting options</span></span>](mobile-engagement-android-advanced-reporting.md)
2. [<span data-ttu-id="1f461-114">位置報告選項</span><span class="sxs-lookup"><span data-stu-id="1f461-114">Location Reporting options</span></span>](mobile-engagement-android-location-reporting.md)
3. [<span data-ttu-id="1f461-115">進階組態選項</span><span class="sxs-lookup"><span data-stu-id="1f461-115">Advanced Configuration options</span></span>](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a><span data-ttu-id="1f461-116">通知:</span><span class="sxs-lookup"><span data-stu-id="1f461-116">Notifications:</span></span>
[<span data-ttu-id="1f461-117">如何在 Android 應用程式中的 toointegrate 觸達 （通知）</span><span class="sxs-lookup"><span data-stu-id="1f461-117">How toointegrate Reach (Notifications) in your Android app</span></span>](mobile-engagement-android-integrate-engagement-reach.md)

1. <span data-ttu-id="1f461-118">Google Cloud Messaging (GCM):[如何 tooIntegrate GCM 與 Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="1f461-118">Google Cloud Messaging (GCM): [How tooIntegrate GCM with Mobile Engagement](mobile-engagement-android-gcm-integrate.md)</span></span>
2. <span data-ttu-id="1f461-119">Amazon 裝置傳訊 (ADM):[如何 tooIntegrate ADM 與 Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span><span class="sxs-lookup"><span data-stu-id="1f461-119">Amazon Device Messaging (ADM): [How tooIntegrate ADM with Mobile Engagement](mobile-engagement-android-adm-integrate.md)</span></span>

### <a name="tag-plan-implementation"></a><span data-ttu-id="1f461-120">標記計畫實作：</span><span class="sxs-lookup"><span data-stu-id="1f461-120">Tag plan implementation:</span></span>
[<span data-ttu-id="1f461-121">如何 toouse hello 進階 Mobile Engagement 標記 Android 應用程式中的應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="1f461-121">How toouse hello advanced Mobile Engagement tagging API in your Android app</span></span>](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a><span data-ttu-id="1f461-122">版本資訊</span><span class="sxs-lookup"><span data-stu-id="1f461-122">Release notes</span></span>

### <a name="431-07172017"></a><span data-ttu-id="1f461-123">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="1f461-123">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="1f461-124">修正損毀時，可能很少發生呼叫`EngagementAgentUtils.isInDedicatedEngagementProcess`，也可由 hello`EngagementApplication`類別。</span><span class="sxs-lookup"><span data-stu-id="1f461-124">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by hello `EngagementApplication` class.</span></span>

### <a name="430-06272017"></a><span data-ttu-id="1f461-125">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="1f461-125">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="1f461-126">Android 8 支援 （舊版本的 SDK 不適用於 Android 8 hello）。</span><span class="sxs-lookup"><span data-stu-id="1f461-126">Android 8 support (previous versions of hello SDK will not work on Android 8).</span></span>
* <span data-ttu-id="1f461-127">不再依賴支援程式庫。</span><span class="sxs-lookup"><span data-stu-id="1f461-127">No more dependency on support library.</span></span>
* <span data-ttu-id="1f461-128">移除 `EngagementFragmentActivity` 類別。</span><span class="sxs-lookup"><span data-stu-id="1f461-128">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="1f461-129">因為太[背景執行限制](https://developer.android.com/preview/features/background.html)Android 8，在背景中的記錄檔可能會延遲，直到 hello 使用者與 hello 裝置互動，這會影響的推送活動**Delivered**和**系統通知顯示**而延遲，如果 hello 裝置已進入休眠狀態的統計資料 （hello 通知仍會顯示，將信號和震動而不發生問題的即時）。</span><span class="sxs-lookup"><span data-stu-id="1f461-129">Due too[Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until hello user interacts with hello device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if hello device was sleeping (hello notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="1f461-130">因為太[背景的位置限制](https://developer.android.com/preview/features/background-location-limits.html)，hello 即時位置，在背景中的將不會更新經常在 Android 8。</span><span class="sxs-lookup"><span data-stu-id="1f461-130">Due too[Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), hello real time location in background will not be updated frequently on Android 8.</span></span>

<span data-ttu-id="1f461-131">對於所有版本，請參閱 hello[完成版本資訊](mobile-engagement-android-release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="1f461-131">For all versions, see hello [complete release notes](mobile-engagement-android-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="1f461-132">升級程序</span><span class="sxs-lookup"><span data-stu-id="1f461-132">Upgrade procedures</span></span>
<span data-ttu-id="1f461-133">如果您已經將較舊版的 SDK 整合到應用程式中，請參閱 [升級程序](mobile-engagement-android-upgrade-procedure.md)。</span><span class="sxs-lookup"><span data-stu-id="1f461-133">If you already have integrated an older version of our SDK into your application, consult [Upgrade Procedures](mobile-engagement-android-upgrade-procedure.md).</span></span>

