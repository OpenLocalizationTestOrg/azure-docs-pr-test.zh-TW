---
title: "在 Azure 虛擬機器上的 aaaMove 資料 tooSQL 伺服器 |Microsoft 文件"
description: "移動資料從一般檔案或從內部部署 SQL Server tooSQL 伺服器，Azure VM 上。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a>在 Azure 虛擬機器上的移動資料 tooSQL 伺服器
本主題概述 hello 選項將資料從一般檔案 （CSV 或 TSV 格式），或是從內部部署 SQL Server tooSQL 伺服器移動 Azure 的虛擬機器上。 移動資料 toohello 雲端這些工作是 hello 資料科學的小組流程的一部分。

概述 hello 選項移動資料 tooan Azure SQL Database 的機器學習的主題，請參閱[移動資料 tooan Azure SQL Database 的 Azure Machine Learning](machine-learning-data-science-move-sql-azure.md)。

hello**功能表**下方連結 tootopics 描述 tooingest 資料至其他目標環境，可以儲存和處理期間 hello 資料 hello 小組資料科學程序 (TDSP) 的方式。

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

hello 下表摘要說明 Azure 的虛擬機器上移動的資料 tooSQL 伺服器 hello 選項。

| <b>來源</b> | <b>目的地：Azure VM 上的 SQL Server</b> |
| --- | --- |
| <b>一般檔案</b> |1.<a href="#insert-tables-bcp">命令列大量複製公用程式 (BCP)</a><br> 2.<a href="#insert-tables-bulkquery">大量插入 SQL 查詢</a><br> 3.<a href="#sql-builtin-utilities">SQL Server 中的圖形化內建公用程式</a> |
| <b>內部部署的 SQL Server</b> |1.<a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">部署 SQL Server 資料庫 tooa Microsoft Azure VM 精靈</a><br> 2.<a href="#export-flat-file">匯出 tooa 一般檔案</a><br> 3.<a href="#sql-migration">SQL Database 移轉精靈</a> <br> 4.<a href="#sql-backup">資料庫備份和還原</a><br> |

請注意，本文件假設 SQL 命令是從 SQL Server Management Studio 或 Visual Studio 資料庫總管中執行。

> [!TIP]
> 或者，您可以使用[Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate 和排程會移動資料 tooa SQL Server VM 在 Azure 的管線。 如需詳細資訊，請參閱 [使用 Azure Data Factory 複製資料 (複製活動)](../data-factory/data-factory-data-movement-activities.md)。
>
>

## <a name="prereqs"></a>必要條件
本教學課程假設您有：

* **Azure 訂用帳戶**。 如果您沒有訂用帳戶，可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure 儲存體帳戶**。 將 hello 資料儲存在本教學課程，您將使用 Azure 儲存體帳戶。 如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)發行項。 建立 hello 儲存體帳戶之後，您必須使用 tooaccess hello 儲存體金鑰 tooobtain hello 帳戶。 請參閱 [管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。
* 已佈建 **Azure VM 上的 SQL Server**。 如需指示，請參閱 [將 Azure SQL Server 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用](machine-learning-data-science-setup-sql-server-virtual-machine.md)。
* 已在本機上安裝和設定 **Azure PowerShell** 。 如需指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a name="filesource_to_sqlonazurevm"></a>一般檔案來源 tooSQL Azure VM 上的伺服器中的資料移
如果您的資料是一般檔案 （以資料列/資料行格式排列） 中，它可以是移動的 tooSQL 伺服器 VM 在 Azure 上透過 hello 下列方法：

1. [命令列大量複製公用程式 (BCP)](#insert-tables-bcp)
2. [大量插入 SQL 查詢 ](#insert-tables-bulkquery)
3. [SQL Server 中的圖形化內建公用程式 (匯入/匯出，SSIS)](#sql-builtin-utilities)

### <a name="insert-tables-bcp"></a>命令列大量複製公用程式 (BCP)
BCP 是隨 SQL Server 安裝的命令列公用程式，其中一個 hello 最快方式 toomove 資料。 它的運作方式可跨越這三個 SQL Server 版本 (內部部署的 SQL Server、SQL Azure，以及 Azure 上的 SQL Server VM)。

> [!NOTE]
> **我應該針對 BCP 將資料放置於何處？**  
> 雖然並非必要項目，讓檔案包含來源資料位於的 hello hello 目標 SQL Server 相同的電腦允許更快的傳輸 （網路速度與本機磁碟 IO 速度）。 您可以移動 hello 一般檔案包含資料 toohello 機器的 SQL Server 安裝使用不同的檔案複製之類的工具[AZCopy](../storage/common/storage-use-azcopy.md)， [Azure 儲存體總管](http://storageexplorer.com/)或 windows 複製/貼上透過遠端桌面通訊協定 (RDP)。
>
>

1. 請 hello 目標 SQL Server 資料庫建立 hello 資料庫和 hello 資料表。 以下是如何的範例 toodo 使用 hello`Create Database`和`Create Table`命令：

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. 產生 hello 格式檔案，其中描述 hello hello 資料表的結構描述發出 hello hello hello 機器的命令列中的下列命令安裝 bcp。

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. Hello 資料插入 hello 資料庫，如下所示使用 hello bcp 命令。 這應該假設 hello SQL Server 安裝在同一部電腦上運作的 hello 命令列：

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> **最佳化 BCP 插入**，請參閱下列文章 hello ['最佳化大量匯入的指導方針'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize 這類插入。
>
>

### <a name="insert-tables-bulkquery-parallel"></a>平行插入以進行更快速的資料移動
如果您要移動的 hello 資料很大，您可以提高效率藉由同時執行多個 BCP 命令以平行方式在 PowerShell 指令碼。

> [!NOTE]
> **巨量資料擷取**toooptimize 資料載入的大型和大型資料集，分割區的邏輯與實體資料庫資料表使用多個檔案群組和分割區資料表。 如需建立及載入資料 toopartition 資料表的詳細資訊，請參閱[平行載入 SQL 資料分割資料表](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。
>
>

hello 以下的範例 PowerShell 指令碼示範使用 bcp 平行插入：

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <a name="insert-tables-bulkquery"></a>大量插入 SQL 查詢
[大量插入的 SQL 查詢](https://msdn.microsoft.com/library/ms188365)可以是使用的 tooimport 資料到資料列/資料行為基礎的檔案從 hello 資料庫 (hello 支援類型會涵蓋[準備的資料大量匯出或匯入 (SQL Server)](https://msdn.microsoft.com/library/ms188609)) 主題。

此處提供一些大量插入的命令範例，如下所示：  

1. 分析資料，然後再匯入 toomake 確定該 hello SQL Server 資料庫會假設的 hello 相同的任何特殊的欄位，例如日期格式設定任何自訂的選項。 以下是如何 tooset hello 日期格式化為年-月-日 （如果您的資料包含 hello 年-月-日格式的日期） 的範例：

        SET DATEFORMAT ymd;    
2. 使用大量匯入陳述式來匯入資料：

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <a name="sql-builtin-utilities"></a>SQL Server 中的內建公用程式
您可以使用 SQL Server 整合服務 (SSIS) tooimport 資料將從一般檔案的 Azure 上的 SQL Server VM。
SSIS 適用於兩種 Studio 環境。 如需詳細資料，請參閱 [Integration Services (SSIS) 和 Studio 環境](https://technet.microsoft.com/library/ms140028.aspx)：

* 如需 SQL Server Data Tools 的詳細資料，請參閱 [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)  
* 如需 hello 匯入/匯出精靈的詳細資訊，請參閱[SQL Server 匯入和匯出精靈](https://msdn.microsoft.com/library/ms141209.aspx)

## <a name="sqlonprem_to_sqlonazurevm"></a>在內部部署 SQL Server tooSQL Azure VM 上的伺服器中的資料移
您也可以使用下列移轉策略的 hello:

1. [部署 SQL Server 資料庫 tooa Microsoft Azure VM 精靈](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [匯出 tooFlat 檔案](#export-flat-file)
3. [SQL Database 移轉精靈](#sql-migration)
4. [資料庫備份和還原](#sql-backup)

我們將在下方說明這每一項內容：

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a>部署 SQL Server 資料庫 tooa Microsoft Azure VM 精靈
hello**部署 SQL Server 資料庫 tooa Microsoft Azure VM 精靈**是簡單且建議的方式 toomove 資料從內部部署 SQL Server 執行個體 tooSQL Azure VM 上的伺服器。 詳細的步驟，以及其他替代方案的討論，請參閱[移轉資料庫 tooSQL Azure VM 上的 Server](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)。

### <a name="export-flat-file"></a>匯出 tooFlat 檔案
各種方法可以是從內部部署 SQL Server 使用的 toobulk 匯出資料，如 hello 中所述[大量匯入和匯出的資料 (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx)主題。 本文件將涵蓋 hello 大量複製程式 (BCP)，做為範例。 一旦資料匯出到一般檔案時，它可以匯入的 tooanother 使用大量匯入的 SQL server。

1. 在內部部署 SQL Server tooa 檔案從匯出 hello 資料，如下所示使用 hello bcp 公用程式

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. 使用 hello Azure 上的 SQL Server VM 上建立 hello 資料庫和 hello 資料表`create database`和`create table`hello 在步驟 1 中匯出的資料表結構描述。
3. 建立格式檔案來描述 hello 的 hello 資料，則匯出/匯入的資料表結構描述。 Hello 格式檔案的詳細資料中所述[建立格式檔案 (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx)。

    當執行 BCP 從 hello SQL Server 電腦產生格式檔案

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    針對 SQL Server 遠端執行 BCP 時產生格式檔案

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. 使用任何一節所述的 hello 方法[移動檔案 」 來源的資料](#filesource_to_sqlonazurevm)toomove 一般檔案 tooa SQL Server 中的 hello 資料。

### <a name="sql-migration"></a>SQL Database 移轉精靈
[SQL Server Database 移轉精靈](http://sqlazuremw.codeplex.com/)提供方便使用的方式 toomove 兩個 SQL server 執行個體之間的資料。 它可讓 hello 使用者 toomap hello 資料結構描述來源和目的地資料表之間，請選擇資料行類型與其他各種功能。 它使用大量複製 (BCP) hello 幕後。 螢幕擷取畫面的 hello 歡迎畫面的 hello SQL Database 移轉精靈會如下所示。  

![SQL Server 移轉精靈][2]

### <a name="sql-backup"></a>資料庫備份和還原
SQL Server 支援：

1. [資料庫備份和還原功能](https://msdn.microsoft.com/library/ms187048.aspx)(這兩個 tooa 本機檔案或 bacpac 匯出 tooblob) 和[資料層應用程式](https://msdn.microsoft.com/library/ee210546.aspx)（使用 bacpac）。
2. 能力 toodirectly Azure 上建立 SQL Server Vm，以複製的資料庫或複本 tooan 現有的 SQL Azure 資料庫。 如需詳細資訊，請參閱[使用 hello 複製資料庫精靈](https://msdn.microsoft.com/library/ms188664.aspx)。

Hello 資料庫備份的螢幕擷取畫面向上/還原 SQL Server Management Studio 中的選項如下所示。

![SQL Server 匯入工具][1]

## <a name="resources"></a>資源
[移轉資料庫 tooSQL Azure VM 上的伺服器](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[Azure 虛擬機器上的 SQL Server 概觀](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
