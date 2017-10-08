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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="1c592-103">使用 HDInsight .NET SDK 執行 MapReduce 作業</span><span class="sxs-lookup"><span data-stu-id="1c592-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="1c592-104">了解如何 toosubmit MapReduce 作業使用 HDInsight.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="1c592-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="1c592-105">HDInsight 叢集隨附內含一些 MapReduce 範例的 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="1c592-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="1c592-106">hello jar 檔案是*/example/jars/hadoop-mapreduce-examples.jar*。</span><span class="sxs-lookup"><span data-stu-id="1c592-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="1c592-107">其中一個 hello 範例是*wordcount*。</span><span class="sxs-lookup"><span data-stu-id="1c592-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="1c592-108">您開發 C# 主控台應用程式 toosubmit wordcount 作業。</span><span class="sxs-lookup"><span data-stu-id="1c592-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="1c592-109">hello 作業讀取 hello */example/data/gutenberg/davinci.txt*檔和輸出 hello 結果太*/example/data/davinciwordcount*。</span><span class="sxs-lookup"><span data-stu-id="1c592-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="1c592-110">如果您想 toorerun hello 應用程式，您必須清除 hello 輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="1c592-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="1c592-111">從 Windows 用戶端必須執行本文中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="1c592-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="1c592-112">使用 Linux、 OS X 或 Unix 用戶端 toowork Hive 與資訊，請使用上 hello hello 文章頂端顯示 hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="1c592-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1c592-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="1c592-113">Prerequisites</span></span>
<span data-ttu-id="1c592-114">在開始這份文件之前，您必須擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="1c592-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="1c592-115">**HDInsight 中的 Hadoop 叢集**。</span><span class="sxs-lookup"><span data-stu-id="1c592-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="1c592-116">請參閱[開始在 Hdinsight 中使用 Linux 型 Hadoop](./hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1c592-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="1c592-117">**Visual Studio 2013/2015/2017**。</span><span class="sxs-lookup"><span data-stu-id="1c592-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="1c592-118">使用 HDInsight .NET SDK 提交 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="1c592-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="1c592-119">hello HDInsight.NET SDK 提供.NET 用戶端程式庫，使其更容易 toowork 與.net 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1c592-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="1c592-120">**tooSubmit 工作**</span><span class="sxs-lookup"><span data-stu-id="1c592-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="1c592-121">在 Visual Studio 建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c592-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="1c592-122">Hello Nuget 封裝管理員主控台中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c592-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="1c592-123">使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="1c592-123">Use hello following code:</span></span>
   
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
4. <span data-ttu-id="1c592-124">按**F5** toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1c592-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="1c592-125">toorun hello 作業同樣地，您必須變更 hello 工作輸出的資料夾名稱中，在 hello 範例中，它是 「 / 範例/資料/davinciwordcount"。</span><span class="sxs-lookup"><span data-stu-id="1c592-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="1c592-126">Hello 工作成功完成時，hello 應用程式會列印 hello 輸出檔"組件-r-00000"hello 內容。</span><span class="sxs-lookup"><span data-stu-id="1c592-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c592-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c592-127">Next steps</span></span>
<span data-ttu-id="1c592-128">在本文中，您已經學會數種方式 toocreate 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="1c592-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="1c592-129">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="1c592-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="1c592-130">對於提交 Hive 作業，請參閱[使用 HDInsight.NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="1c592-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="1c592-131">如需建立 HDInsight 叢集，請參閱[在 HDInsight 中建立 Linux 型 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="1c592-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="1c592-132">如需管理 HDInsight 叢集，請參閱[在 HDInsight 中管理 Hadoop 叢集](hdinsight-administer-use-portal-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="1c592-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="1c592-133">基於學習的 hello HDInsight.NET SDK，請參閱[HDInsight.NET SDK 參考](https://msdn.microsoft.com/library/mt271028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1c592-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="1c592-134">針對非互動式驗證 tooAzure，請參閱[建立.NET HDInsight 應用程式的非互動式驗證](hdinsight-create-non-interactive-authentication-dotnet-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="1c592-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

