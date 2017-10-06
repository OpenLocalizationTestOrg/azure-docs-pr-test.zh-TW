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
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Azure Mobile Engagement 的 Android SDK 整合
> [!div class="op_single_selector"]
> * [Universal Windows](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

本文件說明所有 hello 整合和組態選項可用的 Azure Mobile Engagement Android SDK。

## <a name="prerequisites"></a>必要條件
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>進階功能
### <a name="reporting-features"></a>報告功能
您可以新增這些功能：

1. [進階報告選項](mobile-engagement-android-advanced-reporting.md)
2. [位置報告選項](mobile-engagement-android-location-reporting.md)
3. [進階組態選項](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>通知:
[如何在 Android 應用程式中的 toointegrate 觸達 （通知）](mobile-engagement-android-integrate-engagement-reach.md)

1. Google Cloud Messaging (GCM):[如何 tooIntegrate GCM 與 Mobile Engagement](mobile-engagement-android-gcm-integrate.md)
2. Amazon 裝置傳訊 (ADM):[如何 tooIntegrate ADM 與 Mobile Engagement](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>標記計畫實作：
[如何 toouse hello 進階 Mobile Engagement 標記 Android 應用程式中的應用程式開發介面](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>版本資訊

### <a name="431-07172017"></a>4.3.1 (07/17/2017)
* 修正損毀時，可能很少發生呼叫`EngagementAgentUtils.isInDedicatedEngagementProcess`，也可由 hello`EngagementApplication`類別。

### <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8 支援 （舊版本的 SDK 不適用於 Android 8 hello）。
* 不再依賴支援程式庫。
* 移除 `EngagementFragmentActivity` 類別。
* 因為太[背景執行限制](https://developer.android.com/preview/features/background.html)Android 8，在背景中的記錄檔可能會延遲，直到 hello 使用者與 hello 裝置互動，這會影響的推送活動**Delivered**和**系統通知顯示**而延遲，如果 hello 裝置已進入休眠狀態的統計資料 （hello 通知仍會顯示，將信號和震動而不發生問題的即時）。
* 因為太[背景的位置限制](https://developer.android.com/preview/features/background-location-limits.html)，hello 即時位置，在背景中的將不會更新經常在 Android 8。

對於所有版本，請參閱 hello[完成版本資訊](mobile-engagement-android-release-notes.md)。

## <a name="upgrade-procedures"></a>升級程序
如果您已經將較舊版的 SDK 整合到應用程式中，請參閱 [升級程序](mobile-engagement-android-upgrade-procedure.md)。

