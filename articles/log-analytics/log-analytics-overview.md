---
title: "aaaWhat 是在 Operations Management Suite (OMS) 的記錄分析？ | Microsoft Docs"
description: "Log Analytics 是 Operations Management Suite (OMS) 中的一項服務，可協助您收集和分析雲端和內部部署環境中的資源所產生的操作資料。  本文章提供 hello 不同元件的記錄分析和連結 toodetailed 內容的簡短概觀。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>什麼是 Log Analytics？
記錄分析是中的服務[Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) ，監視您的雲端和內部部署環境 toomaintain 其可用性及效能。  它會收集您的雲端和內部部署環境和其他監視工具 tooprovide 分析資源所產生的跨多個來源資料。  這篇文章提供 hello 值的簡短討論，記錄分析提供的運作方式概觀，並連結 toomore 詳細內容，因此您可以進一步深入。

## <a name="is-log-analytics-for-you"></a>您適合使用 Log Analytics 嗎？
如果您的 Azure 環境目前並未採用任何監視機制，您應該開始使用 [Azure 監視器](../monitoring-and-diagnostics/monitoring-overview.md)，其可收集並分析 Azure 資源的監視資料。  記錄分析可[收集資料，從 Azure 監視器](log-analytics-azure-storage.md)toocorrelate 它與其他資料，並提供其他的分析。

如果您想 toomonitor 在內部部署環境或您有現有的監視使用服務，例如 Azure 監視器或 System Center Operations Manager，記錄分析可以加入重要的值。  它可以直接從您的代理程式，也可以從其他工具將資料收集到單一存放庫中。  Log Analytics 中的分析工具 (例如記錄搜尋、檢視和解決方案) 可處理所有收集的資料，進而為您提供整個環境的集中式分析。


## <a name="using-log-analytics"></a>使用 Log Analytics
您可以存取記錄分析透過 hello OMS 入口網站或 hello Azure 入口網站的任何瀏覽器中執行，並提供您具有存取 tooconfiguration 設定和多個工具 tooanalyze 然後處理收集的資料。  您可以從 hello 入口網站利用[記錄搜尋](log-analytics-log-searches.md)建構查詢 tooanalyze 收集資料，其中[儀表板](log-analytics-dashboards.md)您可利用圖形檢視，您最有價值的搜尋，自訂和[解決方案](log-analytics-add-solutions.md)這兩個提供額外的功能和分析工具。

hello 圖是從 hello OMS 入口網站顯示 hello 的摘要資訊的顯示 hello 儀表板[解決方案](#add-functionality-with-management-solutions)hello 工作區中所安裝。  您可以按一下任何磚 toodrill 進一步 hello 資料為該方案。

![OMS 入口網站](media/log-analytics-overview/portal.png)

記錄分析包含查詢語言 tooquickly 擷取和彙總 hello 儲存機制中的資料。  您可以建立並儲存[記錄搜尋](log-analytics-log-searches.md)toodirectly 分析 hello 入口網站中的資料或記錄搜尋執行自動 toocreate 警示如果 hello hello 查詢結果會指出重要條件。

![記錄搜尋](media/log-analytics-overview/log-search.png)

tooget 整體環境的 hello 健全狀況的快速圖形檢視，您可以加入視覺效果的已儲存的記錄搜尋 tooyour[儀表板](log-analytics-dashboards.md)。   

![儀表板](media/log-analytics-overview/dashboard.png)

在訂單 tooanalyze 外部記錄分析的資料，您可以將匯出 hello 資料 hello OMS 儲存機制從工具例如[Power BI](log-analytics-powerbi.md)或 Excel。  您也可以利用 hello [Log Search API](log-analytics-log-search-api.md) toobuild 利用記錄分析資料或 toointegrate 與其他系統的自訂解決方案。

## <a name="add-functionality-with-management-solutions"></a>透過管理解決方案新增功能
[管理解決方案](log-analytics-add-solutions.md)新增功能 tooOMS，提供額外的資料和分析工具 tooLog 分析。  它們也必須定義新記錄類型 toobe 收集可分析記錄搜尋而 hello 儀表板中的 hello 方案所提供的其他使用者介面。  下面的 hello 範例影像會顯示 hello[變更追蹤解決方案](log-analytics-change-tracking.md)

![資料追蹤方案](media/log-analytics-overview/change-tracking.png)

有些解決方案適用於各種功能，而其他解決方案則會以一致的方式新增。  您可以輕鬆地瀏覽可用的解決方案和[將它們加入 tooyour OMS 工作區](log-analytics-add-solutions.md)hello 解決方案資源庫或 Azure Marketplace。  許多將會自動部署並立即開始運作，而有些則可能需要適度設定。

![方案庫](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Log Analytics 元件
Hello 中心記錄分析是 hello OMS 儲存機制裝載在 hello Azure 雲端。  到 hello 儲存機制從所設定的資料來源和加入解決方案 tooyour 訂用帳戶連線來源收集資料。  資料來源和解決方案將每個建立自己的屬性集，但可能仍然會分析一起查詢 toohello 儲存機制中不同的記錄類型。  這可讓您 toouse hello 與不同類型的資料相同的工具和方法 toowork 收集不同的來源。

![OMS 存放庫](media/log-analytics-overview/overview.png)

已連線的來源為 hello 電腦及其他資源，產生記錄分析所收集的資料。  這可以包括安裝在直接連接的 [Windows](log-analytics-windows-agents.md) 和 [Linux](log-analytics-linux-agents.md) 電腦的代理程式，或[已連線的 System Center Operations Manager 管理群組](log-analytics-om-agents.md)中的代理程式。  對於 Azure 資源，Log Analytics 會從 [Azure 監視器和 Azure 診斷](log-analytics-azure-storage.md)收集資料。

[資料來源](log-analytics-data-sources.md)hello 不同的每個連接的來源收集資料。  這包括[事件](log-analytics-data-sources-windows-events.md)和[效能資料](log-analytics-data-sources-performance-counters.md)從[Windows](log-analytics-data-sources-windows-events.md)和 Linux 代理程式，例如加法 toosources 中的[IIS 記錄檔](log-analytics-data-sources-iis-logs.md)，和[自訂文字記錄檔](log-analytics-data-sources-custom-logs.md)。  您設定您想要 toocollect，，和 hello 組態會自動傳遞的 tooeach 已連接的來源的每個資料來源。

如果您有自訂需求，則您可以使用 hello [HTTP 資料收集器 API](log-analytics-data-collector-api.md) toowrite 資料 toohello 儲存機制從 REST API 用戶端。

## <a name="log-analytics-architecture"></a>Log Analytics 架構
記錄分析的 hello 部署需求很低，因為 hello 的中央元件所裝載的 hello Azure 雲端。  這包括 hello 儲存機制中加入 toohello 服務，允許您 toocorrelate 和分析收集到的資料。  可以從任何瀏覽器存取 hello 入口網站，因此不需要用戶端軟體。

您必須在 [Windows](log-analytics-windows-agents.md) 和 [Linux](log-analytics-linux-agents.md) 電腦上安裝代理程式，但已經是[連線的 SCOM 管理群組](log-analytics-om-agents.md)成員的電腦則不需要其他代理程式。  SCOM 代理程式將會繼續與管理伺服器將會轉送其資料 tooLog 分析 toocommunicate。  雖然某些方案將需要代理程式 toocommunicate 直接與記錄分析。  每個解決方案的 hello 文件會指定其通訊需求。

當您 [註冊 Log Analytics](log-analytics-get-started.md)時，會建立一個 OMS 工作區。  您可以將 hello 工作區視為唯一的記錄分析環境與它自己的資料儲存機制、 資料來源和解決方案。 您可以建立多個工作區，在您的訂用帳戶 toosupport 多個環境，例如生產和測試。

![Log Analytics 架構](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>後續步驟
* [申請免費的記錄分析帳戶](log-analytics-get-started.md)tootest 您自己的環境中。
* 不同的檢視 hello[資料來源](log-analytics-data-sources.md)可用 toocollect 資料到 hello OMS 儲存機制。
* [瀏覽 hello hello 解決方案資源庫中可用的解決方案](log-analytics-add-solutions.md)tooadd 功能 tooLog 分析。

