---
title: "使用.NET 和 HDInsight 的 Azure aaaRun Sqoop 作業 |Microsoft 文件"
description: "了解如何 toouse HDInsight.NET SDK toorun Sqoop 匯入和匯出的 Hadoop 叢集和 Azure SQL database 之間。"
keywords: "Sqoop 作業"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="e2c5c-104">在 HDInsight 中使用 .NET SDK for Hadoop 執行 Sqoop 工作</span><span class="sxs-lookup"><span data-stu-id="e2c5c-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="e2c5c-105">了解 toouse HDInsight.NET SDK toorun Sqoop HDInsight tooimport 中的工作，並匯出 HDInsight 叢集和 Azure SQL database 或 SQL Server 資料庫之間。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="e2c5c-106">可以使用本文章中的 hello 步驟與任一 Windows 或 Linux 的 HDInsight 叢集。不過，這些步驟只會從 Windows 用戶端工作。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="e2c5c-107">此文章 toochoose 的 hello 頂端上其他方法使用 hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="e2c5c-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="e2c5c-108">Prerequisites</span></span>
<span data-ttu-id="e2c5c-109">開始本教學課程之前，您必須具備下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e2c5c-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="e2c5c-110">**HDInsight 中的 Hadoop 叢集**。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="e2c5c-111">請參閱 [建立叢集與 SQL Database](hdinsight-use-sqoop.md#create-cluster-and-sql-database)。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="e2c5c-112">使用 .NET SDK 在 HDInsight 叢集上使用 Sqoop</span><span class="sxs-lookup"><span data-stu-id="e2c5c-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="e2c5c-113">hello HDInsight.NET SDK 提供.NET 用戶端程式庫，使其更容易 toowork 與.net 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="e2c5c-114">在本節中，您建立的 C# 主控台應用程式 tooexport hello hivesampletable toohello SQL Database 資料表您稍早在本教學課程中建立。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="e2c5c-115">提交 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="e2c5c-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="e2c5c-116">在 Visual Studio 建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="e2c5c-117">從 hello Visual Studio Package Manager Console 中，執行下列 Nuget 命令 tooimport hello 套件 hello。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="e2c5c-118">使用下列程式碼 hello Program.cs 檔案中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e2c5c-118">Use hello following code in hello Program.cs file:</span></span>
   
        using System.Collections.Generic;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="e2c5c-119">按**F5** toorun hello 程式。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="e2c5c-120">限制</span><span class="sxs-lookup"><span data-stu-id="e2c5c-120">Limitations</span></span>
* <span data-ttu-id="e2c5c-121">大量匯出的以 Linux 為基礎的 HDInsight、 hello Sqoop 使用連接器 tooexport 資料 tooMicrosoft SQL Server 或 Azure SQL Database 目前不支援大量插入。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="e2c5c-122">批次處理-與 linux 的 HDInsight，當使用 hello`-batch`參數執行插入時，Sqoop 執行而不是批次處理 hello 插入作業的多個插入。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2c5c-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2c5c-123">Next steps</span></span>
<span data-ttu-id="e2c5c-124">現在您已經學會如何 toouse Sqoop。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="e2c5c-125">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="e2c5c-125">toolearn more, see:</span></span>

* <span data-ttu-id="e2c5c-126">[搭配 HDInsight 使用 Oozie](hdinsight-use-oozie.md)：在 Oozie 工作流程中使用 Sqoop 動作。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="e2c5c-127">[飛行延遲使用分析資料 HDInsight](hdinsight-analyze-flight-delay-data.md)： 使用 Hive tooanalyze 飛行延遲的資料，然後再使用 Sqoop tooexport 資料 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="e2c5c-128">[上傳資料 tooHDInsight](hdinsight-upload-data.md)： 尋找其他方法上, 傳資料 tooHDInsight/Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e2c5c-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

