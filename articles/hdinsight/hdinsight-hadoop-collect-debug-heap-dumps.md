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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>收集在 Blob 儲存體 toodebug 堆積傾印和分析 Hadoop 服務
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

堆積的傾印包含 hello 應用程式的記憶體，包括 hello 變數的值在建立 hello 傾印的 hello 階段的快照集。 因此它們有助於為執行階段發生的問題進行診斷。 堆積的傾印可以自動 Hadoop 服務收集並放置於 hello Azure Blob 儲存體帳戶的使用者在 HDInsightHeapDumps /。

在個別的叢集上的服務必須啟用 hello 收集各種服務的堆積傾印。 這項功能的 hello 預設為關閉的 toobe 叢集。 因此建議您 toomonitor hello Blob 儲存體帳戶它們會導致儲存一旦啟用 hello 集合，可能很大，這些堆積傾印。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 本文章中的 hello 資訊僅適用於 tooWindows 為基礎的 HDInsight。 如需以 Linux 為基礎的 HDInsight 資訊，請參閱 [在以 Linux 為基礎的 HDInsight 上啟用 Hadoop 服務的堆積傾印](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>堆積傾印的合格服務
您可以啟用下列服務的 hello 的堆積傾印：

* **hcatalog** - tempelton
* **hive** - hiveserver2、metastore、derbyserver
* **mapreduce** - jobhistoryserver
* **yarn** - resourcemanager、nodemanager、timelineserver
* **hdfs** - datanode、secondarynamenode、namenode

## <a name="configuration-elements-that-enable-heap-dumps"></a>可啟用堆積傾印的組態元素
tooturn 堆積傾印服務上的，您需要 tooset hello 適當的組態項目 hello 區段中該服務，由指定**service_name**。

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

hello 值**service_name**可以是任何此處所列的 hello 服務： tempelton，hiveserver2，中繼存放區，derbyserver，jobhistoryserver，resourcemanager，nodemanager，timelineserver，datanode，secondarynamenode，或namenode。

## <a name="enable-using-azure-powershell"></a>使用 Azure PowerShell 啟用
例如，tooturn 上使用 Azure PowerShell for jobhistoryserver 堆積傾印，您可以使用下列指令碼的 hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>使用 .NET SDK 啟用
例如，堆積傾印使用 jobhistoryserver hello Azure HDInsight.NET SDK 上的 tooturn，您可以使用下列程式碼的 hello:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
