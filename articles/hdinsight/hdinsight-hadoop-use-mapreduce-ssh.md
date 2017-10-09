---
title: "aaaMapReduce 和 SSH 連線，HDInsight 的 Azure 中的 Hadoop |Microsoft 文件"
description: "了解如何 toouse SSH toorun MapReduce 作業使用 HDInsight Hadoop。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="ff27d-103">搭配使用 MapReduce 與 HDInsight 上的 Hadoop 和 SSH</span><span class="sxs-lookup"><span data-stu-id="ff27d-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="ff27d-104">了解從安全殼層 (SSH) 連線 tooHDInsight toosubmit MapReduce 作業的方式。</span><span class="sxs-lookup"><span data-stu-id="ff27d-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="ff27d-105">如果您已經熟悉使用 linux Hadoop 伺服器，但您新 tooHDInsight 資訊，請參閱[以 Linux 為基礎的 HDInsight 秘訣](hdinsight-hadoop-linux-information.md)。</span><span class="sxs-lookup"><span data-stu-id="ff27d-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="ff27d-106"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="ff27d-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="ff27d-107">Linux 型 HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="ff27d-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ff27d-108">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="ff27d-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ff27d-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="ff27d-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ff27d-110">SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ff27d-110">An SSH client.</span></span> <span data-ttu-id="ff27d-111">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="ff27d-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="ff27d-112"><a id="ssh"></a>使用 SSH 連線</span><span class="sxs-lookup"><span data-stu-id="ff27d-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="ff27d-113">Toohello 叢集使用 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="ff27d-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="ff27d-114">比方說，下列命令的 hello 連接名為 tooa 叢集**myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="ff27d-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="ff27d-115">**如果您使用的 SSH 驗證的憑證金鑰**，您可能需要在用戶端系統上，hello 私用金鑰 toospecify hello 位置，例如：</span><span class="sxs-lookup"><span data-stu-id="ff27d-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="ff27d-116">**如果您使用的密碼 SSH 驗證**，您需要 tooprovide hello 密碼提示。</span><span class="sxs-lookup"><span data-stu-id="ff27d-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="ff27d-117">如需搭配 HDInsight 使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="ff27d-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="ff27d-118"><a id="hadoop"></a>使用 Hadoop 命令</span><span class="sxs-lookup"><span data-stu-id="ff27d-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="ff27d-119">連接的 toohello HDInsight 叢集後，請使用下列命令 toostart MapReduce 工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff27d-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="ff27d-120">此命令會啟動 hello`wordcount`類別，包含在 hello`hadoop-mapreduce-examples.jar`檔案。</span><span class="sxs-lookup"><span data-stu-id="ff27d-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="ff27d-121">它會使用 hello`/example/data/gutenberg/davinci.txt`做為輸入，並輸出文件儲存在`/example/data/WordCountOutput`。</span><span class="sxs-lookup"><span data-stu-id="ff27d-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff27d-122">如需此 MapReduce 作業和 hello 範例資料的詳細資訊，請參閱[在 HDInsight 上的 Hadoop 使用 MapReduce](hdinsight-use-mapreduce.md)。</span><span class="sxs-lookup"><span data-stu-id="ff27d-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="ff27d-123">hello 作業處理，以及它會傳回資訊的類似 toohello hello 作業完成時，下列文字，會發出詳細資料：</span><span class="sxs-lookup"><span data-stu-id="ff27d-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="ff27d-124">Hello 作業完成時，請使用下列命令 toolist hello 輸出檔案的 hello:</span><span class="sxs-lookup"><span data-stu-id="ff27d-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="ff27d-125">此命令會顯示兩個檔案︰`_SUCCESS` 和 `part-r-00000`。</span><span class="sxs-lookup"><span data-stu-id="ff27d-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="ff27d-126">hello`part-r-00000`檔案包含這項作業的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="ff27d-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ff27d-127">某些 MapReduce 工作可能跨多個分割 hello 結果**# # r 一部分 #**檔案。</span><span class="sxs-lookup"><span data-stu-id="ff27d-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="ff27d-128">如果是，使用 hello # # # hello 檔案 tooindicate hello 順序後置詞。</span><span class="sxs-lookup"><span data-stu-id="ff27d-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="ff27d-129">下列命令使用 hello tooview hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="ff27d-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="ff27d-130">此命令會顯示一份所包含的 hello 文字中 hello **wasb://example/data/gutenberg/davinci.txt**檔案和 hello 的每個單字發生次數。</span><span class="sxs-lookup"><span data-stu-id="ff27d-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="ff27d-131">hello 下列文字是包含在 hello 檔案中的 hello 資料的範例：</span><span class="sxs-lookup"><span data-stu-id="ff27d-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="ff27d-132"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="ff27d-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="ff27d-133">如您所見，Hadoop 命令也提供簡單的方式 toorun MapReduce 工作的 HDInsight 叢集，然後檢視 hello 作業輸出。</span><span class="sxs-lookup"><span data-stu-id="ff27d-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="ff27d-134"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="ff27d-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ff27d-135">如需 HDInsight 中 MapReduce 工作的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="ff27d-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="ff27d-136">在 HDInsight Hadoop 上使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="ff27d-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="ff27d-137">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="ff27d-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ff27d-138">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ff27d-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ff27d-139">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ff27d-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
