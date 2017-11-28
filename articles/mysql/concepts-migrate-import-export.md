---
title: "適用於 MySQL 的 Azure 資料庫中的匯入與匯出 | Microsoft Docs"
description: "本文說明在適用於 MySQL 的 Azure 資料庫中，使用 MySQL Workbench 之類的工具匯入與匯出資料庫的常見方式。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 2164562af60442375b96a51f820a65d4d4a6f257
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a><span data-ttu-id="83ff5-103">使用匯入和匯出移轉您的 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="83ff5-103">Migrate your MySQL database by using import and export</span></span>
<span data-ttu-id="83ff5-104">本文說明使用 MySQL Workbench 將資料匯入與匯出適用於 MySQL 伺服器的 Azure 資料庫的兩個常見方式。</span><span class="sxs-lookup"><span data-stu-id="83ff5-104">This article explains two common approaches to importing and exporting data to an Azure Database for MySQL server by using MySQL Workbench.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="83ff5-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="83ff5-105">Before you begin</span></span>
<span data-ttu-id="83ff5-106">若要逐步執行本作法指南，您需要：</span><span class="sxs-lookup"><span data-stu-id="83ff5-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="83ff5-107">適用於 MySQL 伺服器的 Azure 資料庫，[使用 Azure 入口網站建立適用於 MySQL 伺服器的 Azure 資料庫](quickstart-create-mysql-server-database-using-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="83ff5-107">An Azure Database for MySQL server, by following [Create an Azure Database for MySQL server using Azure portal](quickstart-create-mysql-server-database-using-azure-portal.md).</span></span>
- <span data-ttu-id="83ff5-108">MySQL Workbench [下載](https://dev.mysql.com/downloads/workbench/)，或其他匯入與匯出的 MySQL 工具。</span><span class="sxs-lookup"><span data-stu-id="83ff5-108">MySQL Workbench [downloaded](https://dev.mysql.com/downloads/workbench/), or another MySQL tool to import and export.</span></span>

## <a name="use-common-tools"></a><span data-ttu-id="83ff5-109">使用一般工具</span><span class="sxs-lookup"><span data-stu-id="83ff5-109">Use common tools</span></span>
<span data-ttu-id="83ff5-110">使用一般工具 (例如 MySQL Workbench、Toad 或 Navicat) 從遠端連接，然後在適用於 MySQL 的 Azure 資料庫中匯入或匯出資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-110">Use common tools such as MySQL Workbench, Toad, or Navicat to remotely connect and import or export data into Azure Database for MySQL.</span></span> 

<span data-ttu-id="83ff5-111">在具有網際網路連線的用戶端電腦上使用這類工具，來連線到適用於 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="83ff5-111">Use such tools on your client machine with an Internet connection to connect to Azure Database for MySQL.</span></span> <span data-ttu-id="83ff5-112">使用 SSL 加密連線以獲得最佳安全性做法，如[在適用於 MySQL 的 Azure 資料庫中設定 SSL 連線能力](concepts-ssl-connection-security.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="83ff5-112">Use an SSL-encrypted connection for best security practices, as described in [Configure SSL connectivity in Azure Database for MySQL](concepts-ssl-connection-security.md).</span></span>

<span data-ttu-id="83ff5-113">在移轉到適用於 MySQL 的 Azure 資料庫時，您不需要將匯入和匯出檔案移至任何特定的雲端位置。</span><span class="sxs-lookup"><span data-stu-id="83ff5-113">You do not need to move your import and export files to any special cloud location when migrating to Azure Database for MySQL.</span></span> 

## <a name="create-a-database-on-the-azure-database-for-mysql-server"></a><span data-ttu-id="83ff5-114">在適用於 MySQL 伺服器的 Azure 資料庫上建立資料庫</span><span class="sxs-lookup"><span data-stu-id="83ff5-114">Create a database on the Azure Database for MySQL server</span></span>
<span data-ttu-id="83ff5-115">在您要移轉資料的適用於 MySQL 伺服器的 Azure 資料庫上建立空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="83ff5-115">Create an empty database on the Azure Database for MySQL server where you want to migrate the data.</span></span> <span data-ttu-id="83ff5-116">使用例如 MySQL Workbench、Toad 或 Navicat 的工具來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="83ff5-116">Use a tool such as MySQL Workbench, Toad, or Navicat to create the database.</span></span> <span data-ttu-id="83ff5-117">資料庫名稱可以與包含傾印資料的資料庫名稱相同，或者您可以建立名稱不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="83ff5-117">The database can have the same name as the database that contains the dumped data, or you can create a database with a different name.</span></span>

<span data-ttu-id="83ff5-118">若要連線，在適用於 MySQL 的 Azure 資料庫中的 [屬性] 窗格中找到連線資訊。</span><span class="sxs-lookup"><span data-stu-id="83ff5-118">To get connected, locate the connection information on the **Properties** pane in Azure Database for MySQL.</span></span>

![在 Azure 入口網站中尋找連線資訊](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

<span data-ttu-id="83ff5-120">將連線資訊新增至 MySQL Workbench。</span><span class="sxs-lookup"><span data-stu-id="83ff5-120">Add the connection information to MySQL Workbench.</span></span>

![MySQL Workbench 連接字串](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-to-use-import-and-export-techniques-instead-of-a-dump-and-restore"></a><span data-ttu-id="83ff5-122">判斷何時要使用匯入和匯出技術，而不是傾印和還原</span><span class="sxs-lookup"><span data-stu-id="83ff5-122">Determine when to use import and export techniques instead of a dump and restore</span></span>
<span data-ttu-id="83ff5-123">在下列案例中，使用 MySQL 工具將資料庫匯入與匯出 Azure MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="83ff5-123">Use MySQL tools to import and export databases into Azure MySQL Database in the following scenarios.</span></span> <span data-ttu-id="83ff5-124">在其他案例中，您可能反而會受益於使用[傾印和還原](concepts-migrate-dump-restore.md)方法。</span><span class="sxs-lookup"><span data-stu-id="83ff5-124">In other scenarios, you might benefit from using the [dump and restore](concepts-migrate-dump-restore.md) approach instead.</span></span> 

- <span data-ttu-id="83ff5-125">當您需要選擇性地選擇從現有 MySQL 資料庫匯入至 Azure MySQL 資料庫的一些資料表時，最好使用匯入和匯出技術。</span><span class="sxs-lookup"><span data-stu-id="83ff5-125">When you need to selectively choose a few tables to import from an existing MySQL database into Azure MySQL Database, it's best to use the import and export technique.</span></span>  <span data-ttu-id="83ff5-126">如此一來，您可以從移轉省略任何不必要的資料表，以節省時間和資源。</span><span class="sxs-lookup"><span data-stu-id="83ff5-126">By doing so, you can omit any unneeded tables from the migration to save time and resources.</span></span> <span data-ttu-id="83ff5-127">例如，搭配使用 `--include-tables` 或 `--exclude-tables` 參數與 [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) 以及搭配使用 `--tables` 參數與 [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables)。</span><span class="sxs-lookup"><span data-stu-id="83ff5-127">For example, use the `--include-tables` or `--exclude-tables` switch with [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) and the `--tables` switch with [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables).</span></span>
- <span data-ttu-id="83ff5-128">移動資料表以外的資料庫物件時，明確建立這些項目。</span><span class="sxs-lookup"><span data-stu-id="83ff5-128">When you're moving the database objects other than tables, explicitly create those.</span></span> <span data-ttu-id="83ff5-129">包含限制式 (主索引鍵、外部索引鍵、索引)、檢視、函式、程序、觸發程序和其他您想要移轉的資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="83ff5-129">Include constraints (primary key, foreign key, indexes), views, functions, procedures, triggers, and any other database objects that you want to migrate.</span></span>
- <span data-ttu-id="83ff5-130">當您從 MySQL 資料庫以外的外部資料來源移轉資料時，建立一般檔案，並且使用 [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html) 來匯入它們。</span><span class="sxs-lookup"><span data-stu-id="83ff5-130">When you're migrating data from external data sources other than a MySQL database, create flat files and import them by using [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html).</span></span>

<span data-ttu-id="83ff5-131">將資料載入至適用於 MySQL 的 Azure 資料庫時，請確定資料庫中的所有資料表都使用 InnoDB 儲存引擎。</span><span class="sxs-lookup"><span data-stu-id="83ff5-131">Make sure that all tables in the database use the InnoDB storage engine when you're loading data into Azure Database for MySQL.</span></span> <span data-ttu-id="83ff5-132">適用於 MySQL 的 Azure 資料庫僅支援 InnoDB 儲存引擎，因此不支援其他儲存引擎。</span><span class="sxs-lookup"><span data-stu-id="83ff5-132">Azure Database for MySQL supports only the InnoDB storage engine, so it doesn't support alternative storage engines.</span></span> <span data-ttu-id="83ff5-133">如果您的資料表需要其他儲存引擎，請確定將它們轉換成 InnoDB 引擎格式，然後再移轉至適用於 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="83ff5-133">If your tables require alternative storage engines, be sure to convert them to use the InnoDB engine format before the migration to Azure Database for MySQL.</span></span> 

<span data-ttu-id="83ff5-134">例如，如果您有使用 MyISAM 引擎的 WordPress 或 Web 應用程式，先將資料移轉至 InnoDB 資料表來轉換資料表。</span><span class="sxs-lookup"><span data-stu-id="83ff5-134">For example, if you have a WordPress or web app that uses the MyISAM engine, first convert the tables by migrating the data into InnoDB tables.</span></span> <span data-ttu-id="83ff5-135">然後還原至適用於 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="83ff5-135">Then restore to Azure Database for MySQL.</span></span> <span data-ttu-id="83ff5-136">使用子句 `ENGINE=INNODB` 以設定引擎來建立資料表，然後在移轉之前將資料傳送到相容的資料表。</span><span class="sxs-lookup"><span data-stu-id="83ff5-136">Use the clause `ENGINE=INNODB` to set the engine for creating a table, and then transfer the data into the compatible table before the migration.</span></span> 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a><span data-ttu-id="83ff5-137">匯入和匯出的效能建議</span><span class="sxs-lookup"><span data-stu-id="83ff5-137">Performance recommendations for import and export</span></span>
-   <span data-ttu-id="83ff5-138">載入資料之前先建立叢集索引和主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="83ff5-138">Create clustered indexes and primary keys before loading data.</span></span> <span data-ttu-id="83ff5-139">以主索引鍵的順序載入資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-139">Load data in primary key order.</span></span> 
-   <span data-ttu-id="83ff5-140">延遲建立次要索引，直到載入資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-140">Delay creation of secondary indexes until after data is loaded.</span></span> <span data-ttu-id="83ff5-141">載入之後建立所有次要索引。</span><span class="sxs-lookup"><span data-stu-id="83ff5-141">Create all secondary indexes after loading.</span></span> 
-   <span data-ttu-id="83ff5-142">載入之前停用外部索引鍵限制式。</span><span class="sxs-lookup"><span data-stu-id="83ff5-142">Disable foreign key constraints before loading.</span></span> <span data-ttu-id="83ff5-143">停用外部索引鍵檢查會提供顯著的效能提升。</span><span class="sxs-lookup"><span data-stu-id="83ff5-143">Disabling foreign key checks provides significant performance gains.</span></span> <span data-ttu-id="83ff5-144">啟用限制式並且確認載入之後的資料，以確保參考完整性。</span><span class="sxs-lookup"><span data-stu-id="83ff5-144">Enable the constraints and verify the data after the load to ensure referential integrity.</span></span>
-   <span data-ttu-id="83ff5-145">平行載入資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-145">Load data in parallel.</span></span> <span data-ttu-id="83ff5-146">避免會導致您達到資源限制的太多平行處理原則，以及使用 Azure 入口網站中可用的計量監視資源。</span><span class="sxs-lookup"><span data-stu-id="83ff5-146">Avoid too much parallelism that would cause you to hit a resource limit, and monitor resources by using the metrics available in the Azure portal.</span></span> 
-   <span data-ttu-id="83ff5-147">適當時使用資料分割資料表。</span><span class="sxs-lookup"><span data-stu-id="83ff5-147">Use partitioned tables when appropriate.</span></span>

## <a name="import-and-export-by-using-mysql-workbench"></a><span data-ttu-id="83ff5-148">使用 MySQL Workbench 匯入和匯出</span><span class="sxs-lookup"><span data-stu-id="83ff5-148">Import and export by using MySQL Workbench</span></span>
<span data-ttu-id="83ff5-149">有兩種方式可在 MySQL Workbench 中匯出和匯入資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-149">There are two ways to export and import data in MySQL Workbench.</span></span> <span data-ttu-id="83ff5-150">每一種適用於不同用途。</span><span class="sxs-lookup"><span data-stu-id="83ff5-150">Each serves a different purpose.</span></span> 

### <a name="table-data-export-and-import-wizards-from-the-object-browsers-context-menu"></a><span data-ttu-id="83ff5-151">物件瀏覽器快顯功能表的資料表資料匯出與匯入精靈</span><span class="sxs-lookup"><span data-stu-id="83ff5-151">Table data export and import wizards from the object browser's context menu</span></span>
![物件瀏覽器之快顯功能表上的 MySQL Workbench 精靈](./media/concepts-migrate-import-export/p1.png)

<span data-ttu-id="83ff5-153">資料表資料的精靈支援使用 CSV 和 JSON 檔案的匯入和匯出作業。</span><span class="sxs-lookup"><span data-stu-id="83ff5-153">The wizards for table data support import and export operations by using CSV and JSON files.</span></span> <span data-ttu-id="83ff5-154">它們包含數個設定選項，例如分隔符號、資料行選取和編碼選取項目。</span><span class="sxs-lookup"><span data-stu-id="83ff5-154">They include several configuration options, such as separators, column selection, and encoding selection.</span></span> <span data-ttu-id="83ff5-155">您可以對本機或遠端連線的 MySQL 伺服器執行每個精靈。</span><span class="sxs-lookup"><span data-stu-id="83ff5-155">You can perform each wizard against local or remotely connected MySQL servers.</span></span> <span data-ttu-id="83ff5-156">匯入動作包括資料表、資料行和類型對應。</span><span class="sxs-lookup"><span data-stu-id="83ff5-156">The import action includes table, column, and type mapping.</span></span> 

<span data-ttu-id="83ff5-157">您可以從物件瀏覽器的快顯功能表以滑鼠右鍵按一下資料表，來存取這些精靈。</span><span class="sxs-lookup"><span data-stu-id="83ff5-157">You can access these wizards from the object browser's context menu by right-clicking a table.</span></span> <span data-ttu-id="83ff5-158">然後選擇 [資料表資料匯出精靈] 或 [資料表資料匯入精靈]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-158">Then choose either **Table Data Export Wizard** or **Table Data Import Wizard**.</span></span> 

#### <a name="table-data-export-wizard"></a><span data-ttu-id="83ff5-159">資料表資料匯出精靈</span><span class="sxs-lookup"><span data-stu-id="83ff5-159">Table Data Export Wizard</span></span>
<span data-ttu-id="83ff5-160">下列範例會將資料表匯出至 CSV 檔案：</span><span class="sxs-lookup"><span data-stu-id="83ff5-160">The following example exports the table to a CSV file:</span></span> 
1. <span data-ttu-id="83ff5-161">以滑鼠右鍵按一下要匯出之資料庫的資料表。</span><span class="sxs-lookup"><span data-stu-id="83ff5-161">Right-click the table of the database to be exported.</span></span> 
2. <span data-ttu-id="83ff5-162">選取 [資料表資料匯出精靈]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-162">Select **Table Data Export Wizard**.</span></span> <span data-ttu-id="83ff5-163">選取要匯出的資料行、資料列位移 (如果有的話) 和計數 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="83ff5-163">Select the columns to be exported, row offset (if any), and count (if any).</span></span> 
3. <span data-ttu-id="83ff5-164">在 [選取要匯出的資料] 分頁上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-164">On the **Select data for export** page, click **Next**.</span></span> <span data-ttu-id="83ff5-165">選取檔案路徑、CSV 或 JSON 檔案類型。</span><span class="sxs-lookup"><span data-stu-id="83ff5-165">Select the file path, CSV, or JSON file type.</span></span> <span data-ttu-id="83ff5-166">同時選取行分隔符號、字串封入方法和欄位分隔符號。</span><span class="sxs-lookup"><span data-stu-id="83ff5-166">Also select the line separator, method of enclosing strings, and field separator.</span></span> 
4. <span data-ttu-id="83ff5-167">在 [選取輸出檔案位置] 分頁上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-167">On the **Select output file location** page, click **Next**.</span></span> 
5. <span data-ttu-id="83ff5-168">在 [匯出資料] 分頁上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-168">On the **Export data** page, click **Next**.</span></span>

#### <a name="table-data-import-wizard"></a><span data-ttu-id="83ff5-169">資料表資料匯入精靈</span><span class="sxs-lookup"><span data-stu-id="83ff5-169">Table Data Import Wizard</span></span>
<span data-ttu-id="83ff5-170">下列範例會從 CSV 檔案匯入資料表：</span><span class="sxs-lookup"><span data-stu-id="83ff5-170">The following example imports the table from a CSV file:</span></span>
1. <span data-ttu-id="83ff5-171">以滑鼠右鍵按一下要匯入之資料庫的資料表。</span><span class="sxs-lookup"><span data-stu-id="83ff5-171">Right-click the table of the database to be imported.</span></span> 
2. <span data-ttu-id="83ff5-172">瀏覽並選取要匯入的 CSV 檔案，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-172">Browse to and select the CSV file to be imported, and then click **Next**.</span></span> 
3. <span data-ttu-id="83ff5-173">選取目的地資料表 (新的或現有的)、選取或取消選取 [匯入前截斷資料表] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="83ff5-173">Select the destination table (new or existing), and select or clear the **Truncate table before import** check box.</span></span> <span data-ttu-id="83ff5-174">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="83ff5-174">Click **Next**.</span></span>
4. <span data-ttu-id="83ff5-175">選取編碼方式和要匯入的資料行，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-175">Select encoding and the columns to be imported, and then click **Next**.</span></span> 
5. <span data-ttu-id="83ff5-176">在 [匯入資料] 分頁上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-176">On the **Import data** page, click **Next**.</span></span> <span data-ttu-id="83ff5-177">精靈會據以匯入資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-177">The wizard imports the data accordingly.</span></span>

### <a name="sql-data-export-and-import-wizards-from-the-navigator-pane"></a><span data-ttu-id="83ff5-178">從導覽器窗格存取 SQL 資料匯出和匯入精靈</span><span class="sxs-lookup"><span data-stu-id="83ff5-178">SQL data export and import wizards from the Navigator pane</span></span>
<span data-ttu-id="83ff5-179">使用精靈，匯出或匯入從 MySQL Workbench 或 mysqldump 命令產生的 SQL。</span><span class="sxs-lookup"><span data-stu-id="83ff5-179">Use a wizard to export or import SQL generated from MySQL Workbench or generated from the mysqldump command.</span></span> <span data-ttu-id="83ff5-180">從 [導覽器] 窗格或從主功能表選取 [伺服器]，來存取這些精靈。</span><span class="sxs-lookup"><span data-stu-id="83ff5-180">Access these wizards from the **Navigator** pane or by selecting **Server** from the main menu.</span></span> <span data-ttu-id="83ff5-181">然後選取 [資料匯出] 或 [資料匯入]。</span><span class="sxs-lookup"><span data-stu-id="83ff5-181">Then select **Data Export** or **Data Import**.</span></span> 

#### <a name="data-export"></a><span data-ttu-id="83ff5-182">資料匯出</span><span class="sxs-lookup"><span data-stu-id="83ff5-182">Data Export</span></span>
![使用導覽器窗格的 MySQL Workbench 資料匯出](./media/concepts-migrate-import-export/p2.png)

<span data-ttu-id="83ff5-184">您可以使用 [資料匯出] 索引標籤，匯出您的 MySQL 資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-184">You can use the **Data Export** tab to export your MySQL data.</span></span> 
1. <span data-ttu-id="83ff5-185">選取每個您想要匯出的結構描述、選擇性地從每個結構描述中選取特定的結構描述物件/資料表，然後產生匯出。</span><span class="sxs-lookup"><span data-stu-id="83ff5-185">Select each schema that you want to export, optionally choose specific schema objects/tables from each schema, and generate the export.</span></span> <span data-ttu-id="83ff5-186">設定選項包含匯出到專案資料夾或自封式 SQL 檔案、傾印儲存的常式和事件，或略過資料表資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-186">Configuration options include export to a project folder or self-contained SQL file, dump stored routines and events, or skip table data.</span></span> 
 
   <span data-ttu-id="83ff5-187">或者，在 SQL 編輯器中，使用 [匯出結果集]，將特定的結果集匯出為另一種格式，例如 CSV、JSON、HTML 和 XML。</span><span class="sxs-lookup"><span data-stu-id="83ff5-187">Alternatively, use **Export a Result Set** to export a specific result set in the SQL editor to another format, such as CSV, JSON, HTML, and XML.</span></span> 
3. <span data-ttu-id="83ff5-188">選取要匯出的資料庫物件，並設定相關選項。</span><span class="sxs-lookup"><span data-stu-id="83ff5-188">Select the database objects to export, and configure the related options.</span></span>
4. <span data-ttu-id="83ff5-189">按一下 [重新整理] 以載入目前的物件。</span><span class="sxs-lookup"><span data-stu-id="83ff5-189">Click **Refresh** to load the current objects.</span></span>
5. <span data-ttu-id="83ff5-190">選擇性開啟 [進階選項] 索引標籤，以調整匯出作業。</span><span class="sxs-lookup"><span data-stu-id="83ff5-190">Optionally, open the **Advanced Options** tab to refine the export operation.</span></span> <span data-ttu-id="83ff5-191">例如，新增資料表鎖定、使用 replace 而不是 insert 陳述式，以及使用反引號字元將識別項括起來。</span><span class="sxs-lookup"><span data-stu-id="83ff5-191">For example, add table locks, use replace instead of insert statements, and quote identifiers with backtick characters.</span></span>
6. <span data-ttu-id="83ff5-192">按一下 [開始匯出] 開始匯出程序。</span><span class="sxs-lookup"><span data-stu-id="83ff5-192">Click **Start Export** to begin the export process.</span></span>


#### <a name="data-import"></a><span data-ttu-id="83ff5-193">資料匯入</span><span class="sxs-lookup"><span data-stu-id="83ff5-193">Data Import</span></span>
![使用管理導覽器的 MySQL Workbench 資料匯入](./media/concepts-migrate-import-export/p3.png)

<span data-ttu-id="83ff5-195">您可以使用 [資料匯入] 索引標籤，匯入或還原來自資料匯出作業或是來自 mysqldump 命令的已匯出資料。</span><span class="sxs-lookup"><span data-stu-id="83ff5-195">You can use the **Data Import** tab to import or restore exported data from the data export operation or from the mysqldump command.</span></span> 
1. <span data-ttu-id="83ff5-196">選擇專案資料夾或自封式 SQL 檔案、選擇將匯入的結構描述，或選擇 [新增] 來定義新的結構描述。</span><span class="sxs-lookup"><span data-stu-id="83ff5-196">Choose the project folder or self-contained SQL file, choose the schema to import into, or choose **New** to define a new schema.</span></span> 
2. <span data-ttu-id="83ff5-197">按一下 [開始匯入] 開始匯入程序。</span><span class="sxs-lookup"><span data-stu-id="83ff5-197">Click **Start Import** to begin the import process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83ff5-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="83ff5-198">Next steps</span></span>
<span data-ttu-id="83ff5-199">至於另一個移轉方法，請參閱[在適用於 MySQL 的 Azure 資料庫中使用傾印和還原來移轉 MySQL 資料庫](concepts-migrate-dump-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="83ff5-199">As another migration approach, read [Migrate your MySQL database using dump and restore in Azure Database for MySQL](concepts-migrate-dump-restore.md).</span></span> 
