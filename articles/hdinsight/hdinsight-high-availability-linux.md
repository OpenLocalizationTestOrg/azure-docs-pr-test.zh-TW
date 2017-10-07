---
title: "Hadoop-Azure HDInsight 的 aaaHigh 可用性 |Microsoft 文件"
description: "了解如何使用額外的前端節點，讓 HDInsight 叢集可以提高可靠性和可用性。 了解如何影響 Hadoop 服務，例如 Ambari 和 Hive，以及如何 tooindividually 連接使用 SSH tooeach 前端節點。"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "hadoop 高可用性"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>HDInsight 上 Hadoop 叢集的可用性和可靠性

HDInsight 叢集提供兩個前端節點 tooincrease hello 可用性和可靠性的 Hadoop 服務及執行的工作。

Hadoop 藉由在叢集中的多個節點間複寫服務和資料，以達到高可用性和可靠性。 不過 Hadoop 的標準散佈功能通常只能有一個前端節點。 Hello 單一前端節點的任何中斷可能會導致 hello 叢集 toostop 工作。 HDInsight 提供兩個 headnodes tooimprove Hadoop 的可用性和可靠性。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="availability-and-reliability-of-nodes"></a>節點的可用性和可靠性

使用 Azure 虛擬機器在 HDInsight 叢集中的節點實作。 hello 下列各節討論 hello HDInsight 搭配使用的個別節點型別。 

> [!NOTE]
> 並非所有的節點類型都可用於某個叢集類型。 例如，Hadoop 叢集類型就不會有任何 Nimbus 節點。 如需有關節點 HDInsight 叢集類型所使用的詳細資訊，請參閱 hello 叢集類型 > 一節的 hello [HDInsight 叢集建立 Linux Hadoop](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)文件。

### <a name="head-nodes"></a>前端節點

tooensure 高可用性的 Hadoop 服務，HDInsight 提供兩個前端節點。 這兩個前端節點會同時為作用中和 hello HDInsight 叢集內執行。 某些服務，例如 HDFS 或 YARN，在任何給定的時間僅能在其中一個前端節點上為「作用中」。 例如 HiveServer2 或 Hive 中繼存放區的其他服務為 hello 在兩個前端節點上使用相同的時間。

前端節點 （和 HDInsight 中的其他節點） 有數值的 hello 節點的 hello 主機名稱的一部分。 例如，`hn0-CLUSTERNAME` 或 `hn4-CLUSTERNAME`。

> [!IMPORTANT]
> 請勿將 hello 數值關聯具有一個節點是主要或次要。 hello 數值為存在 tooprovide 每個節點的唯一名稱。

### <a name="nimbus-nodes"></a>Nimbus 節點

Nimbus 節點可用於 Storm 叢集。 hello Nimbus 節點會提供類似功能 toohello Hadoop JobTracker 散發，並監視背景工作節點之間的處理。 HDInsight 為 Storm 叢集提供兩個 Nimbus 節點

### <a name="zookeeper-nodes"></a>Zookeeper 節點

[ZooKeeper](http://zookeeper.apache.org/) 節點用於前端節點上主要服務的前置選擇。 它們也是使用的 tooinsure 服務、 資料 （背景工作角色） 節點，以及閘道知道哪些主要服務為作用中的前端節點。 根據預設，HDInsight 會提供三個 ZooKeeper 節點。

### <a name="worker-nodes"></a>背景工作節點

背景工作節點執行 hello 實際的資料分析工作時送出的 toohello 叢集。 如果背景工作節點失敗，它的執行狀況的 hello 工作都是送出的 tooanother 背景工作節點。 根據預設，HDInsight 會建立四個背景工作節點。 在和建立叢集之後您可以變更指定這個數字 toosuit 您的需求。

### <a name="edge-node"></a>邊緣節點

邊緣節點不會主動參與 hello 叢集內的資料分析。 而是由開發人員或資料科學家在使用 Hadoop 時搭配使用。 中的 hello 邊緣節點生活 hello 與 hello 相同 Azure 虛擬網路 hello 叢集中的其他節點，並可以直接存取所有其他節點。 可以使用 hello 邊緣節點，而不離開關鍵 Hadoop 服務或分析工作的資源。

目前，HDInsight 上的 R 伺服器是 hello 唯一叢集類型，根據預設，提供邊緣節點。 HDInsight 上的 R 伺服器，會使用 hello 邊緣節點本機上進行分散式處理 toohello 叢集送出之前 hello 節點測試 R 程式碼。

如需使用 R 伺服器以外的叢集類型的邊緣節點資訊，請參閱 hello[使用 HDInsight 中邊緣節點](hdinsight-apps-use-edge-node.md)文件。

## <a name="accessing-hello-nodes"></a>存取 hello 節點

存取 toohello 叢集 hello 透過網際網路提供透過公用閘道。 存取限制的 tooconnecting toohello 前端節點，而且 （如果有的話） hello 邊緣節點。 存取 tooservices hello 前端節點上執行不受到具有多個前端節點。 hello 公用閘道路由要求 toohello 前端節點裝載 hello 要求的服務。 例如，如果 Ambari 目前 hello 次要前端節點上裝載，hello 閘道會路由傳送 Ambari toothat 節點內送要求。

443 (HTTPS)、 22 和 23 的有限的 tooport hello 公用閘道上的存取。

* 連接埠__443__是使用的 tooaccess Ambari 和其他 web UI 或 hello 前端節點上裝載的 REST Api。

* 連接埠__22__使用的 tooaccess hello 的主要前端節點或透過 SSH 的邊緣節點。

* 連接埠__23__是使用的 tooaccess hello 次要前端節點使用 SSH。 例如，`ssh username@mycluster-ssh.azurehdinsight.net`連接 toohello 主要叢集前端節點 hello 名為**mycluster**。

如需有關如何使用 SSH 的詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。

### <a name="internal-fully-qualified-domain-names-fqdn"></a>內部完整網域名稱 (FQDN)

HDInsight 叢集中的節點都有內部 IP 位址及只能存取從 hello 叢集的 FQDN。 當存取使用 hello 內部 FQDN 或 IP 位址的 hello 叢集上的服務，您應該使用 Ambari tooverify hello IP 或 FQDN toouse 存取 hello 服務時發生。

例如，hello 的 Oozie 服務只能執行一個前端節點，並使用 hello`oozie`從的 SSH 工作階段的命令需要 hello URL toohello 服務。 可以使用下列命令的 hello，從 Ambari 擷取此 URL:

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

此命令會傳回下列命令，其中包含以 hello hello 內部 URL toouse 值類似 toohello`oozie`命令：

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

如需使用 hello Ambari REST API 的詳細資訊，請參閱[監視和管理 HDInsight 的使用 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md)。

### <a name="accessing-other-node-types"></a>存取其他節點類型

您可以連接都無法直接存取 over hello 網際網路使用下列方法 hello 的 toonodes:

* **SSH**： 一旦連接 tooa 前端節點使用 SSH，然後您可以使用 SSH 從 hello 前端節點 tooconnect tooother hello 叢集中的節點。 如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。

* **SSH 通道**： 如果您需要的 tooaccess 裝載的 web 服務的其中一個 hello 節點不是公開 toohello 網際網路，您必須使用 SSH 通道。 如需詳細資訊，請參閱 hello [HDInsight 搭配使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)文件。

* **Azure 虛擬網路**： 如果您的 HDInsight 叢集的 Azure 虛擬網路上的任何資源屬於 hello 相同虛擬網路可直接存取 hello 叢集中所有節點。 如需詳細資訊，請參閱 hello[使用 Azure 虛擬網路的延伸 HDInsight](hdinsight-extend-hadoop-virtual-network.md)文件。

## <a name="how-toocheck-on-a-service-status"></a>如何 toocheck 服務狀態

toocheck hello 的 hello 前端節點上執行，請使用 hello Ambari Web UI 或 hello Ambari REST API 服務的狀態。

### <a name="ambari-web-ui"></a>Ambari Web UI

hello Ambari Web UI 是可在 https://CLUSTERNAME.azurehdinsight.net 檢視。 取代**CLUSTERNAME**與 hello 叢集的名稱。 如果出現提示，請輸入您的叢集 hello HTTP 使用者認證。 hello 預設 HTTP 使用者名稱是**admin** hello 密碼為 hello 建立 hello 叢集時所輸入的密碼。

當您來到 hello Ambari 頁面上時，安裝 hello 服務會列在 hello hello 頁面左邊。

![已安裝的服務](./media/hdinsight-high-availability-linux/services.png)

有一系列可能會出現 下一步 tooa 服務 tooindicate 狀態的圖示。 可以使用 hello 檢視 tooa 服務相關的任何警示**警示**hello hello 頁頂端的連結。 您可以選取每個服務 tooview 詳細資訊。

雖然 hello 服務 頁面會提供資訊 hello 狀態和組態的每個服務，它不提供前端節點 hello 服務執行的所在資訊。 tooview 此資訊、 使用 hello**主機**hello hello 頁頂端的連結。 此頁面會顯示 hello 叢集，包括 hello 前端節點內的主機。

![主機清單](./media/hdinsight-high-availability-linux/hosts.png)

選取 hello 連結的其中一個 hello 前端節點會顯示 hello 服務與該節點上執行的元件。

![元件狀態](./media/hdinsight-high-availability-linux/nodeservices.png)

如需有關使用 Ambari 的詳細資訊，請參閱[監視和管理 HDInsight 使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)。

### <a name="ambari-rest-api"></a>Ambari REST API

hello Ambari REST API 是透過 hello 網際網路。 hello HDInsight 公用閘道處理路由要求 toohello 前端節點目前裝載 hello REST API。

您可以使用下列命令 toocheck hello 狀態 hello Ambari REST API 服務的 hello:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* 取代**密碼**與 hello HTTP 使用者 （管理員） 帳戶的密碼。
* 取代**CLUSTERNAME** hello hello 叢集名稱。
* 取代**SERVICENAME** hello hello 服務名稱與您想 toocheck hello 狀態。

例如，toocheck hello 狀態 hello **HDFS**上名為叢集的服務**mycluster**，密碼是**密碼**，您會使用下列命令的 hello:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

hello 回應是類似 toohello 下列 JSON:

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

hello URL 告訴我們 hello 服務目前在名為前端節點上執行**hn0 CLUSTERNAME**。

hello 狀態告訴我們，目前執行 hello 服務，或**已啟動**。

如果您不知道 hello 叢集上安裝了哪些服務，您可以使用下列命令 tooretrieve 清單 hello:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

如需使用 hello Ambari REST API 的詳細資訊，請參閱[監視和管理 HDInsight 的使用 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md)。

#### <a name="service-components"></a>服務元件

服務可能包含您想 toocheck hello 狀態的個別的元件。 例如，HDFS 包含 hello NameNode 元件。 在元件上的 tooview 資訊，hello 命令會是：

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

如果您不知道哪些元件所提供的服務，您可以使用下列命令 tooretrieve 清單 hello:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>如何 tooaccess 登 hello 前端節點上的檔案

### <a name="ssh"></a>SSH

透過 SSH 連線的 tooa 前端節點，而記錄檔可以找到下**/var/記錄**。 例如， **/var/log/hadoop-yarn/yarn** 包含 YARN 的記錄檔。

每個前端節點可以有唯一的記錄項目，所以您應該檢查 hello 登入同時。

### <a name="sftp"></a>SFTP

您也可以連接 toohello hello SSH 檔案傳輸通訊協定或安全檔案傳輸通訊協定 (SFTP) 所使用的前端節點，並直接下載 hello 的記錄檔。

類似 toousing 連接必須提供 toohello 叢集時將 SSH 用戶端 hello SSH 使用者帳戶名稱和 hello SSH hello 叢集位址。 例如： `sftp username@mycluster-ssh.azurehdinsight.net`。 Hello 帳戶出現提示時，提供 hello 密碼或提供的公開公鑰使用 hello`-i`參數。

連線之後，您會看到 `sftp>` 提示。 您可以從該提示變更目錄、上傳和下載檔案。 例如，下列命令的 hello 變更目錄 toohello **/var/log/hadoop/hdfs**目錄，然後再下載 hello 目錄中的所有檔案。

    cd /var/log/hadoop/hdfs
    get *

如需可用命令的清單，請輸入`help`在 hello`sftp>`提示字元。

> [!NOTE]
> 另外還有 toovisualize hello 檔案系統時使用 SFTP 連接可讓您的圖形化介面。 例如， [MobaXTerm](http://mobaxterm.mobatek.net/)可讓您使用介面類似 tooWindows 總管 toobrowse hello 檔案系統。

### <a name="ambari"></a>Ambari

> [!NOTE]
> tooaccess 記錄檔使用 Ambari，您必須使用 SSH 通道。 公開 hello 網際網路上不公開 hello hello 個別服務的 web 介面。 如需使用 SSH 通道的資訊，請參閱 hello[使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)文件。

從 hello Ambari Web UI 中，選取您希望 tooview 記錄檔 (例如，YARN) hello 服務。 然後使用**快速連結**tooselect 的前端節點 tooview hello 記錄檔。

![使用快速連結 tooview 記錄檔](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Tooconfigure hello 節點大小的方式

只可以在叢集建立期間選取節點的 hello 大小。 您可以找到 hello 一份可用的不同 VM 大小 HDInsight 上 hello [HDInsight 定價頁面](https://azure.microsoft.com/pricing/details/hdinsight/)。

在建立叢集時，您可以指定 hello hello 節點大小。 hello 下列資訊提供指引如何 toospecify hello 大小使用 hello [Azure 入口網站][preview-portal]， [Azure PowerShell][azure-powershell]，和 hello [Azure CLI][azure-cli]:

* **Azure 入口網站**： 在建立叢集時，您可以設定的 hello 節點 hello 叢集所用的 hello 大小：

    ![可選取節點大小的 [叢集映像建立精靈]](./media/hdinsight-high-availability-linux/headnodesize.png)

* **Azure CLI**： 當使用 hello`azure hdinsight cluster create`命令時，您可以設定 hello 大小 hello head、 背景工作，以及動物園管理員節點使用 hello `--headNodeSize`， `--workerNodeSize`，和`--zookeeperNodeSize`參數。

* **Azure PowerShell**： 當使用 hello `New-AzureRmHDInsightCluster` cmdlet，您可以設定 hello 大小 hello head、 背景工作，以及動物園管理員節點使用 hello `-HeadNodeVMSize`， `-WorkerNodeSize`，和`-ZookeeperNodeSize`參數。

## <a name="next-steps"></a>後續步驟

使用下列連結 toolearn 更多關於此文件中所述的項目 hello。

* [Ambari REST 參考](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [安裝和設定 hello Azure CLI](../cli-install-nodejs.md)
* [安裝並設定 Azure PowerShell](/powershell/azure/overview)
* [使用 Ambari 管理 HDInsight](hdinsight-hadoop-manage-ambari.md)
* [佈建以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
