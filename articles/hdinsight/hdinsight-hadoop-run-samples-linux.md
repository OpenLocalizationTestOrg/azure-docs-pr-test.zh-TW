---
title: "在 HDInsight 上執行 Hadoop MapReduce 範例 - Azure | Microsoft Docs"
description: "開始使用 HDInsight 中隨附的 jar 檔案中的 MapReduce 範例。 使用 SSH 連接到叢集，然後使用 Hadoop 命令執行範例工作。"
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
ms.openlocfilehash: 447c07f869ff9a2a2a00089248be98e6729d6dc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="run-the-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="9076a-105">執行包含在 HDInsight 中的 MapReduce 範例</span><span class="sxs-lookup"><span data-stu-id="9076a-105">Run the MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="9076a-106">了解如何執行隨附於 HDInsight 上之 Hadoop 的 MapReduce 範例。</span><span class="sxs-lookup"><span data-stu-id="9076a-106">Learn how to run the MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9076a-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="9076a-107">Prerequisites</span></span>

* <span data-ttu-id="9076a-108">**HDInsight 叢集**：請參閱 [在 Linux 上開始在 HDInsight 中搭配使用 Hadoop 與 Hive](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="9076a-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9076a-109">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="9076a-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9076a-110">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="9076a-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9076a-111">**SSH 用戶端**：如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="9076a-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="the-mapreduce-examples"></a><span data-ttu-id="9076a-112">MapReduce 範例</span><span class="sxs-lookup"><span data-stu-id="9076a-112">The MapReduce examples</span></span>

<span data-ttu-id="9076a-113">**位置**：範例位於 HDInsight 叢集上的 `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`。</span><span class="sxs-lookup"><span data-stu-id="9076a-113">**Location**: The samples are located on the HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="9076a-114">**內容**：下列範例都包含在此封存中：</span><span class="sxs-lookup"><span data-stu-id="9076a-114">**Contents**: The following samples are contained in this archive:</span></span>

* <span data-ttu-id="9076a-115">`aggregatewordcount`：以彙總為基礎的 mapreduce 程式，可計算輸入檔中的字數。</span><span class="sxs-lookup"><span data-stu-id="9076a-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="9076a-116">`aggregatewordhist`：以彙總為基礎的 mapreduce 程式，可計算輸入檔中字數的長條圖。</span><span class="sxs-lookup"><span data-stu-id="9076a-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes the histogram of the words in the input files.</span></span>
* <span data-ttu-id="9076a-117">`bbp`：mapreduce 程式，使用貝利-波爾溫-普勞夫公式 (Bailey-Borwein-Plouffe) 計算 Pi 的確切位數。</span><span class="sxs-lookup"><span data-stu-id="9076a-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe to compute exact digits of Pi.</span></span>
* <span data-ttu-id="9076a-118">`dbcount`：範例作業，計數儲存在資料庫中的 pageview 記錄。</span><span class="sxs-lookup"><span data-stu-id="9076a-118">`dbcount`: An example job that counts the pageview logs stored in a database.</span></span>
* <span data-ttu-id="9076a-119">`distbbp`：mapreduce 程式，使用 BBP 類型的公式來計算 Pi 的確切位數。</span><span class="sxs-lookup"><span data-stu-id="9076a-119">`distbbp`: A mapreduce program that uses a BBP-type formula to compute exact bits of Pi.</span></span>
* <span data-ttu-id="9076a-120">`grep`：mapreduce 程式，可計算輸入中 regex 的相符項目。</span><span class="sxs-lookup"><span data-stu-id="9076a-120">`grep`: A mapreduce program that counts the matches of a regex in the input.</span></span>
* <span data-ttu-id="9076a-121">`join`：作業，可執行已排序且平均分割之資料集的聯結。</span><span class="sxs-lookup"><span data-stu-id="9076a-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="9076a-122">`multifilewc`：可從數個檔案計算字數的作業。</span><span class="sxs-lookup"><span data-stu-id="9076a-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="9076a-123">`pentomino`：mapreduce 圖格配置程式，可尋找五格骨牌 (pentomino) 問題的解答。</span><span class="sxs-lookup"><span data-stu-id="9076a-123">`pentomino`: A mapreduce tile laying program to find solutions to pentomino problems.</span></span>
* <span data-ttu-id="9076a-124">`pi`：mapreduce 程式，使用擬蒙特卡羅 (quasi-Monte Carlo) 方法估計 Pi。</span><span class="sxs-lookup"><span data-stu-id="9076a-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="9076a-125">`randomtextwriter`：mapreduce 程式，可為每個節點寫入 10 GB 的隨機文字資料。</span><span class="sxs-lookup"><span data-stu-id="9076a-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="9076a-126">`randomwriter`：mapreduce 程式，可為每個節點寫入 10 GB 的隨機資料。</span><span class="sxs-lookup"><span data-stu-id="9076a-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="9076a-127">`secondarysort`：範例，定義要簡化階段的二次排序。</span><span class="sxs-lookup"><span data-stu-id="9076a-127">`secondarysort`: An example defining a secondary sort to the reduce phase.</span></span>
* <span data-ttu-id="9076a-128">`sort`：mapreduce 程式，可排序隨機寫入器所寫入的資料。</span><span class="sxs-lookup"><span data-stu-id="9076a-128">`sort`: A mapreduce program that sorts the data written by the random writer.</span></span>
* <span data-ttu-id="9076a-129">`sudoku`：數獨解答程式。</span><span class="sxs-lookup"><span data-stu-id="9076a-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="9076a-130">`teragen`：產生用於 TeraSort 的資料。</span><span class="sxs-lookup"><span data-stu-id="9076a-130">`teragen`: Generate data for the terasort.</span></span>
* <span data-ttu-id="9076a-131">`terasort`：執行 TeraSort。</span><span class="sxs-lookup"><span data-stu-id="9076a-131">`terasort`: Run the terasort.</span></span>
* <span data-ttu-id="9076a-132">`teravalidate`：檢查 TeraSort 的結果。</span><span class="sxs-lookup"><span data-stu-id="9076a-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="9076a-133">`wordcount`：mapreduce 程式，可計算輸入檔中的字數。</span><span class="sxs-lookup"><span data-stu-id="9076a-133">`wordcount`: A mapreduce program that counts the words in the input files.</span></span>
* <span data-ttu-id="9076a-134">`wordmean`：mapreduce 程式，可計算輸入檔中字詞的平均長度。</span><span class="sxs-lookup"><span data-stu-id="9076a-134">`wordmean`: A mapreduce program that counts the average length of the words in the input files.</span></span>
* <span data-ttu-id="9076a-135">`wordmedian`：mapreduce 程式，可計算輸入檔中字詞的中位數長度。</span><span class="sxs-lookup"><span data-stu-id="9076a-135">`wordmedian`: A mapreduce program that counts the median length of the words in the input files.</span></span>
* <span data-ttu-id="9076a-136">`wordstandarddeviation`：mapreduce 程式，可計算輸入檔中字詞長度的標準差。</span><span class="sxs-lookup"><span data-stu-id="9076a-136">`wordstandarddeviation`: A mapreduce program that counts the standard deviation of the length of the words in the input files.</span></span>

<span data-ttu-id="9076a-137">**原始程式碼**：這些範例的原始程式碼包含在 HDInsight 叢集上，位於 `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`。</span><span class="sxs-lookup"><span data-stu-id="9076a-137">**Source code**: Source code for these samples is included on the HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="9076a-138">路徑中的 `2.2.4.9-1` 是 HDInsight 叢集所使用的 Hortonworks Data Platform 版本，且可能與您的叢集不同。</span><span class="sxs-lookup"><span data-stu-id="9076a-138">The `2.2.4.9-1` in the path is the version of the Hortonworks Data Platform for the HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-the-wordcount-example"></a><span data-ttu-id="9076a-139">執行 wordcount 範例</span><span class="sxs-lookup"><span data-stu-id="9076a-139">Run the wordcount example</span></span>

1. <span data-ttu-id="9076a-140">使用 SSH 連線到 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="9076a-140">Connect to HDInsight using SSH.</span></span> <span data-ttu-id="9076a-141">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="9076a-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9076a-142">在 `username@#######:~$` 提示中，使用下列命令來列出範例：</span><span class="sxs-lookup"><span data-stu-id="9076a-142">From the `username@#######:~$` prompt, use the following command to list the samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="9076a-143">此命令會產生本文件上一節中的範例清單。</span><span class="sxs-lookup"><span data-stu-id="9076a-143">This command generates the list of sample from the previous section of this document.</span></span>

3. <span data-ttu-id="9076a-144">使用下列命令可取得特定範例的說明。</span><span class="sxs-lookup"><span data-stu-id="9076a-144">Use the following command to get help on a specific sample.</span></span> <span data-ttu-id="9076a-145">在此情況下為 **wordcount** 範例：</span><span class="sxs-lookup"><span data-stu-id="9076a-145">In this case, the **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="9076a-146">您會看見下列訊息：</span><span class="sxs-lookup"><span data-stu-id="9076a-146">You receive the following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="9076a-147">此訊息表示您可以為來源文件提供數個輸入路徑。</span><span class="sxs-lookup"><span data-stu-id="9076a-147">This message indicates that you can provide several input paths for the source documents.</span></span> <span data-ttu-id="9076a-148">最後一個路徑是輸出 (來源文件中的字數計數) 的儲存處。</span><span class="sxs-lookup"><span data-stu-id="9076a-148">The final path is where the output (count of words in the source documents) is stored.</span></span>

4. <span data-ttu-id="9076a-149">使用以下命令計算達文西手稿筆記中的所有字數，該文件已隨附於您的叢集做為範例資料：</span><span class="sxs-lookup"><span data-stu-id="9076a-149">Use the following to count all words in the Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="9076a-150">此作業的輸入讀取自 `/example/data/gutenberg/davinci.txt`。</span><span class="sxs-lookup"><span data-stu-id="9076a-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="9076a-151">此範例的輸出會儲存在 `/example/data/davinciwordcount`。</span><span class="sxs-lookup"><span data-stu-id="9076a-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="9076a-152">這兩個路徑都位於叢集的預設儲存體上，而不是本機檔案系統上。</span><span class="sxs-lookup"><span data-stu-id="9076a-152">Both paths are located on default storage for the cluster, not the local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9076a-153">如 wordcount 範例的說明所述，您也可以指定多個輸入檔。</span><span class="sxs-lookup"><span data-stu-id="9076a-153">As noted in the help for the wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="9076a-154">例如， `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` 會計算 davinci.txt 和 ulysses.txt 中的字數。</span><span class="sxs-lookup"><span data-stu-id="9076a-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="9076a-155">工作完成後，使用以下命令來檢視輸出：</span><span class="sxs-lookup"><span data-stu-id="9076a-155">Once the job completes, use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="9076a-156">此命令會串連作業所產生的所有輸出檔。</span><span class="sxs-lookup"><span data-stu-id="9076a-156">This command concatenates all the output files produced by the job.</span></span> <span data-ttu-id="9076a-157">它會在主控台顯示輸出。</span><span class="sxs-lookup"><span data-stu-id="9076a-157">It displays the output to the console.</span></span> <span data-ttu-id="9076a-158">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="9076a-158">The output is similar to the following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="9076a-159">每一行代表一個字詞，以及該字詞在輸入資料中出現的次數。</span><span class="sxs-lookup"><span data-stu-id="9076a-159">Each line represents a word and how many times it occurred in the input data.</span></span>

## <a name="the-sudoku-example"></a><span data-ttu-id="9076a-160">數獨範例</span><span class="sxs-lookup"><span data-stu-id="9076a-160">The Sudoku example</span></span>

<span data-ttu-id="9076a-161">[數獨](https://en.wikipedia.org/wiki/Sudoku) 是由九個 3x3 的方格所組成的邏輯謎題。</span><span class="sxs-lookup"><span data-stu-id="9076a-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="9076a-162">方格中的一些格子含有數字，而有些格子則為空白，因此目標就是解出空白格子的數字。</span><span class="sxs-lookup"><span data-stu-id="9076a-162">Some cells in the grid have numbers, while others are blank, and the goal is to solve for the blank cells.</span></span> <span data-ttu-id="9076a-163">先前的連結提供謎題的詳細資訊，而此範例的目的是要解出空白格子的數字。</span><span class="sxs-lookup"><span data-stu-id="9076a-163">The previous link has more information on the puzzle, but the purpose of this sample is to solve for the blank cells.</span></span> <span data-ttu-id="9076a-164">所以我們的輸入應該是具有下列格式的檔案：</span><span class="sxs-lookup"><span data-stu-id="9076a-164">So our input should be a file that is in the following format:</span></span>

* <span data-ttu-id="9076a-165">具有九個資料列的九個資料行</span><span class="sxs-lookup"><span data-stu-id="9076a-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="9076a-166">每個資料行可以包含一個數字或 `?` (表示空白的格子)</span><span class="sxs-lookup"><span data-stu-id="9076a-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="9076a-167">格子之間以空格分隔</span><span class="sxs-lookup"><span data-stu-id="9076a-167">Cells are separated by a space</span></span>

<span data-ttu-id="9076a-168">建立數獨謎題必須採用特定的方法，那就是您不能在某個資料行或資料列中使用重複的數字。</span><span class="sxs-lookup"><span data-stu-id="9076a-168">There is a certain way to construct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="9076a-169">HDInsight 叢集上已經有一個正確建立的範例。</span><span class="sxs-lookup"><span data-stu-id="9076a-169">There's an example on the HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="9076a-170">它位於 `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` 且包含下列文字：</span><span class="sxs-lookup"><span data-stu-id="9076a-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains the following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="9076a-171">若要在 Sudoku 範例中執行此範例問題，請使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="9076a-171">To run this example problem through the Sudoku example, use the following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="9076a-172">出現的結果會類似如下文字：</span><span class="sxs-lookup"><span data-stu-id="9076a-172">The results appear similar to the following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="9076a-173">Pi (π) 範例</span><span class="sxs-lookup"><span data-stu-id="9076a-173">Pi (π) example</span></span>

<span data-ttu-id="9076a-174">Pi 範例會使用統計 (擬蒙特卡羅法) 方法來估計 pi 的值。</span><span class="sxs-lookup"><span data-stu-id="9076a-174">The pi sample uses a statistical (quasi-Monte Carlo) method to estimate the value of pi.</span></span> <span data-ttu-id="9076a-175">點隨機放置在單位正方形中。</span><span class="sxs-lookup"><span data-stu-id="9076a-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="9076a-176">正方形也包含一個圓形。</span><span class="sxs-lookup"><span data-stu-id="9076a-176">The square also contains a circle.</span></span> <span data-ttu-id="9076a-177">點落在圓形中的機率等於圓面積，Pi/4。</span><span class="sxs-lookup"><span data-stu-id="9076a-177">The probability that the points fall within the circle are equal to the area of the circle, pi/4.</span></span> <span data-ttu-id="9076a-178">Pi 的值可從 4R 的值來估計。</span><span class="sxs-lookup"><span data-stu-id="9076a-178">The value of pi can be estimated from the value of 4R.</span></span> <span data-ttu-id="9076a-179">其中 R 是圓內點數佔正方形內總點數的比例。</span><span class="sxs-lookup"><span data-stu-id="9076a-179">R is the ratio of the number of points that are inside the circle to the total number of points that are within the square.</span></span> <span data-ttu-id="9076a-180">使用的樣本點越多，估計越準確。</span><span class="sxs-lookup"><span data-stu-id="9076a-180">The larger the sample of points used, the better the estimate is.</span></span>

<span data-ttu-id="9076a-181">使用以下命令來執行此範例。</span><span class="sxs-lookup"><span data-stu-id="9076a-181">Use the following command to run this sample.</span></span> <span data-ttu-id="9076a-182">此命令會每次使用 16 個對應搭配 10,000,000 個取樣來估計 Pi 的值：</span><span class="sxs-lookup"><span data-stu-id="9076a-182">This command uses 16 maps with 10,000,000 samples each to estimate the value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="9076a-183">此命令傳回的值類似於 **3.14159155000000000000**。</span><span class="sxs-lookup"><span data-stu-id="9076a-183">The value returned by this command is similar to **3.14159155000000000000**.</span></span> <span data-ttu-id="9076a-184">Pi 的前 10 個小數位數是 3.1415926535，供您參考。</span><span class="sxs-lookup"><span data-stu-id="9076a-184">For references, the first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="9076a-185">10 GB Greysort 範例</span><span class="sxs-lookup"><span data-stu-id="9076a-185">10 GB Greysort example</span></span>

<span data-ttu-id="9076a-186">GraySort 是一種效能評定排序。</span><span class="sxs-lookup"><span data-stu-id="9076a-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="9076a-187">其計量為排序大量資料時 (通常至少為 100 TB) 所達成的排序速率 (TB/分鐘)。</span><span class="sxs-lookup"><span data-stu-id="9076a-187">The metric is the sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="9076a-188">本範例使用不太大的 10 GB 資料，所以執行起來相對較快。</span><span class="sxs-lookup"><span data-stu-id="9076a-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="9076a-189">本範例使用由 Owen O'Malley 和 Arun Murthy 共同開發的 MapReduce 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9076a-189">It uses the MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="9076a-190">這些應用程式於 2009 年的年度一般目的 (「耐力賽」) TB 排序效能評定中，以 0.578 TB/分鐘 (173 分鐘內達到 100 TB) 的速率獲勝。</span><span class="sxs-lookup"><span data-stu-id="9076a-190">These applications won the annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="9076a-191">如需此效能評比和其他排序效能評比的詳細資訊，請參閱 [Sortbenchmark](http://sortbenchmark.org/) 網站。</span><span class="sxs-lookup"><span data-stu-id="9076a-191">For more information on this and other sorting benchmarks, see the [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="9076a-192">本範例使用三組 MapReduce 程式：</span><span class="sxs-lookup"><span data-stu-id="9076a-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="9076a-193">**TeraGen**：MapReduce 程式，產生要排序的資料列</span><span class="sxs-lookup"><span data-stu-id="9076a-193">**TeraGen**: A MapReduce program that generates rows of data to sort</span></span>

* <span data-ttu-id="9076a-194">**TeraSort**可取樣輸入資料並利用 MapReduce 將資料依全序排列</span><span class="sxs-lookup"><span data-stu-id="9076a-194">**TeraSort**: Samples the input data and uses MapReduce to sort the data into a total order</span></span>

    <span data-ttu-id="9076a-195">TeraSort 是標準的 MapReduce 排序，但有一個自訂 Partitioner。</span><span class="sxs-lookup"><span data-stu-id="9076a-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="9076a-196">此 Partitioner 使用已排序的 N-1 取樣索引鍵清單，其定義每個歸納的索引鍵範圍。</span><span class="sxs-lookup"><span data-stu-id="9076a-196">The partitioner uses a sorted list of N-1 sampled keys that define the key range for each reduce.</span></span> <span data-ttu-id="9076a-197">尤其是，會傳送使得 sample[i-1] <= key < sample[i] 的所有索引鍵給歸納 i。</span><span class="sxs-lookup"><span data-stu-id="9076a-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent to reduce i.</span></span> <span data-ttu-id="9076a-198">此 Partitioner 會保證歸納 i 的輸出全都小於歸納 i+1 的輸出。</span><span class="sxs-lookup"><span data-stu-id="9076a-198">This partitioner guarantees that the outputs of reduce i are all less than the output of reduce i+1.</span></span>

* <span data-ttu-id="9076a-199">**TeraValidate**：可驗證全域排序輸出的 MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="9076a-199">**TeraValidate**: A MapReduce program that validates that the output is globally sorted</span></span>

    <span data-ttu-id="9076a-200">它會在輸出目錄中為每一個檔案建立一個對應，而每個對應可確保每一個索引鍵一定小於或等於前一個對應。</span><span class="sxs-lookup"><span data-stu-id="9076a-200">It creates one map per file in the output directory, and each map ensures that each key is less than or equal to the previous one.</span></span> <span data-ttu-id="9076a-201">對應函式會產生每個檔案的第一個和最後一個金鑰的記錄。</span><span class="sxs-lookup"><span data-stu-id="9076a-201">The map function generates records of the first and last keys of each file.</span></span> <span data-ttu-id="9076a-202">歸納函式可確保檔案 i 的第一個金鑰大於檔案 i-1 的最後一個金鑰。</span><span class="sxs-lookup"><span data-stu-id="9076a-202">The reduce function ensures that the first key of file i is greater than the last key of file i-1.</span></span> <span data-ttu-id="9076a-203">任何問題皆會回報為具備錯誤金鑰歸納階段的輸出。</span><span class="sxs-lookup"><span data-stu-id="9076a-203">Any problems are reported as an output of the reduce phase, with the keys that are out of order.</span></span>

<span data-ttu-id="9076a-204">使用下列步驟來產生資料、排序，並驗證輸出：</span><span class="sxs-lookup"><span data-stu-id="9076a-204">Use the following steps to generate data, sort, and then validate the output:</span></span>

1. <span data-ttu-id="9076a-205">產生 10 GB 的資料，這些資料稍後會儲存在 HDInsight 叢集預設儲存體中，位於 `/example/data/10GB-sort-input`：</span><span class="sxs-lookup"><span data-stu-id="9076a-205">Generate 10 GB of data, which is stored to the HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="9076a-206">`-Dmapred.map.tasks` 會告訴 Hadoop 在這項工作中要使用多少 map 工作。</span><span class="sxs-lookup"><span data-stu-id="9076a-206">The `-Dmapred.map.tasks` tells Hadoop how many map tasks to use for this job.</span></span> <span data-ttu-id="9076a-207">最後兩個參數會指示作業建立 10 GB 的資料，並將資料儲存在 `/example/data/10GB-sort-input`。</span><span class="sxs-lookup"><span data-stu-id="9076a-207">The final two parameters instruct the job to create 10 GB of data and to store it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="9076a-208">使用以下命令來排序資料：</span><span class="sxs-lookup"><span data-stu-id="9076a-208">Use the following command to sort the data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="9076a-209">`-Dmapred.reduce.tasks` 會告訴 Hadoop 在這項工作中要使用多少 reduce 工作。</span><span class="sxs-lookup"><span data-stu-id="9076a-209">The `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks to use for the job.</span></span> <span data-ttu-id="9076a-210">最後兩個參數只是資料的輸入和輸出位置。</span><span class="sxs-lookup"><span data-stu-id="9076a-210">The final two parameters are just the input and output locations for data.</span></span>

3. <span data-ttu-id="9076a-211">使用以下命令驗證依排序產生的資料：</span><span class="sxs-lookup"><span data-stu-id="9076a-211">Use the following to validate the data generated by the sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="9076a-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9076a-212">Next steps</span></span>

<span data-ttu-id="9076a-213">您已在本文中學到如何執行以 Linux 為基礎的 HDInsight 叢集所隨附的範例。</span><span class="sxs-lookup"><span data-stu-id="9076a-213">From this article, you learned how to run the samples included with the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="9076a-214">如需透過 HDInsight 使用 Pig、Hive 和 MapReduce 的教學課程，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="9076a-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see the following topics:</span></span>

* <span data-ttu-id="9076a-215">[搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9076a-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="9076a-216">[搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9076a-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="9076a-217">[搭配使用 MapReduce 與 HDInsight 上的 Hadoop][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="9076a-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
