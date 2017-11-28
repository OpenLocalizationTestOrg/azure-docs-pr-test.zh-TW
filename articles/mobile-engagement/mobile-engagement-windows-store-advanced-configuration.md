---
title: "aaaAdvanced 組態的 Windows 通用應用程式參與 SDK"
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
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="cab3d-103">適用於 Windows 通用 App Engagement SDK 的進階組態</span><span class="sxs-lookup"><span data-stu-id="cab3d-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cab3d-104">Universal Windows</span><span class="sxs-lookup"><span data-stu-id="cab3d-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="cab3d-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="cab3d-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="cab3d-106">iOS</span><span class="sxs-lookup"><span data-stu-id="cab3d-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="cab3d-107">Android</span><span class="sxs-lookup"><span data-stu-id="cab3d-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="cab3d-108">此程序描述如何 tooconfigure Azure Mobile Engagement Android 應用程式的各種組態選項。</span><span class="sxs-lookup"><span data-stu-id="cab3d-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cab3d-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="cab3d-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="cab3d-110">進階組態</span><span class="sxs-lookup"><span data-stu-id="cab3d-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="cab3d-111">停用自動當機報告</span><span class="sxs-lookup"><span data-stu-id="cab3d-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="cab3d-112">您可以停用報告功能的 Engagement hello 自動損毀。</span><span class="sxs-lookup"><span data-stu-id="cab3d-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="cab3d-113">然後，在發生未處理的例外狀況時，Engagement 不做任何動作。</span><span class="sxs-lookup"><span data-stu-id="cab3d-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="cab3d-114">如果您停用這項功能，則您的應用程式中未處理的損毀時，Engagement 不會傳送 hello 損毀**AND** hello 工作階段和工作不會關閉。</span><span class="sxs-lookup"><span data-stu-id="cab3d-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="cab3d-115">toodisable 自動當機報告，自訂您的組態，根據您在宣告的 hello 方式而定：</span><span class="sxs-lookup"><span data-stu-id="cab3d-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="cab3d-116">從 `EngagementConfiguration.xml` 檔案</span><span class="sxs-lookup"><span data-stu-id="cab3d-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="cab3d-117">設定報表損毀太`false`之間`<reportCrash>`和`</reportCrash>`標記。</span><span class="sxs-lookup"><span data-stu-id="cab3d-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="cab3d-118">於執行階段時從 `EngagementConfiguration` 物件</span><span class="sxs-lookup"><span data-stu-id="cab3d-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="cab3d-119">設定報表損毀 toofalse 使用 EngagementConfiguration 物件。</span><span class="sxs-lookup"><span data-stu-id="cab3d-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="cab3d-120">停用即時報告</span><span class="sxs-lookup"><span data-stu-id="cab3d-120">Disable real time reporting</span></span>
<span data-ttu-id="cab3d-121">根據預設，hello Engagement 服務報表會即時記錄。</span><span class="sxs-lookup"><span data-stu-id="cab3d-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="cab3d-122">如果您的應用程式經常報告記錄檔，它是較佳的 toobuffer hello 記錄檔和 tooreport 同時在一般時間為基礎。</span><span class="sxs-lookup"><span data-stu-id="cab3d-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="cab3d-123">這稱為「高載模式」。</span><span class="sxs-lookup"><span data-stu-id="cab3d-123">This is called “burst mode”.</span></span>

<span data-ttu-id="cab3d-124">toodo 因此，呼叫 hello 方法：</span><span class="sxs-lookup"><span data-stu-id="cab3d-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="cab3d-125">hello 引數是中的值**毫秒**。</span><span class="sxs-lookup"><span data-stu-id="cab3d-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="cab3d-126">每當您想 tooreactivate hello 即時記錄，請呼叫 hello 方法未使用任何參數，或使用 hello 0 值。</span><span class="sxs-lookup"><span data-stu-id="cab3d-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="cab3d-127">高載模式稍微增加 hello 電池壽命，但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。</span><span class="sxs-lookup"><span data-stu-id="cab3d-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="cab3d-128">我們建議使用低於 30000 (30 秒) 的高載閾值。</span><span class="sxs-lookup"><span data-stu-id="cab3d-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="cab3d-129">已儲存記錄檔是有限的 too300 項目。</span><span class="sxs-lookup"><span data-stu-id="cab3d-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="cab3d-130">如果傳送太長，您可能會遺失某些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="cab3d-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="cab3d-131">hello 高載閾值不能設定的 tooa 期間一個小於第二個。</span><span class="sxs-lookup"><span data-stu-id="cab3d-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="cab3d-132">如果這樣做，請 hello SDK 顯示追蹤與 hello 錯誤，並會自動重設 toohello 預設值為零秒。</span><span class="sxs-lookup"><span data-stu-id="cab3d-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="cab3d-133">這個觸發程序 hello SDK tooreport hello 記錄中的即時。</span><span class="sxs-lookup"><span data-stu-id="cab3d-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
