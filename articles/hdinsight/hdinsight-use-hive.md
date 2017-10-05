---
title: "什麼是 Apache Hive 和 HiveQL - Azure HDInsight | Microsoft Docs"
description: "Apache Hive 是適用於 Hadoop 的資料倉儲系統。 您可以使用 HiveQL (這類似於 TRANSACT-SQL) 查詢 Hive 中儲存的資料。 在本文件中，您將了解如何使用 Hive 和 HiveQL 搭配 Azure HDInsight。"
keywords: "hiveql,什麼是 hive,hadoop hiveql,如何使用 hive,了解 hive,什麼是s hive"
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
ms.openlocfilehash: 6b3ee17141f773bec07cf40e0b6d63363e9b5164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="1316e-106">Azure HDInsight 上的 Apache Hive 和 HiveQL 是什麼？</span><span class="sxs-lookup"><span data-stu-id="1316e-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="1316e-107">[Apache Hive](http://hive.apache.org/) 是適用於 Hadoop 的資料倉儲系統。</span><span class="sxs-lookup"><span data-stu-id="1316e-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="1316e-108">Hive 可執行資料摘要、查詢以及資料分析。</span><span class="sxs-lookup"><span data-stu-id="1316e-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="1316e-109">Hive 查詢是以 HiveQL 撰寫而成，這是類似 SQL 的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="1316e-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="1316e-110">Hive 可讓您將結構投影在大量非結構化資料上。</span><span class="sxs-lookup"><span data-stu-id="1316e-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="1316e-111">定義結構後，您不需具備 Jave 或 MapReduce 相關知識，即可使用 HiveQL來查詢資料。</span><span class="sxs-lookup"><span data-stu-id="1316e-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="1316e-112">HDInsight 提供數種已針對特定工作負載進行微調的叢集類型。</span><span class="sxs-lookup"><span data-stu-id="1316e-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="1316e-113">下列叢集類型最常用於 Hive 查詢︰</span><span class="sxs-lookup"><span data-stu-id="1316e-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="1316e-114">__Interactive Hive__︰提供[低延遲分析處理 (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) 功能的 Hadoop 叢集，可改善互動式查詢的回應時間。</span><span class="sxs-lookup"><span data-stu-id="1316e-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="1316e-115">如需詳細資訊，請參閱[開始使用 HDInsight 中的 Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="1316e-115">For more information, see the [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="1316e-116">__Hadoop__︰已針對批次處理工作負載進行微調的 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="1316e-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="1316e-117">如需詳細資訊，請參閱[開始使用 HDInsight 中的 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="1316e-117">For more information, see the [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="1316e-118">__Spark__：Apache Spark 有可用於 Hive 的內建功能。</span><span class="sxs-lookup"><span data-stu-id="1316e-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="1316e-119">如需詳細資訊，請參閱[開始使用 HDInsight 上的 Spark](hdinsight-apache-spark-jupyter-spark-sql.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="1316e-119">For more information, see the [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="1316e-120">__HBase__：HiveQL 可以用來查詢 HBase 中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="1316e-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="1316e-121">如需詳細資訊，請參閱[開始使用 HDInsight 上的 HBase](hdinsight-hbase-tutorial-get-started-linux.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="1316e-121">For more information, see the [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="1316e-122">如何使用 Hive</span><span class="sxs-lookup"><span data-stu-id="1316e-122">How to use Hive</span></span>

<span data-ttu-id="1316e-123">使用下表了解如何使用 Hive 搭配 HDInsight︰</span><span class="sxs-lookup"><span data-stu-id="1316e-123">Use the following table to discover how to use Hive with HDInsight:</span></span>

| <span data-ttu-id="1316e-124">**使用此方法**，如果您想要...</span><span class="sxs-lookup"><span data-stu-id="1316e-124">**Use this method** if you want...</span></span> | <span data-ttu-id="1316e-125">...一個 **互動式** 殼層</span><span class="sxs-lookup"><span data-stu-id="1316e-125">...an **interactive** shell</span></span> | <span data-ttu-id="1316e-126">...**批次** 處理</span><span class="sxs-lookup"><span data-stu-id="1316e-126">...**batch** processing</span></span> | <span data-ttu-id="1316e-127">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="1316e-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="1316e-128">...從此 **用戶端作業系統**</span><span class="sxs-lookup"><span data-stu-id="1316e-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="1316e-129">Hive 檢視</span><span class="sxs-lookup"><span data-stu-id="1316e-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="1316e-130">✔</span><span class="sxs-lookup"><span data-stu-id="1316e-130">✔</span></span> |<span data-ttu-id="1316e-131">✔</span><span class="sxs-lookup"><span data-stu-id="1316e-131">✔</span></span> |<span data-ttu-id="1316e-132">Linux</span><span class="sxs-lookup"><span data-stu-id="1316e-132">Linux</span></span> |<span data-ttu-id="1316e-133">任何 (以瀏覽器為基礎)</span><span class="sxs-lookup"><span data-stu-id="1316e-133">Any (browser based)</span></span> |
| [<span data-ttu-id="1316e-134">Beeline 用戶端</span><span class="sxs-lookup"><span data-stu-id="1316e-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="1316e-135">✔</span><span class="sxs-lookup"><span data-stu-id="1316e-135">✔</span></span> |<span data-ttu-id="1316e-136">✔</span><span class="sxs-lookup"><span data-stu-id="1316e-136">✔</span></span> |<span data-ttu-id="1316e-137">Linux</span><span class="sxs-lookup"><span data-stu-id="1316e-137">Linux</span></span> |<span data-ttu-id="1316e-138">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="1316e-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1316e-139">REST API</span><span class="sxs-lookup"><span data-stu-id="1316e-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="1316e-140">✔</span><span class="sxs-lookup"><span data-stu-id="1316e-140">✔</span></span> |<span data-ttu-id="1316e-141">Linux 或 Windows*</span><span class="sxs-lookup"><span data-stu-id="1316e-141">Linux or Windows*</span></span> |<span data-ttu-id="1316e-142">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="1316e-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="1316e-143">HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1316e-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="1316e-144">✔</span><span class="sxs-lookup"><span data-stu-id="1316e-144">✔</span></span> |<span data-ttu-id="1316e-145">Linux 或 Windows*</span><span class="sxs-lookup"><span data-stu-id="1316e-145">Linux or Windows*</span></span> |<span data-ttu-id="1316e-146">Windows</span><span class="sxs-lookup"><span data-stu-id="1316e-146">Windows</span></span> |
| [<span data-ttu-id="1316e-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1316e-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="1316e-148">✔</span><span class="sxs-lookup"><span data-stu-id="1316e-148">✔</span></span> |<span data-ttu-id="1316e-149">Linux 或 Windows*</span><span class="sxs-lookup"><span data-stu-id="1316e-149">Linux or Windows*</span></span> |<span data-ttu-id="1316e-150">Windows</span><span class="sxs-lookup"><span data-stu-id="1316e-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="1316e-151">\* Linux 是 HDInsight 3.4 版或更新版本上唯一使用的作業系統。</span><span class="sxs-lookup"><span data-stu-id="1316e-151">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1316e-152">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="1316e-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="1316e-153">如果您使用以 Windows 為基礎的 HDInsight 叢集，您可以從瀏覽器或[遠端桌面](hdinsight-hadoop-use-hive-remote-desktop.md)使用[查詢主控台](hdinsight-hadoop-use-hive-query-console.md)來執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="1316e-153">If you are using a Windows-based HDInsight cluster, you can use the [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) to run Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="1316e-154">HiveQL 語言參考</span><span class="sxs-lookup"><span data-stu-id="1316e-154">HiveQL language reference</span></span>

<span data-ttu-id="1316e-155">在[語言手冊 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual) 中可取得 HiveQL 語言參考。</span><span class="sxs-lookup"><span data-stu-id="1316e-155">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="1316e-156">Hive 和資料結構</span><span class="sxs-lookup"><span data-stu-id="1316e-156">Hive and data structure</span></span>

<span data-ttu-id="1316e-157">Hive 了解如何使用結構化和半結構化資料。</span><span class="sxs-lookup"><span data-stu-id="1316e-157">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="1316e-158">例如，以特定字元分隔欄位的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="1316e-158">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="1316e-159">下列 HiveQL 陳述式會使用以空格分隔的資料建立資料表︰</span><span class="sxs-lookup"><span data-stu-id="1316e-159">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="1316e-160">Hive 也支援自訂複雜或不規則結構化資料的 **序列化/反序列化程式 (SerDe)** 。</span><span class="sxs-lookup"><span data-stu-id="1316e-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="1316e-161">如需詳細資訊，請參閱[如何搭配 HDInsight 使用自訂 JSON SerDe](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) 文件 (英文)。</span><span class="sxs-lookup"><span data-stu-id="1316e-161">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="1316e-162">如需 Hive 所支援檔案格式的詳細資訊，請參閱[語言手冊 (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="1316e-162">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="1316e-163">Hive 內部和外部資料表比較。</span><span class="sxs-lookup"><span data-stu-id="1316e-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="1316e-164">您可以使用 Hive 建立兩種類型的資料表：</span><span class="sxs-lookup"><span data-stu-id="1316e-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="1316e-165">__內部__︰資料會儲存在 Hive 資料倉儲中。</span><span class="sxs-lookup"><span data-stu-id="1316e-165">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="1316e-166">資料倉儲位於叢集之預設儲存體上的 `/hive/warehouse/`。</span><span class="sxs-lookup"><span data-stu-id="1316e-166">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="1316e-167">使用內部資料表的時機︰</span><span class="sxs-lookup"><span data-stu-id="1316e-167">Use internal tables when:</span></span>

    * <span data-ttu-id="1316e-168">資料是暫存的。</span><span class="sxs-lookup"><span data-stu-id="1316e-168">Data is temporary.</span></span>
    * <span data-ttu-id="1316e-169">您想要 Hive 管理資料表和資料的生命週期。</span><span class="sxs-lookup"><span data-stu-id="1316e-169">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="1316e-170">__外部__︰資料會儲存在資料倉儲之外。</span><span class="sxs-lookup"><span data-stu-id="1316e-170">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="1316e-171">資料可以儲存在叢集可存取的任何儲存體上。</span><span class="sxs-lookup"><span data-stu-id="1316e-171">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="1316e-172">使用外部資料表的時機︰</span><span class="sxs-lookup"><span data-stu-id="1316e-172">Use external tables when:</span></span>

    * <span data-ttu-id="1316e-173">資料也使用於 Hive 之外。</span><span class="sxs-lookup"><span data-stu-id="1316e-173">The data is also used outside of Hive.</span></span> <span data-ttu-id="1316e-174">例如，資料檔案由其他程序所更新 (不會鎖定檔案)。</span><span class="sxs-lookup"><span data-stu-id="1316e-174">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="1316e-175">即使在刪除資料表後，資料都必須保留在基礎位置。</span><span class="sxs-lookup"><span data-stu-id="1316e-175">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="1316e-176">您需要自訂位置，例如非預設儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1316e-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="1316e-177">Hive 以外的程式管理資料格式、位置等等。</span><span class="sxs-lookup"><span data-stu-id="1316e-177">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="1316e-178">如需詳細資訊，請參閱 [Hive 內部和外部資料表簡介][cindygross-hive-tables]部落格文章。</span><span class="sxs-lookup"><span data-stu-id="1316e-178">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="1316e-179">使用者定義函數 (UDF)</span><span class="sxs-lookup"><span data-stu-id="1316e-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="1316e-180">Hive 也可透過 **使用者定義函數 (UDF)**延伸。</span><span class="sxs-lookup"><span data-stu-id="1316e-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="1316e-181">UDF 可讓您在 HiveQL 中實作功能或不易模型化的邏輯。</span><span class="sxs-lookup"><span data-stu-id="1316e-181">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="1316e-182">如需將 UDF 與 Hive 搭配使用的範例，請參閱以下文件：</span><span class="sxs-lookup"><span data-stu-id="1316e-182">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="1316e-183">將 Java 使用者定義的函式與 Hive 搭配使用</span><span class="sxs-lookup"><span data-stu-id="1316e-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="1316e-184">使用 Python 使用者定義的函式搭配 Hive 和 Pig</span><span class="sxs-lookup"><span data-stu-id="1316e-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="1316e-185">使用 C# 使用者定義的函式搭配 Hive 和 Pig</span><span class="sxs-lookup"><span data-stu-id="1316e-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="1316e-186">如何將自訂 Hive 使用者定義的函式新增至 HDInsight</span><span class="sxs-lookup"><span data-stu-id="1316e-186">How to add a custom Hive user-defined function to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="1316e-187">可將日期/時間格式轉換成 Hive 時間戳記的範例 Hive 使用者定義函式</span><span class="sxs-lookup"><span data-stu-id="1316e-187">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="1316e-188"><a id="data"></a>範例資料</span><span class="sxs-lookup"><span data-stu-id="1316e-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="1316e-189">HDInsight 上的 Hive 已預先載入名為 `hivesampletable` 的內部資料表。</span><span class="sxs-lookup"><span data-stu-id="1316e-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="1316e-190">HDInsight 也提供可搭配 Hive 使用的範例資料集。</span><span class="sxs-lookup"><span data-stu-id="1316e-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="1316e-191">這些資料集會儲存在 `/example/data` 和 `/HdiSamples` 目錄中。</span><span class="sxs-lookup"><span data-stu-id="1316e-191">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="1316e-192">這些目錄存在於您叢集的預設儲存體中。</span><span class="sxs-lookup"><span data-stu-id="1316e-192">These directories exist in the default storage for your cluster.</span></span>

## <span data-ttu-id="1316e-193"><a id="job"></a>範例 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="1316e-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="1316e-194">下列 HiveQL 陳述式將資料行投影在 `/example/data/sample.log` 檔案︰</span><span class="sxs-lookup"><span data-stu-id="1316e-194">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="1316e-195">在上一個範例中，HiveQL 陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="1316e-195">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="1316e-196">`set hive.execution.engine=tez;`：設定執行引擎以使用 Tez。</span><span class="sxs-lookup"><span data-stu-id="1316e-196">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="1316e-197">使用 Tez 而非 MapReduce，可以提升查詢效能。</span><span class="sxs-lookup"><span data-stu-id="1316e-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="1316e-198">如需 Tez 的詳細資訊，請參閱 [使用 Apache Tez 以提升效能](#usetez) 一節。</span><span class="sxs-lookup"><span data-stu-id="1316e-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1316e-199">只有在使用以 Windows 為基礎的 HDInsight 叢集時，才需要此陳述式。</span><span class="sxs-lookup"><span data-stu-id="1316e-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="1316e-200">Tez 是以 Linux 為基礎的 HDInsight 預設的執行引擎。</span><span class="sxs-lookup"><span data-stu-id="1316e-200">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="1316e-201">`DROP TABLE`︰如果資料表已存在，請刪除資料表。</span><span class="sxs-lookup"><span data-stu-id="1316e-201">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="1316e-202">`CREATE EXTERNAL TABLE`：在 Hive 中建立新的**外部**資料表。</span><span class="sxs-lookup"><span data-stu-id="1316e-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="1316e-203">外部資料表只會將資料表定義儲存在 Hive 中。</span><span class="sxs-lookup"><span data-stu-id="1316e-203">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="1316e-204">資料會留在原來的位置，並保持原始格式。</span><span class="sxs-lookup"><span data-stu-id="1316e-204">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="1316e-205">`ROW FORMAT`：告訴 Hive 如何格式化資料。</span><span class="sxs-lookup"><span data-stu-id="1316e-205">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="1316e-206">在此情況下，每個記錄中的欄位會以空格隔開。</span><span class="sxs-lookup"><span data-stu-id="1316e-206">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="1316e-207">`STORED AS TEXTFILE LOCATION`：將資料的儲存位置告訴 Hive (`example/data` 目錄)，且資料會儲存為文字。</span><span class="sxs-lookup"><span data-stu-id="1316e-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="1316e-208">資料可以在目錄的一個檔案中，也可以分散在多個檔案中。</span><span class="sxs-lookup"><span data-stu-id="1316e-208">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="1316e-209">`SELECT`：選取資料行 **t4** 包含 **[ERROR]** 值的所有資料列計數。</span><span class="sxs-lookup"><span data-stu-id="1316e-209">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="1316e-210">這個陳述式會傳回值 **3**，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="1316e-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="1316e-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive 嘗試將結構描述套用至目錄中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="1316e-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="1316e-212">在此情況下，目錄包含不符合結構描述的檔案。</span><span class="sxs-lookup"><span data-stu-id="1316e-212">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="1316e-213">若要防止結果中出現亂碼資料，此陳述式會告訴 Hive 我們只應該從檔名以 log 結尾的檔案傳回資料。</span><span class="sxs-lookup"><span data-stu-id="1316e-213">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="1316e-214">當您預期會由外部來源來更新基礎資料時，請使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="1316e-214">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="1316e-215">例如，自動化的資料上傳程序，或 MapReduce 作業。</span><span class="sxs-lookup"><span data-stu-id="1316e-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="1316e-216">捨棄外部資料表並「不會」  刪除資料，只會刪除資料表定義。</span><span class="sxs-lookup"><span data-stu-id="1316e-216">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="1316e-217">若要建立**內部**資料表，而不是外部資料表，請使用下列 HiveQL：</span><span class="sxs-lookup"><span data-stu-id="1316e-217">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="1316e-218">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="1316e-218">These statements perform the following actions:</span></span>

* <span data-ttu-id="1316e-219">`CREATE TABLE IF NOT EXISTS`︰如果資料表不存在，請建立資料表。</span><span class="sxs-lookup"><span data-stu-id="1316e-219">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="1316e-220">因為未使用 **EXTERNAL** 關鍵字，這個陳述式會建立內部資料表。</span><span class="sxs-lookup"><span data-stu-id="1316e-220">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="1316e-221">資料表會儲存在 Hive 資料倉儲中，並完全受到 Hive 所管理。</span><span class="sxs-lookup"><span data-stu-id="1316e-221">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="1316e-222">`STORED AS ORC`：以最佳化資料列單欄式 (Optimized Row Columnar, ORC) 格式儲存資料。</span><span class="sxs-lookup"><span data-stu-id="1316e-222">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="1316e-223">ORC 是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="1316e-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="1316e-224">`INSERT OVERWRITE ... SELECT`：從 **log4jLogs** 資料表選取包含 **[ERROR]** 的資料列，然後將資料插入 **errorLogs** 資料表。</span><span class="sxs-lookup"><span data-stu-id="1316e-224">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="1316e-225">與外部資料表不同之處在於，捨棄內部資料表也會刪除基礎資料。</span><span class="sxs-lookup"><span data-stu-id="1316e-225">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="1316e-226">改善 Hive 查詢效能</span><span class="sxs-lookup"><span data-stu-id="1316e-226">Improve Hive query performance</span></span>

### <span data-ttu-id="1316e-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="1316e-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="1316e-228">[Apache Tez](http://tez.apache.org) 是可讓資料高用量應用程式 (例如 Hive)，以大規模而更有效率方式執行作業的架構。</span><span class="sxs-lookup"><span data-stu-id="1316e-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="1316e-229">對於以 Linux 為基礎的 HDInsight 叢集，Tez 預設為開啟。</span><span class="sxs-lookup"><span data-stu-id="1316e-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="1316e-230">對於 Windows 型的 HDInsight 叢集，Tez 目前預設為關閉，因而必須啟用。</span><span class="sxs-lookup"><span data-stu-id="1316e-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="1316e-231">若要充分發揮 Tez 的效益，您必須設定 Hive 查詢的下列值：</span><span class="sxs-lookup"><span data-stu-id="1316e-231">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="1316e-232">對於以 Linux 為基礎的 HDInsight 叢集，Tez 是預設引擎。</span><span class="sxs-lookup"><span data-stu-id="1316e-232">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="1316e-233">[Tez 上的 Hive 設計文件](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez)包含實作選擇和調整組態的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1316e-233">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="1316e-234">為了使用 Tez 來協助偵錯作業，HDInsight 提供下列 Web UI，讓您檢視 Tez 作業的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="1316e-234">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="1316e-235">在以 Linux 為基礎的 HDInsight 上使用 Ambari Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="1316e-235">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="1316e-236">在以 Windows 為基礎的 HDInsight 上使用 Tez UI</span><span class="sxs-lookup"><span data-stu-id="1316e-236">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="1316e-237">低延遲分析處理 (LLAP)</span><span class="sxs-lookup"><span data-stu-id="1316e-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="1316e-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (有時也稱為 Live Long and Process) 是 Hive 2.0 的新功能，允許在記憶體中快取查詢。</span><span class="sxs-lookup"><span data-stu-id="1316e-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="1316e-239">LLAP 讓 Hive 查詢的速讀變快，在某些情況下可達到[比 Hive 1.x 快 26 倍](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/)。</span><span class="sxs-lookup"><span data-stu-id="1316e-239">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="1316e-240">HDInsight 可提供 Interactive Hive 叢集類型的 LLAP。</span><span class="sxs-lookup"><span data-stu-id="1316e-240">HDInsight provides LLAP in the Interactive Hive cluster type.</span></span> <span data-ttu-id="1316e-241">如需詳細資訊，請參閱[開始使用 Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="1316e-241">For more information, see the [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="1316e-242">Hive 工作和 SQL Server 整合服務</span><span class="sxs-lookup"><span data-stu-id="1316e-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="1316e-243">您可以使用 SQL Server Integration Services (SSIS) 來執行 Hive 作業。</span><span class="sxs-lookup"><span data-stu-id="1316e-243">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="1316e-244">適用於 SSIS 的 Azure Feature Pack 中提供下列元件可搭配 HDInsight 上的 Hive 工作使用。</span><span class="sxs-lookup"><span data-stu-id="1316e-244">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="1316e-245">[Azure HDInsight Hive 工作][hivetask]</span><span class="sxs-lookup"><span data-stu-id="1316e-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="1316e-246">[Azure 訂用帳戶連接管理員][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="1316e-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="1316e-247">在[這裡][ssispack]深入了解適用於 SSIS 的 Azure Feature Pack。</span><span class="sxs-lookup"><span data-stu-id="1316e-247">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="1316e-248"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="1316e-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="1316e-249">現在您已了解什麼是 Hive 以及如何搭配 HDInsight 中的 Hadoop 使用它，接著請使用下列連結探索 Azure HDInsight 的其他使用方式。</span><span class="sxs-lookup"><span data-stu-id="1316e-249">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="1316e-250">[將資料上傳至 HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="1316e-250">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="1316e-251">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1316e-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="1316e-252">[搭配 HDInsight 使用 MapReduce 作業][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="1316e-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
