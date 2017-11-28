---
title: "在 HDInsight Hadoop Pig aaaUse |Microsoft 文件"
description: "深入了解與 HDInsight 上的 Hadoop Pig toouse 的方式。"
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
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="239c5-103">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="239c5-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="239c5-104">深入了解如何 toouse [Apache Pig](http://pig.apache.org/)與 HDInsight...</span><span class="sxs-lookup"><span data-stu-id="239c5-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="239c5-105">Pig 是一個平台，可使用稱為 *Pig Latin*的程序性語言建立 Hadoop 的程式。</span><span class="sxs-lookup"><span data-stu-id="239c5-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="239c5-106">Pig 是建立替代 tooJava *MapReduce*方案和其隨附於 Azure HDInsight。</span><span class="sxs-lookup"><span data-stu-id="239c5-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="239c5-107">使用下列資料表 toodiscover hello Pig 可以搭配 HDInsight 的各種方式 hello:</span><span class="sxs-lookup"><span data-stu-id="239c5-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="239c5-108">**使用此方法** </span><span class="sxs-lookup"><span data-stu-id="239c5-108">**Use this** if you want...</span></span> | <span data-ttu-id="239c5-109">...一個 **互動式** 殼層</span><span class="sxs-lookup"><span data-stu-id="239c5-109">...an **interactive** shell</span></span> | <span data-ttu-id="239c5-110">...**批次** 處理</span><span class="sxs-lookup"><span data-stu-id="239c5-110">...**batch** processing</span></span> | <span data-ttu-id="239c5-111">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="239c5-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="239c5-112">...從此 **用戶端作業系統**</span><span class="sxs-lookup"><span data-stu-id="239c5-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="239c5-113">SSH</span><span class="sxs-lookup"><span data-stu-id="239c5-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="239c5-114">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-114">✔</span></span> |<span data-ttu-id="239c5-115">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-115">✔</span></span> |<span data-ttu-id="239c5-116">Linux</span><span class="sxs-lookup"><span data-stu-id="239c5-116">Linux</span></span> |<span data-ttu-id="239c5-117">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="239c5-118">REST API</span><span class="sxs-lookup"><span data-stu-id="239c5-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="239c5-119">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-119">✔</span></span> |<span data-ttu-id="239c5-120">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-120">Linux or Windows</span></span> |<span data-ttu-id="239c5-121">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="239c5-122">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="239c5-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="239c5-123">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-123">✔</span></span> |<span data-ttu-id="239c5-124">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-124">Linux or Windows</span></span> |<span data-ttu-id="239c5-125">Windows (目前)</span><span class="sxs-lookup"><span data-stu-id="239c5-125">Windows (for now)</span></span> |
| [<span data-ttu-id="239c5-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="239c5-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="239c5-127">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-127">✔</span></span> |<span data-ttu-id="239c5-128">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-128">Linux or Windows</span></span> |<span data-ttu-id="239c5-129">Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-129">Windows</span></span> |
| <span data-ttu-id="239c5-130">[遠端桌面](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 和 3.3)</span><span class="sxs-lookup"><span data-stu-id="239c5-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="239c5-131">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-131">✔</span></span> |<span data-ttu-id="239c5-132">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-132">✔</span></span> |<span data-ttu-id="239c5-133">Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-133">Windows</span></span> |<span data-ttu-id="239c5-134">Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="239c5-135">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="239c5-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="239c5-136">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="239c5-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="239c5-137"><a id="why"></a>為何要使用 Pig</span><span class="sxs-lookup"><span data-stu-id="239c5-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="239c5-138">Hello 挑戰之一使用 MapReduce Hadoop 中處理資料使用只對應和縮減函式來實作處理邏輯。</span><span class="sxs-lookup"><span data-stu-id="239c5-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="239c5-139">複雜的處理，您通常會有 toobreak 處理成多個 MapReduce 作業的鏈結在一起 tooachieve hello 預期結果。</span><span class="sxs-lookup"><span data-stu-id="239c5-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="239c5-140">Pig 可讓您 toodefine 處理為一系列的 hello 資料流經 tooproduce hello 預期輸出的轉換。</span><span class="sxs-lookup"><span data-stu-id="239c5-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="239c5-141">hello Pig 拉丁語言可讓您 toodescribe hello 資料流程從原始的輸入，透過一或多個轉換，tooproduce hello 預期輸出。</span><span class="sxs-lookup"><span data-stu-id="239c5-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="239c5-142">Pig Latin 程式遵循此一般模式：</span><span class="sxs-lookup"><span data-stu-id="239c5-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="239c5-143">**負載**： 讀取資料 toobe hello 檔案系統和操作</span><span class="sxs-lookup"><span data-stu-id="239c5-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="239c5-144">**轉換**： 操作 hello 資料</span><span class="sxs-lookup"><span data-stu-id="239c5-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="239c5-145">**傾印或儲存**： 輸出資料 toohello 螢幕，或將它儲存為處理</span><span class="sxs-lookup"><span data-stu-id="239c5-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="239c5-146">使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="239c5-146">User-defined functions</span></span>

<span data-ttu-id="239c5-147">Pig 拉丁也支援使用者定義函數 (UDF)，可讓您實作邏輯，會在 Pig 拉丁困難 toomodel tooinvoke 外部元件。</span><span class="sxs-lookup"><span data-stu-id="239c5-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="239c5-148">如需 Pig Latin 的詳細資訊，請參閱 [Pig Latin 參考手冊 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) (英文) 和 [Pig Latin 參考手冊 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html) (英文)。</span><span class="sxs-lookup"><span data-stu-id="239c5-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="239c5-149">使用 Pig Udf 的範例，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="239c5-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="239c5-150">[在 HDInsight 中搭配使用 DataFu 與 Pig](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu 是由 Apach 維護的 UDF 實用集合</span><span class="sxs-lookup"><span data-stu-id="239c5-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="239c5-151">在 HDInsight 中使用 Python 搭配 Pig 和 Hive</span><span class="sxs-lookup"><span data-stu-id="239c5-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="239c5-152">在 HDInsight 中搭配 Hive 與 Pig 使用 C#</span><span class="sxs-lookup"><span data-stu-id="239c5-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="239c5-153"><a id="data"></a>範例資料</span><span class="sxs-lookup"><span data-stu-id="239c5-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="239c5-154">HDInsight 提供各種範例資料集，其中會儲存在 hello`/example/data`和`/HdiSamples`目錄。</span><span class="sxs-lookup"><span data-stu-id="239c5-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="239c5-155">這些目錄位於 hello 預設儲存體叢集。</span><span class="sxs-lookup"><span data-stu-id="239c5-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="239c5-156">本文件中的 hello Pig 範例會使用 hello *log4j*檔案從`/example/data/sample.log`。</span><span class="sxs-lookup"><span data-stu-id="239c5-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="239c5-157">Hello 檔案內的每個記錄檔所組成的欄位包含的那一行`[LOG LEVEL]`欄位 tooshow hello 類型和 hello 嚴重性，例如：</span><span class="sxs-lookup"><span data-stu-id="239c5-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="239c5-158">Hello 上述範例中，在 hello 記錄層級會是錯誤。</span><span class="sxs-lookup"><span data-stu-id="239c5-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="239c5-159">您也可以產生 log4j 檔案使用 hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j)記錄工具，然後再上傳該檔案 tooyour blob。</span><span class="sxs-lookup"><span data-stu-id="239c5-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="239c5-160">請參閱[上傳資料 tooHDInsight](hdinsight-upload-data.md)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="239c5-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="239c5-161">如需關於如何搭配 HDInsight 使用 Azure 儲存體 Blob 的詳細資訊，請參閱 [搭配 HDInsight 使用 Azure Blob 儲存體](hdinsight-hadoop-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="239c5-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="239c5-162"><a id="job"></a>範例作業</span><span class="sxs-lookup"><span data-stu-id="239c5-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="239c5-163">hello 以下的 Pig 拉丁工作載入 hello `sample.log` hello 預設儲存體檔案針對您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="239c5-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="239c5-164">然後它會執行一系列轉換所產生的計數方式的多次每個記錄層級發生在 hello 輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="239c5-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="239c5-165">hello 結果會寫入 tooSTDOUT。</span><span class="sxs-lookup"><span data-stu-id="239c5-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="239c5-166">hello 下列影像顯示哪些每個轉換就會執行 toohello 資料的摘要。</span><span class="sxs-lookup"><span data-stu-id="239c5-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Hello 轉換圖形表示法][image-hdi-pig-data-transformation]

## <span data-ttu-id="239c5-168"><a id="run"></a>執行 hello 拉丁 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="239c5-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="239c5-169">HDInsight 可以使用各種方法執行 Pig Latin 工作。</span><span class="sxs-lookup"><span data-stu-id="239c5-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="239c5-170">使用下列資料表 toodecide 哪一種方法是最適合您，hello，然後遵循逐步解說中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="239c5-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="239c5-171">**使用此方法** </span><span class="sxs-lookup"><span data-stu-id="239c5-171">**Use this** if you want...</span></span> | <span data-ttu-id="239c5-172">...一個 **互動式** 殼層</span><span class="sxs-lookup"><span data-stu-id="239c5-172">...an **interactive** shell</span></span> | <span data-ttu-id="239c5-173">...**批次** 處理</span><span class="sxs-lookup"><span data-stu-id="239c5-173">...**batch** processing</span></span> | <span data-ttu-id="239c5-174">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="239c5-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="239c5-175">...從這個**用戶端**</span><span class="sxs-lookup"><span data-stu-id="239c5-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="239c5-176">SSH</span><span class="sxs-lookup"><span data-stu-id="239c5-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="239c5-177">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-177">✔</span></span> |<span data-ttu-id="239c5-178">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-178">✔</span></span> |<span data-ttu-id="239c5-179">Linux</span><span class="sxs-lookup"><span data-stu-id="239c5-179">Linux</span></span> |<span data-ttu-id="239c5-180">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="239c5-181">Curl</span><span class="sxs-lookup"><span data-stu-id="239c5-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="239c5-182">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-182">✔</span></span> |<span data-ttu-id="239c5-183">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-183">Linux or Windows</span></span> |<span data-ttu-id="239c5-184">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="239c5-185">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="239c5-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="239c5-186">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-186">✔</span></span> |<span data-ttu-id="239c5-187">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-187">Linux or Windows</span></span> |<span data-ttu-id="239c5-188">Windows (目前)</span><span class="sxs-lookup"><span data-stu-id="239c5-188">Windows (for now)</span></span> |
| [<span data-ttu-id="239c5-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="239c5-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="239c5-190">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-190">✔</span></span> |<span data-ttu-id="239c5-191">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-191">Linux or Windows</span></span> |<span data-ttu-id="239c5-192">Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-192">Windows</span></span> |
| <span data-ttu-id="239c5-193">[遠端桌面](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 和 3.3)</span><span class="sxs-lookup"><span data-stu-id="239c5-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="239c5-194">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-194">✔</span></span> |<span data-ttu-id="239c5-195">✔</span><span class="sxs-lookup"><span data-stu-id="239c5-195">✔</span></span> |<span data-ttu-id="239c5-196">Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-196">Windows</span></span> |<span data-ttu-id="239c5-197">Windows</span><span class="sxs-lookup"><span data-stu-id="239c5-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="239c5-198">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="239c5-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="239c5-199">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="239c5-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="239c5-200">Pig 和 SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="239c5-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="239c5-201">您可以使用 SQL Server Integration Services (SSIS) toorun Pig 工作。</span><span class="sxs-lookup"><span data-stu-id="239c5-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="239c5-202">hello Azure Feature Pack for SSIS 提供 hello 遵循使用 Pig 工作，在 HDInsight 的元件。</span><span class="sxs-lookup"><span data-stu-id="239c5-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="239c5-203">[Azure HDInsight Pig 工作][pigtask]</span><span class="sxs-lookup"><span data-stu-id="239c5-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="239c5-204">[Azure 訂用帳戶連接管理員][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="239c5-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="239c5-205">深入了解 hello Azure Feature Pack for SSIS[這裡][ssispack]。</span><span class="sxs-lookup"><span data-stu-id="239c5-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="239c5-206"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="239c5-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="239c5-207">既然您已經學會如何 toouse 與 HDInsight，下列使用 hello Pig 會連結 tooexplore Azure HDInsight 以其他方式 toowork。</span><span class="sxs-lookup"><span data-stu-id="239c5-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="239c5-208">[上傳資料 tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="239c5-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="239c5-209">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="239c5-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="239c5-210">搭配 HDInsight 使用 Sqoop</span><span class="sxs-lookup"><span data-stu-id="239c5-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="239c5-211">在 HDInsight 上使用 Oozie</span><span class="sxs-lookup"><span data-stu-id="239c5-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="239c5-212">[搭配 HDInsight 使用 MapReduce 作業][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="239c5-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
