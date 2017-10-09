---
title: "虛擬網路-Azure 內 aaaConfigure HBase 叢集複寫 |Microsoft 文件"
description: "深入了解如何 tooconfigure HBase 複寫負載平衡，高可用性、 零停機時間移轉/更新從一個 HDInsight 版本 tooanother 和災害復原。"
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a>設定虛擬網路中的 HBase 叢集複寫

深入了解如何 tooconfigure HBase 複寫一個虛擬網路 (VNet) 內，或兩個虛擬網路之間。

叢集複寫會使用來源推入方法。 HBase 叢集可以是來源、目的地，或可同時滿足兩個角色。 複寫是非同步的並複寫 hello 目標是最終一致性。 Hello 來源收到編輯 tooa 資料欄系列已啟用複寫時，編輯時傳播的 tooall 目的地叢集。 當資料從一個叢集 tooanother 複寫時，hello 來源叢集與所有已用完 hello 資料的叢集是追蹤的 tooprevent 複寫迴圈。

在本教學課程中，您將設定來源目的地複寫。 若需其他叢集拓撲，請參閱 [Apache HBase 參考指南](http://hbase.apache.org/book.html#_cluster_replication)。

適用於單一虛擬網路的 HBase 複寫使用案例︰

* 負載平衡-例如，在 hello 目的地叢集上執行掃描或 MapReduce 工作和擷取 hello 來源叢集上的資料
* 高可用性
* 從一個 HBase 叢集 tooanother 移轉資料
* 從一個版本 tooanother 升級 Azure HDInsight 叢集

適用於兩個虛擬網路的 HBase 複寫使用案例︰

* 災害復原
* 負載平衡和資料分割 hello 應用程式
* 高可用性

您會使用位於 [GitHub (英文)](https://github.com/Azure/hbase-utils/tree/master/replication) 的[指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)指令碼複寫叢集。

## <a name="prerequisites"></a>必要條件
開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

## <a name="configure-hello-environments"></a>設定 hello 環境

有三個可能的設定︰

- 有兩個 HBase 叢集位於單一 Azure 虛擬網路中
- 兩個不同的虛擬網路中的兩個 HBase 叢集 hello 相同的區域
- 有兩個 HBase 叢集位於不同區域且不同的兩個虛擬網路中 (異地複寫)

toomake 它更容易 tooconfigure hello 環境中，我們建立了一些[Azure 資源管理員範本](../azure-resource-manager/resource-group-overview.md)。 如果您偏好 tooconfigure hello 環境使用其他方法，請參閱：

- [在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)
- [在 Azure 虛擬網路上建立 HBase 叢集](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a>設定一個虛擬網路

按一下下列映像 toocreate 兩個 HBase 叢集在 hello hello 相同虛擬網路。 hello 範本會儲存在[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/)。

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a>在 hello 中設定兩個虛擬網路相同的區域

按一下 hello 下列映像 toocreate 兩個虛擬網路與對等互連的 VNet 中 hello 的兩個 HBase 叢集相同的區域。 hello 範本會儲存在[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/)。

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



此案例需要 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。 hello 範本可讓對等互連的 VNet。   

對 HBase 複寫會使用 hello 動物園管理員 Vm 的 IP 位址。 您必須設定為 hello 目的地 HBase 動物園管理員節點的靜態 IP 位址。

**tooconfigure 靜態 IP 位址**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 從 hello 左窗格中，按一下 **資源群組**。
3. 按一下您的資源群組，其中包含 hello 目的地 HBase 叢集。 這是您指定當您使用 hello 資源管理員範本 toocreate hello 環境的 hello 資源群組。 您可以使用 hello 篩選 toonarrow hello 清單中。 您可以看到包含 hello 兩個虛擬網路資源的清單。
4. 按一下 hello 包含 hello 目的地 HBase 叢集的虛擬網路。 例如，按一下 [xxxx-vnet2]。 您可以看到名稱開頭為 **nic-zookeepermode-** 的三個裝置。 這些裝置是 hello 三動物園管理員 Vm。
5. 按一下其中一個 hello 動物園管理員 Vm。
6. 按一下 [IP 組態]。
7. 按一下**ipConfig1**從 hello 清單。
8. 按一下**靜態**，記下 hello 實際 IP 位址。 當您執行 hello 指令碼動作 tooenable 複寫時，您將需要 hello IP 位址。

  ![HDInsight HBase 複寫 ZooKeeper 靜態 IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. 針對 hello 其他兩個動物園管理員節點重複步驟 6 tooset hello 靜態 IP 位址。

Hello 跨 VNet 案例中，您必須使用 hello **ip**時呼叫 hello 切換**hdi_enable_replication.sh**指令碼動作。

### <a name="configure-two-virtual-networks-in-two-different-regions"></a>在兩個不同區域中設定兩個虛擬網路

按一下下列映像 toocreate 兩個虛擬網路在兩個不同區域中的 hello。 hello 範本會儲存在公用 Azure Blob 容器。

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

建立 hello 兩個虛擬網路之間的 VPN 閘道。 如需指示，請參閱[建立具有站對站連線的 VNet](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)。

對 HBase 複寫會使用 hello 動物園管理員 Vm 的 IP 位址。 您必須設定為 hello 目的地 HBase 動物園管理員節點的靜態 IP 位址。 tooconfigure 靜態 IP，請參閱本文中的 hello"中的設定兩個虛擬網路 hello 相同區域 」 一節。

Hello 跨 VNet 案例中，您必須使用 hello **ip**時呼叫 hello 切換**hdi_enable_replication.sh**指令碼動作。

## <a name="load-test-data"></a>載入測試資料

當您複製的叢集時，您必須指定 hello 資料表 tooreplicate。 在本節中，您會將一些資料載入 hello 來源叢集。 在 hello 下一步 區段中，您將啟用 hello 兩個叢集之間的複寫。

請依照下列中的 hello 指示[HBase 教學課程： 開始 linux HDInsight 中的 Hadoop 使用 Apache HBase](hdinsight-hbase-tutorial-get-started-linux.md) toocreate**連絡人**資料表，並將某些資料插入 hello 資料表。

## <a name="enable-replication"></a>啟用複寫

hello 下列步驟顯示如何 toocall hello hello Azure 入口網站從指令碼動作指令碼。 使用 Azure PowerShell 及 hello Azure 命令列介面 (CLI) 執行指令碼動作，請參閱[使用指令碼動作以自訂 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

**從 Azure 入口網站 hello tooenable HBase 複寫**

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 開啟 hello 來源 HBase 叢集。
3. 從 hello 叢集功能表上，按一下 **指令碼動作**。
4. 按一下**提交新**從 hello hello 刀鋒視窗的頂端。
5. 選取或輸入 hello 下列資訊：

  - **名稱**：輸入「啟用複寫」。
  - **Bash 指令碼 URL**：輸入 **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**。
  - **前端**︰已選取。 清除 hello 其他節點型別。
  - **參數**: hello 下列範例參數啟用所有 hello 現有資料表的複寫，並且所有的 hello 資料複製 hello 來源叢集 toohello 目的地叢集：

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. 按一下 [建立] 。 hello 指令碼可能需要一些時間，特別是當 hello-copydata 引數用。

必要的引數︰

|名稱|說明|
|----|-----------|
|-s, --src-cluster | 指定 hello hello 來源 HBase 叢集 DNS 名稱。 例如：-s hbsrccluster, --src-cluster=hbsrccluster |
|-d, --dst-cluster | 指定 hello hello 目的地 （複本） HBase 叢集 DNS 名稱。 例如：-s dsthbcluster, --src-cluster=dsthbcluster |
|-sp, --src-ambari-password | 指定在 hello 來源 HBase 叢集 Ambari hello 系統管理員密碼。 |
|-dp, --dst-ambari-password | 指定在 hello 目的地 HBase 叢集上 Ambari hello 系統管理員密碼。|

選擇性的引數︰

|名稱|說明|
|----|-----------|
|-su, --src-ambari-user | 指定在 hello 來源 HBase 叢集 Ambari hello 管理員使用者名稱。 hello 預設值是**admin**。 |
|-du, --dst-ambari-user | 指定在 hello 目的地 HBase 叢集上 Ambari hello 管理員使用者名稱。 hello 預設值是**admin**。 |
|-t, --table-list | 指定 hello 資料表 toobe 複寫。 例如：--table-list="table1;table2;table3"。 如果您未指定資料表，則會複寫所有現有的 HBase 資料表。|
|-m, --machine | 指定 hello hello 指令碼動作執行所在的前端節點。 hn1 或 hn0 hello 值。 由於 hn0 通常較忙碌，建議您使用 hn1。 如果您從 hello HDInsight 入口網站或 Azure PowerShell 指令碼動作執行 hello $0 指令碼，您可以使用此選項。|
|-ip | 當您啟用兩個虛擬網路之間的複寫時，需要這個引數。 這個引數做為參數 toouse hello 靜態 Ip 的動物園管理員來自叢集的節點複本而不是 FQDN 名稱。 hello 靜態 Ip 需要 toobe 預先設定的啟用複寫之前。 |
|-cp, -copydata | 啟用 hello hello 已啟用複寫的資料表上的現有資料移轉的功能。 |
|-rpm, -replicate-phoenix-meta | 在 Phoenix 系統資料表上啟用複寫。 <br><br>*請謹慎使用此選項。* 建議您在使用此指令碼前，於複本叢集上重新建立 Phoenix 資料表。 |
|-h, --help | 顯示使用資訊。 |

hello hello print_usage() 區段[指令碼](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh)提供參數的詳細的說明。

Hello 指令碼動作是成功之後部署，您可以使用 SSH tooconnect toohello 目的地 HBase 叢集，並確認已複寫 hello 資料。

### <a name="replication-scenarios"></a>複寫案例

hello 下列清單顯示一些一般使用案例和其參數設定：

- **Hello 兩個叢集之間的所有資料表上啟用複寫**。 此案例不需要 hello 複製/hello 資料表上的現有資料移轉，而且不會使用 in Phoenix 資料表。 使用下列參數的 hello:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- **在特定資料表上啟用複寫**。 使用下列參數 tooenable 複寫 table1、 table2 和 table3 hello:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- **特定資料表上啟用複寫，而且複製 hello 現有資料**。 使用下列參數 tooenable 複寫 table1、 table2 和 table3 hello:

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- **與從來源 toodestination 複寫 in phoenix 中繼資料的所有資料表上啟用複寫**。 Phoenix 中繼資料複寫並不完美，應謹慎啟用。

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a>複製並移轉資料

啟用複寫後，有兩個用來複製/移轉資料的個別指令碼動作指令碼：

- [用於小型資料表的指令碼](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh)（在大小和整體複製數 gb 是預期的 toofinish 中少於一小時）

- [對於大型資料表的指令碼](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh)（預期 tootake 超過一小時 toocopy）

您可以遵循相同的程序中的 hello[啟用複寫](#enable-replication)toocall hello 指令碼動作以 hello 下列參數：

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

hello hello print_usage() 區段[指令碼](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh)提供參數的詳細的描述。

### <a name="scenarios"></a>案例

- **針對到目前為止 (目前時間戳記) 所有已編輯的資料列複製特定資料表 (test1、test2 和 test3)**：

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  或

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- **以指定時間範圍複製特定資料表**：

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a>停用複寫

使用位於另一個指令碼動作指令碼 toodisable 複寫[GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh)。 您可以遵循相同的程序中的 hello[啟用複寫](#enable-replication)toocall hello 指令碼動作以 hello 下列參數：

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

hello hello print_usage() 區段[指令碼](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh)提供參數的詳細的說明。

### <a name="scenarios"></a>案例

- **停用所有資料表上的複寫**：

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  或

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- **停用特定資料表 (table1、table2 和 table3) 上的複寫**：

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a>後續步驟

在本教學課程中，您學到如何 tooconfigure HBase 複寫，跨兩個資料中心。 toolearn 深入了解 HDInsight 和 HBase，請參閱：

* [開始使用 HDInsight 中的 Apache HBase][hdinsight-hbase-get-started]
* [HDInsight HBase 概觀][hdinsight-hbase-overview]
* [在 Azure 虛擬網路上建立 HBase 叢集][hdinsight-hbase-provision-vnet]
* [使用 HBase 分析即時 Twitter 情緒][hdinsight-hbase-twitter-sentiment]
* [在 HDInsight (Hadoop) 中使用 Storm 和 HBase 分析感應器資料][hdinsight-sensor-data]

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
