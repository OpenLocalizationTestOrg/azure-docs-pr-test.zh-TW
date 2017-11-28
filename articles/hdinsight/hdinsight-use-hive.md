---
title: "aaaWhat 是 Apache Hive 和 HiveQL-Azure HDInsight |Microsoft 文件"
description: "Apache Hive 是適用於 Hadoop 的資料倉儲系統。 您可以查詢資料儲存在登錄區利用 HiveQL，哪些類似 tooTransact SQL。 在這份文件，了解如何 toouse hive 控制檔和使用 Azure HDInsight HiveQL。"
keywords: "hiveql，什麼是登錄區，hadoop hiveql 如何 toouse hive 控制檔，了解什麼是登錄區的 hive"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="ae3c7-106">Azure HDInsight 上的 Apache Hive 和 HiveQL 是什麼？</span><span class="sxs-lookup"><span data-stu-id="ae3c7-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="ae3c7-107">[Apache Hive](http://hive.apache.org/) 是適用於 Hadoop 的資料倉儲系統。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="ae3c7-108">Hive 可執行資料摘要、查詢以及資料分析。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="ae3c7-109">已寫入下列 HiveQL，也就是查詢語言類似 tooSQL hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="ae3c7-110">登錄區可讓您 tooproject 結構上大部分的非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="ae3c7-111">您可以定義 hello 結構之後，您可以使用 HiveQL tooquery hello 資料的 Java 或 MapReduce 不知情的情況下。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="ae3c7-112">HDInsight 提供數種已針對特定工作負載進行微調的叢集類型。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="ae3c7-113">下列叢集類型的 hello 最常使用 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="ae3c7-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="ae3c7-114">__互動式 Hive__： 提供的 Hadoop 叢集[低延遲分析處理 (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP)互動式查詢功能 tooimprove 回應時間。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="ae3c7-115">如需詳細資訊，請參閱 hello[開頭 HDInsight 中的互動式 Hive](hdinsight-hadoop-use-interactive-hive.md)文件。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="ae3c7-116">__Hadoop__︰已針對批次處理工作負載進行微調的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="ae3c7-117">如需詳細資訊，請參閱 hello[啟動 HDInsight 中的 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)文件。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="ae3c7-118">__Spark__：Apache Spark 有可用於 Hive 的內建功能。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="ae3c7-119">如需詳細資訊，請參閱 hello[開頭 HDInsight 上的 Spark](hdinsight-apache-spark-jupyter-spark-sql.md)文件。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="ae3c7-120">__對 HBase__: HiveQL 可以是使用的 tooquery 對 HBase 中所儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="ae3c7-121">如需詳細資訊，請參閱 hello[開始在 HDInsight HBase](hdinsight-hbase-tutorial-get-started-linux.md)文件。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="ae3c7-122">如何 toouse hive 控制檔</span><span class="sxs-lookup"><span data-stu-id="ae3c7-122">How toouse Hive</span></span>

<span data-ttu-id="ae3c7-123">使用下列資料表 toodiscover toouse hive 控制檔與 HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="ae3c7-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="ae3c7-124">**使用此方法**，如果您想要...</span><span class="sxs-lookup"><span data-stu-id="ae3c7-124">**Use this method** if you want...</span></span> | <span data-ttu-id="ae3c7-125">...一個 **互動式** 殼層</span><span class="sxs-lookup"><span data-stu-id="ae3c7-125">...an **interactive** shell</span></span> | <span data-ttu-id="ae3c7-126">...**批次** 處理</span><span class="sxs-lookup"><span data-stu-id="ae3c7-126">...**batch** processing</span></span> | <span data-ttu-id="ae3c7-127">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="ae3c7-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="ae3c7-128">...從此 **用戶端作業系統**</span><span class="sxs-lookup"><span data-stu-id="ae3c7-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ae3c7-129">Hive 檢視</span><span class="sxs-lookup"><span data-stu-id="ae3c7-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="ae3c7-130">✔</span><span class="sxs-lookup"><span data-stu-id="ae3c7-130">✔</span></span> |<span data-ttu-id="ae3c7-131">✔</span><span class="sxs-lookup"><span data-stu-id="ae3c7-131">✔</span></span> |<span data-ttu-id="ae3c7-132">Linux</span><span class="sxs-lookup"><span data-stu-id="ae3c7-132">Linux</span></span> |<span data-ttu-id="ae3c7-133">任何 (以瀏覽器為基礎)</span><span class="sxs-lookup"><span data-stu-id="ae3c7-133">Any (browser based)</span></span> |
| [<span data-ttu-id="ae3c7-134">Beeline 用戶端</span><span class="sxs-lookup"><span data-stu-id="ae3c7-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="ae3c7-135">✔</span><span class="sxs-lookup"><span data-stu-id="ae3c7-135">✔</span></span> |<span data-ttu-id="ae3c7-136">✔</span><span class="sxs-lookup"><span data-stu-id="ae3c7-136">✔</span></span> |<span data-ttu-id="ae3c7-137">Linux</span><span class="sxs-lookup"><span data-stu-id="ae3c7-137">Linux</span></span> |<span data-ttu-id="ae3c7-138">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="ae3c7-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ae3c7-139">REST API</span><span class="sxs-lookup"><span data-stu-id="ae3c7-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="ae3c7-140">✔</span><span class="sxs-lookup"><span data-stu-id="ae3c7-140">✔</span></span> |<span data-ttu-id="ae3c7-141">Linux 或 Windows*</span><span class="sxs-lookup"><span data-stu-id="ae3c7-141">Linux or Windows*</span></span> |<span data-ttu-id="ae3c7-142">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="ae3c7-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ae3c7-143">HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae3c7-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="ae3c7-144">✔</span><span class="sxs-lookup"><span data-stu-id="ae3c7-144">✔</span></span> |<span data-ttu-id="ae3c7-145">Linux 或 Windows*</span><span class="sxs-lookup"><span data-stu-id="ae3c7-145">Linux or Windows*</span></span> |<span data-ttu-id="ae3c7-146">Windows</span><span class="sxs-lookup"><span data-stu-id="ae3c7-146">Windows</span></span> |
| [<span data-ttu-id="ae3c7-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae3c7-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="ae3c7-148">✔</span><span class="sxs-lookup"><span data-stu-id="ae3c7-148">✔</span></span> |<span data-ttu-id="ae3c7-149">Linux 或 Windows*</span><span class="sxs-lookup"><span data-stu-id="ae3c7-149">Linux or Windows*</span></span> |<span data-ttu-id="ae3c7-150">Windows</span><span class="sxs-lookup"><span data-stu-id="ae3c7-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ae3c7-151">\*Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ae3c7-152">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="ae3c7-153">如果您使用 Windows 為基礎的 HDInsight 叢集，您可以使用 hello[查詢主控台](hdinsight-hadoop-use-hive-query-console.md)從瀏覽器或[遠端桌面](hdinsight-hadoop-use-hive-remote-desktop.md)toorun Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="ae3c7-154">HiveQL 語言參考</span><span class="sxs-lookup"><span data-stu-id="ae3c7-154">HiveQL language reference</span></span>

<span data-ttu-id="ae3c7-155">這個語言參考位於 hello[語言手動 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="ae3c7-156">Hive 和資料結構</span><span class="sxs-lookup"><span data-stu-id="ae3c7-156">Hive and data structure</span></span>

<span data-ttu-id="ae3c7-157">登錄區了解與 toowork 的結構化和半結構化的資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="ae3c7-158">例如，文字檔 hello 欄位，以特定字元分隔。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="ae3c7-159">hello HiveQL 陳述式之後建立的資料表，以空格分隔的資料：</span><span class="sxs-lookup"><span data-stu-id="ae3c7-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="ae3c7-160">Hive 也支援自訂複雜或不規則結構化資料的 **序列化/反序列化程式 (SerDe)** 。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="ae3c7-161">如需詳細資訊，請參閱 hello[如何 toouse 與 HDInsight 自訂 JSON SerDe](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx)文件。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="ae3c7-162">如需有關登錄區所支援的檔案格式的詳細資訊，請參閱 hello[語言手動 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="ae3c7-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="ae3c7-163">Hive 內部和外部資料表比較。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="ae3c7-164">您可以使用 Hive 建立兩種類型的資料表：</span><span class="sxs-lookup"><span data-stu-id="ae3c7-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="ae3c7-165">__內部__: hello Hive 資料倉儲中所儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="ae3c7-166">hello 資料倉儲位於`/hive/warehouse/`hello hello 叢集的預設儲存體上。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="ae3c7-167">使用內部資料表的時機︰</span><span class="sxs-lookup"><span data-stu-id="ae3c7-167">Use internal tables when:</span></span>

    * <span data-ttu-id="ae3c7-168">資料是暫存的。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-168">Data is temporary.</span></span>
    * <span data-ttu-id="ae3c7-169">您想 Hive toomanage hello 生命週期的 hello 資料表和資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="ae3c7-170">__外部__： 資料會儲存外 hello 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="ae3c7-171">hello 資料可以儲存在任何可存取的存放裝置，由 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="ae3c7-172">使用外部資料表的時機︰</span><span class="sxs-lookup"><span data-stu-id="ae3c7-172">Use external tables when:</span></span>

    * <span data-ttu-id="ae3c7-173">hello 資料也會使用登錄區之外。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="ae3c7-174">例如，hello 資料檔案會更新由其他處理序 （也就不會鎖定 hello 檔案。）</span><span class="sxs-lookup"><span data-stu-id="ae3c7-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="ae3c7-175">需要 tooremain hello 基礎位置，即使之後卸除 hello 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="ae3c7-176">您需要自訂位置，例如非預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="ae3c7-177">登錄區以外的程式管理 hello 資料格式、 位置等等。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="ae3c7-178">如需詳細資訊，請參閱 hello [hive 控制檔內部和外部資料表簡介][ cindygross-hive-tables]部落格文章。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="ae3c7-179">使用者定義函數 (UDF)</span><span class="sxs-lookup"><span data-stu-id="ae3c7-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="ae3c7-180">Hive 也可透過 **使用者定義函數 (UDF)**延伸。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="ae3c7-181">UDF 可讓您 tooimplement 功能或 HiveQL 不容易模型化的邏輯。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="ae3c7-182">使用 Hive Udf 的範例，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae3c7-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="ae3c7-183">將 Java 使用者定義的函式與 Hive 搭配使用</span><span class="sxs-lookup"><span data-stu-id="ae3c7-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="ae3c7-184">使用 Python 使用者定義的函式搭配 Hive 和 Pig</span><span class="sxs-lookup"><span data-stu-id="ae3c7-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="ae3c7-185">使用 C# 使用者定義的函式搭配 Hive 和 Pig</span><span class="sxs-lookup"><span data-stu-id="ae3c7-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="ae3c7-186">使用者定義的自訂 Hive tooadd tooHDInsight 的運作方式</span><span class="sxs-lookup"><span data-stu-id="ae3c7-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="ae3c7-187">範例登錄區的使用者定義函數 tooconvert 日期/時間格式 tooHive 時間戳記</span><span class="sxs-lookup"><span data-stu-id="ae3c7-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="ae3c7-188"><a id="data"></a>範例資料</span><span class="sxs-lookup"><span data-stu-id="ae3c7-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="ae3c7-189">HDInsight 上的 Hive 已預先載入名為 `hivesampletable` 的內部資料表。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="ae3c7-190">HDInsight 也提供可搭配 Hive 使用的範例資料集。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="ae3c7-191">這些資料集儲存在 hello`/example/data`和`/HdiSamples`目錄。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="ae3c7-192">這些目錄存在於 hello 預設儲存體叢集。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="ae3c7-193"><a id="job"></a>範例 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="ae3c7-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="ae3c7-194">hello 下列 HiveQL 陳述式投射資料行拖曳至 hello`/example/data/sample.log`檔案：</span><span class="sxs-lookup"><span data-stu-id="ae3c7-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="ae3c7-195">Hello 上述範例中，在 hello HiveQL 陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae3c7-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="ae3c7-196">`set hive.execution.engine=tez;`： 設定 hello 執行引擎 toouse Tez。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="ae3c7-197">使用 Tez 而非 MapReduce，可以提升查詢效能。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="ae3c7-198">如需有關 Tez 的詳細資訊，請參閱 hello[來改善效能的使用 Apache Tez](#usetez) > 一節。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae3c7-199">只有在使用以 Windows 為基礎的 HDInsight 叢集時，才需要此陳述式。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="ae3c7-200">Tez 是以 Linux 為基礎的 HDInsight hello 預設執行引擎。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="ae3c7-201">`DROP TABLE`： 如果 hello 資料表已經存在，請將它刪除。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="ae3c7-202">`CREATE EXTERNAL TABLE`：在 Hive 中建立新的**外部**資料表。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="ae3c7-203">外部資料表只會儲存在登錄區中的 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="ae3c7-204">hello 原始位置，並以 hello 原始格式保留 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="ae3c7-205">`ROW FORMAT`： 會告知的 Hive hello 資料格式化的方式。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="ae3c7-206">在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="ae3c7-207">`STORED AS TEXTFILE LOCATION`： 會告知 Hive 其中 hello 資料會儲存 (hello`example/data`目錄)，則會儲存為文字。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="ae3c7-208">hello 資料可以在一個檔案，或分散 hello 目錄內的多個檔案。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="ae3c7-209">`SELECT`： 選取所有資料列計數，其中 hello 資料行**t4**包含 hello 值**[錯誤]**。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="ae3c7-210">這個陳述式會傳回值 **3**，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="ae3c7-211">`INPUT__FILE__NAME LIKE '%.log'`-Hive 嘗試 tooapply hello 結構描述 tooall 檔案 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="ae3c7-212">在此情況下，hello 目錄包含不符合 hello 結構描述的檔案。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="ae3c7-213">tooprevent 記憶體回收 hello 結果中的資料，此陳述式會告知登錄區，我們應該只會傳回資料從檔案結尾。 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="ae3c7-214">當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="ae3c7-215">例如，自動化的資料上傳程序，或 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="ae3c7-216">卸除的外部資料表沒有**不**刪除 hello 資料，它只會刪除 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="ae3c7-217">toocreate**內部**而不是外部資料表，請使用下列 HiveQL hello:</span><span class="sxs-lookup"><span data-stu-id="ae3c7-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="ae3c7-218">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae3c7-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="ae3c7-219">`CREATE TABLE IF NOT EXISTS`： 如果 hello 資料表不存在，建立它。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="ae3c7-220">因為 hello**外部**不是關鍵字，這個陳述式會建立內部資料表。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="ae3c7-221">hello 資料表儲存在 hello Hive 資料倉儲和 Hive 完全管理。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="ae3c7-222">`STORED AS ORC`: Hello 資料最佳化的資料列單欄式 (ORC) 格式儲存。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="ae3c7-223">ORC 是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="ae3c7-224">`INSERT OVERWRITE ... SELECT`： 選取資料列從 hello **log4jLogs**資料表，其中包含**[錯誤]**，然後插入 hello 資料到 hello 和**錯誤記錄檔**資料表。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="ae3c7-225">不同於外部資料表，卸除內部資料表也會刪除 hello 基礎資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="ae3c7-226">改善 Hive 查詢效能</span><span class="sxs-lookup"><span data-stu-id="ae3c7-226">Improve Hive query performance</span></span>

### <span data-ttu-id="ae3c7-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="ae3c7-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="ae3c7-228">[Apache Tez](http://tez.apache.org)是此架構可讓資料密集應用程式，例如登錄區，能更有效率地在標尺 toorun。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="ae3c7-229">對於以 Linux 為基礎的 HDInsight 叢集，Tez 預設為開啟。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="ae3c7-230">對於 Windows 型的 HDInsight 叢集，Tez 目前預設為關閉，因而必須啟用。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="ae3c7-231">Hive 查詢必須設定 tootake 優點 Tez，hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="ae3c7-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="ae3c7-232">Tez 是 hello 預設引擎以 Linux 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="ae3c7-233">hello [Hive Tez 設計文件上](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez)包含 hello 實作選項和微調組態詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="ae3c7-234">使用 Tez tooaid 偵錯作業中的執行，HDInsight 提供下列 Tez 工作的 tooview 詳細資料可讓您的 web Ui 的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae3c7-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="ae3c7-235">使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視</span><span class="sxs-lookup"><span data-stu-id="ae3c7-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="ae3c7-236">使用 Windows 為基礎的 HDInsight 上的 hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="ae3c7-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="ae3c7-237">低延遲分析處理 (LLAP)</span><span class="sxs-lookup"><span data-stu-id="ae3c7-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="ae3c7-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (有時也稱為 Live Long and Process) 是 Hive 2.0 的新功能，允許在記憶體中快取查詢。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="ae3c7-239">LLAP 會更快，向上的 Hive 查詢太[26 x 比 Hive 在某些情況下 1.x](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/)。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="ae3c7-240">HDInsight 提供 LLAP hello 互動式 Hive 叢集類型中。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="ae3c7-241">如需詳細資訊，請參閱 hello[開頭互動式 Hive](hdinsight-hadoop-use-interactive-hive.md)文件。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="ae3c7-242">Hive 工作和 SQL Server 整合服務</span><span class="sxs-lookup"><span data-stu-id="ae3c7-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="ae3c7-243">您可以使用 SQL Server Integration Services (SSIS) toorun Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="ae3c7-244">hello Azure Feature Pack for SSIS 提供 hello 遵循使用 HDInsight 的登錄區工作的元件。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="ae3c7-245">[Azure HDInsight Hive 工作][hivetask]</span><span class="sxs-lookup"><span data-stu-id="ae3c7-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="ae3c7-246">[Azure 訂用帳戶連接管理員][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="ae3c7-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="ae3c7-247">深入了解 hello Azure Feature Pack for SSIS[這裡][ssispack]。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="ae3c7-248"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="ae3c7-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ae3c7-249">既然您已經學會 Hive 的是，以及如何使用 hello 下列 HDInsight 中的 Hadoop 連結 tooexplore Azure HDInsight 以其他方式 toowork toouse。</span><span class="sxs-lookup"><span data-stu-id="ae3c7-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="ae3c7-250">[上傳資料 tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ae3c7-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ae3c7-251">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ae3c7-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ae3c7-252">[搭配 HDInsight 使用 MapReduce 作業][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ae3c7-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
