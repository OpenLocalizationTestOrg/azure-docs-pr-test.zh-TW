---
title: "使用 .NET 和 HDInsight 執行 Sqoop 作業 - Azure | Microsoft Docs"
description: "了解如何在 Hadoop 叢集與 Azure SQL Database 之間使用 HDInsight .NET SDK 執行 Sqoop 匯入和匯出。"
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="f96fa-104">在 HDInsight 中使用 .NET SDK for Hadoop 執行 Sqoop 工作</span><span class="sxs-lookup"><span data-stu-id="f96fa-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="f96fa-105">了解如何在 HDInsight 上使用 HDInsight .NET SDK for Hadoop 執行 Sqoop 工作，以進行 HDInsight 叢集與 Azure SQL Database 或 SQL Server Database 之間的匯入和匯出作業。</span><span class="sxs-lookup"><span data-stu-id="f96fa-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="f96fa-106">本文中的步驟可以與以 Windows 為基礎或以 Linux 為基礎的 HDInsight 叢集搭配使用。不過，這些步驟只能從 Windows 用戶端運作。</span><span class="sxs-lookup"><span data-stu-id="f96fa-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="f96fa-107">您可使用本文頂端的索引標籤選取器，以選擇其他方法。</span><span class="sxs-lookup"><span data-stu-id="f96fa-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="f96fa-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="f96fa-108">Prerequisites</span></span>
<span data-ttu-id="f96fa-109">開始進行本教學課程之前，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="f96fa-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="f96fa-110">**HDInsight 中的 Hadoop 叢集**。</span><span class="sxs-lookup"><span data-stu-id="f96fa-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="f96fa-111">請參閱 [建立叢集與 SQL Database](hdinsight-use-sqoop.md#create-cluster-and-sql-database)。</span><span class="sxs-lookup"><span data-stu-id="f96fa-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="f96fa-112">使用 .NET SDK 在 HDInsight 叢集上使用 Sqoop</span><span class="sxs-lookup"><span data-stu-id="f96fa-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="f96fa-113">HDInsight .NET SDK 提供 .NET 用戶端程式庫，讓您輕鬆地從 .NET 使用 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="f96fa-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="f96fa-114">在本節中，您會建立 C# 主控台應用程式，將 hivesampletable 匯出至您稍早在本教學課程中建立的 SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="f96fa-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="f96fa-115">提交 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="f96fa-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="f96fa-116">在 Visual Studio 建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f96fa-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="f96fa-117">從 Visual Studio Package Manager Console 執行下列 Nuget 命令以匯入套件。</span><span class="sxs-lookup"><span data-stu-id="f96fa-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="f96fa-118">在 Program.cs 檔案中使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="f96fa-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="f96fa-119">按 **F5** 鍵執行程式。</span><span class="sxs-lookup"><span data-stu-id="f96fa-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="f96fa-120">限制</span><span class="sxs-lookup"><span data-stu-id="f96fa-120">Limitations</span></span>
* <span data-ttu-id="f96fa-121">大量匯出 - 使用 Linux 型 HDInsight，用來將資料匯出至 Microsoft SQL Server 或 Azure SQL Database 的 Sqoop 連接器目前不支援大量插入。</span><span class="sxs-lookup"><span data-stu-id="f96fa-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="f96fa-122">批次處理 - 使用以 Linux 為基礎的 HDInsight，執行插入時若使用 `-batch` 參數，Sqoop 將會執行多個插入，而不是將插入作業批次處理。</span><span class="sxs-lookup"><span data-stu-id="f96fa-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f96fa-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f96fa-123">Next steps</span></span>
<span data-ttu-id="f96fa-124">現在，您已了解如何使用 Sqoop。</span><span class="sxs-lookup"><span data-stu-id="f96fa-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="f96fa-125">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="f96fa-125">To learn more, see:</span></span>

* <span data-ttu-id="f96fa-126">[搭配 HDInsight 使用 Oozie](hdinsight-use-oozie.md)：在 Oozie 工作流程中使用 Sqoop 動作。</span><span class="sxs-lookup"><span data-stu-id="f96fa-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="f96fa-127">[使用 HDInsight 分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)：使用 Hive 分析航班誤點資料，然後使用 Sqoop 將資料匯出至 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="f96fa-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="f96fa-128">[將資料上傳至 HDInsight](hdinsight-upload-data.md)：尋找可將資料上傳至 HDInsight/Azure Blob 儲存體的其他方法。</span><span class="sxs-lookup"><span data-stu-id="f96fa-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

