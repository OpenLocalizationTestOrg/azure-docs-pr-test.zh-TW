---
title: "MapReduce 和遠端桌面與 HDInsight 中的 Hadoop - Azure | Microsoft Docs"
description: "了解如何使用遠端桌面連線到 HDInsight 上的 Hadoop，並執行 MapReduce 工作。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: b56674857b013f9bb3d4dd4b6e97b34e0a97b1b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="a979f-103">利用遠端桌面在 HDInsight 上的 Hadoop 中使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="a979f-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="a979f-104">在本文中，您將學習如何使用遠端桌面連線至 HDInsight 叢集上的 Hadoop，然後使用 Hadoop 命令執行 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="a979f-104">In this article, you will learn how to connect to a Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using the Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a979f-105">只有在 Windows 型 HDInsight 叢集上才能使用「遠端桌面」。</span><span class="sxs-lookup"><span data-stu-id="a979f-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a979f-106">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a979f-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a979f-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="a979f-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="a979f-108">針對 HDInsight 3.4 或更新版本，請參閱[使用 MapReduce 搭配 SSH](hdinsight-hadoop-use-mapreduce-ssh.md)，以了解如何連線到 HDInsight 叢集及執行 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="a979f-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting to the HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="a979f-109"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="a979f-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="a979f-110">若要完成本文中的步驟，您需要下列項目。</span><span class="sxs-lookup"><span data-stu-id="a979f-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="a979f-111">Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="a979f-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="a979f-112">執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="a979f-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="a979f-113"><a id="connect"></a>使用遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="a979f-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="a979f-114">依照 [使用 RDP 連線到 HDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)中的指示，為 HDInsight 叢集啟用遠端桌面，然後進行連線。</span><span class="sxs-lookup"><span data-stu-id="a979f-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="a979f-115"><a id="hadoop"></a>使用 Hadoop 命令</span><span class="sxs-lookup"><span data-stu-id="a979f-115"><a id="hadoop"></a>Use the Hadoop command</span></span>
<span data-ttu-id="a979f-116">當您連線到 HDInsight 叢集的桌面時，請使用下列步驟，利用 Hadoop 命令來執行 MapReduce 工作：</span><span class="sxs-lookup"><span data-stu-id="a979f-116">When you are connected to the desktop for the HDInsight cluster, use the following steps to run a MapReduce job by using the Hadoop command:</span></span>

1. <span data-ttu-id="a979f-117">從 HDInsight 桌面，啟動 **Hadoop 命令列**。</span><span class="sxs-lookup"><span data-stu-id="a979f-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span> <span data-ttu-id="a979f-118">這會在 **c:\apps\dist\hadoop-&lt;version number>** 目錄中開啟新的命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="a979f-118">This opens a new command prompt in the **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a979f-119">版本號碼會隨著 Hadoop 更新而變更。</span><span class="sxs-lookup"><span data-stu-id="a979f-119">The version number changes as Hadoop is updated.</span></span> <span data-ttu-id="a979f-120">**HADOOP_HOME** 環境變數可用來尋找路徑。</span><span class="sxs-lookup"><span data-stu-id="a979f-120">The **HADOOP_HOME** environment variable can be used to find the path.</span></span> <span data-ttu-id="a979f-121">例如， `cd %HADOOP_HOME%` 會將目錄變更為 Hadoop 目錄，而您並不需要知道版本號碼。</span><span class="sxs-lookup"><span data-stu-id="a979f-121">For example, `cd %HADOOP_HOME%` changes directories to the Hadoop directory, without requiring you to know the version number.</span></span>
   >
   >
2. <span data-ttu-id="a979f-122">若要使用 **Hadoop** 命令執行範例 MapReduce 工作，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a979f-122">To use the **Hadoop** command to run an example MapReduce job, use the following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="a979f-123">這樣會啟動 **wordcount** 類別 (內含於目前目錄的 **hadoop-mapreduce-examples.jar** 檔案中)。</span><span class="sxs-lookup"><span data-stu-id="a979f-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file in the current directory.</span></span> <span data-ttu-id="a979f-124">作為輸入則會使用 **wasb://example/data/gutenberg/davinci.txt** 文件，且輸出會儲存在 **wasb:///example/data/WordCountOutput**。</span><span class="sxs-lookup"><span data-stu-id="a979f-124">As input, it uses the **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a979f-125">如需有關此 MapReduce 工作和範例資料的詳細資訊，請參閱<a href="hdinsight-use-mapreduce.md">在 HDInsight Hadoop 上使用 MapReduce</a>。</span><span class="sxs-lookup"><span data-stu-id="a979f-125">for more information about this MapReduce job and the example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="a979f-126">工作會在處理時發出詳細資料，並於工作完成時傳回與下列類似的資訊：</span><span class="sxs-lookup"><span data-stu-id="a979f-126">The job emits details as it is processed, and it returns information similar to the following when the job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="a979f-127">工作完成之後，請使用下列命令來列出儲存在 **wasb://example/data/WordCountOutput** 的輸出檔：</span><span class="sxs-lookup"><span data-stu-id="a979f-127">When the job is complete, use the following command to list the output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="a979f-128">這應該會顯示兩個檔案：**_SUCCESS** 和 **part-r-00000**。</span><span class="sxs-lookup"><span data-stu-id="a979f-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="a979f-129">**part-r-00000** 檔案包含這項工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="a979f-129">The **part-r-00000** file contains the output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a979f-130">某些 MapReduce 工作可能會將結果分成多個 **part-r-#####** 檔案。</span><span class="sxs-lookup"><span data-stu-id="a979f-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="a979f-131">若是如此，請使用 ##### 尾碼指出檔案的順序。</span><span class="sxs-lookup"><span data-stu-id="a979f-131">If so, use the ##### suffix to indicate the order of the files.</span></span>
   >
   >
5. <span data-ttu-id="a979f-132">若要檢視輸出，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a979f-132">To view the output, use the following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="a979f-133">這會顯示 **wasb://example/data/gutenberg/davinci.txt** 檔案中所含的單字清單，以及每個單字的出現次數。</span><span class="sxs-lookup"><span data-stu-id="a979f-133">This displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file, along with the number of times each word occured.</span></span> <span data-ttu-id="a979f-134">以下是要包含在檔案中之資料的範例：</span><span class="sxs-lookup"><span data-stu-id="a979f-134">The following is an example of the data that will be contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="a979f-135"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="a979f-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="a979f-136">如您所見，Hadoop 命令提供簡單的方法，在 HDInsight 叢集上執行 MapReduce 工作，然後檢視工作輸出。</span><span class="sxs-lookup"><span data-stu-id="a979f-136">As you can see, the Hadoop command provides an easy way to run MapReduce jobs on an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="a979f-137"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="a979f-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="a979f-138">如需 HDInsight 中 MapReduce 工作的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="a979f-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="a979f-139">在 HDInsight Hadoop 上使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="a979f-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="a979f-140">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="a979f-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a979f-141">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="a979f-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a979f-142">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="a979f-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
