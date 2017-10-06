---
title: "在 Azure 記錄分析記錄搜尋 aaaFind 資料 |Microsoft 文件"
description: "Toocombine 可讓您記錄搜尋，並相互關聯您環境內多個來源的任何電腦資料。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>在 Log Analytics 中使用記錄搜尋以尋找資料

>[!NOTE]
> 本文說明的記錄搜尋記錄分析中使用 hello 目前的查詢語言。  如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，再過，您應該參閱[了解記錄搜尋中記錄分析 （新）](log-analytics-log-search-new.md)。


記錄分析的 hello 核心是 hello 記錄搜尋功能，可讓您 toocombine 和相互關聯您環境內多個來源的任何電腦資料。 解決方案也被 powered by 記錄搜尋 toobring 您度量特定問題領域的核心中。

在 hello 搜尋頁面上，您可以建立查詢，，然後在搜尋時，您可以篩選 hello 結果使用 facet 控制。 您也可以建立進階的查詢 tootransform、 篩選和報告結果。

常見的記錄搜尋查詢會出現在大部分解決方案頁面中。 在整個 hello OMS 主控台中，您可以按一下磚或切入 tooother 項目中 tooview hello 項目詳細資料，使用 記錄搜尋。

在本教學課程中，我們將逐步範例 toocover 所有 hello 基本概念當您使用記錄搜尋。

我們會以簡單、 實用的範例開頭，然後根據這些如此就可以了解實際的使用案例 toouse hello 語法 tooextract hello insights 您要如何從 hello 資料。

熟悉搜尋技術之後，您可以檢閱 hello[記錄分析記錄搜尋參考](log-analytics-search-reference.md)。

## <a name="use-basic-filters"></a>使用基本篩選器
hello 首先 tooknow 是該 hello 第一個部分的搜尋查詢，才能進行任何"|"直立線符號字元永遠是*篩選*。 您可以將其視為 TSQL 中的 WHERE 子句，以此判斷*什麼*資料 toopull 從 hello OMS 資料存放區的子集。 Hello 資料存放區中搜尋主要是有關指定您想 tooextract，因此很自然地查詢會以 hello WHERE 子句開頭的 hello 資料 hello 特性。

hello 最基本的篩選，您可以使用會*關鍵字*，例如 'error' 或 'timeout' 或電腦名稱。 這些簡單的查詢類型通常會傳回不同的圖形資料以 hello 相同結果集。 這是因為有不同的記錄分析*類型*hello 系統中的資料。

### <a name="tooconduct-a-simple-search"></a>tooconduct 簡單搜尋
1. 在 hello OMS 入口網站中，按一下 **記錄搜尋**。  
    ![搜尋圖格](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. 在 hello 查詢欄位中，輸入`error`，然後按一下**搜尋**。  
    ![搜尋錯誤](./media/log-analytics-log-searches/oms-search-error.png)  
    例如，hello 查詢`error`hello 在下圖中傳回 100,000 個**事件**記錄 （由記錄管理所收集）、 18 **ConfigurationAlert** （由組態所產生的記錄評估） 到 12 **ConfigurationChange**記錄 （由 hello 變更追蹤所擷取）。   
    ![搜尋結果](./media/log-analytics-log-searches/oms-search-results01.png)  

這些篩選器不一定是物件類型/類別。 *型別*只標記或屬性，或字串/名稱/類別，所附加 tooa 一段資料。 Hello 系統中的某些文件會標記為**Type: ConfigurationAlert**和某些會標記為**類型： 效能**，或**Type: Event**，依此類推。 每個搜尋結果、 文件、 記錄或項目會顯示所有 hello 未經處理的屬性及其值的每個這些片段的資料，而且您可以使用那些欄位名稱 toospecify hello 篩選中想 tooretrieve 僅 hello 記錄時其中 hello 欄位具有指定值。

「類型」其實只是所有記錄都有的欄位，與任何其他欄位並沒有不同。 這被建立根據 hello hello 類型欄位的值。 該記錄會有不同的圖形或形式。 順帶一提，**類型 = Perf**，或**類型 = 事件**也是您的效能資料或事件需要 toolearn tooquery hello 語法。

Hello 欄位名稱之後和 hello 值之前，您可以使用冒號 （:） 或等號 （=）。 **Type: Event**和**類型 = 事件**是相同的意義，您可以選擇 hello 您偏好的樣式。

因此，如果 hello 輸入 = 效能記錄具有名為 'CounterName' 的欄位，然後您可以撰寫類似如下`Type=Perf CounterName="% Processor Time"`。

這可以提供您唯一 hello 效能資料，其中 hello 效能計數器名稱是"%Processor Time"。

### <a name="toosearch-for-processor-time-performance-data"></a>toosearch 處理器時間效能資料
* 在 hello 搜尋查詢欄位中，輸入`Type=Perf CounterName="% Processor Time"`

您也可以更明確，並使用**InstanceName = _'total '** hello 查詢中，此為 Windows 效能計數器。 您也可以選取 facet 和另一個 **field:value**。 hello 篩選器會自動加入 tooyour 篩選 hello 查詢列中。 您可以在下列映像的 hello 看到。 它會示範其中 tooclick tooadd **InstanceName: '_Total'** toohello 查詢，而不需要輸入任何項目。

![搜尋 facet](./media/log-analytics-log-searches/oms-search-facet.png)

您的查詢現在已成為 `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

在此範例中，您不需要 toospecify**類型 = Perf** tooget toothis 結果。 因為 CounterName 和 InstanceName hello 欄位只存在於類型的記錄 = 效能，hello 查詢 hello 先前較長的相同的結果是不夠具體 tooreturn hello:

```
CounterName="% Processor Time" InstanceName="_Total"
```

這是因為 hello 查詢中的所有 hello 篩選條件會都評估為*AND*彼此。 實際上，hello 新增 toohello 準則的多個欄位，您取得小於，更特定且精緻的結果。

例如，hello 查詢`Type=Event EventLog="Windows PowerShell"`太相同`Type=Event AND EventLog="Windows PowerShell"`。 它會傳回登入以及從 hello Windows PowerShell 事件記錄檔收集到的所有事件。 如果您加入篩選多次藉由重複選取相同的 facet，然後 hello 問題會相當明確-它可能會干擾 hello 搜尋列中，但它仍會傳回 hello 相同的結果因為 hello 隱含 AND 運算子一律都會有 hello。

您可以藉由明確使用 NOT 運算子，輕鬆地反轉隱含 AND 運算子 hello。 例如：

`Type:Event NOT(EventLog:"Windows PowerShell")`或它的對等`Type=Event EventLog!="Windows PowerShell"`從所有其他不 hello 的 Windows PowerShell 記錄檔的記錄檔傳回所有事件。

或者，您可以使用其他布林運算子，例如 'OR'。 hello 下列查詢會傳回記錄的 hello EventLog 為應用程式或系統。

```
EventLog=Application OR EventLog=System
```

使用上述查詢的 hello，您會取得項目兩個記錄中 hello 相同結果集。

不過，如果您 hello 或藉由保留 hello 隱含 AND 以移除，然後 hello 下列查詢將不產生任何結果，因為沒有所屬 tooBOTH 記錄的事件記錄檔項目。 每個事件記錄檔項目會寫入 tooonly hello 兩個記錄檔的其中一個。

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>使用其他篩選器
hello 下列查詢會傳回所有已傳送資料的 hello 電腦 2 的事件記錄檔項目。

```
EventLog=Application OR EventLog=System
```

![搜尋結果](./media/log-analytics-log-searches/oms-search-results03.png)

選取其中一個 hello 欄位或篩選器會縮小 hello 查詢 tooa 特定電腦，並排除所有其他電腦。 hello 產生的查詢就會類似下列 hello。

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

這是對等 toohello 下列項目，因為 hello 隱含 and。

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

每個查詢都會進行評估 hello 下列明確的順序。 請注意 hello 括號。

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

如同 hello 事件記錄檔 欄位中，您可以擷取一組特定電腦的資料，藉由新增或者。 例如：

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

同樣地，下列查詢傳回這個 hello **%cpu 時間**hello 所選的兩部電腦。

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>欄位類型
在建立篩選器時，您應該了解 hello 差異，在使用不同類型的記錄搜尋所傳回的欄位。

**可搜尋的欄位**會在搜尋結果中以藍色顯示。  您可以使用可搜尋的欄位中搜尋條件特定 toohello 欄位 hello 如下：

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

**自然語言檢索搜尋旗標欄位**會在搜尋結果中以灰色顯示。  它們不能與搜尋條件特定 toohello 欄位，例如可搜尋的欄位。  它們只會搜尋所有的欄位，例如 hello 下列跨越執行查詢時。

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>布林運算子
在日期時間和數字欄位中，您可以使用「大於」、「小於」和「小於或等於」來搜尋值。 您可以使用簡單的運算子，例如 >，<>、 =、 < =、 ！ = hello 查詢搜尋列中。

您可以查詢特定一段時間的特定事件記錄。 例如，hello 過去 24 小時表示以 hello 下列助憶鍵運算式。

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>toosearch 使用布林運算子
* 在 hello 搜尋查詢欄位中，輸入`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![使用布林值來搜尋](./media/log-analytics-log-searches/oms-search-boolean.png)

雖然您可以控制 hello 時間間隔，以圖形方式，而且大多數時候您可能會想 toodo，有優點 tooincluding 直接在 hello 查詢時間篩選器。 比方說，這非常適合儀表板，您可以覆寫每個圖格，不論 hello hello 時間*全域*hello 儀表板頁面上的時間選取器。 如需詳細資訊，請參閱 [時間對儀表板很重要](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/)。

時藉由時間篩選，請記住，您會得到的結果 hello*交集*hello 的兩個時間週期： hello hello OMS 入口網站 (S1) 中指定的其中一個與 hello hello 查詢 (S2) 中指定的其中一個。

![交集](./media/log-analytics-log-searches/oms-search-intersection.png)

這表示，如果 hello 時間週期不交集，例如您在其中選擇 hello OMS 入口網站中**本週**hello 查詢中定義在**過去一週**沒有交集，您將不會收到任何結果。

用於 hello TimeGenerated 欄位的比較運算子也會在其他情況下很有用。 例如，用於數值欄位。

例如，假設組態評估警示有下列嚴重性值 hello:

* 0 = 資訊
* 1 = 警告
* 2 = 重大

您可以查詢警告和重大警示，並也排除的資訊以 hello 下列查詢：

```
Type=ConfigurationAlert  Severity>=1
```


您也可以使用範圍查詢。 這表示您可以提供的值序列中的 hello 開頭和結尾範圍。 例如，如果您想從 hello Operations Manager 事件記錄檔的事件，其中 hello EventID 是大於或等於 too2100 但小於 2199，然後 hello 下列查詢就會傳回它們。

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> 您必須使用 hello 範圍語法是 hello 冒號 （:） field: value 分隔符號和*不*hello 等號 （=）。 方括號括住 hello hello 範圍的下限和上限結尾，並使用兩個句點 （..） 隔開它們。
>
>

## <a name="manipulate-search-results"></a>操控搜尋結果
當您在搜尋資料時，您會想 toorefine 您的搜尋查詢，且有相當程度的控制權 hello 結果。 當擷取結果時，您可以套用命令 tootransform 它們。

記錄分析搜尋中的命令*必須*hello 直立線符號字元 (|) 之後。 篩選條件必須永遠是 hello 的查詢字串的第一個部分。 它會定義 hello 您正在使用的資料集，並再"那些結果 「 輸送到命令。 然後，您可以使用 hello 管道 tooadd 其他命令。 這是有點類似 toohello Windows PowerShell 管線。

一般情況下，hello 記錄分析搜尋語言會嘗試 toofollow PowerShell 樣式和指導方針 toomake it 類似 toohello IT 專業人員和 tooease hello 學習曲線。

命令具有動詞的名稱，因此您可以輕易地分辨它們執行的動作。  

### <a name="sort"></a>排序
hello sort 命令可讓您利用一或多個欄位排序 toodefine hello。 即使您不使用它，根據預設，會強制執行時間遞減順序。 hello 最新的結果一律會在搜尋結果的 hello 最上方。 這表示當您執行搜尋時，真正利用 `Type=Event EventID=1234` 執行的內容如下：

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

這是經驗的因為它是經驗的您已在記錄中熟悉的 hello 型別。 例如，在 hello Windows 事件檢視器。

您可以使用 toochange hello 方法結果的排序。 hello 下列範例顯示此運作方式。

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


hello 簡單上述範例顯示命令的運作方式--它們會變更 hello 圖形的 hello hello 篩選傳回的結果。

### <a name="limit-and-top"></a>Limit 和 top
另一個較少人知道的命令是 LIMIT。 Limit 為類似 PowerShell 的動詞。 限制為功能上與 toohello TOP 命令。 hello 下列查詢會傳回 hello 相同的結果。

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>使用 top toosearch
* 在 hello 搜尋查詢欄位中，輸入`Type=Event EventID=600 | Top 1`   
    ![搜尋 top](./media/log-analytics-log-searches/oms-search-top.png)

Hello 在圖中，有個 358 一千個記錄，附帶 EventID = 600。 hello 欄位、 facet 和 hello 一律保留傳回的 hello 結果的顯示資訊的篩選器*hello 篩選部分*hello 查詢，這是任何縱線字元之前的 hello 一部分。 hello**結果**窗格只會傳回最新的 1 hello 結果，因為 hello 範例命令會圖形化和轉換 hello 結果。

### <a name="select"></a>選取
hello SELECT 命令的行為類似 PowerShell 中的 Select-object。 它會傳回不包含所有原始屬性的篩選結果。 相反地，它會選取您所指定 hello 屬性。

#### <a name="toorun-a-search-using-hello-select-command"></a>搜尋使用 hello select 命令的 toorun
1. 在 搜尋 中，輸入 `Type=Event`，然後按一下搜尋。
2. 按一下**+ 顯示更多**其中一種 hello 結果 tooview hello 結果的所有 hello 屬性都有。
3. 選取部分會明確地與 hello 查詢變更太`Type=Event | Select Computer,EventID,RenderedDescription`。  
    ![搜尋 select](./media/log-analytics-log-searches/oms-search-select.png)

當您想 toocontrol 搜尋輸出，並選擇對探索，這通常不 hello 完整記錄的 hello 部分真的很重要的資料時，此命令會特別有用。 當不同類型的記錄有「部分」通用屬性，但不是「所有」屬性都共用時，這也非常有用。 ，您可以產生資料表，看起來更自然的輸出，或匯出 tooa CSV 檔案，然後必須在 Excel 中時正常運作。

## <a name="use-hello-measure-command"></a>使用 hello measure 命令
量值是其中一個 hello 記錄分析搜尋中最具彈性的命令。 它可讓您 tooapply 統計*函式*tooyour 資料和彙總的結果依指定的欄位分組。 Measure 支援多個統計函數。

### <a name="measure-count"></a>Measure count()
hello，第一次統計函數 toowork，且其中 hello 簡單 toounderstand hello *count （)*函式。

例如，來自任何搜尋查詢結果`Type=Event`，顯示篩選，又稱為 facet 上 hello 搜尋結果的左邊。 hello 篩選器會顯示執行 hello 搜尋中所指定 hello 結果欄位值的分佈。

![搜尋 measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

例如，在 hello 映像，您會看到 hello**電腦**欄位，它顯示 hello 結果中的 hello 幾乎 739 一千個事件，內有 68 唯一且不同的值為 hello**電腦**那些記錄中的欄位。 hello 磚只會顯示 hello hello 最常見 5 的值所撰寫的 hello 的前 5 個**電腦**欄位)，依據包含該欄位中的該特定値的文件的 hello 數目來排序。 Hello 映像中，您可以看到 – 之間幾乎 369 一千個事件 – 90 千位來自 hello OpsInsights04.contoso.com 電腦，83 千從 hello DB03.contoso.com 電腦，依此類推。

如果您想 toosee 所有值，因為 hello 磚只會顯示只有 hello 前 5 個？

這是什麼 hello 量值與 hello count （） 函式可以執行的命令。 此函數不會使用任何參數。 您只需要指定您要 toogroup 由 hello hello 欄位**電腦**欄位在此情況下：

`Type=Event | Measure count() by Computer`

![搜尋 measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

不過，**Computer** 只是每個資料片段「中」使用的欄位 - 不涉及關聯式資料庫，其他地方也都沒有別的 **Computer** 物件。 只要 hello 值*中*hello 可以描述哪個實體產生它們，以及其他一些特性和層面 hello 資料，因此 hello 詞彙*facet*。 不過，您也可以根據其他欄位分組。 因為 hello 的輸送到 hello measure 命令的幾乎 739 一千個事件的原始結果也具有名為欄位**EventID**，您可以套用 hello 依據該欄位的相同技巧 toogroup 並取得 by EventID 事件計數：

```
Type=Event | Measure count() by EventID
```

如果您不感興趣 hello 實際記錄計數包含特定值，但會改為您只想要的清單 hello 值本身，您可以加入*選取*命令結尾 hello 它，只要選取 hello 第一個資料行：

```
Type=Event | Measure count() by EventID | Select EventID
```

然後您可以取得更複雜和預先排序 hello 查詢中的 hello 結果或也您可以只按一下 hello hello 方格中的資料行。

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>使用 measure count toosearch
* 在 hello 搜尋查詢欄位中，輸入`Type=Event | Measure count() by EventID`
* 附加`| Select EventID`toohello hello 查詢的結尾。
* 最後，將附加`| Sort EventID asc`toohello hello 查詢的結尾。

有幾個要點 toonotice 與強調：

首先，您所看到的 hello 結果不再 hello 未經處理的結果。 相反地，它們是彙總的結果 – 基本上是結果的群組。 這不是問題，但您應該了解您正與非常不同的資料不同的圖形 hello 未經處理的圖形，便會建立 hello 彙總/統計函數結果的 hello 立即進行互動。

第二個，**測量計數**傳回目前只有 hello 前 100 個不同結果。 這項限制不適用 toohello 其他統計函數。 因此，您通常必須 toouse 更精確的篩選器第一個 toosearch 特定項目然後再套用 measure count （）。

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>透過 hello measure 命令使用 hello max 和 min 函數
有 **Measure Max()** 和 **Measure Min()** 在其中很有用的各種案例。 不過，由於每個函數彼此相反，我們將說明 Max ()，而您可以自己實驗 Min ()。

如果您查詢安全性事件，它們會有不同的**層級**屬性。 例如：

```
Type=SecurityEvent
```

![搜尋 measure count 開始](./media/log-analytics-log-searches/oms-search-measure-max01.png)

如果您要 tooview hello 最大值為 hello 安全性的所有事件指定共用 「 電腦，hello 群組依據 欄位中，您可以使用

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![搜尋 measure max 電腦](./media/log-analytics-log-searches/oms-search-measure-max02.png)

它會顯示有 hello 電腦**層級**記錄，其中大部分都有至少層級 8，許多具有 16 個層級。

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![搜尋 measure max 時間產生電腦](./media/log-analytics-log-searches/oms-search-measure-max03.png)

此函數適用於數字，但它也可以使用日期時間欄位。 它是最後一個元素的 hello 有用 toocheck 或任何資料片段的最新時間戳記編製索引的每台電腦。 例如： 當 hello 最新的安全性事件報告的每部機器？

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>使用 hello measure 命令使用 hello avg 函數
hello measure 搭配使用 avg （） 統計函數可讓您 toocalculate hello 平均值某些欄位，以及群組結果 hello 相同或其他欄位。 這適用於各種情況，例如效能資料。

我們將從效能等級開始介紹。 請注意，OMS 目前會收集 Windows 和 Linux 機器的效能計數器。

如 toosearch*所有*效能資料，hello 最基本的查詢如下：

```
Type=Perf
```

![搜尋 avg 開始](./media/log-analytics-log-searches/oms-search-avg01.png)

hello 您會注意到的第一件事是記錄分析會顯示三個檢視方塊： 清單中，它會顯示 hello 圖表; 後面顯示 hello 實際的記錄顯示效能計數器資料; 表格式檢視的資料表並顯示 hello 圖表效能計數器的度量。

Hello 在圖中，有兩組標示的欄位，以指出 hello 下列：

* hello 第一組會識別 Windows 效能計數器名稱、 物件名稱和執行個體名稱中 hello 查詢篩選器。 這些是您可能會最常用來做為 facet/篩選 hello 欄位
* **CounterValue**是 hello 的 hello 計數器的實際值。 在此範例中，hello 值是*75*。
* **TimeGenerated** 為 12:51，採用 24 小時制的時間格式。

以下是在圖形中的 hello 度量的檢視。

![搜尋 avg 開始](./media/log-analytics-log-searches/oms-search-avg02.png)

了解 hello 效能記錄圖形，並閱讀其他搜尋技術之後, 您可以使用 measure avg （) tooaggregate 這種類型的數值資料。

以下是簡單的範例：

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![搜尋 avg samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

在此範例中，您可以選取 hello CPU 時間總計效能計數器和電腦的平均。 如果您想 toonarrow 向您的結果 tooonly hello 6 小時，您可以使用 hello 時間篩選控制項，或指定查詢中，如下所示：

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>toosearch hello measure 命令使用 hello avg 函數
* 在 hello 搜尋查詢方塊中，輸入`Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`。

您可以「跨」  電腦彙總資料，並將其相互關聯。 例如，假設您有一組某種伺服器陣列，其中每個節點都是相等的 tooany 中主機的另一個它們剛剛做所有 hello 相同類型的工作和負載也應該大致平衡。 您可以取得所有在其中一個都將以下列查詢，並取得 hello 整個伺服器陣列的平均 hello 計數器。 您可以選擇以下列範例中的 hello hello 電腦啟動：

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

現在您擁有 hello 電腦，您也只想 tooselect 兩個關鍵效能指標 (Kpi): %cpu 使用量和 %可用磁碟空間。 因此，hello 查詢的該部分會變成：

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

現在您可以將電腦和計數器加入與下列範例中的 hello:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

因為您有非常明確的選取範圍，hello**測量 avg （）**命令可以傳回 hello 平均不是依電腦，而是跨 hello 伺服陣列中，只要群組依據 CounterName。 例如：

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

這可提供您數個環境 KPI 的實用精簡檢視。

![搜尋 avg grouping](./media/log-analytics-log-searches/oms-search-avg04.png)

您可以在儀表板中輕鬆使用 hello 搜尋查詢。 例如，您無法儲存 hello 搜尋查詢，並從名為它建立儀表板*Web 伺服陣列 Kpi*。 toolearn 進一步了解使用儀表板，請參閱[記錄分析中建立自訂的儀表板](log-analytics-dashboards.md)。

![搜尋 avg 儀表板](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>使用 hello measure 命令使用 hello sum 函數
hello sum 函式是 hello measure 命令的類似 tooother 函式。 您可以看到有關如何 toouse hello sum 函數，在範例[Microsoft Azure Operational Insights 中的 W3C IIS 記錄搜尋](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx)。

您可以搭配使用 Max() 和 Min() 與數字、日期時間和文字字串。 透過文字字串，它們會依字母順序排序，而您會取得第一個和最後一個。

不過，您無法搭配使用 Sum() 與數值欄位以外的任何項目。 這也適用於 tooAvg()。

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>透過 hello measure 命令使用 hello 百分位數函數
hello 百分位數函式是類似 tooAvg() 和 sum （），您只可以將它用於數值欄位。 您可以使用任何百分位數的數值欄位 1 too99 之間。 您也可以同時使用 **percentile** 和 **pct** 命令。 以下提供一些範例：  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>在命令時使用 hello
hello 命令的運作方式類似篩選條件，但它可以套用在 hello 管線 toofurther 篩選彙總在 hello 查詢開頭篩選過的相對於的 tooraw 結果由 measure-command-產生的結果。

例如：

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

您可以加入另一個縱線"|"字元和 hello 命令 tooonly 從何處取得的電腦的平均 CPU 高於 80%，與下列範例中的 hello:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

如果您已熟悉 Microsoft System Center Operations Manager，您可以將 hello 的管理組件詞彙中的命令。 如果 hello 範例是一項規則，hello 的 hello 查詢的第一個部分是 hello 資料來源和 hello，命令看起來會 hello 條件偵測。

您可以使用 hello 查詢當做一個磚中**我的儀表板**，作為監視器，toosee 時電腦 Cpu 是否過度使用。 toolearn 深入了解儀表板，請參閱[記錄分析中建立自訂的儀表板](log-analytics-dashboards.md)。 您也可以建立和使用儀表板使用 hello 行動裝置應用程式。 如需詳細資訊，請參閱 [OMS 行動應用程式 ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)。 在 hello 底部兩個磚的 hello 下列映像，您可以看到 hello 監視器顯示清單，表示為數字。 基本上，您一定想 hello 數字 toobe 零，並且 hello 清單 toobe 空白。 否則，它會指出警示條件。 如有需要您可以使用它 tootake 看看那些電腦不足的壓力。

![行動儀表板](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>使用運算子中的 hello
hello *IN*運算子，連同*NOT IN*可讓您 toouse 子搜尋，也就是包含另一個搜尋作為引數的搜尋。 它們會以大括號 {} 包含在另一個「主要」或「外部」搜尋內。 hello 子搜尋的結果，通常是不同結果的清單將做為引數用於其主要搜尋中。

您可以使用子搜尋 toomatch 子集您無法直接在搜尋運算式中，但可從搜尋產生描述您的資料。 例如，如果您想要使用的所有事件的一個搜尋 toofind*缺少安全性更新的電腦*，則您需要 toodesign 子搜尋，先識別*缺少安全性更新的電腦*再尋找事件隸屬 toothose 主機。

因此，您無法表示*電腦目前遺失必要的安全性更新*以 hello 下列查詢：

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Hello 清單之後，您可以使用 hello 搜尋作為內部搜尋 toofeed hello 清單中的電腦到外部 （主要） 搜尋會尋找這些電腦的事件。 您以大括號括住 hello 內部搜尋，再饋送其結果作為篩選/欄位使用 hello IN 運算子的 hello 外部搜尋中的可能值。 hello 查詢會類似如下：

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in02-revised.png)

也請注意 hello hello 內部搜尋中使用，因為篩選 hello 系統更新評估所需的時間的所有電腦的快照集每隔 24 小時。 您可以藉由只搜尋一天，更輕鬆且精確地進行 hello 內部查詢。 hello 外部搜尋則是透過 hello 時間選取範圍在 hello 使用者介面中，擷取事件 hello 過去 7 天。 如需時間運算子的詳細資訊，請參閱 [布林運算子](#boolean-operators) 。

因為您實際上只使用 hello hello 做為篩選值的內部搜尋的結果 hello 外部，您仍然可以套用 hello 外部搜尋中的命令。 例如，您仍然可以上述事件的另一個 measure 命令的群組 hello:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![IN 搜尋範例](./media/log-analytics-log-searches/oms-search-in03-revised.png)

通常，您希望您的內部查詢 tooexecute 快速因為記錄分析服務端逾時，它也 tooreturn 更少結果。 如果 hello 內部查詢傳回更多結果，hello 結果清單會遭到截斷，而可能導致 hello 外部搜尋 tooreturn 不正確的結果。

另一個規則是該 hello 內部搜尋目前必須 tooprovide*彙總*結果。 換句話說，它必須包含「measure」  命令；您目前無法將未經處理的結果送到外部搜尋。

此外，可以有只有一個 IN 運算子，而且它必須是 hello hello 查詢中的最後一個篩選條件。 多個 IN 運算子不可以是或者，這基本上可防止執行多個子搜尋： hello 重要點是該只有一個子/內部搜尋可能會有每個外部搜尋。

即使有這些限制，IN 可讓許多種類的相互關聯的搜尋和可讓您 toodefine 類似 toogroups，例如電腦、 使用者或檔案-不論 hello 欄位資料中的包含。 以下還有其他範例：

**已停用自動更新設定的電腦中遺失的所有更新**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**執行 SQL Server (即 SQL 評估執行所在) 的電腦中的所有錯誤事件**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**屬於網域控制站 (即 AD 評估執行所在) 的電腦中的所有安全性事件**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**哪些其他帳戶已登入 toohello 其中與 baconland\jochan 所登入相同的電腦嗎？**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>使用 hello distinct 命令
如 hello 名稱所示，此命令會提供欄位的相異值清單。 它出乎意料地簡單，但卻相當實用。 hello 達成相同使用 measure count （） 命令也，如下所示。

```
Type=Event | Measure count() by Computer
```

![DISTINCT 搜尋命令範例](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

不過，如果您感興趣的只是只有相異值，且不 hello 計數為具有之值的文件的清單，然後 DISTINCT 可以提供較為簡潔且更容易 tooread 輸出，以及較短的語法，如下所示。

```
Type=Event | Distinct Computer
```
![DISTINCT 搜尋命令範例](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>透過 hello measure 命令使用 hello countdistinct 函數
hello countdistinct 函數會計算每個群組內的相異值的 hello 數目。 例如，它可能是使用 toocount hello 唯一回報的電腦數目每一種類型：

```
* | measure countdistinct(Computer) by Type
```

![OMS-countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>使用 hello measure 間隔命令
透過接近即時的效能資料收集，您可以在 Log Analytics 中收集和視覺化任何效能計數器。 只要輸入 hello 查詢**類型： 效能**會傳回數千個度量 hello 計數器和記錄分析環境中的伺服器數目為基礎的圖形。 視度量彙總，您可以查看 hello 高的層級，以及深入探討更精細的資料，因為您需要在環境中整體度量。

我們假設您想 tooknow 何謂 hello 平均 CPU 跨所有電腦。 查看 hello 的每部電腦的平均 CPU 不可能很有幫助因為結果取得平滑化。toolook 到更多詳細資料，您可以彙總結果中較小的時間視窗區塊，並尋找時間序列跨不同的維度。 例如，您可以執行 hello 每小時的平均 CPU 使用量的所有電腦，如下所示：

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![測量平均間隔](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

根據預設，這些結果會顯示在多數列的互動式折線圖中。  這個圖表支援數列切換 (透過 y 軸重新調整)、縮放和暫留。  hello 資料表顯示選項是仍然可供檢視 hello 未經處理資料，如有必要的。

您也可以根據其他欄位分組。 在此範例中，我要在一部特定電腦的所有 hello %計數器，我想 tooknow 何謂 hello 的每個計數器每小時 70 百分位數：

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
一件事 toonote 是，這些查詢不會限制的 tooperformance 計數器。 您可以套用它們 tooany 度量。 在此範例中，我要查看 W3C IIS 記錄檔。 我想 tooknow 何謂 hello 處理每個要求的 5 分鐘間隔內所需的最大時間：

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>在單一查詢中使用多個彙總
您可以在 measure 命令中指定多個彙總子句。  每個子句皆可獨立給予別名。  如果未指定別名 hello 產生欄位名稱就是所用的 hello 彙總函式 (也就是 「 avg(CounterValue)"avg(CounterValue)) 的。

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS-multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

以下是另一個範例︰

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>後續步驟
如需關於記錄檔搜尋的其他資訊，請參閱：

* 使用[自訂欄位中記錄分析](log-analytics-custom-fields.md)tooextend 記錄搜尋。
* 檢閱 hello[記錄分析記錄搜尋參考](log-analytics-search-reference.md)tooview hello 的所有搜尋欄位和 facet 用於記錄分析。
