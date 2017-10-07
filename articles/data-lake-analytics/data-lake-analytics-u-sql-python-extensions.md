---
title: "aaaExtend U-SQL 指令碼使用在 Azure Data Lake Analytics Python |Microsoft 文件"
description: "了解 toorun Python U-SQL 指令碼中的程式碼"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>教學課程︰開始擴充 U-SQL 與 Python

U sql Python 延伸可讓開發人員 tooperform 大量平行執行 Python 程式碼。 hello 下列範例將說明 hello 基本步驟：

* 使用 hello `REFERENCE ASSEMBLY` hello U-SQL 指令碼的陳述式 tooenable Python 擴充功能
* 使用 hello`REDUCE`作業 toopartition hello 輸入在索引鍵的資料
* hello U-SQL 的 Python 擴充功能包含內建減壓器 (`Extension.Python.Reducer`) 每個頂點指派 toohello 減壓器上執行的 Python 程式碼
* hello U-SQL 指令碼包含內嵌的 hello Python 程式碼具有函式，呼叫`usqlml_main`，接受熊做為輸入的資料框架，並傳回熊做為輸出資料框架。

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a>Python 如何與 U-SQL 整合

### <a name="datatypes"></a>資料類型

* U-SQL 的字串和數值資料行在 Pandas 和 U-SQL 之間會如現狀轉換
* U SQL Null 會轉換從熊 tooand`NA`值

### <a name="schemas"></a>結構描述

* U-SQL 不支援 Pandas 的索引向量。 Hello Python 函式中的所有輸入的資料框架一定 64 位元數字的索引，從 0 到 hello 資料列數目減 1。 
* U-SQL 資料集不能有重複的資料行名稱。
* U-SQL 資料集的資料行名稱不是字串。 

### <a name="python-versions"></a>Python 版本
僅支援 Python 3.5.1 (針對 Windows 編譯)。 

### <a name="standard-python-modules"></a>標準 Python 模組
包含的所有 hello 標準 Python 模組。

### <a name="additional-python-modules"></a>其他 Python 模組
除了 hello 標準的 Python 程式庫，幾個常用的 python 程式庫會包含：

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>例外狀況訊息
目前，Python 程式碼中的例外狀況是顯示為泛型頂點失敗。 在未來的 hello，hello U-SQL 作業錯誤訊息會顯示 hello Python 例外狀況訊息。

### <a name="input-and-output-size-limitations"></a>輸入和輸出的大小限制
每個頂點都有指派 tooit 的記憶體數量有限。 目前，該限制為 6 GB 用於 AU。 Hello 輸入和輸出資料框架必須存在於記憶體中 hello Python 程式碼，因為 hello hello 輸入和輸出的大小總計不能超過 6 GB。

## <a name="see-also"></a>另請參閱
* [Microsoft Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
* [使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)
* [針對 Azure 資料湖分析工作使用 U-SQL 視窗函式](data-lake-analytics-use-window-functions.md)

