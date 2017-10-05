---
title: "開始使用 Azure SQL Database 中的時態表 | Microsoft Docs"
description: "了解如何開始使用 Azure SQL Database 中的時態表。"
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
ms.openlocfilehash: d84db682089c65c2716d2d9bd92f7bc0ac47af27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="42ec4-103">開始使用 Azure SQL Database 中的時態表</span><span class="sxs-lookup"><span data-stu-id="42ec4-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="42ec4-104">時態表是 Azure SQL Database 的一個新的可程式性功能，可讓您追蹤和分析資料變更的完整歷程記錄，而不需要撰寫自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="42ec4-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you to track and analyze the full history of changes in your data, without the need for custom coding.</span></span> <span data-ttu-id="42ec4-105">時態表會保持資料與時間內容之間的密切關係，因此只有在特定期間內，才會將預存的事實解譯為有效。</span><span class="sxs-lookup"><span data-stu-id="42ec4-105">Temporal Tables keep data closely related to time context so that stored facts can be interpreted as valid only within the specific period.</span></span> <span data-ttu-id="42ec4-106">時態表的這個屬性允許進行以有效時間為基礎的分析，並可從資料演進中取得獨到見解。</span><span class="sxs-lookup"><span data-stu-id="42ec4-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="42ec4-107">時態表案例</span><span class="sxs-lookup"><span data-stu-id="42ec4-107">Temporal Scenario</span></span>
<span data-ttu-id="42ec4-108">本文說明在應用程式案例中使用時態表的步驟。</span><span class="sxs-lookup"><span data-stu-id="42ec4-108">This article illustrates the steps to utilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="42ec4-109">假設您想要從頭開始追蹤正在開發的新網站上的使用者活動，或您想要使用使用者活動分析擴充的現有網站上的使用者活動。</span><span class="sxs-lookup"><span data-stu-id="42ec4-109">Suppose that you want to track user activity on a new website that is being developed from scratch or on an existing website that you want to extend with user activity analytics.</span></span> <span data-ttu-id="42ec4-110">在這個簡化的範例中，我們假設在一段時間內瀏覽過的網頁數目是必須在裝載於 Azure SQL Database 的網站資料庫中擷取和監視的指標。</span><span class="sxs-lookup"><span data-stu-id="42ec4-110">In this simplified example, we assume that the number of visited web pages during a period of time is an indicator that needs to be captured and monitored in the website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="42ec4-111">使用者活動歷史分析的目標是要獲得重新設計網站的意見，並為訪客提供更好的經驗。</span><span class="sxs-lookup"><span data-stu-id="42ec4-111">The goal of the historical analysis of user activity is to get inputs to redesign website and provide better experience for the visitors.</span></span>

<span data-ttu-id="42ec4-112">此案例的資料庫模型非常簡單：使用者活動度量是以單一整數欄位 **PageVisited** 表示，而且會與使用者設定檔上的基本資訊一起被擷取。</span><span class="sxs-lookup"><span data-stu-id="42ec4-112">The database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on the user profile.</span></span> <span data-ttu-id="42ec4-113">此外，對於以時間為基礎的分析，您要為每個使用者保留一連串的資料列，其中每個資料列都代表特定的一段時間內特定使用者瀏覽過的頁數。</span><span class="sxs-lookup"><span data-stu-id="42ec4-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents the number of pages a particular user visited within a specific period of time.</span></span>

![結構描述](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="42ec4-115">幸運的是，您不需要在您的 app 上花太多精力，就可以維護此活動資訊。</span><span class="sxs-lookup"><span data-stu-id="42ec4-115">Fortunately, you do not need to put any effort in your app to maintain this activity information.</span></span> <span data-ttu-id="42ec4-116">您可以使用時態表，將此程序自動化：讓您在網站設計期間有完整的彈性以及更多的時間，得以將重點放在資料分析本身。</span><span class="sxs-lookup"><span data-stu-id="42ec4-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time to focus on the data analysis itself.</span></span> <span data-ttu-id="42ec4-117">您只需要確保將 **WebSiteInfo** 資料表設定為 [時態系統設定版本](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0)。</span><span class="sxs-lookup"><span data-stu-id="42ec4-117">The only thing you have to do is to ensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="42ec4-118">在此案例中使用時態表的確切步驟如下所述。</span><span class="sxs-lookup"><span data-stu-id="42ec4-118">The exact steps to utilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="42ec4-119">步驟 1︰將資料表設定為時態表</span><span class="sxs-lookup"><span data-stu-id="42ec4-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="42ec4-120">根據您要開始新的開發工作，還是升級現有的應用程式，您將會建立時態表，或透過新增時態屬性來修改現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="42ec4-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="42ec4-121">在一般情況下，您的案例可能會混用這兩個選項。</span><span class="sxs-lookup"><span data-stu-id="42ec4-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="42ec4-122">使用 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS)、[SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) 或其他任何 Transact-SQL 開發工具執行下列動作。</span><span class="sxs-lookup"><span data-stu-id="42ec4-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42ec4-123">建議您一律使用最新版本的 Management Studio 保持與 Microsoft Azure 及 SQL Database 更新同步。</span><span class="sxs-lookup"><span data-stu-id="42ec4-123">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="42ec4-124">[更新 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)。</span><span class="sxs-lookup"><span data-stu-id="42ec4-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="42ec4-125">建立新資料表</span><span class="sxs-lookup"><span data-stu-id="42ec4-125">Create new table</span></span>
<span data-ttu-id="42ec4-126">在 SSMS 的 [物件總管] 中使用內容功能表項目 [新系統設定版本的資料表] 開啟查詢編輯器與時態表範本指令碼，然後使用 [指定範本參數的值] \(Ctrl + Shift + M) 填入範本：</span><span class="sxs-lookup"><span data-stu-id="42ec4-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer to open the query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) to populate the template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="42ec4-128">在 SSDT 中，將新項目加入至資料庫專案時，選擇 [時態表 (系統設定版本)] 範本。</span><span class="sxs-lookup"><span data-stu-id="42ec4-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items to the database project.</span></span> <span data-ttu-id="42ec4-129">這將會開啟資料表設計工具，並讓您輕鬆地指定資料表配置︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-129">That will open table designer and enable you to easily specify the table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="42ec4-131">您也可以透過直接指定 Transact-SQL 陳述式來建立時態表，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="42ec4-131">You can also a create temporal table by specifying the Transact-SQL statements directly, as shown in the example below.</span></span> <span data-ttu-id="42ec4-132">請注意，每個時態表的必要元素為 PERIOD 定義以及可參照將儲存歷史資料列版本的另一個使用者資料表的 SYSTEM_VERSIONING 子句︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-132">Note that the mandatory elements of every temporal table are the PERIOD definition and the SYSTEM_VERSIONING clause with a reference to another user table that will store historical row versions:</span></span>

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

<span data-ttu-id="42ec4-133">當您建立系統設定版本的時態表時，會自動建立隨附預設組態的歷程記錄資料表。</span><span class="sxs-lookup"><span data-stu-id="42ec4-133">When you create system-versioned temporal table, the accompanying history table with the default configuration is automatically created.</span></span> <span data-ttu-id="42ec4-134">預設的歷程記錄資料表包含期間資料行 (結束、開始) 上啟用頁面壓縮的叢集 B 型樹狀目錄索引。</span><span class="sxs-lookup"><span data-stu-id="42ec4-134">The default history table contains a clustered B-tree index on the period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="42ec4-135">此組態適合使用時態表的大部分案例，特別是用於 [資料稽核](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0)。</span><span class="sxs-lookup"><span data-stu-id="42ec4-135">This configuration is optimal for the majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="42ec4-136">在此特殊案例中，我們的目標是針對一段較長的資料歷程記錄以及較大的資料集，執行以時間為基礎的趨勢分析，因此歷程記錄表格的儲存體選擇為叢集資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="42ec4-136">In this particular case, we aim to perform time-based trend analysis over a longer data history and with bigger data sets, so the storage choice for the history table is a clustered columnstore index.</span></span> <span data-ttu-id="42ec4-137">叢集資料行存放區為分析查詢提供很好的壓縮和效能。</span><span class="sxs-lookup"><span data-stu-id="42ec4-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="42ec4-138">時態表提供您完全獨立地設定目前資料表和時態表的索引的彈性。</span><span class="sxs-lookup"><span data-stu-id="42ec4-138">Temporal Tables give you the flexibility to configure indexes on the current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="42ec4-139">只有在進階服務層中才能使用資料行存放區索引。</span><span class="sxs-lookup"><span data-stu-id="42ec4-139">Columnstore indexes are only available in the premium service tier.</span></span>
>

<span data-ttu-id="42ec4-140">下列指令碼示範如何將歷程記錄資料表的預設索引變更為叢集資料行存放區︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-140">The following script shows how default index on history table can be changed to the clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="42ec4-141">時態表在 [物件總管] 中會以特定圖示表示，讓您更容易識別，而其歷程記錄資料表則會以子節點顯示。</span><span class="sxs-lookup"><span data-stu-id="42ec4-141">Temporal Tables are represented in the Object Explorer with the specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-to-temporal"></a><span data-ttu-id="42ec4-143">將現有的資料表變更為時態表</span><span class="sxs-lookup"><span data-stu-id="42ec4-143">Alter existing table to temporal</span></span>
<span data-ttu-id="42ec4-144">讓我們來看看替代案例，其中 WebsiteUserInfo 資料表已存在，但不是針對保留變更的歷程記錄而設計。</span><span class="sxs-lookup"><span data-stu-id="42ec4-144">Let’s cover the alternative scenario in which the WebsiteUserInfo table already exists, but was not designed to keep a history of changes.</span></span> <span data-ttu-id="42ec4-145">在此情況下，您只能擴充現有的資料表，使其成為時態表，如以下範例所示︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-145">In this case, you can simply extend the existing table to become temporal, as shown in the following example:</span></span>

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

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="42ec4-146">步驟 2：定期執行您的工作負載</span><span class="sxs-lookup"><span data-stu-id="42ec4-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="42ec4-147">時態表的主要優點是您不需要以任何方式變更或調整您的網站，就可以執行變更追蹤。</span><span class="sxs-lookup"><span data-stu-id="42ec4-147">The main advantage of Temporal Tables is that you do not need to change or adjust your website in any way to perform change tracking.</span></span> <span data-ttu-id="42ec4-148">一旦建立時態表之後，當您每次對資料進行修改時，便會自動保存先前的資料列版本。</span><span class="sxs-lookup"><span data-stu-id="42ec4-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="42ec4-149">若要為這個特定案例使用自動變更追蹤功能，我們只需要在每次使用者結束網站上的工作階段時，更新資料行 **PagesVisited** 即可︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-149">In order to leverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on the website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="42ec4-150">請務必注意，更新查詢不需要知道實際作業進行的時間，也不需要知道如何保留歷史資料以供未來分析之用。</span><span class="sxs-lookup"><span data-stu-id="42ec4-150">It is important to notice that the update query doesn’t need to know the exact time when the actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="42ec4-151">Azure SQL Database 會自動處理這兩方面。</span><span class="sxs-lookup"><span data-stu-id="42ec4-151">Both aspects are automatically handled by the Azure SQL Database.</span></span> <span data-ttu-id="42ec4-152">下圖說明如何在每次更新時產生歷程記錄資料。</span><span class="sxs-lookup"><span data-stu-id="42ec4-152">The following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="42ec4-154">步驟 3︰執行歷史資料分析</span><span class="sxs-lookup"><span data-stu-id="42ec4-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="42ec4-155">現在當時態系統設定版本功能啟用時，您只需要一個查詢，就可以進行歷史資料分析。</span><span class="sxs-lookup"><span data-stu-id="42ec4-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="42ec4-156">在本文中，我們將提供一些解決常見分析案例的範例。若要了解所有詳細資料，請瀏覽使用 [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) 子句所導入的各種選項。</span><span class="sxs-lookup"><span data-stu-id="42ec4-156">In this article, we will provide a few examples that address common analysis scenarios - to learn all details, explore various options introduced with the [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="42ec4-157">若要查看依瀏覽網頁次數排序的前 10 名使用者，請執行以下查詢︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-157">To see the top 10 users ordered by the number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="42ec4-158">您可以輕鬆地修改此查詢，以分析截至一天前、一個月前，或您希望的任何過去時間點的網站瀏覽記錄。</span><span class="sxs-lookup"><span data-stu-id="42ec4-158">You can easily modify this query to analyze the site visits as of a day ago, a month ago or at any point in the past you wish.</span></span>

<span data-ttu-id="42ec4-159">若要進行前一天的基本統計分析，請使用以下範例︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-159">To perform basic statistical analysis for the previous day, use the following example:</span></span>

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

<span data-ttu-id="42ec4-160">若要搜尋特定使用者在某段時間的活動，請使用 CONTAINED IN 子句︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-160">To search for activities of a specific user, within a period of time, use the CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="42ec4-161">圖形視覺效果對於時態查詢特別方便，因為您可以以直覺方式，非常輕鬆地顯示趨勢和使用模式︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="42ec4-163">不斷演進的資料表結構描述</span><span class="sxs-lookup"><span data-stu-id="42ec4-163">Evolving table schema</span></span>
<span data-ttu-id="42ec4-164">一般而言，您必須在開發 app 的同時，變更時態表結構描述。</span><span class="sxs-lookup"><span data-stu-id="42ec4-164">Typically, you will need to change the temporal table schema while you are doing app development.</span></span> <span data-ttu-id="42ec4-165">因此，只要執行一般 ALTER TABLE 陳述式，Azure SQL Database 就會適當地傳播歷程記錄資料表的變更。</span><span class="sxs-lookup"><span data-stu-id="42ec4-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes to the history table.</span></span> <span data-ttu-id="42ec4-166">下列指令碼示範如何新增要追蹤的其他屬性︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-166">The following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="42ec4-167">同樣地，您可以在您的工作負載正在作用中時，變更資料行定義︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase the length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="42ec4-168">最後，您可以移除您不再需要的資料行。</span><span class="sxs-lookup"><span data-stu-id="42ec4-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="42ec4-169">或者，當您連線到資料庫 (線上模式)，或您屬於資料庫專案的一部分 (離線模式) 時，使用最新的 [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) 變更時態表結構描述。</span><span class="sxs-lookup"><span data-stu-id="42ec4-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) to change temporal table schema while you are connected to the database (online mode) or as part of the database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="42ec4-170">控制歷史資料的保留期</span><span class="sxs-lookup"><span data-stu-id="42ec4-170">Controlling retention of historical data</span></span>
<span data-ttu-id="42ec4-171">透過系統設定版本的時態表，歷程記錄資料表可以將資料庫大小增加到超過一般資料表。</span><span class="sxs-lookup"><span data-stu-id="42ec4-171">With system-versioned temporal tables, the history table may increase the database size more than regular tables.</span></span> <span data-ttu-id="42ec4-172">一個大型且不斷成長的歷程記錄表格可能會因為單純的儲存體成本，以及對時態查詢效能所徵收的稅額而變成一個問題。</span><span class="sxs-lookup"><span data-stu-id="42ec4-172">A large and ever-growing history table can become an issue both due to pure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="42ec4-173">因此，開發資料保留原則來管理歷程記錄資料表中的資料是規劃及管理每個時態表生命週期的重要環節。</span><span class="sxs-lookup"><span data-stu-id="42ec4-173">Hence, developing a data retention policy for managing data in the history table is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="42ec4-174">使用 Azure SQL Database 時，您有下列方法可以管理時態表中的歷史資料︰</span><span class="sxs-lookup"><span data-stu-id="42ec4-174">With Azure SQL Database, you have the following approaches for managing historical data in the temporal table:</span></span>

* [<span data-ttu-id="42ec4-175">資料表分割</span><span class="sxs-lookup"><span data-stu-id="42ec4-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="42ec4-176">自訂清除指令碼</span><span class="sxs-lookup"><span data-stu-id="42ec4-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="42ec4-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42ec4-177">Next steps</span></span>
<span data-ttu-id="42ec4-178">如需有關時態表的詳細資訊，請參閱 [MSDN 文件](https://msdn.microsoft.com/library/dn935015.aspx)。</span><span class="sxs-lookup"><span data-stu-id="42ec4-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="42ec4-179">瀏覽 Channel 9，聽聽[真實客戶的時態表實作成功案例](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions)，並觀看[時態表的即時示範](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)。</span><span class="sxs-lookup"><span data-stu-id="42ec4-179">Visit Channel 9 to hear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

