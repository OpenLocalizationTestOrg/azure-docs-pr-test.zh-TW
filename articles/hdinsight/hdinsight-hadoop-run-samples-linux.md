---
title: "HDInsight 的 Azure 上 aaaRun Hadoop MapReduce 範例 |Microsoft 文件"
description: "開始使用 HDInsight 中隨附的 jar 檔案中的 MapReduce 範例。 使用 SSH tooconnect toohello 叢集，然後再使用 hello Hadoop 命令 toorun 範例工作。"
keywords: "hadoop 範例 jar、Hadoop 範例 jar、hadoop mapreduce 範例、mapreduce 範例"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="e485d-105">執行包含在 HDInsight 中的 hello MapReduce 範例</span><span class="sxs-lookup"><span data-stu-id="e485d-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="e485d-106">了解如何 toorun hello MapReduce 範例隨附在 HDInsight Hadoop。</span><span class="sxs-lookup"><span data-stu-id="e485d-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e485d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="e485d-107">Prerequisites</span></span>

* <span data-ttu-id="e485d-108">**HDInsight 叢集**：請參閱 [在 Linux 上開始在 HDInsight 中搭配使用 Hadoop 與 Hive](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="e485d-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e485d-109">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="e485d-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e485d-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="e485d-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e485d-111">**SSH 用戶端**：如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="e485d-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="e485d-112">hello MapReduce 範例</span><span class="sxs-lookup"><span data-stu-id="e485d-112">hello MapReduce examples</span></span>

<span data-ttu-id="e485d-113">**位置**: hello 範例位於 HDInsight 叢集在 hello `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`。</span><span class="sxs-lookup"><span data-stu-id="e485d-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="e485d-114">**內容**: hello 下列範例包含在此封存中：</span><span class="sxs-lookup"><span data-stu-id="e485d-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="e485d-115">`aggregatewordcount`： 彙總以計算 hello 輸入檔中的 hello 文字的 mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="e485d-116">`aggregatewordhist`： 彙總以計算 hello 輸入檔中的 hello 文字的 hello 長條圖的 mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="e485d-117">`bbp`： 使用 Pi 的 Bailey-Borwein-Plouffe toocompute 完全位數 mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="e485d-118">`dbcount`： 計算儲存在資料庫中的 hello pageview 記錄檔這是範例工作。</span><span class="sxs-lookup"><span data-stu-id="e485d-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="e485d-119">`distbbp`: 使用 BBP 類型公式 toocompute 確切位元的 Pi mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="e485d-120">`grep`: Regex hello 輸入中會比對計算 hello mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="e485d-121">`join`：作業，可執行已排序且平均分割之資料集的聯結。</span><span class="sxs-lookup"><span data-stu-id="e485d-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="e485d-122">`multifilewc`：可從數個檔案計算字數的作業。</span><span class="sxs-lookup"><span data-stu-id="e485d-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="e485d-123">`pentomino`： 用來配置程式 toofind 解決方案 toopentomino 問題 mapreduce 磚。</span><span class="sxs-lookup"><span data-stu-id="e485d-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="e485d-124">`pi`：mapreduce 程式，使用擬蒙特卡羅 (quasi-Monte Carlo) 方法估計 Pi。</span><span class="sxs-lookup"><span data-stu-id="e485d-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="e485d-125">`randomtextwriter`：mapreduce 程式，可為每個節點寫入 10 GB 的隨機文字資料。</span><span class="sxs-lookup"><span data-stu-id="e485d-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="e485d-126">`randomwriter`：mapreduce 程式，可為每個節點寫入 10 GB 的隨機資料。</span><span class="sxs-lookup"><span data-stu-id="e485d-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="e485d-127">`secondarysort`: 定義次要排序 toohello 範例減少階段。</span><span class="sxs-lookup"><span data-stu-id="e485d-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="e485d-128">`sort`： 排序 hello hello 隨機寫入器寫入的資料 mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="e485d-129">`sudoku`：數獨解答程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="e485d-130">`teragen`： 產生 hello terasort 資料。</span><span class="sxs-lookup"><span data-stu-id="e485d-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="e485d-131">`terasort`： 執行 hello terasort。</span><span class="sxs-lookup"><span data-stu-id="e485d-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="e485d-132">`teravalidate`：檢查 TeraSort 的結果。</span><span class="sxs-lookup"><span data-stu-id="e485d-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="e485d-133">`wordcount`： 計算 hello 輸入檔中的 hello 文字 mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="e485d-134">`wordmean`： 計算 hello 輸入檔中的 hello 文字 hello 平均長度 mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="e485d-135">`wordmedian`： 計算 hello hello 輸入檔中的 hello 文字的中間值的長度 mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="e485d-136">`wordstandarddeviation`： 計算 hello hello 輸入檔中的 hello 文字長度的 hello 標準差 mapreduce 程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="e485d-137">**原始碼**： 這些範例的原始程式碼包含 HDInsight 叢集在 hello `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`。</span><span class="sxs-lookup"><span data-stu-id="e485d-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="e485d-138">hello`2.2.4.9-1`在 hello 路徑是 hello 新版 hello Hortonworks Data Platform hello HDInsight 叢集，而且可能會因您的叢集的。</span><span class="sxs-lookup"><span data-stu-id="e485d-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="e485d-139">執行 hello wordcount 範例</span><span class="sxs-lookup"><span data-stu-id="e485d-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="e485d-140">連接使用 SSH tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="e485d-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="e485d-141">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="e485d-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e485d-142">從 hello`username@#######:~$`提示，請使用下列命令 toolist hello 範例 hello:</span><span class="sxs-lookup"><span data-stu-id="e485d-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="e485d-143">此命令會從 hello 本文件的上一節中產生 hello 清單的範例。</span><span class="sxs-lookup"><span data-stu-id="e485d-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="e485d-144">使用 hello 下列命令 tooget 說明特定的範例。</span><span class="sxs-lookup"><span data-stu-id="e485d-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="e485d-145">在此情況下，hello **wordcount**範例：</span><span class="sxs-lookup"><span data-stu-id="e485d-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="e485d-146">您會收到下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="e485d-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="e485d-147">此訊息表示您可以為 hello 來源文件提供數個輸入的路徑。</span><span class="sxs-lookup"><span data-stu-id="e485d-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="e485d-148">hello 最後一個路徑是儲存 hello 輸出 （hello 來源文件中文字的計數）。</span><span class="sxs-lookup"><span data-stu-id="e485d-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="e485d-149">Hello 筆記本的達文西，與您的叢集提供做為範例資料中使用下列 toocount hello 所有文字：</span><span class="sxs-lookup"><span data-stu-id="e485d-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="e485d-150">此作業的輸入讀取自 `/example/data/gutenberg/davinci.txt`。</span><span class="sxs-lookup"><span data-stu-id="e485d-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="e485d-151">此範例的輸出會儲存在 `/example/data/davinciwordcount`。</span><span class="sxs-lookup"><span data-stu-id="e485d-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="e485d-152">這兩個路徑都位於 hello 叢集中，hello 本機檔案系統的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="e485d-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e485d-153">Hello hello wordcount 範例說明所述，您也可以指定多個輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="e485d-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="e485d-154">例如， `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` 會計算 davinci.txt 和 ulysses.txt 中的字數。</span><span class="sxs-lookup"><span data-stu-id="e485d-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="e485d-155">Hello 作業完成之後，請使用下列命令 tooview hello 輸出 hello:</span><span class="sxs-lookup"><span data-stu-id="e485d-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="e485d-156">此命令會串連 hello 作業所產生的所有 hello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="e485d-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="e485d-157">它會顯示 hello 輸出 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="e485d-157">It displays hello output toohello console.</span></span> <span data-ttu-id="e485d-158">hello 輸出是類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="e485d-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="e485d-159">每一列代表 word 和 hello 在發生多少次輸入資料。</span><span class="sxs-lookup"><span data-stu-id="e485d-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="e485d-160">hello 獨範例</span><span class="sxs-lookup"><span data-stu-id="e485d-160">hello Sudoku example</span></span>

<span data-ttu-id="e485d-161">[數獨](https://en.wikipedia.org/wiki/Sudoku) 是由九個 3x3 的方格所組成的邏輯謎題。</span><span class="sxs-lookup"><span data-stu-id="e485d-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="e485d-162">當其他人會空白，而且 hello 目標 toosolve hello 空白資料格時，hello 方格中的某些資料格都有數字。</span><span class="sxs-lookup"><span data-stu-id="e485d-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="e485d-163">hello 前一個連結有需 hello 拼圖的詳細資訊，但 hello 此範例的目的是 toosolve hello 空白資料格。</span><span class="sxs-lookup"><span data-stu-id="e485d-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="e485d-164">因此，我們輸入應該是處於 hello 遵循格式的檔案：</span><span class="sxs-lookup"><span data-stu-id="e485d-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="e485d-165">具有九個資料列的九個資料行</span><span class="sxs-lookup"><span data-stu-id="e485d-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="e485d-166">每個資料行可以包含一個數字或 `?` (表示空白的格子)</span><span class="sxs-lookup"><span data-stu-id="e485d-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="e485d-167">格子之間以空格分隔</span><span class="sxs-lookup"><span data-stu-id="e485d-167">Cells are separated by a space</span></span>

<span data-ttu-id="e485d-168">沒有特定的方式 tooconstruct 獨謎題;您無法重複的資料行或資料列中的數字。</span><span class="sxs-lookup"><span data-stu-id="e485d-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="e485d-169">沒有已正確建構的 hello HDInsight 叢集上的範例。</span><span class="sxs-lookup"><span data-stu-id="e485d-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="e485d-170">它位於`/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta`而且包含下列文字的 hello:</span><span class="sxs-lookup"><span data-stu-id="e485d-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="e485d-171">toorun hello 獨範例中，透過這個範例問題使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="e485d-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="e485d-172">hello 結果會顯示下列文字類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="e485d-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="e485d-173">Pi (π) 範例</span><span class="sxs-lookup"><span data-stu-id="e485d-173">Pi (π) example</span></span>

<span data-ttu-id="e485d-174">hello pi 範例會使用統計 (odd Monte Carlo) 方法 tooestimate hello pi 的值。</span><span class="sxs-lookup"><span data-stu-id="e485d-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="e485d-175">點隨機放置在單位正方形中。</span><span class="sxs-lookup"><span data-stu-id="e485d-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="e485d-176">hello 方也包含一個圓形。</span><span class="sxs-lookup"><span data-stu-id="e485d-176">hello square also contains a circle.</span></span> <span data-ttu-id="e485d-177">hello hello 點落在 hello 圓圈內的機率會等於 toohello 區域 hello 的圓圈，pi/4。</span><span class="sxs-lookup"><span data-stu-id="e485d-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="e485d-178">hello pi 的值可以從 4R hello 值來估計。</span><span class="sxs-lookup"><span data-stu-id="e485d-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="e485d-179">R 是 hello 比例 hello hello 圓形 toohello 總數 hello 正方形中的點內的點數目。</span><span class="sxs-lookup"><span data-stu-id="e485d-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="e485d-180">hello 較大 hello 範例使用的點數，hello 佳 hello 估計值。</span><span class="sxs-lookup"><span data-stu-id="e485d-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="e485d-181">這個範例使用下列命令 toorun hello。</span><span class="sxs-lookup"><span data-stu-id="e485d-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="e485d-182">此命令會使用 16 對應與 10000000 範例 tooestimate hello pi 的值：</span><span class="sxs-lookup"><span data-stu-id="e485d-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="e485d-183">hello 這個命令所傳回的值太類似**3.14159155000000000000**。</span><span class="sxs-lookup"><span data-stu-id="e485d-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="e485d-184">參考，hello pi 的前 10 個小數位數是 3.1415926535。</span><span class="sxs-lookup"><span data-stu-id="e485d-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="e485d-185">10 GB Greysort 範例</span><span class="sxs-lookup"><span data-stu-id="e485d-185">10 GB Greysort example</span></span>

<span data-ttu-id="e485d-186">GraySort 是一種效能評定排序。</span><span class="sxs-lookup"><span data-stu-id="e485d-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="e485d-187">hello 度量是達到時排序大量的資料，通常是 100 TB 最小的 hello 排序速率 （TB/分鐘）。</span><span class="sxs-lookup"><span data-stu-id="e485d-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="e485d-188">本範例使用不太大的 10 GB 資料，所以執行起來相對較快。</span><span class="sxs-lookup"><span data-stu-id="e485d-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="e485d-189">它會使用由 Owen O'Malley 和 Arun Murthy 所開發的 hello MapReduce 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e485d-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="e485d-190">這些應用程式在 2009 中，以 0.578 TB/分鐘 (以分鐘為單位 173 100 TB) 的速率贏得 hello 年度一般用途 (「 daytona 」) tb 排序基準測試。</span><span class="sxs-lookup"><span data-stu-id="e485d-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="e485d-191">如需有關這個和其他排序基準測試的詳細資訊，請參閱 hello [Sortbenchmark](http://sortbenchmark.org/)站台。</span><span class="sxs-lookup"><span data-stu-id="e485d-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="e485d-192">本範例使用三組 MapReduce 程式：</span><span class="sxs-lookup"><span data-stu-id="e485d-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="e485d-193">**TeraGen**： 產生資料列的資料 toosort 的 MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="e485d-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="e485d-194">**TeraSort**: hello 輸入的資料的範例，並使用 MapReduce toosort hello 資料到訂單總數</span><span class="sxs-lookup"><span data-stu-id="e485d-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="e485d-195">TeraSort 是標準的 MapReduce 排序，但有一個自訂 Partitioner。</span><span class="sxs-lookup"><span data-stu-id="e485d-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="e485d-196">hello partitioner 會使用定義的每個減少 hello 索引鍵範圍的取樣 N-1 索引鍵排序的清單。</span><span class="sxs-lookup"><span data-stu-id="e485d-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="e485d-197">特別是，所有的索引鍵這類範例 [i-1] < = 索引鍵 < 範例 [i] 傳送 tooreduce 我。</span><span class="sxs-lookup"><span data-stu-id="e485d-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="e485d-198">這個 partitioner 保證的 hello 輸出減少 i 全部都是小於 hello 輸出減少 i + 1。</span><span class="sxs-lookup"><span data-stu-id="e485d-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="e485d-199">**TeraValidate**： 全域排序會驗證該 hello 輸出的 MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="e485d-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="e485d-200">它在 hello 輸出目錄中，會建立一個對應，每個檔案和每個對應可確保每個索引鍵是否小於或等於前一個 toohello。</span><span class="sxs-lookup"><span data-stu-id="e485d-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="e485d-201">hello 對應函式會先產生 hello 的記錄，和最後一個索引鍵的每個檔案。</span><span class="sxs-lookup"><span data-stu-id="e485d-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="e485d-202">hello reduce 函式可確保該 hello i 檔案的第一個索引鍵大於檔案 i-1 hello 最後一個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e485d-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="e485d-203">Hello 的輸出，降低階段中，失序的 hello 索引鍵，則會報告任何問題。</span><span class="sxs-lookup"><span data-stu-id="e485d-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="e485d-204">使用 hello 下列步驟 toogenerate 資料排序，並驗證 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="e485d-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="e485d-205">產生 10 GB 的資料，這是預存的 toohello HDInsight 叢集的預設儲存在`/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="e485d-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="e485d-206">hello`-Dmapred.map.tasks`告訴 Hadoop 多少的對應工作 toouse，此作業。</span><span class="sxs-lookup"><span data-stu-id="e485d-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="e485d-207">hello 最後兩個參數會指示 hello 作業 toocreate 10 GB 的資料和 toostore 在`/example/data/10GB-sort-input`。</span><span class="sxs-lookup"><span data-stu-id="e485d-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="e485d-208">使用下列命令 toosort hello 資料 hello:</span><span class="sxs-lookup"><span data-stu-id="e485d-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="e485d-209">hello`-Dmapred.reduce.tasks`告訴 Hadoop 多少減少工作 toouse hello 作業。</span><span class="sxs-lookup"><span data-stu-id="e485d-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="e485d-210">hello 最後兩個參數是只 hello 輸入和輸出資料的位置。</span><span class="sxs-lookup"><span data-stu-id="e485d-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="e485d-211">使用下列 toovalidate hello 資料 hello 排序所產生的 hello:</span><span class="sxs-lookup"><span data-stu-id="e485d-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="e485d-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e485d-212">Next steps</span></span>

<span data-ttu-id="e485d-213">在此文件，您學到如何 toorun hello 範例隨附 hello 以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e485d-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="e485d-214">如需有關搭配使用 Pig、 Hive 和 MapReduce 與 HDInsight 的教學課程，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e485d-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="e485d-215">[搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e485d-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="e485d-216">[搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e485d-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="e485d-217">[搭配使用 MapReduce 與 HDInsight 上的 Hadoop][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="e485d-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
