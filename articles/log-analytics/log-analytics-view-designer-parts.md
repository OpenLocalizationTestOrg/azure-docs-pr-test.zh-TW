---
title: "在 OMS 記錄分析的檢視表設計工具的 aaaPart 參考 |Microsoft 文件"
description: "檢視表設計工具中記錄分析可讓您自訂 toocreate hello OMS 主控台中，包含不同的視覺效果的 hello OMS 儲存機制中資料的檢視。 這篇文章會提供每個自訂檢視中的 hello 視覺效果部分可用 toouse hello 設定的參考。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Log Analytics 檢視設計工具視覺效果部分參考
hello 檢視表設計工具中記錄分析可讓您 toocreate 自訂檢視 hello OMS 主控台中包含不同的視覺效果的資料從 hello OMS 儲存機制。 這篇文章會提供每個自訂檢視中的 hello 視覺效果部分可用 toouse hello 設定的參考。

其他與檢視設計工具相關的文章︰

* [檢視設計工具](log-analytics-view-designer.md)-hello 檢視表設計工具和程序來建立和編輯自訂檢視的概觀。
* [磚參考](log-analytics-view-designer-tiles.md)-參考的每一個 hello hello 設定磚可用 toouse 中自訂檢視。

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則必須寫入所有檢視中的查詢中 hello[新的查詢語言](https://go.microsoft.com/fwlink/?linkid=856078)。  Hello 工作區已升級之前建立的任何檢視會 automtically 轉換。

hello 下表描述 hello 磚 hello 檢視表設計工具中可用的不同型別。  hello 以下章節將詳細資料和其屬性中的每個圖格類型。

| 檢視類型 | 說明 |
|:--- |:--- |
| [查詢清單](#list-of-queries-part) |顯示記錄檔搜尋查詢清單。  hello 使用者可以按一下每個查詢 toodisplay 其結果。 |
| [數字與清單](#number-amp-list-part) |標頭中有一個數字可顯示記錄檔搜尋查詢中的記錄計數。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。 |
| [兩個數字與清單](#two-numbers-amp-list-part) |標頭中有兩個數字可顯示不同記錄檔搜尋查詢中的記錄計數。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。 |
| [環圈與清單](#donut-amp-list-part) |標頭會顯示從記錄檔查詢中的值資料行摘錄而來的單一數字。  hello 環圈圖會以圖形方式顯示 hello 前三筆記錄的結果。 |
| [兩個時間軸與清單](#two-timelines-amp-list-part) |標頭會顯示 hello 導致一段時間為直條圖顯示單一數字的圖說文字具有兩個記錄檔查詢的彙總從記錄檔查詢中的值資料行。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。 |
| [資訊](#information-part) |標頭會顯示靜態文字和選擇性連結。  清單會顯示一或多個包含靜態文字和標題的項目。 |
| [折線圖、圖說文字與清單](#line-chart-callout-amp-list-part) |標頭會顯示一個折線圖 (其中包含一段時間內記錄檔查詢中的多個系列)，以及包含摘錄值的圖說文字。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。 |
| [折線圖與清單](#line-chart-amp-list-part) |標頭會顯示一個折線圖，其中包含一段時間內記錄檔查詢中的多個系列。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。 |
| [折線圖部分堆疊](#stack-of-line-charts-part) |顯示三個獨立的折線圖，其中包含一段時間內記錄檔查詢中的多個系列。 |

## <a name="list-of-queries-part"></a>查詢清單部分
顯示記錄檔搜尋查詢清單。  hello 使用者可以按一下每個查詢 toodisplay 其結果。  根據預設，hello 檢視中會包含單一查詢，您可以按一下**+ 查詢**tooadd 其他查詢。

![查詢清單檢視](media/log-analytics-view-designer/view-list-queries.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| Title |在 hello hello 檢視頂端的文字 toodisplay。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 預先選取的篩選器 |以逗號分隔清單中的 hello 左方的篩選] 窗格中的屬性 tooinclude hello 使用者選取的查詢時。 |
| 轉譯模式 |選取 hello 查詢時顯示的初始檢視。  hello 使用者可以選取任何可用的檢視，開啟 hello 查詢之後。 |
| **查詢** | |
| 搜尋查詢 |查詢 toorun。 |
| 易記名稱 |Hello 查詢 toodisplay toohello 使用者的描述性名稱。 |

## <a name="number--list-part"></a>數字與清單部分
標頭中有一個數字可顯示記錄檔搜尋查詢中的記錄計數。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。

![查詢清單檢視](media/log-analytics-view-designer/view-number-list.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| 群組標題 |在 hello hello 檢視頂端的文字 toodisplay。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 圖示 |映像檔案 toodisplay 下一個 toohello 結果 hello 標頭中。 |
| 使用圖示 |選取 toohave hello 圖示顯示。 |
| **標題** | |
| 圖例 |文字 toodisplay 頂端 hello hello 標頭。 |
| 查詢 |查詢 toorun hello 標頭。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| **清單** | |
| 查詢 |查詢 toorun hello 清單。  針對 hello hello 結果中的前十個資料錄將會顯示 hello 前兩個屬性。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。  橫條圖會自動建立根據 hello 相對 hello 數值資料行值。<br><br>使用 hello 查詢 toosort hello 清單中的 hello 記錄中的 hello Sort 命令。  hello 使用者可以按一下 [查看所有 toorun hello 查詢，並傳回所有記錄。 |
| 隱藏圖形 |選取 toodisable hello 圖形 toohello 右邊的 hello 數值資料行。 |
| 啟用走勢圖 |選取 toodisplay 走勢圖，而不是水平列。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 色彩 |Hello 橫條或走勢圖的色彩。 |
| 名稱和值分隔符號 |如果您想 tooparse hello 文字屬性到多個值的單一字元分隔符號。  請參閱[一般設定](#name-value-separator)以瞭解詳細資料。 |
| 瀏覽查詢 |Hello 使用者 hello 清單中選取項目時，請查詢 toorun。  請參閱[一般設定](#navigation-query)以瞭解詳細資料。 |
| **清單** |**> 資料行標題** |
| 名稱 |文字 toodisplay 頂端 hello hello hello 清單的第一個資料行。 |
| 值 |文字 toodisplay 頂端 hello hello hello 清單的第二個資料行。 |
| **清單** |**> 臨界值** |
| 啟用臨界值 |選取 tooenable 臨界值。  請參閱[一般設定](#thresholds)以瞭解詳細資料。 |

## <a name="two-numbers--list-part"></a>兩個數字與清單部分
標頭中有兩個數字可顯示不同記錄檔搜尋查詢中的記錄計數。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。

![兩個數字與清單檢視](media/log-analytics-view-designer/view-two-numbers-list.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| 群組標題 |在 hello hello 檢視頂端的文字 toodisplay。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 圖示 |映像檔案 toodisplay 下一個 toohello 結果 hello 標頭中。 |
| 使用圖示 |選取 toohave hello 圖示顯示。 |
| **標題** | |
| 圖例 |文字 toodisplay 頂端 hello hello 標頭。 |
| 查詢 |查詢 toorun hello 標頭。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| **清單** | |
| 查詢 |查詢 toorun hello 清單。  針對 hello hello 結果中的前十個資料錄將會顯示 hello 前兩個屬性。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。  橫條圖會自動建立根據 hello 相對 hello 數值資料行值。<br><br>使用 hello 查詢 toosort hello 清單中的 hello 記錄中的 hello Sort 命令。  hello 使用者可以按一下 [查看所有 toorun hello 查詢，並傳回所有記錄。 |
| 隱藏圖形 |選取 toodisable hello 圖形 toohello 右邊的 hello 數值資料行。 |
| 啟用走勢圖 |選取 toodisplay 走勢圖，而不是水平列。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 色彩 |Hello 橫條或走勢圖的色彩。 |
| 作業 |Hello 走勢圖的作業 tooperform。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 名稱和值分隔符號 |如果您想 tooparse hello 文字屬性到多個值的單一字元分隔符號。  請參閱[一般設定](#name-value-separator)以瞭解詳細資料。 |
| 瀏覽查詢 |Hello 使用者 hello 清單中選取項目時，請查詢 toorun。  請參閱[一般設定](#navigation-query)以瞭解詳細資料。 |
| **清單** |**> 資料行標題** |
| 名稱 |文字 toodisplay 頂端 hello hello hello 清單的第一個資料行。 |
| 值 |文字 toodisplay 頂端 hello hello hello 清單的第二個資料行。 |
| **清單** |**> 臨界值** |
| 啟用臨界值 |選取 tooenable 臨界值。  請參閱[一般設定](#thresholds)以瞭解詳細資料。 |

## <a name="donut--list-part"></a>環圈與清單部分
標頭會顯示從記錄檔查詢中的值資料行摘錄而來的單一數字。  hello 環圈圖會以圖形方式顯示 hello 前三筆記錄的結果。

![環圈與清單檢視](media/log-analytics-view-designer/view-donut-list.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| 群組標題 |頂端的 hello hello 文字 toodisplay 磚。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 圖示 |映像檔案 toodisplay 下一個 toohello 結果 hello 標頭中。 |
| 使用圖示 |選取 toohave hello 圖示顯示。 |
| **標頭** | |
| Title |文字 toodisplay 頂端 hello hello 標頭。 |
| 副標題 |文字 toodisplay hello hello 標頭中的 hello 頂端的標題底下。 |
| **環圈** | |
| 查詢 |Hello 甜甜圈的查詢 toorun。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。 |
| **環圈** |**> 中心** |
| 文字 |文字 toodisplay 下 hello hello 環圈圖內的值。 |
| 作業 |hello 作業 tooperform hello 值屬性 toosummarize tooa 單一值。<br><br>-總和： 新增所有記錄的 hello 的值。<br>Hello 傳回的記錄中的 hello 值的百分比： 百分比**center 作業中使用的值會造成**toohello hello 查詢中的記錄總數。 |
| 中心作業使用的結果值 |（選擇性) 按一下 hello 加號 tooadd 一或多個值。  hello hello 查詢結果會限制的 toorecords 與您指定的 hello 屬性值。  如果不加入任何值，則所有記錄都包含 hello 查詢中。 |
| **其他選項** |**> 色彩** |
| 色彩 1<br>色彩 2<br>色彩 3 |選取 hello hello 每個 hello 環圈圖中顯示的 hello 值的色彩。 |
| **其他選項** |**> 進階色彩對應** |
| 欄位值 |型別 hello 名稱欄位 toodisplay 它做為不同的色彩，如果它包含在 hello 環圈圖。 |
| 色彩 |選取 hello hello 唯一欄位的色彩。 |
| **清單** | |
| 查詢 |查詢 toorun hello 清單。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| 隱藏圖形 |選取 toodisable hello 圖形 toohello 右邊的 hello 數值資料行。 |
| 啟用走勢圖 |選取 toodisplay 走勢圖，而不是水平列。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 色彩 |Hello 橫條或走勢圖的色彩。 |
| 作業 |Hello 走勢圖的作業 tooperform。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 名稱和值分隔符號 |如果您想 tooparse hello 文字屬性到多個值的單一字元分隔符號。  請參閱[一般設定](#name-value-separator)以瞭解詳細資料。 |
| 瀏覽查詢 |Hello 使用者 hello 清單中選取項目時，請查詢 toorun。  請參閱[一般設定](#navigation-query)以瞭解詳細資料。 |
| **清單** |**> 資料行標題** |
| 名稱 |文字 toodisplay 頂端 hello hello hello 清單的第一個資料行。 |
| 值 |文字 toodisplay 頂端 hello hello hello 清單的第二個資料行。 |
| **清單** |**> 臨界值** |
| 啟用臨界值 |選取 tooenable 臨界值。  請參閱[一般設定](#thresholds)以瞭解詳細資料。 |

## <a name="two-timelines--list-part"></a>兩個時間軸與清單部分
標頭會顯示 hello 導致一段時間為直條圖顯示單一數字的圖說文字具有兩個記錄檔查詢的彙總從記錄檔查詢中的值資料行。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。

![兩個時間軸與清單檢視](media/log-analytics-view-designer/view-two-timelines-list.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| 群組標題 |頂端的 hello hello 文字 toodisplay 磚。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 圖示 |映像檔案 toodisplay 下一個 toohello 結果 hello 標頭中。 |
| 使用圖示 |選取 toohave hello 圖示顯示。 |
| **第一個圖表<br>第二個圖表** | |
| 圖例 |在 hello 第一個數列的 hello 圖說文字的文字 toodisplay。 |
| 色彩 |色彩 toouse hello hello 數列中的資料行。 |
| 查詢 |查詢 toorun hello 第一個數列。  hello hello 的計數記錄每個時間間隔內會呈現 hello 圖表資料行。 |
| 作業 |hello 作業 tooperform hello 值屬性 toosummarize tooa 單一值的 hello 圖說文字。<br><br>所有記錄中的 hello 值的總和： 總和。<br>所有記錄中的 hello 值的平均： 平均。<br>-最後一個範例： Hello hello 圖表中包含的最後一個間隔中的值。<br>-第一個範例： Hello hello 圖表中包含的第一個間隔值。<br>計數： Hello 查詢所傳回的所有記錄的計數。 |
| **清單** | |
| 查詢 |查詢 toorun hello 清單。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| 隱藏圖形 |選取 toodisable hello 圖形 toohello 右邊的 hello 數值資料行。 |
| 啟用走勢圖 |選取 toodisplay 走勢圖，而不是水平列。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 色彩 |Hello 橫條或走勢圖的色彩。 |
| 作業 |Hello 走勢圖的作業 tooperform。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 瀏覽查詢 |Hello 使用者 hello 清單中選取項目時，請查詢 toorun。  請參閱[一般設定](#navigation-query)以瞭解詳細資料。 |
| **清單** |**> 資料行標題** |
| 名稱 |文字 toodisplay 頂端 hello hello hello 清單的第一個資料行。 |
| 值 |文字 toodisplay 頂端 hello hello hello 清單的第二個資料行。 |
| **清單** |**> 臨界值** |
| 啟用臨界值 |選取 tooenable 臨界值。  請參閱[一般設定](#thresholds)以瞭解詳細資料。 |

## <a name="information-part"></a>資訊部分
標頭會顯示靜態文字和選擇性連結。  清單會顯示一或多個包含靜態文字和標題的項目。

![資訊檢視](media/log-analytics-view-designer/view-information.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| 群組標題 |頂端的 hello hello 文字 toodisplay 磚。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 色彩 |Hello 標頭的背景色彩。 |
| **標頭** | |
| 映像 |映像檔案 toodisplay hello 標頭中。 |
| 標籤 |文字 toodisplay hello 標頭中。 |
| **標頭** |**> 連結** |
| 標籤 |連結文字。 |
| Url |連結的 Url。 |
| **資訊項目** | |
| Title |每個項目的標題的文字 toodisplay。 |
| 內容 |每個項目的文字 toodisplay。 |

## <a name="line-chart-callout--list-part"></a>折線圖、圖說文字與清單部分
標頭會顯示一個折線圖 (其中包含一段時間內記錄檔查詢中的多個系列)，以及包含摘錄值的圖說文字。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。

![折線圖、圖說文字與清單檢視](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| 群組標題 |頂端的 hello hello 文字 toodisplay 磚。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 圖示 |映像檔案 toodisplay 下一個 toohello 結果 hello 標頭中。 |
| 使用圖示 |選取 toohave hello 圖示顯示。 |
| **標頭** | |
| Title |文字 toodisplay 頂端 hello hello 標頭。 |
| 副標題 |文字 toodisplay hello hello 標頭中的 hello 頂端的標題底下。 |
| **折線圖** | |
| 查詢 |查詢 toorun hello 折線圖。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。  這通常是使用 hello 的查詢**量值**關鍵字 toosummarize 結果。  如果 hello 查詢使用 hello**間隔**關鍵字則 hello hello 圖表的 x 軸將會使用此時間間隔。  如果 hello 查詢不包含 hello**間隔**關鍵字，則每小時間隔用於 hello x 軸。 |
| **折線圖** |**> 圖說文字** |
| 圖說文字標題 |文字 toodisplay 高於 hello 圖說文字值。 |
| 系列名稱 |Hello 數列 toouse hello 圖說文字值的屬性值。  如果未不提供任何數列，則會使用從 hello 查詢的所有記錄。 |
| 作業 |hello 作業 tooperform hello 值屬性 toosummarize tooa 單一值的 hello 圖說文字。<br><br>所有記錄中的 hello 值的平均： 平均。<br>Hello 查詢所傳回的所有記錄的計數計數。<br>-最後一個範例： Hello hello 圖表中包含的最後一個間隔中的值。<br>的從包含 hello 圖表中的 hello 間隔最大值： 最大值。<br>的從包含 hello 圖表中的 hello 間隔最小值： 最小值。<br>所有記錄中的 hello 值的總和： 總和。 |
| **折線圖** |**> Y 軸** |
| 使用對數刻度 |選取 toouse hello y 軸的對數標尺。 |
| Units |請指定 hello 單元 hello hello 查詢所傳回的值。  這項資訊是使用的 toodisplay 標籤 hello 圖表指出 hello 實值型別上也可以將 hello 值轉換。  hello 單位類型指定 hello 單元 hello 分類，並定義可用的 hello 目前的單位類型值。  如果您選取的值中數值的轉換 toothen hello 值會轉換從 hello 目前單位類型 toohello Convert tootype。 |
| 自訂標籤 |Hello Y 軸 [下一步 toohello hello 單位型別的標籤的文字 toodisplay。  如果沒有標籤指定時，會顯示 hello 單位類型。 |
| **清單** | |
| 查詢 |查詢 toorun hello 清單。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| 隱藏圖形 |選取 toodisable hello 圖形 toohello 右邊的 hello 數值資料行。 |
| 啟用走勢圖 |選取 toodisplay 走勢圖，而不是水平列。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 色彩 |Hello 橫條或走勢圖的色彩。 |
| 作業 |Hello 走勢圖的作業 tooperform。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 名稱和值分隔符號 |如果您想 tooparse hello 文字屬性到多個值的單一字元分隔符號。  請參閱[一般設定](#name-value-separator)以瞭解詳細資料。 |
| 瀏覽查詢 |Hello 使用者 hello 清單中選取項目時，請查詢 toorun。  請參閱[一般設定](#navigation-query)以瞭解詳細資料。 |
| **清單** |**> 資料行標題** |
| 名稱 |文字 toodisplay 頂端 hello hello hello 清單的第一個資料行。 |
| 值 |文字 toodisplay 頂端 hello hello hello 清單的第二個資料行。 |
| **清單** |**> 臨界值** |
| 啟用臨界值 |選取 tooenable 臨界值。  請參閱[一般設定](#thresholds)以瞭解詳細資料。 |

## <a name="line-chart--list-part"></a>折線圖與清單部分
標頭會顯示一個折線圖，其中包含一段時間內記錄檔查詢中的多個系列。  清單會顯示 hello 前十個查詢的結果，與圖形表示 hello 相對值的數值資料行或一段時間的變更。

![折線圖與清單檢視](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| 群組標題 |頂端的 hello hello 文字 toodisplay 磚。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 圖示 |映像檔案 toodisplay 下一個 toohello 結果 hello 標頭中。 |
| 使用圖示 |選取 toohave hello 圖示顯示。 |
| **標頭** | |
| Title |文字 toodisplay 頂端 hello hello 標頭。 |
| 副標題 |文字 toodisplay hello hello 標頭中的 hello 頂端的標題底下。 |
| **折線圖** | |
| 查詢 |查詢 toorun hello 折線圖。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。  這通常是使用 hello 的查詢**量值**關鍵字 toosummarize 結果。  如果 hello 查詢使用 hello**間隔**關鍵字則 hello hello 圖表的 x 軸將會使用此時間間隔。  如果 hello 查詢不包含 hello**間隔**關鍵字，則每小時間隔用於 hello x 軸。 |
| **折線圖** |**> Y 軸** |
| 使用對數刻度 |選取 toouse hello y 軸的對數標尺。 |
| Units |請指定 hello 單元 hello hello 查詢所傳回的值。  這項資訊是使用的 toodisplay 標籤 hello 圖表指出 hello 實值型別上也可以將 hello 值轉換。  hello 單位類型指定 hello 單元 hello 分類，並定義可用的 hello 目前的單位類型值。  如果您選取的值中數值的轉換 toothen hello 值會轉換從 hello 目前單位類型 toohello Convert tootype。 |
| 自訂標籤 |Hello Y 軸 [下一步 toohello hello 單位型別的標籤的文字 toodisplay。  如果沒有標籤指定時，會顯示 hello 單位類型。 |
| **清單** | |
| 查詢 |查詢 toorun hello 清單。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| 隱藏圖形 |選取 toodisable hello 圖形 toohello 右邊的 hello 數值資料行。 |
| 啟用走勢圖 |選取 toodisplay 走勢圖，而不是水平列。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 色彩 |Hello 橫條或走勢圖的色彩。 |
| 作業 |Hello 走勢圖的作業 tooperform。  請參閱[一般設定](#sparklines)以瞭解詳細資料。 |
| 名稱和值分隔符號 |如果您想 tooparse hello 文字屬性到多個值的單一字元分隔符號。  請參閱[一般設定](#name-value-separator)以瞭解詳細資料。 |
| 瀏覽查詢 |Hello 使用者 hello 清單中選取項目時，請查詢 toorun。  請參閱[一般設定](#navigation-query)以瞭解詳細資料。 |
| **清單** |**> 資料行標題** |
| 名稱 |文字 toodisplay 頂端 hello hello hello 清單的第一個資料行。 |
| 值 |文字 toodisplay 頂端 hello hello hello 清單的第二個資料行。 |
| **清單** |**> 臨界值** |
| 啟用臨界值 |選取 tooenable 臨界值。  請參閱[一般設定](#thresholds)以瞭解詳細資料。 |

## <a name="stack-of-line-charts-part"></a>折線圖部分堆疊
顯示三個獨立的折線圖，其中包含一段時間內記錄檔查詢中的多個系列。

![折線圖堆疊](media/log-analytics-view-designer/view-stack-line-charts.png)

| 設定 | 說明 |
|:--- |:--- |
| **一般** | |
| 群組標題 |頂端的 hello hello 文字 toodisplay 磚。 |
| 新增群組 |在開始 hello 目前檢視的 hello 檢視中選取 toocreate 新的群組。 |
| 圖示 |映像檔案 toodisplay 下一個 toohello 結果 hello 標頭中。 |
| **圖表 1<br>圖表 2<br>圖表 3** |**> 標頭** |
| Title |文字 toodisplay 在 hello hello 圖表的頂端。 |
| 副標題 |文字 toodisplay hello 在 hello hello 圖表頂端的標題底下。 |
| **圖表 1<br>圖表 2<br>圖表 3** |**折線圖** |
| 查詢 |查詢 toorun hello 折線圖。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。  這通常是使用 hello 的查詢**量值**關鍵字 toosummarize 結果。  如果 hello 查詢使用 hello**間隔**關鍵字則 hello hello 圖表的 x 軸將會使用此時間間隔。  如果 hello 查詢不包含 hello**間隔**關鍵字，則每小時間隔用於 hello x 軸。 |
| **圖表** |**> Y 軸** |
| 使用對數刻度 |選取 toouse hello y 軸的對數標尺。 |
| Units |請指定 hello 單元 hello hello 查詢所傳回的值。  這項資訊是使用的 toodisplay 標籤 hello 圖表指出 hello 實值型別上也可以將 hello 值轉換。  hello 單位類型指定 hello 單元 hello 分類，並定義可用的 hello 目前的單位類型值。  如果您選取的值中數值的轉換 toothen hello 值會轉換從 hello 目前單位類型 toohello Convert tootype。 |
| 自訂標籤 |Hello Y 軸 [下一步 toohello hello 單位型別的標籤的文字 toodisplay。  如果沒有標籤指定時，會顯示 hello 單位類型。 |

## <a name="common-settings"></a>一般設定
hello 下列各節描述設定通用 tooseveral 視覺效果部分。

### <a name="name-value-separator">名稱和值分隔符號</a>
如果您想 tooparse hello 文字屬性，從清單中查詢至多個值的單一字元分隔符號。  如果您指定分隔符號，您就可以提供名稱，每個欄位分隔來 hello 相同 hello 名稱] 方塊中的分隔符號。

例如，考慮名為 *Location* 的屬性，其包含 *Redmond-Building 41* 和 *Bellevue-Building12* 等值。  您可以指定 – hello 名稱和值的分隔符號和*縣 （市） 建置*hello 名稱。  這會將每個值剖析成兩個名為 City 和 Building 的屬性。

### <a name="navigation-query">瀏覽查詢</a>
Hello 使用者 hello 清單中選取項目時，請查詢 toorun。  使用*{選取的項目}* tooinclude hello 語法 hello 使用者選取的項目。

例如，如果 hello 查詢具有名的資料行*電腦*hello 巡覽查詢，且*{選取的項目}*，例如查詢*電腦 ="MyComputer"*都會執行時hello 使用者選取的電腦。  如果 hello 瀏覽查詢*類型 = Event {選取的項目}*然後 hello 查詢*類型 = 事件電腦 ="MyComputer"*會執行。

### <a name="sparklines">走勢圖</a>
走勢圖是小型的折線圖，說明 hello 值的清單項目一段時間。  視覺效果組件清單中，您可以選取是否 toodisplay 水平橫條，指出 hello 相對的數值資料行的值或其值指出經過一段時間的走勢圖。

hello 下表描述走勢圖的 hello 的設定。

| 設定 | 說明 |
|:--- |:--- |
| 啟用走勢圖 |選取 toodisplay 走勢圖，而不是水平列。 |
| 作業 |如果已啟用走勢圖，這是 hello 作業 tooperform hello 清單 toocalculate hello 值 hello 走勢圖中每一個屬性上。<br><br>-最後一個範例： Hello 數列 hello 的時間間隔內的最後一個值。<br>-最大值： Hello 數列 hello 的時間間隔內最大值。<br>-最小值： Hello 數列 hello 的時間間隔內最小值。<br>Hello 數列 hello 的時間間隔內的數值總和： 總和。<br>摘要： 使用 hello 做 hello 標頭中的 hello 查詢相同的量值命令。 |

### <a name="thresholds">臨界值</a>
臨界值可讓您 toodisplay 彩色的圖示下一個 tooeach 項目清單中，提供快速的視覺指標，超過特定值或落在特定範圍內的項目中。  比方說，您無法顯示項目可接受的值，如果 hello 值，指出警告，而在範圍內的黃色和紅色的綠色的圖示，如果它超過錯誤值。

當您針對組件啟用臨界值時，必須指定一或多個臨界值。  如果某個項目的 hello 值大於臨界值及低於 hello 下一個臨界值，則會使用該色彩。  Hello 項目是否大於然後最高的臨界值，則會設定該色彩。   

每個臨界值組都有一個具有 **Default** 值的臨界值。  這是 hello 色彩會設定如果不超過任何其他值。  您可以新增或移除臨界值，依序按一下 hello ** + **或**x** ] 按鈕。

hello 下表描述 tresholds hello 設定。

| 設定 | 說明 |
|:--- |:--- |
| 啟用臨界值 |選取 toodisplay 色彩圖示 toohello 剩餘的每個值，指出其健全狀況相對 toospecified 臨界值。 |
| 名稱 |名稱 tooidentify hello 臨界值。 |
| 閾值 |Hello 臨界值。  每個清單項目的 hello 健全狀況色彩會設 toohello 色彩 hello hello 項目的值超過最大臨界值。  沒有一個是 hello 色彩，如果不超過任何臨界值的預設閾值。 |
| 色彩 |Hello 臨界值的色彩。 |

## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)toosupport hello 查詢部分視覺效果中的。
