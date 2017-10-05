---
title: "適用於 Windows 通用 App Engagement SDK 的進階組態"
description: "適用於 Azure Mobile Engagement 與 Windows 通用 App 的進階組態選項"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: cb9454212c94cf65093219c3d24c71277ede7877
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="7ffa4-103">適用於 Windows 通用 App Engagement SDK 的進階組態</span><span class="sxs-lookup"><span data-stu-id="7ffa4-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ffa4-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="7ffa4-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="7ffa4-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7ffa4-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="7ffa4-106">iOS</span><span class="sxs-lookup"><span data-stu-id="7ffa4-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="7ffa4-107">Android</span><span class="sxs-lookup"><span data-stu-id="7ffa4-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="7ffa4-108">此程序描述如何設定 Azure Mobile Engagement Android 應用程式的各種組態選項。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-108">This procedure describes how to configure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ffa4-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="7ffa4-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="7ffa4-110">進階組態</span><span class="sxs-lookup"><span data-stu-id="7ffa4-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="7ffa4-111">停用自動當機報告</span><span class="sxs-lookup"><span data-stu-id="7ffa4-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="7ffa4-112">您可以停用 Engagement 的自動當機報告功能。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-112">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="7ffa4-113">然後，在發生未處理的例外狀況時，Engagement 不做任何動作。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="7ffa4-114">如果您停用此功能，則當應用程式中發生未處理的當機時，Engagement 不會傳送該當機，「且」不會關閉工作階段和工作。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send the crash **AND** does not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="7ffa4-115">若要停用自動當機報告，請依照您宣告的方式自訂您的組態：</span><span class="sxs-lookup"><span data-stu-id="7ffa4-115">To disable automatic crash reporting, customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="7ffa4-116">從 `EngagementConfiguration.xml` 檔案</span><span class="sxs-lookup"><span data-stu-id="7ffa4-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="7ffa4-117">在 `<reportCrash>` 和 `</reportCrash>` 標記之間，將報告當機設為 `false`。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-117">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="7ffa4-118">於執行階段時從 `EngagementConfiguration` 物件</span><span class="sxs-lookup"><span data-stu-id="7ffa4-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="7ffa4-119">使用 EngagementConfiguration 物件將報告當機設為 false。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-119">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="7ffa4-120">停用即時報告</span><span class="sxs-lookup"><span data-stu-id="7ffa4-120">Disable real time reporting</span></span>
<span data-ttu-id="7ffa4-121">根據預設，Engagement 會即時報告記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-121">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="7ffa4-122">如果應用程式報告記錄檔的頻率很高，建議您緩衝記錄檔，以固定時段一次報告全部的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-122">If your application reports logs frequently, it is better to buffer the logs and to report them all at once on a regular time basis.</span></span> <span data-ttu-id="7ffa4-123">這稱為「高載模式」。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-123">This is called “burst mode”.</span></span>

<span data-ttu-id="7ffa4-124">若要這樣做，請呼叫方法：</span><span class="sxs-lookup"><span data-stu-id="7ffa4-124">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="7ffa4-125">該引數是以 「毫秒」為單位的值。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-125">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="7ffa4-126">如果您想要重新啟動及時記錄，可以呼叫該方法，而不需要使用任何參數 (或使用 0 為值)。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-126">Whenever you want to reactivate the real-time logging, call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="7ffa4-127">高載模式可以稍微延長電池使用時間但對 Engagement 監視器會有影響：所有工作階段和工作持續時間會調整為高載閾值 (因此，可能將看不到時間比高載閾值短的工作階段和作業)。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-127">Burst mode slightly increases the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration are rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="7ffa4-128">我們建議使用低於 30000 (30 秒) 的高載閾值。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="7ffa4-129">儲存的記錄檔僅限 300 個項目。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-129">Saved logs are limited to 300 items.</span></span> <span data-ttu-id="7ffa4-130">如果傳送太長，您可能會遺失某些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="7ffa4-131">高載閾值無法設定為小於一秒的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-131">The burst threshold cannot be configured to a period less than one second.</span></span> <span data-ttu-id="7ffa4-132">如果您這樣做，SDK 會顯示含錯誤訊息的追蹤，並且自動重設為預設值 (0 秒)。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-132">If you do so, the SDK shows a trace with the error and automatically resets to the default value, zero seconds.</span></span> <span data-ttu-id="7ffa4-133">這樣會觸發 SDK 以即時的方式報告記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7ffa4-133">This triggers the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
