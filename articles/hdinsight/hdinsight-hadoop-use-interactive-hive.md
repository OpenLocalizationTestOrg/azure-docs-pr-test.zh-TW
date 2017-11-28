---
title: "在 HDInsight 中使用互動式 Hive - Azure | Microsoft Docs"
description: "了解如何在 HDInsight 中使用互動式 Hive (LLAP 上的 Hive)。"
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
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="75974-103">在 HDInsight 中使用互動式 Hive (預覽)</span><span class="sxs-lookup"><span data-stu-id="75974-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="75974-104">互動式 Hive (又稱為.</span><span class="sxs-lookup"><span data-stu-id="75974-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="75974-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) 為新的 HDInsight [叢集類型](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。</span><span class="sxs-lookup"><span data-stu-id="75974-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="75974-106">互動式 Hive 允許記憶體內快取，可讓 Hive 查詢更具互動性且速度更快。</span><span class="sxs-lookup"><span data-stu-id="75974-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="75974-107">這項新功能讓 HDInsight 成為全世界效能、彈性和開放性最佳的雲端巨量資料方案之一，因其具有記憶體內快取 (使用 Hive 和 Spark) 與進階分析功能，而這些功能是透過與 R 服務深入整合而來。</span><span class="sxs-lookup"><span data-stu-id="75974-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solutions on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="75974-108">互動式 Hive 叢集與 Hadoop 叢集不同。</span><span class="sxs-lookup"><span data-stu-id="75974-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="75974-109">它只包含 Hive 服務。</span><span class="sxs-lookup"><span data-stu-id="75974-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="75974-110">很快地，MapReduce、Pig、Sqoop、Oozie 和其他服務便會從這個叢集類型中移除。</span><span class="sxs-lookup"><span data-stu-id="75974-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="75974-111">互動式 Hive 叢集中的 Hive 服務只能透過 Ambari Hive 檢視、Beeline 和 Hive ODBC 存取。</span><span class="sxs-lookup"><span data-stu-id="75974-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="75974-112">無法透過 Hive 主控台、Templeton、Azure CLI 和 Azure PowerShell 存取。</span><span class="sxs-lookup"><span data-stu-id="75974-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="75974-113">建立互動式 Hive 叢集</span><span class="sxs-lookup"><span data-stu-id="75974-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="75974-114">只有以 Linux 為基礎的叢集可支援互動式 Hive 叢集。</span><span class="sxs-lookup"><span data-stu-id="75974-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="75974-115">如需建立 HDInsight 叢集的相關資訊，請參閱[在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="75974-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="75974-116">從互動式 Hive 執行 Hive</span><span class="sxs-lookup"><span data-stu-id="75974-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="75974-117">Hive 查詢的執行方式有不同選項可供您選擇︰</span><span class="sxs-lookup"><span data-stu-id="75974-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="75974-118">使用 Ambari Hive 檢視執行 Hive</span><span class="sxs-lookup"><span data-stu-id="75974-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="75974-119">如需使用 Hive 檢視的相關資訊，請參閱[在 HDInsight 中搭配 Hadoop 使用 Hive 檢視](hdinsight-hadoop-use-hive-ambari-view.md)。</span><span class="sxs-lookup"><span data-stu-id="75974-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="75974-120">使用 Beeline 執行 Hive</span><span class="sxs-lookup"><span data-stu-id="75974-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="75974-121">如需在 HDInsight 上使用 Beeline 的相關資訊，請參閱[利用 Beeline 搭配使用 Hive 與 HDInsight 中的 Hadoop](hdinsight-hadoop-use-hive-beeline.md)。</span><span class="sxs-lookup"><span data-stu-id="75974-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="75974-122">您可以從前端節點或空白邊緣節點使用 Beeline。</span><span class="sxs-lookup"><span data-stu-id="75974-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="75974-123">我們的建議是從空白邊緣節點使用 Beeline。</span><span class="sxs-lookup"><span data-stu-id="75974-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="75974-124">如需使用空白邊緣節點建立 HDInsight 叢集的相關資訊，請參閱[在 HDInsight 中使用空白邊緣節點](hdinsight-apps-use-edge-node.md)。</span><span class="sxs-lookup"><span data-stu-id="75974-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="75974-125">使用 Hive ODBC 執行 Hive</span><span class="sxs-lookup"><span data-stu-id="75974-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="75974-126">如需使用 Hive ODBC 的相關資訊，請參閱[使用 Microsoft Hive ODBC 驅動程式將 Excel 連接到 Hadoop](hdinsight-connect-excel-hive-odbc-driver.md)。</span><span class="sxs-lookup"><span data-stu-id="75974-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="75974-127">**若要尋找 JDBC 連接字串︰**</span><span class="sxs-lookup"><span data-stu-id="75974-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="75974-128">使用下列 URL 登入 Ambari：https://<ClusterName>.AzureHDInsight.net。</span><span class="sxs-lookup"><span data-stu-id="75974-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="75974-129">按一下左側功能表中的 [Hive]  。</span><span class="sxs-lookup"><span data-stu-id="75974-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="75974-130">按一下醒目提示的圖示複製 URL：</span><span class="sxs-lookup"><span data-stu-id="75974-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![HDInsight Hadoop 互動式 Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="75974-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="75974-132">See also</span></span>
* <span data-ttu-id="75974-133">[在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)︰了解如何在 HDInsight 中建立互動式 Hive 叢集。</span><span class="sxs-lookup"><span data-stu-id="75974-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="75974-134">[利用 Beeline 搭配使用 Hive 與 HDInsight 中的 Hadoop](hdinsight-hadoop-use-hive-beeline.md)︰了解如何使用 Beeline 提交 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="75974-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="75974-135">[使用 Microsoft Hive ODBC 驅動程式將 Excel 連接到 Hadoop](hdinsight-connect-excel-hive-odbc-driver.md)：了解如何將 Excel 連接到 Hive。</span><span class="sxs-lookup"><span data-stu-id="75974-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>

