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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>在 HDInsight 中使用 .NET SDK for Hadoop 執行 Sqoop 工作
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

了解 toouse HDInsight.NET SDK toorun Sqoop HDInsight tooimport 中的工作，並匯出 HDInsight 叢集和 Azure SQL database 或 SQL Server 資料庫之間。

> [!NOTE]
> 可以使用本文章中的 hello 步驟與任一 Windows 或 Linux 的 HDInsight 叢集。不過，這些步驟只會從 Windows 用戶端工作。 此文章 toochoose 的 hello 頂端上其他方法使用 hello 索引標籤選取器。
> 
> 

### <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須具備下列項目 hello:

* **HDInsight 中的 Hadoop 叢集**。 請參閱 [建立叢集與 SQL Database](hdinsight-use-sqoop.md#create-cluster-and-sql-database)。

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>使用 .NET SDK 在 HDInsight 叢集上使用 Sqoop
hello HDInsight.NET SDK 提供.NET 用戶端程式庫，使其更容易 toowork 與.net 的 HDInsight 叢集。 在本節中，您建立的 C# 主控台應用程式 tooexport hello hivesampletable toohello SQL Database 資料表您稍早在本教學課程中建立。

## <a name="submit-a-sqoop-job"></a>提交 Sqoop 作業

1. 在 Visual Studio 建立 C# 主控台應用程式。
2. 從 hello Visual Studio Package Manager Console 中，執行下列 Nuget 命令 tooimport hello 套件 hello。
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. 使用下列程式碼 hello Program.cs 檔案中的 hello:
   
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
4. 按**F5** toorun hello 程式。 

## <a name="limitations"></a>限制
* 大量匯出的以 Linux 為基礎的 HDInsight、 hello Sqoop 使用連接器 tooexport 資料 tooMicrosoft SQL Server 或 Azure SQL Database 目前不支援大量插入。
* 批次處理-與 linux 的 HDInsight，當使用 hello`-batch`參數執行插入時，Sqoop 執行而不是批次處理 hello 插入作業的多個插入。

## <a name="next-steps"></a>後續步驟
現在您已經學會如何 toouse Sqoop。 toolearn 詳細資訊，請參閱：

* [搭配 HDInsight 使用 Oozie](hdinsight-use-oozie.md)：在 Oozie 工作流程中使用 Sqoop 動作。
* [飛行延遲使用分析資料 HDInsight](hdinsight-analyze-flight-delay-data.md)： 使用 Hive tooanalyze 飛行延遲的資料，然後再使用 Sqoop tooexport 資料 tooan Azure SQL database。
* [上傳資料 tooHDInsight](hdinsight-upload-data.md)： 尋找其他方法上, 傳資料 tooHDInsight/Azure Blob 儲存體。

