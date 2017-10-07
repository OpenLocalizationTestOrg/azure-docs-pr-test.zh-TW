---
title: "aaaLoad-Azure Data Lake Store tooSQL 資料倉儲 |Microsoft 文件"
description: "了解如何 toouse PolyBase 外部資料表到 Azure SQL 資料倉儲的 tooload 資料從 Azure 資料湖存放區。"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>將資料從 Azure Data Lake Store 載入到 SQL 資料倉儲
這份文件可讓您所有的必要步驟 tooload 您自己的資料從 Azure 資料湖存放區 (ADLS) 至 SQL 資料倉儲使用 PolyBase。
雖然您無法 toorun 臨機操作查詢 hello 中儲存的資料使用 hello 外部資料表的 ADLS，最佳作法建議 hello 資料匯入 hello SQL 資料倉儲。
估計時間： 10 分鐘，假設您擁有 hello 必要條件需要 toocomplete。
在本教學課程中，您將了解如何：

1. 建立外部資料庫物件 tooload 從 Azure 資料湖存放區。
2. 連接 tooan Azure 資料湖存放區目錄。
3. 將資料載入到 Azure SQL 資料倉儲。

## <a name="before-you-begin"></a>開始之前
toorun 本教學課程中，您需要：

* 服務對服務驗證的 azure Active Directory 應用程式 toouse。 toocreate，遵循[Active directory 驗證](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> 您需要 hello 用戶端識別碼、 金鑰和您的 Active Directory 應用程式 tooconnect tooyour 從 SQL 資料倉儲的 Azure Data Lake 的 OAuth2.0 語彙基元端點值。 Tooget 這些值的方式在上面的 hello 連結的詳細資料。
>請注意，Azure Active Directory 應用程式註冊的 hello '應用程式識別碼' 做為 hello 用戶端識別碼。

* SQL Server Management Studio 或 SQL Server Data Tools，toodownload SSMS 並連接，請參閱[查詢 SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Azure SQL 資料倉儲、 toocreate 一個遵循： https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* 一個啟用或未啟用加密的 Azure Data Lake Store。 toocreate 一個後續： https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Hello 資料來源設定
PolyBase 會使用 T-SQL 外部物件 toodefine hello 位置及 hello 外部資料的屬性。 hello 外部物件會儲存在第則儲存在外部的 SQL 資料倉儲和參考 hello 資料。


###  <a name="create-a-credential"></a>建立認證
tooaccess 您 Azure 資料湖存放區，您將需要 toocreate 資料庫主要金鑰 tooencrypt hello 下一個步驟中所使用的認證秘密。
然後，您會建立資料庫範圍認證，將設定在 AAD 中的 hello 服務主體認證。 使用者已使用 PolyBase tooconnect tooWindows Azure 儲存體 Blob，記下該 hello 認證語法的不同。
tooconnect tooAzure 資料湖存放區，您必須**第一個**建立 Azure Active Directory 應用程式，建立便捷鍵，並授與 hello 應用程式存取 toohello Azure 資料湖資源。 Instrucitons tooperform 依照位於[這裡](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)。

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a>建立 hello 外部資料來源
使用此[CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE]命令 toostore hello 位置 hello 資料和 hello 的資料類型。
您可以在 hello Azure 入口網站和 www.portal.azure.com 找到 hello ADL URI。

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a>設定資料格式
從 ADLS tooimport hello 資料，您需要 toospecify hello 外部檔案格式。 此命令皆具有格式特有的選項 toodescribe 您的資料。
以下是常用檔案格式的範例，它是一個以管線符號分隔的文字檔案。
請查閱我們的 T-SQL 文件，以取得 [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] 的完整清單

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```

## <a name="create-hello-external-tables"></a>建立 hello 外部資料表
現在您已經指定 hello 資料來源和檔案格式，您就準備好 toocreate hello 外部資料表。 外部資料表是您與外部資料進行互動的方式。 PolyBase 會使用遞迴目錄周遊 tooread hello 目錄 hello 位置參數中指定的所有子目錄中的所有檔案。 此外，hello 下列範例顯示如何 toocreate hello 物件。 您必須使用您在 ADLS hello 資料 toocustomize hello 陳述式 toowork。

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a>外部資料表考量
建立外部資料表很簡單，但有一些需要 toobe 所討論的細節。

使用 PolyBase 載入資料屬於強型別。 這表示每個資料列的 hello 所內嵌的資料必須滿足 hello 資料表結構描述定義。
如果給定的資料列與 hello 結構描述定義不相符，hello 負載拒絕 hello 資料列。

hello REJECT_TYPE 但 REJECT_VALUE 選項可讓您 toodefine 多少資料列或 hello 資料的百分比必須存在於 hello 最後的資料表。
在載入期間，如果到達 hello 拒絕值時，hello 載入會失敗。 hello 的已拒絕的資料列的最常見原因是結構描述定義不相符。
例如，如果資料行未正確指定 int hello 結構描述字串 hello 檔案中的 hello 資料時，每個資料列將會失敗 tooload。

hello 位置指定您想要從 tooread 資料 hello 最上層目錄。
在此情況下，如果沒有下 /DimProduct/ PolyBase 子目錄會匯入 hello 子目錄內的所有 hello 資料。

## <a name="load-hello-data"></a>將資料載入 hello
從 Azure Data Lake Store tooload 資料使用 hello [CREATE TABLE AS SELECT (TRANSACT-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)]陳述式。 載入 CTAS 搭配使用 hello 強型別已建立的外部資料表。

CTAS 建立新的資料表，並填入 hello select 陳述式的結果。 CTAS 定義新資料表 toohave hello hello 相同資料行和資料類型，如 hello hello 結果 select 陳述式。 如果您從外部資料表選取 hello 的所有資料行，hello 新資料表會是 hello 外部資料表中的 hello 資料行和資料類型的複本。

在此範例中，我們會從我們的外部資料表 DimProduct_external 建立一個名為 DimProduct 的雜湊分散式資料表。

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>最佳化資料行存放區壓縮
根據預設，SQL 資料倉儲會儲存 hello 資料表作為叢集資料行存放區索引。 載入完成後，部分 hello 資料的資料列可能會不壓縮成 hello 資料行存放區。  有許多原因會導致發生此情況。 詳細資訊，請參閱 toolearn[管理資料行存放區索引][manage columnstore indexes]。

toooptimize 查詢效能和負載之後, 的資料行存放區壓縮重建 hello 資料表 tooforce hello 資料行存放區索引 toocompress hello 的所有資料列。

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

如需維護資料行存放區索引的詳細資訊，請參閱 hello[管理資料行存放區索引][ manage columnstore indexes]發行項。

## <a name="optimize-statistics"></a>最佳化統計資料
載入之後立即是最佳的 toocreate 單一資料行統計資料。 針對統計資料，您將會有一些選項。 例如，如果您在每個資料行上建立單一資料行統計資料可能需要很長的時間 toorebuild hello 的所有統計資料。 如果您知道特定資料行不會成為 toobe 查詢述詞中的，您可以跳建立統計資料，這些資料行。

如果您決定 toocreate 每個資料表的每個資料行的單一資料行統計資料，您可以使用 hello 預存程序程式碼範例`prc_sqldw_create_stats`在 hello[統計資料][ statistics]發行項。

下列範例中的 hello 是很好的起點建立統計資料。 在 hello 維度資料表中，每個資料行和 hello 事實資料表中每個聯結資料行，它會建立單一資料行統計資料。 您可以在稍後新增單一或多個資料行統計資料 tooother 事實資料表資料行。


## <a name="achievement-unlocked"></a>成就解鎖！
您已成功將資料載入到 Azure SQL 資料倉儲。 太棒了！

##<a name="next-steps"></a>後續步驟
載入資料是第一個步驟 toodeveloping hello 使用 SQL 資料倉儲的資料倉儲方案。 請查看我們在[資料表](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview)和 [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md) 上提供的開發資源。


<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
