---
title: "開始使用 hello U-SQL 目錄 |Microsoft 文件"
description: "了解如何 toouse hello U-SQL 目錄 tooshare 程式碼和資料。"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a>開始使用 hello U-SQL 類別目錄

## <a name="create-a-tvf"></a>建立 TVF

Hello 先前的 U-SQL 指令碼中重複出現的擷取 tooread 從 hello hello 使用相同原始程式檔。 與 hello U SQL 資料表值函式 (TVF)，您可以將封裝 hello 資料供日後使用。  

hello 下列指令碼會建立稱為 TVF `Searchlog()` hello 預設資料庫和結構描述中：

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

hello 下列指令碼會示範如何 toouse hello TVF hello 至上一個指令碼中所定義：

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a>建立檢視

如果您有單一查詢運算式，而不是 TVF 您可以使用 U-SQL 檢視 tooencapsulate 該運算式。

hello 下列指令碼會建立一個名為檢視`SearchlogView`hello 預設資料庫和結構描述中：

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

下列指令碼的 hello 示範 hello 使用 hello 定義檢視表：

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a>建立資料表
在關聯式資料庫資料表，用 U-SQL 您可以使用預先定義的結構描述建立資料表或資料表建立 hello 從推斷結構描述填入 hello 資料表 （也稱為 CREATE TABLE AS SELECT 或 CTAS） hello 查詢。

使用下列指令碼的 hello 建立的資料庫和兩個資料表：

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a>查詢資料表
您可以查詢資料表，例如建立 hello 先前的指令碼中，在 hello 您查詢 hello 資料檔案的方式相同。 而不是建立使用擷取的資料列集，您現在可以參考 toohello 資料表名稱。

從 hello 資料表 tooread 修改您先前用過的 hello 轉換指令碼：

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 >目前，您無法執行 SELECT 在 hello 相同指令碼以 hello 其中一個資料表上建立 hello 資料表的位置。

## <a name="next-steps"></a>後續步驟
* [Microsoft Azure Data Lake Analytics 概觀](data-lake-analytics-overview.md)
* [使用適用於 Visual Studio 的資料湖工具開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)
* [使用 Azure 入口網站監視和疑難排解 Azure Data Lake Analytics 作業](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
