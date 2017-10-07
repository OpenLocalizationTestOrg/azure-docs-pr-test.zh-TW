---
title: "開始使用 Azure SQL Database 中的時態表 aaaGetting |Microsoft 文件"
description: "了解 tooget 如何開始使用 Azure SQL Database 中使用時態表。"
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a>開始使用 Azure SQL Database 中的時態表
時態表是新的可程式性功能的 Azure SQL Database 可讓您 tootrack 和分析資料，而 hello 需要撰寫自訂程式碼中變更 hello 完整歷程記錄。 時態表保持資料緊密相關的 tootime 內容，讓可以解譯的預存的事實為無效只在 hello 特定期間內。 時態表的這個屬性允許進行以有效時間為基礎的分析，並可從資料演進中取得獨到見解。

## <a name="temporal-scenario"></a>時態表案例
本文說明如何在應用程式案例中的 hello 步驟 tooutilize 時態表。 假設您要從頭開發新的網站或現有網站的使用者活動分析 tooextend tootrack 使用者活動。 在這個簡化的範例中，我們假設在一段時間期間的已瀏覽網頁 hello 數是需要 toobe 擷取，而且在 hello 網站資料庫裝載在 Azure SQL Database 上受監視的指標。 hello hello 的使用者活動的記錄分析的目的是 tooget 輸入 tooredesign 網站，而提供更好的體驗 hello 訪客。

hello 資料庫模型，此案例是非常簡單： 使用者活動公制表示使用單一整數欄位， **PageVisited**，並擷取以及 hello 使用者設定檔的基本資訊。 此外，以時間為基礎的分析，您會保留一系列的資料列的每個使用者，其中每個資料列代表特定的使用者瀏覽特定的一段時間內的 hello 頁數。

![結構描述](./media/sql-database-temporal-tables/AzureTemporal1.png)

幸運的是，您不需要 tooput 任何工作在您的應用程式 toomaintain 此活動資訊。 使用時態表時，會自動化此程序-提供網站設計與 hello 資料分析本身的更多時間 toofocus 期間的完整彈性。 只有您唯一 toodo tooensure hello， **WebSiteInfo**資料表設定為[temporal 系統版本設定](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0)。 以下將說明在此案例中的 hello 確切步驟 tooutilize 時態表。

## <a name="step-1-configure-tables-as-temporal"></a>步驟 1︰將資料表設定為時態表
根據您要開始新的開發工作，還是升級現有的應用程式，您將會建立時態表，或透過新增時態屬性來修改現有的資料表。 在一般情況下，您的案例可能會混用這兩個選項。 使用 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS)、[SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) 或其他任何 Transact-SQL 開發工具執行下列動作。

> [!IMPORTANT]
> 建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。 [更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。
> 
> 

### <a name="create-new-table"></a>建立新資料表
使用操作功能表項目 「 新的系統版本設定資料表 」 在 SSMS 物件總管 tooopen hello 查詢編輯器中使用時態表的範本指令碼，然後使用 [指定值的範本參數] (Ctrl + Shift + M) toopopulate hello 範本：

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

在 SSDT 中，加入新項目 toohello 資料庫專案時選取了 「 暫存資料表 （系統建立版本） 」 範本。 會開啟資料表設計工具並啟用您 tooeasily 指定 hello 資料表配置：

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

您也可以建立的時態表藉由直接指定 hello TRANSACT-SQL 陳述式中 hello 下面範例所示。 請注意，hello 的每個時態表的必要項目是 hello 期間定義和 hello SYSTEM_VERSIONING 子句，與參考 tooanother 使用者資料表將會儲存歷程記錄資料列版本：

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

當您建立系統建立版本時態表時，會自動建立 hello 伴隨 hello 預設組態的歷程記錄資料表。 hello 預設記錄資料表包含已啟用頁面壓縮的 hello 期間資料行 （結尾、 開頭） 的叢集的索引 B 型樹狀目錄。 這個設定適合 hello 大部分的案例中使用時態表，特別是針對[資料稽核](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0)。 

在此案例中，我們的目的是用 tooperform 以時間為基礎的趨勢分析一段較長的資料歷程記錄和更大的資料集，因此 hello 儲存體選擇 hello 歷程記錄資料表的非叢集資料行存放區索引。 叢集資料行存放區為分析查詢提供很好的壓縮和效能。 時態資料表讓您完全獨立 hello hello 目前和暫存資料表的彈性 tooconfigure 索引。 

> [!NOTE]
> 資料行存放區索引只可用在 hello premium 服務層中。
>

下列指令碼的 hello 顯示歷程記錄資料表上的預設索引可以是已變更的 toohello 叢集資料行存放區的方式：

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

時態表是以 hello 物件總管 中，以更容易識別，如 hello 特定圖示表示，雖然其歷程記錄資料表會顯示為子節點。

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a>改變現有的資料表 tootemporal
我們要討論 hello 替代案例中的 hello WebsiteUserInfo 資料表已經存在，但不是設計的 tookeep 變更的歷程記錄。 在此情況下，您只可以擴充 hello 現有資料表 toobecome 時態 hello 下列範例所示：

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a>步驟 2：定期執行您的工作負載
時態表 hello 主要優點是，不需要 toochange 或調整您的網站在任何方式 tooperform 變更追蹤。 一旦建立時態表之後，當您每次對資料進行修改時，便會自動保存先前的資料列版本。 

在這個特定案例的順序 tooleverage 自動變更追蹤，讓我們只更新資料行**PagesVisited**每次當使用者結束 her/his hello 網站上的工作階段：

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

請務必也 hello 實際作業發生時如何歷程記錄資料將保留供未來分析 toonotice hello 更新查詢，不需要 tooknow hello 確切時間。 Hello Azure SQL Database 會自動處理這兩個層面。 hello 下列圖表說明歷程記錄資料在每個更新的產生方式。

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a>步驟 3︰執行歷史資料分析
現在當時態系統設定版本功能啟用時，您只需要一個查詢，就可以進行歷史資料分析。 在本文中，我們會提供解決常見的分析案例-toolearn 的一些範例所有的詳細資訊，請瀏覽以 hello 導入的各種選項[FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3)子句。

toosee hello 前 10 個使用者依 hello 數目為準，一小時，瀏覽的網頁執行此查詢：

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

您可以輕鬆地修改此查詢 tooanalyze hello 站台的查閱次數為準，一天前，一個月前，或在您想在 hello 過去任何時間點。

tooperform hello 前一天，下列範例使用 hello 基本的統計分析：

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

toosearch 內的活動特定使用者的一段時間，使用 hello CONTAINED IN 子句：

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

圖形視覺效果對於時態查詢特別方便，因為您可以以直覺方式，非常輕鬆地顯示趨勢和使用模式︰

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a>不斷演進的資料表結構描述
一般而言，您將需要 toochange hello 時態表結構描述，而您進行應用程式開發。 因此，只需執行一般的 ALTER TABLE 陳述式和 Azure SQL Database 會適當地傳播變更 toohello 歷程記錄資料表。 hello 下列指令碼會示範如何加入追蹤的額外屬性：

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

同樣地，您可以在您的工作負載正在作用中時，變更資料行定義︰

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

最後，您可以移除您不再需要的資料行。

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

或者，使用最新[SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange 時態資料表結構描述，當您連接的 toohello 資料庫 （線上模式） 或做為 hello 資料庫專案 （離線模式） 的一部分。

## <a name="controlling-retention-of-historical-data"></a>控制歷史資料的保留期
使用系統建立版本時態表時，hello 歷程記錄資料表可能會增加 hello 資料庫大小比一般資料表。 大型且不斷成長的歷程記錄資料表可能會造成的問題 toopure 儲存成本，以及諸效能因於時態查詢。 因此，開發資料保留原則來管理 hello 歷程記錄資料表中的資料，是規劃及管理的每個時態表的 hello 生命週期的重要層面。 使用 Azure SQL Database，您有下列方法來管理歷程記錄資料 hello 時態表中的 hello:

* [資料表分割](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [自訂清除指令碼](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a>後續步驟
如需有關時態表的詳細資訊，請參閱 [MSDN 文件](https://msdn.microsoft.com/library/dn935015.aspx)。
請瀏覽 Channel 9 toohear[真實客戶時態實作成功劇本](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions)和監看式[live 時態示範](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)。

