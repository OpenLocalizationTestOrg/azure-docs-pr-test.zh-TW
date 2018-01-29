---
title: "Azure Mobile Engagement 疑難排解指南 - 分析"
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
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>分析、監視、分割，以及儀表板問題的疑難排解指南
以下是您可能會遇到，有關 Azure Mobile Engagement 如何收集應用程式、裝置和使用者相關資訊的問題。

## <a name="missingdelayed-information"></a>遺漏/延遲資訊
### <a name="issue"></a>問題
* 資訊在分析、分割或儀表板中會延遲出現。
* 監視中遺漏資訊。
* 分析、分割或儀表板中遺漏資訊。
* 達到分割限制。

### <a name="causes"></a>原因
* 您可以使用分析 API、監視 API 與區段 API，查看是否能透過 API 看到 UI 中遺漏的任何資料。
* 如果 Azure Mobile Engagement SDK 未正確地整合到您的應用程式中，您就無法查看分析、分割、監視或儀表板中的資訊。
* 區段建立之後就無法變更，只能「再製」(複製) 或「終結」(刪除) 區段。 區段只能包含 10 個準則。
* 測試監視中遺漏資訊的最佳方式是安裝測試裝置、解除安裝及/或重新安裝測試裝置上的應用程式。
* 每隔 24 小時會重新整理分析、分割或儀表板的資訊。
* 在新區段建立 24 小時之後，新區段中的資訊才會顯示，即使該區段是以先前的資訊為根據。
* 在 UI 中篩選您的分析資料，無論您的應用程式版本為何，將會顯示此類型的所有範例。(例如，依名稱篩選「當機」會從您的應用程式第 1 版和第 2 版顯示)。
* 分析的時間週期是以使用者裝置設定的日期為依據，因此使用者的手機日期設定如果不正確，可能會顯示錯誤的時間週期。
* 當您使用按鈕來「測試」推送時，不會記錄任何伺服器端的資料，只會記錄實際推送活動的資料。

## <a name="cant-locate-items-in-ui"></a>在 UI 中找不到項目
### <a name="issue"></a>問題
* 無法建立以特定內建或自訂應用程式資訊標記準則為依據的區段。
* 分析、監視或儀表板中找不到特定內建或自訂應用程式資訊標記準則。
* 無法解譯分析、監視、分割或儀表板中的資料。

### <a name="causes"></a>原因
* 部分內建項目與應用程式資訊標記只能做為推送準則使用，無法新增至區段，或是顯示於分析、監視或儀表板中。 
* 對於無法新增至區段的內建項目與應用程式資訊標記，您必須在每個活動中設定目標準則的清單，來執行以區段為依據之目標的相同函式。
* 請參閱 Azure Mobile Engagement UI 的分析、監視、分割及儀表板區段中的操作功能表，以取得更多協助與使用方式資訊。

## <a name="crash-troubleshooting"></a>當機疑難排解
### <a name="issue"></a>問題
* 分析、監視或儀表板中發生應用程式當機。

### <a name="causes"></a>原因
* 如果要疑難排解分析、監視或儀表板中發生的應用程式當機，請務必查看版本資訊，了解舊版 SDK 的已知問題。
* 若要進一步疑難排解應用程式當機，請在已安裝您應用程式的測試裝置上執行事件，並在 Azure Mobile Engagement UI 的 [監視 – 事件] 區段中查詢您的裝置識別碼。 然後執行造成應用程式當機的事件，並查詢 Azure Mobile Engagement UI 的 [監視 – 當機] 區段中的其他資訊。 

