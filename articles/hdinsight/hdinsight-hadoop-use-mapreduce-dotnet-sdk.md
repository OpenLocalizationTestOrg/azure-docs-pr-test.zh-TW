---
title: "使用 HDInsight .NET SDK 提交 MapReduce 作業 - Azure | Microsoft Docs"
description: "了解如何使用 HDInsight .NET SDK 將 MapReduce 作業提交至 Azure HDInsight Hadoop。"
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
ms.openlocfilehash: 015435270c31bafea0ebf5303b459338755c1410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="17b9b-103">使用 HDInsight .NET SDK 執行 MapReduce 作業</span><span class="sxs-lookup"><span data-stu-id="17b9b-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="17b9b-104">了解如何使用 HDInsight .NET SDK 提交 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="17b9b-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="17b9b-105">HDInsight 叢集隨附內含一些 MapReduce 範例的 jar 檔案。</span><span class="sxs-lookup"><span data-stu-id="17b9b-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="17b9b-106">此 jar 檔案是 /example/jars/hadoop-mapreduce-examples.jar。</span><span class="sxs-lookup"><span data-stu-id="17b9b-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="17b9b-107">其中一個範例是 wordcount。</span><span class="sxs-lookup"><span data-stu-id="17b9b-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="17b9b-108">您可開發 C# 主控台應用程式以提交 wordcount 作業。</span><span class="sxs-lookup"><span data-stu-id="17b9b-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="17b9b-109">此作業會讀取 /example/data/gutenberg/davinci.txt 檔案，並將結果輸出至 /example/data/davinciwordcount。</span><span class="sxs-lookup"><span data-stu-id="17b9b-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="17b9b-110">如果您想要重新執行應用程式，您必須清除輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="17b9b-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="17b9b-111">此文章中的步驟必須從 Windows 用戶端執行。</span><span class="sxs-lookup"><span data-stu-id="17b9b-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="17b9b-112">如需搭配 Linux、OS X 或 Unix 用戶端使用 Hive 的資訊，請使用本文頂端顯示的索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="17b9b-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="17b9b-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="17b9b-113">Prerequisites</span></span>
<span data-ttu-id="17b9b-114">開始閱讀本文之前，您必須有下列各項：</span><span class="sxs-lookup"><span data-stu-id="17b9b-114">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="17b9b-115">**HDInsight 中的 Hadoop 叢集**。</span><span class="sxs-lookup"><span data-stu-id="17b9b-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="17b9b-116">請參閱[開始在 Hdinsight 中使用 Linux 型 Hadoop](./hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="17b9b-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="17b9b-117">**Visual Studio 2013/2015/2017**。</span><span class="sxs-lookup"><span data-stu-id="17b9b-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="17b9b-118">使用 HDInsight .NET SDK 提交 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="17b9b-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="17b9b-119">HDInsight .NET SDK 提供 .NET 用戶端程式庫，讓您輕鬆地從 .NET 使用 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="17b9b-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="17b9b-120">**提交工作**</span><span class="sxs-lookup"><span data-stu-id="17b9b-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="17b9b-121">在 Visual Studio 建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b9b-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="17b9b-122">從 NuGet Package Manager 主控台執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="17b9b-122">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="17b9b-123">使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="17b9b-123">Use the following code:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the MR job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
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
                        // Create the storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create the blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference to a previously created container.
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
4. <span data-ttu-id="17b9b-124">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="17b9b-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="17b9b-125">若要再次執行作業，您必須變更範例中的作業輸出資料夾名稱，在此範例中，它是 "/example/data/davinciwordcount"。</span><span class="sxs-lookup"><span data-stu-id="17b9b-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="17b9b-126">作業順利完成時，應用程式會顯示檔案 "part-r-00000" 的內容。</span><span class="sxs-lookup"><span data-stu-id="17b9b-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="17b9b-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17b9b-127">Next steps</span></span>
<span data-ttu-id="17b9b-128">在本文中，您學到幾種建立 HDInsight 叢集的方法。</span><span class="sxs-lookup"><span data-stu-id="17b9b-128">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="17b9b-129">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="17b9b-129">To learn more, see the following articles:</span></span>

* <span data-ttu-id="17b9b-130">對於提交 Hive 作業，請參閱[使用 HDInsight.NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="17b9b-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="17b9b-131">如需建立 HDInsight 叢集，請參閱[在 HDInsight 中建立 Linux 型 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="17b9b-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="17b9b-132">如需管理 HDInsight 叢集，請參閱[在 HDInsight 中管理 Hadoop 叢集](hdinsight-administer-use-portal-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="17b9b-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="17b9b-133">如需了解 HDInsight .NET SDK，請參閱 [HDInsight .NET SDK 參考](https://msdn.microsoft.com/library/mt271028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="17b9b-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="17b9b-134">若要向 Azure 進行非互動式驗證，請參閱[建立非互動式驗證 .NET HDInsight 應用程式](hdinsight-create-non-interactive-authentication-dotnet-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="17b9b-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

