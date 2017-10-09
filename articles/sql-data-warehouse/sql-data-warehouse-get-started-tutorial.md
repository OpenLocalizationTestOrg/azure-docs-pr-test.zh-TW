---
title: "aaaAzure SQL 資料倉儲-快速入門教學課程 |Microsoft 文件"
description: "本教學課程將教導您如何 tooprovision 和載入資料到 Azure SQL 資料倉儲。 您也將學習 hello 調整、 暫停和微調有關的基本概念。"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a>開始使用 SQL 資料倉儲

本教學課程示範如何將 Azure SQL 資料倉儲的 tooprovision 和載入資料。 您也將學習 hello 調整、 暫停和微調有關的基本概念。 當您完成時，您將會是準備 tooquery 並且瀏覽您的資料倉儲。

**估計時間 toocomplete:**這是一個端對端教學課程，採用約 30 分鐘 toocomplete，一旦您已符合 hello 先決條件的範例程式碼。 

## <a name="prerequisites"></a>必要條件

hello 教學課程假設您熟悉 SQL 資料倉儲基本概念。 如果您需要簡介，請參閱[什麼是 SQL 資料倉儲？](sql-data-warehouse-overview-what-is.md) 

### <a name="sign-up-for-microsoft-azure"></a>註冊 Microsoft Azure
如果您還沒有 Microsoft Azure 帳戶，您需要註冊一個 toouse toosign 這項服務。 如果您已經有帳戶，則可以跳過此步驟。 

1. 瀏覽 toohello 帳戶頁面[https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)
2. 建立免費的 Azure 帳戶，或購買帳戶。
3. 請依照下列指示 hello

### <a name="install-appropriate-sql-client-drivers-and-tools"></a>安裝適當的 SQL 用戶端驅動程式和工具

大部分的 SQL 用戶端工具可以使用 JDBC、 ODBC 或 ADO.NET 連接 tooSQL 資料倉儲。 Toohello 大量 SQL Data Warehouse 支援的 T-SQL 功能，因為某些用戶端應用程式不會與 SQL 資料倉儲完全相容。

如果您執行的是 Windows 作業系統，建議您使用 [Visual Studio] 或 [SQL Server Management Studio]。

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a>建立 SQL 資料倉儲

SQL 資料倉儲是一種特殊類型的資料庫，其設計用來進行大量平行處理。 hello 資料庫分散到多個節點，並處理以平行方式查詢。 SQL 資料倉儲具有協調所有 hello 節點的 hello 活動為控制節點。 hello 節點本身會使用 SQL Database toomanage 您的資料。  

> [!NOTE]
> 建立 SQL 資料倉儲可能會導致新的可計費服務。  如需詳細資訊，請參閱 [SQL 資料倉儲價格](https://azure.microsoft.com/pricing/details/sql-data-warehouse/)。
>

### <a name="create-a-data-warehouse"></a>建立資料倉儲

1. 登入 hello [Azure 入口網站](https://portal.azure.com)。
2. 按一下 [新增] > [資料庫] > [SQL 資料倉儲]。

    ![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)

3. 填寫部署詳細資料

    **資料庫名稱**︰挑選您想要的名稱。 如果您有多個資料倉儲時，我們建議您的名稱包含詳細資料，例如 hello 區域中，環境中，例如*mydw uswest 1-測試*。

    **訂用帳戶**：您的 Azure 訂用帳戶

    **資源群組**：建立新的資源群組，或使用現有的資源群組。
    > [!NOTE]
    > 資源群組適合用來管理資源，例如界定存取控制和樣板化部署的範圍。 您可以[在此](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)深入了解 Azure 資源群組和最佳作法

    **來源**：空白資料庫

    **伺服器**： 您在建立選取 hello 伺服器[必要條件]。

    **定序**： 保留 hello 預設定序 SQL_Latin1_General_CP1_CI_AS。

    **選取 效能**： 我們建議您從 hello 標準 400DWU 開始。

4. 選擇**Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)

5. 耐心和等候您的資料倉儲 toodeploy ！ 這是正常的這個程序 tootake 幾分鐘的時間。 當資料倉儲就緒 toouse hello 入口網站會通知您。 

## <a name="connect-toosql-data-warehouse"></a>連接 tooSQL 資料倉儲

本教學課程會使用 SQL Server Management Studio (SSMS) tooconnect toohello 資料倉儲。 您可以透過這些支援的連接器連接 tooSQL 資料倉儲： ADO.NET、 JDBC、 ODBC 和 PHP。 請記住，非 Microsoft 支援工具的功能可能會受限。


### <a name="get-connection-information"></a>取得連線資訊

tooconnect tooyour 資料倉儲，您需要透過 hello 您在建立邏輯 SQL server tooconnect[必要條件]。

1. 從 hello 儀表板或搜尋您的資源中選取您的資料倉儲。

    ![SQL 資料倉儲儀表板](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. 尋找 hello hello 邏輯 SQL server 的完整名稱。

    ![選取伺服器名稱](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. 開啟 SSMS，並使用物件總管 中 tooconnect toothis 伺服器使用您在建立 hello 伺服器系統管理員認證[必要條件]

    ![以 SSMS 連線](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

如果一切正確，您現在應該連接的 tooyour 邏輯 SQL server。 因為您登入 hello 伺服器系統管理員，您可以連接 tooany hello 伺服器，包括 hello master 資料庫所裝載的資料庫。 

有一個伺服器系統管理員帳戶，而且它有 hello 大部分的權限的任何使用者。 請小心不 tooallow 太多人在您的組織 tooknow hello 的系統管理員密碼。 

您也可以擁有 Azure Active Directory 系統管理帳戶。 我們不提供 hello 詳細資料。 如果您想 toolearn 深入了解使用 Azure Active Directory 驗證時，請參閱[Azure AD 驗證](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)。

接下來，我們將探討建立其他登入和使用者。


## <a name="create-a-database-user"></a>建立資料庫使用者

在此步驟中，您建立使用者帳戶 tooaccess 資料倉儲。 我們也會示範如何 toogive 該使用者 hello 能力 toorun 查詢具有大量的記憶體和 CPU 資源。

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a>配置資源 tooqueries 資源類別的相關注意事項

- tookeep 資料安全，不要將生產資料庫上使用 hello 伺服器系統管理員 toorun 查詢。 它具有 hello 大部分的權限的任何使用者，並使用它 tooperform 使用者資料的作業會讓您的資料面臨風險。 此外，hello 伺服器系統管理員就是 tooperform 管理作業，因為它會執行作業只提供較小的配置的記憶體和 CPU 資源。 

- SQL 資料倉儲會使用預先定義的資料庫角色，稱為資源類別、 記憶體、 CPU 資源，以及並行插槽 toousers tooallocate 不同量。 每個使用者可隸屬 tooa 小型、 中型、 大型或超大資源類別。 hello 使用者的資源類別決定 hello 資源 hello 使用者有 toorun 查詢和載入作業。

- 最佳的資料壓縮 hello 使用者可能需要 tooload 與大型或超大型資源配置。 請[在此](./sql-data-warehouse-develop-concurrency.md#resource-classes)深入了解資源類別：

### <a name="create-an-account-that-can-control-a-database"></a>建立一個可以控制資料庫的帳戶

由於您目前在如 hello 伺服器系統管理員登您有權限 toocreate 登入和使用者。

1. 使用 SSMS 或另一個查詢用戶端，開啟對**主要**的新查詢。

    ![主要資料庫上的新增查詢](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![主要資料庫上的新增查詢 1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. 在 hello 查詢視窗中，執行此 T-SQL 命令 toocreate 名為 MedRCLogin 登入和名為 LoadingUser 使用者。 此登入可以連接 toohello 邏輯 SQL server。

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. 現在查詢 hello *SQL 資料倉儲資料庫*，建立資料庫使用者基礎 hello 登入建立 tooaccess 且 hello 資料庫上執行作業。

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. 提供 hello 資料庫使用者控制的權限 toohello 資料庫呼叫 NYT。 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > 如果您的資料庫名稱中連字號，以確定 toowrap 在方括號 ！ 
    >

### <a name="give-hello-user-medium-resource-allocations"></a>授與 hello 使用者中資源配置

1. 執行這個 T-SQL 命令 toomake 為稱為 mediumrc hello 中資源類別的成員。 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > 按一下[這裡](sql-data-warehouse-develop-concurrency.md#resource-classes)toolearn 更多關於並行與資源類別 ！ 
    >

2. Hello 新的認證與連線 toohello 邏輯伺服器

    ![使用新登入進行登入](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a>從 Azure blob 儲存體載入資料

現在您已經準備就緒 tooload 資料到資料倉儲。 此步驟說明如何 tooload New York City 趕赴從公用 Azure 儲存體的封包資料的 blob。 

- Tooload 資料到 SQL 資料倉儲是 toofirst 的常見方式移動 hello 資料 tooAzure blob 儲存體，，然後將它載入您的資料倉儲。 toomake 它更容易 toounderstand tooload，如何當我們有紐約計程車封包資料已裝載公用 Azure 儲存體 blob 中。 

- 供日後參考，toolearn 如何 tooget 資料 tooAzure blob 儲存體或它直接從您到 SQL 資料倉儲的來源，請參閱的 tooload hello[載入概觀](sql-data-warehouse-overview-load.md)。


### <a name="define-external-data"></a>定義外部資料

1. 建立建立主要金鑰。 您只需要 toocreate 每個資料庫主要金鑰。 

    ```sql
    CREATE MASTER KEY;
    ```

2. 定義 hello hello Azure blob 可包含 hello 計程車封包資料位置。  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. 定義 hello 外部檔案格式

    hello```CREATE EXTERNAL FILE FORMAT```命令是使用的 toospecify 包含 hello 外部資料的檔案格式。 其中包含以一或多個名為分隔符號字元分隔的文字。 針對示範用途，hello 計程車封包資料會儲存為未壓縮的資料，做為 gzip 壓縮資料。

    T-SQL 執行這些命令 toodefine 兩個不同的格式： 未壓縮和壓縮。

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  建立外部檔案格式的結構描述。 

    ```sql
    CREATE SCHEMA ext;
    ```
5. 建立 hello 外部資料表。 這些資料表會參考 Azure Blob 儲存體中儲存的資料。 執行下列 T-SQL 命令 toocreate hello 所有點 toohello Azure blob 我們先前在中定義之外部資料來源的多個外部資料表。

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a>從 Azure blob 儲存體的 hello 資料匯入。

SQL 資料倉儲支援稱為 CREATE TABLE AS SELECT (CTAS) 的重要陳述式。 這個陳述式建立新的資料表，根據 hello select 陳述式的結果。 hello 新的資料表有 hello 相同資料行和資料類型，如 hello hello 結果 select 陳述式。  這是適合用來 tooimport 來自資料到 SQL 資料倉儲的 Azure blob 儲存體。

1. 執行這個指令碼 tooimport 您的資料。

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. 檢視載入中的資料。

   您會載入數 GB 的資料，並將其壓縮成高效能的叢集資料行存放區索引。 執行下列查詢會使用動態管理檢視 (Dmv) tooshow hello 狀態 hello 負載 hello。 啟動之後 hello 查詢，請抓取咖啡和零食但 SQL 資料倉儲會有些困難。
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. 檢視所有系統查詢。

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. 輕鬆地看著資料順利載入至 Azure SQL 資料倉儲。

    ![看著資料載入](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a>改善查詢效能

有數種方式 tooimprove 查詢效能和 tooachieve hello 高速效能 SQL 資料倉儲的設計 tooprovide。  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a>請參閱 hello 的縮放比例，查詢效能的影響 

其中一種方式 tooimprove 查詢效能是 tooscale 資源變更您的資料倉儲的 hello DWU 服務層級。 每個服務等級的成本會往上增加，但您可以隨時調整回來或暫停資源。 

在此步驟中，您將會比較兩個不同 DWU 設定的效能。

首先，讓我們來調整關閉 too100 DWU，因此我們可以得到了解如何計算節點可能會執行本身的 hello 調整大小。

1. 移 toohello 入口網站，然後選取您的 SQL 資料倉儲。

2. 選取在 hello SQL 資料倉儲刀鋒視窗中的小數位數。 

    ![從入口網站調整 DW](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. 縮放列 too100 DWU hello 效能和儲存叫用。

    ![調整並儲存](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. 等候您的標尺作業 toofinish。

    > [!NOTE]
    > 變更 hello 小數位數時，無法執行查詢。 調整會**刪除**目前執行的查詢。 Hello 作業完成時，您可以重新加以啟動。
    >
    
5. 執行掃描作業上選取 hello 頂端百萬個項目 hello 的所有資料行的 hello 路線資料。 如果您積極式 toomove 上快速，則可以免費 tooselect 較少的資料列。 記下 hello 花的時間 toorun 這項作業。

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. 調整您的資料倉儲回 too400 DWU。 請記住，每個 100 DWU 新增另一個計算節點 tooyour Azure SQL 資料倉儲。

7. 再次執行查詢 hello ！ 您應該會發現顯著差異。 

    > [!NOTE]
    > 由於 hello 查詢傳回大量資料，執行 SSMS hello 機器 hello 頻寬可用性可能會造成效能瓶頸。 這會導致您看不到任何效能改善！

> [!NOTE]
> SQL 資料倉儲會使用大量平行處理。 掃描或數百萬個資料列上執行分析函式的查詢遇到 hello 真正強大的 Azure SQL 資料倉儲。
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a>查看對查詢效能的統計資料的 hello 效果

1. 執行查詢聯結 hello hello 路線資料表與日期資料表

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    因為它可以執行 hello 聯結前 SQL 資料倉儲 tooshuffle 資料，這項查詢需要一些時間。 聯結沒有 tooshuffle 資料所設計的 toojoin hello 資料散發的方式相同。 這是更深入的主題了。 

2. 統計資料會造成差異。 
3. Hello 聯結資料行上執行此陳述式 toocreate 統計資料。

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > SQL DW 不會自動管理您的統計資料。 統計資料對於查詢的效能很重要，因此強烈建議您建立和更新統計資料。
    > 
    > **您可以 hello 最大效益，到的資料行聯結，使用 hello 子句資料行找到和 GROUP BY 中的資料行中具有統計資料。**
    >

3. 再次執行必要條件的 hello 查詢，並觀察效能差異。 雖然無法以向上擴充為極端 hello 差異查詢的效能，您應該會注意到加速。 

## <a name="next-steps"></a>後續步驟

您現在已經準備就緒 tooquery 及探索。 請查看我們的最佳作法或提示。

如果您完成 hello 天，瀏覽您的執行個體請確定 toopause ！ 實際執行環境，您可以暫停並調整 toomeet 體驗龐大的節省您的業務需求。

![暫停](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a>實用內容

[並行和工作負載管理][]

[Azure SQL 資料倉儲最佳做法][]

[查詢監視][]

[建立大規模關聯式資料倉儲的 10 大最佳作法][]

[移轉資料 tooAzure SQL 資料倉儲][]

[並行和工作負載管理]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Azure SQL 資料倉儲最佳做法]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[查詢監視]: sql-data-warehouse-manage-monitor.md
[建立大規模關聯式資料倉儲的 10 大最佳作法]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[移轉資料 tooAzure SQL 資料倉儲]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[必要條件]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
