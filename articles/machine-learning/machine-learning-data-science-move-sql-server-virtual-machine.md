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
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="061ff-103">在 Azure 虛擬機器上的移動資料 tooSQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="061ff-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="061ff-104">本主題概述 hello 選項將資料從一般檔案 （CSV 或 TSV 格式），或是從內部部署 SQL Server tooSQL 伺服器移動 Azure 的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="061ff-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="061ff-105">移動資料 toohello 雲端這些工作是 hello 資料科學的小組流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="061ff-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="061ff-106">概述 hello 選項移動資料 tooan Azure SQL Database 的機器學習的主題，請參閱[移動資料 tooan Azure SQL Database 的 Azure Machine Learning](machine-learning-data-science-move-sql-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="061ff-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="061ff-107">hello**功能表**下方連結 tootopics 描述 tooingest 資料至其他目標環境，可以儲存和處理期間 hello 資料 hello 小組資料科學程序 (TDSP) 的方式。</span><span class="sxs-lookup"><span data-stu-id="061ff-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="061ff-108">hello 下表摘要說明 Azure 的虛擬機器上移動的資料 tooSQL 伺服器 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="061ff-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="061ff-109"><b>來源</b></span><span class="sxs-lookup"><span data-stu-id="061ff-109"><b>SOURCE</b></span></span> | <span data-ttu-id="061ff-110"><b>目的地：Azure VM 上的 SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="061ff-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="061ff-111"><b>一般檔案</b></span><span class="sxs-lookup"><span data-stu-id="061ff-111"><b>Flat File</b></span></span> |<span data-ttu-id="061ff-112">1.<a href="#insert-tables-bcp">命令列大量複製公用程式 (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="061ff-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="061ff-113">2.<a href="#insert-tables-bulkquery">大量插入 SQL 查詢</a></span><span class="sxs-lookup"><span data-stu-id="061ff-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="061ff-114">3.<a href="#sql-builtin-utilities">SQL Server 中的圖形化內建公用程式</a></span><span class="sxs-lookup"><span data-stu-id="061ff-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="061ff-115"><b>內部部署的 SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="061ff-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="061ff-116">1.<a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">部署 SQL Server 資料庫 tooa Microsoft Azure VM 精靈</a></span><span class="sxs-lookup"><span data-stu-id="061ff-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="061ff-117">2.<a href="#export-flat-file">匯出 tooa 一般檔案</a></span><span class="sxs-lookup"><span data-stu-id="061ff-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="061ff-118">3.<a href="#sql-migration">SQL Database 移轉精靈</a></span><span class="sxs-lookup"><span data-stu-id="061ff-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="061ff-119">4.<a href="#sql-backup">資料庫備份和還原</a></span><span class="sxs-lookup"><span data-stu-id="061ff-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="061ff-120">請注意，本文件假設 SQL 命令是從 SQL Server Management Studio 或 Visual Studio 資料庫總管中執行。</span><span class="sxs-lookup"><span data-stu-id="061ff-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="061ff-121">或者，您可以使用[Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate 和排程會移動資料 tooa SQL Server VM 在 Azure 的管線。</span><span class="sxs-lookup"><span data-stu-id="061ff-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="061ff-122">如需詳細資訊，請參閱 [使用 Azure Data Factory 複製資料 (複製活動)](../data-factory/data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="061ff-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="061ff-123"><a name="prereqs"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="061ff-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="061ff-124">本教學課程假設您有：</span><span class="sxs-lookup"><span data-stu-id="061ff-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="061ff-125">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="061ff-125">An **Azure subscription**.</span></span> <span data-ttu-id="061ff-126">如果您沒有訂用帳戶，可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="061ff-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="061ff-127">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="061ff-127">An **Azure storage account**.</span></span> <span data-ttu-id="061ff-128">將 hello 資料儲存在本教學課程，您將使用 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="061ff-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="061ff-129">如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)發行項。</span><span class="sxs-lookup"><span data-stu-id="061ff-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="061ff-130">建立 hello 儲存體帳戶之後，您必須使用 tooaccess hello 儲存體金鑰 tooobtain hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="061ff-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="061ff-131">請參閱 [管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="061ff-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="061ff-132">已佈建 **Azure VM 上的 SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="061ff-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="061ff-133">如需指示，請參閱 [將 Azure SQL Server 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用](machine-learning-data-science-setup-sql-server-virtual-machine.md)。</span><span class="sxs-lookup"><span data-stu-id="061ff-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="061ff-134">已在本機上安裝和設定 **Azure PowerShell** 。</span><span class="sxs-lookup"><span data-stu-id="061ff-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="061ff-135">如需指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="061ff-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="061ff-136"><a name="filesource_to_sqlonazurevm"></a>一般檔案來源 tooSQL Azure VM 上的伺服器中的資料移</span><span class="sxs-lookup"><span data-stu-id="061ff-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="061ff-137">如果您的資料是一般檔案 （以資料列/資料行格式排列） 中，它可以是移動的 tooSQL 伺服器 VM 在 Azure 上透過 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="061ff-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="061ff-138">命令列大量複製公用程式 (BCP)</span><span class="sxs-lookup"><span data-stu-id="061ff-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="061ff-139">大量插入 SQL 查詢 </span><span class="sxs-lookup"><span data-stu-id="061ff-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="061ff-140">SQL Server 中的圖形化內建公用程式 (匯入/匯出，SSIS)</span><span class="sxs-lookup"><span data-stu-id="061ff-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="061ff-141"><a name="insert-tables-bcp"></a>命令列大量複製公用程式 (BCP)</span><span class="sxs-lookup"><span data-stu-id="061ff-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="061ff-142">BCP 是隨 SQL Server 安裝的命令列公用程式，其中一個 hello 最快方式 toomove 資料。</span><span class="sxs-lookup"><span data-stu-id="061ff-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="061ff-143">它的運作方式可跨越這三個 SQL Server 版本 (內部部署的 SQL Server、SQL Azure，以及 Azure 上的 SQL Server VM)。</span><span class="sxs-lookup"><span data-stu-id="061ff-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="061ff-144">**我應該針對 BCP 將資料放置於何處？**</span><span class="sxs-lookup"><span data-stu-id="061ff-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="061ff-145">雖然並非必要項目，讓檔案包含來源資料位於的 hello hello 目標 SQL Server 相同的電腦允許更快的傳輸 （網路速度與本機磁碟 IO 速度）。</span><span class="sxs-lookup"><span data-stu-id="061ff-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="061ff-146">您可以移動 hello 一般檔案包含資料 toohello 機器的 SQL Server 安裝使用不同的檔案複製之類的工具[AZCopy](../storage/common/storage-use-azcopy.md)， [Azure 儲存體總管](http://storageexplorer.com/)或 windows 複製/貼上透過遠端桌面通訊協定 (RDP)。</span><span class="sxs-lookup"><span data-stu-id="061ff-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="061ff-147">請 hello 目標 SQL Server 資料庫建立 hello 資料庫和 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="061ff-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="061ff-148">以下是如何的範例 toodo 使用 hello`Create Database`和`Create Table`命令：</span><span class="sxs-lookup"><span data-stu-id="061ff-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="061ff-149">產生 hello 格式檔案，其中描述 hello hello 資料表的結構描述發出 hello hello hello 機器的命令列中的下列命令安裝 bcp。</span><span class="sxs-lookup"><span data-stu-id="061ff-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="061ff-150">Hello 資料插入 hello 資料庫，如下所示使用 hello bcp 命令。</span><span class="sxs-lookup"><span data-stu-id="061ff-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="061ff-151">這應該假設 hello SQL Server 安裝在同一部電腦上運作的 hello 命令列：</span><span class="sxs-lookup"><span data-stu-id="061ff-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="061ff-152">**最佳化 BCP 插入**，請參閱下列文章 hello ['最佳化大量匯入的指導方針'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize 這類插入。</span><span class="sxs-lookup"><span data-stu-id="061ff-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="061ff-153"><a name="insert-tables-bulkquery-parallel"></a>平行插入以進行更快速的資料移動</span><span class="sxs-lookup"><span data-stu-id="061ff-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="061ff-154">如果您要移動的 hello 資料很大，您可以提高效率藉由同時執行多個 BCP 命令以平行方式在 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="061ff-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="061ff-155">**巨量資料擷取**toooptimize 資料載入的大型和大型資料集，分割區的邏輯與實體資料庫資料表使用多個檔案群組和分割區資料表。</span><span class="sxs-lookup"><span data-stu-id="061ff-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="061ff-156">如需建立及載入資料 toopartition 資料表的詳細資訊，請參閱[平行載入 SQL 資料分割資料表](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="061ff-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="061ff-157">hello 以下的範例 PowerShell 指令碼示範使用 bcp 平行插入：</span><span class="sxs-lookup"><span data-stu-id="061ff-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

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


### <span data-ttu-id="061ff-158"><a name="insert-tables-bulkquery"></a>大量插入 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="061ff-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="061ff-159">[大量插入的 SQL 查詢](https://msdn.microsoft.com/library/ms188365)可以是使用的 tooimport 資料到資料列/資料行為基礎的檔案從 hello 資料庫 (hello 支援類型會涵蓋[準備的資料大量匯出或匯入 (SQL Server)](https://msdn.microsoft.com/library/ms188609)) 主題。</span><span class="sxs-lookup"><span data-stu-id="061ff-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="061ff-160">此處提供一些大量插入的命令範例，如下所示：</span><span class="sxs-lookup"><span data-stu-id="061ff-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="061ff-161">分析資料，然後再匯入 toomake 確定該 hello SQL Server 資料庫會假設的 hello 相同的任何特殊的欄位，例如日期格式設定任何自訂的選項。</span><span class="sxs-lookup"><span data-stu-id="061ff-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="061ff-162">以下是如何 tooset hello 日期格式化為年-月-日 （如果您的資料包含 hello 年-月-日格式的日期） 的範例：</span><span class="sxs-lookup"><span data-stu-id="061ff-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="061ff-163">使用大量匯入陳述式來匯入資料：</span><span class="sxs-lookup"><span data-stu-id="061ff-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="061ff-164"><a name="sql-builtin-utilities"></a>SQL Server 中的內建公用程式</span><span class="sxs-lookup"><span data-stu-id="061ff-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="061ff-165">您可以使用 SQL Server 整合服務 (SSIS) tooimport 資料將從一般檔案的 Azure 上的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="061ff-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="061ff-166">SSIS 適用於兩種 Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="061ff-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="061ff-167">如需詳細資料，請參閱 [Integration Services (SSIS) 和 Studio 環境](https://technet.microsoft.com/library/ms140028.aspx)：</span><span class="sxs-lookup"><span data-stu-id="061ff-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="061ff-168">如需 SQL Server Data Tools 的詳細資料，請參閱 [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="061ff-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="061ff-169">如需 hello 匯入/匯出精靈的詳細資訊，請參閱[SQL Server 匯入和匯出精靈](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="061ff-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="061ff-170"><a name="sqlonprem_to_sqlonazurevm"></a>在內部部署 SQL Server tooSQL Azure VM 上的伺服器中的資料移</span><span class="sxs-lookup"><span data-stu-id="061ff-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="061ff-171">您也可以使用下列移轉策略的 hello:</span><span class="sxs-lookup"><span data-stu-id="061ff-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="061ff-172">部署 SQL Server 資料庫 tooa Microsoft Azure VM 精靈</span><span class="sxs-lookup"><span data-stu-id="061ff-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="061ff-173">匯出 tooFlat 檔案</span><span class="sxs-lookup"><span data-stu-id="061ff-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="061ff-174">SQL Database 移轉精靈</span><span class="sxs-lookup"><span data-stu-id="061ff-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="061ff-175">資料庫備份和還原</span><span class="sxs-lookup"><span data-stu-id="061ff-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="061ff-176">我們將在下方說明這每一項內容：</span><span class="sxs-lookup"><span data-stu-id="061ff-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="061ff-177">部署 SQL Server 資料庫 tooa Microsoft Azure VM 精靈</span><span class="sxs-lookup"><span data-stu-id="061ff-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="061ff-178">hello**部署 SQL Server 資料庫 tooa Microsoft Azure VM 精靈**是簡單且建議的方式 toomove 資料從內部部署 SQL Server 執行個體 tooSQL Azure VM 上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="061ff-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="061ff-179">詳細的步驟，以及其他替代方案的討論，請參閱[移轉資料庫 tooSQL Azure VM 上的 Server](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="061ff-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="061ff-180"><a name="export-flat-file"></a>匯出 tooFlat 檔案</span><span class="sxs-lookup"><span data-stu-id="061ff-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="061ff-181">各種方法可以是從內部部署 SQL Server 使用的 toobulk 匯出資料，如 hello 中所述[大量匯入和匯出的資料 (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx)主題。</span><span class="sxs-lookup"><span data-stu-id="061ff-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="061ff-182">本文件將涵蓋 hello 大量複製程式 (BCP)，做為範例。</span><span class="sxs-lookup"><span data-stu-id="061ff-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="061ff-183">一旦資料匯出到一般檔案時，它可以匯入的 tooanother 使用大量匯入的 SQL server。</span><span class="sxs-lookup"><span data-stu-id="061ff-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="061ff-184">在內部部署 SQL Server tooa 檔案從匯出 hello 資料，如下所示使用 hello bcp 公用程式</span><span class="sxs-lookup"><span data-stu-id="061ff-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="061ff-185">使用 hello Azure 上的 SQL Server VM 上建立 hello 資料庫和 hello 資料表`create database`和`create table`hello 在步驟 1 中匯出的資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="061ff-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="061ff-186">建立格式檔案來描述 hello 的 hello 資料，則匯出/匯入的資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="061ff-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="061ff-187">Hello 格式檔案的詳細資料中所述[建立格式檔案 (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx)。</span><span class="sxs-lookup"><span data-stu-id="061ff-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="061ff-188">當執行 BCP 從 hello SQL Server 電腦產生格式檔案</span><span class="sxs-lookup"><span data-stu-id="061ff-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="061ff-189">針對 SQL Server 遠端執行 BCP 時產生格式檔案</span><span class="sxs-lookup"><span data-stu-id="061ff-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="061ff-190">使用任何一節所述的 hello 方法[移動檔案 」 來源的資料](#filesource_to_sqlonazurevm)toomove 一般檔案 tooa SQL Server 中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="061ff-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="061ff-191"><a name="sql-migration"></a>SQL Database 移轉精靈</span><span class="sxs-lookup"><span data-stu-id="061ff-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="061ff-192">[SQL Server Database 移轉精靈](http://sqlazuremw.codeplex.com/)提供方便使用的方式 toomove 兩個 SQL server 執行個體之間的資料。</span><span class="sxs-lookup"><span data-stu-id="061ff-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="061ff-193">它可讓 hello 使用者 toomap hello 資料結構描述來源和目的地資料表之間，請選擇資料行類型與其他各種功能。</span><span class="sxs-lookup"><span data-stu-id="061ff-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="061ff-194">它使用大量複製 (BCP) hello 幕後。</span><span class="sxs-lookup"><span data-stu-id="061ff-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="061ff-195">螢幕擷取畫面的 hello 歡迎畫面的 hello SQL Database 移轉精靈會如下所示。</span><span class="sxs-lookup"><span data-stu-id="061ff-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![SQL Server 移轉精靈][2]

### <span data-ttu-id="061ff-197"><a name="sql-backup"></a>資料庫備份和還原</span><span class="sxs-lookup"><span data-stu-id="061ff-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="061ff-198">SQL Server 支援：</span><span class="sxs-lookup"><span data-stu-id="061ff-198">SQL Server supports:</span></span>

1. <span data-ttu-id="061ff-199">[資料庫備份和還原功能](https://msdn.microsoft.com/library/ms187048.aspx)(這兩個 tooa 本機檔案或 bacpac 匯出 tooblob) 和[資料層應用程式](https://msdn.microsoft.com/library/ee210546.aspx)（使用 bacpac）。</span><span class="sxs-lookup"><span data-stu-id="061ff-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="061ff-200">能力 toodirectly Azure 上建立 SQL Server Vm，以複製的資料庫或複本 tooan 現有的 SQL Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="061ff-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="061ff-201">如需詳細資訊，請參閱[使用 hello 複製資料庫精靈](https://msdn.microsoft.com/library/ms188664.aspx)。</span><span class="sxs-lookup"><span data-stu-id="061ff-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="061ff-202">Hello 資料庫備份的螢幕擷取畫面向上/還原 SQL Server Management Studio 中的選項如下所示。</span><span class="sxs-lookup"><span data-stu-id="061ff-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![SQL Server 匯入工具][1]

## <a name="resources"></a><span data-ttu-id="061ff-204">資源</span><span class="sxs-lookup"><span data-stu-id="061ff-204">Resources</span></span>
[<span data-ttu-id="061ff-205">移轉資料庫 tooSQL Azure VM 上的伺服器</span><span class="sxs-lookup"><span data-stu-id="061ff-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="061ff-206">Azure 虛擬機器上的 SQL Server 概觀</span><span class="sxs-lookup"><span data-stu-id="061ff-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
