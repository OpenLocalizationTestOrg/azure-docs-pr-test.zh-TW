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
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="a4896-103">在 HDInsight 上的 Hadoop 中使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="a4896-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="a4896-104">了解 toorun MapReduce HDInsight 叢集上的工作。</span><span class="sxs-lookup"><span data-stu-id="a4896-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="a4896-105">使用下列資料表 toodiscover hello MapReduce 可以搭配 HDInsight 的各種方式 hello:</span><span class="sxs-lookup"><span data-stu-id="a4896-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="a4896-106">**使用此方法**...</span><span class="sxs-lookup"><span data-stu-id="a4896-106">**Use this**...</span></span> | <span data-ttu-id="a4896-107">**...toodo 這**</span><span class="sxs-lookup"><span data-stu-id="a4896-107">**...toodo this**</span></span> | <span data-ttu-id="a4896-108">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="a4896-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="a4896-109">...從此 **用戶端作業系統**</span><span class="sxs-lookup"><span data-stu-id="a4896-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="a4896-110">SSH</span><span class="sxs-lookup"><span data-stu-id="a4896-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="a4896-111">使用透過 hello Hadoop 命令**SSH**</span><span class="sxs-lookup"><span data-stu-id="a4896-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="a4896-112">Linux</span><span class="sxs-lookup"><span data-stu-id="a4896-112">Linux</span></span> |<span data-ttu-id="a4896-113">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a4896-114">REST</span><span class="sxs-lookup"><span data-stu-id="a4896-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="a4896-115">使用從遠端提交工作 hello **REST** （範例會使用 cURL）</span><span class="sxs-lookup"><span data-stu-id="a4896-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="a4896-116">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-116">Linux or Windows</span></span> |<span data-ttu-id="a4896-117">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a4896-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4896-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="a4896-119">使用從遠端提交工作 hello **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a4896-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="a4896-120">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-120">Linux or Windows</span></span> |<span data-ttu-id="a4896-121">Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-121">Windows</span></span> |
| <span data-ttu-id="a4896-122">[遠端桌面](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 和 3.3)</span><span class="sxs-lookup"><span data-stu-id="a4896-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="a4896-123">使用透過 hello Hadoop 命令**遠端桌面**</span><span class="sxs-lookup"><span data-stu-id="a4896-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="a4896-124">Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-124">Windows</span></span> |<span data-ttu-id="a4896-125">Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a4896-126">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="a4896-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a4896-127">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="a4896-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="a4896-128"><a id="whatis"></a>什麼是 MapReduce</span><span class="sxs-lookup"><span data-stu-id="a4896-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="a4896-129">Hadoop MapReduce 是一種可撰寫工作來處理大量資料的軟體架構。</span><span class="sxs-lookup"><span data-stu-id="a4896-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="a4896-130">輸入的資料分割成獨立的區塊，然後以平行方式處理 hello 您的叢集節點之間。</span><span class="sxs-lookup"><span data-stu-id="a4896-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="a4896-131">MapReduce 工作由兩項功能組成：</span><span class="sxs-lookup"><span data-stu-id="a4896-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="a4896-132">**對應程式**：取用輸入資料、分析 (通常使用篩選及排序作業)，以及發出 Tuple (機碼值組)</span><span class="sxs-lookup"><span data-stu-id="a4896-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="a4896-133">**減壓器**： 會消耗 hello 對應工具所發出的 tuple，並執行摘要的作業，從 hello 對應程式資料建立較小的合併結果</span><span class="sxs-lookup"><span data-stu-id="a4896-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="a4896-134">下列圖表中的 hello 基本 word 計數 MapReduce 工作範例如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4896-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI.WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="a4896-136">這項作業的 hello 輸出是每個單字發生在已分析的 hello 文字的次數的計數。</span><span class="sxs-lookup"><span data-stu-id="a4896-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="a4896-137">hello 對應工具會從 hello 輸入文字，做為輸入的每一行，其分成數字。</span><span class="sxs-lookup"><span data-stu-id="a4896-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="a4896-138">它會發出索引鍵/值組的 hello word，word 就會發生每次後面是 1。</span><span class="sxs-lookup"><span data-stu-id="a4896-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="a4896-139">再將它傳送 tooreducer 排序 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="a4896-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="a4896-140">hello 減壓器加總這些個別計數的每個字，並發出單一索引鍵/值組，其包含 hello 文字後面接 hello 總和，其項目。</span><span class="sxs-lookup"><span data-stu-id="a4896-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="a4896-141">MapReduce 可在各種語言中實作。</span><span class="sxs-lookup"><span data-stu-id="a4896-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="a4896-142">Java hello 最常見的實作，並用於示範用途，此文件中。</span><span class="sxs-lookup"><span data-stu-id="a4896-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="a4896-143">開發語言</span><span class="sxs-lookup"><span data-stu-id="a4896-143">Development languages</span></span>

<span data-ttu-id="a4896-144">可以執行語言或架構以 Java 為基礎，hello Java 虛擬機器，直接以 MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="a4896-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="a4896-145">使用這份文件中的 hello 範例是 Java MapReduce 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a4896-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="a4896-146">非 Java 語言 (例如 C#、Python 或獨立可執行檔) 必須使用 Hadoop 資料流。</span><span class="sxs-lookup"><span data-stu-id="a4896-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="a4896-147">Hadoop 串流與 hello 對應工具和減壓器通訊透過 STDIN 和 STDOUT。</span><span class="sxs-lookup"><span data-stu-id="a4896-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="a4896-148">hello 對應工具和減壓器資料列一次從 STDIN、 讀寫 hello 輸出 tooSTDOUT。</span><span class="sxs-lookup"><span data-stu-id="a4896-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="a4896-149">Hello 的索引鍵/值組，以 tab 字元分隔的格式必須是讀取或 hello 對應工具和減壓器所發出的每一行：</span><span class="sxs-lookup"><span data-stu-id="a4896-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="a4896-150">如需詳細資訊，請參閱 [Hadoop 資料流](http://hadoop.apache.org/docs/r1.2.1/streaming.html)(英文)。</span><span class="sxs-lookup"><span data-stu-id="a4896-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="a4896-151">使用 Hadoop 串流與 HDInsight 的範例，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="a4896-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="a4896-152">開發 C# MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="a4896-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="a4896-153">開發 Python MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="a4896-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="a4896-154"><a id="data"></a>範例資料</span><span class="sxs-lookup"><span data-stu-id="a4896-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="a4896-155">HDInsight 提供各種範例資料集，其中會儲存在 hello`/example/data`和`/HdiSamples`目錄。</span><span class="sxs-lookup"><span data-stu-id="a4896-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="a4896-156">這些目錄位於 hello 預設儲存體叢集。</span><span class="sxs-lookup"><span data-stu-id="a4896-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="a4896-157">在本文件中，我們會使用 hello`/example/data/gutenberg/davinci.txt`檔案。</span><span class="sxs-lookup"><span data-stu-id="a4896-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="a4896-158">此檔案包含達文西 hello 的筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="a4896-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="a4896-159"><a id="job"></a>範例 MapReduce</span><span class="sxs-lookup"><span data-stu-id="a4896-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="a4896-160">範例 MapReduce 字數統計應用程式會包含您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="a4896-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="a4896-161">此範例位於`/example/jars/hadoop-mapreduce-examples.jar`hello 預設儲存體叢集上。</span><span class="sxs-lookup"><span data-stu-id="a4896-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="a4896-162">下列 Java 程式碼的 hello 是 hello MapReduce 應用程式包含在 hello hello 來源`hadoop-mapreduce-examples.jar`檔案：</span><span class="sxs-lookup"><span data-stu-id="a4896-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="a4896-163">指示 toowrite 自己 MapReduce 應用程式，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="a4896-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="a4896-164">開發 HDInsight 的 Java MapReduce 應用程式</span><span class="sxs-lookup"><span data-stu-id="a4896-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="a4896-165">開發 HDInsight 的 Python MapReduce 應用程式</span><span class="sxs-lookup"><span data-stu-id="a4896-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="a4896-166"><a id="run"></a>執行 MapReduce hello</span><span class="sxs-lookup"><span data-stu-id="a4896-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="a4896-167">HDInsight 可以使用各種方法執行 HiveQL 工作。</span><span class="sxs-lookup"><span data-stu-id="a4896-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="a4896-168">使用下列資料表 toodecide 哪一種方法是最適合您，hello，然後遵循逐步解說中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="a4896-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="a4896-169">**使用此方法**...</span><span class="sxs-lookup"><span data-stu-id="a4896-169">**Use this**...</span></span> | <span data-ttu-id="a4896-170">**...toodo 這**</span><span class="sxs-lookup"><span data-stu-id="a4896-170">**...toodo this**</span></span> | <span data-ttu-id="a4896-171">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="a4896-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="a4896-172">...從此 **用戶端作業系統**</span><span class="sxs-lookup"><span data-stu-id="a4896-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="a4896-173">SSH</span><span class="sxs-lookup"><span data-stu-id="a4896-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="a4896-174">使用透過 hello Hadoop 命令**SSH**</span><span class="sxs-lookup"><span data-stu-id="a4896-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="a4896-175">Linux</span><span class="sxs-lookup"><span data-stu-id="a4896-175">Linux</span></span> |<span data-ttu-id="a4896-176">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a4896-177">Curl</span><span class="sxs-lookup"><span data-stu-id="a4896-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="a4896-178">使用從遠端提交工作 hello **REST**</span><span class="sxs-lookup"><span data-stu-id="a4896-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="a4896-179">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-179">Linux or Windows</span></span> |<span data-ttu-id="a4896-180">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a4896-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4896-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="a4896-182">使用從遠端提交工作 hello **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a4896-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="a4896-183">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-183">Linux or Windows</span></span> |<span data-ttu-id="a4896-184">Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-184">Windows</span></span> |
| <span data-ttu-id="a4896-185">[遠端桌面](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 和 3.3)</span><span class="sxs-lookup"><span data-stu-id="a4896-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="a4896-186">使用透過 hello Hadoop 命令**遠端桌面**</span><span class="sxs-lookup"><span data-stu-id="a4896-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="a4896-187">Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-187">Windows</span></span> |<span data-ttu-id="a4896-188">Windows</span><span class="sxs-lookup"><span data-stu-id="a4896-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a4896-189">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="a4896-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a4896-190">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="a4896-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="a4896-191"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="a4896-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="a4896-192">toolearn 有關在 HDInsight 中使用資料的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="a4896-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="a4896-193">開發 HDInsight 的 Java MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="a4896-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="a4896-194">開發 HDInsight 的 Python 資料流 MapReduce 程式</span><span class="sxs-lookup"><span data-stu-id="a4896-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="a4896-195">使用 HDInsight 上的 Apache Hadoop 開發 Scalding MapReduce 工作</span><span class="sxs-lookup"><span data-stu-id="a4896-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="a4896-196">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="a4896-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="a4896-197">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="a4896-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
