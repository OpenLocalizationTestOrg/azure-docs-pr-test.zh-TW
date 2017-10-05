---
title: "在 HDInsight 中使用 Hadoop Pig | Microsoft Docs"
description: "了解如何在 HDInsight 上搭配 Hadoop 使用 Pig。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 474f901ffdaf1ed372ace19076ef723b8b10cb9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="a3a00-103">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="a3a00-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="a3a00-104">了解如何使用 [Apache Pig](http://pig.apache.org/) 搭配 HDInsight...</span><span class="sxs-lookup"><span data-stu-id="a3a00-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="a3a00-105">Pig 是一個平台，可使用稱為 *Pig Latin*的程序性語言建立 Hadoop 的程式。</span><span class="sxs-lookup"><span data-stu-id="a3a00-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="a3a00-106">若要建立 *MapReduce* 解決方案，Pig 是 Java 的替代選項，而且也已包含在 Azure HDInsight 中。</span><span class="sxs-lookup"><span data-stu-id="a3a00-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="a3a00-107">使用下表了解可搭配 HDInsight 使用 Pig 的各種方式︰</span><span class="sxs-lookup"><span data-stu-id="a3a00-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="a3a00-108">**使用此方法** </span><span class="sxs-lookup"><span data-stu-id="a3a00-108">**Use this** if you want...</span></span> | <span data-ttu-id="a3a00-109">...一個 **互動式** 殼層</span><span class="sxs-lookup"><span data-stu-id="a3a00-109">...an **interactive** shell</span></span> | <span data-ttu-id="a3a00-110">...**批次** 處理</span><span class="sxs-lookup"><span data-stu-id="a3a00-110">...**batch** processing</span></span> | <span data-ttu-id="a3a00-111">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="a3a00-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="a3a00-112">...從此 **用戶端作業系統**</span><span class="sxs-lookup"><span data-stu-id="a3a00-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="a3a00-113">SSH</span><span class="sxs-lookup"><span data-stu-id="a3a00-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="a3a00-114">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-114">✔</span></span> |<span data-ttu-id="a3a00-115">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-115">✔</span></span> |<span data-ttu-id="a3a00-116">Linux</span><span class="sxs-lookup"><span data-stu-id="a3a00-116">Linux</span></span> |<span data-ttu-id="a3a00-117">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a3a00-118">REST API</span><span class="sxs-lookup"><span data-stu-id="a3a00-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="a3a00-119">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-119">✔</span></span> |<span data-ttu-id="a3a00-120">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-120">Linux or Windows</span></span> |<span data-ttu-id="a3a00-121">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a3a00-122">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="a3a00-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="a3a00-123">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-123">✔</span></span> |<span data-ttu-id="a3a00-124">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-124">Linux or Windows</span></span> |<span data-ttu-id="a3a00-125">Windows (目前)</span><span class="sxs-lookup"><span data-stu-id="a3a00-125">Windows (for now)</span></span> |
| [<span data-ttu-id="a3a00-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3a00-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="a3a00-127">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-127">✔</span></span> |<span data-ttu-id="a3a00-128">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-128">Linux or Windows</span></span> |<span data-ttu-id="a3a00-129">Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-129">Windows</span></span> |
| <span data-ttu-id="a3a00-130">[遠端桌面](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 和 3.3)</span><span class="sxs-lookup"><span data-stu-id="a3a00-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="a3a00-131">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-131">✔</span></span> |<span data-ttu-id="a3a00-132">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-132">✔</span></span> |<span data-ttu-id="a3a00-133">Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-133">Windows</span></span> |<span data-ttu-id="a3a00-134">Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a3a00-135">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a3a00-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a3a00-136">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="a3a00-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="a3a00-137"><a id="why"></a>為何要使用 Pig</span><span class="sxs-lookup"><span data-stu-id="a3a00-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="a3a00-138">在 Hadoop 中使用 MapReduce 處理資料的其中一項挑戰是，只藉由使用 map 和 reduce 函數實作處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="a3a00-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="a3a00-139">如果是複雜的處理，您經常必須將處理分成多個鏈結在一起的 MapReduce 作業，才能獲得想要的結果。</span><span class="sxs-lookup"><span data-stu-id="a3a00-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="a3a00-140">Pig 可讓您將處理定義為一系列轉換，使資料流過以產生所需的輸出。</span><span class="sxs-lookup"><span data-stu-id="a3a00-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="a3a00-141">Pig Latin 語言可讓您從原始輸入描述資料流 (經過一或多個轉換後) 以產生所需的輸出。</span><span class="sxs-lookup"><span data-stu-id="a3a00-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="a3a00-142">Pig Latin 程式遵循此一般模式：</span><span class="sxs-lookup"><span data-stu-id="a3a00-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="a3a00-143">**載入**：從檔案系統讀取要處理的資料</span><span class="sxs-lookup"><span data-stu-id="a3a00-143">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="a3a00-144">**轉換**：處理資料</span><span class="sxs-lookup"><span data-stu-id="a3a00-144">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="a3a00-145">**傾印或儲存**：將資料輸出至畫面，或儲存資料以供處理</span><span class="sxs-lookup"><span data-stu-id="a3a00-145">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="a3a00-146">使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="a3a00-146">User-defined functions</span></span>

<span data-ttu-id="a3a00-147">Pig Latin 也支援使用者定義函數 (UDF)，此函數讓您可用叫用外部元件，這些元件會實作很難以 Pig Latin 模型化的邏輯。</span><span class="sxs-lookup"><span data-stu-id="a3a00-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="a3a00-148">如需 Pig Latin 的詳細資訊，請參閱 [Pig Latin 參考手冊 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) (英文) 和 [Pig Latin 參考手冊 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html) (英文)。</span><span class="sxs-lookup"><span data-stu-id="a3a00-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="a3a00-149">如需搭配 Pig 使用 UDF 的範例，請參閱以下文件：</span><span class="sxs-lookup"><span data-stu-id="a3a00-149">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="a3a00-150">[在 HDInsight 中搭配使用 DataFu 與 Pig](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu 是由 Apach 維護的 UDF 實用集合</span><span class="sxs-lookup"><span data-stu-id="a3a00-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="a3a00-151">在 HDInsight 中使用 Python 搭配 Pig 和 Hive</span><span class="sxs-lookup"><span data-stu-id="a3a00-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="a3a00-152">在 HDInsight 中搭配 Hive 與 Pig 使用 C#</span><span class="sxs-lookup"><span data-stu-id="a3a00-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="a3a00-153"><a id="data"></a>範例資料</span><span class="sxs-lookup"><span data-stu-id="a3a00-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="a3a00-154">HDInsight 提供各種範例資料集，儲存在 `/example/data` 和 `/HdiSamples` 目錄中。</span><span class="sxs-lookup"><span data-stu-id="a3a00-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="a3a00-155">這些目錄位於您的叢集預設儲存體中。</span><span class="sxs-lookup"><span data-stu-id="a3a00-155">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="a3a00-156">本文件中的 Pig 範例使用 `/example/data/sample.log` 中的 *log4j* 檔案。</span><span class="sxs-lookup"><span data-stu-id="a3a00-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="a3a00-157">檔案中的每一筆記錄均由一列欄位組成，包括以 `[LOG LEVEL]` 欄位來顯示類型和嚴重性，例如：</span><span class="sxs-lookup"><span data-stu-id="a3a00-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="a3a00-158">在上一個範例中，記錄層級是「錯誤」。</span><span class="sxs-lookup"><span data-stu-id="a3a00-158">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="a3a00-159">您也可以使用 [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) 記錄工具產生 log4j 檔案，然後將該檔案上傳至 Blob。</span><span class="sxs-lookup"><span data-stu-id="a3a00-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="a3a00-160">如需指示，請參閱 [將資料上傳至 HDInsight](hdinsight-upload-data.md) 。</span><span class="sxs-lookup"><span data-stu-id="a3a00-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="a3a00-161">如需關於如何搭配 HDInsight 使用 Azure 儲存體 Blob 的詳細資訊，請參閱 [搭配 HDInsight 使用 Azure Blob 儲存體](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="a3a00-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="a3a00-162"><a id="job"></a>範例作業</span><span class="sxs-lookup"><span data-stu-id="a3a00-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="a3a00-163">以下 Pig Latin 作業會從 HDInsight 叢集的預設儲存體載入 `sample.log` 檔案。</span><span class="sxs-lookup"><span data-stu-id="a3a00-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="a3a00-164">然後該工作會執行一系列轉換，進而產生輸入資料中每個記錄層級出現次數的計數。</span><span class="sxs-lookup"><span data-stu-id="a3a00-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="a3a00-165">結果會寫入 STDOUT。</span><span class="sxs-lookup"><span data-stu-id="a3a00-165">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="a3a00-166">下圖顯示每個轉換如何處理資料的摘要。</span><span class="sxs-lookup"><span data-stu-id="a3a00-166">The following image shows a summary of what each transformation does to the data.</span></span>

![轉換的圖形化表示][image-hdi-pig-data-transformation]

## <span data-ttu-id="a3a00-168"><a id="run"></a>執行 Pig Latin 工作</span><span class="sxs-lookup"><span data-stu-id="a3a00-168"><a id="run"></a>Run the Pig Latin job</span></span>

<span data-ttu-id="a3a00-169">HDInsight 可以使用各種方法執行 Pig Latin 工作。</span><span class="sxs-lookup"><span data-stu-id="a3a00-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="a3a00-170">請使用下表決定適合您的方法，然後跟著連結逐項閱讀介紹。</span><span class="sxs-lookup"><span data-stu-id="a3a00-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="a3a00-171">**使用此方法** </span><span class="sxs-lookup"><span data-stu-id="a3a00-171">**Use this** if you want...</span></span> | <span data-ttu-id="a3a00-172">...一個 **互動式** 殼層</span><span class="sxs-lookup"><span data-stu-id="a3a00-172">...an **interactive** shell</span></span> | <span data-ttu-id="a3a00-173">...**批次** 處理</span><span class="sxs-lookup"><span data-stu-id="a3a00-173">...**batch** processing</span></span> | <span data-ttu-id="a3a00-174">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="a3a00-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="a3a00-175">...從這個**用戶端**</span><span class="sxs-lookup"><span data-stu-id="a3a00-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="a3a00-176">SSH</span><span class="sxs-lookup"><span data-stu-id="a3a00-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="a3a00-177">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-177">✔</span></span> |<span data-ttu-id="a3a00-178">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-178">✔</span></span> |<span data-ttu-id="a3a00-179">Linux</span><span class="sxs-lookup"><span data-stu-id="a3a00-179">Linux</span></span> |<span data-ttu-id="a3a00-180">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a3a00-181">Curl</span><span class="sxs-lookup"><span data-stu-id="a3a00-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="a3a00-182">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-182">✔</span></span> |<span data-ttu-id="a3a00-183">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-183">Linux or Windows</span></span> |<span data-ttu-id="a3a00-184">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="a3a00-185">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="a3a00-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="a3a00-186">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-186">✔</span></span> |<span data-ttu-id="a3a00-187">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-187">Linux or Windows</span></span> |<span data-ttu-id="a3a00-188">Windows (目前)</span><span class="sxs-lookup"><span data-stu-id="a3a00-188">Windows (for now)</span></span> |
| [<span data-ttu-id="a3a00-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3a00-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="a3a00-190">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-190">✔</span></span> |<span data-ttu-id="a3a00-191">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-191">Linux or Windows</span></span> |<span data-ttu-id="a3a00-192">Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-192">Windows</span></span> |
| <span data-ttu-id="a3a00-193">[遠端桌面](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 和 3.3)</span><span class="sxs-lookup"><span data-stu-id="a3a00-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="a3a00-194">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-194">✔</span></span> |<span data-ttu-id="a3a00-195">✔</span><span class="sxs-lookup"><span data-stu-id="a3a00-195">✔</span></span> |<span data-ttu-id="a3a00-196">Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-196">Windows</span></span> |<span data-ttu-id="a3a00-197">Windows</span><span class="sxs-lookup"><span data-stu-id="a3a00-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a3a00-198">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a3a00-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a3a00-199">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="a3a00-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="a3a00-200">Pig 和 SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="a3a00-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="a3a00-201">您可以使用 SQL Server Integration Services (SSIS) 執行 Pig 作業。</span><span class="sxs-lookup"><span data-stu-id="a3a00-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="a3a00-202">適用於 SSIS 的 Azure Feature Pack 中提供下列元件可搭配 HDInsight 上的 Pig 工作使用。</span><span class="sxs-lookup"><span data-stu-id="a3a00-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="a3a00-203">[Azure HDInsight Pig 工作][pigtask]</span><span class="sxs-lookup"><span data-stu-id="a3a00-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="a3a00-204">[Azure 訂用帳戶連接管理員][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="a3a00-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="a3a00-205">在[這裡][ssispack]深入了解適用於 SSIS 的 Azure Feature Pack。</span><span class="sxs-lookup"><span data-stu-id="a3a00-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="a3a00-206"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="a3a00-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="a3a00-207">現在您已學會如何搭配 HDInsight 使用 Pig，接著請使用下列連結來探索 Azure HDInsight 的其他使用方式。</span><span class="sxs-lookup"><span data-stu-id="a3a00-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="a3a00-208">[將資料上傳至 HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a3a00-208">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a3a00-209">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="a3a00-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="a3a00-210">搭配 HDInsight 使用 Sqoop</span><span class="sxs-lookup"><span data-stu-id="a3a00-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="a3a00-211">在 HDInsight 上使用 Oozie</span><span class="sxs-lookup"><span data-stu-id="a3a00-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="a3a00-212">[搭配 HDInsight 使用 MapReduce 作業][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="a3a00-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
