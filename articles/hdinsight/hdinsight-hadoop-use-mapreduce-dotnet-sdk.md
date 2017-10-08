---
title: "使用 HDInsight.NET SDK Azure aaaSubmit MapReduce 作業 |Microsoft 文件"
description: "了解如何 toosubmit MapReduce 作業 tooAzure HDInsight Hadoop 使用 HDInsight.NET SDK。"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>使用 HDInsight .NET SDK 執行 MapReduce 作業
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

了解如何 toosubmit MapReduce 作業使用 HDInsight.NET SDK。 HDInsight 叢集隨附內含一些 MapReduce 範例的 jar 檔案。 hello jar 檔案是*/example/jars/hadoop-mapreduce-examples.jar*。  其中一個 hello 範例是*wordcount*。 您開發 C# 主控台應用程式 toosubmit wordcount 作業。  hello 作業讀取 hello */example/data/gutenberg/davinci.txt*檔和輸出 hello 結果太*/example/data/davinciwordcount*。  如果您想 toorerun hello 應用程式，您必須清除 hello 輸出資料夾。

> [!NOTE]
> 從 Windows 用戶端必須執行本文中的 hello 步驟。 使用 Linux、 OS X 或 Unix 用戶端 toowork Hive 與資訊，請使用上 hello hello 文章頂端顯示 hello 索引標籤選取器。
> 
> 

## <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列項目：

* **HDInsight 中的 Hadoop 叢集**。 請參閱[開始在 Hdinsight 中使用 Linux 型 Hadoop](./hdinsight-hadoop-linux-tutorial-get-started.md)。
* **Visual Studio 2013/2015/2017**。

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>使用 HDInsight .NET SDK 提交 MapReduce 工作
hello HDInsight.NET SDK 提供.NET 用戶端程式庫，使其更容易 toowork 與.net 的 HDInsight 叢集。 

**tooSubmit 工作**

1. 在 Visual Studio 建立 C# 主控台應用程式。
2. Hello Nuget 封裝管理員主控台中，執行下列命令的 hello:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. 使用下列程式碼的 hello:
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. 按**F5** toorun hello 應用程式。

toorun hello 作業同樣地，您必須變更 hello 工作輸出的資料夾名稱中，在 hello 範例中，它是 「 / 範例/資料/davinciwordcount"。

Hello 工作成功完成時，hello 應用程式會列印 hello 輸出檔"組件-r-00000"hello 內容。

## <a name="next-steps"></a>後續步驟
在本文中，您已經學會數種方式 toocreate 的 HDInsight 叢集。 toolearn 詳細資訊，請參閱下列文章 hello:

* 對於提交 Hive 作業，請參閱[使用 HDInsight.NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。
* 如需建立 HDInsight 叢集，請參閱[在 HDInsight 中建立 Linux 型 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。
* 如需管理 HDInsight 叢集，請參閱[在 HDInsight 中管理 Hadoop 叢集](hdinsight-administer-use-portal-linux.md)。
* 基於學習的 hello HDInsight.NET SDK，請參閱[HDInsight.NET SDK 參考](https://msdn.microsoft.com/library/mt271028.aspx)。
* 針對非互動式驗證 tooAzure，請參閱[建立.NET HDInsight 應用程式的非互動式驗證](hdinsight-create-non-interactive-authentication-dotnet-applications.md)。

