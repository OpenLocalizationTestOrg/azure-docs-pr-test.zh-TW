---
title: "使用 HDInsight.NET SDK Azure aaaRun Hive 查詢 |Microsoft 文件"
description: "了解如何 toosubmit Hadoop 作業 tooAzure HDInsight Hadoop 使用 HDInsight.NET SDK。"
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
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="69437-103">使用 HDInsight .NET SDK 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="69437-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="69437-104">了解如何 toosubmit Hive 查詢使用 HDInsight.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="69437-104">Learn how toosubmit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="69437-105">您撰寫 C# 程式 toosubmit 列出 Hive 資料表的 Hive 查詢，並顯示 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="69437-105">You write a C# program toosubmit a Hive query for listing Hive tables, and display hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="69437-106">從 Windows 用戶端必須執行本文中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="69437-106">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="69437-107">使用 Linux、 OS X 或 Unix 用戶端 toowork Hive 與資訊，請使用上 hello hello 文章頂端顯示 hello 索引標籤選取器。</span><span class="sxs-lookup"><span data-stu-id="69437-107">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="69437-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="69437-108">Prerequisites</span></span>
<span data-ttu-id="69437-109">在開始這份文件之前，您必須擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="69437-109">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="69437-110">**HDInsight 中的 Hadoop 叢集**。</span><span class="sxs-lookup"><span data-stu-id="69437-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="69437-111">請參閱[開始在 Hdinsight 中使用 Linux 型 Hadoop](./hdinsight-hadoop-linux-tutorial-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="69437-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="69437-112">**Visual Studio 2013/2015/2017**。</span><span class="sxs-lookup"><span data-stu-id="69437-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="69437-113">使用 HDInsight .NET SDK 提交 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="69437-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="69437-114">hello HDInsight.NET SDK 提供.NET 用戶端程式庫，使其更容易 toowork 與.net 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="69437-114">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="69437-115">**tooSubmit 工作**</span><span class="sxs-lookup"><span data-stu-id="69437-115">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="69437-116">在 Visual Studio 建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="69437-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="69437-117">Hello Nuget 封裝管理員主控台中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="69437-117">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="69437-118">使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="69437-118">Use hello following code:</span></span>

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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
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
4. <span data-ttu-id="69437-119">按**F5** toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="69437-119">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="69437-120">hello hello 應用程式的輸出應該類似於：</span><span class="sxs-lookup"><span data-stu-id="69437-120">hello output of hello application shall be similar to:</span></span>

![HDInsight Hadoop Hive 作業輸出](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="69437-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69437-122">Next steps</span></span>
<span data-ttu-id="69437-123">在本文中，您已經學會數種方式 toocreate 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="69437-123">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="69437-124">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="69437-124">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="69437-125">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="69437-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="69437-126">[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="69437-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="69437-127">透過 hello Azure 入口網站來管理 HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="69437-127">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="69437-128">HDInsight .NET SDK 參考</span><span class="sxs-lookup"><span data-stu-id="69437-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="69437-129">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="69437-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="69437-130">搭配 HDInsight 使用 Sqoop</span><span class="sxs-lookup"><span data-stu-id="69437-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="69437-131">建立非互動式驗證 .NET HDInsight 應用程式</span><span class="sxs-lookup"><span data-stu-id="69437-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


