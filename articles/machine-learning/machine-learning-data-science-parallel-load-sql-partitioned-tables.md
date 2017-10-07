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
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>使用 SQL 資料分割資料表平行處理大量資料匯入
本文件說明如何 toobuild 資料分割進行快速平行大量匯入資料 tooa SQL Server 資料庫的資料表。 巨量資料載入/transfer tooa SQL database 匯入資料 toohello SQL DB 和後續查詢，可以使用來改善*分割資料表和檢視表*。 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>建立新的資料庫和一組檔案群組
* [建立新的資料庫](https://technet.microsoft.com/library/ms176061.aspx) (如果尚不存在)。
* 將資料庫檔案群組 toohello 資料庫會保留資料分割的 hello 實體檔案。這可以透過[CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx)如果是新或[ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx)如果 hello 資料庫已經存在。
* 新增一或多個檔案 （如有需要） tooeach 資料庫檔案群組。
  
  > [!NOTE]
  > 指定 hello 目標檔案群組，其中包含此資料分割和 hello 實體資料庫檔案名稱的資料儲存 hello 檔案群組資料。
  > 
  > 

hello 下列範例會建立新的資料庫具有三個主要的 hello 和包含在每一個實體檔案的記錄檔群組以外的檔案群組。 hello 資料庫檔案建立在 hello 預設 SQL Server Data 資料夾中，為 hello SQL Server 執行個體中設定。 如需 hello 預設檔案位置的詳細資訊，請參閱[檔案位置的預設和具名執行個體的 SQL Server](https://msdn.microsoft.com/library/ms143547.aspx)。

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

## <a name="create-a-partitioned-table"></a>建立資料分割資料表
建立根據 toohello 資料結構描述、 對應的 toohello hello 先前步驟中建立的資料庫檔案群組的資料分割的資料表。 大量匯入資料時 toohello 分割資料表，記錄會分配給 hello 根據 tooa 分割區配置的檔案群組，如下所述。

**toocreate 磁碟分割表格，您要：**

* [建立資料分割函數](https://msdn.microsoft.com/library/ms187802.aspx)其定義的界限值/toobe hello 範圍包含在每個個別資料分割資料表，例如 toolimit 依月份的資料分割 (某些\_datetime\_欄位) hello 年 2013年:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [建立資料分割配置](https://msdn.microsoft.com/library/ms179854.aspx)例如對應 hello 資料分割函數 tooa 實體檔案群組中，每個資料分割範圍：
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  tooverify hello 範圍，實際上是在每個資料分割相應 toohello 函式/配置，請執行下列查詢的 hello:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [建立分割區的資料表](https://msdn.microsoft.com/library/ms174979.aspx)(s)，根據 tooyour 資料結構描述，並指定 hello 磁碟分割配置和條件約束欄位使用 toopartition hello 資料表，例如：
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

如需詳細資訊，請參閱 [建立分割區資料表及索引](https://msdn.microsoft.com/library/ms188730.aspx)。

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>針對每個個別資料分割資料表的大量匯入 hello 資料
* 您可以使用 BCP、BULK INSERT 或其他方法，例如 [SQL Server 移轉精靈](http://sqlazuremw.codeplex.com/)。 所提供的 hello 範例會使用 hello BCP 方法。
* [Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange 交易記錄的記錄，例如配置 tooBULK_LOGGED toominimize 負擔：
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* tooexpedite 資料載入，啟動 hello 大量匯入作業，以平行方式。 如需加速將巨量資料大量匯入 SQL Server 資料庫的提示，請參閱 [載入 1 TB 的時間少於 1 小時](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx)(英文)。

hello 下列 PowerShell 指令碼是載入使用 BCP 的平行處理資料的範例。

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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>建立索引 toooptimize 聯結和查詢效能
* 如果您將會從多個資料表來擷取模型的資料，建立索引 hello 聯結索引鍵上 tooimprove hello 聯結的效能。
* [建立索引](https://technet.microsoft.com/library/ms188783.aspx)（叢集或非叢集） 目標 hello 相同的檔案群組，每個分割區，例如：
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  或者，
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > 您可以選擇 toocreate hello hello 資料大量匯入之前的索引。 大量匯入之前的索引建立將會變慢 hello 資料載入。
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>進階分析程序和技術實務範例
如需與公用的資料集使用 hello Cortana 分析程序的端對端逐步解說範例，請參閱[動作中的 Cortana 分析程序： 使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)。

