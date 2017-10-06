---
title: "aaaDevelop Python 串流 MapReduce 工作與 HDInsight 的 Azure |Microsoft 文件"
description: "深入了解如何在資料流 MapReduce 工作 toouse Python。 Hadoop 提供適用於 MapReduce 的串流處理 API，可以 Java 以外的語言撰寫。"
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
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="9379b-104">開發 HDInsight 的 Python 串流處理 MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="9379b-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="9379b-105">深入了解如何在資料流 MapReduce 作業 toouse Python。</span><span class="sxs-lookup"><span data-stu-id="9379b-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="9379b-106">Hadoop MapReduce，可讓您 toowrite 對應並減少 Java 以外的語言中的函式提供的資料流處理的 API。</span><span class="sxs-lookup"><span data-stu-id="9379b-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="9379b-107">hello 本文件中的步驟實作 hello 對應並減少 Python 中的元件。</span><span class="sxs-lookup"><span data-stu-id="9379b-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9379b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="9379b-108">Prerequisites</span></span>

* <span data-ttu-id="9379b-109">HDInsight 叢集上的 Linux 型 Hadoop</span><span class="sxs-lookup"><span data-stu-id="9379b-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9379b-110">本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="9379b-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="9379b-111">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="9379b-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9379b-112">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="9379b-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9379b-113">文字編輯器</span><span class="sxs-lookup"><span data-stu-id="9379b-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9379b-114">hello 文字編輯器必須使用 LF hello 行尾結束符號。</span><span class="sxs-lookup"><span data-stu-id="9379b-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="9379b-115">以 Linux 為基礎的 HDInsight 叢集上執行 hello MapReduce 工作時，使用的 CRLF 行尾結束符號會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="9379b-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="9379b-116">hello`ssh`和`scp`命令，或[Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="9379b-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="9379b-117">字數統計</span><span class="sxs-lookup"><span data-stu-id="9379b-117">Word count</span></span>

<span data-ttu-id="9379b-118">此範例是使用 python 對應器和歸納器實作的基本字數統計。</span><span class="sxs-lookup"><span data-stu-id="9379b-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="9379b-119">hello 對應工具會成單字、 句子，並且 hello 減壓器彙總 hello 文字，並計算 tooproduce hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="9379b-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="9379b-120">下列流程圖 hello 說明什麼 hello 對應期間進行的作業，並減少階段。</span><span class="sxs-lookup"><span data-stu-id="9379b-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![hello mapreduce 程序中的圖例](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="9379b-122">串流 MapReduce</span><span class="sxs-lookup"><span data-stu-id="9379b-122">Streaming MapReduce</span></span>

<span data-ttu-id="9379b-123">Hadoop 可讓您 toospecify 檔案，包含 hello 對應並減少作業使用的邏輯。</span><span class="sxs-lookup"><span data-stu-id="9379b-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="9379b-124">hello hello 特定需求對應和簡化邏輯是：</span><span class="sxs-lookup"><span data-stu-id="9379b-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="9379b-125">**輸入**: hello 對應並減少元件必須讀取 STDIN 的輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="9379b-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="9379b-126">**輸出**: hello 對應並減少元件必須寫入輸出資料 tooSTDOUT。</span><span class="sxs-lookup"><span data-stu-id="9379b-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="9379b-127">**資料格式**: hello 耗用，而且所產生的資料必須是索引鍵/值組，以 tab 字元分隔。</span><span class="sxs-lookup"><span data-stu-id="9379b-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="9379b-128">Python 可以輕鬆地處理這些需求，使用 hello `sys` STDIN，並使用模組 tooread `print` tooprint tooSTDOUT。</span><span class="sxs-lookup"><span data-stu-id="9379b-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="9379b-129">hello 其餘的工作只需格式化 hello 資料 索引標籤 (`\t`) 字元之間 hello 索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="9379b-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="9379b-130">建立 hello 對應工具和減壓器</span><span class="sxs-lookup"><span data-stu-id="9379b-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="9379b-131">建立名為`mapper.py`並使用 hello 遵循為 hello 內容的程式碼：</span><span class="sxs-lookup"><span data-stu-id="9379b-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="9379b-132">建立名為**reducer.py**並使用 hello 遵循為 hello 內容的程式碼：</span><span class="sxs-lookup"><span data-stu-id="9379b-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

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
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="9379b-133">使用 PowerShell 執行</span><span class="sxs-lookup"><span data-stu-id="9379b-133">Run using PowerShell</span></span>

<span data-ttu-id="9379b-134">tooensure 檔案有 hello 右行尾結束符號，使用下列 PowerShell 指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="9379b-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="9379b-135">使用下列 PowerShell 指令碼 tooupload hello 檔案 hello、 執行 hello 工作，以及檢視 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="9379b-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="9379b-136">從 SSH 工作階段執行</span><span class="sxs-lookup"><span data-stu-id="9379b-136">Run from an SSH session</span></span>

1. <span data-ttu-id="9379b-137">從您的開發環境中 hello 相同目錄做為`mapper.py`和`reducer.py`檔，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9379b-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="9379b-138">取代`username`hello 叢集中的 SSH 使用者名稱和`clustername`與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="9379b-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="9379b-139">此命令會將 hello 檔案從 hello 本機系統 toohello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="9379b-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9379b-140">如果您使用密碼 toosecure SSH 帳戶時，系統會提示您 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="9379b-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="9379b-141">如果您使用 SSH 金鑰，您可能必須 toouse hello`-i`參數和 hello 路徑 toohello 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="9379b-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="9379b-142">例如： `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`。</span><span class="sxs-lookup"><span data-stu-id="9379b-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="9379b-143">使用 SSH 連線 toohello 叢集：</span><span class="sxs-lookup"><span data-stu-id="9379b-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="9379b-144">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="9379b-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="9379b-145">tooensure hello mapper.py 和 reducer.py 具有 hello 更正行尾結束符號，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9379b-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="9379b-146">使用下列命令 toostart hello MapReduce 工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="9379b-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="9379b-147">此命令包含下列組件的 hello:</span><span class="sxs-lookup"><span data-stu-id="9379b-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="9379b-148">**hadoop-streaming.jar**：執行串流 MapReduce 作業時使用。</span><span class="sxs-lookup"><span data-stu-id="9379b-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="9379b-149">它與您提供 hello 外部 MapReduce 程式碼介面 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="9379b-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="9379b-150">**-檔案**： 加入指定的 hello 檔案 toohello MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="9379b-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="9379b-151">**-對應程式**： 告訴 Hadoop 檔案 toouse hello 對應工具。</span><span class="sxs-lookup"><span data-stu-id="9379b-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="9379b-152">**-減壓器**: hello 減壓器檔案 toouse 告訴 Hadoop。</span><span class="sxs-lookup"><span data-stu-id="9379b-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="9379b-153">**-輸入**: hello 我們應該計算的輸入的檔中的文字。</span><span class="sxs-lookup"><span data-stu-id="9379b-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="9379b-154">**-輸出**: hello 輸出的 hello 目錄寫入。</span><span class="sxs-lookup"><span data-stu-id="9379b-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="9379b-155">當 hello MapReduce 工作，hello 程序會顯示為百分比。</span><span class="sxs-lookup"><span data-stu-id="9379b-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="9379b-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span><span class="sxs-lookup"><span data-stu-id="9379b-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="9379b-157">下列命令使用 hello tooview hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="9379b-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="9379b-158">此命令顯示一份單字和多少次 hello 文字時發生。</span><span class="sxs-lookup"><span data-stu-id="9379b-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9379b-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9379b-159">Next steps</span></span>

<span data-ttu-id="9379b-160">現在您已經學會 toouse 串流 MapRedcue 與 HDInsight 的工作，使用下列連結 tooexplore hello 其他方式 toowork 與 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="9379b-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="9379b-161">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="9379b-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9379b-162">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="9379b-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9379b-163">搭配 HDInsight 使用 MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="9379b-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
