---
title: "使用 HDInsight 開發 Python 串流處理 MapReduce 工作 - Azure | Microsoft Docs"
description: "了解如何在串流處理 MapReduce 工作中使用 Python。 Hadoop 提供適用於 MapReduce 的串流處理 API，可以 Java 以外的語言撰寫。"
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="5fcbd-104">開發 HDInsight 的 Python 串流處理 MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="5fcbd-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="5fcbd-105">了解如何在串流處理 MapReduce 作業中使用 Python。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="5fcbd-106">Hadoop 為 MapReduce 提供一個串流 API，可讓您以 Java 以外的語言撰寫 map 和 reduce 函數。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="5fcbd-107">本文件中的步驟會以 Python 實作對應和歸納元件。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fcbd-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="5fcbd-108">Prerequisites</span></span>

* <span data-ttu-id="5fcbd-109">HDInsight 叢集上的 Linux 型 Hadoop</span><span class="sxs-lookup"><span data-stu-id="5fcbd-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5fcbd-110">此文件中的步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5fcbd-111">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5fcbd-112">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5fcbd-113">文字編輯器</span><span class="sxs-lookup"><span data-stu-id="5fcbd-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5fcbd-114">文字編輯器必須使用 LF 做為行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="5fcbd-115">在以 Linux 為基礎的 HDInsight 叢集上執行 MapReduce 作業時，使用 CRLF 行尾結束符號會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="5fcbd-116">`ssh` 和 `scp` 命令，或 [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="5fcbd-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="5fcbd-117">字數統計</span><span class="sxs-lookup"><span data-stu-id="5fcbd-117">Word count</span></span>

<span data-ttu-id="5fcbd-118">此範例是使用 python 對應器和歸納器實作的基本字數統計。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="5fcbd-119">對應器會將句子拆解成個別文字，歸納器則會彙總文字和計數來產生輸出。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="5fcbd-120">下列流程圖說明在對應和歸納階段期間所執行的程序。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![mapreduce 程序圖](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="5fcbd-122">串流 MapReduce</span><span class="sxs-lookup"><span data-stu-id="5fcbd-122">Streaming MapReduce</span></span>

<span data-ttu-id="5fcbd-123">Hadoop 可讓您指定包含工作所使用的對應和歸納邏輯的檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="5fcbd-124">對應和歸納邏輯的特殊需求如下：</span><span class="sxs-lookup"><span data-stu-id="5fcbd-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="5fcbd-125">**輸入**：對應和歸納元件必須從 STDIN 讀取輸入資料。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="5fcbd-126">**輸出**：對應和歸納元件必須將輸出資料寫入至 STDOUT。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="5fcbd-127">**資料格式**：所取用和產生的資料必須是機碼/值組，並以 Tab 字元隔開。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="5fcbd-128">Python 可以使用 `sys` 模組來讀取 STDIN 並使用 `print` 來列印到 STDOUT，輕鬆應付這些需求。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="5fcbd-129">剩下的工作便只需要在機碼和值之間以 Tab (`\t`) 字元格式化資料。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="5fcbd-130">建立對應器和歸納器</span><span class="sxs-lookup"><span data-stu-id="5fcbd-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="5fcbd-131">建立名為 `mapper.py` 的檔案並使用下列程式碼作為內容：</span><span class="sxs-lookup"><span data-stu-id="5fcbd-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="5fcbd-132">建立名為 **reducer.py** 的檔案並使用下列程式碼作為內容：</span><span class="sxs-lookup"><span data-stu-id="5fcbd-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="5fcbd-133">使用 PowerShell 執行</span><span class="sxs-lookup"><span data-stu-id="5fcbd-133">Run using PowerShell</span></span>

<span data-ttu-id="5fcbd-134">若要確保您的檔案有正確的行尾結束符號，請使用下列 PowerShell 指令碼︰</span><span class="sxs-lookup"><span data-stu-id="5fcbd-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="5fcbd-135">[!code-powershell[主要](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="5fcbd-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="5fcbd-136">使用下列 PowerShell 指令碼來上傳檔案、執行作業，以及檢視輸出︰</span><span class="sxs-lookup"><span data-stu-id="5fcbd-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="5fcbd-137">[!code-powershell[主要](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="5fcbd-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="5fcbd-138">從 SSH 工作階段執行</span><span class="sxs-lookup"><span data-stu-id="5fcbd-138">Run from an SSH session</span></span>

1. <span data-ttu-id="5fcbd-139">從開發環境上，在 `mapper.py` 和 `reducer.py` 檔案所在的目錄中，使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5fcbd-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="5fcbd-140">以叢集的 SSH 使用者取代 `username`，並以叢集的名稱取代 `clustername`。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="5fcbd-141">此命令會將檔案從本機系統複製到前端節點。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5fcbd-142">如果您使用密碼來保護 SSH 帳戶，系統就會提示您輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="5fcbd-143">如果您使用 SSH 金鑰，您可能必須使用 `-i` 參數和私密金鑰的路徑。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="5fcbd-144">例如， `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="5fcbd-145">使用 SSH 連線到叢集：</span><span class="sxs-lookup"><span data-stu-id="5fcbd-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="5fcbd-146">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="5fcbd-147">若要確保 mapper.py 和 reducer.py 有正確的行尾結束符號，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="5fcbd-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="5fcbd-148">使用下列命令啟動 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="5fcbd-149">此命令有下列幾個部分：</span><span class="sxs-lookup"><span data-stu-id="5fcbd-149">This command has the following parts:</span></span>

   * <span data-ttu-id="5fcbd-150">**hadoop-streaming.jar**：執行串流 MapReduce 作業時使用。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="5fcbd-151">它能連結 Hadoop 和您提供的外部 MapReduce 程式碼。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="5fcbd-152">**-file**：將指定的檔案新增至 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="5fcbd-153">**-mapper**：告訴 Hadoop 要做為對應器的檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="5fcbd-154">**-reducer**：告訴 Hadoop 要做為歸納器的檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="5fcbd-155">**-input**：要從中計算字數的輸入檔案。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="5fcbd-156">**-output**：輸出時寫入的目錄。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="5fcbd-157">MapReduce 作業執行時會以百分比顯示過程。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="5fcbd-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="5fcbd-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="5fcbd-159">若要檢視輸出，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5fcbd-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="5fcbd-160">此命令會顯示單字清單及單字出現次數。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fcbd-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5fcbd-161">Next steps</span></span>

<span data-ttu-id="5fcbd-162">現在您已學會如何搭配 HDInsight 使用串流 MapRedcue 工作，接著請使用下列連結來探索 Azure HDInsight 的其他使用方式。</span><span class="sxs-lookup"><span data-stu-id="5fcbd-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="5fcbd-163">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="5fcbd-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5fcbd-164">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="5fcbd-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5fcbd-165">搭配 HDInsight 使用 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="5fcbd-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
