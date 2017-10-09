---
title: "在 Azure Log Analytics aaaUsing hello 記錄搜尋入口網站 |Microsoft 文件"
description: "本文包含的教學課程，描述如何 toocreate 記錄搜尋並分析資料儲存在您使用 hello 記錄搜尋入口網站的記錄分析工作區中。  hello 教學課程包含 tooreturn 不同類型的資料執行一些簡單的查詢和分析的結果。"
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
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>在 Azure Log Analytics 使用 hello 記錄搜尋入口網站中建立的記錄搜尋

> [!NOTE]
> 本文說明 hello Azure Log Analytics 使用 hello 新的查詢語言中的記錄搜尋入口網站。  您可以深入了解 hello 新語言，並取得 hello 程序 tooupgrade 在工作區[升級您的 Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。  
>
> 如果您的工作區尚未升級的 toohello 新的查詢語言，您應該參閱太[尋找資料記錄分析中使用記錄搜尋](log-analytics-log-searches.md)hello 最新版 hello 記錄搜尋入口網站上的資訊。

本文包含的教學課程，描述如何 toocreate 記錄搜尋並分析資料儲存在您使用 hello 記錄搜尋入口網站的記錄分析工作區中。  hello 教學課程包含 tooreturn 不同類型的資料執行一些簡單的查詢和分析的結果。  它著重在 hello 修改 hello 查詢，而不是直接修改的記錄搜尋入口網站中的功能。  如需直接編輯 hello 查詢的詳細資訊，請參閱 hello[查詢語言參考](https://go.microsoft.com/fwlink/?linkid=856079)。

toocreate 搜尋在 hello Advanced Analytics 入口網站，而不是 hello 記錄搜尋入口網站，請參閱[hello Analytics 入口網站使用者入門](https://go.microsoft.com/fwlink/?linkid=856587)。  這兩個入口網站使用 hello 相同語言 tooaccess hello hello 記錄分析工作區中的相同資料的查詢。

## <a name="prerequisites"></a>必要條件
本教學課程假設您已經有產生的資料為 hello 查詢 tooanalyze 的至少一個已連接來源的記錄分析工作區。  

- 如果您沒有工作區，您可以建立一份免費使用 hello 程序在[開始記錄分析工作區使用](log-analytics-get-started.md)。
- 連線至少一個[Windows 代理程式](log-analytics-windows-agents.md)或一個[Linux 代理程式](log-analytics-linux-agents.md)toohello 工作區。  

## <a name="open-hello-log-search-portal"></a>開啟 hello 記錄搜尋入口網站
首先開啟 hello 記錄搜尋入口網站。  您可以在 hello Azure 入口網站或 hello OMS 入口網站存取它。

1. 開啟 hello Azure 入口網站。
2. 瀏覽 tooLog 分析，然後選取您的工作區。
3. 請選取**記錄搜尋**在 hello Azure 入口網站或啟動 hello OMS 入口網站選取 toostay **OMS 入口網站**，然後按一下hello 記錄搜尋 按鈕。

![記錄檔搜尋按鈕](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>建立簡單搜尋
最快方式 tooretrieve hello 與某些資料 toowork 是簡單的查詢，傳回資料表中的所有記錄。  如果您有任何 Windows 或 Linux 用戶端連線的 tooyour 工作區，然後您就有可能是 hello 事件 (Windows) 或 Syslog (Linux) 資料表中的資料。

輸入一個 hello 遵循 hello [搜尋] 方塊中的查詢，然後按一下 hello [搜尋] 按鈕。  

```
Event
```
```
Syslog
```

中的 hello 預設清單檢視中，傳回資料，您可以看到所傳回的總記錄數。

![簡單查詢](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

只有 hello 每一筆記錄的第一個幾個屬性會顯示。  按一下**顯示更多**toodisplay 特定記錄的所有屬性。

![記錄詳細資料](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>設定 hello 時間範圍
記錄分析所收集的每一筆記錄有**TimeGenerated**建立該 hello 記錄屬性，其中包含 hello 日期和時間。  Hello 記錄搜尋入口網站中的查詢只傳回記錄**TimeGenerated** hello hello 左邊囉 」 畫面顯示的時間範圍內。  

選取 hello 下拉式清單中，或修改 hello 滑桿，您可以變更 hello 時間篩選器。  hello 滑桿顯示橫條圖來顯示 hello 相對 hello 範圍內的每個時間區段的記錄數目。  此區段會因 hello 範圍。

hello 預設時間範圍是**1 天**。  變更此值太**7 天**，應該增加 hello 的總記錄數。

![日期時間範圍](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>篩選查詢結果的 hello
Hello 囉 」 畫面的左下的方是它可讓您篩選 toohello 查詢，而不需要直接修改它的 tooadd hello 篩選 窗格。  傳回的 hello 記錄的數個屬性會顯示其記錄的計數與與其前十個值。

如果您正在使用**事件**，選取 hello 核取方塊旁太**錯誤**下**EVENTLEVELNAME**。   如果您正在使用**Syslog**，選取 hello 核取方塊旁太**err**下**嚴重性層級**。  這樣會變更 hello 查詢的下列 toolimit hello hello tooone 結果 tooerror 事件。

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filter](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

新增屬性 toohello 篩選 窗格選取**新增 toofilters**從 hello 屬性功能表上的其中一個 hello 記錄。

![新增 toofilter 功能表](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

您可以設定相同選取篩選器的 hello**篩選**想 toofilter hello 屬性功能表中的 hello 值的記錄。  

您只需要 hello**篩選**內容的名稱以藍色的選項。  這些是可搜尋的欄位，已針對搜尋條件編列索引。  灰色的欄位是*任意可搜尋的文字*欄位只有 hello**顯示參考**選項。  此選項會傳回在任何屬性中具有該值的記錄。

![篩選功能表](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

您可以藉由選取 hello 群組上的單一屬性的 hello 結果**分組**hello 記錄功能表中的選項。  這會新增[摘要](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator)hello 結果顯示在圖表中的運算子 tooyour 查詢。  您可以群組在一個以上的屬性，但您直接需要 tooedit hello 查詢。  選取 hello 記錄功能表下一步 hello hello**電腦**屬性，並選取**Group by 'Computer'**。  

![依電腦分組](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>處理結果
hello 記錄搜尋入口網站有各種不同的功能使用 hello 查詢的結果。  您可以排序、 篩選和群組結果 tooanalyze hello 資料而不需修改 hello 實際查詢。  根據預設，不會排序查詢的結果。

tooview hello 表單資料的資料表提供其他選項用來篩選和排序，按一下**資料表**。  

![資料表檢視](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

按一下記錄 tooview hello 詳細資料，該記錄 hello 箭號。

![排序結果](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

按一下資料行標題，對欄位進行排序。

![排序結果](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

篩選 hello hello 按一下 hello 篩選按鈕，並提供篩選條件的資料行中的特定值的結果。

![篩選結果](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

藉由拖曳其資料行標題 toohello 結果的頂端 hello 分組的資料行上。  您可以在多個欄位上分組拖曳多個資料行 toohello 頂端。

![群組結果](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>使用效能資料
針對 Windows 和 Linux 代理程式的效能資料會儲存在 hello 記錄分析工作區中 hello**效能**資料表。  效能記錄看起來就像其他任何記錄，我們可以撰寫會傳回所有效能記錄的簡單查詢，就像使用事件一樣。

```
Perf
```

![效能資料](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

針對所有效能物件和計數器傳回數百萬筆記錄並不太實用。  您可以使用相同的方法，您使用上述 toofilter hello 資料或只是輸入 hello 下列查詢的 hello 直接在 hello 記錄搜尋 方塊。  這對於 Windows 和 Linux 電腦都只會傳回處理器使用率記錄。

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![處理器使用率](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

這會限制 hello 資料 tooa 特定計數器，但它仍不會將它放入的形式，尤其有用。  您可以在折線圖中顯示 hello 資料，但首先必須 toogroup 它的電腦和 TimeGenerated。  toogroup 上多個欄位，您需要 toomodify hello 查詢直接管理，因此修改 hello 查詢 toohello 下列。  這會使用 hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg())函式上 hello **CounterValue**每個小時內的屬性 toocalculate hello 平均值。

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![效能資料圖表](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

既然 hello 資料適當分組，您就可以顯示視覺圖表中加入 hello[呈現](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator)運算子。  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![折線圖](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>後續步驟

- 深入了解在 hello 記錄分析查詢語言[hello Analytics 入口網站使用者入門](https://go.microsoft.com/fwlink/?linkid=856079)。
- 逐步解說的教學課程使用 hello [Advanced Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)可讓您 toorun hello 相同的查詢及存取 hello 與 hello 記錄搜尋入口網站相同的資料。
