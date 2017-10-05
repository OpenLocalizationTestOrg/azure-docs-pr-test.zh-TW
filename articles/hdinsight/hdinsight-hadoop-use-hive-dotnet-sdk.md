---
title: "使用 HDInsight .NET SDK 執行 Hive 查詢 - Azure | Microsoft Docs"
description: "了解如何使用 HDInsight .NET SDK 將 Hadoop 工作提交至 Azure HDInsight Hadoop。"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 7b1a5f7ea3b2bda438727dc75a85557ea7930280
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="ae327-103">使用 HDInsight .NET SDK 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="ae327-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="ae327-104">了解如何使用 HDInsight .NET SDK 提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="ae327-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="ae327-105">您要撰寫 C# 程式來提交用於列出 Hive 資料表的 Hive 查詢，並顯示結果。</span><span class="sxs-lookup"><span data-stu-id="ae327-105">You write a C# program to submit a Hive query for listing Hive tables, and display the results.</span></span>

> [!NOTE]
> <span data-ttu-id="ae327-106">此文章中的步驟必須從 Windows 用戶端執行。</span><span class="sxs-lookup"><span data-stu-id="ae327-106">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="ae327-107">如需搭配 Linux、OS X 或 Unix 用戶端使用 Hive 的資訊，請使用本文頂端顯示的索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="ae327-107">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ae327-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="ae327-108">Prerequisites</span></span>
<span data-ttu-id="ae327-109">開始閱讀本文之前，您必須有下列各項：</span><span class="sxs-lookup"><span data-stu-id="ae327-109">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="ae327-110">**HDInsight 中的 Hadoop 叢集**。</span><span class="sxs-lookup"><span data-stu-id="ae327-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="ae327-111">請參閱[開始在 Hdinsight 中使用 Linux 型 Hadoop](./hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ae327-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="ae327-112">**Visual Studio 2013/2015/2017**。</span><span class="sxs-lookup"><span data-stu-id="ae327-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="ae327-113">使用 HDInsight .NET SDK 提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="ae327-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="ae327-114">HDInsight .NET SDK 提供 .NET 用戶端程式庫，讓您輕鬆地從 .NET 使用 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae327-114">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="ae327-115">**提交工作**</span><span class="sxs-lookup"><span data-stu-id="ae327-115">**To Submit jobs**</span></span>

1. <span data-ttu-id="ae327-116">在 Visual Studio 建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae327-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="ae327-117">從 NuGet Package Manager 主控台執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="ae327-117">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="ae327-118">使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="ae327-118">Use the following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
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
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the Hive job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
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
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="ae327-119">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae327-119">Press **F5** to run the application.</span></span>

<span data-ttu-id="ae327-120">應用程式的輸出應該類似這樣：</span><span class="sxs-lookup"><span data-stu-id="ae327-120">The output of the application shall be similar to:</span></span>

![HDInsight Hadoop Hive 作業輸出](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="ae327-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae327-122">Next steps</span></span>
<span data-ttu-id="ae327-123">在本文中，您學到幾種建立 HDInsight 叢集的方法。</span><span class="sxs-lookup"><span data-stu-id="ae327-123">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="ae327-124">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="ae327-124">To learn more, see the following articles:</span></span>

* <span data-ttu-id="ae327-125">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="ae327-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="ae327-126">[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="ae327-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="ae327-127">使用 Azure 入口網站管理 HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="ae327-127">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="ae327-128">HDInsight .NET SDK 參考</span><span class="sxs-lookup"><span data-stu-id="ae327-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="ae327-129">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="ae327-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ae327-130">搭配 HDInsight 使用 Sqoop</span><span class="sxs-lookup"><span data-stu-id="ae327-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="ae327-131">建立非互動式驗證 .NET HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="ae327-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


