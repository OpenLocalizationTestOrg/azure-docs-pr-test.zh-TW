---
title: "aaaBuild 並最佳化資料表，以便快速平行資料匯入到 Azure VM 上的 SQL Server |Microsoft 文件"
description: "使用 SQL 資料分割資料表平行處理大量資料匯入"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="62d5d-103">使用 SQL 資料分割資料表平行處理大量資料匯入</span><span class="sxs-lookup"><span data-stu-id="62d5d-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="62d5d-104">本文件說明如何 toobuild 資料分割進行快速平行大量匯入資料 tooa SQL Server 資料庫的資料表。</span><span class="sxs-lookup"><span data-stu-id="62d5d-104">This document describes how toobuild partitioned tables for fast parallel bulk importing of data tooa SQL Server database.</span></span> <span data-ttu-id="62d5d-105">巨量資料載入/transfer tooa SQL database 匯入資料 toohello SQL DB 和後續查詢，可以使用來改善*分割資料表和檢視表*。</span><span class="sxs-lookup"><span data-stu-id="62d5d-105">For big data loading/transfer tooa SQL database, importing data toohello SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="62d5d-106">建立新的資料庫和一組檔案群組</span><span class="sxs-lookup"><span data-stu-id="62d5d-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="62d5d-107">[建立新的資料庫](https://technet.microsoft.com/library/ms176061.aspx) (如果尚不存在)。</span><span class="sxs-lookup"><span data-stu-id="62d5d-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="62d5d-108">將資料庫檔案群組 toohello 資料庫會保留資料分割的 hello 實體檔案。這可以透過[CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx)如果是新或[ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx)如果 hello 資料庫已經存在。</span><span class="sxs-lookup"><span data-stu-id="62d5d-108">Add database filegroups toohello database which will hold hello partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if hello database exists already.</span></span>
* <span data-ttu-id="62d5d-109">新增一或多個檔案 （如有需要） tooeach 資料庫檔案群組。</span><span class="sxs-lookup"><span data-stu-id="62d5d-109">Add one or more files (as needed) tooeach database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="62d5d-110">指定 hello 目標檔案群組，其中包含此資料分割和 hello 實體資料庫檔案名稱的資料儲存 hello 檔案群組資料。</span><span class="sxs-lookup"><span data-stu-id="62d5d-110">Specify hello target filegroup which holds data for this partition and hello physical database file name(s) where hello filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="62d5d-111">hello 下列範例會建立新的資料庫具有三個主要的 hello 和包含在每一個實體檔案的記錄檔群組以外的檔案群組。</span><span class="sxs-lookup"><span data-stu-id="62d5d-111">hello following example creates a new database with three filegroups other than hello primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="62d5d-112">hello 資料庫檔案建立在 hello 預設 SQL Server Data 資料夾中，為 hello SQL Server 執行個體中設定。</span><span class="sxs-lookup"><span data-stu-id="62d5d-112">hello database files are created in hello default SQL Server Data folder, as configured in hello SQL Server instance.</span></span> <span data-ttu-id="62d5d-113">如需 hello 預設檔案位置的詳細資訊，請參閱[檔案位置的預設和具名執行個體的 SQL Server](https://msdn.microsoft.com/library/ms143547.aspx)。</span><span class="sxs-lookup"><span data-stu-id="62d5d-113">For more information about hello default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="62d5d-114">建立資料分割資料表</span><span class="sxs-lookup"><span data-stu-id="62d5d-114">Create a partitioned table</span></span>
<span data-ttu-id="62d5d-115">建立根據 toohello 資料結構描述、 對應的 toohello hello 先前步驟中建立的資料庫檔案群組的資料分割的資料表。</span><span class="sxs-lookup"><span data-stu-id="62d5d-115">Create partitioned table(s) according toohello data schema, mapped toohello database filegroups created in hello previous step.</span></span> <span data-ttu-id="62d5d-116">大量匯入資料時 toohello 分割資料表，記錄會分配給 hello 根據 tooa 分割區配置的檔案群組，如下所述。</span><span class="sxs-lookup"><span data-stu-id="62d5d-116">When data is bulk imported toohello partitioned table(s), records will be distributed among hello filegroups according tooa partition scheme, as described below.</span></span>

<span data-ttu-id="62d5d-117">**toocreate 磁碟分割表格，您要：**</span><span class="sxs-lookup"><span data-stu-id="62d5d-117">**toocreate a partition table, you need to:**</span></span>

* <span data-ttu-id="62d5d-118">[建立資料分割函數](https://msdn.microsoft.com/library/ms187802.aspx)其定義的界限值/toobe hello 範圍包含在每個個別資料分割資料表，例如 toolimit 依月份的資料分割 (某些\_datetime\_欄位) hello 年 2013年:</span><span class="sxs-lookup"><span data-stu-id="62d5d-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines hello range of values/boundaries toobe included in each individual partition table, e.g., toolimit partitions by month(some\_datetime\_field) in hello year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="62d5d-119">[建立資料分割配置](https://msdn.microsoft.com/library/ms179854.aspx)例如對應 hello 資料分割函數 tooa 實體檔案群組中，每個資料分割範圍：</span><span class="sxs-lookup"><span data-stu-id="62d5d-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in hello partition function tooa physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="62d5d-120">tooverify hello 範圍，實際上是在每個資料分割相應 toohello 函式/配置，請執行下列查詢的 hello:</span><span class="sxs-lookup"><span data-stu-id="62d5d-120">tooverify hello ranges in effect in each partition according toohello function/scheme, run hello following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="62d5d-121">[建立分割區的資料表](https://msdn.microsoft.com/library/ms174979.aspx)(s)，根據 tooyour 資料結構描述，並指定 hello 磁碟分割配置和條件約束欄位使用 toopartition hello 資料表，例如：</span><span class="sxs-lookup"><span data-stu-id="62d5d-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according tooyour data schema, and specify hello partition scheme and constraint field used toopartition hello table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="62d5d-122">如需詳細資訊，請參閱 [建立分割區資料表及索引](https://msdn.microsoft.com/library/ms188730.aspx)。</span><span class="sxs-lookup"><span data-stu-id="62d5d-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a><span data-ttu-id="62d5d-123">針對每個個別資料分割資料表的大量匯入 hello 資料</span><span class="sxs-lookup"><span data-stu-id="62d5d-123">Bulk import hello data for each individual partition table</span></span>
* <span data-ttu-id="62d5d-124">您可以使用 BCP、BULK INSERT 或其他方法，例如 [SQL Server 移轉精靈](http://sqlazuremw.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="62d5d-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="62d5d-125">所提供的 hello 範例會使用 hello BCP 方法。</span><span class="sxs-lookup"><span data-stu-id="62d5d-125">hello example provided uses hello BCP method.</span></span>
* <span data-ttu-id="62d5d-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange 交易記錄的記錄，例如配置 tooBULK_LOGGED toominimize 負擔：</span><span class="sxs-lookup"><span data-stu-id="62d5d-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange transaction logging scheme tooBULK_LOGGED toominimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="62d5d-127">tooexpedite 資料載入，啟動 hello 大量匯入作業，以平行方式。</span><span class="sxs-lookup"><span data-stu-id="62d5d-127">tooexpedite data loading, launch hello bulk import operations in parallel.</span></span> <span data-ttu-id="62d5d-128">如需加速將巨量資料大量匯入 SQL Server 資料庫的提示，請參閱 [載入 1 TB 的時間少於 1 小時](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx)(英文)。</span><span class="sxs-lookup"><span data-stu-id="62d5d-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="62d5d-129">hello 下列 PowerShell 指令碼是載入使用 BCP 的平行處理資料的範例。</span><span class="sxs-lookup"><span data-stu-id="62d5d-129">hello following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a><span data-ttu-id="62d5d-130">建立索引 toooptimize 聯結和查詢效能</span><span class="sxs-lookup"><span data-stu-id="62d5d-130">Create indexes toooptimize joins and query performance</span></span>
* <span data-ttu-id="62d5d-131">如果您將會從多個資料表來擷取模型的資料，建立索引 hello 聯結索引鍵上 tooimprove hello 聯結的效能。</span><span class="sxs-lookup"><span data-stu-id="62d5d-131">If you will extract data for modeling from multiple tables, create indexes on hello join keys tooimprove hello join performance.</span></span>
* <span data-ttu-id="62d5d-132">[建立索引](https://technet.microsoft.com/library/ms188783.aspx)（叢集或非叢集） 目標 hello 相同的檔案群組，每個分割區，例如：</span><span class="sxs-lookup"><span data-stu-id="62d5d-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting hello same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="62d5d-133">或者，</span><span class="sxs-lookup"><span data-stu-id="62d5d-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="62d5d-134">您可以選擇 toocreate hello hello 資料大量匯入之前的索引。</span><span class="sxs-lookup"><span data-stu-id="62d5d-134">You may choose toocreate hello indexes before bulk importing hello data.</span></span> <span data-ttu-id="62d5d-135">大量匯入之前的索引建立將會變慢 hello 資料載入。</span><span class="sxs-lookup"><span data-stu-id="62d5d-135">Index creation before bulk importing will slow down hello data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="62d5d-136">進階分析程序和技術實務範例</span><span class="sxs-lookup"><span data-stu-id="62d5d-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="62d5d-137">如需與公用的資料集使用 hello Cortana 分析程序的端對端逐步解說範例，請參閱[動作中的 Cortana 分析程序： 使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="62d5d-137">For an end-to-end walkthrough example using hello Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

