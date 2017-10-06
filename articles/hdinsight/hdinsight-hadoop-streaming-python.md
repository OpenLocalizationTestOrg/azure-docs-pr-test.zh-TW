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
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>開發 HDInsight 的 Python 串流處理 MapReduce 程式

深入了解如何在資料流 MapReduce 作業 toouse Python。 Hadoop MapReduce，可讓您 toowrite 對應並減少 Java 以外的語言中的函式提供的資料流處理的 API。 hello 本文件中的步驟實作 hello 對應並減少 Python 中的元件。

## <a name="prerequisites"></a>必要條件

* HDInsight 叢集上的 Linux 型 Hadoop

  > [!IMPORTANT]
  > 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* 文字編輯器

  > [!IMPORTANT]
  > hello 文字編輯器必須使用 LF hello 行尾結束符號。 以 Linux 為基礎的 HDInsight 叢集上執行 hello MapReduce 工作時，使用的 CRLF 行尾結束符號會造成錯誤。

* hello`ssh`和`scp`命令，或[Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>字數統計

此範例是使用 python 對應器和歸納器實作的基本字數統計。 hello 對應工具會成單字、 句子，並且 hello 減壓器彙總 hello 文字，並計算 tooproduce hello 輸出。

下列流程圖 hello 說明什麼 hello 對應期間進行的作業，並減少階段。

![hello mapreduce 程序中的圖例](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>串流 MapReduce

Hadoop 可讓您 toospecify 檔案，包含 hello 對應並減少作業使用的邏輯。 hello hello 特定需求對應和簡化邏輯是：

* **輸入**: hello 對應並減少元件必須讀取 STDIN 的輸入的資料。
* **輸出**: hello 對應並減少元件必須寫入輸出資料 tooSTDOUT。
* **資料格式**: hello 耗用，而且所產生的資料必須是索引鍵/值組，以 tab 字元分隔。

Python 可以輕鬆地處理這些需求，使用 hello `sys` STDIN，並使用模組 tooread `print` tooprint tooSTDOUT。 hello 其餘的工作只需格式化 hello 資料 索引標籤 (`\t`) 字元之間 hello 索引鍵和值。

## <a name="create-hello-mapper-and-reducer"></a>建立 hello 對應工具和減壓器

1. 建立名為`mapper.py`並使用 hello 遵循為 hello 內容的程式碼：

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

2. 建立名為**reducer.py**並使用 hello 遵循為 hello 內容的程式碼：

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

## <a name="run-using-powershell"></a>使用 PowerShell 執行

tooensure 檔案有 hello 右行尾結束符號，使用下列 PowerShell 指令碼的 hello:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

使用下列 PowerShell 指令碼 tooupload hello 檔案 hello、 執行 hello 工作，以及檢視 hello 輸出：

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>從 SSH 工作階段執行

1. 從您的開發環境中 hello 相同目錄做為`mapper.py`和`reducer.py`檔，使用下列命令的 hello:

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    取代`username`hello 叢集中的 SSH 使用者名稱和`clustername`與 hello 叢集的名稱。

    此命令會將 hello 檔案從 hello 本機系統 toohello 前端節點。

    > [!NOTE]
    > 如果您使用密碼 toosecure SSH 帳戶時，系統會提示您 hello 密碼。 如果您使用 SSH 金鑰，您可能必須 toouse hello`-i`參數和 hello 路徑 toohello 私密金鑰。 例如： `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`。

2. 使用 SSH 連線 toohello 叢集：

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

3. tooensure hello mapper.py 和 reducer.py 具有 hello 更正行尾結束符號，請使用下列命令的 hello:

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. 使用下列命令 toostart hello MapReduce 工作的 hello。

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    此命令包含下列組件的 hello:

   * **hadoop-streaming.jar**：執行串流 MapReduce 作業時使用。 它與您提供 hello 外部 MapReduce 程式碼介面 Hadoop。

   * **-檔案**： 加入指定的 hello 檔案 toohello MapReduce 工作。

   * **-對應程式**： 告訴 Hadoop 檔案 toouse hello 對應工具。

   * **-減壓器**: hello 減壓器檔案 toouse 告訴 Hadoop。

   * **-輸入**: hello 我們應該計算的輸入的檔中的文字。

   * **-輸出**: hello 輸出的 hello 目錄寫入。

    當 hello MapReduce 工作，hello 程序會顯示為百分比。

        15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%


5. 下列命令使用 hello tooview hello 輸出：

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    此命令顯示一份單字和多少次 hello 文字時發生。

## <a name="next-steps"></a>後續步驟

現在您已經學會 toouse 串流 MapRedcue 與 HDInsight 的工作，使用下列連結 tooexplore hello 其他方式 toowork 與 Azure HDInsight。

* [搭配 HDInsight 使用 Hivet](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [搭配 HDInsight 使用 MapReduce 工作](hdinsight-use-mapreduce.md)
