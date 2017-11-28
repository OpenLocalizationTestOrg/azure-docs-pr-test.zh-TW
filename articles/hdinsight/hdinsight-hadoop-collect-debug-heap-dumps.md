---
title: "aaaDebug 和分析堆積傾印-Azure 與 Hadoop 服務 |Microsoft 文件"
description: "自動收集 Hadoop 服務的堆積傾印，並放在 hello 偵錯和分析 Azure Blob 儲存體帳戶。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="5e0d6-103">收集在 Blob 儲存體 toodebug 堆積傾印和分析 Hadoop 服務</span><span class="sxs-lookup"><span data-stu-id="5e0d6-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="5e0d6-104">堆積的傾印包含 hello 應用程式的記憶體，包括 hello 變數的值在建立 hello 傾印的 hello 階段的快照集。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="5e0d6-105">因此它們有助於為執行階段發生的問題進行診斷。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="5e0d6-106">堆積的傾印可以自動 Hadoop 服務收集並放置於 hello Azure Blob 儲存體帳戶的使用者在 HDInsightHeapDumps /。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="5e0d6-107">在個別的叢集上的服務必須啟用 hello 收集各種服務的堆積傾印。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="5e0d6-108">這項功能的 hello 預設為關閉的 toobe 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="5e0d6-109">因此建議您 toomonitor hello Blob 儲存體帳戶它們會導致儲存一旦啟用 hello 集合，可能很大，這些堆積傾印。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e0d6-110">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5e0d6-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="5e0d6-112">本文章中的 hello 資訊僅適用於 tooWindows 為基礎的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="5e0d6-113">如需以 Linux 為基礎的 HDInsight 資訊，請參閱 [在以 Linux 為基礎的 HDInsight 上啟用 Hadoop 服務的堆積傾印](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="5e0d6-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="5e0d6-114">堆積傾印的合格服務</span><span class="sxs-lookup"><span data-stu-id="5e0d6-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="5e0d6-115">您可以啟用下列服務的 hello 的堆積傾印：</span><span class="sxs-lookup"><span data-stu-id="5e0d6-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="5e0d6-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="5e0d6-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="5e0d6-117">**hive** - hiveserver2、metastore、derbyserver</span><span class="sxs-lookup"><span data-stu-id="5e0d6-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="5e0d6-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="5e0d6-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="5e0d6-119">**yarn** - resourcemanager、nodemanager、timelineserver</span><span class="sxs-lookup"><span data-stu-id="5e0d6-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="5e0d6-120">**hdfs** - datanode、secondarynamenode、namenode</span><span class="sxs-lookup"><span data-stu-id="5e0d6-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="5e0d6-121">可啟用堆積傾印的組態元素</span><span class="sxs-lookup"><span data-stu-id="5e0d6-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="5e0d6-122">tooturn 堆積傾印服務上的，您需要 tooset hello 適當的組態項目 hello 區段中該服務，由指定**service_name**。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="5e0d6-123">hello 值**service_name**可以是任何此處所列的 hello 服務： tempelton，hiveserver2，中繼存放區，derbyserver，jobhistoryserver，resourcemanager，nodemanager，timelineserver，datanode，secondarynamenode，或namenode。</span><span class="sxs-lookup"><span data-stu-id="5e0d6-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="5e0d6-124">使用 Azure PowerShell 啟用</span><span class="sxs-lookup"><span data-stu-id="5e0d6-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="5e0d6-125">例如，tooturn 上使用 Azure PowerShell for jobhistoryserver 堆積傾印，您可以使用下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e0d6-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="5e0d6-126">使用 .NET SDK 啟用</span><span class="sxs-lookup"><span data-stu-id="5e0d6-126">Enable using .NET SDK</span></span>
<span data-ttu-id="5e0d6-127">例如，堆積傾印使用 jobhistoryserver hello Azure HDInsight.NET SDK 上的 tooturn，您可以使用下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e0d6-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
