---
title: "在 OMS 記錄分析 aaaLog 搜尋 |Microsoft 文件"
description: "您要求記錄檔搜尋 tooretrieve 記錄分析中的任何資料。  本文描述新的記錄檔中記錄分析所使用的搜尋，並提供您之前建立一個需要 toounderstand 的概念。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>了解 Log Analytics 中的記錄搜尋

> [!NOTE]
> 本文說明在使用新的查詢語言 hello Azure 記錄分析記錄搜尋。  您可以深入了解 hello 新語言，並取得 hello 程序 tooupgrade 在工作區[升級您的 Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。  
>
> 如果您的工作區尚未升級的 toohello 新的查詢語言，您應該參閱太[尋找資料記錄分析中使用記錄搜尋](log-analytics-log-searches.md)。

您要求記錄檔搜尋 tooretrieve 記錄分析中的任何資料。  是否您正在分析 hello 入口網站中的資料，設定警示規則 toobe 通知的特定條件或擷取的資料使用 hello 記錄分析 API，您將使用您想要記錄檔搜尋 toospecify hello 資料。  本文說明記錄搜尋在 Log Analytics 中的使用方式，並且提供在建立之前應該了解的概念。 請參閱 hello[後續步驟](#next-steps)如需建立和編輯的記錄搜尋詳細資料和 hello 查詢語言參考一節。

## <a name="where-log-searches-are-used"></a>記錄搜尋的使用位置

hello 不同的方式，您將使用中記錄分析記錄搜尋 hello 如下：

- **入口網站。** 您可以執行互動式資料分析與 hello hello 儲存機制中[記錄搜尋入口網站](log-analytics-log-search-log-search-portal.md)或 hello [Advanced Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)。  這可讓您 tooedit 您查詢及分析各種不同的格式和視覺效果中的 hello 結果。  您所建立之大多數查詢會在其中一個 hello 入口網站中開始，然後再複製 [一旦您確認它如預期般運作。
- **警示規則。** [警示規則](log-analytics-alerts.md)會主動識別您的工作區中資料的問題。  每個警示規則是根據以固定間隔自動執行的記錄搜尋。  如果應該建立警示，hello 結果將會檢查的 toodetermine。
- **檢視。**  您可以建立視覺效果的資料包含在與使用者儀表板的 toobe[檢視表設計工具](log-analytics-view-designer.md)。  記錄搜尋提供所使用的 hello 資料[磚](log-analytics-view-designer-tiles.md)和[視覺效果部分](log-analytics-view-designer-parts.md)各檢視中。  您可以向下鑽研視覺效果部分 hello hello 資料記錄搜尋入口 tooperform 進一步分析。
- **匯出。**  當您從 hello 記錄分析工作區 tooExcel 匯出資料或[Power BI](log-analytics-powerbi.md)，建立記錄檔搜尋 toodefine hello 資料 tooexport。
- **Powershell。** 您可以從命令列或使用 Azure 自動化 runbook 執行的 PowerShell 指令碼[Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve 記錄分析的資料。  此 cmdlet 需要查詢 toodetermine hello 資料 tooretrieve。
- **Log Analytics API。**  hello[記錄分析記錄搜尋 API](log-analytics-log-search-api.md) tooretrieve 資料從 hello] 工作區可讓任何 REST API 用戶端。  hello API 要求包含對記錄分析 toodetermine hello 資料 tooretrieve 所執行的查詢。

![記錄檔搜尋](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Log Analytics 資料的組織方式
當您建置查詢時，您先判斷哪些資料表有您要尋找的 hello 資料。 每個[資料來源](log-analytics-data-sources.md)和[方案](../operations-management-suite/operations-management-suite-solutions.md)專用 hello 記錄分析工作區中的資料表中儲存其資料。  針對每個資料來源和解決方案的文件包括 hello hello 資料類型，它會建立名稱和每個屬性的描述。     許多查詢只需要從單一資料表的資料，但其他人可以使用各種不同的選項 tooinclude 資料從多個資料表。

![資料表](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>撰寫查詢
Hello 核心的記錄檔中記錄分析搜尋是[廣泛的查詢語言](https://docs.loganalytics.io/)，可讓您擷取和分析資料，從各種不同的方式 hello 儲存機制。  這個相同的查詢語言用於 [Application Insights](../application-insights/app-insights-analytics.md)。  了解 toowrite 查詢的記錄分析中的重要 toocreating 記錄搜尋的方式。  通常會先處理基本查詢，然後進行 toouse 更進階函式為您的需求變得更複雜。

hello 基本查詢結構是後面接著一系列的運算子，以縱線字元分隔的來源資料表`|`。  您可以鏈結在一起的多個運算子 toorefine hello 資料，以及執行進階函式。

例如，假設您想 toofind hello 前的十個電腦以 hello 大部分的錯誤事件 hello 透過前一天。

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

或者，您想在 hello 最後一天中沒活動訊號的 toofind 電腦。

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

如何折線圖與 hello 從過去一週的每一部電腦的處理器使用量？

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

您可以從 hello 的 hello 種類的資料，您正在使用，不論這些快速範例看到 hello 查詢的結構非常類似。  您可以細分它為不同的步驟，透過 hello 管線 toohello 下一個命令送出 hello 從一個命令產生的資料。

如需包括教學課程和語言參考 hello Azure Log Analytics 查詢語言的完整文件，請參閱 hello [Azure Log Analytics 查詢語言文件](https://docs.loganalytics.io/)。

## <a name="next-steps"></a>後續步驟

- 深入了解 hello[入口網站，您使用 toocreate 和編輯的記錄搜尋](log-analytics-log-search-portals.md)。
- 簽出[上撰寫查詢的教學課程](https://go.microsoft.com/fwlink/?linkid=856078)使用 hello 新的查詢語言。
