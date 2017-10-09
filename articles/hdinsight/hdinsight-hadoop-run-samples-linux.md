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
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>執行包含在 HDInsight 中的 hello MapReduce 範例

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

了解如何 toorun hello MapReduce 範例隨附在 HDInsight Hadoop。

## <a name="prerequisites"></a>必要條件

* **HDInsight 叢集**：請參閱 [在 Linux 上開始在 HDInsight 中搭配使用 Hadoop 與 Hive](hdinsight-hadoop-linux-tutorial-get-started.md)

    > [!IMPORTANT]
    > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* **SSH 用戶端**：如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a name="hello-mapreduce-examples"></a>hello MapReduce 範例

**位置**: hello 範例位於 HDInsight 叢集在 hello `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`。

**內容**: hello 下列範例包含在此封存中：

* `aggregatewordcount`： 彙總以計算 hello 輸入檔中的 hello 文字的 mapreduce 程式。
* `aggregatewordhist`： 彙總以計算 hello 輸入檔中的 hello 文字的 hello 長條圖的 mapreduce 程式。
* `bbp`： 使用 Pi 的 Bailey-Borwein-Plouffe toocompute 完全位數 mapreduce 程式。
* `dbcount`： 計算儲存在資料庫中的 hello pageview 記錄檔這是範例工作。
* `distbbp`: 使用 BBP 類型公式 toocompute 確切位元的 Pi mapreduce 程式。
* `grep`: Regex hello 輸入中會比對計算 hello mapreduce 程式。
* `join`：作業，可執行已排序且平均分割之資料集的聯結。
* `multifilewc`：可從數個檔案計算字數的作業。
* `pentomino`： 用來配置程式 toofind 解決方案 toopentomino 問題 mapreduce 磚。
* `pi`：mapreduce 程式，使用擬蒙特卡羅 (quasi-Monte Carlo) 方法估計 Pi。
* `randomtextwriter`：mapreduce 程式，可為每個節點寫入 10 GB 的隨機文字資料。
* `randomwriter`：mapreduce 程式，可為每個節點寫入 10 GB 的隨機資料。
* `secondarysort`: 定義次要排序 toohello 範例減少階段。
* `sort`： 排序 hello hello 隨機寫入器寫入的資料 mapreduce 程式。
* `sudoku`：數獨解答程式。
* `teragen`： 產生 hello terasort 資料。
* `terasort`： 執行 hello terasort。
* `teravalidate`：檢查 TeraSort 的結果。
* `wordcount`： 計算 hello 輸入檔中的 hello 文字 mapreduce 程式。
* `wordmean`： 計算 hello 輸入檔中的 hello 文字 hello 平均長度 mapreduce 程式。
* `wordmedian`： 計算 hello hello 輸入檔中的 hello 文字的中間值的長度 mapreduce 程式。
* `wordstandarddeviation`： 計算 hello hello 輸入檔中的 hello 文字長度的 hello 標準差 mapreduce 程式。

**原始碼**： 這些範例的原始程式碼包含 HDInsight 叢集在 hello `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`。

> [!NOTE]
> hello`2.2.4.9-1`在 hello 路徑是 hello 新版 hello Hortonworks Data Platform hello HDInsight 叢集，而且可能會因您的叢集的。

## <a name="run-hello-wordcount-example"></a>執行 hello wordcount 範例

1. 連接使用 SSH tooHDInsight。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 從 hello`username@#######:~$`提示，請使用下列命令 toolist hello 範例 hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    此命令會從 hello 本文件的上一節中產生 hello 清單的範例。

3. 使用 hello 下列命令 tooget 說明特定的範例。 在此情況下，hello **wordcount**範例：

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    您會收到下列訊息的 hello:

        Usage: wordcount <in> [<in>...] <out>

    此訊息表示您可以為 hello 來源文件提供數個輸入的路徑。 hello 最後一個路徑是儲存 hello 輸出 （hello 來源文件中文字的計數）。

4. Hello 筆記本的達文西，與您的叢集提供做為範例資料中使用下列 toocount hello 所有文字：

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    此作業的輸入讀取自 `/example/data/gutenberg/davinci.txt`。 此範例的輸出會儲存在 `/example/data/davinciwordcount`。 這兩個路徑都位於 hello 叢集中，hello 本機檔案系統的預設儲存體。

   > [!NOTE]
   > Hello hello wordcount 範例說明所述，您也可以指定多個輸入的檔。 例如， `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` 會計算 davinci.txt 和 ulysses.txt 中的字數。

5. Hello 作業完成之後，請使用下列命令 tooview hello 輸出 hello:

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    此命令會串連 hello 作業所產生的所有 hello 輸出檔。 它會顯示 hello 輸出 toohello 主控台。 hello 輸出是類似 toohello 下列文字：

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    每一列代表 word 和 hello 在發生多少次輸入資料。

## <a name="hello-sudoku-example"></a>hello 獨範例

[數獨](https://en.wikipedia.org/wiki/Sudoku) 是由九個 3x3 的方格所組成的邏輯謎題。 當其他人會空白，而且 hello 目標 toosolve hello 空白資料格時，hello 方格中的某些資料格都有數字。 hello 前一個連結有需 hello 拼圖的詳細資訊，但 hello 此範例的目的是 toosolve hello 空白資料格。 因此，我們輸入應該是處於 hello 遵循格式的檔案：

* 具有九個資料列的九個資料行
* 每個資料行可以包含一個數字或 `?` (表示空白的格子)
* 格子之間以空格分隔

沒有特定的方式 tooconstruct 獨謎題;您無法重複的資料行或資料列中的數字。 沒有已正確建構的 hello HDInsight 叢集上的範例。 它位於`/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta`而且包含下列文字的 hello:

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

toorun hello 獨範例中，透過這個範例問題使用 hello 下列命令：

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

hello 結果會顯示下列文字類似 toohello:

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Pi (π) 範例

hello pi 範例會使用統計 (odd Monte Carlo) 方法 tooestimate hello pi 的值。 點隨機放置在單位正方形中。 hello 方也包含一個圓形。 hello hello 點落在 hello 圓圈內的機率會等於 toohello 區域 hello 的圓圈，pi/4。 hello pi 的值可以從 4R hello 值來估計。 R 是 hello 比例 hello hello 圓形 toohello 總數 hello 正方形中的點內的點數目。 hello 較大 hello 範例使用的點數，hello 佳 hello 估計值。

這個範例使用下列命令 toorun hello。 此命令會使用 16 對應與 10000000 範例 tooestimate hello pi 的值：

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

hello 這個命令所傳回的值太類似**3.14159155000000000000**。 參考，hello pi 的前 10 個小數位數是 3.1415926535。

## <a name="10-gb-greysort-example"></a>10 GB Greysort 範例

GraySort 是一種效能評定排序。 hello 度量是達到時排序大量的資料，通常是 100 TB 最小的 hello 排序速率 （TB/分鐘）。

本範例使用不太大的 10 GB 資料，所以執行起來相對較快。 它會使用由 Owen O'Malley 和 Arun Murthy 所開發的 hello MapReduce 應用程式。 這些應用程式在 2009 中，以 0.578 TB/分鐘 (以分鐘為單位 173 100 TB) 的速率贏得 hello 年度一般用途 (「 daytona 」) tb 排序基準測試。 如需有關這個和其他排序基準測試的詳細資訊，請參閱 hello [Sortbenchmark](http://sortbenchmark.org/)站台。

本範例使用三組 MapReduce 程式：

* **TeraGen**： 產生資料列的資料 toosort 的 MapReduce 程式

* **TeraSort**: hello 輸入的資料的範例，並使用 MapReduce toosort hello 資料到訂單總數

    TeraSort 是標準的 MapReduce 排序，但有一個自訂 Partitioner。 hello partitioner 會使用定義的每個減少 hello 索引鍵範圍的取樣 N-1 索引鍵排序的清單。 特別是，所有的索引鍵這類範例 [i-1] < = 索引鍵 < 範例 [i] 傳送 tooreduce 我。 這個 partitioner 保證的 hello 輸出減少 i 全部都是小於 hello 輸出減少 i + 1。

* **TeraValidate**： 全域排序會驗證該 hello 輸出的 MapReduce 程式

    它在 hello 輸出目錄中，會建立一個對應，每個檔案和每個對應可確保每個索引鍵是否小於或等於前一個 toohello。 hello 對應函式會先產生 hello 的記錄，和最後一個索引鍵的每個檔案。 hello reduce 函式可確保該 hello i 檔案的第一個索引鍵大於檔案 i-1 hello 最後一個索引鍵。 Hello 的輸出，降低階段中，失序的 hello 索引鍵，則會報告任何問題。

使用 hello 下列步驟 toogenerate 資料排序，並驗證 hello 輸出：

1. 產生 10 GB 的資料，這是預存的 toohello HDInsight 叢集的預設儲存在`/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    hello`-Dmapred.map.tasks`告訴 Hadoop 多少的對應工作 toouse，此作業。 hello 最後兩個參數會指示 hello 作業 toocreate 10 GB 的資料和 toostore 在`/example/data/10GB-sort-input`。

2. 使用下列命令 toosort hello 資料 hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    hello`-Dmapred.reduce.tasks`告訴 Hadoop 多少減少工作 toouse hello 作業。 hello 最後兩個參數是只 hello 輸入和輸出資料的位置。

3. 使用下列 toovalidate hello 資料 hello 排序所產生的 hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>後續步驟

在此文件，您學到如何 toorun hello 範例隨附 hello 以 Linux 為基礎的 HDInsight 叢集。 如需有關搭配使用 Pig、 Hive 和 MapReduce 與 HDInsight 的教學課程，請參閱下列主題中的 hello:

* [搭配使用 Pig 與 HDInsight 上的 Hadoop][hdinsight-use-pig]
* [搭配使用 Hive 與 HDInsight 上的 Hadoop][hdinsight-use-hive]
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
