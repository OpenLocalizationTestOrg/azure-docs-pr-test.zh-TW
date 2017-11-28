---
title: "aaaRun Apache Pig 工作 Hadoop-Azure HDInsight.NET sdk |Microsoft 文件"
description: "了解如何 toouse hello.NET SDK 上 HDInsight Hadoop toosubmit Pig 工作 tooHadoop。"
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
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="e6f36-103">執行 hello.NET SDK 用於 HDInsight 中的 Hadoop Pig 工作</span><span class="sxs-lookup"><span data-stu-id="e6f36-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="e6f36-104">了解 toouse hello.NET SDK 的 Hadoop toosubmit Apache Pig 工作 tooHadoop Azure HDInsight 上的方式。</span><span class="sxs-lookup"><span data-stu-id="e6f36-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="e6f36-105">hello HDInsight.NET SDK 提供可讓您更輕鬆 toowork 與 HDInsight 叢集與.NET 的.NET 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="e6f36-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="e6f36-106">Pig 可讓您 toocreate MapReduce 作業依照模型化一系列的資料轉換。</span><span class="sxs-lookup"><span data-stu-id="e6f36-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="e6f36-107">在本文件中，您學會如何 toouse 基本 C# 應用程式 toosubmit Pig 工作 tooan HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e6f36-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6f36-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="e6f36-108">Prerequisites</span></span>

<span data-ttu-id="e6f36-109">toocomplete hello 本文中的步驟，您需要下列 hello。</span><span class="sxs-lookup"><span data-stu-id="e6f36-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="e6f36-110">Azure HDInsight (HDInsight 上的 Hadoop) 叢集 (Windows 或 Linux 型)。</span><span class="sxs-lookup"><span data-stu-id="e6f36-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e6f36-111">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="e6f36-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e6f36-112">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="e6f36-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e6f36-113">Visual Studio 2012、2013、2015 或 2017。</span><span class="sxs-lookup"><span data-stu-id="e6f36-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="e6f36-114">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e6f36-114">Create hello application</span></span>

<span data-ttu-id="e6f36-115">hello HDInsight.NET SDK 提供.NET 用戶端程式庫，使其更容易 toowork 與.net 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e6f36-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="e6f36-116">從 hello**檔案**在 Visual Studio 中，選取功能表**新增**，然後選取 **專案**。</span><span class="sxs-lookup"><span data-stu-id="e6f36-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="e6f36-117">Hello 新專案中，類型或選取 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="e6f36-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="e6f36-118">屬性</span><span class="sxs-lookup"><span data-stu-id="e6f36-118">Property</span></span> | <span data-ttu-id="e6f36-119">值</span><span class="sxs-lookup"><span data-stu-id="e6f36-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="e6f36-120">類別</span><span class="sxs-lookup"><span data-stu-id="e6f36-120">Category</span></span> | <span data-ttu-id="e6f36-121">範本/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="e6f36-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="e6f36-122">範本</span><span class="sxs-lookup"><span data-stu-id="e6f36-122">Template</span></span> | <span data-ttu-id="e6f36-123">主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="e6f36-123">Console Application</span></span> |
   | <span data-ttu-id="e6f36-124">名稱</span><span class="sxs-lookup"><span data-stu-id="e6f36-124">Name</span></span> | <span data-ttu-id="e6f36-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="e6f36-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="e6f36-126">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="e6f36-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="e6f36-127">從 hello**工具**功能表上，選取**程式庫套件管理員**或**Nuget 套件管理員**，然後選取**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="e6f36-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="e6f36-128">tooinstall hello.NET SDK 封裝，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6f36-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="e6f36-129">從 方案總管 中，按兩下  **Program.cs** tooopen 它。</span><span class="sxs-lookup"><span data-stu-id="e6f36-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="e6f36-130">取代 hello 下列 hello 現有程式碼。</span><span class="sxs-lookup"><span data-stu-id="e6f36-130">Replace hello existing code with hello following.</span></span>

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
                System.Console.WriteLine("hello application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
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

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="e6f36-131">toostart hello 應用程式，請按**F5**。</span><span class="sxs-lookup"><span data-stu-id="e6f36-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="e6f36-132">tooexit hello 應用程式，請按**ENTER**。</span><span class="sxs-lookup"><span data-stu-id="e6f36-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="e6f36-133">摘要</span><span class="sxs-lookup"><span data-stu-id="e6f36-133">Summary</span></span>

<span data-ttu-id="e6f36-134">如您所見，hello Hadoop 的.NET SDK 可讓您 toocreate.NET 應用程式，提交 Pig 工作 tooan HDInsight 叢集，並監控 hello 工作狀態。</span><span class="sxs-lookup"><span data-stu-id="e6f36-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6f36-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6f36-135">Next steps</span></span>

<span data-ttu-id="e6f36-136">如需 HDInsight 中 Pig 的詳細資訊，請參閱[搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)。</span><span class="sxs-lookup"><span data-stu-id="e6f36-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="e6f36-137">如需有關使用 HDInsight Hadoop 的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="e6f36-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="e6f36-138">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="e6f36-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e6f36-139">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="e6f36-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
