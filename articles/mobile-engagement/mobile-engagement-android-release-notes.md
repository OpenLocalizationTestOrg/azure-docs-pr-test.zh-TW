---
title: "aaaAzure Mobile Engagement Android SDK 整合"
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
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>版本資訊

## <a name="431-07172017"></a>4.3.1 (07/17/2017)
* 修正損毀時，可能很少發生呼叫`EngagementAgentUtils.isInDedicatedEngagementProcess`，也可由 hello`EngagementApplication`類別。

## <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8 支援 （舊版本的 SDK 不適用於 Android 8 hello）。
* 不再依賴支援程式庫。
* 移除 `EngagementFragmentActivity` 類別。
* 因為太[背景執行限制](https://developer.android.com/preview/features/background.html)Android 8，在背景中的記錄檔可能會延遲，直到 hello 使用者與 hello 裝置互動，這會影響的推送活動**Delivered**和**系統通知顯示**而延遲，如果 hello 裝置已進入休眠狀態的統計資料 （hello 通知仍會顯示，將信號和震動而不發生問題的即時）。
* 因為太[背景的位置限制](https://developer.android.com/preview/features/background-location-limits.html)，hello 即時位置，在背景中的將不會更新經常在 Android 8。

## <a name="424-03302017"></a>4.2.4 (03/30/2017)
* 修正應用程式內通知 Android 7 toobe 上的文字色彩 hello 相同較舊的 Android 版本。

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* 不會再鎖定 WIFI。
* 修正在 init 之前呼叫 getDeviceId 時的死結問題 (4.2.0 中引進的錯誤)。

## <a name="422-05172016"></a>4.2.2 (2016/05/17)
* 穩定性改進。

## <a name="421-05102016"></a>4.2.1 (2016/05/10)
* 安全性︰停用 Web 檢視本機檔案存取權限。
* 安全性︰移除 `EngagementPreferenceActivity` 類別，其可擴充過時且不安全的 `PreferenceActivity` 類別。
* 安全性： 觸達活動現在已記載 toouse `exported="false"`，此旗標也可用在先前的 SDK 版本。

## <a name="420-03112016"></a>4.2.0 (03/11/2016)
* hello SDK 現在是 MIT 授權。
* 允許在 SDK 初始化階段指定自訂裝置識別碼。

## <a name="415-02012016"></a>4.1.5 (02/01/2016)
* 穩定性改進。

## <a name="414-01262016"></a>4.1.4 (01/26/2016)
* 穩定性改進。

## <a name="413-1292015"></a>4.1.3 (12/9/2015)
* 穩定性改進。

## <a name="412-11252015"></a>4.1.2 (11/25/2015)
* 穩定性改進。

## <a name="411-11042015"></a>4.1.1 (11/04/2015)
* 穩定性改進。

## <a name="410-08252015"></a>4.1.0 (2015/08/25)
* 處理 Android M 的新權限模型。
* 除了使用 `AndroidManifest.xml` 之外，現在可以在執行階段設定定位功能。
* 修正權限錯誤：如果您使用 `ACCESS_FINE_LOCATION`，就不再需要 `ACCESS_COARSE_LOCATION`。
* 穩定性改進。

## <a name="400-07062015"></a>4.0.0 (07/06/2015)
* 內部通訊協定變更 toomake 分析及推播更可靠。
* 原生推送 (GCM/ADM) 現在也用於應用程式內通知，您必須設定為任何類型的推播宣傳活動 hello 原生推送認證。
* 修正大圖片通知：它們只會在推播之後顯示 10 秒。
* 在 web 檢視中修正的 bug： 的連結也執行 hello 預設動作 URL。
* 修正極少數的損毀相關 toolocal 存放裝置管理。
* 修正動態組態字串管理。
* 更新 EULA。

## <a name="300-02172015"></a>3.0.0 (2015/02/17)
* Azure Mobile Engagement 的最初發行版本
* appId 組態取代為連接字串組態。
* 移除應用程式開發介面 toosend 和任意 XMPP 訊息接收任意 XMPP 實體。
* 移除應用程式開發介面 toosend 和接收裝置之間的訊息。
* 增強安全性。
* 已移除 Google Play 和 SmartAd 追蹤。

