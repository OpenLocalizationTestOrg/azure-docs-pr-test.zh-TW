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
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="fd141-103">開始使用 Azure SQL Database 中的時態表</span><span class="sxs-lookup"><span data-stu-id="fd141-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="fd141-104">時態表是新的可程式性功能的 Azure SQL Database 可讓您 tootrack 和分析資料，而 hello 需要撰寫自訂程式碼中變更 hello 完整歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="fd141-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="fd141-105">時態表保持資料緊密相關的 tootime 內容，讓可以解譯的預存的事實為無效只在 hello 特定期間內。</span><span class="sxs-lookup"><span data-stu-id="fd141-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="fd141-106">時態表的這個屬性允許進行以有效時間為基礎的分析，並可從資料演進中取得獨到見解。</span><span class="sxs-lookup"><span data-stu-id="fd141-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="fd141-107">時態表案例</span><span class="sxs-lookup"><span data-stu-id="fd141-107">Temporal Scenario</span></span>
<span data-ttu-id="fd141-108">本文說明如何在應用程式案例中的 hello 步驟 tooutilize 時態表。</span><span class="sxs-lookup"><span data-stu-id="fd141-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="fd141-109">假設您要從頭開發新的網站或現有網站的使用者活動分析 tooextend tootrack 使用者活動。</span><span class="sxs-lookup"><span data-stu-id="fd141-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="fd141-110">在這個簡化的範例中，我們假設在一段時間期間的已瀏覽網頁 hello 數是需要 toobe 擷取，而且在 hello 網站資料庫裝載在 Azure SQL Database 上受監視的指標。</span><span class="sxs-lookup"><span data-stu-id="fd141-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="fd141-111">hello hello 的使用者活動的記錄分析的目的是 tooget 輸入 tooredesign 網站，而提供更好的體驗 hello 訪客。</span><span class="sxs-lookup"><span data-stu-id="fd141-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="fd141-112">hello 資料庫模型，此案例是非常簡單： 使用者活動公制表示使用單一整數欄位， **PageVisited**，並擷取以及 hello 使用者設定檔的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="fd141-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="fd141-113">此外，以時間為基礎的分析，您會保留一系列的資料列的每個使用者，其中每個資料列代表特定的使用者瀏覽特定的一段時間內的 hello 頁數。</span><span class="sxs-lookup"><span data-stu-id="fd141-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![結構描述](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="fd141-115">幸運的是，您不需要 tooput 任何工作在您的應用程式 toomaintain 此活動資訊。</span><span class="sxs-lookup"><span data-stu-id="fd141-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="fd141-116">使用時態表時，會自動化此程序-提供網站設計與 hello 資料分析本身的更多時間 toofocus 期間的完整彈性。</span><span class="sxs-lookup"><span data-stu-id="fd141-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="fd141-117">只有您唯一 toodo tooensure hello， **WebSiteInfo**資料表設定為[temporal 系統版本設定](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0)。</span><span class="sxs-lookup"><span data-stu-id="fd141-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="fd141-118">以下將說明在此案例中的 hello 確切步驟 tooutilize 時態表。</span><span class="sxs-lookup"><span data-stu-id="fd141-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="fd141-119">步驟 1︰將資料表設定為時態表</span><span class="sxs-lookup"><span data-stu-id="fd141-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="fd141-120">根據您要開始新的開發工作，還是升級現有的應用程式，您將會建立時態表，或透過新增時態屬性來修改現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="fd141-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="fd141-121">在一般情況下，您的案例可能會混用這兩個選項。</span><span class="sxs-lookup"><span data-stu-id="fd141-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="fd141-122">使用 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS)、[SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) 或其他任何 Transact-SQL 開發工具執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="fd141-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd141-123">建議您一律使用 hello 與更新 tooMicrosoft 同步處理最新版本的 Management Studio tooremain Azure 和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="fd141-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="fd141-124">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fd141-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="fd141-125">建立新資料表</span><span class="sxs-lookup"><span data-stu-id="fd141-125">Create new table</span></span>
<span data-ttu-id="fd141-126">使用操作功能表項目 「 新的系統版本設定資料表 」 在 SSMS 物件總管 tooopen hello 查詢編輯器中使用時態表的範本指令碼，然後使用 [指定值的範本參數] (Ctrl + Shift + M) toopopulate hello 範本：</span><span class="sxs-lookup"><span data-stu-id="fd141-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="fd141-128">在 SSDT 中，加入新項目 toohello 資料庫專案時選取了 「 暫存資料表 （系統建立版本） 」 範本。</span><span class="sxs-lookup"><span data-stu-id="fd141-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="fd141-129">會開啟資料表設計工具並啟用您 tooeasily 指定 hello 資料表配置：</span><span class="sxs-lookup"><span data-stu-id="fd141-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="fd141-131">您也可以建立的時態表藉由直接指定 hello TRANSACT-SQL 陳述式中 hello 下面範例所示。</span><span class="sxs-lookup"><span data-stu-id="fd141-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="fd141-132">請注意，hello 的每個時態表的必要項目是 hello 期間定義和 hello SYSTEM_VERSIONING 子句，與參考 tooanother 使用者資料表將會儲存歷程記錄資料列版本：</span><span class="sxs-lookup"><span data-stu-id="fd141-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

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

<span data-ttu-id="fd141-133">當您建立系統建立版本時態表時，會自動建立 hello 伴隨 hello 預設組態的歷程記錄資料表。</span><span class="sxs-lookup"><span data-stu-id="fd141-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="fd141-134">hello 預設記錄資料表包含已啟用頁面壓縮的 hello 期間資料行 （結尾、 開頭） 的叢集的索引 B 型樹狀目錄。</span><span class="sxs-lookup"><span data-stu-id="fd141-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="fd141-135">這個設定適合 hello 大部分的案例中使用時態表，特別是針對[資料稽核](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0)。</span><span class="sxs-lookup"><span data-stu-id="fd141-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="fd141-136">在此案例中，我們的目的是用 tooperform 以時間為基礎的趨勢分析一段較長的資料歷程記錄和更大的資料集，因此 hello 儲存體選擇 hello 歷程記錄資料表的非叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="fd141-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="fd141-137">叢集資料行存放區為分析查詢提供很好的壓縮和效能。</span><span class="sxs-lookup"><span data-stu-id="fd141-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="fd141-138">時態資料表讓您完全獨立 hello hello 目前和暫存資料表的彈性 tooconfigure 索引。</span><span class="sxs-lookup"><span data-stu-id="fd141-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="fd141-139">資料行存放區索引只可用在 hello premium 服務層中。</span><span class="sxs-lookup"><span data-stu-id="fd141-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="fd141-140">下列指令碼的 hello 顯示歷程記錄資料表上的預設索引可以是已變更的 toohello 叢集資料行存放區的方式：</span><span class="sxs-lookup"><span data-stu-id="fd141-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="fd141-141">時態表是以 hello 物件總管 中，以更容易識別，如 hello 特定圖示表示，雖然其歷程記錄資料表會顯示為子節點。</span><span class="sxs-lookup"><span data-stu-id="fd141-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="fd141-143">改變現有的資料表 tootemporal</span><span class="sxs-lookup"><span data-stu-id="fd141-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="fd141-144">我們要討論 hello 替代案例中的 hello WebsiteUserInfo 資料表已經存在，但不是設計的 tookeep 變更的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="fd141-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="fd141-145">在此情況下，您只可以擴充 hello 現有資料表 toobecome 時態 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="fd141-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

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

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="fd141-146">步驟 2：定期執行您的工作負載</span><span class="sxs-lookup"><span data-stu-id="fd141-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="fd141-147">時態表 hello 主要優點是，不需要 toochange 或調整您的網站在任何方式 tooperform 變更追蹤。</span><span class="sxs-lookup"><span data-stu-id="fd141-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="fd141-148">一旦建立時態表之後，當您每次對資料進行修改時，便會自動保存先前的資料列版本。</span><span class="sxs-lookup"><span data-stu-id="fd141-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="fd141-149">在這個特定案例的順序 tooleverage 自動變更追蹤，讓我們只更新資料行**PagesVisited**每次當使用者結束 her/his hello 網站上的工作階段：</span><span class="sxs-lookup"><span data-stu-id="fd141-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="fd141-150">請務必也 hello 實際作業發生時如何歷程記錄資料將保留供未來分析 toonotice hello 更新查詢，不需要 tooknow hello 確切時間。</span><span class="sxs-lookup"><span data-stu-id="fd141-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="fd141-151">Hello Azure SQL Database 會自動處理這兩個層面。</span><span class="sxs-lookup"><span data-stu-id="fd141-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="fd141-152">hello 下列圖表說明歷程記錄資料在每個更新的產生方式。</span><span class="sxs-lookup"><span data-stu-id="fd141-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="fd141-154">步驟 3︰執行歷史資料分析</span><span class="sxs-lookup"><span data-stu-id="fd141-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="fd141-155">現在當時態系統設定版本功能啟用時，您只需要一個查詢，就可以進行歷史資料分析。</span><span class="sxs-lookup"><span data-stu-id="fd141-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="fd141-156">在本文中，我們會提供解決常見的分析案例-toolearn 的一些範例所有的詳細資訊，請瀏覽以 hello 導入的各種選項[FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3)子句。</span><span class="sxs-lookup"><span data-stu-id="fd141-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="fd141-157">toosee hello 前 10 個使用者依 hello 數目為準，一小時，瀏覽的網頁執行此查詢：</span><span class="sxs-lookup"><span data-stu-id="fd141-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="fd141-158">您可以輕鬆地修改此查詢 tooanalyze hello 站台的查閱次數為準，一天前，一個月前，或在您想在 hello 過去任何時間點。</span><span class="sxs-lookup"><span data-stu-id="fd141-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="fd141-159">tooperform hello 前一天，下列範例使用 hello 基本的統計分析：</span><span class="sxs-lookup"><span data-stu-id="fd141-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

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

<span data-ttu-id="fd141-160">toosearch 內的活動特定使用者的一段時間，使用 hello CONTAINED IN 子句：</span><span class="sxs-lookup"><span data-stu-id="fd141-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="fd141-161">圖形視覺效果對於時態查詢特別方便，因為您可以以直覺方式，非常輕鬆地顯示趨勢和使用模式︰</span><span class="sxs-lookup"><span data-stu-id="fd141-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="fd141-163">不斷演進的資料表結構描述</span><span class="sxs-lookup"><span data-stu-id="fd141-163">Evolving table schema</span></span>
<span data-ttu-id="fd141-164">一般而言，您將需要 toochange hello 時態表結構描述，而您進行應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="fd141-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="fd141-165">因此，只需執行一般的 ALTER TABLE 陳述式和 Azure SQL Database 會適當地傳播變更 toohello 歷程記錄資料表。</span><span class="sxs-lookup"><span data-stu-id="fd141-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="fd141-166">hello 下列指令碼會示範如何加入追蹤的額外屬性：</span><span class="sxs-lookup"><span data-stu-id="fd141-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="fd141-167">同樣地，您可以在您的工作負載正在作用中時，變更資料行定義︰</span><span class="sxs-lookup"><span data-stu-id="fd141-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="fd141-168">最後，您可以移除您不再需要的資料行。</span><span class="sxs-lookup"><span data-stu-id="fd141-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="fd141-169">或者，使用最新[SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange 時態資料表結構描述，當您連接的 toohello 資料庫 （線上模式） 或做為 hello 資料庫專案 （離線模式） 的一部分。</span><span class="sxs-lookup"><span data-stu-id="fd141-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="fd141-170">控制歷史資料的保留期</span><span class="sxs-lookup"><span data-stu-id="fd141-170">Controlling retention of historical data</span></span>
<span data-ttu-id="fd141-171">使用系統建立版本時態表時，hello 歷程記錄資料表可能會增加 hello 資料庫大小比一般資料表。</span><span class="sxs-lookup"><span data-stu-id="fd141-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="fd141-172">大型且不斷成長的歷程記錄資料表可能會造成的問題 toopure 儲存成本，以及諸效能因於時態查詢。</span><span class="sxs-lookup"><span data-stu-id="fd141-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="fd141-173">因此，開發資料保留原則來管理 hello 歷程記錄資料表中的資料，是規劃及管理的每個時態表的 hello 生命週期的重要層面。</span><span class="sxs-lookup"><span data-stu-id="fd141-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="fd141-174">使用 Azure SQL Database，您有下列方法來管理歷程記錄資料 hello 時態表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="fd141-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="fd141-175">資料表分割</span><span class="sxs-lookup"><span data-stu-id="fd141-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="fd141-176">自訂清除指令碼</span><span class="sxs-lookup"><span data-stu-id="fd141-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="fd141-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd141-177">Next steps</span></span>
<span data-ttu-id="fd141-178">如需有關時態表的詳細資訊，請參閱 [MSDN 文件](https://msdn.microsoft.com/library/dn935015.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fd141-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="fd141-179">請瀏覽 Channel 9 toohear[真實客戶時態實作成功劇本](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions)和監看式[live 時態示範](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)。</span><span class="sxs-lookup"><span data-stu-id="fd141-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

