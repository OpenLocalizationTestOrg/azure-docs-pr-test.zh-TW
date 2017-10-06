---
title: "aaaInvoke 預存程序從 Azure 資料 Factory 複製活動 |Microsoft 文件"
description: "了解如何在 Azure SQL Database 或從 Azure Data Factory 的 SQL Server 中的預存程序 tooinvoke 複製活動。"
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>從 Azure Data Factory 中的複製活動叫用預存程序
當將資料複製到[SQL Server](data-factory-sqlserver-connector.md)或[Azure SQL Database](data-factory-azure-sql-connector.md)，您可以設定 hello **SqlSink**在複製活動 tooinvoke 預存程序。 您可能想 toouse hello 預存程序 tooperform toohello 目的地資料表中插入資料之前，需要任何額外的處理 （合併資料行，查閱值，插入多個資料表等）。 此功能會利用[資料表值參數](https://msdn.microsoft.com/library/bb675163.aspx)。 

hello 下列範例顯示如何 tooinvoke 預存程序在 SQL Server 資料庫從 Data Factory 管線 （複製活動）：  

## <a name="output-dataset-json"></a>輸出資料集 JSON
在 hello 輸出資料集 JSON，設定 hello**類型**至： **SqlServerTable**。 設定得**AzureSqlTable** toouse 與 Azure SQL database。 hello 值**tableName**屬性必須符合 hello hello 預存程序之第一個參數的名稱。  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a>複製活動 JSON 中的 SqlSink 區段
定義 hello **SqlSink**區段 hello 複製活動 JSON 中，如下所示。 tooinvoke 預存程序時將資料插入 hello 接收/目的地資料庫，指定兩個值**SqlWriterStoredProcedureName**和**SqlWriterTableType**屬性。 如需這些屬性的描述，請參閱[SqlSink hello SQL Server 連接器文件中的區段](data-factory-sqlserver-connector.md#sqlsink)。

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a>預存程序定義 
在資料庫中，定義 hello 預存程序，以做為名稱相同的 hello **SqlWriterStoredProcedureName**。 hello 預存程序會處理從 hello 來源資料存放區輸入的資料，並將資料插入 hello 目的地資料庫中的資料表。 hello hello 預存程序的第一個參數名稱必須符合 hello tableName hello 資料集 JSON （行銷） 中定義。

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>資料表類型定義
在資料庫中，定義 hello 資料表類型，以做為名稱相同的 hello **SqlWriterTableType**。 hello hello 資料表類型的結構描述必須符合 hello 的 hello 輸入資料集的結構描述。

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>後續步驟
檢閱下列連接器的 hello 文件，如需完整的 JSON 範例： 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
