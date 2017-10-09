---
title: "aaaLog 分析新的記錄搜尋常見問題集 |Microsoft 文件"
description: "本文章提供有關 hello 升級記錄分析 toohello 新查詢語言的常見問題的解答。"
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
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Log Analytics 新記錄搜尋常見問題集與已知問題

這篇文章包含常見問題集與有關 hello 升級的已知的問題[記錄分析 toohello 新查詢語言](log-analytics-log-search-upgrade.md)。  您應該閱讀這份文件之前 hello 決策 tooupgrade 您的工作區。


## <a name="alerts"></a>Alerts

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>問題：我有大量的警示規則。 我需要 toocreate 它們一次在升級之後 hello 新語言？  
否，您的警示規則是新搜尋語言會自動轉換的 toohello 升級期間。  


## <a name="computer-groups"></a>電腦群組

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>問題： 我會收到錯誤時嘗試 toouse 電腦群組。  其語法是否已變更？
是，hello 語法會使用電腦群組變更，升級您的工作區時。  如需詳細資訊，請參閱 [Log Analytics 記錄檔搜尋中的電腦群組](log-analytics-computer-groups.md)。

### <a name="known-issue-groups-imported-from-active-directory"></a>已知問題：從 Active Directory 匯入的群組
您目前無法建立使用從 Active Directory 匯入之電腦群組的查詢。  因應措施更正此問題，直到建立新的電腦群組，使用 hello 匯入 Active Directory 群組，然後在查詢中使用該新的群組。

範例查詢 toocreate 包含匯入 Active Directory 群組的新電腦群組如下所示：

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>儀表板

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>問題：是否仍然可以在升級的工作區中使用儀表板？
您可以繼續 toouse 您新增過任何磚**我的儀表板**之前已升級您的工作區，但您無法編輯這些圖格，或加入新的。  您可以繼續 toocreate 和編輯與檢視[檢視表設計工具](log-analytics-view-designer.md)也可以在 hello Azure 入口網站中建立儀表板。


## <a name="log-searches"></a>記錄檔搜尋

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>問題：我已在升級工作區之外儲存搜尋。 可以將它們轉換 toohello 新搜尋語言會自動嗎？
您可以使用每個在 hello 記錄搜尋頁面 tooconvert hello 語言轉換器工具。  沒有任何方法 tooautomatically 轉換而不升級 hello 工作區的多個搜尋。

### <a name="question-why-are-my-query-results-not-sorted"></a>問題： 為什麼我的查詢結果未排序？
根據預設，在 hello 新的查詢語言，不會排序結果。  使用 hello [sort 運算子](https://go.microsoft.com/fwlink/?linkid=856079)toosort 您依照一個或多個屬性的結果。

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>已知問題：清單中的搜尋結果可能包含沒有資料的屬性
清單中的記錄搜尋結果可能會顯示沒有資料的屬性。  先前 tooupgrade，這些屬性就不會包含在內。  未來將修正此問題，以避免顯示空白屬性。

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>已知問題：選取圖表中的值不會顯示詳細結果
先前 tooupgrade，當您在圖表中，選取值，它就會傳回符合選取的 hello 值記錄的詳細的清單。  升級之後，就會傳回只 hello 單一摘要的行。  目前正在調查此問題。

## <a name="log-search-api"></a>記錄檔搜尋 API

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>問題： 未 hello Log Search API 取得更新之後升級嗎？
hello [Log Search API](log-analytics-log-search-api.md)尚未升級的 toohello 新搜尋語言。  即使在工作區升級之後，請繼續 toouse hello 舊版的查詢語言，使用此 API。  當更新時，更新文件將會提供 hello Log Search API。


## <a name="portals"></a>入口網站

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>問題： 應該使用 hello 新 Advanced Analytics 入口網站或繼續使用 hello 記錄搜尋入口網站？
您可以看到在 hello 兩個入口網站的比較[入口網站來建立和編輯 Azure 記錄分析中的記錄檔查詢](log-analytics-log-search-portals.md)。  每個有不同的優點，因此您可以選擇 hello 適合您的需求。  它是在 hello Advanced Analytics 入口網站中的一般 toowrite 查詢，並將它們貼至其他位置，例如檢視表設計工具。  您應該閱讀[發出 tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal)執行之時。


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>問題：PowerBI 整合有任何變更嗎？
是。  一旦升級您的工作區之後就無法再運作匯出記錄分析資料 tooPower BI hello 程序。  您在升級之前建立的任何現有排程將會變成停用。  升級之後，Azure 記錄分析會使用 hello Application Insights 為相同的平台，而且您使用相同的處理序 tooexport 記錄分析查詢 tooPower 為 BI hello [hello 程序 tooexport Application Insights 查詢 tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)。

### <a name="known-issue-power-bi-request-size-limit"></a>已知問題：Power BI 要求大小限制
目前沒有的記錄分析查詢，可以匯出的 tooPower BI 8 MB 的大小限制。  此限制即將放寬。


##<a name="powershell-cmdlets"></a>PowerShell Cmdlet

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>問題： 未 hello 記錄搜尋 PowerShell cmdlet 取得更新之後升級嗎？
hello [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults)尚未升級的 toohello 新搜尋語言。  即使在工作區升級之後，請繼續 toouse hello 舊版的查詢語言，與這個指令程式。  當更新時，更新文件將會提供 hello 指令程式。


## <a name="resource-manager-templates"></a>Resource Manager 範本

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>問題：我可以使用 Resource Manager 範本建立升級工作區嗎？
是。  您必須使用 2017年-03-15-預覽的應用程式開發介面版本，並包含**功能**如 hello 下列範例所示在範本中的區段。

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>解決方案

### <a name="question-will-my-solutions-continue-toowork"></a>問題： 我的方案將會繼續 toowork 嗎？
所有方案會在升級後的工作區，都繼續 toowork，但如果它們是轉換的 toohello 新的查詢語言，可改善其效能。  本節中所述之現有解決方案目前已知存在問題。

### <a name="known-issue-capacity-and-performance-solution"></a>已知問題：容量與效能解決方案
某些 hello 組件以 hello[容量和效能](log-analytics-capacity.md)可能是空的檢視。  修正 toothis 問題將會很快。

### <a name="known-issue-device-health-solution"></a>已知問題：裝置健康情況解決方案
hello[裝置健全狀況解決方案](https://docs.microsoft.com/windows/deployment/update/device-health-monitor)不會收集在升級後的工作區中的資料。  修正 toothis 問題將會很快。

### <a name="known-issue-application-insights-connector"></a>已知問題：Application Insights Connector
已升級工作區目前不支援 [Application Insights Connector 解決方案](log-analytics-app-insights-connector.md)中的檢視方塊。  修正 toothis 問題目前正在進行分析。

## <a name="upgrade-process"></a>升級程序

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>問題：我有數個工作區。 我可以升級在 hello 的所有工作區相同的時間？  
否。  升級適用於每次 tooa 單一工作區。 目前無法一次升級多個工作區。 請注意，將也會受到 hello 升級 工作區的其他使用者的影響。  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>問題：如果我升級，我的工作區中收集的現有記錄資料會被修改嗎？  
否。 hello 的記錄資料可用 tooyour 工作區中搜尋不會受到 hello 升級。 已儲存的搜尋，警示和檢視都會自動轉換的 toohello 新搜尋語言。  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>問題：如果不升級我的工作區會發生什麼事？  
hello 舊版的記錄搜尋將會取代來自數個月的 hello。 屆時未升級的工作區將會自動升級。

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>問題： 未選擇 tooupgrade，但仍已升級我的工作區 ！ 發生什麼情形？  
此工作區的另一個系統管理員可能已經升級為 hello 工作區。 請注意，所有工作區時便會自動升級 hello 新語言正式運作。  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>問題： 我有升級不小心，而且它和還原的所有項目後，現在需要 toocancel。 我該怎麼辦？！  
沒問題。  我們會在升級時之前建立工作區的快照集，以便您可以將它還原。 請記住，警示或搜尋後 hello 升級但將會遺失您所儲存的檢視。  toorestore 您工作區的環境，在後續 hello 程序[可以在哪裡尋求之後升級嗎？](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Views

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>問題：如何使用檢視設計工具建立新的檢視？
先前 tooupgrade，您可以建立新的檢視與檢視設計工具從 hello 主要儀表板上的磚。  升級您的工作區時，會移除此圖格。  您可以建立新的檢視與檢視設計工具 hello OMS 入口網站中按一下綠色的 hello + hello 左功能表中的按鈕。

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>已知問題：折線圖的檢視全部選項不會產生折線圖
當您按一下 hello*查看所有*選項在 hello 下方列圖表部分檢視中，您會看到與資料表。  先前 tooupgrade，就會顯示與折線圖。  目前正在分析此問題以進行可能的修改。


## <a name="next-steps"></a>後續步驟

- 深入了解[升級您的工作區 toohello 新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)。
