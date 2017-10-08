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
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>在 HDInsight 中搭配 Linux 型 HBase 叢集使用 Apache Phoenix
深入了解如何 toouse [Apache in Phoenix](http://phoenix.apache.org/)在 HDInsight，以及如何 toouse SQLLine。 如需有關 Phoenix 的詳細資訊，請參閱 [15 分鐘內了解 Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)。 Hello in Phoenix 文法，請參閱[in Phoenix 文法](http://phoenix.apache.org/language/index.html)。

> [!NOTE]
> Hello in Phoenix HDInsight 中的版本資訊，請參閱[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？](hdinsight-component-versioning.md)。
>
>

## <a name="use-sqlline"></a>使用 SQLLine
[SQLLine](http://sqlline.sourceforge.net/)是命令列公用程式 tooexecute SQL。

### <a name="prerequisites"></a>必要條件
您可以使用 SQLLine 之前，您必須擁有 hello 下列：

* **HDInsight 中的 HBase 叢集**。 如需有關佈建 HBase 叢集的資訊，請參閱[開始使用 HDInsight 中的 Apache HBase][hdinsight-hbase-get-started]。
* **透過 hello 遠端桌面通訊協定 toohello HBase 叢集連線**。 如需指示，請參閱[HDInsight 中使用的管理 Hadoop 叢集 hello Azure 入口網站][hdinsight-manage-portal]。

當您連接 tooan HBase 叢集時，您需要 hello 動物園 tooconnect 的 tooone。 每個 HDInsight 叢集有三個 Zookeeper。

**toofind 出 hello 動物園管理員主機名稱**

1. 開啟瀏覽過 Ambari**https://<ClusterName>。.azurehdinsight.net**。
2. 輸入 hello HTTP （叢集） 的使用者名稱和密碼 toologin。
3. 按一下**動物園管理員**hello 左側功能表中。 您會看到列出三個「ZooKeeper 伺服器」。
4. 按一下其中一個 hello**動物園管理員伺服器**列出。 在 hello 摘要窗格中，找出 hello **Hostname**。 太類似*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*。

**toouse SQLLine**

1. Toohello 叢集使用 SSH 連線。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. Ssh，執行下列命令 toorun SQLLine hello:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. 執行下列命令 toocreate hello HBase 資料表，並插入一些資料：

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

如需詳細資訊，請參閱 [SQLLine 手冊](http://sqlline.sourceforge.net/#manual)和 [Phoenix 文法](http://phoenix.apache.org/language/index.html)。

## <a name="next-steps"></a>後續步驟
在本文中，您已經學會如何 toouse Apache in Phoenix HDInsight 中。  toolearn 詳細資訊，請參閱：

* [HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。
* [佈建 Azure 虛擬網路上的 HBase 叢集][hdinsight-hbase-provision-vnet]： 與虛擬網路整合 HBase 叢集可以部署的 toohello 相同虛擬網路與您的應用程式因此應用程式可以與通訊直接 HBase。
* [設定在 HDInsight HBase 複寫](hdinsight-hbase-replication.md)： 了解如何 tooconfigure HBase 複寫，跨兩個 Azure 資料中心。
* [分析與在 HDInsight HBase Twitter 情緒][hbase-twitter-sentiment]： 了解如何 toodo 即時[情緒分析](http://en.wikipedia.org/wiki/Sentiment_analysis)的巨量資料在 HDInsight Hadoop 叢集中使用 HBase。

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
