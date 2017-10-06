---
title: "與 HDInsight 上的 Hadoop aaaMapReduce |Microsoft 文件"
description: "了解如何 toorun MapReduce 中的工作在 Hadoop 上的 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>在 HDInsight 上的 Hadoop 中使用 MapReduce

了解 toorun MapReduce HDInsight 叢集上的工作。 使用下列資料表 toodiscover hello MapReduce 可以搭配 HDInsight 的各種方式 hello:

| **使用此方法**... | **...toodo 這** | ...搭配此 **叢集作業系統** | ...從此 **用戶端作業系統** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |使用透過 hello Hadoop 命令**SSH** |Linux |Linux、Unix、Mac OS X 或 Windows |
| [REST](hdinsight-hadoop-use-mapreduce-curl.md) |使用從遠端提交工作 hello **REST** （範例會使用 cURL） |Linux 或 Windows |Linux、Unix、Mac OS X 或 Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |使用從遠端提交工作 hello **Windows PowerShell** |Linux 或 Windows |Windows |
| [遠端桌面](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 和 3.3) |使用透過 hello Hadoop 命令**遠端桌面** |Windows |Windows |

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a id="whatis"></a>什麼是 MapReduce

Hadoop MapReduce 是一種可撰寫工作來處理大量資料的軟體架構。 輸入的資料分割成獨立的區塊，然後以平行方式處理 hello 您的叢集節點之間。 MapReduce 工作由兩項功能組成：

* **對應程式**：取用輸入資料、分析 (通常使用篩選及排序作業)，以及發出 Tuple (機碼值組)

* **減壓器**： 會消耗 hello 對應工具所發出的 tuple，並執行摘要的作業，從 hello 對應程式資料建立較小的合併結果

下列圖表中的 hello 基本 word 計數 MapReduce 工作範例如下所示：

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

這項作業的 hello 輸出是每個單字發生在已分析的 hello 文字的次數的計數。

* hello 對應工具會從 hello 輸入文字，做為輸入的每一行，其分成數字。 它會發出索引鍵/值組的 hello word，word 就會發生每次後面是 1。 再將它傳送 tooreducer 排序 hello 輸出。
* hello 減壓器加總這些個別計數的每個字，並發出單一索引鍵/值組，其包含 hello 文字後面接 hello 總和，其項目。

MapReduce 可在各種語言中實作。 Java hello 最常見的實作，並用於示範用途，此文件中。

## <a name="development-languages"></a>開發語言

可以執行語言或架構以 Java 為基礎，hello Java 虛擬機器，直接以 MapReduce 工作。 使用這份文件中的 hello 範例是 Java MapReduce 應用程式。 非 Java 語言 (例如 C#、Python 或獨立可執行檔) 必須使用 Hadoop 資料流。

Hadoop 串流與 hello 對應工具和減壓器通訊透過 STDIN 和 STDOUT。 hello 對應工具和減壓器資料列一次從 STDIN、 讀寫 hello 輸出 tooSTDOUT。 Hello 的索引鍵/值組，以 tab 字元分隔的格式必須是讀取或 hello 對應工具和減壓器所發出的每一行：

    [key]/t[value]

如需詳細資訊，請參閱 [Hadoop 資料流](http://hadoop.apache.org/docs/r1.2.1/streaming.html)(英文)。

使用 Hadoop 串流與 HDInsight 的範例，請參閱下列文件的 hello:

* [開發 C# MapReduce 工作](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [開發 Python MapReduce 工作](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>範例資料

HDInsight 提供各種範例資料集，其中會儲存在 hello`/example/data`和`/HdiSamples`目錄。 這些目錄位於 hello 預設儲存體叢集。 在本文件中，我們會使用 hello`/example/data/gutenberg/davinci.txt`檔案。 此檔案包含達文西 hello 的筆記型電腦。

## <a id="job"></a>範例 MapReduce

範例 MapReduce 字數統計應用程式會包含您的 HDInsight 叢集。 此範例位於`/example/jars/hadoop-mapreduce-examples.jar`hello 預設儲存體叢集上。

下列 Java 程式碼的 hello 是 hello MapReduce 應用程式包含在 hello hello 來源`hadoop-mapreduce-examples.jar`檔案：

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

指示 toowrite 自己 MapReduce 應用程式，請參閱下列文件的 hello:

* [開發 HDInsight 的 Java MapReduce 應用程式](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [開發 HDInsight 的 Python MapReduce 應用程式](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>執行 MapReduce hello

HDInsight 可以使用各種方法執行 HiveQL 工作。 使用下列資料表 toodecide 哪一種方法是最適合您，hello，然後遵循逐步解說中的 hello 連結。

| **使用此方法**... | **...toodo 這** | ...搭配此 **叢集作業系統** | ...從此 **用戶端作業系統** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |使用透過 hello Hadoop 命令**SSH** |Linux |Linux、Unix、Mac OS X 或 Windows |
| [Curl](hdinsight-hadoop-use-mapreduce-curl.md) |使用從遠端提交工作 hello **REST** |Linux 或 Windows |Linux、Unix、Mac OS X 或 Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |使用從遠端提交工作 hello **Windows PowerShell** |Linux 或 Windows |Windows |
| [遠端桌面](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 和 3.3) |使用透過 hello Hadoop 命令**遠端桌面** |Windows |Windows |

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a id="nextsteps"></a>接續步驟

toolearn 有關在 HDInsight 中使用資料的詳細資訊，請參閱下列文件的 hello:

* [開發 HDInsight 的 Java MapReduce 程式](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [開發 HDInsight 的 Python 資料流 MapReduce 程式](hdinsight-hadoop-streaming-python.md)

* [使用 HDInsight 上的 Apache Hadoop 開發 Scalding MapReduce 工作](hdinsight-hadoop-mapreduce-scalding.md)

* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]

* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
