---
title: "Azure Data Factory 中的 aaaRepeatable 複製 |Microsoft 文件"
description: "了解 tooavoid 重複即使複製資料配量執行一次以上的資料。"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Azure Data Factory 中的可重複複製

## <a name="repeatable-read-from-relational-sources"></a>從關聯式來源進行可重複的讀取
複製資料時從關聯式資料存放區，請注意 tooavoid 重複性非預期的結果。 在 Azure Data Factory 中，您可以手動重新執行配量。 您也可以為資料集設定重試原則，使得在發生失敗時，重新執行配量。 當其中一個方式，重新執行配量時，您需要 toomake 確定的 hello 相同的資料如何讀取無論執行多次的配量。  
 
> [!NOTE]
> hello 下列範例是適用於 Azure SQL 但支援矩形的資料集的適用 tooany 資料存放區。 您可能必須 tooadjust hello**類型**的來源和 hello**查詢**屬性 (例如： 查詢，而不是 sqlReaderQuery) hello 資料存放區。   

通常，當從關聯式存放區讀取，您會想 tooread 對應 toothat 配量只 hello 資料。 因此方式 toodo 會是使用 Azure Data Factory 中的 hello WindowStart 和 WindowEnd 系統變數可用。 閱讀有關 hello 變數和 Azure Data Factory 中的函式，在 hello [Azure Data Factory-函式和系統變數](data-factory-functions-variables.md)發行項。 範例： 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
此查詢會讀取從 hello 資料表 MyTable 落在 hello 配量持續時間範圍 (WindowStart-> WindowEnd) 中的資料。 重新執行此配量一定會確保相同資料讀取該 hello。 

在其他情況下，您可能希望 tooread hello 整份資料表，並可能定義 hello sqlReaderQuery，如下所示：

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>可重複寫入 tooSqlSink
太複製資料時**Azure SQL/SQL Server**從其他資料存放區中，您必須注意 tooavoid tookeep 直至非預期的結果。 

當複製資料 tooAzure SQL/SQL Server 資料庫，hello 複製活動將預設附加 toohello 接收資料表。 例如，您會將資料複製包含兩筆記錄 toohello 下表中的 Azure SQL/SQL Server 資料庫 CSV （逗點分隔值） 檔案。 配量執行時，hello 兩筆記錄會複製的 toohello SQL 資料表。 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

假設您在原始程式檔中發現錯誤，並更新 hello 2 too4 的向下 Tube 最低數量。 如果您重新執行 hello 資料配量的這段時間內以手動方式，您會看到兩個新的記錄會附加 tooAzure SQL/SQL Server 資料庫。 這個範例假設所有的 hello hello 資料表中的資料行都沒有 hello 主索引鍵條件約束。

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid 這種行為，您需要 toospecify UPSERT 語意使用其中一種 hello 下列兩種機制：

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>機制 1：使用 sqlWriterCleanupScript
您可以使用 hello **sqlWriterCleanupScript**屬性 tooclean hello 之前插入 hello 資料配量執行時，接收資料表的資料。 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

對應來源 hello SQL 資料表 toohello 配量的第一個 toodelete 資料配量執行時，執行 hello 清除指令碼。 然後 hello 複製活動會將資料插入 hello SQL 資料表中。 如果重新執行 hello 配量時，更新 hello 數量視。

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

假設 hello 一般墊圈記錄被移除了 hello 原始 csv。 然後重新執行 hello 配量會產生下列結果 hello: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

hello 複製活動已執行 hello 清除指令碼 toodelete hello 對應的資料為該扇區。 然後輸入 hello 讀取 hello csv （可再包含只有一筆記錄） 並插入 hello 資料表。 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>機制 2：使用 sliceIdentifierColumnName
> [!IMPORTANT]
> 目前「Azure SQL 資料倉儲」並不支援 sliceIdentifierColumnName。 

第二個機制 tooachieve 重複性 hello 是專用的資料行 (使用 sliceIdentifierColumnName) 擁有 hello 目標資料表中。 Azure Data Factory tooensure hello 來源和目的地保持同步處理會使用這個資料行。 這個方法的效果時變更，或定義 hello 目的地 SQL 資料表結構描述的彈性。 

此資料行用於 Azure Data factory 重複性和 hello 程序中，Azure Data Factory 不會進行任何結構描述變更 toohello 資料表。 方式 toouse 這種方法：

1. 定義類型的資料行**二進位檔 (32)** hello 目的地 SQL 資料表中。 此資料行不應該有任何條件約束。 讓我們針對此範例將這個資料行命名為 AdfSliceIdentifier。


    來源資料表：

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    目的地資料表： 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. 使用它 hello 複製活動中，如下所示：
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Azure Data Factory 會填入此資料行，其需要根據 tooensure hello 來源和目的地保持同步。 hello 這個資料行值不應該使用這個環境之外。 

類似 toomechanism 1，複製活動會自動清除 hello hello 從 hello 目的地 SQL 資料表指定配量的資料。 然後將資料插入從 toohello 目的地資料表中的來源。 

## <a name="next-steps"></a>後續步驟
檢閱下列連接器的 hello 文件，如需完整的 JSON 範例： 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [Azure SQL 資料倉儲](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)