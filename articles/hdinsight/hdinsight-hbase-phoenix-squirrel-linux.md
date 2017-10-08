---
title: "aaaUse Apache in Phoenix & 與 HBase-Azure HDInsight 松鼠 |Microsoft 文件"
description: "深入了解如何 toouse HDInsight 中的 Apache in Phoenix 以及 tooinstall 及設定松鼠 HDInsight 中您工作站 tooconnect tooan HBase 叢集。"
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
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="1e9aa-103">在 HDInsight 中搭配 Linux 型 HBase 叢集使用 Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="1e9aa-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="1e9aa-104">深入了解如何 toouse [Apache in Phoenix](http://phoenix.apache.org/)在 HDInsight，以及如何 toouse SQLLine。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="1e9aa-105">如需有關 Phoenix 的詳細資訊，請參閱 [15 分鐘內了解 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="1e9aa-106">Hello in Phoenix 文法，請參閱[in Phoenix 文法](http://phoenix.apache.org/language/index.html)。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="1e9aa-107">Hello in Phoenix HDInsight 中的版本資訊，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？](hdinsight-component-versioning.md)。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="1e9aa-108">使用 SQLLine</span><span class="sxs-lookup"><span data-stu-id="1e9aa-108">Use SQLLine</span></span>
<span data-ttu-id="1e9aa-109">[SQLLine](http://sqlline.sourceforge.net/)是命令列公用程式 tooexecute SQL。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1e9aa-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1e9aa-110">Prerequisites</span></span>
<span data-ttu-id="1e9aa-111">您可以使用 SQLLine 之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="1e9aa-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="1e9aa-112">**HDInsight 中的 HBase 叢集**。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="1e9aa-113">如需有關佈建 HBase 叢集的資訊，請參閱[開始使用 HDInsight 中的 Apache HBase][hdinsight-hbase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="1e9aa-114">**透過 hello 遠端桌面通訊協定 toohello HBase 叢集連線**。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="1e9aa-115">如需指示，請參閱[HDInsight 中使用的管理 Hadoop 叢集 hello Azure 入口網站][hdinsight-manage-portal]。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="1e9aa-116">當您連接 tooan HBase 叢集時，您需要 hello 動物園 tooconnect 的 tooone。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="1e9aa-117">每個 HDInsight 叢集有三個 Zookeeper。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="1e9aa-118">**toofind 出 hello 動物園管理員主機名稱**</span><span class="sxs-lookup"><span data-stu-id="1e9aa-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="1e9aa-119">開啟瀏覽過 Ambari**https://<ClusterName>。.azurehdinsight.net**。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="1e9aa-120">輸入 hello HTTP （叢集） 的使用者名稱和密碼 toologin。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="1e9aa-121">按一下**動物園管理員**hello 左側功能表中。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="1e9aa-122">您會看到列出三個「ZooKeeper 伺服器」。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="1e9aa-123">按一下其中一個 hello**動物園管理員伺服器**列出。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="1e9aa-124">在 hello 摘要窗格中，找出 hello **Hostname**。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="1e9aa-125">太類似*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="1e9aa-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="1e9aa-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="1e9aa-127">Toohello 叢集使用 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="1e9aa-128">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1e9aa-129">Ssh，執行下列命令 toorun SQLLine hello:</span><span class="sxs-lookup"><span data-stu-id="1e9aa-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="1e9aa-130">執行下列命令 toocreate hello HBase 資料表，並插入一些資料：</span><span class="sxs-lookup"><span data-stu-id="1e9aa-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="1e9aa-131">如需詳細資訊，請參閱 [SQLLine 手冊](http://sqlline.sourceforge.net/#manual)和 [Phoenix 文法](http://phoenix.apache.org/language/index.html)。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e9aa-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e9aa-132">Next steps</span></span>
<span data-ttu-id="1e9aa-133">在本文中，您已經學會如何 toouse Apache in Phoenix HDInsight 中。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="1e9aa-134">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="1e9aa-134">toolearn more, see:</span></span>

* <span data-ttu-id="1e9aa-135">[HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="1e9aa-136">[佈建 Azure 虛擬網路上的 HBase 叢集][hdinsight-hbase-provision-vnet]： 與虛擬網路整合 HBase 叢集可以部署的 toohello 相同虛擬網路與您的應用程式因此應用程式可以與通訊直接 HBase。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="1e9aa-137">[設定在 HDInsight HBase 複寫](hdinsight-hbase-replication.md)： 了解如何 tooconfigure HBase 複寫，跨兩個 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="1e9aa-138">[分析與在 HDInsight HBase Twitter 情緒][hbase-twitter-sentiment]： 了解如何 toodo 即時[情緒分析](http://en.wikipedia.org/wiki/Sentiment_analysis)的巨量資料在 HDInsight Hadoop 叢集中使用 HBase。</span><span class="sxs-lookup"><span data-stu-id="1e9aa-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
