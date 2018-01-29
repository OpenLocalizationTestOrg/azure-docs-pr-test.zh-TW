---
title: "分析 Azure CDN 使用模式 | Microsoft Docs"
description: "客戶可以啟用 Azure CDN 的記錄分析功能。"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: ce9ec021250a3548e23ad87273a9225cdf700c70
ms.sourcegitcommit: 7f1ce8be5367d492f4c8bb889ad50a99d85d9a89
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>分析 Azure CDN 使用模式

啟用應用程式的 CDN 後，您可以監視 CDN 使用情況、檢查傳遞的健康情況，並為可能的問題進行疑難排解。 Azure CDN 會以下列方式提供這些功能： 

## <a name="core-analytics-via-azure-diagnostic-logs"></a>透過 Azure 診斷記錄的核心分析

核心分析適用於所有屬於 Verizon (標準與進階) 及 Akamai (標準) CDN 設定檔的 CDN 端點。 Azure 診斷記錄可以將核心分析匯出至 Azure 儲存體、事件中樞或 Operations Management Suite (OMS) 記錄分析。 OMS 記錄分析會提供具有圖表的解決方案，這些圖表可由使用者設定和自訂。 如需詳細資訊，請參閱 [Azure 診斷記錄](cdn-azure-diagnostic-logs.md)。

## <a name="verizon-core-reports"></a>Verizon 核心報告

身為具有 Verizon 標準或 Verizon 進階設定檔的 Azure CDN 使用者，您可以在 Verizon 補充入口網站中檢視 Verizon 核心報告。 Verizon 核心報告可以透過 Azure 入口網站的 [管理] 選項存取，並提供各式各樣的圖表和檢視。 如需詳細資訊，請參閱 [Verizon 核心報告](cdn-analyze-usage-patterns.md)。

## <a name="verizon-custom-reports"></a>Verizon 自訂報告

身為具有 Verizon 標準或 Verizon 進階設定檔的 Azure CDN 使用者，您可以在 Verizon 補充入口網站中檢視 Verizon 自訂報告。 Verizon 自訂報告可以透過 Azure 入口網站的 [管理] 選項存取。 [Verizon 自訂報告] 頁面會針對屬於 Azure CDN 設定檔的每個邊緣 CName 顯示點擊次數或傳輸的資料。 此資料可依照任何一段時間的 HTTP 回應碼或快取狀態進行分組。 如需詳細資訊，請參閱 [Verizon 自訂報告](cdn-verizon-custom-reports.md)。

## <a name="verizon-premium-reports"></a>Verizon 高階報告

您也可以使用**來自 Verizon 的 Azure CDN 進階** 來存取下列報告：
   * [進階 HTTP 報告](cdn-advanced-http-reports.md)
   * [即時統計資料](cdn-real-time-stats.md)
   * [邊緣節點效能](cdn-edge-performance.md)

