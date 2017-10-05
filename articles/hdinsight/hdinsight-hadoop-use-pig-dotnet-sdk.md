---
title: "使用 .NET SDK for Hadoop 執行 Apache Pig 工作 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 .NET SDK for Hadoop 將 Pig 工作提交至 HDInsight 上的 Hadoop。"
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: e40d152821b36852c447d5a3adfd39114edbbace
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="079e1-103">在 HDInsight 中使用 .NET SDK for Hadoop 執行 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="079e1-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="079e1-104">了解如何使用 .NET SDK for Hadoop 將 Apache Pig 工作提交至 Azure HDInsight 上的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="079e1-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="079e1-105">HDInsight .NET SDK 提供 .NET 用戶端程式庫，讓您輕鬆地從 .NET 使用 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="079e1-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="079e1-106">Pig 可讓您透過建立一系列資料轉換的模型，來建立 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="079e1-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="079e1-107">在本文件中，您會學習如何使用基本 C# 應用程式將 Pig 作業提交至 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="079e1-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="079e1-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="079e1-108">Prerequisites</span></span>

<span data-ttu-id="079e1-109">若要完成這篇文章中的步驟，您需要下列項目。</span><span class="sxs-lookup"><span data-stu-id="079e1-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="079e1-110">Azure HDInsight (HDInsight 上的 Hadoop) 叢集 (Windows 或 Linux 型)。</span><span class="sxs-lookup"><span data-stu-id="079e1-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="079e1-111">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="079e1-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="079e1-112">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="079e1-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="079e1-113">Visual Studio 2012、2013、2015 或 2017。</span><span class="sxs-lookup"><span data-stu-id="079e1-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="079e1-114">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="079e1-114">Create the application</span></span>

<span data-ttu-id="079e1-115">HDInsight .NET SDK 提供 .NET 用戶端程式庫，讓您輕鬆地從 .NET 使用 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="079e1-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="079e1-116">從 Visual Studio 的 [檔案] 功能表中，選取 [新增]，然後選取 [專案]。</span><span class="sxs-lookup"><span data-stu-id="079e1-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="079e1-117">對於新的專案，輸入或選取下列值：</span><span class="sxs-lookup"><span data-stu-id="079e1-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="079e1-118">屬性</span><span class="sxs-lookup"><span data-stu-id="079e1-118">Property</span></span> | <span data-ttu-id="079e1-119">值</span><span class="sxs-lookup"><span data-stu-id="079e1-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="079e1-120">類別</span><span class="sxs-lookup"><span data-stu-id="079e1-120">Category</span></span> | <span data-ttu-id="079e1-121">範本/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="079e1-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="079e1-122">範本</span><span class="sxs-lookup"><span data-stu-id="079e1-122">Template</span></span> | <span data-ttu-id="079e1-123">主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="079e1-123">Console Application</span></span> |
   | <span data-ttu-id="079e1-124">名稱</span><span class="sxs-lookup"><span data-stu-id="079e1-124">Name</span></span> | <span data-ttu-id="079e1-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="079e1-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="079e1-126">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="079e1-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="079e1-127">從 [工具] 功能表中，選取 [程式庫封裝管理員] 或 [Nuget 封裝管理員]，然後選取 [封裝管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="079e1-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="079e1-128">若要安裝 .NET SDK 封裝，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="079e1-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="079e1-129">在 [方案總管] 中，按兩下 **Program.cs** 加以開啟。</span><span class="sxs-lookup"><span data-stu-id="079e1-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="079e1-130">將現有程式碼取代為下者。</span><span class="sxs-lookup"><span data-stu-id="079e1-130">Replace the existing code with the following.</span></span>

    ```csharp
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

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="079e1-131">若要啟動應用程式，請按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="079e1-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="079e1-132">若要結束應用程式，請按 **ENTER**。</span><span class="sxs-lookup"><span data-stu-id="079e1-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="079e1-133">摘要</span><span class="sxs-lookup"><span data-stu-id="079e1-133">Summary</span></span>

<span data-ttu-id="079e1-134">如您所見，.NET SDK for Hadoop 可讓您建立 .NET 應用程式，以將 Pig 作業提交至 HDInsight 叢集，以及監視作業狀態。</span><span class="sxs-lookup"><span data-stu-id="079e1-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="079e1-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="079e1-135">Next steps</span></span>

<span data-ttu-id="079e1-136">如需 HDInsight 中 Pig 的詳細資訊，請參閱[搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)。</span><span class="sxs-lookup"><span data-stu-id="079e1-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="079e1-137">如需在 HDInsight 上使用 Hadoop 的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="079e1-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="079e1-138">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="079e1-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="079e1-139">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="079e1-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
