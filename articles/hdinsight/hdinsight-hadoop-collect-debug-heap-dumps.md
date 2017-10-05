---
title: "利用堆積傾印偵錯和分析 Hadoop 服務 - Azure |Microsoft Docs"
description: "自動為 Hadoop 服務收集堆積傾印，並放在 Azure Blob 儲存體帳戶內以供偵錯和分析。"
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
ms.openlocfilehash: 6d1d4d47d279eb7a1f0bf1f587445683f0ace7a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="6899e-103">收集 Blob 儲存體中的堆積傾印以偵錯和分析 Hadoop 服務</span><span class="sxs-lookup"><span data-stu-id="6899e-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="6899e-104">堆積傾印含有應用程式記憶體的快照，其中包括建立傾印時的變數值。</span><span class="sxs-lookup"><span data-stu-id="6899e-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="6899e-105">因此它們有助於為執行階段發生的問題進行診斷。</span><span class="sxs-lookup"><span data-stu-id="6899e-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="6899e-106">系統可以自動為 Hadoop 服務收集堆積傾印，並放在使用者之 Azure Blob 儲存體帳戶內的 HDInsightHeapDumps/ 下。</span><span class="sxs-lookup"><span data-stu-id="6899e-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="6899e-107">啟用各種服務的堆積傾印收集時，必須針對個別叢集上的服務啟用。</span><span class="sxs-lookup"><span data-stu-id="6899e-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="6899e-108">叢集的這項功能預設為關閉。</span><span class="sxs-lookup"><span data-stu-id="6899e-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="6899e-109">這些堆積傾印的大小可能會很大，因此一旦啟用收集，建議您監視儲存這些傾印的 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6899e-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6899e-110">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="6899e-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6899e-111">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="6899e-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="6899e-112">本文的資訊僅適用於以 Windows 為基礎的 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="6899e-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="6899e-113">如需以 Linux 為基礎的 HDInsight 資訊，請參閱 [在以 Linux 為基礎的 HDInsight 上啟用 Hadoop 服務的堆積傾印](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="6899e-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="6899e-114">堆積傾印的合格服務</span><span class="sxs-lookup"><span data-stu-id="6899e-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="6899e-115">您可以啟用下列服務的堆積傾印：</span><span class="sxs-lookup"><span data-stu-id="6899e-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="6899e-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="6899e-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="6899e-117">**hive** - hiveserver2、metastore、derbyserver</span><span class="sxs-lookup"><span data-stu-id="6899e-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="6899e-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="6899e-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="6899e-119">**yarn** - resourcemanager、nodemanager、timelineserver</span><span class="sxs-lookup"><span data-stu-id="6899e-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="6899e-120">**hdfs** - datanode、secondarynamenode、namenode</span><span class="sxs-lookup"><span data-stu-id="6899e-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="6899e-121">可啟用堆積傾印的組態元素</span><span class="sxs-lookup"><span data-stu-id="6899e-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="6899e-122">為了開啟服務的堆積傾印，您必須在該服務的區段 (由 **service_name** 指定) 中，設定適當的組態元素。</span><span class="sxs-lookup"><span data-stu-id="6899e-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="6899e-123">**service_name** 的值可以是此處所列的任何服務：tempelton、hiveserver2、metastore、derbyserver、jobhistoryserver、resourcemanager、nodemanager、timelineserver、datanode、secondarynamenode 或 namenode。</span><span class="sxs-lookup"><span data-stu-id="6899e-123">The value of **service_name** can be any of the services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="6899e-124">使用 Azure PowerShell 啟用</span><span class="sxs-lookup"><span data-stu-id="6899e-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="6899e-125">例如，若要使用 Azure PowerShell 來開啟 jobhistoryserver 的堆積傾印，可以使用下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="6899e-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use the following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="6899e-126">使用 .NET SDK 啟用</span><span class="sxs-lookup"><span data-stu-id="6899e-126">Enable using .NET SDK</span></span>
<span data-ttu-id="6899e-127">例如，若要使用 Azure HDInsight .NET SDK 來開啟 jobhistoryserver 的堆積傾印，您可以使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6899e-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you can use the following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
