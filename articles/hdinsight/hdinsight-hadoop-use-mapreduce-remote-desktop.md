---
title: "aaaMapReduce 和遠端桌面 HDInsight 的 Azure 中的 Hadoop |Microsoft 文件"
description: "深入了解如何 toouse 遠端桌面 tooconnect tooHadoop HDInsight 和執行的 MapReduce 工作上。"
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
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="a949d-103">利用遠端桌面在 HDInsight 上的 Hadoop 中使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="a949d-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="a949d-104">在本文中，您將學習如何 tooconnect tooa HDInsight 上的 Hadoop 叢集使用遠端桌面，並使用 hello Hadoop 命令，以執行 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="a949d-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a949d-105">只有在 Windows 型 HDInsight 叢集上才能使用「遠端桌面」。</span><span class="sxs-lookup"><span data-stu-id="a949d-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a949d-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="a949d-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a949d-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="a949d-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="a949d-108">HDInsight 3.4 或更高，請參閱[透過 SSH 使用 MapReduce](hdinsight-hadoop-use-mapreduce-ssh.md)連接 toohello HDInsight 叢集，並在執行 MapReduce 工作的資訊。</span><span class="sxs-lookup"><span data-stu-id="a949d-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="a949d-109"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="a949d-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="a949d-110">toocomplete hello 本文中的步驟，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="a949d-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="a949d-111">Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="a949d-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="a949d-112">執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="a949d-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="a949d-113"><a id="connect"></a>使用遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="a949d-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="a949d-114">Hello HDInsight 叢集，啟用遠端桌面，然後依照指示 hello 連接 tooit[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="a949d-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="a949d-115"><a id="hadoop"></a>使用 hello Hadoop 命令</span><span class="sxs-lookup"><span data-stu-id="a949d-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="a949d-116">當您連接的 toohello 桌面 hello HDInsight 叢集，請使用 hello 使用 hello Hadoop 命令遵循步驟 toorun MapReduce 工作：</span><span class="sxs-lookup"><span data-stu-id="a949d-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="a949d-117">從 hello HDInsight 桌面啟動 hello **Hadoop 命令列**。</span><span class="sxs-lookup"><span data-stu-id="a949d-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="a949d-118">這會開啟新的命令提示字元在 hello **c:\apps\dist\hadoop-&lt;版本號碼 >**目錄。</span><span class="sxs-lookup"><span data-stu-id="a949d-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a949d-119">hello 版本號碼變更為已更新的 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="a949d-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="a949d-120">hello **HADOOP_HOME**環境變數可以是使用的 toofind hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="a949d-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="a949d-121">例如，`cd %HADOOP_HOME%`變更目錄 toohello Hadoop 目錄中的，而不需要您 tooknow hello 版本號碼。</span><span class="sxs-lookup"><span data-stu-id="a949d-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="a949d-122">toouse hello **Hadoop**命令 toorun 範例 MapReduce 工作，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="a949d-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="a949d-123">這會啟動 hello **wordcount**類別，包含在 hello **hadoop-mapreduce-examples.jar** hello 目前目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a949d-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="a949d-124">做為輸入，它會使用 hello **wasb://example/data/gutenberg/davinci.txt**文件和輸出儲存在： **wasb: / 範例/資料/WordCountOutput**。</span><span class="sxs-lookup"><span data-stu-id="a949d-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a949d-125">如需此 MapReduce 作業和 hello 範例資料的詳細資訊，請參閱<a href="hdinsight-use-mapreduce.md">HDInsight Hadoop 中的使用 MapReduce</a>。</span><span class="sxs-lookup"><span data-stu-id="a949d-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="a949d-126">hello 作業會發出詳細資料，處理時，以及 hello 工作完成時，它會傳回類似 toohello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="a949d-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="a949d-127">Hello 工作完成時，使用下列命令 toolist hello 輸出檔案儲存在 hello **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="a949d-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="a949d-128">這應該會顯示兩個檔案：**_SUCCESS** 和 **part-r-00000**。</span><span class="sxs-lookup"><span data-stu-id="a949d-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="a949d-129">hello**一部分-r-00000**檔案包含這項作業的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="a949d-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a949d-130">某些 MapReduce 工作可能跨多個分割 hello 結果**# # r 一部分 #**檔案。</span><span class="sxs-lookup"><span data-stu-id="a949d-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="a949d-131">如果是，使用 hello # # # hello 檔案 tooindicate hello 順序後置詞。</span><span class="sxs-lookup"><span data-stu-id="a949d-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="a949d-132">下列命令使用 hello tooview hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="a949d-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="a949d-133">此顯示中的清單所包含的 hello 文字 hello **wasb://example/data/gutenberg/davinci.txt**檔案，以及發生每個單字的 hello 次數。</span><span class="sxs-lookup"><span data-stu-id="a949d-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="a949d-134">hello 以下是將包含在 hello 檔案中的 hello 資料的範例：</span><span class="sxs-lookup"><span data-stu-id="a949d-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="a949d-135"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="a949d-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="a949d-136">如您所見，hello Hadoop 命令提供簡單的方式 toorun MapReduce 工作的 HDInsight 叢集，然後再檢視 hello 作業輸出。</span><span class="sxs-lookup"><span data-stu-id="a949d-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="a949d-137"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="a949d-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="a949d-138">如需 HDInsight 中 MapReduce 工作的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="a949d-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="a949d-139">在 HDInsight Hadoop 上使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="a949d-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="a949d-140">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="a949d-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a949d-141">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="a949d-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a949d-142">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="a949d-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
