---
title: "使用者定義函數的資料流分析 JavaScript aaaAzure |Microsoft 文件"
description: "使用 JavaScript 使用者定義函式來執行進階查詢技術"
keywords: "javascript, 使用者定義函式, udf"
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 28eeb8f6437c23989e8887687b950361fed4414c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-javascript-user-defined-functions"></a>Azure 串流分析 JavaScript 使用者定義函式
Azure 串流分析支援以 JavaScript 撰寫的使用者定義函式。 使用豐富的 hello**字串**， **RegExp**，**數學**，**陣列**，和**日期**方法，提供 JavaScript，複雜資料轉換與串流分析工作變得更容易 toocreate。

## <a name="javascript-user-defined-functions"></a>JavaScript 使用者定義函式
JavaScript 使用者定義的函式支援無狀態且只做為計算用途的純量函式，而且不需要外部連線能力。 hello 傳回函式的值只能是純量 （單一） 值。 加入 JavaScript 使用者定義函數 tooa 作業之後，您可以在任何地方在 hello 查詢中，內建的純量函式中使用 hello 函式。

從以下的一些案例可以看出 JavaScript 使用者定義函式很實用：
* 剖析及操作具有規則運算式函式的字串，例如：**Regexp_Replace()** 和 **Regexp_Extract()**
* 解碼和編碼資料，例如：從二進位轉換成十六進位
* 使用 JavaScript **Math** 函式做數學運算
* 執行陣列作業，例如，排序、連結、尋找及填入

以下是一些在串流分析中無法使用 JavaScript 使用者定義函式達成的事項：
* 呼叫外部 REST 端點，例如，執行反向 IP 查詢或從外部來源提取參考資料
* 對輸入/輸出執行自訂事件格式序列化或還原序列化
* 建立自訂彙總

雖然函式像**Date.GetDate()**或**Math.random()**不會封鎖在 hello 函式定義中，您應該避免使用它們。 這些函式**不**傳回 hello 相同結果每次您呼叫它們，並 hello Azure Stream Analytics 服務不會保留筆記本的函式引動過程，以及傳回結果。 如果函式會傳回不同的結果上 hello 相同的事件，您或 hello Stream Analytics 服務重新啟動作業時不保證重複性。

## <a name="add-a-javascript-user-defined-function-in-hello-azure-portal"></a>在 hello Azure 入口網站中加入 JavaScript 使用者定義函式
toocreate 的簡單 JavaScript 使用者定義函式在為現有的資料流分析工作，請執行下列步驟：

1.  在 hello Azure 入口網站，尋找您的資料流分析工作。
2.  在 [作業拓撲] 下，選取您的函式。 空白的函式清單隨即出現。
3.  選取新的使用者定義函數，toocreate**新增**。
4.  在 hello**新函式**刀鋒視窗中，針對**函式類型**，選取**JavaScript**。 Hello 編輯器中會出現預設函式樣板。
5.  Hello **UDF 別名**，輸入**hex2Int**，並變更 hello 函式實作，如下所示：

    ```
    // Convert Hex value toointeger.
    function main(hexValue) {
        return parseInt(hexValue, 16);
    }
    ```

6.  選取 [ **儲存**]。 您的函式會出現在 hello 函式清單。
7.  選取新的 hello **hex2Int**函式，並檢查 hello 函式定義。 所有函式具有**UDF**前置詞加入的 toohello 函式的別名。 您需要*包含 hello 前置詞*當資料流分析查詢中呼叫 hello 函式。 在此情況下，您會呼叫 **UDF.hex2Int**。

## <a name="call-a-javascript-user-defined-function-in-a-query"></a>在查詢中呼叫 JavaScript 使用者定義函式

1. 在 [hello 查詢編輯器] 中，在**作業拓撲**，選取**查詢**。
2.  編輯您的查詢，並接著呼叫 hello 使用者定義函數，就像這樣：

    ```
    SELECT
        time,
        UDF.hex2Int(offset) AS IntOffset
    INTO
        output
    FROM
        InputStream
    ```

3.  tooupload hello 範例資料檔，以滑鼠右鍵按一下 hello 作業輸入。
4.  tootest 您查詢中，選取**測試**。


## <a name="supported-javascript-objects"></a>支援的 JavaScript 物件
Azure 串流分析 JavaScript 使用者定義函式支援標準的內建 JavaScript 物件。 如需這些物件的清單，請參閱[全域物件](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects)。

### <a name="stream-analytics-and-javascript-type-conversion"></a>串流分析與 JavaScript 類型轉換

有一些差異在 hello hello 串流分析查詢語言和 JavaScript 支援的型別中。 下表列出之間兩個 hello hello 轉換對應：

串流分析 | JavaScript
--- | ---
bigint | 數字 (JavaScript 只能表示整數向上 tooprecisely 2 ^53)
DateTime | Date (JavaScript 只支援毫秒)
double | Number
nvarchar(MAX) | String
Record | Object
陣列 | 陣列
NULL | Null


以下是 JavaScript 至串流分析的轉換：


JavaScript | 串流分析
--- | ---
數字 | Bigint （如果 round 和長時間之間 hello 號碼。MinValue，長時間。MaxValue。否則，它是 double）
Date | DateTime
String | nvarchar(MAX)
Object | Record
陣列 | 陣列
Null、Undefined | NULL
任何其他類型 (例如，函式或錯誤) | 不支援 (產生執行階段錯誤)

## <a name="troubleshooting"></a>疑難排解
JavaScript 執行階段錯誤會視為嚴重錯誤，並透過 hello 活動記錄檔便會顯示。 tooretrieve hello 記錄中 hello Azure 入口網站中，移 tooyour 作業並選取**活動記錄檔**。


## <a name="other-javascript-user-defined-function-patterns"></a>其他 JavaScript 使用者定義函式模式

### <a name="write-nested-json-toooutput"></a>撰寫巢狀的 JSON toooutput
如果您使用做為輸入，輸出資料流分析工作的待處理的處理步驟，而且需要 JSON 格式，您可以撰寫 JSON 字串 toooutput。 hello 下一個範例會呼叫 hello **JSON.stringify()** toopack hello 的所有名稱/值組輸入，並再將它們寫入為單一字串中的值輸出函式。

**JavaScript 使用者定義函式定義：**

```
function main(x) {
return JSON.stringify(x);
}
```

**範例查詢︰**
```
SELECT
    DataString,
    DataValue,
    HexValue,
    UDF.json_stringify(input) As InputEvent
INTO
    output
FROM
    input PARTITION BY PARTITIONID
```

## <a name="get-help"></a>取得說明
如需其他協助，請參閱我們的 [Azure 串流分析論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure 串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
