---
title: "aaaAzure 記錄分析查詢語言小祕技 |Microsoft 文件"
description: "這篇文章提供協助記錄分析的轉換 toohello 新的查詢語言，如果您已經熟悉 hello 舊版語言。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 8b4ee3d0b5e1ec8a9f95a09e0ad9835615ad1342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transitioning-tooazure-log-analytics-new-query-language"></a>轉換 tooAzure 記錄分析新的查詢語言

> [!NOTE]
> 您可以閱讀的 hello 新的記錄分析查詢語言，並取得有關您的工作區，在升級 hello 程序 tooupgrade 您[Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。

這篇文章提供協助記錄分析的轉換 toohello 新的查詢語言，如果您已經熟悉 hello 舊版語言。

## <a name="language-converter"></a>語言轉換器

如果您已熟悉 hello 舊版記錄分析查詢語言，hello toocreate hello hello 新語言中的相同查詢的最簡單方式為 toouse hello 轉換您的工作區時，在 hello 記錄搜尋入口網站安裝的語言轉換子。  使用 hello 轉換器很簡單，只在舊版查詢的 hello 頂端的文字方塊中輸入，然後按一下**轉換**。  您可以按一下 hello 搜尋按鈕 toorun hello 查詢或複製，並將它貼入 toouse 任一處。

![語言轉換器](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="cheat-sheet"></a>功能提要

hello 下表提供各種不同的一般查詢之間的比較 tooequivalent 命令之間 hello Azure 記錄分析新的版本與舊版的查詢語言。

| 說明 | 舊版 | new |
|:--|:--|:--|
| 搜尋所有資料表      | 錯誤 | 搜尋 "error" (不區分大小寫) |
| 從資料表選取資料 | Type=Event |  Event |
|                        | Type=Event &#124; select Source, EventLog, EventID | Event &#124; project Source, EventLog, EventID |
|                        | Type=Event &#124; top 100 | Event &#124; take 100 |
| 字串比較      | Type=Event Computer=srv01.contoso.com   | Event &#124; where Computer == "srv01.contoso.com" |
|                        | Type=Event Computer=contains("contoso") | Event &#124; where Computer contains "contoso" (不區分大小寫)<br>Event &#124; where Computer contains_cs "Contoso" (區分大小寫) |
|                        | Type=Event Computer=RegEx("@contoso@")  | Event &#124; where Computer matches regex ".*contoso*" |
| 日期比較        | Type=Event TimeGenerated > NOW-1DAYS | Event &#124; where TimeGenerated > ago(1d) |
|                        | Type=Event TimeGenerated>2017-05-01 TimeGenerated<2017-05-31 | Event &#124; where TimeGenerated between (datetime(2017-05-01) .. datetime(2017-05-31)) |
| 布林值比較     | Type=Heartbeat IsGatewayInstalled=false  | Heartbeat | where IsGatewayInstalled == false |
| 排序                   | Type=Event &#124; sort Computer asc, EventLog desc, EventLevelName asc | Event \| sort by Computer asc, EventLog desc, EventLevelName asc |
| Distinct               | Type=Event &#124; dedup Computer \| 選取電腦 | Event &#124; summarize by Computer, EventLog |
| 擴充資料行         | Type=Perf CounterName="% Processor Time" &#124; EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION | Perf &#124; where CounterName == "% Processor Time" \| extend Utilization = iff(CounterValue > 50, "HIGH", "LOW") |
| 彙總            | Type=Event &#124; measure count() as Count by Computer | Event &#124; summarize Count = count() by Computer |
|                                | Type=Perf ObjectName=Processor CounterName="% Processor Time" &#124; measure avg(CounterValue) by Computer interval 5minute | Perf &#124; where ObjectName=="Processor" and CounterName=="% Processor Time" &#124; summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min) |
| 限制的彙總 | Type=Event &#124; measure count() by Computer &#124; top 10 | Event &#124; summarize AggregatedValue = count() by Computer &#124; limit 10 |
| Union                  | Type=Event or Type=Syslog | union Event, Syslog |
| Join                   | Type=NetworkMonitoring &#124; join inner AgentIP (Type=Heartbeat) ComputerIP | NetworkMonitoring &#124; join kind=inner (search Type == "Heartbeat") on $left.AgentIP == $right.ComputerIP |



## <a name="next-steps"></a>後續步驟
- 簽出[上撰寫查詢的教學課程](https://go.microsoft.com/fwlink/?linkid=856078)使用 hello 新的查詢語言。
- 請參閱 toohello[查詢語言參考](https://go.microsoft.com/fwlink/?linkid=856079)如所有命令、 運算子和函式的 hello 新的查詢語言的詳細資訊。  
