---
title: "HDInsight 的 Azure 中的互動式 Hive aaaUse |Microsoft 文件"
description: "深入了解如何 toouse 互動式在 HDInsight Hive （LLAP 上的登錄區）。"
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="3f0b1-103">在 HDInsight 中使用互動式 Hive (預覽)</span><span class="sxs-lookup"><span data-stu-id="3f0b1-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="3f0b1-104">互動式 Hive (又稱為.</span><span class="sxs-lookup"><span data-stu-id="3f0b1-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="3f0b1-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) 為新的 HDInsight [叢集類型](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="3f0b1-106">互動式 Hive 允許記憶體內快取，可讓 Hive 查詢更具互動性且速度更快。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="3f0b1-107">這項新功能讓其中一個 hello HDInsight 世界上大部分高效能、 彈性且開啟巨量資料解決方案 hello 雲端上的記憶體中快取 （使用 Hive 和 Spark） 以及進階分析透過深層整合與 R Services。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="3f0b1-108">hello 互動式 Hive 叢集與不同 hello Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="3f0b1-109">它只包含 hello 登錄區服務。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="3f0b1-110">很快地，MapReduce、Pig、Sqoop、Oozie 和其他服務便會從這個叢集類型中移除。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="3f0b1-111">hello hello 互動式 Hive 叢集中的 Hive 服務僅可透過 hello Ambari Hive 檢視、 Beeline 和 Hive ODBC 存取。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="3f0b1-112">無法透過 Hive 主控台、Templeton、Azure CLI 和 Azure PowerShell 存取。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="3f0b1-113">建立互動式 Hive 叢集</span><span class="sxs-lookup"><span data-stu-id="3f0b1-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="3f0b1-114">只有以 Linux 為基礎的叢集可支援互動式 Hive 叢集。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="3f0b1-115">如需建立 HDInsight 叢集的相關資訊，請參閱[在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="3f0b1-116">從互動式 Hive 執行 Hive</span><span class="sxs-lookup"><span data-stu-id="3f0b1-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="3f0b1-117">Hive 查詢的執行方式有不同選項可供您選擇︰</span><span class="sxs-lookup"><span data-stu-id="3f0b1-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="3f0b1-118">執行 Hive 使用 hello Ambari 登錄區檢視</span><span class="sxs-lookup"><span data-stu-id="3f0b1-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="3f0b1-119">Hello 使用 hello Hive 檢視相關的資訊，請參閱[使用 hello HDInsight 中的 Hadoop hive 控制檔的檢視](hdinsight-hadoop-use-hive-ambari-view.md)。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="3f0b1-120">使用 Beeline 執行 Hive</span><span class="sxs-lookup"><span data-stu-id="3f0b1-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="3f0b1-121">在 HDInsight 上使用 Beeline hello 資訊，請參閱[Beeline 與 HDInsight 中的 Hadoop Hive 使用](hdinsight-hadoop-use-hive-beeline.md)。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="3f0b1-122">您可以使用 Beeline hello 叢集前端節點或空白邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="3f0b1-123">我們的建議是從空白邊緣節點使用 Beeline。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="3f0b1-124">如需使用空白邊緣節點建立 HDInsight 叢集的相關資訊，請參閱[在 HDInsight 中使用空白邊緣節點](hdinsight-apps-use-edge-node.md)。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="3f0b1-125">使用 Hive ODBC 執行 Hive</span><span class="sxs-lookup"><span data-stu-id="3f0b1-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="3f0b1-126">使用 Hive ODBC hello 資訊，請參閱[hello Microsoft Hive ODBC 驅動程式連接的 Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="3f0b1-127">**toofind hello JDBC 連接字串：**</span><span class="sxs-lookup"><span data-stu-id="3f0b1-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="3f0b1-128">登入使用下列 URL 的 hello tooAmbari: https://<ClusterName>。.Azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="3f0b1-129">按一下**Hive** hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="3f0b1-130">按一下反白顯示 hello 圖示 toocopy hello URL:</span><span class="sxs-lookup"><span data-stu-id="3f0b1-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![HDInsight Hadoop 互動式 Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="3f0b1-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3f0b1-132">See also</span></span>
* <span data-ttu-id="3f0b1-133">[在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)： 了解互動式 Hive toocreate HDInsight 中的叢集。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="3f0b1-134">[使用具有 Beeline HDInsight 中的 Hadoop Hive](hdinsight-hadoop-use-hive-beeline.md)： 了解如何 toouse Beeline toosubmit Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="3f0b1-135">[Hello Microsoft Hive ODBC 驅動程式連接 Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)： 了解如何 tooconnect Excel tooHive。</span><span class="sxs-lookup"><span data-stu-id="3f0b1-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

