---
title: "在 OMS 記錄分析的檢視表設計工具的 aaaTile 參考 |Microsoft 文件"
description: "檢視表設計工具中記錄分析可讓您自訂 toocreate hello OMS 主控台中，包含不同的視覺效果的 hello OMS 儲存機制中資料的檢視。 這篇文章會提供每一個自訂檢視中 hello 磚可用 toouse hello 設定的參考。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Log Analytics 檢視設計工具圖格參考
hello 檢視表設計工具中記錄分析可讓您自訂 toocreate hello OMS 主控台中，包含不同的視覺效果的 hello OMS 儲存機制中資料的檢視。 這篇文章會提供每一個自訂檢視中 hello 磚可用 toouse hello 設定的參考。

其他與檢視設計工具相關的文章︰

* [檢視設計工具](log-analytics-view-designer.md)-hello 檢視表設計工具和程序來建立和編輯自訂檢視的概觀。
* [視覺效果部分參考](log-analytics-view-designer-parts.md)-參考的每一個 hello hello 設定磚可用 toouse 中自訂檢視。

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則必須寫入所有檢視中的查詢中 hello[新的查詢語言](https://go.microsoft.com/fwlink/?linkid=856078)。  Hello 工作區已升級之前建立的任何檢視會 automtically 轉換。

hello 下表列出 hello 磚 hello 檢視表設計工具中可用的不同型別。  hello 以下章節將詳細資料和其屬性中的每個圖格類型。

| 圖格 | 說明 |
|:--- |:--- |
| [Number](#number-tile) |單一數字，顯示記查詢中的記錄計數。 |
| [雙數字](#two-numbers-tile) |兩個數字，顯示兩個不同查詢的記錄計數。 |
| [環圈](#donut-tile) |環圈圖中 hello 中心的摘要值的查詢為基礎。 |
| [折線圖與圖說文字](#line-chart-amp-callout-tile) |以查詢為依據的折線圖，以及彙總值圖說文字。 |
| [折線圖](#line-chart-tile) |根據查詢的折線圖。 |
| [雙時間軸](#two-timelines-tile) |兩個各以不同查詢為依據的系列直條圖。 |

## <a name="number-tile"></a>數字圖格
hello**數目**磚會顯示單一數字顯示 hello 次數的記錄記錄查詢和標籤。

![數字圖格](media/log-analytics-view-designer/tile-number.png)

| 設定 | 說明 |
|:--- |:--- |
| 名稱 |頂端的 hello hello 文字 toodisplay 磚。 |
| 說明 |文字 toodisplay hello 磚名稱下。 |
| **圖格** | |
| 圖例 |文字 toodisplay 下 hello 值。 |
| 查詢 |查詢 toorun。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| **進階** |**> 資料流驗證** |
| 已啟用 |如果資料流驗證應啟用 hello 磚，請選取。  如果沒有可用的 hello 磚資料，這會提供替代的訊息。  這是一般常用的 tooprovide 訊息在 hello 暫存期間當 hello 檢視已安裝，而且資料變為可用。 |
| 查詢 |如果沒有可用的 hello 檢視資料，請查詢 toorun toocheck。  如果 hello 查詢會不傳回任何結果，而不是從 hello 主查詢的 hello 值會顯示訊息。 |
| 訊息 |訊息 toodisplay 如果 hello 資料流程驗證查詢會不傳回任何資料。  如果您不提供任何訊息，會顯示「正在執行評估」。 |


## <a name="two-numbers-tile"></a>雙數字圖格
hello**兩個數目**磚會顯示兩個顯示每個記錄，從兩個不同的記錄檔查詢和標籤 hello 計數的數字。

![雙數字圖格](media/log-analytics-view-designer/tile-two-numbers.png)

| 設定 | 說明 |
|:--- |:--- |
| 名稱 |頂端的 hello hello 文字 toodisplay 磚。 |
| 說明 |文字 toodisplay hello 磚名稱下。 |
| **第一個圖格** | |
| 圖例 |文字 toodisplay 下 hello 值。 |
| 查詢 |查詢 toorun。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| **第二個圖格** | |
| 圖例 |文字 toodisplay 下 hello 值。 |
| 查詢 |查詢 toorun。  將會顯示 hello hello 的計數 hello 查詢所傳回的記錄。 |
| **進階** |**> 資料流驗證** |
| 已啟用 |如果資料流驗證應啟用 hello 磚，請選取。  如果沒有可用的 hello 磚資料，這會提供替代的訊息。  這是一般常用的 tooprovide 訊息在 hello 暫存期間當 hello 檢視已安裝，而且資料變為可用。 |
| 查詢 |如果沒有可用的 hello 檢視資料，請查詢 toorun toocheck。  如果 hello 查詢會不傳回任何結果，而不是從 hello 主查詢的 hello 值會顯示訊息。 |
| 訊息 |訊息 toodisplay 如果 hello 資料流程驗證查詢會不傳回任何資料。  如果您不提供任何訊息，會顯示「正在執行評估」。 |


## <a name="donut-tile"></a>環圈圖格
hello**甜甜圈**磚會顯示彙總記錄查詢中的值資料行從一個單一數字。  hello 環圈圖會以圖形方式顯示 hello 前三筆記錄的結果。

![環圈圖格](media/log-analytics-view-designer/tile-donut.png)

| 設定 | 說明 |
|:--- |:--- |
| 名稱 |頂端的 hello hello 文字 toodisplay 磚。 |
| 說明 |文字 toodisplay hello 磚名稱下。 |
| **環圈** | |
| 查詢 |Hello 甜甜圈的查詢 toorun。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。  這通常是使用 hello 的查詢**量值**關鍵字 toosummarize 結果。 |
| **環圈** |**> 中心** |
| 文字 |文字 toodisplay 下 hello hello 環圈圖內的值。 |
| 作業 |hello 作業 tooperform hello 值屬性 toosummarize tooa 單一值。<br><br>-總和： Hello 將值加入所有記錄的 hello 屬性值。<br>百分比： Hello 屬性值比較 toohello 的記錄從 hello 來加總量值的百分比來加總量值的所有記錄。 |
| 中心作業使用的結果值 |（選擇性) 按一下 hello 加號 tooadd 一或多個值。  hello hello 查詢結果會限制的 toorecords 與您指定的 hello 屬性值。  如果不加入任何值，比所有記錄會包含在 hello 查詢。 |
| **環圈** |**> 其他選項** |
| 色彩 |hello 色彩 toodisplay 的每一個 hello 三個最上層屬性。  如果您想 toospecify 替代色彩的特定屬性值，然後使用進階色彩對應。 |
| 進階色彩對應 |顯示特定屬性值的顏色。  如果您指定的 hello 值存在於 hello 最上層的三個，則 hello 替代色彩會顯示而不是 hello 標準色彩。  如果 hello 屬性不在 hello 三，則 hello 色彩不會顯示。 |
| **進階** |**> 資料流驗證** |
| 已啟用 |如果資料流驗證應啟用 hello 磚，請選取。  如果沒有可用的 hello 磚資料，這會提供替代的訊息。  這是一般常用的 tooprovide 訊息在 hello 暫存期間當 hello 檢視已安裝，而且資料變為可用。 |
| 查詢 |如果沒有可用的 hello 檢視資料，請查詢 toorun toocheck。  如果 hello 查詢會不傳回任何結果，而不是從 hello 主查詢的 hello 值會顯示訊息。 |
| 訊息 |訊息 toodisplay 如果 hello 資料流程驗證查詢會不傳回任何資料。  如果您不提供任何訊息，會顯示「正在執行評估」。 |


## <a name="line-chart-tile"></a>折線圖圖格
hello**折線圖**磚會顯示經過一段時間的多個數列從記錄檔查詢的折線圖。  

![折線圖與圖說文字圖格](media/log-analytics-view-designer/tile-line-chart.png)

| 設定 | 說明 |
|:--- |:--- |
| 名稱 |頂端的 hello hello 文字 toodisplay 磚。 |
| 說明 |文字 toodisplay hello 磚名稱下。 |
| **折線圖** | |
| 查詢 |查詢 toorun hello 折線圖。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。  這通常是使用 hello 的查詢**量值**關鍵字 toosummarize 結果。  如果 hello 查詢使用 hello**間隔**關鍵字則 hello hello 圖表的 x 軸將會使用此時間間隔。  如果 hello 查詢不包含 hello**間隔**關鍵字，則每小時間隔用於 hello x 軸。 |
| **折線圖** |**> Y 軸** |
| 使用對數刻度 |選取 toouse hello y 軸的對數標尺。 |
| Units |請指定 hello 單元 hello hello 查詢所傳回的值。  這項資訊是使用的 toodisplay 標籤 hello 圖表指出 hello 實值型別上也可以將 hello 值轉換。  hello**單位類型**指定 hello 單元 hello 分類，並定義 hello**目前的單位類型**可用的值。  如果您選取的值在**轉換成**hello 數值會轉換然後從 hello**目前單位**輸入 toohello**轉換成**型別。 |
| 自訂標籤 |Hello Y 軸 下一步 toohello hello 單位型別的標籤的文字 toodisplay。  如果沒有標籤指定時，會顯示 hello 單位類型。 |
| **進階** |**> 資料流驗證** |
| 已啟用 |如果資料流驗證應啟用 hello 磚，請選取。  如果沒有可用的 hello 磚資料，這會提供替代的訊息。  這是一般常用的 tooprovide 訊息在 hello 暫存期間當 hello 檢視已安裝，而且資料變為可用。 |
| 查詢 |如果沒有可用的 hello 檢視資料，請查詢 toorun toocheck。  如果 hello 查詢會不傳回任何結果，而不是從 hello 主查詢的 hello 值會顯示訊息。 |
| 訊息 |訊息 toodisplay 如果 hello 資料流程驗證查詢會不傳回任何資料。  如果您不提供任何訊息，會顯示「正在執行評估」。 |


## <a name="line-chart--callout-tile"></a>折線圖與圖說文字圖格
hello**行圖表 （& s） 圖說文字**磚會與從記錄檔查詢的多個數列的折線圖顯示隨時間彙總值的註標。  

![折線圖與圖說文字圖格](media/log-analytics-view-designer/tile-line-chart-callout.png)

| 設定 | 說明 |
|:--- |:--- |
| 名稱 |頂端的 hello hello 文字 toodisplay 磚。 |
| 說明 |文字 toodisplay hello 磚名稱下。 |
| **折線圖** | |
| 查詢 |查詢 toorun hello 折線圖。  hello 第一個屬性應為文字值與 hello 第二個屬性的數值。  這通常是使用 hello 的查詢**量值**關鍵字 toosummarize 結果。  如果 hello 查詢使用 hello**間隔**關鍵字則 hello hello 圖表的 x 軸將會使用此時間間隔。  如果 hello 查詢不包含 hello**間隔**關鍵字，則每小時間隔用於 hello x 軸。 |
| **折線圖** |**> 圖說文字** |
| 圖說文字 |標題文字 toodisplay 高於 hello 圖說文字值。 |
| 系列名稱 |Hello 數列 toouse hello 圖說文字值的屬性值。  如果未不提供任何數列，則會使用從 hello 查詢的所有記錄。 |
| 作業 |hello 作業 tooperform hello 值屬性 toosummarize tooa 單一值的 hello 圖說文字。<br>所有記錄中的 hello 值的平均： 平均。<br><br>計數： Hello 查詢所傳回的所有記錄的計數。<br>-最後一個範例： Hello hello 圖表中包含的最後一個間隔中的值。<br>的從包含 hello 圖表中的 hello 間隔最大值： 最大值。<br>的從包含 hello 圖表中的 hello 間隔最小值： 最小值。<br>所有記錄中的 hello 值的總和： 總和。 |
| **折線圖** |**> Y 軸** |
| 使用對數刻度 |選取 toouse hello y 軸的對數標尺。 |
| Units |請指定 hello 單元 hello hello 查詢所傳回的值。  這項資訊是使用的 toodisplay 標籤 hello 圖表指出 hello 實值型別上也可以將 hello 值轉換。  hello**單位類型**指定 hello 單元 hello 分類，並定義 hello**目前的單位類型**可用的值。  如果您選取的值在**轉換成**hello 數值會轉換然後從 hello**目前單位**輸入 toohello**轉換成**型別。 |
| 自訂標籤 |Hello Y 軸 下一步 toohello hello 單位型別的標籤的文字 toodisplay。  如果沒有標籤指定時，會顯示 hello 單位類型。 |
| **進階** |**> 資料流驗證** |
| 已啟用 |如果資料流驗證應啟用 hello 磚，請選取。  如果沒有可用的 hello 磚資料，這會提供替代的訊息。  這是一般常用的 tooprovide 訊息在 hello 暫存期間當 hello 檢視已安裝，而且資料變為可用。 |
| 查詢 |如果沒有可用的 hello 檢視資料，請查詢 toorun toocheck。  如果 hello 查詢會不傳回任何結果，而不是從 hello 主查詢的 hello 值會顯示訊息。 |
| 訊息 |訊息 toodisplay 如果 hello 資料流程驗證查詢會不傳回任何資料。  如果您不提供任何訊息，會顯示「正在執行評估」。 |


## <a name="two-timelines-tile"></a>雙時間軸圖格
hello**兩個時刻表**磚會顯示經過一段時間為直條圖的 hello 的兩個記錄檔查詢的結果。  每個系列會顯示一個圖說文字。  

![雙時間軸圖格](media/log-analytics-view-designer/tile-two-timelines.png)

| 設定 | 說明 |
|:--- |:--- |
| 名稱 |頂端的 hello hello 文字 toodisplay 磚。 |
| 說明 |文字 toodisplay hello 磚名稱下。 |
| 第一個圖 | |
| 圖例 |在 hello 第一個數列的 hello 圖說文字的文字 toodisplay。 |
| 色彩 |色彩 toouse hello hello 第一個數列中的資料行。 |
| 圖表查詢 |查詢 toorun hello 第一個數列。  hello hello 的計數記錄每個時間間隔內會呈現 hello 圖表資料行。 |
| 作業 |hello 作業 tooperform hello 值屬性 toosummarize tooa 單一值的 hello 圖說文字。<br><br>所有記錄中的 hello 值的平均： 平均。<br>計數： Hello 查詢所傳回的所有記錄的計數。<br>-最後一個範例： Hello hello 圖表中包含的最後一個間隔中的值。<br>的從包含 hello 圖表中的 hello 間隔最大值： 最大值。 |
| **第二個圖** | |
| 圖例 |在 hello 第二個數列的 hello 圖說文字的文字 toodisplay。 |
| 色彩 |色彩 toouse hello hello 第二個數列中的資料行。 |
| 圖表查詢 |查詢 toorun hello 第二個數列。  hello hello 的計數記錄每個時間間隔內會呈現 hello 圖表資料行。 |
| 作業 |hello 作業 tooperform hello 值屬性 toosummarize tooa 單一值的 hello 圖說文字。<br><br>所有記錄中的 hello 值的平均： 平均。<br>計數： Hello 查詢所傳回的所有記錄的計數。<br>-最後一個範例： Hello hello 圖表中包含的最後一個間隔中的值。<br>的從包含 hello 圖表中的 hello 間隔最大值： 最大值。 |
| **進階** |**> 資料流驗證** |
| 已啟用 |如果資料流驗證應啟用 hello 磚，請選取。  如果沒有可用的 hello 磚資料，這會提供替代的訊息。  這是一般常用的 tooprovide 訊息在 hello 暫存期間當 hello 檢視已安裝，而且資料變為可用。 |
| 查詢 |如果沒有可用的 hello 檢視資料，請查詢 toorun toocheck。  如果 hello 查詢會不傳回任何結果，而不是從 hello 主查詢的 hello 值會顯示訊息。 |
| 訊息 |訊息 toodisplay 如果 hello 資料流程驗證查詢會不傳回任何資料。  如果您不提供任何訊息，會顯示「正在執行評估」。 |


## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)toosupport hello 查詢磚中的。
* 新增[視覺效果部分](log-analytics-view-designer-parts.md)tooyour 自訂檢視。
