---
title: "aaaAzure Mobile Engagement 疑難排解指南-分析"
description: "Azure Mobile Engagement 中分析、監視、分割，以及儀表板問題的疑難排解指南"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>分析、監視、分割，以及儀表板問題的疑難排解指南
hello 以下是可能的問題可能會遇到與 Azure Mobile Engagement 收集您的應用程式、 裝置和使用者的相關資訊的方式。

## <a name="missingdelayed-information"></a>遺漏/延遲資訊
### <a name="issue"></a>問題
* 資訊在分析、分割或儀表板中會延遲出現。
* 監視中遺漏資訊。
* 分析、分割或儀表板中遺漏資訊。
* 達到分割限制。

### <a name="causes"></a>原因
* 您可以使用 hello 分析 API，監視應用程式開發介面，和區段 API toosee，如果您是從 hello UI 遺失任何資料會顯示透過 hello 應用程式開發介面。
* 如果 hello Azure Mobile Engagement SDK 未正確地整合到應用程式，您不是能 toosee hello 分析、 分割、 監視中] 或儀表板中的資訊。
* 區段建立之後就無法變更，只能「再製」(複製) 或「終結」(刪除) 區段。 區段只能包含 10 個準則。
* hello 遺失的監視資訊最佳方式 tootest 是 toosetup 測試裝置、 解除安裝和/或 hello 測試裝置上重新安裝 hello 應用程式。
* 每隔 24 小時會重新整理分析、分割或儀表板的資訊。
* 等到 24 小時，即使 hello 區段根據先前的資訊建立之後，可能不會顯示新的區段中的資訊。
* 篩選 hello UI 中的分析資料會顯示所有的範例，這種應用程式的 hello 版本不限 （例如依名稱篩選「當機」會從您的應用程式第 1 版和第 2 版顯示)。
* hello 期間分析的日期為基礎 hello hello 使用者的裝置設定，讓的使用者的電話已設定不正確的 hello 日期無法顯示在 hello 錯誤時間週期。
* 當您使用 hello 按鈕時，會記錄資料的任何伺服器端太"test"推播通知，針對實際的推送活動只會記錄資料。

## <a name="cant-locate-items-in-ui"></a>在 UI 中找不到項目
### <a name="issue"></a>問題
* 無法建立以特定內建或自訂應用程式資訊標記準則為依據的區段。
* 分析、監視或儀表板中找不到特定內建或自訂應用程式資訊標記準則。
* 無法解譯分析、 監視、 分割或儀表板中的 hello 資料。

### <a name="causes"></a>原因
* 某些內建的項目和應用程式資訊只可用為推入準則標記，但可能不會新增 tooa 區段或看到從分析、 監視中] 或儀表板。 
* 建立項目和應用程式資訊標記不能加入 tooa 區段中，您將需要 toosetup 清單針對每個活動 tooperform hello 相同函式做為目標為根據的區段中的準則。
* 請參閱 hello 的內容功能表中的 hello Azure Mobile Engagement UI 更多協助以 hello 分析、 監控、 分割及儀表板區段以及 tooinformation。

## <a name="crash-troubleshooting"></a>當機疑難排解
### <a name="issue"></a>問題
* 分析、監視或儀表板中發生應用程式當機。

### <a name="causes"></a>原因
* tootroubleshoot 應用程式當機分析 」、 「 監視 」 或 「 儀表板中所見，請確定 toocheck hello 版本和舊版的 hello SDK 的已知問題的資訊。
* toofurther 疑難排解應用程式當機事件執行從測試裝置，您已安裝的應用程式和查閱您的裝置識別碼 hello Azure Mobile Engagement UI hello < 監視器 – 事件 > 一節中。 然後執行造成您的應用程式 toocrash hello 事件，並且查閱 hello hello Azure Mobile Engagement UI 「 監視器 – 當機 」 一節中的其他資訊。 

