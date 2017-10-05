---
title: "移動資料至 Azure 虛擬機器上的 SQL Server | Microsoft Docs"
description: "從一般檔案或內部部署的 SQL Server 移動資料至 Azure VM 上的 SQL Server"
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
ms.openlocfilehash: aa0cbba6bdb4cfdfe6ceee50c94f706aa0974924
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="cfbdd-103">移動資料至 Azure 虛擬機器上的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="cfbdd-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="cfbdd-104">本主題概述從一般檔案 (CSV 或 TSV 格式) 或是內部部署的 SQL Server，將資料移動至 Azure 虛擬機器上之 SQL Server 的選項。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="cfbdd-105">將資料移到雲端的這些工作是 Team Data Science Process 的一部分。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="cfbdd-106">如需概述移動資料至機器學習的 Azure SQL Database 之選項的主題，請參閱 [移動資料至 Azure Machine Learning 的 Azure SQL Database](machine-learning-data-science-move-sql-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="cfbdd-107">以下 **功能表** 所連結的主題會說明如何將資料內嵌至其他目標環境，以在 Team Data Science Process (TDSP) 期間儲存和處理該資料。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="cfbdd-108">下表摘要說明移動資料至 Azure 虛擬機器上之 SQL Server 的選項。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="cfbdd-109"><b>來源</b></span><span class="sxs-lookup"><span data-stu-id="cfbdd-109"><b>SOURCE</b></span></span> | <span data-ttu-id="cfbdd-110"><b>目的地：Azure VM 上的 SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="cfbdd-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="cfbdd-111"><b>一般檔案</b></span><span class="sxs-lookup"><span data-stu-id="cfbdd-111"><b>Flat File</b></span></span> |<span data-ttu-id="cfbdd-112">1.<a href="#insert-tables-bcp">命令列大量複製公用程式 (BCP)</a></span><span class="sxs-lookup"><span data-stu-id="cfbdd-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="cfbdd-113">2.<a href="#insert-tables-bulkquery">大量插入 SQL 查詢</a></span><span class="sxs-lookup"><span data-stu-id="cfbdd-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="cfbdd-114">3.<a href="#sql-builtin-utilities">SQL Server 中的圖形化內建公用程式</a></span><span class="sxs-lookup"><span data-stu-id="cfbdd-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="cfbdd-115"><b>內部部署的 SQL Server</b></span><span class="sxs-lookup"><span data-stu-id="cfbdd-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="cfbdd-116">1.<a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">將 SQL Server Database 部署到 Microsoft Azure VM 精靈</a></span><span class="sxs-lookup"><span data-stu-id="cfbdd-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="cfbdd-117">2.<a href="#export-flat-file">匯出到一般檔案</a></span><span class="sxs-lookup"><span data-stu-id="cfbdd-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="cfbdd-118">3.<a href="#sql-migration">SQL Database 移轉精靈</a></span><span class="sxs-lookup"><span data-stu-id="cfbdd-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="cfbdd-119">4.<a href="#sql-backup">資料庫備份和還原</a></span><span class="sxs-lookup"><span data-stu-id="cfbdd-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="cfbdd-120">請注意，本文件假設 SQL 命令是從 SQL Server Management Studio 或 Visual Studio 資料庫總管中執行。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="cfbdd-121">或者，您可以使用 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) 建立並排程管線，以將資料移至 Azure 上的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="cfbdd-122">如需詳細資訊，請參閱 [使用 Azure Data Factory 複製資料 (複製活動)](../data-factory/data-factory-data-movement-activities.md)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="cfbdd-123"><a name="prereqs"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="cfbdd-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="cfbdd-124">本教學課程假設您有：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="cfbdd-125">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-125">An **Azure subscription**.</span></span> <span data-ttu-id="cfbdd-126">如果您沒有訂用帳戶，可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cfbdd-127">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-127">An **Azure storage account**.</span></span> <span data-ttu-id="cfbdd-128">在本教學課程中，您將使用 Azure 儲存體帳戶來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="cfbdd-129">如果您沒有 Azure 儲存體帳戶，請參閱 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account) 一文。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="cfbdd-130">建立儲存體帳戶之後，您必須取得用來存取儲存體的帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="cfbdd-131">請參閱[管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="cfbdd-132">已佈建 **Azure VM 上的 SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="cfbdd-133">如需指示，請參閱 [將 Azure SQL Server 虛擬機器設定為 IPython Notebook 伺服器供進階分析使用](machine-learning-data-science-setup-sql-server-virtual-machine.md)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="cfbdd-134">已在本機上安裝和設定 **Azure PowerShell** 。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="cfbdd-135">如需指示，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="cfbdd-136"><a name="filesource_to_sqlonazurevm"></a> 從一般檔案來源移動資料至 Azure VM 上的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="cfbdd-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="cfbdd-137">如果您的資料位於一般檔案 (使用資料列或資料行格式排列) 中，可透過下列方法，將它移到 Azure 上的 SQL Server VM：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="cfbdd-138">命令列大量複製公用程式 (BCP)</span><span class="sxs-lookup"><span data-stu-id="cfbdd-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="cfbdd-139">大量插入 SQL 查詢 </span><span class="sxs-lookup"><span data-stu-id="cfbdd-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="cfbdd-140">SQL Server 中的圖形化內建公用程式 (匯入/匯出，SSIS)</span><span class="sxs-lookup"><span data-stu-id="cfbdd-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="cfbdd-141"><a name="insert-tables-bcp"></a>命令列大量複製公用程式 (BCP)</span><span class="sxs-lookup"><span data-stu-id="cfbdd-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="cfbdd-142">BCP 是與 SQL Server 一起安裝的命令列公用程式，是最快速移動資料的其中一種方式。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="cfbdd-143">它的運作方式可跨越這三個 SQL Server 版本 (內部部署的 SQL Server、SQL Azure，以及 Azure 上的 SQL Server VM)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="cfbdd-144">**我應該針對 BCP 將資料放置於何處？**</span><span class="sxs-lookup"><span data-stu-id="cfbdd-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="cfbdd-145">雖然並非必要，但是，擁有包含與目標 SQL Server 位於相同電腦上之來源資料的檔案可讓傳輸速度 (網路速度與本機磁碟 IO 速度) 變得更快。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="cfbdd-146">您可以使用像是 [AZCopy](../storage/common/storage-use-azcopy.md)、[Azure 儲存體總管](http://storageexplorer.com/)或透過遠端桌面通訊協定 (RDP) 進行的 Windows 複製/貼上等各種檔案複製工具，將包含資料的一般檔案移到安裝 SQL Server 的電腦上。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="cfbdd-147">確定已在目標 SQL Server 資料庫上建立資料庫和資料表。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="cfbdd-148">以下是如何使用 `Create Database` 和 `Create Table` 命令來執行此作業的範例：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="cfbdd-149">從安裝 BCP 的電腦命令列中發出下列命令，以產生說明資料表結構描述的格式檔案。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="cfbdd-150">使用 BCP 命令來將資料插入資料庫，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="cfbdd-151">若假設 SQL Server 安裝於同一部電腦上，這應該就能從命令列順利運作：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="cfbdd-152">**最佳化 BCP 插入** ：請參閱 [最佳化大量匯入的指導方針](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) 這篇文章，以將這類插入最佳化。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <span data-ttu-id="cfbdd-153"><a name="insert-tables-bulkquery-parallel"></a>平行插入以進行更快速的資料移動</span><span class="sxs-lookup"><span data-stu-id="cfbdd-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="cfbdd-154">如果您要移動的資料很大，就可以在 PowerShell 指令碼中同時平行執行多個 BCP 命令來加快運作速度。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="cfbdd-155">**巨量資料擷取** ：若要將大型和超大型資料集的資料載入予以最佳化，可以使用多個檔案群組和資料分割資料表來進行邏輯與實體資料庫資料表的資料分割。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="cfbdd-156">如需關於建立和載入資料至資料分割資料表的詳細資訊，請參閱 [平行載入 SQL 資料分割資料表](machine-learning-data-science-parallel-load-sql-partitioned-tables.md)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="cfbdd-157">下列 PowerShell 指令碼範例將示範使用 BCP 平行插入：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
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


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <span data-ttu-id="cfbdd-158"><a name="insert-tables-bulkquery"></a>大量插入 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="cfbdd-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="cfbdd-159">[大量插入 SQL 查詢](https://msdn.microsoft.com/library/ms188365)可用來將資料從以資料列/資料行為基礎的檔案匯入資料庫 (支援類型請參閱[準備大量匯出或匯入的資料 (SQL Server)](https://msdn.microsoft.com/library/ms188609) 主題中的說明)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="cfbdd-160">此處提供一些大量插入的命令範例，如下所示：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="cfbdd-161">分析您的資料，並在匯入之前設定任何自訂選項，以確定 SQL Server 資料庫會針對任何特殊欄位 (例如日期) 假設相同的格式。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="cfbdd-162">以下範例示範如何將日期格式設為「年-月-日」 (如果您的資料包含「年-月-日」格式的日期)：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="cfbdd-163">使用大量匯入陳述式來匯入資料：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <span data-ttu-id="cfbdd-164"><a name="sql-builtin-utilities"></a>SQL Server 中的內建公用程式</span><span class="sxs-lookup"><span data-stu-id="cfbdd-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="cfbdd-165">您可以使用 SQL Server Integration Services (SSIS)，將資料從一般檔案匯入 Azure 上的 SQL Server VM。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="cfbdd-166">SSIS 適用於兩種 Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="cfbdd-167">如需詳細資料，請參閱 [Integration Services (SSIS) 和 Studio 環境](https://technet.microsoft.com/library/ms140028.aspx)：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="cfbdd-168">如需 SQL Server Data Tools 的詳細資料，請參閱 [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="cfbdd-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="cfbdd-169">如需匯入/匯出精靈的詳細資料，請參閱 [SQL Server 匯入和匯出精靈](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="cfbdd-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="cfbdd-170"><a name="sqlonprem_to_sqlonazurevm"></a>從內部部署的 SQL Server 移動資料至 Azure VM 上的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="cfbdd-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="cfbdd-171">您也可以使用下列移轉策略：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="cfbdd-172">將 SQL Server Database 部署到 Microsoft Azure VM 精靈</span><span class="sxs-lookup"><span data-stu-id="cfbdd-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="cfbdd-173">匯出至一般檔案</span><span class="sxs-lookup"><span data-stu-id="cfbdd-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="cfbdd-174">SQL Database 移轉精靈</span><span class="sxs-lookup"><span data-stu-id="cfbdd-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="cfbdd-175">資料庫備份和還原</span><span class="sxs-lookup"><span data-stu-id="cfbdd-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="cfbdd-176">我們將在下方說明這每一項內容：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="cfbdd-177">將 SQL Server Database 部署到 Microsoft Azure VM 精靈</span><span class="sxs-lookup"><span data-stu-id="cfbdd-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="cfbdd-178">**將 SQL Server Database 部署到 Microsoft Azure VM 精靈** 是簡單且建議的方式，可用於將資料從內部部署 SQL Server 執行個體移至 Azure VM 上的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="cfbdd-179">如需詳細的步驟以及其他替代方案的討論，請參閱[將資料庫移轉至 Azure VM 上的 SQL Server](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="cfbdd-180"><a name="export-flat-file"></a>匯出至一般檔案</span><span class="sxs-lookup"><span data-stu-id="cfbdd-180"><a name="export-flat-file"></a>Export to Flat File</span></span>
<span data-ttu-id="cfbdd-181">有各種方法可用來從內部部署的 SQL Server 大量匯出資料，如 [資料的大量匯入及匯出 (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) 主題所述。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="cfbdd-182">本文件將提供大量複製程式 (BCP) 做為範例。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="cfbdd-183">一旦將資料匯出至一般檔案之後，就可以使用大量匯入功能來將它匯入另一部 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="cfbdd-184">使用 BCP 公用程式，從內部部署的 SQL Server 將資料匯出至檔案，如下所示</span><span class="sxs-lookup"><span data-stu-id="cfbdd-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="cfbdd-185">針對步驟 1 中匯出的資料表結構描述使用 `create database` 和 `create table`，在 Azure 的 SQL Server VM 上建立資料庫和資料表。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="cfbdd-186">建立格式檔案，用以說明要匯出/匯入之資料的資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="cfbdd-187">[建立格式檔案 (SQL 伺服器)](https://msdn.microsoft.com/library/ms191516.aspx)中說明了格式檔案的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="cfbdd-188">從 SQL Server 電腦執行 BCP 時產生格式檔案</span><span class="sxs-lookup"><span data-stu-id="cfbdd-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="cfbdd-189">針對 SQL Server 遠端執行 BCP 時產生格式檔案</span><span class="sxs-lookup"><span data-stu-id="cfbdd-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="cfbdd-190">使用 [從檔案來源移動資料](#filesource_to_sqlonazurevm) 一節中所述的任何方法，將一般檔案中的資料移至 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <span data-ttu-id="cfbdd-191"><a name="sql-migration"></a>SQL Database 移轉精靈</span><span class="sxs-lookup"><span data-stu-id="cfbdd-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="cfbdd-192">[SQL Server 資料庫移轉精靈](http://sqlazuremw.codeplex.com/) 提供方便使用的方式，讓您在兩個 SQL Server 執行個體之間移動資料。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="cfbdd-193">它讓使用者能夠對應來源與目的地資料表之間的資料結構描述，選擇資料行類型和其他各種功能。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="cfbdd-194">它會在幕後使用大量複製 (BCP) 功能。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="cfbdd-195">SQL Database 移轉精靈歡迎畫面的螢幕擷取畫面如下所示。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![SQL Server 移轉精靈][2]

### <span data-ttu-id="cfbdd-197"><a name="sql-backup"></a>資料庫備份和還原</span><span class="sxs-lookup"><span data-stu-id="cfbdd-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="cfbdd-198">SQL Server 支援：</span><span class="sxs-lookup"><span data-stu-id="cfbdd-198">SQL Server supports:</span></span>

1. <span data-ttu-id="cfbdd-199">[資料庫備份和還原功能](https://msdn.microsoft.com/library/ms187048.aspx) (兩者皆可為本機檔案或以 bacpac 匯出至 Blob) 和[資料層應用程式](https://msdn.microsoft.com/library/ee210546.aspx) (使用 bacpac)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="cfbdd-200">使用複製的資料庫直接在 Azure 上建立 SQL Server VM，或者複製到現有 SQL Azure 資料庫的能力。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="cfbdd-201">如需詳細資料，請參閱 [使用複製資料庫精靈](https://msdn.microsoft.com/library/ms188664.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="cfbdd-202">SQL Server Management Studio 的資料庫備份/還原選項的螢幕擷取畫面如下所示。</span><span class="sxs-lookup"><span data-stu-id="cfbdd-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![SQL Server 匯入工具][1]

## <a name="resources"></a><span data-ttu-id="cfbdd-204">資源</span><span class="sxs-lookup"><span data-stu-id="cfbdd-204">Resources</span></span>
[<span data-ttu-id="cfbdd-205">將資料庫移轉至 Azure VM 上的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="cfbdd-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="cfbdd-206">Azure 虛擬機器上的 SQL Server 概觀</span><span class="sxs-lookup"><span data-stu-id="cfbdd-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
