---
title: "搭配 HBase 使用 Apache Phoenix 和 SQuirreL - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 HDinsight 中的 Apache Phoenix，以及如何在您的工作站上安裝與設定 SQuirreL 以連線到 HDInsight 中的 HBase 叢集。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="35114-103">在 HDInsight 中搭配 Linux 型 HBase 叢集使用 Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="35114-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="35114-104">了解如何在 HDInsight 中使用 [Apache Phoenix](http://phoenix.apache.org/) ，以及如何使用 SQLLine。</span><span class="sxs-lookup"><span data-stu-id="35114-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="35114-105">如需有關 Phoenix 的詳細資訊，請參閱 [15 分鐘內了解 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)。</span><span class="sxs-lookup"><span data-stu-id="35114-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="35114-106">如需 Phoenix 文法，請參閱 [Phoenix 文法](http://phoenix.apache.org/language/index.html)。</span><span class="sxs-lookup"><span data-stu-id="35114-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="35114-107">如需 HDInsight 中的 Phoenix 版本資訊，請參閱 [HDInsight 在 Hadoop 叢集版本中提供什麼新功能？](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="35114-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="35114-108">使用 SQLLine</span><span class="sxs-lookup"><span data-stu-id="35114-108">Use SQLLine</span></span>
<span data-ttu-id="35114-109">[SQLLine](http://sqlline.sourceforge.net/) \(英文\) 是執行 SQL 的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="35114-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="35114-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="35114-110">Prerequisites</span></span>
<span data-ttu-id="35114-111">開始使用 SQLLine 之前，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="35114-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="35114-112">**HDInsight 中的 HBase 叢集**。</span><span class="sxs-lookup"><span data-stu-id="35114-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="35114-113">如需有關佈建 HBase 叢集的資訊，請參閱[開始使用 HDInsight 中的 Apache HBase][hdinsight-hbase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="35114-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="35114-114">**透過遠端桌面通訊協定連接到 HBase 叢集**。</span><span class="sxs-lookup"><span data-stu-id="35114-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="35114-115">如需指示，請參閱[使用 Azure 入口網站管理 HDInsight 中的 Hadoop 叢集][hdinsight-manage-portal]。</span><span class="sxs-lookup"><span data-stu-id="35114-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="35114-116">連線到 HBase 叢集時，您必須連線到其中一個 Zookeeper。</span><span class="sxs-lookup"><span data-stu-id="35114-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="35114-117">每個 HDInsight 叢集有三個 Zookeeper。</span><span class="sxs-lookup"><span data-stu-id="35114-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="35114-118">**找出 Zookeeper 主機名稱**</span><span class="sxs-lookup"><span data-stu-id="35114-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="35114-119">瀏覽至 **https://<ClusterName>.azurehdinsight.net** 來開啟 Ambari。</span><span class="sxs-lookup"><span data-stu-id="35114-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="35114-120">輸入 HTTP (叢集) 使用者名稱和密碼來登入。</span><span class="sxs-lookup"><span data-stu-id="35114-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="35114-121">在左側功能表中，按一下 [ZooKeeper]  。</span><span class="sxs-lookup"><span data-stu-id="35114-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="35114-122">您會看到列出三個「ZooKeeper 伺服器」。</span><span class="sxs-lookup"><span data-stu-id="35114-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="35114-123">按一下其中一台列出的「ZooKeeper 伺服器」  。</span><span class="sxs-lookup"><span data-stu-id="35114-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="35114-124">在 [摘要] 窗格中，找到 [主機名稱] 。</span><span class="sxs-lookup"><span data-stu-id="35114-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="35114-125">它類似 *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*。</span><span class="sxs-lookup"><span data-stu-id="35114-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="35114-126">**使用 SQLLine**</span><span class="sxs-lookup"><span data-stu-id="35114-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="35114-127">使用 SSH 連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="35114-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="35114-128">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="35114-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="35114-129">從 SSH，執行下列命令以執行 SQLLine：</span><span class="sxs-lookup"><span data-stu-id="35114-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="35114-130">執行下列命令來建立 HBase 資料表，並插入一些資料︰</span><span class="sxs-lookup"><span data-stu-id="35114-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="35114-131">如需詳細資訊，請參閱 [SQLLine 手冊](http://sqlline.sourceforge.net/#manual)和 [Phoenix 文法](http://phoenix.apache.org/language/index.html)。</span><span class="sxs-lookup"><span data-stu-id="35114-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="35114-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35114-132">Next steps</span></span>
<span data-ttu-id="35114-133">在本文中，您已經學會如何在 HDInsight 中使用 Apache Phoenix。</span><span class="sxs-lookup"><span data-stu-id="35114-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="35114-134">若要深入了解，請參閱：</span><span class="sxs-lookup"><span data-stu-id="35114-134">To learn more, see:</span></span>

* <span data-ttu-id="35114-135">[HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。</span><span class="sxs-lookup"><span data-stu-id="35114-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="35114-136">[在 Azure 虛擬網路上佈建 HBase 叢集][hdinsight-hbase-provision-vnet]：由於 HBase 叢集已與虛擬網路整合，因此能夠部署到和應用程式相同的虛擬網路，讓應用程式得以和 HBase 直接通訊。</span><span class="sxs-lookup"><span data-stu-id="35114-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="35114-137">[設定 HDInsight 中的 HBase 複寫](hdinsight-hbase-replication.md)：了解如何跨兩個 Azure 資料中心設定 HBase 複寫。</span><span class="sxs-lookup"><span data-stu-id="35114-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="35114-138">[利用 HDInsight 中的 HBase 分析 Twitter 情感][hbase-twitter-sentiment]：了解如何使用 HDInsight 之 Hadoop 叢集中的 HBase，執行巨量資料的即時[情感分析](http://en.wikipedia.org/wiki/Sentiment_analysis)。</span><span class="sxs-lookup"><span data-stu-id="35114-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
