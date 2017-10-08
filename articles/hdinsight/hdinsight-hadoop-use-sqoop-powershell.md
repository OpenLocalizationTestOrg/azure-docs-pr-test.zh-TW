---
title: "使用 PowerShell 和 Azure HDInsight aaaRun Sqoop 作業 |Microsoft 文件"
description: "了解如何從工作站 toorun Sqoop toouse Azure PowerShell 匯入和匯出的 Hadoop 叢集和 Azure SQL database 之間。"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: bbb6f53a-e019-4d01-92bd-92c208c760b6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 8313bbd109e968aeab540bbcefefe84ebd64c87e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-azure-powershell-for-hadoop-in-hdinsight"></a><span data-ttu-id="4a433-103">在 HDInsight 中使用 Azure PowerShell for Hadoop 執行 Sqoop 工作</span><span class="sxs-lookup"><span data-stu-id="4a433-103">Run Sqoop jobs using Azure PowerShell for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="4a433-104">了解 toouse Azure PowerShell toorun Sqoop HDInsight tooimport 中的工作，並匯出 HDInsight 叢集和 Azure SQL database 或 SQL Server 資料庫之間。</span><span class="sxs-lookup"><span data-stu-id="4a433-104">Learn how toouse Azure PowerShell toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="4a433-105">可以使用本文章中的 hello 步驟與任一 Windows 或 Linux 的 HDInsight 叢集。不過，這些步驟只會從 Windows 用戶端運作。</span><span class="sxs-lookup"><span data-stu-id="4a433-105">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps will only work from a Windows client.</span></span> <span data-ttu-id="4a433-106">對於其他工作提交方法，按一下 hello 發行項的最上層顯示 hello hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="4a433-106">For other job submission methods, click hello tab selector on hello top of hello article.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="4a433-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="4a433-107">Prerequisites</span></span>
<span data-ttu-id="4a433-108">開始本教學課程之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4a433-108">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="4a433-109">**具有 Azure PowerShell 的工作站**。</span><span class="sxs-lookup"><span data-stu-id="4a433-109">**A workstation with Azure PowerShell**.</span></span>
  
    [!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
* <span data-ttu-id="4a433-110">**HDInsight 中的 Hadoop 叢集**。</span><span class="sxs-lookup"><span data-stu-id="4a433-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="4a433-111">請參閱 [建立叢集與 SQL Database](hdinsight-use-sqoop.md#create-cluster-and-sql-database)。</span><span class="sxs-lookup"><span data-stu-id="4a433-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="run-sqoop-using-powershell"></a><span data-ttu-id="4a433-112">使用 PowerShell 執行 Sqoop</span><span class="sxs-lookup"><span data-stu-id="4a433-112">Run Sqoop using PowerShell</span></span>
<span data-ttu-id="4a433-113">下列 PowerShell 指令碼的 hello 預先處理 hello 原始程式檔，並將它匯出 tooan Azure SQL database:</span><span class="sxs-lookup"><span data-stu-id="4a433-113">hello following PowerShell script pre-processes hello source file, and exports it tooan Azure SQL database:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $hdinsightClusterName = "<HDInsightClusterName>"

    $httpUserName = "admin"
    $httpPassword = "<Password>"

    $defaultStorageAccountName = $hdinsightClusterName + "store"
    $defaultBlobContainerName = $hdinsightClusterName


    $sqlDatabaseServerName = $hdinsightClusterName + "dbserver"
    $sqlDatabaseName = $hdinsightClusterName + "db"
    $sqlDatabaseLogin = "sqluser"
    $sqlDatabasePassword = "<Password>"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - pre-process hello source file

    Write-Host "`nPreprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = Get-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $defaultStorageAccountName
    $storageContainer = ($storageAccount |Get-AzureStorageContainer -Name $defaultBlobContainerName).CloudBlobContainer
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export hello log file from hello cluster toohello SQL database

    Write-Host "Exporting hello log file ..." -ForegroundColor Green

    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $tableName_log4j = "log4jlogs"
    $exportDir_log4j = "/tutorials/usesqoop/data"
    $sqljdbcdriver = "/user/oozie/share/lib/sqoop/sqljdbc41.jar"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1" `
        -Files $sqljdbcdriver

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput
    #endregion

## <a name="limitations"></a><span data-ttu-id="4a433-114">限制</span><span class="sxs-lookup"><span data-stu-id="4a433-114">Limitations</span></span>
* <span data-ttu-id="4a433-115">大量匯出的以 Linux 為基礎的 HDInsight、 hello Sqoop 使用連接器 tooexport 資料 tooMicrosoft SQL Server 或 Azure SQL Database 目前不支援大量插入。</span><span class="sxs-lookup"><span data-stu-id="4a433-115">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="4a433-116">批次處理-與 linux 的 HDInsight，當使用 hello`-batch`切換時執行插入、 Sqoop 會執行多個的插入，而不是批次處理 hello 插入作業。</span><span class="sxs-lookup"><span data-stu-id="4a433-116">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a433-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a433-117">Next steps</span></span>
<span data-ttu-id="4a433-118">現在您已經學會如何 toouse Sqoop。</span><span class="sxs-lookup"><span data-stu-id="4a433-118">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="4a433-119">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="4a433-119">toolearn more, see:</span></span>

* <span data-ttu-id="4a433-120">[搭配 HDInsight 使用 Oozie](hdinsight-use-oozie.md)：在 Oozie 工作流程中使用 Sqoop 動作。</span><span class="sxs-lookup"><span data-stu-id="4a433-120">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="4a433-121">[飛行延遲使用分析資料 HDInsight](hdinsight-analyze-flight-delay-data.md)： 使用 Hive tooanalyze 飛行延遲的資料，然後再使用 Sqoop tooexport 資料 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="4a433-121">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="4a433-122">[上傳資料 tooHDInsight](hdinsight-upload-data.md)： 尋找其他方法上, 傳資料 tooHDInsight/Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4a433-122">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
