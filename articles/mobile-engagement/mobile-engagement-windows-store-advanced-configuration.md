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
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>適用於 Windows 通用 App Engagement SDK 的進階組態
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

此程序描述如何 tooconfigure Azure Mobile Engagement Android 應用程式的各種組態選項。

## <a name="prerequisites"></a>必要條件
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>進階組態
### <a name="disable-automatic-crash-reporting"></a>停用自動當機報告
您可以停用報告功能的 Engagement hello 自動損毀。 然後，在發生未處理的例外狀況時，Engagement 不做任何動作。

> [!WARNING]
> 如果您停用這項功能，則您的應用程式中未處理的損毀時，Engagement 不會傳送 hello 損毀**AND** hello 工作階段和工作不會關閉。
> 
> 

toodisable 自動當機報告，自訂您的組態，根據您在宣告的 hello 方式而定：

#### <a name="from-engagementconfigurationxml-file"></a>從 `EngagementConfiguration.xml` 檔案
設定報表損毀太`false`之間`<reportCrash>`和`</reportCrash>`標記。

#### <a name="from-engagementconfiguration-object-at-run-time"></a>於執行階段時從 `EngagementConfiguration` 物件
設定報表損毀 toofalse 使用 EngagementConfiguration 物件。

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>停用即時報告
根據預設，hello Engagement 服務報表會即時記錄。 如果您的應用程式經常報告記錄檔，它是較佳的 toobuffer hello 記錄檔和 tooreport 同時在一般時間為基礎。 這稱為「高載模式」。

toodo 因此，呼叫 hello 方法：

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

hello 引數是中的值**毫秒**。 每當您想 tooreactivate hello 即時記錄，請呼叫 hello 方法未使用任何參數，或使用 hello 0 值。

高載模式稍微增加 hello 電池壽命，但有 hello Engagement 監視影響： 所有工作階段和作業的持續時間會捨入的 toohello 高載臨界值 （因此，工作階段和短 hello 高載閾值可能不會顯示作業）。 我們建議使用低於 30000 (30 秒) 的高載閾值。 已儲存記錄檔是有限的 too300 項目。 如果傳送太長，您可能會遺失某些記錄檔。

> [!WARNING]
> hello 高載閾值不能設定的 tooa 期間一個小於第二個。 如果這樣做，請 hello SDK 顯示追蹤與 hello 錯誤，並會自動重設 toohello 預設值為零秒。 這個觸發程序 hello SDK tooreport hello 記錄中的即時。
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
