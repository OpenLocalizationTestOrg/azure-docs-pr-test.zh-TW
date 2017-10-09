---
title: "aaaRegular 運算式中的 OMS 記錄分析記錄搜尋 |Microsoft 文件"
description: "記錄分析記錄搜尋 toohello 篩選 hello 結果，根據 tooa 規則運算式中，您可以使用 hello RegEx 關鍵字。  這篇文章會提供數個範例使用這些運算式 hello 語法。"
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
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>記錄分析中使用規則運算式 toofilter 搜尋記錄檔

[記錄搜尋](log-analytics-log-searches.md)tooextract hello 記錄分析儲存機制中的資訊可讓您。  [篩選條件運算式](log-analytics-search-reference.md#filter-expressions)讓您根據 toospecific 準則 hello 搜尋 toofilter hello 結果。  hello **RegEx**關鍵字可讓您 toospecify 此篩選器的規則運算式。  

這篇文章提供 hello 記錄分析所使用的規則運算式語法的詳細資料。

> [!NOTE]
> RegEx 僅能搭配可搜尋的欄位使用。  如需可搜尋欄位的詳細資訊，請參閱[在 Log Analytics 中使用記錄搜尋以尋找資料](log-analytics-log-searches.md#use-additional-filters)中的**欄位類型**。


## <a name="regex-keyword"></a>RegEx 關鍵字

使用下列語法 toouse hello 的 hello **RegEx**記錄搜尋中的關鍵字。  您可以使用 hello 這個發行項 toodetermine hello 語法中的 hello 規則運算式本身的其他章節。

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

類型為 toouse 規則運算式 tooreturn 警示的記錄，例如*警告*或*錯誤*，您可以使用下列記錄搜尋 hello。

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>部分符合結果
請注意 hello 規則運算式必須符合 hello 屬性 hello 整個文字。  部分符合結果不會傳回任何記錄。  例如，如果您嘗試從電腦名為 srv01.contoso.com tooreturn 記錄，下列記錄搜尋 hello 就**不**傳回任何記錄。

    Computer=RegEx("srv..")

這是因為只有 hello 名稱第一個部分 hello 與 hello 的規則運算式。  hello 下列兩個記錄檔搜尋會傳回記錄從這部電腦因為其符合 hello 整個名稱。

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>字元
指定不同的字元。

| Character | 說明 | 範例 | 範例相符項目 |
|:--|:--|:--|:--|
| a | 接著一個 hello 字元。 | Computer=RegEx("srv01.contoso.com") | srv01.contoso.com |
| 。 | 任何單一字元。 | Computer=RegEx("srv...contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| a? | Hello 字元零或一個項目。 | Computer=RegEx("srv01?.contoso.com") | srv0.contoso.com<br>srv01.contoso.com |
| a* | Hello 字元的零或多個項目。 | Computer=RegEx("srv01*.contoso.com") | srv0.contoso.com<br>srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| a+ | Hello 字元的一個或多個項目。 | Computer=RegEx("srv01+.contoso.com") | srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [abc] | 比對任何單一字元 hello 括號括住 | Computer=RegEx("srv0[123].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [a-z] | 比對 hello 範圍中的單一字元。  可以包含多個範圍。 | Computer=RegEx("srv0[1-3].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [^abc] | 無 hello hello 括號括住的字元 | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [^a-z] | 無 hello 範圍中的 hello 字元。 | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | 比對數字字元的範圍。 | Computer=RegEx("srv[01-03].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| @ | 任何字元的字串。 | Computer=RegEx("srv@.contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>字元的多個項目
指定特定字元的多個項目。

| Character | 說明 | 範例 | 範例相符項目 |
|:--|:--|:--|:--|
| a{n} |  *n*hello 字元的項目。 | Computer=RegEx("bw-win-sc01{3}.bwren.lab") | bw-win-sc0111.bwren.lab |
| a{n,} |  *n*或 hello 字元的多個項目。 | Computer=RegEx("bw-win-sc01{3,}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab<br>bw-win-sc0111111.bwren.lab |
| a{n,m} |  *n*太*m* hello 字元的項目。 | Computer=RegEx("bw-win-sc01{3,5}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>邏輯運算式
從多個值選取。

| Character | 說明 | 範例 | 範例相符項目 |
|:--|:--|:--|:--|
| &#124; | 邏輯 OR。  如果符合任一個運算式則傳回結果。 | Type=Alert AlertSeverity=RegEx("Warning&#124;Error") | 警告<br>錯誤 |
| & | 邏輯 AND。  如果符合兩個運算式則傳回結果 | EventData=regex("(Security.\*&.\*success.\*)") | 安全性稽核成功 |


## <a name="literals"></a>常值
將特殊字元 tooliteral 字元轉換。  這包括提供，例如功能 tooregular 運算式的字元嗎？-\*^\[\]{}\(\)+\|。 （& s)。

| Character | 說明 | 範例 | 範例相符項目 |
|:--|:--|:--|:--|
| \\ | 將轉換的特殊字元 tooa 常值。 | Status_CF=\\[Error\\]@<br>Status_CF=Error\\-@ | [Error]找不到檔案。<br>Error-找不到檔案。 |


## <a name="next-steps"></a>後續步驟

* 讓您熟悉[記錄搜尋](log-analytics-log-searches.md)tooview 和分析 hello 記錄分析儲存機制中的資料。
